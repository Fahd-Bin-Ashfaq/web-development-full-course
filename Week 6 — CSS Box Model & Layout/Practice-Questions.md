# Week 6: CSS Box Model & Layout - Practice Questions

**Total Questions: 43**

| Section | Type | Count |
|---------|------|-------|
| A | Multiple Choice Questions | 15 |
| B | Short Answer Questions | 8 |
| C | True or False | 10 |
| D | Box Model Calculations | 5 |
| E | Coding Exercises | 5 |

---

## Section A: Multiple Choice Questions (MCQs)

**Q1.** Which of the following is NOT a component of the CSS Box Model?

- A) Content
- B) Padding
- C) Shadow
- D) Border

<details>
<summary>Answer</summary>

**C) Shadow**

The CSS Box Model consists of four components: Content, Padding, Border, and Margin. Shadow is a visual effect applied via `box-shadow` and is not part of the box model.

</details>

---

**Q2.** What is the correct order of the CSS Box Model layers from inside to outside?

- A) Margin, Border, Padding, Content
- B) Content, Padding, Border, Margin
- C) Content, Border, Padding, Margin
- D) Padding, Content, Border, Margin

<details>
<summary>Answer</summary>

**B) Content, Padding, Border, Margin**

The box model layers from innermost to outermost are: Content, Padding, Border, and Margin.

</details>

---

**Q3.** Which CSS property changes the box model calculation method?

- A) `display`
- B) `box-sizing`
- C) `box-model`
- D) `size-mode`

<details>
<summary>Answer</summary>

**B) `box-sizing`**

The `box-sizing` property determines how the total width and height of an element are calculated. It accepts values `content-box` (default) and `border-box`.

</details>

---

**Q4.** When `box-sizing: border-box` is applied, the `width` property includes which of the following?

- A) Content only
- B) Content + Padding
- C) Content + Padding + Border
- D) Content + Padding + Border + Margin

<details>
<summary>Answer</summary>

**C) Content + Padding + Border**

With `border-box`, the specified `width` includes the content, padding, and border. Margin is always calculated separately and is never included in the width.

</details>

---

**Q5.** Which display type allows setting width and height while still flowing inline with other elements?

- A) `block`
- B) `inline`
- C) `inline-block`
- D) `none`

<details>
<summary>Answer</summary>

**C) `inline-block`**

`inline-block` elements flow inline like text but accept width, height, and vertical margin/padding just like block elements.

</details>

---

**Q6.** What happens when you apply `display: none` to an element?

- A) The element becomes invisible but still occupies space
- B) The element is removed from the document flow and takes no space
- C) The element becomes transparent
- D) The element moves behind other elements

<details>
<summary>Answer</summary>

**B) The element is removed from the document flow and takes no space**

`display: none` completely removes the element from the layout. It is not rendered and does not occupy any space on the page.

</details>

---

**Q7.** Which `position` value positions an element relative to the browser viewport and does not scroll with the page?

- A) `absolute`
- B) `relative`
- C) `fixed`
- D) `sticky`

<details>
<summary>Answer</summary>

**C) `fixed`**

`position: fixed` positions an element relative to the viewport. It stays in the same place even when the page is scrolled.

</details>

---

**Q8.** What is the default value of the `position` property in CSS?

- A) `relative`
- B) `absolute`
- C) `fixed`
- D) `static`

<details>
<summary>Answer</summary>

**D) `static`**

By default, all HTML elements have `position: static`. Static elements are positioned according to the normal document flow, and `top`, `right`, `bottom`, `left`, and `z-index` properties have no effect on them.

</details>

---

**Q9.** Which of the following is true about `position: absolute`?

- A) The element is positioned relative to the viewport
- B) The element is positioned relative to its nearest positioned ancestor
- C) The element remains in the normal document flow
- D) The element scrolls with the page content

<details>
<summary>Answer</summary>

**B) The element is positioned relative to its nearest positioned ancestor**

An absolutely positioned element is removed from the normal flow and positioned relative to its closest ancestor that has a position value other than `static`. If no such ancestor exists, it is positioned relative to the initial containing block (the `<html>` element).

</details>

---

**Q10.** What does `z-index` control?

- A) The horizontal position of an element
- B) The zoom level of an element
- C) The stacking order of overlapping elements
- D) The vertical alignment of an element

<details>
<summary>Answer</summary>

**C) The stacking order of overlapping elements**

`z-index` determines which element appears on top when elements overlap. A higher `z-index` value means the element is rendered in front of elements with a lower value. It only works on positioned elements (not `static`).

</details>

---

**Q11.** What is margin collapse?

- A) Margins of adjacent elements are added together
- B) The larger of two adjacent vertical margins is used instead of their sum
- C) Margins are removed when elements touch
- D) Margins collapse to zero on inline elements

<details>
<summary>Answer</summary>

**B) The larger of two adjacent vertical margins is used instead of their sum**

When vertical margins of two block-level elements meet, they collapse into a single margin equal to the larger of the two. This behavior only occurs with vertical (top and bottom) margins, not horizontal (left and right) margins.

</details>

---

