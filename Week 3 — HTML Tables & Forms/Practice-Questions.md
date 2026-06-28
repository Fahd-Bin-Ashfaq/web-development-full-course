# Week 3: HTML Tables & Forms — Practice Questions

---

## Section A: Multiple Choice Questions (MCQs)

**Instructions:** Choose the correct option for each question.

---

**Q1.** Which HTML element is used to define a row in a table?

- A) `<tc>`
- B) `<td>`
- C) `<tr>`
- D) `<th>`

<details>
<summary>Answer</summary>

**C) `<tr>`**

The `<tr>` element stands for "table row" and is used to define a horizontal row of cells within a table. Each `<tr>` element contains one or more `<td>` or `<th>` elements.
</details>

---

**Q2.** What does the `colspan` attribute do in a table cell?

- A) Merges cells vertically across multiple rows
- B) Merges cells horizontally across multiple columns
- C) Sets the width of a column
- D) Adds spacing between columns

<details>
<summary>Answer</summary>

**B) Merges cells horizontally across multiple columns**

The `colspan` attribute specifies the number of columns a table cell should span. For example, `<td colspan="3">` makes that cell stretch across three columns.
</details>

---

**Q3.** Which attribute is used to make a form field mandatory before submission?

- A) `mandatory`
- B) `validate`
- C) `required`
- D) `notempty`

<details>
<summary>Answer</summary>

**C) `required`**

The `required` attribute is a boolean attribute that, when present, specifies that an input field must be filled out before the form can be submitted. It is part of HTML5's built-in form validation.
</details>

---

**Q4.** What is the correct HTML element used to create a dropdown list?

- A) `<dropdown>`
- B) `<input type="dropdown">`
- C) `<list>`
- D) `<select>`

<details>
<summary>Answer</summary>

**D) `<select>`**

The `<select>` element is used to create a dropdown list. It contains `<option>` elements that define the available choices in the list.
</details>

---

**Q5.** Which input type is used for entering an email address with built-in validation?

- A) `<input type="text">`
- B) `<input type="mail">`
- C) `<input type="email">`
- D) `<input type="address">`

<details>
<summary>Answer</summary>

**C) `<input type="email">`**

The `type="email"` input provides built-in browser validation that checks whether the entered value follows a valid email format (e.g., contains an `@` symbol and a domain).
</details>

---

**Q6.** What is the purpose of the `<label>` element's `for` attribute?

- A) It sets the font style of the label text
- B) It associates the label with a specific form control using the control's `id`
- C) It determines which form the label belongs to
- D) It specifies the position of the label

<details>
<summary>Answer</summary>

**B) It associates the label with a specific form control using the control's `id`**

The `for` attribute links a `<label>` to a form element by matching the element's `id`. This improves accessibility and allows users to click the label to focus or activate the associated input.
</details>

---

**Q7.** Which HTTP method appends form data to the URL as query parameters?

- A) POST
- B) PUT
- C) GET
- D) PATCH

<details>
<summary>Answer</summary>

**C) GET**

The GET method appends form data to the URL in the form of key-value pairs (e.g., `?name=John&age=25`). This makes the data visible in the browser address bar and is suitable only for non-sensitive, small amounts of data.
</details>

---

**Q8.** What does the `<fieldset>` element do in a form?

- A) Creates a submit button
- B) Groups related form controls together with a visual border
- C) Validates form inputs
- D) Sets the form's encoding type

<details>
<summary>Answer</summary>

**B) Groups related form controls together with a visual border**

The `<fieldset>` element groups related form elements together and draws a box around them. It is typically used with the `<legend>` element, which provides a caption for the group.
</details>

---

**Q9.** Which element is used to define a header cell in a table?

- A) `<td>`
- B) `<head>`
- C) `<th>`
- D) `<header>`

<details>
<summary>Answer</summary>

**C) `<th>`**

The `<th>` element stands for "table header" and defines a header cell in a table. By default, text inside `<th>` is bold and centered, distinguishing it from regular data cells (`<td>`).
</details>

---

**Q10.** What is the purpose of the `name` attribute on form input elements?

- A) It provides a tooltip when hovering over the input
- B) It assigns a CSS class to the input
- C) It identifies the data sent to the server as a key-value pair
- D) It sets the default value of the input

<details>
<summary>Answer</summary>

