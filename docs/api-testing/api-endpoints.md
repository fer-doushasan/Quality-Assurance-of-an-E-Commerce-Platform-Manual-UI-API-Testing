# API Endpoints Documentation - E-Commerce Platform

## Base URL
**Staging:** `https://api-staging.ecommerce-platform.com/api/v1`  
**Production:** `https://api.ecommerce-platform.com/api/v1`

## Authentication
Most endpoints require authentication using JWT (JSON Web Token).

**Header Format:**
```
Authorization: Bearer {your_jwt_token}
```

---

## 1. Authentication Endpoints

### Register New User
**POST** `/auth/register`

**Description:** Create a new user account

**Authentication:** None required

**Request Body:**
```json
{
  "firstName": "string (required, 2-50 chars)",
  "lastName": "string (required, 2-50 chars)",
  "email": "string (required, valid email)",
  "password": "string (required, min 8 chars)",
  "confirmPassword": "string (required, must match password)"
}
```

**Success Response:** `201 Created`
```json
{
  "success": true,
  "data": {
    "userId": "uuid",
    "email": "user@example.com",
    "firstName": "John",
    "lastName": "Doe",
    "token": "jwt_token",
    "expiresIn": 86400
  },
  "message": "User registered successfully"
}
```

**Error Responses:**
- `400 Bad Request` - Invalid input
- `409 Conflict` - Email already exists

---

### Login
**POST** `/auth/login`

**Description:** Authenticate user and receive JWT token

**Authentication:** None required

**Request Body:**
```json
{
  "email": "string (required)",
  "password": "string (required)"
}
```

**Success Response:** `200 OK`
```json
{
  "success": true,
  "data": {
    "userId": "uuid",
    "email": "user@example.com",
    "firstName": "John",
    "lastName": "Doe",
    "token": "jwt_token",
    "refreshToken": "refresh_token",
    "expiresIn": 86400
  }
}
```

**Error Responses:**
- `401 Unauthorized` - Invalid credentials
- `400 Bad Request` - Missing required fields

---

### Logout
**POST** `/auth/logout`

**Description:** Invalidate current session token

**Authentication:** Required

**Success Response:** `200 OK`
```json
{
  "success": true,
  "message": "Logged out successfully"
}
```

---

### Refresh Token
**POST** `/auth/refresh`

**Description:** Get new access token using refresh token

**Request Body:**
```json
{
  "refreshToken": "string (required)"
}
```

**Success Response:** `200 OK`
```json
{
  "success": true,
  "data": {
    "token": "new_jwt_token",
    "expiresIn": 86400
  }
}
```

---

### Forgot Password
**POST** `/auth/forgot-password`

**Description:** Request password reset email

**Request Body:**
```json
{
  "email": "string (required)"
}
```

**Success Response:** `200 OK`
```json
{
  "success": true,
  "message": "Password reset email sent"
}
```

---

### Reset Password
**POST** `/auth/reset-password`

**Description:** Reset password using token from email

**Request Body:**
```json
{
  "token": "string (required)",
  "password": "string (required)",
  "confirmPassword": "string (required)"
}
```

**Success Response:** `200 OK`
```json
{
  "success": true,
  "message": "Password reset successfully"
}
```

---

## 2. User Endpoints

### Get Current User Profile
**GET** `/users/me`

**Description:** Get authenticated user's profile

**Authentication:** Required

**Success Response:** `200 OK`
```json
{
  "success": true,
  "data": {
    "userId": "uuid",
    "email": "user@example.com",
    "firstName": "John",
    "lastName": "Doe",
    "phone": "+1234567890",
    "avatar": "https://...",
    "createdAt": "2025-01-01T00:00:00Z",
    "emailVerified": true
  }
}
```

---

### Update User Profile
**PUT** `/users/me`

**Description:** Update user profile information

**Authentication:** Required

**Request Body:**
```json
{
  "firstName": "string (optional)",
  "lastName": "string (optional)",
  "phone": "string (optional)",
  "avatar": "string (optional, URL)"
}
```

**Success Response:** `200 OK`
```json
{
  "success": true,
  "data": {
    "userId": "uuid",
    "email": "user@example.com",
    "firstName": "John",
    "lastName": "Doe",
    "phone": "+1234567890",
    "updatedAt": "2025-12-28T12:00:00Z"
  },
  "message": "Profile updated successfully"
}
```

---

### Change Password
**POST** `/users/me/password`

**Description:** Change user password

**Authentication:** Required

**Request Body:**
```json
{
  "currentPassword": "string (required)",
  "newPassword": "string (required)",
  "confirmPassword": "string (required)"
}
```

**Success Response:** `200 OK`

**Error Responses:**
- `400 Bad Request` - Current password incorrect
- `400 Bad Request` - Password validation failed

---

## 3. Product Endpoints

### List Products
**GET** `/products`

**Description:** Get paginated list of products

**Authentication:** None required

