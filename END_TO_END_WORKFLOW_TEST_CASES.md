# End-to-End Workflow Test Cases
## Stock Addition Feature - AGRIS Warehouse Mobile App

## Document Information
- **Feature**: Stock Addition - AGRIS Warehouse Mobile App
- **Test Type**: End-to-End (E2E) Workflow Testing
- **Platform**: iOS & Android Mobile Devices
- **Purpose**: Validate complete user journeys from start to finish
- **Last Updated**: 2026-02-19

---

## Table of Contents
1. [Overview](#overview)
2. [Test Environment Requirements](#test-environment-requirements)
3. [Happy Path Workflows](#happy-path-workflows)
4. [Alternative Path Workflows](#alternative-path-workflows)
5. [Error Recovery Workflows](#error-recovery-workflows)
6. [Edge Case Workflows](#edge-case-workflows)
7. [Multi-User & Multi-Device Workflows](#multi-user--multi-device-workflows)
8. [Performance & Load Workflows](#performance--load-workflows)
9. [Data Validation Workflows](#data-validation-workflows)

---

## Overview

End-to-end workflow tests validate complete user journeys through the Stock Addition feature, ensuring that all components work together seamlessly from initial setup through final submission and verification in backend systems.

### Key Differences from Unit/Integration Tests
- **Scope**: Complete user journeys, not isolated features
- **Duration**: Longer test execution time (5-15 minutes per workflow)
- **Dependencies**: Requires full system stack (mobile app, AGRIS ERP, AttachToo)
- **Validation**: Verifies business outcomes, not just technical functionality

### Success Criteria
Each workflow test must:
- Complete without system errors
- Produce correct business outcomes
- Maintain data integrity across all systems
- Provide appropriate user feedback at each step
- Handle state transitions correctly

---

## Test Environment Requirements

### Prerequisites
- **Mobile Devices**: 
  - iOS: iPhone 13+ with iOS 16+
  - Android: Samsung Galaxy S22+ with Android 13+
- **Backend Systems**:
  - AGRIS ERP test environment (fully functional)
  - AttachToo document management system (configured)
  - Network: Stable WiFi connection (primary), 4G/LTE (for mobile tests)
- **Test Data**:
  - 10+ test vendors with various configurations
  - 50+ test items (mix of simple and lot-tracked items)
  - Valid transaction codes
  - Test BOL numbers
  - Sample product barcodes
- **User Accounts**:
  - Warehouse PRO users (minimum 2 accounts)
  - Non-PRO user (for access control testing)

### Test Data Setup Scripts
Before running E2E tests, ensure:
1. Test database is reset to known state
2. Test vendors are loaded
3. Test items are available in AGRIS
4. Camera and gallery permissions are granted
5. Barcode scanner is functional

---

## Happy Path Workflows

### E2E-WF-001: First-Time User Complete Setup and Stock Addition
**Priority**: Critical | **Duration**: ~10-12 minutes

**Business Scenario**: A new warehouse staff member uses the Stock Addition feature for the first time, completing full setup and their first stock addition.

**Preconditions**:
- Fresh app install or cleared app data
- User logged in as Warehouse PRO
- No Vendor ID Range configured
- AGRIS ERP and AttachToo systems operational
- Device camera and gallery accessible

**Complete Workflow Steps**:

1. **Launch & Initial Block (2 min)**
   - Launch AGRIS Warehouse Mobile App
   - Navigate to Stock Addition feature
   - **Verify**: Blocking message displayed: "Cannot do Stock Addition without going to Settings and selecting Vendor ID Range"
   - **Verify**: Settings button is available and highlighted

2. **Configure Settings (1 min)**
   - Tap Settings button
   - Navigate to "Vendor Name ID Type Range" option
   - Select "Standard Range (001-999)" from dropdown
   - Save configuration
   - **Verify**: Success message: "Vendor ID Range saved successfully"
   - Navigate back to Stock Addition

3. **Capture BOL Photos (2 min)**
   - **Verify**: Stock Addition screen now accessible
   - Tap "Add Photo" button
   - Select "Take Photo" option
   - Capture photo of BOL document using camera
   - **Verify**: Photo thumbnail appears in gallery
   - Tap "Add Photo" again
   - Select "Choose from Gallery"
   - Select existing photo from gallery
   - **Verify**: Two photos now displayed
   - **Verify**: Photo counter shows "2/4"

4. **Search and Select Vendor (1.5 min)**
   - Tap "Continue" to proceed to vendor selection
   - Enter "Acme Corp" in vendor search field
   - **Verify**: Search results appear within 2 seconds
   - Select "Acme Corporation - Chicago" from results list
   - **Verify**: Vendor details displayed (Name, City, Phone)
   - **Verify**: "Vendor Selected" confirmation shown
   - Tap "Continue"

5. **Add First Item with Lot Number (2 min)**
   - On Item Entry screen, tap "Scan Barcode"
   - Scan barcode "7891234567890"
   - **Verify**: Item details auto-populate:
     - Item Name: "Premium Wheat Flour"
     - UOM: "50 LB BAG"
     - Lot Number Required: Yes
   - Enter quantity: "100"
   - Tap "Lot Number" field
   - Select "Create New Lot"
   - Enter new lot number: "LOT2026-02-19A"
   - **Verify**: Lot number validated and accepted
   - Tap "Add Item"
   - **Verify**: Item added to list with green checkmark

6. **Add Second Item without Lot Number (1.5 min)**
   - Tap "Add Another Item"
   - Use manual search: Enter "Sugar"
   - Select "Granulated Sugar" from results
   - **Verify**: Item details display (no lot number required)
   - Enter quantity: "50"
   - Tap "Add Item"
   - **Verify**: Two items now in list
   - Tap "Continue to Next Step"

7. **Complete Transaction Codes (1 min)**
   - **Verify**: Transaction codes auto-populated based on vendor
   - Review pre-filled fields:
     - Location Code: "WH-01"
     - Department: "Receiving"
   - **Verify**: All required fields are filled
   - Tap "Continue"

8. **Enter BOL Information (1 min)**
   - Enter BOL Number: "BOL-2026-001234"
   - Enter Voucher Description: "Q1 2026 Supplier Delivery - Acme Corp"
   - Enter Remarks: "First stock addition via mobile app"
   - **Verify**: BOL number field marked as required (red asterisk)
   - Tap "Continue to Summary"

9. **Review Summary (1 min)**
   - **Verify**: Summary displays all entered information:
     - 2 BOL photos with thumbnails
     - Vendor: Acme Corporation
     - 2 items with quantities and details
     - Transaction codes
     - BOL#: BOL-2026-001234
     - Description and remarks
   - Scroll to bottom
   - **Verify**: "Submit" button becomes enabled after scrolling
   - Tap "Submit Voucher"

10. **Submission & Confirmation (1 min)**
    - **Verify**: Loading indicator appears
    - **Verify**: Progress message: "Uploading photos..."
    - **Verify**: Progress message: "Creating voucher in AGRIS..."
    - **Verify**: Success screen displays with:
      - Green checkmark animation
      - Voucher Number: "VCH-2026-0001234"
      - Message: "Stock Addition completed successfully"
      - Option to "Email Document"
      - Option to "Start New Stock Addition"

11. **Backend Verification (2 min)**
    - Open AGRIS ERP web interface
    - Navigate to Vouchers > Receiving Vouchers
    - Search for voucher "VCH-2026-0001234"
    - **Verify**: Voucher exists with correct data:
      - Vendor: Acme Corporation
      - 2 line items with correct quantities
      - BOL number: BOL-2026-001234
      - Status: Submitted
    - Open AttachToo system
    - Search for document by voucher number
    - **Verify**: 2 photos attached as sub-documents
    - **Verify**: Photos are viewable and correct

**Expected Results**:
- ✅ Complete workflow executes without errors
- ✅ All data captured correctly at each step
- ✅ Voucher created in AGRIS with accurate information
- ✅ Photos uploaded to AttachToo and linked correctly
- ✅ User receives clear feedback at every step
- ✅ Settings persist for future use
- ✅ No data loss or corruption
- ✅ Total workflow time: Under 15 minutes

**Test Data**:
- Vendor ID Range: "Standard Range (001-999)"
- Vendor: "Acme Corporation - Chicago"
- Item 1: Barcode "7891234567890", Qty: 100, Lot: "LOT2026-02-19A"
- Item 2: "Granulated Sugar", Qty: 50, No lot
- BOL#: "BOL-2026-001234"
- Transaction Codes: Pre-configured for Acme Corp

---

### E2E-WF-002: Experienced User - Quick Stock Addition (Standard Flow)
**Priority**: Critical | **Duration**: ~6-8 minutes

**Business Scenario**: An experienced warehouse operator performs a routine stock addition with familiar vendor and items.

**Preconditions**:
- User has Vendor ID Range already configured
- User is familiar with the workflow
- Frequent vendor and items are recent/favorited
- Device permissions already granted

**Complete Workflow Steps**:

1. **Quick Launch (30 sec)**
   - Open app (already logged in)
   - Navigate directly to Stock Addition
   - **Verify**: No blocking messages, direct access

2. **Fast Photo Capture (1 min)**
   - Capture 1 BOL photo using camera
   - **Verify**: Quick capture mode, minimal UI
   - Continue immediately

3. **Quick Vendor Selection (1 min)**
   - Start typing vendor name "Sysco"
   - **Verify**: Auto-complete suggestions appear
   - Select first match from dropdown (no need to complete typing)
   - **Verify**: Recently used vendors appear at top
   - Tap vendor and proceed

4. **Rapid Item Entry (2 min)**
   - Scan barcode for Item 1
   - Enter quantity: "200" (no lot number required)
   - Tap "Add & Scan Next" (quick action button)
   - Scan barcode for Item 2
   - Enter quantity: "150"
   - Tap "Add & Scan Next"
   - Scan barcode for Item 3
   - Enter quantity: "75"
   - Tap "Done"
   - **Verify**: 3 items added in rapid succession

5. **Auto-Complete Transaction Codes (30 sec)**
   - **Verify**: All codes pre-filled from vendor defaults
   - Quick review (no edits needed)
   - Tap "Continue"

6. **Minimal BOL Entry (1 min)**
   - Enter BOL#: "SYS-2026-5678"
   - Skip optional description and remarks
   - Tap "Continue"

7. **Quick Summary Review (30 sec)**
   - Quick scroll through summary
   - **Verify**: All items present
   - Tap "Submit" immediately

8. **Fast Submission (30 sec)**
   - **Verify**: Submission completes quickly
   - Voucher number displayed
   - Tap "Start New Stock Addition" for next delivery

**Expected Results**:
- ✅ Experienced user completes workflow in under 8 minutes
- ✅ Auto-complete features reduce data entry
- ✅ Recently used data prioritized in searches
- ✅ Quick action buttons streamline multi-item entry
- ✅ Can immediately start next stock addition
- ✅ No unnecessary steps or confirmations

**Test Data**:
- Vendor: "Sysco Foods - Chicago"
- Items: 3 items via barcode scan (no lot numbers)
- BOL#: "SYS-2026-5678"
- Minimal data entry approach

---

### E2E-WF-003: Complex Stock Addition with Multiple Lot Numbers
**Priority**: High | **Duration**: ~12-15 minutes

**Business Scenario**: Receiving multiple lot-tracked items from pharmaceutical supplier, requiring careful lot number management.

**Preconditions**:
- Vendor ID Range configured
- Pharmaceutical vendor with strict lot tracking requirements
- Multiple items requiring lot numbers

**Complete Workflow Steps**:

1. **Setup (1 min)**
   - Launch Stock Addition
   - Capture 3 BOL photos (detailed documentation required)
   - **Verify**: All 3 photos captured successfully

2. **Select Pharmaceutical Vendor (1 min)**
   - Search for "PharmaSupply Inc"
   - Select vendor
   - **Verify**: Vendor requires enhanced transaction codes
   - Continue

3. **Add Item 1 with Existing Lot (2 min)**
   - Scan pharmaceutical item barcode
   - **Verify**: Item name: "Acetaminophen 500mg"
   - Enter quantity: "5000" (5000 tablets)
   - **Verify**: Lot number field becomes required
   - Tap "Select Existing Lot"
   - **Verify**: List of existing lots for this item displayed:
     - LOT-2025-12-001 (Exp: 12/2027)
     - LOT-2026-01-002 (Exp: 01/2028)
   - Select "LOT-2026-01-002"
   - **Verify**: Expiration date auto-populated
   - Tap "Add Item"

4. **Add Item 2 with New Lot (2.5 min)**
   - Scan second pharmaceutical item
   - **Verify**: Item name: "Ibuprofen 200mg"
   - Enter quantity: "10000"
   - Tap "Create New Lot"
   - Enter new lot number: "LOT-2026-02-NEW-A"
   - Enter expiration date: "02/2028"
   - Enter manufacturer lot code: "MFG-12345"
   - **Verify**: All lot fields validated
   - Tap "Add Item"

5. **Add Item 3 with Multiple Lots (3 min)**
   - Scan third item
   - **Verify**: Item name: "Aspirin 81mg"
   - Need to add 15000 tablets from 2 different lots
   - Enter quantity: "7500"
   - Select existing lot: "LOT-2025-11-001"
   - Tap "Add Item"
   - **Verify**: Item added to list
   - Tap "Add Another Item"
   - Scan same item again (same barcode)
   - **Verify**: System recognizes duplicate item, allows for different lot
   - Enter quantity: "7500"
   - Create new lot: "LOT-2026-02-NEW-B"
   - Enter expiration: "03/2028"
   - Tap "Add Item"
   - **Verify**: Same item appears twice in list with different lots

6. **Review Item List (1 min)**
   - **Verify**: Item list shows:
     - Acetaminophen 500mg - 5000 tablets - LOT-2026-01-002
     - Ibuprofen 200mg - 10000 tablets - LOT-2026-02-NEW-A
     - Aspirin 81mg - 7500 tablets - LOT-2025-11-001
     - Aspirin 81mg - 7500 tablets - LOT-2026-02-NEW-B
   - **Verify**: Lot numbers clearly displayed for each item
   - Tap "Continue"

7. **Enhanced Transaction Codes (1.5 min)**
   - **Verify**: Additional fields for pharmaceutical vendor:
     - Receiving Location: "PHARMA-WH-A"
     - Quality Control Required: "Yes"
     - Temperature Log: "Controlled"
     - Compliance Code: "FDA-RX-001"
   - Review and confirm all codes
   - Tap "Continue"

8. **Detailed BOL Entry (1 min)**
   - Enter BOL#: "PHARMA-BOL-2026-02-19"
   - Enter description: "Monthly Pharmaceutical Delivery - PharmaSupply"
   - Enter remarks: "All items temperature controlled, QC inspection required before storage"
   - Tap "Continue"

9. **Comprehensive Summary Review (2 min)**
   - Scroll through detailed summary
   - **Verify**: All 4 line items with lot details visible
   - **Verify**: Expiration dates displayed for each lot
   - **Verify**: Transaction codes show pharmaceutical requirements
   - **Verify**: All 3 photos visible
   - Tap "Submit"

10. **Submission & Verification (2 min)**
    - **Verify**: Extended processing time (due to multiple lots)
    - **Verify**: Progress indicators for each lot creation
    - **Verify**: Success with voucher number
    - **AGRIS Verification**: Confirm all 4 line items created
    - **AGRIS Verification**: Verify lot numbers registered in inventory
    - **AGRIS Verification**: Expiration dates tracked correctly

**Expected Results**:
- ✅ Complex lot tracking handled correctly
- ✅ Same item can be added multiple times with different lots
- ✅ Existing and new lots both supported
- ✅ Expiration dates tracked and validated
- ✅ Enhanced transaction codes for pharmaceutical compliance
- ✅ All lot information synchronized to AGRIS
- ✅ No lot number conflicts or errors
- ✅ Audit trail maintained for regulatory compliance

**Test Data**:
- Vendor: "PharmaSupply Inc" (pharmaceutical supplier)
- 4 line items (3 unique items, one with 2 lots)
- 2 existing lots, 2 new lots created
- Pharmaceutical compliance transaction codes

---

### E2E-WF-004: Maximum Capacity Stock Addition
**Priority**: Medium | **Duration**: ~15-20 minutes

**Business Scenario**: Large delivery with maximum photos, multiple vendors worth of items, testing system limits.

**Preconditions**:
- System performance testing mode
- Large dataset available

**Complete Workflow Steps**:

1. **Maximum Photo Upload (2 min)**
   - Add 4 photos (maximum allowed)
   - **Verify**: Cannot add 5th photo
   - **Verify**: "Maximum 4 photos" message displayed
   - **Verify**: Each photo ~5MB (total ~20MB)
   - Continue

2. **Vendor Selection (1 min)**
   - Select high-volume vendor "Restaurant Depot"
   - Continue

3. **Add 30 Items (10 min)**
   - Add 30 different items using mix of:
     - 20 items via barcode scan
     - 10 items via manual search
   - Include mix of:
     - 15 simple items (no lot)
     - 15 lot-tracked items
   - Enter varying quantities (ranging 1-1000)
   - **Verify**: List scrolling performance remains smooth
   - **Verify**: Item counter updates correctly (1/30, 2/30, etc.)

4. **Edit Multiple Items (2 min)**
   - Scroll to item #5, edit quantity
   - Scroll to item #15, change lot number
   - Delete item #20, re-add corrected version
   - **Verify**: List management remains responsive

5. **Transaction Codes (1 min)**
   - Complete all transaction codes
   - Continue

6. **BOL Entry (1 min)**
   - Enter BOL#: "LARGE-2026-02-19"
   - Enter detailed description
   - Continue

7. **Extended Summary Review (2 min)**
   - Scroll through entire 30-item summary
   - **Verify**: All items visible and correct
   - **Verify**: Scrolling performance acceptable
   - **Verify**: Submit button enabled only after full scroll
   - Submit

8. **Extended Upload Process (3 min)**
   - **Verify**: Progress indicators for:
     - Photo upload (20MB): ~30 seconds on WiFi
     - Data submission: ~20 seconds
     - Voucher creation: ~10 seconds
   - **Verify**: No timeout errors
   - **Verify**: Success confirmation

9. **Performance Verification (2 min)**
   - **AGRIS Verification**: All 30 items created correctly
   - **AttachToo Verification**: All 4 photos uploaded
   - **Verify**: No data truncation
   - **Verify**: No performance degradation in AGRIS

**Expected Results**:
- ✅ System handles maximum photo capacity
- ✅ Large item lists (30+) processed correctly
- ✅ UI remains responsive with large datasets
- ✅ Upload completes within acceptable timeframe
- ✅ No memory issues or crashes
- ✅ All data accurately transmitted
- ✅ Backend systems handle large transactions

**Test Data**:
- 4 photos (~20MB total)
- 30 items (15 simple, 15 with lots)
- Large BOL with detailed information

---

## Alternative Path Workflows

### E2E-WF-005: Stock Addition Without Photos (Optional Photos Path)
**Priority**: High | **Duration**: ~5-7 minutes

**Business Scenario**: Quick receiving where BOL photos are not immediately available or not required by company policy.

**Complete Workflow Steps**:

1. **Skip Photo Capture (1 min)**
   - Launch Stock Addition
   - **Verify**: Photo section displayed
   - Tap "Skip Photos" or "Continue Without Photos"
   - **Verify**: Confirmation dialog: "Are you sure you want to continue without photos?"
   - Confirm "Yes, Continue"
   - **Verify**: Photo section shows "No photos added" status

2. **Complete Vendor Selection (1 min)**
   - Search and select vendor "Quick Delivery Co"
   - Continue

3. **Add Items Normally (2 min)**
   - Add 3 items via barcode scan
   - Enter quantities
   - Continue

4. **Transaction Codes (1 min)**
   - Complete required transaction codes
   - Continue

5. **BOL Entry (1 min)**
   - Enter BOL#: "NOPHOTO-2026-02-19"
   - Add note in remarks: "Photos to be added later if needed"
   - Continue

6. **Summary Without Photos (1 min)**
   - **Verify**: Summary shows "No BOL photos" section
   - **Verify**: All other data present
   - Submit

7. **Submission (30 sec)**
   - **Verify**: Submission completes successfully
   - **Verify**: No errors related to missing photos
   - **AGRIS Verification**: Voucher created without photo attachments

**Expected Results**:
- ✅ Photos confirmed as optional, not mandatory
- ✅ Workflow completes successfully without photos
- ✅ User clearly informed about missing photos
- ✅ Voucher created in AGRIS without photo references
- ✅ Option to add photos later is available (if supported)

---

### E2E-WF-006: Change Vendor Mid-Workflow
**Priority**: Medium | **Duration**: ~8-10 minutes

**Business Scenario**: User selects wrong vendor initially, needs to change after adding items.

**Complete Workflow Steps**:

1. **Initial Setup (2 min)**
   - Capture 2 BOL photos
   - Select vendor "Wrong Vendor Inc"
   - Continue

2. **Add Items (2 min)**
   - Add 3 items for the wrong vendor
   - Enter quantities

3. **Realize Mistake (30 sec)**
   - User notices items don't match vendor
   - Tap "Back" or "Change Vendor" button

4. **Change Vendor (1 min)**
   - **Verify**: Warning dialog: "Changing vendor may clear transaction codes. Continue?"
   - Confirm "Yes"
   - Select correct vendor: "Right Vendor Co"
   - **Verify**: Warning dialog: "Previous items may not be valid for this vendor. Review item list."

5. **Review and Adjust Items (2 min)**
   - **Verify**: System checks item compatibility with new vendor
   - **Verify**: Items still valid for new vendor are retained
   - **Verify**: Transaction codes cleared and need re-entry
   - Review item list
   - Keep valid items, delete any incompatible ones
   - Continue

6. **Re-enter Transaction Codes (1 min)**
   - **Verify**: Transaction codes empty (cleared due to vendor change)
   - Enter new codes based on new vendor
   - Continue

7. **Complete Workflow (1.5 min)**
   - Enter BOL# (remains unchanged)
   - Review summary with corrected vendor
   - Submit
   - **Verify**: Success with correct vendor

**Expected Results**:
- ✅ Vendor can be changed mid-workflow
- ✅ User warned about consequences (transaction codes reset)
- ✅ Items are re-validated for new vendor
- ✅ Transaction codes cleared and require re-entry
- ✅ Photos and BOL# persist through vendor change
- ✅ Final voucher has correct vendor

---

### E2E-WF-007: Manual Item Entry (No Barcode Scanner)
**Priority**: Medium | **Duration**: ~8-10 minutes

**Business Scenario**: Barcode scanner unavailable or items don't have barcodes - all items added manually.

**Complete Workflow Steps**:

1. **Setup (2 min)**
   - Complete photo capture
   - Select vendor
   - Navigate to item entry

2. **Manual Item Search 1 (1.5 min)**
   - **Verify**: "Scan Barcode" button visible
   - Tap "Manual Search" instead
   - Enter item name: "Flour"
   - **Verify**: Search results display list of matching items
   - **Verify**: Search supports partial matches
   - Select "All-Purpose Flour - 50LB"
   - **Verify**: Item details populate
   - Enter quantity: "100"
   - Add item

3. **Manual Item Search 2 with Filters (2 min)**
   - Tap "Add Another Item"
   - Enter search: "Sugar"
   - **Verify**: Multiple results shown
   - Apply filter: Category = "Baking"
   - **Verify**: Results filtered
   - Select "Granulated Sugar - 25LB"
   - Enter quantity: "75"
   - Add item

4. **Manual Search by Item Code (1.5 min)**
   - Tap "Add Another Item"
   - Switch search mode to "Item Code"
   - Enter item code: "ITM-001234"
   - **Verify**: Direct match found
   - **Verify**: Item details displayed
   - Enter quantity: "50"
   - Check lot number required
   - Enter lot: "LOT-MANUAL-001"
   - Add item

5. **Complete Workflow (3 min)**
   - **Verify**: 3 items added, all via manual entry
   - Complete transaction codes
   - Enter BOL information
   - Review summary
   - Submit
   - **Verify**: Success

**Expected Results**:
- ✅ Complete workflow possible without barcode scanner
- ✅ Manual search supports multiple search modes (name, code, filters)
- ✅ Partial matching and auto-complete help users
- ✅ Search results are accurate and relevant
- ✅ Same validation as barcode-scanned items
- ✅ Equivalent functionality to barcode path

---

## Error Recovery Workflows

### E2E-WF-008: Network Loss During Submission - Auto Recovery
**Priority**: Critical | **Duration**: ~10-12 minutes

**Business Scenario**: Network connection lost during voucher submission, system should recover gracefully.

**Complete Workflow Steps**:

1. **Complete Normal Workflow (5 min)**
   - Capture photos
   - Select vendor
   - Add 3 items
   - Complete transaction codes
   - Enter BOL information
   - Review summary
   - Prepare to submit

2. **Simulate Network Loss (1 min)**
   - Just before tapping "Submit", disable WiFi/mobile data
   - **Verify**: Network indicator shows no connection
   - Tap "Submit Voucher"

3. **Initial Failure Handling (1 min)**
   - **Verify**: System attempts submission
   - **Verify**: After timeout (~30 seconds), error message displayed:
     - "Network connection lost. Please check your connection."
     - "Your data has been saved. You can retry submission when connected."
   - **Verify**: "Retry" button available
   - **Verify**: "Save as Draft" button available

4. **Save as Draft (30 sec)**
   - Tap "Save as Draft"
   - **Verify**: Confirmation: "Your stock addition has been saved. You can resume later."
   - **Verify**: Draft saved locally on device
   - Navigate away from Stock Addition

5. **Resume Draft (1 min)**
   - Re-enable network connection
   - **Verify**: WiFi/mobile data connected
   - Navigate back to Stock Addition
   - **Verify**: Draft banner displayed: "You have 1 incomplete stock addition"
   - Tap "Resume Draft"

6. **Review and Retry Submission (1 min)**
   - **Verify**: All previously entered data intact:
     - Photos still present
     - Vendor selected
     - All 3 items in list
     - Transaction codes filled
     - BOL information complete
   - Tap "Submit Voucher"

7. **Successful Submission (30 sec)**
   - **Verify**: Submission succeeds now that network is available
   - **Verify**: Voucher number generated
   - **Verify**: Success confirmation
   - **Verify**: Draft automatically deleted

8. **Backend Verification (1 min)**
   - **AGRIS**: Verify voucher exists with all data
   - **AttachToo**: Verify photos uploaded successfully
   - **Verify**: No duplicate vouchers created

**Expected Results**:
- ✅ Network loss detected immediately
- ✅ User informed with clear error message
- ✅ All data preserved during network loss
- ✅ Draft saved locally for recovery
- ✅ Draft can be resumed successfully
- ✅ Retry submission succeeds after network restored
- ✅ No data loss or corruption
- ✅ No duplicate submissions created

---

### E2E-WF-009: App Crash During Data Entry - State Recovery
**Priority**: High | **Duration**: ~8-10 minutes

**Business Scenario**: App crashes or is force-closed during stock addition, data should be recoverable.

**Complete Workflow Steps**:

1. **Begin Stock Addition (3 min)**
   - Capture 3 BOL photos
   - Select vendor
   - Add 5 items with various quantities
   - **Verify**: Significant data entered

2. **Simulate App Crash (30 sec)**
   - Before completing transaction codes
   - Force close the app (or simulate crash)
   - **Verify**: App terminated

3. **Relaunch App (1 min)**
   - Reopen AGRIS Warehouse Mobile App
   - **Verify**: App launches successfully
   - Navigate to Stock Addition feature

4. **Auto-Recovery Detection (30 sec)**
   - **Verify**: Recovery prompt displayed:
     - "We detected an incomplete stock addition from [timestamp]"
     - "Would you like to recover your work?"
     - "Recover" button
     - "Discard" button

5. **Recover Data (1 min)**
   - Tap "Recover"
   - **Verify**: App restores to state before crash:
     - All 3 photos present
     - Vendor selected
     - All 5 items in list with correct quantities
   - **Verify**: Positioned at transaction codes screen (where crash occurred)

6. **Complete Workflow (3 min)**
   - Complete transaction codes
   - Enter BOL information
   - Review summary
   - Submit successfully
   - **Verify**: No data corruption

**Expected Results**:
- ✅ App crash doesn't result in data loss
- ✅ Auto-save mechanism captures progress regularly
- ✅ User offered clear recovery option
- ✅ All data restored accurately
- ✅ User can continue from point of interruption
- ✅ Recovered data is valid and submittable
- ✅ No duplicate or corrupted entries

---

### E2E-WF-010: AGRIS ERP Temporarily Unavailable - Graceful Degradation
**Priority**: High | **Duration**: ~12-15 minutes

**Business Scenario**: AGRIS ERP backend system temporarily unavailable during stock addition.

**Complete Workflow Steps**:

1. **Begin Workflow (2 min)**
   - Launch Stock Addition
   - Capture photos
   - Navigate to vendor search

2. **AGRIS Unavailable for Vendor Search (2 min)**
   - **Scenario**: AGRIS backend down
   - Enter vendor search query
   - **Verify**: After timeout (~10 seconds), error message:
     - "Unable to connect to AGRIS system"
     - "Searching cached vendor data..."
   - **Verify**: System falls back to locally cached vendors
   - **Verify**: Warning badge: "Using cached data - may not be current"
   - Select vendor from cache
   - Continue

3. **AGRIS Unavailable for Item Lookup (2 min)**
   - Scan barcode
   - **Verify**: Similar fallback to cached item data
   - **Verify**: Warning: "Item data from cache - verify details"
   - Add item with warning acknowledgement
   - Add 2 more items (all from cache)

4. **Queue for Later Submission (1 min)**
   - Complete transaction codes
   - Enter BOL information
   - Tap "Submit"
   - **Verify**: Error: "AGRIS system unavailable. Cannot submit voucher."
   - **Verify**: Options presented:
     - "Queue for Automatic Submission" (when AGRIS available)
     - "Save as Draft" (manual submission later)
     - "Cancel"

5. **Queue for Submission (1 min)**
   - Select "Queue for Automatic Submission"
   - **Verify**: Confirmation:
     - "Your voucher has been queued for submission"
     - "It will automatically submit when AGRIS is available"
     - "You'll receive a notification"
   - **Verify**: Queued item appears in "Pending Submissions" list

6. **Simulate AGRIS Recovery (2 min)**
   - Wait or simulate AGRIS system coming back online
   - **Verify**: Background sync process detects AGRIS availability
   - **Verify**: Automatic submission begins

7. **Automatic Submission & Notification (2 min)**
   - **Verify**: Push notification received:
     - "Stock addition submitted successfully"
     - "Voucher #: VCH-2026-0001235"
   - Open app
   - **Verify**: Queued item removed from pending list
   - **Verify**: Submission summary available

8. **Backend Verification (1 min)**
   - **AGRIS**: Verify voucher created correctly
   - **Verify**: All data from cached sources validated against live data
   - **Verify**: Any discrepancies flagged for review

**Expected Results**:
- ✅ System gracefully handles AGRIS unavailability
- ✅ Falls back to cached data with clear warnings
- ✅ Allows user to complete workflow offline
- ✅ Queues submissions for automatic retry
- ✅ Successfully submits when backend available
- ✅ User notified of submission status
- ✅ Data validation occurs upon actual submission
- ✅ No data loss despite backend unavailability

---

## Edge Case Workflows

### E2E-WF-011: Special Characters in All Text Fields
**Priority**: Medium | **Duration**: ~7-9 minutes

**Business Scenario**: Test system handling of special characters, unicode, and edge cases in text input.

**Complete Workflow Steps**:

1. **Setup (1 min)**
   - Launch Stock Addition
   - Capture photos

2. **Vendor with Special Characters (1 min)**
   - Search for vendor: "José's Café & Restaurant"
   - **Verify**: Special characters (é, ', &) handled correctly
   - Select vendor

3. **Item with Unicode Characters (2 min)**
   - Manual search: "Café Molido"
   - **Verify**: Unicode supported in search
   - Add item
   - Enter quantity: "50"

4. **BOL with Special Characters (1 min)**
   - Enter BOL#: "BOL-2026-#001234/A&B"
   - **Verify**: Special characters (#, /, &) accepted
   - Enter description: "Delivery @ 3:00pm - "Priority Items""
   - **Verify**: Quotes and @ symbol handled
   - Enter remarks with emoji: "✓ Temperature controlled ☑ Inspected"
   - **Verify**: Emoji characters accepted (or gracefully rejected)

5. **Complete and Submit (2 min)**
   - Complete transaction codes
   - Review summary
   - **Verify**: All special characters display correctly
   - Submit

6. **Backend Verification (1 min)**
   - **AGRIS**: Verify all special characters stored correctly
   - **Verify**: No character encoding issues
   - **Verify**: Data retrievable and displayable

**Expected Results**:
- ✅ Special characters supported in all text fields
- ✅ Unicode characters handled correctly
- ✅ No SQL injection vulnerabilities
- ✅ No XSS vulnerabilities
- ✅ Character encoding preserved through full stack
- ✅ Edge cases don't break UI or backend

---

### E2E-WF-012: Boundary Value Testing - Maximum Quantities
**Priority**: Medium | **Duration**: ~6-8 minutes

**Business Scenario**: Test system limits with extremely large quantity values.

**Complete Workflow Steps**:

1. **Standard Setup (2 min)**
   - Complete photos, vendor selection

2. **Test Maximum Valid Quantity (1.5 min)**
   - Add item
   - Enter quantity: "999,999,999" (nine nines)
   - **Verify**: System accepts maximum valid quantity
   - **Verify**: Proper number formatting (commas)
   - Add item

3. **Test Exceeding Maximum (1 min)**
   - Add another item
   - Attempt to enter: "10,000,000,000" (ten billion)
   - **Verify**: Validation error: "Quantity exceeds maximum allowed value"
   - **Verify**: Maximum limit clearly communicated
   - Adjust to valid value

4. **Test Decimal Quantities (1 min)**
   - Add item with decimal UOM
   - Enter quantity: "123.456"
   - **Verify**: Decimals accepted where appropriate
   - Add item

5. **Complete and Submit (2.5 min)**
   - Complete workflow
   - Submit
   - **Verify**: Large quantities processed correctly
   - **AGRIS**: Verify large numbers stored accurately (no overflow)

**Expected Results**:
- ✅ Maximum quantity limits enforced
- ✅ Large numbers formatted for readability
- ✅ Decimal quantities supported where needed
- ✅ No integer overflow errors
- ✅ Backend systems handle large values correctly

---

### E2E-WF-013: Rapid Consecutive Submissions (Race Condition Testing)
**Priority**: Medium | **Duration**: ~10-12 minutes

**Business Scenario**: Submit multiple stock additions in rapid succession to test for race conditions and duplicate prevention.

**Complete Workflow Steps**:

1. **Prepare 3 Complete Stock Additions (6 min)**
   - Complete Stock Addition #1 to summary screen (don't submit yet)
     - Vendor: Vendor A
     - 2 items
     - BOL#: "RAPID-001"
   - Note voucher details
   - Start New Stock Addition
   - Complete Stock Addition #2 to summary screen
     - Vendor: Vendor B
     - 3 items  
     - BOL#: "RAPID-002"
   - Start New Stock Addition
   - Complete Stock Addition #3 to summary screen
     - Vendor: Vendor C
     - 2 items
     - BOL#: "RAPID-003"

2. **Rapid Sequential Submission (3 min)**
   - Submit Stock Addition #3
   - Immediately submit Stock Addition #2 (before #3 completes)
   - Immediately submit Stock Addition #1 (before #2 completes)
   - **Verify**: All 3 submissions proceed simultaneously

3. **Concurrent Processing Verification (2 min)**
   - **Verify**: All 3 show individual progress indicators
   - **Verify**: No errors or conflicts
   - **Verify**: All 3 complete successfully
   - **Verify**: 3 unique voucher numbers generated:
     - VCH-2026-XXXX for #1
     - VCH-2026-YYYY for #2
     - VCH-2026-ZZZZ for #3

4. **Backend Verification (1 min)**
   - **AGRIS**: Verify all 3 vouchers created
   - **Verify**: No duplicate vouchers
   - **Verify**: All voucher data correct and distinct
   - **Verify**: No data mixing between submissions

**Expected Results**:
- ✅ Multiple concurrent submissions handled correctly
- ✅ No race conditions
- ✅ Each submission gets unique voucher number
- ✅ No data corruption or mixing
- ✅ All submissions complete successfully
- ✅ Backend properly queues and processes concurrent requests

---

## Multi-User & Multi-Device Workflows

### E2E-WF-014: Same User on Multiple Devices (Draft Synchronization)
**Priority**: High | **Duration**: ~10-12 minutes

**Business Scenario**: User starts stock addition on phone, continues on tablet.

**Complete Workflow Steps**:

1. **Start on Phone (Device A) (3 min)**
   - Login as user "warehouse_user_1" on iPhone
   - Launch Stock Addition
   - Capture 2 photos
   - Select vendor
   - Add 3 items
   - **Verify**: Auto-save indicator shows "Draft saved"

2. **Switch to Tablet (Device B) (2 min)**
   - Without submitting, close app on phone
   - Login as same user "warehouse_user_1" on iPad
   - Navigate to Stock Addition
   - **Verify**: Draft sync notification:
     - "You have a draft from another device (iPhone)"
     - "Last updated: 2 minutes ago"
     - "Open Draft" button

3. **Continue on Tablet (3 min)**
   - Tap "Open Draft"
   - **Verify**: All data synchronized from phone:
     - Same 2 photos visible
     - Same vendor selected
     - All 3 items present
   - Complete transaction codes on tablet
   - Enter BOL information
   - Review summary

4. **Submit from Tablet (1 min)**
   - Submit voucher from iPad
   - **Verify**: Submission successful
   - **Verify**: Voucher number displayed

5. **Verify Phone State (1 min)**
   - Return to iPhone
   - Open app
   - **Verify**: Draft no longer exists (removed after submission)
   - **Verify**: Submission history shows completed voucher
   - **Verify**: No duplicate drafts

**Expected Results**:
- ✅ Drafts synchronized across devices for same user
- ✅ Data integrity maintained during device switch
- ✅ User clearly informed about draft location
- ✅ Submission from one device clears draft on all devices
- ✅ No conflicts or duplicate submissions
- ✅ Seamless user experience across devices

---

### E2E-WF-015: Multiple Users - Concurrent Different Vendors
**Priority**: Medium | **Duration**: ~12-15 minutes

**Business Scenario**: Multiple warehouse staff processing different deliveries simultaneously.

**Complete Workflow Steps**:

1. **User A - Vendor 1 Delivery (5 min)**
   - User "warehouse_user_1" logs in on Device A
   - Starts Stock Addition for "Vendor Alpha"
   - Adds 5 items
   - Completes to BOL entry stage
   - Pauses (doesn't submit yet)

2. **User B - Vendor 2 Delivery (5 min)**
   - Simultaneously, user "warehouse_user_2" logs in on Device B
   - Starts Stock Addition for "Vendor Beta"
   - Adds 4 items
   - Completes to BOL entry stage
   - Pauses (doesn't submit yet)

3. **User A Submits (1 min)**
   - User A enters BOL#: "BOL-ALPHA-001"
   - Submits voucher
   - **Verify**: Success, voucher VCH-2026-0001

4. **User B Submits (1 min)**
   - User B enters BOL#: "BOL-BETA-002"
   - Submits voucher
   - **Verify**: Success, voucher VCH-2026-0002

5. **Cross-Verification (2 min)**
   - User A checks submission history
   - **Verify**: Only sees their own submission (Vendor Alpha)
   - User B checks submission history
   - **Verify**: Only sees their own submission (Vendor Beta)
   - **AGRIS Verification**:
     - VCH-2026-0001: Vendor Alpha, User A
     - VCH-2026-0002: Vendor Beta, User B
     - Both vouchers correct and independent

**Expected Results**:
- ✅ Multiple users work concurrently without interference
- ✅ Each user's data isolated and protected
- ✅ No data mixing between users
- ✅ Sequential voucher numbers assigned correctly
- ✅ Both submissions successful
- ✅ User-specific submission history maintained

---

## Performance & Load Workflows

### E2E-WF-016: Performance Test - Complete Workflow Under Different Network Conditions
**Priority**: High | **Duration**: ~20-25 minutes

**Business Scenario**: Test stock addition performance under various network speeds.

**Complete Workflow Steps**:

1. **WiFi - Optimal Conditions (5 min)**
   - Connect to WiFi (50+ Mbps)
   - Complete full Stock Addition:
     - 4 photos (~20MB)
     - 1 vendor
     - 10 items
     - Full transaction codes
     - BOL information
   - Measure timings:
     - Photo upload time
     - Vendor search response
     - Item lookup time
     - Final submission time
   - **Target**: < 60 seconds total submission

2. **4G/LTE - Good Mobile Connection (6 min)**
   - Disconnect WiFi, use 4G
   - Complete similar Stock Addition
   - Measure same metrics
   - **Target**: < 90 seconds total submission

3. **3G - Slower Connection (8 min)**
   - Simulate 3G connection (or throttle)
   - Complete similar Stock Addition
   - **Verify**: Progress indicators more prominent
   - **Verify**: User kept informed during longer waits
   - Measure timings
   - **Target**: < 180 seconds total submission

4. **Performance Comparison (1 min)**
   - Compare timings across network conditions:
     - WiFi vs 4G vs 3G
   - **Verify**: All submissions successful regardless of speed
   - **Verify**: App adapts UX based on connection speed

**Expected Results**:
- ✅ App performs well across network conditions
- ✅ Optimal performance on WiFi
- ✅ Acceptable performance on 4G
- ✅ Functional on 3G with appropriate feedback
- ✅ No timeouts or failures due to slower connections
- ✅ Progress indicators adjust to connection speed
- ✅ User experience appropriate for each condition

---

## Data Validation Workflows

### E2E-WF-017: Data Integrity Check - Complete Workflow with Verification
**Priority**: Critical | **Duration**: ~15-20 minutes

**Business Scenario**: Comprehensive validation that all data entered in mobile app accurately transfers to backend systems.

**Complete Workflow Steps**:

1. **Capture Baseline Data (3 min)**
   - Launch Stock Addition
   - Capture 3 specific photos (save copies for comparison)
   - Document exact photo filenames and timestamps
   - Select vendor: "DataTest Vendor Inc"
   - Document vendor ID and details

2. **Add Items with Specific Data (4 min)**
   - Item 1: 
     - Name: "DataTest Item A"
     - Quantity: 123
     - No lot number
   - Item 2:
     - Name: "DataTest Item B" 
     - Quantity: 456
     - Lot: "LOT-VERIFY-001"
   - Item 3:
     - Name: "DataTest Item C"
     - Quantity: 789.5 (decimal)
     - Lot: "LOT-VERIFY-002"
   - Document exact values entered

3. **Transaction Codes with Specific Values (2 min)**
   - Location: "WH-VERIFY-01"
   - Department: "DEPT-TEST-A"
   - Cost Center: "CC-12345"
   - Document all values

4. **BOL Information (1 min)**
   - BOL#: "BOL-VERIFY-2026-02-19"
   - Description: "Data Integrity Verification Test - Exact Match Required"
   - Remarks: "Testing character set: !@#$%^&*()"
   - Document exact text

5. **Pre-Submission Verification (1 min)**
   - Review summary carefully
   - Take screenshot of summary for comparison
   - Document expected voucher data

6. **Submit (1 min)**
   - Submit voucher
   - Capture voucher number: VCH-2026-XXXX
   - Document submission timestamp

7. **AGRIS ERP Verification (3 min)**
   - Login to AGRIS web interface
   - Search for voucher VCH-2026-XXXX
   - **Verify Field-by-Field**:
     - Vendor ID and name: Exact match
     - Line Item 1: Item A, Qty: 123, No lot
     - Line Item 2: Item B, Qty: 456, Lot: LOT-VERIFY-001
     - Line Item 3: Item C, Qty: 789.5, Lot: LOT-VERIFY-002
     - Transaction codes all match
     - BOL# matches exactly
     - Description matches exactly (including special characters)
     - Remarks match exactly
     - Submission timestamp within expected range
   - Take screenshots for evidence

8. **AttachToo Verification (2 min)**
   - Login to AttachToo system
   - Search by voucher number
   - **Verify**:
     - Exactly 3 photos attached
     - Photo filenames or hashes match originals
     - Photos viewable and not corrupted
     - Photos linked correctly to voucher
     - Metadata (upload timestamp, file size) accurate

9. **Audit Trail Verification (1 min)**
   - Check AGRIS audit logs
   - **Verify**:
     - Correct user recorded (warehouse_user)
     - Creation timestamp accurate
     - Source system: Mobile App
     - No modification flags (data not altered)

**Expected Results**:
- ✅ 100% data accuracy from mobile to AGRIS
- ✅ No data truncation or corruption
- ✅ Special characters preserved
- ✅ Decimal quantities accurate
- ✅ Lot numbers correctly assigned
- ✅ Photos uploaded and linked correctly
- ✅ Timestamps accurate across systems
- ✅ Audit trail complete and accurate
- ✅ No data loss or alteration during transmission

---

### E2E-WF-018: Full Regression Suite - Combined Scenario
**Priority**: Critical | **Duration**: ~25-30 minutes

**Business Scenario**: Comprehensive end-to-end test combining multiple challenging scenarios.

**Complete Workflow Steps**:

1. **Complex Setup (3 min)**
   - Fresh user account (first time)
   - Configure Vendor ID Range
   - **Verify**: Configuration persists

2. **Maximum Photo Complexity (2 min)**
   - Add 4 photos:
     - 2 from camera
     - 2 from gallery
   - Delete 1 photo, replace with new one
   - **Verify**: Final count: 4 photos

3. **Vendor Search and Change (2 min)**
   - Search vendor: Partial match "Acme"
   - Select first result
   - Navigate to items
   - Decide to change vendor
   - Go back, select different vendor
   - **Verify**: Vendor change handled correctly

4. **Complex Item Mix (8 min)**
   - Add 15 items total:
     - 5 via barcode scan (no lots)
     - 5 via barcode scan (with lots - mix of existing and new lots)
     - 5 via manual search (mix of lot and no-lot)
   - Include decimal quantities
   - Edit 2 items after adding
   - Delete 1 item and re-add corrected version
   - **Verify**: Final item count: 15

5. **Full Transaction Code Entry (2 min)**
   - Complete all required transaction codes
   - Fill 2 optional transaction codes
   - Leave 1 optional code blank
   - **Verify**: Validation passes

6. **Detailed BOL Entry (1 min)**
   - Enter BOL#: "COMPLEX-BOL-2026-02-19-001"
   - Enter long description (200+ characters)
   - Enter remarks with special characters
   - **Verify**: All fields accepted

7. **Extensive Summary Review (2 min)**
   - Review complete summary
   - Verify all 15 items visible
   - Verify all lot numbers correct
   - Verify photos visible
   - Scroll to bottom
   - **Verify**: Submit enabled

8. **Submission with Progress Tracking (3 min)**
   - Submit voucher
   - **Verify**: Progress indicators for:
     - Photo upload (4 photos)
     - Data validation
     - Voucher creation
     - Line item creation (15 items)
   - **Verify**: Success with voucher number

9. **Comprehensive Backend Verification (3 min)**
   - **AGRIS**: 
     - Voucher exists
     - All 15 line items present and accurate
     - All lot numbers correctly assigned
     - Transaction codes all present
     - BOL and description complete
   - **AttachToo**:
     - All 4 photos uploaded
     - Photos linked to voucher
     - Photos viewable

10. **Immediate Follow-Up Stock Addition (2 min)**
    - Without logging out
    - Start new Stock Addition
    - **Verify**: Settings still configured
    - **Verify**: Recent vendors appear in search
    - **Verify**: App ready for next transaction

**Expected Results**:
- ✅ Complex multi-faceted workflow completes successfully
- ✅ All features work correctly in combination
- ✅ Data integrity maintained throughout
- ✅ Performance acceptable with high data volume
- ✅ User experience smooth despite complexity
- ✅ Backend systems handle complex transaction correctly
- ✅ Ready for immediate next transaction
- ✅ No errors, crashes, or data loss

---

## Workflow Test Execution Matrix

### Priority Execution Order

**Phase 1 - Critical Happy Paths (Day 1-2)**
1. E2E-WF-001: First-Time User Complete Setup
2. E2E-WF-002: Experienced User Standard Flow
3. E2E-WF-017: Data Integrity Verification

**Phase 2 - Complex & Alternative Paths (Day 3-4)**
4. E2E-WF-003: Complex Lot Number Management
5. E2E-WF-004: Maximum Capacity Test
6. E2E-WF-005: Stock Addition Without Photos
7. E2E-WF-006: Change Vendor Mid-Workflow
8. E2E-WF-007: Manual Item Entry

**Phase 3 - Error Handling & Recovery (Day 5)**
9. E2E-WF-008: Network Loss Recovery
10. E2E-WF-009: App Crash Recovery
11. E2E-WF-010: AGRIS Unavailable Graceful Degradation

**Phase 4 - Edge Cases & Performance (Day 6)**
12. E2E-WF-011: Special Characters
13. E2E-WF-012: Boundary Value Testing
14. E2E-WF-013: Rapid Consecutive Submissions
15. E2E-WF-016: Performance Under Various Networks

**Phase 5 - Multi-User & Final Validation (Day 7)**
16. E2E-WF-014: Multi-Device Synchronization
17. E2E-WF-015: Multiple Users Concurrent
18. E2E-WF-018: Full Regression Combined Scenario

---

## Test Data Requirements for E2E Workflows

### Vendor Test Data
- **Vendor A - Simple**: "Acme Corporation" - Standard fields, no special requirements
- **Vendor B - Complex**: "PharmaSupply Inc" - Enhanced transaction codes, lot tracking
- **Vendor C - Recent**: "Quick Delivery Co" - For testing recent/favorite lists
- **Vendor D - Special Chars**: "José's Café & Restaurant" - Unicode and special characters
- **Vendor E - DataTest**: "DataTest Vendor Inc" - For verification testing

### Item Test Data
- **10 Simple Items**: No lot numbers, various quantities
- **10 Lot-Tracked Items**: Requiring lot numbers, mix of existing/new lots
- **5 Barcode Items**: Valid barcodes for scanning
- **5 Manual Items**: Items for manual search
- **1 Special Char Item**: "Café Molido" - Unicode testing

### User Accounts
- **warehouse_user_1**: Warehouse PRO user (primary testing)
- **warehouse_user_2**: Warehouse PRO user (multi-user testing)
- **warehouse_user_non_pro**: Non-PRO user (access control testing)

### BOL Numbers
- Sequential: BOL-2026-001234, BOL-2026-001235, etc.
- Special: BOL-2026-#001234/A&B (special characters)
- Test: BOL-VERIFY-2026-02-19 (verification)

---

## Success Metrics for E2E Workflow Testing

### Functional Metrics
- ✅ 100% of critical workflows pass
- ✅ 95%+ of high-priority workflows pass
- ✅ 90%+ of medium-priority workflows pass
- ✅ 0 P1 (Critical) defects in workflow execution
- ✅ < 3 P2 (High) defects in workflow execution

### Performance Metrics
- ✅ Average workflow completion time < 10 minutes
- ✅ Photo upload < 30 seconds on WiFi
- ✅ Vendor search response < 2 seconds
- ✅ Final submission < 60 seconds

### Data Integrity Metrics
- ✅ 100% data accuracy (mobile → AGRIS → AttachToo)
- ✅ 0 data loss incidents
- ✅ 0 duplicate voucher creations
- ✅ 100% audit trail completeness

### User Experience Metrics
- ✅ Clear error messages for all failure scenarios
- ✅ Successful recovery in 100% of error scenarios
- ✅ No app crashes during workflows
- ✅ Settings persist across sessions

---

## Notes for Test Execution

### Best Practices
1. **Reset State Between Tests**: Ensure clean state for each workflow
2. **Document Timing**: Record actual durations vs. estimated
3. **Capture Evidence**: Screenshots at key workflow steps
4. **Log Defects Immediately**: Don't wait until end of test
5. **Verify Backend**: Always confirm data in AGRIS and AttachToo
6. **Test on Multiple Devices**: Minimum one iOS and one Android device per workflow

### Common Pitfalls to Avoid
- Don't skip backend verification steps
- Don't assume success without checking error logs
- Don't reuse same test data without cleanup
- Don't test multiple workflows simultaneously in same session
- Don't ignore warning messages or visual glitches

### Test Environment Maintenance
- Clear app cache between major test sessions
- Reset test database to known state daily
- Verify backend systems operational before testing
- Keep test devices charged and connected
- Maintain inventory of test data (vendors, items, lots)

---

## Appendix: Workflow Test Template

For creating new E2E workflow tests, use this template:

```markdown
### E2E-WF-XXX: [Workflow Name]
**Priority**: Critical/High/Medium/Low | **Duration**: ~X-Y minutes

**Business Scenario**: [Describe the real-world scenario this tests]

**Preconditions**:
- [List all required preconditions]

**Complete Workflow Steps**:

1. **[Step Name] (X min)**
   - [Action 1]
   - [Action 2]
   - **Verify**: [Expected outcome]

[Continue for all steps...]

**Expected Results**:
- ✅ [Key outcome 1]
- ✅ [Key outcome 2]

**Test Data**:
- [List specific test data required]
```

---

**Document Version**: 1.0  
**Total Workflows Documented**: 18  
**Total Estimated Execution Time**: ~200 minutes (3-4 hours)  
**Recommended Test Cycles**: 2 full cycles before production release
