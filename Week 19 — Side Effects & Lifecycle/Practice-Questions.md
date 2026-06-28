# Week 19 — Side Effects & Lifecycle: Practice Questions

**Total Questions: 23** (10 MCQs + 5 Short Answer + 8 Coding Exercises)

---

## Part 1: Multiple Choice Questions (MCQs)

**1. What is the purpose of `useEffect` in React?**

- A) To manage component state
- B) To perform side effects such as data fetching, subscriptions, or DOM manipulation
- C) To create new components dynamically
- D) To define CSS styles for a component

<details>
<summary>Answer</summary>

**B) To perform side effects such as data fetching, subscriptions, or DOM manipulation**

`useEffect` is a React hook that lets you synchronize a component with external systems. Side effects include fetching data from an API, subscribing to events, setting up timers, directly manipulating the DOM, and interacting with browser APIs like `localStorage`.
</details>

---

**2. When does a `useEffect` with an empty dependency array (`[]`) run?**

- A) On every render
- B) Only once, after the initial render
- C) Only when props change
- D) Before the component mounts

<details>
<summary>Answer</summary>

**B) Only once, after the initial render**

An empty dependency array tells React that the effect does not depend on any state or props, so it only needs to run once after the component first renders. This is the equivalent of the `componentDidMount` lifecycle method in class components.
</details>

---

**3. What happens when you omit the dependency array from `useEffect`?**

```jsx
useEffect(() => {
  console.log("Effect ran");
});
```

- A) The effect never runs
- B) The effect runs only once
- C) The effect runs after every render
- D) The effect runs only when state changes

<details>
<summary>Answer</summary>

**C) The effect runs after every render**

When no dependency array is provided, the effect runs after the initial render and after every subsequent re-render. This is rarely what you want and can lead to performance issues or infinite loops if the effect updates state.
</details>

---

**4. What is the purpose of the cleanup function returned from `useEffect`?**

```jsx
useEffect(() => {
  const timer = setInterval(() => console.log("tick"), 1000);
  return () => clearInterval(timer); // Cleanup function
}, []);
```

- A) To initialize the effect
- B) To run additional logic after the effect
- C) To clean up resources (timers, subscriptions, event listeners) when the component unmounts or before the effect re-runs
- D) To handle errors in the effect

<details>
<summary>Answer</summary>

**C) To clean up resources (timers, subscriptions, event listeners) when the component unmounts or before the effect re-runs**

The cleanup function prevents memory leaks and stale behavior. It runs when the component is removed from the DOM (unmount) and before each re-execution of the effect if the dependencies change. Common use cases include clearing intervals, removing event listeners, canceling network requests, and unsubscribing from data sources.
</details>

---

**5. What is the difference between `useRef` and `useState`?**

- A) `useRef` triggers a re-render when updated; `useState` does not
- B) `useRef` holds a mutable value that does NOT trigger a re-render; `useState` triggers a re-render when updated
- C) `useRef` can only hold DOM elements; `useState` can hold any value
- D) There is no difference; they are interchangeable

<details>
<summary>Answer</summary>

**B) `useRef` holds a mutable value that does NOT trigger a re-render; `useState` triggers a re-render when updated**

`useRef` returns an object with a `.current` property that persists across renders but does not cause re-renders when changed. It is commonly used to reference DOM elements and to store mutable values (like previous state, timer IDs, or counters) that should not trigger UI updates.
</details>

---

**6. What is the correct way to fetch data inside `useEffect`?**

- A)
```jsx
useEffect(async () => {
  const data = await fetch("/api/users");
}, []);
```

- B)
```jsx
useEffect(() => {
  async function fetchData() {
    const response = await fetch("/api/users");
    const data = await response.json();
    setUsers(data);
  }
  fetchData();
}, []);
```

- C)
```jsx
const data = useEffect(() => fetch("/api/users"), []);
```

- D)
```jsx
useEffect(() => {
  return await fetch("/api/users");
}, []);
```

<details>
<summary>Answer</summary>

