# Week 5: Introduction to CSS - Practice Questions

Test your understanding of CSS fundamentals with the following practice questions. This set covers CSS syntax, selectors, specificity, styling methods, colors, fonts, text properties, backgrounds, pseudo-classes, pseudo-elements, inheritance, and the cascade.

---

## Section A: Multiple Choice Questions (15 Questions)

**Q1.** What does CSS stand for?

- A) Computer Style Sheets
- B) Cascading Style Sheets
- C) Creative Style Syntax
- D) Colorful Style Sheets

<details>
<summary>Answer</summary>

**B) Cascading Style Sheets**

CSS stands for Cascading Style Sheets. The word "cascading" refers to the way styles are applied in order of priority when multiple rules target the same element.
</details>

---

**Q2.** Which of the following is the correct CSS syntax to change the text color of a paragraph?

- A) `p {text-color: red;}`
- B) `p {font-color: red;}`
- C) `p {color: red;}`
- D) `p {text: red;}`

<details>
<summary>Answer</summary>

**C) `p {color: red;}`**

In CSS, the `color` property is used to set the text color of an element. There is no `text-color` or `font-color` property in CSS.
</details>

---

**Q3.** Which selector has the highest specificity?

- A) `.card`
- B) `#header`
- C) `div`
- D) `*`

<details>
<summary>Answer</summary>

**B) `#header`**

Specificity is calculated as follows: ID selectors (1,0,0) have the highest specificity, followed by class selectors (0,1,0), element selectors (0,0,1), and the universal selector `*` (0,0,0). Therefore, `#header` has the highest specificity of the options listed.
</details>

---

**Q4.** Which of the following is a valid way to apply an external CSS file to an HTML document?

- A) `<style src="styles.css">`
- B) `<link rel="stylesheet" href="styles.css">`
- C) `<css file="styles.css">`
- D) `<import stylesheet="styles.css">`

<details>
<summary>Answer</summary>

**B) `<link rel="stylesheet" href="styles.css">`**

The `<link>` tag with `rel="stylesheet"` and the `href` attribute pointing to the CSS file is the correct way to include an external stylesheet. It is placed inside the `<head>` section of the HTML document.
</details>

---

**Q5.** What is the correct hexadecimal color code for pure white?

- A) `#000000`
- B) `#FFFFFF`
- C) `#FF0000`
- D) `#AAAAAA`

<details>
<summary>Answer</summary>

**B) `#FFFFFF`**

In hexadecimal color notation, `#FFFFFF` represents white (maximum red, green, and blue values). `#000000` is black, `#FF0000` is red, and `#AAAAAA` is a shade of grey.
</details>

---

**Q6.** Which CSS property is used to change the font of an element?

- A) `font-style`
- B) `font-weight`
- C) `font-family`
- D) `text-font`

<details>
<summary>Answer</summary>

**C) `font-family`**

The `font-family` property specifies the typeface for the text. `font-style` controls italic/normal, `font-weight` controls boldness, and `text-font` is not a valid CSS property.
</details>

---

**Q7.** What does `rgb(0, 128, 0)` represent?

- A) Red
- B) Blue
- C) Green
- D) Yellow

<details>
<summary>Answer</summary>

**C) Green**

In the `rgb()` function, the three values represent red, green, and blue channels respectively, each ranging from 0 to 255. `rgb(0, 128, 0)` has zero red, a mid-level green, and zero blue, producing a green color.
</details>

---

**Q8.** Which property controls the space between lines of text?

- A) `letter-spacing`
- B) `word-spacing`
- C) `line-height`
- D) `text-indent`

<details>
<summary>Answer</summary>

**C) `line-height`**

The `line-height` property sets the vertical distance between lines of text. `letter-spacing` adjusts space between individual characters, `word-spacing` adjusts space between words, and `text-indent` indents the first line of a text block.
</details>

---

**Q9.** Which of the following is a pseudo-class?

