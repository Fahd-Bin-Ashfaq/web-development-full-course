# 🎨 CSS Core Concepts – Complete README

This document covers the **core foundations of CSS layouts** with clear explanations of:

* What each property does
* When to use it
* Available values
* Simple, real-world examples

---

## 1. CSS Units

CSS units define the size of elements such as width, height, margin, padding, and font-size.

### Absolute Units (Fixed)

#### `px` (pixel)

```css
p {
  font-size: 16px;
}
```

**Note:** Absolute units do not change with screen size.

---

### Relative Units (Responsive)

Relative units adapt based on parent, root, or viewport.

| Unit  | Relative To           |
| ----- | --------------------- |
| `%`   | Parent element        |
| `em`  | Parent font-size      |
| `rem` | Root (html) font-size |
| `vw`  | Viewport width        |
| `vh`  | Viewport height       |

```css
div { width: 50%; }
h1 { font-size: 2rem; }
section { height: 100vh; }
```

**Default browser font-size:** `16px`

---

## 2. Display Property

Controls how an element appears and behaves in layout.

### `block`

* Starts on a new line
* Takes full width

```css
div {
  display: block;
}
```

---

### `inline`

* Same line
* Width and height do not work

```css
span {
  display: inline;
}
```

---

### `inline-block`

* Same line
* Width and height work

```css
button {
  display: inline-block;
  width: 120px;
}
```

---

### `none`

* Completely removes element from layout

```css
.modal {
  display: none;
}
```

---

### `flex`

* One-dimensional layout (row OR column)

### `grid`

* Two-dimensional layout (rows AND columns)

---

## 3. Flexbox

### What is Flexbox?

Flexbox is a **one-dimensional layout system** used for arranging items in a row or column.

```css
.container {
  display: flex;
}
```

### When to Use Flexbox

* Navigation bars
* Button groups
* Cards alignment
* Centering elements

---

## Flexbox Container Properties (Parent)

### `flex-direction`

Defines the main axis direction.

**Values:**

* `row` (default)
* `row-reverse`
* `column`
* `column-reverse`

```css
.container {
  flex-direction: row;
}
```

---

### `flex-wrap`

Controls whether items wrap or stay on one line.

**Values:**

* `nowrap` (default)
* `wrap`
* `wrap-reverse`

```css
.container {
  flex-wrap: wrap;
}
```

---

### `justify-content`

Aligns items along the **main axis**.

**Values:**

* `flex-start`
* `center`
* `flex-end`
* `space-between`
* `space-around`
* `space-evenly`

```css
.container {
  justify-content: space-between;
}
```

---

### `align-items`

Aligns items along the **cross axis**.

**Values:**

* `stretch` (default)
* `center`
* `flex-start`
* `flex-end`
* `baseline`

```css
.container {
  align-items: center;
}
```

---

### `align-content`

Used when multiple rows exist (`flex-wrap: wrap`).

```css
.container {
  align-content: space-between;
}
```

---

### `gap`

Adds spacing between flex items.

```css
.container {
  gap: 20px;
}
```

---

## Flexbox Item Properties (Child)

### `order`

Changes visual order of items.

```css
.item1 {
  order: 2;
}
```

---

### `flex-grow`

Controls how much an item grows relative to others.

**Default:** `0`

```css
.item1 {
  flex-grow: 1;
}

.item2 {
  flex-grow: 2;
}
```

---

### `flex-shrink`

Controls how much an item shrinks when space is limited.

```css
.item {
  flex-shrink: 0;
}
```

---

### `flex-basis`

Defines initial size before grow/shrink.

```css
.item {
  flex-basis: 200px;
}
```

---

### `flex`

Shorthand for:

```
flex: grow shrink basis;
```

```css
.item {
  flex: 1 1 200px;
}
```

---

### `align-self`

Overrides `align-items` for a single item.

```css
.item {
  align-self: center;
}
```

---

## 4. CSS Grid

### What is Grid?

CSS Grid is a **two-dimensional layout system**.

```css
.container {
  display: grid;
}
```

### When to Use Grid

* Full website layouts
* Dashboards
* Galleries
* Page structure

---

## Grid Container Properties

### `grid-template-columns`

Defines columns structure.

```css
.container {
  grid-template-columns: 1fr 2fr;
}
```

---

### `grid-template-rows`

Defines row structure.

```css
grid-template-rows: 100px auto;
```

---

### `gap`

Adds spacing between rows and columns.

---

### `justify-items`

Aligns items horizontally inside cells.

---

### `align-items`

Aligns items vertically inside cells.

---

## Grid Item Properties

### `grid-column`

Controls column span.

```css
.item {
  grid-column: 1 / 3;
}
```

---

### `grid-row`

Controls row span.

---

### `grid-area`

Places item using named areas.

---

## 5. Position Property

Controls exact placement of elements.

### `static`

Default behavior.

---

### `relative`

Moves element relative to itself.

```css
.box {
  position: relative;
  top: 10px;
}
```

---

### `absolute`

Moves relative to nearest positioned parent.

---

### `fixed`

Fixed to viewport (e.g., navbar).

---

### `sticky`

Scrolls normally, then sticks.

---

## 6. Flexbox vs Grid

| Flexbox         | Grid            |
| --------------- | --------------- |
| One-dimensional | Two-dimensional |
| Components      | Full layouts    |
| Simple          | Complex         |

---

## ✅ Final Summary

This README covers:

* CSS Units
* Display Property
* Flexbox
* Grid
* Position Property

These topics form the **core foundation of CSS layout design**.

---

🚀 **Happy Learning!**