**B)**
```jsx
useEffect(() => {
  async function fetchData() {
    const response = await fetch("/api/users");
    const data = await response.json();
    setUsers(data);
  }
  fetchData();
}, []);
```

The `useEffect` callback itself cannot be `async` because the return value of `useEffect` must be either `undefined` or a cleanup function (not a Promise). The solution is to define an `async` function inside the effect and then call it immediately.
</details>

---

**7. What is the output of the following code?**

```jsx
function App() {
  const [count, setCount] = useState(0);

  useEffect(() => {
    console.log("A: Effect ran");
    return () => console.log("B: Cleanup ran");
  }, [count]);

  return <button onClick={() => setCount(count + 1)}>Click</button>;
}
```

*After the initial render, then clicking the button once:*

- A) `A: Effect ran` then `A: Effect ran`
- B) `A: Effect ran` then `B: Cleanup ran` then `A: Effect ran`
- C) `B: Cleanup ran` then `A: Effect ran`
- D) `A: Effect ran` only

<details>
<summary>Answer</summary>

**B) `A: Effect ran` then `B: Cleanup ran` then `A: Effect ran`**

On initial render, the effect runs and logs `"A: Effect ran"`. When the button is clicked and `count` changes, React first runs the cleanup function from the previous effect (`"B: Cleanup ran"`), then runs the effect again with the new value (`"A: Effect ran"`). This cleanup-before-re-run pattern ensures resources from the previous effect are properly released.
</details>

---

**8. Which dependency array configuration should you use to run an effect only when the `userId` prop changes?**

- A) `useEffect(() => { ... });`
- B) `useEffect(() => { ... }, []);`
- C) `useEffect(() => { ... }, [userId]);`
- D) `useEffect(() => { ... }, [userId, setUserId]);`

<details>
<summary>Answer</summary>

**C) `useEffect(() => { ... }, [userId]);`**

By including `userId` in the dependency array, the effect will run on the initial render and then re-run only when `userId` changes. Option A runs on every render, option B runs only once, and option D is incorrect because setter functions from `useState` are stable references and do not need to be included (though including them is harmless).
</details>

---

**9. What is a common cause of infinite loops with `useEffect`?**

- A) Using an empty dependency array
- B) Updating state inside `useEffect` without proper dependencies, causing continuous re-renders
- C) Returning a cleanup function
- D) Using multiple `useEffect` hooks in the same component

<details>
<summary>Answer</summary>

**B) Updating state inside `useEffect` without proper dependencies, causing continuous re-renders**

An infinite loop occurs when an effect updates state, which triggers a re-render, which triggers the effect again. For example, omitting the dependency array while setting state inside the effect will cause an infinite loop. Another common case is including an object or array in the dependency array that is recreated on every render, causing the effect to see a "new" dependency each time.
</details>

---

**10. How do you access a DOM element directly in React?**

- A) `document.getElementById("myElement")`
- B) Using `useRef` and attaching the ref to the element
- C) Using `useState` to store the element
- D) Using `useEffect` to query the DOM

<details>
<summary>Answer</summary>

**B) Using `useRef` and attaching the ref to the element**

The React way to access DOM elements directly is through refs:

```jsx
const inputRef = useRef(null);

// Later in JSX:
<input ref={inputRef} />

// Access the DOM element:
inputRef.current.focus();
```

While `document.getElementById()` works, it breaks React's declarative model and can cause issues with server-side rendering and testing. `useRef` is the idiomatic approach.
</details>

---

## Part 2: Short Answer Questions

**1. Explain the three variations of the `useEffect` dependency array and when to use each.**

<details>
<summary>Answer</summary>

The dependency array controls when the effect re-runs:

**No dependency array** -- `useEffect(() => { ... })`: The effect runs after every render (initial and subsequent). Use this rarely; it is appropriate when you need to synchronize with something after every single render, but it can cause performance issues.

**Empty dependency array** -- `useEffect(() => { ... }, [])`: The effect runs only once, after the initial render, and the cleanup runs when the component unmounts. Use this for one-time setup operations like fetching initial data, setting up a WebSocket connection, or adding a global event listener.

