# Week 21 -- React Advanced Patterns & Project: Practice Questions

**Total Questions: 30** (10 MCQs + 5 Short Answer + 5 Coding Exercises + 10 React Phase Comprehensive Review)

---

## Part 1: Multiple Choice Questions (MCQs)

**1. What problem does React Context solve?**

- A) It replaces the need for components entirely
- B) It eliminates prop drilling by providing data directly to any component in the tree
- C) It makes API calls faster
- D) It replaces React Router for navigation

<details>
<summary>Answer</summary>

**B) It eliminates prop drilling by providing data directly to any component in the tree**

Prop drilling occurs when you pass props through multiple intermediate components that do not use the data themselves, just to get it to a deeply nested component. Context creates a "broadcast channel" where a Provider makes data available, and any component anywhere in the tree can consume it directly using `useContext`, regardless of how deep it is. The intermediate components never need to know about the data.
</details>

---

**2. What are the three steps to use React Context?**

- A) Import, Export, Render
- B) Create with `createContext()`, Provide with `<Context.Provider>`, Consume with `useContext()`
- C) Define, Dispatch, Subscribe
- D) Initialize, Mutate, Observe

<details>
<summary>Answer</summary>

**B) Create with `createContext()`, Provide with `<Context.Provider>`, Consume with `useContext()`**

1. **Create:** `const MyContext = createContext(defaultValue)` creates a context object.
2. **Provide:** `<MyContext.Provider value={data}>` wraps the part of the tree that needs access to the data and supplies the value.
3. **Consume:** `const data = useContext(MyContext)` inside any component reads the current value from the nearest Provider above it in the tree.
</details>

---

**3. What happens when a Context Provider's value changes?**

- A) Nothing; context values are immutable
- B) Only the Provider component re-renders
- C) All components that consume that context re-render with the new value
- D) The entire application restarts

<details>
<summary>Answer</summary>

**C) All components that consume that context re-render with the new value**

When the `value` prop of a Provider changes, React re-renders every component that consumes that context via `useContext()`. This happens regardless of whether the component is wrapped in `React.memo` -- context changes always trigger a re-render in consumers. This is why it is important to keep context values stable and avoid putting rapidly changing data into context.
</details>

---

**4. What is the naming requirement for custom hooks?**

- A) They must end with `Hook` (e.g., `fetchHook`)
- B) They must start with `use` (e.g., `useFetch`)
- C) They must be written in uppercase (e.g., `FETCH`)
- D) There is no naming requirement

<details>
<summary>Answer</summary>

**B) They must start with `use` (e.g., `useFetch`)**

This is not just a convention -- it is a rule enforced by React's linter (eslint-plugin-react-hooks). React uses the `use` prefix to identify hooks and enforce the Rules of Hooks: hooks must be called at the top level, never inside conditions, loops, or nested functions. If a function starts with `use`, React treats it as a hook and applies these rules. Without the prefix, React cannot distinguish hooks from regular functions.
</details>

---

**5. When two components use the same custom hook, do they share state?**

```jsx
function ComponentA() {
  const { data } = useFetch("/api/users");
  return <p>{data?.length} users</p>;
}

function ComponentB() {
  const { data } = useFetch("/api/posts");
  return <p>{data?.length} posts</p>;
}
```

- A) Yes, they share the same state
- B) No, each call gets its own independent state
- C) Only if they use the same URL
- D) Only if they are siblings in the component tree

<details>
<summary>Answer</summary>

**B) No, each call gets its own independent state**

Custom hooks share **logic**, not **state**. Each call to a custom hook creates its own independent instances of `useState`, `useEffect`, and any other hooks used inside it. `ComponentA` and `ComponentB` each have their own `data`, `loading`, and `error` state, even though they both use `useFetch`. This is the same as how two components using `useState(0)` each have their own independent counter.
</details>

---

**6. What does `React.memo` do?**

- A) It memorizes the component code for faster initial loading
- B) It prevents a component from ever re-rendering
- C) It skips re-rendering a component if its props have not changed
- D) It caches API responses inside the component

<details>
<summary>Answer</summary>

**C) It skips re-rendering a component if its props have not changed**

`React.memo` is a higher-order component that wraps a component and performs a shallow comparison of its props between renders. If all props are the same (by reference for objects/functions, by value for primitives), React reuses the previously rendered output and skips calling the component function. It does not prevent re-renders from internal state changes or context changes -- only from parent re-renders where props are unchanged.
</details>

---

**7. When should you use `useMemo`?**

- A) For every calculation in every component
- B) Only when a computation is genuinely expensive and its dependencies change infrequently
- C) Whenever you want to prevent any re-renders
- D) Only inside class components

<details>
<summary>Answer</summary>

**B) Only when a computation is genuinely expensive and its dependencies change infrequently**

`useMemo` caches the result of a computation and only recalculates it when its dependencies change. It is useful for expensive operations like sorting large arrays, complex mathematical calculations, or generating derived data from large datasets. Using it for trivial calculations (adding two numbers, simple string concatenation) actually makes performance worse because the memoization overhead (storing the value, comparing dependencies) exceeds the cost of just recalculating.
</details>

---

**8. Why is `useCallback` typically used together with `React.memo`?**

- A) `useCallback` only works inside memoized components
- B) Without `React.memo` on the child, caching the function reference has no effect because the child re-renders anyway
- C) `React.memo` requires `useCallback` to function
- D) `useCallback` automatically applies `React.memo` to children

<details>
<summary>Answer</summary>

**B) Without `React.memo` on the child, caching the function reference has no effect because the child re-renders anyway**

When a parent re-renders, all its children re-render by default. `useCallback` preserves the same function reference across renders, but if the child does not check whether its props changed (which is what `React.memo` does), the child re-renders regardless of the function reference. The combination works like this: `React.memo` on the child says "skip re-render if props are the same," and `useCallback` in the parent ensures the function prop IS the same. Without `React.memo`, there is no prop comparison, so `useCallback` is pointless.
</details>

---

**9. What is the biggest mistake developers make with React performance optimization?**

- A) Not using enough `useMemo` and `useCallback`
- B) Using TypeScript instead of JavaScript
- C) Optimizing prematurely before measuring an actual performance problem
- D) Using too many components

<details>
<summary>Answer</summary>

**C) Optimizing prematurely before measuring an actual performance problem**

Premature optimization adds complexity (more dependencies to track, wrapper components, harder debugging) without measurable benefit. React's default rendering is fast enough for the vast majority of applications. The correct approach is to build your application first, then measure performance using React DevTools Profiler or Chrome's Performance tab. Only when you identify a specific bottleneck should you apply `React.memo`, `useMemo`, or `useCallback` to that specific component. Wrapping everything in memoization can actually make performance worse due to the comparison overhead.
</details>

---

**10. What does prop drilling look like, and which React feature solves it?**

```jsx
<App user={user}>
  <Layout user={user}>
    <Sidebar user={user}>
      <UserAvatar user={user} />
    </Sidebar>
  </Layout>
</App>
```

- A) This is proper React architecture; no changes needed
- B) This is prop drilling; solved by React Context (`useContext`)
- C) This is prop drilling; solved by `useRef`
- D) This is prop drilling; solved by `React.memo`

