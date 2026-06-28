# Week 31 — MongoDB with Express Integration: Practice Questions

**Total Questions: 30** (10 MCQs + 5 Short Answer + 5 Coding Exercises + 10 Database Phase Review)

---

## Part 1: Multiple Choice Questions (MCQs)

**1. What does `mongoose.connect()` return?**

- A) A Mongoose model instance
- B) A Promise that resolves to a Mongoose connection object
- C) A callback function
- D) A MongoDB client object

<details><summary>Answer</summary>

**B) A Promise that resolves to a Mongoose connection object**

`mongoose.connect()` returns a Promise that resolves to the Mongoose instance once the connection to MongoDB is established. This allows you to use `async/await` syntax for clean connection handling:

```javascript
const connectDB = async () => {
  const conn = await mongoose.connect(process.env.MONGO_URI);
  console.log(`MongoDB Connected: ${conn.connection.host}`);
};
```

The connection string follows the format `mongodb://username:password@host:port/database` for local connections or `mongodb+srv://username:password@cluster.mongodb.net/database` for MongoDB Atlas.

</details>

---

**2. In the MVC (Model-View-Controller) pattern, which component is responsible for handling business logic and data manipulation?**

- A) View
- B) Router
- C) Controller
- D) Middleware

<details><summary>Answer</summary>

**C) Controller**

In the MVC pattern applied to Express applications:

- **Model** defines the data structure and interacts with the database (Mongoose schemas and models).
- **View** is the presentation layer (in API development, this is the JSON response sent to the client).
- **Controller** contains the business logic. It receives requests, processes data using models, and sends responses.

Controllers sit between the routes and models. They handle tasks like validation, data transformation, error checking, and coordinating between different models before returning a response.

```javascript
// controllers/productController.js
const getProduct = async (req, res) => {
  const product = await Product.findById(req.params.id);
  if (!product) {
    return res.status(404).json({ success: false, error: 'Product not found' });
  }
  res.status(200).json({ success: true, data: product });
};
```

</details>

---

**3. What problem does an `asyncHandler` wrapper solve in Express applications?**

- A) It speeds up database queries
- B) It automatically catches errors in async route handlers and passes them to the error middleware
- C) It converts synchronous functions to asynchronous functions
- D) It handles CORS requests automatically

<details><summary>Answer</summary>

**B) It automatically catches errors in async route handlers and passes them to the error middleware**

Express does not natively catch errors thrown inside `async` route handlers. If an async function throws an error or a rejected Promise is not caught, it will result in an unhandled promise rejection rather than triggering the Express error-handling middleware. The `asyncHandler` wrapper solves this by wrapping async functions in a try/catch block and forwarding any errors to `next()`:

```javascript
const asyncHandler = (fn) => (req, res, next) => {
  Promise.resolve(fn(req, res, next)).catch(next);
};

// Usage - no try/catch needed in the controller
const getProducts = asyncHandler(async (req, res) => {
  const products = await Product.find();
  res.status(200).json({ success: true, data: products });
});
```

Without `asyncHandler`, you would need to write repetitive try/catch blocks in every single async controller function.

</details>

---

**4. When a client requests a resource that does not exist in the database, what HTTP status code should the server return?**

- A) 400 Bad Request
- B) 401 Unauthorized
- C) 404 Not Found
- D) 500 Internal Server Error

<details><summary>Answer</summary>

**C) 404 Not Found**

HTTP status code 404 indicates that the server cannot find the requested resource. In the context of a REST API, this is the appropriate response when a client requests a specific resource by ID and that resource does not exist in the database:

```javascript
const getProductById = asyncHandler(async (req, res) => {
  const product = await Product.findById(req.params.id);

  if (!product) {
    res.status(404);
    throw new Error('Product not found');
  }

  res.status(200).json({ success: true, data: product });
});
```

Common HTTP status codes in API development include: 200 (OK), 201 (Created), 400 (Bad Request for invalid input), 401 (Unauthorized), 403 (Forbidden), 404 (Not Found), and 500 (Internal Server Error).

</details>

---

**5. How do you mount an Express Router on a specific base path in the main application file?**

- A) `app.route('/api/products', productRouter)`
- B) `app.use('/api/products', productRouter)`
- C) `app.mount('/api/products', productRouter)`
- D) `app.attach('/api/products', productRouter)`

<details><summary>Answer</summary>

**B) `app.use('/api/products', productRouter)`**

`app.use()` is the method used to mount middleware and routers at a specific path. When you pass a path and a router instance to `app.use()`, all routes defined in that router are prefixed with the given path:

```javascript
// routes/productRoutes.js
const router = express.Router();
router.get('/', getAllProducts);       // GET /api/products
router.get('/:id', getProductById);   // GET /api/products/:id
router.post('/', createProduct);       // POST /api/products
module.exports = router;

// server.js
const productRouter = require('./routes/productRoutes');
app.use('/api/products', productRouter);
```

This approach keeps the main application file clean and organizes routes into modular, maintainable files following the separation of concerns principle.

</details>

---

**6. In a MongoDB aggregation pipeline, what does the `_id` field in a `$group` stage determine?**

- A) The unique identifier for each output document
- B) The field or expression by which documents are grouped together
- C) The primary key of the collection
- D) The sort order of the results

<details><summary>Answer</summary>

**B) The field or expression by which documents are grouped together**

In the `$group` stage, the `_id` field specifies the grouping key. All documents that share the same value for the `_id` expression are grouped together, and accumulator expressions (like `$sum`, `$avg`, `$min`, `$max`) are computed across each group:

```javascript
// Group products by category and calculate stats
{
  $group: {
    _id: "$category",            // Group by the "category" field
    totalProducts: { $sum: 1 },  // Count documents in each group
    avgPrice: { $avg: "$price" } // Average price per group
  }
}
```

If `_id` is set to `null`, all documents are grouped into a single group, which is useful for calculating totals across the entire collection. You can also use complex expressions like `{ year: { $year: "$createdAt" }, month: { $month: "$createdAt" } }` as the `_id` for multi-field grouping.

</details>

---

**7. What does the `.populate()` method do in Mongoose?**

- A) It inserts bulk data into a collection
- B) It replaces a reference ObjectId with the actual referenced document data
- C) It creates a new collection from existing data
- D) It duplicates documents across collections

<details><summary>Answer</summary>

**B) It replaces a reference ObjectId with the actual referenced document data**

`.populate()` is Mongoose's way of performing automatic joins. When a document field contains a reference (ObjectId) to another collection, `.populate()` fetches the referenced document and replaces the ObjectId with the actual data. This is much more convenient than performing manual lookups:

```javascript
// Schema with a reference
const productSchema = new mongoose.Schema({
  name: String,
  createdBy: { type: mongoose.Schema.Types.ObjectId, ref: 'User' }
});

// Without populate - returns just the ObjectId
const product = await Product.findById(id);
// { name: "Laptop", createdBy: "60d5f484f1a2c8b1f8e4e1a1" }

// With populate - returns the full user document
const product = await Product.findById(id).populate('createdBy', 'name email');
// { name: "Laptop", createdBy: { _id: "...", name: "John", email: "john@example.com" } }
```

The second argument to `.populate()` lets you select only specific fields from the referenced document, which improves performance by avoiding fetching unnecessary data.

</details>

---

**8. What does the option `{ runValidators: true }` do when passed to a Mongoose update operation?**

- A) It runs the update query faster by skipping middleware
- B) It ensures that the updated data is validated against the schema validators before saving
- C) It validates the query syntax before execution
- D) It checks if the document exists before updating

<details><summary>Answer</summary>

**B) It ensures that the updated data is validated against the schema validators before saving**

