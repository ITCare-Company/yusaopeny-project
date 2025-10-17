# Sprint 3: Theme Part 2 + Activity Finder Isolation

**Phase:** [Phase 1 - Preparation](../phases/PHASE_1_PREPARATION.md)
**Resources:** 1 Developer
**Status:** Not Started

---

## Sprint Goal

Complete openy_carnation theme migration with component templates and CSS updates, and isolate Activity Finder with scoped CSS to prevent Bootstrap conflicts.

---

## Tasks

### Task 1: Update Component Templates - Data Attributes
**Owner:** Developer
**Priority:** CRITICAL

**Actions:**
```bash
cd docroot/themes/contrib/openy_carnation/templates
```

**Find and Replace Across All Templates:**

```bash
# Find all templates with Bootstrap data attributes
grep -r "data-toggle" templates/
grep -r "data-target" templates/
grep -r "data-dismiss" templates/
grep -r "data-slide" templates/
```

**Bootstrap 4 → Bootstrap 5 Attribute Changes:**

```twig
{# Bootstrap 4 #}
<button data-toggle="modal" data-target="#myModal">

{# Bootstrap 5 #}
<button data-bs-toggle="modal" data-bs-target="#myModal">

{# Bootstrap 4 #}
<button data-dismiss="modal">

{# Bootstrap 5 #}
<button data-bs-dismiss="modal">

{# Bootstrap 4 #}
<a data-toggle="collapse" data-target="#collapseExample">

{# Bootstrap 5 #}
<a data-bs-toggle="collapse" data-bs-target="#collapseExample">

{# Bootstrap 4 #}
<button data-slide="next">

{# Bootstrap 5 #}
<button data-bs-slide="next">
```

**Acceptance Criteria:**
- [ ] All `data-toggle` → `data-bs-toggle`
- [ ] All `data-target` → `data-bs-target`
- [ ] All `data-dismiss` → `data-bs-dismiss`
- [ ] All `data-slide` → `data-bs-slide`
- [ ] All `data-ride` → `data-bs-ride`
- [ ] Search confirms no old attributes remain

---

### Task 2: Update Component Templates - CSS Classes
**Owner:** Developer
**Priority:** HIGH

**Actions:**
```bash
cd docroot/themes/contrib/openy_carnation/templates
```

**Bootstrap 4 → Bootstrap 5 Class Changes:**

**Spacing Classes:**
```twig
{# Bootstrap 4 - NO CHANGE (these stay the same) #}
<div class="ml-3 mr-3 mt-2 mb-2 pl-4 pr-4 pt-3 pb-3">

{# Bootstrap 5 - Use new naming (update if standardizing) #}
<div class="ms-3 me-3 mt-2 mb-2 ps-4 pe-4 pt-3 pb-3">

{# RECOMMENDATION: Leave as-is initially, BS5 supports both #}
{# Update to new naming in Phase 3 optimization #}
```

**Form Classes:**
```twig
{# Bootstrap 4 #}
<div class="form-group">
  <label>Email</label>
  <input type="email" class="form-control">
</div>

{# Bootstrap 5 #}
<div class="mb-3">
  <label class="form-label">Email</label>
  <input type="email" class="form-control">
</div>
```

**Utility Classes:**
```twig
{# Bootstrap 4 #}
<div class="float-left">
<div class="float-right">

{# Bootstrap 5 #}
<div class="float-start">
<div class="float-end">

{# Bootstrap 4 #}
<div class="text-left">
<div class="text-right">

{# Bootstrap 5 #}
<div class="text-start">
<div class="text-end">
```

**Find and Replace:**
```bash
# Find all float/text direction classes
grep -r "float-left\|float-right" templates/
grep -r "text-left\|text-right" templates/

# Find form-group
grep -r "form-group" templates/
```

