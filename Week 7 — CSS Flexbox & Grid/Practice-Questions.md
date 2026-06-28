# Week 7: CSS Flexbox & Grid — Practice Questions

**Total Questions: 43**

| Section | Type | Count |
|---------|------|-------|
| A | Multiple Choice Questions | 15 |
| B | Short Answer Questions | 8 |
| C | True or False | 10 |
| D | Layout Challenges | 5 |
| E | Coding Exercises | 5 |

---

## Section A: Multiple Choice Questions (MCQs)

**Q1.** What is the default value of `flex-direction`?

- A) `column`
- B) `row`
- C) `row-reverse`
- D) `column-reverse`

<details>
<summary>Answer</summary>

**B) `row`**

By default, `flex-direction` is set to `row`, which lays out flex items horizontally from left to right (in LTR languages).

</details>

---

**Q2.** Which `justify-content` value distributes items with equal space between them, but no space before the first item or after the last item?

- A) `space-around`
- B) `space-evenly`
- C) `space-between`
- D) `center`

<details>
<summary>Answer</summary>

**C) `space-between`**

`space-between` places the first item at the start, the last item at the end, and distributes remaining space equally between the items.

</details>

---

**Q3.** What does `align-items: baseline` do?

- A) Aligns items to the top of the container
- B) Aligns items so their text baselines are aligned
- C) Aligns items to the bottom of the container
- D) Stretches items to fill the container

<details>
<summary>Answer</summary>

**B) Aligns items so their text baselines are aligned**

`baseline` aligns flex items along their text baseline, which is useful when items have different font sizes but you want their text to line up.

</details>

---

**Q4.** What happens when `flex-wrap` is set to `wrap`?

- A) Items shrink to fit in one line
- B) Items overflow the container
- C) Items wrap onto multiple lines when they exceed the container width
- D) Items are hidden when they exceed the container width

<details>
<summary>Answer</summary>

**C) Items wrap onto multiple lines when they exceed the container width**

`flex-wrap: wrap` allows flex items to move to the next line instead of being forced into a single line.

</details>

---

**Q5.** In the shorthand `flex: 2 1 200px`, what does the value `1` represent?

- A) `flex-grow`
- B) `flex-shrink`
- C) `flex-basis`
- D) `flex-order`

<details>
<summary>Answer</summary>

**B) `flex-shrink`**

The `flex` shorthand follows the order: `flex-grow`, `flex-shrink`, `flex-basis`. So `flex: 2 1 200px` means `flex-grow: 2`, `flex-shrink: 1`, `flex-basis: 200px`.

</details>

---

**Q6.** What does `flex-grow: 0` mean?

- A) The item will grow to fill available space
- B) The item will not grow beyond its base size
- C) The item will shrink if necessary
- D) The item will be hidden

<details>
<summary>Answer</summary>

**B) The item will not grow beyond its base size**

When `flex-grow` is `0`, the item will not take up any additional available space in the flex container. It will remain at its base size defined by `flex-basis` or its content.

</details>

---

**Q7.** Which CSS property defines the column structure of a grid container?

- A) `grid-columns`
- B) `grid-template-rows`
- C) `grid-template-columns`
- D) `grid-column-layout`

<details>
<summary>Answer</summary>

**C) `grid-template-columns`**

`grid-template-columns` defines the number of columns and the width of each column in the grid layout.

</details>

---

**Q8.** What does `1fr` represent in CSS Grid?

- A) 1 fixed pixel
- B) 1 fraction of the available space
- C) 1 full row
- D) 1 percentage of the viewport

<details>
<summary>Answer</summary>

**B) 1 fraction of the available space**

The `fr` unit represents a fraction of the available space in the grid container. For example, `grid-template-columns: 1fr 2fr` gives the second column twice as much space as the first.

</details>

---

**Q9.** Which property is used to assign a grid item to a named area?

- A) `grid-template-areas`
- B) `grid-area`
- C) `grid-column`
- D) `grid-placement`

<details>
<summary>Answer</summary>

**B) `grid-area`**

`grid-area` is applied to a grid item to assign it to a named area defined by `grid-template-areas` on the container. For example, `grid-area: header` places the item in the area named "header".

</details>

---

**Q10.** What does the `gap` property do in Flexbox and Grid?

- A) Adds margin outside the container
- B) Adds padding inside each item
- C) Sets the spacing between rows and columns (between items)
- D) Sets the border width between items

<details>
<summary>Answer</summary>

**C) Sets the spacing between rows and columns (between items)**

The `gap` property (shorthand for `row-gap` and `column-gap`) defines the space between grid/flex items without affecting the outer edges of the container.

</details>

---

**Q11.** When should you prefer CSS Grid over Flexbox?

- A) When you need a one-dimensional layout (row or column only)
- B) When you need a two-dimensional layout (rows and columns simultaneously)
- C) When you need to center a single element
- D) When you need to style inline text elements

<details>
<summary>Answer</summary>

**B) When you need a two-dimensional layout (rows and columns simultaneously)**

CSS Grid excels at two-dimensional layouts where you need to control both rows and columns at the same time. Flexbox is better suited for one-dimensional layouts along a single axis.

</details>

---

**Q12.** What does `repeat(3, 1fr)` produce in `grid-template-columns`?

