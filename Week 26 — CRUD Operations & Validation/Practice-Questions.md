# Week 26: CRUD Operations & Validation - Practice Questions

**Total Questions: 20**

| Section | Topic                    | Questions |
|---------|--------------------------|-----------|
| A       | Multiple Choice Questions| 10        |
| B       | Short Answer Questions   | 5         |
| C       | Coding Exercises         | 5         |

---

## Section A: Multiple Choice Questions (10)

**Q1.** What does CRUD stand for?

- A) Connect, Read, Update, Deploy
- B) Create, Read, Update, Delete
- C) Create, Render, Upload, Download
- D) Connect, Retrieve, Update, Delete

<details>
<summary>Answer</summary>

**B) Create, Read, Update, Delete**

CRUD represents the four fundamental operations performed on data in any application. Create adds new data, Read retrieves existing data, Update modifies existing data, and Delete removes data.
</details>

---

**Q2.** Which HTTP status code should be returned when a new resource is successfully created?

- A) `200 OK`
- B) `201 Created`
- C) `204 No Content`
- D) `202 Accepted`

<details>
<summary>Answer</summary>

**B) `201 Created`**

Status code `201` specifically indicates that a new resource has been successfully created as a result of a `POST` request. It is more semantically correct than `200`, which is a generic success code.
</details>

---

**Q3.** What is the correct HTTP status code to return after a successful `DELETE` operation when there is no content to send back?

- A) `200 OK`
- B) `201 Created`
- C) `204 No Content`
- D) `404 Not Found`

<details>
<summary>Answer</summary>

**C) `204 No Content`**

Status code `204` means the server successfully processed the request but has no content to return in the response body. This is the standard response for a `DELETE` operation because the resource has been removed and there is nothing meaningful to send back.
</details>

---

**Q4.** In Joi validation, what does `abortEarly: false` do?

- A) Stops validation immediately on the first error
- B) Returns all validation errors instead of stopping at the first one
- C) Skips validation entirely
- D) Makes all fields optional

<details>
<summary>Answer</summary>

**B) Returns all validation errors instead of stopping at the first one**

By default, Joi stops validation at the first error it encounters (`abortEarly: true`). Setting `abortEarly: false` tells Joi to continue validating all fields and return every error found. This gives users a complete list of what needs to be fixed.
</details>

---

**Q5.** Which array method is best for finding the index of an element to delete from an in-memory array?

- A) `Array.find()`
- B) `Array.indexOf()`
- C) `Array.findIndex()`
- D) `Array.filter()`

<details>
<summary>Answer</summary>

**C) `Array.findIndex()`**

`findIndex()` accepts a callback function and returns the index of the first element that matches the condition. This is ideal for finding objects in an array by a property (like `id`). `indexOf()` only works with primitive values (strings, numbers) and cannot search by object properties. After getting the index, you can use `splice()` to remove the element.

```javascript
const index = products.findIndex(p => p.id === parseInt(req.params.id));
if (index !== -1) {
    products.splice(index, 1); // Remove 1 element at that index
}
```
</details>

---

**Q6.** What does Multer do in an Express application?

- A) Validates JSON request bodies
- B) Handles file uploads from multipart form data
- C) Compresses response data
- D) Encrypts request data

<details>
<summary>Answer</summary>

**B) Handles file uploads from multipart form data**

Multer is a middleware specifically designed to handle `multipart/form-data`, which is the encoding type used when uploading files through HTML forms. Standard body parsers like `express.json()` cannot process file uploads -- Multer fills this gap by parsing the file data and making it available on `req.file` (single file) or `req.files` (multiple files).
</details>

---

**Q7.** In the MVC pattern, what is the role of the Controller?

- A) Define the database schema and data operations
- B) Render the user interface
- C) Handle business logic and coordinate between Model and View
- D) Configure the server and middleware

<details>
<summary>Answer</summary>

**C) Handle business logic and coordinate between Model and View**

