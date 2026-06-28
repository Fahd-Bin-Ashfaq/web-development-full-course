# Week 11: Functions & Arrays - Practice Questions

**Course:** MERN Stack Web Development  
**Total Questions:** 48 (15 MCQs + 8 Short Answer + 10 Output Prediction + 15 Coding Exercises)

---

## Section A: Multiple Choice Questions (15 Questions)

**Instructions:** Choose the correct answer from the given options.

---

**Q1.** What is the key difference between a function declaration and a function expression?

A) Function declarations cannot accept parameters  
B) Function expressions are hoisted, but function declarations are not  
C) Function declarations are hoisted, but function expressions are not  
D) There is no difference between them  

<details>
<summary>Answer</summary>

**C) Function declarations are hoisted, but function expressions are not.**

Function declarations are fully hoisted, meaning they can be called before they appear in the code. Function expressions are not hoisted in the same way; the variable may be hoisted, but it remains `undefined` until the assignment is executed.
</details>

---

**Q2.** What will the following code output?

```js
const greet = (name = "World") => `Hello, ${name}!`;
console.log(greet());
```

A) `Hello, undefined!`  
B) `Hello, World!`  
C) `Hello, !`  
D) `ReferenceError`  

<details>
<summary>Answer</summary>

**B) `Hello, World!`**

When no argument is passed, the default parameter value `"World"` is used.
</details>

---

**Q3.** Which of the following is NOT a valid way to declare a function in JavaScript?

A) `function add(a, b) { return a + b; }`  
B) `const add = function(a, b) { return a + b; };`  
C) `const add = (a, b) => a + b;`  
D) `function = add(a, b) { return a + b; };`  

<details>
<summary>Answer</summary>

**D) `function = add(a, b) { return a + b; };`**

This is invalid syntax. The correct forms are function declarations (A), function expressions (B), and arrow functions (C).
</details>

---

**Q4.** What does the `push()` method return?

A) The element that was added  
B) The new length of the array  
C) The modified array  
D) `undefined`  

<details>
<summary>Answer</summary>

**B) The new length of the array.**

`push()` adds one or more elements to the end of an array and returns the new length of the array.
</details>

---

**Q5.** What is the output of the following code?

```js
let x = 10;
function test() {
  console.log(x);
  let x = 20;
}
test();
```

A) `10`  
B) `20`  
C) `undefined`  
D) `ReferenceError`  

<details>
<summary>Answer</summary>

**D) `ReferenceError`**

The `let` declaration inside the function creates a block-scoped variable `x`. Due to the temporal dead zone, accessing `x` before the `let` declaration throws a `ReferenceError`.
</details>

---

**Q6.** Which array method does NOT modify the original array?

A) `push()`  
B) `splice()`  
C) `slice()`  
D) `pop()`  

<details>
<summary>Answer</summary>

**C) `slice()`**

`slice()` returns a shallow copy of a portion of an array without modifying the original. `push()`, `splice()`, and `pop()` all mutate the original array.
</details>

---

**Q7.** What does `map()` return?

A) `undefined`  
B) The original array, modified  
C) A new array with the results of calling the provided function on every element  
D) A single accumulated value  

<details>
<summary>Answer</summary>

**C) A new array with the results of calling the provided function on every element.**

`map()` creates and returns a new array populated with the results of the callback function applied to each element. It does not modify the original array.
</details>

---

**Q8.** What is the output of the following code?

```js
const nums = [1, 2, 3, 4, 5];
const result = nums.filter(n => n % 2 === 0);
console.log(result);
```

A) `[1, 3, 5]`  
B) `[2, 4]`  
C) `[false, true, false, true, false]`  
D) `5`  

<details>
<summary>Answer</summary>

**B) `[2, 4]`**

`filter()` creates a new array containing only the elements for which the callback returns a truthy value. Here, only `2` and `4` satisfy `n % 2 === 0`.
</details>

---

**Q9.** What does the `reduce()` method do?

A) Removes elements from an array  
B) Reduces the size of the array by half  
C) Executes a reducer function on each element, resulting in a single output value  
D) Filters out elements that do not meet a condition  

