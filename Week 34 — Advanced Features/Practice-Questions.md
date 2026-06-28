# Week 34 — Advanced Features: Practice Questions

**Total Questions: 20** (10 MCQs + 5 Short Answer + 5 Coding Exercises)

---

## Part 1: Multiple Choice Questions (MCQs)

**Q1. What is the primary purpose of Multer in an Express application?**

- A) To handle JSON request bodies
- B) To handle multipart/form-data for file uploads
- C) To serve static files to the client
- D) To compress response data before sending

<details>
<summary>Answer</summary>

**B) To handle multipart/form-data for file uploads**

Multer is a Node.js middleware specifically designed for handling `multipart/form-data`, which is the encoding type used when uploading files through HTML forms. It processes incoming file data from the request, stores it according to your configuration (memory or disk), and makes file information available on the `req.file` or `req.files` object. Without Multer (or a similar library), Express cannot natively parse file upload data from incoming requests.
</details>

---

**Q2. When uploading a file from a React frontend, which object is used to package the file data before sending it to the server?**

- A) JSON.stringify()
- B) URLSearchParams
- C) FormData
- D) FileReader

<details>
<summary>Answer</summary>

**C) FormData**

The `FormData` object is used to construct a set of key/value pairs representing form fields and their values, including file data. When uploading files, you create a new `FormData` instance, append the file to it using `formData.append('fieldName', file)`, and then send it via `fetch` or `axios`. It is important to note that when using `FormData`, you should not manually set the `Content-Type` header — the browser will automatically set it to `multipart/form-data` with the correct boundary string.
</details>

---

**Q3. In MongoDB, which operator is used to perform pattern-based text searches similar to SQL's LIKE clause?**

- A) $search
- B) $text
- C) $regex
- D) $match

<details>
<summary>Answer</summary>

**C) $regex**

The `$regex` operator in MongoDB provides regular expression capabilities for pattern matching against string fields. For example, `{ name: { $regex: "john", $options: "i" } }` would find all documents where the `name` field contains "john" (case-insensitive due to the `"i"` option). This is commonly used to implement search functionality in applications, allowing users to find documents that partially match their search query rather than requiring exact matches.
</details>

---

**Q4. In a paginated API, which two MongoDB methods work together to return a specific page of results?**

- A) find() and sort()
- B) skip() and limit()
- C) match() and group()
- D) filter() and slice()

<details>
<summary>Answer</summary>

**B) skip() and limit()**

The `skip()` method tells MongoDB how many documents to bypass before returning results, while `limit()` specifies the maximum number of documents to return. Together, they enable pagination. For example, to get page 3 with 10 items per page, you would use `skip(20).limit(10)` — skipping the first 20 documents (pages 1 and 2) and returning the next 10. The formula is: `skip((page - 1) * limit).limit(limit)`.
</details>

---

**Q5. What is the key difference between Socket.io and traditional HTTP requests?**

- A) Socket.io can only send text data, while HTTP can send any data type
- B) Socket.io maintains a persistent bidirectional connection, while HTTP follows a request-response pattern
- C) Socket.io is more secure than HTTP by default
- D) Socket.io requires a different server than Express

<details>
<summary>Answer</summary>

**B) Socket.io maintains a persistent bidirectional connection, while HTTP follows a request-response pattern**

Traditional HTTP follows a request-response model where the client sends a request, the server responds, and the connection effectively ends. The server cannot initiate communication with the client. Socket.io, built on top of WebSockets, establishes a persistent, full-duplex connection between the client and server. This means both sides can send data to each other at any time without the overhead of establishing new connections. This makes Socket.io ideal for real-time applications like chat, live notifications, and collaborative editing.
</details>

---

**Q6. In Nodemailer, what does the "transport" configuration define?**

- A) The format of the email body (HTML or plain text)
- B) The method and credentials used to send the email
- C) The list of recipients for the email
- D) The encryption algorithm for email content

<details>
<summary>Answer</summary>

**B) The method and credentials used to send the email**

The transport in Nodemailer defines how emails are actually sent. It specifies the email service provider (such as Gmail, SendGrid, or a custom SMTP server), along with authentication credentials (username/password or API keys), the host, port, and whether to use secure connections (TLS/SSL). For example, `nodemailer.createTransport({ service: 'gmail', auth: { user: 'your@gmail.com', pass: 'app-password' } })` creates a transport configured to send emails through Gmail's SMTP service.
</details>

---

**Q7. In Stripe's payment flow, what does a "Payment Intent" represent?**

- A) A completed and settled transaction
- B) A customer's saved payment method
- C) The intent to collect a payment, tracking the lifecycle of the charge
- D) A recurring subscription billing cycle

<details>
<summary>Answer</summary>

**C) The intent to collect a payment, tracking the lifecycle of the charge**

