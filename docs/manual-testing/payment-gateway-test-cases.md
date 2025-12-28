# Payment Gateway Test Cases

## Test Case Overview
This document contains detailed test cases for payment gateway integration in the e-commerce platform.

---

## TC-PG-001: Successful Credit Card Payment

**Priority**: Critical  
**Type**: Functional  
**Category**: Positive Testing

### Prerequisites
- Items in cart
- User at payment stage
- Test credit card available

### Test Steps
1. Select Credit Card payment method
2. Enter card details: 4242424242424242
3. Enter expiry: 12/25, CVV: 123
4. Click "Pay Now"
5. Wait for processing

### Expected Results
- Payment processed successfully
- Success message displayed
- Order status: Paid
- Transaction ID generated
- Payment confirmation email sent
- Funds authorization recorded

### Status
☐ Pass ☐ Fail ☐ Blocked ☐ Not Tested

---

## TC-PG-002: Credit Card Payment Declined

**Priority**: High  
**Type**: Functional  
**Category**: Negative Testing

### Test Steps
1. Select Credit Card payment method
2. Enter test card for decline: 4000000000000002
3. Submit payment

### Expected Results
- Payment declined message
- Error: "Your card was declined"
- Order not created or marked as failed
- User prompted to try different payment method
- No charge to card
- Cart preserved for retry

### Status
☐ Pass ☐ Fail ☐ Blocked ☐ Not Tested

---

## TC-PG-003: Insufficient Funds

**Priority**: High  
**Type**: Functional  
**Category**: Negative Testing

### Test Steps
1. Select Credit Card payment method
2. Use test card for insufficient funds
3. Submit payment

### Expected Results
- Payment failed message
- Error: "Insufficient funds"
- Transaction not completed
- Order not placed
- Suggestion to use different payment method

### Status
☐ Pass ☐ Fail ☐ Blocked ☐ Not Tested

---

## TC-PG-004: PayPal Payment Integration

**Priority**: High  
**Type**: Functional  
**Category**: Positive Testing

### Test Steps
1. Select PayPal payment method
2. Click "Pay with PayPal"
3. Redirected to PayPal
4. Login to PayPal sandbox account
5. Confirm payment
6. Return to merchant site

### Expected Results
- Redirect to PayPal smooth
- PayPal login works
- Payment details shown in PayPal
- Payment confirmed
- Return redirect successful
- Order placed successfully
- PayPal transaction ID recorded

### Status
☐ Pass ☐ Fail ☐ Blocked ☐ Not Tested

---

## TC-PG-005: PayPal Payment Cancellation

**Priority**: Medium  
**Type**: Functional  
**Category**: Negative Testing

### Test Steps
1. Select PayPal payment
2. Redirected to PayPal
3. Click "Cancel" on PayPal page
4. Return to merchant site

### Expected Results
- User returned to payment page
- Message: "Payment cancelled"
- Order not placed
- Cart preserved
- Option to try again or choose different method

### Status
☐ Pass ☐ Fail ☐ Blocked ☐ Not Tested

---

## TC-PG-006: Debit Card Payment

**Priority**: High  
**Type**: Functional  
**Category**: Positive Testing

### Test Steps
1. Select Debit Card payment method
2. Enter debit card details
3. Submit payment

### Expected Results
- Debit card accepted
- Payment processed like credit card
- Transaction completed
- Order confirmed
- Receipt generated

### Status
☐ Pass ☐ Fail ☐ Blocked ☐ Not Tested

---

## TC-PG-007: Save Card for Future Use

**Priority**: Medium  
**Type**: Functional  
**Category**: Positive Testing

### Test Steps
1. At payment page, enter new card details
2. Check "Save card for future purchases"
3. Complete payment

### Expected Results
- Card saved securely (tokenized)
- Option appears on next checkout
- CVV not stored (PCI compliance)
- Last 4 digits displayed for identification
- User can manage saved cards in profile

### Status
☐ Pass ☐ Fail ☐ Blocked ☐ Not Tested

---

## TC-PG-008: Use Saved Card for Payment

**Priority**: Medium  
**Type**: Functional  
**Category**: Positive Testing

### Test Steps
1. User with saved card proceeds to checkout
2. Select saved card (shows last 4 digits)
3. Enter CVV only
4. Submit payment

