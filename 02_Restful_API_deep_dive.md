# RESTful API — Complete Deep Dive

A **RESTful API** is an API that follows REST architecture principles and communicates mainly over HTTP.

REST APIs are the backbone of:

* Web applications
* Mobile apps
* Microservices
* SaaS platforms
* Cloud systems

Examples:

* GitHub API
* Stripe API
* Spotify API

---

# 1. What is REST?

REST = **Representational State Transfer**

It is an architectural style introduced by:

Roy Fielding

REST allows communication between:

* Client
* Server

using:

* HTTP
* URLs
* JSON

---

# Real World Understanding

Imagine a food delivery app.

```text id="u3p1pf"
Mobile App  --->  REST API  ---> Database
```

The app:

* requests restaurant data
* places orders
* updates payment

All through APIs.

---

# 2. REST Architecture Principles

---

# A. Client-Server Architecture

Frontend and backend are separate.

```text id="1ckjyv"
Frontend ---> API ---> Database
```

Benefits:

* Independent development
* Better scalability

---

# B. Statelessness

Server does NOT remember previous requests.

Each request must contain:

* authentication
* data
* headers

Example:

```http id="q3c2kc"
GET /users/1
Authorization: Bearer TOKEN
```

---

# C. Cacheable

Responses can be cached.

Benefits:

* Faster performance
* Reduced server load

---

# D. Uniform Interface

REST APIs follow predictable URL structures.

Example:

```text id="4oq2m9"
/users
/users/1
/orders
/orders/5
```

---

# E. Layered System

Client doesn’t know:

* database
* microservices
* proxies
* caching layers

---

# 3. Anatomy of REST API

A REST API request contains:

```text id="zknc5s"
HTTP Method
URL Endpoint
Headers
Body (optional)
Query Parameters
```

---

# Example

```http id="r4k8h3"
POST /users HTTP/1.1
Host: api.example.com
Content-Type: application/json

{
  "name": "Rahul",
  "email": "rahul@gmail.com"
}
```

---

# 4. HTTP Methods (Most Important)

HTTP methods define actions.

---

# A. GET → Fetch Data

Used to retrieve data.

## Example

```http id="zhm4tm"
GET /users
```

## Response

```json id="7uw5px"
[
  {
    "id":1,
    "name":"Rahul"
  }
]
```

---

## GET Characteristics

| Property     | Value      |
| ------------ | ---------- |
| Safe         | Yes        |
| Idempotent   | Yes        |
| Request Body | Usually No |

---

# B. POST → Create Data

Creates new resources.

## Example

```http id="e7ccn8"
POST /users
```

Body:

```json id="o91c7p"
{
  "name":"Amit"
}
```

---

## Response

```json id="0ru3s2"
{
  "id":101,
  "name":"Amit"
}
```

---

## POST Characteristics

| Property   | Value |
| ---------- | ----- |
| Safe       | No    |
| Idempotent | No    |

---

# C. PUT → Replace Entire Resource

Updates full resource.

## Example

```http id="jlwm6i"
PUT /users/1
```

Body:

```json id="5f19dx"
{
  "name":"Rahul Sharma",
  "email":"rahul@gmail.com"
}
```

---

# D. PATCH → Partial Update

Updates only specific fields.

## Example

```http id="ktl1xh"
PATCH /users/1
```

```json id="4hf9x7"
{
  "name":"Updated Name"
}
```

---

# PUT vs PATCH

| Feature        | PUT      | PATCH     |
| -------------- | -------- | --------- |
| Update Type    | Full     | Partial   |
| Missing Fields | Replaced | Unchanged |

---

# E. DELETE → Remove Resource

## Example

```http id="z67kqy"
DELETE /users/1
```

---

# 5. CRUD Operations Mapping

| CRUD   | HTTP Method |
| ------ | ----------- |
| Create | POST        |
| Read   | GET         |
| Update | PUT/PATCH   |
| Delete | DELETE      |

---