A Payment Intent is the core Stripe object that represents your intent to collect a payment from a customer. It tracks the entire payment lifecycle from creation through to completion or failure. When you create a Payment Intent on the server, Stripe returns a `client_secret` that the frontend uses to confirm the payment with the customer's card details. The Payment Intent handles complexities like authentication (3D Secure), retries, and different payment states (requires_payment_method, requires_confirmation, succeeded, etc.).
</details>

---

**Q8. What is the primary purpose of debouncing in a search input field?**

- A) To encrypt the search query before sending it
- B) To delay the API call until the user stops typing, reducing unnecessary requests
- C) To cache search results in the browser
- D) To validate the search query format

<details>
<summary>Answer</summary>

**B) To delay the API call until the user stops typing, reducing unnecessary requests**

Debouncing is a performance optimization technique that delays the execution of a function until a specified period of inactivity has passed. In the context of a search input, without debouncing, an API call would fire on every keystroke (e.g., typing "react" would trigger 5 separate API calls: "r", "re", "rea", "reac", "react"). With debouncing (typically 300-500ms), the API call only fires after the user stops typing for that duration, dramatically reducing server load and improving application performance.
</details>

---

**Q9. When configuring Multer's disk storage, which two functions must you define?**

- A) encode() and decode()
- B) destination() and filename()
- C) read() and write()
- D) upload() and download()

<details>
<summary>Answer</summary>

**B) destination() and filename()**

When using `multer.diskStorage()`, you must define two functions: `destination` determines the folder where uploaded files will be stored (e.g., `'./uploads'`), and `filename` determines the name the file will be saved as on disk. This is important because Multer does not add file extensions by default, so you typically construct a unique filename that includes the original extension. For example:

```js
const storage = multer.diskStorage({
  destination: (req, file, cb) => cb(null, './uploads'),
  filename: (req, file, cb) => cb(null, Date.now() + '-' + file.originalname)
});
```
</details>

---

**Q10. What type of connection does WebSocket establish between the client and server?**

- A) Half-duplex, where only one side can send at a time
- B) Simplex, where only the server can send data
- C) Full-duplex, where both sides can send data simultaneously
- D) Stateless, where each message is independent

<details>
<summary>Answer</summary>

**C) Full-duplex, where both sides can send data simultaneously**

WebSocket establishes a full-duplex communication channel over a single, long-lived TCP connection. Unlike HTTP, which is inherently half-duplex (the client sends a request, then waits for a response), WebSocket allows both the client and the server to send messages independently and simultaneously at any time. The connection begins with an HTTP handshake (the "upgrade" request), and once established, it remains open until either side explicitly closes it. This makes WebSocket ideal for real-time applications where low latency and bidirectional communication are essential.
</details>

---

## Part 2: Short Answer Questions

**Q1. Explain the complete file upload flow from a React frontend to storing the file reference in MongoDB.**

<details>
<summary>Answer</summary>

The complete file upload flow involves several steps across the frontend, backend, and database:

**1. Frontend (React):**
- The user selects a file through an `<input type="file" />` element.
- A change event handler captures the selected file from `e.target.files[0]`.
- A new `FormData` object is created, and the file is appended to it: `formData.append('image', file)`.
- The form data is sent to the server using `fetch` or `axios` with a POST request. The `Content-Type` header should not be set manually — the browser sets it automatically with the correct `multipart/form-data` boundary.

**2. Backend (Express + Multer):**
- The Express route uses Multer middleware to handle the incoming multipart data.
- Multer's storage configuration determines where the file is saved (disk or memory) and what it is named.
- After Multer processes the upload, file metadata is available on `req.file` (for single uploads) or `req.files` (for multiple uploads), including properties like `filename`, `path`, `mimetype`, and `size`.

**3. Database (MongoDB):**
- The file itself is not stored in MongoDB. Instead, the file path or URL (e.g., `/uploads/1698234567-photo.jpg`) is saved as a string field in the relevant document.
- A Mongoose model saves this reference: `await Product.create({ name: req.body.name, image: req.file.path })`.

**4. Serving the File:**
- Express serves the uploaded files using `express.static('uploads')`, making them accessible via a URL that the frontend can use in `<img>` tags or download links.
</details>

---

**Q2. Why is debouncing important for search functionality, and what problems does it solve?**

<details>
<summary>Answer</summary>

Debouncing is critically important for search functionality for several reasons:

**Performance Problem Without Debouncing:**
When a user types a search query like "javascript", without debouncing, the application would fire an API request on every single keystroke — resulting in 10 separate API calls ("j", "ja", "jav", "java", "javas", "javasc", "javascr", "javascri", "javascrip", "javascript"). Most of these intermediate requests are wasted because the user has not finished typing.

**Problems Debouncing Solves:**

1. **Reduces Server Load:** Instead of 10 API calls, debouncing (with a typical delay of 300-500ms) results in only 1 call after the user pauses typing. This dramatically reduces the number of requests hitting your server and database.

2. **Prevents Race Conditions:** Without debouncing, multiple API responses may return out of order. The response for "jav" might arrive after the response for "java", causing the UI to display stale results. Debouncing eliminates this issue by only sending one final request.