- A) `::before`
- B) `::first-line`
- C) `:hover`
- D) `::after`

<details>
<summary>Answer</summary>

**C) `:hover`**

Pseudo-classes use a single colon (`:`) and select elements based on their state or position, such as `:hover`, `:focus`, `:first-child`, etc. The options with double colons (`::before`, `::after`, `::first-line`) are pseudo-elements, which target specific parts of an element's content.
</details>

---

**Q10.** What is the correct CSS syntax for a background shorthand property?

- A) `background: url("bg.jpg") no-repeat center/cover;`
- B) `bg: url("bg.jpg") no-repeat center;`
- C) `background-all: url("bg.jpg") no-repeat;`
- D) `background-style: url("bg.jpg") no-repeat center;`

<details>
<summary>Answer</summary>

**A) `background: url("bg.jpg") no-repeat center/cover;`**

The `background` shorthand property combines `background-image`, `background-repeat`, `background-position`, and `background-size` (after a `/`) into a single declaration. The other options use invalid property names.
</details>

---

**Q11.** In the HSL color model, what does the "S" stand for?

- A) Shade
- B) Saturation
- C) Strength
- D) Style

<details>
<summary>Answer</summary>

**B) Saturation**

HSL stands for Hue, Saturation, and Lightness. Saturation is a percentage value (0% to 100%) that defines how vivid or muted a color appears. A saturation of 0% produces a shade of grey, while 100% is the full, vivid color.
</details>

---

**Q12.** Which of the following properties is inherited by child elements by default?

- A) `border`
- B) `margin`
- C) `color`
- D) `padding`

<details>
<summary>Answer</summary>

**C) `color`**

In CSS, text-related properties such as `color`, `font-family`, `font-size`, and `line-height` are inherited by child elements by default. Box-model properties like `border`, `margin`, and `padding` are not inherited.
</details>

---

**Q13.** What does the `text-transform: uppercase;` declaration do?

- A) Makes the first letter of each word uppercase
- B) Makes all text uppercase
- C) Makes all text lowercase
- D) Removes all text formatting

<details>
<summary>Answer</summary>

**B) Makes all text uppercase**

The `text-transform: uppercase;` property converts all characters in the text to uppercase. To capitalize only the first letter of each word, you would use `text-transform: capitalize;`. To convert all text to lowercase, use `text-transform: lowercase;`.
</details>

---

**Q14.** Which pseudo-element is used to insert content before an element?

- A) `:before`
- B) `::first-letter`
- C) `::before`
- D) `:first-child`

<details>
<summary>Answer</summary>

**C) `::before`**

The `::before` pseudo-element (with double colons, as per the CSS3 standard) is used to insert generated content before an element's actual content. It requires the `content` property to function. While `:before` (single colon) also works for backward compatibility, the double-colon syntax is the recommended standard.
</details>

---

**Q15.** When two CSS rules have the same specificity, which rule takes effect?

- A) The first rule declared in the stylesheet
- B) The last rule declared in the stylesheet
- C) The rule with fewer properties
- D) Neither rule applies

<details>
<summary>Answer</summary>

**B) The last rule declared in the stylesheet**

This is the cascade principle in CSS. When two or more conflicting rules have the same specificity, the rule that appears last in the source order wins. This is why the order of CSS declarations matters.
</details>

---

## Section B: Short Answer Questions (8 Questions)

**Q1.** What is the difference between a class selector and an ID selector in CSS? When would you use each one?

<details>
<summary>Answer</summary>

A **class selector** (`.classname`) can be applied to multiple elements on a page and an element can have multiple classes. It uses a period (`.`) prefix in CSS.

An **ID selector** (`#idname`) must be unique on a page, meaning only one element should have a given ID. It uses a hash (`#`) prefix in CSS.

**When to use each:**
- Use **classes** for reusable styles that apply to multiple elements (e.g., `.btn`, `.card`, `.highlight`).
- Use **IDs** for unique elements that appear only once on a page (e.g., `#main-header`, `#footer`). IDs are also commonly used as JavaScript hooks and HTML anchor targets.

