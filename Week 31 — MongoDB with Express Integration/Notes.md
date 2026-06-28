# Week 31 — MongoDB with Express Integration

> **Prerequisites:** Week 28-30 (MongoDB Basics, Mongoose ODM, Advanced Queries & Relations)
> **Goal:** Learn how to integrate MongoDB into an Express application using the MVC architecture, build a complete CRUD API with robust error handling, seed data scripts, and aggregation-powered analytics endpoints.

---

## Table of Contents

1. [Connecting MongoDB to Express](#1-connecting-mongodb-to-express)
2. [Environment-Based Configuration](#2-environment-based-configuration)
3. [MVC Project Structure](#3-mvc-project-structure)
4. [Creating Models](#4-creating-models)
5. [Creating Controllers](#5-creating-controllers)
6. [Creating Routes](#6-creating-routes)
7. [Complete CRUD API with MongoDB](#7-complete-crud-api-with-mongodb)
8. [Error Handling](#8-error-handling)
9. [Data Seeding Scripts](#9-data-seeding-scripts)
10. [Aggregation Practical Examples](#10-aggregation-practical-examples)
11. [Week 31 Project: Full CRUD API with MongoDB Backend](#11-week-31-project-full-crud-api-with-mongodb-backend)
12. [Database Phase Summary](#12-database-phase-summary)

---

## 1. Connecting MongoDB to Express

> Think of connecting MongoDB to Express like dialing a phone number. You need the correct number (connection string), a working phone line (network), and someone to pick up on the other end (the MongoDB server). If any part fails, the call does not go through and you get an error tone instead of a conversation.

### The Connection String

MongoDB connection strings follow a standard URI format:

```javascript
// Local MongoDB
'mongodb://localhost:27017/myDatabase'

// MongoDB Atlas (cloud)
'mongodb+srv://username:password@cluster0.abc123.mongodb.net/myDatabase?retryWrites=true&w=majority'
```

### Basic Connection with Mongoose

```javascript
const mongoose = require('mongoose');

// Connect to MongoDB using async/await
const connectDB = async () => {
  try {
    const conn = await mongoose.connect('mongodb://localhost:27017/myapp', {
      // Connection options (Mongoose 7+ has sensible defaults)
    });

    console.log(`MongoDB Connected: ${conn.connection.host}`);
  } catch (error) {
    console.error(`Error: ${error.message}`);
    process.exit(1); // Exit process with failure code
  }
};

connectDB();
```

### Connection Options Explained

| Option | Description | Default |
|--------|-------------|---------|
| `serverSelectionTimeoutMS` | How long to wait for server selection | 30000ms |
| `heartbeatFrequencyMS` | How often to check server status | 10000ms |
| `socketTimeoutMS` | How long to wait for socket operations | 0 (no timeout) |
| `maxPoolSize` | Maximum number of connections in the pool | 100 |
| `minPoolSize` | Minimum number of connections in the pool | 0 |
| `retryWrites` | Automatically retry failed write operations | true |

### Connection Events

Mongoose emits events throughout the connection lifecycle. Listening to these events helps you monitor the health of your database connection in real time.

```javascript
const mongoose = require('mongoose');

// ---- Connection Event Listeners ----

// Fires once when the initial connection is established
mongoose.connection.on('connected', () => {
  console.log('Mongoose connected to the database');
});

// Fires when an error occurs on the connection
mongoose.connection.on('error', (err) => {
  console.error(`Mongoose connection error: ${err.message}`);
});

// Fires when the connection is lost
mongoose.connection.on('disconnected', () => {
  console.log('Mongoose disconnected from the database');
});

// Fires when the connection is successfully reopened
mongoose.connection.on('reconnected', () => {
  console.log('Mongoose reconnected to the database');
});

// Graceful shutdown: close connection when the app terminates
process.on('SIGINT', async () => {
  await mongoose.connection.close();
  console.log('Mongoose connection closed due to app termination');
  process.exit(0);
});
```

### Connection Flow Diagram

```
+-------------------+       Connection String        +-------------------+
|                   | -----------------------------> |                   |
|   Express App     |       mongoose.connect()       |   MongoDB Server  |
|                   | <----------------------------- |                   |
+-------------------+       Connected / Error        +-------------------+
        |                                                     |
        v                                                     v
+-------------------+                                +-------------------+
| Event: connected  |                                |  Database Ready   |
| Event: error      |                                |  Collections      |
| Event: disconnected|                               |  Documents        |
+-------------------+                                +-------------------+
```

---

## 2. Environment-Based Configuration

> Think of environment variables like secret instructions in a sealed envelope. The instructions change depending on who opens the envelope: a developer gets local database URLs, while the production server gets the real cloud database URL. The code itself never changes; only the envelope contents do.

### Why Never Hardcode Credentials

Hardcoding database credentials directly in your source code creates serious problems:

- **Security risk:** Anyone with access to the code sees your passwords
- **Inflexibility:** You must change and redeploy code for every environment
- **Version control danger:** Credentials get committed to Git history permanently
- **Team friction:** Every developer needs different local settings

### Setting Up dotenv

```bash
npm install dotenv
```

### The .env File

Create a `.env` file in the root of your project:

```
# Server Configuration
PORT=5000
NODE_ENV=development

# MongoDB Configuration (Development)
MONGO_URI=mongodb://localhost:27017/myapp_dev

# MongoDB Configuration (Production) — use this on your server
# MONGO_URI=mongodb+srv://admin:secretPass@cluster0.abc123.mongodb.net/myapp_prod?retryWrites=true&w=majority

# JWT Secret (for authentication later)
JWT_SECRET=your_jwt_secret_here_change_in_production
JWT_EXPIRE=30d
```

### Loading Environment Variables

At the very top of your entry file (server.js), load dotenv before anything else:

```javascript
// server.js — load environment variables FIRST
const dotenv = require('dotenv');
dotenv.config(); // Reads .env file and loads variables into process.env

// Now process.env.MONGO_URI, process.env.PORT, etc. are available
console.log(process.env.NODE_ENV); // "development"
```

### The config/db.js Module Pattern

Isolate database connection logic into its own module:

```javascript
// config/db.js
const mongoose = require('mongoose');

const connectDB = async () => {
  try {
    const conn = await mongoose.connect(process.env.MONGO_URI);

    console.log(`MongoDB Connected: ${conn.connection.host}`);
  } catch (error) {
    console.error(`Database connection failed: ${error.message}`);
    process.exit(1);
  }
};

module.exports = connectDB;
```

Then use it in server.js:

```javascript
// server.js
const dotenv = require('dotenv');
dotenv.config();

const connectDB = require('./config/db');

// Connect to database
connectDB();
```

### Development vs Production URLs

| Environment | MONGO_URI | Purpose |
|-------------|-----------|---------|
| Development | `mongodb://localhost:27017/myapp_dev` | Local testing with throwaway data |
| Testing | `mongodb://localhost:27017/myapp_test` | Automated tests with isolated data |
| Production | `mongodb+srv://user:pass@cluster.mongodb.net/myapp` | Live user data on Atlas |

### Environment Flow Diagram

```
+----------+       dotenv.config()       +------------------+
|  .env    | --------------------------> | process.env      |
|  file    |    Reads key=value pairs    | (Node.js global) |
+----------+                             +------------------+
                                                  |
                     +----------------------------+----------------------------+
                     |                            |                            |
                     v                            v                            v
            +----------------+          +------------------+         +------------------+
            | process.env    |          | process.env      |         | process.env      |
            | .MONGO_URI     |          | .PORT            |         | .NODE_ENV        |
            +----------------+          +------------------+         +------------------+
                     |                            |                            |
                     v                            v                            v
            +----------------+          +------------------+         +------------------+
            | config/db.js   |          | server.js        |         | Error handler    |
            | connects to DB |          | listens on port  |         | dev vs prod mode |
            +----------------+          +------------------+         +------------------+
```

### Add .env to .gitignore

Never commit your `.env` file. Add it to `.gitignore` immediately:

```
# .gitignore
node_modules/
.env
```

Create a `.env.example` file to show teammates which variables are needed:

```
PORT=5000
NODE_ENV=development
MONGO_URI=mongodb://localhost:27017/your_database_name
JWT_SECRET=your_secret_here
```

---

## 3. MVC Project Structure

> Think of MVC like a restaurant. The **Model** is the kitchen, where ingredients (data) are stored, prepared, and validated. The **View** is the menu that the customer sees (in APIs, this is the JSON response). The **Controller** is the waiter who takes orders from customers, relays them to the kitchen, and delivers the prepared food back. Each role has a clear responsibility, and swapping one part does not break the others.

### Project Folder Structure

```
project/
  +-- config/
  |     +-- db.js                  # Database connection logic
  +-- controllers/
  |     +-- userController.js      # User request handlers
  |     +-- productController.js   # Product request handlers
  +-- middleware/
  |     +-- errorHandler.js        # Global error handling middleware
  |     +-- asyncHandler.js        # Async/await wrapper utility
  +-- models/
  |     +-- User.js                # User schema and model
  |     +-- Product.js             # Product schema and model
  +-- routes/
  |     +-- userRoutes.js          # User endpoint definitions
  |     +-- productRoutes.js       # Product endpoint definitions
  +-- utils/
  |     +-- AppError.js            # Custom error class
  +-- server.js                    # Application entry point
  +-- seed.js                      # Database seeding script
  +-- .env                         # Environment variables (not committed)
  +-- .env.example                 # Template for .env
  +-- .gitignore                   # Files to exclude from Git
  +-- package.json                 # Dependencies and scripts
```

### Folder Responsibilities

| Folder/File | Responsibility |
|-------------|---------------|
| `config/` | Database connection settings and external service configuration |
| `controllers/` | Business logic -- process requests, call models, format responses |
| `middleware/` | Functions that run between request and response (error handling, auth, logging) |
| `models/` | Data structure definitions, validation rules, database interaction methods |
| `routes/` | URL endpoint mapping -- connects HTTP methods and paths to controller functions |
| `utils/` | Shared helper classes and utility functions used across the application |
| `server.js` | Entry point -- initializes Express, loads middleware, mounts routes, starts server |
| `seed.js` | Populates the database with sample data for development and testing |

### MVC Request Flow

```
    Client Request (e.g., GET /api/users/123)
              |
              v
    +-------------------+
    |    server.js       |    Entry point receives the request
    |  (Express App)     |
    +-------------------+
              |
              v
    +-------------------+
    |    routes/         |    Matches URL pattern to a controller function
    | userRoutes.js      |    router.get('/:id', getUser)
    +-------------------+
              |
              v
    +-------------------+
    |   controllers/     |    Executes business logic
    | userController.js  |    Calls Model to fetch/modify data
    +-------------------+
              |
              v
    +-------------------+
    |    models/         |    Interacts with MongoDB through Mongoose
    |    User.js         |    User.findById(req.params.id)
    +-------------------+
              |
              v
    +-------------------+
    |    MongoDB         |    Stores and retrieves documents
    |   (Database)       |
    +-------------------+
              |
              v
    +-------------------+
    |   controllers/     |    Formats the data into a JSON response
    | userController.js  |    res.json({ success: true, data: user })
    +-------------------+
              |
              v
    Client Response (JSON)
```

---

## 4. Creating Models

Models define the structure, validation rules, and behavior of your data. They act as a contract between your application and the database.

### User Model

```javascript
// models/User.js
const mongoose = require('mongoose');

const userSchema = new mongoose.Schema(
  {
    name: {
      type: String,
      required: [true, 'Name is required'],   // Custom error message
      trim: true,                               // Remove leading/trailing spaces
      maxlength: [50, 'Name cannot exceed 50 characters'],
    },
    email: {
      type: String,
      required: [true, 'Email is required'],
      unique: true,                             // No two users share an email
      lowercase: true,                          // Convert to lowercase before saving
      trim: true,
      match: [
        /^[\w-\.]+@([\w-]+\.)+[\w-]{2,4}$/,    // Basic email format validation
        'Please provide a valid email address',
      ],
    },
    password: {
      type: String,
      required: [true, 'Password is required'],
      minlength: [6, 'Password must be at least 6 characters'],
      select: false,                            // Do not return password in queries by default
    },
    role: {
      type: String,
      enum: {
        values: ['user', 'admin', 'moderator'],
        message: '{VALUE} is not a valid role', // Error if value not in list
      },
      default: 'user',
    },
    isActive: {
      type: Boolean,
      default: true,
    },
  },
  {
    timestamps: true, // Adds createdAt and updatedAt automatically
  }
);

// ---- Virtual Field ----
// A virtual field is not stored in the database; it is computed on the fly
userSchema.virtual('profileUrl').get(function () {
  return `/users/${this._id}`;
});

// Ensure virtuals are included when converting to JSON
userSchema.set('toJSON', { virtuals: true });
userSchema.set('toObject', { virtuals: true });

// ---- Pre-save Middleware ----
// Runs before every save operation on this model
userSchema.pre('save', function (next) {
  // Example: log when a new user is about to be saved
  if (this.isNew) {
    console.log(`New user being created: ${this.email}`);
  }
  next();
});

module.exports = mongoose.model('User', userSchema);
```

### Product Model

```javascript
// models/Product.js
const mongoose = require('mongoose');

const productSchema = new mongoose.Schema(
  {
    name: {
      type: String,
      required: [true, 'Product name is required'],
      trim: true,
      maxlength: [100, 'Product name cannot exceed 100 characters'],
    },
    description: {
      type: String,
      required: [true, 'Product description is required'],
      maxlength: [500, 'Description cannot exceed 500 characters'],
    },
    price: {
      type: Number,
      required: [true, 'Price is required'],
      min: [0, 'Price cannot be negative'],
    },
    category: {
      type: String,
      required: [true, 'Category is required'],
      enum: {
        values: ['electronics', 'clothing', 'books', 'home', 'sports'],
        message: '{VALUE} is not a valid category',
      },
    },
    stock: {
      type: Number,
      required: [true, 'Stock quantity is required'],
      min: [0, 'Stock cannot be negative'],
      default: 0,
    },
    createdBy: {
      type: mongoose.Schema.Types.ObjectId,
      ref: 'User',       // References the User model
      required: [true, 'Creator is required'],
    },
    ratings: {
      type: Number,
      default: 0,
      min: [0, 'Rating cannot be below 0'],
      max: [5, 'Rating cannot exceed 5'],
    },
  },
  {
    timestamps: true,
  }
);

// ---- Virtual Field: Price with Tax ----
productSchema.virtual('priceWithTax').get(function () {
  const TAX_RATE = 0.17; // 17% sales tax
  return parseFloat((this.price * (1 + TAX_RATE)).toFixed(2));
});

productSchema.set('toJSON', { virtuals: true });
productSchema.set('toObject', { virtuals: true });

// ---- Pre-save Middleware ----
productSchema.pre('save', function (next) {
  // Capitalize the first letter of the product name
  if (this.name) {
    this.name = this.name.charAt(0).toUpperCase() + this.name.slice(1);
  }
  next();
});

// ---- Index for Better Query Performance ----
productSchema.index({ category: 1, price: 1 }); // Compound index

module.exports = mongoose.model('Product', productSchema);
```

---

## 5. Creating Controllers

> Think of controllers like air traffic controllers. They do not fly the planes (models) or build the runways (routes). Instead, they receive incoming signals (requests), coordinate what needs to happen, and direct traffic so everything arrives safely at its destination (response).

### The asyncHandler Utility

Writing try/catch in every controller function is repetitive. The asyncHandler wrapper eliminates that boilerplate by catching errors automatically and forwarding them to the error handling middleware.

```javascript
// middleware/asyncHandler.js

// Wraps an async function so that any rejected promise
// is automatically caught and passed to next()
const asyncHandler = (fn) => (req, res, next) => {
  Promise.resolve(fn(req, res, next)).catch(next);
};

module.exports = asyncHandler;
```

### How asyncHandler Works

Without asyncHandler, every controller needs manual try/catch:

```javascript
// WITHOUT asyncHandler — repetitive try/catch
const getUser = async (req, res, next) => {
  try {
    const user = await User.findById(req.params.id);
    res.json({ success: true, data: user });
  } catch (error) {
    next(error); // Must remember to call next(error) every time
  }
};
```

With asyncHandler, the wrapper handles it for you:

```javascript
// WITH asyncHandler — clean and concise
const getUser = asyncHandler(async (req, res, next) => {
  const user = await User.findById(req.params.id);
  res.json({ success: true, data: user });
});
// If findById throws, asyncHandler catches it and calls next(error) automatically
```

### User Controller

```javascript
// controllers/userController.js
const User = require('../models/User');
const asyncHandler = require('../middleware/asyncHandler');
const AppError = require('../utils/AppError');

// @desc    Get all users
// @route   GET /api/users
// @access  Public
const getAllUsers = asyncHandler(async (req, res, next) => {
  // Support pagination via query parameters
  const page = parseInt(req.query.page, 10) || 1;       // Default to page 1
  const limit = parseInt(req.query.limit, 10) || 10;     // Default to 10 per page
  const skip = (page - 1) * limit;

  const users = await User.find({ isActive: true })
    .select('-__v')        // Exclude the version key
    .skip(skip)
    .limit(limit)
    .sort({ createdAt: -1 }); // Newest first

  const total = await User.countDocuments({ isActive: true });

  res.status(200).json({
    success: true,
    count: users.length,
    total,
    page,
    pages: Math.ceil(total / limit),
    data: users,
  });
});

// @desc    Get single user by ID
// @route   GET /api/users/:id
// @access  Public
const getUserById = asyncHandler(async (req, res, next) => {
  const user = await User.findById(req.params.id).select('-__v');

  if (!user) {
    return next(new AppError(`User not found with id ${req.params.id}`, 404));
  }

  res.status(200).json({
    success: true,
    data: user,
  });
});

// @desc    Create a new user
// @route   POST /api/users
// @access  Public
const createUser = asyncHandler(async (req, res, next) => {
  const { name, email, password, role } = req.body;

  const user = await User.create({
    name,
    email,
    password,
    role,
  });

  res.status(201).json({
    success: true,
    data: user,
  });
});

// @desc    Update a user
// @route   PUT /api/users/:id
// @access  Public
const updateUser = asyncHandler(async (req, res, next) => {
  const user = await User.findByIdAndUpdate(
    req.params.id,
    req.body,
    {
      new: true,            // Return the updated document
      runValidators: true,  // Re-run schema validation on update
    }
  );

  if (!user) {
    return next(new AppError(`User not found with id ${req.params.id}`, 404));
  }

  res.status(200).json({
    success: true,
    data: user,
  });
});

// @desc    Delete a user
// @route   DELETE /api/users/:id
// @access  Public
const deleteUser = asyncHandler(async (req, res, next) => {
  const user = await User.findByIdAndDelete(req.params.id);

  if (!user) {
    return next(new AppError(`User not found with id ${req.params.id}`, 404));
  }

  res.status(200).json({
    success: true,
    message: 'User deleted successfully',
    data: {},
  });
});

module.exports = {
  getAllUsers,
  getUserById,
  createUser,
  updateUser,
  deleteUser,
};
```

### Consistent Response Structure

Every controller should return responses in a uniform shape so the front end always knows what to expect:

```javascript
// Success response
{
  "success": true,
  "count": 5,           // Optional — for list endpoints
  "data": { ... }       // The actual payload
}

// Error response
{
  "success": false,
  "error": "User not found with id 64a..."
}
```

---

## 6. Creating Routes

Routes define the URL endpoints of your API and connect each endpoint to the appropriate controller function. They answer the question: "When someone visits this URL with this HTTP method, which function should handle it?"

### express.Router()

Express provides the `Router` class to organize routes into modular, mountable groups.

```javascript
// routes/userRoutes.js
const express = require('express');
const router = express.Router();
const {
  getAllUsers,
  getUserById,
  createUser,
  updateUser,
  deleteUser,
} = require('../controllers/userController');

// Each route maps an HTTP method + path to a controller function
router.route('/')
  .get(getAllUsers)      // GET    /api/users
  .post(createUser);     // POST   /api/users

router.route('/:id')
  .get(getUserById)      // GET    /api/users/:id
  .put(updateUser)       // PUT    /api/users/:id
  .delete(deleteUser);   // DELETE /api/users/:id

module.exports = router;
```

### Mounting Routes in server.js

```javascript
// server.js (route mounting section)
const userRoutes = require('./routes/userRoutes');
const productRoutes = require('./routes/productRoutes');

// Mount route modules at their base paths
app.use('/api/users', userRoutes);
app.use('/api/products', productRoutes);
```

When you call `app.use('/api/users', userRoutes)`, Express prepends `/api/users` to every path defined inside `userRoutes`. So `router.get('/')` becomes `GET /api/users/`, and `router.get('/:id')` becomes `GET /api/users/:id`.

### RESTful Endpoint Naming Conventions

| Convention | Example | Explanation |
|------------|---------|-------------|
| Use nouns, not verbs | `/api/users` not `/api/getUsers` | The HTTP method provides the verb |
| Use plural nouns | `/api/products` not `/api/product` | A collection is plural |
| Use lowercase | `/api/users` not `/api/Users` | Consistent casing avoids confusion |
| Nest for relationships | `/api/users/:id/orders` | Sub-resources belong to a parent |
| Use query strings for filters | `/api/products?category=books` | Keep the path clean |

### REST Endpoints Reference

| HTTP Method | Endpoint | Action | Description |
|-------------|----------|--------|-------------|
| GET | `/api/users` | getAllUsers | Retrieve all users (with pagination) |
| GET | `/api/users/:id` | getUserById | Retrieve a single user by ID |
| POST | `/api/users` | createUser | Create a new user |
| PUT | `/api/users/:id` | updateUser | Update an existing user |
| DELETE | `/api/users/:id` | deleteUser | Delete a user |
| GET | `/api/products` | getAllProducts | Retrieve all products |
| GET | `/api/products/:id` | getProductById | Retrieve a single product |
| POST | `/api/products` | createProduct | Create a new product |
| PUT | `/api/products/:id` | updateProduct | Update a product |
| DELETE | `/api/products/:id` | deleteProduct | Delete a product |

---

## 7. Complete CRUD API with MongoDB

This section brings every piece together into a fully working application. Follow along to build a CRUD API from scratch.

### Request Flow Through MVC Layers

```
+--------+     HTTP Request      +-----------+     Route Match     +------------+
| Client | ------------------>   |  server.js | -----------------> |  routes/   |
| (e.g., |                      |  Express   |                    | userRoutes |
| Postman)|                     |  App       |                    |            |
+--------+                      +-----------+                     +------------+
                                                                        |
                                                                        v
+--------+     JSON Response     +------------+    DB Query       +------------+
| Client | <------------------   | controllers| <---------------- |  models/   |
|        |                      | userCtrl   |                    |  User.js   |
+--------+                      +------------+                    +------------+
                                       ^                                |
                                       |         Query Result           |
                                       +--------------------------------+
                                                      |
                                               +------v------+
                                               |   MongoDB   |
                                               |  Database   |
                                               +-------------+
```

### Step 1: Initialize the Project

```bash
mkdir express-mongo-crud && cd express-mongo-crud
npm init -y
npm install express mongoose dotenv
npm install --save-dev nodemon
```

### Step 2: Configure package.json Scripts

```json
{
  "scripts": {
    "start": "node server.js",
    "dev": "nodemon server.js",
    "seed": "node seed.js"
  }
}
```

### Step 3: Create the .env File

```
PORT=5000
NODE_ENV=development
MONGO_URI=mongodb://localhost:27017/express_mongo_crud
```

### Step 4: Database Connection (config/db.js)

```javascript
// config/db.js
const mongoose = require('mongoose');

const connectDB = async () => {
  try {
    const conn = await mongoose.connect(process.env.MONGO_URI);
    console.log(`MongoDB Connected: ${conn.connection.host}`);
  } catch (error) {
    console.error(`Error: ${error.message}`);
    process.exit(1);
  }
};

module.exports = connectDB;
```

### Step 5: User Model (models/User.js)

```javascript
// models/User.js
const mongoose = require('mongoose');

const userSchema = new mongoose.Schema(
  {
    name: {
      type: String,
      required: [true, 'Name is required'],
      trim: true,
    },
    email: {
      type: String,
      required: [true, 'Email is required'],
      unique: true,
      lowercase: true,
      match: [/^[\w-\.]+@([\w-]+\.)+[\w-]{2,4}$/, 'Invalid email format'],
    },
    password: {
      type: String,
      required: [true, 'Password is required'],
      minlength: [6, 'Password must be at least 6 characters'],
      select: false,
    },
    role: {
      type: String,
      enum: ['user', 'admin', 'moderator'],
      default: 'user',
    },
  },
  { timestamps: true }
);

module.exports = mongoose.model('User', userSchema);
```

### Step 6: Utility Files

```javascript
// middleware/asyncHandler.js
const asyncHandler = (fn) => (req, res, next) => {
  Promise.resolve(fn(req, res, next)).catch(next);
};

module.exports = asyncHandler;
```

```javascript
// utils/AppError.js
class AppError extends Error {
  constructor(message, statusCode) {
    super(message);
    this.statusCode = statusCode;
    this.status = `${statusCode}`.startsWith('4') ? 'fail' : 'error';
    this.isOperational = true;
    Error.captureStackTrace(this, this.constructor);
  }
}

module.exports = AppError;
```

### Step 7: Controller with Full CRUD (controllers/userController.js)

```javascript
// controllers/userController.js
const User = require('../models/User');
const asyncHandler = require('../middleware/asyncHandler');
const AppError = require('../utils/AppError');

// CREATE — POST /api/users
const createUser = asyncHandler(async (req, res, next) => {
  const user = await User.create(req.body);

  res.status(201).json({
    success: true,
    data: user,
  });
});

// READ ALL — GET /api/users
const getAllUsers = asyncHandler(async (req, res, next) => {
  // Pagination
  const page = parseInt(req.query.page, 10) || 1;
  const limit = parseInt(req.query.limit, 10) || 10;
  const skip = (page - 1) * limit;

  const users = await User.find().skip(skip).limit(limit).sort('-createdAt');
  const total = await User.countDocuments();

  res.status(200).json({
    success: true,
    count: users.length,
    total,
    page,
    pages: Math.ceil(total / limit),
    data: users,
  });
});

// READ ONE — GET /api/users/:id
const getUserById = asyncHandler(async (req, res, next) => {
  const user = await User.findById(req.params.id);

  if (!user) {
    return next(new AppError(`User not found with id ${req.params.id}`, 404));
  }

  res.status(200).json({
    success: true,
    data: user,
  });
});

// UPDATE — PUT /api/users/:id
const updateUser = asyncHandler(async (req, res, next) => {
  const user = await User.findByIdAndUpdate(req.params.id, req.body, {
    new: true,
    runValidators: true,
  });

  if (!user) {
    return next(new AppError(`User not found with id ${req.params.id}`, 404));
  }

  res.status(200).json({
    success: true,
    data: user,
  });
});

// DELETE — DELETE /api/users/:id
const deleteUser = asyncHandler(async (req, res, next) => {
  const user = await User.findByIdAndDelete(req.params.id);

  if (!user) {
    return next(new AppError(`User not found with id ${req.params.id}`, 404));
  }

  res.status(200).json({
    success: true,
    message: 'User deleted successfully',
    data: {},
  });
});

module.exports = { createUser, getAllUsers, getUserById, updateUser, deleteUser };
```

### Step 8: Routes (routes/userRoutes.js)

```javascript
// routes/userRoutes.js
const express = require('express');
const router = express.Router();
const {
  createUser,
  getAllUsers,
  getUserById,
  updateUser,
  deleteUser,
} = require('../controllers/userController');

router.route('/').get(getAllUsers).post(createUser);
router.route('/:id').get(getUserById).put(updateUser).delete(deleteUser);

module.exports = router;
```

### Step 9: Error Handler Middleware

```javascript
// middleware/errorHandler.js
const errorHandler = (err, req, res, next) => {
  let error = { ...err };
  error.message = err.message;

  // CastError — Invalid ObjectId
  if (err.name === 'CastError') {
    error.message = `Resource not found. Invalid ${err.path}: ${err.value}`;
    error.statusCode = 400;
  }

  // ValidationError — Schema validation failed
  if (err.name === 'ValidationError') {
    error.message = Object.values(err.errors).map((val) => val.message).join('. ');
    error.statusCode = 400;
  }

  // Duplicate Key Error
  if (err.code === 11000) {
    const field = Object.keys(err.keyValue)[0];
    error.message = `Duplicate value for field "${field}". This ${field} already exists.`;
    error.statusCode = 400;
  }

  const statusCode = error.statusCode || 500;

  res.status(statusCode).json({
    success: false,
    error: error.message || 'Server Error',
    ...(process.env.NODE_ENV === 'development' && { stack: err.stack }),
  });
};

module.exports = errorHandler;
```

### Step 10: Server Entry Point (server.js)

```javascript
// server.js
const express = require('express');
const dotenv = require('dotenv');
const connectDB = require('./config/db');
const userRoutes = require('./routes/userRoutes');
const errorHandler = require('./middleware/errorHandler');

// Load environment variables
dotenv.config();

// Connect to database
connectDB();

const app = express();

// Body parser middleware — allows Express to read JSON request bodies
app.use(express.json());

// Mount routes
app.use('/api/users', userRoutes);

// Handle 404 — unknown routes
app.all('*', (req, res, next) => {
  res.status(404).json({
    success: false,
    error: `Route ${req.originalUrl} not found`,
  });
});

// Global error handler (must be after all routes)
app.use(errorHandler);

// Start server
const PORT = process.env.PORT || 5000;
app.listen(PORT, () => {
  console.log(`Server running in ${process.env.NODE_ENV} mode on port ${PORT}`);
});
```

### Example API Requests and Responses

**Create a User (POST /api/users):**

```javascript
// Request Body
{
  "name": "Ahmed Khan",
  "email": "ahmed@example.com",
  "password": "secure123",
  "role": "admin"
}

// Response (201 Created)
{
  "success": true,
  "data": {
    "_id": "64a1b2c3d4e5f6a7b8c9d0e1",
    "name": "Ahmed Khan",
    "email": "ahmed@example.com",
    "role": "admin",
    "createdAt": "2025-07-15T10:30:00.000Z",
    "updatedAt": "2025-07-15T10:30:00.000Z"
  }
}
```

**Get All Users (GET /api/users?page=1&limit=2):**

```javascript
// Response (200 OK)
{
  "success": true,
  "count": 2,
  "total": 15,
  "page": 1,
  "pages": 8,
  "data": [
    {
      "_id": "64a1b2c3d4e5f6a7b8c9d0e1",
      "name": "Ahmed Khan",
      "email": "ahmed@example.com",
      "role": "admin",
      "createdAt": "2025-07-15T10:30:00.000Z"
    },
    {
      "_id": "64a1b2c3d4e5f6a7b8c9d0e2",
      "name": "Sara Ali",
      "email": "sara@example.com",
      "role": "user",
      "createdAt": "2025-07-14T09:15:00.000Z"
    }
  ]
}
```

**Get One User (GET /api/users/64a1b2c3d4e5f6a7b8c9d0e1):**

```javascript
// Response (200 OK)
{
  "success": true,
  "data": {
    "_id": "64a1b2c3d4e5f6a7b8c9d0e1",
    "name": "Ahmed Khan",
    "email": "ahmed@example.com",
    "role": "admin"
  }
}

// If not found (404)
{
  "success": false,
  "error": "User not found with id 64a1b2c3d4e5f6a7b8c9ffff"
}
```

**Update a User (PUT /api/users/64a1b2c3d4e5f6a7b8c9d0e1):**

```javascript
// Request Body
{
  "name": "Ahmed Ali Khan",
  "role": "moderator"
}

// Response (200 OK)
{
  "success": true,
  "data": {
    "_id": "64a1b2c3d4e5f6a7b8c9d0e1",
    "name": "Ahmed Ali Khan",
    "email": "ahmed@example.com",
    "role": "moderator",
    "updatedAt": "2025-07-15T11:00:00.000Z"
  }
}
```

**Delete a User (DELETE /api/users/64a1b2c3d4e5f6a7b8c9d0e1):**

```javascript
// Response (200 OK)
{
  "success": true,
  "message": "User deleted successfully",
  "data": {}
}
```

---

## 8. Error Handling

Proper error handling separates amateur APIs from professional ones. A well-handled error tells the client exactly what went wrong, returns the correct HTTP status code, and never leaks sensitive server details in production.

### Custom AppError Class

```javascript
// utils/AppError.js
class AppError extends Error {
  constructor(message, statusCode) {
    super(message);

    this.statusCode = statusCode;

    // Status is "fail" for 4xx errors, "error" for 5xx errors
    this.status = `${statusCode}`.startsWith('4') ? 'fail' : 'error';

    // Operational errors are expected and handled (e.g., invalid input)
    // Programming errors (bugs) are NOT operational
    this.isOperational = true;

    // Capture the stack trace, excluding the constructor call itself
    Error.captureStackTrace(this, this.constructor);
  }
}

module.exports = AppError;
```

### Global Error Handler Middleware

```javascript
// middleware/errorHandler.js

const errorHandler = (err, req, res, next) => {
  // Clone the error properties we need
  let error = { ...err };
  error.message = err.message;

  // Log the error for the developer (only in development)
  if (process.env.NODE_ENV === 'development') {
    console.error('ERROR:', err);
  }

  // ---- Handle Specific Mongoose Errors ----

  // 1. CastError — Invalid ObjectId format
  //    e.g., GET /api/users/invalidId123
  if (err.name === 'CastError') {
    const message = `Resource not found. Invalid ${err.path}: ${err.value}`;
    error = { message, statusCode: 400 };
  }

  // 2. ValidationError — Schema validation failed
  //    e.g., POST /api/users with missing required fields
  if (err.name === 'ValidationError') {
    const message = Object.values(err.errors)
      .map((val) => val.message)
      .join('. ');
    error = { message, statusCode: 400 };
  }

  // 3. Duplicate Key Error — Unique field violation
  //    e.g., POST /api/users with an email that already exists
  if (err.code === 11000) {
    const field = Object.keys(err.keyValue)[0];
    const message = `Duplicate value for field "${field}". This ${field} already exists.`;
    error = { message, statusCode: 400 };
  }

  // ---- Send Response ----

  const statusCode = error.statusCode || 500;

  if (process.env.NODE_ENV === 'development') {
    // Development: send full error details for debugging
    res.status(statusCode).json({
      success: false,
      error: error.message || 'Server Error',
      stack: err.stack, // Stack trace helps locate the bug
    });
  } else {
    // Production: send clean message, never expose internals
    res.status(statusCode).json({
      success: false,
      error: error.message || 'Server Error',
    });
  }
};

module.exports = errorHandler;
```

### 404 Handler for Unknown Routes

This middleware catches any request that does not match a defined route:

```javascript
// In server.js — place AFTER all route mounts, BEFORE errorHandler
const AppError = require('./utils/AppError');

app.all('*', (req, res, next) => {
  const err = new AppError(`Route ${req.originalUrl} not found on this server`, 404);
  next(err); // Pass to the global error handler
});

app.use(errorHandler);
```

### Common MongoDB Errors Reference

| Error Type | Cause | Status Code | Example |
|------------|-------|-------------|---------|
| CastError | Invalid ObjectId format | 400 | `GET /api/users/notavalidid` |
| ValidationError | Missing required fields or invalid values | 400 | `POST /api/users` with empty body |
| Duplicate Key (11000) | Unique field already exists | 400 | Creating user with existing email |
| MongoNetworkError | Cannot reach the database server | 500 | Database server is down |
| MongoServerError | General database operation failure | 500 | Disk full, permission denied |

### Error Handling Flow

```
    Client sends a bad request
              |
              v
    +-------------------+
    | Controller runs   |
    | an async operation|
    +-------------------+
              |
              v
    +-------------------+       Error thrown        +-------------------+
    | asyncHandler      | ----------------------->  | next(error)       |
    | catches the error |                           | called            |
    +-------------------+                           +-------------------+
                                                            |
                                                            v
                                                  +-------------------+
                                                  | errorHandler.js   |
                                                  | (global middleware)|
                                                  +-------------------+
                                                            |
                     +--------------------------------------+------+
                     |                   |                          |
                     v                   v                          v
            +----------------+  +------------------+     +------------------+
            | CastError      |  | ValidationError  |     | Duplicate Key    |
            | Invalid ID     |  | Missing fields   |     | Unique violation |
            | Status: 400    |  | Status: 400      |     | Status: 400      |
            +----------------+  +------------------+     +------------------+
                     |                   |                          |
                     +--------------------------------------+------+
                                                            |
                                                            v
                                                  +-------------------+
                                                  | JSON Response     |
                                                  | { success: false, |
                                                  |   error: "..."  } |
                                                  +-------------------+
```

---

## 9. Data Seeding Scripts

> Think of seeding like stocking a new store before opening day. Before customers walk through the door, the shelves need products, the registers need test transactions, and the displays need sample items. Without this preparation, everything looks empty and nothing can be tested properly.

### Why Seed Data?

| Reason | Explanation |
|--------|-------------|
| Development | Developers need realistic data to build and test features |
| Testing | Automated tests require predictable, consistent data |
| Demos | Showcasing the product requires populated screens, not empty ones |
| Onboarding | New team members can start with a working database immediately |

### The seed.js Script

```javascript
// seed.js
const mongoose = require('mongoose');
const dotenv = require('dotenv');
const User = require('./models/User');
const Product = require('./models/Product');

// Load env variables
dotenv.config();

// ---- Sample User Data ----

const users = [
  {
    name: 'Admin User',
    email: 'admin@example.com',
    password: 'admin123',
    role: 'admin',
  },
  {
    name: 'Sara Ahmed',
    email: 'sara@example.com',
    password: 'sara1234',
    role: 'user',
  },
  {
    name: 'Ali Hassan',
    email: 'ali@example.com',
    password: 'ali12345',
    role: 'user',
  },
  {
    name: 'Fatima Khan',
    email: 'fatima@example.com',
    password: 'fatima123',
    role: 'moderator',
  },
  {
    name: 'Omar Raza',
    email: 'omar@example.com',
    password: 'omar1234',
    role: 'user',
  },
];

// ---- Main Seed Function ----

const seedDB = async () => {
  try {
    // Connect to database
    await mongoose.connect(process.env.MONGO_URI);
    console.log('Database connected for seeding...');

    // Clear existing data
    await User.deleteMany({});
    await Product.deleteMany({});
    console.log('Existing data cleared.');

    // Insert users first (products need user references)
    const createdUsers = await User.insertMany(users);
    console.log(`${createdUsers.length} users seeded.`);

    // Get the admin user's ID to use as createdBy
    const adminId = createdUsers[0]._id;

    // ---- Sample Product Data (references the admin user) ----
    const products = [
      {
        name: 'Wireless Keyboard',
        description: 'Ergonomic wireless keyboard with backlit keys',
        price: 4500,
        category: 'electronics',
        stock: 50,
        ratings: 4.5,
        createdBy: adminId,
      },
      {
        name: 'Cotton T-Shirt',
        description: 'Premium cotton crew neck t-shirt, available in multiple colors',
        price: 1200,
        category: 'clothing',
        stock: 200,
        ratings: 4.0,
        createdBy: adminId,
      },
      {
        name: 'JavaScript: The Good Parts',
        description: 'Classic programming book by Douglas Crockford',
        price: 2500,
        category: 'books',
        stock: 30,
        ratings: 4.8,
        createdBy: adminId,
      },
      {
        name: 'Desk Lamp',
        description: 'Adjustable LED desk lamp with USB charging port',
        price: 3200,
        category: 'home',
        stock: 75,
        ratings: 4.2,
        createdBy: adminId,
      },
      {
        name: 'Yoga Mat',
        description: 'Non-slip exercise yoga mat, 6mm thick',
        price: 1800,
        category: 'sports',
        stock: 100,
        ratings: 4.6,
        createdBy: adminId,
      },
      {
        name: 'Bluetooth Earbuds',
        description: 'Noise-cancelling wireless earbuds with charging case',
        price: 7500,
        category: 'electronics',
        stock: 40,
        ratings: 4.3,
        createdBy: adminId,
      },
      {
        name: 'Running Shoes',
        description: 'Lightweight running shoes with cushioned sole',
        price: 5500,
        category: 'sports',
        stock: 60,
        ratings: 4.7,
        createdBy: adminId,
      },
      {
        name: 'Node.js Design Patterns',
        description: 'Comprehensive guide to Node.js best practices and patterns',
        price: 3800,
        category: 'books',
        stock: 25,
        ratings: 4.9,
        createdBy: adminId,
      },
    ];

    const createdProducts = await Product.insertMany(products);
    console.log(`${createdProducts.length} products seeded.`);

    console.log('Database seeding completed successfully!');
    process.exit(0);
  } catch (error) {
    console.error(`Seeding error: ${error.message}`);
    process.exit(1);
  }
};

// ---- Handle Destroy Flag ----

if (process.argv[2] === '--destroy') {
  const destroyDB = async () => {
    try {
      await mongoose.connect(process.env.MONGO_URI);
      await User.deleteMany({});
      await Product.deleteMany({});
      console.log('All data destroyed!');
      process.exit(0);
    } catch (error) {
      console.error(error.message);
      process.exit(1);
    }
  };
  destroyDB();
} else {
  seedDB();
}
```

### Running the Seed Script

Add the script to your `package.json`:

```json
{
  "scripts": {
    "start": "node server.js",
    "dev": "nodemon server.js",
    "seed": "node seed.js",
    "seed:destroy": "node seed.js --destroy"
  }
}
```

```bash
# Seed the database with sample data
npm run seed

# Expected output:
# Database connected for seeding...
# Existing data cleared.
# 5 users seeded.
# 8 products seeded.
# Database seeding completed successfully!

# Destroy all data
npm run seed:destroy

# Expected output:
# All data destroyed!
```

---

## 10. Aggregation Practical Examples

Aggregation pipelines let you perform complex data analysis directly inside MongoDB. Instead of fetching raw data and processing it in JavaScript, the database handles the heavy lifting.

### Example 1: Total Revenue Calculation

Calculate the total potential revenue from all products (price multiplied by stock).

```javascript
// Total revenue = sum of (price * stock) for all products
const totalRevenue = await Product.aggregate([
  {
    $group: {
      _id: null, // Group all documents together (no grouping field)
      totalRevenue: {
        $sum: { $multiply: ['$price', '$stock'] },
      },
      totalProducts: { $sum: 1 }, // Count all products
    },
  },
  {
    $project: {
      _id: 0, // Hide the _id field from output
      totalRevenue: 1,
      totalProducts: 1,
    },
  },
]);

// Expected Output:
// [
//   { totalRevenue: 2735000, totalProducts: 8 }
// ]
```

### Example 2: Products Per Category Count

Count how many products exist in each category.

```javascript
const productsPerCategory = await Product.aggregate([
  {
    $group: {
      _id: '$category',       // Group by the category field
      count: { $sum: 1 },      // Count documents in each group
      avgPrice: { $avg: '$price' }, // Average price per category
    },
  },
  {
    $sort: { count: -1 }, // Sort by count, highest first
  },
  {
    $project: {
      _id: 0,
      category: '$_id',
      count: 1,
      avgPrice: { $round: ['$avgPrice', 2] }, // Round to 2 decimals
    },
  },
]);

// Expected Output:
// [
//   { category: "electronics", count: 2, avgPrice: 6000 },
//   { category: "sports",      count: 2, avgPrice: 3650 },
//   { category: "books",       count: 2, avgPrice: 3150 },
//   { category: "clothing",    count: 1, avgPrice: 1200 },
//   { category: "home",        count: 1, avgPrice: 3200 }
// ]
```

### Example 3: Average Product Rating

Calculate the average rating across all products.

```javascript
const avgRating = await Product.aggregate([
  {
    $group: {
      _id: null,
      averageRating: { $avg: '$ratings' },
      highestRating: { $max: '$ratings' },
      lowestRating: { $min: '$ratings' },
      totalProducts: { $sum: 1 },
    },
  },
  {
    $project: {
      _id: 0,
      averageRating: { $round: ['$averageRating', 2] },
      highestRating: 1,
      lowestRating: 1,
      totalProducts: 1,
    },
  },
]);

// Expected Output:
// [
//   {
//     averageRating: 4.5,
//     highestRating: 4.9,
//     lowestRating: 4.0,
//     totalProducts: 8
//   }
// ]
```

### Example 4: Monthly Sales Report

Group products by the month they were created to see a monthly inventory report.

```javascript
const monthlySalesReport = await Product.aggregate([
  {
    $group: {
      _id: {
        year: { $year: '$createdAt' },
        month: { $month: '$createdAt' },
      },
      productsAdded: { $sum: 1 },
      totalStockAdded: { $sum: '$stock' },
      totalValue: { $sum: { $multiply: ['$price', '$stock'] } },
    },
  },
  {
    $sort: { '_id.year': -1, '_id.month': -1 }, // Most recent first
  },
  {
    $project: {
      _id: 0,
      year: '$_id.year',
      month: '$_id.month',
      productsAdded: 1,
      totalStockAdded: 1,
      totalValue: 1,
    },
  },
]);

// Expected Output:
// [
//   {
//     year: 2025,
//     month: 7,
//     productsAdded: 8,
//     totalStockAdded: 580,
//     totalValue: 2735000
//   }
// ]
```

### Example 5: Top 5 Most Expensive Products

Retrieve the five products with the highest prices.

```javascript
const topExpensiveProducts = await Product.aggregate([
  {
    $sort: { price: -1 }, // Sort by price, highest first
  },
  {
    $limit: 5, // Take only the top 5
  },
  {
    $project: {
      _id: 0,
      name: 1,
      price: 1,
      category: 1,
      priceWithTax: {
        $round: [{ $multiply: ['$price', 1.17] }, 2], // 17% tax
      },
    },
  },
]);

// Expected Output:
// [
//   { name: "Bluetooth Earbuds",       price: 7500, category: "electronics", priceWithTax: 8775 },
//   { name: "Running Shoes",           price: 5500, category: "sports",      priceWithTax: 6435 },
//   { name: "Wireless Keyboard",       price: 4500, category: "electronics", priceWithTax: 5265 },
//   { name: "Node.js Design Patterns", price: 3800, category: "books",       priceWithTax: 4446 },
//   { name: "Desk Lamp",               price: 3200, category: "home",        priceWithTax: 3744 }
// ]
```

### Example 6: Category Revenue Breakdown

Find the total revenue potential for each category.

```javascript
const categoryRevenue = await Product.aggregate([
  {
    $group: {
      _id: '$category',
      totalRevenue: { $sum: { $multiply: ['$price', '$stock'] } },
      avgPrice: { $avg: '$price' },
      totalStock: { $sum: '$stock' },
    },
  },
  {
    $addFields: {
      revenuePercentage: {
        $round: [
          { $multiply: [{ $divide: ['$totalRevenue', 2735000] }, 100] },
          1,
        ],
      },
    },
  },
  {
    $sort: { totalRevenue: -1 },
  },
  {
    $project: {
      _id: 0,
      category: '$_id',
      totalRevenue: 1,
      avgPrice: { $round: ['$avgPrice', 0] },
      totalStock: 1,
      revenuePercentage: 1,
    },
  },
]);

// Expected Output:
// [
//   { category: "electronics", totalRevenue: 525000,  avgPrice: 6000, totalStock: 90,  revenuePercentage: 19.2 },
//   { category: "sports",      totalRevenue: 510000,  avgPrice: 3650, totalStock: 160, revenuePercentage: 18.6 },
//   { category: "clothing",    totalRevenue: 240000,  avgPrice: 1200, totalStock: 200, revenuePercentage: 8.8  },
//   { category: "home",        totalRevenue: 240000,  avgPrice: 3200, totalStock: 75,  revenuePercentage: 8.8  },
//   { category: "books",       totalRevenue: 170000,  avgPrice: 3150, totalStock: 55,  revenuePercentage: 6.2  }
// ]
```

### Putting Aggregations in a Controller

```javascript
// controllers/statsController.js
const Product = require('../models/Product');
const asyncHandler = require('../middleware/asyncHandler');

// @desc    Get product statistics
// @route   GET /api/stats/products
// @access  Public
const getProductStats = asyncHandler(async (req, res) => {
  const stats = await Product.aggregate([
    {
      $group: {
        _id: '$category',
        count: { $sum: 1 },
        avgPrice: { $avg: '$price' },
        avgRating: { $avg: '$ratings' },
        totalRevenue: { $sum: { $multiply: ['$price', '$stock'] } },
      },
    },
    { $sort: { totalRevenue: -1 } },
    {
      $project: {
        _id: 0,
        category: '$_id',
        count: 1,
        avgPrice: { $round: ['$avgPrice', 2] },
        avgRating: { $round: ['$avgRating', 1] },
        totalRevenue: 1,
      },
    },
  ]);

  res.status(200).json({
    success: true,
    data: stats,
  });
});

module.exports = { getProductStats };
```

### Stats Route

```javascript
// routes/statsRoutes.js
const express = require('express');
const router = express.Router();
const { getProductStats } = require('../controllers/statsController');

router.get('/products', getProductStats);

module.exports = router;
```

Mount it in server.js:

```javascript
// server.js
const statsRoutes = require('./routes/statsRoutes');
app.use('/api/stats', statsRoutes);
```

---

## 11. Week 31 Project: Full CRUD API with MongoDB Backend

### Project Requirements Checklist

- [ ] Express server with environment-based configuration
- [ ] MongoDB connection via Mongoose with proper error handling
- [ ] MVC folder structure (models, controllers, routes, middleware, config, utils)
- [ ] Product model with full validation (name, description, price, category, stock, createdBy)
- [ ] User model with validation (name, email, password, role)
- [ ] Full CRUD operations for products (Create, Read All, Read One, Update, Delete)
- [ ] Full CRUD operations for users
- [ ] Pagination support on list endpoints
- [ ] Custom AppError class with statusCode and isOperational
- [ ] Global error handler (CastError, ValidationError, duplicate key)
- [ ] 404 handler for unknown routes
- [ ] asyncHandler utility wrapper
- [ ] Data seeding script with sample users and products
- [ ] Aggregation stats endpoint (products per category, average rating, revenue)
- [ ] Tested with Postman or Thunder Client

### Features to Implement

**Products CRUD:**

- `POST /api/products` -- Create a product with validation
- `GET /api/products` -- List all products with pagination
- `GET /api/products/:id` -- Get a single product (populate createdBy to show user name)
- `PUT /api/products/:id` -- Update a product with runValidators
- `DELETE /api/products/:id` -- Delete a product

**Error Handling:**

- Invalid ObjectId returns 400 with a clear message
- Missing required fields returns 400 with field-specific messages
- Duplicate email returns 400 with a duplicate message
- Unknown routes return 404

**Seeding:**

- `npm run seed` populates 5 users and 8+ products
- `node seed.js --destroy` clears all data

**Aggregation Stats Endpoint:**

- `GET /api/stats/products` -- Returns category breakdown with count, avg price, avg rating, and revenue

### Project Folder Structure

```
week-31-project/
  +-- config/
  |     +-- db.js
  +-- controllers/
  |     +-- userController.js
  |     +-- productController.js
  |     +-- statsController.js
  +-- middleware/
  |     +-- errorHandler.js
  |     +-- asyncHandler.js
  +-- models/
  |     +-- User.js
  |     +-- Product.js
  +-- routes/
  |     +-- userRoutes.js
  |     +-- productRoutes.js
  |     +-- statsRoutes.js
  +-- utils/
  |     +-- AppError.js
  +-- server.js
  +-- seed.js
  +-- .env
  +-- .env.example
  +-- .gitignore
  +-- package.json
```

### Product Controller (for reference)

```javascript
// controllers/productController.js
const Product = require('../models/Product');
const asyncHandler = require('../middleware/asyncHandler');
const AppError = require('../utils/AppError');

// @desc    Get all products
// @route   GET /api/products
const getAllProducts = asyncHandler(async (req, res) => {
  const page = parseInt(req.query.page, 10) || 1;
  const limit = parseInt(req.query.limit, 10) || 10;
  const skip = (page - 1) * limit;

  // Optional: filter by category
  const filter = {};
  if (req.query.category) {
    filter.category = req.query.category;
  }

  const products = await Product.find(filter)
    .populate('createdBy', 'name email')  // Show creator's name and email
    .skip(skip)
    .limit(limit)
    .sort('-createdAt');

  const total = await Product.countDocuments(filter);

  res.status(200).json({
    success: true,
    count: products.length,
    total,
    page,
    pages: Math.ceil(total / limit),
    data: products,
  });
});

// @desc    Get single product
// @route   GET /api/products/:id
const getProductById = asyncHandler(async (req, res, next) => {
  const product = await Product.findById(req.params.id)
    .populate('createdBy', 'name email');

  if (!product) {
    return next(new AppError(`Product not found with id ${req.params.id}`, 404));
  }

  res.status(200).json({
    success: true,
    data: product,
  });
});

// @desc    Create product
// @route   POST /api/products
const createProduct = asyncHandler(async (req, res) => {
  const product = await Product.create(req.body);

  res.status(201).json({
    success: true,
    data: product,
  });
});

// @desc    Update product
// @route   PUT /api/products/:id
const updateProduct = asyncHandler(async (req, res, next) => {
  const product = await Product.findByIdAndUpdate(req.params.id, req.body, {
    new: true,
    runValidators: true,
  });

  if (!product) {
    return next(new AppError(`Product not found with id ${req.params.id}`, 404));
  }

  res.status(200).json({
    success: true,
    data: product,
  });
});

// @desc    Delete product
// @route   DELETE /api/products/:id
const deleteProduct = asyncHandler(async (req, res, next) => {
  const product = await Product.findByIdAndDelete(req.params.id);

  if (!product) {
    return next(new AppError(`Product not found with id ${req.params.id}`, 404));
  }

  res.status(200).json({
    success: true,
    message: 'Product deleted successfully',
    data: {},
  });
});

module.exports = {
  getAllProducts,
  getProductById,
  createProduct,
  updateProduct,
  deleteProduct,
};
```

### Product Routes

```javascript
// routes/productRoutes.js
const express = require('express');
const router = express.Router();
const {
  getAllProducts,
  getProductById,
  createProduct,
  updateProduct,
  deleteProduct,
} = require('../controllers/productController');

router.route('/').get(getAllProducts).post(createProduct);
router.route('/:id').get(getProductById).put(updateProduct).delete(deleteProduct);

module.exports = router;
```

### Testing with Postman or Thunder Client

Use an API client to test every endpoint. Here is the complete list of requests to verify:

| Method | URL | Body | Expected Status |
|--------|-----|------|-----------------|
| POST | `http://localhost:5000/api/users` | `{ "name": "Test", "email": "test@example.com", "password": "test123" }` | 201 |
| GET | `http://localhost:5000/api/users` | None | 200 |
| GET | `http://localhost:5000/api/users/:id` | None | 200 or 404 |
| PUT | `http://localhost:5000/api/users/:id` | `{ "name": "Updated Name" }` | 200 or 404 |
| DELETE | `http://localhost:5000/api/users/:id` | None | 200 or 404 |
| POST | `http://localhost:5000/api/products` | `{ "name": "Widget", "description": "A test", "price": 999, "category": "electronics", "stock": 10, "createdBy": "<userId>" }` | 201 |
| GET | `http://localhost:5000/api/products` | None | 200 |
| GET | `http://localhost:5000/api/products/:id` | None | 200 or 404 |
| PUT | `http://localhost:5000/api/products/:id` | `{ "price": 1500 }` | 200 or 404 |
| DELETE | `http://localhost:5000/api/products/:id` | None | 200 or 404 |
| GET | `http://localhost:5000/api/stats/products` | None | 200 |
| GET | `http://localhost:5000/api/nonexistent` | None | 404 |
| GET | `http://localhost:5000/api/users/invalidid` | None | 400 |

### Expected API Endpoints Summary

| Resource | Endpoints | Description |
|----------|-----------|-------------|
| Users | 5 endpoints | Full CRUD for user management |
| Products | 5 endpoints | Full CRUD for product management |
| Stats | 1 endpoint | Aggregation-powered analytics |
| Error | 1 fallback | 404 catch-all for unknown routes |
| **Total** | **12 endpoints** | Complete RESTful API |

---

## 12. Database Phase Summary

This section recaps everything covered across Weeks 28 through 31 of the database phase.

### Weeks 28-31 Recap

| Week | Topic | Key Concepts |
|------|-------|-------------|
| 28 | MongoDB Basics | Documents, collections, BSON, CRUD operations, Mongo Shell, Atlas setup |
| 29 | Mongoose ODM | Schemas, models, validation, middleware, instance/static methods, virtuals |
| 30 | Advanced Queries & Relations | Query operators, population, references, text search, indexing, aggregation fundamentals |
| 31 | MongoDB with Express | MVC architecture, environment config, CRUD API, error handling, seeding, aggregation endpoints |

### Skills Learned Progression

| Skill | Week 28 | Week 29 | Week 30 | Week 31 |
|-------|---------|---------|---------|---------|
| Database concepts | Introduced | -- | -- | -- |
| CRUD operations | Raw MongoDB | Mongoose methods | Advanced queries | Full API endpoints |
| Data modeling | Document structure | Schemas + validation | Relations + population | Models in MVC |
| Error handling | -- | Validation errors | -- | Global error middleware |
| Project structure | -- | -- | -- | Full MVC pattern |
| API design | -- | -- | -- | RESTful conventions |
| Data analysis | -- | -- | Aggregation basics | Aggregation in controllers |

### Database Knowledge Pyramid

```
                          +---------------------------+
                         /        Week 31              \
                        /  Express + MongoDB Integration \
                       /   MVC, CRUD API, Error Handling  \
                      /    Seeding, Aggregation Endpoints   \
                     +---------------------------------------+
                    /            Week 30                       \
                   /   Advanced Queries & Relations              \
                  /    Population, Indexing, Text Search,         \
                 /     Aggregation Pipelines, Operators            \
                +--------------------------------------------------+
               /                 Week 29                             \
              /           Mongoose ODM                                 \
             /    Schemas, Models, Validation, Middleware,               \
            /     Virtuals, Instance Methods, Static Methods              \
           +---------------------------------------------------------------+
          /                       Week 28                                    \
         /                 MongoDB Basics                                      \
        /   Documents, Collections, BSON, CRUD, Mongo Shell, Atlas Setup        \
       +-------------------------------------------------------------------------+
```

### What You Can Build Now

After completing the database phase, you have the skills to build:

- RESTful APIs backed by MongoDB
- Server-side applications with proper data validation
- Paginated data endpoints for large datasets
- Analytics dashboards powered by aggregation pipelines
- Properly structured backend projects using the MVC pattern
- Production-ready error handling and environment configuration

### What is Next: Full MERN Stack Integration

```
+-------------------------------------------------------------------+
|                        MERN Stack                                 |
+-------------------------------------------------------------------+
|                                                                   |
|   +----------+    +-----------+    +---------+    +-----------+   |
|   | MongoDB  | -> | Express   | -> | React   | -> | Node.js   |   |
|   | Database |    | API Layer |    | Frontend|    | Runtime   |   |
|   | (Done)   |    | (Done)    |    | (Next)  |    | (Done)    |   |
|   +----------+    +-----------+    +---------+    +-----------+   |
|                                                                   |
+-------------------------------------------------------------------+
```

In the upcoming weeks, you will connect your React front end to the Express API you built in this phase. The React application will make HTTP requests to your API endpoints, display data from MongoDB in the browser, and allow users to create, update, and delete records through a visual interface. Every piece you have built so far becomes the foundation for a complete, full-stack web application.

---

*End of Week 31 -- MongoDB with Express Integration*