3. **Saves Bandwidth:** Fewer requests mean less data transferred over the network, which is especially important for users on slow or metered connections.

4. **Improves User Experience:** The UI remains responsive because it is not constantly re-rendering with intermediate results. Users see meaningful, complete search results rather than flickering partial matches.

5. **Reduces Database Strain:** Each search query typically involves a database operation (often using `$regex` or text search). Debouncing minimizes the number of database queries, which is crucial as your application scales.
</details>

---

**Q3. Explain how skip() and limit() work together in MongoDB to implement pagination.**

<details>
<summary>Answer</summary>

The `skip()` and `limit()` methods in MongoDB work together to divide a large result set into manageable pages:

**How They Work:**

- **`limit(n)`** restricts the number of documents returned to `n`. If a query matches 1000 documents but you call `.limit(10)`, only 10 documents are returned.

- **`skip(n)`** tells MongoDB to bypass the first `n` documents in the result set before starting to return documents. If you call `.skip(20)`, the first 20 matching documents are ignored.

**Pagination Formula:**

```
skip = (page - 1) * itemsPerPage
limit = itemsPerPage
```

**Example with 10 items per page:**

| Page | skip() | limit() | Documents Returned |
|------|--------|---------|--------------------|
| 1    | 0      | 10      | 1-10               |
| 2    | 10     | 10      | 11-20              |
| 3    | 20     | 10      | 21-30              |
| 4    | 30     | 10      | 31-40              |

**Server Implementation:**

```js
const page = parseInt(req.query.page) || 1;
const limit = parseInt(req.query.limit) || 10;
const skip = (page - 1) * limit;

const products = await Product.find().skip(skip).limit(limit);
const total = await Product.countDocuments();
const totalPages = Math.ceil(total / limit);
```

**Important Considerations:**
- Always use `countDocuments()` to determine the total number of documents so the frontend can render the correct number of page buttons.
- The `skip()` method can become slow on very large collections because MongoDB must iterate through all skipped documents. For extremely large datasets, cursor-based pagination (using `_id` comparisons) is more efficient.
- Always pair `skip()` and `limit()` with a consistent `sort()` order to ensure predictable results across pages.
</details>

---

**Q4. Compare HTTP requests with WebSocket connections. When would you choose one over the other?**

<details>
<summary>Answer</summary>

**HTTP Requests:**

- **Connection Model:** Follows a request-response pattern. The client opens a connection, sends a request, receives a response, and the connection is effectively complete.
- **Direction:** Unidirectional per interaction — the client always initiates, and the server can only respond.
- **Overhead:** Each request includes full HTTP headers, which adds overhead for frequent small messages.
- **Statefulness:** Stateless by default. Each request is independent and carries no memory of previous interactions (session/cookies add state externally).
- **Caching:** Responses can be cached by browsers and CDNs, improving performance for repeated requests.

**WebSocket Connections:**

- **Connection Model:** Establishes a persistent, long-lived connection after an initial HTTP handshake (upgrade request).
- **Direction:** Full-duplex — both the client and server can send messages independently at any time.
- **Overhead:** After the initial handshake, messages have minimal framing overhead (as little as 2-6 bytes per frame), making them efficient for frequent small messages.
- **Statefulness:** Inherently stateful. The connection remains open and both sides maintain awareness of each other.
- **Caching:** Messages cannot be cached since they are dynamic and real-time.

**When to Choose HTTP:**
- Standard CRUD operations (fetching user profiles, submitting forms, loading pages)
- Operations where caching is beneficial (loading product listings, static content)
- Infrequent data requests where the overhead of maintaining a connection is not justified
- RESTful API design where each operation maps cleanly to an HTTP method

**When to Choose WebSocket (Socket.io):**
- Real-time chat applications where messages must appear instantly
- Live notifications (new emails, social media alerts)
- Collaborative editing (Google Docs-style simultaneous editing)
- Live dashboards with frequently updating data (stock prices, analytics)
- Multiplayer games requiring low-latency communication
- Any scenario where the server needs to push data to clients without being asked
</details>

---

**Q5. What security considerations exist when implementing payment processing with Stripe?**

<details>
<summary>Answer</summary>

Payment processing involves handling sensitive financial data, and there are several critical security considerations:

**1. Never Handle Raw Card Data on Your Server:**
- Use Stripe Elements or Stripe.js on the frontend to collect card details. The card information is sent directly to Stripe's servers, never touching your backend. This significantly reduces your PCI DSS compliance burden.

**2. Server-Side Payment Intent Creation:**
- Always create Payment Intents on the server, never on the client. The amount and currency should be determined server-side to prevent users from tampering with the payment amount through browser developer tools.

**3. Protect Your Secret Key:**
- The Stripe secret key (`sk_live_...`) must only exist on the server, stored in environment variables (`.env` file). Never expose it in frontend code, commit it to version control, or log it. Only the publishable key (`pk_live_...`) is safe for the client.

