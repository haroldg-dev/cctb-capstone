### **Thread Endpoints**

#### 1. **Get All Threads**

- **Endpoint**: `GET /api/threads`
- **Description**: Retrieves a list of all threads.
- **Authorization**: Requires Bearer Token.
- **Query Parameters**:
  - `status` (optional): Filter threads by `thread_status`.
- **Response**:
  ```json
  {
    "data": [
      {
        "id": 1,
        "user_id": "user_123",
        "user_name": "John Doe",
        "user_phone": "+1234567890",
        "total_messages": 15,
        "thread_name": "Support Request",
        "thread_status": "open"
      },
      ...
    ],
    "pagination": {
      "total": 100,
      "limit": 10,
      "offset": 0
    }
  }
  ```

---

#### 2. **Get a Single Thread**

- **Endpoint**: `GET /api/threads/{id}`
- **Description**: Retrieves details of a specific thread by its `id`.
- **Authorization**: Requires Bearer Token.
- **Response**:
  ```json
  {
    "data": {
      "id": 1,
      "user_id": "user_123",
      "user_name": "John Doe",
      "user_phone": "+1234567890",
      "total_messages": 15,
      "thread_name": "Support Request",
      "thread_status": "open"
    }
  }
  ```

---

#### 3. **Create a New Thread**

- **Endpoint**: `POST /api/threads`
- **Description**: Creates a new thread.
- **Authorization**: Requires Bearer Token.
- **Request Body**:
  ```json
  {
    "user_id": "user_123",
    "user_name": "John Doe",
    "user_phone": "+1234567890",
    "thread_name": "New Support Request",
    "thread_status": "open"
  }
  ```
- **Response**:
  ```json
  {
    "data": {
      "id": 1,
      "user_id": "user_123",
      "user_name": "John Doe",
      "user_phone": "+1234567890",
      "total_messages": 0,
      "thread_name": "New Support Request",
      "thread_status": "open"
    }
  }
  ```

---

#### 4. **Update a Thread**

- **Endpoint**: `PUT /api/threads/{id}`
- **Description**: Updates an existing thread by its `id`.
- **Authorization**: Requires Bearer Token.
- **Request Body**:
  ```json
  {
    "user_name": "John Doe Updated",
    "user_phone": "+0987654321",
    "thread_name": "Updated Support Request",
    "thread_status": "closed"
  }
  ```
- **Response**:
  ```json
  {
    "data": {
      "id": 1,
      "user_id": "user_123",
      "user_name": "John Doe Updated",
      "user_phone": "+0987654321",
      "total_messages": 15,
      "thread_name": "Updated Support Request",
      "thread_status": "closed"
    }
  }
  ```

---

#### 5. **Delete a Thread**

- **Endpoint**: `DELETE /api/threads/{id}`
- **Description**: Deletes a thread by its `id`.
- **Authorization**: Requires Bearer Token.
- **Response**:
  ```json
  {
    "message": "Thread deleted successfully"
  }
  ```

---

### **Request/Response Format**

- **Request Headers**:
  - `Content-Type: application/json`
  - `Authorization: Bearer <token>`
- **Response Headers**:
  - `Content-Type: application/json`
- **Error Responses**:
  - `400 Bad Request`: Invalid input data.
  - `401 Unauthorized`: Missing or invalid authorization token.
  - `403 Forbidden`: Insufficient permissions.
  - `404 Not Found`: Thread not found.
  - `500 Internal Server Error`: Server error.

---

### **Authorization**

- **Authentication**: Bearer Token (JWT).

---

### **Example Use Case**

1. **Create a Thread**:

   ```bash
   curl -X POST -H "Content-Type: application/json" -H "Authorization: Bearer <token>" \
   -d '{
     "user_id": "user_123",
     "user_name": "John Doe",
     "user_phone": "+1234567890",
     "thread_name": "New Support Request",
     "thread_status": "open"
   }' \
   http://api.example.com/api/threads
   ```

2. **Get All Threads**:

   ```bash
   curl -X GET -H "Authorization: Bearer <token>" \
   http://api.example.com/api/threads?limit=10&offset=0
   ```

3. **Update a Thread**:

   ```bash
   curl -X PUT -H "Content-Type: application/json" -H "Authorization: Bearer <token>" \
   -d '{
     "thread_status": "closed"
   }' \
   http://api.example.com/api/threads/1
   ```

4. **Delete a Thread**:
   ```bash
   curl -X DELETE -H "Authorization: Bearer <token>" \
   http://api.example.com/api/threads/1
   ```
