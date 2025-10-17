# Sprint 5: WS Small Y Batch 2

**Phase:** [Phase 2 - Component Migration](../phases/PHASE_2_COMPONENT_MIGRATION.md)
**Resources:** 1 Developer
**Status:** Not Started

---

## Sprint Goal

Migrate second batch of ws_small_y modules (10 modules) to Bootstrap 5, leveraging the established migration pattern from Sprint 4.

---

## Modules in This Sprint

1. **small_y_modals** - Modal dialog component
2. **small_y_buttons** - Button styles and groups
3. **small_y_breadcrumbs** - Breadcrumb navigation
4. **small_y_pagination** - Pagination component
5. **small_y_progress** - Progress bars
6. **small_y_badges** - Badge component
7. **small_y_tooltips** - Tooltip component
8. **small_y_popovers** - Popover component
9. **small_y_dropdowns** - Dropdown menus
10. **small_y_spinners** - Loading spinners

**Total:** 10 modules

---

## Pre-Sprint Preparation

### Checklist:
- [ ] Sprint 4 completed
- [ ] 6 modules from Batch 1 working
- [ ] Migration pattern validated
- [ ] Lessons learned from Sprint 4 reviewed

---

## Tasks

### Task 1: Module 7 - small_y_modals
**Owner:** Developer
**Priority:** HIGH

**Location:** `docroot/modules/contrib/ws_small_y/modules/small_y_modals/`

**Modal-Specific Updates:**
```twig
{# Bootstrap 4 #}
<div class="modal fade" tabindex="-1">
  <div class="modal-dialog">
    <button class="close" data-dismiss="modal">
      <span>&times;</span>
    </button>

{# Bootstrap 5 #}
<div class="modal fade" tabindex="-1">
  <div class="modal-dialog">
    <button class="btn-close" data-bs-dismiss="modal"></button>
```

**JavaScript:**
```javascript
import { Modal } from 'bootstrap';

const myModal = new Modal(document.getElementById('myModal'));
myModal.show();
```

**Key Changes:**
- `data-dismiss` → `data-bs-dismiss`
- `data-toggle` → `data-bs-toggle`
- `data-target` → `data-bs-target`
- `class="close"` → `class="btn-close"`
- Remove `<span>&times;</span>`

**Acceptance Criteria:**
- [ ] Module builds successfully
- [ ] Modals open/close correctly
- [ ] Close button works
- [ ] Backdrop click closes modal (if configured)
- [ ] ESC key closes modal
- [ ] Keyboard trap works (accessibility)
- [ ] Multiple modals supported

---

### Task 2: Module 8 - small_y_buttons
**Owner:** Developer
**Priority:** HIGH

**Location:** `docroot/modules/contrib/ws_small_y/modules/small_y_buttons/`

**Button-Specific Updates:**
```scss
// Bootstrap 4 - mostly same in BS5
.btn { }

// Button groups - verify classes
.btn-group { }
.btn-group-vertical { }

// Toggle buttons - CHANGED in BS5
// BS4 used data-toggle="button"
// BS5 uses data-bs-toggle="button"
```

**Template Updates:**
```twig
{# Bootstrap 4 #}
<button type="button" class="btn btn-primary" data-toggle="button">

{# Bootstrap 5 #}
<button type="button" class="btn btn-primary" data-bs-toggle="button">
```

**Acceptance Criteria:**
- [ ] Module builds successfully
- [ ] All button styles render correctly
- [ ] Button groups work
- [ ] Toggle buttons work
- [ ] Button states work (active, disabled)
- [ ] Icon buttons work

---

### Task 3: Module 9 - small_y_breadcrumbs
**Owner:** Developer
**Priority:** MEDIUM

**Location:** `docroot/modules/contrib/ws_small_y/modules/small_y_breadcrumbs/`

**Breadcrumb-Specific Updates:**
```twig
{# Bootstrap 4 & 5 - Mostly the same #}
<nav aria-label="breadcrumb">
  <ol class="breadcrumb">
    <li class="breadcrumb-item"><a href="/">Home</a></li>
    <li class="breadcrumb-item active" aria-current="page">Current</li>
  </ol>
</nav>
```

**Key Changes:**
- Minimal changes - mostly CSS updates
- Verify divider styles
- Ensure ARIA attributes correct

**Acceptance Criteria:**
- [ ] Module builds successfully
- [ ] Breadcrumbs display correctly
- [ ] Dividers display correctly
- [ ] Links work
- [ ] Active item styled correctly
- [ ] ARIA attributes correct

---

### Task 4: Module 10 - small_y_pagination
**Owner:** Developer
**Priority:** MEDIUM

**Location:** `docroot/modules/contrib/ws_small_y/modules/small_y_pagination/`

