# Website Services - WS Small Y Modules

**Category:** Website Services - Small Y Suite
**Total Modules:** 16 submodules + 1 parent
**Parent Module:** ws_small_y
**Current Bootstrap:** 4.4.1
**Target Bootstrap:** 5.3.3
**Migration Phase:** Phase 2
**Sprints:** 4-6

---

## Overview

The WS Small Y suite is a collection of 16 submodules that provide content display components for Y USA sites. All modules share a common parent module (`ws_small_y`) and follow similar architectural patterns, making them ideal candidates for batch migration.

**Parent Module Location:** `docroot/modules/contrib/ws_small_y/`

**Key Characteristics:**
- Twig-based component rendering
- Bootstrap 4.4.1 dependencies
- Similar migration patterns across all submodules
- Primarily presentational (minimal custom JavaScript)
- Heavy use of Bootstrap utility classes

---

## Complete Module List

### 1. small_y_accordions

**Path:** `docroot/modules/contrib/ws_small_y/modules/small_y_accordions/`
**Bootstrap:** 4.4.1 → 5.3.3
**Sprint:** Sprint 4 (High Priority Batch 1)

**Description:** Accordion/collapse components for expandable content sections

**Bootstrap Components Used:**
- Accordion/Collapse
- Cards (accordion styling)

**Key Changes Needed:**
- `data-toggle="collapse"` → `data-bs-toggle="collapse"`
- `data-parent` → `data-bs-parent`
- `.card` structure changes
- Update collapse JavaScript initialization

**Migration Complexity:** MEDIUM
### 2. small_y_alerts

**Path:** `docroot/modules/contrib/ws_small_y/modules/small_y_alerts/`
**Bootstrap:** 4.4.1 → 5.3.3
**Sprint:** Sprint 4 (High Priority Batch 1)

**Description:** Alert/notification banners for important messages

**Bootstrap Components Used:**
- Alerts
- Close buttons

**Key Changes Needed:**
- `.alert` class structure unchanged (minimal changes)
- `data-dismiss="alert"` → `data-bs-dismiss="alert"`
- Close button markup updates

**Migration Complexity:** LOW
**Estimated Effort:** Quick migration (1-2 hours)

---

### 3. small_y_articles

**Path:** `docroot/modules/contrib/ws_small_y/modules/small_y_articles/`
**Bootstrap:** 4.4.1 → 5.3.3
**Sprint:** Sprint 5 (Medium Priority Batch 2)

**Description:** Article display with grid/list layouts

**Bootstrap Components Used:**
- Grid system
- Cards
- Media objects (deprecated in BS5)

**Key Changes Needed:**
- Replace `.media` with flex utilities
- Spacing utilities: `.mr-*` → `.me-*`, `.ml-*` → `.ms-*`
- Card structure updates if used

**Migration Complexity:** MEDIUM
### 4. small_y_branch

**Path:** `docroot/modules/contrib/ws_small_y/modules/small_y_branch/`
**Bootstrap:** 4.4.1 → 5.3.3
**Sprint:** Sprint 5 (Medium Priority Batch 2)

**Description:** Branch information display components

**Bootstrap Components Used:**
- Cards
- Grid system
- List groups

**Key Changes Needed:**
- Card structure updates
- Grid column classes: `.col-sm-*`, `.col-md-*` etc.
- List group item markup

**Migration Complexity:** MEDIUM
### 5. small_y_cards

**Path:** `docroot/modules/contrib/ws_small_y/modules/small_y_cards/`
**Bootstrap:** 4.4.1 → 5.3.3
**Sprint:** Sprint 4 (High Priority Batch 1)

**Description:** Card components for content display

**Bootstrap Components Used:**
- Cards (primary component)
- Grid system
- Images

**Key Changes Needed:**
- Card deck/group changes (`.card-deck` removed)
- `.card-columns` removed (use grid instead)
- Image overlay classes

