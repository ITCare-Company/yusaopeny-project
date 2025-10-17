# Sprint 14: Branch & Location Modules

**Phase:** [Phase 4 - Content Types](../phases/PHASE_4_CONTENT_TYPES.md)
**Resources:** 1 Developer
**Status:** Not Started

---

## Sprint Goal

Migrate branch and location content type modules to Bootstrap 5, maintaining branch finder functionality and Location pages display. This sprint initiates Phase 4 by establishing content type migration patterns.

---

## Modules in This Sprint

### Primary Modules (2):
1. **y_branch** - Branch/location content type
   - Path: `docroot/modules/contrib/y_branch`
   - Branch finder integration
   - Location pages
   - Branch-specific content

2. **y_branch_menu** - Branch menu integration
   - Path: `docroot/modules/contrib/y_branch_menu`
   - Branch-specific menu logic
   - Menu integration with branches

---

## Tasks

### Task 1: Audit Branch Modules
**Owner:** Developer
**Priority:** CRITICAL

**Actions:**
```bash
# Review branch modules
cd docroot/modules/contrib/y_branch

# Check for Bootstrap dependencies
grep -r "bootstrap" .
find . -name "package.json"
find . -name "*.scss" -o -name "*.css"
find . -name "*.js"

# Check templates
find . -name "*.twig"

# Check for Activity Finder integration
grep -r "activity_finder" .
```

**Document:**
- Templates using Bootstrap classes
- JavaScript dependencies
- SCSS/CSS files
- Integration with Activity Finder (still BS4 - isolated)
- Form displays
- Field formatters
- Views displays

**Deliverable:** Create `docs/bootstrap-5-migration/modules/y_branch_audit.md`

**Acceptance Criteria:**
- [ ] All Bootstrap 4 usage documented
- [ ] Activity Finder integration points identified
- [ ] Templates inventory complete
- [ ] JavaScript dependencies documented

---

### Task 2: Migrate y_branch Templates
**Owner:** Developer
**Priority:** CRITICAL

**Actions:**

**2.1 Update Twig templates:**
```twig
{# OLD: Bootstrap 4 classes #}
<div class="card">
  <div class="card-body">
    <h5 class="card-title">{{ branch.name }}</h5>
  </div>
</div>

{# NEW: Bootstrap 5 classes (usually same) #}
<div class="card">
  <div class="card-body">
    <h5 class="card-title">{{ branch.name }}</h5>
  </div>
</div>

{# Update data attributes #}
{# OLD: data-toggle, data-target #}
<button data-toggle="collapse" data-target="#details">

{# NEW: data-bs-toggle, data-bs-target #}
<button data-bs-toggle="collapse" data-bs-target="#details">
```

**2.2 Update branch page templates:**
- Branch full view template
- Branch teaser view template
- Branch amenities display
- Branch hours display
- Branch contact information
- Branch location/map display

**2.3 Update form templates:**
- Branch add/edit form
- Branch settings form
- Field configuration forms

**Deliverable:** Updated templates in y_branch module

**Acceptance Criteria:**
- [ ] All templates use Bootstrap 5 classes
- [ ] All data-* attributes updated to data-bs-*
- [ ] Form styling correct
- [ ] Branch pages display correctly
- [ ] No broken layouts

---

### Task 3: Migrate y_branch Styling
**Owner:** Developer
**Priority:** HIGH

**Actions:**

**3.1 Update SCSS files:**
```scss
// OLD: Bootstrap 4 imports
@import "~bootstrap/scss/functions";
@import "~bootstrap/scss/variables";
@import "~bootstrap/scss/mixins";

// NEW: Bootstrap 5 imports (check paths)
@import "bootstrap/scss/functions";
@import "bootstrap/scss/variables";
@import "bootstrap/scss/mixins";

// Update deprecated variables
// $spacer-x → $spacer
// $brand-primary → $primary
// $text-muted → var(--bs-secondary-color)
```

**3.2 Update branch-specific styles:**
- Branch header styles
- Branch amenities grid
- Branch hours table
- Branch contact section
- Branch location/map section

**3.3 Update responsive breakpoints:**
```scss
// OLD: Bootstrap 4 breakpoints
@include media-breakpoint-down(xs) { }

// NEW: Bootstrap 5 breakpoints
@include media-breakpoint-down(sm) { }
```

**Deliverable:** Updated SCSS files in y_branch

**Acceptance Criteria:**
- [ ] SCSS compiles without errors
- [ ] Branch styles match Bootstrap 5 theme
- [ ] Responsive breakpoints work correctly
- [ ] No deprecated variable warnings

---

### Task 4: Test Activity Finder Integration
**Owner:** Developer
**Priority:** CRITICAL

**Actions:**

**4.1 Verify Activity Finder isolation:**
```bash
# Check Activity Finder still uses Bootstrap 4
cd docroot/modules/contrib/yusaopeny_activity_finder

# Verify scoped CSS still works
```