<details>
<summary>Answer</summary>

**C) Executes a reducer function on each element, resulting in a single output value.**

`reduce()` applies a function against an accumulator and each element in the array (from left to right) to reduce it to a single value.
</details>

---

**Q10.** What does `indexOf()` return when the element is not found in the array?

A) `0`  
B) `null`  
C) `-1`  
D) `undefined`  

<details>
<summary>Answer</summary>

**C) `-1`**

`indexOf()` returns the first index at which a given element is found. If the element is not present, it returns `-1`.
</details>

---

**Q11.** What is the output of the following code?

```js
const [a, , b] = [1, 2, 3, 4];
console.log(a, b);
```

A) `1 2`  
B) `1 3`  
C) `1 4`  
D) `2 3`  

<details>
<summary>Answer</summary>

**B) `1 3`**

Array destructuring assigns the first element to `a`. The comma without a variable name skips the second element. The third element is assigned to `b`.
</details>

---

**Q12.** What does the spread operator (`...`) do when used with arrays?

A) Merges all arrays into a single string  
B) Expands an iterable into individual elements  
C) Removes duplicate values from an array  
D) Reverses the order of elements  

<details>
<summary>Answer</summary>

**B) Expands an iterable into individual elements.**

The spread operator (`...`) unpacks elements of an iterable (such as an array) into individual elements. It is commonly used for copying arrays, merging arrays, and passing array elements as function arguments.
</details>

---

**Q13.** What is the difference between `forEach()` and `map()`?

A) `forEach()` returns a new array; `map()` does not  
B) `map()` returns a new array; `forEach()` returns `undefined`  
C) Both return new arrays  
D) Both return `undefined`  

<details>
<summary>Answer</summary>

**B) `map()` returns a new array; `forEach()` returns `undefined`.**

`map()` creates and returns a new array with the results of the callback. `forEach()` simply executes the callback for each element and always returns `undefined`.
</details>

---

**Q14.** Which method checks whether an array contains a specific value and returns a boolean?

A) `indexOf()`  
B) `find()`  
C) `includes()`  
D) `some()`  

<details>
<summary>Answer</summary>

**C) `includes()`**

`includes()` determines whether an array includes a certain value and returns `true` or `false`. While `indexOf()` can serve a similar purpose, it returns an index (or `-1`), not a boolean.
</details>

---

**Q15.** What is the scope of a variable declared with `let` inside a `for` loop?

A) Global scope  
B) Function scope  
C) Block scope (limited to the loop body)  
D) Module scope  

<details>
<summary>Answer</summary>

**C) Block scope (limited to the loop body).**

Variables declared with `let` are block-scoped, meaning they are only accessible within the block (curly braces) in which they are defined. Inside a `for` loop, the variable exists only within that loop's block.
</details>

---

## Section B: Short Answer Questions (8 Questions)

**Instructions:** Answer the following questions in your own words. Aim for clarity and conciseness.

---

**Q1.** What is the difference between a function declaration and a function expression? Provide an example of each.

<details>
<summary>Answer</summary>

A **function declaration** uses the `function` keyword followed by a name and is hoisted to the top of its scope, meaning it can be called before it appears in the code.

```js
function add(a, b) {
  return a + b;
}
```

A **function expression** assigns a function (named or anonymous) to a variable. It is not hoisted in the same way; the variable is hoisted but remains `undefined` until the line of assignment is executed.

```js
const add = function(a, b) {
  return a + b;
};
```

The main practical difference is **hoisting**: function declarations can be invoked before their definition in the code, while function expressions cannot.
</details>

---

**Q2.** What is hoisting in JavaScript? How does it behave differently for `var`, `let`, and `const`?

<details>
<summary>Answer</summary>

**Hoisting** is JavaScript's behavior of moving declarations to the top of their scope during the compilation phase, before the code is executed.

