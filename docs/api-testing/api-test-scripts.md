# API Test Scripts - Postman Collection Guide

## Overview
This document provides guidance on creating and organizing API test scripts using Postman for the e-commerce platform.

---

## 1. Postman Collection Structure

### Collection Organization
```
E-Commerce Platform API Tests
├── 1. Authentication
│   ├── Register User
│   ├── Login
│   ├── Logout
│   ├── Refresh Token
│   └── Forgot/Reset Password
├── 2. User Management
│   ├── Get Profile
│   ├── Update Profile
│   └── Change Password
├── 3. Products
│   ├── List Products
│   ├── Get Product
│   ├── Search Products
│   ├── Create Product (Admin)
│   ├── Update Product (Admin)
│   └── Delete Product (Admin)
├── 4. Shopping Cart
│   ├── Get Cart
│   ├── Add Item
│   ├── Update Item
│   ├── Remove Item
│   └── Clear Cart
├── 5. Orders
│   ├── Create Order
│   ├── Get Order
│   ├── List Orders
│   └── Cancel Order
└── 6. Payments
    ├── Process Payment
    └── Get Payment Status
```

---

## 2. Environment Variables

### Setup Environment Variables in Postman

**Development Environment:**
```json
{
  "baseUrl": "https://api-dev.ecommerce-platform.com/api/v1",
  "token": "",
  "refreshToken": "",
  "userId": "",
  "productId": "",
  "cartItemId": "",
  "orderId": "",
  "paymentId": ""
}
```

**Staging Environment:**
```json
{
  "baseUrl": "https://api-staging.ecommerce-platform.com/api/v1",
  "token": "",
  "refreshToken": "",
  "userId": "",
  "productId": "",
  "cartItemId": "",
  "orderId": "",
  "paymentId": ""
}
```

---

## 3. Pre-request Scripts

### Global Pre-request Script
Add to collection level to run before every request:

```javascript
// Log request for debugging
console.log(`Request: ${pm.request.method} ${pm.request.url}`);

// Add timestamp
pm.environment.set("timestamp", new Date().toISOString());

// Check if token exists and is not expired
const token = pm.environment.get("token");
if (token) {
    // Decode JWT and check expiration
    const tokenParts = token.split('.');
    if (tokenParts.length === 3) {
        const payload = JSON.parse(atob(tokenParts[1]));
        const expiresAt = payload.exp * 1000;
        const now = Date.now();
        
        if (now >= expiresAt) {
            console.warn("Token has expired. Please refresh.");
        }
    }
}
```

### Authentication Token Management
For endpoints requiring authentication:

```javascript
// Add token to header if it exists
const token = pm.environment.get("token");
if (token) {
    pm.request.headers.add({
        key: 'Authorization',
        value: `Bearer ${token}`
    });
}
```

---

## 4. Test Scripts Examples

### Register User Test
```javascript
// Test: Register User - POST /auth/register

pm.test("Status code is 201 Created", function () {
    pm.response.to.have.status(201);
});

pm.test("Response time is less than 2000ms", function () {
    pm.expect(pm.response.responseTime).to.be.below(2000);
});

pm.test("Response has required structure", function () {
    const jsonData = pm.response.json();
    pm.expect(jsonData).to.have.property('success', true);
    pm.expect(jsonData).to.have.property('data');
    pm.expect(jsonData.data).to.have.property('token');
    pm.expect(jsonData.data).to.have.property('userId');
});

pm.test("Token is JWT format", function () {
    const jsonData = pm.response.json();
    const token = jsonData.data.token;
    const parts = token.split('.');
    pm.expect(parts.length).to.equal(3);
});

pm.test("Password is not returned", function () {
    const jsonData = pm.response.json();
    pm.expect(jsonData.data).to.not.have.property('password');
});

// Save token and userId for subsequent requests
if (pm.response.code === 201) {
    const jsonData = pm.response.json();
    pm.environment.set("token", jsonData.data.token);
    pm.environment.set("userId", jsonData.data.userId);
    console.log("Token and userId saved to environment");
}
```

---

