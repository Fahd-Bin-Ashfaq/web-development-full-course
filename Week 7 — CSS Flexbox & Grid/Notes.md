# Week 7: CSS Flexbox and Grid

## Table of Contents

1. [Introduction — Why Flexbox and Grid?](#1-introduction--why-flexbox-and-grid)
2. [CSS Flexbox (One-Dimensional Layout)](#2-css-flexbox-one-dimensional-layout)
3. [CSS Grid (Two-Dimensional Layout)](#3-css-grid-two-dimensional-layout)
4. [Flexbox vs Grid — When to Use Which?](#4-flexbox-vs-grid--when-to-use-which)
5. [Summary](#5-summary)

---

## 1. Introduction — Why Flexbox and Grid?

### The Problem with Old Layout Methods

Before Flexbox and Grid existed, web developers had to rely on techniques that were never designed for creating layouts. These included **floats**, **inline-block hacks**, **table-based layouts**, and **absolute positioning**. While these methods technically worked, they were fragile, required clearfix hacks, and made responsive design extremely painful.

Consider this common scenario from the old days:

```css
/* The old way: float-based layout */
.sidebar {
  float: left;
  width: 25%;
}

.main-content {
  float: left;
  width: 75%;
}

/* Without this clearfix hack, the parent container collapses */
.container::after {
  content: "";
  display: table;
  clear: both;
}
```

**Real-Life Analogy:** Imagine you are trying to arrange furniture in a room, but you can only push things to the left or right wall and hope they line up. That is what float-based layout felt like. Flexbox and Grid gave us the ability to actually plan and control where everything goes, like having a proper floor plan.

### The Solution: Modern Layout Tools

CSS introduced two powerful layout systems to solve these problems:

| Feature         | Purpose                          | Introduced |
| --------------- | -------------------------------- | ---------- |
| **Flexbox**     | One-dimensional layouts          | 2012       |
| **CSS Grid**    | Two-dimensional layouts          | 2017       |

```
OLD WAY (Floats and Hacks):

+----------+----------+----------+
|  float:  |  float:  |  float:  |   <-- Items float, parent collapses
|   left   |   left   |   left   |       Need clearfix hacks
+----------+----------+----------+
  ??? Parent height = 0 ???          <-- Broken!


NEW WAY (Flexbox / Grid):

+----------+----------+----------+
|  Item 1  |  Item 2  |  Item 3  |   <-- Items properly contained
|          |          |          |       Parent wraps correctly
+----------+----------+----------+
  Parent height = automatic            <-- Works perfectly!
```

**Key Takeaway:** Floats were designed for wrapping text around images, not for building entire page layouts. Flexbox and Grid were specifically designed for layout, making them more predictable, more powerful, and far easier to maintain.

---

## 2. CSS Flexbox (One-Dimensional Layout)

### 2.1 What is Flexbox?

Flexbox (Flexible Box Layout) is a CSS layout model designed for arranging items in **one direction at a time** — either horizontally (in a row) or vertically (in a column). It gives you fine-grained control over how items are spaced, aligned, and sized within a container.

**Real-Life Example — Books on a Shelf:**

Think of a bookshelf. You arrange books in a single row from left to right. You can decide whether the books are packed tightly to the left, centered on the shelf, or spread out evenly with equal gaps between them. If the shelf is too narrow, books can wrap to a second row. That is exactly how Flexbox works.

```
Bookshelf (Flex Container):
+----------------------------------------------------+
|  [Book A]  [Book B]  [Book C]  [Book D]  [Book E]  |
+----------------------------------------------------+
   ^                                                ^
   |                                                |
   Items arranged in ONE direction (left to right)
```

### 2.2 Flex Container vs Flex Items

When you apply `display: flex` to an element, it becomes a **flex container**. Its direct children automatically become **flex items**.

```css
.container {
  display: flex;  /* This element is now a flex container */
}
```

```html
<div class="container">      <!-- Flex Container -->
  <div>Item 1</div>          <!-- Flex Item -->
  <div>Item 2</div>          <!-- Flex Item -->
  <div>Item 3</div>          <!-- Flex Item -->
</div>
```

```
Diagram: Container vs Items

+------ Flex Container (display: flex) ------+
|                                             |
|  +--------+  +--------+  +--------+        |
|  | Flex   |  | Flex   |  | Flex   |        |
|  | Item 1 |  | Item 2 |  | Item 3 |        |
|  +--------+  +--------+  +--------+        |
|                                             |
+---------------------------------------------+

Key:
  - Outer box   = Flex Container (the parent)
  - Inner boxes = Flex Items (direct children only)
  - Nested children inside items are NOT flex items
```

**Important:** Only the **direct children** of a flex container become flex items. Grandchildren and deeper descendants are not affected.

### 2.3 Flexbox Axes

Flexbox operates along two axes. Understanding these is crucial for mastering every Flexbox property.

```
When flex-direction: row (default):

Main Axis (horizontal) ──────────────────────>
|
|   +--------+  +--------+  +--------+
|   | Item 1 |  | Item 2 |  | Item 3 |
|   +--------+  +--------+  +--------+
|
v Cross Axis (vertical)


When flex-direction: column:

Cross Axis (horizontal) ──────────────────────>
|
|   +--------+
|   | Item 1 |
|   +--------+
|   +--------+
|   | Item 2 |
|   +--------+
|   +--------+
|   | Item 3 |
|   +--------+
|
v Main Axis (vertical)
```

- **Main Axis:** The primary direction in which flex items are laid out (controlled by `flex-direction`).
- **Cross Axis:** The axis perpendicular to the main axis.
- `justify-content` controls alignment along the **main axis**.
- `align-items` controls alignment along the **cross axis**.

---

### 2.4 Container Properties

These properties are applied to the **flex container** (the parent element).

#### 2.4.1 display: flex

This is the property that activates Flexbox. Without it, none of the other flex properties will work.

```css
.container {
  display: flex;         /* Block-level flex container */
}

/* or */

.container {
  display: inline-flex;  /* Inline-level flex container */
}
```

```
Before display: flex (normal block flow):

+------------------------------------+
| Item 1                             |
+------------------------------------+
+------------------------------------+
| Item 2                             |
+------------------------------------+
+------------------------------------+
| Item 3                             |
+------------------------------------+
  (Each div takes full width, stacked vertically)


After display: flex:

+----------+----------+----------+---+
| Item 1   | Item 2   | Item 3   |   |
+----------+----------+----------+---+
  (Items sit side by side in a row)
```

---

#### 2.4.2 flex-direction

Defines the direction in which flex items are placed inside the container. This property sets the **main axis**.

```css
.container {
  flex-direction: row;             /* Default */
  flex-direction: row-reverse;
  flex-direction: column;
  flex-direction: column-reverse;
}
```

**flex-direction: row** (default) — Items flow left to right.

```
+---------------------------------------------+
|  [Item 1]  [Item 2]  [Item 3]  [Item 4]    |
|  -------->                                   |
|  (left to right)                             |
+---------------------------------------------+
```

**flex-direction: row-reverse** — Items flow right to left.

```
+---------------------------------------------+
|    [Item 4]  [Item 3]  [Item 2]  [Item 1]  |
|                                   <--------  |
|                           (right to left)    |
+---------------------------------------------+
```

**flex-direction: column** — Items flow top to bottom.

```
+------------------+
|  [Item 1]        |
|  [Item 2]        |   |
|  [Item 3]        |   |  (top to bottom)
|  [Item 4]        |   v
+------------------+
```

**flex-direction: column-reverse** — Items flow bottom to top.

```
+------------------+
|  [Item 4]        |   ^
|  [Item 3]        |   |  (bottom to top)
|  [Item 2]        |   |
|  [Item 1]        |
+------------------+
```

**Real-Life Example:** Think of `flex-direction` as deciding whether to arrange photos in a horizontal strip (row) or stack them vertically like a tower of cards (column). The "reverse" variants simply flip the starting point.

---

#### 2.4.3 justify-content

Controls how flex items are distributed along the **main axis**. This is one of the most commonly used Flexbox properties.

```css
.container {
  display: flex;
  justify-content: flex-start;     /* Default */
}
```

Below are visual diagrams for **each value**, assuming `flex-direction: row`:

**justify-content: flex-start** (default) — Items are packed to the start of the main axis.

```
+---------------------------------------------+
|  [A]  [B]  [C]                              |
+---------------------------------------------+
   ^
   Items packed at the start (left)
```

**justify-content: flex-end** — Items are packed to the end of the main axis.

```
+---------------------------------------------+
|                              [A]  [B]  [C]  |
+---------------------------------------------+
                                           ^
                       Items packed at the end (right)
```

**justify-content: center** — Items are centered along the main axis.

```
+---------------------------------------------+
|              [A]  [B]  [C]                  |
+---------------------------------------------+
                    ^
               Items centered
```

**justify-content: space-between** — First item at the start, last item at the end, remaining space is distributed evenly between items.

```
+---------------------------------------------+
|  [A]            [B]            [C]          |
+---------------------------------------------+
   ^     equal     ^     equal     ^
   |<--- gap  --->|<--- gap  --->|
   start                          end
```

**justify-content: space-around** — Equal space is placed around each item. This means the gap between two adjacent items is twice the gap at the edges.

```
+---------------------------------------------+
|    [A]        [B]        [C]    |
+---------------------------------------------+
  ^    ^      ^    ^      ^    ^
  half gap    full gap    half gap
  
  Edge gaps = half the size of gaps between items
```

**justify-content: space-evenly** — Equal space is placed between all items AND at the edges. Every gap is the same size.

```
+---------------------------------------------+
|      [A]      [B]      [C]      |
+---------------------------------------------+
  ^     ^     ^     ^     ^     ^
  equal equal equal equal equal equal

  All gaps are exactly the same size
```

**Comparison of all space values:**

```
space-between:   |[A]      [B]      [C]|   No space at edges
space-around:    | [A]    [B]    [C] |   Half space at edges
space-evenly:    |  [A]   [B]   [C]  |   Equal space everywhere
```

---

#### 2.4.4 align-items

Controls how flex items are aligned along the **cross axis** (perpendicular to the main axis). When `flex-direction` is `row`, the cross axis is vertical.

```css
.container {
  display: flex;
  align-items: stretch;    /* Default */
}
```

In the diagrams below, the items have different heights to illustrate the effect. The container has a fixed height.

**align-items: stretch** (default) — Items stretch to fill the entire cross axis.

```
+---------------------------------------------+
|  +--------+  +--------+  +--------+        |
|  |        |  |        |  |        |        |
|  | Item 1 |  | Item 2 |  | Item 3 |        |
|  |        |  |        |  |        |        |
|  |        |  |        |  |        |        |
|  +--------+  +--------+  +--------+        |
+---------------------------------------------+
   All items stretch to fill the full height
```

**align-items: flex-start** — Items are aligned to the top (start of cross axis).

```
+---------------------------------------------+
|  +--------+  +-----+  +---+                |
|  | Item 1 |  | It2 |  |I3 |                |
|  +--------+  +-----+  +---+                |
|                                             |
|                                             |
+---------------------------------------------+
   Items aligned at the top
```

**align-items: flex-end** — Items are aligned to the bottom (end of cross axis).

```
+---------------------------------------------+
|                                             |
|                                             |
|  +--------+  +-----+  +---+                |
|  | Item 1 |  | It2 |  |I3 |                |
|  +--------+  +-----+  +---+                |
+---------------------------------------------+
   Items aligned at the bottom
```

**align-items: center** — Items are centered along the cross axis.

```
+---------------------------------------------+
|                                             |
|  +--------+  +-----+  +---+                |
|  | Item 1 |  | It2 |  |I3 |                |
|  +--------+  +-----+  +---+                |
|                                             |
+---------------------------------------------+
   Items centered vertically
```

**align-items: baseline** — Items are aligned so that their text baselines line up. This is useful when items have different font sizes or padding.

```
+---------------------------------------------+
|                                             |
|  +--------+  +----------+  +------+        |
|  | Hello  |  |   HELLO  |  |Hello |        |
|  +--------+  |          |  +------+        |
|              +----------+                   |
+---------------------------------------------+
   --------- baseline --------- (text lines up)
```

---

#### 2.4.5 flex-wrap

By default, flex items try to fit on a single line. `flex-wrap` controls whether items are allowed to wrap onto multiple lines.

```css
.container {
  display: flex;
  flex-wrap: nowrap;    /* Default */
}
```

**flex-wrap: nowrap** (default) — All items are forced onto one line (items may shrink).

```
+---------------------------------------------+
|  [Item1] [Item2] [Item3] [Item4] [Item5]    |
+---------------------------------------------+
   All items squeezed onto one line (may overflow)
```

**flex-wrap: wrap** — Items wrap onto the next line when there is not enough space.

```
+---------------------------------------------+
|  [Item 1]  [Item 2]  [Item 3]  [Item 4]    |
|                                             |
|  [Item 5]  [Item 6]  [Item 7]              |
+---------------------------------------------+
   Items wrap to the next line naturally
```

**flex-wrap: wrap-reverse** — Items wrap, but in the reverse direction (new lines appear above).

```
+---------------------------------------------+
|  [Item 5]  [Item 6]  [Item 7]              |
|                                             |
|  [Item 1]  [Item 2]  [Item 3]  [Item 4]    |
+---------------------------------------------+
   New lines appear above instead of below
```

**Real-Life Example:** Imagine hanging photos on a clothesline. With `nowrap`, you squeeze every photo onto one line no matter what. With `wrap`, when the line is full, you start a new line below.

---

#### 2.4.6 align-content

Controls the distribution of **multiple lines** along the cross axis. This property only takes effect when `flex-wrap: wrap` is set and items have wrapped onto multiple lines.

```css
.container {
  display: flex;
  flex-wrap: wrap;
  align-content: stretch;    /* Default */
}
```

**align-content: flex-start** — Lines are packed at the top.

```
+---------------------------------------------+
|  [Item 1]  [Item 2]  [Item 3]  [Item 4]    |
|  [Item 5]  [Item 6]                         |
|                                             |
|                                             |
|                                             |
+---------------------------------------------+
   Both lines packed at the top
```

**align-content: flex-end** — Lines are packed at the bottom.

```
+---------------------------------------------+
|                                             |
|                                             |
|                                             |
|  [Item 1]  [Item 2]  [Item 3]  [Item 4]    |
|  [Item 5]  [Item 6]                         |
+---------------------------------------------+
   Both lines packed at the bottom
```

**align-content: center** — Lines are centered vertically.

```
+---------------------------------------------+
|                                             |
|  [Item 1]  [Item 2]  [Item 3]  [Item 4]    |
|  [Item 5]  [Item 6]                         |
|                                             |
+---------------------------------------------+
   Lines centered vertically
```

**align-content: space-between** — First line at the top, last line at the bottom.

```
+---------------------------------------------+
|  [Item 1]  [Item 2]  [Item 3]  [Item 4]    |
|                                             |
|                                             |
|                                             |
|  [Item 5]  [Item 6]                         |
+---------------------------------------------+
   Equal gap distributed between lines
```

**align-content: space-around** — Equal space around each line.

```
+---------------------------------------------+
|                                             |
|  [Item 1]  [Item 2]  [Item 3]  [Item 4]    |
|                                             |
|                                             |
|  [Item 5]  [Item 6]                         |
|                                             |
+---------------------------------------------+
```

**align-content: stretch** (default) — Lines stretch to fill the available space.

```
+---------------------------------------------+
|  [Item 1]  [Item 2]  [Item 3]  [Item 4]    |
|                                             |
|                                             |
|  [Item 5]  [Item 6]                         |
|                                             |
+---------------------------------------------+
   Each line stretches to take equal height
```

---

#### 2.4.7 gap (row-gap, column-gap)

Adds consistent spacing between flex items without affecting the outer edges. This is much cleaner than using margins.

```css
.container {
  display: flex;
  gap: 20px;               /* Both row and column gap */
  row-gap: 20px;           /* Gap between rows (when wrapping) */
  column-gap: 10px;        /* Gap between columns */
}
```

```
Without gap (using margins — messy):

+---------------------------------------------+
| [A] [B] [C] [D]                             |
+---------------------------------------------+
  You have to manage margins on every item,
  and the first/last items need special treatment.


With gap: 20px:

+---------------------------------------------+
|  [A]    [B]    [C]    [D]                   |
|       20px   20px   20px                     |
+---------------------------------------------+
  Clean, consistent spacing between items only.
  No extra space at the edges.


With row-gap: 20px and column-gap: 10px (wrapping):

+---------------------------------------------+
|  [A]  10px  [B]  10px  [C]  10px  [D]      |
|                                             |
|  20px (vertical gap between rows)           |
|                                             |
|  [E]  10px  [F]  10px  [G]                 |
+---------------------------------------------+
```

**Why use `gap` instead of margins?** The `gap` property only creates space *between* items. With margins, you end up with unwanted space at the edges and have to write extra CSS to remove it.

---

### 2.5 Item Properties

These properties are applied to individual **flex items** (the children).

#### 2.5.1 flex-grow

Defines how much a flex item should **grow** relative to other items when extra space is available. The default value is `0`, meaning items do not grow.

```css
.item {
  flex-grow: 0;    /* Default: do not grow */
}
```

```
All items flex-grow: 0 (default):

+---------------------------------------------+
|  [A]  [B]  [C]              empty space     |
+---------------------------------------------+
  Items keep their natural size. Extra space is unused.


All items flex-grow: 1:

+---------------------------------------------+
|  [  Item A  ]  [  Item B  ]  [  Item C  ]  |
+---------------------------------------------+
  All items grow equally to fill the container.


Item A: flex-grow: 2, Items B and C: flex-grow: 1:

+---------------------------------------------+
|  [     Item A      ]  [ Item B ]  [ Item C ]|
+---------------------------------------------+
  Item A gets 2 "shares" of extra space.
  Items B and C each get 1 "share".
  (A grows twice as fast, not twice the total size)
```

**Real-Life Example:** Imagine three people sharing a pizza. If everyone has `flex-grow: 1`, they each get an equal share of the remaining slices. If one person has `flex-grow: 2`, they get double the share of leftover slices — but they do not necessarily end up with double the total pizza, because the original slice sizes may differ.

---

#### 2.5.2 flex-shrink

Defines how much a flex item should **shrink** when the container is too small to fit all items. The default value is `1`, meaning items shrink equally.

```css
.item {
  flex-shrink: 1;    /* Default: items shrink equally */
}
```

```
Container is 300px, but items need 500px total.

All items flex-shrink: 1 (default):

+------------------------------+
| [A shrunk] [B shrunk] [C shrunk] |
+------------------------------+
  All items shrink equally to fit.


Item B: flex-shrink: 0 (B does not shrink):

+------------------------------+
| [A shrunk] [  Item B  ] [C shrunk] |
+------------------------------+
  Item B keeps its original size.
  A and C absorb all the shrinkage.
```

---

#### 2.5.3 flex-basis

Sets the **initial size** of a flex item before any growing or shrinking happens. It works like `width` (in a row) or `height` (in a column), but is specific to Flexbox.

```css
.item {
  flex-basis: auto;    /* Default: use the item's width/height or content */
  flex-basis: 200px;   /* Start at 200px, then grow/shrink */
  flex-basis: 30%;     /* Start at 30% of the container */
  flex-basis: 0;       /* Ignore content size, distribute all space */
}
```

```
flex-basis: 200px with flex-grow: 1:

Step 1 (Initial):
+---------------------------------------------+
| [200px] [200px] [200px]   remaining space   |
+---------------------------------------------+

Step 2 (After growing):
+---------------------------------------------+
| [  ~282px  ]  [  ~282px  ]  [  ~282px  ]   |
+---------------------------------------------+
  Each item starts at 200px, then grows equally
  to fill the remaining space.
```

---

#### 2.5.4 flex Shorthand

The `flex` shorthand combines `flex-grow`, `flex-shrink`, and `flex-basis` into a single property. It is the recommended way to set these values.

```css
.item {
  flex: 0 1 auto;     /* Default: don't grow, can shrink, auto basis */
  flex: 1;            /* Same as: flex: 1 1 0   (grow equally) */
  flex: auto;         /* Same as: flex: 1 1 auto */
  flex: none;         /* Same as: flex: 0 0 auto (rigid, no flex) */
  flex: 2 0 100px;    /* Grow with factor 2, don't shrink, start at 100px */
}
```

| Shorthand      | flex-grow | flex-shrink | flex-basis | Meaning                              |
| -------------- | --------- | ----------- | ---------- | ------------------------------------ |
| `flex: 0 1 auto` | 0       | 1           | auto       | Default — don't grow, can shrink     |
| `flex: 1`      | 1         | 1           | 0          | Grow and shrink equally              |
| `flex: auto`   | 1         | 1           | auto       | Grow and shrink, respect content     |
| `flex: none`   | 0         | 0           | auto       | Rigid size, no flexibility           |
| `flex: 2`      | 2         | 1           | 0          | Grow at 2x rate                      |

---

#### 2.5.5 align-self

Overrides the container's `align-items` for a **single item**. Accepts the same values: `flex-start`, `flex-end`, `center`, `stretch`, `baseline`.

```css
.container {
  display: flex;
  align-items: flex-start;   /* All items align to the top */
}

.special-item {
  align-self: flex-end;      /* This one aligns to the bottom */
}
```

```
Container: align-items: flex-start
Item C:    align-self: flex-end

+---------------------------------------------+
|  +------+  +------+                         |
|  |  A   |  |  B   |                         |
|  +------+  +------+                         |
|                                             |
|                       +------+              |
|                       |  C   |              |
|                       +------+              |
+---------------------------------------------+
   A and B at top        C at bottom
   (follow container)    (overridden)
```

---

#### 2.5.6 order

Controls the **visual order** of flex items without changing the HTML source order. By default, all items have `order: 0`.

```css
.item-a { order: 3; }
.item-b { order: 1; }
.item-c { order: 2; }
```

```
HTML source order:  A, B, C

Without order property:
+---------------------------------------------+
|  [A]  [B]  [C]                              |
+---------------------------------------------+

With order (B=1, C=2, A=3):
+---------------------------------------------+
|  [B]  [C]  [A]                              |
+---------------------------------------------+
  Items are visually rearranged.
  HTML source remains unchanged.
```

**Important Note:** Use `order` sparingly. Changing the visual order can confuse screen readers and keyboard navigation, since those tools follow the source order.

---

### 2.6 Common Flexbox Patterns

#### Pattern 1: Centering an Element (The Holy Grail of CSS)

Before Flexbox, perfectly centering an element both horizontally and vertically was notoriously difficult. With Flexbox, it takes just three lines.

```css
.container {
  display: flex;
  justify-content: center;    /* Center horizontally */
  align-items: center;        /* Center vertically */
  height: 100vh;              /* Full viewport height */
}
```

```
+---------------------------------------------+
|                                             |
|                                             |
|                                             |
|             +---------------+               |
|             |   Centered!   |               |
|             +---------------+               |
|                                             |
|                                             |
|                                             |
+---------------------------------------------+
  Perfectly centered in both directions.
```

---

#### Pattern 2: Navigation Bar

A common layout with a logo on the left and navigation links on the right.

```css
.navbar {
  display: flex;
  justify-content: space-between;
  align-items: center;
  padding: 10px 20px;
  background-color: #333;
}

.nav-links {
  display: flex;
  gap: 20px;
}
```

```html
<nav class="navbar">
  <div class="logo">MyBrand</div>
  <div class="nav-links">
    <a href="#">Home</a>
    <a href="#">About</a>
    <a href="#">Services</a>
    <a href="#">Contact</a>
  </div>
</nav>
```

```
+-----------------------------------------------------+
|  MyBrand            Home  About  Services  Contact  |
+-----------------------------------------------------+
   ^                                              ^
   flex-start                               flex-end
             space-between pushes them apart
```

---

#### Pattern 3: Card Layout

A responsive row of cards that wraps on smaller screens.

```css
.card-container {
  display: flex;
  flex-wrap: wrap;
  gap: 20px;
}

.card {
  flex: 1 1 300px;    /* Grow, shrink, minimum 300px */
  padding: 20px;
  border: 1px solid #ddd;
  border-radius: 8px;
}
```

```
Wide screen (3 cards per row):
+---------------------------------------------+
|  +----------+  +----------+  +----------+  |
|  | Card 1   |  | Card 2   |  | Card 3   |  |
|  |          |  |          |  |          |  |
|  +----------+  +----------+  +----------+  |
+---------------------------------------------+

Narrow screen (cards wrap):
+----------------------------+
|  +----------+  +----------+|
|  | Card 1   |  | Card 2   ||
|  +----------+  +----------+|
|  +----------+              |
|  | Card 3   |              |
|  +----------+              |
+----------------------------+
```

---

#### Pattern 4: Footer at Bottom of Page (Sticky Footer)

Ensures the footer stays at the bottom of the viewport even when there is not enough content to fill the page.

```css
body {
  display: flex;
  flex-direction: column;
  min-height: 100vh;
  margin: 0;
}

main {
  flex: 1;    /* Main content takes all remaining space */
}

footer {
  padding: 20px;
  background-color: #333;
  color: white;
}
```

```
Short content (footer still at bottom):

+---------------------------------------------+
|  Header                                     |
+---------------------------------------------+
|  Main Content                               |
|  (short — only a few lines)                 |
|                                             |
|          flex: 1 fills this gap             |
|                                             |
|                                             |
+---------------------------------------------+
|  Footer (always at the bottom)              |
+---------------------------------------------+
```

---

## 3. CSS Grid (Two-Dimensional Layout)

### 3.1 What is Grid?

CSS Grid is a layout system designed for creating **two-dimensional layouts** — controlling both rows AND columns simultaneously. While Flexbox handles one direction at a time, Grid lets you define a complete grid structure and place items precisely within it.

**Real-Life Example — A Chess Board or Excel Spreadsheet:**

Think of a chess board. It has 8 rows and 8 columns, forming 64 squares. You can place any piece on any square by specifying its row and column. CSS Grid works exactly the same way — you define the rows and columns, then place items wherever you want.

```
Chess Board (Grid):

     Col 1   Col 2   Col 3   Col 4   Col 5   Col 6   Col 7   Col 8
   +-------+-------+-------+-------+-------+-------+-------+-------+
R1 |       |       |       |       |       |       |       |       |
   +-------+-------+-------+-------+-------+-------+-------+-------+
R2 |       |       |       |       |       |       |       |       |
   +-------+-------+-------+-------+-------+-------+-------+-------+
R3 |       |       |       |       |       |       |       |       |
   +-------+-------+-------+-------+-------+-------+-------+-------+
R4 |       |       |       |       |       |       |       |       |
   +-------+-------+-------+-------+-------+-------+-------+-------+

   You can place items at ANY row and column intersection.
   That is the power of CSS Grid.
```

### 3.2 Grid Container vs Grid Items

Just like Flexbox, when you apply `display: grid` to an element, it becomes a **grid container**. Its direct children become **grid items**.

```css
.container {
  display: grid;
}
```

```html
<div class="container">      <!-- Grid Container -->
  <div>Item 1</div>          <!-- Grid Item -->
  <div>Item 2</div>          <!-- Grid Item -->
  <div>Item 3</div>          <!-- Grid Item -->
  <div>Item 4</div>          <!-- Grid Item -->
</div>
```

```
Diagram: Grid Container vs Grid Items

+------- Grid Container (display: grid) -------+
|                                               |
|  +----------+  +----------+  +----------+    |
|  | Grid     |  | Grid     |  | Grid     |    |
|  | Item 1   |  | Item 2   |  | Item 3   |    |
|  +----------+  +----------+  +----------+    |
|  +----------+  +----------+  +----------+    |
|  | Grid     |  | Grid     |  | Grid     |    |
|  | Item 4   |  | Item 5   |  | Item 6   |    |
|  +----------+  +----------+  +----------+    |
|                                               |
+-----------------------------------------------+
```

### 3.3 Grid Terminology

Before diving into properties, let us understand the key terms.

```
+---------- Grid Container ----------+
|          |          |               |
|  Cell    |  Cell    |  Cell         |  <-- Grid Row
|          |          |               |
+----------+----------+---------------+
|          |          |               |
|  Cell    |  Cell    |  Cell         |  <-- Grid Row
|          |          |               |
+----------+----------+---------------+
     ^          ^          ^
  Column 1   Column 2   Column 3

Grid Lines (numbered from 1):

  1          2          3            4    <-- Column lines
  +----------+----------+------------+
  |          |          |            |  1  <-- Row line
  +----------+----------+------------+
  |          |          |            |  2  <-- Row line
  +----------+----------+------------+
  |          |          |            |  3  <-- Row line
  +----------+----------+------------+

- Grid Line:    The dividing lines between columns and rows
- Grid Cell:    A single unit (intersection of one row and one column)
- Grid Track:   A complete row or column
- Grid Area:    A rectangular region spanning one or more cells
```

---

### 3.4 Container Properties

#### 3.4.1 display: grid

Activates the Grid layout on a container.

```css
.container {
  display: grid;          /* Block-level grid */
}

/* or */

.container {
  display: inline-grid;   /* Inline-level grid */
}
```

---

#### 3.4.2 grid-template-columns

Defines the number of columns and their sizes.

```css
.container {
  display: grid;

  /* Fixed pixel widths */
  grid-template-columns: 200px 200px 200px;

  /* Fractional units */
  grid-template-columns: 1fr 1fr 1fr;

  /* Mixed units */
  grid-template-columns: 200px 1fr 2fr;

  /* Using repeat() */
  grid-template-columns: repeat(3, 1fr);

  /* Using auto-fill with minmax */
  grid-template-columns: repeat(auto-fill, minmax(250px, 1fr));

  /* Using auto-fit with minmax */
  grid-template-columns: repeat(auto-fit, minmax(250px, 1fr));
}
```

**Fixed widths (200px 200px 200px):**

```
+----------+----------+----------+
|  200px   |  200px   |  200px   |
|          |          |          |
+----------+----------+----------+
  Three columns, each exactly 200px wide.
```

**Fractional units (1fr 1fr 1fr):**

```
+-------------+-------------+-------------+
|    1fr      |    1fr      |    1fr      |
|  (33.3%)    |  (33.3%)    |  (33.3%)    |
+-------------+-------------+-------------+
  Three equal columns that share the available space.
```

**Mixed units (200px 1fr 2fr):**

```
+--------+-------------+--------------------------+
| 200px  |    1fr      |         2fr              |
| fixed  | (1/3 rest)  |     (2/3 rest)           |
+--------+-------------+--------------------------+
  First column is fixed. Remaining space is split
  1:2 between the second and third columns.
```

**repeat(3, 1fr):**

```
This is shorthand for:  1fr 1fr 1fr

+-------------+-------------+-------------+
|    1fr      |    1fr      |    1fr      |
+-------------+-------------+-------------+
```

**repeat(auto-fill, minmax(250px, 1fr)):**

Automatically creates as many columns as will fit, each at least 250px wide.

```
Wide screen (4 columns fit):
+----------+----------+----------+----------+
|  250px+  |  250px+  |  250px+  |  250px+  |
+----------+----------+----------+----------+

Narrow screen (2 columns fit):
+------------------+------------------+
|     250px+       |     250px+       |
+------------------+------------------+

auto-fill: creates empty tracks even if no items fill them
auto-fit:  collapses empty tracks, items stretch to fill
```

**auto-fill vs auto-fit:**

```
3 items in a wide container:

auto-fill:
+--------+--------+--------+--------+--------+
| Item 1 | Item 2 | Item 3 | (empty)| (empty)|
+--------+--------+--------+--------+--------+
  Empty tracks are preserved.

auto-fit:
+-------------+-------------+-------------+
|   Item 1    |   Item 2    |   Item 3    |
+-------------+-------------+-------------+
  Empty tracks collapse. Items stretch to fill.
```

---

#### 3.4.3 grid-template-rows

Defines the number of rows and their sizes. Works exactly like `grid-template-columns` but for rows.

```css
.container {
  display: grid;
  grid-template-columns: 1fr 1fr;
  grid-template-rows: 100px 200px 100px;
}
```

```
+---------------------+---------------------+
|                     |                     |  100px
+---------------------+---------------------+
|                     |                     |
|                     |                     |  200px
|                     |                     |
+---------------------+---------------------+
|                     |                     |  100px
+---------------------+---------------------+
```

**Tip:** Rows that are not explicitly defined are sized automatically (using `auto`) based on their content. You can control the size of these implicit rows with `grid-auto-rows`.

```css
.container {
  display: grid;
  grid-template-columns: repeat(3, 1fr);
  grid-auto-rows: 150px;    /* Any new rows default to 150px */
}
```

---

#### 3.4.4 grid-template-areas

Lets you define named areas in your grid and place items by name. This is one of the most readable and powerful features of CSS Grid.

```css
.container {
  display: grid;
  grid-template-columns: 200px 1fr 200px;
  grid-template-rows: 60px 1fr 60px;
  grid-template-areas:
    "header  header  header"
    "sidebar main   aside"
    "footer  footer  footer";
}

.header  { grid-area: header; }
.sidebar { grid-area: sidebar; }
.main    { grid-area: main; }
.aside   { grid-area: aside; }
.footer  { grid-area: footer; }
```

```
Visual result:

+------------------+------------------+------------------+
|                    HEADER                               |
|                   (spans all 3 columns)                 |
+----------+----------------------------+-----------------+
|          |                            |                 |
| SIDEBAR  |           MAIN            |     ASIDE       |
|  200px   |        (flexible)         |     200px       |
|          |                            |                 |
+----------+----------------------------+-----------------+
|                    FOOTER                               |
|                   (spans all 3 columns)                 |
+------------------+------------------+------------------+

The template literally looks like the layout:
  "header  header  header"
  "sidebar main   aside"
  "footer  footer  footer"
```

You can use a dot (`.`) to leave a cell empty:

```css
grid-template-areas:
  "header header header"
  "sidebar main ."          /* Right cell is empty */
  "footer footer footer";
```

```
+-------------+-------------------+-----------+
|              HEADER                         |
+----------+-----------------------+----------+
| SIDEBAR  |        MAIN          | (empty)  |
+----------+-----------------------+----------+
|              FOOTER                         |
+-------------+-------------------+-----------+
```

---

#### 3.4.5 gap, row-gap, column-gap

Works exactly the same as in Flexbox — adds spacing between grid tracks.

```css
.container {
  display: grid;
  grid-template-columns: repeat(3, 1fr);
  gap: 20px;                /* 20px between all rows and columns */
  /* or */
  row-gap: 20px;
  column-gap: 10px;
}
```

```
gap: 20px:

+----------+   +----------+   +----------+
|  Item 1  |   |  Item 2  |   |  Item 3  |
+----------+   +----------+   +----------+
      20px gap        20px gap
+----------+   +----------+   +----------+
|  Item 4  | 20|  Item 5  |   |  Item 6  |
+----------+ px+----------+   +----------+
     20px vertical gap between rows
```

---

#### 3.4.6 justify-items and align-items

Control the alignment of grid items **within their cells**.

```css
.container {
  display: grid;
  grid-template-columns: repeat(3, 200px);
  justify-items: center;    /* Horizontal alignment within cells */
  align-items: center;      /* Vertical alignment within cells */
}
```

**justify-items** (horizontal alignment within each cell):

```
justify-items: start         justify-items: center        justify-items: end
+-----------+                +-----------+                +-----------+
| [item]    |                |  [item]   |                |    [item] |
+-----------+                +-----------+                +-----------+

justify-items: stretch (default)
+-----------+
|[  item   ]|    Item fills the entire cell width
+-----------+
```

**align-items** (vertical alignment within each cell):

```
align-items: start       align-items: center      align-items: end
+-----------+            +-----------+             +-----------+
| [item]    |            |           |             |           |
|           |            | [item]    |             |           |
|           |            |           |             | [item]    |
+-----------+            +-----------+             +-----------+
```

---

#### 3.4.7 justify-content and align-content

Control the alignment of the **entire grid** within the container when the grid is smaller than the container.

```css
.container {
  display: grid;
  width: 800px;
  grid-template-columns: repeat(3, 150px);  /* 450px total, 350px leftover */
  justify-content: center;    /* Center the grid horizontally */
  align-content: start;       /* Align the grid to the top */
}
```

**justify-content** (horizontal alignment of the whole grid):

```
justify-content: start:
+---------------------------------------------------+
| [col1] [col2] [col3]                              |
+---------------------------------------------------+

justify-content: center:
+---------------------------------------------------+
|           [col1] [col2] [col3]                    |
+---------------------------------------------------+

justify-content: end:
+---------------------------------------------------+
|                              [col1] [col2] [col3] |
+---------------------------------------------------+

justify-content: space-between:
+---------------------------------------------------+
| [col1]          [col2]          [col3]             |
+---------------------------------------------------+

justify-content: space-around:
+---------------------------------------------------+
|    [col1]      [col2]      [col3]    |
+---------------------------------------------------+

justify-content: space-evenly:
+---------------------------------------------------+
|     [col1]     [col2]     [col3]     |
+---------------------------------------------------+
```

---

### 3.5 Item Properties

These properties are applied to individual **grid items**.

#### 3.5.1 grid-column (start / end, span)

Controls which columns a grid item occupies by specifying start and end grid lines.

```css
.item {
  grid-column: 1 / 3;       /* Start at line 1, end at line 3 (spans 2 columns) */
  grid-column: 1 / span 2;  /* Start at line 1, span 2 columns */
  grid-column: span 2;      /* Span 2 columns from default position */
  grid-column: 1 / -1;      /* Span the entire row (first to last line) */
}
```

```
Grid lines:   1        2        3        4
              |        |        |        |
              +--------+--------+--------+
              |        |        |        |
              +--------+--------+--------+


grid-column: 1 / 3 (spans columns 1 and 2):

  1        2        3        4
  +--------+--------+--------+
  |  This item      |        |
  |  spans 2 cols   |        |
  +--------+--------+--------+
  |        |        |        |
  +--------+--------+--------+


grid-column: 1 / -1 (spans entire row):

  1        2        3        4
  +--------+--------+--------+
  |  This item spans ALL columns  |
  +--------+--------+--------+
  |        |        |        |
  +--------+--------+--------+
```

---

#### 3.5.2 grid-row (start / end, span)

Works exactly like `grid-column` but for rows.

```css
.item {
  grid-row: 1 / 3;        /* Start at row line 1, end at row line 3 */
  grid-row: span 2;       /* Span 2 rows */
}
```

```
grid-row: 1 / 3 (spans rows 1 and 2):

  +--------+--------+--------+
  |  This  |        |        |  Row 1
  |  item  |        |        |
  |  spans |--------+--------+
  |  2     |        |        |  Row 2
  |  rows  |        |        |
  +--------+--------+--------+
  |        |        |        |  Row 3
  +--------+--------+--------+
```

**Combining grid-column and grid-row:**

```css
.item {
  grid-column: 1 / 3;   /* Span 2 columns */
  grid-row: 1 / 3;      /* Span 2 rows */
}
```

```
+------------------+--------+
|                  |        |
|  This item       |  Item  |
|  spans a 2x2     |        |
|  area            +--------+
|                  |        |
+------------------+--------+
|        |        |        |
+--------+--------+--------+
```

---

#### 3.5.3 grid-area

A shorthand for specifying both `grid-row` and `grid-column`, or for referencing a named area defined in `grid-template-areas`.

```css
/* Shorthand: row-start / column-start / row-end / column-end */
.item {
  grid-area: 1 / 1 / 3 / 3;    /* Row 1-3, Column 1-3 */
}

/* Or reference a named area */
.item {
  grid-area: header;            /* Place in the "header" area */
}
```

---

#### 3.5.4 justify-self and align-self

Override the container's `justify-items` or `align-items` for a single grid item.

```css
.container {
  display: grid;
  justify-items: stretch;   /* All items stretch by default */
}

.special {
  justify-self: center;     /* This item centers itself horizontally */
  align-self: end;          /* This item aligns to the bottom of its cell */
}
```

```
Default (stretch):            .special item:
+-----------+-----------+     +-----------+-----------+
|[ item 1  ]|[ item 2  ]|     |[ item 1  ]|           |
|           |           |     |           |           |
+-----------+-----------+     |           | [special] |
|[ item 3  ]|[ item 4  ]|     +-----------+-----------+
|           |           |     |[ item 3  ]|[ item 4  ]|
+-----------+-----------+     +-----------+-----------+

                               Item 2 is centered horizontally
                               and aligned to the bottom of its cell.
```

---

### 3.6 The fr Unit Explained

The `fr` (fraction) unit represents a fraction of the **available space** in the grid container. It is the most important unit in CSS Grid.

```css
.container {
  display: grid;
  grid-template-columns: 1fr 2fr 1fr;
}
```

```
Container width: 800px

Total fractions: 1 + 2 + 1 = 4
Each fr = 800px / 4 = 200px

+--------+------------------+--------+
| 1fr    |      2fr         | 1fr    |
| 200px  |     400px        | 200px  |
+--------+------------------+--------+


With a fixed column:
grid-template-columns: 200px 1fr 2fr;

Container: 900px
Fixed:     200px
Remaining: 700px
1fr = 700/3 = ~233px
2fr = 700*2/3 = ~467px

+--------+-----------+---------------------+
| 200px  |    1fr    |        2fr          |
| fixed  |  ~233px   |       ~467px        |
+--------+-----------+---------------------+
```

**Why `fr` instead of percentages?**

```
Using percentages with gap is problematic:

grid-template-columns: 33.33% 33.33% 33.33%;
gap: 20px;

  33.33%  +  33.33%  +  33.33%  =  100%
  But gap adds 40px more... items OVERFLOW!


Using fr with gap works perfectly:

grid-template-columns: 1fr 1fr 1fr;
gap: 20px;

  The fr unit automatically accounts for the gap.
  No overflow. No math needed.
```

---

### 3.7 Common Grid Patterns

#### Pattern 1: Holy Grail Layout (Header, Sidebar, Main, Footer)

The classic web page layout that was extremely difficult before Grid.

```css
.layout {
  display: grid;
  grid-template-columns: 250px 1fr;
  grid-template-rows: 60px 1fr 50px;
  grid-template-areas:
    "header  header"
    "sidebar main"
    "footer  footer";
  min-height: 100vh;
  gap: 0;
}

.header  { grid-area: header;  background: #2c3e50; }
.sidebar { grid-area: sidebar; background: #34495e; }
.main    { grid-area: main;    background: #ecf0f1; }
.footer  { grid-area: footer;  background: #2c3e50; }
```

```html
<div class="layout">
  <header class="header">Header</header>
  <aside class="sidebar">Sidebar</aside>
  <main class="main">Main Content</main>
  <footer class="footer">Footer</footer>
</div>
```

```
+--------------------------------------------------+
|                    HEADER                         |  60px
+------------+-------------------------------------+
|            |                                     |
|  SIDEBAR   |           MAIN CONTENT              |
|   250px    |             (1fr)                   |
|            |                                     |
|            |                                     |
|            |                                     |
+------------+-------------------------------------+
|                    FOOTER                         |  50px
+--------------------------------------------------+
```

---

#### Pattern 2: Photo Gallery

A responsive grid of images that automatically adjusts the number of columns.

```css
.gallery {
  display: grid;
  grid-template-columns: repeat(auto-fit, minmax(200px, 1fr));
  gap: 16px;
  padding: 16px;
}

.gallery img {
  width: 100%;
  height: 200px;
  object-fit: cover;
  border-radius: 8px;
}
```

```
Wide screen (5 columns):
+------+------+------+------+------+
| Img1 | Img2 | Img3 | Img4 | Img5 |
+------+------+------+------+------+
| Img6 | Img7 | Img8 | Img9 |Img10 |
+------+------+------+------+------+

Medium screen (3 columns):
+---------+---------+---------+
|  Img 1  |  Img 2  |  Img 3  |
+---------+---------+---------+
|  Img 4  |  Img 5  |  Img 6  |
+---------+---------+---------+
|  Img 7  |  Img 8  |  Img 9  |
+---------+---------+---------+

Narrow screen (2 columns):
+-------------+-------------+
|    Img 1    |    Img 2    |
+-------------+-------------+
|    Img 3    |    Img 4    |
+-------------+-------------+
```

**The magic line:** `repeat(auto-fit, minmax(200px, 1fr))` means "create as many columns as fit, each at least 200px but allowed to grow." No media queries needed.

---

#### Pattern 3: Dashboard Layout

A dashboard with cards of varying sizes.

```css
.dashboard {
  display: grid;
  grid-template-columns: repeat(4, 1fr);
  grid-template-rows: auto;
  gap: 20px;
  padding: 20px;
}

.card-wide {
  grid-column: span 2;     /* Takes 2 columns */
}

.card-tall {
  grid-row: span 2;        /* Takes 2 rows */
}

.card-large {
  grid-column: span 2;     /* Takes 2 columns */
  grid-row: span 2;        /* AND 2 rows */
}
```

```
+------------+------------+------------+------------+
|                         |            |            |
|   Large Card (2x2)      |  Card 3   |  Card 4    |
|   grid-column: span 2   |           |            |
|   grid-row: span 2      +------------+            |
|                         |            | Tall Card  |
|                         |  Card 5   | grid-row:   |
+------------+------------+------------+ span 2     |
|                                      |            |
|   Wide Card (span 2 columns)        |            |
|                                      |            |
+------------+------------+------------+------------+
|   Card 8   |  Card 9   |  Card 10  |  Card 11   |
+------------+------------+------------+------------+
```

---

## 4. Flexbox vs Grid — When to Use Which?

### Comparison Table

| Feature                     | Flexbox                          | Grid                              |
| --------------------------- | -------------------------------- | --------------------------------- |
| **Dimensions**              | One-dimensional (row OR column)  | Two-dimensional (rows AND columns)|
| **Content or Layout first** | Content-first (items define size)| Layout-first (grid defines size)  |
| **Best for**                | Components within a layout       | Overall page structure            |
| **Alignment**               | Along one axis at a time         | Along both axes simultaneously    |
| **Item sizing**             | Items determine their own size   | Grid defines cell sizes           |
| **Overlap**                 | Not possible                     | Items can overlap                 |
| **Named areas**             | Not available                    | grid-template-areas               |
| **Browser support**         | Excellent                        | Excellent                         |
| **Wrapping**                | Items wrap naturally             | Explicit tracks or auto-placement |

### Decision Diagram

```
Start: What kind of layout do you need?
         |
         v
  +------+------+
  |              |
  v              v
One direction?   Both rows AND columns?
  |              |
  v              v
FLEXBOX          GRID

More specific:

+-------------------------------------------+
|  Need to lay out items in a single        |
|  row or column?                           |
|  (navbar, toolbar, list of cards)         |
|               |                           |
|               v                           |
|           USE FLEXBOX                     |
+-------------------------------------------+

+-------------------------------------------+
|  Need to control both rows and columns    |
|  at the same time?                        |
|  (page layout, dashboard, image gallery)  |
|               |                           |
|               v                           |
|           USE GRID                        |
+-------------------------------------------+

+-------------------------------------------+
|  Want items to wrap and fill space         |
|  based on their content size?             |
|               |                           |
|               v                           |
|           USE FLEXBOX                     |
+-------------------------------------------+

+-------------------------------------------+
|  Want precise placement of items          |
|  into specific rows/columns?             |
|               |                           |
|               v                           |
|           USE GRID                        |
+-------------------------------------------+
```

### They Work Together

Flexbox and Grid are not competitors — they are complementary tools. A common pattern is to use **Grid for the overall page layout** and **Flexbox for components within the grid cells**.

```css
/* Grid for page structure */
.page {
  display: grid;
  grid-template-columns: 250px 1fr;
  grid-template-rows: 60px 1fr 50px;
  grid-template-areas:
    "header header"
    "sidebar main"
    "footer footer";
}

/* Flexbox for the navbar inside the header */
.header {
  grid-area: header;
  display: flex;                  /* Flexbox inside a grid cell */
  justify-content: space-between;
  align-items: center;
}

/* Flexbox for card layout inside main */
.main {
  grid-area: main;
  display: flex;                  /* Flexbox inside a grid cell */
  flex-wrap: wrap;
  gap: 20px;
}
```

```
+---------------------------------------------------+
| [Logo]    [Home] [About] [Contact]   [Login]      |  <-- Header (Flexbox)
+----------+----------------------------------------+
|          |  +--------+  +--------+  +--------+   |
| Nav Link |  | Card 1 |  | Card 2 |  | Card 3 |   |
| Nav Link |  +--------+  +--------+  +--------+   |  <-- Main (Flexbox
| Nav Link |  +--------+  +--------+                |       cards inside
| Nav Link |  | Card 4 |  | Card 5 |                |       Grid cell)
|          |  +--------+  +--------+                |
+----------+----------------------------------------+
|                    Footer                          |
+---------------------------------------------------+
  ^                  ^
  Grid               Grid + Flexbox
  (page layout)      (component layout)
```

---

## 5. Summary

### What We Covered

1. **The Problem:** Before Flexbox and Grid, layouts relied on floats and hacks that were fragile and hard to maintain.

2. **Flexbox** is for **one-dimensional** layouts (row or column):
   - Container properties: `display: flex`, `flex-direction`, `justify-content`, `align-items`, `align-content`, `flex-wrap`, `gap`
   - Item properties: `flex-grow`, `flex-shrink`, `flex-basis`, `flex`, `align-self`, `order`
   - Great for: navbars, centering, card rows, component-level layouts

3. **CSS Grid** is for **two-dimensional** layouts (rows and columns together):
   - Container properties: `display: grid`, `grid-template-columns`, `grid-template-rows`, `grid-template-areas`, `gap`, `justify-items`, `align-items`, `justify-content`, `align-content`
   - Item properties: `grid-column`, `grid-row`, `grid-area`, `justify-self`, `align-self`
   - Great for: page layouts, dashboards, galleries, any design that needs both rows and columns

4. **Use them together:** Grid for the macro layout, Flexbox for the micro layout within grid cells.

### Quick Reference Cheat Sheet

```
FLEXBOX (One-Dimensional):
+---------------------------------------------------------+
| Container:                                               |
|   display: flex                                          |
|   flex-direction: row | column                           |
|   justify-content: center | space-between | ...          |
|   align-items: center | flex-start | flex-end | ...      |
|   flex-wrap: wrap | nowrap                               |
|   gap: 20px                                              |
|                                                          |
| Items:                                                   |
|   flex: 1 (shorthand for grow/shrink/basis)              |
|   align-self: center | flex-end | ...                    |
|   order: 1                                               |
+---------------------------------------------------------+

GRID (Two-Dimensional):
+---------------------------------------------------------+
| Container:                                               |
|   display: grid                                          |
|   grid-template-columns: repeat(3, 1fr)                  |
|   grid-template-rows: 100px auto 1fr                     |
|   grid-template-areas: "header header" "side main"       |
|   gap: 20px                                              |
|   justify-items / align-items: start | center | end      |
|                                                          |
| Items:                                                   |
|   grid-column: 1 / 3 (or span 2)                        |
|   grid-row: 1 / 3 (or span 2)                           |
|   grid-area: header                                      |
|   justify-self / align-self: start | center | end        |
+---------------------------------------------------------+
```

### Key Takeaway

Master both Flexbox and Grid. They are not interchangeable — each has specific strengths. Flexbox excels at distributing items along a single axis, while Grid excels at placing items in a two-dimensional structure. Together, they give you complete control over any layout you can imagine.
