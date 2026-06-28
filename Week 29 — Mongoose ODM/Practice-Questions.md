# Week 29 — Mongoose ODM: Practice Questions

**Total Questions: 20** (10 MCQs + 5 Short Answer + 5 Coding Exercises)

---

## Part 1: Multiple Choice Questions (MCQs)

**1. What does ODM stand for in the context of Mongoose?**

- A) Object Document Manager
- B) Object Data Modeling
- C) Online Database Module
- D) Object Driven Middleware

<details>
<summary>Answer</summary>

**B) Object Data Modeling**

Mongoose is an Object Data Modeling (ODM) library for MongoDB and Node.js. It manages relationships between data, provides schema validation, and translates between objects in your code and their representation in MongoDB.
</details>

---

**2. What method is used to connect Mongoose to a MongoDB database?**

- A) `mongoose.open()`
- B) `mongoose.connect()`
- C) `mongoose.link()`
- D) `mongoose.start()`

<details>
<summary>Answer</summary>

**B) `mongoose.connect()`**

`mongoose.connect()` takes a connection string (e.g., `"mongodb://localhost:27017/myApp"`) and returns a Promise. It establishes a connection pool to the MongoDB server.
</details>

---

**3. What does Mongoose automatically do to a model name when creating a collection?**

- A) Keeps it exactly the same
- B) Converts to uppercase
- C) Converts to lowercase and pluralizes
- D) Adds a "collection_" prefix

<details>
<summary>Answer</summary>

**C) Converts to lowercase and pluralizes**

When you create `mongoose.model("Product", schema)`, Mongoose automatically creates a collection called `products` (lowercase + plural). `"User"` becomes `"users"`, `"Category"` becomes `"categories"`.
</details>

---

**4. Which option must you pass to `findByIdAndUpdate()` to receive the updated document instead of the original?**

- A) `{ updated: true }`
- B) `{ new: true }`
- C) `{ return: "after" }`
- D) `{ fresh: true }`

<details>
<summary>Answer</summary>

**B) `{ new: true }`**

By default, `findByIdAndUpdate()` returns the document as it was **before** the update. Passing `{ new: true }` tells Mongoose to return the document **after** the update has been applied.

```javascript
const updated = await User.findByIdAndUpdate(id, { age: 26 }, { new: true });
```
</details>

---

**5. What is the purpose of the `required` validator in a Mongoose schema?**

- A) It sets a default value for the field
- B) It ensures the field must be present when saving a document
- C) It creates a unique index on the field
- D) It converts the field to a specific type

<details>
<summary>Answer</summary>

**B) It ensures the field must be present when saving a document**

When `required: true` is set on a schema field, Mongoose throws a `ValidationError` if you try to save a document without providing a value for that field. You can also provide a custom error message: `required: [true, "Name is required"]`.
</details>

---

**6. What is the difference between `Model.create()` and `new Model() + save()`?**

- A) `create()` is faster because it skips validation
- B) There is no difference — they are identical
- C) `new Model() + save()` allows modifying the document before saving
- D) `create()` does not trigger middleware hooks

<details>
<summary>Answer</summary>

**C) `new Model() + save()` allows modifying the document before saving**

`Model.create(data)` is a shorthand that creates a new document and saves it immediately. Using `new Model(data)` creates the document in memory first, giving you a chance to modify it, run logic, or conditionally adjust fields before calling `.save()`.
</details>

---

**7. Which validator restricts a string field to a specific set of allowed values?**

- A) `match`
- B) `enum`
- C) `in`
- D) `values`

<details>
<summary>Answer</summary>

**B) `enum`**

The `enum` validator specifies an array of allowed values. If a value not in the array is provided, Mongoose throws a validation error.

```javascript
role: {
  type: String,
  enum: ["user", "admin", "moderator"]
}
```
</details>

---

**8. What are Mongoose virtuals?**

- A) Fields that are stored in a separate virtual collection
- B) Computed properties that are NOT stored in the database
- C) Encrypted fields for sensitive data
- D) Temporary fields that expire after a set time

<details>
<summary>Answer</summary>

**B) Computed properties that are NOT stored in the database**

Virtuals are properties that you can get and set but that are not persisted to MongoDB. They are calculated on the fly from other stored fields. For example, a `fullName` virtual computed from `firstName` and `lastName`.
</details>

---

