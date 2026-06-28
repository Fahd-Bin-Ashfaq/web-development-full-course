# Week 2: HTML Links, Images & Lists — Practice Questions

---

## Section A: Multiple Choice Questions (MCQs)

**Instructions:** Choose the correct answer from the given options.

---

**Q1.** Which HTML tag is used to create a hyperlink?

- A) `<link>`
- B) `<a>`
- C) `<href>`
- D) `<url>`

<details>
<summary>Answer</summary>

**B) `<a>`**

The `<a>` (anchor) tag is used to create hyperlinks in HTML. The `<link>` tag is used to link external resources such as stylesheets, not to create clickable hyperlinks on the page.

</details>

---

**Q2.** Which attribute of the `<a>` tag specifies the URL of the page the link goes to?

- A) `src`
- B) `link`
- C) `href`
- D) `url`

<details>
<summary>Answer</summary>

**C) `href`**

The `href` (Hypertext Reference) attribute specifies the destination URL that the link points to. The `src` attribute is used with elements like `<img>` and `<script>`.

</details>

---

**Q3.** What does `target="_blank"` do when added to an anchor tag?

- A) Opens the link in the same tab
- B) Opens the link in a new tab or window
- C) Opens the link in a popup dialog
- D) Prevents the link from opening

<details>
<summary>Answer</summary>

**B) Opens the link in a new tab or window**

The `target="_blank"` attribute value instructs the browser to open the linked document in a new tab or window, rather than navigating away from the current page.

</details>

---

**Q4.** Which attribute is required in the `<img>` tag according to HTML standards?

- A) `title`
- B) `width`
- C) `alt`
- D) `id`

<details>
<summary>Answer</summary>

**C) `alt`**

The `alt` attribute is required for the `<img>` tag. It provides alternative text that is displayed when the image cannot be loaded and is essential for accessibility, as screen readers use it to describe the image to visually impaired users.

</details>

---

**Q5.** Which of the following is an absolute URL?

- A) `images/photo.jpg`
- B) `../about.html`
- C) `https://www.example.com/page.html`
- D) `/contact.html`

<details>
<summary>Answer</summary>

**C) `https://www.example.com/page.html`**

An absolute URL includes the full address with the protocol (e.g., `https://`), domain name, and path. The other options are relative URLs that reference files relative to the current document or website root.

</details>

---

**Q6.** Which HTML tag is used to create an unordered (bulleted) list?

- A) `<ol>`
- B) `<ul>`
- C) `<dl>`
- D) `<list>`

<details>
<summary>Answer</summary>

**B) `<ul>`**

The `<ul>` tag creates an unordered list, which displays items with bullet points by default. The `<ol>` tag creates an ordered (numbered) list, and `<dl>` creates a description list.

</details>

---

**Q7.** What is the correct HTML for inserting an image?

- A) `<img href="image.jpg" alt="Photo">`
- B) `<image src="image.jpg" alt="Photo">`
- C) `<img src="image.jpg" alt="Photo">`
- D) `<img src="image.jpg" alt="Photo"></img>`

<details>
<summary>Answer</summary>

**C) `<img src="image.jpg" alt="Photo">`**

The `<img>` tag uses the `src` attribute to specify the image source and the `alt` attribute for alternative text. The `<img>` tag is a self-closing (void) element and does not require a closing tag.

</details>

---

**Q8.** Which image format is best suited for photographs on the web?

- A) PNG
- B) GIF
- C) SVG
- D) JPEG

<details>
<summary>Answer</summary>

**D) JPEG**

JPEG (Joint Photographic Experts Group) format is best suited for photographs because it supports millions of colors and uses lossy compression to keep file sizes manageable. PNG is better for images with transparency, GIF for simple animations, and SVG for vector graphics.

</details>

---

**Q9.** How do you create a mailto link in HTML?

- A) `<a href="email:user@example.com">Email</a>`
- B) `<a href="mailto:user@example.com">Email</a>`
- C) `<a mail="user@example.com">Email</a>`
- D) `<a href="mail://user@example.com">Email</a>`