### Login Test
```javascript
// Test: Login - POST /auth/login

pm.test("Status code is 200 OK", function () {
    pm.response.to.have.status(200);
});

pm.test("Response contains authentication data", function () {
    const jsonData = pm.response.json();
    pm.expect(jsonData.data).to.have.property('token');
    pm.expect(jsonData.data).to.have.property('refreshToken');
    pm.expect(jsonData.data).to.have.property('expiresIn');
});

pm.test("Token is valid JWT", function () {
    const jsonData = pm.response.json();
    const token = jsonData.data.token;
    pm.expect(token).to.be.a('string');
    pm.expect(token.split('.')).to.have.lengthOf(3);
});

// Store tokens
const jsonData = pm.response.json();
pm.environment.set("token", jsonData.data.token);
pm.environment.set("refreshToken", jsonData.data.refreshToken);
```

---

### Get Products Test
```javascript
// Test: Get Products - GET /products

pm.test("Status code is 200 OK", function () {
    pm.response.to.have.status(200);
});

pm.test("Response contains products array", function () {
    const jsonData = pm.response.json();
    pm.expect(jsonData.data).to.have.property('products');
    pm.expect(jsonData.data.products).to.be.an('array');
});

pm.test("Products have required fields", function () {
    const jsonData = pm.response.json();
    const products = jsonData.data.products;
    
    if (products.length > 0) {
        const product = products[0];
        pm.expect(product).to.have.property('productId');
        pm.expect(product).to.have.property('name');
        pm.expect(product).to.have.property('price');
        pm.expect(product).to.have.property('category');
    }
});

pm.test("Pagination data is present", function () {
    const jsonData = pm.response.json();
    pm.expect(jsonData.data).to.have.property('pagination');
    pm.expect(jsonData.data.pagination).to.have.property('currentPage');
    pm.expect(jsonData.data.pagination).to.have.property('totalPages');
    pm.expect(jsonData.data.pagination).to.have.property('totalItems');
});

pm.test("Product prices are positive numbers", function () {
    const jsonData = pm.response.json();
    const products = jsonData.data.products;
    
    products.forEach(product => {
        pm.expect(product.price).to.be.a('number');
        pm.expect(product.price).to.be.above(0);
    });
});

// Save first product ID for later tests
if (pm.response.code === 200) {
    const jsonData = pm.response.json();
    if (jsonData.data.products.length > 0) {
        pm.environment.set("productId", jsonData.data.products[0].productId);
    }
}
```

---

### Get Product by ID Test
```javascript
// Test: Get Product - GET /products/:productId

pm.test("Status code is 200 OK", function () {
    pm.response.to.have.status(200);
});

pm.test("Product details are complete", function () {
    const jsonData = pm.response.json();
    const product = jsonData.data;
    
    pm.expect(product).to.have.property('productId');
    pm.expect(product).to.have.property('name');
    pm.expect(product).to.have.property('description');
    pm.expect(product).to.have.property('price');
    pm.expect(product).to.have.property('category');
    pm.expect(product).to.have.property('brand');
    pm.expect(product).to.have.property('images');
    pm.expect(product).to.have.property('stock');
});

pm.test("Images array is not empty", function () {
    const jsonData = pm.response.json();
    pm.expect(jsonData.data.images).to.be.an('array');
    pm.expect(jsonData.data.images.length).to.be.above(0);
});

pm.test("Stock is non-negative integer", function () {
    const jsonData = pm.response.json();
    pm.expect(jsonData.data.stock).to.be.a('number');
    pm.expect(jsonData.data.stock).to.be.at.least(0);
});
```

---

### Add to Cart Test
```javascript
// Test: Add to Cart - POST /cart/items

pm.test("Status code is 200 or 201", function () {
    pm.expect(pm.response.code).to.be.oneOf([200, 201]);
});

pm.test("Cart is updated", function () {
    const jsonData = pm.response.json();
    pm.expect(jsonData.data).to.have.property('items');
    pm.expect(jsonData.data.items).to.be.an('array');
    pm.expect(jsonData.data.items.length).to.be.above(0);
});

pm.test("Cart totals are calculated", function () {
    const jsonData = pm.response.json();
    pm.expect(jsonData.data).to.have.property('subtotal');
    pm.expect(jsonData.data).to.have.property('total');
    pm.expect(jsonData.data.total).to.be.a('number');
});

pm.test("Item count is correct", function () {
    const jsonData = pm.response.json();
    const itemCount = jsonData.data.itemCount;
    const actualCount = jsonData.data.items.reduce((sum, item) => sum + item.quantity, 0);
    pm.expect(itemCount).to.equal(actualCount);
});

// Save cart item ID
const jsonData = pm.response.json();
if (jsonData.data.items.length > 0) {
    pm.environment.set("cartItemId", jsonData.data.items[0].itemId);
}
```

---

