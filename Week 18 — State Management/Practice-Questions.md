# Week 18 — State Management: Practice Questions

**Total Questions: 23** (10 MCQs + 5 Short Answer + 8 Coding Exercises)

---

## Part 1: Multiple Choice Questions (MCQs)

**1. What is the correct way to declare a state variable in a functional component?**

- A) `const count = useState(0);`
- B) `const [count, setCount] = useState(0);`
- C) `let count = 0;`
- D) `this.state = { count: 0 };`

<details>
<summary>Answer</summary>

**B) `const [count, setCount] = useState(0);`**

The `useState` hook returns an array with two elements: the current state value and a function to update it. Array destructuring is used to assign meaningful names. Option D is the class component syntax and is not used in functional components.
</details>

---

**2. What happens when you call a state setter function (e.g., `setCount(5)`)?**

- A) The variable `count` is immediately updated to 5
- B) React schedules a re-render, and `count` will be 5 on the next render
- C) The DOM is updated immediately
- D) Nothing happens until you call `forceUpdate()`

<details>
<summary>Answer</summary>

**B) React schedules a re-render, and `count` will be 5 on the next render**

State updates in React are asynchronous. When you call a setter function, React does not update the variable immediately. Instead, it schedules a re-render of the component, during which the new state value is used. This means you cannot read the updated value immediately after calling the setter within the same execution context.
</details>

---

**3. Why should you NOT directly mutate state in React?**

```jsx
// Example of direct mutation
const [items, setItems] = useState(["a", "b"]);
items.push("c"); // Direct mutation
```

- A) It will throw a syntax error
- B) React will not detect the change and will not re-render the component
- C) It causes the entire application to crash
- D) It is only a problem in class components

<details>
<summary>Answer</summary>

**B) React will not detect the change and will not re-render the component**

React relies on reference comparison to determine if state has changed. When you mutate an object or array directly, the reference stays the same, so React does not know that the data has changed and will not trigger a re-render. You must create a new array or object (e.g., using the spread operator) and pass it to the setter function.
</details>

---

**4. What is a controlled component in React?**

- A) A component that has no state
- B) A form element whose value is controlled by React state
- C) A component wrapped in a higher-order component
- D) A component that cannot be re-rendered

<details>
<summary>Answer</summary>

**B) A form element whose value is controlled by React state**

In a controlled component, form elements like `<input>`, `<textarea>`, and `<select>` have their values tied to React state. The component's state is the "single source of truth," and changes are handled through event handlers that update the state. For example: `<input value={name} onChange={(e) => setName(e.target.value)} />`.
</details>

---

**5. What is the correct way to update state based on the previous state value?**

- A) `setCount(count + 1);`
- B) `setCount((prevCount) => prevCount + 1);`
- C) `setCount(count++);`
- D) `count = count + 1; setCount(count);`

<details>
<summary>Answer</summary>

**B) `setCount((prevCount) => prevCount + 1);`**

When the new state depends on the previous state, you should use the functional form of the setter, which receives the most recent state value as its argument. Option A can lead to stale state bugs if multiple updates are batched together, because `count` may not reflect the latest value. Option C mutates the variable directly, and option D also mutates before setting.
</details>

---

**6. What does "lifting state up" mean in React?**

- A) Moving state from a child component to a parent component so it can be shared
- B) Moving state to a global variable
- C) Increasing the value of a state variable
- D) Transferring state from the server to the client

<details>
<summary>Answer</summary>

**A) Moving state from a child component to a parent component so it can be shared**

When two or more sibling components need to share the same data, the state should be "lifted up" to their closest common ancestor. The parent component manages the state and passes it down as props, along with any callback functions needed to update it. This ensures a single source of truth for the shared data.
</details>

---

**7. What is the output of the following code when the button is clicked once?**

```jsx
function Counter() {
  const [count, setCount] = useState(0);

  function handleClick() {
    setCount(count + 1);
    setCount(count + 1);
    setCount(count + 1);
  }

  return <button onClick={handleClick}>Count: {count}</button>;
}
```