The Controller receives incoming requests, processes them using business logic, interacts with the Model to read or write data, and sends the appropriate response (View). It acts as the middleman between the data layer (Model) and the presentation layer (View/Response).
</details>

---

**Q8.** What does the `stripUnknown: true` option do in Joi validation?

- A) Removes all fields from the request body
- B) Removes fields that are not defined in the validation schema
- C) Throws an error for unknown fields
- D) Converts all values to strings

<details>
<summary>Answer</summary>

**B) Removes fields that are not defined in the validation schema**

When `stripUnknown: true` is set, Joi automatically removes any fields from the input that are not defined in the schema. This is a security measure that prevents clients from sending unexpected or malicious fields that your application does not expect.
</details>

---

**Q9.** What is the purpose of the `asyncHandler` wrapper function used with Express route handlers?

- A) It makes synchronous code run asynchronously
- B) It catches errors from async/await functions and passes them to the error handler
- C) It speeds up request processing
- D) It adds timeout functionality to routes

<details>
<summary>Answer</summary>

**B) It catches errors from async/await functions and passes them to the error handler**

When using `async/await` in Express route handlers, thrown errors or rejected promises are not automatically caught by Express. They result in unhandled promise rejections that crash the server. The `asyncHandler` wraps the async function in a `try/catch` (via `Promise.resolve().catch(next)`) and forwards any errors to the centralized error handling middleware.

```javascript
function asyncHandler(fn) {
    return (req, res, next) => {
        Promise.resolve(fn(req, res, next)).catch(next);
    };
}
```
</details>

---

**Q10.** Which Joi method would you use to validate that a field must be one of a specific set of values?

- A) `.pattern()`
- B) `.valid()`
- C) `.allow()`
- D) `.enum()`

<details>
<summary>Answer</summary>

**B) `.valid()`**

The `.valid()` method restricts the field to one of the specified values. For example, `Joi.string().valid("Electronics", "Sports", "Kitchen")` ensures the value must be exactly one of those three strings. `.allow()` permits additional values without restricting, and `.pattern()` validates against a regular expression.
</details>

---

## Section B: Short Answer Questions (5)

**Q11.** Explain the difference between using `Array.find()` and `Array.findIndex()` when working with CRUD operations on an in-memory array. When would you use each?

<details>
<summary>Answer</summary>

**`Array.find()`** returns the **actual element** (object) that matches the condition, or `undefined` if no match is found. Use it when you need to access or modify the object's properties.

**`Array.findIndex()`** returns the **index** (position number) of the matching element, or `-1` if no match is found. Use it when you need to remove the element from the array using `splice()`.

```javascript
// READ or UPDATE -- need the object itself
const product = products.find(p => p.id === 5);
if (product) {
    product.name = "Updated Name"; // Modify directly
}

// DELETE -- need the index for splice
const index = products.findIndex(p => p.id === 5);
if (index !== -1) {
    products.splice(index, 1); // Remove from array
}
```

Use `find()` for GET and PUT operations (where you need the object), and `findIndex()` for DELETE operations (where you need to remove it by position).
</details>

---

**Q12.** Why is it important to validate incoming request data, and what are the risks of skipping validation?

<details>
<summary>Answer</summary>

Validation ensures that the data received from clients is correct, complete, and safe before it is processed or stored. Skipping validation introduces several risks:

1. **Data corruption:** Invalid data types (sending a string where a number is expected) can corrupt your database and cause application errors downstream.

2. **Security vulnerabilities:** Without validation, attackers can inject malicious data such as SQL injection strings, XSS scripts, or excessively large payloads that crash the server.

3. **Application crashes:** If code expects a specific data structure (like accessing `req.body.name.trim()`) and the field is missing or null, the application will throw a runtime error.

4. **Inconsistent data:** Without rules like minimum length or valid formats, the database fills with inconsistent entries (empty strings, negative prices, invalid emails).