<details>
<summary>Answer</summary>

**B) This is prop drilling; solved by React Context (`useContext`)**

In this example, `user` is passed through `Layout` and `Sidebar` even though they do not use it -- they merely forward it to their children. This is prop drilling. With Context, you would create a `UserContext`, wrap the tree in `<UserContext.Provider value={user}>`, and have `UserAvatar` call `useContext(UserContext)` to access the user directly. `Layout` and `Sidebar` would no longer need the `user` prop at all.
</details>

---

## Part 2: Short Answer Questions

**1. Explain the difference between passing state through props, lifting state up, and using Context. When is each approach appropriate?**

<details>
<summary>Answer</summary>

**Passing state through props** is the most basic approach. A parent component holds state and passes it to a child via props. This is appropriate when data flows in one direction (parent to child) and only travels one or two levels deep. It is explicit, easy to trace, and should be the default choice.

**Lifting state up** is used when two sibling components need to share or synchronize state. Since siblings cannot pass data directly to each other, you move the shared state to their nearest common parent. The parent holds the state and passes it down to both children as props, along with a setter function so children can update it. This is appropriate when a small number of closely related components need to share data.

**Context** is used when data needs to be accessible by many components at various depths in the component tree. Instead of passing props through intermediaries (prop drilling), you create a Context Provider that broadcasts data, and any consumer component can read it directly. This is appropriate for truly global data like the current user, theme, language, or authentication status.

The general guideline is: start with props. If you need siblings to share, lift state up. If data must travel through many layers or be available app-wide, use Context.
</details>

---

**2. Explain the purpose of the custom hook pattern. Why would you create a `useFetch` hook instead of writing fetch logic directly in each component?**

<details>
<summary>Answer</summary>

