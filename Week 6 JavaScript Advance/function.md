# Functions in JavaScript

## Introduction

A **function** is a reusable block of code that performs a specific task. Functions help make code **clean, modular, reusable, and easy to maintain**.

Real-life analogy:

* A **calculator button** → press it anytime, same task runs again.
* A **recipe** → same steps, different ingredients.

---

## Why Functions Are Important

* Avoid code repetition
* Improve readability
* Make debugging easier
* Core concept for interviews & real projects

---

## 1. Function Declaration

### Definition

A function declared using the `function` keyword.

### Syntax

```js
function functionName() {
  // code to execute
}
```

### Example

```js
function greet() {
  console.log("Hello World");
}

greet();
```

---

## 2. Function Parameters & Arguments

### Definition

* **Parameters** → variables defined in function
* **Arguments** → values passed to function

### Example

```js
function greetUser(name) {
  console.log("Hello " + name);
}

greetUser("Fahad");
```

---

## 3. Return Values

### Definition

The `return` statement sends a value back from the function.

### Example

```js
function add(a, b) {
  return a + b;
}

let result = add(4, 6);
console.log(result);
```

📌 **Best Practice:** A function should return a value instead of printing whenever possible.

---

## 4. Function Expressions

### Definition

Functions stored inside variables.

```js
const multiply = function (a, b) {
  return a * b;
};
```

---

## 5. Arrow Functions

### Definition

Shorter syntax for functions (ES6).

```js
const square = n => n * n;
```

📌 Arrow functions do **not** have their own `this`.

---

## 6. Function Scope

### Definition

Variables declared inside a function are **only accessible within that function**.

```js
function demo() {
  let x = 10;
  console.log(x);
}
```

❌ This will cause error:

```js
console.log(x);
```

---

## 7. Default Parameters

```js
function greet(name = "Guest") {
  return "Hello " + name;
}
```

---

## 8. Rest Parameters

Used when number of arguments is unknown.

```js
function sum(...numbers) {
  return numbers.reduce((total, n) => total + n, 0);
}
```

---

## 9. Callback Functions

### Definition

A function passed as an argument to another function.

```js
function process(callback) {
  callback();
}

process(() => console.log("Callback executed"));
```

---

## 10. Higher-Order Functions

Functions that:

* accept functions as arguments OR
* return functions

```js
function calculate(a, b, operation) {
  return operation(a, b);
}
```

---

## 11. Closures (Important)

A function that **remembers variables from its outer scope**.

```js
function counter() {
  let count = 0;
  return function () {
    count++;
    return count;
  };
}
```

---

## 12. Best Practices

* Use meaningful function names
* One function = one responsibility
* Avoid global variables
* Keep functions small
* Prefer `return` over `console.log`

---

## Practice Questions

### Basic

1. Write a function to check even or odd number
2. Write a function to calculate area of a circle

### Intermediate

3. Create a function to find maximum number in an array
4. Write a callback-based function

### Advanced

5. Create a counter using closure
6. Write a function using rest parameters

---

## Mini Assignment

Create utility functions for:

* Email validation
* Password strength check
* Calculator (add, subtract, multiply, divide)

---

## Key Takeaways

* Functions are building blocks of JavaScript
* Parameters make functions flexible
* Return values enable reuse
* Closures & callbacks are interview favorites

---

Happy Coding 🚀