**9. Why should you NOT use arrow functions when defining instance methods?**

- A) Arrow functions are slower in Node.js
- B) Arrow functions do not bind `this` to the document
- C) Arrow functions cannot return values
- D) Mongoose does not support ES6 syntax

<details>
<summary>Answer</summary>

**B) Arrow functions do not bind `this` to the document**

Arrow functions inherit `this` from their surrounding scope (lexical `this`), so inside an instance method, `this` would not point to the document. Regular functions bind `this` to the calling context, which is the document instance in Mongoose.

```javascript
// WRONG - this is undefined/wrong context
userSchema.methods.greet = () => `Hello, ${this.name}`;

// CORRECT - this refers to the document
userSchema.methods.greet = function () { return `Hello, ${this.name}`; };
```
</details>

---

**10. What is the difference between instance methods and static methods in Mongoose?**

- A) Instance methods are faster; static methods are slower
- B) Instance methods run on individual documents; static methods run on the Model
- C) Static methods can only read data; instance methods can write data
- D) There is no difference — they are aliases

<details>
<summary>Answer</summary>

**B) Instance methods run on individual documents; static methods run on the Model**

Instance methods are called on a specific document (`user.getSummary()`) and have access to that document's data via `this`. Static methods are called on the Model itself (`User.findAdmins()`) and operate on the entire collection.
</details>

---

## Part 2: Short Answer Questions

**1. Explain the role of a Mongoose Schema. What happens if you try to save a field that is not defined in the schema?**

<details>
<summary>Answer</summary>

A Mongoose **Schema** defines the structure of documents in a MongoDB collection. It specifies:

- **Field names** and their **data types** (String, Number, Boolean, Date, etc.)
- **Validation rules** (required, min, max, enum, match, custom)
- **Default values** for fields
- **Options** like timestamps, virtuals, and indexes

If you try to save a field that is not defined in the schema, Mongoose **silently ignores** it by default. The document is saved without the undefined field. This is called "strict mode" and is enabled by default.

```javascript
const userSchema = new mongoose.Schema({ name: String });
const User = mongoose.model("User", userSchema);

await User.create({ name: "Ali", favoriteColor: "blue" });
// "favoriteColor" is silently removed — only { name: "Ali" } is saved
```

You can change this behavior by setting `strict: false` in schema options, but this is generally not recommended.
</details>

---

**2. What are timestamps in Mongoose? How do you enable them and what fields do they add?**

<details>
<summary>Answer</summary>

**Timestamps** are an automatic feature that adds two date fields to every document:

- **`createdAt`**: Set once when the document is first created, never changed afterward
- **`updatedAt`**: Set when created and automatically updated every time the document is modified and saved

**Enabling timestamps:**

```javascript
const postSchema = new mongoose.Schema(
  { title: String, content: String },
  { timestamps: true }  // Pass as second argument (schema options)
);
```

**Custom field names:**

```javascript
const postSchema = new mongoose.Schema(
  { title: String },
  { timestamps: { createdAt: "created_at", updatedAt: "updated_at" } }
);
```

Timestamps are useful for:

- Tracking when records were created
- Sorting by most recent
- Implementing "last modified" features
- Audit trails
</details>

---

**3. Compare `findByIdAndUpdate()` with the `find() + save()` pattern. When would you use each?**

<details>
<summary>Answer</summary>

**`findByIdAndUpdate()`** finds a document by its `_id` and updates it in a single atomic operation. It sends an `updateOne` command directly to MongoDB.

**`find() + save()`** first retrieves the document into memory, modifies it in your application code, then saves it back to the database.

| Aspect                  | `findByIdAndUpdate()`          | `find() + save()`              |
|-------------------------|--------------------------------|--------------------------------|
| Database operations     | 1 (single atomic update)       | 2 (find + update)              |
| Middleware (pre/post)   | Pre/post `findOneAndUpdate`    | Pre/post `save`                |
| Validation              | Only with `runValidators: true`| Always runs validators         |
| Document modification   | Limited to update operators    | Full JavaScript logic possible |

**Use `findByIdAndUpdate()`** for simple field updates where performance matters:

```javascript
await User.findByIdAndUpdate(id, { age: 26 }, { new: true, runValidators: true });
```

**Use `find() + save()`** when you need complex logic before saving:

```javascript
const user = await User.findById(id);
user.loginCount += 1;
user.lastLogin = new Date();
if (user.loginCount > 100) user.badge = "power-user";
await user.save();
```
</details>

---

**4. Explain the difference between `unique: true` and `required: true` in a Mongoose schema.**

<details>
<summary>Answer</summary>

**`required: true`** is a **validator**. It ensures that the field must be present (not `null`, `undefined`, or empty string) when saving a document. If the field is missing, Mongoose throws a `ValidationError`.

**`unique: true`** is **not a validator** — it creates a **unique index** in MongoDB. It ensures that no two documents can have the same value for that field. If a duplicate value is inserted, MongoDB throws a `MongoServerError` with code `11000` (duplicate key error).

Key differences:

| Aspect              | `required: true`                | `unique: true`                 |
|---------------------|---------------------------------|--------------------------------|
| Type                | Mongoose validator              | MongoDB index                  |
| Checks              | Field must be present           | Field must not be duplicated   |
| Error type          | `ValidationError`               | `MongoServerError` (code 11000)|
| Allows null         | No                              | Yes (but only one null)        |
| Handled by          | Mongoose (before sending to DB) | MongoDB (at the database level)|

```javascript
email: {
  type: String,
  required: true,  // Must be provided
  unique: true     // Must be different from all other documents
}
```
</details>

---

**5. What is a virtual setter? Provide a practical example of when you would use one.**

<details>
<summary>Answer</summary>

A **virtual setter** is a function that runs when you assign a value to a virtual property. It takes the assigned value and breaks it down into actual stored fields.

**Practical example — setting a full name:**

```javascript
const userSchema = new mongoose.Schema({
  firstName: String,
  lastName: String
});

userSchema.virtual("fullName")
  .get(function () {
    return `${this.firstName} ${this.lastName}`;
  })
  .set(function (fullName) {
    const parts = fullName.split(" ");
    this.firstName = parts[0];
    this.lastName = parts.slice(1).join(" ");
  });
```

Usage:

```javascript
const user = new User();
user.fullName = "Ali Ahmed Khan";   // Virtual setter runs
console.log(user.firstName);        // "Ali"
console.log(user.lastName);         // "Ahmed Khan"
```

Virtual setters are useful when an API or form sends combined data (like a full name or full address) that needs to be stored as separate fields in the database.
</details>

---

## Part 3: Coding Exercises

**Exercise 1: Create a Product Schema and Model**

Create a Mongoose schema for a `Product` with the following fields:
- `name` (String, required, trimmed, 2-100 characters)
- `price` (Number, required, minimum 0)
- `category` (String, required, only "electronics", "clothing", "books", or "food")
- `inStock` (Boolean, default `true`)
- `tags` (Array of Strings)

Create the model and export it.

<details>
<summary>Solution</summary>

```javascript
const mongoose = require("mongoose");

const productSchema = new mongoose.Schema(
  {
    name: {
      type: String,
      required: [true, "Product name is required"],
      trim: true,
      minlength: [2, "Name must be at least 2 characters"],
      maxlength: [100, "Name cannot exceed 100 characters"]
    },
    price: {
      type: Number,
      required: [true, "Price is required"],
      min: [0, "Price cannot be negative"]
    },
    category: {
      type: String,
      required: [true, "Category is required"],
      enum: {
        values: ["electronics", "clothing", "books", "food"],
        message: "{VALUE} is not a valid category"
      }
    },
    inStock: {
      type: Boolean,
      default: true
    },
    tags: {
      type: [String],
      default: []
    }
  },
  {
    timestamps: true
  }
);

const Product = mongoose.model("Product", productSchema);

module.exports = Product;
```
</details>

---

**Exercise 2: Complete CRUD Operations**

Using the `Product` model from Exercise 1, write async functions that:
1. Create three products
2. Find all products in the "electronics" category
3. Update a product's price by its ID
4. Delete a product by its ID

<details>
<summary>Solution</summary>

