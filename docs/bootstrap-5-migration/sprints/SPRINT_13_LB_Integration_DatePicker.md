# Sprint 13: Layout Builder Integration & Date Picker Replacement

**Phase:** [Phase 3 - Layout Builder](../phases/PHASE_3_LAYOUT_BUILDER.md)
**Resources:** 1 Developer + QA Support
**Status:** Not Started

---

## Sprint Goal

Complete Phase 3 by performing comprehensive integration testing of all Layout Builder modules and replacing the deprecated bootstrap-datepicker with a Bootstrap 5-compatible solution.

---

## Focus Areas

### 1. Integration Testing
- Test all 19 LB modules working together
- Test multiple components on same page
- Test nested/combined components
- Test edge cases and real-world scenarios

### 2. Date Picker Replacement
- Replace bootstrap-datepicker 1.3.0 (Bootstrap 3/4 only)
- Implement chosen solution from Phase 1 Sprint 1
- Update openy_repeat module
- Update lb_repeat_schedules

### 3. Bug Fixes & Polish
- Fix issues discovered during integration testing
- Address edge cases
- Performance optimization
- Documentation completion

---

## Tasks

### Task 1: Replace bootstrap-datepicker
**Owner:** Developer
**Priority:** CRITICAL

**Background:**
- Current: bootstrap-datepicker 1.3.0 (NOT compatible with Bootstrap 5)
- Modules affected: openy_repeat, lb_repeat_schedules
- Decision made in Phase 1 Sprint 1 (Task 5)

**Actions:**

**1.1 Review Phase 1 decision:**
```bash
# Check decision document
cat docs/bootstrap-5-migration/decisions/DECISION_DATE_PICKER.md

# Likely choice: Flatpickr (lightweight, accessible, no Bootstrap dependency)
```

**1.2 Install chosen date picker (assuming Flatpickr):**
```bash
cd docroot/modules/contrib/openy_repeat

# Update package.json
npm install flatpickr --save
```

**1.3 Update package.json:**
```json
{
  "dependencies": {
    "bootstrap": "^5.3.3",
    "@popperjs/core": "^2.11.8",
    "flatpickr": "^4.6.13"
  }
}
```

**1.4 Remove bootstrap-datepicker:**
```bash
# Remove old dependency
npm uninstall bootstrap-datepicker
```

**1.5 Update JavaScript:**
```javascript
// OLD: bootstrap-datepicker
$('.datepicker').datepicker({
  format: 'mm/dd/yyyy',
  autoclose: true,
  todayHighlight: true
});

// NEW: Flatpickr
import flatpickr from 'flatpickr';

flatpickr('.datepicker', {
  dateFormat: 'm/d/Y',
  enableTime: false,
  defaultDate: 'today'
});

// With time picker
flatpickr('.datetimepicker', {
  enableTime: true,
  dateFormat: 'm/d/Y H:i',
  time_24hr: false
});

// With range selection
flatpickr('.daterange', {
  mode: 'range',
  dateFormat: 'm/d/Y'
});
```

**1.6 Update CSS:**
```scss
// Import Flatpickr styles
@import "flatpickr/dist/flatpickr.css";

// Or import theme
@import "flatpickr/dist/themes/material_blue.css";

// Customize to match Bootstrap 5 theme
.flatpickr-calendar {
  // Match Bootstrap form styling
}
```

**1.7 Update templates:**
```twig
{# OLD: bootstrap-datepicker #}
<input type="text" class="form-control datepicker" data-provide="datepicker">

{# NEW: Flatpickr #}
<input type="text" class="form-control datepicker" placeholder="Select date...">
```

**1.8 Test date picker functionality:**
- [ ] Date selection works
- [ ] Date formatting correct
- [ ] Min/max date constraints work
- [ ] Disabled dates work (if used)
- [ ] Keyboard input works
- [ ] Mobile date picker works
- [ ] Multiple date pickers on same page
- [ ] Form submission with date

**1.9 Update openy_repeat module:**
```bash
cd docroot/modules/contrib/openy_repeat

# Update all date picker instances
# Test repeat schedule functionality
# Verify date range selection
```

