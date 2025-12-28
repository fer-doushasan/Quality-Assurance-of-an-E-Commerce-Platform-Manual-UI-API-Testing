# API Test Cases - E-Commerce Platform

## Overview
This document contains comprehensive API test cases for the e-commerce platform's RESTful API endpoints.

---

## 1. Authentication API Test Cases

### TC-API-AUTH-001: User Registration - Success

**Endpoint:** `POST /api/auth/register`  
**Priority:** Critical  
**Type:** Positive

**Request Headers:**
```json
{
  "Content-Type": "application/json"
}
```

**Request Body:**
```json
{
  "firstName": "John",
  "lastName": "Doe",
  "email": "john.doe@example.com",
  "password": "SecurePass123!",
  "confirmPassword": "SecurePass123!"
}
```

**Expected Response:**
- Status Code: `201 Created`
- Response Body:
```json
{
  "success": true,
  "data": {
    "userId": "uuid",
    "email": "john.doe@example.com",
    "firstName": "John",
    "lastName": "Doe",
    "token": "jwt_token_here"
  },
  "message": "User registered successfully"
}
```

**Validations:**
- Response time < 2 seconds
- Token is JWT format
- Password not returned
- Email sent for verification

---

### TC-API-AUTH-002: User Registration - Duplicate Email

**Endpoint:** `POST /api/auth/register`  
**Priority:** High  
**Type:** Negative

**Request Body:**
```json
{
  "firstName": "Jane",
  "lastName": "Smith",
  "email": "existing@example.com",
  "password": "SecurePass123!",
  "confirmPassword": "SecurePass123!"
}
```

**Expected Response:**
- Status Code: `409 Conflict`
- Response Body:
```json
{
  "success": false,
  "message": "Email already registered",
  "errors": [
    {
      "field": "email",
      "message": "This email is already in use"
    }
  ]
}
```

---

### TC-API-AUTH-003: User Login - Valid Credentials

**Endpoint:** `POST /api/auth/login`  
**Priority:** Critical  
**Type:** Positive

**Request Body:**
```json
{
  "email": "john.doe@example.com",
  "password": "SecurePass123!"
}
```

**Expected Response:**
- Status Code: `200 OK`
- Response Body:
```json
{
  "success": true,
  "data": {
    "userId": "uuid",
    "email": "john.doe@example.com",
    "firstName": "John",
    "lastName": "Doe",
    "token": "jwt_token_here",
    "refreshToken": "refresh_token_here",
    "expiresIn": 86400
  },
  "message": "Login successful"
}
```

**Validations:**
- Token is valid JWT
- Expires timestamp reasonable
- Session created

---

### TC-API-AUTH-004: User Login - Invalid Credentials

**Endpoint:** `POST /api/auth/login`  
**Priority:** High  
**Type:** Negative

**Request Body:**
```json
{
  "email": "john.doe@example.com",
  "password": "WrongPassword123!"
}
```

**Expected Response:**
- Status Code: `401 Unauthorized`
- Response Body:
```json
{
  "success": false,
  "message": "Invalid email or password",
  "errors": []
}
```

**Security Check:**
- No indication which field is wrong (security best practice)
- No account enumeration possible

---

### TC-API-AUTH-005: Logout

**Endpoint:** `POST /api/auth/logout`  
**Priority:** High  
**Type:** Positive

**Request Headers:**
```json
{
  "Authorization": "Bearer {token}",
  "Content-Type": "application/json"
}
```

**Expected Response:**
- Status Code: `200 OK`
- Response Body:
```json
{
  "success": true,
  "message": "Logged out successfully"
}
```

**Validations:**
- Token invalidated
- Subsequent requests with token fail

---

## 2. Product API Test Cases

### TC-API-PROD-001: Get All Products

**Endpoint:** `GET /api/products`  
**Priority:** High  
**Type:** Positive

**Query Parameters:**
- `page=1`
- `limit=20`
- `sort=price_asc`

