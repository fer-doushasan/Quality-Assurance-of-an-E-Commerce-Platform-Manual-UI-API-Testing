# Product Browsing Test Cases

## Test Case Overview
This document contains detailed test cases for product browsing functionality in the e-commerce platform.

---

## TC-PB-001: View Product Catalog

**Priority**: High  
**Type**: Functional  
**Category**: Positive Testing

### Prerequisites
- Navigate to homepage or products page
- Products available in database

### Test Steps
1. Navigate to products page
2. Observe product catalog display
3. Verify product grid/list layout
4. Check product information displayed

### Expected Results
- Products displayed in grid or list format
- Each product shows: image, name, price, rating
- Products loaded successfully
- Layout is organized and user-friendly
- Pagination controls visible if applicable

### Status
☐ Pass ☐ Fail ☐ Blocked ☐ Not Tested

---

## TC-PB-002: Filter Products by Category

**Priority**: High  
**Type**: Functional  
**Category**: Positive Testing

### Test Steps
1. Navigate to products page
2. Select a category from filter menu (e.g., "Electronics")
3. Observe filtered results

### Expected Results
- Only products from selected category displayed
- Product count updated
- Filter indicator shows active category
- Can clear filter to view all products

### Status
☐ Pass ☐ Fail ☐ Blocked ☐ Not Tested

---

## TC-PB-003: Search Products by Name

**Priority**: High  
**Type**: Functional  
**Category**: Positive Testing

### Test Steps
1. Navigate to products page
2. Enter product name in search box (e.g., "laptop")
3. Click search or press Enter
4. View search results

### Expected Results
- Relevant products displayed based on search term
- Search term highlighted in results (optional)
- Result count shown
- No results message if nothing matches

### Status
☐ Pass ☐ Fail ☐ Blocked ☐ Not Tested

---

## TC-PB-004: Sort Products by Price (Low to High)

**Priority**: Medium  
**Type**: Functional  
**Category**: Positive Testing

### Test Steps
1. Navigate to products page
2. Select "Price: Low to High" from sort dropdown
3. Observe product order

### Expected Results
- Products sorted by ascending price
- Cheapest product shown first
- Sort persists during browsing
- Sort indicator shows active selection

### Status
☐ Pass ☐ Fail ☐ Blocked ☐ Not Tested

---

## TC-PB-005: Sort Products by Price (High to Low)

**Priority**: Medium  
**Type**: Functional  
**Category**: Positive Testing

### Test Steps
1. Navigate to products page
2. Select "Price: High to Low" from sort dropdown
3. Observe product order

### Expected Results
- Products sorted by descending price
- Most expensive product shown first
- Sort maintained during navigation
- Clear visual indication of active sort

### Status
☐ Pass ☐ Fail ☐ Blocked ☐ Not Tested

---

## TC-PB-006: View Product Details

**Priority**: High  
**Type**: Functional  
**Category**: Positive Testing

### Test Steps
1. Navigate to products page
2. Click on a product card or image
3. View product details page

### Expected Results
- Product details page loads
- Displays: name, description, price, images, specifications
- Add to cart button visible
- Quantity selector available
- Breadcrumb navigation shown
- Related products suggested (optional)

### Status
☐ Pass ☐ Fail ☐ Blocked ☐ Not Tested

---

## TC-PB-007: Product Image Gallery

**Priority**: Medium  
**Type**: Functional  
**Category**: Positive Testing

### Test Steps
1. Navigate to product details page
2. Click on product thumbnail images
3. Use next/previous arrows if available
4. Click main image to enlarge

### Expected Results
- Main image updates when thumbnail clicked
- Image gallery navigation works smoothly
- Zoom or lightbox feature works (if available)
- All images load correctly
- Image quality is acceptable

### Status
☐ Pass ☐ Fail ☐ Blocked ☐ Not Tested

---

## TC-PB-008: Filter Products by Price Range

**Priority**: Medium  
**Type**: Functional  
**Category**: Positive Testing

### Test Steps
1. Navigate to products page
2. Set minimum price: $50
3. Set maximum price: $200
4. Apply price filter

