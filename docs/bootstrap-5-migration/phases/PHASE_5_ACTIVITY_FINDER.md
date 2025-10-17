# Phase 5: Activity Finder Vue.js Applications

**Duration:** 8 weeks (Sprints 18-21)
**Status:** Not Started
**Goal:** Migrate 3 Vue.js Activity Finder applications to Bootstrap 5

---

## Overview

Phase 5 focuses on migrating the Vue.js Activity Finder applications from Bootstrap 4 (via BootstrapVue 2) to Bootstrap 5. This is the most technically complex phase because:

1. **BootstrapVue 2 is NOT compatible with Bootstrap 5**
2. **BootstrapVue 3 (BS5 version) is still in alpha and not production-ready**
3. **Must remove BootstrapVue dependency entirely and create custom component library**

**Critical Challenge:** These are Vue.js 2 applications using BootstrapVue 2 components extensively. We cannot simply update Bootstrap - we must refactor the applications.

**Key Strategy:** Remove BootstrapVue dependency, create lightweight Bootstrap 5 component library, migrate apps one at a time.

---

## Sprints in This Phase

### Sprint 18: Camp Finder Isolation + Component Library
**Focus:** Preparation and component library
- Isolate Camp Finder with scoped Bootstrap 4 CSS (same as Activity Finder in Phase 1)
- Audit BootstrapVue component usage across all 3 apps
- Create Bootstrap 5 Vue component library (b-card, b-button, b-modal, b-form, etc.)
- Test component library in isolation

**See:** [sprints/SPRINT_18_CampFinder_Isolation_Components.md](../sprints/SPRINT_18_CampFinder_Isolation_Components.md)

### Sprint 19: Activity Finder 4 Migration
**Modules (1):** Latest Activity Finder
- openy_activity_finder (Activity Finder 4)
- Replace BootstrapVue with custom component library
- Update to Bootstrap 5
- Test thoroughly

**See:** [sprints/SPRINT_19_ActivityFinder4.md](../sprints/SPRINT_19_ActivityFinder4.md)

### Sprint 20: Activity Finder (Legacy) Migration
**Modules (1):** Original Activity Finder
- openy_af (Activity Finder legacy)
- Replace BootstrapVue with custom component library
- Update to Bootstrap 5
- Test thoroughly
- Verify both AF versions work

**See:** [sprints/SPRINT_20_ActivityFinder_Legacy.md](../sprints/SPRINT_20_ActivityFinder_Legacy.md)

### Sprint 21: Camp Finder Migration + Testing
**Modules (1):** Camp Finder
- openy_prgf_camp_finder (Camp Finder)
- Replace BootstrapVue with custom component library
- Update to Bootstrap 5
- Integration testing all 3 apps
- Phase 5 completion

**See:** [sprints/SPRINT_21_CampFinder_Testing.md](../sprints/SPRINT_21_CampFinder_Testing.md)

---

## Key Deliverables

### Sprint 18 Deliverables
- [ ] Camp Finder isolated with scoped Bootstrap 4 CSS
- [ ] BootstrapVue component audit complete
- [ ] Custom Bootstrap 5 Vue component library created
- [ ] Component library tested in isolation
- [ ] Migration plan finalized

### Sprint 19 Deliverables
- [ ] Activity Finder 4 migrated to Bootstrap 5
- [ ] BootstrapVue removed from Activity Finder 4
- [ ] Custom components integrated
- [ ] Activity Finder 4 fully functional
- [ ] Activity Finder 4 isolation removed

### Sprint 20 Deliverables
- [ ] Activity Finder (legacy) migrated to Bootstrap 5
- [ ] BootstrapVue removed from Activity Finder
- [ ] Custom components integrated
- [ ] Activity Finder fully functional
- [ ] Activity Finder isolation removed
- [ ] Both AF versions work together