- A) `Count: 3`
- B) `Count: 1`
- C) `Count: 0`
- D) An error is thrown

<details>
<summary>Answer</summary>

**B) `Count: 1`**

All three `setCount(count + 1)` calls use the same `count` value from the current render (which is `0`). So each call effectively sets the count to `0 + 1 = 1`. Since React batches state updates, the result after one click is `1`, not `3`. To get `3`, you would need to use the functional updater form: `setCount(prev => prev + 1)`.
</details>

---

**8. Which of the following correctly adds a new item to a state array?**

- A) `items.push(newItem); setItems(items);`
- B) `setItems([...items, newItem]);`
- C) `setItems(items.concat(newItem));`
- D) Both B and C

<details>
<summary>Answer</summary>

**D) Both B and C**

Both the spread operator (`[...items, newItem]`) and `concat()` create a new array, which is required for React to detect the state change. Option A directly mutates the original array and passes the same reference, so React will not re-render.
</details>

---

**9. When does a React component re-render?**

- A) Only when its props change
- B) Only when its state changes
- C) When its state changes, when its props change, or when its parent re-renders
- D) Only when `forceUpdate()` is called

<details>
<summary>Answer</summary>

**C) When its state changes, when its props change, or when its parent re-renders**

A React component re-renders in several scenarios: when its own state is updated via a setter function, when it receives new props from its parent, or when its parent component re-renders (even if the child's props have not changed). Understanding these triggers is essential for optimizing performance.
</details>

---

**10. What is the correct way to handle multiple form inputs with a single state object?**

- A) Create a separate `useState` for each input
- B) Use a single state object and update it with the spread operator
- C) Use `document.getElementById()` to read values
- D) Both A and B are valid approaches

<details>
<summary>Answer</summary>

**D) Both A and B are valid approaches**

For forms with a small number of inputs, using separate `useState` calls (option A) keeps the code simple. For forms with many inputs, using a single state object (option B) reduces repetition:

```jsx
const [form, setForm] = useState({ name: "", email: "" });
const handleChange = (e) => {
  setForm({ ...form, [e.target.name]: e.target.value });
};
```

Both approaches are valid and commonly used in React applications.
</details>

---

## Part 2: Short Answer Questions

**1. What is the difference between state and props in React?**

<details>
<summary>Answer</summary>

State and props are both mechanisms for managing data in React, but they serve different purposes. State is internal data owned and managed by the component itself. It is mutable (through setter functions), private to the component, and causes a re-render when updated. Props are external data passed from a parent component to a child. They are read-only from the child's perspective and cannot be modified by the receiving component. State represents data that changes over time within a component, while props represent configuration or data passed in from the outside. A useful analogy: props are like function arguments, while state is like local variables declared inside the function.
</details>

---

**2. What is the difference between a controlled and an uncontrolled component?**

<details>
<summary>Answer</summary>

A controlled component is a form element whose value is managed by React state. The component's state serves as the single source of truth, and every change to the input is handled through an `onChange` event handler that updates the state. For example: `<input value={name} onChange={(e) => setName(e.target.value)} />`.

An uncontrolled component is a form element that manages its own internal state through the DOM, similar to traditional HTML forms. The value is accessed using a `ref` (via `useRef`) when needed, rather than being tracked in React state on every keystroke. For example: `<input ref={inputRef} />` where you read `inputRef.current.value` when the form is submitted.

Controlled components are generally preferred because they give React full control over the form data, making it easier to validate, transform, or conditionally render based on the current input values.
</details>

---

**3. Why should you never directly mutate state in React? Provide an example of the correct approach.**

<details>
<summary>Answer</summary>

You should never directly mutate state because React uses reference comparison to determine if state has changed. When you mutate an object or array in place, the reference remains the same, so React does not detect any change and will not re-render the component.

Incorrect approach (direct mutation):
```jsx
const [user, setUser] = useState({ name: "Alice", age: 25 });
user.age = 26;       // Mutates the existing object
setUser(user);       // Same reference -- React will not re-render
```

