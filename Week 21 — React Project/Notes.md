# Week 21: React Advanced Patterns & Project

> **Prerequisites:** React components, JSX, props, state, useState, useEffect, useRef, and React Router from Weeks 16-20.

---

## Table of Contents

1. [useContext Hook for Global State](#1-usecontext-hook-for-global-state)
2. [Context in Action: Theme & Auth Examples](#2-context-in-action-theme--auth-examples)
3. [Custom Hooks](#3-custom-hooks)
4. [Performance Optimization: React.memo, useMemo, useCallback](#4-performance-optimization-reactmemo-usememo-usecallback)
5. [React Project: Multi-Page Blog/E-Commerce UI](#5-react-project-multi-page-bloge-commerce-ui)
6. [React Phase Summary (Weeks 16-21)](#6-react-phase-summary-weeks-16-21)

---

## 1. useContext Hook for Global State

### The Problem: Prop Drilling

As your React applications grow, you will often need to share data (like the current user, theme, or language) across many components at different levels of the component tree. The obvious approach is to pass this data through props from parent to child to grandchild. But when data needs to travel through many layers of components that do not even use it, this becomes painful. This problem is called **prop drilling**.

### Real-Life Analogy: The Office Memo

Imagine you are the CEO of a company and you need to send a message to an intern who works five floors below you. With prop drilling, you hand the memo to your VP, who hands it to the Director, who hands it to the Manager, who hands it to the Team Lead, who finally hands it to the Intern. Four people touched the memo but none of them needed to read it. They were just passing it along.

With Context, you post the memo on a company-wide bulletin board. Anyone who needs it can read it directly, regardless of where they sit in the organization.

```
  PROP DRILLING (Without Context)
  =================================

  <App>              user={currentUser}
    |
    +-- <Layout>     user={currentUser}       (does not use it, just passes it)
          |
          +-- <Sidebar>   user={currentUser}  (does not use it, just passes it)
                |
                +-- <UserMenu>  user={currentUser}   (does not use it, just passes it)
                      |
                      +-- <Avatar>  user={currentUser}   (FINALLY uses it!)

  Problem: Layout, Sidebar, and UserMenu receive "user" only to pass it down.
           They do not use it themselves. This is prop drilling.


  WITH CONTEXT (useContext)
  ==========================

  <UserContext.Provider value={currentUser}>     <-- Broadcast from the top
    <App>
      +-- <Layout>                               <-- Does NOT need user prop
            +-- <Sidebar>                        <-- Does NOT need user prop
                  +-- <UserMenu>                 <-- Does NOT need user prop
                        +-- <Avatar>             <-- useContext(UserContext) --> gets currentUser
  </UserContext.Provider>

  Solution: Only <Avatar> accesses the user. No one else is burdened.
```

### How Context Works: Three Steps

Context follows a simple three-step pattern:

1. **Create** the context (define the bulletin board).
2. **Provide** the context value (post the memo on the board).
3. **Consume** the context value (read the memo from the board).

```
  CONTEXT: THREE STEPS
  =====================

  Step 1: CREATE                Step 2: PROVIDE              Step 3: CONSUME
  +-----------------+           +-------------------+        +-------------------+
  | createContext()  |           | <Context.Provider |        | useContext(Ctx)    |
  |                 |           |   value={data}>   |        |                   |
  | Creates a       |    --->   |   <App />         |  --->  | Any component     |
  | "channel"       |           | </Context.Provider>|        | can read the data |
  +-----------------+           +-------------------+        +-------------------+
```

### Step 1: Create Context

```javascript
// src/context/ThemeContext.js
import { createContext } from "react";

// Create a context with a default value
const ThemeContext = createContext("light");

export default ThemeContext;
```

`createContext` creates a context object. The argument (`"light"`) is the default value used only when a component tries to consume the context but there is no Provider above it in the tree.

### Step 2: Provide Context

The Provider wraps the part of the component tree that needs access to the value. Any component inside the Provider can access the value.

```jsx
// src/App.jsx
import { useState } from "react";
import ThemeContext from "./context/ThemeContext";
import Page from "./components/Page";

function App() {
  const [theme, setTheme] = useState("light");

  return (
    <ThemeContext.Provider value={theme}>
      <button onClick={() => setTheme(theme === "light" ? "dark" : "light")}>
        Toggle Theme
      </button>
      <Page />
    </ThemeContext.Provider>
  );
}
```

### Step 3: Consume Context

Any component inside the Provider can read the context value using the `useContext` hook. It does not matter how deep in the tree the component is.

```jsx
// src/components/Page.jsx
import Card from "./Card";

function Page() {
  // Page does NOT need the theme prop. It just renders Card.
  return (
    <div>
      <h1>My Page</h1>
      <Card />
    </div>
  );
}

export default Page;
```

```jsx
// src/components/Card.jsx
import { useContext } from "react";
import ThemeContext from "../context/ThemeContext";

function Card() {
  const theme = useContext(ThemeContext);

  const styles = {
    backgroundColor: theme === "dark" ? "#1f2937" : "#ffffff",
    color: theme === "dark" ? "#f9fafb" : "#111827",
    padding: "20px",
    borderRadius: "8px",
    border: "1px solid #e5e7eb",
  };

  return (
    <div style={styles}>
      <h2>Card Component</h2>
      <p>The current theme is: {theme}</p>
    </div>
  );
}

export default Card;
```

Notice: `Page` never receives or passes the `theme` prop. `Card` reads it directly from the context. Prop drilling is eliminated.

### When to Use Context vs Props

| Use Props When...                          | Use Context When...                              |
| ------------------------------------------ | ------------------------------------------------ |
| Data is only needed 1-2 levels deep        | Data is needed by many components at many levels  |
| Only a few components need the data        | The same data is used across the entire app       |
| The data flow is straightforward           | Passing through intermediaries is cumbersome      |
| Component reusability is a priority        | Data is truly "global" (theme, auth, language)    |

**Rule of thumb:** If you find yourself passing a prop through three or more components that do not use it, consider using Context.

---

## 2. Context in Action: Theme & Auth Examples

### Theme Context: Complete Example

This example implements a full dark/light mode toggle using Context.

```jsx
// src/context/ThemeContext.jsx
import { createContext, useState, useContext } from "react";

// 1. Create the context
const ThemeContext = createContext();

// 2. Create a Provider component that manages the state
function ThemeProvider({ children }) {
  const [theme, setTheme] = useState("light");

  function toggleTheme() {
    setTheme((prev) => (prev === "light" ? "dark" : "light"));
  }

  // The value includes both the current theme AND the toggle function
  const value = { theme, toggleTheme };

  return (
    <ThemeContext.Provider value={value}>
      {children}
    </ThemeContext.Provider>
  );
}

// 3. Create a custom hook for easy consumption
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

```jsx
// src/App.jsx
import { useTheme } from "./context/ThemeContext";
import Navbar from "./components/Navbar";
import Content from "./components/Content";

function App() {
  const { theme } = useTheme();

  const appStyles = {
    minHeight: "100vh",
    backgroundColor: theme === "dark" ? "#111827" : "#f9fafb",
    color: theme === "dark" ? "#f9fafb" : "#111827",
    transition: "background-color 0.3s, color 0.3s",
  };

  return (
    <div style={appStyles}>
      <Navbar />
      <Content />
    </div>
  );
}

export default App;
```

```jsx
// src/components/Navbar.jsx
import { useTheme } from "../context/ThemeContext";

function Navbar() {
  const { theme, toggleTheme } = useTheme();

  return (
    <nav style={{
      display: "flex",
      justifyContent: "space-between",
      alignItems: "center",
      padding: "16px 32px",
      backgroundColor: theme === "dark" ? "#1f2937" : "#ffffff",
      borderBottom: "1px solid",
      borderColor: theme === "dark" ? "#374151" : "#e5e7eb",
    }}>
      <h2 style={{ margin: 0 }}>MyApp</h2>
      <button
        onClick={toggleTheme}
        style={{
          padding: "8px 16px",
          borderRadius: "6px",
          border: "1px solid",
          cursor: "pointer",
          backgroundColor: theme === "dark" ? "#374151" : "#e5e7eb",
          color: theme === "dark" ? "#f9fafb" : "#111827",
        }}
      >
        Switch to {theme === "light" ? "Dark" : "Light"} Mode
      </button>
    </nav>
  );
}

export default Navbar;
```

```jsx
// src/components/Content.jsx
import { useTheme } from "../context/ThemeContext";

function Content() {
  const { theme } = useTheme();

  const cardStyle = {
    padding: "24px",
    margin: "20px",
    borderRadius: "8px",
    backgroundColor: theme === "dark" ? "#1f2937" : "#ffffff",
    border: "1px solid",
    borderColor: theme === "dark" ? "#374151" : "#e5e7eb",
  };

  return (
    <main style={{ padding: "20px" }}>
      <div style={cardStyle}>
        <h2>Welcome</h2>
        <p>This card respects the current theme: <strong>{theme}</strong></p>
        <p>Click the button in the navbar to toggle between light and dark mode.</p>
      </div>
      <div style={cardStyle}>
        <h2>How It Works</h2>
        <p>The ThemeContext provides the current theme to every component.</p>
        <p>No props are passed through intermediate components.</p>
      </div>
    </main>
  );
}

export default Content;
```

```
  THEME CONTEXT FLOW
  ====================

  ThemeProvider (manages state: "light" / "dark")
       |
       |--- provides { theme, toggleTheme }
       |
       +-- <App>
             |--- useTheme() --> reads "theme" for background color
             |
             +-- <Navbar>
             |     |--- useTheme() --> reads "theme" for styling
             |     |--- calls toggleTheme() on button click
             |
             +-- <Content>
                   |--- useTheme() --> reads "theme" for card styling

  Every component gets the theme directly. No prop drilling.
  When toggleTheme() is called, ALL consumers re-render with the new value.
```

### Auth Context: Complete Example

This example implements user authentication state that is accessible throughout the application.

```jsx
// src/context/AuthContext.jsx
import { createContext, useState, useContext } from "react";

const AuthContext = createContext();

function AuthProvider({ children }) {
  const [user, setUser] = useState(null);

  function login(email, password) {
    // In a real app, you would make an API call here:
    // const response = await fetch("/api/login", { method: "POST", body: ... });
    // const userData = await response.json();

    // Simulating a successful login
    const userData = {
      id: 1,
      name: "Sarah Ahmed",
      email: email,
      role: "admin",
    };
    setUser(userData);
  }

  function logout() {
    setUser(null);
  }

  // isAuthenticated is derived from whether user exists
  const isAuthenticated = user !== null;

  const value = { user, isAuthenticated, login, logout };

  return (
    <AuthContext.Provider value={value}>
      {children}
    </AuthContext.Provider>
  );
}

function useAuth() {
  const context = useContext(AuthContext);
  if (context === undefined) {
    throw new Error("useAuth must be used within an AuthProvider");
  }
  return context;
}

export { AuthProvider, useAuth };
```

```jsx
// src/main.jsx
import React from "react";
import ReactDOM from "react-dom/client";
import { BrowserRouter } from "react-router-dom";
import { AuthProvider } from "./context/AuthContext";
import App from "./App";

ReactDOM.createRoot(document.getElementById("root")).render(
  <React.StrictMode>
    <BrowserRouter>
      <AuthProvider>
        <App />
      </AuthProvider>
    </BrowserRouter>
  </React.StrictMode>
);
```

```jsx
// src/components/ProtectedRoute.jsx
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
// src/pages/Login.jsx
import { useState } from "react";
import { useNavigate } from "react-router-dom";
import { useAuth } from "../context/AuthContext";

function Login() {
  const [email, setEmail] = useState("");
  const [password, setPassword] = useState("");
  const { login } = useAuth();
  const navigate = useNavigate();

  function handleSubmit(event) {
    event.preventDefault();
    login(email, password);
    navigate("/dashboard", { replace: true });
  }

  return (
    <div style={{ maxWidth: "400px", margin: "40px auto" }}>
      <h1>Login</h1>
      <form onSubmit={handleSubmit}>
        <input
          type="email"
          value={email}
          onChange={(e) => setEmail(e.target.value)}
          placeholder="Email"
          style={{ display: "block", width: "100%", padding: "8px", marginBottom: "12px" }}
        />
        <input
          type="password"
          value={password}
          onChange={(e) => setPassword(e.target.value)}
          placeholder="Password"
          style={{ display: "block", width: "100%", padding: "8px", marginBottom: "12px" }}
        />
        <button type="submit" style={{ padding: "10px 24px" }}>Log In</button>
      </form>
    </div>
  );
}

export default Login;
```

```jsx
// src/pages/Dashboard.jsx
import { useAuth } from "../context/AuthContext";
import { useNavigate } from "react-router-dom";

function Dashboard() {
  const { user, logout } = useAuth();
  const navigate = useNavigate();

  function handleLogout() {
    logout();
    navigate("/login");
  }

  return (
    <div style={{ padding: "20px" }}>
      <h1>Dashboard</h1>
      <p>Welcome, {user.name}!</p>
      <p>Email: {user.email}</p>
      <p>Role: {user.role}</p>
      <button onClick={handleLogout} style={{ padding: "8px 16px", marginTop: "12px" }}>
        Log Out
      </button>
    </div>
  );
}

export default Dashboard;
```

```jsx
// src/App.jsx
import { Routes, Route } from "react-router-dom";
import Login from "./pages/Login";
import Dashboard from "./pages/Dashboard";
import ProtectedRoute from "./components/ProtectedRoute";

function App() {
  return (
    <Routes>
      <Route path="/login" element={<Login />} />
      <Route
        path="/dashboard"
        element={
          <ProtectedRoute>
            <Dashboard />
          </ProtectedRoute>
        }
      />
    </Routes>
  );
}

export default App;
```

```
  AUTH CONTEXT FLOW
  ==================

  AuthProvider (manages state: user object or null)
       |
       |--- provides { user, isAuthenticated, login, logout }
       |
       +-- <App>
             |
             +-- <Login>
             |     |--- useAuth() --> calls login(email, password)
             |     |--- After login: user is set, navigates to /dashboard
             |
             +-- <ProtectedRoute>
             |     |--- useAuth() --> checks isAuthenticated
             |     |--- If false: <Navigate to="/login" />
             |     |--- If true: renders children
             |
             +-- <Dashboard>
                   |--- useAuth() --> reads user.name, user.email
                   |--- calls logout() on button click
```

---

## 3. Custom Hooks

### What Are Custom Hooks?

A **custom hook** is a JavaScript function that starts with the word `use` and can call other React hooks inside it. Custom hooks let you extract and reuse stateful logic across multiple components.

Think of it this way: if you find yourself writing the same combination of `useState`, `useEffect`, or other hooks in multiple components, you can extract that logic into a custom hook and reuse it everywhere.

### Real-Life Analogy: A Recipe vs Ingredients

Without custom hooks, every component that needs to fetch data has to write the same fetch-loading-error pattern from scratch. It is like every cook in a restaurant individually figuring out how to make the base tomato sauce.

A custom hook is like writing the sauce recipe on a card. Any cook can follow the recipe card and get the same result without reinventing it each time.

### Rules of Custom Hooks

1. **Name must start with `use`** -- This is not optional. React uses this naming convention to detect hooks and enforce the rules of hooks (like not calling them inside conditions or loops). `useFetch`, `useLocalStorage`, `useToggle` are valid names. `fetchData`, `localStorage`, `toggle` are not.

2. **Can call other hooks** -- Custom hooks can use `useState`, `useEffect`, `useRef`, `useContext`, and even other custom hooks.

3. **Follow the rules of hooks** -- Like all hooks, custom hooks must be called at the top level of a function component or another custom hook. Never inside loops, conditions, or nested functions.

4. **Each call gets its own state** -- If two components use the same custom hook, they each get their own independent copy of the state. Custom hooks share logic, not state.

```
  CUSTOM HOOKS: SHARED LOGIC, INDEPENDENT STATE
  ===============================================

  useFetch("/api/users")  <-- Component A calls it
       |
       +-- own loading state: true
       +-- own data state: null
       +-- own error state: null

  useFetch("/api/posts")  <-- Component B calls it
       |
       +-- own loading state: true    <-- Completely separate!
       +-- own data state: null
       +-- own error state: null
```

### Example 1: useFetch Hook

This hook handles the common pattern of fetching data from an API with loading and error states.

```jsx
// src/hooks/useFetch.js
import { useState, useEffect } from "react";

function useFetch(url) {
  const [data, setData] = useState(null);
  const [loading, setLoading] = useState(true);
  const [error, setError] = useState(null);

  useEffect(() => {
    // Reset state when URL changes
    setData(null);
    setLoading(true);
    setError(null);

    async function fetchData() {
      try {
        const response = await fetch(url);

        if (!response.ok) {
          throw new Error(`HTTP error! Status: ${response.status}`);
        }

        const result = await response.json();
        setData(result);
      } catch (err) {
        setError(err.message);
      } finally {
        setLoading(false);
      }
    }

    fetchData();
  }, [url]);

  return { data, loading, error };
}

export default useFetch;
```

**Using useFetch in components:**

```jsx
// src/pages/Users.jsx
import useFetch from "../hooks/useFetch";

function Users() {
  const { data: users, loading, error } = useFetch("https://jsonplaceholder.typicode.com/users");

  if (loading) return <p>Loading users...</p>;
  if (error) return <p>Error: {error}</p>;

  return (
    <div>
      <h1>Users</h1>
      <ul>
        {users.map((user) => (
          <li key={user.id}>{user.name} - {user.email}</li>
        ))}
      </ul>
    </div>
  );
}

export default Users;
```

```jsx
// src/pages/Posts.jsx
import useFetch from "../hooks/useFetch";

function Posts() {
  const { data: posts, loading, error } = useFetch("https://jsonplaceholder.typicode.com/posts");

  if (loading) return <p>Loading posts...</p>;
  if (error) return <p>Error: {error}</p>;

  return (
    <div>
      <h1>Posts ({posts.length} total)</h1>
      {posts.slice(0, 10).map((post) => (
        <div key={post.id} style={{ marginBottom: "16px" }}>
          <h3>{post.title}</h3>
          <p>{post.body}</p>
        </div>
      ))}
    </div>
  );
}

export default Posts;
```

Both `Users` and `Posts` use `useFetch` but each has its own independent `data`, `loading`, and `error` state. The fetch logic is written once and reused everywhere.

### Example 2: useLocalStorage Hook

This hook works like `useState` but automatically syncs the value with `localStorage`, so data persists across page reloads.

```jsx
// src/hooks/useLocalStorage.js
import { useState } from "react";

function useLocalStorage(key, initialValue) {
  // Initialize state from localStorage (or use initialValue as fallback)
  const [storedValue, setStoredValue] = useState(() => {
    try {
      const item = localStorage.getItem(key);
      // If item exists in localStorage, parse and return it
      // Otherwise, return the initialValue
      return item !== null ? JSON.parse(item) : initialValue;
    } catch (error) {
      console.error("Error reading localStorage:", error);
      return initialValue;
    }
  });

  // Wrapper around setState that also saves to localStorage
  function setValue(value) {
    try {
      // Allow value to be a function (like useState)
      const valueToStore = value instanceof Function ? value(storedValue) : value;
      setStoredValue(valueToStore);
      localStorage.setItem(key, JSON.stringify(valueToStore));
    } catch (error) {
      console.error("Error writing to localStorage:", error);
    }
  }

  return [storedValue, setValue];
}

export default useLocalStorage;
```

**Using useLocalStorage:**

```jsx
// src/components/Settings.jsx
import useLocalStorage from "../hooks/useLocalStorage";

function Settings() {
  const [name, setName] = useLocalStorage("userName", "");
  const [fontSize, setFontSize] = useLocalStorage("fontSize", 16);
  const [notifications, setNotifications] = useLocalStorage("notifications", true);

  return (
    <div style={{ fontSize: `${fontSize}px` }}>
      <h1>Settings</h1>

      <label>Name: </label>
      <input value={name} onChange={(e) => setName(e.target.value)} />

      <br /><br />

      <label>Font Size: {fontSize}px </label>
      <input
        type="range"
        min="12"
        max="24"
        value={fontSize}
        onChange={(e) => setFontSize(Number(e.target.value))}
      />

      <br /><br />

      <label>
        <input
          type="checkbox"
          checked={notifications}
          onChange={(e) => setNotifications(e.target.checked)}
        />
        Enable Notifications
      </label>

      <p>Hello, {name || "Guest"}! Refresh the page -- your settings will persist.</p>
    </div>
  );
}

export default Settings;
```

Every setting is automatically saved to `localStorage` when it changes and restored when the page reloads.

### Example 3: useToggle Hook

A simple hook for boolean toggle state -- useful for modals, dropdowns, show/hide toggles, and similar patterns.

```jsx
// src/hooks/useToggle.js
import { useState } from "react";

function useToggle(initialValue = false) {
  const [value, setValue] = useState(initialValue);

  function toggle() {
    setValue((prev) => !prev);
  }

  function setTrue() {
    setValue(true);
  }

  function setFalse() {
    setValue(false);
  }

  return { value, toggle, setTrue, setFalse };
}

export default useToggle;
```

**Using useToggle:**

```jsx
import useToggle from "../hooks/useToggle";

function FAQ() {
  const answer1 = useToggle();
  const answer2 = useToggle();
  const answer3 = useToggle();

  return (
    <div>
      <h1>FAQ</h1>

      <div>
        <button onClick={answer1.toggle}>
          What is React? {answer1.value ? "[-]" : "[+]"}
        </button>
        {answer1.value && <p>React is a JavaScript library for building user interfaces.</p>}
      </div>

      <div>
        <button onClick={answer2.toggle}>
          What is JSX? {answer2.value ? "[-]" : "[+]"}
        </button>
        {answer2.value && <p>JSX is a syntax extension that lets you write HTML-like code in JavaScript.</p>}
      </div>

      <div>
        <button onClick={answer3.toggle}>
          What is a hook? {answer3.value ? "[-]" : "[+]"}
        </button>
        {answer3.value && <p>A hook is a function that lets you use state and lifecycle features in function components.</p>}
      </div>
    </div>
  );
}
```

Each FAQ item has its own independent toggle state, even though they all use the same `useToggle` hook.

---

## 4. Performance Optimization: React.memo, useMemo, useCallback

### Understanding React Re-renders

Before diving into optimization, you need to understand when React re-renders components.

**A component re-renders when:**
1. Its **state** changes (via `useState` setter).
2. Its **parent** re-renders (even if the child's props have not changed).
3. A **context** value it consumes changes.

Point 2 is the important one. When a parent re-renders, **all of its children re-render**, even if their props are exactly the same. For most applications this is perfectly fine because React is fast. But in specific cases with expensive components, this can cause noticeable slowdowns.

```
  DEFAULT RE-RENDER BEHAVIOR
  ============================

  <App>  (state changes here)
    |
    +-- <Header />        re-renders (child of App)
    |
    +-- <ProductList />   re-renders (child of App)
    |     |
    |     +-- <ProductCard />  x100   ALL 100 re-render!
    |
    +-- <Footer />        re-renders (child of App)

  Even if Header, Footer, and 99 of the ProductCards
  received NO prop changes, they all re-render.
```

### React.memo -- Memoizing Components

`React.memo` is a higher-order component that wraps a component and tells React: "Only re-render this component if its props actually changed." If the same props are passed, React skips the re-render and reuses the last rendered output.

```jsx
import React from "react";

// Without memo: re-renders every time parent re-renders
function ProductCard({ name, price }) {
  console.log(`Rendering: ${name}`);
  return (
    <div style={{ border: "1px solid #e5e7eb", padding: "16px", borderRadius: "8px" }}>
      <h3>{name}</h3>
      <p>${price}</p>
    </div>
  );
}

// With memo: only re-renders if name or price changed
const MemoizedProductCard = React.memo(ProductCard);

export default MemoizedProductCard;
```

**Using it:**

```jsx
import { useState } from "react";
import ProductCard from "./ProductCard";

function App() {
  const [count, setCount] = useState(0);

  return (
    <div>
      <p>Count: {count}</p>
      <button onClick={() => setCount(count + 1)}>Increment</button>

      {/* Without memo: re-renders on every count change */}
      {/* With memo: does NOT re-render because name and price never change */}
      <ProductCard name="Laptop" price={999} />
      <ProductCard name="Mouse" price={29} />
    </div>
  );
}
```

Without `React.memo`, clicking "Increment" would re-render both `ProductCard` components even though their props (`name` and `price`) never change. With `React.memo`, React compares the old and new props and skips the re-render because they are identical.

### useMemo -- Memoizing Expensive Calculations

`useMemo` caches the result of an **expensive computation** so it is not recalculated on every render. It only recalculates when one of its dependencies changes.

```jsx
import { useState, useMemo } from "react";

function ProductList({ products }) {
  const [sortBy, setSortBy] = useState("name");
  const [searchQuery, setSearchQuery] = useState("");

  // WITHOUT useMemo: sorts the entire array on EVERY render
  // (even if only searchQuery changed, not sortBy)

  // WITH useMemo: only re-sorts when products or sortBy changes
  const sortedProducts = useMemo(() => {
    console.log("Sorting products...");  // Check when this runs
    return [...products].sort((a, b) => {
      if (sortBy === "name") return a.name.localeCompare(b.name);
      if (sortBy === "price") return a.price - b.price;
      return 0;
    });
  }, [products, sortBy]);
  //    ^^^^^^^^^^^^^^^^
  //    Only recalculates when products or sortBy changes.
  //    Typing in the search box does NOT trigger re-sort.

  const filteredProducts = sortedProducts.filter((p) =>
    p.name.toLowerCase().includes(searchQuery.toLowerCase())
  );

  return (
    <div>
      <input
        value={searchQuery}
        onChange={(e) => setSearchQuery(e.target.value)}
        placeholder="Search products..."
      />
      <select value={sortBy} onChange={(e) => setSortBy(e.target.value)}>
        <option value="name">Sort by Name</option>
        <option value="price">Sort by Price</option>
      </select>
      <ul>
        {filteredProducts.map((p) => (
          <li key={p.id}>{p.name} - ${p.price}</li>
        ))}
      </ul>
    </div>
  );
}
```

### useMemo Syntax

```javascript
const memoizedValue = useMemo(() => {
  // Expensive computation
  return computeExpensiveValue(a, b);
}, [a, b]);
//  ^^^^
//  Dependencies: only recompute when a or b changes
```

### useCallback -- Memoizing Functions

`useCallback` caches a **function definition** so that the same function reference is reused across renders. This is useful when passing callbacks to memoized child components.

**Why is this needed?** In JavaScript, every time a component renders, all functions defined inside it are recreated as new function objects. Even if the function code is identical, it is a new reference:

```javascript
// Every render creates a NEW function object:
function Parent() {
  // This is a new function reference on every render
  const handleClick = () => {
    console.log("clicked");
  };

  // React.memo on Child sees a "new" prop every time
  // because handleClick is a different reference
  return <Child onClick={handleClick} />;
}
```

`useCallback` solves this:

```jsx
import { useState, useCallback } from "react";
import React from "react";

// Memoized child component
const ExpensiveChild = React.memo(function ExpensiveChild({ onClick, label }) {
  console.log(`Rendering: ${label}`);
  return <button onClick={onClick}>{label}</button>;
});

function Parent() {
  const [count, setCount] = useState(0);
  const [text, setText] = useState("");

  // WITHOUT useCallback: new function on every render
  // React.memo on ExpensiveChild would be useless because
  // it always receives a "new" onClick prop

  // WITH useCallback: same function reference unless count changes
  const handleIncrement = useCallback(() => {
    setCount((prev) => prev + 1);
  }, []);
  //  ^^
  //  Empty deps: function never changes (it uses functional update)

  return (
    <div>
      <p>Count: {count}</p>
      <input value={text} onChange={(e) => setText(e.target.value)} />

      {/* Typing in the input re-renders Parent, but ExpensiveChild
          does NOT re-render because handleIncrement is the same reference */}
      <ExpensiveChild onClick={handleIncrement} label="Increment" />
    </div>
  );
}
```

### useCallback Syntax

```javascript
const memoizedFunction = useCallback(() => {
  // Function body
  doSomething(a, b);
}, [a, b]);
//  ^^^^
//  Dependencies: only create a new function when a or b changes
```

### When to Use (and When NOT to Over-Optimize)

| Tool            | Use When...                                        | Do NOT Use When...                              |
| --------------- | -------------------------------------------------- | ----------------------------------------------- |
| `React.memo`    | Component is expensive to render AND receives the same props often | Component is cheap or props change every render |
| `useMemo`       | Computation is genuinely expensive (sorting 10000 items, complex math) | Computation is trivial (adding two numbers)    |
| `useCallback`   | Passing callbacks to `React.memo` children          | No memoized children depend on the callback     |

### The Golden Rule: Do NOT Over-Optimize

```
  OPTIMIZATION DECISION TREE
  ============================

  Is there a noticeable performance problem?
       |
      NO  ------>  Do NOT optimize. React is fast enough.
       |
      YES
       |
       v
  Profile to find the bottleneck.
       |
       v
  Is a specific component re-rendering too often?
       |
      YES ------>  Use React.memo + useCallback
       |
  Is an expensive calculation running on every render?
       |
      YES ------>  Use useMemo
```

**Premature optimization is the root of all evil.** These tools add complexity to your code (extra dependencies to track, wrapper components, harder to debug). Only use them when you have measured an actual performance problem. For 95% of components, the default re-render behavior is perfectly fast.

### Common Mistakes

| Mistake                                         | Why It Is Wrong                                       |
| ------------------------------------------------ | ----------------------------------------------------- |
| Wrapping every component in `React.memo`         | Adds overhead; comparison cost may exceed re-render cost |
| Using `useMemo` for trivial calculations         | The memoization itself costs memory and comparison time |
| Using `useCallback` without `React.memo` child   | Pointless; the child re-renders anyway                |
| Forgetting dependencies in `useMemo`/`useCallback` | Stale values, bugs that are hard to track down       |
| Optimizing before measuring                      | You might optimize the wrong thing                    |

---

## 5. React Project: Multi-Page Blog/E-Commerce UI

### Project Overview

Now it is time to bring together everything from Weeks 16-21. You will build a multi-page React application that uses components, props, state, effects, routing, context, and custom hooks.

Choose one of the following project ideas (or create your own):

**Option A: Multi-Page Blog**
- Home page with featured posts
- All Posts listing page
- Individual Post detail page (dynamic route)
- About page
- Dark/Light theme toggle

**Option B: E-Commerce Product UI**
- Home page with featured products
- Products listing page with search and filter
- Individual Product detail page (dynamic route)
- Shopping cart page
- Dark/Light theme toggle

### Features List

Regardless of which project you choose, your application should include:

| Feature                      | React Concepts Used                       |
| ---------------------------- | ----------------------------------------- |
| Multiple pages               | React Router (BrowserRouter, Routes, Route) |
| Navigation bar               | NavLink with active styling               |
| Dynamic detail pages         | URL parameters, useParams                 |
| Data fetching or mock data   | useEffect, useState (or useFetch hook)    |
| Theme toggle                 | useContext (ThemeContext)                  |
| Persistent preferences       | useLocalStorage custom hook               |
| Form (search or contact)     | useState, controlled inputs               |
| Programmatic navigation      | useNavigate                               |
| 404 page                     | path="*" catch-all route                  |
| Loading and error states     | Conditional rendering                     |

### Component Tree

```
  PROJECT COMPONENT TREE
  =======================

  <BrowserRouter>
    <ThemeProvider>
      <AuthProvider>
        <App>
          |
          +-- <Navbar />                     NavLink, useTheme, useAuth
          |
          +-- <Routes>
                |
                +-- "/" ---------> <Home />          Featured items, Link
                |
                +-- "/items" ----> <ItemList />      useFetch or useState, search, filter
                |
                +-- "/items/:id" -> <ItemDetail />   useParams, useFetch
                |
                +-- "/about" ----> <About />         Static content
                |
                +-- "/login" ----> <Login />         useAuth, useNavigate
                |
                +-- "/cart" -----> <Cart />           useState or useContext
                |     (Protected)
                |
                +-- "*" ---------> <NotFound />      404 catch-all
          |
          +-- <Footer />                    Static content, useTheme
        </App>
      </AuthProvider>
    </ThemeProvider>
  </BrowserRouter>
```

### Recommended File Structure

```
  PROJECT FILE STRUCTURE
  =======================

  src/
  +-- main.jsx                    Entry point, wraps providers
  +-- App.jsx                     Routes definition
  +-- App.css                     Global styles
  |
  +-- components/                 Reusable UI components
  |     +-- Navbar.jsx
  |     +-- Footer.jsx
  |     +-- ItemCard.jsx
  |     +-- ProtectedRoute.jsx
  |     +-- SearchBar.jsx
  |     +-- LoadingSpinner.jsx
  |
  +-- pages/                      Full page components
  |     +-- Home.jsx
  |     +-- ItemList.jsx
  |     +-- ItemDetail.jsx
  |     +-- About.jsx
  |     +-- Login.jsx
  |     +-- Cart.jsx
  |     +-- NotFound.jsx
  |
  +-- context/                    Context providers
  |     +-- ThemeContext.jsx
  |     +-- AuthContext.jsx
  |
  +-- hooks/                      Custom hooks
  |     +-- useFetch.js
  |     +-- useLocalStorage.js
  |     +-- useToggle.js
  |
  +-- data/                       Mock data (if not using API)
        +-- items.js
```

### Architecture Overview

```
  APPLICATION ARCHITECTURE
  =========================

  +--------------------------------------------------+
  |                    PROVIDERS                      |
  |  BrowserRouter > ThemeProvider > AuthProvider      |
  +--------------------------------------------------+
          |
          v
  +--------------------------------------------------+
  |                    APP SHELL                      |
  |  +----------------------------------------------+|
  |  |  Navbar (NavLink, Theme Toggle, Auth Status) ||
  |  +----------------------------------------------+|
  |  |                                              ||
  |  |  +------------------------------------------+||
  |  |  |           ROUTE CONTENT                  |||
  |  |  |  (swapped by React Router)               |||
  |  |  |                                          |||
  |  |  |  Home | ItemList | ItemDetail | About    |||
  |  |  |  Login | Cart | NotFound                 |||
  |  |  +------------------------------------------+||
  |  |                                              ||
  |  +----------------------------------------------+|
  |  |  Footer                                      ||
  |  +----------------------------------------------+|
  +--------------------------------------------------+
          |                    |
          v                    v
  +----------------+  +------------------+
  | Custom Hooks   |  |  Context Values  |
  | useFetch       |  |  theme, user     |
  | useLocalStorage|  |  toggleTheme     |
  | useToggle      |  |  login, logout   |
  +----------------+  +------------------+
```

### Getting Started

1. **Create a new Vite project:** `npm create vite@latest my-project -- --template react`
2. **Install React Router:** `npm install react-router-dom`
3. **Set up your file structure** following the recommended layout above.
4. **Build in this order:**
   - Static pages first (Home, About, NotFound)
   - Navbar with routing
   - Item listing page with mock data
   - Dynamic detail page with useParams
   - Theme context
   - Custom hooks (useFetch, useLocalStorage)
   - Auth context and protected routes
   - Styling and polish

---

## 6. React Phase Summary (Weeks 16-21)

### Everything We Covered

Over the past six weeks, you have gone from zero React knowledge to building complete, multi-page, interactive web applications. Here is a recap of every major concept.

| Week | Topic                         | Key Concepts                                                         |
| ---- | ----------------------------- | -------------------------------------------------------------------- |
| 16   | Introduction to React         | Components, JSX, props, rendering, Vite setup                       |
| 17   | Props & Communication          | Props passing, children prop, conditional rendering, lists with keys |
| 18   | State Management               | useState, event handling, controlled inputs, lifting state up        |
| 19   | Side Effects & Lifecycle       | useEffect, data fetching, cleanup, useRef, component lifecycle      |
| 20   | React Router & Navigation      | BrowserRouter, Route, Link, NavLink, useParams, nested routes, protected routes |
| 21   | Advanced Patterns & Project    | useContext, custom hooks, React.memo, useMemo, useCallback          |

### React Hooks Summary

```
  ALL HOOKS COVERED (Weeks 16-21)
  =================================

  HOOK             PURPOSE                           WEEK
  ----             -------                           ----
  useState         Component state                   18
  useEffect        Side effects (fetch, timers)      19
  useRef           DOM refs, persistent values       19
  useParams        Read URL parameters               20
  useNavigate      Programmatic navigation           20
  useLocation      Current URL info                  20
  useSearchParams  URL query parameters              20
  useContext       Global state from context          21
  useMemo          Cache expensive calculations      21
  useCallback      Cache function references         21
```

### Key Patterns Learned

```
  REACT PATTERNS REFERENCE
  =========================

  1. Component Pattern:
     function MyComponent({ title, children }) {
       return <div><h1>{title}</h1>{children}</div>;
     }

  2. State Pattern:
     const [value, setValue] = useState(initialValue);

  3. Effect Pattern:
     useEffect(() => {
       // setup
       return () => { /* cleanup */ };
     }, [dependencies]);

  4. Fetch Pattern:
     useEffect(() => {
       async function load() {
         const res = await fetch(url);
         const data = await res.json();
         setData(data);
       }
       load();
     }, [url]);

  5. Routing Pattern:
     <Route path="/items/:id" element={<ItemDetail />} />
     const { id } = useParams();

  6. Context Pattern:
     const MyContext = createContext();
     <MyContext.Provider value={data}>
     const data = useContext(MyContext);

  7. Custom Hook Pattern:
     function useMyHook() {
       const [state, setState] = useState();
       useEffect(() => { ... }, []);
       return { state };
     }

  8. Protected Route Pattern:
     if (!isAuthenticated) return <Navigate to="/login" />;
     return children;
```

### What Is Next

With the React phase complete, you are now ready to move to the **backend**. Starting with Week 22, you will learn Node.js, Express.js, and MongoDB to build the server side of full-stack applications. Eventually, you will connect your React frontend to a backend API, completing the full MERN stack (MongoDB, Express, React, Node.js).
