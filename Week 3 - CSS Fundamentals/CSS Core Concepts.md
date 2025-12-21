# CSS Core Concepts – README

---

## 1. CSS Units

CSS units define the size of elements like width, height, margin, padding, and font size.

### Types of Units

### Absolute Units (Fixed)

* `px` (pixel)

```css
p {
  font-size: 16px;
}
```

**Point:** Absolute units do not change automatically.

---

### Relative Units (Responsive)

These units change according to screen, browser, or parent element.

* `%` → relative to parent
* `em` → relative to parent font size
* `rem` → relative to root (html) font size
* `vw` → viewport width
* `vh` → viewport height

```css
div { width: 50%; }
h1 { font-size: 2rem; }
section { height: 100vh; }
```

**Default browser font size:** `16px`

---

## 2. Display Property

The `display` property controls how an element appears on the screen.

### Common Display Values

### `block`

* Starts on a new line
* Takes full width

Examples: `div`, `p`, `h1`

### `inline`

* Stays in same line
* Width/height do not work

Examples: `span`, `a`

### `inline-block`

* Same line
* Width/height work

Examples: `img`, `button`, `input`

### `none`

* Completely hides element

### `flex`

* One‑dimensional layout

### `grid`

* Two‑dimensional layout

---

## 3. Flexbox

### What is Flexbox?

Flexbox is a layout system used to align items in a **row or column**.

```css
.container {
  display: flex;
}
```

### When to Use Flexbox

* Navbar
* Buttons in a row
* Cards alignment
* Centering elements

### Why Use Flexbox?

* Easy alignment
* Responsive design
* Less CSS code

---

### Flexbox Container Properties

* `display: flex`
* `flex-direction`
* `flex-wrap`
* `justify-content`
* `align-items`
* `align-content`
* `gap`

### Flexbox Item Properties

* `order`
* `flex-grow`
* `flex-shrink`
* `flex-basis`
* `flex`
* `align-self`

---

## 4. CSS Grid

### What is Grid?

CSS Grid is a **two‑dimensional layout system** (rows + columns).

```css
.container {
  display: grid;
}
```

### When to Use Grid

* Full page layout
* Dashboards
* Image galleries
* Website structure

---

### Grid Container Properties

* `grid-template-columns`
* `grid-template-rows`
* `gap`
* `justify-items`
* `align-items`
* `justify-content`
* `align-content`
* `grid-template-areas`

### Grid Item Properties

* `grid-column`
* `grid-row`
* `grid-area`
* `justify-self`
* `align-self`

### `fr` Unit

* Fraction of available space

```css
grid-template-columns: 1fr 2fr;
```

---

## 5. Position Property

The `position` property controls the exact placement of elements.

### Position Types

### `static`

* Default position

### `relative`

* Moves relative to itself

### `absolute`

* Moves relative to nearest positioned parent

### `fixed`

* Fixed to viewport

### `sticky`

* Scroll then stick

```css
.box {
  position: absolute;
  top: 0;
  right: 0;
}
```

---

## 6. Flex vs Grid (Quick Review)

| Flexbox         | Grid             |
| --------------- | ---------------- |
| One‑dimensional | Two‑dimensional  |
| Row OR column   | Rows AND columns |
| Small layouts   | Full layouts     |

---

## Final Summary

This README covers:

* CSS Units
* Display property
* Flexbox
* Grid
* Position property

These topics together form the **core foundation of CSS layouts**.

---

Happy Learning 🚀
