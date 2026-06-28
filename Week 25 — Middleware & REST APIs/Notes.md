# Week 25: Middleware & REST APIs

A comprehensive guide to Express.js middleware and RESTful API design. This document builds on the Express.js fundamentals covered in Week 24 and introduces the middleware pipeline, error handling patterns, and the principles behind designing clean, professional REST APIs.

---

## Table of Contents

1. [What is Middleware?](#1-what-is-middleware)
   - [Real-Life Analogy: Airport Security](#11-real-life-analogy-airport-security)
   - [The Request Pipeline](#12-the-request-pipeline)
   - [How Middleware Works in Code](#13-how-middleware-works-in-code)
2. [Built-in Middleware](#2-built-in-middleware)
   - [express.json()](#21-expressjson)
   - [express.urlencoded()](#22-expressurlencoded)
   - [express.static()](#23-expressstatic)
3. [Custom Middleware](#3-custom-middleware)
   - [Creating a Logger Middleware](#31-creating-a-logger-middleware)
   - [Authentication Check Middleware](#32-authentication-check-middleware)
   - [Application-Level vs Route-Level Middleware](#33-application-level-vs-route-level-middleware)
4. [Third-Party Middleware](#4-third-party-middleware)
   - [cors](#41-cors)
   - [morgan](#42-morgan)
   - [helmet](#43-helmet)
5. [Error Handling Middleware](#5-error-handling-middleware)
   - [The Four-Parameter Signature](#51-the-four-parameter-signature)
   - [Throwing and Forwarding Errors](#52-throwing-and-forwarding-errors)
   - [Centralized Error Handler](#53-centralized-error-handler)
6. [What is a REST API?](#6-what-is-a-rest-api)
   - [Understanding APIs](#61-understanding-apis)
   - [What Makes an API RESTful?](#62-what-makes-an-api-restful)
7. [REST Principles](#7-rest-principles)
8. [HTTP Methods](#8-http-methods)
9. [HTTP Status Codes](#9-http-status-codes)
10. [RESTful URL Design](#10-restful-url-design)
    - [Good vs Bad URL Examples](#101-good-vs-bad-url-examples)
    - [URL Design Rules](#102-url-design-rules)
11. [Summary](#11-summary)

---

## 1. What is Middleware?

Middleware is a function that sits **between** the incoming request and the final route handler. It has access to the request object (`req`), the response object (`res`), and a `next` function that passes control to the next middleware in the chain.

Every time a request reaches your Express server, it travels through a pipeline of middleware functions before arriving at the route handler that sends back a response.

```
Middleware Function Signature:

function middlewareName(req, res, next) {
    // Do something with req or res
    next();  // Pass control to the next middleware
}
```

### 1.1 Real-Life Analogy: Airport Security

Think of middleware like the checkpoints you pass through at an airport before boarding your flight.

```
+------------------------------------------------------------------+
|                    AIRPORT JOURNEY (Request Pipeline)             |
+------------------------------------------------------------------+
|                                                                    |
|  PASSENGER (Request)                                               |
|       |                                                            |
|       v                                                            |
|  +-----------------+                                               |
|  | CHECK-IN DESK   |  <-- Middleware 1: Parse & validate ticket    |
|  +-----------------+                                               |
|       |                                                            |
|       v                                                            |
|  +-----------------+                                               |
|  | SECURITY SCAN   |  <-- Middleware 2: Authentication check       |
|  +-----------------+                                               |
|       |                                                            |
|       v                                                            |
|  +-----------------+                                               |
|  | PASSPORT CHECK  |  <-- Middleware 3: Authorization check        |
|  +-----------------+                                               |
|       |                                                            |
|       v                                                            |
|  +-----------------+                                               |
|  | BOARDING GATE   |  <-- Route Handler: Final destination         |
|  +-----------------+                                               |
|       |                                                            |
|       v                                                            |
|  FLIGHT (Response)                                                 |
|                                                                    |
+------------------------------------------------------------------+
```

At each checkpoint:
- The passenger (request) can be **inspected** -- read the ticket, scan bags.
- The passenger can be **modified** -- add a boarding pass, stamp a passport.
- The passenger can be **rejected** -- denied entry if documents are invalid.
- The passenger can be **forwarded** -- sent to the next checkpoint.

Middleware works exactly the same way. Each middleware function can read the request, modify it, reject it (send an error response), or pass it forward with `next()`.

### 1.2 The Request Pipeline

Here is how Express processes every incoming request:

```
   Client Request
        |
        v
+------------------+
|  express.json()  |  Built-in: Parse JSON body
+------------------+
        |
        v
+------------------+
|  Logger          |  Custom: Log request details
+------------------+
        |
        v
+------------------+
|  Auth Check      |  Custom: Verify user token
+------------------+
        |
        v
+------------------+
|  CORS            |  Third-party: Handle cross-origin
+------------------+
        |
        v
+------------------+
|  Route Handler   |  Your actual route logic
+------------------+
        |
        v
+------------------+
|  Error Handler   |  Catches any errors from above
+------------------+
        |
        v
   Client Response
```

**Key Rule:** Middleware executes in the **order it is registered**. If you register authentication middleware before your routes, every route will require authentication. If you register it after, no route will be protected.

### 1.3 How Middleware Works in Code

```javascript
const express = require("express");
const app = express();

// Middleware 1: Runs for EVERY request
app.use((req, res, next) => {
    console.log("Middleware 1: Request received");
    next(); // Pass to next middleware
});

// Middleware 2: Runs for EVERY request
app.use((req, res, next) => {
    console.log("Middleware 2: Processing...");
    next(); // Pass to route handler
});

// Route Handler: Final destination
app.get("/", (req, res) => {
    console.log("Route Handler: Sending response");
    res.send("Hello World");
});

app.listen(3000);
```

**Console output when visiting `/`:**
```
Middleware 1: Request received
Middleware 2: Processing...
Route Handler: Sending response
```

**What happens if you forget `next()`?** The request gets stuck. The client waits forever and eventually times out. The middleware holds onto the request and never passes it forward -- like a security checkpoint where the officer walks away with your passport and never comes back.

---

## 2. Built-in Middleware

Express ships with three built-in middleware functions. You do not need to install anything extra to use them.

### 2.1 express.json()

Parses incoming request bodies that contain JSON data. Without this middleware, `req.body` is `undefined` when a client sends JSON.

```javascript
const express = require("express");
const app = express();

// Enable JSON body parsing
app.use(express.json());

app.post("/api/users", (req, res) => {
    console.log(req.body); // { name: "Fahad", email: "fahad@example.com" }
    res.json({ message: "User received", user: req.body });
});

app.listen(3000);
```

**What happens behind the scenes:**

```
Client sends POST request with body:
{ "name": "Fahad", "email": "fahad@example.com" }

                    Without express.json()          With express.json()
                    ----------------------          -------------------
req.body =          undefined                       { name: "Fahad", email: "fahad@example.com" }
```

### 2.2 express.urlencoded()

Parses incoming request bodies from HTML forms. When a user submits a traditional HTML form, the data is sent in `application/x-www-form-urlencoded` format (like `name=Fahad&email=fahad@example.com`).

```javascript
// Enable form data parsing
app.use(express.urlencoded({ extended: true }));

app.post("/login", (req, res) => {
    const { username, password } = req.body;
    console.log(username, password); // Values from the form
    res.send("Login received");
});
```

**The `extended: true` option** allows parsing of nested objects and arrays. With `extended: false`, only simple key-value pairs are supported.

### 2.3 express.static()

Serves static files (HTML, CSS, images, JavaScript files) directly from a folder. This is how you serve your frontend files from an Express server.

```javascript
// Serve all files from the "public" folder
app.use(express.static("public"));
```

**Project folder structure:**

```
my-project/
    server.js
    public/
        index.html
        style.css
        logo.png
        js/
            app.js
```

Now these files are accessible directly:
- `http://localhost:3000/index.html`
- `http://localhost:3000/style.css`
- `http://localhost:3000/logo.png`
- `http://localhost:3000/js/app.js`

You can also set a URL prefix:

```javascript
app.use("/static", express.static("public"));
// Now access via: http://localhost:3000/static/style.css
```

---

## 3. Custom Middleware

You can create your own middleware functions for any purpose -- logging, authentication, validation, rate limiting, or anything else your application needs.

### 3.1 Creating a Logger Middleware

A logger middleware records information about every incoming request. This is extremely useful for debugging and monitoring.

```javascript
// logger.js - Custom Logger Middleware
function logger(req, res, next) {
    const timestamp = new Date().toISOString();
    const method = req.method;
    const url = req.url;

    console.log(`[${timestamp}] ${method} ${url}`);

    next(); // Always call next() to continue
}

module.exports = logger;
```

```javascript
// server.js
const express = require("express");
const logger = require("./logger");

const app = express();

// Apply logger to ALL routes
app.use(logger);

app.get("/", (req, res) => {
    res.send("Home Page");
});

app.get("/about", (req, res) => {
    res.send("About Page");
});

app.listen(3000);
```

**Console output:**
```
[2025-06-15T10:30:45.123Z] GET /
[2025-06-15T10:30:52.456Z] GET /about
```

### 3.2 Authentication Check Middleware

This middleware checks if the user has provided a valid token before allowing access to protected routes.

```javascript
// authMiddleware.js
function authCheck(req, res, next) {
    const token = req.headers["authorization"];

    if (!token) {
        return res.status(401).json({
            error: "Access denied. No token provided."
        });
    }

    // In a real application, you would verify the token here
    if (token !== "Bearer my-secret-token") {
        return res.status(403).json({
            error: "Invalid token."
        });
    }

    // Token is valid -- attach user info and continue
    req.user = { id: 1, name: "Fahad" };
    next();
}

module.exports = authCheck;
```

**Notice:** When authentication fails, we send a response and **do not** call `next()`. This stops the request from reaching the route handler. The request is rejected at the checkpoint.

### 3.3 Application-Level vs Route-Level Middleware

**Application-level middleware** runs on every single request:

```javascript
// Applies to ALL routes
app.use(logger);
app.use(express.json());
```

**Route-level middleware** runs only on specific routes:

```javascript
// Only the /dashboard route requires authentication
app.get("/dashboard", authCheck, (req, res) => {
    res.send(`Welcome ${req.user.name}`);
});

// The home page is public -- no authCheck
app.get("/", (req, res) => {
    res.send("Public Home Page");
});
```

You can also apply middleware to a group of routes using `express.Router()`:

```javascript
const router = express.Router();

// All routes in this router require authentication
router.use(authCheck);

router.get("/profile", (req, res) => {
    res.json({ user: req.user });
});

router.get("/settings", (req, res) => {
    res.json({ settings: {} });
});

// Mount the router
app.use("/api", router);
// /api/profile and /api/settings now both require auth
```

---

## 4. Third-Party Middleware

The Express ecosystem has hundreds of middleware packages on npm. Here are the three most commonly used ones.

### 4.1 cors

**CORS** (Cross-Origin Resource Sharing) controls which websites can make requests to your API. By default, browsers block requests from a different origin (domain, port, or protocol) for security.

```bash
npm install cors
```

```javascript
const cors = require("cors");

// Allow ALL origins (development only)
app.use(cors());

// Allow specific origins (production)
app.use(cors({
    origin: "https://mywebsite.com",
    methods: ["GET", "POST", "PUT", "DELETE"],
    credentials: true
}));
```

**Real-life scenario:** Your React app runs on `http://localhost:3000` and your API runs on `http://localhost:5000`. Without CORS middleware, the browser blocks the React app from calling the API because they are on different ports (different origins).

### 4.2 morgan

Morgan is a professional HTTP request logger. It provides pre-built logging formats that are more detailed than a custom logger.

```bash
npm install morgan
```

```javascript
const morgan = require("morgan");

// "dev" format: colored, concise output for development
app.use(morgan("dev"));
// Output: GET /api/users 200 5.123 ms - 245

// "combined" format: Apache-style logs for production
app.use(morgan("combined"));
// Output: ::1 - - [15/Jun/2025:10:30:45 +0000] "GET /api/users HTTP/1.1" 200 245
```

### 4.3 helmet

Helmet sets various HTTP security headers to protect your app from common web vulnerabilities like cross-site scripting (XSS), clickjacking, and MIME type sniffing.

```bash
npm install helmet
```

```javascript
const helmet = require("helmet");

app.use(helmet());
```

**What helmet does behind the scenes:**

| Header Set by Helmet           | Protection Against                        |
|--------------------------------|-------------------------------------------|
| `X-XSS-Protection`            | Cross-site scripting attacks              |
| `X-Frame-Options`             | Clickjacking (embedding in iframes)       |
| `X-Content-Type-Options`      | MIME type sniffing                         |
| `Strict-Transport-Security`   | Forces HTTPS connections                  |
| `Content-Security-Policy`     | Unauthorized script injection             |

---

## 5. Error Handling Middleware

Error handling middleware is special in Express. It has **four** parameters instead of the usual three.

### 5.1 The Four-Parameter Signature

```javascript
// Regular middleware:  (req, res, next)     -- 3 parameters
// Error middleware:    (err, req, res, next) -- 4 parameters

app.use((err, req, res, next) => {
    console.error(err.message);
    res.status(500).json({ error: "Something went wrong" });
});
```

**Important:** Express identifies error handling middleware by counting its parameters. You **must** include all four parameters (`err`, `req`, `res`, `next`), even if you do not use `next`. If you only write three, Express treats it as regular middleware.

### 5.2 Throwing and Forwarding Errors

There are two ways to trigger error handling middleware:

**Method 1: Pass an error to `next()`**

```javascript
app.get("/api/users/:id", (req, res, next) => {
    const user = users.find(u => u.id === parseInt(req.params.id));

    if (!user) {
        const error = new Error("User not found");
        error.status = 404;
        return next(error); // Forward to error handler
    }

    res.json(user);
});
```

**Method 2: Throw inside an async route (with wrapper)**

```javascript
// Async error wrapper
function asyncHandler(fn) {
    return (req, res, next) => {
        Promise.resolve(fn(req, res, next)).catch(next);
    };
}

app.get("/api/data", asyncHandler(async (req, res) => {
    const data = await fetchDataFromDatabase(); // If this throws, error handler catches it
    res.json(data);
}));
```

### 5.3 Centralized Error Handler

A centralized error handler sits at the **end** of your middleware stack and catches all errors from the routes above it.

```javascript
const express = require("express");
const app = express();

app.use(express.json());

// --- Your routes go here ---

app.get("/api/test", (req, res, next) => {
    try {
        // Simulate an error
        throw new Error("Something broke!");
    } catch (err) {
        next(err); // Forward to error handler
    }
});

// --- Error handling middleware (MUST be last) ---

app.use((err, req, res, next) => {
    const statusCode = err.status || 500;
    const message = err.message || "Internal Server Error";

    console.error(`[ERROR] ${statusCode}: ${message}`);

    res.status(statusCode).json({
        success: false,
        error: message,
        // Only show stack trace in development
        stack: process.env.NODE_ENV === "development" ? err.stack : undefined
    });
});

app.listen(3000);
```

**Why centralized?** Instead of writing `try-catch` blocks and error responses in every single route, you forward all errors to one place. This keeps your route handlers clean and your error responses consistent.

---

## 6. What is a REST API?

### 6.1 Understanding APIs

An **API** (Application Programming Interface) is a set of rules that allows one piece of software to communicate with another.

**Real-Life Analogy: A Restaurant**

```
+-------------------+         +-------------------+         +-------------------+
|                   |         |                   |         |                   |
|    CUSTOMER       | ------> |     WAITER        | ------> |     KITCHEN       |
|   (Client /       |         |    (API)          |         |   (Server /       |
|    Frontend)      | <------ |                   | <------ |    Database)      |
|                   |  Food   |  Takes order,     |  Cooks  |                   |
|   Places order    |         |  delivers food    |  food   |  Prepares food    |
+-------------------+         +-------------------+         +-------------------+
```

- The **customer** (client) does not walk into the kitchen. They interact only through the waiter.
- The **waiter** (API) takes requests from the customer, delivers them to the kitchen, and brings back the result.
- The **kitchen** (server) does the actual work but is hidden from the customer.

A **REST API** is an API that follows a specific set of architectural rules called REST (Representational State Transfer). It uses standard HTTP methods and URLs to perform operations on resources.

### 6.2 What Makes an API RESTful?

A RESTful API treats everything as a **resource** (users, products, orders) and uses standard HTTP methods to perform actions on those resources.

```
Resource: Users

GET    /api/users       --> Get all users
GET    /api/users/5     --> Get user with ID 5
POST   /api/users       --> Create a new user
PUT    /api/users/5     --> Update user with ID 5
DELETE /api/users/5     --> Delete user with ID 5
```

---

## 7. REST Principles

REST APIs follow six core principles:

| Principle               | Meaning                                                                 | Example                                                       |
|-------------------------|-------------------------------------------------------------------------|---------------------------------------------------------------|
| **Client-Server**       | Frontend and backend are separate and independent                       | React app (client) talks to Express API (server)              |
| **Stateless**           | Each request contains all the info the server needs; no session memory  | Token sent with every request, server does not remember you   |
| **Cacheable**           | Responses can be cached to improve performance                          | Product list cached for 5 minutes                             |
| **Uniform Interface**   | Consistent URL structure and HTTP methods                               | Always use `/api/users`, not `/getUsers` or `/fetchAllUsers`  |
| **Layered System**      | Client does not know if it talks to the server directly or via proxy    | Load balancer sits between client and server                  |
| **Code on Demand**      | Server can optionally send executable code (rarely used)                | Server sends a JavaScript snippet to the client               |

**The Stateless Principle Explained:**

```
STATEFUL (Not REST):                    STATELESS (REST):
-----------------------                  -------------------------
Request 1: "I am Fahad"                  Request 1: "I am Fahad, here is
Server: "OK, I remember you"                        my token: abc123.
                                                     Give me my orders."
Request 2: "Give me my orders"           Server: "Token valid. Here
Server: "OK Fahad, here they are"                are your orders."
         (Server remembered who
          you are from Request 1)        Request 2: "Here is my token:
                                                     abc123. Update
                                                     my profile."
                                         Server: "Token valid. Profile
                                                  updated."
```

In a stateless API, the server does not store any information about the client between requests. Every request must carry its own authentication (usually a token).

---

## 8. HTTP Methods

HTTP methods (also called HTTP verbs) tell the server what action to perform on a resource.

| HTTP Method | CRUD Operation | Description                          | Request Body? | Example                        |
|-------------|----------------|--------------------------------------|---------------|---------------------------------|
| `GET`       | **Read**       | Retrieve data from the server        | No            | Get list of all products        |
| `POST`      | **Create**     | Send new data to the server          | Yes           | Create a new user account       |
| `PUT`       | **Update**     | Replace an existing resource entirely| Yes           | Update all fields of a product  |
| `PATCH`     | **Update**     | Partially update an existing resource| Yes           | Update only the price of a product |
| `DELETE`    | **Delete**     | Remove a resource from the server    | No            | Delete a user account           |

**GET vs POST comparison:**

```
GET Request:                              POST Request:
-------------------                       -------------------
GET /api/users                            POST /api/users
                                          Content-Type: application/json
No body                                   
                                          {
                                            "name": "Fahad",
                                            "email": "fahad@example.com"
                                          }

Response: List of all users               Response: The newly created user
```

**PUT vs PATCH comparison:**

```
PUT (Full Replace):                       PATCH (Partial Update):
----------------------------              ----------------------------
PUT /api/products/5                       PATCH /api/products/5
{                                         {
  "name": "Laptop",                         "price": 1200
  "price": 1200,                          }
  "category": "Electronics",
  "stock": 50                             Only the price field is updated.
}                                         All other fields stay the same.

ALL fields must be provided.
Missing fields may be set to null.
```

---

## 9. HTTP Status Codes

Status codes tell the client whether a request succeeded or failed, and why.

| Status Code | Name                    | Meaning                                              | When to Use                                      |
|-------------|-------------------------|------------------------------------------------------|--------------------------------------------------|
| `200`       | OK                      | The request succeeded                                | Successful GET, PUT, PATCH                        |
| `201`       | Created                 | A new resource was successfully created               | Successful POST that creates something            |
| `204`       | No Content              | Success, but nothing to send back                     | Successful DELETE                                 |
| `400`       | Bad Request             | The client sent invalid or malformed data             | Missing required fields, wrong data types         |
| `401`       | Unauthorized            | The client is not authenticated                       | No token provided, expired token                  |
| `403`       | Forbidden               | The client is authenticated but lacks permission      | Regular user trying to access admin route         |
| `404`       | Not Found               | The requested resource does not exist                 | User with ID 999 does not exist                   |
| `500`       | Internal Server Error   | Something went wrong on the server                    | Database crash, unhandled exception                |

**Status Code Categories:**

```
+-------+---------------------------+
| Range | Category                  |
+-------+---------------------------+
| 1xx   | Informational             |
| 2xx   | Success                   |
| 3xx   | Redirection               |
| 4xx   | Client Error (your fault) |
| 5xx   | Server Error (our fault)  |
+-------+---------------------------+
```

**Analogy:** Think of status codes like a delivery service.
- **200:** "Package delivered successfully."
- **201:** "New package has been created and shipped."
- **400:** "We cannot deliver -- the address you wrote is invalid."
- **401:** "We cannot deliver -- you did not provide your ID."
- **403:** "We verified your ID, but you are not authorized to receive this package."
- **404:** "The address does not exist."
- **500:** "Our delivery truck broke down. Sorry, it is our fault."

---

## 10. RESTful URL Design

### 10.1 Good vs Bad URL Examples

| Bad URL (Not RESTful)                    | Good URL (RESTful)            | Why It Is Better                             |
|------------------------------------------|-------------------------------|----------------------------------------------|
| `GET /getAllUsers`                        | `GET /api/users`              | Use nouns, not verbs. HTTP method implies the action. |
| `POST /createNewUser`                    | `POST /api/users`             | POST already means "create."                 |
| `GET /getUserById?id=5`                  | `GET /api/users/5`            | Use URL parameters, not query strings for IDs.|
| `DELETE /removeProduct/5`               | `DELETE /api/products/5`      | DELETE already means "remove."               |
| `GET /api/user`                          | `GET /api/users`              | Use plural nouns for collections.            |
| `PUT /api/updateUserEmail/5`            | `PUT /api/users/5`            | Do not put the action or field in the URL.   |
| `GET /api/users/5/getOrders`            | `GET /api/users/5/orders`     | Nested resources use nouns, not verbs.       |

### 10.2 URL Design Rules

1. **Use nouns, not verbs** -- The HTTP method already describes the action.
2. **Use plural nouns** -- `/api/users` not `/api/user`.
3. **Use URL parameters for IDs** -- `/api/users/5` not `/api/users?id=5`.
4. **Nest related resources** -- `/api/users/5/orders` to get orders for user 5.
5. **Use query strings for filtering and sorting** -- `/api/products?category=electronics&sort=price`.
6. **Use a consistent prefix** -- `/api/` makes it clear these are API endpoints.
7. **Use lowercase and hyphens** -- `/api/order-items` not `/api/OrderItems` or `/api/order_items`.

**Complete RESTful URL structure for an e-commerce API:**

```
USERS:
  GET    /api/users              Get all users
  GET    /api/users/5            Get user 5
  POST   /api/users              Create a new user
  PUT    /api/users/5            Update user 5
  DELETE /api/users/5            Delete user 5

PRODUCTS:
  GET    /api/products           Get all products
  GET    /api/products/12        Get product 12
  POST   /api/products           Create a new product
  PUT    /api/products/12        Update product 12
  DELETE /api/products/12        Delete product 12

NESTED RESOURCES:
  GET    /api/users/5/orders     Get all orders for user 5
  GET    /api/users/5/orders/3   Get order 3 for user 5
  POST   /api/users/5/orders     Create a new order for user 5

FILTERING & SORTING:
  GET    /api/products?category=electronics
  GET    /api/products?minPrice=100&maxPrice=500
  GET    /api/products?sort=price&order=desc
  GET    /api/products?page=2&limit=10
```

---

## 11. Summary

| Topic                   | Key Takeaway                                                                 |
|-------------------------|------------------------------------------------------------------------------|
| **Middleware**          | Functions that process requests before they reach route handlers              |
| **Built-in Middleware** | `express.json()`, `express.urlencoded()`, `express.static()`                 |
| **Custom Middleware**   | You can write your own for logging, auth, validation, and more               |
| **Third-party**         | `cors`, `morgan`, `helmet` are the most commonly used packages               |
| **Error Handling**      | Uses four parameters `(err, req, res, next)` and must be registered last     |
| **REST API**            | An API that uses HTTP methods and structured URLs to manage resources         |
| **HTTP Methods**        | GET (Read), POST (Create), PUT (Update), DELETE (Delete)                     |
| **Status Codes**        | 2xx = Success, 4xx = Client error, 5xx = Server error                        |
| **URL Design**          | Use plural nouns, URL params for IDs, query strings for filtering            |

**Middleware Execution Order Recap:**

```
Request --> express.json() --> cors() --> morgan() --> authCheck --> Route Handler
                                                                        |
                                                                        v
Response <------------------------- Error Handler <--------- (if error thrown)
```

---

*Next week, we will put these concepts into practice by building a complete CRUD API with validation, file uploads, and the MVC pattern.*
