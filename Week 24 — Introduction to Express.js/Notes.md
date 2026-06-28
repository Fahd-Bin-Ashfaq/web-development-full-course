# Week 24 — Introduction to Express.js

> **Prerequisites:** Week 22 (Node.js basics), Week 23 (npm & Modules)
> **Goal:** Learn Express.js fundamentals — routing, request/response handling, middleware basics, and building a modular API.

---

## Table of Contents

1. [What is Express.js?](#1-what-is-expressjs)
2. [Why Express.js vs Raw HTTP?](#2-why-expressjs-vs-raw-http)
3. [Installing and Setting Up Express](#3-installing-and-setting-up-express)
4. [Creating Your First Server](#4-creating-your-first-server)
5. [Routing](#5-routing)
6. [Route Parameters (`req.params`)](#6-route-parameters-reqparams)
7. [Query Parameters (`req.query`)](#7-query-parameters-reqquery)
8. [Request Body (`req.body`)](#8-request-body-reqbody)
9. [Response Methods](#9-response-methods)
10. [Serving Static Files](#10-serving-static-files)
11. [Modular Routing with `express.Router()`](#11-modular-routing-with-expressrouter)
12. [The Request-Response Cycle](#12-the-request-response-cycle)
13. [Summary](#13-summary)

---

## 1. What is Express.js?

**Express.js** is a fast, unopinionated, and minimalist **web framework** for Node.js. It sits on top of Node's built-in `http` module and provides a cleaner, more powerful way to build web servers and APIs.

> Think of Node.js's `http` module as **driving through a city without GPS**. You can technically reach your destination, but you have to figure out every turn, handle every intersection, and manage every traffic signal yourself. **Express.js is the GPS** — it provides clear routes, turn-by-turn instructions, and handles the complicated navigation logic so you can focus on reaching your destination.

### Key Facts

| Fact                   | Detail                                                        |
|------------------------|---------------------------------------------------------------|
| **Created**            | 2010 by TJ Holowaychuk                                       |
| **Current maintainer** | OpenJS Foundation                                             |
| **npm downloads**      | 25+ million per week                                          |
| **Philosophy**         | Minimal and flexible — add only what you need                  |
| **Use case**           | REST APIs, web applications, server-side rendering             |

### Where Express Fits in the Stack

```
  +-----------------------------------------------------------+
  |                    YOUR APPLICATION                        |
  |  (Routes, Controllers, Business Logic)                    |
  +-----------------------------------------------------------+
  |                      EXPRESS.JS                            |
  |  (Routing, Middleware, Request/Response Handling)           |
  +-----------------------------------------------------------+
  |                      NODE.js                               |
  |  (V8 Engine, libuv, Core Modules)                          |
  +-----------------------------------------------------------+
  |                   OPERATING SYSTEM                         |
  |  (Network, File System, Processes)                         |
  +-----------------------------------------------------------+
```

---

## 2. Why Express.js vs Raw HTTP?

In Week 22, you built an HTTP server using Node's `http` module. That approach works, but it becomes painful as your application grows. Express simplifies everything.

### Side-by-Side Comparison

**Raw HTTP (Week 22 approach):**

```javascript
const http = require("http");

const server = http.createServer((req, res) => {
  if (req.url === "/" && req.method === "GET") {
    res.writeHead(200, { "Content-Type": "application/json" });
    res.end(JSON.stringify({ message: "Home" }));
  } else if (req.url === "/about" && req.method === "GET") {
    res.writeHead(200, { "Content-Type": "application/json" });
    res.end(JSON.stringify({ message: "About" }));
  } else if (req.url === "/contact" && req.method === "POST") {
    let body = "";
    req.on("data", (chunk) => { body += chunk; });
    req.on("end", () => {
      const data = JSON.parse(body);
      res.writeHead(201, { "Content-Type": "application/json" });
      res.end(JSON.stringify({ received: data }));
    });
  } else {
    res.writeHead(404, { "Content-Type": "application/json" });
    res.end(JSON.stringify({ error: "Not found" }));
  }
});

server.listen(3000);
```

**Express (cleaner, more readable):**

```javascript
const express = require("express");
const app = express();

app.use(express.json());

app.get("/", (req, res) => {
  res.json({ message: "Home" });
});

app.get("/about", (req, res) => {
  res.json({ message: "About" });
});

app.post("/contact", (req, res) => {
  res.status(201).json({ received: req.body });
});

app.listen(3000);
```

### Comparison Table

| Feature                      | Raw `http` Module              | Express.js                      |
|------------------------------|--------------------------------|---------------------------------|
| **Route handling**           | Manual `if/else` chains        | Built-in `app.get()`, `app.post()` |
| **URL parameters**           | Manual string parsing          | `req.params` (automatic)        |
| **Query strings**            | Manual URL parsing             | `req.query` (automatic)         |
| **Request body parsing**     | Manual chunk collection        | `express.json()` middleware     |
| **Response helpers**         | `res.writeHead()` + `res.end()`| `res.json()`, `res.send()`      |
| **Static files**             | Manual file reading            | `express.static()` (one line)   |
| **Middleware support**       | None                           | Built-in middleware pipeline    |
| **Code readability**         | Complex, verbose               | Clean, declarative              |
| **Lines of code (typical)**  | 30+ for basic server           | 10 for equivalent server        |

---

## 3. Installing and Setting Up Express

### Step-by-Step Setup

```bash
# Create project directory
mkdir my-express-app
cd my-express-app

# Initialize npm
npm init -y

# Install Express
npm install express

# Install Nodemon for development
npm install -D nodemon
```

### Update `package.json` Scripts

```json
{
  "scripts": {
    "start": "node index.js",
    "dev": "nodemon index.js"
  }
}
```

### Project Structure

```
  my-express-app/
  +-- node_modules/
  +-- index.js              (main entry point)
  +-- package.json
  +-- package-lock.json
  +-- .gitignore
```

---

## 4. Creating Your First Server

```javascript
// index.js
const express = require("express");
const app = express();
const PORT = 3000;

// Define a route
app.get("/", (req, res) => {
  res.send("Hello, Express! Your first server is running.");
});

// Start the server
app.listen(PORT, () => {
  console.log(`Server is running at http://localhost:${PORT}`);
});
```

Run it:

```bash
npm run dev
```

Visit `http://localhost:3000` in your browser — you will see the message displayed.

### Breaking Down the Code

```
  const express = require("express");   // 1. Import Express
  const app = express();                // 2. Create an Express application
                                        //    (app is the central object)

  app.get("/", (req, res) => {          // 3. Define a route
    res.send("Hello!");                 //    - Method: GET
  });                                   //    - Path: /
                                        //    - Handler: function(req, res)

  app.listen(3000, () => {              // 4. Start listening on port 3000
    console.log("Running...");
  });
```

---

## 5. Routing

Routing determines **how your application responds** to a client request at a particular URL (path) with a specific HTTP method.

### HTTP Methods

| Method     | Purpose                              | Example                        |
|------------|--------------------------------------|--------------------------------|
| **GET**    | Retrieve data                        | Get a list of products         |
| **POST**   | Create new data                      | Add a new product              |
| **PUT**    | Update existing data (full replace)  | Update a product's details     |
| **PATCH**  | Update existing data (partial)       | Change a product's price only  |
| **DELETE** | Remove data                          | Delete a product               |

### Defining Routes

```javascript
const express = require("express");
const app = express();

app.use(express.json());

// Sample data
let products = [
  { id: 1, name: "Laptop", price: 999 },
  { id: 2, name: "Phone", price: 699 },
  { id: 3, name: "Tablet", price: 499 }
];

// GET — Retrieve all products
app.get("/api/products", (req, res) => {
  res.json(products);
});

// POST — Create a new product
app.post("/api/products", (req, res) => {
  const newProduct = {
    id: products.length + 1,
    name: req.body.name,
    price: req.body.price
  };
  products.push(newProduct);
  res.status(201).json(newProduct);
});

// PUT — Update a product (full replace)
app.put("/api/products/:id", (req, res) => {
  const id = parseInt(req.params.id);
  const index = products.findIndex((p) => p.id === id);

  if (index === -1) {
    return res.status(404).json({ error: "Product not found" });
  }

  products[index] = { id, name: req.body.name, price: req.body.price };
  res.json(products[index]);
});

// DELETE — Remove a product
app.delete("/api/products/:id", (req, res) => {
  const id = parseInt(req.params.id);
  const index = products.findIndex((p) => p.id === id);

  if (index === -1) {
    return res.status(404).json({ error: "Product not found" });
  }

  const deleted = products.splice(index, 1);
  res.json({ message: "Product deleted", product: deleted[0] });
});

app.listen(3000, () => console.log("Server running on port 3000"));
```

### Route Pattern Overview

```
  app.METHOD(PATH, HANDLER)

  app    --> The Express application instance
  METHOD --> HTTP method (get, post, put, patch, delete)
  PATH   --> URL path ("/api/products", "/users/:id")
  HANDLER --> Function that runs when route is matched: (req, res) => { }

  Examples:
  +------+---------------------+----------------------------+
  | GET  | /api/products       | Get all products           |
  | GET  | /api/products/:id   | Get one product by ID      |
  | POST | /api/products       | Create a new product       |
  | PUT  | /api/products/:id   | Update a product           |
  | DEL  | /api/products/:id   | Delete a product           |
  +------+---------------------+----------------------------+
```

---

## 6. Route Parameters (`req.params`)

Route parameters are **named segments** in the URL path, prefixed with a colon (`:`). They let you capture dynamic values from the URL.

### Example

```javascript
// Single parameter
app.get("/api/users/:id", (req, res) => {
  console.log(req.params);   // { id: "42" }
  const userId = req.params.id;
  res.json({ message: `Fetching user with ID: ${userId}` });
});

// Multiple parameters
app.get("/api/courses/:courseId/lessons/:lessonId", (req, res) => {
  console.log(req.params);
  // { courseId: "5", lessonId: "12" }
  res.json({
    course: req.params.courseId,
    lesson: req.params.lessonId
  });
});
```

### How It Works

```
  URL:   /api/users/42
  Route: /api/users/:id

  +----------+----------+----------+
  | /api     | /users   | /42      |
  | (static) | (static) | (dynamic)|
  +----------+----------+----------+
                           |
                           v
                    req.params.id = "42"

  URL:   /api/courses/5/lessons/12
  Route: /api/courses/:courseId/lessons/:lessonId

  +-----+----------+----+----------+-----+
  | /api| /courses | /5 | /lessons | /12 |
  +-----+----------+----+----------+-----+
                     |               |
                     v               v
           req.params.courseId  req.params.lessonId
                  = "5"             = "12"
```

> **Important:** Route parameters are always **strings**. If you need a number, convert it with `parseInt()` or `Number()`.

### Practical Example: Find a User by ID

```javascript
const users = [
  { id: 1, name: "Ali", email: "ali@example.com" },
  { id: 2, name: "Sara", email: "sara@example.com" },
  { id: 3, name: "Omar", email: "omar@example.com" }
];

app.get("/api/users/:id", (req, res) => {
  const id = parseInt(req.params.id);
  const user = users.find((u) => u.id === id);

  if (!user) {
    return res.status(404).json({ error: "User not found" });
  }

  res.json(user);
});

// GET /api/users/2
// Response: { "id": 2, "name": "Sara", "email": "sara@example.com" }

// GET /api/users/99
// Response: { "error": "User not found" } (status 404)
```

---

## 7. Query Parameters (`req.query`)

Query parameters are key-value pairs that appear **after the `?`** in a URL. They are typically used for filtering, sorting, searching, and pagination.

### Example

```javascript
// URL: /api/products?category=electronics&sort=price&order=asc

app.get("/api/products", (req, res) => {
  console.log(req.query);
  // {
  //   category: "electronics",
  //   sort: "price",
  //   order: "asc"
  // }

  const { category, sort, order } = req.query;
  res.json({
    message: `Showing ${category} products, sorted by ${sort} (${order})`
  });
});
```

### How Query Parameters Work

```
  URL: /api/products?category=electronics&sort=price&limit=10
                     |                                       |
                     +-- Everything after ? is the query ----+

  Parsed by Express automatically:
  req.query = {
    category: "electronics",
    sort: "price",
    limit: "10"         <-- Always strings!
  }
```

### Practical Example: Search and Pagination

```javascript
const products = [
  { id: 1, name: "Laptop", category: "electronics", price: 999 },
  { id: 2, name: "T-Shirt", category: "clothing", price: 29 },
  { id: 3, name: "Phone", category: "electronics", price: 699 },
  { id: 4, name: "Jeans", category: "clothing", price: 59 },
  { id: 5, name: "Headphones", category: "electronics", price: 149 }
];

app.get("/api/products", (req, res) => {
  let results = [...products];

  // Filter by category
  if (req.query.category) {
    results = results.filter((p) => p.category === req.query.category);
  }

  // Search by name
  if (req.query.search) {
    const search = req.query.search.toLowerCase();
    results = results.filter((p) => p.name.toLowerCase().includes(search));
  }

  // Pagination
  const page = parseInt(req.query.page) || 1;
  const limit = parseInt(req.query.limit) || 10;
  const start = (page - 1) * limit;
  const end = start + limit;
  const paginated = results.slice(start, end);

  res.json({
    total: results.length,
    page,
    limit,
    data: paginated
  });
});

// GET /api/products?category=electronics
// GET /api/products?search=lap
// GET /api/products?page=1&limit=2
```

### Route Params vs Query Params

| Feature           | Route Params (`req.params`) | Query Params (`req.query`)      |
|-------------------|-----------------------------|---------------------------------|
| **Location**      | In the URL path             | After the `?` in the URL        |
| **Syntax**        | `/users/:id`                | `/users?role=admin`             |
| **Purpose**       | Identify a specific resource| Filter, sort, search, paginate  |
| **Required?**     | Yes (route won't match)     | No (optional by default)        |
| **Example**       | `/api/users/42`             | `/api/users?age=25&city=NYC`    |

---

## 8. Request Body (`req.body`)

The request body contains data sent by the client, typically with **POST** and **PUT** requests. To access `req.body`, you must use a **parser middleware**.

### Setting Up Body Parsing

```javascript
const express = require("express");
const app = express();

// Parse JSON bodies (Content-Type: application/json)
app.use(express.json());

// Parse URL-encoded bodies (Content-Type: application/x-www-form-urlencoded)
app.use(express.urlencoded({ extended: true }));
```

### Receiving Data from the Client

```javascript
app.post("/api/users", (req, res) => {
  console.log("Received body:", req.body);
  // { name: "Ali", email: "ali@example.com", age: 25 }

  const { name, email, age } = req.body;

  // Validate the data
  if (!name || !email) {
    return res.status(400).json({
      error: "Name and email are required"
    });
  }

  // Create the user (in a real app, you would save to a database)
  const newUser = {
    id: Date.now(),
    name,
    email,
    age: age || null
  };

  res.status(201).json({
    message: "User created successfully",
    user: newUser
  });
});
```

### How the Body Flows

```
  CLIENT (React, Postman, curl)
  +-----------------------------------+
  |  POST /api/users                  |
  |  Content-Type: application/json   |
  |                                   |
  |  Body: {                          |
  |    "name": "Ali",                 |
  |    "email": "ali@example.com"     |
  |  }                                |
  +----------------+------------------+
                   |
                   v
  EXPRESS MIDDLEWARE: express.json()
  +-----------------------------------+
  |  Parses the raw JSON string       |
  |  into a JavaScript object         |
  |  and attaches it to req.body      |
  +----------------+------------------+
                   |
                   v
  ROUTE HANDLER
  +-----------------------------------+
  |  req.body = {                     |
  |    name: "Ali",                   |
  |    email: "ali@example.com"       |
  |  }                                |
  |                                   |
  |  You can now use req.body.name,   |
  |  req.body.email, etc.             |
  +-----------------------------------+
```

> **Without `express.json()` middleware, `req.body` will be `undefined`.** This is the most common mistake beginners make.

---

## 9. Response Methods

Express provides several methods on the `res` object to send responses back to the client.

### Common Response Methods

```javascript
// res.send() — Send a string, object, or Buffer
app.get("/text", (req, res) => {
  res.send("Hello, World!");
});

// res.json() — Send a JSON response (sets Content-Type automatically)
app.get("/data", (req, res) => {
  res.json({ name: "Ali", age: 25 });
});

// res.status() — Set the HTTP status code (chainable)
app.get("/not-found", (req, res) => {
  res.status(404).json({ error: "Resource not found" });
});

// res.redirect() — Redirect to another URL
app.get("/old-page", (req, res) => {
  res.redirect("/new-page");
});

// res.sendFile() — Send a file as the response
const path = require("path");
app.get("/download", (req, res) => {
  res.sendFile(path.join(__dirname, "files", "report.pdf"));
});
```

### HTTP Status Codes You Should Know

| Code | Name                    | Meaning                                    |
|------|-------------------------|--------------------------------------------|
| 200  | OK                      | Request succeeded.                         |
| 201  | Created                 | Resource was created successfully.         |
| 204  | No Content              | Success, but no data to return.            |
| 400  | Bad Request             | Client sent invalid data.                  |
| 401  | Unauthorized            | Authentication required.                   |
| 403  | Forbidden               | Authenticated but not allowed.             |
| 404  | Not Found               | Resource does not exist.                   |
| 409  | Conflict                | Duplicate resource (e.g., email exists).   |
| 500  | Internal Server Error   | Server crashed or encountered an error.    |

### Status Code Categories

```
  +------+--------------------+--------------------------------+
  | 1xx  | Informational      | Request received, continuing   |
  | 2xx  | Success            | Request accepted and processed |
  | 3xx  | Redirection        | Further action needed          |
  | 4xx  | Client Error       | Bad request from the client    |
  | 5xx  | Server Error       | Server failed to process       |
  +------+--------------------+--------------------------------+
```

---

## 10. Serving Static Files

Static files are files that the server delivers **as-is** without processing — HTML, CSS, JavaScript (frontend), images, fonts, and documents.

### Setting Up Static File Serving

```javascript
const express = require("express");
const path = require("path");
const app = express();

// Serve all files inside the "public" folder
app.use(express.static(path.join(__dirname, "public")));

app.listen(3000, () => {
  console.log("Server running on port 3000");
});
```

### Project Structure

```
  my-express-app/
  +-- index.js
  +-- public/                  <-- Static files go here
  |   +-- index.html
  |   +-- css/
  |   |   +-- style.css
  |   +-- js/
  |   |   +-- script.js
  |   +-- images/
  |       +-- logo.png
  +-- package.json
```

### How URLs Map to Files

```
  Request URL                  File Served
  -------------------------------------------------------
  http://localhost:3000/                  public/index.html
  http://localhost:3000/css/style.css     public/css/style.css
  http://localhost:3000/js/script.js      public/js/script.js
  http://localhost:3000/images/logo.png   public/images/logo.png
```

### Example: `public/index.html`

```html
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>My Express App</title>
  <link rel="stylesheet" href="/css/style.css">
</head>
<body>
  <h1>Welcome to My Express App</h1>
  <p>This HTML file is served as a static file by Express.</p>
  <img src="/images/logo.png" alt="Logo">
  <script src="/js/script.js"></script>
</body>
</html>
```

> **Note:** When building a full-stack app (React frontend + Express backend), you typically serve your React build files as static files using `express.static()`.

---

## 11. Modular Routing with `express.Router()`

As your application grows, putting all routes in a single file becomes unmanageable. Express provides the `Router` object to organize routes into separate modules.

### Without Modular Routing (Everything in One File)

```javascript
// index.js — This gets messy fast
app.get("/api/users", ...);
app.get("/api/users/:id", ...);
app.post("/api/users", ...);
app.put("/api/users/:id", ...);
app.delete("/api/users/:id", ...);

app.get("/api/products", ...);
app.get("/api/products/:id", ...);
app.post("/api/products", ...);
app.put("/api/products/:id", ...);
app.delete("/api/products/:id", ...);

app.get("/api/orders", ...);
// ... 50 more routes
```

### With Modular Routing (Organized)

**Project structure:**

```
  my-express-app/
  +-- index.js                (main entry point)
  +-- routes/
  |   +-- userRoutes.js       (all /api/users routes)
  |   +-- productRoutes.js    (all /api/products routes)
  +-- package.json
```

**`routes/userRoutes.js`:**

```javascript
// routes/userRoutes.js
const express = require("express");
const router = express.Router();

// Sample data
let users = [
  { id: 1, name: "Ali", email: "ali@example.com" },
  { id: 2, name: "Sara", email: "sara@example.com" }
];

// GET /api/users
router.get("/", (req, res) => {
  res.json(users);
});

// GET /api/users/:id
router.get("/:id", (req, res) => {
  const user = users.find((u) => u.id === parseInt(req.params.id));
  if (!user) return res.status(404).json({ error: "User not found" });
  res.json(user);
});

// POST /api/users
router.post("/", (req, res) => {
  const newUser = {
    id: users.length + 1,
    name: req.body.name,
    email: req.body.email
  };
  users.push(newUser);
  res.status(201).json(newUser);
});

// DELETE /api/users/:id
router.delete("/:id", (req, res) => {
  const index = users.findIndex((u) => u.id === parseInt(req.params.id));
  if (index === -1) return res.status(404).json({ error: "User not found" });
  const deleted = users.splice(index, 1);
  res.json({ message: "User deleted", user: deleted[0] });
});

module.exports = router;
```

**`routes/productRoutes.js`:**

```javascript
// routes/productRoutes.js
const express = require("express");
const router = express.Router();

let products = [
  { id: 1, name: "Laptop", price: 999, category: "electronics" },
  { id: 2, name: "T-Shirt", price: 29, category: "clothing" }
];

// GET /api/products
router.get("/", (req, res) => {
  let results = [...products];

  // Optional filtering by category
  if (req.query.category) {
    results = results.filter((p) => p.category === req.query.category);
  }

  res.json(results);
});

// GET /api/products/:id
router.get("/:id", (req, res) => {
  const product = products.find((p) => p.id === parseInt(req.params.id));
  if (!product) return res.status(404).json({ error: "Product not found" });
  res.json(product);
});

// POST /api/products
router.post("/", (req, res) => {
  const newProduct = {
    id: products.length + 1,
    name: req.body.name,
    price: req.body.price,
    category: req.body.category
  };
  products.push(newProduct);
  res.status(201).json(newProduct);
});

module.exports = router;
```

**`index.js`** — Main file that connects everything:

```javascript
// index.js
const express = require("express");
const app = express();

// Middleware
app.use(express.json());

// Import route modules
const userRoutes = require("./routes/userRoutes");
const productRoutes = require("./routes/productRoutes");

// Mount routes with prefixes
app.use("/api/users", userRoutes);
app.use("/api/products", productRoutes);

// Home route
app.get("/", (req, res) => {
  res.json({
    message: "Welcome to the API",
    endpoints: ["/api/users", "/api/products"]
  });
});

// 404 handler for undefined routes
app.use((req, res) => {
  res.status(404).json({ error: "Route not found" });
});

const PORT = process.env.PORT || 3000;
app.listen(PORT, () => {
  console.log(`Server running on port ${PORT}`);
});
```

### How `app.use()` Mounts Routers

```
  app.use("/api/users", userRoutes);

  This means:
  +--------------------+-------------------+
  | PREFIX             | ROUTER PATH       |    FULL URL
  +--------------------+-------------------+
  | /api/users         | /                 | -> /api/users
  | /api/users         | /:id              | -> /api/users/:id
  | /api/users         | / (POST)          | -> POST /api/users
  +--------------------+-------------------+

  The router only defines relative paths ("/", "/:id").
  The prefix is added by app.use().
```

---

## 12. The Request-Response Cycle

Every interaction between a client and your Express server follows a predictable cycle.

```
  THE EXPRESS REQUEST-RESPONSE CYCLE
  ==================================

  CLIENT                          EXPRESS SERVER
  +--------+                     +----------------------------------+
  |        |   1. HTTP Request   |                                  |
  |        | ------------------> |  2. Middleware Pipeline           |
  |        |    (method, URL,    |  +----------------------------+  |
  |        |     headers, body)  |  | express.json()             |  |
  |        |                     |  | (parse body)               |  |
  |        |                     |  +----------------------------+  |
  |        |                     |              |                   |
  |        |                     |              v                   |
  |        |                     |  +----------------------------+  |
  |        |                     |  | express.static()           |  |
  |        |                     |  | (serve static files)       |  |
  |        |                     |  +----------------------------+  |
  |        |                     |              |                   |
  |        |                     |              v                   |
  |        |                     |  3. Route Matching               |
  |        |                     |  +----------------------------+  |
  |        |                     |  | GET /api/users  --> handler |  |
  |        |                     |  | POST /api/users --> handler |  |
  |        |                     |  | ...                        |  |
  |        |                     |  +----------------------------+  |
  |        |                     |              |                   |
  |        |                     |              v                   |
  |        |                     |  4. Route Handler Executes       |
  |        |                     |  +----------------------------+  |
  |        |   5. HTTP Response  |  | Process data               |  |
  |        | <------------------ |  | Send response              |  |
  |        |    (status, headers,|  | res.json({ ... })          |  |
  |        |     body)           |  +----------------------------+  |
  +--------+                     +----------------------------------+
```

### Step-by-Step

1. **Client sends a request** — The browser, React app, or API tool (like Postman) sends an HTTP request with a method (GET, POST, etc.), URL, headers, and optionally a body.

2. **Middleware processes the request** — Express runs the request through any middleware functions registered with `app.use()`. Middleware can parse the body, check authentication, log the request, and more.

3. **Route matching** — Express checks each defined route to find one that matches both the HTTP method and URL path. The first match wins.

4. **Handler executes** — The matched route's handler function runs, processing the request (reading data, querying a database, applying business logic).

5. **Response sent** — The handler sends a response back to the client using methods like `res.json()`, `res.send()`, or `res.redirect()`.

---

## 13. Summary

| Concept                 | Key Takeaway                                                     |
|-------------------------|------------------------------------------------------------------|
| **Express.js**          | A minimal web framework for Node.js that simplifies server dev.  |
| **Why Express**         | Cleaner routing, built-in parsing, middleware, less boilerplate.  |
| **`app.get/post/put/delete`** | Define routes for different HTTP methods.                   |
| **`req.params`**        | Capture dynamic values from the URL path (`:id`).                |
| **`req.query`**         | Access key-value pairs after `?` in the URL.                     |
| **`req.body`**          | Access data sent in the request body (needs `express.json()`).   |
| **`res.json()`**        | Send a JSON response (most common for APIs).                     |
| **`res.status()`**      | Set the HTTP status code (chainable with `.json()`).             |
| **`res.redirect()`**    | Redirect the client to a different URL.                          |
| **`express.static()`**  | Serve static files (HTML, CSS, images) from a directory.         |
| **`express.Router()`**  | Organize routes into modular, separate files.                    |
| **Request-Response**    | Client sends request, middleware processes it, handler responds.  |

### What is Coming Next

In **Week 25**, you will learn about **Middleware** in depth and build complete **REST APIs** — the standard architecture for modern web applications.

---

> **Pro Tip:** Use a tool like **Postman** or the **Thunder Client** extension in VS Code to test your API endpoints. You cannot easily send POST, PUT, or DELETE requests from a browser's address bar — those tools let you set methods, headers, and body data for each request.
