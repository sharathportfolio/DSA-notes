
# JavaScript Arrays — Short Guide

## 1. What is an Array?

An **array** is an ordered collection of elements stored in a single variable.

JavaScript arrays:
- Use **zero-based indexing**.
- Can store different data types.
- Are dynamic (can grow or shrink).
- Allow duplicate values.
- Provide fast access using an index.

```javascript
const arr = [10, 20, 30, 40, 50];

console.log(arr[0]); // 10
console.log(arr[2]); // 30
console.log(arr.length); // 5
```

**Index visualization:**

```text
Index:   0   1   2   3   4
       ┌───┬───┬───┬───┬───┐
Value: │10 │20 │30 │40 │50 │
       └───┴───┴───┴───┴───┘
```

**Time Complexity:**
- Access by index: `O(1)`
- Update by index: `O(1)`
- Search by value: `O(n)`

---

## 2. Array Operations

### 2.1 push() — Add at End

Adds one or more elements to the **end** of an array.

```javascript
const arr = [10, 20, 30];

arr.push(40);

console.log(arr); // [10, 20, 30, 40]
```

**Time Complexity:** `O(1)` amortized

**Why?** Existing elements usually do not need to move.

---

### 2.2 pop() — Remove from End

Removes and returns the **last element**.

```javascript
const arr = [10, 20, 30];

const removed = arr.pop();

console.log(removed); // 30
console.log(arr); // [10, 20]
```

**Time Complexity:** `O(1)`

---

### 2.3 unshift() — Add at Beginning

Adds one or more elements to the **beginning**.

```javascript
const arr = [10, 20, 30];

arr.unshift(5);

console.log(arr); // [5, 10, 20, 30]
```

**Time Complexity:** `O(n)`

**Why?** Existing elements must be shifted to new indexes.

---

### 2.4 shift() — Remove from Beginning

Removes and returns the **first element**.

```javascript
const arr = [10, 20, 30];

const removed = arr.shift();

console.log(removed); // 10
console.log(arr); // [20, 30]
```

**Time Complexity:** `O(n)`

**Why?** Remaining elements must be reindexed.

---

### 2.5 splice() — Insert, Delete, Replace

The `splice()` method modifies the original array.

**Syntax:**

```javascript
arr.splice(startIndex, deleteCount, ...items);
```

**Insert an element:**

```javascript
const arr = [10, 20, 30];

arr.splice(1, 0, 15);

console.log(arr); // [10, 15, 20, 30]
```

**Delete an element:**

```javascript
const arr = [10, 20, 30];

arr.splice(1, 1);

console.log(arr); // [10, 30]
```

**Replace an element:**

```javascript
const arr = [10, 20, 30];

arr.splice(1, 1, 99);

console.log(arr); // [10, 99, 30]
```

**Time Complexity:** `O(n)` worst case

**Note:** Operations near the end can be faster.

---

## 3. Access and Update Elements

### Access by Index

```javascript
const arr = [10, 20, 30, 40];

console.log(arr[2]); // 30
```

**Time Complexity:** `O(1)`

### Update by Index

```javascript
arr[2] = 100;

console.log(arr); // [10, 20, 100, 40]
```

**Time Complexity:** `O(1)`

**Why?** The array can directly access a known index.

---

## 4. Searching in Arrays

### 4.1 includes()

Checks whether an array contains a value.

```javascript
const arr = [10, 20, 30, 40];

console.log(arr.includes(30)); // true
console.log(arr.includes(50)); // false
```

**Time Complexity:** `O(n)`

---

### 4.2 indexOf()

Returns the first matching index or `-1`.

```javascript
const arr = [10, 20, 30];

console.log(arr.indexOf(20)); // 1
console.log(arr.indexOf(50)); // -1
```

**Time Complexity:** `O(n)`

---

### 4.3 find()

Returns the first element that satisfies a condition.

```javascript
const arr = [10, 20, 30, 40];

const result = arr.find(num => num > 20);

console.log(result); // 30
```

**Time Complexity:** `O(n)`

---

### 4.4 findIndex()

Returns the index of the first matching element.

```javascript
const arr = [10, 20, 30, 40];

const index = arr.findIndex(num => num > 20);

console.log(index); // 2
```

**Time Complexity:** `O(n)`

---

## 5. Array Iteration Methods

### 5.1 forEach()

Executes a function for each element.

```javascript
const arr = [10, 20, 30];

arr.forEach(num => {
  console.log(num);
});
```

