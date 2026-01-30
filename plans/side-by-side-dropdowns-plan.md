# Plan: Place "Longe" and "Perto" Dropdowns Side by Side

## Objective
Modify the "Cálculo de Adição" block to display the "Longe" and "Perto" dropdowns side by side instead of vertically stacked.

## Current Structure
The "Cálculo de Adição" block (lines 253-348) currently has:
- Header section (lines 255-262)
- Content area with vertical layout:
  - "Longe" section (lines 264-297)
  - "Perto" section (lines 298-331)
  - Button and result section (lines 332-346)

## Proposed Changes

### 1. Wrap "Longe" and "Perto" sections in a grid container
- Create a new `div` wrapper with `grid grid-cols-1 sm:grid-cols-2 gap-4` classes
- This will:
  - Stack vertically on mobile (single column)
  - Display side by side on screens ≥640px (two columns)

### 2. Adjust spacing
- Reduce gap between the two sections from `gap-6` to `gap-4` for a tighter side-by-side layout
- Maintain `gap-6` between the grid container and the button/result section

## Implementation Details

### Before (Current):
```html
<div class="p-6 flex flex-col gap-6 flex-1">
    <div><!-- Longe section --></div>
    <div><!-- Perto section --></div>
    <div class="mt-auto pt-4"><!-- Button and result --></div>
</div>
```

### After (Proposed):
```html
<div class="p-6 flex flex-col gap-6 flex-1">
    <div class="grid grid-cols-1 sm:grid-cols-2 gap-4">
        <div><!-- Longe section --></div>
        <div><!-- Perto section --></div>
    </div>
    <div class="mt-auto pt-4"><!-- Button and result --></div>
</div>
```

## Responsive Behavior
- **Mobile (<640px)**: Dropdowns stack vertically (single column)
- **Tablet/Desktop (≥640px)**: Dropdowns display side by side (two columns)

## Files to Modify
- `public/index.html` - Lines 263-347 (the content area of "Cálculo de Adição" block)
