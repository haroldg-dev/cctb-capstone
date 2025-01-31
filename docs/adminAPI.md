# Admin Entity API Contract

## Base URL

```
/api/v1/admins
```

## Authentication & Authorization

- All endpoints require authentication with a **Bearer Token**.
- `SUPER_ADMIN` role is required for managing admins (create, update, delete other admins).
- Admins can only access and update their own profiles unless they are a `SUPER_ADMIN`.
- Uses JWT for authentication (Authorization: Bearer <token>).

---

## 1. Create an Admin

**Endpoint:**

```
POST /admins
```

**Authorization:** `SUPER_ADMIN` only

### Request Body (JSON)

```json
{
  "personId": 1,
  "company": "Tech Corp",
  "jobTitle": "CTO",
  "department": "Management",
  "role": "ADMIN"
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
  "company": "Tech Corp",
  "jobTitle": "CTO",
  "department": "Management",
  "role": "ADMIN",
  "createdAt": "2025-01-30T12:00:00Z",
  "updatedAt": "2025-01-30T12:00:00Z"
}
```

---

## 2. Get Admin by ID

**Endpoint:**

```
GET /admins/{id}
```

**Authorization:** Authenticated Admins (Admins can only access their profile unless `SUPER_ADMIN`)

### Response (200 OK)

```json
{
  "id": 1,
  "person": {
    "id": 1,
    "name": "John",
    "lastName": "Doe"
  },
  "company": "Tech Corp",
  "jobTitle": "CTO",
  "department": "Management",
  "role": "ADMIN",
  "createdAt": "2025-01-30T12:00:00Z",
  "updatedAt": "2025-01-30T12:00:00Z"
}
```

---

## 3. Update Admin

**Endpoint:**

```
PUT /admins/{id}
```

**Authorization:** Authenticated Admins (Admins can only update their own profile unless `SUPER_ADMIN`)

### Request Body (JSON)

```json
{
  "company": "New Tech Corp",
  "jobTitle": "CIO",
  "department": "IT"
}
```

### Response (200 OK)

```json
{
  "id": 1,
  "company": "New Tech Corp",
  "jobTitle": "CIO",
  "department": "IT",
  "updatedAt": "2025-01-30T12:30:00Z"
}
```

---

## 4. Delete Admin

**Endpoint:**

```
DELETE /admins/{id}
```

**Authorization:** `SUPER_ADMIN` only

### Response (204 No Content)

---

## 5. Get All Admins

**Endpoint:**

```
GET /admins
```

**Authorization:** `SUPER_ADMIN` only

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
    "company": "Tech Corp",
    "jobTitle": "CTO",
    "department": "Management",
    "role": "ADMIN",
    "createdAt": "2025-01-30T12:00:00Z",
    "updatedAt": "2025-01-30T12:00:00Z"
  }
]
```
