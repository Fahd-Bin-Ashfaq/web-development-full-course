# Week 8: Responsive Design & CSS Animations — Practice Questions

**Total Questions: 53**

| Section | Type | Count |
|---------|------|-------|
| A | Multiple Choice Questions | 15 |
| B | Short Answer Questions | 8 |
| C | True or False | 10 |
| D | Media Query Challenge | 5 |
| E | Coding Exercises | 5 |
| F | CSS Weeks 5-8 Comprehensive Review | 10 |

---

## Section A: Multiple Choice Questions (15 Questions)

**1. Which of the following is the correct syntax for a CSS media query?**

- A) `@media screen and (max-width: 768px) { }`
- B) `@media (screen, max-width: 768px) { }`
- C) `@media screen [max-width: 768px] { }`
- D) `@media screen: max-width(768px) { }`

<details>
<summary>Answer</summary>

**A) `@media screen and (max-width: 768px) { }`**

Media queries use the `@media` rule followed by the media type and conditions enclosed in parentheses, joined by `and`.
</details>

---

**2. In a mobile-first approach, which property is primarily used in media queries?**

- A) `max-width`
- B) `min-width`
- C) `max-height`
- D) `device-width`

<details>
<summary>Answer</summary>

**B) `min-width`**

Mobile-first design starts with styles for the smallest screens and uses `min-width` media queries to progressively add styles for larger screens.
</details>

---

**3. What is the purpose of the following meta tag?**

```html
<meta name="viewport" content="width=device-width, initial-scale=1.0">
```

- A) It sets the page title in the browser tab
- B) It ensures the page scales correctly on mobile devices
- C) It links an external stylesheet
- D) It enables JavaScript on the page

<details>
<summary>Answer</summary>

**B) It ensures the page scales correctly on mobile devices**

The viewport meta tag instructs the browser to set the viewport width to the device width and the initial zoom level to 1.0, which is essential for responsive design.
</details>

---

**4. Which set of breakpoints is most commonly used in responsive design frameworks?**

- A) 320px, 480px, 640px
- B) 576px, 768px, 992px, 1200px
- C) 100px, 500px, 1000px, 1500px
- D) 600px, 900px, 1800px

<details>
<summary>Answer</summary>

**B) 576px, 768px, 992px, 1200px**

These are the standard breakpoints used by popular frameworks such as Bootstrap. They correspond to small, medium, large, and extra-large screen sizes.
</details>

---

**5. Which CSS property is NOT a valid transition property?**

- A) `transition-property`
- B) `transition-duration`
- C) `transition-style`
- D) `transition-timing-function`

<details>
<summary>Answer</summary>

**C) `transition-style`**

The valid transition sub-properties are `transition-property`, `transition-duration`, `transition-timing-function`, and `transition-delay`. There is no `transition-style` property.
</details>

---

**6. What does the `@keyframes` rule define in CSS?**

- A) A media query breakpoint
- B) The stages of a CSS animation sequence
- C) A new CSS variable
- D) A transition timing function

<details>
<summary>Answer</summary>

**B) The stages of a CSS animation sequence**

The `@keyframes` rule specifies the intermediate steps (keyframes) in a CSS animation, defining what styles apply at various points during the animation.
</details>

---

**7. Which shorthand correctly sets an animation named `fadeIn` that lasts 2 seconds, eases in, and runs infinitely?**

- A) `animation: fadeIn 2s ease-in infinite;`
- B) `animation: 2s fadeIn ease-in forever;`
- C) `animation: fadeIn infinite 2s ease-in;`
- D) `animate: fadeIn 2s ease-in infinite;`

<details>
<summary>Answer</summary>

**A) `animation: fadeIn 2s ease-in infinite;`**

The correct shorthand order is `animation: name duration timing-function iteration-count`. Option D uses an invalid property name (`animate`), and option B uses an invalid keyword (`forever`).
</details>

---

**8. Which `transform` function rotates an element 45 degrees clockwise?**

- A) `transform: rotate(45);`
- B) `transform: rotate(45deg);`
- C) `transform: spin(45deg);`
- D) `transform: turn(45deg);`

<details>
<summary>Answer</summary>

**B) `transform: rotate(45deg);`**

The `rotate()` function requires a unit (such as `deg`). Without the unit, the value is invalid. `spin()` and `turn()` are not valid CSS transform functions.
</details>

---

**9. How are CSS custom properties (CSS variables) declared?**

- A) `$primary-color: #3498db;`
- B) `--primary-color: #3498db;`
- C) `@primary-color: #3498db;`
- D) `var-primary-color: #3498db;`

<details>
<summary>Answer</summary>

**B) `--primary-color: #3498db;`**

CSS custom properties are declared with a double hyphen prefix (`--`). They are accessed using the `var()` function, for example `color: var(--primary-color);`.
</details>

---

**10. What does the unit `vw` represent in CSS?**

- A) Variable width
- B) 1% of the viewport width
- C) 1% of the parent element width
- D) 1 pixel of the viewport

<details>
<summary>Answer</summary>

**B) 1% of the viewport width**

`1vw` equals 1% of the viewport's width. So `100vw` equals the full width of the browser viewport.
</details>

---

**11. What does the CSS `clamp()` function do?**

- A) Restricts a value between a minimum and maximum
- B) Rounds a value to the nearest integer
- C) Converts pixels to rem units
- D) Clamps an animation to a specific duration

<details>
<summary>Answer</summary>

**A) Restricts a value between a minimum and maximum**

`clamp(min, preferred, max)` returns the preferred value as long as it falls between the minimum and maximum. If it is smaller than the minimum, the minimum is used; if larger than the maximum, the maximum is used.
</details>

---

**12. Which of the following is a valid use of `clamp()` for responsive font sizing?**

- A) `font-size: clamp(1rem, 2.5vw, 3rem);`
- B) `font-size: clamp(2.5vw);`
- C) `font-size: clamp(1rem, 3rem);`
- D) `font-size: clamp(min: 1rem, max: 3rem);`

<details>
<summary>Answer</summary>

**A) `font-size: clamp(1rem, 2.5vw, 3rem);`**

`clamp()` requires exactly three arguments: a minimum value, a preferred value, and a maximum value, separated by commas.
</details>

---

**13. What is the difference between `max-width` and `min-width` in media queries?**

- A) There is no difference; they are interchangeable
- B) `max-width` applies styles up to a given width; `min-width` applies styles from a given width upward
- C) `max-width` is for print media; `min-width` is for screen media
- D) `max-width` sets the element width; `min-width` sets the viewport width

<details>
<summary>Answer</summary>

**B) `max-width` applies styles up to a given width; `min-width` applies styles from a given width upward**

`max-width: 768px` targets screens that are 768px wide or narrower (desktop-first). `min-width: 768px` targets screens that are 768px wide or wider (mobile-first).
</details>

---

**14. Which `animation-fill-mode` value keeps the element styled as defined in the last keyframe after the animation ends?**

- A) `none`
- B) `backwards`
- C) `forwards`
- D) `alternate`

<details>
<summary>Answer</summary>

**C) `forwards`**

