# Week 17 — Props & Component Communication: Practice Questions

**Total Questions: 20** (10 MCQs + 5 Short Answer + 5 Coding Exercises)

---

## Part 1: Multiple Choice Questions (MCQs)

**1. What are props in React?**

- A) Internal data managed by a component
- B) Read-only inputs passed from a parent component to a child component
- C) Global variables accessible by all components
- D) CSS properties used for styling components

<details>
<summary>Answer</summary>

**B) Read-only inputs passed from a parent component to a child component**

Props (short for "properties") are the mechanism by which data flows from parent to child components in React. They are read-only, meaning the child component cannot modify the props it receives.
</details>

---

**2. What happens if you try to modify a prop directly inside a child component?**

- A) The prop is updated successfully
- B) The parent component re-renders automatically
- C) React throws an error or the behavior is undefined (props are read-only)
- D) The change is saved and persisted across re-renders

<details>
<summary>Answer</summary>

**C) React throws an error or the behavior is undefined (props are read-only)**

Props follow a one-way data flow from parent to child. Attempting to directly mutate a prop violates React's design principles and can lead to bugs. If a child needs to communicate a change back to the parent, it should invoke a callback function passed down as a prop.
</details>

---

**3. How do you set a default value for a prop in a functional component?**

- A) `function Button(props = { color: "blue" })`
- B) `function Button({ color = "blue" })`
- C) `Button.defaultProps = { color: "blue" }` (only option)
- D) `function Button(color: "blue")`

<details>
<summary>Answer</summary>

**B) `function Button({ color = "blue" })`**

In modern React with functional components, default prop values are set using JavaScript default parameter syntax during destructuring. While `defaultProps` (option C) also works, default parameters are the preferred and more idiomatic approach.
</details>

---

**4. What is the `children` prop in React?**

- A) An array of all child components in the application
- B) The content placed between the opening and closing tags of a component
- C) A special prop that stores the component's state
- D) A method for creating nested routes

<details>
<summary>Answer</summary>

**B) The content placed between the opening and closing tags of a component**

The `children` prop is a special prop automatically provided by React. It contains whatever JSX or content is placed between the opening and closing tags when a component is used: `<Card>This is children</Card>`. This pattern is fundamental to component composition.
</details>

---

**5. What is the correct way to pass a number as a prop?**

- A) `<Product price="29.99" />`
- B) `<Product price={29.99} />`
- C) `<Product price=29.99 />`
- D) `<Product price=(29.99) />`

<details>
<summary>Answer</summary>

**B) `<Product price={29.99} />`**

Non-string values (numbers, booleans, arrays, objects, functions) must be passed inside curly braces `{}`. Option A would pass the string `"29.99"` instead of the number `29.99`, which could cause unexpected behavior in calculations.
</details>

---

**6. Why is the `key` prop important when rendering lists?**

- A) It applies CSS styling to list items
- B) It helps React identify which items have changed, been added, or removed
- C) It makes list items clickable
- D) It determines the rendering order of elements

<details>
<summary>Answer</summary>

**B) It helps React identify which items have changed, been added, or removed**

The `key` prop is used by React's reconciliation algorithm to efficiently update lists. Keys should be stable, unique identifiers (such as database IDs). Using array indices as keys is discouraged when the list order can change, as it can lead to rendering bugs and degraded performance.
</details>

---

**7. Which of the following demonstrates correct component composition?**

- A)
```jsx
<Layout>
  <Header />
  <Content />
  <Footer />
</Layout>
```

- B)
```jsx
<Layout components={[Header, Content, Footer]} />
```

- C)
```jsx
<Layout header="Header" content="Content" footer="Footer" />
```

- D)
```jsx
Layout(Header, Content, Footer)
```

<details>
<summary>Answer</summary>

**A)**
```jsx
<Layout>
  <Header />
  <Content />
  <Footer />
</Layout>
```

This demonstrates the composition pattern using the `children` prop. The `Layout` component receives `Header`, `Content`, and `Footer` as its children and can render them within its own structure. This approach is flexible, readable, and follows React's compositional model.
</details>

---

**8. What does "one-way data flow" mean in React?**

- A) Data can only flow from the server to the client
- B) Data flows from parent components to child components, not the other way around
- C) Components can only read data once
- D) Data is passed only through global variables

<details>
<summary>Answer</summary>

**B) Data flows from parent components to child components, not the other way around**

One-way data flow (also called "unidirectional data flow") means that props are passed down from parent to child. If a child needs to send data back to a parent, it does so by calling a callback function that the parent passed down as a prop. This makes the data flow predictable and easier to debug.
</details>

