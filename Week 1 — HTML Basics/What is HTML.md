

## 🎯 What you will learn (simple)

* What HTML is and why we use it
* What tags, elements, and attributes are
* Difference between block and inline elements
* How to make a simple form to collect names
* Examples you can copy and try

---

## 🧠 What is HTML?

HTML stands for **HyperText Markup Language**. It is like the bones of a webpage — it tells a browser what parts are headings, paragraphs, images, and links.

**Think:** If a webpage is a storybook, HTML is the book’s pages and chapters.

---

## 📚 Easy core ideas

### 1) Tags — the building blocks

Tags look like this: `<tag>` and most have a closing tag `</tag>`.

**Example:**

```html
<p>This is a paragraph.</p>
```

* `<p>` is the opening tag.
* `</p>` is the closing tag.
* The text in the middle is the content.

**Real-life:** A tag is like a label on a box that says what is inside.

---

### 2) Elements — a full piece

An element is the opening tag + content + closing tag.

**Example:** `<h1>My Title</h1>` is an element.

**Real-life:** An element is like a full room (walls + furniture).

---

### 3) Attributes — extra details

Attributes give more information inside the opening tag. They look like `name="value"`.

**Example:**

```html
<a href="https://example.com" target="_blank">Visit</a>
<img src="photo.jpg" alt="My Photo">
```

* `href` tells where the link goes.
* `src` tells where the image file is.

**Real-life:** Attributes are like signs on a door that say “Staff Only” or “Push / Pull”.

---

## 🧩 Types of tags (easy)

1. **Paired tags** — have opening and closing:

```html
<p>Hi</p>
```

2. **Self-closing tags** — no closing tag needed:

```html
<img src="pic.jpg" alt="pic">
<br>
```

**Real-life:** Paired = box with lid. Self-closing = sticker.

---

## 🧱 Block vs Inline (very simple)

* **Block elements** start on a new line and take full width.

  * Examples: `<div>`, `<p>`, `<h1>`
  * Real-life: A full wall.

* **Inline elements** stay in the same line and take only needed space.

  * Examples: `<span>`, `<a>`, `<img>`
  * Real-life: A poster on the wall.

**Try this:** Copy and paste in a file to see difference:

```html
<p>This is a paragraph. <span>Inline text here</span> More paragraph text.</p>
<div>This is a div</div>
<div>This is another div</div>
```

---

## 🏷 Common tags with simple examples (copy and try)

* Headings: `<h1>Big title</h1>` up to `<h6>`
* Paragraph: `<p>This is a paragraph.</p>`
* Link: `<a href="https://example.com">Click me</a>`
* Image: `<img src="photo.jpg" alt="photo">`
* Unordered list:

```html
<ul>
  <li>Apple</li>
  <li>Banana</li>
</ul>
```

* Ordered list:

```html
<ol>
  <li>First</li>
  <li>Second</li>
</ol>
```

* Container: `<div>Section content</div>`
* Inline: `<span>small text</span>`

**Real-life short analogies:**

* Heading = chapter title
* Paragraph = a paragraph in a book
* Link = a road sign to another page
* Image = a photo on the wall
* List = grocery list or recipe steps

---

## 📝 Forms — collect input from users

A form lets us ask users for information like name or email.

**Simple form example:**

```html
<form>
  <label for="name">Name:</label>
  <input type="text" id="name" name="name" placeholder="Enter your name">
  <br>
  <label for="age">Age:</label>
  <input type="number" id="age" name="age">
  <br>
  <button type="submit">Send</button>
</form>
```

### Common input types (with short meaning):

* `text` — for short words or names
* `number` — for numbers
* `email` — email addresses
* `password` — hidden text for passwords
* `checkbox` — choose many options
* `radio` — choose one of many
* `date` — pick a date
* `file` — upload a file or image

**Real-life:** A form is like a school registration paper where you write name, age and class.

---

## ✅ Small Tasks (easy)

1. Make a file `intro.html`. Add:

   * `<h1>` with your name
   * A short `<p>` about your hobby
   * An `<img>` (any photo) with `alt`
   * A link to your favourite website

2. Make `list.html` with:

   * An unordered list of 3 favourite foods
   * An ordered list of steps to make tea

3. Make `form.html` with a form that asks for name and age. Add comments to explain each line.

---