<details>
<summary>Answer</summary>

**B) `<a href="mailto:user@example.com">Email</a>`**

The `mailto:` protocol in the `href` attribute creates a link that opens the user's default email client with the specified email address pre-filled in the "To" field.

</details>

---

**Q10.** Which tag is used for each item inside both `<ol>` and `<ul>` lists?

- A) `<item>`
- B) `<li>`
- C) `<dt>`
- D) `<entry>`

<details>
<summary>Answer</summary>

**B) `<li>`**

The `<li>` (list item) tag is used to define each item within both ordered (`<ol>`) and unordered (`<ul>`) lists. The `<dt>` tag is used in description lists (`<dl>`).

</details>

---

**Q11.** What does the `alt` attribute in the `<img>` tag provide?

- A) A tooltip when hovering over the image
- B) Alternative text for screen readers and when the image fails to load
- C) A caption displayed below the image
- D) The file name of the image

<details>
<summary>Answer</summary>

**B) Alternative text for screen readers and when the image fails to load**

The `alt` attribute provides a text description of the image. It is read aloud by screen readers for visually impaired users and is displayed as a placeholder when the image cannot be loaded. The `title` attribute provides a tooltip on hover.

</details>

---

**Q12.** Which of the following creates a nested list?

- A) Placing a `<ul>` inside an `<li>` of another list
- B) Placing a `<ul>` directly inside another `<ul>`
- C) Using the `nested` attribute on a `<ul>` tag
- D) Placing two `<ul>` tags side by side

<details>
<summary>Answer</summary>

**A) Placing a `<ul>` inside an `<li>` of another list**

To create a nested list, you place a new list (`<ul>` or `<ol>`) inside a list item (`<li>`) of the parent list. The nested list must be a child of `<li>`, not a direct child of the parent `<ul>` or `<ol>`.

</details>

---

**Q13.** Which attribute should be used alongside `target="_blank"` for security purposes?

- A) `rel="nofollow"`
- B) `rel="noopener"`
- C) `rel="external"`
- D) `rel="secure"`

<details>
<summary>Answer</summary>

**B) `rel="noopener"`**

When using `target="_blank"`, adding `rel="noopener"` (or `rel="noopener noreferrer"`) prevents the newly opened page from accessing the `window.opener` property of the original page, which protects against potential security vulnerabilities such as reverse tabnabbing.

</details>

---

**Q14.** What is a relative URL?

- A) A URL that includes the full web address with protocol and domain
- B) A URL that references a file relative to the current page's location
- C) A URL that only works on the same computer
- D) A URL that changes based on the user's browser

<details>
<summary>Answer</summary>

**B) A URL that references a file relative to the current page's location**

A relative URL specifies the path to a resource relative to the location of the current document. For example, `images/photo.jpg` refers to a file inside an `images` folder at the same level as the current page. Relative URLs do not include the protocol or domain name.

</details>

---

**Q15.** Which image format supports transparency?

- A) JPEG
- B) BMP
- C) PNG
- D) TIFF

<details>
<summary>Answer</summary>

**C) PNG**

PNG (Portable Network Graphics) supports transparency (alpha channel), making it ideal for logos, icons, and images that need a transparent background. JPEG does not support transparency.

</details>

---

## Section B: Short Answer Questions

**Instructions:** Write concise and clear answers to the following questions.

---

**Q1.** Why is the `alt` attribute important for the `<img>` tag? List at least three reasons.

<details>
<summary>Answer</summary>

The `alt` attribute is important for the following reasons:

1. **Accessibility:** Screen readers read the `alt` text aloud, allowing visually impaired users to understand the content and purpose of the image.
2. **Fallback Content:** If the image fails to load (due to a broken link, slow connection, or missing file), the browser displays the `alt` text in place of the image, so users still understand what was intended.
3. **SEO (Search Engine Optimization):** Search engines use `alt` text to understand and index images, which can improve the page's ranking in search results.
4. **Compliance:** Web accessibility standards (such as WCAG) require meaningful `alt` text for all informational images, making it a legal requirement in many jurisdictions.

