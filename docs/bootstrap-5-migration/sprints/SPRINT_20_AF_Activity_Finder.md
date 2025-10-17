# Sprint 20: Activity Finder (Legacy) Migration

**Phase:** [Phase 5 - Activity Finder](../phases/PHASE_5_ACTIVITY_FINDER.md)
**Resources:** 1 Frontend Developer (Vue.js experience required)
**Status:** Not Started

---

## Sprint Goal

Migrate Activity Finder legacy (openy_af_vue_app) from BootstrapVue 2 + Bootstrap 4 to custom components + Bootstrap 5. Remove isolation, verify both Activity Finder versions work together on same site.

---

## Module in This Sprint

**openy_af_vue_app** - Activity Finder (Legacy) Vue.js Application
- Path: `docroot/modules/contrib/yusaopeny_activity_finder/openy_af_vue_app`
- Current: Vue.js 2 + BootstrapVue 2 + Bootstrap 4.4.1 (isolated)
- Target: Vue.js 2 + Custom Components + Bootstrap 5.3.3
- Isolation: Remove after migration complete
- Note: Older Activity Finder version, still used by some sites

---

## Tasks

### Task 1: Prepare Activity Finder for Migration
**Owner:** Developer
**Priority:** CRITICAL

**Actions:**
```bash
cd docroot/modules/contrib/yusaopeny_activity_finder/openy_af_vue_app

# Review structure
ls -la
cat package.json

# Compare with Camp Finder (Sprint 19)
# Use same migration patterns
```

**Document:**
- Current functionality (activity search, filters, results, registration)
- Differences from Camp Finder
- Component usage patterns
- Integration points with Drupal

**Deliverable:** Migration plan based on Sprint 19 patterns

**Acceptance Criteria:**
- [ ] Current functionality documented
- [ ] Differences from Camp Finder identified
- [ ] Migration approach defined using Sprint 19 lessons

---

### Task 2: Update Dependencies (Same as Sprint 19)
**Owner:** Developer
**Priority:** CRITICAL

**Actions:**
```bash
# Remove BootstrapVue
npm uninstall bootstrap-vue

# Update Bootstrap
npm uninstall bootstrap@4.4.1
npm install bootstrap@5.3.3 @popperjs/core

# Link custom component library
# Use same library from Sprint 18/19
```

**Deliverable:** Updated dependencies

**Acceptance Criteria:**
- [ ] BootstrapVue removed
- [ ] Bootstrap 5.3.3 installed
- [ ] Custom components accessible

---

### Task 3: Remove Bootstrap 4 Isolation
**Owner:** Developer
**Priority:** HIGH

**Actions:**
- Remove webpack CSS scoping (same as Sprint 19)
- Update SCSS to Bootstrap 5
- Remove template wrapper
- Update data-bs-* attributes

**Deliverable:** Isolation removed

**Acceptance Criteria:**
- [ ] Webpack scoping removed
- [ ] SCSS updated
- [ ] Build succeeds

---

### Task 4: Replace BootstrapVue Components
**Owner:** Developer
**Priority:** CRITICAL

**Actions:**

**Use patterns from Sprint 19:**
- Replace all b-* components with bs-* or HTML
- Update imports
- Update component usage

**Key Components to Replace:**

**4.1 SearchForm.vue:**
```vue
<!-- Replace b-form, b-form-input, b-button -->
<form @submit.prevent="onSubmit">
  <div class="mb-3">
    <label class="form-label">Search Activities</label>
    <bs-form-input v-model="searchTerm" placeholder="Enter keywords..." />
  </div>
  <bs-button type="submit" variant="primary">Search</bs-button>
</form>
```

**4.2 FilterPanel.vue:**
```vue
<!-- Replace b-form-select for multiple filters -->
<div class="row g-3">
  <div class="col-md-3">
    <label class="form-label">Location</label>
    <bs-form-select v-model="filters.location">
      <option value="">All Locations</option>
      <!-- options -->
    </bs-form-select>
  </div>
  <!-- Repeat for other filters: category, age, time, day -->
</div>
```

