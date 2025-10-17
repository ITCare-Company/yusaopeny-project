# Bootstrap 5 Migration - Layout Builder Modules Details

**Module Category:** Layout Builder Components
**Total Modules:** 20 (1 complete, 19 to migrate)
**Priority:** HIGH
**Phase:** Phase 3 (Sprints 8-13)
**Status:** 1/20 Complete (lb_accordion)

---

## Overview

Layout Builder modules provide page-building

 capabilities with drag-and-drop components. These modules range from simple display components to complex interactive elements with JavaScript, forms, and external integrations.

**Key Challenge:** Many modules use Bootstrap JavaScript components (modals, carousels, tabs) that have significant API changes in Bootstrap 5.

**Key Strategy:** Group by complexity, migrate simple components first, then tackle JavaScript-heavy components.

---

## Module Inventory

### ✅ Already Migrated (1 module)

#### lb_accordion
- **Path:** `docroot/modules/contrib/lb_accordion`
- **Bootstrap:** 5.3.3 ✅
- **Status:** Complete - USE AS REFERENCE
- **Notes:** Fully migrated to Bootstrap 5, Webpack 5

**Reference Implementation Files:**
```
docroot/modules/contrib/lb_accordion/
├── package.json          # Bootstrap 5.3.3, @popperjs/core 2.11.8
├── webpack.config.js     # Webpack 5 configuration
├── scss/                 # Bootstrap 5 SCSS
│   └── style.scss
├── templates/            # Bootstrap 5 templates (data-bs-*)
│   └── *.html.twig
├── js/                   # Bootstrap 5 JavaScript
└── lb_accordion.libraries.yml
```

**Use lb_accordion as reference for:**
- package.json structure
- Webpack 5 configuration
- SCSS compilation
- Template updates
- Library configuration
- Build scripts

---

### ❌ Need Migration (19 modules)

## Simple Components (10 modules) - Sprints 8-9

These modules are primarily template-based with minimal or no JavaScript.

### 1. lb_banner
- **Path:** `docroot/modules/contrib/lb_banner`
- **Priority:** MEDIUM
- **Sprint:** Sprint 8
- **Complexity:** LOW
- **JavaScript:** Minimal
- **Description:** Banner display component
- **Key Files:**
  - `scss/banner.scss`
  - `templates/lb-banner.html.twig`
- **Migration Notes:**
  - Update template classes
  - Test responsive behavior
  - Verify image scaling

### 2. lb_breaker
- **Path:** `docroot/modules/contrib/lb_breaker`
- **Priority:** LOW
- **Sprint:** Sprint 8
- **Complexity:** LOW
- **JavaScript:** None
- **Description:** Visual section breaks / dividers
- **Key Files:**
  - `scss/breaker.scss`
  - `templates/lb-breaker.html.twig`
- **Migration Notes:**
  - Simple CSS updates
  - Spacing utilities may change

### 3. lb_cards
- **Path:** `docroot/modules/contrib/lb_cards`
- **Priority:** CRITICAL
- **Sprint:** Sprint 8
- **Complexity:** MEDIUM
- **JavaScript:** Minimal
- **Description:** Card layouts for content display
- **Key Files:**
  - `scss/cards.scss`
  - `templates/lb-cards.html.twig`
  - `templates/lb-cards-card.html.twig`
- **Migration Notes:**
  - `.card-deck` removed in BS5 (use grid instead)
  - Card image positioning may change
  - Test various card configurations
- **Special Attention:**
  - `.card-deck` → grid system with `.row` and `.col-*`

### 4. lb_grid_content
- **Path:** `docroot/modules/contrib/lb_grid_content`
- **Priority:** MEDIUM
- **Sprint:** Sprint 9
- **Complexity:** MEDIUM
- **JavaScript:** None
- **Description:** Grid-based content layouts
- **Key Files:**
  - `scss/grid-content.scss`
  - `templates/lb-grid-content.html.twig`
