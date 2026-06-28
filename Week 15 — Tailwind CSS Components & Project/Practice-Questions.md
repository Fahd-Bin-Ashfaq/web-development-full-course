# Week 15: Tailwind CSS Components & Project — Practice Questions

**Total Questions: 20**

| Section | Type | Count |
|---------|------|-------|
| A | Multiple Choice Questions | 10 |
| B | Short Answer Questions | 5 |
| C | Coding Exercises | 5 |

---

## Section A: Multiple Choice Questions (MCQs)

**Q1.** How do you enable dark mode in Tailwind CSS using the `class` strategy?

- A) Add `dark-mode: true` to your HTML
- B) Set `darkMode: 'class'` in `tailwind.config.js` and toggle the `dark` class on the `<html>` element
- C) Use the `@dark` directive in your CSS file
- D) Dark mode is enabled by default and cannot be configured

<details>
<summary>Answer</summary>

**B) Set `darkMode: 'class'` in `tailwind.config.js` and toggle the `dark` class on the `<html>` element**

When you configure `darkMode: 'class'` in your Tailwind config, you can prefix any utility with `dark:` to apply it only when the `dark` class is present on the `<html>` element. For example, `dark:bg-gray-900` sets a dark background in dark mode. You control the toggle via JavaScript by adding or removing the `dark` class.
</details>

---

**Q2.** What does the `dark:bg-gray-900` class do?

- A) Always sets the background to dark gray
- B) Sets the background to dark gray only when dark mode is active
- C) Sets the background to dark gray on hover
- D) Sets the background to dark gray on screens larger than 900px

<details>
<summary>Answer</summary>

**B) Sets the background to dark gray only when dark mode is active**

The `dark:` prefix is a conditional variant that applies the following utility only when dark mode is enabled. When using the `class` strategy, this means the `dark` class must be present on the `<html>` element. When using the `media` strategy, it responds to the user's operating system preference via `prefers-color-scheme: dark`.
</details>

---

**Q3.** What does the `group` class do in Tailwind CSS?

- A) Groups multiple elements into a grid
- B) Marks a parent element so that child elements can respond to the parent's hover, focus, or other states
- C) Creates a CSS animation group
- D) Combines multiple utility classes into one shorthand

<details>
<summary>Answer</summary>

**B) Marks a parent element so that child elements can respond to the parent's hover, focus, or other states**

By adding the `group` class to a parent element, you can use variants like `group-hover:`, `group-focus:`, and `group-active:` on child elements. This is useful for card components where hovering over the entire card should change the styling of a button or icon inside it.

```html
<div class="group p-4 bg-white hover:bg-blue-50">
  <h3 class="group-hover:text-blue-600">Card Title</h3>
</div>
```
</details>

---

**Q4.** Which section of `tailwind.config.js` should you use to add a custom font family **without removing** the default font families?

- A) `theme.fontFamily`
- B) `theme.extend.fontFamily`
- C) `plugins.fontFamily`
- D) `variants.fontFamily`

<details>
<summary>Answer</summary>

**B) `theme.extend.fontFamily`**

Placing customizations inside `theme.extend` adds your values alongside the defaults rather than replacing them. If you define `fontFamily` directly under `theme` (without `extend`), it replaces all default font families.

```js
module.exports = {
  theme: {
    extend: {
      fontFamily: {
        heading: ["Poppins", "sans-serif"],
      },
    },
  },
};
```
This makes `font-heading` available while keeping `font-sans`, `font-serif`, and `font-mono`.
</details>

---

**Q5.** What is the purpose of the `@apply` directive in Tailwind CSS?

- A) It imports external CSS files
- B) It lets you extract repeated utility patterns into a custom CSS class
- C) It applies JavaScript to an element
- D) It applies a media query to a set of elements

<details>
<summary>Answer</summary>

**B) It lets you extract repeated utility patterns into a custom CSS class**

`@apply` allows you to compose Tailwind utilities inside a traditional CSS rule. This is useful when you have a pattern of classes that repeats across many elements and you want a reusable class name.

```css
.btn-primary {
  @apply bg-blue-500 hover:bg-blue-700 text-white font-bold py-2 px-4 rounded;
}
```

You can then use `<button class="btn-primary">` instead of repeating all the utility classes. However, overusing `@apply` can negate the benefits of the utility-first approach.
</details>

---

**Q6.** How do you add a custom color called `brand` with a value of `#1a73e8` in the Tailwind configuration?

- A) Add `brand: "#1a73e8"` to `theme.colors`
- B) Add `brand: "#1a73e8"` to `theme.extend.colors`
- C) Both A and B work, but B preserves default colors while A replaces them
- D) Custom colors are not supported in Tailwind

<details>
<summary>Answer</summary>

**C) Both A and B work, but B preserves default colors while A replaces them**

Adding to `theme.colors` replaces the entire default color palette, so only your custom colors will be available. Adding to `theme.extend.colors` adds the custom color alongside all default colors. In most cases, option B is preferred:

```js
module.exports = {
  theme: {
    extend: {
      colors: {
        brand: "#1a73e8",
      },
    },
  },
};
```
This creates utilities like `text-brand`, `bg-brand`, and `border-brand`.
</details>

---

**Q7.** Which class adds a transition effect to **all properties** with a duration of 300ms?

- A) `transition duration-300`
- B) `animate-300`
- C) `transition-all ease-300`
- D) `transform duration-300`

<details>
<summary>Answer</summary>

**A) `transition duration-300`**

The `transition` class applies CSS transitions to common properties (color, background, border, shadow, opacity, transform). The `duration-300` class sets the transition duration to 300ms. Combined, they produce a smooth 300ms transition on state changes like hover or focus. For transitioning all properties (including non-default ones), use `transition-all duration-300`.
</details>

---

**Q8.** What is the `peer` class used for in Tailwind CSS?

- A) It creates a peer-to-peer network connection
- B) It marks a sibling element so other siblings can style themselves based on its state
- C) It groups elements for animation purposes
- D) It links two components together for data sharing

<details>
<summary>Answer</summary>

**B) It marks a sibling element so other siblings can style themselves based on its state**

The `peer` class is similar to `group`, but instead of parent-child relationships, it works with **sibling** elements. You mark one sibling with `peer`, and subsequent siblings can use variants like `peer-checked:`, `peer-focus:`, or `peer-invalid:`.

```html
<input type="checkbox" class="peer" id="toggle" />
<label for="toggle" class="peer-checked:text-green-600">
  Toggle is on
</label>
```
When the checkbox is checked, the label text turns green.
</details>

---

**Q9.** Which Tailwind plugin provides pre-styled form elements like inputs, selects, and textareas?

- A) `@tailwindcss/typography`
- B) `@tailwindcss/forms`
- C) `@tailwindcss/aspect-ratio`
- D) `@tailwindcss/container-queries`

<details>
<summary>Answer</summary>

**B) `@tailwindcss/forms`**

The `@tailwindcss/forms` plugin resets form elements to a consistent, minimal style that is easy to customize with Tailwind utilities. Without this plugin, form elements like `<input>`, `<select>`, and `<textarea>` retain their browser-default styling, which varies across browsers and is difficult to override.

Installation:
```bash
npm install @tailwindcss/forms
```

Configuration:
```js
module.exports = {
  plugins: [require("@tailwindcss/forms")],
};
```
</details>

---

**Q10.** What is the recommended way to build reusable components in a Tailwind CSS project using a framework like React?

- A) Use `@apply` for every component
- B) Extract components as framework components (e.g., React components) that encapsulate the utility classes
- C) Create a separate CSS file for each component
- D) Use inline styles instead of Tailwind classes

<details>
<summary>Answer</summary>

**B) Extract components as framework components (e.g., React components) that encapsulate the utility classes**

The Tailwind team recommends keeping utility classes in your markup and managing reuse through your framework's component system. For example, in React:

```jsx
function Button({ children, variant = "primary" }) {
  const base = "font-bold py-2 px-4 rounded transition-colors";
  const variants = {
    primary: "bg-blue-500 hover:bg-blue-700 text-white",
    secondary: "bg-gray-200 hover:bg-gray-300 text-gray-800",
  };

  return (
    <button className={`${base} ${variants[variant]}`}>
      {children}
    </button>
  );
}
```