**Q12.** Which `overflow` value hides content that overflows the element's box and provides a scrollbar only when needed?

- A) `overflow: hidden`
- B) `overflow: scroll`
- C) `overflow: auto`
- D) `overflow: visible`

<details>
<summary>Answer</summary>

**C) `overflow: auto`**

`overflow: auto` adds scrollbars only when the content actually overflows the element's box. `scroll` always shows scrollbars regardless of content size, `hidden` clips the content without any scrollbar, and `visible` (default) lets the content overflow without clipping.

</details>

---

**Q13.** Which of the following properties does NOT work on an `inline` element?

- A) `color`
- B) `width`
- C) `font-size`
- D) `padding-left`

<details>
<summary>Answer</summary>

**B) `width`**

Inline elements do not respect `width` and `height` properties. Their dimensions are determined by their content. Properties like `color`, `font-size`, and horizontal padding still apply to inline elements.

</details>

---

**Q14.** What does `position: sticky` do?

- A) The element sticks to the bottom of the page
- B) The element behaves like `relative` until a scroll threshold is reached, then behaves like `fixed`
- C) The element is always fixed to the viewport
- D) The element is glued to its parent element and cannot move

<details>
<summary>Answer</summary>

**B) The element behaves like `relative` until a scroll threshold is reached, then behaves like `fixed`**

A sticky element toggles between `relative` and `fixed` positioning depending on the user's scroll position. It is positioned relative until it crosses a specified threshold (set with `top`, `right`, `bottom`, or `left`), at which point it becomes fixed within its containing block.

</details>

---

**Q15.** When using `float: left` on an element, what happens to the surrounding text?

- A) The text is hidden behind the floated element
- B) The text wraps around the right side of the floated element
- C) The text moves below the floated element
- D) The text is not affected

<details>
<summary>Answer</summary>

**B) The text wraps around the right side of the floated element**

When an element is floated to the left, it is taken out of the normal flow and pushed to the left side of its container. Surrounding inline content (such as text) wraps around the right side of the floated element.

</details>

---

## Section B: Short Answer Questions

**Q1.** Explain the CSS Box Model with a diagram.

<details>
<summary>Answer</summary>

The CSS Box Model describes how every HTML element is rendered as a rectangular box. Each box consists of four layers:

```
+--------------------------------------+
|              MARGIN                  |
|  +--------------------------------+  |
|  |            BORDER              |  |
|  |  +--------------------------+  |  |
|  |  |         PADDING          |  |  |
|  |  |  +--------------------+  |  |  |
|  |  |  |                    |  |  |  |
|  |  |  |     CONTENT        |  |  |  |
|  |  |  |                    |  |  |  |
|  |  |  +--------------------+  |  |  |
|  |  +--------------------------+  |  |
|  +--------------------------------+  |
+--------------------------------------+
```

1. **Content**: The innermost area where text, images, and other media are displayed. Its size is controlled by `width` and `height`.
2. **Padding**: The transparent space between the content and the border. It pushes the border outward from the content. Controlled by `padding` properties.
3. **Border**: The layer that wraps around the padding. It has a visible edge that can be styled with `border-width`, `border-style`, and `border-color`.
4. **Margin**: The outermost transparent space that separates the element from neighboring elements. Controlled by `margin` properties.

The total space an element occupies (using the default `content-box` model) is calculated as:

**Total Width** = margin-left + border-left + padding-left + width + padding-right + border-right + margin-right

**Total Height** = margin-top + border-top + padding-top + height + padding-bottom + border-bottom + margin-bottom

</details>

---

**Q2.** What is the difference between padding and margin?

<details>
<summary>Answer</summary>

| Feature | Padding | Margin |
|---------|---------|--------|
| **Location** | Space between the content and the border (inside the border) | Space outside the border (between the element and other elements) |
| **Background** | Inherits the element's background color | Always transparent |
| **Collapse** | Does not collapse | Vertical margins collapse between adjacent block elements |
| **Negative Values** | Does not accept negative values | Accepts negative values (can overlap elements) |
| **Click Area** | Part of the element's clickable area | Not part of the element's clickable area |
| **Purpose** | Creates internal spacing within an element | Creates external spacing between elements |

**Example:**
```css
.box {
  padding: 20px; /* Space inside the border */
  margin: 20px;  /* Space outside the border */
}
```

</details>

---

**Q3.** What is margin collapse? When does it occur and when does it not?

<details>
<summary>Answer</summary>

**Margin collapse** is a behavior in CSS where the vertical margins of adjacent block-level elements combine into a single margin instead of being added together. The resulting margin equals the larger of the two margins.

**When margin collapse occurs:**

1. **Adjacent siblings**: The bottom margin of one element and the top margin of the next sibling collapse.
2. **Parent and first/last child**: If there is no border, padding, or inline content separating a parent's margin from its child's margin, they collapse.
3. **Empty blocks**: If a block element has no height, padding, border, or content, its top and bottom margins collapse into one.

**When margin collapse does NOT occur:**