- **Migration Notes:**
  - `.no-gutters` → `.g-0`
  - New `.xxl` breakpoint available
  - Test grid at all breakpoints

### 5. lb_header_footer
- **Path:** `docroot/modules/contrib/lb_header_footer`
- **Priority:** MEDIUM
- **Sprint:** Sprint 8
- **Complexity:** LOW
- **JavaScript:** None
- **Description:** Custom header/footer components
- **Key Files:**
  - `scss/header-footer.scss`
  - `templates/lb-header.html.twig`
  - `templates/lb-footer.html.twig`
- **Migration Notes:**
  - Update spacing utilities
  - Test responsive behavior

### 6. lb_icon_grid
- **Path:** `docroot/modules/contrib/lb_icon_grid`
- **Priority:** MEDIUM
- **Sprint:** Sprint 9
- **Complexity:** MEDIUM
- **JavaScript:** None
- **Description:** Icon grid layouts
- **Key Files:**
  - `scss/icon-grid.scss`
  - `templates/lb-icon-grid.html.twig`
- **Migration Notes:**
  - Grid system changes
  - Icon alignment utilities
  - Test responsive columns

### 7. lb_ping_pong
- **Path:** `docroot/modules/contrib/lb_ping_pong`
- **Priority:** MEDIUM
- **Sprint:** Sprint 9
- **Complexity:** MEDIUM
- **JavaScript:** None
- **Description:** Alternating content blocks (image left, text right, etc.)
- **Key Files:**
  - `scss/ping-pong.scss`
  - `templates/lb-ping-pong.html.twig`
- **Migration Notes:**
  - `.media` component removed (use flexbox)
  - `.float-left` → `.float-start`
  - `.float-right` → `.float-end`
  - Test image/text alternation

### 8. lb_stat
- **Path:** `docroot/modules/contrib/lb_stat`
- **Priority:** MEDIUM
- **Sprint:** Sprint 8
- **Complexity:** LOW
- **JavaScript:** None
- **Description:** Statistics display component
- **Key Files:**
  - `scss/stat.scss`
  - `templates/lb-stat.html.twig`
- **Migration Notes:**
  - Typography utilities
  - Display classes
  - Test number formatting

### 9. lb_table
- **Path:** `docroot/modules/contrib/lb_table`
- **Priority:** MEDIUM
- **Sprint:** Sprint 9
- **Complexity:** MEDIUM
- **JavaScript:** None
- **Description:** Table component
- **Key Files:**
  - `scss/table.scss`
  - `templates/lb-table.html.twig`
- **Migration Notes:**
  - **CRITICAL:** Nested tables no longer inherit styles
  - `.thead-light` → `.table-light`
  - `.thead-dark` → `.table-dark`
  - Test responsive tables

### 10. lb_text
- **Path:** `docroot/modules/contrib/lb_text`
- **Priority:** LOW
- **Sprint:** Sprint 8
- **Complexity:** LOW
- **JavaScript:** None
- **Description:** Text block component
- **Key Files:**
  - `scss/text.scss`
  - `templates/lb-text.html.twig`
- **Migration Notes:**
  - Typography utilities
  - Text alignment (`.text-start`, `.text-end`)
  - Simple migration

---

## Interactive Components (7 modules) - Sprints 10-11

These modules have significant JavaScript and Bootstrap component interactions.

### 11. lb_carousel
- **Path:** `docroot/modules/contrib/lb_carousel`
- **Priority:** CRITICAL
- **Sprint:** Sprint 10
- **Complexity:** HIGH
- **JavaScript:** HEAVY
- **Description:** Image/content carousels
- **Key Files:**
  - `scss/carousel.scss`
  - `templates/lb-carousel.html.twig`
  - `js/carousel.js`
- **Migration Notes:**
  - **CRITICAL:** Carousel JavaScript API changed significantly
  - Data attributes: `data-slide` → `data-bs-slide`
  - JavaScript: `.carousel()` → `new bootstrap.Carousel()`
  - Test touch/swipe on mobile
  - Test keyboard controls (arrow keys)
  - Test auto-play behavior
  - Test pause on hover
