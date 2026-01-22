# Objects in JavaScript

## Introduction

An **object** is a collection of **key–value pairs** used to represent real-world entities.

### Real-Life Example

A **student** has properties:

* name
* age
* roll number
* course

In JavaScript, we store this information using objects.

---

## Why Objects Are Important

* Represent real-world data
* Used everywhere (APIs, JSON, databases)
* Core concept for frontend & backend
* Very important for interviews

---

## 1. Creating an Object

### Object Literal (Most Common)

```js
let student = {
  name: "Fahad",
  age: 22,
  course: "JavaScript"
};
```

---

## 2. Accessing Object Properties

### Dot Notation

```js
console.log(student.name);
```

### Bracket Notation

```js
console.log(student["age"]);
```

📌 Use bracket notation when property name is dynamic.

---

## 3. Modifying Object Properties

```js
student.age = 23;
student.city = "Karachi";
```

---

## 4. Deleting Properties

```js
delete student.course;
```

---

## 5. Objects with Methods

Objects can store functions as values.

```js
let user = {
  username: "admin",
  login() {
    console.log("Login successful");
  }
};

user.login();
```

---

## 6. The `this` Keyword

`this` refers to the **current object**.

```js
let car = {
  brand: "Toyota",
  showBrand() {
    console.log(this.brand);
  }
};
```

---

## 7. Looping Through Objects

### for...in Loop

```js
for (let key in student) {
  console.log(key + ": " + student[key]);
}
```

---

## 8. Object Destructuring

```js
let { name, age } = student;
```

---

## 9. Spread Operator with Objects

```js
let extra = { city: "Karachi" };
let updatedStudent = { ...student, ...extra };
```

---

## 10. Nested Objects

```js
let company = {
  name: "TechSoft",
  address: {
    city: "Karachi",
    country: "Pakistan"
  }
};

console.log(company.address.city);
```

---

## 11. Object Methods (Built-in)

### Object.keys()

```js
Object.keys(student);
```

### Object.values()

```js
Object.values(student);
```

### Object.entries()

```js
Object.entries(student);
```

---

## 12. Objects vs Arrays

| Feature  | Object          | Array          |
| -------- | --------------- | -------------- |
| Stores   | Key–value       | Indexed values |
| Access   | By key          | By index       |
| Use case | Structured data | Lists          |

---

## Best Practices

* Use meaningful keys
* Avoid deep nesting when possible
* Prefer destructuring
* Keep objects immutable if possible

---

## Practice Questions

### Basic

1. Create an object for a book (title, author, price)
2. Access and update object properties

### Intermediate

3. Loop through object and print keys & values
4. Add a method to calculate discount

### Advanced

5. Create nested object for university structure
6. Merge two objects using spread operator

---

## Mini Assignment

Create an object-based program that:

* Stores user profile data
* Has login method
* Updates profile info
* Displays full user details

---

## Key Takeaways

* Objects store real-world data
* `this` connects object to its data
* Destructuring & spread are must-know
* Objects are everywhere in JavaScript

---

Happy Coding 🚀
