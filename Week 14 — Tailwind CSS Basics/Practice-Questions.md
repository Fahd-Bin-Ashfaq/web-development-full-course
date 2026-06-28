# Week 14: Tailwind CSS Basics — Practice Questions

**Total Questions: 38**

| Section | Type | Count |
|---------|------|-------|
| A | Multiple Choice Questions | 15 |
| B | Short Answer Questions | 8 |
| C | True or False | 10 |
| D | Coding Exercises | 5 |

---

## Section A: Multiple Choice Questions (MCQs)

**Q1.** What type of CSS framework is Tailwind CSS?

- A) Component-based framework
- B) Utility-first framework
- C) Semantic framework
- D) Object-oriented framework

<details>
<summary>Answer</summary>

**B) Utility-first framework**

Tailwind CSS is a utility-first CSS framework that provides low-level utility classes (such as `p-4`, `text-center`, `bg-blue-500`) which can be composed directly in HTML to build custom designs without writing custom CSS.
</details>

---

**Q2.** Which class applies a padding of `1rem` (16px) on all sides of an element?

- A) `p-2`
- B) `p-4`
- C) `p-8`
- D) `p-16`

<details>
<summary>Answer</summary>

**B) `p-4`**

In Tailwind's default spacing scale, each unit equals `0.25rem`. So `p-4` applies `1rem` (4 x 0.25rem = 1rem = 16px) of padding on all four sides. `p-2` would be `0.5rem`, `p-8` would be `2rem`, and `p-16` would be `4rem`.
</details>

---

**Q3.** What does the class `text-red-500` do?

- A) Sets the background color to red with 500ms animation
- B) Sets the text color to a medium shade of red
- C) Sets the font size to 500px in red
- D) Sets the border color to red

<details>
<summary>Answer</summary>

**B) Sets the text color to a medium shade of red**

In Tailwind, `text-{color}-{shade}` sets the text color. The number `500` represents the shade intensity on a scale from 50 (lightest) to 950 (darkest). A value of 500 is the base or medium shade of the color.
</details>

---

**Q4.** Which responsive prefix targets screens that are **768px and wider** in Tailwind's default breakpoints?

- A) `sm:`
- B) `md:`
- C) `lg:`
- D) `xl:`

<details>
<summary>Answer</summary>

**B) `md:`**

Tailwind's default breakpoints are: `sm` (640px), `md` (768px), `lg` (1024px), `xl` (1280px), and `2xl` (1536px). The `md:` prefix applies styles at 768px and above.
</details>

---

**Q5.** What does the class `flex` do when applied to an element?

- A) Sets the element to `display: inline-flex`
- B) Sets the element to `display: flex`
- C) Sets the element to `display: block` with flex wrapping
- D) Sets the element to `display: grid`

<details>
<summary>Answer</summary>

**B) Sets the element to `display: flex`**

The `flex` utility class applies `display: flex` to the element, turning it into a flex container. Its direct children become flex items that can be positioned using additional flex utility classes such as `justify-center`, `items-center`, and `flex-col`.
</details>

---

**Q6.** Which class is used to center flex items along the **cross axis**?

- A) `justify-center`
- B) `items-center`
- C) `text-center`
- D) `align-center`

<details>
<summary>Answer</summary>

**B) `items-center`**

`items-center` applies `align-items: center`, which centers flex items along the cross axis (vertically in a row layout). `justify-center` centers items along the main axis. `text-center` centers inline text content. There is no `align-center` class in Tailwind.
</details>

---

**Q7.** How do you apply a style **only on hover** in Tailwind CSS?

- A) `onhover:bg-blue-500`
- B) `hover-bg-blue-500`
- C) `hover:bg-blue-500`
- D) `:hover-bg-blue-500`

<details>
<summary>Answer</summary>

**C) `hover:bg-blue-500`**

Tailwind uses state variant prefixes with a colon. The `hover:` prefix applies the following utility only when the user hovers over the element. For example, `hover:bg-blue-500` changes the background color to blue on hover.
</details>

---

**Q8.** Which class creates a three-column grid layout?

- A) `grid grid-cols-3`
- B) `flex flex-3`
- C) `columns-3`
- D) `grid-3-col`

<details>
<summary>Answer</summary>

**A) `grid grid-cols-3`**

To create a grid layout, you first apply the `grid` class (which sets `display: grid`) and then use `grid-cols-3` to define three equal-width columns. The resulting CSS is `grid-template-columns: repeat(3, minmax(0, 1fr))`.
</details>

