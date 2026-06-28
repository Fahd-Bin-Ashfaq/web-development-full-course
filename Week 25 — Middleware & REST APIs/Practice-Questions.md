# Week 25: Middleware & REST APIs - Practice Questions

**Total Questions: 20**

| Section | Topic                    | Questions |
|---------|--------------------------|-----------|
| A       | Multiple Choice Questions| 10        |
| B       | Short Answer Questions   | 5         |
| C       | Coding Exercises         | 5         |

---

## Section A: Multiple Choice Questions (10)

**Q1.** What is the correct signature for a middleware function in Express?

- A) `function(req, res)`
- B) `function(req, res, next)`
- C) `function(next, req, res)`
- D) `function(res, req, next)`

<details>
<summary>Answer</summary>

**B) `function(req, res, next)`**

A middleware function in Express receives three arguments in this specific order: the request object (`req`), the response object (`res`), and the `next` function. Calling `next()` passes control to the next middleware in the pipeline.
</details>

---

**Q2.** What happens if you forget to call `next()` inside a middleware function?

- A) Express automatically moves to the next middleware
- B) The server crashes with an error
- C) The request gets stuck and the client eventually times out
- D) The response is sent automatically

<details>
<summary>Answer</summary>

**C) The request gets stuck and the client eventually times out**

If `next()` is not called and no response is sent, the request remains pending. Express does not automatically advance to the next middleware. The client will wait until the connection times out.
</details>

---

**Q3.** Which built-in middleware is required to parse JSON data from incoming request bodies?

- A) `express.static()`
- B) `express.urlencoded()`
- C) `express.json()`
- D) `express.bodyParser()`

<details>
<summary>Answer</summary>

**C) `express.json()`**

`express.json()` parses incoming request bodies that have a `Content-Type` of `application/json` and makes the parsed data available on `req.body`. Without it, `req.body` is `undefined` for JSON payloads.
</details>

---

**Q4.** How many parameters does an error handling middleware function have?

- A) 2 -- `(err, res)`
- B) 3 -- `(req, res, next)`
- C) 4 -- `(err, req, res, next)`
- D) 1 -- `(err)`

<details>
<summary>Answer</summary>

**C) 4 -- `(err, req, res, next)`**

Express identifies error handling middleware by the fact that it has exactly four parameters. The first parameter is the error object. All four parameters must be declared even if `next` is not used, otherwise Express will not recognize it as error handling middleware.
</details>

---

**Q5.** Which HTTP method should be used to create a new resource on the server?

- A) `GET`
- B) `PUT`
- C) `POST`
- D) `PATCH`

<details>
<summary>Answer</summary>

**C) `POST`**

In RESTful API design, `POST` is the method used to create new resources. `GET` is for reading, `PUT` is for full updates, `PATCH` is for partial updates, and `DELETE` is for removing resources.
</details>

---

**Q6.** What is the correct HTTP status code to return when a new resource has been successfully created?

- A) `200 OK`
- B) `201 Created`
- C) `204 No Content`
- D) `202 Accepted`

<details>
<summary>Answer</summary>

**B) `201 Created`**

Status code `201` specifically indicates that a new resource has been successfully created on the server. This is the standard response for a successful `POST` request that creates something. `200` is for general success, and `204` is for success with no response body.
</details>

---

**Q7.** Which third-party middleware is used to allow requests from different origins (domains)?

- A) `helmet`
- B) `morgan`
- C) `cors`
- D) `express.static()`

<details>
<summary>Answer</summary>

**C) `cors`**

The `cors` (Cross-Origin Resource Sharing) middleware configures HTTP headers to allow or restrict requests from different origins. Without it, browsers block requests from a frontend running on a different domain or port than the API server.
</details>

---

**Q8.** Which of the following is a correctly designed RESTful URL?

- A) `GET /getAllProducts`
- B) `GET /api/products`
- C) `GET /fetchProducts`
- D) `GET /api/getProductList`

<details>
<summary>Answer</summary>

**B) `GET /api/products`**

