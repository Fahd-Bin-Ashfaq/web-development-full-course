# Week 10: Control Flow & Loops — Practice Questions

**Total Questions: 53**

| Section | Type | Count |
|---------|------|-------|
| A | Multiple Choice Questions | 15 |
| B | Short Answer Questions | 8 |
| C | What Is the Output? | 10 |
| D | Trace the Code | 5 |
| E | Coding Exercises | 15 |

---

## Section A: Multiple Choice Questions (MCQs)

**Q1.** What is the correct syntax for an `if` statement in JavaScript?

- A) `if x > 5 { }`
- B) `if (x > 5) { }`
- C) `if x > 5 then { }`
- D) `if [x > 5] { }`

<details>
<summary>Answer</summary>

**B) `if (x > 5) { }`**

In JavaScript, the condition in an `if` statement must be enclosed in parentheses `()`, and the block of code to execute is enclosed in curly braces `{}`.
</details>

---

**Q2.** What will be the output of the following code?

```js
let x = 10;
if (x > 5) {
  console.log("Big");
} else {
  console.log("Small");
}
```

- A) Small
- B) Big
- C) undefined
- D) Error

<details>
<summary>Answer</summary>

**B) Big**

Since `x` is 10 and 10 > 5 is `true`, the code inside the `if` block executes, printing "Big".
</details>

---

**Q3.** Which statement is used to select one of many blocks of code to execute based on a single value?

- A) `if...else if`
- B) `for`
- C) `switch`
- D) `while`

<details>
<summary>Answer</summary>

**C) `switch`**

The `switch` statement evaluates an expression and matches its value against multiple `case` clauses, executing the corresponding block of code.
</details>

---

**Q4.** What happens if you omit the `break` keyword in a `switch` case?

- A) The program throws an error
- B) Only the matched case runs
- C) Execution falls through to subsequent cases
- D) The switch statement is skipped entirely

<details>
<summary>Answer</summary>

**C) Execution falls through to subsequent cases**

Without a `break`, JavaScript continues executing the code in the next case(s) regardless of whether those cases match. This is known as "fall-through" behavior.
</details>

---

**Q5.** What is the correct syntax for a ternary operator?

- A) `condition : trueValue ? falseValue`
- B) `condition ? trueValue : falseValue`
- C) `condition ?? trueValue :: falseValue`
- D) `if condition then trueValue else falseValue`

<details>
<summary>Answer</summary>

**B) `condition ? trueValue : falseValue`**

The ternary operator uses `?` after the condition and `:` to separate the value returned when the condition is true from the value returned when it is false.
</details>

---

**Q6.** What is the correct syntax for a `for` loop in JavaScript?

- A) `for (i = 0; i < 5; i++) { }`
- B) `for (let i = 0, i < 5, i++) { }`
- C) `for (let i = 0; i < 5; i++) { }`
- D) `for let i = 0 to 5 { }`

<details>
<summary>Answer</summary>

**C) `for (let i = 0; i < 5; i++) { }`**

A `for` loop has three parts separated by semicolons: initialization (`let i = 0`), condition (`i < 5`), and update expression (`i++`). Option A is technically valid but uses an undeclared variable, which is bad practice.
</details>

---

**Q7.** How many times will the following loop run?

```js
for (let i = 1; i <= 5; i++) {
  console.log(i);
}
```

- A) 4
- B) 5
- C) 6
- D) Infinite

<details>
<summary>Answer</summary>

**B) 5**

The loop starts at 1 and runs while `i <= 5`. It executes for `i = 1, 2, 3, 4, 5`, which is 5 iterations.
</details>

---

**Q8.** What is the key difference between a `while` loop and a `do...while` loop?

- A) `while` can use `break`, but `do...while` cannot
- B) `do...while` always executes at least once
- C) `while` runs faster than `do...while`
- D) There is no difference

<details>
<summary>Answer</summary>

**B) `do...while` always executes at least once**