**Query Parameters:**
- `page` (integer, default: 1) - Page number
- `limit` (integer, default: 20, max: 100) - Items per page
- `category` (string, optional) - Filter by category
- `search` (string, optional) - Search in name and description
- `minPrice` (number, optional) - Minimum price filter
- `maxPrice` (number, optional) - Maximum price filter
- `sort` (string, optional) - Sort order: `price_asc`, `price_desc`, `name_asc`, `name_desc`, `rating`, `newest`
- `inStock` (boolean, optional) - Filter in-stock items only

**Success Response:** `200 OK`
```json
{
  "success": true,
  "data": {
    "products": [
      {
        "productId": "uuid",
        "name": "Product Name",
        "description": "Short description",
        "price": 29.99,
        "salePrice": null,
        "currency": "USD",
        "category": "Electronics",
        "brand": "Brand Name",
        "imageUrl": "https://...",
        "stock": 100,
        "rating": 4.5,
        "reviewCount": 120,
        "inStock": true
      }
    ],
    "pagination": {
      "currentPage": 1,
      "totalPages": 10,
      "totalItems": 200,
      "itemsPerPage": 20,
      "hasNext": true,
      "hasPrev": false
    }
  }
}
```

---

### Get Product Details
**GET** `/products/{productId}`

**Description:** Get detailed information about a specific product

**Authentication:** None required

**Path Parameters:**
- `productId` (uuid, required) - Product identifier

**Success Response:** `200 OK`
```json
{
  "success": true,
  "data": {
    "productId": "uuid",
    "name": "Product Name",
    "description": "Detailed product description",
    "price": 29.99,
    "salePrice": 24.99,
    "discount": 17,
    "currency": "USD",
    "category": "Electronics",
    "subCategory": "Smartphones",
    "brand": "Brand Name",
    "images": [
      "https://image1.jpg",
      "https://image2.jpg",
      "https://image3.jpg"
    ],
    "stock": 100,
    "sku": "SKU-12345",
    "specifications": {
      "color": "Black",
      "size": "Medium",
      "weight": "1.5kg",
      "dimensions": "15x10x2 cm"
    },
    "features": [
      "Feature 1",
      "Feature 2",
      "Feature 3"
    ],
    "rating": 4.5,
    "reviewCount": 120,
    "tags": ["tag1", "tag2"],
    "inStock": true,
    "createdAt": "2025-01-01T00:00:00Z",
    "updatedAt": "2025-01-15T00:00:00Z"
  }
}
```

**Error Responses:**
- `404 Not Found` - Product does not exist

---

### Create Product (Admin)
**POST** `/products`

**Description:** Create a new product

**Authentication:** Required (Admin role)

**Request Body:**
```json
{
  "name": "string (required)",
  "description": "string (required)",
  "price": "number (required, > 0)",
  "salePrice": "number (optional)",
  "category": "string (required)",
  "brand": "string (required)",
  "images": "array of strings (required)",
  "stock": "integer (required, >= 0)",
  "sku": "string (required, unique)",
  "specifications": "object (optional)",
  "features": "array of strings (optional)"
}
```

**Success Response:** `201 Created`

**Error Responses:**
- `400 Bad Request` - Validation failed
- `403 Forbidden` - Insufficient permissions
- `409 Conflict` - SKU already exists

---

### Update Product (Admin)
**PUT** `/products/{productId}`

**Description:** Update existing product

**Authentication:** Required (Admin role)

**Success Response:** `200 OK`

---

### Delete Product (Admin)
**DELETE** `/products/{productId}`

**Description:** Delete a product

**Authentication:** Required (Admin role)

**Success Response:** `204 No Content`

---

## 4. Cart Endpoints

### Get Cart
**GET** `/cart`

**Description:** Get current user's shopping cart

**Authentication:** Required

**Success Response:** `200 OK`
```json
{
  "success": true,
  "data": {
    "cartId": "uuid",
    "userId": "uuid",
    "items": [
      {
        "itemId": "uuid",
        "productId": "uuid",
        "productName": "Product Name",
        "productImage": "https://...",
        "quantity": 2,
        "price": 29.99,
        "subtotal": 59.98
      }
    ],
    "subtotal": 59.98,
    "tax": 5.40,
    "shipping": 10.00,
    "discount": 0.00,
    "total": 75.38,
    "itemCount": 2,
    "updatedAt": "2025-12-28T12:00:00Z"
  }
}
```

---

### Add Item to Cart
**POST** `/cart/items`

**Description:** Add a product to cart

**Authentication:** Required

**Request Body:**
```json
{
  "productId": "uuid (required)",
  "quantity": "integer (required, > 0)"
}
```

**Success Response:** `200 OK` (cart updated) or `201 Created` (new item)

**Error Responses:**
- `400 Bad Request` - Invalid quantity or product
- `404 Not Found` - Product not found
- `409 Conflict` - Insufficient stock

---

### Update Cart Item
**PUT** `/cart/items/{itemId}`

