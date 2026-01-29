# Callback Functions and Asynchronous Programming

## What is a Callback Function?

A **callback function** is a function that is passed as an argument to another function and is executed after a specific operation is completed. Callbacks are commonly used to manage **asynchronous operations** such as API requests, file handling, timers, and event handling.

In simple terms, a callback allows one function to notify another function when a task has finished.

---

## Why Callbacks Are Used

* To handle asynchronous operations efficiently
* To control the order of execution
* To prevent blocking the main execution thread

---

## Basic Callback Example (JavaScript)

```js
function greet(name, callback) {
  console.log("Hello " + name);
  callback();
}

function sayGoodbye() {
  console.log("Goodbye!");
}

greet("Fahad", sayGoodbye);
```

**Output:**

```
Hello Fahad
Goodbye!
```

---

## Callback with an Asynchronous Operation

```js
function fetchData(callback) {
  setTimeout(() => {
    console.log("Data fetched successfully");
    callback();
  }, 2000);
}

fetchData(() => {
  console.log("Processing data");
});
```

---

## Synchronous vs Asynchronous Programming

### Synchronous Programming

In **synchronous programming**, tasks are executed sequentially. Each operation must complete before the next one begins. This approach is straightforward but can be inefficient for long-running tasks.

**Real-life Example:**
An ATM machine processes one customer at a time. The next customer must wait until the current transaction is completed.

**Example:**

```js
console.log("Task 1");
console.log("Task 2");
console.log("Task 3");
```

**Output:**

```
Task 1
Task 2
Task 3
```

---

### Asynchronous Programming

In **asynchronous programming**, time-consuming tasks run in the background while the program continues executing other operations. This approach improves performance and responsiveness.

**Real-life Example:**
In a restaurant, you place an order and continue your conversation while the food is being prepared.

**Example:**

```js
console.log("Task 1");

setTimeout(() => {
  console.log("Task 2");
}, 2000);

console.log("Task 3");
```

**Output:**

```
Task 1
Task 3
Task 2
```

---

## Callback Hell

**Callback Hell** occurs when callbacks are deeply nested, making the code difficult to read, debug, and maintain.

```js
setTimeout(() => {
  console.log("Task 1");
  setTimeout(() => {
    console.log("Task 2");
    setTimeout(() => {
      console.log("Task 3");
    }, 1000);
  }, 1000);
}, 1000);
```

---

## Solutions to Callback Hell

* Use **Promises**
* Use **async / await**

These approaches improve readability and maintainability.

---

## Programming Languages That Support Asynchronous Programming

### JavaScript

* Callbacks
* Promises
* async / await

```js
async function fetchData() {
  await new Promise(resolve => setTimeout(resolve, 2000));
  console.log("Data received");
}

fetchData();
```

---

### Python

* asyncio module
* async / await
* threading and multiprocessing

```python
import asyncio

async def main():
    await asyncio.sleep(2)
    print("Hello from Async Python")

asyncio.run(main())
```

---

### Java

* Multithreading
* CompletableFuture

```java
CompletableFuture.runAsync(() -> {
    System.out.println("Asynchronous task running");
});
```

---

### C#

* async / await
* Task Parallel Library

```csharp
await Task.Delay(2000);
Console.WriteLine("Asynchronous programming in C#");
```

---

## Summary

* **Synchronous programming** executes tasks one at a time and may block execution
* **Asynchronous programming** allows tasks to run in the background, improving performance
* Callbacks enable asynchronous behavior but can lead to complexity if not managed properly
* Modern applications prefer Promises and async/await for cleaner code

---

📌 **Professional Tip:** Asynchronous programming is a core concept in modern web, mobile, and backend development and is frequently tested in technical interviews.