This approach keeps your styling co-located with your component logic, avoids the complexity of managing separate CSS files, and takes full advantage of Tailwind's utility-first philosophy.
</details>

---

## Section B: Short Answer Questions

**Q1.** Explain the two dark mode strategies available in Tailwind CSS (`class` vs. `media`). When would you choose one over the other?

<details>
<summary>Answer</summary>

Tailwind CSS supports two dark mode strategies:

**1. `media` strategy (default):**
- Uses the CSS `prefers-color-scheme: dark` media query.
- Automatically activates dark mode based on the user's **operating system** or **browser** preference.
- No JavaScript is required.
- You have **no manual control** — dark mode is entirely determined by the OS setting.

**2. `class` strategy:**
- Activates dark mode when the `dark` class is present on the `<html>` element.
- Requires JavaScript to toggle the `dark` class on and off.
- Gives you **full control** — you can let users choose their theme preference, store it in `localStorage`, or default to the system preference and allow manual override.

**Configuration:**
```js
// tailwind.config.js
module.exports = {
  darkMode: 'class', // or 'media'
};
```

**When to choose each:**
- Use `media` for simple projects where matching the OS preference is sufficient.
- Use `class` when you need a manual toggle button, want to persist the user's choice, or need to support dark mode independently of the operating system setting. The `class` strategy is more common in production applications.
</details>

---

**Q2.** How do you extend Tailwind CSS with custom utilities or components using the plugin system?

<details>
<summary>Answer</summary>

Tailwind's plugin system lets you register custom utilities, components, base styles, and variants programmatically in `tailwind.config.js`.

**Creating a custom plugin:**

```js
// tailwind.config.js
const plugin = require("tailwindcss/plugin");

module.exports = {
  plugins: [
    plugin(function ({ addUtilities, addComponents, theme }) {

      // Add custom utilities
      addUtilities({
        ".text-shadow": {
          textShadow: "2px 2px 4px rgba(0, 0, 0, 0.1)",
        },
        ".text-shadow-lg": {
          textShadow: "4px 4px 8px rgba(0, 0, 0, 0.2)",
        },
      });

      // Add custom components
      addComponents({
        ".card": {
          backgroundColor: theme("colors.white"),
          borderRadius: theme("borderRadius.lg"),
          padding: theme("spacing.6"),
          boxShadow: theme("boxShadow.md"),
        },
      });
    }),
  ],
};
```

**Using official plugins:**
```bash
npm install @tailwindcss/typography @tailwindcss/forms
```
```js
module.exports = {
  plugins: [
    require("@tailwindcss/typography"),
    require("@tailwindcss/forms"),
  ],
};
```

Plugins are the recommended way to add reusable custom functionality that goes beyond what `theme.extend` offers.
</details>

---

**Q3.** What are component libraries built on top of Tailwind CSS? Name at least three and briefly describe them.

<details>
<summary>Answer</summary>

Several component libraries provide pre-built, customizable UI components styled with Tailwind CSS:

**1. Headless UI** (by the Tailwind Labs team)
- Provides completely unstyled, accessible UI components (modals, dropdowns, tabs, switches).
- You bring your own Tailwind styling.
- Designed for React and Vue.

**2. daisyUI**
- Adds semantic component classes (like `btn`, `card`, `modal`) on top of Tailwind.
- Includes multiple themes with a simple theme-switching system.
- Reduces class verbosity while still allowing utility overrides.

**3. Flowbite**
- Offers a large collection of pre-designed components (navbars, footers, pricing cards, dashboards).
- Includes JavaScript for interactive components.
- Available for vanilla HTML, React, Vue, Svelte, and Angular.

**4. Shadcn/UI**
- A collection of copy-paste components built with Radix UI and Tailwind CSS.
- Components are added directly to your project (not installed as a package), giving you full control.
- Popular in the React and Next.js ecosystem.

**5. Preline UI**
- Open-source set of Tailwind CSS components with built-in JavaScript for interactivity.
- Covers a wide range of UI patterns including dashboards, marketing pages, and application shells.

These libraries speed up development by providing production-ready components while maintaining the flexibility of Tailwind's utility-first approach.
</details>

---

**Q4.** What is the `group-hover` variant, and how does it differ from a regular `hover` variant? Provide a practical example.

<details>
<summary>Answer</summary>

**Regular `hover:`** applies styles when the element itself is hovered.

**`group-hover:`** applies styles to a child element when a **parent element** marked with the `group` class is hovered. This is essential for compound components where hovering one part should visually affect another.

**Practical example — a card with an icon that changes color when the card is hovered:**

```html
<a href="#" class="group block bg-white rounded-lg shadow p-6 hover:bg-blue-50 transition-colors">
  <div class="flex items-center gap-4">
    <!-- Icon changes color on card hover -->
    <svg class="w-8 h-8 text-gray-400 group-hover:text-blue-600 transition-colors" fill="currentColor" viewBox="0 0 20 20">
      <path d="M10 2a8 8 0 100 16 8 8 0 000-16z" />
    </svg>

    <div>
      <!-- Title changes color on card hover -->
      <h3 class="font-semibold text-gray-800 group-hover:text-blue-800">
        Feature Title
      </h3>
      <p class="text-sm text-gray-500">
        A short description of this feature.
      </p>
    </div>
  </div>
</a>
```

When the user hovers anywhere on the card (the `group` parent), the icon and title change color simultaneously. Without `group-hover`, you would need custom CSS or JavaScript to achieve this coordinated effect.
</details>

---

**Q5.** How would you handle responsive images and aspect ratios in Tailwind CSS?

<details>
<summary>Answer</summary>

Tailwind provides several approaches for responsive images and aspect ratios:

**1. Responsive images with `object-fit`:**
```html
<img
  src="photo.jpg"
  alt="Description"
  class="w-full h-64 object-cover rounded-lg"
/>
```
- `w-full` — image spans the full width of its container
- `h-64` — fixed height of 16rem
- `object-cover` — the image covers the area while maintaining its aspect ratio (excess is cropped)
- Other options: `object-contain` (fits inside without cropping), `object-fill` (stretches to fill)

**2. Aspect ratio utilities:**
```html
<div class="aspect-video">
  <img src="video-thumbnail.jpg" alt="Video" class="w-full h-full object-cover rounded-lg" />
</div>
```
- `aspect-video` — applies a 16:9 aspect ratio
- `aspect-square` — applies a 1:1 aspect ratio
- `aspect-auto` — uses the element's natural aspect ratio

**3. Custom aspect ratios via config:**
```js
// tailwind.config.js
module.exports = {
  theme: {
    extend: {
      aspectRatio: {
        '4/3': '4 / 3',
        '3/2': '3 / 2',
      },
    },
  },
};
```
This creates `aspect-4/3` and `aspect-3/2` utilities.

**4. Responsive sizing:**
```html
<img
  src="photo.jpg"
  alt="Description"
  class="w-full md:w-1/2 lg:w-1/3 h-auto object-cover"
/>
```
The image takes full width on mobile, half width on tablet, and one-third width on desktop, with `h-auto` preserving the natural aspect ratio.
</details>

---

## Section C: Coding Exercises

### Exercise 1: Build a Pricing Card Set

Create a set of three pricing cards (Basic, Pro, Enterprise) using Tailwind CSS. Requirements:
- Three cards side by side on desktop, stacked on mobile
- Each card shows a plan name, price, a list of features, and a "Choose Plan" button
- The middle card (Pro) should be highlighted as the recommended plan with a different color scheme and a "Most Popular" badge
- Hover effects on the cards

<details>
<summary>Solution</summary>