RESTful URLs use plural nouns (not verbs) to represent resources. The HTTP method (`GET`) already describes the action being performed. URLs like `/getAllProducts` or `/fetchProducts` violate REST conventions by embedding verbs in the URL.
</details>

---

**Q9.** What is the difference between HTTP status codes `401` and `403`?

- A) `401` means the server is down; `403` means the resource does not exist
- B) `401` means not authenticated; `403` means authenticated but not authorized
- C) `401` means bad request; `403` means server error
- D) There is no difference; they are interchangeable

<details>
<summary>Answer</summary>

**B) `401` means not authenticated; `403` means authenticated but not authorized**

`401 Unauthorized` means the client has not provided valid authentication credentials (no token, expired token). `403 Forbidden` means the client is authenticated (identity is known) but does not have permission to access the requested resource (for example, a regular user trying to access an admin-only endpoint).
</details>

---

**Q10.** Which REST principle states that each request must contain all the information the server needs to process it?

- A) Client-Server
- B) Layered System
- C) Stateless
- D) Uniform Interface

<details>
<summary>Answer</summary>

**C) Stateless**

The stateless principle means the server does not store any session information about the client between requests. Every request must carry all the data the server needs, including authentication tokens. The server treats each request as completely independent.
</details>

---

## Section B: Short Answer Questions (5)

**Q11.** Explain the difference between application-level middleware and route-level middleware. When would you use each?

<details>
<summary>Answer</summary>

**Application-level middleware** is registered with `app.use()` and runs on every incoming request, regardless of the route. Examples include `express.json()`, logging middleware, and CORS. You use it when every request needs to be processed in the same way.

**Route-level middleware** is passed as an argument to a specific route handler and runs only when that route is matched. For example, `app.get("/dashboard", authCheck, handler)` applies `authCheck` only to the `/dashboard` route. You use it when only certain routes need specific processing, such as authentication on protected endpoints.

```javascript
// Application-level: runs on ALL requests
app.use(express.json());

// Route-level: runs only on GET /dashboard
app.get("/dashboard", authCheck, (req, res) => {
    res.send("Dashboard");
});
```
</details>

---

**Q12.** Why must error handling middleware be registered after all route definitions in Express?

<details>
<summary>Answer</summary>

Error handling middleware must be registered last because Express processes middleware in the order it is registered. When a route handler or any middleware calls `next(error)` with an error object, Express skips all remaining regular middleware and jumps to the next error handling middleware (the one with four parameters).

If the error handler is registered before the routes, errors thrown in those routes will have no error handler to catch them. By placing it at the end of the middleware stack, it acts as a safety net that catches errors from all routes and middleware above it.

```javascript
// Routes first
app.get("/api/users", usersHandler);
app.get("/api/products", productsHandler);

// Error handler last -- catches errors from ALL routes above
app.use((err, req, res, next) => {
    res.status(err.status || 500).json({ error: err.message });
});
```
</details>

---

**Q13.** What is the purpose of the `helmet` middleware, and what types of attacks does it help prevent?

<details>
<summary>Answer</summary>

Helmet is a third-party middleware that sets various HTTP security headers on every response. It helps protect Express applications from common web vulnerabilities by configuring headers such as:

- **X-XSS-Protection:** Helps prevent cross-site scripting (XSS) attacks where attackers inject malicious scripts into web pages.
- **X-Frame-Options:** Prevents clickjacking by blocking the page from being embedded in an iframe on another site.
- **X-Content-Type-Options:** Stops browsers from MIME-type sniffing, which could allow attackers to disguise malicious files.
- **Strict-Transport-Security:** Forces browsers to use HTTPS instead of HTTP, preventing man-in-the-middle attacks.
- **Content-Security-Policy:** Controls which sources of scripts, styles, and other resources are allowed to load.

Helmet is used with a single line -- `app.use(helmet())` -- and it applies sensible security defaults.
</details>

---

**Q14.** Explain the difference between `PUT` and `PATCH` HTTP methods with a practical example.