In practice, classes are preferred for styling because of their reusability, while IDs are typically reserved for JavaScript interactions and in-page navigation.
</details>

---

**Q2.** What is CSS specificity and how is it calculated? Provide an example to illustrate the concept.

<details>
<summary>Answer</summary>

**CSS specificity** is a scoring system that determines which CSS rule takes priority when multiple rules target the same element. It is calculated based on the types of selectors used in a rule.

**The specificity hierarchy (from highest to lowest):**

| Level | Selector Type | Example | Specificity Value |
|-------|--------------|---------|-------------------|
| 1 | Inline styles | `style="color: red;"` | (1,0,0,0) |
| 2 | ID selectors | `#header` | (0,1,0,0) |
| 3 | Class selectors, attribute selectors, pseudo-classes | `.nav`, `[type="text"]`, `:hover` | (0,0,1,0) |
| 4 | Element selectors, pseudo-elements | `div`, `::before` | (0,0,0,1) |

**Example:**

```css
p { color: blue; }                /* Specificity: 0,0,0,1 */
.intro { color: green; }          /* Specificity: 0,0,1,0 */
#main p.intro { color: red; }     /* Specificity: 0,1,1,1 */
```

If a `<p>` element has the class `intro` and is inside an element with `id="main"`, its text color will be red because `#main p.intro` has the highest specificity (0,1,1,1).
</details>

---

**Q3.** Describe the three ways to apply CSS to an HTML document. Which method is considered best practice and why?

<details>
<summary>Answer</summary>

The three ways to apply CSS to an HTML document are:

**1. Inline CSS** - Applied directly to an HTML element using the `style` attribute.
```html
<p style="color: red; font-size: 16px;">Hello</p>
```

**2. Internal (Embedded) CSS** - Written inside a `<style>` tag within the `<head>` section.
```html
<head>
  <style>
    p { color: red; font-size: 16px; }
  </style>
</head>
```

**3. External CSS** - Written in a separate `.css` file and linked to the HTML document.
```html
<head>
  <link rel="stylesheet" href="styles.css">
</head>
```

**Best Practice: External CSS**

External stylesheets are considered the best practice for the following reasons:
- **Separation of concerns:** HTML handles structure, CSS handles presentation.
- **Reusability:** A single CSS file can be linked to multiple HTML pages.
- **Maintainability:** Changes to styles only need to be made in one place.
- **Caching:** Browsers can cache external CSS files, improving page load speed on subsequent visits.
- **Cleaner HTML:** Keeps the HTML markup free of styling clutter.
</details>

---

**Q4.** What is the difference between `em` and `rem` units in CSS? Provide an example showing how they behave differently.

<details>
<summary>Answer</summary>

Both `em` and `rem` are relative CSS units, but they differ in what they are relative to:

- **`em`** is relative to the **font size of the parent element** (or the element itself for properties like `font-size`).
- **`rem`** is relative to the **font size of the root element** (`<html>`), which defaults to `16px` in most browsers.

**Example:**

```css
html { font-size: 16px; }

.parent {
  font-size: 20px;
}

.child-em {
  font-size: 1.5em;   /* 1.5 x 20px (parent) = 30px */
  padding: 1em;        /* 1 x 30px (own font-size) = 30px */
}

.child-rem {
  font-size: 1.5rem;  /* 1.5 x 16px (root) = 24px */
  padding: 1rem;       /* 1 x 16px (root) = 16px */
}
```