**Migration Complexity:** MEDIUM-HIGH
**Special Considerations:**
- Card deck removal is a breaking change
- May need custom CSS for previous card-deck behavior
- Test responsive behavior thoroughly

---

### 6. small_y_carousels

**Path:** `docroot/modules/contrib/ws_small_y/modules/small_y_carousels/`
**Bootstrap:** 4.4.1 → 5.3.3
**Sprint:** Sprint 4 (High Priority Batch 1)

**Description:** Image/content carousels/sliders

**Bootstrap Components Used:**
- Carousel
- Indicators
- Controls

**Key Changes Needed:**
- `data-ride="carousel"` → `data-bs-ride="carousel"`
- `data-slide-to` → `data-bs-slide-to`
- Carousel JavaScript initialization
- Control button markup

**Migration Complexity:** MEDIUM
### 7. small_y_editor

**Path:** `docroot/modules/contrib/ws_small_y/modules/small_y_editor/`
**Bootstrap:** 4.4.1 → 5.3.3
**Sprint:** Sprint 5 (Medium Priority Batch 2)

**Description:** WYSIWYG content editor integration

**Bootstrap Components Used:**
- May include various components inserted via editor

**Key Changes Needed:**
- Update editor button configurations
- Review embedded component markup
- CKEditor integration updates

**Migration Complexity:** MEDIUM
### 8. small_y_events

**Path:** `docroot/modules/contrib/ws_small_y/modules/small_y_events/`
**Bootstrap:** 4.4.1 → 5.3.3
**Sprint:** Sprint 5 (Medium Priority Batch 2)

**Description:** Event listing and display components

**Bootstrap Components Used:**
- Cards
- List groups
- Grid system

**Key Changes Needed:**
- Card structure updates
- List group markup
- Grid column classes

**Migration Complexity:** MEDIUM
### 9. small_y_hero

**Path:** `docroot/modules/contrib/ws_small_y/modules/small_y_hero/`
**Bootstrap:** 4.4.1 → 5.3.3
**Sprint:** Sprint 4 (High Priority Batch 1)

**Description:** Hero/jumbotron banner components

**Bootstrap Components Used:**
- Jumbotron (removed in BS5!)
- Grid system
- Utilities

**Key Changes Needed:**
- Replace `.jumbotron` (removed in Bootstrap 5)
- Create custom jumbotron styles or use utilities
- Background image handling

**Migration Complexity:** HIGH
**Special Considerations:**
- Jumbotron component completely removed in Bootstrap 5
- Need custom CSS solution or utility class combination
- Reference: https://getbootstrap.com/docs/5.3/migration/#jumbotron

---

### 10. small_y_icon_grid

**Path:** `docroot/modules/contrib/ws_small_y/modules/small_y_icon_grid/`
**Bootstrap:** 4.4.1 → 5.3.3
**Sprint:** Sprint 5 (Medium Priority Batch 2)

**Description:** Icon grid display components

**Bootstrap Components Used:**
- Grid system
- Flex utilities
- Spacing utilities

**Key Changes Needed:**
- Grid column updates
- Flex utilities: align-items, justify-content
- Spacing: `.mr-*` → `.me-*`, `.ml-*` → `.ms-*`

**Migration Complexity:** LOW-MEDIUM
### 11. small_y_ping_pongs

**Path:** `docroot/modules/contrib/ws_small_y/modules/small_y_ping_pongs/`
**Bootstrap:** 4.4.1 → 5.3.3
**Sprint:** Sprint 5 (Medium Priority Batch 2)

**Description:** Alternating content blocks (text + image)

**Bootstrap Components Used:**
- Grid system
- Media objects (deprecated)
- Flex utilities

**Key Changes Needed:**
- Replace `.media` with flex utilities
- Grid row/column updates
- Order utilities for alternating layout

**Migration Complexity:** MEDIUM
### 12. small_y_search