<details>
<summary>Answer</summary>

**PUT** replaces an entire resource with the data provided. All fields must be included in the request body, and any missing fields may be set to `null` or their default values. It is a full replacement.

**PATCH** partially updates a resource. Only the fields that need to change are included in the request body. All other fields remain unchanged.

**Example:** Updating a product with ID 5 that has fields: `name`, `price`, `category`, and `stock`.

```javascript
// PUT /api/products/5 -- Must send ALL fields
{
    "name": "Gaming Laptop",
    "price": 1500,
    "category": "Electronics",
    "stock": 25
}
// If you omit "stock", it might be set to null

// PATCH /api/products/5 -- Send only what changed
{
    "price": 1500
}
// Only price is updated; name, category, and stock remain the same
```

Use `PUT` when the client has the complete updated version of the resource. Use `PATCH` when the client only wants to modify one or two fields.
</details>

---

**Q15.** What does CORS stand for, and why is it necessary when building a full-stack application?

<details>
<summary>Answer</summary>

CORS stands for **Cross-Origin Resource Sharing**. It is a browser security mechanism that controls which web pages can make requests to a server from a different origin.

An **origin** is defined by the combination of protocol, domain, and port. For example, `http://localhost:3000` and `http://localhost:5000` are different origins because they use different ports.

In a full-stack application, the frontend (React app on port 3000) and backend (Express API on port 5000) run on different origins. When the React app tries to fetch data from the API, the browser blocks the request by default because it comes from a different origin.

The `cors` middleware on the Express server adds the `Access-Control-Allow-Origin` header to responses, telling the browser that requests from the frontend origin are permitted.

```javascript
// Without cors: Browser blocks the request
// With cors: Browser allows the request

const cors = require("cors");
app.use(cors({ origin: "http://localhost:3000" }));
```
</details>

---

## Section C: Coding Exercises (5)

**Q16.** Create a custom logger middleware that logs the HTTP method, URL, and timestamp for every incoming request. Export it as a module and use it in a basic Express application with two routes (`/` and `/about`).

<details>
<summary>Answer</summary>

**logger.js:**

```javascript
function logger(req, res, next) {
    const timestamp = new Date().toISOString();
    const method = req.method;
    const url = req.url;

    console.log(`[${timestamp}] ${method} ${url}`);

    next();
}

module.exports = logger;
```

**server.js:**

```javascript
const express = require("express");
const logger = require("./logger");

const app = express();

// Apply logger middleware globally
app.use(logger);

app.get("/", (req, res) => {
    res.send("Home Page");
});

app.get("/about", (req, res) => {
    res.send("About Page");
});

app.listen(3000, () => {
    console.log("Server running on port 3000");
});
```

**Expected output when visiting both routes:**

```
[2025-06-15T10:00:00.000Z] GET /
[2025-06-15T10:00:05.000Z] GET /about
```
</details>

---

**Q17.** Build a complete set of RESTful routes for a `books` resource using an Express Router. Include routes for GET all, GET one by ID, POST, PUT, and DELETE. Use an in-memory array and return appropriate status codes for each operation.

<details>
<summary>Answer</summary>