1. Horizontal (left and right) margins never collapse.
2. Margins of floated elements do not collapse.
3. Margins of absolutely or fixed positioned elements do not collapse.
4. Margins of `inline-block` elements do not collapse.
5. Elements with `overflow` set to anything other than `visible` do not collapse with their children.
6. Margins of flex items and grid items do not collapse.

**Example:**
```css
.box-a { margin-bottom: 30px; }
.box-b { margin-top: 20px; }
/* The gap between them is 30px, NOT 50px */
```

</details>

---

**Q4.** What is the difference between `content-box` and `border-box`?

<details>
<summary>Answer</summary>

These are the two values for the `box-sizing` property that determine how the `width` and `height` of an element are calculated.

**`content-box` (default):**
- `width` and `height` apply only to the content area.
- Padding and border are added on top of the specified width/height.
- Total element size = width + padding + border (+ margin for total space).

```css
.box {
  box-sizing: content-box;
  width: 200px;
  padding: 20px;
  border: 5px solid black;
}
/* Rendered width = 200 + 20 + 20 + 5 + 5 = 250px */
```

**`border-box`:**
- `width` and `height` include the content, padding, and border.
- Padding and border are drawn inside the specified width/height, reducing the content area.
- Total element size = width (+ margin for total space).

```css
.box {
  box-sizing: border-box;
  width: 200px;
  padding: 20px;
  border: 5px solid black;
}
/* Rendered width = 200px (content area = 200 - 20 - 20 - 5 - 5 = 150px) */
```

**Best Practice:** Most developers use `border-box` globally because it makes sizing more predictable:
```css
*, *::before, *::after {
  box-sizing: border-box;
}
```

</details>

---

**Q5.** What is the difference between `display: none` and `visibility: hidden`?

<details>
<summary>Answer</summary>

| Feature | `display: none` | `visibility: hidden` |
|---------|-----------------|----------------------|
| **Visibility** | Element is not visible | Element is not visible |
| **Space** | Element is removed from the document flow and occupies no space | Element remains in the document flow and its space is preserved |
| **DOM** | Element still exists in the DOM but is not rendered | Element exists in the DOM and is rendered (just invisible) |
| **Child Elements** | All child elements are also hidden and cannot be made visible independently | Child elements can be made visible using `visibility: visible` |
| **Events** | Element cannot receive click or hover events | Element does not receive click or hover events |
| **Transitions** | Cannot be animated with CSS transitions | Can be animated with CSS transitions |
| **Screen Readers** | Content is not read by screen readers | Content may still be read by some screen readers |

**Example:**
```css
.hidden-none { display: none; }       /* Gone from layout */
.hidden-visible { visibility: hidden; } /* Invisible but space is kept */
```

</details>

---

**Q6.** When should you use `position: absolute` vs `position: fixed`?

<details>
<summary>Answer</summary>

**Use `position: absolute` when:**

- You need to position an element relative to a specific parent container (the nearest positioned ancestor).
- The element should scroll with the page along with its parent.
- You are creating overlays, tooltips, dropdown menus, or badges that are tied to a particular component.

```css
.parent {
  position: relative; /* Establishes positioning context */
}
.child {
  position: absolute;
  top: 10px;
  right: 10px;
}
```

**Use `position: fixed` when:**

- You need an element to stay in the same position on the screen regardless of scrolling.
- The element should be positioned relative to the browser viewport.
- You are creating sticky navigation bars, floating action buttons, cookie banners, or persistent chat widgets.

```css
.navbar {
  position: fixed;
  top: 0;
  left: 0;
  width: 100%;
}
```

**Key Difference Summary:**
- `absolute` is relative to the nearest positioned ancestor and scrolls with the page.
- `fixed` is relative to the viewport and stays in place during scrolling.

</details>

---

**Q7.** What is `z-index` and how does it work?

<details>
<summary>Answer</summary>

`z-index` is a CSS property that controls the stacking order of positioned elements along the z-axis (the axis coming towards the viewer). When elements overlap, `z-index` determines which element appears in front.

**Key Rules:**

1. `z-index` only works on elements with a `position` value other than `static` (i.e., `relative`, `absolute`, `fixed`, or `sticky`).
2. A higher `z-index` value means the element is rendered in front of elements with a lower value.
3. Elements with the same `z-index` are stacked in the order they appear in the HTML (later elements appear on top).
4. `z-index` can accept negative values, which place the element behind the normal flow.
5. `z-index` creates a **stacking context** -- a child element's `z-index` is only compared with other elements in the same stacking context, not globally.

**Example:**
```css
.box-a {
  position: relative;
  z-index: 1;   /* Behind */
}
.box-b {
  position: relative;
  z-index: 10;  /* In front */
}
.box-c {
  position: relative;
  z-index: 5;   /* Between A and B */
}
```

**Stacking order (back to front):** box-a (1) -> box-c (5) -> box-b (10)

</details>

---

**Q8.** What is the `overflow` property and what are its possible values?

<details>
<summary>Answer</summary>

The `overflow` property controls what happens when content is too large to fit inside an element's box.

**Values:**