**Path:** `docroot/modules/contrib/ws_small_y/modules/small_y_search/`
**Bootstrap:** 4.4.1 → 5.3.3
**Sprint:** Sprint 5 (Medium Priority Batch 2)

**Description:** Search interface components

**Bootstrap Components Used:**
- Forms
- Input groups
- Buttons

**Key Changes Needed:**
- Form control classes (minimal changes)
- Input group structure
- Button classes

**Migration Complexity:** LOW
### 13. small_y_tabs

**Path:** `docroot/modules/contrib/ws_small_y/modules/small_y_tabs/`
**Bootstrap:** 4.4.1 → 5.3.3
**Sprint:** Sprint 4 (High Priority Batch 1)

**Description:** Tab navigation components

**Bootstrap Components Used:**
- Nav tabs
- Tab content
- Tab panes

**Key Changes Needed:**
- `data-toggle="tab"` → `data-bs-toggle="tab"`
- Nav item/link structure
- Tab pane activation classes

**Migration Complexity:** MEDIUM
### 14. ws_small_y_staff

**Path:** `docroot/modules/contrib/ws_small_y/modules/ws_small_y_staff/`
**Bootstrap:** 4.4.1 → 5.3.3
**Sprint:** Sprint 5 (Medium Priority Batch 2)

**Description:** Staff member profile display

**Bootstrap Components Used:**
- Cards
- Grid system
- Modal (possibly for staff details)

**Key Changes Needed:**
- Card structure updates
- Grid column classes
- Modal data attributes if used

**Migration Complexity:** MEDIUM
### 15. ws_small_y_statistics

**Path:** `docroot/modules/contrib/ws_small_y/modules/ws_small_y_statistics/`
**Bootstrap:** 4.4.1 → 5.3.3
**Sprint:** Sprint 5 (Medium Priority Batch 2)

**Description:** Statistics/metrics display components

**Bootstrap Components Used:**
- Grid system
- Cards
- Utilities

**Key Changes Needed:**
- Card structure if used
- Grid column classes
- Spacing utilities

**Migration Complexity:** LOW-MEDIUM
### 16. ws_small_y_testimonials

**Path:** `docroot/modules/contrib/ws_small_y/modules/ws_small_y_testimonials/`
**Bootstrap:** 4.4.1 → 5.3.3
**Sprint:** Sprint 5 (Medium Priority Batch 2)

**Description:** Testimonial/quote display components

**Bootstrap Components Used:**
- Cards
- Blockquotes
- Grid system

**Key Changes Needed:**
- Card structure updates
- Blockquote footer (BS5 uses `.blockquote-footer`)
- Grid column classes

**Migration Complexity:** LOW-MEDIUM
## Migration Priority Grouping

### Sprint 4: High Priority Batch 1 (6 modules)

**Why High Priority:**
- Frequently used components
- Visible on most pages
- Interactive components requiring JavaScript updates

**Modules:**
1. small_y_hero (jumbotron removal - complex)
2. small_y_cards (card deck removal - complex)
3. small_y_carousels (interactive)
4. small_y_accordions (interactive)
5. small_y_alerts (simple, but commonly used)
6. small_y_tabs (interactive)

**Sprint Goal:** Migrate most visible/interactive components first

---

### Sprint 5: Medium Priority Batch 2 (10 modules)

**Why Medium Priority:**
- Less frequently used or simpler components
- Fewer interactive elements
- Follow patterns established in Sprint 4

**Modules:**
1. small_y_articles
2. small_y_branch
3. small_y_editor
4. small_y_events
5. small_y_icon_grid
6. small_y_ping_pongs
7. small_y_search
8. ws_small_y_staff
9. ws_small_y_statistics
10. ws_small_y_testimonials

**Sprint Goal:** Complete remaining small_y modules using batch patterns

---

## Common Migration Patterns

### Pattern 1: Data Attribute Updates

**Bootstrap 4:**
```html
<button data-toggle="collapse" data-target="#example">
<div data-ride="carousel">
<a data-toggle="tab" href="#tab1">
```

