# Week 1: HTML Introduction & Basic Tags — Practice Questions

---

## Section A: Multiple Choice Questions (MCQs)

**Instructions:** Choose the correct option from the given choices.

---

**Q1. What does HTML stand for?**

- A) Hyper Text Markup Language
- B) High Tech Modern Language
- C) Hyper Transfer Markup Language
- D) Home Tool Markup Language

<details>
<summary>View Answer</summary>

**Answer: A) Hyper Text Markup Language**

HTML stands for Hyper Text Markup Language. It is the standard markup language used to create and structure content on web pages.
</details>

---

**Q2. Which of the following is the correct way to write an HTML element?**

- A) `<p>This is a paragraph<p>`
- B) `<p>This is a paragraph</p>`
- C) `</p>This is a paragraph<p>`
- D) `<p/>This is a paragraph</p>`

<details>
<summary>View Answer</summary>

**Answer: B) `<p>This is a paragraph</p>`**

An HTML element consists of an opening tag, content, and a closing tag. The opening tag is `<p>`, the content is the text, and the closing tag is `</p>`.
</details>

---

**Q3. What is the purpose of the `<!DOCTYPE html>` declaration?**

- A) It defines the title of the document
- B) It tells the browser which version of HTML the page is written in
- C) It creates a new HTML element
- D) It links an external CSS file

<details>
<summary>View Answer</summary>

**Answer: B) It tells the browser which version of HTML the page is written in**

The `<!DOCTYPE html>` declaration informs the browser that the document is an HTML5 document. It must be the very first line in an HTML document, before the `<html>` tag.
</details>

---

**Q4. Which tag is used to create the largest heading in HTML?**

- A) `<h6>`
- B) `<heading>`
- C) `<h1>`
- D) `<head>`

<details>
<summary>View Answer</summary>

**Answer: C) `<h1>`**

HTML provides six levels of headings from `<h1>` to `<h6>`. The `<h1>` tag produces the largest heading, and `<h6>` produces the smallest. The `<head>` tag is not a heading — it contains metadata about the document.
</details>

---

**Q5. Which of the following is a self-closing (void) tag?**

- A) `<p>`
- B) `<div>`
- C) `<br>`
- D) `<span>`

<details>
<summary>View Answer</summary>

**Answer: C) `<br>`**

The `<br>` tag is a self-closing (void) tag used to insert a line break. It does not have a closing tag because it does not contain any content. Other examples of self-closing tags include `<hr>`, `<img>`, and `<input>`.
</details>

---

**Q6. What is the difference between an HTML tag and an HTML element?**

- A) There is no difference; they are the same thing
- B) A tag is the markup syntax (e.g., `<p>`), while an element includes the opening tag, content, and closing tag
- C) An element is only the content between the tags
- D) A tag always has attributes, but an element does not

<details>
<summary>View Answer</summary>

**Answer: B) A tag is the markup syntax (e.g., `<p>`), while an element includes the opening tag, content, and closing tag**

A tag is the individual piece of markup like `<p>` or `</p>`. An element is the complete structure: the opening tag + content + closing tag combined, such as `<p>Hello World</p>`.
</details>

---

**Q7. Which tag is used to make text bold without adding semantic importance?**

- A) `<strong>`
- B) `<b>`
- C) `<em>`
- D) `<bold>`

<details>
<summary>View Answer</summary>

**Answer: B) `<b>`**

The `<b>` tag makes text visually bold without conveying any extra semantic importance. The `<strong>` tag also makes text bold but carries semantic meaning, indicating that the content is of strong importance. The `<bold>` tag does not exist in HTML.
</details>

---

**Q8. What is the correct HTML document structure?**

- A) `<html> → <head> → <body>`
- B) `<body> → <head> → <html>`
- C) `<head> → <html> → <body>`
- D) `<html> → <body> → <head>`

<details>
<summary>View Answer</summary>

**Answer: A) `<html> → <head> → <body>`**

The correct structure of an HTML document is: `<!DOCTYPE html>` declaration first, followed by the `<html>` element, which contains the `<head>` section (for metadata, title, links) and the `<body>` section (for visible content), in that order.
</details>

---