- **Special Attention:**
  ```javascript
  // Bootstrap 4
  $('.carousel').carousel({
    interval: 5000,
    pause: 'hover'
  });

  // Bootstrap 5
  import { Carousel } from 'bootstrap';
  const carouselEl = document.querySelector('.carousel');
  const carousel = new Carousel(carouselEl, {
    interval: 5000,
    pause: 'hover'
  });
  ```

### 12. lb_gallery_cards
- **Path:** `docroot/modules/contrib/lb_gallery_cards`
- **Priority:** MEDIUM
- **Sprint:** Sprint 10
- **Complexity:** MEDIUM
- **JavaScript:** MEDIUM
- **Description:** Gallery with lightbox/modal functionality
- **Key Files:**
  - `scss/gallery-cards.scss`
  - `templates/lb-gallery-cards.html.twig`
  - `js/gallery.js`
- **Migration Notes:**
  - Card layout changes
  - Modal integration (if used)
  - Lightbox JavaScript updates
  - Test image loading
  - Test modal interactions

### 13. lb_modal
- **Path:** `docroot/modules/contrib/lb_modal`
- **Priority:** CRITICAL
- **Sprint:** Sprint 11
- **Complexity:** HIGH
- **JavaScript:** HEAVY
- **Description:** Modal dialog component
- **Key Files:**
  - `scss/modal.scss`
  - `templates/lb-modal.html.twig`
  - `js/modal.js`
- **Migration Notes:**
  - **CRITICAL:** Modal API changed significantly
  - Data attributes: `data-toggle="modal"` → `data-bs-toggle="modal"`
  - JavaScript: `.modal('show')` → `bootstrap.Modal.getInstance().show()`
  - Test open/close via button
  - Test open/close via JavaScript
  - Test ESC key closes modal
  - Test backdrop click closes modal
  - Test focus trap (Tab cycles within modal)
  - Test with Drupal's dialog system (potential conflicts)
- **Special Attention:**
  ```javascript
  // Bootstrap 4
  $('#myModal').modal('show');
  $('#myModal').on('show.bs.modal', function (e) {
    // Do something
  });

  // Bootstrap 5
  const modalEl = document.getElementById('myModal');
  const modal = new bootstrap.Modal(modalEl);
  modal.show();
  modalEl.addEventListener('show.bs.modal', event => {
    // Do something
  });
  ```

### 14. lb_promo_card
- **Path:** `docroot/modules/contrib/lb_promo_card`
- **Priority:** MEDIUM
- **Sprint:** Sprint 11
- **Complexity:** MEDIUM
- **JavaScript:** MEDIUM
- **Description:** Promotional cards with interactions (hover, click)
- **Key Files:**
  - `scss/promo-card.scss`
  - `templates/lb-promo-card.html.twig`
  - `js/promo-card.js`
- **Migration Notes:**
  - Card component changes
  - Interaction JavaScript
  - Test hover effects
  - Test click interactions
  - Test card animations

### 15. lb_search
- **Path:** `docroot/modules/contrib/lb_search`
- **Priority:** MEDIUM
- **Sprint:** Sprint 11
- **Complexity:** MEDIUM
- **JavaScript:** MEDIUM
- **Description:** Search component with form
- **Key Files:**
  - `scss/search.scss`
  - `templates/lb-search.html.twig`
  - `js/search.js`
- **Migration Notes:**
  - Form class changes (`.form-group` → `.mb-3`)
  - Input group changes (no prepend/append wrappers)
  - Search button styling
  - Test form submission
  - Test AJAX search (if used)

### 16. lb_tabs
- **Path:** `docroot/modules/contrib/lb_tabs`
- **Priority:** HIGH
- **Sprint:** Sprint 10
- **Complexity:** HIGH
- **JavaScript:** HEAVY
- **Description:** Tab navigation component
- **Key Files:**
  - `scss/tabs.scss`
  - `templates/lb-tabs.html.twig`
  - `js/tabs.js`