**4. Webhook Verification:**
- Use Stripe webhooks to confirm payment completion rather than relying solely on client-side confirmation. Always verify webhook signatures using `stripe.webhooks.constructEvent()` to ensure the webhook genuinely came from Stripe and was not forged.

**5. Idempotency:**
- Use idempotency keys for critical operations to prevent duplicate charges if a request is retried due to network issues.

**6. HTTPS Enforcement:**
- All communication between your server and clients must use HTTPS. Stripe's API rejects requests from non-HTTPS origins in production.

**7. Input Validation:**
- Validate all payment-related inputs on the server (amounts, currency, product IDs). Never trust client-supplied price data — always look up prices from your database.

**8. Error Handling:**
- Handle payment errors gracefully without exposing internal details. Show user-friendly messages for declined cards or failed payments while logging detailed errors securely on the server.

**9. Test Mode Before Production:**
- Always develop and test using Stripe's test mode keys (`sk_test_...`) and test card numbers before switching to live keys. This prevents accidental real charges during development.
</details>

---

## Part 3: Coding Exercises

**Exercise 1: Create a File Upload Component in React with Image Preview**

Build a React component that allows users to select an image file, displays a preview of the selected image before uploading, and sends the file to the server.

**Starter Code:**

```jsx
import { useState } from 'react';

function FileUpload() {
  // TODO: Create state for selected file and preview URL

  // TODO: Handle file selection and generate preview

  // TODO: Handle file upload to server

  return (
    <div>
      <h2>Upload Image</h2>
      {/* TODO: File input */}
      {/* TODO: Image preview */}
      {/* TODO: Upload button */}
    </div>
  );
}

export default FileUpload;
```

<details>
<summary>Solution</summary>

```jsx
import { useState } from 'react';
import axios from 'axios';

function FileUpload() {
  const [file, setFile] = useState(null);
  const [preview, setPreview] = useState(null);
  const [uploadStatus, setUploadStatus] = useState('');

  const handleFileChange = (e) => {
    const selectedFile = e.target.files[0];

    if (selectedFile) {
      setFile(selectedFile);

      // Generate a preview URL using URL.createObjectURL
      const previewURL = URL.createObjectURL(selectedFile);
      setPreview(previewURL);
      setUploadStatus('');
    }
  };

  const handleUpload = async () => {
    if (!file) {
      setUploadStatus('Please select a file first.');
      return;
    }

    const formData = new FormData();
    formData.append('image', file);

    try {
      setUploadStatus('Uploading...');

      const response = await axios.post('http://localhost:5000/api/upload', formData);
      // Note: Do NOT set Content-Type header manually.
      // Axios (and fetch) will set it automatically with the correct boundary.

      setUploadStatus('Upload successful!');
      console.log('Server response:', response.data);
    } catch (error) {
      setUploadStatus('Upload failed. Please try again.');
      console.error('Upload error:', error);
    }
  };

  return (
    <div style={{ maxWidth: '400px', margin: '20px auto' }}>
      <h2>Upload Image</h2>

      <input
        type="file"
        accept="image/*"
        onChange={handleFileChange}
      />

      {preview && (
        <div style={{ margin: '15px 0' }}>
          <img
            src={preview}
            alt="Preview"
            style={{ maxWidth: '100%', maxHeight: '300px', borderRadius: '8px' }}
          />
        </div>
      )}

      <button onClick={handleUpload} disabled={!file}>
        Upload Image
      </button>

      {uploadStatus && <p>{uploadStatus}</p>}
    </div>
  );
}

export default FileUpload;
```

**Key Concepts:**

- **`URL.createObjectURL(file)`** creates a temporary local URL for the selected file, allowing you to display a preview without uploading it first.
- **`FormData`** is used to package the file for transmission. The field name (`'image'`) must match the field name expected by Multer on the server.
- **Do not set the `Content-Type` header** when sending `FormData` — the browser or Axios will automatically set it to `multipart/form-data` with the correct boundary.
- The `accept="image/*"` attribute on the file input restricts selection to image files only.
</details>

---

**Exercise 2: Build an Express Route with Multer for Image Upload**

Create an Express server with a POST route that accepts image uploads using Multer, validates the file type, and returns the file information.

**Starter Code:**

```js
const express = require('express');
const multer = require('multer');
const path = require('path');

const app = express();

// TODO: Configure Multer disk storage (destination and filename)

// TODO: Create a file filter to accept only images

// TODO: Initialize the Multer upload middleware

// TODO: Create POST route '/api/upload' that handles single file upload

// TODO: Serve uploaded files statically

app.listen(5000, () => console.log('Server running on port 5000'));
```

<details>
<summary>Solution</summary>