5. **Poor user experience:** Without clear error messages about what is wrong with their input, users have no way to correct their submissions.

Validation should be performed on the server side even if the frontend has its own validation, because API endpoints can be accessed directly using tools like Postman, curl, or malicious scripts that bypass the frontend entirely.
</details>

---

**Q13.** What is the purpose of a custom `AppError` class, and how does it differ from the built-in `Error` class?

<details>
<summary>Answer</summary>

A custom `AppError` class extends the built-in `Error` class with additional properties that are useful for API error handling:

```javascript
class AppError extends Error {
    constructor(message, statusCode) {
        super(message);
        this.statusCode = statusCode;
        this.isOperational = true;
    }
}
```

**Key differences from the built-in `Error`:**

1. **`statusCode` property:** The built-in `Error` only has `message` and `stack`. `AppError` adds a `statusCode` so the error handler knows which HTTP status to send (404, 400, 403, etc.).

2. **`isOperational` property:** This flag distinguishes between expected errors (user not found, invalid input) and unexpected programming bugs (null reference, syntax errors). The error handler can use this to decide whether to show the error message to the client or display a generic "Internal Server Error."

3. **Consistency:** Every error thrown throughout the application follows the same structure, making the centralized error handler simpler and more predictable.
</details>

---

**Q14.** Explain the MVC folder structure and the responsibility of each layer in a REST API application.

<details>
<summary>Answer</summary>

The MVC (Model-View-Controller) pattern separates an application into three layers, each in its own folder:

**Models (`models/`):**
Responsible for data structure and data operations. In an in-memory application, models contain the data array and functions like `findAll()`, `findById()`, `create()`, `update()`, and `remove()`. When a database is added, models define the schema and query logic.

**Controllers (`controllers/`):**
Responsible for request handling and business logic. Controllers receive the parsed request from the route, call the appropriate model functions to read or write data, and send back the response. They act as the bridge between the incoming HTTP request and the data layer.

**Routes (`routes/`):**
Responsible for mapping URLs to controller functions. Routes define which HTTP method and URL pattern triggers which controller function. They may also attach middleware like validation.

**Additional supporting folders:**
- `middleware/` -- Reusable middleware functions (auth, validation, error handler)
- `utils/` -- Helper utilities (AppError, asyncHandler)
- `schemas/` -- Joi validation schema definitions
- `config/` -- Configuration files (database connection, environment variables)

This separation ensures each file has a single responsibility, making the codebase easier to navigate, maintain, and test.
</details>

---

**Q15.** When using Multer for file uploads, what is the difference between `upload.single()` and `upload.array()`? Provide a use case for each.

<details>
<summary>Answer</summary>

**`upload.single("fieldName")`** accepts exactly one file from the specified form field. The uploaded file is available on `req.file`.

**Use case:** Uploading a user profile picture.
```javascript
app.post("/api/users/avatar", upload.single("avatar"), (req, res) => {
    // req.file contains the single uploaded file
    res.json({ avatar: req.file.filename });
});
```

**`upload.array("fieldName", maxCount)`** accepts multiple files (up to `maxCount`) from the specified form field. The uploaded files are available on `req.files` as an array.

**Use case:** Uploading multiple product images for an e-commerce listing.
```javascript
app.post("/api/products/images", upload.array("images", 5), (req, res) => {
    // req.files is an array of up to 5 uploaded files
    const filenames = req.files.map(f => f.filename);
    res.json({ images: filenames });
});
```

There is also `upload.fields()` which accepts files from multiple named fields:
```javascript
upload.fields([
    { name: "avatar", maxCount: 1 },
    { name: "gallery", maxCount: 5 }
])
// req.files.avatar[0] and req.files.gallery[]
```
</details>

---

## Section C: Coding Exercises (5)

**Q16.** Build a complete CRUD API for a `products` resource using an in-memory array. Each product should have `id`, `name`, `price`, and `category`. Include all five CRUD operations (GET all, GET one, POST, PUT, DELETE) with proper status codes and error handling for not-found cases.