```javascript
const mongoose = require("mongoose");
const Product = require("./models/Product");

async function main() {
  await mongoose.connect("mongodb://localhost:27017/shopDB");

  // 1. Create three products
  const products = await Product.create([
    {
      name: "Wireless Mouse",
      price: 29.99,
      category: "electronics",
      tags: ["computer", "wireless", "accessory"]
    },
    {
      name: "JavaScript Book",
      price: 39.99,
      category: "books",
      tags: ["programming", "web-development"]
    },
    {
      name: "Cotton T-Shirt",
      price: 15.99,
      category: "clothing",
      tags: ["casual", "summer"]
    }
  ]);

  console.log("Created products:", products.length);

  // 2. Find all electronics
  const electronics = await Product.find({ category: "electronics" });
  console.log("Electronics:", electronics);

  // 3. Update a product's price by ID
  const updatedProduct = await Product.findByIdAndUpdate(
    products[0]._id,
    { price: 24.99 },
    { new: true, runValidators: true }
  );
  console.log("Updated product:", updatedProduct.name, "-> $" + updatedProduct.price);

  // 4. Delete a product by ID
  const deletedProduct = await Product.findByIdAndDelete(products[2]._id);
  console.log("Deleted product:", deletedProduct.name);

  // Verify remaining products
  const remaining = await Product.find();
  console.log("Remaining products:", remaining.length);

  await mongoose.connection.close();
}

main().catch(console.error);
```
</details>

---

**Exercise 3: Schema with Custom Validation**

Create a `User` schema with the following requirements:
- `username` (String, required, 3-20 characters, must be alphanumeric)
- `email` (String, required, must match email format)
- `age` (Number, must be between 13 and 120)
- `password` (String, required, minimum 8 characters, must contain at least one number)

Write code that attempts to create an invalid user and properly catches and displays all validation errors.

<details>
<summary>Solution</summary>

```javascript
const mongoose = require("mongoose");

const userSchema = new mongoose.Schema({
  username: {
    type: String,
    required: [true, "Username is required"],
    minlength: [3, "Username must be at least 3 characters"],
    maxlength: [20, "Username cannot exceed 20 characters"],
    validate: {
      validator: function (value) {
        return /^[a-zA-Z0-9]+$/.test(value);
      },
      message: "Username must contain only letters and numbers"
    }
  },
  email: {
    type: String,
    required: [true, "Email is required"],
    lowercase: true,
    match: [/^\S+@\S+\.\S+$/, "Please enter a valid email address"]
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
    required: [true, "Password is required"],
    minlength: [8, "Password must be at least 8 characters"],
    validate: {
      validator: function (value) {
        return /\d/.test(value);
      },
      message: "Password must contain at least one number"
    }
  }
});

const User = mongoose.model("User", userSchema);

async function testValidation() {
  await mongoose.connect("mongodb://localhost:27017/testDB");

  try {
    // Attempt to create an invalid user
    await User.create({
      username: "a!",           // Too short + has special character
      email: "not-an-email",    // Invalid email format
      age: 10,                  // Below minimum (13)
      password: "short"         // Too short + no number
    });
  } catch (error) {
    if (error.name === "ValidationError") {
      console.log("Validation Errors Found:");
      console.log("========================");

      for (const field in error.errors) {
        console.log(`  ${field}: ${error.errors[field].message}`);
      }
    }
  }

  // Expected output:
  // Validation Errors Found:
  // ========================
  //   username: Username must contain only letters and numbers
  //   email: Please enter a valid email address
  //   age: Age must be between 13 and 120
  //   password: Password must be at least 8 characters

  await mongoose.connection.close();
}

testValidation();
```
</details>

---

**Exercise 4: Virtuals and Instance Methods**

Create a `Student` model with:
- Fields: `firstName`, `lastName`, `scores` (array of numbers)
- Virtual: `fullName` (getter and setter)
- Instance method: `getAverage()` that returns the average of scores
- Instance method: `isPassing()` that returns true if average is 60 or above

<details>
<summary>Solution</summary>