**With specific dependencies** -- `useEffect(() => { ... }, [dep1, dep2])`: The effect runs after the initial render and again whenever any listed dependency changes. Use this when the effect depends on specific state or prop values, such as fetching new data when a query parameter changes or updating the document title based on a state value.
</details>

---

**2. What are cleanup functions in `useEffect`, and why are they important?**

<details>
<summary>Answer</summary>

A cleanup function is the function returned from a `useEffect` callback. It runs in two situations: (1) before the effect re-runs when dependencies change, and (2) when the component unmounts (is removed from the DOM).

Cleanup functions are important because they prevent memory leaks and stale behavior. Without cleanup, resources like intervals, timeouts, event listeners, and active network requests would continue running even after the component is no longer on screen. This can cause errors (updating state on an unmounted component), memory leaks (event listeners accumulating over time), and unexpected behavior (stale data from outdated requests).

Common cleanup examples include `clearInterval` and `clearTimeout` for timers, `removeEventListener` for event listeners, `controller.abort()` for fetch requests using `AbortController`, and unsubscribe functions for data subscriptions.
</details>

---

**3. What is the difference between `useRef` and `useState`, and when would you choose `useRef`?**

<details>
<summary>Answer</summary>

Both `useRef` and `useState` persist values across renders, but they differ in a critical way: updating a `useState` value triggers a re-render, while updating `useRef.current` does not.

Choose `useRef` when you need to store a value that should persist across renders but should not trigger a re-render when changed. Common use cases include: holding a reference to a DOM element (for focusing an input, measuring dimensions, or scrolling), storing timer IDs that need to be cleared later, keeping track of the previous value of a prop or state, counting renders without causing additional renders, and holding any mutable value that is not part of the rendered output.

Choose `useState` when the value is part of the component's visual output and the UI should update when it changes.
</details>

---

**4. Why can you not make the `useEffect` callback function `async` directly?**

<details>
<summary>Answer</summary>

The `useEffect` callback must return either `undefined` (no return statement) or a cleanup function. An `async` function always returns a Promise, so making the callback `async` would mean `useEffect` receives a Promise as its return value instead of a cleanup function. React would not know how to handle this and it would not execute the cleanup properly.

The solution is to define an `async` function inside the effect and call it immediately:

```jsx
useEffect(() => {
  async function fetchData() {
    const response = await fetch("/api/data");
    const data = await response.json();
    setData(data);
  }
  fetchData();
}, []);
```

This way, the outer function remains synchronous and can optionally return a cleanup function, while the inner function handles the asynchronous logic.
</details>

---

**5. What are side effects in React, and why do they need special handling?**

<details>
<summary>Answer</summary>

Side effects are any operations that interact with the outside world or affect something outside the scope of the current function. In React, this includes data fetching from APIs, subscribing to event listeners or WebSockets, manually modifying the DOM, setting timers (`setTimeout`, `setInterval`), reading from or writing to `localStorage`, and logging.

Side effects need special handling because React's rendering process should be pure -- a component should be a function of its props and state that produces JSX output without causing observable changes elsewhere. If side effects ran during rendering, they could execute multiple times (due to React's concurrent features and strict mode), run at unpredictable times, and cause inconsistencies between the UI and external systems.

`useEffect` provides a controlled mechanism for running side effects after the render is committed to the screen, with dependency tracking to control when effects re-run and cleanup functions to prevent resource leaks.
</details>

---

## Part 3: Coding Exercises

**Exercise 1: Fetch and Display Users from API**

Fetch a list of users from `https://jsonplaceholder.typicode.com/users` and display them. Handle loading and error states.

<details>
<summary>Solution</summary>

