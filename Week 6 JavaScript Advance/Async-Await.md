# JavaScript Async/Await

---

## 1. What is Async/Await?

**Async/Await** is a modern way to write **asynchronous code** in JavaScript that looks and behaves like **synchronous code**, making it easier to read and maintain.

* `async` keyword: Marks a function as asynchronous. This function **always returns a Promise**.
* `await` keyword: Pauses the execution of the `async` function until the Promise is **resolved or rejected**.

### Real-life Example

Think of it as ordering food and **waiting for it**:

* `async` = You go to the restaurant.
* `await` = You wait until the food arrives before you eat.

---

## 2. How to Use Async/Await

### Basic Example

```js
async function fetchData() {
  let response = await fetch('https://api.example.com/data');
  let data = await response.json();
  console.log(data);
}

fetchData();
```

* The code pauses at each `await` until the Promise is resolved.
* Easier to read than multiple `.then()` calls.

---

## 3. Error Handling with Try/Catch

```js
async function fetchData() {
  try {
    let response = await fetch('https://api.example.com/data');
    let data = await response.json();
    console.log(data);
  } catch (error) {
    console.error('Error fetching data:', error);
  }
}

fetchData();
```

* `try/catch` handles errors instead of `.catch()`.

---

## 4. Async/Await vs Promise Chain

| Feature        | Promise Chain    | Async/Await                |
| -------------- | ---------------- | -------------------------- |
| Syntax         | `.then().then()` | `async` function + `await` |
| Readability    | Medium           | Very readable              |
| Error Handling | `.catch()`       | `try/catch`                |
| Execution      | Sequential       | Sequential (with `await`)  |

---

## 5. Multiple Promises with Async/Await

### Sequential Execution

```js
async function runTasks() {
  let result1 = await task1();
  let result2 = await task2();
  console.log(result1, result2);
}
```

### Parallel Execution

```js
async function runTasks() {
  let [result1, result2] = await Promise.all([task1(), task2()]);
  console.log(result1, result2);
}
```

* Use `Promise.all` to run independent tasks in parallel.

---

## 6. Common Interview Questions

1. What is the difference between `async/await` and Promise chaining?
2. Can you use `await` outside an `async` function?
3. How do you handle errors with async/await?
4. How do you run multiple async tasks in parallel with async/await?
5. Explain a real-life example of async/await.

---

## 7. Practice Questions

1. Create an async function that fetches data from an API and logs it.
2. Rewrite a Promise chain using async/await.
3. Use `Promise.all` with async/await to run 3 API requests in parallel.
4. Handle an error in async function using try/catch.
5. Create 2 async functions, one depending on the result of the other, and log the final output.
