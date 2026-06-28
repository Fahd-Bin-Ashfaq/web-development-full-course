# Week 9: JavaScript Fundamentals - Practice Questions

**Total Questions: 48**

| Section | Type | Questions |
|---------|------|-----------|
| A | Multiple Choice Questions (MCQs) | 15 |
| B | Short Answer Questions | 8 |
| C | What Is the Output? | 10 |
| D | Code Correction | 5 |
| E | Coding Exercises | 10 |

---

## Section A: Multiple Choice Questions (MCQs)

**Instructions:** Choose the correct answer from the four options provided.

---

**Q1.** Which keyword is used to declare a variable that cannot be reassigned?

- A) `var`
- B) `let`
- C) `const`
- D) `define`

<details>
<summary>Answer</summary>

**C) `const`**

The `const` keyword declares a variable whose value cannot be reassigned after initialization. If you try to reassign a `const` variable, JavaScript will throw a `TypeError`.

</details>

---

**Q2.** What is the output of `typeof "Hello"`?

- A) `text`
- B) `string`
- C) `String`
- D) `char`

<details>
<summary>Answer</summary>

**B) `string`**

The `typeof` operator returns `"string"` (lowercase) for any string value. JavaScript does not have a `char` or `text` type.

</details>

---

**Q3.** Which of the following is NOT a primitive data type in JavaScript?

- A) `string`
- B) `number`
- C) `boolean`
- D) `array`

<details>
<summary>Answer</summary>

**D) `array`**

Arrays are objects in JavaScript, not primitive types. The primitive data types are `string`, `number`, `boolean`, `null`, `undefined`, `symbol`, and `bigint`.

</details>

---

**Q4.** What does `==` do differently from `===`?

- A) `==` compares values only; `===` compares values and types
- B) `==` is faster than `===`
- C) `===` compares values only; `==` compares values and types
- D) There is no difference

<details>
<summary>Answer</summary>

**A) `==` compares values only; `===` compares values and types**

The `==` operator performs type coercion before comparison, meaning it converts both values to the same type. The `===` operator checks both the value and the type without any conversion.

</details>

---

**Q5.** What is the result of `typeof null`?

- A) `null`
- B) `undefined`
- C) `object`
- D) `NaN`

<details>
<summary>Answer</summary>

**C) `object`**

This is a well-known bug in JavaScript that has existed since the language was first created. `typeof null` returns `"object"` even though `null` is not actually an object. This behavior has been kept for backward compatibility.

</details>

---

**Q6.** Which of the following values is falsy in JavaScript?

- A) `"false"`
- B) `1`
- C) `[]`
- D) `0`

<details>
<summary>Answer</summary>

**D) `0`**

In JavaScript, the falsy values are: `false`, `0`, `""` (empty string), `null`, `undefined`, and `NaN`. The string `"false"` is truthy because it is a non-empty string. An empty array `[]` is also truthy.

</details>

---

**Q7.** What is the correct way to write a template literal?

- A) `'Hello ' + name`
- B) `"Hello " + name`
- C) `` `Hello ${name}` ``
- D) `'Hello ${name}'`

<details>
<summary>Answer</summary>

**C)** `` `Hello ${name}` ``