| Value | Behavior |
|-------|----------|
| `visible` (default) | Content is not clipped and may overflow outside the element's box |
| `hidden` | Content that overflows is clipped and not visible. No scrollbar is provided |
| `scroll` | Content is clipped, and scrollbars are always shown (even if content fits) |
| `auto` | Content is clipped, and scrollbars appear only when the content actually overflows |

**Axis-Specific Properties:**
- `overflow-x`: Controls horizontal overflow only.
- `overflow-y`: Controls vertical overflow only.

**Example:**
```css
.container {
  width: 300px;
  height: 200px;
  overflow: auto; /* Scrollbar appears only when needed */
}

.no-scroll {
  overflow: hidden; /* Clips overflowing content */
}
```

**Note:** Setting `overflow` to any value other than `visible` creates a new block formatting context, which prevents margin collapse with child elements.

</details>

---

## Section C: True or False

| # | Statement | Answer | Explanation |
|---|-----------|--------|-------------|
| 1 | The default value of `box-sizing` is `border-box`. | **False** | The default value is `content-box`. With `content-box`, `width` and `height` apply only to the content area, and padding and border are added outside. |
| 2 | Margin can have negative values. | **True** | Negative margins are valid in CSS. They can pull an element closer to its neighbors or even overlap them. |
| 3 | Padding is transparent and does not show the element's background color. | **False** | Padding inherits the element's background color. The background extends through the content and padding areas, stopping at the border. |
| 4 | `display: inline-block` elements respect `width` and `height` properties. | **True** | Unlike `inline` elements, `inline-block` elements accept `width`, `height`, and vertical margin/padding while still flowing inline. |
| 5 | Horizontal margins (left and right) collapse just like vertical margins. | **False** | Only vertical (top and bottom) margins collapse. Horizontal margins never collapse; they are always added together. |
| 6 | An element with `position: absolute` is positioned relative to the viewport. | **False** | An absolutely positioned element is positioned relative to its nearest positioned ancestor (an ancestor with `position` set to `relative`, `absolute`, `fixed`, or `sticky`). If no positioned ancestor exists, it is positioned relative to the initial containing block. |
| 7 | `z-index` works on elements with `position: static`. | **False** | `z-index` only takes effect on elements that have a `position` value other than `static` (i.e., `relative`, `absolute`, `fixed`, or `sticky`). |
| 8 | The `float` property removes an element from the normal document flow. | **True** | A floated element is taken out of the normal flow and shifted to the left or right of its container. Surrounding inline content wraps around it. |
| 9 | `visibility: hidden` removes an element from the document flow. | **False** | `visibility: hidden` makes the element invisible but it still occupies space in the layout. To remove it from the flow, use `display: none`. |
| 10 | `overflow: auto` always shows scrollbars on the element. | **False** | `overflow: auto` shows scrollbars only when the content actually overflows the element. `overflow: scroll` always shows scrollbars regardless of whether the content overflows. |

---

## Section D: Box Model Calculation Questions

**Q1.** An element has the following CSS (default `box-sizing: content-box`):

```css
.box {
  width: 300px;
  height: 200px;
  padding: 20px;
  border: 5px solid black;
  margin: 15px;
}
```

Calculate the total width and total height of the space this element occupies.

<details>
<summary>Answer</summary>

**Box Sizing: `content-box` (default)**

**Total Width:**

| Component | Left | Right |
|-----------|------|-------|
| Margin | 15px | 15px |
| Border | 5px | 5px |
| Padding | 20px | 20px |
| Content | 300px | -- |

Total Width = 15 + 5 + 20 + 300 + 20 + 5 + 15 = **380px**

**Total Height:**

| Component | Top | Bottom |
|-----------|-----|--------|
| Margin | 15px | 15px |
| Border | 5px | 5px |
| Padding | 20px | 20px |
| Content | 200px | -- |

Total Height = 15 + 5 + 20 + 200 + 20 + 5 + 15 = **280px**

**Rendered box (visible area, excluding margin):** 350px wide x 250px tall

</details>

---

**Q2.** The same element now uses `box-sizing: border-box`:

```css
.box {
  box-sizing: border-box;
  width: 300px;
  height: 200px;
  padding: 20px;
  border: 5px solid black;
  margin: 15px;
}
```

Calculate the total width, total height, and the actual content area dimensions.

<details>
<summary>Answer</summary>

**Box Sizing: `border-box`**

With `border-box`, the `width` and `height` include content + padding + border.

**Content Area Width:**

Content Width = width - padding-left - padding-right - border-left - border-right
Content Width = 300 - 20 - 20 - 5 - 5 = **250px**

**Content Area Height:**

Content Height = height - padding-top - padding-bottom - border-top - border-bottom
Content Height = 200 - 20 - 20 - 5 - 5 = **150px**

**Total Space Occupied:**

Total Width = margin-left + width + margin-right = 15 + 300 + 15 = **330px**

Total Height = margin-top + height + margin-bottom = 15 + 200 + 15 = **230px**

**Rendered box (visible area, excluding margin):** 300px wide x 200px tall

</details>

---

**Q3.** Two vertically adjacent elements have the following CSS:

```css
.box-a {
  margin-bottom: 40px;
}
.box-b {
  margin-top: 25px;
}
```

