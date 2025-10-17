# Sprint 16: Facility & Landing Page Modules

**Phase:** [Phase 4 - Content Types](../phases/PHASE_4_CONTENT_TYPES.md)
**Resources:** 1 Developer
**Status:** Not Started

---

## Sprint Goal

Migrate facility and landing page modules to Bootstrap 5, with special focus on Layout Builder integration for y_lb (landing page) content type. This sprint tests LB integration extensively with content types.

---

## Modules in This Sprint

### Primary Modules (3):
1. **y_facility** - Facility content type
   - Path: `docroot/modules/contrib/y_facility`
   - Facility pages and displays
   - Facility amenities

2. **y_lb** + **y_lb_main_menu_cta_block** - Landing page content type
   - Path: `docroot/modules/contrib/y_lb`
   - Landing page builder
   - Layout Builder integration (CRITICAL)
   - Main menu CTA block

3. **y_lb_article** - Article landing page extension
   - Path: `docroot/modules/contrib/y_lb_article`
   - Article-specific landing pages
   - Layout Builder integration

---

## Tasks

### Task 1: Audit Facility & LB Modules
**Owner:** Developer
**Priority:** CRITICAL

**Actions:**
```bash
# Review facility module
cd docroot/modules/contrib/y_facility
grep -r "bootstrap" .
find . -name "*.twig"

# Review y_lb module (CRITICAL)
cd docroot/modules/contrib/y_lb
grep -r "bootstrap" .
grep -r "layout_builder" .
find . -name "*.twig"

# Review y_lb_article
cd docroot/modules/contrib/y_lb_article
find . -name "*.twig"
```

**Document:**
- Facility templates and styling
- y_lb Layout Builder integration points
- LB module dependencies (from Phase 3)
- Templates using LB components
- Main menu CTA block

**Deliverable:** Module audit documents

**Acceptance Criteria:**
- [ ] All Bootstrap usage documented
- [ ] Layout Builder integration points identified
- [ ] LB module dependencies documented
- [ ] Migration scope clear

---

### Task 2: Migrate y_facility Module
**Owner:** Developer
**Priority:** HIGH

**Actions:**

**2.1 Update facility page templates:**
```twig
{# Facility full view #}
<article class="facility">
  <div class="facility-header">
    <h1>{{ facility.title }}</h1>
  </div>
  <div class="facility-content">
    {# Update Bootstrap 5 classes #}
  </div>
</article>

{# Facility teaser #}
<div class="card facility-teaser">
  <div class="card-img-top">{{ image }}</div>
  <div class="card-body">
    <h3 class="card-title">{{ title }}</h3>
  </div>
</div>
```

**2.2 Update facility components:**
- Facility header/hero
- Facility description
- Facility amenities section
- Facility schedule/hours
- Facility location information
- Facility contact section
- Facility images/gallery

**2.3 Update facility forms:**
- Facility add/edit form
- Amenities field
- Schedule field

**2.4 Update facility styling:**
```scss
@import "bootstrap/scss/functions";
@import "bootstrap/scss/variables";

.facility {
  // Update Bootstrap 5 classes
  // Update deprecated variables
}

.facility-amenities {
  // Update grid system
  display: grid;
  // or use Bootstrap 5 grid
}
```

**Deliverable:** Migrated y_facility module

**Acceptance Criteria:**
- [ ] Facility pages display correctly
- [ ] Amenities display correctly
- [ ] Forms functional
- [ ] Bootstrap 5 classes used
- [ ] SCSS compiles without errors

---

### Task 3: Migrate y_lb Module (CRITICAL)
**Owner:** Developer
**Priority:** CRITICAL

**Actions:**

**3.1 Update landing page templates:**
```twig
{# Landing page with Layout Builder #}
<article class="landing-page">
  {# Layout Builder content region #}
  <div class="layout-builder-content">
    {{ content.layout_builder }}
  </div>
</article>
```

**3.2 Test Layout Builder integration:**
- [ ] LB components render in y_lb pages
- [ ] Multiple LB components on same page
- [ ] LB component configuration preserved
- [ ] LB inline editing works
- [ ] LB component library accessible