A `do...while` loop checks the condition after executing the loop body, which means the body runs at least once even if the condition is initially `false`. A `while` loop checks the condition before executing the body.
</details>

---

**Q9.** What does the `break` statement do inside a loop?

- A) Skips the current iteration and moves to the next one
- B) Terminates the loop entirely
- C) Restarts the loop from the beginning
- D) Pauses the loop temporarily

<details>
<summary>Answer</summary>

**B) Terminates the loop entirely**

The `break` statement immediately exits the loop, and execution continues with the statement after the loop.
</details>

---

**Q10.** What does the `continue` statement do inside a loop?

- A) Terminates the loop entirely
- B) Skips the current iteration and moves to the next one
- C) Continues executing the remaining code in the current iteration
- D) Restarts the loop from iteration zero

<details>
<summary>Answer</summary>

**B) Skips the current iteration and moves to the next one**

The `continue` statement skips the rest of the code in the current iteration and jumps to the next iteration of the loop.
</details>

---

**Q11.** Which of the following will cause an infinite loop?

- A) `for (let i = 0; i < 10; i++) { }`
- B) `while (true) { break; }`
- C) `while (true) { }`
- D) `for (let i = 10; i > 0; i--) { }`

<details>
<summary>Answer</summary>

**C) `while (true) { }`**

A `while (true)` loop with no `break` statement inside it will run forever because the condition never becomes `false`. Option B also uses `while (true)`, but it contains a `break` that immediately exits the loop.
</details>

---

**Q12.** What will the following nested loop print in total?

```js
for (let i = 0; i < 3; i++) {
  for (let j = 0; j < 2; j++) {
    console.log("*");
  }
}
```

- A) 3 stars
- B) 5 stars
- C) 6 stars
- D) 2 stars

<details>
<summary>Answer</summary>

**C) 6 stars**

The outer loop runs 3 times (i = 0, 1, 2). For each iteration of the outer loop, the inner loop runs 2 times (j = 0, 1). Total = 3 x 2 = 6.
</details>

---

**Q13.** What is the value of `i` when the following loop terminates?

```js
let i = 0;
while (i < 5) {
  i++;
}
console.log(i);
```

- A) 4
- B) 5
- C) 6
- D) undefined

<details>
<summary>Answer</summary>

**B) 5**

The loop increments `i` on each iteration. When `i` becomes 5, the condition `i < 5` is `false`, so the loop exits and `console.log(i)` prints 5.
</details>

---

**Q14.** Which loop is best suited for iterating over the elements of an array?

- A) `for...in`
- B) `for...of`
- C) `do...while`
- D) `switch`

<details>
<summary>Answer</summary>

**B) `for...of`**

The `for...of` loop is designed to iterate over iterable objects such as arrays, strings, and other collections. It provides the value of each element directly. While `for...in` iterates over property keys (indices for arrays), `for...of` is the preferred choice for array values.
</details>

---

**Q15.** What is the output of the following code?

```js
let result = 5 > 3 ? "Yes" : "No";
console.log(result);
```

- A) true
- B) false
- C) Yes
- D) No

<details>
<summary>Answer</summary>

**C) Yes**

The ternary operator evaluates `5 > 3`, which is `true`. When the condition is true, the value before the colon (`"Yes"`) is returned and assigned to `result`.
</details>

---

## Section B: Short Answer Questions

**Q1.** When should you use a `switch` statement instead of multiple `if...else if` statements? Provide an example scenario.

<details>
<summary>Answer</summary>

Use a `switch` statement when you are comparing a single variable or expression against multiple specific, discrete values. It improves readability and is cleaner than writing many `else if` blocks.