**C) It identifies the data sent to the server as a key-value pair**

The `name` attribute is essential for form submission. When a form is submitted, the data is sent as key-value pairs where the `name` attribute serves as the key. Without a `name`, the input's value will not be included in the submitted data.
</details>

---

**Q11.** Which input type allows a user to select only one option from a group?

- A) `checkbox`
- B) `radio`
- C) `select`
- D) `toggle`

<details>
<summary>Answer</summary>

**B) `radio`**

Radio buttons (`<input type="radio">`) allow only one selection within a group. All radio buttons in the same group must share the same `name` attribute to ensure mutual exclusivity.
</details>

---

**Q12.** What does the `rowspan` attribute do?

- A) Sets the height of a row
- B) Adds spacing between rows
- C) Merges a cell vertically across multiple rows
- D) Defines the number of rows in a table

<details>
<summary>Answer</summary>

**C) Merges a cell vertically across multiple rows**

The `rowspan` attribute specifies the number of rows a table cell should span. For example, `<td rowspan="2">` makes that cell extend vertically across two rows.
</details>

---

**Q13.** Which element is used to create a multi-line text input field?

- A) `<input type="text">`
- B) `<input type="multiline">`
- C) `<textbox>`
- D) `<textarea>`

<details>
<summary>Answer</summary>

**D) `<textarea>`**

The `<textarea>` element creates a multi-line text input area. Unlike `<input type="text">`, which allows only a single line, `<textarea>` supports multiple lines and can be resized. Its dimensions are controlled by the `rows` and `cols` attributes.
</details>

---

**Q14.** Which attribute of the `<form>` element specifies where the form data should be sent?

- A) `method`
- B) `target`
- C) `action`
- D) `destination`

<details>
<summary>Answer</summary>

**C) `action`**

The `action` attribute specifies the URL where the form data will be sent for processing when the form is submitted. For example, `<form action="/submit-form">` sends the data to the `/submit-form` endpoint.
</details>

---

**Q15.** What is the purpose of the `<legend>` element?

- A) It creates a footnote for a table
- B) It provides a caption for a `<fieldset>` group
- C) It defines a label for an input field
- D) It adds a title to the entire form

<details>
<summary>Answer</summary>

**B) It provides a caption for a `<fieldset>` group**

The `<legend>` element defines a caption for the content of a `<fieldset>`. It appears as a title embedded in the top border of the fieldset box, helping users understand the purpose of the grouped form controls.
</details>

---

## Section B: Short Answer Questions

**Instructions:** Write concise answers to the following questions.

---

**Q1.** Explain the difference between the GET and POST methods in HTML forms. When would you use each one?

<details>
<summary>Answer</summary>

**GET Method:**
- Appends form data to the URL as query string parameters (e.g., `?name=John&age=25`).
- Data is visible in the browser's address bar and browser history.
- Has a character limit (approximately 2048 characters depending on the browser).
- Can be bookmarked and cached.
- Best used for non-sensitive data such as search queries and filters.

**POST Method:**
- Sends form data in the body of the HTTP request, not in the URL.
- Data is not visible in the address bar.
- Has no practical size limit for data.
- Cannot be bookmarked or cached.
- Best used for sensitive data (passwords, personal information), file uploads, and operations that modify data on the server.
</details>

---

**Q2.** Why is it important to use `<label>` elements in forms? What are the benefits?

<details>
<summary>Answer</summary>

Using `<label>` elements is important for several reasons:

1. **Accessibility:** Screen readers use labels to announce what each form field is for, making forms usable for visually impaired users.
2. **Usability:** When a label is properly associated with an input (using the `for` attribute matching the input's `id`), clicking the label text focuses or activates the corresponding input. This is especially helpful for small targets like checkboxes and radio buttons.
3. **Clarity:** Labels provide clear visual descriptions of what information each field expects.
4. **Standards Compliance:** Using labels is a best practice recommended by W3C and web accessibility guidelines (WCAG).
</details>

---

**Q3.** What is the difference between `colspan` and `rowspan`? Provide an example scenario for each.

<details>
<summary>Answer</summary>

- **`colspan`** merges a cell **horizontally** across multiple columns. For example, a table header that reads "Student Information" could span across three columns (Name, Age, Grade) using `<th colspan="3">Student Information</th>`.

- **`rowspan`** merges a cell **vertically** across multiple rows. For example, in a class schedule table, if a lecture runs from 9:00 AM to 11:00 AM (covering two time-slot rows), the cell could use `<td rowspan="2">Mathematics</td>` to span both rows.

In short, `colspan` works across columns (left to right) while `rowspan` works across rows (top to bottom).
</details>

---

**Q4.** When should you use HTML tables, and when should you avoid using them?

<details>
<summary>Answer</summary>

**Use tables when:**
- Displaying tabular data such as spreadsheets, schedules, comparison charts, financial reports, or statistical data.
- The data has a clear row-and-column relationship where headers apply to the data cells.

**Avoid tables when:**
- Creating page layouts. Using tables for layout purposes is outdated and causes accessibility issues. Use CSS (Flexbox, Grid) for layout instead.
- Displaying non-tabular content such as navigation menus, image galleries, or general page structure.
- The content does not have a logical row-column relationship.

The rule of thumb is: if the data would make sense in a spreadsheet, use a table. If you are just trying to position elements on a page, use CSS.
</details>

---

**Q5.** What does the `required` attribute do, and on which elements can it be used?

<details>
<summary>Answer</summary>

The `required` attribute is a boolean HTML5 attribute that specifies that a form field must be filled out before the form can be submitted. If a user attempts to submit the form with a required field left empty, the browser will display a validation message and prevent submission.

It can be used on the following form elements:
- `<input>` (most types including text, email, password, number, url, tel, date, checkbox, radio, file)
- `<select>` (requires the user to choose a non-placeholder option)
- `<textarea>` (requires the text area to contain content)

Example: `<input type="text" name="username" required>`
</details>

---

**Q6.** What is the difference between radio buttons and checkboxes? When would you use each?

<details>
<summary>Answer</summary>

**Radio Buttons (`<input type="radio">`):**
- Allow the user to select **only one option** from a group.
- All radio buttons in the same group must share the same `name` attribute.
- Once a selection is made, the user cannot deselect it without choosing another option.
- Use when only one choice is valid (e.g., selecting a gender, choosing a payment method).

**Checkboxes (`<input type="checkbox">`):**
- Allow the user to select **multiple options** independently.
- Each checkbox operates independently, even if they share the same `name`.
- Users can check and uncheck freely.
- Use when multiple selections are allowed (e.g., selecting hobbies, choosing toppings, agreeing to terms).
</details>

---

**Q7.** Why is the `name` attribute important for form elements? What happens if it is missing?

<details>
<summary>Answer</summary>

The `name` attribute is critical because it serves as the **key** in the key-value pair sent to the server when the form is submitted. For example, `<input type="text" name="email" value="test@example.com">` sends `email=test@example.com` to the server.

**If the `name` attribute is missing:**
- The input's value will **not be included** in the form submission data at all.
- The server will have no way to identify or receive that field's data.
- For radio buttons, the `name` attribute also groups them together. Without a shared `name`, radio buttons will not function as a mutually exclusive group.

In summary, a form input without a `name` attribute is essentially invisible to the server during form submission.
</details>

---

**Q8.** Explain the structure of an HTML table. What are the roles of `<table>`, `<thead>`, `<tbody>`, `<tfoot>`, `<tr>`, `<th>`, and `<td>`?

<details>
<summary>Answer</summary>

An HTML table is built using the following elements in a hierarchical structure:

- **`<table>`**: The container element that wraps the entire table.
- **`<thead>`**: Groups the header rows of the table. Typically contains column titles. Helps browsers and screen readers understand the table structure.
- **`<tbody>`**: Groups the main body content of the table. Contains the primary data rows.
- **`<tfoot>`**: Groups the footer rows of the table. Often used for summary information like totals or averages.
- **`<tr>`**: Defines a single row within `<thead>`, `<tbody>`, or `<tfoot>`.
- **`<th>`**: Defines a header cell. By default, its content is bold and centered. Used in `<thead>` for column headings or at the start of rows for row headings.
- **`<td>`**: Defines a standard data cell that holds regular content.

Using `<thead>`, `<tbody>`, and `<tfoot>` is not strictly required but is strongly recommended for accessibility, styling, and semantic clarity.
</details>

---

## Section C: True or False

**Instructions:** Determine whether each statement is True or False. Review the answer and explanation after attempting each question.

| # | Statement | Your Answer |
|---|-----------|-------------|
| 1 | The `<td>` element is used to define a table header cell. | |
| 2 | The POST method appends data to the URL as query parameters. | |
| 3 | The `<textarea>` element is a self-closing tag. | |
| 4 | Radio buttons with the same `name` attribute form a mutually exclusive group. | |
| 5 | The `action` attribute in a `<form>` specifies the HTTP method to use. | |
| 6 | The `colspan` attribute allows a cell to span multiple rows. | |
| 7 | The `<option>` element is used inside a `<select>` element to define choices. | |
| 8 | A form can be submitted without any `<input>` elements having a `name` attribute. | |
| 9 | The `<fieldset>` element is used to group related form controls together. | |
| 10 | The `placeholder` attribute submits a default value if the user leaves the field empty. | |

<details>
<summary>Answers and Explanations</summary>

| # | Statement | Answer | Explanation |
|---|-----------|--------|-------------|
| 1 | The `<td>` element is used to define a table header cell. | **False** | `<td>` stands for "table data" and defines a standard data cell. The `<th>` element is used for header cells. |
| 2 | The POST method appends data to the URL as query parameters. | **False** | The GET method appends data to the URL. The POST method sends data in the body of the HTTP request, keeping it hidden from the URL. |
| 3 | The `<textarea>` element is a self-closing tag. | **False** | `<textarea>` requires both an opening and closing tag: `<textarea></textarea>`. Any default text is placed between the tags. |
| 4 | Radio buttons with the same `name` attribute form a mutually exclusive group. | **True** | When radio buttons share the same `name`, the browser ensures only one can be selected at a time within that group. |
| 5 | The `action` attribute in a `<form>` specifies the HTTP method to use. | **False** | The `action` attribute specifies the URL where form data is sent. The `method` attribute specifies the HTTP method (GET or POST). |
| 6 | The `colspan` attribute allows a cell to span multiple rows. | **False** | `colspan` allows a cell to span multiple columns (horizontally). The `rowspan` attribute is used to span multiple rows (vertically). |
| 7 | The `<option>` element is used inside a `<select>` element to define choices. | **True** | Each `<option>` element within a `<select>` represents one item in the dropdown list. |
| 8 | A form can be submitted without any `<input>` elements having a `name` attribute. | **True** | The form will submit, but no input data will be sent to the server. The submission will essentially be empty because only inputs with a `name` attribute are included in the form data. |
| 9 | The `<fieldset>` element is used to group related form controls together. | **True** | `<fieldset>` groups related form elements and typically renders a border around them. It is used with `<legend>` to provide a descriptive caption. |
| 10 | The `placeholder` attribute submits a default value if the user leaves the field empty. | **False** | The `placeholder` attribute only provides a visual hint inside the field. It is not submitted as a value. If the field is left empty, no value is sent. To set a default submitted value, use the `value` attribute instead. |

</details>

---

## Section D: Code Correction

**Instructions:** Each code snippet below contains one or more errors. Identify the errors and write the corrected code.

---

**Q1.** Fix the following HTML table code:

```html
<table>
  <tr>
    <th>Name<th>
    <th>Age</th>
  </tr>
  <tr>
    <td>Ali</td>
    <td>22</td>
  <tr>
  <tr>
    <td>Sara</td>
    <td>25</td>
  </tr>
</table>
```

<details>
<summary>Corrected Code</summary>

**Errors found:**
1. The first `<th>` is closed with `<th>` instead of `</th>` (missing forward slash).
2. The second `<tr>` is closed with `<tr>` instead of `</tr>` (missing forward slash).

```html
<table>
  <tr>
    <th>Name</th>
    <th>Age</th>
  </tr>
  <tr>
    <td>Ali</td>
    <td>22</td>
  </tr>
  <tr>
    <td>Sara</td>
    <td>25</td>
  </tr>
</table>
```
</details>

---

**Q2.** Fix the following form code:

```html
<form action="/register" method="POST">
  <label>Username</label>
  <input type="text" id="user" required>

  <label for="pass">Password</label>
  <input type="password" name="password">

  <input type="submit" value="Register">
</form>
```

<details>
<summary>Corrected Code</summary>

**Errors found:**
1. The first `<label>` is missing the `for` attribute to associate it with the input.
2. The username `<input>` is missing the `name` attribute, so its value will not be sent to the server.
3. The `<label for="pass">` references `id="pass"`, but the password input does not have an `id` attribute.

```html
<form action="/register" method="POST">
  <label for="user">Username</label>
  <input type="text" id="user" name="username" required>

  <label for="pass">Password</label>
  <input type="password" id="pass" name="password">

  <input type="submit" value="Register">
</form>
```
</details>

---

**Q3.** Fix the following table with `colspan`:

```html
<table>
  <tr>
    <th colspan="3">Student Report</td>
  </tr>
  <tr>
    <th>Name</th>
    <th>Subject</th>
    <th>Grade</th>
  </tr>
  <tr>
    <td>Ahmed</td>
    <td>Math<td>
    <td>A</td>
  </tr>
</table>
```

<details>
<summary>Corrected Code</summary>

**Errors found:**
1. The `<th colspan="3">` is closed with `</td>` instead of `</th>` (mismatched tags).
2. The "Math" cell is closed with `<td>` instead of `</td>` (missing forward slash).

```html
<table>
  <tr>
    <th colspan="3">Student Report</th>
  </tr>
  <tr>
    <th>Name</th>
    <th>Subject</th>
    <th>Grade</th>
  </tr>
  <tr>
    <td>Ahmed</td>
    <td>Math</td>
    <td>A</td>
  </tr>
</table>
```
</details>

---

**Q4.** Fix the following form with radio buttons:

```html
<form>
  <p>Select your gender:</p>

  <input type="radio" name="gender" id="male">
  <label for="m">Male</label>

  <input type="radio" name="gen" id="female">
  <label for="female">Female</label>

  <input type="submit" value="Submit">
</form>
```

<details>
<summary>Corrected Code</summary>

**Errors found:**
1. The first `<label for="m">` does not match the input's `id="male"`. The `for` value must match the `id` exactly.
2. The second radio button has `name="gen"` instead of `name="gender"`. Both radio buttons must share the same `name` to form a mutually exclusive group.
3. Neither radio button has a `value` attribute, so no meaningful data will be sent to the server.

```html
<form>
  <p>Select your gender:</p>

  <input type="radio" name="gender" id="male" value="male">
  <label for="male">Male</label>

  <input type="radio" name="gender" id="female" value="female">
  <label for="female">Female</label>

  <input type="submit" value="Submit">
</form>
```
</details>

---

**Q5.** Fix the following form with a select dropdown and textarea:

```html
<form action="/feedback" method="GET">
  <label for="dept">Department:</label>
  <select id="dept">
    <option>-- Select --</option>
    <option value="hr">Human Resources<option>
    <option value="it">IT Department</option>
  </select>

  <label for="comments">Comments:</label>
  <textarea id="comments" name="comments" rows="5" cols="40" />

  <input type="submit" value="Send">
</form>
```

<details>
<summary>Corrected Code</summary>

**Errors found:**
1. The `<select>` element is missing the `name` attribute, so the selected value will not be sent to the server.
2. The "Human Resources" `<option>` is closed with `<option>` instead of `</option>` (missing forward slash).
3. The `<textarea>` is written as a self-closing tag (`/>`), but `<textarea>` requires a separate closing tag (`</textarea>`).
4. The first `<option>` should have an empty `value` and be `disabled`/`selected` so it acts as a proper placeholder.

```html
<form action="/feedback" method="GET">
  <label for="dept">Department:</label>
  <select id="dept" name="department">
    <option value="" disabled selected>-- Select --</option>
    <option value="hr">Human Resources</option>
    <option value="it">IT Department</option>
  </select>

  <label for="comments">Comments:</label>
  <textarea id="comments" name="comments" rows="5" cols="40"></textarea>

  <input type="submit" value="Send">
</form>
```
</details>

---

## Section E: Coding Exercises

**Instructions:** Write complete, valid HTML code for each task below. Test your code in a browser to verify it works correctly.

---

### Task 1: Class Schedule Table

Create an HTML table that displays a weekly class schedule with the following requirements:

- The table should have columns for: **Time**, **Monday**, **Tuesday**, **Wednesday**, **Thursday**, **Friday**.
- Include at least 4 time slots (e.g., 9:00 AM, 10:00 AM, 11:00 AM, 12:00 PM).
- Use `colspan` to show a "Lunch Break" row that spans all day columns.
- Use `rowspan` to show a "Lab Session" that runs across two consecutive time slots on one day.
- Add a table caption: "Weekly Class Schedule".
- Use `<thead>` and `<tbody>` for proper table structure.

<details>
<summary>Sample Solution</summary>

```html
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <title>Class Schedule</title>
</head>
<body>

<table border="1">
  <caption>Weekly Class Schedule</caption>
  <thead>
    <tr>
      <th>Time</th>
      <th>Monday</th>
      <th>Tuesday</th>
      <th>Wednesday</th>
      <th>Thursday</th>
      <th>Friday</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td>9:00 AM</td>
      <td>Mathematics</td>
      <td rowspan="2">Lab Session (Physics)</td>
      <td>English</td>
      <td>Mathematics</td>
      <td>History</td>
    </tr>
    <tr>
      <td>10:00 AM</td>
      <td>Science</td>
      <td>Computer Science</td>
      <td>English</td>
      <td>Science</td>
    </tr>
    <tr>
      <td>11:00 AM</td>
      <td>English</td>
      <td>Mathematics</td>
      <td>Science</td>
      <td>Computer Science</td>
      <td>Mathematics</td>
    </tr>
    <tr>
      <td>12:00 PM</td>
      <td colspan="5">Lunch Break</td>
    </tr>
    <tr>
      <td>1:00 PM</td>
      <td>History</td>
      <td>English</td>
      <td>Mathematics</td>
      <td>History</td>
      <td>Computer Science</td>
    </tr>
  </tbody>
</table>

</body>
</html>
```
</details>

---

### Task 2: Student Registration Form

Create a student registration form with the following fields and requirements:

- **Full Name** — text input, required
- **Email Address** — email input, required
- **Password** — password input, required, minimum 8 characters
- **Gender** — radio buttons (Male, Female, Other), required
- **Courses** — checkboxes (HTML, CSS, JavaScript, React)
- All fields must have proper `<label>` elements with `for` attributes.
- Use `<fieldset>` and `<legend>` to group the Gender and Courses sections.
- Include a submit and reset button.

<details>
<summary>Sample Solution</summary>

```html
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <title>Student Registration</title>
</head>
<body>

<h1>Student Registration Form</h1>

<form action="/register" method="POST">
  <div>
    <label for="fullname">Full Name:</label><br>
    <input type="text" id="fullname" name="fullname" required>
  </div>
  <br>

  <div>
    <label for="email">Email Address:</label><br>
    <input type="email" id="email" name="email" required>
  </div>
  <br>

  <div>
    <label for="password">Password:</label><br>
    <input type="password" id="password" name="password" required minlength="8">
  </div>
  <br>

  <fieldset>
    <legend>Gender</legend>
    <input type="radio" id="male" name="gender" value="male" required>
    <label for="male">Male</label>

    <input type="radio" id="female" name="gender" value="female">
    <label for="female">Female</label>

    <input type="radio" id="other" name="gender" value="other">
    <label for="other">Other</label>
  </fieldset>
  <br>

  <fieldset>
    <legend>Select Courses</legend>
    <input type="checkbox" id="html" name="courses" value="html">
    <label for="html">HTML</label>

    <input type="checkbox" id="css" name="courses" value="css">
    <label for="css">CSS</label>

    <input type="checkbox" id="javascript" name="courses" value="javascript">
    <label for="javascript">JavaScript</label>

    <input type="checkbox" id="react" name="courses" value="react">
    <label for="react">React</label>
  </fieldset>
  <br>

  <input type="submit" value="Register">
  <input type="reset" value="Clear Form">
</form>

</body>
</html>
```
</details>

---

### Task 3: Product Comparison Table

Create a product comparison table that compares **3 products** across **5 features**:

- Products: Laptop A, Laptop B, Laptop C (use as column headers).
- Features (row headers): Price, Processor, RAM, Storage, Battery Life.
- Add a title row that spans all columns using `colspan`: "Laptop Comparison Chart".
- Use `<thead>`, `<tbody>`, and `<tfoot>`.
- In the `<tfoot>`, add a row with a "Best Value" recommendation that spans all columns.

<details>
<summary>Sample Solution</summary>

```html
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <title>Product Comparison</title>
</head>
<body>

<table border="1">
  <thead>
    <tr>
      <th colspan="4">Laptop Comparison Chart</th>
    </tr>
    <tr>
      <th>Feature</th>
      <th>Laptop A</th>
      <th>Laptop B</th>
      <th>Laptop C</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>Price</th>
      <td>$799</td>
      <td>$1,099</td>
      <td>$1,499</td>
    </tr>
    <tr>
      <th>Processor</th>
      <td>Intel Core i5</td>
      <td>Intel Core i7</td>
      <td>Intel Core i9</td>
    </tr>
    <tr>
      <th>RAM</th>
      <td>8 GB</td>
      <td>16 GB</td>
      <td>32 GB</td>
    </tr>
    <tr>
      <th>Storage</th>
      <td>256 GB SSD</td>
      <td>512 GB SSD</td>
      <td>1 TB SSD</td>
    </tr>
    <tr>
      <th>Battery Life</th>
      <td>8 Hours</td>
      <td>10 Hours</td>
      <td>12 Hours</td>
    </tr>
  </tbody>
  <tfoot>
    <tr>
      <td colspan="4">
        <strong>Best Value:</strong> Laptop B offers the best balance of performance and price.
      </td>
    </tr>
  </tfoot>
</table>

</body>
</html>
```
</details>

---

### Task 4: Contact Form with Validation

Create a contact form with built-in HTML5 validation:

- **Name** — text input, required, minimum 3 characters
- **Email** — email input, required
- **Phone** — tel input, with a placeholder showing the expected format
- **Subject** — dropdown with options: General Inquiry, Technical Support, Billing, Feedback
- **Message** — textarea, required, minimum 20 characters
- **Preferred Contact Method** — radio buttons: Email, Phone
- Use the `pattern` attribute on the phone input to accept a valid format.
- The form should use the POST method.

<details>
<summary>Sample Solution</summary>

```html
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <title>Contact Us</title>
</head>
<body>

<h1>Contact Us</h1>

<form action="/contact" method="POST">
  <div>
    <label for="name">Name:</label><br>
    <input type="text" id="name" name="name" required minlength="3"
           placeholder="Enter your full name">
  </div>
  <br>

  <div>
    <label for="email">Email:</label><br>
    <input type="email" id="email" name="email" required
           placeholder="example@email.com">
  </div>
  <br>

  <div>
    <label for="phone">Phone:</label><br>
    <input type="tel" id="phone" name="phone"
           placeholder="03XX-XXXXXXX"
           pattern="[0-9]{4}-[0-9]{7}"
           title="Format: 03XX-XXXXXXX">
  </div>
  <br>

  <div>
    <label for="subject">Subject:</label><br>
    <select id="subject" name="subject" required>
      <option value="" disabled selected>-- Choose a subject --</option>
      <option value="general">General Inquiry</option>
      <option value="technical">Technical Support</option>
      <option value="billing">Billing</option>
      <option value="feedback">Feedback</option>
    </select>
  </div>
  <br>

  <fieldset>
    <legend>Preferred Contact Method</legend>
    <input type="radio" id="contact-email" name="contact_method" value="email">
    <label for="contact-email">Email</label>

    <input type="radio" id="contact-phone" name="contact_method" value="phone">
    <label for="contact-phone">Phone</label>
  </fieldset>
  <br>

  <div>
    <label for="message">Message:</label><br>
    <textarea id="message" name="message" rows="6" cols="50"
              required minlength="20"
              placeholder="Enter your message (minimum 20 characters)"></textarea>
  </div>
  <br>

  <input type="submit" value="Send Message">
  <input type="reset" value="Clear">
</form>

</body>
</html>
```
</details>

---

### Task 5: Complete Survey Form

Build a comprehensive survey form that uses **all the input types and form elements** covered in this week. The form should include:

- **Personal Information** (fieldset): Name (text), Email (email), Age (number), Date of Birth (date)
- **Preferences** (fieldset): Favorite Color (color picker), Satisfaction Level (range slider 1-10)
- **Experience** (fieldset): Experience Level (radio: Beginner/Intermediate/Advanced), Skills Known (checkboxes: HTML, CSS, JS, Python)
- **Additional Information** (fieldset): Country (select dropdown with at least 5 countries), Website URL (url input), Resume Upload (file input), Additional Comments (textarea)
- Use proper `<label>` elements, `<fieldset>`, and `<legend>` for all groups.
- Apply appropriate validation: required fields, min/max for number, minlength for text.
- Use the POST method with `enctype="multipart/form-data"` (needed for file upload).
- Include submit and reset buttons.

<details>
<summary>Sample Solution</summary>

```html
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <title>Complete Survey Form</title>
</head>
<body>

<h1>Developer Survey Form</h1>

<form action="/survey" method="POST" enctype="multipart/form-data">

  <!-- Personal Information -->
  <fieldset>
    <legend>Personal Information</legend>

    <label for="name">Full Name:</label><br>
    <input type="text" id="name" name="name" required minlength="2"
           placeholder="Your full name"><br><br>

    <label for="email">Email Address:</label><br>
    <input type="email" id="email" name="email" required
           placeholder="you@example.com"><br><br>

    <label for="age">Age:</label><br>
    <input type="number" id="age" name="age" min="16" max="100"
           required placeholder="Your age"><br><br>

    <label for="dob">Date of Birth:</label><br>
    <input type="date" id="dob" name="dob">
  </fieldset>
  <br>

  <!-- Preferences -->
  <fieldset>
    <legend>Preferences</legend>

    <label for="fav-color">Favorite Color:</label><br>
    <input type="color" id="fav-color" name="fav_color" value="#3498db"><br><br>

    <label for="satisfaction">Satisfaction Level (1-10):
      <span id="range-value">5</span>
    </label><br>
    <input type="range" id="satisfaction" name="satisfaction"
           min="1" max="10" value="5">
  </fieldset>
  <br>

  <!-- Experience -->
  <fieldset>
    <legend>Experience</legend>

    <p><strong>Experience Level:</strong></p>
    <input type="radio" id="beginner" name="experience" value="beginner" required>
    <label for="beginner">Beginner</label><br>

    <input type="radio" id="intermediate" name="experience" value="intermediate">
    <label for="intermediate">Intermediate</label><br>

    <input type="radio" id="advanced" name="experience" value="advanced">
    <label for="advanced">Advanced</label><br><br>

    <p><strong>Skills Known:</strong></p>
    <input type="checkbox" id="skill-html" name="skills" value="html">
    <label for="skill-html">HTML</label><br>

    <input type="checkbox" id="skill-css" name="skills" value="css">
    <label for="skill-css">CSS</label><br>

    <input type="checkbox" id="skill-js" name="skills" value="javascript">
    <label for="skill-js">JavaScript</label><br>

    <input type="checkbox" id="skill-python" name="skills" value="python">
    <label for="skill-python">Python</label>
  </fieldset>
  <br>

  <!-- Additional Information -->
  <fieldset>
    <legend>Additional Information</legend>

    <label for="country">Country:</label><br>
    <select id="country" name="country" required>
      <option value="" disabled selected>-- Select your country --</option>
      <option value="pk">Pakistan</option>
      <option value="us">United States</option>
      <option value="uk">United Kingdom</option>
      <option value="ca">Canada</option>
      <option value="ae">United Arab Emirates</option>
      <option value="sa">Saudi Arabia</option>
      <option value="in">India</option>
    </select><br><br>

    <label for="website">Website URL:</label><br>
    <input type="url" id="website" name="website"
           placeholder="https://yourwebsite.com"><br><br>

    <label for="resume">Upload Resume:</label><br>
    <input type="file" id="resume" name="resume"
           accept=".pdf,.doc,.docx"><br><br>

    <label for="comments">Additional Comments:</label><br>
    <textarea id="comments" name="comments" rows="5" cols="50"
              placeholder="Any additional comments..."></textarea>
  </fieldset>
  <br>

  <input type="submit" value="Submit Survey">
  <input type="reset" value="Reset Form">
</form>

</body>
</html>
```
</details>

---

## Summary

| Section | Type | Number of Questions |
|---------|------|---------------------|
| Section A | Multiple Choice Questions (MCQs) | 15 |
| Section B | Short Answer Questions | 8 |
| Section C | True or False | 10 |
| Section D | Code Correction | 5 |
| Section E | Coding Exercises | 5 |
| **Total** | | **43 Questions** |

---

*Week 3: HTML Tables & Forms — MERN Stack Full Course*