Correct approach (creating a new object):
```jsx
const [user, setUser] = useState({ name: "Alice", age: 25 });
setUser({ ...user, age: 26 }); // Creates a new object with the updated value
```

The spread operator creates a shallow copy of the object with the updated property, producing a new reference that React can detect as a change.
</details>

---

**4. What does "lifting state up" mean, and when should you do it?**

<details>
<summary>Answer</summary>

"Lifting state up" is the practice of moving state from a child component to the nearest common ancestor (parent) component when multiple components need to share or synchronize the same data. The parent then passes the state down as props and provides callback functions for children to request changes.

You should lift state up when two or more sibling components need to reflect the same changing data. For example, if a temperature converter has both Celsius and Fahrenheit inputs that must stay synchronized, the shared temperature value should be stored in their common parent, not in each input separately.

The process involves three steps: (1) remove state from the child components, (2) add the state to the closest common parent, and (3) pass the state and update handlers down as props. This ensures a single source of truth and keeps the components in sync.
</details>

---

**5. What is the functional updater form of `useState`, and when should you use it?**

<details>
<summary>Answer</summary>

The functional updater form is when you pass a function (instead of a value) to a state setter. The function receives the most recent state value as its argument and returns the new state.

```jsx
setCount((prevCount) => prevCount + 1);
```

You should use the functional updater form whenever the new state depends on the previous state. This is important because React batches state updates for performance. If you call `setCount(count + 1)` multiple times in the same event handler, each call uses the same stale `count` value from the current render. With the functional form, each call receives the most up-to-date value:

```jsx
// Without functional updater: count goes from 0 to 1 (not 3)
setCount(count + 1);
setCount(count + 1);
setCount(count + 1);

// With functional updater: count goes from 0 to 3
setCount((prev) => prev + 1);
setCount((prev) => prev + 1);
setCount((prev) => prev + 1);
```
</details>

---

## Part 3: Coding Exercises

**Exercise 1: Counter App**

Build a `Counter` component with increment, decrement, and reset buttons. The counter should not go below zero.

<details>
<summary>Solution</summary>

```jsx
import { useState } from "react";

function Counter() {
  const [count, setCount] = useState(0);

  const increment = () => setCount((prev) => prev + 1);
  const decrement = () => setCount((prev) => Math.max(0, prev - 1));
  const reset = () => setCount(0);

  return (
    <div className="counter">
      <h1>Counter: {count}</h1>
      <div className="counter-buttons">
        <button onClick={decrement}>-</button>
        <button onClick={reset}>Reset</button>
        <button onClick={increment}>+</button>
      </div>
      {count === 0 && <p className="message">Counter is at minimum value.</p>}
    </div>
  );
}

export default Counter;
```

**Key Points:**
- `Math.max(0, prev - 1)` prevents the counter from going below zero.
- The functional updater form (`prev => ...`) ensures accurate updates.
- Conditional rendering shows a message when the counter is at zero.
</details>

---

**Exercise 2: Toggle Visibility**

Create a component that toggles the visibility of a paragraph when a button is clicked. The button text should change based on the current visibility state.

<details>
<summary>Solution</summary>

```jsx
import { useState } from "react";

function ToggleContent() {
  const [isVisible, setIsVisible] = useState(false);

  const toggleVisibility = () => setIsVisible((prev) => !prev);

  return (
    <div className="toggle-content">
      <h2>Toggle Visibility Demo</h2>

      <button onClick={toggleVisibility}>
        {isVisible ? "Hide Content" : "Show Content"}
      </button>

      {isVisible && (
        <div className="content-box">
          <p>
            This paragraph is conditionally rendered based on the isVisible state.
            Click the button above to hide it again.
          </p>
        </div>
      )}
    </div>
  );
}

export default ToggleContent;
```

**Key Points:**
- A boolean state variable controls visibility.
- The logical NOT operator (`!prev`) flips the boolean.
- The button text dynamically changes using a ternary operator.
- The `&&` operator conditionally renders the content.
</details>