**Example scenario:** Determining the name of a day based on a number (1 through 7).

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
    console.log("Other day");
}
```

Use `if...else if` when conditions involve ranges, complex expressions, or comparisons with different variables (e.g., `if (score >= 90)`, `if (age > 18 && hasLicense)`).
</details>

---

**Q2.** Explain the difference between a `while` loop and a `do...while` loop. When would you choose one over the other?

<details>
<summary>Answer</summary>

- A **`while` loop** checks the condition **before** executing the loop body. If the condition is `false` from the start, the body never executes.
- A **`do...while` loop** executes the loop body **first** and then checks the condition. This guarantees the body runs **at least once**.

```js
// while — may not execute at all
let x = 10;
while (x < 5) {
  console.log(x); // Never runs
}

// do...while — executes at least once
let y = 10;
do {
  console.log(y); // Prints 10
} while (y < 5);
```

**When to choose `do...while`:** When you need the loop body to execute at least once, such as displaying a menu to the user and then asking whether they want to continue.
</details>

---

**Q3.** What is an infinite loop? List two common causes and explain how to prevent them.

<details>
<summary>Answer</summary>

An **infinite loop** is a loop that never terminates because its exit condition is never met. The program becomes stuck, and the browser or runtime may freeze or crash.

**Common causes:**

1. **Forgetting to update the loop variable:**
   ```js
   let i = 0;
   while (i < 5) {
     console.log(i);
     // Missing: i++
   }
   ```

2. **Using a condition that can never become false:**
   ```js
   while (true) {
     console.log("Running forever");
   }
   ```

**How to prevent them:**

- Always ensure the loop variable is updated inside the loop body so the condition eventually becomes `false`.
- When using `while (true)`, always include a `break` statement with a clear exit condition.
- Double-check your loop's logic before running the code.
</details>

---

**Q4.** What does the `break` statement do, and how does it differ from `continue`? Provide a code example for each.

<details>
<summary>Answer</summary>

- **`break`** immediately **terminates** the entire loop, and execution continues after the loop.
- **`continue`** **skips the rest of the current iteration** and moves to the next iteration of the loop.

**`break` example:**
```js
for (let i = 1; i <= 10; i++) {
  if (i === 5) {
    break; // Loop stops entirely at 5
  }
  console.log(i);
}
// Output: 1, 2, 3, 4
```

**`continue` example:**
```js
for (let i = 1; i <= 10; i++) {
  if (i === 5) {
    continue; // Skips 5, continues with 6
  }
  console.log(i);
}
// Output: 1, 2, 3, 4, 6, 7, 8, 9, 10
```
</details>

---

**Q5.** When should you use a `for` loop versus a `while` loop?

<details>
<summary>Answer</summary>

- Use a **`for` loop** when you know **how many times** the loop should run (i.e., the number of iterations is known in advance). It keeps the initialization, condition, and update in one line.

  ```js
  // Print numbers 1 to 10
  for (let i = 1; i <= 10; i++) {
    console.log(i);
  }
  ```

- Use a **`while` loop** when the number of iterations is **unknown** and depends on a condition that changes during execution.

  ```js
  // Keep halving a number until it drops below 1
  let num = 100;
  while (num >= 1) {
    console.log(num);
    num = num / 2;
  }
  ```
</details>

---

**Q6.** Explain what the `for...of` loop does and how it differs from a traditional `for` loop.

<details>
<summary>Answer</summary>

The `for...of` loop iterates over the **values** of an iterable object (such as an array or a string) without requiring you to manage an index variable.

```js
// Traditional for loop
let fruits = ["Apple", "Banana", "Cherry"];
for (let i = 0; i < fruits.length; i++) {
  console.log(fruits[i]);
}

