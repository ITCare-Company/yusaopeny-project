# Sprint 15: Program & Camp Modules

**Phase:** [Phase 4 - Content Types](../phases/PHASE_4_CONTENT_TYPES.md)
**Resources:** 1 Developer
**Status:** Not Started

---

## Sprint Goal

Migrate program and camp content type modules to Bootstrap 5, maintaining Activity Finder integration and program categorization. Focus on program display templates and taxonomy integration.

---

## Modules in This Sprint

### Primary Modules (3):
1. **y_program** - Program content type
   - Path: `docroot/modules/contrib/y_program`
   - Program pages and displays
   - Activity Finder integration points

2. **y_program_subcategory** - Program subcategory taxonomy
   - Path: `docroot/modules/contrib/y_program_subcategory`
   - Program categorization
   - Program filtering

3. **y_camp** - Camp content type
   - Path: `docroot/modules/contrib/y_camp`
   - Camp pages
   - Camp Finder integration (still BS4)

---

## Tasks

### Task 1: Audit Program & Camp Modules
**Owner:** Developer
**Priority:** CRITICAL

**Actions:**
```bash
# Review program module
cd docroot/modules/contrib/y_program
grep -r "bootstrap" .
find . -name "*.twig"
grep -r "activity_finder" .

# Review program subcategory
cd docroot/modules/contrib/y_program_subcategory
find . -name "*.twig"

# Review camp module
cd docroot/modules/contrib/y_camp
grep -r "bootstrap" .
find . -name "*.twig"
grep -r "camp_finder" .
```

**Document:**
- Program templates and views
- Program taxonomy displays
- Camp templates
- Activity Finder integration (y_program)
- Camp Finder integration (y_camp)
- Form displays and field formatters

**Deliverable:** Module audit documents

**Acceptance Criteria:**
- [ ] All Bootstrap 4 usage documented
- [ ] Integration points identified
- [ ] Template inventory complete
- [ ] Migration scope clear

---

### Task 2: Migrate y_program Module
**Owner:** Developer
**Priority:** CRITICAL

**Actions:**

**2.1 Update program page templates:**
```twig
{# Program full view #}
<article class="program">
  <div class="program-header">
    {# Update Bootstrap classes #}
  </div>
  <div class="program-content">
    {# Update data-bs-* attributes #}
  </div>
</article>

{# Program teaser view #}
<div class="card program-teaser">
  <div class="card-body">
    <h3 class="card-title">{{ program.title }}</h3>
    <div class="card-text">{{ program.description }}</div>
  </div>
</div>
```

**2.2 Update program display components:**
- Program header/hero section
- Program description
- Program schedule section
- Program registration links
- Program categories/tags
- Program location information
- Program instructor/staff (if present)

**2.3 Update program listing templates:**
- Program grid view
- Program list view
- Program filtered views
- Program search results

**2.4 Update program forms:**
- Program add/edit form
- Program settings
- Field configuration forms

**2.5 Update program styling:**
```scss
// Update SCSS files
@import "bootstrap/scss/functions";
@import "bootstrap/scss/variables";

.program {
  // Update deprecated variables
  // Update responsive breakpoints
}
```

**Deliverable:** Migrated y_program module

**Acceptance Criteria:**
- [ ] All templates use Bootstrap 5
- [ ] Program pages display correctly
- [ ] Program listings functional
- [ ] Forms styled correctly
- [ ] SCSS compiles without errors

---

### Task 3: Test Activity Finder on Program Pages
**Owner:** Developer
**Priority:** CRITICAL

**Actions:**

**3.1 Verify Activity Finder isolation:**
- [ ] Activity Finder still uses Bootstrap 4
- [ ] Scoped CSS still working
- [ ] No style conflicts

**3.2 Test Activity Finder on program pages:**
- [ ] Activity Finder renders correctly
- [ ] Program content displays around Activity Finder
- [ ] Search/filters work
- [ ] Results display correctly
- [ ] No console errors

**3.3 Test responsive behavior:**
- [ ] Mobile view with Activity Finder
- [ ] Tablet view with Activity Finder
- [ ] Desktop view with Activity Finder
- [ ] Touch interactions work

**Deliverable:** Activity Finder integration test report

**Acceptance Criteria:**
- [ ] Activity Finder functional on program pages
- [ ] Style isolation maintained
- [ ] No JavaScript errors
- [ ] Responsive behavior correct

---

### Task 4: Migrate y_program_subcategory Module
**Owner:** Developer
**Priority:** HIGH

**Actions:**

**4.1 Update taxonomy term templates:**
```twig
{# Program subcategory term display #}
<div class="program-category">
  <h2 class="category-title">{{ term.name }}</h2>
  <div class="category-description">
    {{ term.description }}
  </div>
</div>

{# Category tag display #}
<span class="badge bg-primary">{{ category }}</span>
```

**4.2 Update taxonomy views:**
- Category listing page
- Category filter displays
- Category in program displays
- Category breadcrumbs

