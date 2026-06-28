# Week 19: Side Effects & Lifecycle

> **Prerequisites:** React components, JSX, props, state, and the useState hook from Weeks 16-18.

---

## Table of Contents

1. [What Are Side Effects?](#1-what-are-side-effects)
2. [useEffect Hook](#2-useeffect-hook)
3. [Fetching Data from APIs](#3-fetching-data-from-apis)
4. [Cleanup Functions](#4-cleanup-functions)
5. [useRef Hook](#5-useref-hook)
6. [Common useEffect Patterns](#6-common-useeffect-patterns)
7. [Component Lifecycle in Functional Components](#7-component-lifecycle-in-functional-components)
8. [Summary](#8-summary)

---

## 1. What Are Side Effects?

### Pure Functions vs Side Effects

To understand side effects, you first need to understand **pure functions**.

A **pure function** always produces the same output for the same input and does not affect anything outside of itself. It takes data in, processes it, and returns a result. Nothing else changes.

```javascript
// PURE FUNCTION
// Same input always gives same output. No outside interaction.
function add(a, b) {
  return a + b;
}

add(2, 3); // Always returns 5
add(2, 3); // Still returns 5. Always.
```

A **side effect** occurs when a function reaches beyond its own scope to interact with the outside world. It might read from or write to something external: the network, the browser, a database, a timer, or the DOM.

```javascript
// FUNCTION WITH SIDE EFFECTS
// It reaches outside itself to interact with the DOM and localStorage.
function saveAndDisplay(username) {
  document.title = username;                    // Side effect: modifies the DOM
  localStorage.setItem("user", username);       // Side effect: writes to browser storage
  console.log("Saved:", username);              // Side effect: writes to console
}
```

```
          PURE FUNCTION vs SIDE EFFECT

  Pure Function:                   Function with Side Effects:
  +-----------+                    +-----------+
  |           |                    |           |----> API call
  | Input --> | --> Output         | Input --> |----> DOM change
  |           |                    |           |----> localStorage
  +-----------+                    |           |----> Timer
  Nothing else                     +-----------+
  is touched.                      Reaches outside itself.
```

### Real-Life Analogy: Cooking vs Ordering Delivery

**Cooking at home** is like a pure function. You take ingredients (input), follow a recipe (process), and produce a meal (output). Everything happens inside your kitchen. Nothing external is involved.

**Ordering food delivery** is like a side effect. You pick up your phone, call a restaurant (external system), place an order (network request), wait for delivery (asynchronous), and eventually receive food. You are interacting with the outside world, and you cannot fully control the timing or outcome. The restaurant might be closed, the driver might be late, or the order might be wrong.

```
  COOKING (Pure)                    ORDERING DELIVERY (Side Effect)
  +----------+                      +----------+
  | Kitchen  |                      | You      |
  |          |                      |          |
  | eggs  ---|---> omelette         | phone ---|---> Restaurant (external)
  | salt     |                      |          |        |
  | butter   |                      |          |        v
  +----------+                      |          |<--- Delivery (async response)
  Self-contained.                   +----------+
  Predictable.                      Depends on outside world.
                                    Timing is uncertain.
```

### Common Side Effects in React

React components are meant to be pure when it comes to rendering: given the same props and state, they should produce the same JSX. But real applications need to interact with the outside world. These interactions are side effects.

| Side Effect              | Example                                          |
| ------------------------ | ------------------------------------------------ |
| **API calls**            | Fetching user data from a server                 |
| **Timers**               | setTimeout, setInterval for countdowns or delays |
| **localStorage**         | Saving user preferences in the browser           |
| **DOM manipulation**     | Changing the document title, focusing an input   |
| **Subscriptions**        | WebSocket connections, event listeners            |
| **Logging**              | Sending analytics data to a tracking service     |

**The rule:** You should never perform side effects directly inside the render logic of a component. Side effects should be handled in a controlled, predictable way. That is exactly what the `useEffect` hook is for.

---

## 2. useEffect Hook

### What Is useEffect?

`useEffect` is a React hook that lets you perform side effects in function components. It tells React: "After you finish rendering this component, run this code."

Think of it as scheduling a task that should happen after the component appears on screen or after something changes.

### Syntax

```javascript
useEffect(() => {
  // Side effect code goes here
}, [dependencies]);
```

The hook takes two arguments:

1. **Effect function** -- the code to run (the side effect itself).
2. **Dependency array** (optional) -- a list of values that the effect depends on. React uses this array to decide when to re-run the effect.

### Three Variations of useEffect

The behavior of `useEffect` changes entirely depending on what you pass as the second argument.

---

#### Variation 1: No Dependency Array -- Runs After EVERY Render

```javascript
useEffect(() => {
  console.log("I run after EVERY render");
});
```

Without a dependency array, the effect runs after the initial render and after every subsequent re-render. Every time the component updates for any reason, this effect fires.

**Real-life analogy:** A security camera that records every single movement. Every time anything happens in the room, it captures it. This is thorough but expensive. You rarely want this behavior.

**When to use:** Almost never. This is the least common variation because it runs too frequently. It can cause performance problems or infinite loops if the effect itself triggers a re-render.

```javascript
import { useState, useEffect } from "react";

function RenderCounter() {
  const [count, setCount] = useState(0);
  const [text, setText] = useState("");

  useEffect(() => {
    console.log("Component rendered! Count:", count, "Text:", text);
  });
  // No dependency array -- runs on every render

  return (
    <div>
      <p>Count: {count}</p>
      <button onClick={() => setCount(count + 1)}>Increment</button>
      <input value={text} onChange={(e) => setText(e.target.value)} />
    </div>
  );
}
```

Every button click and every keystroke in the input triggers a re-render, and the effect runs each time.

---

#### Variation 2: Empty Array [] -- Runs ONCE After Mount

```javascript
useEffect(() => {
  console.log("I run ONCE when the component mounts");
}, []);
```

With an empty dependency array, the effect runs only once, right after the component first appears on screen (mounts). It does not run again on subsequent re-renders.

**Real-life analogy:** Setting up your desk on the first day at a new job. You arrange your monitor, keyboard, and chair once. You do not rearrange everything every time you sit down. It is a one-time setup.

**When to use:** Fetching initial data from an API, setting up a subscription, reading from localStorage on component load.

```javascript
import { useState, useEffect } from "react";

function WelcomeMessage() {
  const [message, setMessage] = useState("Loading...");

  useEffect(() => {
    // This runs only once when the component first appears
    console.log("Component mounted! Fetching welcome message...");
    setMessage("Welcome to the application!");
  }, []);
  // Empty array -- runs once on mount

  return <h1>{message}</h1>;
}
```

---

#### Variation 3: With Dependencies [value] -- Runs When Dependencies Change

```javascript
useEffect(() => {
  console.log("I run when 'searchTerm' changes");
}, [searchTerm]);
```

When you provide values in the dependency array, the effect runs after the initial render and then again whenever any of those values change. React compares the current values to the previous ones. If they differ, the effect re-runs.

**Real-life analogy:** A thermostat. It does not check the temperature every second. It reacts only when the temperature changes past a threshold. It watches a specific value and responds when that value changes.

**When to use:** Reacting to state or prop changes. Searching when a query changes. Updating the document title when a page name changes.

```javascript
import { useState, useEffect } from "react";

function SearchComponent() {
  const [searchTerm, setSearchTerm] = useState("");
  const [results, setResults] = useState([]);

  useEffect(() => {
    if (searchTerm.length > 0) {
      console.log("Searching for:", searchTerm);
      // In a real app, you would fetch from an API here
      setResults([`Result for "${searchTerm}"`]);
    } else {
      setResults([]);
    }
  }, [searchTerm]);
  // Runs when searchTerm changes

  return (
    <div>
      <input
        value={searchTerm}
        onChange={(e) => setSearchTerm(e.target.value)}
        placeholder="Search..."
      />
      <ul>
        {results.map((result, index) => (
          <li key={index}>{result}</li>
        ))}
      </ul>
    </div>
  );
}
```

You can also pass multiple dependencies:

```javascript
useEffect(() => {
  console.log("Either 'page' or 'filter' changed");
  fetchProducts(page, filter);
}, [page, filter]);
// Runs when page OR filter changes
```

---

### When Does Each Variation Run?

```
  TIMELINE: Component Lifecycle with useEffect Variations
  =======================================================

  Mount          Re-render #1       Re-render #2       Unmount
  (first         (state changed)    (state changed)
  render)
    |                 |                  |                |
    v                 v                  v                v
  -----------------------------------------------------------------> Time

  No deps:        RUNS              RUNS               RUNS
  useEffect(fn)     |                 |                  |

  Empty []:       RUNS
  useEffect(fn,     |
  [])

  With [dep]:     RUNS            RUNS (if dep       RUNS (if dep
  useEffect(fn,     |             changed)           changed)
  [dep])
```

### Quick Reference Table

| Variation          | Runs on Mount? | Runs on Re-render?        | Common Use Case              |
| ------------------ | -------------- | ------------------------- | ---------------------------- |
| No dependency array | Yes           | Yes, every re-render      | Rarely used (debugging)      |
| Empty array `[]`   | Yes            | No                        | Initial data fetch, setup    |
| With deps `[a, b]` | Yes            | Only when `a` or `b` change | Reacting to specific changes |

---

## 3. Fetching Data from APIs

Fetching data from a server is the most common side effect in React applications. Users expect to see real data -- user profiles, product listings, blog posts -- and that data lives on a server. The `useEffect` hook is where you perform these network requests.

### Basic Fetch Inside useEffect

```javascript
import { useState, useEffect } from "react";

function UsersList() {
  const [users, setUsers] = useState([]);

  useEffect(() => {
    fetch("https://jsonplaceholder.typicode.com/users")
      .then((response) => response.json())
      .then((data) => setUsers(data));
  }, []);

  return (
    <ul>
      {users.map((user) => (
        <li key={user.id}>{user.name}</li>
      ))}
    </ul>
  );
}
```

This works, but it has no loading indicator and no error handling. In a real application, you need both.

### The async/await Problem

You might be tempted to write this:

```javascript
// THIS IS WRONG. Do not do this.
useEffect(async () => {
  const response = await fetch("https://jsonplaceholder.typicode.com/users");
  const data = await response.json();
  setUsers(data);
}, []);
```

**Why is this wrong?** The `useEffect` callback must return either nothing (`undefined`) or a cleanup function. An `async` function always returns a Promise. React does not know what to do with a Promise as a return value, and this causes warnings and unexpected behavior.

**The solution:** Create a separate async function inside the effect and call it immediately.

```javascript
useEffect(() => {
  async function fetchUsers() {
    const response = await fetch("https://jsonplaceholder.typicode.com/users");
    const data = await response.json();
    setUsers(data);
  }

  fetchUsers();
}, []);
```

### Complete Example: Loading State, Error State, and Data

A production-quality data fetch handles three states: loading, error, and success.

```
  DATA FETCHING FLOW
  ==================

  Component Mounts
        |
        v
  +-------------+
  | loading:    |     "Loading..." shown on screen
  | true        |
  +-------------+
        |
        v
  +-----------+
  | fetch()   |----> Network Request to API
  +-----------+
        |
       / \
      /   \
     v     v
  Success    Failure
     |         |
     v         v
  +--------+  +--------+
  | Store  |  | Store  |
  | data   |  | error  |
  | in     |  | message|
  | state  |  | in     |
  +--------+  | state  |
     |        +--------+
     v           |
  +--------+    v
  | Render |  +--------+
  | the    |  | Render |
  | data   |  | error  |
  +--------+  +--------+
```

```javascript
import { useState, useEffect } from "react";

function UsersList() {
  const [users, setUsers] = useState([]);
  const [loading, setLoading] = useState(true);
  const [error, setError] = useState(null);

  useEffect(() => {
    async function fetchUsers() {
      try {
        const response = await fetch(
          "https://jsonplaceholder.typicode.com/users"
        );

        if (!response.ok) {
          throw new Error(`HTTP error! Status: ${response.status}`);
        }

        const data = await response.json();
        setUsers(data);
      } catch (err) {
        setError(err.message);
      } finally {
        setLoading(false);
      }
    }

    fetchUsers();
  }, []);

  // LOADING STATE
  if (loading) {
    return <p>Loading users...</p>;
  }

  // ERROR STATE
  if (error) {
    return <p style={{ color: "red" }}>Error: {error}</p>;
  }

  // SUCCESS STATE
  return (
    <div>
      <h2>Users</h2>
      <ul>
        {users.map((user) => (
          <li key={user.id}>
            <strong>{user.name}</strong> - {user.email}
          </li>
        ))}
      </ul>
    </div>
  );
}

export default UsersList;
```

### Breaking Down the Pattern

| State Variable | Purpose                          | Initial Value |
| -------------- | -------------------------------- | ------------- |
| `users`        | Stores the fetched data          | `[]`          |
| `loading`      | Tracks whether data is loading   | `true`        |
| `error`        | Stores the error message, if any | `null`        |

**Why start `loading` as `true`?** Because the fetch starts immediately on mount. The component is in a loading state from the very beginning until the fetch completes.

**Why use `try/catch/finally`?**
- `try` runs the fetch. If anything goes wrong, execution jumps to `catch`.
- `catch` stores the error message in state.
- `finally` runs regardless of success or failure and sets loading to `false`.

### Fetching Data Based on User Input

Sometimes you need to re-fetch data when a value changes. Use that value as a dependency.

```javascript
import { useState, useEffect } from "react";

function UserProfile({ userId }) {
  const [user, setUser] = useState(null);
  const [loading, setLoading] = useState(true);

  useEffect(() => {
    setLoading(true);

    async function fetchUser() {
      try {
        const response = await fetch(
          `https://jsonplaceholder.typicode.com/users/${userId}`
        );
        const data = await response.json();
        setUser(data);
      } catch (err) {
        console.error("Failed to fetch user:", err);
      } finally {
        setLoading(false);
      }
    }

    fetchUser();
  }, [userId]);
  // Re-fetches whenever userId changes

  if (loading) return <p>Loading...</p>;
  if (!user) return <p>No user found.</p>;

  return (
    <div>
      <h2>{user.name}</h2>
      <p>Email: {user.email}</p>
      <p>Phone: {user.phone}</p>
    </div>
  );
}
```

When `userId` changes (for example, when a parent component passes a different user ID), the effect re-runs and fetches the new user's data.

---

## 4. Cleanup Functions

### What Is Cleanup and Why Is It Needed?

Some side effects create ongoing processes: timers that keep ticking, event listeners that keep listening, WebSocket connections that stay open. If the component that created these processes is removed from the screen (unmounts) or the effect re-runs, those processes do not automatically stop. They keep running in the background, consuming memory and potentially causing errors.

This is called a **memory leak**. The process keeps holding onto memory and resources even though nothing needs it anymore.

**Real-life analogy: Cleaning your desk before leaving the office.** When you leave work, you turn off your desk lamp, close your laptop, and put away your files. If you do not, the lamp stays on wasting electricity, the laptop stays running wasting battery, and papers pile up until the desk is unusable. Cleanup is about being responsible: when you are done, you undo what you set up.

```
  WITHOUT CLEANUP                        WITH CLEANUP
  ================                       =============

  Mount:                                 Mount:
  Start timer every 1s                   Start timer every 1s
       |                                      |
       v                                      v
  Unmount:                               Unmount:
  Component removed                      Component removed
  Timer keeps running!                   Cleanup: clearInterval()
  Still updating state!                  Timer stopped cleanly.
  Error: "Can't update                   No errors.
  state on unmounted                     No wasted resources.
  component"
       |
       v
  MEMORY LEAK
```

### Returning a Cleanup Function from useEffect

To perform cleanup, you return a function from inside `useEffect`. React will call this returned function:

1. **Before the effect re-runs** (if dependencies changed).
2. **When the component unmounts** (is removed from the screen).

```javascript
useEffect(() => {
  // SETUP: start the side effect
  const intervalId = setInterval(() => {
    console.log("Tick");
  }, 1000);

  // CLEANUP: stop the side effect
  return () => {
    clearInterval(intervalId);
    console.log("Timer cleared!");
  };
}, []);
```

### Use Case 1: Clearing Timers

Timers are the most straightforward example. If you start an interval, you must clear it.

```javascript
import { useState, useEffect } from "react";

function StopWatch() {
  const [seconds, setSeconds] = useState(0);

  useEffect(() => {
    const intervalId = setInterval(() => {
      setSeconds((prev) => prev + 1);
    }, 1000);

    // Cleanup: stop the timer when component unmounts
    return () => {
      clearInterval(intervalId);
    };
  }, []);

  return <p>Time elapsed: {seconds} seconds</p>;
}
```

If `StopWatch` is removed from the screen without the cleanup function, the `setInterval` would keep running and trying to call `setSeconds` on a component that no longer exists. The cleanup prevents this.

### Use Case 2: Removing Event Listeners

If you add a global event listener (like listening for keyboard presses or window resizing), you must remove it when the component is done.

```javascript
import { useState, useEffect } from "react";

function WindowWidth() {
  const [width, setWidth] = useState(window.innerWidth);

  useEffect(() => {
    function handleResize() {
      setWidth(window.innerWidth);
    }

    // SETUP: add the listener
    window.addEventListener("resize", handleResize);

    // CLEANUP: remove the listener
    return () => {
      window.removeEventListener("resize", handleResize);
    };
  }, []);

  return <p>Window width: {width}px</p>;
}
```

Without cleanup, every time this component mounts and unmounts, a new `resize` listener would be added but never removed. After mounting 10 times, there would be 10 listeners all firing on every resize.

### Use Case 3: Canceling Subscriptions and Aborting Fetch Requests

You can use the browser's `AbortController` to cancel a fetch request if the component unmounts before the response arrives.

```javascript
import { useState, useEffect } from "react";

function UserData({ userId }) {
  const [user, setUser] = useState(null);

  useEffect(() => {
    const controller = new AbortController();

    async function fetchUser() {
      try {
        const response = await fetch(
          `https://jsonplaceholder.typicode.com/users/${userId}`,
          { signal: controller.signal }
        );
        const data = await response.json();
        setUser(data);
      } catch (err) {
        if (err.name !== "AbortError") {
          console.error("Fetch failed:", err);
        }
      }
    }

    fetchUser();

    // CLEANUP: cancel the request if component unmounts
    // or if userId changes before the response arrives
    return () => {
      controller.abort();
    };
  }, [userId]);

  if (!user) return <p>Loading...</p>;
  return <p>{user.name}</p>;
}
```

### Cleanup Timing Summary

```
  CLEANUP TIMING
  ==============

  First render:
    1. Component renders
    2. useEffect runs (SETUP)

  Dependency changes (re-render):
    1. Component re-renders
    2. CLEANUP from previous effect runs
    3. New useEffect runs (SETUP)

  Unmount:
    1. CLEANUP from last effect runs
    2. Component removed from screen
```

| Scenario                 | Does Cleanup Run? | When?                          |
| ------------------------ | ----------------- | ------------------------------ |
| Component mounts         | No                | --                             |
| Dependency changes       | Yes               | Before new effect runs         |
| Component unmounts       | Yes               | Right before removal from DOM  |

---

## 5. useRef Hook

### What Is useRef?

`useRef` is a React hook that creates a container (called a "ref") that can hold any value. This container has two important properties:

1. **Its value persists across renders.** Unlike a regular variable that resets every time the component re-renders, a ref keeps its value.
2. **Changing its value does NOT cause a re-render.** Unlike `useState`, updating a ref is silent. React does not re-render the component when a ref changes.

### Syntax

```javascript
import { useRef } from "react";

const myRef = useRef(initialValue);

// Access the value:
console.log(myRef.current); // initialValue

// Update the value:
myRef.current = newValue;
```

The value is always stored in the `.current` property.

```
  useRef STRUCTURE
  ================

  const myRef = useRef(42);

  +------------------+
  |   myRef          |
  |                  |
  |  .current: 42   |    <-- The value lives here
  |                  |
  +------------------+

  myRef.current = 100;    <-- You update it directly
                              No re-render happens!
```

### Use Case 1: Accessing DOM Elements Directly

The most common use of `useRef` is to get a direct reference to a DOM element. You attach the ref to a JSX element using the `ref` attribute, and React will set `ref.current` to the actual DOM node.

```javascript
import { useRef } from "react";

function FocusInput() {
  const inputRef = useRef(null);

  function handleClick() {
    // Directly access the DOM element and focus it
    inputRef.current.focus();
  }

  return (
    <div>
      <input ref={inputRef} placeholder="Click the button to focus me" />
      <button onClick={handleClick}>Focus the Input</button>
    </div>
  );
}
```

**How it works:**

1. `useRef(null)` creates a ref with an initial value of `null`.
2. `ref={inputRef}` tells React to attach this ref to the `<input>` element.
3. After the component renders, `inputRef.current` points to the actual `<input>` DOM node.
4. `inputRef.current.focus()` calls the browser's native `.focus()` method on that input.

### Use Case 2: Storing Previous Values

Sometimes you need to know what a value was during the previous render. `useRef` is perfect for this because it does not cause a re-render when updated.

```javascript
import { useState, useEffect, useRef } from "react";

function Counter() {
  const [count, setCount] = useState(0);
  const prevCountRef = useRef(0);

  useEffect(() => {
    // After each render, store the current count as the "previous" value
    prevCountRef.current = count;
  });

  return (
    <div>
      <p>Current count: {count}</p>
      <p>Previous count: {prevCountRef.current}</p>
      <button onClick={() => setCount(count + 1)}>Increment</button>
    </div>
  );
}
```

**How it works:**

1. The component renders with `count = 0`. At this point, `prevCountRef.current` is still `0`.
2. After the render, the `useEffect` runs and stores `count` (0) in `prevCountRef.current`.
3. When the user clicks the button, `count` becomes `1`. The component re-renders.
4. During this render, `prevCountRef.current` is still `0` (the value from last render). So "Previous count: 0" is displayed.
5. After this render, the effect runs again and stores `1` in `prevCountRef.current`.

The ref always holds the value from one render behind.

### Use Case 3: Storing Mutable Values That Do Not Need Re-render

If you need a value to persist between renders but changing it should not trigger a re-render, use a ref instead of state.

```javascript
import { useState, useEffect, useRef } from "react";

function StopWatch() {
  const [seconds, setSeconds] = useState(0);
  const [isRunning, setIsRunning] = useState(false);
  const intervalRef = useRef(null);

  function start() {
    if (!isRunning) {
      setIsRunning(true);
      intervalRef.current = setInterval(() => {
        setSeconds((prev) => prev + 1);
      }, 1000);
    }
  }

  function stop() {
    clearInterval(intervalRef.current);
    setIsRunning(false);
  }

  function reset() {
    clearInterval(intervalRef.current);
    setIsRunning(false);
    setSeconds(0);
  }

  // Cleanup on unmount
  useEffect(() => {
    return () => clearInterval(intervalRef.current);
  }, []);

  return (
    <div>
      <p>{seconds} seconds</p>
      <button onClick={start}>Start</button>
      <button onClick={stop}>Stop</button>
      <button onClick={reset}>Reset</button>
    </div>
  );
}
```

Here, `intervalRef` stores the timer ID. We need this ID to clear the interval later, but changing it should not re-render the component. A ref is the right choice. If we used `useState` for the timer ID, changing it would trigger an unnecessary re-render.

### useRef vs useState Comparison

| Feature                      | useState                       | useRef                          |
| ---------------------------- | ------------------------------ | ------------------------------- |
| **Causes re-render on change** | Yes                          | No                              |
| **Persists between renders** | Yes                            | Yes                             |
| **Access syntax**            | `value`                        | `ref.current`                   |
| **Update syntax**            | `setValue(newValue)`           | `ref.current = newValue`        |
| **Triggers UI update**       | Yes                            | No                              |
| **Common use**               | Data that the UI displays      | DOM refs, timer IDs, previous values |
| **Updated during render?**   | Via setter function only       | Directly (but avoid during render) |

**Rule of thumb:** If the value needs to appear on screen, use `useState`. If the value is just for internal bookkeeping, use `useRef`.

---

## 6. Common useEffect Patterns

### Pattern 1: Debouncing Search Input

When a user types in a search box, you do not want to fire an API request on every single keystroke. That would flood the server with requests. Instead, wait until the user stops typing for a short period (for example, 500 milliseconds) and then search. This is called **debouncing**.

```javascript
import { useState, useEffect } from "react";

function SearchBar() {
  const [query, setQuery] = useState("");
  const [results, setResults] = useState([]);

  useEffect(() => {
    if (query.length === 0) {
      setResults([]);
      return;
    }

    // Set a timer: only search after 500ms of no typing
    const timerId = setTimeout(() => {
      console.log("Searching for:", query);
      // Replace with actual API call
      fetch(`https://jsonplaceholder.typicode.com/users?q=${query}`)
        .then((res) => res.json())
        .then((data) => setResults(data));
    }, 500);

    // CLEANUP: if the user types again before 500ms, cancel the old timer
    return () => clearTimeout(timerId);
  }, [query]);

  return (
    <div>
      <input
        value={query}
        onChange={(e) => setQuery(e.target.value)}
        placeholder="Search users..."
      />
      <ul>
        {results.map((user) => (
          <li key={user.id}>{user.name}</li>
        ))}
      </ul>
    </div>
  );
}
```

**How debouncing works here:**

1. User types "J" -- a timer is set for 500ms.
2. User types "Jo" (within 500ms) -- cleanup cancels the old timer, a new timer is set.
3. User types "Joh" (within 500ms) -- cleanup cancels again, new timer set.
4. User stops typing. 500ms passes. The timer fires and the search runs for "Joh".

```
  DEBOUNCING TIMELINE
  ===================

  User types:  J        Jo       Joh      John     (stops)
  Time:        0ms      100ms    200ms    350ms    850ms (350+500)
               |         |        |        |           |
               v         v        v        v           v
  Timer:     set 500ms  cancel   cancel   cancel     FIRES!
                        set new  set new  set new    Search: "John"
```

### Pattern 2: Setting Document Title

Update the browser tab title to reflect the current page or content.

```javascript
import { useState, useEffect } from "react";

function NotesApp() {
  const [noteTitle, setNoteTitle] = useState("Untitled");

  useEffect(() => {
    document.title = `${noteTitle} - Notes App`;
  }, [noteTitle]);

  return (
    <input
      value={noteTitle}
      onChange={(e) => setNoteTitle(e.target.value)}
      placeholder="Enter note title"
    />
  );
}
```

Every time `noteTitle` changes, the browser tab title updates to match. If the user types "Meeting Notes", the tab shows "Meeting Notes - Notes App".

### Pattern 3: Listening to Window Resize

Track the window dimensions and respond to changes.

```javascript
import { useState, useEffect } from "react";

function ResponsiveLayout() {
  const [windowSize, setWindowSize] = useState({
    width: window.innerWidth,
    height: window.innerHeight,
  });

  useEffect(() => {
    function handleResize() {
      setWindowSize({
        width: window.innerWidth,
        height: window.innerHeight,
      });
    }

    window.addEventListener("resize", handleResize);

    return () => window.removeEventListener("resize", handleResize);
  }, []);

  return (
    <div>
      <p>
        Window: {windowSize.width} x {windowSize.height}
      </p>
      {windowSize.width < 768 ? (
        <p>Mobile layout active</p>
      ) : (
        <p>Desktop layout active</p>
      )}
    </div>
  );
}
```

### Pattern 4: Syncing with localStorage

Save user preferences to `localStorage` so they persist across page reloads.

```javascript
import { useState, useEffect } from "react";

function ThemeSwitcher() {
  // Initialize state from localStorage (or default to "light")
  const [theme, setTheme] = useState(() => {
    return localStorage.getItem("theme") || "light";
  });

  // Sync to localStorage whenever theme changes
  useEffect(() => {
    localStorage.setItem("theme", theme);
    document.body.className = theme;
    console.log("Theme saved to localStorage:", theme);
  }, [theme]);

  return (
    <button onClick={() => setTheme(theme === "light" ? "dark" : "light")}>
      Switch to {theme === "light" ? "Dark" : "Light"} Mode
    </button>
  );
}
```

**Key detail:** The initial state uses a function `() => localStorage.getItem("theme") || "light"` rather than calling `localStorage.getItem` directly. This is called **lazy initialization**. The function runs only once during the first render, which is more efficient than reading from localStorage on every render.

---

## 7. Component Lifecycle in Functional Components

### What Is a Component Lifecycle?

Every React component goes through three phases during its existence:

1. **Mount** -- The component is created and inserted into the DOM for the first time.
2. **Update** -- The component re-renders because its state or props changed.
3. **Unmount** -- The component is removed from the DOM.

```
  COMPONENT LIFECYCLE
  ====================

  +-------------------+
  |                   |
  |      MOUNT        |    Component appears on screen
  |  (first render)   |    - Initial state is set
  |                   |    - JSX is rendered to DOM
  |                   |    - useEffect with [] runs
  +-------------------+
           |
           v
  +-------------------+
  |                   |
  |      UPDATE       |    Component re-renders
  |  (re-renders)     |    - State or props changed
  |                   |    - New JSX is rendered
  |                   |    - useEffect with [deps] runs
  |   (can happen     |      (if deps changed)
  |    many times)    |
  +-------------------+
           |
           v
  +-------------------+
  |                   |
  |     UNMOUNT       |    Component removed from screen
  |  (removal)        |    - Cleanup functions run
  |                   |    - Event listeners removed
  |                   |    - Timers cleared
  +-------------------+
```

### How useEffect Maps to Lifecycle Phases

```
  useEffect AND LIFECYCLE MAPPING
  ================================

  PHASE        useEffect CODE                  WHEN IT RUNS
  -----        ---------------                 ------------

  Mount        useEffect(() => {               After first render
                 // setup code
               }, []);

  Update       useEffect(() => {               After re-render
                 // runs when deps change       (when deps changed)
               }, [dep1, dep2]);

  Unmount      useEffect(() => {               When component is
                 return () => {                 removed from DOM
                   // cleanup code
                 };
               }, []);
```

A single `useEffect` can handle all three phases:

```javascript
useEffect(() => {
  // --- MOUNT / UPDATE ---
  // This code runs after mount and after every update
  // (when dependencies change)
  console.log("Component mounted or updated");

  const subscription = subscribeToData();

  // --- UNMOUNT / BEFORE RE-RUN ---
  // This cleanup code runs before the effect re-runs
  // and when the component unmounts
  return () => {
    console.log("Cleaning up before next effect or unmount");
    subscription.unsubscribe();
  };
}, [someDependency]);
```

### Comparison with Class Component Lifecycle (Brief Reference)

Before hooks, React used class components with named lifecycle methods. You may encounter these in older codebases or tutorials. Here is how they map to hooks.

| Class Component Method   | Functional Component Equivalent     | When It Runs                          |
| ------------------------ | ----------------------------------- | ------------------------------------- |
| `componentDidMount()`    | `useEffect(() => {}, [])`           | Once, after first render              |
| `componentDidUpdate()`   | `useEffect(() => {}, [deps])`       | After re-render when deps change      |
| `componentWillUnmount()` | `return () => {}` inside useEffect  | When component is removed             |
| `this.state`             | `useState()`                        | Managing component state              |
| `this.refs`              | `useRef()`                          | Accessing DOM elements or storing values |

**Example comparison:**

```javascript
// CLASS COMPONENT (old approach -- for reference only)
class Timer extends React.Component {
  state = { seconds: 0 };

  componentDidMount() {
    this.intervalId = setInterval(() => {
      this.setState((prev) => ({ seconds: prev.seconds + 1 }));
    }, 1000);
  }

  componentWillUnmount() {
    clearInterval(this.intervalId);
  }

  render() {
    return <p>{this.state.seconds} seconds</p>;
  }
}
```

```javascript
// FUNCTIONAL COMPONENT (modern approach)
function Timer() {
  const [seconds, setSeconds] = useState(0);

  useEffect(() => {
    const intervalId = setInterval(() => {
      setSeconds((prev) => prev + 1);
    }, 1000);

    return () => clearInterval(intervalId);
  }, []);

  return <p>{seconds} seconds</p>;
}
```

The functional version is shorter, all related logic (setup and cleanup) lives together in one `useEffect` block, and there is no `this` keyword to worry about.

### Full Lifecycle Diagram with useEffect

```
  COMPLETE LIFECYCLE WITH useEffect
  ==================================

  Component Created
        |
        v
  +--------------+
  | First Render |  React runs the component function.
  | (Mount)      |  JSX is calculated and DOM is updated.
  +--------------+
        |
        v
  +--------------+
  | useEffect    |  Effects run AFTER the browser paints.
  | (setup)      |  API calls, subscriptions, timers start here.
  +--------------+
        |
        v
  +--------------+
  | User         |  User clicks a button, types in an input,
  | Interaction  |  or a parent re-renders with new props.
  +--------------+
        |
        v
  +--------------+
  | State/Props  |  React detects the change and schedules
  | Change       |  a re-render.
  +--------------+
        |
        v
  +--------------+
  | Re-render    |  Component function runs again with new values.
  | (Update)     |  New JSX is calculated, DOM is updated.
  +--------------+
        |
        v
  +--------------+
  | Cleanup      |  If the effect has dependencies that changed,
  | (previous    |  React runs the PREVIOUS cleanup function first.
  |  effect)     |
  +--------------+
        |
        v
  +--------------+
  | useEffect    |  Then the new effect runs with the new values.
  | (new setup)  |
  +--------------+
        |
        v
      (cycle repeats for each update)
        |
        v
  +--------------+
  | Component    |  The component is removed from the screen
  | Unmounts     |  (e.g., navigating to a different page).
  +--------------+
        |
        v
  +--------------+
  | Final        |  React runs the cleanup function one last time
  | Cleanup      |  to prevent memory leaks.
  +--------------+
```

---

## 8. Summary

### What We Covered

This week introduced the tools React provides for interacting with the outside world and managing component lifecycle.

| Concept                | Key Takeaway                                                              |
| ---------------------- | ------------------------------------------------------------------------- |
| **Side Effects**       | Any interaction with the outside world (APIs, DOM, timers, storage)       |
| **useEffect**          | The hook for scheduling side effects after render                         |
| **Dependency Array**   | Controls when the effect runs: every render, once, or on specific changes |
| **Data Fetching**      | Use async functions inside useEffect with loading and error states        |
| **Cleanup Functions**  | Prevent memory leaks by undoing setup (timers, listeners, subscriptions)  |
| **useRef**             | A persistent container that does not trigger re-renders                   |
| **Component Lifecycle** | Mount, Update, Unmount -- managed through useEffect in functional components |

### useEffect Quick Reference

```javascript
// Run once on mount
useEffect(() => {
  fetchData();
}, []);

// Run when a value changes
useEffect(() => {
  searchUsers(query);
}, [query]);

// Run with cleanup
useEffect(() => {
  const id = setInterval(tick, 1000);
  return () => clearInterval(id);
}, []);

// Run on every render (rarely needed)
useEffect(() => {
  console.log("Rendered");
});
```

### useRef Quick Reference

```javascript
// Reference a DOM element
const inputRef = useRef(null);
<input ref={inputRef} />;
inputRef.current.focus();

// Store a value without re-rendering
const countRef = useRef(0);
countRef.current += 1;
```

### Common Mistakes to Avoid

| Mistake                               | Problem                                  | Solution                                    |
| ------------------------------------- | ---------------------------------------- | ------------------------------------------- |
| Making useEffect callback async       | Returns a Promise instead of cleanup     | Create an inner async function              |
| Missing dependency array              | Effect runs on every render              | Add `[]` or `[deps]`                        |
| Missing dependencies in the array     | Effect uses stale values                 | Include all values the effect reads         |
| No cleanup for timers/listeners       | Memory leaks                             | Return a cleanup function                   |
| Setting state in effect without deps  | Infinite re-render loop                  | Add proper dependencies                     |
| Using useRef value in render for UI   | UI does not update when ref changes      | Use useState for values shown on screen     |

### What Is Next

In Week 20, we will use React Router to add navigation and multiple pages to our React applications. The concepts from this week -- especially `useEffect` for data fetching and cleanup -- will be essential as we build components that load data when users navigate between pages.