// for...of loop
for (let fruit of fruits) {
  console.log(fruit);
}
```

**Differences:**
- `for...of` is cleaner and less error-prone because there is no index to manage.
- A traditional `for` loop gives you access to the index, which is useful when you need the position of each element.
- `for...of` works with any iterable (arrays, strings, Maps, Sets), while the traditional `for` loop works with anything that has a numeric index.
</details>

---

**Q7.** What is a nested loop? Explain with a practical example where you would need one.

<details>
<summary>Answer</summary>

A **nested loop** is a loop inside another loop. The inner loop completes all of its iterations for each single iteration of the outer loop.

**Practical example — printing a multiplication table:**

```js
for (let i = 1; i <= 3; i++) {
  for (let j = 1; j <= 3; j++) {
    console.log(`${i} x ${j} = ${i * j}`);
  }
}
```

Output:
```
1 x 1 = 1
1 x 2 = 2
1 x 3 = 3
2 x 1 = 2
2 x 2 = 4
2 x 3 = 6
3 x 1 = 3
3 x 2 = 6
3 x 3 = 9
```

Nested loops are commonly used for working with grids, multi-dimensional arrays, pattern printing, and comparing elements within a collection.
</details>

---

**Q8.** What is the purpose of the `default` case in a `switch` statement? Is it required?

<details>
<summary>Answer</summary>

The `default` case acts as a **fallback** that executes when none of the `case` values match the expression. It is similar to the `else` block in an `if...else` chain.

```js
let color = "purple";