---

**Exercise 3: Form with Multiple Inputs**

Create a registration form with name, email, and password fields using a single state object. Display the entered values in real time below the form.

<details>
<summary>Solution</summary>

```jsx
import { useState } from "react";

function RegistrationForm() {
  const [formData, setFormData] = useState({
    name: "",
    email: "",
    password: "",
  });

  const handleChange = (e) => {
    const { name, value } = e.target;
    setFormData((prev) => ({
      ...prev,
      [name]: value,
    }));
  };

  const handleSubmit = (e) => {
    e.preventDefault();
    console.log("Form submitted:", formData);
    alert(`Welcome, ${formData.name}!`);
  };

  return (
    <div className="registration-form">
      <h2>Register</h2>

      <form onSubmit={handleSubmit}>
        <div className="form-group">
          <label htmlFor="name">Name:</label>
          <input
            type="text"
            id="name"
            name="name"
            value={formData.name}
            onChange={handleChange}
            placeholder="Enter your name"
          />
        </div>

        <div className="form-group">
          <label htmlFor="email">Email:</label>
          <input
            type="email"
            id="email"
            name="email"
            value={formData.email}
            onChange={handleChange}
            placeholder="Enter your email"
          />
        </div>

        <div className="form-group">
          <label htmlFor="password">Password:</label>
          <input
            type="password"
            id="password"
            name="password"
            value={formData.password}
            onChange={handleChange}
            placeholder="Enter your password"
          />
        </div>

        <button type="submit">Register</button>
      </form>

      <div className="preview">
        <h3>Live Preview:</h3>
        <p><strong>Name:</strong> {formData.name || "Not entered"}</p>
        <p><strong>Email:</strong> {formData.email || "Not entered"}</p>
        <p><strong>Password:</strong> {"*".repeat(formData.password.length) || "Not entered"}</p>
      </div>
    </div>
  );
}

export default RegistrationForm;
```

**Key Points:**
- A single state object manages all form fields.
- Computed property names (`[name]: value`) allow a single handler for all inputs.
- The spread operator creates a new object on each update to maintain immutability.
- The password is masked in the preview using `"*".repeat()`.
</details>

---

**Exercise 4: Todo List (Add and Delete)**

Build a todo list application where users can add new todos and delete existing ones. Each todo should have a unique ID.

<details>
<summary>Solution</summary>

```jsx
import { useState } from "react";

function TodoList() {
  const [todos, setTodos] = useState([
    { id: 1, text: "Learn React basics" },
    { id: 2, text: "Practice useState" },
  ]);
  const [inputValue, setInputValue] = useState("");

  const addTodo = (e) => {
    e.preventDefault();

    if (inputValue.trim() === "") return;

    const newTodo = {
      id: Date.now(),
      text: inputValue.trim(),
    };

    setTodos((prev) => [...prev, newTodo]);
    setInputValue("");
  };

  const deleteTodo = (id) => {
    setTodos((prev) => prev.filter((todo) => todo.id !== id));
  };

  return (
    <div className="todo-app">
      <h2>Todo List</h2>

      <form onSubmit={addTodo} className="todo-form">
        <input
          type="text"
          value={inputValue}
          onChange={(e) => setInputValue(e.target.value)}
          placeholder="Add a new todo..."
        />
        <button type="submit">Add</button>
      </form>

      <p className="todo-count">{todos.length} item(s)</p>

      <ul className="todo-list">
        {todos.map((todo) => (
          <li key={todo.id} className="todo-item">
            <span>{todo.text}</span>
            <button
              className="delete-btn"
              onClick={() => deleteTodo(todo.id)}
            >
              Delete
            </button>
          </li>
        ))}
      </ul>

      {todos.length === 0 && (
        <p className="empty-message">No todos yet. Add one above!</p>
      )}
    </div>
  );
}

export default TodoList;
```

**Key Points:**
- `Date.now()` generates unique IDs (sufficient for a client-side app).
- The spread operator adds items without mutating the original array.
- `filter()` removes items by creating a new array that excludes the deleted item.
- Empty input validation prevents adding blank todos.
</details>

