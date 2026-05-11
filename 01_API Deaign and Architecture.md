An **API (Application Programming Interface)** is a set of rules that allows two software applications to communicate with each other.

Think of it like a **waiter in a restaurant**:

* **You (Client)** → place an order
* **Waiter (API)** → takes request to kitchen
* **Kitchen (Server)** → prepares food
* **Waiter (API)** → brings response back

So, APIs help applications exchange data and functionality without exposing internal code.

---

# Simple Real-World Example

When you use the Instagram app:

1. App requests your profile data
2. Instagram API sends request to server
3. Server responds with JSON data
4. App displays your feed

---

# Why APIs are Used

| Purpose                     | Example                          |
| --------------------------- | -------------------------------- |
| Share data                  | Weather app getting weather data |
| Connect services            | Payment gateway integration      |
| Reuse functionality         | Login with Google                |
| Microservices communication | Frontend ↔ Backend               |
| Third-party integrations    | Maps, SMS, Email APIs            |

---

# Basic API Flow

```text
Client (Frontend/App)
        |
        | HTTP Request
        v
      API Server
        |
        | Database Query
        v
     Database
        |
        | Response Data
        v
      API Server
        |
        | JSON Response
        v
Client receives data
```

---

# Example of an API Request

## Request

```http
GET /users/1
```

## Response

```json
{
  "id": 1,
  "name": "Rahul",
  "email": "rahul@gmail.com"
}
```

---

# Types of APIs

APIs can be classified in multiple ways.

---

# 1. Based on Accessibility

## A. Open API (Public API)

Available for everyone.

### Examples

* OpenWeather Weather API
* Google Maps API

### Uses

* Third-party integrations
* Public developers

---

## B. Private API

Used internally within a company.

### Example

Frontend communicating with company backend.

```text
Company App → Internal API → Database
```

### Uses

* Internal systems
* Microservices

---

## C. Partner API

Shared with specific business partners.

### Example

Payment APIs shared with merchants.

---

## D. Composite API

Combines multiple APIs into one request.

### Example

One API call returns:

* User details
* Orders
* Payments

instead of multiple requests.

---

# 2. Based on Architecture Style

This is the most important classification for developers.

---

# A. REST API (Most Popular)

REST = Representational State Transfer

Uses HTTP methods.

## Features

* Simple
* Fast
* Stateless
* Uses JSON mostly

## HTTP Methods

| Method | Purpose     |
| ------ | ----------- |
| GET    | Fetch data  |
| POST   | Create data |
| PUT    | Update data |
| DELETE | Remove data |

---

## REST API Example

### Get users

```http
GET /users
```

### Create user

```http
POST /users
```

Body:

```json
{
  "name": "Amit"
}
```

---

## REST Architecture Flow

```text
Frontend
   |
HTTP Request
   |
REST API
   |
Database
```

---

# B. SOAP API

SOAP = Simple Object Access Protocol

Older and stricter than REST.

## Features

* XML only
* Highly secure
* Used in banking & enterprise systems

---

## SOAP Example

```xml
<soap:Envelope>
  <soap:Body>
    <getUser>
      <id>1</id>
    </getUser>
  </soap:Body>
</soap:Envelope>
```

---

## REST vs SOAP

| Feature     | REST            | SOAP               |
| ----------- | --------------- | ------------------ |
| Data Format | JSON            | XML                |
| Speed       | Faster          | Slower             |
| Simplicity  | Easy            | Complex            |
| Security    | Medium          | High               |
| Usage       | Web/Mobile apps | Enterprise systems |

---

# C. GraphQL API

Created by Meta (Facebook).

Client requests exactly the data it needs.

---

## Problem with REST

REST may return extra data.

```json
{
  "id":1,
  "name":"Rahul",
  "email":"abc@gmail.com",
  "address":"Delhi",
  "phone":"9999999999"
}
```

But maybe frontend only needs `name`.

---

## GraphQL Solution

### Query

```graphql
{
  user(id:1){
    name
  }
}
```

### Response

```json
{
  "data": {
    "user": {
      "name": "Rahul"
    }
  }
}
```

---

## Advantages

* Fetch exact data
* Reduces over-fetching
* Better for mobile apps

---

# D. gRPC API

Developed by Google.

Uses:

* Protocol Buffers (protobuf)
* HTTP/2

## Features

* Very fast
* Efficient
* Best for microservices

---

## Common Usage

* Real-time systems
* Internal services
* High-performance backend systems

---

# E. WebSocket API

Provides real-time communication.

## Features

* Two-way communication
* Persistent connection

---

## Uses

* Chat apps
* Live games
* Stock market apps

---

## Flow

```text
Client <=======> Server
   Real-time connection
```

---

# 3. Based on Communication

| Type             | Description              |
| ---------------- | ------------------------ |
| Synchronous API  | Waits for response       |
| Asynchronous API | Doesn't wait immediately |

---

# API Data Formats

| Format           | Used In     |
| ---------------- | ----------- |
| JSON             | REST APIs   |
| XML              | SOAP APIs   |
| Protocol Buffers | gRPC        |
| Plain Text       | Simple APIs |

---

# Status Codes in APIs

| Code | Meaning      |
| ---- | ------------ |
| 200  | Success      |
| 201  | Created      |
| 400  | Bad Request  |
| 401  | Unauthorized |
| 404  | Not Found    |
| 500  | Server Error |

---

# Authentication in APIs

## Common Methods

| Method     | Description                |
| ---------- | -------------------------- |
| API Key    | Simple key                 |
| JWT Token  | Secure login token         |
| OAuth      | Login with Google/Facebook |
| Basic Auth | Username/password          |

---

# Example Using JavaScript Fetch API

```javascript
fetch("https://api.example.com/users")
  .then(response => response.json())
  .then(data => console.log(data));
```

---

# API Lifecycle

```text
Client Request
      ↓
Authentication
      ↓
Business Logic
      ↓
Database Access
      ↓
Response Generation
      ↓
Client Receives Data
```

---

# Where APIs Are Used

| Industry     | Example         |
| ------------ | --------------- |
| E-commerce   | Payments        |
| Social Media | Feed loading    |
| Banking      | Transactions    |
| Maps         | Navigation      |
| Healthcare   | Patient records |
| AI           | Chatbots        |

---

# Popular API Tools

| Tool     | Purpose           |
| -------- | ----------------- |
| Postman  | API testing       |
| Swagger  | API documentation |
| Insomnia | API testing       |
| cURL     | API requests      |

---

# Simple REST API Example in Node.js

```javascript
const express = require("express");
const app = express();

app.get("/users", (req, res) => {
  res.json([
    { id: 1, name: "Rahul" },
    { id: 2, name: "Amit" }
  ]);
});

app.listen(3000, () => {
  console.log("Server running");
});
```

---

# Key Takeaways

## API is:

* A communication bridge between applications
* Used everywhere in modern software
* Mostly works over HTTP

---

# Most Important API Types

| API Type  | Best For               |
| --------- | ---------------------- |
| REST      | Web apps               |
| GraphQL   | Flexible data fetching |
| SOAP      | Enterprise systems     |
| gRPC      | High performance       |
| WebSocket | Real-time apps         |

---


