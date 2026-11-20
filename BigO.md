# Big O Notation & Data Structures

> Personal notes for understanding **time complexity, space complexity, data structures, algorithms, and problem-solving patterns**.

---

# 1. What is Big O?

**Big O notation** describes how the **time or space requirements of an algorithm grow as the input size (`n`) increases**.

It helps us compare algorithms based on their efficiency, especially when dealing with large inputs.

### Important

Big O does **not** tell us the exact execution time.

Instead, it tells us the **growth rate** of an algorithm.

For example:

```text
O(1)       → Constant
O(log n)   → Logarithmic
O(n)       → Linear
O(n log n) → Linearithmic
O(n²)      → Quadratic
O(2ⁿ)      → Exponential
O(n!)      → Factorial
```

As `n` becomes very large, the difference between these growth rates becomes significant.

---

# 2. Time Complexity vs Space Complexity

## Time Complexity

**Time complexity** describes how the number of operations performed by an algorithm grows as the input size increases.

Example:

```javascript
function logItems(n) {
  for (let i = 0; i < n; i++) {
    console.log(i);
  }
}
```

If `n = 10`, the loop runs 10 times.

If `n = 1,000`, the loop runs 1,000 times.

Therefore:

```text
Time Complexity: O(n)
```

---

## Space Complexity

**Space complexity** describes how much additional memory an algorithm requires as the input size increases.

Example:

```javascript
function createArray(n) {
  const arr = [];

  for (let i = 0; i < n; i++) {
    arr.push(i);
  }

  return arr;
}
```

The array grows with `n`.

Therefore:

```text
Space Complexity: O(n)
```

### Important distinction

Space complexity can include:

- Variables
- Arrays
- Objects
- Recursion call stack
- Other dynamically allocated memory

---


# 3. O(1) — Constant Time

The amount of work does not grow with the input size.

```javascript
function addItems(n) {
  return n + n;
}
```

Regardless of whether:

```text
n = 10
n = 1,000
n = 1,000,000
```

the function performs a constant amount of work.

```text
Time Complexity: O(1)
Space Complexity: O(1)
```

---

# 4. O(log n) — Logarithmic Time

The amount of work grows logarithmically as the input increases.

A common example is **Binary Search**.

The search space is repeatedly divided, usually by half.

Example:

```text
1,000,000 elements

500,000
250,000
125,000
...
```

This is why binary search is much faster than checking every element when the data is sorted.

```text
Time Complexity: O(log n)
```

### Example idea

```javascript
function binarySearch(arr, target) {
  let left = 0;
  let right = arr.length - 1;

  while (left <= right) {
    const mid = Math.floor((left + right) / 2);

    if (arr[mid] === target) {
      return mid;
    }

    if (arr[mid] < target) {
      left = mid + 1;
    } else {
      right = mid - 1;
    }
  }

  return -1;
}
```

---

# 7. O(n) — Linear Time

The number of operations grows directly with the input size.

```javascript
function logItems(n) {
  for (let i = 0; i < n; i++) {
    console.log(i);
  }
}
```

If:

```text
n = 5
```

the loop runs approximately 5 times.

If:

```text
n = 1,000
```

it runs approximately 1,000 times.

Therefore:

```text
Time Complexity: O(n)
```

---

# 8. O(n log n) — Linearithmic Time

`O(n log n)` is common in efficient sorting algorithms.

Examples include:

- Merge Sort
- Heap Sort
- Quick Sort

Conceptually, algorithms with this complexity often combine:

```text
n operations
```

with:

```text
log n levels
```

Therefore:

```text
O(n log n)
```

is generally much better than:

```text
O(n²)
```

for large inputs.

---

# 9. O(n²) — Quadratic Time

The number of operations grows approximately with the square of the input size.

A common example is nested loops:

```javascript
function logItems(n) {
  for (let i = 0; i < n; i++) {
    for (let j = 0; j < n; j++) {
      console.log(i, j);
    }
  }
}
```

The outer loop runs `n` times.

For every outer-loop iteration, the inner loop also runs `n` times.

Therefore:

```text
n × n = n²
```

So:

```text
Time Complexity: O(n²)
```

---

# 10. O(2ⁿ) — Exponential Time

The amount of work grows exponentially as the input increases.

A common example is naive recursive solutions to problems such as Fibonacci.

```text
n → 1
n → 2
n → 4
n → 8
n → 16
...
```

