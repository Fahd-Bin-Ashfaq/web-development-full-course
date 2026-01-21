# Conditional Statements in JavaScript

## Introduction

Conditional statements are used to **make decisions in a program**. They allow the program to execute different blocks of code based on whether a condition is **true** or **false**.

In real life, we use conditions all the time:

* **If** it rains, **take an umbrella**.
* **If** marks are above 50, **pass**, otherwise **fail**.

JavaScript works the same way.

---

## Why Conditional Statements Matter

* Control the flow of a program
* Add logic and decision-making
* Build real-world applications (login systems, grading systems, payments, etc.)

---

## Types of Conditional Statements in JavaScript

1. `if` statement
2. `if...else` statement
3. `if...else if...else` statement
4. `switch` statement
5. Ternary Operator (`? :`)

---

## 1. `if` Statement

### Definition

The `if` statement executes a block of code **only if the condition is true**.

### Syntax

```js
if (condition) {
  // code to run if condition is true
}
```

### Real-Life Example

If a person is **18 or older**, they can vote.

### JavaScript Example

```js
let age = 20;

if (age >= 18) {
  console.log("You are eligible to vote");
}
```

---

## 2. `if...else` Statement

### Definition

The `else` block runs when the `if` condition is **false**.

### Syntax

```js
if (condition) {
  // runs if condition is true
} else {
  // runs if condition is false
}
```

### Real-Life Example

If balance is sufficient, payment succeeds; otherwise, payment fails.

### JavaScript Example

```js
let balance = 500;
let price = 700;

if (balance >= price) {
  console.log("Payment Successful");
} else {
  console.log("Insufficient Balance");
}
```

---

## 3. `if...else if...else` Statement

### Definition

Used when **multiple conditions** need to be checked.

### Syntax

```js
if (condition1) {
  // code
} else if (condition2) {
  // code
} else {
  // default code
}
```

### Real-Life Example

Grading system based on marks.

### JavaScript Example

```js
let marks = 78;

if (marks >= 85) {
  console.log("Grade A");
} else if (marks >= 70) {
  console.log("Grade B");
} else if (marks >= 50) {
  console.log("Grade C");
} else {
  console.log("Fail");
}
```

---

## 4. `switch` Statement

### Definition

The `switch` statement is used when you want to compare **one value** with multiple possible cases.

### Syntax

```js
switch (expression) {
  case value1:
    // code
    break;
  case value2:
    // code
    break;
  default:
    // code
}
```

### Real-Life Example

Selecting a day of the week.

### JavaScript Example

```js
let day = 3;

switch (day) {
  case 1:
    console.log("Monday");
    break;
  case 2:
    console.log("Tuesday");
    break;
  case 3:
    console.log("Wednesday");
    break;
  default:
    console.log("Invalid Day");
}
```

---

## 5. Ternary Operator (`? :`)

### Definition

A **short form of if...else** used for simple conditions.

### Syntax

```js
condition ? expressionIfTrue : expressionIfFalse;
```

### Real-Life Example

Check pass or fail in one line.

### JavaScript Example

```js
let score = 45;
let result = score >= 50 ? "Pass" : "Fail";

console.log(result);
```

---

## Comparison Operators Used in Conditions

| Operator | Meaning                     |
| -------- | --------------------------- |
| `==`     | Equal to                    |
| `===`    | Strict equal (value + type) |
| `!=`     | Not equal                   |
| `>`      | Greater than                |
| `<`      | Less than                   |
| `>=`     | Greater than or equal       |
| `<=`     | Less than or equal          |

---

## Logical Operators

| Operator | Meaning |   |    |
| -------- | ------- | - | -- |
| `&&`     | AND     |   |    |
| `        |         | ` | OR |
| `!`      | NOT     |   |    |

### Example

```js
let age = 22;
let hasCNIC = true;

if (age >= 18 && hasCNIC) {
  console.log("Eligible for registration");
}
```

---

## Practice Questions

### Basic Level

1. Write a program to check if a number is positive or negative.
2. Check whether a person is eligible to vote.
3. Write a program to check even or odd number.

### Intermediate Level

4. Create a grading system using `if...else if...else`.
5. Use `switch` to display the name of a month.
6. Write a program to check login access using username and password.

### Advanced Level

7. Check whether a year is a leap year.
8. Create a simple ATM withdrawal condition.
9. Use ternary operator to check pass or fail.

---

## Mini Assignment

Create a **JavaScript program** that:

* Takes user age
* Checks eligibility for:

  * School (age < 18)
  * University (18–25)
  * Job (25+)

---

## Key Takeaways

* Conditional statements control decision-making
* Use `if` for simple conditions
* Use `else if` for multiple conditions
* Use `switch` for fixed value comparisons
* Use ternary operator for short logic

---

Happy Coding 🚀