**Q9. Which HTML entity is used to display a non-breaking space?**

- A) `&space;`
- B) `&nbsp;`
- C) `&nbs;`
- D) `&#space;`

<details>
<summary>View Answer</summary>

**Answer: B) `&nbsp;`**

The `&nbsp;` entity represents a non-breaking space in HTML. It prevents the browser from collapsing multiple spaces into one and keeps words on the same line. HTML entities always begin with `&` and end with `;`.
</details>

---

**Q10. Which of the following is a semantic HTML tag?**

- A) `<div>`
- B) `<span>`
- C) `<strong>`
- D) `<b>`

<details>
<summary>View Answer</summary>

**Answer: C) `<strong>`**

The `<strong>` tag is a semantic tag because it conveys meaning — it tells the browser and assistive technologies that the enclosed text is of strong importance. Tags like `<div>` and `<span>` are non-semantic because they carry no inherent meaning about the content they contain.
</details>

---

**Q11. What does the `<em>` tag do in HTML?**

- A) Creates an embedded video
- B) Makes text italic and indicates emphasis
- C) Creates an email link
- D) Marks the end of a paragraph

<details>
<summary>View Answer</summary>

**Answer: B) Makes text italic and indicates emphasis**

The `<em>` tag is used to emphasize text. Browsers typically render it in italics, and screen readers may change the tone of voice when reading emphasized text. It is the semantic alternative to the `<i>` tag.
</details>

---

**Q12. How many heading levels does HTML provide?**

- A) 4
- B) 5
- C) 6
- D) 8

<details>
<summary>View Answer</summary>

**Answer: C) 6**

HTML provides six levels of headings, from `<h1>` (the largest and most important) to `<h6>` (the smallest and least important). Headings should be used in hierarchical order to create a logical structure for the document.
</details>

---

**Q13. Which HTML entity displays the less-than symbol (<)?**

- A) `&less;`
- B) `&lt;`
- C) `&#60`
- D) `&lte;`

<details>
<summary>View Answer</summary>

**Answer: B) `&lt;`**

The `&lt;` entity is used to display the less-than symbol (`<`) in HTML. Since `<` is used to open HTML tags, you must use the entity to display it as text. Similarly, `&gt;` is used for the greater-than symbol (`>`).
</details>

---

**Q14. Which of the following is NOT a valid HTML attribute?**

- A) `class`
- B) `id`
- C) `color`
- D) `title`

<details>
<summary>View Answer</summary>

**Answer: C) `color`**

The `color` attribute is not a standard HTML attribute. While `class`, `id`, and `title` are global attributes that can be used on almost any HTML element, colors are set using CSS, not HTML attributes. In older HTML versions, some elements supported a `color` attribute, but it is now deprecated.
</details>

---

**Q15. Where should the `<title>` tag be placed in an HTML document?**

- A) Inside the `<body>` tag
- B) Inside the `<head>` tag
- C) Before the `<!DOCTYPE>` declaration
- D) Inside the `<footer>` tag

<details>
<summary>View Answer</summary>

**Answer: B) Inside the `<head>` tag**

The `<title>` tag must be placed inside the `<head>` section of an HTML document. It defines the title that appears in the browser tab or window title bar. Every HTML document should have exactly one `<title>` element.
</details>

---

## Section B: Short Answer Questions

**Instructions:** Answer each question in 2-5 sentences.

---

**Q1. What is the difference between the `<b>` tag and the `<strong>` tag?**

<details>
<summary>View Answer</summary>

Both `<b>` and `<strong>` render text in bold in the browser. However, the key difference lies in their semantic meaning. The `<b>` tag is purely presentational — it makes text bold without implying any added importance. The `<strong>` tag, on the other hand, is a semantic tag that indicates the enclosed text has strong importance. Screen readers and search engines treat `<strong>` text as more significant, while `<b>` is treated as regular text that simply looks different.
</details>

---

**Q2. What is the `<!DOCTYPE html>` declaration and why is it important?**

<details>
<summary>View Answer</summary>