**Bootstrap 5:**
```html
<button data-bs-toggle="collapse" data-bs-target="#example">
<div data-bs-ride="carousel">
<a data-bs-toggle="tab" href="#tab1">
```

**Action:** Global find/replace in all `.twig` files

---

### Pattern 2: Spacing Utilities

**Bootstrap 4:**
```html
<div class="mr-3 ml-2 pr-4 pl-1">
```

**Bootstrap 5:**
```html
<div class="me-3 ms-2 pe-4 ps-1">
```

**Mapping:**
- `ml-*` → `ms-*` (margin-left → margin-start)
- `mr-*` → `me-*` (margin-right → margin-end)
- `pl-*` → `ps-*` (padding-left → padding-start)
- `pr-*` → `pe-*` (padding-right → padding-end)

---

### Pattern 3: Card Deck Replacement

**Bootstrap 4:**
```html
<div class="card-deck">
  <div class="card">...</div>
  <div class="card">...</div>
  <div class="card">...</div>
</div>
```

**Bootstrap 5:**
```html
<div class="row row-cols-1 row-cols-md-3 g-4">
  <div class="col">
    <div class="card h-100">...</div>
  </div>
  <div class="col">
    <div class="card h-100">...</div>
  </div>
  <div class="col">
    <div class="card h-100">...</div>
  </div>
</div>
```

**Action:** Replace all `.card-deck` with grid system

---

### Pattern 4: Media Object Replacement

**Bootstrap 4:**
```html
<div class="media">
  <img class="mr-3" src="...">
  <div class="media-body">
    <h5 class="mt-0">Title</h5>
    <p>Content</p>
  </div>
</div>
```

**Bootstrap 5:**
```html
<div class="d-flex">
  <img class="me-3 flex-shrink-0" src="...">
  <div class="flex-grow-1">
    <h5 class="mt-0">Title</h5>
    <p>Content</p>
  </div>
</div>
```

**Action:** Replace all `.media` with flex utilities

---

### Pattern 5: Jumbotron Replacement

**Bootstrap 4:**
```html
<div class="jumbotron">
  <h1 class="display-4">Hello, world!</h1>
  <p class="lead">This is a simple hero unit.</p>
</div>
```

**Bootstrap 5 Option 1 (Utilities):**
```html
<div class="bg-light p-5 rounded-3">
  <h1 class="display-4">Hello, world!</h1>
  <p class="lead">This is a simple hero unit.</p>
</div>
```

**Bootstrap 5 Option 2 (Custom CSS):**
```scss
.jumbotron {
  padding: 2rem 1rem;
  margin-bottom: 2rem;
  background-color: #e9ecef;
  border-radius: .3rem;

  @media (min-width: 576px) {
    padding: 4rem 2rem;
  }
}
```

**Action:** Choose approach and apply consistently

---

## Batch Migration Strategy

### Step 1: Setup (Sprint 4 Start)
1. Create feature branch for WS Small Y
2. Set up testing baseline for all 16 modules
3. Document current Bootstrap 4 behavior (screenshots)

### Step 2: Batch Processing
1. Apply Pattern 1 (data attributes) to all modules at once
2. Apply Pattern 2 (spacing utilities) to all modules at once
3. Handle component-specific changes per module

### Step 3: Testing
1. Visual regression testing per module
2. Interactive component testing (accordions, carousels, tabs)
3. Responsive testing at all breakpoints

### Step 4: Integration
1. Test all 16 modules together
2. Check for CSS conflicts
3. Verify no JavaScript errors

---

## Testing Requirements

### Visual Regression Testing
**Tool:** BackstopJS

**Test Scenarios per Module:**
- Desktop (1920x1080)
- Tablet (768x1024)
- Mobile (375x667)
- Interactive states (open/closed accordions, active tabs, etc.)

**Baseline:** Create before migration starts

---

### Accessibility Testing
**Tool:** Pa11y