**3.3 Test all Phase 3 LB modules with y_lb:**

**High Priority LB Components:**
- [ ] lb_hero on landing page
- [ ] lb_cards on landing page
- [ ] lb_carousel on landing page
- [ ] lb_modal on landing page
- [ ] lb_webform on landing page
- [ ] lb_accordion on landing page

**Medium Priority LB Components:**
- [ ] lb_amenities on landing page
- [ ] lb_hours on landing page
- [ ] lb_social_links on landing page
- [ ] lb_promo on landing page
- [ ] lb_grid_cta on landing page

**Lower Priority LB Components:**
- [ ] lb_staff on landing page
- [ ] lb_statistics on landing page
- [ ] lb_testimonials on landing page
- [ ] lb_table on landing page

**3.4 Test LB component interactions:**
- [ ] Add LB component to page
- [ ] Configure LB component
- [ ] Reorder LB components
- [ ] Remove LB component
- [ ] Save page with LB components
- [ ] View page with LB components

**3.5 Update main menu CTA block:**
```twig
{# y_lb_main_menu_cta_block submodule #}
<div class="cta-block">
  <a href="{{ url }}" class="btn btn-primary">
    {{ label }}
  </a>
</div>
```

**3.6 Update landing page styling:**
```scss
.landing-page {
  // Ensure LB components display correctly
  // No conflicts with LB component styles
}

.layout-builder-content {
  // Container styles for LB content
}
```

**Deliverable:** Migrated y_lb module with full LB integration

**Acceptance Criteria:**
- [ ] Landing pages display correctly
- [ ] All Phase 3 LB components work in y_lb
- [ ] LB inline editing works
- [ ] No style conflicts with LB components
- [ ] Main menu CTA block works
- [ ] Bootstrap 5 classes used

---

### Task 4: Layout Builder Integration Testing
**Owner:** Developer
**Priority:** CRITICAL

**Actions:**

**4.1 Create comprehensive test landing pages:**
```bash
# Create test landing pages with various LB components
drush node:create landing-page

# Test pages to create:
# 1. Hero + Cards + CTA
# 2. Carousel + Webform + Modal
# 3. Accordion + Testimonials + Stats
# 4. Multiple components of same type
# 5. All LB components (kitchen sink)
```

**4.2 Test component combinations:**
- [ ] Hero + Cards + Grid CTA
- [ ] Carousel + Modal (modal inside carousel)
- [ ] Tabs + Accordion + Collapse
- [ ] Webform + Modal (webform in modal)
- [ ] Staff + Testimonials + Partners
- [ ] Multiple carousels on same page
- [ ] Multiple modals on same page

**4.3 Test LB edit mode:**
- [ ] Add component via component library
- [ ] Configure component settings
- [ ] Reorder components drag-drop
- [ ] Remove component
- [ ] Duplicate component
- [ ] Preview changes
- [ ] Save changes

**4.4 Test LB view mode:**
- [ ] All components render correctly
- [ ] Component interactions work (modal, carousel, etc.)
- [ ] No JavaScript conflicts
- [ ] No console errors
- [ ] Responsive display correct

**4.5 Test edge cases:**
- [ ] Empty landing page
- [ ] Landing page with 20+ components
- [ ] Nested components (if applicable)
- [ ] Components with missing content
- [ ] Components with long content

**Deliverable:** LB integration test report

**Acceptance Criteria:**
- [ ] All LB components work in y_lb
- [ ] Component combinations work
- [ ] Edit mode functional
- [ ] View mode functional
- [ ] No critical issues
- [ ] Edge cases handled

---

### Task 5: Migrate y_lb_article Module
**Owner:** Developer
**Priority:** MEDIUM

**Actions:**

**5.1 Update article landing page templates:**
```twig
{# Article landing page #}
<article class="article-landing-page">
  <div class="article-content">
    {{ content.body }}
  </div>
  <div class="layout-builder-content">
    {{ content.layout_builder }}
  </div>
</article>
```

**5.2 Test article landing pages:**
- [ ] Article content displays correctly
- [ ] LB components work with articles
- [ ] Article metadata displays
- [ ] Article navigation works