By default, Mongoose does **not** run schema validators on update operations like `findByIdAndUpdate()` or `updateOne()`. This means invalid data could be saved to the database even if you have validators defined in your schema. Setting `runValidators: true` forces Mongoose to validate the update data against your schema rules:

```javascript
const productSchema = new mongoose.Schema({
  name: { type: String, required: true },
  price: { type: Number, min: 0 },
  category: { type: String, enum: ['Electronics', 'Clothing', 'Books'] }
});

// Without runValidators - invalid data could be saved
await Product.findByIdAndUpdate(id, { price: -50 });

// With runValidators - throws ValidationError for price < 0
await Product.findByIdAndUpdate(
  id,
  { price: -50 },
  { new: true, runValidators: true }
);
```

It is considered a best practice to always include `runValidators: true` in update operations to maintain data integrity.

</details>

---

**9. Why should you use the `dotenv` package and environment variables instead of hardcoding configuration values like database connection strings?**

- A) It makes the application run faster
- B) It provides security by keeping sensitive data out of source code, and flexibility across different environments
- C) It is required by MongoDB to establish a connection
- D) It automatically encrypts the connection string

<details><summary>Answer</summary>

**B) It provides security by keeping sensitive data out of source code, and flexibility across different environments**

The `dotenv` package loads variables from a `.env` file into `process.env`, providing several important benefits:

1. **Security**: Sensitive data like database credentials, API keys, and secrets are kept out of version control (`.env` is added to `.gitignore`).
2. **Environment flexibility**: Different configurations for development, staging, and production without code changes.
3. **Team collaboration**: Each developer can have their own `.env` file with local settings.

```javascript
// .env file (never committed to git)
MONGO_URI=mongodb+srv://user:password@cluster.mongodb.net/mydb
PORT=5000
NODE_ENV=development

// config/db.js
require('dotenv').config();

const connectDB = async () => {
  await mongoose.connect(process.env.MONGO_URI);
};
```

Without environment variables, changing a database URL would require modifying and redeploying the source code, and credentials would be visible in the repository history.

</details>

---

**10. What is the primary purpose of a seed script in a database-backed application?**

- A) To optimize database query performance
- B) To populate the database with initial or sample data for development and testing
- C) To back up the production database
- D) To migrate the database schema to a new version

<details><summary>Answer</summary>

**B) To populate the database with initial or sample data for development and testing**

A seed script is a standalone script that connects to the database, optionally clears existing data, and inserts a predefined set of documents. Seed scripts are essential for:

1. **Development**: Quickly setting up a local database with realistic test data.
2. **Testing**: Ensuring consistent starting data for automated tests.
3. **Demos**: Populating the application with sample data for presentations.
4. **Onboarding**: New team members can get a working database in one command.

```javascript
// seed.js
const seedDB = async () => {
  await mongoose.connect(process.env.MONGO_URI);
  await Product.deleteMany({});
  await Product.insertMany(sampleProducts);
  console.log('Database seeded successfully');
  process.exit(0);
};
```

Seed scripts are typically run with a command like `node seed.js` or configured as an npm script such as `npm run seed`.

</details>

---

## Part 2: Short Answer Questions

**11. Explain the benefits of the MVC pattern for Express applications. Give at least three advantages.**

<details><summary>Answer</summary>

The **MVC (Model-View-Controller)** pattern organizes an Express application into three distinct layers, each with a clear responsibility. Here are the key advantages:

**1. Separation of Concerns**

Each layer has a single responsibility, making the codebase easier to understand and maintain:

| Layer | Responsibility | Express Equivalent |
|-------|---------------|-------------------|
| Model | Data structure and database interaction | Mongoose schemas and models |
| View | Presentation and response formatting | JSON responses (in APIs) |
| Controller | Business logic and request handling | Controller functions |

**2. Code Reusability**

Models can be reused across multiple controllers, and controllers can be shared across different routes. For example, the same `User` model can be used by both an authentication controller and an admin controller.

**3. Easier Testing**

Each component can be tested in isolation. You can unit test controllers by mocking models, test models independently of HTTP concerns, and test routes separately:

```javascript
// Controller can be tested independently
const { getProducts } = require('../controllers/productController');

// Mock the model
jest.mock('../models/Product');
Product.find.mockResolvedValue([{ name: 'Test Product' }]);

// Test the controller logic without HTTP
```

**4. Team Collaboration**

Multiple developers can work on different layers simultaneously. One developer can build models while another works on controllers, reducing merge conflicts and improving productivity.

**5. Scalability and Maintainability**

As the application grows, new features can be added by creating new model-controller-route sets without modifying existing code. The organized structure makes it easy to locate and modify specific functionality:

```
project/
  models/
    Product.js
    User.js
  controllers/
    productController.js
    userController.js
  routes/
    productRoutes.js
    userRoutes.js
  server.js
```

**6. Consistent Code Organization**

Every team member follows the same structure, making the codebase predictable and reducing the learning curve for new developers joining the project.

</details>

---

**12. Why should you use an asyncHandler wrapper instead of writing try/catch in every controller function?**

<details><summary>Answer</summary>

Using an `asyncHandler` wrapper eliminates repetitive try/catch boilerplate in every async controller function and ensures that all errors are consistently forwarded to the Express error-handling middleware.

**The Problem Without asyncHandler:**

Express does not automatically catch errors from async functions. Without explicit error handling, rejected promises go unhandled:

```javascript
// Without asyncHandler - repetitive and error-prone
const getProducts = async (req, res, next) => {
  try {
    const products = await Product.find();
    res.status(200).json({ success: true, data: products });
  } catch (error) {
    next(error); // Easy to forget this line
  }
};

const getProductById = async (req, res, next) => {
  try {
    const product = await Product.findById(req.params.id);
    if (!product) {
      return res.status(404).json({ success: false, error: 'Not found' });
    }
    res.status(200).json({ success: true, data: product });
  } catch (error) {
    next(error); // Same boilerplate repeated
  }
};
```

**The Solution With asyncHandler:**

```javascript
// The asyncHandler utility
const asyncHandler = (fn) => (req, res, next) => {
  Promise.resolve(fn(req, res, next)).catch(next);
};

// Clean controller functions - no try/catch needed
const getProducts = asyncHandler(async (req, res) => {
  const products = await Product.find();
  res.status(200).json({ success: true, data: products });
});

const getProductById = asyncHandler(async (req, res) => {
  const product = await Product.findById(req.params.id);
  if (!product) {
    res.status(404);
    throw new Error('Product not found');
  }
  res.status(200).json({ success: true, data: product });
});
```

**Key Benefits:**

1. **DRY Principle**: Write the error-catching logic once instead of in every function.
2. **Consistency**: Every async error is guaranteed to reach the error middleware.
3. **Readability**: Controller functions focus purely on business logic.
4. **Safety**: Eliminates the risk of forgetting a `try/catch` block and leaving unhandled promise rejections.
5. **Centralized Error Handling**: All errors flow to the global error handler, where they can be logged, formatted, and responded to uniformly.

You can also install the `express-async-handler` npm package instead of writing your own implementation.

</details>

---

**13. Describe a comprehensive error handling strategy for an Express + MongoDB API. Include a custom error class, a global error handler, and how to handle specific error types.**

<details><summary>Answer</summary>

A robust error handling strategy involves multiple layers working together to catch, classify, and respond to errors consistently.

**Layer 1: Custom Error Class**

Create an `AppError` class that extends the built-in `Error` to include HTTP status codes and operational flags:

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

**Layer 2: asyncHandler for Catching Async Errors**

```javascript
// middleware/asyncHandler.js
const asyncHandler = (fn) => (req, res, next) => {
  Promise.resolve(fn(req, res, next)).catch(next);
};
```