```javascript
const express = require("express");
const app = express();
const router = express.Router();

app.use(express.json());

// In-memory data store
let books = [
    { id: 1, title: "The Great Gatsby", author: "F. Scott Fitzgerald" },
    { id: 2, title: "To Kill a Mockingbird", author: "Harper Lee" },
    { id: 3, title: "1984", author: "George Orwell" }
];

let nextId = 4;

// GET all books
router.get("/", (req, res) => {
    res.status(200).json(books);
});

// GET a single book by ID
router.get("/:id", (req, res) => {
    const book = books.find(b => b.id === parseInt(req.params.id));

    if (!book) {
        return res.status(404).json({ error: "Book not found" });
    }

    res.status(200).json(book);
});

// POST a new book
router.post("/", (req, res) => {
    const { title, author } = req.body;

    if (!title || !author) {
        return res.status(400).json({ error: "Title and author are required" });
    }

    const newBook = { id: nextId++, title, author };
    books.push(newBook);

    res.status(201).json(newBook);
});

// PUT (update) a book
router.put("/:id", (req, res) => {
    const book = books.find(b => b.id === parseInt(req.params.id));

    if (!book) {
        return res.status(404).json({ error: "Book not found" });
    }

    const { title, author } = req.body;

    if (!title || !author) {
        return res.status(400).json({ error: "Title and author are required" });
    }

    book.title = title;
    book.author = author;

    res.status(200).json(book);
});

// DELETE a book
router.delete("/:id", (req, res) => {
    const index = books.findIndex(b => b.id === parseInt(req.params.id));

    if (index === -1) {
        return res.status(404).json({ error: "Book not found" });
    }

    books.splice(index, 1);
    res.status(204).send();
});

// Mount router
app.use("/api/books", router);

app.listen(3000, () => {
    console.log("Server running on port 3000");
});
```
</details>

---

**Q18.** Write an error handling middleware that catches all errors and returns a structured JSON response. The response should include the error message, status code, and the stack trace only when the application is running in development mode. Test it with a route that deliberately throws an error.

<details>
<summary>Answer</summary>

```javascript
const express = require("express");
const app = express();

app.use(express.json());

// Route that works fine
app.get("/api/health", (req, res) => {
    res.json({ status: "OK" });
});

// Route that deliberately throws an error
app.get("/api/error", (req, res, next) => {
    const error = new Error("This is a test error");
    error.status = 400;
    next(error);
});

// Route that simulates a server crash
app.get("/api/crash", (req, res, next) => {
    try {
        // Simulate accessing a property on undefined
        const data = undefined;
        data.name; // This will throw a TypeError
    } catch (err) {
        next(err); // Forward to error handler
    }
});

// Centralized Error Handling Middleware (must be last)
app.use((err, req, res, next) => {
    const statusCode = err.status || 500;
    const message = err.message || "Internal Server Error";

    console.error(`[ERROR] ${statusCode}: ${message}`);

    const response = {
        success: false,
        status: statusCode,
        error: message
    };

    // Only include stack trace in development mode
    if (process.env.NODE_ENV === "development") {
        response.stack = err.stack;
    }

    res.status(statusCode).json(response);
});

app.listen(3000, () => {
    console.log("Server running on port 3000");
});
```

**Test with:**
- `GET /api/health` returns `{ status: "OK" }` with status 200
- `GET /api/error` returns `{ success: false, status: 400, error: "This is a test error" }`
- `GET /api/crash` returns `{ success: false, status: 500, error: "Cannot read properties of undefined (reading 'name')" }`
</details>

---

**Q19.** Set up an Express application that uses `cors`, `morgan`, and `helmet` as third-party middleware. Configure CORS to allow requests only from `http://localhost:3000`, allow only GET and POST methods, and enable credentials.

<details>
<summary>Answer</summary>

```bash
npm install express cors morgan helmet
```

```javascript
const express = require("express");
const cors = require("cors");
const morgan = require("morgan");
const helmet = require("helmet");

const app = express();

// Security headers
app.use(helmet());

// CORS configuration
app.use(cors({
    origin: "http://localhost:3000",       // Only allow this origin
    methods: ["GET", "POST"],              // Only allow these methods
    credentials: true                      // Allow cookies and auth headers
}));

// Request logging
app.use(morgan("dev"));

// Body parsing
app.use(express.json());

// Sample routes
app.get("/api/data", (req, res) => {
    res.json({
        message: "This data is accessible from http://localhost:3000",
        items: ["Item 1", "Item 2", "Item 3"]
    });
});

app.post("/api/data", (req, res) => {
    res.status(201).json({
        message: "Data created",
        data: req.body
    });
});

// This route exists but DELETE is not allowed by CORS
app.delete("/api/data/:id", (req, res) => {
    res.status(204).send();
});

app.listen(5000, () => {
    console.log("API server running on port 5000");
});
```