- **`var`**: The declaration is hoisted and initialized with `undefined`. You can reference the variable before its declaration line, but its value will be `undefined`.
- **`let` and `const`**: The declarations are hoisted but are NOT initialized. They remain in a **temporal dead zone (TDZ)** from the start of the block until the declaration is encountered. Accessing them before declaration throws a `ReferenceError`.
- **Function declarations**: Are fully hoisted, including the function body, so they can be called before they appear in the code.
- **Function expressions**: Follow the hoisting rules of the variable keyword used (`var`, `let`, or `const`).
</details>

---

**Q3.** What does `map()` return compared to `forEach()`? When would you use one over the other?

<details>
<summary>Answer</summary>

- **`map()`** returns a **new array** containing the results of applying the callback function to each element of the original array. The original array is not modified.
- **`forEach()`** returns **`undefined`**. It simply executes the callback function once for each array element as a side effect.

**When to use `map()`:** When you need to transform each element and collect the results into a new array (e.g., doubling numbers, extracting properties).

**When to use `forEach()`:** When you want to perform an action for each element without needing a new array (e.g., logging values, updating external state, making API calls).

```js
const nums = [1, 2, 3];

// map: returns a new array
const doubled = nums.map(n => n * 2); // [2, 4, 6]

// forEach: returns undefined
nums.forEach(n => console.log(n)); // logs 1, 2, 3
```
</details>

---

**Q4.** Explain the scope chain in JavaScript. How does the JavaScript engine resolve variable references?

<details>
<summary>Answer</summary>

The **scope chain** is the mechanism JavaScript uses to resolve variable references. When a variable is accessed, the engine looks for it in the following order:

1. **Local scope**: The engine first checks the current function or block scope.
2. **Outer scope(s)**: If not found locally, it moves outward to the enclosing function's scope.
3. **Global scope**: If the variable is not found in any enclosing scope, the engine checks the global scope.
4. **ReferenceError**: If the variable is not found anywhere in the chain, a `ReferenceError` is thrown.

Each function creates its own scope, and inner functions have access to variables in their outer (parent) scopes. This chain of scopes forms the scope chain.

```js
const global = "I am global";

function outer() {
  const outerVar = "I am outer";

  function inner() {
    const innerVar = "I am inner";
    console.log(innerVar);  // Found in local scope
    console.log(outerVar);  // Found in outer scope
    console.log(global);    // Found in global scope
  }

  inner();
}

outer();
```
</details>

---

**Q5.** What is the difference between `splice()` and `slice()`?

<details>
<summary>Answer</summary>

| Feature | `splice()` | `slice()` |
|---|---|---|
| **Mutates original array** | Yes | No |
| **Return value** | Array of removed elements | A shallow copy of a portion of the array |
| **Purpose** | Add, remove, or replace elements | Extract a section of the array |
| **Parameters** | `(startIndex, deleteCount, ...items)` | `(startIndex, endIndex)` |

**`splice()`** modifies the original array by removing, replacing, or adding elements in place:

```js
const arr = [1, 2, 3, 4, 5];
const removed = arr.splice(1, 2); // removes 2 elements starting at index 1
console.log(arr);     // [1, 4, 5]
console.log(removed); // [2, 3]
```

**`slice()`** does not modify the original array. It returns a new array containing a shallow copy from the start index up to (but not including) the end index:

```js
const arr = [1, 2, 3, 4, 5];
const sliced = arr.slice(1, 3);
console.log(arr);    // [1, 2, 3, 4, 5] (unchanged)
console.log(sliced); // [2, 3]
```
</details>

---

**Q6.** What is a callback function? Provide a practical example.

<details>
<summary>Answer</summary>

A **callback function** is a function that is passed as an argument to another function and is invoked (called back) at a later point, either synchronously or asynchronously.

Callbacks allow you to customize the behavior of a function without modifying its internal logic.

**Synchronous callback example:**

```js
function processArray(arr, callback) {
  const result = [];
  for (let i = 0; i < arr.length; i++) {
    result.push(callback(arr[i]));
  }
  return result;
}

const numbers = [1, 2, 3, 4];
const squares = processArray(numbers, function(num) {
  return num * num;
});

console.log(squares); // [1, 4, 9, 16]
```

**Built-in callback example:**

```js
const names = ["Charlie", "Alice", "Bob"];
names.sort((a, b) => a.localeCompare(b));
console.log(names); // ["Alice", "Bob", "Charlie"]
```