### Expected Results
- Saved card details auto-populated
- Only CVV required
- Payment processes faster
- Transaction successful
- Card remains saved after use

### Status
☐ Pass ☐ Fail ☐ Blocked ☐ Not Tested

---

## TC-PG-009: Remove Saved Card

**Priority**: Low  
**Type**: Functional  
**Category**: Positive Testing

### Test Steps
1. Navigate to "Saved Payment Methods" in profile
2. Click "Remove" on a saved card
3. Confirm removal

### Expected Results
- Card removed from account
- Confirmation message shown
- Card no longer appears in saved cards
- Cannot be used for future payments
- No impact on past orders

### Status
☐ Pass ☐ Fail ☐ Blocked ☐ Not Tested

---

## TC-PG-010: Payment Gateway Timeout

**Priority**: High  
**Type**: Functional  
**Category**: Error Handling

### Test Steps
1. Submit payment
2. Simulate gateway timeout
3. Observe system behavior

### Expected Results
- Timeout handled gracefully
- Error message: "Payment processing timed out"
- Order not duplicated
- User instructed to check email or order history
- Support contact information provided
- No double charging

### Status
☐ Pass ☐ Fail ☐ Blocked ☐ Not Tested

---

## TC-PG-011: 3D Secure Authentication

**Priority**: High  
**Type**: Functional  
**Category**: Positive Testing

### Test Steps
1. Use card requiring 3D Secure
2. Enter card details
3. Submit payment
4. Complete 3D Secure verification
5. Return to merchant

### Expected Results
- 3D Secure challenge presented
- Authentication iframe/redirect works
- Successful verification
- Payment completes after auth
- Order placed successfully
- Enhanced security applied

### Status
☐ Pass ☐ Fail ☐ Blocked ☐ Not Tested

---

## TC-PG-012: Failed 3D Secure Authentication

**Priority**: High  
**Type**: Functional  
**Category**: Negative Testing

### Test Steps
1. Use card requiring 3D Secure
2. Submit payment
3. Fail 3D Secure verification

### Expected Results
- Authentication failed message
- Payment not processed
- Order not created
- User returned to payment page
- Option to try different card

### Status
☐ Pass ☐ Fail ☐ Blocked ☐ Not Tested

---

## TC-PG-013: Mixed Currency Payment

**Priority**: Medium  
**Type**: Functional  
**Category**: Positive Testing

### Test Steps
1. Browse products in USD
2. Change currency to EUR
3. Add items to cart
4. Proceed to checkout
5. Complete payment

### Expected Results
- Currency converted correctly
- Exchange rate applied
- Payment processed in selected currency
- Order shows correct currency
- No currency mismatch errors

### Status
☐ Pass ☐ Fail ☐ Blocked ☐ Not Tested

---

## TC-PG-014: Refund Processing

**Priority**: Medium  
**Type**: Functional  
**Category**: Positive Testing

### Test Steps
1. Complete an order with payment
2. Request refund (admin or customer)
3. Process refund
4. Verify refund status

### Expected Results
- Refund initiated in payment gateway
- Refund status tracked
- Customer notified of refund
- Refund appears in payment method (3-5 days)
- Order status updated to "Refunded"

### Status
☐ Pass ☐ Fail ☐ Blocked ☐ Not Tested

---

## TC-PG-015: Payment Security - SSL/TLS

**Priority**: Critical  
**Type**: Security  
**Category**: Positive Testing

### Test Steps
1. Navigate to checkout page
2. Inspect browser security indicator
3. Verify HTTPS protocol
4. Check SSL certificate

### Expected Results
- Page loaded over HTTPS
- Valid SSL certificate
- Padlock icon in browser
- No mixed content warnings
- Secure connection throughout payment flow
- PCI DSS compliance maintained

### Status
☐ Pass ☐ Fail ☐ Blocked ☐ Not Tested

---

## Test Summary

| Total Test Cases | Pass | Fail | Blocked | Not Tested |
|-----------------|------|------|---------|------------|
| 15 | | | | |

**Test Coverage**: Payment Gateway Module  
**Test Execution Date**: ___________  
**Tested By**: ___________  
**Environment**: Staging  

---
**Document Version**: 1.0  
**Last Updated**: December 2025