The custom hook pattern allows you to extract and reuse **stateful logic** across multiple components. When multiple components need the same combination of hooks (e.g., `useState` for data/loading/error + `useEffect` for fetching), duplicating that code in every component violates the DRY (Don't Repeat Yourself) principle.

A `useFetch` hook encapsulates the entire data-fetching pattern -- declaring state variables, making the fetch call, handling loading and error states, and running cleanup -- into a single reusable function. Benefits include:

1. **Code reuse:** Write the fetch logic once, use it in dozens of components.
2. **Consistency:** Every component that fetches data handles loading, errors, and success the same way.
3. **Maintainability:** If you need to change the fetching pattern (add caching, retry logic, abort controllers), you change it in one place.
4. **Testability:** You can test the hook independently of any component.
5. **Readability:** Components become simpler because the "how" of data fetching is abstracted away. The component just says `const { data, loading, error } = useFetch(url)` and focuses on rendering.

Importantly, each component that calls `useFetch` gets its own independent state. The hook shares logic, not state.
</details>

---

**3. What is the difference between `useMemo` and `useCallback`? Provide a one-sentence description and a use case for each.**

<details>
<summary>Answer</summary>

**`useMemo`** caches the **result of a computation** and only recalculates when its dependencies change. Use it when you have an expensive calculation (like sorting a large array) that should not re-run on every render.

```jsx
const sortedItems = useMemo(() => items.sort(compareFn), [items]);
// Caches the sorted array. Only re-sorts when `items` changes.
```

**`useCallback`** caches the **function itself** (its reference) and only creates a new function when its dependencies change. Use it when you pass a callback to a `React.memo`-wrapped child component to prevent unnecessary re-renders.

```jsx
const handleClick = useCallback(() => setCount(c => c + 1), []);
// Caches the function reference. Same reference across renders.
```

The key distinction: `useMemo` returns a **value** (the result of calling the function), while `useCallback` returns a **function** (the function itself, without calling it). In fact, `useCallback(fn, deps)` is equivalent to `useMemo(() => fn, deps)`.
</details>

---

**4. Why does `React.memo` not protect against re-renders caused by Context changes? What can you do about it?**

<details>
<summary>Answer</summary>

`React.memo` performs a shallow comparison of **props** to decide whether to skip a re-render. However, when a component consumes a context value via `useContext()`, context changes bypass the prop comparison entirely. React treats context updates as a direct trigger for re-rendering all consumers, regardless of `React.memo`.

This happens because the context value is not a prop -- it is a separate subscription that React manages internally. When the Provider's `value` changes, React notifies all consumers and forces them to re-render.

To mitigate unnecessary context re-renders:

1. **Split contexts:** Instead of putting all global state in one massive context, split it into focused contexts (ThemeContext, AuthContext, CartContext). A component that only cares about the theme will not re-render when auth changes.

2. **Memoize the context value:** If the Provider re-renders frequently, use `useMemo` to stabilize the context value object so that consumers only re-render when the actual data changes, not when the parent re-renders.

```jsx
const value = useMemo(() => ({ theme, toggleTheme }), [theme]);
return <ThemeContext.Provider value={value}>{children}</ThemeContext.Provider>;
```

3. **Extract consuming components:** Move the `useContext` call into a small wrapper component, and memoize the rest of the UI separately.
</details>

---

**5. Describe three rules you must follow when creating and using custom hooks.**

<details>
<summary>Answer</summary>

**Rule 1: The name must start with `use`.** This is mandatory, not optional. React's linter uses the `use` prefix to identify hooks and enforce the Rules of Hooks. A function named `fetchData` will not be recognized as a hook and its internal hook calls (`useState`, `useEffect`) will not be properly validated. Valid names include `useFetch`, `useLocalStorage`, `useToggle`, `useAuth`.

**Rule 2: Hooks must be called at the top level.** Custom hooks (like all hooks) cannot be called inside conditions, loops, or nested functions. React relies on the order of hook calls being identical on every render. If a hook is inside an `if` statement, it might be called on some renders but not others, which breaks React's internal bookkeeping.

```jsx
// WRONG
if (shouldFetch) {
  const data = useFetch(url);  // Breaks the Rules of Hooks
}

// CORRECT
const data = useFetch(shouldFetch ? url : null);  // Always called
```

**Rule 3: Custom hooks can only be called from React function components or from other custom hooks.** You cannot call `useFetch` inside a plain JavaScript function, a class method, an event handler, or a callback. Custom hooks must be called during the render phase of a component or another hook, so React can properly track their state.
</details>

---

## Part 3: Coding Exercises

**Exercise 1: Theme Toggle with Context**

Build a theme toggle system using React Context. The theme should switch between "light" and "dark" modes, and the theme should affect the entire application's appearance.

Requirements:
- Create a `ThemeContext` with `createContext`
- Create a `ThemeProvider` component that manages the theme state and provides a `toggleTheme` function
- Create a custom `useTheme` hook for consuming the context
- Build a `ThemeToggle` button component that uses the context
- Build a `Card` component that changes its styling based on the theme

<details>
<summary>Solution</summary>

```jsx
// src/context/ThemeContext.jsx
import { createContext, useState, useContext } from "react";

const ThemeContext = createContext();

function ThemeProvider({ children }) {
  const [theme, setTheme] = useState("light");

  function toggleTheme() {
    setTheme((prev) => (prev === "light" ? "dark" : "light"));
  }

  return (
    <ThemeContext.Provider value={{ theme, toggleTheme }}>
      {children}
    </ThemeContext.Provider>
  );
}

function useTheme() {
  const context = useContext(ThemeContext);
  if (context === undefined) {
    throw new Error("useTheme must be used within a ThemeProvider");
  }
  return context;
}

export { ThemeProvider, useTheme };
```

```jsx
// src/components/ThemeToggle.jsx
import { useTheme } from "../context/ThemeContext";

function ThemeToggle() {
  const { theme, toggleTheme } = useTheme();

  return (
    <button
      onClick={toggleTheme}
      style={{
        padding: "10px 20px",
        borderRadius: "8px",
        border: "none",
        cursor: "pointer",
        backgroundColor: theme === "dark" ? "#fbbf24" : "#1f2937",
        color: theme === "dark" ? "#1f2937" : "#ffffff",
        fontSize: "1rem",
      }}
    >
      Switch to {theme === "light" ? "Dark" : "Light"} Mode
    </button>
  );
}

export default ThemeToggle;
```

```jsx
// src/components/Card.jsx
import { useTheme } from "../context/ThemeContext";

function Card({ title, description }) {
  const { theme } = useTheme();

  const styles = {
    padding: "24px",
    margin: "16px 0",
    borderRadius: "12px",
    backgroundColor: theme === "dark" ? "#1f2937" : "#ffffff",
    color: theme === "dark" ? "#f3f4f6" : "#111827",
    border: `1px solid ${theme === "dark" ? "#374151" : "#e5e7eb"}`,
    boxShadow: theme === "dark"
      ? "0 4px 6px rgba(0, 0, 0, 0.3)"
      : "0 4px 6px rgba(0, 0, 0, 0.1)",
    transition: "all 0.3s ease",
  };

  return (
    <div style={styles}>
      <h2>{title}</h2>
      <p>{description}</p>
    </div>
  );
}

export default Card;
```

```jsx
// src/App.jsx
import { useTheme } from "./context/ThemeContext";
import ThemeToggle from "./components/ThemeToggle";
import Card from "./components/Card";

function App() {
  const { theme } = useTheme();

  return (
    <div style={{
      minHeight: "100vh",
      padding: "32px",
      backgroundColor: theme === "dark" ? "#111827" : "#f9fafb",
      color: theme === "dark" ? "#f9fafb" : "#111827",
      transition: "all 0.3s ease",
    }}>
      <h1>Theme Context Demo</h1>
      <ThemeToggle />
      <Card title="First Card" description="This card changes with the theme." />
      <Card title="Second Card" description="All cards respond to the same context." />
      <Card title="Third Card" description="No prop drilling needed!" />
    </div>
  );
}

export default App;
```

```jsx
// src/main.jsx
import React from "react";
import ReactDOM from "react-dom/client";
import { ThemeProvider } from "./context/ThemeContext";
import App from "./App";

ReactDOM.createRoot(document.getElementById("root")).render(
  <React.StrictMode>
    <ThemeProvider>
      <App />
    </ThemeProvider>
  </React.StrictMode>
);
```

**Key points:**
- `ThemeProvider` holds the `theme` state and the `toggleTheme` function.
- `useTheme` is a custom convenience hook that calls `useContext(ThemeContext)` and includes an error check.
- `ThemeToggle` reads and modifies the theme without any props being passed through intermediate components.
- `Card` reads the theme for styling without receiving it as a prop.
</details>

---

**Exercise 2: useFetch Custom Hook**

Create a reusable `useFetch` hook that handles data fetching, loading state, and error handling. Use it in two different components.

Requirements:
- The hook should accept a URL and return `{ data, loading, error }`
- It should handle loading state, success, and errors
- Build two components that use the same hook to fetch different data
- Use `https://jsonplaceholder.typicode.com/users` and `https://jsonplaceholder.typicode.com/todos?_limit=10`

<details>
<summary>Solution</summary>

```jsx
// src/hooks/useFetch.js
import { useState, useEffect } from "react";

function useFetch(url) {
  const [data, setData] = useState(null);
  const [loading, setLoading] = useState(true);
  const [error, setError] = useState(null);

  useEffect(() => {
    // Reset states when URL changes
    setData(null);
    setLoading(true);
    setError(null);

    // Create an abort controller for cleanup
    const controller = new AbortController();

    async function fetchData() {
      try {
        const response = await fetch(url, { signal: controller.signal });

        if (!response.ok) {
          throw new Error(`HTTP error! Status: ${response.status}`);
        }

        const result = await response.json();
        setData(result);
      } catch (err) {
        // Do not set error if the fetch was aborted (cleanup)
        if (err.name !== "AbortError") {
          setError(err.message);
        }
      } finally {
        setLoading(false);
      }
    }

    fetchData();

    // Cleanup: abort the fetch if the component unmounts
    // or if the URL changes before the fetch completes
    return () => controller.abort();
  }, [url]);

  return { data, loading, error };
}

export default useFetch;
```

```jsx
// src/components/UserList.jsx
import useFetch from "../hooks/useFetch";

function UserList() {
  const { data: users, loading, error } = useFetch(
    "https://jsonplaceholder.typicode.com/users"
  );

  if (loading) return <p>Loading users...</p>;
  if (error) return <p style={{ color: "red" }}>Error: {error}</p>;

  return (
    <div>
      <h2>Users ({users.length})</h2>
      <ul>
        {users.map((user) => (
          <li key={user.id}>
            <strong>{user.name}</strong> -- {user.email}
          </li>
        ))}
      </ul>
    </div>
  );
}

export default UserList;
```

```jsx
// src/components/TodoList.jsx
import useFetch from "../hooks/useFetch";

function TodoList() {
  const { data: todos, loading, error } = useFetch(
    "https://jsonplaceholder.typicode.com/todos?_limit=10"
  );

  if (loading) return <p>Loading todos...</p>;
  if (error) return <p style={{ color: "red" }}>Error: {error}</p>;

  return (
    <div>
      <h2>Todos ({todos.length})</h2>
      <ul>
        {todos.map((todo) => (
          <li key={todo.id} style={{ textDecoration: todo.completed ? "line-through" : "none" }}>
            {todo.title}
          </li>
        ))}
      </ul>
    </div>
  );
}

export default TodoList;
```

```jsx
// src/App.jsx
import UserList from "./components/UserList";
import TodoList from "./components/TodoList";

function App() {
  return (
    <div style={{ padding: "20px" }}>
      <h1>useFetch Custom Hook Demo</h1>
      <UserList />
      <hr />
      <TodoList />
    </div>
  );
}

export default App;
```

**Key points:**
- The `useFetch` hook encapsulates all fetch logic: state initialization, the async fetch call, error handling, and cleanup.
- `AbortController` is used for cleanup, canceling in-flight requests if the component unmounts or the URL changes.
- `UserList` and `TodoList` each call `useFetch` with different URLs and get their own independent state.
- The components are clean and focused on rendering, with no fetch boilerplate.
</details>

---

**Exercise 3: useLocalStorage Custom Hook**

Create a `useLocalStorage` hook that works exactly like `useState` but persists the value in the browser's `localStorage`.

Requirements:
- Accept a key and initial value
- Return `[storedValue, setValue]` like `useState`
- Read from `localStorage` on initialization
- Write to `localStorage` on every update
- Build a settings component that uses it for name and font size

<details>
<summary>Solution</summary>

```jsx
// src/hooks/useLocalStorage.js
import { useState } from "react";

function useLocalStorage(key, initialValue) {
  const [storedValue, setStoredValue] = useState(() => {
    try {
      const item = localStorage.getItem(key);
      return item !== null ? JSON.parse(item) : initialValue;
    } catch (error) {
      console.error(`Error reading localStorage key "${key}":`, error);
      return initialValue;
    }
  });

  function setValue(value) {
    try {
      const valueToStore = value instanceof Function ? value(storedValue) : value;
      setStoredValue(valueToStore);
      localStorage.setItem(key, JSON.stringify(valueToStore));
    } catch (error) {
      console.error(`Error writing localStorage key "${key}":`, error);
    }
  }

  return [storedValue, setValue];
}

export default useLocalStorage;
```

```jsx
// src/components/UserSettings.jsx
import useLocalStorage from "../hooks/useLocalStorage";

function UserSettings() {
  const [name, setName] = useLocalStorage("settings-name", "");
  const [fontSize, setFontSize] = useLocalStorage("settings-fontSize", 16);
  const [darkMode, setDarkMode] = useLocalStorage("settings-darkMode", false);

  return (
    <div style={{
      padding: "24px",
      fontSize: `${fontSize}px`,
      backgroundColor: darkMode ? "#1f2937" : "#ffffff",
      color: darkMode ? "#f9fafb" : "#111827",
      minHeight: "100vh",
      transition: "all 0.3s",
    }}>
      <h1>User Settings</h1>
      <p style={{ color: darkMode ? "#9ca3af" : "#6b7280" }}>
        All settings persist in localStorage. Refresh the page to verify!
      </p>

      <div style={{ marginBottom: "20px" }}>
        <label><strong>Name: </strong></label>
        <input
          value={name}
          onChange={(e) => setName(e.target.value)}
          placeholder="Enter your name"
          style={{ padding: "8px", fontSize: "inherit" }}
        />
      </div>

      <div style={{ marginBottom: "20px" }}>
        <label><strong>Font Size: {fontSize}px </strong></label>
        <input
          type="range"
          min="12"
          max="28"
          value={fontSize}
          onChange={(e) => setFontSize(Number(e.target.value))}
        />
      </div>

      <div style={{ marginBottom: "20px" }}>
        <label>
          <input
            type="checkbox"
            checked={darkMode}
            onChange={(e) => setDarkMode(e.target.checked)}
          />
          <strong> Dark Mode</strong>
        </label>
      </div>

      <div style={{
        padding: "16px",
        borderRadius: "8px",
        backgroundColor: darkMode ? "#374151" : "#f3f4f6",
        marginTop: "20px",
      }}>
        <h3>Preview</h3>
        <p>Hello, {name || "Guest"}!</p>
        <p>This text is {fontSize}px in {darkMode ? "dark" : "light"} mode.</p>
      </div>
    </div>
  );
}

export default UserSettings;
```

```jsx
// src/App.jsx
import UserSettings from "./components/UserSettings";

function App() {
  return <UserSettings />;
}

export default App;
```

**Key points:**
- `useLocalStorage` uses lazy initialization (`useState(() => ...)`) to read from `localStorage` only once.
- The `setValue` function supports both direct values and updater functions (`setValue(prev => prev + 1)`), matching `useState` behavior.
- `JSON.stringify` and `JSON.parse` handle serialization, so the hook works with strings, numbers, booleans, objects, and arrays.
- The `try/catch` blocks handle edge cases like localStorage being full or disabled in private browsing.
</details>

---

**Exercise 4: React.memo Optimization**

Demonstrate the difference between a memoized and non-memoized component. Create a parent that re-renders frequently, a child that is expensive to render, and show how `React.memo` with `useCallback` prevents unnecessary re-renders.

Requirements:
- Create a parent with a counter that increments (causing frequent re-renders)
- Create an "expensive" child component that logs when it renders
- First show the problem: the child re-renders on every parent render
- Then fix it with `React.memo` and `useCallback`

<details>
<summary>Solution</summary>

```jsx
// src/components/ExpensiveList.jsx
import React from "react";

// Without memo: this would re-render every time Parent re-renders
// With memo: only re-renders when items or onItemClick actually change
const ExpensiveList = React.memo(function ExpensiveList({ items, onItemClick }) {
  console.log("ExpensiveList rendered!"); // Watch the console

  return (
    <div style={{
      border: "2px solid #3b82f6",
      padding: "16px",
      borderRadius: "8px",
      marginTop: "16px",
    }}>
      <h3>Expensive List (check console for renders)</h3>
      <ul>
        {items.map((item, index) => (
          <li key={index}>
            <button onClick={() => onItemClick(item)}>{item}</button>
          </li>
        ))}
      </ul>
    </div>
  );
});

export default ExpensiveList;
```

```jsx
// src/App.jsx
import { useState, useCallback, useMemo } from "react";
import ExpensiveList from "./components/ExpensiveList";

function App() {
  const [count, setCount] = useState(0);
  const [selectedItem, setSelectedItem] = useState(null);

  // WITHOUT useMemo: a new array is created on every render.
  // React.memo sees a "new" prop and re-renders ExpensiveList.

  // WITH useMemo: the same array reference is reused.
  const items = useMemo(
    () => ["Apple", "Banana", "Cherry", "Date", "Elderberry"],
    [] // Empty deps: items never change
  );

  // WITHOUT useCallback: a new function is created on every render.
  // React.memo sees a "new" onItemClick prop and re-renders ExpensiveList.

  // WITH useCallback: the same function reference is reused.
  const handleItemClick = useCallback((item) => {
    setSelectedItem(item);
  }, []);

  return (
    <div style={{ padding: "20px" }}>
      <h1>React.memo + useCallback Demo</h1>

      <div style={{
        padding: "16px",
        backgroundColor: "#f3f4f6",
        borderRadius: "8px",
        marginBottom: "16px",
      }}>
        <p>Counter: {count}</p>
        <button onClick={() => setCount(count + 1)} style={{ padding: "8px 16px" }}>
          Increment Counter
        </button>
        <p style={{ color: "#6b7280", fontSize: "0.9rem" }}>
          Clicking this re-renders App, but ExpensiveList should NOT re-render.
          Check the console.
        </p>
      </div>

      {selectedItem && (
        <p style={{ color: "#16a34a" }}>Selected: {selectedItem}</p>
      )}

      <ExpensiveList items={items} onItemClick={handleItemClick} />
    </div>
  );
}

export default App;
```

**Key points:**
- `ExpensiveList` is wrapped in `React.memo`, so it only re-renders if its props change by reference.
- `useMemo` ensures the `items` array is the same reference across renders (otherwise a new array `["Apple", ...]` is created on each render).
- `useCallback` ensures `handleItemClick` is the same function reference across renders.
- Clicking "Increment Counter" re-renders `App` but does NOT re-render `ExpensiveList`, because its props (`items` and `onItemClick`) are stable references.
- Without `useMemo` and `useCallback`, `React.memo` would be useless because every render creates new props.
</details>

---

**Exercise 5: Complete React Phase Project -- Multi-Page Product Store**

Build a multi-page product store that combines all concepts from Weeks 16-21: components, props, state, effects, routing, context, and custom hooks.

Requirements:
- React Router with at least 4 pages (Home, Products, Product Detail, About)
- NavLink navigation with active styling
- Dynamic routes for product details using `useParams`
- Theme context for dark/light mode
- `useFetch` custom hook (or mock data with loading state)
- 404 page with catch-all route
- Clean component structure

<details>
<summary>Solution</summary>

```jsx
// src/context/ThemeContext.jsx
import { createContext, useState, useContext } from "react";

const ThemeContext = createContext();

function ThemeProvider({ children }) {
  const [theme, setTheme] = useState("light");
  const toggleTheme = () => setTheme((p) => (p === "light" ? "dark" : "light"));
  return (
    <ThemeContext.Provider value={{ theme, toggleTheme }}>
      {children}
    </ThemeContext.Provider>
  );
}

function useTheme() {
  const ctx = useContext(ThemeContext);
  if (!ctx) throw new Error("useTheme must be used within ThemeProvider");
  return ctx;
}

export { ThemeProvider, useTheme };
```

```jsx
// src/hooks/useFetch.js
import { useState, useEffect } from "react";

function useFetch(url) {
  const [data, setData] = useState(null);
  const [loading, setLoading] = useState(true);
  const [error, setError] = useState(null);

  useEffect(() => {
    setData(null);
    setLoading(true);
    setError(null);
    const controller = new AbortController();

    async function load() {
      try {
        const res = await fetch(url, { signal: controller.signal });
        if (!res.ok) throw new Error(`Status: ${res.status}`);
        const json = await res.json();
        setData(json);
      } catch (err) {
        if (err.name !== "AbortError") setError(err.message);
      } finally {
        setLoading(false);
      }
    }

    load();
    return () => controller.abort();
  }, [url]);

  return { data, loading, error };
}

export default useFetch;
```

```jsx
// src/data/products.js
const products = [
  { id: 1, name: "Wireless Earbuds", price: 59.99, category: "Audio",
    description: "True wireless earbuds with active noise cancellation, 8-hour battery life, and IPX5 water resistance." },
  { id: 2, name: "Mechanical Keyboard", price: 129.99, category: "Peripherals",
    description: "Full-size mechanical keyboard with Cherry MX Blue switches, RGB backlighting, and USB-C connection." },
  { id: 3, name: "Portable Charger", price: 34.99, category: "Accessories",
    description: "20000mAh portable charger with USB-C PD fast charging, dual output, and LED indicator." },
  { id: 4, name: "Webcam 4K", price: 89.99, category: "Video",
    description: "4K ultra-HD webcam with auto-focus, built-in ring light, and noise-cancelling microphone." },
  { id: 5, name: "Monitor Stand", price: 44.99, category: "Accessories",
    description: "Aluminum monitor riser with storage drawer, cable management, and non-slip feet." },
  { id: 6, name: "USB-C Hub", price: 49.99, category: "Peripherals",
    description: "7-in-1 USB-C hub with HDMI 4K, 3x USB-A, SD/microSD card reader, and 100W PD pass-through." },
];

export default products;
```

```jsx
// src/components/Navbar.jsx
import { NavLink } from "react-router-dom";
import { useTheme } from "../context/ThemeContext";

function Navbar() {
  const { theme, toggleTheme } = useTheme();

  const linkClass = ({ isActive }) =>
    `nav-link ${isActive ? "nav-link-active" : ""}`;

  const navStyle = {
    display: "flex",
    justifyContent: "space-between",
    alignItems: "center",
    padding: "14px 32px",
    backgroundColor: theme === "dark" ? "#1e293b" : "#ffffff",
    borderBottom: `1px solid ${theme === "dark" ? "#334155" : "#e5e7eb"}`,
  };

  return (
    <nav style={navStyle}>
      <div style={{ display: "flex", alignItems: "center", gap: "24px" }}>
        <span style={{
          fontWeight: "bold",
          fontSize: "1.3rem",
          color: theme === "dark" ? "#f1f5f9" : "#0f172a",
        }}>
          TechStore
        </span>
        <div style={{ display: "flex", gap: "4px" }}>
          <NavLink to="/" end className={linkClass}>Home</NavLink>
          <NavLink to="/products" className={linkClass}>Products</NavLink>
          <NavLink to="/about" className={linkClass}>About</NavLink>
        </div>
      </div>
      <button
        onClick={toggleTheme}
        style={{
          padding: "6px 14px",
          borderRadius: "6px",
          border: "1px solid",
          cursor: "pointer",
          backgroundColor: theme === "dark" ? "#334155" : "#f1f5f9",
          color: theme === "dark" ? "#f1f5f9" : "#0f172a",
          borderColor: theme === "dark" ? "#475569" : "#cbd5e1",
        }}
      >
        {theme === "light" ? "Dark" : "Light"} Mode
      </button>
    </nav>
  );
}

export default Navbar;
```

```jsx
// src/pages/Home.jsx
import { Link } from "react-router-dom";
import { useTheme } from "../context/ThemeContext";
import products from "../data/products";

function Home() {
  const { theme } = useTheme();
  const featured = products.slice(0, 3);

  return (
    <div>
      <div style={{
        textAlign: "center",
        padding: "60px 20px",
        backgroundColor: theme === "dark" ? "#1e293b" : "#eff6ff",
        borderRadius: "12px",
        marginBottom: "32px",
      }}>
        <h1 style={{ fontSize: "2.5rem", marginBottom: "12px" }}>Welcome to TechStore</h1>
        <p style={{ fontSize: "1.1rem", color: theme === "dark" ? "#94a3b8" : "#64748b" }}>
          Your one-stop shop for tech accessories
        </p>
        <Link
          to="/products"
          style={{
            display: "inline-block",
            marginTop: "20px",
            padding: "12px 28px",
            backgroundColor: "#3b82f6",
            color: "white",
            textDecoration: "none",
            borderRadius: "8px",
            fontWeight: "600",
          }}
        >
          Browse Products
        </Link>
      </div>

      <h2>Featured Products</h2>
      <div style={{ display: "grid", gridTemplateColumns: "repeat(auto-fill, minmax(250px, 1fr))", gap: "16px" }}>
        {featured.map((product) => (
          <div key={product.id} style={{
            padding: "20px",
            borderRadius: "10px",
            backgroundColor: theme === "dark" ? "#1e293b" : "#ffffff",
            border: `1px solid ${theme === "dark" ? "#334155" : "#e2e8f0"}`,
          }}>
            <h3>{product.name}</h3>
            <p style={{ color: "#3b82f6", fontWeight: "bold" }}>${product.price}</p>
            <Link to={`/products/${product.id}`} style={{ color: "#3b82f6" }}>
              View Details
            </Link>
          </div>
        ))}
      </div>
    </div>
  );
}

export default Home;
```

```jsx
// src/pages/ProductList.jsx
import { useState } from "react";
import { Link } from "react-router-dom";
import { useTheme } from "../context/ThemeContext";
import products from "../data/products";

function ProductList() {
  const { theme } = useTheme();
  const [search, setSearch] = useState("");

  const filtered = products.filter((p) =>
    p.name.toLowerCase().includes(search.toLowerCase())
  );

  return (
    <div>
      <h1>All Products</h1>
      <input
        value={search}
        onChange={(e) => setSearch(e.target.value)}
        placeholder="Search products..."
        style={{
          width: "100%",
          maxWidth: "400px",
          padding: "10px 16px",
          borderRadius: "8px",
          border: `1px solid ${theme === "dark" ? "#475569" : "#cbd5e1"}`,
          backgroundColor: theme === "dark" ? "#1e293b" : "#ffffff",
          color: theme === "dark" ? "#f1f5f9" : "#0f172a",
          marginBottom: "24px",
          fontSize: "1rem",
        }}
      />

      {filtered.length === 0 ? (
        <p>No products match "{search}".</p>
      ) : (
        <div style={{ display: "grid", gridTemplateColumns: "repeat(auto-fill, minmax(280px, 1fr))", gap: "20px" }}>
          {filtered.map((product) => (
            <div key={product.id} style={{
              padding: "20px",
              borderRadius: "10px",
              backgroundColor: theme === "dark" ? "#1e293b" : "#ffffff",
              border: `1px solid ${theme === "dark" ? "#334155" : "#e2e8f0"}`,
            }}>
              <span style={{
                fontSize: "0.8rem",
                backgroundColor: theme === "dark" ? "#334155" : "#e2e8f0",
                padding: "2px 8px",
                borderRadius: "4px",
              }}>
                {product.category}
              </span>
              <h3 style={{ marginTop: "12px" }}>{product.name}</h3>
              <p style={{ color: "#3b82f6", fontSize: "1.2rem", fontWeight: "bold" }}>
                ${product.price}
              </p>
              <p style={{ color: theme === "dark" ? "#94a3b8" : "#64748b", fontSize: "0.9rem" }}>
                {product.description.substring(0, 80)}...
              </p>
              <Link
                to={`/products/${product.id}`}
                style={{
                  display: "inline-block",
                  marginTop: "12px",
                  padding: "8px 16px",
                  backgroundColor: "#3b82f6",
                  color: "white",
                  textDecoration: "none",
                  borderRadius: "6px",
                  fontSize: "0.9rem",
                }}
              >
                View Details
              </Link>
            </div>
          ))}
        </div>
      )}
    </div>
  );
}

export default ProductList;
```

```jsx
// src/pages/ProductDetail.jsx
import { useParams, Link, useNavigate } from "react-router-dom";
import { useTheme } from "../context/ThemeContext";
import products from "../data/products";

function ProductDetail() {
  const { productId } = useParams();
  const { theme } = useTheme();
  const navigate = useNavigate();
  const product = products.find((p) => p.id === Number(productId));

  if (!product) {
    return (
      <div style={{ textAlign: "center", padding: "60px 20px" }}>
        <h1>Product Not Found</h1>
        <p>No product with ID "{productId}" exists.</p>
        <Link to="/products" style={{ color: "#3b82f6" }}>Back to Products</Link>
      </div>
    );
  }

  return (
    <div>
      <button
        onClick={() => navigate(-1)}
        style={{
          background: "none",
          border: "none",
          color: "#3b82f6",
          cursor: "pointer",
          fontSize: "1rem",
          marginBottom: "20px",
        }}
      >
        &larr; Back
      </button>

      <div style={{
        padding: "32px",
        borderRadius: "12px",
        backgroundColor: theme === "dark" ? "#1e293b" : "#ffffff",
        border: `1px solid ${theme === "dark" ? "#334155" : "#e2e8f0"}`,
      }}>
        <span style={{
          fontSize: "0.85rem",
          backgroundColor: theme === "dark" ? "#334155" : "#e2e8f0",
          padding: "4px 12px",
          borderRadius: "4px",
        }}>
          {product.category}
        </span>
        <h1 style={{ marginTop: "16px" }}>{product.name}</h1>
        <p style={{ color: "#3b82f6", fontSize: "2rem", fontWeight: "bold" }}>
          ${product.price}
        </p>
        <p style={{ lineHeight: "1.7", color: theme === "dark" ? "#cbd5e1" : "#475569" }}>
          {product.description}
        </p>
        <button style={{
          marginTop: "20px",
          padding: "12px 32px",
          backgroundColor: "#3b82f6",
          color: "white",
          border: "none",
          borderRadius: "8px",
          fontSize: "1rem",
          cursor: "pointer",
        }}>
          Add to Cart
        </button>
      </div>
    </div>
  );
}

export default ProductDetail;
```

```jsx
// src/pages/About.jsx
import { useTheme } from "../context/ThemeContext";

function About() {
  const { theme } = useTheme();

  return (
    <div style={{ maxWidth: "600px" }}>
      <h1>About TechStore</h1>
      <p style={{ lineHeight: "1.8", color: theme === "dark" ? "#cbd5e1" : "#475569" }}>
        TechStore is a demo e-commerce application built with React to demonstrate
        components, props, state management, side effects, routing, context, and
        custom hooks -- everything covered in Weeks 16 through 21 of our web
        development course.
      </p>
      <h2>Technologies Used</h2>
      <ul style={{ lineHeight: "2" }}>
        <li>React (Components, Hooks)</li>
        <li>React Router (Navigation, Dynamic Routes)</li>
        <li>Context API (Theme Management)</li>
        <li>Custom Hooks (useFetch, useLocalStorage)</li>
      </ul>
    </div>
  );
}

export default About;
```

```jsx
// src/pages/NotFound.jsx
import { Link } from "react-router-dom";

function NotFound() {
  return (
    <div style={{ textAlign: "center", padding: "80px 20px" }}>
      <h1 style={{ fontSize: "6rem", margin: 0, color: "#e5e7eb" }}>404</h1>
      <h2>Page Not Found</h2>
      <p style={{ color: "#6b7280" }}>The page you are looking for does not exist.</p>
      <Link to="/" style={{
        display: "inline-block",
        marginTop: "16px",
        padding: "12px 24px",
        backgroundColor: "#3b82f6",
        color: "white",
        textDecoration: "none",
        borderRadius: "8px",
      }}>
        Go Home
      </Link>
    </div>
  );
}

export default NotFound;
```

```jsx
// src/App.jsx
import { Routes, Route } from "react-router-dom";
import { useTheme } from "./context/ThemeContext";
import Navbar from "./components/Navbar";
import Home from "./pages/Home";
import ProductList from "./pages/ProductList";
import ProductDetail from "./pages/ProductDetail";
import About from "./pages/About";
import NotFound from "./pages/NotFound";

function App() {
  const { theme } = useTheme();

  return (
    <div style={{
      minHeight: "100vh",
      backgroundColor: theme === "dark" ? "#0f172a" : "#f8fafc",
      color: theme === "dark" ? "#f1f5f9" : "#0f172a",
      transition: "background-color 0.3s, color 0.3s",
    }}>
      <Navbar />
      <main style={{ maxWidth: "1000px", margin: "0 auto", padding: "32px 20px" }}>
        <Routes>
          <Route path="/" element={<Home />} />
          <Route path="/products" element={<ProductList />} />
          <Route path="/products/:productId" element={<ProductDetail />} />
          <Route path="/about" element={<About />} />
          <Route path="*" element={<NotFound />} />
        </Routes>
      </main>
    </div>
  );
}

export default App;
```

```jsx
// src/main.jsx
import React from "react";
import ReactDOM from "react-dom/client";
import { BrowserRouter } from "react-router-dom";
import { ThemeProvider } from "./context/ThemeContext";
import App from "./App";
import "./index.css";

ReactDOM.createRoot(document.getElementById("root")).render(
  <React.StrictMode>
    <BrowserRouter>
      <ThemeProvider>
        <App />
      </ThemeProvider>
    </BrowserRouter>
  </React.StrictMode>
);
```

```css
/* src/index.css */
* {
  margin: 0;
  padding: 0;
  box-sizing: border-box;
}

body {
  font-family: -apple-system, BlinkMacSystemFont, "Segoe UI", Roboto, sans-serif;
}

.nav-link {
  text-decoration: none;
  padding: 8px 14px;
  border-radius: 6px;
  color: #64748b;
  transition: all 0.2s;
}

.nav-link:hover {
  background-color: rgba(59, 130, 246, 0.1);
  color: #3b82f6;
}

.nav-link-active {
  background-color: #3b82f6;
  color: white !important;
  font-weight: 600;
}
```

**This project integrates:**
- **Components & Props** (Navbar, product cards, pages)
- **useState** (search filter, theme state)
- **useEffect** (available in useFetch hook)
- **React Router** (BrowserRouter, Routes, Route, NavLink, useParams, useNavigate)
- **Context API** (ThemeContext for dark/light mode)
- **Custom Hooks** (useFetch available in hooks folder)
- **Dynamic Routes** (/products/:productId)
- **404 Catch-All** (path="*")
- **Active NavLink Styling** (className callback with `end` prop)
</details>

---

## Part 4: React Phase Comprehensive Review (Weeks 16-21)

**These questions cover material from the entire React phase to test your overall understanding.**

---

**Review 1 (MCQ): What does JSX get compiled to?**

- A) HTML strings
- B) `React.createElement()` function calls
- C) Direct DOM manipulation commands
- D) CSS stylesheets