- A) A single column that is 3 fractions wide
- B) Three columns, each taking one fraction of the available space
- C) Three rows of equal height
- D) A 3-pixel wide column

<details>
<summary>Answer</summary>

**B) Three columns, each taking one fraction of the available space**

`repeat(3, 1fr)` is shorthand for `1fr 1fr 1fr`, creating three equal-width columns that each take up one-third of the available space.

</details>

---

**Q13.** What does `minmax(200px, 1fr)` do in a grid track definition?

- A) Sets the track to exactly 200px
- B) Sets the track to exactly 1fr
- C) Sets a minimum width of 200px and a maximum of 1fr (remaining space)
- D) Creates two tracks: one at 200px and one at 1fr

<details>
<summary>Answer</summary>

**C) Sets a minimum width of 200px and a maximum of 1fr (remaining space)**

`minmax(200px, 1fr)` ensures the track will be at least 200px wide but can grow to fill available space (up to `1fr`). This is commonly used for responsive grid layouts.

</details>

---

**Q14.** Which `justify-content` value places all items at the center of the main axis?

- A) `flex-start`
- B) `flex-end`
- C) `center`
- D) `stretch`

<details>
<summary>Answer</summary>

**C) `center`**

`justify-content: center` packs all flex items toward the center of the main axis, leaving equal space on both sides of the group.

</details>

---

**Q15.** What is the default value of `flex-basis`?

- A) `0`
- B) `1`
- C) `auto`
- D) `100%`

<details>
<summary>Answer</summary>

**C) `auto`**

The default value of `flex-basis` is `auto`, which means the item's size is determined by its content or any explicitly set `width`/`height` property.

</details>

---

## Section B: Short Answer Questions

**Q1.** When should you use Flexbox versus CSS Grid? Provide at least two scenarios for each.

<details>
<summary>Answer</summary>

**Use Flexbox when:**
- You need a one-dimensional layout (a single row or a single column), such as a navigation bar or a row of buttons.
- You want items to dynamically size and distribute space along one axis, such as centering content vertically and horizontally.
- You are building component-level layouts like card footers, form input groups, or toolbar items.

**Use CSS Grid when:**
- You need a two-dimensional layout controlling both rows and columns simultaneously, such as a full page layout with header, sidebar, main content, and footer.
- You want precise placement of items in specific cells or areas of a grid, such as a dashboard with widgets of different sizes.
- You need to create complex, magazine-style or asymmetric layouts where items span multiple rows or columns.

**General rule:** Flexbox is ideal for distributing items within a component; Grid is ideal for defining the overall page or section structure.

</details>

---

**Q2.** What is the `fr` unit in CSS Grid? How does it differ from percentage-based widths?

<details>
<summary>Answer</summary>

The `fr` (fractional) unit represents a fraction of the **available free space** in the grid container. Unlike percentages, which are calculated relative to the total container width (and do not account for gaps or other fixed-size tracks), the `fr` unit distributes only the **remaining space** after fixed-size tracks and gaps have been accounted for.

**Example:**
```css
grid-template-columns: 200px 1fr 2fr;
```
Here, the first column is fixed at 200px. The remaining space is divided into 3 parts: the second column gets 1 part, and the third column gets 2 parts. If percentages were used instead, you would have to manually calculate the remaining width after subtracting 200px and any gaps.

</details>

---

**Q3.** Explain the difference between `justify-content` and `align-items` in Flexbox.

<details>
<summary>Answer</summary>

- **`justify-content`** controls the alignment and distribution of flex items along the **main axis** (horizontal by default when `flex-direction` is `row`). Values include `flex-start`, `flex-end`, `center`, `space-between`, `space-around`, and `space-evenly`.

- **`align-items`** controls the alignment of flex items along the **cross axis** (vertical by default when `flex-direction` is `row`). Values include `flex-start`, `flex-end`, `center`, `stretch`, and `baseline`.

**In short:**
- `justify-content` = main axis alignment (horizontal in a row layout)
- `align-items` = cross axis alignment (vertical in a row layout)

If `flex-direction` is set to `column`, the axes are swapped: `justify-content` controls vertical distribution, and `align-items` controls horizontal alignment.

</details>

---

**Q4.** What does `flex: 1` mean? Break down what values it sets.

<details>
<summary>Answer</summary>

`flex: 1` is shorthand for:

```css
flex-grow: 1;
flex-shrink: 1;
flex-basis: 0%;
```

- **`flex-grow: 1`** — The item will grow to fill available space proportionally.
- **`flex-shrink: 1`** — The item will shrink if the container is too small.
- **`flex-basis: 0%`** — The item starts with a base size of zero before distributing space.

This means the item will expand to share all available space equally with other items that also have `flex: 1`. It is commonly used to make flex items fill their container evenly.

**Note:** `flex: 1` is different from `flex: 1 1 auto`. When you write `flex: 1`, the `flex-basis` is set to `0%`, not `auto`.

</details>

---

**Q5.** How does `grid-template-areas` work? Provide a brief example.

<details>
<summary>Answer</summary>

`grid-template-areas` allows you to define a grid layout using named areas. Each string represents a row, and each word within the string represents a cell assigned to a named area. Grid items are then placed into these areas using the `grid-area` property.