---

**Q9.** What does the class `mx-auto` do?

- A) Sets the maximum width to auto
- B) Centers the element horizontally by setting left and right margins to auto
- C) Sets all margins to automatic values
- D) Applies a horizontal media query

<details>
<summary>Answer</summary>

**B) Centers the element horizontally by setting left and right margins to auto**

The `mx-auto` class applies `margin-left: auto` and `margin-right: auto`, which centers a block-level element horizontally within its parent. The `mx` prefix refers to horizontal (x-axis) margins.
</details>

---

**Q10.** Which class makes an element take the full width of its parent?

- A) `w-100`
- B) `w-full`
- C) `w-screen`
- D) `w-max`

<details>
<summary>Answer</summary>

**B) `w-full`**

`w-full` applies `width: 100%`, making the element span the entire width of its parent container. `w-screen` sets the width to `100vw` (the full viewport width), `w-max` sets `width: max-content`, and `w-100` sets a fixed width of `25rem` in Tailwind v3+.
</details>

---

**Q11.** What does `gap-4` do in a grid or flex container?

- A) Adds 4px of padding inside each child
- B) Adds a `1rem` gap between rows and columns
- C) Adds a 4% margin around the container
- D) Adds a 4-pixel border between elements

<details>
<summary>Answer</summary>

**B) Adds a `1rem` gap between rows and columns**

The `gap-4` class applies `gap: 1rem` (4 x 0.25rem) to a grid or flex container, creating equal spacing between all child elements. You can also use `gap-x-4` for column gaps only or `gap-y-4` for row gaps only.
</details>

---

**Q12.** Which Tailwind class applies a **box shadow** to an element?

- A) `shadow`
- B) `box-shadow`
- C) `drop-shadow`
- D) `border-shadow`

<details>
<summary>Answer</summary>

**A) `shadow`**

Tailwind provides shadow utilities such as `shadow-sm`, `shadow`, `shadow-md`, `shadow-lg`, `shadow-xl`, and `shadow-2xl`. The `shadow` class applies a medium default box shadow. `drop-shadow` applies a filter-based drop shadow, which is a different effect.
</details>

---

**Q13.** What does the class `rounded-lg` do?

- A) Rotates the element by a large angle
- B) Applies a large border radius to round the corners
- C) Makes the element circular
- D) Rounds the font size to the nearest large value

<details>
<summary>Answer</summary>

**B) Applies a large border radius to round the corners**

`rounded-lg` applies `border-radius: 0.5rem` (8px), creating rounded corners. Tailwind offers a scale from `rounded-none` (0) to `rounded-full` (9999px, which creates a circle or pill shape).
</details>

---

**Q14.** Which class would you use to hide an element on small screens but show it on medium screens and above?

- A) `visible md:hidden`
- B) `hidden md:block`
- C) `block md:hidden`
- D) `display-none md:display-block`

<details>
<summary>Answer</summary>

**B) `hidden md:block`**

`hidden` applies `display: none` by default (on all screen sizes). The `md:block` prefix overrides this at the `md` breakpoint (768px) and above, setting `display: block`. Tailwind uses a mobile-first approach, so unprefixed classes apply to all sizes and prefixed classes apply from that breakpoint upward.
</details>

---

**Q15.** What is the default design approach in Tailwind CSS for responsive breakpoints?

- A) Desktop-first (styles apply to large screens and are overridden for smaller screens)
- B) Mobile-first (styles apply to all sizes and are overridden at larger breakpoints)
- C) Tablet-first (styles target medium screens by default)
- D) No default approach; the developer must specify each breakpoint explicitly

<details>
<summary>Answer</summary>

**B) Mobile-first (styles apply to all sizes and are overridden at larger breakpoints)**

Tailwind CSS follows a mobile-first methodology. Unprefixed utility classes apply at all screen sizes. Responsive prefixes like `sm:`, `md:`, `lg:` act as **minimum-width** breakpoints, meaning styles apply from that breakpoint and above. For example, `bg-red-500 md:bg-blue-500` gives a red background on mobile and blue from 768px upward.
</details>

---

## Section B: Short Answer Questions

**Q1.** What is the "utility-first" approach in Tailwind CSS, and how does it differ from writing traditional CSS?

<details>
<summary>Answer</summary>