<details>
<summary>Answer</summary>

```javascript
const express = require("express");
const app = express();

app.use(express.json());

// In-memory data store
let products = [
    { id: 1, name: "Wireless Mouse", price: 29.99, category: "Electronics" },
    { id: 2, name: "Yoga Mat", price: 24.99, category: "Sports" },
    { id: 3, name: "Blender", price: 49.99, category: "Kitchen" }
];
let nextId = 4;

// GET all products
app.get("/api/products", (req, res) => {
    res.status(200).json({
        success: true,
        count: products.length,
        data: products
    });
});

// GET single product
app.get("/api/products/:id", (req, res) => {
    const product = products.find(p => p.id === parseInt(req.params.id));

    if (!product) {
        return res.status(404).json({
            success: false,
            error: `Product with ID ${req.params.id} not found`
        });
    }

    res.status(200).json({ success: true, data: product });
});

// POST create product
app.post("/api/products", (req, res) => {
    const { name, price, category } = req.body;

    if (!name || price === undefined || !category) {
        return res.status(400).json({
            success: false,
            error: "Name, price, and category are required"
        });
    }

    if (typeof price !== "number" || price <= 0) {
        return res.status(400).json({
            success: false,
            error: "Price must be a positive number"
        });
    }

    const newProduct = { id: nextId++, name, price, category };
    products.push(newProduct);

    res.status(201).json({ success: true, data: newProduct });
});

// PUT update product
app.put("/api/products/:id", (req, res) => {
    const product = products.find(p => p.id === parseInt(req.params.id));

    if (!product) {
        return res.status(404).json({
            success: false,
            error: `Product with ID ${req.params.id} not found`
        });
    }

    const { name, price, category } = req.body;

    if (!name || price === undefined || !category) {
        return res.status(400).json({
            success: false,
            error: "Name, price, and category are required"
        });
    }

    product.name = name;
    product.price = price;
    product.category = category;

    res.status(200).json({ success: true, data: product });
});

// DELETE product
app.delete("/api/products/:id", (req, res) => {
    const index = products.findIndex(p => p.id === parseInt(req.params.id));

    if (index === -1) {
        return res.status(404).json({
            success: false,
            error: `Product with ID ${req.params.id} not found`
        });
    }

    products.splice(index, 1);
    res.status(204).send();
});

app.listen(3000, () => {
    console.log("Products API running on http://localhost:3000");
});
```
</details>

---

**Q17.** Add Joi validation to the products API from Q16. Create a Joi schema that validates: `name` (string, 3-100 chars, required), `price` (positive number, required), `category` (must be one of "Electronics", "Sports", "Kitchen", "Clothing", "Books", required). Create a reusable validation middleware function and apply it to POST and PUT routes.

<details>
<summary>Answer</summary>