The `<!DOCTYPE html>` declaration is an instruction to the web browser that tells it which version of HTML the page is written in. In HTML5, the declaration is simply `<!DOCTYPE html>`. It must appear as the very first line in an HTML document, before the `<html>` tag. Without it, the browser may render the page in "quirks mode," which can cause inconsistent layout and styling behavior across different browsers. It is not an HTML tag — it is a document type declaration.
</details>

---

**Q3. Explain the basic structure of an HTML document.**

<details>
<summary>View Answer</summary>

A standard HTML document follows this structure:

1. **`<!DOCTYPE html>`** — Declares the document type as HTML5.
2. **`<html>`** — The root element that wraps the entire HTML document.
3. **`<head>`** — Contains metadata about the page such as the `<title>`, character encoding (`<meta charset="UTF-8">`), and links to external stylesheets or scripts.
4. **`<body>`** — Contains all the visible content that is displayed in the browser, including text, images, headings, paragraphs, and other elements.

The `<head>` section provides information about the page, while the `<body>` section provides the actual content.
</details>

---

**Q4. What are HTML entities and when do you use them?**

<details>
<summary>View Answer</summary>

HTML entities are special codes used to display reserved characters and symbols that cannot be typed directly in HTML. They begin with an ampersand (`&`) and end with a semicolon (`;`). You use them in the following situations:

- **Reserved characters:** Characters like `<`, `>`, and `&` have special meaning in HTML (they are part of the tag syntax). To display them as text, you must use `&lt;`, `&gt;`, and `&amp;` respectively.
- **Special symbols:** Symbols not found on a standard keyboard, such as copyright (`&copy;`), trademark (`&trade;`), or arrows (`&larr;`).
- **Whitespace control:** The `&nbsp;` entity inserts a non-breaking space where the browser would normally collapse multiple spaces into one.
</details>

---

**Q5. What is the difference between semantic and non-semantic HTML tags? Give examples of each.**

<details>
<summary>View Answer</summary>

**Semantic tags** carry meaning about the content they contain. They tell the browser, developers, and assistive technologies (like screen readers) what type of content is inside. Examples include `<strong>` (important text), `<em>` (emphasized text), `<header>`, `<footer>`, `<article>`, and `<nav>`.

**Non-semantic tags** provide no information about the type of content they contain. They are generic containers used purely for grouping or styling purposes. Examples include `<div>` (block-level container) and `<span>` (inline container).

Using semantic tags improves accessibility, SEO, and code readability.
</details>

---

**Q6. What are HTML attributes? How are they written?**

<details>
<summary>View Answer</summary>

HTML attributes provide additional information about an HTML element. They are always written inside the opening tag and follow the format `name="value"`. For example, in `<p class="intro">`, the attribute name is `class` and its value is `intro`.

Key points about attributes:
- They always appear in the opening tag, never in the closing tag.
- Values should be enclosed in double quotes (single quotes also work).
- Some attributes are global (usable on any element), such as `class`, `id`, `title`, and `style`.
- Some attributes are specific to certain elements, such as `src` for `<img>` and `href` for `<a>`.
</details>

---

**Q7. What is the difference between the `<i>` tag and the `<em>` tag?**

<details>
<summary>View Answer</summary>

Both `<i>` and `<em>` render text in italics, but they differ in semantic meaning. The `<i>` tag is a presentational tag that simply makes text italic without conveying any extra meaning. It is typically used for technical terms, phrases in a foreign language, or thoughts. The `<em>` tag is a semantic tag that indicates emphasis — screen readers may change the tone of voice when reading `<em>` text, and search engines consider the text to be emphasized. In modern HTML, you should prefer `<em>` when you genuinely want to stress importance and `<i>` for stylistic italics.
</details>

---

**Q8. Why should headings be used in a hierarchical order (h1 through h6)?**

<details>
<summary>View Answer</summary>

Headings should be used in hierarchical order because they define the logical structure and outline of a web page. Starting with `<h1>` as the main title and using `<h2>` through `<h6>` for subheadings creates a clear content hierarchy. This hierarchy is important for three reasons: (1) **Accessibility** — screen readers use heading levels to help users navigate through the page; (2) **SEO** — search engines use headings to understand the content and structure of a page; (3) **Readability** — a logical heading structure makes the content easier for developers and users to scan and understand. You should not skip heading levels (e.g., jumping from `<h1>` directly to `<h4>`).
</details>