switch (color) {
  case "red":
    console.log("Stop");
    break;
  case "green":
    console.log("Go");
    break;
  default:
    console.log("Unknown color");
}
// Output: Unknown color
```

**Is it required?** No, the `default` case is optional. However, it is considered a best practice to include one so that unexpected values are handled gracefully rather than ignored.
</details>

---

## Section C: What Is the Output?

**Q1.** What is the output of the following code?

```js
for (let i = 0; i < 5; i++) {
  console.log(i);
}
```

<details>
<summary>Answer</summary>

```
0
1
2
3
4
```

**Explanation:** The loop starts at `i = 0` and runs while `i < 5`, incrementing by 1 each time. It prints 0, 1, 2, 3, and 4.
</details>

---

**Q2.** What is the output of the following code?

```js
for (let i = 1; i <= 10; i++) {
  if (i === 6) {
    break;
  }
  console.log(i);
}
```

<details>
<summary>Answer</summary>

```
1
2
3
4
5
```

**Explanation:** The loop prints numbers starting from 1. When `i` reaches 6, the `break` statement executes before `console.log(i)`, so 6 is never printed and the loop terminates immediately.
</details>

---

**Q3.** What is the output of the following code?

```js
for (let i = 1; i <= 10; i++) {
  if (i % 2 === 0) {
    continue;
  }
  console.log(i);
}
```

<details>
<summary>Answer</summary>

```
1
3
5
7
9
```

**Explanation:** When `i` is even (`i % 2 === 0`), the `continue` statement skips the `console.log(i)` call and moves to the next iteration. Only odd numbers are printed.
</details>

---

**Q4.** What is the output of the following code?

```js
let count = 0;
for (let i = 0; i < 3; i++) {
  for (let j = 0; j < 3; j++) {
    count++;
  }
}
console.log(count);
```

<details>
<summary>Answer</summary>

```
9
```

**Explanation:** The outer loop runs 3 times. For each outer iteration, the inner loop also runs 3 times, incrementing `count` by 1 each time. Total increments = 3 x 3 = 9.
</details>

---

**Q5.** What is the output of the following code?

```js
let x = 15;
let result = x > 10 ? "Greater" : "Smaller";
console.log(result);
```

<details>
<summary>Answer</summary>

```
Greater
```

**Explanation:** The ternary operator checks if `x > 10`. Since 15 > 10 is `true`, the expression evaluates to `"Greater"`.
</details>

---

**Q6.** What is the output of the following code?

```js
let i = 5;
while (i > 0) {
  console.log(i);
  i -= 2;
}
```

<details>
<summary>Answer</summary>

```
5
3
1
```

**Explanation:** The loop starts with `i = 5` and decrements by 2 each iteration. It prints 5, then 3, then 1. After printing 1, `i` becomes -1, which is not greater than 0, so the loop ends.
</details>

---

**Q7.** What is the output of the following code?

```js
let num = 3;
do {
  console.log(num);
  num--;
} while (num > 0);
```

<details>
<summary>Answer</summary>

```
3
2
1
```

**Explanation:** The `do...while` loop executes the body first, printing `num`, then decrements it. It prints 3, 2, and 1. After `num` becomes 0, the condition `num > 0` is `false`, and the loop stops.
</details>

---

**Q8.** What is the output of the following code?

```js
for (let i = 0; i < 3; i++) {
  for (let j = 0; j <= i; j++) {
    process.stdout.write("* ");
  }
  console.log();
}
```

<details>
<summary>Answer</summary>

```
* 
* * 
* * * 
```

**Explanation:** When `i = 0`, the inner loop runs once (j = 0) and prints one star. When `i = 1`, it runs twice (j = 0, 1) and prints two stars. When `i = 2`, it runs three times and prints three stars. Each row ends with a newline from `console.log()`.
</details>

---

**Q9.** What is the output of the following code?

```js
let sum = 0;
for (let i = 1; i <= 5; i++) {
  if (i === 3) {
    continue;
  }
  sum += i;
}
console.log(sum);
```

<details>
<summary>Answer</summary>

```
12
```

**Explanation:** The loop adds numbers 1 through 5 to `sum`, but skips 3 because of the `continue` statement. So `sum = 1 + 2 + 4 + 5 = 12`.
</details>

---

**Q10.** What is the output of the following code?

```js
let text = "Hello";
let reversed = "";
for (let char of text) {
  reversed = char + reversed;
}
console.log(reversed);
```

<details>
<summary>Answer</summary>

```
olleH
```

**Explanation:** The `for...of` loop iterates over each character of `"Hello"`. Each character is prepended to `reversed`. After all iterations: `"H"` becomes `"He"` reversed to `"eH"`, then `"leH"`, then `"lleH"`, and finally `"olleH"`.
</details>

---

## Section D: Trace the Code

**Q1.** Trace through the following code and fill in the table showing the value of `i` and `sum` at the end of each iteration.

```js
let sum = 0;
for (let i = 1; i <= 4; i++) {
  sum += i;
}
console.log(sum);
```

<details>
<summary>Answer</summary>

| Iteration | `i` | `sum` (after `sum += i`) |
|-----------|-----|--------------------------|
| 1         | 1   | 1                        |
| 2         | 2   | 3                        |
| 3         | 3   | 6                        |
| 4         | 4   | 10                       |

**Final output:** `10`

After iteration 4, `i` becomes 5, the condition `i <= 4` is `false`, and the loop exits.
</details>

---

**Q2.** Trace through the following code and fill in the table.

```js
let result = 1;
let n = 5;
for (let i = 1; i <= n; i++) {
  result *= i;
}
console.log(result);
```

<details>
<summary>Answer</summary>

| Iteration | `i` | `result` (after `result *= i`) |
|-----------|-----|--------------------------------|
| 1         | 1   | 1                              |
| 2         | 2   | 2                              |
| 3         | 3   | 6                              |
| 4         | 4   | 24                             |
| 5         | 5   | 120                            |

**Final output:** `120`

This code calculates the factorial of 5 (5! = 120).
</details>

---

**Q3.** Trace through the following code and fill in the table.

```js
let x = 64;
let count = 0;
while (x > 1) {
  x = x / 2;
  count++;
}
console.log(count);
```

<details>
<summary>Answer</summary>

| Iteration | `x` (after `x = x / 2`) | `count` (after `count++`) |
|-----------|--------------------------|---------------------------|
| 1         | 32                       | 1                         |
| 2         | 16                       | 2                         |
| 3         | 8                        | 3                         |
| 4         | 4                        | 4                         |
| 5         | 2                        | 5                         |
| 6         | 1                        | 6                         |

**Final output:** `6`

The loop divides 64 by 2 repeatedly until `x` is no longer greater than 1. It takes 6 divisions, so `count = 6`.
</details>

---

**Q4.** Trace through the following code and fill in the table.

```js
let str = "code";
let output = "";
for (let i = str.length - 1; i >= 0; i--) {
  output += str[i];
}
console.log(output);
```

<details>
<summary>Answer</summary>

| Iteration | `i` | `str[i]` | `output` (after `output += str[i]`) |
|-----------|-----|----------|--------------------------------------|
| 1         | 3   | `"e"`    | `"e"`                                |
| 2         | 2   | `"d"`    | `"ed"`                               |
| 3         | 1   | `"o"`    | `"edo"`                              |
| 4         | 0   | `"c"`    | `"edoc"`                             |

**Final output:** `"edoc"`

The loop traverses the string `"code"` from the last character to the first, building the reversed string.
</details>

---

**Q5.** Trace through the following code and fill in the table.

```js
let a = 0;
let b = 1;
for (let i = 0; i < 6; i++) {
  console.log(a);
  let temp = a + b;
  a = b;
  b = temp;
}
```

<details>
<summary>Answer</summary>

| Iteration | `i` | `a` (printed) | `b` (before update) | `temp` (`a + b`) | `a` (after) | `b` (after) |
|-----------|-----|---------------|----------------------|-------------------|-------------|-------------|
| 1         | 0   | 0             | 1                    | 1                 | 1           | 1           |
| 2         | 1   | 1             | 1                    | 2                 | 1           | 2           |
| 3         | 2   | 1             | 2                    | 3                 | 2           | 3           |
| 4         | 3   | 2             | 3                    | 5                 | 3           | 5           |
| 5         | 4   | 3             | 5                    | 8                 | 5           | 8           |
| 6         | 5   | 5             | 8                    | 13                | 8           | 13          |

**Output:**
```
0
1
1
2
3
5
```

This code prints the first 6 numbers of the Fibonacci sequence.
</details>

---

## Section E: Coding Exercises

### Task 1: Positive, Negative, or Zero

Write a program that takes a number and prints whether it is **positive**, **negative**, or **zero**.

**Example:**
```
Input: -7
Output: "The number is negative"
```

<details>
<summary>Solution</summary>

```js
function checkNumber(num) {
  if (num > 0) {
    console.log("The number is positive");
  } else if (num < 0) {
    console.log("The number is negative");
  } else {
    console.log("The number is zero");
  }
}

