# Week 12: Objects, DOM & Events - Practice Questions

**Total Questions: 53**

| Section | Topic | Questions |
|---------|-------|-----------|
| A | Multiple Choice Questions | 15 |
| B | Short Answer Questions | 8 |
| C | What Is the Output? | 10 |
| D | Coding Exercises | 10 |
| E | JavaScript Weeks 9-12 Comprehensive Review | 10 |

---

## Section A: Multiple Choice Questions (15)

**Q1.** Which of the following is a valid way to create an object in JavaScript?

- A) `let obj = object()`
- B) `let obj = {}`
- C) `let obj = new Array()`
- D) `let obj = create Object()`

<details>
<summary>Answer</summary>

**B) `let obj = {}`**

Objects in JavaScript can be created using object literal notation `{}`, the `new Object()` constructor, or `Object.create()`. The curly brace literal is the most common and recommended approach.
</details>

---

**Q2.** What is the output of the following code?

```js
const car = { brand: "Toyota", year: 2023 };
console.log(car["brand"]);
```

- A) `undefined`
- B) `brand`
- C) `Toyota`
- D) `Error`

<details>
<summary>Answer</summary>

**C) `Toyota`**

Bracket notation `car["brand"]` accesses the property `brand` on the object, which holds the value `"Toyota"`. Bracket notation is equivalent to dot notation (`car.brand`) but allows dynamic keys and keys with special characters.
</details>

---

**Q3.** When should you use bracket notation instead of dot notation to access an object property?

- A) When the property name is a number or contains spaces
- B) When the object is nested
- C) When the property value is a string
- D) When the object has more than 5 properties

<details>
<summary>Answer</summary>

**A) When the property name is a number or contains spaces**

Bracket notation is required when a property name contains spaces, special characters, starts with a number, or when the property name is stored in a variable. Dot notation only works with valid JavaScript identifiers.
</details>

---

**Q4.** What does the `this` keyword refer to inside a method of an object?

- A) The global window object
- B) The function itself
- C) The object that owns the method
- D) The parent object in the prototype chain

<details>
<summary>Answer</summary>

**C) The object that owns the method**

When a function is called as a method of an object (e.g., `obj.method()`), `this` refers to the object that the method belongs to. This allows the method to access and modify other properties on the same object.
</details>

---

**Q5.** What does `JSON.stringify()` do?

- A) Parses a JSON string into a JavaScript object
- B) Converts a JavaScript object into a JSON-formatted string
- C) Validates whether a string is valid JSON
- D) Creates a deep copy of an object

<details>
<summary>Answer</summary>

**B) Converts a JavaScript object into a JSON-formatted string**

`JSON.stringify()` takes a JavaScript value (typically an object or array) and converts it into a JSON string. This is commonly used when sending data to a server or storing data in localStorage.
</details>

---

**Q6.** What does `JSON.parse()` return?

- A) A JSON-formatted string
- B) A JavaScript object or value
- C) A boolean indicating valid JSON
- D) An array of key-value pairs

<details>
<summary>Answer</summary>

**B) A JavaScript object or value**

`JSON.parse()` takes a valid JSON string and converts it back into a JavaScript object, array, or primitive value. It is the reverse operation of `JSON.stringify()`.
</details>

---

**Q7.** Which method selects an element by its `id` attribute?

- A) `document.querySelector()`
- B) `document.getElementsByClassName()`
- C) `document.getElementById()`
- D) `document.getElementByTag()`

<details>
<summary>Answer</summary>

**C) `document.getElementById()`**

`document.getElementById("myId")` selects and returns the single element that has the specified `id` attribute. Since IDs must be unique in a document, this method always returns one element or `null`.
</details>

---

**Q8.** What is the difference between `textContent` and `innerHTML`?

- A) There is no difference
- B) `textContent` sets only plain text; `innerHTML` can set HTML markup
- C) `innerHTML` is faster than `textContent`
- D) `textContent` only works on `<p>` elements

<details>
<summary>Answer</summary>

**B) `textContent` sets only plain text; `innerHTML` can set HTML markup**

`textContent` treats everything as plain text and does not parse HTML tags. `innerHTML` parses and renders any HTML tags in the string. Using `textContent` is safer against XSS attacks when displaying user input.
</details>

---

**Q9.** Which `classList` method adds a class only if it is not already present, and removes it if it is?

- A) `classList.add()`
- B) `classList.remove()`
- C) `classList.toggle()`
- D) `classList.replace()`

<details>
<summary>Answer</summary>

**C) `classList.toggle()`**

`classList.toggle("className")` checks whether the specified class exists on the element. If it does, it removes it; if it does not, it adds it. This is commonly used for toggling UI states like showing/hiding menus or switching themes.
</details>

---

**Q10.** What does `document.createElement("div")` do?