**4.3 Update category styling:**
```scss
.program-category {
  // Update Bootstrap 5 classes
}

.badge {
  // Use new badge styles
}
```

**4.4 Test taxonomy functionality:**
- [ ] Taxonomy terms display correctly
- [ ] Category filtering works
- [ ] Category pages work
- [ ] Category in program displays

**Deliverable:** Migrated y_program_subcategory module

**Acceptance Criteria:**
- [ ] Taxonomy displays correct
- [ ] Category filtering works
- [ ] Bootstrap 5 classes used
- [ ] No display issues

---

### Task 5: Migrate y_camp Module
**Owner:** Developer
**Priority:** HIGH

**Actions:**

**5.1 Update camp page templates:**
```twig
{# Camp full view #}
<article class="camp">
  <div class="camp-header">
    {# Update Bootstrap classes #}
  </div>
  <div class="camp-content">
    {# Camp sessions, dates, registration #}
  </div>
</article>

{# Camp teaser #}
<div class="card camp-teaser">
  <div class="card-body">
    <h3 class="card-title">{{ camp.title }}</h3>
    <div class="camp-dates">{{ dates }}</div>
  </div>
</div>
```

**5.2 Update camp display components:**
- Camp header/hero
- Camp description
- Camp sessions display
- Camp dates/schedule
- Camp registration section
- Camp location information
- Camp pricing information

**5.3 Update camp forms:**
- Camp add/edit form
- Camp session configuration
- Camp registration settings

**5.4 Update camp styling:**
```scss
.camp {
  // Update Bootstrap 5 classes
  // Update responsive breakpoints
}
```

**5.5 Camp Finder placeholder:**
```html
<!-- Camp Finder still Bootstrap 4 (isolated) -->
<!-- Will be migrated in Phase 5 Sprint 21 -->
<div class="camp-finder-wrapper">
  <!-- Camp Finder component here -->
</div>
```

**Deliverable:** Migrated y_camp module

**Acceptance Criteria:**
- [ ] Camp pages display correctly
- [ ] Camp sessions display correctly
- [ ] Camp forms functional
- [ ] Camp Finder integration maintained
- [ ] Bootstrap 5 classes used

---

### Task 6: Integration Testing
**Owner:** Developer
**Priority:** HIGH

**Actions:**

**6.1 Test program/camp together:**
- [ ] Multiple programs on site
- [ ] Multiple camps on site
- [ ] Program categories work
- [ ] Camp categories work (if present)
- [ ] Program listings
- [ ] Camp listings
- [ ] Search/filter across both

**6.2 Test with Activity Finder:**
- [ ] Activity Finder on program pages
- [ ] Activity Finder on camp pages (if applicable)
- [ ] No conflicts between content types

**6.3 Test views and listings:**
- [ ] Program views display correctly
- [ ] Camp views display correctly
- [ ] Category views display correctly
- [ ] Combined listings work

**Deliverable:** Integration test report

