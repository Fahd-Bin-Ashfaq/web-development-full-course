# Week 29 — Mongoose ODM

> **Prerequisites:** Week 28 (MongoDB fundamentals, CRUD in MongoDB Shell)
> **Goal:** Learn Mongoose — the standard ODM for MongoDB in Node.js. Define schemas, create models, perform CRUD, and add validation to your data.

---

## Table of Contents

1. [What is Mongoose?](#1-what-is-mongoose)
2. [Why Mongoose Over the Raw MongoDB Driver?](#2-why-mongoose-over-the-raw-mongodb-driver)
3. [Installing and Connecting](#3-installing-and-connecting)
4. [Schemas — Defining Structure](#4-schemas--defining-structure)
5. [Models — The Interface to MongoDB](#5-models--the-interface-to-mongodb)
6. [CRUD with Mongoose](#6-crud-with-mongoose)
7. [Schema Validation](#7-schema-validation)
8. [Timestamps](#8-timestamps)
9. [Virtuals](#9-virtuals)
10. [Instance Methods](#10-instance-methods)
11. [Static Methods](#11-static-methods)
12. [Summary](#12-summary)

---

## 1. What is Mongoose?

**Mongoose** is an **Object Data Modeling (ODM)** library for MongoDB and Node.js. It provides a structured, schema-based approach to working with MongoDB data.

> Think of Mongoose as a **building inspector** for your database. MongoDB is like an open construction site where you can build anything in any shape — no rules, no inspections. Mongoose steps in as the inspector who says: "Every house MUST have a foundation (required fields), the walls MUST be a certain height (validation), and the electrical wiring MUST follow a standard (data types)." You still have the flexibility of MongoDB, but Mongoose adds safety and consistency.

### Where Mongoose Fits

```
  +-----------------------------------------------------------+
  |                    YOUR EXPRESS APP                        |
  |  (Routes, Controllers, Business Logic)                    |
  +-----------------------------------------------------------+
  |                      MONGOOSE (ODM)                       |
  |  (Schemas, Models, Validation, Query Helpers)             |
  +-----------------------------------------------------------+
  |                  MONGODB NODE.js DRIVER                   |
  |  (Low-level connection, raw commands)                     |
  +-----------------------------------------------------------+
  |                    MONGODB SERVER                          |
  |  (Database engine, storage, indexing)                      |
  +-----------------------------------------------------------+
```

### Key Facts

| Fact                   | Detail                                             |
|------------------------|----------------------------------------------------|
| **Created**            | 2010 by Valeri Karpov (at Cisco)                   |
| **npm downloads**      | 3+ million per week                                |
| **Purpose**            | Schema-based data modeling for MongoDB             |
| **Relationship**       | Sits on top of the official MongoDB Node.js driver |
| **Version**            | Mongoose 7+ (modern async/await support)           |

---

## 2. Why Mongoose Over the Raw MongoDB Driver?

You can interact with MongoDB using the official `mongodb` npm package (the raw driver). It works, but Mongoose adds powerful features that save time and prevent bugs.

### Side-by-Side Comparison

**Raw MongoDB Driver:**

```javascript
const { MongoClient } = require("mongodb");

async function createUser() {
  const client = new MongoClient("mongodb://localhost:27017");
  await client.connect();
  const db = client.db("myApp");

  // No validation — you can insert ANYTHING
  await db.collection("users").insertOne({
    naem: "Ali",       // Typo in field name — no error!
    age: "twenty-five", // String instead of number — no error!
    email: 12345        // Number instead of string — no error!
  });

  await client.close();
}
```

**Mongoose:**

```javascript
const mongoose = require("mongoose");

// Define a strict schema
const userSchema = new mongoose.Schema({
  name:  { type: String, required: true },
  age:   { type: Number, required: true },
  email: { type: String, required: true }
});

const User = mongoose.model("User", userSchema);

async function createUser() {
  await mongoose.connect("mongodb://localhost:27017/myApp");

  // Mongoose validates — errors catch mistakes early
  await User.create({
    naem: "Ali",        // "naem" is not in schema — silently ignored
    age: "twenty-five", // Fails: not a valid number
    email: 12345        // Fails: not a valid string
  });
}
```

### Feature Comparison

| Feature                | Raw MongoDB Driver       | Mongoose                         |
|------------------------|--------------------------|----------------------------------|
| **Schema enforcement** | None                     | Strict schemas with types        |
| **Validation**         | Manual                   | Built-in + custom validators     |
| **Type casting**       | None                     | Automatic (`"25"` becomes `25`)  |
| **Middleware (hooks)** | None                     | Pre/post save, validate, remove  |
| **Populate (JOINs)**   | Manual `$lookup`         | Simple `.populate()` method      |
| **Virtuals**           | None                     | Computed properties              |
| **Query helpers**      | Basic                    | Chainable, expressive queries    |

---

## 3. Installing and Connecting

### Installation

```bash
# Initialize a project (if not already done)
npm init -y

# Install Mongoose
npm install mongoose
```

### Basic Connection

```javascript
const mongoose = require("mongoose");

// Connect to MongoDB
mongoose.connect("mongodb://localhost:27017/myApp")
  .then(() => console.log("Connected to MongoDB"))
  .catch((err) => console.error("Connection failed:", err));
```

### Connection with Options (Recommended)

```javascript
const mongoose = require("mongoose");

const connectDB = async () => {
  try {
    const conn = await mongoose.connect("mongodb://localhost:27017/myApp");
    console.log(`MongoDB Connected: ${conn.connection.host}`);
  } catch (error) {
    console.error(`Error: ${error.message}`);
    process.exit(1);  // Exit process with failure
  }
};

module.exports = connectDB;
```

### Connection to Atlas

```javascript
const mongoose = require("mongoose");

// Replace with your actual Atlas connection string
const MONGO_URI = "mongodb+srv://username:password@cluster0.xxxxx.mongodb.net/myApp?retryWrites=true&w=majority";

mongoose.connect(MONGO_URI)
  .then(() => console.log("Connected to MongoDB Atlas"))
  .catch((err) => console.error("Atlas connection failed:", err));
```

### Connection Events

```javascript
const mongoose = require("mongoose");

// Monitor connection events
mongoose.connection.on("connected", () => {
  console.log("Mongoose connected to MongoDB");
});

mongoose.connection.on("error", (err) => {
  console.error("Mongoose connection error:", err);
});

mongoose.connection.on("disconnected", () => {
  console.log("Mongoose disconnected");
});

// Graceful shutdown
process.on("SIGINT", async () => {
  await mongoose.connection.close();
  console.log("Mongoose connection closed due to app termination");
  process.exit(0);
});
```

### Connection Flow Diagram

```
  Your App                 Mongoose                MongoDB Server
  --------                 --------                --------------
     |                        |                         |
     |  mongoose.connect()    |                         |
     |----------------------->|                         |
     |                        |   TCP connection        |
     |                        |------------------------>|
     |                        |   Authentication        |
     |                        |<----------------------->|
     |                        |   Connection pooling    |
     |  Promise resolved      |<----------------------->|
     |<-----------------------|                         |
     |                        |                         |
     |  User.create({...})    |                         |
     |----------------------->|  Validate schema        |
     |                        |  Cast types             |
     |                        |  insertOne()            |
     |                        |------------------------>|
     |                        |  Result                 |
     |  Document returned     |<------------------------|
     |<-----------------------|                         |
```

---

## 4. Schemas — Defining Structure

A **Schema** defines the shape of documents in a MongoDB collection. It specifies field names, data types, default values, and validation rules.

### Basic Schema

```javascript
const mongoose = require("mongoose");

const userSchema = new mongoose.Schema({
  name: String,
  email: String,
  age: Number,
  isActive: Boolean
});
```

### Schema with Detailed Configuration

```javascript
const userSchema = new mongoose.Schema({
  name: {
    type: String,
    required: true,
    trim: true,              // Removes whitespace from both ends
    minlength: 2,
    maxlength: 50
  },
  email: {
    type: String,
    required: true,
    unique: true,            // Creates a unique index
    lowercase: true          // Converts to lowercase before saving
  },
  age: {
    type: Number,
    min: 0,
    max: 120,
    default: 18              // Default value if not provided
  },
  role: {
    type: String,
    enum: ["user", "admin", "moderator"],  // Only these values allowed
    default: "user"
  },
  hobbies: {
    type: [String],          // Array of strings
    default: []
  },
  address: {
    street: String,          // Nested object (subdocument)
    city: String,
    country: { type: String, default: "Pakistan" }
  },
  joinedAt: {
    type: Date,
    default: Date.now        // Auto-set to current date
  }
});
```

### Supported Schema Types

| Type           | Example                          | Description                     |
|----------------|----------------------------------|---------------------------------|
| `String`       | `name: String`                   | Text values                     |
| `Number`       | `age: Number`                    | Integer or floating-point       |
| `Boolean`      | `isActive: Boolean`              | True or false                   |
| `Date`         | `createdAt: Date`                | Date/time values                |
| `Buffer`       | `photo: Buffer`                  | Binary data                     |
| `ObjectId`     | `author: Schema.Types.ObjectId`  | Reference to another document   |
| `Array`        | `tags: [String]`                 | Array of any type               |
| `Map`          | `meta: Map`                      | Key-value pairs                 |
| `Schema.Types.Mixed` | `data: Schema.Types.Mixed` | Any type (no validation)        |
| `Decimal128`   | `price: Schema.Types.Decimal128` | High-precision decimals         |

### Schema Options

```javascript
const userSchema = new mongoose.Schema(
  {
    name: String,
    email: String
  },
  {
    timestamps: true,          // Adds createdAt and updatedAt
    versionKey: false,         // Removes __v field
    toJSON: { virtuals: true },// Include virtuals in JSON output
    toObject: { virtuals: true }
  }
);
```

---

## 5. Models — The Interface to MongoDB

A **Model** is a compiled version of a Schema. It provides the interface for creating, reading, updating, and deleting documents in the corresponding MongoDB collection.

### Creating a Model

```javascript
const mongoose = require("mongoose");

// Step 1: Define the schema
const productSchema = new mongoose.Schema({
  name: { type: String, required: true },
  price: { type: Number, required: true },
  category: { type: String, required: true },
  inStock: { type: Boolean, default: true }
});

// Step 2: Create the model
// mongoose.model("ModelName", schema)
// "Product" -> MongoDB creates a "products" collection (lowercase + plural)
const Product = mongoose.model("Product", productSchema);

module.exports = Product;
```

### How Models Map to Collections

```
  Model Name          Collection Name (MongoDB)
  ----------          -------------------------
  "User"       --->   "users"
  "Product"    --->   "products"
  "Category"   --->   "categories"
  "Person"     --->   "people"
  "BlogPost"   --->   "blogposts"
```

Mongoose automatically converts the model name to lowercase and pluralizes it. You can override this behavior:

```javascript
// Force a specific collection name
const userSchema = new mongoose.Schema({ name: String }, { collection: "app_users" });
```

### Typical File Structure

```
  project/
  +-- models/
  |   +-- User.js           // User schema + model
  |   +-- Product.js        // Product schema + model
  |   +-- Order.js          // Order schema + model
  +-- config/
  |   +-- db.js             // Database connection
  +-- server.js             // Entry point
```

**models/User.js:**

```javascript
const mongoose = require("mongoose");

const userSchema = new mongoose.Schema({
  name: { type: String, required: true },
  email: { type: String, required: true, unique: true },
  age: { type: Number, default: 18 }
});

module.exports = mongoose.model("User", userSchema);
```

**config/db.js:**

```javascript
const mongoose = require("mongoose");

const connectDB = async () => {
  try {
    await mongoose.connect("mongodb://localhost:27017/myApp");
    console.log("MongoDB Connected");
  } catch (error) {
    console.error("Connection failed:", error.message);
    process.exit(1);
  }
};

module.exports = connectDB;
```

**server.js:**

```javascript
const express = require("express");
const connectDB = require("./config/db");
const User = require("./models/User");

const app = express();
app.use(express.json());

// Connect to database
connectDB();

app.listen(3000, () => console.log("Server running on port 3000"));
```

---

## 6. CRUD with Mongoose

### 6.1 CREATE — Adding Documents

**Using `Model.create()`:**

```javascript
const User = require("./models/User");

// Create a single user
const newUser = await User.create({
  name: "Ali Ahmed",
  email: "ali@example.com",
  age: 25
});

console.log(newUser);
// {
//   _id: ObjectId("..."),
//   name: "Ali Ahmed",
//   email: "ali@example.com",
//   age: 25,
//   __v: 0
// }
```

**Using `new Model()` + `.save()`:**

```javascript
const user = new User({
  name: "Sara Khan",
  email: "sara@example.com",
  age: 30
});

// The document is NOT saved yet — it only exists in memory
console.log(user.isNew);  // true

// Now save it to the database
await user.save();

console.log(user.isNew);  // false
```

**Create multiple documents:**

```javascript
const users = await User.create([
  { name: "Omar", email: "omar@example.com", age: 22 },
  { name: "Fatima", email: "fatima@example.com", age: 28 }
]);
```

### When to Use `create()` vs `new + save()`

| Method             | Use When                                          |
|--------------------|---------------------------------------------------|
| `Model.create()`   | Simple creation, no pre-save modifications needed |
| `new Model + save` | Need to modify the document before saving         |

### 6.2 READ — Finding Documents

**Find all documents:**

```javascript
const users = await User.find();
// Returns an array of all user documents
```

**Find with filter:**

```javascript
// Find all users in Karachi
const karachiUsers = await User.find({ city: "Karachi" });

// Find users older than 25
const olderUsers = await User.find({ age: { $gt: 25 } });
```

**Find one document:**

```javascript
// Find the first matching document
const user = await User.findOne({ email: "ali@example.com" });
```

**Find by ID:**

```javascript
// Find a specific document by its _id
const user = await User.findById("6578a1b2c3d4e5f6a7b8c9d0");
```

**Select specific fields:**

```javascript
// Only return name and email
const users = await User.find().select("name email");

// Exclude a field
const users = await User.find().select("-__v");
```

### 6.3 UPDATE — Modifying Documents

**Find by ID and update:**

```javascript
const updatedUser = await User.findByIdAndUpdate(
  "6578a1b2c3d4e5f6a7b8c9d0",     // ID to find
  { age: 26, city: "Dubai" },       // Fields to update
  { new: true, runValidators: true } // Options
);
// { new: true }           -> Return the UPDATED document (not the old one)
// { runValidators: true } -> Run schema validation on the update
```

**Find one and update:**

```javascript
const updatedUser = await User.findOneAndUpdate(
  { email: "ali@example.com" },     // Filter
  { $inc: { age: 1 } },             // Increment age by 1
  { new: true }
);
```

**Update many:**

```javascript
const result = await User.updateMany(
  { isActive: false },               // Filter
  { $set: { isActive: true } }       // Update
);
console.log(result.modifiedCount);    // Number of documents modified
```

### 6.4 DELETE — Removing Documents

**Find by ID and delete:**

```javascript
const deletedUser = await User.findByIdAndDelete("6578a1b2c3d4e5f6a7b8c9d0");
console.log(deletedUser); // The deleted document (or null if not found)
```

**Find one and delete:**

```javascript
const deletedUser = await User.findOneAndDelete({ email: "ali@example.com" });
```

**Delete many:**

```javascript
const result = await User.deleteMany({ isActive: false });
console.log(result.deletedCount); // Number of deleted documents
```

### CRUD Method Summary

```
  +---------------------+--------------------------------------------+
  |     Operation        |    Mongoose Methods                        |
  +---------------------+--------------------------------------------+
  |     CREATE           |    Model.create()                          |
  |                      |    new Model() + .save()                   |
  +---------------------+--------------------------------------------+
  |     READ             |    Model.find()                            |
  |                      |    Model.findOne()                         |
  |                      |    Model.findById()                        |
  +---------------------+--------------------------------------------+
  |     UPDATE           |    Model.findByIdAndUpdate()               |
  |                      |    Model.findOneAndUpdate()                |
  |                      |    Model.updateMany()                      |
  +---------------------+--------------------------------------------+
  |     DELETE           |    Model.findByIdAndDelete()               |
  |                      |    Model.findOneAndDelete()                |
  |                      |    Model.deleteMany()                      |
  +---------------------+--------------------------------------------+
```

---

## 7. Schema Validation

Mongoose provides powerful built-in validators and supports custom validation functions.

### Built-in Validators

```javascript
const productSchema = new mongoose.Schema({
  name: {
    type: String,
    required: [true, "Product name is required"],   // Custom error message
    trim: true,
    minlength: [2, "Name must be at least 2 characters"],
    maxlength: [100, "Name cannot exceed 100 characters"]
  },
  price: {
    type: Number,
    required: [true, "Price is required"],
    min: [0, "Price cannot be negative"],
    max: [1000000, "Price cannot exceed 1,000,000"]
  },
  category: {
    type: String,
    required: true,
    enum: {
      values: ["electronics", "clothing", "books", "food"],
      message: "{VALUE} is not a valid category"
    }
  },
  sku: {
    type: String,
    match: [/^[A-Z]{3}-\d{4}$/, "SKU must be in format ABC-1234"]
  },
  email: {
    type: String,
    match: [/^\S+@\S+\.\S+$/, "Please enter a valid email"]
  }
});
```

### Validators Reference

| Validator      | Applies To    | Example                                      |
|----------------|---------------|-----------------------------------------------|
| `required`     | All types     | `required: true` or `required: [true, "msg"]` |
| `min`          | Number, Date  | `min: [0, "Must be positive"]`                |
| `max`          | Number, Date  | `max: [100, "Cannot exceed 100"]`             |
| `minlength`    | String        | `minlength: [2, "Too short"]`                 |
| `maxlength`    | String        | `maxlength: [100, "Too long"]`                |
| `enum`         | String        | `enum: ["a", "b", "c"]`                       |
| `match`        | String        | `match: /^[A-Z]+$/`                           |
| `trim`         | String        | `trim: true`                                  |
| `lowercase`    | String        | `lowercase: true`                             |
| `uppercase`    | String        | `uppercase: true`                             |
| `default`      | All types     | `default: "user"` or `default: Date.now`      |
| `unique`       | All types     | `unique: true` (creates a unique index)       |

### Custom Validators

```javascript
const userSchema = new mongoose.Schema({
  phone: {
    type: String,
    validate: {
      validator: function (value) {
        // Pakistani phone number format
        return /^(\+92|0)?3\d{9}$/.test(value);
      },
      message: "Please enter a valid Pakistani phone number"
    }
  },
  age: {
    type: Number,
    validate: {
      validator: function (value) {
        return value >= 13 && value <= 120;
      },
      message: "Age must be between 13 and 120"
    }
  },
  password: {
    type: String,
    required: true,
    minlength: 8,
    validate: {
      validator: function (value) {
        // Must contain at least one uppercase, one lowercase, one number
        return /^(?=.*[a-z])(?=.*[A-Z])(?=.*\d).+$/.test(value);
      },
      message: "Password must contain uppercase, lowercase, and a number"
    }
  }
});
```

### Handling Validation Errors

```javascript
try {
  const user = await User.create({
    name: "",        // Fails: required
    email: "invalid", // Fails: match
    age: -5          // Fails: min
  });
} catch (error) {
  if (error.name === "ValidationError") {
    // Loop through each field's error
    for (const field in error.errors) {
      console.log(`${field}: ${error.errors[field].message}`);
    }
    // Output:
    // name: Product name is required
    // email: Please enter a valid email
    // age: Age must be between 13 and 120
  }
}
```

---

## 8. Timestamps

Mongoose can automatically manage `createdAt` and `updatedAt` fields for every document.

### Enabling Timestamps

```javascript
const postSchema = new mongoose.Schema(
  {
    title: { type: String, required: true },
    content: { type: String, required: true },
    author: { type: String, required: true }
  },
  {
    timestamps: true  // Adds createdAt and updatedAt automatically
  }
);

const Post = mongoose.model("Post", postSchema);
```

### How Timestamps Work

```javascript
// When you create a document
const post = await Post.create({
  title: "My First Post",
  content: "Hello World!",
  author: "Ali"
});

console.log(post.createdAt);  // 2024-06-15T10:30:00.000Z
console.log(post.updatedAt);  // 2024-06-15T10:30:00.000Z (same as createdAt)

// When you update the document
post.title = "My Updated Post";
await post.save();

console.log(post.createdAt);  // 2024-06-15T10:30:00.000Z (unchanged)
console.log(post.updatedAt);  // 2024-06-15T11:45:00.000Z (auto-updated)
```

### Custom Timestamp Field Names

```javascript
const postSchema = new mongoose.Schema(
  { title: String },
  {
    timestamps: {
      createdAt: "created_at",   // Custom name
      updatedAt: "updated_at"    // Custom name
    }
  }
);
```

---

## 9. Virtuals

**Virtuals** are computed properties that do not get stored in MongoDB. They are calculated on the fly from existing fields.

> Think of virtuals like a calculator display. The numbers you enter (stored fields) are saved, but the result shown on the display (virtual) is computed each time you look at it — it is never stored separately.

### Defining Virtuals

```javascript
const userSchema = new mongoose.Schema({
  firstName: { type: String, required: true },
  lastName: { type: String, required: true },
  birthYear: { type: Number }
});

// Virtual: fullName (computed from firstName + lastName)
userSchema.virtual("fullName").get(function () {
  return `${this.firstName} ${this.lastName}`;
});

// Virtual: age (computed from birthYear)
userSchema.virtual("age").get(function () {
  return new Date().getFullYear() - this.birthYear;
});

// Include virtuals in JSON and Object output
userSchema.set("toJSON", { virtuals: true });
userSchema.set("toObject", { virtuals: true });

const User = mongoose.model("User", userSchema);
```

### Using Virtuals

```javascript
const user = await User.create({
  firstName: "Ali",
  lastName: "Ahmed",
  birthYear: 1999
});

console.log(user.fullName);  // "Ali Ahmed"
console.log(user.age);       // 25 (calculated dynamically)

// fullName and age are NOT stored in MongoDB
// They are computed each time you access them
```

### Virtual Setters

```javascript
userSchema.virtual("fullName")
  .get(function () {
    return `${this.firstName} ${this.lastName}`;
  })
  .set(function (fullName) {
    const parts = fullName.split(" ");
    this.firstName = parts[0];
    this.lastName = parts.slice(1).join(" ");
  });

// Now you can set fullName and it splits into firstName + lastName
const user = new User();
user.fullName = "Sara Khan";
console.log(user.firstName);  // "Sara"
console.log(user.lastName);   // "Khan"
```

---

## 10. Instance Methods

**Instance methods** are custom functions that you can call on individual document instances. They are useful for operations that relate to a single document.

### Defining Instance Methods

```javascript
const userSchema = new mongoose.Schema({
  name: String,
  email: String,
  loginCount: { type: Number, default: 0 },
  lastLogin: Date
});

// Instance method: record a login
userSchema.methods.recordLogin = function () {
  this.loginCount += 1;
  this.lastLogin = new Date();
  return this.save();  // Save the updated document
};

// Instance method: get a summary
userSchema.methods.getSummary = function () {
  return `${this.name} (${this.email}) - Logins: ${this.loginCount}`;
};

// Instance method: check if recently active
userSchema.methods.isRecentlyActive = function (days = 30) {
  if (!this.lastLogin) return false;
  const cutoff = new Date();
  cutoff.setDate(cutoff.getDate() - days);
  return this.lastLogin >= cutoff;
};

const User = mongoose.model("User", userSchema);
```

### Using Instance Methods

```javascript
const user = await User.create({
  name: "Ali Ahmed",
  email: "ali@example.com"
});

// Call the instance method
await user.recordLogin();
console.log(user.loginCount);  // 1
console.log(user.lastLogin);   // Current date/time

// Get summary
console.log(user.getSummary());
// "Ali Ahmed (ali@example.com) - Logins: 1"

// Check activity
console.log(user.isRecentlyActive());  // true
```

> **Important:** Do NOT use arrow functions for instance methods. Arrow functions do not bind `this`, so `this` will not refer to the document.

---

## 11. Static Methods

**Static methods** are custom functions called on the **Model** itself (not on a document instance). They are useful for queries and operations that involve the entire collection.

### Defining Static Methods

```javascript
const userSchema = new mongoose.Schema({
  name: String,
  email: String,
  role: { type: String, enum: ["user", "admin", "moderator"], default: "user" },
  isActive: { type: Boolean, default: true }
});

// Static method: find all admins
userSchema.statics.findAdmins = function () {
  return this.find({ role: "admin" });
};

// Static method: find active users by role
userSchema.statics.findByRole = function (role) {
  return this.find({ role, isActive: true });
};

// Static method: get user statistics
userSchema.statics.getStats = async function () {
  const total = await this.countDocuments();
  const active = await this.countDocuments({ isActive: true });
  const admins = await this.countDocuments({ role: "admin" });
  return { total, active, admins, inactive: total - active };
};

// Static method: search by name (case-insensitive)
userSchema.statics.searchByName = function (name) {
  return this.find({ name: { $regex: name, $options: "i" } });
};

const User = mongoose.model("User", userSchema);
```

### Using Static Methods

```javascript
// Called on the MODEL, not on a document
const admins = await User.findAdmins();

const moderators = await User.findByRole("moderator");

const stats = await User.getStats();
console.log(stats);
// { total: 150, active: 142, admins: 5, inactive: 8 }

const results = await User.searchByName("ali");
// Finds "Ali Ahmed", "Aliya Khan", etc.
```

### Instance vs Static Methods

```
  +-------------------------------+----------------------------------+
  |       Instance Methods        |        Static Methods            |
  +-------------------------------+----------------------------------+
  | Called on a DOCUMENT          | Called on the MODEL              |
  | user.recordLogin()            | User.findAdmins()                |
  |                               |                                  |
  | Has access to `this`          | Has access to `this`             |
  | (the document)                | (the Model/Collection)           |
  |                               |                                  |
  | For single-document ops       | For collection-wide ops          |
  | (save, update, compare)       | (query, aggregate, count)        |
  +-------------------------------+----------------------------------+
```

---

## 12. Summary

| Concept                | Key Takeaway                                                       |
|------------------------|--------------------------------------------------------------------|
| **Mongoose**           | ODM library that adds schemas, validation, and helpers to MongoDB  |
| **Schema**             | Defines the structure, types, and rules for documents              |
| **Model**              | Compiled schema that provides the CRUD interface                   |
| **`mongoose.connect`** | Connects your Node.js app to a MongoDB database                    |
| **`Model.create()`**   | Creates and saves a new document in one step                       |
| **`Model.find()`**     | Retrieves documents matching a filter                              |
| **`findByIdAndUpdate`**| Finds a document by `_id` and updates it                           |
| **`findByIdAndDelete`**| Finds a document by `_id` and removes it                           |
| **Validation**         | Required, min/max, enum, match, custom validators                  |
| **Timestamps**         | Auto-managed `createdAt` and `updatedAt` fields                    |
| **Virtuals**           | Computed properties not stored in the database                     |
| **Instance Methods**   | Custom functions on individual documents                           |
| **Static Methods**     | Custom functions on the Model (collection-wide operations)         |

### What is Next?

In **Week 30**, you will learn **Advanced Queries and Relations** — query operators, sorting, pagination, embedding vs referencing, population, indexing, and the aggregation pipeline.
