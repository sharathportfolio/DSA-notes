# Classes, References & Garbage Collection

# 1. Classes

A **class** is like a **cookie cutter / mold**.

The class defines the structure and behavior, while the objects are the actual cookies created from that mold.

```text
Class
  ↓
Cookie Cutter / Mold
  ↓
Creates Objects
```

For example:

```javascript
class Cookie {
  constructor(color) {
    this.color = color;
  }

  getColor() {
    return this.color;
  }

  setColor(color) {
    this.color = color;
  }
}
```

The `Cookie` class is the mold.

We can create multiple cookie objects from it:

```javascript
const cookieOne = new Cookie("green");
const cookieTwo = new Cookie("blue");
```

Now:

```text
cookieOne → { color: "green" }
cookieTwo → { color: "blue" }
```

Both objects were created from the same class, but they contain different data.

---

# 2. Constructor

The `constructor()` method runs automatically when we create a new object using `new`.

```javascript
class Cookie {
  constructor(color) {
    this.color = color;
  }
}
```

When we do:

```javascript
const cookieOne = new Cookie("green");
```

JavaScript automatically calls:

```javascript
constructor("green")
```

So:

```text
cookieOne
   ↓
{ color: "green" }
```

---

# 3. `this`

`this` refers to the **current object**.

Example:

```javascript
class Cookie {
  constructor(color) {
    this.color = color;
  }
}
```

When:

```javascript
const cookieOne = new Cookie("green");
```

Think of:

```text
this → cookieOne
```

Therefore:

```javascript
this.color = color;
```

becomes conceptually:

```javascript
cookieOne.color = "green";
```

---

# 4. Class Methods

Methods are functions defined inside a class.

```javascript
class Cookie {
  constructor(color) {
    this.color = color;
  }

  getColor() {
    return this.color;
  }

  setColor(color) {
    this.color = color;
  }
}
```

### `getColor()`

Used to read the color:

```javascript
const cookie = new Cookie("green");

console.log(cookie.getColor());
// green
```

### `setColor()`

Used to change the color:

```javascript
cookie.setColor("blue");

console.log(cookie.getColor());
// blue
```

---

# 5. Creating Objects from a Class

Use the `new` keyword.

```javascript
const cookieOne = new Cookie("green");
const cookieTwo = new Cookie("red");
const cookieThree = new Cookie("blue");
```

Each object has its own data:

```text
cookieOne   → green
cookieTwo   → red
cookieThree → blue
```

But they all follow the same structure defined by the `Cookie` class.

---

# 6. Class Example

```javascript
class Cookie {
  constructor(color) {
    this.color = color;
  }

  getColor() {
    return this.color;
  }

  setColor(color) {
    this.color = color;
  }
}

const cookieOne = new Cookie("green");

console.log(cookieOne.getColor());
// green

cookieOne.setColor("blue");

console.log(cookieOne.getColor());
// blue
```

---

# 7. Classes and Linked Lists

A Linked List can also be represented using classes.

A Linked List is made up of **nodes**.

Each node contains:

```text
Value
Next → reference to another node
```

Example:

```text
[10] → [20] → [30] → null
```

Each box is a Node.

---

# 8. Node Class

A simple Node can be created using a class:

```javascript
class Node {
  constructor(value) {
    this.value = value;
    this.next = null;
  }
}
```

Create a node:

```javascript
const nodeOne = new Node(10);
```

It looks conceptually like:

```text
nodeOne
   ↓
┌──────────────┐
│ value: 10    │
│ next: null   │
└──────────────┘
```

Create another:

```javascript
const nodeTwo = new Node(20);
```

Connect them:

```javascript
nodeOne.next = nodeTwo;
```

Now:

```text
nodeOne
   ↓
[10] → [20] → null
```

---

# 9. Linked List Class

Instead of managing nodes manually, we can create a `LinkedList` class.

```javascript
class LinkedList {
  constructor(value) {
    const newNode = new Node(value);

    this.head = newNode;
    this.tail = newNode;
    this.length = 1;
  }

  push(value) {
    // Add node to the end
  }

  unshift(value) {
    // Add node to the beginning
  }

  insert(index, value) {
    // Add node at a specific index
  }

  remove(index) {
    // Remove node at a specific index
  }

  pop() {
    // Remove last node
  }

  shift() {
    // Remove first node
  }
}
```

The Linked List keeps track of:

```text
head
tail
length
```

Example:

```text
head
 ↓
[23] → [7] → [11] → null
                   ↑
                  tail
```

---

# 10. Using the Linked List

```javascript
const myLinkedList = new LinkedList(23);

myLinkedList.push(7);

myLinkedList.unshift(3);

myLinkedList.insert(1, 11);

myLinkedList.remove(1);

myLinkedList.pop();

myLinkedList.shift();
```

Each method changes the linked list.

Typical operations:

```text
push(value)
→ Add to end

pop()
→ Remove from end

unshift(value)
→ Add to beginning

shift()
→ Remove from beginning

insert(index, value)
→ Add at specific index

remove(index)
→ Remove at specific index
```

---

# 11. What is a Pointer?

In languages such as C/C++, a pointer is a variable that directly stores a memory address.

JavaScript does not expose raw memory pointers like C/C++.

However, JavaScript objects and arrays are **reference values**, so variables can hold references to the same object.

For learning DSA, people often casually call these references "pointers."

---

# 12. Primitive Values vs References

This is one of the most important JavaScript concepts.

## Primitive Values

Examples:

```text
number
string
boolean
null
undefined
bigint
symbol
```

When primitive values are assigned, the value itself is copied.

Example:

```javascript
let num1 = 5;
let num2 = num1;
```