Template literals use backticks (`` ` ``) instead of single or double quotes. Variables and expressions are embedded using the `${...}` syntax. Option D uses single quotes, so `${name}` would be treated as plain text, not a variable.

</details>

---

**Q8.** What does `"hello".toUpperCase()` return?

- A) `"Hello"`
- B) `"HELLO"`
- C) `"hello"`
- D) `undefined`

<details>
<summary>Answer</summary>

**B) `"HELLO"`**

The `toUpperCase()` string method converts all characters in the string to uppercase and returns a new string. It does not modify the original string.

</details>

---

**Q9.** What is the result of `"5" + 3` in JavaScript?

- A) `8`
- B) `"53"`
- C) `53`
- D) `NaN`

<details>
<summary>Answer</summary>

**B) `"53"`**

When the `+` operator is used with a string and a number, JavaScript performs type coercion and converts the number to a string, then concatenates them. The result is the string `"53"`.

</details>

---

**Q10.** What does `NaN === NaN` evaluate to?

- A) `true`
- B) `false`
- C) `NaN`
- D) `undefined`

<details>
<summary>Answer</summary>

**B) `false`**

`NaN` is the only value in JavaScript that is not equal to itself. Both `NaN == NaN` and `NaN === NaN` return `false`. To check if a value is `NaN`, use the `isNaN()` function or `Number.isNaN()`.

</details>

---

**Q11.** Which of the following will cause an error?

- A) `let x = 10; x = 20;`
- B) `const y = 10; y = 20;`
- C) `var z = 10; z = 20;`
- D) `let a = 10; let b = 20;`

<details>
<summary>Answer</summary>

**B) `const y = 10; y = 20;`**

Variables declared with `const` cannot be reassigned. Attempting to do so will throw a `TypeError: Assignment to constant variable`. Both `let` and `var` allow reassignment.

</details>

---

**Q12.** What is the result of `10 % 3`?

- A) `3`
- B) `1`
- C) `3.33`
- D) `0`

<details>
<summary>Answer</summary>

**B) `1`**

The `%` operator is the modulus (remainder) operator. It returns the remainder when the left operand is divided by the right operand. `10 / 3 = 3` with a remainder of `1`.

</details>

---

**Q13.** What does `Boolean("")` return?

- A) `true`
- B) `false`
- C) `""`
- D) `undefined`

<details>
<summary>Answer</summary>

**B) `false`**

An empty string `""` is a falsy value in JavaScript. When converted to a boolean using `Boolean()`, it returns `false`. Non-empty strings are truthy.

</details>

---

**Q14.** Which logical operator returns `true` only if BOTH conditions are true?

- A) `||`
- B) `&&`
- C) `!`
- D) `??`

<details>
<summary>Answer</summary>

**B) `&&`**

The `&&` (logical AND) operator returns `true` only when both operands are true. The `||` (logical OR) returns `true` if at least one operand is true. The `!` (logical NOT) negates a value.

</details>

---

**Q15.** What is the output of `typeof undefined`?

- A) `"null"`
- B) `"undefined"`
- C) `"object"`
- D) `"NaN"`

<details>
<summary>Answer</summary>

**B) `"undefined"`**

The `typeof` operator returns `"undefined"` for variables that have been declared but not assigned a value, or for the `undefined` value itself.

</details>

---

## Section B: Short Answer Questions

**Instructions:** Answer the following questions in your own words. Aim for 3-5 sentences per answer.

---

**Q1.** What is the difference between `let`, `var`, and `const`? When should you use each one?

<details>
<summary>Answer</summary>

`var` is the oldest way to declare variables in JavaScript. It is function-scoped, meaning it is accessible anywhere within the function where it is declared. It can be redeclared and reassigned, which can lead to unexpected bugs.

`let` was introduced in ES6 (2015). It is block-scoped, meaning it is only accessible within the block `{ }` where it is declared. It can be reassigned but cannot be redeclared in the same scope.

`const` is also block-scoped and was introduced in ES6. It must be initialized at the time of declaration and cannot be reassigned. Use `const` by default for values that should not change, use `let` when the value needs to change, and avoid `var` in modern JavaScript.

</details>

---

**Q2.** What is type coercion in JavaScript? Provide an example.

<details>
<summary>Answer</summary>

Type coercion is the automatic conversion of a value from one data type to another by the JavaScript engine. This happens when an operator or function expects a certain type but receives a different one.

For example, in the expression `"5" + 3`, JavaScript coerces the number `3` into the string `"3"` and then concatenates them, resulting in `"53"`. However, in `"5" - 3`, JavaScript coerces the string `"5"` into the number `5` and performs subtraction, resulting in `2`. This is because the `-` operator only works with numbers, while `+` can work with both strings and numbers.

</details>

---

**Q3.** What is the difference between `==` (loose equality) and `===` (strict equality)?

<details>
<summary>Answer</summary>

The `==` operator compares two values for equality after performing type coercion. This means it converts both values to a common type before comparing. For example, `"5" == 5` returns `true` because the string `"5"` is converted to the number `5` before comparison.

The `===` operator compares both the value and the data type without performing any type conversion. So `"5" === 5` returns `false` because a string is not the same type as a number. It is considered best practice to use `===` in most situations to avoid unexpected results caused by type coercion.

</details>

---

**Q4.** What are truthy and falsy values in JavaScript? List all the falsy values.

<details>
<summary>Answer</summary>

In JavaScript, every value has an inherent boolean identity. When evaluated in a boolean context (such as an `if` statement), a value is either considered "truthy" or "falsy."

A falsy value is one that evaluates to `false` when converted to a boolean. There are exactly six falsy values in JavaScript:
1. `false`
2. `0` (the number zero)
3. `""` (empty string)
4. `null`
5. `undefined`
6. `NaN`

Every other value is truthy, including `"0"` (a string containing zero), `"false"` (a string containing the word false), empty arrays `[]`, and empty objects `{}`.

</details>

---

**Q5.** What is a template literal and how is it different from a regular string?

<details>
<summary>Answer</summary>

A template literal is a special way to create strings in JavaScript, introduced in ES6. It uses backticks (`` ` ``) instead of single quotes (`'`) or double quotes (`"`).

