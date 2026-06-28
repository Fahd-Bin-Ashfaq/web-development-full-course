# Week 22 — Introduction to Node.js

> **Prerequisites:** HTML, CSS, JavaScript (ES6+), React fundamentals
> **Goal:** Understand what backend development is, install Node.js, and write your first server-side JavaScript programs.

---

## Table of Contents

1. [What is Backend Development?](#1-what-is-backend-development)
2. [What is Node.js?](#2-what-is-nodejs)
3. [Node.js vs Browser JavaScript](#3-nodejs-vs-browser-javascript)
4. [Installing Node.js](#4-installing-nodejs)
5. [Running JavaScript Files with Node](#5-running-javascript-files-with-node)
6. [Core Modules](#6-core-modules)
7. [CommonJS vs ES Modules](#7-commonjs-vs-es-modules)
8. [Creating an HTTP Server](#8-creating-an-http-server)
9. [The Event Loop](#9-the-event-loop)
10. [Summary](#10-summary)

---

## 1. What is Backend Development?

Every web application has two halves: the **frontend** (what users see and interact with) and the **backend** (the engine that processes data, stores information, and enforces business rules behind the scenes).

> Think of a **restaurant**. The **dining area** is the frontend — customers see the menu, place orders, and receive food. The **kitchen** is the backend — chefs receive orders, cook food, manage inventory, and ensure everything is prepared correctly. The customer never sees the kitchen, but without it, the restaurant cannot function.

```
             THE RESTAURANT ANALOGY
  =============================================

   FRONTEND (Dining Area)          BACKEND (Kitchen)
  +---------------------+        +---------------------+
  |                     |        |                     |
  |   Menu (UI)         |        |   Chef (Server)     |
  |   Waiter (Browser)  | -----> |   Recipes (Logic)   |
  |   Table (Layout)    | <----- |   Pantry (Database)  |
  |   Customer (User)   |        |   Inventory (Auth)  |
  |                     |        |                     |
  +---------------------+        +---------------------+

   - Customer places order  -->  Kitchen receives order
   - Kitchen prepares food  -->  Waiter delivers to table
   - Customer never enters the kitchen
```

### What Does a Backend Do?

| Responsibility         | Example                                                        |
|------------------------|----------------------------------------------------------------|
| **Process requests**   | When you click "Login," the backend checks your password.      |
| **Store data**         | Your profile picture, posts, and settings live in a database.  |
| **Authentication**     | The backend verifies who you are and what you can access.      |
| **Business logic**     | Calculating shipping costs, applying discounts, sending emails.|
| **Serve files**        | Delivering HTML, CSS, JS, and images to the browser.           |

### The Client-Server Model

```
  +----------+    HTTP Request     +----------+     Query      +----------+
  |          | ------------------> |          | -------------> |          |
  |  CLIENT  |  "GET /products"    |  SERVER  |  "SELECT * .." | DATABASE |
  | (Browser)|                     | (Node.js)|                | (MongoDB)|
  |          | <------------------ |          | <------------- |          |
  +----------+    HTTP Response    +----------+     Results    +----------+
                  (JSON data)
```

Until now, you have been building the **client** side. Starting this week, you will learn to build the **server** side.

---

## 2. What is Node.js?

**Node.js** is a **JavaScript runtime environment** that lets you run JavaScript **outside the browser** — on your computer, on a server, or anywhere a machine runs.

### A Brief History

- **2009:** Ryan Dahl created Node.js because he was frustrated with how Apache (a popular web server) handled multiple connections. Apache created a new thread for each connection, which consumed a lot of memory. Ryan wanted a server that could handle thousands of connections using a single thread.
- **Engine:** Node.js is built on Google Chrome's **V8 JavaScript engine** — the same engine that makes Chrome fast at running JavaScript.
- **Key idea:** Instead of waiting for one task to finish before starting the next (blocking), Node.js uses an **event-driven, non-blocking** model that can handle many operations simultaneously.

### How Node.js Works

```
  +-----------------------------------------------------------+
  |                        Node.js                             |
  |  +-----------------------------------------------------+  |
  |  |                   V8 Engine                          |  |
  |  |  (Compiles JavaScript to machine code)               |  |
  |  +-----------------------------------------------------+  |
  |  +-----------------------------------------------------+  |
  |  |                   libuv                              |  |
  |  |  (Handles async I/O: files, network, timers)         |  |
  |  +-----------------------------------------------------+  |
  |  +-----------------------------------------------------+  |
  |  |              Core Modules (Built-in)                 |  |
  |  |  fs | path | os | http | events | crypto | ...       |  |
  |  +-----------------------------------------------------+  |
  +-----------------------------------------------------------+
```

### Real-World Companies Using Node.js

| Company     | How They Use Node.js                                      |
|-------------|-----------------------------------------------------------|
| **Netflix** | Reduced startup time from 10 minutes to under 1 minute.   |
| **PayPal**  | Handles 2x more requests per second than their Java setup. |
| **LinkedIn**| Moved from Ruby to Node.js, reduced servers from 30 to 3. |
| **Uber**    | Handles millions of real-time ride requests.               |
| **NASA**    | Reduced data access time from 24 hours to 15 minutes.      |

---

## 3. Node.js vs Browser JavaScript

JavaScript is the same language in both environments, but the **capabilities** differ because the host environment provides different global objects and APIs.

| Feature                   | Browser JavaScript            | Node.js                           |
|---------------------------|-------------------------------|-----------------------------------|
| **Primary purpose**       | Manipulate web pages (DOM)    | Run server-side applications      |
| **Global object**         | `window`                      | `global` (or `globalThis`)        |
| **DOM access**            | Yes (`document.querySelector`)| No (no DOM exists)                |
| **File system access**    | No (security restriction)     | Yes (`fs` module)                 |
| **Module system**         | ES Modules (`import/export`)  | CommonJS + ES Modules             |
| **HTTP server**           | Cannot create one             | Built-in `http` module            |
| **Console**               | Browser DevTools              | Terminal / Command Line           |
| **User interaction**      | `alert()`, `prompt()`         | Not available                     |
| **Package manager**       | None (uses CDN or bundlers)   | npm (built-in)                    |
| **Process access**        | No                            | Yes (`process` object)            |

```
  BROWSER JAVASCRIPT                    NODE.js JAVASCRIPT
  +-------------------------+          +-------------------------+
  |  window                 |          |  global                 |
  |  document               |          |  process                |
  |  alert() / prompt()     |          |  __dirname / __filename |
  |  fetch()                |          |  require()              |
  |  localStorage           |          |  fs / path / os / http  |
  |  DOM manipulation       |          |  Buffer                 |
  |  Event listeners (click)|          |  Streams                |
  +-------------------------+          +-------------------------+

  SHARED (Available in Both):
  +-------------------------+
  |  console.log()          |
  |  setTimeout/setInterval |
  |  JSON.parse/stringify   |
  |  Promise / async-await  |
  |  Array, Object, String  |
  |  Math, Date, RegExp     |
  +-------------------------+
```

---

## 4. Installing Node.js

### Step 1: Download

Visit [https://nodejs.org](https://nodejs.org) and download the **LTS (Long Term Support)** version. LTS is recommended because it receives security updates and is more stable than the "Current" version.

### Step 2: Verify Installation

Open your terminal (Command Prompt, PowerShell, or any terminal) and run:

```bash
node --version
# Example output: v20.11.0

npm --version
# Example output: 10.2.4
```

If both commands print version numbers, Node.js and npm are installed correctly.

### What Got Installed?

| Tool    | What It Does                                                   |
|---------|----------------------------------------------------------------|
| `node`  | The runtime that executes JavaScript files.                    |
| `npm`   | Node Package Manager — installs libraries (covered in Week 23).|
| `npx`   | Runs packages without installing them globally.                |

---

## 5. Running JavaScript Files with Node

### Using the Node REPL

The **REPL** (Read-Eval-Print Loop) is an interactive shell. Type `node` in your terminal and press Enter:

```bash
$ node
> 2 + 2
4
> "Hello".toUpperCase()
'HELLO'
> const greet = (name) => `Hello, ${name}!`
> greet("Node.js")
'Hello, Node.js!'
> .exit
```

The REPL is useful for quick experiments, but real programs go in files.

### Running a JavaScript File

Create a file called `app.js`:

```javascript
// app.js
const courseName = "Web Development Full Course";
const currentWeek = 22;

console.log(`Welcome to ${courseName}`);
console.log(`This is Week ${currentWeek}: Introduction to Node.js`);
console.log(`Node.js version: ${process.version}`);
console.log(`Operating system: ${process.platform}`);
console.log(`Current directory: ${process.cwd()}`);
```

Run it in the terminal:

```bash
node app.js
```

Output:

```
Welcome to Web Development Full Course
This is Week 22: Introduction to Node.js
Node.js version: v20.11.0
Operating system: win32
Current directory: C:\Users\student\projects
```

### The `process` Object

The `process` object is a global object in Node.js that provides information about the current running process.

```javascript
// process-demo.js

// Command line arguments
// Run: node process-demo.js hello world
console.log(process.argv);
// Output: ['path/to/node', 'path/to/process-demo.js', 'hello', 'world']

// Environment variables
console.log(process.env.PATH);   // System PATH variable

// Exit the process
// process.exit(0);  // 0 = success, 1 = error
```

---

## 6. Core Modules

Node.js comes with several **built-in modules** that you can use without installing anything. You simply `require()` them (or `import` them with ES Modules).

### 6.1 The `fs` (File System) Module

The `fs` module lets you read, write, update, and delete files on your computer.

#### Reading a File

```javascript
// read-file.js
const fs = require("fs");

// --- Synchronous (blocks execution until done) ---
const data = fs.readFileSync("message.txt", "utf-8");
console.log("Sync:", data);

// --- Asynchronous (non-blocking, uses callback) ---
fs.readFile("message.txt", "utf-8", (error, data) => {
  if (error) {
    console.error("Error reading file:", error.message);
    return;
  }
  console.log("Async:", data);
});

console.log("This runs BEFORE the async read finishes!");
```

#### Writing a File

```javascript
// write-file.js
const fs = require("fs");

// Write new content (creates file if it does not exist, overwrites if it does)
fs.writeFileSync("notes.txt", "Node.js is amazing!\n");
console.log("File written successfully.");

// Append content (adds to end of file)
fs.appendFileSync("notes.txt", "This line was appended.\n");
console.log("Content appended.");

// Read back to verify
const content = fs.readFileSync("notes.txt", "utf-8");
console.log("File contents:\n", content);
```

#### Checking if a File Exists and Deleting

```javascript
// delete-file.js
const fs = require("fs");

const filename = "temp.txt";

// Create a temporary file
fs.writeFileSync(filename, "Temporary data");

// Check if file exists
if (fs.existsSync(filename)) {
  console.log(`${filename} exists. Deleting...`);
  fs.unlinkSync(filename);
  console.log(`${filename} deleted.`);
} else {
  console.log(`${filename} does not exist.`);
}
```

### 6.2 The `path` Module

The `path` module helps you work with file and directory paths in a cross-platform way (Windows uses `\`, macOS/Linux use `/`).

```javascript
// path-demo.js
const path = require("path");

// Join path segments safely
const filePath = path.join("users", "fahad", "documents", "notes.txt");
console.log("Joined path:", filePath);
// Windows: users\fahad\documents\notes.txt
// macOS:   users/fahad/documents/notes.txt

// Get parts of a path
console.log("Directory:", path.dirname(filePath));   // users/fahad/documents
console.log("Filename:", path.basename(filePath));    // notes.txt
console.log("Extension:", path.extname(filePath));    // .txt

// Get absolute path
console.log("Absolute:", path.resolve("app.js"));
// Output: C:\Users\fahad\projects\app.js

// Parse a path into an object
console.log(path.parse("/home/user/file.txt"));
// {
//   root: '/',
//   dir: '/home/user',
//   base: 'file.txt',
//   ext: '.txt',
//   name: 'file'
// }
```

### 6.3 The `os` Module

The `os` module provides information about the operating system.

```javascript
// os-demo.js
const os = require("os");

console.log("Platform:", os.platform());       // win32, darwin, linux
console.log("Architecture:", os.arch());       // x64, arm64
console.log("CPU Cores:", os.cpus().length);   // 8
console.log("Total Memory:", (os.totalmem() / 1024 / 1024 / 1024).toFixed(2), "GB");
console.log("Free Memory:", (os.freemem() / 1024 / 1024 / 1024).toFixed(2), "GB");
console.log("Home Directory:", os.homedir());  // C:\Users\fahad
console.log("Hostname:", os.hostname());       // MY-COMPUTER
console.log("Uptime:", (os.uptime() / 3600).toFixed(2), "hours");
```

### Core Modules Summary

```
  +------------------------------------------------------------------+
  |                    Node.js Core Modules                          |
  +------------------------------------------------------------------+
  |  fs       | Read, write, delete files and directories            |
  |  path     | Handle file paths across operating systems           |
  |  os       | Get operating system information                     |
  |  http     | Create web servers and make HTTP requests             |
  |  events   | Create and handle custom events                      |
  |  crypto   | Encrypt data, hash passwords                         |
  |  url      | Parse and format URLs                                |
  |  util     | Utility functions (promisify, format, etc.)          |
  |  stream   | Handle streaming data (reading large files)           |
  +------------------------------------------------------------------+
```

---

## 7. CommonJS vs ES Modules

Node.js supports two module systems. Understanding both is important because you will encounter both in real-world projects.

### CommonJS (CJS) — The Original Node.js Way

```javascript
// --- math.js (Exporting) ---
const add = (a, b) => a + b;
const subtract = (a, b) => a - b;

module.exports = { add, subtract };

// --- app.js (Importing) ---
const { add, subtract } = require("./math");

console.log(add(5, 3));       // 8
console.log(subtract(10, 4)); // 6
```

### ES Modules (ESM) — The Modern Standard

To use ES Modules in Node.js, you must either:
- Add `"type": "module"` to your `package.json`, **or**
- Use the `.mjs` file extension.

```javascript
// --- math.mjs (Exporting) ---
export const add = (a, b) => a + b;
export const subtract = (a, b) => a - b;

// Default export
const calculator = { add, subtract };
export default calculator;

// --- app.mjs (Importing) ---
import { add, subtract } from "./math.mjs";
import calculator from "./math.mjs";

console.log(add(5, 3));                 // 8
console.log(calculator.subtract(10, 4)); // 6
```

### Comparison Table

| Feature              | CommonJS (`require`)          | ES Modules (`import`)          |
|----------------------|-------------------------------|--------------------------------|
| **Syntax**           | `require()` / `module.exports`| `import` / `export`            |
| **Loading**          | Synchronous                   | Asynchronous                   |
| **File extension**   | `.js` (default)               | `.mjs` or `"type": "module"`   |
| **Top-level await**  | Not supported                 | Supported                      |
| **Browser support**  | No (needs bundler)            | Yes (native)                   |
| **Node.js support**  | Since the beginning           | Since Node 12+ (stable in 14+) |
| **Usage trend**      | Legacy / existing projects    | Recommended for new projects   |

```
  CommonJS                          ES Modules
  +---------------------------+    +---------------------------+
  |  const x = require("x")  |    |  import x from "x"       |
  |  module.exports = { ... } |    |  export { ... }           |
  |                           |    |  export default ...       |
  |  Synchronous loading      |    |  Asynchronous loading     |
  |  Dynamic (can require     |    |  Static (analyzed at      |
  |   inside if blocks)       |    |   compile time)           |
  +---------------------------+    +---------------------------+
```

---

## 8. Creating an HTTP Server

One of the most powerful features of Node.js is the ability to create a web server with just a few lines of code.

### Your First Server

```javascript
// server.js
const http = require("http");

const server = http.createServer((request, response) => {
  // Set the response header
  response.writeHead(200, { "Content-Type": "text/plain" });

  // Send the response body
  response.end("Hello, World! This is my first Node.js server.");
});

const PORT = 3000;

server.listen(PORT, () => {
  console.log(`Server is running at http://localhost:${PORT}`);
});
```

Run it:

```bash
node server.js
# Output: Server is running at http://localhost:3000
```

Open your browser and visit `http://localhost:3000`. You will see "Hello, World! This is my first Node.js server."

### Handling Different Routes

```javascript
// server-routes.js
const http = require("http");

const server = http.createServer((req, res) => {
  // Set JSON content type for all responses
  res.setHeader("Content-Type", "application/json");

  if (req.url === "/" && req.method === "GET") {
    res.writeHead(200);
    res.end(JSON.stringify({ message: "Welcome to the Home Page" }));

  } else if (req.url === "/about" && req.method === "GET") {
    res.writeHead(200);
    res.end(JSON.stringify({ message: "About Us", version: "1.0.0" }));

  } else if (req.url === "/products" && req.method === "GET") {
    res.writeHead(200);
    res.end(JSON.stringify({
      products: [
        { id: 1, name: "Laptop", price: 999 },
        { id: 2, name: "Phone", price: 699 },
        { id: 3, name: "Tablet", price: 499 }
      ]
    }));

  } else {
    res.writeHead(404);
    res.end(JSON.stringify({ error: "Page not found" }));
  }
});

server.listen(3000, () => {
  console.log("Server running at http://localhost:3000");
});
```

### How the HTTP Request-Response Cycle Works

```
  +--------+                                           +--------+
  |        |  1. GET /products HTTP/1.1                |        |
  |        | ----------------------------------------> |        |
  | CLIENT |                                           | SERVER |
  |(Browser|  2. HTTP/1.1 200 OK                       |(Node.js|
  |   or   |     Content-Type: application/json        |   )    |
  |  React |     {"products": [...]}                   |        |
  |  App)  | <---------------------------------------- |        |
  |        |                                           |        |
  +--------+                                           +--------+

  Step 1: Client sends an HTTP REQUEST (method + URL + headers + body)
  Step 2: Server processes the request (reads data, runs logic)
  Step 3: Server sends an HTTP RESPONSE (status code + headers + body)
  Step 4: Client receives and renders the response
```

> Notice how painful it is to handle routes with raw `if/else` blocks. This is exactly why **Express.js** was created — it makes routing clean and simple. You will learn Express in Week 24.

---

## 9. The Event Loop

The Event Loop is the secret behind Node.js's ability to handle thousands of connections with a single thread.

### The Problem with Traditional Servers

Traditional servers (like Apache) create a **new thread** for every incoming request. If 10,000 users connect, the server needs 10,000 threads. Each thread uses memory, and eventually the server runs out of resources.

### Node.js's Solution: Single-Threaded Non-Blocking

Node.js uses **one thread** but never waits (blocks) for slow operations like reading files or querying databases. Instead, it delegates those tasks and moves on to the next request. When the slow task finishes, a callback is triggered.

```
  THE NODE.js EVENT LOOP
  ======================

  +--------------------------------------------------+
  |                    CALL STACK                     |
  |  (Executes code one function at a time)          |
  |  +--------------------------------------------+  |
  |  | console.log("Start")                       |  |
  |  | fs.readFile("data.txt", callback)           |  |
  |  | console.log("End")                         |  |
  +--+-----------+--------------------------------+--+
                  |
                  | Async tasks are sent to...
                  v
  +--------------------------------------------------+
  |              NODE.js APIs (libuv)                |
  |  (Handles file I/O, network, timers, etc.)       |
  |  +--------------------------------------------+  |
  |  | Timer: setTimeout(cb, 1000)                |  |
  |  | I/O:   fs.readFile("data.txt", cb)          |  |
  |  | Network: http.get("url", cb)               |  |
  +--+-----------+--------------------------------+--+
                  |
                  | When task completes, callback goes to...
                  v
  +--------------------------------------------------+
  |              CALLBACK QUEUE                      |
  |  (Waiting callbacks, processed in order)         |
  |  +--------------------------------------------+  |
  |  | [callback1] [callback2] [callback3]        |  |
  +--+-----------+--------------------------------+--+
                  |
                  | Event Loop checks: "Is call stack empty?"
                  | If yes, move callback from queue to stack.
                  v
  +--------------------------------------------------+
  |              EVENT LOOP                          |
  |  (Continuously checks stack and queue)           |
  |                                                  |
  |    Stack empty? --YES--> Move callback to stack  |
  |                  --NO--> Wait and check again    |
  +--------------------------------------------------+
```

### Example: Seeing the Event Loop in Action

```javascript
// event-loop-demo.js
console.log("1. Start");

setTimeout(() => {
  console.log("2. Timeout callback (after 0ms)");
}, 0);

Promise.resolve().then(() => {
  console.log("3. Promise resolved");
});

console.log("4. End");
```

Output:

```
1. Start
4. End
3. Promise resolved
2. Timeout callback (after 0ms)
```

**Why this order?**

1. `console.log("1. Start")` runs immediately (call stack).
2. `setTimeout` sends the callback to the timer queue (even with 0ms delay).
3. `Promise.then` sends the callback to the **microtask queue** (higher priority than timer queue).
4. `console.log("4. End")` runs immediately (call stack).
5. Call stack is empty. Microtask queue runs first: Promise callback logs "3."
6. Timer queue runs next: setTimeout callback logs "2."

### Blocking vs Non-Blocking

```javascript
// blocking.js
const fs = require("fs");

console.log("Before reading");
const data = fs.readFileSync("large-file.txt", "utf-8"); // BLOCKS here
console.log("After reading");   // Waits until file is fully read
console.log("Server can handle other requests now");

// non-blocking.js
const fs2 = require("fs");

console.log("Before reading");
fs2.readFile("large-file.txt", "utf-8", (err, data) => {
  console.log("File read complete"); // Runs later when file is ready
});
console.log("After reading");   // Runs IMMEDIATELY, does not wait
console.log("Server can handle other requests now");
```

```
  BLOCKING                          NON-BLOCKING
  +-----------+                     +-----------+
  | Task 1    |                     | Task 1    |
  | ......... | (waiting)           | Task 2    | (runs immediately)
  | Task 2    |                     | Task 3    | (runs immediately)
  | Task 3    |                     | ......... | (Task 1 completes later)
  +-----------+                     +-----------+
  Total: 9 seconds                  Total: 3 seconds
```

---

## 10. Summary

| Concept                | Key Takeaway                                                     |
|------------------------|------------------------------------------------------------------|
| **Backend**            | The server-side logic that processes requests and manages data.  |
| **Node.js**            | A JavaScript runtime built on V8 that runs JS outside browsers. |
| **V8 Engine**          | Google's engine that compiles JS to fast machine code.           |
| **Core Modules**       | Built-in modules like `fs`, `path`, `os`, `http`.                |
| **fs module**          | Read, write, append, and delete files.                           |
| **path module**        | Handle file paths safely across operating systems.               |
| **os module**          | Get system information (CPU, memory, platform).                  |
| **CommonJS**           | Original Node.js module system: `require` / `module.exports`.    |
| **ES Modules**         | Modern standard: `import` / `export`. Recommended for new code.  |
| **HTTP Server**        | Node.js can create web servers with the built-in `http` module.  |
| **Event Loop**         | Single-threaded mechanism that handles async operations.         |
| **Non-blocking I/O**   | Node.js delegates slow tasks and continues processing.           |

### What is Coming Next

In **Week 23**, you will learn about **npm** (Node Package Manager) — how to install and manage third-party packages, create your own modules, and set up a professional Node.js project structure.

---

> **Pro Tip:** Always use the **asynchronous** versions of `fs` methods in production servers. Synchronous methods block the entire event loop and prevent your server from handling other requests while waiting for a file operation to complete.