**Layer 3: Controller Usage**

```javascript
const getProduct = asyncHandler(async (req, res) => {
  const product = await Product.findById(req.params.id);
  if (!product) {
    throw new AppError('Product not found', 404);
  }
  res.status(200).json({ success: true, data: product });
});
```

**Layer 4: Global Error Handling Middleware**

This middleware catches all errors and sends a formatted response. It handles specific MongoDB/Mongoose error types:

```javascript
// middleware/errorHandler.js
const errorHandler = (err, req, res, next) => {
  let error = { ...err };
  error.message = err.message;

  // Log for development
  console.error(err.stack);

  // Mongoose bad ObjectId (CastError)
  if (err.name === 'CastError') {
    error = new AppError(`Resource not found with id: ${err.value}`, 400);
  }

  // Mongoose validation error
  if (err.name === 'ValidationError') {
    const messages = Object.values(err.errors).map((val) => val.message);
    error = new AppError(`Validation failed: ${messages.join(', ')}`, 400);
  }

  // MongoDB duplicate key error
  if (err.code === 11000) {
    const field = Object.keys(err.keyValue)[0];
    error = new AppError(`Duplicate value for field: ${field}`, 400);
  }

  res.status(error.statusCode || 500).json({
    success: false,
    error: error.message || 'Internal Server Error'
  });
};
```

**Layer 5: 404 Route Handler**

```javascript
// Catch requests to undefined routes
app.use('*', (req, res, next) => {
  next(new AppError(`Cannot find ${req.originalUrl} on this server`, 404));
});

// Error handler must be registered last
app.use(errorHandler);
```

**Error Types Summary:**

| Error Type | Cause | Status Code |
|-----------|-------|-------------|
| CastError | Invalid ObjectId format | 400 |
| ValidationError | Schema validation failure | 400 |
| 11000 | Duplicate unique field | 400 |
| AppError (404) | Resource not found | 404 |
| Unhandled | Unexpected server error | 500 |

</details>

---

**14. What is data seeding, when is it useful, and what should a seed script do?**

<details><summary>Answer</summary>

**Data seeding** is the process of populating a database with an initial set of data programmatically. Instead of manually entering data through an application interface or the MongoDB shell, a seed script automates this process.

**When Data Seeding Is Useful:**

1. **Development Setup**: New developers clone the repo and run one command to have a working database with realistic data.
2. **Testing**: Automated tests need a known, consistent dataset to produce reliable results.
3. **Demos and Presentations**: Quickly populate the application with polished sample data.
4. **After Schema Changes**: When you modify your data models, you may need to repopulate with data that matches the new structure.
5. **Staging Environments**: Set up preview environments with representative data.

**What a Seed Script Should Do:**

1. **Connect** to the database using the same configuration as the application.
2. **Clear** existing data from target collections to ensure a clean state.
3. **Create** sample data, respecting relationships between collections.
4. **Log** results so the developer knows what was created.
5. **Disconnect** and exit the process cleanly.

**Example Seed Script Structure:**

```javascript
const mongoose = require('mongoose');
require('dotenv').config();
const User = require('./models/User');
const Product = require('./models/Product');

const users = [
  { name: 'Alice', email: 'alice@example.com', role: 'admin' },
  { name: 'Bob', email: 'bob@example.com', role: 'user' }
];

const seedDB = async () => {
  try {
    await mongoose.connect(process.env.MONGO_URI);
    console.log('Connected to database');

    // Clear existing data
    await User.deleteMany({});
    await Product.deleteMany({});
    console.log('Existing data cleared');

    // Create users first (products reference users)
    const createdUsers = await User.insertMany(users);
    console.log(`${createdUsers.length} users created`);

    // Create products with user references
    const products = [
      { name: 'Laptop', price: 999, createdBy: createdUsers[0]._id },
      { name: 'Phone', price: 699, createdBy: createdUsers[1]._id }
    ];
    const createdProducts = await Product.insertMany(products);
    console.log(`${createdProducts.length} products created`);

    console.log('Database seeded successfully');
  } catch (error) {
    console.error('Seeding failed:', error.message);
  } finally {
    await mongoose.disconnect();
    process.exit(0);
  }
};

seedDB();
```

**Best Practices:**

- Add `"seed": "node seed.js"` to your `package.json` scripts.
- Use realistic but clearly fake data (avoid real personal information).
- Maintain referential integrity when seeding related collections.
- Support both "seed" (add data) and "destroy" (clear data) modes via command-line flags.

</details>

---

**15. Explain how the MongoDB aggregation pipeline works. Walk through a 3-stage pipeline example.**

<details><summary>Answer</summary>

The **aggregation pipeline** is MongoDB's framework for data processing and transformation. Documents enter the pipeline and pass through a sequence of stages, where each stage transforms the documents and passes the results to the next stage. Think of it like an assembly line where each station performs one specific operation.

**How It Works:**

1. Documents from a collection enter the first stage.
2. Each stage receives documents, processes them, and outputs the results.
3. The output of one stage becomes the input of the next stage.
4. The final stage produces the result set.

**Common Pipeline Stages:**

| Stage | Purpose |
|-------|---------|
| `$match` | Filter documents (like `find()`) |
| `$group` | Group documents and compute aggregates |
| `$sort` | Sort the results |
| `$project` | Reshape documents, include/exclude fields |
| `$lookup` | Join with another collection |
| `$unwind` | Deconstruct an array field |
| `$limit` | Limit the number of results |
| `$skip` | Skip a number of documents |

**3-Stage Pipeline Example:**

Suppose we have an `orders` collection and we want to find the total revenue per product category for completed orders, sorted by revenue:

```javascript
const result = await Order.aggregate([
  // Stage 1: $match - Filter only completed orders
  {
    $match: {
      status: 'completed',
      orderDate: {
        $gte: new Date('2025-01-01'),
        $lt: new Date('2026-01-01')
      }
    }
  },

  // Stage 2: $group - Group by category and calculate totals
  {
    $group: {
      _id: '$category',
      totalRevenue: { $sum: '$totalAmount' },
      orderCount: { $sum: 1 },
      averageOrderValue: { $avg: '$totalAmount' }
    }
  },

  // Stage 3: $sort - Sort by total revenue descending
  {
    $sort: { totalRevenue: -1 }
  }
]);
```

**How Data Flows Through the Pipeline:**

```
Collection (all orders)
        |
  Stage 1: $match
  (only completed orders in 2025)
        |
  [500 documents pass through]
        |
  Stage 2: $group
  (grouped by category with totals)
        |
  [5 grouped documents]
        |
  Stage 3: $sort
  (sorted by revenue, highest first)
        |
  Final Result:
  [
    { _id: "Electronics", totalRevenue: 150000, orderCount: 200, averageOrderValue: 750 },
    { _id: "Clothing", totalRevenue: 85000, orderCount: 340, averageOrderValue: 250 },
    { _id: "Books", totalRevenue: 32000, orderCount: 640, averageOrderValue: 50 },
    ...
  ]
```

**Key Principles:**

1. **Order matters**: Place `$match` early to reduce the number of documents processed by subsequent stages.
2. **Each stage is independent**: It only sees the output from the previous stage, not the original collection.
3. **Performance**: The pipeline is executed on the MongoDB server, not in your Node.js application, making it efficient for large datasets.
4. **Chainable**: You can add as many stages as needed to achieve complex transformations.

</details>

---

## Part 3: Coding Exercises

**16. Write a complete `config/db.js` module that connects Express to MongoDB using Mongoose. Include dotenv configuration, async/await, connection event listeners, and graceful shutdown handling.**

<details><summary>Answer</summary>