```js
const express = require('express');
const multer = require('multer');
const path = require('path');

const app = express();

// Configure Multer disk storage
const storage = multer.diskStorage({
  destination: (req, file, cb) => {
    cb(null, './uploads');
  },
  filename: (req, file, cb) => {
    // Create a unique filename: timestamp-originalname
    const uniqueName = Date.now() + '-' + file.originalname;
    cb(uniqueName);
    cb(null, uniqueName);
  }
});

// File filter to accept only image files
const fileFilter = (req, file, cb) => {
  const allowedTypes = ['image/jpeg', 'image/png', 'image/gif', 'image/webp'];

  if (allowedTypes.includes(file.mimetype)) {
    cb(null, true);   // Accept the file
  } else {
    cb(new Error('Only image files (JPEG, PNG, GIF, WEBP) are allowed.'), false);
  }
};

// Initialize Multer with storage, file filter, and size limit
const upload = multer({
  storage: storage,
  fileFilter: fileFilter,
  limits: {
    fileSize: 5 * 1024 * 1024  // 5 MB limit
  }
});

// POST route for single file upload
app.post('/api/upload', upload.single('image'), (req, res) => {
  if (!req.file) {
    return res.status(400).json({ message: 'No file uploaded.' });
  }

  res.status(200).json({
    message: 'File uploaded successfully!',
    file: {
      filename: req.file.filename,
      path: req.file.path,
      size: req.file.size,
      mimetype: req.file.mimetype
    }
  });
});

// Error handling middleware for Multer errors
app.use((err, req, res, next) => {
  if (err instanceof multer.MulterError) {
    if (err.code === 'LIMIT_FILE_SIZE') {
      return res.status(400).json({ message: 'File too large. Maximum size is 5MB.' });
    }
    return res.status(400).json({ message: err.message });
  }

  if (err) {
    return res.status(400).json({ message: err.message });
  }

  next();
});

// Serve uploaded files statically
app.use('/uploads', express.static('uploads'));

app.listen(5000, () => console.log('Server running on port 5000'));
```

**Key Concepts:**

- **`multer.diskStorage()`** gives you full control over where files are stored (`destination`) and what they are named (`filename`). Without custom storage, Multer uses memory storage and generates random filenames with no extension.
- **`fileFilter`** validates the uploaded file before it is saved. The callback `cb(null, true)` accepts the file, while `cb(new Error(...), false)` rejects it.
- **`upload.single('image')`** is middleware that processes a single file upload from the form field named `'image'`. For multiple files, use `upload.array('images', maxCount)`.
- **`limits.fileSize`** prevents excessively large uploads. The value is in bytes (5 * 1024 * 1024 = 5 MB).
- **Error handling middleware** (with 4 parameters) catches Multer-specific errors and sends appropriate error responses to the client.
- **`express.static('uploads')`** serves the uploaded files so they can be accessed via URLs like `http://localhost:5000/uploads/filename.jpg`.
</details>

---

**Exercise 3: Implement Search with Debounce in React and Express Endpoint with $regex**

Build a search feature with a debounced input in React and an Express endpoint that queries MongoDB using the `$regex` operator.

**Starter Code:**

```jsx
// Frontend: SearchComponent.jsx
import { useState, useEffect } from 'react';

function SearchComponent() {
  // TODO: Create state for search term and results

  // TODO: Implement debounced search using useEffect

  // TODO: Create function to fetch results from API

  return (
    <div>
      <h2>Search Products</h2>
      {/* TODO: Search input */}
      {/* TODO: Display results */}
    </div>
  );
}

export default SearchComponent;
```

```js
// Backend: server.js
const express = require('express');
const mongoose = require('mongoose');

const app = express();

// TODO: Create Product model

// TODO: Create GET route '/api/products/search' that uses $regex

app.listen(5000, () => console.log('Server running on port 5000'));
```

<details>
<summary>Solution</summary>

**Frontend: SearchComponent.jsx**

```jsx
import { useState, useEffect } from 'react';
import axios from 'axios';

function SearchComponent() {
  const [searchTerm, setSearchTerm] = useState('');
  const [results, setResults] = useState([]);
  const [loading, setLoading] = useState(false);

  // Debounced search using useEffect
  useEffect(() => {
    // If search term is empty, clear results and do not call API
    if (!searchTerm.trim()) {
      setResults([]);
      return;
    }

    // Set a timer that will fire after 500ms of inactivity
    const delayDebounce = setTimeout(() => {
      fetchResults(searchTerm);
    }, 500);

    // Cleanup: clear the timer if searchTerm changes before 500ms
    // This is the core of debouncing — each new keystroke cancels the previous timer
    return () => clearTimeout(delayDebounce);
  }, [searchTerm]);

  const fetchResults = async (query) => {
    try {
      setLoading(true);
      const response = await axios.get(
        `http://localhost:5000/api/products/search?q=${query}`
      );
      setResults(response.data);
    } catch (error) {
      console.error('Search error:', error);
    } finally {
      setLoading(false);
    }
  };

  return (
    <div style={{ maxWidth: '600px', margin: '20px auto' }}>
      <h2>Search Products</h2>

      <input
        type="text"
        placeholder="Search products..."
        value={searchTerm}
        onChange={(e) => setSearchTerm(e.target.value)}
        style={{ width: '100%', padding: '10px', fontSize: '16px' }}
      />

      {loading && <p>Searching...</p>}

      <ul style={{ listStyle: 'none', padding: 0 }}>
        {results.map((product) => (
          <li key={product._id} style={{ padding: '10px', borderBottom: '1px solid #ddd' }}>
            <h3>{product.name}</h3>
            <p>{product.description}</p>
            <span>Price: ${product.price}</span>
          </li>
        ))}
      </ul>

      {!loading && searchTerm && results.length === 0 && (
        <p>No products found.</p>
      )}
    </div>
  );
}