</details>

---

**Q2.** Explain the difference between a relative path and an absolute path. Provide one example of each.

<details>
<summary>Answer</summary>

**Absolute Path:** An absolute path provides the complete URL to a resource, including the protocol and domain name. It works regardless of the location of the current page because it specifies the full address.

- Example: `https://www.example.com/images/logo.png`

**Relative Path:** A relative path specifies the location of a resource relative to the current document's position in the file structure. It does not include the protocol or domain.

- Example: `images/logo.png` (references a file inside an `images` folder at the same level as the current page)
- Example: `../about.html` (moves one directory up and accesses `about.html`)

**Key Difference:** Absolute paths always point to the same resource regardless of where they are used, while relative paths depend on the location of the file that references them.

</details>

---

**Q3.** When should you use an ordered list (`<ol>`) versus an unordered list (`<ul>`)? Give two practical examples of each.

<details>
<summary>Answer</summary>

**Use an ordered list (`<ol>`) when the sequence or ranking of items matters:**

1. Step-by-step instructions (e.g., a cooking recipe: Step 1 - Preheat oven, Step 2 - Mix ingredients, etc.)
2. A ranking or leaderboard (e.g., Top 5 programming languages)

**Use an unordered list (`<ul>`) when the order of items does not matter:**

1. A shopping list (e.g., Milk, Eggs, Bread, Butter)
2. A navigation menu with links (e.g., Home, About, Services, Contact)

**Rule of Thumb:** If rearranging the items would change the meaning or usefulness of the list, use `<ol>`. If the items can appear in any order without affecting meaning, use `<ul>`.

</details>

---

**Q4.** Why is it recommended to use `rel="noopener"` (or `rel="noopener noreferrer"`) with `target="_blank"`?

<details>
<summary>Answer</summary>

When a link opens in a new tab using `target="_blank"`, the newly opened page can access the original page through the `window.opener` JavaScript property. This creates a security vulnerability known as **reverse tabnabbing**, where the new page could redirect the original page to a malicious URL (such as a phishing page) without the user's knowledge.

Adding `rel="noopener"` prevents the new page from accessing `window.opener`, effectively severing the connection between the two tabs. Adding `noreferrer` goes one step further by also preventing the new page from knowing which page referred the user to it (the `Referer` header is not sent).

**Best Practice:**
```html
<a href="https://example.com" target="_blank" rel="noopener noreferrer">Visit Example</a>
```

Note: Modern browsers (since around 2021) implicitly set `rel="noopener"` for `target="_blank"` links, but explicitly adding it remains a best practice for backward compatibility and clarity.

</details>

---

**Q5.** What is the difference between the `alt` attribute and the `title` attribute on an `<img>` tag?

<details>
<summary>Answer</summary>

| Feature | `alt` Attribute | `title` Attribute |
|---|---|---|
| **Purpose** | Provides alternative text when the image cannot be displayed and for accessibility | Provides supplementary advisory information |
| **Visibility** | Displayed in place of the image when it fails to load | Displayed as a tooltip when the user hovers over the image |
| **Screen Readers** | Read aloud by screen readers as the primary description | May or may not be read, depending on the screen reader and settings |
| **Required** | Yes, required by HTML standards for all `<img>` tags | No, it is optional |
| **SEO** | Used by search engines to understand image content | Has minimal impact on SEO |

**Example:**
```html
<img src="sunset.jpg" alt="A golden sunset over the ocean" title="Sunset at Malibu Beach, 2024">
```

</details>

---

**Q6.** Describe the three types of lists available in HTML and state when each is most appropriate.

<details>
<summary>Answer</summary>

**1. Unordered List (`<ul>`):**
Displays items with bullet points. Use when listing items where the order does not matter.
```html
<ul>
  <li>HTML</li>
  <li>CSS</li>
  <li>JavaScript</li>
</ul>
```

**2. Ordered List (`<ol>`):**
Displays items with sequential numbers (or letters/roman numerals). Use when the order or ranking of items is meaningful.
```html
<ol>
  <li>Preheat the oven to 180 degrees Celsius.</li>
  <li>Mix the flour and sugar together.</li>
  <li>Bake for 25 minutes.</li>
</ol>
```

