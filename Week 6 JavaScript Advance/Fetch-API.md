# Fetch API

## What is an API?

API stands for **Application Programming Interface**. It is a set of rules that allows one software application to communicate with another.

In simple words:

> An API is a **bridge** that lets two applications talk to each other.

### Real-Life Example

* You order food using a mobile app
* The app sends a request to the restaurant (API)
* Restaurant sends back the response (order status)

---

## Types of APIs

* **REST APIs** (Most common)
* **SOAP APIs**
* **GraphQL APIs**
* **Public APIs**
* **Private APIs**

---

## What is Fetch API?

The **Fetch API** is a modern JavaScript interface used to make HTTP requests (GET, POST, PUT, DELETE) from the browser.

It returns a **Promise** and is used to communicate with APIs.

---

## Basic Fetch Syntax

```js
fetch('https://api.example.com/data')
  .then(response => response.json())
  .then(data => console.log(data))
  .catch(error => console.error(error));
```

---

## HTTP Methods

* **GET** → Fetch data
* **POST** → Send data
* **PUT** → Update data
* **DELETE** → Remove data

---

## GET Request Example

```js
fetch('https://jsonplaceholder.typicode.com/posts')
  .then(res => res.json())
  .then(data => console.log(data));
```

---

## POST Request Example

```js
fetch('https://jsonplaceholder.typicode.com/posts', {
  method: 'POST',
  headers: {
    'Content-Type': 'application/json'
  },
  body: JSON.stringify({
    title: 'Hello',
    body: 'Fetch API example',
    userId: 1
  })
})
.then(res => res.json())
.then(data => console.log(data));
```

---

## Using Fetch with async / await

```js
async function getData() {
  try {
    const response = await fetch('https://jsonplaceholder.typicode.com/users');
    const data = await response.json();
    console.log(data);
  } catch (error) {
    console.error(error);
  }
}

getData();
```

---

## Error Handling in Fetch

```js
fetch(url)
  .then(res => {
    if (!res.ok) {
      throw new Error('Network response was not ok');
    }
    return res.json();
  })
  .then(data => console.log(data))
  .catch(err => console.log(err));
```

---

## What is API Creation?

Creating an API means building a **backend service** that provides data or functionality to other applications.

APIs are usually created using:

* Node.js (Express)
* Python (Flask / Django)
* Java (Spring Boot)

---

## Simple API Example (Node.js + Express)

```js
const express = require('express');
const app = express();

app.get('/api/users', (req, res) => {
  res.json([{ name: 'Ali' }, { name: 'Ahmed' }]);
});

app.listen(3000, () => console.log('API running'));
```

---

## How to Test an API

* Browser
* Postman
* Thunder Client
* cURL

---

## How to Buy an API

You can buy APIs from:

* RapidAPI
* Stripe
* OpenWeather
* Google APIs

Steps:

1. Create account
2. Subscribe to API plan
3. Get API key
4. Use key in request headers

---

## How to Sell an API

To sell your API:

1. Build a secure API
2. Add authentication (API Key / OAuth)
3. Set rate limits
4. Create pricing plans
5. Publish documentation
6. Use platforms like RapidAPI or your own website

---

## API Security Basics

* API Keys
* JWT Tokens
* HTTPS
* Rate Limiting
* Authentication & Authorization

---

## Real-World Uses of APIs

* Payment systems
* Maps & GPS
* Weather apps
* Social media
* AI services

---

## Best Practices

* Use proper HTTP status codes
* Validate input data
* Handle errors properly
* Secure your API
* Write clear documentation

---

## Summary

Fetch API allows JavaScript to communicate with APIs. APIs are essential for modern web applications and can be created, used, bought, or sold as services.

---

*Author: Fahad Ahmed*