`animation-fill-mode: forwards` retains the styles from the final keyframe after the animation completes. `backwards` applies the first keyframe styles during the delay period. `alternate` is an `animation-direction` value, not a fill mode.
</details>

---

**15. What does `1rem` equal by default in most browsers?**

- A) 1 pixel
- B) 10 pixels
- C) 16 pixels
- D) 100% of the viewport width

<details>
<summary>Answer</summary>

**C) 16 pixels**

`1rem` equals the font size of the root element (`<html>`). Most browsers set the default root font size to 16px, so `1rem = 16px` unless overridden.
</details>

---

## Section B: Short Answer Questions (8 Questions)

**1. What is responsive web design, and why is it important in modern web development?**

<details>
<summary>Answer</summary>

Responsive web design is an approach to building websites that adapt their layout, content, and visual presentation based on the screen size and capabilities of the device being used. It uses flexible grids, flexible images, and CSS media queries to create a single codebase that works across desktops, tablets, and mobile phones.

It is important because users access websites from a wide variety of devices with different screen sizes. A responsive design ensures a consistent and usable experience for all users, improves SEO (search engines favor mobile-friendly sites), reduces development costs by eliminating the need for separate mobile sites, and increases accessibility.
</details>

---

**2. Explain the difference between mobile-first and desktop-first design approaches. Which is generally recommended and why?**

<details>
<summary>Answer</summary>

**Mobile-first** starts by designing and coding for the smallest screen size, then uses `min-width` media queries to progressively add complexity for larger screens.

**Desktop-first** starts by designing for large screens, then uses `max-width` media queries to scale down and adjust the layout for smaller screens.

Mobile-first is generally recommended because:
- It forces developers to prioritize essential content and functionality.
- Mobile devices often have slower connections, so loading minimal CSS first improves performance.
- It is easier to add complexity than to remove it.
- The majority of global web traffic now comes from mobile devices.
</details>

---

**3. What is the difference between CSS transitions and CSS animations? When would you use each?**

<details>
<summary>Answer</summary>

**CSS Transitions** provide a way to smoothly change a CSS property from one value to another over a specified duration. They require a trigger (such as `:hover`, `:focus`, or a class change) and only animate between two states (start and end).

**CSS Animations** use `@keyframes` to define multiple intermediate steps in an animation sequence. They can run automatically (without a trigger), loop infinitely, alternate direction, and control multiple stages of the animation independently.

**When to use transitions:** Simple state changes like hover effects, color changes, and element resizing where only two states are involved.

**When to use animations:** Complex multi-step animations like loading spinners, bouncing effects, or any animation that needs to run on page load without user interaction.
</details>

---

**4. How does `transform: translate()` differ from using `position` with `top`/`left` offsets to move an element?**

<details>
<summary>Answer</summary>

`transform: translate()` moves an element visually without affecting the document flow. The element still occupies its original space in the layout, and other elements are not repositioned. It is also hardware-accelerated by the GPU, making it more performant for animations.

Using `position` with `top`/`left` (when set to `relative`, `absolute`, or `fixed`) physically repositions the element within the layout context. With `absolute` or `fixed` positioning, the element is removed from normal flow entirely. Changes to `top`/`left` trigger layout recalculations, which are more expensive for the browser to process during animations.

For animations and transitions, `transform: translate()` is the preferred approach because it is smoother and more performant.
</details>

---

**5. What are CSS custom properties (CSS variables), and how do they improve maintainability?**

<details>
<summary>Answer</summary>

CSS custom properties are author-defined values that can be reused throughout a stylesheet. They are declared with a `--` prefix and accessed using the `var()` function:

```css
:root {
  --primary-color: #3498db;
  --spacing: 1rem;
}

.button {
  background-color: var(--primary-color);
  padding: var(--spacing);
}
```

They improve maintainability by:
- **Centralizing values:** Changing a variable in one place updates it everywhere it is used.
- **Improving readability:** Descriptive names like `--primary-color` are more meaningful than raw hex codes.
- **Enabling theming:** Variables can be overridden within specific selectors or media queries to create themes or responsive adjustments.
- **Supporting dynamic updates:** Unlike preprocessor variables, CSS custom properties can be changed at runtime using JavaScript.
</details>

---

**6. Explain the `clamp()` function in CSS. Provide an example of how it can be used for responsive typography.**

<details>
<summary>Answer</summary>

The `clamp()` function accepts three values: a minimum, a preferred, and a maximum. It returns the preferred value as long as it stays within the min-max range. If the preferred value drops below the minimum, the minimum is used. If it exceeds the maximum, the maximum is used.

**Syntax:** `clamp(minimum, preferred, maximum)`

**Example for responsive typography:**

```css
h1 {
  font-size: clamp(1.5rem, 4vw, 3rem);
}
```

In this example:
- The font size will never be smaller than `1.5rem` (24px at default).
- The font size will scale with the viewport at `4vw`.
- The font size will never exceed `3rem` (48px at default).

This creates fluid, responsive typography without the need for multiple media query breakpoints.
</details>

---

**7. What are the key differences between `vw`, `vh`, `rem`, `em`, and `%` units in CSS? When is each most appropriate?**

<details>
<summary>Answer</summary>

| Unit | Relative To | Best Used For |
|------|-------------|---------------|
| `vw` | 1% of the viewport width | Full-width sections, responsive typography |
| `vh` | 1% of the viewport height | Full-screen hero sections, modals |
| `rem` | Font size of the root element (`<html>`) | Font sizes, spacing, consistent scaling |
| `em` | Font size of the parent element | Component-level spacing relative to text size |
| `%` | The parent element's corresponding property | Fluid widths, relative sizing within containers |

- Use `rem` for global consistency (font sizes, margins, padding).
- Use `em` when you want sizing to scale with a component's own text size.
- Use `vw`/`vh` for elements that should scale relative to the browser window.
- Use `%` for elements that should be proportional to their parent container.
</details>

---

**8. Describe the `transition` shorthand property. What are its individual sub-properties, and what does each control?**

<details>
<summary>Answer</summary>

The `transition` shorthand combines four sub-properties into one declaration:

```css
transition: property duration timing-function delay;
```

| Sub-Property | Description | Example |
|---|---|---|
| `transition-property` | The CSS property to animate | `background-color`, `transform`, `all` |
| `transition-duration` | How long the transition takes | `0.3s`, `500ms` |
| `transition-timing-function` | The speed curve of the transition | `ease`, `linear`, `ease-in-out`, `cubic-bezier()` |
| `transition-delay` | Time to wait before the transition starts | `0s`, `0.2s` |

**Example:**

```css
.button {
  background-color: #3498db;
  transition: background-color 0.3s ease-in-out 0s;
}

.button:hover {
  background-color: #2980b9;
}
```

Multiple transitions can be comma-separated:

```css
transition: background-color 0.3s ease, transform 0.2s ease-in;
```
</details>

---

## Section C: True or False (10 Questions)