In both examples, the function passed as an argument is the callback. The receiving function decides when and how to call it.
</details>

---

**Q7.** What does the `reduce()` method do? Walk through an example step by step.

<details>
<summary>Answer</summary>

The **`reduce()`** method executes a **reducer function** on each element of the array, passing the result of the previous iteration as an accumulator, and ultimately produces a **single output value**.

**Syntax:** `array.reduce((accumulator, currentValue, index, array) => { ... }, initialValue)`

**Step-by-step example:**

```js
const numbers = [1, 2, 3, 4];
const sum = numbers.reduce((acc, curr) => acc + curr, 0);
```

| Iteration | `acc` (Accumulator) | `curr` (Current Value) | Result (`acc + curr`) |
|---|---|---|---|
| 1 | 0 (initial value) | 1 | 1 |
| 2 | 1 | 2 | 3 |
| 3 | 3 | 3 | 6 |
| 4 | 6 | 4 | 10 |

**Final result:** `sum = 10`

`reduce()` is versatile and can be used for summing, counting, grouping, flattening arrays, building objects, and many other accumulation patterns.
</details>

---

**Q8.** What is the difference between global scope, function scope, and block scope in JavaScript?

<details>
<summary>Answer</summary>

**Global Scope:**
- Variables declared outside any function or block are in the global scope.
- They are accessible from anywhere in the code.
- Variables declared with `var` in the global scope become properties of the `window` object (in browsers).

```js
var globalVar = "I am global"; // accessible everywhere
```

**Function Scope:**
- Variables declared inside a function (using `var`, `let`, or `const`) are accessible only within that function.
- `var` is function-scoped, meaning it does not respect block boundaries within a function.

```js
function myFunc() {
  var funcVar = "I am function-scoped";
  console.log(funcVar); // accessible here
}
// console.log(funcVar); // ReferenceError
```

**Block Scope:**
- Variables declared with `let` or `const` inside a block (`{}`) are only accessible within that block.
- Blocks include `if` statements, `for` loops, and any `{}` pair.

```js
if (true) {
  let blockVar = "I am block-scoped";
  console.log(blockVar); // accessible here
}
// console.log(blockVar); // ReferenceError
```

**Key takeaway:** `var` is function-scoped, while `let` and `const` are block-scoped.
</details>

---

## Section C: What Is the Output? (10 Questions)

**Instructions:** Read each code snippet carefully and predict the output. Pay close attention to scope, hoisting, and how array methods work.

---

**Q1.**

```js
var a = 1;
function outer() {
  var a = 2;
  function inner() {
    console.log(a);
  }
  inner();
}
outer();
console.log(a);
```

<details>
<summary>Answer</summary>

**Output:**
```
2
1
```

**Explanation:** Inside `inner()`, the JavaScript engine looks up the scope chain and finds `a = 2` in the `outer()` function scope. The final `console.log(a)` refers to the global `a`, which is `1`.
</details>

---

**Q2.**

```js
const numbers = [10, 20, 30, 40, 50];
const result = numbers.map(n => n / 10).filter(n => n > 2);
console.log(result);
```

<details>
<summary>Answer</summary>

**Output:**
```
[3, 4, 5]
```

**Explanation:** `map(n => n / 10)` transforms the array to `[1, 2, 3, 4, 5]`. Then `filter(n => n > 2)` keeps only elements greater than 2, resulting in `[3, 4, 5]`.
</details>

---

**Q3.**

```js
const add = (a, b) => a + b;
const multiply = (a, b) => a * b;

console.log(add(2, 3));
console.log(multiply(2, 3));
console.log(add(multiply(2, 3), 4));
```

<details>
<summary>Answer</summary>

**Output:**
```
5
6
10
```

**Explanation:** `add(2, 3)` returns `5`. `multiply(2, 3)` returns `6`. `add(multiply(2, 3), 4)` first evaluates `multiply(2, 3)` which is `6`, then `add(6, 4)` returns `10`.
</details>

---

**Q4.**

