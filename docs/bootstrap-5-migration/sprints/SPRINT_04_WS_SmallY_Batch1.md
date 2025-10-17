# Sprint 4: WS Small Y Batch 1

**Phase:** [Phase 2 - Component Migration](../phases/PHASE_2_COMPONENT_MIGRATION.md)
**Resources:** 1 Developer
**Status:** Not Started

---

## Sprint Goal

Migrate first batch of ws_small_y modules (6 modules) to Bootstrap 5, establishing a repeatable migration pattern for remaining modules.

---

## Modules in This Sprint

1. **small_y_hero** - Hero banner component
2. **small_y_cards** - Card layouts
3. **small_y_carousels** - Carousel/slider component
4. **small_y_accordions** - Accordion component
5. **small_y_alerts** - Alert messages
6. **small_y_tabs** - Tab component

**Total:** 6 modules

---

## Pre-Sprint Preparation

### Checklist:
- [ ] Phase 1 (Sprints 1-3) completed
- [ ] Theme fully migrated to Bootstrap 5
- [ ] Activity Finder isolated
- [ ] Migration checklist template ready
- [ ] lb_accordion reference documentation ready

---

## Tasks

### Task 1: Module 1 - small_y_hero
**Owner:** Developer
**Priority:** HIGH

**Location:** `docroot/modules/contrib/ws_small_y/modules/small_y_hero/`

**Actions:**
```bash
cd docroot/modules/contrib/ws_small_y/modules/small_y_hero

# Study module
cat package.json
cat webpack.config.js
ls -la assets/scss/
ls -la templates/
```

**Migration Steps:**

**1. Update package.json:**
```json
{
  "name": "small_y_hero",
  "version": "1.0.0",
  "dependencies": {
    "bootstrap": "^5.3.3"
  },
  "devDependencies": {
    "webpack": "^5.89.0",
    "webpack-cli": "^5.1.4",
    "sass": "^1.69.5",
    "sass-loader": "^13.3.2",
    "css-loader": "^6.8.1",
    "mini-css-extract-plugin": "^2.7.6"
  },
  "scripts": {
    "build": "webpack --mode production",
    "dev": "webpack --mode development --watch"
  }
}
```

**2. Update webpack.config.js** (follow lb_accordion pattern)

**3. Update SCSS:**
```bash
# Update imports
# Update variables
# Update mixins
# Test compilation
```

**4. Update Templates:**
```twig
{# Update data-toggle → data-bs-toggle #}
{# Update data-target → data-bs-target #}
{# Update CSS classes (left/right → start/end) #}
```

**5. Update JavaScript** (if any):
```javascript
// Update Bootstrap imports
import { Carousel } from 'bootstrap';

// Update initialization code
```

**6. Build and Test:**
```bash
npm install
npm run build
fin drush cr
# Test in browser
```

**Acceptance Criteria:**
- [ ] Module builds successfully
- [ ] Templates render correctly
- [ ] Functionality works (animations, interactions)
- [ ] Responsive design works
- [ ] No console errors
- [ ] Documentation updated

---

### Task 2: Module 2 - small_y_cards
**Owner:** Developer
**Priority:** HIGH

**Location:** `docroot/modules/contrib/ws_small_y/modules/small_y_cards/`

**Actions:**
Follow same pattern as Task 1:
1. Update package.json
2. Update webpack.config.js
3. Update SCSS
4. Update templates
5. Update JavaScript
6. Build and test

**Card-Specific Updates:**
```scss
// Bootstrap 4 - card-deck (REMOVED in BS5)
.card-deck {
  display: flex;
  flex-flow: row wrap;
}

// Bootstrap 5 - Use grid instead
<div class="row row-cols-1 row-cols-md-3 g-4">
  <div class="col">
    <div class="card">...</div>
  </div>
</div>
```

**Acceptance Criteria:**
- [ ] Module builds successfully
- [ ] Card layouts work correctly
- [ ] Card decks replaced with grid
- [ ] Responsive behavior correct
- [ ] No console errors