### Sprint 21 Deliverables
- [ ] Camp Finder migrated to Bootstrap 5
- [ ] BootstrapVue removed from Camp Finder
- [ ] Custom components integrated
- [ ] Camp Finder fully functional
- [ ] Camp Finder isolation removed
- [ ] All 3 Vue apps tested together
- [ ] Visual regression tests passed
- [ ] Performance tests passed
- [ ] Phase 5 documentation complete
- [ ] GO/NO-GO decision for Phase 6

---

## Components in This Phase

### Vue.js Applications (3 modules)

**Activity Finder Suite:**

1. **openy_activity_finder** (Activity Finder 4)
   - Path: `docroot/modules/contrib/openy_activity_finder`
   - Current: Vue.js 2 + BootstrapVue 2 + Bootstrap 4.4.1
   - Target: Vue.js 2 + Custom Components + Bootstrap 5.3.3
   - Priority: HIGH (newer version, more usage)
   - Isolated in Phase 1: ✓

2. **openy_af** (Activity Finder Legacy)
   - Path: `docroot/modules/contrib/openy_af`
   - Current: Vue.js 2 + BootstrapVue 2 + Bootstrap 4.4.1
   - Target: Vue.js 2 + Custom Components + Bootstrap 5.3.3
   - Priority: MEDIUM (older version, still used)
   - Isolated in Phase 1: ✓

3. **openy_prgf_camp_finder** (Camp Finder)
   - Path: `docroot/modules/contrib/openy_prgf_camp_finder`
   - Current: Vue.js 2 + BootstrapVue 2 + Bootstrap 4.4.1
   - Target: Vue.js 2 + Custom Components + Bootstrap 5.3.3
   - Priority: MEDIUM (seasonal usage)
   - Isolated in Phase 5 Sprint 18: ⬜

---

## Success Criteria

### Technical
- [ ] All 3 Vue.js apps migrated to Bootstrap 5.3.3
- [ ] BootstrapVue completely removed
- [ ] Custom Bootstrap 5 component library working
- [ ] Apps build without errors (npm run build)
- [ ] No JavaScript console errors
- [ ] No Vue warnings in console
- [ ] Webpack bundles optimized

### Functionality
- [ ] Activity Finder 4 search works
- [ ] Activity Finder 4 filters work
- [ ] Activity Finder 4 results display correctly
- [ ] Activity Finder 4 responsive on all devices
- [ ] Activity Finder legacy search works
- [ ] Activity Finder legacy filters work
- [ ] Activity Finder legacy results display correctly
- [ ] Activity Finder legacy responsive on all devices
- [ ] Camp Finder search works
- [ ] Camp Finder filters work
- [ ] Camp Finder results display correctly
- [ ] Camp Finder responsive on all devices

### Quality
- [ ] Visual regression tests passed (all 3 apps)
- [ ] Accessibility maintained (WCAG 2.2 AA)
- [ ] Keyboard navigation works
- [ ] Screen reader compatible
- [ ] Touch/mobile interactions work
- [ ] Cross-browser compatibility verified

### Performance
- [ ] Bundle size not significantly increased
- [ ] Load time maintained or improved
- [ ] Search performance maintained
- [ ] No memory leaks
- [ ] Vue reactivity working efficiently

### Process
- [ ] Component library documented
- [ ] Vue component migration patterns documented
- [ ] Build process documented
- [ ] Known issues documented

---

## Risks & Mitigation

### Risk 1: BootstrapVue Removal Breaks Apps (CRITICAL)
**Impact:** CRITICAL - Apps may not work at all
**Probability:** HIGH
**Affected Modules:** All 3 Vue apps
**Mitigation:**
- Create comprehensive BootstrapVue component audit first
- Build custom component library before migrating apps
- Test custom components in isolation
- Migrate apps one at a time (not all at once)
- Keep isolated Bootstrap 4 versions as backup
- Allocate extra time for debugging and refactoring

**BootstrapVue Components Used (estimate):**
- b-card, b-card-body, b-card-title
- b-button, b-button-group
- b-form, b-form-input, b-form-select, b-form-checkbox, b-form-radio
- b-modal
- b-dropdown, b-dropdown-item
- b-collapse
- b-badge
- b-spinner
- b-alert
- b-table (maybe)
- b-pagination (maybe)

