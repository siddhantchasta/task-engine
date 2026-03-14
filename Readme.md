# Secure Task Manager (Full Stack)

A full-stack task management application with **end-to-end encrypted API communication**, built using **Next.js, Node.js, Express, and MongoDB**.

Live Demo
Frontend: https://task-engine-delta.vercel.app
Backend API: https://task-engine.onrender.com

---

## Features

* User authentication with JWT
* Secure cookies for session management
* End-to-end AES encrypted API payloads
* Task creation and management
* Search and status filtering
* Pagination support
* Responsive modern UI
* Fully deployed cloud architecture

---

## Tech Stack

Frontend

* Next.js (App Router)
* TailwindCSS
* Axios

Backend

* Node.js
* Express.js
* JWT Authentication

Database

* MongoDB Atlas

Deployment

* Vercel (Frontend)
* Render (Backend)

Security

* AES Encryption (CryptoJS)
* HTTP-only cookies
* CORS protection

---

## Architecture

           ┌──────────────────────┐
           │  Next.js Frontend    │
           │  (Vercel Deployment) │
           └─────────┬────────────┘
                     │
                     │ AES Encrypted API Requests
                     │
           ┌─────────▼────────────┐
           │  Express Backend     │
           │  (Render Deployment) │
           │  JWT Authentication  │
           └─────────┬────────────┘
                     │
                     │
             ┌───────▼────────┐
             │   MongoDB      │
             │   Atlas DB     │
             └────────────────┘

The frontend encrypts request payloads before sending them to the backend.
The backend decrypts incoming data, processes the request, and returns encrypted responses.
---

## Screenshots

### Authentication Page

![Auth](screenshots/auth.png)

### Dashboard & Task Management

![Dashboard](screenshots/dashboard.png)

---

## Running Locally

Backend

```bash
cd backend
npm install
npm run dev
```

Frontend

```bash
cd frontend
npm install
npm run dev
```

---

## Environment Variables

Create a `.env` file in the backend folder:

```
PORT=5001
MONGO_URI=your_mongo_uri
JWT_SECRET=your_secret
AES_SECRET=your_secret
```

---

## API Documentation

The backend exposes REST APIs for authentication and task management.  
All task-related requests and responses are **AES encrypted** for secure communication.

Base URL:

```
https://task-engine.onrender.com/api
```

---

### 1. Register User

**Endpoint**

```
POST /api/auth/register
```

**Request Body**

```json
{
  "email": "user@example.com",
  "password": "123456"
}
```

**Response**

```json
{
  "message": "User created"
}
```

---

### 2. Login User

**Endpoint**

```
POST /api/auth/login
```

**Request Body**

```json
{
  "email": "user@example.com",
  "password": "123456"
}
```

**Response**

```json
{
  "message": "Logged in"
}
```

**Notes**

- A JWT token is issued on successful login.
- The token is stored in an **HTTP-only cookie** for secure authentication.

---

### 3. Create Task

**Endpoint**

```
POST /api/tasks
```

**Request Body**

The request payload is **AES encrypted**.

Example:

```json
{
  "payload": "AES_ENCRYPTED_STRING"
}
```

Example decrypted payload:

```json
{
  "title": "Complete Assignment",
  "description": "Finish the SyncUp internship assignment",
  "status": "pending"
}
```

**Response**

```json
{
  "title": "Complete Assignment",
  "description": "Finish the SyncUp internship assignment",
  "status": "pending"
}
```

---

### 4. Fetch Tasks

**Endpoint**

```
GET /api/tasks
```

**Query Parameters**

| Parameter | Description |
|-----------|-------------|
| page | Pagination page number |
| search | Search by task title |
| status | Filter by task status |

Example:

```
GET /api/tasks?page=1&search=&status=
```

**Response**

```json
{
  "tasks": [
    {
      "_id": "12345",
      "title": "Complete Assignment",
      "description": "Finish project",
      "status": "pending"
    }
  ],
  "currentPage": 1,
  "totalPages": 1
}
```

---

### 5. Update Task

**Endpoint**

```
PUT /api/tasks/:id
```

**Request Body**

```json
{
  "title": "Updated Task Title",
  "description": "Updated description",
  "status": "completed"
}
```

**Response**

```json
{
  "message": "Task updated successfully"
}
```

---

### 6. Delete Task

**Endpoint**

```
DELETE /api/tasks/:id
```

**Response**

```json
{
  "message": "Task deleted"
}
```

---

## Security Implementation

The application implements multiple security mechanisms:

- **JWT Authentication** for protected routes
- **HTTP-only cookies** to store authentication tokens
- **AES encryption** for request and response payloads
- **Environment variables** to store secrets (`JWT_SECRET`, `AES_SECRET`)
- **CORS configuration** for controlled cross-origin access
---

## Author

Siddhant Chasta
IIT Kharagpur

---