**Pagination-Specific Updates:**
```twig
{# Bootstrap 4 & 5 - Very similar #}
<nav aria-label="Page navigation">
  <ul class="pagination">
    <li class="page-item"><a class="page-link" href="#">Previous</a></li>
    <li class="page-item"><a class="page-link" href="#">1</a></li>
    <li class="page-item active"><a class="page-link" href="#">2</a></li>
    <li class="page-item"><a class="page-link" href="#">Next</a></li>
  </ul>
</nav>
```

**Key Changes:**
- Minimal changes
- Verify sizing classes (pagination-sm, pagination-lg)
- Verify disabled state styling

**Acceptance Criteria:**
- [ ] Module builds successfully
- [ ] Pagination displays correctly
- [ ] Links work
- [ ] Active state styled correctly
- [ ] Disabled state works
- [ ] Sizing variants work

---

### Task 5: Module 11 - small_y_progress
**Owner:** Developer
**Priority:** MEDIUM

**Location:** `docroot/modules/contrib/ws_small_y/modules/small_y_progress/`

**Progress-Specific Updates:**
```twig
{# Bootstrap 4 & 5 - Same structure #}
<div class="progress">
  <div class="progress-bar" role="progressbar" style="width: 75%"
       aria-valuenow="75" aria-valuemin="0" aria-valuemax="100">75%</div>
</div>
```

**Key Changes:**
- Structure unchanged
- Verify color variants
- Verify striped/animated variants
- Verify stacked progress bars

**Acceptance Criteria:**
- [ ] Module builds successfully
- [ ] Progress bars display correctly
- [ ] Color variants work
- [ ] Striped variant works
- [ ] Animated variant works
- [ ] Stacked bars work
- [ ] ARIA attributes correct

---

### Task 6: Module 12 - small_y_badges
**Owner:** Developer
**Priority:** LOW

**Location:** `docroot/modules/contrib/ws_small_y/modules/small_y_badges/`

**Badge-Specific Updates:**
```twig
{# Bootstrap 4 #}
<span class="badge badge-primary">Primary</span>

{# Bootstrap 5 #}
<span class="badge bg-primary">Primary</span>
```

**Key Changes:**
- `badge-{color}` → `bg-{color}` or `text-bg-{color}`
- Pill badges: `badge-pill` → `rounded-pill`

**Template Updates:**
```twig
{# Bootstrap 4 #}
<span class="badge badge-pill badge-primary">Pill</span>

{# Bootstrap 5 #}
<span class="badge rounded-pill bg-primary">Pill</span>
```

**Acceptance Criteria:**
- [ ] Module builds successfully
- [ ] Badges display correctly
- [ ] Color variants work
- [ ] Pill badges work
- [ ] Badge positioning works (in buttons, etc.)

---

### Task 7: Module 13 - small_y_tooltips
**Owner:** Developer
**Priority:** MEDIUM

**Location:** `docroot/modules/contrib/ws_small_y/modules/small_y_tooltips/`

**Tooltip-Specific Updates:**
```twig
{# Bootstrap 4 #}
<button data-toggle="tooltip" data-placement="top" title="Tooltip text">

{# Bootstrap 5 #}
<button data-bs-toggle="tooltip" data-bs-placement="top" title="Tooltip text">
```

**JavaScript:**
```javascript
import { Tooltip } from 'bootstrap';

// Initialize all tooltips
const tooltipTriggerList = document.querySelectorAll('[data-bs-toggle="tooltip"]');
const tooltipList = [...tooltipTriggerList].map(tooltipTriggerEl =>
  new Tooltip(tooltipTriggerEl)
);
```

**Key Changes:**
- `data-toggle` → `data-bs-toggle`
- `data-placement` → `data-bs-placement`
- Must manually initialize (not auto-initialized)

**Acceptance Criteria:**
- [ ] Module builds successfully
- [ ] Tooltips appear on hover/focus
- [ ] All placements work (top, bottom, left, right)
- [ ] Tooltips dismiss correctly
- [ ] Keyboard accessible
- [ ] ARIA attributes correct

---

### Task 8: Module 14 - small_y_popovers
**Owner:** Developer
**Priority:** MEDIUM

**Location:** `docroot/modules/contrib/ws_small_y/modules/small_y_popovers/`

**Popover-Specific Updates:**
```twig
{# Bootstrap 4 #}
<button data-toggle="popover" data-content="Popover content"
        data-placement="top" title="Popover title">

{# Bootstrap 5 #}
<button data-bs-toggle="popover" data-bs-content="Popover content"
        data-bs-placement="top" data-bs-title="Popover title">
```

**JavaScript:**
```javascript
import { Popover } from 'bootstrap';

// Initialize all popovers
const popoverTriggerList = document.querySelectorAll('[data-bs-toggle="popover"]');
const popoverList = [...popoverTriggerList].map(popoverTriggerEl =>
  new Popover(popoverTriggerEl)
);
```

