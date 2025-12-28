# User Registration Test Cases

## Test Case Overview
This document contains detailed test cases for user registration functionality in the e-commerce platform.

---

## TC-UR-001: Successful User Registration with Valid Data

**Priority**: High  
**Type**: Functional  
**Category**: Positive Testing

### Prerequisites
- Navigate to registration page
- No existing account with test email

### Test Steps
1. Navigate to the registration page
2. Enter valid first name: "John"
3. Enter valid last name: "Doe"
4. Enter valid email: "john.doe@example.com"
5. Enter valid password: "SecurePass123!"
6. Confirm password: "SecurePass123!"
7. Check "I agree to Terms and Conditions" checkbox
8. Click "Register" button

### Expected Results
- Registration successful message displayed
- Verification email sent to registered email
- User redirected to verification pending page or dashboard
- User account created in the system

### Actual Results
_To be filled during test execution_

### Status
☐ Pass ☐ Fail ☐ Blocked ☐ Not Tested

### Comments
_Additional notes_

---

## TC-UR-002: Registration with Existing Email

**Priority**: High  
**Type**: Functional  
**Category**: Negative Testing

### Prerequisites
- Existing user account with email: "existing@example.com"
- Navigate to registration page

### Test Steps
1. Navigate to the registration page
2. Enter first name: "Jane"
3. Enter last name: "Smith"
4. Enter email: "existing@example.com" (already registered)
5. Enter password: "SecurePass123!"
6. Confirm password: "SecurePass123!"
7. Check terms and conditions checkbox
8. Click "Register" button

### Expected Results
- Error message displayed: "This email is already registered"
- Registration form remains on screen
- User is not registered
- Suggestion to login or reset password

### Actual Results
_To be filled during test execution_

### Status
☐ Pass ☐ Fail ☐ Blocked ☐ Not Tested

---

## TC-UR-003: Registration with Invalid Email Format

**Priority**: Medium  
**Type**: Functional  
**Category**: Negative Testing

### Prerequisites
- Navigate to registration page

### Test Steps
1. Navigate to the registration page
2. Enter first name: "Test"
3. Enter last name: "User"
4. Enter invalid email: "invalidemail.com" (missing @)
5. Enter password: "SecurePass123!"
6. Confirm password: "SecurePass123!"
7. Check terms and conditions checkbox
8. Attempt to click "Register" button

### Expected Results
- Inline validation error: "Please enter a valid email address"
- Email field highlighted in red
- Register button remains disabled or form not submitted
- User remains on registration page

### Actual Results
_To be filled during test execution_

### Status
☐ Pass ☐ Fail ☐ Blocked ☐ Not Tested

---

## TC-UR-004: Registration with Weak Password

**Priority**: High  
**Type**: Functional  
**Category**: Negative Testing

### Prerequisites
- Navigate to registration page

### Test Steps
1. Navigate to the registration page
2. Enter first name: "Test"
3. Enter last name: "User"
4. Enter valid email: "test@example.com"
5. Enter weak password: "123" (too short)
6. Confirm password: "123"
7. Check terms and conditions checkbox
8. Attempt to click "Register" button

### Expected Results
- Password strength indicator shows "Weak"
- Error message: "Password must be at least 8 characters with uppercase, lowercase, number, and special character"
- Password field highlighted
- Form not submitted

### Actual Results
_To be filled during test execution_

### Status
☐ Pass ☐ Fail ☐ Blocked ☐ Not Tested

---

## TC-UR-005: Registration with Mismatched Passwords

**Priority**: High  
**Type**: Functional  
**Category**: Negative Testing

### Prerequisites
- Navigate to registration page

### Test Steps
1. Navigate to the registration page
2. Enter first name: "Test"
3. Enter last name: "User"
4. Enter valid email: "test@example.com"
5. Enter password: "SecurePass123!"
6. Enter confirm password: "DifferentPass123!"
7. Check terms and conditions checkbox
8. Attempt to click "Register" button

### Expected Results
- Error message: "Passwords do not match"
- Confirm password field highlighted
- Form not submitted
- User remains on registration page