export default SearchComponent;
```

**Backend: server.js**

```js
const express = require('express');
const mongoose = require('mongoose');
const cors = require('cors');

const app = express();
app.use(cors());
app.use(express.json());

// Connect to MongoDB
mongoose.connect('mongodb://localhost:27017/shopDB');

// Product model
const Product = mongoose.model('Product', new mongoose.Schema({
  name: { type: String, required: true },
  description: { type: String },
  price: { type: Number, required: true }
}));

// Search route using $regex
app.get('/api/products/search', async (req, res) => {
  try {
    const { q } = req.query;

    if (!q) {
      return res.status(400).json({ message: 'Search query is required.' });
    }

    // Use $regex with 'i' option for case-insensitive search
    // Search across both name and description fields using $or
    const products = await Product.find({
      $or: [
        { name: { $regex: q, $options: 'i' } },
        { description: { $regex: q, $options: 'i' } }
      ]
    }).limit(20);

    res.json(products);
  } catch (error) {
    console.error('Search error:', error);
    res.status(500).json({ message: 'Server error during search.' });
  }
});

app.listen(5000, () => console.log('Server running on port 5000'));
```

**Key Concepts:**

- **Debouncing with `useEffect`:** The `setTimeout` inside `useEffect` creates a delay. The cleanup function (`return () => clearTimeout(...)`) cancels the previous timer whenever `searchTerm` changes. This means the API call only fires once the user has stopped typing for 500ms.
- **`$regex` with `$options: 'i'`:** The `$regex` operator performs a pattern match against the string field. The `'i'` option makes it case-insensitive, so searching for "phone" will match "Phone", "PHONE", and "phone".
- **`$or` operator:** Allows searching across multiple fields. The query matches documents where either the `name` or `description` contains the search term.
- **`.limit(20)`** prevents returning too many results, which could slow down the response and overwhelm the UI.
</details>

---

**Exercise 4: Build Pagination with React Page Buttons and Express skip/limit Endpoint**

Implement a complete pagination system with a React component that displays page navigation buttons and an Express endpoint that returns paginated results.

**Starter Code:**

```jsx
// Frontend: PaginatedList.jsx
import { useState, useEffect } from 'react';

function PaginatedList() {
  // TODO: Create state for items, current page, and total pages

  // TODO: Fetch paginated data from API

  // TODO: Create page change handler

  return (
    <div>
      <h2>Products</h2>
      {/* TODO: Display items */}
      {/* TODO: Pagination buttons */}
    </div>
  );
}

export default PaginatedList;
```

```js
// Backend: server.js
// TODO: Create GET route '/api/products' with pagination using skip and limit
```

<details>
<summary>Solution</summary>

**Frontend: PaginatedList.jsx**

```jsx
import { useState, useEffect } from 'react';
import axios from 'axios';

function PaginatedList() {
  const [products, setProducts] = useState([]);
  const [currentPage, setCurrentPage] = useState(1);
  const [totalPages, setTotalPages] = useState(1);
  const [loading, setLoading] = useState(false);
  const itemsPerPage = 10;

  // Fetch paginated data whenever currentPage changes
  useEffect(() => {
    fetchProducts(currentPage);
  }, [currentPage]);

  const fetchProducts = async (page) => {
    try {
      setLoading(true);
      const response = await axios.get(
        `http://localhost:5000/api/products?page=${page}&limit=${itemsPerPage}`
      );
      setProducts(response.data.products);
      setTotalPages(response.data.totalPages);
    } catch (error) {
      console.error('Fetch error:', error);
    } finally {
      setLoading(false);
    }
  };

  const handlePageChange = (page) => {
    if (page >= 1 && page <= totalPages) {
      setCurrentPage(page);
    }
  };

  // Generate array of page numbers for buttons
  const getPageNumbers = () => {
    const pages = [];
    for (let i = 1; i <= totalPages; i++) {
      pages.push(i);
    }
    return pages;
  };

  return (
    <div style={{ maxWidth: '600px', margin: '20px auto' }}>
      <h2>Products</h2>

      {loading ? (
        <p>Loading...</p>
      ) : (
        <ul style={{ listStyle: 'none', padding: 0 }}>
          {products.map((product) => (
            <li key={product._id} style={{ padding: '10px', borderBottom: '1px solid #eee' }}>
              <h3>{product.name}</h3>
              <p>Price: ${product.price}</p>
            </li>
          ))}
        </ul>
      )}

      {/* Pagination Controls */}
      <div style={{ display: 'flex', gap: '5px', justifyContent: 'center', marginTop: '20px' }}>
        <button
          onClick={() => handlePageChange(currentPage - 1)}
          disabled={currentPage === 1}
        >
          Previous
        </button>

        {getPageNumbers().map((page) => (
          <button
            key={page}
            onClick={() => handlePageChange(page)}
            style={{
              backgroundColor: currentPage === page ? '#007bff' : '#fff',
              color: currentPage === page ? '#fff' : '#000',
              border: '1px solid #ddd',
              padding: '8px 12px',
              cursor: 'pointer'
            }}
          >
            {page}
          </button>
        ))}

        <button
          onClick={() => handlePageChange(currentPage + 1)}
          disabled={currentPage === totalPages}
        >
          Next
        </button>
      </div>

      <p style={{ textAlign: 'center', marginTop: '10px' }}>
        Page {currentPage} of {totalPages}
      </p>
    </div>
  );
}