- A) Selects the first `<div>` in the document
- B) Creates a new `<div>` element in memory (not yet in the DOM)
- C) Deletes all `<div>` elements from the page
- D) Creates a `<div>` and automatically appends it to the body

<details>
<summary>Answer</summary>

**B) Creates a new `<div>` element in memory (not yet in the DOM)**

`document.createElement()` creates a new HTML element in memory. It does not appear on the page until you explicitly append it to the DOM using methods like `appendChild()` or `append()`.
</details>

---

**Q11.** Which method is used to attach an event handler to an element?

- A) `element.onEvent()`
- B) `element.addEventListener()`
- C) `element.attachEvent()`
- D) `element.bindEvent()`

<details>
<summary>Answer</summary>

**B) `element.addEventListener()`**

`addEventListener("event", callback)` is the modern and preferred way to attach event handlers. Unlike inline event handlers or `onclick` properties, it allows multiple handlers for the same event and provides more control over event propagation.
</details>

---

**Q12.** What does `event.preventDefault()` do?

- A) Stops event bubbling
- B) Removes the event listener
- C) Prevents the browser's default action for that event
- D) Prevents other event listeners from being called

<details>
<summary>Answer</summary>

**C) Prevents the browser's default action for that event**

`event.preventDefault()` stops the browser from performing its default behavior. For example, it prevents a form from submitting and refreshing the page, or prevents a link from navigating to its `href`. It does not stop event propagation.
</details>

---

**Q13.** What is event bubbling?

- A) Events are handled only on the target element
- B) Events propagate from the target element up through its ancestors to the document
- C) Events propagate from the document down to the target element
- D) Events are triggered multiple times on the same element

<details>
<summary>Answer</summary>

**B) Events propagate from the target element up through its ancestors to the document**

In event bubbling, when an event occurs on an element, it first runs the handler on that element, then on its parent, then on its grandparent, and so on up through the DOM tree. This is the default propagation behavior in JavaScript.
</details>

---

**Q14.** What is event delegation?

- A) Assigning a separate event listener to every child element
- B) Attaching a single event listener to a parent element to handle events on its children
- C) Preventing events from reaching child elements
- D) Delegating events to the browser's default handler

<details>
<summary>Answer</summary>

**B) Attaching a single event listener to a parent element to handle events on its children**

Event delegation takes advantage of event bubbling by placing a single event listener on a parent element. When an event occurs on a child, it bubbles up to the parent where the listener can check `event.target` to determine which child was clicked. This is efficient for dynamic lists and reduces memory usage.
</details>

---

**Q15.** What does `Object.keys(obj)` return?

- A) An array of the object's values
- B) An array of the object's key-value pairs
- C) An array of the object's property names (keys)
- D) The number of properties in the object

<details>
<summary>Answer</summary>

**C) An array of the object's property names (keys)**

`Object.keys(obj)` returns an array containing all the enumerable property names of the object. Similarly, `Object.values(obj)` returns an array of the values, and `Object.entries(obj)` returns an array of `[key, value]` pairs.
</details>

---

## Section B: Short Answer Questions (8)

**Q1.** What is the DOM?

<details>
<summary>Answer</summary>

The DOM (Document Object Model) is a programming interface provided by the browser that represents the HTML document as a tree of objects. Each HTML element becomes a node in this tree. JavaScript uses the DOM to access, modify, add, or delete HTML elements and their content dynamically. When you write `document.getElementById("title")`, you are interacting with the DOM, not the HTML file directly. The DOM is what makes web pages interactive.
</details>

---

**Q2.** What is the difference between `textContent` and `innerHTML`?

<details>
<summary>Answer</summary>

`textContent` returns or sets the plain text content of an element, ignoring any HTML tags. If you assign a string with HTML tags to `textContent`, the tags are displayed as literal text, not rendered.

`innerHTML` returns or sets the HTML content of an element, including any HTML tags. If you assign a string with HTML tags to `innerHTML`, the browser parses and renders those tags.

**Example:**
```js
element.textContent = "<b>Hello</b>"; // Displays: <b>Hello</b> (as text)
element.innerHTML = "<b>Hello</b>";   // Displays: Hello (bold)
```

`textContent` is safer to use with user-generated content because it does not execute or render HTML, which prevents Cross-Site Scripting (XSS) attacks.
</details>

---

**Q3.** What is event bubbling? Provide an example.

<details>
<summary>Answer</summary>

Event bubbling is the process where an event triggered on a child element propagates upward through its parent elements all the way to the document root. Each ancestor element's event handler for that event type gets a chance to respond.

**Example:**
```html
<div id="parent">
  <button id="child">Click Me</button>
</div>
```
```js
document.getElementById("parent").addEventListener("click", () => {
  console.log("Parent clicked");
});

document.getElementById("child").addEventListener("click", () => {
  console.log("Child clicked");
});
```