### Actual Results
_To be filled during test execution_

### Status
☐ Pass ☐ Fail ☐ Blocked ☐ Not Tested

---

## TC-UR-006: Registration without Accepting Terms and Conditions

**Priority**: High  
**Type**: Functional  
**Category**: Negative Testing

### Prerequisites
- Navigate to registration page

### Test Steps
1. Navigate to the registration page
2. Enter valid first name: "Test"
3. Enter valid last name: "User"
4. Enter valid email: "test@example.com"
5. Enter valid password: "SecurePass123!"
6. Confirm password: "SecurePass123!"
7. Leave "I agree to Terms and Conditions" checkbox unchecked
8. Attempt to click "Register" button

### Expected Results
- Error message: "You must accept the Terms and Conditions to register"
- Checkbox highlighted or error shown near it
- Form not submitted
- User remains on registration page

### Actual Results
_To be filled during test execution_

### Status
☐ Pass ☐ Fail ☐ Blocked ☐ Not Tested

---

## TC-UR-007: Registration with Missing Required Fields

**Priority**: High  
**Type**: Functional  
**Category**: Negative Testing

### Prerequisites
- Navigate to registration page

### Test Steps
1. Navigate to the registration page
2. Leave first name empty
3. Leave last name empty
4. Enter valid email: "test@example.com"
5. Leave password empty
6. Leave confirm password empty
7. Attempt to click "Register" button

### Expected Results
- Multiple validation errors displayed for each missing field
- Required fields highlighted in red
- Error messages: "First name is required", "Last name is required", "Password is required"
- Form not submitted

### Actual Results
_To be filled during test execution_

### Status
☐ Pass ☐ Fail ☐ Blocked ☐ Not Tested

---

## TC-UR-008: Registration with SQL Injection Attempt

**Priority**: Critical  
**Type**: Security  
**Category**: Negative Testing

### Prerequisites
- Navigate to registration page

### Test Steps
1. Navigate to the registration page
2. Enter first name: "Test"
3. Enter last name: "User"
4. Enter email with SQL injection: "test@example.com'; DROP TABLE users;--"
5. Enter password: "SecurePass123!"
6. Confirm password: "SecurePass123!"
7. Check terms and conditions checkbox
8. Click "Register" button

### Expected Results
- Input sanitized and treated as plain text
- Either validation error shown or email stored safely as string
- No SQL injection executed
- Database tables remain intact
- Error message about invalid email format (optional)

### Actual Results
_To be filled during test execution_

### Status
☐ Pass ☐ Fail ☐ Blocked ☐ Not Tested

---

## TC-UR-009: Registration with XSS Attack Attempt

**Priority**: Critical  
**Type**: Security  
**Category**: Negative Testing

### Prerequisites
- Navigate to registration page

### Test Steps
1. Navigate to the registration page
2. Enter first name: "<script>alert('XSS')</script>"
3. Enter last name: "User"
4. Enter valid email: "test@example.com"
5. Enter password: "SecurePass123!"
6. Confirm password: "SecurePass123!"
7. Check terms and conditions checkbox
8. Click "Register" button

### Expected Results
- Input sanitized and encoded
- Script not executed
- No alert popup shown
- Data stored safely with encoded special characters
- Profile displays sanitized text

### Actual Results
_To be filled during test execution_

### Status
☐ Pass ☐ Fail ☐ Blocked ☐ Not Tested

---

## TC-UR-010: Registration with Special Characters in Name

**Priority**: Medium  
**Type**: Functional  
**Category**: Boundary Testing

### Prerequisites
- Navigate to registration page

### Test Steps
1. Navigate to the registration page
2. Enter first name: "O'Brien"
3. Enter last name: "Müller-Schmidt"
4. Enter valid email: "test@example.com"
5. Enter password: "SecurePass123!"
6. Confirm password: "SecurePass123!"
7. Check terms and conditions checkbox
8. Click "Register" button

### Expected Results
- Registration successful
- Names with apostrophes, hyphens, and special characters accepted
- Data stored correctly
- Profile displays names correctly

