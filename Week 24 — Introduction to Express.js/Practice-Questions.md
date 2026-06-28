# Week 24 — Introduction to Express.js: Practice Questions

**Total Questions: 20** (10 MCQs + 5 Short Answer + 5 Coding Exercises)

---

## Part 1: Multiple Choice Questions (MCQs)

**1. What is Express.js?**

- A) A database for Node.js
- B) A frontend JavaScript framework
- C) A minimal web framework for Node.js
- D) A replacement for npm

<details>
<summary>Answer</summary>

**C) A minimal web framework for Node.js**

Express.js is a fast, unopinionated, and minimalist web framework that sits on top of Node.js's built-in `http` module. It simplifies creating web servers, defining routes, handling requests, and building APIs. It was created in 2010 and is the most widely used Node.js framework.
</details>

---

**2. Which command correctly installs Express in a project?**

- A) `npm init express`
- B) `npm install express`
- C) `npm create express-app`
- D) `node install express`

<details>
<summary>Answer</summary>

**B) `npm install express`**

Express is a regular npm package. You install it with `npm install express` (or the shorthand `npm i express`). This adds it to the `dependencies` section of your `package.json` and downloads it into `node_modules`.
</details>

---

**3. What does `app.use(express.json())` do?**

- A) Converts the entire application to JSON format
- B) Parses incoming JSON request bodies and makes the data available in `req.body`
- C) Sends all responses as JSON automatically
- D) Validates that all data is valid JSON

<details>
<summary>Answer</summary>

**B) Parses incoming JSON request bodies and makes the data available in `req.body`**

`express.json()` is a built-in middleware that reads the raw JSON string from incoming requests (with `Content-Type: application/json`) and converts it into a JavaScript object. Without this middleware, `req.body` will be `undefined` when clients send JSON data.
</details>

---

**4. Which route definition correctly captures a dynamic user ID from the URL?**

- A) `app.get("/users/id", ...)`
- B) `app.get("/users/{id}", ...)`
- C) `app.get("/users/:id", ...)`
- D) `app.get("/users/$id", ...)`

<details>
<summary>Answer</summary>

**C) `app.get("/users/:id", ...)`**

In Express, route parameters are defined by prefixing a segment with a colon (`:`). When a request matches this route (e.g., `/users/42`), Express captures the value and makes it available in `req.params.id`. The value is always a string, so you must convert it with `parseInt()` if you need a number.
</details>

---

**5. Given the URL `/api/products?category=electronics&limit=10`, how do you access the `category` value in Express?**

- A) `req.params.category`
- B) `req.body.category`
- C) `req.query.category`
- D) `req.url.category`

<details>
<summary>Answer</summary>

**C) `req.query.category`**

Query parameters (the key-value pairs after `?` in a URL) are automatically parsed by Express and made available in the `req.query` object. In this case, `req.query` would be `{ category: "electronics", limit: "10" }`. Note that all query values are strings.
</details>

---

**6. What HTTP status code should be returned when a new resource is successfully created?**

- A) 200 OK
- B) 201 Created
- C) 204 No Content
- D) 301 Moved Permanently

<details>
<summary>Answer</summary>

**B) 201 Created**

The 201 status code indicates that the request was successful and resulted in the creation of a new resource. It is the standard response for successful POST requests that create data. For example: `res.status(201).json(newUser)`.
</details>

---

**7. What does `express.static("public")` do?**

- A) Creates a public folder
- B) Encrypts files in the public folder
- C) Serves files from the "public" directory as static assets
- D) Uploads files to the public folder

<details>
<summary>Answer</summary>

**C) Serves files from the "public" directory as static assets**

`express.static()` is a built-in middleware that serves static files (HTML, CSS, JavaScript, images, fonts) from the specified directory. When you write `app.use(express.static("public"))`, a request to `/style.css` will serve the file at `public/style.css`. This is how you serve frontend files from an Express server.
</details>

---

**8. What is the purpose of `express.Router()`?**

- A) To create a new Express application
- B) To organize routes into separate, modular files
- C) To handle database routing
- D) To redirect all traffic to HTTPS

<details>
<summary>Answer</summary>

**B) To organize routes into separate, modular files**

`express.Router()` creates a mini Express application that only handles routes. You define routes on the router (e.g., `router.get("/", handler)`), export it from a module, and mount it in your main file with `app.use("/api/users", userRouter)`. This keeps your code organized as your application grows.
</details>

---

**9. What happens if you forget to call `res.send()`, `res.json()`, or any response method in a route handler?**