**Description:** Update quantity of cart item

**Authentication:** Required

**Request Body:**
```json
{
  "quantity": "integer (required, > 0)"
}
```

**Success Response:** `200 OK`

---

### Remove Cart Item
**DELETE** `/cart/items/{itemId}`

**Description:** Remove item from cart

**Authentication:** Required

**Success Response:** `204 No Content`

---

### Clear Cart
**DELETE** `/cart`

**Description:** Remove all items from cart

**Authentication:** Required

**Success Response:** `200 OK`

---

## 5. Order Endpoints

### Create Order
**POST** `/orders`

**Description:** Place a new order

**Authentication:** Required

**Request Body:**
```json
{
  "shippingAddress": {
    "firstName": "string (required)",
    "lastName": "string (required)",
    "street": "string (required)",
    "city": "string (required)",
    "state": "string (required)",
    "zipCode": "string (required)",
    "country": "string (required)",
    "phone": "string (required)"
  },
  "billingAddress": {
    "same": "boolean (if true, use shipping address)",
    "firstName": "string (conditional)",
    "lastName": "string (conditional)",
    "street": "string (conditional)",
    "city": "string (conditional)",
    "state": "string (conditional)",
    "zipCode": "string (conditional)",
    "country": "string (conditional)"
  },
  "paymentMethod": "string (required): credit_card, paypal, etc.",
  "paymentToken": "string (required from payment gateway)"
}
```

**Success Response:** `201 Created`
```json
{
  "success": true,
  "data": {
    "orderId": "uuid",
    "orderNumber": "ORD-2025-001",
    "status": "pending",
    "items": [...],
    "shippingAddress": {...},
    "subtotal": 59.98,
    "tax": 5.40,
    "shipping": 10.00,
    "total": 75.38,
    "paymentStatus": "pending",
    "createdAt": "2025-12-28T12:00:00Z"
  },
  "message": "Order placed successfully"
}
```

---

### Get Order
**GET** `/orders/{orderId}`

**Description:** Get order details

**Authentication:** Required

**Success Response:** `200 OK`

---

### List User Orders
**GET** `/users/me/orders`

**Description:** Get all orders for current user

**Authentication:** Required

**Query Parameters:**
- `page` (integer, default: 1)
- `limit` (integer, default: 10)
- `status` (string, optional) - Filter by status

**Success Response:** `200 OK`

---

### Cancel Order
**PUT** `/orders/{orderId}/cancel`

**Description:** Cancel an order

**Authentication:** Required

**Request Body:**
```json
{
  "reason": "string (optional)"
}
```

**Success Response:** `200 OK`

**Error Responses:**
- `400 Bad Request` - Order cannot be cancelled (already shipped/delivered)
- `403 Forbidden` - Not your order
- `404 Not Found` - Order not found

---

## 6. Payment Endpoints

### Process Payment
**POST** `/payments/process`

**Description:** Process payment for an order

**Authentication:** Required

**Request Body:**
```json
{
  "orderId": "uuid (required)",
  "paymentMethod": "string (required)",
  "amount": "number (required)",
  "currency": "string (required)",
  "paymentToken": "string (required)"
}
```

**Success Response:** `200 OK`

---

### Get Payment Status
**GET** `/payments/{paymentId}`

**Description:** Get payment status

**Authentication:** Required

**Success Response:** `200 OK`

---

## Rate Limiting

**Rate Limit:** 100 requests per minute per IP address

**Response Headers:**
```
X-RateLimit-Limit: 100
X-RateLimit-Remaining: 95
X-RateLimit-Reset: 1640000000
```

**Rate Limit Exceeded:** `429 Too Many Requests`
```json
{
  "success": false,
  "message": "Rate limit exceeded. Please try again later.",
  "retryAfter": 60
}
```

---

## Error Response Format

All error responses follow this structure:

```json
{
  "success": false,
  "message": "Human-readable error message",
  "errors": [
    {
      "field": "fieldName",
      "code": "error_code",
      "message": "Specific error message"
    }
  ],
  "timestamp": "2025-12-28T12:00:00Z",
  "path": "/api/v1/endpoint"
}
```

---

## Common HTTP Status Codes

| Code | Meaning | Description |
|------|---------|-------------|
| 200 | OK | Request successful |
| 201 | Created | Resource created |
| 204 | No Content | Success with no response body |
| 400 | Bad Request | Invalid request data |
| 401 | Unauthorized | Authentication required |
| 403 | Forbidden | Insufficient permissions |
| 404 | Not Found | Resource not found |
| 409 | Conflict | Resource conflict (duplicate) |
| 422 | Unprocessable Entity | Validation errors |
| 429 | Too Many Requests | Rate limit exceeded |
| 500 | Internal Server Error | Server error |
| 502 | Bad Gateway | Gateway error |
| 503 | Service Unavailable | Service temporarily unavailable |

---

**API Version:** v1  
**Last Updated:** December 2025