### Actual Results
_To be filled during test execution_

### Status
☐ Pass ☐ Fail ☐ Blocked ☐ Not Tested

---

## TC-UR-011: Registration with Maximum Length Input

**Priority**: Low  
**Type**: Functional  
**Category**: Boundary Testing

### Prerequisites
- Navigate to registration page

### Test Steps
1. Navigate to the registration page
2. Enter first name: 50 characters (if max is 50)
3. Enter last name: 50 characters
4. Enter valid email: "test@example.com"
5. Enter password: "SecurePass123!"
6. Confirm password: "SecurePass123!"
7. Check terms and conditions checkbox
8. Click "Register" button

### Expected Results
- Registration successful if within limits
- Names accepted up to maximum allowed length
- No truncation without warning
- Data stored correctly

### Actual Results
_To be filled during test execution_

### Status
☐ Pass ☐ Fail ☐ Blocked ☐ Not Tested

---

## TC-UR-012: Email Verification Flow

**Priority**: High  
**Type**: Functional  
**Category**: Positive Testing

### Prerequisites
- Successfully registered user
- Verification email sent

### Test Steps
1. Complete registration process
2. Check email inbox for verification email
3. Open verification email
4. Click verification link
5. Observe redirect to application

### Expected Results
- Verification email received within 2 minutes
- Email contains valid verification link
- Clicking link verifies account
- Success message displayed: "Email verified successfully"
- User redirected to login or dashboard
- Account status changed to "Verified"

### Actual Results
_To be filled during test execution_

### Status
☐ Pass ☐ Fail ☐ Blocked ☐ Not Tested

---

## TC-UR-013: Registration with International Characters

**Priority**: Medium  
**Type**: Functional  
**Category**: Boundary Testing

### Prerequisites
- Navigate to registration page

### Test Steps
1. Navigate to the registration page
2. Enter first name: "李明" (Chinese characters)
3. Enter last name: "Αλέξανδρος" (Greek characters)
4. Enter valid email: "test@example.com"
5. Enter password: "SecurePass123!"
6. Confirm password: "SecurePass123!"
7. Check terms and conditions checkbox
8. Click "Register" button

### Expected Results
- Registration successful
- Unicode characters supported
- Names displayed correctly throughout application
- Data stored and retrieved correctly

### Actual Results
_To be filled during test execution_

### Status
☐ Pass ☐ Fail ☐ Blocked ☐ Not Tested

---

## TC-UR-014: Registration Form Field Validation on Blur

**Priority**: Low  
**Type**: Usability  
**Category**: Positive Testing

### Test Steps
1. Navigate to registration page
2. Click in email field
3. Enter invalid email
4. Tab out of field (blur event)
5. Observe validation

### Expected Results
- Validation error shown immediately after blur
- Error message appears below or near field
- Field highlighted to indicate error
- Real-time feedback improves UX

### Actual Results
_To be filled during test execution_

### Status
☐ Pass ☐ Fail ☐ Blocked ☐ Not Tested

---

## TC-UR-015: Password Visibility Toggle

**Priority**: Low  
**Type**: Usability  
**Category**: Positive Testing

### Test Steps
1. Navigate to registration page
2. Enter password in password field
3. Click "Show/Hide password" icon
4. Observe password visibility change
5. Click icon again to hide

### Expected Results
- Password shown in plain text when "Show" clicked
- Password masked when "Hide" clicked
- Icon changes to indicate current state
- Functionality works for both password and confirm password fields

### Actual Results
_To be filled during test execution_

### Status
☐ Pass ☐ Fail ☐ Blocked ☐ Not Tested

---

## Test Summary

| Total Test Cases | Pass | Fail | Blocked | Not Tested |
|-----------------|------|------|---------|------------|
| 15 | | | | |

**Test Coverage**: User Registration Module  
**Test Execution Date**: ___________  
**Tested By**: ___________  
**Environment**: Staging  

---
**Document Version**: 1.0  
**Last Updated**: December 2025