<details>
<summary>Answer</summary>

**B) `React.createElement()` function calls**

JSX is syntactic sugar. When your build tool (Vite, Babel) processes JSX, it transforms `<h1 className="title">Hello</h1>` into `React.createElement("h1", { className: "title" }, "Hello")`. These function calls return plain JavaScript objects (called "React elements") that describe what should appear on screen. React then uses these objects to efficiently update the actual DOM. (Week 16)
</details>

---

**Review 2 (MCQ): Why must you use a `key` prop when rendering lists in React?**

- A) Keys add CSS styling to list items
- B) Keys let React uniquely identify each item so it can efficiently update, reorder, or remove items
- C) Keys prevent the list from re-rendering
- D) Keys are optional and have no effect

<details>
<summary>Answer</summary>

**B) Keys let React uniquely identify each item so it can efficiently update, reorder, or remove items**

When React re-renders a list, it needs to figure out which items are new, which were removed, and which simply moved. Without keys, React has no way to track individual items and falls back to re-rendering the entire list from scratch. With unique, stable keys (like database IDs), React can match old items to new items and only update what actually changed. Never use array indices as keys if the list can be reordered, filtered, or modified. (Week 17)
</details>

---

**Review 3 (MCQ): What is the correct way to update state that depends on the previous state value?**