### Expected Results
- Only products within price range displayed
- Price range indicator visible
- Filter can be cleared or adjusted
- Product count updates

### Status
☐ Pass ☐ Fail ☐ Blocked ☐ Not Tested

---

## TC-PB-009: Filter Products by Multiple Criteria

**Priority**: High  
**Type**: Functional  
**Category**: Positive Testing

### Test Steps
1. Navigate to products page
2. Select category: "Electronics"
3. Set price range: $100-$500
4. Select brand filter: "Samsung"
5. View filtered results

### Expected Results
- Products match all selected filters
- Each filter contributes to narrowing results
- Active filters clearly indicated
- Can remove individual filters
- Filter combination works correctly

### Status
☐ Pass ☐ Fail ☐ Blocked ☐ Not Tested

---

## TC-PB-010: Pagination - Navigate to Next Page

**Priority**: Medium  
**Type**: Functional  
**Category**: Positive Testing

### Test Steps
1. Navigate to products page (with multiple pages)
2. Click "Next" or page "2" button
3. Observe next page of products

### Expected Results
- Next set of products loaded
- Page indicator shows current page (2)
- URL updates with page parameter
- Previous button becomes enabled
- Product count consistent

### Status
☐ Pass ☐ Fail ☐ Blocked ☐ Not Tested

---

## TC-PB-011: Search with No Results

**Priority**: Medium  
**Type**: Functional  
**Category**: Negative Testing

### Test Steps
1. Navigate to products page
2. Enter search term unlikely to match: "xyzabc123"
3. Execute search

### Expected Results
- No results message displayed clearly
- Suggestions provided (search tips, popular products)
- Search term shown in message
- Option to clear search or browse all products
- No error message, just empty state

### Status
☐ Pass ☐ Fail ☐ Blocked ☐ Not Tested

---

## TC-PB-012: Out of Stock Product Display

**Priority**: Medium  
**Type**: Functional  
**Category**: Positive Testing

### Test Steps
1. Navigate to products page
2. Find out-of-stock product
3. View product details

### Expected Results
- "Out of Stock" badge visible on product card
- Add to cart button disabled or shows "Notify Me"
- Clear indication product unavailable
- Option to notify when back in stock
- Product still visible for browsing

### Status
☐ Pass ☐ Fail ☐ Blocked ☐ Not Tested

---

## TC-PB-013: Product Rating Display

**Priority**: Low  
**Type**: Functional  
**Category**: Positive Testing

### Test Steps
1. Navigate to products page
2. Observe product ratings
3. Click on a product with reviews
4. View detailed ratings

### Expected Results
- Star rating visible on product cards
- Number of reviews shown
- Average rating calculated correctly
- Detailed breakdown on product page
- Reviews readable and properly formatted

### Status
☐ Pass ☐ Fail ☐ Blocked ☐ Not Tested

---

## TC-PB-014: Quick View Product

**Priority**: Low  
**Type**: Functional  
**Category**: Positive Testing

### Test Steps
1. Navigate to products page
2. Hover over product card
3. Click "Quick View" button (if available)
4. View product modal/popup

### Expected Results
- Modal opens with product details
- Essential information displayed
- Add to cart from quick view works
- Close button functional
- Background dimmed/disabled

### Status
☐ Pass ☐ Fail ☐ Blocked ☐ Not Tested

---

## TC-PB-015: Clear All Filters

**Priority**: Medium  
**Type**: Functional  
**Category**: Positive Testing

### Test Steps
1. Navigate to products page
2. Apply multiple filters (category, price, brand)
3. Click "Clear All Filters" button
4. Observe results

### Expected Results
- All filters removed
- Full product catalog displayed
- Filter indicators cleared
- Product count shows total products
- Page resets to first page

### Status
☐ Pass ☐ Fail ☐ Blocked ☐ Not Tested

---

## Test Summary

| Total Test Cases | Pass | Fail | Blocked | Not Tested |
|-----------------|------|------|---------|------------|
| 15 | | | | |

**Test Coverage**: Product Browsing Module  
**Test Execution Date**: ___________  
**Tested By**: ___________  
**Environment**: Staging  

---
**Document Version**: 1.0  
**Last Updated**: December 2025
