# Week 12: Objects, DOM & Events

A comprehensive guide to JavaScript objects, JSON, DOM manipulation, and event handling. This document builds on the fundamentals covered in Weeks 9-11 (variables, data types, control flow, loops, functions, and arrays) and prepares students for building truly interactive web applications.

---

## Table of Contents

1. [JavaScript Objects](#1-javascript-objects)
   - [What is an Object?](#11-what-is-an-object)
   - [Creating Objects: Literal Syntax](#12-creating-objects-literal-syntax)
   - [Properties and Values](#13-properties-and-values)
   - [Accessing Properties](#14-accessing-properties-dot-vs-bracket-notation)
   - [Adding, Modifying, and Deleting Properties](#15-adding-modifying-and-deleting-properties)
   - [Methods in Objects](#16-methods-in-objects)
   - [The this Keyword](#17-the-this-keyword)
   - [Nested Objects](#18-nested-objects)
   - [Object Destructuring (ES6)](#19-object-destructuring-es6)
   - [Spread Operator with Objects](#110-spread-operator-with-objects)
   - [Object.keys(), Object.values(), Object.entries()](#111-objectkeys-objectvalues-objectentries)
   - [Looping Through Objects with for...in](#112-looping-through-objects-with-forin)
2. [JSON (JavaScript Object Notation)](#2-json-javascript-object-notation)
   - [What is JSON?](#21-what-is-json)
   - [JSON Syntax Rules](#22-json-syntax-rules)
   - [JSON.stringify()](#23-jsonstringify--object-to-json-string)
   - [JSON.parse()](#24-jsonparse--json-string-to-object)
   - [Real-Life Use Case: APIs](#25-real-life-use-case-apis-and-json)
3. [DOM Manipulation](#3-dom-manipulation)
   - [What is the DOM?](#31-what-is-the-dom)
   - [DOM Tree Diagram](#32-dom-tree-diagram)
   - [Selecting Elements](#33-selecting-elements)
   - [Modifying Element Content](#34-modifying-element-content)
   - [Modifying Styles](#35-modifying-styles)
   - [Modifying Attributes](#36-modifying-attributes)
   - [Creating and Removing Elements](#37-creating-and-removing-elements)
   - [Parent, Child, and Sibling Navigation](#38-parent-child-and-sibling-navigation)
4. [JavaScript Events](#4-javascript-events)
   - [What are Events?](#41-what-are-events)
   - [Event Listeners](#42-event-listeners-addeventlistener)
   - [Common Events Table](#43-common-events-table)
   - [The Event Object](#44-the-event-object)
   - [event.preventDefault()](#45-eventpreventdefault)
   - [event.target](#46-eventtarget)
   - [Event Bubbling and Capturing](#47-event-bubbling-and-capturing)
   - [Event Delegation](#48-event-delegation)
5. [Week 12 Project: Interactive To-Do App](#5-week-12-project-interactive-to-do-app)
6. [Summary: JavaScript Weeks 9-12 Recap](#6-summary--javascript-weeks-9-12-recap)

---

## 1. JavaScript Objects

### 1.1 What is an Object?

An object is a collection of related data and functionality stored together as **key-value pairs**. While arrays store data in an ordered list accessed by index numbers, objects store data with meaningful names (called **keys** or **properties**).

**Real-Life Analogy: A Student ID Card**

Think of a student ID card. It does not just contain a single piece of data -- it holds multiple related pieces of information grouped together:

```
+-------------------------------------+
|         STUDENT ID CARD             |
|-------------------------------------|
|  Name:       Fahad Ahmed            |
|  Age:        22                     |
|  Roll No:    CS-2024-0042           |
|  Department: Computer Science       |
|  GPA:        3.75                   |
|  Active:     Yes                    |
+-------------------------------------+
```

In JavaScript, this same ID card can be represented as an object:

```javascript
let student = {
    name: "Fahad Ahmed",
    age: 22,
    rollNo: "CS-2024-0042",
    department: "Computer Science",
    gpa: 3.75,
    isActive: true
};
```

Each piece of information has a **key** (like `name`) and a **value** (like `"Fahad Ahmed"`). Together, they form a **property**.

**Why Objects Matter:**

- Arrays are great for lists of similar items (e.g., a list of names).
- Objects are ideal for describing a single entity with multiple attributes (e.g., one student, one product, one user account).

---

### 1.2 Creating Objects: Literal Syntax

The most common and straightforward way to create an object in JavaScript is using **object literal syntax** with curly braces `{}`.

```javascript
// Empty object
let emptyObj = {};

// Object with properties
let car = {
    brand: "Toyota",
    model: "Corolla",
    year: 2024,
    color: "White",
    isElectric: false
};
```

**Rules for Property Names (Keys):**

- Keys are usually written without quotes if they are valid identifiers (no spaces, no special characters, do not start with a number).
- If a key contains spaces or special characters, wrap it in quotes.

```javascript
let person = {
    firstName: "Ali",           // valid identifier -- no quotes needed
    "last name": "Khan",       // contains a space -- quotes required
    "phone-number": "0300..."  // contains a hyphen -- quotes required
};
```

---

### 1.3 Properties and Values

Every object is built from **properties**. Each property is a key-value pair.

```
+--------------------------------------------------+
|  Object: car                                     |
|--------------------------------------------------|
|  KEY (Property)   |   VALUE                      |
|--------------------------------------------------|
|  brand            |   "Toyota"       (string)    |
|  model            |   "Corolla"      (string)    |
|  year             |   2024           (number)    |
|  color            |   "White"        (string)    |
|  isElectric       |   false          (boolean)   |
+--------------------------------------------------+
```

Values can be any JavaScript data type:

| Value Type | Example |
|------------|---------|
| String | `"Fahad"` |
| Number | `25` |
| Boolean | `true` |
| Array | `["Math", "Science"]` |
| Object | `{ city: "Karachi" }` |
| Function | `function() { ... }` |
| null | `null` |
| undefined | `undefined` |

```javascript
let student = {
    name: "Sara",               // string
    age: 20,                    // number
    isEnrolled: true,           // boolean
    courses: ["JS", "React"],   // array
    address: {                  // nested object
        city: "Lahore",
        zip: "54000"
    },
    greet: function() {         // function (method)
        return "Hello!";
    }
};
```

---

### 1.4 Accessing Properties: Dot vs Bracket Notation

There are two ways to read a property's value from an object.

**Dot Notation (Most Common)**

```javascript
let book = {
    title: "JavaScript Essentials",
    author: "John Doe",
    pages: 350
};

console.log(book.title);   // "JavaScript Essentials"
console.log(book.author);  // "John Doe"
console.log(book.pages);   // 350
```

**Bracket Notation**

```javascript
console.log(book["title"]);   // "JavaScript Essentials"
console.log(book["author"]);  // "John Doe"
```

**When Must You Use Bracket Notation?**

1. When the key contains spaces or special characters:

```javascript
let person = { "first name": "Ali" };

// person.first name    -- SYNTAX ERROR
console.log(person["first name"]);  // "Ali"
```

2. When the key is stored in a variable:

```javascript
let key = "title";

console.log(book[key]);    // "JavaScript Essentials"
// console.log(book.key);  // undefined (looks for a property literally named "key")
```

3. When the key is computed dynamically:

```javascript
let field = "auth" + "or";
console.log(book[field]);  // "John Doe"
```

**Comparison Table:**

| Feature | Dot Notation | Bracket Notation |
|---------|-------------|-----------------|
| Syntax | `obj.key` | `obj["key"]` |
| Readability | Cleaner and preferred | Slightly verbose |
| Keys with spaces | Not possible | Works |
| Dynamic keys (variables) | Not possible | Works |
| When to use | Default choice | Special cases above |

---

### 1.5 Adding, Modifying, and Deleting Properties

Objects in JavaScript are **mutable** -- you can change them after creation.

**Adding New Properties**

```javascript
let user = {
    name: "Ahmed"
};

user.age = 25;                 // add using dot notation
user["email"] = "a@mail.com";  // add using bracket notation

console.log(user);
// { name: "Ahmed", age: 25, email: "a@mail.com" }
```

**Modifying Existing Properties**

```javascript
user.name = "Ahmed Khan";   // overwrite existing value
user.age = 26;

console.log(user.name);  // "Ahmed Khan"
console.log(user.age);   // 26
```

**Deleting Properties**

```javascript
delete user.email;

console.log(user);
// { name: "Ahmed Khan", age: 26 }
```

The `delete` operator removes the property entirely from the object. After deletion, accessing that property returns `undefined`.

---

### 1.6 Methods in Objects

When a function is stored as a property of an object, it is called a **method**. Methods define the **behavior** of an object.

**Real-Life Analogy:** A calculator object does not just have data (like its brand) -- it also has actions it can perform (add, subtract, multiply).

```javascript
let calculator = {
    brand: "Casio",

    add: function(a, b) {
        return a + b;
    },

    subtract: function(a, b) {
        return a - b;
    },

    multiply: function(a, b) {
        return a * b;
    }
};

console.log(calculator.add(10, 5));       // 15
console.log(calculator.subtract(10, 5));  // 5
console.log(calculator.multiply(10, 5));  // 50
```

**ES6 Shorthand Method Syntax:**

You can omit the `: function` part for cleaner code:

```javascript
let calculator = {
    brand: "Casio",

    add(a, b) {
        return a + b;
    },

    subtract(a, b) {
        return a - b;
    }
};
```

Both forms are identical in behavior. The shorthand is preferred in modern JavaScript.

---

### 1.7 The `this` Keyword

Inside a method, `this` refers to **the object that the method belongs to**. It allows a method to access other properties of the same object.

**Real-Life Analogy:** When you say "My name is Fahad," the word "my" refers to yourself. Similarly, `this` inside a method refers to the object itself.

```javascript
let student = {
    name: "Fahad",
    age: 22,
    department: "Computer Science",

    introduce() {
        return "Hi, I am " + this.name + " and I study " + this.department;
    }
};

console.log(student.introduce());
// "Hi, I am Fahad and I study Computer Science"
```

**Why not just write `student.name` instead of `this.name`?**

Using `this` makes the method reusable and independent of the variable name:

```javascript
let employee = {
    name: "Sara",
    position: "Developer",

    describe() {
        // this.name works regardless of what variable holds this object
        return this.name + " works as a " + this.position;
    }
};

console.log(employee.describe());  // "Sara works as a Developer"
```

**Important Note:** Arrow functions (`=>`) do NOT have their own `this`. Always use regular functions for object methods when you need `this`.

```javascript
let user = {
    name: "Ali",

    // WRONG -- arrow function does not bind 'this' to the object
    greet: () => {
        return "Hello, " + this.name;  // 'this' is NOT the user object here
    },

    // CORRECT -- regular function binds 'this' to the object
    greetCorrect() {
        return "Hello, " + this.name;  // 'this' IS the user object
    }
};

console.log(user.greetCorrect());  // "Hello, Ali"
```

---

### 1.8 Nested Objects

Objects can contain other objects as values. This is called **nesting** and is very common when representing complex real-world data.

**Real-Life Analogy:** A university record contains a student, who has an address, which itself has a city and zip code. Data is naturally layered.

```javascript
let student = {
    name: "Zainab",
    age: 21,
    address: {
        street: "Block 5, Gulshan",
        city: "Karachi",
        zip: "75300"
    },
    courses: {
        semester1: ["Intro to CS", "Calculus"],
        semester2: ["Data Structures", "OOP"]
    }
};
```

**Accessing Nested Properties:**

```javascript
// Access city using dot notation chain
console.log(student.address.city);  // "Karachi"

// Access second semester courses
console.log(student.courses.semester2[0]);  // "Data Structures"

// Using bracket notation
console.log(student["address"]["zip"]);  // "75300"
```

**Modifying Nested Properties:**

```javascript
student.address.city = "Islamabad";
console.log(student.address.city);  // "Islamabad"
```

**Visual Representation of Nesting:**

```
student
  |
  |-- name: "Zainab"
  |-- age: 21
  |-- address (object)
  |     |-- street: "Block 5, Gulshan"
  |     |-- city: "Karachi"
  |     +-- zip: "75300"
  |
  +-- courses (object)
        |-- semester1: ["Intro to CS", "Calculus"]
        +-- semester2: ["Data Structures", "OOP"]
```

---

### 1.9 Object Destructuring (ES6)

Destructuring allows you to **extract properties from an object into individual variables** in a single line. It eliminates the need to write repetitive `object.property` statements.

**Without Destructuring (Old Way):**

```javascript
let product = {
    name: "Laptop",
    price: 85000,
    brand: "Dell"
};

let name = product.name;
let price = product.price;
let brand = product.brand;
```

**With Destructuring (ES6 Way):**

```javascript
let product = {
    name: "Laptop",
    price: 85000,
    brand: "Dell"
};

let { name, price, brand } = product;

console.log(name);   // "Laptop"
console.log(price);  // 85000
console.log(brand);  // "Dell"
```

**Renaming Variables During Destructuring:**

```javascript
let { name: productName, price: cost } = product;

console.log(productName);  // "Laptop"
console.log(cost);         // 85000
```

**Default Values:**

If a property does not exist, you can assign a default:

```javascript
let { name, warranty = "1 year" } = product;

console.log(warranty);  // "1 year" (product has no warranty property)
```

**Destructuring Nested Objects:**

```javascript
let user = {
    name: "Ali",
    address: {
        city: "Lahore",
        zip: "54000"
    }
};

let { name, address: { city, zip } } = user;

console.log(city);  // "Lahore"
console.log(zip);   // "54000"
```

**Destructuring in Function Parameters:**

This is extremely common in real projects:

```javascript
function displayUser({ name, age, city }) {
    console.log(name + " is " + age + " years old from " + city);
}

displayUser({ name: "Fahad", age: 22, city: "Karachi" });
// "Fahad is 22 years old from Karachi"
```

---

### 1.10 Spread Operator with Objects

The spread operator (`...`) copies all properties from one object into another. It is used for **cloning** objects, **merging** objects, and **overriding** specific properties.

**Copying an Object:**

```javascript
let original = { name: "Ali", age: 25 };
let copy = { ...original };

console.log(copy);  // { name: "Ali", age: 25 }

copy.age = 30;
console.log(original.age);  // 25 (original is NOT affected)
```

**Merging Objects:**

```javascript
let personalInfo = { name: "Sara", age: 22 };
let jobInfo = { company: "Google", role: "Engineer" };

let fullProfile = { ...personalInfo, ...jobInfo };

console.log(fullProfile);
// { name: "Sara", age: 22, company: "Google", role: "Engineer" }
```

**Overriding Properties:**

When the same key appears, the last one wins:

```javascript
let defaults = { theme: "light", language: "en", fontSize: 14 };
let userPrefs = { theme: "dark", fontSize: 18 };

let settings = { ...defaults, ...userPrefs };

console.log(settings);
// { theme: "dark", language: "en", fontSize: 18 }
```

**Adding New Properties While Spreading:**

```javascript
let student = { name: "Fahad", age: 22 };
let updatedStudent = { ...student, semester: 6, gpa: 3.8 };

console.log(updatedStudent);
// { name: "Fahad", age: 22, semester: 6, gpa: 3.8 }
```

---

### 1.11 Object.keys(), Object.values(), Object.entries()

These three built-in methods let you extract different parts of an object into arrays, which you can then loop over or process.

```javascript
let phone = {
    brand: "Samsung",
    model: "Galaxy S24",
    price: 250000,
    color: "Black"
};
```

**Object.keys() -- Returns an array of all keys:**

```javascript
let keys = Object.keys(phone);
console.log(keys);
// ["brand", "model", "price", "color"]
```

**Object.values() -- Returns an array of all values:**

```javascript
let values = Object.values(phone);
console.log(values);
// ["Samsung", "Galaxy S24", 250000, "Black"]
```

**Object.entries() -- Returns an array of [key, value] pairs:**

```javascript
let entries = Object.entries(phone);
console.log(entries);
// [
//   ["brand", "Samsung"],
//   ["model", "Galaxy S24"],
//   ["price", 250000],
//   ["color", "Black"]
// ]
```

**Practical Use -- Looping with forEach:**

```javascript
Object.entries(phone).forEach(function([key, value]) {
    console.log(key + ": " + value);
});

// brand: Samsung
// model: Galaxy S24
// price: 250000
// color: Black
```

**Visual Summary:**

```
phone = { brand: "Samsung", model: "Galaxy S24", price: 250000 }

Object.keys(phone)    -->  ["brand", "model", "price"]
Object.values(phone)  -->  ["Samsung", "Galaxy S24", 250000]
Object.entries(phone) -->  [["brand","Samsung"], ["model","Galaxy S24"], ["price",250000]]
```

---

### 1.12 Looping Through Objects with for...in

The `for...in` loop is specifically designed to iterate over the **keys (properties)** of an object.

```javascript
let student = {
    name: "Hamza",
    age: 20,
    department: "Software Engineering",
    gpa: 3.5
};

for (let key in student) {
    console.log(key + ": " + student[key]);
}

// name: Hamza
// age: 20
// department: Software Engineering
// gpa: 3.5
```

**Important:** Inside the loop, you must use **bracket notation** (`student[key]`) because `key` is a variable. Using `student.key` would look for a property literally named `"key"`.

**for...in vs for...of -- Do Not Confuse Them:**

| Loop | Used For | Iterates Over |
|------|----------|---------------|
| `for...in` | Objects | Keys (property names) |
| `for...of` | Arrays, strings, iterables | Values |

```javascript
// for...in with object -- CORRECT
let car = { brand: "Honda", year: 2023 };
for (let key in car) {
    console.log(key);  // "brand", "year"
}

// for...of with array -- CORRECT
let colors = ["red", "green", "blue"];
for (let color of colors) {
    console.log(color);  // "red", "green", "blue"
}
```

---

## 2. JSON (JavaScript Object Notation)

### 2.1 What is JSON?

**JSON (JavaScript Object Notation)** is a lightweight data format used to store and exchange data between a server and a client (browser). It is the standard format for APIs across the web.

**Real-Life Analogy:** Think of JSON as a universal language for computers to share data. Just like English might be the common language between two people who speak different native languages, JSON is the common format between a frontend (React, HTML) and a backend (Node.js, Python, Java).

```
+-----------+         JSON          +-----------+
|           | --------------------> |           |
|  Frontend |   { "name": "Ali" }  |  Backend  |
|  (React)  | <-------------------- |  (Node)   |
|           |         JSON          |           |
+-----------+                       +-----------+
```

**Why JSON?**

- Human-readable (you can open and understand it)
- Language-independent (used by JavaScript, Python, Java, PHP, etc.)
- Lightweight and fast to transmit over the internet
- The standard format for REST APIs

---

### 2.2 JSON Syntax Rules

JSON looks very similar to JavaScript objects, but with strict rules:

| Rule | JavaScript Object | JSON |
|------|-------------------|------|
| Keys | Can be unquoted | Must be in **double quotes** |
| Strings | Single or double quotes | **Double quotes only** |
| Trailing commas | Allowed | **Not allowed** |
| Functions | Allowed as values | **Not allowed** |
| Comments | Allowed (`//`) | **Not allowed** |
| undefined | Allowed as value | **Not allowed** |

**Valid JSON:**

```json
{
    "name": "Fahad Ahmed",
    "age": 22,
    "isStudent": true,
    "courses": ["JavaScript", "React", "Node.js"],
    "address": {
        "city": "Karachi",
        "country": "Pakistan"
    }
}
```

**Invalid JSON (Common Mistakes):**

```
{
    name: "Fahad",          // INVALID: key not in double quotes
    'age': 22,              // INVALID: single quotes on key
    "hobby": 'coding',     // INVALID: single quotes on string value
    "score": undefined,     // INVALID: undefined not allowed
    "greet": function(){},  // INVALID: functions not allowed
}                           // INVALID: trailing comma after last item
```

---

### 2.3 JSON.stringify() -- Object to JSON String

`JSON.stringify()` converts a JavaScript object into a JSON-formatted string. This is necessary when you need to **send data to a server** or **store data in localStorage**.

```javascript
let student = {
    name: "Sara",
    age: 21,
    courses: ["Math", "Physics"]
};

let jsonString = JSON.stringify(student);

console.log(jsonString);
// '{"name":"Sara","age":21,"courses":["Math","Physics"]}'

console.log(typeof jsonString);  // "string"
```

**Pretty Printing (for readability):**

```javascript
let prettyJson = JSON.stringify(student, null, 2);
console.log(prettyJson);
// {
//   "name": "Sara",
//   "age": 21,
//   "courses": [
//     "Math",
//     "Physics"
//   ]
// }
```

The third argument (`2`) adds 2 spaces of indentation for readability.

**Practical Use -- Saving to localStorage:**

```javascript
let settings = { theme: "dark", language: "en" };
localStorage.setItem("userSettings", JSON.stringify(settings));
```

---

### 2.4 JSON.parse() -- JSON String to Object

`JSON.parse()` converts a JSON string back into a JavaScript object. This is necessary when you **receive data from a server** or **read data from localStorage**.

```javascript
let jsonString = '{"name":"Sara","age":21,"courses":["Math","Physics"]}';

let student = JSON.parse(jsonString);

console.log(student.name);      // "Sara"
console.log(student.courses);   // ["Math", "Physics"]
console.log(typeof student);    // "object"
```

**Practical Use -- Reading from localStorage:**

```javascript
let savedSettings = localStorage.getItem("userSettings");
let settings = JSON.parse(savedSettings);

console.log(settings.theme);  // "dark"
```

**Common Error -- Parsing Invalid JSON:**

```javascript
// This will throw a SyntaxError
let bad = JSON.parse("{ name: 'Ali' }");
// Error: keys and strings must use double quotes
```

**The Full Cycle:**

```
JavaScript Object
       |
       | JSON.stringify()
       v
   JSON String  -------> Send to server / Save to localStorage
       |
       | JSON.parse()
       v
JavaScript Object  <----- Receive from server / Read from localStorage
```

---

### 2.5 Real-Life Use Case: APIs and JSON

When your frontend application communicates with a backend API, data travels as JSON.

**Example: Fetching User Data from an API**

```javascript
// The API returns a JSON string like this:
// '{"id": 1, "name": "Fahad", "email": "fahad@example.com"}'

fetch("https://api.example.com/users/1")
    .then(function(response) {
        return response.json();  // parses JSON string into object
    })
    .then(function(user) {
        console.log(user.name);   // "Fahad"
        console.log(user.email);  // "fahad@example.com"
    });
```

In the MERN stack, the Express.js backend sends JSON responses, and the React frontend receives and parses them. You will use this pattern extensively in later weeks.

---

## 3. DOM Manipulation

### 3.1 What is the DOM?

The **DOM (Document Object Model)** is the browser's internal representation of an HTML page. When the browser loads an HTML file, it does not simply display raw text -- it parses the HTML and builds a **tree structure** of objects in memory. This tree is the DOM.

JavaScript can interact with this tree to **read, modify, add, or remove** elements on the page dynamically, without reloading.

**Real-Life Analogy: A Family Tree**

Think of the DOM as a family tree. The `<html>` element is the great-grandparent. It has two children: `<head>` and `<body>`. The `<body>` has its own children (paragraphs, divs, headings), and those can have children too. Every element knows who its parent is, who its siblings are, and who its children are.

```
                        document
                           |
                         <html>
                        /      \
                   <head>      <body>
                    /           /    \
               <title>       <div>   <footer>
                              /  \
                          <h1>   <p>
```

---

### 3.2 DOM Tree Diagram

Consider this HTML page:

```html
<!DOCTYPE html>
<html>
<head>
    <title>My Page</title>
</head>
<body>
    <header>
        <h1 id="main-title">Welcome</h1>
        <nav>
            <ul>
                <li><a href="/">Home</a></li>
                <li><a href="/about">About</a></li>
            </ul>
        </nav>
    </header>
    <main>
        <p class="intro">Hello World</p>
        <button id="btn">Click Me</button>
    </main>
</body>
</html>
```

**The browser builds this DOM tree:**

```
document
  |
  +-- html
       |
       +-- head
       |    |
       |    +-- title
       |         |
       |         +-- "My Page" (text node)
       |
       +-- body
            |
            +-- header
            |    |
            |    +-- h1#main-title
            |    |    |
            |    |    +-- "Welcome" (text node)
            |    |
            |    +-- nav
            |         |
            |         +-- ul
            |              |
            |              +-- li
            |              |    |
            |              |    +-- a [href="/"]
            |              |         |
            |              |         +-- "Home" (text node)
            |              |
            |              +-- li
            |                   |
            |                   +-- a [href="/about"]
            |                        |
            |                        +-- "About" (text node)
            |
            +-- main
                 |
                 +-- p.intro
                 |    |
                 |    +-- "Hello World" (text node)
                 |
                 +-- button#btn
                      |
                      +-- "Click Me" (text node)
```

Every HTML element, attribute, and piece of text becomes a **node** in this tree. JavaScript interacts with these nodes through the DOM API.

---

### 3.3 Selecting Elements

Before you can modify an element, you need to **select** it. The DOM provides several methods for this.

**document.getElementById()**

Selects a single element by its `id` attribute. Returns `null` if no match is found.

```javascript
let title = document.getElementById("main-title");
console.log(title);  // <h1 id="main-title">Welcome</h1>
```

**document.getElementsByClassName()**

Selects all elements with a given class name. Returns an **HTMLCollection** (array-like, but not a real array).

```javascript
let intros = document.getElementsByClassName("intro");
console.log(intros[0]);  // <p class="intro">Hello World</p>
console.log(intros.length);  // 1
```

**document.getElementsByTagName()**

Selects all elements with a given tag name. Also returns an HTMLCollection.

```javascript
let paragraphs = document.getElementsByTagName("p");
console.log(paragraphs.length);  // number of <p> elements
```

**document.querySelector() -- MOST USED**

Selects the **first** element that matches a CSS selector. This is the most flexible and widely used method.

```javascript
let title = document.querySelector("#main-title");       // by ID
let intro = document.querySelector(".intro");             // by class
let firstLink = document.querySelector("a");              // by tag
let navLink = document.querySelector("nav ul li a");      // by nested selector
let btn = document.querySelector("button#btn");           // combined selector
```

**document.querySelectorAll()**

Selects **all** elements that match a CSS selector. Returns a **NodeList** (can use `forEach`).

```javascript
let allLinks = document.querySelectorAll("a");

allLinks.forEach(function(link) {
    console.log(link.href);
});
```

**Comparison Table of All Selectors:**

| Method | Selects | Returns | Live? | forEach? |
|--------|---------|---------|-------|----------|
| `getElementById()` | One element by ID | Element or `null` | N/A | N/A |
| `getElementsByClassName()` | All by class name | HTMLCollection | Yes | No |
| `getElementsByTagName()` | All by tag name | HTMLCollection | Yes | No |
| `querySelector()` | First match (CSS selector) | Element or `null` | No | N/A |
| `querySelectorAll()` | All matches (CSS selector) | NodeList | No | Yes |

**"Live" means** the collection automatically updates when the DOM changes. HTMLCollections are live; NodeLists from `querySelectorAll()` are static snapshots.

**Recommendation:** Use `querySelector()` and `querySelectorAll()` for most cases. They accept any CSS selector, making them the most powerful and flexible options.

---

### 3.4 Modifying Element Content

Once you have selected an element, you can change what it displays.

**textContent**

Gets or sets the plain text content of an element, including text in hidden elements. It does **not** parse HTML.

```javascript
let title = document.querySelector("#main-title");

// Reading
console.log(title.textContent);  // "Welcome"

// Writing
title.textContent = "Hello Students";
```

**innerHTML**

Gets or sets the HTML content of an element. It **does** parse HTML tags.

```javascript
let container = document.querySelector(".intro");

// Reading
console.log(container.innerHTML);  // "Hello World"

// Writing (HTML is parsed and rendered)
container.innerHTML = "<strong>Hello</strong> <em>World</em>";
```

**innerText**

Similar to `textContent`, but only returns **visible** text (respects CSS `display: none`).

```javascript
let element = document.querySelector(".intro");
console.log(element.innerText);  // only visible text
```

**textContent vs innerHTML vs innerText:**

| Property | Parses HTML? | Returns Hidden Text? | Performance | Security |
|----------|-------------|---------------------|-------------|----------|
| `textContent` | No | Yes | Fastest | Safe |
| `innerHTML` | Yes | Yes | Slower | XSS risk if used with user input |
| `innerText` | No | No | Slowest (triggers reflow) | Safe |

**Security Warning:** Never insert user-provided data using `innerHTML`. A malicious user could inject `<script>` tags. Use `textContent` for user-generated content.

```javascript
// DANGEROUS -- never do this with user input
element.innerHTML = userInput;

// SAFE -- use textContent instead
element.textContent = userInput;
```

---

### 3.5 Modifying Styles

**Inline Styles with element.style**

You can directly set CSS properties on an element. Note that CSS property names with hyphens are written in camelCase in JavaScript.

```javascript
let title = document.querySelector("#main-title");

title.style.color = "blue";
title.style.fontSize = "32px";         // CSS: font-size
title.style.backgroundColor = "#f0f0f0";  // CSS: background-color
title.style.padding = "10px";
title.style.textAlign = "center";      // CSS: text-align
```

| CSS Property | JavaScript Equivalent |
|-------------|----------------------|
| `font-size` | `fontSize` |
| `background-color` | `backgroundColor` |
| `text-align` | `textAlign` |
| `margin-top` | `marginTop` |
| `border-radius` | `borderRadius` |

**classList Methods (Preferred Approach)**

Instead of setting styles directly, the best practice is to add or remove CSS classes. This keeps styling in your CSS file and behavior in your JavaScript file.

```css
/* In your CSS file */
.highlight {
    background-color: yellow;
    font-weight: bold;
}

.hidden {
    display: none;
}

.active {
    border: 2px solid blue;
}
```

```javascript
let element = document.querySelector(".intro");

// Add a class
element.classList.add("highlight");

// Remove a class
element.classList.remove("highlight");

// Toggle a class (add if absent, remove if present)
element.classList.toggle("hidden");

// Check if an element has a class
if (element.classList.contains("active")) {
    console.log("Element is active");
}

// Add multiple classes at once
element.classList.add("highlight", "active");
```

**Why classList is Better Than Inline Styles:**

- Keeps CSS separate from JavaScript (separation of concerns)
- Easier to maintain and update styles
- Can use CSS transitions and animations
- One class can set multiple properties at once

---

### 3.6 Modifying Attributes

HTML elements have attributes like `src`, `href`, `alt`, `class`, `id`, `data-*`, etc. JavaScript can read, set, and remove them.

**getAttribute() -- Read an attribute**

```javascript
let link = document.querySelector("a");
let url = link.getAttribute("href");
console.log(url);  // "/"
```

**setAttribute() -- Set or update an attribute**

```javascript
let link = document.querySelector("a");
link.setAttribute("href", "https://google.com");
link.setAttribute("target", "_blank");

let img = document.querySelector("img");
img.setAttribute("src", "new-image.jpg");
img.setAttribute("alt", "A new image");
```

**removeAttribute() -- Remove an attribute entirely**

```javascript
let link = document.querySelector("a");
link.removeAttribute("target");
```

**Practical Example -- Disabling a Button:**

```javascript
let btn = document.querySelector("#btn");

// Disable the button
btn.setAttribute("disabled", "true");

// Enable it again
btn.removeAttribute("disabled");
```

---

### 3.7 Creating and Removing Elements

One of the most powerful features of the DOM is the ability to create new elements and add them to the page dynamically.

**document.createElement() -- Create a new element**

```javascript
let newParagraph = document.createElement("p");
newParagraph.textContent = "This paragraph was created by JavaScript.";
newParagraph.classList.add("intro");
```

At this point, the element exists in memory but is NOT visible on the page. You must attach it to the DOM.

**element.appendChild() -- Add as the last child**

```javascript
let container = document.querySelector("main");
container.appendChild(newParagraph);
// The new <p> now appears at the end of <main>
```

**element.prepend() -- Add as the first child**

```javascript
let notice = document.createElement("div");
notice.textContent = "Important Notice!";
notice.style.color = "red";

document.querySelector("body").prepend(notice);
// The notice appears at the very top of <body>
```

**element.insertBefore() -- Insert before a specific child**

```javascript
let parent = document.querySelector("main");
let existingBtn = document.querySelector("#btn");
let newHeading = document.createElement("h2");
newHeading.textContent = "New Section";

parent.insertBefore(newHeading, existingBtn);
// The <h2> is inserted right before the button
```

**element.remove() -- Remove an element from the DOM**

```javascript
let btn = document.querySelector("#btn");
btn.remove();
// The button is completely removed from the page
```

**Complete Example -- Building a List Dynamically:**

```javascript
// Create a <ul> element
let list = document.createElement("ul");

// Array of items to display
let fruits = ["Apple", "Banana", "Cherry", "Mango"];

// Create an <li> for each fruit and append to the list
fruits.forEach(function(fruit) {
    let li = document.createElement("li");
    li.textContent = fruit;
    list.appendChild(li);
});

// Add the complete list to the page
document.querySelector("main").appendChild(list);
```

**Result in the DOM:**

```html
<ul>
    <li>Apple</li>
    <li>Banana</li>
    <li>Cherry</li>
    <li>Mango</li>
</ul>
```

---

### 3.8 Parent, Child, and Sibling Navigation

Once you have selected one element, you can navigate to related elements using DOM traversal properties.

```
                    +------------------+
                    |   parentElement   |
                    +------------------+
                           |
          +----------------+----------------+
          |                |                |
   +--------------+ +--------------+ +--------------+
   | previousElem | | ** current **| | nextElement  |
   |   Sibling    | |   element    | |   Sibling    |
   +--------------+ +--------------+ +--------------+
                           |
          +----------------+----------------+
          |                                 |
   +----------------+             +----------------+
   | firstElement   |             | lastElement    |
   |    Child       |             |    Child       |
   +----------------+             +----------------+
```

**parentElement -- Get the parent**

```javascript
let btn = document.querySelector("#btn");
let parent = btn.parentElement;
console.log(parent);  // <main>...</main>
```

**children -- Get all child elements**

```javascript
let main = document.querySelector("main");
console.log(main.children);        // HTMLCollection of child elements
console.log(main.children.length); // number of children
```

**firstElementChild / lastElementChild**

```javascript
let main = document.querySelector("main");
console.log(main.firstElementChild);  // <p class="intro">Hello World</p>
console.log(main.lastElementChild);   // <button id="btn">Click Me</button>
```

**nextElementSibling / previousElementSibling**

```javascript
let intro = document.querySelector(".intro");
console.log(intro.nextElementSibling);      // <button id="btn">Click Me</button>

let btn = document.querySelector("#btn");
console.log(btn.previousElementSibling);    // <p class="intro">Hello World</p>
```

**Practical Example -- Navigating a List:**

```javascript
let secondItem = document.querySelector("ul li:nth-child(2)");

console.log(secondItem.textContent);                      // second item
console.log(secondItem.previousElementSibling.textContent); // first item
console.log(secondItem.nextElementSibling.textContent);     // third item
console.log(secondItem.parentElement.tagName);              // "UL"
```

---

## 4. JavaScript Events

### 4.1 What are Events?

Events are **actions or occurrences** that happen in the browser, which JavaScript can detect and respond to. Every time a user clicks a button, types in a textbox, scrolls the page, or submits a form, an event fires.

**Real-Life Analogy: A Doorbell**

Pressing a doorbell is an **event**. The doorbell ringing is the **response** to that event. You do not stand at the door constantly checking -- you set up the doorbell (an event listener) and it notifies you when someone presses it (the event fires).

```
+--------------------+        +--------------------+
|  EVENT (Trigger)   | -----> |  RESPONSE (Action) |
+--------------------+        +--------------------+
|  Button clicked    | -----> |  Show alert        |
|  Form submitted    | -----> |  Validate inputs   |
|  Key pressed       | -----> |  Search results    |
|  Page loaded       | -----> |  Fetch data        |
|  Mouse hovers      | -----> |  Show tooltip      |
+--------------------+        +--------------------+
```

---

### 4.2 Event Listeners: addEventListener()

The modern and recommended way to handle events is with `addEventListener()`. It attaches an event handler to an element without overwriting existing handlers.

**Syntax:**

```javascript
element.addEventListener(eventType, callbackFunction);
```

**Basic Example:**

```javascript
let btn = document.querySelector("#btn");

btn.addEventListener("click", function() {
    alert("Button was clicked!");
});
```

**With a Named Function:**

```javascript
function handleClick() {
    console.log("Button clicked at " + new Date().toLocaleTimeString());
}

let btn = document.querySelector("#btn");
btn.addEventListener("click", handleClick);
```

**Removing an Event Listener:**

You can only remove a listener if you passed a named function (not an anonymous one):

```javascript
btn.removeEventListener("click", handleClick);
```

**Why addEventListener() is Better Than onclick:**

```javascript
// OLD WAY -- onclick property (overwrites previous handlers)
btn.onclick = function() { console.log("First"); };
btn.onclick = function() { console.log("Second"); };
// Only "Second" runs -- the first handler is overwritten

// MODERN WAY -- addEventListener (multiple handlers coexist)
btn.addEventListener("click", function() { console.log("First"); });
btn.addEventListener("click", function() { console.log("Second"); });
// Both "First" and "Second" run
```

---

### 4.3 Common Events Table

| Category | Event | Fires When |
|----------|-------|-----------|
| **Mouse** | `click` | Element is clicked |
| | `dblclick` | Element is double-clicked |
| | `mouseover` | Mouse pointer enters the element |
| | `mouseout` | Mouse pointer leaves the element |
| | `mousedown` | Mouse button is pressed down |
| | `mouseup` | Mouse button is released |
| **Keyboard** | `keydown` | A key is pressed down |
| | `keyup` | A key is released |
| | `keypress` | A key that produces a character is pressed (deprecated) |
| **Form** | `submit` | Form is submitted |
| | `change` | Value of input/select/textarea changes and loses focus |
| | `input` | Value of input changes (fires immediately on each keystroke) |
| | `focus` | Element receives focus (user clicks in or tabs to it) |
| | `blur` | Element loses focus (user clicks away or tabs out) |
| **Window** | `load` | Entire page (including images, scripts) has finished loading |
| | `resize` | Browser window is resized |
| | `scroll` | Page or element is scrolled |

**Examples of Each Category:**

```javascript
// Mouse Event
document.querySelector("#btn").addEventListener("click", function() {
    console.log("Clicked!");
});

// Keyboard Event
document.addEventListener("keydown", function(e) {
    console.log("Key pressed: " + e.key);
});

// Form Event
document.querySelector("#myForm").addEventListener("submit", function(e) {
    e.preventDefault();
    console.log("Form submitted");
});

// Input Event (real-time feedback)
document.querySelector("#search").addEventListener("input", function(e) {
    console.log("Searching for: " + e.target.value);
});

// Window Event
window.addEventListener("resize", function() {
    console.log("Window width: " + window.innerWidth);
});
```

---

### 4.4 The Event Object

When an event fires, the browser automatically creates an **event object** and passes it to the callback function. This object contains detailed information about the event.

```javascript
document.querySelector("#btn").addEventListener("click", function(event) {
    console.log(event);  // the full event object
});
```

**Commonly Used Event Object Properties:**

| Property | Description | Example Value |
|----------|-------------|---------------|
| `event.type` | Type of event | `"click"`, `"keydown"` |
| `event.target` | Element that triggered the event | `<button id="btn">` |
| `event.currentTarget` | Element the listener is attached to | `<div id="container">` |
| `event.key` | Key that was pressed (keyboard events) | `"Enter"`, `"a"` |
| `event.clientX` | Mouse X position relative to viewport | `150` |
| `event.clientY` | Mouse Y position relative to viewport | `200` |
| `event.timeStamp` | Time (ms) when event occurred | `15234.5` |

```javascript
document.addEventListener("keydown", function(event) {
    console.log("Event type: " + event.type);       // "keydown"
    console.log("Key pressed: " + event.key);       // e.g., "Enter"
    console.log("Time: " + event.timeStamp);        // e.g., 15234.5
});

document.addEventListener("click", function(event) {
    console.log("Clicked element: " + event.target.tagName);
    console.log("Mouse position: " + event.clientX + ", " + event.clientY);
});
```

---

### 4.5 event.preventDefault()

Many HTML elements have **default behaviors**. For example:
- A form submits and reloads the page
- A link navigates to a new URL
- A checkbox toggles its state

`event.preventDefault()` stops these default behaviors so you can handle things with JavaScript instead.

**Example 1: Preventing Form Submission (Most Common Use)**

```javascript
let form = document.querySelector("#loginForm");

form.addEventListener("submit", function(event) {
    event.preventDefault();  // stop the page from reloading

    let username = document.querySelector("#username").value;
    let password = document.querySelector("#password").value;

    console.log("Username: " + username);
    console.log("Password: " + password);

    // Now you can validate and send data via fetch() instead
});
```

Without `preventDefault()`, the browser would reload the page immediately on form submission, and your JavaScript code after the submit event would not run as intended.

**Example 2: Preventing Link Navigation**

```javascript
let link = document.querySelector("a");

link.addEventListener("click", function(event) {
    event.preventDefault();  // stop navigation
    console.log("Link click intercepted. URL was: " + this.href);
});
```

---

### 4.6 event.target

`event.target` returns the **exact element** that triggered the event, even if the listener is on a parent element. This is different from `event.currentTarget`, which always refers to the element the listener is attached to.

```javascript
document.querySelector("ul").addEventListener("click", function(event) {
    console.log("Clicked on: " + event.target.tagName);
    // If you clicked on an <li>, event.target is the <li>
    // event.currentTarget is the <ul> (where the listener is)
});
```

**Practical Example -- Identifying Which Button Was Clicked:**

```html
<div id="button-group">
    <button data-action="save">Save</button>
    <button data-action="delete">Delete</button>
    <button data-action="cancel">Cancel</button>
</div>
```

```javascript
document.querySelector("#button-group").addEventListener("click", function(event) {
    if (event.target.tagName === "BUTTON") {
        let action = event.target.getAttribute("data-action");
        console.log("Action: " + action);
    }
});
```

---

### 4.7 Event Bubbling and Capturing

When you click on an element, the event does not just fire on that element. It travels through the DOM tree in two phases:

1. **Capturing Phase (top-down):** The event starts at the `document` and travels down to the target element.
2. **Bubbling Phase (bottom-up):** The event starts at the target element and bubbles up to the `document`.

```
                CAPTURING PHASE              BUBBLING PHASE
                (top to bottom)              (bottom to top)

                  document                     document
                     |                            ^
                     v                            |
                   <html>                       <html>
                     |                            ^
                     v                            |
                   <body>                       <body>
                     |                            ^
                     v                            |
                   <div>                        <div>
                     |                            ^
                     v                            |
                  <button>  <-- EVENT FIRES --> <button>
                  (Target)                     (Target)

   Phase 1: Capture (down)        Phase 2: Bubble (up)
```

**By default**, `addEventListener()` listens during the **bubbling phase**.

**Bubbling Example:**

```html
<div id="outer">
    <div id="inner">
        <button id="btn">Click Me</button>
    </div>
</div>
```

```javascript
document.querySelector("#outer").addEventListener("click", function() {
    console.log("Outer div clicked");
});

document.querySelector("#inner").addEventListener("click", function() {
    console.log("Inner div clicked");
});

document.querySelector("#btn").addEventListener("click", function() {
    console.log("Button clicked");
});

// Clicking the button outputs (bubbling order):
// "Button clicked"
// "Inner div clicked"
// "Outer div clicked"
```

**Listening During Capturing Phase:**

Pass `true` as the third argument to `addEventListener()`:

```javascript
document.querySelector("#outer").addEventListener("click", function() {
    console.log("Outer (capture)");
}, true);  // <-- enables capturing
```

**Stopping Propagation:**

If you want the event to stop traveling up (or down), use `event.stopPropagation()`:

```javascript
document.querySelector("#btn").addEventListener("click", function(event) {
    event.stopPropagation();  // event stops here -- does not bubble up
    console.log("Button clicked");
});

// Now clicking the button only logs "Button clicked"
// The inner and outer div handlers do NOT fire
```

---

### 4.8 Event Delegation

Event delegation is a pattern where you add **a single event listener to a parent element** instead of adding individual listeners to each child. It relies on event bubbling -- when a child is clicked, the event bubbles up to the parent where the listener catches it.

**Why Use Event Delegation?**

1. **Performance:** One listener on the parent instead of hundreds on individual children.
2. **Dynamic Elements:** It works for elements added to the DOM after the listener was set up.
3. **Cleaner Code:** Less code to write and maintain.

**Without Event Delegation (Inefficient):**

```javascript
// Adding a listener to EVERY list item -- bad for large lists
let items = document.querySelectorAll("li");
items.forEach(function(item) {
    item.addEventListener("click", function() {
        console.log("Clicked: " + this.textContent);
    });
});
// Problem: new <li> elements added later will NOT have the listener
```

**With Event Delegation (Efficient):**

```javascript
// ONE listener on the parent <ul>
document.querySelector("ul").addEventListener("click", function(event) {
    if (event.target.tagName === "LI") {
        console.log("Clicked: " + event.target.textContent);
    }
});
// Works for existing AND future <li> elements
```

**Practical Example -- Dynamic Button Handling:**

```html
<div id="toolbar">
    <button class="tool-btn" data-tool="bold">B</button>
    <button class="tool-btn" data-tool="italic">I</button>
    <button class="tool-btn" data-tool="underline">U</button>
</div>
```

```javascript
document.querySelector("#toolbar").addEventListener("click", function(event) {
    let button = event.target.closest(".tool-btn");
    if (button) {
        let tool = button.getAttribute("data-tool");
        console.log("Tool selected: " + tool);
        button.classList.toggle("active");
    }
});
```

The `closest()` method walks up the DOM tree to find the nearest ancestor matching the selector, making delegation more robust when buttons have nested content (like icons inside the button).

---

## 5. Week 12 Project: Interactive To-Do App

Apply everything from this week to build a fully interactive To-Do application using HTML, CSS, and vanilla JavaScript.

### Project Description

Build a single-page To-Do application that lets users add tasks, mark them as complete, and delete them. All data is managed in a JavaScript array and rendered dynamically to the DOM.

### Features

- **Add Tasks:** User types a task into an input field and clicks "Add" (or presses Enter) to add it to the list.
- **Delete Tasks:** Each task has a delete button that removes it from the list.
- **Mark as Complete:** Clicking on a task toggles a "completed" style (e.g., strikethrough text).
- **Store in Array:** All tasks are stored in a JavaScript array of objects. The DOM is re-rendered from this array whenever a change occurs.

### Data Structure

Each task is stored as an object in an array:

```javascript
let tasks = [
    { id: 1, text: "Learn JavaScript Objects", completed: false },
    { id: 2, text: "Practice DOM Manipulation", completed: true },
    { id: 3, text: "Build To-Do App", completed: false }
];
```

### HTML Structure

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>To-Do App</title>
    <style>
        * { margin: 0; padding: 0; box-sizing: border-box; }
        body { font-family: Arial, sans-serif; max-width: 500px; margin: 40px auto; padding: 20px; }
        h1 { text-align: center; margin-bottom: 20px; }
        .input-container { display: flex; gap: 10px; margin-bottom: 20px; }
        .input-container input { flex: 1; padding: 10px; font-size: 16px; border: 1px solid #ccc; border-radius: 4px; }
        .input-container button { padding: 10px 20px; font-size: 16px; background: #4CAF50; color: white; border: none; border-radius: 4px; cursor: pointer; }
        .input-container button:hover { background: #45a049; }
        ul { list-style: none; }
        li { display: flex; justify-content: space-between; align-items: center; padding: 12px; margin-bottom: 8px; background: #f9f9f9; border: 1px solid #ddd; border-radius: 4px; }
        li.completed span { text-decoration: line-through; color: #999; }
        li span { cursor: pointer; flex: 1; }
        li button { background: #e74c3c; color: white; border: none; padding: 6px 12px; border-radius: 4px; cursor: pointer; }
        li button:hover { background: #c0392b; }
    </style>
</head>
<body>
    <h1>To-Do App</h1>
    <div class="input-container">
        <input type="text" id="taskInput" placeholder="Enter a new task...">
        <button id="addBtn">Add</button>
    </div>
    <ul id="taskList"></ul>

    <script src="app.js"></script>
</body>
</html>
```

### JavaScript Logic (app.js)

```javascript
// =============================================
// DATA: Array of task objects
// =============================================
let tasks = [];
let nextId = 1;

// =============================================
// DOM REFERENCES
// =============================================
let taskInput = document.querySelector("#taskInput");
let addBtn = document.querySelector("#addBtn");
let taskList = document.querySelector("#taskList");

// =============================================
// RENDER: Display tasks from array to DOM
// =============================================
function renderTasks() {
    // Clear the current list
    taskList.innerHTML = "";

    // Loop through the tasks array and create DOM elements
    tasks.forEach(function(task) {
        // Create <li> element
        let li = document.createElement("li");
        if (task.completed) {
            li.classList.add("completed");
        }

        // Create <span> for task text (click to toggle complete)
        let span = document.createElement("span");
        span.textContent = task.text;

        // Create delete <button>
        let deleteBtn = document.createElement("button");
        deleteBtn.textContent = "Delete";
        deleteBtn.setAttribute("data-id", task.id);

        // Assemble the <li>
        li.appendChild(span);
        li.appendChild(deleteBtn);
        li.setAttribute("data-id", task.id);

        // Add to the <ul>
        taskList.appendChild(li);
    });
}

// =============================================
// ADD TASK
// =============================================
function addTask() {
    let text = taskInput.value.trim();

    // Do nothing if input is empty
    if (text === "") {
        return;
    }

    // Create a new task object and add to array
    let newTask = {
        id: nextId,
        text: text,
        completed: false
    };

    tasks.push(newTask);
    nextId++;

    // Clear the input field
    taskInput.value = "";
    taskInput.focus();

    // Re-render the list
    renderTasks();
}

// =============================================
// EVENT LISTENERS
// =============================================

// Add task on button click
addBtn.addEventListener("click", addTask);

// Add task on Enter key press
taskInput.addEventListener("keydown", function(event) {
    if (event.key === "Enter") {
        addTask();
    }
});

// Event Delegation: handle clicks on the task list
taskList.addEventListener("click", function(event) {
    let target = event.target;

    // If delete button was clicked
    if (target.tagName === "BUTTON") {
        let id = Number(target.getAttribute("data-id"));
        tasks = tasks.filter(function(task) {
            return task.id !== id;
        });
        renderTasks();
    }

    // If task text (span) was clicked -- toggle completed
    if (target.tagName === "SPAN") {
        let li = target.parentElement;
        let id = Number(li.getAttribute("data-id"));
        tasks.forEach(function(task) {
            if (task.id === id) {
                task.completed = !task.completed;
            }
        });
        renderTasks();
    }
});

// Initial render
renderTasks();
```

### How the Project Uses Week 12 Concepts

| Concept | How It Is Used |
|---------|---------------|
| Objects | Each task is an object with `id`, `text`, `completed` |
| Arrays of Objects | `tasks` array holds all task objects |
| DOM Selection | `querySelector()` selects input, button, and list |
| DOM Creation | `createElement()` builds `<li>`, `<span>`, `<button>` |
| DOM Modification | `textContent`, `classList`, `setAttribute()` |
| Events | `click`, `keydown` events with `addEventListener()` |
| Event Delegation | Single listener on `<ul>` handles all child clicks |
| event.target | Identifies whether a `<span>` or `<button>` was clicked |
| Object Properties | Reading `task.id`, `task.text`, `task.completed` |

---

## 6. Summary -- JavaScript Weeks 9-12 Recap

Over the last four weeks, you have built a solid foundation in JavaScript. Here is a visual map of everything covered:

```
+================================================================+
|                  JAVASCRIPT FUNDAMENTALS                       |
|                     Weeks 9 - 12                               |
+================================================================+

WEEK 9: JavaScript Fundamentals
+---------------------------------------------------------------+
|  - What is JavaScript and how it runs in the browser          |
|  - Variables: var, let, const                                 |
|  - Data Types: string, number, boolean, null, undefined       |
|  - Operators: arithmetic, comparison, logical, assignment     |
|  - Type Conversion and Coercion                               |
|  - Template Literals (backtick strings)                       |
+---------------------------------------------------------------+

WEEK 10: Control Flow & Loops
+---------------------------------------------------------------+
|  - Conditional Statements: if, else if, else                  |
|  - Switch Statement                                           |
|  - Ternary Operator                                           |
|  - Loops: for, while, do...while                              |
|  - Loop Control: break, continue                              |
|  - Nested Loops                                               |
+---------------------------------------------------------------+

WEEK 11: Functions & Arrays
+---------------------------------------------------------------+
|  - Function Declaration and Expression                        |
|  - Parameters, Arguments, Return Values                       |
|  - Arrow Functions (ES6)                                      |
|  - Scope: Global, Local, Block                                |
|  - Arrays: Creating, Accessing, Modifying                     |
|  - Array Methods: push, pop, shift, unshift, splice, slice    |
|  - Iteration: forEach, map, filter, find, reduce              |
+---------------------------------------------------------------+

WEEK 12: Objects, DOM & Events  <-- YOU ARE HERE
+---------------------------------------------------------------+
|  - Objects: Properties, Methods, this keyword                 |
|  - Nested Objects, Destructuring, Spread Operator             |
|  - Object.keys(), Object.values(), Object.entries()           |
|  - JSON: stringify, parse, API data exchange                  |
|  - DOM: Selecting, Modifying, Creating, Removing elements     |
|  - DOM Traversal: parent, children, siblings                  |
|  - Events: addEventListener, Event Object                     |
|  - Event Bubbling, Capturing, Delegation                      |
|  - Project: Interactive To-Do App                             |
+---------------------------------------------------------------+

                            |
                            v
                   COMING UP NEXT...
+---------------------------------------------------------------+
|  Week 13: Git & GitHub                                        |
|  Version control, repositories, branching, collaboration      |
+---------------------------------------------------------------+
```

### Key Takeaways from Week 12

1. **Objects** are the building blocks of JavaScript. Almost everything in JS is an object, including DOM elements, arrays, and even functions.
2. **JSON** is the universal language of web data exchange. Every API you work with in the MERN stack will use JSON.
3. **The DOM** bridges HTML and JavaScript. Without it, JavaScript cannot interact with the webpage.
4. **Events** make websites interactive. Without event listeners, a webpage is just a static document.
5. **Event delegation** is a professional pattern you will use in every real project, including React (which uses a similar mechanism internally).

### What to Practice

- Create objects that represent real-world entities (students, products, orders).
- Convert objects to JSON and back. Practice with `localStorage`.
- Build small interactive pages: a counter, a color changer, a dynamic list.
- Use event delegation to handle clicks on dynamically generated content.
- Complete the To-Do App project and experiment with adding new features (edit tasks, filter by status, persist to localStorage).

---

*End of Week 12 Notes. Next week: Git and GitHub -- version control and collaboration.*