When the button is clicked, the console will log:
1. `"Child clicked"` (the target element first)
2. `"Parent clicked"` (then bubbles up to the parent)

You can stop bubbling by calling `event.stopPropagation()` inside a handler.
</details>

---

**Q4.** What is event delegation and why should you use it?

<details>
<summary>Answer</summary>

Event delegation is a pattern where you attach a single event listener to a parent element instead of adding individual listeners to each child element. It works because of event bubbling; when a child element is clicked, the event bubbles up to the parent where the listener can inspect `event.target` to determine which child triggered the event.

**Why use it:**
- **Performance:** One listener on a parent is more efficient than dozens of listeners on individual children, especially for large lists.
- **Dynamic elements:** Elements added to the DOM after the page loads automatically work with the parent's listener without needing to attach new listeners.
- **Cleaner code:** Reduces the amount of setup code needed for repetitive elements.

**Example:**
```js
document.getElementById("todo-list").addEventListener("click", (event) => {
  if (event.target.tagName === "LI") {
    event.target.classList.toggle("completed");
  }
});
```
</details>

---

**Q5.** What is the difference between `getElementById` and `querySelector`?

<details>
<summary>Answer</summary>

`getElementById("myId")` selects a single element by its `id` attribute. It only accepts an ID name (without the `#` symbol) and returns one element or `null`.

`querySelector(".myClass")` selects the first element that matches any valid CSS selector. It can select by ID (`"#myId"`), class (`".myClass"`), tag (`"div"`), attribute (`"[type='text']"`), or complex selectors (`"div.container > p:first-child"`).

**Key differences:**
| Feature | `getElementById` | `querySelector` |
|---|---|---|
| Selector type | ID only | Any CSS selector |
| Returns | Single element | First matching element |
| Syntax | No `#` prefix | Uses CSS syntax with `#` |
| Speed | Slightly faster | Slightly slower |
| Flexibility | Limited | Very flexible |

In modern development, `querySelector` and `querySelectorAll` are preferred for their flexibility, while `getElementById` remains useful for its simplicity and performance when selecting by ID.
</details>

---

**Q6.** What does `event.preventDefault()` do? Give two practical examples.

<details>
<summary>Answer</summary>

`event.preventDefault()` stops the browser from executing the default action associated with an event. It does not stop the event from propagating (bubbling) to other elements.

**Example 1 -- Preventing form submission:**
```js
document.getElementById("myForm").addEventListener("submit", (event) => {
  event.preventDefault(); // Stops the page from refreshing
  // Perform custom validation or send data via fetch()
  console.log("Form submitted via JavaScript");
});
```
Without `preventDefault()`, submitting a form causes the browser to refresh the page.

**Example 2 -- Preventing a link from navigating:**
```js
document.getElementById("myLink").addEventListener("click", (event) => {
  event.preventDefault(); // Stops navigation to the href
  console.log("Link click handled by JavaScript");
});
```
Without `preventDefault()`, clicking an anchor tag navigates the browser to the URL specified in `href`.
</details>

---

**Q7.** What is JSON and why is it important in web development?

<details>
<summary>Answer</summary>

JSON (JavaScript Object Notation) is a lightweight, text-based data format used to store and exchange data. It looks very similar to JavaScript object syntax but is a language-independent format supported by virtually every programming language.

**Why it is important:**
- **API communication:** JSON is the standard format for sending and receiving data between a client (browser) and a server via APIs (e.g., REST APIs, Fetch API).
- **localStorage:** Browsers can only store strings in localStorage. JSON allows you to convert objects to strings (`JSON.stringify()`) for storage and back to objects (`JSON.parse()`) for use.
- **Configuration files:** Many tools and frameworks (e.g., `package.json` in Node.js) use JSON for configuration.
- **Readability:** JSON is human-readable and easy to debug compared to formats like XML.

**Example:**
```js
const user = { name: "Ali", age: 25, city: "Karachi" };
const jsonString = JSON.stringify(user); // '{"name":"Ali","age":25,"city":"Karachi"}'
const parsed = JSON.parse(jsonString);   // Back to a JavaScript object
```
</details>

---

**Q8.** What are `classList.add()`, `classList.remove()`, `classList.toggle()`, and `classList.contains()`? When would you use each?

<details>
<summary>Answer</summary>

These are methods on an element's `classList` property that allow you to manipulate CSS classes without directly editing the `className` string.

- **`classList.add("className")`** -- Adds one or more classes to the element. If the class already exists, it does nothing (no duplicates).
  - *Use case:* Highlighting a selected item, showing an element by adding a `visible` class.

- **`classList.remove("className")`** -- Removes one or more classes from the element. If the class does not exist, it does nothing (no error).
  - *Use case:* Removing an `active` class from a navigation link, hiding an error message.