| # | Statement | Answer | Explanation |
|---|-----------|--------|-------------|
| 1 | Media queries can only target screen width. | **False** | Media queries can target many features including height, orientation, resolution, aspect-ratio, color scheme (prefers-color-scheme), reduced motion (prefers-reduced-motion), and more. |
| 2 | The `min-width` media query is associated with the mobile-first approach. | **True** | In mobile-first design, base styles are written for small screens and `min-width` queries are used to add styles as the screen gets larger. |
| 3 | CSS transitions can animate between multiple keyframes. | **False** | CSS transitions only animate between two states (a start and an end). For multi-step animations, `@keyframes` with the `animation` property must be used. |
| 4 | The `transform` property modifies the document flow of an element. | **False** | `transform` applies visual changes (rotate, scale, translate, skew) without affecting the document flow. The element still occupies its original space in the layout. |
| 5 | `animation-iteration-count: infinite;` makes an animation repeat forever. | **True** | Setting the iteration count to `infinite` causes the animation to loop indefinitely until it is stopped or the element is removed. |
| 6 | CSS custom properties declared in `:root` are accessible throughout the entire document. | **True** | The `:root` selector targets the highest-level parent element (`<html>`), so variables declared there are globally available to all elements via inheritance. |
| 7 | The `vh` unit is relative to the parent element's height. | **False** | `vh` is relative to 1% of the viewport height, not the parent element's height. Use `%` for parent-relative sizing. |
| 8 | The `animation-direction: alternate` property makes the animation play forward and then backward. | **True** | When set to `alternate`, the animation plays forward on odd iterations and backward on even iterations, creating a back-and-forth effect. |
| 9 | You must include the viewport meta tag for media queries to work correctly on mobile devices. | **True** | Without the viewport meta tag, mobile browsers render pages at a virtual desktop width (typically 980px) and scale down, causing media queries based on device width to not trigger as expected. |
| 10 | The `clamp()` function requires exactly two arguments. | **False** | `clamp()` requires exactly three arguments: a minimum value, a preferred value, and a maximum value. Example: `clamp(1rem, 2.5vw, 3rem)`. |

---

## Section D: Media Query Challenge (5 Questions)

**1. Hide a sidebar on screens smaller than 768px.**

Write a media query that hides an element with the class `.sidebar` on screens narrower than 768px.

<details>
<summary>Answer</summary>

```css
@media screen and (max-width: 767px) {
  .sidebar {
    display: none;
  }
}
```

This targets screens up to 767px wide (below the 768px tablet breakpoint) and hides the sidebar entirely.
</details>

---

**2. Change a three-column grid layout to a single column on screens smaller than 576px.**

Write a media query that converts a `.grid-container` from three columns to one column.

<details>
<summary>Answer</summary>

```css
.grid-container {
  display: grid;
  grid-template-columns: repeat(3, 1fr);
  gap: 1rem;
}

@media screen and (max-width: 575px) {
  .grid-container {
    grid-template-columns: 1fr;
  }
}
```

On screens narrower than 576px, the grid switches from three columns to a single stacked column layout.
</details>

---

**3. Increase the font size of headings on screens wider than 1200px.**

Write a mobile-first media query that increases all `h1` elements to `3rem` on large screens.

<details>
<summary>Answer</summary>

```css
h1 {
  font-size: 1.8rem;
}

@media screen and (min-width: 1200px) {
  h1 {
    font-size: 3rem;
  }
}
```

Using `min-width` (mobile-first), the base font size is `1.8rem` and it increases to `3rem` on screens 1200px and wider.
</details>

---

**4. Apply a dark background when the user prefers a dark color scheme.**

Write a media query that changes the `body` background to `#1a1a2e` and text color to `#e0e0e0` when the user has dark mode enabled.

<details>
<summary>Answer</summary>

```css
@media (prefers-color-scheme: dark) {
  body {
    background-color: #1a1a2e;
    color: #e0e0e0;
  }
}
```

The `prefers-color-scheme` media feature detects the user's operating system or browser color scheme preference.
</details>

---

**5. Stack navigation links vertically on screens smaller than 992px and center-align them.**

Write a media query for a `.nav-links` container that uses flexbox.

<details>
<summary>Answer</summary>

```css
.nav-links {
  display: flex;
  flex-direction: row;
  gap: 1.5rem;
}

@media screen and (max-width: 991px) {
  .nav-links {
    flex-direction: column;
    align-items: center;
    text-align: center;
  }
}
```

On screens narrower than 992px, the navigation links switch from a horizontal row to a vertical stack with center alignment.
</details>

---

## Section E: Coding Exercises (5 Tasks)

### Task 1: Make an Existing HTML Page Responsive

**Objective:** Take the provided HTML page and make it fully responsive using media queries at three breakpoints.

**Requirements:**
- Use three breakpoints: `576px` (mobile), `768px` (tablet), `992px` (desktop)
- Apply a mobile-first approach using `min-width` queries
- Include the viewport meta tag
- Ensure the navigation, content area, and footer adapt to each breakpoint

**Starter HTML:**

```html
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>Responsive Page</title>
  <link rel="stylesheet" href="styles.css">
</head>
<body>
  <header>
    <nav class="navbar">
      <div class="logo">MyBrand</div>
      <ul class="nav-links">
        <li><a href="#">Home</a></li>
        <li><a href="#">About</a></li>
        <li><a href="#">Services</a></li>
        <li><a href="#">Contact</a></li>
      </ul>
    </nav>
  </header>

  <main class="content">
    <section class="hero">
      <h1>Welcome to MyBrand</h1>
      <p>We build amazing web experiences.</p>
    </section>

    <section class="features">
      <div class="feature-card">
        <h3>Feature 1</h3>
        <p>Description of feature one.</p>
      </div>
      <div class="feature-card">
        <h3>Feature 2</h3>
        <p>Description of feature two.</p>
      </div>
      <div class="feature-card">
        <h3>Feature 3</h3>
        <p>Description of feature three.</p>
      </div>
    </section>
  </main>

  <footer>
    <p>&copy; 2025 MyBrand. All rights reserved.</p>
  </footer>
</body>
</html>
```

**Your Task:** Write the complete `styles.css` file with responsive styles for all three breakpoints.

<details>
<summary>Solution</summary>

