# Week 30 — Advanced Queries & Relations: Practice Questions

**Total Questions: 20** (10 MCQs + 5 Short Answer + 5 Coding Exercises)

---

## Part 1: Multiple Choice Questions (MCQs)

**1. Which query operator would you use to find all products with a price greater than 50?**

- A) `{ price: { $gt: 50 } }`
- B) `{ price: { $gte: 50 } }`
- C) `{ price: { $more: 50 } }`
- D) `{ price: { $above: 50 } }`

<details>
<summary>Answer</summary>

**A) `{ price: { $gt: 50 } }`**

`$gt` stands for "greater than." It matches documents where the field value is strictly greater than the specified value (not including 50 itself). To include 50, you would use `$gte` (greater than or equal).
</details>

---

**2. What does `.sort({ price: -1 })` do?**

- A) Sorts by price in ascending order (lowest first)
- B) Sorts by price in descending order (highest first)
- C) Removes the price field
- D) Filters out negative prices

<details>
<summary>Answer</summary>

**B) Sorts by price in descending order (highest first)**

In MongoDB and Mongoose, `1` means ascending (A-Z, low-to-high) and `-1` means descending (Z-A, high-to-low). So `{ price: -1 }` returns the most expensive items first.
</details>

---

**3. Given 100 documents, page 4, and a limit of 10, what is the correct `skip` value?**

- A) 40
- B) 30
- C) 10
- D) 4

<details>
<summary>Answer</summary>

**B) 30**

The pagination formula is `skip = (page - 1) * limit`. For page 4 with 10 items per page: `(4 - 1) * 10 = 30`. This skips the first 30 documents (pages 1-3) and returns documents 31-40.
</details>

---

**4. What does `.select('-password -__v')` do?**

- A) Selects only the password and __v fields
- B) Excludes the password and __v fields from the result
- C) Deletes the password and __v fields from the database
- D) Sorts by password in descending order

<details>
<summary>Answer</summary>

**B) Excludes the password and __v fields from the result**

The `-` prefix before a field name in `.select()` means "exclude this field." This is commonly used to prevent sensitive data (like passwords) or internal fields (like `__v`) from being sent in API responses. All other fields are included.
</details>

---

**5. When should you use EMBEDDING over REFERENCING in MongoDB?**

- A) When the related data is large and unbounded
- B) When the related data is small, bounded, and always read together
- C) When the data needs to be queried independently
- D) When dealing with many-to-many relationships

<details>
<summary>Answer</summary>

**B) When the related data is small, bounded, and always read together**

Embedding is ideal when:
- The data is small (e.g., a user's 3-5 shipping addresses)
- It has a natural upper bound (will not grow to thousands)
- It is almost always accessed together with the parent document

This avoids the extra query that referencing + population requires.
</details>

---

**6. What does `.populate('author')` do in Mongoose?**

- A) Creates a new author document
- B) Replaces the ObjectId in the `author` field with the actual referenced document
- C) Deletes the author field
- D) Adds an author field to every document

<details>
<summary>Answer</summary>

**B) Replaces the ObjectId in the `author` field with the actual referenced document**

When a schema field is defined with `ref: 'User'` and stores an ObjectId, calling `.populate('author')` tells Mongoose to fetch the corresponding User document and replace the ObjectId with the full object. This is similar to a JOIN in SQL databases.
</details>

---

**7. What is the purpose of indexing in MongoDB?**

- A) To encrypt data at rest
- B) To compress the collection size
- C) To speed up queries by avoiding full collection scans
- D) To create backups of the data

<details>
<summary>Answer</summary>

**C) To speed up queries by avoiding full collection scans**

Without an index, MongoDB must scan every document in a collection to find matches (O(n) time). An index is a B-tree data structure that allows MongoDB to locate documents in O(log n) time, dramatically speeding up queries on indexed fields — especially in large collections.
</details>

---

**8. In the aggregation pipeline, which stage is equivalent to `.find()` with a filter?**

- A) `$group`
- B) `$project`
- C) `$match`
- D) `$sort`

<details>
<summary>Answer</summary>

**C) `$match`**

`$match` filters documents in the aggregation pipeline, just as a filter object in `.find()` does. It is usually placed early in the pipeline to reduce the number of documents processed by subsequent stages, improving performance.
</details>

---

**9. What does `$group` do in the aggregation pipeline?**

- A) Sorts documents into groups by date
- B) Groups documents by a specified field and applies accumulator operations (sum, avg, count, etc.)
- C) Groups all documents into one result
- D) Creates subgroups of collections