Template literals have two major advantages over regular strings. First, they allow you to embed variables and expressions directly using the `${...}` syntax, which is called string interpolation. For example, `` `My name is ${name}` `` is much cleaner than `"My name is " + name`. Second, template literals can span multiple lines without needing special characters like `\n`.

</details>

---

**Q6.** Why is JavaScript not the same as Java?

<details>
<summary>Answer</summary>

Despite the similar names, JavaScript and Java are completely different programming languages. JavaScript was created by Brendan Eich at Netscape in 1995 and was originally named "Mocha," then "LiveScript." It was renamed to "JavaScript" as a marketing strategy to ride the popularity of Java at the time.

Java is a compiled, statically-typed, class-based object-oriented language primarily used for building desktop applications, Android apps, and enterprise backend systems. JavaScript is an interpreted, dynamically-typed, prototype-based language originally designed for adding interactivity to web pages. Today, JavaScript runs in browsers and on servers (via Node.js) and is a core language in web development stacks like MERN.

</details>

---

**Q7.** What is `NaN` in JavaScript? How can you check if a value is `NaN`?

<details>
<summary>Answer</summary>

`NaN` stands for "Not a Number." It is a special value in JavaScript that represents the result of an invalid or undefined mathematical operation. For example, `"hello" * 2` produces `NaN` because you cannot multiply a non-numeric string by a number.

Interestingly, `typeof NaN` returns `"number"`, and `NaN` is not equal to itself (`NaN === NaN` is `false`). To check if a value is `NaN`, you should use the `Number.isNaN()` function, which returns `true` only if the value is actually `NaN`. The older `isNaN()` function can give misleading results because it first tries to convert the value to a number.

</details>

---

**Q8.** What is the difference between `null` and `undefined` in JavaScript?

<details>
<summary>Answer</summary>

Both `null` and `undefined` represent the absence of a value, but they are used in different situations.

`undefined` means a variable has been declared but has not been assigned a value yet. JavaScript automatically assigns `undefined` to uninitialized variables. For example, `let x;` makes `x` equal to `undefined`.

`null` is an intentional assignment that represents "no value" or "empty." A developer explicitly sets a variable to `null` to indicate that it is deliberately empty. For example, `let user = null;` means the user variable exists but currently holds no data. Note that `typeof undefined` returns `"undefined"`, while `typeof null` returns `"object"` (which is a known JavaScript bug).

</details>

---

## Section C: What Is the Output?

**Instructions:** Read each code snippet carefully and predict the output. Then reveal the answer to check your understanding.

---

**Q1.**
```javascript
console.log("5" + 3);
```

<details>
<summary>Answer</summary>

**Output:** `53`