What is the actual vertical gap between these two elements?

<details>
<summary>Answer</summary>

**The actual gap is 40px, NOT 65px.**

Due to **margin collapse**, when two vertical margins meet, they do not add together. Instead, the larger margin wins.

- `.box-a` bottom margin: 40px
- `.box-b` top margin: 25px
- Collapsed margin = max(40px, 25px) = **40px**

If you want the full 65px gap, you can prevent margin collapse by:
- Adding a border or padding to the separating area
- Using `display: inline-block` on one of the elements
- Using `overflow: hidden` on the parent
- Using flexbox or grid layout

</details>

---

**Q4.** An element has the following CSS with `content-box`:

```css
.card {
  box-sizing: content-box;
  width: 250px;
  padding: 10px 30px;
  border: 2px solid gray;
  margin: 5px 10px;
}
```

Calculate the total horizontal space the element occupies.

<details>
<summary>Answer</summary>

**Note:** The shorthand `padding: 10px 30px` means 10px top/bottom and 30px left/right. Similarly, `margin: 5px 10px` means 5px top/bottom and 10px left/right.

**Total Horizontal Space:**

| Component | Left | Right |
|-----------|------|-------|
| Margin | 10px | 10px |
| Border | 2px | 2px |
| Padding | 30px | 30px |
| Content | 250px | -- |

Total Width = 10 + 2 + 30 + 250 + 30 + 2 + 10 = **334px**

**Rendered box width (excluding margin):** 314px

</details>

---

**Q5.** You want a `border-box` element to have a content area exactly 400px wide. It has the following padding and border:

```css
.container {
  box-sizing: border-box;
  padding: 25px;
  border: 3px solid black;
}
```

What value should you set for the `width` property?

<details>
<summary>Answer</summary>

With `border-box`, the `width` must include the content, padding, and border.

**Calculation:**

Width = Content + Padding-Left + Padding-Right + Border-Left + Border-Right
Width = 400 + 25 + 25 + 3 + 3 = **456px**

```css
.container {
  box-sizing: border-box;
  width: 456px;
  padding: 25px;
  border: 3px solid black;
}
/* The content area will be exactly 400px wide */
```

</details>

---

## Section E: Coding Exercises

### Task 1: Demonstrate the CSS Box Model

Create three card elements that clearly demonstrate each layer of the CSS Box Model (content, padding, border, and margin).

**Requirements:**
- Each card should have visible padding, a styled border, and margin separating it from other cards.
- Use different background colors to make the padding area visible.
- Add text content inside each card.
- Use `box-sizing: border-box` for all cards.

<details>
<summary>Solution</summary>

```html
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>Box Model Demo</title>
  <style>
    * {
      box-sizing: border-box;
    }

    body {
      font-family: Arial, sans-serif;
      background-color: #f0f0f0;
      padding: 20px;
    }

    .card {
      width: 350px;
      background-color: #e0f7fa;
      padding: 30px;
      border: 4px solid #00796b;
      margin: 20px auto;
      border-radius: 8px;
    }

    .card h3 {
      margin-top: 0;
      color: #00796b;
    }

    .card-highlight {
      background-color: #fff3e0;
      border: 4px dashed #e65100;
      padding: 40px;
      margin: 30px auto;
    }

    .card-minimal {
      background-color: #fce4ec;
      border: 2px solid #c62828;
      padding: 15px;
      margin: 10px auto;
    }
  </style>
</head>
<body>
  <h1>CSS Box Model Demonstration</h1>

  <div class="card">
    <h3>Card 1 - Standard Box</h3>
    <p>This card has 30px padding, a 4px solid border, and 20px margin. The background color fills the padding area.</p>
  </div>

  <div class="card card-highlight">
    <h3>Card 2 - Large Padding & Margin</h3>
    <p>This card has 40px padding, a 4px dashed border, and 30px margin. Notice the extra space inside and outside the border.</p>
  </div>

  <div class="card card-minimal">
    <h3>Card 3 - Minimal Spacing</h3>
    <p>This card has 15px padding, a 2px solid border, and 10px margin. Compact and tight layout.</p>
  </div>
</body>
</html>
```

</details>

---

### Task 2: Center a Div Horizontally and Vertically

Center a box (200px x 200px) both horizontally and vertically on the page using three different methods.

**Requirements:**
- Method 1: Using `position: absolute` with `transform`
- Method 2: Using Flexbox
- Method 3: Using `margin: auto` with `position: absolute`

<details>
<summary>Solution</summary>

