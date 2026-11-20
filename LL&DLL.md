# Linked List

# 1. Introduction to Linked List

A **Linked List** is a linear data structure where elements (called nodes) are stored in separate objects and connected using references.

Unlike arrays, linked list nodes do not need to be stored in contiguous memory locations.

There are two common types:

1. Singly Linked List
2. Doubly Linked List

## 1.1 Singly Linked List

Each node contains:

- `value` – Stores the data.
- `next` – Points to the next node.

```javascript
{
  value: 10,
  next: null
}
```

Structure:

```text
head
 |
 v
[10 | next] → [20 | next] → [30 | null]
                                ^
                                |
                               tail
```

Traversal is possible only in the forward direction.

## 1.2 Doubly Linked List

Each node contains:

- `value` – Stores the data.
- `next` – Points to the next node.
- `prev` – Points to the previous node.

```javascript
{
  value: 10,
  next: null,
  prev: null
}
```

Structure:

```text
null ← [10] ⇄ [20] ⇄ [30] → null
        ^               ^
        |               |
       head            tail
```

Traversal is possible in both forward and backward directions.

---

# 2. Singly vs Doubly Linked List – Basic Comparison

| Feature | Singly Linked List | Doubly Linked List |
|---|---|---|
| Node properties | value, next | value, next, prev |
| Head | First node | First node |
| Tail | Last node | Last node |
| Traversal | Forward only | Forward and backward |
| Memory usage | Less | More |
| Pointer updates | Fewer | More |
| Reverse traversal | Not directly possible | Possible |
| Pop | O(n) | O(1) |
| Push | O(1) | O(1) |
| Shift | O(1) | O(1) |
| Unshift | O(1) | O(1) |

## 2.1 When to Use Which?

**Singly Linked List**
- When only forward traversal is needed.
- When memory efficiency is important.
- When implementing simple stacks and adjacency lists.

**Doubly Linked List**
- When forward and backward traversal is needed.
- When removing the last node frequently.
- When implementing browser history, undo/redo, or LRU cache structures.

---

# 3. Big O Comparison

## 3.1 Time Complexity Table

| Operation | Singly Linked List | Doubly Linked List |
|---|---:|---:|
| Push | O(1) | O(1) |
| Pop | O(n) | O(1) |
| Shift | O(1) | O(1) |
| Unshift | O(1) | O(1) |
| Get by index | O(n) | O(n) |
| Get by value | O(n) | O(n) |
| Set by index | O(n) | O(n) |
| Insert by index | O(n) | O(n) |
| Remove by index | O(n) | O(n) |
| Reverse | O(n) | O(n) |

**Important:** In both implementations, insertion and deletion at an already-known node can be O(1). The O(n) complexity in the table includes the time required to find the position by index.

## 3.2 Why is Pop Different?

**Singly Linked List: O(n)**

A singly linked list only has `next`.

To remove the last node, we need to find the second-last node.

```text
10 → 20 → 30 → null
```

We must traverse from `head` to reach `20`.

**Doubly Linked List: O(1)**

A doubly linked list has `prev`.

We can directly access the second-last node using:

```javascript
this.tail.prev
```

Therefore, Pop takes O(1).

## 3.3 Why is Get O(n)?

Linked lists do not provide direct index-based access like arrays.

To find index 3, we must traverse the nodes.

```text
Index:  0      1      2      3
       [10] → [20] → [30] → [40]
```

In a doubly linked list, we can start from whichever end is closer, but worst-case complexity remains O(n).

---

# 4. Node Class – Comparison

## 4.1 Singly Linked List Node

```javascript
class Node {
  constructor(value) {
    this.value = value;
    this.next = null;
  }
}
```

## 4.2 Doubly Linked List Node

```javascript
class Node {
  constructor(value) {
    this.value = value;
    this.next = null;
    this.prev = null;
  }
}
```

### Main Difference

| Singly | Doubly |
|---|---|
| Has `next` | Has `next` and `prev` |
| One connection per node | Two connections per node |
| Forward traversal | Forward and backward traversal |

---

# 5. Constructor – Comparison

The constructor initializes the linked list.

Both implementations maintain:

- `head`
- `tail`
- `length`

## 5.1 Singly Linked List

```javascript
class LinkedList {
  constructor(value) {
    const newNode = new Node(value);

    this.head = newNode;
    this.tail = newNode;
    this.length = 1;
  }
}
```

## 5.2 Doubly Linked List