**Key difference:** `em` values can compound when elements are nested (a child's `em` is based on its parent, which may itself use `em`), leading to unexpected sizes. `rem` values always remain consistent because they reference the root element. For this reason, `rem` is generally preferred for font sizes, while `em` can be useful for component-level spacing that should scale with the component's own text size.
</details>

---

**Q5.** What are pseudo-classes in CSS? List at least five commonly used pseudo-classes and explain what each one does.

<details>
<summary>Answer</summary>

**Pseudo-classes** are special keywords added to selectors that target elements based on their state, position, or user interaction. They are prefixed with a single colon (`:`).

**Five commonly used pseudo-classes:**

1. **`:hover`** - Targets an element when the user hovers over it with a mouse.
   ```css
   a:hover { color: orange; }
   ```

2. **`:focus`** - Targets an element when it receives focus (e.g., when a user clicks on or tabs to an input field).
   ```css
   input:focus { border-color: blue; }
   ```

3. **`:first-child`** - Targets an element that is the first child of its parent.
   ```css
   li:first-child { font-weight: bold; }
   ```

4. **`:last-child`** - Targets an element that is the last child of its parent.
   ```css
   li:last-child { border-bottom: none; }
   ```

5. **`:nth-child(n)`** - Targets elements based on their position among siblings using a formula.
   ```css
   tr:nth-child(even) { background-color: #f2f2f2; }
   ```

Other notable pseudo-classes include `:active`, `:visited`, `:not()`, `:checked`, and `:disabled`.
</details>

---

**Q6.** How does the CSS cascade work? Explain the order of priority when multiple styles conflict.

<details>
<summary>Answer</summary>

The **CSS cascade** is the algorithm that determines which styles are applied when multiple conflicting rules target the same element. It resolves conflicts using the following criteria, in order of priority (highest to lowest):

**1. Origin and Importance**
   - `!important` declarations override normal declarations.
   - Author styles (your CSS) override browser default styles.

**2. Specificity**
   - Inline styles beat ID selectors, which beat class selectors, which beat element selectors.
   - See the specificity calculation in Q2 above.

**3. Source Order**
   - When two rules have the same specificity and origin, the rule that appears last in the source code wins.

**Example:**

```css
p { color: blue; }             /* Specificity: 0,0,0,1 */
.text { color: green; }        /* Specificity: 0,0,1,0 - WINS over element */
#intro { color: red; }         /* Specificity: 0,1,0,0 - WINS over class */
p { color: yellow !important; } /* !important - WINS over everything */
```

If a `<p class="text" id="intro">` element exists, the text color will be yellow because `!important` overrides all other cascade rules. Without the `!important` rule, the color would be red (highest specificity).
</details>

---

**Q7.** What is the difference between `background-color` and `background-image`? Can they be used together on the same element?

<details>
<summary>Answer</summary>

- **`background-color`** sets a solid color as the background of an element.
  ```css
  div { background-color: #3498db; }
  ```

- **`background-image`** sets an image (or gradient) as the background of an element.
  ```css
  div { background-image: url("pattern.png"); }
  ```

**Yes, they can be used together.** When both are applied to the same element, the background color is rendered behind the background image. This is useful as a fallback: if the image fails to load, the background color will still be visible.

```css
.hero {
  background-color: #2c3e50;
  background-image: url("hero-bg.jpg");
  background-size: cover;
  background-position: center;
}
```

You can also use the `background` shorthand to combine them:
```css
.hero {
  background: #2c3e50 url("hero-bg.jpg") no-repeat center/cover;
}
```
</details>

---

**Q8.** Explain the difference between `visibility: hidden;` and `display: none;`. When would you choose one over the other?

<details>
<summary>Answer</summary>

Both properties hide an element from the user's view, but they behave differently in terms of layout:

- **`visibility: hidden;`** hides the element visually, but the element still **occupies space** in the layout. The surrounding elements are not affected.
  ```css
  .hidden { visibility: hidden; }
  ```

- **`display: none;`** removes the element from the layout entirely. It does **not occupy any space**, and surrounding elements collapse into the empty area as if the element does not exist.
  ```css
  .removed { display: none; }
  ```

**When to use each:**

| Scenario | Recommended Property |
|----------|---------------------|
| You want to hide an element but maintain the page layout (avoid content shifting) | `visibility: hidden;` |
| You want to completely remove an element from the page flow (e.g., toggling a menu) | `display: none;` |
| You want to animate the disappearance (transition support) | `visibility: hidden;` (transitions work with `visibility` but not with `display`) |
| You want screen readers to skip the element | `display: none;` (both hide from screen readers, but `display: none` is more definitive) |
</details>

---

## Section C: True or False (10 Questions)

| # | Statement | Answer | Explanation |
|---|-----------|--------|-------------|
| 1 | CSS stands for "Creative Style Sheets." | **False** | CSS stands for Cascading Style Sheets. The "cascading" part refers to the way styles are applied based on priority rules. |
| 2 | An ID selector is more specific than a class selector. | **True** | An ID selector has a specificity of (0,1,0,0) while a class selector has (0,0,1,0), making the ID selector more specific and higher priority. |
| 3 | Inline CSS is the recommended method for styling web pages. | **False** | External CSS is the recommended method because it promotes separation of concerns, reusability across multiple pages, and easier maintenance. Inline CSS should be avoided in most cases. |
| 4 | The `font-weight` property can accept numeric values such as `100`, `400`, and `700`. | **True** | `font-weight` accepts numeric values in multiples of 100, ranging from 100 (thin) to 900 (black). `400` is equivalent to `normal` and `700` is equivalent to `bold`. |
| 5 | The universal selector `*` has the highest specificity in CSS. | **False** | The universal selector `*` has a specificity of (0,0,0,0), which is the lowest possible specificity. Inline styles have the highest specificity, followed by ID selectors. |
| 6 | Pseudo-elements use a double colon (`::`) in modern CSS syntax. | **True** | CSS3 introduced the double-colon notation (`::before`, `::after`, `::first-line`, `::first-letter`) to distinguish pseudo-elements from pseudo-classes. Single-colon syntax still works for backward compatibility. |
| 7 | The `color` property in CSS changes the background color of an element. | **False** | The `color` property changes the text (foreground) color of an element. To change the background color, you must use the `background-color` property. |
| 8 | CSS properties like `font-family` and `color` are inherited by child elements. | **True** | Text-related properties such as `font-family`, `color`, `font-size`, `line-height`, and `text-align` are inherited by child elements by default. Box-model properties like `margin`, `padding`, and `border` are not. |
| 9 | `hsl(0, 100%, 50%)` produces a blue color. | **False** | `hsl(0, 100%, 50%)` produces red. In the HSL model, the hue value of 0 (or 360) corresponds to red. Blue is at a hue of approximately 240. |
| 10 | The `!important` declaration overrides all other CSS rules regardless of specificity. | **True** | The `!important` flag gives a declaration the highest priority in the cascade, overriding any other conflicting rule regardless of selector specificity. However, if two rules both use `!important`, normal specificity rules apply between them. |

---

## Section D: Selector Challenge (5 Questions)

Study the HTML structure provided with each question and write the correct CSS selector to target the specified element(s).

---

**Q1.** Given the following HTML, write a CSS selector to target only the paragraph with the class `highlight` inside the `<div>` with the ID `content`.

```html
<div id="content">
  <p class="highlight">Important text</p>
  <p>Regular text</p>
</div>
<div id="sidebar">
  <p class="highlight">Sidebar text</p>
</div>
```

<details>
<summary>Answer</summary>

```css
#content .highlight {
  /* Your styles here */
}
```

This selector uses the descendant combinator to target only `.highlight` elements that are inside `#content`. The sidebar paragraph with the same class will not be affected.
</details>

---

**Q2.** Write a CSS selector to style the first `<li>` element inside an unordered list.

```html
<ul class="menu">
  <li>Home</li>
  <li>About</li>
  <li>Services</li>
  <li>Contact</li>
</ul>
```

<details>
<summary>Answer</summary>

```css
.menu li:first-child {
  /* Your styles here */
}
```

The `:first-child` pseudo-class targets the first child element of its parent. This selector will style only the "Home" list item. Alternatively, you could use `.menu li:nth-child(1)`.
</details>

---

**Q3.** Write a CSS selector to apply alternating background colors to table rows (even rows only).

```html
<table class="data-table">
  <tr><th>Name</th><th>Age</th></tr>
  <tr><td>Ali</td><td>22</td></tr>
  <tr><td>Sara</td><td>25</td></tr>
  <tr><td>Ahmed</td><td>28</td></tr>
  <tr><td>Fatima</td><td>21</td></tr>
</table>
```

<details>
<summary>Answer</summary>

```css
.data-table tr:nth-child(even) {
  background-color: #f2f2f2;
}
```

The `:nth-child(even)` pseudo-class matches every even-numbered child element. You could also write it as `:nth-child(2n)`. For odd rows, use `:nth-child(odd)` or `:nth-child(2n+1)`.
</details>

---

**Q4.** Write a CSS selector to target all `<a>` tags that have been visited and are inside the `<nav>` element.

```html
<nav>
  <a href="/home">Home</a>
  <a href="/about">About</a>
  <a href="/contact">Contact</a>
</nav>
<footer>
  <a href="/privacy">Privacy Policy</a>
</footer>
```

<details>
<summary>Answer</summary>

```css
nav a:visited {
  /* Your styles here */
}
```

This selector combines a descendant selector (`nav a`) with the `:visited` pseudo-class to target only visited links within the `<nav>` element. Links in the `<footer>` will not be affected.

Note: For security and privacy reasons, browsers limit which CSS properties can be styled with `:visited`. Typically, only `color`, `background-color`, `border-color`, `outline-color`, and `column-rule-color` can be changed.
</details>

---

**Q5.** Write CSS selectors to insert a decorative bullet before each list item and a horizontal line after the last list item in the following HTML.

```html
<ul class="features">
  <li>Fast Performance</li>
  <li>Easy to Use</li>
  <li>Fully Responsive</li>
</ul>
```

<details>
<summary>Answer</summary>

```css
.features li::before {
  content: "\2726 ";   /* Decorative star bullet */
  color: #e74c3c;
  font-size: 1.2em;
}

.features li:last-child::after {
  content: "";
  display: block;
  margin-top: 10px;
  border-bottom: 2px solid #ccc;
}
```

The `::before` pseudo-element inserts content before each list item's text. The `::after` pseudo-element on the `:last-child` inserts a styled horizontal line after the final list item. Both pseudo-elements require the `content` property to function, even if the value is an empty string.
</details>

---

## Section E: Coding Exercises (5 Tasks)

### Task 1: Style a Heading with Text Properties

Create an HTML page with a heading (`<h1>`) and a subheading (`<h2>`). Apply the following CSS styles using an internal stylesheet:

- `<h1>`: Set the font to `Georgia`, color to `#2c3e50`, font size to `36px`, text aligned to center, letter spacing of `3px`, and text transformed to uppercase.
- `<h2>`: Set the font to `Arial`, color to `rgb(52, 152, 219)`, font size to `24px`, font weight to `300`, and text decorated with an underline.

<details>
<summary>Expected Output / Hint</summary>

```html
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <title>Task 1 - Heading Styles</title>
  <style>
    h1 {
      font-family: Georgia, serif;
      color: #2c3e50;
      font-size: 36px;
      text-align: center;
      letter-spacing: 3px;
      text-transform: uppercase;
    }

    h2 {
      font-family: Arial, sans-serif;
      color: rgb(52, 152, 219);
      font-size: 24px;
      font-weight: 300;
      text-decoration: underline;
    }
  </style>
</head>
<body>
  <h1>Welcome to CSS</h1>
  <h2>Learning Text Properties</h2>
</body>
</html>
```
</details>

---

### Task 2: Create a Styled Card Component

Build a card component using HTML and CSS. The card should include:

- A container `<div>` with the class `card`
- A title (`<h3>`), a description paragraph (`<p>`), and a button (`<a>` styled as a button)
- Apply the following styles using class selectors:
  - Card: `300px` width, white background, `15px` padding, a subtle box shadow, and rounded corners (`8px`)
  - Title: Dark color (`#333`), `20px` font size
  - Description: Grey color (`#666`), `14px` font size, `1.6` line height
  - Button: Background color `#3498db`, white text, `10px 20px` padding, no text decoration, rounded corners, and display as `inline-block`

<details>
<summary>Expected Output / Hint</summary>

```html
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <title>Task 2 - Card Component</title>
  <style>
    body {
      font-family: Arial, sans-serif;
      background-color: #f4f4f4;
      display: flex;
      justify-content: center;
      padding: 50px;
    }

    .card {
      width: 300px;
      background-color: #ffffff;
      padding: 15px;
      border-radius: 8px;
      box-shadow: 0 2px 8px rgba(0, 0, 0, 0.1);
    }

    .card-title {
      color: #333333;
      font-size: 20px;
    }

    .card-description {
      color: #666666;
      font-size: 14px;
      line-height: 1.6;
    }

    .card-button {
      background-color: #3498db;
      color: #ffffff;
      padding: 10px 20px;
      text-decoration: none;
      border-radius: 5px;
      display: inline-block;
    }
  </style>
</head>
<body>
  <div class="card">
    <h3 class="card-title">Card Title</h3>
    <p class="card-description">
      This is a sample card component built with HTML and CSS.
      It demonstrates class selectors and common styling patterns.
    </p>
    <a href="#" class="card-button">Learn More</a>
  </div>
</body>
</html>
```
</details>

---

### Task 3: Style a Navigation Menu with Hover Effects

Create a horizontal navigation menu using an unordered list. Apply the following styles:

- Remove the default list bullets and padding
- Display list items horizontally using `display: inline-block`
- Style the links (`<a>` tags) with padding (`10px 20px`), no underline, a dark background (`#333`), and white text
- Add a hover effect that changes the background to a different color (e.g., `#3498db`) with a smooth transition
- Use the `:active` pseudo-class to add a pressed effect (darker background)

<details>
<summary>Expected Output / Hint</summary>

```html
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <title>Task 3 - Navigation Menu</title>
  <style>
    .navbar {
      list-style: none;
      padding: 0;
      margin: 0;
      background-color: #333;
    }

    .navbar li {
      display: inline-block;
    }

    .navbar a {
      display: block;
      padding: 10px 20px;
      text-decoration: none;
      color: #ffffff;
      background-color: #333;
      transition: background-color 0.3s ease;
    }

    .navbar a:hover {
      background-color: #3498db;
    }

    .navbar a:active {
      background-color: #1a5276;
    }
  </style>
</head>
<body>
  <ul class="navbar">
    <li><a href="#">Home</a></li>
    <li><a href="#">About</a></li>
    <li><a href="#">Services</a></li>
    <li><a href="#">Portfolio</a></li>
    <li><a href="#">Contact</a></li>
  </ul>
</body>
</html>
```
</details>

---

### Task 4: Create a Page with Gradient Backgrounds and Google Fonts

Build a landing page section that demonstrates the following:

- Import a Google Font (e.g., `Poppins`) using `@import` or `<link>`
- Apply the Google Font to the entire page
- Create a hero section with a **linear gradient** background (e.g., from `#667eea` to `#764ba2`)
- Add a heading and a paragraph inside the hero section with white text
- Create a secondary section below with a **radial gradient** background
- Style both sections with appropriate padding, text alignment, and font sizes

<details>
<summary>Expected Output / Hint</summary>

```html
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <title>Task 4 - Gradients & Google Fonts</title>
  <link href="https://fonts.googleapis.com/css2?family=Poppins:wght@300;400;600&display=swap" rel="stylesheet">
  <style>
    * {
      margin: 0;
      padding: 0;
      box-sizing: border-box;
    }

    body {
      font-family: 'Poppins', sans-serif;
    }

    .hero {
      background: linear-gradient(135deg, #667eea, #764ba2);
      color: #ffffff;
      text-align: center;
      padding: 100px 20px;
    }

    .hero h1 {
      font-size: 48px;
      font-weight: 600;
      margin-bottom: 20px;
    }

    .hero p {
      font-size: 18px;
      font-weight: 300;
      max-width: 600px;
      margin: 0 auto;
      line-height: 1.8;
    }

    .features {
      background: radial-gradient(circle, #f5f7fa, #c3cfe2);
      text-align: center;
      padding: 80px 20px;
    }

    .features h2 {
      font-size: 32px;
      color: #333333;
      margin-bottom: 15px;
    }

    .features p {
      font-size: 16px;
      color: #555555;
      line-height: 1.6;
    }
  </style>
</head>
<body>
  <section class="hero">
    <h1>Welcome to Our Website</h1>
    <p>
      This landing page demonstrates the use of Google Fonts
      and CSS gradient backgrounds to create visually appealing designs.
    </p>
  </section>

  <section class="features">
    <h2>Our Features</h2>
    <p>This section uses a radial gradient background for a unique visual effect.</p>
  </section>
</body>
</html>
```
</details>

---

### Task 5: Restyle an HTML Page from Week 1-4 Using External CSS

Take any HTML page you built during Weeks 1 through 4 (e.g., a personal profile page, a form, or a table) and restyle it completely using an **external CSS file**.

**Requirements:**

1. Create a separate `styles.css` file and link it to your HTML page.
2. Apply at least **10 different CSS properties** from the following categories:
   - **Typography:** `font-family`, `font-size`, `font-weight`, `line-height`, `text-align`, `text-transform`, `letter-spacing`
   - **Colors:** Use at least one `hex`, one `rgb()`, and one `hsl()` color value
   - **Backgrounds:** Apply a background color or image to at least one element
   - **Selectors:** Use at least one class selector, one ID selector, and one pseudo-class
3. Add meaningful comments in your CSS file explaining your style choices.
4. Ensure the page looks visually improved compared to the unstyled version.

<details>
<summary>Hint</summary>

Start by identifying the major sections of your HTML page (header, main content, footer). Create class names for each section and style them systematically. Here is a sample structure for your `styles.css` file:

```css
/* ===========================
   External Stylesheet for Week 5 Task 5
   =========================== */

/* --- Global Styles --- */
* {
  margin: 0;
  padding: 0;
  box-sizing: border-box;
}

body {
  font-family: 'Segoe UI', Tahoma, Geneva, Verdana, sans-serif;
  line-height: 1.6;
  color: #333;
  background-color: hsl(210, 36%, 96%);
}

/* --- Header --- */
#main-header {
  background-color: #2c3e50;
  color: rgb(255, 255, 255);
  text-align: center;
  padding: 20px;
  text-transform: uppercase;
  letter-spacing: 2px;
}

/* --- Content Section --- */
.content {
  max-width: 800px;
  margin: 20px auto;
  padding: 20px;
  background-color: #ffffff;
  border-radius: 8px;
}

/* --- Links with Pseudo-class --- */
a:hover {
  color: #e74c3c;
  text-decoration: underline;
}

/* Add more styles as needed... */
```

Focus on making the page look clean, readable, and well-structured. Compare the before and after versions to see the impact of CSS.
</details>

---

## Summary

| Section | Type | Number of Questions |
|---------|------|-------------------|
| Section A | Multiple Choice Questions | 15 |
| Section B | Short Answer Questions | 8 |
| Section C | True or False | 10 |
| Section D | Selector Challenge | 5 |
| Section E | Coding Exercises | 5 |
| **Total** | | **43 Questions** |

---

*Practice consistently and experiment with different CSS properties in your browser's developer tools. Understanding CSS fundamentals is essential before moving on to advanced layout techniques like Flexbox and Grid.*
