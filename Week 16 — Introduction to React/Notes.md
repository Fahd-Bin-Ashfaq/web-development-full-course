# Week 16 — Introduction to React

> **Prerequisites:** HTML, CSS, JavaScript (ES6+), Git & GitHub, Tailwind CSS
> **Goal:** Understand what React is, set up a project, and build your first components using JSX.

---

## Table of Contents

1. [What is React?](#1-what-is-react)
2. [Single Page Applications (SPA)](#2-single-page-applications-spa)
3. [Setting Up a React Project](#3-setting-up-a-react-project)
4. [JSX — JavaScript XML](#4-jsx--javascript-xml)
5. [Components](#5-components)
6. [Rendering Lists](#6-rendering-lists)
7. [Conditional Rendering](#7-conditional-rendering)
8. [Styling in React](#8-styling-in-react)
9. [Fragments](#9-fragments)
10. [Summary](#10-summary)

---

## 1. What is React?

**React** is an open-source JavaScript **library** for building user interfaces. It was created by **Facebook (now Meta)** in 2013 and has since become the most widely used front-end library in the world.

> Think of React as a set of power tools for building websites. You already know how to build things with hand tools (vanilla HTML, CSS, and JavaScript). React gives you power tools that make the job faster, more organized, and easier to maintain — especially as projects grow larger.

### Why React?

| Reason                  | Explanation                                                                 |
|-------------------------|-----------------------------------------------------------------------------|
| **Component-Based**     | Build small, reusable pieces of UI and compose them together.               |
| **Virtual DOM**         | React updates only what changed, not the entire page. This makes it fast.   |
| **Huge Ecosystem**      | Thousands of libraries, tools, and tutorials are available.                 |
| **Job Market Demand**   | React is the most requested front-end skill in job listings worldwide.      |
| **Backed by Meta**      | Actively maintained by one of the largest tech companies.                   |
| **Learn Once, Use Everywhere** | React Native lets you build mobile apps with the same concepts.     |

### How the Virtual DOM Works

```
   REAL DOM (Browser)              VIRTUAL DOM (React's Copy)
  +-------------------+           +-------------------+
  |     <html>        |           |     <html>        |
  |  +-------------+  |           |  +-------------+  |
  |  |  <header>   |  |           |  |  <header>   |  |
  |  +-------------+  |           |  +-------------+  |
  |  +-------------+  |           |  +-------------+  |
  |  |  <main>     |  |  <----->  |  |  <main>  *  |  | (* changed)
  |  |  +-------+  |  |           |  |  +-------+  |  |
  |  |  | <p>   |  |  |           |  |  | <p> * |  |  |
  |  |  +-------+  |  |           |  |  +-------+  |  |
  |  +-------------+  |           |  +-------------+  |
  |  +-------------+  |           |  +-------------+  |
  |  |  <footer>   |  |           |  |  <footer>   |  |
  |  +-------------+  |           |  +-------------+  |
  +-------------------+           +-------------------+

  Step 1: React keeps a lightweight copy of the DOM in memory (Virtual DOM).
  Step 2: When data changes, React creates a NEW Virtual DOM.
  Step 3: React COMPARES the old and new Virtual DOMs (this is called "diffing").
  Step 4: React updates ONLY the parts that changed in the Real DOM.

  Result: Faster updates because we avoid re-rendering the entire page.
```

### React vs Vanilla JavaScript — A Counter Example

Building a simple counter helps you see the difference immediately.

**Vanilla JavaScript:**

```html
<!-- index.html -->
<!DOCTYPE html>
<html>
<body>
  <h1>Counter</h1>
  <p id="count">0</p>
  <button id="increment">+</button>
  <button id="decrement">-</button>

  <script>
    let count = 0;
    const countDisplay = document.getElementById("count");
    const incrementBtn = document.getElementById("increment");
    const decrementBtn = document.getElementById("decrement");

    incrementBtn.addEventListener("click", () => {
      count++;
      countDisplay.textContent = count;
    });

    decrementBtn.addEventListener("click", () => {
      count--;
      countDisplay.textContent = count;
    });
  </script>
</body>
</html>
```

**React:**

```jsx
// Counter.jsx
import { useState } from "react";

function Counter() {
  const [count, setCount] = useState(0);

  return (
    <div>
      <h1>Counter</h1>
      <p>{count}</p>
      <button onClick={() => setCount(count + 1)}>+</button>
      <button onClick={() => setCount(count - 1)}>-</button>
    </div>
  );
}

export default Counter;
```

**Key differences:**

| Aspect                | Vanilla JS                              | React                                    |
|-----------------------|-----------------------------------------|------------------------------------------|
| DOM manipulation      | Manual (`getElementById`, `textContent`)| Automatic (React handles it)             |
| State management      | Variables + manual UI updates           | `useState` — UI updates automatically    |
| Code organization     | All in one place, gets messy at scale   | Separated into reusable components       |
| Event handling        | `addEventListener`                      | Inline: `onClick`, `onChange`            |
| Scalability           | Difficult for large apps                | Designed for large applications          |

> In vanilla JS, **you** are responsible for keeping the UI in sync with the data. In React, **you describe what the UI should look like**, and React keeps it in sync for you.

---

## 2. Single Page Applications (SPA)

### What is a SPA?

A **Single Page Application** is a web application that loads a single HTML page and dynamically updates the content as the user interacts with the app — **without full page reloads**.

> **Real-life analogy:** Think of a traditional website like reading a physical book — you turn pages (page reloads) to see new content. A SPA is like using a tablet — you tap and the content changes on the same screen, instantly. It feels like a mobile app running in your browser.

### SPA vs Multi-Page Application (MPA)

```
  MULTI-PAGE APPLICATION (Traditional)
  =====================================

  User clicks "About"
       |
       v
  +----------+    Full Page    +----------+    Full Page    +----------+
  |          |    Reload       |          |    Reload       |          |
  |  HOME    | -------------> |  ABOUT   | -------------> | CONTACT  |
  |  PAGE    |    (Server     |  PAGE    |    (Server     |  PAGE    |
  |          |    sends new   |          |    sends new   |          |
  |          |    HTML file)  |          |    HTML file)  |          |
  +----------+                +----------+                +----------+
    home.html                  about.html                 contact.html

  - Each page is a separate HTML file
  - Browser reloads entirely on every navigation
  - White flash / loading between pages
  - Server does more work


  SINGLE PAGE APPLICATION (React)
  ================================

  User clicks "About"
       |
       v
  +------------------------------------------------------------------+
  |                        index.html (ONE file)                     |
  |                                                                  |
  |  +----------+    Content    +----------+    Content               |
  |  |          |    Swap       |          |    Swap                  |
  |  |  HOME    | ----------> |  ABOUT   | ----------> | CONTACT  | |
  |  |  View    |  (No reload) |  View    |  (No reload)|  View    | |
  |  |          |              |          |             |          | |
  |  +----------+              +----------+             +----------+ |
  |                                                                  |
  +------------------------------------------------------------------+

  - ONE HTML file, JavaScript swaps the content
  - No page reload — instant transitions
  - Feels like a native mobile app
  - Server sends data (JSON), not pages
```

### How React Handles Routing

React uses a library called **React Router** to handle navigation without page reloads. We will cover React Router in detail in a later week, but here is the basic idea:

1. The browser loads `index.html` once.
2. React takes over and renders the correct component based on the URL.
3. When the user clicks a link, React swaps the displayed component — the page does not reload.

```
  URL: /home      ---->  React renders <Home />
  URL: /about     ---->  React renders <About />
  URL: /contact   ---->  React renders <Contact />

  All within the same index.html — no server round-trip.
```

---

## 3. Setting Up a React Project

### Using Vite (Recommended)

**Vite** (pronounced "veet," French for "fast") is a modern build tool that provides an extremely fast development experience. It is the recommended way to start a new React project.

> Older tutorials may reference Create React App (CRA). CRA is **no longer recommended** by the React team. Always use Vite for new projects.

### Step-by-Step Setup

**Step 1: Create a new project**

```bash
npm create vite@latest my-app -- --template react
```

**Step 2: Navigate into the project**

```bash
cd my-app
```

**Step 3: Install dependencies**

```bash
npm install
```

**Step 4: Start the development server**

```bash
npm run dev
```

The terminal will display something like:

```
  VITE v5.x.x  ready in 300ms

  ->  Local:   http://localhost:5173/
  ->  Network: http://192.168.1.5:5173/
```

Open `http://localhost:5173/` in your browser to see your React app running.

### Project Folder Structure

```
my-app/
  |
  +-- node_modules/          # All installed packages (managed by npm)
  |
  +-- public/                # Static assets served as-is
  |     +-- vite.svg         # Vite logo (example static file)
  |
  +-- src/                   # YOUR CODE LIVES HERE
  |     +-- assets/          # Images, fonts, etc. used in components
  |     |     +-- react.svg  # React logo (example asset)
  |     |
  |     +-- App.css          # Styles for the App component
  |     +-- App.jsx          # Main App component (your starting point)
  |     +-- index.css        # Global styles
  |     +-- main.jsx         # Entry point — mounts React to the DOM
  |
  +-- .eslintrc.cjs          # ESLint configuration (code quality rules)
  +-- .gitignore             # Files/folders Git should ignore
  +-- index.html             # The single HTML page (React mounts here)
  +-- package.json           # Project metadata, scripts, and dependencies
  +-- package-lock.json      # Locked dependency versions
  +-- vite.config.js         # Vite configuration
```

### What Each File Does

| File / Folder      | Purpose                                                                       |
|---------------------|-------------------------------------------------------------------------------|
| `node_modules/`     | Contains all npm packages. Never edit this. Never commit to Git.              |
| `public/`           | Static files that are served directly (favicons, robots.txt, etc.).           |
| `src/`              | All your React code goes here. This is where you spend 99% of your time.     |
| `src/main.jsx`      | The entry point. It renders the `<App />` component into `index.html`.       |
| `src/App.jsx`       | The root component. All other components are nested inside this.             |
| `index.html`        | The single HTML file. Contains a `<div id="root">` where React mounts.      |
| `package.json`      | Lists your project's dependencies and defines scripts like `npm run dev`.    |
| `vite.config.js`    | Configuration for Vite (plugins, port, build settings, etc.).                |

### Understanding main.jsx

```jsx
// src/main.jsx
import React from "react";
import ReactDOM from "react-dom/client";
import App from "./App.jsx";
import "./index.css";

ReactDOM.createRoot(document.getElementById("root")).render(
  <React.StrictMode>
    <App />
  </React.StrictMode>
);
```

What this does, line by line:

1. **Import React** — the core library.
2. **Import ReactDOM** — the library that connects React to the browser DOM.
3. **Import App** — your root component.
4. **Import styles** — global CSS.
5. **Mount React** — find the `<div id="root">` in `index.html` and render `<App />` inside it.

---

## 4. JSX — JavaScript XML

### What is JSX?

**JSX** stands for **JavaScript XML**. It is a syntax extension that lets you write HTML-like code directly inside JavaScript. JSX is not valid JavaScript on its own — tools like Vite transform it into regular JavaScript behind the scenes.

> **Real-life analogy:** Writing vanilla JS DOM code is like giving someone directions using GPS coordinates. JSX is like giving them a street address. Both get you to the same place, but one is much easier to read and write.

**Without JSX (plain JavaScript):**

```js
const element = React.createElement("h1", { className: "title" }, "Hello, World!");
```

**With JSX:**

```jsx
const element = <h1 className="title">Hello, World!</h1>;
```

Both produce the exact same result, but JSX is far more readable.

### JSX Rules

#### Rule 1: Return a Single Parent Element

Every component must return **one** root element. If you have multiple elements, wrap them in a parent `<div>` or use a Fragment (`<> </>`).

```jsx
// WRONG - multiple root elements
function App() {
  return (
    <h1>Title</h1>
    <p>Paragraph</p>
  );
}

// CORRECT - wrapped in a single parent
function App() {
  return (
    <div>
      <h1>Title</h1>
      <p>Paragraph</p>
    </div>
  );
}

// ALSO CORRECT - using a Fragment (no extra div in the DOM)
function App() {
  return (
    <>
      <h1>Title</h1>
      <p>Paragraph</p>
    </>
  );
}
```

#### Rule 2: Use `className` Instead of `class`

In HTML you write `class`. In JSX you write `className` because `class` is a reserved keyword in JavaScript.

```jsx
// HTML
<div class="container">Hello</div>

// JSX
<div className="container">Hello</div>
```

#### Rule 3: Use `htmlFor` Instead of `for`

In HTML labels, you write `for`. In JSX you write `htmlFor` because `for` is a reserved keyword in JavaScript.

```jsx
// HTML
<label for="email">Email</label>

// JSX
<label htmlFor="email">Email</label>
```

#### Rule 4: camelCase for Attributes

HTML attributes that are multi-word become camelCase in JSX.

```jsx
// HTML                          // JSX
onclick="handleClick()"          onClick={handleClick}
onchange="handleChange()"       onChange={handleChange}
tabindex="1"                     tabIndex="1"
maxlength="50"                   maxLength="50"
```

#### Rule 5: Self-Closing Tags Are Required

Tags that don't have children must self-close in JSX.

```jsx
// HTML (valid without self-closing)
<img src="photo.jpg">
<input type="text">
<br>

// JSX (MUST self-close)
<img src="photo.jpg" />
<input type="text" />
<br />
```

#### Rule 6: JavaScript Expressions in Curly Braces

Use `{}` to embed any JavaScript expression inside JSX.

```jsx
function Greeting() {
  const name = "Ahmed";
  const currentHour = new Date().getHours();

  return (
    <div>
      <h1>Hello, {name}!</h1>
      <p>It is currently {currentHour}:00</p>
      <p>2 + 2 = {2 + 2}</p>
      <p>{name.toUpperCase()}</p>
    </div>
  );
}
```

### JSX vs HTML Comparison Table

| Feature              | HTML                          | JSX                            |
|----------------------|-------------------------------|--------------------------------|
| CSS classes          | `class="btn"`                 | `className="btn"`              |
| Label `for`          | `for="name"`                  | `htmlFor="name"`               |
| Inline styles        | `style="color: red"`          | `style={{ color: "red" }}`     |
| Event handlers       | `onclick="fn()"`              | `onClick={fn}`                 |
| Self-closing tags    | `<br>` (optional)             | `<br />` (required)            |
| Multi-word attrs     | `tabindex`, `maxlength`       | `tabIndex`, `maxLength`        |
| Embedding JS         | Not possible directly         | `{expression}`                 |
| Comments             | `<!-- comment -->`            | `{/* comment */}`              |
| Boolean attributes   | `disabled`                    | `disabled={true}` or `disabled`|

---

## 5. Components

### What is a Component?

A **component** is a reusable, self-contained piece of UI. Every React application is made up of components.

> **Real-life analogy:** Think of LEGO blocks. Each block is a component — a button, a navigation bar, a card, a footer. Individually they are small and simple. But you snap them together to build an entire structure. If you want to change the color of one block, you only change that block — nothing else breaks.

```
  A Website Built from Components
  ================================

  +--------------------------------------------------+
  |                  <App />                          |
  |                                                  |
  |  +----------------------------------------------+|
  |  |              <Header />                      ||
  |  |   [Logo]    [Home] [About] [Contact]         ||
  |  +----------------------------------------------+|
  |                                                  |
  |  +----------------------------------------------+|
  |  |              <Main />                        ||
  |  |                                              ||
  |  |  +----------+  +----------+  +----------+   ||
  |  |  | <Card /> |  | <Card /> |  | <Card /> |   ||
  |  |  |          |  |          |  |          |   ||
  |  |  | [image]  |  | [image]  |  | [image]  |   ||
  |  |  | [title]  |  | [title]  |  | [title]  |   ||
  |  |  | [text]   |  | [text]   |  | [text]   |   ||
  |  |  | [button] |  | [button] |  | [button] |   ||
  |  |  +----------+  +----------+  +----------+   ||
  |  |                                              ||
  |  +----------------------------------------------+|
  |                                                  |
  |  +----------------------------------------------+|
  |  |              <Footer />                      ||
  |  |   (c) 2025 MyWebsite. All rights reserved.  ||
  |  +----------------------------------------------+|
  |                                                  |
  +--------------------------------------------------+
```

### Functional Components (The Modern Way)

In React, there are two types of components: **class components** (old) and **functional components** (modern). We will only use **functional components** because they are simpler, cleaner, and the standard in modern React.

A functional component is simply a JavaScript function that returns JSX.

```jsx
function Welcome() {
  return <h1>Welcome to React!</h1>;
}
```

That is it. A function that returns JSX is a React component.

### Component Naming Convention

React components **must** start with an **uppercase letter** (PascalCase). This is how React distinguishes between HTML elements and custom components.

```jsx
// CORRECT (PascalCase)
function UserProfile() { ... }
function NavBar() { ... }
function ProductCard() { ... }

// WRONG (lowercase — React treats these as HTML tags)
function userProfile() { ... }
function navbar() { ... }
```

### Creating Your First Component

**File: `src/components/Greeting.jsx`**

```jsx
function Greeting() {
  const name = "Student";

  return (
    <div>
      <h1>Hello, {name}!</h1>
      <p>Welcome to your first React component.</p>
    </div>
  );
}

export default Greeting;
```

### Importing and Exporting Components

React uses JavaScript's module system (ES Modules) to share components between files.

**Default Export (one per file):**

```jsx
// Greeting.jsx
function Greeting() {
  return <h1>Hello!</h1>;
}
export default Greeting;

// App.jsx — import with any name
import Greeting from "./components/Greeting";
import MyGreeting from "./components/Greeting"; // also valid
```

**Named Export (multiple per file):**

```jsx
// utils.jsx
export function Greeting() {
  return <h1>Hello!</h1>;
}
export function Farewell() {
  return <h1>Goodbye!</h1>;
}

// App.jsx — import with exact name inside curly braces
import { Greeting, Farewell } from "./components/utils";
```

### Component Tree

Every React app has a **component tree** — a hierarchy showing how components are nested inside each other. The root of the tree is always the `<App />` component.

```
  Component Tree
  ==============

                         App
                          |
            +-------------+-------------+
            |             |             |
         Header         Main         Footer
            |             |
     +------+------+     |
     |      |      |     |
   Logo  NavLink NavLink |
                         |
                   +-----+-----+
                   |     |     |
                 Card  Card  Card
                   |
              +----+----+
              |    |    |
           Image Title Button
```

### Using a Component in App.jsx

```jsx
// src/App.jsx
import Header from "./components/Header";
import Main from "./components/Main";
import Footer from "./components/Footer";

function App() {
  return (
    <div>
      <Header />
      <Main />
      <Footer />
    </div>
  );
}

export default App;
```

### Nesting Components

Components can contain other components. This is how you build complex UIs from simple pieces.

```jsx
// src/components/Header.jsx
function Logo() {
  return <img src="/logo.png" alt="Logo" />;
}

function NavLink({ text }) {
  return <a href="#">{text}</a>;
}

function Header() {
  return (
    <header>
      <Logo />
      <nav>
        <NavLink text="Home" />
        <NavLink text="About" />
        <NavLink text="Contact" />
      </nav>
    </header>
  );
}

export default Header;
```

In this example, `Header` is composed of `Logo` and multiple `NavLink` components. Each piece is simple. Together, they form a complete header.

---

## 6. Rendering Lists

In real applications, you often need to display a list of items — products, users, messages, etc. React uses JavaScript's `.map()` method to render arrays of data as components.

### Using .map() to Render Arrays

```jsx
function FruitList() {
  const fruits = ["Apple", "Banana", "Cherry", "Date", "Elderberry"];

  return (
    <ul>
      {fruits.map((fruit, index) => (
        <li key={index}>{fruit}</li>
      ))}
    </ul>
  );
}
```

**A more realistic example with objects:**

```jsx
function StudentList() {
  const students = [
    { id: 1, name: "Ahmed", grade: "A" },
    { id: 2, name: "Sara", grade: "B+" },
    { id: 3, name: "Ali", grade: "A-" },
    { id: 4, name: "Fatima", grade: "A+" },
  ];

  return (
    <table>
      <thead>
        <tr>
          <th>Name</th>
          <th>Grade</th>
        </tr>
      </thead>
      <tbody>
        {students.map((student) => (
          <tr key={student.id}>
            <td>{student.name}</td>
            <td>{student.grade}</td>
          </tr>
        ))}
      </tbody>
    </table>
  );
}
```

### The `key` Prop — Why It Matters

When rendering lists, React requires a **`key`** prop on each item. The key helps React identify which items have changed, been added, or been removed.

```
  Without keys, React has no way to know which item changed:

  Before:                After (added "Mango"):
  +----------+           +----------+
  | Apple    |           | Mango    |   <-- Is this new or renamed?
  +----------+           +----------+
  | Banana   |           | Apple    |   <-- Did this move?
  +----------+           +----------+
  | Cherry   |           | Banana   |   <-- React is confused.
  +----------+           +----------+
                          | Cherry   |
                          +----------+

  With keys, React tracks each item precisely:

  Before:                After:
  +--key=1--+            +--key=4--+   <-- New item! Insert it.
  | Apple   |            | Mango   |
  +--key=2--+            +--key=1--+   <-- Same item, just moved.
  | Banana  |            | Apple   |
  +--key=3--+            +--key=2--+   <-- Same item, just moved.
  | Cherry  |            | Banana  |
  +---------+            +--key=3--+
                          | Cherry  |
                          +---------+
```

**Rules for keys:**

| Rule                                      | Example                          |
|-------------------------------------------|----------------------------------|
| Keys must be **unique** among siblings    | Use `id` from your data          |
| Keys should be **stable** (not change)    | Database IDs are ideal           |
| **Avoid using array index** as key        | Index changes when items reorder |
| Keys are **not passed** as a prop         | You cannot access `props.key`    |

```jsx
// GOOD - using a unique, stable ID
{students.map((student) => (
  <StudentCard key={student.id} name={student.name} />
))}

// AVOID - using array index (only acceptable for static lists that never reorder)
{students.map((student, index) => (
  <StudentCard key={index} name={student.name} />
))}
```

---

## 7. Conditional Rendering

Sometimes you want to show or hide UI elements based on certain conditions. React gives you several ways to do this.

### Using if Statements

You can use regular `if` statements **before** the return.

```jsx
function UserGreeting({ isLoggedIn }) {
  if (isLoggedIn) {
    return <h1>Welcome back!</h1>;
  }

  return <h1>Please sign in.</h1>;
}
```

### Ternary Operator in JSX

The ternary operator (`condition ? trueResult : falseResult`) works directly inside JSX, making it the most common approach for inline conditional rendering.

```jsx
function UserGreeting({ isLoggedIn }) {
  return (
    <div>
      <h1>{isLoggedIn ? "Welcome back!" : "Please sign in."}</h1>
      {isLoggedIn ? (
        <button>Log Out</button>
      ) : (
        <button>Log In</button>
      )}
    </div>
  );
}
```

### && (Short-Circuit) Operator

Use `&&` when you want to render something **or nothing** — there is no "else" case.

```jsx
function Notifications({ count }) {
  return (
    <div>
      <h1>Dashboard</h1>
      {count > 0 && <p>You have {count} new notifications.</p>}
    </div>
  );
}

// If count is 5:  renders the <p> tag
// If count is 0:  renders nothing (the <p> is skipped entirely)
```

### When to Use Which

```
  Decision Guide for Conditional Rendering
  =========================================

  Do you need to render
  one thing OR another?
        |
        +-- YES --> Use TERNARY operator
        |           condition ? <A /> : <B />
        |
        +-- NO
             |
             Do you need to render
             something OR nothing?
                   |
                   +-- YES --> Use && operator
                   |           condition && <A />
                   |
                   +-- NO
                        |
                        Is the logic complex
                        (multiple conditions)?
                              |
                              +-- YES --> Use IF/ELSE before return
                              |
                              +-- NO --> Ternary is fine
```

**A practical example combining all three:**

```jsx
function ProductPage({ product, isLoggedIn, reviews }) {
  // Complex logic: use if/else before return
  let badge;
  if (product.stock === 0) {
    badge = <span className="badge-red">Out of Stock</span>;
  } else if (product.stock < 5) {
    badge = <span className="badge-yellow">Low Stock</span>;
  } else {
    badge = <span className="badge-green">In Stock</span>;
  }

  return (
    <div>
      <h1>{product.name}</h1>
      {badge}

      {/* Ternary: one thing or another */}
      <p>{product.onSale ? "ON SALE!" : "Regular Price"}</p>

      {/* Short-circuit: something or nothing */}
      {isLoggedIn && <button>Add to Cart</button>}
      {reviews.length > 0 && <ReviewList reviews={reviews} />}
    </div>
  );
}
```

---

## 8. Styling in React

React supports multiple approaches to styling. Each has its use cases.

### Inline Styles

In React, inline styles are written as JavaScript objects with camelCase property names. The `style` attribute accepts an object, not a string.

```jsx
function InlineExample() {
  const headingStyle = {
    color: "navy",
    fontSize: "24px",          // camelCase, not font-size
    backgroundColor: "#f0f0f0", // camelCase, not background-color
    padding: "16px",
    borderRadius: "8px",
  };

  return (
    <div>
      <h1 style={headingStyle}>Styled Heading</h1>
      <p style={{ color: "gray", marginTop: "8px" }}>Styled paragraph.</p>
    </div>
  );
}
```

> **Note:** The double curly braces `{{ }}` are not special syntax. The outer `{}` is the JSX expression wrapper. The inner `{}` is the JavaScript object literal.

### CSS Modules

CSS Modules are CSS files where class names are scoped locally by default, preventing naming conflicts across components.

**File: `Button.module.css`**

```css
.primary {
  background-color: #3b82f6;
  color: white;
  padding: 8px 16px;
  border: none;
  border-radius: 4px;
  cursor: pointer;
}

.primary:hover {
  background-color: #2563eb;
}
```

**File: `Button.jsx`**

```jsx
import styles from "./Button.module.css";

function Button({ children }) {
  return <button className={styles.primary}>{children}</button>;
}

export default Button;
```

The actual class name in the DOM will be something like `Button_primary_x7ks3`, ensuring it never conflicts with another `.primary` class in a different component.

### Using Tailwind CSS with React (Our Preferred Approach)

Since you already know Tailwind CSS from Weeks 14 and 15, the good news is that Tailwind works beautifully with React. You simply use `className` instead of `class`.

**Setting up Tailwind in a Vite + React project:**

```bash
npm install -D tailwindcss @tailwindcss/vite
```

**Update `vite.config.js`:**

```js
import { defineConfig } from "vite";
import react from "@vitejs/plugin-react";
import tailwindcss from "@tailwindcss/vite";

export default defineConfig({
  plugins: [react(), tailwindcss()],
});
```

**Update `src/index.css`:**

```css
@import "tailwindcss";
```

**Using Tailwind in components:**

```jsx
function ProductCard({ name, price, image }) {
  return (
    <div className="max-w-sm rounded-lg overflow-hidden shadow-lg bg-white">
      <img className="w-full h-48 object-cover" src={image} alt={name} />
      <div className="p-4">
        <h2 className="text-xl font-bold text-gray-800">{name}</h2>
        <p className="text-green-600 font-semibold mt-2">${price}</p>
        <button className="mt-4 w-full bg-blue-500 text-white py-2 px-4 rounded hover:bg-blue-600 transition">
          Add to Cart
        </button>
      </div>
    </div>
  );
}
```

Everything you learned about Tailwind applies directly — the only difference is writing `className` instead of `class`.

### className with Dynamic Values

You can dynamically assign classes using template literals or conditional logic.

```jsx
function Alert({ type, message }) {
  // Using template literals
  const baseClasses = "p-4 rounded-lg border";
  const typeClasses = {
    success: "bg-green-100 border-green-500 text-green-700",
    error: "bg-red-100 border-red-500 text-red-700",
    warning: "bg-yellow-100 border-yellow-500 text-yellow-700",
  };

  return (
    <div className={`${baseClasses} ${typeClasses[type]}`}>
      {message}
    </div>
  );
}

// Usage:
// <Alert type="success" message="File saved successfully!" />
// <Alert type="error" message="Something went wrong." />
```

### Styling Approaches Comparison

| Approach        | Scoped? | Dynamic? | Learning Curve | Best For                          |
|-----------------|---------|----------|----------------|-----------------------------------|
| Inline Styles   | Yes     | Yes      | Low            | Quick prototyping, one-off styles |
| CSS Modules     | Yes     | Limited  | Low            | Component-specific styles         |
| Tailwind CSS    | Yes     | Yes      | Medium         | Full projects (our preference)    |
| Plain CSS       | No      | No       | Low            | Small projects, global styles     |

---

## 9. Fragments

### What are Fragments?

A **Fragment** lets you group a list of child elements **without adding an extra node to the DOM**. Remember JSX Rule #1 — you must return a single parent element. Fragments solve this without polluting your HTML with unnecessary `<div>` wrappers.

### Using Fragments

**Long form:**

```jsx
import { Fragment } from "react";

function Columns() {
  return (
    <Fragment>
      <td>Column 1</td>
      <td>Column 2</td>
      <td>Column 3</td>
    </Fragment>
  );
}
```

**Shorthand (preferred):**

```jsx
function Columns() {
  return (
    <>
      <td>Column 1</td>
      <td>Column 2</td>
      <td>Column 3</td>
    </>
  );
}
```

### When and Why to Use Fragments

**Problem without Fragments:**

```jsx
// This creates an invalid HTML structure:
// <table> <tr> <div> <td>...</td> </div> </tr> </table>
function Columns() {
  return (
    <div>          {/* This div breaks the table structure! */}
      <td>Column 1</td>
      <td>Column 2</td>
    </div>
  );
}
```

**Solution with Fragments:**

```jsx
// Clean HTML output:
// <table> <tr> <td>...</td> <td>...</td> </tr> </table>
function Columns() {
  return (
    <>              {/* No extra element in the DOM */}
      <td>Column 1</td>
      <td>Column 2</td>
    </>
  );
}
```

> **Use `<Fragment>` (long form) when you need to pass a `key` prop** (e.g., rendering a list). The shorthand `<> </>` does not support attributes.

```jsx
// Long form is required when mapping with keys
{items.map((item) => (
  <Fragment key={item.id}>
    <dt>{item.term}</dt>
    <dd>{item.description}</dd>
  </Fragment>
))}
```

---

## 10. Summary

Here is a recap of everything covered in this week:

```
  Week 16 — What You Learned
  ============================

  React Basics
    +-- What is React? (Library for building UIs, created by Meta)
    +-- Virtual DOM (efficient updates by diffing)
    +-- SPA vs MPA (single page vs multi-page)

  Project Setup
    +-- Vite (modern, fast build tool)
    +-- Folder structure (src/, public/, main.jsx, App.jsx)
    +-- npm run dev (start the dev server)

  JSX
    +-- HTML-like syntax in JavaScript
    +-- className, htmlFor, camelCase, self-closing tags
    +-- {} for JavaScript expressions

  Components
    +-- Reusable UI building blocks
    +-- Functional components (modern standard)
    +-- PascalCase naming
    +-- Import/export system
    +-- Component tree (nesting components)

  Lists & Conditional Rendering
    +-- .map() for rendering arrays
    +-- key prop for list items
    +-- Ternary operator for "this or that"
    +-- && operator for "this or nothing"
    +-- if/else for complex logic

  Styling
    +-- Inline styles (JavaScript objects)
    +-- CSS Modules (scoped class names)
    +-- Tailwind CSS (our preferred approach)
    +-- Dynamic className values

  Fragments
    +-- <> </> to group without extra DOM nodes
    +-- <Fragment key={...}> when keys are needed
```

### Key Takeaways

1. **React is a library, not a framework.** It focuses on the UI layer and lets you choose other tools for routing, state management, etc.
2. **Components are the core building block.** Think of every piece of your UI as a component.
3. **JSX is not HTML.** It looks similar, but has its own rules (`className`, camelCase, self-closing tags, etc.).
4. **Always use unique, stable keys** when rendering lists.
5. **React takes care of the DOM for you.** You describe *what* the UI should look like, and React figures out *how* to update it efficiently.

### What is Coming Next

In **Week 17**, we will learn about **Props and Component Communication** — how to pass data from parent components to child components, making your components truly dynamic and reusable.

---

> **Practice Assignment:** Create a new React project with Vite. Build a simple "Student Card" component that displays a name, grade, and a profile image. Then render a list of five students using `.map()` on an array of student objects. Style everything with Tailwind CSS.