Exponential algorithms become impractical very quickly as `n` grows.

Example:

```text
O(2ⁿ)
```

Dynamic Programming can often reduce certain exponential recursive solutions to polynomial or linear complexity by avoiding repeated work.

---

# 11. O(n!) — Factorial Time

Factorial complexity grows extremely quickly.

A common example is generating **all permutations** of `n` elements.

For example:

```text
3! = 6
4! = 24
5! = 120
6! = 720
10! = 3,628,800
```

Therefore:

```text
O(n!)
```

is generally practical only for relatively small input sizes.

---

# 12. Rules for Calculating Big O

## Rule 1 — Focus on Growth

We care about how the algorithm behaves as `n` becomes large.

For example:

```text
O(5n + 10)
```

becomes:

```text
O(n)
```

---

## Rule 2 — Drop Constants

Constants do not affect the asymptotic growth rate.

```javascript
function logItems(n) {
  for (let i = 0; i < n; i++) {
    console.log(i);
  }

  for (let j = 0; j < n; j++) {
    console.log(j);
  }
}
```

The two loops run sequentially:

```text
n + n = 2n
```

Therefore:

```text
O(2n) → O(n)
```

---

## Rule 3 — Drop Non-Dominant Terms

Consider:

```text
O(n² + n)
```

As `n` becomes very large, `n²` grows much faster than `n`.

Therefore:

```text
O(n² + n) → O(n²)
```

Example:

```javascript
function logItems(n) {
  for (let i = 0; i < n; i++) {
    for (let j = 0; j < n; j++) {
      console.log(i, j);
    }

    for (let k = 0; k < n; k++) {
      console.log(k);
    }
  }
}
```

The nested loop contributes:

```text
O(n²)
```

The second loop is inside the outer loop, so it also executes:

```text
O(n²)
```

Together:

```text
O(n² + n²)
→ O(2n²)
→ O(n²)
```

---

# 13. Sequential vs Nested Loops

This is one of the most important Big O concepts.

## Sequential loops → Add

```javascript
for (...) {
  // O(n)
}

for (...) {
  // O(n)
}
```

Complexity:

```text
O(n + n)
→ O(2n)
→ O(n)
```

---

## Nested loops → Multiply

```javascript
for (...) {
  for (...) {
    // O(1)
  }
}
```

Complexity:

```text
O(n × n)
→ O(n²)
```

### Quick rule

```text
Sequential → Add
Nested → Multiply
```

---

# 14. Different Inputs Use Different Variables

Do not automatically assume every input is `n`.

Suppose an algorithm processes two independent arrays:

```javascript
function compare(arr1, arr2) {
  for (const item of arr1) {
    console.log(item);
  }

  for (const item of arr2) {
    console.log(item);
  }
}
```

If:

```text
arr1 = a elements
arr2 = b elements
```

then:

```text
O(a + b)
```

Not:

```text
O(n)
```

Similarly, nested loops over two different inputs may result in:

```text
O(a × b)
```

This distinction is important when the input sizes can be different.

---

# 15. Time Complexity vs Space Complexity Example

Consider:

```javascript
function createArray(n) {
  const arr = [];

  for (let i = 0; i < n; i++) {
    arr.push(i);
  }

  return arr;
}
```

The loop runs `n` times:

```text
Time: O(n)
```

The array stores `n` elements:

```text
Space: O(n)
```

Therefore:

```text
Time Complexity  → O(n)
Space Complexity → O(n)
```

---

# 16. Fundamental Data Structures

Data structures provide ways to organize and store data so that we can efficiently perform operations on it.

They can broadly be divided into:

```text
Linear Data Structures
Non-Linear Data Structures
```

---

# 17. Linear Data Structures

Linear data structures organize elements sequentially.

## Arrays

Arrays store elements in an ordered collection and typically provide efficient indexed access.

```javascript
const numbers = [10, 20, 30, 40];
```

Access by index:

```javascript
numbers[2];
```

Typically:

```text
Access by index → O(1)
```

Inserting or deleting in the middle may require shifting elements:

```text
Insertion → O(n)
Deletion   → O(n)
```

> Exact complexity depends on the operation and implementation.

---

## Strings

Strings are sequences of characters.

Common operations include:

- Searching
- Reversing
- Concatenation
- Substring extraction
- Pattern matching

Example:

```javascript
const name = "hello";
```

