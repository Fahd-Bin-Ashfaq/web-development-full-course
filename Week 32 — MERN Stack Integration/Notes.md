# Week 32 — MERN Stack Integration

> **Prerequisites:** React (Weeks 16-21), Node.js & Express (Weeks 22-27), MongoDB & Mongoose (Weeks 28-31)
> **Goal:** Learn how to connect a React frontend with an Express backend and a MongoDB database to build complete full-stack web applications using the MERN stack.

---

## Table of Contents

1. [What is Full-Stack Development?](#1-what-is-full-stack-development)
2. [Connecting React to Express](#2-connecting-react-to-express)
3. [CORS Configuration and Why It's Needed](#3-cors-configuration-and-why-its-needed)
4. [Proxy Setup in Vite](#4-proxy-setup-in-vite)
5. [Using Axios vs Fetch for API Calls](#5-using-axios-vs-fetch-for-api-calls)
6. [Folder Structure for Full-Stack Projects](#6-folder-structure-for-full-stack-projects)
7. [Environment Variables for Frontend](#7-environment-variables-for-frontend)
8. [Building a Complete Data Flow Diagram](#8-building-a-complete-data-flow-diagram)
9. [Summary](#9-summary)

---

## 1. What is Full-Stack Development?

Until now, you have learned three major technologies separately:

- **React** (Weeks 16-21) — building user interfaces that run in the browser.
- **Express** (Weeks 24-27) — creating server-side APIs that handle requests and business logic.
- **MongoDB with Mongoose** (Weeks 28-31) — storing and retrieving data in a database.

Each of these is powerful on its own, but a real application requires all three working together. **Full-stack development** means building both the frontend (what the user sees) and the backend (what processes data and communicates with the database), and connecting them into a single, cohesive application.

The **MERN stack** is one of the most popular full-stack combinations:

| Letter | Technology | Role                                      |
|--------|------------|-------------------------------------------|
| **M**  | MongoDB    | Database — stores application data        |
| **E**  | Express.js | Backend framework — handles API routes    |
| **R**  | React      | Frontend library — builds the user interface |
| **N**  | Node.js    | Runtime — executes JavaScript on the server |

### The Restaurant Analogy

> Imagine a **restaurant**. The **dining area** is your React frontend — it is where customers (users) sit, read the menu, and place orders. The **kitchen** is your Express backend — it receives orders, processes them, applies business rules (no substitutions after 9 PM), and prepares the response. The **pantry and cold storage** is your MongoDB database — it holds all the raw ingredients (data) that the kitchen needs to prepare dishes. The **waiter** carrying orders between the dining area and the kitchen is the **HTTP request** — the communication layer that connects frontend to backend.

```
              THE RESTAURANT ANALOGY — MERN STACK

  +---------------------+        +---------------------+        +---------------------+
  |    DINING AREA      |        |      KITCHEN         |        |      PANTRY         |
  |    (React)          |        |      (Express)       |        |      (MongoDB)      |
  |                     |        |                      |        |                     |
  |  Customer reads     | Order  |  Chef receives       | Fetch  |  Ingredients are    |
  |  the menu and  -----|------->|  the order and  -----|------->|  stored here.       |
  |  places an order.   |        |  prepares the dish.  |        |  Chef grabs what    |
  |                     | Dish   |                      | Data   |  is needed.         |
  |  Customer receives  |<-------|  Dish is ready and   |<-------|                     |
  |  the finished dish. |        |  sent to the table.  |        |                     |
  +---------------------+        +---------------------+        +---------------------+
        FRONTEND                       BACKEND                       DATABASE
    (User Interface)              (Business Logic)                (Data Storage)
```

### How the Pieces Fit Together

In a MERN application, data flows in a clear path:

1. The **user** interacts with the **React frontend** (clicks a button, submits a form).
2. React sends an **HTTP request** (GET, POST, PUT, DELETE) to the **Express backend**.
3. Express receives the request, processes it, and communicates with **MongoDB** using **Mongoose** models.
4. MongoDB returns the requested data to Express.
5. Express sends an **HTTP response** (usually JSON) back to React.
6. React updates the **UI** to reflect the new data.

```
  THE MERN DATA FLOW

  +----------+     HTTP Request      +-----------+     Mongoose Query     +----------+
  |          | -------------------> |            | --------------------> |          |
  |  React   |                      |  Express   |                       | MongoDB  |
  | Frontend |                      |  Backend   |                       | Database |
  |          | <------------------- |            | <-------------------- |          |
  +----------+     HTTP Response     +-----------+     Query Result       +----------+
    (Port 5173)     (JSON data)       (Port 5000)                         (Port 27017)
```

Each part runs independently. React runs in the browser, Express runs on a Node.js server, and MongoDB runs as a separate database service. They communicate over the network using HTTP requests and database queries. This separation is what makes full-stack applications flexible, scalable, and maintainable.

---

## 2. Connecting React to Express

The most fundamental skill in full-stack development is making your React frontend talk to your Express backend. This happens through **HTTP requests** — the same mechanism your browser uses when you visit any website.

### The Post Office Analogy

> Think of your React app as a person who needs to send letters and receive replies. The **Express server** is the post office. When React needs data, it writes a letter (HTTP request), addresses it to a specific route (`/api/products`), and sends it off. The post office (Express) processes the letter, gathers the information requested, and sends a reply letter (HTTP response) back. React then opens the reply and displays the contents to the user.

### Step 1: The Express Backend Route

First, let us create a simple Express API that serves product data. This is the backend that React will communicate with.

```javascript
// server/index.js
const express = require("express");
const app = express();
const PORT = 5000;

// Middleware to parse JSON request bodies
app.use(express.json());

// Sample product data (in a real app, this comes from MongoDB)
const products = [
  { id: 1, name: "Wireless Headphones", price: 59.99, inStock: true },
  { id: 2, name: "Mechanical Keyboard", price: 129.99, inStock: true },
  { id: 3, name: "USB-C Hub", price: 34.99, inStock: false },
  { id: 4, name: "Webcam HD", price: 79.99, inStock: true },
];

// GET all products
app.get("/api/products", (req, res) => {
  res.json(products);
});

// GET a single product by ID
app.get("/api/products/:id", (req, res) => {
  const product = products.find((p) => p.id === parseInt(req.params.id));

  if (!product) {
    return res.status(404).json({ message: "Product not found" });
  }

  res.json(product);
});

// POST a new product
app.post("/api/products", (req, res) => {
  const newProduct = {
    id: products.length + 1,
    name: req.body.name,
    price: req.body.price,
    inStock: req.body.inStock ?? true,
  };

  products.push(newProduct);
  res.status(201).json(newProduct);
});

app.listen(PORT, () => {
  console.log(`Server running on http://localhost:${PORT}`);
});
```

### Step 2: The React Frontend Component

Now, let us create a React component that fetches products from the Express backend and displays them.

```jsx
// client/src/components/ProductList.jsx
import { useState, useEffect } from "react";

function ProductList() {
  const [products, setProducts] = useState([]);
  const [loading, setLoading] = useState(true);
  const [error, setError] = useState(null);

  useEffect(() => {
    // Fetch products from the Express backend
    fetch("http://localhost:5000/api/products")
      .then((response) => {
        // Check if the response is OK (status 200-299)
        if (!response.ok) {
          throw new Error(`HTTP error! Status: ${response.status}`);
        }
        return response.json();
      })
      .then((data) => {
        setProducts(data);
        setLoading(false);
      })
      .catch((err) => {
        setError(err.message);
        setLoading(false);
      });
  }, []); // Empty dependency array = runs once on mount

  if (loading) return <p>Loading products...</p>;
  if (error) return <p>Error: {error}</p>;

  return (
    <div>
      <h1>Our Products</h1>
      <ul>
        {products.map((product) => (
          <li key={product.id}>
            <strong>{product.name}</strong> — ${product.price.toFixed(2)}
            {product.inStock ? " (In Stock)" : " (Out of Stock)"}
          </li>
        ))}
      </ul>
    </div>
  );
}

export default ProductList;
```

### Step 3: Adding a New Product (POST Request)

```jsx
// client/src/components/AddProduct.jsx
import { useState } from "react";

function AddProduct({ onProductAdded }) {
  const [name, setName] = useState("");
  const [price, setPrice] = useState("");

  const handleSubmit = async (e) => {
    e.preventDefault();

    try {
      const response = await fetch("http://localhost:5000/api/products", {
        method: "POST",
        headers: {
          "Content-Type": "application/json",
        },
        body: JSON.stringify({
          name: name,
          price: parseFloat(price),
        }),
      });

      if (!response.ok) {
        throw new Error("Failed to add product");
      }

      const newProduct = await response.json();
      onProductAdded(newProduct); // Notify parent component
      setName("");
      setPrice("");
    } catch (err) {
      console.error("Error adding product:", err);
    }
  };

  return (
    <form onSubmit={handleSubmit}>
      <h2>Add New Product</h2>
      <input
        type="text"
        placeholder="Product name"
        value={name}
        onChange={(e) => setName(e.target.value)}
        required
      />
      <input
        type="number"
        placeholder="Price"
        value={price}
        onChange={(e) => setPrice(e.target.value)}
        step="0.01"
        required
      />
      <button type="submit">Add Product</button>
    </form>
  );
}

export default AddProduct;
```

### What Happens Under the Hood

When the React component mounts, here is the exact sequence of events:

```
  FETCH REQUEST LIFECYCLE

  React Component                    Express Server
  +-----------------+               +-----------------+
  |                 |               |                 |
  | 1. useEffect    |               |                 |
  |    fires        |               |                 |
  |                 |               |                 |
  | 2. fetch() is   |   HTTP GET    |                 |
  |    called  -----|-------------->| 3. Route handler |
  |                 |               |    executes      |
  |                 |               |                 |
  |                 |   JSON data   | 4. res.json()   |
  | 5. .then()      |<-------------|    sends data    |
  |    receives     |               |                 |
  |    response     |               |                 |
  |                 |               |                 |
  | 6. setProducts  |               |                 |
  |    updates      |               |                 |
  |    state        |               |                 |
  |                 |               |                 |
  | 7. Component    |               |                 |
  |    re-renders   |               |                 |
  |    with data    |               |                 |
  +-----------------+               +-----------------+
```

If you try to run this right now, you will encounter an error. The browser will block the request. This is because of something called **CORS**, which we will cover in the next section.

---

## 3. CORS Configuration and Why It's Needed

### The Same-Origin Policy

Browsers enforce a security rule called the **Same-Origin Policy**. It states that a web page can only make requests to the same **origin** it was loaded from. An origin is defined by three parts:

| Part       | Example                |
|------------|------------------------|
| **Protocol** | `http` or `https`    |
| **Domain**   | `localhost`          |
| **Port**     | `5173` or `5000`     |

If any of these three parts differ between the page and the request target, the browser considers it a **cross-origin request** and blocks it by default.

```
  SAME-ORIGIN vs CROSS-ORIGIN

  React App (http://localhost:5173)
  +---------------------------------+
  |                                 |
  | fetch("http://localhost:5173/x")  --> SAME ORIGIN      --> Allowed
  |                                 |
  | fetch("http://localhost:5000/x")  --> DIFFERENT PORT    --> Blocked!
  |                                 |
  | fetch("https://localhost:5173/x") --> DIFFERENT PROTOCOL --> Blocked!
  |                                 |
  | fetch("http://example.com/x")    --> DIFFERENT DOMAIN   --> Blocked!
  |                                 |
  +---------------------------------+
```

### Why Does This Rule Exist?

The Same-Origin Policy exists to protect users. Without it, any website you visit could silently make requests to your bank's website, your email, or any other service you are logged into — using your cookies and session data. This would be a massive security vulnerability.

> Imagine you live in an apartment building with a **security guard**. The guard knows you live in apartment 5173. If someone from apartment 5000 tries to send you a package, the guard stops it and says: "I do not recognize this sender. They are from a different apartment. The package is rejected unless the sender provides proper identification (CORS headers)."

### What is CORS?

**CORS** stands for **Cross-Origin Resource Sharing**. It is a mechanism that allows a server to explicitly tell browsers: "It is safe to accept requests from this other origin." The server does this by including special headers in its response.

```
  CORS FLOW — How the Browser Handles Cross-Origin Requests

  React (localhost:5173)          Browser                    Express (localhost:5000)
  +-------------------+      +-------------+              +-------------------+
  |                   |      |             |              |                   |
  | 1. fetch("/api")  |----->| 2. Detects  |              |                   |
  |                   |      | cross-origin|              |                   |
  |                   |      |             |  3. Preflight|                   |
  |                   |      |    OPTIONS   |  (OPTIONS)  |                   |
  |                   |      |    request --|------------->| 4. Server checks  |
  |                   |      |             |              |    origin and     |
  |                   |      |             |  5. CORS     |    responds with  |
  |                   |      |    headers  |<-------------|    CORS headers   |
  |                   |      |             |              |                   |
  |                   |      | 6. Headers  |              |                   |
  |                   |      |    OK?      |              |                   |
  |                   |      |    YES -->  |  7. Actual   |                   |
  |                   |      |    send     |  GET request |                   |
  |                   |      |    real  ---|------------->| 8. Process and    |
  |                   |      |    request  |              |    return data    |
  |                   |      |             |  9. JSON     |                   |
  | 10. Receives data |<-----|    data  ---|<-------------|                   |
  |     and renders   |      |             |              |                   |
  +-------------------+      +-------------+              +-------------------+
```

For certain requests (POST with JSON, custom headers, etc.), the browser sends a **preflight request** first — an OPTIONS request that asks the server: "Are you willing to accept this type of request from this origin?" Only if the server responds with the correct CORS headers does the browser proceed with the actual request.

### Setting Up CORS in Express

Install the `cors` package:

```bash
npm install cors
```

Then configure it in your Express application:

```javascript
// server/index.js
const express = require("express");
const cors = require("cors");
const app = express();

// Option 1: Allow ALL origins (good for development, risky for production)
app.use(cors());

// Option 2: Allow specific origin(s) (recommended for production)
app.use(
  cors({
    origin: "http://localhost:5173", // Only allow your React app
    methods: ["GET", "POST", "PUT", "DELETE"], // Allowed HTTP methods
    credentials: true, // Allow cookies and auth headers
  })
);

// Option 3: Allow multiple specific origins
app.use(
  cors({
    origin: ["http://localhost:5173", "http://localhost:3000"],
    methods: ["GET", "POST", "PUT", "DELETE"],
    credentials: true,
  })
);

app.use(express.json());

// ... your routes here
```

### CORS Configuration Options Explained

| Option          | Description                                                   | Example                                |
|-----------------|---------------------------------------------------------------|----------------------------------------|
| `origin`        | Which origins are allowed to make requests                    | `"http://localhost:5173"` or `"*"`     |
| `methods`       | Which HTTP methods are allowed                                | `["GET", "POST", "PUT", "DELETE"]`     |
| `credentials`   | Whether cookies and auth headers are allowed                  | `true` or `false`                      |
| `allowedHeaders`| Which custom headers the client can send                      | `["Content-Type", "Authorization"]`    |
| `exposedHeaders`| Which response headers the client can access                  | `["X-Total-Count"]`                    |
| `maxAge`        | How long (in seconds) the browser caches preflight results    | `86400` (24 hours)                     |

After adding CORS middleware, the fetch request from our React component in Section 2 will work correctly. The server now tells the browser: "Yes, requests from `http://localhost:5173` are allowed."

---

## 4. Proxy Setup in Vite

### The Problem with CORS in Development

While CORS solves the cross-origin problem, there is a cleaner approach for development: using a **proxy**. A proxy tells your development server: "Whenever you receive a request to `/api/...`, forward it to `http://localhost:5000`."

This means your React code no longer needs to specify the full backend URL. Instead of writing `fetch("http://localhost:5000/api/products")`, you simply write `fetch("/api/products")`.

> Think of a proxy as a **personal assistant**. Instead of you (React) walking across town to deliver a letter to the post office (Express server) yourself, you hand the letter to your assistant (Vite proxy). The assistant takes the letter, delivers it on your behalf, collects the reply, and brings it back to you. From your perspective, it feels like the post office is right next door.

### Configuring the Proxy in Vite

Open (or create) the `vite.config.js` file in your React project:

```javascript
// client/vite.config.js
import { defineConfig } from "vite";
import react from "@vitejs/plugin-react";

export default defineConfig({
  plugins: [react()],
  server: {
    proxy: {
      // Any request starting with /api will be forwarded to the Express server
      "/api": {
        target: "http://localhost:5000",
        changeOrigin: true,
        secure: false,
      },
    },
  },
});
```

### How the Proxy Works

```
  WITHOUT PROXY (Cross-Origin Request)

  Browser (localhost:5173)                      Express (localhost:5000)
  +---------------------+                      +---------------------+
  | React App           |   CORS required!     | API Server          |
  |                     | -------------------> |                     |
  | fetch("http://      |                      |                     |
  |  localhost:5000      |                      |                     |
  |  /api/products")    |                      |                     |
  +---------------------+                      +---------------------+
  Different origins --> Browser blocks unless CORS headers are present.


  WITH PROXY (Same-Origin Request)

  Browser (localhost:5173)       Vite Dev Server             Express (localhost:5000)
  +---------------------+      +------------------+         +---------------------+
  | React App           |      | Proxy            |         | API Server          |
  |                     | ---> |                  | ------> |                     |
  | fetch("/api/        |      | Forwards /api/*  |         |                     |
  |  products")         |      | to localhost:5000|         |                     |
  |                     | <--- |                  | <------ |                     |
  +---------------------+      +------------------+         +---------------------+
  Same origin --> No CORS needed. Browser is happy.
```

### Why Proxy is Better in Development

| Aspect                   | CORS                                     | Proxy                                   |
|--------------------------|------------------------------------------|------------------------------------------|
| **Frontend code**        | Must use full URL with port               | Uses relative paths (`/api/...`)         |
| **Backend configuration**| Must install and configure `cors` package | No CORS configuration needed             |
| **Security risk**        | Opens backend to cross-origin requests    | No cross-origin exposure                 |
| **Production similarity**| Different behavior in production          | Mimics production (same-origin serving)  |
| **Setup location**       | Backend (`server/index.js`)               | Frontend (`vite.config.js`)              |

### Updated React Code with Proxy

With the proxy configured, the only change in your React component is the URL:

```jsx
// BEFORE (without proxy — full URL required)
fetch("http://localhost:5000/api/products")

// AFTER (with proxy — relative path)
fetch("/api/products")
```

The Vite dev server intercepts requests to `/api/...` and forwards them to `http://localhost:5000` behind the scenes. Your React code no longer needs to know the backend's port number.

**Important:** The proxy only works during development (when using `npm run dev`). In production, you will either serve the React build from Express directly or configure a reverse proxy like Nginx. We will cover deployment in later weeks.

---

## 5. Using Axios vs Fetch for API Calls

When making HTTP requests from React, you have two main options: the built-in **Fetch API** or the third-party library **Axios**. Both accomplish the same goal — sending HTTP requests — but they differ in syntax, features, and error handling.

### The Tool Analogy

> Imagine you need to tighten a bolt. **Fetch** is like a basic wrench — it comes in the toolbox (browser), does the job, but requires some manual adjustment. **Axios** is like a torque wrench — you need to buy it separately, but it has a comfortable grip, auto-calibrates, and provides precise feedback. Both tighten the bolt, but one offers more convenience out of the box.

### Comparison Table

| Feature                  | Fetch (Built-in)                           | Axios (Third-party)                        |
|--------------------------|--------------------------------------------|--------------------------------------------|
| **Installation**         | None (built into browsers)                 | `npm install axios`                        |
| **JSON parsing**         | Manual (`.json()` method required)         | Automatic (response data is already parsed)|
| **Error handling**       | Only rejects on network failure            | Rejects on any non-2xx status code         |
| **Request cancellation** | AbortController                            | Built-in CancelToken or AbortController    |
| **Interceptors**         | Not available                              | Built-in request/response interceptors     |
| **Timeout**              | Manual with AbortController                | Built-in `timeout` option                  |
| **Progress tracking**    | Not built-in                               | Built-in upload/download progress          |
| **Browser support**      | Modern browsers (IE not supported)         | All browsers (includes polyfills)          |
| **Request body**         | Must `JSON.stringify()` manually           | Automatically serializes objects to JSON   |
| **Base URL**             | Must repeat full URL each time             | Configurable with `axios.create()`         |

### Installing Axios

```bash
npm install axios
```

### GET Request — Side by Side

**Using Fetch:**

```javascript
// GET request with Fetch
async function getProducts() {
  try {
    const response = await fetch("/api/products");

    // Fetch does NOT throw on 404 or 500 errors!
    // You must check response.ok manually.
    if (!response.ok) {
      throw new Error(`HTTP error! Status: ${response.status}`);
    }

    // You must manually parse the JSON
    const data = await response.json();
    return data;
  } catch (error) {
    console.error("Failed to fetch products:", error);
    throw error;
  }
}
```

**Using Axios:**

```javascript
// GET request with Axios
import axios from "axios";

async function getProducts() {
  try {
    // Axios automatically parses JSON and throws on non-2xx status
    const response = await axios.get("/api/products");
    return response.data; // Data is already parsed
  } catch (error) {
    // Axios provides detailed error information
    if (error.response) {
      // Server responded with a non-2xx status
      console.error("Server error:", error.response.status);
      console.error("Error data:", error.response.data);
    } else if (error.request) {
      // Request was made but no response received
      console.error("No response from server");
    } else {
      // Something went wrong setting up the request
      console.error("Request setup error:", error.message);
    }
    throw error;
  }
}
```

### POST Request — Side by Side

**Using Fetch:**

```javascript
// POST request with Fetch
async function createProduct(productData) {
  try {
    const response = await fetch("/api/products", {
      method: "POST",
      headers: {
        "Content-Type": "application/json", // Must set manually
      },
      body: JSON.stringify(productData), // Must stringify manually
    });

    if (!response.ok) {
      throw new Error(`HTTP error! Status: ${response.status}`);
    }

    const newProduct = await response.json(); // Must parse manually
    return newProduct;
  } catch (error) {
    console.error("Failed to create product:", error);
    throw error;
  }
}
```

**Using Axios:**

```javascript
// POST request with Axios
import axios from "axios";

async function createProduct(productData) {
  try {
    // Axios automatically:
    // - Sets Content-Type to application/json
    // - Stringifies the object
    // - Parses the response JSON
    const response = await axios.post("/api/products", productData);
    return response.data;
  } catch (error) {
    console.error("Failed to create product:", error.response?.data);
    throw error;
  }
}
```

### Creating an Axios Instance (Best Practice)

For larger applications, create a pre-configured Axios instance with a base URL and interceptors:

```javascript
// client/src/api/axiosClient.js
import axios from "axios";

const api = axios.create({
  baseURL: "/api",           // All requests will start with /api
  timeout: 10000,            // Timeout after 10 seconds
  headers: {
    "Content-Type": "application/json",
  },
});

// Request interceptor — attach auth token to every request
api.interceptors.request.use((config) => {
  const token = localStorage.getItem("token");
  if (token) {
    config.headers.Authorization = `Bearer ${token}`;
  }
  return config;
});

// Response interceptor — handle 401 errors globally
api.interceptors.response.use(
  (response) => response,
  (error) => {
    if (error.response?.status === 401) {
      window.location.href = "/login"; // Redirect on token expiry
    }
    return Promise.reject(error);
  }
);

export default api;
```

Using the instance:

```javascript
import api from "../api/axiosClient";

const products = await api.get("/products");             // GET
const newProduct = await api.post("/products", { name: "Mouse", price: 29.99 }); // POST
await api.put("/products/1", { price: 24.99 });          // PUT
await api.delete("/products/1");                          // DELETE
```

### When to Use Which

- **Use Fetch** when you want zero dependencies, are making simple requests, or are building a lightweight application.
- **Use Axios** when your application makes many API calls, you need interceptors (for authentication), you want automatic error handling, or you prefer cleaner syntax.

For the rest of this course, we will use **Axios** because it reduces boilerplate and provides better error handling for production-grade applications.

---

## 6. Folder Structure for Full-Stack Projects

A well-organized folder structure is essential for maintaining and scaling a full-stack application. The most common approach is to keep the frontend and backend in **separate directories** within a single repository.

### The Factory Analogy

> Imagine a **factory**. The factory has two main sections: the **showroom** (where customers browse products — the frontend) and the **manufacturing floor** (where products are built — the backend). Each section has its own manager, its own team, and its own processes. But they exist within the same building (repository) and coordinate with each other through internal communication channels (API calls).

### Recommended Folder Structure

```
  my-mern-app/
  +-- client/                          # React Frontend
  |   +-- public/                      # Static assets (favicon, etc.)
  |   +-- src/
  |   |   +-- api/                     # API client (Axios instance)
  |   |   |   +-- axiosClient.js
  |   |   +-- components/              # Reusable UI components
  |   |   |   +-- Header.jsx
  |   |   |   +-- Footer.jsx
  |   |   |   +-- ProductCard.jsx
  |   |   +-- pages/                   # Page-level components
  |   |   |   +-- HomePage.jsx
  |   |   |   +-- ProductPage.jsx
  |   |   |   +-- LoginPage.jsx
  |   |   +-- hooks/                   # Custom React hooks
  |   |   |   +-- useProducts.js
  |   |   |   +-- useAuth.js
  |   |   +-- context/                 # React Context providers
  |   |   |   +-- AuthContext.jsx
  |   |   +-- utils/                   # Utility/helper functions
  |   |   |   +-- formatPrice.js
  |   |   +-- App.jsx                  # Root component
  |   |   +-- main.jsx                 # Entry point
  |   +-- .env                         # Frontend environment variables
  |   +-- vite.config.js               # Vite configuration (proxy, etc.)
  |   +-- package.json                 # Frontend dependencies
  |
  +-- server/                          # Express Backend
  |   +-- config/                      # Configuration files
  |   |   +-- db.js                    # MongoDB connection
  |   |   +-- cors.js                  # CORS configuration
  |   +-- controllers/                 # Route handler logic
  |   |   +-- productController.js
  |   |   +-- userController.js
  |   +-- models/                      # Mongoose schemas/models
  |   |   +-- Product.js
  |   |   +-- User.js
  |   +-- routes/                      # Express route definitions
  |   |   +-- productRoutes.js
  |   |   +-- userRoutes.js
  |   +-- middleware/                   # Custom middleware
  |   |   +-- auth.js
  |   |   +-- errorHandler.js
  |   +-- utils/                       # Backend utility functions
  |   |   +-- generateToken.js
  |   +-- index.js                     # Server entry point
  |   +-- .env                         # Backend environment variables
  |   +-- package.json                 # Backend dependencies
  |
  +-- .gitignore                       # Git ignore rules
  +-- package.json                     # Root package.json (scripts)
  +-- README.md                        # Project documentation
```

### Purpose of Each Directory

| Directory               | Purpose                                                    |
|--------------------------|------------------------------------------------------------|
| `client/src/api/`       | Centralized API configuration (Axios instance, endpoints)  |
| `client/src/components/`| Reusable UI building blocks (buttons, cards, forms)        |
| `client/src/pages/`     | Full page components (each mapped to a route)              |
| `client/src/hooks/`     | Custom hooks for shared logic (data fetching, auth)        |
| `client/src/context/`   | Global state management using React Context                |
| `server/config/`        | Database connection, CORS settings, app configuration      |
| `server/controllers/`   | Business logic for handling requests                       |
| `server/models/`        | Mongoose schemas defining data structure                   |
| `server/routes/`        | URL path definitions that map to controllers               |
| `server/middleware/`    | Functions that process requests before they reach routes    |

### Root package.json with Scripts

The root `package.json` provides convenient scripts to run both the client and server simultaneously:

```json
{
  "name": "my-mern-app",
  "version": "1.0.0",
  "private": true,
  "scripts": {
    "client": "cd client && npm run dev",
    "server": "cd server && npm run dev",
    "dev": "concurrently \"npm run server\" \"npm run client\"",
    "install-all": "npm install && cd client && npm install && cd ../server && npm install",
    "build": "cd client && npm run build",
    "start": "cd server && node index.js"
  },
  "devDependencies": {
    "concurrently": "^8.2.0"
  }
}
```

### Understanding the Scripts

| Script         | What It Does                                                   |
|----------------|----------------------------------------------------------------|
| `npm run client` | Starts the React development server (Vite)                  |
| `npm run server` | Starts the Express server with nodemon                       |
| `npm run dev`    | Starts both client and server simultaneously                 |
| `npm run install-all` | Installs dependencies for root, client, and server      |
| `npm run build`  | Creates a production build of the React app                  |
| `npm start`      | Runs the Express server in production mode                   |

Install `concurrently` to run both servers at once:

```bash
npm install concurrently --save-dev
```

Now a single command — `npm run dev` — starts both your React frontend and Express backend, making development seamless.

---

## 7. Environment Variables for Frontend

Environment variables let you store configuration values (API URLs, API keys, feature flags) outside of your source code. This is critical for security and flexibility — you can change settings without modifying code, and you can use different values for development and production.

### The ID Badge Analogy

> In a company, every employee wears an **ID badge**. Regular employees have badges that show their name and department (public information). But some employees have **security clearance badges** that grant access to restricted areas (sensitive information). In Vite, the `VITE_` prefix works like a security clearance badge — only variables with this prefix are "cleared" to be visible to the frontend. Variables without the prefix remain hidden on the server side, just like restricted areas remain off-limits to regular badge holders.

### Creating a .env File

Create a `.env` file in the root of your **client** directory:

```bash
# client/.env

# Variables WITH the VITE_ prefix — accessible in React code
VITE_API_URL=http://localhost:5000/api
VITE_APP_NAME=My MERN Store
VITE_ENABLE_ANALYTICS=false

# Variables WITHOUT the VITE_ prefix — NOT accessible in React code
# These are only available to the Vite build process itself
DB_PASSWORD=super_secret_123
SECRET_API_KEY=sk-abc123xyz
```

### Why the VITE_ Prefix is Required

This is a **security feature**, not an inconvenience. Here is why:

When Vite builds your React application, it takes your JavaScript code and bundles it into static files that are served to the browser. **Everything in the browser bundle is visible to anyone who opens DevTools.** If Vite automatically included all environment variables, your database password, API secret keys, and other sensitive values would be exposed to every user who visits your site.

The `VITE_` prefix acts as an explicit opt-in. You are telling Vite: "Yes, I understand this value will be visible in the browser, and I am okay with that."

```
  ENVIRONMENT VARIABLE SECURITY

  .env file
  +-----------------------------------------+
  | VITE_API_URL=http://localhost:5000       |  --> Included in browser bundle (public)
  | VITE_APP_NAME=My Store                   |  --> Included in browser bundle (public)
  | DB_PASSWORD=secret123                    |  --> NOT included (stays on server)
  | JWT_SECRET=my-jwt-key                    |  --> NOT included (stays on server)
  +-----------------------------------------+

  After Vite Build:
  +---------------------+                +---------------------+
  | Browser Bundle      |                | Server Only         |
  | (VISIBLE to users)  |                | (HIDDEN from users) |
  |                     |                |                     |
  | VITE_API_URL  ✓     |                | DB_PASSWORD    ✓    |
  | VITE_APP_NAME ✓     |                | JWT_SECRET     ✓    |
  +---------------------+                +---------------------+
```

### Accessing Environment Variables in React

Use `import.meta.env` to access environment variables in your React code:

```jsx
// client/src/components/App.jsx

function App() {
  // Access environment variables with import.meta.env
  const apiUrl = import.meta.env.VITE_API_URL;
  const appName = import.meta.env.VITE_APP_NAME;
  const isDev = import.meta.env.DEV;  // Built-in: true in development

  console.log("API URL:", apiUrl);      // "http://localhost:5000/api"
  console.log("App Name:", appName);    // "My MERN Store"
  console.log("Dev Mode:", isDev);      // true (during development)

  return (
    <div>
      <h1>{appName}</h1>
      {isDev && <p>Running in development mode</p>}
    </div>
  );
}

export default App;
```

### Using Environment Variables in API Configuration

```javascript
// client/src/api/axiosClient.js
import axios from "axios";

const api = axios.create({
  baseURL: import.meta.env.VITE_API_URL || "/api",
  timeout: 10000,
});

export default api;
```

### The .env.example Pattern

Never commit your `.env` file to Git (it may contain sensitive values). Instead, create a `.env.example` file that shows what variables are expected, without the actual values:

```bash
# client/.env.example
# Copy this file to .env and fill in your values

VITE_API_URL=http://localhost:5000/api
VITE_APP_NAME=Your App Name
VITE_ENABLE_ANALYTICS=false
```

Add `.env` to your `.gitignore`:

```bash
# .gitignore
.env
.env.local
.env.*.local
```

This way, a new developer joining the project can see exactly which environment variables are needed by looking at `.env.example`, then create their own `.env` with the appropriate values.

### Multiple Environment Files

Vite supports different `.env` files for different environments:

| File              | When It's Loaded                              | Priority    |
|-------------------|-----------------------------------------------|-------------|
| `.env`            | Always loaded                                 | Lowest      |
| `.env.local`      | Always loaded, ignored by Git                 | Above `.env`|
| `.env.development`| Only during `npm run dev`                     | Higher      |
| `.env.production` | Only during `npm run build`                   | Higher      |
| `.env.development.local` | Dev only, ignored by Git              | Highest     |
| `.env.production.local`  | Build only, ignored by Git             | Highest     |

```bash
# client/.env.development
VITE_API_URL=http://localhost:5000/api

# client/.env.production
VITE_API_URL=https://myapp.com/api
```

This means you can use `http://localhost:5000` during development and your production URL during builds, without changing any code.

---

## 8. Building a Complete Data Flow Diagram

Now that you understand each piece of the MERN stack, let us trace the complete journey of data through the entire application. We will follow a real example: a user creating a new blog post.

### The Assembly Line Analogy

> Picture a **factory assembly line**. A customer (user) walks into the showroom (React) and fills out an order form (form submission). The form is handed to a delivery driver (Axios/Fetch) who carries it to the receiving dock (Express Router). The dock worker checks the paperwork (middleware) and passes it to the assembly team (Controller). The assembly team reads the blueprint (Mongoose Model), gathers materials from the warehouse (MongoDB), builds the product, and sends the finished item back along the same path to the customer.

### The Complete Data Flow

```
  COMPLETE MERN DATA FLOW — Creating a Blog Post

  +--------+    +----------------+    +-----------+    +--------+    +------------+    +---------+    +---------+
  |        |    |                |    |           |    |        |    |            |    |         |    |         |
  |  USER  |--->| React          |--->| Axios/    |--->| Express|--->| Controller |--->| Mongoose|--->| MongoDB |
  |        |    | Component      |    | Fetch     |    | Router |    |            |    | Model   |    |         |
  |        |    |                |    |           |    |        |    |            |    |         |    |         |
  +--------+    +----------------+    +-----------+    +--------+    +------------+    +---------+    +---------+
      ^                                                                                                   |
      |                                                                                                   |
      +---------------------------------------------------------------------------------------------------+
                                        Response flows back the same path
```

### Walking Through Each Step

Let us trace the exact journey of data when a user creates a blog post:

#### Step 1: User Fills Out the Form (React Component)

The user types a title and content into a form in the browser.

```jsx
// client/src/pages/CreatePost.jsx
import { useState } from "react";
import api from "../api/axiosClient";

function CreatePost() {
  const [title, setTitle] = useState("");
  const [content, setContent] = useState("");
  const [message, setMessage] = useState("");

  const handleSubmit = async (e) => {
    e.preventDefault();

    try {
      // Step 2: Send data to the backend
      const response = await api.post("/posts", {
        title: title,
        content: content,
      });

      setMessage(`Post created: ${response.data.title}`);
      setTitle("");
      setContent("");
    } catch (error) {
      setMessage(`Error: ${error.response?.data?.message || "Server error"}`);
    }
  };

  return (
    <form onSubmit={handleSubmit}>
      <h1>Create New Blog Post</h1>
      <input
        type="text"
        placeholder="Post title"
        value={title}
        onChange={(e) => setTitle(e.target.value)}
        required
      />
      <textarea
        placeholder="Write your post..."
        value={content}
        onChange={(e) => setContent(e.target.value)}
        required
      />
      <button type="submit">Publish</button>
      {message && <p>{message}</p>}
    </form>
  );
}

export default CreatePost;
```

#### Step 2: Axios Sends the HTTP Request

When `api.post("/posts", { title, content })` is called, Axios:

1. Serializes the JavaScript object into a JSON string.
2. Sets the `Content-Type` header to `application/json`.
3. Sends a POST request to `/api/posts` (the baseURL from our Axios instance adds the `/api` prefix).
4. The Vite proxy forwards this request from `localhost:5173` to `localhost:5000`.

```
  REQUEST BEING SENT

  POST /api/posts HTTP/1.1
  Host: localhost:5000
  Content-Type: application/json

  {
    "title": "My First Blog Post",
    "content": "This is the content of my first post..."
  }
```

#### Step 3: Express Router Receives the Request

The Express router matches the URL path and HTTP method to the correct route handler.

```javascript
// server/routes/postRoutes.js
const express = require("express");
const router = express.Router();
const postController = require("../controllers/postController");

router.get("/", postController.getAllPosts);       // GET /api/posts
router.get("/:id", postController.getPostById);    // GET /api/posts/:id
router.post("/", postController.createPost);       // POST /api/posts  <-- This one matches
router.put("/:id", postController.updatePost);     // PUT /api/posts/:id
router.delete("/:id", postController.deletePost);  // DELETE /api/posts/:id

module.exports = router;
```

```javascript
// server/index.js
const express = require("express");
const connectDB = require("./config/db");
const postRoutes = require("./routes/postRoutes");

const app = express();

connectDB(); // Connect to MongoDB

app.use(express.json()); // Parse JSON request bodies
app.use("/api/posts", postRoutes); // Mount post routes

app.listen(5000, () => console.log("Server running on port 5000"));
```

#### Step 4: Controller Processes the Request

The controller contains the business logic. It validates the incoming data, creates a new document using the Mongoose model, and sends the response.

```javascript
// server/controllers/postController.js
const Post = require("../models/Post");

const createPost = async (req, res) => {
  try {
    // Extract data from the request body
    const { title, content } = req.body;

    // Validate input
    if (!title || !content) {
      return res.status(400).json({ message: "Title and content are required" });
    }

    // Step 5: Create a new post using the Mongoose model
    const newPost = await Post.create({
      title: title,
      content: content,
    });

    // Step 7: Send the created post back to the client
    res.status(201).json(newPost);
  } catch (error) {
    res.status(500).json({ message: "Server error", error: error.message });
  }
};

module.exports = { createPost };
```

#### Step 5: Mongoose Model Validates and Structures the Data

The Mongoose model defines the schema — what fields are allowed, their types, and validation rules. When `Post.create()` is called, Mongoose validates the data against the schema before saving it.

```javascript
// server/models/Post.js
const mongoose = require("mongoose");

const postSchema = new mongoose.Schema(
  {
    title: {
      type: String,
      required: [true, "Title is required"],
      trim: true,
      maxlength: [200, "Title cannot exceed 200 characters"],
    },
    content: {
      type: String,
      required: [true, "Content is required"],
    },
  },
  {
    timestamps: true, // Adds createdAt and updatedAt fields automatically
  }
);

module.exports = mongoose.model("Post", postSchema);
```

#### Step 6: MongoDB Stores the Document

Mongoose converts the validated data into a MongoDB document and saves it to the `posts` collection. MongoDB assigns a unique `_id` and returns the saved document.

```
  DOCUMENT STORED IN MONGODB

  posts collection:
  +-------------------------------------------------------------------+
  | {                                                                  |
  |   "_id": "64f1a2b3c4d5e6f7a8b9c0d1",                             |
  |   "title": "My First Blog Post",                                  |
  |   "content": "This is the content of my first post...",           |
  |   "createdAt": "2024-09-01T10:30:00.000Z",                       |
  |   "updatedAt": "2024-09-01T10:30:00.000Z",                       |
  |   "__v": 0                                                        |
  | }                                                                  |
  +-------------------------------------------------------------------+
```

#### Step 7: Response Flows Back

The saved document travels back through each layer:

```
  RESPONSE JOURNEY

  MongoDB                Mongoose              Controller           Express              Axios               React
  +--------+            +---------+           +------------+       +--------+           +----------+        +----------+
  | Saved  |  Document  | Returns |  JS Object| Calls      | JSON  | Sends  |  HTTP     | Parses   | State  | Re-renders|
  | docu-  |---------->| the     |---------->| res.json() |------>| HTTP   |---------->| JSON to  |------->| with new |
  | ment   |           | saved   |           | with the   |       | response|          | JS object|        | data     |
  +--------+            | doc     |           | document   |       +--------+           +----------+        +----------+
                        +---------+           +------------+
```

### The Complete Expanded Diagram

```
  FULL MERN STACK DATA FLOW — Detailed View

  +====================+
  |       USER         |
  |  Fills out form    |
  |  and clicks Submit |
  +==========|=========+
             |
             v
  +====================+
  |   REACT COMPONENT  |
  |                    |
  |  handleSubmit()    |
  |  calls api.post()  |
  +==========|=========+
             |
             v
  +====================+
  |   AXIOS / FETCH    |
  |                    |
  |  Serializes data   |
  |  Sets headers      |
  |  Sends HTTP POST   |
  +==========|=========+
             |
             | HTTP POST /api/posts
             | { "title": "...", "content": "..." }
             |
             v
  +====================+
  |   VITE PROXY       |
  |  (dev only)        |
  |                    |
  |  Forwards /api/*   |
  |  to localhost:5000 |
  +==========|=========+
             |
             v
  +====================+
  |   EXPRESS ROUTER   |
  |                    |
  |  Matches POST      |
  |  /api/posts to     |
  |  createPost()      |
  +==========|=========+
             |
             v
  +====================+
  |   MIDDLEWARE        |
  |                    |
  |  express.json()    |
  |  parses body       |
  |  Auth checks (if   |
  |  applicable)       |
  +==========|=========+
             |
             v
  +====================+
  |   CONTROLLER       |
  |                    |
  |  Validates input   |
  |  Calls Post.create |
  +==========|=========+
             |
             v
  +====================+
  |   MONGOOSE MODEL   |
  |                    |
  |  Validates against |
  |  schema            |
  |  Converts to BSON  |
  +==========|=========+
             |
             v
  +====================+
  |   MONGODB          |
  |                    |
  |  Stores document   |
  |  in posts          |
  |  collection        |
  |  Returns saved doc |
  +==========|=========+
             |
             | (Response flows back up through each layer)
             |
             v
  +====================+
  |   REACT RE-RENDER  |
  |                    |
  |  setState updates  |
  |  UI reflects the   |
  |  new blog post     |
  +====================+
```

### MongoDB Connection Configuration

For completeness, here is the database connection file referenced in the server setup:

```javascript
// server/config/db.js
const mongoose = require("mongoose");

const connectDB = async () => {
  try {
    const conn = await mongoose.connect(process.env.MONGO_URI);
    console.log(`MongoDB connected: ${conn.connection.host}`);
  } catch (error) {
    console.error(`Database connection error: ${error.message}`);
    process.exit(1);
  }
};

module.exports = connectDB;
```

```bash
# server/.env
MONGO_URI=mongodb://localhost:27017/mern-blog
PORT=5000
JWT_SECRET=your-secret-key-here
```

This complete data flow — from user interaction to database storage and back — is the foundation of every MERN application. Whether you are building a blog, an e-commerce platform, or a social network, the data always follows this same path. Understanding each step ensures you can debug issues at any point in the chain.

---

## 9. Summary

Here is a recap of everything covered in this week:

- **Full-stack development** means building both the frontend (React) and backend (Express + MongoDB) and connecting them through HTTP requests.

- **The MERN stack** consists of MongoDB, Express, React, and Node.js — four technologies that work together to deliver complete web applications.

- **React connects to Express** by making HTTP requests (GET, POST, PUT, DELETE) to API endpoints using `fetch()` or `axios`.

- **CORS (Cross-Origin Resource Sharing)** is a browser security mechanism that blocks requests between different origins. The `cors` middleware in Express allows you to explicitly permit cross-origin requests from your React application.

- **Vite proxy** is the preferred development solution — it forwards API requests from the React dev server to Express, avoiding CORS entirely. Configure it in `vite.config.js` under `server.proxy`.

- **Axios** offers advantages over the built-in Fetch API: automatic JSON parsing, better error handling (throws on non-2xx responses), request/response interceptors, and configurable instances with `axios.create()`.

- **Folder structure** matters. Separate your project into `client/` and `server/` directories, each with their own `package.json`. Use a root `package.json` with `concurrently` to run both in development.

- **Environment variables** in Vite require the `VITE_` prefix to be accessible in the browser. This is a security feature — it prevents sensitive values from being bundled into the frontend code. Use `.env.example` to document required variables without committing actual values.

- **Data flows** through a predictable path: User interaction triggers a React event handler, which sends an HTTP request through Axios, which reaches the Express router, passes through middleware, hits the controller, interacts with a Mongoose model, and ultimately reads from or writes to MongoDB. The response travels back through the same layers.

### What is Coming Next

In **Week 33**, you will learn about **Authentication in MERN** — implementing user registration, login, JSON Web Tokens (JWT), protected routes on both the frontend and backend, and managing authenticated sessions across the full stack.

---

> **Pro Tip:** During development, always start your Express server before your React dev server. If the backend is not running when React tries to make an API call, you will see confusing network errors. Use `concurrently` in your root `package.json` to start both with a single command and avoid this issue.
