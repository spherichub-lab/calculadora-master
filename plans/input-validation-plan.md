# Input Validation Implementation Plan

## Overview
Update the calculator's input validation to meet new requirements:
- Always display inputs with 2 decimal places
- Change error message to "Valor inválido"
- Only show errors on blur or when clicking calculate buttons (not while typing)

## Current Behavior Analysis

### Existing Implementation
- **Real-time validation**: Errors appear immediately while typing (lines 451-466)
- **Error message**: "Valor inválido. Use incrementos de 0,25 (ex: 0,00, 0,25, 0,50, 0,75)"
- **Formatting**: Already uses `toFixed(2)` for 2 decimal places (line 302)
- **Validation triggers**: Both 'input' event (real-time) and 'blur' event

## Required Changes

### 1. Update Error Messages
**Location**: Lines 90-91, 106-107, 151-152, 167-168, 213-214, 229-230

**Change**: Replace all error message text from:
```
"Valor inválido. Use incrementos de 0,25 (ex: 0,00, 0,25, 0,50, 0,75)"
```
to:
```
"Valor inválido"
```

### 2. Remove Real-Time Validation
**Location**: Lines 449-466

**Change**: Remove the 'input' event listener that validates on each keystroke. This section currently:
- Shows/hides errors while typing
- Validates on every character input

**Action**: Delete or comment out the `input.addEventListener('input', ...)` block (lines 451-466)

### 3. Keep Blur Event Validation
**Location**: Lines 469-471

**Status**: Already correctly implemented - this should remain unchanged

The `blur` event listener already:
- Validates the input when focus is lost
- Formats the value with 2 decimal places
- Shows/hides error message appropriately

### 4. Keep Calculate Button Validation
**Location**: Lines 371-381, 384-394, 397-407

**Status**: Already correctly implemented - this should remain unchanged

The calculate functions already:
- Call `validateAndFormatInput()` which shows errors
- Prevent calculation if inputs are invalid

### 5. Verify 2 Decimal Places Formatting
**Location**: Line 302 (`formatNumberWithComma` function)

**Status**: Already correctly implemented

The function uses `num.toFixed(2)` which ensures:
- Always displays exactly 2 decimal places
- Examples: "1.50", "1,00", "0.25", "2.00"

## Implementation Steps

### Step 1: Update Error Message HTML
Update all 6 error message divs in the HTML:
1. `addLongeError` (line 90-91)
2. `addPertoError` (line 106-107)
3. `nearLongeError` (line 151-152)
4. `nearAddError` (line 167-168)
5. `farPertoError` (line 213-214)
6. `farAddError` (line 229-230)

### Step 2: Remove Real-Time Validation
Remove the 'input' event listener block (lines 451-466) from the event listeners section.

### Step 3: Verify Existing Functionality
Confirm that:
- Blur event validation still works (lines 469-471)
- Calculate button validation still works (lines 371-407)
- 2 decimal places formatting works (line 302)

## Expected Behavior After Changes

### User Experience Flow:
1. **Typing**: User types numbers - no errors shown while typing
2. **Blur**: User clicks away from input - validation occurs:
   - If valid: format to 2 decimal places (e.g., "1.5" → "1,50")
   - If invalid: show "Valor inválido" error
3. **Calculate**: User clicks calculate button - validation occurs:
   - If any input invalid: show "Valor inválido" error
   - If all valid: perform calculation

### Examples:
- ✅ User types "1.5" → blurs → displays "1,50" (no error)
- ✅ User types "1" → blurs → displays "1,00" (no error)
- ✅ User types "0.25" → blurs → displays "0,25" (no error)
- ❌ User types "1.3" → blurs → shows "Valor inválido" (not a 0.25 increment)
- ❌ User types "abc" → blurs → shows "Valor inválido" (not a number)

## Testing Checklist

- [ ] Type valid number (e.g., "1.5"), blur - should format to "1,50" with no error
- [ ] Type integer (e.g., "2"), blur - should format to "2,00" with no error
- [ ] Type 0.25 increment (e.g., "0.75"), blur - should display "0,75" with no error
- [ ] Type invalid increment (e.g., "1.3"), blur - should show "Valor inválido"
- [ ] Type non-numeric (e.g., "abc"), blur - should show "Valor inválido"
- [ ] Type valid numbers and click calculate - should calculate and show result
- [ ] Type invalid numbers and click calculate - should show "Valor inválido"
- [ ] Verify error message text is exactly "Valor inválido" (no extra text)
- [ ] Verify all 6 input fields behave consistently

## Files to Modify
- `index.html` - All changes in this single file

## Notes
- The existing `formatNumberWithComma()` function already ensures 2 decimal places via `toFixed(2)`
- The Portuguese locale formatting (comma as decimal separator) is already implemented
- No changes needed to calculation logic, only validation timing and error messages