- A) `setCount(count + 1)`
- B) `setCount((prevCount) => prevCount + 1)`
- C) `count = count + 1`
- D) `this.setState({ count: count + 1 })`

<details>
<summary>Answer</summary>

**B) `setCount((prevCount) => prevCount + 1)`**

When the new state depends on the previous state, you should use the functional updater form: `setCount(prev => prev + 1)`. This is because state updates may be batched and asynchronous. If you call `setCount(count + 1)` multiple times in the same event handler, each call reads the same stale `count` value. The functional form guarantees you are working with the most recent state. Option C directly mutates state, which React cannot detect. Option D is class component syntax. (Week 18)
</details>

---

**Review 4 (MCQ): What is the purpose of the dependency array in `useEffect`?**

```jsx
useEffect(() => {
  fetchData(userId);
}, [userId]);
```

- A) It lists all the variables the effect creates
- B) It tells React when to re-run the effect -- only when the listed values change
- C) It defines the props the component accepts
- D) It prevents the component from unmounting

<details>
<summary>Answer</summary>

**B) It tells React when to re-run the effect -- only when the listed values change**

The dependency array controls when the effect function re-executes. After each render, React compares the current dependency values to the previous ones. If any value changed, the effect runs again. If none changed, the effect is skipped. `[]` means "no dependencies, run once on mount." `[userId]` means "re-run whenever userId changes." Omitting the array entirely means "run after every render." (Week 19)
</details>