All must be replaced with custom Vue components or vanilla Bootstrap 5.

### Risk 2: Custom Component Library Incomplete (HIGH)
**Impact:** HIGH - Missing components will block migration
**Probability:** MEDIUM
**Mitigation:**
- Complete component audit before starting library (Sprint 18)
- Build all needed components before migrating first app
- Test each component thoroughly
- Create component documentation
- Have fallback plan (vanilla Bootstrap 5 + manual DOM manipulation)

**Component Library Requirements:**
- Must match BootstrapVue API where possible
- Must work with Vue 2
- Must use Bootstrap 5 classes
- Must be accessible
- Must be performant
- Must be maintainable

### Risk 3: Vue 2 Compatibility Issues (MEDIUM)
**Impact:** MEDIUM - Components may not work with Vue 2
**Probability:** LOW
**Mitigation:**
- Keep Vue 2 as is (don't upgrade to Vue 3)
- Test custom components with Vue 2 extensively
- Follow Vue 2 composition patterns
- Avoid Vue 3-specific features
- Document Vue 2 compatibility requirements

**Note:** Vue 2 reached EOL in December 2023, but upgrading to Vue 3 is out of scope for this migration. That would be a separate project.

### Risk 4: Build System Issues (MEDIUM)
**Impact:** MEDIUM - Apps may not build
**Probability:** MEDIUM
**Affected Modules:** All 3 Vue apps
**Mitigation:**
- Update webpack configurations carefully
- Test build process after each change
- Document webpack configuration changes
- Keep working build configurations as backup
- Update npm dependencies incrementally

**Build System Changes:**
- Update Bootstrap from 4.4.1 to 5.3.3
- Remove BootstrapVue from package.json
- Update webpack loaders if needed
- Update babel configuration if needed
- Test in both dev and production modes

### Risk 5: Activity Finder Integration with Drupal (MEDIUM)
**Impact:** HIGH - Finders may not work on Drupal pages
**Probability:** LOW
**Mitigation:**
- Test each app embedded in Drupal pages
- Test on branch pages (y_branch)
- Test on program pages (y_program)
- Test on camp pages (y_camp)
- Verify Drupal-to-Vue data passing still works
- Test with realistic content

**Integration Points:**
- Drupal passes data to Vue via data attributes
- Vue apps render in Drupal template regions
- Apps use Drupal's API for data
- Apps respect Drupal's theming

### Risk 6: Performance Regression (LOW)
**Impact:** MEDIUM - Apps may be slower
**Probability:** LOW
**Mitigation:**
- Profile Vue apps before migration (baseline)
- Profile after migration
- Optimize webpack bundles
- Use Vue's production build
- Lazy load components if needed
- Test on mobile devices

---

## Testing Strategy

### Sprint 18 Testing
**Component Library Only:**
- Unit test each custom component
- Test component props
- Test component events
- Test component slots
- Test component accessibility
- Test component responsiveness

### Sprint 19 Testing
**Activity Finder 4:**
- Functional testing (search, filters, results)
- Visual regression testing (BackstopJS)
- Accessibility testing (Pa11y + manual)
- Performance testing (Chrome DevTools)
- Cross-browser testing
- Mobile/touch testing
- Integration testing with Drupal

### Sprint 20 Testing
**Activity Finder Legacy:**
- Same as Sprint 19
- Plus: Test both AF versions on same site
- Verify no conflicts between AF4 and AF legacy

### Sprint 21 Testing
**Camp Finder + Integration:**
- Same as Sprints 19-20 for Camp Finder
- Plus: Integration testing all 3 apps together
- Test all 3 apps on same site
- Test all 3 apps on same page (if applicable)
- Verify no conflicts
- Full regression testing

### Test Scenarios for Each App

**Search Functionality:**
- [ ] Search with no filters
- [ ] Search with location filter
- [ ] Search with category filter
- [ ] Search with multiple filters
- [ ] Search with date range (if applicable)
- [ ] Search with no results
- [ ] Search with many results
- [ ] Search with pagination

**Filters:**
- [ ] Apply single filter
- [ ] Apply multiple filters
- [ ] Clear filters
- [ ] Filter combinations
- [ ] Filter persistence (URL params)

**Results Display:**
- [ ] Results list view
- [ ] Results map view (if applicable)
- [ ] Result detail modal/popup
- [ ] Result registration link
- [ ] Result location display
- [ ] Result date/time display
- [ ] No results message

**Responsive:**
- [ ] Mobile view (< 576px)
- [ ] Tablet view (576px - 768px)
- [ ] Desktop view (> 768px)
- [ ] Touch interactions
- [ ] Mobile keyboard

**Accessibility:**
- [ ] Keyboard navigation
- [ ] Screen reader announcements
- [ ] Focus management
- [ ] ARIA labels
- [ ] Color contrast
- [ ] Error messages

**Performance:**
- [ ] Initial load time
- [ ] Search response time
- [ ] Filter response time
- [ ] Memory usage
- [ ] Bundle size

---

## Resources

### Team
- 1 Full-time Frontend Developer (Vue.js experience required)
- Optional: Vue.js Contractor (highly recommended)
- Part-time QA for testing support

### Tools
- Node.js 16+
- Vue.js 2 (don't upgrade)
- Webpack 5
- Bootstrap 5.3.3
- BackstopJS (visual regression)
- Pa11y (accessibility)
- Chrome DevTools (performance profiling)
- Vue DevTools (debugging)

### Reference Materials
- BootstrapVue 2 documentation (for component audit)
- Bootstrap 5 documentation (for custom components)
- Vue 2 documentation
- Webpack documentation
- Activity Finder isolation documentation (from Phase 1)

### Skills Required
- **Critical:** Vue.js 2 experience
- **Critical:** Bootstrap 5 knowledge
- **Important:** BootstrapVue 2 knowledge
- **Important:** Webpack configuration
- **Important:** Component library design
- **Nice to have:** Vue.js testing experience

### Time
- Sprint 18: 2 weeks (isolation + component library)
- Sprint 19: 2 weeks (Activity Finder 4)
- Sprint 20: 2 weeks (Activity Finder legacy)
- Sprint 21: 2 weeks (Camp Finder + testing)
- **Total: 8 weeks**

**Note:** This is the most technically complex phase. If timeline slips, consider:
- Adding contractor for parallel work
- Extending to 10 weeks (add 1 week to Sprints 19-20)
- Simplifying component library (use vanilla Bootstrap more)

---

## Dependencies

### Before Phase 5 Can Start:
- [x] Phase 1 complete (theme migrated)
- [x] Phase 2 complete (WS modules migrated)
- [x] Phase 3 complete (LB modules migrated)
- [x] Phase 4 complete (content types migrated)
- [x] Activity Finder isolated (from Phase 1)
- [ ] GO/NO-GO decision from Phase 4

### Before Phase 6 Can Start:
- [ ] All 3 Vue apps migrated
- [ ] BootstrapVue completely removed
- [ ] Custom component library documented
- [ ] All apps functional
- [ ] Integration testing passed
- [ ] Performance testing passed
- [ ] GO/NO-GO decision approved

### External Dependencies:
- Vue.js 2 (keep as is - don't upgrade)
- Bootstrap 5.3.3
- Drupal's API for data (don't change)

---

## Decision Points

### End of Sprint 18:
- [ ] Is component library complete enough?
- [ ] Are custom components working well?
- [ ] Is Camp Finder isolated successfully?
- [ ] Ready to start migrating apps?
- [ ] Should we bring in contractor?

### End of Sprint 19:
- [ ] Is Activity Finder 4 fully functional?
- [ ] Is migration approach working?
- [ ] Any major blockers discovered?
- [ ] Should we adjust timeline?

### End of Sprint 20:
- [ ] Are both Activity Finder versions working?
- [ ] Any conflicts between versions?
- [ ] Ready for Camp Finder migration?

### End of Sprint 21 (End of Phase 5):
- [ ] **GO/NO-GO for Phase 6**
- [ ] Are all Vue apps production-ready?
- [ ] Is performance acceptable?
- [ ] Are there any critical bugs?
- [ ] Ready for comprehensive testing and rollout?

---

## Notes

### Important Considerations:

1. **BootstrapVue is NOT Compatible:** Cannot use BootstrapVue 2 with Bootstrap 5
2. **BootstrapVue 3 is Not Ready:** Still in alpha, not production-ready
3. **Component Library is Critical:** Must build custom components before migrating
4. **Vue 2 is EOL:** But upgrading to Vue 3 is separate project
5. **Most Complex Phase:** Requires Vue.js expertise

### Why We Can't Use BootstrapVue 3:

- BootstrapVue 3 (for Bootstrap 5) is in alpha stage
- Not recommended for production
- Requires Vue 3 (we're on Vue 2)
- Upgrading to Vue 3 is out of scope (major refactor)
- Safer to build custom component library

### Custom Component Library Strategy:

**Option A: Thin Wrapper Components (Recommended)**
- Create Vue components that wrap Bootstrap 5 HTML
- Use Bootstrap 5 classes directly
- Add Vue reactivity where needed
- Minimal JavaScript

**Example:**
```vue
<template>
  <div class="card">
    <div class="card-body">
      <slot></slot>
    </div>
  </div>
</template>
```

**Option B: Full JavaScript Components**
- Recreate Bootstrap 5 JavaScript components in Vue
- More work, more control
- Use for complex components (modal, dropdown)

**Option C: Hybrid**
- Use Option A for simple components (card, button)
- Use Option B for complex components (modal)
- Recommended approach

### Migration Order Rationale:

**Sprint 18:** Preparation and component library first
**Sprint 19:** Activity Finder 4 first (most used, newest code)
**Sprint 20:** Activity Finder legacy second (older code, lessons learned)
**Sprint 21:** Camp Finder last (seasonal use, buffer sprint)

### Isolation vs Migration:

**Phase 1:** Activity Finder & Activity Finder 4 isolated with scoped BS4 CSS
**Sprint 18:** Camp Finder isolated with scoped BS4 CSS
**Sprint 19:** Activity Finder 4 migrated, isolation removed
**Sprint 20:** Activity Finder legacy migrated, isolation removed
**Sprint 21:** Camp Finder migrated, isolation removed

All 3 apps will use Bootstrap 5 after Phase 5.

---

## Next Phase

After Phase 5 is complete:
- **Phase 6:** Testing & Rollout (Sprints 22-24)

See: [PHASE_6_TESTING_ROLLOUT.md](PHASE_6_TESTING_ROLLOUT.md)

---

## Related Documents

- [../EXECUTIVE_SUMMARY.md](../EXECUTIVE_SUMMARY.md)
- [../MODULE_INVENTORY.md](../MODULE_INVENTORY.md)
- [PHASE_1_PREPARATION.md](PHASE_1_PREPARATION.md)
- [PHASE_4_CONTENT_TYPES.md](PHASE_4_CONTENT_TYPES.md)
- [PHASE_6_TESTING_ROLLOUT.md](PHASE_6_TESTING_ROLLOUT.md)
- [../sprints/SPRINT_18_CampFinder_Isolation_Components.md](../sprints/SPRINT_18_CampFinder_Isolation_Components.md)
- [../sprints/SPRINT_19_ActivityFinder4.md](../sprints/SPRINT_19_ActivityFinder4.md)
- [../sprints/SPRINT_20_ActivityFinder_Legacy.md](../sprints/SPRINT_20_ActivityFinder_Legacy.md)
- [../sprints/SPRINT_21_CampFinder_Testing.md](../sprints/SPRINT_21_CampFinder_Testing.md)

---

**Phase Status:** ⬜ Not Started
**Last Updated:** 2025-10-17