```javascript
// config/db.js
const mongoose = require('mongoose');
require('dotenv').config();

// Connect to MongoDB
const connectDB = async () => {
  try {
    const conn = await mongoose.connect(process.env.MONGO_URI, {
      // Mongoose 6+ does not require these options, but they are
      // included here for clarity and backward compatibility
    });

    console.log(`MongoDB Connected: ${conn.connection.host}`);
  } catch (error) {
    console.error(`MongoDB Connection Error: ${error.message}`);
    process.exit(1); // Exit process with failure code
  }
};

// ---- Connection Event Listeners ----

// Fires when the connection is successfully established
mongoose.connection.on('connected', () => {
  console.log('Mongoose connected to the database');
});

// Fires when the connection encounters an error
mongoose.connection.on('error', (err) => {
  console.error(`Mongoose connection error: ${err.message}`);
});

// Fires when the connection is disconnected
mongoose.connection.on('disconnected', () => {
  console.log('Mongoose disconnected from the database');
});

// ---- Graceful Shutdown Handling ----

// Handle application termination (Ctrl+C)
process.on('SIGINT', async () => {
  try {
    await mongoose.connection.close();
    console.log('MongoDB connection closed due to application termination');
    process.exit(0);
  } catch (error) {
    console.error('Error during graceful shutdown:', error.message);
    process.exit(1);
  }
});

// Handle process termination signals (e.g., from hosting platforms)
process.on('SIGTERM', async () => {
  try {
    await mongoose.connection.close();
    console.log('MongoDB connection closed due to SIGTERM');
    process.exit(0);
  } catch (error) {
    console.error('Error during SIGTERM shutdown:', error.message);
    process.exit(1);
  }
});

module.exports = connectDB;
```

**Usage in `server.js`:**

```javascript
// server.js
const express = require('express');
const connectDB = require('./config/db');

const app = express();

// Connect to database
connectDB();

// Middleware
app.use(express.json());

// Routes
app.use('/api/products', require('./routes/productRoutes'));

const PORT = process.env.PORT || 5000;
app.listen(PORT, () => {
  console.log(`Server running on port ${PORT}`);
});
```

**Corresponding `.env` file:**

```
MONGO_URI=mongodb+srv://username:password@cluster.mongodb.net/myapp
PORT=5000
NODE_ENV=development
```

This module provides a robust database connection setup with proper error handling, event monitoring, and clean shutdown behavior for production applications.

</details>

---

**17. Build a complete Product CRUD controller with asyncHandler. Include getAllProducts (with pagination), getProductById (with 404 handling), createProduct (with validation), updateProduct (with runValidators), and deleteProduct. Use a consistent response format.**

<details><summary>Answer</summary>

```javascript
// middleware/asyncHandler.js
const asyncHandler = (fn) => (req, res, next) => {
  Promise.resolve(fn(req, res, next)).catch(next);
};

module.exports = asyncHandler;
```

```javascript
// controllers/productController.js
const Product = require('../models/Product');
const asyncHandler = require('../middleware/asyncHandler');

// @desc    Get all products with pagination
// @route   GET /api/products
// @access  Public
const getAllProducts = asyncHandler(async (req, res) => {
  // Extract pagination parameters from query string
  const page = parseInt(req.query.page, 10) || 1;
  const limit = parseInt(req.query.limit, 10) || 10;
  const skip = (page - 1) * limit;

  // Optional: filter by category if provided
  const filter = {};
  if (req.query.category) {
    filter.category = req.query.category;
  }

  // Execute query with pagination
  const products = await Product.find(filter)
    .sort({ createdAt: -1 })
    .skip(skip)
    .limit(limit);

  // Get total count for pagination metadata
  const total = await Product.countDocuments(filter);

  res.status(200).json({
    success: true,
    data: products,
    pagination: {
      currentPage: page,
      totalPages: Math.ceil(total / limit),
      totalItems: total,
      itemsPerPage: limit
    }
  });
});

// @desc    Get a single product by ID
// @route   GET /api/products/:id
// @access  Public
const getProductById = asyncHandler(async (req, res) => {
  const product = await Product.findById(req.params.id).populate(
    'createdBy',
    'name email'
  );

  // If no product found, throw a 404 error
  if (!product) {
    res.status(404);
    throw new Error('Product not found');
  }

  res.status(200).json({
    success: true,
    data: product
  });
});

// @desc    Create a new product
// @route   POST /api/products
// @access  Private
const createProduct = asyncHandler(async (req, res) => {
  // Destructure and validate required fields
  const { name, description, price, category, stock } = req.body;

  // Check for required fields before attempting to create
  if (!name || !price) {
    res.status(400);
    throw new Error('Please provide at least a name and price');
  }

  // Create the product (Mongoose schema validation will also run)
  const product = await Product.create({
    name,
    description,
    price,
    category,
    stock,
    createdBy: req.body.createdBy
  });

  res.status(201).json({
    success: true,
    data: product
  });
});

// @desc    Update a product
// @route   PUT /api/products/:id
// @access  Private
const updateProduct = asyncHandler(async (req, res) => {
  // Find the product and update it with validation
  const product = await Product.findByIdAndUpdate(
    req.params.id,
    req.body,
    {
      new: true,            // Return the updated document
      runValidators: true   // Run schema validators on update
    }
  );

  // If no product found, throw a 404 error
  if (!product) {
    res.status(404);
    throw new Error('Product not found');
  }

  res.status(200).json({
    success: true,
    data: product
  });
});

// @desc    Delete a product
// @route   DELETE /api/products/:id
// @access  Private
const deleteProduct = asyncHandler(async (req, res) => {
  const product = await Product.findById(req.params.id);

  // If no product found, throw a 404 error
  if (!product) {
    res.status(404);
    throw new Error('Product not found');
  }

  // Remove the product from the database
  await product.deleteOne();

  res.status(200).json({
    success: true,
    data: {},
    message: 'Product deleted successfully'
  });
});

module.exports = {
  getAllProducts,
  getProductById,
  createProduct,
  updateProduct,
  deleteProduct
};
```

**Corresponding Route File:**

```javascript
// routes/productRoutes.js
const express = require('express');
const router = express.Router();
const {
  getAllProducts,
  getProductById,
  createProduct,
  updateProduct,
  deleteProduct
} = require('../controllers/productController');

router.route('/')
  .get(getAllProducts)
  .post(createProduct);

router.route('/:id')
  .get(getProductById)
  .put(updateProduct)
  .delete(deleteProduct);

module.exports = router;
```

This controller demonstrates clean separation of concerns, consistent error handling through asyncHandler, pagination support, and proper use of Mongoose options like `runValidators` and `new`.

</details>

---

**18. Create a global error handling middleware that handles CastError, ValidationError, duplicate key error (code 11000), and a generic fallback. Include a custom AppError class.**

<details><summary>Answer</summary>

```javascript
// utils/AppError.js
class AppError extends Error {
  constructor(message, statusCode) {
    super(message);
    this.statusCode = statusCode;
    this.status = `${statusCode}`.startsWith('4') ? 'fail' : 'error';
    // Operational errors are expected errors we can handle gracefully
    this.isOperational = true;

    // Capture the stack trace, excluding the constructor call
    Error.captureStackTrace(this, this.constructor);
  }
}

module.exports = AppError;
```