- **Migration Notes:**
  - **CRITICAL:** Tab API changed
  - Data attributes: `data-toggle="tab"` → `data-bs-toggle="tab"`
  - JavaScript: `.tab('show')` → `new bootstrap.Tab().show()`
  - Test tab switching via click
  - Test tab switching via keyboard (Arrow keys)
  - Test deep linking to tabs
  - Test multiple tab sets on same page
- **Special Attention:**
  ```javascript
  // Bootstrap 4
  $('#myTab a').on('click', function (e) {
    e.preventDefault();
    $(this).tab('show');
  });

  // Bootstrap 5
  document.querySelectorAll('#myTab button').forEach(triggerEl => {
    triggerEl.addEventListener('click', event => {
      event.preventDefault();
      const tab = new bootstrap.Tab(triggerEl);
      tab.show();
    });
  });
  ```

### 17. ws_lb_tabs (different from lb_tabs)
- **Path:** `docroot/modules/contrib/ws_lb_tabs`
- **Priority:** MEDIUM
- **Sprint:** Sprint 11 (or Sprint 6 with WS modules)
- **Complexity:** HIGH
- **JavaScript:** HEAVY
- **Description:** Website Services tab component (separate from lb_tabs)
- **Migration Notes:**
  - Similar to lb_tabs
  - May have different styling
  - Coordinate with WS modules or LB modules phase

---

## Form Components (2 modules) - Sprint 12

These modules involve forms with JavaScript and potentially date pickers.

### 18. lb_group_schedules
- **Path:** `docroot/modules/contrib/lb_group_schedules`
- **Priority:** HIGH
- **Sprint:** Sprint 12
- **Complexity:** HIGH
- **JavaScript:** HEAVY
- **Description:** Schedule forms with date picker
- **Key Files:**
  - `scss/group-schedules.scss`
  - `templates/lb-group-schedules.html.twig`
  - `js/group-schedules.js`
- **Migration Notes:**
  - **CRITICAL:** Date picker replacement needed
  - Form class changes (`.form-group` → `.mb-3`)
  - `.custom-select` → `.form-select`
  - Input group changes
  - Replace tempusdominus date picker
  - Test date selection
  - Test form validation
  - Test form submission
- **Date Picker Options (from Phase 1 decision):**
  1. **Flatpickr** (recommended - lightweight, accessible)
  2. **Tempus Dominus 6** (Bootstrap 5 version)
  3. **Native HTML5 date input** (fallback)

### 19. lb_webform
- **Path:** `docroot/modules/contrib/lb_webform`
- **Priority:** CRITICAL
- **Sprint:** Sprint 12
- **Complexity:** HIGH
- **JavaScript:** MEDIUM
- **Description:** Webform integration with Layout Builder
- **Key Files:**
  - `scss/webform.scss`
  - `templates/lb-webform.html.twig`
  - `js/webform.js` (if any)
- **Migration Notes:**
  - **CRITICAL:** Form class changes throughout
  - `.form-group` → `.mb-3`
  - `.custom-select` → `.form-select`
  - `.custom-checkbox` → `.form-check`
  - `.custom-radio` → `.form-check`
  - `.custom-file` → native file input (styled differently)
  - `.input-group-prepend` / `.input-group-append` → simplified
  - Coordinate with webform_bootstrap module
  - Test all form element types (text, select, checkbox, radio, file, textarea, etc.)
  - Test form validation
  - Test form submission (including AJAX)
  - Test error states
  - Test required field indicators
- **Special Attention:**
  ```html
  <!-- Bootstrap 4 -->
  <div class="form-group">
    <label>Email</label>
    <input type="email" class="form-control">
  </div>

  <select class="custom-select">
    <option>Choose...</option>
  </select>

  <div class="custom-control custom-checkbox">
    <input type="checkbox" class="custom-control-input" id="check1">
    <label class="custom-control-label" for="check1">Check me</label>
  </div>

  <!-- Bootstrap 5 -->
  <div class="mb-3">
    <label class="form-label">Email</label>
    <input type="email" class="form-control">
  </div>

  <select class="form-select">
    <option>Choose...</option>
  </select>

  <div class="form-check">
    <input type="checkbox" class="form-check-input" id="check1">
    <label class="form-check-label" for="check1">Check me</label>
  </div>
  ```

