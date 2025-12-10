# CSS Properties — Simple Guide with Examples

This document explains the main CSS properties using simple language, real-world examples, and code examples.

---

## 🎨 Text Properties

Text properties control how text looks.

### Common Types:

* **color** — change text color
* **text-align** — left, center, right, justify
* **text-decoration** — underline, line-through, overline
* **text-transform** — uppercase, lowercase, capitalize
* **line-height** — spacing between lines
* **letter-spacing** — spacing between letters
* **text-shadow** — shadow behind text

### Real World Example:

Newspaper headings are centered, paragraphs are justified.

### Example Code:

```css
h1 {
  color: blue;
  text-align: center;
  text-transform: uppercase;
  letter-spacing: 3px;
  text-shadow: 2px 2px 4px gray;
}

p {
  color: darkgreen;
  line-height: 1.8;
  text-decoration: underline;
}
```

---

## 🔤 Font Properties

Font properties control the size, style and family of text.

### Common Types:

* **font-family** — Arial, Verdana, etc.
* **font-size** — how big text is
* **font-weight** — boldness
* **font-style** — normal or italic
* **font-variant** — small-caps

### Example Code:

```css
body {
  font-family: Arial, sans-serif;
}

h2 {
  font-size: 35px;
  font-weight: bold;
  font-style: italic;
}
```

---

## 🔧 Icon Properties

Icons usually come from libraries like **Font Awesome**.

### Example Code:

```html
<link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/font-awesome/6.0.0/css/all.min.css">

<i class="fa fa-home"></i>
<i class="fa fa-phone"></i>
```

### Style Icons:

```css
i {
  font-size: 30px;
  color: red;
}
```

---

## 🖼️ Background Properties

Background controls what is behind an element.

### Common Types:

* **background-color**
* **background-image**
* **background-size** — cover, contain
* **background-repeat** — repeat, no-repeat
* **background-position** — left, center, right
* **background-attachment** — fixed, scroll

### Example Code:

```css
div {
  height: 200px;
  background-image: url("wall.jpg");
  background-size: cover;
  background-repeat: no-repeat;
  background-position: center;
}
```

---

## 📦 Margin Properties

Margin is **space outside the box**.

### Types:

* margin-top
* margin-right
* margin-bottom
* margin-left
* margin

### Example Code:

```css
.box {
  background-color: lightblue;
  margin: 40px;
}
```

---

## 📐 Height & Width

Controls the size of elements.

### Example Code:

```css
.box {
  background-color: lightgreen;
  height: 150px;
  width: 300px;
}
```

---

## 🧊 Padding Properties

Padding is **space inside the box**, around content.

### Types:

* padding-top
* padding-right
* padding-bottom
* padding-left
* padding

### Example Code:

```css
.box {
  border: 2px solid black;
  padding: 20px;
}
```

---

## 📦 Box Model

Every HTML element is a **box**.

### Layers:

1. Content
2. Padding
3. Border
4. Margin

### Real World:

Gift box example:

* Gift = content
* Bubble wrap = padding
* Box walls = border
* Space on table = margin

### Example Code:

```css
.box {
  height: 120px;
  width: 220px;
  background-color: lightyellow;
  padding: 20px;
  border: 3px solid brown;
  margin: 30px;
}
```

---

## 📝 Practice Questions

### Theory Questions

1. What is the difference between **margin** and **padding**?
2. What is the purpose of **background-size: cover**?
3. How does **text-transform: uppercase** work?
4. What is the difference between **font-weight** and **font-style**?
5. What is the Box Model? Name all 4 parts.

### Write CSS Code

1. Make a heading center aligned, red, and uppercase.
2. Create a div with:

   * height: 200px
   * width: 300px
   * background-color: yellow
3. Add a phone icon and make it 40px size.
4. Add 20px padding and 10px margin to a box.
5. Use a background image that does not repeat and stays fixed.

### Output Prediction

#### Q1:

```css
p {
  margin: 50px;
  padding: 0;
}
```

What is the result?

#### Q2:

```css
h1 {
  text-shadow: 5px 5px 8px black;
}
```

What effect will you see?

#### Q3:

```css
.box {
  width: 100px;
  max-width: 50px;
}
```

Which width will apply?