```html
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>Centering Methods</title>
  <style>
    * {
      box-sizing: border-box;
      margin: 0;
      padding: 0;
    }

    body {
      font-family: Arial, sans-serif;
    }

    .container {
      width: 100%;
      height: 300px;
      background-color: #f5f5f5;
      margin-bottom: 20px;
      position: relative;
      border: 2px solid #ccc;
    }

    .box {
      width: 200px;
      height: 200px;
      display: flex;
      align-items: center;
      justify-content: center;
      color: white;
      font-weight: bold;
      text-align: center;
      border-radius: 8px;
    }

    /* Method 1: Absolute + Transform */
    .method-1 .box {
      background-color: #1976d2;
      position: absolute;
      top: 50%;
      left: 50%;
      transform: translate(-50%, -50%);
    }

    /* Method 2: Flexbox */
    .method-2 {
      display: flex;
      justify-content: center;
      align-items: center;
    }
    .method-2 .box {
      background-color: #388e3c;
    }

    /* Method 3: Absolute + Margin Auto */
    .method-3 .box {
      background-color: #d32f2f;
      position: absolute;
      top: 0;
      right: 0;
      bottom: 0;
      left: 0;
      margin: auto;
    }

    h2 {
      padding: 10px 20px;
      background-color: #333;
      color: white;
    }
  </style>
</head>
<body>
  <h2>Method 1: position: absolute + transform</h2>
  <div class="container method-1">
    <div class="box">Centered with<br>Transform</div>
  </div>

  <h2>Method 2: Flexbox</h2>
  <div class="container method-2">
    <div class="box">Centered with<br>Flexbox</div>
  </div>

  <h2>Method 3: position: absolute + margin: auto</h2>
  <div class="container method-3">
    <div class="box">Centered with<br>Margin Auto</div>
  </div>
</body>
</html>
```

</details>

---

### Task 3: Sticky Header and Fixed Footer Layout

Create a webpage layout with a sticky header that stays at the top while scrolling and a fixed footer that always remains at the bottom of the viewport.

**Requirements:**
- The header should use `position: sticky`.
- The footer should use `position: fixed`.
- Add enough content to make the page scrollable.
- Ensure the main content is not hidden behind the header or footer.

<details>
<summary>Solution</summary>

```html
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>Sticky Header & Fixed Footer</title>
  <style>
    * {
      box-sizing: border-box;
      margin: 0;
      padding: 0;
    }

    body {
      font-family: Arial, sans-serif;
      padding-bottom: 60px; /* Space for fixed footer */
    }

    /* Sticky Header */
    header {
      position: sticky;
      top: 0;
      background-color: #1a237e;
      color: white;
      padding: 15px 30px;
      z-index: 100;
      box-shadow: 0 2px 5px rgba(0, 0, 0, 0.3);
    }

    header h1 {
      font-size: 1.5rem;
    }

    /* Main Content */
    main {
      max-width: 800px;
      margin: 0 auto;
      padding: 30px 20px;
    }

    .section {
      margin-bottom: 30px;
      padding: 25px;
      background-color: #f5f5f5;
      border-left: 4px solid #1a237e;
      border-radius: 4px;
    }

    .section h2 {
      margin-bottom: 15px;
      color: #1a237e;
    }

    .section p {
      line-height: 1.8;
      color: #333;
    }

    /* Fixed Footer */
    footer {
      position: fixed;
      bottom: 0;
      left: 0;
      width: 100%;
      background-color: #333;
      color: white;
      text-align: center;
      padding: 15px;
      z-index: 100;
      box-shadow: 0 -2px 5px rgba(0, 0, 0, 0.3);
    }
  </style>
</head>
<body>
  <header>
    <h1>Sticky Header - Scroll Down to Test</h1>
  </header>

  <main>
    <div class="section">
      <h2>Section 1</h2>
      <p>This is a demonstration of sticky header and fixed footer layout. The header above will remain at the top of the viewport as you scroll down through the content. The footer at the bottom will always stay visible.</p>
    </div>

    <div class="section">
      <h2>Section 2</h2>
      <p>Lorem ipsum dolor sit amet, consectetur adipiscing elit. Sed do eiusmod tempor incididunt ut labore et dolore magna aliqua. Ut enim ad minim veniam, quis nostrud exercitation ullamco laboris.</p>
    </div>

    <div class="section">
      <h2>Section 3</h2>
      <p>Duis aute irure dolor in reprehenderit in voluptate velit esse cillum dolore eu fugiat nulla pariatur. Excepteur sint occaecat cupidatat non proident.</p>
    </div>

    <div class="section">
      <h2>Section 4</h2>
      <p>Sed ut perspiciatis unde omnis iste natus error sit voluptatem accusantium doloremque laudantium, totam rem aperiam, eaque ipsa quae ab illo inventore veritatis.</p>
    </div>

    <div class="section">
      <h2>Section 5</h2>
      <p>Nemo enim ipsam voluptatem quia voluptas sit aspernatur aut odit aut fugit, sed quia consequuntur magni dolores eos qui ratione voluptatem sequi nesciunt.</p>
    </div>

    <div class="section">
      <h2>Section 6</h2>
      <p>At vero eos et accusamus et iusto odio dignissimos ducimus qui blanditiis praesentium voluptatum deleniti atque corrupti quos dolores et quas molestias excepturi.</p>
    </div>
  </main>

  <footer>
    <p>Fixed Footer - Always visible at the bottom of the viewport</p>
  </footer>
</body>
</html>
```

</details>

---

### Task 4: Overlay Modal Using Absolute Positioning and Z-Index

Create a modal (popup) overlay that appears on top of the page content. Include an overlay background and a centered modal box.

