# Week 16 — Introduction to React: Practice Questions

**Total Questions: 20** (10 MCQs + 5 Short Answer + 5 Coding Exercises)

---

## Part 1: Multiple Choice Questions (MCQs)

**1. What is the correct way to create a new React project using Vite?**

- A) `npx create-react-app my-app`
- B) `npm create vite@latest my-app -- --template react`
- C) `npm install react`
- D) `npx vite create my-app`

<details>
<summary>Answer</summary>

**B) `npm create vite@latest my-app -- --template react`**

Vite is the recommended build tool for modern React projects. The command scaffolds a new project with the React template, providing faster development server startup and hot module replacement compared to older tools.
</details>

---

**2. Which of the following is valid JSX?**

- A) `<div class="container">Hello</div>`
- B) `<div className="container">Hello</div>`
- C) `<div className="container">Hello</div><p>World</p>`
- D) `<div Class="container">Hello</div>`

<details>
<summary>Answer</summary>

**B) `<div className="container">Hello</div>`**

In JSX, the HTML `class` attribute must be written as `className` because `class` is a reserved keyword in JavaScript. Option C is invalid because JSX expressions must have a single parent element.
</details>

---

**3. What must a React component function always return?**

- A) A string
- B) An array of HTML elements
- C) A single JSX element (or `null`)
- D) Multiple sibling JSX elements without a wrapper

<details>
<summary>Answer</summary>

**C) A single JSX element (or `null`)**

A React component must return a single root element. If you need to return multiple sibling elements without adding an extra DOM node, you can use a React Fragment (`<>...</>` or `<React.Fragment>...</React.Fragment>`).
</details>

---

**4. What is the purpose of React Fragments (`<>...</>`)?**

- A) To add styling to components
- B) To group multiple elements without adding an extra DOM node
- C) To create reusable components
- D) To handle events in React

<details>
<summary>Answer</summary>

**B) To group multiple elements without adding an extra DOM node**

Fragments let you return multiple elements from a component without wrapping them in an unnecessary `<div>` or other HTML element, keeping the DOM clean.
</details>

---

**5. How do you embed a JavaScript expression inside JSX?**

- A) `{{ expression }}`
- B) `{ expression }`
- C) `${ expression }`
- D) `<% expression %>`

<details>
<summary>Answer</summary>

**B) `{ expression }`**

Single curly braces are used to embed JavaScript expressions inside JSX. This allows you to dynamically render values, call functions, or evaluate expressions directly within your markup.
</details>

---

**6. What is the primary advantage of React over vanilla JavaScript for building UIs?**

- A) React makes websites load faster by default
- B) React provides a component-based architecture with declarative UI updates
- C) React eliminates the need for CSS
- D) React does not require a build step

<details>
<summary>Answer</summary>

**B) React provides a component-based architecture with declarative UI updates**

React allows developers to build UIs from reusable components and uses a declarative approach where you describe what the UI should look like for a given state. React then efficiently updates the DOM to match, eliminating the need for manual DOM manipulation.
</details>

---

**7. When rendering a list of elements using `.map()`, what special prop must each element have?**

- A) `id`
- B) `index`
- C) `key`
- D) `ref`

<details>
<summary>Answer</summary>

**C) `key`**

Each element in a list rendered with `.map()` must have a unique `key` prop. Keys help React identify which items have changed, been added, or removed, enabling efficient re-rendering. Ideally, keys should be stable, unique identifiers (such as database IDs), not array indices.
</details>

---

**8. Which of the following correctly renders content conditionally in JSX?**

- A) `{ if (isLoggedIn) return <p>Welcome</p> }`
- B) `{ isLoggedIn && <p>Welcome</p> }`
- C) `{ isLoggedIn ? <p>Welcome</p> }`
- D) `<if condition={isLoggedIn}><p>Welcome</p></if>`

<details>
<summary>Answer</summary>

**B) `{ isLoggedIn && <p>Welcome</p> }`**

The logical AND (`&&`) operator is a common pattern for conditional rendering in JSX. If `isLoggedIn` is `true`, the `<p>` element is rendered; if `false`, nothing is rendered. You can also use the ternary operator (`condition ? <A /> : <B />`) for if/else scenarios. The `if` statement cannot be used directly inside JSX curly braces because it is a statement, not an expression.
</details>

---

**9. What is the output of the following JSX?**

```jsx
const name = "React";
return <h1>Hello, {name.toUpperCase()}!</h1>;
```

- A) `Hello, {name.toUpperCase()}!`
- B) `Hello, React!`
- C) `Hello, REACT!`
- D) An error is thrown

<details>
<summary>Answer</summary>

**C) `Hello, REACT!`**

