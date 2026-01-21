# Loops in JavaScript

## Introduction

Loops are used to **repeat a block of code multiple times** until a specific condition is met.

In real life, repetition happens everywhere:

* Teacher checks attendance for **each student**
* ATM prints receipt **line by line**
* Gym workout repeats **sets and reps**

In programming, loops help us avoid writing the same code again and again.

---

## Why Loops Are Important

* Reduce code duplication
* Save time and effort
* Work with large data (arrays, records)
* Essential for real-world applications

---

## Types of Loops in JavaScript

1. `for` loop
2. `while` loop
3. `do...while` loop
4. `for...of` loop
5. `for...in` loop

---

## 1. `for` Loop

### Definition

The `for` loop is used when the **number of iterations is known**.

### Syntax

```js
for (initialization; condition; increment/decrement) {
  // code to repeat
}
```

### Real-Life Example

Attendance checking from roll number 1 to 50.

### JavaScript Example

```js
for (let i = 1; i <= 5; i++) {
  console.log("Count:", i);
}
```

---

## 2. `while` Loop

### Definition

The `while` loop runs **as long as the condition is true**.

### Syntax

```js
while (condition) {
  // code
}
```

### Real-Life Example

Keep studying **until exam is over**.

### JavaScript Example

```js
let i = 1;

while (i <= 5) {
  console.log(i);
  i++;
}
```

---

## 3. `do...while` Loop

### Definition

The `do...while` loop executes the code **at least once**, even if the condition is false.

### Syntax

```js
do {
  // code
} while (condition);
```

### Real-Life Example

ATM shows menu **at least once**, even if card is invalid.

### JavaScript Example

```js
let num = 6;

do {
  console.log(num);
  num++;
} while (num <= 5);
```

---

## 4. `for...of` Loop

### Definition

Used to iterate over **iterable objects** like arrays and strings.

### Syntax

```js
for (let item of iterable) {
  // code
}
```

### Real-Life Example

Checking each item in a shopping cart.

### JavaScript Example

```js
let fruits = ["Apple", "Banana", "Mango"];

for (let fruit of fruits) {
  console.log(fruit);
}
```

---

## 5. `for...in` Loop

### Definition

Used to iterate over **object properties**.

### Syntax

```js
for (let key in object) {
  // code
}
```

### Real-Life Example

Checking details on a student form.

### JavaScript Example

```js
let student = {
  name: "Fahad",
  age: 22,
  course: "JavaScript"
};

for (let key in student) {
  console.log(key + ": " + student[key]);
}
```

---

## Loop Control Statements

### `break`

Stops the loop immediately.

```js
for (let i = 1; i <= 10; i++) {
  if (i === 5) break;
  console.log(i);
}
```

### `continue`

Skips the current iteration.

```js
for (let i = 1; i <= 5; i++) {
  if (i === 3) continue;
  console.log(i);
}
```

---

## Common Loop Use Cases

* Print numbers
* Work with arrays
* Search data
* Calculations (sum, average)

### Example: Sum of Numbers

```js
let sum = 0;

for (let i = 1; i <= 5; i++) {
  sum += i;
}

console.log("Sum:", sum);
```

---

## Practice Questions

### Basic Level

1. Print numbers from 1 to 10 using `for` loop.
2. Print even numbers between 1 and 20.
3. Print multiplication table of 5.

### Intermediate Level

4. Calculate sum of array elements.
5. Count total vowels in a string.
6. Reverse an array using a loop.

### Advanced Level

7. Find largest number in an array.
8. Create a simple number guessing loop.
9. Print star pattern using nested loops.

---

## Mini Assignment

Create a JavaScript program that:

* Stores marks of 5 students in an array
* Calculates average marks
* Displays result using loop

---

## Key Takeaways

* Loops repeat code efficiently
* `for` loop is best when count is known
* `while` loop depends on condition
* `do...while` runs at least once
* `for...of` for arrays
* `for...in` for objects

---

Happy Coding 🚀