```jsx
import { useState, useEffect } from "react";

function UserDirectory() {
  const [users, setUsers] = useState([]);
  const [loading, setLoading] = useState(true);
  const [error, setError] = useState(null);

  useEffect(() => {
    async function fetchUsers() {
      try {
        const response = await fetch("https://jsonplaceholder.typicode.com/users");

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

  if (loading) {
    return <p className="loading">Loading users...</p>;
  }

  if (error) {
    return <p className="error">Error: {error}</p>;
  }

  return (
    <div className="user-directory">
      <h2>User Directory ({users.length} users)</h2>
      <div className="user-grid">
        {users.map((user) => (
          <div key={user.id} className="user-card">
            <h3>{user.name}</h3>
            <p>Username: {user.username}</p>
            <p>Email: {user.email}</p>
            <p>City: {user.address.city}</p>
            <p>Company: {user.company.name}</p>
          </div>
        ))}
      </div>
    </div>
  );
}

export default UserDirectory;
```

**Key Points:**
- The `async` function is defined inside the effect, not as the effect callback itself.
- The empty dependency array ensures the fetch runs only once on mount.
- Three states (loading, error, data) handle all possible outcomes of the fetch.
- `response.ok` is checked to catch HTTP errors that `fetch` does not throw by default.
</details>

---

**Exercise 2: Digital Clock with `setInterval` and Cleanup**

Build a digital clock component that displays the current time, updated every second. Properly clean up the interval when the component unmounts.

<details>
<summary>Solution</summary>

```jsx
import { useState, useEffect } from "react";

function DigitalClock() {
  const [time, setTime] = useState(new Date());

  useEffect(() => {
    const intervalId = setInterval(() => {
      setTime(new Date());
    }, 1000);

    // Cleanup: clear the interval when the component unmounts
    return () => {
      clearInterval(intervalId);
    };
  }, []);

  const formatTime = (date) => {
    return date.toLocaleTimeString("en-US", {
      hour: "2-digit",
      minute: "2-digit",
      second: "2-digit",
      hour12: true,
    });
  };

  const formatDate = (date) => {
    return date.toLocaleDateString("en-US", {
      weekday: "long",
      year: "numeric",
      month: "long",
      day: "numeric",
    });
  };

  return (
    <div className="digital-clock">
      <div className="time-display">{formatTime(time)}</div>
      <div className="date-display">{formatDate(time)}</div>
    </div>
  );
}

function App() {
  const [showClock, setShowClock] = useState(true);

  return (
    <div className="app">
      <button onClick={() => setShowClock((prev) => !prev)}>
        {showClock ? "Hide Clock" : "Show Clock"}
      </button>

      {showClock && <DigitalClock />}
    </div>
  );
}

export default App;
```

**Key Points:**
- `setInterval` creates a recurring timer that updates the time state every second.
- The cleanup function (`clearInterval`) is critical -- without it, the interval continues running after the component unmounts, causing a memory leak and a "state update on unmounted component" warning.
- The `App` component demonstrates mount/unmount behavior by toggling the clock's visibility.
</details>

---

**Exercise 3: Search with Debounce**

Build a search component that debounces the input. The search should only trigger 500ms after the user stops typing, and any pending search should be canceled if the user types again.

<details>
<summary>Solution</summary>

```jsx
import { useState, useEffect } from "react";

function DebouncedSearch() {
  const [query, setQuery] = useState("");
  const [debouncedQuery, setDebouncedQuery] = useState("");
  const [results, setResults] = useState([]);
  const [loading, setLoading] = useState(false);

  // Debounce the query
  useEffect(() => {
    const timerId = setTimeout(() => {
      setDebouncedQuery(query);
    }, 500);

    // Cleanup: cancel the previous timeout if the user types again
    return () => clearTimeout(timerId);
  }, [query]);

  // Fetch results when the debounced query changes
  useEffect(() => {
    if (debouncedQuery.trim() === "") {
      setResults([]);
      return;
    }

    async function search() {
      setLoading(true);
      try {
        const response = await fetch(
          `https://jsonplaceholder.typicode.com/posts?q=${encodeURIComponent(debouncedQuery)}`
        );
        const data = await response.json();
        setResults(data.slice(0, 10)); // Limit to 10 results
      } catch (err) {
        console.error("Search failed:", err);
      } finally {
        setLoading(false);
      }
    }

    search();
  }, [debouncedQuery]);

  return (
    <div className="search-component">
      <h2>Search Posts</h2>

      <input
        type="text"
        value={query}
        onChange={(e) => setQuery(e.target.value)}
        placeholder="Type to search..."
        className="search-input"
      />

      {query !== debouncedQuery && <p className="debounce-indicator">Waiting...</p>}
      {loading && <p className="loading">Searching...</p>}

      <div className="search-results">
        {results.length > 0 ? (
          <ul>
            {results.map((post) => (
              <li key={post.id}>
                <h4>{post.title}</h4>
                <p>{post.body.substring(0, 100)}...</p>
              </li>
            ))}
          </ul>
        ) : (
          debouncedQuery && !loading && <p>No results found.</p>
        )}
      </div>
    </div>
  );
}

