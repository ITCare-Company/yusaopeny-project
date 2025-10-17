# Sprint 6: WS Other Modules

**Phase:** [Phase 2 - Component Migration](../phases/PHASE_2_COMPONENT_MIGRATION.md)
**Resources:** 1 Developer
**Status:** Not Started

---

## Sprint Goal

Migrate remaining WS modules outside of small_y package (6 modules), completing the WS module family migration.

---

## Modules in This Sprint

1. **ws_event** - Event display and management components
2. **ws_promotion** - Promotional content components
3. **ws_colorway_canada** - Canada-specific color schemes
4. **ws_lb_tabs** - Layout Builder tabs integration
5. **ws_home_branch** - Home branch selector
6. **ws_alerts** - Alert/notification system (if separate from small_y_alerts)

**Total:** 6 modules (estimated - verify exact count)

---

## Pre-Sprint Preparation

### Checklist:
- [ ] Sprint 5 completed
- [ ] All 16 ws_small_y modules working
- [ ] Migration pattern established and efficient
- [ ] No blockers from previous sprints

---

## Tasks

### Task 1: Module 17 - ws_event
**Owner:** Developer
**Priority:** HIGH

**Location:** `docroot/modules/contrib/ws_event/`

**Actions:**
```bash
cd docroot/modules/contrib/ws_event

# Study module structure
cat package.json
ls -la assets/
cat ws_event.info.yml
cat ws_event.libraries.yml
```

**Event Module Specifics:**
- May include complex layouts (event listings, calendars)
- May use cards, badges, buttons from Bootstrap
- May have custom date/time display components
- Check for any date picker usage

**Migration Steps:**
1. Update package.json
2. Update webpack.config.js
3. Update SCSS files
4. Update templates (check for card layouts, buttons, badges)
5. Update JavaScript (check for date pickers, modals)
6. Build and test

**Special Attention:**
```twig
{# Check for event card layouts #}
<div class="card event-card">
  {# Update card structure if needed #}
</div>

{# Check for date badges #}
<span class="badge badge-primary"> → <span class="badge bg-primary">

{# Check for event modals/details #}
<button data-toggle="modal"> → <button data-bs-toggle="modal">
```

**Acceptance Criteria:**
- [ ] Module builds successfully
- [ ] Event listings display correctly
- [ ] Event details display correctly
- [ ] Date/time formatting correct
- [ ] Links and buttons work
- [ ] Responsive layout works
- [ ] No console errors

---

### Task 2: Module 18 - ws_promotion
**Owner:** Developer
**Priority:** HIGH

**Location:** `docroot/modules/contrib/ws_promotion/`

**Actions:**
```bash
cd docroot/modules/contrib/ws_promotion

# Study module
cat package.json
ls -la assets/
```

**Promotion Module Specifics:**
- Promotional banners/cards
- Call-to-action buttons
- May use alerts or cards
- Image overlays and text positioning

**Migration Steps:**
1. Update package.json
2. Update webpack.config.js
3. Update SCSS files
4. Update templates
5. Update JavaScript (if any)
6. Build and test

**Special Attention:**
```scss
// Check for card overlays
.card-img-overlay {
  // Verify positioning still works
}

// Check for text alignment classes
.text-left → .text-start
.text-right → .text-end

// Check for button groups
.btn-group {
  // Verify still works with BS5
}
```

**Acceptance Criteria:**
- [ ] Module builds successfully
- [ ] Promotional content displays correctly
- [ ] Images display correctly
- [ ] Overlays work correctly
- [ ] Call-to-action buttons styled correctly
- [ ] Responsive design works

---

### Task 3: Module 19 - ws_colorway_canada
**Owner:** Developer
**Priority:** MEDIUM

**Location:** `docroot/modules/contrib/ws_colorway_canada/`

**Actions:**
```bash
cd docroot/modules/contrib/ws_colorway_canada

# Study color system
cat assets/scss/_variables.scss
cat assets/scss/components/*.scss
```