Strings are especially common in coding interview problems.

---

## Linked Lists

A linked list consists of nodes connected through references/pointers.

Conceptually:

```text
[10] → [20] → [30] → [40]
```

Each node typically contains:

```text
Data
Next pointer/reference
```

Advantages:

- Dynamic size
- Efficient insertion/deletion when the node position/reference is known

Disadvantages:

- No direct random access
- Traversal is generally `O(n)`

Typical complexities:

```text
Access       → O(n)
Search       → O(n)
Insert at head → O(1)
Delete at head → O(1)
```

---

## Stack

A stack follows:

```text
LIFO
Last In, First Out
```

Example:

```text
Push 10
Push 20
Push 30

Pop → 30
```

Common applications:

- Function call stack
- Undo/redo
- Browser history
- Parentheses/bracket matching
- DFS

Typical operations:

```text
Push → O(1)
Pop  → O(1)
Peek → O(1)
```

---

## Queue

A queue follows:

```text
FIFO
First In, First Out
```

Example:

```text
10 → 20 → 30 → 40

Remove → 10
```

Common applications:

- Task scheduling
- Message queues
- BFS
- Request processing

Typical queue operations can be:

```text
Enqueue → O(1)
Dequeue → O(1)
```

when implemented appropriately.

---

# 18. Non-Linear & Advanced Data Structures

## Hash Table / Hash Map

Stores data as key-value pairs.

```javascript
const user = new Map();

user.set("name", "John");
user.set("age", 25);
```

Average-case complexity:

```text
Search   → O(1)
Insert   → O(1)
Delete   → O(1)
```

Worst-case complexity can be `O(n)` depending on collisions and implementation.

Hash maps are extremely useful when we need fast lookup.

---

# 19. Trees

A tree is a hierarchical data structure.

Example:

```text
        10
       /  \
      5    15
     / \     \
    2   7     20
```

Important tree types include:

- Binary Tree
- Binary Search Tree (BST)
- AVL Tree
- Red-Black Tree
- Heap
- Trie

---

## Binary Search Tree

A BST generally follows:

```text
Left subtree < Node < Right subtree
```

For a balanced BST:

```text
Search → O(log n)
Insert → O(log n)
Delete → O(log n)
```

However, an unbalanced BST can degrade to:

```text
O(n)
```

---

# 20. Heaps

A heap is a specialized tree-based data structure commonly used to implement priority queues.

Types include:

```text
Min Heap
Max Heap
```

The root contains the minimum or maximum element depending on the heap type.

Typical operations:

```text
Get min/max → O(1)
Insert      → O(log n)
Delete root → O(log n)
```

Common applications:

- Priority queues
- Scheduling
- Heap Sort
- Dijkstra's algorithm

---

# 21. Graphs

Graphs represent relationships between objects.

A graph consists of:

```text
Vertices (Nodes)
Edges (Connections)
```

Example:

```text
A ─── B
│     │
│     │
C ─── D
```

Graphs are useful for:

- Maps
- Social networks
- Computer networks
- Dependencies
- Routing
- Recommendation systems

Graphs can be:

- Directed
- Undirected
- Weighted
- Unweighted

---

# 22. Tries

A **Trie**, also called a **Prefix Tree**, is a tree structure designed for storing strings based on their prefixes.

Example:

```text
        root
       /    \
      c      d
      |
      a
      |
      t
```

Useful for:

- Autocomplete
- Dictionary lookup
- Prefix searching
- Spell checking
- IP routing

Trie operations are commonly described in terms of the length of the string:

```text
Search → O(L)
Insert → O(L)
Delete → O(L)
```

where `L` is the length of the word.

---

# 23. Essential Algorithms

Algorithms are step-by-step procedures used to solve computational problems.

---

## Searching

### Linear Search

Checks elements one by one.

```text
Time → O(n)
```

Works even when the data is not sorted.

---

### Binary Search

Repeatedly divides the search space in half.

```text
Time → O(log n)
```

Usually requires the data to be sorted.

---

# 24. Sorting Algorithms

Sorting arranges data into a particular order.

Common algorithms:

| Algorithm | Average Time | Typical Worst Case |
|---|---:|---:|
| Bubble Sort | O(n²) | O(n²) |
| Selection Sort | O(n²) | O(n²) |
| Insertion Sort | O(n²) | O(n²) |
| Merge Sort | O(n log n) | O(n log n) |
| Heap Sort | O(n log n) | O(n log n) |
| Quick Sort | O(n log n) | O(n²) |