checkNumber(-7);  // The number is negative
checkNumber(10);  // The number is positive
checkNumber(0);   // The number is zero
```
</details>

---

### Task 2: Largest of Three Numbers

Write a program that takes three numbers and prints the **largest** one.

**Example:**
```
Input: 25, 67, 43
Output: "The largest number is 67"
```

<details>
<summary>Solution</summary>

```js
function findLargest(a, b, c) {
  if (a >= b && a >= c) {
    console.log(`The largest number is ${a}`);
  } else if (b >= a && b >= c) {
    console.log(`The largest number is ${b}`);
  } else {
    console.log(`The largest number is ${c}`);
  }
}

findLargest(25, 67, 43);  // The largest number is 67
```
</details>

---

### Task 3: Grade Calculator

Write a program that takes a student's marks (0-100) and prints the grade:
- **A**: 90-100
- **B**: 80-89
- **C**: 70-79
- **D**: 60-69
- **F**: Below 60

**Example:**
```
Input: 85
Output: "Grade: B"
```

<details>
<summary>Solution</summary>

```js
function calculateGrade(marks) {
  if (marks < 0 || marks > 100) {
    console.log("Invalid marks. Please enter a value between 0 and 100.");
  } else if (marks >= 90) {
    console.log("Grade: A");
  } else if (marks >= 80) {
    console.log("Grade: B");
  } else if (marks >= 70) {
    console.log("Grade: C");
  } else if (marks >= 60) {
    console.log("Grade: D");
  } else {
    console.log("Grade: F");
  }
}

