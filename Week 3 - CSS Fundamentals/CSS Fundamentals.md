# CSS — Complete Guide for Beginners

## 📌 What is CSS?

CSS (Cascading Style Sheets) is a language used to **style and design web pages**.

HTML gives **structure**, CSS gives **style**.

👉 Real-life example:
Think of a **house**.

* The walls and rooms are HTML (structure)
* Paint, colors, furniture are CSS (style)

---

## 🎯 Why Do We Use CSS?

CSS makes a website look **beautiful, clean, and professional**.

With CSS you can:

* Change colors
* Change size of text
* Add spacing
* Align elements
* Make the layout responsive

👉 Without CSS → website looks like a plain document.
👉 With CSS → website looks like a modern web app.

---

## 🧩 CSS Syntax

A CSS rule has 3 parts:

```css
selector {
  property: value;
}
```

✔ **Selector** → selects the element
✔ **Property** → what you want to change
✔ **Value** → how you want to change it

Example:

```css
p {
  color: blue;
}
```

This changes all `<p>` text to blue.

---

## 🎯 CSS Selectors

Selectors are used to **select HTML elements**.

### 1. Universal Selector

Selects **all elements**.

```css
* {
  margin: 0;
  padding: 0;
}
```

### 2. Tag Selector

Selects by **tag name**.

```css
p {
  font-size: 18px;
}
```

### 3. Class Selector

Selects by **class**.

```html
<p class="title">Welcome</p>
```

```css
.title {
  color: blue;
}
```

### 4. ID Selector

Selects by **id** (unique).

```html
<p id="main">Hello</p>
```

```css
#main {
  color: red;
}
```

---

## 📁 Three Ways to Insert CSS

### 1. External CSS (Best Practice)

Write CSS in a **separate file**.

```html
<link rel="stylesheet" href="style.css">
```

### 2. Internal CSS

Write inside `<style>` tag.

```html
<style>
h1 { color: green; }
</style>
```

### 3. Inline CSS

Write inside the tag.

```html
<p style="color: orange;">Hello</p>
```

---

## 💬 CSS Comments

Used to explain code.

```css
/* This is a comment */
```

---

## 🎨 Colors

### Text Color

```css
p {
  color: red;
}
```

### Background Color

```css
body {
  background-color: lightgray;
}
```

---

## 📏 Height, Width, Margin, Padding

### Height & Width

```css
div {
  height: 200px;
  width: 300px;
}
```

### Margin (Outside Space)

```css
div {
  margin: 20px;
}
```

### Padding (Inside Space)

```css
div {
  padding: 15px;
}
```

👉 Real-life example:

* **Margin** = space between cars in a parking lot
* **Padding** = space between the seat and the car door

---

## 🔲 Border

```css
div {
  border: 2px solid black;
}
```

---

## 📝 Text Alignment

```css
p {
  text-align: center;
}
```

---

## 🔤 Text Properties

```css
p {
  text-transform: uppercase;
  letter-spacing: 2px;
}
```

---

## ✍️ Fonts

```css
body {
  font-family: Arial;
  font-size: 16px;
}
```

---

## 🧩 Icons

Use Font Awesome:

```html
<link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/font-awesome/6.0.0/css/all.min.css">

<i class="fa-solid fa-house"></i>
```

---

## 📊 Tables

```html
<table>
  <tr><th>Name</th><th>Age</th></tr>
  <tr><td>Ali</td><td>20</td></tr>
</table>
```

```css
table {
  border-collapse: collapse;
}
th, td {
  border: 1px solid black;
  padding: 10px;
}
```

---

## 📜 Lists

### Unordered List

```html
<ul>
  <li>Apple</li>
  <li>Mango</li>
</ul>
```

### Ordered List

```html
<ol>
  <li>Step 1</li>
  <li>Step 2</li>
</ol>
```

---

## 🎉 Summary

CSS is used to:

* Style web pages
* Control layout
* Make websites responsive
* Improve user experience

**Learn once → use forever in web development** 🚀

---

# 🏋️‍♂️ Beginner-Friendly Practice Questions

## 1️⃣ Selectors Practice

* Use universal selector to reset margin and padding
* Style a paragraph using tag selector
* Style multiple elements using class selector
* Style a unique element using ID selector

## 2️⃣ Colors & Background

* Create a `<div>` with yellow background and black text
* Change color of a heading to green

## 3️⃣ Height, Width, Margin & Padding

* Create a box 200px by 200px
* Add margin 20px and padding 15px

## 4️⃣ Border Practice

* Create a card with 2px solid border and 10px border radius

## 5️⃣ Text & Font Practice (Beginner-Friendly)

* Center align a heading
* Make paragraph text uppercase with letter spacing 2px
* Apply font-family Arial and font-size 18px

## 6️⃣ Tables & Lists

* Create a table with 2 rows, 2 columns, and add border
* Make an ordered and unordered list with 3 items each

## 7️⃣ Buttons & Hover Effects

* Create a button with background blue, text white, padding 10px
* Add hover effect to change background to dark blue

---

# 💡 Challenge Task

Create a simple webpage containing:

* Heading
* Paragraph
* Button
* Box with border
* Ordered and unordered list
* All styles applied using **external CSS**

🎯 Goal: Make it **clean, responsive, and visually appealing**.
