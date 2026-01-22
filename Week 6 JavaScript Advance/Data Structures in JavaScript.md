# Data Structures in JavaScript

## Introduction

**Data Structures** are ways to **store, organize, and manage data efficiently** so it can be used easily.

### Real-Life Analogy

* Books on shelves → arranged properly = easy access
* Contacts in a phone → structured data

In programming, choosing the right data structure improves **performance, readability, and scalability**.

---

## Why Data Structures Are Important

* Efficient data handling
* Faster operations (search, insert, delete)
* Core topic for interviews
* Foundation of problem-solving

---

## Common Data Structures in JavaScript

1. Array
2. Object
3. Stack
4. Queue
5. Set
6. Map
7. Linked List (basic concept)

---

## 1. Array

Stores ordered data (indexed).

```js
let arr = [10, 20, 30];
```

### Use Cases

* Lists of items
* Iteration & calculations

---

## 2. Object

Stores data in **key–value pairs**.

```js
let user = {
  name: "Fahad",
  age: 22
};
```

### Use Cases

* User profiles
* API responses

---

## 3. Stack (LIFO)

**Last In, First Out**

### Real-Life Example

* Browser back button
* Stack of plates

### Implementation (Using Array)

```js
let stack = [];
stack.push(1);
stack.push(2);
stack.pop();
```

---

## 4. Queue (FIFO)

**First In, First Out**

### Real-Life Example

* Line at a bank
* Print queue

### Implementation

```js
let queue = [];
queue.push(1);
queue.push(2);
queue.shift();
```

---

## 5. Set

Stores **unique values only**.

```js
let mySet = new Set([1, 2, 2, 3]);
console.log(mySet);
```

### Use Cases

* Remove duplicates
* Track unique items

---

## 6. Map

Stores **key–value pairs** with better performance than objects.

```js
let myMap = new Map();
myMap.set("name", "Fahad");
myMap.set("age", 22);
```

### Difference Between Map & Object

| Feature   | Map       | Object        |
| --------- | --------- | ------------- |
| Key types | Any       | String/Symbol |
| Order     | Maintains | No guarantee  |

---

## 7. Linked List (Conceptual)

Each element points to the next element.

### Real-Life Example

* Train compartments

### Node Structure

```js
{
  value: 10,
  next: null
}
```

📌 Mostly used in interviews (conceptual understanding is enough).

---

## Time Complexity Basics

| Operation | Array | Object |
| --------- | ----- | ------ |
| Access    | O(1)  | O(1)   |
| Search    | O(n)  | O(1)   |

---

## Choosing the Right Data Structure

* Ordered data → Array
* Structured data → Object
* Undo/Redo → Stack
* Scheduling → Queue
* Unique values → Set
* Fast key access → Map

---

## Practice Questions

### Basic

1. Create an array and print all elements
2. Create an object for student details

### Intermediate

3. Implement stack using array
4. Implement queue using array

### Advanced

5. Remove duplicates using Set
6. Store and retrieve values using Map

---

## Mini Assignment

Create a **student management system** using:

* Array to store students
* Object for student details
* Stack for undo feature

---

## Key Takeaways

* Data structures organize data efficiently
* Arrays & objects are most common
* Stack & queue are logical structures
* Set & Map are modern JS tools

---

Happy Coding 🚀