> Quick Sort's exact behavior depends on pivot selection and implementation.

---

# 25. Graph Traversal

## BFS — Breadth-First Search

BFS explores a graph **level by level**.

```text
Start
 ↓
Neighbors
 ↓
Neighbors of neighbors
 ↓
...
```

Usually implemented using a queue.

Common uses:

- Shortest path in an unweighted graph
- Level-order tree traversal
- Network exploration

---

## DFS — Depth-First Search

DFS explores as deeply as possible before backtracking.

Usually implemented using:

- Recursion
- Stack

Common uses:

- Path exploration
- Cycle detection
- Connected components
- Topological sorting
- Backtracking problems

For a graph represented with adjacency lists:

```text
BFS → O(V + E)
DFS → O(V + E)
```

where:

```text
V = number of vertices
E = number of edges
```

---

# 26. Shortest Path Algorithms

## Dijkstra's Algorithm

Used to find shortest paths from a source node when edge weights are **non-negative**.

Common applications:

- GPS/navigation
- Network routing
- Pathfinding

---

## Bellman-Ford Algorithm

Also finds shortest paths from a source.

Unlike Dijkstra's algorithm, Bellman-Ford can handle **negative edge weights**.

It can also detect negative-weight cycles.

Typical complexity:

```text
O(VE)
```

---

# 27. Problem-Solving Patterns

Understanding data structures is important, but solving problems efficiently also requires recognizing common patterns.

---

# 28. Two Pointers

The **Two Pointer** technique uses two positions to process an array or string efficiently.

Example:

```text
left  →        ← right
[1, 2, 3, 4, 5]
```

Common applications:

- Two Sum on sorted arrays
- Palindrome checking
- Removing duplicates
- Pair searching
- Partitioning

Often helps reduce:

```text
O(n²)
```

to:

```text
O(n)
```

when the problem structure allows it.

---

# 29. Sliding Window

The Sliding Window technique maintains a moving range over an array or string.

Example:

```text
[1, 2, 3, 4, 5, 6]
 ↑     ↑
left  right
```

Instead of repeatedly recalculating information for every possible subarray, we maintain the current window and update it as it moves.

Common applications:

- Maximum/minimum subarray
- Longest substring
- Fixed-size window problems
- Frequency-based substring problems

Many sliding-window problems can be solved in:

```text
O(n)
```

---

# 30. Recursion

Recursion occurs when a function calls itself.

Example:

```javascript
function countdown(n) {
  if (n === 0) {
    return;
  }

  console.log(n);
  countdown(n - 1);
}
```

A recursive solution usually contains:

1. **Base case**
2. **Recursive case**

Without a base case, recursion can continue indefinitely.

Recursion uses the **call stack**, so recursive algorithms can have additional space complexity.

---

# 31. Backtracking

Backtracking explores possible solutions and abandons a path as soon as it becomes invalid.

General idea:

```text
Choose
  ↓
Explore
  ↓
Valid?
 ↙   ↘
Yes   No
 ↓     ↓
Continue  Backtrack
```

Common applications:

- Sudoku
- N-Queens
- Permutations
- Combinations
- Maze solving

Backtracking problems can often have exponential or factorial time complexity.

---

# 32. Greedy Algorithms

A greedy algorithm makes the **best local choice at each step**.

The goal is that these local choices lead to a globally optimal solution.

Examples:

- Kruskal's Algorithm
- Prim's Algorithm
- Activity Selection
- Huffman Coding

> Greedy algorithms do **not** always produce the optimal solution. They work when the problem has the appropriate greedy-choice property.

---

# 33. Dynamic Programming

Dynamic Programming (DP) solves problems by breaking them into smaller overlapping subproblems and storing their results.

The two common approaches are:

### Memoization

Top-down approach.

```text
Recursion
   ↓
Cache results
   ↓
Avoid repeated work
```

### Tabulation

Bottom-up approach.

```text
Small problems
      ↓
Build larger problems
      ↓
Final answer
```

DP is useful when a problem has:

1. **Overlapping subproblems**
2. **Optimal substructure**

Common examples:

- Fibonacci
- 0/1 Knapsack
- Coin Change
- Longest Common Subsequence
- Longest Increasing Subsequence

---

# 34. Quick Big O Cheat Sheet