# 6. API Endpoints

Endpoints are URLs exposing resources.

---

# Good REST Endpoint Design

## Resource-Based Naming

✅ Good

```text id="z7cljf"
/users
/products
/orders
```

❌ Bad

```text id="3l0d8w"
/getUsers
/createProduct
```

REST uses HTTP methods instead of verbs in URLs.

---

# Nested Endpoints

```text id="k2o7pb"
/users/1/orders
```

Meaning:

* fetch orders of user 1

---

# Endpoint Examples

| Action       | Endpoint        |
| ------------ | --------------- |
| Get users    | GET /users      |
| Get one user | GET /users/1    |
| Create user  | POST /users     |
| Update user  | PUT /users/1    |
| Delete user  | DELETE /users/1 |

---

# 7. Path Parameters

Dynamic values in URL.

## Example

```text id="eswz48"
/users/:id
```

Actual:

```text id="ujyd6n"
/users/10
```

---

# Express Example

```javascript id="4b0ryy"
app.get("/users/:id", (req, res) => {
  console.log(req.params.id);
});
```

---

# 8. Query Parameters

Used for:

* filtering
* pagination
* searching
* sorting

---

# Example

```text id="qenl14"
/products?page=1&limit=10
```

---

# Common Query Usage

| Purpose    | Example       |
| ---------- | ------------- |
| Pagination | ?page=1       |
| Limit      | ?limit=10     |
| Search     | ?search=phone |
| Sort       | ?sort=price   |

---

# 9. Request Headers

Headers contain metadata.

---

# Common Headers

| Header        | Purpose                |
| ------------- | ---------------------- |
| Content-Type  | Data format            |
| Authorization | Authentication         |
| Accept        | Expected response type |

---

# Example

```http id="8s6w8p"
Authorization: Bearer JWT_TOKEN
```

---

# 10. Request Body

Mainly used with:

* POST
* PUT
* PATCH

Usually JSON.

---

# Example

```json id="jrcshn"
{
  "title":"iPhone",
  "price":1000
}
```

---

# 11. JSON Deep Dive

JSON = JavaScript Object Notation

Most REST APIs use JSON.

---

# JSON Rules

✅ Valid

```json id="s9h0f3"
{
  "name":"Rahul",
  "age":25
}
```

❌ Invalid

```json id="2nf9nm"
{
  name:"Rahul"
}
```

Keys must be in double quotes.

---

# JSON Data Types

| Type    | Example |
| ------- | ------- |
| String  | "hello" |
| Number  | 25      |
| Boolean | true    |
| Array   | []      |
| Object  | {}      |
| Null    | null    |

---

# Complex JSON Example

```json id="qztj2f"
{
  "user": {
    "id": 1,
    "name": "Rahul",
    "skills": ["React", "Node"],
    "address": {
      "city": "Delhi"
    }
  }
}
```

---

# 12. HTTP Responses

Server sends response.

Structure:

```text id="7j6mnf"
Status Code
Headers
Body
```

---

# Example Response

```http id="z8q8an"
HTTP/1.1 200 OK
Content-Type: application/json

{
  "success": true
}
```

---

# 13. HTTP Status Codes (VERY IMPORTANT)

---

# A. 2xx → Success

| Code | Meaning    |
| ---- | ---------- |
| 200  | OK         |
| 201  | Created    |
| 204  | No Content |

---

# Example

```http id="zj8zsl"
201 Created
```

Used after successful POST.

---

# B. 3xx → Redirection

| Code | Meaning            |
| ---- | ------------------ |
| 301  | Permanent Redirect |
| 302  | Temporary Redirect |

Rare in APIs.

---

# C. 4xx → Client Errors

| Code | Meaning           |
| ---- | ----------------- |
| 400  | Bad Request       |
| 401  | Unauthorized      |
| 403  | Forbidden         |
| 404  | Not Found         |
| 409  | Conflict          |
| 422  | Validation Error  |
| 429  | Too Many Requests |