```javascript
class DoublyLinkedList {
  constructor(value) {
    const newNode = new Node(value);

    this.head = newNode;
    this.tail = newNode;
    this.length = 1;
  }
}
```

### Visual Representation

```text
head
 |
 v
[10] → null
 ^
 |
tail

length = 1
```

In a one-node list, both `head` and `tail` point to the same node.

---

# 6. Push – Add Node at the End

**Time Complexity: O(1) for both.**

Push adds a new node at the end.

## 6.1 Singly Linked List
  // edge case if head and tail is null
// edge case what if there is no item
// only one item 
// we can use pre, temp
```javascript
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
```

## 6.2 Doubly Linked List

```javascript
push(value) {
  const newNode = new Node(value);

  if (!this.head) {
    this.head = newNode;
    this.tail = newNode;
  } else {
    this.tail.next = newNode;
    newNode.prev = this.tail;
    this.tail = newNode;
  }

  this.length++;
  return this;
}
```

### Example

Execute:

```javascript
list.push(20);
list.push(30);
```

Singly:

```text
10 → 20 → 30 → null
```

Doubly:

```text
null ← 10 ⇄ 20 ⇄ 30 → null
```

### Difference

Doubly Linked List requires an additional connection:

```javascript
newNode.prev = this.tail;
```

---

# 7. Pop – Remove Node from the End

## Time Complexity

| Singly | Doubly |
|---|---|
| O(n) | O(1) |

## 7.1 Singly Linked List

We need to find the second-last node.

Variables:

- `temp` – Current node.
- `pre` – Previous node.

```javascript
pop() {
  if (!this.head) return undefined;

  let temp = this.head;
  let pre = this.head;

  while (temp.next) {
    pre = temp;
    temp = temp.next;
  }

  this.tail = pre;
  this.tail.next = null;

  this.length--;

  if (this.length === 0) {
    this.head = null;
    this.tail = null;
  }

  return temp;
}
```

## 7.2 Doubly Linked List

We can directly access the previous node using `tail.prev`.

```javascript
pop() {
  if (this.length === 0) return undefined;

  let temp = this.tail;

  if (this.length === 1) {
    this.head = null;
    this.tail = null;
  } else {
    this.tail = this.tail.prev;
    this.tail.next = null;
    temp.prev = null;
  }

  this.length--;

  return temp;
}
```

### Example

Before:

```text
10 → 20 → 30
```

After Pop:

```text
10 → 20
```

### Important Edge Cases

1. Empty list: Return `undefined`.
2. One node: Set both `head` and `tail` to `null`.
3. Multiple nodes: Update the tail and disconnect the removed node.

---

# 8. Unshift – Add Node at the Beginning

**Time Complexity: O(1) for both.**

## 8.1 Singly Linked List

```javascript
unshift(value) {
  const newNode = new Node(value);

  if (!this.head) {
    this.head = newNode;
    this.tail = newNode;
  } else {
    newNode.next = this.head;
    this.head = newNode;
  }

  this.length++;
  return this;
}
```

## 8.2 Doubly Linked List

```javascript
unshift(value) {
  const newNode = new Node(value);

  if (!this.head) {
    this.head = newNode;
    this.tail = newNode;
  } else {
    newNode.next = this.head;
    this.head.prev = newNode;
    this.head = newNode;
  }

  this.length++;
  return this;
}
```

### Example

Before:

```text
10 ⇄ 20 ⇄ 30
```

Execute:

```javascript
list.unshift(5);
```

After:

```text
5 ⇄ 10 ⇄ 20 ⇄ 30
```

### Difference

In Doubly Linked List, we also update:

```javascript
this.head.prev = newNode;
```

---

# 9. Shift – Remove Node from the Beginning

**Time Complexity: O(1) for both.**

## 9.1 Singly Linked List

```javascript
shift() {
  if (!this.head) return undefined;

  let temp = this.head;

  this.head = this.head.next;
  temp.next = null;

  this.length--;

  if (this.length === 0) {
    this.tail = null;
  }

  return temp;
}
```

## 9.2 Doubly Linked List

```javascript
shift() {
  if (this.length === 0) return undefined;

  let temp = this.head;

  if (this.length === 1) {
    this.head = null;
    this.tail = null;
  } else {
    this.head = this.head.next;
    this.head.prev = null;
    temp.next = null;
  }

  this.length--;

  return temp;
}
```

### Example

Before:

```text
10 ⇄ 20 ⇄ 30
```

After Shift:

```text
20 ⇄ 30
```

### Difference

In Doubly Linked List, we must disconnect the previous reference:

```javascript
this.head.prev = null;
```

---

# 10. Get – Find Node by Index

**Time Complexity: O(n) for both.**

Get returns the node at a given index.

Remember:

```text
Index:  0      1      2      3
       [10] → [20] → [30] → [40]
```

## 10.1 Singly Linked List

Traversal always starts from `head`.

```javascript
get(index) {
  if (index < 0 || index >= this.length) {
    return undefined;
  }

  let temp = this.head;

  for (let i = 0; i < index; i++) {
    temp = temp.next;
  }

  return temp;
}
```

## 10.2 Doubly Linked List

We can start from either `head` or `tail`.

```javascript
get(index) {
  if (index < 0 || index >= this.length) {
    return undefined;
  }

  let temp = this.head;

  if (index < this.length / 2) {
    for (let i = 0; i < index; i++) {
      temp = temp.next;
    }
  } else {
    temp = this.tail;

    for (let i = this.length - 1; i > index; i--) {
      temp = temp.prev;
    }
  }

  return temp;
}
```

### Difference

| Singly | Doubly |
|---|---|
| Always starts at head | Starts at the closer end |
| Uses `next` | Uses `next` or `prev` |
| O(n) | O(n) worst case |

---

# 11. Set – Update Node Value

**Time Complexity: O(n) for both.**

Set updates the value of a node at a particular index.

## 11.1 Singly Linked List

```javascript
set(index, value) {
  let temp = this.get(index);

  if (temp) {
    temp.value = value;
    return true;
  }

  return false;
}
```

## 11.2 Doubly Linked List

```javascript
set(index, value) {
  let temp = this.get(index);

  if (temp) {
    temp.value = value;
    return true;
  }

  return false;
}
```

### Example

Before:

```text
10 ⇄ 20 ⇄ 30
```

Execute:

```javascript
list.set(1, 100);
```

After:

```text
10 ⇄ 100 ⇄ 30
```

**Note:** Both implementations use the same Set logic. Only the internal `get()` implementation differs.

---

# 12. Insert – Add Node at a Specific Index

**Time Complexity: O(n) for both.**

Insert adds a node at a specific index.

### Edge Cases

1. Index is `0` → Use `unshift()`.
2. Index equals length → Use `push()`.
3. Invalid index → Return `false`.
4. Otherwise, insert between nodes.

## 12.1 Singly Linked List

```javascript
insert(index, value) {
  if (index < 0 || index > this.length) {
    return false;
  }

  if (index === 0) {
    return this.unshift(value);
  }

  if (index === this.length) {
    return this.push(value);
  }

  const newNode = new Node(value);
  const temp = this.get(index - 1);

  newNode.next = temp.next;
  temp.next = newNode;

  this.length++;

  return true;
}
```

## 12.2 Doubly Linked List

```javascript
insert(index, value) {
  if (index < 0 || index > this.length) {
    return false;
  }

  if (index === this.length) {
    return this.push(value);
  }

  if (index === 0) {
    return this.unshift(value);
  }

  const newNode = new Node(value);

  const before = this.get(index - 1);
  const after = before.next;

  before.next = newNode;
  newNode.prev = before;

  newNode.next = after;
  after.prev = newNode;

  this.length++;

  return true;
}
```

### Example

Before:

```text
10 ⇄ 20 ⇄ 40
```

Execute:

```javascript
list.insert(2, 30);
```

After:

```text
10 ⇄ 20 ⇄ 30 ⇄ 40
```

### Difference

Singly Linked List updates two references:

```javascript
newNode.next = temp.next;
temp.next = newNode;
```

Doubly Linked List updates four references:

```javascript
before.next = newNode;
newNode.prev = before;

newNode.next = after;
after.prev = newNode;
```

---

# 13. Remove – Delete Node at a Specific Index

**Time Complexity: O(n) for both.**

Remove deletes a node at a given index.

## 13.1 Singly Linked List

```javascript
remove(index) {
  if (index < 0 || index >= this.length) {
    return undefined;
  }

  if (index === 0) {
    return this.shift();
  }

  if (index === this.length - 1) {
    return this.pop();
  }

  const before = this.get(index - 1);
  const temp = before.next;

  before.next = temp.next;
  temp.next = null;

  this.length--;

  return temp;
}
```