**Example:**
```css
.container {
  display: grid;
  grid-template-columns: 200px 1fr;
  grid-template-rows: 60px 1fr 50px;
  grid-template-areas:
    "header  header"
    "sidebar main"
    "footer  footer";
}

.header  { grid-area: header; }
.sidebar { grid-area: sidebar; }
.main    { grid-area: main; }
.footer  { grid-area: footer; }
```

This creates a layout where:
- The **header** spans the full width across both columns.
- The **sidebar** occupies the left column of the middle row.
- The **main** content occupies the right column of the middle row.
- The **footer** spans the full width across both columns.

Use a period (`.`) to represent an empty cell: `"header ."` leaves the second cell empty.

</details>

---

**Q6.** What is the difference between `auto-fill` and `auto-fit` in CSS Grid?

<details>
<summary>Answer</summary>

Both `auto-fill` and `auto-fit` are used with the `repeat()` function to create a dynamic number of grid tracks. The difference appears when there are **fewer items than available tracks**:

- **`auto-fill`** creates as many tracks as will fit in the container, even if some tracks are empty. Empty tracks remain and preserve their space.

- **`auto-fit`** also creates as many tracks as will fit, but **collapses empty tracks to zero width**, allowing the existing items to stretch and fill the remaining space.

**Example:**
```css
/* auto-fill: empty columns remain, items do not stretch */
grid-template-columns: repeat(auto-fill, minmax(200px, 1fr));

/* auto-fit: empty columns collapse, items stretch to fill space */
grid-template-columns: repeat(auto-fit, minmax(200px, 1fr));
```

**When to use which:**
- Use `auto-fill` when you want consistent column sizes regardless of how many items you have.
- Use `auto-fit` when you want items to expand and fill all available space.

</details>

---

**Q7.** What is the purpose of the `order` property in Flexbox? What is its default value?

<details>
<summary>Answer</summary>

The `order` property controls the **visual order** of flex items within their container, without changing the HTML source order. Items are laid out in ascending order of their `order` value.

- **Default value:** `0`
- Items with the same `order` value are displayed in their source order.
- Negative values are allowed, allowing items to appear before items with the default order.

**Example:**
```css
.item-a { order: 2; }  /* Appears third */
.item-b { order: -1; } /* Appears first */
.item-c { order: 0; }  /* Appears second (default) */
```

**Important note:** Changing visual order with `order` does not change the tab order or screen reader reading order. This can create accessibility issues if the visual order significantly differs from the source order.

</details>

---

**Q8.** Explain the `align-self` property. How does it differ from `align-items`?

<details>
<summary>Answer</summary>

- **`align-items`** is set on the **flex/grid container** and applies the same cross-axis alignment to **all** items inside it.

- **`align-self`** is set on an **individual flex/grid item** and overrides the container's `align-items` value for that specific item only.

**Example:**
```css
.container {
  display: flex;
  align-items: center; /* All items centered vertically */
}

.special-item {
  align-self: flex-end; /* This item aligns to the bottom */
}
```

Both properties accept the same values: `auto`, `flex-start`, `flex-end`, `center`, `baseline`, and `stretch`. The default value of `align-self` is `auto`, which inherits the `align-items` value from the parent container.

</details>

---

## Section C: True or False

| # | Statement | Answer |
|---|-----------|--------|
| 1 | Flexbox is a two-dimensional layout system. | **False** — Flexbox is a one-dimensional layout system. It works along either a row or a column, not both simultaneously. |
| 2 | The default value of `flex-direction` is `row`. | **True** — Flex items are laid out horizontally from left to right by default. |
| 3 | `justify-content` aligns items along the cross axis. | **False** — `justify-content` aligns items along the main axis. `align-items` handles the cross axis. |
| 4 | The `gap` property works in both Flexbox and CSS Grid. | **True** — The `gap` property is supported in both Flexbox and Grid containers in all modern browsers. |
| 5 | `grid-template-areas` requires each row string to have the same number of cell names. | **True** — Each row must have the same number of cells to form a valid rectangular grid. |
| 6 | `flex-shrink: 0` prevents a flex item from shrinking below its base size. | **True** — Setting `flex-shrink` to `0` stops the item from shrinking when the container is too small. |
| 7 | The `fr` unit can be used outside of CSS Grid (e.g., in Flexbox). | **False** — The `fr` unit is specific to CSS Grid and cannot be used with Flexbox or other layout properties. |
| 8 | `align-self` can override the `align-items` value for an individual flex item. | **True** — `align-self` on a child item takes precedence over the container's `align-items` for that item. |
| 9 | `repeat(auto-fit, minmax(200px, 1fr))` and `repeat(auto-fill, minmax(200px, 1fr))` produce identical results when all grid tracks are filled with items. | **True** — The difference between `auto-fit` and `auto-fill` only appears when there are empty tracks. |
| 10 | In CSS Grid, items can only be placed in adjacent cells and cannot span multiple rows or columns. | **False** — Grid items can span multiple rows and/or columns using `grid-row` and `grid-column` with the `span` keyword or explicit line numbers. |

---

## Section D: Layout Challenges

**Q1.** Write the CSS (using Flexbox) to achieve the following layout:

```
+------------------------------------------+
|  [Logo]              [Home] [About] [Contact] |
+------------------------------------------+
```

The logo should be on the far left, and the navigation links should be grouped on the far right.

<details>
<summary>Answer</summary>