**Colorway Module Specifics:**
- Custom color palette for Canadian YMCA sites
- May override Bootstrap color variables
- Theme customization

**Migration Steps:**
1. Update package.json
2. Update webpack.config.js
3. **Critical:** Update color variable names (BS4 → BS5)
4. Update SCSS imports
5. Build and test

**Bootstrap 5 Color System Changes:**
```scss
// Bootstrap 4 variables
$brand-primary → $primary
$brand-success → $success

// Bootstrap 5 - verify these exist
$primary: #custom-color;
$secondary: #custom-color;

// New in BS5 - additional theme colors
$colors: (
  "primary": $primary,
  "secondary": $secondary,
  "custom-color": #custom-value
);
```

**Acceptance Criteria:**
- [ ] Module builds successfully
- [ ] Color palette renders correctly
- [ ] Custom colors applied correctly
- [ ] No color variable warnings
- [ ] Theme switcher works (if applicable)
- [ ] All color variants work (primary, secondary, etc.)

---

### Task 4: Module 20 - ws_lb_tabs
**Owner:** Developer
**Priority:** HIGH

**Location:** `docroot/modules/contrib/ws_lb_tabs/`

**Actions:**
```bash
cd docroot/modules/contrib/ws_lb_tabs

# Study Layout Builder integration
cat ws_lb_tabs.info.yml
cat ws_lb_tabs.libraries.yml
ls -la templates/
```

**WS LB Tabs Specifics:**
- Layout Builder integration
- May be similar to small_y_tabs but with LB-specific features
- Tab navigation with content regions
- May include drag-and-drop admin UI

**Migration Steps:**
1. Update package.json
2. Update webpack.config.js
3. Update SCSS files
4. Update templates (tab structure, data attributes)
5. Update JavaScript (tab initialization, LB integration)
6. Build and test

**Tab-Specific Updates:**
```twig
{# Bootstrap 4 #}
<ul class="nav nav-tabs">
  <li class="nav-item">
    <a class="nav-link" data-toggle="tab" href="#tab1">

{# Bootstrap 5 #}
<ul class="nav nav-tabs">
  <li class="nav-item">
    <button class="nav-link" data-bs-toggle="tab" data-bs-target="#tab1">
```

**Layout Builder Considerations:**
- Test in Layout Builder admin UI
- Test tab rendering on frontend
- Test with multiple tab instances
- Verify drag-and-drop doesn't break tabs

**Acceptance Criteria:**
- [ ] Module builds successfully
- [ ] Tabs work in Layout Builder admin
- [ ] Tabs render correctly on frontend
- [ ] Tab content displays correctly
- [ ] Multiple tab instances work
- [ ] Deep linking works (if implemented)
- [ ] Keyboard navigation works

---

### Task 5: Module 21 - ws_home_branch
**Owner:** Developer
**Priority:** HIGH

**Location:** `docroot/modules/contrib/ws_home_branch/`

**Actions:**
```bash
cd docroot/modules/contrib/ws_home_branch

# Study module
cat package.json
ls -la assets/
cat templates/*.html.twig
```

**Home Branch Module Specifics:**
- Branch selector/switcher UI
- Likely uses dropdowns or modals
- May have geolocation features
- Session storage for user preference

**Migration Steps:**
1. Update package.json
2. Update webpack.config.js
3. Update SCSS files
4. Update templates (dropdown/modal structure)
5. Update JavaScript (dropdown/modal API, storage)
6. Build and test

**Component Updates:**
```twig
{# If using dropdown #}
<div class="dropdown">
  <button data-toggle="dropdown"> → data-bs-toggle="dropdown">
</div>

{# If using modal #}
<div class="modal">
  <button data-toggle="modal"> → data-bs-toggle="modal">
</div>
```

**JavaScript Updates:**
```javascript
// Bootstrap 5 API
import { Dropdown } from 'bootstrap';
import { Modal } from 'bootstrap';

// Initialize components
const dropdown = new Dropdown(element);
const modal = new Modal(element);
```