## 13.2 Doubly Linked List

```javascript
remove(index) {
  if (index < 0 || index >= this.length) {
    return undefined;
  }

  if (index === 0) {
    return this.shift();
  }

  if (index === this.length - 1) {
    return this.pop();
  }

  const temp = this.get(index);

  temp.prev.next = temp.next;
  temp.next.prev = temp.prev;

  temp.next = null;
  temp.prev = null;

  this.length--;

  return temp;
}
```

### Example

Before:

```text
10 ⇄ 20 ⇄ 30 ⇄ 40
```

Execute:

```javascript
list.remove(2);
```

After:

```text
10 ⇄ 20 ⇄ 40
```

### Difference

Singly Linked List only needs to update the previous node's `next`.

Doubly Linked List must update both the previous and next nodes.

---

# 14. Reverse – Reverse the Linked List

**Time Complexity: O(n) for both.**

Reversing changes the direction of node connections.

## 14.1 Singly Linked List

Three important variables:

- `prev` – Previous node.
- `temp` – Current node.
- `next` – Next node.

```javascript
reverse() {
  let temp = this.head;

  this.head = this.tail;
  this.tail = temp;

  let prev = null;
  let next = temp.next

  for (let i = 0; i < this.length; i++) {
    next = temp.next;
    temp.next = prev;

    prev = temp;
    temp = next;
  }

  return this;
}
```

### Example

Before:

```text
10 → 20 → 30 → 40 → null
```

After:

```text
40 → 30 → 20 → 10 → null
```

## 14.2 Doubly Linked List

In a doubly linked list, we can reverse by swapping the `next` and `prev` references of each node.

```javascript
reverse() {
  let current = this.head;

  while (current) {
    const temp = current.next;

    current.next = current.prev;
    current.prev = temp;

    current = temp;
  }

  const temp = this.head;
  this.head = this.tail;
  this.tail = temp;

  return this;
}
```

### Example

Before:

```text
null ← 10 ⇄ 20 ⇄ 30 → null
```

After:

```text
null ← 30 ⇄ 20 ⇄ 10 → null
```

### Difference

| Singly | Doubly |
|---|---|
| Reverses `next` connections | Swaps `next` and `prev` |
| Uses `prev`, `temp`, `next` | Uses `current` and `temp` |
| O(n) | O(n) |

---

# 15. Lookup by Value

**Time Complexity: O(n) for both.**

Lookup by value searches for a node containing a specific value.

Unlike `get(index)`, which searches by position, this operation searches by data.

## Singly Linked List

```javascript
find(value) {
  let temp = this.head;

  while (temp) {
    if (temp.value === value) {
      return temp;
    }

    temp = temp.next;
  }

  return undefined;
}
```

## Doubly Linked List

```javascript
find(value) {
  let temp = this.head;

  while (temp) {
    if (temp.value === value) {
      return temp;
    }

    temp = temp.next;
  }

  return undefined;
}
```

### Example

```javascript
list.find(30);
```

If the list contains:

```text
10 → 20 → 30 → 40
```

The method returns the node containing `30`.

**Note:** This implementation searches from the head in both lists. A doubly linked list could also search backward from the tail.

---

# 16. Complete Implementation Comparison

## Singly Linked List – Complete Code