**Expected Response:**
- Status Code: `200 OK`
- Response Body:
```json
{
  "success": true,
  "data": {
    "products": [
      {
        "productId": "uuid",
        "name": "Product Name",
        "description": "Product description",
        "price": 29.99,
        "currency": "USD",
        "category": "Electronics",
        "imageUrl": "https://...",
        "stock": 100,
        "rating": 4.5,
        "reviewCount": 120
      }
    ],
    "pagination": {
      "currentPage": 1,
      "totalPages": 10,
      "totalItems": 200,
      "itemsPerPage": 20
    }
  }
}
```

**Validations:**
- Array of products returned
- Pagination data accurate
- All required fields present
- Data types correct

---

### TC-API-PROD-002: Get Product by ID

**Endpoint:** `GET /api/products/{productId}`  
**Priority:** High  
**Type:** Positive

**Expected Response:**
- Status Code: `200 OK`
- Response Body:
```json
{
  "success": true,
  "data": {
    "productId": "uuid",
    "name": "Product Name",
    "description": "Detailed description",
    "price": 29.99,
    "salePrice": 24.99,
    "currency": "USD",
    "category": "Electronics",
    "brand": "Brand Name",
    "images": [
      "https://image1.jpg",
      "https://image2.jpg"
    ],
    "stock": 100,
    "sku": "SKU-12345",
    "specifications": {
      "color": "Black",
      "size": "Medium",
      "weight": "1.5kg"
    },
    "rating": 4.5,
    "reviewCount": 120,
    "createdAt": "2025-01-01T00:00:00Z",
    "updatedAt": "2025-01-15T00:00:00Z"
  }
}
```

---

### TC-API-PROD-003: Get Non-Existent Product

**Endpoint:** `GET /api/products/{invalid_id}`  
**Priority:** Medium  
**Type:** Negative

**Expected Response:**
- Status Code: `404 Not Found`
- Response Body:
```json
{
  "success": false,
  "message": "Product not found",
  "errors": []
}
```

---

### TC-API-PROD-004: Create Product (Admin)

**Endpoint:** `POST /api/products`  
**Priority:** High  
**Type:** Positive

**Request Headers:**
```json
{
  "Authorization": "Bearer {admin_token}",
  "Content-Type": "application/json"
}
```

**Request Body:**
```json
{
  "name": "New Product",
  "description": "Product description",
  "price": 49.99,
  "category": "Electronics",
  "brand": "Brand Name",
  "stock": 50,
  "sku": "SKU-67890",
  "specifications": {
    "color": "White"
  }
}
```

**Expected Response:**
- Status Code: `201 Created`
- Response includes created product with generated ID
- Location header with product URL

---

### TC-API-PROD-005: Create Product - Unauthorized

**Endpoint:** `POST /api/products`  
**Priority:** High  
**Type:** Negative

**Request Headers:**
```json
{
  "Authorization": "Bearer {regular_user_token}",
  "Content-Type": "application/json"
}
```

**Expected Response:**
- Status Code: `403 Forbidden`
- Response Body:
```json
{
  "success": false,
  "message": "You do not have permission to perform this action",
  "errors": []
}
```

---

### TC-API-PROD-006: Update Product (Admin)

**Endpoint:** `PUT /api/products/{productId}`  
**Priority:** High  
**Type:** Positive

**Request Headers:**
```json
{
  "Authorization": "Bearer {admin_token}",
  "Content-Type": "application/json"
}
```

**Request Body:**
```json
{
  "price": 39.99,
  "stock": 75
}
```

**Expected Response:**
- Status Code: `200 OK`
- Response includes updated product
- Only specified fields updated

---

### TC-API-PROD-007: Delete Product (Admin)

**Endpoint:** `DELETE /api/products/{productId}`  
**Priority:** Medium  
**Type:** Positive

**Request Headers:**
```json
{
  "Authorization": "Bearer {admin_token}"
}
```

**Expected Response:**
- Status Code: `204 No Content`
- No response body

**Validations:**
- Product no longer accessible
- Related data handled appropriately

---

### TC-API-PROD-008: Search Products

**Endpoint:** `GET /api/products/search`  
**Priority:** High  
**Type:** Positive

**Query Parameters:**
- `q=laptop`
- `category=Electronics`
- `minPrice=500`
- `maxPrice=1500`

**Expected Response:**
- Status Code: `200 OK`
- Returns filtered products
- Relevance sorted

---

## 3. Cart API Test Cases

