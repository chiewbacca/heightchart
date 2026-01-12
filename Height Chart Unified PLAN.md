# Height Chart Unified Page Plan

## Overview

Combine `index.html` and `prediction.html` into a single page with a toggle between "Current" and "Prediction" modes, while improving visual appeal and cleaning up code.

---

## Implementation Steps

### 1. Add Toggle Component

**Location:** Below header, above children legend

**Design:** Segmented pill-style toggle

```html
<div class="view-toggle">
    <div class="toggle-container">
        <div class="toggle-slider"></div>
        <button class="toggle-option active" data-mode="current">Current</button>
        <button class="toggle-option" data-mode="prediction">Prediction</button>
    </div>
</div>
```

**Styling:** Rounded pill with sliding background indicator that smoothly animates between options.

---

### 2. Merge JavaScript

**Unified Data Structure:**
- Single `CHILDREN` object with all child data (name, dob, gender, color, measurements)
- CDC data tables for projections
- State object tracking current mode and child visibility

**Key Functions to Merge:**
- Keep: `calcAge()`, `formatAge()`, `findPercentile()`, `getHeightAtPercentile()`, `generateProjection()`
- Add: `setMode()`, `updateChartForMode()`, `updateToggleSlider()`

**Chart Strategy:**
- Always include all 8 datasets (4 actual + 4 projected)
- Hide projection datasets by default
- Toggle visibility and axis scales based on mode

---

### 3. Dynamic Content Updates

When mode changes, update:

| Element | Current Mode | Prediction Mode |
|---------|--------------|-----------------|
| Overline | "A Family Record - 2020-2025" | "Growth Projections to Adulthood" |
| Intro | "Measuring the heights..." | "Tracking heights by age with projected..." |
| X-axis | 0-12 years | 0-21 years |
| Y-axis | 70-160 cm | 70-200 cm |
| Chart legend | Hidden | Visible (solid/dashed) |
| Stats title | "Latest Measurements - December 2025" | "Projected Adult Heights at Age 20" |
| Stats content | Current height + age + growth note | Current + projected + percentile |
| Methodology | Hidden | Visible |
| Footer | "Hover over points..." | Extended description |

---

### 4. Animations & Transitions

- **Toggle slider:** CSS transition (0.3s cubic-bezier)
- **Chart scales:** Chart.js default animation (0.8s)
- **Stats section:** Crossfade transition (0.3s)
- **Methodology:** Height animation with max-height (0.5s)

---

### 5. Visual Enhancements (Subtle & Elegant)

**Micro-interactions:**
- Stat cards: Subtle lift (translateY -2px) + soft shadow on hover
- Child tags: Gentle scale (1.02) on hover
- Toggle: Smooth sliding pill indicator with easeOutQuart timing

**Transitions:**
- All interactive elements: 0.2-0.3s transitions
- Chart mode switch: Smooth axis scale animation
- Stats crossfade: Opacity + subtle translateY

**Shadows (light mode):**
```css
--shadow-subtle: 0 2px 8px rgba(45, 41, 38, 0.04);
--shadow-hover: 0 4px 12px rgba(45, 41, 38, 0.08);
```

**Shadows (dark mode):**
```css
--shadow-subtle: 0 2px 8px rgba(0, 0, 0, 0.15);
--shadow-hover: 0 4px 12px rgba(0, 0, 0, 0.25);
```

**Chart polish:**
- Maintain current clean line styling (no gradients)
- Smooth point hover enlargement
- Refined tooltip styling with consistent padding

---

### 6. Code Cleanup

**CSS:**
- Remove duplicate style rules between files
- Organize by section (layout, typography, components, animations)
- Use CSS custom properties consistently

**JavaScript:**
- Single initialization function
- Clear separation: data, chart, UI updates, event handlers
- Remove redundant dataset definitions

**HTML:**
- Use semantic IDs for dynamic elements
- Single stats grid with both views (toggle visibility)
- Clean indentation

---

## Files to Modify

- **[index.html](index.html)** - Becomes the unified page
- **[prediction.html](prediction.html)** - Can be deleted after merge

---

## Verification

**Test the changes by:**
1. Open `index.html` in a browser
2. Click toggle between "Current" and "Prediction" modes
3. Verify chart scales animate smoothly
4. Verify projection lines appear/disappear
5. Verify stats content switches appropriately
6. Verify methodology shows in prediction mode only
7. Test child visibility toggles in both modes
8. Test dark mode (system preference or browser devtools)
9. Test on mobile viewport (320px width)
