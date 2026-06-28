# Week 5 — Introduction to CSS

A comprehensive beginner-to-professional guide covering the fundamentals of CSS (Cascading Style Sheets). This document is designed for students who have completed 4 weeks of HTML and are now learning CSS for the first time. It covers what CSS is, how to apply it, selectors, colors, backgrounds, typography, and the cascade.

---

## Table of Contents

1. [What Is CSS?](#1-what-is-css)
2. [Why CSS Is Needed](#2-why-css-is-needed)
3. [History of CSS](#3-history-of-css)
4. [Three Ways to Apply CSS](#4-three-ways-to-apply-css)
5. [CSS Syntax](#5-css-syntax)
6. [CSS Selectors](#6-css-selectors)
7. [CSS Colors](#7-css-colors)
8. [CSS Backgrounds](#8-css-backgrounds)
9. [CSS Typography](#9-css-typography)
10. [CSS Inheritance and the Cascade](#10-css-inheritance-and-the-cascade)
11. [Summary](#11-summary)

---

## 1. What Is CSS?

**CSS (Cascading Style Sheets)** is a stylesheet language used to describe the presentation and visual appearance of an HTML document. While HTML defines the structure and content of a web page, CSS controls how that content looks — colors, fonts, spacing, layout, and animations.

### The Three Pillars of a Web Page

```
┌────────────────────────────────────────────────────────────────┐
│                   THE THREE PILLARS OF THE WEB                 │
│                                                                │
│   ┌──────────────┐   ┌──────────────┐   ┌──────────────┐      │
│   │     HTML     │   │     CSS      │   │  JavaScript  │      │
│   │              │   │              │   │              │      │
│   │  Structure   │   │   Styling    │   │  Behavior    │      │
│   │  (Skeleton)  │   │ (Skin,       │   │ (Muscles     │      │
│   │              │   │  Clothes,    │   │  & Brain)    │      │
│   │              │   │  Makeup)     │   │              │      │
│   └──────────────┘   └──────────────┘   └──────────────┘      │
│                                                                │
│   Defines WHAT       Defines HOW        Defines WHAT           │
│   is on the page     it looks           it does                │
└────────────────────────────────────────────────────────────────┘
```

### Real-Life Example: Building a House

Think of a web page like a human body or a house:

| Component | Web Technology | Real-Life Analogy |
|-----------|---------------|-------------------|
| **HTML** | Structure & content | The skeleton of a body, or the bricks and walls of a house |
| **CSS** | Visual presentation | The skin, clothes, and makeup on a body, or the paint, curtains, and decorations in a house |
| **JavaScript** | Interactivity & logic | The muscles and brain that let the body move and think, or the electrical system and plumbing that make the house functional |

**Without CSS**, every website would look like a plain text document — black text on a white background with no colors, no spacing, and no visual design. CSS is what transforms a plain HTML skeleton into a beautiful, professional-looking web page.

---

## 2. Why CSS Is Needed

### Websites Without CSS vs. With CSS

```
┌─────────────────────────────┐     ┌─────────────────────────────┐
│   WITHOUT CSS               │     │   WITH CSS                  │
│                             │     │                             │
│   My Website                │     │  ┌───────────────────────┐  │
│                             │     │  │  MY WEBSITE     [=]   │  │
│   Home About Contact        │     │  │  ==================== │  │
│                             │     │  │  Home | About | Contact│  │
│   Welcome to my site.       │     │  ├───────────────────────┤  │
│   This is a paragraph.      │     │  │                       │  │
│                             │     │  │  Welcome to my site.  │  │
│   - Item 1                  │     │  │                       │  │
│   - Item 2                  │     │  │  This is a paragraph  │  │
│   - Item 3                  │     │  │  with nice spacing.   │  │
│                             │     │  │                       │  │
│   Submit                    │     │  │  * Item 1             │  │
│                             │     │  │  * Item 2             │  │
│   Plain, boring, and        │     │  │  * Item 3             │  │
│   unprofessional.           │     │  │                       │  │
│                             │     │  │  [  Submit  ]         │  │
│                             │     │  │                       │  │
│                             │     │  │  Professional and     │  │
│                             │     │  │  visually appealing!  │  │
│                             │     │  └───────────────────────┘  │
└─────────────────────────────┘     └─────────────────────────────┘
```

### Key Reasons CSS Is Essential

| Reason | Explanation |
|--------|-------------|
| **Visual Appeal** | CSS makes websites attractive with colors, fonts, spacing, and layout |
| **Separation of Concerns** | CSS separates presentation from structure, making code cleaner and easier to maintain |
| **Consistency** | One CSS file can style an entire website with hundreds of pages — change it once, and the update applies everywhere |
| **Responsiveness** | CSS allows websites to adapt to different screen sizes (phones, tablets, desktops) |
| **Accessibility** | Proper styling improves readability and usability for all users, including those with disabilities |
| **Performance** | External CSS files are cached by the browser, so pages load faster on repeat visits |

**Real-Life Example:** Imagine a school uniform policy. Instead of telling each student individually what to wear every day (inline styling), the school publishes one rulebook (external CSS file). If the school changes the uniform color from blue to green, they update one document and all 500 students follow the new rule. That is the power of CSS.

---

## 3. History of CSS

CSS was created to solve the problem of mixing content and presentation in HTML. In the early days of the web, developers used HTML tags like `<font>`, `<center>`, and `bgcolor` attributes to style pages — this made HTML documents messy and hard to maintain.

### Timeline of CSS Versions

```
┌──────────────────────────────────────────────────────────────────┐
│                    CSS VERSION TIMELINE                           │
│                                                                  │
│  1996          2004            2011-Present                       │
│   │             │               │                                │
│   ▼             ▼               ▼                                │
│  CSS1          CSS2           CSS3                                │
│   │             │               │                                │
│   │ Fonts       │ Positioning   │ Flexbox, Grid                  │
│   │ Colors      │ z-index       │ Animations                     │
│   │ Margins     │ Media types   │ Transitions                    │
│   │ Borders     │ Pseudo-       │ Media Queries                  │
│   │ Text        │  elements     │ Shadows                        │
│   │  alignment  │ Overflow      │ Gradients                      │
│   │             │ Visibility    │ Custom Properties              │
│   │             │               │ (Variables)                    │
│                                                                  │
│   Basic         Intermediate    Modern & Powerful                 │
│   Styling       Layout          Layout + Animation               │
└──────────────────────────────────────────────────────────────────┘
```

### CSS Versions in Detail

| Version | Year | Key Features |
|---------|------|-------------|
| **CSS1** | 1996 | Basic fonts, colors, text properties, margins, padding, borders |
| **CSS2** | 1998 | Positioning (`absolute`, `relative`, `fixed`), `z-index`, media types, `overflow`, pseudo-elements |
| **CSS2.1** | 2004 (revised) | Bug fixes and clarifications of CSS2; became the stable standard for years |
| **CSS3** | 2011 onwards | Modular approach — Flexbox, Grid, animations, transitions, shadows, gradients, media queries, custom properties, and much more |

**Important:** CSS3 is not a single specification. Unlike CSS1 and CSS2, CSS3 is divided into independent **modules** (e.g., Selectors Module, Flexbox Module, Grid Module). Each module is developed and updated separately. This means CSS continues to evolve — there will be no "CSS4." New features are simply added as new modules under the CSS3 umbrella.

---

## 4. Three Ways to Apply CSS

There are three methods to apply CSS styles to an HTML document. Each has its own use case, advantages, and disadvantages.

### 4.1 Inline CSS (style attribute)

Inline CSS is written directly inside an HTML element using the `style` attribute. The styles apply only to that specific element.

```html
<h1 style="color: blue; font-size: 24px;">Hello World</h1>
<p style="color: gray; line-height: 1.6;">This is a paragraph.</p>
```

**When to Use:** Quick testing or one-off styles that apply to a single element only.

**Real-Life Example:** Inline CSS is like whispering dress instructions to one person at a party: "You wear red today." It only affects that one person and nobody else.

---

### 4.2 Internal CSS (style tag in head)

Internal CSS is written inside a `<style>` tag within the `<head>` section of the HTML document. The styles apply to all matching elements on that single page.

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>My Page</title>
    <style>
        h1 {
            color: blue;
            font-size: 24px;
        }
        p {
            color: gray;
            line-height: 1.6;
        }
    </style>
</head>
<body>
    <h1>Hello World</h1>
    <p>This is a paragraph.</p>
</body>
</html>
```

**When to Use:** Single-page projects, email templates, or when you need page-specific styles that should not affect other pages.

**Real-Life Example:** Internal CSS is like a poster on the classroom wall that says "Everyone in this room must wear blue." It applies to everyone in that room (page), but not to other rooms (pages).

---

### 4.3 External CSS (separate .css file — preferred)

External CSS is written in a separate `.css` file and linked to the HTML document using the `<link>` tag. This is the **industry standard and recommended approach**.

**style.css** (separate file):
```css
h1 {
    color: blue;
    font-size: 24px;
}

p {
    color: gray;
    line-height: 1.6;
}
```

**index.html**:
```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>My Page</title>
    <link rel="stylesheet" href="style.css">
</head>
<body>
    <h1>Hello World</h1>
    <p>This is a paragraph.</p>
</body>
</html>
```

**When to Use:** All real-world projects. One CSS file can style hundreds of HTML pages.

**Real-Life Example:** External CSS is like a school uniform policy document stored in the principal's office. Every student in every classroom follows the same document. If the principal changes the uniform color, it automatically applies to every student in the school.

---

### 4.4 Comparison Table: Inline vs. Internal vs. External CSS

| Feature | Inline CSS | Internal CSS | External CSS |
|---------|-----------|-------------|-------------|
| **Where it is written** | Inside the `style` attribute of an element | Inside `<style>` tag in `<head>` | In a separate `.css` file |
| **Scope** | One element only | One page only | Entire website (multiple pages) |
| **Reusability** | Not reusable | Reusable within one page | Fully reusable across all pages |
| **Separation of concerns** | No separation (HTML + CSS mixed) | Partial separation | Full separation |
| **Maintainability** | Very difficult for large projects | Moderate | Excellent |
| **Browser caching** | Not cacheable | Not cacheable | Cacheable (faster load times) |
| **Specificity priority** | Highest (overrides internal and external) | Medium | Lowest (unless specificity is higher) |
| **Best for** | Quick testing, email templates | Single-page projects | All real-world projects |
| **Recommendation** | Avoid in production | Use sparingly | **Always preferred** |

```
┌──────────────────────────────────────────────────────────────┐
│           CSS APPLICATION METHODS — PRIORITY ORDER           │
│                                                              │
│   ┌────────────────┐                                         │
│   │   Inline CSS   │  ◀── Highest Priority (overrides all)   │
│   │  style="..."   │                                         │
│   └───────┬────────┘                                         │
│           │                                                  │
│   ┌───────▼────────┐                                         │
│   │  Internal CSS  │  ◀── Medium Priority                    │
│   │  <style>...</   │                                         │
│   └───────┬────────┘                                         │
│           │                                                  │
│   ┌───────▼────────┐                                         │
│   │  External CSS  │  ◀── Lowest Priority (but best practice)│
│   │  .css file     │                                         │
│   └────────────────┘                                         │
└──────────────────────────────────────────────────────────────┘
```

---

## 5. CSS Syntax

Every CSS rule follows a specific structure. Understanding this structure is essential before writing any CSS.

### The CSS Rule Structure

```
┌──────────────────────────────────────────────────────────────┐
│                      CSS RULE ANATOMY                        │
│                                                              │
│                                                              │
│      selector {                                              │
│          property: value;     ◀── Declaration                │
│          property: value;     ◀── Declaration                │
│      }                                                       │
│                                                              │
│                                                              │
│   Example:                                                   │
│                                                              │
│      h1 {                     ◀── Selector                   │
│        ┌──────────────────┐                                  │
│        │ color: blue;     │   ◀── Property: Value            │
│        │ font-size: 24px; │   ◀── Property: Value            │
│        └──────────────────┘                                  │
│      }            ▲                                          │
│                   │                                          │
│          Declaration Block                                   │
│          (everything between { })                            │
└──────────────────────────────────────────────────────────────┘
```

### Key Terminology

| Term | Definition | Example |
|------|-----------|---------|
| **Selector** | Targets which HTML element(s) to style | `h1`, `.card`, `#header` |
| **Property** | The aspect of the element you want to change | `color`, `font-size`, `margin` |
| **Value** | The setting you want to apply to the property | `blue`, `24px`, `10px` |
| **Declaration** | A single property-value pair | `color: blue;` |
| **Declaration Block** | All declarations inside `{ }` | `{ color: blue; font-size: 24px; }` |
| **CSS Rule** | The complete selector + declaration block | `h1 { color: blue; }` |

### Syntax Rules to Remember

1. **Every declaration must end with a semicolon (`;`)**
2. **Properties and values are separated by a colon (`:`)**
3. **The declaration block is wrapped in curly braces (`{ }`)**
4. **CSS is not case-sensitive** for property names and most values, but **selectors are case-sensitive** for class and ID names
5. **Whitespace and indentation** do not affect CSS behavior but improve readability

```css
/* Correct CSS syntax */
p {
    color: red;
    font-size: 16px;
    line-height: 1.5;
}

/* Multiple selectors, same style */
h1, h2, h3 {
    color: navy;
    font-weight: bold;
}
```

### CSS Comments

CSS comments are written between `/*` and `*/`. They are ignored by the browser and are useful for documentation.

```css
/* This is a single-line comment */

/*
   This is a
   multi-line comment
*/

h1 {
    color: blue;   /* heading color */
    font-size: 32px;
}
```

---

## 6. CSS Selectors

Selectors are the most important concept in CSS. A selector tells the browser **which HTML elements** should receive the styles you define. Mastering selectors gives you precise control over the appearance of every element on a web page.

### 6.1 Element / Tag Selector

Selects **all elements** of a given HTML tag. No symbol is needed — just write the tag name.

```css
p {
    color: gray;
    font-size: 16px;
}

h1 {
    color: navy;
}
```

This applies to **every** `<p>` and **every** `<h1>` on the page.

---

### 6.2 Class Selector (.)

Selects all elements that have a specific `class` attribute. Use a **dot (`.`)** before the class name.

```html
<p class="highlight">This is highlighted.</p>
<p>This is normal.</p>
<p class="highlight">This is also highlighted.</p>
```

```css
.highlight {
    background-color: yellow;
    font-weight: bold;
}
```

**Key Points:**
- A class can be applied to **multiple elements**
- An element can have **multiple classes**: `class="highlight large"`
- Classes are **reusable** — use them for styles you want to apply to many elements

---

### 6.3 ID Selector (#)

Selects a **single element** that has a specific `id` attribute. Use a **hash (`#`)** before the ID name.

```html
<h1 id="main-title">Welcome to My Website</h1>
```

```css
#main-title {
    color: darkblue;
    text-align: center;
    border-bottom: 2px solid gray;
}
```

**Key Points:**
- An ID must be **unique** on each page — only one element can have a specific ID
- IDs have **higher specificity** than classes (more on this later)
- In real-world projects, **prefer classes over IDs** for styling. Reserve IDs for JavaScript targeting and anchor links

---

### 6.4 Universal Selector (*)

Selects **every element** on the page. Use the **asterisk (`*`)**.

```css
* {
    margin: 0;
    padding: 0;
    box-sizing: border-box;
}
```

This is commonly used as a **CSS reset** to remove default browser styles and ensure consistent styling across all browsers.

---

### 6.5 Grouping Selectors

When multiple selectors share the same styles, you can group them with **commas** to avoid repetition.

```css
/* Without grouping — repetitive */
h1 {
    color: navy;
    font-family: Arial, sans-serif;
}
h2 {
    color: navy;
    font-family: Arial, sans-serif;
}
h3 {
    color: navy;
    font-family: Arial, sans-serif;
}

/* With grouping — clean and efficient */
h1, h2, h3 {
    color: navy;
    font-family: Arial, sans-serif;
}
```

---

### 6.6 Descendant Selector (space)

Selects elements that are **nested inside** (descendants of) another element. Use a **space** between selectors.

```html
<div class="article">
    <p>This paragraph WILL be styled.</p>
    <div>
        <p>This nested paragraph WILL ALSO be styled.</p>
    </div>
</div>
<p>This paragraph will NOT be styled.</p>
```

```css
.article p {
    color: darkgray;
    line-height: 1.8;
}
```

The descendant selector selects **all** `<p>` elements inside `.article`, no matter how deeply nested they are.

---

### 6.7 Child Selector (>)

Selects elements that are **direct children** of another element. Use the **greater-than sign (`>`)**.

```html
<div class="container">
    <p>Direct child — WILL be styled.</p>
    <div>
        <p>Grandchild — will NOT be styled.</p>
    </div>
</div>
```

```css
.container > p {
    font-weight: bold;
    color: green;
}
```

Unlike the descendant selector, the child selector **only selects immediate children**, not deeper nested elements.

---

### 6.8 Attribute Selector

Selects elements based on the presence or value of an HTML attribute. Use **square brackets (`[]`)**.

```css
/* Select all elements with a "target" attribute */
a[target] {
    color: red;
}

/* Select all elements where target equals "_blank" */
a[target="_blank"] {
    text-decoration: underline;
}

/* Select all inputs of type "text" */
input[type="text"] {
    border: 1px solid gray;
    padding: 8px;
}

/* Select elements whose class starts with "btn-" */
[class^="btn-"] {
    padding: 10px 20px;
    border-radius: 4px;
}

/* Select elements whose href ends with ".pdf" */
a[href$=".pdf"] {
    color: red;
}

/* Select elements whose class contains "card" */
[class*="card"] {
    box-shadow: 0 2px 4px rgba(0, 0, 0, 0.1);
}
```

### Attribute Selector Variants

| Selector | Meaning | Example |
|----------|---------|---------|
| `[attr]` | Has the attribute | `a[target]` |
| `[attr="value"]` | Exact match | `input[type="text"]` |
| `[attr^="value"]` | Starts with | `[class^="btn-"]` |
| `[attr$="value"]` | Ends with | `a[href$=".pdf"]` |
| `[attr*="value"]` | Contains | `[class*="card"]` |

---

### 6.9 Pseudo-Classes

Pseudo-classes select elements based on their **state** or **position** in the document. They use a single **colon (`:`)**.

#### Interactive Pseudo-Classes

```css
/* When the mouse hovers over a link */
a:hover {
    color: red;
    text-decoration: underline;
}

/* When an input field is focused (clicked into) */
input:focus {
    border-color: blue;
    outline: none;
    box-shadow: 0 0 5px rgba(0, 0, 255, 0.3);
}

/* When a link is being clicked */
a:active {
    color: darkred;
}

/* A link that has already been visited */
a:visited {
    color: purple;
}
```

#### Structural Pseudo-Classes

```css
/* Select the first child of its parent */
li:first-child {
    font-weight: bold;
    color: green;
}

/* Select the last child of its parent */
li:last-child {
    color: red;
}

/* Select every odd row in a table (1st, 3rd, 5th...) */
tr:nth-child(odd) {
    background-color: #f2f2f2;
}

/* Select every even row (2nd, 4th, 6th...) */
tr:nth-child(even) {
    background-color: #ffffff;
}

/* Select the 3rd child specifically */
li:nth-child(3) {
    text-decoration: underline;
}

/* Select every 3rd child (3rd, 6th, 9th...) */
li:nth-child(3n) {
    color: blue;
}
```

### Common Pseudo-Classes Reference

| Pseudo-Class | What It Selects |
|-------------|----------------|
| `:hover` | Element when mouse is over it |
| `:focus` | Element when it is focused (e.g., input clicked) |
| `:active` | Element during the moment it is being clicked |
| `:visited` | A link that has already been visited |
| `:first-child` | The first child element of its parent |
| `:last-child` | The last child element of its parent |
| `:nth-child(n)` | The nth child element (supports formulas like `2n`, `odd`, `even`) |
| `:not(selector)` | Elements that do NOT match the given selector |
| `:first-of-type` | The first element of its type within a parent |
| `:last-of-type` | The last element of its type within a parent |

---

### 6.10 Pseudo-Elements

Pseudo-elements style **specific parts** of an element. They use a **double colon (`::`)**.

```css
/* Add content before an element */
.note::before {
    content: "Note: ";
    font-weight: bold;
    color: red;
}

/* Add content after an element */
.link::after {
    content: " >";
    color: gray;
}

/* Style the first letter of a paragraph */
p::first-letter {
    font-size: 2em;
    font-weight: bold;
    color: navy;
    float: left;
    margin-right: 4px;
}

/* Style the first line of a paragraph */
p::first-line {
    font-weight: bold;
    color: darkgray;
}

/* Style the text a user selects with their mouse */
::selection {
    background-color: yellow;
    color: black;
}
```

### Common Pseudo-Elements Reference

| Pseudo-Element | What It Styles |
|---------------|---------------|
| `::before` | Inserts content before the element's actual content |
| `::after` | Inserts content after the element's actual content |
| `::first-letter` | The first letter of the text content |
| `::first-line` | The first line of the text content |
| `::selection` | The portion of text that the user highlights |
| `::placeholder` | The placeholder text inside an input field |

**Important:** `::before` and `::after` require the `content` property to work — even if you set it to an empty string (`content: ""`).

---

### 6.11 Selector Specificity

When multiple CSS rules target the same element, the browser must decide which rule wins. This decision is based on **specificity** — a scoring system that determines the priority of CSS selectors.

```
┌──────────────────────────────────────────────────────────────┐
│              CSS SPECIFICITY HIERARCHY                        │
│                                                              │
│   HIGHEST PRIORITY                                           │
│   ┌──────────────────────────┐                               │
│   │  !important              │  Score: Overrides everything  │
│   │  (avoid using this)      │                               │
│   └────────────┬─────────────┘                               │
│                │                                             │
│   ┌────────────▼─────────────┐                               │
│   │  Inline Styles           │  Score: 1,0,0,0               │
│   │  style="color: red"     │                               │
│   └────────────┬─────────────┘                               │
│                │                                             │
│   ┌────────────▼─────────────┐                               │
│   │  ID Selectors            │  Score: 0,1,0,0               │
│   │  #header                 │                               │
│   └────────────┬─────────────┘                               │
│                │                                             │
│   ┌────────────▼─────────────┐                               │
│   │  Class / Pseudo-class /  │  Score: 0,0,1,0               │
│   │  Attribute Selectors     │                               │
│   │  .menu  :hover  [type]   │                               │
│   └────────────┬─────────────┘                               │
│                │                                             │
│   ┌────────────▼─────────────┐                               │
│   │  Element / Pseudo-       │  Score: 0,0,0,1               │
│   │  element Selectors       │                               │
│   │  p  h1  ::before         │                               │
│   └────────────┬─────────────┘                               │
│                │                                             │
│   ┌────────────▼─────────────┐                               │
│   │  Universal Selector (*)  │  Score: 0,0,0,0               │
│   │  (no specificity)        │                               │
│   └──────────────────────────┘                               │
│   LOWEST PRIORITY                                            │
└──────────────────────────────────────────────────────────────┘
```

### Specificity Scoring Examples

| Selector | Inline | IDs | Classes | Elements | Total Score |
|----------|--------|-----|---------|----------|-------------|
| `p` | 0 | 0 | 0 | 1 | 0,0,0,1 |
| `.card` | 0 | 0 | 1 | 0 | 0,0,1,0 |
| `#header` | 0 | 1 | 0 | 0 | 0,1,0,0 |
| `div p` | 0 | 0 | 0 | 2 | 0,0,0,2 |
| `.nav .link` | 0 | 0 | 2 | 0 | 0,0,2,0 |
| `#sidebar .widget h2` | 0 | 1 | 1 | 1 | 0,1,1,1 |
| `style="..."` | 1 | 0 | 0 | 0 | 1,0,0,0 |

### Specificity Rules

1. **Higher specificity always wins**, regardless of source order
2. If two selectors have **equal specificity**, the one that appears **later** in the CSS wins
3. `!important` overrides all specificity — but **avoid using it** because it makes debugging extremely difficult
4. Inline styles have the highest specificity (aside from `!important`)
5. The universal selector (`*`) has **zero specificity** and never overrides anything

```css
/* Specificity example */
p {
    color: blue;        /* Specificity: 0,0,0,1 */
}

.intro {
    color: green;       /* Specificity: 0,0,1,0 — WINS over p */
}

#welcome {
    color: red;         /* Specificity: 0,1,0,0 — WINS over .intro */
}

/* If an element is <p class="intro" id="welcome">,
   the text color will be RED because #welcome has the highest specificity */
```

---

## 7. CSS Colors

CSS provides multiple ways to define colors. Understanding each format helps you choose the right one for different situations.

### 7.1 Named Colors

CSS supports **147 predefined color names** that you can use directly.

```css
h1 {
    color: red;
}

p {
    color: steelblue;
}

body {
    background-color: whitesmoke;
}
```

**Common Named Colors:** `red`, `blue`, `green`, `yellow`, `orange`, `purple`, `pink`, `gray`, `black`, `white`, `navy`, `teal`, `coral`, `tomato`, `steelblue`, `darkslategray`, `whitesmoke`, `transparent`

**Limitation:** Named colors are limited to 147 options and do not allow fine-grained control.

---

### 7.2 Hexadecimal (#RRGGBB)

Hexadecimal (hex) is the most commonly used color format on the web. It uses a `#` followed by six characters representing Red, Green, and Blue values in base-16 (0-9 and A-F).

```
┌──────────────────────────────────────────────┐
│          HEXADECIMAL COLOR FORMAT             │
│                                              │
│              # R R G G B B                   │
│                │ │ │ │ │ │                   │
│                └─┘ └─┘ └─┘                   │
│                 │   │   │                    │
│                Red Green Blue                │
│                                              │
│   Each pair ranges from 00 (none) to         │
│   FF (maximum intensity = 255)               │
│                                              │
│   Examples:                                  │
│   #FF0000 = Pure Red                         │
│   #00FF00 = Pure Green                       │
│   #0000FF = Pure Blue                        │
│   #000000 = Black (no color)                 │
│   #FFFFFF = White (all colors at max)        │
│   #808080 = Gray (equal parts R, G, B)       │
└──────────────────────────────────────────────┘
```

```css
h1 {
    color: #FF5733;          /* Orange-red */
}

.card {
    background-color: #3498DB;  /* Bright blue */
    border: 1px solid #2C3E50;  /* Dark blue-gray */
}
```

**Shorthand:** When both characters in each pair are identical, you can use a 3-character shorthand:
- `#FF0000` can be written as `#F00`
- `#336699` can be written as `#369`
- `#FFFFFF` can be written as `#FFF`

---

### 7.3 RGB / RGBA

RGB defines colors using decimal values for Red, Green, and Blue. Each value ranges from **0 to 255**. RGBA adds an **Alpha** channel for transparency (0 = fully transparent, 1 = fully opaque).

```css
/* RGB — no transparency */
h1 {
    color: rgb(255, 87, 51);         /* Orange-red */
}

/* RGBA — with transparency */
.overlay {
    background-color: rgba(0, 0, 0, 0.5);  /* 50% transparent black */
}

.banner {
    background-color: rgba(52, 152, 219, 0.8);  /* 80% opaque blue */
}
```

**Real-Life Example:** Think of RGBA like tinted glass. RGB chooses the glass color, and the Alpha value decides how see-through the glass is. An alpha of `0.5` is like frosted glass — you can partially see through it.

---

### 7.4 HSL / HSLA

HSL stands for **Hue, Saturation, Lightness**. This format is often more intuitive for designers because it aligns with how humans think about color.

```
┌──────────────────────────────────────────────────────────────┐
│                    HSL COLOR MODEL                            │
│                                                              │
│   H (Hue)        → Color on the color wheel (0-360 degrees) │
│                     0/360 = Red                              │
│                     120   = Green                            │
│                     240   = Blue                             │
│                                                              │
│   S (Saturation)  → Intensity of the color (0%-100%)        │
│                     0%   = Gray (no color)                   │
│                     100% = Full, vivid color                 │
│                                                              │
│   L (Lightness)   → Brightness (0%-100%)                    │
│                     0%   = Black                             │
│                     50%  = Normal color                      │
│                     100% = White                             │
│                                                              │
│         0/360                                                │
│          Red                                                 │
│           |                                                  │
│   300     |     60                                           │
│  Magenta--+---Yellow                                         │
│           |                                                  │
│   240     |     120                                          │
│   Blue----+---Green                                          │
│           |                                                  │
│          180                                                 │
│          Cyan                                                │
└──────────────────────────────────────────────────────────────┘
```

```css
h1 {
    color: hsl(9, 100%, 60%);         /* Bright orange-red */
}

.muted-text {
    color: hsl(210, 20%, 50%);        /* Muted blue-gray */
}

/* HSLA — with transparency */
.card {
    background-color: hsla(210, 79%, 53%, 0.7);  /* 70% opaque blue */
}
```

**When to Use HSL:** HSL is excellent when you want to create color variations quickly. To make a color darker, decrease the Lightness. To make it muted, decrease the Saturation. The Hue stays the same.

---

### 7.5 Color Formats Comparison Table

| Format | Syntax Example | Transparency | Ease of Use | Common Usage |
|--------|---------------|-------------|------------|-------------|
| **Named** | `red`, `steelblue` | No | Very easy | Quick prototyping, simple projects |
| **Hex** | `#FF5733` | No (or #RRGGBBAA) | Moderate | Most common format on the web |
| **RGB** | `rgb(255, 87, 51)` | No | Moderate | When you need decimal color values |
| **RGBA** | `rgba(255, 87, 51, 0.5)` | Yes | Moderate | Overlays, shadows, transparent backgrounds |
| **HSL** | `hsl(9, 100%, 60%)` | No | Intuitive | Design-oriented work, creating color palettes |
| **HSLA** | `hsla(9, 100%, 60%, 0.5)` | Yes | Intuitive | Transparent design elements |

**Pro Tip:** Modern CSS also supports the newer `rgb()` and `hsl()` syntax without commas and with an optional slash for alpha:

```css
/* Modern syntax (CSS Level 4) */
color: rgb(255 87 51);           /* No commas */
color: rgb(255 87 51 / 0.5);    /* Alpha with slash */
color: hsl(9 100% 60% / 0.5);   /* HSL with alpha */
```

---

## 8. CSS Backgrounds

CSS provides powerful properties to control the background of any element — from simple solid colors to complex gradients and images.

### 8.1 background-color

Sets a solid background color for an element.

```css
body {
    background-color: #f5f5f5;
}

.card {
    background-color: white;
}

.alert {
    background-color: rgba(255, 0, 0, 0.1);   /* Light red with transparency */
}
```

---

### 8.2 background-image

Sets an image as the background of an element.

```css
.hero {
    background-image: url("images/hero-banner.jpg");
}

.pattern {
    background-image: url("https://example.com/pattern.png");
}
```

**Note:** When using `background-image`, you almost always need to set `background-repeat`, `background-position`, and `background-size` to control how the image is displayed.

---

### 8.3 background-repeat

Controls whether and how the background image repeats (tiles).

```css
.pattern {
    background-image: url("texture.png");
    background-repeat: repeat;       /* Default: tiles in both directions */
}

.banner {
    background-image: url("banner.jpg");
    background-repeat: no-repeat;    /* Image appears only once */
}

.divider {
    background-image: url("line.png");
    background-repeat: repeat-x;    /* Tiles horizontally only */
}
```

| Value | Behavior |
|-------|----------|
| `repeat` | Tiles in both X and Y directions (default) |
| `no-repeat` | Image appears only once |
| `repeat-x` | Tiles horizontally only |
| `repeat-y` | Tiles vertically only |
| `space` | Tiles with even spacing, no clipping |
| `round` | Tiles and stretches to fill without clipping |

---

### 8.4 background-position

Controls where the background image is placed within the element.

```css
.hero {
    background-image: url("hero.jpg");
    background-repeat: no-repeat;
    background-position: center center;   /* Centered both horizontally and vertically */
}

.logo {
    background-image: url("logo.png");
    background-repeat: no-repeat;
    background-position: top right;       /* Top-right corner */
}

.custom {
    background-image: url("icon.png");
    background-repeat: no-repeat;
    background-position: 20px 50px;       /* 20px from left, 50px from top */
}
```

| Value | Position |
|-------|----------|
| `center` | Center of the element |
| `top`, `bottom` | Vertical alignment |
| `left`, `right` | Horizontal alignment |
| `top left` | Top-left corner |
| `center bottom` | Bottom-center |
| `50% 50%` | Same as center center |
| `20px 30px` | Specific pixel offsets from top-left |

---

### 8.5 background-size

Controls how large the background image appears.

```css
.hero {
    background-image: url("hero.jpg");
    background-size: cover;     /* Image covers the entire element, may crop */
}

.preview {
    background-image: url("preview.jpg");
    background-size: contain;   /* Entire image is visible, may leave gaps */
}

.icon {
    background-image: url("icon.png");
    background-size: 100px 100px;   /* Exact width and height */
}
```

```
┌──────────────────────────────────────────────────────────────┐
│           background-size: cover vs. contain                 │
│                                                              │
│   COVER                          CONTAIN                     │
│   ┌──────────────────┐          ┌──────────────────┐         │
│   │ ################ │          │                  │         │
│   │ ################ │          │   ############   │         │
│   │ ###  IMAGE  #### │          │   ###  IMAGE ##  │         │
│   │ ################ │          │   ############   │         │
│   │ ################ │          │                  │         │
│   └──────────────────┘          └──────────────────┘         │
│                                                              │
│   Image fills the entire        Image fits entirely inside   │
│   container. Parts of the       the container. May leave     │
│   image may be cropped.         empty space (gaps).          │
└──────────────────────────────────────────────────────────────┘
```

| Value | Behavior |
|-------|----------|
| `cover` | Scales image to fill the entire element; may crop edges |
| `contain` | Scales image to fit entirely inside the element; may leave empty space |
| `auto` | Keeps the image's original size (default) |
| `100px 200px` | Sets exact width and height |
| `50% auto` | Sets width to 50% of the element, height scales proportionally |

---

### 8.6 background Shorthand

Instead of writing each background property separately, you can use the `background` shorthand property.

```css
/* Longhand — separate properties */
.hero {
    background-color: #333;
    background-image: url("hero.jpg");
    background-repeat: no-repeat;
    background-position: center center;
    background-size: cover;
}

/* Shorthand — all in one line */
.hero {
    background: #333 url("hero.jpg") no-repeat center center / cover;
}
```

**Shorthand order:** `background: color image repeat position / size;`

**Note:** When using the shorthand, `background-size` must come right after `background-position` and must be separated by a **forward slash (`/`)**.

---

### 8.7 CSS Gradients

Gradients are special background images that create smooth transitions between two or more colors.

#### Linear Gradient

Creates a gradient along a straight line.

```css
/* Top to bottom (default direction) */
.gradient-1 {
    background: linear-gradient(#FF5733, #3498DB);
}

/* Left to right */
.gradient-2 {
    background: linear-gradient(to right, #FF5733, #3498DB);
}

/* Diagonal — top-left to bottom-right */
.gradient-3 {
    background: linear-gradient(to bottom right, #FF5733, #FFC300, #3498DB);
}

/* Using specific angle */
.gradient-4 {
    background: linear-gradient(135deg, #667eea, #764ba2);
}

/* With color stops (control where each color starts and ends) */
.gradient-5 {
    background: linear-gradient(to right, #FF5733 0%, #FFC300 50%, #3498DB 100%);
}
```

```
┌──────────────────────────────────────────────────┐
│            LINEAR GRADIENT DIRECTIONS             │
│                                                  │
│   to top          to top right       to right    │
│      ^               ^                  -->      │
│      |              /                            │
│      |             /                             │
│                                                  │
│   to left        (center)          to right      │
│     <--                              -->         │
│                                                  │
│                    \                             │
│      |              \                            │
│      v               v                           │
│   to bottom     to bottom right   to bottom      │
│                                                  │
│   Or use degrees: 0deg = to top                  │
│                   90deg = to right               │
│                   180deg = to bottom             │
│                   270deg = to left               │
└──────────────────────────────────────────────────┘
```

#### Radial Gradient

Creates a gradient that radiates outward from a center point.

```css
/* Basic radial gradient — center outward */
.gradient-radial {
    background: radial-gradient(circle, #FF5733, #3498DB);
}

/* Elliptical gradient */
.gradient-ellipse {
    background: radial-gradient(ellipse, #FF5733, #FFC300, #3498DB);
}

/* Radial gradient from a specific position */
.gradient-position {
    background: radial-gradient(circle at top left, #FF5733, #3498DB);
}
```

**Real-Life Example:** A linear gradient is like sunrise — colors transition smoothly from one side to the other. A radial gradient is like a spotlight on a stage — the brightest color is at the center and fades outward.

---

## 9. CSS Typography

Typography controls how text appears on a web page. Good typography is essential for readability, accessibility, and the overall feel of a website.

### 9.1 font-family

Specifies the font to use for text. You should always provide **fallback fonts** in case the primary font is not available.

```css
/* Web-safe fonts with fallbacks */
body {
    font-family: Arial, Helvetica, sans-serif;
}

h1 {
    font-family: Georgia, "Times New Roman", serif;
}

code {
    font-family: "Courier New", Courier, monospace;
}
```

#### Web-Safe Fonts

These fonts are pre-installed on most operating systems and do not require any external loading:

| Font Family | Category | Example Use |
|-------------|----------|------------|
| `Arial` | Sans-serif | Body text, general use |
| `Helvetica` | Sans-serif | Clean, professional designs |
| `Verdana` | Sans-serif | Readable on screens |
| `Georgia` | Serif | Elegant headings, articles |
| `Times New Roman` | Serif | Formal documents |
| `Courier New` | Monospace | Code blocks, technical text |

#### Google Fonts

To use custom fonts beyond web-safe options, you can load fonts from **Google Fonts** (fonts.google.com).

**Step 1:** Add the `<link>` tag in your HTML `<head>`:
```html
<link href="https://fonts.googleapis.com/css2?family=Roboto:wght@300;400;700&display=swap" rel="stylesheet">
```

**Step 2:** Use the font in your CSS:
```css
body {
    font-family: "Roboto", sans-serif;
}
```

**Popular Google Fonts:** `Roboto`, `Open Sans`, `Lato`, `Montserrat`, `Poppins`, `Inter`, `Nunito`

---

### 9.2 font-size

Controls the size of text. CSS offers many units for font sizing.

```css
h1 {
    font-size: 32px;     /* Absolute size in pixels */
}

p {
    font-size: 1rem;     /* Relative to root element font size */
}

.small-text {
    font-size: 0.875em;  /* Relative to parent element font size */
}

.responsive-heading {
    font-size: 5vw;      /* 5% of viewport width — scales with screen size */
}
```

---

### 9.3 font-weight

Controls how bold or thin the text appears. Values range from **100** (thinnest) to **900** (boldest).

```css
.light {
    font-weight: 300;    /* Light */
}

.normal {
    font-weight: 400;    /* Normal (same as 'normal') */
}

.bold {
    font-weight: 700;    /* Bold (same as 'bold') */
}

.extra-bold {
    font-weight: 900;    /* Extra bold / Black */
}
```

| Value | Keyword | Appearance |
|-------|---------|-----------|
| 100 | Thin | Very light |
| 200 | Extra Light | |
| 300 | Light | Slightly lighter than normal |
| 400 | **Normal** | Default weight |
| 500 | Medium | |
| 600 | Semi Bold | |
| 700 | **Bold** | Standard bold |
| 800 | Extra Bold | |
| 900 | Black | Maximum boldness |

---

### 9.4 font-style

Controls whether text is displayed in normal, italic, or oblique style.

```css
.italic-text {
    font-style: italic;
}

.normal-text {
    font-style: normal;    /* Default */
}

.oblique-text {
    font-style: oblique;   /* Similar to italic but slanted mechanically */
}
```

---

### 9.5 text-align

Controls the horizontal alignment of text within its container.

```css
.center {
    text-align: center;
}

.right {
    text-align: right;
}

.justify {
    text-align: justify;   /* Stretches text to fill the full width of the line */
}

.left {
    text-align: left;      /* Default */
}
```

---

### 9.6 text-decoration

Adds or removes decorations from text such as underlines, overlines, and strikethroughs.

```css
a {
    text-decoration: none;           /* Remove underline from links */
}

.underline {
    text-decoration: underline;
}

.strikethrough {
    text-decoration: line-through;   /* Draws a line through the text */
}

.overline {
    text-decoration: overline;       /* Line above the text */
}

/* Advanced — color and style */
.fancy-underline {
    text-decoration: underline wavy red;
}
```

---

### 9.7 text-transform

Controls the capitalization of text without changing the HTML content.

```css
.uppercase {
    text-transform: uppercase;    /* ALL LETTERS BECOME UPPERCASE */
}

.lowercase {
    text-transform: lowercase;    /* all letters become lowercase */
}

.capitalize {
    text-transform: capitalize;   /* First Letter Of Each Word Is Capitalized */
}

.none {
    text-transform: none;         /* Default — no change */
}
```

---

### 9.8 letter-spacing and word-spacing

Control the space between individual letters and between words.

```css
.spaced-letters {
    letter-spacing: 2px;    /* 2px gap between each letter */
}

.tight-letters {
    letter-spacing: -1px;   /* Letters closer together */
}

.spaced-words {
    word-spacing: 8px;      /* 8px gap between each word */
}
```

**Real-Life Example:** `letter-spacing` is like adjusting the gaps between tiles on a Scrabble board. You can spread them apart for a spacious look or push them closer for a compact feel.

---

### 9.9 line-height

Controls the vertical space between lines of text. This is one of the most important properties for readability.

```css
p {
    line-height: 1.6;      /* 1.6 times the font size — recommended for body text */
}

h1 {
    line-height: 1.2;      /* Tighter spacing for headings */
}

.double-spaced {
    line-height: 2.0;      /* Double-spaced text */
}
```

**Best Practice:** For body text, use a `line-height` between **1.4** and **1.8** for optimal readability. Headings can use tighter values like **1.1** to **1.3**.

---

### 9.10 CSS Units Comparison Table

Understanding CSS units is critical for responsive and accessible design.

```
┌──────────────────────────────────────────────────────────────┐
│                  CSS UNIT CATEGORIES                         │
│                                                              │
│   ┌─────────────────────┐    ┌─────────────────────────┐     │
│   │   ABSOLUTE UNITS    │    │    RELATIVE UNITS       │     │
│   │                     │    │                         │     │
│   │   px  — pixels      │    │   em   — relative to    │     │
│   │   pt  — points      │    │          parent font    │     │
│   │   cm  — centimeters │    │   rem  — relative to    │     │
│   │   in  — inches      │    │          root font      │     │
│   │                     │    │   %    — relative to    │     │
│   │   Fixed size, does  │    │          parent element │     │
│   │   not scale         │    │   vw   — viewport width │     │
│   │                     │    │   vh   — viewport height│     │
│   │                     │    │                         │     │
│   │                     │    │   Scales with context   │     │
│   └─────────────────────┘    └─────────────────────────┘     │
└──────────────────────────────────────────────────────────────┘
```

| Unit | Full Name | Relative To | Example | Best For |
|------|-----------|-------------|---------|----------|
| **px** | Pixels | Nothing (absolute) | `font-size: 16px` | Borders, shadows, precise sizing |
| **em** | Em | Parent element's font size | `font-size: 1.5em` | Component-level scaling, padding, margins |
| **rem** | Root Em | Root (`<html>`) element's font size | `font-size: 1rem` | Global font sizes, spacing (most recommended) |
| **%** | Percentage | Parent element's corresponding property | `width: 50%` | Widths, responsive layouts |
| **vw** | Viewport Width | 1% of the browser window's width | `font-size: 5vw` | Responsive headings, full-width elements |
| **vh** | Viewport Height | 1% of the browser window's height | `height: 100vh` | Full-height sections, hero banners |

### How em and rem Work

```css
/* Root font size (browser default is 16px) */
html {
    font-size: 16px;
}

/* rem — always relative to the root (html) element */
h1 {
    font-size: 2rem;     /* 2 x 16px = 32px */
}

p {
    font-size: 1rem;     /* 1 x 16px = 16px */
}

/* em — relative to the parent element's font size */
.parent {
    font-size: 20px;
}

.parent .child {
    font-size: 1.5em;   /* 1.5 x 20px = 30px */
}

.parent .child .grandchild {
    font-size: 1.5em;   /* 1.5 x 30px = 45px — em compounds! */
}
```

**Important:** `em` values compound (multiply) as they nest deeper. This can cause unexpected sizing. `rem` avoids this problem by always referencing the root element. **For this reason, `rem` is generally preferred over `em` for font sizes.**

---

## 10. CSS Inheritance and the Cascade

The "C" in CSS stands for **Cascading**, which refers to the set of rules that determine which styles are applied when multiple rules target the same element.

### What Is Inheritance?

Some CSS properties are **inherited** by child elements from their parents. This means if you set a property on a parent element, its children automatically receive the same value — unless they explicitly override it.

```css
body {
    color: #333;              /* All text inside body inherits this color */
    font-family: Arial, sans-serif;   /* All text inherits this font */
}

/* The <p> and <h1> inside <body> will automatically use
   color: #333 and font-family: Arial, sans-serif
   without needing to specify it again */
```

#### Inherited vs. Non-Inherited Properties

| Inherited Properties | Non-Inherited Properties |
|---------------------|------------------------|
| `color` | `background-color` |
| `font-family` | `width`, `height` |
| `font-size` | `margin`, `padding` |
| `font-weight` | `border` |
| `line-height` | `display` |
| `text-align` | `position` |
| `letter-spacing` | `box-shadow` |
| `visibility` | `overflow` |
| `cursor` | `z-index` |

**Rule of Thumb:** Properties related to **text** are generally inherited. Properties related to **layout and box model** are generally not inherited.

**Real-Life Example:** Inheritance is like family traits. If a parent has brown hair (color), the children are born with brown hair too — unless they dye it (override it). But the parent's house (background) does not automatically belong to the children.

### The Cascade — How the Browser Decides Which Style Wins

When multiple CSS rules apply to the same element, the browser follows a strict order of priority to determine which style wins:

```
┌──────────────────────────────────────────────────────────────┐
│              THE CASCADE — ORDER OF PRIORITY                 │
│              (from highest to lowest)                        │
│                                                              │
│   1. IMPORTANCE                                              │
│      └── !important declarations override everything         │
│                                                              │
│   2. ORIGIN                                                  │
│      └── Inline styles > Internal CSS > External CSS         │
│                                                              │
│   3. SPECIFICITY                                             │
│      └── Inline > ID > Class > Element                       │
│          (see Section 6.11 for scoring details)              │
│                                                              │
│   4. SOURCE ORDER                                            │
│      └── If all else is equal, the rule that appears         │
│          LATER in the CSS file wins                          │
└──────────────────────────────────────────────────────────────┘
```

### Cascade Example

```css
/* Rule 1 — Element selector (specificity: 0,0,0,1) */
p {
    color: blue;
}

/* Rule 2 — Class selector (specificity: 0,0,1,0) */
.intro {
    color: green;
}

/* Rule 3 — ID selector (specificity: 0,1,0,0) */
#welcome {
    color: red;
}
```

```html
<p class="intro" id="welcome">What color am I?</p>
```

**Answer:** The text will be **red** because `#welcome` (ID selector) has the highest specificity among the three rules.

### The !important Rule

The `!important` flag forces a style to override all other rules, regardless of specificity.

```css
p {
    color: red !important;   /* This WILL override even inline styles */
}

#special {
    color: blue;             /* This loses to !important above */
}
```

**Warning:** Avoid using `!important` in your code. It breaks the natural flow of the cascade and makes debugging extremely difficult. If you find yourself needing `!important`, it is usually a sign that your selectors need to be restructured.

---

## 11. Summary

```
┌──────────────────────────────────────────────────────────────┐
│                  WEEK 5 — KEY TAKEAWAYS                      │
│                                                              │
│  1. CSS controls how HTML elements LOOK on the page          │
│                                                              │
│  2. Three ways to apply CSS:                                 │
│     Inline (style="") | Internal (<style>) | External (.css) │
│     Always prefer EXTERNAL CSS in real projects              │
│                                                              │
│  3. CSS Syntax:  selector { property: value; }               │
│                                                              │
│  4. Selectors target elements:                               │
│     element | .class | #id | * | [attr] | :pseudo | ::pseudo │
│                                                              │
│  5. Specificity determines which style wins:                 │
│     !important > inline > #id > .class > element             │
│                                                              │
│  6. Colors: named | #hex | rgb() | rgba() | hsl() | hsla()  │
│                                                              │
│  7. Backgrounds: color, image, repeat, position, size,       │
│     shorthand, and gradients (linear + radial)               │
│                                                              │
│  8. Typography: font-family, font-size, font-weight,         │
│     text-align, text-decoration, text-transform,             │
│     letter-spacing, line-height                              │
│                                                              │
│  9. Units: px (absolute) vs em/rem/% /vw/vh (relative)      │
│     Prefer rem for font sizes                                │
│                                                              │
│  10. Inheritance: text properties inherit; layout ones don't │
│      The cascade resolves conflicts using importance,        │
│      origin, specificity, and source order                   │
│                                                              │
│  NEXT WEEK: CSS Box Model & Layout (margin, padding,         │
│  border, width, height, display, and box-sizing)             │
└──────────────────────────────────────────────────────────────┘
```

### Quick Reference Cheat Sheet

| Concept | Syntax / Example |
|---------|-----------------|
| **External CSS link** | `<link rel="stylesheet" href="style.css">` |
| **Class selector** | `.classname { }` |
| **ID selector** | `#idname { }` |
| **Grouping** | `h1, h2, h3 { }` |
| **Descendant** | `.parent p { }` |
| **Child** | `.parent > p { }` |
| **Hover** | `a:hover { }` |
| **Before** | `.box::before { content: ""; }` |
| **Hex color** | `color: #3498DB;` |
| **RGBA** | `background: rgba(0, 0, 0, 0.5);` |
| **Gradient** | `background: linear-gradient(to right, #FF5733, #3498DB);` |
| **Google Font** | `font-family: "Roboto", sans-serif;` |
| **Font size (rem)** | `font-size: 1.125rem;` |
| **Line height** | `line-height: 1.6;` |
| **Reset** | `* { margin: 0; padding: 0; box-sizing: border-box; }` |

---

**End of Week 5 — Introduction to CSS**

*Next up: Week 6 — CSS Box Model & Layout, where you will learn about margin, padding, border, width, height, display properties, and the box-sizing concept.*
