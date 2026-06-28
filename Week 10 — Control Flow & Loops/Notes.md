# Week 10: Control Flow & Loops

> **Prerequisites:** JavaScript fundamentals — variables, data types, and operators (Week 9).

---

## Table of Contents

1. [Control Flow Introduction](#1-control-flow-introduction)
2. [Conditional Statements](#2-conditional-statements)
3. [Switch Statement](#3-switch-statement)
4. [Ternary Operator](#4-ternary-operator)
5. [Loops Introduction](#5-loops-introduction)
6. [for Loop](#6-for-loop)
7. [while Loop](#7-while-loop)
8. [do...while Loop](#8-dowhile-loop)
9. [Loop Control](#9-loop-control)
10. [for...of Loop](#10-forof-loop)
11. [for...in Loop](#11-forin-loop)
12. [Common Loop Patterns](#12-common-loop-patterns)
13. [Summary](#13-summary)

---

## 1. Control Flow Introduction

### What Is Control Flow?

By default, JavaScript executes code **line by line, from top to bottom**. This is called
**sequential execution**. But real programs need to make decisions and repeat actions.
**Control flow** is the mechanism that lets us change the order in which statements are
executed.

**Real-life analogy:** Think of a traffic signal at an intersection. Without it, every car
would try to go at once — chaos. The signal controls the *flow* of cars: green means go,
red means stop, yellow means slow down. In the same way, conditional statements control
the *flow* of code — deciding which block runs and which is skipped.

### The Big Picture

```
+---------------------------------------------+
|           CONTROL FLOW IN JAVASCRIPT         |
+---------------------------------------------+
|                                              |
|   +-------------------+  +----------------+ |
|   | Decision Making   |  | Repetition     | |
|   | (Conditionals)    |  | (Loops)        | |
|   +-------------------+  +----------------+ |
|   | - if / else       |  | - for          | |
|   | - else if         |  | - while        | |
|   | - switch          |  | - do...while   | |
|   | - ternary ( ? : ) |  | - for...of     | |
|   |                   |  | - for...in     | |
|   +-------------------+  +----------------+ |
|                                              |
|   +----------------------------------------+ |
|   | Loop Control: break, continue, labels  | |
|   +----------------------------------------+ |
+---------------------------------------------+
```

### Flowchart: How Decision Making Works

```
        +----------+
        |  START   |
        +----+-----+
             |
             v
      +--------------+
      | Is condition  |
      |    true?      |
      +------+--------+
             |
        +----+----+
        |         |
      YES        NO
        |         |
        v         v
  +---------+ +---------+
  | Do this | | Do that |
  +---------+ +---------+
        |         |
        +----+----+
             |
             v
        +----------+
        |   END    |
        +----------+
```

---

## 2. Conditional Statements

Conditional statements let your program choose between different paths based on whether a
condition evaluates to `true` or `false`.

---

### 2.1 The `if` Statement

The simplest form of decision making. The code block runs **only** if the condition is true.

**Syntax:**

```javascript
if (condition) {
    // Code to execute if condition is true
}
```

**Flowchart:**

```
        +----------+
        |  START   |
        +----+-----+
             |
             v
      +--------------+
      | condition     |-------- false --------+
      | is true?      |                       |
      +------+--------+                       |
             |                                |
           true                               |
             |                                |
             v                                |
    +------------------+                      |
    | Execute the code |                      |
    | inside { ... }   |                      |
    +--------+---------+                      |
             |                                |
             +----------+----+----------------+
                        |
                        v
                   +----------+
                   |   END    |
                   +----------+
```

**Example — Age Verification:**

```javascript
let age = 20;

if (age >= 18) {
    console.log("You are eligible to vote.");
}
// Output: You are eligible to vote.
```

**Real-life parallel:** A bouncer at a club checks your ID. If you are 18 or older, you
get in. If not, nothing happens — you simply walk away.

---

### 2.2 The `if...else` Statement

When you need to handle **both** outcomes — what happens when the condition is true, and
what happens when it is false.

**Syntax:**

```javascript
if (condition) {
    // Runs if condition is true
} else {
    // Runs if condition is false
}
```

**Flowchart:**

```
        +----------+
        |  START   |
        +----+-----+
             |
             v
      +--------------+
      | condition     |
      | is true?      |
      +------+--------+
             |
        +----+----+
        |         |
      true      false
        |         |
        v         v
  +---------+ +---------+
  |  if     | |  else   |
  |  block  | |  block  |
  +---------+ +---------+
        |         |
        +----+----+
             |
             v
        +----------+
        |   END    |
        +----------+
```

**Example — Pass or Fail:**

```javascript
let score = 45;

if (score >= 50) {
    console.log("You passed the exam!");
} else {
    console.log("You failed. Better luck next time.");
}
// Output: You failed. Better luck next time.
```

**Example — Login Check:**

```javascript
let enteredPassword = "hello123";
let correctPassword = "secure@456";

if (enteredPassword === correctPassword) {
    console.log("Login successful. Welcome!");
} else {
    console.log("Incorrect password. Access denied.");
}
// Output: Incorrect password. Access denied.
```

---

### 2.3 The `if...else if...else` Chain

When you have **more than two possible outcomes**, chain multiple conditions together.
JavaScript checks each condition from top to bottom and executes the **first** block whose
condition is true.

**Syntax:**

```javascript
if (condition1) {
    // Runs if condition1 is true
} else if (condition2) {
    // Runs if condition2 is true
} else if (condition3) {
    // Runs if condition3 is true
} else {
    // Runs if none of the above conditions are true
}
```

**Flowchart:**

```
        +----------+
        |  START   |
        +----+-----+
             |
             v
      +---------------+
      | condition1     |--- true ---> Execute Block 1 ---+
      | is true?       |                                  |
      +-------+--------+                                  |
              |                                           |
            false                                         |
              |                                           |
              v                                           |
      +---------------+                                   |
      | condition2     |--- true ---> Execute Block 2 ---+|
      | is true?       |                                  |
      +-------+--------+                                  |
              |                                           |
            false                                         |
              |                                           |
              v                                           |
      +---------------+                                   |
      | condition3     |--- true ---> Execute Block 3 ---+|
      | is true?       |                                  |
      +-------+--------+                                  |
              |                                           |
            false                                         |
              |                                           |
              v                                           |
      +---------------+                                   |
      | else block     |----------------------------------+
      | (default)      |                                  |
      +----------------+                                  |
                                                          |
             +--------------------------------------------+
             |
             v
        +----------+
        |   END    |
        +----------+
```

**Example — Grade Calculation:**

```javascript
let marks = 82;
let grade;

if (marks >= 90) {
    grade = "A+";
} else if (marks >= 80) {
    grade = "A";
} else if (marks >= 70) {
    grade = "B";
} else if (marks >= 60) {
    grade = "C";
} else if (marks >= 50) {
    grade = "D";
} else {
    grade = "F";
}

console.log("Your grade is: " + grade);
// Output: Your grade is: A
```

**Real-life parallel:** Think of a restaurant menu with price tiers. If you have more
than $50, you order steak. If you have more than $30, you order pasta. If you have more
than $15, you order a sandwich. Otherwise, you just get water.

**Example — Temperature Advice:**

```javascript
let temperature = 35;

if (temperature >= 40) {
    console.log("Extreme heat! Stay indoors.");
} else if (temperature >= 30) {
    console.log("It's hot. Stay hydrated.");
} else if (temperature >= 20) {
    console.log("Pleasant weather. Enjoy your day!");
} else if (temperature >= 10) {
    console.log("It's chilly. Wear a jacket.");
} else {
    console.log("It's freezing! Bundle up.");
}
// Output: It's hot. Stay hydrated.
```

---

## 3. Switch Statement

The `switch` statement provides a cleaner way to compare **one value** against **many
possible matches**. It is especially useful when you are checking the same variable against
a list of known values.

### Syntax

```javascript
switch (expression) {
    case value1:
        // Code to run if expression === value1
        break;
    case value2:
        // Code to run if expression === value2
        break;
    case value3:
        // Code to run if expression === value3
        break;
    default:
        // Code to run if no case matches
}
```

### How It Works

1. JavaScript evaluates the `expression` once.
2. It compares the result to each `case` value using **strict equality** (`===`).
3. If a match is found, the corresponding block runs.
4. The `break` keyword exits the switch.
5. If no case matches, the `default` block runs (if provided).

### The `break` Keyword Is Critical

Without `break`, JavaScript **falls through** to the next case and keeps executing code
until it hits a `break` or the end of the switch block. This is called **fall-through
behavior**, and it is almost always a bug when unintentional.

```
+---------------------------------------------------------+
|  What happens WITHOUT break:                            |
|                                                         |
|  case "A":  console.log("Excellent");  // runs          |
|  case "B":  console.log("Good");       // ALSO runs!    |
|  case "C":  console.log("Average");    // ALSO runs!    |
|  default:   console.log("Unknown");    // ALSO runs!    |
|                                                         |
|  All four messages print. This is fall-through.         |
+---------------------------------------------------------+
```

### Example — Day of the Week

```javascript
let day = 3;
let dayName;

switch (day) {
    case 1:
        dayName = "Monday";
        break;
    case 2:
        dayName = "Tuesday";
        break;
    case 3:
        dayName = "Wednesday";
        break;
    case 4:
        dayName = "Thursday";
        break;
    case 5:
        dayName = "Friday";
        break;
    case 6:
        dayName = "Saturday";
        break;
    case 7:
        dayName = "Sunday";
        break;
    default:
        dayName = "Invalid day number";
}

console.log("Today is " + dayName);
// Output: Today is Wednesday
```

### Intentional Fall-Through

Sometimes fall-through is useful. For example, grouping multiple cases that share the
same action:

```javascript
let fruit = "apple";

switch (fruit) {
    case "apple":
    case "mango":
    case "banana":
        console.log("This is a fruit.");
        break;
    case "carrot":
    case "potato":
        console.log("This is a vegetable.");
        break;
    default:
        console.log("Unknown item.");
}
// Output: This is a fruit.
```

### The `default` Case

The `default` block acts as a **catch-all**. It runs when no other case matches. It is
similar to the final `else` in an `if...else if...else` chain.

```javascript
let color = "purple";

switch (color) {
    case "red":
        console.log("Stop!");
        break;
    case "yellow":
        console.log("Slow down.");
        break;
    case "green":
        console.log("Go!");
        break;
    default:
        console.log("Unknown signal color: " + color);
}
// Output: Unknown signal color: purple
```

### Switch vs If-Else: When to Use Which

```
+-------------------+-------------------------------+-------------------------------+
| Criteria          | switch                        | if...else if...else           |
+-------------------+-------------------------------+-------------------------------+
| Best for          | Comparing one variable        | Complex conditions, ranges,   |
|                   | against many exact values      | multiple variables            |
+-------------------+-------------------------------+-------------------------------+
| Comparison type   | Strict equality (===) only    | Any expression (>, <, &&, ||) |
+-------------------+-------------------------------+-------------------------------+
| Readability       | Cleaner for many exact        | Better for range checks       |
|                   | value checks                  | (e.g., marks >= 90)           |
+-------------------+-------------------------------+-------------------------------+
| Flexibility       | Limited (single value match)  | Highly flexible               |
+-------------------+-------------------------------+-------------------------------+
| Fall-through      | Yes (can be useful or risky)  | No                            |
+-------------------+-------------------------------+-------------------------------+
| Example use case  | Menu options, day of week,    | Grade ranges, age checks,     |
|                   | status codes                  | nested conditions             |
+-------------------+-------------------------------+-------------------------------+
```

**Rule of thumb:** If you are checking one variable against 3 or more exact values, prefer
`switch`. If your conditions involve ranges, inequalities, or multiple variables, use
`if...else if...else`.

---

## 4. Ternary Operator

The **ternary operator** is a shorthand for a simple `if...else` statement. It is the only
JavaScript operator that takes three operands, which is where the name "ternary" comes from.

### Syntax

```javascript
condition ? valueIfTrue : valueIfFalse;
```

This is equivalent to:

```javascript
if (condition) {
    result = valueIfTrue;
} else {
    result = valueIfFalse;
}
```

### Examples

**Checking eligibility:**

```javascript
let age = 20;
let status = age >= 18 ? "Adult" : "Minor";
console.log(status);
// Output: Adult
```

**Greeting based on time:**

```javascript
let hour = 14;
let greeting = hour < 12 ? "Good morning!" : "Good afternoon!";
console.log(greeting);
// Output: Good afternoon!
```

**Setting a default value:**

```javascript
let userName = "";
let displayName = userName ? userName : "Guest";
console.log("Welcome, " + displayName);
// Output: Welcome, Guest
```

### When to Use vs When NOT to Use

```
+-------------------------------+--------------------------------------+
| USE the ternary operator      | AVOID the ternary operator           |
+-------------------------------+--------------------------------------+
| Simple true/false assignments | Complex logic with multiple steps    |
| Inline values in templates    | Side effects (console.log, etc.)     |
| Setting default values        | When readability suffers             |
| Short, clear conditions       | Nested ternaries (usually confusing) |
+-------------------------------+--------------------------------------+
```

### Nested Ternary (Use With Caution)

You can nest ternary operators, but it quickly becomes hard to read:

```javascript
let score = 85;

// Nested ternary — works but difficult to read
let result = score >= 90 ? "A+" :
             score >= 80 ? "A"  :
             score >= 70 ? "B"  :
             score >= 60 ? "C"  : "F";

console.log(result);
// Output: A
```

**Best practice:** If your ternary needs nesting, switch to a standard `if...else if...else`
chain instead. Code that is easy to read is always better than code that is clever.

---

## 5. Loops Introduction

### What Are Loops?

A **loop** is a programming construct that repeats a block of code as long as a specified
condition remains true.

**Real-life analogy:** Think about brushing your teeth every morning. You do not decide
each day from scratch whether to brush — it is a repeated action that happens daily as long
as you have teeth (the condition). That is a loop.

Another example: A factory assembly line. The same sequence of steps is performed on each
item that comes down the belt, over and over, until the shift ends.

### Why Loops Are Needed

Without loops, repetitive tasks require writing the same code many times:

```javascript
// WITHOUT loops — printing numbers 1 to 5
console.log(1);
console.log(2);
console.log(3);
console.log(4);
console.log(5);
```

Now imagine printing numbers 1 to 1000. That would be 1000 lines of code. With a loop:

```javascript
// WITH a loop — printing numbers 1 to 1000
for (let i = 1; i <= 1000; i++) {
    console.log(i);
}
```

Three lines instead of a thousand. Loops save time, reduce errors, and keep code clean.

### Types of Loops in JavaScript

```
+-----------------------------------------------+
|           LOOPS IN JAVASCRIPT                  |
+-----------------------------------------------+
|                                                |
|   +--------+  +--------+  +------------+      |
|   |  for   |  | while  |  | do...while |      |
|   +--------+  +--------+  +------------+      |
|                                                |
|   +----------+  +-----------+                  |
|   | for...of |  | for...in  |                  |
|   +----------+  +-----------+                  |
|                                                |
+-----------------------------------------------+
```

---

## 6. for Loop

The `for` loop is the most commonly used loop in JavaScript. It is ideal when you know
**exactly how many times** you want to repeat something.

### Syntax

```javascript
for (initialization; condition; increment) {
    // Code to repeat
}
```

| Part             | Purpose                                    | Example      |
|------------------|--------------------------------------------|--------------|
| `initialization` | Runs once before the loop starts           | `let i = 0`  |
| `condition`      | Checked before each iteration; loop continues while true | `i < 5` |
| `increment`      | Runs after each iteration                  | `i++`        |

### Step-by-Step Execution Diagram

```
for (let i = 1; i <= 3; i++) {
    console.log(i);
}

  +-------------------+
  | Initialization    |    let i = 1  (runs ONCE)
  | let i = 1         |
  +---------+---------+
            |
            v
  +---------+---------+
  | Check condition   |<--------------------------+
  | i <= 3 ?          |                           |
  +---------+---------+                           |
            |                                     |
       +----+----+                                |
       |         |                                |
     true      false                              |
       |         |                                |
       v         v                                |
  +---------+ +-------+                           |
  | Execute | | EXIT  |                           |
  | body    | | LOOP  |                           |
  +---------+ +-------+                           |
       |                                          |
       v                                          |
  +---------+---------+                           |
  | Increment         |                           |
  | i++               |--------------------------+
  +-------------------+

  Trace:
  +------+-----------+----------+---------+
  | Step | i value   | i <= 3 ? | Output  |
  +------+-----------+----------+---------+
  |  1   | 1         | true     | 1       |
  |  2   | 2         | true     | 2       |
  |  3   | 3         | true     | 3       |
  |  4   | 4         | false    | (exit)  |
  +------+-----------+----------+---------+
```

### Example — Counting 1 to 10

```javascript
for (let i = 1; i <= 10; i++) {
    console.log(i);
}
// Output: 1  2  3  4  5  6  7  8  9  10
```

### Example — Even Numbers from 2 to 20

```javascript
for (let i = 2; i <= 20; i += 2) {
    console.log(i);
}
// Output: 2  4  6  8  10  12  14  16  18  20
```

### Example — Countdown

```javascript
for (let i = 10; i >= 1; i--) {
    console.log(i);
}
console.log("Liftoff!");
// Output: 10  9  8  7  6  5  4  3  2  1  Liftoff!
```

### Nested for Loops

A loop inside another loop. The **inner loop completes all its iterations** for each
single iteration of the **outer loop**.

**Example — Multiplication Table (1 to 5):**

```javascript
for (let i = 1; i <= 5; i++) {
    let row = "";
    for (let j = 1; j <= 10; j++) {
        row += (i * j) + "\t";
    }
    console.log(row);
}

// Output:
// 1    2    3    4    5    6    7    8    9    10
// 2    4    6    8    10   12   14   16   18   20
// 3    6    9    12   15   18   21   24   27   30
// 4    8    12   16   20   24   28   32   36   40
// 5    10   15   20   25   30   35   40   45   50
```

**How nested loops work — visual:**

```
Outer loop (i = 1):
    Inner loop: j = 1, 2, 3, ..., 10   -->  Prints row for 1

Outer loop (i = 2):
    Inner loop: j = 1, 2, 3, ..., 10   -->  Prints row for 2

Outer loop (i = 3):
    Inner loop: j = 1, 2, 3, ..., 10   -->  Prints row for 3

...and so on.
```

**Example — Star Pattern:**

```javascript
for (let i = 1; i <= 5; i++) {
    let stars = "";
    for (let j = 1; j <= i; j++) {
        stars += "* ";
    }
    console.log(stars);
}

// Output:
// *
// * *
// * * *
// * * * *
// * * * * *
```

---

## 7. while Loop

The `while` loop repeats a block of code as long as a condition is true. It is best suited
for situations where you **do not know in advance** how many iterations will be needed.

### Syntax

```javascript
while (condition) {
    // Code to repeat
    // IMPORTANT: update something so condition eventually becomes false
}
```

### Flowchart

```
        +----------+
        |  START   |
        +----+-----+
             |
             v
      +--------------+
      | condition     |<----------+
      | is true?      |           |
      +------+--------+           |
             |                    |
        +----+----+               |
        |         |               |
      true      false             |
        |         |               |
        v         v               |
  +---------+ +--------+         |
  | Execute | |  EXIT  |         |
  |  body   | |  LOOP  |         |
  +----+----+ +--------+         |
       |                          |
       +--------------------------+
```

### Example — Counting to 5

```javascript
let count = 1;

while (count <= 5) {
    console.log(count);
    count++;
}
// Output: 1  2  3  4  5
```

### Infinite Loop Warning

If the condition **never becomes false**, the loop runs forever and crashes your program
or browser tab.

```javascript
// DANGER: Infinite loop!
// let x = 1;
// while (x > 0) {       <-- x is always > 0 because we never change it
//     console.log(x);
// }
```

**Always make sure** something inside the loop changes the condition so it will eventually
be false.

### Real-Life Example — Keep Asking Password Until Correct

```javascript
let correctPassword = "secret123";
let attempt = "";
let tries = 0;

// Simulating user input with an array (in real apps you'd use prompt() or a form)
let simulatedInputs = ["wrongpass", "12345", "secret123"];

while (attempt !== correctPassword) {
    attempt = simulatedInputs[tries];
    console.log("Attempt " + (tries + 1) + ": " + attempt);
    tries++;
}

console.log("Access granted after " + tries + " attempts.");
// Output:
// Attempt 1: wrongpass
// Attempt 2: 12345
// Attempt 3: secret123
// Access granted after 3 attempts.
```

This is a perfect `while` loop use case: you do not know how many wrong passwords the user
will enter before getting it right.

---

## 8. do...while Loop

The `do...while` loop is similar to `while`, but with one key difference: it executes the
code block **at least once** before checking the condition.

### Syntax

```javascript
do {
    // Code to execute (runs at least once)
} while (condition);
```

> **Note:** There is a semicolon after `while (condition);`. This is required.

### Flowchart

```
        +----------+
        |  START   |
        +----+-----+
             |
             v
     +---------------+
     |   Execute     |<-----------+
     |   body        |            |
     +-------+-------+            |
             |                    |
             v                    |
      +--------------+            |
      | condition     |           |
      | is true?      |           |
      +------+--------+           |
             |                    |
        +----+----+               |
        |         |               |
      true      false             |
        |         |               |
        +----+    v               |
             |  +--------+        |
             |  |  EXIT  |        |
             |  |  LOOP  |        |
             |  +--------+        |
             |                    |
             +--------------------+
```

### Difference from while

```
+-----------------------+----------------------------------+----------------------------------+
| Feature               | while                            | do...while                       |
+-----------------------+----------------------------------+----------------------------------+
| Condition check       | BEFORE the body runs             | AFTER the body runs              |
+-----------------------+----------------------------------+----------------------------------+
| Minimum executions    | 0 (if condition is false          | 1 (body always runs at least     |
|                       | from the start)                  | once)                            |
+-----------------------+----------------------------------+----------------------------------+
| Use case              | When you might not need           | When you need at least one       |
|                       | to run the body at all           | execution                        |
+-----------------------+----------------------------------+----------------------------------+
```

**Demonstration of the difference:**

```javascript
// while — condition is false from the start: body never runs
let x = 10;
while (x < 5) {
    console.log("while: " + x);   // This NEVER prints
    x++;
}

// do...while — condition is false, but body runs ONCE
let y = 10;
do {
    console.log("do...while: " + y);   // This prints ONCE
    y++;
} while (y < 5);

// Output:
// do...while: 10
```

### Real-Life Example — ATM Menu

An ATM always shows you the menu **at least once** when you insert your card. After each
transaction, it asks if you want to do something else.

```javascript
let simulatedChoices = [1, 2, 4];   // Simulated user selections
let choiceIndex = 0;
let choice;

do {
    console.log("\n--- ATM Menu ---");
    console.log("1. Check Balance");
    console.log("2. Withdraw Cash");
    console.log("3. Deposit Cash");
    console.log("4. Exit");

    choice = simulatedChoices[choiceIndex];
    console.log("You selected: " + choice);
    choiceIndex++;

    switch (choice) {
        case 1:
            console.log("Your balance is $5,000.");
            break;
        case 2:
            console.log("Cash dispensed.");
            break;
        case 3:
            console.log("Cash deposited.");
            break;
        case 4:
            console.log("Thank you. Goodbye!");
            break;
        default:
            console.log("Invalid option.");
    }
} while (choice !== 4);

// Output:
// --- ATM Menu ---
// 1. Check Balance
// 2. Withdraw Cash
// 3. Deposit Cash
// 4. Exit
// You selected: 1
// Your balance is $5,000.
//
// --- ATM Menu ---
// ...
// You selected: 2
// Cash dispensed.
//
// --- ATM Menu ---
// ...
// You selected: 4
// Thank you. Goodbye!
```

---

## 9. Loop Control

JavaScript provides keywords to **alter the normal flow** of a loop.

### 9.1 `break` — Exit the Loop Early

The `break` statement immediately terminates the loop, regardless of whether the condition
is still true.

```javascript
for (let i = 1; i <= 10; i++) {
    if (i === 6) {
        console.log("Found 6! Stopping the loop.");
        break;
    }
    console.log(i);
}
// Output: 1  2  3  4  5  Found 6! Stopping the loop.
```

**Real-life analogy:** You are searching for your keys in 10 drawers. Once you find them
in drawer 5, you stop searching — you do not open drawers 6 through 10.

### 9.2 `continue` — Skip the Current Iteration

The `continue` statement skips the **rest of the current iteration** and jumps to the next
one.

```javascript
for (let i = 1; i <= 10; i++) {
    if (i % 2 === 0) {
        continue;   // Skip even numbers
    }
    console.log(i);
}
// Output: 1  3  5  7  9
```

**Visual flow of `continue`:**

```
  i = 1  -->  1 is odd   -->  print 1
  i = 2  -->  2 is even  -->  SKIP (continue)
  i = 3  -->  3 is odd   -->  print 3
  i = 4  -->  4 is even  -->  SKIP (continue)
  i = 5  -->  5 is odd   -->  print 5
  ... and so on
```

### 9.3 Labeled Statements (Brief Mention)

Labels let you `break` or `continue` an **outer** loop from inside an **inner** loop. They
are rarely used but worth knowing about.

```javascript
outerLoop:
for (let i = 1; i <= 3; i++) {
    for (let j = 1; j <= 3; j++) {
        if (i === 2 && j === 2) {
            console.log("Breaking outer loop at i=" + i + ", j=" + j);
            break outerLoop;   // Breaks the OUTER loop, not just the inner one
        }
        console.log("i=" + i + ", j=" + j);
    }
}
// Output:
// i=1, j=1
// i=1, j=2
// i=1, j=3
// i=2, j=1
// Breaking outer loop at i=2, j=2
```

Without the label, `break` would only exit the inner loop, and the outer loop would
continue with `i = 3`.

---

## 10. for...of Loop

The `for...of` loop provides a clean, readable way to iterate over **iterable** values
such as **arrays** and **strings**. It was introduced in ES6 (ES2015).

### Syntax

```javascript
for (let element of iterable) {
    // Code using element
}
```

### Iterating Over an Array

```javascript
let fruits = ["Apple", "Banana", "Cherry", "Date"];

for (let fruit of fruits) {
    console.log(fruit);
}
// Output:
// Apple
// Banana
// Cherry
// Date
```

Compare this with a traditional `for` loop:

```javascript
// Traditional for loop — more verbose
for (let i = 0; i < fruits.length; i++) {
    console.log(fruits[i]);
}
```

The `for...of` version is shorter and eliminates the need to manage an index variable.

### Iterating Over a String

```javascript
let word = "Hello";

for (let char of word) {
    console.log(char);
}
// Output:
// H
// e
// l
// l
// o
```

### When to Use `for...of`

- When you need the **values** from an array or string.
- When you do **not** need the index.
- When you want clean, readable code.

> **Note:** `for...of` does **not** work on plain objects. Use `for...in` for objects
> (covered in the next section).

---

## 11. for...in Loop

The `for...in` loop iterates over the **enumerable property names (keys)** of an object.

### Syntax

```javascript
for (let key in object) {
    // Code using key and object[key]
}
```

### Iterating Over Object Properties

```javascript
let student = {
    name: "Ali",
    age: 22,
    course: "MERN Stack",
    city: "Karachi"
};

for (let key in student) {
    console.log(key + ": " + student[key]);
}
// Output:
// name: Ali
// age: 22
// course: MERN Stack
// city: Karachi
```

### `for...in` on Arrays (Not Recommended)

While `for...in` technically works on arrays, it iterates over **index strings** and may
include inherited properties. Always prefer `for...of` for arrays.

```javascript
let colors = ["red", "green", "blue"];

for (let index in colors) {
    console.log(index + " -> " + colors[index]);
}
// Output:
// 0 -> red
// 1 -> green
// 2 -> blue
// Note: index is a STRING ("0", "1", "2"), not a number
```

### for...of vs for...in — Quick Comparison

```
+---------------------+----------------------------+----------------------------+
| Feature             | for...of                   | for...in                   |
+---------------------+----------------------------+----------------------------+
| Iterates over       | Values                     | Keys (property names)      |
+---------------------+----------------------------+----------------------------+
| Best for            | Arrays, Strings, Maps,     | Objects                    |
|                     | Sets                       |                            |
+---------------------+----------------------------+----------------------------+
| Works on objects?   | No                         | Yes                        |
+---------------------+----------------------------+----------------------------+
| Works on arrays?    | Yes (recommended)          | Yes (not recommended)      |
+---------------------+----------------------------+----------------------------+
| Returns             | Element values             | Index or property name     |
|                     |                            | (as a string)              |
+---------------------+----------------------------+----------------------------+
```

---

## 12. Common Loop Patterns

These are classic problems that every developer should be comfortable solving with loops.

### 12.1 Sum of Numbers

```javascript
let sum = 0;

for (let i = 1; i <= 100; i++) {
    sum += i;
}

console.log("Sum of 1 to 100: " + sum);
// Output: Sum of 1 to 100: 5050
```

### 12.2 Finding Maximum and Minimum

```javascript
let numbers = [45, 12, 89, 3, 67, 34, 91, 23];

let max = numbers[0];
let min = numbers[0];

for (let i = 1; i < numbers.length; i++) {
    if (numbers[i] > max) {
        max = numbers[i];
    }
    if (numbers[i] < min) {
        min = numbers[i];
    }
}

console.log("Maximum: " + max);   // Output: Maximum: 91
console.log("Minimum: " + min);   // Output: Minimum: 3
```

### 12.3 Counting Characters in a String

```javascript
let sentence = "hello world";
let charCount = {};

for (let char of sentence) {
    if (char === " ") continue;   // Skip spaces

    if (charCount[char]) {
        charCount[char]++;
    } else {
        charCount[char] = 1;
    }
}

console.log(charCount);
// Output: { h: 1, e: 1, l: 3, o: 2, w: 1, r: 1, d: 1 }
```

### 12.4 Reversing a String

```javascript
let original = "JavaScript";
let reversed = "";

for (let i = original.length - 1; i >= 0; i--) {
    reversed += original[i];
}

console.log("Original: " + original);    // Output: Original: JavaScript
console.log("Reversed: " + reversed);    // Output: Reversed: tpircSavaJ
```

### 12.5 FizzBuzz (Classic Interview Problem)

**The rules:**
- Print numbers from 1 to 30.
- If a number is divisible by 3, print **"Fizz"** instead.
- If a number is divisible by 5, print **"Buzz"** instead.
- If a number is divisible by both 3 and 5, print **"FizzBuzz"** instead.

```javascript
for (let i = 1; i <= 30; i++) {
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

// Output:
// 1
// 2
// Fizz
// 4
// Buzz
// Fizz
// 7
// 8
// Fizz
// Buzz
// 11
// Fizz
// 13
// 14
// FizzBuzz
// 16
// 17
// Fizz
// 19
// Buzz
// Fizz
// 22
// 23
// Fizz
// Buzz
// 26
// Fizz
// 28
// 29
// FizzBuzz
```

**Why FizzBuzz matters:** It tests your understanding of loops, conditionals, and the
modulus operator all at once. It is one of the most common coding interview screening
questions.

---

## 13. Summary

### Conditionals at a Glance

```
+---------------------+--------------------------------------------------+
| Statement           | Use When                                         |
+---------------------+--------------------------------------------------+
| if                  | You have a single condition to check              |
| if...else           | You have two possible outcomes                    |
| if...else if...else | You have multiple conditions to check in order    |
| switch              | You compare one value against many exact matches  |
| ternary ( ? : )     | You need a quick inline true/false assignment     |
+---------------------+--------------------------------------------------+
```

### Loops at a Glance

```
+---------------------+--------------------------------------------------+
| Loop                | Use When                                         |
+---------------------+--------------------------------------------------+
| for                 | You know exactly how many times to iterate        |
| while               | Number of iterations is unknown (condition-based) |
| do...while          | You need at least one execution before checking   |
| for...of            | You want to iterate over array/string values      |
| for...in            | You want to iterate over object keys              |
+---------------------+--------------------------------------------------+
```

### Loop Control at a Glance

```
+---------------------+--------------------------------------------------+
| Keyword             | What It Does                                     |
+---------------------+--------------------------------------------------+
| break               | Immediately exits the loop                        |
| continue            | Skips the rest of the current iteration            |
| label:              | Names a loop so break/continue can target it       |
+---------------------+--------------------------------------------------+
```

### Key Takeaways

1. **Control flow** changes the default top-to-bottom execution of code.
2. **Conditionals** (if, else, switch, ternary) let your program make decisions.
3. **Loops** (for, while, do...while) let your program repeat actions efficiently.
4. Always ensure loops have a **termination condition** to avoid infinite loops.
5. Use `break` to exit early and `continue` to skip iterations.
6. Use `for...of` for arrays and strings; use `for...in` for objects.
7. Practice with classic problems like FizzBuzz, reversing strings, and finding max/min
   values to build your loop skills.

---

> **Next Week (Week 11):** Functions & Arrays — writing reusable code and working with
> collections of data.
