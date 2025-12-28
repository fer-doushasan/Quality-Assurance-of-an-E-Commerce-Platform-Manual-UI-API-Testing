# Shopping Cart Test Cases

## Test Case Overview
This document contains detailed test cases for shopping cart functionality in the e-commerce platform.

---

## TC-SC-001: Add Product to Empty Cart

**Priority**: Critical  
**Type**: Functional  
**Category**: Positive Testing

### Prerequisites
- User logged in (or guest checkout enabled)
- Empty shopping cart

### Test Steps
1. Navigate to product details page
2. Select quantity: 1
3. Click "Add to Cart" button
4. Observe cart update

### Expected Results
- Success message: "Product added to cart"
- Cart icon counter increases to 1
- Product appears in cart
- Cart total updated with product price
- Option to continue shopping or view cart

### Status
☐ Pass ☐ Fail ☐ Blocked ☐ Not Tested

---

## TC-SC-002: Add Multiple Products to Cart

**Priority**: High  
**Type**: Functional  
**Category**: Positive Testing

### Test Steps
1. Add first product to cart (Product A)
2. Navigate to different product (Product B)
3. Add second product to cart
4. View cart

### Expected Results
- Both products visible in cart
- Cart counter shows 2
- Each product listed separately
- Subtotals calculated for each item
- Total price is sum of both products

### Status
☐ Pass ☐ Fail ☐ Blocked ☐ Not Tested

---

## TC-SC-003: Add Same Product Multiple Times

**Priority**: High  
**Type**: Functional  
**Category**: Positive Testing

### Test Steps
1. Add product to cart (Quantity: 1)
2. Return to same product page
3. Add product to cart again (Quantity: 1)
4. View cart

### Expected Results
- Single cart item with quantity: 2
- NOT two separate line items
- Price multiplied by quantity
- Quantity can be edited from cart

### Status
☐ Pass ☐ Fail ☐ Blocked ☐ Not Tested

---

## TC-SC-004: Update Product Quantity in Cart

**Priority**: High  
**Type**: Functional  
**Category**: Positive Testing

### Test Steps
1. Add product to cart
2. Navigate to cart page
3. Change quantity from 1 to 3
4. Click update or wait for auto-update

### Expected Results
- Quantity updated to 3
- Line item total recalculated (price × 3)
- Cart total updated
- Update confirmation shown
- Stock availability checked

### Status
☐ Pass ☐ Fail ☐ Blocked ☐ Not Tested

---

## TC-SC-005: Remove Product from Cart

**Priority**: High  
**Type**: Functional  
**Category**: Positive Testing

### Test Steps
1. Add product to cart
2. Navigate to cart page
3. Click "Remove" or trash icon
4. Confirm removal if prompted

### Expected Results
- Product removed from cart
- Cart counter decreases
- Cart total updated
- Empty cart message if no items left
- Option to undo removal (optional)

### Status
☐ Pass ☐ Fail ☐ Blocked ☐ Not Tested

---

## TC-SC-006: Apply Valid Promo Code

**Priority**: High  
**Type**: Functional  
**Category**: Positive Testing

### Test Steps
1. Add products to cart
2. Navigate to cart page
3. Enter valid promo code: "SAVE10"
4. Click "Apply" button

### Expected Results
- Promo code accepted message
- Discount applied to cart total
- Discount amount shown separately
- Final price reflects discount
- Promo code details displayed (e.g., "10% off")

### Status
☐ Pass ☐ Fail ☐ Blocked ☐ Not Tested

---

## TC-SC-007: Apply Invalid Promo Code

**Priority**: Medium  
**Type**: Functional  
**Category**: Negative Testing

### Test Steps
1. Add products to cart
2. Navigate to cart page
3. Enter invalid promo code: "INVALID123"
4. Click "Apply" button

### Expected Results
- Error message: "Invalid promo code"
- No discount applied
- Original price maintained
- Promo code input cleared or highlighted
- Option to try different code

### Status
☐ Pass ☐ Fail ☐ Blocked ☐ Not Tested

---

## TC-SC-008: Apply Expired Promo Code

**Priority**: Medium  
**Type**: Functional  
**Category**: Negative Testing

### Test Steps
1. Add products to cart
2. Navigate to cart page
3. Enter expired promo code
4. Click "Apply" button