**3. Description List (`<dl>`):**
Displays a list of terms (`<dt>`) and their descriptions (`<dd>`). Use for glossaries, metadata, or any content that pairs a term with its definition.
```html
<dl>
  <dt>HTML</dt>
  <dd>HyperText Markup Language, the standard language for creating web pages.</dd>
  <dt>CSS</dt>
  <dd>Cascading Style Sheets, used for styling HTML elements.</dd>
</dl>
```

</details>

---

**Q7.** What are the key differences between JPEG, PNG, GIF, and SVG image formats? When would you use each?

<details>
<summary>Answer</summary>

| Format | Compression | Transparency | Animation | Best Used For |
|---|---|---|---|---|
| **JPEG** | Lossy | No | No | Photographs and complex images with many colors |
| **PNG** | Lossless | Yes (alpha channel) | No | Logos, icons, screenshots, images requiring transparency |
| **GIF** | Lossless | Yes (binary only) | Yes | Simple animations, small icons with limited colors (max 256) |
| **SVG** | N/A (vector) | Yes | Yes (via code) | Logos, icons, illustrations, and graphics that need to scale without losing quality |

**Guidelines:**
- Use **JPEG** for photos to keep file sizes small.
- Use **PNG** when you need transparency or pixel-perfect quality.
- Use **GIF** for simple, short animations.
- Use **SVG** for scalable graphics like logos and icons that must look sharp at any size.

</details>

---

**Q8.** Explain how anchor links (internal page navigation) work. Write the HTML required to link to a section with the heading "Contact Us" on the same page.

<details>
<summary>Answer</summary>

Anchor links allow users to jump to a specific section within the same page. They work by linking the `href` attribute of an `<a>` tag to the `id` attribute of a target element using the `#` symbol.

**Step 1:** Add an `id` attribute to the target element (the section you want to navigate to):
```html
<h2 id="contact-us">Contact Us</h2>
<p>You can reach us at info@example.com.</p>
```

**Step 2:** Create an anchor link that points to that `id`:
```html
<a href="#contact-us">Go to Contact Us</a>
```

When the user clicks the link, the browser scrolls down (or up) to the element with `id="contact-us"`. The `#` prefix in the `href` tells the browser to look for an element with that `id` on the current page rather than navigating to a different page.

</details>

---

## Section C: True or False

**Instructions:** Determine whether each statement is True or False. Review the explanation for each answer.

| # | Statement | Answer | Explanation |
|---|---|---|---|
| 1 | The `<img>` tag requires a closing tag (`</img>`). | **False** | The `<img>` tag is a void (self-closing) element in HTML. It does not have a closing tag. The correct syntax is `<img src="image.jpg" alt="description">`. |
| 2 | The `href` attribute in an anchor tag can link to an email address using the `mailto:` protocol. | **True** | Using `href="mailto:user@example.com"` creates a link that opens the user's default email client with the specified address pre-filled. |
| 3 | An ordered list (`<ol>`) always starts numbering from 1 by default. | **True** | By default, an `<ol>` starts from 1. However, you can change the starting number using the `start` attribute (e.g., `<ol start="5">`). |
| 4 | The `src` attribute of the `<img>` tag specifies alternative text for the image. | **False** | The `src` attribute specifies the source (file path or URL) of the image. The `alt` attribute provides the alternative text. |
| 5 | You can nest an unordered list inside an ordered list. | **True** | HTML allows any type of list to be nested within any other list. You can place a `<ul>` inside an `<li>` of an `<ol>`, and vice versa. |
| 6 | The `target="_self"` attribute value opens a link in a new tab. | **False** | `target="_self"` opens the link in the same tab or frame (this is the default behavior). To open in a new tab, use `target="_blank"`. |
| 7 | SVG images lose quality when scaled up. | **False** | SVG (Scalable Vector Graphics) is a vector-based format that uses mathematical paths rather than pixels. It can be scaled to any size without any loss in quality. |
| 8 | The `<li>` tag can only be used inside `<ul>` tags. | **False** | The `<li>` tag can be used inside both `<ul>` (unordered list) and `<ol>` (ordered list) elements. |
| 9 | A relative URL like `../images/photo.jpg` navigates one directory up from the current file's location. | **True** | The `..` notation moves one level up in the directory structure. So `../images/photo.jpg` goes up one folder from the current file and then into the `images` folder to find `photo.jpg`. |
| 10 | The `alt` attribute is optional and has no impact on web accessibility. | **False** | The `alt` attribute is required by HTML standards and is critical for web accessibility. Screen readers rely on `alt` text to describe images to visually impaired users, and it is a key requirement of WCAG (Web Content Accessibility Guidelines). |

