# Week 28 — Introduction to MongoDB

> **Prerequisites:** Week 24-27 (Node.js, npm, Express.js, Middleware & Authentication basics)
> **Goal:** Understand what databases are, learn the difference between SQL and NoSQL, and perform CRUD operations in MongoDB Shell.

---

## Table of Contents

1. [What is a Database?](#1-what-is-a-database)
2. [SQL vs NoSQL](#2-sql-vs-nosql)
3. [What is MongoDB?](#3-what-is-mongodb)
4. [Installing MongoDB and MongoDB Compass](#4-installing-mongodb-and-mongodb-compass)
5. [MongoDB Atlas — Cloud Setup](#5-mongodb-atlas--cloud-setup)
6. [MongoDB Shell Basics](#6-mongodb-shell-basics)
7. [CRUD Operations in MongoDB Shell](#7-crud-operations-in-mongodb-shell)
8. [Collections and Documents Explained](#8-collections-and-documents-explained)
9. [Data Types in MongoDB](#9-data-types-in-mongodb)
10. [Summary](#10-summary)

---

## 1. What is a Database?

A **database** is an organized collection of data that can be easily accessed, managed, and updated. Every application that stores information — user accounts, blog posts, product listings, order histories — relies on a database.

> Think of a database like a **filing cabinet** in a large office. Without the cabinet, important papers would be scattered across desks, drawers, and folders with no logical order. The filing cabinet provides **labeled drawers** (tables or collections), **organized folders** (rows or documents), and a **system** that lets any employee quickly find, add, update, or remove a specific file.

### Real-Life Analogy: The Filing Cabinet

```
  FILING CABINET (Database)
  +--------------------------------------------------+
  |                                                    |
  |   DRAWER: "Customers"  (Collection / Table)       |
  |   +----------------------------------------------+|
  |   |  Folder: { name: "Ali", age: 25, ... }       ||
  |   |  Folder: { name: "Sara", age: 30, ... }      ||
  |   |  Folder: { name: "Omar", age: 22, ... }      ||
  |   +----------------------------------------------+|
  |                                                    |
  |   DRAWER: "Orders"  (Collection / Table)           |
  |   +----------------------------------------------+|
  |   |  Folder: { orderId: 1, item: "Laptop" }      ||
  |   |  Folder: { orderId: 2, item: "Phone" }       ||
  |   +----------------------------------------------+|
  |                                                    |
  |   DRAWER: "Products"  (Collection / Table)         |
  |   +----------------------------------------------+|
  |   |  Folder: { name: "Laptop", price: 999 }      ||
  |   |  Folder: { name: "Phone", price: 699 }       ||
  |   +----------------------------------------------+|
  |                                                    |
  +--------------------------------------------------+
```

### Why Not Just Use Files?

You could store data in JSON or text files, but files fall apart at scale:

| Problem                   | File-Based Storage             | Database                          |
|---------------------------|--------------------------------|-----------------------------------|
| **Speed**                 | Reads entire file every time   | Uses indexes to find data fast    |
| **Concurrent access**     | Corrupts if two users write    | Handles thousands simultaneously  |
| **Querying**              | Manual parsing needed          | Built-in query language           |
| **Data integrity**        | No validation rules            | Enforces structure and rules      |
| **Scalability**           | Breaks with large data         | Designed for millions of records  |

---

## 2. SQL vs NoSQL

Databases fall into two major categories: **SQL** (Structured Query Language) and **NoSQL** (Not Only SQL). Understanding the difference is critical before choosing one.

### Comparison Table

| Feature              | SQL (Relational)                    | NoSQL (Non-Relational)               |
|----------------------|-------------------------------------|--------------------------------------|
| **Structure**        | Tables with rows and columns        | Documents, key-value, graph, etc.    |
| **Schema**           | Fixed schema (must define upfront)  | Flexible schema (can vary per doc)   |
| **Language**         | SQL (SELECT, INSERT, UPDATE...)     | Varies (MongoDB uses JavaScript)     |
| **Relationships**    | JOINs between tables                | Embedding or referencing documents   |
| **Scaling**          | Vertical (bigger server)            | Horizontal (more servers)            |
| **Examples**         | MySQL, PostgreSQL, SQLite           | MongoDB, Redis, CouchDB             |
| **Best for**         | Structured, relational data         | Flexible, rapidly changing data      |

### Visual Comparison

```
  SQL DATABASE (e.g., MySQL)             NoSQL DATABASE (e.g., MongoDB)
  +-----------------------+              +---------------------------+
  | TABLE: users          |              | COLLECTION: users         |
  +-----------------------+              +---------------------------+
  | id | name   | age     |              | {                         |
  |----|--------|---------|              |   _id: ObjectId("..."),   |
  |  1 | Ali    |  25     |              |   name: "Ali",            |
  |  2 | Sara   |  30     |              |   age: 25,                |
  |  3 | Omar   |  22     |              |   hobbies: ["reading"]    |
  +-----------------------+              | }                         |
                                         | {                         |
  Every row MUST have the               |   _id: ObjectId("..."),   |
  same columns. Adding a                |   name: "Sara",           |
  "hobbies" column affects              |   age: 30                 |
  ALL rows.                              | }                         |
                                         +---------------------------+
                                         Each document can have
                                         DIFFERENT fields. Sara has
                                         no "hobbies" — that is fine.
```

### When to Use Which?

| Use Case                          | Best Choice |
|-----------------------------------|-------------|
| Banking system with transactions  | SQL         |
| E-commerce product catalog        | NoSQL       |
| Social media with varied content  | NoSQL       |
| Accounting / ERP systems          | SQL         |
| Real-time analytics               | NoSQL       |
| Content management systems        | Either      |

---

## 3. What is MongoDB?

**MongoDB** is the most popular NoSQL database. It stores data as **documents** in a format called **BSON** (Binary JSON), which looks and feels like regular JavaScript objects.

> Think of MongoDB like a **notebook** where each page is an independent document. Unlike a spreadsheet where every row must have the same columns, each page in your notebook can have whatever information is relevant — some pages have sketches, some have lists, some have paragraphs. MongoDB gives you this same flexibility with data.

### Key Facts

| Fact                   | Detail                                                    |
|------------------------|-----------------------------------------------------------|
| **Created**            | 2007 by 10gen (now MongoDB, Inc.)                         |
| **Name origin**        | From "hu**mongo**us" — designed for huge data             |
| **Data format**        | BSON (Binary JSON)                                        |
| **Query language**     | JavaScript-like syntax                                    |
| **Default port**       | 27017                                                     |
| **License**            | Server Side Public License (SSPL)                         |

### MongoDB Architecture

```
  +--------------------------------------------------+
  |              MongoDB SERVER                       |
  |                                                    |
  |   DATABASE: "myApp"                                |
  |   +----------------------------------------------+|
  |   |                                              ||
  |   |  COLLECTION: "users"                         ||
  |   |  +------------------------------------------+||
  |   |  | DOCUMENT: { name: "Ali", age: 25 }       |||
  |   |  | DOCUMENT: { name: "Sara", age: 30 }      |||
  |   |  +------------------------------------------+||
  |   |                                              ||
  |   |  COLLECTION: "products"                      ||
  |   |  +------------------------------------------+||
  |   |  | DOCUMENT: { name: "Laptop", price: 999 } |||
  |   |  | DOCUMENT: { name: "Phone", price: 699 }  |||
  |   |  +------------------------------------------+||
  |   |                                              ||
  |   +----------------------------------------------+|
  |                                                    |
  +--------------------------------------------------+
```

### SQL to MongoDB Terminology Mapping

| SQL Term       | MongoDB Term    |
|----------------|-----------------|
| Database       | Database        |
| Table          | Collection      |
| Row            | Document        |
| Column         | Field           |
| Primary Key    | `_id`           |
| JOIN           | `$lookup` / embedding |

---

## 4. Installing MongoDB and MongoDB Compass

### Step 1: Install MongoDB Community Edition

**On Windows:**

1. Go to [mongodb.com/try/download/community](https://www.mongodb.com/try/download/community)
2. Select your OS version (Windows x64)
3. Download the MSI installer
4. Run the installer — choose **Complete** setup
5. Check the box for **Install MongoDB as a Service**
6. Check the box for **Install MongoDB Compass** (GUI tool)

**On macOS (using Homebrew):**

```bash
# Tap the MongoDB formula
brew tap mongodb/brew

# Install MongoDB Community Edition
brew install mongodb-community

# Start MongoDB as a background service
brew services start mongodb-community
```

**On Ubuntu/Linux:**

```bash
# Import the public key
curl -fsSL https://www.mongodb.org/static/pgp/server-7.0.asc | sudo gpg --dearmor -o /usr/share/keyrings/mongodb-server-7.0.gpg

# Add the repository
echo "deb [ signed-by=/usr/share/keyrings/mongodb-server-7.0.gpg ] https://repo.mongodb.org/apt/ubuntu jammy/mongodb-org/7.0 multiverse" | sudo tee /etc/apt/sources.list.d/mongodb-org-7.0.list

# Install
sudo apt-get update
sudo apt-get install -y mongodb-org

# Start the service
sudo systemctl start mongod
```

### Step 2: Verify Installation

```bash
# Check MongoDB version
mongod --version

# Start the MongoDB Shell
mongosh
```

### Step 3: MongoDB Compass

**MongoDB Compass** is the official GUI for MongoDB. It lets you visually explore databases, run queries, and manage collections without writing shell commands.

```
  +-------------------------------------------------------+
  |  MongoDB Compass                                       |
  +-------------------------------------------------------+
  |  Connection: mongodb://localhost:27017                  |
  +-------------------------------------------------------+
  |  Databases    |  Collections  |  Documents             |
  |  ------------ |  ------------ |  ---------------------- |
  |  > myApp      |  > users      |  { name: "Ali" }       |
  |  > admin      |  > products   |  { name: "Sara" }      |
  |  > local      |               |  { name: "Omar" }      |
  +-------------------------------------------------------+
```

To connect with Compass:

1. Open MongoDB Compass
2. Enter the connection string: `mongodb://localhost:27017`
3. Click **Connect**
4. You will see your databases listed on the left panel

---

## 5. MongoDB Atlas — Cloud Setup

**MongoDB Atlas** is the fully managed cloud version of MongoDB. It eliminates the need to install, configure, or maintain a database server on your machine.

### Why Atlas?

| Feature                | Local MongoDB              | MongoDB Atlas                     |
|------------------------|----------------------------|-----------------------------------|
| **Setup**              | Manual installation        | Click a few buttons               |
| **Maintenance**        | You manage updates/backups | Automated by Atlas                |
| **Scaling**            | Limited to your machine    | Auto-scales in the cloud          |
| **Availability**       | Single machine             | Multi-region replication          |
| **Cost**               | Free (local)               | Free tier available (512MB)       |

### Setting Up Atlas (Step by Step)

1. Go to [mongodb.com/atlas](https://www.mongodb.com/atlas) and sign up
2. Create a new **Organization** and **Project**
3. Click **Build a Database**
4. Choose **M0 Free Tier** (Shared Cluster)
5. Select a cloud provider (AWS, Google Cloud, or Azure) and region
6. Click **Create Cluster**

### Configure Access

**Create a Database User:**

1. Go to **Database Access** in the left sidebar
2. Click **Add New Database User**
3. Set a username and strong password
4. Set privileges to **Read and Write to any database**

**Whitelist Your IP:**

1. Go to **Network Access** in the left sidebar
2. Click **Add IP Address**
3. Choose **Allow Access from Anywhere** (for development only) or add your specific IP

### Get Your Connection String

1. Go to your cluster and click **Connect**
2. Choose **Connect your application**
3. Copy the connection string:

```
mongodb+srv://yourUsername:yourPassword@cluster0.xxxxx.mongodb.net/yourDatabaseName?retryWrites=true&w=majority
```

4. Replace `yourUsername`, `yourPassword`, and `yourDatabaseName` with your actual values

### Connect via Compass

Use the same connection string in MongoDB Compass to browse your Atlas data visually.

---

## 6. MongoDB Shell Basics

The **MongoDB Shell** (`mongosh`) is a JavaScript-based interactive environment for working with MongoDB.

### Starting the Shell

```bash
# Connect to local MongoDB
mongosh

# Connect to a specific host
mongosh "mongodb://localhost:27017"

# Connect to Atlas
mongosh "mongodb+srv://user:password@cluster0.xxxxx.mongodb.net/myApp"
```

### Essential Shell Commands

```javascript
// Show all databases
show dbs

// Switch to a database (creates it if it does not exist)
use myApp

// Show current database
db

// Show all collections in the current database
show collections

// Drop (delete) the current database
db.dropDatabase()

// Create a collection explicitly
db.createCollection("users")

// Drop a specific collection
db.users.drop()
```

### The Shell Workflow

```
  +------------------+     +-----------------+     +------------------+
  |   mongosh        | --> |  MongoDB Server  | --> |  Database: myApp |
  |   (your terminal)|     |  (port 27017)    |     |                  |
  +------------------+     +-----------------+     +------------------+
                                                           |
                                          +----------------+----------------+
                                          |                                 |
                                   Collection: users              Collection: products
                                   +----------------+             +------------------+
                                   | Document 1     |             | Document 1       |
                                   | Document 2     |             | Document 2       |
                                   +----------------+             +------------------+
```

---

## 7. CRUD Operations in MongoDB Shell

**CRUD** stands for **Create, Read, Update, Delete** — the four fundamental operations for any database.

### 7.1 CREATE — Inserting Documents

**Insert a single document:**

```javascript
db.users.insertOne({
  name: "Ali Ahmed",
  email: "ali@example.com",
  age: 25,
  city: "Karachi",
  hobbies: ["reading", "coding"]
});
```

Output:

```javascript
{
  acknowledged: true,
  insertedId: ObjectId("6578a1b2c3d4e5f6a7b8c9d0")
}
```

**Insert multiple documents:**

```javascript
db.users.insertMany([
  {
    name: "Sara Khan",
    email: "sara@example.com",
    age: 30,
    city: "Lahore",
    hobbies: ["painting", "cooking"]
  },
  {
    name: "Omar Farooq",
    email: "omar@example.com",
    age: 22,
    city: "Islamabad",
    hobbies: ["gaming", "football"]
  },
  {
    name: "Fatima Noor",
    email: "fatima@example.com",
    age: 28,
    city: "Karachi",
    hobbies: ["reading", "traveling"]
  }
]);
```

Output:

```javascript
{
  acknowledged: true,
  insertedIds: {
    '0': ObjectId("..."),
    '1': ObjectId("..."),
    '2': ObjectId("...")
  }
}
```

### 7.2 READ — Finding Documents

**Find all documents:**

```javascript
db.users.find();
```

**Find with formatting:**

```javascript
db.users.find().pretty();
```

**Find with a filter:**

```javascript
// Find users in Karachi
db.users.find({ city: "Karachi" });

// Find users older than 25
db.users.find({ age: { $gt: 25 } });

// Find a specific user by name
db.users.find({ name: "Ali Ahmed" });
```

**Find one document:**

```javascript
db.users.findOne({ email: "ali@example.com" });
```

**Projection — selecting specific fields:**

```javascript
// Only return name and email (exclude _id)
db.users.find({}, { name: 1, email: 1, _id: 0 });
```

### 7.3 UPDATE — Modifying Documents

**Update one document:**

```javascript
db.users.updateOne(
  { name: "Ali Ahmed" },           // filter: which document
  { $set: { age: 26, city: "Dubai" } }  // update: what to change
);
```

Output:

```javascript
{
  acknowledged: true,
  matchedCount: 1,
  modifiedCount: 1
}
```

**Common update operators:**

| Operator       | Purpose                          | Example                               |
|----------------|----------------------------------|---------------------------------------|
| `$set`         | Set a field's value              | `{ $set: { age: 26 } }`              |
| `$unset`       | Remove a field                   | `{ $unset: { city: "" } }`           |
| `$inc`         | Increment a number               | `{ $inc: { age: 1 } }`               |
| `$push`        | Add to an array                  | `{ $push: { hobbies: "swimming" } }` |
| `$pull`        | Remove from an array             | `{ $pull: { hobbies: "gaming" } }`   |
| `$rename`      | Rename a field                   | `{ $rename: { city: "location" } }`  |

**Update many documents:**

```javascript
// Give everyone in Karachi a "verified" field
db.users.updateMany(
  { city: "Karachi" },
  { $set: { verified: true } }
);
```

**Replace a document entirely:**

```javascript
db.users.replaceOne(
  { name: "Omar Farooq" },
  {
    name: "Omar Farooq",
    email: "omar.new@example.com",
    age: 23,
    city: "Rawalpindi"
  }
);
```

### 7.4 DELETE — Removing Documents

**Delete one document:**

```javascript
db.users.deleteOne({ name: "Omar Farooq" });
```

Output:

```javascript
{
  acknowledged: true,
  deletedCount: 1
}
```

**Delete many documents:**

```javascript
// Delete all users under age 25
db.users.deleteMany({ age: { $lt: 25 } });
```

**Delete ALL documents in a collection (be careful):**

```javascript
db.users.deleteMany({});
```

### CRUD Summary Diagram

```
  +------------------+     +------------------+     +------------------+
  |     CREATE       |     |      READ        |     |     UPDATE       |
  |                  |     |                  |     |                  |
  | insertOne()      |     | find()           |     | updateOne()      |
  | insertMany()     |     | findOne()        |     | updateMany()     |
  |                  |     | find().pretty()  |     | replaceOne()     |
  +------------------+     +------------------+     +------------------+
                                                    +------------------+
                                                    |     DELETE       |
                                                    |                  |
                                                    | deleteOne()      |
                                                    | deleteMany()     |
                                                    +------------------+
```

---

## 8. Collections and Documents Explained

### What is a Collection?

A **collection** is a group of related documents — equivalent to a "table" in SQL databases. Collections are created automatically when you insert the first document.

```javascript
// This creates the "products" collection automatically
db.products.insertOne({ name: "Laptop", price: 999 });
```

### What is a Document?

A **document** is a single record in a collection — equivalent to a "row" in SQL. Documents are stored as BSON (Binary JSON) and can contain nested objects and arrays.

```javascript
// A rich document with various data types
{
  _id: ObjectId("6578a1b2c3d4e5f6a7b8c9d0"),
  name: "Ali Ahmed",
  age: 25,
  email: "ali@example.com",
  address: {                        // Nested object (embedded document)
    street: "123 Main Street",
    city: "Karachi",
    country: "Pakistan"
  },
  hobbies: ["reading", "coding"],   // Array of strings
  scores: [95, 88, 76],             // Array of numbers
  isActive: true,                   // Boolean
  createdAt: ISODate("2024-01-15")  // Date
}
```

### The `_id` Field

Every document in MongoDB **must** have an `_id` field. If you do not provide one, MongoDB automatically generates an **ObjectId**.

```javascript
// MongoDB generates _id automatically
db.users.insertOne({ name: "Ali" });
// Result: { _id: ObjectId("6578a1b2c3d4e5f6a7b8c9d0"), name: "Ali" }

// You can provide your own _id
db.users.insertOne({ _id: "user_001", name: "Sara" });
// Result: { _id: "user_001", name: "Sara" }
```

### ObjectId Anatomy

```
  ObjectId("6578a1b2c3d4e5f6a7b8c9d0")
            |--------|----|----|--------|
            Timestamp Rand  Inc  Counter
            (4 bytes) (5 bytes) (3 bytes)

  - Timestamp: When the document was created
  - Random:    Unique to the machine/process
  - Counter:   Incrementing counter for uniqueness
  - Total:     12 bytes = 24 hex characters
```

---

## 9. Data Types in MongoDB

MongoDB supports a rich set of data types through BSON.

| Data Type       | Example                                      | Description                          |
|-----------------|----------------------------------------------|--------------------------------------|
| **String**      | `"Hello World"`                              | UTF-8 text                           |
| **Number (int)**| `42`                                         | 32-bit integer                       |
| **Number (long)**| `NumberLong("9999999999")`                  | 64-bit integer                       |
| **Double**      | `3.14`                                       | 64-bit floating point                |
| **Boolean**     | `true` / `false`                             | True or false                        |
| **Array**       | `["a", "b", "c"]`                            | Ordered list of values               |
| **Object**      | `{ key: "value" }`                           | Embedded document                    |
| **ObjectId**    | `ObjectId("6578...")`                        | Unique 12-byte identifier            |
| **Date**        | `ISODate("2024-01-15")`                      | Date and time                        |
| **Null**        | `null`                                       | Null or missing value                |
| **Decimal128**  | `NumberDecimal("19.99")`                     | High-precision decimal               |
| **Timestamp**   | `Timestamp()`                                | Internal MongoDB timestamp           |
| **Binary**      | `BinData(0, "...")`                          | Binary data (images, files)          |
| **RegExp**      | `/pattern/flags`                             | Regular expression                   |

### Practical Example: A Complete Document

```javascript
db.products.insertOne({
  name: "MacBook Pro 14",                       // String
  price: NumberDecimal("2499.99"),               // Decimal128
  stock: 150,                                   // Number (int)
  isAvailable: true,                             // Boolean
  categories: ["electronics", "laptops"],        // Array
  specifications: {                              // Embedded Object
    processor: "M3 Pro",
    ram: "18GB",
    storage: "512GB SSD"
  },
  ratings: [4.5, 4.8, 4.2, 4.9],               // Array of numbers
  releaseDate: ISODate("2024-01-15"),            // Date
  manufacturer: null,                            // Null
  createdAt: new Date()                          // Current date/time
});
```

---

## 10. Summary

| Concept                    | Key Takeaway                                                      |
|----------------------------|-------------------------------------------------------------------|
| **Database**               | Organized collection of data; like a filing cabinet               |
| **SQL vs NoSQL**           | SQL = structured tables; NoSQL = flexible documents               |
| **MongoDB**                | Document-based NoSQL database using BSON format                   |
| **MongoDB Compass**        | Official GUI tool for visually managing MongoDB                   |
| **MongoDB Atlas**          | Cloud-hosted MongoDB with free tier                               |
| **MongoDB Shell**          | JavaScript-based CLI for interacting with MongoDB                 |
| **CRUD**                   | Create (insert), Read (find), Update (update), Delete (delete)    |
| **Collection**             | A group of documents (like a table in SQL)                        |
| **Document**               | A single record stored as BSON (like a row in SQL)                |
| **`_id`**                  | Unique identifier auto-generated as ObjectId                      |
| **BSON Data Types**        | String, Number, Boolean, Array, Object, Date, ObjectId, and more  |

### What is Next?

In **Week 29**, you will learn **Mongoose** — an ODM (Object Data Modeling) library that provides a structured way to interact with MongoDB from your Node.js/Express applications. Mongoose adds schemas, validation, and powerful query helpers on top of raw MongoDB.