calculateGrade(85);   // Grade: B
calculateGrade(92);   // Grade: A
calculateGrade(45);   // Grade: F
```
</details>

---

### Task 4: Print Numbers 1 to 100

Write a program that prints numbers from **1 to 100** using a `for` loop.

<details>
<summary>Solution</summary>

```js
for (let i = 1; i <= 100; i++) {
  console.log(i);
}
```
</details>

---

### Task 5: Even Numbers Between 1 and 50

Write a program that prints all **even numbers** between 1 and 50.

**Expected output:** `2, 4, 6, 8, 10, ... 48, 50`

<details>
<summary>Solution</summary>

```js
// Method 1: Using modulus operator
for (let i = 1; i <= 50; i++) {
  if (i % 2 === 0) {
    console.log(i);
  }
}

// Method 2: Incrementing by 2
for (let i = 2; i <= 50; i += 2) {
  console.log(i);
}
```
</details>

---

### Task 6: Sum of Numbers from 1 to N

Write a program that calculates the **sum of all numbers from 1 to N**, where N is provided by the user.

**Example:**
```
Input: N = 5
Output: "The sum is 15" (1 + 2 + 3 + 4 + 5 = 15)
```

<details>
<summary>Solution</summary>

```js
function sumUpToN(n) {
  let sum = 0;
  for (let i = 1; i <= n; i++) {
    sum += i;
  }
  console.log(`The sum is ${sum}`);
}

sumUpToN(5);    // The sum is 15
sumUpToN(10);   // The sum is 55
sumUpToN(100);  // The sum is 5050
```
</details>

---

### Task 7: Multiplication Table

Write a program that prints the **multiplication table** for any given number.

**Example:**
```
Input: 7
Output:
7 x 1 = 7
7 x 2 = 14
...
7 x 10 = 70
```

<details>
<summary>Solution</summary>

```js
function multiplicationTable(num) {
  for (let i = 1; i <= 10; i++) {
    console.log(`${num} x ${i} = ${num * i}`);
  }
}

multiplicationTable(7);
```
</details>

---

### Task 8: Factorial Calculator

Write a program that calculates the **factorial** of a given number.

**Reminder:** Factorial of 5 = 5 x 4 x 3 x 2 x 1 = 120

**Example:**
```
Input: 5
Output: "The factorial of 5 is 120"
```

<details>
<summary>Solution</summary>

```js
function factorial(n) {
  let result = 1;
  for (let i = 1; i <= n; i++) {
    result *= i;
  }
  console.log(`The factorial of ${n} is ${result}`);
}

factorial(5);   // The factorial of 5 is 120
factorial(0);   // The factorial of 0 is 1
factorial(8);   // The factorial of 8 is 40320
```
</details>

---

### Task 9: FizzBuzz

Write a program that prints numbers from **1 to 100** with the following rules:
- Print **"Fizz"** for multiples of 3
- Print **"Buzz"** for multiples of 5
- Print **"FizzBuzz"** for multiples of both 3 and 5
- Print the number itself otherwise

**Expected output:** `1, 2, Fizz, 4, Buzz, Fizz, 7, 8, Fizz, Buzz, 11, Fizz, 13, 14, FizzBuzz, 16, ...`

<details>
<summary>Solution</summary>

```js
for (let i = 1; i <= 100; i++) {
  if (i % 3 === 0 && i % 5 === 0) {
    console.log("FizzBuzz");
  } else if (i % 3 === 0) {
    console.log("Fizz");
  } else if (i % 5 === 0) {
    console.log("Buzz");
  } else {
    console.log(i);
  }
}
```
</details>

---

### Task 10: Reverse a String

Write a program that **reverses a string** using a loop.

**Example:**
```
Input: "JavaScript"
Output: "tpircSavaJ"
```

<details>
<summary>Solution</summary>

```js
function reverseString(str) {
  let reversed = "";
  for (let i = str.length - 1; i >= 0; i--) {
    reversed += str[i];
  }
  console.log(reversed);
}