---

## Section D: Code Correction

**Instructions:** Each of the following HTML code snippets contains one or more errors. Identify the errors and write the corrected code.

---

**Q1.** Find and fix the error(s) in the following code:

```html
<a src="https://www.google.com">Visit Google</a>
```

<details>
<summary>Answer</summary>

**Error:** The `<a>` tag uses `src` instead of `href`. The `src` attribute is used with elements like `<img>`, `<script>`, and `<iframe>`, not with anchor tags.

**Corrected Code:**
```html
<a href="https://www.google.com">Visit Google</a>
```

</details>

---

**Q2.** Find and fix the error(s) in the following code:

```html
<img src="photo.jpg">
<ul>
  <li>Item 1
  <li>Item 2
  <li>Item 3
</ul>
```

<details>
<summary>Answer</summary>

**Errors:**
1. The `<img>` tag is missing the required `alt` attribute.
2. The `<li>` tags are missing their closing `</li>` tags. While some browsers may render them correctly, it is best practice to always close `<li>` tags.

**Corrected Code:**
```html
<img src="photo.jpg" alt="A descriptive text for the photo">
<ul>
  <li>Item 1</li>
  <li>Item 2</li>
  <li>Item 3</li>
</ul>
```

</details>

---

**Q3.** Find and fix the error(s) in the following code:

```html
<a href="https://www.example.com" target="_blank">Click Here</a>
<img src="logo.png" alt="Company Logo"></img>
```

<details>
<summary>Answer</summary>

**Errors:**
1. The `<a>` tag with `target="_blank"` is missing the `rel="noopener noreferrer"` attribute for security.
2. The `<img>` tag has a closing `</img>` tag, but `<img>` is a void element and should not have a closing tag.

**Corrected Code:**
```html
<a href="https://www.example.com" target="_blank" rel="noopener noreferrer">Click Here</a>
<img src="logo.png" alt="Company Logo">
```

</details>

---

**Q4.** Find and fix the error(s) in the following code:

```html
<ol>
  <ul>
    <li>Sub-item A</li>
    <li>Sub-item B</li>
  </ul>
  <li>First item</li>
  <li>Second item</li>
</ol>
```

<details>
<summary>Answer</summary>

**Error:** The nested `<ul>` is placed directly inside the `<ol>` instead of inside an `<li>` element. A nested list must be a child of a list item, not a direct child of the parent list. Additionally, the nested list should logically appear within one of the parent list items.

**Corrected Code:**
```html
<ol>
  <li>First item
    <ul>
      <li>Sub-item A</li>
      <li>Sub-item B</li>
    </ul>
  </li>
  <li>Second item</li>
</ol>
```

</details>

---

**Q5.** Find and fix the error(s) in the following code:

```html
<a href="mailto:user@example.com" target="_blank">
  <img src="contact-icon" alt=>
  Email Us
</a>
```

<details>
<summary>Answer</summary>

**Errors:**
1. The `mailto:` link should not use `target="_blank"` because email links open the default email client, not a web page.
2. The `src` attribute value `"contact-icon"` is missing a file extension (e.g., `.png`, `.jpg`).
3. The `alt` attribute has no value (`alt=>`). It must have a proper string value.

**Corrected Code:**
```html
<a href="mailto:user@example.com">
  <img src="contact-icon.png" alt="Contact icon">
  Email Us
</a>
```