The expression inside the curly braces is evaluated as JavaScript. `name.toUpperCase()` converts the string `"React"` to `"REACT"`, which is then rendered inside the `<h1>` element.
</details>

---

**10. Which file serves as the entry point in a Vite-based React project?**

- A) `index.html` and `src/main.jsx`
- B) `src/App.js` only
- C) `public/index.html` only
- D) `server.js`

<details>
<summary>Answer</summary>

**A) `index.html` and `src/main.jsx`**

In a Vite-based React project, `index.html` in the project root is the HTML entry point, and it includes a `<script>` tag that references `src/main.jsx`. The `main.jsx` file uses `ReactDOM.createRoot()` to render the root `<App />` component into the DOM.
</details>

---

## Part 2: Short Answer Questions

**1. What is React, and why is it used in modern web development?**

<details>
<summary>Answer</summary>

React is an open-source JavaScript library developed by Meta (Facebook) for building user interfaces, particularly single-page applications. It is used in modern web development because it offers a component-based architecture that promotes code reusability, a Virtual DOM that optimizes UI updates for performance, a declarative syntax that makes code easier to understand and debug, and a large ecosystem of tools and libraries that accelerate development.
</details>

---

**2. What is JSX, and how does it differ from regular HTML?**

<details>
<summary>Answer</summary>

JSX (JavaScript XML) is a syntax extension for JavaScript that allows you to write HTML-like markup directly within JavaScript code. Key differences from regular HTML include: attributes use camelCase naming (`className` instead of `class`, `onClick` instead of `onclick`), all tags must be closed (including self-closing tags like `<img />`), JavaScript expressions can be embedded using curly braces `{}`, and a component must return a single root element. JSX is not valid JavaScript on its own; it is transformed into `React.createElement()` calls by a compiler like Babel during the build process.
</details>

---

**3. What is a Single-Page Application (SPA), and how does React support this architecture?**

<details>
<summary>Answer</summary>

A Single-Page Application is a web application that loads a single HTML page and dynamically updates the content as the user interacts with it, without requiring full page reloads from the server. React supports SPA architecture by rendering components dynamically based on application state, managing UI updates efficiently through the Virtual DOM, and integrating with routing libraries (such as React Router) that handle navigation on the client side. This results in faster, more fluid user experiences that feel similar to native applications.
</details>

---

**4. What is a React component, and what are the rules for naming one?**

<details>
<summary>Answer</summary>

A React component is a reusable, self-contained piece of UI that can accept inputs (props) and returns JSX describing what should appear on screen. In modern React, components are typically written as JavaScript functions. The naming rules are: the component name must start with an uppercase letter (e.g., `MyComponent`, not `myComponent`), because React treats elements starting with lowercase letters as HTML tags and elements starting with uppercase letters as custom components. Component names should be descriptive and use PascalCase convention.
</details>

---

**5. What is the Virtual DOM, and why does React use it?**

<details>
<summary>Answer</summary>

The Virtual DOM is a lightweight, in-memory representation of the actual browser DOM. When state or props change in a React application, React creates a new Virtual DOM tree, compares it with the previous one using a process called "reconciliation" (or "diffing"), and calculates the minimal set of changes needed. Only those specific changes are then applied to the real DOM. React uses this approach because directly manipulating the browser DOM is slow and expensive. By batching and minimizing DOM updates, React achieves significantly better performance, especially in applications with frequent UI changes.
</details>

---

## Part 3: Coding Exercises

**Exercise 1: Create a Greeting Component**

Create a functional React component called `Greeting` that accepts a `name` prop and displays a greeting message. If no name is provided, it should display "Hello, Guest!".

<details>
<summary>Solution</summary>

```jsx
function Greeting({ name }) {
  return (
    <h1>Hello, {name || "Guest"}!</h1>
  );
}

// Usage
function App() {
  return (
    <div>
      <Greeting name="Alice" />
      <Greeting />
    </div>
  );
}

export default App;
```

**Output:**
- `Hello, Alice!`
- `Hello, Guest!`
</details>

---

**Exercise 2: Build a Profile Card**

Create a `ProfileCard` component that displays a user's name, email, and bio. Use proper JSX syntax with `className` for styling. The component should render a structured card layout.

<details>
<summary>Solution</summary>

```jsx
function ProfileCard({ name, email, bio }) {
  return (
    <div className="profile-card">
      <h2 className="profile-name">{name}</h2>
      <p className="profile-email">{email}</p>
      <p className="profile-bio">{bio}</p>
    </div>
  );
}

function App() {
  return (
    <div className="app">
      <ProfileCard
        name="Jane Doe"
        email="jane@example.com"
        bio="Full-stack developer who loves building web applications."
      />
      <ProfileCard
        name="John Smith"
        email="john@example.com"
        bio="UI/UX designer passionate about creating beautiful interfaces."
      />
    </div>
  );
}

export default App;
```
</details>