---

### Task 3: Module 3 - small_y_carousels
**Owner:** Developer
**Priority:** HIGH

**Location:** `docroot/modules/contrib/ws_small_y/modules/small_y_carousels/`

**Actions:**
Follow same pattern as Task 1

**Carousel-Specific Updates:**
```twig
{# Bootstrap 4 #}
<div class="carousel slide" data-ride="carousel">
  <a class="carousel-control-prev" data-slide="prev">

{# Bootstrap 5 #}
<div class="carousel slide" data-bs-ride="carousel">
  <button class="carousel-control-prev" data-bs-slide="prev">
```

**JavaScript:**
```javascript
// Bootstrap 5 Carousel API
import { Carousel } from 'bootstrap';

const myCarousel = document.querySelector('#myCarousel');
const carousel = new Carousel(myCarousel, {
  interval: 5000,
  wrap: true
});
```

**Acceptance Criteria:**
- [ ] Module builds successfully
- [ ] Carousel slides work
- [ ] Controls work (prev/next)
- [ ] Indicators work
- [ ] Auto-play works (if enabled)
- [ ] Touch gestures work on mobile

---

### Task 4: Module 4 - small_y_accordions
**Owner:** Developer
**Priority:** HIGH

**Location:** `docroot/modules/contrib/ws_small_y/modules/small_y_accordions/`

**Actions:**
Follow same pattern as Task 1

**Reference:** This should be very similar to lb_accordion!

**Accordion-Specific Updates:**
```twig
{# Bootstrap 4 #}
<div class="accordion" id="accordionExample">
  <div class="card">
    <div class="card-header">
      <button data-toggle="collapse" data-target="#collapseOne">

{# Bootstrap 5 #}
<div class="accordion" id="accordionExample">
  <div class="accordion-item">
    <h2 class="accordion-header">
      <button class="accordion-button" data-bs-toggle="collapse" data-bs-target="#collapseOne">
```

**Note:** Bootstrap 5 accordion structure changed significantly - review documentation.

**Acceptance Criteria:**
- [ ] Module builds successfully
- [ ] Accordions expand/collapse correctly
- [ ] Multiple accordions work on same page
- [ ] Only one item open at a time (if configured)
- [ ] Keyboard navigation works
- [ ] ARIA attributes correct

---

### Task 5: Module 5 - small_y_alerts
**Owner:** Developer
**Priority:** MEDIUM

**Location:** `docroot/modules/contrib/ws_small_y/modules/small_y_alerts/`

**Actions:**
Follow same pattern as Task 1

**Alert-Specific Updates:**
```twig
{# Bootstrap 4 #}
<div class="alert alert-warning alert-dismissible fade show">
  <button type="button" class="close" data-dismiss="alert">
    <span>&times;</span>
  </button>

{# Bootstrap 5 #}
<div class="alert alert-warning alert-dismissible fade show">
  <button type="button" class="btn-close" data-bs-dismiss="alert"></button>
```

**Key Changes:**
- `class="close"` → `class="btn-close"`
- `data-dismiss` → `data-bs-dismiss`
- Remove `<span>&times;</span>` (btn-close is styled automatically)

**Acceptance Criteria:**
- [ ] Module builds successfully
- [ ] Alerts display correctly
- [ ] Dismiss button works
- [ ] Alert types styled correctly (success, warning, danger, info)
- [ ] Icons display if used

---

### Task 6: Module 6 - small_y_tabs
**Owner:** Developer
**Priority:** HIGH

**Location:** `docroot/modules/contrib/ws_small_y/modules/small_y_tabs/`

**Actions:**
Follow same pattern as Task 1

**Tab-Specific Updates:**
```twig
{# Bootstrap 4 #}
<ul class="nav nav-tabs">
  <li class="nav-item">
    <a class="nav-link" data-toggle="tab" href="#home">

{# Bootstrap 5 #}
<ul class="nav nav-tabs">
  <li class="nav-item">
    <button class="nav-link" data-bs-toggle="tab" data-bs-target="#home">
```