The **utility-first approach** means building designs by applying small, single-purpose CSS classes directly in your HTML markup rather than writing custom CSS rules in separate stylesheets.

**Traditional CSS approach:**
```html
<div class="card">Welcome</div>
```
```css
.card {
  padding: 1rem;
  background-color: white;
  border-radius: 0.5rem;
  box-shadow: 0 1px 3px rgba(0, 0, 0, 0.1);
}
```

**Tailwind utility-first approach:**
```html
<div class="p-4 bg-white rounded-lg shadow">Welcome</div>
```

With utilities, you avoid context-switching between HTML and CSS files, eliminate the need to invent class names, and reduce the total amount of CSS shipped because utilities are reused across components. The trade-off is that your HTML contains more class names, which some developers find verbose at first.
</details>

---

**Q2.** How does Tailwind CSS compare to Bootstrap? List at least three key differences.

<details>
<summary>Answer</summary>

| Aspect | Tailwind CSS | Bootstrap |
|--------|-------------|-----------|
| **Approach** | Utility-first — provides low-level utility classes to build custom designs | Component-based — provides pre-designed, opinionated components (buttons, cards, navbars) |
| **Customization** | Highly customizable; every design is built from scratch using utilities, so no two projects look alike | Requires overriding existing component styles to deviate from the default Bootstrap look |
| **File size** | Uses a JIT (Just-In-Time) compiler that generates only the CSS classes you actually use, resulting in very small production builds | Ships a larger CSS bundle that includes all component styles, although unused styles can be purged |
| **Learning curve** | Steeper initial learning curve because you must learn many utility class names | Easier to start with because pre-built components work out of the box |
| **JavaScript** | Does not include JavaScript; you pair it with a JS framework of your choice | Includes JavaScript plugins for dropdowns, modals, carousels, and other interactive components |
</details>

---

**Q3.** Explain how responsive design works in Tailwind CSS. What does "mobile-first" mean in this context?

<details>
<summary>Answer</summary>

Tailwind CSS uses a **mobile-first** responsive system. This means:

1. **Unprefixed classes** apply at **all screen sizes**, starting from the smallest.
2. **Responsive prefixes** (`sm:`, `md:`, `lg:`, `xl:`, `2xl:`) act as **minimum-width media queries**. A prefixed class applies from that breakpoint and above.

**Default breakpoints:**
- `sm` — 640px and above
- `md` — 768px and above
- `lg` — 1024px and above
- `xl` — 1280px and above
- `2xl` — 1536px and above

**Example:**
```html
<div class="text-sm md:text-base lg:text-lg">
  Responsive text
</div>
```

- On screens below 768px: `text-sm` applies (small font).
- From 768px to 1023px: `md:text-base` overrides (medium font).
- From 1024px and above: `lg:text-lg` overrides (large font).

You design for mobile first and then layer on changes for progressively larger screens.
</details>

---

**Q4.** What is the `tailwind.config.js` file, and why is it important?

<details>
<summary>Answer</summary>

The `tailwind.config.js` file is Tailwind's **configuration file** where you customize and extend the default design system. It is created by running `npx tailwindcss init` and allows you to:

1. **Define content sources** — specify which files Tailwind should scan for class names (used for tree-shaking unused styles in production).
2. **Extend the theme** — add custom colors, spacing values, fonts, breakpoints, and other design tokens.
3. **Override defaults** — replace Tailwind's default values with your own.
4. **Add plugins** — integrate official or community plugins for forms, typography, aspect ratios, and more.

**Example:**
```js
module.exports = {
  content: ["./src/**/*.{html,js,jsx,ts,tsx}"],
  theme: {
    extend: {
      colors: {
        brand: "#1a73e8",
      },
      fontFamily: {
        heading: ["Poppins", "sans-serif"],
      },
    },
  },
  plugins: [],
};
```

Without this file, Tailwind uses its default configuration. The file is important because it lets you tailor the framework to your project's design requirements.
</details>

---

**Q5.** Explain the Tailwind spacing scale. How do classes like `p-1`, `p-2`, `p-4`, and `p-8` translate to actual CSS values?

<details>
<summary>Answer</summary>

Tailwind uses a **numeric spacing scale** where each unit equals **0.25rem** (4px at the default browser font size of 16px).