- A) Express automatically sends a 200 response
- B) The client's request will hang indefinitely (never receive a response)
- C) Express throws an error and crashes
- D) The client receives an empty 404 response

<details>
<summary>Answer</summary>

**B) The client's request will hang indefinitely (never receive a response)**

If a route handler does not send a response, the client will wait forever (until a timeout occurs). Express does not automatically send a response — it is your responsibility to call a response method like `res.send()`, `res.json()`, or `res.end()` in every route handler. This is a common bug, especially when forgetting to send a response in error-handling branches.
</details>

---

**10. Which of the following is the correct order of the Express request-response cycle?**

- A) Route matching, Middleware, Handler, Response
- B) Middleware, Route matching, Handler, Response
- C) Handler, Middleware, Route matching, Response
- D) Response, Middleware, Route matching, Handler

<details>
<summary>Answer</summary>

**B) Middleware, Route matching, Handler, Response**

When a request arrives, Express first runs it through any registered middleware (like `express.json()`, logging, authentication). Then it tries to match the request's method and URL to a defined route. If a match is found, the route's handler function executes. Finally, the handler sends a response back to the client using methods like `res.json()`.
</details>

---

## Part 2: Short Answer Questions

**1. Explain the GPS analogy for Express.js. Why is Express compared to a GPS, and what is Node.js's `http` module compared to in this analogy?**

<details>
<summary>Answer</summary>

In this analogy, Node.js's raw `http` module is compared to **driving through a city without GPS**. You can technically reach your destination, but you have to figure out every turn yourself — manually parsing URLs, handling different HTTP methods with `if/else` chains, reading request bodies chunk by chunk, and setting response headers.

Express.js is compared to a **GPS** because it handles the complicated navigation logic for you. It provides clear, named routes (`app.get("/users")`), automatic URL parsing (`req.params`, `req.query`), built-in body parsing (`express.json()`), and clean response methods (`res.json()`). Just as a GPS lets you focus on driving instead of map reading, Express lets you focus on your application logic instead of low-level HTTP handling.
</details>

---

**2. What is the difference between `req.params`, `req.query`, and `req.body`? Give a URL or request example for each.**

<details>
<summary>Answer</summary>

**`req.params`** — Captures dynamic values from the URL **path**. Defined with a colon in the route.
- Route: `app.get("/users/:id")`
- URL: `/users/42`
- Result: `req.params = { id: "42" }`

**`req.query`** — Captures key-value pairs from the URL **query string** (after the `?`). No route definition needed.
- Route: `app.get("/products")`
- URL: `/products?category=electronics&sort=price`
- Result: `req.query = { category: "electronics", sort: "price" }`

**`req.body`** — Contains data sent in the **request body**, typically with POST or PUT requests. Requires `express.json()` middleware.
- Route: `app.post("/users")`
- Request body (JSON): `{ "name": "Ali", "email": "ali@example.com" }`
- Result: `req.body = { name: "Ali", email: "ali@example.com" }`

In summary: **params** identify a resource, **query** filters/sorts results, and **body** sends data to create or update resources.
</details>

---

**3. Why is it important to use `res.status()` with the correct HTTP status code instead of always sending 200?**

<details>
<summary>Answer</summary>

HTTP status codes communicate the **result** of the request to the client. Using the correct code is important for several reasons:

1. **Client-side handling:** Frontend applications (like React) use status codes to decide how to handle responses. A 401 might redirect to a login page, while a 200 displays the data normally.

2. **Debugging:** When something goes wrong, the status code immediately tells developers what type of error occurred (400 = bad input, 404 = wrong URL, 500 = server crash).

3. **API standards:** REST API conventions expect specific codes. `201` for created resources, `204` for successful deletions with no content, `404` for missing resources. APIs that always return 200 are harder to work with.

4. **Search engines and caching:** Browsers and proxies use status codes to decide whether to cache responses, retry requests, or report errors.

5. **Professional quality:** Correct status codes make your API predictable and trustworthy for other developers who consume it.
</details>

---

**4. What is `express.Router()` and how does it help organize a large application? Describe the steps to set it up.**

<details>
<summary>Answer</summary>

`express.Router()` creates a modular, mountable route handler — essentially a mini Express application that only deals with routing. It helps organize large applications by allowing you to split routes into separate files based on resource type.

**Steps to set it up:**

1. **Create a route file** (e.g., `routes/userRoutes.js`):
   - Import Express and create a router: `const router = express.Router()`
   - Define routes on the router: `router.get("/", handler)`, `router.post("/", handler)`
   - Export the router: `module.exports = router`