```js
console.log(sayHello());

function sayHello() {
  return "Hello!";
}

console.log(sayBye());

var sayBye = function() {
  return "Bye!";
};
```

<details>
<summary>Answer</summary>

**Output:**
```
Hello!
TypeError: sayBye is not a function
```

**Explanation:** The function declaration `sayHello` is fully hoisted, so it can be called before its definition. However, `sayBye` is a function expression assigned to a `var` variable. The variable `sayBye` is hoisted and initialized to `undefined`, so calling it as a function throws a `TypeError`.
</details>

---

**Q5.**

```js
const fruits = ["apple", "banana", "cherry"];
const [first, ...rest] = fruits;
console.log(first);
console.log(rest);
console.log(fruits.length);
```

<details>
<summary>Answer</summary>

**Output:**
```
apple
["banana", "cherry"]
3
```

**Explanation:** Destructuring assigns `"apple"` to `first`. The rest operator (`...rest`) collects the remaining elements into a new array `["banana", "cherry"]`. The original array is not modified, so `fruits.length` remains `3`.
</details>

---

**Q6.**

```js
let count = 0;
const arr = [1, 2, 3, 4, 5];

arr.forEach(num => {
  if (num % 2 === 0) {
    count++;
  }
});

console.log(count);
console.log(arr.forEach(n => n * 2));
```

<details>
<summary>Answer</summary>

**Output:**
```
2
undefined
```

**Explanation:** The first `forEach` increments `count` for each even number (2 and 4), so `count` becomes `2`. The second `console.log` prints `undefined` because `forEach()` always returns `undefined`, regardless of what the callback returns.
</details>

---

**Q7.**

```js
function makeCounter() {
  let count = 0;
  return function() {
    count++;
    return count;
  };
}

const counter = makeCounter();
console.log(counter());
console.log(counter());
console.log(counter());
```

<details>
<summary>Answer</summary>

**Output:**
```
1
2
3
```

**Explanation:** `makeCounter()` returns an inner function that forms a closure over the `count` variable. Each call to `counter()` increments and returns the same `count` variable, which persists across calls due to the closure.
</details>

---

**Q8.**

```js
const arr1 = [1, 2, 3];
const arr2 = [4, 5, 6];
const merged = [...arr1, ...arr2];
const copy = [...arr1];

copy.push(99);

console.log(merged);
console.log(arr1);
console.log(copy);
```

<details>
<summary>Answer</summary>

**Output:**
```
[1, 2, 3, 4, 5, 6]
[1, 2, 3]
[1, 2, 3, 99]
```

**Explanation:** The spread operator creates new arrays. `merged` combines both arrays into `[1, 2, 3, 4, 5, 6]`. `copy` is a shallow copy of `arr1`. Pushing `99` to `copy` does not affect `arr1` because they are separate arrays.
</details>

---

**Q9.**

```js
const data = [3, 7, 2, 9, 1, 4];
const result = data
  .filter(n => n > 3)
  .map(n => n * 2)
  .reduce((acc, curr) => acc + curr, 0);

console.log(result);
```

<details>
<summary>Answer</summary>

**Output:**
```
40
```

**Explanation:**
1. `filter(n => n > 3)` produces `[7, 9, 4]`.
2. `map(n => n * 2)` transforms it to `[14, 18, 8]`.
3. `reduce((acc, curr) => acc + curr, 0)` sums the values: `14 + 18 + 8 = 40`.
</details>

---

**Q10.**

```js
const greet = (name, greeting = "Hello") => {
  return `${greeting}, ${name}!`;
};

console.log(greet("Alice"));
console.log(greet("Bob", "Hi"));
console.log(greet("Charlie", undefined));
```

<details>
<summary>Answer</summary>

**Output:**
```
Hello, Alice!
Hi, Bob!
Hello, Charlie!
```

**Explanation:** When `greet("Alice")` is called without a second argument, the default parameter `"Hello"` is used. When `greet("Bob", "Hi")` is called, the provided `"Hi"` overrides the default. When `undefined` is explicitly passed as the second argument, the default parameter is used because JavaScript treats `undefined` as a missing argument.
</details>

---