```javascript
const express = require("express");
const Joi = require("joi");

const app = express();
app.use(express.json());

// ---------- JOI SCHEMA ----------

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

// ---------- VALIDATION MIDDLEWARE ----------

function validate(schema) {
    return (req, res, next) => {
        const { error, value } = schema.validate(req.body, {
            abortEarly: false,
            stripUnknown: true
        });

        if (error) {
            const messages = error.details.map(detail => detail.message);
            return res.status(400).json({
                success: false,
                errors: messages
            });
        }

        req.body = value; // Use sanitized data
        next();
    };
}

// ---------- DATA STORE ----------

let products = [
    { id: 1, name: "Wireless Mouse", price: 29.99, category: "Electronics" },
    { id: 2, name: "Yoga Mat", price: 24.99, category: "Sports" }
];
let nextId = 3;

// ---------- ROUTES ----------

app.get("/api/products", (req, res) => {
    res.status(200).json({ success: true, count: products.length, data: products });
});

app.get("/api/products/:id", (req, res) => {
    const product = products.find(p => p.id === parseInt(req.params.id));
    if (!product) {
        return res.status(404).json({ success: false, error: "Product not found" });
    }
    res.status(200).json({ success: true, data: product });
});

// POST with Joi validation middleware
app.post("/api/products", validate(productSchema), (req, res) => {
    const newProduct = { id: nextId++, ...req.body };
    products.push(newProduct);
    res.status(201).json({ success: true, data: newProduct });
});

// PUT with Joi validation middleware
app.put("/api/products/:id", validate(productSchema), (req, res) => {
    const product = products.find(p => p.id === parseInt(req.params.id));
    if (!product) {
        return res.status(404).json({ success: false, error: "Product not found" });
    }
    Object.assign(product, req.body);
    res.status(200).json({ success: true, data: product });
});

app.delete("/api/products/:id", (req, res) => {
    const index = products.findIndex(p => p.id === parseInt(req.params.id));
    if (index === -1) {
        return res.status(404).json({ success: false, error: "Product not found" });
    }
    products.splice(index, 1);
    res.status(204).send();
});

app.listen(3000, () => console.log("Server running on port 3000"));
```

**Test with invalid data:**
```json
// POST /api/products with body:
{ "name": "AB", "price": -5, "category": "Food" }

// Response (400):
{
    "success": false,
    "errors": [
        "Product name must be at least 3 characters",
        "Price must be a positive number",
        "Category must be one of: Electronics, Sports, Kitchen, Clothing, Books"
    ]
}
```
</details>

---

**Q18.** Create a file upload endpoint using Multer that accepts a single image file. Configure it to: save files to an `uploads/` directory with unique filenames, only allow JPEG and PNG files, limit file size to 2 MB, and return the file details in the response.

<details>
<summary>Answer</summary>

```javascript
const express = require("express");
const multer = require("multer");
const path = require("path");
const fs = require("fs");

const app = express();

// Ensure uploads directory exists
const uploadsDir = path.join(__dirname, "uploads");
if (!fs.existsSync(uploadsDir)) {
    fs.mkdirSync(uploadsDir);
}

// Configure Multer storage
const storage = multer.diskStorage({
    destination: (req, file, cb) => {
        cb(null, "uploads/");
    },
    filename: (req, file, cb) => {
        const ext = path.extname(file.originalname);
        const uniqueName = `${Date.now()}-${Math.round(Math.random() * 1000)}${ext}`;
        cb(null, uniqueName);
    }
});

// Configure Multer with file filter and size limit
const upload = multer({
    storage,
    limits: {
        fileSize: 2 * 1024 * 1024 // 2 MB
    },
    fileFilter: (req, file, cb) => {
        const allowedTypes = ["image/jpeg", "image/png"];

        if (allowedTypes.includes(file.mimetype)) {
            cb(null, true);
        } else {
            cb(new Error("Only JPEG and PNG images are allowed"), false);
        }
    }
});

// Upload endpoint
app.post("/api/upload", (req, res) => {
    // Use upload.single as middleware, handle errors manually
    upload.single("image")(req, res, (err) => {
        if (err instanceof multer.MulterError) {
            // Multer-specific errors (file too large, etc.)
            if (err.code === "LIMIT_FILE_SIZE") {
                return res.status(400).json({
                    success: false,
                    error: "File size exceeds 2 MB limit"
                });
            }
            return res.status(400).json({ success: false, error: err.message });
        }

        if (err) {
            // Custom errors (wrong file type)
            return res.status(400).json({ success: false, error: err.message });
        }

        if (!req.file) {
            return res.status(400).json({
                success: false,
                error: "No file uploaded. Use field name 'image'"
            });
        }

        res.status(200).json({
            success: true,
            file: {
                filename: req.file.filename,
                originalName: req.file.originalname,
                mimeType: req.file.mimetype,
                size: `${(req.file.size / 1024).toFixed(2)} KB`,
                path: req.file.path
            }
        });
    });
});

app.listen(3000, () => {
    console.log("Upload server running on http://localhost:3000");
});
```

