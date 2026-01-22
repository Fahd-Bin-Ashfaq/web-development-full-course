# Arrays in JavaScript

## Introduction

An **array** is a data structure used to store **multiple values in a single variable**. Arrays help us manage lists of data efficiently.

### Real-Life Examples

* List of students in a class
* Products in a shopping cart
* Marks of students

---

## Why Arrays Are Important

* Store multiple values
* Easy data management
* Widely used in web & backend development
* Core topic for interviews

---

## 1. Creating Arrays

```js
let numbers = [1, 2, 3, 4, 5];
let fruits = ["Apple", "Banana", "Mango"];
```

---

## 2. Accessing Array Elements

```js
let fruits = ["Apple", "Banana", "Mango"];
console.log(fruits[0]); // Apple
console.log(fruits[2]); // Mango
```

📌 Array index always starts from **0**.

---

## 3. Modifying Array Elements

```js
let fruits = ["Apple", "Banana", "Mango"];
fruits[1] = "Orange";
```

---

## 4. Array Length

```js
let arr = [10, 20, 30];
console.log(arr.length);
```

---

## 5. Common Array Methods

### push() – Add at end

```js
let arr = [1, 2];
arr.push(3);
```

### pop() – Remove from end

```js
arr.pop();
```

### unshift() – Add at start

```js
arr.unshift(0);
```

### shift() – Remove from start

```js
arr.shift();
```

---

## 6. Looping Through Arrays

### for Loop

```js
let nums = [1, 2, 3];
for (let i = 0; i < nums.length; i++) {
  console.log(nums[i]);
}
```

### for...of Loop

```js
for (let num of nums) {
  console.log(num);
}
```

---

## 7. Important Array Methods (Advanced & Must-Know)

### map()

Transforms each element.

```js
let nums = [1, 2, 3];
let squares = nums.map(n => n * n);
```

---

### filter()

Filters elements based on condition.

```js
let even = nums.filter(n => n % 2 === 0);
```

---

### reduce()

Reduces array to a single value.

```js
let sum = nums.reduce((total, n) => total + n, 0);
```

---

## 8. Destructuring Arrays

```js
let [a, b] = [10, 20];
```

---

## 9. Spread Operator

```js
let arr1 = [1, 2];
let arr2 = [...arr1, 3, 4];
```

---

## 10. Array Best Practices

* Use array methods instead of manual loops
* Avoid modifying original array unnecessarily
* Use meaningful variable names

---

## Practice Questions

### Basic Level

1. Create an array of 5 numbers and print them
2. Find the length of an array
3. Add and remove elements using `push` and `pop`

### Intermediate Level

4. Print all even numbers from an array
5. Find sum of array elements
6. Reverse an array

### Advanced Level

7. Find maximum number in an array
8. Use `map` to square all elements
9. Use `filter` to get numbers greater than 10
10. Use `reduce` to calculate total marks

---

## Mini Assignment

Create a program that:

* Stores marks of students in an array
* Calculates total & average marks
* Finds highest and lowest marks

---

## Key Takeaways

* Arrays store multiple values
* Index starts from 0
* `map`, `filter`, `reduce` are essential
* Arrays are used everywhere in JS

---

Happy Coding 🚀