```javascript
class Node {
  constructor(value) {
    this.value = value;
    this.next = null;
  }
}

class LinkedList {
  constructor(value) {
    const newNode = new Node(value);

    this.head = newNode;
    this.tail = newNode;
    this.length = 1;
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

  pop() {
    if (!this.head) return undefined;

    let temp = this.head;
    let pre = this.head;

    while (temp.next) {
      pre = temp;
      temp = temp.next;
    }

    this.tail = pre;
    this.tail.next = null;

    this.length--;

    if (this.length === 0) {
      this.head = null;
      this.tail = null;
    }

    return temp;
  }

  unshift(value) {
    const newNode = new Node(value);

    if (!this.head) {
      this.head = newNode;
      this.tail = newNode;
    } else {
      newNode.next = this.head;
      this.head = newNode;
    }

    this.length++;
    return this;
  }

  shift() {
    if (!this.head) return undefined;

    let temp = this.head;

    this.head = this.head.next;
    temp.next = null;

    this.length--;

    if (this.length === 0) {
      this.tail = null;
    }

    return temp;
  }

  get(index) {
    if (index < 0 || index >= this.length) {
      return undefined;
    }

    let temp = this.head;

    for (let i = 0; i < index; i++) {
      temp = temp.next;
    }

    return temp;
  }

  set(index, value) {
    let temp = this.get(index);

    if (temp) {
      temp.value = value;
      return true;
    }

    return false;
  }

  insert(index, value) {
    if (index < 0 || index > this.length) {
      return false;
    }

    if (index === 0) return this.unshift(value);
    if (index === this.length) return this.push(value);

    const newNode = new Node(value);
    const temp = this.get(index - 1);

    newNode.next = temp.next;
    temp.next = newNode;

    this.length++;
    return true;
  }

  remove(index) {
    if (index < 0 || index >= this.length) {
      return undefined;
    }

    if (index === 0) return this.shift();
    if (index === this.length - 1) return this.pop();

    const before = this.get(index - 1);
    const temp = before.next;

    before.next = temp.next;
    temp.next = null;

    this.length--;
    return temp;
  }

  find(value) {
    let temp = this.head;

    while (temp) {
      if (temp.value === value) return temp;
      temp = temp.next;
    }

    return undefined;
  }

  reverse() {
    let temp = this.head;

    this.head = this.tail;
    this.tail = temp;

    let prev = null;
    let next = null;

    for (let i = 0; i < this.length; i++) {
      next = temp.next;
      temp.next = prev;
      prev = temp;
      temp = next;
    }

    return this;
  }
}
```

## Doubly Linked List – Complete Code

```javascript
class Node {
  constructor(value) {
    this.value = value;
    this.next = null;
    this.prev = null;
  }
}

class DoublyLinkedList {
  constructor(value) {
    const newNode = new Node(value);

    this.head = newNode;
    this.tail = newNode;
    this.length = 1;
  }

  push(value) {
    const newNode = new Node(value);

    if (!this.head) {
      this.head = newNode;
      this.tail = newNode;
    } else {
      this.tail.next = newNode;
      newNode.prev = this.tail;
      this.tail = newNode;
    }

    this.length++;
    return this;
  }

  pop() {
    if (this.length === 0) return undefined;

    let temp = this.tail;

    if (this.length === 1) {
      this.head = null;
      this.tail = null;
    } else {
      this.tail = this.tail.prev;
      this.tail.next = null;
      temp.prev = null;
    }

    this.length--;
    return temp;
  }

  unshift(value) {
    const newNode = new Node(value);

    if (!this.head) {
      this.head = newNode;
      this.tail = newNode;
    } else {
      newNode.next = this.head;
      this.head.prev = newNode;
      this.head = newNode;
    }

    this.length++;
    return this;
  }

  shift() {
    if (this.length === 0) return undefined;

    let temp = this.head;

    if (this.length === 1) {
      this.head = null;
      this.tail = null;
    } else {
      this.head = this.head.next;
      this.head.prev = null;
      temp.next = null;
    }

    this.length--;
    return temp;
  }

  get(index) {
    if (index < 0 || index >= this.length) {
      return undefined;
    }

    let temp = this.head;

    if (index < this.length / 2) {
      for (let i = 0; i < index; i++) {
        temp = temp.next;
      }
    } else {
      temp = this.tail;

      for (let i = this.length - 1; i > index; i--) {
        temp = temp.prev;
      }
    }

    return temp;
  }

  set(index, value) {
    let temp = this.get(index);

    if (temp) {
      temp.value = value;
      return true;
    }

    return false;
  }

  insert(index, value) {
    if (index < 0 || index > this.length) {
      return false;
    }

    if (index === 0) return this.unshift(value);
    if (index === this.length) return this.push(value);

    const newNode = new Node(value);

    const before = this.get(index - 1);
    const after = before.next;

    before.next = newNode;
    newNode.prev = before;

    newNode.next = after;
    after.prev = newNode;

    this.length++;
    return true;
  }

  remove(index) {
    if (index < 0 || index >= this.length) {
      return undefined;
    }

    if (index === 0) return this.shift();
    if (index === this.length - 1) return this.pop();

    const temp = this.get(index);

    temp.prev.next = temp.next;
    temp.next.prev = temp.prev;

    temp.next = null;
    temp.prev = null;

    this.length--;
    return temp;
  }

  find(value) {
    let temp = this.head;

    while (temp) {
      if (temp.value === value) return temp;
      temp = temp.next;
    }

    return undefined;
  }

  reverse() {
    let current = this.head;

    while (current) {
      const temp = current.next;

      current.next = current.prev;
      current.prev = temp;

      current = temp;
    }

    const temp = this.head;
    this.head = this.tail;
    this.tail = temp;

    return this;
  }
}
```