```css
.navbar {
  display: flex;
  justify-content: space-between;
  align-items: center;
  padding: 10px 20px;
}

.logo {
  /* No special flex properties needed; stays at the start */
}

.nav-links {
  display: flex;
  gap: 20px;
}
```

```html
<nav class="navbar">
  <div class="logo">Logo</div>
  <ul class="nav-links">
    <li>Home</li>
    <li>About</li>
    <li>Contact</li>
  </ul>
</nav>
```

**Explanation:** `justify-content: space-between` pushes the logo to the left edge and the nav-links group to the right edge. The nested flex container on `.nav-links` arranges the links horizontally with a gap.

</details>

---

**Q2.** Write the CSS (using CSS Grid) to achieve the following layout:

```
+--------+--------+--------+
| Card 1 | Card 2 | Card 3 |
+--------+--------+--------+
| Card 4 | Card 5 |        |
+--------+--------+--------+
```

Three equal-width columns with a 20px gap between cards.

<details>
<summary>Answer</summary>

```css
.card-grid {
  display: grid;
  grid-template-columns: repeat(3, 1fr);
  gap: 20px;
}

.card {
  background-color: #f0f0f0;
  padding: 20px;
  border-radius: 8px;
}
```

```html
<div class="card-grid">
  <div class="card">Card 1</div>
  <div class="card">Card 2</div>
  <div class="card">Card 3</div>
  <div class="card">Card 4</div>
  <div class="card">Card 5</div>
</div>
```

**Explanation:** `repeat(3, 1fr)` creates three equal-width columns. The `gap: 20px` adds consistent spacing between all cards. Items flow automatically into the grid cells.

</details>

---

**Q3.** Write the CSS (using CSS Grid) to achieve this Holy Grail layout:

```
+------------------------------------------+
|                 HEADER                    |
+----------+--------------------+----------+
|          |                    |          |
| SIDEBAR  |       MAIN         |  ASIDE  |
|          |                    |          |
+----------+--------------------+----------+
|                 FOOTER                    |
+------------------------------------------+
```

The sidebar should be 200px, the aside should be 150px, and the main content should fill the remaining space.

<details>
<summary>Answer</summary>

```css
.layout {
  display: grid;
  grid-template-columns: 200px 1fr 150px;
  grid-template-rows: 60px 1fr 50px;
  grid-template-areas:
    "header  header  header"
    "sidebar main    aside"
    "footer  footer  footer";
  min-height: 100vh;
  gap: 0;
}

.header  { grid-area: header; }
.sidebar { grid-area: sidebar; }
.main    { grid-area: main; }
.aside   { grid-area: aside; }
.footer  { grid-area: footer; }
```

```html
<div class="layout">
  <header class="header">Header</header>
  <nav class="sidebar">Sidebar</nav>
  <main class="main">Main Content</main>
  <aside class="aside">Aside</aside>
  <footer class="footer">Footer</footer>
</div>
```

**Explanation:** `grid-template-areas` defines the visual layout using named areas. The sidebar is fixed at 200px, the aside at 150px, and `1fr` gives the main content all remaining space. `min-height: 100vh` ensures the layout fills the full viewport height.

</details>

---

**Q4.** Write the CSS to achieve the following centered layout using Flexbox:

```
+------------------------------------------+
|                                          |
|                                          |
|            +------------+                |
|            |  CENTERED  |                |
|            |    BOX     |                |
|            +------------+                |
|                                          |
|                                          |
+------------------------------------------+
```

The box should be perfectly centered both vertically and horizontally within a full-viewport container.

<details>
<summary>Answer</summary>

```css
.container {
  display: flex;
  justify-content: center;
  align-items: center;
  min-height: 100vh;
}

.centered-box {
  width: 200px;
  padding: 40px;
  background-color: #f0f0f0;
  border-radius: 8px;
  text-align: center;
}
```

```html
<div class="container">
  <div class="centered-box">
    <p>CENTERED BOX</p>
  </div>
</div>
```

**Explanation:** `justify-content: center` centers the box along the main axis (horizontal), and `align-items: center` centers it along the cross axis (vertical). `min-height: 100vh` ensures the container spans the full viewport height so the centering is visible.

</details>

---

**Q5.** Write the CSS (using CSS Grid) to achieve the following dashboard widget layout:

```
+-------------------+----------+
|                   |          |
|   LARGE WIDGET    | WIDGET 2 |
|                   |          |
+----------+--------+----------+
| WIDGET 3 |      WIDGET 4     |
+----------+-------------------+
```

The large widget spans 2 rows. Widget 4 spans 2 columns.

<details>
<summary>Answer</summary>

```css
.dashboard {
  display: grid;
  grid-template-columns: repeat(3, 1fr);
  grid-template-rows: repeat(2, 200px);
  gap: 15px;
}

.widget-large {
  grid-column: 1 / 3;   /* Spans columns 1 and 2 */
  grid-row: 1 / 2;       /* First row only */
}

.widget-2 {
  grid-column: 3 / 4;   /* Third column */
  grid-row: 1 / 2;       /* First row only */
}

.widget-3 {
  grid-column: 1 / 2;   /* First column */
  grid-row: 2 / 3;       /* Second row */
}

.widget-4 {
  grid-column: 2 / 4;   /* Spans columns 2 and 3 */
  grid-row: 2 / 3;       /* Second row */
}

.dashboard > div {
  background-color: #e8e8e8;
  border-radius: 8px;
  padding: 20px;
}
```