**Key Changes:**
- `data-toggle` → `data-bs-toggle`
- `data-content` → `data-bs-content`
- `data-placement` → `data-bs-placement`
- `title` → `data-bs-title` (recommended)
- Must manually initialize

**Acceptance Criteria:**
- [ ] Module builds successfully
- [ ] Popovers appear on click/hover
- [ ] All placements work
- [ ] Popovers dismiss correctly
- [ ] HTML content works (if enabled)
- [ ] Keyboard accessible

---

### Task 9: Module 15 - small_y_dropdowns
**Owner:** Developer
**Priority:** HIGH

**Location:** `docroot/modules/contrib/ws_small_y/modules/small_y_dropdowns/`

**Dropdown-Specific Updates:**
```twig
{# Bootstrap 4 #}
<div class="dropdown">
  <button class="btn dropdown-toggle" data-toggle="dropdown">
    Dropdown
  </button>
  <div class="dropdown-menu">
    <a class="dropdown-item" href="#">Action</a>
  </div>
</div>

{# Bootstrap 5 #}
<div class="dropdown">
  <button class="btn dropdown-toggle" data-bs-toggle="dropdown">
    Dropdown
  </button>
  <ul class="dropdown-menu">
    <li><a class="dropdown-item" href="#">Action</a></li>
  </ul>
</div>
```

**Key Changes:**
- `data-toggle` → `data-bs-toggle`
- Dropdown menu can be `<ul>` with `<li>` items (better semantics)
- Verify dropdown directions (dropup, dropend, dropstart)

**JavaScript:**
```javascript
import { Dropdown } from 'bootstrap';

// Auto-initialized, but can manually control
const dropdown = new Dropdown(document.getElementById('myDropdown'));
```

**Acceptance Criteria:**
- [ ] Module builds successfully
- [ ] Dropdowns open/close correctly
- [ ] Click outside closes dropdown
- [ ] Keyboard navigation works
- [ ] All directions work (down, up, start, end)
- [ ] Dropdown dividers work
- [ ] Disabled items styled correctly

---

### Task 10: Module 16 - small_y_spinners
**Owner:** Developer
**Priority:** LOW

**Location:** `docroot/modules/contrib/ws_small_y/modules/small_y_spinners/`

**Spinner-Specific Updates:**
```twig
{# Bootstrap 4 & 5 - Similar, but BS5 added improvements #}
<div class="spinner-border" role="status">
  <span class="visually-hidden">Loading...</span>
</div>

<div class="spinner-grow" role="status">
  <span class="visually-hidden">Loading...</span>
</div>
```

**Key Changes:**
- `sr-only` → `visually-hidden`
- Verify color variants
- Verify sizing variants (spinner-border-sm)

**Acceptance Criteria:**
- [ ] Module builds successfully
- [ ] Border spinners work
- [ ] Grow spinners work
- [ ] Color variants work
- [ ] Sizing variants work
- [ ] ARIA attributes correct

---

### Task 11: Integration Testing - Batch 2
**Owner:** Developer
**Priority:** CRITICAL

**Actions:**
```bash
# Rebuild all modules
cd docroot/modules/contrib/ws_small_y/modules

for module in small_y_modals small_y_buttons small_y_breadcrumbs small_y_pagination small_y_progress small_y_badges small_y_tooltips small_y_popovers small_y_dropdowns small_y_spinners; do
  cd $module
  npm run build
  cd ..
done

# Clear Drupal cache
fin drush cr
```

**Test Scenarios:**
1. Test each module individually
2. Test modules together on same page
3. Test with Batch 1 modules (from Sprint 4)
4. Test interactions between components
5. Test responsive behavior
6. Test browser compatibility
7. Test accessibility

**Special Focus:**
- Tooltips and popovers on same page
- Modals with dropdowns inside
- Dropdowns in navigation
- Interactive components together

**Acceptance Criteria:**
- [ ] All 10 modules work individually
- [ ] All modules work together
- [ ] No conflicts with Batch 1 modules
- [ ] No CSS conflicts
- [ ] No JavaScript errors
- [ ] All interactions work correctly

---

### Task 12: Accessibility Testing - Batch 2
**Owner:** Developer
**Priority:** HIGH

**Actions:**
```bash
cd /private/var/www/YMCAWS_11/docs/bootstrap-5-migration/testing

# Run Pa11y on pages with new components
npx pa11y-ci --reporter html > pa11y-batch2.html
```

**Focus Areas:**
- Modal keyboard trap
- Tooltip/popover keyboard access
- Dropdown keyboard navigation
- Button states (disabled, active)
- Progress bar ARIA attributes
- Spinner ARIA attributes

**Manual Testing:**
- [ ] Keyboard navigation works for all components
- [ ] Screen reader announces components correctly
- [ ] Focus management correct (modals, dropdowns)
- [ ] Color contrast adequate for all variants