```javascript
// middleware/errorHandler.js
const AppError = require('../utils/AppError');

const errorHandler = (err, req, res, next) => {
  // Clone the error properties
  let error = {
    message: err.message,
    statusCode: err.statusCode,
    status: err.status
  };

  // Log the full error in development for debugging
  if (process.env.NODE_ENV === 'development') {
    console.error('ERROR:', err);
  }

  // ---- Handle Specific Error Types ----

  // 1. Mongoose CastError - Invalid ObjectId
  // Triggered when an invalid ID format is passed (e.g., "abc" instead of a valid ObjectId)
  if (err.name === 'CastError') {
    const message = `Invalid ${err.path}: ${err.value}. Expected a valid ObjectId.`;
    error = new AppError(message, 400);
  }

  // 2. Mongoose ValidationError - Schema validation failed
  // Triggered when required fields are missing or values fail validation rules
  if (err.name === 'ValidationError') {
    const messages = Object.values(err.errors).map((val) => val.message);
    const message = `Validation failed: ${messages.join('. ')}`;
    error = new AppError(message, 400);
  }

  // 3. MongoDB Duplicate Key Error - Code 11000
  // Triggered when a unique field (like email) already exists
  if (err.code === 11000) {
    const field = Object.keys(err.keyValue)[0];
    const value = err.keyValue[field];
    const message = `Duplicate value '${value}' for field '${field}'. Please use a different value.`;
    error = new AppError(message, 400);
  }

  // 4. JWT Errors (useful for authentication later)
  if (err.name === 'JsonWebTokenError') {
    error = new AppError('Invalid token. Please log in again.', 401);
  }

  if (err.name === 'TokenExpiredError') {
    error = new AppError('Token expired. Please log in again.', 401);
  }

  // ---- Send Error Response ----

  // Development: send detailed error information
  if (process.env.NODE_ENV === 'development') {
    res.status(error.statusCode || 500).json({
      success: false,
      error: error.message || 'Internal Server Error',
      stack: err.stack,
      fullError: err
    });
  } else {
    // Production: send only the message, no stack trace
    res.status(error.statusCode || 500).json({
      success: false,
      error: error.message || 'Internal Server Error'
    });
  }
};

module.exports = errorHandler;
```

**Registering the Error Handler in `server.js`:**

```javascript
// server.js
const express = require('express');
const AppError = require('./utils/AppError');
const errorHandler = require('./middleware/errorHandler');

const app = express();
app.use(express.json());

// Routes
app.use('/api/products', require('./routes/productRoutes'));
app.use('/api/users', require('./routes/userRoutes'));

// Handle undefined routes - must come after all route definitions
app.all('*', (req, res, next) => {
  next(new AppError(`Cannot find ${req.method} ${req.originalUrl} on this server`, 404));
});

// Global error handler - must be the last middleware
app.use(errorHandler);

module.exports = app;
```

**Using AppError in Controllers:**

```javascript
const AppError = require('../utils/AppError');
const asyncHandler = require('../middleware/asyncHandler');

const getProduct = asyncHandler(async (req, res, next) => {
  const product = await Product.findById(req.params.id);

  if (!product) {
    return next(new AppError('No product found with that ID', 404));
  }

  res.status(200).json({ success: true, data: product });
});
```

This error handling system ensures that every error, whether expected or unexpected, is caught, classified, and returned to the client in a consistent format.

</details>

---

**19. Write a seed script (seed.js) that connects to MongoDB, clears the products and users collections, creates 3 sample users, creates 5 sample products referencing those users, logs results, and disconnects.**

<details><summary>Answer</summary>

```javascript
// seed.js
const mongoose = require('mongoose');
require('dotenv').config();

// Import models
const User = require('./models/User');
const Product = require('./models/Product');

// Sample user data
const sampleUsers = [
  {
    name: 'Alice Johnson',
    email: 'alice@example.com',
    role: 'admin'
  },
  {
    name: 'Bob Smith',
    email: 'bob@example.com',
    role: 'user'
  },
  {
    name: 'Charlie Brown',
    email: 'charlie@example.com',
    role: 'user'
  }
];

// Function to generate product data with user references
const generateProducts = (users) => [
  {
    name: 'Wireless Headphones',
    description: 'High-quality Bluetooth headphones with noise cancellation',
    price: 149.99,
    category: 'Electronics',
    stock: 50,
    inStock: true,
    createdBy: users[0]._id // Alice (admin)
  },
  {
    name: 'Running Shoes',
    description: 'Lightweight running shoes with cushioned sole',
    price: 89.99,
    category: 'Clothing',
    stock: 120,
    inStock: true,
    createdBy: users[1]._id // Bob
  },
  {
    name: 'JavaScript: The Good Parts',
    description: 'A comprehensive guide to the best features of JavaScript',
    price: 29.99,
    category: 'Books',
    stock: 200,
    inStock: true,
    createdBy: users[0]._id // Alice (admin)
  },
  {
    name: 'Mechanical Keyboard',
    description: 'RGB mechanical keyboard with Cherry MX switches',
    price: 129.99,
    category: 'Electronics',
    stock: 0,
    inStock: false,
    createdBy: users[2]._id // Charlie
  },
  {
    name: 'Yoga Mat',
    description: 'Non-slip exercise yoga mat, 6mm thick',
    price: 24.99,
    category: 'Sports',
    stock: 75,
    inStock: true,
    createdBy: users[1]._id // Bob
  }
];

// Main seed function
const seedDatabase = async () => {
  try {
    // Step 1: Connect to the database
    const conn = await mongoose.connect(process.env.MONGO_URI);
    console.log(`Connected to MongoDB: ${conn.connection.host}`);
    console.log('---');

    // Step 2: Clear existing data
    const deletedUsers = await User.deleteMany({});
    const deletedProducts = await Product.deleteMany({});
    console.log(`Cleared ${deletedUsers.deletedCount} existing users`);
    console.log(`Cleared ${deletedProducts.deletedCount} existing products`);
    console.log('---');

    // Step 3: Create sample users
    const createdUsers = await User.insertMany(sampleUsers);
    console.log(`Created ${createdUsers.length} users:`);
    createdUsers.forEach((user) => {
      console.log(`  - ${user.name} (${user.email}) [${user.role}]`);
    });
    console.log('---');

    // Step 4: Create sample products with user references
    const productData = generateProducts(createdUsers);
    const createdProducts = await Product.insertMany(productData);
    console.log(`Created ${createdProducts.length} products:`);
    createdProducts.forEach((product) => {
      console.log(`  - ${product.name} | $${product.price} | ${product.category}`);
    });
    console.log('---');

    // Step 5: Summary
    console.log('Database seeded successfully!');
    console.log(`Total Users: ${createdUsers.length}`);
    console.log(`Total Products: ${createdProducts.length}`);
  } catch (error) {
    console.error('Seeding failed:', error.message);
  } finally {
    // Step 6: Disconnect from the database
    await mongoose.disconnect();
    console.log('Disconnected from MongoDB');
    process.exit(0);
  }
};

// Run the seed function
seedDatabase();
```

**Add to `package.json` scripts:**

```json
{
  "scripts": {
    "start": "node server.js",
    "dev": "nodemon server.js",
    "seed": "node seed.js"
  }
}
```

**Running the script:**

```bash
npm run seed
```

**Expected output:**

```
Connected to MongoDB: cluster0-shard.mongodb.net
---
Cleared 0 existing users
Cleared 0 existing products
---
Created 3 users:
  - Alice Johnson (alice@example.com) [admin]
  - Bob Smith (bob@example.com) [user]
  - Charlie Brown (charlie@example.com) [user]
---
Created 5 products:
  - Wireless Headphones | $149.99 | Electronics
  - Running Shoes | $89.99 | Clothing
  - JavaScript: The Good Parts | $29.99 | Books
  - Mechanical Keyboard | $129.99 | Electronics
  - Yoga Mat | $24.99 | Sports
---
Database seeded successfully!
Total Users: 3
Total Products: 5
Disconnected from MongoDB
```