```html
<section class="bg-gray-50 py-16 px-6">
  <div class="max-w-6xl mx-auto">

    <h2 class="text-3xl font-bold text-center text-gray-800 mb-4">
      Choose Your Plan
    </h2>
    <p class="text-center text-gray-500 mb-12 max-w-xl mx-auto">
      Select the plan that fits your needs. Upgrade or downgrade at any time.
    </p>

    <div class="grid grid-cols-1 md:grid-cols-3 gap-8">

      <!-- Basic Plan -->
      <div class="bg-white rounded-xl shadow-md p-8 hover:shadow-xl transition-shadow duration-300 flex flex-col">
        <h3 class="text-xl font-semibold text-gray-800 mb-2">Basic</h3>
        <p class="text-gray-500 mb-6">For individuals getting started.</p>
        <div class="mb-6">
          <span class="text-4xl font-bold text-gray-800">$9</span>
          <span class="text-gray-500">/month</span>
        </div>
        <ul class="space-y-3 mb-8 flex-grow">
          <li class="flex items-center text-gray-600">
            <span class="text-green-500 mr-2">&#10003;</span> 5 Projects
          </li>
          <li class="flex items-center text-gray-600">
            <span class="text-green-500 mr-2">&#10003;</span> 10 GB Storage
          </li>
          <li class="flex items-center text-gray-600">
            <span class="text-green-500 mr-2">&#10003;</span> Email Support
          </li>
          <li class="flex items-center text-gray-400 line-through">
            <span class="mr-2">&#10007;</span> Custom Domain
          </li>
          <li class="flex items-center text-gray-400 line-through">
            <span class="mr-2">&#10007;</span> Analytics Dashboard
          </li>
        </ul>
        <button class="w-full bg-gray-800 hover:bg-gray-900 text-white font-semibold py-3 rounded-lg transition-colors">
          Choose Plan
        </button>
      </div>

      <!-- Pro Plan (Highlighted) -->
      <div class="bg-blue-600 rounded-xl shadow-xl p-8 hover:shadow-2xl transition-shadow duration-300 flex flex-col relative">
        <span class="absolute -top-4 left-1/2 -translate-x-1/2 bg-yellow-400 text-yellow-900 text-sm font-bold px-4 py-1 rounded-full">
          Most Popular
        </span>
        <h3 class="text-xl font-semibold text-white mb-2">Pro</h3>
        <p class="text-blue-200 mb-6">For professionals and small teams.</p>
        <div class="mb-6">
          <span class="text-4xl font-bold text-white">$29</span>
          <span class="text-blue-200">/month</span>
        </div>
        <ul class="space-y-3 mb-8 flex-grow">
          <li class="flex items-center text-blue-100">
            <span class="text-yellow-300 mr-2">&#10003;</span> 25 Projects
          </li>
          <li class="flex items-center text-blue-100">
            <span class="text-yellow-300 mr-2">&#10003;</span> 100 GB Storage
          </li>
          <li class="flex items-center text-blue-100">
            <span class="text-yellow-300 mr-2">&#10003;</span> Priority Support
          </li>
          <li class="flex items-center text-blue-100">
            <span class="text-yellow-300 mr-2">&#10003;</span> Custom Domain
          </li>
          <li class="flex items-center text-blue-100">
            <span class="text-yellow-300 mr-2">&#10003;</span> Analytics Dashboard
          </li>
        </ul>
        <button class="w-full bg-white hover:bg-blue-50 text-blue-600 font-semibold py-3 rounded-lg transition-colors">
          Choose Plan
        </button>
      </div>

      <!-- Enterprise Plan -->
      <div class="bg-white rounded-xl shadow-md p-8 hover:shadow-xl transition-shadow duration-300 flex flex-col">
        <h3 class="text-xl font-semibold text-gray-800 mb-2">Enterprise</h3>
        <p class="text-gray-500 mb-6">For large teams and organizations.</p>
        <div class="mb-6">
          <span class="text-4xl font-bold text-gray-800">$79</span>
          <span class="text-gray-500">/month</span>
        </div>
        <ul class="space-y-3 mb-8 flex-grow">
          <li class="flex items-center text-gray-600">
            <span class="text-green-500 mr-2">&#10003;</span> Unlimited Projects
          </li>
          <li class="flex items-center text-gray-600">
            <span class="text-green-500 mr-2">&#10003;</span> 1 TB Storage
          </li>
          <li class="flex items-center text-gray-600">
            <span class="text-green-500 mr-2">&#10003;</span> 24/7 Dedicated Support
          </li>
          <li class="flex items-center text-gray-600">
            <span class="text-green-500 mr-2">&#10003;</span> Custom Domain
          </li>
          <li class="flex items-center text-gray-600">
            <span class="text-green-500 mr-2">&#10003;</span> Advanced Analytics
          </li>
        </ul>
        <button class="w-full bg-gray-800 hover:bg-gray-900 text-white font-semibold py-3 rounded-lg transition-colors">
          Choose Plan
        </button>
      </div>

    </div>
  </div>
</section>
```

**Key Tailwind patterns used:**
- `grid grid-cols-1 md:grid-cols-3 gap-8` — responsive three-column grid
- `flex flex-col` and `flex-grow` — ensures all cards have equal height with the feature list expanding to fill space
- `relative` and `absolute -top-4 left-1/2 -translate-x-1/2` — positions the "Most Popular" badge above the card
- `hover:shadow-xl transition-shadow duration-300` — smooth shadow elevation on hover
- `line-through text-gray-400` — visually indicates unavailable features
- `space-y-3` — consistent vertical spacing in the feature list
</details>

---

### Exercise 2: Create a Footer with Columns

Build a responsive footer with:
- A logo and brief description on the left
- Three columns of links (Product, Company, Resources)
- A bottom bar with copyright text and social media icon placeholders
- The columns should stack on mobile and display side by side on desktop

<details>
<summary>Solution</summary>

