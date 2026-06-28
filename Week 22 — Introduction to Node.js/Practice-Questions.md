# Week 22 — Introduction to Node.js: Practice Questions

**Total Questions: 20** (10 MCQs + 5 Short Answer + 5 Coding Exercises)

---

## Part 1: Multiple Choice Questions (MCQs)

**1. What is Node.js?**

- A) A web browser for running JavaScript
- B) A JavaScript runtime built on Chrome's V8 engine
- C) A JavaScript framework like React
- D) A database management system

<details>
<summary>Answer</summary>

**B) A JavaScript runtime built on Chrome's V8 engine**

Node.js is a runtime environment that allows JavaScript to run outside the browser. It was created by Ryan Dahl in 2009 and uses Google Chrome's V8 engine to compile JavaScript into fast machine code.
</details>

---

**2. Which global object is available in Node.js but NOT in the browser?**

- A) `console`
- B) `window`
- C) `process`
- D) `JSON`

<details>
<summary>Answer</summary>

**C) `process`**

The `process` object is unique to Node.js and provides information about the current running process, including environment variables (`process.env`), command-line arguments (`process.argv`), and the Node.js version (`process.version`). The `window` object exists only in the browser.
</details>

---

**3. Which core module is used to read and write files in Node.js?**

- A) `http`
- B) `path`
- C) `os`
- D) `fs`

<details>
<summary>Answer</summary>

**D) `fs`**

The `fs` (file system) module provides methods to interact with the file system, including `readFile`, `writeFile`, `appendFile`, `unlink` (delete), and many more.
</details>

---

**4. What is the correct way to import a module using CommonJS?**

- A) `import fs from "fs"`
- B) `const fs = require("fs")`
- C) `include("fs")`
- D) `using fs = "fs"`

<details>
<summary>Answer</summary>

**B) `const fs = require("fs")`**

CommonJS uses the `require()` function to import modules. This is the original module system in Node.js. ES Modules (`import/export`) are the modern alternative but require either `"type": "module"` in `package.json` or the `.mjs` file extension.
</details>

---

**5. What does the following code output?**

```javascript
console.log("A");
setTimeout(() => console.log("B"), 0);
console.log("C");
```

- A) A, B, C
- B) A, C, B
- C) B, A, C
- D) C, A, B

<details>
<summary>Answer</summary>

**B) A, C, B**

Even with a delay of 0 milliseconds, `setTimeout` is an asynchronous function. Its callback is placed in the callback queue and only executed after the call stack is empty. So `"A"` and `"C"` print first (synchronous), then `"B"` prints (asynchronous callback).
</details>

---

**6. Which method creates an HTTP server in Node.js?**

- A) `http.listen()`
- B) `http.createServer()`
- C) `http.newServer()`
- D) `http.start()`

<details>
<summary>Answer</summary>

**B) `http.createServer()`**

The `http.createServer()` method creates a new HTTP server. It takes a callback function with `request` and `response` parameters. You then call `.listen(port)` on the returned server object to start listening for connections.
</details>

---

**7. What does `path.join("users", "docs", "file.txt")` return on Windows?**

- A) `users/docs/file.txt`
- B) `users\docs\file.txt`
- C) `/users/docs/file.txt`
- D) `users.docs.file.txt`

<details>
<summary>Answer</summary>

**B) `users\docs\file.txt`**

