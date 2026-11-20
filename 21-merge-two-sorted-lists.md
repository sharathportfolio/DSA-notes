# 21. Merge Two Sorted Lists

**LeetCode:** https://leetcode.com/problems/merge-two-sorted-lists/\
**Difficulty:** Easy\
**Pattern:** Two Pointers + Dummy Node\
**Data Structure:** Singly Linked List

## 1. Problem

Merge two sorted singly linked lists into one sorted linked list by
reusing their nodes. Return the head of the merged list.

## 2. Input

-   `list1`: head of the first sorted linked list
-   `list2`: head of the second sorted linked list
-   LeetCode supplies linked-list **head nodes**, not JavaScript arrays
    or custom list-wrapper objects.

Example:

``` text
list1 = 1 -> 2 -> 4 -> null
list2 = 1 -> 3 -> 4 -> null
```

## 3. Output

Return the head node of the merged sorted list.

``` text
1 -> 1 -> 2 -> 3 -> 4 -> 4 -> null
```

LeetCode displays this as `[1,1,2,3,4,4]`, but the function must return
a **node**, not an array.

## 4. Edge Cases and Constraints

**Edge cases** - Both lists empty: `[]`, `[]` → `[]` - One list empty:
`[]`, `[0]` → `[0]` - Duplicate values: `[1,1]`, `[1]` → `[1,1,1]` -
Negative values: `[-3,-1]`, `[-2]` → `[-3,-2,-1]` - Different lengths

**Constraints** - Each list has 0--50 nodes. - Node values range from
-100 to 100. - Both lists are sorted in non-decreasing order.

## 5. Data Structure and Algorithm

**DS:** Singly Linked List\
**Algorithm:** Two Pointers + Dummy Node

**Rough approach** 1. Create a dummy node and set `curr = dummy`. 2. Set
`p1` and `p2` to the input heads. 3. While both pointers exist, compare
their values. 4. Attach the smaller node to `curr.next`. 5. Advance the
pointer whose node was attached. 6. Advance `curr`. 7. Attach the
remaining chain when one list ends. 8. Return `dummy.next`.

## 6. Time and Space Complexity

Let `n` and `m` be the lengths of the two lists.

-   **Time:** `O(n + m)` --- each node is processed at most once.
-   **Auxiliary space:** `O(1)` --- one dummy node and a constant number
    of pointers.
-   Converting the result to an array for local display takes `O(n + m)`
    extra space.

------------------------------------------------------------------------

## 7. JavaScript --- LeetCode Version

Paste this function into LeetCode's JavaScript editor. LeetCode provides
`ListNode`.

``` javascript
/**
 * Definition for singly-linked list.
 * function ListNode(val, next) {
 *   this.val = (val === undefined ? 0 : val);
 *   this.next = (next === undefined ? null : next);
 * }
 *
 * @param {ListNode} list1
 * @param {ListNode} list2
 * @return {ListNode}
 */
var mergeTwoLists = function(list1, list2) {
  // Step 1: Dummy node
  let dummy = new ListNode(0);
  let curr = dummy;

  // Step 2: Two pointers
  let p1 = list1;
  let p2 = list2;

  // Step 3: Compare and attach
  while (p1 && p2) {
    if (p1.val <= p2.val) {
      curr.next = p1;
      p1 = p1.next;
    } else {
      curr.next = p2;
      p2 = p2.next;
    }
    curr = curr.next;
  }

  // Step 4: Attach remaining nodes
  curr.next = p1 || p2;

  // Step 5: Return merged head
  return dummy.next;
};
```

**Explanation:** `val` is the property on LeetCode nodes. Inputs are
already head nodes, so do not use `list1.head`. Return `dummy.next`, not
an array.

------------------------------------------------------------------------

## 8. JavaScript --- Custom Node and LinkedList (Local Practice)

This version retains `Node`, `LinkedList`, `push()`, `toArray()`, and
`static mergeTwoLists()`.

``` javascript
class Node {
  constructor(value) {
    this.value = value;
    this.next = null;
  }
}

class LinkedList {
  constructor(value) {
    this.head = null;
    this.tail = null;
    this.length = 0;

    // Supports empty linked lists
    if (value !== undefined) {
      this.push(value);
    }
  }

  push(value) {
    const newNode = new Node(value);

    if (!this.head) {
      this.head = newNode;
      this.tail = newNode;
    } else {
      this.tail.next = newNode;
      this.tail = newNode;
    }

    this.length++;
    return this;
  }

  static toArray(head) {
    let result = [];
    let curr = head;

    while (curr) {
      result.push(curr.value);
      curr = curr.next;
    }

    return result;
  }

  static mergeTwoLists(list1, list2) {
    // Step 1: Dummy node
    let dummy = new Node(0);
    let curr = dummy;

    // Step 2: Start from custom list heads
    let p1 = list1.head;
    let p2 = list2.head;

    // Step 3: Compare and attach
    while (p1 && p2) {
      if (p1.value <= p2.value) {
        curr.next = p1;
        p1 = p1.next;
      } else {
        curr.next = p2;
        p2 = p2.next;
      }
      curr = curr.next;
    }

    // Step 4: Attach remaining nodes
    curr.next = p1 || p2;

    // Step 5: Return head, not array
    return dummy.next;
  }
}

// Create first linked list
let list1 = new LinkedList(1);
list1.push(2);
list1.push(4);

// Create second linked list
let list2 = new LinkedList(1);
list2.push(3);
list2.push(4);

// Merge
let mergedHead = LinkedList.mergeTwoLists(list1, list2);

// Display result as an array (local testing only)
console.log(LinkedList.toArray(mergedHead));
// [1, 1, 2, 3, 4, 4]
```