**4.2 Test Activity Finder on branch pages:**
- [ ] Activity Finder renders correctly on branch pages
- [ ] Bootstrap 5 styles don't leak into Activity Finder
- [ ] Bootstrap 4 styles don't leak out of Activity Finder
- [ ] Activity Finder JavaScript works
- [ ] Activity Finder search/filters work
- [ ] No console errors

**4.3 Test branch page layout:**
- [ ] Branch content displays correctly around Activity Finder
- [ ] Page layout not broken by Activity Finder
- [ ] Responsive behavior maintained

**Deliverable:** Activity Finder integration test report

**Acceptance Criteria:**
- [ ] Activity Finder still uses Bootstrap 4
- [ ] Isolation still working
- [ ] No style conflicts
- [ ] Branch pages functional with Activity Finder

---

### Task 5: Migrate y_branch_menu Module
**Owner:** Developer
**Priority:** MEDIUM

**Actions:**

**5.1 Update menu templates:**
```twig
{# Update Bootstrap classes in menu templates #}
{# Update dropdown menus if present #}

{# OLD: #}
<div class="dropdown">
  <button data-toggle="dropdown">Menu</button>
  <div class="dropdown-menu">

{# NEW: #}
<div class="dropdown">
  <button data-bs-toggle="dropdown">Menu</button>
  <div class="dropdown-menu">
```

**5.2 Update menu styling:**
- Menu item styles
- Active states
- Hover states
- Branch-specific menu logic

**5.3 Test menu functionality:**
- [ ] Branch menu displays correctly
- [ ] Menu interactions work
- [ ] Active states correct
- [ ] Responsive menu works

**Deliverable:** Updated y_branch_menu module

**Acceptance Criteria:**
- [ ] Menu displays correctly
- [ ] Menu interactions work
- [ ] Bootstrap 5 classes used
- [ ] No JavaScript errors

---

### Task 6: Branch Finder Testing
**Owner:** Developer
**Priority:** HIGH

**Actions:**

**6.1 Test branch finder functionality:**
- [ ] Branch search works
- [ ] Branch filters work
- [ ] Branch results display correctly
- [ ] Branch map integration works (if present)
- [ ] Branch geolocation works (if present)
- [ ] Branch sorting works

**6.2 Test branch redirect logic:**
- [ ] User location detection works
- [ ] Branch redirects work
- [ ] Redirect preferences saved

**6.3 Test branch pages:**
- [ ] Branch full page displays correctly
- [ ] Branch amenities display
- [ ] Branch hours display
- [ ] Branch contact information displays
- [ ] Branch programs display (if present)

**Deliverable:** Branch finder test report

**Acceptance Criteria:**
- [ ] Branch finder fully functional
- [ ] All branch displays working
- [ ] No regressions from Bootstrap 4
- [ ] Mobile experience good

---

### Task 7: Visual Regression Testing
**Owner:** Developer
**Priority:** HIGH

**Actions:**

**7.1 Update BackstopJS scenarios:**
```json
{
  "scenarios": [
    {
      "label": "Branch Page Full",
      "url": "http://yusaopeny.docksal.site/branch/test-branch",
      "delay": 1000
    },
    {
      "label": "Branch Finder",
      "url": "http://yusaopeny.docksal.site/branch-finder",
      "delay": 1000
    },
    {
      "label": "Branch with Activity Finder",
      "url": "http://yusaopeny.docksal.site/branch/test-branch-with-af",
      "delay": 2000
    }
  ]
}
```

**7.2 Run visual regression tests:**
```bash
cd docs/bootstrap-5-migration/testing
npx backstop test
npx backstop openReport
```

**7.3 Document differences:**
- Expected differences (Bootstrap 5 improvements)
- Unexpected differences (investigate and fix)

**Deliverable:** Visual regression test report

**Acceptance Criteria:**
- [ ] Visual tests run successfully
- [ ] Differences documented
- [ ] Critical issues fixed
- [ ] Acceptable differences approved

---

### Task 8: Accessibility Testing
**Owner:** Developer
**Priority:** HIGH

**Actions:**

**8.1 Run Pa11y tests:**
```bash
cd docs/bootstrap-5-migration/testing
npx pa11y-ci
```

**8.2 Manual accessibility testing:**
- [ ] Keyboard navigation (branch pages)
- [ ] Screen reader testing (branch information)
- [ ] Focus indicators visible
- [ ] Form labels correct
- [ ] ARIA attributes correct
- [ ] Color contrast passes WCAG 2.2 AA

**8.3 Test branch-specific accessibility:**
- [ ] Branch amenities accessible
- [ ] Branch hours table accessible
- [ ] Branch contact information accessible
- [ ] Branch finder accessible

**Deliverable:** Accessibility test report