Think:

```text
num1 → 5
num2 → 5
```

Now change `num1`:

```javascript
num1 = 10;
```

Result:

```text
num1 → 10
num2 → 5
```

`num2` is still `5`.

---

# 13. Reference Values

Objects behave differently.

Example:

```javascript
let obj1 = {
  value: 11
};

let obj2 = obj1;
```

Here, `obj1` and `obj2` refer to the **same object**.

Conceptually:

```text
          ┌──────────────┐
obj1 ───→ │ value: 11   │
          │              │
obj2 ───→ │              │
          └──────────────┘
```

There is only **one object**.

There are two variables referring to it.

---

# 14. Changing the Object

Now:

```javascript
obj1.value = 22;
```

Because `obj1` and `obj2` refer to the same object:

```javascript
console.log(obj1.value);
// 22

console.log(obj2.value);
// 22
```

Conceptually:

```text
          ┌──────────────┐
obj1 ───→ │ value: 22   │
          │              │
obj2 ───→ │              │
          └──────────────┘
```

Both see the same change.

---

# 15. Important Difference

## Primitive

```javascript
let num1 = 5;
let num2 = num1;

num1 = 10;
```

Result:

```text
num1 → 10
num2 → 5
```

They contain independent primitive values.

---

## Object

```javascript
let obj1 = {
  value: 11
};

let obj2 = obj1;

obj1.value = 22;
```

Result:

```text
obj1 ──┐
       ↓
    { value: 22 }
       ↑
       │
obj2 ──┘
```

Both variables refer to the same object.

---

# 16. Reassigning vs Mutating

This distinction is extremely important.

### Mutating the object

```javascript
obj1.value = 22;
```

Changes the existing object.

```text
obj1 ──┐
       ↓
    { value: 22 }
       ↑
       │
obj2 ──┘
```

So `obj2.value` is also `22`.

---

### Reassigning the variable

```javascript
obj1 = {
  value: 33
};
```

Now `obj1` points to a **different object**.

```text
obj1 ──→ { value: 33 }


obj2 ──→ { value: 22 }
```

`obj2` still points to the original object.

---

# 17. Example: Reassignment

```javascript
let obj1 = {
  value: 11
};

let obj2 = obj1;

obj1.value = 22;

console.log(obj1.value);
// 22

console.log(obj2.value);
// 22
```

Now:

```javascript
obj1 = {
  value: 33
};
```

Result:

```javascript
console.log(obj1.value);
// 33

console.log(obj2.value);
// 22
```

Why?

Because:

```text
obj1 → new object
obj2 → old object
```

---

# 18. Visualizing References

Start:

```javascript
let obj1 = {
  value: 11
};

let obj2 = obj1;
```

Think:

```text
obj1 ─────┐
          ↓
       ┌─────────┐
       │ value:11│
       └─────────┘
          ↑
          │
obj2 ─────┘
```

After:

```javascript
obj1.value = 22;
```

```text
obj1 ─────┐
          ↓
       ┌─────────┐
       │ value:22│
       └─────────┘
          ↑
          │
obj2 ─────┘
```

After:

```javascript
obj1 = {
  value: 33
};
```

```text
obj1 ─────→ ┌─────────┐
            │ value:33│
            └─────────┘


obj2 ─────→ ┌─────────┐
            │ value:22│
            └─────────┘
```

---

# 19. Why References Matter in Linked Lists

References are the foundation of a Linked List.

Consider:

```javascript
class Node {
  constructor(value) {
    this.value = value;
    this.next = null;
  }
}
```

Create two nodes:

```javascript
const node1 = new Node(10);
const node2 = new Node(20);
```

Connect them:

```javascript
node1.next = node2;
```

Now:

```text
node1
 ↓
┌──────────────┐
│ value: 10    │
│ next ────────┼─────┐
└──────────────┘     │
                     ↓
                ┌──────────────┐
                │ value: 20    │
                │ next: null   │
                └──────────────┘
```

This is how nodes are connected.

The `next` property holds a **reference to another node**.

---

# 20. Garbage Collection

**Garbage Collection (GC)** is JavaScript's automatic memory-management system.

The JavaScript runtime automatically identifies objects that are no longer reachable by the program and can reclaim their memory.

You generally do not manually free objects in JavaScript.

---

# 21. Example of Garbage Collection

```javascript
let user = {
  name: "John"
};
```

Conceptually:

```text
user ──→ { name: "John" }
```

Now:

```javascript
user = null;
```

The object may become unreachable:

```text
user → null

{ name: "John" }   ← no reference
```

Because the object is no longer reachable, the garbage collector can eventually reclaim its memory.

> The exact timing of garbage collection is controlled by the JavaScript engine. You should not assume it happens immediately.

---

# 22. Multiple References and Garbage Collection

Consider:

```javascript
let obj1 = {
  value: 10
};

let obj2 = obj1;
```

There are two references:

```text
obj1 ──┐
       ↓
    { value: 10 }
       ↑
       │
obj2 ──┘
```

Now:

```javascript
obj1 = null;
```

The object is still reachable through `obj2`:

```text
obj1 → null

obj2 ──→ { value: 10 }
```

Therefore, the object **cannot be garbage collected yet**.

Now:

```javascript
obj2 = null;
```

There are no remaining references:

```text
obj1 → null

obj2 → null

{ value: 10 } ← unreachable
```

The garbage collector can eventually reclaim that memory.

---

# 23. Reachability — The Key Idea

The important concept behind garbage collection is:

```text
Can the program still reach this object?
```

If yes:

```text
Object is reachable
→ Keep it
```

If no:

```text
Object is unreachable
→ Can be garbage collected
```