---

## Common Patterns Across All LB Modules

### Standard Migration Process (per module)

#### Step 1: Update Dependencies
```bash
cd docroot/modules/contrib/[MODULE_NAME]

# Update package.json
npm install bootstrap@^5.3.3 @popperjs/core@^2.11.8 --save

# Update build tools (follow lb_accordion pattern)
npm install webpack@^5.91.0 webpack-cli@^5.1.4 --save-dev
npm install sass@^1.75.0 sass-loader@^14.2.0 --save-dev
npm install css-loader@^7.1.1 style-loader@^4.0.0 --save-dev
npm install mini-css-extract-plugin@^2.8.1 --save-dev

# Install
npm install
```

#### Step 2: Update Webpack Config
Copy pattern from lb_accordion `webpack.config.js`

**Key changes:**
- mode: 'production'
- Webpack 5 syntax
- MiniCssExtractPlugin configuration
- sass-loader configuration
- PurgeCSS (optional)

#### Step 3: Update SCSS Files
**Common replacements:**
- `.ml-*` → `.ms-*`
- `.mr-*` → `.me-*`
- `.text-left` → `.text-start`
- `.text-right` → `.text-end`
- `.close` → `.btn-close`
- `.no-gutters` → `.g-0`
- `.form-group` → `.mb-3`
- `.custom-select` → `.form-select`

#### Step 4: Update Templates
**Automated replacements:**
```bash
find templates/ -name "*.twig" -exec sed -i.bak \
  -e 's/data-toggle="/data-bs-toggle="/g' \
  -e 's/data-target="/data-bs-target="/g' \
  -e 's/data-dismiss="/data-bs-dismiss="/g' \
  -e 's/data-slide="/data-bs-slide="/g' \
  -e 's/data-parent="/data-bs-parent="/g' \
  {} +
```

**Manual updates:**
- `.btn-block` → `.d-grid` wrapper
- `.form-group` → margin utilities
- `.custom-*` form elements → `.form-*`
- Input groups (remove prepend/append wrappers)

#### Step 5: Update JavaScript (if any)
**For interactive components:**
- Update Bootstrap component initialization
- Convert jQuery to vanilla JS
- Update event listeners
- Test all interactions

#### Step 6: Update Libraries YAML
```yaml
# [module_name].libraries.yml
module_library:
  version: 2.0  # Increment for Bootstrap 5
  css:
    theme:
      dist/style.css: {}
  js:
    dist/bundle.js: {}
  dependencies:
    - core/drupal
    - core/once
```

#### Step 7: Build and Test
```bash
# Build
npm run build

# Clear Drupal cache
fin drush cr

# Test module functionality
# - Visual appearance
# - Interactive behavior (if any)
# - Responsive design
# - Accessibility
```

#### Step 8: Document
- Update module README.md
- Document any breaking changes
- Add to migration log
- Note any special considerations

---

## Batch Migration Strategy

### Sprint 8: Simple Batch 1 (6 modules)
**Approach:** Parallel migration
- lb_banner
- lb_breaker
- lb_cards
- lb_header_footer
- lb_stat
- lb_text

**Strategy:**
- All are template-focused
- Minimal/no JavaScript
- Can be done in parallel by one developer or split with contractor
- Test together at end of sprint

### Sprint 9: Simple Batch 2 (4 modules)
**Approach:** Parallel migration
- lb_grid_content
- lb_icon_grid
- lb_ping_pong
- lb_table

**Strategy:**
- Similar to Sprint 8
- lb_table needs special attention (nested tables)
- Test grid layouts thoroughly