The script handles errors gracefully and always disconnects from the database in the `finally` block, whether the seeding succeeds or fails.

</details>

---

**20. Write an aggregation pipeline that finds only in-stock products, groups them by category, calculates count, average price, min price, and max price per category, sorts by count descending, and formats the output with $project.**

<details><summary>Answer</summary>

```javascript
// aggregation/productStats.js
const Product = require('../models/Product');

const getProductStatsByCategory = async () => {
  const stats = await Product.aggregate([
    // Stage 1: $match - Filter only in-stock products
    {
      $match: {
        inStock: true,
        stock: { $gt: 0 }
      }
    },

    // Stage 2: $group - Group by category and calculate statistics
    {
      $group: {
        _id: '$category',
        totalProducts: { $sum: 1 },
        averagePrice: { $avg: '$price' },
        minimumPrice: { $min: '$price' },
        maximumPrice: { $max: '$price' },
        totalStockUnits: { $sum: '$stock' }
      }
    },

    // Stage 3: $sort - Sort by product count, highest first
    {
      $sort: { totalProducts: -1 }
    },

    // Stage 4: $project - Format the output for a clean response
    {
      $project: {
        _id: 0, // Hide the default _id field
        category: '$_id', // Rename _id to category
        totalProducts: 1,
        totalStockUnits: 1,
        pricing: {
          average: { $round: ['$averagePrice', 2] },
          min: { $round: ['$minimumPrice', 2] },
          max: { $round: ['$maximumPrice', 2] },
          range: {
            $round: [
              { $subtract: ['$maximumPrice', '$minimumPrice'] },
              2
            ]
          }
        }
      }
    }
  ]);

  return stats;
};

module.exports = getProductStatsByCategory;
```

**Using the Aggregation in a Controller:**

```javascript
// controllers/productController.js
const getProductStatsByCategory = require('../aggregation/productStats');
const asyncHandler = require('../middleware/asyncHandler');

const getProductStats = asyncHandler(async (req, res) => {
  const stats = await getProductStatsByCategory();

  res.status(200).json({
    success: true,
    count: stats.length,
    data: stats
  });
});
```

**Example Output:**

```json
{
  "success": true,
  "count": 3,
  "data": [
    {
      "category": "Electronics",
      "totalProducts": 5,
      "totalStockUnits": 230,
      "pricing": {
        "average": 349.99,
        "min": 29.99,
        "max": 999.99,
        "range": 970.00
      }
    },
    {
      "category": "Clothing",
      "totalProducts": 3,
      "totalStockUnits": 180,
      "pricing": {
        "average": 59.99,
        "min": 19.99,
        "max": 89.99,
        "range": 70.00
      }
    },
    {
      "category": "Books",
      "totalProducts": 2,
      "totalStockUnits": 400,
      "pricing": {
        "average": 34.99,
        "min": 24.99,
        "max": 44.99,
        "range": 20.00
      }
    }
  ]
}
```

**Pipeline Flow Explanation:**

1. **$match**: Filters the collection down to only products where `inStock` is `true` and `stock` is greater than 0. This reduces the dataset early for better performance.
2. **$group**: Groups the remaining documents by their `category` field. For each group, it calculates the count (`$sum: 1`), average price, minimum price, maximum price, and total stock units.
3. **$sort**: Orders the grouped results by `totalProducts` in descending order so the most populated categories appear first.
4. **$project**: Reshapes each document for a cleaner API response. It renames `_id` to `category`, rounds decimal values to 2 places, calculates the price range, and nests pricing data into a sub-object.

</details>

---

## Part 4: Database Phase Review (Weeks 28-31)

**21. How does a MongoDB document differ from a row in a SQL database?**

- A) MongoDB documents must follow a strict schema; SQL rows can be flexible
- B) MongoDB documents are stored as BSON and can have nested structures and varying fields; SQL rows follow a fixed schema with flat columns
- C) MongoDB documents can only contain string values
- D) There is no difference; they are functionally identical

<details><summary>Answer</summary>

**B) MongoDB documents are stored as BSON and can have nested structures and varying fields; SQL rows follow a fixed schema with flat columns**

MongoDB documents are stored in BSON (Binary JSON) format and offer significant flexibility compared to SQL rows:

| Feature | MongoDB Document | SQL Row |
|---------|-----------------|---------|
| Format | BSON (JSON-like) | Fixed columns |
| Schema | Flexible (schema-less by default) | Rigid (predefined schema) |
| Nesting | Supports embedded documents and arrays | Flat structure (requires JOINs) |
| Fields | Can vary between documents in the same collection | Every row has the same columns |
| Data types | Rich types including arrays, objects, ObjectId | Standard SQL types |

```javascript
// MongoDB document - flexible, nested structure
{
  _id: ObjectId("507f1f77bcf86cd799439011"),
  name: "John Doe",
  address: {                    // Embedded document
    street: "123 Main St",
    city: "New York"
  },
  hobbies: ["reading", "coding"] // Array field
}
```

</details>

---

**22. Which of the following is NOT a valid Mongoose schema type?**

- A) `mongoose.Schema.Types.ObjectId`
- B) `mongoose.Schema.Types.Decimal128`
- C) `mongoose.Schema.Types.Float`
- D) `mongoose.Schema.Types.Mixed`

<details><summary>Answer</summary>

**C) `mongoose.Schema.Types.Float`**

Mongoose does not have a `Float` schema type. For decimal/floating-point numbers, you use the `Number` type or `Decimal128` for precise decimal arithmetic. The valid Mongoose schema types are:

| Type | Description |
|------|-------------|
| `String` | Text data |
| `Number` | Integer or floating-point numbers |
| `Boolean` | True/false values |
| `Date` | Date and time values |
| `Buffer` | Binary data |
| `ObjectId` | MongoDB ObjectId references |
| `Array` | Arrays of any type |
| `Decimal128` | High-precision decimal numbers |
| `Map` | Key-value pairs |
| `Mixed` | Any data type (schema-less) |
| `UUID` | Universally unique identifiers |

```javascript
const schema = new mongoose.Schema({
  name: String,
  price: Number,              // Handles both integers and floats
  preciseCost: mongoose.Schema.Types.Decimal128, // High precision
  metadata: mongoose.Schema.Types.Mixed          // Any structure
});
```

</details>

---

**23. What is the key difference between embedding and referencing in MongoDB data modeling?**

- A) Embedding is faster for writes; referencing is faster for reads
- B) Embedding stores related data inside the parent document; referencing stores a link (ObjectId) to data in a separate collection
- C) Embedding is only used for arrays; referencing is only used for objects
- D) There is no practical difference between the two approaches

<details><summary>Answer</summary>

**B) Embedding stores related data inside the parent document; referencing stores a link (ObjectId) to data in a separate collection**

These are the two fundamental strategies for representing relationships in MongoDB:

**Embedding (Denormalization):**

```javascript
// The address data is embedded directly inside the user document
{
  name: "Alice",
  address: {
    street: "123 Main St",
    city: "New York",
    zip: "10001"
  }
}
```

**Referencing (Normalization):**

```javascript
// User document stores only a reference to the address
{ name: "Alice", addressId: ObjectId("60d5f484...") }

// Address is stored in a separate collection
{ _id: ObjectId("60d5f484..."), street: "123 Main St", city: "New York" }
```

| Criteria | Embedding | Referencing |
|----------|-----------|-------------|
| Read performance | Faster (single query) | Slower (requires populate/lookup) |
| Write performance | Slower for large subdocuments | Faster for updates to related data |
| Data duplication | Possible | Avoided |
| Document size | Can grow large (16MB limit) | Stays small |
| Best for | One-to-few, data read together | One-to-many, shared/large data |

</details>