```html
<div class="dashboard">
  <div class="widget-large">Large Widget</div>
  <div class="widget-2">Widget 2</div>
  <div class="widget-3">Widget 3</div>
  <div class="widget-4">Widget 4</div>
</div>
```

**Explanation:** The grid has 3 columns and 2 rows. The large widget spans the first two columns of row 1 using `grid-column: 1 / 3`. Widget 4 spans the last two columns of row 2 using `grid-column: 2 / 4`. Explicit `grid-column` and `grid-row` values control the placement and spanning of each widget.

</details>

---

## Section E: Coding Exercises

### Task 1: Horizontal Navigation Bar (Flexbox)

Create a horizontal navigation bar with the following requirements:
- The company logo is on the left side.
- Navigation links (Home, About, Services, Contact) are on the right side.
- The navbar has a background color, padding, and items are vertically centered.
- Links should have hover effects.

<details>
<summary>Solution</summary>

```html
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>Flexbox Navbar</title>
  <style>
    * {
      margin: 0;
      padding: 0;
      box-sizing: border-box;
    }

    .navbar {
      display: flex;
      justify-content: space-between;
      align-items: center;
      background-color: #2c3e50;
      padding: 15px 30px;
    }

    .logo {
      color: #ecf0f1;
      font-size: 24px;
      font-weight: bold;
    }

    .nav-links {
      display: flex;
      list-style: none;
      gap: 25px;
    }

    .nav-links a {
      color: #bdc3c7;
      text-decoration: none;
      font-size: 16px;
      padding: 8px 12px;
      border-radius: 4px;
      transition: background-color 0.3s, color 0.3s;
    }

    .nav-links a:hover {
      background-color: #34495e;
      color: #ecf0f1;
    }
  </style>
</head>
<body>
  <nav class="navbar">
    <div class="logo">MyBrand</div>
    <ul class="nav-links">
      <li><a href="#">Home</a></li>
      <li><a href="#">About</a></li>
      <li><a href="#">Services</a></li>
      <li><a href="#">Contact</a></li>
    </ul>
  </nav>
</body>
</html>
```

**Key concepts used:**
- `display: flex` on the navbar container
- `justify-content: space-between` to push logo left and links right
- `align-items: center` for vertical centering
- Nested flex container on `.nav-links` with `gap` for link spacing

</details>

---

### Task 2: Responsive Card Layout (Flexbox)

Create a 3-column card layout using Flexbox with the following requirements:
- Each card has a title, description, and a button.
- Cards should be arranged in a row on large screens.
- Cards should wrap and stack vertically on smaller screens.
- Each card should have equal width on large screens.

<details>
<summary>Solution</summary>

```html
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>Flexbox Card Layout</title>
  <style>
    * {
      margin: 0;
      padding: 0;
      box-sizing: border-box;
    }

    body {
      font-family: Arial, sans-serif;
      background-color: #f5f5f5;
      padding: 40px 20px;
    }

    .card-container {
      display: flex;
      flex-wrap: wrap;
      gap: 20px;
      max-width: 1200px;
      margin: 0 auto;
    }

    .card {
      flex: 1 1 300px;
      background-color: #ffffff;
      border-radius: 8px;
      padding: 30px;
      box-shadow: 0 2px 8px rgba(0, 0, 0, 0.1);
      display: flex;
      flex-direction: column;
    }

    .card h3 {
      margin-bottom: 15px;
      color: #2c3e50;
    }

    .card p {
      color: #7f8c8d;
      line-height: 1.6;
      flex-grow: 1;
    }

    .card button {
      margin-top: 20px;
      padding: 10px 20px;
      background-color: #3498db;
      color: white;
      border: none;
      border-radius: 5px;
      cursor: pointer;
      font-size: 14px;
      transition: background-color 0.3s;
      align-self: flex-start;
    }

    .card button:hover {
      background-color: #2980b9;
    }
  </style>
</head>
<body>
  <div class="card-container">
    <div class="card">
      <h3>Web Development</h3>
      <p>Learn how to build modern, responsive websites using HTML, CSS, and JavaScript.</p>
      <button>Learn More</button>
    </div>
    <div class="card">
      <h3>Backend Development</h3>
      <p>Master server-side programming with Node.js, Express, and MongoDB for full-stack applications.</p>
      <button>Learn More</button>
    </div>
    <div class="card">
      <h3>React Framework</h3>
      <p>Build dynamic user interfaces with React, the most popular front-end JavaScript library.</p>
      <button>Learn More</button>
    </div>
  </div>
</body>
</html>
```

**Key concepts used:**
- `flex-wrap: wrap` allows cards to wrap onto the next row
- `flex: 1 1 300px` gives each card a minimum width of 300px and allows them to grow equally
- Nested flex on `.card` with `flex-direction: column` to control internal card layout
- `flex-grow: 1` on the paragraph pushes the button to the bottom consistently

</details>

---

### Task 3: Holy Grail Layout (CSS Grid)

Create a classic "Holy Grail" layout using CSS Grid with the following requirements:
- A full-width header at the top.
- A left sidebar (250px wide).
- A main content area that fills the remaining space.
- A full-width footer at the bottom.
- The layout should fill the full viewport height.