**Testing in Postman / Thunder Client:**
1. Method: `POST`
2. URL: `http://localhost:3000/api/upload`
3. Body tab: select "Form" or "Multipart"
4. Add field: key = `image`, type = File, value = select a JPEG or PNG file
5. Send

**Success response:**
```json
{
    "success": true,
    "file": {
        "filename": "1718456789-342.jpg",
        "originalName": "my-photo.jpg",
        "mimeType": "image/jpeg",
        "size": "156.78 KB",
        "path": "uploads/1718456789-342.jpg"
    }
}
```
</details>

---

**Q19.** Write a centralized error handling system that includes: a custom `AppError` class with `statusCode` and `isOperational` properties, an `asyncHandler` wrapper, and an error handler middleware. Demonstrate it working with a route that throws a 404 error.

<details>
<summary>Answer</summary>

```javascript
const express = require("express");
const app = express();

app.use(express.json());

// ---------- CUSTOM ERROR CLASS ----------

class AppError extends Error {
    constructor(message, statusCode) {
        super(message);
        this.statusCode = statusCode;
        this.isOperational = true;

        // Capture stack trace, excluding the constructor call
        Error.captureStackTrace(this, this.constructor);
    }
}

// ---------- ASYNC HANDLER ----------

function asyncHandler(fn) {
    return (req, res, next) => {
        Promise.resolve(fn(req, res, next)).catch(next);
    };
}

// ---------- DATA ----------

const users = [
    { id: 1, name: "Fahad", email: "fahad@example.com" },
    { id: 2, name: "Ahmed", email: "ahmed@example.com" }
];

// ---------- ROUTES ----------

// Successful route
app.get("/api/users", (req, res) => {
    res.status(200).json({ success: true, data: users });
});

// Route that throws AppError (404)
app.get("/api/users/:id", (req, res, next) => {
    const user = users.find(u => u.id === parseInt(req.params.id));

    if (!user) {
        return next(new AppError(`User with ID ${req.params.id} not found`, 404));
    }

    res.status(200).json({ success: true, data: user });
});

// Async route that might throw
app.get("/api/data", asyncHandler(async (req, res) => {
    // Simulate an async operation that fails
    const result = await new Promise((resolve, reject) => {
        reject(new AppError("Failed to fetch external data", 503));
    });

    res.json(result);
}));

// Route with validation error
app.post("/api/users", (req, res, next) => {
    const { name, email } = req.body;

    if (!name || !email) {
        return next(new AppError("Name and email are required", 400));
    }

    const newUser = { id: users.length + 1, name, email };
    users.push(newUser);
    res.status(201).json({ success: true, data: newUser });
});

// ---------- ERROR HANDLER MIDDLEWARE (must be last) ----------

app.use((err, req, res, next) => {
    const statusCode = err.statusCode || 500;
    const message = err.isOperational
        ? err.message
        : "An unexpected error occurred";

    // Log error details to console
    console.error(`[${new Date().toISOString()}] ${statusCode} - ${err.message}`);

    // Send error response
    res.status(statusCode).json({
        success: false,
        error: message,
        ...(process.env.NODE_ENV === "development" && {
            stack: err.stack
        })
    });
});

app.listen(3000, () => {
    console.log("Server running on http://localhost:3000");
});
```

**Test results:**
- `GET /api/users/999` returns `{ success: false, error: "User with ID 999 not found" }` with status 404
- `GET /api/data` returns `{ success: false, error: "Failed to fetch external data" }` with status 503
- `POST /api/users` with empty body returns `{ success: false, error: "Name and email are required" }` with status 400
</details>

---

**Q20.** Organize the products CRUD API using the MVC pattern. Create separate files for: `models/productModel.js` (data and data access functions), `controllers/productController.js` (request handlers), `routes/productRoutes.js` (URL definitions), and `server.js` (entry point). Show the complete code for each file.