export default DebouncedSearch;
```

**Key Points:**
- Two separate effects handle debouncing and fetching independently.
- The first effect sets a timeout that updates `debouncedQuery` after 500ms. The cleanup function clears the timeout if `query` changes before the timeout fires, effectively debouncing the input.
- The second effect fetches data only when `debouncedQuery` changes, avoiding unnecessary API calls while the user is still typing.
</details>

---

**Exercise 4: Document Title Updater**

Create a component that updates the browser's document title based on a counter value. The title should reflect the current count.

<details>
<summary>Solution</summary>

```jsx
import { useState, useEffect } from "react";

function DocumentTitleUpdater() {
  const [count, setCount] = useState(0);
  const [customTitle, setCustomTitle] = useState("");

  useEffect(() => {
    if (customTitle.trim()) {
      document.title = `${customTitle} (${count})`;
    } else {
      document.title = `Count: ${count} | My React App`;
    }

    // Cleanup: restore original title when component unmounts
    return () => {
      document.title = "React App";
    };
  }, [count, customTitle]);

  return (
    <div className="title-updater">
      <h2>Document Title Updater</h2>
      <p>Check your browser tab to see the title change!</p>

      <div className="counter-section">
        <button onClick={() => setCount((prev) => prev - 1)}>-</button>
        <span className="count">{count}</span>
        <button onClick={() => setCount((prev) => prev + 1)}>+</button>
      </div>

      <div className="custom-title-section">
        <label htmlFor="titleInput">Custom Title Prefix:</label>
        <input
          id="titleInput"
          type="text"
          value={customTitle}
          onChange={(e) => setCustomTitle(e.target.value)}
          placeholder="Enter custom title..."
        />
      </div>

      <p className="current-title">
        Current title: <strong>{customTitle.trim() ? `${customTitle} (${count})` : `Count: ${count} | My React App`}</strong>
      </p>
    </div>
  );
}

export default DocumentTitleUpdater;
```

**Key Points:**
- `document.title` is a side effect because it modifies something outside the component.
- The dependency array `[count, customTitle]` ensures the effect runs whenever either value changes.
- The cleanup function restores the original title when the component unmounts.
</details>

---

**Exercise 5: localStorage Sync**

Build a notes component that saves and loads its content from `localStorage`, persisting data across page refreshes.

<details>
<summary>Solution</summary>

```jsx
import { useState, useEffect } from "react";