---

## Section C: True or False

**Instructions:** Determine whether each statement is True or False.

| # | Statement | Answer | Explanation |
|---|-----------|--------|-------------|
| 1 | HTML is a programming language. | **False** | HTML is a markup language, not a programming language. It is used to structure content on web pages but does not have logic, loops, or conditional statements like programming languages do. |
| 2 | The `<br>` tag requires a closing tag. | **False** | The `<br>` tag is a self-closing (void) element. It does not wrap any content, so it has no closing tag. Writing `<br>` or `<br />` are both acceptable. |
| 3 | The `<title>` tag content is displayed inside the browser tab. | **True** | The text inside the `<title>` tag appears in the browser's title bar or tab. It is also used by search engines as the page title in search results. |
| 4 | You can have multiple `<h1>` tags on a single HTML page. | **True** | While it is technically valid to have multiple `<h1>` tags, it is considered a best practice to use only one `<h1>` per page for better SEO and accessibility. |
| 5 | The `<head>` tag contains content visible to the user on the web page. | **False** | The `<head>` section contains metadata, the page title, links to stylesheets, and scripts. It does not contain any content that is directly visible on the web page. Visible content goes inside the `<body>` tag. |
| 6 | The `<!DOCTYPE html>` declaration is an HTML tag. | **False** | The `<!DOCTYPE html>` declaration is not an HTML tag. It is a document type declaration that tells the browser which version of HTML the page uses. It does not have a closing tag. |
| 7 | The `<strong>` tag and the `<b>` tag produce the same visual output in the browser. | **True** | Both tags render text in bold by default. However, `<strong>` carries semantic meaning (strong importance), while `<b>` is purely presentational. |
| 8 | HTML attributes are written inside the closing tag. | **False** | HTML attributes are always written inside the opening tag, never the closing tag. For example: `<p class="intro">Text</p>`. |
| 9 | The `&amp;` entity displays the ampersand (&) symbol in HTML. | **True** | Since the `&` character is used to begin HTML entities, you must use `&amp;` to display a literal ampersand on the page. |
| 10 | The `<p>` tag is used to create a line break. | **False** | The `<p>` tag defines a paragraph, not a line break. The `<br>` tag is used to insert a line break. A paragraph element adds spacing above and below the content. |

---

## Section D: Fill in the Blanks

**Instructions:** Complete the HTML code by filling in the missing parts.

---

**Q1.** Complete the basic HTML5 document structure:

```html
______
<html>
  <______>
    <title>My First Page</title>
  </______>
  <______>
    <h1>Hello World</h1>
  </______>
</html>
```

<details>
<summary>View Answer</summary>

```html
<!DOCTYPE html>
<html>
  <head>
    <title>My First Page</title>
  </head>
  <body>
    <h1>Hello World</h1>
  </body>
</html>
```

The blanks are: `<!DOCTYPE html>`, `head`, `head`, `body`, `body`.
</details>

---

**Q2.** Write the correct tag to create the second-largest heading with the text "About Us":

```html
<____>About Us</____>
```

<details>
<summary>View Answer</summary>

```html
<h2>About Us</h2>
```

The `<h2>` tag creates the second-largest heading. Heading levels range from `<h1>` (largest) to `<h6>` (smallest).
</details>

---

**Q3.** Make the word "important" bold with semantic meaning:

```html
<p>This is an <______>important</______> announcement.</p>
```

<details>
<summary>View Answer</summary>

```html
<p>This is an <strong>important</strong> announcement.</p>
```

The `<strong>` tag is used to indicate that the text has strong importance, and it renders as bold text.
</details>

---

**Q4.** Insert a line break between the two lines:

```html
<p>Line one______Line two</p>
```

<details>
<summary>View Answer</summary>

```html
<p>Line one<br>Line two</p>
```

The `<br>` tag is used to insert a line break within a block of text. It is a self-closing tag.
</details>

---

**Q5.** Display the less-than symbol (<) and greater-than symbol (>) using HTML entities:

```html
<p>In HTML, tags are written as ______ tagname ______</p>
```