**Explanation** - Custom nodes use `value`, while LeetCode nodes use
`val`. - Custom list instances have `.head`; LeetCode passes the head
node directly. - `mergeTwoLists()` returns the merged head; `toArray()`
is only for displaying it. - The merge **relinks the original nodes**.
After merging, the original list objects may have stale `tail` and
`length` metadata. Do not treat them as unchanged independent lists. -
`static` means the method is called as
`LinkedList.mergeTwoLists(list1, list2)`.

------------------------------------------------------------------------

## 9. TypeScript --- LeetCode Version

LeetCode supplies the `ListNode` class.

``` typescript
/**
 * Definition for singly-linked list.
 * class ListNode {
 *   val: number;
 *   next: ListNode | null;
 *
 *   constructor(val?: number, next?: ListNode | null) {
 *     this.val = (val === undefined ? 0 : val);
 *     this.next = (next === undefined ? null : next);
 *   }
 * }
 */

function mergeTwoLists(
  list1: ListNode | null,
  list2: ListNode | null
): ListNode | null {
  // Step 1: Dummy node
  const dummy = new ListNode(0);
  let curr: ListNode = dummy;

  // Step 2: Two pointers
  let p1: ListNode | null = list1;
  let p2: ListNode | null = list2;

  // Step 3: Compare and attach
  while (p1 !== null && p2 !== null) {
    if (p1.val <= p2.val) {
      curr.next = p1;
      p1 = p1.next;
    } else {
      curr.next = p2;
      p2 = p2.next;
    }

    curr = curr.next!;
  }

  // Step 4: Attach remaining nodes
  curr.next = p1 ?? p2;

  // Step 5: Return merged head
  return dummy.next;
}
```

**Explanation** - `ListNode | null` means the pointer can hold a node or
`null`. - `curr.next!` asserts the next node is non-null after we attach
it. - `p1 ?? p2` chooses whichever remaining pointer is not null. -
Algorithm and complexity are unchanged from JavaScript.

------------------------------------------------------------------------

## 10. Python --- LeetCode Version

LeetCode supplies `ListNode` and the `Optional` typing support.

``` python
# Definition for singly-linked list.
# class ListNode:
#     def __init__(self, val=0, next=None):
#         self.val = val
#         self.next = next

class Solution:
    def mergeTwoLists(
        self,
        list1: Optional[ListNode],
        list2: Optional[ListNode]
    ) -> Optional[ListNode]:
        # Step 1: Dummy node
        dummy = ListNode(0)
        curr = dummy

        # Step 2: Two pointers
        p1 = list1
        p2 = list2

        # Step 3: Compare and attach
        while p1 and p2:
            if p1.val <= p2.val:
                curr.next = p1
                p1 = p1.next
            else:
                curr.next = p2
                p2 = p2.next

            curr = curr.next

        # Step 4: Attach remaining nodes
        curr.next = p1 or p2

        # Step 5: Return merged head
        return dummy.next
```

**Explanation** - Python uses `and` instead of `&&`. - Python uses `or`
instead of `||`. - Python indentation replaces braces. - The `Solution`
class and `mergeTwoLists` method match LeetCode's Python interface.

------------------------------------------------------------------------


## 11. Test Cases

  | Case | list1 | list2 | Expected |
  | --- | --- | --- | --- |
  | Normal |  `[1,2,4]` | `[1,3,4]` | `[1,1,2,3,4,4]`|
  | Both empty |    `[]`    |      `[]`    |     `[]` |
  | First empty  | `[]`    |      `[0]`   |     `[0]` |
  |Second empty |  `[1,2]`   |    `[]`    |     `[1,2]` |
  | Negatives    |  `[-3,-1,2]` |  `[-2,0,3]` |   `[-3,-2,-1,0,2,3]`|
  | Duplicates   |  `[1,1,2]` |    `[1,2,2]` |   `[1,1,1,2,2,2]` |


## 12. Interview Explanation

> I use two pointers and a dummy node. The pointers start at the heads
> of the sorted lists. At each step, I compare their values, attach the
> smaller node to the merged list, and advance the selected pointer.
> When one list is exhausted, I attach the remainder of the other list.
> I return `dummy.next` to skip the temporary dummy node. Every node is
> processed at most once, so time is O(n + m). The merge reuses existing
> nodes and uses O(1) auxiliary space.

**Remember:** Dummy → Two Pointers → Compare → Attach → Move → Attach
Remainder → Return Head.
