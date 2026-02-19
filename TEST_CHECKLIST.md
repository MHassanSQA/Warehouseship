# Stock Addition - Quick Test Checklist

## Pre-Flight Checklist
- [ ] Test environment configured
- [ ] Test data loaded (vendors, items, transaction codes)
- [ ] AGRIS ERP accessible
- [ ] AttachToo system available
- [ ] Test devices ready (iOS + Android)
- [ ] Test user accounts verified

---

## Critical Path Testing (Must Pass)

### Setup & Access
- [ ] TC-001: First-time user blocked without Vendor ID Range
- [ ] TC-002: Configure Vendor ID Range successfully
- [ ] TC-003: Non-PRO user denied access

### Photos
- [ ] TC-004: Capture photo using camera
- [ ] TC-005: Select photo from gallery
- [ ] TC-007: Maximum 4 photos enforced

### Vendor
- [ ] TC-011: Search vendor by name
- [ ] TC-015: Select vendor from list

### Items
- [ ] TC-020: Scan item barcode (valid)
- [ ] TC-022: Enter quantity for simple item
- [ ] TC-024: Select existing lot number
- [ ] TC-025: Create new lot number
- [ ] TC-027: Add multiple items

### BOL & Submission
- [ ] TC-036: Enter BOL number (required)
- [ ] TC-037: BOL number validation (missing)
- [ ] TC-041: View complete summary
- [ ] TC-046: Submit voucher successfully
- [ ] TC-047: Voucher number generated

### Integration
- [ ] INT-001: End-to-end happy path
- [ ] TC-049: Verify data in AGRIS ERP
- [ ] TC-050: Verify photos in AttachToo

---

## High Priority Testing

### Photos
- [ ] TC-006: Mix camera & gallery photos
- [ ] TC-008: Delete and replace photo

### Vendor
- [ ] TC-012: Search by Name ID
- [ ] TC-013: Search by City
- [ ] TC-014: Search by Phone
- [ ] TC-016: Change vendor selection

### Items
- [ ] TC-019: Manual item search
- [ ] TC-021: Invalid barcode handling
- [ ] TC-023: Quantity validation (zero/negative)
- [ ] TC-026: Lot number required validation
- [ ] TC-028: Edit item in list
- [ ] TC-029: Delete item from list

### Transaction Codes
- [ ] TC-031: Auto-populated from vendor
- [ ] TC-032: Required field validation
- [ ] TC-033: Dropdown suggestions

### Error Handling
- [ ] TC-051: Submit without network
- [ ] TC-052: Network loss during submission
- [ ] TC-056: App background/foreground persistence

---

## Medium Priority Testing

### Photos
- [ ] TC-009: Delete all photos
- [ ] TC-010: Continue without photos

### Vendor
- [ ] TC-017: Cancel vendor change
- [ ] TC-018: Invalid vendor search

### Transaction Codes
- [ ] TC-034: Optional fields
- [ ] TC-035: Skip transaction codes (vendor without)

### BOL
- [ ] TC-038: Voucher description (optional)
- [ ] TC-039: Remarks (optional)
- [ ] TC-040: Skip optional fields

### Summary
- [ ] TC-042: Scroll to bottom required
- [ ] TC-043: Go back - edit vendor
- [ ] TC-044: Go back - edit items
- [ ] TC-045: Go back - edit BOL

### Completion
- [ ] TC-048: Email document option

### Edge Cases
- [ ] TC-053: AGRIS ERP unavailable
- [ ] TC-054: Large photo upload
- [ ] TC-055: Special characters in text
- [ ] TC-057: App crash recovery
- [ ] TC-058: Duplicate voucher prevention
- [ ] TC-060: Maximum quantity values

---

## Performance Testing
- [ ] PERF-001: App launch time (< 3 sec)
- [ ] PERF-002: Vendor search (< 2 sec)
- [ ] PERF-003: Photo upload (< 30 sec on WiFi)
- [ ] PERF-004: Large item list (50+ items)

---

## Security Testing
- [ ] SEC-001: Authentication required
- [ ] SEC-002: Role-based access control
- [ ] SEC-003: Data encryption (HTTPS)
- [ ] SEC-004: SQL injection prevention

---

## Integration Testing
- [ ] INT-002: Barcode to AGRIS lookup
- [ ] INT-003: Vendor data synchronization

---

## Device Testing Matrix

### iOS Devices
- [ ] iPhone 14/15 - iOS 17.x
- [ ] iPhone 13 - iOS 16.x
- [ ] iPad Pro - iOS 17.x

### Android Devices
- [ ] Samsung Galaxy S23 - Android 14
- [ ] Google Pixel 7 - Android 14
- [ ] Samsung Galaxy S22 - Android 13

---

## Sign-Off Checklist

### Test Completion
- [ ] All 60 test cases executed
- [ ] 100% of Critical test cases passed
- [ ] 95%+ of High priority passed
- [ ] Test results documented
- [ ] Defects logged and tracked

### Quality Gates
- [ ] No P1 (Critical) defects open
- [ ] No P2 (High) defects in core workflow
- [ ] Performance benchmarks met
- [ ] Security review completed
- [ ] Integration tests passed

### Documentation
- [ ] Test summary report completed
- [ ] Known issues documented
- [ ] User documentation reviewed
- [ ] Release notes prepared

### Approvals
- [ ] QA Lead sign-off
- [ ] Product Owner acceptance
- [ ] Technical Lead approval
- [ ] Ready for production deployment

---

## Quick Reference: Test Execution Order

**Day 1 - Setup & Core Workflow**
1. Setup tests (TC-001 to TC-003)
2. Photo management (TC-004 to TC-010)
3. Vendor search (TC-011 to TC-018)

**Day 2 - Items & Data Entry**
1. Item search & scanning (TC-019 to TC-023)
2. Lot number handling (TC-024 to TC-026)
3. Multiple items (TC-027 to TC-030)

**Day 3 - Transaction & Submission**
1. Transaction codes (TC-031 to TC-035)
2. BOL entry (TC-036 to TC-040)
3. Summary & review (TC-041 to TC-045)
4. Submission (TC-046 to TC-050)

**Day 4 - Error Handling & Edge Cases**
1. Network errors (TC-051 to TC-053)
2. Edge cases (TC-054 to TC-060)

**Day 5 - Integration, Performance, Security**
1. Integration tests (INT-001 to INT-003)
2. Performance tests (PERF-001 to PERF-004)
3. Security tests (SEC-001 to SEC-004)

**Day 6 - Regression & Final Validation**
1. Full regression on all devices
2. User acceptance scenarios
3. Final sign-off tests

---

**Total Estimated Testing Time**: 6-8 days
**Recommended Team Size**: 2-3 QA testers
**Automation Candidates**: TC-001, TC-002, TC-011, TC-020, TC-046, INT-001