<details>
<summary>Solution</summary>

```html
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>Holy Grail Layout</title>
  <style>
    * {
      margin: 0;
      padding: 0;
      box-sizing: border-box;
    }

    body {
      font-family: Arial, sans-serif;
      min-height: 100vh;
    }

    .layout {
      display: grid;
      grid-template-columns: 250px 1fr;
      grid-template-rows: 70px 1fr 60px;
      grid-template-areas:
        "header  header"
        "sidebar main"
        "footer  footer";
      min-height: 100vh;
    }

    .header {
      grid-area: header;
      background-color: #2c3e50;
      color: white;
      display: flex;
      align-items: center;
      padding: 0 30px;
      font-size: 22px;
      font-weight: bold;
    }

    .sidebar {
      grid-area: sidebar;
      background-color: #34495e;
      color: #ecf0f1;
      padding: 20px;
    }

    .sidebar ul {
      list-style: none;
      margin-top: 10px;
    }

    .sidebar li {
      padding: 10px 0;
      border-bottom: 1px solid #4a6278;
    }

    .sidebar a {
      color: #bdc3c7;
      text-decoration: none;
    }

    .sidebar a:hover {
      color: #ecf0f1;
    }

    .main {
      grid-area: main;
      background-color: #ecf0f1;
      padding: 30px;
    }

    .main h1 {
      color: #2c3e50;
      margin-bottom: 15px;
    }

    .main p {
      color: #7f8c8d;
      line-height: 1.8;
    }

    .footer {
      grid-area: footer;
      background-color: #2c3e50;
      color: #bdc3c7;
      display: flex;
      align-items: center;
      justify-content: center;
      font-size: 14px;
    }
  </style>
</head>
<body>
  <div class="layout">
    <header class="header">My Website</header>
    <nav class="sidebar">
      <h3>Navigation</h3>
      <ul>
        <li><a href="#">Dashboard</a></li>
        <li><a href="#">Profile</a></li>
        <li><a href="#">Settings</a></li>
        <li><a href="#">Logout</a></li>
      </ul>
    </nav>
    <main class="main">
      <h1>Welcome to the Main Content</h1>
      <p>This is the holy grail layout built entirely with CSS Grid. The header spans the full width, the sidebar is fixed at 250px, the main content fills the remaining space, and the footer sits at the bottom.</p>
    </main>
    <footer class="footer">Copyright 2026. All rights reserved.</footer>
  </div>
</body>
</html>
```

**Key concepts used:**
- `grid-template-areas` for a readable, visual layout definition
- `grid-template-columns: 250px 1fr` for a fixed sidebar and fluid main area
- `grid-template-rows: 70px 1fr 60px` for fixed header/footer and flexible main row
- `min-height: 100vh` to fill the full viewport
- Flexbox used inside the header and footer for centering text

</details>

---

### Task 4: Responsive Photo Gallery (CSS Grid)

Create a responsive photo gallery using CSS Grid with the following requirements:
- Use `auto-fill` and `minmax()` to create a dynamic number of columns.
- Each photo card should have a minimum width of 250px.
- Cards should expand to fill available space.
- Add a subtle hover effect on each card.

<details>
<summary>Solution</summary>

```html
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>Photo Gallery</title>
  <style>
    * {
      margin: 0;
      padding: 0;
      box-sizing: border-box;
    }

    body {
      font-family: Arial, sans-serif;
      background-color: #1a1a2e;
      padding: 40px 20px;
    }

    h1 {
      text-align: center;
      color: #e0e0e0;
      margin-bottom: 30px;
      font-size: 28px;
    }

    .gallery {
      display: grid;
      grid-template-columns: repeat(auto-fill, minmax(250px, 1fr));
      gap: 20px;
      max-width: 1400px;
      margin: 0 auto;
    }

    .photo-card {
      background-color: #16213e;
      border-radius: 10px;
      overflow: hidden;
      transition: transform 0.3s, box-shadow 0.3s;
    }

    .photo-card:hover {
      transform: translateY(-5px);
      box-shadow: 0 10px 30px rgba(0, 0, 0, 0.4);
    }

    .photo-card img {
      width: 100%;
      height: 200px;
      object-fit: cover;
      display: block;
    }

    .photo-info {
      padding: 15px;
    }

    .photo-info h3 {
      color: #e0e0e0;
      margin-bottom: 5px;
      font-size: 16px;
    }

    .photo-info p {
      color: #8d8d8d;
      font-size: 13px;
    }
  </style>
</head>
<body>
  <h1>Photo Gallery</h1>
  <div class="gallery">
    <div class="photo-card">
      <img src="https://via.placeholder.com/400x200/3498db/ffffff?text=Mountains" alt="Mountains">
      <div class="photo-info">
        <h3>Mountain Sunrise</h3>
        <p>A beautiful sunrise over the mountains</p>
      </div>
    </div>
    <div class="photo-card">
      <img src="https://via.placeholder.com/400x200/e74c3c/ffffff?text=Ocean" alt="Ocean">
      <div class="photo-info">
        <h3>Ocean Waves</h3>
        <p>Crashing waves along the rocky coast</p>
      </div>
    </div>
    <div class="photo-card">
      <img src="https://via.placeholder.com/400x200/2ecc71/ffffff?text=Forest" alt="Forest">
      <div class="photo-info">
        <h3>Green Forest</h3>
        <p>A dense forest in the early morning mist</p>
      </div>
    </div>
    <div class="photo-card">
      <img src="https://via.placeholder.com/400x200/f39c12/ffffff?text=Desert" alt="Desert">
      <div class="photo-info">
        <h3>Desert Sunset</h3>
        <p>Golden sand dunes under a fiery sunset</p>
      </div>
    </div>
    <div class="photo-card">
      <img src="https://via.placeholder.com/400x200/9b59b6/ffffff?text=City" alt="City">
      <div class="photo-info">
        <h3>City Lights</h3>
        <p>A vibrant city skyline at night</p>
      </div>
    </div>
    <div class="photo-card">
      <img src="https://via.placeholder.com/400x200/1abc9c/ffffff?text=Lake" alt="Lake">
      <div class="photo-info">
        <h3>Calm Lake</h3>
        <p>A serene lake reflecting the surrounding trees</p>
      </div>
    </div>
  </div>
</body>
</html>
```