**Requirements:**
- WCAG 2.2 Level AA compliance
- Keyboard navigation for interactive components
- Screen reader compatibility
- Color contrast verification

---

### Manual Testing Checklist

**For Each Module:**
- [ ] Displays correctly on desktop
- [ ] Displays correctly on tablet
- [ ] Displays correctly on mobile
- [ ] Interactive elements work (if applicable)
- [ ] No JavaScript console errors
- [ ] No CSS rendering issues
- [ ] Spacing/alignment matches Bootstrap 4 version
- [ ] Accessibility maintained

---

## Risk Assessment

### Risk 1: Card Deck Removal (MEDIUM-HIGH)
**Impact:** Visual layout changes in small_y_cards
**Mitigation:**
- Test grid replacement thoroughly
- Create custom CSS fallback if needed
- Document breaking changes for site builders

### Risk 2: Jumbotron Removal (MEDIUM-HIGH)
**Impact:** Hero component in small_y_hero requires complete refactor
**Mitigation:**
- Decide on utility vs custom CSS approach early
- Test across all themes
- Provide migration guide for custom implementations

### Risk 3: Media Object Removal (MEDIUM)
**Impact:** Affects small_y_articles, small_y_ping_pongs
**Mitigation:**
- Flex utility replacement is straightforward
- Test layout behavior thoroughly
- Check for edge cases (long text, large images)

### Risk 4: Batch Processing Errors (LOW-MEDIUM)
**Impact:** One broken module could block entire batch
**Mitigation:**
- Test each module individually before integration
- Use version control branches per module
- Maintain rollback capability

---

## Dependencies

### Before WS Small Y Migration:
- [x] Phase 1 complete (theme migrated to Bootstrap 5)
- [x] Testing infrastructure ready (BackstopJS, Pa11y)
- [x] Migration patterns documented

### After WS Small Y Migration (for other modules):
- [ ] All 16 small_y modules tested and working
- [ ] Batch migration patterns validated
- [ ] Common issues documented

---

## Success Criteria

### Technical Requirements:
- [ ] All 16 modules build without errors
- [ ] All modules display correctly at all breakpoints
- [ ] Interactive components functional (accordions, carousels, tabs)
- [ ] No JavaScript console errors
- [ ] Webpack builds successfully

### Quality Requirements:
- [ ] Visual regression tests pass (or changes documented)
- [ ] Accessibility maintained (WCAG 2.2 AA)
- [ ] Performance maintained or improved
- [ ] Code quality passes linting

### Documentation Requirements:
- [ ] Migration patterns documented
- [ ] Breaking changes documented
- [ ] Common issues and solutions documented

---

## Related Documents

**Phase Documentation:**
- [Phase 2: Website Services Modules](../phases/PHASE_2_WEBSITE_SERVICES.md)

**Sprint Documentation:**
- [Sprint 4: WS Small Y Batch 1](../sprints/SPRINT_04_WS_SmallY_Batch1.md)
- [Sprint 5: WS Small Y Batch 2](../sprints/SPRINT_05_WS_SmallY_Batch2.md)
- [Sprint 6: Other WS Modules](../sprints/SPRINT_06_WS_Other_Modules.md)

**Reference Materials:**
- [Bootstrap 5 Cheatsheet](../reference/BOOTSTRAP_5_CHEATSHEET.md)
- [Migration Checklist Template](../reference/MIGRATION_CHECKLIST_TEMPLATE.md)
- [Troubleshooting Guide](../reference/TROUBLESHOOTING.md)

**Testing Documentation:**
- [Testing Overview](../testing/TESTING_OVERVIEW.md)
- [Visual Regression Testing](../testing/TESTING_VISUAL_REGRESSION.md)
- [Accessibility Testing](../testing/TESTING_ACCESSIBILITY.md)

---

**Document Status:** ✅ Complete
**Last Updated:** 2025-10-17
**Modules Documented:** 16
**Total Lines:** < 999
