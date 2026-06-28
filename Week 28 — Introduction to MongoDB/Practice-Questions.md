# Week 28 — Introduction to MongoDB: Practice Questions

**Total Questions: 20** (10 MCQs + 5 Short Answer + 5 Coding Exercises)

---

## Part 1: Multiple Choice Questions (MCQs)

**1. What type of database is MongoDB?**

- A) Relational (SQL)
- B) Document-based (NoSQL)
- C) Graph-based
- D) Key-value store

<details>
<summary>Answer</summary>

**B) Document-based (NoSQL)**

MongoDB is a document-based NoSQL database that stores data in BSON (Binary JSON) format. Unlike relational databases that use tables with rows and columns, MongoDB uses collections of flexible documents.
</details>

---

**2. What data format does MongoDB use internally to store documents?**

- A) JSON
- B) XML
- C) BSON
- D) CSV

<details>
<summary>Answer</summary>

**C) BSON**

BSON stands for Binary JSON. While MongoDB documents look like JSON when you read and write them, they are stored internally as BSON. BSON extends JSON with additional data types like Date, ObjectId, and Decimal128, and is optimized for storage and traversal speed.
</details>

---

**3. What is the default port number for MongoDB?**

- A) 3000
- B) 5432
- C) 27017
- D) 8080

<details>
<summary>Answer</summary>

**C) 27017**

MongoDB listens on port 27017 by default. This is important when configuring connection strings, for example: `mongodb://localhost:27017/myDatabase`.
</details>

---

**4. Which MongoDB Shell command displays all databases on the server?**

- A) `list databases`
- B) `show dbs`
- C) `db.showAll()`
- D) `SELECT * FROM databases`

<details>
<summary>Answer</summary>

**B) `show dbs`**

The `show dbs` command lists all databases on the MongoDB server along with their sizes. Note that a database only appears in this list after it contains at least one document.
</details>

---

**5. What happens if you do not provide an `_id` field when inserting a document?**

- A) The insert fails with an error
- B) MongoDB sets `_id` to null
- C) MongoDB automatically generates an ObjectId
- D) The document is stored without an `_id`

<details>
<summary>Answer</summary>

**C) MongoDB automatically generates an ObjectId**

Every document in MongoDB must have a unique `_id` field. If you do not provide one, MongoDB automatically generates a 12-byte ObjectId (displayed as 24 hex characters) that includes a timestamp, random value, and incrementing counter.
</details>

---

**6. Which method inserts multiple documents into a collection at once?**

- A) `db.collection.insertOne([])`
- B) `db.collection.insertMany([])`
- C) `db.collection.insertAll([])`
- D) `db.collection.bulkInsert([])`

<details>
<summary>Answer</summary>

**B) `db.collection.insertMany([])`**

`insertMany()` accepts an array of documents and inserts them all into the collection in a single operation. It returns an object containing the `insertedIds` for all newly created documents.
</details>

---

**7. What does the `$set` operator do in an update operation?**

- A) Deletes the specified fields
- B) Sets the value of specified fields
- C) Increments a numeric field
- D) Renames a field

<details>
<summary>Answer</summary>

**B) Sets the value of specified fields**

The `$set` operator replaces the value of a field with a specified value. If the field does not exist, `$set` creates it. Example: `db.users.updateOne({ name: "Ali" }, { $set: { age: 26 } })`.
</details>

---

**8. Which SQL term is equivalent to a MongoDB "collection"?**

- A) Database
- B) Row
- C) Table
- D) Column

<details>
<summary>Answer</summary>

**C) Table**

In MongoDB terminology, a "collection" is equivalent to a "table" in SQL databases. Similarly, a "document" is equivalent to a "row," and a "field" is equivalent to a "column."
</details>

---

**9. What does `db.users.find({ age: { $gt: 25 } })` return?**

- A) Users with age equal to 25
- B) Users with age greater than 25
- C) Users with age greater than or equal to 25
- D) Users with age less than 25

<details>
<summary>Answer</summary>

**B) Users with age greater than 25**

The `$gt` operator stands for "greater than." It matches documents where the field value is strictly greater than the specified value. To include 25, you would use `$gte` (greater than or equal to).
</details>

---

**10. What is MongoDB Atlas?**

- A) A MongoDB desktop application
- B) A MongoDB query language
- C) A fully managed cloud database service
- D) A MongoDB testing framework

<details>
<summary>Answer</summary>

**C) A fully managed cloud database service**

MongoDB Atlas is the official cloud-hosted version of MongoDB. It handles server setup, security, backups, scaling, and maintenance. Atlas offers a free tier (M0) with 512MB storage, making it ideal for development and learning.
</details>

---

## Part 2: Short Answer Questions

**1. Explain the difference between `insertOne()` and `insertMany()` with an example of when you would use each.**

<details>
<summary>Answer</summary>

`insertOne()` inserts a single document into a collection, while `insertMany()` inserts an array of multiple documents at once.

**Use `insertOne()`** when adding a single record, for example, when a user registers on your website:

```javascript
db.users.insertOne({ name: "Ali", email: "ali@example.com" });
```

**Use `insertMany()`** when seeding initial data or importing bulk records, for example, adding a catalog of products:

```javascript
db.products.insertMany([
  { name: "Laptop", price: 999 },
  { name: "Phone", price: 699 },
  { name: "Tablet", price: 499 }
]);
```

`insertMany()` is more efficient for bulk operations because it makes a single round-trip to the database server instead of multiple individual requests.
</details>

---

**2. What is the difference between `deleteOne()` and `deleteMany()`? What happens if you call `deleteMany({})` with an empty filter?**

<details>
<summary>Answer</summary>

`deleteOne()` removes the **first** document that matches the filter. `deleteMany()` removes **all** documents that match the filter.

If you call `deleteMany({})` with an empty filter (empty object), it deletes **every document** in the collection. This is equivalent to clearing the entire collection but keeps the collection itself intact (unlike `db.collection.drop()` which removes the collection entirely).

```javascript
// Deletes the first user named "Ali"
db.users.deleteOne({ name: "Ali" });

// Deletes ALL users in Karachi
db.users.deleteMany({ city: "Karachi" });

// Deletes ALL documents in the users collection
db.users.deleteMany({});
```
</details>

---

**3. What is an ObjectId in MongoDB? Describe its structure and purpose.**

<details>
<summary>Answer</summary>

An **ObjectId** is a 12-byte unique identifier that MongoDB generates automatically for the `_id` field of every document. It is displayed as a 24-character hexadecimal string.

**Structure (12 bytes total):**

- **4 bytes:** Unix timestamp (when the document was created)
- **5 bytes:** Random value (unique to the machine and process)
- **3 bytes:** Incrementing counter (ensures uniqueness within the same second)

**Purpose:**

- Provides a globally unique identifier without a centralized counter
- Embeds the creation timestamp, so you can extract when a document was created
- Is small enough to be efficient as an index key
- Does not require coordination between servers (important for distributed systems)

Example: `ObjectId("6578a1b2c3d4e5f6a7b8c9d0")`
</details>

---

**4. Compare SQL and NoSQL databases. Give two scenarios where you would prefer NoSQL over SQL.**

<details>
<summary>Answer</summary>

**Key Differences:**

| Aspect        | SQL                          | NoSQL                            |
|---------------|------------------------------|----------------------------------|
| Schema        | Fixed, predefined            | Flexible, dynamic                |
| Data format   | Tables with rows/columns     | Documents, key-value, etc.       |
| Relationships | JOINs between tables         | Embedding or referencing         |
| Scaling       | Vertical (bigger server)     | Horizontal (more servers)        |

**Two scenarios favoring NoSQL:**

1. **Social media platform:** User posts can vary widely in structure — some have images, some have videos, some have polls, some have location data. A flexible document model handles this variation naturally without null-filled columns.

2. **Real-time analytics dashboard:** When ingesting millions of events per second with varying fields (page views, clicks, purchases), NoSQL handles the high write throughput and schema variations better than a rigid relational schema.
</details>

---

**5. What is MongoDB Compass? How does it differ from the MongoDB Shell?**

<details>
<summary>Answer</summary>

**MongoDB Compass** is the official graphical user interface (GUI) for MongoDB. It provides a visual way to explore databases, browse documents, build queries, view performance metrics, and manage indexes.

**MongoDB Shell (mongosh)** is a command-line interface (CLI) that uses JavaScript syntax to interact with MongoDB.

| Feature              | MongoDB Compass (GUI)          | MongoDB Shell (CLI)           |
|----------------------|-------------------------------|-------------------------------|
| Interface            | Visual, point-and-click       | Text-based, command-driven    |
| Best for             | Exploring data, beginners     | Scripting, automation         |
| Query building       | Visual query builder          | Write queries manually        |
| Performance insights | Built-in charts and metrics   | Manual profiling commands     |
| Automation           | Not designed for scripting    | Fully scriptable              |

Both tools connect to the same MongoDB server and can perform the same operations. Compass is better for visual exploration, while the shell is better for scripting and production workflows.
</details>

---

## Part 3: Coding Exercises

**Exercise 1: Insert a Collection of Students**

Create a database called `school` and insert five student documents into a `students` collection. Each student should have: `name`, `age`, `grade`, `subjects` (array), and `isActive` (boolean).

<details>
<summary>Solution</summary>

```javascript
// Switch to the school database
use school

// Insert five students
db.students.insertMany([
  {
    name: "Ahmed Hassan",
    age: 16,
    grade: "10th",
    subjects: ["Math", "Science", "English"],
    isActive: true
  },
  {
    name: "Zainab Ali",
    age: 15,
    grade: "9th",
    subjects: ["Math", "Art", "History"],
    isActive: true
  },
  {
    name: "Bilal Khan",
    age: 17,
    grade: "11th",
    subjects: ["Physics", "Chemistry", "Math"],
    isActive: false
  },
  {
    name: "Maryam Noor",
    age: 16,
    grade: "10th",
    subjects: ["Biology", "English", "Urdu"],
    isActive: true
  },
  {
    name: "Usman Tariq",
    age: 18,
    grade: "12th",
    subjects: ["Computer Science", "Math", "Physics"],
    isActive: true
  }
]);

// Verify insertion
db.students.find().pretty();
```
</details>