### Expected Results
- Error message: "This promo code has expired"
- No discount applied
- Expiration date shown (optional)
- Suggestion for valid codes (optional)

### Status
☐ Pass ☐ Fail ☐ Blocked ☐ Not Tested

---

## TC-SC-009: Cart Persistence After Logout/Login

**Priority**: High  
**Type**: Functional  
**Category**: Positive Testing

### Test Steps
1. Login to account
2. Add products to cart
3. Logout
4. Login again with same account
5. View cart

### Expected Results
- Cart items preserved
- Same products and quantities present
- Prices updated if changed
- Cart total maintained
- No data loss

### Status
☐ Pass ☐ Fail ☐ Blocked ☐ Not Tested

---

## TC-SC-010: Add Product Exceeding Stock Quantity

**Priority**: High  
**Type**: Functional  
**Category**: Negative Testing

### Test Steps
1. Navigate to product with limited stock (e.g., 5 available)
2. Attempt to add quantity: 10
3. Try to add to cart

### Expected Results
- Error message: "Only 5 items available in stock"
- Maximum available quantity indicated
- Quantity auto-adjusted to maximum (optional)
- Product not added with excessive quantity
- Stock limit enforced

### Status
☐ Pass ☐ Fail ☐ Blocked ☐ Not Tested

---

## TC-SC-011: View Cart Summary

**Priority**: Medium  
**Type**: Functional  
**Category**: Positive Testing

### Test Steps
1. Add multiple products to cart
2. Navigate to cart page
3. Review cart summary

### Expected Results
- All cart items listed with details
- Item count correct
- Subtotal for each item shown
- Cart subtotal displayed
- Tax calculation shown (if applicable)
- Shipping cost indicated or "calculated at checkout"
- Grand total displayed
- Proceed to checkout button visible

### Status
☐ Pass ☐ Fail ☐ Blocked ☐ Not Tested

---

## TC-SC-012: Mini Cart Display

**Priority**: Medium  
**Type**: Functional  
**Category**: Positive Testing

### Test Steps
1. Add product to cart
2. Click on cart icon in header
3. View mini cart dropdown/popup

### Expected Results
- Mini cart displays recent items
- Item count shown
- Cart total visible
- Quick access to cart or checkout
- View full cart option available

### Status
☐ Pass ☐ Fail ☐ Blocked ☐ Not Tested

---

## TC-SC-013: Empty Cart Functionality

**Priority**: Medium  
**Type**: Functional  
**Category**: Positive Testing

### Test Steps
1. Add multiple products to cart
2. Click "Clear Cart" or "Empty Cart" button
3. Confirm action if prompted

### Expected Results
- All items removed from cart
- Cart counter reset to 0
- Empty cart message displayed
- Suggestions to continue shopping
- Cart total shows $0

### Status
☐ Pass ☐ Fail ☐ Blocked ☐ Not Tested

---

## TC-SC-014: Update Quantity to Zero

**Priority**: Medium  
**Type**: Functional  
**Category**: Boundary Testing

### Test Steps
1. Add product to cart
2. Navigate to cart page
3. Change quantity to 0
4. Update cart

### Expected Results
- Product removed from cart (same as delete)
- OR error: "Quantity must be at least 1"
- Appropriate feedback provided
- Cart updated accordingly

### Status
☐ Pass ☐ Fail ☐ Blocked ☐ Not Tested

---

## TC-SC-015: Continue Shopping from Cart

**Priority**: Low  
**Type**: Functional  
**Category**: Positive Testing

### Test Steps
1. Add product to cart
2. View cart page
3. Click "Continue Shopping" button

### Expected Results
- Redirected to products page or previous page
- Cart preserved
- Can continue adding items
- Smooth navigation experience

### Status
☐ Pass ☐ Fail ☐ Blocked ☐ Not Tested

---

## Test Summary

| Total Test Cases | Pass | Fail | Blocked | Not Tested |
|-----------------|------|------|---------|------------|
| 15 | | | | |

**Test Coverage**: Shopping Cart Module  
**Test Execution Date**: ___________  
**Tested By**: ___________  
**Environment**: Staging  

---
**Document Version**: 1.0  
**Last Updated**: December 2025
