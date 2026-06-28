# Week 8 -- Responsive Design & CSS Animations

> **Prerequisites:** CSS Selectors, Box Model (Week 5-6), Flexbox & Grid (Week 7)
> **Goal:** Build websites that look great on every screen size and feel alive with smooth animations.

---

## Table of Contents

1. [What is Responsive Web Design?](#1-what-is-responsive-web-design)
2. [Media Queries](#2-media-queries)
3. [Responsive Units](#3-responsive-units)
4. [Responsive Images](#4-responsive-images)
5. [Responsive Typography](#5-responsive-typography)
6. [CSS Transitions](#6-css-transitions)
7. [CSS Animations with @keyframes](#7-css-animations-with-keyframes)
8. [CSS Transform](#8-css-transform)
9. [CSS Variables (Custom Properties)](#9-css-variables-custom-properties)
10. [Week 8 Project: Fully Responsive Portfolio Page](#10-week-8-project-fully-responsive-portfolio-page)
11. [Summary -- CSS Weeks 5-8 Recap](#11-summary--css-weeks-5-8-recap)

---

## 1. What is Responsive Web Design?

Responsive Web Design (RWD) is an approach where a website's layout **automatically adjusts** to fit the screen size of the device viewing it -- whether that device is a phone, tablet, laptop, or desktop monitor.

### Real-Life Analogy

Think of a newspaper. The same news content appears in a broadsheet paper, a tabloid, and a mobile news app -- but the **layout changes** to fit each format. The headlines, images, and articles rearrange themselves so the reader always has a comfortable experience.

Responsive design does the same thing for websites.

```
  SAME WEBSITE -- DIFFERENT SCREENS
  ==================================

  Desktop (1440px)          Tablet (768px)        Phone (375px)
  +------------------+     +--------------+      +--------+
  | [Logo]  Nav Nav  |     | [Logo]       |      | [Logo] |
  +------------------+     |  Nav  Nav    |      | [=]    |
  | Hero  Image      |     +--------------+      +--------+
  | Big Heading      |     | Hero Image   |      | Hero   |
  +--------+---------+     | Heading      |      | Image  |
  | Card   | Card    |     +------+-------+      +--------+
  | Card   | Card    |     | Card | Card  |      | Card 1 |
  +--------+---------+     +------+-------+      +--------+
  | Footer           |     | Card | Card  |      | Card 2 |
  +------------------+     +------+-------+      +--------+
                            | Footer      |      | Card 3 |
                            +--------------+      +--------+
                                                  | Footer |
                                                  +--------+
```

### Why Responsive Design Matters

- **Mobile traffic dominates.** Over 60% of global web traffic now comes from mobile devices. If your site does not work on a phone, you are losing the majority of your audience.
- **Google ranks mobile-friendly sites higher.** Since 2019, Google uses mobile-first indexing -- it looks at your mobile version first.
- **One codebase, all devices.** Instead of building separate websites for phone, tablet, and desktop, you build one site that adapts.
- **Better user experience.** No one likes pinching and zooming on a phone to read tiny text.

### The Viewport Meta Tag

Before writing any responsive CSS, you must include this tag in the `<head>` of every HTML page:

```html
<meta name="viewport" content="width=device-width, initial-scale=1.0">
```

**What it does:**

| Attribute              | Meaning                                          |
|------------------------|--------------------------------------------------|
| `width=device-width`   | Sets the page width to match the device's screen  |
| `initial-scale=1.0`    | Sets the initial zoom level to 100% (no zoom)     |

**Without this tag**, mobile browsers render the page at a desktop width (typically 980px) and then shrink it down, making everything tiny and unreadable.

```
  WITHOUT viewport tag          WITH viewport tag
  +--------------------+        +--------+
  |  Entire desktop    |        | Header |
  |  page shrunk to    |        +--------+
  |  fit phone screen  |        | Nice   |
  |  (tiny text!)      |        | sized  |
  |  Can't read this   |        | text   |
  +--------------------+        +--------+
```

---

## 2. Media Queries

Media queries are the **backbone** of responsive design. They let you apply CSS rules **only when certain conditions are true** -- most commonly, conditions about screen width.

### Basic Syntax

```css
@media (condition) {
  /* CSS rules that apply ONLY when the condition is true */
}
```

**Example:** Change background color on small screens:

```css
@media (max-width: 768px) {
  body {
    background-color: lightblue;
  }
}
```

This says: "When the screen width is **768px or less**, make the background light blue."

### Common Breakpoints

A **breakpoint** is the screen width at which your layout changes. Here are industry-standard breakpoints:

```
  Breakpoint Reference Chart
  ============================================================
  Device         Width Range       Common Breakpoint
  ------------------------------------------------------------
  Small Phone    320px - 480px     max-width: 480px
  Large Phone    481px - 767px     max-width: 767px
  Tablet         768px - 1024px    max-width: 1024px
  Laptop         1025px - 1440px   max-width: 1440px
  Desktop        1441px+           min-width: 1441px
  ============================================================
```

| Device       | Width Range      | Typical Breakpoint   |
|--------------|------------------|----------------------|
| Small Phone  | 320px -- 480px   | `max-width: 480px`   |
| Large Phone  | 481px -- 767px   | `max-width: 767px`   |
| Tablet       | 768px -- 1024px  | `max-width: 1024px`  |
| Laptop       | 1025px -- 1440px | `max-width: 1440px`  |
| Desktop      | 1441px+          | `min-width: 1441px`  |

> **Note:** These are guidelines, not strict rules. Always test your design and add breakpoints where your content actually breaks.

### Mobile-First vs Desktop-First

There are two strategies for writing responsive CSS:

**Mobile-First (Recommended)**
Write your base CSS for mobile, then use `min-width` media queries to add styles for larger screens.

```css
/* Base styles: mobile (default) */
.container {
  display: flex;
  flex-direction: column;     /* Stack vertically on mobile */
  padding: 10px;
}

/* Tablet and up */
@media (min-width: 768px) {
  .container {
    flex-direction: row;      /* Side by side on tablet */
    padding: 20px;
  }
}

/* Desktop and up */
@media (min-width: 1024px) {
  .container {
    max-width: 1200px;
    margin: 0 auto;           /* Center on desktop */
    padding: 40px;
  }
}
```

**Desktop-First**
Write your base CSS for desktop, then use `max-width` media queries to override styles for smaller screens.

```css
/* Base styles: desktop (default) */
.container {
  display: flex;
  flex-direction: row;
  max-width: 1200px;
  margin: 0 auto;
  padding: 40px;
}

/* Tablet and below */
@media (max-width: 1024px) {
  .container {
    padding: 20px;
  }
}

/* Mobile and below */
@media (max-width: 768px) {
  .container {
    flex-direction: column;
    padding: 10px;
  }
}
```

**Comparison:**

```
  Mobile-First (min-width)         Desktop-First (max-width)
  ===========================      ===========================
  Start: smallest screen           Start: largest screen
  Add complexity as you go UP      Remove features going DOWN
  Uses: @media (min-width: X)      Uses: @media (max-width: X)
  Industry standard                Legacy approach
  Better performance on mobile     Can be easier to visualize
```

> **Best Practice:** Use **mobile-first**. Since most users are on phones, your mobile styles load first with no media query overhead.

### min-width vs max-width

```
  min-width: 768px                 max-width: 768px
  ===========================      ===========================
  Applies at 768px AND ABOVE       Applies at 768px AND BELOW

       0px          768px                0px          768px
  -----[============|=====>        <====|============]-----
       NOT active   ACTIVE              ACTIVE       NOT active
```

- **`min-width: 768px`** -- "From 768px and wider" (mobile-first, building up)
- **`max-width: 768px`** -- "From 768px and narrower" (desktop-first, scaling down)

### Combining Conditions

You can combine multiple conditions using `and`, comma (acts as `or`), and `not`:

```css
/* AND -- both conditions must be true */
@media (min-width: 768px) and (max-width: 1024px) {
  /* Tablet only */
  .sidebar {
    width: 200px;
  }
}

/* OR (comma) -- either condition can be true */
@media (max-width: 480px), (orientation: landscape) {
  /* Small phone OR landscape mode */
  .hero {
    height: 50vh;
  }
}

/* NOT -- invert the condition */
@media not print {
  /* Everything except print */
  .no-print {
    display: block;
  }
}
```

### Practical Examples

**Example 1: Hide sidebar on mobile**

```css
.sidebar {
  width: 250px;
  display: block;
}

@media (max-width: 768px) {
  .sidebar {
    display: none;   /* Sidebar disappears on small screens */
  }
}
```

**Example 2: Stack columns on mobile**

```css
.grid {
  display: grid;
  grid-template-columns: repeat(3, 1fr);   /* 3 columns on desktop */
  gap: 20px;
}

@media (max-width: 1024px) {
  .grid {
    grid-template-columns: repeat(2, 1fr); /* 2 columns on tablet */
  }
}

@media (max-width: 600px) {
  .grid {
    grid-template-columns: 1fr;            /* 1 column on mobile */
  }
}
```

**Example 3: Change font sizes for readability**

```css
h1 {
  font-size: 1.8rem;   /* Mobile default */
}

@media (min-width: 768px) {
  h1 {
    font-size: 2.5rem;  /* Tablet */
  }
}

@media (min-width: 1024px) {
  h1 {
    font-size: 3.5rem;  /* Desktop */
  }
}
```

---

## 3. Responsive Units

Fixed units like `px` create rigid layouts. Responsive units let elements **scale proportionally** with the screen or their parent.

### Percentage (%)

Relative to the **parent element's** size.

```css
.child {
  width: 50%;   /* Half the width of the parent */
}
```

### Viewport Units

Relative to the **browser window** (viewport) size.

| Unit   | Meaning                            | Example                     |
|--------|------------------------------------|-----------------------------|
| `vw`   | 1% of viewport width               | `width: 50vw` = half screen |
| `vh`   | 1% of viewport height              | `height: 100vh` = full screen height |
| `vmin` | 1% of the smaller dimension (w or h) | Good for square elements  |
| `vmax` | 1% of the larger dimension (w or h)  | Rarely used               |

```css
/* Full-screen hero section */
.hero {
  width: 100vw;
  height: 100vh;
}

/* Text that scales with screen width */
.title {
  font-size: 5vw;   /* Gets bigger on wider screens */
}
```

```
  Viewport Units Visualized (Screen = 1200px x 800px)
  =====================================================

  1vw  = 12px    (1% of 1200)
  1vh  = 8px     (1% of 800)
  1vmin = 8px    (1% of the smaller: 800)
  1vmax = 12px   (1% of the larger: 1200)

  +-------- 100vw (1200px) --------+
  |                                | 100vh
  |          50vw = 600px          | (800px)
  |          50vh = 400px          |
  |                                |
  +--------------------------------+
```

### em vs rem

These are the two most important responsive font-size units:

| Unit  | Relative To              | Compounds? |
|-------|--------------------------|------------|
| `em`  | Parent element's font-size | Yes       |
| `rem` | Root (`<html>`) font-size  | No        |

**The compounding problem with `em`:**

```css
html { font-size: 16px; }

.parent {
  font-size: 1.5em;   /* 16 x 1.5 = 24px */
}

.parent .child {
  font-size: 1.5em;   /* 24 x 1.5 = 36px  (compounds!) */
}

.parent .child .grandchild {
  font-size: 1.5em;   /* 36 x 1.5 = 54px  (keeps growing!) */
}
```

**`rem` stays consistent:**

```css
html { font-size: 16px; }

.parent {
  font-size: 1.5rem;   /* 16 x 1.5 = 24px */
}

.parent .child {
  font-size: 1.5rem;   /* 16 x 1.5 = 24px  (same!) */
}

.parent .child .grandchild {
  font-size: 1.5rem;   /* 16 x 1.5 = 24px  (always same!) */
}
```

```
  em vs rem -- The Compounding Problem
  ======================================

  html (16px)
    |
    +-- .parent (1.5em)
    |     |
    |     |   em:  16 x 1.5 = 24px
    |     |   rem: 16 x 1.5 = 24px    <-- Same so far
    |     |
    |     +-- .child (1.5em)
    |           |
    |           |   em:  24 x 1.5 = 36px    <-- Compounded!
    |           |   rem: 16 x 1.5 = 24px    <-- Still 24px
    |           |
    |           +-- .grandchild (1.5em)
    |                 |
    |                 em:  36 x 1.5 = 54px    <-- Out of control!
    |                 rem: 16 x 1.5 = 24px    <-- Predictable
```

### When to Use Which Unit

| Situation                        | Recommended Unit | Why                                     |
|----------------------------------|------------------|-----------------------------------------|
| Font sizes                       | `rem`            | Predictable, no compounding             |
| Padding/margin (component)       | `em`             | Scales with the element's own font size |
| Layout widths                    | `%` or `fr`      | Relative to parent or grid              |
| Full-screen sections             | `vh` / `vw`      | Relative to viewport                    |
| Borders, shadows, small details  | `px`             | Should stay crisp at any size           |

---

## 4. Responsive Images

Images can break layouts if they are wider than their container. Responsive images **scale down** to fit.

### The Essential Rule

```css
img {
  max-width: 100%;
  height: auto;
}
```

This single rule ensures no image ever overflows its container. `max-width: 100%` means "be as wide as you want, but never wider than your parent." `height: auto` maintains the aspect ratio.

### object-fit

When an image must fill a container of a specific size (like a card thumbnail), use `object-fit` to control how it behaves:

```css
.thumbnail {
  width: 300px;
  height: 200px;
  object-fit: cover;    /* Crop to fill, maintain aspect ratio */
}
```

| Value      | Behavior                                    | Use Case                   |
|------------|---------------------------------------------|----------------------------|
| `cover`    | Fills container, crops excess               | Hero images, thumbnails    |
| `contain`  | Fits entirely inside, may leave empty space | Product images, logos      |
| `fill`     | Stretches to fill (distorts image)          | Rarely used                |
| `none`     | No resizing at all                          | When you need original size|

```
  object-fit Comparison (container is 300x200, image is 400x400)
  ================================================================

  cover                  contain               fill
  +----------+           +----------+          +----------+
  |//////////|           |   +--+   |          |//////////|
  |//IMAGE///|           |   |IM|   |          |/STRETCHED|
  |//CROPPED/|           |   |AG|   |          |//IMAGE///|
  |//////////|           |   +--+   |          |//////////|
  +----------+           +----------+          +----------+
  Fills area,            Fits inside,          Stretches to
  crops edges            gaps on sides         fill (distorts)
```

### picture Element and srcset

For advanced responsive images, HTML provides the `<picture>` element and `srcset` attribute. These let you serve **different image files** for different screen sizes, saving bandwidth on mobile:

```html
<!-- srcset: browser picks the best image based on screen width -->
<img
  src="image-small.jpg"
  srcset="
    image-small.jpg 480w,
    image-medium.jpg 768w,
    image-large.jpg 1200w
  "
  sizes="(max-width: 480px) 100vw,
         (max-width: 768px) 50vw,
         33vw"
  alt="Responsive image example"
>

<!-- picture: explicit art direction for different breakpoints -->
<picture>
  <source media="(max-width: 480px)" srcset="hero-mobile.jpg">
  <source media="(max-width: 1024px)" srcset="hero-tablet.jpg">
  <img src="hero-desktop.jpg" alt="Hero image">
</picture>
```

> **Why this matters:** A 3000px-wide hero image is 2MB. A phone only needs a 480px version at 100KB. Serving the right image saves data and load time.

---

## 5. Responsive Typography

Text sizes should **adapt smoothly** to the screen, not just jump at breakpoints.

### The clamp() Function

`clamp()` sets a font size that scales with the viewport but stays within a minimum and maximum:

```css
clamp(minimum, preferred, maximum)
```

```css
h1 {
  font-size: clamp(1.5rem, 4vw, 3.5rem);
  /*
    minimum:   1.5rem  (24px) -- never smaller than this
    preferred: 4vw     -- scales with viewport width
    maximum:   3.5rem  (56px) -- never larger than this
  */
}
```

```
  How clamp() Works
  ========================================================

  Font
  Size
   |
   |                          +------ maximum (3.5rem)
   |                     ____/
   |                ____/
   |           ____/         <-- preferred (4vw) scales here
   |      ____/
   |  ___/
   | /
   |/________________________+------ minimum (1.5rem)
   |
   +-----+-------+-------+--------> Screen Width
        320px   768px   1024px  1440px
```

### Fluid Typography Examples

```css
/* Body text */
body {
  font-size: clamp(1rem, 1.5vw, 1.25rem);
}

/* Main heading */
h1 {
  font-size: clamp(2rem, 5vw, 4rem);
}

/* Subheading */
h2 {
  font-size: clamp(1.5rem, 3vw, 2.5rem);
}

/* Small text */
small {
  font-size: clamp(0.75rem, 1.2vw, 0.875rem);
}
```

> **Tip:** `clamp()` replaces the need for multiple media queries just to change font sizes. One line handles all screen sizes.

---

## 6. CSS Transitions

Transitions let you **smoothly animate** a CSS property from one value to another when a change occurs (like a hover or a class toggle).

### Real-Life Analogy

When you dim a light with a dimmer switch, the brightness changes **gradually** -- not instantly. CSS transitions work the same way: instead of a property jumping from value A to value B, it glides there over a duration you choose.

### Transition Properties

| Property                       | What It Controls                         | Example                              |
|--------------------------------|------------------------------------------|--------------------------------------|
| `transition-property`          | Which CSS property to animate            | `background-color`, `transform`, `all` |
| `transition-duration`          | How long the animation takes             | `0.3s`, `500ms`                      |
| `transition-timing-function`   | The speed curve of the animation         | `ease`, `linear`, `ease-in-out`      |
| `transition-delay`             | Wait time before the transition starts   | `0s`, `0.2s`                         |

### transition-property

Specifies which property should transition:

```css
.button {
  background-color: blue;
  color: white;
  transition-property: background-color;   /* Only animate background */
}

.button:hover {
  background-color: darkblue;
}
```

Use `all` to transition every property that changes:

```css
.button {
  transition-property: all;
}
```

### transition-duration

How long the transition takes (in seconds `s` or milliseconds `ms`):

```css
.button {
  transition-duration: 0.3s;    /* 300 milliseconds */
}
```

### transition-timing-function

Controls the **speed curve** -- how fast the animation goes at different points:

```css
.box {
  transition-timing-function: ease;
}
```

```
  Timing Functions Visualized (progress over time)
  ==================================================

  ease (default)     linear           ease-in
  Progress           Progress         Progress
  |      ___/        |       /        |       /
  |    /             |      /         |      /
  |  /               |     /          |     /
  | /                |    /           |   /
  |/___              |   /            |__/
  +-------> Time     +-------> Time   +-------> Time
  Slow-fast-slow     Constant speed   Slow start

  ease-out           ease-in-out
  Progress           Progress
  |    ___/          |      ___/
  |   /              |    /
  |  /               |  /
  | /                | /
  |/                 |/___
  +-------> Time     +-------> Time
  Fast start,        Slow-fast-slow
  slow end           (pronounced)
```

**cubic-bezier:** For custom curves, define your own with four control points:

```css
.box {
  transition-timing-function: cubic-bezier(0.68, -0.55, 0.27, 1.55);
  /* This creates a slight "overshoot" bounce effect */
}
```

### transition-delay

Wait before the transition begins:

```css
.tooltip {
  opacity: 0;
  transition-property: opacity;
  transition-duration: 0.3s;
  transition-delay: 0.5s;     /* Wait 500ms, then fade in */
}

.parent:hover .tooltip {
  opacity: 1;
}
```

### Transition Shorthand

Combine all transition properties into one line:

```css
/* transition: property duration timing-function delay; */

.button {
  transition: background-color 0.3s ease 0s;
}

/* Multiple properties */
.card {
  transition: transform 0.3s ease, box-shadow 0.3s ease 0.1s;
}

/* All properties */
.element {
  transition: all 0.3s ease;
}
```

### Common Use Cases

**Hover effect on a button:**

```css
.btn {
  background-color: #3498db;
  color: white;
  padding: 12px 24px;
  border: none;
  border-radius: 5px;
  cursor: pointer;
  transition: all 0.3s ease;
}

.btn:hover {
  background-color: #2980b9;
  transform: translateY(-2px);
  box-shadow: 0 4px 12px rgba(0, 0, 0, 0.2);
}
```

**Smooth color change on links:**

```css
a {
  color: #3498db;
  transition: color 0.2s ease;
}

a:hover {
  color: #e74c3c;
}
```

**Card lift on hover:**

```css
.card {
  background: white;
  border-radius: 8px;
  box-shadow: 0 2px 8px rgba(0, 0, 0, 0.1);
  transition: transform 0.3s ease, box-shadow 0.3s ease;
}

.card:hover {
  transform: translateY(-5px);
  box-shadow: 0 8px 25px rgba(0, 0, 0, 0.15);
}
```

---

## 7. CSS Animations with @keyframes

While transitions animate between **two states** (e.g., hover on/off), CSS animations let you define **multi-step sequences** that can run automatically, loop infinitely, and move through many stages.

### Real-Life Analogy

A transition is like flipping a light switch -- on or off. An animation is like a light show at a concert -- the lights change color, intensity, and position through a choreographed sequence of steps.

### @keyframes Rule

Define the animation steps using `@keyframes`:

```css
@keyframes fadeIn {
  from {
    opacity: 0;
  }
  to {
    opacity: 1;
  }
}
```

Or use percentage-based steps for more control:

```css
@keyframes colorCycle {
  0%   { background-color: red; }
  25%  { background-color: yellow; }
  50%  { background-color: green; }
  75%  { background-color: blue; }
  100% { background-color: red; }
}
```

### Animation Properties

| Property                       | What It Controls                           | Values                                  |
|--------------------------------|--------------------------------------------|-----------------------------------------|
| `animation-name`               | Which `@keyframes` to use                  | Name of the keyframes                   |
| `animation-duration`           | How long one cycle takes                   | `1s`, `500ms`                           |
| `animation-timing-function`    | Speed curve                                | `ease`, `linear`, `ease-in-out`         |
| `animation-delay`              | Wait before starting                       | `0s`, `0.5s`                            |
| `animation-iteration-count`    | How many times to repeat                   | `1`, `3`, `infinite`                    |
| `animation-direction`          | Which direction to play                    | `normal`, `reverse`, `alternate`        |
| `animation-fill-mode`          | Style before/after animation               | `none`, `forwards`, `backwards`, `both` |

### animation-name and animation-duration

```css
.box {
  animation-name: fadeIn;
  animation-duration: 1s;
}
```

### animation-timing-function

Same options as transitions: `ease`, `linear`, `ease-in`, `ease-out`, `ease-in-out`, `cubic-bezier()`.

```css
.box {
  animation-timing-function: ease-in-out;
}
```

### animation-delay

```css
.box {
  animation-delay: 0.5s;   /* Wait half a second before starting */
}
```

### animation-iteration-count

```css
.spinner {
  animation-iteration-count: infinite;   /* Loop forever */
}

.notification {
  animation-iteration-count: 3;          /* Play 3 times, then stop */
}
```

### animation-direction

| Value       | Behavior                                            |
|-------------|-----------------------------------------------------|
| `normal`    | Plays forward every time (0% to 100%)                |
| `reverse`   | Plays backward every time (100% to 0%)               |
| `alternate` | Plays forward, then backward, then forward...        |
| `alternate-reverse` | Plays backward first, then alternates         |

```
  animation-direction Visualized
  ================================

  normal:    --> --> --> -->     (always forward)
  reverse:   <-- <-- <-- <--    (always backward)
  alternate: --> <-- --> <--    (forward, backward, ...)
```

### animation-fill-mode

Controls what styles apply **before** and **after** the animation:

| Value      | Before Animation        | After Animation          |
|------------|-------------------------|--------------------------|
| `none`     | Original styles         | Original styles          |
| `forwards` | Original styles         | Keeps final keyframe     |
| `backwards`| Uses first keyframe     | Original styles          |
| `both`     | Uses first keyframe     | Keeps final keyframe     |

```css
.fade-in {
  opacity: 0;
  animation: fadeIn 1s ease forwards;
  /* "forwards" keeps opacity: 1 after the animation ends */
}
```

### Animation Shorthand

```css
/* animation: name duration timing-function delay iteration-count direction fill-mode; */

.element {
  animation: fadeIn 1s ease 0s 1 normal forwards;
}

/* Shorter version (most common) */
.element {
  animation: fadeIn 1s ease forwards;
}
```

### Practical Animation Examples

**1. Loading Spinner**

```css
@keyframes spin {
  from {
    transform: rotate(0deg);
  }
  to {
    transform: rotate(360deg);
  }
}

.spinner {
  width: 40px;
  height: 40px;
  border: 4px solid #ddd;
  border-top: 4px solid #3498db;
  border-radius: 50%;
  animation: spin 1s linear infinite;
}
```

**2. Fade In**

```css
@keyframes fadeIn {
  from {
    opacity: 0;
    transform: translateY(20px);
  }
  to {
    opacity: 1;
    transform: translateY(0);
  }
}

.fade-in {
  animation: fadeIn 0.6s ease forwards;
}
```

**3. Slide In from Left**

```css
@keyframes slideInLeft {
  from {
    transform: translateX(-100%);
    opacity: 0;
  }
  to {
    transform: translateX(0);
    opacity: 1;
  }
}

.slide-in {
  animation: slideInLeft 0.5s ease-out forwards;
}
```

**4. Pulse Effect**

```css
@keyframes pulse {
  0%   { transform: scale(1); }
  50%  { transform: scale(1.05); }
  100% { transform: scale(1); }
}

.pulse {
  animation: pulse 2s ease-in-out infinite;
}
```

**5. Bounce**

```css
@keyframes bounce {
  0%, 100% {
    transform: translateY(0);
  }
  25% {
    transform: translateY(-15px);
  }
  50% {
    transform: translateY(0);
  }
  75% {
    transform: translateY(-7px);
  }
}

.bounce {
  animation: bounce 1s ease infinite;
}
```

---

## 8. CSS Transform

Transforms let you **move, rotate, scale, and skew** elements without affecting the normal document flow. They are the building blocks of animation.

### translate(x, y) -- Move

Moves an element from its current position:

```css
.box {
  transform: translate(50px, 100px);
  /* Move 50px right and 100px down */
}

/* Single axis shortcuts */
.box {
  transform: translateX(50px);    /* Move right */
  transform: translateY(-30px);   /* Move up */
}
```

```
  translate(50px, 30px)
  ===========================

  +------+
  |Before|
  +------+
       \
        \  50px right, 30px down
         \
          +------+
          |After |
          +------+
```

### rotate(deg) -- Rotate

Rotates an element clockwise by the given degrees:

```css
.box {
  transform: rotate(45deg);     /* 45 degrees clockwise */
}

.box {
  transform: rotate(-90deg);    /* 90 degrees counter-clockwise */
}
```

```
  rotate(45deg)
  ===========================

  Before          After

  +------+           /\
  |      |          /  \
  |      |         /    \
  +------+         \    /
                    \  /
                     \/
```

### scale(x, y) -- Resize

Scales an element larger or smaller:

```css
.box {
  transform: scale(1.5);        /* 150% of original size */
}

.box {
  transform: scale(2, 0.5);     /* 2x wide, half height */
}

.box {
  transform: scaleX(2);         /* Double width only */
}
```

```
  scale(0.5)          scale(1)          scale(2)
  +---+               +------+          +------------+
  |   |               |      |          |            |
  +---+               |      |          |            |
  Half size           +------+          |            |
                      Original          |            |
                                        +------------+
                                        Double size
```

### skew(x, y) -- Slant

Tilts an element along the X or Y axis:

```css
.box {
  transform: skew(20deg, 0);     /* Slant horizontally */
}

.box {
  transform: skewX(20deg);       /* Same as above */
  transform: skewY(10deg);       /* Slant vertically */
}
```

```
  skewX(20deg)
  ===========================

  Before              After

  +------+            +--------+
  |      |           / Slanted/
  |      |          / shape  /
  +------+         +--------+
```

### transform-origin

By default, transforms happen from the **center** of the element. `transform-origin` changes the pivot point:

```css
.box {
  transform: rotate(45deg);
  transform-origin: top left;       /* Rotate from the top-left corner */
}

.box {
  transform-origin: center;         /* Default */
  transform-origin: 0% 100%;        /* Bottom-left */
  transform-origin: 50px 50px;      /* Specific pixel position */
}
```

```
  transform-origin with rotate(45deg)
  ======================================

  Origin: center (default)      Origin: top left

       .---.                    *---------
      / Box \                    \  Box   \
     /       \                    \        \
     \       /                     \        \
      \ Box /                       \--------
       '---'
  Rotates around center        Rotates around top-left corner
  (*) = pivot point
```

### Combining Multiple Transforms

Chain multiple transforms in a single `transform` property:

```css
.card:hover {
  transform: translateY(-10px) rotate(2deg) scale(1.02);
  /* Move up, slight tilt, and slightly larger */
}
```

> **Important:** The order matters. Transforms are applied **right to left**. `translate` then `rotate` gives a different result than `rotate` then `translate`.

```css
/* These produce DIFFERENT results: */
transform: translate(100px, 0) rotate(45deg);   /* Rotate first, then move */
transform: rotate(45deg) translate(100px, 0);   /* Move first, then rotate */
```

---

## 9. CSS Variables (Custom Properties)

CSS variables (also called custom properties) let you **store values once** and **reuse them everywhere** -- making your code easier to maintain and enabling powerful features like theming.

### Real-Life Analogy

Think of a paint store. Instead of telling each worker "use hex color #3498db," you label a paint can "brand-blue." If you later decide to change the brand color, you change the label on one can -- not every wall in the building. CSS variables work the same way.

### Declaring Variables

Declare variables with a double-dash prefix `--`:

```css
:root {
  --primary-color: #3498db;
  --secondary-color: #2ecc71;
  --text-color: #333333;
  --font-main: 'Segoe UI', sans-serif;
  --spacing-sm: 8px;
  --spacing-md: 16px;
  --spacing-lg: 32px;
  --border-radius: 8px;
}
```

> **`:root`** is the highest-level selector (equivalent to `<html>`) -- variables declared here are available **everywhere** in your CSS.

### Using Variables

Use the `var()` function to retrieve a variable's value:

```css
.button {
  background-color: var(--primary-color);
  color: white;
  padding: var(--spacing-sm) var(--spacing-md);
  border-radius: var(--border-radius);
  font-family: var(--font-main);
}

.card {
  border: 1px solid var(--primary-color);
  padding: var(--spacing-lg);
  border-radius: var(--border-radius);
}
```

**Fallback values:** Provide a default in case the variable is not defined:

```css
.element {
  color: var(--accent-color, #e74c3c);
  /* If --accent-color is not defined, use #e74c3c */
}
```

### Root-Level Variables for Theming

The real power of CSS variables is **theming** -- changing multiple styles at once by updating a few variables.

```css
/* Default (Light) Theme */
:root {
  --bg-color: #ffffff;
  --text-color: #333333;
  --card-bg: #f5f5f5;
  --border-color: #dddddd;
  --primary: #3498db;
  --shadow: 0 2px 8px rgba(0, 0, 0, 0.1);
}

/* Dark Theme */
[data-theme="dark"] {
  --bg-color: #1a1a2e;
  --text-color: #e0e0e0;
  --card-bg: #16213e;
  --border-color: #333355;
  --primary: #4fc3f7;
  --shadow: 0 2px 8px rgba(0, 0, 0, 0.4);
}

/* Styles using variables -- these do NOT change */
body {
  background-color: var(--bg-color);
  color: var(--text-color);
}

.card {
  background-color: var(--card-bg);
  border: 1px solid var(--border-color);
  box-shadow: var(--shadow);
}

.btn-primary {
  background-color: var(--primary);
}
```

```
  CSS Variables: Theming Flow
  ==========================================

  :root (light)             [data-theme="dark"]
  +-------------------+     +-------------------+
  | --bg: #fff        |     | --bg: #1a1a2e     |
  | --text: #333      |     | --text: #e0e0e0   |
  | --primary: #3498db|     | --primary: #4fc3f7|
  +-------------------+     +-------------------+
           |                          |
           v                          v
  +-------------------+     +-------------------+
  | body {            |     | body {            |
  |   bg: var(--bg)   |     |   bg: var(--bg)   |
  |   color: var(--t) |     |   color: var(--t) |
  | }                 |     | }                 |
  +-------------------+     +-------------------+
  Same CSS rules, different results!
```

### Real-Life Use: Dark Mode Toggle

Here is a complete dark mode implementation:

**HTML:**

```html
<button id="theme-toggle">Toggle Dark Mode</button>
```

**CSS:**

```css
:root {
  --bg-color: #ffffff;
  --text-color: #333333;
  --card-bg: #f8f9fa;
  --primary: #3498db;
  --transition-speed: 0.3s;
}

[data-theme="dark"] {
  --bg-color: #1a1a2e;
  --text-color: #e0e0e0;
  --card-bg: #16213e;
  --primary: #4fc3f7;
}

body {
  background-color: var(--bg-color);
  color: var(--text-color);
  transition: background-color var(--transition-speed),
              color var(--transition-speed);
}

.card {
  background-color: var(--card-bg);
  transition: background-color var(--transition-speed);
}
```

**JavaScript:**

```javascript
const toggleBtn = document.getElementById("theme-toggle");

toggleBtn.addEventListener("click", () => {
  const currentTheme = document.documentElement.getAttribute("data-theme");

  if (currentTheme === "dark") {
    document.documentElement.removeAttribute("data-theme");
  } else {
    document.documentElement.setAttribute("data-theme", "dark");
  }
});
```

---

## 10. Week 8 Project: Fully Responsive Portfolio Page

Build a **complete portfolio page** that is responsive across all devices and uses smooth animations.

### Project Requirements

```
  Portfolio Page Layout
  ================================================================

  DESKTOP (1024px+)              TABLET (768px)     MOBILE (480px)
  +----------------------+     +--------------+     +--------+
  | [Logo]  Nav  Nav Nav |     | [Logo] [=]   |     | [Logo] |
  +----------------------+     +--------------+     | [=]    |
  |                      |     |              |     +--------+
  |    HERO SECTION      |     |    HERO      |     |  HERO  |
  |    Name & Title      |     |   Section    |     | Section|
  |    [CTA Button]      |     |              |     |        |
  +----------------------+     +--------------+     +--------+
  |  Skill | Skill | Skl |     | Skill | Skl  |     | Skill  |
  |  Skill | Skill | Skl |     | Skill | Skl  |     | Skill  |
  +----------------------+     +--------------+     | Skill  |
  | Project  | Project   |     | Project      |     +--------+
  | Card     | Card      |     | Project      |     | Proj 1 |
  | Project  | Project   |     | Project      |     | Proj 2 |
  | Card     | Card      |     | Project      |     | Proj 3 |
  +----------------------+     +--------------+     +--------+
  |   Contact Form       |     | Contact Form |     | Contact|
  +----------------------+     +--------------+     | Form   |
  |   Footer             |     | Footer       |     +--------+
  +----------------------+     +--------------+     | Footer |
                                                     +--------+
```

### Full Project Code

**index.html**

```html
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>My Portfolio</title>
  <link rel="stylesheet" href="style.css">
</head>
<body>

  <!-- Navigation -->
  <nav class="navbar">
    <div class="nav-container">
      <a href="#" class="logo">Portfolio</a>
      <button class="hamburger" id="hamburger">
        &#9776;
      </button>
      <ul class="nav-links" id="nav-links">
        <li><a href="#hero">Home</a></li>
        <li><a href="#skills">Skills</a></li>
        <li><a href="#projects">Projects</a></li>
        <li><a href="#contact">Contact</a></li>
      </ul>
    </div>
  </nav>

  <!-- Hero Section -->
  <section id="hero" class="hero">
    <div class="hero-content">
      <h1 class="hero-title">Hi, I'm <span class="highlight">John Doe</span></h1>
      <p class="hero-subtitle">Full-Stack Web Developer</p>
      <a href="#projects" class="btn btn-primary">View My Work</a>
    </div>
  </section>

  <!-- Skills Section -->
  <section id="skills" class="skills">
    <h2 class="section-title">My Skills</h2>
    <div class="skills-grid">
      <div class="skill-card">
        <h3>HTML5</h3>
        <p>Semantic markup & accessibility</p>
      </div>
      <div class="skill-card">
        <h3>CSS3</h3>
        <p>Responsive design & animations</p>
      </div>
      <div class="skill-card">
        <h3>JavaScript</h3>
        <p>ES6+, DOM manipulation</p>
      </div>
      <div class="skill-card">
        <h3>React</h3>
        <p>Components, hooks, state</p>
      </div>
      <div class="skill-card">
        <h3>Node.js</h3>
        <p>REST APIs, Express</p>
      </div>
      <div class="skill-card">
        <h3>MongoDB</h3>
        <p>Database design, Mongoose</p>
      </div>
    </div>
  </section>

  <!-- Projects Section -->
  <section id="projects" class="projects">
    <h2 class="section-title">My Projects</h2>
    <div class="projects-grid">
      <div class="project-card">
        <div class="project-image"></div>
        <div class="project-info">
          <h3>E-Commerce Store</h3>
          <p>A full-stack online store built with MERN stack.</p>
          <a href="#" class="btn btn-small">View Project</a>
        </div>
      </div>
      <div class="project-card">
        <div class="project-image"></div>
        <div class="project-info">
          <h3>Task Manager</h3>
          <p>A productivity app with drag-and-drop features.</p>
          <a href="#" class="btn btn-small">View Project</a>
        </div>
      </div>
      <div class="project-card">
        <div class="project-image"></div>
        <div class="project-info">
          <h3>Weather Dashboard</h3>
          <p>Real-time weather data using external APIs.</p>
          <a href="#" class="btn btn-small">View Project</a>
        </div>
      </div>
      <div class="project-card">
        <div class="project-image"></div>
        <div class="project-info">
          <h3>Chat Application</h3>
          <p>Real-time messaging with Socket.IO.</p>
          <a href="#" class="btn btn-small">View Project</a>
        </div>
      </div>
    </div>
  </section>

  <!-- Contact Section -->
  <section id="contact" class="contact">
    <h2 class="section-title">Get In Touch</h2>
    <form class="contact-form">
      <div class="form-group">
        <input type="text" placeholder="Your Name" required>
      </div>
      <div class="form-group">
        <input type="email" placeholder="Your Email" required>
      </div>
      <div class="form-group">
        <textarea placeholder="Your Message" rows="5" required></textarea>
      </div>
      <button type="submit" class="btn btn-primary">Send Message</button>
    </form>
  </section>

  <!-- Footer -->
  <footer class="footer">
    <p>Designed & Built by John Doe &copy; 2026</p>
  </footer>

  <script src="script.js"></script>
</body>
</html>
```

**style.css**

```css
/* ========================================
   CSS Variables
   ======================================== */
:root {
  --primary: #3498db;
  --primary-dark: #2980b9;
  --bg-color: #ffffff;
  --text-color: #333333;
  --text-light: #777777;
  --card-bg: #f8f9fa;
  --border-color: #e0e0e0;
  --shadow: 0 2px 10px rgba(0, 0, 0, 0.1);
  --shadow-hover: 0 8px 25px rgba(0, 0, 0, 0.15);
  --font-main: 'Segoe UI', Tahoma, Geneva, Verdana, sans-serif;
  --border-radius: 8px;
  --transition: 0.3s ease;
  --max-width: 1200px;
}

/* ========================================
   Reset & Base Styles
   ======================================== */
* {
  margin: 0;
  padding: 0;
  box-sizing: border-box;
}

html {
  scroll-behavior: smooth;
}

body {
  font-family: var(--font-main);
  color: var(--text-color);
  background-color: var(--bg-color);
  line-height: 1.6;
}

a {
  text-decoration: none;
  color: inherit;
}

ul {
  list-style: none;
}

/* ========================================
   Reusable Components
   ======================================== */
.section-title {
  font-size: clamp(1.8rem, 4vw, 2.5rem);
  text-align: center;
  margin-bottom: 40px;
  position: relative;
}

.section-title::after {
  content: '';
  display: block;
  width: 60px;
  height: 3px;
  background-color: var(--primary);
  margin: 10px auto 0;
  border-radius: 2px;
}

.btn {
  display: inline-block;
  padding: 12px 30px;
  border: none;
  border-radius: var(--border-radius);
  cursor: pointer;
  font-size: 1rem;
  transition: all var(--transition);
}

.btn-primary {
  background-color: var(--primary);
  color: white;
}

.btn-primary:hover {
  background-color: var(--primary-dark);
  transform: translateY(-2px);
  box-shadow: var(--shadow-hover);
}

.btn-small {
  padding: 8px 20px;
  font-size: 0.9rem;
  background-color: var(--primary);
  color: white;
}

.btn-small:hover {
  background-color: var(--primary-dark);
}

/* ========================================
   Navbar
   ======================================== */
.navbar {
  position: fixed;
  top: 0;
  left: 0;
  width: 100%;
  background-color: var(--bg-color);
  box-shadow: var(--shadow);
  z-index: 1000;
}

.nav-container {
  max-width: var(--max-width);
  margin: 0 auto;
  padding: 15px 20px;
  display: flex;
  justify-content: space-between;
  align-items: center;
}

.logo {
  font-size: 1.5rem;
  font-weight: 700;
  color: var(--primary);
}

.nav-links {
  display: flex;
  gap: 30px;
}

.nav-links a {
  font-size: 1rem;
  color: var(--text-color);
  transition: color var(--transition);
  position: relative;
}

.nav-links a::after {
  content: '';
  position: absolute;
  bottom: -5px;
  left: 0;
  width: 0%;
  height: 2px;
  background-color: var(--primary);
  transition: width var(--transition);
}

.nav-links a:hover {
  color: var(--primary);
}

.nav-links a:hover::after {
  width: 100%;
}

.hamburger {
  display: none;
  background: none;
  border: none;
  font-size: 1.5rem;
  cursor: pointer;
  color: var(--text-color);
}

/* ========================================
   Hero Section
   ======================================== */
.hero {
  height: 100vh;
  display: flex;
  align-items: center;
  justify-content: center;
  text-align: center;
  padding: 0 20px;
  background: linear-gradient(135deg, #667eea 0%, #764ba2 100%);
  color: white;
}

.hero-title {
  font-size: clamp(2rem, 6vw, 4rem);
  margin-bottom: 15px;
  animation: fadeInDown 1s ease forwards;
}

.highlight {
  color: #f1c40f;
}

.hero-subtitle {
  font-size: clamp(1rem, 3vw, 1.5rem);
  margin-bottom: 30px;
  opacity: 0;
  animation: fadeInUp 1s ease 0.3s forwards;
}

.hero .btn {
  opacity: 0;
  animation: fadeInUp 1s ease 0.6s forwards;
}

/* ========================================
   Skills Section
   ======================================== */
.skills {
  padding: 80px 20px;
  max-width: var(--max-width);
  margin: 0 auto;
}

.skills-grid {
  display: grid;
  grid-template-columns: repeat(3, 1fr);
  gap: 25px;
}

.skill-card {
  background-color: var(--card-bg);
  padding: 30px;
  border-radius: var(--border-radius);
  text-align: center;
  border: 1px solid var(--border-color);
  transition: all var(--transition);
}

.skill-card:hover {
  transform: translateY(-5px);
  box-shadow: var(--shadow-hover);
  border-color: var(--primary);
}

.skill-card h3 {
  color: var(--primary);
  margin-bottom: 10px;
  font-size: 1.3rem;
}

.skill-card p {
  color: var(--text-light);
  font-size: 0.95rem;
}

/* ========================================
   Projects Section
   ======================================== */
.projects {
  padding: 80px 20px;
  background-color: var(--card-bg);
}

.projects-grid {
  max-width: var(--max-width);
  margin: 0 auto;
  display: grid;
  grid-template-columns: repeat(2, 1fr);
  gap: 30px;
}

.project-card {
  background-color: var(--bg-color);
  border-radius: var(--border-radius);
  overflow: hidden;
  box-shadow: var(--shadow);
  transition: all var(--transition);
}

.project-card:hover {
  transform: translateY(-5px);
  box-shadow: var(--shadow-hover);
}

.project-image {
  height: 200px;
  background: linear-gradient(135deg, #3498db, #8e44ad);
}

.project-info {
  padding: 20px;
}

.project-info h3 {
  margin-bottom: 10px;
  font-size: 1.2rem;
}

.project-info p {
  color: var(--text-light);
  margin-bottom: 15px;
  font-size: 0.95rem;
}

/* ========================================
   Contact Section
   ======================================== */
.contact {
  padding: 80px 20px;
  max-width: 600px;
  margin: 0 auto;
}

.contact-form {
  display: flex;
  flex-direction: column;
  gap: 15px;
}

.contact-form input,
.contact-form textarea {
  width: 100%;
  padding: 12px 15px;
  border: 1px solid var(--border-color);
  border-radius: var(--border-radius);
  font-size: 1rem;
  font-family: var(--font-main);
  transition: border-color var(--transition);
}

.contact-form input:focus,
.contact-form textarea:focus {
  outline: none;
  border-color: var(--primary);
  box-shadow: 0 0 0 3px rgba(52, 152, 219, 0.1);
}

/* ========================================
   Footer
   ======================================== */
.footer {
  text-align: center;
  padding: 30px 20px;
  background-color: #2c3e50;
  color: #ecf0f1;
  font-size: 0.9rem;
}

/* ========================================
   Animations
   ======================================== */
@keyframes fadeInDown {
  from {
    opacity: 0;
    transform: translateY(-30px);
  }
  to {
    opacity: 1;
    transform: translateY(0);
  }
}

@keyframes fadeInUp {
  from {
    opacity: 0;
    transform: translateY(30px);
  }
  to {
    opacity: 1;
    transform: translateY(0);
  }
}

/* ========================================
   Responsive -- Tablet (max-width: 1024px)
   ======================================== */
@media (max-width: 1024px) {
  .skills-grid {
    grid-template-columns: repeat(2, 1fr);
  }
}

/* ========================================
   Responsive -- Mobile (max-width: 768px)
   ======================================== */
@media (max-width: 768px) {
  /* Hamburger menu */
  .hamburger {
    display: block;
  }

  .nav-links {
    display: none;
    flex-direction: column;
    position: absolute;
    top: 60px;
    left: 0;
    width: 100%;
    background-color: var(--bg-color);
    box-shadow: var(--shadow);
    padding: 20px;
    gap: 15px;
  }

  .nav-links.active {
    display: flex;
  }

  /* Skills: stack to single column */
  .skills-grid {
    grid-template-columns: 1fr;
  }

  /* Projects: stack to single column */
  .projects-grid {
    grid-template-columns: 1fr;
  }

  /* Hero adjustments */
  .hero {
    padding: 0 15px;
  }
}

/* ========================================
   Responsive -- Small Phone (max-width: 480px)
   ======================================== */
@media (max-width: 480px) {
  .skill-card {
    padding: 20px;
  }

  .project-image {
    height: 150px;
  }

  .btn {
    padding: 10px 20px;
    font-size: 0.9rem;
  }
}
```

**script.js**

```javascript
// Mobile hamburger menu toggle
const hamburger = document.getElementById("hamburger");
const navLinks = document.getElementById("nav-links");

hamburger.addEventListener("click", () => {
  navLinks.classList.toggle("active");
});

// Close menu when a link is clicked
navLinks.addEventListener("click", (e) => {
  if (e.target.tagName === "A") {
    navLinks.classList.remove("active");
  }
});
```

---

## 11. Summary -- CSS Weeks 5-8 Recap

Here is a complete overview of everything covered in the CSS portion of this course:

```
  CSS Learning Path -- Weeks 5 through 8
  ================================================================

  Week 5: CSS Fundamentals
  +------------------------------------------------------+
  |  Selectors    |  Colors       |  Typography          |
  |  Specificity  |  Backgrounds  |  Text Styling        |
  |  Cascade      |  Borders      |  Units (px, %, em)   |
  +------------------------------------------------------+
                          |
                          v
  Week 6: Box Model & Layout
  +------------------------------------------------------+
  |  Content, Padding, Border, Margin                    |
  |  Display (block, inline, inline-block, none)         |
  |  Position (static, relative, absolute, fixed)        |
  |  Float & Clear (legacy)                              |
  +------------------------------------------------------+
                          |
                          v
  Week 7: Flexbox & Grid
  +------------------------------------------------------+
  |  Flexbox: 1D layouts (rows OR columns)               |
  |  Grid: 2D layouts (rows AND columns)                 |
  |  Alignment: justify-content, align-items             |
  |  Responsive: auto-fit, minmax()                      |
  +------------------------------------------------------+
                          |
                          v
  Week 8: Responsive Design & Animations
  +------------------------------------------------------+
  |  Media Queries & Breakpoints                         |
  |  Responsive Units (%, vw, vh, rem)                   |
  |  Responsive Images & Typography                      |
  |  CSS Transitions & Animations (@keyframes)           |
  |  CSS Transforms (translate, rotate, scale, skew)     |
  |  CSS Variables & Theming                             |
  +------------------------------------------------------+
```

### Quick Reference Table

| Topic                  | Key Concept                              | Example                                    |
|------------------------|------------------------------------------|--------------------------------------------|
| Media Queries          | Apply CSS at specific screen widths      | `@media (max-width: 768px) { }`           |
| Responsive Units       | Scale with screen/parent                 | `rem`, `vw`, `vh`, `%`                    |
| Responsive Images      | Never overflow container                 | `max-width: 100%; height: auto;`          |
| Fluid Typography       | Text scales smoothly                     | `clamp(1rem, 3vw, 2rem)`                  |
| Transitions            | Smooth state changes                     | `transition: all 0.3s ease;`              |
| Animations             | Multi-step, auto-playing                 | `animation: fadeIn 1s ease forwards;`     |
| Transforms             | Move, rotate, scale, skew               | `transform: translateY(-5px) scale(1.02);`|
| CSS Variables           | Reusable, themeable values              | `var(--primary-color)`                     |

### What is Next?

In **Week 9**, we will move into **JavaScript with the Browser** -- combining everything we have learned about HTML, CSS, and JS to build fully interactive web applications. The responsive layouts and animations from this week will be essential as we start building real projects.

---

> **Practice Assignment:** Take any website you use daily (a news site, social media, an online store) and resize your browser window from desktop to mobile width. Observe how the layout changes at each breakpoint. Try to identify which CSS techniques from this week are being used.
