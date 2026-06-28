# Week 1: Introduction to HTML & Basic Tags

> **Course:** MERN Stack Web Development  
> **Prerequisites:** Week 0 (Basic Computing)  
> **Objective:** Understand what HTML is, set up your development environment, and write your first web pages using basic HTML tags.

---

## Table of Contents

1. [What is HTML?](#1-what-is-html)
2. [History of HTML](#2-history-of-html)
3. [How Browsers Render HTML](#3-how-browsers-render-html)
4. [Setting Up the Development Environment](#4-setting-up-the-development-environment)
5. [HTML Document Structure](#5-html-document-structure)
6. [Your First HTML Page](#6-your-first-html-page)
7. [Headings](#7-headings)
8. [Paragraphs](#8-paragraphs)
9. [Line Breaks and Horizontal Rules](#9-line-breaks-and-horizontal-rules)
10. [Text Formatting Tags](#10-text-formatting-tags)
11. [Difference Between Visual and Semantic Tags](#11-difference-between-visual-and-semantic-tags)
12. [HTML Comments](#12-html-comments)
13. [HTML Entities](#13-html-entities)
14. [Summary and Key Takeaways](#14-summary-and-key-takeaways)

---

## 1. What is HTML?

**HTML** stands for **HyperText Markup Language**. It is the standard language used to create and structure content on the World Wide Web. Every website you have ever visited -- Google, YouTube, Facebook, Amazon -- is built using HTML at its core.

Let us break the name down:

| Word       | Meaning                                                        |
|------------|----------------------------------------------------------------|
| HyperText  | Text that contains links to other text or pages                |
| Markup     | A system of annotations (tags) that define structure           |
| Language   | A set of rules and syntax that browsers understand             |

### The Skeleton Analogy

Think of a website like a human body:

```
    THE HUMAN BODY                    A WEBSITE
    ==============                    =========

    Skeleton (bones)        <--->     HTML (structure)
    Skin & appearance       <--->     CSS (styling)
    Muscles & movement      <--->     JavaScript (behavior)
```

Just as the skeleton gives shape and structure to the human body -- determining where the head is, where the arms are, and how tall the body stands -- HTML gives structure to a web page. It determines where the heading goes, where the paragraph sits, and where images appear.

Without a skeleton, the human body would be a shapeless mass. Without HTML, a website would be nothing but raw, unstructured text with no headings, no paragraphs, no images, and no links.

```
    +-------------------------------------------------------+
    |                    HUMAN BODY                          |
    |                                                        |
    |       O        <-- Skull = <head> (metadata)           |
    |      /|\       <-- Ribcage = <body> (visible content)  |
    |      / \       <-- Legs = <footer> (base/support)      |
    |                                                        |
    |   Skeleton = HTML    (gives STRUCTURE)                  |
    |   Skin     = CSS     (gives APPEARANCE)                 |
    |   Muscles  = JS      (gives MOVEMENT/INTERACTION)      |
    +-------------------------------------------------------+
```

### Real-Life Example

Imagine you are building a house:

1. **HTML** is the bricks, walls, doors, and windows -- the raw structure.
2. **CSS** is the paint, wallpaper, flooring, and decorations -- the visual style.
3. **JavaScript** is the electricity, plumbing, and smart home features -- the interactive functionality.

You always start with the structure (HTML) before you paint it (CSS) or wire it (JavaScript). That is exactly why HTML is the first thing you learn in web development.

### What HTML is NOT

- HTML is **not** a programming language. It does not have logic, loops, or conditions.
- HTML is a **markup language**. It labels and organizes content so that browsers know how to display it.

---

## 2. History of HTML

HTML was created by **Sir Tim Berners-Lee**, a British computer scientist who is widely regarded as the inventor of the World Wide Web. He developed HTML in **1991** while working at **CERN** (the European Organization for Nuclear Research) in Geneva, Switzerland.

His goal was simple: create a way for scientists to share research documents across the internet, with clickable links connecting related papers.

### Timeline of HTML Versions

```
  1991        1995        1997        1999        2014       Present
   |           |           |           |           |           |
   v           v           v           v           v           v
 HTML 1.0    HTML 2.0    HTML 3.2    HTML 4.01   HTML5      HTML5
 (Birth)    (Standard)  (Tables,   (CSS-ready, (Modern    (Living
                         Scripts)    Frames)     Web Apps)  Standard)
   |           |           |           |           |           |
   +-----------+-----------+-----------+-----------+-----------+
                    Evolution of HTML
```

| Version      | Year | Key Features                                                          |
|--------------|------|-----------------------------------------------------------------------|
| HTML 1.0     | 1991 | Basic tags -- headings, paragraphs, links. Very limited.              |
| HTML 2.0     | 1995 | First official standard. Added forms and basic input elements.        |
| HTML 3.2     | 1997 | Added tables, applets, and text flow around images.                   |
| HTML 4.01    | 1999 | Introduced CSS support, scripting, accessibility features, frames.    |
| XHTML 1.0    | 2000 | Stricter XML-based version of HTML 4. Required well-formed documents. |
| HTML5        | 2014 | Major overhaul. Added `<video>`, `<audio>`, `<canvas>`, semantic tags, local storage, and much more. |
| HTML5 (Living Standard) | Ongoing | Continuously updated by WHATWG. No more version numbers. |

### Key Takeaway

HTML5 is the version we use today. It is maintained as a **living standard**, meaning it is constantly being improved. You do not need to memorize old versions, but understanding the evolution helps you appreciate why certain tags exist and why modern HTML is so powerful.

---

## 3. How Browsers Render HTML

When you open a website, your browser (Chrome, Firefox, Edge, Safari) performs a series of steps to convert raw HTML code into the visual page you see on screen.

### The Rendering Pipeline

```
  +------------------+       +------------------+       +------------------+
  |                  |       |                  |       |                  |
  |   HTML File      | ----> |   Web Browser    | ----> |  Visual Output   |
  |   (source code)  |       |   (parser &      |       |  (what you see   |
  |                  |       |    renderer)     |       |   on screen)     |
  +------------------+       +------------------+       +------------------+

       index.html              Chrome / Firefox          The rendered page
    (text with tags)          (reads & interprets)       (headings, text,
                                                          images, links)
```

### Step-by-Step Process

```
  Step 1: You write HTML code and save it as a .html file
            |
            v
  Step 2: You open the file in a browser (or use a local server)
            |
            v
  Step 3: The browser PARSES the HTML
          (reads each tag and understands the structure)
            |
            v
  Step 4: The browser builds a DOM (Document Object Model)
          (a tree-like representation of your page)
            |
            v
  Step 5: The browser RENDERS the page
          (draws the visual output on your screen)
```

### The DOM Tree (Preview)

When a browser reads this HTML:

```html
<html>
  <head>
    <title>My Page</title>
  </head>
  <body>
    <h1>Hello</h1>
    <p>Welcome to my website.</p>
  </body>
</html>
```

It builds a tree structure in memory:

```
                        html
                       /    \
                    head     body
                     |       /  \
                   title    h1    p
                     |       |     |
                  "My Page" "Hello" "Welcome to my website."
```

You will learn much more about the DOM in later weeks when you study JavaScript. For now, just understand that the browser reads your HTML and converts it into a visual page.

---

## 4. Setting Up the Development Environment

Before you can write HTML, you need three things:

```
  +-------------------+    +-------------------+    +-------------------+
  |                   |    |                   |    |                   |
  |   CODE EDITOR     |    |   LOCAL SERVER    |    |   WEB BROWSER     |
  |   (VS Code)       |    |   (Live Server)   |    |   (Chrome)        |
  |                   |    |                   |    |                   |
  |  Where you WRITE  |    |  Serves your page |    |  Where you VIEW   |
  |  your HTML code   |    |  and auto-reloads |    |  your results     |
  |                   |    |                   |    |                   |
  +-------------------+    +-------------------+    +-------------------+
```

### 4.1 Installing Visual Studio Code (VS Code)

VS Code is a free, lightweight, and powerful code editor made by Microsoft. It is the most popular editor for web development.

**Steps:**

1. Open your browser and go to [https://code.visualstudio.com](https://code.visualstudio.com)
2. Click the **Download** button for your operating system (Windows, macOS, or Linux).
3. Run the installer and follow the on-screen instructions.
4. During installation, check the box that says **"Add to PATH"** (important for later).
5. Launch VS Code after installation.

### 4.2 Installing the Live Server Extension

Live Server is a VS Code extension that creates a local development server. When you save your HTML file, it automatically reloads the page in your browser -- no manual refreshing needed.

**Steps:**

1. Open VS Code.
2. Click the **Extensions** icon in the left sidebar (it looks like four squares).
3. In the search bar, type **"Live Server"**.
4. Find the extension by **Ritwick Dey** (it has millions of downloads).
5. Click **Install**.
6. After installation, you will see a **"Go Live"** button in the bottom-right corner of VS Code.

### 4.3 Setting Up Google Chrome

Chrome is the recommended browser for web development because of its powerful Developer Tools (DevTools).

**Steps:**

1. Download Chrome from [https://www.google.com/chrome](https://www.google.com/chrome) if you do not already have it.
2. Set it as your default browser (recommended but not required).
3. Learn the shortcut **F12** or **Ctrl + Shift + I** to open Developer Tools (you will use this constantly).

### 4.4 Your First Workflow

```
  +----------+     Write Code     +----------+     Auto-Reload     +----------+
  |          | -----------------> |          | ------------------> |          |
  |  VS Code |                    |   Live   |                     |  Chrome  |
  |          | <----------------- |  Server  | <------------------ |          |
  +----------+     Save File      +----------+     View Output     +----------+
                  (Ctrl + S)
```

1. Create a new folder on your computer called `week-1-html`.
2. Open that folder in VS Code (File > Open Folder).
3. Create a new file called `index.html`.
4. Write your HTML code.
5. Right-click the file and select **"Open with Live Server"** (or click "Go Live" in the status bar).
6. Chrome will open automatically showing your page.
7. Every time you save (Ctrl + S), the browser refreshes automatically.

---

## 5. HTML Document Structure

Every HTML page follows a specific structure. Think of it as a template that every web page must have, just like every formal letter has a date, salutation, body, and closing.

### The Anatomy of an HTML Document

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>My First Web Page</title>
</head>
<body>
    <h1>Hello, World!</h1>
    <p>This is my first web page.</p>
</body>
</html>
```

### Visual Diagram of the Structure

```
+------------------------------------------------------------------+
|  <!DOCTYPE html>                                                  |
|  (Declaration: Tells the browser this is an HTML5 document)       |
|                                                                   |
|  +--------------------------------------------------------------+ |
|  | <html lang="en">                                             | |
|  | (Root element: The container for EVERYTHING)                 | |
|  |                                                              | |
|  |  +----------------------------------------------------------+| |
|  |  | <head>                                                    || |
|  |  | (The "brain" -- invisible to users)                       || |
|  |  |                                                           || |
|  |  |   <meta charset="UTF-8">                                 || |
|  |  |   <meta name="viewport" content="...">                   || |
|  |  |   <title>My First Web Page</title>                       || |
|  |  |                                                           || |
|  |  +----------------------------------------------------------+| |
|  |                                                              | |
|  |  +----------------------------------------------------------+| |
|  |  | <body>                                                    || |
|  |  | (The "body" -- everything visible on the page)            || |
|  |  |                                                           || |
|  |  |   <h1>Hello, World!</h1>                                 || |
|  |  |   <p>This is my first web page.</p>                      || |
|  |  |                                                           || |
|  |  +----------------------------------------------------------+| |
|  |                                                              | |
|  | </html>                                                      | |
|  +--------------------------------------------------------------+ |
+------------------------------------------------------------------+
```

### Breakdown of Each Part

| Element                    | Purpose                                                                                 |
|----------------------------|-----------------------------------------------------------------------------------------|
| `<!DOCTYPE html>`          | Declares the document type. Tells the browser to use HTML5 standards.                   |
| `<html lang="en">`        | The root element that wraps the entire page. `lang="en"` specifies the language.        |
| `<head>`                   | Contains metadata (information about the page). Nothing here is visible on the page.    |
| `<meta charset="UTF-8">`  | Specifies character encoding. UTF-8 supports virtually all characters and symbols.      |
| `<meta name="viewport">`  | Makes the page responsive on mobile devices.                                            |
| `<title>`                  | Sets the text that appears on the browser tab.                                          |
| `<body>`                   | Contains all the content that is visible to the user -- text, images, links, etc.       |

### Real-Life Analogy

Think of an HTML document like a book:

```
  +----------------------------------+
  |           BOOK ANALOGY           |
  +----------------------------------+
  |                                  |
  |  <!DOCTYPE html>  =  "This is   |
  |                       a novel"   |
  |                                  |
  |  <html>           =  The entire  |
  |                       book       |
  |                                  |
  |  <head>            =  The title  |
  |                       page &     |
  |                       copyright  |
  |                       info       |
  |                                  |
  |  <title>           =  The title  |
  |                       on the     |
  |                       book cover |
  |                                  |
  |  <body>            =  All the    |
  |                       chapters   |
  |                       and text   |
  |                       the reader |
  |                       actually   |
  |                       reads      |
  +----------------------------------+
```

---

## 6. Your First HTML Page

Let us build your first web page from scratch, step by step.

### Step 1: Create the Project Folder

1. Create a folder on your desktop called `my-first-page`.
2. Open VS Code.
3. Go to **File > Open Folder** and select the folder you just created.

### Step 2: Create the HTML File

1. In the VS Code Explorer (left panel), click the **New File** icon.
2. Name the file `index.html`.

> **Why "index.html"?** Web servers look for a file named `index.html` by default when someone visits a website. It is a convention, like naming the front door of a building "Main Entrance."

### Step 3: Write the HTML Code

Type the following code into `index.html`:

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>My First Page</title>
</head>
<body>
    <h1>Welcome to My First Web Page!</h1>
    <p>My name is [Your Name] and I am learning HTML.</p>
    <p>HTML stands for HyperText Markup Language.</p>
    <p>This is the beginning of my web development journey.</p>
</body>
</html>
```

### Step 4: Preview in the Browser

1. Save the file with **Ctrl + S**.
2. Right-click anywhere in the editor.
3. Select **"Open with Live Server"**.
4. Your default browser will open and display your page.

### Step 5: Experiment!

Try changing the text inside `<h1>` and `<p>` tags. Save the file and watch the browser update automatically. This instant feedback loop is one of the best parts of learning HTML.

> **Pro Tip:** In VS Code, type `!` (exclamation mark) and press **Tab** or **Enter**. VS Code will generate the entire HTML boilerplate for you automatically. This shortcut is called **Emmet**.

---

## 7. Headings

Headings define titles and subtitles on a web page. HTML provides six levels of headings, from `<h1>` (the largest and most important) to `<h6>` (the smallest and least important).

### All Six Heading Levels

```html
<h1>Heading Level 1</h1>
<h2>Heading Level 2</h2>
<h3>Heading Level 3</h3>
<h4>Heading Level 4</h4>
<h5>Heading Level 5</h5>
<h6>Heading Level 6</h6>
```

### Visual Size Comparison

```
  +--------------------------------------------------+
  |                                                  |
  |  ███  Heading 1  ███    (largest, main title)    |
  |                                                  |
  |  ██  Heading 2  ██     (section title)           |
  |                                                  |
  |  █  Heading 3  █       (sub-section)             |
  |                                                  |
  |  Heading 4              (sub-sub-section)        |
  |                                                  |
  |  Heading 5              (minor heading)          |
  |                                                  |
  |  Heading 6              (smallest heading)       |
  |                                                  |
  +--------------------------------------------------+
```

### When to Use Each Heading

| Heading | Purpose                              | Real-Life Example                      |
|---------|--------------------------------------|----------------------------------------|
| `<h1>`  | Main page title. Use only **once**.  | The name of a newspaper                |
| `<h2>`  | Major section titles.                | Section names like "Sports," "Weather" |
| `<h3>`  | Sub-sections within an `<h2>`.       | "Premier League Results" under Sports  |
| `<h4>`  | Sub-sub-sections within an `<h3>`.   | "Match Highlights" under a team name   |
| `<h5>`  | Minor headings. Rarely used.        | Fine-print categories                  |
| `<h6>`  | Smallest heading. Very rarely used.  | Footnote headings                      |

### Heading Hierarchy (Like a Book)

```
  <h1> Book Title
    |
    +-- <h2> Chapter 1
    |     |
    |     +-- <h3> Section 1.1
    |     |     |
    |     |     +-- <h4> Sub-section 1.1.1
    |     |
    |     +-- <h3> Section 1.2
    |
    +-- <h2> Chapter 2
          |
          +-- <h3> Section 2.1
```

### Important Rules

1. **Use only one `<h1>` per page.** It represents the main title of the page, just like a book has only one title.
2. **Do not skip heading levels.** Go from `<h1>` to `<h2>` to `<h3>`, not from `<h1>` directly to `<h4>`.
3. **Headings are not for making text big.** Use them for structure. If you want big text without heading meaning, use CSS instead.

### Example: A Blog Post

```html
<h1>How to Learn Web Development in 2024</h1>

<h2>Step 1: Learn HTML</h2>
<p>HTML is the foundation of every website...</p>

<h3>What is HTML?</h3>
<p>HTML stands for HyperText Markup Language...</p>

<h3>Why Start with HTML?</h3>
<p>Because every web page is built with it...</p>

<h2>Step 2: Learn CSS</h2>
<p>CSS makes your pages look beautiful...</p>

<h2>Step 3: Learn JavaScript</h2>
<p>JavaScript adds interactivity...</p>
```

---

## 8. Paragraphs

The `<p>` tag defines a paragraph of text. It is one of the most frequently used HTML tags.

### Basic Usage

```html
<p>This is a paragraph. It contains one or more sentences about a single topic.</p>

<p>This is another paragraph. Notice that the browser automatically adds
   space between paragraphs.</p>
```

### Key Behaviors

1. **Automatic spacing:** The browser adds vertical space (margin) before and after each `<p>` element.
2. **Whitespace collapsing:** Multiple spaces, tabs, and line breaks inside a `<p>` tag are collapsed into a single space.

### Whitespace Collapsing in Action

```html
<!-- What you write: -->
<p>This    has     many      spaces    and
   line breaks
   in the source code.</p>

<!-- What the browser displays: -->
<!-- "This has many spaces and line breaks in the source code." -->
```

The browser treats all consecutive whitespace characters as a single space. This is an important concept to remember. If you need to preserve exact spacing or force a line break, you will need special tags (covered in the next section).

### Real-Life Analogy

Think of `<p>` tags like paragraphs in a newspaper article. Each paragraph covers one idea, and there is clear spacing between them so the reader knows when one thought ends and another begins.

---

## 9. Line Breaks and Horizontal Rules

### 9.1 The `<br>` Tag (Line Break)

The `<br>` tag inserts a single line break. It is a **self-closing tag** (also called a void element), meaning it does not have a closing tag.

```html
<p>
    Roses are red,<br>
    Violets are blue,<br>
    HTML is awesome,<br>
    And so are you.
</p>
```

**Output:**

```
Roses are red,
Violets are blue,
HTML is awesome,
And so are you.
```

**When to use `<br>`:**
- Poetry or song lyrics
- Addresses
- Short lines that belong together but need to be on separate lines

**When NOT to use `<br>`:**
- To create spacing between paragraphs (use separate `<p>` tags instead).
- To push content down the page (use CSS margin/padding instead).

### 9.2 The `<hr>` Tag (Horizontal Rule)

The `<hr>` tag creates a horizontal line across the page. It is used to separate sections of content visually. Like `<br>`, it is a self-closing tag.

```html
<h2>Section 1: Introduction</h2>
<p>This is the introduction to the topic.</p>

<hr>

<h2>Section 2: Main Content</h2>
<p>This is the main content area.</p>
```

**Output:**

```
  Section 1: Introduction
  This is the introduction to the topic.
  ________________________________________

  Section 2: Main Content
  This is the main content area.
```

**When to use `<hr>`:**
- To visually separate distinct sections of content.
- In articles, between the main content and the author bio.
- Between topics on a single page.

### Self-Closing Tags

Both `<br>` and `<hr>` are self-closing. They do not wrap around content, so they have no closing tag.

```
  Regular Tag:       <p>Content goes here</p>
                     ^^^                 ^^^^
                   Opening             Closing

  Self-Closing Tag:  <br>    or    <hr>
                     ^^^^         ^^^^
                   No closing tag needed
```

> **Note:** You may also see these written as `<br />` and `<hr />` with a trailing slash. Both forms are valid in HTML5, but the simpler `<br>` and `<hr>` are preferred.

---

## 10. Text Formatting Tags

HTML provides several tags to format text. These tags change how text appears in the browser.

### Complete Formatting Tags Reference

| Tag        | Purpose                    | Example Code                         | Visual Result           |
|------------|----------------------------|--------------------------------------|-------------------------|
| `<b>`      | Bold text                  | `<b>Bold</b>`                        | **Bold**                |
| `<strong>`  | Important text (bold)      | `<strong>Important</strong>`         | **Important**           |
| `<i>`      | Italic text                | `<i>Italic</i>`                      | *Italic*                |
| `<em>`     | Emphasized text (italic)   | `<em>Emphasized</em>`               | *Emphasized*            |
| `<u>`      | Underlined text            | `<u>Underlined</u>`                  | Underlined              |
| `<mark>`   | Highlighted/marked text    | `<mark>Highlighted</mark>`          | Highlighted (yellow bg) |
| `<del>`    | Deleted/strikethrough text | `<del>Deleted</del>`                 | ~~Deleted~~             |
| `<sub>`    | Subscript text             | `H<sub>2</sub>O`                     | H2O (2 is lowered)      |
| `<sup>`    | Superscript text           | `x<sup>2</sup>`                      | x2 (2 is raised)        |
| `<small>`  | Smaller text               | `<small>Fine print</small>`         | Fine print (smaller)    |

### Practical Examples

```html
<!-- Bold and Strong -->
<p>The concert is on <b>Saturday</b> at <b>7 PM</b>.</p>
<p><strong>Warning:</strong> Do not touch the hot surface.</p>

<!-- Italic and Emphasis -->
<p>She was reading <i>Harry Potter</i> on the train.</p>
<p>You <em>must</em> submit the form before midnight.</p>

<!-- Underline -->
<p>Please read the <u>terms and conditions</u> carefully.</p>

<!-- Mark (Highlight) -->
<p>The answer to question 5 is <mark>Photosynthesis</mark>.</p>

<!-- Delete (Strikethrough) -->
<p>The original price was <del>$50</del> and now it is $30.</p>

<!-- Subscript and Superscript -->
<p>The chemical formula for water is H<sub>2</sub>O.</p>
<p>The area of a circle is pi times r<sup>2</sup>.</p>
<p>Einstein's equation: E = mc<sup>2</sup></p>

<!-- Small -->
<p><small>Copyright 2024. All rights reserved.</small></p>
```

### Nesting Formatting Tags

You can combine multiple formatting tags by nesting them:

```html
<p>This text is <b><i>bold and italic</i></b>.</p>
<p>This is <strong><em>strongly emphasized</em></strong>.</p>
<p>This is <b><u>bold and underlined</u></b>.</p>
```

> **Rule:** Always close tags in the reverse order that you opened them. If you open `<b>` then `<i>`, close `</i>` first, then `</b>`.

---

## 11. Difference Between Visual and Semantic Tags

This is one of the most important concepts in modern HTML. Some tags look the same in the browser but carry very different meanings.

### `<b>` vs `<strong>`

| Feature         | `<b>`                                  | `<strong>`                                 |
|-----------------|----------------------------------------|--------------------------------------------|
| Visual Result   | Bold text                              | Bold text                                  |
| Meaning         | None. Purely visual.                   | This text is **important**.                |
| Screen Readers  | Read normally.                         | Read with emphasis or strong tone.         |
| SEO Impact      | None.                                  | Search engines give it weight.             |
| When to Use     | When you want bold for style only.     | When the text is genuinely important.      |

### `<i>` vs `<em>`

| Feature         | `<i>`                                  | `<em>`                                     |
|-----------------|----------------------------------------|--------------------------------------------|
| Visual Result   | Italic text                            | Italic text                                |
| Meaning         | None. Purely visual.                   | This text is **emphasized**.               |
| Screen Readers  | Read normally.                         | Read with verbal emphasis.                 |
| SEO Impact      | None.                                  | Signals emphasis to search engines.        |
| When to Use     | Book titles, foreign words, terms.     | When you want to stress a word or phrase.  |

### Why Does This Matter?

```
  +------------------------------------------------------------+
  |                                                            |
  |   VISUAL TAGS             SEMANTIC TAGS                    |
  |   (how it LOOKS)          (what it MEANS)                  |
  |                                                            |
  |   <b>  = "Make it bold"   <strong> = "This is important"   |
  |   <i>  = "Make it italic" <em>     = "Stress this word"    |
  |                                                            |
  |   Both produce the same visual result, but semantic        |
  |   tags carry MEANING that helps:                           |
  |                                                            |
  |     1. Screen readers (accessibility for blind users)      |
  |     2. Search engines (SEO ranking)                        |
  |     3. Other developers (understanding your intent)        |
  |                                                            |
  +------------------------------------------------------------+
```

### Real-Life Analogy

Imagine two signs at a crosswalk:

- A sign that is simply painted in red: `<b>` -- it looks attention-grabbing, but there is no inherent "warning" associated with it.
- A sign that is an official STOP sign: `<strong>` -- it looks the same (red and bold), but it carries legal authority and meaning.

Both look similar, but one has meaning behind it. Always prefer semantic tags when the meaning applies.

### Best Practices

```
  PREFER THIS                    OVER THIS
  ============                   ===========

  <strong>Warning!</strong>      <b>Warning!</b>
  <em>must</em>                  <i>must</i>

  USE VISUAL TAGS FOR:
  <i>Hamlet</i>                  (book title -- no emphasis intended)
  <b>Keyword</b>                 (visual styling only -- no importance)
```

---

## 12. HTML Comments

Comments are notes in your code that the browser completely ignores. They are invisible to users viewing the web page but visible to anyone reading the source code.

### Syntax

```html
<!-- This is an HTML comment -->
```

Everything between `<!--` and `-->` is treated as a comment.

### Examples

```html
<!-- This is the navigation bar -->
<h1>My Website</h1>

<!-- TODO: Add a logo here later -->

<p>Welcome to my site.</p>

<!--
    This is a multi-line comment.
    You can write as many lines as you want.
    The browser will ignore all of this.
-->

<p>This paragraph is visible.</p>
<!-- <p>This paragraph is hidden because it is inside a comment.</p> -->
<p>This paragraph is also visible.</p>
```

### When to Use Comments

| Use Case                         | Example                                              |
|----------------------------------|------------------------------------------------------|
| Explain complex code             | `<!-- Calculate total with tax -->`                  |
| Leave notes for yourself/team    | `<!-- TODO: Replace placeholder image -->`           |
| Temporarily disable code         | `<!-- <p>Hide this for now</p> -->`                  |
| Mark sections of the page        | `<!-- ===== HEADER SECTION ===== -->`                |
| Document why a decision was made | `<!-- Using table here for email compatibility -->`  |

### VS Code Shortcut

In VS Code, you can quickly comment or uncomment a line or selected block:

- **Windows/Linux:** `Ctrl + /`
- **Mac:** `Cmd + /`

> **Warning:** Never put sensitive information (passwords, API keys, personal data) in HTML comments. Anyone can view your page source by pressing **Ctrl + U** in the browser. Comments are hidden from the rendered page, but they are fully visible in the source code.

---

## 13. HTML Entities

HTML entities are special codes used to display reserved characters or symbols that cannot be typed directly in HTML.

### Why Do We Need Entities?

Some characters have special meaning in HTML. For example, `<` and `>` are used for tags. If you try to write `5 < 10` directly in HTML, the browser might interpret `< 10` as the beginning of an incomplete tag and break your page.

```
  Problem:
  <p>5 < 10 and 20 > 15</p>     <-- Browser gets confused!

  Solution:
  <p>5 &lt; 10 and 20 &gt; 15</p>  <-- Works perfectly!
```

### Common HTML Entities

| Character | Entity Name | Entity Number | Description                    |
|-----------|-------------|---------------|--------------------------------|
| `&`       | `&amp;`     | `&#38;`       | Ampersand                      |
| `<`       | `&lt;`      | `&#60;`       | Less than sign                 |
| `>`       | `&gt;`      | `&#62;`       | Greater than sign              |
|           | `&nbsp;`    | `&#160;`      | Non-breaking space             |
| `"`       | `&quot;`    | `&#34;`       | Quotation mark                 |
| `'`       | `&apos;`    | `&#39;`       | Apostrophe                     |
| `(c)`     | `&copy;`    | `&#169;`      | Copyright symbol               |
| `(R)`     | `&reg;`     | `&#174;`      | Registered trademark           |
| `TM`      | `&trade;`   | `&#8482;`     | Trademark symbol               |

### Practical Examples

```html
<!-- Displaying HTML code as text -->
<p>The paragraph tag is written as &lt;p&gt;.</p>

<!-- Copyright notice -->
<p>&copy; 2024 My Company. All rights reserved.</p>

<!-- Using non-breaking spaces for extra spacing -->
<p>Price: &nbsp;&nbsp;&nbsp; $29.99</p>

<!-- Showing an ampersand -->
<p>Tom &amp; Jerry</p>

<!-- Combining entities -->
<p>&lt;strong&gt; makes text bold &lt;/strong&gt;</p>
```

### Non-Breaking Space (`&nbsp;`) Explained

A normal space allows the browser to break a line at that point. A non-breaking space (`&nbsp;`) prevents the browser from breaking the line between two words.

```
  Normal spaces:               Non-breaking spaces:
  "100 km" might wrap as:      "100&nbsp;km" stays together:

  ...text text text 100        ...text text text
  km more text...              100 km more text...

  (100 and km got separated)   (100 km stays on the same line)
```

**Common uses of `&nbsp;`:**
- Keeping numbers and units together: `100&nbsp;km`, `5&nbsp;PM`
- Adding multiple spaces (since browsers collapse regular spaces)
- Preventing awkward line breaks

### When to Use Entities vs. Direct Characters

```
  MUST use entities for:
  +---------------------------+
  |  <  >  &  "  (in attrs)  |
  |  These have special       |
  |  meaning in HTML          |
  +---------------------------+

  OPTIONAL (but good practice) for:
  +---------------------------+
  |  (c) (R) TM  special     |
  |  symbols, currency signs  |
  |  and non-keyboard chars   |
  +---------------------------+
```

---

## 14. Summary and Key Takeaways

### What We Learned This Week

```
  +---------------------------------------------------------------+
  |                  WEEK 1 AT A GLANCE                           |
  +---------------------------------------------------------------+
  |                                                               |
  |  1. HTML = Structure of a web page (the skeleton)             |
  |  2. Created by Tim Berners-Lee in 1991 at CERN               |
  |  3. We use HTML5 today (a living standard)                    |
  |  4. Browsers parse HTML and render it visually                |
  |  5. VS Code + Live Server + Chrome = our dev environment      |
  |  6. Every HTML page needs: DOCTYPE, html, head, body          |
  |  7. Headings (h1-h6) provide document structure               |
  |  8. Paragraphs (<p>) hold blocks of text                      |
  |  9. <br> = line break, <hr> = horizontal rule                 |
  | 10. Formatting: <b>, <i>, <u>, <mark>, <del>, <sub>, <sup>   |
  | 11. <strong> and <em> are SEMANTIC (meaningful) versions      |
  |     of <b> and <i>                                            |
  | 12. Comments <!-- --> are invisible notes in your code        |
  | 13. Entities like &lt; &gt; &amp; display special characters  |
  |                                                               |
  +---------------------------------------------------------------+
```

### Quick Reference Cheat Sheet

```
  DOCUMENT STRUCTURE
  ==================
  <!DOCTYPE html>        Declare HTML5
  <html>                 Root element
  <head>                 Metadata container
  <title>                Browser tab title
  <body>                 Visible content

  HEADINGS
  ========
  <h1> to <h6>           Heading levels (1 = largest)

  TEXT
  ====
  <p>                    Paragraph
  <br>                   Line break (self-closing)
  <hr>                   Horizontal rule (self-closing)

  FORMATTING
  ==========
  <b>     / <strong>     Bold / Important
  <i>     / <em>         Italic / Emphasized
  <u>                    Underline
  <mark>                 Highlight
  <del>                  Strikethrough
  <sub>                  Subscript
  <sup>                  Superscript
  <small>                Smaller text

  COMMENTS
  ========
  <!-- comment -->       Ignored by browser

  ENTITIES
  ========
  &lt;    <              Less than
  &gt;    >              Greater than
  &amp;   &              Ampersand
  &nbsp;  (space)        Non-breaking space
  &copy;  (c)            Copyright
```

### Key Principles to Remember

1. **HTML is for structure, not for styling.** Use HTML to define *what* content is (heading, paragraph, emphasis). Use CSS (which you will learn later) to define *how* it looks.

2. **Semantic tags matter.** Prefer `<strong>` over `<b>` and `<em>` over `<i>` when meaning is intended. This improves accessibility and search engine optimization.

3. **Every page needs a proper structure.** Always include `<!DOCTYPE html>`, `<html>`, `<head>`, and `<body>`.

4. **Use only one `<h1>` per page** and maintain heading hierarchy (`<h1>` > `<h2>` > `<h3>` ...).

5. **Comments are for developers, not for users.** Use them generously to explain your code.

6. **Indentation matters** for readability. Indent child elements inside their parent elements. This is not required by the browser, but it makes your code much easier to read and maintain.

### Practice Exercises

1. **Exercise 1:** Create an HTML page about yourself. Include your name as an `<h1>`, a paragraph about your hobbies, and use at least three different formatting tags.

2. **Exercise 2:** Create a page that displays the chemical formulas for water (H2O), carbon dioxide (CO2), and glucose (C6H12O6) using subscript tags.

3. **Exercise 3:** Build an HTML page for a fictional restaurant menu. Use headings for categories (Appetizers, Main Course, Desserts), paragraphs for descriptions, horizontal rules between sections, and `<del>` for items that are out of stock.

4. **Exercise 4:** Create a page that demonstrates all HTML entities covered in this lesson. Show the entity code and the rendered character side by side.

5. **Exercise 5:** Write an HTML page that uses comments to plan a personal portfolio website. Use comments to mark where you would put a header, navigation, about section, projects section, and footer. Fill in basic content for each section.

---

> **Next Week:** Week 2 will cover HTML Links, Images, and Lists. You will learn how to connect pages together, add images, and organize information using ordered and unordered lists.

---

*End of Week 1 Notes*
