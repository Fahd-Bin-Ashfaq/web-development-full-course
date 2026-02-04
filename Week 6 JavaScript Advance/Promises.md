# JavaScript Promises

---

## 1. What is a Promise?

A **Promise** in JavaScript is an object that shows the result of an async task, whether it finishes successfully or fails.

### Promise States

1. **Pending** – Initial state, the operation is not yet completed.
2. **Fulfilled (Resolved)** – Operation completed successfully.
3. **Rejected** – Operation failed.

### Real-life Example

Ordering food at a restaurant:

* **Pending:** You placed your order.
* **Fulfilled:** The waiter serves your food.
* **Rejected:** The restaurant ran out of the dish.

---

## 2. Why and When to Use Promises?

Promises are used for **asynchronous operations**, like:

* Fetching data from a server (`fetch` API)
* Reading/writing files (Node.js)
* Timers (`setTimeout`, `setInterval`)
* Database queries

**Advantages:**

* Avoids **callback hell**
* Makes **async code readable**
* Easier **error handling** with `.catch()`

---

## 3. How to Create a Promise

```js
let myPromise = new Promise((resolve, reject) => {
  let success = true;

  if (success) {
    resolve("Task completed successfully");
  } else {
    reject("Task failed");
  }
});
```

* `resolve(value)` → marks promise as **fulfilled**
* `reject(error)` → marks promise as **rejected**

---

## 4. How to Use a Promise

```js
myPromise
  .then(result => console.log("Success:", result))
  .catch(error => console.log("Error:", error));
```

* `.then()` → executed if **fulfilled**
* `.catch()` → executed if **rejected**

---

## 5. Promise Chaining

Allows multiple async tasks to run **in sequence**:

```js
new Promise(resolve => resolve(5))
  .then(result => {
    console.log(result); // 5
    return result * 2;
  })
  .then(result => {
    console.log(result); // 10
    return result + 1;
  })
  .then(result => console.log(result)); // 11
```

**Use case:** Step-by-step operations where next task depends on previous result.

**Real-life example:** Login → Get Profile → Get Orders

---

## 6. Promise.all

Runs **multiple independent promises in parallel** and waits for **all to complete**.

```js
let p1 = new Promise(resolve => setTimeout(() => resolve("A"), 1000));
let p2 = new Promise(resolve => setTimeout(() => resolve("B"), 2000));
let p3 = new Promise(resolve => setTimeout(() => resolve("C"), 3000));

Promise.all([p1, p2, p3]).then(results => console.log(results)); // ["A", "B", "C"]
```

* Faster than chaining if tasks are independent.
* If any promise **rejects**, `Promise.all` rejects immediately.

---

## 7. Common Interview Questions

1. What are the states of a Promise?
2. Difference between **Promise chaining** and **Promise.all**?
3. Difference between **synchronous** and **asynchronous** code?
4. How do you handle errors in a Promise?
5. Can a Promise be resolved more than once?
6. Explain **callback hell** and how Promises help.
7. Difference between `.then().catch()` and `try/catch` with `async/await`.

---

## 8. Practice Questions

1. Create a promise that resolves after 2 seconds and prints "Task complete".
2. Chain 3 promises where each adds 5 to the previous value.
3. Use `Promise.all` to fetch data from 3 different APIs and log all results together.
4. Create a promise that rejects after 3 seconds and handle the error with `.catch()`.
5. Convert a callback-based function to return a promise and use chaining.
