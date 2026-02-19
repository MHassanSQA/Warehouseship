# Stock Addition Feature - Regression Test Cases

## Test Documentation Information
- **Feature**: Stock Addition - AGRIS Warehouse Mobile App
- **Test Type**: Regression Testing
- **Platform**: iOS & Android Mobile Devices
- **Version**: As per documentation
- **Last Updated**: 2026-02-19

---

## Table of Contents
1. [Test Environment Setup](#test-environment-setup)
2. [Pre-requisites](#pre-requisites)
3. [Test Cases by Module](#test-cases-by-module)
4. [Integration Test Cases](#integration-test-cases)
5. [Performance Test Cases](#performance-test-cases)
6. [Security Test Cases](#security-test-cases)
7. [Test Data Requirements](#test-data-requirements)

---

## Test Environment Setup

### Required Test Environment
- Mobile devices: iOS (latest 2 versions) and Android (latest 2 versions)
- AGRIS ERP test environment with sample data
- AttachToo document management system (test environment)
- Network conditions: WiFi, 4G, 3G, Airplane mode
- Test user accounts: Warehouse PRO users

### Test Data Requirements
- Minimum 10 test vendors with various attributes
- Minimum 20 test items (10 with lot numbers, 10 without)
- Pre-configured Vendor ID Range options
- Valid transaction codes in AGRIS
- Test BOL numbers

---

## Pre-requisites

### Before Testing
- [ ] Warehouse PRO user credentials available
- [ ] AGRIS ERP test environment accessible
- [ ] AttachToo system configured
- [ ] Camera and gallery access permissions granted
- [ ] Barcode scanner functionality available
- [ ] Network connectivity verified

---

## Test Cases by Module

## Module 1: Initial Setup & Configuration

### TC-001: First Time User - Vendor ID Range Configuration Required
**Priority**: Critical | **Type**: Functional

**Preconditions**: 
- Fresh install or user has not configured Vendor ID Range
- User logged in as Warehouse PRO

**Test Steps**:
1. Launch application
2. Navigate to Stock Addition feature
3. Observe blocking message

**Expected Results**:
- User is blocked from proceeding
- Clear error message displayed: "Cannot do Stock Addition without going to Settings and selecting Vendor ID Range"
- Settings button/link available to navigate to configuration

**Test Data**: N/A

---

### TC-002: Configure Vendor ID Range - Valid Selection
**Priority**: Critical | **Type**: Functional

**Preconditions**: 
- User logged in as Warehouse PRO
- No Vendor ID Range configured

**Test Steps**:
1. Navigate to Settings
2. Locate "Vendor Name ID Type Range" option
3. Select valid ID type range from available options
4. Save settings
5. Navigate back to Stock Addition

**Expected Results**:
- Vendor ID Range options displayed
- Selection saved successfully
- Confirmation message shown
- Stock Addition feature now accessible
- Settings persist across app sessions

**Test Data**: Valid Vendor ID Range values

---

### TC-003: Access Control - Non-PRO User
**Priority**: Critical | **Type**: Security

**Preconditions**: 
- User logged in with non-PRO role

**Test Steps**:
1. Attempt to access Stock Addition feature

**Expected Results**:
- Feature is not visible/accessible
- Appropriate access denied message if attempted
- User redirected or feature hidden

**Test Data**: Non-PRO user credentials

---

## Module 2: BOL Photo Management

### TC-004: Capture Photo Using Camera
**Priority**: High | **Type**: Functional

**Preconditions**: 
- Stock Addition accessible
- Camera permission granted
- Device has working camera

**Test Steps**:
1. Start new Stock Addition
2. Tap "Camera" option
3. Device camera opens
4. Capture photo
5. Review captured photo

**Expected Results**:
- Camera opens successfully
- Photo captured clearly
- Photo preview displayed
- Options to Confirm, Delete, or Retake shown
- Photo added to BOL photo list (1/4)

**Test Data**: N/A

---

### TC-005: Select Photos from Gallery
**Priority**: High | **Type**: Functional

**Preconditions**: 
- Stock Addition accessible
- Gallery permission granted
- Test images available in gallery

**Test Steps**:
1. Start new Stock Addition
2. Tap "Gallery" option
3. Device gallery opens
4. Select 1 photo
5. Confirm selection

**Expected Results**:
- Gallery opens successfully
- Photos are selectable
- Selected photo preview shown
- Photo added to BOL photo list (1/4)
- Photo count updates

**Test Data**: Sample images in device gallery

---

### TC-006: Add Multiple Photos (Mixed Camera & Gallery)
**Priority**: High | **Type**: Functional

**Preconditions**: 
- Stock Addition accessible
- Both camera and gallery permissions granted

**Test Steps**:
1. Start new Stock Addition
2. Capture 2 photos using camera
3. Add 2 photos from gallery
4. Verify total count

**Expected Results**:
- All 4 photos successfully added
- Photo sources (camera/gallery) don't conflict
- All photos displayed in preview
- Counter shows 4/4

**Test Data**: 2+ sample images in gallery

---

### TC-007: Maximum Photo Limit Enforcement (4 Photos)
**Priority**: Critical | **Type**: Boundary

**Preconditions**: 
- Stock Addition accessible

**Test Steps**:
1. Start new Stock Addition
2. Add 4 photos (any combination)
3. Attempt to add 5th photo

**Expected Results**:
- First 4 photos added successfully
- Camera/Gallery options disabled after 4 photos
- Clear message: "Maximum 4 photos allowed"
- User cannot exceed limit
- Continue button remains enabled

**Test Data**: 5+ test images

---

### TC-008: Delete Photo and Add Replacement
**Priority**: High | **Type**: Functional

**Preconditions**: 
- At least 1 photo added

**Test Steps**:
1. Add 3 photos
2. Delete 1 photo using delete button
3. Add new photo to replace deleted one

**Expected Results**:
- Photo deleted successfully
- Counter decreases (3/4 → 2/4)
- Add photo options re-enabled
- New photo added successfully
- Counter updates correctly (3/4)

**Test Data**: Sample images

---

### TC-009: Delete All Photos
**Priority**: Medium | **Type**: Functional

**Preconditions**: 
- Multiple photos added

**Test Steps**:
1. Add 4 photos
2. Delete all photos one by one

**Expected Results**:
- Each photo deletes successfully
- Counter updates correctly (4→3→2→1→0)
- No photos remain
- Add photo options fully enabled
- User can still continue (photos optional per workflow)

**Test Data**: 4 test images

---

### TC-010: Continue Without Photos
**Priority**: Medium | **Type**: Functional

**Preconditions**: 
- Stock Addition screen with no photos

**Test Steps**:
1. Start new Stock Addition
2. Skip photo capture
3. Click Continue

**Expected Results**:
- User can proceed to vendor selection
- No validation error for missing photos
- Workflow continues normally

**Test Data**: N/A

---

## Module 3: Vendor Search & Selection

### TC-011: Search Vendor by Name
**Priority**: Critical | **Type**: Functional

**Preconditions**: 
- Vendor ID Range configured
- Test vendors exist in AGRIS

**Test Steps**:
1. Navigate to vendor search screen
2. Enter vendor name in search field
3. View search results

**Expected Results**:
- Search executes successfully
- Matching vendors displayed in list
- Vendor details shown (Name, ID, City, Phone)
- Partial match supported
- Results update dynamically as typing

**Test Data**: Vendor name: "ABC Company"

---

### TC-012: Search Vendor by Name ID
**Priority**: High | **Type**: Functional

**Preconditions**: 
- Vendor ID Range configured

**Test Steps**:
1. Navigate to vendor search screen
2. Enter vendor Name ID
3. View results

**Expected Results**:
- Exact match returned
- Vendor card displayed with full details
- Selectable

**Test Data**: Valid Vendor Name ID: "V001"

---

### TC-013: Search Vendor by City
**Priority**: High | **Type**: Functional

**Preconditions**: 
- Vendor ID Range configured

**Test Steps**:
1. Navigate to vendor search screen
2. Enter city name
3. View results

**Expected Results**:
- All vendors in that city displayed
- Multiple results if applicable
- Results sorted appropriately

**Test Data**: City: "New York"

---

### TC-014: Search Vendor by Phone Number
**Priority**: High | **Type**: Functional

**Preconditions**: 
- Vendor ID Range configured

**Test Steps**:
1. Navigate to vendor search screen
2. Enter phone number
3. View results

**Expected Results**:
- Matching vendor(s) displayed
- Phone number formatting handled correctly
- Partial phone number search supported

**Test Data**: Phone: "(555) 123-4567"

---

### TC-015: Select Vendor from List
**Priority**: Critical | **Type**: Functional

**Preconditions**: 
- Vendor search results displayed

**Test Steps**:
1. Search for vendor
2. Tap on vendor from results list
3. View selected vendor card

**Expected Results**:
- Vendor selected successfully
- Vendor card displays with full details
- "Change" button available
- "Continue" button enabled
- Remit To auto-populated (hidden from UI)

**Test Data**: Any valid vendor

---

### TC-016: Change Vendor Selection
**Priority**: High | **Type**: Functional

**Preconditions**: 
- Vendor already selected

**Test Steps**:
1. Select initial vendor
2. Click "Change" button
3. Search and select different vendor

**Expected Results**:
- Returns to vendor search screen
- Previous selection cleared
- New vendor search works
- New vendor selection replaces old one
- Transaction codes update based on new vendor

**Test Data**: 2 different vendors

---

### TC-017: Cancel Vendor Change
**Priority**: Medium | **Type**: Functional

**Preconditions**: 
- Vendor already selected

**Test Steps**:
1. Select initial vendor
2. Click "Change" button
3. Click "Cancel" or back button

**Expected Results**:
- Returns to selected vendor screen
- Original vendor selection retained
- No data lost

**Test Data**: Any valid vendor

---

### TC-018: Invalid Vendor Search
**Priority**: Medium | **Type**: Negative

**Preconditions**: 
- Vendor ID Range configured

**Test Steps**:
1. Navigate to vendor search
2. Enter non-existent vendor name

**Expected Results**:
- "No vendors found" message displayed
- Search field remains active
- User can retry search
- No error/crash

**Test Data**: "XXXNONEXISTENT999"

---

## Module 4: Item Search & Selection

### TC-019: Search Item Manually
**Priority**: High | **Type**: Functional

**Preconditions**: 
- Vendor selected
- Test items exist in system

**Test Steps**:
1. Navigate to item search screen
2. Enter item name or code
3. View search results
4. Select item from list

**Expected Results**:
- Search returns matching items
- Item details displayed (Name, Code, UOM)
- Item selectable
- Taken to quantity entry screen

**Test Data**: Item name: "Widget A"

---

### TC-020: Scan Item Barcode - Valid Item
**Priority**: Critical | **Type**: Functional

**Preconditions**: 
- Barcode scanner permission granted
- Valid barcode available

**Test Steps**:
1. Navigate to item search
2. Click "Scan Item" button
3. Camera/scanner opens
4. Scan valid product barcode

**Expected Results**:
- Scanner opens successfully
- Barcode detected and processed
- Item automatically identified
- Item details displayed
- Taken directly to quantity entry screen

**Test Data**: Valid product barcode

---

### TC-021: Scan Item Barcode - Invalid/Unknown Barcode
**Priority**: High | **Type**: Negative

**Preconditions**: 
- Barcode scanner available

**Test Steps**:
1. Navigate to item search
2. Click "Scan Item" button
3. Scan invalid or unknown barcode

**Expected Results**:
- Scanner processes barcode
- "Item not found" error message
- User returned to search screen
- Can retry scan or search manually

**Test Data**: Invalid barcode

---

### TC-022: Enter Item Quantity - Simple Item (No Lot Number)
**Priority**: Critical | **Type**: Functional

**Preconditions**: 
- Item selected (without lot number requirement)

**Test Steps**:
1. Select item without lot number
2. View quantity entry screen
3. Enter valid quantity
4. Review UOM display
5. Click Continue

**Expected Results**:
- Quantity field displayed and editable
- UOM shown correctly (e.g., "EA", "LB", "BOX")
- Numeric keyboard displayed
- Quantity accepts valid numbers
- Item added to list successfully

**Test Data**: Quantity: 100, UOM: EA

---

### TC-023: Enter Item Quantity - Zero or Negative
**Priority**: High | **Type**: Negative

**Preconditions**: 
- Item selected

**Test Steps**:
1. Select item
2. Enter quantity: 0
3. Attempt to continue

**Expected Results**:
- Validation error: "Quantity must be greater than 0"
- Cannot proceed
- Field highlighted in red

**Test Data**: Quantity: 0, -5

---

### TC-024: Enter Item with Lot Number - Select Existing Lot
**Priority**: Critical | **Type**: Functional

**Preconditions**: 
- Item requiring lot number selected
- Existing lot numbers available

**Test Steps**:
1. Select item with lot number requirement
2. View lot number screen
3. See "Select existing lot" option
4. Choose existing lot number from list
5. Enter quantity
6. Continue

**Expected Results**:
- Lot number requirement displayed
- Existing lots shown in dropdown/list
- Lot selection works correctly
- Lot number populated
- Quantity field enabled after lot selection
- Item added with lot number

**Test Data**: Existing Lot: "LOT2024-001"

---

### TC-025: Enter Item with Lot Number - Create New Lot
**Priority**: Critical | **Type**: Functional

**Preconditions**: 
- Item requiring lot number selected

**Test Steps**:
1. Select item with lot number requirement
2. Choose "Create new lot" option
3. Enter new lot number
4. Enter quantity
5. Continue

**Expected Results**:
- "Create new lot" option available
- Lot number field editable
- Validation for lot number format
- New lot accepted
- Item added with new lot number

**Test Data**: New Lot: "LOT2026-NEW001"

---

### TC-026: Item with Lot Number - Missing Lot Number
**Priority**: High | **Type**: Negative

**Preconditions**: 
- Item requiring lot number selected

**Test Steps**:
1. Select item requiring lot number
2. Skip lot number entry
3. Enter quantity
4. Attempt to continue

**Expected Results**:
- Validation error: "Lot number required for this item"
- Cannot proceed
- Lot number field highlighted
- Quantity entry disabled until lot selected

**Test Data**: N/A

---

### TC-027: Add Multiple Items
**Priority**: High | **Type**: Functional

**Preconditions**: 
- At least 1 item added

**Test Steps**:
1. Add first item successfully
2. On item list screen, click "Add Another Item"
3. Search and add second item
4. Repeat for third item

**Expected Results**:
- Each item added successfully
- Item list displays all items
- Each item shows: Name, Quantity, UOM, Lot# (if applicable)
- Can add multiple items without limit
- "Add Another Item" button always available

**Test Data**: 3 different items

---

### TC-028: Edit Item in List
**Priority**: High | **Type**: Functional

**Preconditions**: 
- Multiple items in list

**Test Steps**:
1. View item list
2. Click "Edit" on specific item
3. Modify quantity
4. Save changes

**Expected Results**:
- Edit screen opens with current values
- Quantity editable
- Changes saved successfully
- Item list updates with new values
- Other items unaffected

**Test Data**: Original Qty: 100, New Qty: 150

---

### TC-029: Delete Item from List
**Priority**: High | **Type**: Functional

**Preconditions**: 
- Multiple items in list

**Test Steps**:
1. View item list with 3+ items
2. Click "Delete" on second item
3. Confirm deletion

**Expected Results**:
- Confirmation prompt shown
- Item deleted after confirmation
- Remaining items still displayed
- Item count updated
- Can continue with remaining items

**Test Data**: Any item in list

---

### TC-030: Delete All Items
**Priority**: Medium | **Type**: Negative

**Preconditions**: 
- Items in list

**Test Steps**:
1. Delete all items from list one by one
2. Attempt to continue with empty list

**Expected Results**:
- All items deletable
- Warning shown: "At least one item required"
- Continue button disabled
- Must add item to proceed

**Test Data**: N/A

---

## Module 5: Transaction Codes

### TC-031: Transaction Codes - Auto-populated from Vendor
**Priority**: High | **Type**: Functional

**Preconditions**: 
- Vendor with transaction codes selected
- Items added

**Test Steps**:
1. Complete item entry
2. Proceed to Transaction Codes screen
3. View pre-filled transaction codes

**Expected Results**:
- Transaction codes screen displayed
- Codes auto-populated based on vendor
- Required fields marked with asterisk
- Optional fields clearly indicated
- Values fetched from AGRIS ERP

**Test Data**: Vendor with configured transaction codes

---

### TC-032: Transaction Codes - Required Field Validation
**Priority**: Critical | **Type**: Functional

**Preconditions**: 
- Transaction codes screen with required fields

**Test Steps**:
1. View transaction codes screen
2. Leave required field empty
3. Attempt to continue

**Expected Results**:
- Validation error displayed
- Required field highlighted in red
- Cannot proceed without completing required fields
- Error message: "Field [name] is required"

**Test Data**: N/A

---

### TC-033: Transaction Codes - Dropdown Suggestions
**Priority**: High | **Type**: Functional

**Preconditions**: 
- Transaction codes screen displayed

**Test Steps**:
1. Click on transaction code field
2. Start typing
3. View dropdown suggestions
4. Select from dropdown

**Expected Results**:
- Dropdown appears as typing
- Suggestions filtered based on input
- Only valid AGRIS values shown
- Selection populates field
- Invalid entries not allowed

**Test Data**: Valid transaction codes from AGRIS

---

### TC-034: Transaction Codes - Optional Fields
**Priority**: Medium | **Type**: Functional

**Preconditions**: 
- Transaction codes screen with optional fields

**Test Steps**:
1. Complete required fields only
2. Leave optional fields blank
3. Continue

**Expected Results**:
- Can proceed with optional fields empty
- No validation error
- Optional fields clearly marked
- Values saved correctly

**Test Data**: N/A

---

### TC-035: Skip Transaction Codes (Vendor without codes)
**Priority**: Medium | **Type**: Functional

**Preconditions**: 
- Vendor without transaction codes selected

**Test Steps**:
1. Select vendor with no transaction codes configured
2. Add items
3. Proceed through workflow

**Expected Results**:
- Transaction codes screen skipped
- Proceeds directly to BOL entry
- No error
- Workflow continues normally

**Test Data**: Vendor without transaction codes

---

## Module 6: BOL & Voucher Information

### TC-036: Enter BOL Number - Valid
**Priority**: Critical | **Type**: Functional

**Preconditions**: 
- Items added, transaction codes completed (if required)

**Test Steps**:
1. Navigate to BOL/Voucher information screen
2. Enter valid BOL number in required field
3. Continue

**Expected Results**:
- BOL field accepts alphanumeric input
- Field marked as required (asterisk/red border)
- Valid BOL accepted
- Can proceed to summary

**Test Data**: BOL#: "BOL-2026-001234"

---

### TC-037: BOL Number - Missing (Required Field)
**Priority**: Critical | **Type**: Negative

**Preconditions**: 
- BOL entry screen displayed

**Test Steps**:
1. Leave BOL number field empty
2. Attempt to continue

**Expected Results**:
- Validation error: "BOL number is required"
- Field highlighted
- Cannot proceed
- Focus returns to BOL field

**Test Data**: N/A

---

### TC-038: Enter Voucher Description - Optional
**Priority**: Medium | **Type**: Functional

**Preconditions**: 
- BOL entry screen displayed

**Test Steps**:
1. Enter BOL number
2. Enter voucher description
3. Continue

**Expected Results**:
- Description field accepts text
- Marked as optional
- Description saved with voucher
- Visible in summary

**Test Data**: Description: "Q1 2026 Stock Delivery"

---

### TC-039: Enter Remarks - Optional
**Priority**: Medium | **Type**: Functional

**Preconditions**: 
- BOL entry screen displayed

**Test Steps**:
1. Enter BOL number
2. Enter remarks/notes
3. Continue

**Expected Results**:
- Remarks field accepts text
- Multi-line text supported
- Marked as optional
- Remarks saved
- Visible in summary

**Test Data**: Remarks: "Urgent delivery - handle with care"

---

### TC-040: Skip Optional Fields (Description & Remarks)
**Priority**: Medium | **Type**: Functional

**Preconditions**: 
- BOL entry screen displayed

**Test Steps**:
1. Enter only BOL number (required)
2. Leave description and remarks empty
3. Continue

**Expected Results**:
- Can proceed with only BOL number
- No validation errors
- Optional fields remain empty in summary

**Test Data**: BOL#: "BOL-TEST-001"

---

## Module 7: Summary & Review

### TC-041: View Complete Summary
**Priority**: Critical | **Type**: Functional

**Preconditions**: 
- All required fields completed

**Test Steps**:
1. Complete entire workflow
2. View summary screen
3. Review all sections

**Expected Results**:
- Summary displays all information:
  - Vendor details (Name, ID)
  - BOL photos (all 4 or fewer)
  - Item list (all items with qty, UOM, lot#)
  - BOL number
  - Voucher description (if entered)
  - Remarks (if entered)
  - Transaction codes (if applicable)
- All data accurate
- Scrollable content
- Submit button at bottom

**Test Data**: Complete stock addition data

---

### TC-042: Summary - Scroll to Bottom Required
**Priority**: High | **Type**: Functional

**Preconditions**: 
- Summary screen displayed

**Test Steps**:
1. View summary screen
2. Observe Submit button location
3. Scroll to bottom

**Expected Results**:
- Submit button initially not visible
- User must scroll down to see Submit
- Submit button clearly visible after scroll
- Ensures user reviews all information

**Test Data**: N/A

---

### TC-043: Go Back from Summary - Edit Vendor
**Priority**: High | **Type**: Functional

**Preconditions**: 
- Summary screen displayed

**Test Steps**:
1. View summary
2. Click back/edit button
3. Navigate to vendor section
4. Change vendor
5. Return to summary

**Expected Results**:
- Can navigate back
- All sections accessible for editing
- Vendor change successful
- Transaction codes update for new vendor
- Summary reflects changes
- Data integrity maintained

**Test Data**: 2 different vendors

---

### TC-044: Go Back from Summary - Edit Items
**Priority**: High | **Type**: Functional

**Preconditions**: 
- Summary screen with multiple items

**Test Steps**:
1. View summary
2. Navigate back to items
3. Edit item quantity or delete item
4. Return to summary

**Expected Results**:
- Item modifications successful
- Summary updates correctly
- Changed quantity reflected
- Deleted item removed from summary

**Test Data**: Any item

---

### TC-045: Go Back from Summary - Edit BOL Number
**Priority**: Medium | **Type**: Functional

**Preconditions**: 
- Summary screen displayed

**Test Steps**:
1. View summary
2. Navigate back to BOL entry
3. Modify BOL number
4. Return to summary

**Expected Results**:
- BOL number editable
- New value saved
- Summary shows updated BOL number

**Test Data**: Original BOL: "BOL-001", New BOL: "BOL-002"

---

## Module 8: Submission & Completion

### TC-046: Submit Voucher - Successful Submission
**Priority**: Critical | **Type**: Functional

**Preconditions**: 
- Complete summary ready
- Network connectivity available
- AGRIS ERP accessible

**Test Steps**:
1. Review summary
2. Scroll to bottom
3. Click Submit button
4. Wait for processing

**Expected Results**:
- Submit button processes click
- Loading indicator shown
- Submission successful
- Success confirmation screen displayed
- Auto-generated Voucher number from AGRIS shown
- Voucher number format: "V-XXXXXX" or per AGRIS format
- Success message clear

**Test Data**: Complete valid stock addition

---

### TC-047: Voucher Number Generation
**Priority**: Critical | **Type**: Functional

**Preconditions**: 
- Successful submission

**Test Steps**:
1. Submit voucher
2. View confirmation screen
3. Note voucher number

**Expected Results**:
- Voucher number generated by AGRIS
- Number displayed prominently
- Number follows AGRIS format
- Number is unique
- User can copy/share number

**Test Data**: N/A

---

### TC-048: Email Document Option
**Priority**: Medium | **Type**: Functional

**Preconditions**: 
- Successful submission
- Email app available on device

**Test Steps**:
1. Complete submission
2. View confirmation screen
3. Click email option
4. Email app opens

**Expected Results**:
- Email option available
- Device email app opens
- Voucher details pre-populated in email body or attachment
- User can send to any email address

**Test Data**: Valid email address

---

### TC-049: Verify Data in AGRIS ERP
**Priority**: Critical | **Type**: Integration

**Preconditions**: 
- Voucher submitted successfully
- Access to AGRIS ERP

**Test Steps**:
1. Submit stock addition
2. Note voucher number
3. Log into AGRIS ERP
4. Search for voucher by number
5. Verify all data

**Expected Results**:
- Voucher exists in AGRIS
- Vendor information correct
- Items and quantities match
- BOL number correct
- Transaction codes saved
- Description and remarks present
- All data accurate
- Status shows as received/completed

**Test Data**: Submitted voucher number

---

### TC-050: Verify Photos in AttachToo
**Priority**: Critical | **Type**: Integration

**Preconditions**: 
- Voucher submitted with photos
- Access to AttachToo system

**Test Steps**:
1. Submit stock addition with 4 photos
2. Note voucher number
3. Access AttachToo system
4. Navigate to configured path (per AL configuration)
5. Search for voucher attachments

**Expected Results**:
- All 4 photos uploaded successfully
- Photos linked to voucher as sub-documents
- Photos viewable and downloadable
- Image quality preserved
- Correct document type assigned

**Test Data**: Voucher with 4 photos

---

## Module 9: Error Handling & Edge Cases

### TC-051: Submit Without Network Connection
**Priority**: Critical | **Type**: Negative

**Preconditions**: 
- Complete summary ready
- No network connectivity

**Test Steps**:
1. Disable WiFi and cellular data
2. Attempt to submit voucher

**Expected Results**:
- Network error detected
- Clear error message: "No network connection. Please check your internet and try again."
- Data saved locally (if offline mode supported)
- Submit button remains available for retry
- Data not lost

**Test Data**: N/A

---

### TC-052: Network Loss During Submission
**Priority**: High | **Type**: Negative

**Preconditions**: 
- Network available, submission in progress

**Test Steps**:
1. Click Submit
2. Disable network during submission process
3. Observe behavior

**Expected Results**:
- Timeout handling implemented
- Error message displayed
- User notified of failure
- Can retry submission
- No duplicate voucher created
- Data preserved for retry

**Test Data**: N/A

---

### TC-053: AGRIS ERP Unavailable
**Priority**: High | **Type**: Negative

**Preconditions**: 
- AGRIS ERP is down or unreachable

**Test Steps**:
1. Complete stock addition
2. Submit voucher

**Expected Results**:
- Error detected
- User-friendly message: "Unable to connect to AGRIS. Please try again later."
- Data saved locally for retry
- Technical error not shown to user
- Retry option available

**Test Data**: N/A

---

### TC-054: Large Photo Upload Failure
**Priority**: Medium | **Type**: Negative

**Preconditions**: 
- Very large photo files (>10MB each)

**Test Steps**:
1. Add 4 very large photos
2. Complete workflow
3. Submit

**Expected Results**:
- App handles large files
- Either: Photos compressed automatically, OR
- Warning shown before upload, OR
- Upload proceeds with progress indicator
- Timeout handling if needed
- User notified of upload status

**Test Data**: 4 photos > 10MB each

---

### TC-055: Special Characters in Text Fields
**Priority**: Medium | **Type**: Functional

**Preconditions**: 
- Any text entry screen

**Test Steps**:
1. Enter special characters in description/remarks: !@#$%^&*()
2. Enter Unicode characters: émojis, 中文
3. Submit

**Expected Results**:
- Special characters accepted
- Characters saved correctly
- Display correctly in summary
- Synchronize to AGRIS without corruption
- No SQL injection vulnerabilities

**Test Data**: "Test!@#$%^&*() émoji 😊 中文"

---

### TC-056: App Background/Foreground - Data Persistence
**Priority**: High | **Type**: Functional

**Preconditions**: 
- Stock addition in progress

**Test Steps**:
1. Add photos, vendor, items
2. Put app in background (home button)
3. Wait 5 minutes
4. Return to app

**Expected Results**:
- All entered data persists
- User returns to same screen
- No data loss
- Can continue workflow
- Session maintained

**Test Data**: Partial stock addition data

---

### TC-057: App Crash Recovery
**Priority**: High | **Type**: Functional

**Preconditions**: 
- Stock addition in progress

**Test Steps**:
1. Enter substantial data (photos, vendor, multiple items)
2. Force app crash/kill
3. Reopen app
4. Navigate to Stock Addition

**Expected Results**:
- Draft saved automatically OR
- User prompted to recover previous session
- Data recoverable
- Minimal data loss
- User can choose to continue or start fresh

**Test Data**: N/A

---

### TC-058: Duplicate Voucher Prevention
**Priority**: Critical | **Type**: Negative

**Preconditions**: 
- Successful voucher submitted

**Test Steps**:
1. Submit voucher successfully
2. Use browser back or app navigation to return to summary
3. Attempt to submit again

**Expected Results**:
- Submit button disabled after first submission OR
- User redirected away from summary OR
- Duplicate submission prevented
- Error message if attempted: "Voucher already submitted"
- No duplicate voucher created in AGRIS

**Test Data**: Any complete voucher

---

### TC-059: Concurrent User Sessions
**Priority**: Medium | **Type**: Functional

**Preconditions**: 
- Multiple PRO users with same device or different devices

**Test Steps**:
1. User A logs in and starts stock addition
2. User A logs out without completing
3. User B logs in on same device
4. User B starts stock addition

**Expected Results**:
- User sessions independent
- User A's draft not visible to User B
- No data crossover
- Each user's data isolated
- Proper session management

**Test Data**: 2 different user accounts

---

### TC-060: Maximum Quantity Values
**Priority**: Medium | **Type**: Boundary

**Preconditions**: 
- Item quantity entry screen

**Test Steps**:
1. Enter very large quantity: 999,999,999
2. Attempt to save

**Expected Results**:
- System accepts or validates against max limit
- If max limit exists, validation error shown
- No integer overflow
- Error message clear: "Maximum quantity is [limit]"

**Test Data**: Qty: 999999999

---

---

## Integration Test Cases

### INT-001: End-to-End Happy Path
**Priority**: Critical | **Type**: Integration

**Test Steps**:
1. Configure Vendor ID Range
2. Start Stock Addition
3. Capture 2 BOL photos
4. Search and select vendor
5. Scan 2 items with barcode
6. Add quantities (1 with lot number, 1 without)
7. Complete transaction codes
8. Enter BOL# and description
9. Review summary
10. Submit
11. Verify in AGRIS ERP
12. Verify photos in AttachToo

**Expected Results**:
- Complete workflow executes flawlessly
- Data flows correctly through all systems
- Voucher created in AGRIS with correct data
- Photos stored in AttachToo and linked
- Email confirmation works
- All integrations successful

**Test Data**: Complete valid dataset

---

### INT-002: Barcode to AGRIS Item Lookup
**Priority**: Critical | **Type**: Integration

**Test Steps**:
1. Scan product barcode
2. Verify item retrieved from AGRIS
3. Check item details accuracy

**Expected Results**:
- Barcode matches AGRIS item record
- Item details (name, UOM, lot requirement) accurate
- Response time < 2 seconds
- No timeout errors

**Test Data**: Valid AGRIS barcodes

---

### INT-003: Vendor Data Synchronization
**Priority**: High | **Type**: Integration

**Test Steps**:
1. Add new vendor in AGRIS
2. Configure with transaction codes
3. Search for vendor in mobile app
4. Verify data accuracy

**Expected Results**:
- New vendor appears in search
- All vendor attributes synchronized
- Transaction codes available
- Real-time or near-real-time sync

**Test Data**: Newly created vendor in AGRIS

---

---

## Performance Test Cases

### PERF-001: App Launch Time
**Priority**: Medium | **Type**: Performance

**Test Steps**:
1. Close app completely
2. Launch app
3. Measure time to ready state

**Expected Results**:
- App launches in < 3 seconds
- Splash screen appropriate duration
- No lag or freeze

**Test Data**: N/A

---

### PERF-002: Vendor Search Response Time
**Priority**: Medium | **Type**: Performance

**Test Steps**:
1. Enter search term
2. Measure time to display results

**Expected Results**:
- Results display in < 2 seconds
- Search feels responsive
- No lag on typing

**Test Data**: Various vendor search terms

---

### PERF-003: Photo Upload Performance
**Priority**: High | **Type**: Performance

**Test Steps**:
1. Add 4 photos (each ~5MB)
2. Complete workflow
3. Submit
4. Measure upload time

**Expected Results**:
- Upload completes in reasonable time (< 30 seconds on WiFi)
- Progress indicator shown
- User kept informed
- No timeout on normal connection

**Test Data**: 4 photos totaling ~20MB

---

### PERF-004: Large Item List Performance
**Priority**: Medium | **Type**: Performance

**Test Steps**:
1. Add 50+ items to stock addition
2. Navigate through item list
3. Submit

**Expected Results**:
- UI remains responsive
- Scrolling smooth
- Submission successful
- No memory issues
- List renders efficiently

**Test Data**: 50+ different items

---

---

## Security Test Cases

### SEC-001: User Authentication Required
**Priority**: Critical | **Type**: Security

**Test Steps**:
1. Logout from app
2. Attempt to access Stock Addition via deep link

**Expected Results**:
- Feature not accessible without authentication
- Redirected to login
- No data exposed
- Session properly terminated

**Test Data**: N/A

---

### SEC-002: Role-Based Access Control
**Priority**: Critical | **Type**: Security

**Test Steps**:
1. Login with various user roles
2. Attempt to access Stock Addition

**Expected Results**:
- Only Warehouse PRO users can access
- Other roles denied access
- Proper error messaging
- No workarounds possible

**Test Data**: Various user roles

---

### SEC-003: Data Encryption in Transit
**Priority**: Critical | **Type**: Security

**Test Steps**:
1. Submit stock addition
2. Monitor network traffic
3. Verify encryption

**Expected Results**:
- All API calls use HTTPS
- Data encrypted in transit
- No sensitive data in plain text
- SSL/TLS properly configured

**Test Data**: Any submission

---

### SEC-004: SQL Injection Prevention
**Priority**: Critical | **Type**: Security

**Test Steps**:
1. Enter SQL injection strings in text fields: `'; DROP TABLE vendors; --`
2. Submit

**Expected Results**:
- Input sanitized
- No SQL execution
- Proper parameterized queries
- Error handled gracefully

**Test Data**: Various SQL injection payloads

---

---

## Test Data Requirements

### Vendor Test Data
```
Vendor 1: ABC Supply Co.
  - Name ID: V001
  - City: New York
  - Phone: (555) 123-4567
  - Has transaction codes: Yes

Vendor 2: XYZ Distributors
  - Name ID: V002
  - City: Los Angeles
  - Phone: (555) 987-6543
  - Has transaction codes: No

Vendor 3: Test Vendor Inc.
  - Name ID: V003
  - City: Chicago
  - Phone: (555) 555-5555
  - Has transaction codes: Yes (required fields)
```

### Item Test Data
```
Item 1: Widget A
  - Code: ITEM001
  - UOM: EA
  - Requires Lot: No
  - Barcode: 123456789012

Item 2: Part B
  - Code: ITEM002
  - UOM: BOX
  - Requires Lot: Yes
  - Existing Lots: LOT-2024-001, LOT-2024-002
  - Barcode: 234567890123

Item 3: Material C
  - Code: ITEM003
  - UOM: LB
  - Requires Lot: Yes
  - No existing lots
  - Barcode: 345678901234
```

### Transaction Code Test Data
```
Code 1: DEPT (Department) - Required
  Valid values: DEPT01, DEPT02, DEPT03

Code 2: PROJ (Project) - Optional
  Valid values: PROJ-A, PROJ-B, PROJ-C

Code 3: COST-CTR (Cost Center) - Required
  Valid values: CC100, CC200, CC300
```

---

## Test Execution Summary Template

```
Test Cycle: [Date]
Environment: [Test/Staging]
Tester: [Name]

Total Test Cases: 60
Executed: __
Passed: __
Failed: __
Blocked: __
Skipped: __

Pass Rate: __%

Critical Issues Found: __
High Priority Issues: __
Medium Priority Issues: __
Low Priority Issues: __

Overall Status: [PASS/FAIL/BLOCKED]
```

---

## Defect Template

```
Defect ID: [AUTO]
Test Case: TC-XXX
Summary: [One line description]
Severity: [Critical/High/Medium/Low]
Priority: [P1/P2/P3/P4]

Steps to Reproduce:
1. 
2. 
3. 

Expected Result:
[What should happen]

Actual Result:
[What actually happened]

Environment:
- OS: [iOS 17.2 / Android 14]
- Device: [iPhone 14 / Samsung S23]
- App Version: [1.0.0]
- Build: [#123]

Screenshots/Logs:
[Attach]

Additional Notes:
[Any other relevant information]
```

---

## Test Sign-Off Criteria

Before marking Stock Addition feature as "Ready for Production":

- [ ] All Critical test cases (Priority: Critical) passed
- [ ] 95%+ of High priority test cases passed
- [ ] No open P1 (Critical) defects
- [ ] No open P2 (High) defects affecting core workflow
- [ ] Integration with AGRIS ERP verified
- [ ] Integration with AttachToo verified
- [ ] Performance benchmarks met
- [ ] Security tests passed
- [ ] User acceptance testing completed
- [ ] Regression testing completed on all supported devices
- [ ] Documentation updated
- [ ] Training materials prepared

---

**Document Version**: 1.0  
**Last Updated**: 2026-02-19  
**Prepared By**: QA Team  
**Status**: Ready for Test Execution
