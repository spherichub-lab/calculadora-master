# Input Sign Formatting Plan

## Overview
Implement new formatting rules for calculator inputs to display signs explicitly for all numeric values.

## Rules to Implement
1. **All inputs can have positive or negative signs EXCEPT "adição" inputs**
2. **Adição inputs only accept positive numbers**
3. **Adição result is always positive (never negative)**
4. **When typing a number without a sign, format it with the positive sign (+). Example: "1,00" → "+1,00", "-1,00" → "-1,00"**
5. **Zero values should display as "+0,00" for visual consistency**

## Current State Analysis

### Existing Inputs
- **Adição Calculator** (Calculates Addition):
  - `addLongeInput` - Longe value (should only accept positive)
  - `addPertoInput` - Perto value (should only accept positive)
  
- **Perto Calculator** (Calculates Near):
  - `nearLongeInput` - Longe value (can be positive or negative, has toggle button)
  - `nearAddInput` - Adição value (should only accept positive)
  
- **Longe Calculator** (Calculates Far):
  - `farPertoInput` - Perto value (can be positive or negative, has toggle button)
  - `farAddInput` - Adição value (should only accept positive)

### Existing Functions
- `formatNumberWithComma(num)` - Formats with comma, no sign prefix
- `formatNumber(num)` - Formats with "+" for positive numbers, "0,00" for zero
- `formatAddition(num)` - Formats as "ADD X,XX" always positive

## Implementation Plan

### Step 1: Update formatNumber() Function for Zero Consistency
**File:** `public/index.html`
**Lines:** 553-557

**Current code:**
```javascript
function formatNumber(num) {
    if (num === 0) return '0,00';
    const sign = num > 0 ? '+' : '';
    return sign + formatNumberWithComma(num);
}
```

**Updated code:**
```javascript
function formatNumber(num) {
    const sign = num >= 0 ? '+' : '';
    return sign + formatNumberWithComma(num);
}
```

**Rationale:** Changed `num === 0` to `num >= 0` so zero displays as "+0,00" for visual consistency.

### Step 2: Update formatAddition() Function
**File:** `public/index.html`
**Lines:** 559-563

**Current code:**
```javascript
function formatAddition(num) {
    if (num < 0) return 'ADD ' + formatNumberWithComma(Math.abs(num));
    return 'ADD ' + formatNumberWithComma(num);
}
```

**Updated code:**
```javascript
function formatAddition(num) {
    const absNum = Math.abs(num);
    return 'ADD ' + formatNumber(absNum);
}
```

**Rationale:** Always use Math.abs to ensure positive value, and use formatNumber() to get explicit "+" sign.

### Step 3: Update calculateAddition() Function
**File:** `public/index.html`
**Lines:** 696-707

**Current code:**
```javascript
function calculateAddition() {
    const longe = validateAdicaoInput(addLongeInput, addLongeError);
    const perto = validateAdicaoInput(addPertoInput, addPertoError);

    if (longe === null || perto === null) {
        return; // Don't calculate if inputs are invalid
    }

    const addition = longe + perto;
    addResult.textContent = formatAddition(addition);
}
```

**Updated code:**
```javascript
function calculateAddition() {
    const longe = validateAdicaoInput(addLongeInput, addLongeError);
    const perto = validateAdicaoInput(addPertoInput, addPertoError);

    if (longe === null || perto === null) {
        return; // Don't calculate if inputs are invalid
    }

    const addition = Math.abs(longe + perto);
    addResult.textContent = formatAddition(addition);
}
```

**Rationale:** Use Math.abs() on the calculation result to ensure it's never negative.

### Step 4: Update Adição Input Formatting
**Changes needed in `formatInputOnBlur()` function (lines 641-694):**

Update line 671 from:
```javascript
input.value = formatNumberWithComma(num);
```
to:
```javascript
input.value = formatNumber(num);
```

### Step 5: Update Non-Adição Input Formatting
**Changes needed in `formatInputOnBlur()` function:**

Update line 688 from:
```javascript
input.value = formatNumberWithComma(num);
```
to:
```javascript
input.value = formatNumber(num);
```