</details>

---

## Section E: Coding Exercises

**Instructions:** Complete each of the following tasks by writing valid HTML code. Focus on using correct syntax, proper attributes, and semantic structure.

---

### Task 1: Navigation Menu Using an Unordered List

Create a horizontal navigation menu using an unordered list (`<ul>`). The menu should contain the following links:

- **Home** — links to `index.html`
- **About** — links to `about.html`
- **Services** — links to `services.html`
- **Portfolio** — links to `portfolio.html`
- **Contact** — links to `contact.html`

**Requirements:**
- Each menu item must be a list item (`<li>`) containing an anchor (`<a>`) tag.
- Wrap the navigation in a `<nav>` element.

<details>
<summary>Sample Solution</summary>

```html
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>Navigation Menu</title>
</head>
<body>

  <nav>
    <ul>
      <li><a href="index.html">Home</a></li>
      <li><a href="about.html">About</a></li>
      <li><a href="services.html">Services</a></li>
      <li><a href="portfolio.html">Portfolio</a></li>
      <li><a href="contact.html">Contact</a></li>
    </ul>
  </nav>

</body>
</html>
```

</details>

---

### Task 2: Image Gallery Page

Create an image gallery page that displays 5 images. Each image should include:

- A descriptive `alt` attribute
- A `width` attribute set to `300`
- A heading or caption below each image describing what it shows

**Requirements:**
- Use appropriate and meaningful `alt` text for each image.
- Organize the gallery using headings and paragraphs for captions.
- You may use placeholder image URLs such as `https://via.placeholder.com/300`.

<details>
<summary>Sample Solution</summary>

```html
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>Image Gallery</title>
</head>
<body>

  <h1>My Image Gallery</h1>

  <div>
    <img src="https://via.placeholder.com/300" alt="A serene mountain landscape at sunrise" width="300">
    <p>Mountain Sunrise</p>
  </div>

  <div>
    <img src="https://via.placeholder.com/300" alt="A sandy beach with crystal clear blue water" width="300">
    <p>Tropical Beach</p>
  </div>

  <div>
    <img src="https://via.placeholder.com/300" alt="A dense forest with tall green trees" width="300">
    <p>Green Forest</p>
  </div>

  <div>
    <img src="https://via.placeholder.com/300" alt="A city skyline illuminated at night" width="300">
    <p>City Skyline at Night</p>
  </div>

  <div>
    <img src="https://via.placeholder.com/300" alt="A field of colorful wildflowers in spring" width="300">
    <p>Spring Wildflowers</p>
  </div>

</body>
</html>
```

</details>

---

### Task 3: Recipe Page

Create a recipe page for any dish of your choice. The page must include:

- A main heading with the recipe name
- An image of the dish (use a placeholder if needed) with appropriate `alt` text
- An **unordered list** of ingredients
- An **ordered list** of step-by-step cooking instructions

**Requirements:**
- Use at least 6 ingredients and 5 steps.
- Use proper list nesting if any ingredient has sub-items (e.g., "Spices: cumin, turmeric, chili powder").

<details>
<summary>Sample Solution</summary>

