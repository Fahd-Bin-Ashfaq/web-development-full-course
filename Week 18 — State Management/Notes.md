# Week 18: State Management

> **Prerequisites:** React components, JSX, and props from Weeks 16-17.

---

## Table of Contents

1. [What is State?](#1-what-is-state)
2. [useState Hook](#2-usestate-hook)
3. [Handling Forms and User Input](#3-handling-forms-and-user-input)
4. [Controlled vs Uncontrolled Components](#4-controlled-vs-uncontrolled-components)
5. [State with Arrays and Objects](#5-state-with-arrays-and-objects)
6. [Lifting State Up](#6-lifting-state-up)
7. [Conditional Rendering Based on State](#7-conditional-rendering-based-on-state)
8. [Multiple useState vs One State Object](#8-multiple-usestate-vs-one-state-object)
9. [Summary](#9-summary)

---

## 1. What is State?

### Understanding State Through Real Life

Every application deals with data that changes over time. When a user clicks a button, types into a search bar, or adds an item to a cart, the application needs to remember what changed and update the screen accordingly. That changing data is called **state**.

**Real-life analogy: A Scoreboard**

Imagine a cricket match on TV. The scoreboard shows the team names and the current score. The team names were decided before the match started and they never change during the game. But the score? It changes every time someone hits a boundary or takes a wicket. The team names are like **props** -- they come from outside and stay fixed. The score is like **state** -- it lives inside the scoreboard and updates as the game progresses.

```
             SCOREBOARD (Component)
  +--------------------------------------+
  |                                      |
  |   Team A: Pakistan    (prop)         |
  |   Team B: India       (prop)         |
  |                                      |
  |   Score: 245 / 6      (state)        |
  |   Overs: 38.2         (state)        |
  |                                      |
  |   Props don't change during match    |
  |   State changes with every ball      |
  |                                      |
  +--------------------------------------+
```

### Props vs State

| Feature           | Props                              | State                               |
|-------------------|------------------------------------|--------------------------------------|
| **Source**         | Passed from parent component       | Created and managed inside component |
| **Mutability**    | Read-only (cannot be changed)      | Mutable (can be updated)             |
| **Who controls?** | Parent component                   | The component itself                 |
| **Purpose**       | Configure a component from outside | Track data that changes over time     |
| **Re-render?**    | Yes, when parent passes new props  | Yes, when state is updated           |
| **Analogy**       | Your name on a name tag            | Your mood throughout the day         |

```
  PROPS vs STATE — Data Flow
  ============================

  PROPS (External Data)
  +----------+          +----------+
  | Parent   |  props   | Child    |
  |          | -------> |          |
  |          |          | (read    |
  |          |          |  only)   |
  +----------+          +----------+

  STATE (Internal Data)
  +----------------------------+
  | Component                  |
  |                            |
  |   state lives HERE         |
  |   component can READ it    |
  |   component can UPDATE it  |
  |                            |
  |   When state changes,      |
  |   React re-renders this    |
  |   component automatically  |
  +----------------------------+
```

### When to Use Props vs State

Use **props** when:
- A parent component needs to pass data down to a child
- The child should not modify the data
- The data is configuration or display information

Use **state** when:
- The data originates inside the component
- The data will change over time (user interaction, timer, API response)
- The component needs to re-render when the data changes

```javascript
// Props: the parent decides what title to show
function Header({ title }) {
  return <h1>{title}</h1>;
}

// State: the component tracks its own count
function Counter() {
  const [count, setCount] = useState(0);
  return <button onClick={() => setCount(count + 1)}>Clicked {count} times</button>;
}
```

---

## 2. useState Hook

### What is a Hook?

A Hook is a special function provided by React that lets you "hook into" React features (like state) from inside a function component. Before Hooks existed, you had to write class components to use state. Hooks make function components just as powerful, but simpler.

The most fundamental Hook is `useState`.

### Syntax

```javascript
import { useState } from "react";

const [value, setValue] = useState(initialValue);
```

- `value` -- the current state value
- `setValue` -- a function to update the state
- `initialValue` -- the starting value when the component first renders

```
  useState BREAKDOWN
  ====================

  const [count, setCount] = useState(0);
        |       |                   |
        |       |                   +---> Initial value (0)
        |       |
        |       +---> Updater function (call this to change state)
        |
        +---> Current state value (read this to display)
```

### Why Array Destructuring?

`useState` returns an array with exactly two elements: the current value and the updater function. Array destructuring lets you give them any names you want.

```javascript
// What useState actually returns
const stateArray = useState(0);
const count = stateArray[0];       // current value
const setCount = stateArray[1];    // updater function

// Array destructuring does the same thing in one line
const [count, setCount] = useState(0);

// You can name them whatever you want
const [age, setAge] = useState(25);
const [name, setName] = useState("Ali");
const [isLoggedIn, setIsLoggedIn] = useState(false);
```

The convention is to name them `[something, setSomething]`.

### A Complete Example

```javascript
import { useState } from "react";

function Counter() {
  const [count, setCount] = useState(0);

  function handleIncrement() {
    setCount(count + 1);
  }

  function handleDecrement() {
    setCount(count - 1);
  }

  function handleReset() {
    setCount(0);
  }

  return (
    <div>
      <h2>Counter: {count}</h2>
      <button onClick={handleIncrement}>+</button>
      <button onClick={handleDecrement}>-</button>
      <button onClick={handleReset}>Reset</button>
    </div>
  );
}

export default Counter;
```

```
  HOW STATE UPDATES TRIGGER RE-RENDER
  ======================================

  1. User clicks "+" button
            |
            v
  2. handleIncrement() runs
            |
            v
  3. setCount(count + 1) is called
            |
            v
  4. React schedules a re-render
            |
            v
  5. Component function runs again
     with count = new value
            |
            v
  6. New JSX is returned
            |
            v
  7. React updates the DOM
            |
            v
  8. User sees updated screen
```

### State with Different Types

State can hold any JavaScript data type.

```javascript
function ProfileForm() {
  // String state
  const [name, setName] = useState("Ali");

  // Number state
  const [age, setAge] = useState(25);

  // Boolean state
  const [isStudent, setIsStudent] = useState(true);

  // Array state
  const [hobbies, setHobbies] = useState(["reading", "coding"]);

  // Object state
  const [address, setAddress] = useState({
    city: "Karachi",
    country: "Pakistan"
  });

  return (
    <div>
      <p>Name: {name}</p>
      <p>Age: {age}</p>
      <p>Student: {isStudent ? "Yes" : "No"}</p>
      <p>Hobbies: {hobbies.join(", ")}</p>
      <p>City: {address.city}</p>
    </div>
  );
}
```

### Rules of Hooks

React Hooks follow two strict rules. Breaking them will cause bugs or errors.

**Rule 1: Only call Hooks at the top level**

Do not call Hooks inside loops, conditions, or nested functions. React relies on the order Hooks are called to correctly associate state with the right variable.

```javascript
// WRONG -- Hook inside a condition
function MyComponent({ isLoggedIn }) {
  if (isLoggedIn) {
    const [name, setName] = useState("");  // This breaks React
  }
}

// CORRECT -- Hook at the top level, condition inside
function MyComponent({ isLoggedIn }) {
  const [name, setName] = useState("");

  if (isLoggedIn) {
    // Use name here
  }
}
```

**Rule 2: Only call Hooks in React functions**

Hooks must be called inside React function components or inside custom Hooks (functions that start with `use`). Never call them in regular JavaScript functions.

```javascript
// WRONG -- Hook in a regular function
function calculateTotal() {
  const [total, setTotal] = useState(0);  // This will not work
}

// CORRECT -- Hook in a React component
function ShoppingCart() {
  const [total, setTotal] = useState(0);  // This works
  return <p>Total: {total}</p>;
}
```

### State is Asynchronous

When you call a state updater function, React does not update the state immediately. It schedules the update and processes it before the next render. This means you cannot read the new value right after calling the setter.

```javascript
function Counter() {
  const [count, setCount] = useState(0);

  function handleClick() {
    setCount(count + 1);
    console.log(count);  // Still shows the OLD value!
    // If count was 0, this logs 0, not 1
  }

  return <button onClick={handleClick}>Count: {count}</button>;
}
```

**Why?** React batches multiple state updates together for performance. Instead of re-rendering after every single `setState` call, React processes them all at once and does a single re-render.

**Functional update form** -- when the new state depends on the previous state, use a callback:

```javascript
function Counter() {
  const [count, setCount] = useState(0);

  function handleTripleIncrement() {
    // WRONG -- all three read the same stale count value
    setCount(count + 1);  // 0 + 1 = 1
    setCount(count + 1);  // 0 + 1 = 1 (still using old count!)
    setCount(count + 1);  // 0 + 1 = 1 (still using old count!)
    // Result: count becomes 1, not 3

    // CORRECT -- each callback receives the latest state
    setCount(prev => prev + 1);  // 0 + 1 = 1
    setCount(prev => prev + 1);  // 1 + 1 = 2
    setCount(prev => prev + 1);  // 2 + 1 = 3
    // Result: count becomes 3
  }

  return <button onClick={handleTripleIncrement}>Count: {count}</button>;
}
```

---

## 3. Handling Forms and User Input

### Controlled Components

A controlled component is an input element whose value is driven by React state. The state is the "single source of truth." Every time the user types, the state updates, and the input displays whatever the state holds.

```
  CONTROLLED INPUT FLOW
  =======================

  +--------+   onChange   +----------+   re-render   +--------+
  | User   | ----------> | setState | ------------> | Input  |
  | types  |             | (update  |               | shows  |
  | "H"    |             |  state)  |               | new    |
  +--------+             +----------+               | value  |
       ^                                            +--------+
       |                                                |
       +------------------------------------------------+
              The input value ALWAYS equals state
```

```javascript
import { useState } from "react";

function NameInput() {
  const [name, setName] = useState("");

  function handleChange(event) {
    setName(event.target.value);
  }

  return (
    <div>
      <label htmlFor="name">Your Name:</label>
      <input
        id="name"
        type="text"
        value={name}           // Tied to state
        onChange={handleChange} // Updates state on every keystroke
      />
      <p>Hello, {name}!</p>
    </div>
  );
}
```

### The onChange Event Handler

The `onChange` event fires every time the input value changes. React passes an event object to the handler function. The typed value lives at `event.target.value`.

```javascript
function handleChange(event) {
  console.log(event.target.value);  // Whatever the user typed
  console.log(event.target.name);   // The "name" attribute of the input
  console.log(event.target.type);   // "text", "email", "checkbox", etc.
}
```

### Form Submission

Use the `onSubmit` event on the `<form>` element. Always call `event.preventDefault()` to stop the browser from refreshing the page.

```javascript
import { useState } from "react";

function LoginForm() {
  const [email, setEmail] = useState("");
  const [password, setPassword] = useState("");

  function handleSubmit(event) {
    event.preventDefault();  // Prevent page refresh
    console.log("Submitting:", { email, password });
    // Send data to server, validate, etc.
  }

  return (
    <form onSubmit={handleSubmit}>
      <input
        type="email"
        value={email}
        onChange={(e) => setEmail(e.target.value)}
        placeholder="Email"
      />
      <input
        type="password"
        value={password}
        onChange={(e) => setPassword(e.target.value)}
        placeholder="Password"
      />
      <button type="submit">Log In</button>
    </form>
  );
}
```

### Multiple Inputs in One Form

When a form has many inputs, using a separate `useState` for each field works but can get repetitive. A cleaner approach is to use one state object and a single change handler. You set the `name` attribute on each input to match the state key.

```javascript
import { useState } from "react";

function RegistrationForm() {
  const [formData, setFormData] = useState({
    firstName: "",
    lastName: "",
    email: "",
    password: "",
    age: "",
    agreeToTerms: false
  });

  function handleChange(event) {
    const { name, value, type, checked } = event.target;

    setFormData(prev => ({
      ...prev,
      [name]: type === "checkbox" ? checked : value
    }));
  }

  function handleSubmit(event) {
    event.preventDefault();
    console.log("Form submitted:", formData);
  }

  return (
    <form onSubmit={handleSubmit}>
      <div>
        <label htmlFor="firstName">First Name:</label>
        <input
          id="firstName"
          type="text"
          name="firstName"
          value={formData.firstName}
          onChange={handleChange}
        />
      </div>

      <div>
        <label htmlFor="lastName">Last Name:</label>
        <input
          id="lastName"
          type="text"
          name="lastName"
          value={formData.lastName}
          onChange={handleChange}
        />
      </div>

      <div>
        <label htmlFor="email">Email:</label>
        <input
          id="email"
          type="email"
          name="email"
          value={formData.email}
          onChange={handleChange}
        />
      </div>

      <div>
        <label htmlFor="password">Password:</label>
        <input
          id="password"
          type="password"
          name="password"
          value={formData.password}
          onChange={handleChange}
        />
      </div>

      <div>
        <label htmlFor="age">Age:</label>
        <input
          id="age"
          type="number"
          name="age"
          value={formData.age}
          onChange={handleChange}
        />
      </div>

      <div>
        <label>
          <input
            type="checkbox"
            name="agreeToTerms"
            checked={formData.agreeToTerms}
            onChange={handleChange}
          />
          I agree to the Terms and Conditions
        </label>
      </div>

      <button type="submit">Register</button>
    </form>
  );
}

export default RegistrationForm;
```

```
  HOW THE SINGLE HANDLER WORKS
  ==============================

  Input has name="email" and user types "a@b.com"
           |
           v
  event.target gives us:
    name  = "email"
    value = "a@b.com"
    type  = "email"
           |
           v
  setFormData(prev => ({
    ...prev,               <-- copy all existing fields
    [name]: value          <-- overwrite just "email" with "a@b.com"
  }))
           |
           v
  State becomes:
  {
    firstName: "Ali",       <-- unchanged
    lastName: "Khan",       <-- unchanged
    email: "a@b.com",      <-- updated!
    password: "secret",    <-- unchanged
    age: "22",             <-- unchanged
    agreeToTerms: true     <-- unchanged
  }
```

---

## 4. Controlled vs Uncontrolled Components

### Controlled Components (Recommended)

In a controlled component, React state is the single source of truth. The input's value is always whatever the state says.

```javascript
function ControlledInput() {
  const [text, setText] = useState("");

  return (
    <input
      type="text"
      value={text}                          // React controls the value
      onChange={(e) => setText(e.target.value)}
    />
  );
}
```

### Uncontrolled Components

In an uncontrolled component, the DOM itself holds the value. You read the value only when you need it (for example, on form submit) using a **ref**.

```javascript
import { useRef } from "react";

function UncontrolledInput() {
  const inputRef = useRef(null);

  function handleSubmit(event) {
    event.preventDefault();
    console.log("Input value:", inputRef.current.value);  // Read from DOM
  }

  return (
    <form onSubmit={handleSubmit}>
      <input
        type="text"
        ref={inputRef}                // DOM controls the value
        defaultValue="initial text"   // Note: defaultValue, not value
      />
      <button type="submit">Submit</button>
    </form>
  );
}
```

### Comparison Table

| Feature                 | Controlled                          | Uncontrolled                       |
|-------------------------|-------------------------------------|------------------------------------|
| **Value source**        | React state                         | The DOM                            |
| **How to read value**   | From state variable                 | Using ref (`inputRef.current.value`) |
| **Initial value**       | `value={state}`                     | `defaultValue="..."`               |
| **On every keystroke**  | onChange handler fires, state updates | Nothing happens in React           |
| **Validation**          | Instant (on every change)           | Only when you read the ref         |
| **Code complexity**     | Slightly more boilerplate           | Less code                          |
| **React recommendation**| Preferred approach                  | Use only when needed               |

```
  CONTROLLED vs UNCONTROLLED
  ============================

  CONTROLLED:
  React State  <----->  Input Value
  (always in sync, React is the boss)

  UNCONTROLLED:
  React State          Input Value
  (disconnected, DOM is the boss,
   you ask the DOM when you need the value)
```

### When to Use Which

**Use controlled components** (most of the time):
- When you need instant validation as the user types
- When you need to conditionally disable a submit button
- When you need to enforce a specific input format (for example, only numbers)
- When multiple elements depend on the same value

**Use uncontrolled components** (rare cases):
- When integrating with non-React code or third-party DOM libraries
- When building a simple file upload input (`<input type="file" />` is always uncontrolled)
- When you want a quick prototype and do not need real-time validation

---

## 5. State with Arrays and Objects

### The Golden Rule: Never Mutate State Directly

React detects changes by comparing the old state reference with the new one. If you mutate the existing object or array, the reference stays the same, and React does not re-render.

```javascript
// WRONG -- mutating state directly
const [items, setItems] = useState(["Apple", "Banana"]);

function addItem() {
  items.push("Cherry");  // Mutates the existing array
  setItems(items);        // Same reference -- React sees no change!
}

// CORRECT -- creating a new array
function addItem() {
  setItems([...items, "Cherry"]);  // New array, new reference
}
```

```
  WHY MUTATION FAILS
  ====================

  WRONG (mutation):
  items = [A, B]        items = [A, B, C]
  ref: 0x001            ref: 0x001          <-- same reference!
                        React: "nothing changed"

  CORRECT (new array):
  items = [A, B]        newItems = [A, B, C]
  ref: 0x001            ref: 0x002          <-- different reference!
                        React: "state changed, re-render!"
```

### Adding to an Array

Use the spread operator to copy existing items and append the new one.

```javascript
function TodoApp() {
  const [todos, setTodos] = useState([
    { id: 1, text: "Learn React", done: false },
    { id: 2, text: "Learn State", done: false }
  ]);
  const [input, setInput] = useState("");

  function addTodo() {
    if (input.trim() === "") return;

    const newTodo = {
      id: Date.now(),          // Simple unique ID
      text: input,
      done: false
    };

    setTodos([...todos, newTodo]);  // Add to end
    // setTodos([newTodo, ...todos]);  // Add to beginning
    setInput("");
  }

  return (
    <div>
      <input value={input} onChange={(e) => setInput(e.target.value)} />
      <button onClick={addTodo}>Add</button>
      <ul>
        {todos.map(todo => (
          <li key={todo.id}>{todo.text}</li>
        ))}
      </ul>
    </div>
  );
}
```

### Removing from an Array

Use `filter` to create a new array that excludes the item you want to remove.

```javascript
function removeTodo(id) {
  setTodos(todos.filter(todo => todo.id !== id));
}

// Usage in JSX
<ul>
  {todos.map(todo => (
    <li key={todo.id}>
      {todo.text}
      <button onClick={() => removeTodo(todo.id)}>Delete</button>
    </li>
  ))}
</ul>
```

```
  REMOVING WITH FILTER
  ======================

  Before: [{ id: 1 }, { id: 2 }, { id: 3 }]

  removeTodo(2)
  filter keeps items where todo.id !== 2

  After:  [{ id: 1 }, { id: 3 }]   <-- new array, id:2 is gone
```

### Updating an Item in an Array

Use `map` to create a new array. For the item you want to update, return a new object with the changed property. For all other items, return them unchanged.

```javascript
function toggleTodo(id) {
  setTodos(
    todos.map(todo =>
      todo.id === id
        ? { ...todo, done: !todo.done }   // New object with flipped "done"
        : todo                              // Keep unchanged
    )
  );
}

// Usage in JSX
<ul>
  {todos.map(todo => (
    <li
      key={todo.id}
      style={{ textDecoration: todo.done ? "line-through" : "none" }}
    >
      <input
        type="checkbox"
        checked={todo.done}
        onChange={() => toggleTodo(todo.id)}
      />
      {todo.text}
    </li>
  ))}
</ul>
```

### Updating Object State

Use the spread operator to copy all existing properties and override the ones that changed.

```javascript
function UserProfile() {
  const [user, setUser] = useState({
    name: "Ali",
    email: "ali@example.com",
    age: 25,
    city: "Karachi"
  });

  function updateCity(newCity) {
    setUser({
      ...user,       // Copy name, email, age
      city: newCity   // Override city
    });
  }

  function handleBirthday() {
    setUser(prev => ({
      ...prev,
      age: prev.age + 1
    }));
  }

  return (
    <div>
      <p>{user.name}, Age {user.age}, {user.city}</p>
      <button onClick={() => updateCity("Lahore")}>Move to Lahore</button>
      <button onClick={handleBirthday}>Birthday!</button>
    </div>
  );
}
```

### Quick Reference: Immutable State Updates

| Operation            | Code                                                        |
|----------------------|-------------------------------------------------------------|
| Add to array         | `setItems([...items, newItem])`                             |
| Add to beginning     | `setItems([newItem, ...items])`                             |
| Remove from array    | `setItems(items.filter(item => item.id !== id))`            |
| Update in array      | `setItems(items.map(i => i.id === id ? {...i, done: true} : i))` |
| Update object field  | `setUser({...user, name: "Sara"})`                          |
| Update nested object | `setUser({...user, address: {...user.address, city: "Lahore"}})` |

---

## 6. Lifting State Up

### The Problem

Sometimes two sibling components need to share the same data. But state is private to each component. One component cannot directly access or modify another component's state.

**Real-life analogy: A Thermostat**

Imagine two rooms in a house. Both rooms need to know the current temperature setting. If each room has its own thermostat with its own reading, they will go out of sync. The solution is to put one thermostat in the hallway (the parent) and let both rooms read from it.

### The Solution: Lift State Up

Move the shared state to the closest common parent of the components that need it. Then pass the state down as props, and pass the updater function down so children can request changes.

```
  BEFORE: State in sibling (broken)
  ====================================

  +------------------+
  |     Parent       |
  +------------------+
       |         |
       v         v
  +---------+ +---------+
  | Child A | | Child B |
  | count=5 | | count=? |  <-- Child B cannot access Child A's state
  +---------+ +---------+


  AFTER: State lifted to parent (working)
  ==========================================

  +-------------------------+
  |       Parent            |
  |   const [count, setCount] = useState(5)
  +-------------------------+
       |              |
       | count        | count
       | setCount     |
       v              v
  +---------+    +---------+
  | Child A |    | Child B |
  | (shows  |    | (shows  |
  |  count) |    |  count) |
  | (calls  |    |         |
  | setCount)|   |         |
  +---------+    +---------+

  Data flows DOWN via props.
  Events flow UP via callback functions.
```

### Complete Example: Temperature Converter

Two sibling components -- one for Celsius and one for Fahrenheit -- need to stay in sync. When you type in either field, the other updates automatically.

```javascript
import { useState } from "react";

// Parent component holds the shared state
function TemperatureCalculator() {
  const [celsius, setCelsius] = useState("");

  function handleCelsiusChange(value) {
    setCelsius(value);
  }

  function handleFahrenheitChange(value) {
    // Convert Fahrenheit back to Celsius for storage
    if (value === "") {
      setCelsius("");
    } else {
      setCelsius(((parseFloat(value) - 32) * 5 / 9).toFixed(2));
    }
  }

  // Convert Celsius to Fahrenheit for display
  const fahrenheit = celsius === ""
    ? ""
    : ((parseFloat(celsius) * 9 / 5) + 32).toFixed(2);

  return (
    <div>
      <h2>Temperature Converter</h2>
      <TemperatureInput
        label="Celsius"
        value={celsius}
        onChange={handleCelsiusChange}
      />
      <TemperatureInput
        label="Fahrenheit"
        value={fahrenheit}
        onChange={handleFahrenheitChange}
      />
    </div>
  );
}

// Child component -- displays and edits one temperature
function TemperatureInput({ label, value, onChange }) {
  return (
    <div>
      <label>{label}: </label>
      <input
        type="number"
        value={value}
        onChange={(e) => onChange(e.target.value)}
      />
    </div>
  );
}

export default TemperatureCalculator;
```

```
  DATA FLOW IN TEMPERATURE CONVERTER
  =====================================

  User types "100" in Celsius input
           |
           v
  onChange callback fires --> handleCelsiusChange("100")
           |
           v
  setCelsius("100")
           |
           v
  Parent re-renders:
    celsius = "100"
    fahrenheit = "212.00"
           |
           +-------> CelsiusInput  receives value="100"
           |
           +-------> FahrenheitInput receives value="212.00"
           
  Both inputs are now in sync!
```

### Another Example: Sibling Communication

A parent manages a list of products. One child displays the list. Another child adds new products.

```javascript
import { useState } from "react";

function ProductManager() {
  const [products, setProducts] = useState([
    { id: 1, name: "Laptop", price: 999 },
    { id: 2, name: "Phone", price: 699 }
  ]);

  function addProduct(newProduct) {
    setProducts([...products, { ...newProduct, id: Date.now() }]);
  }

  return (
    <div>
      <h2>Product Manager</h2>
      <AddProductForm onAdd={addProduct} />
      <ProductList products={products} />
    </div>
  );
}

function AddProductForm({ onAdd }) {
  const [name, setName] = useState("");
  const [price, setPrice] = useState("");

  function handleSubmit(e) {
    e.preventDefault();
    onAdd({ name, price: Number(price) });
    setName("");
    setPrice("");
  }

  return (
    <form onSubmit={handleSubmit}>
      <input value={name} onChange={(e) => setName(e.target.value)} placeholder="Product name" />
      <input value={price} onChange={(e) => setPrice(e.target.value)} placeholder="Price" type="number" />
      <button type="submit">Add Product</button>
    </form>
  );
}

function ProductList({ products }) {
  return (
    <ul>
      {products.map(p => (
        <li key={p.id}>{p.name} - ${p.price}</li>
      ))}
    </ul>
  );
}

export default ProductManager;
```

---

## 7. Conditional Rendering Based on State

State frequently determines what the user sees. A boolean state can show or hide a panel. A loading state can swap a spinner for the actual content. A user state can switch between a login form and a dashboard.

### Show and Hide Elements

```javascript
import { useState } from "react";

function ToggleMessage() {
  const [isVisible, setIsVisible] = useState(false);

  return (
    <div>
      <button onClick={() => setIsVisible(!isVisible)}>
        {isVisible ? "Hide" : "Show"} Message
      </button>

      {isVisible && <p>This message can be toggled on and off.</p>}
    </div>
  );
}
```

The `&&` operator works because in JavaScript, `true && <p>...</p>` returns the JSX, while `false && <p>...</p>` returns `false`, which React ignores.

### Toggle Between Components

```javascript
function TabSwitcher() {
  const [activeTab, setActiveTab] = useState("home");

  return (
    <div>
      <nav>
        <button onClick={() => setActiveTab("home")}>Home</button>
        <button onClick={() => setActiveTab("about")}>About</button>
        <button onClick={() => setActiveTab("contact")}>Contact</button>
      </nav>

      {activeTab === "home" && <HomeContent />}
      {activeTab === "about" && <AboutContent />}
      {activeTab === "contact" && <ContactContent />}
    </div>
  );
}

function HomeContent() {
  return <h2>Welcome to the Home Page</h2>;
}

function AboutContent() {
  return <h2>About Us</h2>;
}

function ContactContent() {
  return <h2>Contact Us</h2>;
}
```

### Loading States

A common pattern: show a loading indicator while data is being fetched, then show the actual content when the data arrives, or an error message if something went wrong.

```javascript
function UserList() {
  const [users, setUsers] = useState([]);
  const [isLoading, setIsLoading] = useState(true);
  const [error, setError] = useState(null);

  // Imagine this is called after data fetching (covered in Week 19)
  // For now, focus on how state drives what is rendered

  if (error) {
    return <p style={{ color: "red" }}>Error: {error}</p>;
  }

  if (isLoading) {
    return <p>Loading users...</p>;
  }

  if (users.length === 0) {
    return <p>No users found.</p>;
  }

  return (
    <ul>
      {users.map(user => (
        <li key={user.id}>{user.name}</li>
      ))}
    </ul>
  );
}
```

```
  CONDITIONAL RENDERING DECISION TREE
  ======================================

  Component renders
        |
        v
  Is there an error?
    YES --> Show error message
    NO  --> Continue
              |
              v
        Is it loading?
          YES --> Show spinner / "Loading..."
          NO  --> Continue
                    |
                    v
              Is data empty?
                YES --> Show "No data found"
                NO  --> Show the actual data
```

### Conditional Rendering Techniques Summary

| Technique              | Use Case                                 | Example                                    |
|------------------------|------------------------------------------|--------------------------------------------|
| `&&` operator          | Show something only if condition is true | `{isLoggedIn && <Dashboard />}`            |
| Ternary `? :`          | Choose between two elements              | `{isLoggedIn ? <Dashboard /> : <Login />}` |
| Early return           | Render completely different UI            | `if (isLoading) return <Spinner />;`       |
| Variable assignment    | Complex conditions                       | `let content; if (...) content = ...;`     |

---

## 8. Multiple useState vs One State Object

### Using Multiple useState Calls

```javascript
function UserForm() {
  const [firstName, setFirstName] = useState("");
  const [lastName, setLastName] = useState("");
  const [email, setEmail] = useState("");
  const [age, setAge] = useState(0);
  const [isSubscribed, setIsSubscribed] = useState(false);
}
```

### Using One State Object

```javascript
function UserForm() {
  const [formData, setFormData] = useState({
    firstName: "",
    lastName: "",
    email: "",
    age: 0,
    isSubscribed: false
  });

  function updateField(field, value) {
    setFormData(prev => ({ ...prev, [field]: value }));
  }
}
```

### When to Split vs Combine

| Situation                                          | Recommendation         |
|----------------------------------------------------|------------------------|
| Values change independently (e.g., isOpen, count)  | Separate `useState`    |
| Values always change together (e.g., x and y coords)| One state object      |
| Form with many fields                              | One state object       |
| Two or three unrelated booleans                    | Separate `useState`    |
| Data fetched from API as one unit                  | One state object       |

**General guidance:**

- If two pieces of state always update together, combine them into one object.
- If state values are independent and unrelated, keep them separate.
- If you find yourself calling multiple setters in the same handler, consider combining those values into one object.
- Do not overthink it. Start with multiple `useState` calls. Refactor to an object later if the component gets cluttered.

```
  SPLIT vs COMBINE — DECISION GUIDE
  ====================================

  Do these values change together?
        |
    YES |              NO
        v               v
  Combine into       Keep as separate
  one object         useState calls

  Example (combine):           Example (split):
  const [position, set...] =   const [name, setName] = useState("");
    useState({ x: 0, y: 0 })  const [isOpen, setIsOpen] = useState(false);
                               // name and isOpen are unrelated
```

---

## 9. Summary

### Key Concepts Recap

| Concept                     | Key Takeaway                                                      |
|-----------------------------|-------------------------------------------------------------------|
| State                       | Data owned by a component that changes over time                  |
| Props vs State              | Props are read-only from parent; state is mutable within component|
| `useState`                  | `const [val, setVal] = useState(initial)` -- the core Hook        |
| Rules of Hooks              | Only at top level, only in React functions                        |
| Controlled components       | Input value tied to state via `value` and `onChange`              |
| Uncontrolled components     | DOM holds value, read via `useRef` when needed                   |
| Immutable updates           | Never mutate state -- always create new arrays and objects        |
| Lifting state up            | Move shared state to the closest common parent                   |
| Conditional rendering       | Use `&&`, ternary, or early return based on state                |
| Functional updates          | Use `setCount(prev => prev + 1)` when new state depends on old  |

### State Management Cheat Sheet

```
  STATE LIFECYCLE IN A COMPONENT
  =================================

  1. Initialize
     const [count, setCount] = useState(0);

  2. Read
     <p>{count}</p>

  3. Update (triggers re-render)
     setCount(count + 1);
     // or
     setCount(prev => prev + 1);

  4. React re-renders the component
     with the new state value

  5. Repeat from step 2
```

```
  COMPLETE DATA FLOW DIAGRAM
  ============================

  +-----------------------+
  |   Parent Component    |
  |   (owns state)        |
  |                       |
  |  [data, setData]      |
  +-----------+-----------+
              |
     +--------+--------+
     |                  |
     v                  v
  +----------+    +----------+
  | Child A  |    | Child B  |
  | props:   |    | props:   |
  |  data    |    |  data    |
  |  onUpdate|    |          |
  +----------+    +----------+
       |
       | User clicks button
       | calls onUpdate(newVal)
       |
       v
  Parent's setData(newVal)
       |
       v
  React re-renders Parent
       |
       +---> Child A gets new data via props
       +---> Child B gets new data via props
```

### What is Next?

In **Week 19**, you will learn about **side effects and lifecycle** with the `useEffect` Hook. You will learn how to fetch data from APIs, run code when a component mounts, and clean up resources when a component unmounts.