**5.3 Update article styling:**
```scss
.article-landing-page {
  // Ensure article content and LB content coexist
}
```

**Deliverable:** Migrated y_lb_article module

**Acceptance Criteria:**
- [ ] Article landing pages display correctly
- [ ] LB integration works
- [ ] Article content and LB content coexist
- [ ] Bootstrap 5 classes used

---

### Task 6: Visual Regression Testing
**Owner:** Developer
**Priority:** HIGH

**Actions:**

**6.1 Update BackstopJS scenarios:**
```json
{
  "scenarios": [
    {
      "label": "Facility Page",
      "url": "http://yusaopeny.docksal.site/facility/test-facility"
    },
    {
      "label": "Landing Page - Hero Cards",
      "url": "http://yusaopeny.docksal.site/landing/test-hero-cards"
    },
    {
      "label": "Landing Page - Kitchen Sink",
      "url": "http://yusaopeny.docksal.site/landing/test-kitchen-sink"
    },
    {
      "label": "Article Landing Page",
      "url": "http://yusaopeny.docksal.site/article/test-article-landing"
    },
    {
      "label": "Landing Page LB Edit Mode",
      "url": "http://yusaopeny.docksal.site/node/123/layout",
      "requireAuth": true
    }
  ]
}
```

**6.2 Run and review tests:**
```bash
cd docs/bootstrap-5-migration/testing
npx backstop test
npx backstop openReport
```

**6.3 Test LB component rendering:**
- Visual tests for each LB component in landing pages
- Compare to standalone LB component pages

**Deliverable:** Visual regression report

**Acceptance Criteria:**
- [ ] Visual tests passed
- [ ] LB components render correctly in y_lb
- [ ] Differences documented
- [ ] Critical issues fixed

---

### Task 7: Accessibility Testing
**Owner:** Developer
**Priority:** HIGH

**Actions:**

**7.1 Run Pa11y tests:**
```bash
npx pa11y-ci
```

**7.2 Manual accessibility testing:**
- [ ] Keyboard navigation (facility/landing pages)
- [ ] Screen reader testing
- [ ] Focus indicators visible
- [ ] LB component accessibility maintained
- [ ] Form labels correct
- [ ] ARIA attributes correct
- [ ] Color contrast WCAG 2.2 AA

**7.3 Test LB edit mode accessibility:**
- [ ] Keyboard navigation in edit mode
- [ ] Screen reader in edit mode
- [ ] Component library accessible
- [ ] Drag-drop accessible (keyboard alternative)

**Deliverable:** Accessibility test report

**Acceptance Criteria:**
- [ ] WCAG 2.2 AA compliance
- [ ] No critical accessibility issues
- [ ] Keyboard navigation works
- [ ] Screen reader compatible
- [ ] LB edit mode accessible

---

### Task 8: Documentation
**Owner:** Developer
**Priority:** MEDIUM

**Actions:**

**8.1 Document module migrations:**
```bash
touch docs/bootstrap-5-migration/modules/y_facility.md
touch docs/bootstrap-5-migration/modules/y_lb.md
touch docs/bootstrap-5-migration/modules/y_lb_article.md
```

**8.2 Document LB integration:**
- LB component usage in y_lb
- LB component combinations tested
- LB edit mode functionality
- Known LB integration issues
- Best practices for LB with content types

**8.3 Update migration log:**
```bash
vim docs/bootstrap-5-migration/MIGRATION_LOG.md
```

**Deliverable:** Complete documentation

**Acceptance Criteria:**
- [ ] Module docs created
- [ ] LB integration documented
- [ ] Known issues documented
- [ ] Migration log updated

---

## Testing

### Manual Testing Checklist

**Facility Pages:**
- [ ] Facility full page
- [ ] Facility teaser view
- [ ] Facility listing
- [ ] Facility amenities section
- [ ] Facility schedule/hours
- [ ] Facility forms

