# Operators in Programming (JavaScript)

## 📌 What is an Operator?

An **operator** is a special symbol used to **perform an action on values (called operands)**.

In simple words:
👉 **Operators tell the computer what to do with data.**

**Example:**

```js
let sum = 10 + 5;
```

Here, `+` is an operator that adds two values.

---

## 🎯 Why Do We Use Operators?

Operators are used to:

* Perform mathematical calculations
* Assign values to variables
* Compare values
* Make decisions in programs
* Combine multiple conditions

> Without operators, programming logic cannot exist.

---

## 🧩 Types of Operators (Easy + Real-Life Examples)

---

## 1️⃣ Arithmetic Operators

Used for **mathematical calculations**.

| Operator | Purpose        |
| -------- | -------------- |
| `+`      | Addition       |
| `-`      | Subtraction    |
| `*`      | Multiplication |
| `/`      | Division       |
| `%`      | Remainder      |

**JavaScript Example:**

```js
let totalPrice = 500 + 200;
```

**Real-Life Example:**
Adding prices of items while shopping.

---

## 2️⃣ Assignment Operators

Used to **assign or update values**.

| Operator | Purpose             |
| -------- | ------------------- |
| `=`      | Assign value        |
| `+=`     | Add and assign      |
| `-=`     | Subtract and assign |

**JavaScript Example:**

```js
let balance = 1000;
balance += 500;
```

**Real-Life Example:**
Updating your bank balance after receiving salary.

---

## 3️⃣ Comparison Operators

Used to **compare two values**.
Result is always **true or false**.

| Operator | Purpose               |
| -------- | --------------------- |
| `==`     | Equal to              |
| `===`    | Equal value and type  |
| `!=`     | Not equal             |
| `>`      | Greater than          |
| `<`      | Less than             |
| `>=`     | Greater than or equal |
| `<=`     | Less than or equal    |

**JavaScript Example:**

```js
let age = 20;
age >= 18;
```

**Real-Life Example:**
Checking if a person is eligible to vote.

---

## 4️⃣ Logical Operators

Used to **combine multiple conditions**.

| Operator | Purpose |   |    |
| -------- | ------- | - | -- |
| `&&`     | AND     |   |    |
| `        |         | ` | OR |
| `!`      | NOT     |   |    |

**JavaScript Example:**

```js
let hasID = true;
let age = 19;

age >= 18 && hasID;
```

**Real-Life Example:**
You can enter an exam hall only if you have an ID card **AND** admit slip.

---

## 5️⃣ Unary Operators

Operate on **a single value**.

| Operator | Purpose             |
| -------- | ------------------- |
| `++`     | Increase value by 1 |
| `--`     | Decrease value by 1 |

**JavaScript Example:**

```js
let score = 5;
score++;
```

**Real-Life Example:**
Increasing score by one point in a game.

---

## 6️⃣ Ternary Operator

Used as a **short form of if-else**.

**Syntax:**

```js
condition ? valueIfTrue : valueIfFalse;
```

**JavaScript Example:**

```js
let age = 20;
let result = age >= 18 ? "Adult" : "Minor";
```

**Real-Life Example:**
Deciding ticket price: Adult or Child.

---

## ✅ Summary

* Operators perform actions on data
* They are essential for logic and decision-making
* JavaScript provides different types of operators
* Operators are used in almost every program

---

## 📝 Practice Questions

1. What is an operator in JavaScript? Explain in your own words with one example.
2. Write a JavaScript statement using an **arithmetic operator** to calculate the total price of two items.
3. What is the difference between `==` and `===`? Write one example for each.
4. Write a condition using **logical operators** to check if a user can vote (age ≥ 18 and has CNIC).
5. Use a **ternary operator** to check whether a number is even or odd.

---

## 💻 Practical Coding Questions (Using Operators)

1. **Area of a Circle**
   Write a JavaScript program to calculate the area of a circle using the formula:

```
area = π × r × r
```

Use arithmetic operators.

2. **Area of a Square**
   Write a program to calculate the area of a square.

```
area = side × side
```

3. **Simple Calculator**
   Write a program that takes two numbers and calculates:

* Addition
* Subtraction
* Multiplication
* Division

4. **Even or Odd Checker**
   Write a program to check whether a number is **even or odd** using:

* Modulus operator `%`
* Ternary operator

5. **Student Pass or Fail**
   Write a program that checks if a student has passed.

* Marks ≥ 50 → Pass
* Marks < 50 → Fail
  Use comparison and ternary operators.

---

📘 **Tip for Students:**
Practice operators daily by solving small problems. The more you use them, the easier programming becomes.