2. **Import and mount in the main file** (`index.js`):
   - Import the router: `const userRoutes = require("./routes/userRoutes")`
   - Mount it with a prefix: `app.use("/api/users", userRoutes)`

3. **Route paths are relative.** In the router file, `router.get("/")` becomes `GET /api/users` when mounted with `app.use("/api/users", ...)`. This means each router file stays clean and only cares about its own relative paths.

This pattern keeps your main file small and makes it easy to find, modify, and test routes for specific resources.
</details>

---

**5. What happens if you do not add `express.json()` middleware before your routes? How do you properly set it up?**

<details>
<summary>Answer</summary>

If you do not add `express.json()` middleware, `req.body` will be **`undefined`** for all incoming requests. When a client sends JSON data in a POST or PUT request, Express will not parse it, and any code that tries to access `req.body.name` or `req.body.email` will throw an error or return `undefined`.

**How to set it up properly:**

```javascript
const express = require("express");
const app = express();

// Add BEFORE any routes that need req.body
app.use(express.json());

// Now req.body is available in this route
app.post("/api/users", (req, res) => {
  console.log(req.body);   // { name: "Ali", email: "..." }
  res.status(201).json(req.body);
});
```

The key rule is that `app.use(express.json())` must come **before** any route definitions that access `req.body`. Middleware executes in the order it is defined, so placing it after your routes means the routes will never benefit from the parsing.
</details>

---

## Part 3: Coding Exercises

**1. Basic Express Server — Create a server with three routes**

Create an Express server that listens on port 3000 and has three routes:
- `GET /` responds with `"Welcome to the Express Server"`
- `GET /about` responds with a JSON object containing `name`, `version`, and `description` fields
- Any undefined route responds with a 404 JSON error message

<details>
<summary>Answer</summary>

```javascript
// index.js
const express = require("express");
const app = express();
const PORT = 3000;

// Home route
app.get("/", (req, res) => {
  res.send("Welcome to the Express Server");
});

// About route
app.get("/about", (req, res) => {
  res.json({
    name: "My Express API",
    version: "1.0.0",
    description: "A practice Express server for Week 24"
  });
});

// 404 handler (must be the last route)
app.use((req, res) => {
  res.status(404).json({
    error: "Route not found",
    requestedURL: req.originalUrl
  });
});

app.listen(PORT, () => {
  console.log(`Server running at http://localhost:${PORT}`);
});
```

**Testing:**
- `GET /` returns: `Welcome to the Express Server`
- `GET /about` returns: `{ "name": "My Express API", ... }`
- `GET /xyz` returns: `{ "error": "Route not found", "requestedURL": "/xyz" }` with status 404

**Key concepts:** Creating an Express app, defining routes with different response methods (`res.send()` vs `res.json()`), and adding a catch-all 404 handler at the end of the route definitions.
</details>

---

**2. Route Parameters — Build a book lookup API**

Create an Express server with an array of book objects (each with `id`, `title`, `author`, and `year`). Implement two routes:
- `GET /api/books` returns all books
- `GET /api/books/:id` returns a single book by its ID, or a 404 error if the book is not found

<details>
<summary>Answer</summary>

```javascript
// index.js
const express = require("express");
const app = express();

const books = [
  { id: 1, title: "The Great Gatsby", author: "F. Scott Fitzgerald", year: 1925 },
  { id: 2, title: "To Kill a Mockingbird", author: "Harper Lee", year: 1960 },
  { id: 3, title: "1984", author: "George Orwell", year: 1949 },
  { id: 4, title: "Pride and Prejudice", author: "Jane Austen", year: 1813 },
  { id: 5, title: "The Catcher in the Rye", author: "J.D. Salinger", year: 1951 }
];

// GET all books
app.get("/api/books", (req, res) => {
  res.json({
    count: books.length,
    data: books
  });
});

// GET a single book by ID
app.get("/api/books/:id", (req, res) => {
  const id = parseInt(req.params.id);
  const book = books.find((b) => b.id === id);

  if (!book) {
    return res.status(404).json({
      error: `Book with ID ${id} not found`
    });
  }

  res.json(book);
});