- **`classList.toggle("className")`** -- Adds the class if it is absent; removes it if it is present.
  - *Use case:* Toggling a dark mode theme, showing/hiding a dropdown menu.

- **`classList.contains("className")`** -- Returns `true` if the element has the specified class, `false` otherwise.
  - *Use case:* Checking if an item is already marked as complete before performing an action.

**Example:**
```js
const box = document.getElementById("box");
box.classList.add("highlight");          // Adds 'highlight'
box.classList.remove("highlight");       // Removes 'highlight'
box.classList.toggle("highlight");       // Adds it back
console.log(box.classList.contains("highlight")); // true
```
</details>

---

## Section C: What Is the Output? (10)

**Q1.** What is the output?

```js
const person = { name: "Sara", age: 28 };
console.log(person.name);
console.log(person["age"]);
```

<details>
<summary>Answer</summary>

```
Sara
28
```

**Explanation:** `person.name` uses dot notation to access the `name` property. `person["age"]` uses bracket notation to access the `age` property. Both approaches return the corresponding values.
</details>

---

**Q2.** What is the output?

```js
const user = { name: "Ahmed", city: "Lahore" };
const json = JSON.stringify(user);
console.log(json);
console.log(typeof json);
```

<details>
<summary>Answer</summary>

```
{"name":"Ahmed","city":"Lahore"}
string
```

**Explanation:** `JSON.stringify()` converts the JavaScript object into a JSON-formatted string. The `typeof` operator confirms that the result is a `"string"`, not an object.
</details>

---

**Q3.** What is the output?

```js
const jsonString = '{"fruit":"Mango","quantity":10}';
const obj = JSON.parse(jsonString);
console.log(obj.fruit);
console.log(obj.quantity + 5);
```

<details>
<summary>Answer</summary>

```
Mango
15
```

**Explanation:** `JSON.parse()` converts the JSON string back into a JavaScript object. `obj.fruit` accesses the `"Mango"` value. `obj.quantity` is the number `10`, so adding `5` gives `15` (numeric addition, not string concatenation).
</details>

---

**Q4.** What is the output?

```js
const calculator = {
  value: 100,
  getDouble: function () {
    return this.value * 2;
  },
};
console.log(calculator.getDouble());
```

<details>
<summary>Answer</summary>

```
200
```

**Explanation:** Inside the `getDouble` method, `this` refers to the `calculator` object because the method is called using dot notation (`calculator.getDouble()`). Therefore, `this.value` is `100`, and `100 * 2` equals `200`.
</details>

---

**Q5.** What is the output?

```js
const car = {
  brand: "Honda",
  model: "Civic",
  year: 2024,
};

const keys = Object.keys(car);
const values = Object.values(car);

console.log(keys);
console.log(values);
```

<details>
<summary>Answer</summary>

```
["brand", "model", "year"]
["Honda", "Civic", 2024]
```

**Explanation:** `Object.keys()` returns an array of the object's property names. `Object.values()` returns an array of the object's property values. Both follow the order in which the properties were defined.
</details>

---

**Q6.** What is the output?

```js
const student = { name: "Zain", grade: "A", score: 95 };
const { name, score } = student;
console.log(name);
console.log(score);
console.log(typeof student);
```

<details>
<summary>Answer</summary>

```
Zain
95
object
```

**Explanation:** Destructuring extracts `name` and `score` from the `student` object into individual variables. `typeof student` returns `"object"` because the original `student` variable still holds the object.
</details>

---

**Q7.** What is the output?

```js
const settings = {
  theme: "dark",
  fontSize: 16,
};

settings.language = "en";
console.log(Object.keys(settings).length);
```

<details>
<summary>Answer</summary>

```
3
```

**Explanation:** The object initially has 2 properties (`theme` and `fontSize`). A third property (`language`) is added dynamically. `Object.keys(settings)` returns `["theme", "fontSize", "language"]`, which has a `length` of `3`. Objects declared with `const` cannot be reassigned, but their properties can be added, modified, or deleted.
</details>

---

**Q8.** What is the output?

```js
const book = { title: "JavaScript Guide", pages: 350 };
const copy = JSON.parse(JSON.stringify(book));
copy.pages = 500;

console.log(book.pages);
console.log(copy.pages);
```

<details>
<summary>Answer</summary>

```
350
500
```

**Explanation:** `JSON.parse(JSON.stringify(book))` creates a deep copy of the object. Modifying `copy.pages` does not affect `book.pages` because they are completely separate objects in memory. This is a common technique for creating deep copies of objects that contain only JSON-compatible values.
</details>

---

**Q9.** What is the output?

```js
const team = {
  name: "Alpha",
  members: ["Ali", "Sara", "Zain"],
  getCount: function () {
    return this.members.length;
  },
};

console.log(team.getCount());
console.log(team.members[1]);
```