---

**24. Which MongoDB query operator is used to match documents where a field's value is in a specified array of values?**

- A) `$contains`
- B) `$in`
- C) `$includes`
- D) `$match`

<details><summary>Answer</summary>

**B) `$in`**

The `$in` operator selects documents where the value of a field equals any value in the specified array. It is the MongoDB equivalent of SQL's `IN` clause:

```javascript
// Find products in specific categories
const products = await Product.find({
  category: { $in: ['Electronics', 'Books', 'Sports'] }
});

// Find users with specific roles
const users = await User.find({
  role: { $in: ['admin', 'moderator'] }
});

// SQL equivalent: SELECT * FROM products WHERE category IN ('Electronics', 'Books', 'Sports')
```

Related operators include `$nin` (not in), which matches documents where the field value is not in the array, and `$all`, which matches documents where an array field contains all specified values.

</details>

---

**25. What does the `$lookup` stage do in a MongoDB aggregation pipeline?**

- A) It searches for text within documents
- B) It performs a left outer join with another collection in the same database
- C) It creates an index on a specified field
- D) It validates document structure against a schema

<details><summary>Answer</summary>

**B) It performs a left outer join with another collection in the same database**

`$lookup` is MongoDB's aggregation stage for joining data from two collections, similar to a LEFT JOIN in SQL. It adds an array field to each input document containing matching documents from the "joined" collection:

```javascript
const ordersWithProducts = await Order.aggregate([
  {
    $lookup: {
      from: 'products',        // The collection to join with
      localField: 'productId', // Field from the input documents
      foreignField: '_id',     // Field from the "from" collection
      as: 'productDetails'     // Output array field name
    }
  },
  {
    $unwind: '$productDetails' // Convert the array to a single object
  }
]);
```

Key points about `$lookup`:
- It always produces an array in the output field, even if there is only one match.
- Use `$unwind` after `$lookup` to flatten the result if you expect a one-to-one relationship.
- The `from` value must be the actual collection name in MongoDB (typically lowercase and plural), not the Mongoose model name.
- It is the aggregation pipeline equivalent of Mongoose's `.populate()` method, but runs entirely on the database server.

</details>

---

**26. Explain the journey of data interaction from the MongoDB shell (Week 28) to a full Express API (Week 31). How does each layer build upon the previous one?**

<details><summary>Answer</summary>

The database phase of this course follows a progressive learning path where each week adds a new layer of abstraction and functionality:

**Week 28: MongoDB Fundamentals (Raw Shell)**

In the first week, you interacted with MongoDB directly through the `mongosh` shell. You learned the core CRUD operations without any abstraction layer:

```javascript
// Direct MongoDB shell commands
db.products.insertOne({ name: "Laptop", price: 999 });
db.products.find({ price: { $gt: 500 } });
db.products.updateOne({ name: "Laptop" }, { $set: { price: 899 } });
db.products.deleteOne({ name: "Laptop" });
```

This gave you a foundational understanding of how MongoDB stores and retrieves data.

**Week 29: Mongoose ODM (Schema Layer)**

Mongoose added structure on top of MongoDB. Instead of working with raw documents, you defined schemas with types, validation, and defaults:

```javascript
const productSchema = new mongoose.Schema({
  name: { type: String, required: true },
  price: { type: Number, min: 0 },
  category: { type: String, enum: ['Electronics', 'Books'] }
});
const Product = mongoose.model('Product', productSchema);
```

This layer provided data validation, type casting, middleware hooks, and a more intuitive query API.

**Week 30: Advanced Queries and Aggregation (Data Processing Layer)**

You learned to perform complex data operations: filtering, sorting, pagination, population (joins), and aggregation pipelines:

```javascript
const stats = await Product.aggregate([
  { $match: { inStock: true } },
  { $group: { _id: "$category", avgPrice: { $avg: "$price" } } }
]);
```

This layer transformed MongoDB from a simple data store into a powerful data processing engine.

**Week 31: Express Integration (API Layer)**

Finally, you combined everything into a complete REST API. The Express layer wraps all previous knowledge into HTTP endpoints accessible by any client:

```
Client Request --> Express Router --> Controller --> Mongoose Model --> MongoDB
     |                                                                    |
     <-------- JSON Response <-- Error Handler <-- Query Result <---------
```

Each layer builds upon the last:
- **MongoDB** provides the storage engine.
- **Mongoose** provides structure, validation, and a developer-friendly API.
- **Advanced queries** provide powerful data retrieval and processing.
- **Express** provides the HTTP interface that connects your database to the outside world.

The MVC pattern, error handling, environment configuration, and seed scripts complete the picture, turning raw database knowledge into a production-ready API.

</details>

---

**27. Compare `findById()`, `findOne()`, and `find()` in Mongoose. When would you use each one?**

<details><summary>Answer</summary>

These three methods are the primary ways to retrieve documents from MongoDB using Mongoose. Each serves a different purpose:

**`find()` - Retrieve Multiple Documents**

Returns an array of all documents matching the query. If no query is provided, it returns all documents in the collection:

```javascript
// Get all products
const allProducts = await Product.find();

// Get products in a specific category
const electronics = await Product.find({ category: 'Electronics' });

// Get products with price > 100 and in stock
const filtered = await Product.find({ price: { $gt: 100 }, inStock: true });

// Returns: [] (empty array if no matches)
```

**`findOne()` - Retrieve a Single Document by Any Criteria**

Returns the first document matching the query, or `null` if no match is found:

```javascript
// Find a user by email (not by ID)
const user = await User.findOne({ email: 'alice@example.com' });

// Find the most expensive product
const priciest = await Product.findOne().sort({ price: -1 });

// Returns: null (if no match)
```

**`findById()` - Retrieve a Single Document by its _id**

A shorthand for `findOne({ _id: id })`. It is specifically designed for looking up documents by their unique identifier:

```javascript
// Find a specific product by its ObjectId
const product = await Product.findById('507f1f77bcf86cd799439011');

// Equivalent to:
const product = await Product.findOne({ _id: '507f1f77bcf86cd799439011' });

// Returns: null (if no match)
```

**Comparison Table:**

| Feature | `find()` | `findOne()` | `findById()` |
|---------|----------|-------------|--------------|
| Returns | Array of documents | Single document or null | Single document or null |
| Use case | List/search | Lookup by any field | Lookup by `_id` |
| Common in | GET /api/products | Login (find by email) | GET /api/products/:id |
| Query | Any filter object | Any filter object | Only an `_id` value |
| No match | Empty array `[]` | `null` | `null` |

**When to Use Each:**

- Use `find()` when building list endpoints, search features, or any query that could return multiple results.
- Use `findOne()` when you need a single document based on a field other than `_id`, such as looking up a user by email or username.
- Use `findById()` when you have the document's `_id`, which is the most common case in RESTful APIs when handling requests like `GET /api/products/:id`.

</details>

---

**28. When should you create an index on a MongoDB collection field?**

- A) On every field in the collection for maximum performance
- B) On fields that are frequently used in query filters, sort operations, or unique constraints
- C) Only on the `_id` field
- D) Indexes should be avoided because they slow down all operations

<details><summary>Answer</summary>

**B) On fields that are frequently used in query filters, sort operations, or unique constraints**

Indexes improve read performance by allowing MongoDB to locate documents without scanning the entire collection. However, they come with trade-offs and should be created strategically:

**When to Create Indexes:**

1. **Frequently queried fields**: Fields used in `find()`, `$match`, or `WHERE` conditions.
2. **Sort fields**: Fields used in `.sort()` operations.
3. **Unique constraints**: Fields that must be unique across all documents (like email).
4. **Foreign key fields**: Fields storing ObjectId references used in `$lookup` or `.populate()`.