app.listen(3000, () => {
  console.log("Book API running at http://localhost:3000");
});
```

**Testing:**
- `GET /api/books` returns all 5 books with a count
- `GET /api/books/3` returns: `{ "id": 3, "title": "1984", "author": "George Orwell", "year": 1949 }`
- `GET /api/books/99` returns: `{ "error": "Book with ID 99 not found" }` with status 404

**Key concepts:** Using `req.params` to capture dynamic URL segments, converting the parameter string to a number with `parseInt()`, using `Array.find()` to search data, and returning appropriate status codes.
</details>

---

**3. Query Parameters and Request Body — Build a filterable task API**

Create an Express server with an array of tasks. Implement:
- `GET /api/tasks` returns all tasks, with optional filtering by `status` query parameter (e.g., `/api/tasks?status=completed`)
- `POST /api/tasks` creates a new task from the request body (expects `title` and `status` fields)
- Validate that `title` is provided when creating a task; return 400 if missing

<details>
<summary>Answer</summary>

```javascript
// index.js
const express = require("express");
const app = express();

// Middleware to parse JSON bodies
app.use(express.json());

let tasks = [
  { id: 1, title: "Learn Express basics", status: "completed" },
  { id: 2, title: "Build a REST API", status: "in-progress" },
  { id: 3, title: "Connect to a database", status: "pending" },
  { id: 4, title: "Write unit tests", status: "pending" }
];

// GET all tasks with optional status filter
app.get("/api/tasks", (req, res) => {
  let results = [...tasks];

  // Filter by status if query param is provided
  if (req.query.status) {
    results = results.filter((t) => t.status === req.query.status);
  }

  res.json({
    count: results.length,
    data: results
  });
});

// POST a new task
app.post("/api/tasks", (req, res) => {
  const { title, status } = req.body;

  // Validation
  if (!title || title.trim() === "") {
    return res.status(400).json({
      error: "Title is required and cannot be empty"
    });
  }

  const newTask = {
    id: tasks.length + 1,
    title: title.trim(),
    status: status || "pending"
  };

  tasks.push(newTask);

  res.status(201).json({
    message: "Task created successfully",
    task: newTask
  });
});

app.listen(3000, () => {
  console.log("Task API running at http://localhost:3000");
});
```

**Testing:**
- `GET /api/tasks` returns all 4 tasks
- `GET /api/tasks?status=pending` returns only pending tasks
- `POST /api/tasks` with body `{ "title": "Deploy to production" }` creates a new task with default status "pending"
- `POST /api/tasks` with body `{}` returns `{ "error": "Title is required..." }` with status 400

**Key concepts:** Using `req.query` for optional filtering, `req.body` for receiving client data, input validation with proper error responses, `express.json()` middleware, and defaulting values with `||`.
</details>

---

**4. Serving Static Files — Serve an HTML page with CSS**

Create an Express server that serves static files from a `public` folder. Create a simple `index.html` with a heading and a paragraph, and a `style.css` that styles the page. Also add an API route at `GET /api/info` that returns JSON data about the server.

<details>
<summary>Answer</summary>

**Project structure:**

```
my-static-app/
+-- index.js
+-- public/
|   +-- index.html
|   +-- css/
|       +-- style.css
+-- package.json
```

**`index.js`:**

```javascript
// index.js
const express = require("express");
const path = require("path");
const app = express();
const PORT = 3000;

// Serve static files from the "public" directory
app.use(express.static(path.join(__dirname, "public")));

// API route
app.get("/api/info", (req, res) => {
  res.json({
    server: "Express Static File Server",
    version: "1.0.0",
    staticDirectory: "public",
    timestamp: new Date().toISOString()
  });
});

app.listen(PORT, () => {
  console.log(`Server running at http://localhost:${PORT}`);
  console.log(`Static files served from: ${path.join(__dirname, "public")}`);
});
```

**`public/index.html`:**

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
  <div class="container">
    <h1>Welcome to My Express App</h1>
    <p>This page is served as a static file by Express.js.</p>
    <p>Visit <a href="/api/info">/api/info</a> to see the API response.</p>
  </div>
</body>
</html>
```

**`public/css/style.css`:**

```css
* {
  margin: 0;
  padding: 0;
  box-sizing: border-box;
}

body {
  font-family: Arial, sans-serif;
  background-color: #f0f2f5;
  display: flex;
  justify-content: center;
  align-items: center;
  min-height: 100vh;
}

.container {
  background: white;
  padding: 2rem 3rem;
  border-radius: 8px;
  box-shadow: 0 2px 10px rgba(0, 0, 0, 0.1);
  text-align: center;
}

h1 {
  color: #333;
  margin-bottom: 1rem;
}

p {
  color: #666;
  line-height: 1.6;
  margin-bottom: 0.5rem;
}

a {
  color: #0066cc;
}
```