export default PaginatedList;
```

**Backend: server.js**

```js
const express = require('express');
const mongoose = require('mongoose');
const cors = require('cors');

const app = express();
app.use(cors());
app.use(express.json());

mongoose.connect('mongodb://localhost:27017/shopDB');

const Product = mongoose.model('Product', new mongoose.Schema({
  name: { type: String, required: true },
  description: String,
  price: { type: Number, required: true }
}));

// Paginated GET route
app.get('/api/products', async (req, res) => {
  try {
    // Parse query parameters with defaults
    const page = parseInt(req.query.page) || 1;
    const limit = parseInt(req.query.limit) || 10;

    // Calculate how many documents to skip
    const skip = (page - 1) * limit;

    // Get total count for calculating total pages
    const totalProducts = await Product.countDocuments();
    const totalPages = Math.ceil(totalProducts / limit);

    // Fetch the paginated results
    const products = await Product.find()
      .sort({ createdAt: -1 })    // Newest first
      .skip(skip)
      .limit(limit);

    res.json({
      products,
      currentPage: page,
      totalPages,
      totalProducts
    });
  } catch (error) {
    console.error('Pagination error:', error);
    res.status(500).json({ message: 'Server error.' });
  }
});

app.listen(5000, () => console.log('Server running on port 5000'));
```

**Key Concepts:**

- **`skip((page - 1) * limit)`** calculates the correct offset. Page 1 skips 0 documents, page 2 skips 10, page 3 skips 20, and so on.
- **`countDocuments()`** returns the total number of documents matching the query, which is essential for calculating the total number of pages.
- **`Math.ceil(total / limit)`** rounds up to ensure the last page is included even if it has fewer items than the limit.
- **`sort({ createdAt: -1 })`** ensures consistent ordering across pages. Without sorting, MongoDB may return documents in different orders between queries.
- The frontend tracks `currentPage` in state and re-fetches data whenever the page changes via `useEffect`.
- Previous and Next buttons are disabled at the boundaries to prevent invalid page requests.
</details>

---

**Exercise 5: Create a Basic Socket.io Chat Setup with Server Events and Client Connection**

Build a simple real-time chat application using Socket.io with a Node.js server that handles connection events and message broadcasting, and a React client that connects and sends/receives messages.

**Starter Code:**

```js
// Backend: server.js
const express = require('express');
const http = require('http');

const app = express();
const server = http.createServer(app);

// TODO: Set up Socket.io on the server

// TODO: Handle connection, message, and disconnect events

server.listen(5000, () => console.log('Server running on port 5000'));
```

```jsx
// Frontend: ChatComponent.jsx
import { useState, useEffect } from 'react';

function ChatComponent() {
  // TODO: Create state for messages, current message, and socket connection

  // TODO: Connect to Socket.io server and listen for messages

  // TODO: Handle sending messages

  return (
    <div>
      <h2>Chat Room</h2>
      {/* TODO: Display messages */}
      {/* TODO: Message input and send button */}
    </div>
  );
}

export default ChatComponent;
```

<details>
<summary>Solution</summary>

**Backend: server.js**

```js
const express = require('express');
const http = require('http');
const { Server } = require('socket.io');
const cors = require('cors');

const app = express();
app.use(cors());

const server = http.createServer(app);

// Initialize Socket.io with CORS configuration
const io = new Server(server, {
  cors: {
    origin: 'http://localhost:3000',
    methods: ['GET', 'POST']
  }
});