The `path.join()` method joins path segments using the correct separator for the operating system. On Windows, it uses backslashes (`\`). On macOS and Linux, it uses forward slashes (`/`). This is why you should always use `path.join()` instead of manually concatenating paths with `/` or `\`.
</details>

---

**8. Which statement about Node.js is TRUE?**

- A) Node.js is multi-threaded by default
- B) Node.js can access the DOM
- C) Node.js uses an event-driven, non-blocking I/O model
- D) Node.js can only run on Linux servers

<details>
<summary>Answer</summary>

**C) Node.js uses an event-driven, non-blocking I/O model**

Node.js is single-threaded and uses a non-blocking I/O model powered by the event loop. This allows it to handle many concurrent connections efficiently without creating a new thread for each request. It cannot access the DOM (that is browser-only) and it runs on Windows, macOS, and Linux.
</details>

---

**9. What is the difference between `fs.readFileSync()` and `fs.readFile()`?**

- A) `readFileSync` is faster
- B) `readFile` is synchronous, `readFileSync` is asynchronous
- C) `readFileSync` blocks execution until the file is read; `readFile` does not block
- D) There is no difference

<details>
<summary>Answer</summary>

**C) `readFileSync` blocks execution until the file is read; `readFile` does not block**

`readFileSync` is synchronous — it pauses all other code execution until the file is fully read. `readFile` is asynchronous — it delegates the file reading to the system and continues executing the next lines of code. When the file is ready, it calls the provided callback function.
</details>

---

**10. To use ES Modules (`import`/`export`) in Node.js, you must:**

- A) Install a special package
- B) Add `"type": "module"` to `package.json` or use `.mjs` extension
- C) Use Node.js version 8 or older
- D) Wrap your code in `<script type="module">`

<details>
<summary>Answer</summary>

**B) Add `"type": "module"` to `package.json` or use `.mjs` extension**

By default, Node.js uses CommonJS modules. To enable ES Modules, you either set `"type": "module"` in your `package.json` (which makes all `.js` files in the project use ES Module syntax) or rename individual files to use the `.mjs` extension.
</details>

---

## Part 2: Short Answer Questions

**1. Explain the restaurant analogy for backend development in your own words. What does the "kitchen" represent, and why does the customer never see it?**

<details>
<summary>Answer</summary>

In the restaurant analogy, the **dining area** represents the frontend — it is what the customer (user) sees and interacts with, including the menu (UI), tables (layout), and waiters (browser). The **kitchen** represents the backend — it is where the actual work happens: chefs (server logic) prepare food (process data), follow recipes (business rules), and manage the pantry (database).

The customer never sees the kitchen because the backend operates behind the scenes. Users interact only with the frontend, which communicates with the backend through HTTP requests. Just as the waiter carries orders to the kitchen and delivers food back, the browser sends requests to the server and receives responses.
</details>

---

**2. What is the V8 engine, and why is it important to Node.js?**

<details>
<summary>Answer</summary>

The **V8 engine** is an open-source JavaScript engine developed by Google for the Chrome browser. It compiles JavaScript directly into machine code (instead of interpreting it line by line), which makes execution extremely fast.

V8 is important to Node.js because it is the foundation that allows JavaScript to run outside the browser. Ryan Dahl chose V8 when building Node.js in 2009 because of its speed and performance. Without V8, Node.js would not be able to compile and execute JavaScript at the speeds required for server-side applications.
</details>

---

**3. What is the Event Loop in Node.js? Why does it matter for server performance?**

<details>
<summary>Answer</summary>

The **Event Loop** is a mechanism in Node.js that continuously checks whether the call stack is empty and, if so, moves callbacks from the callback queue to the call stack for execution. It is the core of Node.js's non-blocking architecture.

It matters for server performance because it allows Node.js to handle thousands of concurrent connections using a single thread. Instead of creating a new thread for each request (which consumes memory), Node.js delegates slow operations (file I/O, database queries, network calls) to the system and continues processing other requests. When the slow operation completes, its callback is placed in the queue and eventually executed by the event loop. This makes Node.js highly efficient for I/O-heavy applications.
</details>

---

**4. What is the difference between CommonJS and ES Modules? When would you use each?**

<details>
<summary>Answer</summary>

**CommonJS** uses `require()` to import and `module.exports` to export. It loads modules **synchronously** and has been the default module system in Node.js since its creation. It is widely used in existing Node.js projects and supports dynamic imports (you can call `require()` inside `if` blocks).

**ES Modules** use `import` and `export` syntax. They load modules **asynchronously** and support top-level `await`. They are the modern JavaScript standard, work natively in browsers, and allow static analysis (tools can optimize imports at build time).

**When to use each:** Use ES Modules for new projects — they are the modern standard and offer better tooling support. Use CommonJS when working with legacy Node.js projects that already use `require()`, or when a library only supports CommonJS.
</details>

---

**5. Why should you use `path.join()` instead of manually writing file paths like `"folder/file.txt"`?**

<details>
<summary>Answer</summary>

You should use `path.join()` because different operating systems use different path separators. Windows uses backslashes (`\`) while macOS and Linux use forward slashes (`/`). If you manually write `"folder/file.txt"`, your code may break on Windows.

`path.join()` automatically uses the correct separator for the operating system where the code is running. For example, `path.join("users", "docs", "file.txt")` produces `users\docs\file.txt` on Windows and `users/docs/file.txt` on macOS/Linux. This makes your code portable and reliable across all platforms.
</details>

---

## Part 3: Coding Exercises

**1. File Reader — Read and display a file's contents**

Create a file called `message.txt` with the text "Hello from Node.js!" inside it. Then write a Node.js script that reads this file asynchronously and prints its content to the console. Handle any errors that might occur (for example, if the file does not exist).

<details>
<summary>Answer</summary>

```javascript
// exercise1.js
const fs = require("fs");

// First, create the file
fs.writeFileSync("message.txt", "Hello from Node.js!");

// Then, read it asynchronously
fs.readFile("message.txt", "utf-8", (error, data) => {
  if (error) {
    console.error("Error reading file:", error.message);
    return;
  }
  console.log("File contents:", data);
});
```

**Expected output:**
```
File contents: Hello from Node.js!
```

**Key concepts:** Using `fs.readFile()` for asynchronous file reading, passing `"utf-8"` encoding to get a string (instead of a Buffer), and handling potential errors with the error-first callback pattern.
</details>

---

**2. File Writer — Create a to-do list file**

Write a Node.js script that creates a file called `todo.txt` and writes three to-do items to it (each on a new line). Then append two more items to the same file. Finally, read the file and print all five items.

<details>
<summary>Answer</summary>

```javascript
// exercise2.js
const fs = require("fs");

// Write initial to-do items
const initialTodos = `1. Learn Node.js basics
2. Practice file system operations
3. Build an HTTP server
`;

fs.writeFileSync("todo.txt", initialTodos);
console.log("Initial to-do items written.");

// Append more items
const moreTodos = `4. Understand the Event Loop
5. Learn about npm packages
`;

fs.appendFileSync("todo.txt", moreTodos);
console.log("Additional items appended.");

// Read and display all items
const allTodos = fs.readFileSync("todo.txt", "utf-8");
console.log("\nMy To-Do List:");
console.log(allTodos);
```

**Expected output:**
```
Initial to-do items written.
Additional items appended.

My To-Do List:
1. Learn Node.js basics
2. Practice file system operations
3. Build an HTTP server
4. Understand the Event Loop
5. Learn about npm packages
```

**Key concepts:** `writeFileSync` creates a new file (or overwrites existing content), `appendFileSync` adds content to the end without erasing existing data, and `readFileSync` reads the full file.
</details>

---

**3. System Information Reporter**

Write a Node.js script that uses the `os` and `path` modules to display the following system information: platform, CPU architecture, number of CPU cores, total memory (in GB), home directory, and the absolute path to the current script file.

<details>
<summary>Answer</summary>

```javascript
// exercise3.js
const os = require("os");
const path = require("path");

console.log("=== System Information ===");
console.log(`Platform:      ${os.platform()}`);
console.log(`Architecture:  ${os.arch()}`);
console.log(`CPU Cores:     ${os.cpus().length}`);
console.log(`Total Memory:  ${(os.totalmem() / 1024 / 1024 / 1024).toFixed(2)} GB`);
console.log(`Free Memory:   ${(os.freemem() / 1024 / 1024 / 1024).toFixed(2)} GB`);
console.log(`Home Directory: ${os.homedir()}`);
console.log(`Script Path:   ${path.resolve(__filename)}`);
console.log(`Script Name:   ${path.basename(__filename)}`);
console.log(`Script Dir:    ${path.dirname(__filename)}`);
```

**Example output:**
```
=== System Information ===
Platform:      win32
Architecture:  x64
CPU Cores:     8
Total Memory:  16.00 GB
Free Memory:   8.45 GB
Home Directory: C:\Users\fahad
Script Path:   C:\Users\fahad\projects\exercise3.js
Script Name:   exercise3.js
Script Dir:    C:\Users\fahad\projects
```

**Key concepts:** Using `os` methods to retrieve system data, converting bytes to gigabytes with division, and using `path.resolve()`, `path.basename()`, and `path.dirname()` to work with file paths.
</details>

---

**4. Basic HTTP Server — Serve different responses based on the URL**

Create an HTTP server that listens on port 3000 and responds to three routes:
- `/` returns `"Welcome to the Home Page"`
- `/about` returns `"This is the About Page"`
- Any other URL returns `"404 — Page Not Found"` with a 404 status code

<details>
<summary>Answer</summary>

```javascript
// exercise4.js
const http = require("http");

const server = http.createServer((req, res) => {
  if (req.url === "/" && req.method === "GET") {
    res.writeHead(200, { "Content-Type": "text/plain" });
    res.end("Welcome to the Home Page");

  } else if (req.url === "/about" && req.method === "GET") {
    res.writeHead(200, { "Content-Type": "text/plain" });
    res.end("This is the About Page");

  } else {
    res.writeHead(404, { "Content-Type": "text/plain" });
    res.end("404 — Page Not Found");
  }
});

server.listen(3000, () => {
  console.log("Server running at http://localhost:3000");
});
```

**Testing:**
- Visit `http://localhost:3000/` in your browser to see the home page message.
- Visit `http://localhost:3000/about` to see the about page message.
- Visit `http://localhost:3000/anything-else` to see the 404 error.

**Key concepts:** Using `http.createServer()` to handle incoming requests, checking `req.url` and `req.method` to determine routing, setting appropriate status codes with `res.writeHead()`, and starting the server with `server.listen()`.
</details>

---

**5. JSON API Server**

Create an HTTP server that responds to `/api/students` with a JSON array containing three student objects (each with `id`, `name`, and `grade` properties). The response should have the correct `Content-Type` header set to `application/json`. For any other route, return a JSON error message with a 404 status code.

<details>
<summary>Answer</summary>

```javascript
// exercise5.js
const http = require("http");

const students = [
  { id: 1, name: "Ali Ahmed", grade: "A" },
  { id: 2, name: "Sara Khan", grade: "B+" },
  { id: 3, name: "Omar Farooq", grade: "A-" }
];

const server = http.createServer((req, res) => {
  res.setHeader("Content-Type", "application/json");

  if (req.url === "/api/students" && req.method === "GET") {
    res.writeHead(200);
    res.end(JSON.stringify({
      success: true,
      count: students.length,
      data: students
    }));

  } else {
    res.writeHead(404);
    res.end(JSON.stringify({
      success: false,
      error: "Endpoint not found. Try GET /api/students"
    }));
  }
});

server.listen(3000, () => {
  console.log("JSON API server running at http://localhost:3000");
  console.log("Try: http://localhost:3000/api/students");
});
```

**Expected response at `/api/students`:**
```json
{
  "success": true,
  "count": 3,
  "data": [
    { "id": 1, "name": "Ali Ahmed", "grade": "A" },
    { "id": 2, "name": "Sara Khan", "grade": "B+" },
    { "id": 3, "name": "Omar Farooq", "grade": "A-" }
  ]
}
```

**Key concepts:** Setting `Content-Type` to `application/json` for API responses, using `JSON.stringify()` to convert JavaScript objects to JSON strings, structuring API responses with `success`, `count`, and `data` fields, and handling unknown routes with proper error messages.
</details>

---

> **Tip:** After completing these exercises, try combining them. For example, build an HTTP server that reads data from a JSON file using the `fs` module and serves it at an API endpoint. This combines file operations with server creation — a pattern you will use constantly in backend development.