function PersistentNotes() {
  const [notes, setNotes] = useState(() => {
    const saved = localStorage.getItem("user-notes");
    return saved ? JSON.parse(saved) : [];
  });

  const [inputValue, setInputValue] = useState("");

  // Sync notes to localStorage whenever they change
  useEffect(() => {
    localStorage.setItem("user-notes", JSON.stringify(notes));
  }, [notes]);

  const addNote = (e) => {
    e.preventDefault();
    if (inputValue.trim() === "") return;

    const newNote = {
      id: Date.now(),
      text: inputValue.trim(),
      createdAt: new Date().toLocaleString(),
    };

    setNotes((prev) => [newNote, ...prev]);
    setInputValue("");
  };

  const deleteNote = (id) => {
    setNotes((prev) => prev.filter((note) => note.id !== id));
  };

  const clearAllNotes = () => {
    setNotes([]);
  };

  return (
    <div className="persistent-notes">
      <h2>My Notes</h2>
      <p className="subtitle">Notes are saved automatically to localStorage.</p>

      <form onSubmit={addNote} className="note-form">
        <input
          type="text"
          value={inputValue}
          onChange={(e) => setInputValue(e.target.value)}
          placeholder="Write a note..."
        />
        <button type="submit">Add Note</button>
      </form>

      {notes.length > 0 && (
        <div className="notes-header">
          <span>{notes.length} note(s)</span>
          <button className="clear-btn" onClick={clearAllNotes}>
            Clear All
          </button>
        </div>
      )}

      <ul className="notes-list">
        {notes.map((note) => (
          <li key={note.id} className="note-item">
            <div className="note-content">
              <p>{note.text}</p>
              <small>{note.createdAt}</small>
            </div>
            <button
              className="delete-btn"
              onClick={() => deleteNote(note.id)}
            >
              Delete
            </button>
          </li>
        ))}
      </ul>

      {notes.length === 0 && (
        <p className="empty-message">No notes yet. Start writing!</p>
      )}
    </div>
  );
}

export default PersistentNotes;
```

**Key Points:**
- Lazy initialization (`useState(() => ...)`) reads from `localStorage` only on the first render, avoiding unnecessary reads on re-renders.
- The `useEffect` with `[notes]` dependency writes to `localStorage` whenever notes change.
- `JSON.stringify` and `JSON.parse` are used because `localStorage` only stores strings.
- New notes are prepended to the array so the most recent appears first.
</details>

---

**Exercise 6: Window Resize Tracker**

Create a component that tracks the browser window dimensions in real time and displays them. Clean up the event listener when the component unmounts.

<details>
<summary>Solution</summary>

```jsx
import { useState, useEffect } from "react";

function WindowSizeTracker() {
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

    // Cleanup: remove the event listener on unmount
    return () => {
      window.removeEventListener("resize", handleResize);
    };
  }, []);

  const getDeviceType = () => {
    if (windowSize.width < 768) return "Mobile";
    if (windowSize.width < 1024) return "Tablet";
    return "Desktop";
  };

  const getBreakpointColor = () => {
    if (windowSize.width < 768) return "#e74c3c";
    if (windowSize.width < 1024) return "#f39c12";
    return "#2ecc71";
  };

  return (
    <div className="window-tracker">
      <h2>Window Size Tracker</h2>

      <div className="size-display">
        <div className="dimension">
          <span className="label">Width</span>
          <span className="value">{windowSize.width}px</span>
        </div>
        <div className="dimension">
          <span className="label">Height</span>
          <span className="value">{windowSize.height}px</span>
        </div>
      </div>

      <div
        className="device-indicator"
        style={{ backgroundColor: getBreakpointColor() }}
      >
        <p>Device Type: <strong>{getDeviceType()}</strong></p>
      </div>

      <p className="instruction">Resize your browser window to see the values update.</p>
    </div>
  );
}

export default WindowSizeTracker;
```

**Key Points:**
- The `resize` event listener is added once (empty dependency array) and removed on unmount.
- The cleanup function is essential to prevent memory leaks from lingering event listeners.
- Derived values (`getDeviceType`, `getBreakpointColor`) are computed from state rather than stored as separate state variables.
</details>

---

**Exercise 7: Weather App -- Fetch Data Based on City Input**

Build a weather app that fetches weather data whenever the user enters a new city. Use debouncing to avoid excessive API calls and handle loading/error states.

<details>
<summary>Solution</summary>

```jsx
import { useState, useEffect } from "react";