```html
<footer class="bg-gray-900 text-gray-300">
  <div class="max-w-6xl mx-auto px-6 py-12">
    <div class="grid grid-cols-1 md:grid-cols-2 lg:grid-cols-4 gap-8">

      <!-- Brand Column -->
      <div>
        <h3 class="text-white text-xl font-bold mb-4">MyBrand</h3>
        <p class="text-gray-400 text-sm leading-relaxed mb-4">
          Building modern web experiences with cutting-edge technologies.
          We help businesses grow through beautiful, performant websites.
        </p>
        <!-- Social Icons -->
        <div class="flex gap-4">
          <a href="#" class="text-gray-400 hover:text-white transition-colors" aria-label="Twitter">
            <svg class="w-5 h-5" fill="currentColor" viewBox="0 0 24 24"><path d="M24 4.557a9.83 9.83 0 01-2.828.775 4.932 4.932 0 002.165-2.724 9.864 9.864 0 01-3.127 1.195 4.916 4.916 0 00-8.384 4.482A13.944 13.944 0 011.671 3.149a4.916 4.916 0 001.523 6.574 4.897 4.897 0 01-2.229-.616v.062a4.918 4.918 0 003.946 4.827 4.902 4.902 0 01-2.224.084 4.92 4.92 0 004.6 3.417A9.868 9.868 0 010 19.54a13.905 13.905 0 007.548 2.212c9.057 0 14.01-7.503 14.01-14.01 0-.213-.005-.425-.014-.636A10.012 10.012 0 0024 4.557z"/></svg>
          </a>
          <a href="#" class="text-gray-400 hover:text-white transition-colors" aria-label="GitHub">
            <svg class="w-5 h-5" fill="currentColor" viewBox="0 0 24 24"><path d="M12 0C5.374 0 0 5.373 0 12c0 5.302 3.438 9.8 8.207 11.387.599.111.793-.261.793-.577v-2.234c-3.338.726-4.033-1.416-4.033-1.416-.546-1.387-1.333-1.756-1.333-1.756-1.089-.745.083-.729.083-.729 1.205.084 1.839 1.237 1.839 1.237 1.07 1.834 2.807 1.304 3.492.997.107-.775.418-1.305.762-1.604-2.665-.305-5.467-1.334-5.467-5.931 0-1.311.469-2.381 1.236-3.221-.124-.303-.535-1.524.117-3.176 0 0 1.008-.322 3.301 1.23A11.509 11.509 0 0112 5.803c1.02.005 2.047.138 3.006.404 2.291-1.552 3.297-1.23 3.297-1.23.653 1.653.242 2.874.118 3.176.77.84 1.235 1.911 1.235 3.221 0 4.609-2.807 5.624-5.479 5.921.43.372.823 1.102.823 2.222v3.293c0 .319.192.694.801.576C20.566 21.797 24 17.3 24 12c0-6.627-5.373-12-12-12z"/></svg>
          </a>
          <a href="#" class="text-gray-400 hover:text-white transition-colors" aria-label="LinkedIn">
            <svg class="w-5 h-5" fill="currentColor" viewBox="0 0 24 24"><path d="M20.447 20.452h-3.554v-5.569c0-1.328-.027-3.037-1.852-3.037-1.853 0-2.136 1.445-2.136 2.939v5.667H9.351V9h3.414v1.561h.046c.477-.9 1.637-1.85 3.37-1.85 3.601 0 4.267 2.37 4.267 5.455v6.286zM5.337 7.433a2.062 2.062 0 01-2.063-2.065 2.064 2.064 0 112.063 2.065zm1.782 13.019H3.555V9h3.564v11.452zM22.225 0H1.771C.792 0 0 .774 0 1.729v20.542C0 23.227.792 24 1.771 24h20.451C23.2 24 24 23.227 24 22.271V1.729C24 .774 23.2 0 22.222 0h.003z"/></svg>
          </a>
        </div>
      </div>

      <!-- Product Column -->
      <div>
        <h4 class="text-white font-semibold mb-4">Product</h4>
        <ul class="space-y-2">
          <li><a href="#" class="text-gray-400 hover:text-white text-sm transition-colors">Features</a></li>
          <li><a href="#" class="text-gray-400 hover:text-white text-sm transition-colors">Pricing</a></li>
          <li><a href="#" class="text-gray-400 hover:text-white text-sm transition-colors">Integrations</a></li>
          <li><a href="#" class="text-gray-400 hover:text-white text-sm transition-colors">Changelog</a></li>
          <li><a href="#" class="text-gray-400 hover:text-white text-sm transition-colors">Roadmap</a></li>
        </ul>
      </div>

      <!-- Company Column -->
      <div>
        <h4 class="text-white font-semibold mb-4">Company</h4>
        <ul class="space-y-2">
          <li><a href="#" class="text-gray-400 hover:text-white text-sm transition-colors">About Us</a></li>
          <li><a href="#" class="text-gray-400 hover:text-white text-sm transition-colors">Careers</a></li>
          <li><a href="#" class="text-gray-400 hover:text-white text-sm transition-colors">Blog</a></li>
          <li><a href="#" class="text-gray-400 hover:text-white text-sm transition-colors">Press</a></li>
          <li><a href="#" class="text-gray-400 hover:text-white text-sm transition-colors">Partners</a></li>
        </ul>
      </div>

      <!-- Resources Column -->
      <div>
        <h4 class="text-white font-semibold mb-4">Resources</h4>
        <ul class="space-y-2">
          <li><a href="#" class="text-gray-400 hover:text-white text-sm transition-colors">Documentation</a></li>
          <li><a href="#" class="text-gray-400 hover:text-white text-sm transition-colors">Tutorials</a></li>
          <li><a href="#" class="text-gray-400 hover:text-white text-sm transition-colors">Community</a></li>
          <li><a href="#" class="text-gray-400 hover:text-white text-sm transition-colors">Support</a></li>
          <li><a href="#" class="text-gray-400 hover:text-white text-sm transition-colors">Contact</a></li>
        </ul>
      </div>

    </div>

    <!-- Bottom Bar -->
    <div class="border-t border-gray-700 mt-12 pt-8 flex flex-col md:flex-row justify-between items-center gap-4">
      <p class="text-gray-500 text-sm">
        &copy; 2025 MyBrand. All rights reserved.
      </p>
      <div class="flex gap-6">
        <a href="#" class="text-gray-500 hover:text-white text-sm transition-colors">Privacy Policy</a>
        <a href="#" class="text-gray-500 hover:text-white text-sm transition-colors">Terms of Service</a>
        <a href="#" class="text-gray-500 hover:text-white text-sm transition-colors">Cookie Policy</a>
      </div>
    </div>

  </div>
</footer>
```

**Key Tailwind patterns used:**
- `grid grid-cols-1 md:grid-cols-2 lg:grid-cols-4 gap-8` — footer columns adapt from 1 to 4 across breakpoints
- `space-y-2` — consistent vertical spacing for link lists
- `border-t border-gray-700 mt-12 pt-8` — divider line between the main footer and bottom bar
- `flex flex-col md:flex-row justify-between items-center` — bottom bar stacks on mobile and spreads horizontally on larger screens
- SVG icons use `fill="currentColor"` so they inherit Tailwind's `text-*` color classes
</details>

---

### Exercise 3: Build a Testimonial Section

Create a testimonials section with:
- A section heading
- Three testimonial cards, each with a quote, the person's name, their role, and an avatar placeholder
- A star rating display
- Responsive layout (1 column on mobile, 3 columns on desktop)

<details>
<summary>Solution</summary>

```html
<section class="bg-white py-16 px-6">
  <div class="max-w-6xl mx-auto">

    <h2 class="text-3xl font-bold text-center text-gray-800 mb-4">
      What Our Customers Say
    </h2>
    <p class="text-center text-gray-500 mb-12 max-w-2xl mx-auto">
      Trusted by thousands of developers and businesses around the world.
    </p>

    <div class="grid grid-cols-1 md:grid-cols-2 lg:grid-cols-3 gap-8">

      <!-- Testimonial 1 -->
      <div class="bg-gray-50 rounded-xl p-8 hover:shadow-lg transition-shadow duration-300">
        <!-- Stars -->
        <div class="flex gap-1 mb-4">
          <span class="text-yellow-400 text-lg">&#9733;</span>
          <span class="text-yellow-400 text-lg">&#9733;</span>
          <span class="text-yellow-400 text-lg">&#9733;</span>
          <span class="text-yellow-400 text-lg">&#9733;</span>
          <span class="text-yellow-400 text-lg">&#9733;</span>
        </div>
        <!-- Quote -->
        <p class="text-gray-600 italic mb-6 leading-relaxed">
          "This product has completely transformed the way we build websites.
          The utility-first approach saves us hours every sprint."
        </p>
        <!-- Author -->
        <div class="flex items-center gap-4">
          <div class="w-12 h-12 bg-blue-500 rounded-full flex items-center justify-center text-white font-bold text-lg">
            SA
          </div>
          <div>
            <p class="font-semibold text-gray-800">Sarah Ahmed</p>
            <p class="text-sm text-gray-500">Frontend Developer, TechCorp</p>
          </div>
        </div>
      </div>

      <!-- Testimonial 2 -->
      <div class="bg-gray-50 rounded-xl p-8 hover:shadow-lg transition-shadow duration-300">
        <!-- Stars -->
        <div class="flex gap-1 mb-4">
          <span class="text-yellow-400 text-lg">&#9733;</span>
          <span class="text-yellow-400 text-lg">&#9733;</span>
          <span class="text-yellow-400 text-lg">&#9733;</span>
          <span class="text-yellow-400 text-lg">&#9733;</span>
          <span class="text-yellow-400 text-lg">&#9733;</span>
        </div>
        <!-- Quote -->
        <p class="text-gray-600 italic mb-6 leading-relaxed">
          "The responsive design utilities are incredible. We went from
          spending days on media queries to handling everything with simple class prefixes."
        </p>
        <!-- Author -->
        <div class="flex items-center gap-4">
          <div class="w-12 h-12 bg-green-500 rounded-full flex items-center justify-center text-white font-bold text-lg">
            MK
          </div>
          <div>
            <p class="font-semibold text-gray-800">Mohammed Khan</p>
            <p class="text-sm text-gray-500">Lead Engineer, StartupXYZ</p>
          </div>
        </div>
      </div>

      <!-- Testimonial 3 -->
      <div class="bg-gray-50 rounded-xl p-8 hover:shadow-lg transition-shadow duration-300">
        <!-- Stars -->
        <div class="flex gap-1 mb-4">
          <span class="text-yellow-400 text-lg">&#9733;</span>
          <span class="text-yellow-400 text-lg">&#9733;</span>
          <span class="text-yellow-400 text-lg">&#9733;</span>
          <span class="text-yellow-400 text-lg">&#9733;</span>
          <span class="text-gray-300 text-lg">&#9733;</span>
        </div>
        <!-- Quote -->
        <p class="text-gray-600 italic mb-6 leading-relaxed">
          "Customization through the config file is seamless. We matched our
          entire brand guidelines in under an hour. Highly recommended."
        </p>
        <!-- Author -->
        <div class="flex items-center gap-4">
          <div class="w-12 h-12 bg-purple-500 rounded-full flex items-center justify-center text-white font-bold text-lg">
            LR
          </div>
          <div>
            <p class="font-semibold text-gray-800">Lisa Rodriguez</p>
            <p class="text-sm text-gray-500">UI Designer, DesignStudio</p>
          </div>
        </div>
      </div>

    </div>
  </div>
</section>
```