---

**Exercise 5: Color Picker**

Create a color picker component that lets the user choose from predefined colors or enter a custom hex code. Display a preview box that updates in real time.

<details>
<summary>Solution</summary>

```jsx
import { useState } from "react";

function ColorPicker() {
  const [selectedColor, setSelectedColor] = useState("#3498db");
  const [customColor, setCustomColor] = useState("");

  const presetColors = [
    { name: "Blue", hex: "#3498db" },
    { name: "Red", hex: "#e74c3c" },
    { name: "Green", hex: "#2ecc71" },
    { name: "Purple", hex: "#9b59b6" },
    { name: "Orange", hex: "#e67e22" },
    { name: "Dark", hex: "#2c3e50" },
  ];

  const handleCustomColor = (e) => {
    const value = e.target.value;
    setCustomColor(value);

    if (/^#[0-9A-Fa-f]{6}$/.test(value)) {
      setSelectedColor(value);
    }
  };

  return (
    <div className="color-picker">
      <h2>Color Picker</h2>

      <div
        className="color-preview"
        style={{
          backgroundColor: selectedColor,
          width: "200px",
          height: "200px",
          borderRadius: "12px",
          margin: "20px auto",
        }}
      />

      <p className="color-value">Selected: {selectedColor}</p>

      <div className="preset-colors">
        <h3>Preset Colors</h3>
        <div className="color-grid">
          {presetColors.map((color) => (
            <button
              key={color.hex}
              className={`color-swatch ${selectedColor === color.hex ? "active" : ""}`}
              style={{ backgroundColor: color.hex }}
              onClick={() => setSelectedColor(color.hex)}
              title={color.name}
            />
          ))}
        </div>
      </div>

      <div className="custom-color">
        <h3>Custom Color</h3>
        <input
          type="text"
          value={customColor}
          onChange={handleCustomColor}
          placeholder="#ff5733"
          maxLength={7}
        />
      </div>
    </div>
  );
}

export default ColorPicker;
```

**Key Points:**
- Two state variables manage the selected color and the custom input independently.
- Inline styles use the `style` prop with a JavaScript object (camelCase properties).
- Regex validation ensures only valid hex codes update the preview.
- Preset colors are rendered from an array, making it easy to add or remove options.
</details>

---

**Exercise 6: Shopping Cart (Add, Remove, and Quantity)**

Build a shopping cart that allows users to add products, adjust quantities, and remove items. Display the total price.

<details>
<summary>Solution</summary>

```jsx
import { useState } from "react";

function ShoppingCart() {
  const [cart, setCart] = useState([]);

  const products = [
    { id: 1, name: "Laptop", price: 999.99 },
    { id: 2, name: "Mouse", price: 29.99 },
    { id: 3, name: "Keyboard", price: 59.99 },
    { id: 4, name: "Monitor", price: 349.99 },
    { id: 5, name: "Headphones", price: 79.99 },
  ];

  const addToCart = (product) => {
    setCart((prev) => {
      const existingItem = prev.find((item) => item.id === product.id);

      if (existingItem) {
        return prev.map((item) =>
          item.id === product.id
            ? { ...item, quantity: item.quantity + 1 }
            : item
        );
      }

      return [...prev, { ...product, quantity: 1 }];
    });
  };

  const updateQuantity = (id, delta) => {
    setCart((prev) =>
      prev
        .map((item) =>
          item.id === id
            ? { ...item, quantity: item.quantity + delta }
            : item
        )
        .filter((item) => item.quantity > 0)
    );
  };

  const removeFromCart = (id) => {
    setCart((prev) => prev.filter((item) => item.id !== id));
  };

  const totalPrice = cart.reduce(
    (sum, item) => sum + item.price * item.quantity,
    0
  );

  const totalItems = cart.reduce((sum, item) => sum + item.quantity, 0);

  return (
    <div className="shopping-cart-app">
      <h2>Shop</h2>

      <div className="product-list">
        {products.map((product) => (
          <div key={product.id} className="product-item">
            <span>{product.name} - ${product.price.toFixed(2)}</span>
            <button onClick={() => addToCart(product)}>Add to Cart</button>
          </div>
        ))}
      </div>

      <h2>Cart ({totalItems} items)</h2>

      {cart.length === 0 ? (
        <p>Your cart is empty.</p>
      ) : (
        <>
          <ul className="cart-list">
            {cart.map((item) => (
              <li key={item.id} className="cart-item">
                <span className="item-name">{item.name}</span>
                <div className="quantity-controls">
                  <button onClick={() => updateQuantity(item.id, -1)}>-</button>
                  <span className="quantity">{item.quantity}</span>
                  <button onClick={() => updateQuantity(item.id, 1)}>+</button>
                </div>
                <span className="item-total">
                  ${(item.price * item.quantity).toFixed(2)}
                </span>
                <button
                  className="remove-btn"
                  onClick={() => removeFromCart(item.id)}
                >
                  Remove
                </button>
              </li>
            ))}
          </ul>

          <div className="cart-total">
            <strong>Total: ${totalPrice.toFixed(2)}</strong>
          </div>
        </>
      )}
    </div>
  );
}

export default ShoppingCart;
```