### TC-API-CART-001: Get Cart

**Endpoint:** `GET /api/cart`  
**Priority:** High  
**Type:** Positive

**Request Headers:**
```json
{
  "Authorization": "Bearer {token}"
}
```

**Expected Response:**
- Status Code: `200 OK`
- Response Body:
```json
{
  "success": true,
  "data": {
    "cartId": "uuid",
    "items": [
      {
        "itemId": "uuid",
        "productId": "uuid",
        "productName": "Product Name",
        "quantity": 2,
        "price": 29.99,
        "subtotal": 59.98,
        "imageUrl": "https://..."
      }
    ],
    "subtotal": 59.98,
    "tax": 5.40,
    "shipping": 0.00,
    "total": 65.38,
    "itemCount": 2
  }
}
```

---

### TC-API-CART-002: Add Item to Cart

**Endpoint:** `POST /api/cart/items`  
**Priority:** Critical  
**Type:** Positive

**Request Headers:**
```json
{
  "Authorization": "Bearer {token}",
  "Content-Type": "application/json"
}
```

**Request Body:**
```json
{
  "productId": "uuid",
  "quantity": 1
}
```

**Expected Response:**
- Status Code: `200 OK` or `201 Created`
- Response includes updated cart
- Item count increased

---

### TC-API-CART-003: Add Item - Exceeds Stock

**Endpoint:** `POST /api/cart/items`  
**Priority:** High  
**Type:** Negative

**Request Body:**
```json
{
  "productId": "uuid",
  "quantity": 999
}
```

**Expected Response:**
- Status Code: `400 Bad Request`
- Response Body:
```json
{
  "success": false,
  "message": "Requested quantity exceeds available stock",
  "errors": [
    {
      "field": "quantity",
      "message": "Only 50 items available in stock"
    }
  ]
}
```

---

### TC-API-CART-004: Update Cart Item Quantity

**Endpoint:** `PUT /api/cart/items/{itemId}`  
**Priority:** High  
**Type:** Positive

**Request Body:**
```json
{
  "quantity": 3
}
```

**Expected Response:**
- Status Code: `200 OK`
- Response includes updated cart
- Subtotal recalculated

---

### TC-API-CART-005: Remove Item from Cart

**Endpoint:** `DELETE /api/cart/items/{itemId}`  
**Priority:** High  
**Type:** Positive

**Request Headers:**
```json
{
  "Authorization": "Bearer {token}"
}
```

**Expected Response:**
- Status Code: `200 OK` or `204 No Content`
- Item removed from cart
- Cart totals updated

---

### TC-API-CART-006: Clear Cart

**Endpoint:** `DELETE /api/cart`  
**Priority:** Medium  
**Type:** Positive

**Expected Response:**
- Status Code: `200 OK`
- Response Body:
```json
{
  "success": true,
  "message": "Cart cleared successfully",
  "data": {
    "items": [],
    "total": 0.00
  }
}
```

---

## 4. Order API Test Cases

### TC-API-ORDER-001: Create Order

**Endpoint:** `POST /api/orders`  
**Priority:** Critical  
**Type:** Positive

**Request Headers:**
```json
{
  "Authorization": "Bearer {token}",
  "Content-Type": "application/json"
}
```

**Request Body:**
```json
{
  "shippingAddress": {
    "firstName": "John",
    "lastName": "Doe",
    "street": "123 Main St",
    "city": "New York",
    "state": "NY",
    "zipCode": "10001",
    "country": "USA",
    "phone": "+1234567890"
  },
  "billingAddress": {
    "same": true
  },
  "paymentMethod": "credit_card",
  "paymentDetails": {
    "token": "payment_token_from_gateway"
  }
}
```

**Expected Response:**
- Status Code: `201 Created`
- Response Body:
```json
{
  "success": true,
  "data": {
    "orderId": "uuid",
    "orderNumber": "ORD-2025-001",
    "status": "pending",
    "items": [...],
    "subtotal": 59.98,
    "tax": 5.40,
    "shipping": 10.00,
    "total": 75.38,
    "createdAt": "2025-12-28T12:00:00Z"
  },
  "message": "Order placed successfully"
}
```

**Validations:**
- Order created in database
- Cart cleared after order
- Inventory decremented
- Confirmation email sent