**Acceptance Criteria:**
- [ ] All `float-left` → `float-start`
- [ ] All `float-right` → `float-end`
- [ ] All `text-left` → `text-start`
- [ ] All `text-right` → `text-end`
- [ ] All `form-group` removed (use `mb-3` or similar)
- [ ] Labels updated with `form-label` class

---

### Task 3: Update Component SCSS Files
**Owner:** Developer
**Priority:** HIGH

**Actions:**
```bash
cd docroot/themes/contrib/openy_carnation/assets/scss/components
```

**Update Each Component SCSS:**

**1. Header (`_header.scss`):**
- Update navbar classes if using Bootstrap navbar
- Check offcanvas implementation (new in BS5)
- Update dropdown styles

**2. Navigation (`_navigation.scss`):**
- Update nav classes
- Check tabs styling
- Check pills styling

**3. Cards (`_cards.scss`):**
- Verify card classes (mostly unchanged)
- Check card image caps
- Check card decks (removed in BS5 - use grid)

**4. Forms (`_forms.scss`):**
- Update form-group styles (now deprecated)
- Update input-group styles
- Update validation styles
- Check floating labels (new in BS5)

**5. Buttons (`_buttons.scss`):**
- Verify button classes (mostly unchanged)
- Check button groups
- Check toggle buttons (changed in BS5)

**6. Modals (`_modals.scss`):**
- Verify modal styles
- Check modal backdrop
- Check modal sizing

**7. Utilities (`_utilities.scss`):**
- Update custom spacing utilities
- Update custom color utilities
- Remove deprecated utilities

**Common SCSS Updates:**
```scss
// Remove deprecated mixins
// @include hover { } → &:hover { }

// Update media queries (no change needed, but verify)
@include media-breakpoint-up(md) { }

// Update color functions if using deprecated ones
// color-yiq() is deprecated, use custom function
```

**Acceptance Criteria:**
- [ ] All component SCSS files reviewed
- [ ] Deprecated mixin usage removed
- [ ] Card deck usage replaced with grid
- [ ] Form styles updated
- [ ] No SCSS compilation warnings

---

### Task 4: Test Theme - Visual Regression
**Owner:** Developer
**Priority:** HIGH

**Actions:**
```bash
# Rebuild theme
cd docroot/themes/contrib/openy_carnation
npm run build

# Clear Drupal cache
fin drush cr

# Run BackstopJS tests
cd /private/var/www/YMCAWS_11/docs/bootstrap-5-migration/testing
npx backstop test
```

**Review Results:**
- Compare Bootstrap 4 baseline vs current Bootstrap 5
- Document intentional changes
- Document unintentional regressions
- Prioritize fixes

**Acceptance Criteria:**
- [ ] BackstopJS tests executed
- [ ] Results reviewed and documented
- [ ] Critical regressions identified
- [ ] Fix plan documented (if needed)

---

### Task 5: Activity Finder - Research Current State
**Owner:** Developer
**Priority:** HIGH

**Actions:**
```bash
# Find Activity Finder module
cd docroot/modules/contrib/openy_activity_finder

# Review structure
ls -la
cat package.json
cat webpack.config.js (if exists)

# Review Angular implementation
ls -la components/
```

**Document:**
1. Is Activity Finder a separate Angular app?
2. Does it have its own Bootstrap dependency?
3. How is it loaded on the page?
4. What CSS classes does it use?
5. Are there any Bootstrap JS dependencies?

**Create Documentation:**
`docs/bootstrap-5-migration/modules/ACTIVITY_FINDER_ANALYSIS.md`

**Acceptance Criteria:**
- [ ] Activity Finder structure documented
- [ ] Bootstrap dependencies identified
- [ ] CSS class usage documented
- [ ] Loading mechanism understood

---

### Task 6: Activity Finder - Implement CSS Scoping
**Owner:** Developer
**Priority:** HIGH

**Approach:** Wrap Activity Finder styles in a scoped namespace to prevent conflicts

**Actions:**
```bash
cd docroot/modules/contrib/openy_activity_finder
```

