# Sprint 21: Activity Finder 4 Migration & Phase 5 Testing

**Phase:** [Phase 5 - Activity Finder](../phases/PHASE_5_ACTIVITY_FINDER.md)
**Resources:** 1 Frontend Developer + QA Support
**Status:** Not Started

---

## Sprint Goal

Migrate Activity Finder 4 (openy_af4_vue_app) to Bootstrap 5, complete comprehensive Phase 5 integration testing of all 3 Vue.js applications, and make GO/NO-GO decision for Phase 6.

---

## Module in This Sprint

**openy_af4_vue_app** - Activity Finder 4 Vue.js Application
- Path: `docroot/modules/contrib/yusaopeny_activity_finder/openy_af4_vue_app`
- Current: Vue.js 2 + BootstrapVue 2 + Bootstrap 4.6.1 (isolated)
- Target: Vue.js 2 + Custom Components + Bootstrap 5.3.3
- Priority: HIGH (most modern implementation, most used)
- Isolation: Remove after migration complete

---

## Tasks

### Task 1: Migrate Activity Finder 4
**Owner:** Developer
**Priority:** CRITICAL

**Actions:**

**1.1 Prepare for migration:**
```bash
cd docroot/modules/contrib/yusaopeny_activity_finder/openy_af4_vue_app

# Review structure (most modern AF version)
# Use Sprint 19 & 20 patterns
```

**1.2 Update dependencies:**
```bash
# Remove BootstrapVue
npm uninstall bootstrap-vue

# Update Bootstrap
npm uninstall bootstrap@4.6.1
npm install bootstrap@5.3.3 @popperjs/core

# Link custom component library
```

**1.3 Remove Bootstrap 4 isolation:**
- Remove webpack CSS scoping
- Update SCSS to Bootstrap 5
- Remove template wrapper

**1.4 Replace BootstrapVue components:**

**Key components (same patterns as Sprint 19-20):**
- SearchForm.vue → Replace b-form-*, b-button
- FilterPanel.vue → Replace b-form-select, b-button-group
- ResultsList.vue → Replace b-card
- ResultsMap.vue (if present) → Replace b-* components
- ActivityDetailModal.vue → Replace b-modal
- ScheduleView.vue (if present) → Replace b-table, b-tabs

**Example (same as previous sprints):**
```vue
<!-- OLD: BootstrapVue -->
<b-form @submit.prevent="onSubmit">
  <b-form-input v-model="search" />
  <b-button type="submit" variant="primary">Search</b-button>
</b-form>

<!-- NEW: Custom components -->
<form @submit.prevent="onSubmit">
  <bs-form-input v-model="search" />
  <bs-button type="submit" variant="primary">Search</bs-button>
</form>
```

**1.5 Update styling:**
- Bootstrap 4 → Bootstrap 5 classes
- Utility classes (ml/mr → ms/me)
- Form classes (form-group → mb-3)
- Grid gutters
- Data attributes (data-toggle → data-bs-toggle)

**1.6 Build and initial test:**
```bash
npm run dev
npm run build
```

**Test basic functionality:**
- [ ] App loads
- [ ] Search works
- [ ] Filters work
- [ ] Results display
- [ ] No console errors

**Deliverable:** Migrated Activity Finder 4

**Acceptance Criteria:**
- [ ] BootstrapVue removed
- [ ] Bootstrap 5.3.3 integrated
- [ ] Custom components used
- [ ] Isolation removed
- [ ] Build succeeds
- [ ] Basic functionality works

---

### Task 2: Comprehensive Activity Finder 4 Testing
**Owner:** Developer
**Priority:** CRITICAL

**Actions:**

**2.1 Test search functionality:**
- [ ] Keyword search
- [ ] Location-based search
- [ ] Advanced search options
- [ ] Empty search
- [ ] No results
- [ ] Many results
- [ ] Pagination

**2.2 Test filters:**
- [ ] Location filter
- [ ] Category filter
- [ ] Age group filter
- [ ] Day of week filter
- [ ] Time of day filter
- [ ] Instructor filter (if present)
- [ ] Multiple filters combined
- [ ] Clear filters
- [ ] Filter persistence (URL params)