<details>
<summary>Answer</summary>

```
3
Sara
```

**Explanation:** `this.members` inside `getCount()` refers to the `members` array of the `team` object, which has 3 elements. `team.members[1]` accesses the element at index 1, which is `"Sara"` (arrays are zero-indexed).
</details>

---

**Q10.** What is the output?

```js
const product = { name: "Laptop", price: 1200, inStock: true };

for (const key in product) {
  console.log(`${key}: ${product[key]}`);
}
```

<details>
<summary>Answer</summary>

```
name: Laptop
price: 1200
inStock: true
```

**Explanation:** The `for...in` loop iterates over all enumerable properties of the object. On each iteration, `key` holds the property name and `product[key]` retrieves the corresponding value using bracket notation. Template literals format the output as `key: value`.
</details>

---

## Section D: Coding Exercises (10)

**Task 1: Student Object with Average Grade Calculator**

Create an object called `student` with the following properties:
- `name` (string)
- `age` (number)
- `grades` (array of numbers, at least 5 grades)

Add a method called `getAverageGrade` that calculates and returns the average of all grades.

```
Expected Output:
Student: Ali
Average Grade: 82
```

<details>
<summary>Hint</summary>

Use `this.grades` inside the method to access the grades array. Use `reduce()` or a loop to calculate the sum, then divide by the array's length.
</details>

---

**Task 2: Product Filter and Map**

Create an array of 5 product objects. Each product should have `name` (string) and `price` (number) properties.

1. Use `filter()` to get all products with a price under $50.
2. Use `map()` to get an array of only the product names.
3. Log both results.

```
Expected Output:
Affordable Products: [{name: "Mouse", price: 25}, {name: "Keyboard", price: 45}]
Product Names: ["Mouse", "Keyboard", "Monitor", "Headphones", "Webcam"]
```

<details>
<summary>Hint</summary>

Use `.filter(product => product.price < 50)` to filter by price. Use `.map(product => product.name)` to extract names from the original array.
</details>

---

**Task 3: JSON Convert and Restore**

1. Create a JavaScript object representing a movie with `title`, `director`, `year`, and `genres` (array) properties.
2. Convert the object to a JSON string using `JSON.stringify()`.
3. Log the JSON string.
4. Parse the JSON string back into a JavaScript object using `JSON.parse()`.
5. Log the restored object's title and genres.

```
Expected Output:
JSON String: {"title":"Inception","director":"Christopher Nolan","year":2010,"genres":["Sci-Fi","Thriller"]}
Title: Inception
Genres: Sci-Fi, Thriller
```

<details>
<summary>Hint</summary>

Use `JSON.stringify(movie)` to convert and `JSON.parse(jsonString)` to restore. Access the parsed object's properties with dot notation. Use `.join(", ")` to format the genres array.
</details>

---

**Task 4: Select and Modify a DOM Element**

Create an HTML file with a heading element that has `id="main-title"` and some default text. Write JavaScript to:

1. Select the element by its ID.
2. Change its text content to `"Welcome to JavaScript DOM"`.
3. Change its color to `"darkblue"`.

```html
<!-- HTML -->
<h1 id="main-title">Original Title</h1>
```

```
Expected Result:
The heading should display "Welcome to JavaScript DOM" in dark blue color.
```

<details>
<summary>Hint</summary>

Use `document.getElementById("main-title")` to select the element. Use `.textContent` to change the text. Use `.style.color` to change the color.
</details>

---

**Task 5: Background Color Changer Button**

Create a page with a button. When the button is clicked, the background color of the page should change to a random color.

**Requirements:**
- The button should display the text `"Change Color"`.
- Each click should produce a different random color.
- Display the current color code on the page.

<details>
<summary>Hint</summary>

Generate a random hex color using:
```js
const randomColor = "#" + Math.floor(Math.random() * 16777215).toString(16).padStart(6, "0");
```
Set `document.body.style.backgroundColor` to the generated color. Update a paragraph element with the color code.
</details>

---

**Task 6: Form Validation with Error Messages**

Create a simple registration form with the following fields:
- Username (required, at least 3 characters)
- Email (required, must contain `@`)
- Password (required, at least 6 characters)

**Requirements:**
- On form submission, validate all fields using JavaScript.
- Use `event.preventDefault()` to stop the form from refreshing.
- Display error messages below each invalid field using DOM manipulation.
- If all fields are valid, show a success message.

<details>
<summary>Hint</summary>

Add an event listener to the form's `submit` event. Check each field's `.value` property. Create error message elements with `document.createElement("p")` or show/hide pre-existing error `<span>` elements. Use `classList.add("error")` for styling.
</details>

---

**Task 7: Counter Application**

Build a counter application with the following features:

- Display the current count (starting at 0).
- An **Increment** button that increases the count by 1.
- A **Decrement** button that decreases the count by 1.
- A **Reset** button that sets the count back to 0.
- The count should never go below 0.
- Change the count color to green for positive values, red when it reaches 0.

<details>
<summary>Hint</summary>

Store the count in a variable. Each button's event listener modifies the variable and updates the display element's `textContent`. Use a conditional check to prevent negative values. Use `element.style.color` to change the color based on the count value.
</details>

---

**Task 8: Dynamic List Builder**

Create a page with an input field, an "Add" button, and an empty unordered list (`<ul>`).

**Requirements:**
- When the user types text into the input and clicks "Add", a new `<li>` item should appear in the list.
- The input field should be cleared after adding an item.
- Do not add empty items (validate the input).
- Each list item should have a "Delete" button that removes it from the list.
- Use event delegation on the `<ul>` for handling delete button clicks.

<details>
<summary>Hint</summary>

Use `document.createElement("li")` to create a new list item. Set its `textContent` or `innerHTML` to include the text and a delete button. Use `ul.appendChild(li)` to add it to the list. For event delegation, add one `click` listener on the `<ul>` and check if `event.target` is a delete button.
</details>

---

**Task 9: Image Gallery with Navigation**

Create an image gallery that displays one image at a time with "Previous" and "Next" buttons.

**Requirements:**
- Store at least 5 image URLs in an array.
- Display one image at a time.
- The "Next" button shows the next image in the array.
- The "Previous" button shows the previous image.
- The gallery should wrap around (after the last image, "Next" goes back to the first).
- Display the current image number (e.g., "Image 3 of 5").

<details>
<summary>Hint</summary>

Maintain a `currentIndex` variable. The "Next" button increments it using `(currentIndex + 1) % images.length` to wrap around. The "Previous" button decrements it using `(currentIndex - 1 + images.length) % images.length`. Update the `src` attribute of an `<img>` element to show the current image.
</details>

---

**Task 10: To-Do Application (JavaScript Phase Project)**

Build a complete To-Do application with the following features:

**Core Features:**
- An input field to type a task and an "Add" button to add it.
- Each task appears as a list item with the task text, a "Complete" button, and a "Delete" button.
- Clicking "Complete" should toggle a strikethrough style on the task (using `classList.toggle`).
- Clicking "Delete" should remove the task from the list.
- Do not allow adding empty tasks.

**Bonus Features (optional but recommended):**
- Store tasks in `localStorage` so they persist after page refresh (use `JSON.stringify` and `JSON.parse`).
- Add an "Edit" button to modify existing tasks.
- Display a task count (e.g., "3 tasks remaining").
- Add a "Clear All Completed" button that removes all completed tasks at once.

**Technologies:** HTML, CSS, Vanilla JavaScript (No frameworks)

<details>
<summary>Hint</summary>

Structure your code by keeping a `tasks` array where each task is an object `{ id, text, completed }`. Whenever a task is added, modified, or deleted, update the array and re-render the list (or manipulate the DOM directly). For localStorage, save the array with `localStorage.setItem("tasks", JSON.stringify(tasks))` and load it on page load with `JSON.parse(localStorage.getItem("tasks"))`. Use event delegation on the task list container for handling complete, edit, and delete button clicks.
</details>

---

## Section E: JavaScript Weeks 9-12 Comprehensive Review (10)

This section covers all JavaScript topics from Weeks 9 through 12 as a phase assessment. Topics include: variables, data types, operators, conditionals, loops, functions, arrays, array methods, objects, the DOM, and events.

---

**Q1.** What will be logged to the console?

```js
let x = 10;
let y = "10";
console.log(x == y);
console.log(x === y);
```

- A) `true`, `true`
- B) `true`, `false`
- C) `false`, `true`
- D) `false`, `false`

<details>
<summary>Answer</summary>

**B) `true`, `false`**

The `==` operator performs type coercion and considers `10` and `"10"` equal. The `===` operator checks both value and type, so a number and a string are not strictly equal.
</details>

---

**Q2.** Write a function called `isPalindrome` that takes a string and returns `true` if the string reads the same forwards and backwards (case-insensitive), and `false` otherwise.

```
isPalindrome("Racecar")  // true
isPalindrome("Hello")    // false
isPalindrome("Madam")    // true
```

<details>
<summary>Answer</summary>

```js
function isPalindrome(str) {
  const cleaned = str.toLowerCase();
  const reversed = cleaned.split("").reverse().join("");
  return cleaned === reversed;
}

console.log(isPalindrome("Racecar")); // true
console.log(isPalindrome("Hello"));   // false
console.log(isPalindrome("Madam"));   // true
```