**4.3 ResultsList.vue:**
```vue
<!-- Replace b-card for activity cards -->
<div class="row">
  <div v-for="activity in activities" :key="activity.id" class="col-md-4 mb-4">
    <bs-card>
      <bs-card-body>
        <bs-card-title>{{ activity.name }}</bs-card-title>
        <p>{{ activity.description }}</p>
        <bs-button @click="showDetails(activity)" variant="primary">
          View Details
        </bs-button>
      </bs-card-body>
    </bs-card>
  </div>
</div>
```

**4.4 ActivityDetailModal.vue:**
```vue
<!-- Replace b-modal -->
<bs-modal v-model="showModal" :title="activity.name" size="lg">
  <div class="activity-details">
    <!-- Activity details content -->
  </div>
  <template #footer>
    <bs-button variant="secondary" @click="closeModal">Close</bs-button>
    <bs-button variant="primary" :href="activity.registrationUrl">
      Register
    </bs-button>
  </template>
</bs-modal>
```

**4.5 MapView.vue (if present):**
- Replace BootstrapVue components
- Update map integration
- Maintain map functionality

**Deliverable:** All BootstrapVue components replaced

**Acceptance Criteria:**
- [ ] All b-* components replaced
- [ ] All imports updated
- [ ] App builds successfully
- [ ] No BootstrapVue references

---

### Task 5: Update Styling and Classes
**Owner:** Developer
**Priority:** HIGH

**Actions:**
- Update Bootstrap 4 classes to Bootstrap 5
- Update utility classes (ml/mr → ms/me)
- Update form classes
- Update grid gutters
- Update data-bs-* attributes

**Same patterns as Sprint 19**

**Deliverable:** Updated styles

**Acceptance Criteria:**
- [ ] All Bootstrap classes updated
- [ ] Responsive design maintained
- [ ] Visual appearance correct

---

### Task 6: Build and Test Activity Finder
**Owner:** Developer
**Priority:** CRITICAL

**Actions:**

**6.1 Build:**
```bash
npm run dev
npm run build
```

**6.2 Test functionality:**
- [ ] Activity search works
- [ ] Filters work (location, category, age, time, day)
- [ ] Results display correctly
- [ ] Activity detail modal works
- [ ] Registration links work
- [ ] Map view works (if present)

**6.3 Test responsive:**
- [ ] Desktop, tablet, mobile views
- [ ] Touch interactions

**6.4 Test on Drupal pages:**
- [ ] Activity Finder on branch pages
- [ ] Activity Finder on program pages
- [ ] Data loads from Drupal
- [ ] No style conflicts

**Deliverable:** Test report

**Acceptance Criteria:**
- [ ] All functionality works
- [ ] Responsive design works
- [ ] Integration with Drupal works
- [ ] No console errors

---

### Task 7: Test Both Activity Finder Versions Together
**Owner:** Developer
**Priority:** CRITICAL

**Actions:**

**7.1 Test on same site:**
- [ ] Activity Finder (legacy) on one page
- [ ] Activity Finder 4 on another page
- [ ] Both load without conflicts
- [ ] No JavaScript errors
- [ ] No style conflicts

**7.2 Test switching between versions:**
- [ ] Navigate from page with AF legacy to page with AF4
- [ ] Navigate back
- [ ] Both work correctly

**7.3 Test on same page (if applicable):**
- [ ] Both Activity Finders on same page (edge case)
- [ ] Both work independently
- [ ] No conflicts

**7.4 Verify isolation removed from both:**
- [ ] Activity Finder (legacy) uses Bootstrap 5
- [ ] Activity Finder 4 uses Bootstrap 5 (will migrate in Sprint 21)
- [ ] No Bootstrap 4 CSS remaining

**Deliverable:** Compatibility test report

**Acceptance Criteria:**
- [ ] Both Activity Finder versions work on same site
- [ ] No conflicts between versions
- [ ] Both use Bootstrap 5 (after Sprint 21)
- [ ] Site navigation works with both

---

### Task 8: Visual Regression Testing
**Owner:** Developer
**Priority:** HIGH

**Actions:**
```json
{
  "scenarios": [
    {
      "label": "Activity Finder Legacy - Initial",
      "url": "http://yusaopeny.docksal.site/activity-finder"
    },
    {
      "label": "Activity Finder Legacy - Search",
      "url": "http://yusaopeny.docksal.site/activity-finder?search=yoga"
    },
    {
      "label": "Activity Finder Legacy - Filters",
      "url": "http://yusaopeny.docksal.site/activity-finder?location=1&category=2"
    }
  ]
}
```