### Create Order Test
```javascript
// Test: Create Order - POST /orders

pm.test("Status code is 201 Created", function () {
    pm.response.to.have.status(201);
});

pm.test("Order is created with order number", function () {
    const jsonData = pm.response.json();
    pm.expect(jsonData.data).to.have.property('orderId');
    pm.expect(jsonData.data).to.have.property('orderNumber');
    pm.expect(jsonData.data.orderNumber).to.match(/^ORD-/);
});

pm.test("Order has correct status", function () {
    const jsonData = pm.response.json();
    pm.expect(jsonData.data.status).to.be.oneOf(['pending', 'processing']);
});

pm.test("Order totals match cart", function () {
    const jsonData = pm.response.json();
    pm.expect(jsonData.data).to.have.property('total');
    pm.expect(jsonData.data).to.have.property('items');
});

pm.test("Shipping address is included", function () {
    const jsonData = pm.response.json();
    pm.expect(jsonData.data).to.have.property('shippingAddress');
});

// Save order ID
const jsonData = pm.response.json();
pm.environment.set("orderId", jsonData.data.orderId);
```

---

### Negative Test - Invalid Request
```javascript
// Test: Invalid Product ID - GET /products/:invalidId

pm.test("Status code is 404 Not Found", function () {
    pm.response.to.have.status(404);
});

pm.test("Error message is provided", function () {
    const jsonData = pm.response.json();
    pm.expect(jsonData.success).to.be.false;
    pm.expect(jsonData).to.have.property('message');
    pm.expect(jsonData.message).to.not.be.empty;
});
```

---

### Negative Test - Unauthorized Access
```javascript
// Test: Unauthorized Access - GET /users/me (no token)

pm.test("Status code is 401 Unauthorized", function () {
    pm.response.to.have.status(401);
});

pm.test("Error indicates authentication required", function () {
    const jsonData = pm.response.json();
    pm.expect(jsonData.success).to.be.false;
    pm.expect(jsonData.message).to.include.oneOf(['unauthorized', 'authentication', 'token']);
});
```

---

## 5. Collection Runner

### Running Tests Sequentially

1. **Prepare Collection:**
   - Ensure proper order of requests
   - Set up environment variables
   - Add delays if needed

2. **Configure Runner:**
   ```
   Collection: E-Commerce Platform API Tests
   Environment: Staging
   Iterations: 1
   Delay: 100ms (between requests)
   Data File: (optional for data-driven tests)
   ```

3. **Review Results:**
   - Check pass/fail status
   - Review response times
   - Inspect failed tests
   - Export results

---

## 6. Newman (CLI) Execution

### Install Newman
```bash
npm install -g newman
npm install -g newman-reporter-htmlextra
```

### Run Collection
```bash
newman run "E-Commerce-API-Tests.postman_collection.json" \
  -e "Staging.postman_environment.json" \
  --reporters cli,htmlextra \
  --reporter-htmlextra-export "test-results.html" \
  --delay-request 100
```

### With Data File (Data-Driven Testing)
```bash
newman run collection.json \
  -e environment.json \
  -d test-data.csv \
  --reporters cli,json \
  --reporter-json-export results.json
```

---

## 7. CI/CD Integration

### GitHub Actions Example
```yaml
name: API Tests

on: [push, pull_request]

jobs:
  api-tests:
    runs-on: ubuntu-latest
    
    steps:
      - uses: actions/checkout@v2
      
      - name: Install Newman
        run: npm install -g newman newman-reporter-htmlextra
      
      - name: Run API Tests
        run: |
          newman run postman/collection.json \
            -e postman/environment.json \
            --reporters cli,htmlextra \
            --reporter-htmlextra-export results/test-report.html
      
      - name: Upload Results
        uses: actions/upload-artifact@v2
        with:
          name: test-results
          path: results/
```

---

## 8. Best Practices

### Test Organization
- Group related endpoints together
- Use descriptive request names
- Add request descriptions
- Order tests logically (auth first, then dependent requests)

### Environment Management
- Use variables for all dynamic data
- Don't hardcode sensitive data
- Create separate environments for dev/staging/prod
- Use collection variables for collection-specific data

### Test Writing
- Write clear, specific test assertions
- Test both positive and negative scenarios
- Validate response structure, not just status codes
- Check response times
- Validate data types and formats

### Data Management
- Clean up test data after tests
- Use unique identifiers to avoid conflicts
- Reset environment between test runs
- Use random data generators for unique values

---

**Document Version**: 1.0  
**Last Updated**: December 2025