**1.10 Update lb_repeat_schedules:**
```bash
cd docroot/modules/contrib/openy_repeat/modules/lb_repeat_schedules

# Update date picker usage
# Test schedule creation
# Test schedule display
```

**Deliverables:**
- [ ] `docs/bootstrap-5-migration/modules/openy_repeat.md`
- [ ] `docs/bootstrap-5-migration/modules/lb_repeat_schedules.md`
- [ ] Date picker replacement guide
- [ ] Migration documentation for custom code

**Acceptance Criteria:**
- [ ] bootstrap-datepicker completely removed
- [ ] New date picker installed and working
- [ ] All date selection functionality works
- [ ] Mobile date picker works
- [ ] Keyboard navigation works
- [ ] Accessibility maintained (ARIA, screen readers)
- [ ] Form submission works
- [ ] openy_repeat module functional
- [ ] lb_repeat_schedules module functional

---

### Task 2: Integration Testing - Multiple Components on Same Page
**Owner:** Developer + QA
**Priority:** CRITICAL

**Actions:**

**2.1 Create comprehensive test pages:**
```bash
# Create test nodes with multiple LB components
drush node:create test-page

# Suggested test pages:
# 1. Kitchen sink: All components
# 2. Interactive components: Modal + Carousel + Tabs + Accordion
# 3. Forms: Webform + Modal + Date picker
# 4. Content: Cards + Hero + Testimonials + Statistics
# 5. Branch: Amenities + Hours + Social links + Staff
```

**2.2 Test component combinations:**

**Test Page 1: Interactive Components**
- [ ] Carousel inside modal
- [ ] Tabs with multiple carousels
- [ ] Accordion with embedded webform
- [ ] Modal triggered from carousel slide
- [ ] Multiple modals on same page

**Test Page 2: Form Components**
- [ ] Webform inside modal
- [ ] Multiple webforms on page
- [ ] Webform with date picker
- [ ] Date picker with validation
- [ ] Form submission with AJAX

**Test Page 3: Grid Layouts**
- [ ] Cards + Promo + Statistics
- [ ] Staff + Testimonials + Partners
- [ ] Multiple grids with different columns
- [ ] Nested grids (if applicable)

**Test Page 4: Branch Page**
- [ ] Hero + Hours + Amenities
- [ ] Social links + Staff + Testimonials
- [ ] Embedded programs/schedules
- [ ] Date picker for schedule filtering

**2.3 Test JavaScript interactions:**
- [ ] No console errors
- [ ] No JavaScript conflicts
- [ ] Events fire correctly
- [ ] State management works
- [ ] Memory leaks check (Chrome DevTools)

**2.4 Test responsive behavior:**
- [ ] All components responsive
- [ ] No layout breaks
- [ ] Mobile interactions work
- [ ] Touch gestures work
- [ ] Viewport transitions smooth

**Deliverables:**
- [ ] Test page suite created
- [ ] Integration test report
- [ ] Known issues documented
- [ ] Bug tickets created (if needed)

**Acceptance Criteria:**
- [ ] All component combinations work
- [ ] No JavaScript conflicts
- [ ] No layout issues
- [ ] Mobile experience good
- [ ] Performance acceptable

---

### Task 3: Visual Regression Testing - All LB Modules
**Owner:** Developer
**Priority:** HIGH

**Actions:**

**3.1 Update BackstopJS configuration:**
```bash
cd docs/bootstrap-5-migration/testing

# Update backstop.json with all LB modules
```