**Acceptance Criteria:**
- [ ] Module builds successfully
- [ ] Branch selector displays correctly
- [ ] Branch selection works
- [ ] User preference saved
- [ ] Geolocation works (if implemented)
- [ ] Modal/dropdown closes correctly
- [ ] Responsive design works

---

### Task 6: Module 22 - ws_alerts (if separate)
**Owner:** Developer
**Priority:** MEDIUM

**Note:** This may be the same as small_y_alerts from Sprint 4. Verify if this is a separate module.

**Location:** `docroot/modules/contrib/ws_alerts/`

**Actions:**
```bash
# Check if module exists
ls -la docroot/modules/contrib/ws_alerts/

# If separate from small_y_alerts, migrate
# If same, skip this task
```

**If Separate Module:**
Follow alert migration pattern from Sprint 5:
- Update close button: `class="close"` → `class="btn-close"`
- Update data attributes: `data-dismiss` → `data-bs-dismiss`
- Remove `<span>&times;</span>`

**Acceptance Criteria:**
- [ ] Module existence verified
- [ ] If separate: Module migrated following alert pattern
- [ ] If same: Task marked as N/A

---

### Task 7: Verify Module Inventory Complete
**Owner:** Developer
**Priority:** HIGH

**Actions:**
```bash
# List all WS modules
find docroot/modules/contrib/ -name "ws_*" -type d -maxdepth 1

# List all ws_small_y modules
find docroot/modules/contrib/ws_small_y/modules/ -type d -maxdepth 1

# Cross-reference with MODULE_INVENTORY.md
```

**Verification:**
1. Confirm all WS modules identified
2. Confirm all have been migrated or planned
3. Update MODULE_INVENTORY.md with status
4. Identify any missed modules

**Update Status:**
```markdown
## WS Module Family - Status

### ws_small_y modules (16): ✅ Complete
1. ✅ small_y_hero (Sprint 4)
2. ✅ small_y_cards (Sprint 4)
[... all 16 modules listed ...]

### WS Other Modules (6): ✅ Complete
1. ✅ ws_event (Sprint 6)
2. ✅ ws_promotion (Sprint 6)
3. ✅ ws_colorway_canada (Sprint 6)
4. ✅ ws_lb_tabs (Sprint 6)
5. ✅ ws_home_branch (Sprint 6)
6. ✅ ws_alerts (Sprint 6 or N/A)

**Total WS Modules: 22 completed**
```

**Acceptance Criteria:**
- [ ] All WS modules identified
- [ ] All WS modules migrated
- [ ] MODULE_INVENTORY.md updated
- [ ] No WS modules missed

---

### Task 8: Integration Testing - All WS Modules
**Owner:** Developer
**Priority:** CRITICAL

**Actions:**
```bash
# Rebuild all WS modules
cd docroot/modules/contrib

# ws_small_y modules
for module in ws_small_y/modules/*; do
  cd $module
  if [ -f package.json ]; then
    npm run build
  fi
  cd ../..
done

# WS other modules
for module in ws_event ws_promotion ws_colorway_canada ws_lb_tabs ws_home_branch; do
  if [ -d $module ]; then
    cd $module
    if [ -f package.json ]; then
      npm run build
    fi
    cd ..
  fi
done

# Clear Drupal cache
fin drush cr
```

**Comprehensive Testing:**

**1. Create Test Page:**
- Layout Builder page with multiple WS components
- Include components from all sprints (4, 5, 6)
- Test component interactions

**2. Test Scenarios:**
- [ ] All 22 WS modules render correctly
- [ ] No CSS conflicts between modules
- [ ] No JavaScript errors
- [ ] Components work together on same page
- [ ] Nested components work (tabs with cards, modals with forms, etc.)
- [ ] Responsive design works across all breakpoints
- [ ] Browser compatibility (Chrome, Firefox, Safari, Edge)