---

### TC-API-ORDER-002: Get Order by ID

**Endpoint:** `GET /api/orders/{orderId}`  
**Priority:** High  
**Type:** Positive

**Request Headers:**
```json
{
  "Authorization": "Bearer {token}"
}
```

**Expected Response:**
- Status Code: `200 OK`
- Response includes complete order details
- User can only access their own orders

---

### TC-API-ORDER-003: Get Order - Unauthorized Access

**Endpoint:** `GET /api/orders/{other_user_order_id}`  
**Priority:** High  
**Type:** Negative

**Expected Response:**
- Status Code: `403 Forbidden`
- Response Body:
```json
{
  "success": false,
  "message": "You do not have permission to view this order"
}
```

---

### TC-API-ORDER-004: Get User Orders

**Endpoint:** `GET /api/users/{userId}/orders`  
**Priority:** High  
**Type:** Positive

**Query Parameters:**
- `page=1`
- `limit=10`

**Expected Response:**
- Status Code: `200 OK`
- Response includes paginated list of user's orders
- Sorted by date (newest first)

---

### TC-API-ORDER-005: Cancel Order

**Endpoint:** `PUT /api/orders/{orderId}/cancel`  
**Priority:** High  
**Type:** Positive

**Request Headers:**
```json
{
  "Authorization": "Bearer {token}",
  "Content-Type": "application/json"
}
```

**Request Body:**
```json
{
  "reason": "Changed mind"
}
```

**Expected Response:**
- Status Code: `200 OK`
- Response Body:
```json
{
  "success": true,
  "data": {
    "orderId": "uuid",
    "status": "cancelled",
    "cancelledAt": "2025-12-28T13:00:00Z"
  },
  "message": "Order cancelled successfully"
}
```

**Validations:**
- Order status updated
- Inventory restored
- Refund initiated (if paid)

---

### TC-API-ORDER-006: Cancel Order - Already Shipped

**Endpoint:** `PUT /api/orders/{orderId}/cancel`  
**Priority:** High  
**Type:** Negative

**Expected Response:**
- Status Code: `400 Bad Request`
- Response Body:
```json
{
  "success": false,
  "message": "Cannot cancel order that has already been shipped"
}
```

---

## 5. Payment API Test Cases

### TC-API-PAY-001: Process Payment

**Endpoint:** `POST /api/payments/process`  
**Priority:** Critical  
**Type:** Positive

**Request Headers:**
```json
{
  "Authorization": "Bearer {token}",
  "Content-Type": "application/json"
}
```

**Request Body:**
```json
{
  "orderId": "uuid",
  "paymentMethod": "credit_card",
  "amount": 75.38,
  "currency": "USD",
  "paymentToken": "tok_visa"
}
```

**Expected Response:**
- Status Code: `200 OK`
- Response Body:
```json
{
  "success": true,
  "data": {
    "paymentId": "uuid",
    "transactionId": "txn_123456",
    "status": "completed",
    "amount": 75.38,
    "currency": "USD",
    "paymentMethod": "credit_card",
    "last4": "4242",
    "processedAt": "2025-12-28T12:00:00Z"
  },
  "message": "Payment processed successfully"
}
```

---

### TC-API-PAY-002: Payment Declined

**Endpoint:** `POST /api/payments/process`  
**Priority:** High  
**Type:** Negative

**Expected Response:**
- Status Code: `402 Payment Required`
- Response Body:
```json
{
  "success": false,
  "message": "Payment declined",
  "errors": [
    {
      "code": "card_declined",
      "message": "Your card was declined"
    }
  ]
}
```

---

### TC-API-PAY-003: Get Payment Status

**Endpoint:** `GET /api/payments/{paymentId}`  
**Priority:** Medium  
**Type:** Positive

**Expected Response:**
- Status Code: `200 OK`
- Response includes payment details and status

---

## Test Summary

| API Category | Total Test Cases | Priority |
|--------------|------------------|----------|
| Authentication | 5 | Critical |
| Products | 8 | High |
| Cart | 6 | Critical |
| Orders | 6 | Critical |
| Payments | 3 | Critical |

---

**Document Version**: 1.0  
**Last Updated**: December 2025