---

**Exercise 2: Query with Filters and Projections**

Using the `students` collection from Exercise 1, write queries to:
1. Find all students in grade "10th"
2. Find all active students older than 15
3. Find all students and display only their `name` and `grade` (exclude `_id`)

<details>
<summary>Solution</summary>

```javascript
// 1. Find all students in grade "10th"
db.students.find({ grade: "10th" });
// Returns: Ahmed Hassan and Maryam Noor

// 2. Find all active students older than 15
db.students.find({
  isActive: true,
  age: { $gt: 15 }
});
// Returns: Ahmed Hassan (16), Maryam Noor (16), Usman Tariq (18)

// 3. Display only name and grade, exclude _id
db.students.find(
  {},
  { name: 1, grade: 1, _id: 0 }
);
// Returns:
// { name: "Ahmed Hassan", grade: "10th" }
// { name: "Zainab Ali", grade: "9th" }
// { name: "Bilal Khan", grade: "11th" }
// { name: "Maryam Noor", grade: "10th" }
// { name: "Usman Tariq", grade: "12th" }
```
</details>

---

**Exercise 3: Update Documents**

Using the `students` collection:
1. Update Bilal Khan's `isActive` status to `true`
2. Add "Computer Science" to Ahmed Hassan's `subjects` array
3. Increment all students' ages by 1

<details>
<summary>Solution</summary>

```javascript
// 1. Update Bilal Khan's isActive to true
db.students.updateOne(
  { name: "Bilal Khan" },
  { $set: { isActive: true } }
);

// Verify
db.students.findOne({ name: "Bilal Khan" });
// isActive is now true

// 2. Add "Computer Science" to Ahmed's subjects
db.students.updateOne(
  { name: "Ahmed Hassan" },
  { $push: { subjects: "Computer Science" } }
);

// Verify
db.students.findOne({ name: "Ahmed Hassan" });
// subjects now includes "Computer Science"

// 3. Increment all students' ages by 1
db.students.updateMany(
  {},
  { $inc: { age: 1 } }
);

// Verify
db.students.find({}, { name: 1, age: 1, _id: 0 });
// All ages have increased by 1
```
</details>

---

**Exercise 4: Delete Documents and Clean Up**

Using the `students` collection:
1. Delete the student named "Usman Tariq"
2. Delete all students who are in grade "9th"
3. Count the remaining documents in the collection

<details>
<summary>Solution</summary>

```javascript
// 1. Delete Usman Tariq
db.students.deleteOne({ name: "Usman Tariq" });
// { acknowledged: true, deletedCount: 1 }

// 2. Delete all students in 9th grade
db.students.deleteMany({ grade: "9th" });
// { acknowledged: true, deletedCount: 1 } (Zainab Ali)

// 3. Count remaining documents
db.students.countDocuments();
// Returns: 3 (Ahmed Hassan, Bilal Khan, Maryam Noor)

// You can also verify by listing them
db.students.find({}, { name: 1, _id: 0 });
// { name: "Ahmed Hassan" }
// { name: "Bilal Khan" }
// { name: "Maryam Noor" }
```
</details>

---

**Exercise 5: MongoDB Atlas Setup Verification**

Create a MongoDB Atlas account (if you have not already) and complete these steps:
1. Create a free-tier cluster (M0)
2. Create a database user with read/write access
3. Whitelist your IP address
4. Connect using `mongosh` with your Atlas connection string
5. Create a database called `testAtlas` and insert one document

<details>
<summary>Solution</summary>

**Step-by-step verification:**

```bash
# Step 4: Connect to Atlas via mongosh
mongosh "mongodb+srv://yourUsername:yourPassword@cluster0.xxxxx.mongodb.net/"
```

```javascript
// Step 5: Create database and insert a document
use testAtlas

db.testCollection.insertOne({
  message: "Atlas is connected!",
  timestamp: new Date(),
  source: "Week 28 Exercise"
});

// Verify the document exists
db.testCollection.find().pretty();
// Should display:
// {
//   _id: ObjectId("..."),
//   message: "Atlas is connected!",
//   timestamp: ISODate("2024-..."),
//   source: "Week 28 Exercise"
// }

// Verify the database appears
show dbs
// testAtlas should appear in the list
```

**Checklist:**

- [ ] Atlas account created at mongodb.com/atlas
- [ ] Free-tier cluster (M0) deployed
- [ ] Database user created with readWriteAnyDatabase role
- [ ] IP address whitelisted (or 0.0.0.0/0 for development)
- [ ] Successfully connected via mongosh
- [ ] Document inserted and verified in testAtlas database
</details>
