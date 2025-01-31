# Person Entity API Contract

## Base URL

```
/api/v1/persons
```

## Authentication & Authorization

- All endpoints require authentication.
- Admin-specific actions (delete, update role) require `ADMIN` role.
- Users can only update their own profiles unless they are an `ADMIN`.
- Uses JWT for authentication (Authorization: Bearer <token>).

---

## 1. Create a Person (Sign-up)

**Endpoint:**

```
POST /persons
```

### Request Body (JSON)

```json
{
  "name": "John",
  "lastName": "Doe",
  "email": "john.doe@example.com",
  "password": "securepassword",
  "idType": 1,
  "idNum": 12345678,
  "phone": "+1234567890",
  "countryCode": 1,
  "nationalNumber": 987654321,
  "gender": "MALE",
  "avatar": "DEFAULT"
}
```

### Response (201 Created)

```json
{
  "id": 1,
  "name": "John",
  "lastName": "Doe",
  "email": "john.doe@example.com",
  "phone": "+1234567890",
  "gender": "MALE",
  "avatar": "DEFAULT",
  "role": "USER"
}
```

---

## 2. Get Person by ID

**Endpoint:**

```
GET /persons/{id}
```

**Authorization:** Authenticated Users (Users can only access their profile unless `ADMIN`)

### Response (200 OK)

```json
{
  "id": 1,
  "name": "John",
  "lastName": "Doe",
  "email": "john.doe@example.com",
  "phone": "+1234567890",
  "gender": "MALE",
  "avatar": "DEFAULT",
  "role": "USER"
}
```

---

## 3. Update Person

**Endpoint:**

```
PUT /persons/{id}
```

**Authorization:** Authenticated Users (Users can only update their own profile unless `ADMIN`)

### Request Body (JSON)

```json
{
  "name": "John Updated",
  "lastName": "Doe",
  "phone": "+1234567890",
  "gender": "MALE",
  "avatar": "CUSTOM"
}
```

### Response (200 OK)

```json
{
  "id": 1,
  "name": "John Updated",
  "lastName": "Doe",
  "phone": "+1234567890",
  "gender": "MALE",
  "avatar": "CUSTOM"
}
```

---

## 4. Delete Person

**Endpoint:**

```
DELETE /persons/{id}
```

**Authorization:** `ADMIN` only

### Response (204 No Content)

---

## 5. Login

**Endpoint:**

```
POST /persons/login
```

**Authorization:** Public

### Request Body (JSON)

```json
{
  "email": "john.doe@example.com",
  "password": "securepassword"
}
```

### Response (200 OK)

```json
{
  "accessToken": "eyJhbGciOiJI...",
  "refreshToken": "eyJhbGciOiJI..."
}
```

---

## 6. Refresh Token

**Endpoint:**

```
POST /persons/refresh
```

**Authorization:** Public

### Request Body (JSON)

```json
{
  "refreshToken": "eyJhbGciOiJI..."
}
```

### Response (200 OK)

```json
{
  "accessToken": "eyJhbGciOiJI..."
}
```

---

## 7. Logout

**Endpoint:**

```
POST /persons/logout
```

**Authorization:** Authenticated Users

### Request Body (JSON)

```json
{
  "refreshToken": "eyJhbGciOiJI..."
}
```

### Response (200 OK)

```json
{
  "message": "Logged out successfully"
}
```