**Landing Pages (y_lb):**
- [ ] Empty landing page
- [ ] Landing page with hero
- [ ] Landing page with multiple components
- [ ] Landing page kitchen sink
- [ ] LB edit mode
- [ ] LB component library
- [ ] LB component configuration
- [ ] LB component reordering

**Article Landing Pages:**
- [ ] Article with LB components
- [ ] Article content display
- [ ] Article metadata

**Layout Builder Components:**
- [ ] All Phase 3 LB components in y_lb
- [ ] Component interactions
- [ ] Component combinations

**Responsive:**
- [ ] Mobile view (< 576px)
- [ ] Tablet view (576px - 768px)
- [ ] Desktop view (> 768px)

---

## Deliverables

### Must Have (Critical):
- [ ] y_facility module migrated
- [ ] y_lb module migrated
- [ ] y_lb_article module migrated
- [ ] Layout Builder integration working
- [ ] All Phase 3 LB components work in y_lb
- [ ] LB edit mode functional
- [ ] Visual regression tests passed
- [ ] Accessibility tests passed

### Should Have (High Priority):
- [ ] LB integration test report
- [ ] Component combinations tested
- [ ] Module documentation complete
- [ ] Known issues documented

### Nice to Have:
- [ ] LB performance testing
- [ ] LB optimization recommendations

---

## Decision Points

### Decision: LB Component Support
**Question:** Should all Phase 3 LB components be tested with y_lb?
**Answer:** Yes - y_lb is primary use case for LB components
**Rationale:** Landing pages use LB extensively, must verify all components work

---

## Risks

### Risk: Layout Builder Integration Breaks (CRITICAL)
**Impact:** CRITICAL - Landing pages may not work
**Mitigation:**
- Verify Phase 3 LB modules stable first
- Test LB components incrementally
- Test component combinations extensively
- Document integration requirements
- Have rollback plan
- Allocate extra time for debugging

### Risk: LB Component Style Conflicts (HIGH)
**Impact:** HIGH - Components may not display correctly
**Mitigation:**
- Ensure y_lb styles don't override LB component styles
- Test each LB component in y_lb
- Use visual regression testing
- Fix conflicts immediately

### Risk: LB Edit Mode Issues (MEDIUM)
**Impact:** MEDIUM - Content editors can't create pages
**Mitigation:**
- Test edit mode thoroughly
- Test all edit actions (add, configure, reorder, remove)
- Test with realistic editor workflow
- Document edit mode issues

---

## Notes

### Important:
- y_lb is most critical module in Phase 4
- Layout Builder integration is key success factor
- All Phase 3 LB components must work
- Test extensively with realistic content
- LB edit mode must be functional

### Tips:
- Test LB integration early and frequently
- Create comprehensive test landing pages
- Document LB component combinations
- Test both edit and view modes
- Use Phase 3 LB tests as reference

### Phase 4 Context:
- Sprint 14: Branch/location modules (complete)
- Sprint 15: Program/camp modules (complete)
- Sprint 16: Facility & LB modules (this sprint)
- Sprint 17: Donation + integration testing

### Layout Builder Dependencies:
Phase 3 LB modules (19 modules) must be stable:
- High Priority: hero, cards, carousel, modal, webform, accordion
- Medium Priority: amenities, hours, social links, promo, grid CTA, etc.
- Lower Priority: staff, statistics, testimonials, table

---

## Sprint Review Checklist

At end of sprint, verify:
- [ ] All 3 modules migrated
- [ ] Facility pages functional
- [ ] Landing pages functional
- [ ] Layout Builder integration working
- [ ] All LB components tested
- [ ] Testing complete
- [ ] Documentation complete
- [ ] Next sprint ready

---

## Navigation

- **Previous:** [Sprint 15 - Program & Camp](SPRINT_15_Y_Program_Camp.md)
- **Next:** [Sprint 17 - Donate & Testing](SPRINT_17_Y_Donate_Testing.md)
- **Phase:** [Phase 4 - Content Types](../phases/PHASE_4_CONTENT_TYPES.md)
- **Overview:** [Executive Summary](../EXECUTIVE_SUMMARY.md)

---

**Sprint Status:** ⬜ Not Started
**Last Updated:** 2025-10-17