<details>
<summary>Answer</summary>

**B) Groups documents by a specified field and applies accumulator operations (sum, avg, count, etc.)**

`$group` takes an `_id` field that specifies the grouping key and one or more accumulator expressions. For example, `{ $group: { _id: '$category', total: { $sum: '$price' } } }` groups documents by category and sums their prices within each group.
</details>

---

**10. Which aggregation stage performs a JOIN-like operation between two collections?**

- A) `$merge`
- B) `$lookup`
- C) `$unwind`
- D) `$join`

<details>
<summary>Answer</summary>

**B) `$lookup`**

`$lookup` performs a left outer join with another collection. It takes four parameters: `from` (the other collection), `localField` (field in the current collection), `foreignField` (field in the other collection), and `as` (the output array name). It is the aggregation equivalent of SQL JOIN.
</details>

---

## Part 2: Short Answer Questions

**11. Explain the pagination formula `skip = (page - 1) * limit` with a concrete example.**

<details>
<summary>Answer</summary>

The formula calculates how many documents to skip to reach the desired page.

**Example:** You have 50 products and want to show 10 per page. A user requests page 3.

```
skip = (page - 1) * limit
skip = (3 - 1) * 10
skip = 20
```

This means: skip the first 20 documents (which belong to pages 1 and 2), then return the next 10 documents (items 21-30), which is page 3.

| Page | Skip | Documents Returned |
|------|------|--------------------|
| 1    | 0    | Items 1-10         |
| 2    | 10   | Items 11-20        |
| 3    | 20   | Items 21-30        |
| 4    | 30   | Items 31-40        |
| 5    | 40   | Items 41-50        |

Total pages = `Math.ceil(totalItems / limit)` = `Math.ceil(50 / 10)` = 5.
</details>

---

**12. Compare embedding and referencing in MongoDB. Give one scenario where each is the better choice.**

<details>
<summary>Answer</summary>

**Embedding** stores related data inside the parent document. **Referencing** stores related data in a separate collection and links them with ObjectIds.

| Aspect              | Embedding                          | Referencing                        |
|---------------------|------------------------------------|------------------------------------|
| Data location       | Inside the parent document         | Separate collection                |
| Read performance    | Fast (one query)                   | Slower (needs populate / $lookup)  |
| Data independence   | Cannot query subdocs alone         | Can query children independently   |
| Growth              | Limited by 16 MB document size     | No practical limit                 |

**Embedding scenario:** A user profile with an array of shipping addresses (maximum 5). The addresses are small, bounded, and always needed when displaying the user profile.

**Referencing scenario:** A blog platform where each post can have thousands of comments. Embedding thousands of comments inside a post document would approach the 16 MB limit and make updates expensive. Storing comments in a separate collection with a `postId` reference is more scalable.
</details>

---

**13. What is the purpose of `$unwind` in an aggregation pipeline, and when would you use it?**

<details>
<summary>Answer</summary>

`$unwind` deconstructs an array field, creating one output document for each element in the array.

**Example:** If a document has `tags: ["javascript", "mongodb", "node"]`, `$unwind` produces three separate documents, each with a single tag value.

```javascript
// Before $unwind:
{ _id: 1, name: "Post A", tags: ["javascript", "mongodb"] }

// After { $unwind: '$tags' }:
{ _id: 1, name: "Post A", tags: "javascript" }
{ _id: 1, name: "Post A", tags: "mongodb" }
```

**When to use it:**
- After `$lookup` to flatten the resulting array into individual documents.
- Before `$group` when you need to group by array elements (e.g., count posts per tag).
- When you need to perform calculations on individual array elements.
</details>

---

**14. Explain why you should NOT index every field in a collection.**

<details>
<summary>Answer</summary>

While indexes speed up read queries, they come with costs:

1. **Storage overhead:** Each index is a separate data structure (B-tree) stored on disk. More indexes means more disk space consumed.

2. **Slower writes:** Every time you insert, update, or delete a document, MongoDB must also update all relevant indexes. More indexes means every write operation takes longer.

3. **Memory usage:** MongoDB tries to keep indexes in RAM for fast access. Too many indexes can exhaust available memory, forcing some indexes to be read from disk and negating their performance benefit.

4. **Diminishing returns:** An index on a field with low cardinality (e.g., a boolean `isActive` with only two possible values) provides minimal query speedup because the index still points to roughly half the collection.