**When NOT to Create Indexes:**

1. **Small collections**: Collections with fewer than a few hundred documents gain little benefit.
2. **Rarely queried fields**: Indexes on unused fields waste storage and slow down writes.
3. **High-write, low-read collections**: Every insert and update must also update the index.

```javascript
// Creating indexes in a Mongoose schema
const userSchema = new mongoose.Schema({
  email: { type: String, unique: true, index: true },
  name: String,
  createdAt: { type: Date, index: true }
});

// Compound index for queries that filter by multiple fields
userSchema.index({ role: 1, createdAt: -1 });
```

MongoDB automatically creates an index on the `_id` field. All other indexes must be created explicitly based on your application's query patterns.

</details>

---

**29. What are Mongoose middleware (pre/post hooks), and when are they executed?**

- A) They are Express middleware functions that run before route handlers
- B) They are functions that run before or after specific Mongoose operations like save, validate, and remove
- C) They are database triggers that run inside MongoDB
- D) They are authentication checks performed before database access

<details><summary>Answer</summary>

**B) They are functions that run before or after specific Mongoose operations like save, validate, and remove**

Mongoose middleware (also called hooks) are functions that intercept Mongoose operations at specific points. They allow you to execute custom logic before (`pre`) or after (`post`) operations like saving, validating, updating, or removing documents:

```javascript
const userSchema = new mongoose.Schema({
  name: String,
  email: String,
  password: String
});

// Pre-save hook: runs before the document is saved
userSchema.pre('save', async function (next) {
  // Only hash the password if it has been modified
  if (!this.isModified('password')) return next();
  this.password = await bcrypt.hash(this.password, 10);
  next();
});

// Post-save hook: runs after the document is saved
userSchema.post('save', function (doc) {
  console.log(`New user saved: ${doc.email}`);
});

// Pre-find hook: runs before any find query
userSchema.pre(/^find/, function (next) {
  // Automatically exclude inactive users from all queries
  this.where({ isActive: true });
  next();
});
```

Common use cases include password hashing before save, logging after operations, automatically updating timestamps, cascading deletes, and data sanitization. Middleware must be defined on the schema before compiling it into a model with `mongoose.model()`.

</details>

---

**30. Write a complete mini-API for a "Book" resource. Include the Mongoose model with validation, a controller with at least 3 CRUD operations using asyncHandler, and the route file. The Book should have title (required), author (required), isbn (unique), pages (min 1), and genre (enum).**

<details><summary>Answer</summary>

```javascript
// models/Book.js
const mongoose = require('mongoose');

const bookSchema = new mongoose.Schema(
  {
    title: {
      type: String,
      required: [true, 'Book title is required'],
      trim: true,
      maxlength: [200, 'Title cannot exceed 200 characters']
    },
    author: {
      type: String,
      required: [true, 'Author name is required'],
      trim: true
    },
    isbn: {
      type: String,
      unique: true,
      sparse: true, // Allows multiple documents without isbn
      trim: true
    },
    pages: {
      type: Number,
      min: [1, 'A book must have at least 1 page']
    },
    genre: {
      type: String,
      enum: {
        values: ['Fiction', 'Non-Fiction', 'Science', 'Technology', 'History', 'Biography', 'Fantasy'],
        message: '{VALUE} is not a supported genre'
      }
    },
    publishedDate: {
      type: Date
    },
    isAvailable: {
      type: Boolean,
      default: true
    }
  },
  {
    timestamps: true // Adds createdAt and updatedAt automatically
  }
);

// Index for common query patterns
bookSchema.index({ author: 1, genre: 1 });

module.exports = mongoose.model('Book', bookSchema);
```

```javascript
// middleware/asyncHandler.js
const asyncHandler = (fn) => (req, res, next) => {
  Promise.resolve(fn(req, res, next)).catch(next);
};

module.exports = asyncHandler;
```

```javascript
// controllers/bookController.js
const Book = require('../models/Book');
const asyncHandler = require('../middleware/asyncHandler');

// @desc    Get all books (with optional genre filter and pagination)
// @route   GET /api/books
const getAllBooks = asyncHandler(async (req, res) => {
  const page = parseInt(req.query.page, 10) || 1;
  const limit = parseInt(req.query.limit, 10) || 10;
  const skip = (page - 1) * limit;

  // Build filter object from query parameters
  const filter = {};
  if (req.query.genre) filter.genre = req.query.genre;
  if (req.query.author) filter.author = new RegExp(req.query.author, 'i');

  const books = await Book.find(filter)
    .sort({ createdAt: -1 })
    .skip(skip)
    .limit(limit);

  const total = await Book.countDocuments(filter);

  res.status(200).json({
    success: true,
    data: books,
    pagination: {
      currentPage: page,
      totalPages: Math.ceil(total / limit),
      totalItems: total
    }
  });
});

// @desc    Get a single book by ID
// @route   GET /api/books/:id
const getBookById = asyncHandler(async (req, res) => {
  const book = await Book.findById(req.params.id);

  if (!book) {
    res.status(404);
    throw new Error('Book not found');
  }

  res.status(200).json({
    success: true,
    data: book
  });
});

// @desc    Create a new book
// @route   POST /api/books
const createBook = asyncHandler(async (req, res) => {
  const { title, author, isbn, pages, genre, publishedDate } = req.body;

  if (!title || !author) {
    res.status(400);
    throw new Error('Title and author are required');
  }

  const book = await Book.create({
    title,
    author,
    isbn,
    pages,
    genre,
    publishedDate
  });

  res.status(201).json({
    success: true,
    data: book
  });
});

// @desc    Update a book
// @route   PUT /api/books/:id
const updateBook = asyncHandler(async (req, res) => {
  const book = await Book.findByIdAndUpdate(
    req.params.id,
    req.body,
    { new: true, runValidators: true }
  );

  if (!book) {
    res.status(404);
    throw new Error('Book not found');
  }

  res.status(200).json({
    success: true,
    data: book
  });
});

// @desc    Delete a book
// @route   DELETE /api/books/:id
const deleteBook = asyncHandler(async (req, res) => {
  const book = await Book.findById(req.params.id);

  if (!book) {
    res.status(404);
    throw new Error('Book not found');
  }

  await book.deleteOne();

  res.status(200).json({
    success: true,
    data: {},
    message: 'Book deleted successfully'
  });
});

module.exports = {
  getAllBooks,
  getBookById,
  createBook,
  updateBook,
  deleteBook
};
```

```javascript
// routes/bookRoutes.js
const express = require('express');
const router = express.Router();
const {
  getAllBooks,
  getBookById,
  createBook,
  updateBook,
  deleteBook
} = require('../controllers/bookController');

// Routes for /api/books
router.route('/')
  .get(getAllBooks)
  .post(createBook);

// Routes for /api/books/:id
router.route('/:id')
  .get(getBookById)
  .put(updateBook)
  .delete(deleteBook);

module.exports = router;
```

**Mounting in `server.js`:**

```javascript
const bookRoutes = require('./routes/bookRoutes');
app.use('/api/books', bookRoutes);
```

**API Endpoints Summary:**

| Method | Endpoint | Description |
|--------|----------|-------------|
| GET | `/api/books` | Get all books (supports `?genre=Fiction&page=1&limit=10`) |
| GET | `/api/books/:id` | Get a specific book by ID |
| POST | `/api/books` | Create a new book |
| PUT | `/api/books/:id` | Update an existing book |
| DELETE | `/api/books/:id` | Delete a book |

This mini-API demonstrates the complete MVC pattern with Mongoose validation, asyncHandler for error catching, pagination, filtering, and proper HTTP status codes.

</details>