---

**Review 5 (MCQ): In the following code, what does `<Outlet />` do?**

```jsx
function DashboardLayout() {
  return (
    <div>
      <Sidebar />
      <main>
        <Outlet />
      </main>
    </div>
  );
}
```

- A) It exits the component early
- B) It renders the matched child route's component inside the parent layout
- C) It creates a new route
- D) It provides context to child components

<details>
<summary>Answer</summary>

**B) It renders the matched child route's component inside the parent layout**

`<Outlet />` is a placeholder in a parent route's component that says "render whichever child route currently matches the URL here." The parent layout (sidebar, header) stays on screen, and only the `<Outlet />` area changes as the user navigates between child routes. For example, if the routes are `/dashboard/profile` and `/dashboard/settings`, the `DashboardLayout` remains mounted while `<Outlet />` swaps between `<Profile />` and `<Settings />`. (Week 20)
</details>

---

**Review 6 (Coding): Fix the Bug**

The following component has a bug. The counter shows stale values when clicking rapidly. Identify and fix the issue.

```jsx
function Counter() {
  const [count, setCount] = useState(0);

  function handleTripleIncrement() {
    setCount(count + 1);
    setCount(count + 1);
    setCount(count + 1);
  }

  return (
    <div>
      <p>Count: {count}</p>
      <button onClick={handleTripleIncrement}>+3</button>
    </div>
  );
}
```