```html
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>Chicken Biryani Recipe</title>
</head>
<body>

  <h1>Chicken Biryani</h1>
  <img src="https://via.placeholder.com/400x300" alt="A plate of chicken biryani garnished with fresh herbs" width="400">

  <h2>Ingredients</h2>
  <ul>
    <li>500g chicken, cut into pieces</li>
    <li>2 cups basmati rice, soaked for 30 minutes</li>
    <li>2 large onions, thinly sliced</li>
    <li>1 cup yogurt</li>
    <li>Spices:
      <ul>
        <li>1 tsp cumin seeds</li>
        <li>1 tsp turmeric powder</li>
        <li>1 tsp red chili powder</li>
        <li>2 bay leaves</li>
        <li>4 green cardamom pods</li>
      </ul>
    </li>
    <li>Fresh cilantro and mint leaves for garnish</li>
    <li>3 tbsp cooking oil or ghee</li>
    <li>Salt to taste</li>
  </ul>

  <h2>Instructions</h2>
  <ol>
    <li>Heat oil in a large pot and fry the sliced onions until golden brown. Remove half and set aside for garnish.</li>
    <li>Add the chicken pieces to the pot and cook on medium heat for 5 minutes until lightly browned.</li>
    <li>Add yogurt, turmeric, chili powder, cumin seeds, bay leaves, cardamom, and salt. Cook for 10 minutes until the chicken is tender.</li>
    <li>In a separate pot, boil water with salt and cook the soaked rice until 70% done. Drain the water.</li>
    <li>Layer the partially cooked rice over the chicken mixture in the pot.</li>
    <li>Sprinkle the fried onions, fresh cilantro, and mint leaves on top of the rice.</li>
    <li>Cover the pot tightly and cook on low heat for 20 minutes until the rice is fully cooked and flavors are absorbed.</li>
  </ol>

</body>
</html>
```

</details>

---

### Task 4: Page with Internal Navigation (Anchor Links)

Create a single-page website with a navigation menu at the top that links to different sections on the same page. The page must have:

- A navigation menu with links to at least 4 sections
- Four content sections, each with a heading, a paragraph, and an image
- A "Back to Top" link at the bottom of each section

**Requirements:**
- Use `id` attributes on section headings.
- Use `#id` links in the navigation.
- Include a "Back to Top" link that scrolls to the top of the page.

<details>
<summary>Sample Solution</summary>

```html
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>Internal Navigation Page</title>
</head>
<body>

  <h1 id="top">Explore the World</h1>

  <nav>
    <ul>
      <li><a href="#asia">Asia</a></li>
      <li><a href="#europe">Europe</a></li>
      <li><a href="#africa">Africa</a></li>
      <li><a href="#americas">The Americas</a></li>
    </ul>
  </nav>

  <hr>

  <section>
    <h2 id="asia">Asia</h2>
    <img src="https://via.placeholder.com/400x200" alt="A panoramic view of the Great Wall of China" width="400">
    <p>Asia is the largest and most populous continent, home to diverse cultures, ancient civilizations, and stunning natural landscapes ranging from the Himalayas to tropical rainforests.</p>
    <a href="#top">Back to Top</a>
  </section>

  <hr>

  <section>
    <h2 id="europe">Europe</h2>
    <img src="https://via.placeholder.com/400x200" alt="The Eiffel Tower in Paris on a clear day" width="400">
    <p>Europe is known for its rich history, architectural marvels, and cultural heritage. From the canals of Venice to the fjords of Norway, it offers a wide range of experiences for every traveler.</p>
    <a href="#top">Back to Top</a>
  </section>

  <hr>

  <section>
    <h2 id="africa">Africa</h2>
    <img src="https://via.placeholder.com/400x200" alt="A herd of elephants walking across the African savanna" width="400">
    <p>Africa is a continent of breathtaking wildlife, vast deserts, lush rainforests, and vibrant cultures. It is home to some of the most iconic natural wonders on Earth, including Victoria Falls and the Sahara Desert.</p>
    <a href="#top">Back to Top</a>
  </section>

  <hr>

  <section>
    <h2 id="americas">The Americas</h2>
    <img src="https://via.placeholder.com/400x200" alt="The Statue of Liberty in New York City at sunset" width="400">
    <p>The Americas span two continents and encompass an incredible variety of landscapes, from the Amazon Rainforest to the Rocky Mountains, and cultures shaped by centuries of indigenous, European, and African heritage.</p>
    <a href="#top">Back to Top</a>
  </section>

</body>
</html>
```

</details>

---

### Task 5: "My Favorite Things" Page

Build a complete HTML page titled "My Favorite Things" that combines all the concepts learned in Week 2. The page must include:

1. A main heading and a short introductory paragraph
2. A **navigation menu** (unordered list with anchor links) linking to each section below
3. A **"Favorite Movies"** section with an ordered list (ranked) and at least one image
4. A **"Favorite Foods"** section with an unordered list of foods, including a nested list for one category (e.g., "Desserts: cake, ice cream, brownies")
5. A **"Favorite Websites"** section with at least 3 external links (opening in new tabs with `rel="noopener noreferrer"`)
6. A **"Contact Me"** section with a `mailto:` link and an image (e.g., a contact icon)
7. **"Back to Top"** links after each section
8. Proper use of `alt` attributes on all images

<details>
<summary>Sample Solution</summary>

```html
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>My Favorite Things</title>
</head>
<body>

  <h1 id="top">My Favorite Things</h1>
  <p>Welcome to my page! Here you will find a collection of my favorite movies, foods, websites, and a way to get in touch with me. Enjoy exploring!</p>

  <!-- Navigation Menu -->
  <nav>
    <ul>
      <li><a href="#movies">Favorite Movies</a></li>
      <li><a href="#foods">Favorite Foods</a></li>
      <li><a href="#websites">Favorite Websites</a></li>
      <li><a href="#contact">Contact Me</a></li>
    </ul>
  </nav>

  <hr>

  <!-- Favorite Movies Section -->
  <section>
    <h2 id="movies">Favorite Movies</h2>
    <img src="https://via.placeholder.com/400x200" alt="A collection of classic movie posters" width="400">
    <p>Here are my top 5 favorite movies of all time, ranked in order:</p>
    <ol>
      <li>The Shawshank Redemption</li>
      <li>Inception</li>
      <li>The Dark Knight</li>
      <li>Interstellar</li>
      <li>The Lord of the Rings: The Return of the King</li>
    </ol>
    <a href="#top">Back to Top</a>
  </section>

  <hr>

  <!-- Favorite Foods Section -->
  <section>
    <h2 id="foods">Favorite Foods</h2>
    <img src="https://via.placeholder.com/400x200" alt="A table full of delicious dishes from around the world" width="400">
    <p>I love trying different cuisines. Here are some of my favorite foods:</p>
    <ul>
      <li>Biryani</li>
      <li>Pizza</li>
      <li>Sushi</li>
      <li>Grilled Chicken</li>
      <li>Desserts:
        <ul>
          <li>Chocolate Cake</li>
          <li>Ice Cream</li>
          <li>Brownies</li>
          <li>Cheesecake</li>
        </ul>
      </li>
      <li>Fresh Fruit Salad</li>
    </ul>
    <a href="#top">Back to Top</a>
  </section>

  <hr>

  <!-- Favorite Websites Section -->
  <section>
    <h2 id="websites">Favorite Websites</h2>
    <p>These are some of my go-to websites for learning and entertainment:</p>
    <ul>
      <li><a href="https://developer.mozilla.org" target="_blank" rel="noopener noreferrer">MDN Web Docs</a> — The best resource for web development documentation.</li>
      <li><a href="https://www.freecodecamp.org" target="_blank" rel="noopener noreferrer">freeCodeCamp</a> — A free platform to learn coding through hands-on projects.</li>
      <li><a href="https://stackoverflow.com" target="_blank" rel="noopener noreferrer">Stack Overflow</a> — The go-to community for programming questions and answers.</li>
    </ul>
    <a href="#top">Back to Top</a>
  </section>

  <hr>

  <!-- Contact Me Section -->
  <section>
    <h2 id="contact">Contact Me</h2>
    <img src="https://via.placeholder.com/100" alt="Email contact icon" width="100">
    <p>I would love to hear from you! Feel free to reach out via email:</p>
    <p><a href="mailto:yourname@example.com">yourname@example.com</a></p>
    <a href="#top">Back to Top</a>
  </section>

</body>
</html>
```

</details>

---

## Summary

| Section | Type | Count |
|---|---|---|
| Section A | Multiple Choice Questions (MCQs) | 15 |
| Section B | Short Answer Questions | 8 |
| Section C | True or False | 10 |
| Section D | Code Correction | 5 |
| Section E | Coding Exercises | 5 |
| **Total** | | **43 Questions** |

---

*Week 2: HTML Links, Images & Lists — MERN Stack Full Course*