**2.3 Test results display:**
- [ ] List view
- [ ] Grid view
- [ ] Map view (if present)
- [ ] Calendar view (if present)
- [ ] Activity cards render correctly
- [ ] Activity details display
- [ ] Registration links work
- [ ] Favorite/save functionality (if present)

**2.4 Test activity details:**
- [ ] Detail modal opens
- [ ] All activity information displays
- [ ] Schedule information
- [ ] Location information
- [ ] Instructor information
- [ ] Pricing information
- [ ] Registration button works
- [ ] Share functionality (if present)

**2.5 Test responsive:**
- [ ] Desktop view (> 992px)
- [ ] Tablet view (768px - 992px)
- [ ] Mobile view (< 768px)
- [ ] Touch interactions
- [ ] Mobile keyboard
- [ ] Orientation changes

**2.6 Test on Drupal pages:**
- [ ] Activity Finder 4 on branch pages
- [ ] Activity Finder 4 on program pages
- [ ] Data loads from Drupal API
- [ ] No style conflicts with page
- [ ] Page layout maintained

**Deliverable:** Activity Finder 4 test report

**Acceptance Criteria:**
- [ ] All functionality works
- [ ] No regressions from Bootstrap 4 version
- [ ] Responsive design works
- [ ] Integration with Drupal works
- [ ] No console errors

---

### Task 3: Phase 5 Integration Testing - All 3 Vue Apps
**Owner:** Developer + QA
**Priority:** CRITICAL

**Actions:**

**3.1 Test all 3 Vue apps on same site:**

**Apps:**
1. Camp Finder (openy_cf_vue_app) - Sprint 19
2. Activity Finder (openy_af_vue_app) - Sprint 20
3. Activity Finder 4 (openy_af4_vue_app) - Sprint 21

**3.2 Test each app individually:**
- [ ] Camp Finder fully functional
- [ ] Activity Finder fully functional
- [ ] Activity Finder 4 fully functional
- [ ] All apps use Bootstrap 5.3.3
- [ ] All apps use custom component library
- [ ] No BootstrapVue remaining

**3.3 Test apps together on same site:**
- [ ] All 3 apps installed
- [ ] No JavaScript conflicts
- [ ] No style conflicts
- [ ] No CSS specificity issues
- [ ] Each app works independently

**3.4 Test navigation between apps:**
- [ ] Navigate from Camp Finder page to Activity Finder page
- [ ] Navigate from Activity Finder to Activity Finder 4 page
- [ ] Navigate back and forth
- [ ] Apps load correctly after navigation
- [ ] No memory leaks

**3.5 Test app combinations on pages:**
- [ ] Branch page with Activity Finder 4
- [ ] Program page with Activity Finder 4
- [ ] Camp page with Camp Finder
- [ ] Landing page with multiple finders (if applicable)

**3.6 Test with Layout Builder modules:**
- [ ] Vue apps in pages with LB components
- [ ] LB modal + Vue app on same page
- [ ] LB carousel + Vue app on same page
- [ ] No conflicts with LB JavaScript

**3.7 Test with content types (Phase 4):**
- [ ] Vue apps on branch pages (y_branch)
- [ ] Vue apps on program pages (y_program)
- [ ] Vue apps on camp pages (y_camp)
- [ ] Vue apps on facility pages (y_facility)
- [ ] Vue apps on landing pages (y_lb)

**3.8 Create comprehensive test site:**
```bash
# Create test site with all components
drush site:install

# Create content
drush node:create branch --title="Test Branch with AF4"
drush node:create program --title="Test Program with AF4"
drush node:create camp --title="Test Camp with CF"
drush node:create landing-page --title="Test Landing with Multiple Finders"

# Add Vue apps to pages
# Test all combinations
```

**Deliverable:** Phase 5 integration test report

**Acceptance Criteria:**
- [ ] All 3 Vue apps work together
- [ ] No conflicts between apps
- [ ] Integration with Drupal maintained
- [ ] Integration with LB modules works
- [ ] Integration with content types works
- [ ] Realistic test site created

---

### Task 4: Visual Regression Testing - All Phase 5
**Owner:** Developer
**Priority:** HIGH

**Actions:**