<details>
<summary>Answer</summary>

**Bug:** All three `setCount(count + 1)` calls read the same `count` value from the closure. If `count` is 0, all three calls evaluate to `setCount(0 + 1)`, so the counter only increments by 1, not 3.

**Fix:** Use the functional updater form:

```jsx
function Counter() {
  const [count, setCount] = useState(0);

  function handleTripleIncrement() {
    setCount((prev) => prev + 1);  // prev = 0, returns 1
    setCount((prev) => prev + 1);  // prev = 1, returns 2
    setCount((prev) => prev + 1);  // prev = 2, returns 3
  }

  return (
    <div>
      <p>Count: {count}</p>
      <button onClick={handleTripleIncrement}>+3</button>
    </div>
  );
}
```

The functional updater `(prev) => prev + 1` always receives the most recent pending state value, so each call correctly builds on the previous one. This is essential whenever new state depends on old state. (Week 18)
</details>

---

**Review 7 (Coding): Write a `useWindowWidth` Custom Hook**

Create a custom hook that tracks the browser window's width and returns it. The component using this hook should update whenever the window is resized.

<details>
<summary>Answer</summary>

```jsx
// src/hooks/useWindowWidth.js
import { useState, useEffect } from "react";

function useWindowWidth() {
  const [width, setWidth] = useState(window.innerWidth);

  useEffect(() => {
    function handleResize() {
      setWidth(window.innerWidth);
    }

    window.addEventListener("resize", handleResize);

    // Cleanup: remove the event listener on unmount
    return () => window.removeEventListener("resize", handleResize);
  }, []);

  return width;
}

export default useWindowWidth;
```

