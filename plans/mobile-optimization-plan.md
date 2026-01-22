# Mobile Optimization Plan for Calculadora Master

## Current State Analysis

The calculator currently uses:
- `grid-cols-1 lg:grid-cols-3` - Already stacks vertically on mobile
- `p-4 lg:p-8` - Basic padding on main container
- `max-w-[1400px]` - Wide max-width for desktop
- `px-4 lg:px-8` - Horizontal padding on manual section

### Issues on Mobile Devices
1. **Insufficient horizontal margins** - Content touches screen edges on small devices
2. **No tablet-specific optimization** - Medium screens (768px-1024px) need better spacing
3. **Max-width too wide** - 1400px is excessive for mobile/tablet layouts

---

## Proposed Changes

### 1. Main Calculator Section (Line 66)

**Current:**
```html
<div class="max-w-[1400px] mx-auto grid grid-cols-1 lg:grid-cols-3 gap-6">
```

**Proposed:**
```html
<div class="max-w-7xl mx-auto px-4 sm:px-6 md:px-8 lg:px-12 grid grid-cols-1 lg:grid-cols-3 gap-6">
```

**Breakdown:**
- `max-w-7xl` (80rem/1280px) - More reasonable max-width
- `px-4` - 16px horizontal padding on mobile (phones)
- `sm:px-6` - 24px on small tablets (640px+)
- `md:px-8` - 32px on medium tablets (768px+)
- `lg:px-12` - 48px on larger screens (1024px+)

---

### 2. Manual Section (Line 255)

**Current:**
```html
<section class="mt-12 max-w-[1400px] mx-auto px-4 lg:px-8" aria-labelledby="manual-calculo">
```

**Proposed:**
```html
<section class="mt-12 max-w-7xl mx-auto px-4 sm:px-6 md:px-8 lg:px-12" aria-labelledby="manual-calculo">
```

**Breakdown:**
- Same responsive padding as main section
- Consistent spacing across the page

---

### 3. Main Container (Line 65)

**Current:**
```html
<main class="flex-1 p-4 lg:p-8 overflow-y-auto">
```

**Proposed:**
```html
<main class="flex-1 overflow-y-auto">
```

**Breakdown:**
- Remove `p-4 lg:p-8` to avoid double padding
- Let the inner containers handle spacing

---

### 4. Header Padding (Line 51)

**Current:**
```html
<header class="flex items-center justify-between whitespace-nowrap border-b border-solid border-slate-200 dark:border-slate-800 bg-white dark:bg-slate-900 px-6 py-4 sticky top-0 z-50 shadow-sm">
```

**Proposed:**
```html
<header class="flex items-center justify-between whitespace-nowrap border-b border-solid border-slate-200 dark:border-slate-800 bg-white dark:bg-slate-900 px-4 sm:px-6 py-4 sticky top-0 z-50 shadow-sm">
```

**Breakdown:**
- `px-4` on mobile (16px)
- `sm:px-6` on small screens+ (24px)

---

## Tailwind Breakpoints Reference

| Breakpoint | Size | Device Type |
|------------|------|-------------|
| `default` | 0px+ | Mobile phones |
| `sm` | 640px+ | Large phones, small tablets |
| `md` | 768px+ | Tablets (portrait) |
| `lg` | 1024px+ | Tablets (landscape), small laptops |
| `xl` | 1280px+ | Desktops |

---

## Visual Impact

### Mobile (< 640px)
- 16px margins on both sides (32px total horizontal space)
- Blocks stacked vertically (already implemented)
- Content doesn't touch screen edges

### Tablet (640px - 1024px)
- 24-32px margins on both sides
- Still stacked vertically on portrait
- May show 2 columns on landscape (lg:grid-cols-3)

### Desktop (1024px+)
- 48px margins on both sides
- 3-column grid layout
- Maximum width of 1280px

---

## Implementation Steps

1. Modify main calculator grid container (line 66)
2. Modify manual section container (line 255)
3. Remove padding from main container (line 65)
4. Update header padding (line 51)
5. Verify responsive behavior on different screen sizes

---

## Files to Modify

- `index.html` - All changes in a single file

---

## Testing Checklist

- [ ] Verify on mobile phone (< 640px) - blocks stacked, 16px margins
- [ ] Verify on small tablet (640px-768px) - blocks stacked, 24px margins
- [ ] Verify on tablet (768px-1024px) - blocks stacked, 32px margins
- [ ] Verify on desktop (1024px+) - 3 columns, 48px margins
- [ ] Check horizontal scroll doesn't appear
- [ ] Ensure touch targets remain accessible