**Key Tailwind patterns used:**
- `grid grid-cols-1 md:grid-cols-2 lg:grid-cols-3 gap-8` — responsive testimonial grid
- `bg-gray-50 rounded-xl p-8` — subtle card background with generous padding
- `hover:shadow-lg transition-shadow duration-300` — cards elevate on hover
- `text-yellow-400` for filled stars and `text-gray-300` for empty stars
- `w-12 h-12 rounded-full flex items-center justify-center` — circular avatar placeholder with initials
- `italic leading-relaxed` — styled quote text with comfortable line height
</details>

---

### Exercise 4: Create a Dark/Light Mode Toggle Page

Build a simple page that supports both dark and light modes using Tailwind CSS. Requirements:
- A toggle button to switch between dark and light modes
- The page background, text colors, and card colors should all change
- Use the `dark:` variant for styling
- Include a small JavaScript snippet to handle the toggle

<details>
<summary>Solution</summary>

```html
<!DOCTYPE html>
<html lang="en" class="">
<head>
  <meta charset="UTF-8" />
  <meta name="viewport" content="width=device-width, initial-scale=1.0" />
  <title>Dark Mode Toggle</title>
  <!-- Include Tailwind CSS (use your project's build setup in production) -->
  <script src="https://cdn.tailwindcss.com"></script>
  <script>
    tailwind.config = {
      darkMode: 'class',
    };
  </script>
</head>
<body class="bg-gray-100 dark:bg-gray-900 text-gray-800 dark:text-gray-200 transition-colors duration-300 min-h-screen">

  <!-- Header with Toggle -->
  <header class="bg-white dark:bg-gray-800 shadow-sm py-4 px-6">
    <div class="max-w-4xl mx-auto flex justify-between items-center">
      <h1 class="text-xl font-bold text-gray-800 dark:text-white">
        My App
      </h1>
      <button
        id="themeToggle"
        class="bg-gray-200 dark:bg-gray-700 text-gray-800 dark:text-gray-200 px-4 py-2 rounded-lg hover:bg-gray-300 dark:hover:bg-gray-600 transition-colors font-medium text-sm"
      >
        Toggle Dark Mode
      </button>
    </div>
  </header>

  <!-- Main Content -->
  <main class="max-w-4xl mx-auto px-6 py-12">

    <h2 class="text-2xl font-bold mb-6 text-gray-800 dark:text-white">
      Dashboard
    </h2>

    <div class="grid grid-cols-1 md:grid-cols-2 gap-6">

      <!-- Card 1 -->
      <div class="bg-white dark:bg-gray-800 rounded-lg shadow p-6">
        <h3 class="font-semibold text-lg mb-2 text-gray-800 dark:text-white">
          Total Users
        </h3>
        <p class="text-3xl font-bold text-blue-600 dark:text-blue-400">
          12,450
        </p>
        <p class="text-sm text-gray-500 dark:text-gray-400 mt-2">
          +12% from last month
        </p>
      </div>

      <!-- Card 2 -->
      <div class="bg-white dark:bg-gray-800 rounded-lg shadow p-6">
        <h3 class="font-semibold text-lg mb-2 text-gray-800 dark:text-white">
          Revenue
        </h3>
        <p class="text-3xl font-bold text-green-600 dark:text-green-400">
          $48,200
        </p>
        <p class="text-sm text-gray-500 dark:text-gray-400 mt-2">
          +8% from last month
        </p>
      </div>

      <!-- Card 3 -->
      <div class="bg-white dark:bg-gray-800 rounded-lg shadow p-6">
        <h3 class="font-semibold text-lg mb-2 text-gray-800 dark:text-white">
          Active Projects
        </h3>
        <p class="text-3xl font-bold text-purple-600 dark:text-purple-400">
          34
        </p>
        <p class="text-sm text-gray-500 dark:text-gray-400 mt-2">
          5 completed this week
        </p>
      </div>

      <!-- Card 4 -->
      <div class="bg-white dark:bg-gray-800 rounded-lg shadow p-6">
        <h3 class="font-semibold text-lg mb-2 text-gray-800 dark:text-white">
          Support Tickets
        </h3>
        <p class="text-3xl font-bold text-red-600 dark:text-red-400">
          7
        </p>
        <p class="text-sm text-gray-500 dark:text-gray-400 mt-2">
          3 resolved today
        </p>
      </div>

    </div>
  </main>

  <!-- Toggle Script -->
  <script>
    const toggleBtn = document.getElementById("themeToggle");
    const html = document.documentElement;

    // Check for saved preference or default to light
    if (localStorage.getItem("theme") === "dark") {
      html.classList.add("dark");
    }

    toggleBtn.addEventListener("click", () => {
      html.classList.toggle("dark");

      // Save the preference
      if (html.classList.contains("dark")) {
        localStorage.setItem("theme", "dark");
      } else {
        localStorage.setItem("theme", "light");
      }
    });
  </script>

</body>
</html>
```

**Key Tailwind patterns used:**
- `darkMode: 'class'` — enables dark mode via a class on the `<html>` element
- `bg-gray-100 dark:bg-gray-900` — light gray background in light mode, near-black in dark mode
- `text-gray-800 dark:text-gray-200` — dark text in light mode, light text in dark mode
- `bg-white dark:bg-gray-800` — white cards in light mode, dark gray cards in dark mode
- `text-blue-600 dark:text-blue-400` — accent colors shift to lighter variants in dark mode for readability
- `transition-colors duration-300` — smooth color transitions when toggling modes
- JavaScript toggles the `dark` class on `<html>` and persists the choice in `localStorage`
</details>

---

### Exercise 5: Tailwind Phase Project — Build a Complete Responsive Landing Page

Build a **complete, production-quality landing page** using only Tailwind CSS. This is the culminating project for the Tailwind CSS phase. The page must include all of the following sections:

1. **Navigation bar** — logo on the left, links on the right, responsive (hamburger concept on mobile)
2. **Hero section** — large heading, subtitle, two CTA buttons, background gradient
3. **Features section** — grid of 3-6 feature cards with icons, titles, and descriptions
4. **Testimonials section** — at least 3 testimonial cards with quotes, names, and roles
5. **Pricing section** — 3 pricing tiers with feature lists and CTA buttons (one highlighted)
6. **Call-to-Action (CTA) section** — a standout banner encouraging sign-up
7. **Footer** — multi-column footer with links and copyright

<details>
<summary>Solution</summary>

