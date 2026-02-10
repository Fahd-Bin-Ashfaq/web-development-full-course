# Fetch API – Complete Practical Guide (JavaScript)

This document explains **how, when, and why** to use the Fetch API in JavaScript. It covers:

* Response methods (`json`, `text`, `blob`, etc.)
* `fetch()` options (`method`, `headers`, `body`, etc.)
* Real-life daily examples
* Best practices and interview-ready explanations

---

## 1. What is Fetch API?

The **Fetch API** is a modern JavaScript interface used to make HTTP requests (GET, POST, PUT, DELETE) to servers.

It is **promise-based**, meaning it works naturally with:

* `.then()` (Promise chaining)
* `async / await`

```js
fetch(url)
  .then(response => response.json())
  .then(data => console.log(data));
```

---

## 2. Understanding the `response` Object

When `fetch()` is successful, it returns a **Response object**.

```js
const response = await fetch(url);
```

This object contains:

* Data reading methods
* Status information
* Headers

---

## 3. Response Data Reading Methods (When & Why to Use)

All methods below **return a Promise**.

### 3.1 `response.json()`

**When to use:**

* REST APIs
* Backend returns JSON

**Why:**

* Automatically converts JSON into JavaScript objects

**Example (Daily Life):**
Fetching user profile data from a server

```js
const data = await response.json();
```

---

### 3.2 `response.text()`

**When to use:**

* Plain text responses
* HTML or simple messages

**Daily Life Example:**
Reading a server message like: "Login successful"

```js
const text = await response.text();
```

---

### 3.3 `response.blob()`

**When to use:**

* Images
* PDFs
* Videos

**Daily Life Example:**
Downloading an invoice PDF or displaying a profile picture

```js
const file = await response.blob();
```

---

### 3.4 `response.arrayBuffer()`

**When to use:**

* Binary data
* Low-level file processing

**Daily Life Example:**
Audio or video streaming services

```js
const buffer = await response.arrayBuffer();
```

---

### 3.5 `response.formData()`

**When to use:**

* Form-based responses
* File uploads

**Daily Life Example:**
Uploading documents or images via a form

```js
const form = await response.formData();
```

---

## 4. Response Status & Validation Methods

### 4.1 `response.ok`

**Purpose:**

* Checks if request was successful (status 200–299)

```js
if (!response.ok) {
  throw new Error("Request failed");
}
```

---

### 4.2 `response.status`

**Purpose:**

* Returns HTTP status code

```js
console.log(response.status); // 200, 404, 500
```

---

### 4.3 `response.statusText`

**Purpose:**

* Human-readable status message

```js
console.log(response.statusText); // OK, Not Found
```

---

## 5. Fetch API Options (MOST IMPORTANT SECTION)

`fetch()` can take a **second argument (options object)**.

```js
fetch(url, options)
```

---

## 6. Fetch Options – Types, Usage & Daily Examples

### 6.1 `method`

**Purpose:**
Defines the HTTP request type

**Types:**

* GET (read data)
* POST (send data)
* PUT (update data)
* DELETE (remove data)

**Daily Life Example:**

* GET → View products
* POST → Place an order

```js
method: "POST"
```

---

### 6.2 `headers`

**Purpose:**

* Send metadata
* Define content type
* Authorization tokens

**Daily Life Example:**
Sending ID card before entering an office

```js
headers: {
  "Content-Type": "application/json",
  "Authorization": "Bearer TOKEN"
}
```

---

### 6.3 `body`

**Purpose:**

* Send data to server

**Used with:** POST / PUT

**Daily Life Example:**
Submitting a registration form

```js
body: JSON.stringify({
  name: "Ali",
  age: 22
})
```

---

### 6.4 `mode`

**Purpose:**

* Handle CORS requests

**Types:**

* cors (default)
* no-cors

**Daily Life Example:**
Accessing data from another domain

```js
mode: "cors"
```

---

### 6.5 `credentials`

**Purpose:**

* Send cookies or authentication info

**Daily Life Example:**
Staying logged in on a website

```js
credentials: "include"
```

---

### 6.6 `cache`

**Purpose:**

* Control caching behavior

**Daily Life Example:**
Using saved data vs fresh data

```js
cache: "no-cache"
```

---

## 7. Complete Professional Example

```js
async function fetchUsers() {
  try {
    const response = await fetch("https://jsonplaceholder.typicode.com/users", {
      method: "GET",
      headers: {
        "Content-Type": "application/json"
      }
    });

    if (!response.ok) {
      throw new Error(`HTTP Error: ${response.status}`);
    }

    const data = await response.json();
    console.log(data);

  } catch (error) {
    console.error("Fetch Error:", error.message);
  }
}

fetchUsers();
```

---

## 8. Important Notes (Interview Ready)

* `fetch()` **does NOT throw error on 404/500**
* Always check `response.ok`
* `response.json()` can be used **only once**
* `async/await` is just a cleaner syntax over promises

---

## 9. Quick Summary Table

| Feature         | Why Used            |
| --------------- | ------------------- |
| fetch()         | Make HTTP requests  |
| response.json() | Read JSON data      |
| response.ok     | Check success       |
| headers         | Metadata & auth     |
| body            | Send data           |
| method          | Define request type |

---

## 10. Final Thought

The Fetch API is a **core skill** for:

* Frontend developers
* Backend integration
* API consumption
* SOC & automation scripts

Mastering fetch means mastering **real-world JavaScript networking**.

---

**Author:** Fahad Ahmed
**Purpose:** Learning, Teaching & Professional Use