**Best practice:** Only index fields that are frequently used in query filters, sort operations, or join conditions. Monitor index usage with `db.collection.aggregate([{ $indexStats: {} }])` and remove unused indexes.
</details>

---

**15. Describe what the aggregation pipeline does and name three common stages with their purposes.**

<details>
<summary>Answer</summary>

The **aggregation pipeline** processes documents through a series of sequential stages, where each stage transforms the data and passes its output to the next stage. It is MongoDB's framework for data analysis, reporting, and transformation.

**Three common stages:**

1. **`$match`** — Filters documents by a condition. Equivalent to `.find()` with a filter. Place it early in the pipeline to reduce the volume of data processed by later stages.
   ```javascript
   { $match: { status: 'completed' } }
   ```

2. **`$group`** — Groups documents by a field and applies accumulator operations like `$sum`, `$avg`, `$min`, `$max`, and `$count`. Used for aggregations like "total sales per category" or "average rating per product."
   ```javascript
   { $group: { _id: '$category', total: { $sum: '$price' } } }
   ```

3. **`$project`** — Reshapes each document by including, excluding, or computing new fields. Useful for renaming fields, performing calculations, or formatting output.
   ```javascript
   { $project: { name: 1, totalWithTax: { $multiply: ['$price', 1.15] } } }
   ```
</details>

---

## Part 3: Coding Exercises

**16. Write a Mongoose query that finds all products in the "electronics" category with a price between 100 and 500 (inclusive), sorted by price from highest to lowest, showing only the name and price fields.**

<details>
<summary>Answer</summary>

```javascript
const results = await Product.find({
  category: 'electronics',
  price: { $gte: 100, $lte: 500 }
})
  .sort({ price: -1 })
  .select('name price');

console.log(results);
// [
//   { _id: "...", name: "Tablet Pro", price: 499 },
//   { _id: "...", name: "Wireless Headphones", price: 249 },
//   { _id: "...", name: "Smart Watch", price: 199 }
// ]
```

**Breakdown:**
- `category: 'electronics'` — exact match filter
- `price: { $gte: 100, $lte: 500 }` — range filter (inclusive on both ends)
- `.sort({ price: -1 })` — descending order (highest price first)
- `.select('name price')` — only return `name` and `price` (plus `_id` by default)
</details>

---

**17. Implement a reusable pagination function that accepts `page`, `limit`, and an optional `filter` object. It should return the paginated data along with metadata (currentPage, totalPages, totalItems).**

<details>
<summary>Answer</summary>

```javascript
const paginateProducts = async (page = 1, limit = 10, filter = {}) => {
  // Ensure page and limit are positive integers
  page = Math.max(1, parseInt(page));
  limit = Math.max(1, Math.min(100, parseInt(limit))); // cap at 100

  const skip = (page - 1) * limit;

  // Run both queries in parallel for efficiency
  const [data, totalItems] = await Promise.all([
    Product.find(filter)
      .sort({ createdAt: -1 })
      .skip(skip)
      .limit(limit)
      .select('name price category'),
    Product.countDocuments(filter)
  ]);

  const totalPages = Math.ceil(totalItems / limit);

  return {
    data,
    pagination: {
      currentPage: page,
      totalPages,
      totalItems,
      hasNextPage: page < totalPages,
      hasPrevPage: page > 1
    }
  };
};

// Usage examples:
// All products, page 1
const page1 = await paginateProducts(1, 10);

// Only electronics, page 2
const elecPage2 = await paginateProducts(2, 10, { category: 'electronics' });

// Expensive products, page 1
const expensive = await paginateProducts(1, 5, { price: { $gte: 100 } });
```
</details>

---

**18. Set up two models, `Author` and `Book`, with a one-to-many reference relationship. Write code to create an author, create two books referencing that author, and then fetch a book with its author data populated.**

<details>
<summary>Answer</summary>