| Class | Calculation | CSS Value |
|-------|-------------|-----------|
| `p-0` | 0 x 0.25rem | `padding: 0` |
| `p-1` | 1 x 0.25rem | `padding: 0.25rem` (4px) |
| `p-2` | 2 x 0.25rem | `padding: 0.5rem` (8px) |
| `p-3` | 3 x 0.25rem | `padding: 0.75rem` (12px) |
| `p-4` | 4 x 0.25rem | `padding: 1rem` (16px) |
| `p-6` | 6 x 0.25rem | `padding: 1.5rem` (24px) |
| `p-8` | 8 x 0.25rem | `padding: 2rem` (32px) |
| `p-12` | 12 x 0.25rem | `padding: 3rem` (48px) |

This same scale applies to margin (`m-`), width (`w-`), height (`h-`), gap (`gap-`), and other spacing-related properties. You can also target specific sides: `pt-` (top), `pb-` (bottom), `pl-` (left), `pr-` (right), `px-` (horizontal), `py-` (vertical).
</details>

---

**Q6.** How do you apply hover and focus states in Tailwind CSS? Provide examples.

<details>
<summary>Answer</summary>

Tailwind uses **state variant prefixes** followed by a colon to apply styles conditionally based on user interaction:

**Hover state — `hover:`**
```html
<button class="bg-blue-500 hover:bg-blue-700 text-white py-2 px-4 rounded">
  Hover Me
</button>
```
The background changes from `blue-500` to `blue-700` when the user hovers over the button.

**Focus state — `focus:`**
```html
<input
  class="border border-gray-300 focus:border-blue-500 focus:ring-2 focus:ring-blue-200 rounded px-3 py-2"
  type="text"
  placeholder="Focus on me"
/>
```
The border turns blue and a ring appears when the input receives focus.

**Other common state variants:**
- `active:` — applied while the element is being clicked
- `disabled:` — applied when the element has the `disabled` attribute
- `focus-within:` — applied when any child of the element has focus
- `group-hover:` — applied when a parent marked with `group` is hovered

These variants can be combined: `hover:focus:bg-green-500` applies only when the element is both hovered and focused.
</details>

---

**Q7.** What are Tailwind's flex-direction utilities, and when would you use each one?

<details>
<summary>Answer</summary>

Tailwind provides four `flex-direction` utilities:

| Class | CSS | Description |
|-------|-----|-------------|
| `flex-row` | `flex-direction: row` | Items are placed horizontally, left to right (default) |
| `flex-row-reverse` | `flex-direction: row-reverse` | Items are placed horizontally, right to left |
| `flex-col` | `flex-direction: column` | Items are stacked vertically, top to bottom |
| `flex-col-reverse` | `flex-direction: column-reverse` | Items are stacked vertically, bottom to top |

**Common use case — responsive navigation:**
```html
<nav class="flex flex-col md:flex-row gap-4">
  <a href="#">Home</a>
  <a href="#">About</a>
  <a href="#">Contact</a>
</nav>
```

On mobile, `flex-col` stacks the navigation links vertically. From the `md` breakpoint and above, `md:flex-row` arranges them horizontally. This is a very common responsive pattern in Tailwind.
</details>

---

**Q8.** How can you customize the default color palette in Tailwind? What is the difference between `extend` and replacing a color?

<details>
<summary>Answer</summary>

You customize colors in the `tailwind.config.js` file under the `theme` key.

**Extending (adding new colors while keeping all defaults):**
```js
module.exports = {
  theme: {
    extend: {
      colors: {
        brand: {
          light: "#93c5fd",
          DEFAULT: "#3b82f6",
          dark: "#1d4ed8",
        },
      },
    },
  },
};
```
This adds `brand-light`, `brand`, and `brand-dark` as new color utilities (e.g., `text-brand`, `bg-brand-dark`) while keeping all of Tailwind's default colors available.

**Replacing (overriding the entire color palette):**
```js
module.exports = {
  theme: {
    colors: {
      primary: "#1a73e8",
      secondary: "#f59e0b",
      white: "#ffffff",
      black: "#000000",
    },
  },
};
```
Placing colors directly under `theme.colors` (without `extend`) **replaces** the entire default palette. Only the colors you define will be available. This approach is useful when you want strict control over which colors are allowed in your project.
</details>

---

## Section C: True or False