**3.2 Create comprehensive scenario list:**
```json
{
  "scenarios": [
    // High Priority (Sprints 8-9)
    {"label": "LB Hero", "url": "http://yusaopeny.docksal.site/test/lb-hero"},
    {"label": "LB Cards", "url": "http://yusaopeny.docksal.site/test/lb-cards"},
    {"label": "LB Carousel", "url": "http://yusaopeny.docksal.site/test/lb-carousel"},
    {"label": "LB Modal", "url": "http://yusaopeny.docksal.site/test/lb-modal"},
    {"label": "LB Modal Open", "url": "http://yusaopeny.docksal.site/test/lb-modal", "clickSelector": "[data-bs-toggle='modal']"},
    {"label": "LB Webform", "url": "http://yusaopeny.docksal.site/test/lb-webform"},

    // Medium Priority (Sprints 10-11)
    {"label": "LB Amenities", "url": "http://yusaopeny.docksal.site/test/lb-amenities"},
    {"label": "LB Hours", "url": "http://yusaopeny.docksal.site/test/lb-hours"},
    {"label": "LB Social Links", "url": "http://yusaopeny.docksal.site/test/lb-social-links"},
    {"label": "LB Ping Pong", "url": "http://yusaopeny.docksal.site/test/lb-ping-pong"},
    {"label": "LB Promo", "url": "http://yusaopeny.docksal.site/test/lb-promo"},
    {"label": "LB Grid CTA", "url": "http://yusaopeny.docksal.site/test/lb-grid-cta"},
    {"label": "LB Partners", "url": "http://yusaopeny.docksal.site/test/lb-partners"},
    {"label": "LB Related Articles", "url": "http://yusaopeny.docksal.site/test/lb-related-articles"},
    {"label": "LB Related Events", "url": "http://yusaopeny.docksal.site/test/lb-related-events"},
    {"label": "LB Simple Menu", "url": "http://yusaopeny.docksal.site/test/lb-simple-menu"},

    // Lower Priority (Sprint 12)
    {"label": "LB Staff", "url": "http://yusaopeny.docksal.site/test/lb-staff"},
    {"label": "LB Statistics", "url": "http://yusaopeny.docksal.site/test/lb-statistics"},
    {"label": "LB Table", "url": "http://yusaopeny.docksal.site/test/lb-table"},
    {"label": "LB Testimonials", "url": "http://yusaopeny.docksal.site/test/lb-testimonials"},

    // Integration pages
    {"label": "Kitchen Sink", "url": "http://yusaopeny.docksal.site/test/kitchen-sink"},
    {"label": "Branch Page", "url": "http://yusaopeny.docksal.site/test/branch-page"}
  ]
}
```

**3.3 Run visual regression tests:**
```bash
# Run tests
npx backstop test

# Review results
npx backstop openReport

# Approve changes if acceptable
npx backstop approve
```

**3.4 Document visual differences:**
- [ ] Expected differences (Bootstrap 5 improvements)
- [ ] Unexpected differences (bugs)
- [ ] Acceptable differences (minor rendering)
- [ ] Unacceptable differences (must fix)

**Deliverables:**
- [ ] Complete BackstopJS test suite
- [ ] Visual regression report
- [ ] Approved baseline screenshots
- [ ] Visual differences documented

**Acceptance Criteria:**
- [ ] All LB modules have visual tests
- [ ] Tests pass or differences documented
- [ ] Regression baseline approved
- [ ] Visual bugs documented

---

### Task 4: Accessibility Testing - All LB Modules
**Owner:** Developer + QA
**Priority:** HIGH

**Actions:**

**4.1 Update Pa11y configuration:**
```bash
cd docs/bootstrap-5-migration/testing

# Update .pa11yci.json with all test pages
```

**4.2 Run accessibility tests:**
```bash
# Run Pa11y CI
npx pa11y-ci --reporter html > reports/phase-3-accessibility.html

# Review results
open reports/phase-3-accessibility.html
```

**4.3 Manual accessibility testing:**
- [ ] Keyboard navigation (all interactive components)
- [ ] Screen reader testing (NVDA/JAWS)
- [ ] Focus indicators visible
- [ ] Skip links work
- [ ] Heading hierarchy correct
- [ ] Form labels correct
- [ ] ARIA attributes correct
- [ ] Color contrast passes WCAG 2.2 AA

**4.4 Interactive component accessibility:**
- [ ] Modal: Focus trap, ESC to close, ARIA
- [ ] Carousel: Keyboard controls, auto-play pause, ARIA
- [ ] Tabs: Keyboard navigation, ARIA
- [ ] Accordion: Keyboard controls, ARIA (already tested)
- [ ] Forms: Labels, validation, error messages
- [ ] Date picker: Keyboard navigation, ARIA

**4.5 Create accessibility report:**
```bash
touch docs/bootstrap-5-migration/testing/PHASE_3_ACCESSIBILITY_REPORT.md
```

