# User Entity API Contract

## Base URL

```
/api/v1/users
```

## Authentication & Authorization

- All endpoints require authentication with a **Bearer Token**.
- `ADMIN` role is required for managing users (create, update, delete other users).
- Users can only access and update their own profiles unless they are an `ADMIN`.
- Uses JWT for authentication (Authorization: Bearer <token>).

---

## 1. Create a User

**Endpoint:**

```
POST /users
```

**Authorization:** `ADMIN` only

### Request Body (JSON)

```json
{
  "personId": 1,
  "status": "Active",
  "jobTitle": "Software Engineer",
  "department": "IT",
  "company": "Tech Corp",
  "role": "USER"
}
```

### Response (201 Created)

```json
{
  "id": 1,
  "person": {
    "id": 1,
    "name": "John",
    "lastName": "Doe"
  },
  "status": "Active",
  "jobTitle": "Software Engineer",
  "department": "IT",
  "company": "Tech Corp",
  "role": "USER",
  "createdAt": "2025-01-30T12:00:00Z",
  "updatedAt": "2025-01-30T12:00:00Z"
}
```

---

## 2. Get User by ID

**Endpoint:**

```
GET /users/{id}
```

**Authorization:** Authenticated Users (Users can only access their profile unless `ADMIN`)

### Response (200 OK)

```json
{
  "id": 1,
  "person": {
    "id": 1,
    "name": "John",
    "lastName": "Doe"
  },
  "status": "Active",
  "jobTitle": "Software Engineer",
  "department": "IT",
  "company": "Tech Corp",
  "role": "USER",
  "createdAt": "2025-01-30T12:00:00Z",
  "updatedAt": "2025-01-30T12:00:00Z"
}
```

---

## 3. Update User

**Endpoint:**

```
PUT /users/{id}
```

**Authorization:** Authenticated Users (Users can only update their own profile unless `ADMIN`)

### Request Body (JSON)

```json
{
  "status": "Inactive",
  "jobTitle": "Senior Engineer",
  "department": "R&D",
  "company": "Tech Corp"
}
```

### Response (200 OK)

```json
{
  "id": 1,
  "status": "Inactive",
  "jobTitle": "Senior Engineer",
  "department": "R&D",
  "company": "Tech Corp",
  "updatedAt": "2025-01-30T12:30:00Z"
}
```

---

## 4. Delete User

**Endpoint:**

```
DELETE /users/{id}
```

**Authorization:** `ADMIN` only

### Response (204 No Content)

---

## 5. Get All Users

**Endpoint:**

```
GET /users
```

**Authorization:** `ADMIN` only

### Response (200 OK)

```json
[
  {
    "id": 1,
    "person": {
      "id": 1,
      "name": "John",
      "lastName": "Doe"
    },
    "status": "Active",
    "jobTitle": "Software Engineer",
    "department": "IT",
    "company": "Tech Corp",
    "role": "USER",
    "createdAt": "2025-01-30T12:00:00Z",
    "updatedAt": "2025-01-30T12:00:00Z"
  }
]
```