reverseString("JavaScript");  // tpircSavaJ
reverseString("Hello");       // olleH
```
</details>

---

### Task 11: Palindrome Checker

Write a program that checks if a given string is a **palindrome** (reads the same forwards and backwards).

**Example:**
```
Input: "madam"
Output: "madam is a palindrome"

Input: "hello"
Output: "hello is not a palindrome"
```

<details>
<summary>Solution</summary>

```js
function isPalindrome(str) {
  let reversed = "";
  for (let i = str.length - 1; i >= 0; i--) {
    reversed += str[i];
  }

  if (str === reversed) {
    console.log(`${str} is a palindrome`);
  } else {
    console.log(`${str} is not a palindrome`);
  }
}

isPalindrome("madam");    // madam is a palindrome
isPalindrome("racecar");  // racecar is a palindrome
isPalindrome("hello");    // hello is not a palindrome
```
</details>

---

### Task 12: Count Vowels

Write a program that counts the number of **vowels** (a, e, i, o, u) in a given string.

**Example:**
```
Input: "JavaScript"
Output: "Number of vowels: 3"
```

<details>
<summary>Solution</summary>

```js
function countVowels(str) {
  let count = 0;
  let vowels = "aeiouAEIOU";

  for (let char of str) {
    if (vowels.includes(char)) {
      count++;
    }
  }

  console.log(`Number of vowels: ${count}`);
}

countVowels("JavaScript");       // Number of vowels: 3
countVowels("Hello World");      // Number of vowels: 3
countVowels("Programming");      // Number of vowels: 3
```
</details>

---

### Task 13: Star Triangle Pattern

Write a program that prints a **right-angled triangle pattern** using stars.

**Example (for 5 rows):**
```
*
* *
* * *
* * * *
* * * * *
```

<details>
<summary>Solution</summary>

```js
function starTriangle(rows) {
  for (let i = 1; i <= rows; i++) {
    let line = "";
    for (let j = 1; j <= i; j++) {
      line += "* ";
    }
    console.log(line.trim());
  }
}

starTriangle(5);
```
</details>

---

### Task 14: Prime Numbers Between 1 and 100

Write a program that finds and prints all **prime numbers** between 1 and 100.

**Reminder:** A prime number is a number greater than 1 that has no divisors other than 1 and itself.

<details>
<summary>Solution</summary>

```js
for (let num = 2; num <= 100; num++) {
  let isPrime = true;

  for (let i = 2; i <= Math.sqrt(num); i++) {
    if (num % i === 0) {
      isPrime = false;
      break;
    }
  }

  if (isPrime) {
    console.log(num);
  }
}
```

**Expected output:** `2, 3, 5, 7, 11, 13, 17, 19, 23, 29, 31, 37, 41, 43, 47, 53, 59, 61, 67, 71, 73, 79, 83, 89, 97`
</details>

---

### Task 15: Number Guessing Game

Write a **number guessing game** that:
1. Generates a random number between 1 and 100
2. Asks the user to guess the number
3. Tells the user if their guess is too high or too low
4. Loops until the user guesses correctly
5. Displays the number of attempts it took

<details>
<summary>Solution</summary>

```js
const readline = require("readline");

const rl = readline.createInterface({
  input: process.stdin,
  output: process.stdout,
});

const secretNumber = Math.floor(Math.random() * 100) + 1;
let attempts = 0;

function askGuess() {
  rl.question("Guess a number between 1 and 100: ", (input) => {
    let guess = parseInt(input);
    attempts++;

    if (isNaN(guess)) {
      console.log("Please enter a valid number.");
      askGuess();
    } else if (guess < secretNumber) {
      console.log("Too low! Try again.");
      askGuess();
    } else if (guess > secretNumber) {
      console.log("Too high! Try again.");
      askGuess();
    } else {
      console.log(
        `Congratulations! You guessed it in ${attempts} attempt(s)!`
      );
      rl.close();
    }
  });
}

console.log("Welcome to the Number Guessing Game!");
askGuess();
```
</details>

---

**End of Practice Questions — Week 10: Control Flow & Loops**