| # | Statement | Answer |
|---|-----------|--------|
| 1 | Tailwind CSS requires you to write custom CSS for every component. | <details><summary>Answer</summary>**False.** Tailwind provides utility classes that you compose directly in HTML. You rarely need to write custom CSS.</details> |
| 2 | The class `mt-4` applies a top margin of `1rem`. | <details><summary>Answer</summary>**True.** `mt-4` stands for `margin-top: 1rem` (4 x 0.25rem = 1rem).</details> |
| 3 | In Tailwind, the `sm:` prefix targets screens **smaller** than 640px. | <details><summary>Answer</summary>**False.** The `sm:` prefix is a minimum-width breakpoint that targets screens **640px and wider**. Tailwind is mobile-first, so prefixes apply from that breakpoint upward.</details> |
| 4 | The class `bg-green-900` produces a darker shade of green than `bg-green-300`. | <details><summary>Answer</summary>**True.** Higher numbers in Tailwind's color scale represent darker shades. `900` is near the darkest end, while `300` is a lighter shade.</details> |
| 5 | You can combine multiple responsive prefixes on the same element, such as `sm:text-sm md:text-base lg:text-lg`. | <details><summary>Answer</summary>**True.** You can apply different utilities at different breakpoints. Tailwind applies each prefixed class starting from its respective breakpoint and above.</details> |
| 6 | The `hidden` class in Tailwind sets `visibility: hidden` on the element. | <details><summary>Answer</summary>**False.** The `hidden` class applies `display: none`, which completely removes the element from the layout. To set `visibility: hidden` (which hides the element but preserves its space), you use the `invisible` class.</details> |
| 7 | Tailwind's JIT (Just-In-Time) mode generates only the CSS classes that are actually used in your project. | <details><summary>Answer</summary>**True.** JIT mode scans your content files and generates CSS on-demand for only the classes it finds, resulting in much smaller production builds.</details> |
| 8 | The class `space-x-4` adds horizontal spacing between child elements inside a container. | <details><summary>Answer</summary>**True.** `space-x-4` adds `1rem` of horizontal margin between adjacent child elements using the `> * + *` selector. It is a convenient alternative to applying individual margins.</details> |
| 9 | Tailwind CSS comes with pre-built JavaScript components like modals and carousels. | <details><summary>Answer</summary>**False.** Tailwind CSS is a CSS-only framework. It does not include any JavaScript. For interactive components, you need to write your own JavaScript or use a companion library such as Headless UI.</details> |
| 10 | The class `container` in Tailwind automatically centers itself and applies responsive max-widths. | <details><summary>Answer</summary>**True.** The `container` class sets `max-width` to match the current breakpoint and, when combined with `mx-auto`, centers itself horizontally. By default, it does not include `mx-auto` unless configured in `tailwind.config.js`.</details> |

---

## Section D: Coding Exercises

### Exercise 1: Style a Card Component

Create an HTML card component using **only Tailwind CSS utility classes**. The card should include:
- A card container with white background, rounded corners, a shadow, and padding
- A title in bold, large text
- A description paragraph in gray text
- A "Read More" link in blue that turns darker blue on hover

<details>
<summary>Solution</summary>

```html
<div class="max-w-sm mx-auto bg-white rounded-lg shadow-md p-6">
  <h2 class="text-xl font-bold text-gray-800 mb-2">
    Card Title
  </h2>
  <p class="text-gray-600 mb-4">
    This is a short description for the card component. It provides a
    brief overview of the content and encourages the reader to learn more.
  </p>
  <a
    href="#"
    class="text-blue-500 hover:text-blue-700 font-medium"
  >
    Read More &rarr;
  </a>
</div>
```

**Explanation of key classes:**
- `max-w-sm` — limits the card width to 24rem (384px)
- `mx-auto` — centers the card horizontally
- `bg-white` — white background
- `rounded-lg` — rounded corners (0.5rem border radius)
- `shadow-md` — medium box shadow for depth
- `p-6` — 1.5rem padding on all sides
- `text-xl font-bold` — large, bold title text
- `text-gray-600` — medium gray for the description
- `mb-2` / `mb-4` — bottom margin for spacing between elements
- `hover:text-blue-700` — darker blue text on hover
</details>

---

### Exercise 2: Create a Responsive Navbar

Build a responsive navigation bar using Tailwind CSS that:
- Displays the brand name on the left
- Shows navigation links horizontally on medium screens and above
- Stacks the links vertically on small screens
- Has a colored background with white text

<details>
<summary>Solution</summary>

