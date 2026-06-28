# Week 6: CSS Box Model & Layout

> **Prerequisites:** CSS basics from Week 5 (selectors, properties, colors, typography).
>
> **Goal:** Master the CSS Box Model, understand how elements are sized and positioned, and learn the foundational layout mechanisms that every web developer must know.

---

## Table of Contents

1. [The CSS Box Model](#1-the-css-box-model)
   - [Box Model Diagram](#box-model-diagram)
   - [Real-Life Analogy](#real-life-analogy)
   - [Content](#content)
   - [Padding](#padding)
   - [Border](#border)
   - [Margin](#margin)
   - [box-sizing: content-box vs border-box](#box-sizing-content-box-vs-border-box)
   - [Outline vs Border](#outline-vs-border)
2. [CSS Display Property](#2-css-display-property)
   - [block](#block)
   - [inline](#inline)
   - [inline-block](#inline-block)
   - [none](#none)
   - [Comparison Table](#comparison-table)
   - [display: none vs visibility: hidden](#display-none-vs-visibility-hidden)
3. [CSS Positioning](#3-css-positioning)
   - [static](#static-default)
   - [relative](#relative)
   - [absolute](#absolute)
   - [fixed](#fixed)
   - [sticky](#sticky)
   - [z-index](#z-index--stacking-order)
4. [CSS Float and Clear](#4-css-float-and-clear)
5. [CSS Overflow](#5-css-overflow)
6. [CSS Width and Height](#6-css-width-and-height)
7. [Summary](#7-summary)

---

## 1. The CSS Box Model

The CSS Box Model is arguably **the single most important concept in CSS**. Every HTML element on a webpage is treated as a rectangular box, and the Box Model defines how that box is structured, sized, and spaced.

If you understand the Box Model deeply, layout and spacing problems become straightforward. If you do not, CSS will feel unpredictable and frustrating.

### Box Model Diagram

Every element in CSS is composed of four layers, from inside to outside:

```
+------------------------------------------------------+
|                      MARGIN                          |
|   +----------------------------------------------+   |
|   |                  BORDER                      |   |
|   |   +--------------------------------------+   |   |
|   |   |              PADDING                 |   |   |
|   |   |   +------------------------------+   |   |   |
|   |   |   |                              |   |   |   |
|   |   |   |           CONTENT            |   |   |   |
|   |   |   |                              |   |   |   |
|   |   |   |     (width x height)         |   |   |   |
|   |   |   |                              |   |   |   |
|   |   |   +------------------------------+   |   |   |
|   |   |              PADDING                 |   |   |
|   |   +--------------------------------------+   |   |
|   |                  BORDER                      |   |
|   +----------------------------------------------+   |
|                      MARGIN                          |
+------------------------------------------------------+
```

### Real-Life Analogy

Think of the Box Model like a **framed picture hanging on a wall**:

| Box Model Layer | Picture Frame Analogy       | Description                            |
| --------------- | --------------------------- | -------------------------------------- |
| **Content**     | The photograph itself       | The actual image or artwork            |
| **Padding**     | The matting (white border)  | Space between the photo and the frame  |
| **Border**      | The wooden/metal frame      | The visible frame around the matting   |
| **Margin**      | Wall space between pictures | Empty space separating one frame from another |

```
    Wall (the webpage)
    |                                              |
    |    [  Margin (wall space)  ]                  |
    |    +========================+                 |
    |    ||      Border (frame)  ||                 |
    |    ||  +----------------+  ||                 |
    |    ||  | Padding (mat)  |  ||                 |
    |    ||  |  +----------+  |  ||                 |
    |    ||  |  |  Content |  |  ||                 |
    |    ||  |  |  (photo) |  |  ||                 |
    |    ||  |  +----------+  |  ||                 |
    |    ||  |                |  ||                 |
    |    ||  +----------------+  ||                 |
    |    ||                      ||                 |
    |    +========================+                 |
    |    [  Margin (wall space)  ]                  |
    |                                              |
```

---

### Content

The **content area** holds the actual text, images, or child elements. Its size is controlled by the `width` and `height` properties.

```css
.box {
  width: 300px;
  height: 200px;
}
```

- `width` sets the horizontal size of the content area.
- `height` sets the vertical size of the content area.
- By default (with `content-box`), `width` and `height` apply **only** to the content, not including padding or border.

---

### Padding

**Padding** is the transparent space between the content and the border. It pushes the content inward, giving it breathing room. Padding takes on the background color of the element.

**Individual sides:**

```css
.box {
  padding-top: 20px;
  padding-right: 15px;
  padding-bottom: 20px;
  padding-left: 15px;
}
```

**Shorthand notation:**

```css
/* All four sides */
padding: 20px;                    /* top=20, right=20, bottom=20, left=20 */

/* Vertical | Horizontal */
padding: 20px 15px;               /* top=20, right=15, bottom=20, left=15 */

/* Top | Horizontal | Bottom */
padding: 10px 15px 20px;          /* top=10, right=15, bottom=20, left=15 */

/* Top | Right | Bottom | Left (clockwise) */
padding: 10px 15px 20px 25px;     /* top=10, right=15, bottom=20, left=25 */
```

> **Memory trick:** The shorthand goes **clockwise** starting from the top: **T**op, **R**ight, **B**ottom, **L**eft -- think **TR**ou**BL**e.

**Real-life example:** Padding is like the empty space inside a shipping box between the product and the cardboard walls. Without padding, the product (content) is pressed right against the edges.

---

### Border

The **border** wraps around the padding and content. It is the visible edge of the element.

**Individual properties:**

```css
.box {
  border-width: 2px;
  border-style: solid;
  border-color: #333333;
}
```

**Border styles available:**

| Style      | Appearance                        |
| ---------- | --------------------------------- |
| `none`     | No border                         |
| `solid`    | A single solid line               |
| `dashed`   | A series of dashes                |
| `dotted`   | A series of dots                  |
| `double`   | Two solid lines                   |
| `groove`   | Appears carved into the page      |
| `ridge`    | Appears raised from the page      |
| `inset`    | Appears pressed into the page     |
| `outset`   | Appears popping out of the page   |

**Shorthand:**

```css
/* width | style | color */
border: 2px solid #333333;
```

**Individual side borders:**

```css
border-top: 3px solid red;
border-right: 1px dashed blue;
border-bottom: 3px solid red;
border-left: 1px dashed blue;
```

**Border radius (rounded corners):**

```css
/* All corners */
border-radius: 10px;

/* Top-left | Top-right | Bottom-right | Bottom-left */
border-radius: 10px 20px 10px 20px;

/* Perfect circle (if element is square) */
border-radius: 50%;
```

```
  Sharp corners              Rounded corners            Circle
  +-----------+              /'-----------'\            /'''''''\
  |           |             |               |          |         |
  |           |             |               |          |         |
  |           |             |               |          |         |
  +-----------+              \.-----------./            \......./
  border-radius: 0       border-radius: 10px      border-radius: 50%
```

---

### Margin

**Margin** is the transparent space **outside** the border. It creates distance between the element and its neighbors. Unlike padding, margin does **not** take the element's background color.

**Individual sides:**

```css
.box {
  margin-top: 20px;
  margin-right: 15px;
  margin-bottom: 20px;
  margin-left: 15px;
}
```

**Shorthand (same clockwise pattern as padding):**

```css
margin: 20px;                     /* All sides */
margin: 20px 15px;                /* Vertical | Horizontal */
margin: 10px 15px 20px;           /* Top | Horizontal | Bottom */
margin: 10px 15px 20px 25px;      /* Top | Right | Bottom | Left */
```

**Centering with `auto`:**

One of the most common uses of margin is **horizontally centering** a block element:

```css
.container {
  width: 800px;
  margin: 0 auto;    /* 0 on top/bottom, auto on left/right */
}
```

`auto` tells the browser to split the remaining horizontal space equally between the left and right margins, centering the element.

```
  |<--- browser window width (e.g., 1200px) --->|
  |                                              |
  |  [auto margin]  +----------+  [auto margin]  |
  |    (200px)      | 800px    |    (200px)      |
  |                 | content  |                 |
  |                 +----------+                 |
```

**Margin Collapse:**

This is one of CSS's most surprising behaviors. When two **vertical** margins meet (top margin of one element and bottom margin of the element above it), they do not add together. Instead, **only the larger margin is used**.

```css
.heading {
  margin-bottom: 30px;
}
.paragraph {
  margin-top: 20px;
}
```

You might expect 50px of space between them. But the actual space is **30px** (the larger of the two).

```
  +------------------+
  |     Heading      |
  +------------------+
        margin-bottom: 30px
                                 ---> Collapsed margin = 30px (NOT 50px)
        margin-top: 20px
  +------------------+
  |    Paragraph     |
  +------------------+
```

**Key rules of margin collapse:**
- Only **vertical** margins collapse (top/bottom), never horizontal (left/right).
- Margins collapse between **adjacent siblings** and between **parent and first/last child** (if no padding or border separates them).
- **Negative margins** follow special rules: the most negative is used if both are negative; if one is positive and one is negative, they are added together.

**Real-life example:** Margin is like the personal space between people standing in a line. If person A wants 3 feet of space and person B wants 2 feet, they do not need 5 feet between them -- 3 feet satisfies both. That is margin collapse.

---

### box-sizing: content-box vs border-box

This property changes **what `width` and `height` actually measure**.

#### content-box (default)

With `content-box`, `width` and `height` apply only to the content. Padding and border are **added on top**.

```css
.box {
  box-sizing: content-box;   /* default */
  width: 300px;
  padding: 20px;
  border: 5px solid black;
}
```

```
  Total visible width = width + padding-left + padding-right + border-left + border-right
                      = 300   + 20           + 20            + 5           + 5
                      = 350px

  +---------------------------------------------------+  350px total
  | 5px border                                        |
  |  +---------------------------------------------+  |
  |  | 20px padding                                |  |
  |  |  +---------------------------------------+  |  |
  |  |  |          300px content                |  |  |
  |  |  +---------------------------------------+  |  |
  |  |                                             |  |
  |  +---------------------------------------------+  |
  |                                                   |
  +---------------------------------------------------+
```

**The problem:** You set `width: 300px`, but the element actually takes up 350px on screen. This makes layouts unpredictable.

#### border-box (recommended)

With `border-box`, `width` and `height` include the content, padding, **and** border. The content area shrinks to accommodate padding and border.

```css
.box {
  box-sizing: border-box;
  width: 300px;
  padding: 20px;
  border: 5px solid black;
}
```

```
  Total visible width = 300px (exactly what you set!)

  +---------------------------------------------------+  300px total
  | 5px border                                        |
  |  +---------------------------------------------+  |
  |  | 20px padding                                |  |
  |  |  +---------------------------------------+  |  |
  |  |  |          250px content                |  |  |
  |  |  |   (300 - 20 - 20 - 5 - 5 = 250)      |  |  |
  |  |  +---------------------------------------+  |  |
  |  |                                             |  |
  |  +---------------------------------------------+  |
  |                                                   |
  +---------------------------------------------------+
```

**Why `border-box` is better:** When you say `width: 300px`, the box is exactly 300px wide. No surprises. This is how most humans think about sizing.

**Best practice -- apply `border-box` globally:**

```css
*, *::before, *::after {
  box-sizing: border-box;
}
```

This is included in virtually every modern CSS reset or framework and is considered an industry standard.

---

### Outline vs Border

`outline` and `border` look similar but behave very differently.

| Feature              | Border                          | Outline                            |
| -------------------- | ------------------------------- | ---------------------------------- |
| Part of Box Model?   | Yes -- affects element size     | No -- does not affect size         |
| Can be per-side?     | Yes (`border-top`, etc.)        | No -- always all four sides        |
| Can have radius?     | Yes (`border-radius`)           | Limited (`outline-offset`)         |
| Affects layout?      | Yes -- pushes other elements    | No -- drawn on top of everything   |
| Common use           | Visual design                   | Focus indicators (accessibility)   |

```css
/* Border adds to the element's size */
.card {
  border: 2px solid blue;
}

/* Outline does NOT add to size -- it floats on top */
.card:focus {
  outline: 3px solid orange;
  outline-offset: 4px;      /* space between border and outline */
}
```

```
  With border:                    With outline:
  +-----------+  <-- border       +-----------+  <-- outline (no size change)
  |           |  element is       |           |  element stays
  |           |  bigger           |           |  same size
  +-----------+                   +-----------+
  Total width = content           Total width = content
              + border                        (outline ignored)
```

> **Important:** Never remove `outline` on focusable elements without providing an alternative focus style. The outline is critical for keyboard navigation and accessibility.

---

## 2. CSS Display Property

The `display` property controls **how an element participates in the layout flow**. It determines whether an element behaves as a block, inline, or something else entirely.

### block

Block-level elements:
- Take up the **full width** available (stretch to fill their parent).
- Always start on a **new line**.
- Respect `width`, `height`, `margin`, and `padding` on all sides.

**Default block elements:** `<div>`, `<p>`, `<h1>`-`<h6>`, `<section>`, `<article>`, `<header>`, `<footer>`, `<ul>`, `<ol>`, `<li>`, `<form>`

```css
.block-example {
  display: block;
  width: 200px;
  height: 50px;
  background: lightblue;
}
```

```
  |<----------- parent width (100%) ----------->|
  +----------------------------------------------+
  |              Block Element 1                 |
  +----------------------------------------------+
  +----------------------------------------------+
  |              Block Element 2                 |
  +----------------------------------------------+
  +----------------------------------------------+
  |              Block Element 3                 |
  +----------------------------------------------+

  Each block takes the full row (even if its content is short).
```

---

### inline

Inline elements:
- Take up **only as much width** as their content needs.
- Do **not** start on a new line -- they sit side by side.
- **Cannot** have `width` or `height` set (those properties are ignored).
- Vertical `margin` and `padding` do not push other elements away.

**Default inline elements:** `<span>`, `<a>`, `<strong>`, `<em>`, `<img>` (special case), `<code>`, `<br>`

```css
.inline-example {
  display: inline;
  background: lightyellow;
  /* width: 200px;   <-- This would be IGNORED */
  /* height: 50px;   <-- This would be IGNORED */
}
```

```
  |<----------- parent width ----------->|
  | [Inline A] [Inline B] [Inline C]     |
  |  ^-- they flow left to right,        |
  |      wrapping like words in text      |
```

---

### inline-block

`inline-block` is a hybrid. The element:
- Flows **inline** (sits side by side with other elements, does not force a new line).
- But **respects** `width`, `height`, `margin`, and `padding` like a block element.

This is extremely useful for things like navigation links or button groups.

```css
.nav-item {
  display: inline-block;
  width: 120px;
  height: 40px;
  background: lightgreen;
  text-align: center;
  line-height: 40px;
}
```

```
  |<-------------- parent width -------------->|
  | +--------+ +--------+ +--------+          |
  | | Item 1 | | Item 2 | | Item 3 |          |
  | +--------+ +--------+ +--------+          |
  |                                            |
  |  Inline flow (side by side)                |
  |  but each item has a defined width/height  |
```

---

### none

`display: none` **completely removes** the element from the document flow. It is as if the element does not exist at all. It takes up no space, and other elements fill in where it would have been.

```css
.hidden {
  display: none;    /* Element is removed from layout entirely */
}
```

---

### Comparison Table

| Feature                     | `block`         | `inline`        | `inline-block`  |
| --------------------------- | --------------- | --------------- | --------------- |
| Starts on new line?         | Yes             | No              | No              |
| Takes full width?           | Yes             | No              | No              |
| Respects width/height?      | Yes             | No              | Yes             |
| Respects vertical margin?   | Yes             | No              | Yes             |
| Respects horizontal margin? | Yes             | Yes             | Yes             |
| Respects padding?           | Yes             | Partially       | Yes             |

**Visual comparison:**

```
  BLOCK:
  +----------------------------------------------+
  |                   DIV 1                      |
  +----------------------------------------------+
  +----------------------------------------------+
  |                   DIV 2                      |
  +----------------------------------------------+

  INLINE:
  [span1] [span2] [span3] [span4] [span5]

  INLINE-BLOCK:
  +--------+ +--------+ +--------+
  | Box 1  | | Box 2  | | Box 3  |
  |        | |        | |        |
  +--------+ +--------+ +--------+
```

---

### display: none vs visibility: hidden

These two properties both "hide" elements, but they behave very differently.

| Feature                  | `display: none`          | `visibility: hidden`     |
| ------------------------ | ------------------------ | ------------------------ |
| Element visible?         | No                       | No                       |
| Takes up space?          | No (removed from flow)   | Yes (space is preserved) |
| Affects layout?          | No                       | Yes                      |
| Accessible to screen readers? | No                 | Depends on context       |

```css
/* Element is completely gone from the layout */
.gone {
  display: none;
}

/* Element is invisible but still occupies space */
.invisible {
  visibility: hidden;
}
```

```
  display: none                    visibility: hidden
  +-------+ +-------+             +-------+ +-------+
  | Box 1 | | Box 3 |             | Box 1 | |       |  <-- empty space
  +-------+ +-------+             +-------+ +-------+
  (Box 2 is gone,                 (Box 2 is invisible,
   Box 3 moves up)                 but space remains)
                                              +-------+
                                              | Box 3 |
                                              +-------+
```

**Real-life example:** `display: none` is like removing a chair from a row of seats -- everyone shifts over. `visibility: hidden` is like draping an invisible cloak over the chair -- the chair is still there taking up space, you just cannot see it.

---

## 3. CSS Positioning

The `position` property controls **how an element is placed** on the page. It works together with the offset properties: `top`, `right`, `bottom`, and `left`.

### static (default)

Every element is `position: static` by default. Static elements:
- Follow the **normal document flow**.
- Are **not affected** by `top`, `right`, `bottom`, `left`, or `z-index`.

```css
.box {
  position: static;    /* default -- no need to write this */
}
```

```
  Normal document flow:
  +----------------------------------------------+
  |                  Element 1                   |
  +----------------------------------------------+
  +----------------------------------------------+
  |                  Element 2                   |
  +----------------------------------------------+
  +----------------------------------------------+
  |                  Element 3                   |
  +----------------------------------------------+
  (Elements stack top to bottom in order)
```

---

### relative

A relatively positioned element is placed according to the normal flow **first**, and then **offset** from that position. The original space it occupied is **preserved** -- other elements do not move to fill the gap.

```css
.box {
  position: relative;
  top: 20px;       /* moves DOWN 20px from original position */
  left: 30px;      /* moves RIGHT 30px from original position */
}
```

```
  Before:                          After (position: relative; top: 20px; left: 30px;)
  +----------+                     +----------+  <-- original space preserved (ghost)
  | Element  |                     |  (empty) |
  +----------+                     +----------+
                                        \
                                    30px  \  20px down
                                           \
                                        +----------+
                                        | Element  |  <-- visually shifted
                                        +----------+
```

**Real-life example:** Imagine a student sitting in their assigned seat in a classroom. With `position: relative`, the student slides their chair 20cm back and 30cm to the right, but their assigned seat (the original space) is still reserved -- no one else can sit there.

---

### absolute

An absolutely positioned element is **removed from the normal flow** (it does not take up space). It is positioned relative to its **nearest positioned ancestor** (any ancestor with `position` set to anything other than `static`). If no positioned ancestor exists, it is positioned relative to the `<html>` element (the page itself).

```css
.parent {
  position: relative;     /* This makes parent the reference point */
  width: 400px;
  height: 300px;
}

.child {
  position: absolute;
  top: 10px;              /* 10px from parent's top edge */
  right: 10px;            /* 10px from parent's right edge */
  width: 100px;
  height: 50px;
}
```

```
  +------------------------------------------+
  |  .parent (position: relative)            |
  |                                          |
  |                            +---------+   |
  |                            | .child  |   |
  |                            | (abs)   |   |
  |                            +---------+   |
  |                              ^  10px from top
  |                              |  10px from right
  |                                          |
  |                                          |
  +------------------------------------------+
```

**Real-life example:** Think of a bulletin board (the parent). You can pin a note (the child) anywhere on the board. The note does not push other notes around -- it sits on top at the exact coordinates you choose.

---

### fixed

A fixed element is **removed from the normal flow** and positioned relative to the **browser viewport** (the visible screen). It **does not move when the page scrolls**.

```css
.navbar {
  position: fixed;
  top: 0;
  left: 0;
  width: 100%;
  height: 60px;
  background: white;
  z-index: 1000;
}
```

```
  +================================+
  | FIXED NAVBAR (always visible)  |  <-- stays here even when scrolling
  +================================+
  |                                |
  |   Page content scrolls         |
  |   behind the navbar            |
  |                                |
  |   . . . . . . . . . . . .     |
  |                                |
  +================================+
       (viewport bottom)
```

**Common uses:** Navigation bars, "back to top" buttons, cookie consent banners, floating chat widgets.

**Real-life example:** A fixed element is like a sticker on your car windshield. As you drive (scroll), the scenery behind it changes, but the sticker stays in the same spot on the glass.

---

### sticky

Sticky positioning is a **hybrid** of relative and fixed. The element behaves as `relative` until it reaches a specified scroll threshold, at which point it becomes `fixed` (sticks in place).

```css
.section-header {
  position: sticky;
  top: 0;              /* sticks when it reaches the top of the viewport */
  background: white;
  padding: 10px;
}
```

```
  BEFORE scrolling to it:           AFTER scrolling past it:
  +==========================+      +==========================+
  |  Viewport                |      | .section-header (STUCK)  |  <-- now fixed
  |                          |      +==========================+
  |  Other content above     |      |                          |
  |                          |      |  Section content scrolls |
  +--------------------------+      |  underneath              |
  | .section-header          |      |                          |
  +--------------------------+      |                          |
  |  Section content         |      +==========================+
  |                          |
```

**Common uses:** Table headers that stay visible while scrolling, section titles, sidebar navigation.

**Real-life example:** Sticky positioning works like a magnet on a refrigerator. You can slide a note up the fridge (scroll), and when it reaches the top edge, the magnet holds it there. It stays put while everything else continues to scroll underneath.

> **Important:** A sticky element only works within its **parent container**. Once the parent scrolls out of view, the sticky element scrolls away with it.

---

### z-index -- Stacking Order

When elements overlap (due to positioning), `z-index` controls **which element appears on top**. Higher values are closer to the viewer.

- `z-index` only works on **positioned elements** (anything except `position: static`).
- Elements with higher `z-index` values appear **in front of** elements with lower values.
- Default `z-index` is `auto` (effectively 0).

```css
.card-1 {
  position: relative;
  z-index: 1;
}
.card-2 {
  position: relative;
  z-index: 2;        /* This appears on top of card-1 */
}
.modal {
  position: fixed;
  z-index: 1000;     /* This appears on top of everything */
}
```

```
  Viewer's eye
      |
      |     z-index: 1000  (modal overlay)
      |     +==========================+
      |     |                          |
      |     z-index: 2  (card-2)
      |     +------------------+
      |     |                  |
      |     z-index: 1  (card-1)
      |     +-----------+
      |     |           |
      v     z-index: 0  (default page content)
      +----------------------------------------------+
      |                                              |
      |            Background / Page                 |
      +----------------------------------------------+

  Think of it as layers stacked toward the viewer:

  [  Page Content  ]    z-index: 0   (back)
  [    Card 1      ]    z-index: 1
  [    Card 2      ]    z-index: 2
  [  Modal Overlay ]    z-index: 1000 (front)
```

**Practical z-index scale (a common convention):**

| Layer              | z-index Range | Example                  |
| ------------------ | ------------- | ------------------------ |
| Background         | 0             | Default content          |
| Dropdown menus     | 100           | Navigation dropdowns     |
| Fixed elements     | 500           | Sticky headers           |
| Overlays/Backdrops | 900           | Dark overlay behind modal|
| Modals/Dialogs     | 1000          | Pop-up windows           |
| Tooltips           | 1100          | Hover information        |

> **Common mistake:** Do not just keep increasing z-index to 9999, 99999, etc. Use a planned scale so your stacking order remains maintainable.

---

## 4. CSS Float and Clear

**Float** was originally designed for wrapping text around images (like in a newspaper or magazine). For years, developers also used it for creating multi-column layouts, but it has largely been **replaced by Flexbox and Grid** for layout purposes.

### float: left and float: right

A floated element is taken out of the normal flow and pushed to the left or right side of its container. Surrounding inline content wraps around it.

```css
.image {
  float: left;
  margin-right: 15px;
  margin-bottom: 10px;
}
```

```
  float: left                         float: right
  +-------+  Text wraps around        Text wraps around  +-------+
  | Image |  the image on the         the image on the   | Image |
  |       |  right side. The text     left side. The     |       |
  +-------+  continues to flow        text continues     +-------+
  naturally below the image when       naturally below
  there is enough text to fill the     the image.
  available space.
```

### clear: both

The `clear` property prevents an element from wrapping alongside a floated element. It forces the element to move **below** any floats.

```css
.clear {
  clear: both;      /* Clears both left and right floats */
}
```

| Value   | Effect                                |
| ------- | ------------------------------------- |
| `left`  | Clears left floats only               |
| `right` | Clears right floats only              |
| `both`  | Clears both left and right floats     |
| `none`  | Default -- no clearing                |

### The Clearfix Hack

When all children of a container are floated, the parent container **collapses** to zero height because floated elements are removed from the normal flow. The "clearfix" hack forces the parent to contain its floated children.

```css
/* The classic clearfix */
.clearfix::after {
  content: "";
  display: table;
  clear: both;
}
```

```
  WITHOUT clearfix:                  WITH clearfix:
  +------------------------+        +------------------------+
  | .parent (height: 0!)   |        | .parent                |
  +------------------------+        |  +------+  +------+    |
  +------+  +------+                |  | left |  | right|    |
  | left |  | right|                |  +------+  +------+    |
  +------+  +------+                +------------------------+
  (floats overflow parent)           (parent wraps children)
```

### Why Float is Mostly Replaced

Float was designed for **text wrapping**, not layout. Using it for columns, grids, and page structure led to fragile code full of clearfix hacks and collapsing containers.

**Modern alternatives:**
- **Flexbox** (Week 7) -- one-dimensional layouts (rows or columns).
- **CSS Grid** (Week 7) -- two-dimensional layouts (rows and columns).

Today, use `float` only for its original purpose: **wrapping text around images**.

---

## 5. CSS Overflow

The `overflow` property controls what happens when an element's content is **larger than its box** (i.e., the content overflows the defined width/height).

### Overflow Values

| Value     | Behavior                                                        |
| --------- | --------------------------------------------------------------- |
| `visible` | Default. Content spills outside the box. No clipping.           |
| `hidden`  | Content that overflows is clipped and invisible.                |
| `scroll`  | Scrollbars are **always** shown, even if content fits.          |
| `auto`    | Scrollbars appear **only when needed** (content overflows).     |

```css
.container {
  width: 200px;
  height: 100px;
  border: 1px solid #ccc;
}

.visible-overflow  { overflow: visible; }
.hidden-overflow   { overflow: hidden;  }
.scroll-overflow   { overflow: scroll;  }
.auto-overflow     { overflow: auto;    }
```

```
  overflow: visible          overflow: hidden
  +-----------+              +-----------+
  | Content   |              | Content   |
  | that is   |              | that is   |
  +-----------+              +-----------+
  | too tall  |  <-- spills  (rest is clipped/invisible)
  | to fit    |      out
  |           |

  overflow: scroll           overflow: auto
  +-----------+|^|           +-----------+
  | Content   || |           | Content   |
  | that is   || |           | that is   |
  | too tall  ||=|           | too tall  ||^|  <-- scrollbar only
  +-----------+|v|           +-----------+|v|     if needed
  (scrollbar always)
```

### overflow-x and overflow-y

You can control horizontal and vertical overflow independently:

```css
.code-block {
  overflow-x: auto;      /* horizontal scroll if code is too wide */
  overflow-y: hidden;    /* clip any vertical overflow */
}
```

**Real-life example:** Think of `overflow` like a window in your house. `visible` means the curtains are open and items on the windowsill can stick out past the frame. `hidden` means anything past the window frame is cut off. `scroll` is like having adjustable blinds you can slide to reveal more. `auto` is like smart blinds that only appear when needed.

---

## 6. CSS Width and Height

### Basic Width and Height

```css
.box {
  width: 300px;       /* Fixed width */
  height: 200px;      /* Fixed height */
}
```

Width and height can use various units:

| Unit   | Description                          | Example          |
| ------ | ------------------------------------ | ---------------- |
| `px`   | Fixed pixels                         | `width: 300px`   |
| `%`    | Percentage of parent element         | `width: 50%`     |
| `vw`   | Percentage of viewport width         | `width: 100vw`   |
| `vh`   | Percentage of viewport height        | `height: 100vh`  |
| `em`   | Relative to element's font size      | `width: 20em`    |
| `rem`  | Relative to root font size           | `width: 20rem`   |
| `auto` | Browser calculates automatically     | `width: auto`    |

### max-width and min-width

These constrain the width within a range, which is essential for responsive design.

```css
.container {
  width: 80%;           /* Takes 80% of parent */
  max-width: 1200px;    /* But never wider than 1200px */
  min-width: 320px;     /* And never narrower than 320px */
}
```

```
  On a wide screen (1920px):
  |<----- 80% of 1920 = 1536px ----->|
  |<----- max-width caps at 1200px ------>|
  +====================================+
  |          Container: 1200px         |  <-- max-width wins
  +====================================+

  On a medium screen (1000px):
  |<----- 80% of 1000 = 800px ----->|
  +============================+
  |      Container: 800px      |  <-- 80% is within bounds
  +============================+

  On a small screen (300px):
  |<--- 80% of 300 = 240px --->|
  |<--- min-width: 320px ----->|
  +========================+
  |    Container: 320px    |  <-- min-width wins
  +========================+
```

### max-height and min-height

Same concept, but for vertical sizing:

```css
.card {
  min-height: 200px;     /* At least 200px tall */
  max-height: 500px;     /* At most 500px tall */
  overflow: auto;        /* Scroll if content exceeds max-height */
}
```

### The calc() Function

`calc()` lets you perform **math with mixed units**. This is incredibly useful when you need to combine different unit types.

```css
/* Full width minus a fixed sidebar */
.main-content {
  width: calc(100% - 250px);
}

/* Full viewport height minus a fixed header */
.page-body {
  height: calc(100vh - 60px);
}

/* Centering with offset */
.element {
  margin-left: calc(50% - 150px);
}

/* Combining multiple operations */
.complex {
  width: calc(100% - 2rem - 4px);
  padding: calc(1rem + 5px);
}
```

**Important `calc()` rules:**
- Spaces around `+` and `-` operators are **required**: `calc(100% - 20px)` works, `calc(100%-20px)` does not.
- `*` and `/` do not require spaces, but using them improves readability.
- You can nest `calc()` inside `calc()`, though it is rarely needed.
- You can mix any CSS units: `px`, `%`, `em`, `rem`, `vw`, `vh`, etc.

```
  Without calc():                    With calc():
  +-----------+   +-----------+      +----------------------------------+
  | Sidebar   |   | Main      |      |  width: calc(100% - 250px)      |
  | 250px     |   | ??? px    |      |  Always fills remaining space    |
  | (fixed)   |   | (guess?)  |      |  regardless of screen width      |
  +-----------+   +-----------+      +----------------------------------+
```

---

## 7. Summary

### Key Concepts at a Glance

| Concept           | What It Controls                                    | Most Important Takeaway                                 |
| ----------------- | --------------------------------------------------- | ------------------------------------------------------- |
| **Box Model**     | How elements are sized (content, padding, border, margin) | Always use `box-sizing: border-box`                |
| **Display**       | How elements flow in the document                   | `block` = full width, `inline` = content width only     |
| **Position**      | Where elements are placed                           | `relative` for nudging, `absolute` for precise placement|
| **Float**         | Wrapping text around elements                       | Use only for text wrapping; prefer Flexbox/Grid for layout |
| **Overflow**      | What happens when content exceeds the box           | `auto` is the safest choice for most cases              |
| **Width/Height**  | Sizing constraints                                  | Use `max-width` for responsive design + `calc()` for mixed-unit math |

### The Universal Reset You Should Always Use

```css
/* Apply border-box sizing to everything */
*, *::before, *::after {
  box-sizing: border-box;
}

/* Reset default margins and padding */
body {
  margin: 0;
  padding: 0;
}
```

### Quick Reference: Position Values

```
  static     -> Normal flow. No offset properties. The default.
  relative   -> Offset from its normal position. Original space preserved.
  absolute   -> Removed from flow. Positioned relative to nearest positioned ancestor.
  fixed      -> Removed from flow. Positioned relative to viewport. Stays on scroll.
  sticky     -> Relative until scroll threshold, then fixed.
```

### What is Next?

In **Week 7**, we will learn **CSS Flexbox and Grid** -- the modern, powerful layout systems that make creating responsive, complex layouts straightforward and predictable. The Box Model knowledge from this week is the foundation upon which Flexbox and Grid build.

---

> **Practice Tip:** Open your browser's Developer Tools (F12), select any element, and look at the "Box Model" diagram in the Computed tab. You will see the content, padding, border, and margin values visualized for that element. This is the fastest way to debug spacing and sizing issues.