### Sprint 10: Interactive Batch 1 (4 modules)
**Approach:** Sequential or parallel (depending on complexity)
- lb_accordion (reference - already done)
- lb_carousel (high priority)
- lb_tabs (high priority)
- lb_gallery_cards (medium priority)

**Strategy:**
- Study lb_accordion first
- Carousel and tabs need careful JavaScript migration
- Test interactive components thoroughly
- Allocate extra time for JavaScript debugging

### Sprint 11: Interactive Batch 2 (3 modules)
**Approach:** Sequential (high complexity)
- lb_modal (CRITICAL)
- lb_search
- lb_promo_card

**Strategy:**
- lb_modal is most critical (API changes significant)
- Test modal with Drupal's dialog system
- Test all event listeners
- Thorough JavaScript testing

### Sprint 12: Form Components (2 modules)
**Approach:** Sequential
- lb_webform (first)
- lb_group_schedules (second - includes date picker)

**Strategy:**
- lb_webform first (more critical)
- Coordinate with webform_bootstrap module
- Replace date picker in lb_group_schedules
- Test all form elements
- Test form validation and submission

### Sprint 13: Integration Testing & Date Picker Replacement
**Approach:** Testing and cleanup
- Test all 19 LB modules together
- Replace date picker (if not done in Sprint 12)
- Fix any bugs found
- Complete documentation

---

## Interactive Components - JavaScript API Changes

### Modal API
```javascript
// Bootstrap 4
$('#myModal').modal('show');
$('#myModal').modal('hide');
$('#myModal').modal('toggle');
$('#myModal').on('show.bs.modal', function (e) {
  // Event handler
});

// Bootstrap 5
const modal = new bootstrap.Modal(document.getElementById('myModal'));
modal.show();
modal.hide();
modal.toggle();

// Or use getInstance
const modal = bootstrap.Modal.getInstance(document.getElementById('myModal'));
if (modal) {
  modal.show();
}

// Event listener
const modalEl = document.getElementById('myModal');
modalEl.addEventListener('show.bs.modal', event => {
  // Event handler
});
```

### Carousel API
```javascript
// Bootstrap 4
$('.carousel').carousel({
  interval: 5000,
  pause: 'hover',
  wrap: true,
  keyboard: true
});
$('.carousel').carousel('cycle');
$('.carousel').carousel('pause');

// Bootstrap 5
import { Carousel } from 'bootstrap';
const carouselEl = document.querySelector('.carousel');
const carousel = new Carousel(carouselEl, {
  interval: 5000,
  pause: 'hover',
  wrap: true,
  keyboard: true
});
carousel.cycle();
carousel.pause();
```

### Tab API
```javascript
// Bootstrap 4
$('#myTab a').on('click', function (e) {
  e.preventDefault();
  $(this).tab('show');
});

// Bootstrap 5
document.querySelectorAll('#myTab button').forEach(triggerEl => {
  triggerEl.addEventListener('click', event => {
    event.preventDefault();
    const tab = new bootstrap.Tab(triggerEl);
    tab.show();
  });
});

// Or use data attributes (auto-initialized)
<button data-bs-toggle="tab" data-bs-target="#profile">Profile</button>
```

### Collapse API (for accordions)
```javascript
// Bootstrap 4
$('#myCollapse').collapse('toggle');
$('#myCollapse').collapse('show');
$('#myCollapse').collapse('hide');

// Bootstrap 5
const collapse = new bootstrap.Collapse(document.getElementById('myCollapse'));
collapse.toggle();
collapse.show();
collapse.hide();

// Or use data attributes (auto-initialized)
<button data-bs-toggle="collapse" data-bs-target="#myCollapse">Toggle</button>
```

---

## Testing Requirements

### Standard Testing (All Modules)
- [ ] Build completes without errors
- [ ] Visual appearance matches Bootstrap 4 (or approved differences)
- [ ] Responsive at all breakpoints (sm, md, lg, xl, xxl)
- [ ] Cross-browser compatible (Chrome, Firefox, Safari, Edge)
- [ ] BackstopJS visual regression passed
- [ ] Pa11y accessibility passed