```css
/* ===== CSS Reset & Base Styles (Mobile-First) ===== */
* {
  margin: 0;
  padding: 0;
  box-sizing: border-box;
}

body {
  font-family: 'Segoe UI', Tahoma, Geneva, Verdana, sans-serif;
  line-height: 1.6;
  color: #333;
}

/* ===== Navigation ===== */
.navbar {
  background-color: #2c3e50;
  padding: 1rem;
  display: flex;
  flex-direction: column;
  align-items: center;
}

.logo {
  color: #ecf0f1;
  font-size: 1.5rem;
  font-weight: bold;
  margin-bottom: 0.5rem;
}

.nav-links {
  list-style: none;
  display: flex;
  flex-direction: column;
  align-items: center;
  gap: 0.5rem;
}

.nav-links a {
  color: #ecf0f1;
  text-decoration: none;
  padding: 0.25rem 0.5rem;
}

/* ===== Hero Section ===== */
.hero {
  text-align: center;
  padding: 2rem 1rem;
  background-color: #3498db;
  color: white;
}

.hero h1 {
  font-size: 1.8rem;
  margin-bottom: 0.5rem;
}

/* ===== Feature Cards ===== */
.features {
  display: grid;
  grid-template-columns: 1fr;
  gap: 1rem;
  padding: 1.5rem 1rem;
}

.feature-card {
  background-color: #f8f9fa;
  padding: 1.5rem;
  border-radius: 8px;
  box-shadow: 0 2px 4px rgba(0, 0, 0, 0.1);
}

/* ===== Footer ===== */
footer {
  background-color: #2c3e50;
  color: #ecf0f1;
  text-align: center;
  padding: 1rem;
}

/* ===== Tablet (min-width: 576px) ===== */
@media screen and (min-width: 576px) {
  .features {
    grid-template-columns: repeat(2, 1fr);
    padding: 2rem;
  }

  .hero h1 {
    font-size: 2.2rem;
  }

  .nav-links {
    flex-direction: row;
    gap: 1rem;
  }

  .navbar {
    flex-direction: row;
    justify-content: space-between;
  }

  .logo {
    margin-bottom: 0;
  }
}

/* ===== Tablet Landscape (min-width: 768px) ===== */
@media screen and (min-width: 768px) {
  .hero {
    padding: 3rem 2rem;
  }

  .hero h1 {
    font-size: 2.5rem;
  }

  .features {
    padding: 2.5rem;
    gap: 1.5rem;
  }

  .nav-links a {
    padding: 0.5rem 1rem;
  }
}

/* ===== Desktop (min-width: 992px) ===== */
@media screen and (min-width: 992px) {
  .hero {
    padding: 4rem 2rem;
  }

  .hero h1 {
    font-size: 3rem;
  }

  .features {
    grid-template-columns: repeat(3, 1fr);
    max-width: 1200px;
    margin: 0 auto;
    padding: 3rem 2rem;
  }

  .navbar {
    padding: 1rem 3rem;
  }

  .nav-links {
    gap: 2rem;
  }
}
```
</details>

---

### Task 2: Animated Buttons with Hover Transitions

**Objective:** Create a set of buttons with smooth hover transitions including scale, color change, and shadow effects.

**Requirements:**
- Create three buttons with different styles (primary, secondary, outline)
- Add hover transitions for `background-color`, `transform: scale()`, and `box-shadow`
- Each transition should have a smooth easing function
- Include a focus state for accessibility

<details>
<summary>Solution</summary>

```html
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>Animated Buttons</title>
  <style>
    body {
      display: flex;
      justify-content: center;
      align-items: center;
      min-height: 100vh;
      gap: 2rem;
      background-color: #f5f5f5;
      font-family: 'Segoe UI', sans-serif;
    }

    .btn {
      padding: 0.75rem 2rem;
      font-size: 1rem;
      border: 2px solid transparent;
      border-radius: 8px;
      cursor: pointer;
      font-weight: 600;
      transition: background-color 0.3s ease,
                  transform 0.2s ease-out,
                  box-shadow 0.3s ease,
                  border-color 0.3s ease;
    }

    .btn:focus {
      outline: 3px solid #74b9ff;
      outline-offset: 2px;
    }

    /* Primary Button */
    .btn-primary {
      background-color: #3498db;
      color: white;
    }

    .btn-primary:hover {
      background-color: #2980b9;
      transform: scale(1.05);
      box-shadow: 0 4px 15px rgba(52, 152, 219, 0.4);
    }

    .btn-primary:active {
      transform: scale(0.98);
    }

    /* Secondary Button */
    .btn-secondary {
      background-color: #2ecc71;
      color: white;
    }

    .btn-secondary:hover {
      background-color: #27ae60;
      transform: scale(1.05);
      box-shadow: 0 4px 15px rgba(46, 204, 113, 0.4);
    }

    .btn-secondary:active {
      transform: scale(0.98);
    }

    /* Outline Button */
    .btn-outline {
      background-color: transparent;
      color: #e74c3c;
      border-color: #e74c3c;
    }

    .btn-outline:hover {
      background-color: #e74c3c;
      color: white;
      transform: scale(1.05);
      box-shadow: 0 4px 15px rgba(231, 76, 60, 0.4);
    }

    .btn-outline:active {
      transform: scale(0.98);
    }
  </style>
</head>
<body>
  <button class="btn btn-primary">Primary</button>
  <button class="btn btn-secondary">Secondary</button>
  <button class="btn btn-outline">Outline</button>
</body>
</html>
```
</details>

---

### Task 3: Loading Spinner Animation Using @keyframes

**Objective:** Create a CSS-only loading spinner animation.

**Requirements:**
- Use `@keyframes` to define a rotation animation
- The spinner should rotate 360 degrees continuously
- Style it as a circular border with one transparent side
- Use `animation` shorthand
- Center the spinner on the page

<details>
<summary>Solution</summary>

```html
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>Loading Spinner</title>
  <style>
    body {
      display: flex;
      justify-content: center;
      align-items: center;
      min-height: 100vh;
      background-color: #f5f5f5;
      margin: 0;
    }

    .spinner-container {
      display: flex;
      flex-direction: column;
      align-items: center;
      gap: 1.5rem;
    }

    .spinner {
      width: 60px;
      height: 60px;
      border: 5px solid #e0e0e0;
      border-top: 5px solid #3498db;
      border-radius: 50%;
      animation: spin 1s linear infinite;
    }

    .spinner-text {
      font-family: 'Segoe UI', sans-serif;
      color: #555;
      font-size: 1.1rem;
    }

    @keyframes spin {
      0% {
        transform: rotate(0deg);
      }
      100% {
        transform: rotate(360deg);
      }
    }

    /* Bonus: Pulse animation for the text */
    .spinner-text {
      animation: pulse 1.5s ease-in-out infinite;
    }

    @keyframes pulse {
      0%, 100% {
        opacity: 1;
      }
      50% {
        opacity: 0.5;
      }
    }
  </style>
</head>
<body>
  <div class="spinner-container">
    <div class="spinner"></div>
    <p class="spinner-text">Loading...</p>
  </div>
</body>
</html>
```
</details>

---

### Task 4: Responsive Navbar That Collapses on Mobile (CSS Only)

**Objective:** Build a navigation bar that displays horizontally on desktop and collapses into a hamburger-toggled menu on mobile using CSS only (no JavaScript).

**Requirements:**
- Use the checkbox hack for toggling the mobile menu
- Horizontal layout on screens wider than 768px
- Vertical slide-down menu on mobile
- Smooth transition for menu opening/closing
- Accessible label for the hamburger toggle

<details>
<summary>Solution</summary>