```html
<nav class="bg-blue-600 text-white px-6 py-4">
  <div class="max-w-6xl mx-auto flex flex-col md:flex-row md:items-center md:justify-between gap-4">

    <!-- Brand -->
    <div class="text-xl font-bold">
      MyBrand
    </div>

    <!-- Navigation Links -->
    <ul class="flex flex-col md:flex-row gap-2 md:gap-6">
      <li>
        <a href="#" class="hover:text-blue-200 transition-colors">Home</a>
      </li>
      <li>
        <a href="#" class="hover:text-blue-200 transition-colors">About</a>
      </li>
      <li>
        <a href="#" class="hover:text-blue-200 transition-colors">Services</a>
      </li>
      <li>
        <a href="#" class="hover:text-blue-200 transition-colors">Contact</a>
      </li>
    </ul>

  </div>
</nav>
```

**Explanation of key classes:**
- `bg-blue-600 text-white` — blue background with white text
- `flex flex-col md:flex-row` — links stack vertically on mobile, horizontally from 768px
- `md:items-center md:justify-between` — vertically centers items and pushes brand and links to opposite ends on larger screens
- `gap-2 md:gap-6` — spacing between links adapts to screen size
- `hover:text-blue-200 transition-colors` — subtle hover effect with a smooth color transition
</details>

---

### Exercise 3: Build a Button Set with Hover Effects

Create a set of four buttons using Tailwind CSS with the following styles:
1. **Primary** — blue background, white text, darker blue on hover
2. **Secondary** — gray background, white text, darker gray on hover
3. **Success** — green background, white text, darker green on hover
4. **Danger** — red background, white text, darker red on hover, slightly transparent when disabled

Each button should have rounded corners, padding, and a smooth transition effect.

<details>
<summary>Solution</summary>

```html
<div class="flex flex-wrap gap-4 p-8">

  <!-- Primary Button -->
  <button class="bg-blue-500 hover:bg-blue-700 text-white font-semibold py-2 px-6 rounded-lg transition-colors duration-200">
    Primary
  </button>

  <!-- Secondary Button -->
  <button class="bg-gray-500 hover:bg-gray-700 text-white font-semibold py-2 px-6 rounded-lg transition-colors duration-200">
    Secondary
  </button>

  <!-- Success Button -->
  <button class="bg-green-500 hover:bg-green-700 text-white font-semibold py-2 px-6 rounded-lg transition-colors duration-200">
    Success
  </button>

  <!-- Danger Button -->
  <button class="bg-red-500 hover:bg-red-700 text-white font-semibold py-2 px-6 rounded-lg transition-colors duration-200 disabled:opacity-50 disabled:cursor-not-allowed" disabled>
    Danger (Disabled)
  </button>

</div>
```

**Explanation of key classes:**
- `bg-{color}-500 hover:bg-{color}-700` — base color shifts to a darker shade on hover
- `font-semibold` — semi-bold text for button labels
- `py-2 px-6` — vertical and horizontal padding
- `rounded-lg` — rounded corners
- `transition-colors duration-200` — smooth 200ms color transition
- `disabled:opacity-50 disabled:cursor-not-allowed` — reduces opacity and changes cursor for disabled buttons
- `flex flex-wrap gap-4` — buttons wrap to the next line on narrow screens with consistent spacing
</details>

---

### Exercise 4: Create a Hero Section

Build a full-width hero section with:
- A background color or gradient
- Centered text with a large heading and a subtitle
- A call-to-action button
- Responsive text sizing (larger text on bigger screens)

<details>
<summary>Solution</summary>

```html
<section class="bg-gradient-to-r from-blue-600 to-purple-600 text-white py-20 px-6">
  <div class="max-w-4xl mx-auto text-center">

    <!-- Heading -->
    <h1 class="text-3xl md:text-5xl lg:text-6xl font-bold mb-4">
      Build Modern Websites with Tailwind CSS
    </h1>

    <!-- Subtitle -->
    <p class="text-lg md:text-xl lg:text-2xl text-blue-100 mb-8 max-w-2xl mx-auto">
      A utility-first CSS framework that gives you the building blocks
      to create any design directly in your markup.
    </p>

    <!-- Call to Action -->
    <a
      href="#"
      class="inline-block bg-white text-blue-600 font-bold py-3 px-8 rounded-full hover:bg-blue-50 transition-colors duration-200 text-lg"
    >
      Get Started
    </a>

  </div>
</section>
```