**Explanation:** Convert the string to lowercase for case-insensitive comparison. Split it into an array of characters, reverse the array, and join it back into a string. Compare the original and reversed strings.
</details>

---

**Q3.** What is the output of this code?

```js
const nums = [1, 2, 3, 4, 5, 6];
const result = nums.filter(n => n % 2 === 0).map(n => n * 10);
console.log(result);
```

- A) `[1, 2, 3, 4, 5, 6]`
- B) `[20, 40, 60]`
- C) `[10, 30, 50]`
- D) `[2, 4, 6]`

<details>
<summary>Answer</summary>

**B) `[20, 40, 60]`**

`filter(n => n % 2 === 0)` keeps only even numbers: `[2, 4, 6]`. Then `map(n => n * 10)` multiplies each by 10: `[20, 40, 60]`. Method chaining applies the transformations in sequence.
</details>

---

**Q4.** What is the difference between `let`, `const`, and `var`? When should you use each?

<details>
<summary>Answer</summary>

| Feature | `var` | `let` | `const` |
|---|---|---|---|
| Scope | Function-scoped | Block-scoped | Block-scoped |
| Reassignment | Allowed | Allowed | Not allowed |
| Redeclaration | Allowed | Not allowed | Not allowed |
| Hoisting | Hoisted (initialized as `undefined`) | Hoisted (not initialized, TDZ) | Hoisted (not initialized, TDZ) |

**When to use:**
- Use `const` by default for values that should not be reassigned (most variables).
- Use `let` when the value needs to change (loop counters, accumulators, flags).
- Avoid `var` in modern JavaScript because its function-scoping and hoisting behavior can lead to bugs.
</details>

---

**Q5.** Write a function called `countVowels` that takes a string and returns the number of vowels (a, e, i, o, u) in it.

```
countVowels("Hello World")  // 3
countVowels("JavaScript")   // 3
```

<details>
<summary>Answer</summary>

```js
function countVowels(str) {
  const vowels = "aeiouAEIOU";
  let count = 0;
  for (const char of str) {
    if (vowels.includes(char)) {
      count++;
    }
  }
  return count;
}

console.log(countVowels("Hello World")); // 3
console.log(countVowels("JavaScript"));  // 3
```

**Explanation:** Loop through each character in the string. Check if the character exists in the vowels string using `includes()`. Increment the counter for each vowel found. This covers both uppercase and lowercase vowels.
</details>

---

**Q6.** What is the output?

```js
function greet(name = "Guest") {
  return `Hello, ${name}!`;
}

console.log(greet("Ali"));
console.log(greet());
```

- A) `Hello, Ali!` and `Hello, undefined!`
- B) `Hello, Ali!` and `Hello, Guest!`
- C) `Hello, Ali!` and `Hello, !`
- D) Error

<details>
<summary>Answer</summary>

**B) `Hello, Ali!` and `Hello, Guest!`**

Default parameters assign a fallback value when no argument is passed (or `undefined` is passed). When `greet("Ali")` is called, `name` is `"Ali"`. When `greet()` is called without arguments, `name` defaults to `"Guest"`.
</details>

---

**Q7.** Write a program that:
1. Creates an array of 5 student objects, each with `name` and `score` properties.
2. Uses `filter()` to find students who scored 80 or above.
3. Uses `map()` to create an array of just the names of passing students.
4. Uses `forEach()` to log each passing student's name.

<details>
<summary>Answer</summary>

```js
const students = [
  { name: "Ali", score: 92 },
  { name: "Sara", score: 75 },
  { name: "Zain", score: 88 },
  { name: "Hira", score: 64 },
  { name: "Omar", score: 81 },
];

const passingStudents = students.filter((student) => student.score >= 80);
const passingNames = passingStudents.map((student) => student.name);

passingNames.forEach((name) => {
  console.log(`${name} passed!`);
});

// Output:
// Ali passed!
// Zain passed!
// Omar passed!
```

**Explanation:** `filter()` returns a new array with students whose score is 80 or above. `map()` transforms the filtered array into an array of names. `forEach()` iterates over the names and logs each one.
</details>

---

**Q8.** What will this code log?

```js
for (let i = 0; i < 3; i++) {
  setTimeout(() => {
    console.log(i);
  }, 1000);
}
```

- A) `0, 0, 0`
- B) `3, 3, 3`
- C) `0, 1, 2`
- D) `1, 2, 3`

<details>
<summary>Answer</summary>

**C) `0, 1, 2`**

Because `let` is block-scoped, each iteration of the loop creates a new scope with its own copy of `i`. When the `setTimeout` callbacks execute after 1 second, each one logs its own value of `i`. If `var` were used instead, the answer would be `3, 3, 3` because `var` is function-scoped and all callbacks would share the same `i`.
</details>

---