```html
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>Responsive Navbar</title>
  <style>
    * {
      margin: 0;
      padding: 0;
      box-sizing: border-box;
    }

    body {
      font-family: 'Segoe UI', sans-serif;
    }

    .navbar {
      background-color: #2c3e50;
      padding: 0 1.5rem;
    }

    .nav-container {
      display: flex;
      justify-content: space-between;
      align-items: center;
      max-width: 1200px;
      margin: 0 auto;
    }

    .logo {
      color: #ecf0f1;
      font-size: 1.5rem;
      font-weight: bold;
      padding: 1rem 0;
    }

    /* Hide the checkbox */
    .menu-toggle {
      display: none;
    }

    /* Hamburger icon */
    .hamburger {
      display: flex;
      flex-direction: column;
      gap: 5px;
      cursor: pointer;
      padding: 0.5rem;
    }

    .hamburger span {
      display: block;
      width: 25px;
      height: 3px;
      background-color: #ecf0f1;
      border-radius: 3px;
      transition: transform 0.3s ease, opacity 0.3s ease;
    }

    /* Navigation links */
    .nav-links {
      list-style: none;
      display: flex;
      flex-direction: column;
      position: absolute;
      top: 60px;
      left: 0;
      right: 0;
      background-color: #34495e;
      max-height: 0;
      overflow: hidden;
      transition: max-height 0.4s ease;
    }

    .nav-links li a {
      display: block;
      color: #ecf0f1;
      text-decoration: none;
      padding: 1rem 1.5rem;
      border-bottom: 1px solid #3d566e;
      transition: background-color 0.2s ease;
    }

    .nav-links li a:hover {
      background-color: #3498db;
    }

    /* When checkbox is checked, expand the menu */
    .menu-toggle:checked ~ .nav-links {
      max-height: 300px;
    }

    /* Animate hamburger to X */
    .menu-toggle:checked ~ .hamburger span:nth-child(1) {
      transform: rotate(45deg) translate(5px, 6px);
    }

    .menu-toggle:checked ~ .hamburger span:nth-child(2) {
      opacity: 0;
    }

    .menu-toggle:checked ~ .hamburger span:nth-child(3) {
      transform: rotate(-45deg) translate(5px, -6px);
    }

    /* ===== Desktop (min-width: 768px) ===== */
    @media screen and (min-width: 768px) {
      .hamburger {
        display: none;
      }

      .nav-links {
        position: static;
        flex-direction: row;
        max-height: none;
        overflow: visible;
        background-color: transparent;
      }

      .nav-links li a {
        border-bottom: none;
        padding: 1rem 1.25rem;
      }

      .nav-links li a:hover {
        background-color: transparent;
        color: #3498db;
      }
    }
  </style>
</head>
<body>
  <nav class="navbar">
    <div class="nav-container">
      <a href="#" class="logo">MyBrand</a>

      <input type="checkbox" id="menu-toggle" class="menu-toggle" aria-label="Toggle navigation menu">
      <label for="menu-toggle" class="hamburger" aria-label="Open menu">
        <span></span>
        <span></span>
        <span></span>
      </label>

      <ul class="nav-links">
        <li><a href="#">Home</a></li>
        <li><a href="#">About</a></li>
        <li><a href="#">Services</a></li>
        <li><a href="#">Portfolio</a></li>
        <li><a href="#">Contact</a></li>
      </ul>
    </div>
  </nav>
</body>
</html>
```
</details>

---

### Task 5: Responsive Portfolio Page with Animations (CSS Phase Project)

**Objective:** Build a complete, responsive single-page portfolio website incorporating everything learned in the CSS phase (Weeks 5-8). This is the culminating project for the CSS section of the course.

**Requirements:**
- **Responsive layout** with at least three breakpoints (mobile, tablet, desktop)
- **CSS Grid and Flexbox** for layout
- **CSS variables** for colors and spacing
- **Transitions** on interactive elements (buttons, links, cards)
- **At least one @keyframes animation** (e.g., hero text fade-in, scroll indicator)
- **Responsive typography** using `clamp()`
- **A responsive navigation bar** that adapts to mobile screens
- Mobile-first approach

**Sections to include:**
1. Navigation bar
2. Hero section with animated heading
3. About Me section
4. Projects/portfolio grid (responsive cards)
5. Contact section
6. Footer

<details>
<summary>Solution</summary>

