
## 1. What is HTML?

**HTML (HyperText Markup Language)** is the language used to **structure content on websites**.

### 🔧 Real-Life Example

* HTML = Structure of the house (walls, rooms)
* CSS = Decoration & paint
* JavaScript = Electricity & appliances

---

## 2. HTML Tags

HTML tags tell the browser **how content should appear**.

### Syntax

```html
<tagname>Content</tagname>
```

### Example

```html
<p>Hello World!</p>
```

---

## 3. Types of HTML Tags

### 3.1 Text Formatting Tags

| Tag                | Purpose         | Example            |
| ------------------ | --------------- | ------------------ |
| `<h1>`-`<h6>`      | Headings        | Page titles        |
| `<p>`              | Paragraph       | Article text       |
| `<b>` / `<strong>` | Bold            | Important text     |
| `<i>` / `<em>`     | Italic          | Quotes             |
| `<br>`             | Line break      | Address formatting |
| `<hr>`             | Horizontal line | Section breaker    |

---

### 3.2 Container Tags

| Tag         | Purpose             | Example        |
| ----------- | ------------------- | -------------- |
| `<div>`     | Block container     | Page layout    |
| `<span>`    | Inline container    | Highlight word |
| `<section>` | Page section        | Services area  |
| `<article>` | Independent content | Blog post      |
| `<header>`  | Top section         | Website header |
| `<footer>`  | Bottom section      | Contact info   |
| `<main>`    | Main page           | Main article   |
| `<nav>`     | Navigation links    | Menu bar       |
| `<aside>`   | Side content        | Ads, links     |

---

### 3.3 Link & Media Tags

| Tag        | Purpose    | Example            |
| ---------- | ---------- | ------------------ |
| `<a>`      | Hyperlink  | Go to another page |
| `<img>`    | Image      | Display picture    |
| `<video>`  | Video      | Embedded video     |
| `<audio>`  | Audio      | Music player       |
| `<iframe>` | Embed page | YouTube            |

---

### 3.4 Lists

| Tag    | Purpose        |
| ------ | -------------- |
| `<ul>` | Unordered list |
| `<ol>` | Ordered list   |
| `<li>` | List item      |

---

### 3.5 Tables

| Tag       | Purpose         |
| --------- | --------------- |
| `<table>` | Table container |
| `<tr>`    | Table row       |
| `<td>`    | Table cell      |
| `<th>`    | Table header    |
| `<thead>` | Header area     |
| `<tbody>` | Data rows       |
| `<tfoot>` | Summary         |

---

### 3.6 Forms

| Tag          | Purpose         |
| ------------ | --------------- |
| `<form>`     | Form container  |
| `<input>`    | Input field     |
| `<textarea>` | Message box     |
| `<button>`   | Button          |
| `<label>`    | Label for input |
| `<select>`   | Dropdown        |
| `<option>`   | Dropdown option |

🔑 **Input types:** text, email, password, number, checkbox, radio, file, submit.

---

## 4. Must-Know Attributes

* `id`
* `class`
* `style`
* `href`
* `src`
* `alt`
* `title`
* `value`
* `placeholder`
* `type`

---

## 5. Semantic vs Non-Semantic Tags

### Semantic Tags

Meaningful tags → better structure & SEO.

Examples:
`header`, `footer`, `nav`, `section`, `article`, `aside`, `main`

**Example:**

```html
<header>
  <h1>My Website</h1>
</header>
```

### Non-Semantic Tags

No meaning → only layout.

Examples:
`div`, `span`

---

## 6. Inline vs Block Elements

### Block-Level

* Start on new line
* Full width

Examples: `div`, `p`, `section`, `article`

### Inline

* Stay on same line

Examples: `span`, `a`, `img`, `strong`

---

## 7. Class vs ID

### Class

* Used many times

```html
<p class="highlight">Hello</p>
```

### ID

* Unique

```html
<p id="title">Main title</p>
```

---

## 8. Forms

Forms collect user input.

```html
<form action="/submit" method="post"></form>
```

### Most Common Inputs

* Text
* Email
* Password
* Radio
* Checkbox
* Dropdown
* Textarea
* Submit Button

---

## 9. Complete Form Example

```html
<form action="/submit" method="post">

<label>Name:</label>
<input type="text" required>
<br>

<label>Email:</label>
<input type="email" required>
<br>

<button type="submit">Submit</button>

</form>
```

---

# 📝 Practical Exercises

## 1️⃣ Text Formatting

Create a page with:

* `<h1>` Your Name
* `<h2>` Your Profession
* `<p>` Introduction
* Bold & italic words
* `<hr>` line

---

## 2️⃣ Lists & Links

* Create `<ul>` of 5 foods
* Create `<ol>` steps to make tea
* Add a link that opens in new tab

---

## 3️⃣ Images

* Add a profile picture using `<img>`
* Add `alt` and `title`

---

## 4️⃣ Forms

Create:

* Name
* Email
* Message
* Submit button

---

## 5️⃣ Mini Projects

* Personal bio page
* Favorite hobby post
* Product table
* Contact form
* Simple portfolio

---

# 🎯 Beginner Tips

* Close your tags
* Use semantic tags
* Indent properly
* Test in browser often

---

## End of Document ✔