When the `+` operator encounters a string and a number, it converts the number to a string and performs concatenation instead of addition. The string `"5"` is joined with `"3"` to produce `"53"`.

</details>

---

**Q2.**
```javascript
console.log("5" - 3);
```

<details>
<summary>Answer</summary>

**Output:** `2`

Unlike `+`, the `-` operator does not work with strings. JavaScript converts the string `"5"` to the number `5` and then performs subtraction: `5 - 3 = 2`.

</details>

---

**Q3.**
```javascript
console.log(typeof null);
```

<details>
<summary>Answer</summary>

**Output:** `object`

This is a historical bug in JavaScript. `typeof null` returns `"object"` even though `null` is a primitive value and not an object. This has remained in the language for backward compatibility.

</details>

---

**Q4.**
```javascript
console.log(0 == false);
```

<details>
<summary>Answer</summary>

**Output:** `true`

The `==` operator performs type coercion. `false` is converted to the number `0`, and since `0 == 0` is `true`, the expression evaluates to `true`.

</details>

---

**Q5.**
```javascript
console.log("" == false);
```

<details>
<summary>Answer</summary>

**Output:** `true`

With loose equality (`==`), both the empty string `""` and `false` are converted to the number `0` during comparison. Since `0 == 0` is `true`, the result is `true`.

</details>

---

**Q6.**
```javascript
console.log(NaN === NaN);
```

<details>
<summary>Answer</summary>

**Output:** `false`

`NaN` is the only value in JavaScript that is not equal to itself. Both `NaN == NaN` and `NaN === NaN` return `false`. This is part of the IEEE 754 floating-point specification that JavaScript follows.

</details>

---

**Q7.**
```javascript
let x = 10;
let y = "10";
console.log(x == y);
console.log(x === y);
```

<details>
<summary>Answer</summary>

**Output:**
```
true
false
```

`x == y` returns `true` because the `==` operator converts the string `"10"` to the number `10` before comparing. `x === y` returns `false` because the `===` operator checks the type as well, and `number` is not the same as `string`.

</details>

---

**Q8.**
```javascript
console.log(typeof undefined);
console.log(typeof NaN);
```

<details>
<summary>Answer</summary>

**Output:**
```
undefined
number
```

`typeof undefined` returns `"undefined"` as expected. However, `typeof NaN` returns `"number"`, which is surprising because `NaN` stands for "Not a Number." Despite its name, `NaN` is technically of the number data type in JavaScript.

</details>

---

**Q9.**
```javascript
let a = "Hello";
let b = a;
b = "World";
console.log(a);
console.log(b);
```

<details>
<summary>Answer</summary>

**Output:**
```
Hello
World
```

Primitive values like strings are copied by value, not by reference. When `b = a` is executed, a copy of the value `"Hello"` is assigned to `b`. Changing `b` to `"World"` does not affect `a` because they are independent copies.

</details>

---

**Q10.**
```javascript
console.log(true + true);
console.log(true + false);
console.log(false + false);
```

<details>
<summary>Answer</summary>

**Output:**
```
2
1
0
```

When booleans are used with the `+` operator, JavaScript converts `true` to `1` and `false` to `0`. So `true + true` is `1 + 1 = 2`, `true + false` is `1 + 0 = 1`, and `false + false` is `0 + 0 = 0`.

</details>

---

## Section D: Code Correction

**Instructions:** Each code snippet below contains one or more errors. Find the errors and fix them.

---

**Q1.** The following code should print a greeting message but it has an error:

```javascript
const greeting = "Hello, World!";
greeting = "Hi, World!";
console.log(greeting);
```

<details>
<summary>Answer</summary>

**Error:** A `const` variable cannot be reassigned.

**Fixed Code:**
```javascript
let greeting = "Hello, World!";
greeting = "Hi, World!";
console.log(greeting);
```

Since the value of `greeting` needs to change, it should be declared with `let` instead of `const`.

</details>

---

**Q2.** The following code should calculate the sum of two numbers but it produces the wrong result:

```javascript
let num1 = "10";
let num2 = 20;
let sum = num1 + num2;
console.log("The sum is: " + sum);
```