```html
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>Portfolio - CSS Phase Project</title>
  <style>
    /* ===== CSS Variables ===== */
    :root {
      --color-primary: #3498db;
      --color-primary-dark: #2980b9;
      --color-secondary: #2ecc71;
      --color-dark: #2c3e50;
      --color-darker: #1a252f;
      --color-light: #ecf0f1;
      --color-text: #333;
      --color-text-light: #777;
      --color-bg: #ffffff;
      --color-bg-alt: #f8f9fa;
      --spacing-sm: 0.5rem;
      --spacing-md: 1rem;
      --spacing-lg: 2rem;
      --spacing-xl: 4rem;
      --border-radius: 8px;
      --shadow: 0 2px 10px rgba(0, 0, 0, 0.1);
      --shadow-hover: 0 8px 25px rgba(0, 0, 0, 0.15);
      --transition-speed: 0.3s;
    }

    /* ===== Reset & Base ===== */
    * {
      margin: 0;
      padding: 0;
      box-sizing: border-box;
    }

    html {
      scroll-behavior: smooth;
    }

    body {
      font-family: 'Segoe UI', Tahoma, Geneva, Verdana, sans-serif;
      line-height: 1.6;
      color: var(--color-text);
      background-color: var(--color-bg);
    }

    a {
      text-decoration: none;
      color: inherit;
    }

    img {
      max-width: 100%;
      display: block;
    }

    /* ===== Typography with clamp() ===== */
    h1 {
      font-size: clamp(2rem, 5vw, 3.5rem);
    }

    h2 {
      font-size: clamp(1.5rem, 3.5vw, 2.5rem);
    }

    h3 {
      font-size: clamp(1.1rem, 2vw, 1.4rem);
    }

    p {
      font-size: clamp(0.95rem, 1.5vw, 1.1rem);
    }

    /* ===== Section Styling ===== */
    .section {
      padding: var(--spacing-lg) var(--spacing-md);
    }

    .section-title {
      text-align: center;
      margin-bottom: var(--spacing-lg);
      color: var(--color-dark);
    }

    .section-title::after {
      content: '';
      display: block;
      width: 60px;
      height: 3px;
      background-color: var(--color-primary);
      margin: var(--spacing-sm) auto 0;
      border-radius: 2px;
    }

    .container {
      max-width: 1200px;
      margin: 0 auto;
      padding: 0 var(--spacing-md);
    }

    /* ===== Navigation ===== */
    .navbar {
      background-color: var(--color-dark);
      padding: 0 var(--spacing-md);
      position: sticky;
      top: 0;
      z-index: 1000;
    }

    .nav-inner {
      display: flex;
      justify-content: space-between;
      align-items: center;
      max-width: 1200px;
      margin: 0 auto;
    }

    .nav-logo {
      color: var(--color-light);
      font-size: 1.4rem;
      font-weight: 700;
      padding: var(--spacing-md) 0;
    }

    .nav-logo span {
      color: var(--color-primary);
    }

    .nav-checkbox {
      display: none;
    }

    .nav-hamburger {
      display: flex;
      flex-direction: column;
      gap: 5px;
      cursor: pointer;
      padding: var(--spacing-sm);
    }

    .nav-hamburger span {
      width: 25px;
      height: 3px;
      background-color: var(--color-light);
      border-radius: 2px;
      transition: transform var(--transition-speed) ease,
                  opacity var(--transition-speed) ease;
    }

    .nav-links {
      list-style: none;
      display: flex;
      flex-direction: column;
      position: absolute;
      top: 56px;
      left: 0;
      right: 0;
      background-color: var(--color-darker);
      max-height: 0;
      overflow: hidden;
      transition: max-height 0.4s ease;
    }

    .nav-links a {
      display: block;
      color: var(--color-light);
      padding: 0.8rem var(--spacing-md);
      transition: background-color var(--transition-speed) ease;
    }

    .nav-links a:hover {
      background-color: var(--color-primary);
    }

    .nav-checkbox:checked ~ .nav-links {
      max-height: 400px;
    }

    .nav-checkbox:checked ~ .nav-hamburger span:nth-child(1) {
      transform: rotate(45deg) translate(5px, 6px);
    }

    .nav-checkbox:checked ~ .nav-hamburger span:nth-child(2) {
      opacity: 0;
    }

    .nav-checkbox:checked ~ .nav-hamburger span:nth-child(3) {
      transform: rotate(-45deg) translate(5px, -6px);
    }

    /* ===== Hero Section ===== */
    .hero {
      background: linear-gradient(135deg, var(--color-dark), var(--color-primary));
      color: white;
      text-align: center;
      padding: var(--spacing-xl) var(--spacing-md);
      min-height: 80vh;
      display: flex;
      flex-direction: column;
      justify-content: center;
      align-items: center;
    }

    .hero h1 {
      animation: fadeInDown 1s ease-out;
    }

    .hero p {
      margin-top: var(--spacing-md);
      color: rgba(255, 255, 255, 0.85);
      max-width: 600px;
      animation: fadeInUp 1s ease-out 0.3s both;
    }

    .hero-btn {
      display: inline-block;
      margin-top: var(--spacing-lg);
      padding: 0.8rem 2rem;
      background-color: var(--color-secondary);
      color: white;
      border: none;
      border-radius: var(--border-radius);
      font-size: 1rem;
      font-weight: 600;
      cursor: pointer;
      transition: background-color var(--transition-speed) ease,
                  transform 0.2s ease,
                  box-shadow var(--transition-speed) ease;
      animation: fadeInUp 1s ease-out 0.6s both;
    }

    .hero-btn:hover {
      background-color: #27ae60;
      transform: translateY(-2px);
      box-shadow: 0 4px 15px rgba(46, 204, 113, 0.4);
    }

    /* Scroll indicator */
    .scroll-indicator {
      margin-top: var(--spacing-lg);
      animation: bounce 2s ease-in-out infinite;
    }

    .scroll-indicator span {
      display: block;
      width: 30px;
      height: 30px;
      border-right: 3px solid rgba(255, 255, 255, 0.6);
      border-bottom: 3px solid rgba(255, 255, 255, 0.6);
      transform: rotate(45deg);
      margin: 0 auto;
    }

    /* ===== About Section ===== */
    .about {
      background-color: var(--color-bg-alt);
    }

    .about-content {
      display: flex;
      flex-direction: column;
      gap: var(--spacing-lg);
      align-items: center;
    }

    .about-image {
      width: 200px;
      height: 200px;
      border-radius: 50%;
      background-color: var(--color-primary);
      display: flex;
      align-items: center;
      justify-content: center;
      color: white;
      font-size: 3rem;
      font-weight: bold;
      flex-shrink: 0;
    }

    .about-text {
      text-align: center;
    }

    .about-text p {
      color: var(--color-text-light);
      margin-bottom: var(--spacing-md);
    }

    .skills-list {
      display: flex;
      flex-wrap: wrap;
      gap: var(--spacing-sm);
      justify-content: center;
      margin-top: var(--spacing-md);
    }

    .skill-tag {
      background-color: var(--color-primary);
      color: white;
      padding: 0.3rem 0.8rem;
      border-radius: 20px;
      font-size: 0.85rem;
      transition: transform var(--transition-speed) ease,
                  box-shadow var(--transition-speed) ease;
    }

    .skill-tag:hover {
      transform: translateY(-2px);
      box-shadow: var(--shadow);
    }

    /* ===== Projects Section ===== */
    .projects-grid {
      display: grid;
      grid-template-columns: 1fr;
      gap: var(--spacing-lg);
    }

    .project-card {
      background-color: var(--color-bg);
      border-radius: var(--border-radius);
      box-shadow: var(--shadow);
      overflow: hidden;
      transition: transform var(--transition-speed) ease,
                  box-shadow var(--transition-speed) ease;
    }

    .project-card:hover {
      transform: translateY(-5px);
      box-shadow: var(--shadow-hover);
    }

    .project-image {
      height: 200px;
      background-color: var(--color-dark);
      display: flex;
      align-items: center;
      justify-content: center;
      color: var(--color-light);
      font-size: 1.2rem;
    }

    .project-info {
      padding: var(--spacing-md);
    }

    .project-info h3 {
      margin-bottom: var(--spacing-sm);
      color: var(--color-dark);
    }

    .project-info p {
      color: var(--color-text-light);
      margin-bottom: var(--spacing-md);
      font-size: 0.95rem;
    }

    .project-tags {
      display: flex;
      flex-wrap: wrap;
      gap: var(--spacing-sm);
    }

    .project-tags span {
      font-size: 0.8rem;
      padding: 0.2rem 0.6rem;
      background-color: var(--color-bg-alt);
      border-radius: 4px;
      color: var(--color-text-light);
    }

    /* ===== Contact Section ===== */
    .contact {
      background-color: var(--color-bg-alt);
    }

    .contact-form {
      max-width: 600px;
      margin: 0 auto;
      display: flex;
      flex-direction: column;
      gap: var(--spacing-md);
    }

    .contact-form input,
    .contact-form textarea {
      padding: 0.8rem;
      border: 2px solid #ddd;
      border-radius: var(--border-radius);
      font-family: inherit;
      font-size: 1rem;
      transition: border-color var(--transition-speed) ease,
                  box-shadow var(--transition-speed) ease;
    }

    .contact-form input:focus,
    .contact-form textarea:focus {
      outline: none;
      border-color: var(--color-primary);
      box-shadow: 0 0 0 3px rgba(52, 152, 219, 0.2);
    }

    .contact-form textarea {
      min-height: 150px;
      resize: vertical;
    }

    .contact-form button {
      padding: 0.8rem;
      background-color: var(--color-primary);
      color: white;
      border: none;
      border-radius: var(--border-radius);
      font-size: 1rem;
      font-weight: 600;
      cursor: pointer;
      transition: background-color var(--transition-speed) ease,
                  transform 0.2s ease;
    }

    .contact-form button:hover {
      background-color: var(--color-primary-dark);
      transform: translateY(-2px);
    }

    /* ===== Footer ===== */
    .footer {
      background-color: var(--color-darker);
      color: var(--color-light);
      text-align: center;
      padding: var(--spacing-lg) var(--spacing-md);
    }

    .footer p {
      color: rgba(255, 255, 255, 0.6);
      font-size: 0.9rem;
    }

    .footer-links {
      display: flex;
      justify-content: center;
      gap: var(--spacing-md);
      margin-bottom: var(--spacing-md);
    }

    .footer-links a {
      color: var(--color-light);
      transition: color var(--transition-speed) ease;
    }

    .footer-links a:hover {
      color: var(--color-primary);
    }

    /* ===== Keyframe Animations ===== */
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

    @keyframes bounce {
      0%, 20%, 50%, 80%, 100% {
        transform: translateY(0);
      }
      40% {
        transform: translateY(-15px);
      }
      60% {
        transform: translateY(-7px);
      }
    }

    /* ===== Tablet (min-width: 576px) ===== */
    @media screen and (min-width: 576px) {
      .projects-grid {
        grid-template-columns: repeat(2, 1fr);
      }

      .about-content {
        flex-direction: row;
        text-align: left;
      }

      .about-text {
        text-align: left;
      }

      .skills-list {
        justify-content: flex-start;
      }
    }

    /* ===== Tablet Landscape (min-width: 768px) ===== */
    @media screen and (min-width: 768px) {
      .nav-hamburger {
        display: none;
      }

      .nav-links {
        position: static;
        flex-direction: row;
        max-height: none;
        overflow: visible;
        background-color: transparent;
      }

      .nav-links a {
        padding: var(--spacing-md) var(--spacing-md);
      }

      .nav-links a:hover {
        background-color: transparent;
        color: var(--color-primary);
      }

      .section {
        padding: var(--spacing-xl) var(--spacing-lg);
      }

      .hero {
        min-height: 90vh;
      }
    }

    /* ===== Desktop (min-width: 992px) ===== */
    @media screen and (min-width: 992px) {
      .projects-grid {
        grid-template-columns: repeat(3, 1fr);
      }

      .about-image {
        width: 250px;
        height: 250px;
        font-size: 4rem;
      }

      .hero {
        min-height: 100vh;
      }

      .contact-form {
        max-width: 700px;
      }

      .nav-links a {
        padding: var(--spacing-md) var(--spacing-lg);
      }
    }
  </style>
</head>
<body>

  <!-- Navigation -->
  <nav class="navbar">
    <div class="nav-inner">
      <a href="#" class="nav-logo">My<span>Portfolio</span></a>
      <input type="checkbox" id="nav-check" class="nav-checkbox" aria-label="Toggle navigation">
      <label for="nav-check" class="nav-hamburger" aria-label="Open menu">
        <span></span>
        <span></span>
        <span></span>
      </label>
      <ul class="nav-links">
        <li><a href="#hero">Home</a></li>
        <li><a href="#about">About</a></li>
        <li><a href="#projects">Projects</a></li>
        <li><a href="#contact">Contact</a></li>
      </ul>
    </div>
  </nav>

  <!-- Hero Section -->
  <section id="hero" class="hero">
    <h1>Hello, I am a Web Developer</h1>
    <p>I build responsive, accessible, and performant web experiences using modern technologies.</p>
    <a href="#projects" class="hero-btn">View My Work</a>
    <div class="scroll-indicator">
      <span></span>
    </div>
  </section>

  <!-- About Section -->
  <section id="about" class="section about">
    <div class="container">
      <h2 class="section-title">About Me</h2>
      <div class="about-content">
        <div class="about-image">JD</div>
        <div class="about-text">
          <p>I am a passionate web developer with a focus on creating clean, responsive, and user-friendly websites. I enjoy turning complex problems into simple, elegant solutions.</p>
          <p>Currently learning the MERN stack and building projects that make a difference.</p>
          <div class="skills-list">
            <span class="skill-tag">HTML5</span>
            <span class="skill-tag">CSS3</span>
            <span class="skill-tag">JavaScript</span>
            <span class="skill-tag">React</span>
            <span class="skill-tag">Node.js</span>
            <span class="skill-tag">MongoDB</span>
            <span class="skill-tag">Git</span>
            <span class="skill-tag">Responsive Design</span>
          </div>
        </div>
      </div>
    </div>
  </section>

  <!-- Projects Section -->
  <section id="projects" class="section">
    <div class="container">
      <h2 class="section-title">My Projects</h2>
      <div class="projects-grid">
        <div class="project-card">
          <div class="project-image">Project Screenshot</div>
          <div class="project-info">
            <h3>E-Commerce Store</h3>
            <p>A fully responsive online store with product filtering, cart functionality, and checkout flow.</p>
            <div class="project-tags">
              <span>HTML</span>
              <span>CSS</span>
              <span>JavaScript</span>
            </div>
          </div>
        </div>
        <div class="project-card">
          <div class="project-image">Project Screenshot</div>
          <div class="project-info">
            <h3>Weather Dashboard</h3>
            <p>A weather application that displays real-time weather data with animated icons and responsive charts.</p>
            <div class="project-tags">
              <span>React</span>
              <span>API</span>
              <span>CSS Grid</span>
            </div>
          </div>
        </div>
        <div class="project-card">
          <div class="project-image">Project Screenshot</div>
          <div class="project-info">
            <h3>Task Manager</h3>
            <p>A full-stack task management app with user authentication, CRUD operations, and drag-and-drop.</p>
            <div class="project-tags">
              <span>MongoDB</span>
              <span>Express</span>
              <span>React</span>
              <span>Node.js</span>
            </div>
          </div>
        </div>
      </div>
    </div>
  </section>

  <!-- Contact Section -->
  <section id="contact" class="section contact">
    <div class="container">
      <h2 class="section-title">Get In Touch</h2>
      <form class="contact-form" action="#" method="POST">
        <input type="text" name="name" placeholder="Your Name" required>
        <input type="email" name="email" placeholder="Your Email" required>
        <textarea name="message" placeholder="Your Message" required></textarea>
        <button type="submit">Send Message</button>
      </form>
    </div>
  </section>

  <!-- Footer -->
  <footer class="footer">
    <div class="footer-links">
      <a href="#">GitHub</a>
      <a href="#">LinkedIn</a>
      <a href="#">Twitter</a>
    </div>
    <p>&copy; 2025 MyPortfolio. All rights reserved.</p>
  </footer>

</body>
</html>
```
</details>

