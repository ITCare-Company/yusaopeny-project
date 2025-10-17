# Sprint 22: Comprehensive Testing & Bug Fixes

**Phase:** [Phase 6 - Testing & Rollout](../phases/PHASE_6_TESTING_ROLLOUT.md)
**Resources:** 1 Developer + QA Support
**Status:** Not Started

---

## Sprint Goal

Execute comprehensive testing (visual regression, accessibility, performance, cross-browser) across all migrated modules. Fix all critical bugs before rollout.

---

## Tasks

### Task 1: Visual Regression Testing (BackstopJS)
**Owner:** Developer
**Priority:** CRITICAL

**Actions:**
```bash
cd docs/bootstrap-5-migration/testing

# Configure 200+ scenarios covering:
# - All page types (homepage, branch, program, camp, event, donation)
# - All 19 LB + 22 WS components
# - Activity Finder, Camp Finder
# - 4 viewports (mobile 375px, tablet 768px, desktop 1024px, large 1440px)

npx backstop test
npx backstop openReport
npx backstop approve
```

**Document visual differences:**
- Expected: Bootstrap 5 improvements (spacing, shadows, rounded corners)
- Acceptable: Minor browser rendering differences
- Unacceptable: Layout breaks, missing content, broken functionality

**Acceptance Criteria:**
- [ ] 200+ scenarios configured and tested
- [ ] 98%+ pass rate achieved
- [ ] All failures categorized and documented
- [ ] Baseline approved

---

### Task 2: Accessibility Testing (Pa11y + Manual)
**Owner:** Developer + QA
**Priority:** CRITICAL

**Automated Testing:**
```bash
cd docs/bootstrap-5-migration/testing
npx pa11y-ci --reporter html > reports/accessibility-report.html
# Test all pages for WCAG 2.2 AA compliance
```

**Manual Testing:**
- [ ] Keyboard navigation (Tab, Enter, Esc, Arrows) - all components
- [ ] Screen reader (NVDA/JAWS/VoiceOver) - content announced correctly
- [ ] Focus indicators visible
- [ ] Color contrast WCAG 2.2 AA (normal 4.5:1, large 3:1, UI 3:1)

**Priority Components:**
- [ ] Activity Finder 4 (complex Vue app)
- [ ] Donation forms (critical user path)
- [ ] Modals (focus trap, ESC close)
- [ ] Carousels (pause, keyboard controls)
- [ ] Navigation menus

**Deliverables:**
- [ ] Pa11y report complete
- [ ] Manual testing checklist complete
- [ ] `reports/ACCESSIBILITY_REPORT.md`

**Acceptance Criteria:**
- [ ] WCAG 2.2 AA compliant
- [ ] Zero critical accessibility issues
- [ ] All interactive elements keyboard accessible

---

### Task 3: Performance Testing & Optimization
**Owner:** Developer
**Priority:** HIGH

**Lighthouse Testing (target 90+ scores):**
```bash
# Test key pages: Homepage, Branch detail, Activity Finder, LB landing page
# Metrics:
# - First Contentful Paint < 1.8s
# - Largest Contentful Paint < 2.5s
# - Time to Interactive < 3.8s
# - Cumulative Layout Shift < 0.1
# - Total Blocking Time < 200ms
```

**Bundle Size Analysis:**
```bash
cd docroot/modules/contrib
for module in lb_* ws_*; do
  if [ -d "$module/dist" ]; then
    ls -lh $module/dist/*.js
  fi
done
# Expected: Similar or smaller than Bootstrap 4
# Flag: Any bundle >100KB increase
```

**Memory Leak Testing:**
```bash
# Use Chrome DevTools Memory Profiler
# - Open/close modal 20 times
# - Navigate carousel 50 slides
# - Open/close accordions 10 times
# Memory should return to baseline
```

**Deliverables:**
- [ ] Lighthouse scores 90+ documented
- [ ] Bundle size comparison
- [ ] `reports/PERFORMANCE_REPORT.md`

**Acceptance Criteria:**
- [ ] All Lighthouse scores 90+
- [ ] No significant bundle size increase
- [ ] No memory leaks
- [ ] Page load < 3s (3G)

---

### Task 4: Cross-Browser Testing
**Owner:** Developer + QA
**Priority:** HIGH

**Desktop Browsers:**
- [ ] Chrome (latest 2 versions)
- [ ] Firefox (latest 2 versions)
- [ ] Safari (latest 2 versions)
- [ ] Edge (latest 2 versions)

**Mobile Browsers:**
- [ ] Safari iOS (latest 2 versions) - Real device
- [ ] Chrome Android (latest 2 versions) - Real device
- [ ] Samsung Internet (latest)

**Test Matrix:**
- [ ] Homepage
- [ ] Branch page with Activity Finder
- [ ] Landing page with LB components
- [ ] Form submission
- [ ] Modal interactions
- [ ] Carousel swipe/click
- [ ] Date picker on mobile

**Deliverables:**
- [ ] Browser compatibility matrix
- [ ] `reports/BROWSER_COMPATIBILITY_REPORT.md`