**When a request comes from `http://localhost:3000`:**
- `GET /api/data` -- Allowed (200 OK)
- `POST /api/data` -- Allowed (201 Created)
- `DELETE /api/data/1` -- Blocked by CORS (method not in allowed list)

**When a request comes from `http://localhost:8080`:**
- All requests blocked by CORS (origin not allowed)
</details>

---

**Q20.** Build a complete REST API structure for a `tasks` resource. Include: JSON parsing middleware, a custom request-timing middleware that logs how long each request takes, full CRUD routes with proper status codes, and a centralized error handler.

<details>
<summary>Answer</summary>

```javascript
const express = require("express");
const app = express();

// ---------- MIDDLEWARE ----------

// Parse JSON bodies
app.use(express.json());

// Custom Request Timing Middleware
app.use((req, res, next) => {
    const start = Date.now();

    // Listen for when the response finishes
    res.on("finish", () => {
        const duration = Date.now() - start;
        console.log(
            `${req.method} ${req.url} - ${res.statusCode} - ${duration}ms`
        );
    });

    next();
});

// ---------- DATA STORE ----------

let tasks = [
    { id: 1, title: "Learn Express", completed: false },
    { id: 2, title: "Build REST API", completed: false },
    { id: 3, title: "Study Middleware", completed: true }
];
let nextId = 4;

// ---------- ROUTES ----------

// GET all tasks
app.get("/api/tasks", (req, res) => {
    res.status(200).json({
        success: true,
        count: tasks.length,
        data: tasks
    });
});

// GET single task
app.get("/api/tasks/:id", (req, res, next) => {
    const task = tasks.find(t => t.id === parseInt(req.params.id));

    if (!task) {
        const error = new Error(`Task with ID ${req.params.id} not found`);
        error.status = 404;
        return next(error);
    }

    res.status(200).json({ success: true, data: task });
});

// POST new task
app.post("/api/tasks", (req, res, next) => {
    const { title } = req.body;

    if (!title || title.trim() === "") {
        const error = new Error("Title is required and cannot be empty");
        error.status = 400;
        return next(error);
    }

    const newTask = {
        id: nextId++,
        title: title.trim(),
        completed: false
    };

    tasks.push(newTask);
    res.status(201).json({ success: true, data: newTask });
});

// PUT update task
app.put("/api/tasks/:id", (req, res, next) => {
    const task = tasks.find(t => t.id === parseInt(req.params.id));

    if (!task) {
        const error = new Error(`Task with ID ${req.params.id} not found`);
        error.status = 404;
        return next(error);
    }

    const { title, completed } = req.body;

    if (!title || title.trim() === "") {
        const error = new Error("Title is required");
        error.status = 400;
        return next(error);
    }

    task.title = title.trim();
    task.completed = Boolean(completed);

    res.status(200).json({ success: true, data: task });
});

// DELETE task
app.delete("/api/tasks/:id", (req, res, next) => {
    const index = tasks.findIndex(t => t.id === parseInt(req.params.id));

    if (index === -1) {
        const error = new Error(`Task with ID ${req.params.id} not found`);
        error.status = 404;
        return next(error);
    }

    tasks.splice(index, 1);
    res.status(204).send();
});

// ---------- ERROR HANDLER (must be last) ----------

app.use((err, req, res, next) => {
    const statusCode = err.status || 500;
    const message = err.message || "Internal Server Error";

    console.error(`[ERROR] ${statusCode}: ${message}`);

    res.status(statusCode).json({
        success: false,
        error: message
    });
});

// ---------- START SERVER ----------

app.listen(3000, () => {
    console.log("Task API running on http://localhost:3000");
});
```

**Sample console output:**
```
GET /api/tasks - 200 - 3ms
GET /api/tasks/1 - 200 - 1ms
POST /api/tasks - 201 - 2ms
GET /api/tasks/999 - 404 - 1ms
DELETE /api/tasks/2 - 204 - 1ms
```
</details>

---

*End of Week 25 Practice Questions.*