<details>
<summary>View Answer</summary>

```html
<p>In HTML, tags are written as &lt; tagname &gt;</p>
```

The entity `&lt;` displays `<` and `&gt;` displays `>`. These characters must be written as entities because they are reserved for HTML tag syntax.
</details>

---

**Q6.** Add a class attribute with the value "highlight" and an id attribute with the value "intro" to the paragraph:

```html
<p ______="______" ______="______">Welcome to my website.</p>
```

<details>
<summary>View Answer</summary>

```html
<p class="highlight" id="intro">Welcome to my website.</p>
```

Attributes are written inside the opening tag in the format `name="value"`. The `class` attribute assigns a CSS class, and the `id` attribute provides a unique identifier.
</details>

---

**Q7.** Add emphasis (italic with semantic meaning) to the word "never":

```html
<p>You should <____>never</____> skip breakfast.</p>
```

<details>
<summary>View Answer</summary>

```html
<p>You should <em>never</em> skip breakfast.</p>
```

The `<em>` tag adds semantic emphasis to text, and browsers render it in italics by default.
</details>

---

**Q8.** Insert a horizontal rule between the two paragraphs:

```html
<p>Section One Content</p>
______
<p>Section Two Content</p>
```

<details>
<summary>View Answer</summary>

```html
<p>Section One Content</p>
<hr>
<p>Section Two Content</p>
```

The `<hr>` tag creates a horizontal rule (a thematic break) and is a self-closing tag. It is used to separate sections of content visually.
</details>

---

## Section E: Coding Exercises

**Instructions:** Write the complete HTML code for each task. Practice writing the code by hand before checking the solution.

---

### Task 1: Heading Levels Page

**Difficulty:** Beginner

Create a basic HTML page that displays all six heading levels (`<h1>` through `<h6>`). Each heading should describe its own level (e.g., "This is Heading 1").

<details>
<summary>View Solution</summary>

```html
<!DOCTYPE html>
<html>
  <head>
    <title>HTML Heading Levels</title>
  </head>
  <body>
    <h1>This is Heading 1</h1>
    <h2>This is Heading 2</h2>
    <h3>This is Heading 3</h3>
    <h4>This is Heading 4</h4>
    <h5>This is Heading 5</h5>
    <h6>This is Heading 6</h6>
  </body>
</html>
```
</details>

---

### Task 2: Personal Introduction Page

**Difficulty:** Beginner

Create an HTML page about yourself. Include the following:

- A main heading with your name
- A subheading for each section (e.g., "About Me", "My Hobbies", "My Goals")
- At least two paragraphs of text
- Use `<strong>` to bold important words
- Use `<em>` to emphasize key phrases
- Use `<br>` for a line break where appropriate

<details>
<summary>View Solution</summary>

```html
<!DOCTYPE html>
<html>
  <head>
    <title>About Me</title>
  </head>
  <body>
    <h1>John Doe</h1>

    <h2>About Me</h2>
    <p>
      My name is <strong>John Doe</strong> and I am a web development student.
      I am currently learning <em>HTML</em> as my first step toward becoming
      a full-stack developer.
    </p>

    <h2>My Hobbies</h2>
    <p>
      I enjoy reading books, playing chess, and exploring new technologies.<br>
      On weekends, I like to spend time learning <strong>programming</strong>
      and building small projects.
    </p>

    <h2>My Goals</h2>
    <p>
      My primary goal is to become a <strong>MERN stack developer</strong>. I
      believe that <em>consistent practice</em> is the key to mastering any
      skill.
    </p>
  </body>
</html>
```
</details>

---

### Task 3: HTML Entities Showcase

**Difficulty:** Intermediate

Create an HTML page that demonstrates the use of HTML entities. Include the following:

- A main heading titled "HTML Entities Reference"
- Display each of the following symbols using HTML entities: less-than (`<`), greater-than (`>`), ampersand (`&`), non-breaking space, copyright symbol, quotation marks
- For each entity, show the entity code and the resulting symbol in a descriptive paragraph

<details>
<summary>View Solution</summary>

