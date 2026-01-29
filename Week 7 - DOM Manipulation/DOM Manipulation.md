# DOM Manipulation

## What is the DOM?

DOM stands for **Document Object Model**. It is a programming interface for web documents that represents the structure of an HTML page as a tree of objects. Using the DOM, JavaScript can **access, change, add, or remove** HTML elements and attributes dynamically.

In simple words: **DOM allows JavaScript to interact with HTML and CSS.**

---
![DOM Manipulation Diagram](https://tse4.mm.bing.net/th/id/OIP.m3kU2N2lwM_8lqX8-ZIXZQHaFM?rs=1&pid=ImgDetMain&o=7&rm=3)


## Why DOM Manipulation is Important?

* Makes web pages **interactive**
* Allows **dynamic content updates** without reloading the page
* Used in forms, animations, validations, dashboards, and SPAs
* Core concept for modern frameworks (React, Angular, Vue)

---

## DOM Tree Structure

An HTML document is represented as a tree:

* Document

  * HTML

    * Head
    * Body

      * Elements (div, p, h1, etc.)

Each part of the HTML becomes a **node** in the DOM tree.

---

## Accessing DOM Elements

### By ID

```javascript
document.getElementById("title");
```

### By Class Name

```javascript
document.getElementsByClassName("box");
```

### By Tag Name

```javascript
document.getElementsByTagName("p");
```

### Using Query Selector

```javascript
document.querySelector(".box");
document.querySelectorAll(".box");
```

---

## Changing HTML Content

### Change Text

```javascript
element.innerText = "Hello World";
```

### Change HTML

```javascript
element.innerHTML = "<b>Hello</b>";
```

---

## Changing Attributes

```javascript
element.setAttribute("class", "active");
element.getAttribute("id");
element.removeAttribute("disabled");
```

---

## Changing CSS Styles

```javascript
element.style.color = "red";
element.style.backgroundColor = "yellow";
```

---

## Creating and Removing Elements

### Create Element

```javascript
let div = document.createElement("div");
div.innerText = "New Element";
document.body.appendChild(div);
```

### Remove Element

```javascript
element.remove();
```

---

## Event Handling

### Click Event

```javascript
element.addEventListener("click", function () {
  alert("Button Clicked");
});
```

### Common Events

* click
* submit
* mouseover
* keydown
* load

---

## Form Handling Example

```javascript
document.querySelector("form").addEventListener("submit", function(e) {
  e.preventDefault();
  console.log("Form Submitted");
});
```

---

## DOM vs BOM

| DOM             | BOM                |
| --------------- | ------------------ |
| Works with HTML | Works with browser |
| document object | window object      |
| Page structure  | Browser features   |

---

## Best Practices

* Use `querySelector` for cleaner code
* Avoid inline JavaScript
* Minimize direct DOM manipulation for performance
* Use event delegation when possible

---

## Conclusion

DOM Manipulation is a fundamental concept in JavaScript that enables developers to create dynamic and interactive web applications. Mastering DOM operations is essential before moving to advanced frameworks.

---

📌 **Next Topics:**

* Event Bubbling & Capturing
* DOM Traversing
* Local Storage
* Async JavaScript