```javascript
const mongoose = require("mongoose");

const studentSchema = new mongoose.Schema({
  firstName: { type: String, required: true },
  lastName: { type: String, required: true },
  scores: { type: [Number], default: [] }
});

// Virtual: fullName (getter)
studentSchema.virtual("fullName")
  .get(function () {
    return `${this.firstName} ${this.lastName}`;
  })
  .set(function (fullName) {
    const parts = fullName.split(" ");
    this.firstName = parts[0];
    this.lastName = parts.slice(1).join(" ");
  });

// Instance method: getAverage
studentSchema.methods.getAverage = function () {
  if (this.scores.length === 0) return 0;
  const sum = this.scores.reduce((total, score) => total + score, 0);
  return Math.round((sum / this.scores.length) * 100) / 100;
};

// Instance method: isPassing
studentSchema.methods.isPassing = function () {
  return this.getAverage() >= 60;
};

// Include virtuals in JSON output
studentSchema.set("toJSON", { virtuals: true });

const Student = mongoose.model("Student", studentSchema);

// Test the model
async function testStudent() {
  await mongoose.connect("mongodb://localhost:27017/schoolDB");

  const student = await Student.create({
    firstName: "Ahmed",
    lastName: "Hassan",
    scores: [85, 72, 90, 68, 95]
  });

  console.log("Full Name:", student.fullName);       // "Ahmed Hassan"
  console.log("Average:", student.getAverage());      // 82
  console.log("Passing:", student.isPassing());       // true

  // Test virtual setter
  const student2 = new Student();
  student2.fullName = "Zainab Ali Khan";
  console.log("First:", student2.firstName);          // "Zainab"
  console.log("Last:", student2.lastName);            // "Ali Khan"

  await mongoose.connection.close();
}

testStudent().catch(console.error);
```
</details>

---

**Exercise 5: Static Methods**

Add the following static methods to a `Book` model:
- `findByCategory(category)` — finds all books in a given category
- `findExpensive(minPrice)` — finds all books above a minimum price
- `getStats()` — returns total count, average price, and books per category

<details>
<summary>Solution</summary>

```javascript
const mongoose = require("mongoose");

const bookSchema = new mongoose.Schema({
  title: { type: String, required: true },
  author: { type: String, required: true },
  price: { type: Number, required: true, min: 0 },
  category: {
    type: String,
    required: true,
    enum: ["fiction", "non-fiction", "science", "history", "technology"]
  },
  publishedYear: Number
});

// Static: find by category
bookSchema.statics.findByCategory = function (category) {
  return this.find({ category }).sort({ title: 1 });
};

// Static: find expensive books
bookSchema.statics.findExpensive = function (minPrice) {
  return this.find({ price: { $gte: minPrice } }).sort({ price: -1 });
};

// Static: get collection statistics
bookSchema.statics.getStats = async function () {
  const total = await this.countDocuments();

  const priceAgg = await this.aggregate([
    { $group: { _id: null, avgPrice: { $avg: "$price" } } }
  ]);
  const avgPrice = priceAgg.length > 0
    ? Math.round(priceAgg[0].avgPrice * 100) / 100
    : 0;

  const categoryAgg = await this.aggregate([
    { $group: { _id: "$category", count: { $sum: 1 } } },
    { $sort: { count: -1 } }
  ]);
  const byCategory = {};
  categoryAgg.forEach((item) => {
    byCategory[item._id] = item.count;
  });

  return { total, avgPrice, byCategory };
};

const Book = mongoose.model("Book", bookSchema);

// Test static methods
async function testStatics() {
  await mongoose.connect("mongodb://localhost:27017/libraryDB");

  // Seed data
  await Book.deleteMany({});
  await Book.create([
    { title: "Dune", author: "Frank Herbert", price: 14.99, category: "fiction", publishedYear: 1965 },
    { title: "Clean Code", author: "Robert Martin", price: 34.99, category: "technology", publishedYear: 2008 },
    { title: "Sapiens", author: "Yuval Harari", price: 18.99, category: "history", publishedYear: 2011 },
    { title: "The Pragmatic Programmer", author: "David Thomas", price: 42.99, category: "technology", publishedYear: 1999 },
    { title: "1984", author: "George Orwell", price: 9.99, category: "fiction", publishedYear: 1949 }
  ]);

  // Find by category
  const techBooks = await Book.findByCategory("technology");
  console.log("Tech books:", techBooks.map((b) => b.title));
  // ["Clean Code", "The Pragmatic Programmer"]

  // Find expensive books (above $20)
  const expensive = await Book.findExpensive(20);
  console.log("Expensive:", expensive.map((b) => `${b.title} ($${b.price})`));
  // ["The Pragmatic Programmer ($42.99)", "Clean Code ($34.99)"]

  // Get stats
  const stats = await Book.getStats();
  console.log("Stats:", stats);
  // { total: 5, avgPrice: 24.39, byCategory: { technology: 2, fiction: 2, history: 1 } }

  await mongoose.connection.close();
}

testStatics().catch(console.error);
```
</details>