**4.1 Update BackstopJS with all Vue apps:**
```json
{
  "scenarios": [
    // Camp Finder
    {"label": "Camp Finder - Initial", "url": "http://yusaopeny.docksal.site/camp-finder"},
    {"label": "Camp Finder - Results", "url": "http://yusaopeny.docksal.site/camp-finder?search=summer"},

    // Activity Finder (Legacy)
    {"label": "Activity Finder - Initial", "url": "http://yusaopeny.docksal.site/activity-finder"},
    {"label": "Activity Finder - Results", "url": "http://yusaopeny.docksal.site/activity-finder?search=yoga"},

    // Activity Finder 4
    {"label": "Activity Finder 4 - Initial", "url": "http://yusaopeny.docksal.site/activity-finder-v4"},
    {"label": "Activity Finder 4 - Results", "url": "http://yusaopeny.docksal.site/activity-finder-v4?search=swim"},

    // Integration pages
    {"label": "Branch with AF4", "url": "http://yusaopeny.docksal.site/branch/test-af4"},
    {"label": "Program with AF4", "url": "http://yusaopeny.docksal.site/program/test-af4"},
    {"label": "Camp with CF", "url": "http://yusaopeny.docksal.site/camp/test-cf"}
  ]
}
```

**4.2 Run comprehensive visual tests:**
```bash
cd docs/bootstrap-5-migration/testing
npx backstop test
npx backstop openReport
```

**4.3 Review and document differences:**
- Expected differences (Bootstrap 5 improvements)
- Unexpected differences (investigate and fix)
- Acceptable differences (minor rendering)

**Deliverable:** Phase 5 visual regression report

**Acceptance Criteria:**
- [ ] Visual tests run successfully
- [ ] All Vue apps tested
- [ ] Differences documented
- [ ] Critical issues fixed

---

### Task 5: Accessibility Testing - All Phase 5
**Owner:** Developer + QA
**Priority:** HIGH

**Actions:**

**5.1 Run Pa11y tests on all Vue apps:**
```bash
npx pa11y-ci
```

**5.2 Manual accessibility testing:**
- [ ] Keyboard navigation (all 3 Vue apps)
- [ ] Screen reader testing (all 3 Vue apps)
- [ ] Focus indicators visible
- [ ] Form labels correct
- [ ] ARIA attributes correct
- [ ] Color contrast WCAG 2.2 AA

**5.3 Test Vue app accessibility:**

**Camp Finder:**
- [ ] Search form accessible
- [ ] Filter controls accessible
- [ ] Results announced
- [ ] Modal accessible

**Activity Finder:**
- [ ] Search form accessible
- [ ] Filter controls accessible
- [ ] Results announced
- [ ] Map accessible (if present)

**Activity Finder 4:**
- [ ] Search form accessible
- [ ] Filter controls accessible
- [ ] Results announced
- [ ] Calendar accessible (if present)

**5.4 Test dynamic content accessibility:**
- [ ] Loading states announced
- [ ] Error messages announced
- [ ] Results count announced
- [ ] Filter changes announced

**Deliverable:** Phase 5 accessibility report

**Acceptance Criteria:**
- [ ] WCAG 2.2 AA compliance maintained
- [ ] No critical accessibility issues
- [ ] Keyboard navigation works
- [ ] Screen reader compatible
- [ ] Dynamic content accessible

---

### Task 6: Performance Testing - All Vue Apps
**Owner:** Developer
**Priority:** MEDIUM

**Actions:**

**6.1 JavaScript bundle size analysis:**
```bash
# Compare bundle sizes: Bootstrap 4 vs Bootstrap 5
# Check compiled JavaScript sizes

for app in openy_cf_vue_app openy_af_vue_app openy_af4_vue_app; do
  echo "=== $app ==="
  ls -lh docroot/modules/contrib/yusaopeny_activity_finder/$app/dist/*.js
done
```

**6.2 Compare bundle sizes:**
- [ ] Camp Finder bundle size
- [ ] Activity Finder bundle size
- [ ] Activity Finder 4 bundle size
- [ ] Total vs Bootstrap 4 versions
- [ ] Identify size increases/decreases