---

# 17. Important Edge Cases

Every linked list operation must consider these scenarios.

| Edge Case | Expected Behaviour |
|---|---|
| Empty list | `head = null`, `tail = null`, `length = 0` |
| One node | `head` and `tail` point to the same node |
| Remove first node | Update head |
| Remove last node | Update tail |
| Insert at index 0 | Update head |
| Insert at length | Update tail |
| Invalid index | Return `undefined` or `false` |
| Remove only node | Set head and tail to null |
| Reverse empty list | Remain empty |
| Reverse one node | Remain unchanged |

## Important Implementation Rules

1. Always validate indexes.
2. Update `length` after successful insertion or deletion.
3. Update both `head` and `tail` when required.
4. In a Doubly Linked List, update both `next` and `prev`.
5. Disconnect removed nodes from the list.
6. Save the next node before reversing connections.
7. Handle empty and one-node lists separately.

---

# 18. Common Mistakes in Linked Lists

| Mistake | Correct Approach |
|---|---|
| Using `head` instead of `this.head` | Use `this.head` |
| Writing `cosnt` | Write `const` |
| Checking `this.head === 0` | Check `!this.head` |
| Setting `length = null` | Decrement length |
| Forgetting to update tail | Update tail when removing last node |
| Forgetting `prev` update | Update both directions |
| Not disconnecting removed node | Set its links to null |
| Changing `next` before saving it | Save `next` first |
| Not handling one-node lists | Add a dedicated edge case |

---

# 19. Interview Questions and Answers

### Q1. What is a Linked List?

A linear data structure made up of nodes connected through references.

### Q2. What is the difference between Singly and Doubly Linked Lists?

Singly Linked List has one reference (`next`), while Doubly Linked List has two references (`next` and `prev`).

### Q3. Why is Array Lookup O(1)?

Arrays provide direct index-based access.

### Q4. Why is Linked List Lookup O(n)?

We must traverse nodes one by one to find a particular index.

### Q5. Why is Singly Linked List Pop O(n)?

Because we must find the second-last node by traversing from the head.

### Q6. Why is Doubly Linked List Pop O(1)?

Because `tail.prev` gives direct access to the second-last node.

### Q7. Why do we need Head and Tail?

- Head provides direct access to the first node.
- Tail provides direct access to the last node.

### Q8. What happens when the Linked List has only one node?

Both `head` and `tail` point to the same node. When it is removed, both become `null`.

### Q9. What is the advantage of a Doubly Linked List?

It supports traversal in both directions and allows O(1) removal of a known node.

### Q10. What is the disadvantage of a Doubly Linked List?

It requires additional memory for the `prev` reference and more pointer updates.

### Q11. Can we insert a node in O(1)?

Yes, if we already have a reference to the insertion position (or the node before it in a singly linked list). Finding that position by index generally takes O(n).

### Q12. Can we remove a node in O(1)?

Yes, if we already have the necessary node reference:
- Singly Linked List: Need the previous node.
- Doubly Linked List: The node's `prev` and `next` references are sufficient, provided it is not an endpoint requiring special handling.

---

# 20. Final Revision Cheat Sheet

| Method | Singly Linked List | Doubly Linked List |
|---|---:|---:|
| Push | O(1) | O(1) |
| Pop | O(n) | O(1) |
| Shift | O(1) | O(1) |
| Unshift | O(1) | O(1) |
| Get | O(n) | O(n) |
| Set | O(n) | O(n) |
| Insert | O(n) | O(n) |
| Remove | O(n) | O(n) |
| Find | O(n) | O(n) |
| Reverse | O(n) | O(n) |

## Most Important Concepts to Remember

**Singly Linked List**
- One pointer: `next`.
- Forward traversal only.
- Pop takes O(n).
- Less memory usage.
- Reverse requires changing `next` connections.

**Doubly Linked List**
- Two pointers: `next` and `prev`.
- Forward and backward traversal.
- Pop takes O(1).
- More memory usage.
- Reverse requires swapping `next` and `prev`.

## Final Takeaway

A Linked List is useful when frequent insertions and deletions are required.

- Use a **Singly Linked List** when forward traversal and lower memory usage are sufficient.
- Use a **Doubly Linked List** when backward traversal and efficient removal from both ends are important.