---

## Section F: CSS Weeks 5-8 Comprehensive Review (10 Questions)

This section serves as a phase assessment covering all CSS topics from Weeks 5 through 8: CSS fundamentals, the box model and layout, Flexbox and Grid, and responsive design with animations.

---

**1. (MCQ) Which CSS property is used to add space OUTSIDE an element's border?**

- A) `padding`
- B) `margin`
- C) `border-spacing`
- D) `outline-offset`

<details>
<summary>Answer</summary>

**B) `margin`**

In the CSS box model, `margin` is the outermost layer that creates space between the element's border and surrounding elements. `padding` adds space inside the border, between the border and the content.
</details>

---

**2. (MCQ) What does `box-sizing: border-box` do?**

- A) Removes the element's border
- B) Includes padding and border in the element's total width and height
- C) Adds a box shadow to the element
- D) Makes the element a block-level element

<details>
<summary>Answer</summary>

**B) Includes padding and border in the element's total width and height**

With `border-box`, if you set `width: 300px`, the element's total rendered width will be 300px including padding and border. Without it (default `content-box`), padding and border are added on top of the specified width.
</details>

---

**3. (MCQ) Which Flexbox property is used to align items along the cross axis?**

- A) `justify-content`
- B) `align-items`
- C) `flex-direction`
- D) `flex-wrap`