**Acceptance Criteria:**
- [ ] All modules work together
- [ ] No conflicts or errors
- [ ] Views functional
- [ ] Activity Finder integration maintained

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
      "label": "Program Page Full",
      "url": "http://yusaopeny.docksal.site/program/test-program"
    },
    {
      "label": "Program with Activity Finder",
      "url": "http://yusaopeny.docksal.site/program/test-program-af"
    },
    {
      "label": "Program Listing",
      "url": "http://yusaopeny.docksal.site/programs"
    },
    {
      "label": "Camp Page Full",
      "url": "http://yusaopeny.docksal.site/camp/test-camp"
    },
    {
      "label": "Camp Listing",
      "url": "http://yusaopeny.docksal.site/camps"
    },
    {
      "label": "Program Category",
      "url": "http://yusaopeny.docksal.site/programs/category/fitness"
    }
  ]
}
```

**7.2 Run and review tests:**
```bash
cd docs/bootstrap-5-migration/testing
npx backstop test
npx backstop openReport
```

**Deliverable:** Visual regression report

**Acceptance Criteria:**
- [ ] Visual tests passed
- [ ] Differences documented
- [ ] Critical issues fixed

---

### Task 8: Accessibility Testing
**Owner:** Developer
**Priority:** HIGH

**Actions:**

**8.1 Run Pa11y tests:**
```bash
npx pa11y-ci
```

**8.2 Manual accessibility testing:**
- [ ] Keyboard navigation (program/camp pages)
- [ ] Screen reader testing
- [ ] Focus indicators visible
- [ ] Form labels correct
- [ ] ARIA attributes correct
- [ ] Color contrast WCAG 2.2 AA

**8.3 Test specific components:**
- [ ] Program schedule accessible
- [ ] Camp sessions accessible
- [ ] Registration links accessible
- [ ] Category filters accessible

**Deliverable:** Accessibility test report

**Acceptance Criteria:**
- [ ] WCAG 2.2 AA compliance
- [ ] No critical accessibility issues
- [ ] Keyboard navigation works
- [ ] Screen reader compatible

---

### Task 9: Documentation
**Owner:** Developer
**Priority:** MEDIUM

**Actions:**

**9.1 Document module migrations:**
```bash
touch docs/bootstrap-5-migration/modules/y_program.md
touch docs/bootstrap-5-migration/modules/y_program_subcategory.md
touch docs/bootstrap-5-migration/modules/y_camp.md
```

**9.2 Document patterns:**
- Taxonomy integration patterns
- Program display patterns
- Activity Finder integration maintenance
- Camp Finder placeholder approach

**9.3 Update migration log:**
```bash
vim docs/bootstrap-5-migration/MIGRATION_LOG.md
```

**Deliverable:** Complete documentation

**Acceptance Criteria:**
- [ ] Module docs created
- [ ] Patterns documented
- [ ] Known issues documented
- [ ] Migration log updated

---

## Testing

### Manual Testing Checklist

**Program Pages:**
- [ ] Program full page
- [ ] Program teaser view
- [ ] Program listing
- [ ] Program category pages
- [ ] Program with Activity Finder
- [ ] Program schedule display
- [ ] Program registration links

**Camp Pages:**
- [ ] Camp full page
- [ ] Camp teaser view
- [ ] Camp listing
- [ ] Camp sessions display
- [ ] Camp dates/schedule
- [ ] Camp registration section
- [ ] Camp with Camp Finder (if applicable)

**Taxonomy:**
- [ ] Program categories display
- [ ] Category filtering
- [ ] Category pages
- [ ] Category in program displays
- [ ] Category badges/tags

**Forms:**
- [ ] Program add/edit forms
- [ ] Camp add/edit forms
- [ ] Field configuration forms

**Responsive:**
- [ ] Mobile view (< 576px)
- [ ] Tablet view (576px - 768px)
- [ ] Desktop view (> 768px)

---

## Deliverables

### Must Have (Critical):
- [ ] y_program module migrated
- [ ] y_program_subcategory module migrated
- [ ] y_camp module migrated
- [ ] Program pages display correctly
- [ ] Camp pages display correctly
- [ ] Activity Finder integration maintained
- [ ] Category filtering works
- [ ] Visual regression tests passed
- [ ] Accessibility tests passed

### Should Have (High Priority):
- [ ] Integration test report
- [ ] Module documentation complete
- [ ] Known issues documented

### Nice to Have:
- [ ] Performance comparison
- [ ] Optimization opportunities identified

---

## Decision Points

### Decision: Camp Finder Isolation
**Question:** Should Camp Finder be isolated now or wait for Phase 5?
**Answer:** Wait for Phase 5 Sprint 18 (Camp Finder isolation sprint)
**Rationale:** Camp Finder will be isolated at start of Phase 5

---

## Risks

### Risk: Activity Finder Integration Issues (MEDIUM)
**Impact:** HIGH - Activity Finder may break on program pages
**Mitigation:**
- Test Activity Finder early and frequently
- Verify isolation maintained
- Document integration points
- Have rollback plan

### Risk: Taxonomy Display Issues (LOW)
**Impact:** MEDIUM - Categories may not display correctly
**Mitigation:**
- Test taxonomy displays thoroughly
- Test category filtering
- Test with realistic data
- Document taxonomy patterns

### Risk: Camp Finder Not Yet Isolated (LOW)
**Impact:** LOW - Camp module migration may affect Camp Finder
**Mitigation:**
- Document Camp Finder integration points
- Test Camp Finder on camp pages
- Prepare for Phase 5 isolation
- Minimal changes to Camp Finder integration

---

## Notes

### Important:
- Activity Finder integration critical for program pages
- Camp Finder will be isolated in Phase 5 Sprint 18
- Taxonomy displays important for program filtering
- Test with realistic program/camp content

### Tips:
- Use patterns from Sprint 14 (branch modules)
- Document any new patterns discovered
- Test Activity Finder frequently
- Create realistic test content

### Phase 4 Context:
- Sprint 14: Branch/location modules (complete)
- Sprint 15: Program/camp modules (this sprint)
- Sprint 16: Facility & LB modules
- Sprint 17: Donation module + testing

---

## Sprint Review Checklist

At end of sprint, verify:
- [ ] All 3 modules migrated
- [ ] Program pages functional
- [ ] Camp pages functional
- [ ] Activity Finder integration maintained
- [ ] Category filtering works
- [ ] Testing complete
- [ ] Documentation complete
- [ ] Next sprint ready

---

## Navigation

- **Previous:** [Sprint 14 - Branch & Location](SPRINT_14_Y_Branch_Related.md)
- **Next:** [Sprint 16 - Facility & LB](SPRINT_16_Y_Facility_LB.md)
- **Phase:** [Phase 4 - Content Types](../phases/PHASE_4_CONTENT_TYPES.md)
- **Overview:** [Executive Summary](../EXECUTIVE_SUMMARY.md)

---

**Sprint Status:** ⬜ Not Started
**Last Updated:** 2025-10-17