### Enhanced Testing (Interactive Components)
**Additional tests for lb_carousel, lb_modal, lb_tabs, lb_gallery_cards:**
- [ ] JavaScript functionality works
- [ ] Keyboard navigation functional (Tab, Enter, Esc, Arrow keys)
- [ ] Touch/gesture testing (mobile)
- [ ] Event listeners working
- [ ] No memory leaks (Chrome DevTools)
- [ ] State management correct (open/close, show/hide)
- [ ] Multiple instances on same page

### Form Testing (lb_webform, lb_group_schedules)
- [ ] All form element types work (text, select, checkbox, radio, file, textarea)
- [ ] Form validation works
- [ ] Form submission works (including AJAX)
- [ ] Error states display correctly
- [ ] Required field indicators present
- [ ] Date picker functional (if applicable)
- [ ] Keyboard accessibility for forms

### Integration Testing (Sprint 13)
- [ ] Multiple LB components on same page
- [ ] Nested components (if applicable)
- [ ] Modal + carousel + tabs on same page
- [ ] Form submissions with other components
- [ ] AJAX interactions
- [ ] Drupal dialog interactions
- [ ] Layout Builder admin interface still works

---

## Special Considerations

### 1. lb_accordion as Reference
- **Always** refer to lb_accordion for patterns
- Copy webpack config
- Copy package.json structure
- Follow same SCSS patterns
- Use same build scripts

### 2. Modal and Drupal Dialogs
- Test lb_modal with Drupal's core dialog system
- Check for event listener conflicts
- Verify z-index stacking
- Test nested modals (if used)

### 3. Date Picker Replacement
- Decision made in Phase 1 Sprint 1
- Likely: Flatpickr (lightweight, accessible)
- Alternative: Tempus Dominus 6 (Bootstrap 5 version)
- Fallback: Native HTML5 date input
- Test with all browsers
- Test mobile date picker
- Test accessibility

### 4. Card Deck Removal
- `.card-deck` removed in Bootstrap 5
- Use grid system: `.row` with `.col-*`
- Test card spacing
- Test responsive card layouts

### 5. Table Nested Styles
- Nested tables no longer inherit styles in Bootstrap 5
- Must explicitly add table classes to nested tables
- Test any modules with nested tables

### 6. Form Class Changes
- Most significant changes in lb_webform
- `.form-group` → `.mb-3` (margin-bottom 3)
- `.custom-*` → `.form-*`
- Input groups simplified (no wrappers)
- Test all form variations

---

## Dependencies

### Before Phase 3 Can Start:
- [x] Phase 1 complete (theme migrated to BS5)
- [x] Phase 2 complete (WS modules migrated to BS5)
- [x] Testing infrastructure working (BackstopJS, Pa11y)
- [x] Date picker replacement chosen (from Phase 1 Sprint 1)
- [ ] GO/NO-GO decision from Phase 2

### Before Phase 4 Can Start:
- [ ] All 19 LB modules migrated to BS5
- [ ] Interactive components fully functional
- [ ] Date picker replaced and tested
- [ ] Integration testing passed
- [ ] Visual regression tests passed
- [ ] Accessibility tests passed
- [ ] GO/NO-GO decision approved

---

## Sprint Assignments

- **Sprint 8:** lb_banner, lb_breaker, lb_cards, lb_header_footer, lb_stat, lb_text (6 modules)
- **Sprint 9:** lb_grid_content, lb_icon_grid, lb_ping_pong, lb_table (4 modules)
- **Sprint 10:** lb_carousel, lb_tabs, lb_gallery_cards (3 modules + lb_accordion reference)
- **Sprint 11:** lb_modal, lb_search, lb_promo_card (3 modules)
- **Sprint 12:** lb_webform, lb_group_schedules (2 modules)
- **Sprint 13:** Integration testing, date picker replacement, bug fixes, documentation