**Option A: SCSS Namespace Wrapping**

**Create `assets/scss/activity-finder-scoped.scss`:**
```scss
// Wrapper to scope Activity Finder styles
.activity-finder-app {
  // Import Bootstrap 4 for Activity Finder ONLY
  // (Keep AF on BS4 while theme uses BS5)
  @import '~bootstrap/scss/bootstrap';

  // Import Activity Finder component styles
  @import 'components/all';

  // Ensure specificity
  & * {
    // Reset if needed
  }
}
```

**Update Activity Finder Container:**
```html
<div class="activity-finder-app" id="activity-finder-root">
  <!-- Activity Finder Angular app loads here -->
</div>
```

**Option B: Shadow DOM (Advanced)**

If Activity Finder is a separate Angular app, consider using Shadow DOM:
```javascript
// Encapsulate Activity Finder in Shadow DOM
const afContainer = document.getElementById('activity-finder-root');
const shadow = afContainer.attachShadow({ mode: 'open' });
// Load Angular app into shadow DOM
```

**Acceptance Criteria:**
- [ ] Activity Finder styles scoped/isolated
- [ ] No CSS conflicts with theme Bootstrap 5
- [ ] Activity Finder still functions correctly
- [ ] No visual regressions in Activity Finder
- [ ] Documentation updated

---

### Task 7: Activity Finder - Test Isolation
**Owner:** Developer
**Priority:** HIGH

**Actions:**
```bash
# Rebuild everything
cd docroot/themes/contrib/openy_carnation
npm run build

cd docroot/modules/contrib/openy_activity_finder
npm run build

# Clear cache
fin drush cr
```

**Test Scenarios:**
1. Load page with Activity Finder
2. Verify Activity Finder renders correctly
3. Verify Activity Finder functionality works
4. Verify theme styles don't affect Activity Finder
5. Verify Activity Finder styles don't affect theme
6. Test responsive behavior
7. Test browser console for errors

**Test Pages:**
- Activity Finder standalone page
- Activity Finder embedded in landing page
- Activity Finder with theme components nearby

**Acceptance Criteria:**
- [ ] Activity Finder renders correctly
- [ ] Activity Finder functionality works
- [ ] No CSS conflicts detected
- [ ] No JavaScript errors
- [ ] Responsive behavior correct

---

### Task 8: Update Theme README and Documentation
**Owner:** Developer
**Priority:** MEDIUM

**Actions:**
```bash
cd docroot/themes/contrib/openy_carnation
```

**Update README.md:**
- Document Bootstrap 5 usage
- Document build process
- Document development workflow
- Document Activity Finder isolation approach

**Create BOOTSTRAP5_MIGRATION.md:**
- Document what changed from Bootstrap 4
- Document any breaking changes
- Document new features available
- Document known issues

**Acceptance Criteria:**
- [ ] README.md updated
- [ ] BOOTSTRAP5_MIGRATION.md created
- [ ] Build process documented
- [ ] Activity Finder isolation documented

---

### Task 9: Accessibility Testing - Baseline
**Owner:** Developer
**Priority:** MEDIUM

**Actions:**
```bash
cd /private/var/www/YMCAWS_11/docs/bootstrap-5-migration/testing

# Run Pa11y on updated theme
npx pa11y-ci --reporter html > pa11y-theme-bs5.html
```

**Compare:**
- Baseline (Bootstrap 4) accessibility report
- Current (Bootstrap 5) accessibility report
- Identify any regressions
- Identify any improvements

**Acceptance Criteria:**
- [ ] Pa11y tests executed
- [ ] Results compared to baseline
- [ ] No new accessibility issues introduced
- [ ] Results documented

---

## Testing

### Build Testing:
- [ ] Theme builds successfully
- [ ] Activity Finder builds successfully
- [ ] No build errors or warnings

### Visual Testing:
- [ ] Homepage renders correctly
- [ ] Branch page renders correctly
- [ ] Program page renders correctly
- [ ] Activity Finder renders correctly
- [ ] All responsive breakpoints work