**6.3 Page load performance:**
```bash
# Use Lighthouse or WebPageTest
# Test pages with Vue apps:
# - Branch page with Activity Finder 4
# - Program page with Activity Finder 4
# - Camp page with Camp Finder
```

**6.4 JavaScript performance profiling:**
- [ ] Use Chrome DevTools Performance tab
- [ ] Profile search operations
- [ ] Profile filter changes
- [ ] Check for memory leaks
- [ ] Check for unnecessary re-renders

**6.5 Optimization opportunities:**
- [ ] Lazy load Vue apps
- [ ] Code splitting
- [ ] Tree shaking
- [ ] Optimize images
- [ ] Cache API responses

**Deliverable:** Performance report

**Acceptance Criteria:**
- [ ] Bundle sizes documented
- [ ] Performance baseline established
- [ ] No significant regressions
- [ ] Optimization opportunities identified

---

### Task 7: Phase 5 Documentation & GO/NO-GO
**Owner:** Developer
**Priority:** CRITICAL

**Actions:**

**7.1 Document Activity Finder 4 migration:**
```bash
touch docs/bootstrap-5-migration/modules/openy_af4_vue_app.md
```

**7.2 Create Phase 5 summary:**
```bash
touch docs/bootstrap-5-migration/phases/PHASE_5_SUMMARY.md
```

**Phase 5 Summary should include:**
- All 3 Vue apps migrated
- BootstrapVue completely removed
- Custom component library created and used
- Integration testing results
- Performance results
- Accessibility results
- Known issues
- Lessons learned
- Recommendations

**7.3 Update executive summary:**
```bash
vim docs/bootstrap-5-migration/EXECUTIVE_SUMMARY.md

# Update progress:
# - Phase 5: Complete
# - 3 Vue.js apps migrated
# - BootstrapVue removed
# - Custom component library created
```

**7.4 Create GO/NO-GO decision document:**
```bash
touch docs/bootstrap-5-migration/decisions/DECISION_PHASE_5_GO_NO_GO.md
```

**GO/NO-GO Criteria:**
- [ ] All 3 Vue apps migrated to Bootstrap 5
- [ ] BootstrapVue completely removed
- [ ] Custom component library functional
- [ ] All apps build without errors
- [ ] Integration testing passed
- [ ] Visual regression tests passed
- [ ] Accessibility tests passed
- [ ] Performance acceptable
- [ ] No critical bugs
- [ ] Documentation complete

**7.5 Document custom component library:**
```bash
# Update component library docs
vim docs/bootstrap-5-migration/reference/CUSTOM_COMPONENT_LIBRARY.md

# Add:
# - Final component list
# - Usage examples
# - API documentation
# - Migration guide
# - Maintenance guide
```

**Deliverable:** Phase 5 completion documentation

**Acceptance Criteria:**
- [ ] All documentation complete
- [ ] Phase 5 summary created
- [ ] GO/NO-GO decision made
- [ ] Executive summary updated
- [ ] Phase 6 ready to start (if approved)

---

## Testing

### Comprehensive Testing Matrix - All Vue Apps

**Functionality Testing:**
| App | Search | Filters | Results | Details | Integration | Responsive | Accessibility |
|-----|--------|---------|---------|---------|-------------|------------|---------------|
| Camp Finder | ✓ | ✓ | ✓ | ✓ | ✓ | ✓ | ✓ |
| Activity Finder | ✓ | ✓ | ✓ | ✓ | ✓ | ✓ | ✓ |
| Activity Finder 4 | ✓ | ✓ | ✓ | ✓ | ✓ | ✓ | ✓ |

**Integration Testing:**
| Integration Point | Camp Finder | Activity Finder | Activity Finder 4 |
|-------------------|-------------|-----------------|-------------------|
| Branch pages | N/A | ✓ | ✓ |
| Program pages | N/A | ✓ | ✓ |
| Camp pages | ✓ | N/A | N/A |
| Landing pages (LB) | ✓ | ✓ | ✓ |
| With LB components | ✓ | ✓ | ✓ |

**Test Environment:**
- [ ] Desktop (Chrome, Firefox, Safari, Edge)
- [ ] Tablet (iPad, Android)
- [ ] Mobile (iPhone, Android)
- [ ] Screen readers (NVDA, JAWS, VoiceOver)