**Key Changes:**
- Can use `<button>` instead of `<a>` (better accessibility)
- `href="#home"` → `data-bs-target="#home"` (if using button)
- `data-toggle` → `data-bs-toggle`

**JavaScript:**
```javascript
import { Tab } from 'bootstrap';

const triggerTabList = document.querySelectorAll('button[data-bs-toggle="tab"]');
triggerTabList.forEach(triggerEl => {
  const tabTrigger = new Tab(triggerEl);
  // Can listen to events if needed
});
```

**Acceptance Criteria:**
- [ ] Module builds successfully
- [ ] Tabs switch correctly
- [ ] Tab content displays
- [ ] Keyboard navigation works
- [ ] Deep linking works (if implemented)
- [ ] ARIA attributes correct

---

### Task 7: Integration Testing - Batch 1
**Owner:** Developer
**Priority:** CRITICAL

**Actions:**
```bash
# Rebuild all modules
cd docroot/modules/contrib/ws_small_y/modules

for module in small_y_hero small_y_cards small_y_carousels small_y_accordions small_y_alerts small_y_tabs; do
  cd $module
  npm run build
  cd ..
done

# Clear Drupal cache
fin drush cr
```

**Test Scenarios:**
1. Create test page with all 6 components
2. Test each component individually
3. Test components together on same page
4. Test responsive behavior
5. Test browser compatibility
6. Test accessibility

**Create Test Page:**
```bash
# Create landing page with all components
fin drush pm-enable small_y_hero small_y_cards small_y_carousels small_y_accordions small_y_alerts small_y_tabs
# Use Layout Builder or Paragraphs to add all components
```

**Acceptance Criteria:**
- [ ] All 6 modules work individually
- [ ] All 6 modules work together on same page
- [ ] No CSS conflicts
- [ ] No JavaScript errors
- [ ] Responsive design works
- [ ] Accessibility maintained

---

### Task 8: Visual Regression Testing - Batch 1
**Owner:** Developer
**Priority:** HIGH

**Actions:**
```bash
cd /private/var/www/YMCAWS_11/docs/bootstrap-5-migration/testing

# Update backstop.json with test page
# Add scenarios for each component

npx backstop test
```

**Review Results:**
- Compare visual differences
- Document intentional changes
- Document unintentional issues
- Create fix list if needed

**Acceptance Criteria:**
- [ ] Visual regression tests executed
- [ ] Results reviewed
- [ ] Critical issues identified
- [ ] Results documented

---

### Task 9: Documentation - Batch 1
**Owner:** Developer
**Priority:** MEDIUM

**Actions:**
```bash
cd docs/bootstrap-5-migration/modules
```

**Create Module Documentation:**

For each migrated module, create:
`docs/bootstrap-5-migration/modules/SMALL_Y_HERO.md`
`docs/bootstrap-5-migration/modules/SMALL_Y_CARDS.md`
etc.

**Template:**
```markdown
# Module: small_y_hero

**Status:** ✅ Migrated
**Sprint:** Sprint 4
**Date:** 2025-10-XX

## Changes Made
- Updated package.json to Bootstrap 5.3.3
- Updated webpack.config.js
- Updated SCSS imports
- Updated templates (data-bs-* attributes)
- Updated JavaScript (Bootstrap 5 API)

## Breaking Changes
- [List any breaking changes]

## Known Issues
- [List any known issues]

## Testing
- [x] Build successful
- [x] Functionality tested
- [x] Responsive tested
- [x] Accessibility tested
```

**Update MIGRATION_LOG.md:**
```markdown
## Sprint 4 - WS Small Y Batch 1

### Completed Modules (6):
1. ✅ small_y_hero
2. ✅ small_y_cards
3. ✅ small_y_carousels
4. ✅ small_y_accordions
5. ✅ small_y_alerts
6. ✅ small_y_tabs

### Issues Encountered:
- [List any issues]

### Lessons Learned:
- [Document lessons learned]
```

