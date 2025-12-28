# Checkout Process Test Cases

## Test Case Overview
This document contains detailed test cases for the checkout process in the e-commerce platform.

---

## TC-CP-001: Complete Checkout with Saved Address

**Priority**: Critical  
**Type**: Functional  
**Category**: Positive Testing

### Prerequisites
- User logged in
- Items in cart
- Saved address available

### Test Steps
1. Navigate to cart and click "Proceed to Checkout"
2. Select saved shipping address
3. Select shipping method
4. Review order summary
5. Enter payment details
6. Click "Place Order"

### Expected Results
- Checkout flow progresses smoothly
- Saved address populated correctly
- Order total calculated with shipping
- Payment processed successfully
- Order confirmation page displayed
- Confirmation email sent
- Order created in system

### Status
☐ Pass ☐ Fail ☐ Blocked ☐ Not Tested

---

## TC-CP-002: Checkout with New Shipping Address

**Priority**: High  
**Type**: Functional  
**Category**: Positive Testing

### Test Steps
1. Proceed to checkout
2. Select "Add New Address"
3. Fill in address form (name, street, city, state, ZIP, country)
4. Save address
5. Continue with checkout
6. Complete payment

### Expected Results
- New address form displays
- All required fields validated
- Address saved successfully
- Address used for current order
- Option to set as default address
- Checkout completes successfully

### Status
☐ Pass ☐ Fail ☐ Blocked ☐ Not Tested

---

## TC-CP-003: Select Shipping Method

**Priority**: High  
**Type**: Functional  
**Category**: Positive Testing

### Test Steps
1. Proceed to checkout
2. View available shipping methods
3. Select "Express Shipping"
4. Observe price update
5. Continue to payment

### Expected Results
- Multiple shipping options displayed
- Each option shows cost and delivery time
- Selected method highlighted
- Order total updated with shipping cost
- Estimated delivery date shown

### Status
☐ Pass ☐ Fail ☐ Blocked ☐ Not Tested

---

## TC-CP-004: Apply Promo Code During Checkout

**Priority**: Medium  
**Type**: Functional  
**Category**: Positive Testing

### Test Steps
1. Proceed to checkout
2. Enter promo code in checkout page
3. Click "Apply"
4. Review discount
5. Complete checkout

### Expected Results
- Promo code applied successfully
- Discount reflected in order total
- Discount breakdown visible
- Final price correct
- Order summary shows promo code used

### Status
☐ Pass ☐ Fail ☐ Blocked ☐ Not Tested

---

## TC-CP-005: Checkout with Credit Card Payment

**Priority**: Critical  
**Type**: Functional  
**Category**: Positive Testing

### Test Steps
1. Proceed to payment section
2. Select "Credit Card" payment method
3. Enter card number: 4111111111111111 (test)
4. Enter expiry: 12/25
5. Enter CVV: 123
6. Enter cardholder name
7. Submit payment

### Expected Results
- Payment form displays correctly
- Card validation works (Luhn algorithm)
- Secure connection indicator visible
- Payment processed
- Order confirmed
- No sensitive data stored in browser

### Status
☐ Pass ☐ Fail ☐ Blocked ☐ Not Tested

---

## TC-CP-006: Checkout with Insufficient Payment Details

**Priority**: High  
**Type**: Functional  
**Category**: Negative Testing

### Test Steps
1. Proceed to payment
2. Leave card number empty
3. Attempt to place order

### Expected Results
- Validation error: "Card number is required"
- Form not submitted
- Error field highlighted
- User remains on payment page
- Clear error messaging

### Status
☐ Pass ☐ Fail ☐ Blocked ☐ Not Tested

---

## TC-CP-007: Checkout with Invalid Card Number

**Priority**: High  
**Type**: Functional  
**Category**: Negative Testing

### Test Steps
1. Proceed to payment
2. Enter invalid card number: 1234567890123456
3. Complete other fields
4. Submit payment

### Expected Results
- Validation error: "Invalid card number"
- Payment not processed
- Card field highlighted
- Helpful error message
- Option to retry

### Status
☐ Pass ☐ Fail ☐ Blocked ☐ Not Tested

---

## TC-CP-008: Checkout with Expired Card

**Priority**: High  
**Type**: Functional  
**Category**: Negative Testing

### Test Steps
1. Proceed to payment
2. Enter valid card number
3. Enter past expiry date: 01/20
4. Submit payment