<details>
<summary>Answer</summary>

**Error:** `num1` is a string, so the `+` operator performs string concatenation instead of addition. The result would be `"1020"` instead of `30`.

**Fixed Code:**
```javascript
let num1 = 10;
let num2 = 20;
let sum = num1 + num2;
console.log("The sum is: " + sum);
```

Alternatively, you can convert the string to a number using `Number(num1)`, `parseInt(num1)`, or the unary `+` operator (`+num1`).

</details>

---

**Q3.** The following code should print a multi-line message using a template literal but it has a syntax error:

```javascript
let name = "Ahmed";
let age = 20;
let message = 'My name is ${name}.
I am ${age} years old.';
console.log(message);
```

<details>
<summary>Answer</summary>

**Error:** Template literals require backticks (`` ` ``), not single quotes (`'`). With single quotes, `${name}` and `${age}` are treated as plain text.

**Fixed Code:**
```javascript
let name = "Ahmed";
let age = 20;
let message = `My name is ${name}.
I am ${age} years old.`;
console.log(message);
```

</details>

---

**Q4.** The following code should check if a number is even but it does not work correctly:

```javascript
let number = 7;
if (number % 2 = 0) {
  console.log("Even");
} else {
  console.log("Odd");
}
```

<details>
<summary>Answer</summary>

**Error:** The single `=` is the assignment operator, not the comparison operator. Inside the `if` condition, `==` or `===` should be used for comparison.

**Fixed Code:**
```javascript
let number = 7;
if (number % 2 === 0) {
  console.log("Even");
} else {
  console.log("Odd");
}
```

</details>

---

**Q5.** The following code should declare three variables and print them, but it contains multiple errors:

```javascript
Let myName = "Sara"
let my age = 25;
let city = Karachi;
console.log(myName, my age, city);
```

<details>
<summary>Answer</summary>

**Errors:**
1. `Let` should be `let` (JavaScript is case-sensitive).
2. Missing semicolon at the end of the first line (not an error in most cases, but inconsistent style).
3. `my age` is not a valid variable name because variable names cannot contain spaces.
4. `Karachi` is not wrapped in quotes, so JavaScript treats it as an undefined variable name.
5. `my age` in the `console.log` also has the same space issue.

**Fixed Code:**
```javascript
let myName = "Sara";
let myAge = 25;
let city = "Karachi";
console.log(myName, myAge, city);
```

</details>

---

## Section E: Coding Exercises

**Instructions:** Write JavaScript code to complete each task. Test your code in the browser console or a code editor.

---

**Task 1:** Declare variables for your name, age, and city. Print them in a single sentence using template literals.

<details>
<summary>Solution</summary>

```javascript
let name = "Ali";
let age = 22;
let city = "Lahore";

console.log(`My name is ${name}, I am ${age} years old, and I live in ${city}.`);
```

**Output:** `My name is Ali, I am 22 years old, and I live in Lahore.`

</details>

---

**Task 2:** Write a program to calculate the area of a rectangle given its length and width.

<details>
<summary>Solution</summary>

```javascript
let length = 10;
let width = 5;
let area = length * width;

console.log(`The area of the rectangle is ${area} square units.`);
```

**Output:** `The area of the rectangle is 50 square units.`

</details>

---

**Task 3:** Write a program to convert a temperature from Celsius to Fahrenheit using the formula: `F = (C * 9/5) + 32`.

<details>
<summary>Solution</summary>

```javascript
let celsius = 37;
let fahrenheit = (celsius * 9 / 5) + 32;

console.log(`${celsius}°C is equal to ${fahrenheit}°F.`);
```

**Output:** `37°C is equal to 98.6°F.`

</details>

---

**Task 4:** Write a program to swap the values of two variables without using a third (temporary) variable.

<details>
<summary>Solution</summary>

```javascript
let a = 5;
let b = 10;

console.log(`Before swap: a = ${a}, b = ${b}`);

a = a + b;  // a = 15
b = a - b;  // b = 5
a = a - b;  // a = 10

console.log(`After swap: a = ${a}, b = ${b}`);
```

**Output:**
```
Before swap: a = 5, b = 10
After swap: a = 10, b = 5
```

**Alternative (ES6 destructuring):**
```javascript
let a = 5;
let b = 10;
[a, b] = [b, a];
console.log(`a = ${a}, b = ${b}`);
```

</details>

---

**Task 5:** Write a program to check if a number is even or odd using the modulus operator (`%`).

<details>
<summary>Solution</summary>

```javascript
let number = 15;

if (number % 2 === 0) {
  console.log(`${number} is even.`);
} else {
  console.log(`${number} is odd.`);
}
```

**Output:** `15 is odd.`

</details>

---

**Task 6:** Write a program to find the length of a string and convert it to uppercase.

<details>
<summary>Solution</summary>

```javascript
let message = "hello world";

let length = message.length;
let uppercased = message.toUpperCase();

console.log(`Original string: "${message}"`);
console.log(`Length: ${length}`);
console.log(`Uppercase: "${uppercased}"`);
```

**Output:**
```
Original string: "hello world"
Length: 11
Uppercase: "HELLO WORLD"
```

</details>

---

**Task 7:** Write a program to generate a random number between 1 and 100.

<details>
<summary>Solution</summary>

```javascript
let randomNumber = Math.floor(Math.random() * 100) + 1;

console.log(`Random number between 1 and 100: ${randomNumber}`);
```

**Explanation:** `Math.random()` generates a decimal between 0 (inclusive) and 1 (exclusive). Multiplying by 100 gives a range of 0 to 99.99. `Math.floor()` rounds down to the nearest integer (0 to 99). Adding 1 shifts the range to 1 to 100.

</details>

---

**Task 8:** Write a program to calculate simple interest using the formula: `SI = (P * R * T) / 100`.

<details>
<summary>Solution</summary>

```javascript
let principal = 10000;
let rate = 5;
let time = 3;

let simpleInterest = (principal * rate * time) / 100;
let totalAmount = principal + simpleInterest;

console.log(`Principal: ${principal}`);
console.log(`Rate: ${rate}%`);
console.log(`Time: ${time} years`);
console.log(`Simple Interest: ${simpleInterest}`);
console.log(`Total Amount: ${totalAmount}`);
```

**Output:**
```
Principal: 10000
Rate: 5%
Time: 3 years
Simple Interest: 1500
Total Amount: 11500
```

</details>

---

**Task 9:** Write a program to extract the first name from a full name string using string methods.

<details>
<summary>Solution</summary>

```javascript
let fullName = "Muhammad Ahmed Khan";

let firstName = fullName.split(" ")[0];

console.log(`Full Name: ${fullName}`);
console.log(`First Name: ${firstName}`);
```

**Output:**
```
Full Name: Muhammad Ahmed Khan
First Name: Muhammad
```

**Explanation:** The `split(" ")` method splits the string at every space and returns an array: `["Muhammad", "Ahmed", "Khan"]`. Using `[0]` accesses the first element, which is the first name. Alternatively, you could use `fullName.slice(0, fullName.indexOf(" "))` to achieve the same result.

</details>

---

**Task 10:** Create a program that takes a price and a tax rate, then calculates and displays the total price including tax.

<details>
<summary>Solution</summary>

```javascript
let price = 1500;
let taxRate = 17;

let taxAmount = (price * taxRate) / 100;
let totalPrice = price + taxAmount;

console.log(`Original Price: Rs. ${price}`);
console.log(`Tax Rate: ${taxRate}%`);
console.log(`Tax Amount: Rs. ${taxAmount}`);
console.log(`Total Price: Rs. ${totalPrice}`);
```

**Output:**
```
Original Price: Rs. 1500
Tax Rate: 17%
Tax Amount: Rs. 255
Total Price: Rs. 1755
```

</details>

---

**End of Practice Questions**

> **Tip:** Try solving each question on your own before checking the answers. Practice writing the code in your browser console or a code editor like VS Code. The more you practice, the stronger your JavaScript fundamentals will become.