---

**9. What is the output of the following code?**

```jsx
function Welcome({ name, greeting = "Hello" }) {
  return <p>{greeting}, {name}!</p>;
}

function App() {
  return (
    <div>
      <Welcome name="Alice" greeting="Hi" />
      <Welcome name="Bob" />
    </div>
  );
}
```

- A) `Hi, Alice!` and `Hello, Bob!`
- B) `Hello, Alice!` and `Hello, Bob!`
- C) `Hi, Alice!` and `undefined, Bob!`
- D) An error is thrown

<details>
<summary>Answer</summary>

**A) `Hi, Alice!` and `Hello, Bob!`**

The first `<Welcome>` receives `greeting="Hi"`, which overrides the default value. The second `<Welcome>` does not receive a `greeting` prop, so the default value `"Hello"` is used. This demonstrates how default parameter values work with props.
</details>

---

**10. Which of the following is NOT a valid way to pass props?**

- A) `<User {...userData} />`
- B) `<User name="Alice" age={30} />`
- C) `<User props={{ name: "Alice", age: 30 }} />`
- D) `<User name="Alice" isActive={true} />`

<details>
<summary>Answer</summary>

**C) `<User props={{ name: "Alice", age: 30 }} />`**

Option C passes a single prop called `props` with an object value, which is not how props are intended to be used. Options A (spread syntax), B (individual props), and D (individual props with a boolean) are all valid. With option A, each property of `userData` becomes a separate prop on the `User` component.
</details>

---

## Part 2: Short Answer Questions

**1. What is the difference between props and state in React?**

<details>
<summary>Answer</summary>

Props and state are both plain JavaScript data that influence what a component renders, but they differ in important ways. Props are passed from a parent component to a child component and are read-only within the child; the child cannot modify its own props. State, on the other hand, is managed internally by the component itself using hooks like `useState`. State can be updated by the component that owns it, and when state changes, the component re-renders. In summary, props are external inputs (controlled by the parent), while state is internal data (controlled by the component itself).
</details>

---

**2. What is the `children` prop, and how does it enable component composition?**

<details>
<summary>Answer</summary>

The `children` prop is a special prop in React that contains the content placed between a component's opening and closing tags. For example, in `<Card><p>Hello</p></Card>`, the `<p>Hello</p>` element is passed as `children` to the `Card` component. This enables component composition because it allows you to create wrapper or layout components that do not need to know their content in advance. A `Card` component can provide structure and styling, while the parent decides what content goes inside it. This pattern promotes reusability and separation of concerns, as components can be combined like building blocks without tightly coupling their implementations.
</details>

---

**3. Why are keys important in React lists, and what makes a good key?**

<details>
<summary>Answer</summary>

Keys are important because they help React's reconciliation algorithm identify individual items in a list. When a list changes (items added, removed, or reordered), React uses keys to determine which items need to be re-rendered, moved, or destroyed. Without proper keys, React may unnecessarily recreate DOM elements or associate the wrong state with the wrong item.

A good key is a value that is (1) unique among siblings -- no two items in the same list should share a key, (2) stable -- the same item should always produce the same key across re-renders, and (3) predictable -- ideally derived from the data itself (e.g., a database ID or a unique field). Using array indices as keys is generally discouraged because they fail the stability requirement when items are reordered, inserted, or deleted.
</details>

---

**4. What is component composition in React, and why is it preferred over component inheritance?**

<details>
<summary>Answer</summary>

Component composition is the practice of building complex UIs by combining simpler, reusable components together, much like assembling building blocks. Instead of creating specialized components through inheritance hierarchies, you create general-purpose components and combine them using props and the `children` prop.

Composition is preferred over inheritance for several reasons. It provides greater flexibility because components can be assembled in many different ways without modifying their source code. It keeps components simple and focused on a single responsibility. It avoids the fragile coupling that comes with deep inheritance chains. The React team officially recommends composition over inheritance, noting that in years of working with thousands of React components, they have not found any use case where inheritance is necessary.
</details>

---

**5. Explain how a child component can communicate data back to its parent in React.**

<details>
<summary>Answer</summary>

Since React enforces one-way data flow (parent to child), a child component communicates data back to its parent by invoking a callback function that the parent passes down as a prop. The parent defines a function that handles the data, passes that function as a prop to the child, and the child calls it when the relevant event occurs.

For example, a parent might pass an `onSubmit` function to a form component. When the user submits the form, the child calls `onSubmit(formData)`, effectively sending the form data up to the parent. The parent can then update its own state based on the received data, which may trigger a re-render of both the parent and child.
</details>