---

# Important Difference

## 401 Unauthorized

User NOT authenticated.

## 403 Forbidden

User authenticated but no permission.

---

# D. 5xx → Server Errors

| Code | Meaning               |
| ---- | --------------------- |
| 500  | Internal Server Error |
| 502  | Bad Gateway           |
| 503  | Service Unavailable   |

---

# Real API Error Example

```json id="6yx1sn"
{
  "error": "Email already exists"
}
```

---

# 14. REST API Response Best Practices

---

# Good Response Structure

```json id="g92rzv"
{
  "success": true,
  "message": "User fetched successfully",
  "data": {
    "id": 1,
    "name": "Rahul"
  }
}
```

---

# Error Response

```json id="p4t8mb"
{
  "success": false,
  "message": "Validation failed"
}
```

---

# 15. Authentication in REST APIs

---

# A. API Key

Simple access key.

```http id="aqrx0f"
x-api-key: abc123
```

---

# B. JWT Authentication

Most common modern auth.

Flow:

```text id="qivkk6"
Login
  ↓
Server generates JWT
  ↓
Client stores token
  ↓
Client sends token in headers
```

---

# JWT Example

```http id="e4myul"
Authorization: Bearer TOKEN
```

---

# C. OAuth

Used in:

* Login with Google
* Login with GitHub

---

# 16. Idempotency

Very important interview topic.

---

# What is Idempotent?

Multiple identical requests produce same result.

---

# Examples

| Method | Idempotent |
| ------ | ---------- |
| GET    | Yes        |
| PUT    | Yes        |
| DELETE | Yes        |
| POST   | No         |

---

# Why POST is NOT Idempotent?

```text id="91u61f"
POST /orders
```

Sending twice may create:

* two orders

---

# 17. Pagination

Avoid returning huge data.

---

# Pagination Example

```text id="b56ah1"
/products?page=2&limit=20
```

---

# Response

```json id="x96cnq"
{
  "page": 2,
  "limit": 20,
  "total": 200,
  "data": []
}
```

---

# 18. Filtering & Sorting

---

# Filtering

```text id="d90ogd"
/products?category=mobile
```

---

# Sorting

```text id="98juyz"
/products?sort=price
```

---

# 19. Versioning APIs

Prevents breaking frontend apps.

---

# Common Methods

| Type              | Example   |
| ----------------- | --------- |
| URL Versioning    | /v1/users |
| Header Versioning | Accept:v2 |

---

# 20. Rate Limiting

Protects APIs from abuse.

---

# Example

```text id="ry5zwu"
100 requests/minute
```

If exceeded:

```http id="l4e9iw"
429 Too Many Requests
```

---

# 21. REST API Lifecycle

```text id="4s5s1p"
Client Request
      ↓
Routing
      ↓
Middleware
      ↓
Authentication
      ↓
Controller
      ↓
Service Logic
      ↓
Database
      ↓
Response
```

---

# 22. REST API in Express.js

---

# Basic Server

```javascript id="2yr1p0"
const express = require("express");
const app = express();

app.use(express.json());

app.get("/users", (req, res) => {
  res.json([
    { id: 1, name: "Rahul" }
  ]);
});

app.post("/users", (req, res) => {
  const user = req.body;

  res.status(201).json({
    success: true,
    data: user
  });
});

app.listen(3000);
```

---

# 23. REST API Folder Structure

```text id="zrqdcv"
project/
│
├── routes/
├── controllers/
├── services/
├── models/
├── middleware/
├── utils/
└── app.js
```

---

# 24. Common REST API Best Practices

---

# Naming

✅ Use nouns

```text id="wzjlwm"
/users
```

❌ Avoid verbs

```text id="1yb4ne"
/getUsers
```

---

# Use Proper Status Codes

* 200 → success
* 201 → created
* 404 → not found

---

# Validate Inputs

Never trust client data.

---

# Use HTTPS

Protects sensitive data.

---

# Return Consistent Responses