---

**Exercise 3: Render a List of Items with `.map()`**

Create a `FruitList` component that receives an array of fruit objects (each with `id` and `name`) and renders them as an unordered list. Use `.map()` with proper `key` props.

<details>
<summary>Solution</summary>

```jsx
function FruitList({ fruits }) {
  return (
    <ul>
      {fruits.map((fruit) => (
        <li key={fruit.id}>{fruit.name}</li>
      ))}
    </ul>
  );
}

function App() {
  const fruits = [
    { id: 1, name: "Apple" },
    { id: 2, name: "Banana" },
    { id: 3, name: "Cherry" },
    { id: 4, name: "Dragonfruit" },
    { id: 5, name: "Elderberry" },
  ];

  return (
    <div>
      <h1>Fruit List</h1>
      <FruitList fruits={fruits} />
    </div>
  );
}

export default App;
```

**Key Points:**
- Each `<li>` has a unique `key` prop using `fruit.id`.
- The `key` prop helps React efficiently update the list when items change.
- Using the array index as a key is discouraged when the list can be reordered.
</details>

---

**Exercise 4: Conditional Rendering Based on a Variable**

Create a `Dashboard` component that shows different content based on an `isLoggedIn` variable. If the user is logged in, display a welcome message and a logout button. If not, display a login prompt.

<details>
<summary>Solution</summary>

```jsx
function Dashboard({ isLoggedIn, username }) {
  return (
    <div className="dashboard">
      <h1>Dashboard</h1>

      {isLoggedIn ? (
        <div>
          <p>Welcome back, {username}!</p>
          <button>Logout</button>
        </div>
      ) : (
        <div>
          <p>Please log in to access your dashboard.</p>
          <button>Login</button>
        </div>
      )}

      {isLoggedIn && (
        <div className="dashboard-content">
          <h2>Your Recent Activity</h2>
          <p>Here is a summary of your recent activity...</p>
        </div>
      )}
    </div>
  );
}

function App() {
  return (
    <div>
      <Dashboard isLoggedIn={true} username="Alice" />
      <hr />
      <Dashboard isLoggedIn={false} />
    </div>
  );
}

export default App;
```

**Key Points:**
- The ternary operator (`? :`) is used for if/else rendering.
- The logical AND operator (`&&`) is used to render content only when a condition is true.
- Both patterns are standard approaches to conditional rendering in React.
</details>

---

**Exercise 5: Build a Complete Page with Header, Main, and Footer Components**

Create three separate components (`Header`, `Main`, `Footer`) and compose them together in an `App` component to build a complete webpage layout.

<details>
<summary>Solution</summary>

```jsx
function Header() {
  const navItems = ["Home", "About", "Services", "Contact"];

  return (
    <header className="header">
      <h1 className="logo">MyWebsite</h1>
      <nav>
        <ul className="nav-list">
          {navItems.map((item) => (
            <li key={item}>
              <a href={`#${item.toLowerCase()}`}>{item}</a>
            </li>
          ))}
        </ul>
      </nav>
    </header>
  );
}

function Main() {
  return (
    <main className="main-content">
      <section className="hero">
        <h2>Welcome to Our Website</h2>
        <p>We build modern web applications with React.</p>
      </section>

      <section className="features">
        <h3>Our Features</h3>
        <div className="feature-grid">
          <div className="feature-card">
            <h4>Fast</h4>
            <p>Optimized for performance and speed.</p>
          </div>
          <div className="feature-card">
            <h4>Responsive</h4>
            <p>Works on all devices and screen sizes.</p>
          </div>
          <div className="feature-card">
            <h4>Modern</h4>
            <p>Built with the latest web technologies.</p>
          </div>
        </div>
      </section>
    </main>
  );
}

function Footer() {
  const currentYear = new Date().getFullYear();

  return (
    <footer className="footer">
      <p>&copy; {currentYear} MyWebsite. All rights reserved.</p>
      <div className="footer-links">
        <a href="#privacy">Privacy Policy</a>
        <a href="#terms">Terms of Service</a>
      </div>
    </footer>
  );
}

function App() {
  return (
    <div className="app">
      <Header />
      <Main />
      <Footer />
    </div>
  );
}

export default App;
```

**Key Points:**
- Each section of the page is a separate, reusable component.
- Components are composed together in `App` to form the complete page.
- JavaScript expressions (like `new Date().getFullYear()`) can be used inside JSX.
- The `.map()` method is used to dynamically render navigation items.
</details>