function WeatherApp() {
  const [city, setCity] = useState("");
  const [debouncedCity, setDebouncedCity] = useState("");
  const [weather, setWeather] = useState(null);
  const [loading, setLoading] = useState(false);
  const [error, setError] = useState(null);

  // Debounce the city input
  useEffect(() => {
    const timerId = setTimeout(() => {
      setDebouncedCity(city);
    }, 600);

    return () => clearTimeout(timerId);
  }, [city]);

  // Fetch weather data when debounced city changes
  useEffect(() => {
    if (debouncedCity.trim() === "") {
      setWeather(null);
      setError(null);
      return;
    }

    const controller = new AbortController();

    async function fetchWeather() {
      setLoading(true);
      setError(null);

      try {
        // Using a free weather API (replace API_KEY with a real key in production)
        const response = await fetch(
          `https://api.openweathermap.org/data/2.5/weather?q=${encodeURIComponent(debouncedCity)}&appid=API_KEY&units=metric`,
          { signal: controller.signal }
        );

        if (!response.ok) {
          if (response.status === 404) {
            throw new Error("City not found. Please check the spelling.");
          }
          throw new Error(`Failed to fetch weather data (${response.status}).`);
        }

        const data = await response.json();
        setWeather({
          city: data.name,
          country: data.sys.country,
          temperature: Math.round(data.main.temp),
          feelsLike: Math.round(data.main.feels_like),
          humidity: data.main.humidity,
          description: data.weather[0].description,
          windSpeed: data.wind.speed,
        });
      } catch (err) {
        if (err.name !== "AbortError") {
          setError(err.message);
          setWeather(null);
        }
      } finally {
        setLoading(false);
      }
    }

    fetchWeather();

    // Cleanup: abort the fetch if the city changes before the request completes
    return () => controller.abort();
  }, [debouncedCity]);

  return (
    <div className="weather-app">
      <h2>Weather App</h2>

      <input
        type="text"
        value={city}
        onChange={(e) => setCity(e.target.value)}
        placeholder="Enter a city name..."
        className="city-input"
      />

      {loading && <p className="loading">Fetching weather data...</p>}
      {error && <p className="error">{error}</p>}

      {weather && !loading && (
        <div className="weather-card">
          <h3>{weather.city}, {weather.country}</h3>
          <div className="weather-main">
            <span className="temperature">{weather.temperature}°C</span>
            <span className="description">{weather.description}</span>
          </div>
          <div className="weather-details">
            <p>Feels like: {weather.feelsLike}°C</p>
            <p>Humidity: {weather.humidity}%</p>
            <p>Wind: {weather.windSpeed} m/s</p>
          </div>
        </div>
      )}

      {!weather && !loading && !error && (
        <p className="placeholder">Enter a city name to see the weather.</p>
      )}
    </div>
  );
}

export default WeatherApp;
```

**Key Points:**
- Debouncing prevents an API call on every keystroke.
- `AbortController` cancels in-flight requests when the city changes, preventing race conditions where an older request returns after a newer one.
- The `AbortError` is caught and ignored because it is an intentional cancellation.
- Error handling distinguishes between "city not found" (404) and other errors.
- Note: In production, replace `API_KEY` with an actual API key and store it in an environment variable.
</details>

---

**Exercise 8: Complete Dashboard -- Fetch Multiple APIs**

Build a dashboard that fetches data from multiple API endpoints simultaneously and displays users, posts, and todos. Include loading states, error handling, and a refresh button.

<details>
<summary>Solution</summary>

```jsx
import { useState, useEffect, useRef } from "react";