**Key Points:**
- Adding an existing product increments its quantity instead of duplicating it.
- `updateQuantity` handles both increment and decrement with a single function using a `delta` parameter.
- Items with a quantity of zero are automatically removed using `.filter()`.
- The total price and item count are derived values computed from the cart state, not stored as separate state.
</details>

---

**Exercise 7: Tabs Component**

Build a `Tabs` component that displays multiple tab buttons and shows the content of the selected tab. Only one tab can be active at a time.

<details>
<summary>Solution</summary>

```jsx
import { useState } from "react";

function Tabs({ tabs }) {
  const [activeIndex, setActiveIndex] = useState(0);

  return (
    <div className="tabs-component">
      <div className="tab-buttons">
        {tabs.map((tab, index) => (
          <button
            key={tab.label}
            className={`tab-btn ${activeIndex === index ? "active" : ""}`}
            onClick={() => setActiveIndex(index)}
          >
            {tab.label}
          </button>
        ))}
      </div>

      <div className="tab-content">
        {tabs[activeIndex].content}
      </div>
    </div>
  );
}

function App() {
  const tabData = [
    {
      label: "Overview",
      content: (
        <div>
          <h3>Project Overview</h3>
          <p>This project is a MERN stack application designed to manage tasks
             and improve team collaboration.</p>
        </div>
      ),
    },
    {
      label: "Features",
      content: (
        <div>
          <h3>Key Features</h3>
          <ul>
            <li>User authentication and authorization</li>
            <li>Real-time task updates</li>
            <li>Team collaboration tools</li>
            <li>Analytics dashboard</li>
          </ul>
        </div>
      ),
    },
    {
      label: "Settings",
      content: (
        <div>
          <h3>Settings</h3>
          <p>Configure your account preferences, notification settings,
             and display options here.</p>
        </div>
      ),
    },
  ];

  return (
    <div className="app">
      <h1>Dashboard</h1>
      <Tabs tabs={tabData} />
    </div>
  );
}

export default App;
```

**Key Points:**
- `activeIndex` state tracks which tab is currently selected.
- Only the content of the active tab is rendered, controlled by array indexing.
- The `Tabs` component is generic and reusable -- it accepts any array of tab objects.
- Active tab styling is applied by comparing the current index to `activeIndex`.
</details>

---

**Exercise 8: Complete Contact Form with Validation**

Build a comprehensive contact form with name, email, phone, and message fields. Implement client-side validation with error messages and a submission success state.

<details>
<summary>Solution</summary>