```html
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8" />
  <meta name="viewport" content="width=device-width, initial-scale=1.0" />
  <title>LaunchPad — Ship Faster</title>
  <script src="https://cdn.tailwindcss.com"></script>
</head>
<body class="bg-white text-gray-800 font-sans">

  <!-- ==================== NAVIGATION ==================== -->
  <nav class="bg-white shadow-sm sticky top-0 z-50">
    <div class="max-w-6xl mx-auto px-6 py-4 flex items-center justify-between">
      <!-- Logo -->
      <a href="#" class="text-2xl font-bold text-blue-600">LaunchPad</a>

      <!-- Desktop Links -->
      <ul class="hidden md:flex items-center gap-8">
        <li><a href="#features" class="text-gray-600 hover:text-blue-600 transition-colors">Features</a></li>
        <li><a href="#testimonials" class="text-gray-600 hover:text-blue-600 transition-colors">Testimonials</a></li>
        <li><a href="#pricing" class="text-gray-600 hover:text-blue-600 transition-colors">Pricing</a></li>
        <li><a href="#contact" class="text-gray-600 hover:text-blue-600 transition-colors">Contact</a></li>
      </ul>

      <!-- CTA Button (Desktop) -->
      <a href="#pricing" class="hidden md:inline-block bg-blue-600 hover:bg-blue-700 text-white font-semibold py-2 px-6 rounded-lg transition-colors">
        Get Started
      </a>

      <!-- Mobile Menu Button -->
      <button id="menuBtn" class="md:hidden text-gray-600 hover:text-blue-600 focus:outline-none">
        <svg class="w-6 h-6" fill="none" stroke="currentColor" viewBox="0 0 24 24">
          <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M4 6h16M4 12h16M4 18h16" />
        </svg>
      </button>
    </div>

    <!-- Mobile Menu -->
    <div id="mobileMenu" class="hidden md:hidden bg-white border-t px-6 pb-4">
      <ul class="flex flex-col gap-3 pt-4">
        <li><a href="#features" class="text-gray-600 hover:text-blue-600 transition-colors">Features</a></li>
        <li><a href="#testimonials" class="text-gray-600 hover:text-blue-600 transition-colors">Testimonials</a></li>
        <li><a href="#pricing" class="text-gray-600 hover:text-blue-600 transition-colors">Pricing</a></li>
        <li><a href="#contact" class="text-gray-600 hover:text-blue-600 transition-colors">Contact</a></li>
        <li>
          <a href="#pricing" class="inline-block bg-blue-600 hover:bg-blue-700 text-white font-semibold py-2 px-6 rounded-lg transition-colors mt-2">
            Get Started
          </a>
        </li>
      </ul>
    </div>
  </nav>

  <!-- ==================== HERO SECTION ==================== -->
  <section class="bg-gradient-to-br from-blue-600 via-blue-700 to-purple-700 text-white py-24 px-6">
    <div class="max-w-5xl mx-auto text-center">
      <h1 class="text-4xl md:text-5xl lg:text-6xl font-bold mb-6 leading-tight">
        Ship Your Ideas<br class="hidden md:block" /> Faster Than Ever
      </h1>
      <p class="text-lg md:text-xl text-blue-100 mb-10 max-w-2xl mx-auto leading-relaxed">
        LaunchPad gives your team the tools to go from concept to production
        in record time. Focus on building, not configuring.
      </p>
      <div class="flex flex-col sm:flex-row gap-4 justify-center">
        <a href="#pricing" class="bg-white text-blue-600 font-bold py-3 px-8 rounded-full hover:bg-blue-50 transition-colors text-lg">
          Start Free Trial
        </a>
        <a href="#features" class="border-2 border-white text-white font-bold py-3 px-8 rounded-full hover:bg-white hover:text-blue-600 transition-colors text-lg">
          Learn More
        </a>
      </div>
    </div>
  </section>

  <!-- ==================== FEATURES SECTION ==================== -->
  <section id="features" class="py-20 px-6 bg-gray-50">
    <div class="max-w-6xl mx-auto">
      <h2 class="text-3xl md:text-4xl font-bold text-center text-gray-800 mb-4">
        Everything You Need
      </h2>
      <p class="text-center text-gray-500 mb-14 max-w-2xl mx-auto">
        Powerful features designed to streamline your workflow and accelerate development.
      </p>

      <div class="grid grid-cols-1 md:grid-cols-2 lg:grid-cols-3 gap-8">

        <!-- Feature 1 -->
        <div class="bg-white rounded-xl shadow-sm p-8 hover:shadow-md transition-shadow duration-300">
          <div class="w-12 h-12 bg-blue-100 text-blue-600 rounded-lg flex items-center justify-center mb-5">
            <svg class="w-6 h-6" fill="none" stroke="currentColor" viewBox="0 0 24 24"><path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M13 10V3L4 14h7v7l9-11h-7z" /></svg>
          </div>
          <h3 class="text-lg font-semibold text-gray-800 mb-2">Lightning Fast</h3>
          <p class="text-gray-500 text-sm leading-relaxed">Optimized performance from the ground up. Pages load in milliseconds, not seconds.</p>
        </div>

        <!-- Feature 2 -->
        <div class="bg-white rounded-xl shadow-sm p-8 hover:shadow-md transition-shadow duration-300">
          <div class="w-12 h-12 bg-green-100 text-green-600 rounded-lg flex items-center justify-center mb-5">
            <svg class="w-6 h-6" fill="none" stroke="currentColor" viewBox="0 0 24 24"><path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M9 12l2 2 4-4m5.618-4.016A11.955 11.955 0 0112 2.944a11.955 11.955 0 01-8.618 3.04A12.02 12.02 0 003 9c0 5.591 3.824 10.29 9 11.622 5.176-1.332 9-6.03 9-11.622 0-1.042-.133-2.052-.382-3.016z" /></svg>
          </div>
          <h3 class="text-lg font-semibold text-gray-800 mb-2">Secure by Default</h3>
          <p class="text-gray-500 text-sm leading-relaxed">Enterprise-grade security built in. SSL, encryption, and compliance out of the box.</p>
        </div>

        <!-- Feature 3 -->
        <div class="bg-white rounded-xl shadow-sm p-8 hover:shadow-md transition-shadow duration-300">
          <div class="w-12 h-12 bg-purple-100 text-purple-600 rounded-lg flex items-center justify-center mb-5">
            <svg class="w-6 h-6" fill="none" stroke="currentColor" viewBox="0 0 24 24"><path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M4 5a1 1 0 011-1h14a1 1 0 011 1v2a1 1 0 01-1 1H5a1 1 0 01-1-1V5zM4 13a1 1 0 011-1h6a1 1 0 011 1v6a1 1 0 01-1 1H5a1 1 0 01-1-1v-6zM16 13a1 1 0 011-1h2a1 1 0 011 1v6a1 1 0 01-1 1h-2a1 1 0 01-1-1v-6z" /></svg>
          </div>
          <h3 class="text-lg font-semibold text-gray-800 mb-2">Responsive Layouts</h3>
          <p class="text-gray-500 text-sm leading-relaxed">Every component adapts seamlessly to any screen size. Desktop, tablet, or mobile.</p>
        </div>

        <!-- Feature 4 -->
        <div class="bg-white rounded-xl shadow-sm p-8 hover:shadow-md transition-shadow duration-300">
          <div class="w-12 h-12 bg-yellow-100 text-yellow-600 rounded-lg flex items-center justify-center mb-5">
            <svg class="w-6 h-6" fill="none" stroke="currentColor" viewBox="0 0 24 24"><path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M11 4a2 2 0 114 0v1a1 1 0 001 1h3a1 1 0 011 1v3a1 1 0 01-1 1h-1a2 2 0 100 4h1a1 1 0 011 1v3a1 1 0 01-1 1h-3a1 1 0 01-1-1v-1a2 2 0 10-4 0v1a1 1 0 01-1 1H7a1 1 0 01-1-1v-3a1 1 0 00-1-1H4a2 2 0 110-4h1a1 1 0 001-1V7a1 1 0 011-1h3a1 1 0 001-1V4z" /></svg>
          </div>
          <h3 class="text-lg font-semibold text-gray-800 mb-2">Easy Integration</h3>
          <p class="text-gray-500 text-sm leading-relaxed">Connect with your favorite tools in minutes. REST APIs, webhooks, and SDKs included.</p>
        </div>

        <!-- Feature 5 -->
        <div class="bg-white rounded-xl shadow-sm p-8 hover:shadow-md transition-shadow duration-300">
          <div class="w-12 h-12 bg-red-100 text-red-600 rounded-lg flex items-center justify-center mb-5">
            <svg class="w-6 h-6" fill="none" stroke="currentColor" viewBox="0 0 24 24"><path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M9 19v-6a2 2 0 00-2-2H5a2 2 0 00-2 2v6a2 2 0 002 2h2a2 2 0 002-2zm0 0V9a2 2 0 012-2h2a2 2 0 012 2v10m-6 0a2 2 0 002 2h2a2 2 0 002-2m0 0V5a2 2 0 012-2h2a2 2 0 012 2v14a2 2 0 01-2 2h-2a2 2 0 01-2-2z" /></svg>
          </div>
          <h3 class="text-lg font-semibold text-gray-800 mb-2">Analytics Built In</h3>
          <p class="text-gray-500 text-sm leading-relaxed">Track performance, user engagement, and growth metrics from a single dashboard.</p>
        </div>

        <!-- Feature 6 -->
        <div class="bg-white rounded-xl shadow-sm p-8 hover:shadow-md transition-shadow duration-300">
          <div class="w-12 h-12 bg-indigo-100 text-indigo-600 rounded-lg flex items-center justify-center mb-5">
            <svg class="w-6 h-6" fill="none" stroke="currentColor" viewBox="0 0 24 24"><path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M17 20h5v-2a3 3 0 00-5.356-1.857M17 20H7m10 0v-2c0-.656-.126-1.283-.356-1.857M7 20H2v-2a3 3 0 015.356-1.857M7 20v-2c0-.656.126-1.283.356-1.857m0 0a5.002 5.002 0 019.288 0M15 7a3 3 0 11-6 0 3 3 0 016 0zm6 3a2 2 0 11-4 0 2 2 0 014 0zM7 10a2 2 0 11-4 0 2 2 0 014 0z" /></svg>
          </div>
          <h3 class="text-lg font-semibold text-gray-800 mb-2">Team Collaboration</h3>
          <p class="text-gray-500 text-sm leading-relaxed">Real-time collaboration tools that keep your team aligned and productive.</p>
        </div>

      </div>
    </div>
  </section>

  <!-- ==================== TESTIMONIALS SECTION ==================== -->
  <section id="testimonials" class="py-20 px-6 bg-white">
    <div class="max-w-6xl mx-auto">
      <h2 class="text-3xl md:text-4xl font-bold text-center text-gray-800 mb-4">
        Loved by Teams Everywhere
      </h2>
      <p class="text-center text-gray-500 mb-14 max-w-2xl mx-auto">
        See what developers and businesses are saying about LaunchPad.
      </p>

      <div class="grid grid-cols-1 md:grid-cols-2 lg:grid-cols-3 gap-8">

        <!-- Testimonial 1 -->
        <div class="bg-gray-50 rounded-xl p-8">
          <div class="flex gap-1 mb-4">
            <span class="text-yellow-400">&#9733;</span>
            <span class="text-yellow-400">&#9733;</span>
            <span class="text-yellow-400">&#9733;</span>
            <span class="text-yellow-400">&#9733;</span>
            <span class="text-yellow-400">&#9733;</span>
          </div>
          <p class="text-gray-600 italic mb-6 leading-relaxed">
            "LaunchPad cut our development time in half. We shipped our MVP in
            two weeks instead of two months. The team tools are outstanding."
          </p>
          <div class="flex items-center gap-3">
            <div class="w-10 h-10 bg-blue-500 rounded-full flex items-center justify-center text-white font-bold text-sm">JD</div>
            <div>
              <p class="font-semibold text-gray-800 text-sm">James Donovan</p>
              <p class="text-xs text-gray-500">CTO, Rapid Solutions</p>
            </div>
          </div>
        </div>

        <!-- Testimonial 2 -->
        <div class="bg-gray-50 rounded-xl p-8">
          <div class="flex gap-1 mb-4">
            <span class="text-yellow-400">&#9733;</span>
            <span class="text-yellow-400">&#9733;</span>
            <span class="text-yellow-400">&#9733;</span>
            <span class="text-yellow-400">&#9733;</span>
            <span class="text-yellow-400">&#9733;</span>
          </div>
          <p class="text-gray-600 italic mb-6 leading-relaxed">
            "The integration capabilities are top-notch. We connected our existing
            stack in under an hour. Support team was incredibly responsive."
          </p>
          <div class="flex items-center gap-3">
            <div class="w-10 h-10 bg-green-500 rounded-full flex items-center justify-center text-white font-bold text-sm">AN</div>
            <div>
              <p class="font-semibold text-gray-800 text-sm">Aisha Noor</p>
              <p class="text-xs text-gray-500">Engineering Lead, CloudFirst</p>
            </div>
          </div>
        </div>

        <!-- Testimonial 3 -->
        <div class="bg-gray-50 rounded-xl p-8">
          <div class="flex gap-1 mb-4">
            <span class="text-yellow-400">&#9733;</span>
            <span class="text-yellow-400">&#9733;</span>
            <span class="text-yellow-400">&#9733;</span>
            <span class="text-yellow-400">&#9733;</span>
            <span class="text-gray-300">&#9733;</span>
          </div>
          <p class="text-gray-600 italic mb-6 leading-relaxed">
            "We migrated our entire platform to LaunchPad and saw a 40% improvement
            in page load times. Our customers noticed the difference immediately."
          </p>
          <div class="flex items-center gap-3">
            <div class="w-10 h-10 bg-purple-500 rounded-full flex items-center justify-center text-white font-bold text-sm">CR</div>
            <div>
              <p class="font-semibold text-gray-800 text-sm">Carlos Reyes</p>
              <p class="text-xs text-gray-500">Product Manager, ScaleUp Inc.</p>
            </div>
          </div>
        </div>

      </div>
    </div>
  </section>

  <!-- ==================== PRICING SECTION ==================== -->
  <section id="pricing" class="py-20 px-6 bg-gray-50">
    <div class="max-w-6xl mx-auto">
      <h2 class="text-3xl md:text-4xl font-bold text-center text-gray-800 mb-4">
        Simple, Transparent Pricing
      </h2>
      <p class="text-center text-gray-500 mb-14 max-w-2xl mx-auto">
        No hidden fees. No surprises. Choose the plan that works for you.
      </p>

      <div class="grid grid-cols-1 md:grid-cols-3 gap-8 items-start">

        <!-- Starter Plan -->
        <div class="bg-white rounded-xl shadow-sm p-8 hover:shadow-lg transition-shadow duration-300 flex flex-col">
          <h3 class="text-xl font-semibold text-gray-800 mb-1">Starter</h3>
          <p class="text-gray-500 text-sm mb-6">Perfect for individuals.</p>
          <div class="mb-6">
            <span class="text-4xl font-bold text-gray-800">$0</span>
            <span class="text-gray-500">/month</span>
          </div>
          <ul class="space-y-3 mb-8 flex-grow">
            <li class="flex items-center text-gray-600 text-sm"><span class="text-green-500 mr-2">&#10003;</span> 3 Projects</li>
            <li class="flex items-center text-gray-600 text-sm"><span class="text-green-500 mr-2">&#10003;</span> 1 GB Storage</li>
            <li class="flex items-center text-gray-600 text-sm"><span class="text-green-500 mr-2">&#10003;</span> Community Support</li>
            <li class="flex items-center text-gray-400 text-sm line-through"><span class="mr-2">&#10007;</span> Custom Domain</li>
            <li class="flex items-center text-gray-400 text-sm line-through"><span class="mr-2">&#10007;</span> Analytics</li>
            <li class="flex items-center text-gray-400 text-sm line-through"><span class="mr-2">&#10007;</span> Priority Support</li>
          </ul>
          <button class="w-full border-2 border-gray-800 text-gray-800 hover:bg-gray-800 hover:text-white font-semibold py-3 rounded-lg transition-colors">
            Get Started Free
          </button>
        </div>

        <!-- Pro Plan (Highlighted) -->
        <div class="bg-blue-600 rounded-xl shadow-xl p-8 hover:shadow-2xl transition-shadow duration-300 flex flex-col relative">
          <span class="absolute -top-4 left-1/2 -translate-x-1/2 bg-yellow-400 text-yellow-900 text-xs font-bold px-4 py-1 rounded-full uppercase tracking-wide">
            Most Popular
          </span>
          <h3 class="text-xl font-semibold text-white mb-1">Pro</h3>
          <p class="text-blue-200 text-sm mb-6">For growing teams.</p>
          <div class="mb-6">
            <span class="text-4xl font-bold text-white">$29</span>
            <span class="text-blue-200">/month</span>
          </div>
          <ul class="space-y-3 mb-8 flex-grow">
            <li class="flex items-center text-blue-100 text-sm"><span class="text-yellow-300 mr-2">&#10003;</span> Unlimited Projects</li>
            <li class="flex items-center text-blue-100 text-sm"><span class="text-yellow-300 mr-2">&#10003;</span> 100 GB Storage</li>
            <li class="flex items-center text-blue-100 text-sm"><span class="text-yellow-300 mr-2">&#10003;</span> Priority Support</li>
            <li class="flex items-center text-blue-100 text-sm"><span class="text-yellow-300 mr-2">&#10003;</span> Custom Domain</li>
            <li class="flex items-center text-blue-100 text-sm"><span class="text-yellow-300 mr-2">&#10003;</span> Advanced Analytics</li>
            <li class="flex items-center text-blue-100 text-sm"><span class="text-yellow-300 mr-2">&#10003;</span> Team Collaboration</li>
          </ul>
          <button class="w-full bg-white hover:bg-blue-50 text-blue-600 font-semibold py-3 rounded-lg transition-colors">
            Start Free Trial
          </button>
        </div>

        <!-- Enterprise Plan -->
        <div class="bg-white rounded-xl shadow-sm p-8 hover:shadow-lg transition-shadow duration-300 flex flex-col">
          <h3 class="text-xl font-semibold text-gray-800 mb-1">Enterprise</h3>
          <p class="text-gray-500 text-sm mb-6">For large organizations.</p>
          <div class="mb-6">
            <span class="text-4xl font-bold text-gray-800">$99</span>
            <span class="text-gray-500">/month</span>
          </div>
          <ul class="space-y-3 mb-8 flex-grow">
            <li class="flex items-center text-gray-600 text-sm"><span class="text-green-500 mr-2">&#10003;</span> Unlimited Everything</li>
            <li class="flex items-center text-gray-600 text-sm"><span class="text-green-500 mr-2">&#10003;</span> 1 TB Storage</li>
            <li class="flex items-center text-gray-600 text-sm"><span class="text-green-500 mr-2">&#10003;</span> 24/7 Dedicated Support</li>
            <li class="flex items-center text-gray-600 text-sm"><span class="text-green-500 mr-2">&#10003;</span> SSO & SAML</li>
            <li class="flex items-center text-gray-600 text-sm"><span class="text-green-500 mr-2">&#10003;</span> SLA Guarantee</li>
            <li class="flex items-center text-gray-600 text-sm"><span class="text-green-500 mr-2">&#10003;</span> Custom Integrations</li>
          </ul>
          <button class="w-full border-2 border-gray-800 text-gray-800 hover:bg-gray-800 hover:text-white font-semibold py-3 rounded-lg transition-colors">
            Contact Sales
          </button>
        </div>

      </div>
    </div>
  </section>

  <!-- ==================== CTA SECTION ==================== -->
  <section class="bg-gradient-to-r from-blue-600 to-purple-600 py-16 px-6">
    <div class="max-w-4xl mx-auto text-center">
      <h2 class="text-3xl md:text-4xl font-bold text-white mb-4">
        Ready to Launch Your Next Project?
      </h2>
      <p class="text-blue-100 text-lg mb-8 max-w-2xl mx-auto">
        Join thousands of developers who are building and shipping faster with LaunchPad.
        Start your free trial today — no credit card required.
      </p>
      <div class="flex flex-col sm:flex-row gap-4 justify-center">
        <a href="#" class="bg-white text-blue-600 font-bold py-3 px-8 rounded-full hover:bg-blue-50 transition-colors text-lg">
          Start Free Trial
        </a>
        <a href="#" class="border-2 border-white text-white font-bold py-3 px-8 rounded-full hover:bg-white hover:text-blue-600 transition-colors text-lg">
          Schedule a Demo
        </a>
      </div>
    </div>
  </section>

  <!-- ==================== FOOTER ==================== -->
  <footer id="contact" class="bg-gray-900 text-gray-400">
    <div class="max-w-6xl mx-auto px-6 py-12">
      <div class="grid grid-cols-1 md:grid-cols-2 lg:grid-cols-4 gap-8">

        <!-- Brand -->
        <div>
          <h3 class="text-white text-xl font-bold mb-4">LaunchPad</h3>
          <p class="text-sm leading-relaxed mb-4">
            Empowering developers and teams to build, ship, and scale
            their ideas faster than ever before.
          </p>
        </div>

        <!-- Product -->
        <div>
          <h4 class="text-white font-semibold mb-4">Product</h4>
          <ul class="space-y-2">
            <li><a href="#" class="text-sm hover:text-white transition-colors">Features</a></li>
            <li><a href="#" class="text-sm hover:text-white transition-colors">Pricing</a></li>
            <li><a href="#" class="text-sm hover:text-white transition-colors">Integrations</a></li>
            <li><a href="#" class="text-sm hover:text-white transition-colors">Changelog</a></li>
          </ul>
        </div>

        <!-- Company -->
        <div>
          <h4 class="text-white font-semibold mb-4">Company</h4>
          <ul class="space-y-2">
            <li><a href="#" class="text-sm hover:text-white transition-colors">About</a></li>
            <li><a href="#" class="text-sm hover:text-white transition-colors">Blog</a></li>
            <li><a href="#" class="text-sm hover:text-white transition-colors">Careers</a></li>
            <li><a href="#" class="text-sm hover:text-white transition-colors">Contact</a></li>
          </ul>
        </div>

        <!-- Legal -->
        <div>
          <h4 class="text-white font-semibold mb-4">Legal</h4>
          <ul class="space-y-2">
            <li><a href="#" class="text-sm hover:text-white transition-colors">Privacy Policy</a></li>
            <li><a href="#" class="text-sm hover:text-white transition-colors">Terms of Service</a></li>
            <li><a href="#" class="text-sm hover:text-white transition-colors">Cookie Policy</a></li>
            <li><a href="#" class="text-sm hover:text-white transition-colors">Security</a></li>
          </ul>
        </div>

      </div>

      <!-- Bottom Bar -->
      <div class="border-t border-gray-700 mt-12 pt-8 text-center text-sm text-gray-500">
        <p>&copy; 2025 LaunchPad. All rights reserved.</p>
      </div>

    </div>
  </footer>

  <!-- ==================== MOBILE MENU SCRIPT ==================== -->
  <script>
    const menuBtn = document.getElementById("menuBtn");
    const mobileMenu = document.getElementById("mobileMenu");

    menuBtn.addEventListener("click", () => {
      mobileMenu.classList.toggle("hidden");
    });
  </script>

</body>
</html>
```

