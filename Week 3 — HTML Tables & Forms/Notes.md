# Week 3: HTML Tables & Forms

> **Prerequisites:** You should already know basic HTML tags (`<h1>`-`<h6>`, `<p>`, `<br>`, `<hr>`, `<strong>`, `<em>`), links (`<a>`), images (`<img>`), and lists (`<ul>`, `<ol>`, `<li>`, `<dl>`) from Weeks 1-2.

---

## Table of Contents

| #   | Topic                                         |
| --- | --------------------------------------------- |
| 1   | [HTML Tables](#1-html-tables)                 |
| 1.1 | [What Are Tables?](#11-what-are-tables)       |
| 1.2 | [Basic Table Structure](#12-basic-table-structure) |
| 1.3 | [Table Head, Body, and Footer](#13-table-head-body-and-footer) |
| 1.4 | [Caption for Table Titles](#14-caption-for-table-titles) |
| 1.5 | [Colspan and Rowspan](#15-colspan-and-rowspan) |
| 1.6 | [Table Accessibility](#16-table-accessibility) |
| 1.7 | [When NOT to Use Tables](#17-when-not-to-use-tables) |
| 2   | [HTML Forms](#2-html-forms)                   |
| 2.1 | [What Are Forms?](#21-what-are-forms)         |
| 2.2 | [Form Structure](#22-form-structure)          |
| 2.3 | [Text Inputs](#23-text-inputs)                |
| 2.4 | [Password Inputs](#24-password-inputs)        |
| 2.5 | [Email Inputs](#25-email-inputs)              |
| 2.6 | [Number Inputs](#26-number-inputs)            |
| 2.7 | [Date Inputs](#27-date-inputs)                |
| 2.8 | [Radio Buttons](#28-radio-buttons)            |
| 2.9 | [Checkboxes](#29-checkboxes)                  |
| 2.10 | [Dropdown Menus](#210-dropdown-menus)        |
| 2.11 | [Textarea](#211-textarea)                    |
| 2.12 | [Buttons](#212-buttons)                      |
| 2.13 | [Labels](#213-labels)                        |
| 2.14 | [Fieldset and Legend](#214-fieldset-and-legend) |
| 3   | [Form Validation (HTML5 Built-in)](#3-form-validation-html5-built-in) |
| 3.1 | [Required Attribute](#31-required-attribute)  |
| 3.2 | [Minlength and Maxlength](#32-minlength-and-maxlength) |
| 3.3 | [Min and Max for Numbers](#33-min-and-max-for-numbers) |
| 3.4 | [Pattern Attribute with Regex](#34-pattern-attribute-with-regex) |
| 3.5 | [Input Types That Auto-Validate](#35-input-types-that-auto-validate) |
| 4   | [Summary](#4-summary)                         |

---

## 1. HTML Tables

### 1.1 What Are Tables?

An HTML table displays data organized into rows and columns -- exactly like a spreadsheet. Tables exist to present **tabular data**: information that has a natural row-and-column relationship.

**Real-life examples of tabular data:**

| Where You See Tables        | Example                                      |
| --------------------------- | -------------------------------------------- |
| Spreadsheets (Excel/Sheets) | Financial reports, budgets, inventory lists   |
| School schedules            | Days of the week mapped to class periods      |
| Price lists                 | Product names paired with prices and features |
| Sports scoreboards          | Teams, points, wins, losses, draws            |
| Flight departure boards     | Flight number, destination, gate, time        |

```
Real-Life Analogy:

Think of a table like a shelf organizer in a store.

    +------------+------------+------------+
    |  Shampoo   |   Soap     |  Lotion    |    <-- Row 1 (Product Names)
    +------------+------------+------------+
    |   $5.99    |   $2.49    |   $8.99    |    <-- Row 2 (Prices)
    +------------+------------+------------+
    |   In Stock |  In Stock  |  Sold Out  |    <-- Row 3 (Availability)
    +------------+------------+------------+

    Each shelf  = a row
    Each slot   = a cell
    The labels  = column headers
```

---

### 1.2 Basic Table Structure

Every HTML table is built from four core elements:

| Element  | Purpose                          |
| -------- | -------------------------------- |
| `<table>` | Creates the table container     |
| `<tr>`    | Defines a table row             |
| `<td>`    | Defines a standard table cell (table data) |
| `<th>`    | Defines a header cell (bold and centered by default) |

```
How these elements nest together:

    <table>
        |
        +-- <tr>           (Row 1 - Header Row)
        |     +-- <th>     (Header Cell 1)
        |     +-- <th>     (Header Cell 2)
        |     +-- <th>     (Header Cell 3)
        |
        +-- <tr>           (Row 2 - Data Row)
        |     +-- <td>     (Data Cell 1)
        |     +-- <td>     (Data Cell 2)
        |     +-- <td>     (Data Cell 3)
        |
        +-- <tr>           (Row 3 - Data Row)
              +-- <td>     (Data Cell 1)
              +-- <td>     (Data Cell 2)
              +-- <td>     (Data Cell 3)
```

**Example -- Student Grade Sheet:**

```html
<table>
  <tr>
    <th>Student Name</th>
    <th>Subject</th>
    <th>Grade</th>
  </tr>
  <tr>
    <td>Ali Khan</td>
    <td>Mathematics</td>
    <td>A</td>
  </tr>
  <tr>
    <td>Sara Ahmed</td>
    <td>Science</td>
    <td>B+</td>
  </tr>
  <tr>
    <td>Omar Farooq</td>
    <td>English</td>
    <td>A-</td>
  </tr>
</table>
```

**This renders as:**

```
+---------------+-------------+-------+
| Student Name  | Subject     | Grade |
+---------------+-------------+-------+
| Ali Khan      | Mathematics | A     |
+---------------+-------------+-------+
| Sara Ahmed    | Science     | B+    |
+---------------+-------------+-------+
| Omar Farooq   | English     | A-    |
+---------------+-------------+-------+
```

> **Key difference between `<th>` and `<td>`:** The `<th>` element tells the browser (and screen readers) that this cell is a **header**. Browsers render `<th>` text as bold and centered by default, while `<td>` text is normal weight and left-aligned.

---

### 1.3 Table Head, Body, and Footer

For well-structured tables, HTML provides three sectioning elements that group rows by purpose:

| Element    | Purpose                                           |
| ---------- | ------------------------------------------------- |
| `<thead>`  | Groups the header row(s) at the top of the table  |
| `<tbody>`  | Groups the main data rows                         |
| `<tfoot>`  | Groups the footer row(s), such as totals or notes |

```
Table Section Layout:

    +=======================================+
    |              <thead>                  |   Header section
    |   +--------+--------+--------+       |   (column titles)
    |   |  <th>  |  <th>  |  <th>  |       |
    |   +--------+--------+--------+       |
    +=======================================+
    |              <tbody>                  |   Body section
    |   +--------+--------+--------+       |   (main data)
    |   |  <td>  |  <td>  |  <td>  |       |
    |   +--------+--------+--------+       |
    |   |  <td>  |  <td>  |  <td>  |       |
    |   +--------+--------+--------+       |
    |   |  <td>  |  <td>  |  <td>  |       |
    |   +--------+--------+--------+       |
    +=======================================+
    |              <tfoot>                  |   Footer section
    |   +--------+--------+--------+       |   (totals, summaries)
    |   |  <td>  |  <td>  |  <td>  |       |
    |   +--------+--------+--------+       |
    +=======================================+
```

**Example -- Monthly Expense Report:**

```html
<table>
  <thead>
    <tr>
      <th>Category</th>
      <th>Amount</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td>Rent</td>
      <td>$1,200</td>
    </tr>
    <tr>
      <td>Groceries</td>
      <td>$350</td>
    </tr>
    <tr>
      <td>Utilities</td>
      <td>$150</td>
    </tr>
  </tbody>
  <tfoot>
    <tr>
      <td>Total</td>
      <td>$1,700</td>
    </tr>
  </tfoot>
</table>
```

**Why use these sections?**

1. **Readability** -- Your code is clearer and easier to maintain.
2. **Styling** -- CSS can target `thead`, `tbody`, and `tfoot` independently (e.g., give headers a dark background, zebra-stripe body rows).
3. **Printing** -- When a long table spans multiple pages, the browser can repeat the `<thead>` at the top of each printed page.
4. **Accessibility** -- Screen readers use these sections to help users navigate large tables.

---

### 1.4 Caption for Table Titles

The `<caption>` element provides a visible title or description for a table. It must be the **first child** of the `<table>` element.

```html
<table>
  <caption>Q1 2026 Sales Report</caption>
  <thead>
    <tr>
      <th>Month</th>
      <th>Revenue</th>
      <th>Units Sold</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td>January</td>
      <td>$45,000</td>
      <td>320</td>
    </tr>
    <tr>
      <td>February</td>
      <td>$52,000</td>
      <td>410</td>
    </tr>
    <tr>
      <td>March</td>
      <td>$48,500</td>
      <td>375</td>
    </tr>
  </tbody>
</table>
```

> **Why use `<caption>` instead of a separate `<h3>` above the table?** Because `<caption>` is semantically tied to the table. Screen readers announce it as part of the table, and search engines understand the relationship.

---

### 1.5 Colspan and Rowspan

Sometimes a cell needs to stretch across multiple columns or multiple rows. That is what `colspan` and `rowspan` do.

| Attribute  | What It Does                                |
| ---------- | ------------------------------------------- |
| `colspan`  | Makes a cell span across multiple **columns** |
| `rowspan`  | Makes a cell span across multiple **rows**    |

#### Colspan

```
Before colspan:                     After colspan="3":

+------+------+------+             +--------------------+
| Cell | Cell | Cell |             |     Merged Cell    |
+------+------+------+             +--------------------+
| Cell | Cell | Cell |             | Cell | Cell | Cell |
+------+------+------+             +------+------+------+

The top cell stretches across all 3 columns.
```

```html
<table>
  <tr>
    <th colspan="3">2026 Annual Budget</th>
  </tr>
  <tr>
    <th>Q1</th>
    <th>Q2</th>
    <th>Q3</th>
  </tr>
  <tr>
    <td>$10,000</td>
    <td>$12,000</td>
    <td>$11,500</td>
  </tr>
</table>
```

#### Rowspan

```
Before rowspan:                     After rowspan="3":

+----------+--------+              +----------+--------+
| Category | Item 1 |              |          | Item 1 |
+----------+--------+              |          +--------+
| Category | Item 2 |              | Category | Item 2 |
+----------+--------+              |          +--------+
| Category | Item 3 |              |          | Item 3 |
+----------+--------+              +----------+--------+

The left cell stretches across all 3 rows.
```

```html
<table>
  <tr>
    <td rowspan="3">Electronics</td>
    <td>Laptop</td>
    <td>$999</td>
  </tr>
  <tr>
    <td>Tablet</td>
    <td>$499</td>
  </tr>
  <tr>
    <td>Phone</td>
    <td>$699</td>
  </tr>
</table>
```

#### Combining Both -- A Real Schedule Example

```html
<table>
  <caption>Weekly Class Schedule</caption>
  <thead>
    <tr>
      <th>Time</th>
      <th>Monday</th>
      <th>Tuesday</th>
      <th>Wednesday</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td>9:00 AM</td>
      <td rowspan="2">Math (Double Period)</td>
      <td>English</td>
      <td>Science</td>
    </tr>
    <tr>
      <td>10:00 AM</td>
      <!-- No cell here: Math spans down from above -->
      <td>History</td>
      <td>Art</td>
    </tr>
    <tr>
      <td colspan="4">12:00 PM - Lunch Break</td>
    </tr>
  </tbody>
</table>
```

```
Rendered result:

+-----------+-----------------------+-----------+-----------+
|   Time    |       Monday          |  Tuesday  | Wednesday |
+-----------+-----------------------+-----------+-----------+
|  9:00 AM  |                       |  English  |  Science  |
+-----------+  Math (Double Period) +-----------+-----------+
| 10:00 AM  |                       |  History  |    Art    |
+-----------+-----------------------+-----------+-----------+
|              12:00 PM - Lunch Break                       |
+-----------------------------------------------------------+
```

> **Important:** When a cell uses `rowspan` or `colspan`, the cells it covers must be removed from those rows. If you forget to remove them, the table will break and columns will misalign.

---

### 1.6 Table Accessibility

People who use screen readers rely on properly marked-up tables to understand data relationships. The `scope` attribute on `<th>` elements tells the screen reader whether a header applies to a **row** or a **column**.

| Scope Value  | Meaning                                    |
| ------------ | ------------------------------------------ |
| `scope="col"`  | This header labels the entire column below it |
| `scope="row"`  | This header labels the entire row beside it   |

```html
<table>
  <thead>
    <tr>
      <th scope="col">Product</th>
      <th scope="col">Price</th>
      <th scope="col">Stock</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th scope="row">Widget A</th>
      <td>$9.99</td>
      <td>150</td>
    </tr>
    <tr>
      <th scope="row">Widget B</th>
      <td>$14.99</td>
      <td>85</td>
    </tr>
  </tbody>
</table>
```

```
How scope helps screen readers:

    When a blind user lands on the "$14.99" cell, the screen reader
    announces: "Price, Widget B, $14.99" -- because it knows:

         scope="col"                 scope="row"
             |                           |
             v                           v
         +----------+                +-----------+
         |  Price   | <-- column     | Widget B  | <-- row
         +----------+   header       +-----------+   header
                   \                 /
                    \               /
                     v             v
                   +----------+
                   |  $14.99  |  <-- the current cell
                   +----------+
```

**Other accessibility best practices for tables:**

- Always use `<caption>` so users know what the table is about before reading it.
- Use `<thead>`, `<tbody>`, and `<tfoot>` to provide structural context.
- Keep tables as simple as possible; avoid deeply nested `colspan`/`rowspan` combinations.

---

### 1.7 When NOT to Use Tables

**Never use tables for page layout.** In the early days of the web (1990s-2000s), developers used tables to create multi-column layouts, sidebars, and navigation bars. This is now considered a serious anti-pattern.

```
WRONG -- Using a table for layout:

    <table>
      <tr>
        <td>Navigation Menu</td>       <-- This is NOT tabular data!
        <td>Main Content Area</td>
        <td>Sidebar</td>
      </tr>
    </table>

RIGHT -- Using CSS for layout:

    <nav>Navigation Menu</nav>          <-- Semantic HTML
    <main>Main Content Area</main>      <-- plus CSS Flexbox or Grid
    <aside>Sidebar</aside>              <-- for positioning
```

**Why tables for layout are harmful:**

| Problem          | Explanation                                                    |
| ---------------- | -------------------------------------------------------------- |
| Accessibility    | Screen readers announce layout tables as data tables, confusing blind users |
| Responsiveness   | Tables do not adapt well to mobile screens                     |
| Maintainability  | Layout changes require restructuring deeply nested HTML        |
| Performance      | Browsers cannot render a table until the entire table is loaded |
| Semantics        | Search engines cannot understand the purpose of your content   |

**Rule of thumb:** If the data naturally belongs in rows and columns (like a spreadsheet), use a table. If you are positioning page elements, use CSS Flexbox or Grid.

---

## 2. HTML Forms

### 2.1 What Are Forms?

HTML forms are the primary way users **send data** to a web server. Every interactive website relies on forms for gathering user input.

**Real-life examples of forms on the web:**

| Website    | Form Used For                                  |
| ---------- | ---------------------------------------------- |
| Google     | The search bar is a form                       |
| Facebook   | Registration, login, posting status updates    |
| Amazon     | Search, checkout, shipping address, reviews    |
| Gmail      | Composing emails, setting filters              |
| Any bank   | Account login, fund transfers, bill payments   |

```
How Forms Work (The Big Picture):

    +-------------------+                    +-------------------+
    |                   |   User clicks      |                   |
    |   Browser         |   "Submit"         |   Web Server      |
    |                   | =================> |                   |
    |  +-----------+    |   Form data sent   |  Receives data    |
    |  | Name: Ali |    |   via HTTP         |  Processes it     |
    |  +-----------+    |   (GET or POST)    |  Stores in DB     |
    |  | Pass: *** |    |                    |  Sends response   |
    |  +-----------+    |                    |                   |
    |  [  Submit  ]     | <================= |  "Welcome, Ali!"  |
    |                   |   Response sent    |                   |
    +-------------------+   back to browser  +-------------------+
```

In the MERN stack, forms on the **React frontend** will send data to your **Express/Node.js backend**, which stores it in **MongoDB**. Understanding HTML forms is the foundation for all of that.

---

### 2.2 Form Structure

The `<form>` element wraps all the input fields and buttons. It has two critical attributes:

| Attribute | Purpose                                              |
| --------- | ---------------------------------------------------- |
| `action`  | The URL where the form data will be sent             |
| `method`  | The HTTP method used to send data (`GET` or `POST`)  |

```html
<form action="/submit-registration" method="POST">
  <!-- Form fields go here -->
</form>
```

#### GET vs POST

```
GET Method:
    Data is appended to the URL as query parameters.
    Visible in the browser address bar.

    User fills form:  Name = Ali, City = Lahore
    Browser sends:    https://example.com/search?name=Ali&city=Lahore
                                                 ^^^^^^^^^^^^^^^^^^^^^^^^^
                                                 Data visible in URL!

    Use GET for:
    - Search forms
    - Filters
    - Non-sensitive data
    - When you want bookmarkable results


POST Method:
    Data is sent inside the HTTP request body.
    NOT visible in the address bar.

    User fills form:  Name = Ali, Password = secret123
    Browser sends:    https://example.com/register
                      Body: { name: "Ali", password: "secret123" }
                             ^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^
                             Data hidden from URL!

    Use POST for:
    - Login forms
    - Registration forms
    - Any form with sensitive data (passwords, payment info)
    - File uploads
    - Creating or modifying data on the server
```

**Comparison Table:**

| Feature              | GET                          | POST                        |
| -------------------- | ---------------------------- | --------------------------- |
| Data visibility      | Visible in URL               | Hidden in request body      |
| Data length limit    | Limited (~2048 characters)   | No practical limit          |
| Bookmarkable         | Yes                          | No                          |
| Cacheable            | Yes                          | No                          |
| Security             | Less secure                  | More secure                 |
| Use case             | Searching, filtering         | Login, registration, payment|
| Browser back button  | Safe to re-submit            | Browser warns before re-submit |

---

### 2.3 Text Inputs

The most common form element. It creates a single-line text field.

```html
<input type="text" name="username" placeholder="Enter your name" value="">
```

| Attribute     | Purpose                                                  |
| ------------- | -------------------------------------------------------- |
| `type="text"` | Tells the browser to render a single-line text field     |
| `name`        | The key used when sending data (e.g., `username=Ali`)    |
| `placeholder` | Gray hint text shown when the field is empty             |
| `value`       | Pre-fills the field with a default value                 |

```
What the user sees:

    +------------------------------------------+
    |  Enter your name                         |   <-- placeholder (gray)
    +------------------------------------------+

    After typing:

    +------------------------------------------+
    |  Ali Khan                                |   <-- user's input
    +------------------------------------------+

What gets sent to the server:

    username=Ali+Khan
    ^^^^^^^      ^^^^^^^^
    name attr    value typed by user
```

> **The `name` attribute is essential.** Without it, the input's data will NOT be sent to the server when the form is submitted. Think of `name` as the label on the envelope -- without it, the post office does not know where to deliver.

---

### 2.4 Password Inputs

Masks the characters typed by the user so that people nearby cannot read the password.

```html
<input type="password" name="user_password" placeholder="Enter your password">
```

```
What the user sees while typing:

    +------------------------------------------+
    |  * * * * * * * *                         |   <-- characters are masked
    +------------------------------------------+

What actually gets sent:

    user_password=secret123
```

> **Important:** `type="password"` only hides the text visually. It does NOT encrypt the data. To actually secure passwords, you must use HTTPS (SSL/TLS) and hash passwords on the server side -- which you will learn when we get to Node.js and Express.

---

### 2.5 Email Inputs

Looks like a regular text field, but the browser validates that the input follows the email format.

```html
<input type="email" name="user_email" placeholder="you@example.com">
```

**Browser behavior:**

- On mobile devices, the keyboard shows the `@` symbol prominently for convenience.
- On form submission, the browser checks for a valid email pattern (must contain `@` and a domain).
- If invalid, the browser blocks submission and shows a built-in error message.

```
Valid:     ali@gmail.com       -->  Form submits successfully
Valid:     sara@company.co.uk  -->  Form submits successfully
Invalid:   ali@               -->  Browser shows: "Please include an '@' ..."
Invalid:   just-text           -->  Browser shows: "Please include an '@' ..."
```

---

### 2.6 Number Inputs

Restricts input to numeric values. The browser renders increment/decrement arrows (spinner controls).

```html
<input type="number" name="quantity" min="1" max="100" value="1">
```

| Attribute | Purpose                                  |
| --------- | ---------------------------------------- |
| `min`     | The lowest number allowed                |
| `max`     | The highest number allowed               |
| `step`    | The increment value (default is 1)       |
| `value`   | The default starting number              |

```
What the user sees:

    +---------------------+
    |  1           [^][v] |   <-- spinner arrows to increase/decrease
    +---------------------+

    min="1"   --> user cannot go below 1
    max="100" --> user cannot go above 100
```

**Example -- Product quantity selector on an e-commerce site:**

```html
<label for="qty">Quantity:</label>
<input type="number" id="qty" name="quantity" min="1" max="10" step="1" value="1">
```

---

### 2.7 Date Inputs

Renders a native date picker in the browser. No need for external JavaScript date-picker libraries for basic use cases.

```html
<input type="date" name="birthday" min="1950-01-01" max="2010-12-31">
```

```
What the user sees (varies by browser):

    +------------------------------+
    |  mm / dd / yyyy        [📅]  |   <-- calendar icon
    +------------------------------+

    Clicking opens a native calendar picker:

    +----------------------------+
    |  <  June 2026  >           |
    +----------------------------+
    | Su  Mo  Tu  We  Th  Fr  Sa |
    |      1   2   3   4   5   6 |
    |  7   8   9  10  11  12  13 |
    | 14  15  16  17  18  19  20 |
    | 21  22  23  24 [25] 26  27 |
    | 28  29  30                 |
    +----------------------------+
```

The value is always sent in `YYYY-MM-DD` format (e.g., `birthday=2000-05-15`), regardless of how the browser displays it to the user.

---

### 2.8 Radio Buttons

Radio buttons let the user select **exactly one option** from a group. All radio buttons in the same group must share the same `name` attribute.

```html
<p>Select your payment method:</p>

<input type="radio" name="payment" id="credit" value="credit_card">
<label for="credit">Credit Card</label>

<input type="radio" name="payment" id="debit" value="debit_card">
<label for="debit">Debit Card</label>

<input type="radio" name="payment" id="paypal" value="paypal">
<label for="paypal">PayPal</label>
```

```
What the user sees:

    Select your payment method:

    ( ) Credit Card        <-- empty circle
    (*) Debit Card         <-- filled circle (selected)
    ( ) PayPal             <-- empty circle

    Only ONE can be selected at a time.
    Selecting "PayPal" automatically deselects "Debit Card."

What gets sent:

    payment=debit_card
```

> **Why same `name`?** The `name` attribute creates the group. Radio buttons with different `name` values are independent and do not deselect each other. This is a common beginner mistake.

```
CORRECT -- same name, one group:

    <input type="radio" name="color" value="red">
    <input type="radio" name="color" value="blue">
    <input type="radio" name="color" value="green">
    --> Selecting "blue" deselects "red" and "green"

WRONG -- different names, three independent buttons:

    <input type="radio" name="color1" value="red">
    <input type="radio" name="color2" value="blue">
    <input type="radio" name="color3" value="green">
    --> All three can be selected simultaneously (defeats the purpose)
```

---

### 2.9 Checkboxes

Checkboxes let the user select **zero or more options** from a group. Unlike radio buttons, multiple checkboxes can be selected at the same time.

```html
<p>Select your hobbies:</p>

<input type="checkbox" name="hobbies" id="reading" value="reading">
<label for="reading">Reading</label>

<input type="checkbox" name="hobbies" id="gaming" value="gaming">
<label for="gaming">Gaming</label>

<input type="checkbox" name="hobbies" id="cooking" value="cooking">
<label for="cooking">Cooking</label>

<input type="checkbox" name="hobbies" id="sports" value="sports">
<label for="sports">Sports</label>
```

```
What the user sees:

    Select your hobbies:

    [x] Reading            <-- checked
    [ ] Gaming             <-- unchecked
    [x] Cooking            <-- checked
    [ ] Sports             <-- unchecked

    Multiple selections allowed.

What gets sent:

    hobbies=reading&hobbies=cooking
```

**Radio vs Checkbox -- Quick Comparison:**

| Feature             | Radio Buttons            | Checkboxes                |
| ------------------- | ------------------------ | ------------------------- |
| Shape               | Circle (o)               | Square [ ]                |
| Selection           | One only                 | Zero or more              |
| Use case            | Gender, payment method   | Hobbies, preferences      |
| Deselect behavior   | Selecting one deselects others | Each is independent  |

---

### 2.10 Dropdown Menus

Dropdown menus (select boxes) let the user pick from a list of options without taking up much screen space.

```html
<label for="country">Select your country:</label>
<select name="country" id="country">
  <option value="">-- Choose a country --</option>
  <option value="pk">Pakistan</option>
  <option value="in">India</option>
  <option value="us">United States</option>
  <option value="uk">United Kingdom</option>
  <option value="ae">UAE</option>
</select>
```

```
What the user sees:

    Select your country:
    +------------------------------+
    | -- Choose a country --    [v]|   <-- collapsed dropdown
    +------------------------------+

    After clicking:

    +------------------------------+
    | -- Choose a country --       |
    | Pakistan                     |
    | India                        |   <-- expanded list
    | United States                |
    | United Kingdom               |
    | UAE                          |
    +------------------------------+

What gets sent (if user picks Pakistan):

    country=pk
```

#### Grouping Options with `<optgroup>`

For long dropdowns, you can group related options under labeled headings:

```html
<label for="car">Choose a car:</label>
<select name="car" id="car">
  <optgroup label="Japanese">
    <option value="toyota">Toyota</option>
    <option value="honda">Honda</option>
    <option value="suzuki">Suzuki</option>
  </optgroup>
  <optgroup label="German">
    <option value="bmw">BMW</option>
    <option value="mercedes">Mercedes</option>
    <option value="audi">Audi</option>
  </optgroup>
  <optgroup label="American">
    <option value="ford">Ford</option>
    <option value="chevrolet">Chevrolet</option>
  </optgroup>
</select>
```

```
Rendered dropdown:

    +------------------------------+
    | Japanese                     |   <-- group label (not selectable)
    |   Toyota                     |
    |   Honda                      |
    |   Suzuki                     |
    | German                       |   <-- group label
    |   BMW                        |
    |   Mercedes                   |
    |   Audi                       |
    | American                     |   <-- group label
    |   Ford                       |
    |   Chevrolet                  |
    +------------------------------+
```

> **Note:** The `<optgroup>` labels are displayed but cannot be selected by the user. They serve only as visual separators.

---

### 2.11 Textarea

A `<textarea>` creates a multi-line text input area, suitable for longer content like comments, messages, or descriptions.

```html
<label for="message">Your Message:</label>
<textarea id="message" name="message" rows="5" cols="40" placeholder="Write your message here..."></textarea>
```

| Attribute | Purpose                                         |
| --------- | ----------------------------------------------- |
| `rows`    | The visible height (number of text lines)       |
| `cols`    | The visible width (number of characters)        |

```
What the user sees:

    Your Message:
    +------------------------------------------+
    |  Write your message here...              |
    |                                          |
    |                                          |
    |                                          |
    |                                          |
    +------------------------------------------+

    The user can type multiple lines and
    typically resize the box by dragging
    the bottom-right corner.
```

> **`<textarea>` vs `<input type="text">`:** Use `<input type="text">` for short, single-line values (names, email addresses). Use `<textarea>` for longer, multi-line content (comments, messages, descriptions).

> **Important:** Unlike `<input>`, the `<textarea>` element uses a closing tag. Any default text goes **between the tags**, not in a `value` attribute:
> ```html
> <textarea name="bio">Default text goes here</textarea>
> ```

---

### 2.12 Buttons

HTML provides multiple ways to create buttons in forms:

#### 1. The `<button>` Element (Recommended)

```html
<button type="submit">Register</button>
<button type="reset">Clear Form</button>
<button type="button">Click Me (No Submit)</button>
```

| Type Value         | Behavior                                             |
| ------------------ | ---------------------------------------------------- |
| `type="submit"`    | Submits the form (this is the default)               |
| `type="reset"`     | Resets all fields to their initial values             |
| `type="button"`    | Does nothing by default; used with JavaScript         |

#### 2. Input-Based Buttons

```html
<input type="submit" value="Submit Form">
<input type="reset" value="Reset Form">
```

**`<button>` vs `<input type="submit">`:**

| Feature            | `<button>`                     | `<input type="submit">`       |
| ------------------ | ------------------------------ | ----------------------------- |
| Can contain HTML   | Yes (images, icons, spans)     | No (text only via `value`)    |
| Flexibility        | High                           | Low                           |
| Recommended        | Yes                            | Legacy, still valid           |

```html
<!-- You can put HTML inside <button> -->
<button type="submit">
  <strong>Submit</strong> Your Application
</button>

<!-- You CANNOT put HTML inside <input> -->
<input type="submit" value="Submit Your Application">
```

---

### 2.13 Labels

The `<label>` element creates a clickable text label that is linked to a form control. This is essential for both usability and accessibility.

**Two ways to link a label to an input:**

#### Method 1: Using `for` and `id` (Recommended)

```html
<label for="email">Email Address:</label>
<input type="email" id="email" name="email">
```

The `for` attribute on `<label>` must match the `id` attribute on the corresponding `<input>`.

#### Method 2: Wrapping the input inside the label

```html
<label>
  Email Address:
  <input type="email" name="email">
</label>
```

```
Why labels matter:

    WITHOUT labels:                    WITH labels:
    +---+                              +----------------+
    |(o)| Male                         | (o) Male       |
    +---+                              +----------------+
    User must click the               User can click the
    tiny circle only.                 text "Male" too!

    This is especially important for:
    - People with motor disabilities (larger click target)
    - People using screen readers (the reader announces what each field is)
    - Mobile users (small screens, large fingers)
```

> **Accessibility requirement:** Every form input MUST have a label. A form without labels is like a paper form without printed instructions -- users (and especially screen readers) have no idea what information goes where.

---

### 2.14 Fieldset and Legend

The `<fieldset>` element groups related form controls together, and `<legend>` gives the group a visible title. The browser draws a box around the grouped fields.

```html
<form action="/register" method="POST">

  <fieldset>
    <legend>Personal Information</legend>
    <label for="fname">First Name:</label>
    <input type="text" id="fname" name="first_name"><br><br>
    <label for="lname">Last Name:</label>
    <input type="text" id="lname" name="last_name"><br><br>
    <label for="dob">Date of Birth:</label>
    <input type="date" id="dob" name="date_of_birth">
  </fieldset>

  <fieldset>
    <legend>Account Details</legend>
    <label for="user_email">Email:</label>
    <input type="email" id="user_email" name="email"><br><br>
    <label for="user_pass">Password:</label>
    <input type="password" id="user_pass" name="password"><br><br>
    <label for="user_pass2">Confirm Password:</label>
    <input type="password" id="user_pass2" name="confirm_password">
  </fieldset>

  <button type="submit">Create Account</button>

</form>
```

```
What the user sees:

    +-- Personal Information ----------------------+
    |                                              |
    |  First Name:     [___________________]       |
    |                                              |
    |  Last Name:      [___________________]       |
    |                                              |
    |  Date of Birth:  [__ / __ / ____]            |
    |                                              |
    +----------------------------------------------+

    +-- Account Details ---------------------------+
    |                                              |
    |  Email:             [___________________]    |
    |                                              |
    |  Password:          [___________________]    |
    |                                              |
    |  Confirm Password:  [___________________]    |
    |                                              |
    +----------------------------------------------+

    [ Create Account ]
```

> **When to use fieldset:** Use it when your form has distinct sections. For example, a checkout form might have "Shipping Address," "Billing Address," and "Payment Information" fieldsets. Screen readers announce the legend text when a user enters the group, providing useful context.

---

## 3. Form Validation (HTML5 Built-in)

Before HTML5, form validation required JavaScript. Now, the browser can validate many common rules automatically -- no scripts needed. This is called **client-side validation**.

```
Validation Flow:

    User fills form
         |
         v
    User clicks "Submit"
         |
         v
    +--------------------+
    | Browser checks     |     FAIL --> Browser blocks submission
    | HTML5 validation   | ---------> and shows error message
    | rules              |
    +--------------------+
         |
         | PASS
         v
    Form data sent to server
         |
         v
    +--------------------+
    | Server validates   |     Server-side validation is ALWAYS
    | again (Node.js)    |     needed too -- never trust the client!
    +--------------------+
```

> **Important:** HTML5 validation is a convenience for users, NOT a security measure. A skilled user can bypass browser validation easily (by editing HTML in DevTools). You must always validate data again on the server side.

---

### 3.1 Required Attribute

The simplest validation: the field must not be empty.

```html
<label for="name">Full Name (required):</label>
<input type="text" id="name" name="full_name" required>
```

If the user tries to submit the form with this field empty, the browser will block submission and display a message like:

```
    +------------------------------------------+
    |                                          |
    +------------------------------------------+
          ^
          |
    +---------------------------+
    | Please fill out this      |
    | field.                    |
    +---------------------------+
```

You can add `required` to any input type: text, email, password, select, textarea, checkboxes, and radio buttons.

```html
<!-- Required dropdown -->
<select name="country" required>
  <option value="">-- Select Country --</option>
  <option value="pk">Pakistan</option>
  <option value="us">United States</option>
</select>

<!-- Required textarea -->
<textarea name="comments" required></textarea>
```

> **Tip for dropdowns:** The first `<option>` must have an empty `value=""` for the `required` attribute to work. If every option has a non-empty value, the browser considers the field always "filled."

---

### 3.2 Minlength and Maxlength

Control the allowed length of text input.

```html
<!-- Username must be between 3 and 20 characters -->
<input type="text" name="username" minlength="3" maxlength="20" required>

<!-- Password must be at least 8 characters -->
<input type="password" name="password" minlength="8" required>

<!-- Bio limited to 500 characters -->
<textarea name="bio" maxlength="500"></textarea>
```

| Attribute    | Behavior                                                       |
| ------------ | -------------------------------------------------------------- |
| `minlength`  | Browser shows an error if the user types fewer characters than this |
| `maxlength`  | Browser prevents the user from typing more characters than this    |

```
Example with minlength="3":

    User types: "Al"
    User clicks Submit.

    +------------------------------------------+
    |  Al                                      |
    +------------------------------------------+
          ^
    +-----------------------------------+
    | Please lengthen this text to 3    |
    | characters or more (you are      |
    | currently using 2 characters).   |
    +-----------------------------------+
```

> **Note the difference:** `minlength` shows an error on submit (the user can still type fewer characters). `maxlength` hard-stops the user from typing beyond the limit -- the keyboard simply stops adding characters.

---

### 3.3 Min and Max for Numbers

For `<input type="number">`, `<input type="date">`, and similar numeric types, `min` and `max` constrain the allowed range.

```html
<!-- Age between 18 and 120 -->
<input type="number" name="age" min="18" max="120" required>

<!-- Appointment date must be in the future (example for June 2026) -->
<input type="date" name="appointment" min="2026-06-25">

<!-- Rating from 1 to 5 -->
<input type="number" name="rating" min="1" max="5" step="1">
```

```
Example with min="18" max="120":

    User types: 15
    User clicks Submit.

    +---------------------+
    |  15          [^][v] |
    +---------------------+
          ^
    +-----------------------------+
    | Value must be 18 or more.   |
    +-----------------------------+
```

---

### 3.4 Pattern Attribute with Regex

The `pattern` attribute lets you define a custom validation rule using a **regular expression** (regex). The browser checks the user's input against this pattern.

```html
<!-- Phone number: exactly 11 digits -->
<input type="text" name="phone" pattern="[0-9]{11}"
       title="Please enter an 11-digit phone number"
       placeholder="03001234567">

<!-- Username: letters and numbers only, 3-15 characters -->
<input type="text" name="username" pattern="[a-zA-Z0-9]{3,15}"
       title="3-15 characters, letters and numbers only">

<!-- Pakistani CNIC: format XXXXX-XXXXXXX-X -->
<input type="text" name="cnic" pattern="[0-9]{5}-[0-9]{7}-[0-9]{1}"
       title="Format: 12345-1234567-1"
       placeholder="12345-1234567-1">
```

**Common Regex Patterns:**

| Pattern              | Meaning                                | Example Match      |
| -------------------- | -------------------------------------- | ------------------ |
| `[0-9]{11}`          | Exactly 11 digits                      | `03001234567`      |
| `[a-zA-Z]+`          | One or more letters only               | `Hello`            |
| `[a-zA-Z0-9]{3,15}`  | 3-15 alphanumeric characters           | `user42`           |
| `[A-Z]{2}[0-9]{4}`   | 2 uppercase letters + 4 digits         | `PK1234`           |
| `.{8,}`              | At least 8 characters (any character)  | `anything`         |

> **The `title` attribute:** When you use `pattern`, always include a `title` attribute. The browser displays this text as part of the error message, explaining to the user what format is expected.

```
Example with pattern="[0-9]{11}":

    User types: 0300-123
    User clicks Submit.

    +------------------------------------------+
    |  0300-123                                |
    +------------------------------------------+
          ^
    +-------------------------------------------+
    | Please match the requested format.        |
    | Please enter an 11-digit phone number.    |
    +-------------------------------------------+
          ^
          |
          This comes from the title attribute!
```

---

### 3.5 Input Types That Auto-Validate

Several HTML5 input types include built-in validation without needing extra attributes:

| Input Type        | What It Auto-Validates                                    |
| ----------------- | --------------------------------------------------------- |
| `type="email"`    | Must contain `@` and a domain (e.g., `user@domain.com`)  |
| `type="url"`      | Must start with a protocol (e.g., `https://example.com`) |
| `type="number"`   | Must be a valid number; respects `min`, `max`, `step`     |
| `type="date"`     | Must be a valid date; respects `min` and `max`            |
| `type="tel"`      | No auto-validation (phone formats vary globally), but shows numeric keyboard on mobile |

**Example -- URL Input:**

```html
<label for="website">Your Website:</label>
<input type="url" id="website" name="website" placeholder="https://example.com">
```

```
Valid:     https://google.com      -->  Accepted
Valid:     http://my-site.co.uk    -->  Accepted
Invalid:   google.com              -->  Browser shows: "Please enter a URL."
Invalid:   just some text          -->  Browser shows: "Please enter a URL."
```

**Complete Validated Form Example:**

```html
<form action="/api/register" method="POST">
  <fieldset>
    <legend>Create Your Account</legend>

    <label for="reg_name">Full Name:</label><br>
    <input type="text" id="reg_name" name="full_name"
           required minlength="2" maxlength="50"
           placeholder="Ali Khan"><br><br>

    <label for="reg_email">Email:</label><br>
    <input type="email" id="reg_email" name="email"
           required placeholder="ali@example.com"><br><br>

    <label for="reg_phone">Phone:</label><br>
    <input type="tel" id="reg_phone" name="phone"
           pattern="[0-9]{11}" title="11-digit phone number"
           placeholder="03001234567"><br><br>

    <label for="reg_pass">Password:</label><br>
    <input type="password" id="reg_pass" name="password"
           required minlength="8"
           title="At least 8 characters"><br><br>

    <label for="reg_age">Age:</label><br>
    <input type="number" id="reg_age" name="age"
           min="18" max="120"><br><br>

    <label for="reg_website">Website (optional):</label><br>
    <input type="url" id="reg_website" name="website"
           placeholder="https://yoursite.com"><br><br>

    <button type="submit">Register</button>
    <button type="reset">Clear</button>
  </fieldset>
</form>
```

```
Validation Summary for the Above Form:

    +------------------+----------------------------------------------+
    | Field            | Rules Applied                                |
    +------------------+----------------------------------------------+
    | Full Name        | required, min 2 chars, max 50 chars          |
    | Email            | required, must be valid email format          |
    | Phone            | must match 11-digit pattern (if provided)    |
    | Password         | required, min 8 chars                        |
    | Age              | must be between 18 and 120 (if provided)     |
    | Website          | must be valid URL (if provided)              |
    +------------------+----------------------------------------------+

    "required" = must be filled to submit
    No "required" = optional, but validated if filled
```

---

## 4. Summary

### HTML Tables -- Key Points

| Concept              | What to Remember                                           |
| -------------------- | ---------------------------------------------------------- |
| `<table>`            | Container for tabular data                                 |
| `<tr>`               | Table row                                                  |
| `<th>`               | Header cell (bold, centered by default)                    |
| `<td>`               | Data cell                                                  |
| `<thead>/<tbody>/<tfoot>` | Structural sections for headers, body, and footers    |
| `<caption>`          | Title for the table, must be the first child of `<table>`  |
| `colspan`            | Merge cells horizontally across columns                    |
| `rowspan`            | Merge cells vertically across rows                         |
| `scope`              | Accessibility attribute for `<th>` (values: `col`, `row`)  |
| Layout rule          | NEVER use tables for page layout -- use CSS instead        |

### HTML Forms -- Key Points

| Concept              | What to Remember                                           |
| -------------------- | ---------------------------------------------------------- |
| `<form>`             | Container for form controls; needs `action` and `method`   |
| `GET` vs `POST`      | GET for searches (data in URL); POST for sensitive data    |
| `<input type="...">`  | Creates various input controls based on the type value    |
| `name` attribute     | MUST be present for data to be sent to the server          |
| `<label>`            | Links text to inputs for accessibility; use `for` + `id`   |
| `<select>/<option>`  | Dropdown menus; use `<optgroup>` for grouped options       |
| `<textarea>`         | Multi-line text input with `rows` and `cols`               |
| `<fieldset>/<legend>` | Groups related fields with a visible border and title     |
| Radio vs Checkbox    | Radio = one choice; Checkbox = multiple choices            |

### HTML5 Validation -- Key Points

| Attribute        | What It Does                                               |
| ---------------- | ---------------------------------------------------------- |
| `required`       | Field must not be empty                                    |
| `minlength`      | Minimum text length (error shown on submit)                |
| `maxlength`      | Maximum text length (hard limit while typing)              |
| `min` / `max`    | Minimum and maximum numeric or date values                 |
| `pattern`        | Custom regex validation (always add `title` for the error) |
| Auto-validating  | `email`, `url`, `number`, `date` types validate format automatically |

### What is Coming Next

```
Week 3 gave you:                What is ahead:

    Tables + Forms              Week 4 --> Semantic HTML & HTML5 Features
    (collecting data)           (structuring entire web pages properly)
         |
         |                      Later in the MERN stack:
         |
         +---- React -------->  React forms with useState, controlled components
         |
         +---- Express ------>  Server routes to receive form data via req.body
         |
         +---- MongoDB ------>  Storing submitted form data in the database
```

> **Practice is essential.** Build at least two complete forms this week: a registration form and a contact form. Use every input type covered in this lesson. Add validation rules. Open them in a browser and try submitting with invalid data to see the browser's built-in error messages in action.

---

*End of Week 3 Notes*