---

## Part 3: Coding Exercises

**Exercise 1: Create a Button Component with Variant Props**

Create a reusable `Button` component that accepts `variant` (primary, secondary, danger), `size` (small, medium, large), and `onClick` props. Render several buttons with different configurations.

<details>
<summary>Solution</summary>

```jsx
function Button({ variant = "primary", size = "medium", onClick, children }) {
  const baseClass = "btn";
  const variantClass = `btn-${variant}`;
  const sizeClass = `btn-${size}`;

  return (
    <button
      className={`${baseClass} ${variantClass} ${sizeClass}`}
      onClick={onClick}
    >
      {children}
    </button>
  );
}

function App() {
  const handleClick = (message) => {
    alert(message);
  };

  return (
    <div className="app">
      <h1>Button Variants</h1>

      <Button variant="primary" size="large" onClick={() => handleClick("Primary clicked!")}>
        Primary Button
      </Button>

      <Button variant="secondary" size="medium" onClick={() => handleClick("Secondary clicked!")}>
        Secondary Button
      </Button>

      <Button variant="danger" size="small" onClick={() => handleClick("Danger clicked!")}>
        Delete
      </Button>

      {/* Using defaults: primary variant, medium size */}
      <Button onClick={() => handleClick("Default clicked!")}>
        Default Button
      </Button>
    </div>
  );
}

export default App;
```

**Key Points:**
- Default values ensure the component works even when optional props are omitted.
- The `children` prop is used for the button label, making the component flexible.
- Dynamic class names are constructed from the prop values.
</details>

---

**Exercise 2: Card Component with Children**

Create a `Card` component that uses the `children` prop to display any content inside a styled card wrapper. The card should also accept an optional `title` prop.

<details>
<summary>Solution</summary>

```jsx
function Card({ title, children }) {
  return (
    <div className="card">
      {title && <h2 className="card-title">{title}</h2>}
      <div className="card-body">
        {children}
      </div>
    </div>
  );
}

function App() {
  return (
    <div className="app">
      <Card title="User Profile">
        <img src="https://via.placeholder.com/100" alt="Avatar" />
        <p>Name: Jane Doe</p>
        <p>Role: Developer</p>
      </Card>

      <Card title="Statistics">
        <ul>
          <li>Projects: 12</li>
          <li>Commits: 340</li>
          <li>Stars: 89</li>
        </ul>
      </Card>

      <Card>
        <p>This card has no title, only body content.</p>
      </Card>
    </div>
  );
}

export default App;
```

**Key Points:**
- The `children` prop allows any JSX to be placed inside the `Card` component.
- Conditional rendering (`title &&`) ensures the title section only appears when a title is provided.
- The same component can display entirely different content depending on what is passed as children.
</details>

---

**Exercise 3: UserList that Maps a User Array**

Create a `UserList` component that receives an array of user objects and renders each user using a separate `UserCard` component. Each user has `id`, `name`, `email`, and `role` properties.

<details>
<summary>Solution</summary>

```jsx
function UserCard({ name, email, role }) {
  return (
    <div className="user-card">
      <h3>{name}</h3>
      <p>Email: {email}</p>
      <span className={`role-badge role-${role.toLowerCase()}`}>
        {role}
      </span>
    </div>
  );
}

function UserList({ users }) {
  if (users.length === 0) {
    return <p className="empty-message">No users found.</p>;
  }

  return (
    <div className="user-list">
      {users.map((user) => (
        <UserCard
          key={user.id}
          name={user.name}
          email={user.email}
          role={user.role}
        />
      ))}
    </div>
  );
}

function App() {
  const users = [
    { id: 1, name: "Alice Johnson", email: "alice@example.com", role: "Admin" },
    { id: 2, name: "Bob Smith", email: "bob@example.com", role: "Developer" },
    { id: 3, name: "Charlie Brown", email: "charlie@example.com", role: "Designer" },
    { id: 4, name: "Diana Prince", email: "diana@example.com", role: "Developer" },
  ];

  return (
    <div className="app">
      <h1>Team Members</h1>
      <UserList users={users} />
    </div>
  );
}

export default App;
```

**Key Points:**
- `UserList` is responsible for mapping the array, while `UserCard` handles rendering a single user.
- The `key` prop is placed on the element returned by `.map()` (the `UserCard`), not on elements inside `UserCard`.
- An empty state is handled for when the user array is empty.
</details>

---

**Exercise 4: Reusable Alert Component**

Create a reusable `Alert` component that accepts `type` (success, warning, error, info), `title`, and `message` props. The component should render with appropriate styling and an optional close button.