**Deliverables:**
- [ ] Complete Pa11y test suite
- [ ] Accessibility test report
- [ ] Manual testing results
- [ ] Issues documented and prioritized

**Acceptance Criteria:**
- [ ] All LB modules meet WCAG 2.2 AA
- [ ] No critical accessibility issues
- [ ] Keyboard navigation works
- [ ] Screen reader compatible
- [ ] Issues documented with remediation plan

---

### Task 5: Performance Testing & Optimization
**Owner:** Developer
**Priority:** MEDIUM

**Actions:**

**5.1 JavaScript bundle size analysis:**
```bash
# Check compiled JavaScript sizes
cd docroot/modules/contrib/

for module in lb_*/; do
  echo "=== $module ==="
  if [ -d "$module/dist" ]; then
    ls -lh $module/dist/*.js
  fi
done
```

**5.2 Compare Bootstrap 4 vs. 5 bundle sizes:**
- [ ] Document size increases/decreases
- [ ] Identify large dependencies
- [ ] Check for duplicate Bootstrap bundles
- [ ] Optimize if needed (tree-shaking, code splitting)

**5.3 Page load performance:**
```bash
# Use Lighthouse or WebPageTest
# Test key pages:
# - Homepage with hero + carousel
# - Branch page with multiple components
# - Page with modal + webform
```

**5.4 JavaScript performance profiling:**
- [ ] Use Chrome DevTools Performance tab
- [ ] Profile carousel animations
- [ ] Profile modal open/close
- [ ] Check for memory leaks
- [ ] Check for layout thrashing

**5.5 Optimization opportunities:**
- [ ] Lazy load carousels below fold
- [ ] Defer non-critical JavaScript
- [ ] Optimize images in components
- [ ] Reduce unused CSS

**Deliverables:**
- [ ] Performance report
- [ ] Bundle size comparison
- [ ] Optimization recommendations
- [ ] Performance baseline established

**Acceptance Criteria:**
- [ ] JavaScript bundle size not significantly increased
- [ ] Page load times acceptable (< 3s)
- [ ] No memory leaks detected
- [ ] Performance regression documented (if any)

---

### Task 6: Phase 3 Completion & Documentation
**Owner:** Developer
**Priority:** HIGH

**Actions:**

**6.1 Complete Phase 3 documentation:**
```bash
# Update Phase 3 summary
vim docs/bootstrap-5-migration/phases/PHASE_3_SUMMARY.md

# Update module inventory
vim docs/bootstrap-5-migration/MODULE_INVENTORY.md

# Update migration log
vim docs/bootstrap-5-migration/MIGRATION_LOG.md
```

**6.2 Create migration guides:**
- [ ] Date picker migration guide
- [ ] Layout Builder component usage guide
- [ ] Troubleshooting guide
- [ ] Known issues and workarounds

**6.3 Update executive summary:**
```bash
vim docs/bootstrap-5-migration/EXECUTIVE_SUMMARY.md

# Update progress:
# - Phase 3: Complete
# - 19 LB modules migrated
# - Date picker replaced
```

**6.4 Create GO/NO-GO decision document:**
```bash
touch docs/bootstrap-5-migration/decisions/DECISION_PHASE_3_GONO_GO.md
```

**6.5 GO/NO-GO criteria checklist:**
- [ ] All 19 LB modules migrated and tested
- [ ] Date picker replaced and functional
- [ ] Integration testing passed
- [ ] Visual regression tests passed
- [ ] Accessibility tests passed
- [ ] Performance acceptable
- [ ] No critical bugs
- [ ] Documentation complete

**Deliverables:**
- [ ] Phase 3 summary complete
- [ ] Migration guides created
- [ ] GO/NO-GO decision document
- [ ] All documentation updated

**Acceptance Criteria:**
- [ ] All Phase 3 documentation complete
- [ ] GO/NO-GO decision made
- [ ] Phase 4 ready to start (if approved)
- [ ] All issues documented

---

## Testing

### Comprehensive Testing Matrix