```html
<!DOCTYPE html>
<html>
  <head>
    <title>HTML Entities Reference</title>
  </head>
  <body>
    <h1>HTML Entities Reference</h1>

    <h2>Common HTML Entities</h2>

    <p>
      <strong>Less-than symbol:</strong> The entity
      <em>&amp;lt;</em> displays: &lt;
    </p>

    <p>
      <strong>Greater-than symbol:</strong> The entity
      <em>&amp;gt;</em> displays: &gt;
    </p>

    <p>
      <strong>Ampersand:</strong> The entity
      <em>&amp;amp;</em> displays: &amp;
    </p>

    <p>
      <strong>Non-breaking space:</strong> The entity
      <em>&amp;nbsp;</em> creates a space that prevents line breaking.
      Example: Word1&nbsp;&nbsp;&nbsp;&nbsp;Word2
    </p>

    <p>
      <strong>Copyright symbol:</strong> The entity
      <em>&amp;copy;</em> displays: &copy;
    </p>

    <p>
      <strong>Quotation marks:</strong> The entity
      <em>&amp;quot;</em> displays: &quot;Hello World&quot;
    </p>

    <hr>

    <h2>Why Use HTML Entities?</h2>
    <p>
      Characters like <strong>&lt;</strong>, <strong>&gt;</strong>, and
      <strong>&amp;</strong> are reserved in HTML. If you type them directly,
      the browser may interpret them as HTML code. Entities ensure these
      characters are displayed correctly as text.
    </p>

    <p>&copy; 2026 HTML Entities Showcase. All rights reserved.</p>
  </body>
</html>
```
</details>

---

### Task 4: News Article Page

**Difficulty:** Intermediate

Create an HTML page that resembles a news article. Include the following:

- A main heading for the article title
- A subheading for the author name and date
- At least three paragraphs for the article body
- Use `<strong>` for key facts or names
- Use `<em>` for quotes or emphasis
- Use `<hr>` to separate the article from the footer
- A footer paragraph with a copyright notice using the `&copy;` entity

<details>
<summary>View Solution</summary>

```html
<!DOCTYPE html>
<html>
  <head>
    <title>Tech Industry News</title>
  </head>
  <body>
    <h1>Web Development Continues to Grow in 2026</h1>
    <h3>By <strong>Jane Smith</strong> | June 25, 2026</h3>

    <p>
      The demand for <strong>web developers</strong> has reached an all-time
      high in 2026, with companies across every industry seeking skilled
      professionals to build and maintain their online presence. According to
      recent reports, the number of job postings for web development roles has
      increased by <strong>35%</strong> compared to last year.
    </p>

    <p>
      <em>"Full-stack development skills, particularly in the MERN stack, are
      among the most sought-after in the tech job market,"</em> said Dr.
      <strong>Ahmed Khan</strong>, a technology analyst at TechWatch Research.
      He emphasized that beginners who invest time in learning HTML, CSS, and
      JavaScript have a strong foundation for a successful career.
    </p>

    <p>
      Industry experts recommend starting with <strong>HTML</strong> as the
      first step in the web development journey. Understanding the structure
      of web pages provides the groundwork for learning CSS for styling and
      JavaScript for interactivity. Many free and paid resources are available
      online for aspiring developers to begin their learning path.
    </p>

    <p>
      As the digital landscape continues to evolve, the ability to build
      responsive and accessible websites remains a <em>critical skill</em>
      for developers at every level.
    </p>

    <hr>

    <p>
      <em>&copy; 2026 Tech News Daily. All rights reserved.</em>
    </p>
  </body>
</html>
```
</details>

---

### Task 5: Complete "About Me" Webpage

**Difficulty:** Advanced

Build a complete "About Me" webpage using all the HTML tags and concepts learned in Week 1. Your page must include:

- Proper HTML5 document structure with `<!DOCTYPE html>`
- A meaningful `<title>`
- All six heading levels used appropriately
- Multiple paragraphs with `<p>`
- Text formatting with `<strong>`, `<em>`, `<b>`, and `<i>`
- Line breaks with `<br>`
- Horizontal rules with `<hr>` to separate sections
- At least three different HTML entities
- Both semantic and non-semantic tags

Structure the page with the following sections: Header/Name, About Me, Education, Skills, Hobbies, and a Footer with a copyright notice.