**Requirements:**
- Use a semi-transparent overlay that covers the entire viewport.
- Center the modal box using absolute positioning.
- Use `z-index` to ensure the modal appears above all other content.
- Include a close button in the modal.
- Use JavaScript to toggle the modal visibility.

<details>
<summary>Solution</summary>

```html
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>Modal Overlay</title>
  <style>
    * {
      box-sizing: border-box;
      margin: 0;
      padding: 0;
    }

    body {
      font-family: Arial, sans-serif;
      padding: 40px;
      background-color: #fafafa;
    }

    h1 {
      margin-bottom: 20px;
    }

    p {
      margin-bottom: 15px;
      line-height: 1.6;
    }

    .open-btn {
      padding: 12px 24px;
      background-color: #1976d2;
      color: white;
      border: none;
      border-radius: 4px;
      font-size: 1rem;
      cursor: pointer;
    }

    .open-btn:hover {
      background-color: #1565c0;
    }

    /* Overlay */
    .overlay {
      display: none;
      position: fixed;
      top: 0;
      left: 0;
      width: 100%;
      height: 100%;
      background-color: rgba(0, 0, 0, 0.6);
      z-index: 1000;
    }

    /* Modal Box */
    .modal {
      position: absolute;
      top: 50%;
      left: 50%;
      transform: translate(-50%, -50%);
      background-color: white;
      width: 90%;
      max-width: 500px;
      padding: 30px;
      border-radius: 12px;
      box-shadow: 0 10px 30px rgba(0, 0, 0, 0.3);
      z-index: 1001;
    }

    .modal h2 {
      margin-bottom: 15px;
      color: #333;
    }

    .modal p {
      color: #666;
    }

    .close-btn {
      position: absolute;
      top: 10px;
      right: 15px;
      background: none;
      border: none;
      font-size: 1.5rem;
      cursor: pointer;
      color: #999;
    }

    .close-btn:hover {
      color: #333;
    }

    .modal-footer {
      margin-top: 20px;
      text-align: right;
    }

    .modal-footer button {
      padding: 10px 20px;
      background-color: #1976d2;
      color: white;
      border: none;
      border-radius: 4px;
      cursor: pointer;
    }

    .modal-footer button:hover {
      background-color: #1565c0;
    }

    /* Show state */
    .overlay.active {
      display: block;
    }
  </style>
</head>
<body>
  <h1>Modal Overlay Demo</h1>
  <p>This page demonstrates how to create a modal overlay using absolute positioning and z-index. Click the button below to open the modal.</p>
  <button class="open-btn" onclick="openModal()">Open Modal</button>

  <!-- Overlay + Modal -->
  <div class="overlay" id="overlay">
    <div class="modal">
      <button class="close-btn" onclick="closeModal()">&times;</button>
      <h2>Modal Title</h2>
      <p>This modal is positioned using <code>position: absolute</code> with <code>top: 50%</code>, <code>left: 50%</code>, and <code>transform: translate(-50%, -50%)</code> to center it on the screen.</p>
      <p>The dark overlay behind it uses <code>position: fixed</code> with <code>z-index: 1000</code> to cover the entire viewport.</p>
      <div class="modal-footer">
        <button onclick="closeModal()">Got It</button>
      </div>
    </div>
  </div>

  <script>
    function openModal() {
      document.getElementById('overlay').classList.add('active');
    }

    function closeModal() {
      document.getElementById('overlay').classList.remove('active');
    }

    // Close modal when clicking outside
    document.getElementById('overlay').addEventListener('click', function(e) {
      if (e.target === this) {
        closeModal();
      }
    });
  </script>
</body>
</html>
```

</details>

---

### Task 5: Complete Page Layout Using Display and Positioning Properties

Build a complete single-page layout that combines multiple display and positioning techniques.

**Requirements:**
- A fixed navigation bar at the top.
- A hero section with a centered heading (use absolute positioning).
- A three-column content section using `inline-block`.
- A "Back to Top" button using `position: fixed` in the bottom-right corner.
- A standard footer at the bottom.
- Use proper `z-index` layering throughout.

<details>
<summary>Solution</summary>