### Expected Results
- Validation error: "Card has expired"
- Payment not processed
- Alternative payment suggested
- Clear next steps provided

### Status
☐ Pass ☐ Fail ☐ Blocked ☐ Not Tested

---

## TC-CP-009: Order Summary Review Before Payment

**Priority**: High  
**Type**: Functional  
**Category**: Positive Testing

### Test Steps
1. Proceed through checkout
2. Reach order review page
3. Verify all order details

### Expected Results
- All items listed with quantities and prices
- Shipping address displayed correctly
- Shipping method shown
- Subtotal, tax, shipping, discount, and total visible
- Edit options available for address/items
- Promo code reflected
- Terms and conditions checkbox present

### Status
☐ Pass ☐ Fail ☐ Blocked ☐ Not Tested

---

## TC-CP-010: Guest Checkout Process

**Priority**: High  
**Type**: Functional  
**Category**: Positive Testing

### Test Steps
1. Add items to cart (not logged in)
2. Proceed to checkout
3. Select "Guest Checkout"
4. Enter email and shipping details
5. Complete payment
6. Place order

### Expected Results
- Guest checkout option available
- Email field for order confirmation
- All checkout steps accessible
- Order placed successfully
- Order confirmation sent to email
- Option to create account after order

### Status
☐ Pass ☐ Fail ☐ Blocked ☐ Not Tested

---

## TC-CP-011: Edit Cart from Checkout

**Priority**: Medium  
**Type**: Functional  
**Category**: Positive Testing

### Test Steps
1. Proceed to checkout
2. Click "Edit Cart" or "Back to Cart"
3. Modify cart items
4. Return to checkout

### Expected Results
- Can navigate back to cart
- Changes reflected in checkout
- Order total updated
- Checkout progress saved where possible
- Smooth navigation

### Status
☐ Pass ☐ Fail ☐ Blocked ☐ Not Tested

---

## TC-CP-012: Billing Address Same as Shipping

**Priority**: Medium  
**Type**: Functional  
**Category**: Positive Testing

### Test Steps
1. Proceed to checkout
2. Enter shipping address
3. Check "Billing address same as shipping"
4. Continue to payment

### Expected Results
- Billing address form hidden or auto-filled
- Same address used for billing
- One less step for user
- Address correctly associated with payment

### Status
☐ Pass ☐ Fail ☐ Blocked ☐ Not Tested

---

## TC-CP-013: Billing Address Different from Shipping

**Priority**: Medium  
**Type**: Functional  
**Category**: Positive Testing

### Test Steps
1. Proceed to checkout
2. Enter shipping address
3. Uncheck "Billing address same as shipping"
4. Enter different billing address
5. Complete checkout

### Expected Results
- Billing address form displayed
- Both addresses captured separately
- Billing address used for payment verification
- Shipping address used for delivery
- Order shows both addresses

### Status
☐ Pass ☐ Fail ☐ Blocked ☐ Not Tested

---

## TC-CP-014: Payment Processing Timeout

**Priority**: Medium  
**Type**: Functional  
**Category**: Error Handling

### Test Steps
1. Proceed to payment
2. Submit payment
3. Simulate slow payment gateway response

### Expected Results
- Loading indicator shown
- Timeout message after reasonable wait (30-60 seconds)
- Order not duplicated
- Clear instructions provided
- Option to retry or contact support

### Status
☐ Pass ☐ Fail ☐ Blocked ☐ Not Tested

---

## TC-CP-015: Order Confirmation Display

**Priority**: High  
**Type**: Functional  
**Category**: Positive Testing

### Test Steps
1. Complete checkout successfully
2. View order confirmation page

### Expected Results
- "Order Successful" message displayed
- Order number prominently shown
- Order summary visible
- Shipping address confirmed
- Estimated delivery date shown
- Download invoice option
- Continue shopping button
- Confirmation email notification

### Status
☐ Pass ☐ Fail ☐ Blocked ☐ Not Tested

---

## Test Summary

| Total Test Cases | Pass | Fail | Blocked | Not Tested |
|-----------------|------|------|---------|------------|
| 15 | | | | |

**Test Coverage**: Checkout Process Module  
**Test Execution Date**: ___________  
**Tested By**: ___________  
**Environment**: Staging  

---
**Document Version**: 1.0  
**Last Updated**: December 2025