**Key concepts used:**
- `repeat(auto-fill, minmax(250px, 1fr))` creates as many columns as fit, each at least 250px wide
- `auto-fill` ensures columns are generated dynamically based on container width
- `minmax(250px, 1fr)` sets a minimum of 250px and allows columns to grow to fill remaining space
- `object-fit: cover` ensures images fill their container without distortion
- CSS transitions provide smooth hover effects

</details>

---

### Task 5: Dashboard Layout (Grid + Flexbox)

Build a complete dashboard layout that combines CSS Grid for the overall page structure and Flexbox for the internal component layouts. Requirements:
- **Grid** handles the outer layout: a top navigation bar, a left sidebar, and a main content area.
- **Flexbox** handles internal components: stats cards in a row, a toolbar with buttons, and a data section.
- The sidebar should be collapsible-width (250px).

<details>
<summary>Solution</summary>

```html
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>Dashboard Layout</title>
  <style>
    * {
      margin: 0;
      padding: 0;
      box-sizing: border-box;
    }

    body {
      font-family: Arial, sans-serif;
    }

    /* ============ GRID: Overall Page Structure ============ */
    .dashboard {
      display: grid;
      grid-template-columns: 250px 1fr;
      grid-template-rows: 60px 1fr;
      grid-template-areas:
        "sidebar topbar"
        "sidebar content";
      min-height: 100vh;
    }

    /* ============ Top Navigation Bar ============ */
    .topbar {
      grid-area: topbar;
      background-color: #ffffff;
      border-bottom: 1px solid #e0e0e0;
      display: flex;
      justify-content: space-between;
      align-items: center;
      padding: 0 30px;
    }

    .topbar .search-bar {
      padding: 8px 16px;
      border: 1px solid #ddd;
      border-radius: 20px;
      width: 300px;
      font-size: 14px;
      outline: none;
    }

    .topbar .user-info {
      display: flex;
      align-items: center;
      gap: 10px;
    }

    .topbar .avatar {
      width: 35px;
      height: 35px;
      border-radius: 50%;
      background-color: #3498db;
      display: flex;
      align-items: center;
      justify-content: center;
      color: white;
      font-weight: bold;
      font-size: 14px;
    }

    /* ============ Sidebar ============ */
    .sidebar {
      grid-area: sidebar;
      background-color: #2c3e50;
      color: #ecf0f1;
      padding: 20px 0;
      display: flex;
      flex-direction: column;
    }

    .sidebar .brand {
      font-size: 20px;
      font-weight: bold;
      padding: 0 20px 20px;
      border-bottom: 1px solid #34495e;
    }

    .sidebar nav {
      flex-grow: 1;
      margin-top: 20px;
    }

    .sidebar nav a {
      display: flex;
      align-items: center;
      gap: 10px;
      color: #bdc3c7;
      text-decoration: none;
      padding: 12px 20px;
      transition: background-color 0.2s;
    }

    .sidebar nav a:hover,
    .sidebar nav a.active {
      background-color: #34495e;
      color: #ecf0f1;
    }

    /* ============ Main Content Area ============ */
    .content {
      grid-area: content;
      background-color: #f5f6fa;
      padding: 30px;
      overflow-y: auto;
    }

    .content h1 {
      color: #2c3e50;
      margin-bottom: 25px;
      font-size: 24px;
    }

    /* ============ FLEXBOX: Stats Cards Row ============ */
    .stats-row {
      display: flex;
      gap: 20px;
      margin-bottom: 30px;
    }

    .stat-card {
      flex: 1;
      background-color: #ffffff;
      border-radius: 8px;
      padding: 20px;
      box-shadow: 0 2px 6px rgba(0, 0, 0, 0.08);
      display: flex;
      flex-direction: column;
    }

    .stat-card .stat-label {
      font-size: 13px;
      color: #95a5a6;
      text-transform: uppercase;
      letter-spacing: 1px;
    }

    .stat-card .stat-value {
      font-size: 28px;
      font-weight: bold;
      color: #2c3e50;
      margin-top: 8px;
    }

    .stat-card .stat-change {
      font-size: 13px;
      margin-top: 5px;
      color: #27ae60;
    }

    /* ============ FLEXBOX: Toolbar ============ */
    .toolbar {
      display: flex;
      justify-content: space-between;
      align-items: center;
      margin-bottom: 20px;
    }

    .toolbar h2 {
      color: #2c3e50;
      font-size: 18px;
    }

    .toolbar .actions {
      display: flex;
      gap: 10px;
    }

    .toolbar button {
      padding: 8px 16px;
      border: none;
      border-radius: 5px;
      cursor: pointer;
      font-size: 13px;
      transition: background-color 0.2s;
    }

    .btn-primary {
      background-color: #3498db;
      color: white;
    }

    .btn-primary:hover {
      background-color: #2980b9;
    }

    .btn-secondary {
      background-color: #ecf0f1;
      color: #2c3e50;
    }

    .btn-secondary:hover {
      background-color: #dfe6e9;
    }

    /* ============ Data Table Section ============ */
    .data-section {
      background-color: #ffffff;
      border-radius: 8px;
      box-shadow: 0 2px 6px rgba(0, 0, 0, 0.08);
      overflow: hidden;
    }

    .data-section table {
      width: 100%;
      border-collapse: collapse;
    }

    .data-section th,
    .data-section td {
      text-align: left;
      padding: 14px 20px;
      border-bottom: 1px solid #f0f0f0;
      font-size: 14px;
    }

    .data-section th {
      background-color: #fafafa;
      color: #95a5a6;
      text-transform: uppercase;
      font-size: 12px;
      letter-spacing: 1px;
    }

    .data-section td {
      color: #2c3e50;
    }
  </style>
</head>
<body>
  <!-- GRID: Overall Page Structure -->
  <div class="dashboard">

    <!-- Sidebar (uses Flexbox internally for vertical layout) -->
    <aside class="sidebar">
      <div class="brand">Dashboard</div>
      <nav>
        <a href="#" class="active">Overview</a>
        <a href="#">Analytics</a>
        <a href="#">Customers</a>
        <a href="#">Products</a>
        <a href="#">Orders</a>
        <a href="#">Settings</a>
      </nav>
    </aside>

    <!-- Top Bar (uses Flexbox for horizontal layout) -->
    <header class="topbar">
      <input type="text" class="search-bar" placeholder="Search...">
      <div class="user-info">
        <span>Admin User</span>
        <div class="avatar">A</div>
      </div>
    </header>

    <!-- Main Content Area -->
    <main class="content">
      <h1>Overview</h1>

      <!-- FLEXBOX: Stats Cards in a Row -->
      <div class="stats-row">
        <div class="stat-card">
          <span class="stat-label">Total Users</span>
          <span class="stat-value">12,845</span>
          <span class="stat-change">+12% from last month</span>
        </div>
        <div class="stat-card">
          <span class="stat-label">Revenue</span>
          <span class="stat-value">$48,290</span>
          <span class="stat-change">+8% from last month</span>
        </div>
        <div class="stat-card">
          <span class="stat-label">Orders</span>
          <span class="stat-value">1,340</span>
          <span class="stat-change">+23% from last month</span>
        </div>
        <div class="stat-card">
          <span class="stat-label">Conversion</span>
          <span class="stat-value">3.6%</span>
          <span class="stat-change">+2% from last month</span>
        </div>
      </div>

      <!-- FLEXBOX: Toolbar with Title and Action Buttons -->
      <div class="toolbar">
        <h2>Recent Orders</h2>
        <div class="actions">
          <button class="btn-secondary">Export</button>
          <button class="btn-primary">Add Order</button>
        </div>
      </div>

      <!-- Data Table Section -->
      <div class="data-section">
        <table>
          <thead>
            <tr>
              <th>Order ID</th>
              <th>Customer</th>
              <th>Product</th>
              <th>Amount</th>
              <th>Status</th>
            </tr>
          </thead>
          <tbody>
            <tr>
              <td>#ORD-001</td>
              <td>Ali Khan</td>
              <td>Laptop Pro 15</td>
              <td>$1,299</td>
              <td>Completed</td>
            </tr>
            <tr>
              <td>#ORD-002</td>
              <td>Sara Ahmed</td>
              <td>Wireless Mouse</td>
              <td>$49</td>
              <td>Pending</td>
            </tr>
            <tr>
              <td>#ORD-003</td>
              <td>Usman Tariq</td>
              <td>Mechanical Keyboard</td>
              <td>$129</td>
              <td>Shipped</td>
            </tr>
            <tr>
              <td>#ORD-004</td>
              <td>Fatima Noor</td>
              <td>Monitor 27"</td>
              <td>$399</td>
              <td>Completed</td>
            </tr>
            <tr>
              <td>#ORD-005</td>
              <td>Hassan Raza</td>
              <td>USB-C Hub</td>
              <td>$59</td>
              <td>Processing</td>
            </tr>
          </tbody>
        </table>
      </div>
    </main>
  </div>
</body>
</html>
```

**Key concepts demonstrated:**
- **CSS Grid** manages the overall page layout: sidebar, topbar, and content area using `grid-template-areas`
- **Flexbox** is used inside components:
  - Sidebar uses `flex-direction: column` for vertical navigation layout
  - Topbar uses `justify-content: space-between` for search bar and user info
  - Stats row uses `flex: 1` for equal-width cards
  - Toolbar uses Flexbox to separate the title from action buttons
- This pattern of Grid for page structure and Flexbox for component internals is a widely used best practice in modern web development

</details>

---

**End of Practice Questions**
