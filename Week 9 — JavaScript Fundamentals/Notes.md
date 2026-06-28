# Week 9: JavaScript Fundamentals

> **Course:** MERN Stack Web Development  
> **Prerequisites:** Weeks 1-4 (HTML), Weeks 5-8 (CSS)  
> **Objective:** Understand what JavaScript is, set up your development environment, learn variables, data types, operators, type conversion, debugging basics, and essential string and number methods.

---

## Table of Contents

1. [What is JavaScript?](#1-what-is-javascript)
2. [Setting Up](#2-setting-up)
3. [Variables](#3-variables)
4. [Data Types](#4-data-types)
5. [Operators](#5-operators)
6. [Type Conversion and Coercion](#6-type-conversion-and-coercion)
7. [console.log() and Debugging Basics](#7-consolelog-and-debugging-basics)
8. [String Methods](#8-string-methods)
9. [Number Methods](#9-number-methods)
10. [Summary](#10-summary)

---

## 1. What is JavaScript?

**JavaScript** (often abbreviated as **JS**) is a high-level, interpreted programming language that makes websites interactive and dynamic. Up until now, you have learned HTML (the structure of a web page) and CSS (the appearance of a web page). JavaScript is the third and final pillar of front-end web development -- it adds **behavior** and **interactivity** to your pages.

```
    THE THREE PILLARS OF THE WEB
    ============================

    ┌──────────────────────────────────────────────┐
    │                  WEBSITE                     │
    │                                              │
    │   ┌──────────┐  ┌──────────┐  ┌──────────┐  │
    │   │   HTML   │  │   CSS    │  │    JS    │  │
    │   │          │  │          │  │          │  │
    │   │Structure │  │  Style   │  │ Behavior │  │
    │   │  (Bones) │  │  (Skin)  │  │(Muscles) │  │
    │   └──────────┘  └──────────┘  └──────────┘  │
    │                                              │
    │   "What is     "How does     "What does     │
    │    on the       it look?"     it do?"        │
    │    page?"                                    │
    └──────────────────────────────────────────────┘
```

**Real-Life Example:** Think of a car. HTML is the body, frame, and seats -- the physical structure. CSS is the paint color, leather interior, and chrome finish -- the visual appearance. JavaScript is the engine, steering wheel, and brakes -- the parts that make it actually *do* things when you interact with it.

Without JavaScript, clicking a button on a website would do absolutely nothing. There would be no dropdown menus, no form validation, no animations triggered by user actions, and no way to load new content without refreshing the entire page.

---

### 1.1 History of JavaScript

JavaScript was created by **Brendan Eich** in **1995** while he was working at **Netscape Communications**. Here is the remarkable part: he built the first version of the language in just **10 days**.

```
    TIMELINE OF JAVASCRIPT
    ======================

    1995  ──▶  Brendan Eich creates "Mocha" at Netscape (in 10 days!)
              Renamed to "LiveScript", then to "JavaScript"

    1997  ──▶  ECMAScript 1 (ES1) — the first official standard

    2009  ──▶  Node.js released — JavaScript can now run on servers!

    2015  ──▶  ECMAScript 6 (ES6) — massive update with modern features
              (let, const, arrow functions, template literals, classes)

    2020+ ──▶  JavaScript is the most popular programming language
              in the world (Stack Overflow Developer Survey)
```

> **Fun Fact:** The name "JavaScript" was a marketing decision. Java was extremely popular in 1995, so Netscape named their new language "JavaScript" to ride the wave of Java's popularity. The two languages are fundamentally different.

---

### 1.2 Why JavaScript?

JavaScript holds a unique position in the programming world. It is the **only language that runs natively in every web browser** -- Chrome, Firefox, Safari, Edge, and all others. No other programming language can make this claim.

| Feature | JavaScript | Other Languages |
|---------|-----------|-----------------|
| Runs in the browser | Yes (natively) | No (requires plugins or compilation) |
| Runs on the server | Yes (with Node.js) | Yes |
| Runs on mobile | Yes (React Native) | Yes |
| Required for web development | Yes | No |
| Beginner-friendly syntax | Yes | Varies |

**Real-Life Example:** Think of JavaScript like English in international business. Many languages exist, but English is the one language that is understood almost everywhere. Similarly, JavaScript is the one language that every web browser understands without any additional setup.

---

### 1.3 JavaScript vs Java

This is one of the most common confusions for beginners. **JavaScript and Java are completely different languages.** They share a name for historical marketing reasons, but they differ in nearly every way.

```
    JAVASCRIPT vs JAVA — THEY ARE NOT THE SAME!
    =============================================

    ┌────────────────────────┐    ┌────────────────────────┐
    │      JavaScript        │    │         Java           │
    ├────────────────────────┤    ├────────────────────────┤
    │ Created: 1995          │    │ Created: 1995          │
    │ By: Brendan Eich       │    │ By: James Gosling      │
    │ At: Netscape           │    │ At: Sun Microsystems   │
    │ Type: Interpreted      │    │ Type: Compiled         │
    │ Typing: Dynamic        │    │ Typing: Static         │
    │ Runs in: Browser +     │    │ Runs in: JVM           │
    │          Node.js       │    │ (Java Virtual Machine)  │
    │ Used for: Web, Apps    │    │ Used for: Enterprise,  │
    │                        │    │ Android, Backend       │
    └────────────────────────┘    └────────────────────────┘
```

> **Analogy:** JavaScript is to Java as **car** is to **carpet**. They share the first three letters, but they are entirely different things.

---

### 1.4 What Can JavaScript Do?

JavaScript is one of the most versatile programming languages in existence. Here is what you can build with it:

| What You Can Build | Technology | Example |
|-------------------|------------|---------|
| Interactive Websites | Vanilla JS, React, Vue, Angular | Gmail, Facebook, Twitter |
| Server-Side Applications | Node.js, Express.js | API servers, real-time chat apps |
| Mobile Applications | React Native, Ionic | Instagram, Uber Eats |
| Desktop Applications | Electron.js | VS Code, Slack, Discord |
| Games | Phaser.js, Three.js | Browser-based 2D and 3D games |
| Machine Learning / AI | TensorFlow.js | Image recognition in the browser |
| Command-Line Tools | Node.js | npm, webpack, eslint |

**Real-Life Example:** The very tool you are using to write code -- **Visual Studio Code** -- is built entirely with JavaScript (using a framework called Electron). That is how powerful this language is.

---

## 2. Setting Up

Before you can write JavaScript, you need to know **where** and **how** to run it. There are four common ways to run JavaScript code.

---

### 2.1 Running JavaScript in the Browser Console

Every modern browser has a built-in JavaScript engine. You can write and run JavaScript code directly in the browser's **Developer Tools Console**.

**Steps:**
1. Open your browser (Chrome is recommended).
2. Press `F12` or `Ctrl + Shift + J` (Windows) / `Cmd + Option + J` (Mac).
3. Click on the **Console** tab.
4. Type your JavaScript code and press `Enter`.

```javascript
// Try this in your browser console:
console.log("Hello, World!");
// Output: Hello, World!

2 + 3
// Output: 5

"JavaScript" + " is " + "awesome!"
// Output: JavaScript is awesome!
```

```
    BROWSER DEVELOPER TOOLS
    =======================

    ┌──────────────────────────────────────────────┐
    │  Chrome Browser                         - X  │
    ├──────────────────────────────────────────────┤
    │                                              │
    │   Your Website Content Here                  │
    │                                              │
    ├──────────────────────────────────────────────┤
    │  Elements | Console | Sources | Network      │
    ├──────────────────────────────────────────────┤
    │  > console.log("Hello!");                    │
    │    Hello!                                    │
    │  > 10 * 5                                    │
    │    50                                        │
    │  > _                                         │
    └──────────────────────────────────────────────┘
```

> **Note:** The browser console is great for quick experiments, but you should not write entire programs here. It is a testing tool, not a development environment.

---

### 2.2 Running JavaScript with a Script Tag in HTML

You can write JavaScript directly inside an HTML file using the `<script>` tag.

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>My First JavaScript</title>
</head>
<body>
    <h1>JavaScript in HTML</h1>

    <script>
        // This JavaScript runs when the browser reaches this point
        console.log("Hello from inside the HTML file!");
        alert("Welcome to JavaScript!");
    </script>
</body>
</html>
```

> **Important:** Always place your `<script>` tag just before the closing `</body>` tag. This ensures that all HTML elements are loaded before JavaScript tries to interact with them.

---

### 2.3 External JavaScript File Linked to HTML

For real projects, you should always keep your JavaScript in a **separate file** with the `.js` extension. This follows the principle of **separation of concerns** -- HTML handles structure, CSS handles style, and JavaScript handles behavior.

**index.html:**
```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>External JavaScript</title>
    <link rel="stylesheet" href="style.css">
</head>
<body>
    <h1>Hello World</h1>

    <!-- Link your external JavaScript file -->
    <script src="script.js"></script>
</body>
</html>
```

**script.js:**
```javascript
console.log("Hello from an external JavaScript file!");
alert("This code lives in script.js");
```

```
    PROJECT FILE STRUCTURE
    ======================

    my-project/
    ├── index.html      ← Structure (HTML)
    ├── style.css       ← Appearance (CSS)
    └── script.js       ← Behavior (JavaScript)

    ┌─────────────┐
    │ index.html  │──── links to ────▶ style.css
    │             │──── links to ────▶ script.js
    └─────────────┘
```

**Why use external files?**
- Code is cleaner and more organized.
- Multiple HTML pages can share the same JavaScript file.
- The browser can cache the JavaScript file, making your site faster.
- Teams can work on HTML and JavaScript separately.

---

### 2.4 Using VS Code with Live Server

**Live Server** is a VS Code extension that automatically refreshes your browser whenever you save a file. This is extremely helpful during development.

**Steps to set up:**
1. Open **VS Code**.
2. Go to the **Extensions** panel (Ctrl + Shift + X).
3. Search for **"Live Server"** by Ritwick Dey.
4. Click **Install**.
5. Open your project folder in VS Code.
6. Right-click on `index.html` and select **"Open with Live Server"**.
7. Your browser will open and automatically refresh whenever you save changes.

> **Tip:** You can also click the **"Go Live"** button in the bottom-right corner of the VS Code status bar.

---

## 3. Variables

### 3.1 What is a Variable?

A **variable** is a named container that stores a value in your program's memory. You can think of it as a **labeled box** -- the label is the variable's name, and the content inside the box is the variable's value.

**Real-Life Example:** Imagine you are moving to a new house. You have several cardboard boxes, and you write a label on each one:

- A box labeled **"Kitchen Stuff"** contains plates, cups, and spoons.
- A box labeled **"Books"** contains your novels and textbooks.
- A box labeled **"Clothes"** contains your shirts and pants.

In programming, variables work the same way. You give each "box" a name, and you store a value inside it.

```
    VARIABLE = A LABELED BOX
    ========================

    ┌─────────────────────┐    ┌─────────────────────┐
    │     name: "age"     │    │   name: "userName"   │
    │  ┌───────────────┐  │    │  ┌───────────────┐  │
    │  │               │  │    │  │               │  │
    │  │      25       │  │    │  │   "Fahad"     │  │
    │  │               │  │    │  │               │  │
    │  └───────────────┘  │    │  └───────────────┘  │
    │     value: 25       │    │   value: "Fahad"    │
    └─────────────────────┘    └─────────────────────┘

    In code:
    let age = 25;
    let userName = "Fahad";
```

---

### 3.2 var, let, and const

JavaScript provides three keywords for declaring variables: `var`, `let`, and `const`. Each behaves differently.

#### var (The Old Way)

`var` was the original way to declare variables in JavaScript. It has been available since the language was first created in 1995. However, it has some problematic behaviors, and **modern JavaScript avoids using `var`**.

```javascript
var greeting = "Hello";
console.log(greeting); // Output: Hello

var greeting = "Hi";   // No error! var allows re-declaration
console.log(greeting); // Output: Hi
```

> **Problem with var:** It allows you to accidentally re-declare the same variable, which can introduce bugs in large programs.

#### let (The Modern Way for Changeable Values)

`let` was introduced in **ES6 (2015)**. Use `let` when you need a variable whose value **will change** later.

```javascript
let score = 0;
console.log(score); // Output: 0

score = 10;         // Updating the value is allowed
console.log(score); // Output: 10

// let score = 20;  // ERROR! Cannot re-declare with let
```

**Real-Life Example:** Your age is a `let` variable. It changes every year, but you only have one age at a time.

#### const (The Modern Way for Fixed Values)

`const` was also introduced in **ES6 (2015)**. Use `const` when you need a variable whose value **should never change** after being set.

```javascript
const PI = 3.14159;
console.log(PI); // Output: 3.14159

// PI = 3.14;     // ERROR! Cannot reassign a const variable
// const PI = 3;  // ERROR! Cannot re-declare a const variable
```

**Real-Life Example:** Your date of birth is a `const` variable. It was set once and will never change.

#### When to Use Each

| Keyword | Can Reassign? | Can Re-declare? | Scope | When to Use |
|---------|:------------:|:--------------:|-------|-------------|
| `var` | Yes | Yes | Function | Avoid using `var` in modern code |
| `let` | Yes | No | Block | When the value will change |
| `const` | No | No | Block | When the value should stay the same |

> **Best Practice:** Always start with `const`. Only switch to `let` if you realize you need to change the value later. Never use `var` in new code.

```
    DECISION FLOWCHART: WHICH KEYWORD TO USE?
    ==========================================

    Will this value change later?
            │
            ├── YES ──▶ Use "let"
            │
            └── NO  ──▶ Use "const"

    (Never use "var" in modern JavaScript)
```

---

### 3.3 Variable Naming Rules and Conventions

JavaScript has strict rules about what you can and cannot name a variable.

#### Rules (Must Follow -- Otherwise You Get an Error)

| Rule | Valid Example | Invalid Example |
|------|:------------:|:--------------:|
| Must start with a letter, `_`, or `$` | `name`, `_count`, `$price` | `1name`, `-count` |
| Cannot contain spaces | `firstName` | `first name` |
| Cannot use reserved keywords | `myClass` | `class`, `return`, `let` |
| Case-sensitive | `Age` and `age` are different | -- |

#### Conventions (Should Follow -- Makes Code Readable)

| Convention | Example | Used For |
|-----------|---------|----------|
| **camelCase** | `firstName`, `totalPrice`, `isLoggedIn` | Variables and functions |
| **PascalCase** | `UserProfile`, `ShoppingCart` | Classes and constructors |
| **UPPER_SNAKE_CASE** | `MAX_SIZE`, `API_KEY` | Constants that never change |

```javascript
// Good variable names (descriptive and camelCase)
let firstName = "Ali";
let totalPrice = 299.99;
let isLoggedIn = true;
const MAX_RETRIES = 3;

// Bad variable names (avoid these)
let x = "Ali";        // Too vague — what is "x"?
let fn = "Ali";        // Unclear abbreviation
let data = "Ali";      // Too generic
let myvar = "Ali";     // Not camelCase
```

> **Tip:** Always choose variable names that describe what the variable contains. Your code should read like a story. Someone looking at your code six months later (including yourself) should understand what each variable represents.

---

### 3.4 Variable as a Labeled Container (Diagram)

```
    HOW VARIABLES WORK IN MEMORY
    ============================

    Your Code:                    Computer Memory:
    ──────────                    ────────────────

    let city = "Karachi";        ┌──────────────────┐
                          ──────▶│  city: "Karachi"  │  Address: 0x001
                                 └──────────────────┘

    let population = 16000000;   ┌──────────────────────┐
                          ──────▶│  population: 16000000│  Address: 0x002
                                 └──────────────────────┘

    const country = "Pakistan";  ┌────────────────────────┐
                          ──────▶│  country: "Pakistan"   │  Address: 0x003
                                 │  (locked — cannot      │
                                 │   be changed)          │
                                 └────────────────────────┘

    When you write:
        city = "Lahore";

    The memory updates:
                                 ┌──────────────────┐
                                 │  city: "Lahore"   │  Address: 0x001
                                 └──────────────────┘
                                      (value changed)
```

---

## 4. Data Types

Every value in JavaScript has a **type**. The type determines what kind of data the value represents and what operations you can perform on it. JavaScript has two categories of data types: **Primitive Types** and **Reference Types** (objects, arrays -- covered in later weeks).

---

### 4.1 Primitive Types

Primitive types are the most basic data types. They represent a single, simple value.

---

#### String

A **String** is a sequence of characters (letters, numbers, symbols) enclosed in quotes. Strings represent text.

There are three ways to create a string in JavaScript:

```javascript
// 1. Single Quotes
let greeting = 'Hello, World!';

// 2. Double Quotes
let message = "Welcome to JavaScript";

// 3. Template Literals (Backticks) — introduced in ES6
let name = "Fahad";
let welcomeMessage = `Hello, ${name}! Welcome aboard.`;
console.log(welcomeMessage);
// Output: Hello, Fahad! Welcome aboard.
```

**Real-Life Example:** A string is like a necklace of beads. Each bead is a character, and the thread holding them together is the string itself. The quotes are like the clasp that holds the necklace at both ends.

```
    STRING: "Hello"
    ===============

    Index:    0     1     2     3     4
            ┌─────┬─────┬─────┬─────┬─────┐
            │  H  │  e  │  l  │  l  │  o  │
            └─────┴─────┴─────┴─────┴─────┘

    "Hello".length = 5
    "Hello"[0]     = "H"
    "Hello"[4]     = "o"
```

> **Note on Template Literals:** Backtick strings (`` ` ``) are special because they allow you to embed variables and expressions inside `${ }`. This is called **string interpolation** and is much cleaner than using the `+` operator to join strings together.

```javascript
// Without template literals (old way)
let age = 25;
let oldWay = "I am " + age + " years old.";
console.log(oldWay); // Output: I am 25 years old.

// With template literals (modern way)
let newWay = `I am ${age} years old.`;
console.log(newWay); // Output: I am 25 years old.

// Template literals can contain expressions
let price = 100;
let tax = 0.17;
console.log(`Total: Rs. ${price + price * tax}`);
// Output: Total: Rs. 117
```

---

#### Number

A **Number** represents numeric values. Unlike many other programming languages, JavaScript does **not** have separate types for integers and decimals -- they are all just "numbers."

```javascript
let age = 25;           // Integer (whole number)
let price = 99.99;      // Decimal (floating-point number)
let negative = -10;     // Negative number
let billion = 1e9;      // Scientific notation (1,000,000,000)

console.log(typeof age);    // Output: "number"
console.log(typeof price);  // Output: "number"
```

**Special Number Values:**

```javascript
console.log(1 / 0);          // Output: Infinity
console.log(-1 / 0);         // Output: -Infinity
console.log("hello" * 2);    // Output: NaN (Not a Number)

// NaN is a special value that results from invalid math operations
console.log(typeof NaN);     // Output: "number" (yes, NaN is technically a number!)
```

**Real-Life Example:** Think of numbers like a ruler. A ruler does not care whether you are measuring 5 centimeters or 5.7 centimeters -- it handles both. JavaScript's Number type works the same way.

---

#### Boolean

A **Boolean** represents a logical value: either `true` or `false`. Booleans are the foundation of decision-making in programming.

```javascript
let isLoggedIn = true;
let hasPermission = false;
let isAdult = (age >= 18);  // true if age is 18 or more

console.log(isLoggedIn);     // Output: true
console.log(typeof isAdult); // Output: "boolean"
```

**Real-Life Example:** A light switch is a Boolean. It is either **ON** (true) or **OFF** (false). There is no third option. Every yes/no question in real life is essentially a Boolean: "Is the door open?" -- true or false. "Is the student present?" -- true or false.

```
    BOOLEAN VALUES
    ==============

    ┌───────────┐         ┌───────────┐
    │   true    │         │   false   │
    │           │         │           │
    │   ON      │         │   OFF     │
    │   YES     │         │   NO      │
    │   1       │         │   0       │
    └───────────┘         └───────────┘
```

---

#### undefined

A variable that has been **declared but not assigned a value** automatically holds the value `undefined`.

```javascript
let score;
console.log(score);        // Output: undefined
console.log(typeof score); // Output: "undefined"
```

**Real-Life Example:** You buy a new notebook and write a label on the cover: "Meeting Notes." But you have not written anything inside yet. The notebook exists (it is declared), but its pages are blank (its value is undefined).

---

#### null

`null` is a value that represents **intentional emptiness**. It is used when you deliberately want to indicate that a variable has no value.

```javascript
let selectedProduct = null; // No product selected yet
console.log(selectedProduct);        // Output: null
console.log(typeof selectedProduct); // Output: "object" (this is a known bug in JS!)
```

**Real-Life Example:** Imagine a parking spot with a sign that says "Reserved." The spot is intentionally left empty for a specific car. That is `null` -- a deliberate, purposeful absence of a value.

---

#### undefined vs null

```
    undefined vs null
    =================

    undefined                          null
    ─────────                          ────
    "I forgot to put                   "I intentionally
     something here"                    left this empty"

    ┌─────────────────┐               ┌─────────────────┐
    │  let x;         │               │  let x = null;  │
    │                 │               │                 │
    │  ┌───────────┐  │               │  ┌───────────┐  │
    │  │           │  │               │  │  (empty)  │  │
    │  │    ???    │  │               │  │   null    │  │
    │  │           │  │               │  │           │  │
    │  └───────────┘  │               │  └───────────┘  │
    │  "value was     │               │  "value was     │
    │   never set"    │               │   set to empty" │
    └─────────────────┘               └─────────────────┘
```

---

#### BigInt (Brief Mention)

**BigInt** is a special numeric type that can represent integers of arbitrary length. Regular numbers in JavaScript cannot safely represent integers larger than 2^53 - 1 (approximately 9 quadrillion).

```javascript
let bigNumber = 123456789012345678901234567890n; // Note the "n" at the end
console.log(typeof bigNumber); // Output: "bigint"
```

> **Note:** You will rarely need BigInt in typical web development. It is mainly used for cryptography, scientific computing, or working with extremely large numbers.

---

#### Symbol (Brief Mention)

A **Symbol** is a unique and immutable value, often used as a unique identifier for object properties.

```javascript
let id = Symbol("userID");
console.log(typeof id); // Output: "symbol"
```

> **Note:** Symbols are an advanced topic. You do not need to worry about them right now. They are mentioned here for completeness.

---

### 4.2 The typeof Operator

The `typeof` operator returns a string indicating the type of a value. It is extremely useful for debugging.

```javascript
console.log(typeof "Hello");     // Output: "string"
console.log(typeof 42);          // Output: "number"
console.log(typeof true);        // Output: "boolean"
console.log(typeof undefined);   // Output: "undefined"
console.log(typeof null);        // Output: "object"   (historical bug)
console.log(typeof 10n);         // Output: "bigint"
console.log(typeof Symbol());    // Output: "symbol"
console.log(typeof {});          // Output: "object"
console.log(typeof []);          // Output: "object"   (arrays are objects)
console.log(typeof function(){}); // Output: "function"
```

---

### 4.3 Comparison Table of All Data Types

| Data Type | Example | typeof Result | Description |
|-----------|---------|:------------:|-------------|
| **String** | `"Hello"`, `'World'`, `` `Hi` `` | `"string"` | Text data |
| **Number** | `42`, `3.14`, `-7`, `NaN`, `Infinity` | `"number"` | Numeric data (integers and decimals) |
| **Boolean** | `true`, `false` | `"boolean"` | Logical true or false |
| **undefined** | `undefined` | `"undefined"` | Variable declared but not assigned |
| **null** | `null` | `"object"` | Intentionally empty (typeof is a bug) |
| **BigInt** | `123n` | `"bigint"` | Arbitrarily large integers |
| **Symbol** | `Symbol("id")` | `"symbol"` | Unique identifiers |

---

## 5. Operators

An **operator** is a symbol that tells JavaScript to perform a specific operation on one or more values. Think of operators as verbs in a sentence -- they describe the action being performed.

---

### 5.1 Arithmetic Operators

Arithmetic operators perform mathematical calculations.

| Operator | Name | Example | Result |
|:--------:|------|---------|:------:|
| `+` | Addition | `10 + 5` | `15` |
| `-` | Subtraction | `10 - 5` | `5` |
| `*` | Multiplication | `10 * 5` | `50` |
| `/` | Division | `10 / 3` | `3.333...` |
| `%` | Modulus (Remainder) | `10 % 3` | `1` |
| `**` | Exponentiation (Power) | `2 ** 3` | `8` |

```javascript
let a = 10;
let b = 3;

console.log(a + b);   // Output: 13
console.log(a - b);   // Output: 7
console.log(a * b);   // Output: 30
console.log(a / b);   // Output: 3.3333333333333335
console.log(a % b);   // Output: 1  (10 divided by 3 = remainder 1)
console.log(a ** b);  // Output: 1000  (10 to the power of 3)
```

**Real-Life Example of Modulus (%):**
The modulus operator returns the **remainder** after division. It is useful for determining if a number is even or odd:

```javascript
console.log(10 % 2);  // Output: 0  (even — no remainder)
console.log(7 % 2);   // Output: 1  (odd — remainder is 1)
console.log(15 % 4);  // Output: 3  (15 / 4 = 3 remainder 3)
```

**Real-Life Example:** Think of modulus like sharing items equally. If you have 10 cookies and 3 friends, each friend gets 3 cookies (`10 / 3 = 3`), and you have 1 cookie left over (`10 % 3 = 1`).

---

### 5.2 Assignment Operators

Assignment operators store values in variables. The basic assignment operator is `=`, but there are shorthand versions that combine assignment with arithmetic.

| Operator | Example | Equivalent To | Description |
|:--------:|---------|:------------:|-------------|
| `=` | `x = 10` | -- | Assigns value |
| `+=` | `x += 5` | `x = x + 5` | Add and assign |
| `-=` | `x -= 5` | `x = x - 5` | Subtract and assign |
| `*=` | `x *= 5` | `x = x * 5` | Multiply and assign |
| `/=` | `x /= 5` | `x = x / 5` | Divide and assign |
| `%=` | `x %= 5` | `x = x % 5` | Modulus and assign |

```javascript
let score = 100;

score += 10;  // score = 100 + 10 = 110
console.log(score); // Output: 110

score -= 20;  // score = 110 - 20 = 90
console.log(score); // Output: 90

score *= 2;   // score = 90 * 2 = 180
console.log(score); // Output: 180

score /= 3;   // score = 180 / 3 = 60
console.log(score); // Output: 60

score %= 7;   // score = 60 % 7 = 4 (remainder)
console.log(score); // Output: 4
```

---

### 5.3 Comparison Operators

Comparison operators compare two values and return a **Boolean** (`true` or `false`).

| Operator | Name | Example | Result |
|:--------:|------|---------|:------:|
| `==` | Equal to (loose) | `5 == "5"` | `true` |
| `===` | Equal to (strict) | `5 === "5"` | `false` |
| `!=` | Not equal (loose) | `5 != "5"` | `false` |
| `!==` | Not equal (strict) | `5 !== "5"` | `true` |
| `>` | Greater than | `10 > 5` | `true` |
| `<` | Less than | `10 < 5` | `false` |
| `>=` | Greater than or equal | `5 >= 5` | `true` |
| `<=` | Less than or equal | `4 <= 5` | `true` |

```javascript
let x = 10;
let y = 20;

console.log(x > y);   // Output: false
console.log(x < y);   // Output: true
console.log(x >= 10); // Output: true
console.log(x <= 9);  // Output: false
```

---

### 5.4 == vs === (The Most Important Distinction)

This is one of the most critical concepts in JavaScript. Understanding the difference between `==` and `===` will save you from countless bugs.

- `==` (Loose Equality): Compares values **after converting them to the same type** (type coercion).
- `===` (Strict Equality): Compares values **without any type conversion**. Both the value AND the type must match.

```javascript
// Loose equality (==) — performs type coercion
console.log(5 == "5");     // Output: true   (string "5" is converted to number 5)
console.log(0 == false);   // Output: true   (false is converted to 0)
console.log(null == undefined); // Output: true
console.log("" == 0);     // Output: true   (empty string converts to 0)

// Strict equality (===) — no type coercion
console.log(5 === "5");    // Output: false  (number vs string — different types!)
console.log(0 === false);  // Output: false  (number vs boolean — different types!)
console.log(null === undefined); // Output: false
console.log("" === 0);    // Output: false  (string vs number — different types!)
```

```
    == vs === EXPLAINED
    ===================

    == (Loose Equality)                === (Strict Equality)
    ───────────────────                ────────────────────

    Step 1: Convert types              Step 1: Check types
    Step 2: Compare values             - If types differ → FALSE
                                       Step 2: Compare values

    5 == "5"                           5 === "5"
    ┌─────┐    ┌─────┐                ┌─────┐    ┌─────┐
    │  5  │ == │ "5" │                │  5  │===│ "5" │
    │(num)│    │(str)│                │(num)│   │(str)│
    └──┬──┘    └──┬──┘                └─────┘    └─────┘
       │          │                      │          │
       │   Convert "5" to 5             num !== str
       │          │                      │
       ▼          ▼                      ▼
    ┌─────┐    ┌─────┐                FALSE
    │  5  │ == │  5  │                (types are different,
    └─────┘    └─────┘                 so stop immediately)
         │
         ▼
       TRUE
```

> **Best Practice:** Always use `===` (strict equality) and `!==` (strict inequality). Only use `==` if you have a specific reason and understand the type coercion rules.

**Real-Life Example:** Loose equality (`==`) is like asking "Do these two things look similar?" Strict equality (`===`) is like asking "Are these two things exactly identical?" The number 5 and the string "5" look similar, but they are not the same thing -- one is a number you can do math with, and the other is text.

---

### 5.5 Logical Operators

Logical operators combine or modify Boolean values. They are essential for building conditions in your programs.

#### AND Operator (&&)

Returns `true` only if **both** conditions are `true`.

```javascript
let age = 25;
let hasLicense = true;

console.log(age >= 18 && hasLicense); // Output: true (both conditions are true)
console.log(age >= 18 && !hasLicense); // Output: false (one condition is false)
```

**Real-Life Example:** To drive a car, you must be 18 or older **AND** have a driver's license. Both conditions must be true.

#### OR Operator (||)

Returns `true` if **at least one** condition is `true`.

```javascript
let isWeekend = true;
let isHoliday = false;

console.log(isWeekend || isHoliday); // Output: true (at least one is true)
console.log(false || false);         // Output: false (neither is true)
```

**Real-Life Example:** You stay home if it is a weekend **OR** a holiday. Either condition being true is enough.

#### NOT Operator (!)

**Reverses** a Boolean value. `true` becomes `false`, and `false` becomes `true`.

```javascript
let isRaining = true;

console.log(!isRaining);  // Output: false
console.log(!false);      // Output: true
```

**Real-Life Example:** The NOT operator is like a mirror image. If it IS raining (`true`), then "not raining" is `false`.

#### Truth Tables

```
    AND (&&) TRUTH TABLE          OR (||) TRUTH TABLE
    =====================         ====================

      A     │  B    │ A && B       A     │  B    │ A || B
    ────────┼───────┼────────    ────────┼───────┼────────
     true   │ true  │ true       true   │ true  │ true
     true   │ false │ false      true   │ false │ true
     false  │ true  │ false      false  │ true  │ true
     false  │ false │ false      false  │ false │ false


    NOT (!) TRUTH TABLE
    ===================

      A     │  !A
    ────────┼────────
     true   │ false
     false  │ true
```

---

### 5.6 String Concatenation vs Template Literals

There are two ways to combine strings with variables:

```javascript
let firstName = "Muhammad";
let lastName = "Fahad";
let age = 25;

// Method 1: String Concatenation (using +)
let intro1 = "My name is " + firstName + " " + lastName + " and I am " + age + " years old.";
console.log(intro1);
// Output: My name is Muhammad Fahad and I am 25 years old.

// Method 2: Template Literals (using backticks and ${})
let intro2 = `My name is ${firstName} ${lastName} and I am ${age} years old.`;
console.log(intro2);
// Output: My name is Muhammad Fahad and I am 25 years old.
```

> **Best Practice:** Always prefer template literals over string concatenation. They are cleaner, easier to read, and less error-prone.

---

### 5.7 Unary Operators: ++ and --

The increment (`++`) and decrement (`--`) operators add or subtract 1 from a variable.

```javascript
let count = 5;

count++;         // count = count + 1
console.log(count); // Output: 6

count--;         // count = count - 1
console.log(count); // Output: 5

// Prefix vs Postfix
let a = 10;
console.log(a++); // Output: 10 (returns value FIRST, then increments)
console.log(a);   // Output: 11

let b = 10;
console.log(++b); // Output: 11 (increments FIRST, then returns value)
console.log(b);   // Output: 11
```

```
    PREFIX vs POSTFIX
    =================

    let x = 5;

    x++ (Postfix)                ++x (Prefix)
    ─────────────                ─────────────
    1. Return current value (5)  1. Increment first (6)
    2. Then increment to 6       2. Then return new value (6)
```

---

## 6. Type Conversion and Coercion

JavaScript is a **dynamically typed** language, meaning a variable can hold any type of value, and the type can change during the program's execution. This flexibility is powerful, but it can also lead to unexpected behavior if you do not understand how type conversion works.

---

### 6.1 Explicit Conversion (You Do It Manually)

Explicit conversion is when **you** deliberately convert a value from one type to another using built-in functions.

#### Converting to String

```javascript
let num = 42;
let boolVal = true;

console.log(String(num));       // Output: "42"
console.log(String(boolVal));   // Output: "true"
console.log(String(null));      // Output: "null"
console.log(String(undefined)); // Output: "undefined"

// Alternative: .toString() method
console.log(num.toString());    // Output: "42"
console.log((100).toString());  // Output: "100"
```

#### Converting to Number

```javascript
console.log(Number("42"));       // Output: 42
console.log(Number("3.14"));     // Output: 3.14
console.log(Number(""));         // Output: 0
console.log(Number("hello"));    // Output: NaN (cannot convert text to number)
console.log(Number(true));       // Output: 1
console.log(Number(false));      // Output: 0
console.log(Number(null));       // Output: 0
console.log(Number(undefined));  // Output: NaN

// parseInt() and parseFloat()
console.log(parseInt("42px"));      // Output: 42  (parses until non-digit)
console.log(parseInt("3.99"));      // Output: 3   (ignores decimal part)
console.log(parseFloat("3.99"));    // Output: 3.99
console.log(parseInt("abc"));       // Output: NaN
console.log(parseInt("100", 2));    // Output: 4   (binary to decimal)
```

#### Converting to Boolean

```javascript
console.log(Boolean(1));          // Output: true
console.log(Boolean(0));          // Output: false
console.log(Boolean("hello"));    // Output: true
console.log(Boolean(""));         // Output: false
console.log(Boolean(null));       // Output: false
console.log(Boolean(undefined));  // Output: false
console.log(Boolean(NaN));        // Output: false
```

---

### 6.2 Implicit Coercion (JavaScript Does It Automatically)

Implicit coercion happens when JavaScript **automatically** converts a value's type behind the scenes. This is one of the most confusing aspects of JavaScript for beginners.

```javascript
// The + operator with strings triggers string concatenation
console.log("5" + 3);      // Output: "53"   (3 is converted to "3", then concatenated)
console.log("5" + true);   // Output: "5true"
console.log("5" + null);   // Output: "5null"

// Other math operators trigger number conversion
console.log("5" - 3);      // Output: 2     ("5" is converted to 5, then subtracted)
console.log("5" * 2);      // Output: 10    ("5" is converted to 5, then multiplied)
console.log("10" / 2);     // Output: 5     ("10" is converted to 10, then divided)
console.log("5" - true);   // Output: 4     (true is converted to 1)

// Some surprising results
console.log(true + true);  // Output: 2     (true = 1, so 1 + 1 = 2)
console.log(true + false); // Output: 1     (1 + 0 = 1)
console.log("" - 1);       // Output: -1    ("" converts to 0, so 0 - 1 = -1)
```

```
    WHY "5" + 3 = "53" BUT "5" - 3 = 2
    ====================================

    The + operator has TWO jobs:
    1. Addition (numbers)
    2. Concatenation (strings)

    When + sees a string, it picks concatenation:

    "5" + 3
    ┌─────┐   ┌─────┐
    │ "5" │ + │  3  │
    │(str)│   │(num)│
    └─────┘   └─────┘
        │         │
        │    Convert 3 to "3"
        │         │
        ▼         ▼
    ┌─────┐   ┌─────┐
    │ "5" │ + │ "3" │  =  "53" (string concatenation)
    └─────┘   └─────┘


    The - operator ONLY does subtraction:

    "5" - 3
    ┌─────┐   ┌─────┐
    │ "5" │ - │  3  │
    │(str)│   │(num)│
    └─────┘   └─────┘
        │         │
    Convert "5" to 5
        │         │
        ▼         ▼
    ┌─────┐   ┌─────┐
    │  5  │ - │  3  │  =  2 (math subtraction)
    └─────┘   └─────┘
```

---

### 6.3 Truthy and Falsy Values

In JavaScript, every value can be treated as either `true` or `false` when used in a Boolean context (such as an `if` statement). Values that behave like `true` are called **truthy**, and values that behave like `false` are called **falsy**.

#### All Falsy Values in JavaScript (There Are Only 8)

| Falsy Value | typeof | Description |
|:-----------:|:------:|-------------|
| `false` | boolean | The Boolean false itself |
| `0` | number | Zero |
| `-0` | number | Negative zero |
| `0n` | bigint | BigInt zero |
| `""` | string | Empty string (no characters) |
| `null` | object | Intentional absence of value |
| `undefined` | undefined | Variable not assigned |
| `NaN` | number | Not a Number (invalid math) |

> **Everything else is truthy.** This includes: any non-zero number, any non-empty string (even `"0"` and `"false"`), arrays `[]`, objects `{}`, and functions.

```javascript
// Falsy values
console.log(Boolean(0));         // Output: false
console.log(Boolean(""));        // Output: false
console.log(Boolean(null));      // Output: false
console.log(Boolean(undefined)); // Output: false
console.log(Boolean(NaN));       // Output: false

// Truthy values (some surprising ones!)
console.log(Boolean("0"));      // Output: true  (non-empty string!)
console.log(Boolean("false"));  // Output: true  (non-empty string!)
console.log(Boolean([]));       // Output: true  (empty array is truthy!)
console.log(Boolean({}));       // Output: true  (empty object is truthy!)
console.log(Boolean(-1));       // Output: true  (any non-zero number is truthy!)
```

**Real-Life Example:** Think of it like a light switch being controlled by the value. Falsy values turn the light OFF. Everything else turns the light ON. Zero, emptiness, and nothingness are "off." Anything with substance is "on."

---

## 7. console.log() and Debugging Basics

### 7.1 Console Methods

The `console` object provides several methods for printing output and debugging your JavaScript code.

#### console.log()

The most commonly used method. It prints values to the browser's Developer Tools Console.

```javascript
console.log("Hello, World!");             // Output: Hello, World!
console.log(42);                          // Output: 42
console.log(true);                        // Output: true
console.log("Name:", "Fahad", "Age:", 25); // Output: Name: Fahad Age: 25

// You can log multiple values separated by commas
let x = 10;
let y = 20;
console.log("x =", x, "y =", y, "sum =", x + y);
// Output: x = 10 y = 20 sum = 30
```

#### console.warn()

Displays a **warning message** with a yellow background in the console.

```javascript
console.warn("This feature is deprecated. Use the new API instead.");
// Output: ⚠ This feature is deprecated. Use the new API instead.
```

#### console.error()

Displays an **error message** with a red background in the console.

```javascript
console.error("Failed to load user data!");
// Output: ✖ Failed to load user data!
```

#### console.table()

Displays data in a formatted **table** in the console. This is especially useful for arrays and objects.

```javascript
let students = [
    { name: "Ali", age: 20, grade: "A" },
    { name: "Sara", age: 22, grade: "B" },
    { name: "Ahmed", age: 21, grade: "A+" }
];

console.table(students);
// Output:
// ┌─────────┬─────────┬─────┬───────┐
// │ (index) │  name   │ age │ grade │
// ├─────────┼─────────┼─────┼───────┤
// │    0    │ "Ali"   │ 20  │ "A"   │
// │    1    │ "Sara"  │ 22  │ "B"   │
// │    2    │ "Ahmed" │ 21  │ "A+"  │
// └─────────┴─────────┴─────┴───────┘
```

```
    CONSOLE METHODS AT A GLANCE
    ===========================

    ┌──────────────────┬──────────────────────────────────┐
    │     Method       │          Use Case                │
    ├──────────────────┼──────────────────────────────────┤
    │  console.log()   │  General output and debugging    │
    │  console.warn()  │  Warning messages (yellow)       │
    │  console.error() │  Error messages (red)            │
    │  console.table() │  Display arrays/objects as table │
    └──────────────────┴──────────────────────────────────┘
```

---

### 7.2 Using Browser DevTools

The **Developer Tools** (DevTools) built into every modern browser are your best friend for debugging JavaScript.

**How to Open DevTools:**

| Browser | Shortcut (Windows) | Shortcut (Mac) |
|---------|-------------------|----------------|
| Chrome | `F12` or `Ctrl + Shift + J` | `Cmd + Option + J` |
| Firefox | `F12` or `Ctrl + Shift + K` | `Cmd + Option + K` |
| Edge | `F12` or `Ctrl + Shift + J` | `Cmd + Option + J` |

**Key DevTools Tabs:**

| Tab | Purpose |
|-----|---------|
| **Console** | View output, errors, and run JavaScript commands |
| **Elements** | Inspect and modify HTML and CSS in real time |
| **Sources** | View and debug your JavaScript source files |
| **Network** | Monitor HTTP requests and responses |

**Debugging Tips for Beginners:**

1. **Read the error message carefully.** JavaScript error messages tell you the file name, line number, and type of error. Always read them.
2. **Use `console.log()` liberally.** When your code is not working, add `console.log()` statements to check the values of your variables at different points.
3. **Check the Console tab first.** If your code is not working, open DevTools and look for red error messages.
4. **Check for typos.** Most beginner bugs are caused by misspelled variable names, missing semicolons, or unclosed brackets.

---

## 8. String Methods

Strings in JavaScript come with many built-in methods that allow you to manipulate and inspect text. These methods do **not** change the original string -- they return a **new** string instead (strings are immutable).

---

### 8.1 length

The `length` property returns the number of characters in a string.

```javascript
let message = "Hello, World!";
console.log(message.length); // Output: 13 (spaces and punctuation count!)

let empty = "";
console.log(empty.length);  // Output: 0
```

> **Note:** `length` is a **property**, not a method -- so you do not use parentheses `()`.

---

### 8.2 toUpperCase() and toLowerCase()

Convert a string to all uppercase or all lowercase letters.

```javascript
let greeting = "Hello, World!";

console.log(greeting.toUpperCase()); // Output: "HELLO, WORLD!"
console.log(greeting.toLowerCase()); // Output: "hello, world!"

// The original string is NOT changed
console.log(greeting); // Output: "Hello, World!" (unchanged)
```

**Real-Life Example:** When websites store email addresses, they often convert them to lowercase first to avoid duplicates: `"User@Email.COM"` becomes `"user@email.com"`.

---

### 8.3 trim(), trimStart(), trimEnd()

Remove whitespace from the beginning and/or end of a string.

```javascript
let userInput = "   Hello, World!   ";

console.log(userInput.trim());      // Output: "Hello, World!"
console.log(userInput.trimStart()); // Output: "Hello, World!   "
console.log(userInput.trimEnd());   // Output: "   Hello, World!"
```

**Real-Life Example:** When a user types their name in a form and accidentally adds spaces before or after, `trim()` cleans it up before saving to the database.

---

### 8.4 includes()

Checks if a string **contains** a specific substring. Returns `true` or `false`.

```javascript
let sentence = "JavaScript is an amazing language";

console.log(sentence.includes("amazing"));   // Output: true
console.log(sentence.includes("terrible"));  // Output: false
console.log(sentence.includes("java"));      // Output: false (case-sensitive!)
console.log(sentence.includes("Java"));      // Output: true
```

---

### 8.5 indexOf()

Returns the **position** (index) of the first occurrence of a substring. Returns `-1` if not found.

```javascript
let text = "Hello, World! Hello, JavaScript!";

console.log(text.indexOf("Hello"));       // Output: 0  (first occurrence)
console.log(text.indexOf("World"));       // Output: 7
console.log(text.indexOf("Python"));      // Output: -1 (not found)
console.log(text.indexOf("Hello", 5));    // Output: 14 (search starting from index 5)
```

---

### 8.6 slice()

Extracts a portion of a string and returns it as a new string.

```javascript
let text = "Hello, World!";

console.log(text.slice(0, 5));    // Output: "Hello"    (from index 0 to 4)
console.log(text.slice(7));       // Output: "World!"   (from index 7 to end)
console.log(text.slice(-6));      // Output: "orld!"    (last 6 characters — wait!)
console.log(text.slice(-6));      // Output: "orld!"    
console.log(text.slice(0, -1));   // Output: "Hello, World"  (everything except last char)

// Negative indices count from the end
// -1 = last character, -2 = second to last, etc.
```

```
    HOW slice() WORKS
    =================

    text = "Hello, World!"

    Index:    0  1  2  3  4  5  6  7  8  9  10  11  12
            ┌──┬──┬──┬──┬──┬──┬──┬──┬──┬──┬───┬───┬───┐
            │H │e │l │l │o │, │  │W │o │r │ l │ d │ ! │
            └──┴──┴──┴──┴──┴──┴──┴──┴──┴──┴───┴───┴───┘
    Negative: -13       -8  -7  -6          -3  -2  -1

    slice(0, 5)  →  "Hello"       (index 0 to 4)
    slice(7)     →  "World!"      (index 7 to end)
    slice(-6)    →  "orld!"       (from 6th-to-last to end)
    slice(0, -1) →  "Hello, World" (start to second-to-last)
```

---

### 8.7 split()

Splits a string into an **array** of substrings based on a separator.

```javascript
let csv = "Ali,Sara,Ahmed,Fatima";
let names = csv.split(",");
console.log(names);
// Output: ["Ali", "Sara", "Ahmed", "Fatima"]

let sentence = "JavaScript is awesome";
let words = sentence.split(" ");
console.log(words);
// Output: ["JavaScript", "is", "awesome"]

let word = "Hello";
let letters = word.split("");
console.log(letters);
// Output: ["H", "e", "l", "l", "o"]
```

---

### 8.8 replace() and replaceAll()

Replaces occurrences of a substring with another substring.

```javascript
let message = "Hello, World!";

console.log(message.replace("World", "JavaScript"));
// Output: "Hello, JavaScript!"

// replace() only replaces the FIRST occurrence
let text = "cat and cat and cat";
console.log(text.replace("cat", "dog"));
// Output: "dog and cat and cat"

// replaceAll() replaces ALL occurrences
console.log(text.replaceAll("cat", "dog"));
// Output: "dog and dog and dog"
```

---

### 8.9 charAt()

Returns the character at a specific index.

```javascript
let text = "JavaScript";

console.log(text.charAt(0));   // Output: "J"
console.log(text.charAt(4));   // Output: "S"
console.log(text.charAt(100)); // Output: "" (empty string if index is out of range)

// You can also use bracket notation (more common in modern JS)
console.log(text[0]);          // Output: "J"
console.log(text[4]);          // Output: "S"
```

---

### 8.10 startsWith() and endsWith()

Check if a string starts or ends with a specific substring. Returns `true` or `false`.

```javascript
let url = "https://www.google.com";

console.log(url.startsWith("https")); // Output: true
console.log(url.startsWith("http"));  // Output: true
console.log(url.startsWith("ftp"));   // Output: false

let fileName = "report.pdf";

console.log(fileName.endsWith(".pdf"));  // Output: true
console.log(fileName.endsWith(".doc"));  // Output: false
```

---

### 8.11 repeat()

Returns a new string with the original string repeated a specified number of times.

```javascript
let star = "*";
console.log(star.repeat(5));     // Output: "*****"

let dash = "-";
console.log(dash.repeat(20));    // Output: "--------------------"

let greeting = "Ho! ";
console.log(greeting.repeat(3)); // Output: "Ho! Ho! Ho! "
```

---

### 8.12 Template Literals with Expressions

Template literals are not just for inserting variables. You can put any valid JavaScript **expression** inside `${}`.

```javascript
let price = 500;
let quantity = 3;
let taxRate = 0.17;

console.log(`Subtotal: Rs. ${price * quantity}`);
// Output: Subtotal: Rs. 1500

console.log(`Tax: Rs. ${(price * quantity * taxRate).toFixed(2)}`);
// Output: Tax: Rs. 255.00

console.log(`Total: Rs. ${(price * quantity * (1 + taxRate)).toFixed(2)}`);
// Output: Total: Rs. 1755.00

// You can even call methods inside ${}
let name = "fahad";
console.log(`Hello, ${name.toUpperCase()}!`);
// Output: Hello, FAHAD!

// Ternary expressions work too
let age = 20;
console.log(`You are ${age >= 18 ? "an adult" : "a minor"}.`);
// Output: You are an adult.
```

---

### String Methods Quick Reference Table

| Method | What It Does | Example | Result |
|--------|-------------|---------|--------|
| `.length` | Returns string length | `"Hello".length` | `5` |
| `.toUpperCase()` | Converts to uppercase | `"hello".toUpperCase()` | `"HELLO"` |
| `.toLowerCase()` | Converts to lowercase | `"HELLO".toLowerCase()` | `"hello"` |
| `.trim()` | Removes surrounding spaces | `" hi ".trim()` | `"hi"` |
| `.includes("x")` | Checks if contains "x" | `"Hello".includes("ell")` | `true` |
| `.indexOf("x")` | Finds position of "x" | `"Hello".indexOf("l")` | `2` |
| `.slice(a, b)` | Extracts from a to b | `"Hello".slice(1, 4)` | `"ell"` |
| `.split("x")` | Splits by "x" into array | `"a-b-c".split("-")` | `["a","b","c"]` |
| `.replace("a","b")` | Replaces first "a" with "b" | `"Hi Hi".replace("Hi","Bye")` | `"Bye Hi"` |
| `.charAt(n)` | Character at index n | `"Hello".charAt(1)` | `"e"` |
| `.startsWith("x")` | Starts with "x"? | `"Hello".startsWith("He")` | `true` |
| `.endsWith("x")` | Ends with "x"? | `"Hello".endsWith("lo")` | `true` |
| `.repeat(n)` | Repeats n times | `"Ha".repeat(3)` | `"HaHaHa"` |

---

## 9. Number Methods

JavaScript provides built-in methods and the `Math` object for working with numbers.

---

### 9.1 toFixed()

Formats a number to a specified number of decimal places. Returns a **string**.

```javascript
let price = 19.99678;

console.log(price.toFixed(2));  // Output: "19.99"
console.log(price.toFixed(0));  // Output: "20"     (rounded)
console.log(price.toFixed(4));  // Output: "19.9968" (rounded)

// Useful for displaying prices
let total = 100 / 3;
console.log(`Total: Rs. ${total.toFixed(2)}`);
// Output: Total: Rs. 33.33
```

> **Note:** `toFixed()` returns a **string**, not a number. If you need a number, wrap it with `Number()` or use the unary `+` operator: `+price.toFixed(2)`.

---

### 9.2 parseInt() and parseFloat()

These functions convert strings to numbers by parsing the string from left to right.

```javascript
// parseInt() — parses an integer (whole number)
console.log(parseInt("42"));        // Output: 42
console.log(parseInt("42.99"));     // Output: 42    (drops decimal part)
console.log(parseInt("42px"));      // Output: 42    (stops at non-digit)
console.log(parseInt("width: 42")); // Output: NaN   (starts with non-digit)
console.log(parseInt("0xFF"));      // Output: 255   (hexadecimal)

// parseFloat() — parses a decimal number
console.log(parseFloat("3.14"));    // Output: 3.14
console.log(parseFloat("3.14.15")); // Output: 3.14  (stops at second dot)
console.log(parseFloat("42px"));    // Output: 42
```

**Real-Life Example:** If you get user input from an HTML form, it always comes as a string. If the user types "25" in an age field, you receive the string `"25"`, not the number `25`. You need `parseInt()` or `Number()` to convert it.

---

### 9.3 The Math Object

The `Math` object is a built-in JavaScript object that provides mathematical constants and functions. You do not need to create it -- it is always available.

#### Math.round() — Round to Nearest Integer

```javascript
console.log(Math.round(4.5));  // Output: 5  (rounds up at .5)
console.log(Math.round(4.4));  // Output: 4  (rounds down below .5)
console.log(Math.round(4.7));  // Output: 5
console.log(Math.round(-4.5)); // Output: -4
```

#### Math.floor() — Round DOWN (Towards Negative Infinity)

```javascript
console.log(Math.floor(4.9));  // Output: 4  (always rounds down)
console.log(Math.floor(4.1));  // Output: 4
console.log(Math.floor(-4.1)); // Output: -5 (rounds towards negative infinity)
```

#### Math.ceil() — Round UP (Towards Positive Infinity)

```javascript
console.log(Math.ceil(4.1));   // Output: 5  (always rounds up)
console.log(Math.ceil(4.9));   // Output: 5
console.log(Math.ceil(-4.9));  // Output: -4 (rounds towards positive infinity)
```

```
    ROUNDING METHODS COMPARED
    =========================

    Value     │ Math.round() │ Math.floor() │ Math.ceil()
    ──────────┼──────────────┼──────────────┼────────────
     4.2      │      4       │      4       │     5
     4.5      │      5       │      4       │     5
     4.8      │      5       │      4       │     5
    -4.2      │     -4       │     -5       │    -4
    -4.5      │     -4       │     -5       │    -4
    -4.8      │     -5       │     -5       │    -4
```

#### Math.random() — Generate a Random Number

`Math.random()` returns a random decimal number between 0 (inclusive) and 1 (exclusive).

```javascript
console.log(Math.random());  // Output: 0.7382947362... (different every time)
console.log(Math.random());  // Output: 0.1293847561... (different every time)

// Random number between 0 and 9
console.log(Math.floor(Math.random() * 10));
// Output: 0, 1, 2, 3, 4, 5, 6, 7, 8, or 9

// Random number between 1 and 10
console.log(Math.floor(Math.random() * 10) + 1);
// Output: 1, 2, 3, 4, 5, 6, 7, 8, 9, or 10

// Random number between min and max (inclusive)
function getRandomInt(min, max) {
    return Math.floor(Math.random() * (max - min + 1)) + min;
}
console.log(getRandomInt(1, 100));  // Random number between 1 and 100
```

```
    GENERATING RANDOM NUMBERS
    =========================

    Math.random()
    │
    ▼
    0.0 ──────────────────────── 0.999...
    (inclusive)                  (exclusive)


    Math.floor(Math.random() * 10)
    │
    ▼
    0, 1, 2, 3, 4, 5, 6, 7, 8, 9


    Math.floor(Math.random() * 10) + 1
    │
    ▼
    1, 2, 3, 4, 5, 6, 7, 8, 9, 10
```

#### Math.max() and Math.min() — Find Largest/Smallest

```javascript
console.log(Math.max(10, 20, 5, 30, 15)); // Output: 30
console.log(Math.min(10, 20, 5, 30, 15)); // Output: 5

// Useful with arrays (using the spread operator)
let scores = [85, 92, 78, 95, 88];
console.log(Math.max(...scores)); // Output: 95
console.log(Math.min(...scores)); // Output: 78
```

#### Math.abs() — Absolute Value

Returns the absolute (positive) value of a number.

```javascript
console.log(Math.abs(-5));    // Output: 5
console.log(Math.abs(5));     // Output: 5
console.log(Math.abs(-3.14)); // Output: 3.14
console.log(Math.abs(0));     // Output: 0
```

**Real-Life Example:** If the temperature drops by -10 degrees, the absolute change is still 10 degrees. `Math.abs()` gives you the magnitude without the sign.

---

### Number Methods and Math Object Quick Reference

| Method/Property | What It Does | Example | Result |
|----------------|-------------|---------|--------|
| `.toFixed(n)` | Format to n decimal places | `(3.14159).toFixed(2)` | `"3.14"` |
| `parseInt(str)` | Parse string to integer | `parseInt("42px")` | `42` |
| `parseFloat(str)` | Parse string to decimal | `parseFloat("3.14px")` | `3.14` |
| `Math.round(x)` | Round to nearest integer | `Math.round(4.5)` | `5` |
| `Math.floor(x)` | Round down | `Math.floor(4.9)` | `4` |
| `Math.ceil(x)` | Round up | `Math.ceil(4.1)` | `5` |
| `Math.random()` | Random decimal 0 to 0.999... | `Math.random()` | `0.482...` |
| `Math.max(a,b,...)` | Largest value | `Math.max(1,5,3)` | `5` |
| `Math.min(a,b,...)` | Smallest value | `Math.min(1,5,3)` | `1` |
| `Math.abs(x)` | Absolute value | `Math.abs(-7)` | `7` |

---

## 10. Summary

Congratulations! You have completed your introduction to JavaScript. This is a massive milestone -- you have gone from building static web pages with HTML and CSS to writing your first lines of code in a real programming language.

### What You Learned This Week

| Topic | Key Takeaway |
|-------|-------------|
| **What is JavaScript** | A programming language that makes websites interactive. Created by Brendan Eich in 1995. The only language that runs natively in browsers. |
| **Setting Up** | You can run JS in the browser console, inline with `<script>` tags, or from external `.js` files linked to HTML. |
| **Variables** | Named containers for storing data. Use `const` by default, `let` when the value needs to change. Never use `var`. |
| **Data Types** | 7 primitive types: String, Number, Boolean, undefined, null, BigInt, Symbol. Use `typeof` to check types. |
| **Operators** | Arithmetic (`+`, `-`, `*`, `/`, `%`, `**`), Assignment (`=`, `+=`), Comparison (`===`, `!==`), Logical (`&&`, `\|\|`, `!`). |
| **Type Conversion** | Explicit (you do it with `String()`, `Number()`, `Boolean()`) vs Implicit (JS does it automatically). |
| **Debugging** | Use `console.log()` to inspect values. Open DevTools with F12. Read error messages carefully. |
| **String Methods** | `.toUpperCase()`, `.toLowerCase()`, `.trim()`, `.includes()`, `.slice()`, `.split()`, `.replace()`, and more. |
| **Number Methods** | `.toFixed()`, `parseInt()`, `parseFloat()`, `Math.round()`, `Math.floor()`, `Math.ceil()`, `Math.random()`. |

### The Most Important Rules to Remember

1. **Always use `===` instead of `==`** -- avoid type coercion bugs.
2. **Always use `const` first** -- only switch to `let` if you need to reassign.
3. **Never use `var`** -- it has scoping issues that cause hard-to-find bugs.
4. **Use template literals** (backticks) instead of string concatenation.
5. **Name your variables descriptively** -- use camelCase and avoid single letters.
6. **Use `console.log()` liberally** -- it is your best debugging tool as a beginner.

```
    YOUR JAVASCRIPT JOURNEY
    =======================

    Weeks 1-4          Weeks 5-8          Week 9
    ┌──────────┐       ┌──────────┐       ┌──────────────────┐
    │   HTML   │ ────▶ │   CSS    │ ────▶ │   JavaScript     │
    │Structure │       │  Style   │       │   Fundamentals   │
    └──────────┘       └──────────┘       └──────────────────┘
                                                 │
                                                 │  You are HERE!
                                                 ▼
                                          ┌──────────────────┐
                                          │   Week 10+       │
                                          │   Control Flow   │
                                          │   Functions      │
                                          │   Arrays         │
                                          │   Objects        │
                                          │   DOM            │
                                          │   ... and more!  │
                                          └──────────────────┘
```

> **Next Week Preview:** In Week 10, you will learn about **Control Flow** -- `if/else` statements, `switch`, and loops (`for`, `while`). These tools will let your programs make decisions and repeat actions, bringing your code to life!

---

*End of Week 9 Notes*
