# Week 17: Props & Component Communication

> **Prerequisites:** React basics, JSX syntax, and functional components from Week 16.

---

## Table of Contents

1. [What Are Props?](#1-what-are-props)
2. [Passing Props](#2-passing-props)
3. [Children Props](#3-children-props)
4. [Default Props](#4-default-props)
5. [Prop Types (Brief Intro)](#5-prop-types-brief-intro)
6. [Component Composition](#6-component-composition)
7. [Reusable Component Patterns](#7-reusable-component-patterns)
8. [Mapping Data to Components](#8-mapping-data-to-components)
9. [Summary](#9-summary)

---

## 1. What Are Props?

### Understanding Props

Props (short for "properties") are the mechanism React uses to pass data from one component to another. Specifically, data flows from a **parent** component down to a **child** component.

If you have written JavaScript functions before, you already understand the core idea. A function accepts parameters, and those parameters customize what the function does. Props work the same way for React components.

```javascript
// A regular JavaScript function with parameters
function greetStudent(name, course) {
  return "Hello, " + name + "! Welcome to " + course + ".";
}

greetStudent("Ali", "MERN Stack"); // "Hello, Ali! Welcome to MERN Stack."

// A React component with props -- same concept
function StudentGreeting({ name, course }) {
  return <h1>Hello, {name}! Welcome to {course}.</h1>;
}

<StudentGreeting name="Ali" course="MERN Stack" />
```

**Real-life analogy: Sending a Letter**

Think of props like sending a letter. You (the parent component) write information on a piece of paper, place it inside an envelope, and address it to the recipient (the child component). The recipient opens the envelope, reads the information, and uses it. However, the recipient cannot change what was written on the original letter. They can only read it.

```
  PROPS ARE LIKE SENDING A LETTER
  ================================

  PARENT COMPONENT (Sender)          CHILD COMPONENT (Recipient)
  +-----------------------+          +--------------------------+
  |                       |          |                          |
  |  "I want to send      |   PROPS  |  "I received the data.  |
  |   name='Ali' and      | =======> |   I will use it to      |
  |   age={25} to my      |          |   display information.  |
  |   child component."   |          |   But I CANNOT change   |
  |                       |          |   what was sent to me." |
  +-----------------------+          +--------------------------+
```

### Props Are READ-ONLY

This is a fundamental rule in React: **a component must never modify its own props.** Props flow in one direction only, from parent to child. This is called **one-way data flow** or **unidirectional data flow**.

```
  ONE-WAY DATA FLOW
  ==================

  +----------+     props      +-----------+     props      +-----------+
  |  Parent  | ------------> |   Child   | ------------> | Grandchild|
  |Component |               | Component |               | Component |
  +----------+               +-----------+               +-----------+

      Data flows DOWN only (parent to child).
      A child CANNOT send props back up to its parent.
      A child CANNOT modify the props it receives.
```

Why does React enforce this? Because it makes your application **predictable**. If you know that data only flows in one direction, you always know where a piece of data came from. Debugging becomes straightforward because you can trace any value back to the parent that provided it.

```jsx
function Greeting({ name }) {
  // WRONG -- never do this
  // name = "Something else";  // This violates the read-only rule

  // CORRECT -- just read and use the prop
  return <h1>Hello, {name}!</h1>;
}
```

### Why Props Matter

| Benefit            | Description                                                       |
|--------------------|-------------------------------------------------------------------|
| Reusability        | The same component can display different data based on props      |
| Predictability     | One-way data flow makes it easy to trace where data comes from    |
| Separation         | Parent controls the data, child controls the presentation         |
| Maintainability    | Change data in one place (parent), and the child updates          |

---

## 2. Passing Props

### Basic Syntax

Passing props involves two sides: the **parent** component that sends data, and the **child** component that receives it.

**Parent side:** You add attributes to the child component's JSX tag, just like adding attributes to an HTML element.

**Child side:** The component receives all props as a single object parameter. You can access individual props from that object.

```jsx
// ============ PARENT COMPONENT ============
function App() {
  return (
    <div>
      <StudentCard name="Ali" age={22} />
    </div>
  );
}

// ============ CHILD COMPONENT ============
function StudentCard(props) {
  return (
    <div>
      <h2>{props.name}</h2>
      <p>Age: {props.age}</p>
    </div>
  );
}
```

```
  HOW PROPS GET PASSED
  =====================

  In JSX (Parent):
  <StudentCard name="Ali" age={22} />

  React packages these attributes into a plain object:
  { name: "Ali", age: 22 }

  This object is passed as the first argument to the function:
  function StudentCard(props) {
    // props = { name: "Ali", age: 22 }
    // props.name = "Ali"
    // props.age = 22
  }
```

### Passing Different Data Types

Props can carry any JavaScript value. Strings are the only type that can be passed without curly braces. Everything else must be wrapped in `{}`.

```jsx
function App() {
  return (
    <UserProfile
      name="Sara"                           // String (quotes, no braces needed)
      age={25}                              // Number
      isStudent={true}                      // Boolean
      hobbies={["Reading", "Coding"]}       // Array
      address={{ city: "Karachi", zip: "75100" }}  // Object (double braces!)
    />
  );
}

function UserProfile(props) {
  return (
    <div>
      <h2>{props.name}</h2>
      <p>Age: {props.age}</p>
      <p>Student: {props.isStudent ? "Yes" : "No"}</p>
      <p>Hobbies: {props.hobbies.join(", ")}</p>
      <p>City: {props.address.city}</p>
    </div>
  );
}
```

**Why the double curly braces for objects?**

The outer `{}` is JSX syntax that says "evaluate this JavaScript expression." The inner `{}` is the JavaScript object literal. So `{{ city: "Karachi" }}` means "evaluate this expression: `{ city: "Karachi" }`."

### Props Data Type Reference

| Data Type | Example in JSX                          | Notes                                      |
|-----------|-----------------------------------------|--------------------------------------------|
| String    | `name="Ali"`                            | Can omit curly braces for strings          |
| String    | `name={"Ali"}`                          | Curly braces also work for strings         |
| Number    | `age={25}`                              | Must use curly braces                      |
| Boolean   | `isActive={true}`                       | Must use curly braces                      |
| Boolean   | `isActive`                              | Shorthand for `isActive={true}`            |
| Array     | `items={["a", "b"]}`                    | Must use curly braces                      |
| Object    | `style={{ color: "red" }}`              | Double braces (JSX + object literal)       |
| Function  | `onClick={handleClick}`                 | Pass reference, do not call it             |
| JSX       | `icon={<Icon />}`                       | You can pass JSX elements as props         |

### Props Destructuring

Typing `props.name`, `props.age`, and so on repeatedly is tedious. JavaScript destructuring lets you extract values directly from the props object in the function parameter.

```jsx
// WITHOUT destructuring -- verbose
function StudentCard(props) {
  return (
    <div>
      <h2>{props.name}</h2>
      <p>Age: {props.age}</p>
      <p>Grade: {props.grade}</p>
    </div>
  );
}

// WITH destructuring -- clean and readable
function StudentCard({ name, age, grade }) {
  return (
    <div>
      <h2>{name}</h2>
      <p>Age: {age}</p>
      <p>Grade: {grade}</p>
    </div>
  );
}
```

Both versions produce exactly the same result. Destructuring is preferred in practice because it makes clear at a glance which props the component uses.

```
  DESTRUCTURING COMPARISON
  =========================

  OPTION A: props object             OPTION B: destructuring
  +----------------------------+     +----------------------------+
  | function Card(props) {     |     | function Card({ name,      |
  |   props.name               |     |   age, grade }) {          |
  |   props.age                |     |   name                     |
  |   props.grade              |     |   age                      |
  | }                          |     |   grade                    |
  +----------------------------+     | }                          |
                                     +----------------------------+
  Verbose, but you can see           Clean, and you see all
  the full props object if           expected props at a glance.
  needed for debugging.
```

### Passing Variables and Expressions as Props

Props are not limited to hard-coded values. You can pass variables, function return values, and any JavaScript expression.

```jsx
function App() {
  const studentName = "Ahmed";
  const studentAge = 21;
  const courses = ["React", "Node.js", "MongoDB"];

  return (
    <StudentCard
      name={studentName}
      age={studentAge}
      courses={courses}
      isGraduating={studentAge >= 22}
      displayName={studentName.toUpperCase()}
    />
  );
}

function StudentCard({ name, age, courses, isGraduating, displayName }) {
  return (
    <div>
      <h2>{displayName}</h2>
      <p>Age: {age}</p>
      <p>Courses: {courses.join(", ")}</p>
      <p>{isGraduating ? "Ready to graduate" : "Still studying"}</p>
    </div>
  );
}
```

### Passing Functions as Props

Functions can be passed as props too. This is how child components communicate events back to the parent (you will see this pattern frequently in React).

```jsx
function App() {
  const handleGreet = (name) => {
    alert("Hello, " + name + "!");
  };

  return <GreetButton onGreet={handleGreet} name="Ali" />;
}

function GreetButton({ onGreet, name }) {
  return (
    <button onClick={() => onGreet(name)}>
      Greet {name}
    </button>
  );
}
```

---

## 3. Children Props

### What Is props.children?

When you write HTML, you place content between opening and closing tags: `<div>Content here</div>`. React components work the same way. Anything you place between a component's opening and closing tags becomes available inside that component as `props.children`.

```jsx
// PARENT -- placing content between tags
function App() {
  return (
    <Card>
      <h2>Welcome to React</h2>
      <p>This content is passed as children.</p>
    </Card>
  );
}

// CHILD -- receiving the content via props.children
function Card({ children }) {
  return (
    <div style={{ border: "1px solid #ccc", padding: "16px", borderRadius: "8px" }}>
      {children}
    </div>
  );
}
```

**Real-life analogy: A Picture Frame**

A picture frame (the wrapper component) can hold any picture (the children). The frame provides structure, style, and decoration. The picture inside can be anything -- a landscape, a portrait, an abstract painting. The frame does not care what picture you put in it. It just frames whatever is there.

```
  props.children IS LIKE A PICTURE FRAME
  ========================================

  +====================================+
  ||                                  ||
  ||   +----------------------------+ ||
  ||   |                            | ||
  ||   |   ANY CONTENT GOES HERE    | ||
  ||   |   (this is "children")     | ||
  ||   |                            | ||
  ||   +----------------------------+ ||
  ||                                  ||
  +====================================+
       ^                            ^
       |   This is the "frame"      |
       |   (the wrapper component)  |
```

### Building Wrapper Components

The `children` pattern is ideal for building reusable wrapper or layout components.

```jsx
// A reusable container component
function Section({ title, children }) {
  return (
    <section>
      <h2>{title}</h2>
      <div style={{ padding: "16px" }}>
        {children}
      </div>
    </section>
  );
}

// Using it with different content
function App() {
  return (
    <div>
      <Section title="About Us">
        <p>We are a web development company based in Karachi.</p>
        <p>We specialize in the MERN stack.</p>
      </Section>

      <Section title="Our Services">
        <ul>
          <li>Web Development</li>
          <li>Mobile Apps</li>
          <li>API Development</li>
        </ul>
      </Section>
    </div>
  );
}
```

### Layout Component Example

```jsx
function PageLayout({ children }) {
  return (
    <div>
      <header style={{ background: "#333", color: "#fff", padding: "16px" }}>
        <h1>My MERN App</h1>
      </header>

      <main style={{ padding: "24px", minHeight: "80vh" }}>
        {children}
      </main>

      <footer style={{ background: "#333", color: "#fff", padding: "16px" }}>
        <p>Copyright 2026</p>
      </footer>
    </div>
  );
}

// Every page uses the same layout but with different content
function HomePage() {
  return (
    <PageLayout>
      <h2>Welcome Home</h2>
      <p>This is the home page.</p>
    </PageLayout>
  );
}

function AboutPage() {
  return (
    <PageLayout>
      <h2>About Us</h2>
      <p>Learn more about our company.</p>
    </PageLayout>
  );
}
```

### Children Can Be Anything

`props.children` can be a string, a JSX element, multiple elements, or even nothing at all.

```jsx
// String as children
<Wrapper>Hello World</Wrapper>

// Single element as children
<Wrapper><h1>Title</h1></Wrapper>

// Multiple elements as children
<Wrapper>
  <h1>Title</h1>
  <p>Paragraph</p>
</Wrapper>

// No children (self-closing tag)
<Wrapper />

// Another component as children
<Wrapper>
  <StudentCard name="Ali" age={22} />
</Wrapper>
```

---

## 4. Default Props

### Using Default Parameter Values

Sometimes a prop is optional. If the parent does not provide it, you want the component to use a sensible fallback value. In modern React, you handle this with JavaScript default parameter values.

```jsx
function Greeting({ name = "Guest", greeting = "Hello" }) {
  return <h1>{greeting}, {name}!</h1>;
}

// All props provided
<Greeting name="Ali" greeting="Hi" />
// Renders: Hi, Ali!

// Only name provided -- greeting uses default
<Greeting name="Sara" />
// Renders: Hello, Sara!

// No props provided -- both use defaults
<Greeting />
// Renders: Hello, Guest!
```

**Real-life analogy:** Think of a restaurant order. If a customer does not specify a drink, they get water by default. If they do not mention spice level, the kitchen uses medium. Defaults ensure that the system works even when information is incomplete.

### Default Values for Different Types

```jsx
function ProductCard({
  title = "Untitled Product",
  price = 0,
  inStock = true,
  tags = [],
  image = "/placeholder.png"
}) {
  return (
    <div>
      <img src={image} alt={title} />
      <h3>{title}</h3>
      <p>Price: Rs. {price}</p>
      <p>{inStock ? "In Stock" : "Out of Stock"}</p>
      <p>Tags: {tags.length > 0 ? tags.join(", ") : "None"}</p>
    </div>
  );
}

// Minimal usage -- defaults fill in the gaps
<ProductCard title="Laptop" price={85000} />
// image uses "/placeholder.png"
// inStock defaults to true
// tags defaults to []
```

### When to Use Default Props

| Scenario                              | Example Default Value                 |
|---------------------------------------|---------------------------------------|
| Optional display text                 | `title = "Untitled"`                  |
| Optional styling variant              | `variant = "primary"`                 |
| Optional numeric value                | `count = 0`                           |
| Optional array for lists              | `items = []`                          |
| Optional boolean flag                 | `isVisible = true`                    |
| Optional callback function            | `onClick = () => {}`                  |

---

## 5. Prop Types (Brief Intro)

### Why Type Checking Matters

As your application grows, you will have dozens or even hundreds of components, each expecting specific props. Without type checking, bugs creep in silently. You might pass a string where a number is expected, forget a required prop, or misspell a prop name. The component will not crash immediately -- it will just behave incorrectly, and tracking down the issue wastes time.

```jsx
// Imagine this component expects a number for "price"
function ProductCard({ title, price }) {
  return <p>{title}: Rs. {price.toFixed(2)}</p>;
}

// But someone accidentally passes a string
<ProductCard title="Laptop" price="85000" />
// This might work (toFixed exists on strings? No, it does not.)
// Result: Runtime error -- price.toFixed is not a function
```

### The PropTypes Library

React provides an optional library called `prop-types` that lets you declare what types each prop should be. If a wrong type is passed, you see a warning in the browser console during development.

```bash
npm install prop-types
```

```jsx
import PropTypes from 'prop-types';

function StudentCard({ name, age, isActive }) {
  return (
    <div>
      <h2>{name}</h2>
      <p>Age: {age}</p>
      <p>Status: {isActive ? "Active" : "Inactive"}</p>
    </div>
  );
}

StudentCard.propTypes = {
  name: PropTypes.string.isRequired,  // Must be a string, required
  age: PropTypes.number.isRequired,   // Must be a number, required
  isActive: PropTypes.bool            // Must be a boolean, optional
};
```

### Common PropTypes

| PropType                    | Validates                                  |
|-----------------------------|--------------------------------------------|
| `PropTypes.string`          | A string value                             |
| `PropTypes.number`          | A number value                             |
| `PropTypes.bool`            | A boolean value                            |
| `PropTypes.array`           | An array                                   |
| `PropTypes.object`          | An object                                  |
| `PropTypes.func`            | A function                                 |
| `PropTypes.node`            | Anything renderable (string, number, JSX)  |
| `PropTypes.element`         | A React element                            |
| `PropTypes.oneOf(["a","b"])`| One of the specified values                |
| `.isRequired`               | Add to any type to make it required        |

### Why TypeScript Is Better (Mention Only)

PropTypes only catch errors at **runtime** (while the app is running in the browser) and only in **development** mode. TypeScript catches type errors at **compile time** (before the code even runs), directly in your code editor. This is faster, more reliable, and covers more cases. Most professional React projects use TypeScript instead of PropTypes today.

We will not cover TypeScript in detail in this course, but know that it is the industry standard for type safety in React applications.

---

## 6. Component Composition

### What Is Component Composition?

Component composition is the practice of building complex user interfaces by combining small, focused components together. Instead of creating one massive component that does everything, you break the UI into small pieces and assemble them.

**Real-life analogy:** Think of building with LEGO bricks. Each brick is small and simple on its own, but by snapping them together, you can build houses, cars, and spaceships. You do not create a single giant custom piece for the entire house. You compose it from smaller standard pieces.

### Building a Complex UI from Simple Components

```jsx
// Small, focused components -- each does ONE thing

function Avatar({ src, alt }) {
  return <img src={src} alt={alt} style={{ borderRadius: "50%", width: "60px" }} />;
}

function UserName({ name }) {
  return <h3>{name}</h3>;
}

function UserBio({ bio }) {
  return <p style={{ color: "#666" }}>{bio}</p>;
}

// Composed together into a larger component
function UserProfile({ user }) {
  return (
    <div style={{ border: "1px solid #ddd", padding: "16px", borderRadius: "8px" }}>
      <Avatar src={user.avatar} alt={user.name} />
      <UserName name={user.name} />
      <UserBio bio={user.bio} />
    </div>
  );
}

// Used in the App
function App() {
  const user = {
    name: "Ali Khan",
    avatar: "/images/ali.jpg",
    bio: "Full-stack developer specializing in MERN."
  };

  return <UserProfile user={user} />;
}
```

### Component Tree and Data Flow

Every React application forms a tree of components. Data flows from the root (top) down through the tree via props.

```
  COMPONENT TREE -- DATA FLOWS DOWNWARD
  =======================================

                      +-------+
                      |  App  |  (Root component -- owns the data)
                      +---+---+
                          |
           +--------------+--------------+
           |                             |
      +----+-----+               +------+------+
      |  Header  |               |   Main      |
      +----+-----+               +------+------+
           |                            |
     +-----+-----+          +----------+----------+
     |           |           |                     |
  +--+--+   +---+---+   +---+-------+     +-------+---+
  | Logo|   |  Nav  |   | UserList  |     | Sidebar   |
  +-----+   +---+---+   +---+-------+     +-----------+
                 |           |
            +----+----+  +---+-------+
            |NavItem  |  | UserCard  |
            |NavItem  |  | UserCard  |
            |NavItem  |  | UserCard  |
            +---------+  +-----------+

  RULES:
  - Data flows DOWN (parent to child) via props.
  - Each component only knows about its own props.
  - A child does NOT know about its siblings.
```

### Composition vs Inheritance

In many object-oriented languages, you use **inheritance** to share behavior between classes (a `Dog` class inherits from an `Animal` class). React takes a different approach. React strongly recommends **composition** over inheritance.

With composition, you combine components together rather than extending them.

```jsx
// COMPOSITION (React way) -- components wrap or include other components

function Dialog({ title, children }) {
  return (
    <div style={{ border: "2px solid #333", padding: "20px", borderRadius: "8px" }}>
      <h2>{title}</h2>
      <div>{children}</div>
    </div>
  );
}

function WelcomeDialog() {
  return (
    <Dialog title="Welcome!">
      <p>Thank you for joining our MERN stack course.</p>
      <p>Let us get started with React props.</p>
    </Dialog>
  );
}

function WarningDialog() {
  return (
    <Dialog title="Warning">
      <p>Are you sure you want to delete this item?</p>
      <button>Confirm</button>
      <button>Cancel</button>
    </Dialog>
  );
}
```

```
  COMPOSITION vs INHERITANCE
  ===========================

  INHERITANCE (NOT recommended in React):

      BaseComponent
           |
      SpecialComponent extends BaseComponent
           |
      VerySpecialComponent extends SpecialComponent

      Problem: Deep hierarchy, tightly coupled, hard to change.

  COMPOSITION (React way):

      +----------+
      | Wrapper  |  <-- provides structure/style
      |  +----+  |
      |  |Child|  |  <-- provides content
      |  +----+  |
      +----------+

      Flexible: any child can go inside any wrapper.
      No hierarchy to manage.
```

| Approach     | How It Works                                      | React Recommendation |
|--------------|---------------------------------------------------|----------------------|
| Inheritance  | Child class extends parent class                  | Not recommended      |
| Composition  | Components contain other components via props     | Strongly recommended |

---

## 7. Reusable Component Patterns

### Pattern 1: Button Component with Variants

A button is one of the most reused UI elements. Instead of creating separate components for each button style, create one component that accepts a `variant` prop.

```jsx
function Button({ variant = "primary", children, onClick }) {
  const styles = {
    primary: {
      backgroundColor: "#3B82F6",
      color: "#fff",
      border: "none",
      padding: "10px 20px",
      borderRadius: "6px",
      cursor: "pointer"
    },
    secondary: {
      backgroundColor: "#fff",
      color: "#3B82F6",
      border: "2px solid #3B82F6",
      padding: "10px 20px",
      borderRadius: "6px",
      cursor: "pointer"
    },
    danger: {
      backgroundColor: "#EF4444",
      color: "#fff",
      border: "none",
      padding: "10px 20px",
      borderRadius: "6px",
      cursor: "pointer"
    }
  };

  return (
    <button style={styles[variant]} onClick={onClick}>
      {children}
    </button>
  );
}

// Usage
function App() {
  return (
    <div>
      <Button variant="primary" onClick={() => alert("Saved!")}>
        Save
      </Button>

      <Button variant="secondary" onClick={() => alert("Cancelled")}>
        Cancel
      </Button>

      <Button variant="danger" onClick={() => alert("Deleted!")}>
        Delete
      </Button>

      {/* Uses default variant ("primary") */}
      <Button onClick={() => alert("Clicked!")}>
        Default Button
      </Button>
    </div>
  );
}
```

```
  BUTTON VARIANTS
  ================

  Same component, different appearance based on the "variant" prop:

  +-------------------+   +-------------------+   +-------------------+
  | [####  Save ####] |   | [   Cancel      ] |   | [#### Delete ###] |
  | variant="primary" |   | variant="secondary"|   | variant="danger"  |
  | Blue background   |   | White background  |   | Red background    |
  | White text        |   | Blue border/text  |   | White text        |
  +-------------------+   +-------------------+   +-------------------+
```

### Pattern 2: Card Component That Accepts Different Content

```jsx
function Card({ title, subtitle, children, footer }) {
  return (
    <div style={{
      border: "1px solid #e5e7eb",
      borderRadius: "8px",
      overflow: "hidden",
      boxShadow: "0 1px 3px rgba(0,0,0,0.1)"
    }}>
      {/* Card Header */}
      <div style={{ padding: "16px", borderBottom: "1px solid #e5e7eb" }}>
        <h3 style={{ margin: 0 }}>{title}</h3>
        {subtitle && <p style={{ margin: "4px 0 0", color: "#6b7280" }}>{subtitle}</p>}
      </div>

      {/* Card Body */}
      <div style={{ padding: "16px" }}>
        {children}
      </div>

      {/* Card Footer (optional) */}
      {footer && (
        <div style={{ padding: "16px", borderTop: "1px solid #e5e7eb", background: "#f9fafb" }}>
          {footer}
        </div>
      )}
    </div>
  );
}

// Usage with different content
function App() {
  return (
    <div>
      {/* User Profile Card */}
      <Card
        title="Ali Khan"
        subtitle="Full-Stack Developer"
        footer={<Button variant="primary">View Profile</Button>}
      >
        <p>Experienced MERN stack developer based in Karachi.</p>
        <p>Skills: React, Node.js, MongoDB, Express</p>
      </Card>

      {/* Course Card */}
      <Card title="MERN Stack Course" subtitle="Week 17">
        <p>Learning about Props and Component Communication.</p>
        <p>Duration: 2 hours</p>
      </Card>

      {/* Simple Notification Card */}
      <Card title="Notification">
        <p>Your assignment has been submitted successfully.</p>
      </Card>
    </div>
  );
}
```

### Pattern 3: List Component That Renders Any Array

```jsx
function List({ items, renderItem, emptyMessage = "No items to display." }) {
  if (items.length === 0) {
    return <p style={{ color: "#999" }}>{emptyMessage}</p>;
  }

  return (
    <ul style={{ listStyle: "none", padding: 0 }}>
      {items.map((item, index) => (
        <li key={index} style={{ padding: "8px 0", borderBottom: "1px solid #eee" }}>
          {renderItem(item)}
        </li>
      ))}
    </ul>
  );
}

// Usage -- the same List component renders completely different content

function App() {
  const students = ["Ali", "Sara", "Ahmed", "Fatima"];
  const products = [
    { name: "Laptop", price: 85000 },
    { name: "Mouse", price: 1500 },
    { name: "Keyboard", price: 3000 }
  ];

  return (
    <div>
      {/* List of student names */}
      <h2>Students</h2>
      <List
        items={students}
        renderItem={(student) => <span>{student}</span>}
      />

      {/* List of products with prices */}
      <h2>Products</h2>
      <List
        items={products}
        renderItem={(product) => (
          <span>{product.name} -- Rs. {product.price}</span>
        )}
      />

      {/* Empty list */}
      <h2>Notifications</h2>
      <List
        items={[]}
        renderItem={(item) => <span>{item}</span>}
        emptyMessage="You have no new notifications."
      />
    </div>
  );
}
```

---

## 8. Mapping Data to Components

### Rendering Arrays of Components

In real applications, you rarely hard-code each component. Instead, you have an array of data (from an API, a database, or a local file), and you use JavaScript's `map()` method to transform each item into a component.

```jsx
function App() {
  const students = [
    { name: "Ali", grade: "A" },
    { name: "Sara", grade: "B+" },
    { name: "Ahmed", grade: "A-" },
    { name: "Fatima", grade: "A+" }
  ];

  return (
    <div>
      <h1>Class Roster</h1>
      {students.map((student, index) => (
        <div key={index}>
          <h3>{student.name}</h3>
          <p>Grade: {student.grade}</p>
        </div>
      ))}
    </div>
  );
}
```

```
  HOW map() RENDERS COMPONENTS
  ==============================

  Data Array:
  [
    { name: "Ali",    grade: "A"  },
    { name: "Sara",   grade: "B+" },
    { name: "Ahmed",  grade: "A-" },
    { name: "Fatima", grade: "A+" }
  ]

       |  .map()  transforms each item into JSX
       v

  Rendered Output:
  +--------------------+
  | Ali      Grade: A  |
  +--------------------+
  | Sara     Grade: B+ |
  +--------------------+
  | Ahmed    Grade: A- |
  +--------------------+
  | Fatima   Grade: A+ |
  +--------------------+
```

### Mapping into Separate Components

For better organization, map each item into its own dedicated component.

```jsx
function StudentCard({ name, grade, enrollmentDate }) {
  return (
    <div style={{ border: "1px solid #ddd", padding: "12px", margin: "8px 0", borderRadius: "6px" }}>
      <h3>{name}</h3>
      <p>Grade: {grade}</p>
      <p>Enrolled: {enrollmentDate}</p>
    </div>
  );
}

function StudentList() {
  const students = [
    { id: 1, name: "Ali Khan", grade: "A", enrollmentDate: "2025-01-15" },
    { id: 2, name: "Sara Ahmed", grade: "B+", enrollmentDate: "2025-01-20" },
    { id: 3, name: "Usman Malik", grade: "A-", enrollmentDate: "2025-02-01" },
    { id: 4, name: "Fatima Noor", grade: "A+", enrollmentDate: "2025-01-10" }
  ];

  return (
    <div>
      <h1>Students</h1>
      {students.map((student) => (
        <StudentCard
          key={student.id}
          name={student.name}
          grade={student.grade}
          enrollmentDate={student.enrollmentDate}
        />
      ))}
    </div>
  );
}
```

### The Key Prop: Why It Matters

When you render a list of components, React needs a way to identify each item uniquely. This is what the `key` prop is for. Without keys, React cannot efficiently update the list when items are added, removed, or reordered.

**Real-life analogy: Student ID Numbers**

Imagine a university with 500 students named on a roster. If two students are both named "Ahmed Ali," how does the registrar know which one got an A and which one got a B? They use student ID numbers. Each student has a unique ID that distinguishes them from everyone else, regardless of whether names overlap.

The `key` prop works the same way. It gives React a stable, unique identifier for each item in a list.

```
  WHY KEYS MATTER
  =================

  WITHOUT keys -- React does not know which item changed:

  Before:                      After (Ahmed removed):
  +--------+                   +--------+
  | Ali    |                   | Ali    |  <-- Is this the same "Ali"?
  | Ahmed  |                   | Sara   |  <-- Is this the old "Sara" or "Ahmed" renamed?
  | Sara   |                   +--------+
  +--------+
  React has to guess. It might re-render everything.

  WITH keys -- React knows exactly what changed:

  Before:                      After (key=2 removed):
  +------------+               +------------+
  | key=1: Ali |               | key=1: Ali |  <-- Same, skip
  | key=2: Ahmed|              | key=3: Sara|  <-- Same, skip
  | key=3: Sara|               +------------+
  +------------+
  React removes only key=2. Efficient!
```

### Key Prop Rules

```jsx
// GOOD -- using a unique ID from the data
{students.map((student) => (
  <StudentCard key={student.id} name={student.name} />
))}

// ACCEPTABLE -- using index when the list is static and never reorders
{colors.map((color, index) => (
  <ColorSwatch key={index} color={color} />
))}

// BAD -- using index when items can be added, removed, or reordered
// This causes bugs because the index changes when the list changes
{todoItems.map((item, index) => (
  <TodoItem key={index} text={item.text} />  // Do NOT do this for dynamic lists
))}

// BAD -- using random values (new key every render = full re-render every time)
{students.map((student) => (
  <StudentCard key={Math.random()} name={student.name} />  // NEVER do this
))}
```

| Key Strategy              | When to Use                          | When to Avoid                        |
|---------------------------|--------------------------------------|--------------------------------------|
| Unique ID from data       | Always the best choice               | Never avoid this                     |
| Array index               | Static lists that never change order | Dynamic lists, sortable lists        |
| Random values             | Never                                | Always avoid                         |

### Complete Example: Mapping Data to a Reusable Component

```jsx
function CourseCard({ title, instructor, duration, level }) {
  const levelColors = {
    beginner: "#22C55E",
    intermediate: "#F59E0B",
    advanced: "#EF4444"
  };

  return (
    <div style={{
      border: "1px solid #e5e7eb",
      borderRadius: "8px",
      padding: "16px",
      margin: "8px 0",
      borderLeft: `4px solid ${levelColors[level] || "#999"}`
    }}>
      <h3>{title}</h3>
      <p>Instructor: {instructor}</p>
      <p>Duration: {duration}</p>
      <span style={{
        background: levelColors[level],
        color: "#fff",
        padding: "2px 8px",
        borderRadius: "4px",
        fontSize: "12px"
      }}>
        {level.toUpperCase()}
      </span>
    </div>
  );
}

function CourseCatalog() {
  const courses = [
    { id: "c1", title: "HTML & CSS Fundamentals", instructor: "Ali", duration: "4 weeks", level: "beginner" },
    { id: "c2", title: "JavaScript Deep Dive", instructor: "Sara", duration: "6 weeks", level: "intermediate" },
    { id: "c3", title: "React & Redux", instructor: "Ahmed", duration: "8 weeks", level: "advanced" },
    { id: "c4", title: "Node.js & Express", instructor: "Fatima", duration: "6 weeks", level: "intermediate" },
    { id: "c5", title: "MongoDB Mastery", instructor: "Usman", duration: "5 weeks", level: "intermediate" }
  ];

  return (
    <div>
      <h1>Course Catalog</h1>
      <p>Showing {courses.length} courses</p>
      {courses.map((course) => (
        <CourseCard
          key={course.id}
          title={course.title}
          instructor={course.instructor}
          duration={course.duration}
          level={course.level}
        />
      ))}
    </div>
  );
}
```

---

## 9. Summary

### Key Concepts at a Glance

| Concept                 | What It Means                                                           |
|-------------------------|-------------------------------------------------------------------------|
| Props                   | Data passed from parent to child component                              |
| One-way data flow       | Data flows downward only (parent to child), never upward                |
| Read-only               | A component must never modify its own props                             |
| Destructuring           | `({ name, age })` extracts props directly in the function parameter     |
| props.children          | Content placed between a component's opening and closing tags           |
| Default props           | Fallback values when a prop is not provided                             |
| PropTypes               | Runtime type checking library for props (development only)              |
| Component composition   | Building complex UIs by combining small, focused components             |
| Composition > Inheritance| React prefers combining components over extending them                 |
| key prop                | Unique identifier for each item in a rendered list                      |
| map() for rendering     | Transform an array of data into an array of components                  |

### Props Flow Cheat Sheet

```
  COMPLETE PROPS FLOW
  =====================

  1. PARENT defines data and passes it as attributes:

     <Child name="Ali" age={22} />

  2. REACT packages attributes into a props object:

     { name: "Ali", age: 22 }

  3. CHILD receives the object and reads from it:

     function Child({ name, age }) {
       return <p>{name} is {age} years old.</p>;
     }

  4. CHILD renders using the prop values:

     "Ali is 22 years old."
```

### Component Patterns Cheat Sheet

| Pattern                  | Use Case                                          | Example                      |
|--------------------------|---------------------------------------------------|------------------------------|
| Variant prop             | Same component, different visual styles           | Button with primary/danger   |
| Children prop            | Wrapper components that accept any content         | Card, Dialog, Layout         |
| Render prop (renderItem) | Components that render custom content per item    | List, Table, Dropdown        |
| Default props            | Optional props with sensible fallback values      | Greeting with default name   |
| Mapping arrays           | Rendering dynamic lists from data                 | Student list, product grid   |

### Common Mistakes to Avoid

| Mistake                                    | Why It Is Wrong                                           | Correct Approach                             |
|--------------------------------------------|-----------------------------------------------------------|----------------------------------------------|
| Modifying props inside a child             | Props are read-only; violates React's rules               | Use state (Week 18) to manage mutable data   |
| Forgetting the `key` prop in lists         | React cannot track list items efficiently                 | Always provide a unique `key` from the data  |
| Using array index as key for dynamic lists | Index shifts when items are added/removed, causing bugs   | Use a stable unique ID from the data         |
| Using `Math.random()` as key              | New key every render forces full re-mount of every item   | Use a stable unique ID from the data         |
| Passing too many props to one component    | Makes the component hard to use and maintain              | Break into smaller composed components       |
| Not destructuring props                    | `props.x` repeated everywhere is verbose and hard to read | Destructure in the parameter: `({ x, y })`  |

---

> **Next Week (Week 18):** State Management -- where you will learn how components manage their own internal data using `useState`, handle user interactions, and build truly dynamic, interactive applications.
