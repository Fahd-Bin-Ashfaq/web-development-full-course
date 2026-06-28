# Week 34: Advanced Features

> **Prerequisites:** React fundamentals (components, state, props, hooks), Node.js and Express basics, MongoDB and Mongoose CRUD operations, REST API design from previous weeks.
>
> **Goal:** Learn how to implement production-level features that real-world applications require -- file uploads, search, pagination, filtering, real-time communication, email notifications, and payment integration.

---

## Table of Contents

1. [Image and File Upload](#1-image-and-file-upload)
2. [Search Functionality](#2-search-functionality)
3. [Pagination](#3-pagination)
4. [Filtering and Sorting](#4-filtering-and-sorting)
5. [Real-Time Features with Socket.io](#5-real-time-features-with-socketio)
6. [Email Notifications with Nodemailer](#6-email-notifications-with-nodemailer)
7. [Payment Integration Overview](#7-payment-integration-overview)
8. [Summary](#8-summary)

---

## 1. Image and File Upload

Every modern application needs file uploads. Users upload profile pictures, attach documents to emails, submit resumes on job boards, and share images on social media. Understanding how files travel from a browser to a server and eventually get stored is a fundamental skill for any full-stack developer.

> **Real-Life Analogy: The Passport Office**
>
> Imagine you visit a passport office to submit your application. You fill out a form (text data) and attach a photograph (file data). The clerk at the counter receives both, checks that the photo meets the required dimensions and format, and then files everything away in a folder with your application number written on it.
>
> In web development, the browser is you, the Express server is the clerk, Multer is the rule checker, the disk or cloud storage is the filing cabinet, and MongoDB stores the reference number (the file path) so the photo can be found again later.

### 1.1 How File Uploads Work

Unlike regular JSON data, files are binary data. They cannot be sent as plain JSON in a request body. Instead, the browser sends files using a special encoding called `multipart/form-data`. On the server side, a middleware called **Multer** parses this multipart data and saves the file to disk or memory.

```
+------------------------------------------------------------------+
|                    FILE UPLOAD FLOW                               |
+------------------------------------------------------------------+
|                                                                    |
|  [ Browser ]                                                       |
|      |                                                             |
|      |  1. User selects file via <input type="file" />             |
|      |  2. JavaScript creates a FormData object                    |
|      |  3. FormData is sent via POST request                       |
|      |                                                             |
|      v                                                             |
|  [ Express Server ]                                                |
|      |                                                             |
|      |  4. Multer middleware intercepts the request                 |
|      |  5. Multer validates file type and size                      |
|      |  6. Multer saves file to disk (or cloud storage)             |
|      |                                                             |
|      v                                                             |
|  [ Disk / Cloud Storage ]                                          |
|      |                                                             |
|      |  7. File is stored with a unique filename                    |
|      |                                                             |
|      v                                                             |
|  [ MongoDB ]                                                       |
|      |                                                             |
|      |  8. The file PATH (not the file itself) is saved             |
|      |     in the database as a string field                        |
|      |                                                             |
+------------------------------------------------------------------+
```

### 1.2 Backend: Multer Setup and Configuration

Multer is a Node.js middleware for handling `multipart/form-data`. It processes file uploads and makes the file information available on `req.file` (for single uploads) or `req.files` (for multiple uploads).

**Step 1: Install Multer**

```bash
npm install multer
```

**Step 2: Configure Multer**

```javascript
// config/multer.js

const multer = require("multer");
const path = require("path");

// Storage configuration: where and how to save files
const storage = multer.diskStorage({
  // destination: the folder where uploaded files will be saved
  destination: function (req, file, cb) {
    cb(null, "uploads/"); // Make sure this folder exists
  },

  // filename: how the saved file should be named
  filename: function (req, file, cb) {
    // Create a unique filename: timestamp + random number + original extension
    const uniqueName =
      Date.now() + "-" + Math.round(Math.random() * 1e9) + path.extname(file.originalname);
    cb(null, uniqueName);
  },
});

// File filter: only allow certain file types
const fileFilter = function (req, file, cb) {
  const allowedTypes = /jpeg|jpg|png|gif|webp/;
  const extname = allowedTypes.test(path.extname(file.originalname).toLowerCase());
  const mimetype = allowedTypes.test(file.mimetype);

  if (extname && mimetype) {
    cb(null, true); // Accept the file
  } else {
    cb(new Error("Only image files (jpeg, jpg, png, gif, webp) are allowed."));
  }
};

// Create the multer instance with configuration
const upload = multer({
  storage: storage,
  fileFilter: fileFilter,
  limits: {
    fileSize: 5 * 1024 * 1024, // 5 MB max file size
  },
});

module.exports = upload;
```

**Step 3: Use Multer in a Route**

```javascript
// routes/productRoutes.js

const express = require("express");
const router = express.Router();
const upload = require("../config/multer");
const Product = require("../models/Product");

// POST /api/products -- Create a product with an image
router.post("/", upload.single("image"), async (req, res) => {
  try {
    const { name, price, description } = req.body;

    const product = new Product({
      name,
      price,
      description,
      image: req.file ? req.file.path : null, // Save the file path, not the file
    });

    await product.save();

    res.status(201).json({
      message: "Product created successfully",
      product,
    });
  } catch (error) {
    res.status(500).json({ message: "Upload failed", error: error.message });
  }
});

module.exports = router;
```

**Step 4: The Mongoose Model**

```javascript
// models/Product.js

const mongoose = require("mongoose");

const productSchema = new mongoose.Schema(
  {
    name: { type: String, required: true },
    price: { type: Number, required: true },
    description: { type: String },
    image: { type: String, default: null }, // Stores the file path as a string
    category: { type: String },
  },
  { timestamps: true }
);

module.exports = mongoose.model("Product", productSchema);
```

**Step 5: Serve Uploaded Files as Static Assets**

```javascript
// server.js (add this line)

app.use("/uploads", express.static("uploads"));
// Now files are accessible at: http://localhost:5000/uploads/filename.jpg
```

### 1.3 Frontend: File Upload in React

On the frontend, we use the native `FormData` API to package both text fields and files into a single request.

```jsx
// components/ProductForm.jsx

import { useState } from "react";
import axios from "axios";

function ProductForm() {
  const [name, setName] = useState("");
  const [price, setPrice] = useState("");
  const [description, setDescription] = useState("");
  const [image, setImage] = useState(null);
  const [preview, setPreview] = useState(null);
  const [loading, setLoading] = useState(false);
  const [message, setMessage] = useState("");

  // Handle file selection
  const handleFileChange = (e) => {
    const file = e.target.files[0];

    if (file) {
      setImage(file);
      // Create a preview URL so the user can see their image before uploading
      setPreview(URL.createObjectURL(file));
    }
  };

  // Handle form submission
  const handleSubmit = async (e) => {
    e.preventDefault();
    setLoading(true);

    // FormData allows us to send files + text in one request
    const formData = new FormData();
    formData.append("name", name);
    formData.append("price", price);
    formData.append("description", description);

    if (image) {
      formData.append("image", image); // Key must match upload.single("image")
    }

    try {
      const response = await axios.post("/api/products", formData, {
        headers: {
          "Content-Type": "multipart/form-data", // Important: tells server to expect file data
        },
      });

      setMessage("Product created successfully!");
      // Reset form
      setName("");
      setPrice("");
      setDescription("");
      setImage(null);
      setPreview(null);
    } catch (error) {
      setMessage("Upload failed: " + error.response?.data?.message);
    } finally {
      setLoading(false);
    }
  };

  return (
    <form onSubmit={handleSubmit}>
      <h2>Add New Product</h2>

      <input
        type="text"
        placeholder="Product Name"
        value={name}
        onChange={(e) => setName(e.target.value)}
        required
      />

      <input
        type="number"
        placeholder="Price"
        value={price}
        onChange={(e) => setPrice(e.target.value)}
        required
      />

      <textarea
        placeholder="Description"
        value={description}
        onChange={(e) => setDescription(e.target.value)}
      />

      <input type="file" accept="image/*" onChange={handleFileChange} />

      {/* Show image preview */}
      {preview && (
        <div>
          <img src={preview} alt="Preview" style={{ width: 200, marginTop: 10 }} />
        </div>
      )}

      <button type="submit" disabled={loading}>
        {loading ? "Uploading..." : "Create Product"}
      </button>

      {message && <p>{message}</p>}
    </form>
  );
}

export default ProductForm;
```

### 1.4 Key Points About File Uploads

| Concept | Details |
|---------|---------|
| **FormData** | Browser API that encodes files + text as `multipart/form-data` |
| **Multer** | Express middleware that parses `multipart/form-data` requests |
| **req.file** | Contains the uploaded file info (path, size, mimetype) after Multer processes it |
| **Static serving** | `express.static()` lets the browser access uploaded files via URL |
| **Never store files in MongoDB** | Store the file on disk or cloud; store only the **path** in the database |
| **File validation** | Always validate file type and size on the server, never trust the client alone |

---

## 2. Search Functionality

Almost every application has a search bar. Users expect to type a few characters and instantly see relevant results. Building a search feature involves three parts: a search input on the frontend, a search endpoint on the backend, and a database query that finds matching records.

### 2.1 The Search Flow

```
+------------------------------------------------------------------+
|                      SEARCH FLOW                                  |
+------------------------------------------------------------------+
|                                                                    |
|  [ User Types in Search Bar ]                                      |
|      |                                                             |
|      |  "lap"  -->  (waits 300ms, debounce)                        |
|      |                                                             |
|      v                                                             |
|  [ React App ]                                                     |
|      |                                                             |
|      |  GET /api/products/search?q=lap                             |
|      |                                                             |
|      v                                                             |
|  [ Express Server ]                                                |
|      |                                                             |
|      |  Reads req.query.q --> "lap"                                 |
|      |  Builds MongoDB query: { name: { $regex: "lap", $options: "i" } }
|      |                                                             |
|      v                                                             |
|  [ MongoDB ]                                                       |
|      |                                                             |
|      |  Finds: "Laptop", "Laptop Stand", "Lap Desk"                |
|      |                                                             |
|      v                                                             |
|  [ Results Sent Back to React ]                                    |
|      |                                                             |
|      |  Displayed in a list on the page                             |
|      |                                                             |
+------------------------------------------------------------------+
```

### 2.2 What is Debouncing?

When a user types in a search bar, every keystroke could trigger an API call. Typing "laptop" would fire five requests: "l", "la", "lap", "lapt", "lapto", "laptop". That is wasteful.

**Debouncing** means waiting until the user stops typing for a set duration (for example, 300 milliseconds) before making the request. If the user types another character within that window, the timer resets.

> **Real-Life Analogy: The Elevator Door**
>
> An elevator door does not close the instant someone presses the button. It waits a moment to see if anyone else is coming. If someone approaches, the timer resets and the door stays open. Only when no one has approached for a few seconds does the door finally close. Debouncing works the same way -- the request only fires when the user stops typing.

### 2.3 Backend: Search Endpoint

```javascript
// routes/productRoutes.js

// GET /api/products/search?q=laptop
router.get("/search", async (req, res) => {
  try {
    const { q } = req.query;

    // If no search query provided, return empty array
    if (!q || q.trim() === "") {
      return res.json({ products: [] });
    }

    // $regex performs a pattern match in MongoDB
    // $options: "i" makes it case-insensitive (matches "Laptop", "laptop", "LAPTOP")
    const products = await Product.find({
      name: { $regex: q, $options: "i" },
    }).limit(20); // Limit results to prevent huge responses

    res.json({ products, count: products.length });
  } catch (error) {
    res.status(500).json({ message: "Search failed", error: error.message });
  }
});
```

### 2.4 Frontend: Search Bar with Debounce

```jsx
// components/SearchBar.jsx

import { useState, useEffect } from "react";
import axios from "axios";

function SearchBar() {
  const [query, setQuery] = useState("");
  const [results, setResults] = useState([]);
  const [loading, setLoading] = useState(false);

  // useEffect with a timer implements debounce
  useEffect(() => {
    // Don't search if query is empty
    if (!query.trim()) {
      setResults([]);
      return;
    }

    // Set a timer: only search after user stops typing for 300ms
    const timer = setTimeout(async () => {
      setLoading(true);
      try {
        const response = await axios.get(`/api/products/search?q=${query}`);
        setResults(response.data.products);
      } catch (error) {
        console.error("Search error:", error);
      } finally {
        setLoading(false);
      }
    }, 300);

    // Cleanup: if user types again before 300ms, cancel the previous timer
    return () => clearTimeout(timer);
  }, [query]); // Runs every time `query` changes

  return (
    <div>
      <input
        type="text"
        placeholder="Search products..."
        value={query}
        onChange={(e) => setQuery(e.target.value)}
      />

      {loading && <p>Searching...</p>}

      <ul>
        {results.map((product) => (
          <li key={product._id}>
            <strong>{product.name}</strong> - ${product.price}
          </li>
        ))}
      </ul>

      {!loading && query && results.length === 0 && <p>No products found.</p>}
    </div>
  );
}

export default SearchBar;
```

### 2.5 MongoDB Text Search Operators

| Operator | Usage | Description |
|----------|-------|-------------|
| `$regex` | `{ name: { $regex: "lap", $options: "i" } }` | Pattern matching, case-insensitive |
| `$text` | `{ $text: { $search: "laptop" } }` | Full-text search (requires a text index) |
| `$options: "i"` | Used with `$regex` | Makes the search case-insensitive |

For small to medium datasets, `$regex` works well. For large-scale production applications, consider creating a **text index** on the fields you want to search, which allows MongoDB to use its optimized full-text search engine.

---

## 3. Pagination

When a database contains thousands of records, loading all of them at once is impractical. It would be slow, consume excessive memory, and overwhelm the user. Pagination solves this by dividing data into manageable pages, showing a fixed number of items per page.

> **Real-Life Analogy: Pages in a Book**
>
> A 500-page book does not show you all 500 pages at once. It shows you one page at a time, and you flip forward or backward as needed. Google search results work the same way -- you see 10 results per page, and you click "Next" to see more. Pagination on a website follows the exact same principle: show a slice of the data, and let the user navigate between slices.

### 3.1 How Pagination Works

```
+------------------------------------------------------------------+
|                    PAGINATION CONCEPT                             |
+------------------------------------------------------------------+
|                                                                    |
|  Total Products: 50          Items per page: 10                    |
|  Total Pages:    50 / 10 = 5 pages                                 |
|                                                                    |
|  Page 1:  Products  1 - 10    (skip 0,  limit 10)                  |
|  Page 2:  Products 11 - 20    (skip 10, limit 10)                  |
|  Page 3:  Products 21 - 30    (skip 20, limit 10)                  |
|  Page 4:  Products 31 - 40    (skip 30, limit 10)                  |
|  Page 5:  Products 41 - 50    (skip 40, limit 10)                  |
|                                                                    |
|  Formula:                                                          |
|    skip  = (page - 1) * limit                                      |
|    pages = Math.ceil(totalItems / limit)                           |
|                                                                    |
+------------------------------------------------------------------+
```

### 3.2 Backend: Paginated Endpoint

```javascript
// routes/productRoutes.js

// GET /api/products?page=2&limit=10
router.get("/", async (req, res) => {
  try {
    // Read page and limit from query string, with defaults
    const page = parseInt(req.query.page) || 1; // Default: page 1
    const limit = parseInt(req.query.limit) || 10; // Default: 10 items per page
    const skip = (page - 1) * limit;

    // Count total documents for calculating total pages
    const totalItems = await Product.countDocuments();
    const totalPages = Math.ceil(totalItems / limit);

    // Fetch only the products for the current page
    const products = await Product.find()
      .skip(skip) // Skip the products from previous pages
      .limit(limit) // Only return `limit` number of products
      .sort({ createdAt: -1 }); // Newest first

    res.json({
      products,
      pagination: {
        currentPage: page,
        totalPages,
        totalItems,
        itemsPerPage: limit,
        hasNextPage: page < totalPages,
        hasPrevPage: page > 1,
      },
    });
  } catch (error) {
    res.status(500).json({ message: "Failed to fetch products", error: error.message });
  }
});
```

### 3.3 Frontend: Pagination Component

```jsx
// components/ProductList.jsx

import { useState, useEffect } from "react";
import axios from "axios";

function ProductList() {
  const [products, setProducts] = useState([]);
  const [pagination, setPagination] = useState({});
  const [currentPage, setCurrentPage] = useState(1);
  const [loading, setLoading] = useState(false);
  const limit = 10;

  // Fetch products whenever the page changes
  useEffect(() => {
    const fetchProducts = async () => {
      setLoading(true);
      try {
        const response = await axios.get(
          `/api/products?page=${currentPage}&limit=${limit}`
        );
        setProducts(response.data.products);
        setPagination(response.data.pagination);
      } catch (error) {
        console.error("Failed to fetch products:", error);
      } finally {
        setLoading(false);
      }
    };

    fetchProducts();
  }, [currentPage]);

  // Generate an array of page numbers for the buttons
  const pageNumbers = [];
  for (let i = 1; i <= pagination.totalPages; i++) {
    pageNumbers.push(i);
  }

  return (
    <div>
      <h2>Products</h2>

      {loading ? (
        <p>Loading...</p>
      ) : (
        <ul>
          {products.map((product) => (
            <li key={product._id}>
              {product.name} - ${product.price}
            </li>
          ))}
        </ul>
      )}

      {/* Pagination Controls */}
      <div style={{ marginTop: 20 }}>
        <button
          onClick={() => setCurrentPage((prev) => prev - 1)}
          disabled={!pagination.hasPrevPage}
        >
          Previous
        </button>

        {pageNumbers.map((number) => (
          <button
            key={number}
            onClick={() => setCurrentPage(number)}
            style={{
              fontWeight: currentPage === number ? "bold" : "normal",
              margin: "0 4px",
            }}
          >
            {number}
          </button>
        ))}

        <button
          onClick={() => setCurrentPage((prev) => prev + 1)}
          disabled={!pagination.hasNextPage}
        >
          Next
        </button>
      </div>

      <p>
        Page {pagination.currentPage} of {pagination.totalPages} ({pagination.totalItems} total
        items)
      </p>
    </div>
  );
}

export default ProductList;
```

### 3.4 Pagination Summary Table

| Concept | Backend (Mongoose) | Frontend (React) |
|---------|--------------------|-------------------|
| **Current page** | `req.query.page` | `useState` for `currentPage` |
| **Items per page** | `req.query.limit` | Constant or state variable |
| **Skip formula** | `.skip((page - 1) * limit)` | Sent as query parameter |
| **Limit** | `.limit(limit)` | Sent as query parameter |
| **Total pages** | `Math.ceil(totalItems / limit)` | Received from API response |
| **Navigation** | N/A | Previous/Next buttons + page number buttons |

---

## 4. Filtering and Sorting

Filtering lets users narrow down results (for example, "show only electronics under $500"), while sorting lets users order results (for example, "cheapest first" or "newest first"). Together, they give users control over how they browse data.

### 4.1 Backend: Filtering and Sorting Endpoint

```javascript
// routes/productRoutes.js

// GET /api/products?category=electronics&minPrice=100&maxPrice=500&sort=price&order=asc&page=1&limit=10
router.get("/", async (req, res) => {
  try {
    const { category, minPrice, maxPrice, sort, order, page, limit } = req.query;

    // Build the filter object dynamically
    const filter = {};

    if (category) {
      filter.category = category;
    }

    if (minPrice || maxPrice) {
      filter.price = {};
      if (minPrice) filter.price.$gte = parseFloat(minPrice); // Greater than or equal
      if (maxPrice) filter.price.$lte = parseFloat(maxPrice); // Less than or equal
    }

    // Build the sort object
    const sortObj = {};
    if (sort) {
      // order can be "asc" (1) or "desc" (-1)
      sortObj[sort] = order === "desc" ? -1 : 1;
    } else {
      sortObj.createdAt = -1; // Default: newest first
    }

    // Pagination
    const pageNum = parseInt(page) || 1;
    const limitNum = parseInt(limit) || 10;
    const skip = (pageNum - 1) * limitNum;

    // Count matching documents (with filters applied)
    const totalItems = await Product.countDocuments(filter);
    const totalPages = Math.ceil(totalItems / limitNum);

    // Execute the query with filter, sort, skip, and limit
    const products = await Product.find(filter)
      .sort(sortObj)
      .skip(skip)
      .limit(limitNum);

    res.json({
      products,
      pagination: {
        currentPage: pageNum,
        totalPages,
        totalItems,
      },
    });
  } catch (error) {
    res.status(500).json({ message: "Failed to fetch products", error: error.message });
  }
});
```

### 4.2 Frontend: Filter and Sort Controls

```jsx
// components/FilterableProductList.jsx

import { useState, useEffect } from "react";
import axios from "axios";

function FilterableProductList() {
  const [products, setProducts] = useState([]);
  const [category, setCategory] = useState("");
  const [minPrice, setMinPrice] = useState("");
  const [maxPrice, setMaxPrice] = useState("");
  const [sortField, setSortField] = useState("createdAt");
  const [sortOrder, setSortOrder] = useState("desc");
  const [currentPage, setCurrentPage] = useState(1);
  const [totalPages, setTotalPages] = useState(1);

  useEffect(() => {
    const fetchProducts = async () => {
      // Build query string from state
      const params = new URLSearchParams();
      if (category) params.append("category", category);
      if (minPrice) params.append("minPrice", minPrice);
      if (maxPrice) params.append("maxPrice", maxPrice);
      params.append("sort", sortField);
      params.append("order", sortOrder);
      params.append("page", currentPage);
      params.append("limit", 10);

      try {
        const response = await axios.get(`/api/products?${params.toString()}`);
        setProducts(response.data.products);
        setTotalPages(response.data.pagination.totalPages);
      } catch (error) {
        console.error("Fetch error:", error);
      }
    };

    fetchProducts();
  }, [category, minPrice, maxPrice, sortField, sortOrder, currentPage]);

  // Reset to page 1 when filters change
  useEffect(() => {
    setCurrentPage(1);
  }, [category, minPrice, maxPrice, sortField, sortOrder]);

  return (
    <div>
      <h2>Products</h2>

      {/* Filter Controls */}
      <div>
        <label>Category: </label>
        <select value={category} onChange={(e) => setCategory(e.target.value)}>
          <option value="">All Categories</option>
          <option value="electronics">Electronics</option>
          <option value="clothing">Clothing</option>
          <option value="books">Books</option>
          <option value="home">Home & Garden</option>
        </select>

        <label> Min Price: </label>
        <input
          type="number"
          placeholder="0"
          value={minPrice}
          onChange={(e) => setMinPrice(e.target.value)}
        />

        <label> Max Price: </label>
        <input
          type="number"
          placeholder="1000"
          value={maxPrice}
          onChange={(e) => setMaxPrice(e.target.value)}
        />
      </div>

      {/* Sort Controls */}
      <div style={{ marginTop: 10 }}>
        <label>Sort by: </label>
        <select value={sortField} onChange={(e) => setSortField(e.target.value)}>
          <option value="createdAt">Date Added</option>
          <option value="price">Price</option>
          <option value="name">Name</option>
        </select>

        <button onClick={() => setSortOrder(sortOrder === "asc" ? "desc" : "asc")}>
          {sortOrder === "asc" ? "Ascending" : "Descending"}
        </button>
      </div>

      {/* Product List */}
      <ul>
        {products.map((product) => (
          <li key={product._id}>
            {product.name} - ${product.price} ({product.category})
          </li>
        ))}
      </ul>

      {/* Pagination */}
      <div>
        <button
          onClick={() => setCurrentPage((p) => p - 1)}
          disabled={currentPage === 1}
        >
          Previous
        </button>
        <span>
          {" "}Page {currentPage} of {totalPages}{" "}
        </span>
        <button
          onClick={() => setCurrentPage((p) => p + 1)}
          disabled={currentPage === totalPages}
        >
          Next
        </button>
      </div>
    </div>
  );
}

export default FilterableProductList;
```

### 4.3 Common MongoDB Query Operators for Filtering

| Operator | Meaning | Example |
|----------|---------|---------|
| `$eq` | Equal to | `{ status: { $eq: "active" } }` |
| `$ne` | Not equal to | `{ status: { $ne: "deleted" } }` |
| `$gt` | Greater than | `{ price: { $gt: 100 } }` |
| `$gte` | Greater than or equal | `{ price: { $gte: 100 } }` |
| `$lt` | Less than | `{ price: { $lt: 500 } }` |
| `$lte` | Less than or equal | `{ price: { $lte: 500 } }` |
| `$in` | Matches any value in array | `{ category: { $in: ["electronics", "books"] } }` |
| `$regex` | Pattern matching | `{ name: { $regex: "phone", $options: "i" } }` |

---

## 5. Real-Time Features with Socket.io

Traditional HTTP communication follows a strict request-response pattern: the client sends a request, the server sends back a response, and the connection closes. But what if you need the server to push data to the client without the client asking? Think of a chat application, live sports scores, stock tickers, or collaborative editing tools. This is where **WebSockets** come in.

### 5.1 HTTP vs WebSocket

```
+------------------------------------------------------------------+
|               HTTP (Request-Response)                             |
+------------------------------------------------------------------+
|                                                                    |
|  Client                              Server                       |
|    |                                    |                          |
|    |------- Request ("Any new msgs?") ->|                          |
|    |<------ Response ("No") ------------|                          |
|    |                                    |                          |
|    |------- Request ("Any new msgs?") ->|                          |
|    |<------ Response ("No") ------------|                          |
|    |                                    |                          |
|    |------- Request ("Any new msgs?") ->|                          |
|    |<------ Response ("Yes! Here.") ----|                          |
|    |                                    |                          |
|  The client must keep asking. Wasteful.                            |
|                                                                    |
+------------------------------------------------------------------+

+------------------------------------------------------------------+
|               WebSocket (Bidirectional)                            |
+------------------------------------------------------------------+
|                                                                    |
|  Client                              Server                       |
|    |                                    |                          |
|    |===== Connection Established =======|  (handshake, stays open) |
|    |                                    |                          |
|    |<------ "New message from Ali" -----|  (server pushes data)    |
|    |------- "Reply: Thanks!" --------->|  (client sends data)     |
|    |<------ "Ali is typing..." --------|  (server pushes again)   |
|    |                                    |                          |
|  Connection stays open. Both sides can send anytime.               |
|                                                                    |
+------------------------------------------------------------------+
```

| Feature | HTTP | WebSocket |
|---------|------|-----------|
| **Connection** | Opens and closes per request | Stays open continuously |
| **Direction** | Client initiates, server responds | Both sides can send anytime |
| **Use case** | Loading pages, form submissions, API calls | Chat, live updates, gaming |
| **Overhead** | Higher (new connection each time) | Lower (single persistent connection) |
| **Library** | Axios, Fetch API | Socket.io |

### 5.2 What is Socket.io?

**Socket.io** is a JavaScript library that provides real-time, bidirectional, event-based communication. It uses WebSockets under the hood but adds features like automatic reconnection, fallback to HTTP long-polling, and room-based communication.

### 5.3 Backend: Socket.io Server Setup

```bash
npm install socket.io
```

```javascript
// server.js

const express = require("express");
const http = require("http");
const { Server } = require("socket.io");

const app = express();

// Create an HTTP server from the Express app
const server = http.createServer(app);

// Attach Socket.io to the HTTP server
const io = new Server(server, {
  cors: {
    origin: "http://localhost:3000", // React app URL
    methods: ["GET", "POST"],
  },
});

// Listen for client connections
io.on("connection", (socket) => {
  console.log("A user connected:", socket.id);

  // Listen for "chat message" events from this client
  socket.on("chat message", (data) => {
    console.log("Message received:", data);

    // Broadcast the message to ALL connected clients (including sender)
    io.emit("chat message", data);
  });

  // Listen for "typing" events
  socket.on("typing", (username) => {
    // Broadcast to everyone EXCEPT the sender
    socket.broadcast.emit("typing", username);
  });

  // Handle disconnection
  socket.on("disconnect", () => {
    console.log("User disconnected:", socket.id);
  });
});

// Start the server
const PORT = 5000;
server.listen(PORT, () => {
  console.log(`Server running on port ${PORT}`);
});
```

### 5.4 Frontend: Socket.io Client in React

```bash
npm install socket.io-client
```

```jsx
// components/Chat.jsx

import { useState, useEffect, useRef } from "react";
import { io } from "socket.io-client";

// Connect to the server
const socket = io("http://localhost:5000");

function Chat() {
  const [messages, setMessages] = useState([]);
  const [input, setInput] = useState("");
  const [username, setUsername] = useState("");
  const [typingUser, setTypingUser] = useState("");
  const messagesEndRef = useRef(null);

  useEffect(() => {
    // Prompt for username on mount
    const name = prompt("Enter your name:") || "Anonymous";
    setUsername(name);

    // Listen for incoming messages
    socket.on("chat message", (data) => {
      setMessages((prev) => [...prev, data]);
    });

    // Listen for typing indicators
    socket.on("typing", (user) => {
      setTypingUser(`${user} is typing...`);
      // Clear typing indicator after 2 seconds
      setTimeout(() => setTypingUser(""), 2000);
    });

    // Cleanup listeners on unmount
    return () => {
      socket.off("chat message");
      socket.off("typing");
    };
  }, []);

  // Auto-scroll to the latest message
  useEffect(() => {
    messagesEndRef.current?.scrollIntoView({ behavior: "smooth" });
  }, [messages]);

  const sendMessage = (e) => {
    e.preventDefault();
    if (!input.trim()) return;

    const messageData = {
      username,
      text: input,
      time: new Date().toLocaleTimeString(),
    };

    socket.emit("chat message", messageData);
    setInput("");
  };

  const handleTyping = () => {
    socket.emit("typing", username);
  };

  return (
    <div>
      <h2>Chat Room</h2>

      <div style={{ height: 400, overflowY: "auto", border: "1px solid #ccc", padding: 10 }}>
        {messages.map((msg, index) => (
          <div key={index}>
            <strong>{msg.username}</strong> <small>({msg.time})</small>
            <p>{msg.text}</p>
          </div>
        ))}
        <div ref={messagesEndRef} />
      </div>

      {typingUser && <p><em>{typingUser}</em></p>}

      <form onSubmit={sendMessage}>
        <input
          type="text"
          value={input}
          onChange={(e) => setInput(e.target.value)}
          onKeyDown={handleTyping}
          placeholder="Type a message..."
        />
        <button type="submit">Send</button>
      </form>
    </div>
  );
}

export default Chat;
```

### 5.5 Key Socket.io Concepts

| Method | Description |
|--------|-------------|
| `io.on("connection", callback)` | Server listens for new client connections |
| `socket.on("event", callback)` | Listen for a custom event from the other side |
| `socket.emit("event", data)` | Send a custom event to the other side |
| `io.emit("event", data)` | Server sends to ALL connected clients |
| `socket.broadcast.emit("event", data)` | Server sends to all clients EXCEPT the sender |
| `socket.disconnect()` | Disconnect from the server |

---

## 6. Email Notifications with Nodemailer

Applications frequently need to send emails: welcome messages after registration, password reset links, order confirmations, or notification alerts. **Nodemailer** is the most popular Node.js library for sending emails.

### 6.1 When to Send Emails

| Scenario | Email Type | Trigger |
|----------|-----------|---------|
| User signs up | Welcome email | After successful registration |
| User forgets password | Password reset link | After requesting reset |
| Order placed | Order confirmation | After payment is processed |
| Shipment update | Shipping notification | When order status changes |
| Account activity | Security alert | When login from new device |

### 6.2 Setting Up Nodemailer

```bash
npm install nodemailer
```

### 6.3 Gmail SMTP Configuration

To use Gmail as your email provider, you need to generate an **App Password** (not your regular Gmail password). Go to your Google Account settings, enable 2-Factor Authentication, and then create an App Password specifically for your application.

```javascript
// config/email.js

const nodemailer = require("nodemailer");

// Create a transporter -- this is the "mail carrier" that delivers your emails
const transporter = nodemailer.createTransport({
  service: "gmail",
  auth: {
    user: process.env.EMAIL_USER, // Your Gmail address
    pass: process.env.EMAIL_PASS, // App Password (not your regular password)
  },
});

module.exports = transporter;
```

### 6.4 Sending Emails

```javascript
// utils/sendEmail.js

const transporter = require("../config/email");

async function sendEmail({ to, subject, html }) {
  try {
    const mailOptions = {
      from: `"My App" <${process.env.EMAIL_USER}>`, // Sender name and address
      to, // Recipient email address
      subject, // Email subject line
      html, // Email body in HTML format
    };

    const info = await transporter.sendMail(mailOptions);
    console.log("Email sent:", info.messageId);
    return info;
  } catch (error) {
    console.error("Email sending failed:", error);
    throw error;
  }
}

module.exports = sendEmail;
```

### 6.5 Using the Email Utility in Routes

```javascript
// routes/authRoutes.js

const sendEmail = require("../utils/sendEmail");

// POST /api/auth/register
router.post("/register", async (req, res) => {
  try {
    const { name, email, password } = req.body;

    // ... create user in database ...

    // Send welcome email after registration
    await sendEmail({
      to: email,
      subject: "Welcome to Our App!",
      html: `
        <h1>Welcome, ${name}!</h1>
        <p>Thank you for signing up. Your account has been created successfully.</p>
        <p>You can now log in and start exploring.</p>
        <a href="http://localhost:3000/login">Log In Now</a>
      `,
    });

    res.status(201).json({ message: "User registered. Welcome email sent." });
  } catch (error) {
    res.status(500).json({ message: "Registration failed", error: error.message });
  }
});
```

### 6.6 Environment Variables for Email

Always store email credentials in environment variables, never in your source code.

```bash
# .env file
EMAIL_USER=yourname@gmail.com
EMAIL_PASS=your-app-password-here
```

> **Important Security Note:** Never commit your `.env` file to Git. Add `.env` to your `.gitignore` file. App Passwords should be treated with the same care as any other secret credential.

---

## 7. Payment Integration Overview

Accepting payments is one of the most sensitive features a web application can implement. You are dealing with real money and real credit card numbers. This is why developers use established payment processors like **Stripe** rather than handling card details directly.

> **Real-Life Analogy: The Cash Register vs. The Card Machine**
>
> When you pay with cash at a store, the cashier handles your money directly. But when you pay with a card, neither the cashier nor the store ever sees your card number. The card machine (Stripe) handles everything -- it securely reads your card, talks to your bank, confirms the payment, and tells the cashier "payment approved." The store only receives a confirmation, never the card details. Stripe works the same way in web applications.

### 7.1 Why Use Stripe?

| Concern | Without Stripe | With Stripe |
|---------|----------------|-------------|
| **Card security** | You store card numbers (PCI compliance nightmare) | Stripe handles all card data securely |
| **Fraud detection** | You build your own fraud system | Stripe has built-in fraud detection |
| **Multiple payment methods** | You integrate each one separately | Stripe supports cards, wallets, bank transfers |
| **Compliance** | You handle PCI DSS compliance yourself | Stripe is PCI Level 1 certified |
| **Refunds** | You build refund logic | Stripe provides refund APIs |

### 7.2 Payment Flow

```
+------------------------------------------------------------------+
|                    STRIPE PAYMENT FLOW                             |
+------------------------------------------------------------------+
|                                                                    |
|  [ 1. Customer Clicks "Pay" ]                                     |
|      |                                                             |
|      v                                                             |
|  [ 2. React App ]                                                  |
|      |  Sends order details to your backend                        |
|      |                                                             |
|      v                                                             |
|  [ 3. Express Server ]                                             |
|      |  Creates a "Payment Intent" via Stripe API                  |
|      |  Receives a client_secret from Stripe                       |
|      |  Sends client_secret back to React                          |
|      |                                                             |
|      v                                                             |
|  [ 4. React App ]                                                  |
|      |  Uses Stripe Elements (secure card form)                    |
|      |  Confirms payment using the client_secret                   |
|      |  Card details go DIRECTLY to Stripe (never touch your server)
|      |                                                             |
|      v                                                             |
|  [ 5. Stripe ]                                                     |
|      |  Processes the payment with the bank                        |
|      |  Returns success or failure                                  |
|      |                                                             |
|      v                                                             |
|  [ 6. React App ]                                                  |
|      |  Shows "Payment Successful" or error message                 |
|      |                                                             |
|      v                                                             |
|  [ 7. Stripe Webhook (Optional) ]                                  |
|      |  Stripe sends a confirmation event to your server            |
|      |  Server updates the order status in MongoDB                  |
|      |                                                             |
+------------------------------------------------------------------+
```

### 7.3 Backend: Creating a Payment Intent

```bash
npm install stripe
```

```javascript
// routes/paymentRoutes.js

const express = require("express");
const router = express.Router();
const stripe = require("stripe")(process.env.STRIPE_SECRET_KEY);

// POST /api/payments/create-payment-intent
router.post("/create-payment-intent", async (req, res) => {
  try {
    const { amount, currency } = req.body;

    // Create a Payment Intent on Stripe
    // amount is in the smallest currency unit (cents for USD)
    // $49.99 = 4999 cents
    const paymentIntent = await stripe.paymentIntents.create({
      amount: amount, // e.g., 4999 for $49.99
      currency: currency || "usd",
      automatic_payment_methods: {
        enabled: true,
      },
    });

    // Send the client secret to the frontend
    // The frontend uses this to confirm the payment
    res.json({
      clientSecret: paymentIntent.client_secret,
    });
  } catch (error) {
    res.status(500).json({ message: "Payment failed", error: error.message });
  }
});

module.exports = router;
```

### 7.4 Frontend: Stripe Elements (Concept)

Stripe provides pre-built, secure UI components called **Stripe Elements**. These are iframes that Stripe hosts -- your application never touches the card details.

```bash
npm install @stripe/react-stripe-js @stripe/stripe-js
```

```jsx
// components/CheckoutForm.jsx

import { useState } from "react";
import { CardElement, useStripe, useElements } from "@stripe/react-stripe-js";
import axios from "axios";

function CheckoutForm({ amount }) {
  const stripe = useStripe();
  const elements = useElements();
  const [loading, setLoading] = useState(false);
  const [message, setMessage] = useState("");

  const handleSubmit = async (e) => {
    e.preventDefault();
    setLoading(true);

    try {
      // Step 1: Ask your server to create a Payment Intent
      const { data } = await axios.post("/api/payments/create-payment-intent", {
        amount: amount * 100, // Convert dollars to cents
        currency: "usd",
      });

      // Step 2: Confirm the payment using the client secret
      const result = await stripe.confirmCardPayment(data.clientSecret, {
        payment_method: {
          card: elements.getElement(CardElement),
        },
      });

      if (result.error) {
        setMessage(`Payment failed: ${result.error.message}`);
      } else if (result.paymentIntent.status === "succeeded") {
        setMessage("Payment successful!");
      }
    } catch (error) {
      setMessage("An error occurred.");
    } finally {
      setLoading(false);
    }
  };

  return (
    <form onSubmit={handleSubmit}>
      <h3>Pay ${amount}</h3>

      {/* Stripe's secure card input -- card details never touch your server */}
      <CardElement />

      <button type="submit" disabled={!stripe || loading}>
        {loading ? "Processing..." : `Pay $${amount}`}
      </button>

      {message && <p>{message}</p>}
    </form>
  );
}

export default CheckoutForm;
```

```jsx
// App.jsx (wrapping with Stripe provider)

import { Elements } from "@stripe/react-stripe-js";
import { loadStripe } from "@stripe/stripe-js";
import CheckoutForm from "./components/CheckoutForm";

// Load Stripe with your PUBLISHABLE key (not the secret key)
const stripePromise = loadStripe("pk_test_your_publishable_key_here");

function App() {
  return (
    <Elements stripe={stripePromise}>
      <CheckoutForm amount={49.99} />
    </Elements>
  );
}

export default App;
```

### 7.5 Security Considerations

| Rule | Reason |
|------|--------|
| **Never log card numbers** | PCI compliance violation; legal liability |
| **Use HTTPS in production** | Encrypts data in transit; Stripe requires it |
| **Secret key on server only** | `STRIPE_SECRET_KEY` must never appear in frontend code |
| **Publishable key on client** | `pk_test_...` is safe to use in the browser |
| **Validate amounts server-side** | Never trust the client to send the correct price |
| **Use webhooks for confirmation** | Do not rely solely on client-side success; use Stripe webhooks to verify |
| **Store keys in .env** | Never hardcode API keys in source code |

### 7.6 Environment Variables for Stripe

```bash
# .env file
STRIPE_SECRET_KEY=sk_test_your_secret_key_here
STRIPE_PUBLISHABLE_KEY=pk_test_your_publishable_key_here
```

---

## 8. Summary

This week covered seven advanced features that elevate a basic CRUD application into something closer to a production-ready product.

| Feature | Frontend | Backend | Key Tool/Library |
|---------|----------|---------|------------------|
| **File Upload** | FormData, file input, preview | Multer middleware, static serving | `multer` |
| **Search** | Debounced search bar | `$regex` query on MongoDB | `useEffect` timer |
| **Pagination** | Page buttons, page state | `skip()` and `limit()` in Mongoose | Query parameters |
| **Filtering & Sorting** | Dropdowns, sort buttons | Dynamic query building | MongoDB operators |
| **Real-Time (Socket.io)** | `socket.io-client`, event listeners | `socket.io`, event emitters | WebSocket protocol |
| **Email (Nodemailer)** | N/A (triggered by backend) | SMTP transporter, sendMail | `nodemailer` |
| **Payments (Stripe)** | Stripe Elements, card form | Payment Intent API | `stripe` |

### Key Takeaways

1. **File uploads** use `multipart/form-data` encoding. Never store files directly in the database -- store them on disk or cloud and save the path.

2. **Search** should always be debounced on the frontend to avoid excessive API calls. MongoDB's `$regex` operator handles basic pattern matching.

3. **Pagination** uses `skip()` and `limit()` to divide large datasets into pages. Always send pagination metadata (total pages, current page) in the API response.

4. **Filtering and sorting** are built by dynamically constructing MongoDB query objects from URL query parameters. This keeps the API flexible.

5. **WebSockets** enable real-time, bidirectional communication. Socket.io simplifies WebSocket usage with features like automatic reconnection and event-based messaging.

6. **Nodemailer** sends emails through SMTP. Always use environment variables for credentials and never commit secrets to version control.

7. **Stripe** handles payment processing securely. Card details flow directly from the browser to Stripe, never passing through your server. Always validate payment amounts on the server side.

These features form the backbone of most modern web applications. Mastering them will prepare you to build fully functional, production-grade projects.