**3. Layout Builder Testing:**
- [ ] Add/remove components in LB admin
- [ ] Reorder components
- [ ] Configure component settings
- [ ] Preview changes
- [ ] Save and publish
- [ ] Verify frontend display

**4. Performance Testing:**
- [ ] Page load time acceptable
- [ ] CSS bundle size reasonable
- [ ] JavaScript bundle size reasonable
- [ ] No render-blocking resources

**Acceptance Criteria:**
- [ ] All 22 WS modules work correctly
- [ ] No integration issues
- [ ] Performance acceptable
- [ ] All tests passing

---

### Task 9: Visual Regression Testing - Complete WS Suite
**Owner:** Developer
**Priority:** HIGH

**Actions:**
```bash
cd /private/var/www/YMCAWS_11/docs/bootstrap-5-migration/testing

# Update backstop.json with comprehensive scenarios
# Include all WS components

npx backstop test
```

**Test Scenarios:**
Create comprehensive scenarios covering:
- Individual components
- Component combinations
- Common page layouts
- Edge cases (long text, many items, etc.)

**Acceptance Criteria:**
- [ ] Visual regression tests cover all WS modules
- [ ] Tests executed successfully
- [ ] Results reviewed and documented
- [ ] Critical visual issues fixed
- [ ] Intentional changes documented

---

### Task 10: Accessibility Testing - Complete WS Suite
**Owner:** Developer
**Priority:** HIGH

**Actions:**
```bash
cd /private/var/www/YMCAWS_11/docs/bootstrap-5-migration/testing

# Run Pa11y on comprehensive test pages
npx pa11y-ci --reporter html > pa11y-ws-complete.html
```

**Focus Areas:**
- [ ] Keyboard navigation (all interactive components)
- [ ] Screen reader announcements
- [ ] Focus indicators visible
- [ ] Color contrast adequate
- [ ] ARIA attributes correct
- [ ] Form labels present
- [ ] Error messages accessible
- [ ] Loading states announced

**Manual Testing:**
- [ ] Test with screen reader (NVDA/JAWS/VoiceOver)
- [ ] Test keyboard-only navigation
- [ ] Test with high contrast mode
- [ ] Test with zoom (200%)

**Acceptance Criteria:**
- [ ] Pa11y tests pass (WCAG 2.1 AA)
- [ ] Manual testing complete
- [ ] No critical accessibility issues
- [ ] Issues documented and prioritized

---

### Task 11: Documentation - WS Modules Complete
**Owner:** Developer
**Priority:** HIGH

**Actions:**
```bash
cd docs/bootstrap-5-migration
```

**Create/Update Documentation:**

**1. Individual Module Docs:**
- `modules/WS_EVENT.md`
- `modules/WS_PROMOTION.md`
- `modules/WS_COLORWAY_CANADA.md`
- `modules/WS_LB_TABS.md`
- `modules/WS_HOME_BRANCH.md`

**2. Update MIGRATION_LOG.md:**
```markdown
## Sprint 6 - WS Other Modules

### Completed Modules (6):
1. ✅ ws_event
2. ✅ ws_promotion
3. ✅ ws_colorway_canada
4. ✅ ws_lb_tabs
5. ✅ ws_home_branch
6. ✅ ws_alerts (or N/A)

### WS Module Family Summary:
- **Sprint 4:** 6 modules (small_y batch 1)
- **Sprint 5:** 10 modules (small_y batch 2)
- **Sprint 6:** 6 modules (WS other)
- **Total WS Modules Migrated:** 22 modules ✅

### Phase 2 Progress:
- WS Module Family: ✅ Complete
- LB Modules: ⏳ Next (Sprints 8-11)
- OpenY Modules: ⏳ Next (Sprints 12-15)

### Lessons Learned:
[Document key lessons from WS migration]
```