```jsx
import { useState } from "react";

function ContactForm() {
  const [formData, setFormData] = useState({
    name: "",
    email: "",
    phone: "",
    message: "",
  });

  const [errors, setErrors] = useState({});
  const [isSubmitted, setIsSubmitted] = useState(false);

  const handleChange = (e) => {
    const { name, value } = e.target;
    setFormData((prev) => ({ ...prev, [name]: value }));

    // Clear the error for this field as the user types
    if (errors[name]) {
      setErrors((prev) => {
        const updated = { ...prev };
        delete updated[name];
        return updated;
      });
    }
  };

  const validate = () => {
    const newErrors = {};

    if (formData.name.trim().length < 2) {
      newErrors.name = "Name must be at least 2 characters.";
    }

    const emailRegex = /^[^\s@]+@[^\s@]+\.[^\s@]+$/;
    if (!emailRegex.test(formData.email)) {
      newErrors.email = "Please enter a valid email address.";
    }

    const phoneRegex = /^[0-9]{10,15}$/;
    if (formData.phone && !phoneRegex.test(formData.phone.replace(/[\s-()]/g, ""))) {
      newErrors.phone = "Please enter a valid phone number.";
    }

    if (formData.message.trim().length < 10) {
      newErrors.message = "Message must be at least 10 characters.";
    }

    return newErrors;
  };

  const handleSubmit = (e) => {
    e.preventDefault();
    const validationErrors = validate();

    if (Object.keys(validationErrors).length > 0) {
      setErrors(validationErrors);
      return;
    }

    console.log("Form submitted:", formData);
    setIsSubmitted(true);
  };

  const handleReset = () => {
    setFormData({ name: "", email: "", phone: "", message: "" });
    setErrors({});
    setIsSubmitted(false);
  };

  if (isSubmitted) {
    return (
      <div className="success-message">
        <h2>Thank You!</h2>
        <p>Your message has been sent successfully.</p>
        <p>We will get back to you at <strong>{formData.email}</strong>.</p>
        <button onClick={handleReset}>Send Another Message</button>
      </div>
    );
  }

  return (
    <div className="contact-form">
      <h2>Contact Us</h2>

      <form onSubmit={handleSubmit}>
        <div className="form-group">
          <label htmlFor="name">Name *</label>
          <input
            type="text"
            id="name"
            name="name"
            value={formData.name}
            onChange={handleChange}
            className={errors.name ? "input-error" : ""}
            placeholder="Your full name"
          />
          {errors.name && <span className="error">{errors.name}</span>}
        </div>

        <div className="form-group">
          <label htmlFor="email">Email *</label>
          <input
            type="email"
            id="email"
            name="email"
            value={formData.email}
            onChange={handleChange}
            className={errors.email ? "input-error" : ""}
            placeholder="you@example.com"
          />
          {errors.email && <span className="error">{errors.email}</span>}
        </div>

        <div className="form-group">
          <label htmlFor="phone">Phone (optional)</label>
          <input
            type="tel"
            id="phone"
            name="phone"
            value={formData.phone}
            onChange={handleChange}
            className={errors.phone ? "input-error" : ""}
            placeholder="1234567890"
          />
          {errors.phone && <span className="error">{errors.phone}</span>}
        </div>

        <div className="form-group">
          <label htmlFor="message">Message *</label>
          <textarea
            id="message"
            name="message"
            value={formData.message}
            onChange={handleChange}
            className={errors.message ? "input-error" : ""}
            placeholder="Write your message here..."
            rows={5}
          />
          {errors.message && <span className="error">{errors.message}</span>}
          <small>{formData.message.length}/500 characters</small>
        </div>

        <div className="form-actions">
          <button type="submit">Send Message</button>
          <button type="button" onClick={handleReset}>
            Clear Form
          </button>
        </div>
      </form>
    </div>
  );
}

export default ContactForm;
```

**Key Points:**
- A single `handleChange` function manages all inputs via computed property names.
- Validation runs on submit, and errors are stored in a separate state object.
- Errors are cleared for individual fields as the user types, providing immediate feedback.
- The form transitions to a success state upon valid submission.
- The phone field is optional, so it is only validated when a value is provided.
- A character counter helps users stay within the expected message length.
</details>
