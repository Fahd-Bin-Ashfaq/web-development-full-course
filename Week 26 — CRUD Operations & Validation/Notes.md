# Week 26: CRUD Operations & Validation

A comprehensive guide to building complete CRUD APIs with data validation, file uploads, API testing, and the MVC architectural pattern. This document builds on the middleware and REST API concepts covered in Week 25 and moves into practical, production-quality backend development.

---

## Table of Contents

1. [CRUD Overview](#1-crud-overview)
   - [What is CRUD?](#11-what-is-crud)
   - [CRUD Mapped to HTTP Methods](#12-crud-mapped-to-http-methods)
2. [Building a Complete CRUD API](#2-building-a-complete-crud-api)
   - [Project Setup](#21-project-setup)
   - [GET All Items](#22-get-all-items)
   - [GET One Item by ID](#23-get-one-item-by-id)
   - [POST: Create a New Item](#24-post-create-a-new-item)
   - [PUT: Update an Item](#25-put-update-an-item)
   - [DELETE: Remove an Item](#26-delete-remove-an-item)
   - [Complete CRUD Server Code](#27-complete-crud-server-code)
3. [Request Validation with Joi](#3-request-validation-with-joi)
   - [Why Validate?](#31-why-validate)
   - [Installing and Using Joi](#32-installing-and-using-joi)
   - [Common Joi Validators](#33-common-joi-validators)
   - [Validation Middleware Pattern](#34-validation-middleware-pattern)
4. [express-validator Alternative](#4-express-validator-alternative)
5. [Centralized Error Handling](#5-centralized-error-handling)
   - [Custom Error Class](#51-custom-error-class)
   - [Async Error Wrapper](#52-async-error-wrapper)
   - [Error Handler Middleware](#53-error-handler-middleware)
6. [File Uploads with Multer](#6-file-uploads-with-multer)
   - [What is Multer?](#61-what-is-multer)
   - [Basic File Upload](#62-basic-file-upload)
   - [File Filtering and Limits](#63-file-filtering-and-limits)
7. [API Testing with Postman / Thunder Client](#7-api-testing-with-postman--thunder-client)
   - [Why Use API Testing Tools?](#71-why-use-api-testing-tools)
   - [Testing Each CRUD Operation](#72-testing-each-crud-operation)
8. [The MVC Pattern](#8-the-mvc-pattern)
   - [What is MVC?](#81-what-is-mvc)
   - [MVC Folder Structure](#82-mvc-folder-structure)
   - [Implementing MVC](#83-implementing-mvc)
9. [Summary](#9-summary)

---

## 1. CRUD Overview

### 1.1 What is CRUD?

CRUD stands for the four fundamental operations that every data-driven application performs:

```
+----------------------------------------------------------+
|                    CRUD OPERATIONS                        |
+----------------------------------------------------------+
|                                                            |
|   C  =  CREATE    -->  Add new data                        |
|   R  =  READ      -->  View / retrieve data                |
|   U  =  UPDATE    -->  Modify existing data                |
|   D  =  DELETE    -->  Remove data                         |
|                                                            |
+----------------------------------------------------------+
```

**Real-Life Analogy: A Phone Contacts App**

| Action in Contacts App        | CRUD Operation | What Happens                    |
|-------------------------------|----------------|---------------------------------|
| Add a new contact             | **Create**     | New entry saved to the list     |
| Open and view a contact       | **Read**       | Data retrieved and displayed    |
| Edit a contact's phone number | **Update**     | Existing entry modified         |
| Delete an old contact         | **Delete**     | Entry removed from the list     |

Every application you use daily -- social media, email, banking apps, e-commerce stores -- performs these four operations on data.

### 1.2 CRUD Mapped to HTTP Methods

| CRUD Operation | HTTP Method | URL Example          | Description                    |
|----------------|-------------|----------------------|--------------------------------|
| **Create**     | `POST`      | `/api/products`      | Add a new product              |
| **Read All**   | `GET`       | `/api/products`      | Get all products               |
| **Read One**   | `GET`       | `/api/products/5`    | Get product with ID 5          |
| **Update**     | `PUT`       | `/api/products/5`    | Update product with ID 5       |
| **Delete**     | `DELETE`    | `/api/products/5`    | Delete product with ID 5       |

```
CLIENT                              SERVER
+----------+    POST /api/products    +----------+
|          | -----------------------> |          |
|          |    { name, price }       |  CREATE  |
|          |                          |          |
|          |    GET /api/products     |          |
|          | -----------------------> |  READ    |
|          |                          |          |
|  Browser |    PUT /api/products/5   |  Express |
|  or      | -----------------------> |  API     |
|  Postman |    { name, price }       |  UPDATE  |
|          |                          |          |
|          |    DELETE /api/products/5 |          |
|          | -----------------------> |  DELETE  |
+----------+                          +----------+
```

---

## 2. Building a Complete CRUD API

We will build a complete CRUD API for managing products using an in-memory array. This approach lets you focus on the API logic without worrying about database setup (databases will be covered in later weeks).

### 2.1 Project Setup

```bash
mkdir products-api
cd products-api
npm init -y
npm install express
```

**Initial data structure:**

```javascript
let products = [
    { id: 1, name: "Laptop", price: 999, category: "Electronics" },
    { id: 2, name: "Running Shoes", price: 85, category: "Sports" },
    { id: 3, name: "Coffee Maker", price: 45, category: "Kitchen" }
];

let nextId = 4; // Auto-increment ID tracker
```

### 2.2 GET All Items

Retrieve the entire list of products.

```javascript
// GET /api/products - Get all products
app.get("/api/products", (req, res) => {
    res.status(200).json({
        success: true,
        count: products.length,
        data: products
    });
});
```

**Response:**
```json
{
    "success": true,
    "count": 3,
    "data": [
        { "id": 1, "name": "Laptop", "price": 999, "category": "Electronics" },
        { "id": 2, "name": "Running Shoes", "price": 85, "category": "Sports" },
        { "id": 3, "name": "Coffee Maker", "price": 45, "category": "Kitchen" }
    ]
}
```

### 2.3 GET One Item by ID

Retrieve a single product by its unique ID.

```javascript
// GET /api/products/:id - Get a single product
app.get("/api/products/:id", (req, res) => {
    const id = parseInt(req.params.id);
    const product = products.find(p => p.id === id);

    if (!product) {
        return res.status(404).json({
            success: false,
            error: `Product with ID ${id} not found`
        });
    }

    res.status(200).json({
        success: true,
        data: product
    });
});
```

**URL parameter:** The `:id` in `/api/products/:id` is a route parameter. When a request is made to `/api/products/2`, the value `2` is available as `req.params.id`.

### 2.4 POST: Create a New Item

Add a new product to the collection.

```javascript
// POST /api/products - Create a new product
app.post("/api/products", (req, res) => {
    const { name, price, category } = req.body;

    // Basic validation
    if (!name || !price || !category) {
        return res.status(400).json({
            success: false,
            error: "Please provide name, price, and category"
        });
    }

    if (typeof price !== "number" || price <= 0) {
        return res.status(400).json({
            success: false,
            error: "Price must be a positive number"
        });
    }

    const newProduct = {
        id: nextId++,
        name,
        price,
        category
    };

    products.push(newProduct);

    res.status(201).json({
        success: true,
        data: newProduct
    });
});
```

**Key points:**
- Status `201` (Created) is returned on success, not `200`.
- The server generates the `id`, not the client.
- Validation ensures required fields are present before creating.

### 2.5 PUT: Update an Item

Replace an existing product with new data.

```javascript
// PUT /api/products/:id - Update a product
app.put("/api/products/:id", (req, res) => {
    const id = parseInt(req.params.id);
    const product = products.find(p => p.id === id);

    if (!product) {
        return res.status(404).json({
            success: false,
            error: `Product with ID ${id} not found`
        });
    }

    const { name, price, category } = req.body;

    if (!name || !price || !category) {
        return res.status(400).json({
            success: false,
            error: "Please provide name, price, and category"
        });
    }

    // Update the product
    product.name = name;
    product.price = price;
    product.category = category;

    res.status(200).json({
        success: true,
        data: product
    });
});
```

### 2.6 DELETE: Remove an Item

Remove a product from the collection.

```javascript
// DELETE /api/products/:id - Delete a product
app.delete("/api/products/:id", (req, res) => {
    const id = parseInt(req.params.id);
    const index = products.findIndex(p => p.id === id);

    if (index === -1) {
        return res.status(404).json({
            success: false,
            error: `Product with ID ${id} not found`
        });
    }

    products.splice(index, 1);

    res.status(204).send(); // No content to return
});
```

**Why `204` and not `200`?** Status `204 No Content` indicates success but tells the client there is no response body. Since the product has been deleted, there is nothing meaningful to return.

### 2.7 Complete CRUD Server Code

Here is the entire server in one file:

```javascript
const express = require("express");
const app = express();

app.use(express.json());

// ---------- DATA STORE ----------
let products = [
    { id: 1, name: "Laptop", price: 999, category: "Electronics" },
    { id: 2, name: "Running Shoes", price: 85, category: "Sports" },
    { id: 3, name: "Coffee Maker", price: 45, category: "Kitchen" }
];
let nextId = 4;

// ---------- CRUD ROUTES ----------

// READ all
app.get("/api/products", (req, res) => {
    res.status(200).json({ success: true, count: products.length, data: products });
});

// READ one
app.get("/api/products/:id", (req, res) => {
    const product = products.find(p => p.id === parseInt(req.params.id));
    if (!product) {
        return res.status(404).json({ success: false, error: "Product not found" });
    }
    res.status(200).json({ success: true, data: product });
});

// CREATE
app.post("/api/products", (req, res) => {
    const { name, price, category } = req.body;
    if (!name || !price || !category) {
        return res.status(400).json({ success: false, error: "All fields required" });
    }
    const newProduct = { id: nextId++, name, price, category };
    products.push(newProduct);
    res.status(201).json({ success: true, data: newProduct });
});

// UPDATE
app.put("/api/products/:id", (req, res) => {
    const product = products.find(p => p.id === parseInt(req.params.id));
    if (!product) {
        return res.status(404).json({ success: false, error: "Product not found" });
    }
    const { name, price, category } = req.body;
    if (!name || !price || !category) {
        return res.status(400).json({ success: false, error: "All fields required" });
    }
    product.name = name;
    product.price = price;
    product.category = category;
    res.status(200).json({ success: true, data: product });
});

// DELETE
app.delete("/api/products/:id", (req, res) => {
    const index = products.findIndex(p => p.id === parseInt(req.params.id));
    if (index === -1) {
        return res.status(404).json({ success: false, error: "Product not found" });
    }
    products.splice(index, 1);
    res.status(204).send();
});

// ---------- START ----------
app.listen(3000, () => console.log("Products API on http://localhost:3000"));
```

---

## 3. Request Validation with Joi

### 3.1 Why Validate?

Manual validation (checking each field with `if` statements) quickly becomes messy as your data grows. What if a product has 15 fields? You would need dozens of `if` statements.

```
Manual Validation:                    Joi Validation:
-------------------                   ----------------
if (!name) ...                        const schema = Joi.object({
if (name.length < 3) ...                 name: Joi.string().min(3).required(),
if (name.length > 100) ...               price: Joi.number().positive().required(),
if (!price) ...                          category: Joi.string().required()
if (typeof price !== "number") ...    });
if (price <= 0) ...
if (!category) ...                    const { error } = schema.validate(req.body);

7 lines of if statements              3 lines, same result, more readable
```

**Joi** is a powerful validation library that lets you define rules for your data using a clean, chainable syntax.

### 3.2 Installing and Using Joi

```bash
npm install joi
```

```javascript
const Joi = require("joi");

// Define a validation schema
const productSchema = Joi.object({
    name: Joi.string()
        .min(3)
        .max(100)
        .required()
        .messages({
            "string.min": "Product name must be at least 3 characters",
            "string.max": "Product name cannot exceed 100 characters",
            "any.required": "Product name is required"
        }),

    price: Joi.number()
        .positive()
        .precision(2)
        .required()
        .messages({
            "number.positive": "Price must be a positive number",
            "any.required": "Price is required"
        }),

    category: Joi.string()
        .valid("Electronics", "Sports", "Kitchen", "Clothing", "Books")
        .required()
        .messages({
            "any.only": "Category must be one of: Electronics, Sports, Kitchen, Clothing, Books",
            "any.required": "Category is required"
        })
});

// Using the schema in a route
app.post("/api/products", (req, res) => {
    const { error, value } = productSchema.validate(req.body, {
        abortEarly: false // Report ALL errors, not just the first one
    });

    if (error) {
        const messages = error.details.map(d => d.message);
        return res.status(400).json({
            success: false,
            errors: messages
        });
    }

    // Data is valid -- use "value" (it is the sanitized version)
    const newProduct = { id: nextId++, ...value };
    products.push(newProduct);
    res.status(201).json({ success: true, data: newProduct });
});
```

**Sample error response when sending invalid data:**
```json
{
    "success": false,
    "errors": [
        "Product name must be at least 3 characters",
        "Price must be a positive number",
        "Category must be one of: Electronics, Sports, Kitchen, Clothing, Books"
    ]
}
```

### 3.3 Common Joi Validators

| Validator                          | What It Does                                    |
|------------------------------------|-------------------------------------------------|
| `Joi.string()`                     | Must be a string                                |
| `.min(3)`                          | Minimum 3 characters                            |
| `.max(100)`                        | Maximum 100 characters                          |
| `.required()`                      | Field must be present                           |
| `.optional()`                      | Field is not required                           |
| `.email()`                         | Must be a valid email format                    |
| `Joi.number()`                     | Must be a number                                |
| `.positive()`                      | Must be greater than 0                          |
| `.integer()`                       | Must be a whole number                          |
| `.min(0).max(100)`                 | Must be between 0 and 100                       |
| `Joi.boolean()`                    | Must be true or false                           |
| `Joi.date()`                       | Must be a valid date                            |
| `Joi.array().items(Joi.string())`  | Must be an array of strings                     |
| `.valid("a", "b", "c")`           | Must be one of the listed values                |
| `.pattern(/^[a-zA-Z]+$/)`         | Must match the regular expression               |

### 3.4 Validation Middleware Pattern

Instead of putting validation logic inside every route, create a reusable validation middleware:

```javascript
// middleware/validate.js
function validate(schema) {
    return (req, res, next) => {
        const { error, value } = schema.validate(req.body, {
            abortEarly: false,
            stripUnknown: true // Remove fields not in schema
        });

        if (error) {
            const messages = error.details.map(d => d.message);
            return res.status(400).json({
                success: false,
                errors: messages
            });
        }

        req.body = value; // Replace body with validated + sanitized data
        next();
    };
}

module.exports = validate;
```

**Usage in routes:**

```javascript
const validate = require("./middleware/validate");
const { productSchema } = require("./schemas/product");

// Clean route -- validation is handled by middleware
app.post("/api/products", validate(productSchema), (req, res) => {
    const newProduct = { id: nextId++, ...req.body };
    products.push(newProduct);
    res.status(201).json({ success: true, data: newProduct });
});

app.put("/api/products/:id", validate(productSchema), (req, res) => {
    // req.body is guaranteed to be valid here
    // ... update logic
});
```

---

## 4. express-validator Alternative

`express-validator` is another popular validation library that uses a different syntax style. Instead of defining a schema object, you chain validation rules directly in the route definition.

```bash
npm install express-validator
```

```javascript
const { body, validationResult } = require("express-validator");

app.post("/api/products",
    // Validation rules as middleware
    body("name").isString().isLength({ min: 3 }).withMessage("Name must be at least 3 characters"),
    body("price").isFloat({ gt: 0 }).withMessage("Price must be a positive number"),
    body("category").isIn(["Electronics", "Sports", "Kitchen"]).withMessage("Invalid category"),

    // Route handler
    (req, res) => {
        const errors = validationResult(req);

        if (!errors.isEmpty()) {
            return res.status(400).json({
                success: false,
                errors: errors.array().map(e => e.msg)
            });
        }

        // Data is valid
        const newProduct = { id: nextId++, ...req.body };
        products.push(newProduct);
        res.status(201).json({ success: true, data: newProduct });
    }
);
```

**Joi vs express-validator:**

| Feature              | Joi                              | express-validator                 |
|----------------------|----------------------------------|-----------------------------------|
| Syntax style         | Schema object                    | Chained middleware                |
| Learning curve       | Moderate                         | Easier for simple cases           |
| Schema reusability   | Easy (export schema objects)     | Harder (validation in route file) |
| Custom error messages| Built-in `.messages()`           | `.withMessage()`                  |
| Recommendation       | Better for larger applications   | Good for smaller applications     |

---

## 5. Centralized Error Handling

### 5.1 Custom Error Class

Create a custom error class that carries a status code. This makes error handling consistent throughout your application.

```javascript
// utils/AppError.js
class AppError extends Error {
    constructor(message, statusCode) {
        super(message);
        this.statusCode = statusCode;
        this.isOperational = true; // Distinguish from programming bugs
    }
}

module.exports = AppError;
```

**Usage in routes:**

```javascript
const AppError = require("./utils/AppError");

app.get("/api/products/:id", (req, res, next) => {
    const product = products.find(p => p.id === parseInt(req.params.id));

    if (!product) {
        return next(new AppError("Product not found", 404));
    }

    res.json({ success: true, data: product });
});
```

### 5.2 Async Error Wrapper

When using `async/await` in route handlers, thrown errors do not automatically reach the error handler. This wrapper catches them for you.

```javascript
// utils/asyncHandler.js
function asyncHandler(fn) {
    return (req, res, next) => {
        Promise.resolve(fn(req, res, next)).catch(next);
    };
}

module.exports = asyncHandler;
```

**Usage:**

```javascript
const asyncHandler = require("./utils/asyncHandler");

// Without wrapper -- errors crash the server
app.get("/api/data", async (req, res) => {
    const data = await someAsyncOperation(); // If this fails, unhandled rejection
    res.json(data);
});

// With wrapper -- errors forwarded to error handler
app.get("/api/data", asyncHandler(async (req, res) => {
    const data = await someAsyncOperation(); // If this fails, error handler catches it
    res.json(data);
}));
```

### 5.3 Error Handler Middleware

```javascript
// middleware/errorHandler.js
function errorHandler(err, req, res, next) {
    const statusCode = err.statusCode || 500;
    const message = err.isOperational ? err.message : "Internal Server Error";

    console.error(`[${new Date().toISOString()}] ERROR ${statusCode}: ${err.message}`);

    if (process.env.NODE_ENV === "development") {
        console.error(err.stack);
    }

    res.status(statusCode).json({
        success: false,
        error: message,
        ...(process.env.NODE_ENV === "development" && { stack: err.stack })
    });
}

module.exports = errorHandler;
```

---

## 6. File Uploads with Multer

### 6.1 What is Multer?

Multer is a middleware for handling `multipart/form-data`, which is the encoding type used for file uploads. Regular body parsers like `express.json()` cannot handle file uploads -- Multer fills that gap.

```bash
npm install multer
```

### 6.2 Basic File Upload

```javascript
const express = require("express");
const multer = require("multer");
const path = require("path");

const app = express();

// Configure storage
const storage = multer.diskStorage({
    destination: (req, file, cb) => {
        cb(null, "uploads/"); // Save to "uploads" folder
    },
    filename: (req, file, cb) => {
        // Create unique filename: timestamp-originalname
        const uniqueName = `${Date.now()}-${file.originalname}`;
        cb(null, uniqueName);
    }
});

const upload = multer({ storage });

// Single file upload
app.post("/api/upload", upload.single("image"), (req, res) => {
    if (!req.file) {
        return res.status(400).json({ error: "No file uploaded" });
    }

    res.status(200).json({
        success: true,
        file: {
            filename: req.file.filename,
            originalname: req.file.originalname,
            size: req.file.size,
            mimetype: req.file.mimetype,
            path: req.file.path
        }
    });
});

// Multiple file upload (max 5 files)
app.post("/api/upload-multiple", upload.array("images", 5), (req, res) => {
    if (!req.files || req.files.length === 0) {
        return res.status(400).json({ error: "No files uploaded" });
    }

    const fileInfo = req.files.map(f => ({
        filename: f.filename,
        size: f.size
    }));

    res.status(200).json({ success: true, count: req.files.length, files: fileInfo });
});

app.listen(3000);
```

**File upload flow:**

```
Client (Postman / Form)                       Server (Express + Multer)
+---------------------+                       +------------------------+
|                     |   POST /api/upload     |                        |
|  Form with file     | --------------------> |  Multer parses the     |
|  input:             |   Content-Type:        |  multipart data        |
|                     |   multipart/form-data  |                        |
|  [Choose File]      |                        |  Saves file to         |
|  photo.jpg (2MB)    |                        |  uploads/1718...-      |
|                     |                        |  photo.jpg             |
|                     |   { success: true,     |                        |
|                     | <-------------------- |  req.file contains     |
|                     |     file: { ... } }    |  file metadata         |
+---------------------+                       +------------------------+
```

### 6.3 File Filtering and Limits

```javascript
const upload = multer({
    storage,
    limits: {
        fileSize: 5 * 1024 * 1024 // 5 MB max file size
    },
    fileFilter: (req, file, cb) => {
        // Only allow image files
        const allowedTypes = ["image/jpeg", "image/png", "image/gif", "image/webp"];

        if (allowedTypes.includes(file.mimetype)) {
            cb(null, true);  // Accept the file
        } else {
            cb(new Error("Only image files (JPEG, PNG, GIF, WebP) are allowed"), false);
        }
    }
});
```

---

## 7. API Testing with Postman / Thunder Client

### 7.1 Why Use API Testing Tools?

When building a backend API, there is no user interface to interact with. You cannot simply open a browser and click buttons to test your endpoints. API testing tools let you:

- Send any type of HTTP request (GET, POST, PUT, DELETE)
- Include request bodies, headers, and authentication tokens
- See the response status code, headers, and body
- Save and organize collections of requests

**Postman** is a standalone application. **Thunder Client** is a VS Code extension that does the same thing without leaving your editor.

### 7.2 Testing Each CRUD Operation

```
+----------------------------------------------------------------+
|  TESTING CRUD OPERATIONS                                        |
+----------------------------------------------------------------+
|                                                                  |
|  1. GET All Products                                             |
|     Method: GET                                                  |
|     URL:    http://localhost:3000/api/products                    |
|     Body:   (none)                                               |
|     Expect: 200 OK + array of products                           |
|                                                                  |
|  2. GET One Product                                              |
|     Method: GET                                                  |
|     URL:    http://localhost:3000/api/products/1                  |
|     Body:   (none)                                               |
|     Expect: 200 OK + single product object                       |
|                                                                  |
|  3. CREATE Product                                               |
|     Method: POST                                                 |
|     URL:    http://localhost:3000/api/products                    |
|     Headers: Content-Type: application/json                      |
|     Body:   { "name": "Headphones", "price": 59,                 |
|               "category": "Electronics" }                        |
|     Expect: 201 Created + new product with ID                    |
|                                                                  |
|  4. UPDATE Product                                               |
|     Method: PUT                                                  |
|     URL:    http://localhost:3000/api/products/1                  |
|     Headers: Content-Type: application/json                      |
|     Body:   { "name": "Gaming Laptop", "price": 1299,            |
|               "category": "Electronics" }                        |
|     Expect: 200 OK + updated product                             |
|                                                                  |
|  5. DELETE Product                                               |
|     Method: DELETE                                               |
|     URL:    http://localhost:3000/api/products/1                  |
|     Body:   (none)                                               |
|     Expect: 204 No Content                                       |
|                                                                  |
|  6. GET Non-existent Product                                     |
|     Method: GET                                                  |
|     URL:    http://localhost:3000/api/products/999                |
|     Expect: 404 Not Found + error message                        |
|                                                                  |
+----------------------------------------------------------------+
```

---

## 8. The MVC Pattern

### 8.1 What is MVC?

MVC (Model-View-Controller) is an architectural pattern that separates your application into three distinct layers:

```
+----------------------------------------------------------------+
|                        MVC PATTERN                              |
+----------------------------------------------------------------+
|                                                                  |
|  +----------+     +--------------+     +-----------+             |
|  |  MODEL   |     |  CONTROLLER  |     |   VIEW    |             |
|  |          |     |              |     |           |             |
|  |  Data &  |<--->|  Business    |<--->|  What the |             |
|  |  Database|     |  Logic       |     |  user sees|             |
|  |  Rules   |     |  (Routes)    |     |  (JSON /  |             |
|  |          |     |              |     |   HTML)   |             |
|  +----------+     +--------------+     +-----------+             |
|                                                                  |
|  Example:                                                        |
|  Model = Product data structure and database queries             |
|  Controller = Route handlers (get products, create product)      |
|  View = JSON responses (in APIs) or HTML templates               |
|                                                                  |
+----------------------------------------------------------------+
```

**Why use MVC?**
- **Separation of concerns** -- Each file has one job.
- **Easier to maintain** -- Finding and fixing bugs is faster when code is organized.
- **Easier to test** -- You can test controllers without touching the database.
- **Team collaboration** -- Different developers can work on different layers.

### 8.2 MVC Folder Structure

```
products-api/
    server.js                    <-- Entry point: starts the server
    package.json
    |
    +-- config/
    |       db.js                <-- Database connection (later weeks)
    |
    +-- models/
    |       productModel.js      <-- Data structure and data operations
    |
    +-- controllers/
    |       productController.js <-- Route handler functions
    |
    +-- routes/
    |       productRoutes.js     <-- Route definitions
    |
    +-- middleware/
    |       errorHandler.js      <-- Error handling middleware
    |       validate.js          <-- Validation middleware
    |       auth.js              <-- Authentication middleware
    |
    +-- schemas/
    |       productSchema.js     <-- Joi validation schemas
    |
    +-- utils/
    |       AppError.js          <-- Custom error class
    |       asyncHandler.js      <-- Async wrapper
    |
    +-- uploads/                 <-- Uploaded files directory
```

### 8.3 Implementing MVC

**Step 1: Model** -- Define the data and data operations.

```javascript
// models/productModel.js
let products = [
    { id: 1, name: "Laptop", price: 999, category: "Electronics" },
    { id: 2, name: "Running Shoes", price: 85, category: "Sports" },
    { id: 3, name: "Coffee Maker", price: 45, category: "Kitchen" }
];
let nextId = 4;

// Data access functions
const findAll = () => products;
const findById = (id) => products.find(p => p.id === id);
const create = (data) => {
    const product = { id: nextId++, ...data };
    products.push(product);
    return product;
};
const update = (id, data) => {
    const product = findById(id);
    if (!product) return null;
    Object.assign(product, data);
    return product;
};
const remove = (id) => {
    const index = products.findIndex(p => p.id === id);
    if (index === -1) return false;
    products.splice(index, 1);
    return true;
};

module.exports = { findAll, findById, create, update, remove };
```

**Step 2: Controller** -- Handle request logic.

```javascript
// controllers/productController.js
const Product = require("../models/productModel");
const AppError = require("../utils/AppError");

exports.getAllProducts = (req, res) => {
    const products = Product.findAll();
    res.status(200).json({ success: true, count: products.length, data: products });
};

exports.getProduct = (req, res, next) => {
    const product = Product.findById(parseInt(req.params.id));
    if (!product) {
        return next(new AppError("Product not found", 404));
    }
    res.status(200).json({ success: true, data: product });
};

exports.createProduct = (req, res) => {
    const product = Product.create(req.body);
    res.status(201).json({ success: true, data: product });
};

exports.updateProduct = (req, res, next) => {
    const product = Product.update(parseInt(req.params.id), req.body);
    if (!product) {
        return next(new AppError("Product not found", 404));
    }
    res.status(200).json({ success: true, data: product });
};

exports.deleteProduct = (req, res, next) => {
    const deleted = Product.remove(parseInt(req.params.id));
    if (!deleted) {
        return next(new AppError("Product not found", 404));
    }
    res.status(204).send();
};
```

**Step 3: Routes** -- Define URL-to-controller mappings.

```javascript
// routes/productRoutes.js
const express = require("express");
const router = express.Router();
const productController = require("../controllers/productController");
const validate = require("../middleware/validate");
const { productSchema } = require("../schemas/productSchema");

router.get("/",     productController.getAllProducts);
router.get("/:id",  productController.getProduct);
router.post("/",    validate(productSchema), productController.createProduct);
router.put("/:id",  validate(productSchema), productController.updateProduct);
router.delete("/:id", productController.deleteProduct);

module.exports = router;
```

**Step 4: Server** -- Wire everything together.

```javascript
// server.js
const express = require("express");
const productRoutes = require("./routes/productRoutes");
const errorHandler = require("./middleware/errorHandler");

const app = express();

app.use(express.json());

// Mount routes
app.use("/api/products", productRoutes);

// Error handler (must be last)
app.use(errorHandler);

const PORT = process.env.PORT || 3000;
app.listen(PORT, () => console.log(`Server running on port ${PORT}`));
```

**Data flow through MVC:**

```
Request: GET /api/products/5

  server.js              routes/                controllers/            models/
  ---------              -------                ------------            -------
  app.use(               router.get(            getProduct(req,res) {   findById(5) {
    "/api/products",       "/:id",                const product =        return products
    productRoutes          productController       Product.findById(5);    .find(p =>
  );                       .getProduct            res.json(product);       p.id === 5);
                         );                     }                       }

  Entry Point  --->  Route Matching  --->  Business Logic  --->  Data Access
```

---

## 9. Summary

| Topic                     | Key Takeaway                                                              |
|---------------------------|---------------------------------------------------------------------------|
| **CRUD**                  | Create, Read, Update, Delete -- the four fundamental data operations      |
| **CRUD + HTTP**           | POST = Create, GET = Read, PUT = Update, DELETE = Delete                  |
| **In-memory CRUD**        | Use arrays and `find`/`findIndex`/`splice`/`push` for data operations     |
| **Joi Validation**        | Define schema objects with rules; validate `req.body` before processing   |
| **express-validator**     | Chain validation rules directly in route definitions                      |
| **Centralized Errors**    | Custom `AppError` class + `asyncHandler` + error handler middleware        |
| **Multer**                | Middleware for handling file uploads (single and multiple files)           |
| **API Testing**           | Use Postman or Thunder Client to test endpoints without a frontend        |
| **MVC Pattern**           | Separate code into Models, Controllers, and Routes for maintainability    |

---

*Next week, we will add authentication and security to our API -- password hashing, JWT tokens, and protected routes.*
