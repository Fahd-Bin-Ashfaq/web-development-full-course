# Week 30 — Advanced Queries & Relations

> **Prerequisites:** Week 28-29 (MongoDB basics, Mongoose ODM, Schemas, Models, CRUD)
> **Goal:** Master advanced query operators, sorting, pagination, field selection, relations (embedding vs. referencing), population, indexing, and the aggregation pipeline.

---

## Table of Contents

1. [Query Operators](#1-query-operators)
2. [Sorting](#2-sorting)
3. [Pagination](#3-pagination)
4. [Selecting Fields](#4-selecting-fields)
5. [Counting Documents](#5-counting-documents)
6. [Relations in MongoDB](#6-relations-in-mongodb)
7. [Population](#7-population)
8. [Virtuals for Reverse Population](#8-virtuals-for-reverse-population)
9. [Indexing](#9-indexing)
10. [Aggregation Pipeline](#10-aggregation-pipeline)
11. [Summary](#11-summary)

---

## 1. Query Operators

In Week 28 you used simple filters like `{ role: 'admin' }`. Real applications need more expressive queries: "find products under $50," "find users aged 18 to 30," or "find posts that contain the word 'JavaScript'." MongoDB provides **query operators** for these needs.

> Think of query operators like the **filters on an e-commerce website**. When you shop online, you do not scroll through every product. You set filters: price range, brand, rating, category. Query operators are those filters for your database.

### Comparison Operators

```javascript
// Greater than
const expensive = await Product.find({ price: { $gt: 100 } });

// Less than
const cheap = await Product.find({ price: { $lt: 20 } });

// Greater than or equal
const adults = await User.find({ age: { $gte: 18 } });

// Less than or equal
const discounted = await Product.find({ price: { $lte: 50 } });

// Range: price between 20 and 100 (inclusive)
const midRange = await Product.find({
  price: { $gte: 20, $lte: 100 }
});
```

### Membership Operators

```javascript
// $in: match any value in the array
const techProducts = await Product.find({
  category: { $in: ['electronics', 'computers', 'phones'] }
});

// $nin: match values NOT in the array
const nonFood = await Product.find({
  category: { $nin: ['food', 'beverages'] }
});
```

### Pattern Matching and Existence

```javascript
// $regex: match a pattern (case-insensitive search)
const results = await Product.find({
  name: { $regex: 'phone', $options: 'i' }  // "i" = case-insensitive
});

// $exists: check if a field exists
const withPhone = await User.find({ phone: { $exists: true } });
const noPhone  = await User.find({ phone: { $exists: false } });
```

### Operator Reference Table

| Operator   | Meaning                    | Example                                     |
|------------|----------------------------|----------------------------------------------|
| `$gt`      | Greater than               | `{ price: { $gt: 100 } }`                   |
| `$lt`      | Less than                  | `{ price: { $lt: 20 } }`                    |
| `$gte`     | Greater than or equal      | `{ age: { $gte: 18 } }`                     |
| `$lte`     | Less than or equal         | `{ price: { $lte: 50 } }`                   |
| `$in`      | Matches any in array       | `{ status: { $in: ['active', 'pending'] } }` |
| `$nin`     | Matches none in array      | `{ role: { $nin: ['banned'] } }`             |
| `$regex`   | Regular expression match   | `{ name: { $regex: /^ali/i } }`              |
| `$exists`  | Field exists or not        | `{ phone: { $exists: true } }`               |
| `$ne`      | Not equal                  | `{ status: { $ne: 'deleted' } }`             |
| `$or`      | Logical OR                 | `{ $or: [{ age: 25 }, { role: 'admin' }] }`  |
| `$and`     | Logical AND (implicit)     | `{ age: { $gte: 18, $lte: 65 } }`           |

### Combining Operators

```javascript
// Find active users who are either admins or aged 25+
const users = await User.find({
  isActive: true,
  $or: [
    { role: 'admin' },
    { age: { $gte: 25 } }
  ]
});
```

---

## 2. Sorting

Sorting arranges query results in a specific order. Use `.sort()` chained after `.find()`.

```javascript
// Sort by price ascending (lowest first)
const cheapFirst = await Product.find().sort({ price: 1 });

// Sort by price descending (highest first)
const expensiveFirst = await Product.find().sort({ price: -1 });

// Sort by multiple fields: category A-Z, then price low to high
const organized = await Product.find().sort({ category: 1, price: 1 });

// String shorthand (prefix with - for descending)
const newest = await Product.find().sort('-createdAt');
```

### Sort Direction Reference

| Value | Direction   | Example Use Case                    |
|-------|-------------|--------------------------------------|
| `1`   | Ascending   | Price low-to-high, name A-to-Z      |
| `-1`  | Descending  | Price high-to-low, newest first      |

> **Real-life analogy:** Sorting is like organizing books on a shelf. You can arrange them alphabetically by title (ascending), by publication year newest-first (descending), or first by genre then by author within each genre (multi-field sort).

---

## 3. Pagination

Pagination splits large result sets into manageable **pages**. Without it, fetching 10,000 products at once would be slow and wasteful.

> Think of pagination like pages in a **book catalog**. Instead of printing all 10,000 items on one giant page, the catalog shows 20 items per page. You flip to page 3 to see items 41-60.

### The Formula

```
  skip = (page - 1) * limit

  Example: Page 3, 10 items per page
  skip = (3 - 1) * 10 = 20
  Show items 21 through 30
```

### Implementation

```javascript
const getPaginatedProducts = async (page = 1, limit = 10) => {
  const skip = (page - 1) * limit;

  const products = await Product.find()
    .sort({ createdAt: -1 })  // newest first
    .skip(skip)                // skip previous pages
    .limit(limit);             // take only 'limit' items

  const total = await Product.countDocuments();

  return {
    data: products,
    currentPage: page,
    totalPages: Math.ceil(total / limit),
    totalItems: total
  };
};

// Usage:
// Page 1: skip 0,  show items 1-10
// Page 2: skip 10, show items 11-20
// Page 3: skip 20, show items 21-30
```

### Pagination Flow Diagram

```
  Database: 50 products total
  Limit: 10 per page

  Page 1:  skip(0)  .limit(10)  --> Items  1 - 10
  Page 2:  skip(10) .limit(10)  --> Items 11 - 20
  Page 3:  skip(20) .limit(10)  --> Items 21 - 30
  Page 4:  skip(30) .limit(10)  --> Items 31 - 40
  Page 5:  skip(40) .limit(10)  --> Items 41 - 50

  Response:
  {
    "data": [ ... 10 products ... ],
    "currentPage": 3,
    "totalPages": 5,
    "totalItems": 50
  }
```

---

## 4. Selecting Fields

By default, `.find()` returns all fields. Use `.select()` to return only the fields you need, reducing bandwidth and improving performance.

```javascript
// Include only name and price (+ _id, which is included by default)
const products = await Product.find().select('name price');

// Exclude specific fields (prefix with -)
const users = await User.find().select('-password -__v');

// Object syntax
const items = await Product.find().select({ name: 1, price: 1, _id: 0 });
```

### Select Syntax

| Syntax              | Meaning                        |
|---------------------|--------------------------------|
| `'name price'`      | Include name and price         |
| `'-password -__v'`  | Exclude password and __v       |
| `{ name: 1 }`       | Include name (object syntax)   |
| `{ password: 0 }`   | Exclude password               |

> **Real-life analogy:** Selecting fields is like requesting a **summary report** instead of a full dossier. When you ask HR for a list of employee names and departments, you do not need their home addresses, emergency contacts, and salary history.

---

## 5. Counting Documents

Use `.countDocuments()` to get the number of documents matching a filter without fetching the actual data.

```javascript
// Count all products
const total = await Product.countDocuments();

// Count products in a category
const electronicsCount = await Product.countDocuments({ category: 'electronics' });

// Count active users
const activeUsers = await User.countDocuments({ isActive: true });
```

This is essential for pagination (calculating total pages) and for dashboards that display statistics.

---

## 6. Relations in MongoDB

In relational databases, you use JOINs to connect tables. MongoDB does not have JOINs in the same way. Instead, you have two strategies: **embedding** and **referencing**.

### Strategy 1: Embedding (Denormalization)

Store related data **inside** the parent document.

```javascript
// Embedded: reviews live INSIDE the product document
const productSchema = new mongoose.Schema({
  name: String,
  price: Number,
  reviews: [{
    user: String,
    rating: Number,
    comment: String,
    date: { type: Date, default: Date.now }
  }]
});
```

### Strategy 2: Referencing (Normalization)

Store related data in a **separate collection** and link with ObjectId.

```javascript
// Reference: reviews are in a separate collection
const reviewSchema = new mongoose.Schema({
  product: { type: mongoose.Schema.Types.ObjectId, ref: 'Product' },
  user:    { type: mongoose.Schema.Types.ObjectId, ref: 'User' },
  rating:  Number,
  comment: String
});

const productSchema = new mongoose.Schema({
  name: String,
  price: Number
});
```

### Embedding vs Referencing — Comparison

| Factor                  | Embedding                           | Referencing                          |
|-------------------------|--------------------------------------|--------------------------------------|
| **Data location**       | Inside the parent document           | Separate collection with ObjectId    |
| **Read speed**          | Faster (single query)                | Slower (requires populate/lookup)    |
| **Write speed**         | Slower for large subdocs             | Faster (update only the child doc)   |
| **Data duplication**    | Possible                             | None                                 |
| **Document size limit** | 16 MB per document                   | Not a concern                        |
| **Independent access**  | Cannot query subdocs independently   | Can query children directly          |
| **Best for**            | Small, bounded, read-heavy data      | Large, unbounded, write-heavy data   |

### Decision Diagram

```
  Should I EMBED or REFERENCE?

  Is the related data...
       |
       +-- Small and bounded? (e.g., max 5 addresses per user)
       |        |
       |        YES --> EMBED
       |
       +-- Large or unbounded? (e.g., thousands of comments)
       |        |
       |        YES --> REFERENCE
       |
       +-- Frequently accessed together? (e.g., user + profile)
       |        |
       |        YES --> EMBED
       |
       +-- Accessed independently? (e.g., orders queried alone)
       |        |
       |        YES --> REFERENCE
       |
       +-- Many-to-many? (e.g., students <-> courses)
                |
                YES --> REFERENCE (with arrays of ObjectIds)
```

### Real-Life Examples

| Scenario                              | Strategy    | Reason                                    |
|---------------------------------------|-------------|-------------------------------------------|
| User's shipping addresses (max 5)     | Embed       | Small, bounded, always read with user     |
| Blog post comments (unlimited)        | Reference   | Unbounded, can grow to thousands          |
| Product categories (static list)      | Embed       | Rarely changes, always read with product  |
| E-commerce order items                | Embed       | Always read together, snapshot of purchase |
| Student-Course enrollment             | Reference   | Many-to-many relationship                 |

---

## 7. Population

**Population** is Mongoose's way of replacing ObjectId references with the actual documents from the referenced collection. It is similar to a JOIN in SQL.

### Setting Up References

```javascript
// models/User.js
const userSchema = new mongoose.Schema({
  name:  String,
  email: String
});

// models/Post.js
const postSchema = new mongoose.Schema({
  title:   String,
  content: String,
  author:  { type: mongoose.Schema.Types.ObjectId, ref: 'User' }
});
```

### Using populate()

```javascript
// WITHOUT populate - returns raw ObjectId
const post = await Post.findById(postId);
console.log(post.author); // ObjectId("665abc123...")

// WITH populate - replaces ObjectId with full document
const post = await Post.findById(postId).populate('author');
console.log(post.author); // { _id: "665abc123...", name: "Ali", email: "ali@example.com" }
```

### Selective Population

```javascript
// Populate only specific fields
const post = await Post.findById(postId)
  .populate('author', 'name email');  // Only name and email, no password

// Populate multiple fields
const order = await Order.findById(orderId)
  .populate('user', 'name email')
  .populate('product', 'name price');
```

### Population Flow Diagram

```
  POST DOCUMENT (before populate)
  +-----------------------------------+
  |  _id:     ObjectId("post123")     |
  |  title:   "Learn MongoDB"         |
  |  author:  ObjectId("user456") ----+----+
  +-----------------------------------+    |
                                           |
                    Mongoose sends a       |
                    second query to the    |
                    "users" collection     |
                                           |
  USER DOCUMENT                            |
  +-----------------------------------+    |
  |  _id:   ObjectId("user456") <-----+----+
  |  name:  "Ali Khan"                |
  |  email: "ali@example.com"         |
  +-----------------------------------+

  POST DOCUMENT (after populate)
  +-----------------------------------+
  |  _id:    ObjectId("post123")      |
  |  title:  "Learn MongoDB"          |
  |  author: {                        |
  |    _id:   "user456",              |
  |    name:  "Ali Khan",             |
  |    email: "ali@example.com"       |
  |  }                                |
  +-----------------------------------+
```

---

## 8. Virtuals for Reverse Population

Standard population goes **from child to parent** (a Post references a User). But what if you want to go the other direction — from a User, get all their Posts? Mongoose **virtual populate** handles this without storing an array of Post IDs on the User.

### Setting Up Virtual Populate

```javascript
const userSchema = new mongoose.Schema({
  name: String,
  email: String
}, {
  toJSON:   { virtuals: true },
  toObject: { virtuals: true }
});

// Virtual field: "posts" does not exist in the DB
// It is populated by looking at the Post collection
userSchema.virtual('posts', {
  ref: 'Post',           // The model to populate from
  localField: '_id',     // Field on User
  foreignField: 'author' // Field on Post that references User
});
```

### Using Virtual Populate

```javascript
const user = await User.findById(userId).populate('posts');

console.log(user.posts);
// [
//   { _id: "...", title: "Learn MongoDB", author: userId },
//   { _id: "...", title: "Mongoose Tips", author: userId }
// ]
```

### Virtual Populate Diagram

```
  USER (no "posts" field stored in DB)
  +---------------------------+
  |  _id:  ObjectId("u1")    |
  |  name: "Ali"             |
  |                           |         POSTS COLLECTION
  |  posts: (virtual) -------+------>  +----------------------------+
  |                           |        |  { author: "u1", ... }     |
  +---------------------------+        |  { author: "u1", ... }     |
                                       |  { author: "u2", ... }     |
                                       +----------------------------+
                                       Mongoose filters posts where
                                       author === user._id
```

---

## 9. Indexing

An **index** is a data structure that makes queries faster by allowing MongoDB to find documents without scanning every document in the collection.

> Think of an index like the **index at the back of a textbook**. Without it, finding the word "aggregation" means reading every page. With the index, you look up "aggregation" and immediately jump to page 247.

### Why Indexing Matters

```
  WITHOUT INDEX (Collection Scan)
  Query: { email: "ali@example.com" }

  MongoDB checks EVERY document:
  Doc 1: email = "omar@..."    No
  Doc 2: email = "sara@..."    No
  Doc 3: email = "ali@..."     YES  <-- found after scanning 3
  ...
  Doc 100,000: checked unnecessarily

  Time: O(n) -- grows with collection size


  WITH INDEX on "email"

  MongoDB uses a B-tree index:
  Jump directly to "ali@example.com"

  Time: O(log n) -- stays fast even with millions of docs
```

### Creating Indexes in Mongoose

```javascript
// Method 1: In the schema definition
const userSchema = new mongoose.Schema({
  email: { type: String, unique: true },     // unique creates an index
  name:  { type: String, index: true }       // simple index
});

// Method 2: Using schema.index() for compound indexes
userSchema.index({ lastName: 1, firstName: 1 });  // compound index
userSchema.index({ email: 1 }, { unique: true });  // explicit unique index
```

### Compound Indexes

A compound index covers queries on multiple fields:

```javascript
// Compound index: category + price
productSchema.index({ category: 1, price: -1 });

// This index speeds up these queries:
await Product.find({ category: 'electronics' }).sort({ price: -1 });
await Product.find({ category: 'electronics', price: { $gt: 50 } });
```

### Index Best Practices

| Do                                         | Do Not                                    |
|--------------------------------------------|-------------------------------------------|
| Index fields used in queries and sorts     | Index every field (wastes space and slows writes) |
| Use compound indexes for multi-field queries | Create redundant single-field indexes     |
| Index fields with high cardinality (many unique values) | Index boolean fields with only 2 values |
| Monitor index usage with `explain()`       | Forget indexes exist after creating them  |

---

## 10. Aggregation Pipeline

The **aggregation pipeline** processes documents through a series of stages, where each stage transforms the data. It is MongoDB's most powerful tool for analytics and data transformation.

> Think of an aggregation pipeline like an **assembly line in a factory**. Raw materials (documents) enter the conveyor belt and pass through stations (stages). Each station performs one task — filtering, sorting, grouping, reshaping — and passes the result to the next station.

### Pipeline Concept

```
  DOCUMENTS IN COLLECTION
  +--------------------------------------------------+
  |  { name: "Laptop",  category: "electronics", ... }|
  |  { name: "Phone",   category: "electronics", ... }|
  |  { name: "T-Shirt", category: "clothing", ... }   |
  |  { name: "Jacket",  category: "clothing", ... }   |
  |  { name: "Tablet",  category: "electronics", ... }|
  +--------------------------------------------------+
         |
         v
  Stage 1: $match  { category: "electronics" }
         |
         v
  +--------------------------------------------------+
  |  Laptop, Phone, Tablet  (3 documents remain)     |
  +--------------------------------------------------+
         |
         v
  Stage 2: $group  { _id: "$category", avgPrice: { $avg: "$price" } }
         |
         v
  +--------------------------------------------------+
  |  { _id: "electronics", avgPrice: 699.99 }        |
  +--------------------------------------------------+
         |
         v
  Stage 3: $sort   { avgPrice: -1 }
         |
         v
  FINAL RESULT
```

### Common Pipeline Stages

#### $match — Filter Documents

```javascript
// Like .find() but inside the pipeline
const result = await Order.aggregate([
  { $match: { status: 'completed', total: { $gte: 100 } } }
]);
```

#### $group — Group and Aggregate

```javascript
// Total sales per category
const salesByCategory = await Product.aggregate([
  {
    $group: {
      _id: '$category',                    // group by category
      totalSales:  { $sum: '$sales' },     // sum of sales
      avgPrice:    { $avg: '$price' },     // average price
      productCount: { $sum: 1 }            // count documents
    }
  }
]);

// Result:
// [
//   { _id: "electronics", totalSales: 15000, avgPrice: 499.99, productCount: 25 },
//   { _id: "clothing",    totalSales: 8000,  avgPrice: 49.99,  productCount: 120 }
// ]
```

#### $sort — Sort Results

```javascript
const topCategories = await Product.aggregate([
  { $group: { _id: '$category', totalRevenue: { $sum: '$revenue' } } },
  { $sort: { totalRevenue: -1 } }  // highest revenue first
]);
```

#### $project — Reshape Output

```javascript
const formatted = await User.aggregate([
  {
    $project: {
      fullName: { $concat: ['$firstName', ' ', '$lastName'] },
      email: 1,
      yearJoined: { $year: '$createdAt' },
      _id: 0    // exclude _id
    }
  }
]);

// Result:
// [
//   { fullName: "Ali Khan", email: "ali@example.com", yearJoined: 2024 },
//   { fullName: "Sara Ahmed", email: "sara@example.com", yearJoined: 2025 }
// ]
```

#### $lookup — Join Collections

`$lookup` performs a left outer join with another collection, similar to SQL JOIN.

```javascript
const ordersWithUsers = await Order.aggregate([
  {
    $lookup: {
      from: 'users',           // the other collection
      localField: 'userId',    // field in orders
      foreignField: '_id',     // field in users
      as: 'userDetails'        // output array field
    }
  },
  {
    $unwind: '$userDetails'    // flatten the array to a single object
  },
  {
    $project: {
      orderTotal: '$total',
      userName: '$userDetails.name',
      userEmail: '$userDetails.email'
    }
  }
]);
```

### $group Accumulator Reference

| Accumulator | Purpose              | Example                           |
|-------------|----------------------|-----------------------------------|
| `$sum`      | Sum values           | `{ $sum: '$price' }`             |
| `$avg`      | Average              | `{ $avg: '$rating' }`            |
| `$min`      | Minimum value        | `{ $min: '$price' }`             |
| `$max`      | Maximum value        | `{ $max: '$price' }`             |
| `$first`    | First in group       | `{ $first: '$name' }`            |
| `$last`     | Last in group        | `{ $last: '$name' }`             |
| `$push`     | Collect into array   | `{ $push: '$name' }`             |
| `$addToSet` | Collect unique values | `{ $addToSet: '$category' }`    |

### Practical Example: Monthly Revenue Report

```javascript
const monthlyRevenue = await Order.aggregate([
  // Stage 1: Only completed orders
  { $match: { status: 'completed' } },

  // Stage 2: Group by year and month
  {
    $group: {
      _id: {
        year:  { $year: '$createdAt' },
        month: { $month: '$createdAt' }
      },
      totalRevenue: { $sum: '$total' },
      orderCount:   { $sum: 1 },
      avgOrderValue: { $avg: '$total' }
    }
  },

  // Stage 3: Sort by date
  { $sort: { '_id.year': -1, '_id.month': -1 } },

  // Stage 4: Reshape output
  {
    $project: {
      _id: 0,
      year:  '$_id.year',
      month: '$_id.month',
      totalRevenue: { $round: ['$totalRevenue', 2] },
      orderCount: 1,
      avgOrderValue: { $round: ['$avgOrderValue', 2] }
    }
  }
]);

// Result:
// [
//   { year: 2025, month: 6, totalRevenue: 45230.50, orderCount: 312, avgOrderValue: 145.00 },
//   { year: 2025, month: 5, totalRevenue: 38750.00, orderCount: 289, avgOrderValue: 134.08 }
// ]
```

---

## 11. Summary

```
  ADVANCED QUERIES & RELATIONS
  +----------------------------------------------------------+
  |                                                            |
  |  QUERY OPERATORS ----> $gt, $lt, $in, $regex, $exists     |
  |       |                                                    |
  |       v                                                    |
  |  SORTING -----------> .sort({ field: 1 or -1 })           |
  |       |                                                    |
  |       v                                                    |
  |  PAGINATION --------> .skip((page-1)*limit).limit(limit)  |
  |       |                                                    |
  |       v                                                    |
  |  SELECT FIELDS -----> .select('name price -password')     |
  |       |                                                    |
  |       v                                                    |
  |  RELATIONS ----------> Embed (inside doc) vs              |
  |       |                Reference (ObjectId + populate)     |
  |       |                                                    |
  |       v                                                    |
  |  INDEXING -----------> Speed up reads with B-tree indexes |
  |       |                                                    |
  |       v                                                    |
  |  AGGREGATION --------> Pipeline stages for analytics      |
  |                        $match, $group, $sort, $project,   |
  |                        $lookup                             |
  +----------------------------------------------------------+
```

| Topic              | Key Takeaway                                                 |
|--------------------|--------------------------------------------------------------|
| Query operators    | Filter with $gt, $lt, $in, $regex, $exists, and more        |
| Sorting            | `.sort({ field: 1 })` for ascending, `-1` for descending    |
| Pagination         | `skip((page-1)*limit).limit(limit)` with total count        |
| Field selection    | `.select('field1 field2')` to reduce response size           |
| Embedding          | Store related data inside the document (fast reads)          |
| Referencing        | Store ObjectId + use `.populate()` (normalized data)         |
| Virtual populate   | Reverse population without storing IDs on the parent         |
| Indexing           | Dramatically speeds up queries on indexed fields             |
| Aggregation        | Multi-stage pipeline for grouping, joining, and analytics    |

> **Next Week:** We will integrate MongoDB with Express.js to build a complete CRUD API with the MVC pattern, error handling, and data seeding.