**Acceptance Criteria:**
- [ ] Pa11y tests pass (or issues documented)
- [ ] Keyboard navigation works
- [ ] Screen reader compatible
- [ ] No new accessibility issues
- [ ] WCAG 2.1 AA compliant

---

### Task 13: Visual Regression Testing - Batch 2
**Owner:** Developer
**Priority:** HIGH

**Actions:**
```bash
cd /private/var/www/YMCAWS_11/docs/bootstrap-5-migration/testing

# Update backstop.json with new test scenarios
npx backstop test
```

**Acceptance Criteria:**
- [ ] Visual regression tests executed
- [ ] Results reviewed
- [ ] Differences documented
- [ ] Critical issues fixed

---

### Task 14: Documentation - Batch 2
**Owner:** Developer
**Priority:** MEDIUM

**Actions:**
```bash
cd docs/bootstrap-5-migration/modules
```

**Create Module Documentation:**
For each module: `SMALL_Y_MODALS.md`, `SMALL_Y_BUTTONS.md`, etc.

**Update MIGRATION_LOG.md:**
```markdown
## Sprint 5 - WS Small Y Batch 2

### Completed Modules (10):
1. ✅ small_y_modals
2. ✅ small_y_buttons
3. ✅ small_y_breadcrumbs
4. ✅ small_y_pagination
5. ✅ small_y_progress
6. ✅ small_y_badges
7. ✅ small_y_tooltips
8. ✅ small_y_popovers
9. ✅ small_y_dropdowns
10. ✅ small_y_spinners

### Total Progress:
- Batch 1 (Sprint 4): 6 modules
- Batch 2 (Sprint 5): 10 modules
- **Total ws_small_y: 16 modules completed**

### Issues Encountered:
[Document any issues]

### Lessons Learned:
[Document lessons]
```

**Acceptance Criteria:**
- [ ] Individual module docs created
- [ ] MIGRATION_LOG.md updated
- [ ] Issues documented
- [ ] Progress tracked

---

## Testing

### Build Testing:
- [ ] All 10 modules build successfully
- [ ] No build errors or warnings

### Functional Testing:
- [ ] All interactive components work
- [ ] Tooltips/popovers initialize
- [ ] Modals open/close
- [ ] Dropdowns open/close
- [ ] Buttons respond correctly
- [ ] Progress bars display
- [ ] Spinners animate

### Accessibility Testing:
- [ ] Pa11y tests pass
- [ ] Keyboard navigation works
- [ ] Screen reader compatible
- [ ] Focus management correct

### Visual Testing:
- [ ] BackstopJS tests reviewed
- [ ] Components match design
- [ ] Responsive design works

### Browser Testing:
- [ ] Chrome/Edge
- [ ] Firefox
- [ ] Safari
- [ ] Mobile browsers

---

## Deliverables

### Must Have:
- [ ] 10 modules migrated to Bootstrap 5
- [ ] All modules build successfully
- [ ] All modules functional
- [ ] Integration testing complete
- [ ] Accessibility testing complete
- [ ] Documentation complete

### Nice to Have:
- [ ] Performance metrics
- [ ] Bundle size analysis
- [ ] Interaction patterns documented

---

## Risks

### Risk: JavaScript Initialization Conflicts
**Likelihood:** Medium
**Impact:** Medium
**Mitigation:** Test tooltips/popovers together, ensure proper initialization

### Risk: Modal Focus Trap Issues
**Likelihood:** Low
**Impact:** High (accessibility)
**Mitigation:** Test keyboard navigation thoroughly, verify Bootstrap 5 implementation

---

## Notes

### Important:
- This completes all small_y modules (16 total)
- Interactive components require extra testing
- Accessibility is critical for modals, tooltips, dropdowns
- Document initialization patterns for JavaScript components

### Tips:
- Test JavaScript components in isolation first
- Initialize components after DOM ready
- Test multiple instances on same page
- Test nested components (dropdown in modal, etc.)

---

## Sprint Review Checklist

At end of sprint, verify:
- [ ] All 10 modules completed
- [ ] Total 16 ws_small_y modules complete
- [ ] All tests passing
- [ ] Documentation complete
- [ ] Next sprint ready

---

## Navigation

- **Previous:** [Sprint 4 - WS Small Y Batch 1](SPRINT_04_WS_SmallY_Batch1.md)
- **Next:** [Sprint 6 - WS Other Modules](SPRINT_06_WS_Other_Modules.md)
- **Phase:** [Phase 2 - Component Migration](../phases/PHASE_2_COMPONENT_MIGRATION.md)
- **Overview:** [Executive Summary](../EXECUTIVE_SUMMARY.md)

---

**Sprint Status:** ⬜ Not Started
**Last Updated:** 2025-10-17
