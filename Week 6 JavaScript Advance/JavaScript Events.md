# JavaScript Events

## What are JavaScript Events?

JavaScript events are actions or occurrences that happen in the browser and can be detected by JavaScript. These events allow web pages to respond to user interactions such as clicks, key presses, mouse movements, form submissions, page load, and more.

---

## Why Events are Important?

* Make web pages interactive
* Respond to user actions
* Control application flow
* Improve user experience

---

## Common JavaScript Events

### Mouse Events

* `click`
* `dblclick`
* `mouseover`
* `mouseout`
* `mousedown`
* `mouseup`

### Keyboard Events

* `keydown`
* `keyup`
* `keypress`

### Form Events

* `submit`
* `change`
* `focus`
* `blur`

### Window / Document Events

* `load`
* `resize`
* `scroll`
* `DOMContentLoaded`

---

## Event Handling Methods

### 1. Inline Event Handler (Not Recommended)

```html
<button onclick="alert('Button Clicked')">Click Me</button>
```

### 2. Using HTML DOM Property

```html
<button id="btn">Click Me</button>
<script>
  document.getElementById("btn").onclick = function () {
    alert("Button Clicked");
  };
</script>
```

### 3. Using addEventListener (Recommended)

```html
<button id="btn">Click Me</button>
<script>
  document.getElementById("btn").addEventListener("click", function () {
    alert("Button Clicked");
  });
</script>
```

---

## Event Object

When an event occurs, JavaScript automatically creates an event object.

```js
document.addEventListener("click", function (event) {
  console.log(event.type);      // click
  console.log(event.target);    // element that triggered event
});
```

Common Event Object Properties:

* `event.type`
* `event.target`
* `event.preventDefault()`
* `event.stopPropagation()`

---

## Event Bubbling and Capturing

### Event Bubbling (Default)

Event starts from the target element and bubbles up to parent elements.

### Event Capturing

Event starts from the parent and goes down to the target element.

```js
element.addEventListener("click", handler, true); // capturing
element.addEventListener("click", handler, false); // bubbling
```

---

## Prevent Default Behavior

```html
<a href="https://example.com" id="link">Click</a>
<script>
  document.getElementById("link").addEventListener("click", function (e) {
    e.preventDefault();
    alert("Default action prevented");
  });
</script>
```

---

## Example: Button Click Counter

```html
<button id="countBtn">Click Me</button>
<p id="count">0</p>
<script>
  let count = 0;
  document.getElementById("countBtn").addEventListener("click", () => {
    count++;
    document.getElementById("count").innerText = count;
  });
</script>
```

---

## Best Practices

* Use `addEventListener`
* Avoid inline event handlers
* Remove unused event listeners
* Use event delegation for performance

---

## Summary

JavaScript events allow interaction between users and web pages. Understanding events is essential for building dynamic and interactive web applications.

---

*Author: Fahad Ahmed*