**Acceptance Criteria:**
- [ ] WCAG 2.2 AA compliance maintained
- [ ] No critical accessibility issues
- [ ] Keyboard navigation works
- [ ] Screen reader compatible

---

### Task 9: Documentation
**Owner:** Developer
**Priority:** MEDIUM

**Actions:**

**9.1 Document branch module migration:**
```bash
touch docs/bootstrap-5-migration/modules/y_branch.md
touch docs/bootstrap-5-migration/modules/y_branch_menu.md
```

**9.2 Document content type migration patterns:**
- Template migration process
- Styling migration process
- Activity Finder integration verification
- Testing approach

**9.3 Update migration log:**
```bash
vim docs/bootstrap-5-migration/MIGRATION_LOG.md
```

**Deliverable:** Complete module documentation

**Acceptance Criteria:**
- [ ] Module docs created
- [ ] Migration patterns documented
- [ ] Known issues documented
- [ ] Migration log updated

---

## Testing

### Manual Testing Checklist

**Branch Pages:**
- [ ] Branch full page displays correctly
- [ ] Branch teaser displays correctly
- [ ] Branch amenities section
- [ ] Branch hours section
- [ ] Branch contact section
- [ ] Branch location/map section

**Branch Finder:**
- [ ] Search functionality
- [ ] Filter functionality
- [ ] Results display
- [ ] Location detection (if present)
- [ ] Branch redirects

**Activity Finder Integration:**
- [ ] Activity Finder on branch pages
- [ ] Style isolation maintained
- [ ] No console errors
- [ ] Responsive behavior

**Forms:**
- [ ] Branch add form
- [ ] Branch edit form
- [ ] Field configuration forms

**Responsive:**
- [ ] Mobile view (< 576px)
- [ ] Tablet view (576px - 768px)
- [ ] Desktop view (> 768px)

---

## Deliverables

### Must Have (Critical):
- [ ] y_branch module migrated to Bootstrap 5
- [ ] y_branch_menu module migrated to Bootstrap 5
- [ ] Branch pages display correctly
- [ ] Branch finder functional
- [ ] Activity Finder integration maintained
- [ ] Visual regression tests passed
- [ ] Accessibility tests passed
- [ ] Module documentation complete

### Should Have (High Priority):
- [ ] Branch redirect logic tested
- [ ] Content type migration patterns documented
- [ ] Known issues documented

### Nice to Have:
- [ ] Branch finder optimization opportunities identified
- [ ] Performance baseline established

---

## Decision Points

### Decision: Content Type Migration Pattern
**Question:** Should we establish a standard migration checklist for all content types?
**Options:**
- Create detailed checklist (recommended)
- Handle each content type uniquely
**Decision Maker:** Developer + Project Lead
**Documentation:** Content type migration patterns doc

---

## Risks

### Risk: Activity Finder Integration Breaks (MEDIUM)
**Impact:** HIGH - Activity Finder may not work on branch pages
**Mitigation:**
- Verify isolation early in sprint
- Test Activity Finder on branch pages frequently
- Have rollback plan ready
- Document isolation requirements

### Risk: Branch Finder Regression (MEDIUM)
**Impact:** MEDIUM - Branch finder may not work correctly
**Mitigation:**
- Test branch finder early
- Test geolocation thoroughly
- Test on mobile devices
- Document branch finder dependencies

### Risk: Template Changes Break Layout (LOW)
**Impact:** MEDIUM - Branch pages may display incorrectly
**Mitigation:**
- Test templates incrementally
- Use visual regression testing
- Test with realistic content
- Review all view modes

---

## Notes

### Important:
- This is the first content type sprint - establishes patterns
- Activity Finder integration must be tested thoroughly
- Branch modules are critical for YMCA sites
- Test with realistic content (not just test data)

### Tips:
- Start with template audit - understand scope
- Test Activity Finder integration early
- Document any issues for other content types
- Create reusable migration patterns

### Phase 4 Context:
- Sprint 14: Branch/location modules (this sprint)
- Sprint 15: Program/activity modules
- Sprint 16: Events/camps/facilities modules
- Sprint 17: Donation module + integration testing

---

## Sprint Review Checklist

At end of sprint, verify:
- [ ] All tasks completed
- [ ] Both modules migrated
- [ ] Branch pages functional
- [ ] Activity Finder integration maintained
- [ ] Testing complete
- [ ] Documentation complete
- [ ] Next sprint ready to start

---

## Navigation

- **Previous:** [Sprint 13 - LB Integration & Date Picker](SPRINT_13_LB_Integration_DatePicker.md)
- **Next:** [Sprint 15 - Program & Camp](SPRINT_15_Y_Program_Camp.md)
- **Phase:** [Phase 4 - Content Types](../phases/PHASE_4_CONTENT_TYPES.md)
- **Overview:** [Executive Summary](../EXECUTIVE_SUMMARY.md)

---

**Sprint Status:** ⬜ Not Started
**Last Updated:** 2025-10-17