## Section D: Coding Exercises (15 Tasks)

**Instructions:** Write JavaScript functions or code snippets to solve each task. Focus on using appropriate functions and array methods.

---

**Task 1: Area of a Circle**

Write a function `calculateArea` that takes the radius of a circle as a parameter and returns the area. Use `Math.PI` for the value of pi.

```js
// Example:
// calculateArea(5)  => 78.53981633974483
// calculateArea(10) => 314.1592653589793
```

<details>
<summary>Solution</summary>

```js
function calculateArea(radius) {
  return Math.PI * radius * radius;
}

console.log(calculateArea(5));  // 78.53981633974483
console.log(calculateArea(10)); // 314.1592653589793
```
</details>

---

**Task 2: Prime Number Checker**

Write an arrow function `isPrime` that takes a number and returns `true` if it is a prime number, or `false` otherwise.

```js
// Example:
// isPrime(7)  => true
// isPrime(10) => false
// isPrime(1)  => false
```

<details>
<summary>Solution</summary>

```js
const isPrime = (num) => {
  if (num <= 1) return false;
  if (num <= 3) return true;
  if (num % 2 === 0 || num % 3 === 0) return false;

  for (let i = 5; i * i <= num; i += 6) {
    if (num % i === 0 || num % (i + 2) === 0) return false;
  }

  return true;
};

console.log(isPrime(7));  // true
console.log(isPrime(10)); // false
console.log(isPrime(1));  // false
console.log(isPrime(29)); // true
```
</details>

---

**Task 3: Greeting with Default Parameters**

Write a function `greet` that takes two parameters: `name` and `greeting` (with a default value of `"Hello"`). The function should return a greeting message.

```js
// Example:
// greet("Alice")            => "Hello, Alice! Welcome!"
// greet("Bob", "Hey there") => "Hey there, Bob! Welcome!"
```

<details>
<summary>Solution</summary>

```js
function greet(name, greeting = "Hello") {
  return `${greeting}, ${name}! Welcome!`;
}

console.log(greet("Alice"));            // "Hello, Alice! Welcome!"
console.log(greet("Bob", "Hey there")); // "Hey there, Bob! Welcome!"
console.log(greet("Charlie", "Hi"));    // "Hi, Charlie! Welcome!"
```
</details>

---

**Task 4: Double All Numbers Using map()**

Given an array of numbers, use `map()` to return a new array where every number is doubled.

```js
// Input:  [1, 2, 3, 4, 5]
// Output: [2, 4, 6, 8, 10]
```

<details>
<summary>Solution</summary>

```js
const numbers = [1, 2, 3, 4, 5];
const doubled = numbers.map(num => num * 2);

console.log(doubled); // [2, 4, 6, 8, 10]
```
</details>

---

**Task 5: Filter Even Numbers**

Given an array of numbers, use `filter()` to return a new array containing only the even numbers.

```js
// Input:  [1, 2, 3, 4, 5, 6, 7, 8, 9, 10]
// Output: [2, 4, 6, 8, 10]
```

<details>
<summary>Solution</summary>

```js
const numbers = [1, 2, 3, 4, 5, 6, 7, 8, 9, 10];
const evens = numbers.filter(num => num % 2 === 0);

console.log(evens); // [2, 4, 6, 8, 10]
```
</details>

---

**Task 6: Sum of an Array Using reduce()**

Use `reduce()` to find the sum of all numbers in an array.

```js
// Input:  [10, 20, 30, 40, 50]
// Output: 150
```

<details>
<summary>Solution</summary>

```js
const numbers = [10, 20, 30, 40, 50];
const sum = numbers.reduce((accumulator, current) => accumulator + current, 0);

console.log(sum); // 150
```
</details>

---

**Task 7: Find First High-Scoring Student**

Given an array of student objects, use `find()` to get the first student with a grade greater than 90.

```js
// Input:
// [
//   { name: "Alice", grade: 85 },
//   { name: "Bob", grade: 92 },
//   { name: "Charlie", grade: 95 },
//   { name: "Diana", grade: 78 }
// ]
// Output: { name: "Bob", grade: 92 }
```

