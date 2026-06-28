# Week 14: Tailwind CSS Basics

> **Prerequisites:** HTML (Weeks 1-4), CSS fundamentals including Box Model, Flexbox, and Grid (Weeks 5-7), JavaScript (Weeks 8-12), Git & GitHub (Week 13).
>
> **Goal:** Understand the utility-first philosophy of Tailwind CSS, learn to install and configure it, master the core utility classes, and build responsive, interactive layouts without writing a single line of custom CSS.

---

## Table of Contents

1. [What Is Tailwind CSS?](#1-what-is-tailwind-css)
   - [The Utility-First Philosophy](#the-utility-first-philosophy)
   - [Real-Life Analogy](#real-life-analogy)
   - [Tailwind vs Traditional CSS vs Bootstrap](#tailwind-vs-traditional-css-vs-bootstrap)
2. [Why Tailwind CSS?](#2-why-tailwind-css)
   - [No Context Switching](#no-context-switching)
   - [Consistent Design System](#consistent-design-system)
   - [Rapid Prototyping](#rapid-prototyping)
   - [Smaller Final CSS](#smaller-final-css)
   - [Highly Customizable](#highly-customizable)
3. [Installation and Setup](#3-installation-and-setup)
   - [Method 1: CDN (Learning and Prototyping)](#method-1-cdn-learning-and-prototyping)
   - [Method 2: npm Install with Vite (Production)](#method-2-npm-install-with-vite-production)
   - [tailwind.config.js Configuration](#tailwindconfigjs-configuration)
   - [Setting Up VS Code](#setting-up-vs-code)
4. [Core Utility Classes](#4-core-utility-classes)
   - [Spacing](#spacing)
   - [Sizing](#sizing)
   - [Typography](#typography)
   - [Colors](#colors)
   - [Backgrounds and Gradients](#backgrounds-and-gradients)
   - [Borders](#borders)
   - [Shadows](#shadows)
5. [Flexbox Utilities](#5-flexbox-utilities)
6. [Grid Utilities](#6-grid-utilities)
7. [Responsive Design with Tailwind](#7-responsive-design-with-tailwind)
   - [Breakpoint Prefixes](#breakpoint-prefixes)
   - [Mobile-First Approach](#mobile-first-approach)
   - [Responsive Examples](#responsive-examples)
8. [States and Interactivity](#8-states-and-interactivity)
   - [Hover, Focus, Active, Disabled](#hover-focus-active-disabled)
   - [Group Hover](#group-hover)
   - [Child Selectors](#child-selectors-first-last-odd-even)
9. [Common Tailwind Patterns](#9-common-tailwind-patterns)
   - [Centering Content](#centering-content)
   - [Card Component](#card-component)
   - [Button Styles](#button-styles)
   - [Container and Max-Width](#container-and-max-width)
10. [Tailwind vs Writing Custom CSS -- When to Use Which?](#10-tailwind-vs-writing-custom-css--when-to-use-which)
11. [Summary and Cheat Sheet](#11-summary-and-cheat-sheet)

---

## 1. What Is Tailwind CSS?

Tailwind CSS is a **utility-first CSS framework** that provides hundreds of small, single-purpose CSS classes you apply directly in your HTML. Instead of writing custom CSS rules in a separate stylesheet, you compose designs by combining utility classes like `text-center`, `bg-blue-500`, `p-4`, and `rounded-lg` right on your elements.

### The Utility-First Philosophy

In traditional CSS, you invent class names (`.card-title`, `.sidebar-nav`) and then write the styles for them in a separate file. With Tailwind, each class does exactly **one thing**, and you build up complex designs by combining many small classes.

```
Traditional CSS Workflow:
=========================

  HTML File                        CSS File
  +-----------------------+        +---------------------------+
  | <div class="card">    |  --->  | .card {                   |
  |   <h2 class="title">  |  --->  |   padding: 16px;          |
  |     Hello             |        |   background: white;      |
  |   </h2>               |        |   border-radius: 8px;     |
  |   <p class="desc">    |  --->  |   box-shadow: 0 2px 4px;  |
  |     World             |        | }                         |
  |   </p>                |        | .title {                  |
  | </div>                |        |   font-size: 1.25rem;     |
  +-----------------------+        |   font-weight: bold;      |
                                   | }                         |
  You jump back and forth          | .desc {                   |
  between two files.               |   color: #6b7280;         |
                                   | }                         |
                                   +---------------------------+


Tailwind CSS Workflow:
=========================

  HTML File (everything in one place)
  +------------------------------------------------------+
  | <div class="p-4 bg-white rounded-lg shadow-md">      |
  |   <h2 class="text-xl font-bold">                     |
  |     Hello                                            |
  |   </h2>                                              |
  |   <p class="text-gray-500">                          |
  |     World                                            |
  |   </p>                                              |
  | </div>                                               |
  +------------------------------------------------------+

  No separate CSS file needed.
  You read the HTML and immediately know the styling.
```

### Real-Life Analogy

Think of it this way:

- **Traditional CSS** is like painting a wall from scratch. You go to the store, buy base pigments, mix them yourself in a bucket to get the exact shade you want, then apply it with a brush. You have total control, but it takes time and effort every single time.

- **Tailwind CSS** is like having a wall of pre-mixed paint cans, each clearly labeled: "Red-500", "Large-Brush", "Rounded-Edges", "Shadow-Medium". You walk up, grab the cans you need, and apply them directly. No mixing, no guessing, no cleanup. You can still get any result you want, but the building blocks are already prepared.

- **Bootstrap** is like hiring a painter who comes with a catalog of pre-designed rooms. You pick "Living Room Style A" or "Modern Office Style B" and the painter does it all. It looks polished, but every room looks similar, and customizing beyond the catalog is difficult.

### Tailwind vs Traditional CSS vs Bootstrap

| Feature                    | Traditional CSS       | Bootstrap              | Tailwind CSS            |
| -------------------------- | --------------------- | ---------------------- | ----------------------- |
| **Approach**               | Write custom rules    | Pre-built components   | Utility classes         |
| **File organization**      | Separate CSS files    | Link Bootstrap CSS     | Classes in HTML         |
| **Learning curve**         | Must learn CSS deeply | Learn component names  | Learn utility names     |
| **Customization**          | Unlimited but slow    | Limited without hacks  | Unlimited and fast      |
| **Design consistency**     | Manual discipline     | Enforced by framework  | Enforced by design tokens |
| **Final CSS size**         | Can grow very large   | Large (full framework) | Tiny (unused styles purged) |
| **Component look**         | Unique per project    | Generic Bootstrap look | Unique per project      |
| **Responsive design**      | Write media queries   | Grid classes (col-md-6)| Prefix classes (md:w-1/2) |
| **Speed of development**   | Slower                | Fast for prototypes    | Very fast               |
| **Best for**               | Full control projects | Quick admin dashboards | Modern production apps  |

---

## 2. Why Tailwind CSS?

### No Context Switching

With traditional CSS, you constantly jump between your HTML file and your CSS file. You write a class name in HTML, switch to CSS to define it, switch back to HTML to check the result, switch to CSS to adjust. This back-and-forth is mentally expensive.

With Tailwind, everything lives in your HTML. You see the element and its styles together.

```
Context Switching with Traditional CSS:
========================================

  [HTML file]  --switch-->  [CSS file]  --switch-->  [HTML file]  --switch-->  [CSS file]
      |                        |                        |                        |
  Write class name       Write styles            Check result             Adjust styles
      |                        |                        |                        |
      +--- Mental overhead ----+--- Mental overhead ----+--- Mental overhead ----+


With Tailwind CSS:
==================

  [HTML file]
      |
  Write classes + see styles immediately
      |
  Done.
```

### Consistent Design System

Tailwind provides a pre-defined set of values for spacing, colors, font sizes, and more. Instead of one developer using `padding: 14px` and another using `padding: 1.1rem`, everyone uses `p-3` (12px) or `p-4` (16px). The design system is enforced automatically.

```
Without Tailwind (inconsistent):          With Tailwind (consistent):
  Developer A: padding: 14px;              Developer A: p-4  (16px)
  Developer B: padding: 1.1rem;            Developer B: p-4  (16px)
  Developer C: padding: 15px;              Developer C: p-4  (16px)
```

### Rapid Prototyping

Need a button? Instead of creating a CSS file, writing a `.btn` class, and linking it, you write one line:

```html
<button class="bg-blue-500 text-white px-4 py-2 rounded hover:bg-blue-600">
  Click Me
</button>
```

That is a fully styled, hover-responsive button in a single HTML element.

### Smaller Final CSS

Traditional CSS files grow endlessly. You add styles but rarely remove old ones. Over months, your CSS file might be 200 KB of mostly unused rules.

Tailwind uses a **purge** mechanism. During the production build, it scans your HTML files, finds every Tailwind class you actually used, and removes everything else. The result is often a CSS file under 10 KB.

```
Traditional CSS over time:
==========================

  Month 1:  [====]              20 KB
  Month 3:  [============]      60 KB
  Month 6:  [====================]  100 KB
  Month 12: [================================]  200 KB  (50%+ unused)


Tailwind CSS (purged for production):
=====================================

  Any stage: [==]  5-10 KB  (only what you use)
```

### Highly Customizable

Tailwind is not opinionated about how your site should look. It gives you tools, not templates. Through the `tailwind.config.js` file, you can customize every color, spacing value, font, breakpoint, and more to match your brand or design system.

---

## 3. Installation and Setup

### Method 1: CDN (Learning and Prototyping)

The fastest way to start using Tailwind is with a CDN link. This is ideal for learning and quick experiments, but **not recommended for production** because it loads the entire Tailwind library (no purging).

```html
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>Tailwind CDN Demo</title>
  <script src="https://cdn.tailwindcss.com"></script>
</head>
<body class="bg-gray-100 min-h-screen">

  <div class="max-w-md mx-auto mt-10 p-6 bg-white rounded-lg shadow-md">
    <h1 class="text-2xl font-bold text-gray-800">Hello Tailwind!</h1>
    <p class="mt-2 text-gray-600">This is styled entirely with utility classes.</p>
  </div>

</body>
</html>
```

Save this as an HTML file, open it in your browser, and you will see a styled card immediately. No build tools, no terminal commands.

### Method 2: npm Install with Vite (Production)

For real projects, install Tailwind via npm. Vite is a fast, modern build tool that works perfectly with Tailwind.

**Step 1: Create a Vite project**

```bash
npm create vite@latest my-tailwind-project -- --template vanilla
cd my-tailwind-project
npm install
```

**Step 2: Install Tailwind CSS and its dependencies**

```bash
npm install -D tailwindcss @tailwindcss/vite
```

**Step 3: Configure the Vite plugin**

Open `vite.config.js` and add the Tailwind plugin:

```js
// vite.config.js
import { defineConfig } from 'vite';
import tailwindcss from '@tailwindcss/vite';

export default defineConfig({
  plugins: [
    tailwindcss(),
  ],
});
```

**Step 4: Import Tailwind in your CSS**

Open your main CSS file (e.g., `src/style.css`) and add:

```css
@import "tailwindcss";
```

**Step 5: Start the development server**

```bash
npm run dev
```

Your project is now ready. Any Tailwind class you use in your HTML will be compiled into optimized CSS automatically.

```
Project Structure:
==================

  my-tailwind-project/
  +-- index.html
  +-- package.json
  +-- vite.config.js
  +-- src/
  |   +-- main.js
  |   +-- style.css          <-- @import "tailwindcss"
  +-- node_modules/
  +-- public/
```

### tailwind.config.js Configuration

For deeper customization you can create a `tailwind.config.js` file in your project root. This file lets you extend or override Tailwind's default design tokens.

```js
// tailwind.config.js
/** @type {import('tailwindcss').Config} */
export default {
  content: [
    "./index.html",
    "./src/**/*.{js,ts,jsx,tsx,html}",
  ],
  theme: {
    extend: {
      // Add custom colors
      colors: {
        brand: {
          light: '#e0f2fe',
          DEFAULT: '#0284c7',
          dark: '#075985',
        },
      },
      // Add custom fonts
      fontFamily: {
        heading: ['Poppins', 'sans-serif'],
        body: ['Inter', 'sans-serif'],
      },
      // Add custom spacing
      spacing: {
        '18': '4.5rem',
        '88': '22rem',
      },
    },
  },
  plugins: [],
};
```

Now you can use `bg-brand`, `text-brand-dark`, `font-heading`, and `p-18` in your HTML.

| Config Section | What It Does                                  | Example                        |
| -------------- | --------------------------------------------- | ------------------------------ |
| `content`      | Tells Tailwind which files to scan for classes | `"./src/**/*.{js,html}"`       |
| `theme.extend` | Adds new values without removing defaults      | Custom colors, fonts, spacing  |
| `theme`        | Completely overrides default values             | Replace all colors with yours  |
| `plugins`      | Adds third-party or custom plugins              | `@tailwindcss/forms`           |

### Setting Up VS Code

Install the **Tailwind CSS IntelliSense** extension by the Tailwind Labs team. This gives you:

- **Autocomplete** -- Start typing a class name (e.g., `bg-`) and see all matching options with color previews
- **Linting** -- Warns you about conflicting or invalid class names
- **Hover preview** -- Hover over a Tailwind class to see the exact CSS it generates
- **Class sorting** -- Automatically sorts classes in a consistent order (with Prettier plugin)

```
VS Code Setup Checklist:
=========================

  [x] Install "Tailwind CSS IntelliSense" extension
  [x] Install "PostCSS Language Support" extension (for syntax highlighting)
  [ ] Optional: Install "Prettier" + "prettier-plugin-tailwindcss" for class sorting
```

To install the Prettier plugin for automatic class sorting:

```bash
npm install -D prettier prettier-plugin-tailwindcss
```

Create a `.prettierrc` file:

```json
{
  "plugins": ["prettier-plugin-tailwindcss"]
}
```

---

## 4. Core Utility Classes

Tailwind provides utility classes for nearly every CSS property. This section covers the most commonly used ones.

### Spacing

Tailwind uses a consistent spacing scale where each unit equals **4px** (0.25rem). So `p-1` is 4px, `p-2` is 8px, `p-4` is 16px, and so on.

```
Tailwind Spacing Scale:
========================

  Class    Value       Pixels
  -----    --------    ------
  p-0      0           0px
  p-1      0.25rem     4px
  p-2      0.5rem      8px
  p-3      0.75rem     12px
  p-4      1rem        16px
  p-5      1.25rem     20px
  p-6      1.5rem      24px
  p-8      2rem        32px
  p-10     2.5rem      40px
  p-12     3rem        48px
  p-16     4rem        64px
  p-20     5rem        80px
```

**Padding classes:**

| Class       | What It Does                              | CSS Equivalent                          |
| ----------- | ----------------------------------------- | --------------------------------------- |
| `p-4`       | Padding on all four sides                 | `padding: 1rem;`                        |
| `px-4`      | Padding left and right (x-axis)           | `padding-left: 1rem; padding-right: 1rem;` |
| `py-4`      | Padding top and bottom (y-axis)           | `padding-top: 1rem; padding-bottom: 1rem;` |
| `pt-4`      | Padding top only                          | `padding-top: 1rem;`                    |
| `pr-4`      | Padding right only                        | `padding-right: 1rem;`                  |
| `pb-4`      | Padding bottom only                       | `padding-bottom: 1rem;`                 |
| `pl-4`      | Padding left only                         | `padding-left: 1rem;`                   |

**Margin classes follow the same pattern:** `m-4`, `mx-auto`, `my-2`, `mt-6`, `mb-8`, etc.

**Special margin values:**

| Class       | What It Does                              |
| ----------- | ----------------------------------------- |
| `mx-auto`   | Centers a block element horizontally      |
| `-mt-4`     | Negative top margin (-1rem)               |
| `space-x-4` | Adds horizontal space between children    |
| `space-y-4` | Adds vertical space between children      |

```html
<!-- Horizontal spacing between child elements -->
<div class="flex space-x-4">
  <div>Item 1</div>
  <div>Item 2</div>
  <div>Item 3</div>
</div>

<!-- Vertical spacing between child elements -->
<div class="space-y-4">
  <p>Paragraph 1</p>
  <p>Paragraph 2</p>
  <p>Paragraph 3</p>
</div>
```

### Sizing

```
Sizing Utilities Overview:
===========================

  Width:                         Height:
  +---------+------------------+ +---------+------------------+
  | Class   | CSS              | | Class   | CSS              |
  +---------+------------------+ +---------+------------------+
  | w-full  | width: 100%      | | h-full  | height: 100%     |
  | w-1/2   | width: 50%       | | h-screen| height: 100vh    |
  | w-1/3   | width: 33.33%    | | h-64    | height: 16rem    |
  | w-1/4   | width: 25%       | | h-auto  | height: auto     |
  | w-screen| width: 100vw     | | min-h-screen | min-h: 100vh|
  | w-auto  | width: auto      | | max-h-96| max-height: 24rem|
  | w-64    | width: 16rem     | |         |                  |
  | max-w-lg| max-width: 32rem | |         |                  |
  | min-w-0 | min-width: 0     | |         |                  |
  +---------+------------------+ +---------+------------------+
```

**Common sizing patterns:**

```html
<!-- Full-width container with max-width -->
<div class="w-full max-w-lg mx-auto">
  Centered content with a maximum width of 32rem.
</div>

<!-- Full-screen height layout -->
<div class="min-h-screen bg-gray-100">
  This div is at least as tall as the viewport.
</div>

<!-- Fractional widths for columns -->
<div class="flex">
  <div class="w-1/3 bg-blue-200">One Third</div>
  <div class="w-2/3 bg-blue-400">Two Thirds</div>
</div>
```

### Typography

Tailwind provides comprehensive text styling utilities.

| Class             | CSS Equivalent                | Description                  |
| ----------------- | ----------------------------- | ---------------------------- |
| `text-xs`         | `font-size: 0.75rem;`        | Extra small text             |
| `text-sm`         | `font-size: 0.875rem;`       | Small text                   |
| `text-base`       | `font-size: 1rem;`           | Base text (default)          |
| `text-lg`         | `font-size: 1.125rem;`       | Large text                   |
| `text-xl`         | `font-size: 1.25rem;`        | Extra large text             |
| `text-2xl`        | `font-size: 1.5rem;`         | 2x large text               |
| `text-3xl`        | `font-size: 1.875rem;`       | 3x large text               |
| `text-4xl`        | `font-size: 2.25rem;`        | 4x large text               |
| `font-thin`       | `font-weight: 100;`          | Thin weight                  |
| `font-light`      | `font-weight: 300;`          | Light weight                 |
| `font-normal`     | `font-weight: 400;`          | Normal weight                |
| `font-medium`     | `font-weight: 500;`          | Medium weight                |
| `font-semibold`   | `font-weight: 600;`          | Semi-bold weight             |
| `font-bold`       | `font-weight: 700;`          | Bold weight                  |
| `font-extrabold`  | `font-weight: 800;`          | Extra bold weight            |
| `italic`          | `font-style: italic;`        | Italic text                  |
| `uppercase`       | `text-transform: uppercase;` | UPPERCASE TEXT               |
| `lowercase`       | `text-transform: lowercase;` | lowercase text               |
| `capitalize`      | `text-transform: capitalize;`| Capitalize Each Word         |
| `text-left`       | `text-align: left;`          | Left-aligned text            |
| `text-center`     | `text-align: center;`        | Centered text                |
| `text-right`      | `text-align: right;`         | Right-aligned text           |
| `tracking-wide`   | `letter-spacing: 0.025em;`   | Wide letter spacing          |
| `tracking-wider`  | `letter-spacing: 0.05em;`    | Wider letter spacing         |
| `leading-relaxed` | `line-height: 1.625;`        | Relaxed line height          |
| `leading-loose`   | `line-height: 2;`            | Loose line height            |

```html
<!-- Typography example -->
<h1 class="text-4xl font-bold tracking-wide uppercase text-center">
  Welcome to Our Site
</h1>
<p class="text-lg text-gray-600 leading-relaxed mt-4">
  This paragraph has large text, gray color, relaxed line height,
  and a top margin. All defined with utility classes.
</p>
```

### Colors

Tailwind ships with a carefully crafted color palette. Each color has shades from 50 (lightest) to 950 (darkest).

```
Tailwind Color Palette (Simplified):
======================================

  Shade:    50     100    200    300    400    500    600    700    800    900    950
            |      |      |      |      |      |      |      |      |      |      |
  gray:   [.  ] [.   ] [..  ] [... ] [....] [.....] [.... ] [... ] [..  ] [.   ] [.  ]
          light -----------------------------------------> dark

  red:    #fef2f2  ...  #fecaca  ...  #f87171  #ef4444  #dc2626  ...  #991b1b  ...  #450a0a
  blue:   #eff6ff  ...  #bfdbfe  ...  #60a5fa  #3b82f6  #2563eb  ...  #1e3a8a  ...  #172554
  green:  #f0fdf4  ...  #bbf7d0  ...  #4ade80  #22c55e  #16a34a  ...  #166534  ...  #052e16

  Available colors:
  slate, gray, zinc, neutral, stone,
  red, orange, amber, yellow, lime, green, emerald, teal,
  cyan, sky, blue, indigo, violet, purple, fuchsia, pink, rose
```

**How to use colors:**

| Pattern              | What It Styles        | Example                  |
| -------------------- | --------------------- | ------------------------ |
| `text-{color}-{shade}` | Text color           | `text-red-500`           |
| `bg-{color}-{shade}`   | Background color     | `bg-blue-200`            |
| `border-{color}-{shade}` | Border color       | `border-gray-300`        |
| `ring-{color}-{shade}`   | Ring/outline color | `ring-indigo-500`        |
| `placeholder-{color}-{shade}` | Placeholder text | `placeholder-gray-400` |

```html
<!-- Color examples -->
<div class="bg-blue-100 text-blue-800 border border-blue-300 p-4 rounded">
  This is an info box with blue theme.
</div>

<div class="bg-red-100 text-red-800 border border-red-300 p-4 rounded">
  This is an error box with red theme.
</div>

<div class="bg-green-100 text-green-800 border border-green-300 p-4 rounded">
  This is a success box with green theme.
</div>
```

### Backgrounds and Gradients

Tailwind makes CSS gradients simple with utility classes.

```html
<!-- Solid background -->
<div class="bg-blue-500 text-white p-6">
  Solid blue background.
</div>

<!-- Gradient from left to right -->
<div class="bg-gradient-to-r from-blue-500 to-purple-500 text-white p-6 rounded-lg">
  Blue to purple gradient.
</div>

<!-- Gradient with a middle stop -->
<div class="bg-gradient-to-r from-green-400 via-blue-500 to-purple-600 text-white p-6 rounded-lg">
  Three-color gradient with a via stop.
</div>

<!-- Gradient directions -->
<!-- bg-gradient-to-r   = left to right    -->
<!-- bg-gradient-to-l   = right to left    -->
<!-- bg-gradient-to-t   = bottom to top    -->
<!-- bg-gradient-to-b   = top to bottom    -->
<!-- bg-gradient-to-br  = top-left to bottom-right -->
<!-- bg-gradient-to-tr  = bottom-left to top-right -->
```

```
Gradient Direction Reference:
==============================

  bg-gradient-to-tl    bg-gradient-to-t    bg-gradient-to-tr
         \                    |                   /
          \                   |                  /
           +------------------+------------------+
           |                                     |
  to-l  -- |            ELEMENT                  | -- to-r
           |                                     |
           +------------------+------------------+
          /                   |                  \
         /                    |                   \
  bg-gradient-to-bl    bg-gradient-to-b    bg-gradient-to-br
```

### Borders

| Class          | CSS Equivalent                    | Description                |
| -------------- | --------------------------------- | -------------------------- |
| `border`       | `border-width: 1px;`             | 1px border on all sides    |
| `border-2`     | `border-width: 2px;`             | 2px border                 |
| `border-4`     | `border-width: 4px;`             | 4px border                 |
| `border-t`     | `border-top-width: 1px;`         | Top border only            |
| `border-b-2`   | `border-bottom-width: 2px;`      | 2px bottom border          |
| `border-red-500` | `border-color: #ef4444;`        | Red border color           |
| `rounded`      | `border-radius: 0.25rem;`        | Slight rounding            |
| `rounded-md`   | `border-radius: 0.375rem;`       | Medium rounding            |
| `rounded-lg`   | `border-radius: 0.5rem;`         | Large rounding             |
| `rounded-xl`   | `border-radius: 0.75rem;`        | Extra large rounding       |
| `rounded-2xl`  | `border-radius: 1rem;`           | 2x large rounding          |
| `rounded-full` | `border-radius: 9999px;`         | Fully circular             |
| `rounded-t-lg` | Top corners only rounded          | Top-left and top-right     |

```
Border Radius Visual:
======================

  rounded-none      rounded         rounded-lg      rounded-full
  +----------+     /----------\    /----------\       /------\
  |          |    |            |  |            |     /        \
  |          |    |            |  |            |    |          |
  |          |    |            |  |            |     \        /
  +----------+     \----------/    \----------/       \------/
```

```html
<!-- Circle avatar -->
<img class="w-16 h-16 rounded-full border-2 border-gray-300"
     src="avatar.jpg" alt="User avatar">

<!-- Card with top-rounded corners -->
<div class="rounded-t-lg bg-blue-500 text-white p-4">
  Card Header
</div>
<div class="border border-t-0 border-gray-200 p-4">
  Card Body
</div>
```

### Shadows

| Class          | Effect                         | Use Case                      |
| -------------- | ------------------------------ | ----------------------------- |
| `shadow-sm`    | Very subtle shadow             | Subtle depth                  |
| `shadow`       | Small shadow                   | Cards, buttons                |
| `shadow-md`    | Medium shadow                  | Dropdown menus                |
| `shadow-lg`    | Large shadow                   | Modals, popovers              |
| `shadow-xl`    | Extra large shadow             | Prominent floating elements   |
| `shadow-2xl`   | Maximum shadow                 | Hero sections, overlays       |
| `shadow-inner` | Inset shadow                   | Input fields, pressed buttons |
| `shadow-none`  | No shadow                      | Remove shadow on hover/focus  |

```
Shadow Depth Visual:
=====================

  shadow-sm           shadow-md           shadow-xl
  +----------+        +----------+        +----------+
  |          |        |          |        |          |
  |  Card    |        |  Card    |        |  Card    |
  |          |        |          |        |          |
  +----------+        +----------+        +----------+
   \__________\        \\__________\\       \\\__________\\\
     barely             noticeable            prominent
     visible            elevation             floating
```

```html
<!-- Shadow examples -->
<div class="shadow-sm p-4 bg-white rounded">Small shadow</div>
<div class="shadow-md p-4 bg-white rounded">Medium shadow</div>
<div class="shadow-xl p-4 bg-white rounded">Extra large shadow</div>
```

---

## 5. Flexbox Utilities

You already know Flexbox from vanilla CSS. Tailwind gives you utility classes for every Flexbox property. No need to write `display: flex; justify-content: center; align-items: center;` -- just use `flex justify-center items-center`.

| Class              | CSS Equivalent                       | Description                        |
| ------------------ | ------------------------------------ | ---------------------------------- |
| `flex`             | `display: flex;`                     | Enable Flexbox                     |
| `inline-flex`      | `display: inline-flex;`              | Inline Flexbox                     |
| `flex-row`         | `flex-direction: row;`               | Horizontal direction (default)     |
| `flex-col`         | `flex-direction: column;`            | Vertical direction                 |
| `flex-row-reverse` | `flex-direction: row-reverse;`       | Reversed horizontal                |
| `flex-col-reverse` | `flex-direction: column-reverse;`    | Reversed vertical                  |
| `flex-wrap`        | `flex-wrap: wrap;`                   | Allow items to wrap                |
| `flex-nowrap`      | `flex-wrap: nowrap;`                 | Prevent wrapping (default)         |
| `justify-start`    | `justify-content: flex-start;`       | Pack items to the start            |
| `justify-center`   | `justify-content: center;`           | Center items on main axis          |
| `justify-end`      | `justify-content: flex-end;`         | Pack items to the end              |
| `justify-between`  | `justify-content: space-between;`    | Equal space between items          |
| `justify-around`   | `justify-content: space-around;`     | Equal space around items           |
| `justify-evenly`   | `justify-content: space-evenly;`     | Equal space including edges        |
| `items-start`      | `align-items: flex-start;`           | Align items to the top             |
| `items-center`     | `align-items: center;`               | Center items on cross axis         |
| `items-end`        | `align-items: flex-end;`             | Align items to the bottom          |
| `items-stretch`    | `align-items: stretch;`              | Stretch items to fill (default)    |
| `gap-4`            | `gap: 1rem;`                         | Gap between all items              |
| `gap-x-2`          | `column-gap: 0.5rem;`               | Horizontal gap only                |
| `gap-y-4`          | `row-gap: 1rem;`                     | Vertical gap only                  |
| `flex-1`           | `flex: 1 1 0%;`                      | Grow and shrink equally            |
| `flex-grow`        | `flex-grow: 1;`                      | Allow item to grow                 |
| `flex-shrink`      | `flex-shrink: 1;`                    | Allow item to shrink               |
| `flex-shrink-0`    | `flex-shrink: 0;`                    | Prevent item from shrinking        |

```html
<!-- Navigation bar with Flexbox -->
<nav class="flex justify-between items-center bg-white shadow px-6 py-4">
  <div class="text-xl font-bold">MyBrand</div>
  <div class="flex gap-6">
    <a href="#" class="text-gray-700 hover:text-blue-500">Home</a>
    <a href="#" class="text-gray-700 hover:text-blue-500">About</a>
    <a href="#" class="text-gray-700 hover:text-blue-500">Contact</a>
  </div>
</nav>
```

```
Flexbox justify-content Visual:
================================

  justify-start:      [A][B][C]                     
  justify-center:          [A][B][C]               
  justify-end:                          [A][B][C]  
  justify-between:    [A]      [B]      [C]        
  justify-around:      [A]    [B]    [C]           
  justify-evenly:     [A]   [B]   [C]              


  items-start:        [A]  [B ]  [C  ]       (top-aligned)
                      
  items-center:            [A]               (vertically centered)
                      [B ]
                           [C  ]

  items-end:                          [A]    (bottom-aligned)
                                [B ]
                           [C  ]
```

```html
<!-- Sidebar + Content layout -->
<div class="flex min-h-screen">
  <aside class="w-64 bg-gray-800 text-white p-4 flex-shrink-0">
    Sidebar
  </aside>
  <main class="flex-1 bg-gray-100 p-6">
    Main Content Area
  </main>
</div>

<!-- Evenly distributed columns -->
<div class="flex gap-4">
  <div class="flex-1 bg-blue-100 p-4 rounded">Column 1</div>
  <div class="flex-1 bg-blue-200 p-4 rounded">Column 2</div>
  <div class="flex-1 bg-blue-300 p-4 rounded">Column 3</div>
</div>
```

---

## 6. Grid Utilities

CSS Grid in Tailwind is just as powerful as writing it by hand, but far faster to type.

| Class            | CSS Equivalent                          | Description                    |
| ---------------- | --------------------------------------- | ------------------------------ |
| `grid`           | `display: grid;`                        | Enable Grid layout             |
| `grid-cols-1`    | `grid-template-columns: repeat(1, 1fr)` | 1 column                      |
| `grid-cols-2`    | `grid-template-columns: repeat(2, 1fr)` | 2 equal columns               |
| `grid-cols-3`    | `grid-template-columns: repeat(3, 1fr)` | 3 equal columns               |
| `grid-cols-4`    | `grid-template-columns: repeat(4, 1fr)` | 4 equal columns               |
| `grid-cols-12`   | `grid-template-columns: repeat(12, 1fr)`| 12-column layout              |
| `grid-rows-2`    | `grid-template-rows: repeat(2, 1fr)`    | 2 equal rows                  |
| `grid-rows-3`    | `grid-template-rows: repeat(3, 1fr)`    | 3 equal rows                  |
| `col-span-2`     | `grid-column: span 2 / span 2;`         | Item spans 2 columns          |
| `col-span-full`  | `grid-column: 1 / -1;`                  | Item spans all columns        |
| `row-span-2`     | `grid-row: span 2 / span 2;`            | Item spans 2 rows             |
| `gap-4`          | `gap: 1rem;`                            | Gap between grid items        |
| `gap-x-4`        | `column-gap: 1rem;`                     | Horizontal gap only           |
| `gap-y-2`        | `row-gap: 0.5rem;`                      | Vertical gap only             |

```html
<!-- Basic 3-column grid -->
<div class="grid grid-cols-3 gap-4">
  <div class="bg-blue-200 p-4 rounded">Item 1</div>
  <div class="bg-blue-200 p-4 rounded">Item 2</div>
  <div class="bg-blue-200 p-4 rounded">Item 3</div>
  <div class="bg-blue-200 p-4 rounded">Item 4</div>
  <div class="bg-blue-200 p-4 rounded">Item 5</div>
  <div class="bg-blue-200 p-4 rounded">Item 6</div>
</div>
```

```
3-Column Grid Visualization:
==============================

  +-------------+  +-------------+  +-------------+
  |   Item 1    |  |   Item 2    |  |   Item 3    |
  +-------------+  +-------------+  +-------------+
       gap               gap
  +-------------+  +-------------+  +-------------+
  |   Item 4    |  |   Item 5    |  |   Item 6    |
  +-------------+  +-------------+  +-------------+
```

```html
<!-- Dashboard layout with spanning -->
<div class="grid grid-cols-4 gap-4">
  <div class="col-span-4 bg-gray-800 text-white p-4 rounded">
    Header (spans all 4 columns)
  </div>
  <div class="col-span-1 row-span-2 bg-gray-200 p-4 rounded">
    Sidebar (spans 2 rows)
  </div>
  <div class="col-span-3 bg-white p-4 rounded border">
    Main Content
  </div>
  <div class="col-span-3 bg-white p-4 rounded border">
    Additional Content
  </div>
  <div class="col-span-4 bg-gray-800 text-white p-4 rounded">
    Footer (spans all 4 columns)
  </div>
</div>
```

```
Dashboard Layout Visualization:
================================

  +---------------------------------------------------+
  |              Header (col-span-4)                   |
  +----------+----------------------------------------+
  |          |        Main Content                     |
  | Sidebar  |        (col-span-3)                     |
  | (row-    +----------------------------------------+
  |  span-2) |        Additional Content               |
  |          |        (col-span-3)                     |
  +----------+----------------------------------------+
  |              Footer (col-span-4)                   |
  +---------------------------------------------------+
```

---

## 7. Responsive Design with Tailwind

Tailwind uses a **mobile-first** responsive design approach. Every utility class applies to all screen sizes by default. You then add breakpoint prefixes to override styles at larger screens.

### Breakpoint Prefixes

| Prefix | Minimum Width | CSS Equivalent                | Typical Device    |
| ------ | ------------- | ----------------------------- | ----------------- |
| (none) | 0px           | Default (applies everywhere)  | All devices       |
| `sm:`  | 640px         | `@media (min-width: 640px)`   | Small phones      |
| `md:`  | 768px         | `@media (min-width: 768px)`   | Tablets           |
| `lg:`  | 1024px        | `@media (min-width: 1024px)`  | Laptops           |
| `xl:`  | 1280px        | `@media (min-width: 1280px)`  | Desktops          |
| `2xl:` | 1536px        | `@media (min-width: 1536px)`  | Large desktops    |

```
Breakpoints on a Screen Width Scale:
======================================

  0px        640px       768px       1024px      1280px      1536px
  |           |           |           |           |           |
  |  (default)|   sm:     |   md:     |   lg:     |   xl:     |   2xl:
  |           |           |           |           |           |
  |<- Mobile->|<- Small ->|<- Tablet->|<- Laptop->|<-Desktop->|<- Large ->
  |           |  Phones   |           |           |           |  Desktop
  |           |           |           |           |           |
```

### Mobile-First Approach

The key insight: **write styles for mobile first, then add overrides for larger screens.**

Do NOT think: "I will style for desktop, then make it responsive." Instead think: "I will style for mobile, then enhance for bigger screens."

```
Mobile-First Thinking:
=======================

  WRONG approach (desktop-first):
  "Hide sidebar on mobile"  -->  You end up fighting your own CSS

  RIGHT approach (mobile-first):
  "Show sidebar on desktop"  -->  Mobile is the default, desktop is the enhancement


  class="hidden md:block"

  This means:
    - By default (mobile): hidden
    - At md (768px) and above: block (visible)
```

### Responsive Examples

**Example 1: Responsive grid columns**

```html
<div class="grid grid-cols-1 md:grid-cols-2 lg:grid-cols-3 gap-4">
  <div class="bg-white p-4 rounded shadow">Card 1</div>
  <div class="bg-white p-4 rounded shadow">Card 2</div>
  <div class="bg-white p-4 rounded shadow">Card 3</div>
  <div class="bg-white p-4 rounded shadow">Card 4</div>
  <div class="bg-white p-4 rounded shadow">Card 5</div>
  <div class="bg-white p-4 rounded shadow">Card 6</div>
</div>
```

```
Responsive Grid Behavior:
==========================

  Mobile (< 768px):              Tablet (>= 768px):          Desktop (>= 1024px):
  grid-cols-1                    md:grid-cols-2               lg:grid-cols-3

  +-------------------+          +---------+---------+        +------+------+------+
  |      Card 1       |          | Card 1  | Card 2  |        |Card 1|Card 2|Card 3|
  +-------------------+          +---------+---------+        +------+------+------+
  |      Card 2       |          | Card 3  | Card 4  |        |Card 4|Card 5|Card 6|
  +-------------------+          +---------+---------+        +------+------+------+
  |      Card 3       |          | Card 5  | Card 6  |
  +-------------------+          +---------+---------+
  |      Card 4       |
  +-------------------+
  |      Card 5       |
  +-------------------+
  |      Card 6       |
  +-------------------+
```

**Example 2: Responsive typography and spacing**

```html
<h1 class="text-2xl md:text-4xl lg:text-6xl font-bold px-4 md:px-8 lg:px-16">
  Responsive Heading
</h1>
```

**Example 3: Responsive navigation**

```html
<nav class="flex flex-col md:flex-row justify-between items-center p-4 bg-white shadow">
  <div class="text-xl font-bold mb-4 md:mb-0">Logo</div>
  <div class="flex flex-col md:flex-row gap-2 md:gap-6">
    <a href="#" class="text-gray-700 hover:text-blue-500">Home</a>
    <a href="#" class="text-gray-700 hover:text-blue-500">About</a>
    <a href="#" class="text-gray-700 hover:text-blue-500">Services</a>
    <a href="#" class="text-gray-700 hover:text-blue-500">Contact</a>
  </div>
</nav>
```

**Example 4: Show/hide elements based on screen size**

```html
<!-- Mobile menu icon (visible on mobile, hidden on desktop) -->
<button class="block md:hidden">
  Menu Icon
</button>

<!-- Desktop navigation (hidden on mobile, visible on desktop) -->
<nav class="hidden md:flex gap-6">
  <a href="#">Home</a>
  <a href="#">About</a>
  <a href="#">Contact</a>
</nav>
```

---

## 8. States and Interactivity

In vanilla CSS, you use pseudo-classes like `:hover`, `:focus`, and `:active`. In Tailwind, these become prefixes you add to any utility class.

### Hover, Focus, Active, Disabled

| Prefix       | CSS Equivalent    | When It Applies                           |
| ------------ | ----------------- | ----------------------------------------- |
| `hover:`     | `:hover`          | When the user hovers over the element     |
| `focus:`     | `:focus`          | When the element has keyboard focus       |
| `active:`    | `:active`         | While the element is being clicked        |
| `disabled:`  | `:disabled`       | When a form element is disabled           |
| `visited:`   | `:visited`        | For visited links                         |
| `focus-within:` | `:focus-within` | When any child has focus                 |

```html
<!-- Interactive button with multiple states -->
<button class="bg-blue-500 text-white px-6 py-3 rounded-lg
               hover:bg-blue-600
               focus:outline-none focus:ring-2 focus:ring-blue-300
               active:bg-blue-700
               disabled:bg-gray-300 disabled:cursor-not-allowed
               transition duration-200">
  Click Me
</button>

<!-- Link with hover underline -->
<a href="#" class="text-blue-500 hover:text-blue-700 hover:underline">
  Read more
</a>

<!-- Input with focus styling -->
<input type="text"
       class="border border-gray-300 rounded px-4 py-2
              focus:border-blue-500 focus:ring-2 focus:ring-blue-200
              focus:outline-none
              transition duration-200"
       placeholder="Enter your name">
```

### Group Hover

Sometimes you want to change a child element when the parent is hovered. Use `group` on the parent and `group-hover:` on the child.

```html
<!-- Card where hovering the card changes the title color and shows the arrow -->
<div class="group bg-white p-6 rounded-lg shadow hover:shadow-lg transition duration-200">
  <h3 class="text-lg font-bold text-gray-800 group-hover:text-blue-500 transition">
    Card Title
  </h3>
  <p class="text-gray-600 mt-2">
    Card description goes here.
  </p>
  <span class="text-blue-500 opacity-0 group-hover:opacity-100 transition mt-4 inline-block">
    Learn more -->
  </span>
</div>
```

```
Group Hover Behavior:
======================

  Normal state:                     On hover:
  +-----------------------+         +-----------------------+
  | Card Title            |         | Card Title  (blue)    |
  | Card description...   |         | Card description...   |
  |                       |         | Learn more -->        |
  +-----------------------+         +-----------------------+
                                       shadow increases
  Parent has "group" class
  Children use "group-hover:" prefix
```

### Child Selectors: first, last, odd, even

These prefixes apply styles based on an element's position among its siblings.

| Prefix    | CSS Equivalent     | Description                             |
| --------- | ------------------ | --------------------------------------- |
| `first:`  | `:first-child`     | First child element                     |
| `last:`   | `:last-child`      | Last child element                      |
| `odd:`    | `:nth-child(odd)`  | Odd-numbered children (1st, 3rd, 5th)   |
| `even:`   | `:nth-child(even)` | Even-numbered children (2nd, 4th, 6th)  |

```html
<!-- Striped table rows -->
<table class="w-full">
  <tbody>
    <tr class="odd:bg-white even:bg-gray-50 border-b">
      <td class="p-3">Row 1</td>
    </tr>
    <tr class="odd:bg-white even:bg-gray-50 border-b">
      <td class="p-3">Row 2</td>
    </tr>
    <tr class="odd:bg-white even:bg-gray-50 border-b">
      <td class="p-3">Row 3</td>
    </tr>
    <tr class="odd:bg-white even:bg-gray-50 border-b">
      <td class="p-3">Row 4</td>
    </tr>
  </tbody>
</table>

<!-- List with special first/last styling -->
<ul class="divide-y divide-gray-200">
  <li class="py-3 first:pt-0 last:pb-0">Item 1</li>
  <li class="py-3 first:pt-0 last:pb-0">Item 2</li>
  <li class="py-3 first:pt-0 last:pb-0">Item 3</li>
</ul>
```

---

## 9. Common Tailwind Patterns

These are the patterns you will use in nearly every project. Memorize them.

### Centering Content

```html
<!-- Center horizontally and vertically (full screen) -->
<div class="flex items-center justify-center min-h-screen bg-gray-100">
  <div class="text-2xl font-bold">I am perfectly centered.</div>
</div>

<!-- Center a block element horizontally -->
<div class="max-w-lg mx-auto">
  Centered container with max-width.
</div>

<!-- Center text -->
<p class="text-center">This text is centered.</p>

<!-- Center with Grid (alternative) -->
<div class="grid place-items-center min-h-screen">
  <div>Centered with Grid.</div>
</div>
```

```
Centering Cheat Sheet:
=======================

  Horizontal center (block):     mx-auto
  Horizontal center (text):      text-center
  Vertical + Horizontal (flex):  flex items-center justify-center
  Vertical + Horizontal (grid):  grid place-items-center
```

### Card Component

```html
<!-- Basic card -->
<div class="max-w-sm bg-white rounded-lg shadow-md overflow-hidden">
  <img src="image.jpg" alt="Card image" class="w-full h-48 object-cover">
  <div class="p-6">
    <h2 class="text-xl font-bold text-gray-800">Card Title</h2>
    <p class="text-gray-600 mt-2">
      This is a card description. It provides a brief summary of the content.
    </p>
    <button class="mt-4 bg-blue-500 text-white px-4 py-2 rounded
                   hover:bg-blue-600 transition duration-200">
      Read More
    </button>
  </div>
</div>
```

```
Card Structure Breakdown:
==========================

  +----------------------------------+
  |                                  |
  |           IMAGE                  |  <-- w-full h-48 object-cover
  |         (object-cover)           |
  |                                  |
  +----------------------------------+  <-- overflow-hidden + rounded-lg
  |  p-6                             |      clips the image corners
  |                                  |
  |  Card Title         (text-xl)    |
  |                     (font-bold)  |
  |                                  |
  |  Description text   (text-gray)  |
  |  goes here...       (mt-2)      |
  |                                  |
  |  [  Read More  ]    (mt-4)      |
  |                     (bg-blue)    |
  +----------------------------------+
      shadow-md   rounded-lg   bg-white
```

### Button Styles

```html
<!-- Primary button -->
<button class="bg-blue-500 text-white px-6 py-2 rounded-lg
               hover:bg-blue-600 active:bg-blue-700
               focus:outline-none focus:ring-2 focus:ring-blue-300
               transition duration-200">
  Primary
</button>

<!-- Secondary button (outline) -->
<button class="border-2 border-blue-500 text-blue-500 px-6 py-2 rounded-lg
               hover:bg-blue-500 hover:text-white
               transition duration-200">
  Secondary
</button>

<!-- Danger button -->
<button class="bg-red-500 text-white px-6 py-2 rounded-lg
               hover:bg-red-600
               transition duration-200">
  Delete
</button>

<!-- Disabled button -->
<button class="bg-gray-300 text-gray-500 px-6 py-2 rounded-lg
               cursor-not-allowed" disabled>
  Disabled
</button>

<!-- Pill button -->
<button class="bg-green-500 text-white px-6 py-2 rounded-full
               hover:bg-green-600
               transition duration-200">
  Pill Button
</button>

<!-- Icon button -->
<button class="bg-gray-100 text-gray-700 p-3 rounded-full
               hover:bg-gray-200
               transition duration-200">
  +
</button>
```

### Container and Max-Width

Tailwind provides a `container` class that sets `max-width` based on the current breakpoint. Combine it with `mx-auto` and `px-4` for a standard page layout.

```html
<!-- Standard page container -->
<div class="container mx-auto px-4">
  <h1 class="text-3xl font-bold">Page Title</h1>
  <p class="mt-4 text-gray-600">Page content goes here...</p>
</div>

<!-- Fixed max-width alternative -->
<div class="max-w-7xl mx-auto px-4 sm:px-6 lg:px-8">
  This container maxes out at 80rem (1280px).
</div>
```

| Max-Width Class | Value     | Common Use                |
| --------------- | --------- | ------------------------- |
| `max-w-sm`      | 24rem     | Small modals              |
| `max-w-md`      | 28rem     | Forms                     |
| `max-w-lg`      | 32rem     | Cards, narrow content     |
| `max-w-xl`      | 36rem     | Articles                  |
| `max-w-2xl`     | 42rem     | Blog posts                |
| `max-w-4xl`     | 56rem     | Wide content              |
| `max-w-6xl`     | 72rem     | Dashboard layouts         |
| `max-w-7xl`     | 80rem     | Full page containers      |
| `max-w-full`    | 100%      | Full width                |
| `max-w-screen-xl` | 1280px | Match screen breakpoints  |

---

## 10. Tailwind vs Writing Custom CSS -- When to Use Which?

Tailwind is powerful, but it is not always the right tool. Here is a practical decision guide.

**Use Tailwind when:**

- You are building UI quickly and need consistent spacing, colors, and typography
- You are working on a team and want enforced design consistency
- You are building a component-based application (React, Vue, etc.)
- You want responsive design without writing media queries manually
- You are building prototypes or MVPs

**Use custom CSS when:**

- You need highly complex animations or keyframes
- You are working with CSS art or very specific visual effects
- You have deeply nested selectors that would be clunky with utilities
- You are building a reusable CSS library for others to consume
- You need CSS features Tailwind does not cover (e.g., complex `::before`/`::after` content)

**Use both together (most common in real projects):**

```html
<!-- Tailwind for layout and common styles -->
<div class="flex items-center gap-4 p-6 bg-white rounded-lg shadow">
  <!-- Custom CSS for complex animation -->
  <div class="pulse-animation">
    <span class="w-3 h-3 bg-green-500 rounded-full inline-block"></span>
  </div>
  <span class="text-gray-700">Server is online</span>
</div>
```

```css
/* Custom CSS for things Tailwind doesn't handle well */
@keyframes pulse {
  0%, 100% { transform: scale(1); opacity: 1; }
  50% { transform: scale(1.5); opacity: 0.5; }
}
.pulse-animation {
  animation: pulse 2s infinite;
}
```

| Scenario                          | Recommendation         |
| --------------------------------- | ---------------------- |
| Standard layout and spacing       | Tailwind               |
| Colors, typography, shadows       | Tailwind               |
| Responsive breakpoints            | Tailwind               |
| Hover, focus, state changes       | Tailwind               |
| Complex keyframe animations       | Custom CSS             |
| `::before` / `::after` content    | Custom CSS or Tailwind |
| Third-party library overrides     | Custom CSS             |
| One-off unique visual effects     | Custom CSS             |
| Team project with design system   | Tailwind               |

---

## 11. Summary and Cheat Sheet

### What We Learned

1. **Tailwind CSS** is a utility-first framework that lets you style elements by applying small, single-purpose classes directly in HTML.
2. **Installation** can be done via CDN (for learning) or npm with Vite (for production).
3. **Core utilities** cover spacing, sizing, typography, colors, backgrounds, borders, and shadows.
4. **Flexbox and Grid** utilities mirror their CSS counterparts but are faster to write.
5. **Responsive design** uses mobile-first breakpoint prefixes (`sm:`, `md:`, `lg:`, `xl:`, `2xl:`).
6. **State variants** (`hover:`, `focus:`, `active:`, `group-hover:`) handle interactivity without custom CSS.
7. **Custom CSS** still has its place alongside Tailwind for complex animations and unique effects.

### Utility Class Quick Reference

```
+------------------+----------------------------+---------------------------+
|    CATEGORY       |    COMMON CLASSES          |    EXAMPLE                |
+------------------+----------------------------+---------------------------+
|                   |                            |                           |
|  SPACING          |  p-4, px-2, py-3          |  <div class="p-4 mx-auto">|
|                   |  m-4, mx-auto              |                           |
|                   |  space-x-4, space-y-2      |                           |
|                   |                            |                           |
+------------------+----------------------------+---------------------------+
|                   |                            |                           |
|  SIZING           |  w-full, w-1/2, w-screen   |  <div class="w-full       |
|                   |  h-screen, min-h-screen    |    max-w-lg mx-auto">     |
|                   |  max-w-lg, max-w-7xl       |                           |
|                   |                            |                           |
+------------------+----------------------------+---------------------------+
|                   |                            |                           |
|  TYPOGRAPHY       |  text-lg, text-xl          |  <h1 class="text-2xl      |
|                   |  font-bold, font-semibold  |    font-bold uppercase">  |
|                   |  text-center, uppercase    |                           |
|                   |  tracking-wide             |                           |
|                   |  leading-relaxed           |                           |
|                   |                            |                           |
+------------------+----------------------------+---------------------------+
|                   |                            |                           |
|  COLORS           |  text-red-500              |  <p class="text-gray-600  |
|                   |  bg-blue-200               |    bg-blue-50">           |
|                   |  border-gray-300           |                           |
|                   |                            |                           |
+------------------+----------------------------+---------------------------+
|                   |                            |                           |
|  BACKGROUNDS      |  bg-gradient-to-r          |  <div class="bg-gradient- |
|                   |  from-blue-500             |    to-r from-blue-500     |
|                   |  via-purple-500            |    to-purple-500">        |
|                   |  to-purple-500             |                           |
|                   |                            |                           |
+------------------+----------------------------+---------------------------+
|                   |                            |                           |
|  BORDERS          |  border, border-2          |  <div class="border       |
|                   |  border-red-500            |    rounded-lg             |
|                   |  rounded, rounded-lg       |    border-gray-200">      |
|                   |  rounded-full              |                           |
|                   |                            |                           |
+------------------+----------------------------+---------------------------+
|                   |                            |                           |
|  SHADOWS          |  shadow, shadow-md         |  <div class="shadow-lg    |
|                   |  shadow-lg, shadow-xl      |    rounded-lg bg-white">  |
|                   |  shadow-inner              |                           |
|                   |                            |                           |
+------------------+----------------------------+---------------------------+
|                   |                            |                           |
|  FLEXBOX          |  flex, flex-col            |  <div class="flex         |
|                   |  justify-center            |    justify-between        |
|                   |  justify-between           |    items-center">         |
|                   |  items-center              |                           |
|                   |  gap-4, flex-1             |                           |
|                   |                            |                           |
+------------------+----------------------------+---------------------------+
|                   |                            |                           |
|  GRID             |  grid, grid-cols-3         |  <div class="grid         |
|                   |  grid-cols-12              |    grid-cols-3 gap-4">    |
|                   |  col-span-2, row-span-2    |                           |
|                   |  gap-4                     |                           |
|                   |                            |                           |
+------------------+----------------------------+---------------------------+
|                   |                            |                           |
|  RESPONSIVE       |  sm:, md:, lg:, xl:, 2xl:  |  <div class="grid-cols-1  |
|                   |  (prefix any utility)      |    md:grid-cols-2         |
|                   |                            |    lg:grid-cols-3">       |
|                   |                            |                           |
+------------------+----------------------------+---------------------------+
|                   |                            |                           |
|  STATES           |  hover:, focus:, active:   |  <button class="bg-blue   |
|                   |  disabled:, group-hover:   |    hover:bg-blue-600      |
|                   |  first:, last:             |    focus:ring-2">         |
|                   |  odd:, even:               |                           |
|                   |                            |                           |
+------------------+----------------------------+---------------------------+
```

### Common Patterns Cheat Sheet

```
Pattern                     Classes
--------------------------  ------------------------------------------------
Center (flex)               flex items-center justify-center
Center (block)              mx-auto max-w-lg
Full-screen center          flex items-center justify-center min-h-screen
Card                        bg-white rounded-lg shadow-md p-6
Primary button              bg-blue-500 text-white px-4 py-2 rounded
                            hover:bg-blue-600 transition
Outline button              border-2 border-blue-500 text-blue-500 px-4 py-2
                            rounded hover:bg-blue-500 hover:text-white
Page container              max-w-7xl mx-auto px-4
Navbar                      flex justify-between items-center px-6 py-4
Sidebar layout              flex min-h-screen (sidebar: w-64, main: flex-1)
Responsive grid             grid grid-cols-1 md:grid-cols-2 lg:grid-cols-3 gap-4
Hide on mobile              hidden md:block
Show only on mobile         block md:hidden
Striped rows                odd:bg-white even:bg-gray-50
```

---

> **Next Week:** We will build real components and a complete project page using Tailwind CSS, covering forms, navigation bars, hero sections, and deploying a polished landing page.