<details>
<summary>Answer</summary>

**B) `align-items`**

`align-items` aligns flex items along the cross axis (vertically in a row layout, horizontally in a column layout). `justify-content` aligns items along the main axis.
</details>

---

**4. (MCQ) Which CSS Grid property creates a grid with three equal columns?**

- A) `grid-template-columns: 3fr;`
- B) `grid-template-columns: repeat(3, 1fr);`
- C) `grid-columns: 3;`
- D) `grid-template-columns: auto auto auto auto;`

<details>
<summary>Answer</summary>

**B) `grid-template-columns: repeat(3, 1fr);`**

`repeat(3, 1fr)` creates three columns that each take up one fraction of the available space, making them equal in width.
</details>

---

**5. (MCQ) What is the correct order of properties in the CSS box model, from innermost to outermost?**

- A) Margin, Border, Padding, Content
- B) Content, Padding, Border, Margin
- C) Content, Border, Padding, Margin
- D) Padding, Content, Border, Margin

<details>
<summary>Answer</summary>

**B) Content, Padding, Border, Margin**

The box model layers from inside out are: Content (the actual text/image), Padding (space around content), Border (the border around padding), and Margin (space outside the border).
</details>

---

**6. (Coding) Write CSS to create a centered card component that is 300px wide, has 20px of padding, a 1px solid gray border, and a subtle shadow. Use `box-sizing: border-box`.**

<details>
<summary>Answer</summary>

```css
.card {
  width: 300px;
  padding: 20px;
  border: 1px solid #ccc;
  box-shadow: 0 2px 8px rgba(0, 0, 0, 0.1);
  box-sizing: border-box;
  border-radius: 8px;
  margin: 0 auto;
}
```

With `border-box`, the total width remains 300px even with padding and border included. `margin: 0 auto` centers the block-level element horizontally.
</details>

---

**7. (Coding) Using Flexbox, write CSS to create a navigation bar where the logo is on the left and the links are on the right, vertically centered.**

<details>
<summary>Answer</summary>

```css
.navbar {
  display: flex;
  justify-content: space-between;
  align-items: center;
  padding: 1rem 2rem;
  background-color: #2c3e50;
}

.logo {
  font-size: 1.5rem;
  font-weight: bold;
  color: white;
}

.nav-links {
  display: flex;
  list-style: none;
  gap: 1.5rem;
}

.nav-links a {
  color: white;
  text-decoration: none;
}
```

`justify-content: space-between` pushes the logo and links to opposite ends. `align-items: center` vertically centers them.
</details>

---

**8. (Coding) Using CSS Grid, create a layout where a sidebar takes up 250px on the left and the main content fills the remaining space. On screens smaller than 768px, stack them vertically.**

<details>
<summary>Answer</summary>

```css
.layout {
  display: grid;
  grid-template-columns: 1fr;
  gap: 1rem;
}

.sidebar {
  background-color: #f0f0f0;
  padding: 1.5rem;
}

.main-content {
  padding: 1.5rem;
}

@media screen and (min-width: 768px) {
  .layout {
    grid-template-columns: 250px 1fr;
  }
}
```

On mobile, both elements stack in a single column. On screens 768px and wider, the sidebar takes a fixed 250px and the main content fills the rest with `1fr`.
</details>

---

**9. (Coding) Write a CSS rule that uses a media query, a CSS variable, a transition, and a transform. The rule should make a `.card` element scale up slightly on hover, but only on screens wider than 992px.**

<details>
<summary>Answer</summary>

```css
:root {
  --card-scale: 1.05;
  --transition-speed: 0.3s;
}

.card {
  transition: transform var(--transition-speed) ease,
              box-shadow var(--transition-speed) ease;
}

@media screen and (min-width: 992px) {
  .card:hover {
    transform: scale(var(--card-scale));
    box-shadow: 0 8px 25px rgba(0, 0, 0, 0.15);
  }
}
```

This combines CSS variables (`--card-scale`, `--transition-speed`), a transition, a transform (`scale`), and a media query to only apply the hover effect on desktop screens.
</details>

---

**10. (Coding) Write a complete CSS snippet that demonstrates all four major CSS concepts from Weeks 5-8: box model properties, Flexbox, CSS Grid, and a responsive media query with an animation.**

<details>
<summary>Answer</summary>

```css
/* Week 5: CSS Fundamentals - Box Model */
* {
  margin: 0;
  padding: 0;
  box-sizing: border-box;
}

body {
  font-family: 'Segoe UI', sans-serif;
  color: #333;
}

/* Week 6: Box Model & Layout */
.container {
  max-width: 1200px;
  margin: 0 auto;
  padding: 2rem;
}

.card {
  padding: 1.5rem;
  margin-bottom: 1rem;
  border: 1px solid #ddd;
  border-radius: 8px;
  box-shadow: 0 2px 8px rgba(0, 0, 0, 0.1);
}

/* Week 7: Flexbox */
.navbar {
  display: flex;
  justify-content: space-between;
  align-items: center;
  padding: 1rem 2rem;
  background-color: #2c3e50;
}

.nav-links {
  display: flex;
  gap: 1.5rem;
  list-style: none;
}

/* Week 7: CSS Grid */
.projects {
  display: grid;
  grid-template-columns: 1fr;
  gap: 1.5rem;
}

/* Week 8: Responsive Design */
@media screen and (min-width: 768px) {
  .projects {
    grid-template-columns: repeat(2, 1fr);
  }
}

@media screen and (min-width: 992px) {
  .projects {
    grid-template-columns: repeat(3, 1fr);
  }
}

/* Week 8: CSS Animation */
@keyframes slideIn {
  from {
    opacity: 0;
    transform: translateY(20px);
  }
  to {
    opacity: 1;
    transform: translateY(0);
  }
}

.card {
  animation: slideIn 0.5s ease-out;
  transition: transform 0.3s ease, box-shadow 0.3s ease;
}

.card:hover {
  transform: translateY(-5px);
  box-shadow: 0 8px 20px rgba(0, 0, 0, 0.15);
}
```

This snippet demonstrates:
- **Week 5 (CSS Fundamentals):** Reset, font styling, and basic selectors.
- **Week 6 (Box Model & Layout):** `box-sizing`, `margin`, `padding`, `border`, and `box-shadow`.
- **Week 7 (Flexbox & Grid):** Flexbox for the navbar and CSS Grid for the project layout.
- **Week 8 (Responsive & Animations):** Media queries for responsive breakpoints, `@keyframes` for entry animation, and transitions for hover effects.
</details>

---

**End of Practice Questions**

Total: 53 questions across 6 sections.