**Acceptance Criteria:**
- [ ] Individual module docs created
- [ ] MIGRATION_LOG.md updated
- [ ] Issues documented
- [ ] Lessons learned documented

---

## Testing

### Build Testing:
- [ ] All 6 modules build successfully
- [ ] No build errors or warnings
- [ ] Output files generated correctly

### Functional Testing:
- [ ] Hero banners display and function
- [ ] Cards display correctly
- [ ] Carousels slide correctly
- [ ] Accordions expand/collapse
- [ ] Alerts display and dismiss
- [ ] Tabs switch correctly

### Visual Testing:
- [ ] BackstopJS tests pass (or differences documented)
- [ ] Responsive design works (phone, tablet, desktop)
- [ ] Components match design system

### Accessibility Testing:
- [ ] Keyboard navigation works
- [ ] Screen reader compatible
- [ ] ARIA attributes correct
- [ ] Color contrast adequate

### Browser Testing:
- [ ] Chrome/Edge
- [ ] Firefox
- [ ] Safari
- [ ] Mobile browsers

---

## Deliverables

### Must Have:
- [ ] 6 modules migrated to Bootstrap 5
- [ ] All modules build successfully
- [ ] All modules functional
- [ ] Integration testing complete
- [ ] Documentation complete

### Nice to Have:
- [ ] Performance metrics documented
- [ ] Bundle size comparison (BS4 vs BS5)
- [ ] Migration pattern documented for future sprints

---

## Decision Points

### Decision: Handle Card Deck Deprecation
**Options:**
1. Replace with Bootstrap 5 grid system
2. Create custom card-deck class
3. Use CSS Grid

**Recommendation:** Option 1 - Use Bootstrap 5 grid system

**Decision Required By:** Task 2
**Decision Maker:** Developer

---

## Risks

### Risk: Module Dependencies on Each Other
**Likelihood:** Low
**Impact:** Medium
**Mitigation:** Test modules individually first, then together

### Risk: Unexpected Breaking Changes
**Likelihood:** Medium
**Impact:** Medium
**Mitigation:** Keep Bootstrap 4 branch for reference, test thoroughly

### Risk: Time Underestimate
**Likelihood:** Medium
**Impact:** Medium
**Mitigation:** Prioritize critical modules, defer nice-to-have features

---

## Notes

### Important:
- This sprint establishes the pattern for all remaining modules
- Document everything - will speed up future sprints
- Focus on getting the process right, not just speed
- Test thoroughly - these are commonly used components

### Tips:
- Use migration checklist for each module
- Commit after each module completion
- Test in browser frequently
- Compare with lb_accordion for reference
- Ask for help if stuck - don't waste time

### Migration Pattern Established:
1. Study module structure
2. Update package.json
3. Update webpack.config.js
4. Update SCSS
5. Update templates
6. Update JavaScript
7. Build and test
8. Document

**This pattern will be repeated for all remaining modules.**

---

## Sprint Review Checklist

At end of sprint, verify:
- [ ] All 6 modules completed
- [ ] All tests passing
- [ ] All deliverables created
- [ ] Documentation complete
- [ ] Next sprint ready to start
- [ ] Migration pattern validated

---

## Navigation

- **Previous:** [Sprint 3 - Theme Part 2 + Activity Finder Isolation](SPRINT_03_Theme_Part2_AF_Isolation.md)
- **Next:** [Sprint 5 - WS Small Y Batch 2](SPRINT_05_WS_SmallY_Batch2.md)
- **Phase:** [Phase 2 - Component Migration](../phases/PHASE_2_COMPONENT_MIGRATION.md)
- **Overview:** [Executive Summary](../EXECUTIVE_SUMMARY.md)

---

**Sprint Status:** ⬜ Not Started
**Last Updated:** 2025-10-17