```javascript
const mongoose = require('mongoose');

// ---------- Author Model ----------
const authorSchema = new mongoose.Schema({
  name:    { type: String, required: true },
  country: { type: String }
});

const Author = mongoose.model('Author', authorSchema);

// ---------- Book Model ----------
const bookSchema = new mongoose.Schema({
  title:     { type: String, required: true },
  year:      { type: Number },
  author:    { type: mongoose.Schema.Types.ObjectId, ref: 'Author', required: true }
});

const Book = mongoose.model('Book', bookSchema);

// ---------- Usage ----------
async function demo() {
  // 1. Create an author
  const author = await Author.create({
    name: 'Khaled Hosseini',
    country: 'Afghanistan'
  });

  // 2. Create two books referencing the author
  await Book.create([
    { title: 'The Kite Runner', year: 2003, author: author._id },
    { title: 'A Thousand Splendid Suns', year: 2007, author: author._id }
  ]);

  // 3. Fetch a book WITH populated author
  const book = await Book.findOne({ title: 'The Kite Runner' })
    .populate('author', 'name country');

  console.log(book);
  // {
  //   _id: "...",
  //   title: "The Kite Runner",
  //   year: 2003,
  //   author: {
  //     _id: "...",
  //     name: "Khaled Hosseini",
  //     country: "Afghanistan"
  //   }
  // }

  // 4. Fetch all books by this author
  const allBooks = await Book.find({ author: author._id })
    .populate('author', 'name');

  console.log(allBooks);
  // [ { title: "The Kite Runner", author: { name: "Khaled Hosseini" } },
  //   { title: "A Thousand Splendid Suns", author: { name: "Khaled Hosseini" } } ]
}
```
</details>

---

**19. Write an aggregation pipeline that calculates the total revenue and average order value per month for completed orders, sorted by most recent month first.**

<details>
<summary>Answer</summary>

```javascript
const monthlyReport = await Order.aggregate([
  // Stage 1: Filter only completed orders
  {
    $match: {
      status: 'completed'
    }
  },

  // Stage 2: Group by year and month
  {
    $group: {
      _id: {
        year:  { $year: '$createdAt' },
        month: { $month: '$createdAt' }
      },
      totalRevenue:   { $sum: '$total' },
      avgOrderValue:  { $avg: '$total' },
      orderCount:     { $sum: 1 },
      highestOrder:   { $max: '$total' },
      lowestOrder:    { $min: '$total' }
    }
  },

  // Stage 3: Sort by most recent first
  {
    $sort: {
      '_id.year': -1,
      '_id.month': -1
    }
  },

  // Stage 4: Reshape the output for readability
  {
    $project: {
      _id: 0,
      year:          '$_id.year',
      month:         '$_id.month',
      totalRevenue:  { $round: ['$totalRevenue', 2] },
      avgOrderValue: { $round: ['$avgOrderValue', 2] },
      orderCount:    1,
      highestOrder:  1,
      lowestOrder:   1
    }
  }
]);

console.log(monthlyReport);
// [
//   {
//     year: 2025, month: 6,
//     totalRevenue: 45230.50, avgOrderValue: 145.00,
//     orderCount: 312, highestOrder: 999.99, lowestOrder: 12.50
//   },
//   {
//     year: 2025, month: 5,
//     totalRevenue: 38750.00, avgOrderValue: 134.08,
//     orderCount: 289, highestOrder: 850.00, lowestOrder: 15.00
//   }
// ]
```
</details>

---

**20. Write an aggregation pipeline using `$lookup` to join an `orders` collection with a `users` collection, then project each order to show only the order total, the user's name, and the user's email.**

<details>
<summary>Answer</summary>

```javascript
const ordersWithUsers = await Order.aggregate([
  // Stage 1: Join with users collection
  {
    $lookup: {
      from: 'users',            // collection to join (use the DB collection name, not Model name)
      localField: 'userId',     // field in orders that references users
      foreignField: '_id',      // field in users to match against
      as: 'user'                // output field name (array)
    }
  },

  // Stage 2: Unwind the user array (since each order has one user)
  {
    $unwind: '$user'
  },

  // Stage 3: Project only the fields we need
  {
    $project: {
      _id: 1,
      orderTotal: '$total',
      orderDate:  '$createdAt',
      userName:   '$user.name',
      userEmail:  '$user.email'
    }
  },

  // Stage 4: Sort by newest orders first
  {
    $sort: { orderDate: -1 }
  }
]);

console.log(ordersWithUsers);
// [
//   {
//     _id: "...",
//     orderTotal: 249.99,
//     orderDate: "2025-06-15T...",
//     userName: "Ali Khan",
//     userEmail: "ali@example.com"
//   },
//   {
//     _id: "...",
//     orderTotal: 89.50,
//     orderDate: "2025-06-14T...",
//     userName: "Sara Ahmed",
//     userEmail: "sara@example.com"
//   }
// ]
```

**Key points:**
- `from` uses the **actual collection name** in MongoDB (lowercase, plural: `'users'`), not the Mongoose model name.
- `$lookup` always outputs an array, so `$unwind` is needed when you expect a single matching document.
- `$project` reshapes the output to include only relevant fields, keeping the API response clean.
</details>