**Explanation of key classes:**
- `bg-gradient-to-r from-blue-600 to-purple-600` — horizontal gradient from blue to purple
- `py-20 px-6` — generous vertical padding with horizontal padding for mobile
- `text-3xl md:text-5xl lg:text-6xl` — responsive heading that grows with screen size
- `max-w-4xl mx-auto text-center` — centers content with a maximum width
- `text-blue-100` — light tint for the subtitle that contrasts well on the gradient
- `rounded-full` — pill-shaped button
- `inline-block` — ensures the anchor element respects padding and width like a button
</details>

---

### Exercise 5: Build a Responsive Grid Layout

Create a responsive grid of six content cards that arranges as follows:
- **Mobile:** 1 column (cards stack)
- **Tablet (md):** 2 columns
- **Desktop (lg):** 3 columns

Each card should have a number, a title, and a short description.

<details>
<summary>Solution</summary>

```html
<div class="max-w-6xl mx-auto px-6 py-12">
  <h2 class="text-2xl font-bold text-gray-800 text-center mb-8">
    Our Features
  </h2>

  <div class="grid grid-cols-1 md:grid-cols-2 lg:grid-cols-3 gap-6">

    <!-- Card 1 -->
    <div class="bg-white rounded-lg shadow p-6">
      <span class="inline-block bg-blue-100 text-blue-600 text-sm font-bold px-3 py-1 rounded-full mb-3">01</span>
      <h3 class="text-lg font-semibold text-gray-800 mb-2">Fast Performance</h3>
      <p class="text-gray-600 text-sm">Optimized for speed with minimal CSS output in production builds.</p>
    </div>

    <!-- Card 2 -->
    <div class="bg-white rounded-lg shadow p-6">
      <span class="inline-block bg-green-100 text-green-600 text-sm font-bold px-3 py-1 rounded-full mb-3">02</span>
      <h3 class="text-lg font-semibold text-gray-800 mb-2">Responsive Design</h3>
      <p class="text-gray-600 text-sm">Built-in responsive modifiers make adapting layouts effortless.</p>
    </div>

    <!-- Card 3 -->
    <div class="bg-white rounded-lg shadow p-6">
      <span class="inline-block bg-purple-100 text-purple-600 text-sm font-bold px-3 py-1 rounded-full mb-3">03</span>
      <h3 class="text-lg font-semibold text-gray-800 mb-2">Customizable</h3>
      <p class="text-gray-600 text-sm">Tailor every design token through the configuration file.</p>
    </div>

    <!-- Card 4 -->
    <div class="bg-white rounded-lg shadow p-6">
      <span class="inline-block bg-yellow-100 text-yellow-600 text-sm font-bold px-3 py-1 rounded-full mb-3">04</span>
      <h3 class="text-lg font-semibold text-gray-800 mb-2">Utility-First</h3>
      <p class="text-gray-600 text-sm">Compose designs with low-level utility classes instead of opinionated components.</p>
    </div>

    <!-- Card 5 -->
    <div class="bg-white rounded-lg shadow p-6">
      <span class="inline-block bg-red-100 text-red-600 text-sm font-bold px-3 py-1 rounded-full mb-3">05</span>
      <h3 class="text-lg font-semibold text-gray-800 mb-2">Developer Experience</h3>
      <p class="text-gray-600 text-sm">Enjoy rapid prototyping with instant feedback and IntelliSense support.</p>
    </div>

    <!-- Card 6 -->
    <div class="bg-white rounded-lg shadow p-6">
      <span class="inline-block bg-indigo-100 text-indigo-600 text-sm font-bold px-3 py-1 rounded-full mb-3">06</span>
      <h3 class="text-lg font-semibold text-gray-800 mb-2">Community & Plugins</h3>
      <p class="text-gray-600 text-sm">Rich ecosystem of official plugins and community-driven extensions.</p>
    </div>

  </div>
</div>
```

**Explanation of key classes:**
- `grid grid-cols-1 md:grid-cols-2 lg:grid-cols-3` — responsive column layout: 1 column on mobile, 2 on tablet, 3 on desktop
- `gap-6` — 1.5rem spacing between all cards
- `max-w-6xl mx-auto` — constrains the grid width and centers it
- `px-6 py-12` — outer padding for spacing from the viewport edges
- Each card uses `bg-white rounded-lg shadow p-6` for a clean, elevated appearance
- Colored badge spans use `bg-{color}-100 text-{color}-600` for a soft, tinted look
</details>

---

**End of Practice Questions — Week 14: Tailwind CSS Basics**