<details>
<summary>Solution</summary>

```jsx
function Alert({ type = "info", title, message, onClose }) {
  const icons = {
    success: "✓",
    warning: "⚠",
    error: "✕",
    info: "ℹ",
  };

  return (
    <div className={`alert alert-${type}`}>
      <div className="alert-content">
        <span className="alert-icon">{icons[type]}</span>
        <div>
          {title && <strong className="alert-title">{title}</strong>}
          <p className="alert-message">{message}</p>
        </div>
      </div>
      {onClose && (
        <button className="alert-close" onClick={onClose}>
          &times;
        </button>
      )}
    </div>
  );
}

function App() {
  return (
    <div className="app">
      <h1>Notifications</h1>

      <Alert
        type="success"
        title="Success!"
        message="Your changes have been saved successfully."
        onClose={() => console.log("Closed success alert")}
      />

      <Alert
        type="error"
        title="Error"
        message="Failed to connect to the server. Please try again."
        onClose={() => console.log("Closed error alert")}
      />

      <Alert
        type="warning"
        message="Your session will expire in 5 minutes."
      />

      <Alert
        type="info"
        title="Did you know?"
        message="You can customize your profile settings in the dashboard."
      />
    </div>
  );
}

export default App;
```

**Key Points:**
- The component adapts its appearance based on the `type` prop.
- The close button only renders when an `onClose` callback is provided.
- Default values ensure the component has sensible defaults.
</details>

---

**Exercise 5: Build a Product Listing Page with Reusable Components**

Build a product listing page using multiple reusable components: `ProductCard`, `ProductList`, `CategoryFilter`, and a `PageHeader`. Compose them together in an `App` component.

<details>
<summary>Solution</summary>

```jsx
function PageHeader({ title, subtitle }) {
  return (
    <header className="page-header">
      <h1>{title}</h1>
      {subtitle && <p className="subtitle">{subtitle}</p>}
    </header>
  );
}

function CategoryFilter({ categories, activeCategory, onCategoryChange }) {
  return (
    <div className="category-filter">
      {categories.map((category) => (
        <button
          key={category}
          className={`filter-btn ${activeCategory === category ? "active" : ""}`}
          onClick={() => onCategoryChange(category)}
        >
          {category}
        </button>
      ))}
    </div>
  );
}

function ProductCard({ name, price, category, inStock }) {
  return (
    <div className="product-card">
      <div className="product-image-placeholder">
        {name.charAt(0)}
      </div>
      <div className="product-info">
        <h3 className="product-name">{name}</h3>
        <span className="product-category">{category}</span>
        <p className="product-price">${price.toFixed(2)}</p>
        <span className={`stock-badge ${inStock ? "in-stock" : "out-of-stock"}`}>
          {inStock ? "In Stock" : "Out of Stock"}
        </span>
      </div>
    </div>
  );
}

function ProductList({ products }) {
  if (products.length === 0) {
    return <p className="no-products">No products found in this category.</p>;
  }

  return (
    <div className="product-grid">
      {products.map((product) => (
        <ProductCard
          key={product.id}
          name={product.name}
          price={product.price}
          category={product.category}
          inStock={product.inStock}
        />
      ))}
    </div>
  );
}

function App() {
  const products = [
    { id: 1, name: "Wireless Headphones", price: 59.99, category: "Electronics", inStock: true },
    { id: 2, name: "Running Shoes", price: 89.99, category: "Sports", inStock: true },
    { id: 3, name: "Coffee Maker", price: 34.99, category: "Home", inStock: false },
    { id: 4, name: "Yoga Mat", price: 24.99, category: "Sports", inStock: true },
    { id: 5, name: "Bluetooth Speaker", price: 45.99, category: "Electronics", inStock: true },
    { id: 6, name: "Desk Lamp", price: 29.99, category: "Home", inStock: true },
  ];

  const categories = ["All", "Electronics", "Sports", "Home"];

  return (
    <div className="app">
      <PageHeader
        title="Our Products"
        subtitle="Browse our collection of quality products"
      />

      <CategoryFilter
        categories={categories}
        activeCategory="All"
        onCategoryChange={(category) => console.log("Selected:", category)}
      />

      <ProductList products={products} />
    </div>
  );
}

export default App;
```

**Key Points:**
- Each component has a single, well-defined responsibility.
- `ProductCard` is reused for every product via `.map()` inside `ProductList`.
- `CategoryFilter` communicates the selected category back to the parent through the `onCategoryChange` callback prop.
- The `PageHeader` component demonstrates optional props with conditional rendering.
- Data flows downward from `App` to child components via props.
</details>