**Run tests and review differences**

**Deliverable:** Visual regression report

**Acceptance Criteria:**
- [ ] Visual tests passed
- [ ] Differences documented

---

### Task 9: Accessibility Testing
**Owner:** Developer
**Priority:** HIGH

**Actions:**
- Run Pa11y tests
- Manual keyboard navigation testing
- Screen reader testing
- ARIA attributes verification
- Color contrast testing

**Same patterns as Sprint 19**

**Deliverable:** Accessibility report

**Acceptance Criteria:**
- [ ] WCAG 2.2 AA compliance
- [ ] Keyboard navigation works
- [ ] Screen reader compatible

---

### Task 10: Documentation
**Owner:** Developer
**Priority:** MEDIUM

**Actions:**
```bash
touch docs/bootstrap-5-migration/modules/openy_af_vue_app.md
```

**Document:**
- Migration process
- Differences from Camp Finder migration
- Known issues
- Lessons learned for Sprint 21

**Update migration log**

**Deliverable:** Complete documentation

**Acceptance Criteria:**
- [ ] Module documentation complete
- [ ] Migration log updated

---

## Testing

### Activity Finder Specific Tests

**Search:**
- [ ] Keyword search
- [ ] Empty search
- [ ] No results

**Filters:**
- [ ] Location filter
- [ ] Category filter
- [ ] Age filter
- [ ] Time of day filter
- [ ] Day of week filter
- [ ] Multiple filters
- [ ] Clear filters

**Results:**
- [ ] List view
- [ ] Map view (if present)
- [ ] Activity cards
- [ ] Registration links

**Details:**
- [ ] Modal opens
- [ ] Content displays
- [ ] Registration works

**Integration:**
- [ ] On branch pages
- [ ] On program pages
- [ ] Data from Drupal

**Compatibility:**
- [ ] Works with Activity Finder 4 on same site

---

## Deliverables

### Must Have:
- [ ] Activity Finder migrated to Bootstrap 5
- [ ] BootstrapVue removed
- [ ] Custom components integrated
- [ ] Isolation removed
- [ ] All functionality working
- [ ] Both AF versions work together
- [ ] Visual regression tests passed
- [ ] Accessibility tests passed
- [ ] Documentation complete

### Should Have:
- [ ] Compatibility test report
- [ ] Migration patterns refined
- [ ] Known issues documented

---

## Risks

### Risk: Conflicts with Activity Finder 4 (MEDIUM)
**Impact:** HIGH - Both versions may not work together
**Mitigation:**
- Test both versions together extensively
- Verify no JavaScript conflicts
- Verify no style conflicts
- Test navigation between pages

### Risk: Legacy Code Issues (MEDIUM)
**Impact:** MEDIUM - Older code may be harder to migrate
**Mitigation:**
- Use patterns from Sprint 19
- Allocate extra time for debugging
- Document workarounds
- Consider refactoring if needed

---

## Notes

### Important:
- Second Vue app migration - use Sprint 19 patterns
- Must work with Activity Finder 4 on same site
- Older codebase may have unique challenges
- Test compatibility thoroughly

### Tips:
- Follow Sprint 19 migration process closely
- Document any differences from Sprint 19
- Test both AF versions together early
- Keep Sprint 19 migration docs handy

### Phase 5 Context:
- Sprint 18: Preparation (complete)
- Sprint 19: Camp Finder (complete)
- Sprint 20: Activity Finder (this sprint)
- Sprint 21: Activity Finder 4 + testing

---

## Sprint Review Checklist

- [ ] Activity Finder migrated
- [ ] All functionality works
- [ ] Both AF versions work together
- [ ] Testing complete
- [ ] Documentation complete
- [ ] Sprint 21 ready

---

## Navigation

- **Previous:** [Sprint 19 - Camp Finder](SPRINT_19_AF_Camp_Finder.md)
- **Next:** [Sprint 21 - Activity Finder 4](SPRINT_21_AF_Activity_Finder4.md)
- **Phase:** [Phase 5 - Activity Finder](../phases/PHASE_5_ACTIVITY_FINDER.md)
- **Overview:** [Executive Summary](../EXECUTIVE_SUMMARY.md)

---

**Sprint Status:** ⬜ Not Started
**Last Updated:** 2025-10-17