| Complexity | Name | Example |
|---|---|---|
| `O(1)` | Constant | Array index access |
| `O(log n)` | Logarithmic | Binary Search |
| `O(n)` | Linear | Linear Search |
| `O(n log n)` | Linearithmic | Merge Sort |
| `O(n²)` | Quadratic | Nested loops |
| `O(2ⁿ)` | Exponential | Some recursive/backtracking problems |
| `O(n!)` | Factorial | Generating permutations |

---

# 35. Data Structure Cheat Sheet

| Data Structure | Access | Search | Insert | Delete |
|---|---:|---:|---:|---:|
| Array | O(1) | O(n) | O(n)* | O(n)* |
| Linked List | O(n) | O(n) | O(1)** | O(1)** |
| Stack | O(n) | O(n) | O(1) | O(1) |
| Queue | O(n) | O(n) | O(1) | O(1) |
| Hash Map | — | O(1) avg. | O(1) avg. | O(1) avg. |
| Balanced BST | O(log n) | O(log n) | O(log n) | O(log n) |
| Heap | — | O(n) | O(log n) | O(log n) |

\* Array insertion/deletion depends on where the operation occurs.

\** For a linked list, insertion/deletion can be `O(1)` when the relevant node/position is already known; finding that position may take `O(n)`.

---

# 36. How to Think About Big O

When analyzing code, ask these questions:

### 1. How many times does each loop run?

```javascript
for (let i = 0; i < n; i++)
```

Usually:

```text
O(n)
```

### 2. Are loops nested?

```javascript
for (...) {
  for (...) {
  }
}
```

Usually:

```text
O(n²)
```

### 3. Are loops sequential?

```javascript
for (...) {}
for (...) {}
```

Usually:

```text
O(n + n)
→ O(n)
```

### 4. Is the input repeatedly divided?

```text
n → n/2 → n/4 → n/8
```

Usually:

```text
O(log n)
```

### 5. Is there recursion?

Look at:

- Number of recursive calls
- Number of levels
- Work performed at each level
- Recursion stack space

### 6. Is additional memory being created?

Look for:

- Arrays
- Objects
- Maps/Sets
- Temporary data structures
- Recursive call stack

These determine **space complexity**.

---

# 37. Most Important Mental Model

When learning Big O, remember:

```text
Big O = How does the cost grow as input grows?
```

Not:

```text
How many milliseconds does this code take?
```

Think about the **shape of the growth**.

```text
O(1)       → Doesn't grow
O(log n)   → Grows very slowly
O(n)       → Grows proportionally
O(n log n) → Grows faster than n
O(n²)      → Grows much faster
O(2ⁿ)      → Grows extremely fast
O(n!)      → Grows explosively
```

---

# 38. Final Takeaways

The most important concepts to remember:

1. **Big O describes asymptotic growth.**
2. **Time complexity** describes computational work.
3. **Space complexity** describes additional memory usage.
4. **O(1)** is constant.
5. **O(log n)** commonly appears when the search space is repeatedly divided.
6. **O(n)** means work grows linearly with the input.
7. **O(n log n)** is common in efficient sorting.
8. **O(n²)** commonly appears with nested loops.
9. **O(2ⁿ)** and **O(n!)** become impractical quickly.
10. Sequential operations are usually **added**.
11. Nested operations are usually **multiplied**.
12. Drop constants and non-dominant terms when simplifying asymptotic complexity.
13. Use different variables for independent input sizes: `O(a + b)`, `O(a × b)`, etc.
14. Big O is an **upper-bound notation**, while Big Ω represents a lower bound and Big Θ represents a tight bound.
15. Choosing the right **data structure and algorithm** can dramatically improve performance.

---

# 39. Learning Roadmap

A good order for learning Data Structures & Algorithms is:

```text
1. Big O
   ↓
2. Arrays & Strings
   ↓
3. Hash Maps & Sets
   ↓
4. Linked Lists
   ↓
5. Stacks & Queues
   ↓
6. Recursion
   ↓
7. Binary Search
   ↓
8. Trees & BST
   ↓
9. Heaps / Priority Queues
   ↓
10. Graphs
   ↓
11. BFS & DFS
   ↓
12. Sorting
   ↓
13. Two Pointers
   ↓
14. Sliding Window
   ↓
15. Greedy
   ↓
16. Backtracking
   ↓
17. Dynamic Programming
```

