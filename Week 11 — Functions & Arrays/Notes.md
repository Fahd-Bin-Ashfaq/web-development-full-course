# Week 11: Functions & Arrays

> **Prerequisites:** JavaScript fundamentals, control flow (if/else, switch), and loops (for, while) from Weeks 9-10.

---

## Table of Contents

1. [Functions Introduction](#1-functions-introduction)
2. [Function Declaration](#2-function-declaration)
3. [Function Expression](#3-function-expression)
4. [Arrow Functions (ES6)](#4-arrow-functions-es6)
5. [Scope](#5-scope)
6. [Callback Functions (Introduction)](#6-callback-functions-introduction)
7. [Arrays Introduction](#7-arrays-introduction)
8. [Array Methods (Detailed)](#8-array-methods-detailed)
9. [Destructuring Arrays (ES6)](#9-destructuring-arrays-es6)
10. [Spread Operator with Arrays](#10-spread-operator-with-arrays)
11. [Summary & Method Cheat Sheet](#11-summary--method-cheat-sheet)

---

## 1. Functions Introduction

### What Is a Function?

A function is a reusable block of code designed to perform a specific task. You define it once and call it as many times as you need.

**Real-life analogy: A Recipe**

Think of a function like a recipe. A recipe for pancakes tells you the ingredients (inputs), the steps (process), and what you get at the end (output). You do not rewrite the recipe every time you want pancakes. You just follow the same recipe again and again.

**Real-life analogy: A Coffee Machine**

A coffee machine is a function. You put in coffee beans and water (inputs), the machine brews the coffee (process), and you get a cup of coffee (output). You do not need to know the internal mechanics. You just use it.

```
               FUNCTION FLOW
  =========================================

  +--------+      +-----------+      +--------+
  | INPUT  | ---> | PROCESS   | ---> | OUTPUT |
  | (data) |      | (code     |      | (result)|
  |        |      |  runs)    |      |        |
  +--------+      +-----------+      +--------+

  Example: Coffee Machine

  +----------+      +-------------+      +--------+
  | Coffee   | ---> | Brewing     | ---> | Coffee |
  | Beans +  |      | Process     |      | Cup    |
  | Water    |      |             |      |        |
  +----------+      +-------------+      +--------+
```

### Why Use Functions?

**The DRY Principle: Don't Repeat Yourself**

Without functions, you would copy-paste the same logic over and over. If you need to change that logic later, you would have to find and update every copy. Functions solve this problem.

```javascript
// WITHOUT functions (repeating yourself)
console.log("Hello, Ali! Welcome to the course.");
console.log("Hello, Sara! Welcome to the course.");
console.log("Hello, Ahmed! Welcome to the course.");

// WITH a function (DRY principle)
function greetStudent(name) {
  console.log("Hello, " + name + "! Welcome to the course.");
}

greetStudent("Ali");     // Hello, Ali! Welcome to the course.
greetStudent("Sara");    // Hello, Sara! Welcome to the course.
greetStudent("Ahmed");   // Hello, Ahmed! Welcome to the course.
```

**Benefits of functions:**

| Benefit         | Description                                              |
|-----------------|----------------------------------------------------------|
| Reusability     | Write once, use many times                               |
| Readability     | Give meaningful names to blocks of code                  |
| Maintainability | Change logic in one place, and it updates everywhere     |
| Debugging       | Isolate problems to specific functions                   |
| Organization    | Break large programs into small, manageable pieces       |

---

## 2. Function Declaration

### Basic Syntax

```javascript
function functionName(parameter1, parameter2) {
  // Code to execute
  return result;
}
```

```javascript
function add(a, b) {
  return a + b;
}

let sum = add(5, 3);
console.log(sum); // 8
```

### Parameters vs Arguments

Parameters and arguments are related but different concepts. People often mix them up, so pay attention to the distinction.

- **Parameters** are the variable names listed in the function definition. They are placeholders.
- **Arguments** are the actual values you pass when you call the function.

```
  PARAMETERS vs ARGUMENTS
  ========================

  Function Definition (PARAMETERS are placeholders):
  +--------------------------------------------+
  | function greet(name, age) {                |
  |                ^^^^  ^^^                   |
  |            parameter  parameter            |
  |   return "Hi " + name + ", age " + age;    |
  | }                                          |
  +--------------------------------------------+

  Function Call (ARGUMENTS are real values):
  +--------------------------------------------+
  | greet("Ali", 25);                          |
  |        ^^^   ^^                            |
  |    argument  argument                      |
  +--------------------------------------------+

  When called: name = "Ali", age = 25
```

```javascript
// "name" and "age" are PARAMETERS
function introduce(name, age) {
  return "My name is " + name + " and I am " + age + " years old.";
}

// "Ali" and 25 are ARGUMENTS
console.log(introduce("Ali", 25));
// My name is Ali and I am 25 years old.
```

### The Return Statement

The `return` statement does two things:

1. It sends a value back to wherever the function was called.
2. It immediately stops the function. Any code after `return` will not execute.

```javascript
function multiply(a, b) {
  return a * b;
  console.log("This will NEVER run"); // Unreachable code
}

let result = multiply(4, 5);
console.log(result); // 20
```

**What happens without a return statement?**

If a function has no `return`, it returns `undefined` by default.

```javascript
function sayHello(name) {
  console.log("Hello, " + name);
  // No return statement
}

let value = sayHello("Sara"); // Hello, Sara
console.log(value);           // undefined
```

### Multiple Parameters

Functions can accept any number of parameters.

```javascript
function createFullName(firstName, middleName, lastName) {
  return firstName + " " + middleName + " " + lastName;
}

console.log(createFullName("Muhammad", "Ali", "Khan"));
// Muhammad Ali Khan
```

### Default Parameters (ES6)

Default parameters let you set fallback values. If the caller does not provide an argument, the default kicks in.

```javascript
function greet(name = "Guest", greeting = "Hello") {
  return greeting + ", " + name + "!";
}

console.log(greet("Ali", "Hi"));   // Hi, Ali!
console.log(greet("Sara"));        // Hello, Sara!
console.log(greet());              // Hello, Guest!
```

**Real-life analogy:** Think of a restaurant order form. If a customer does not specify a drink, the default is water. If they do not specify spice level, the default is medium.

---

## 3. Function Expression

A function expression stores a function inside a variable.

```javascript
const greet = function(name) {
  return "Hello, " + name + "!";
};

console.log(greet("Ali")); // Hello, Ali!
```

Note the semicolon at the end. Since this is a variable assignment statement, it ends with a semicolon just like any other assignment.

### Declaration vs Expression: Hoisting

The key difference between a function declaration and a function expression is **hoisting**.

**Hoisting** means JavaScript moves declarations to the top of their scope before execution. Function declarations are fully hoisted. Function expressions are not.

```javascript
// FUNCTION DECLARATION -- works even if called BEFORE it is defined
console.log(add(2, 3)); // 5

function add(a, b) {
  return a + b;
}
```

```javascript
// FUNCTION EXPRESSION -- does NOT work before it is defined
console.log(multiply(2, 3)); // ERROR: Cannot access 'multiply' before initialization

const multiply = function(a, b) {
  return a * b;
};
```

```
  HOISTING BEHAVIOR
  ==================

  JavaScript reads your file in two passes:

  Pass 1 (Compilation):
  +------------------------------------------------+
  | - Finds all "function" declarations             |
  | - Moves them to the top (hoists them)           |
  | - Variables declared with const/let are noted   |
  |   but NOT initialized (Temporal Dead Zone)      |
  +------------------------------------------------+

  Pass 2 (Execution):
  +------------------------------------------------+
  | - Runs code line by line from top to bottom     |
  | - Declarations are already available            |
  | - Expressions are assigned when their line runs |
  +------------------------------------------------+
```

| Feature              | Function Declaration          | Function Expression             |
|----------------------|-------------------------------|---------------------------------|
| Syntax               | `function name() {}`          | `const name = function() {}`    |
| Hoisted?             | Yes (fully)                   | No                              |
| Can call before def? | Yes                           | No                              |
| Named/Anonymous      | Always named                  | Can be anonymous                |

---

## 4. Arrow Functions (ES6)

Arrow functions provide a shorter syntax for writing functions. They were introduced in ES6 (2015).

### Basic Syntax

```javascript
// Regular function expression
const greet = function(name) {
  return "Hello, " + name + "!";
};

// Arrow function (equivalent)
const greetArrow = (name) => {
  return "Hello, " + name + "!";
};

console.log(greetArrow("Ali")); // Hello, Ali!
```

### Shorthand Rules

**1. Single parameter: parentheses are optional**

```javascript
const square = x => {
  return x * x;
};

console.log(square(5)); // 25
```

**2. Single expression: curly braces and return are optional (implicit return)**

```javascript
const square = x => x * x;

console.log(square(5)); // 25
```

**3. No parameters: empty parentheses are required**

```javascript
const sayHello = () => "Hello, World!";

console.log(sayHello()); // Hello, World!
```

**4. Multiple parameters: parentheses are required**

```javascript
const add = (a, b) => a + b;

console.log(add(3, 7)); // 10
```

### When to Use Arrow Functions vs Regular Functions

Arrow functions are great for short, simple operations, especially when passing functions as arguments (callbacks). However, they have some differences with regular functions regarding the `this` keyword, which you will learn about when we cover objects and classes.

**General rule for now:** Use arrow functions for short operations and callbacks. Use regular functions when you need hoisting or when defining methods on objects.

### Comparison Table: All Three Function Types

| Feature               | Declaration              | Expression                    | Arrow Function              |
|-----------------------|--------------------------|-------------------------------|-----------------------------|
| Syntax                | `function name() {}`     | `const name = function() {}`  | `const name = () => {}`     |
| Hoisted?              | Yes                      | No                            | No                          |
| `this` binding        | Dynamic                  | Dynamic                       | Lexical (inherits parent)   |
| Can be anonymous?     | No                       | Yes                           | Yes                         |
| Best for              | General-purpose          | Conditional assignment        | Callbacks, short operations |
| `arguments` object    | Yes                      | Yes                           | No                          |

```javascript
// All three doing the same thing:

// 1. Function Declaration
function addDecl(a, b) {
  return a + b;
}

// 2. Function Expression
const addExpr = function(a, b) {
  return a + b;
};

// 3. Arrow Function
const addArrow = (a, b) => a + b;

console.log(addDecl(2, 3));  // 5
console.log(addExpr(2, 3));  // 5
console.log(addArrow(2, 3)); // 5
```

---

## 5. Scope

Scope determines where variables are accessible in your code. Think of it as the "visibility" of a variable.

### Real-Life Analogy: Access Levels in a Building

```
  SCOPE IS LIKE ACCESS LEVELS IN A BUILDING
  ==========================================

  +=============================================+
  |  GLOBAL SCOPE (Public Lobby)                |
  |  Everyone can access this area.             |
  |  Variables here are visible everywhere.     |
  |                                             |
  |  +---------------------------------------+  |
  |  |  FUNCTION SCOPE (Employee Floor)      |  |
  |  |  Only employees can enter here.       |  |
  |  |  Variables here are NOT visible       |  |
  |  |  in the lobby.                        |  |
  |  |                                       |  |
  |  |  +-------------------------------+    |  |
  |  |  |  BLOCK SCOPE (Manager Office) |    |  |
  |  |  |  Only managers can enter.     |    |  |
  |  |  |  Variables here are NOT       |    |  |
  |  |  |  visible on the employee      |    |  |
  |  |  |  floor or the lobby.          |    |  |
  |  |  +-------------------------------+    |  |
  |  |                                       |  |
  |  +---------------------------------------+  |
  |                                             |
  +=============================================+

  Inner scopes CAN see outer scopes.
  Outer scopes CANNOT see inner scopes.
```

### Global Scope

Variables declared outside of any function or block are in the global scope. They are accessible everywhere.

```javascript
let appName = "My MERN App"; // Global scope

function showApp() {
  console.log(appName); // Can access global variable
}

showApp(); // My MERN App
console.log(appName); // My MERN App
```

### Local / Function Scope

Variables declared inside a function are only accessible within that function.

```javascript
function calculateArea() {
  let width = 10;  // Local to this function
  let height = 5;  // Local to this function
  return width * height;
}

console.log(calculateArea()); // 50
// console.log(width);        // ERROR: width is not defined
```

### Block Scope (let and const vs var)

`let` and `const` are block-scoped: they exist only within the nearest set of curly braces `{}`. `var` ignores block scope and is function-scoped.

```javascript
if (true) {
  let blockLet = "I am block-scoped";
  const blockConst = "I am also block-scoped";
  var notBlock = "I am NOT block-scoped";
}

// console.log(blockLet);   // ERROR: not defined
// console.log(blockConst); // ERROR: not defined
console.log(notBlock);      // "I am NOT block-scoped" (var leaks out!)
```

This is one of the main reasons we prefer `let` and `const` over `var`. The `var` keyword can lead to unexpected bugs because it does not respect block boundaries.

### Scope Nesting Diagram

```
  SCOPE NESTING
  ==============

  +------ GLOBAL SCOPE ---------------------------------+
  |  let a = "global";                                   |
  |                                                      |
  |  +------ FUNCTION SCOPE (outer) -----------------+  |
  |  |  let b = "outer function";                     |  |
  |  |  // Can access: a, b                           |  |
  |  |                                                |  |
  |  |  +------ FUNCTION SCOPE (inner) -----------+   |  |
  |  |  |  let c = "inner function";              |   |  |
  |  |  |  // Can access: a, b, c                 |   |  |
  |  |  |                                         |   |  |
  |  |  |  +--- BLOCK SCOPE (if/for) ---------+   |   |  |
  |  |  |  |  let d = "block";                |   |   |  |
  |  |  |  |  // Can access: a, b, c, d       |   |   |  |
  |  |  |  +----------------------------------+   |   |  |
  |  |  |                                         |   |  |
  |  |  |  // Cannot access: d                    |   |  |
  |  |  +-----------------------------------------+   |  |
  |  |                                                |  |
  |  |  // Cannot access: c, d                        |  |
  |  +------------------------------------------------+  |
  |                                                      |
  |  // Cannot access: b, c, d                           |
  +------------------------------------------------------+
```

### Scope Chain

When JavaScript encounters a variable, it looks for it in the current scope first. If it does not find it, it moves up to the parent scope, then the parent's parent, and so on until it reaches the global scope. This is called the **scope chain**.

```javascript
let color = "red"; // Global

function outer() {
  let size = "large"; // outer function scope

  function inner() {
    let shape = "circle"; // inner function scope

    // JavaScript looks for each variable starting from the current scope
    console.log(shape); // Found in current scope: "circle"
    console.log(size);  // Not here, look up -> found in outer: "large"
    console.log(color); // Not here, not in outer, look up -> found in global: "red"
  }

  inner();
}

outer();
```

```
  SCOPE CHAIN LOOKUP
  ===================

  console.log(color) inside inner():

  Step 1: Look in inner() scope    --> Not found
  Step 2: Look in outer() scope    --> Not found
  Step 3: Look in global scope     --> Found! "red"
```

---

## 6. Callback Functions (Introduction)

### What Is a Callback?

A callback is a function that is passed as an argument to another function. The receiving function can then "call back" (execute) that function whenever it needs to.

**Real-life analogy:** You call a restaurant and they say, "We will call you back when your table is ready." You give them your phone number (the callback), and they use it later.

```javascript
function processOrder(orderName, callback) {
  console.log("Processing order: " + orderName);
  callback(); // Execute the callback function
}

function notifyCustomer() {
  console.log("Your order is ready!");
}

processOrder("Burger", notifyCustomer);
// Processing order: Burger
// Your order is ready!
```

### More Practical Examples

```javascript
// Callback with parameters
function calculate(a, b, operation) {
  return operation(a, b);
}

const add = (x, y) => x + y;
const subtract = (x, y) => x - y;
const multiply = (x, y) => x * y;

console.log(calculate(10, 5, add));      // 15
console.log(calculate(10, 5, subtract)); // 5
console.log(calculate(10, 5, multiply)); // 50
```

```javascript
// Anonymous callback (inline function)
function repeatAction(times, action) {
  for (let i = 0; i < times; i++) {
    action(i);
  }
}

repeatAction(3, function(index) {
  console.log("Action #" + (index + 1));
});
// Action #1
// Action #2
// Action #3

// Same thing with an arrow function
repeatAction(3, (index) => {
  console.log("Arrow action #" + (index + 1));
});
// Arrow action #1
// Arrow action #2
// Arrow action #3
```

### Why Callbacks Matter

Callbacks are foundational to JavaScript programming. You will encounter them constantly:

- **Array methods** like `map()`, `filter()`, and `forEach()` all use callbacks (covered later in this lesson).
- **Event handling** uses callbacks (e.g., what to do when a button is clicked).
- **Asynchronous JavaScript** relies heavily on callbacks (e.g., fetching data from a server).
- **React** uses callbacks extensively for event handlers and effects.

---

## 7. Arrays Introduction

### What Is an Array?

An array is an ordered collection of values stored in a single variable. Each value has a numbered position called an **index**.

**Real-life examples:**

- A **shopping list**: `["Milk", "Eggs", "Bread", "Butter"]`
- A **class of students**: `["Ali", "Sara", "Ahmed", "Fatima"]`
- A **playlist**: `["Song A", "Song B", "Song C"]`

### Creating Arrays

```javascript
// Method 1: Array literal (preferred)
let fruits = ["Apple", "Banana", "Orange"];

// Method 2: Array constructor (rarely used)
let numbers = new Array(1, 2, 3, 4, 5);

// Empty array
let emptyList = [];

// Mixed data types (allowed but generally avoided)
let mixed = ["Ali", 25, true, null, undefined];
```

### Accessing Elements by Index (Zero-Based!)

Arrays use **zero-based indexing**. The first element is at index 0, not index 1.

```
  ARRAY WITH INDICES
  ===================

  let fruits = ["Apple", "Banana", "Orange", "Mango", "Grape"];

  +---------------------------------------------------+
  | Index:  |  0      |  1      |  2      |  3    |  4    |
  +---------+---------+---------+---------+-------+-------+
  | Value:  | "Apple" | "Banana"| "Orange"| "Mango"| "Grape"|
  +---------------------------------------------------+

  fruits[0]  -->  "Apple"    (first element)
  fruits[2]  -->  "Orange"   (third element)
  fruits[4]  -->  "Grape"    (last element)
  fruits[5]  -->  undefined  (does not exist)
```

```javascript
let fruits = ["Apple", "Banana", "Orange", "Mango", "Grape"];

console.log(fruits[0]); // "Apple"
console.log(fruits[2]); // "Orange"
console.log(fruits[4]); // "Grape"
console.log(fruits[5]); // undefined (out of bounds)

// Access the last element dynamically
console.log(fruits[fruits.length - 1]); // "Grape"
```

### Array Length Property

The `length` property tells you how many elements are in the array.

```javascript
let colors = ["Red", "Green", "Blue"];
console.log(colors.length); // 3
```

### Modifying Elements

You can change any element by assigning a new value to its index.

```javascript
let animals = ["Cat", "Dog", "Bird"];

animals[1] = "Fish"; // Replace "Dog" with "Fish"
console.log(animals); // ["Cat", "Fish", "Bird"]

animals[3] = "Horse"; // Add at index 3
console.log(animals); // ["Cat", "Fish", "Bird", "Horse"]
```

---

## 8. Array Methods (Detailed)

### Adding and Removing Elements

#### push() -- Add to End

Adds one or more elements to the **end** of the array. Returns the new length.

```javascript
let fruits = ["Apple", "Banana"];

fruits.push("Orange");
console.log(fruits); // ["Apple", "Banana", "Orange"]

fruits.push("Mango", "Grape"); // Add multiple
console.log(fruits); // ["Apple", "Banana", "Orange", "Mango", "Grape"]

let newLength = fruits.push("Kiwi");
console.log(newLength); // 6
```

#### pop() -- Remove from End

Removes the **last** element from the array. Returns the removed element.

```javascript
let fruits = ["Apple", "Banana", "Orange"];

let removed = fruits.pop();
console.log(removed); // "Orange"
console.log(fruits);  // ["Apple", "Banana"]
```

#### unshift() -- Add to Beginning

Adds one or more elements to the **beginning** of the array. Returns the new length.

```javascript
let fruits = ["Banana", "Orange"];

fruits.unshift("Apple");
console.log(fruits); // ["Apple", "Banana", "Orange"]

fruits.unshift("Mango", "Grape");
console.log(fruits); // ["Mango", "Grape", "Apple", "Banana", "Orange"]
```

#### shift() -- Remove from Beginning

Removes the **first** element from the array. Returns the removed element.

```javascript
let fruits = ["Apple", "Banana", "Orange"];

let removed = fruits.shift();
console.log(removed); // "Apple"
console.log(fruits);  // ["Banana", "Orange"]
```

```
  push / pop / unshift / shift VISUALIZED
  =========================================

                  unshift                       push
                  adds here                     adds here
                     |                             |
                     v                             v
               +---+---+---+---+---+---+---+
               | 0 | 1 | 2 | 3 | 4 | 5 | 6 |
               +---+---+---+---+---+---+---+
                     ^                             ^
                     |                             |
                  shift                          pop
                  removes here                   removes here
```

#### splice() -- Add/Remove at Any Position

`splice(startIndex, deleteCount, item1, item2, ...)`

This is the most versatile array method for adding and removing elements.

```javascript
let fruits = ["Apple", "Banana", "Orange", "Mango"];

// Remove 1 element at index 1
let removed = fruits.splice(1, 1);
console.log(removed); // ["Banana"]
console.log(fruits);  // ["Apple", "Orange", "Mango"]

// Remove 2 elements starting at index 1
fruits.splice(1, 2);
console.log(fruits); // ["Apple"]
```

```javascript
let colors = ["Red", "Blue", "Green"];

// Insert without removing (deleteCount = 0)
colors.splice(1, 0, "Yellow");
console.log(colors); // ["Red", "Yellow", "Blue", "Green"]

// Replace: remove 1 and insert 2
colors.splice(2, 1, "Purple", "Pink");
console.log(colors); // ["Red", "Yellow", "Purple", "Pink", "Green"]
```

---

### Searching

#### indexOf() -- Find Index of Element

Returns the **first** index where the element is found, or **-1** if not found.

```javascript
let fruits = ["Apple", "Banana", "Orange", "Banana"];

console.log(fruits.indexOf("Banana"));  // 1 (first occurrence)
console.log(fruits.indexOf("Grape"));   // -1 (not found)
console.log(fruits.indexOf("Banana", 2)); // 3 (search from index 2)
```

#### includes() -- Check If Element Exists

Returns `true` or `false`.

```javascript
let fruits = ["Apple", "Banana", "Orange"];

console.log(fruits.includes("Banana")); // true
console.log(fruits.includes("Grape"));  // false
```

#### find() -- Find First Matching Element

Returns the **first element** that satisfies the condition, or `undefined` if none match. Takes a callback function.

```javascript
let numbers = [5, 12, 8, 130, 44];

let found = numbers.find(num => num > 10);
console.log(found); // 12 (first number greater than 10)

let notFound = numbers.find(num => num > 200);
console.log(notFound); // undefined
```

```javascript
// More practical: finding an object in an array (preview of objects)
let students = [
  { name: "Ali", grade: 85 },
  { name: "Sara", grade: 92 },
  { name: "Ahmed", grade: 78 }
];

let topStudent = students.find(student => student.grade > 90);
console.log(topStudent); // { name: "Sara", grade: 92 }
```

#### findIndex() -- Find Index of First Match

Like `find()`, but returns the **index** instead of the element. Returns **-1** if not found.

```javascript
let numbers = [5, 12, 8, 130, 44];

let index = numbers.findIndex(num => num > 10);
console.log(index); // 1

let noIndex = numbers.findIndex(num => num > 200);
console.log(noIndex); // -1
```

---

### Transforming

#### map() -- Transform Each Element

Creates a **new array** by applying a function to every element. The original array is unchanged.

**This is one of the most important methods for React development.** You will use `map()` constantly to render lists of components.

```javascript
let numbers = [1, 2, 3, 4, 5];

let doubled = numbers.map(num => num * 2);
console.log(doubled); // [2, 4, 6, 8, 10]
console.log(numbers); // [1, 2, 3, 4, 5] (unchanged)
```

```javascript
let names = ["ali", "sara", "ahmed"];

let capitalized = names.map(name => name.charAt(0).toUpperCase() + name.slice(1));
console.log(capitalized); // ["Ali", "Sara", "Ahmed"]
```

```javascript
// Preview: How map() is used in React (you will learn React later)
// const listItems = students.map(student => <li>{student.name}</li>);
```

```
  HOW map() WORKS
  ================

  Original:  [1,    2,    3,    4,    5   ]
              |     |     |     |     |
              v     v     v     v     v
  Function:  x*2   x*2   x*2   x*2   x*2
              |     |     |     |     |
              v     v     v     v     v
  Result:    [2,    4,    6,    8,    10  ]
```

#### filter() -- Keep Elements That Match

Creates a **new array** with only the elements that pass a test (return `true`).

```javascript
let numbers = [1, 2, 3, 4, 5, 6, 7, 8, 9, 10];

let evenNumbers = numbers.filter(num => num % 2 === 0);
console.log(evenNumbers); // [2, 4, 6, 8, 10]

let bigNumbers = numbers.filter(num => num > 5);
console.log(bigNumbers); // [6, 7, 8, 9, 10]
```

```javascript
let students = [
  { name: "Ali", grade: 85 },
  { name: "Sara", grade: 92 },
  { name: "Ahmed", grade: 55 },
  { name: "Fatima", grade: 78 }
];

let passing = students.filter(student => student.grade >= 60);
console.log(passing);
// [{ name: "Ali", grade: 85 }, { name: "Sara", grade: 92 }, { name: "Fatima", grade: 78 }]
```

#### reduce() -- Combine All Elements into One Value

Reduces an array to a **single value** by applying a function to an accumulator and each element.

Syntax: `array.reduce((accumulator, currentValue) => ..., initialValue)`

```javascript
let numbers = [1, 2, 3, 4, 5];

let sum = numbers.reduce((accumulator, current) => accumulator + current, 0);
console.log(sum); // 15
```

```
  HOW reduce() WORKS (summing [1, 2, 3, 4, 5])
  ==============================================

  Initial value: 0

  Step 1: accumulator = 0, current = 1  -->  0 + 1 = 1
  Step 2: accumulator = 1, current = 2  -->  1 + 2 = 3
  Step 3: accumulator = 3, current = 3  -->  3 + 3 = 6
  Step 4: accumulator = 6, current = 4  -->  6 + 4 = 10
  Step 5: accumulator = 10, current = 5 --> 10 + 5 = 15

  Final result: 15
```

```javascript
// Find the maximum value
let numbers = [23, 65, 12, 89, 34];

let max = numbers.reduce((max, current) => current > max ? current : max, numbers[0]);
console.log(max); // 89
```

```javascript
// Calculate total price of items in a cart
let cart = [
  { item: "Shirt", price: 1500 },
  { item: "Pants", price: 2500 },
  { item: "Shoes", price: 4000 }
];

let total = cart.reduce((sum, product) => sum + product.price, 0);
console.log(total); // 8000
```

#### sort() -- Sort Elements

Sorts elements **in place** (modifies the original array). By default, it sorts as strings.

```javascript
let fruits = ["Banana", "Apple", "Orange", "Mango"];
fruits.sort();
console.log(fruits); // ["Apple", "Banana", "Mango", "Orange"]
```

**Warning:** Default sort converts numbers to strings, which gives unexpected results.

```javascript
let numbers = [10, 5, 40, 25, 100];
numbers.sort();
console.log(numbers); // [10, 100, 25, 40, 5] -- WRONG! String comparison

// Correct way: provide a compare function
numbers.sort((a, b) => a - b); // Ascending
console.log(numbers); // [5, 10, 25, 40, 100]

numbers.sort((a, b) => b - a); // Descending
console.log(numbers); // [100, 40, 25, 10, 5]
```

#### reverse() -- Reverse the Array

Reverses the array **in place**.

```javascript
let letters = ["A", "B", "C", "D"];
letters.reverse();
console.log(letters); // ["D", "C", "B", "A"]
```

---

### Other Important Methods

#### forEach() -- Loop Through Elements

Executes a function for each element. Unlike `map()`, it does **not** return a new array. Use it for side effects (like logging).

```javascript
let fruits = ["Apple", "Banana", "Orange"];

fruits.forEach((fruit, index) => {
  console.log(index + ": " + fruit);
});
// 0: Apple
// 1: Banana
// 2: Orange
```

| Feature        | forEach()                   | map()                              |
|----------------|-----------------------------|------------------------------------|
| Returns        | `undefined`                 | A new array                        |
| Use for        | Side effects (logging, DOM) | Transforming data                  |
| Chainable?     | No                          | Yes                                |

#### concat() -- Merge Arrays

Creates a **new array** by merging two or more arrays.

```javascript
let arr1 = [1, 2, 3];
let arr2 = [4, 5, 6];
let arr3 = [7, 8, 9];

let merged = arr1.concat(arr2);
console.log(merged); // [1, 2, 3, 4, 5, 6]

let allMerged = arr1.concat(arr2, arr3);
console.log(allMerged); // [1, 2, 3, 4, 5, 6, 7, 8, 9]
```

#### slice() -- Extract a Portion

Returns a **new array** containing a portion of the original. Does not modify the original.

Syntax: `array.slice(startIndex, endIndex)` -- `endIndex` is **not included**.

```javascript
let fruits = ["Apple", "Banana", "Orange", "Mango", "Grape"];

let citrus = fruits.slice(1, 3);
console.log(citrus); // ["Banana", "Orange"] (index 1 and 2, NOT 3)

let lastTwo = fruits.slice(-2);
console.log(lastTwo); // ["Mango", "Grape"]

let copy = fruits.slice(); // Copy the entire array
console.log(copy); // ["Apple", "Banana", "Orange", "Mango", "Grape"]
```

**Do not confuse `slice()` with `splice()`:**

| Feature     | slice()                        | splice()                        |
|-------------|--------------------------------|---------------------------------|
| Modifies?   | No (returns new array)         | Yes (modifies original)         |
| Purpose     | Extract a portion              | Add/remove elements             |
| Returns     | New array with extracted items | Array of removed items          |

#### join() -- Array to String

Joins all elements into a single string, separated by a specified separator.

```javascript
let words = ["Hello", "World", "from", "JavaScript"];

console.log(words.join(" "));   // "Hello World from JavaScript"
console.log(words.join(", "));  // "Hello, World, from, JavaScript"
console.log(words.join("-"));   // "Hello-World-from-JavaScript"
console.log(words.join(""));    // "HelloWorldfromJavaScript"
```

#### flat() -- Flatten Nested Arrays

Creates a new array with all sub-array elements concatenated into it.

```javascript
let nested = [1, [2, 3], [4, [5, 6]]];

console.log(nested.flat());    // [1, 2, 3, 4, [5, 6]] (1 level deep, default)
console.log(nested.flat(2));   // [1, 2, 3, 4, 5, 6]   (2 levels deep)
console.log(nested.flat(Infinity)); // [1, 2, 3, 4, 5, 6] (all levels)
```

#### Array.isArray() -- Check If Something Is an Array

Returns `true` if the value is an array, `false` otherwise. This is a static method called on the `Array` constructor, not on an instance.

```javascript
console.log(Array.isArray([1, 2, 3]));    // true
console.log(Array.isArray("hello"));       // false
console.log(Array.isArray({ a: 1 }));      // false
console.log(Array.isArray(undefined));     // false
```

You might wonder why we need this when we have `typeof`. The problem is that `typeof` returns `"object"` for arrays, which is not helpful.

```javascript
console.log(typeof [1, 2, 3]);    // "object" (not useful!)
console.log(Array.isArray([1, 2, 3])); // true (this is what you want)
```

---

## 9. Destructuring Arrays (ES6)

Destructuring lets you unpack values from arrays into individual variables in a single, clean statement.

### Basic Destructuring

```javascript
// Without destructuring
let colors = ["Red", "Green", "Blue"];
let first = colors[0];
let second = colors[1];
let third = colors[2];

// With destructuring
let [red, green, blue] = ["Red", "Green", "Blue"];
console.log(red);   // "Red"
console.log(green); // "Green"
console.log(blue);  // "Blue"
```

### Skipping Values

Use commas to skip values you do not need.

```javascript
let numbers = [1, 2, 3, 4, 5];

let [first, , third] = numbers;
console.log(first); // 1
console.log(third); // 3

let [, , , fourth] = numbers;
console.log(fourth); // 4
```

### The Rest Operator (...)

The rest operator collects the remaining elements into a new array.

```javascript
let fruits = ["Apple", "Banana", "Orange", "Mango", "Grape"];

let [first, second, ...remaining] = fruits;
console.log(first);     // "Apple"
console.log(second);    // "Banana"
console.log(remaining); // ["Orange", "Mango", "Grape"]
```

```javascript
// Practical: separating the head from the tail
let scores = [95, 88, 76, 65, 92];

let [highest, ...others] = scores;
console.log(highest); // 95
console.log(others);  // [88, 76, 65, 92]
```

### Swapping Variables

Destructuring makes swapping two variables easy without needing a temporary variable.

```javascript
let a = 1;
let b = 2;

[a, b] = [b, a];

console.log(a); // 2
console.log(b); // 1
```

### Default Values

You can provide default values in case the array does not have enough elements.

```javascript
let [x = 10, y = 20, z = 30] = [1, 2];

console.log(x); // 1  (from array)
console.log(y); // 2  (from array)
console.log(z); // 30 (default, since array has no third element)
```

---

## 10. Spread Operator with Arrays

The spread operator `...` expands an array into individual elements. It looks identical to the rest operator but is used in a different context.

- **Rest**: Collects multiple elements into an array (used in destructuring and function parameters).
- **Spread**: Expands an array into individual elements (used in array literals and function calls).

### Copying Arrays

```javascript
let original = [1, 2, 3];

let copy = [...original];
console.log(copy); // [1, 2, 3]

copy.push(4);
console.log(original); // [1, 2, 3] (unchanged)
console.log(copy);     // [1, 2, 3, 4]
```

**Why not just use `=`?** Because arrays are reference types. Using `=` makes both variables point to the **same** array in memory, so changes to one affect the other.

```javascript
let original = [1, 2, 3];
let notACopy = original; // Both point to the SAME array

notACopy.push(4);
console.log(original); // [1, 2, 3, 4] -- original is also changed!
```

### Merging Arrays

```javascript
let frontend = ["HTML", "CSS", "JavaScript"];
let backend = ["Node.js", "Express", "MongoDB"];

let fullStack = [...frontend, ...backend];
console.log(fullStack);
// ["HTML", "CSS", "JavaScript", "Node.js", "Express", "MongoDB"]
```

```javascript
// Insert elements in between
let start = [1, 2];
let end = [5, 6];

let combined = [...start, 3, 4, ...end];
console.log(combined); // [1, 2, 3, 4, 5, 6]
```

### Spread in Function Calls

```javascript
let numbers = [5, 12, 8, 130, 44];

// Math.max does not accept arrays, but spread expands it
console.log(Math.max(...numbers)); // 130
console.log(Math.min(...numbers)); // 5
```

---

## 11. Summary & Method Cheat Sheet

### Functions Summary

| Concept             | Key Point                                                 |
|---------------------|-----------------------------------------------------------|
| Function Declaration| `function name() {}` -- hoisted, can call before defining |
| Function Expression | `const name = function() {}` -- not hoisted               |
| Arrow Function      | `const name = () => {}` -- concise, no own `this`         |
| Parameters          | Placeholders in function definition                       |
| Arguments           | Actual values passed when calling                         |
| Return              | Sends a value back and stops the function                 |
| Default Parameters  | `function(x = 10)` -- fallback if no argument given       |
| Scope               | Determines where variables are accessible                 |
| Callback            | A function passed as an argument to another function      |

### Array Methods Cheat Sheet

| Method           | Purpose                      | Returns             | Modifies Original? |
|------------------|------------------------------|---------------------|---------------------|
| `push()`         | Add to end                   | New length          | Yes                 |
| `pop()`          | Remove from end              | Removed element     | Yes                 |
| `unshift()`      | Add to beginning             | New length          | Yes                 |
| `shift()`        | Remove from beginning        | Removed element     | Yes                 |
| `splice()`       | Add/remove at position       | Removed elements    | Yes                 |
| `indexOf()`      | Find index of element        | Index or -1         | No                  |
| `includes()`     | Check if element exists      | Boolean             | No                  |
| `find()`         | Find first matching element  | Element or undefined| No                  |
| `findIndex()`    | Find index of first match    | Index or -1         | No                  |
| `map()`          | Transform each element       | New array           | No                  |
| `filter()`       | Keep matching elements       | New array           | No                  |
| `reduce()`       | Combine into single value    | Single value        | No                  |
| `sort()`         | Sort elements                | Sorted array        | Yes                 |
| `reverse()`      | Reverse order                | Reversed array      | Yes                 |
| `forEach()`      | Loop through elements        | `undefined`         | No                  |
| `concat()`       | Merge arrays                 | New array           | No                  |
| `slice()`        | Extract portion              | New array           | No                  |
| `join()`         | Array to string              | String              | No                  |
| `flat()`         | Flatten nested arrays        | New array           | No                  |
| `Array.isArray()`| Check if value is an array   | Boolean             | No                  |

### ES6 Features Covered

| Feature              | Syntax Example                        |
|----------------------|---------------------------------------|
| Arrow Functions      | `const fn = (x) => x * 2;`           |
| Default Parameters   | `function greet(name = "Guest") {}`   |
| Destructuring        | `const [a, b] = [1, 2];`             |
| Rest Operator        | `const [first, ...rest] = arr;`       |
| Spread Operator      | `const copy = [...arr];`              |

---

> **Next Week (Week 12):** Objects, DOM Manipulation, and Events -- where you will learn to work with complex data structures and make your web pages interactive.