**Q9.** Build a mini interactive page that combines DOM manipulation and events:
1. Create an HTML page with a text input, a "Submit" button, and an empty `<div id="output">`.
2. When the user types a name and clicks "Submit," display a personalized greeting inside the div (e.g., "Hello, Ali! Welcome to Week 12.").
3. If the input is empty, display an error message in red.
4. After displaying the greeting, clear the input field.
5. Add a keyboard event: pressing Enter in the input field should also trigger the submission.

<details>
<summary>Answer</summary>

```html
<!DOCTYPE html>
<html>
<head>
  <title>Greeting App</title>
  <style>
    .error { color: red; }
    .success { color: green; font-size: 1.2rem; }
  </style>
</head>
<body>
  <input type="text" id="nameInput" placeholder="Enter your name" />
  <button id="submitBtn">Submit</button>
  <div id="output"></div>

  <script>
    const input = document.getElementById("nameInput");
    const button = document.getElementById("submitBtn");
    const output = document.getElementById("output");

    function handleSubmit() {
      const name = input.value.trim();
      if (name === "") {
        output.textContent = "Please enter a name.";
        output.className = "error";
      } else {
        output.textContent = `Hello, ${name}! Welcome to Week 12.`;
        output.className = "success";
        input.value = "";
      }
    }

    button.addEventListener("click", handleSubmit);

    input.addEventListener("keydown", (event) => {
      if (event.key === "Enter") {
        handleSubmit();
      }
    });
  </script>
</body>
</html>
```

**Explanation:** The `handleSubmit` function validates the input, displays the appropriate message using `textContent`, and uses `className` to switch between error and success styles. The function is triggered by both the button click and the Enter key press via separate event listeners.
</details>

---

**Q10.** Complete the following challenge that brings together all JavaScript fundamentals from Weeks 9-12:

**Student Grade Manager**

Build a JavaScript program (console-based or with a simple DOM interface) that:
1. Stores an array of student objects, each with `name`, `scores` (array of numbers), and a method `getAverage()`.
2. Has a function `getTopStudent()` that returns the student with the highest average.
3. Has a function `getPassingStudents(passMark)` that uses `filter()` to return students whose average is at or above the pass mark.
4. Has a function `getSummary()` that uses `map()` to return an array of strings like `"Ali: 85 (Pass)"` or `"Sara: 45 (Fail)"` based on a pass mark of 50.
5. Logs the top student, all passing students, and the full summary.

<details>
<summary>Answer</summary>

```js
const students = [
  {
    name: "Ali",
    scores: [80, 90, 85],
    getAverage() {
      const sum = this.scores.reduce((total, s) => total + s, 0);
      return Math.round(sum / this.scores.length);
    },
  },
  {
    name: "Sara",
    scores: [40, 55, 45],
    getAverage() {
      const sum = this.scores.reduce((total, s) => total + s, 0);
      return Math.round(sum / this.scores.length);
    },
  },
  {
    name: "Zain",
    scores: [70, 75, 80],
    getAverage() {
      const sum = this.scores.reduce((total, s) => total + s, 0);
      return Math.round(sum / this.scores.length);
    },
  },
  {
    name: "Hira",
    scores: [90, 95, 92],
    getAverage() {
      const sum = this.scores.reduce((total, s) => total + s, 0);
      return Math.round(sum / this.scores.length);
    },
  },
];

function getTopStudent(studentList) {
  return studentList.reduce((top, student) => {
    return student.getAverage() > top.getAverage() ? student : top;
  });
}

function getPassingStudents(studentList, passMark) {
  return studentList.filter((student) => student.getAverage() >= passMark);
}

function getSummary(studentList, passMark) {
  return studentList.map((student) => {
    const avg = student.getAverage();
    const status = avg >= passMark ? "Pass" : "Fail";
    return `${student.name}: ${avg} (${status})`;
  });
}

// Usage
const top = getTopStudent(students);
console.log(`Top Student: ${top.name} (Average: ${top.getAverage()})`);

const passing = getPassingStudents(students, 50);
console.log("Passing Students:", passing.map((s) => s.name));

const summary = getSummary(students, 50);
summary.forEach((line) => console.log(line));

// Output:
// Top Student: Hira (Average: 92)
// Passing Students: ["Ali", "Zain", "Hira"]
// Ali: 85 (Pass)
// Sara: 47 (Fail)
// Zain: 75 (Pass)
// Hira: 92 (Pass)
```

**Explanation:** Each student object has a `getAverage()` method that uses `this.scores` and `reduce()` to calculate the average. `getTopStudent()` uses `reduce()` to compare averages. `getPassingStudents()` uses `filter()` to return students above the pass mark. `getSummary()` uses `map()` to create formatted strings. This exercise combines objects, methods, `this`, array methods, template literals, and functions.
</details>

---

**End of Practice Questions -- Week 12: Objects, DOM & Events**