---

## Deliverables

### Must Have (Critical):
- [ ] Activity Finder 4 migrated to Bootstrap 5
- [ ] All 3 Vue apps migrated
- [ ] BootstrapVue completely removed
- [ ] Custom component library used throughout
- [ ] Phase 5 integration testing complete
- [ ] All apps work together
- [ ] Visual regression tests passed
- [ ] Accessibility tests passed
- [ ] Performance acceptable
- [ ] Phase 5 documentation complete
- [ ] GO/NO-GO decision made

### Should Have (High Priority):
- [ ] Performance comparison report
- [ ] Bundle size analysis
- [ ] Integration test matrix complete
- [ ] Custom component library fully documented
- [ ] Known issues documented

### Nice to Have:
- [ ] Performance optimization recommendations
- [ ] Component library Storybook
- [ ] Video demos of all 3 apps
- [ ] Developer training materials

---

## Decision Points

### Decision: Phase 5 GO/NO-GO (END OF SPRINT)
**Criteria:**
- All 3 Vue apps functional
- BootstrapVue completely removed
- Custom component library working
- No critical bugs
- Acceptable performance
- Accessibility standards met
- Integration working

**Options:**
- GO: Proceed to Phase 6 (Final testing & rollout)
- NO-GO: Additional sprint for bug fixes

**Decision Maker:** Project Lead + Stakeholders
**Documentation:** `decisions/DECISION_PHASE_5_GO_NO_GO.md`

---

## Risks

### Risk: Activity Finder 4 Issues (MEDIUM)
**Impact:** HIGH - Most used Activity Finder version
**Mitigation:**
- Use proven patterns from Sprints 19-20
- Allocate extra time for testing
- Test extensively on real pages
- Have rollback plan

### Risk: Vue App Conflicts (MEDIUM)
**Impact:** HIGH - Apps may not work together
**Mitigation:**
- Test all 3 apps together early
- Verify no JavaScript conflicts
- Verify no style conflicts
- Test on realistic pages

### Risk: Performance Regression (LOW)
**Impact:** MEDIUM - Apps may be slower
**Mitigation:**
- Profile performance early
- Compare to Bootstrap 4 baseline
- Optimize if needed
- Document acceptable trade-offs

---

## Notes

### Important:
- Final Phase 5 sprint - most critical
- Activity Finder 4 most used - must work perfectly
- All 3 Vue apps must work together
- GO/NO-GO decision crucial
- Custom component library must be maintainable

### Tips:
- Use Sprints 19-20 patterns religiously
- Test all 3 apps together continuously
- Document everything for future maintenance
- Save buffer time for unexpected issues
- Create comprehensive test content

### Phase 5 Success Metrics:
- 3 Vue.js apps migrated ✓
- BootstrapVue removed ✓
- Bootstrap 5.3.3 throughout ✓
- Custom component library ✓
- All tests passing ✓
- Performance acceptable ✓
- Accessibility maintained ✓

### What's Next (Phase 6):
- Final comprehensive testing
- Performance optimization
- Browser compatibility testing
- Production deployment preparation
- Documentation finalization
- Training materials
- Rollout plan

---

## Sprint Review Checklist

At end of sprint, verify:
- [ ] Activity Finder 4 migrated
- [ ] All 3 Vue apps working
- [ ] Integration testing complete
- [ ] Visual regression tests passed
- [ ] Accessibility tests passed
- [ ] Performance acceptable
- [ ] Documentation complete
- [ ] GO/NO-GO decision made
- [ ] Phase 6 ready (if approved)

---

## Navigation

- **Previous:** [Sprint 20 - Activity Finder](SPRINT_20_AF_Activity_Finder.md)
- **Next:** Sprint 22 - Final Testing (Phase 6)
- **Phase:** [Phase 5 - Activity Finder](../phases/PHASE_5_ACTIVITY_FINDER.md)
- **Overview:** [Executive Summary](../EXECUTIVE_SUMMARY.md)

---

**Sprint Status:** ⬜ Not Started
**Last Updated:** 2025-10-17