<details>
<summary>Solution</summary>

```js
const students = [
  { name: "Alice", grade: 85 },
  { name: "Bob", grade: 92 },
  { name: "Charlie", grade: 95 },
  { name: "Diana", grade: 78 }
];

const topStudent = students.find(student => student.grade > 90);

console.log(topStudent); // { name: "Bob", grade: 92 }
```
</details>

---

**Task 8: Sort Names Alphabetically**

Given an array of names, sort them in alphabetical order.

```js
// Input:  ["Charlie", "Alice", "Bob", "Diana", "Eve"]
// Output: ["Alice", "Bob", "Charlie", "Diana", "Eve"]
```

<details>
<summary>Solution</summary>

```js
const names = ["Charlie", "Alice", "Bob", "Diana", "Eve"];
const sorted = [...names].sort((a, b) => a.localeCompare(b));

console.log(sorted); // ["Alice", "Bob", "Charlie", "Diana", "Eve"]
```

**Note:** Using `[...names].sort()` creates a copy before sorting, preserving the original array. If modifying the original is acceptable, you can call `names.sort()` directly.
</details>

---

**Task 9: Remove Duplicates from an Array**

Write a function `removeDuplicates` that takes an array and returns a new array with all duplicate values removed.

```js
// Input:  [1, 2, 2, 3, 4, 4, 5, 1, 3]
// Output: [1, 2, 3, 4, 5]
```

<details>
<summary>Solution</summary>

```js
function removeDuplicates(arr) {
  return [...new Set(arr)];
}

console.log(removeDuplicates([1, 2, 2, 3, 4, 4, 5, 1, 3])); // [1, 2, 3, 4, 5]
console.log(removeDuplicates(["a", "b", "a", "c", "b"]));    // ["a", "b", "c"]
```

**Alternative approach using `filter()`:**

```js
function removeDuplicates(arr) {
  return arr.filter((item, index) => arr.indexOf(item) === index);
}
```
</details>

---

**Task 10: Flatten a Nested Array**

Write a function `flattenArray` that takes a nested array and returns a single, flat array.

```js
// Input:  [[1, 2], [3, 4], [5, [6, 7]]]
// Output: [1, 2, 3, 4, 5, 6, 7]
```

<details>
<summary>Solution</summary>

```js
function flattenArray(arr) {
  return arr.flat(Infinity);
}

console.log(flattenArray([[1, 2], [3, 4], [5, [6, 7]]])); // [1, 2, 3, 4, 5, 6, 7]
```

**Alternative recursive approach:**

```js
function flattenArray(arr) {
  return arr.reduce((acc, curr) => {
    return acc.concat(Array.isArray(curr) ? flattenArray(curr) : curr);
  }, []);
}
```
</details>

---

**Task 11: Custom forEach Using a Callback**

Write a function `customForEach` that takes an array and a callback function, then applies the callback to each element of the array.

```js
// Example:
// customForEach([1, 2, 3], (num) => console.log(num * 2));
// Output: 2, 4, 6 (each on a new line)
```

<details>
<summary>Solution</summary>

```js
function customForEach(arr, callback) {
  for (let i = 0; i < arr.length; i++) {
    callback(arr[i], i, arr);
  }
}

// Usage
customForEach([1, 2, 3], (num) => console.log(num * 2));
// Output:
// 2
// 4
// 6

customForEach(["a", "b", "c"], (item, index) => {
  console.log(`${index}: ${item}`);
});
// Output:
// 0: a
// 1: b
// 2: c
```
</details>

---

**Task 12: Merge and Sort Two Arrays**

Write a function `mergeAndSort` that takes two arrays of numbers, merges them into one, and returns the result sorted in ascending order.

```js
// Input:  [5, 3, 1], [4, 2, 6]
// Output: [1, 2, 3, 4, 5, 6]
```

<details>
<summary>Solution</summary>

```js
function mergeAndSort(arr1, arr2) {
  return [...arr1, ...arr2].sort((a, b) => a - b);
}

console.log(mergeAndSort([5, 3, 1], [4, 2, 6]));     // [1, 2, 3, 4, 5, 6]
console.log(mergeAndSort([10, 30], [20, 40, 5]));     // [5, 10, 20, 30, 40]
```