<details>
<summary>Answer</summary>

**models/productModel.js:**

```javascript
// Data store (will be replaced with a database later)
let products = [
    { id: 1, name: "Laptop", price: 999, category: "Electronics" },
    { id: 2, name: "Running Shoes", price: 85, category: "Sports" },
    { id: 3, name: "Coffee Maker", price: 45, category: "Kitchen" }
];
let nextId = 4;

// Data access functions
exports.findAll = () => products;

exports.findById = (id) => {
    return products.find(p => p.id === id);
};

exports.create = (data) => {
    const product = { id: nextId++, ...data };
    products.push(product);
    return product;
};

exports.update = (id, data) => {
    const product = products.find(p => p.id === id);
    if (!product) return null;
    Object.assign(product, data);
    return product;
};

exports.remove = (id) => {
    const index = products.findIndex(p => p.id === id);
    if (index === -1) return false;
    products.splice(index, 1);
    return true;
};
```

**controllers/productController.js:**

```javascript
const Product = require("../models/productModel");

// GET /api/products
exports.getAllProducts = (req, res) => {
    const products = Product.findAll();
    res.status(200).json({
        success: true,
        count: products.length,
        data: products
    });
};

// GET /api/products/:id
exports.getProduct = (req, res) => {
    const product = Product.findById(parseInt(req.params.id));

    if (!product) {
        return res.status(404).json({
            success: false,
            error: "Product not found"
        });
    }

    res.status(200).json({ success: true, data: product });
};

// POST /api/products
exports.createProduct = (req, res) => {
    const { name, price, category } = req.body;

    if (!name || !price || !category) {
        return res.status(400).json({
            success: false,
            error: "Name, price, and category are required"
        });
    }

    const product = Product.create({ name, price, category });
    res.status(201).json({ success: true, data: product });
};

// PUT /api/products/:id
exports.updateProduct = (req, res) => {
    const { name, price, category } = req.body;

    if (!name || !price || !category) {
        return res.status(400).json({
            success: false,
            error: "Name, price, and category are required"
        });
    }

    const product = Product.update(parseInt(req.params.id), { name, price, category });

    if (!product) {
        return res.status(404).json({
            success: false,
            error: "Product not found"
        });
    }

    res.status(200).json({ success: true, data: product });
};

// DELETE /api/products/:id
exports.deleteProduct = (req, res) => {
    const deleted = Product.remove(parseInt(req.params.id));

    if (!deleted) {
        return res.status(404).json({
            success: false,
            error: "Product not found"
        });
    }

    res.status(204).send();
};
```

**routes/productRoutes.js:**

```javascript
const express = require("express");
const router = express.Router();
const productController = require("../controllers/productController");

router.get("/",       productController.getAllProducts);
router.get("/:id",    productController.getProduct);
router.post("/",      productController.createProduct);
router.put("/:id",    productController.updateProduct);
router.delete("/:id", productController.deleteProduct);

module.exports = router;
```

**server.js:**

```javascript
const express = require("express");
const productRoutes = require("./routes/productRoutes");

const app = express();

// Middleware
app.use(express.json());

// Routes
app.use("/api/products", productRoutes);

// 404 handler for undefined routes
app.use((req, res) => {
    res.status(404).json({
        success: false,
        error: `Route ${req.method} ${req.url} not found`
    });
});

// Error handler
app.use((err, req, res, next) => {
    console.error(err.message);
    res.status(500).json({
        success: false,
        error: "Internal Server Error"
    });
});

// Start server
const PORT = process.env.PORT || 3000;
app.listen(PORT, () => {
    console.log(`Server running on http://localhost:${PORT}`);
});
```

**Folder structure:**
```
products-api/
    server.js
    models/
        productModel.js
    controllers/
        productController.js
    routes/
        productRoutes.js
```
</details>

---

*End of Week 26 Practice Questions.*