**Testing:**
- Visit `http://localhost:3000` to see the styled HTML page
- Visit `http://localhost:3000/api/info` to see the JSON response
- Visit `http://localhost:3000/css/style.css` to see the raw CSS file

**Key concepts:** Using `express.static()` to serve files, using `path.join()` with `__dirname` for absolute paths, combining static file serving with API routes, and linking CSS files with absolute paths (`/css/style.css`).
</details>

---

**5. Modular Routing — Build an API with separate route files**

Create an Express application with two separate route files:
- `routes/studentRoutes.js` handles `GET /api/students` (list all) and `GET /api/students/:id` (get one)
- `routes/courseRoutes.js` handles `GET /api/courses` (list all) and `POST /api/courses` (create new)

Mount both routers in `index.js` with appropriate prefixes.

<details>
<summary>Answer</summary>

**Project structure:**

```
my-modular-app/
+-- index.js
+-- routes/
|   +-- studentRoutes.js
|   +-- courseRoutes.js
+-- package.json
```

**`routes/studentRoutes.js`:**

```javascript
// routes/studentRoutes.js
const express = require("express");
const router = express.Router();

const students = [
  { id: 1, name: "Ali Ahmed", grade: "A", major: "Computer Science" },
  { id: 2, name: "Sara Khan", grade: "B+", major: "Mathematics" },
  { id: 3, name: "Omar Farooq", grade: "A-", major: "Physics" }
];

// GET /api/students
router.get("/", (req, res) => {
  res.json({ count: students.length, data: students });
});

// GET /api/students/:id
router.get("/:id", (req, res) => {
  const id = parseInt(req.params.id);
  const student = students.find((s) => s.id === id);

  if (!student) {
    return res.status(404).json({ error: `Student with ID ${id} not found` });
  }

  res.json(student);
});

module.exports = router;
```

**`routes/courseRoutes.js`:**

```javascript
// routes/courseRoutes.js
const express = require("express");
const router = express.Router();

let courses = [
  { id: 1, name: "Web Development", instructor: "Dr. Ahmed", credits: 3 },
  { id: 2, name: "Data Structures", instructor: "Dr. Khan", credits: 4 }
];

// GET /api/courses
router.get("/", (req, res) => {
  res.json({ count: courses.length, data: courses });
});

// POST /api/courses
router.post("/", (req, res) => {
  const { name, instructor, credits } = req.body;

  if (!name || !instructor) {
    return res.status(400).json({
      error: "Course name and instructor are required"
    });
  }

  const newCourse = {
    id: courses.length + 1,
    name,
    instructor,
    credits: credits || 3
  };

  courses.push(newCourse);
  res.status(201).json({
    message: "Course created",
    course: newCourse
  });
});

module.exports = router;
```

**`index.js`:**

```javascript
// index.js
const express = require("express");
const app = express();
const PORT = 3000;

// Middleware
app.use(express.json());

// Import route modules
const studentRoutes = require("./routes/studentRoutes");
const courseRoutes = require("./routes/courseRoutes");

// Mount routes
app.use("/api/students", studentRoutes);
app.use("/api/courses", courseRoutes);

// Home route
app.get("/", (req, res) => {
  res.json({
    message: "Welcome to the University API",
    endpoints: {
      students: "/api/students",
      courses: "/api/courses"
    }
  });
});

// 404 handler
app.use((req, res) => {
  res.status(404).json({ error: "Endpoint not found" });
});

app.listen(PORT, () => {
  console.log(`University API running at http://localhost:${PORT}`);
});
```

**Testing:**
- `GET /` returns the welcome message with available endpoints
- `GET /api/students` returns all 3 students
- `GET /api/students/2` returns Sara Khan's data
- `GET /api/students/99` returns 404 error
- `GET /api/courses` returns all courses
- `POST /api/courses` with `{ "name": "AI", "instructor": "Dr. Lee" }` creates a new course
- `GET /unknown` returns 404 error

**Key concepts:** Using `express.Router()` to create modular route handlers, exporting routers with `module.exports`, mounting routers with `app.use()` and path prefixes, keeping the main file clean by delegating routing to separate modules, and adding a catch-all 404 handler at the end.
</details>

---

> **Tip:** Test all your Express APIs using Postman or Thunder Client (VS Code extension). For GET requests, you can use the browser. For POST, PUT, and DELETE requests, you need a tool that lets you set the HTTP method, headers, and request body. This is an essential skill for backend development.