**Total:** 19 modules over 6 sprints (12 weeks)

---

## Success Criteria

### Technical
- [ ] All 19 modules migrated to Bootstrap 5.3.3
- [ ] All modules build without errors
- [ ] All JavaScript components functional
- [ ] Modal, carousel, tab APIs updated to Bootstrap 5
- [ ] Date picker replaced (tempusdominus removed)
- [ ] No JavaScript console errors
- [ ] No jQuery dependencies added (except Drupal core)

### Quality
- [ ] Visual regression tests passed (all modules)
- [ ] Accessibility maintained (WCAG 2.2 AA)
- [ ] Interactive components keyboard-accessible
- [ ] Focus states maintained
- [ ] Responsive at all breakpoints (sm, md, lg, xl, xxl)
- [ ] Cross-browser compatibility verified

### Performance
- [ ] JavaScript bundle size not increased significantly
- [ ] No memory leaks in interactive components
- [ ] Smooth animations maintained
- [ ] Lighthouse scores 90+ (Performance, Accessibility, Best Practices, SEO)

### Process
- [ ] Interactive component migration patterns documented
- [ ] JavaScript API changes documented
- [ ] Testing matrix complete
- [ ] Known issues documented
- [ ] Module READMEs updated
- [ ] Migration log complete

---

## Risk Assessment

### Risk 1: JavaScript API Changes Break Components (HIGH)
**Impact:** CRITICAL
**Mitigation:**
- Study Bootstrap 5 migration guide (JavaScript section)
- Use lb_accordion as reference
- Test each interactive component thoroughly
- Create test pages for all interactive components
- Document API changes
- Allocate extra time for debugging

### Risk 2: Modal Conflicts with Drupal (MEDIUM)
**Impact:** HIGH
**Mitigation:**
- Test modal with Drupal's dialog system
- Check for event listener conflicts
- Test modal with AJAX forms
- Verify z-index stacking
- Test nested modals

### Risk 3: Date Picker Replacement Fails (MEDIUM)
**Impact:** HIGH
**Mitigation:**
- Decision made in Phase 1
- Test date picker early
- Have fallback ready (Flatpickr recommended)
- Test with all form contexts
- Test accessibility
- Test mobile interactions

### Risk 4: Timeline Slippage (MEDIUM)
**Impact:** MEDIUM
**Mitigation:**
- Batch similar modules
- Use Sprint 13 as buffer
- Contractor support available
- Regular progress check-ins

---

## Related Documents

- [../EXECUTIVE_SUMMARY.md](../EXECUTIVE_SUMMARY.md)
- [../MODULE_INVENTORY.md](../MODULE_INVENTORY.md)
- [../phases/PHASE_3_LAYOUT_BUILDER.md](../phases/PHASE_3_LAYOUT_BUILDER.md)
- [../sprints/SPRINT_08_LB_Simple_Batch1.md](../sprints/SPRINT_08_LB_Simple_Batch1.md)
- [../sprints/SPRINT_09_LB_Simple_Batch2.md](../sprints/SPRINT_09_LB_Simple_Batch2.md)
- [../sprints/SPRINT_10_LB_Interactive_Batch1.md](../sprints/SPRINT_10_LB_Interactive_Batch1.md)
- [../sprints/SPRINT_11_LB_Interactive_Batch2.md](../sprints/SPRINT_11_LB_Interactive_Batch2.md)
- [../sprints/SPRINT_12_LB_Form_Components.md](../sprints/SPRINT_12_LB_Form_Components.md)
- [../sprints/SPRINT_13_LB_Testing_DatePicker.md](../sprints/SPRINT_13_LB_Testing_DatePicker.md)
- [MODULES_THEME.md](MODULES_THEME.md)
- [Bootstrap 5 JavaScript Documentation](https://getbootstrap.com/docs/5.3/getting-started/javascript/)

---

**Module Status:** 1/20 Complete (lb_accordion ✅)
**Last Updated:** 2025-10-17