**3. Create WS_MIGRATION_SUMMARY.md:**
```markdown
# WS Module Family Migration Summary

## Overview
Complete migration of 22 WS modules from Bootstrap 4 to Bootstrap 5.

## Modules Migrated
[List all 22 modules with links to individual docs]

## Common Patterns
[Document common migration patterns discovered]

## Challenges
[Document challenges and solutions]

## Performance
[Document bundle size comparisons, performance metrics]

## Next Steps
[Point to next phase - LB modules]
```

**Acceptance Criteria:**
- [ ] All module docs created
- [ ] MIGRATION_LOG.md updated
- [ ] WS_MIGRATION_SUMMARY.md created
- [ ] Lessons learned documented
- [ ] Progress tracked accurately

---

## Testing

### Build Testing:
- [ ] All 6 modules build successfully
- [ ] All 22 WS modules build successfully
- [ ] No build errors or warnings

### Functional Testing:
- [ ] All WS components work individually
- [ ] All WS components work together
- [ ] Layout Builder integration works
- [ ] Home branch selector works
- [ ] Event display works
- [ ] Promotional content works

### Visual Testing:
- [ ] BackstopJS comprehensive tests pass
- [ ] Visual consistency across all WS modules
- [ ] Responsive design works

### Accessibility Testing:
- [ ] Pa11y tests pass (WCAG 2.1 AA)
- [ ] Manual accessibility testing complete
- [ ] No critical accessibility issues

### Performance Testing:
- [ ] Page load time acceptable
- [ ] Bundle sizes reasonable
- [ ] No performance regressions

---

## Deliverables

### Must Have:
- [ ] 6 WS other modules migrated
- [ ] All 22 WS modules working
- [ ] Integration testing complete
- [ ] Visual regression testing complete
- [ ] Accessibility testing complete
- [ ] Documentation complete
- [ ] WS migration summary document

### Nice to Have:
- [ ] Performance benchmark document
- [ ] Bundle size comparison (BS4 vs BS5)
- [ ] Migration pattern guide for next phases

---

## Decision Points

### Decision: ws_alerts Module Status
**Options:**
1. Separate module - migrate in Sprint 6
2. Same as small_y_alerts - mark as N/A

**Decision Required By:** Task 6
**Decision Maker:** Developer

---

## Risks

### Risk: Unknown Module Dependencies
**Likelihood:** Low
**Impact:** Medium
**Mitigation:** Thorough inventory check, test all modules together

### Risk: Layout Builder Integration Issues
**Likelihood:** Medium
**Impact:** High
**Mitigation:** Test LB admin UI thoroughly, verify component configuration works

### Risk: Color System Conflicts (ws_colorway_canada)
**Likelihood:** Low
**Impact:** Medium
**Mitigation:** Test color variables carefully, verify no conflicts with theme

---

## Notes

### Important:
- This sprint completes ALL WS modules (22 total)
- Comprehensive testing is critical before moving to next module family
- Document patterns for use in LB and OpenY module migrations
- Celebrate milestone - WS module family complete!

### Tips:
- Use established migration pattern - should be efficient now
- Test in Layout Builder admin frequently
- Test component interactions thoroughly
- Document any new patterns discovered

### Milestone:
**WS Module Family Complete! 🎉**
- 22 modules migrated
- ~33% of total migration complete
- Foundation established for remaining modules

---

## Sprint Review Checklist

At end of sprint, verify:
- [ ] All 6 modules completed
- [ ] All 22 WS modules working
- [ ] Comprehensive testing complete
- [ ] Documentation complete
- [ ] Milestone celebrated with team
- [ ] Next sprint (LB modules) ready to start

---

## Navigation

- **Previous:** [Sprint 5 - WS Small Y Batch 2](SPRINT_05_WS_SmallY_Batch2.md)
- **Next:** [Sprint 7 - Testing & Catchup](SPRINT_07_Testing_Catchup.md)
- **Phase:** [Phase 2 - Component Migration](../phases/PHASE_2_COMPONENT_MIGRATION.md)
- **Overview:** [Executive Summary](../EXECUTIVE_SUMMARY.md)

---

**Sprint Status:** ⬜ Not Started
**Last Updated:** 2025-10-17