**Key Tailwind concepts demonstrated in this project:**

1. **Responsive design** — `grid-cols-1 md:grid-cols-2 lg:grid-cols-3`, `flex-col sm:flex-row`, `hidden md:flex`
2. **Spacing system** — `p-6`, `py-20`, `gap-8`, `mb-4`, `space-y-3`
3. **Color system** — `bg-blue-600`, `text-gray-800`, `text-blue-100`, `bg-gray-50`
4. **Gradients** — `bg-gradient-to-br from-blue-600 via-blue-700 to-purple-700`
5. **Hover and transition** — `hover:shadow-lg transition-shadow duration-300`, `hover:bg-blue-700`
6. **Typography** — `text-4xl md:text-5xl lg:text-6xl font-bold`, `text-sm leading-relaxed`
7. **Flexbox utilities** — `flex items-center justify-between`, `flex-grow`
8. **Grid utilities** — `grid grid-cols-1 md:grid-cols-3 gap-8`
9. **Positioning** — `sticky top-0 z-50`, `relative`, `absolute -top-4 left-1/2 -translate-x-1/2`
10. **Shadows and borders** — `shadow-sm`, `shadow-xl`, `rounded-xl`, `border-t border-gray-700`
</details>

---

**End of Practice Questions — Week 15: Tailwind CSS Components & Project**