### Step 6: Update Toggle Sign Function
**Changes needed in `toggleSign()` function (lines 839-872):**

Update line 862 from:
```javascript
input.value = formatNumberWithComma(toggledNum);
```
to:
```javascript
input.value = formatNumber(toggledNum);
```

### Step 7: Update Initial Result Display
**Changes needed in resetAll() function (lines 738-761):**

Update line 742 from:
```javascript
addResult.textContent = 'ADD 0,00';
```
to:
```javascript
addResult.textContent = 'ADD +0,00';
```

Update line 749 from:
```javascript
nearResult.textContent = '0,00';
```
to:
```javascript
nearResult.textContent = '+0,00';
```

Update line 757 from:
```javascript
farResult.textContent = '0,00';
```
to:
```javascript
farResult.textContent = '+0,00';
```

### Step 8: Update HTML Initial Result Values
**Changes needed in HTML:**

Line 136 (Adição result):
```html
<div id="addResult" class="text-3xl font-bold text-primary">
    ADD +0,00
</div>
```

Line 205 (Near result):
```html
<div id="nearResult" class="text-3xl font-bold text-primary">
    +0,00
</div>
```

Line 274 (Far result):
```html
<div id="farResult" class="text-3xl font-bold text-primary">
    +0,00
</div>
```

## Affected Code Locations

| Function/Element | Line Range | Change Type |
|------------------|-----------|-------------|
| `formatNumber()` | 553-557 | Update zero handling |
| `formatAddition()` | 559-563 | Use Math.abs and formatNumber() |
| `calculateAddition()` | 696-707 | Use Math.abs on result |
| `formatInputOnBlur()` | 641-694 | Update formatting calls |
| `toggleSign()` | 839-872 | Update formatting call |
| `resetAll()` | 738-761 | Update initial result values |
| HTML result displays | 136, 205, 274 | Update initial values |

## Validation Logic (Already Implemented - Unchanged)

1. **Adição inputs reject negative values** (lines 606-638, 658-673, 810-820)
2. **Letter detection** (lines 535-537)
3. **0.25 increment validation** (lines 540-545)
4. **Real-time validation on input** (lines 786-821)

## Expected Behavior After Implementation

### Adição Calculator Inputs
- User types: `1,00` → Display: `+1,00`
- User types: `-1,00` → Error: "Valor inválido, adição tem valor positivo"
- User types: `0` → Display: `+0,00`

### Adição Calculator Result
- Calculation: Longe (+2,00) + Perto (+1,50) → Result: `ADD +3,50`
- Calculation: Longe (+2,00) + Perto (+0,00) → Result: `ADD +0,00`
- Even if calculation would be negative, result is always positive

### Perto/Longe Calculator Non-Adição Inputs
- User types: `1,00` → Display: `+1,00`
- User types: `-1,00` → Display: `-1,00`
- User types: `0` → Display: `+0,00`
- Toggle button switches between `+` and `-`

### Perto/Longe Calculator Adição Inputs
- User types: `1,00` → Display: `+1,00`
- User types: `-1,00` → Error: "Valor inválido, adição tem valor positivo"
- User types: `0` → Display: `+0,00`

### Perto/Longe Calculator Results
- Calculation: Longe (+2,00) + Adição (+1,50) → Result: `+3,50`
- Calculation: Longe (-2,00) + Adição (+1,50) → Result: `-0,50`
- Calculation: Longe (+0,00) + Adição (+0,00) → Result: `+0,00`

## Testing Checklist

- [ ] All inputs display "+" for positive values
- [ ] All inputs display "-" for negative values (except Adição inputs)
- [ ] Zero values display as "+0,00" for consistency
- [ ] Adição inputs reject negative values with appropriate error message
- [ ] Adição result is never negative (always uses Math.abs)
- [ ] Adição result displays with explicit "+" sign
- [ ] Toggle buttons work correctly and update display
- [ ] Real-time validation still works
- [ ] Calculation results remain correct
- [ ] Blur formatting works correctly
- [ ] Reset functionality still works with "+0,00" values
- [ ] Initial HTML result displays show "+0,00"