function Dashboard() {
  const [data, setData] = useState({
    users: [],
    posts: [],
    todos: [],
  });
  const [loading, setLoading] = useState(true);
  const [error, setError] = useState(null);
  const [lastUpdated, setLastUpdated] = useState(null);
  const abortControllerRef = useRef(null);

  const fetchDashboardData = async () => {
    // Abort any in-flight request
    if (abortControllerRef.current) {
      abortControllerRef.current.abort();
    }

    const controller = new AbortController();
    abortControllerRef.current = controller;

    setLoading(true);
    setError(null);

    try {
      const [usersResponse, postsResponse, todosResponse] = await Promise.all([
        fetch("https://jsonplaceholder.typicode.com/users", {
          signal: controller.signal,
        }),
        fetch("https://jsonplaceholder.typicode.com/posts?_limit=5", {
          signal: controller.signal,
        }),
        fetch("https://jsonplaceholder.typicode.com/todos?_limit=10", {
          signal: controller.signal,
        }),
      ]);

      if (!usersResponse.ok || !postsResponse.ok || !todosResponse.ok) {
        throw new Error("One or more API requests failed.");
      }

      const [users, posts, todos] = await Promise.all([
        usersResponse.json(),
        postsResponse.json(),
        todosResponse.json(),
      ]);

      setData({ users, posts, todos });
      setLastUpdated(new Date().toLocaleTimeString());
    } catch (err) {
      if (err.name !== "AbortError") {
        setError(err.message);
      }
    } finally {
      setLoading(false);
    }
  };

  useEffect(() => {
    fetchDashboardData();

    // Cleanup: abort on unmount
    return () => {
      if (abortControllerRef.current) {
        abortControllerRef.current.abort();
      }
    };
  }, []);

  if (loading && data.users.length === 0) {
    return (
      <div className="dashboard-loading">
        <h2>Dashboard</h2>
        <p>Loading dashboard data...</p>
      </div>
    );
  }

  if (error) {
    return (
      <div className="dashboard-error">
        <h2>Dashboard</h2>
        <p className="error">Error: {error}</p>
        <button onClick={fetchDashboardData}>Retry</button>
      </div>
    );
  }

  return (
    <div className="dashboard">
      <div className="dashboard-header">
        <h2>Dashboard</h2>
        <div className="header-actions">
          {lastUpdated && <span>Last updated: {lastUpdated}</span>}
          <button onClick={fetchDashboardData} disabled={loading}>
            {loading ? "Refreshing..." : "Refresh"}
          </button>
        </div>
      </div>

      <div className="dashboard-grid">
        {/* Users Panel */}
        <div className="dashboard-panel">
          <h3>Users ({data.users.length})</h3>
          <ul>
            {data.users.slice(0, 5).map((user) => (
              <li key={user.id}>
                <strong>{user.name}</strong>
                <span>{user.email}</span>
              </li>
            ))}
          </ul>
        </div>

        {/* Recent Posts Panel */}
        <div className="dashboard-panel">
          <h3>Recent Posts ({data.posts.length})</h3>
          <ul>
            {data.posts.map((post) => (
              <li key={post.id}>
                <strong>{post.title}</strong>
                <p>{post.body.substring(0, 80)}...</p>
              </li>
            ))}
          </ul>
        </div>

        {/* Todos Panel */}
        <div className="dashboard-panel">
          <h3>Todos ({data.todos.length})</h3>
          <ul>
            {data.todos.map((todo) => (
              <li
                key={todo.id}
                className={todo.completed ? "completed" : "pending"}
              >
                <span className={todo.completed ? "line-through" : ""}>
                  {todo.title}
                </span>
                <span className="status">
                  {todo.completed ? "Done" : "Pending"}
                </span>
              </li>
            ))}
          </ul>
        </div>
      </div>

      {/* Summary Stats */}
      <div className="dashboard-stats">
        <div className="stat-card">
          <span className="stat-number">{data.users.length}</span>
          <span className="stat-label">Total Users</span>
        </div>
        <div className="stat-card">
          <span className="stat-number">{data.posts.length}</span>
          <span className="stat-label">Recent Posts</span>
        </div>
        <div className="stat-card">
          <span className="stat-number">
            {data.todos.filter((t) => t.completed).length}
          </span>
          <span className="stat-label">Completed Todos</span>
        </div>
        <div className="stat-card">
          <span className="stat-number">
            {data.todos.filter((t) => !t.completed).length}
          </span>
          <span className="stat-label">Pending Todos</span>
        </div>
      </div>
    </div>
  );
}

export default Dashboard;
```

**Key Points:**
- `Promise.all` fetches from multiple endpoints concurrently, reducing total load time compared to sequential fetches.
- `AbortController` is stored in a `useRef` so it persists across renders without triggering re-renders. It cancels in-flight requests on unmount and when a refresh is triggered.
- The refresh button allows the user to manually re-fetch all data.
- Summary statistics are derived from the fetched data rather than stored as separate state.
- The initial loading state shows a full-page loader, while subsequent refreshes use the button's disabled state to indicate progress.
</details>