**Interactive Components:**
| Component | Keyboard | Mobile | Screen Reader | Visual | Performance |
|-----------|----------|--------|---------------|--------|-------------|
| Modal | ✓ | ✓ | ✓ | ✓ | ✓ |
| Carousel | ✓ | ✓ | ✓ | ✓ | ✓ |
| Tabs | ✓ | ✓ | ✓ | ✓ | ✓ |
| Accordion | ✓ | ✓ | ✓ | ✓ | ✓ |
| Webform | ✓ | ✓ | ✓ | ✓ | ✓ |
| Date Picker | ✓ | ✓ | ✓ | ✓ | ✓ |

**Test Environment:**
- [ ] Desktop (Chrome, Firefox, Safari, Edge)
- [ ] Tablet (iPad, Android)
- [ ] Mobile (iPhone, Android)
- [ ] Screen readers (NVDA, JAWS, VoiceOver)

---

## Deliverables

### Must Have (Critical):
- [ ] bootstrap-datepicker replaced
- [ ] New date picker working in all contexts
- [ ] Integration testing complete
- [ ] Visual regression tests passed
- [ ] Accessibility tests passed
- [ ] All critical bugs fixed
- [ ] Phase 3 documentation complete
- [ ] GO/NO-GO decision made

### Should Have (High Priority):
- [ ] Performance testing complete
- [ ] Optimization recommendations documented
- [ ] Migration guides created
- [ ] Known issues documented

### Nice to Have:
- [ ] Video tutorials for date picker
- [ ] Component showcase page
- [ ] Developer troubleshooting guide

---

## Decision Points

### Decision: Phase 3 GO/NO-GO (END OF SPRINT)
**Criteria:**
- All 19 LB modules functional
- Date picker replaced and working
- No critical bugs
- Acceptable performance
- Accessibility standards met

**Options:**
- GO: Proceed to Phase 4 (Content Type modules)
- NO-GO: Additional sprint for bug fixes

**Decision Maker:** Project Lead + Stakeholders
**Documentation:** `decisions/DECISION_PHASE_3_GO_NO_GO.md`

---

## Risks

### Risk: Date Picker Replacement Fails (HIGH)
**Impact:** CRITICAL - Schedule forms don't work
**Mitigation:**
- Decision already made in Phase 1
- Test early in sprint
- Have fallback option (HTML5 date input)
- Allocate extra time if needed

### Risk: Integration Issues Not Discovered Until Late (MEDIUM)
**Mitigation:**
- Start integration testing early (Task 2 first)
- Run tests continuously
- Use buffer time for fixes
- Prioritize critical bugs

### Risk: Performance Degradation (MEDIUM)
**Mitigation:**
- Profile performance early
- Compare to Bootstrap 4 baseline
- Optimize critical paths
- Document acceptable trade-offs

---

## Notes

### Important:
- This is the final Phase 3 sprint - be thorough
- Integration testing is critical - don't skip
- Date picker replacement affects multiple modules
- GO/NO-GO decision is crucial for project success

### Tips:
- Start with date picker replacement (longest task)
- Run integration tests continuously
- Document all issues, even minor ones
- Create regression tests for bugs found
- Save buffer time for unexpected issues

### Phase 3 Success Metrics:
- 19 LB modules migrated ✓
- Bootstrap 5.3.3 throughout ✓
- Date picker Bootstrap 5 compatible ✓
- All tests passing ✓
- Performance acceptable ✓
- Accessibility maintained ✓

---

## Sprint Review Checklist

At end of sprint, verify:
- [ ] All tasks completed
- [ ] Date picker replaced
- [ ] Integration testing complete
- [ ] Visual regression tests passed
- [ ] Accessibility tests passed
- [ ] Performance acceptable
- [ ] Documentation complete
- [ ] GO/NO-GO decision made
- [ ] Phase 4 ready (if approved)

---

## Navigation

- **Previous:** [Sprint 12 - LB Lower Priority](SPRINT_12_LB_LowerPriority.md)
- **Next:** [Sprint 14 - Content Types Branch](SPRINT_14_ContentTypes_Branch.md)
- **Phase:** [Phase 3 - Layout Builder](../phases/PHASE_3_LAYOUT_BUILDER.md)
- **Overview:** [Executive Summary](../EXECUTIVE_SUMMARY.md)

---

**Sprint Status:** ⬜ Not Started
**Last Updated:** 2025-10-17