**Acceptance Criteria:**
- [ ] 100% compatibility on target browsers
- [ ] All features work on mobile
- [ ] No browser-specific bugs

---

### Task 5: Integration Testing
**Owner:** Developer + QA
**Priority:** HIGH

**Module Combinations:**
- [ ] Multiple LB components on same page (10+)
- [ ] Activity Finder + Branch content type
- [ ] Camp Finder + Camp content type
- [ ] Webform + Modal + Date picker
- [ ] All Vue apps on same site

**Drupal Integration:**
- [ ] Layout Builder inline editing
- [ ] Content editing forms (all content types)
- [ ] Media library
- [ ] Webform submissions
- [ ] Search functionality

**Real-World Scenarios:**
- [ ] Site builder creates branch page
- [ ] Site builder creates landing page with 15+ LB components
- [ ] User filters Activity Finder
- [ ] User submits donation form

**Acceptance Criteria:**
- [ ] All module combinations work
- [ ] No JavaScript conflicts
- [ ] Drupal editing experience intact

---

### Task 6: Bug Triage & Critical Fixes
**Owner:** Developer
**Priority:** CRITICAL

**Triage Criteria:**
- **Critical:** Site down, data loss, security → Fix immediately
- **High:** Major feature broken, bad UX → Fix before rollout
- **Medium:** Minor feature issue → Fix before A-tier or document
- **Low:** Edge case, cosmetic → Document as known issue

**Actions:**
```bash
touch docs/bootstrap-5-migration/testing/BUG_TRACKER.md
```

- Fix all critical and high-priority bugs
- Document fixes in MIGRATION_LOG.md
- Create regression tests for bugs
- Document medium/low bugs with workarounds in KNOWN_ISSUES.md

**Acceptance Criteria:**
- [ ] Zero critical bugs
- [ ] Zero high-priority bugs in core functionality
- [ ] All bugs documented
- [ ] Known issues have workarounds

---

## Testing Checklist

- [ ] Visual regression: 200+ scenarios, 98%+ pass
- [ ] Accessibility: WCAG 2.2 AA, keyboard + screen reader
- [ ] Performance: Lighthouse 90+, no memory leaks
- [ ] Cross-browser: 6 browsers, 100% compatible
- [ ] Mobile: iOS + Android, touch gestures
- [ ] Integration: All modules work together

---

## Deliverables

### Must Have:
- [ ] Visual regression suite (200+ scenarios)
- [ ] Accessibility testing (WCAG 2.2 AA)
- [ ] Performance testing (90+ scores)
- [ ] Cross-browser testing (100%)
- [ ] All critical/high bugs fixed
- [ ] Bug tracker and known issues documented
- [ ] GO/NO-GO decision document

### Nice to Have:
- [ ] Medium-priority bugs fixed
- [ ] Video recordings of tests
- [ ] Automated CI/CD test suite

---

## Decision Points

### Decision: GO/NO-GO for Rollout
**Criteria:**
- All critical bugs fixed
- All high-priority bugs fixed
- Testing coverage 98%+
- WCAG 2.2 AA compliant
- Lighthouse 90+ scores

**Options:**
- **GO:** Proceed to Sprint 23 (documentation and rollout)
- **NO-GO:** Extend sprint for bug fixes

**Decision Maker:** Project Lead + Stakeholders
**Documentation:** `decisions/DECISION_SPRINT_22_GO_NO_GO.md`

---

## Risks

### Risk: Too Many Critical Bugs (HIGH)
**Mitigation:**
- Start testing early
- Triage immediately
- 16 hours buffer time
- Contingency to extend sprint

### Risk: Testing Takes Too Long (MEDIUM)
**Mitigation:**
- Automate (BackstopJS, Pa11y)
- Focus on critical paths
- Run tests in parallel
- Use QA support

---

## Notes

**Important:**
- This is the quality gate - be thorough
- Fix critical bugs before rollout
- Document everything
- Create regression tests

**Tips:**
- Start with automated tests
- Run tests continuously
- Prioritize bugs ruthlessly
- Use buffer time wisely

---

## Sprint Review Checklist

- [ ] All testing completed
- [ ] Visual regression 98%+
- [ ] Accessibility WCAG 2.2 AA
- [ ] Performance 90+
- [ ] Cross-browser 100%
- [ ] Zero critical bugs
- [ ] GO/NO-GO decision made
- [ ] Sprint 23 ready

---

## Navigation

- **Previous:** [Sprint 21 - Vue Apps Final](SPRINT_21_VueApps_Final.md)
- **Next:** [Sprint 23 - Documentation & Community](SPRINT_23_Documentation_Community.md)
- **Phase:** [Phase 6 - Testing & Rollout](../phases/PHASE_6_TESTING_ROLLOUT.md)
- **Overview:** [Executive Summary](../EXECUTIVE_SUMMARY.md)

---

**Sprint Status:** ⬜ Not Started
**Last Updated:** 2025-10-17