```html
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>Complete Page Layout</title>
  <style>
    * {
      box-sizing: border-box;
      margin: 0;
      padding: 0;
    }

    body {
      font-family: Arial, sans-serif;
      color: #333;
    }

    /* Fixed Navbar */
    .navbar {
      position: fixed;
      top: 0;
      left: 0;
      width: 100%;
      background-color: #1a237e;
      color: white;
      padding: 15px 30px;
      z-index: 1000;
      display: flex;
      justify-content: space-between;
      align-items: center;
      box-shadow: 0 2px 8px rgba(0, 0, 0, 0.3);
    }

    .navbar .logo {
      font-size: 1.5rem;
      font-weight: bold;
    }

    .navbar .nav-links a {
      color: white;
      text-decoration: none;
      margin-left: 20px;
      font-size: 1rem;
    }

    .navbar .nav-links a:hover {
      text-decoration: underline;
    }

    /* Hero Section */
    .hero {
      position: relative;
      width: 100%;
      height: 400px;
      background-color: #283593;
      margin-top: 55px; /* Offset for fixed navbar */
      overflow: hidden;
    }

    .hero-content {
      position: absolute;
      top: 50%;
      left: 50%;
      transform: translate(-50%, -50%);
      text-align: center;
      color: white;
      z-index: 1;
    }

    .hero-content h1 {
      font-size: 2.5rem;
      margin-bottom: 15px;
    }

    .hero-content p {
      font-size: 1.2rem;
      opacity: 0.9;
    }

    /* Three Column Section */
    .columns-section {
      max-width: 1100px;
      margin: 40px auto;
      padding: 0 20px;
      text-align: center;
    }

    .columns-section h2 {
      font-size: 2rem;
      margin-bottom: 30px;
      color: #1a237e;
    }

    .column {
      display: inline-block;
      width: 30%;
      vertical-align: top;
      margin: 0 1.5%;
      padding: 25px;
      background-color: #f5f5f5;
      border-radius: 8px;
      text-align: left;
      border-top: 4px solid #1a237e;
    }

    .column h3 {
      margin-bottom: 15px;
      color: #1a237e;
    }

    .column p {
      line-height: 1.7;
      color: #555;
    }

    /* Extra Content for Scrolling */
    .content-section {
      max-width: 800px;
      margin: 40px auto;
      padding: 30px 20px;
    }

    .content-section h2 {
      font-size: 1.8rem;
      margin-bottom: 20px;
      color: #1a237e;
    }

    .content-section p {
      line-height: 1.8;
      margin-bottom: 15px;
    }

    /* Back to Top Button */
    .back-to-top {
      position: fixed;
      bottom: 30px;
      right: 30px;
      width: 50px;
      height: 50px;
      background-color: #1a237e;
      color: white;
      border: none;
      border-radius: 50%;
      font-size: 1.5rem;
      cursor: pointer;
      z-index: 999;
      box-shadow: 0 2px 10px rgba(0, 0, 0, 0.3);
      display: flex;
      align-items: center;
      justify-content: center;
      text-decoration: none;
    }

    .back-to-top:hover {
      background-color: #283593;
    }

    /* Footer */
    footer {
      background-color: #212121;
      color: #bbb;
      text-align: center;
      padding: 30px;
      margin-top: 40px;
    }

    footer p {
      margin-bottom: 5px;
    }
  </style>
</head>
<body id="top">

  <!-- Fixed Navbar -->
  <nav class="navbar">
    <div class="logo">MyWebsite</div>
    <div class="nav-links">
      <a href="#top">Home</a>
      <a href="#features">Features</a>
      <a href="#about">About</a>
      <a href="#contact">Contact</a>
    </div>
  </nav>

  <!-- Hero Section -->
  <section class="hero">
    <div class="hero-content">
      <h1>Welcome to Our Website</h1>
      <p>A complete page layout using CSS display and positioning properties</p>
    </div>
  </section>

  <!-- Three Column Section -->
  <section class="columns-section" id="features">
    <h2>Our Features</h2>
    <div class="column">
      <h3>Feature One</h3>
      <p>This column uses display: inline-block to sit side by side with other columns. Each column has padding, border-top, and consistent spacing.</p>
    </div>
    <div class="column">
      <h3>Feature Two</h3>
      <p>The inline-block display allows these elements to respect width and height while flowing horizontally, unlike pure inline elements.</p>
    </div>
    <div class="column">
      <h3>Feature Three</h3>
      <p>Vertical alignment is handled with vertical-align: top to ensure all columns start from the same baseline regardless of content height.</p>
    </div>
  </section>

  <!-- Additional Content -->
  <section class="content-section" id="about">
    <h2>About This Layout</h2>
    <p>This layout demonstrates several CSS positioning and display techniques working together. The navigation bar uses position: fixed to stay at the top of the viewport at all times. The hero section uses position: relative as a container, with the heading centered using position: absolute and transform.</p>
    <p>The three-column section uses display: inline-block to arrange content horizontally without flexbox or grid. The "Back to Top" button in the bottom-right corner uses position: fixed to remain accessible no matter how far the user scrolls.</p>
    <p>Proper z-index layering ensures the navbar (z-index: 1000) always stays above the hero content (z-index: 1) and the back-to-top button (z-index: 999).</p>
  </section>

  <section class="content-section" id="contact">
    <h2>Contact Us</h2>
    <p>This section adds more content to make the page scrollable, allowing you to test the fixed navbar and the back-to-top button behavior during scrolling.</p>
    <p>Try scrolling up and down to see how the fixed elements remain in place while the rest of the content scrolls normally beneath them.</p>
  </section>

  <!-- Back to Top Button -->
  <a href="#top" class="back-to-top" title="Back to Top">&#8679;</a>

  <!-- Footer -->
  <footer>
    <p>CSS Box Model & Layout - Week 6 Practice</p>
    <p>MERN Stack Full Course</p>
  </footer>

</body>
</html>
```

</details>

---

**End of Practice Questions - Week 6: CSS Box Model & Layout**