**Time Complexity:** `O(n)`

**Note:** `forEach()` returns `undefined`.

---

### 5.2 map()

Creates a **new array** by transforming each element.

```javascript
const arr = [1, 2, 3];

const doubled = arr.map(num => num * 2);

console.log(doubled); // [2, 4, 6]
```

**Time Complexity:** `O(n)`

**Space Complexity:** `O(n)`

---

### 5.3 filter()

Creates a new array containing elements that satisfy a condition.

```javascript
const arr = [10, 15, 20, 25, 30];

const even = arr.filter(num => num % 2 === 0);

console.log(even); // [10, 20, 30]
```

**Time Complexity:** `O(n)`

**Space Complexity:** `O(n)` worst case

---

### 5.4 reduce()

Reduces an array to a single accumulated result.

```javascript
const arr = [10, 20, 30];

const sum = arr.reduce((acc, num) => acc + num, 0);

console.log(sum); // 60
```

**Time Complexity:** `O(n)`

**Space Complexity:** `O(1)` for this example

---

### 5.5 some()

Returns `true` if at least one element matches.

```javascript
const arr = [10, 20, 30];

console.log(arr.some(num => num > 25)); // true
```

**Time Complexity:** `O(n)` worst case

---

### 5.6 every()

Returns `true` if all elements satisfy the condition.

```javascript
const arr = [10, 20, 30];

console.log(arr.every(num => num > 5)); // true
```

**Time Complexity:** `O(n)` worst case

---

## 6. Other Useful Array Methods

### slice() — Copy a Portion

Returns a new array without modifying the original.

```javascript
const arr = [10, 20, 30, 40, 50];

const result = arr.slice(1, 4);

console.log(result); // [20, 30, 40]
```

**Time Complexity:** `O(k)`

Where `k` is the number of copied elements.

---

### concat() — Merge Arrays

```javascript
const a = [10, 20];
const b = [30, 40];

const result = a.concat(b);

console.log(result); // [10, 20, 30, 40]
```

**Time Complexity:** `O(n + m)`

---

### reverse() — Reverse Array

```javascript
const arr = [10, 20, 30];

arr.reverse();

console.log(arr); // [30, 20, 10]
```

**Time Complexity:** `O(n)`

**Note:** Modifies the original array.

---

### sort() — Sort Elements

```javascript
const arr = [30, 10, 40, 20];

arr.sort((a, b) => a - b);

console.log(arr); // [10, 20, 30, 40]
```

**Time Complexity:** Typically `O(n log n)`

**Note:** Sorting algorithm and worst-case complexity depend on the JavaScript engine.

For numeric sorting, use a comparator.

```javascript
// Ascending
arr.sort((a, b) => a - b);

// Descending
arr.sort((a, b) => b - a);
```

---

### join() — Convert to String

```javascript
const arr = ["React", "Next.js", "Node.js"];

console.log(arr.join(", "));
// React, Next.js, Node.js
```

**Time Complexity:** `O(n + L)`

Where `L` represents the total output string length.

---

### flat() — Flatten Nested Arrays

```javascript
const arr = [1, [2, 3], [4, 5]];

console.log(arr.flat());
// [1, 2, 3, 4, 5]
```

**Time Complexity:** `O(n)` for a flat output of `n` elements.

---

## 7. Array Traversal

### Using for Loop

```javascript
const arr = [10, 20, 30];

for (let i = 0; i < arr.length; i++) {
  console.log(arr[i]);
}
```

**Time Complexity:** `O(n)`

**Space Complexity:** `O(1)`

### Using for...of

```javascript
for (const num of arr) {
  console.log(num);
}
```

**Time Complexity:** `O(n)`

---

## 8. Array Big O Cheat Sheet

| Operation | Time Complexity |
|---|---|
| Access by index | O(1) |
| Update by index | O(1) |
| push() | O(1) amortized |
| pop() | O(1) |
| unshift() | O(n) |
| shift() | O(n) |
| splice() | O(n) worst case |
| includes() | O(n) |
| indexOf() | O(n) |
| find() | O(n) |
| findIndex() | O(n) |
| forEach() | O(n) |
| map() | O(n) |
| filter() | O(n) |
| reduce() | O(n) |
| some() | O(n) |
| every() | O(n) |
| slice() | O(k) |
| concat() | O(n + m) |
| reverse() | O(n) |
| sort() | O(n log n) typical |