// Handle socket connections
io.on('connection', (socket) => {
  console.log(`User connected: ${socket.id}`);

  // Listen for 'send_message' events from this client
  socket.on('send_message', (data) => {
    console.log('Message received:', data);

    // Broadcast the message to ALL connected clients (including sender)
    io.emit('receive_message', {
      id: Date.now(),
      text: data.text,
      sender: socket.id,
      timestamp: new Date().toLocaleTimeString()
    });
  });

  // Listen for 'typing' events
  socket.on('typing', (data) => {
    // Broadcast to all clients EXCEPT the sender
    socket.broadcast.emit('user_typing', {
      sender: socket.id
    });
  });

  // Handle disconnection
  socket.on('disconnect', () => {
    console.log(`User disconnected: ${socket.id}`);
  });
});

server.listen(5000, () => console.log('Server running on port 5000'));
```

**Frontend: ChatComponent.jsx**

```jsx
import { useState, useEffect, useRef } from 'react';
import { io } from 'socket.io-client';

// Create socket connection outside the component to prevent
// re-creating the connection on every re-render
const socket = io('http://localhost:5000');

function ChatComponent() {
  const [messages, setMessages] = useState([]);
  const [currentMessage, setCurrentMessage] = useState('');
  const [isTyping, setIsTyping] = useState(false);
  const messagesEndRef = useRef(null);

  useEffect(() => {
    // Listen for incoming messages from the server
    socket.on('receive_message', (data) => {
      setMessages((prevMessages) => [...prevMessages, data]);
    });

    // Listen for typing indicator
    socket.on('user_typing', () => {
      setIsTyping(true);
      setTimeout(() => setIsTyping(false), 2000);
    });

    // Cleanup: remove listeners when component unmounts
    return () => {
      socket.off('receive_message');
      socket.off('user_typing');
    };
  }, []);

  // Auto-scroll to the latest message
  useEffect(() => {
    messagesEndRef.current?.scrollIntoView({ behavior: 'smooth' });
  }, [messages]);

  const sendMessage = () => {
    if (currentMessage.trim()) {
      // Emit the message to the server
      socket.emit('send_message', { text: currentMessage });
      setCurrentMessage('');
    }
  };

  const handleKeyPress = (e) => {
    if (e.key === 'Enter') {
      sendMessage();
    } else {
      // Notify others that this user is typing
      socket.emit('typing');
    }
  };

  return (
    <div style={{ maxWidth: '500px', margin: '20px auto', fontFamily: 'Arial' }}>
      <h2>Chat Room</h2>

      {/* Messages Display */}
      <div style={{
        height: '400px',
        overflowY: 'auto',
        border: '1px solid #ddd',
        borderRadius: '8px',
        padding: '15px',
        marginBottom: '10px',
        backgroundColor: '#f9f9f9'
      }}>
        {messages.map((msg) => (
          <div
            key={msg.id}
            style={{
              marginBottom: '10px',
              padding: '8px 12px',
              backgroundColor: msg.sender === socket.id ? '#007bff' : '#e9ecef',
              color: msg.sender === socket.id ? '#fff' : '#000',
              borderRadius: '12px',
              maxWidth: '75%',
              marginLeft: msg.sender === socket.id ? 'auto' : '0',
              textAlign: msg.sender === socket.id ? 'right' : 'left'
            }}
          >
            <p style={{ margin: 0 }}>{msg.text}</p>
            <small style={{ opacity: 0.7 }}>{msg.timestamp}</small>
          </div>
        ))}
        <div ref={messagesEndRef} />
      </div>

      {isTyping && <p style={{ fontSize: '12px', color: '#888' }}>Someone is typing...</p>}

      {/* Input and Send Button */}
      <div style={{ display: 'flex', gap: '10px' }}>
        <input
          type="text"
          placeholder="Type a message..."
          value={currentMessage}
          onChange={(e) => setCurrentMessage(e.target.value)}
          onKeyDown={handleKeyPress}
          style={{ flex: 1, padding: '10px', borderRadius: '8px', border: '1px solid #ddd' }}
        />
        <button
          onClick={sendMessage}
          style={{
            padding: '10px 20px',
            backgroundColor: '#007bff',
            color: '#fff',
            border: 'none',
            borderRadius: '8px',
            cursor: 'pointer'
          }}
        >
          Send
        </button>
      </div>
    </div>
  );
}

export default ChatComponent;
```

**Key Concepts:**

- **`io.on('connection')`** on the server fires whenever a new client connects. Each client receives a unique `socket.id`.
- **`io.emit()`** broadcasts a message to all connected clients, including the sender. Use **`socket.broadcast.emit()`** to send to everyone except the sender.
- **`socket.on()`** on the client listens for specific events emitted by the server. Event names (like `'receive_message'`) must match between client and server.
- **`socket.emit()`** on the client sends a message/event to the server.
- The socket connection is created outside the component to prevent re-creating it on every re-render. This is important because each `io()` call establishes a new WebSocket connection.
- The **cleanup function** in `useEffect` removes event listeners when the component unmounts to prevent memory leaks and duplicate handlers.
- **`useRef`** with `scrollIntoView` provides automatic scrolling to the most recent message, improving the user experience.
</details>