### Functional Testing:
- [ ] Navigation works
- [ ] Dropdowns work
- [ ] Modals work (if any)
- [ ] Forms work
- [ ] Activity Finder search works
- [ ] Activity Finder filters work

### Cross-Browser Testing:
- [ ] Chrome/Edge (Chromium)
- [ ] Firefox
- [ ] Safari
- [ ] Mobile Safari
- [ ] Mobile Chrome

### Accessibility Testing:
- [ ] Pa11y report generated
- [ ] No new issues introduced
- [ ] Keyboard navigation works
- [ ] Screen reader compatible

---

## Deliverables

### Must Have:
- [ ] openy_carnation theme fully migrated to Bootstrap 5
- [ ] All templates updated
- [ ] All SCSS updated
- [ ] Activity Finder isolated with scoped CSS
- [ ] No CSS conflicts
- [ ] All functionality working
- [ ] Documentation updated

### Nice to Have:
- [ ] Performance optimization
- [ ] Code splitting
- [ ] Source maps
- [ ] Development mode

---

## Decision Points

### Decision: Activity Finder Isolation Strategy
**Options:**
1. SCSS namespace wrapping (`.activity-finder-app { }`)
2. Shadow DOM encapsulation
3. Keep Activity Finder on Bootstrap 4 (isolated)
4. Migrate Activity Finder to Bootstrap 5 immediately

**Recommendation:** Option 3 - Keep Activity Finder on Bootstrap 4, isolated with namespace

**Decision Required By:** Task 6
**Decision Maker:** Developer + Project Lead
**Documentation:** `docs/bootstrap-5-migration/decisions/DECISION_ACTIVITY_FINDER_ISOLATION.md`

---

## Risks

### Risk: Activity Finder CSS Conflicts
**Likelihood:** High
**Impact:** High
**Mitigation:** Thorough testing, use CSS specificity, consider Shadow DOM if needed

### Risk: Template Updates Break Functionality
**Likelihood:** Medium
**Impact:** High
**Mitigation:** Test each component individually, keep Bootstrap 4 branch for reference

### Risk: Accessibility Regressions
**Likelihood:** Low
**Impact:** High
**Mitigation:** Run Pa11y tests before and after, manual keyboard testing

---

## Notes

### Important:
- Activity Finder isolation is critical - prevents need to migrate AF immediately
- Test thoroughly - this completes Phase 1
- All theme work must be complete before starting module migrations
- Document everything - will help with module migrations

### Tips:
- Commit after each major component update
- Test in browser frequently
- Keep Bootstrap 5 migration guide open
- Compare with lb_accordion for reference
- Use browser dev tools to inspect CSS conflicts

### References:
- Bootstrap 5 Migration Guide: https://getbootstrap.com/docs/5.3/migration/
- Bootstrap 5 Components: https://getbootstrap.com/docs/5.3/components/
- CSS Scoping: https://developer.mozilla.org/en-US/docs/Web/CSS/:scope

---

## Sprint Review Checklist

At end of sprint, verify:
- [ ] All tasks completed
- [ ] Theme fully functional with Bootstrap 5
- [ ] Activity Finder isolated and functional
- [ ] All deliverables created
- [ ] Documentation updated
- [ ] Phase 1 complete and Phase 2 ready to start
- [ ] Stakeholders informed

---

## Navigation

- **Previous:** [Sprint 2 - Theme Part 1](SPRINT_02_Theme_Part1.md)
- **Next:** [Sprint 4 - WS Small Y Batch 1](SPRINT_04_WS_SmallY_Batch1.md)
- **Phase:** [Phase 1 - Preparation](../phases/PHASE_1_PREPARATION.md)
- **Overview:** [Executive Summary](../EXECUTIVE_SUMMARY.md)

---

**Sprint Status:** ⬜ Not Started
**Last Updated:** 2025-10-17
