# JSON (JavaScript Object Notation)

## What is JSON?

JSON (JavaScript Object Notation) is a **lightweight data-interchange format** used to store and exchange data between a **client and a server**. It is easy for humans to read and write, and easy for machines to parse and generate.

JSON is language-independent but is **based on JavaScript object syntax**, which makes it very popular in web development.

---

## Why JSON is Important

* Used in **APIs and web services**
* Common format for **frontend–backend communication**
* Lightweight and fast compared to XML
* Supported by almost **all programming languages**

---

## JSON Data Types

JSON supports the following data types:

* String
* Number
* Boolean
* Null
* Object
* Array

Example:

```json
{
  "name": "Fahad",
  "age": 22,
  "isStudent": true,
  "skills": ["Python", "Cyber Security", "Web Development"],
  "address": null
}
```

---

## JSON vs JavaScript Object

| Feature   | JSON                          | JavaScript Object          |
| --------- | ----------------------------- | -------------------------- |
| Quotes    | Keys must be in double quotes | Keys may be without quotes |
| Functions | Not allowed                   | Allowed                    |
| Usage     | Data transfer                 | Logic + data               |

---

## JSON Syntax Rules

* Data is in **key-value pairs**
* Keys must be **strings in double quotes**
* Values must be valid JSON data types
* No comments allowed

❌ Invalid JSON:

```json
{
  name: "Ali" // comment not allowed
}
```

✅ Valid JSON:

```json
{
  "name": "Ali"
}
```

---

## Working with JSON in JavaScript

### Convert Object to JSON (stringify)

```javascript
const user = { name: "Fahad", role: "Developer" };
const jsonData = JSON.stringify(user);
console.log(jsonData);
```

### Convert JSON to Object (parse)

```javascript
const data = '{"name":"Fahad","role":"Developer"}';
const obj = JSON.parse(data);
console.log(obj.name);
```

---

## JSON in APIs

Most APIs send and receive data in JSON format.

Example API Response:

```json
{
  "status": "success",
  "data": {
    "id": 1,
    "username": "fahad_dev"
  }
}
```

---

## Common Use Cases

* REST APIs
* Configuration files
* AJAX / Fetch requests
* Mobile & web applications

---

## Best Practices

* Keep JSON structure **simple and clean**
* Use meaningful key names
* Avoid deeply nested objects
* Validate JSON before using

---

## Practice Questions

### Basic

1. What is JSON and why is it used?
2. List all JSON data types.
3. Is JSON language dependent? Explain.

### Intermediate

4. Convert a JavaScript object into JSON.
5. Parse a JSON string into an object.
6. Identify errors in an invalid JSON file.

### Practical

7. Create a JSON object for a student (name, age, courses).
8. Write JavaScript code to fetch JSON data from an API.
9. Store and retrieve JSON data using `localStorage`.

---

## Summary

JSON is the backbone of modern web communication. Understanding JSON is **mandatory** for frontend, backend, API development, and cybersecurity workflows.

> If you know JSON well, APIs become easy. 🚀