```jsx
// Usage in a component
import useWindowWidth from "../hooks/useWindowWidth";

function ResponsiveMessage() {
  const width = useWindowWidth();

  return (
    <div>
      <p>Window width: {width}px</p>
      {width < 768 ? (
        <p>You are on a mobile device.</p>
      ) : (
        <p>You are on a desktop device.</p>
      )}
    </div>
  );
}
```

This hook combines `useState` (to hold the width) and `useEffect` (to set up and clean up the resize listener). It follows all hook rules: named with `use`, called at the top level, and includes proper cleanup to prevent memory leaks. Each component that calls `useWindowWidth()` gets its own independent width state. (Weeks 19 + 21)
</details>

---

**Review 8 (Coding): Build a Component That Fetches Data on Route Change**

Write a `UserProfile` component that reads a `userId` from the URL parameters and fetches the user's data from `https://jsonplaceholder.typicode.com/users/{userId}`. Handle loading, error, and success states.

<details>
<summary>Answer</summary>

```jsx
// Route setup (in App.jsx):
// <Route path="/users/:userId" element={<UserProfile />} />

import { useState, useEffect } from "react";
import { useParams, Link } from "react-router-dom";

function UserProfile() {
  const { userId } = useParams();
  const [user, setUser] = useState(null);
  const [loading, setLoading] = useState(true);
  const [error, setError] = useState(null);

  useEffect(() => {
    setUser(null);
    setLoading(true);
    setError(null);

    async function fetchUser() {
      try {
        const response = await fetch(
          `https://jsonplaceholder.typicode.com/users/${userId}`
        );

        if (!response.ok) {
          throw new Error(`User not found (status ${response.status})`);
        }

        const data = await response.json();
        setUser(data);
      } catch (err) {
        setError(err.message);
      } finally {
        setLoading(false);
      }
    }

    fetchUser();
  }, [userId]); // Re-fetch when userId changes (user navigates to different profile)

  if (loading) return <p>Loading user profile...</p>;
  if (error) return <p style={{ color: "red" }}>Error: {error}</p>;
  if (!user) return <p>No user data available.</p>;

  return (
    <div style={{ padding: "20px" }}>
      <Link to="/users" style={{ color: "#3b82f6" }}>&larr; All Users</Link>
      <h1>{user.name}</h1>
      <p><strong>Email:</strong> {user.email}</p>
      <p><strong>Phone:</strong> {user.phone}</p>
      <p><strong>Website:</strong> {user.website}</p>
      <p><strong>Company:</strong> {user.company.name}</p>
      <p><strong>City:</strong> {user.address.city}</p>
    </div>
  );
}

export default UserProfile;
```

This component combines concepts from multiple weeks:
- **useParams** (Week 20) to read the dynamic route parameter.
- **useEffect with dependency** (Week 19) to fetch data when the parameter changes.
- **useState** (Week 18) to manage loading, error, and data states.
- **Conditional rendering** (Week 17) to show different UI based on the current state.
- **Link** (Week 20) for navigation back to the user list.
</details>

---

**Review 9 (MCQ): Which of the following is the correct order of the React component lifecycle in functional components?**

- A) Unmount, Mount, Update
- B) Mount (first render + useEffect), Update (re-render + useEffect if deps changed), Unmount (cleanup runs)
- C) Render, State, Props, Effects
- D) Initialize, Execute, Destroy

<details>
<summary>Answer</summary>

**B) Mount (first render + useEffect), Update (re-render + useEffect if deps changed), Unmount (cleanup runs)**

In functional components using hooks:
1. **Mount:** The component function runs for the first time, JSX is rendered to the DOM, and `useEffect` callbacks execute after the browser paints.
2. **Update:** When state or props change, the component function runs again with new values. If `useEffect` dependencies changed, the previous cleanup runs first, then the new effect executes.
3. **Unmount:** When the component is removed from the DOM, all `useEffect` cleanup functions run one final time to prevent memory leaks (clearing timers, removing event listeners, aborting fetches).
(Week 19)
</details>

---

**Review 10 (Coding): Combine Context with React Router for Authentication**

Write a brief code outline (not a full application) showing how you would structure an `AuthContext` that works with React Router's `<Navigate>` to protect routes. Show the context, the protected route component, and the route setup.

<details>
<summary>Answer</summary>

```jsx
// 1. AUTH CONTEXT
import { createContext, useState, useContext } from "react";

const AuthContext = createContext();

function AuthProvider({ children }) {
  const [user, setUser] = useState(null);

  const login = (userData) => setUser(userData);
  const logout = () => setUser(null);
  const isAuthenticated = user !== null;

  return (
    <AuthContext.Provider value={{ user, isAuthenticated, login, logout }}>
      {children}
    </AuthContext.Provider>
  );
}

function useAuth() {
  const context = useContext(AuthContext);
  if (!context) throw new Error("useAuth must be used within AuthProvider");
  return context;
}

export { AuthProvider, useAuth };
```

```jsx
// 2. PROTECTED ROUTE COMPONENT
import { Navigate } from "react-router-dom";
import { useAuth } from "../context/AuthContext";

function ProtectedRoute({ children }) {
  const { isAuthenticated } = useAuth();

  if (!isAuthenticated) {
    return <Navigate to="/login" replace />;
  }

  return children;
}

export default ProtectedRoute;
```

```jsx
// 3. ROUTE SETUP (App.jsx)
import { Routes, Route } from "react-router-dom";
import ProtectedRoute from "./components/ProtectedRoute";

function App() {
  return (
    <Routes>
      {/* Public */}
      <Route path="/" element={<Home />} />
      <Route path="/login" element={<Login />} />

      {/* Protected */}
      <Route path="/dashboard" element={
        <ProtectedRoute><Dashboard /></ProtectedRoute>
      } />
      <Route path="/settings" element={
        <ProtectedRoute><Settings /></ProtectedRoute>
      } />
    </Routes>
  );
}
```

```jsx
// 4. ENTRY POINT (main.jsx)
import { BrowserRouter } from "react-router-dom";
import { AuthProvider } from "./context/AuthContext";

ReactDOM.createRoot(document.getElementById("root")).render(
  <BrowserRouter>
    <AuthProvider>
      <App />
    </AuthProvider>
  </BrowserRouter>
);
```

This pattern combines:
- **Context** (Week 21): `AuthProvider` broadcasts auth state to all components.
- **useContext** (Week 21): `useAuth` hook provides clean access.
- **Navigate** (Week 20): Redirects unauthenticated users.
- **Protected Routes** (Week 20): Guards components behind an auth check.
- **Component composition** (Week 17): `ProtectedRoute` uses `children` prop.
</details>