Maintain standard response structure.

---

# 25. Common Mistakes

| Mistake                  | Problem           |
| ------------------------ | ----------------- |
| Using verbs in URLs      | Not RESTful       |
| Returning 200 for errors | Confusing         |
| Huge responses           | Performance issue |
| No validation            | Security risks    |
| No pagination            | Slow APIs         |

---

# 26. REST vs GraphQL

| Feature            | REST     | GraphQL |
| ------------------ | -------- | ------- |
| Multiple endpoints | Yes      | No      |
| Overfetching       | Possible | Minimal |
| Simplicity         | Easier   | Complex |
| Caching            | Better   | Harder  |

---

# 27. Scenario-Based Interview Questions

---

# Q1. PUT vs PATCH?

### Answer

* PUT replaces full resource
* PATCH updates partial fields

---

# Q2. Why is REST stateless?

### Answer

Because each request contains all required information.
Server doesn’t store client session state.

Benefits:

* scalability
* reliability

---

# Q3. Difference between 401 and 403?

### Answer

401:

* authentication missing

403:

* authenticated but not authorized

---

# Q4. Why use pagination?

### Answer

Prevents:

* huge payloads
* slow responses
* high memory usage

---

# Q5. How would you design a product API?

### Example Endpoints

```text id="cx7vma"
GET /products
GET /products/:id
POST /products
PUT /products/:id
DELETE /products/:id
```

---

# Q6. How do you secure REST APIs?

### Answer

* HTTPS
* JWT
* Rate limiting
* Input validation
* CORS
* Helmet
* API Gateway

---

# Q7. What happens when client sends invalid JSON?

### Answer

Server returns:

```http id="ydrm9k"
400 Bad Request
```

---

# Q8. Explain Idempotency with Example

genui{"math_block_widget_always_prefetch_v2":{"content":"f(x)=x"}}

Example idea:

* Calling GET multiple times gives same result
* Calling PUT with same data repeatedly keeps same state

POST may create duplicates.

---

# Q9. What status code for successful DELETE?

### Answer

Usually:

```http id="spmf88"
204 No Content
```

or

```http id="mjlwm4"
200 OK
```

---

# Q10. How do you handle API versioning?

### Answer

Most common:

```text id="5e7k1x"
/api/v1/users
```

---

# 28. Advanced Scenario Questions

---

# Scenario 1

## API taking 8 seconds to respond. What will you do?

### Answer

* Add indexing
* Use caching
* Optimize queries
* Add pagination
* Compress responses
* Reduce joins
* Use CDN

---

# Scenario 2

## Multiple clients updating same resource simultaneously?

### Solutions

* Optimistic locking
* Version field
* Transactions

---

# Scenario 3

## Users spamming API requests?

### Solutions

* Rate limiting
* API Gateway
* Captcha
* IP blocking

---

# Scenario 4

## Frontend needs only specific fields?

### Solutions

* Query params
* GraphQL
* Sparse fieldsets

Example:

```text id="54m0b2"
/users?fields=name,email
```

---

# Scenario 5

## Large file upload handling?

### Solutions

* Multipart upload
* Streaming
* Chunk uploads

---

# 29. Frequently Asked REST Interview Questions

| Question                        | Level        |
| ------------------------------- | ------------ |
| What is REST?                   | Beginner     |
| Difference between PUT & PATCH? | Beginner     |
| What is statelessness?          | Beginner     |
| Explain idempotency             | Intermediate |
| How JWT works?                  | Intermediate |
| How caching works in REST?      | Intermediate |
| Design scalable APIs            | Advanced     |
| API security best practices     | Advanced     |
| Handle millions of requests?    | Advanced     |

---

# 30. Final Mental Model

```text id="9mpsgq"
Client
  ↓
HTTP Request
  ↓
REST Endpoint
  ↓
Middleware/Auth
  ↓
Business Logic
  ↓
Database
  ↓
JSON Response
  ↓
Client
```

