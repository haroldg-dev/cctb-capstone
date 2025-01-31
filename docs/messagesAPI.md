### **Messages Endpoints**

#### 1. **Get All Messages**

- **Endpoint**: `GET /api/messages`
- **Description**: Retrieves a list of all messages.
- **Authorization**: Requires Bearer Token.
- **Query Parameters**:
  - `thread_id` (optional): Filter messages by `thread_id`.
- **Response**:
  ```json
  {
    "data": [
      {
        "id": 1,
        "thread_id": "thread_123",
        "status": "delivered",
        "direction": "inbound",
        "message_type": "text",
        "created_time": "2023-10-01T12:34:56Z",
        "content_type": "text",
        "content_text": "Hello, how can I help you?",
        "content_media_url": null,
        "content_media_type": null,
        "content_media_caption": null,
        "inbound_sender_full_name": "John Doe",
        "inbound_sender_number": "+1234567890",
        "outbound_sender_full_name": null
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

#### 2. **Get a Single Message**

- **Endpoint**: `GET /api/messages/{id}`
- **Description**: Retrieves details of a specific message by its `id`.
- **Authorization**: Requires Bearer Token.
- **Response**:
  ```json
  {
    "data": {
      "id": 1,
      "thread_id": "thread_123",
      "status": "delivered",
      "direction": "inbound",
      "message_type": "text",
      "created_time": "2023-10-01T12:34:56Z",
      "content_type": "text",
      "content_text": "Hello, how can I help you?",
      "content_media_url": null,
      "content_media_type": null,
      "content_media_caption": null,
      "inbound_sender_full_name": "John Doe",
      "inbound_sender_number": "+1234567890",
      "outbound_sender_full_name": null
    }
  }
  ```

---

#### 3. **Create a New Message**

- **Endpoint**: `POST /api/messages`
- **Description**: Creates a new message.
- **Authorization**: Requires Bearer Token.
- **Request Body**:
  ```json
  {
    "thread_id": "thread_123",
    "status": "sent",
    "direction": "outbound",
    "message_type": "text",
    "content_type": "text",
    "content_text": "Thank you for reaching out!",
    "content_media_url": null,
    "content_media_type": null,
    "content_media_caption": null,
    "outbound_sender_full_name": "Support Team"
  }
  ```
- **Response**:
  ```json
  {
    "data": {
      "id": 2,
      "thread_id": "thread_123",
      "status": "sent",
      "direction": "outbound",
      "message_type": "text",
      "created_time": "2023-10-01T12:35:10Z",
      "content_type": "text",
      "content_text": "Thank you for reaching out!",
      "content_media_url": null,
      "content_media_type": null,
      "content_media_caption": null,
      "inbound_sender_full_name": null,
      "inbound_sender_number": null,
      "outbound_sender_full_name": "Support Team"
    }
  }
  ```

---

#### 4. **Update a Message**

- **Endpoint**: `PUT /api/messages/{id}`
- **Description**: Updates an existing message by its `id`.
- **Authorization**: Requires Bearer Token.
- **Request Body**:
  ```json
  {
    "status": "read"
  }
  ```
- **Response**:
  ```json
  {
    "data": {
      "id": 1,
      "thread_id": "thread_123",
      "status": "read",
      "direction": "inbound",
      "message_type": "text",
      "created_time": "2023-10-01T12:34:56Z",
      "content_type": "text",
      "content_text": "Hello, how can I help you?",
      "content_media_url": null,
      "content_media_type": null,
      "content_media_caption": null,
      "inbound_sender_full_name": "John Doe",
      "inbound_sender_number": "+1234567890",
      "outbound_sender_full_name": null
    }
  }
  ```

---

#### 5. **Delete a Message**

- **Endpoint**: `DELETE /api/messages/{id}`
- **Description**: Deletes a message by its `id`.
- **Authorization**: Requires Bearer Token.
- **Response**:
  ```json
  {
    "message": "Message deleted successfully"
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
  - `404 Not Found`: Message not found.
  - `500 Internal Server Error`: Server error.

---

### **Authorization**

- **Authentication**: Bearer Token (JWT).
- **No specific permissions required**: Only a valid Bearer Token is needed for all endpoints.

---

### **Example Use Case**

1. **Create a Message**:

   ```bash
   curl -X POST -H "Content-Type: application/json" -H "Authorization: Bearer <token>" \
   -d '{
     "thread_id": "thread_123",
     "status": "sent",
     "direction": "outbound",
     "message_type": "text",
     "content_type": "text",
     "content_text": "Thank you for reaching out!",
     "outbound_sender_full_name": "Support Team"
   }' \
   http://api.example.com/api/messages
   ```

2. **Get All Messages**:

   ```bash
   curl -X GET -H "Authorization: Bearer <token>" \
   http://api.example.com/api/messages?thread_id=thread_123&limit=10&offset=0
   ```

3. **Update a Message**:

   ```bash
   curl -X PUT -H "Content-Type: application/json" -H "Authorization: Bearer <token>" \
   -d '{
     "status": "read"
   }' \
   http://api.example.com/api/messages/1
   ```

4. **Delete a Message**:
   ```bash
   curl -X DELETE -H "Authorization: Bearer <token>" \
   http://api.example.com/api/messages/1
   ```