<details>
<summary>View Solution</summary>

```html
<!DOCTYPE html>
<html>
  <head>
    <title>About Me - Sarah Ahmed</title>
  </head>
  <body>
    <!-- Header Section -->
    <h1>Sarah Ahmed</h1>
    <h2>Aspiring Full-Stack Web Developer</h2>
    <p>
      <em>Welcome to my personal webpage!</em><br>
      I am passionate about building beautiful &amp; functional websites.
    </p>

    <hr>

    <!-- About Me Section -->
    <h2>About Me</h2>
    <p>
      My name is <strong>Sarah Ahmed</strong> and I am an aspiring
      <strong>MERN stack developer</strong>. I am currently enrolled in a
      comprehensive web development course where I am learning everything
      from <em>HTML basics</em> to advanced back-end development.
    </p>
    <p>
      I believe that <em>every expert was once a beginner</em>, and I am
      committed to putting in the work needed to master web development. My
      journey begins with <strong>HTML</strong> &mdash; the foundation of
      every website.
    </p>

    <hr>

    <!-- Education Section -->
    <h3>Education</h3>
    <p>
      <strong>Bachelor of Science in Computer Science</strong><br>
      <i>University of Technology</i> &mdash; 2022 &ndash; 2026
    </p>
    <h4>Relevant Coursework</h4>
    <p>
      Introduction to Programming, Data Structures, Web Technologies,
      and Database Management Systems.
    </p>

    <hr>

    <!-- Skills Section -->
    <h3>Skills</h3>
    <h5>Currently Learning</h5>
    <p>
      <strong>HTML5</strong> &bull; CSS3 &bull; JavaScript &bull; React.js
      &bull; Node.js &bull; Express.js &bull; MongoDB
    </p>
    <p>
      <em>Note: I am at the beginning of my journey, and this list will
      grow as I progress through the course!</em>
    </p>

    <hr>

    <!-- Hobbies Section -->
    <h3>Hobbies &amp; Interests</h3>
    <p>
      When I am not coding, I enjoy the following activities:
    </p>
    <p>
      <b>Reading</b> &ndash; I love reading technology blogs and books on
      software development.<br>
      <b>Problem Solving</b> &ndash; I enjoy solving logical puzzles and
      coding challenges.<br>
      <b>Photography</b> &ndash; Capturing moments is another creative
      outlet for me.
    </p>

    <hr>

    <!-- Contact Section -->
    <h4>Get in Touch</h4>
    <p>
      Feel free to reach out to me for collaborations or just to say hello!
    </p>
    <p>
      Email: sarah.ahmed@example.com<br>
      Location: Karachi, Pakistan
    </p>

    <hr>

    <!-- Footer Section -->
    <h6>Footer</h6>
    <p>
      <em>&copy; 2026 Sarah Ahmed. All rights reserved.</em><br>
      <small>Built with &hearts; using HTML5</small>
    </p>
  </body>
</html>
```

**Tags used in this solution:**
- Document structure: `<!DOCTYPE html>`, `<html>`, `<head>`, `<title>`, `<body>`
- Headings: `<h1>`, `<h2>`, `<h3>`, `<h4>`, `<h5>`, `<h6>`
- Text: `<p>`, `<br>`, `<hr>`
- Semantic formatting: `<strong>`, `<em>`
- Non-semantic formatting: `<b>`, `<i>`, `<small>`
- HTML entities: `&copy;`, `&amp;`, `&mdash;`, `&ndash;`, `&bull;`, `&hearts;`
- Comments: `<!-- -->`
</details>

---

## Summary

| Section | Type | Number of Questions |
|---------|------|:-------------------:|
| Section A | Multiple Choice Questions (MCQs) | 15 |
| Section B | Short Answer Questions | 8 |
| Section C | True or False | 10 |
| Section D | Fill in the Blanks | 8 |
| Section E | Coding Exercises | 5 |
| **Total** | | **46** |

---

> **Tip:** Try answering all questions without looking at the solutions first. After completing each section, review the answers and revisit any topics where you made mistakes. Practice the coding exercises by typing the code in a text editor and opening the HTML files in your browser to see the results.