> These are common Big O estimates for ordinary JavaScript arrays. Actual performance can depend on the JavaScript engine, array representation, and callback work.

---

## 9. Mutable vs Immutable Methods

### Mutable Methods

These methods modify the original array.

| Method | Purpose |
|---|---|
| push() | Add at end |
| pop() | Remove from end |
| shift() | Remove first |
| unshift() | Add at beginning |
| splice() | Insert/delete/replace |
| sort() | Sort original |
| reverse() | Reverse original |
| fill() | Fill values |

### Non-Mutating Methods

These methods do not modify the original array.

| Method | Purpose |
|---|---|
| map() | Transform |
| filter() | Filter |
| reduce() | Accumulate |
| slice() | Copy portion |
| concat() | Merge |
| includes() | Check existence |
| find() | Find element |
| toSorted() | Return sorted copy |
| toReversed() | Return reversed copy |
| toSpliced() | Return modified copy |

**React Tip:**

Prefer immutable updates when working with React state.

```javascript
// Avoid mutating state directly
items.push(40);

// Preferred
setItems(prev => [...prev, 40]);
```

---

## 10. Easy Way to Remember

```text
END OF ARRAY
push()       → O(1) amortized
pop()        → O(1)

BEGINNING OF ARRAY
unshift()    → O(n)
shift()      → O(n)

INDEX
arr[index]   → O(1)
arr[i] = x   → O(1)

SEARCH
includes()   → O(n)
indexOf()    → O(n)
find()       → O(n)

TRANSFORM
map()        → O(n)
filter()     → O(n)
reduce()     → O(n)

SORTING
sort()       → O(n log n) typical
```

---

## 11. Why These Complexities?

### Adding at the End

```text
Before:
[10, 20, 30]

After push(40):
[10, 20, 30, 40]
            ↑
        New element
```

No existing elements usually need to move.

**Complexity:** `O(1)` amortized

### Adding at the Beginning

```text
Before:
[10, 20, 30]

After unshift(5):
[5, 10, 20, 30]
 ↑   →   →   →
New   Shifted elements
```

Existing elements must be reindexed.

**Complexity:** `O(n)`

### Accessing by Index

```text
Index:  0   1   2   3
       [10, 20, 30, 40]
                ↑
              arr[2]
```

Direct access to a known position.

**Complexity:** `O(1)`

### Searching by Value

```text
Array: [10, 20, 30, 40, 50]

Search: 50

Step 1 → Check 10
Step 2 → Check 20
Step 3 → Check 30
Step 4 → Check 40
Step 5 → Check 50 ✓
```

Worst case: check every element.

**Complexity:** `O(n)`

---

## 12. Common Array Interview Questions

Practice these problems:

1. Find the largest element in an array.
2. Find the smallest element in an array.
3. Reverse an array without `reverse()`.
4. Remove duplicate elements.
5. Find the second-largest element.
6. Find the sum of all elements.
7. Count the frequency of each element.
8. Move all zeros to the end.
9. Rotate an array by `k` positions.
10. Find two numbers whose sum equals a target.
11. Merge two sorted arrays.
12. Find the missing number in a sequence.
13. Find the maximum subarray sum.
14. Find the intersection of two arrays.
15. Implement binary search on a sorted array.

### Important DSA Patterns

| Pattern | Common Use Case |
|---|---|
| Two Pointers | Pair sum, reverse array |
| Sliding Window | Subarray problems |
| Prefix Sum | Range sum queries |
| Hash Map | Frequency counting |
| Binary Search | Search sorted data |
| Sorting | Ordering and grouping |
| Kadane's Algorithm | Maximum subarray sum |

---

## 13. Key Interview Takeaways

- Arrays use **zero-based indexing**.
- Index access is generally **O(1)**.
- Searching an unsorted array is generally **O(n)**.
- Adding/removing at the end is usually efficient.
- Adding/removing at the beginning costs **O(n)**.
- `map()` transforms data.
- `filter()` selects data.
- `reduce()` accumulates data.
- `find()` returns the first matching element.
- `some()` checks whether any element matches.
- `every()` checks whether all elements match.
- `sort()` mutates the original array.
- Prefer immutable array operations in React.
- Learn **Two Pointers, Sliding Window, Prefix Sum, and Binary Search** for DSA interviews.

---

**Remember:**

> Access by index is fast. Searching by value may require scanning. Inserting or deleting near the beginning requires shifting elements.