**Note:** The comparator `(a, b) => a - b` is essential for numeric sorting. Without it, `sort()` converts elements to strings and sorts lexicographically (e.g., `10` would come before `2`).
</details>

---

**Task 13: Swap Two Variables Using Destructuring**

Use array destructuring to swap the values of two variables without using a temporary variable.

```js
// Before: a = 5, b = 10
// After:  a = 10, b = 5
```

<details>
<summary>Solution</summary>

```js
let a = 5;
let b = 10;

console.log("Before swap:", a, b); // Before swap: 5 10

[a, b] = [b, a];

console.log("After swap:", a, b);  // After swap: 10 5
```

**Explanation:** The right side `[b, a]` creates a temporary array `[10, 5]`. Destructuring then assigns `10` to `a` and `5` to `b`, effectively swapping their values in a single line.
</details>

---

**Task 14: Top 3 Scores**

Write a function `getTopScores` that takes an array of numbers and returns the top 3 highest scores in descending order.

```js
// Input:  [45, 92, 78, 100, 65, 88, 55]
// Output: [100, 92, 88]
```

<details>
<summary>Solution</summary>

```js
function getTopScores(scores) {
  return [...scores]
    .sort((a, b) => b - a)
    .slice(0, 3);
}

console.log(getTopScores([45, 92, 78, 100, 65, 88, 55])); // [100, 92, 88]
console.log(getTopScores([10, 20]));                        // [20, 10]
```

**Explanation:**
1. `[...scores]` creates a copy to avoid mutating the original array.
2. `.sort((a, b) => b - a)` sorts in descending order.
3. `.slice(0, 3)` extracts the first three elements (the top 3 scores).
</details>

---

**Task 15: Chain map, filter, and reduce on Student Grades**

Given an array of student objects with `name` and `grade` properties, write a function that:
1. Filters students who scored above 60 (passing grade).
2. Adds 5 bonus points to each passing student's grade (capped at 100).
3. Calculates the average grade of the passing students after the bonus.

```js
// Input:
// [
//   { name: "Alice", grade: 85 },
//   { name: "Bob", grade: 55 },
//   { name: "Charlie", grade: 92 },
//   { name: "Diana", grade: 40 },
//   { name: "Eve", grade: 78 }
// ]
// Output: Average = 88.33 (approximately)
```

<details>
<summary>Solution</summary>

```js
function calculatePassingAverage(students) {
  const passingStudents = students.filter(s => s.grade > 60);

  const bonusGrades = passingStudents.map(s => ({
    ...s,
    grade: Math.min(s.grade + 5, 100)
  }));

  const totalGrades = bonusGrades.reduce((sum, s) => sum + s.grade, 0);

  const average = totalGrades / bonusGrades.length;

  return Math.round(average * 100) / 100;
}

const students = [
  { name: "Alice", grade: 85 },
  { name: "Bob", grade: 55 },
  { name: "Charlie", grade: 92 },
  { name: "Diana", grade: 40 },
  { name: "Eve", grade: 78 }
];

console.log(calculatePassingAverage(students)); // 88.33

// Chained version (single expression):
const avg = students
  .filter(s => s.grade > 60)
  .map(s => Math.min(s.grade + 5, 100))
  .reduce((acc, grade, i, arr) => {
    acc += grade;
    return i === arr.length - 1 ? Math.round((acc / arr.length) * 100) / 100 : acc;
  }, 0);

console.log(avg); // 88.33
```

**Explanation:**
1. `filter(s => s.grade > 60)` keeps Alice (85), Charlie (92), and Eve (78).
2. `map()` adds 5 bonus points: Alice (90), Charlie (97), Eve (83), capping at 100.
3. `reduce()` sums the grades: 90 + 97 + 83 = 270, then divides by 3 to get 90. With actual computation: (90 + 97 + 83) / 3 = 90.
</details>

---

**End of Practice Questions**

*Best of luck with your practice! Make sure to type out each solution yourself before checking the answers.*
