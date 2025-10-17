# Sprint 7: Testing & Catchup

**Phase:** [Phase 2 - Component Migration](../phases/PHASE_2_COMPONENT_MIGRATION.md)
**Resources:** 1 Developer
**Status:** Not Started

---

## Sprint Goal

Comprehensive testing of all migrated components, upgrade BackstopJS test suite, establish Pa11y baseline for entire site, fix any discovered issues, and catch up on technical debt from Sprints 1-6.

---

## Sprint Overview

This is a **catch-up and consolidation sprint** focused on:
- Quality assurance across all migrated modules
- Test infrastructure upgrades
- Bug fixes and polish
- Technical debt resolution
- Documentation cleanup
- Preparation for next phase (LB modules)

---

## Tasks

### Task 1: BackstopJS Test Suite Upgrade
**Owner:** Developer
**Priority:** HIGH

**Current State:**
- Basic BackstopJS configuration from Sprint 1
- Limited scenarios
- May need additional configuration

**Actions:**
```bash
cd /private/var/www/YMCAWS_11/docs/bootstrap-5-migration/testing
```

**Upgrade backstop.json:**

```json
{
  "id": "yusaopeny_bootstrap5_complete",
  "viewports": [
    {
      "label": "phone",
      "width": 375,
      "height": 667
    },
    {
      "label": "tablet_portrait",
      "width": 768,
      "height": 1024
    },
    {
      "label": "tablet_landscape",
      "width": 1024,
      "height": 768
    },
    {
      "label": "desktop",
      "width": 1280,
      "height": 1024
    },
    {
      "label": "desktop_large",
      "width": 1920,
      "height": 1080
    }
  ],
  "onBeforeScript": "puppet/onBefore.js",
  "onReadyScript": "puppet/onReady.js",
  "scenarios": [
    {
      "label": "Homepage",
      "cookiePath": "backstop_data/cookies.json",
      "url": "http://yusaopeny.docksal.site/",
      "referenceUrl": "",
      "readyEvent": "",
      "readySelector": "",
      "delay": 2000,
      "hideSelectors": [],
      "removeSelectors": [],
      "hoverSelector": "",
      "clickSelector": "",
      "postInteractionWait": 0,
      "selectors": [
        "document"
      ],
      "selectorExpansion": true,
      "expect": 0,
      "misMatchThreshold": 0.1,
      "requireSameDimensions": true
    },
    // Add comprehensive scenarios below
  ],
  "paths": {
    "bitmaps_reference": "backstop_data/bitmaps_reference",
    "bitmaps_test": "backstop_data/bitmaps_test",
    "engine_scripts": "backstop_data/engine_scripts",
    "html_report": "backstop_data/html_report",
    "ci_report": "backstop_data/ci_report"
  },
  "report": ["browser", "json"],
  "engine": "puppeteer",
  "engineOptions": {
    "args": ["--no-sandbox"]
  },
  "asyncCaptureLimit": 5,
  "asyncCompareLimit": 50,
  "debug": false,
  "debugWindow": false
}
```

**Add Comprehensive Scenarios:**

**1. Component Scenarios (WS Modules):**
```json
{
  "label": "WS Hero Banner",
  "url": "http://yusaopeny.docksal.site/test/ws-hero",
  "delay": 1000
},
{
  "label": "WS Cards Layout",
  "url": "http://yusaopeny.docksal.site/test/ws-cards",
  "delay": 1000
},
{
  "label": "WS Carousel",
  "url": "http://yusaopeny.docksal.site/test/ws-carousel",
  "delay": 2000
},
{
  "label": "WS Accordion",
  "url": "http://yusaopeny.docksal.site/test/ws-accordion",
  "delay": 1000
}
// ... add all 22 WS modules
```

**2. Interactive Component Scenarios:**
```json
{
  "label": "Modal - Open State",
  "url": "http://yusaopeny.docksal.site/test/modal",
  "clickSelector": "[data-bs-toggle='modal']",
  "postInteractionWait": 500,
  "delay": 1000
},
{
  "label": "Dropdown - Open State",
  "url": "http://yusaopeny.docksal.site/test/dropdown",
  "clickSelector": "[data-bs-toggle='dropdown']",
  "postInteractionWait": 500,
  "delay": 1000
},
{
  "label": "Tabs - Second Tab",
  "url": "http://yusaopeny.docksal.site/test/tabs",
  "clickSelector": ".nav-tabs .nav-link:nth-child(2)",
  "postInteractionWait": 500,
  "delay": 1000
}
```

**3. Page Layout Scenarios:**
```json
{
  "label": "Branch Page",
  "url": "http://yusaopeny.docksal.site/branch/example",
  "delay": 2000
},
{
  "label": "Program Page",
  "url": "http://yusaopeny.docksal.site/program/example",
  "delay": 2000
},
{
  "label": "Event Page",
  "url": "http://yusaopeny.docksal.site/event/example",
  "delay": 2000
},
{
  "label": "Landing Page - Full Components",
  "url": "http://yusaopeny.docksal.site/landing/test-all-components",
  "delay": 3000
}
```

**4. Theme Scenarios:**
```json
{
  "label": "Header - Desktop",
  "url": "http://yusaopeny.docksal.site/",
  "selectors": ["header"],
  "delay": 1000
},
{
  "label": "Footer - Desktop",
  "url": "http://yusaopeny.docksal.site/",
  "selectors": ["footer"],
  "delay": 1000
},
{
  "label": "Navigation - Desktop",
  "url": "http://yusaopeny.docksal.site/",
  "selectors": [".main-navigation"],
  "delay": 1000
}
```

**Create Test Pages:**
```bash
# Create test content pages for each component
fin drush php-eval "
  // Create landing page with all WS components
  // Script to create test pages
"
```

**Run Comprehensive Tests:**
```bash
# Capture new baseline (Bootstrap 5)
npx backstop reference

# Run tests
npx backstop test

# Approve differences (if intentional)
npx backstop approve
```

**Acceptance Criteria:**
- [ ] backstop.json upgraded with comprehensive scenarios
- [ ] 50+ scenarios covering all WS modules
- [ ] Interactive state scenarios added
- [ ] Test pages created
- [ ] Baseline captured
- [ ] Tests executed and documented
- [ ] CI integration considered

---

### Task 2: Pa11y Baseline - Complete Site
**Owner:** Developer
**Priority:** HIGH

**Current State:**
- Basic Pa11y configuration from Sprint 1
- Limited URL coverage

**Actions:**
```bash
cd /private/var/www/YMCAWS_11/docs/bootstrap-5-migration/testing
```

**Upgrade .pa11yci.json:**

```json
{
  "defaults": {
    "standard": "WCAG2AA",
    "runners": ["axe", "htmlcs"],
    "timeout": 15000,
    "wait": 2000,
    "chromeLaunchConfig": {
      "args": ["--no-sandbox"]
    },
    "hideElements": ".admin-toolbar, .contextual-links"
  },
  "urls": [
    // Homepage and main pages
    "http://yusaopeny.docksal.site/",

    // Content type pages
    "http://yusaopeny.docksal.site/branch/example",
    "http://yusaopeny.docksal.site/program/example",
    "http://yusaopeny.docksal.site/event/example",
    "http://yusaopeny.docksal.site/class/example",
    "http://yusaopeny.docksal.site/camp/example",

    // Component test pages (all WS modules)
    "http://yusaopeny.docksal.site/test/ws-hero",
    "http://yusaopeny.docksal.site/test/ws-cards",
    "http://yusaopeny.docksal.site/test/ws-carousel",
    "http://yusaopeny.docksal.site/test/ws-accordion",
    "http://yusaopeny.docksal.site/test/ws-alerts",
    "http://yusaopeny.docksal.site/test/ws-tabs",
    "http://yusaopeny.docksal.site/test/ws-modals",
    "http://yusaopeny.docksal.site/test/ws-buttons",
    "http://yusaopeny.docksal.site/test/ws-breadcrumbs",
    "http://yusaopeny.docksal.site/test/ws-pagination",
    "http://yusaopeny.docksal.site/test/ws-progress",
    "http://yusaopeny.docksal.site/test/ws-badges",
    "http://yusaopeny.docksal.site/test/ws-tooltips",
    "http://yusaopeny.docksal.site/test/ws-popovers",
    "http://yusaopeny.docksal.site/test/ws-dropdowns",
    "http://yusaopeny.docksal.site/test/ws-spinners",
    "http://yusaopeny.docksal.site/test/ws-event",
    "http://yusaopeny.docksal.site/test/ws-promotion",
    "http://yusaopeny.docksal.site/test/ws-lb-tabs",
    "http://yusaopeny.docksal.site/test/ws-home-branch",

    // Landing page with all components
    "http://yusaopeny.docksal.site/landing/test-all-components",

    // Activity Finder (isolated)
    "http://yusaopeny.docksal.site/activity-finder"
  ]
}
```

**Run Pa11y Suite:**
```bash
# Run tests and generate reports
npx pa11y-ci --reporter html > pa11y-complete-baseline.html
npx pa11y-ci --reporter json > pa11y-complete-baseline.json

# Generate summary
npx pa11y-ci --reporter cli
```

**Analyze Results:**
1. Review all accessibility issues
2. Categorize by severity (error, warning, notice)
3. Identify common patterns
4. Create fix plan for critical issues
5. Document known issues (if acceptable)

**Create Accessibility Report:**
`docs/bootstrap-5-migration/testing/ACCESSIBILITY_BASELINE.md`

```markdown
# Accessibility Baseline Report

**Date:** 2025-10-XX
**Standard:** WCAG 2.1 AA
**Tool:** Pa11y CI (Axe + HTML_CodeSniffer)
**Pages Tested:** 25+

## Summary
- Total Issues: X
- Errors: X
- Warnings: X
- Notices: X

## Critical Issues (Errors)
[List with page URLs]

## Common Patterns
[Document recurring issues]

## Fix Plan
[Prioritized list of fixes]

## Known Issues (Accepted)
[Issues that won't be fixed with justification]
```

**Acceptance Criteria:**
- [ ] .pa11yci.json upgraded with comprehensive URLs
- [ ] 25+ pages tested
- [ ] Baseline report generated
- [ ] Results analyzed and categorized
- [ ] Critical issues identified
- [ ] Fix plan created
- [ ] Documentation complete

---

### Task 3: Cross-Browser Testing
**Owner:** Developer
**Priority:** HIGH

**Browsers to Test:**
- Chrome (latest)
- Firefox (latest)
- Safari (latest - macOS)
- Edge (latest)
- Mobile Safari (iOS)
- Mobile Chrome (Android)

**Test Matrix:**

**For Each Browser:**
1. Homepage
2. Branch page
3. Program page
4. Landing page with all WS components
5. Activity Finder page

**Test Checklist:**
- [ ] Page loads without errors
- [ ] Layout renders correctly
- [ ] Components function correctly
- [ ] Responsive breakpoints work
- [ ] Interactive components work (modals, dropdowns, tabs)
- [ ] Forms work
- [ ] Navigation works
- [ ] No console errors

**Create Browser Test Report:**
`docs/bootstrap-5-migration/testing/BROWSER_COMPATIBILITY.md`

```markdown
# Browser Compatibility Report

**Date:** 2025-10-XX

## Tested Browsers
- Chrome 120+ ✅
- Firefox 121+ ✅
- Safari 17+ ✅
- Edge 120+ ✅
- Mobile Safari (iOS 16+) ✅
- Mobile Chrome (Android 12+) ✅

## Issues Found
[List any browser-specific issues]

## Known Limitations
[Document any known browser limitations]
```

**Tools to Use:**
- BrowserStack (if available)
- Local browser installations
- Mobile device testing (physical devices)
- Chrome DevTools device emulation

**Acceptance Criteria:**
- [ ] All 6 browsers tested
- [ ] Test matrix completed
- [ ] Issues documented
- [ ] Critical issues fixed
- [ ] Browser compatibility report created

---

### Task 4: Performance Testing & Optimization
**Owner:** Developer
**Priority:** MEDIUM

**Metrics to Measure:**

**1. Page Load Performance:**
```bash
# Use Lighthouse
fin bash
cd /path/to/theme
npx lighthouse http://yusaopeny.docksal.site/ --output html --output-path ./lighthouse-report.html
```

**2. Bundle Size Analysis:**
```bash
# For each migrated module
cd docroot/modules/contrib/ws_small_y/modules/small_y_hero

# Check built file sizes
ls -lh dist/css/
ls -lh dist/js/

# Compare with Bootstrap 4 version (if available)
```

**3. CSS Analysis:**
```bash
# Check for unused CSS
npm install -g purgecss

purgecss --css dist/css/*.css --content templates/**/*.twig --output optimized/
```

**4. JavaScript Analysis:**
```bash
# Check bundle sizes
npm install -g webpack-bundle-analyzer

# Add to webpack config and run
webpack --profile --json > stats.json
webpack-bundle-analyzer stats.json
```

**Create Performance Report:**
`docs/bootstrap-5-migration/testing/PERFORMANCE_REPORT.md`

```markdown
# Performance Report

**Date:** 2025-10-XX

## Bundle Sizes

### Bootstrap 4 (Baseline)
- Theme CSS: XXX KB
- Theme JS: XXX KB
- Total: XXX KB

### Bootstrap 5 (Current)
- Theme CSS: XXX KB
- Theme JS: XXX KB
- Total: XXX KB

**Change:** +/- XX%

## Page Load Metrics

### Homepage
- First Contentful Paint: X.Xs
- Largest Contentful Paint: X.Xs
- Time to Interactive: X.Xs
- Total Blocking Time: XXms
- Cumulative Layout Shift: X.XX

### Lighthouse Score
- Performance: XX/100
- Accessibility: XX/100
- Best Practices: XX/100
- SEO: XX/100

## Optimization Opportunities
[List potential optimizations]
```

**Acceptance Criteria:**
- [ ] Lighthouse reports generated
- [ ] Bundle sizes measured and compared
- [ ] Performance metrics documented
- [ ] Optimization opportunities identified
- [ ] Performance report created

---

### Task 5: Bug Fixes and Polish
**Owner:** Developer
**Priority:** CRITICAL

**Actions:**

**1. Review Issue Tracker:**
```bash
# Compile issues from Sprints 1-6
# - MIGRATION_LOG.md issues
# - Module documentation known issues
# - Test results issues
# - Developer notes
```

**2. Categorize Issues:**
- Critical (blocks functionality)
- High (significant visual/functional issue)
- Medium (minor issue, should fix)
- Low (nice-to-have, defer if needed)

**3. Create Fix List:**
`docs/bootstrap-5-migration/ISSUE_TRACKER.md`

```markdown
# Issue Tracker

## Critical Issues (Must Fix)
- [ ] Issue 1: [Description] - Found in [Module/Sprint]
- [ ] Issue 2: [Description] - Found in [Module/Sprint]

## High Priority Issues
- [ ] Issue 3: [Description]
- [ ] Issue 4: [Description]

## Medium Priority Issues
- [ ] Issue 5: [Description]

## Low Priority / Deferred
- [ ] Issue 6: [Description] - Defer to Phase 3
```

**4. Fix Issues:**
- Work through critical issues first
- Test each fix thoroughly
- Document fix in module documentation
- Commit with descriptive messages

**5. Regression Testing:**
After each fix:
- [ ] Test affected component
- [ ] Test related components
- [ ] Run visual regression test for affected areas
- [ ] Run accessibility test for affected areas

**Acceptance Criteria:**
- [ ] All critical issues fixed
- [ ] High priority issues fixed (or defer with justification)
- [ ] Medium issues addressed (time permitting)
- [ ] All fixes tested
- [ ] No new issues introduced
- [ ] Issue tracker updated

---

### Task 6: Documentation Cleanup and Organization
**Owner:** Developer
**Priority:** MEDIUM

**Actions:**

**1. Review All Documentation:**
```bash
cd docs/bootstrap-5-migration

# Review structure
tree

# Check for completeness
# - All modules documented?
# - All sprints documented?
# - All decisions documented?
```

**2. Create Missing Documentation:**
- [ ] Any missing module docs
- [ ] Decision documents not yet created
- [ ] Test reports not documented

**3. Organize and Link:**
- [ ] Add cross-references between documents
- [ ] Update navigation links
- [ ] Create table of contents where needed
- [ ] Add "See also" sections

**4. Update Main Documents:**

**Update EXECUTIVE_SUMMARY.md:**
```markdown
## Progress Update (End of Sprint 7)

### Completed:
- ✅ Phase 1: Preparation (Sprints 1-3)
  - Theme migrated
  - Activity Finder isolated
  - Testing infrastructure established

- 🔄 Phase 2: Component Migration (In Progress)
  - ✅ WS Module Family (22 modules) - Sprints 4-6
  - ✅ Testing & Catchup - Sprint 7
  - ⏳ LB Modules (Next) - Sprints 8-11
  - ⏳ OpenY Modules (Next) - Sprints 12-15

### Statistics:
- **Modules Migrated:** 22 / 66+ (33%)
- **Sprints Completed:** 7 / 15 (47%)
- **Estimated Time Used:** 14 weeks / 30 weeks (47%)
```

**Update README.md (if exists):**
- Overview of migration project
- Links to key documents
- Quick start guide
- How to contribute

**Create INDEX.md:**
`docs/bootstrap-5-migration/INDEX.md`

```markdown
# Bootstrap 5 Migration - Document Index

## Quick Links
- [Executive Summary](EXECUTIVE_SUMMARY.md)
- [Migration Log](MIGRATION_LOG.md)
- [Module Inventory](MODULE_INVENTORY.md)

## Documentation by Category

### Project Overview
- [Executive Summary](EXECUTIVE_SUMMARY.md)
- [Migration Strategy](MIGRATION_STRATEGY.md)
- [Timeline](TIMELINE.md)

### Phases
- [Phase 1: Preparation](phases/PHASE_1_PREPARATION.md)
- [Phase 2: Component Migration](phases/PHASE_2_COMPONENT_MIGRATION.md)
- [Phase 3: Optimization](phases/PHASE_3_OPTIMIZATION.md)

### Sprints
- [Sprint 1: Infrastructure](sprints/SPRINT_01_Infrastructure.md)
- [Sprint 2: Theme Part 1](sprints/SPRINT_02_Theme_Part1.md)
- [Sprint 3: Theme Part 2 + AF Isolation](sprints/SPRINT_03_Theme_Part2_AF_Isolation.md)
- [Sprint 4: WS Small Y Batch 1](sprints/SPRINT_04_WS_SmallY_Batch1.md)
- [Sprint 5: WS Small Y Batch 2](sprints/SPRINT_05_WS_SmallY_Batch2.md)
- [Sprint 6: WS Other Modules](sprints/SPRINT_06_WS_Other_Modules.md)
- [Sprint 7: Testing & Catchup](sprints/SPRINT_07_Testing_Catchup.md)

### Module Documentation
[Links to all module docs]

### Reference
- [LB Accordion Patterns](reference/LB_ACCORDION_PATTERNS.md)
- [Migration Checklist Template](reference/MIGRATION_CHECKLIST_TEMPLATE.md)

### Decisions
- [Date Picker Decision](decisions/DECISION_DATE_PICKER.md)
- [Activity Finder Isolation](decisions/DECISION_ACTIVITY_FINDER_ISOLATION.md)

### Testing
- [Accessibility Baseline](testing/ACCESSIBILITY_BASELINE.md)
- [Browser Compatibility](testing/BROWSER_COMPATIBILITY.md)
- [Performance Report](testing/PERFORMANCE_REPORT.md)
```

**Acceptance Criteria:**
- [ ] All documentation reviewed
- [ ] Missing docs created
- [ ] Cross-references added
- [ ] INDEX.md created
- [ ] Main documents updated
- [ ] Navigation improved

---

### Task 7: Prepare for Next Phase (LB Modules)
**Owner:** Developer
**Priority:** MEDIUM

**Actions:**

**1. Review LB Module List:**
```bash
# List all lb_* modules
find docroot/modules/contrib/ -name "lb_*" -type d -maxdepth 1

# Verify MODULE_INVENTORY.md is accurate
```

**2. Prioritize LB Modules:**
```markdown
## LB Modules Priority

### High Priority (commonly used):
1. lb_accordion (already migrated - reference)
2. lb_hero
3. lb_tabs
4. lb_cards
5. lb_carousel

### Medium Priority:
[List]

### Low Priority:
[List]
```

**3. Plan LB Migration Sprints:**
- Sprint 8: LB Batch 1 (5 modules)
- Sprint 9: LB Batch 2 (5 modules)
- Sprint 10: LB Batch 3 (5 modules)
- Sprint 11: LB Remaining + Integration

**4. Create LB Migration Kickoff Doc:**
`docs/bootstrap-5-migration/phases/LB_MIGRATION_KICKOFF.md`

```markdown
# LB Module Migration Kickoff

## Overview
Layout Builder modules migration (Sprints 8-11)

## Modules to Migrate
[List of all LB modules]

## Reference Module
- lb_accordion (already migrated in BS5)
- Use as primary reference

## Key Considerations
- Layout Builder integration
- Block configuration
- Template structure
- Admin UI compatibility

## Success Criteria
[Define success criteria]
```

**Acceptance Criteria:**
- [ ] LB module list verified
- [ ] Modules prioritized
- [ ] Sprint plan created
- [ ] Kickoff document created
- [ ] Next sprint ready to start

---

### Task 8: Team Knowledge Sharing
**Owner:** Developer
**Priority:** LOW

**Actions:**

**1. Create Migration Guide:**
`docs/bootstrap-5-migration/MIGRATION_GUIDE.md`

```markdown
# Bootstrap 5 Migration Guide

## Quick Reference

### Data Attribute Changes
- `data-toggle` → `data-bs-toggle`
- `data-target` → `data-bs-target`
- `data-dismiss` → `data-bs-dismiss`
- `data-slide` → `data-bs-slide`

### CSS Class Changes
- `float-left` → `float-start`
- `float-right` → `float-end`
- `text-left` → `text-start`
- `text-right` → `text-end`
- `ml-*` → `ms-*` (margin-left → margin-start)
- `mr-*` → `me-*` (margin-right → margin-end)
- `pl-*` → `ps-*` (padding-left → padding-start)
- `pr-*` → `pe-*` (padding-right → padding-end)
- `badge-{color}` → `bg-{color}`
- `badge-pill` → `rounded-pill`
- `close` → `btn-close`
- `form-group` → remove (use `mb-3`)
- `sr-only` → `visually-hidden`

### Component Changes
- Cards: No card-deck, use grid
- Alerts: Use btn-close, no × span
- Modals: Use btn-close
- Forms: Add form-label class
- Dropdowns: Can use <ul> structure

### JavaScript Changes
- Import individual components
- Use ES6 imports
- Manual initialization required
- New API methods

## Migration Process
[Step-by-step process]

## Common Issues
[List common issues and solutions]
```

**2. Create FAQ:**
`docs/bootstrap-5-migration/FAQ.md`

**3. Presentation/Demo:**
- Create slides or document for team presentation
- Demo key changes
- Share lessons learned

**Acceptance Criteria:**
- [ ] Migration guide created
- [ ] FAQ created
- [ ] Presentation material prepared
- [ ] Team knowledge sharing session scheduled (optional)

---

## Testing

### Comprehensive Testing:
- [ ] All WS modules tested
- [ ] BackstopJS suite executed
- [ ] Pa11y suite executed
- [ ] Cross-browser testing complete
- [ ] Performance testing complete

### Quality Gates:
- [ ] No critical bugs
- [ ] Accessibility: WCAG 2.1 AA compliant
- [ ] Performance: Lighthouse score > 90
- [ ] Browser compatibility: All tested browsers working
- [ ] Visual regression: All differences documented

---

## Deliverables

### Must Have:
- [ ] BackstopJS test suite upgraded
- [ ] Pa11y baseline established
- [ ] Cross-browser testing complete
- [ ] Performance report created
- [ ] All critical bugs fixed
- [ ] Documentation organized
- [ ] Next phase prepared

### Nice to Have:
- [ ] Migration guide for team
- [ ] FAQ document
- [ ] Presentation materials
- [ ] Optimization recommendations

---

## Risks

### Risk: Hidden Issues Discovered
**Likelihood:** Medium
**Impact:** Medium
**Mitigation:** Allocate time for unexpected issues, prioritize critical fixes

### Risk: Time Underestimate for Testing
**Likelihood:** Medium
**Impact:** Low
**Mitigation:** Focus on must-have deliverables first, defer nice-to-have if needed

---

## Notes

### Important:
- This is a consolidation sprint - focus on quality
- Fix issues before moving to next phase
- Ensure test infrastructure is robust
- Document everything for future reference

### Tips:
- Don't rush - quality is critical
- Test thoroughly before declaring complete
- Document issues even if not fixing (for later)
- Use this time to refine process for remaining sprints

---

## Sprint Review Checklist

At end of sprint, verify:
- [ ] All testing complete
- [ ] Test infrastructure upgraded
- [ ] Critical bugs fixed
- [ ] Documentation organized
- [ ] Next phase ready to start
- [ ] Team aligned on progress
- [ ] **Phase 2a complete (WS modules + testing)**

---

## Navigation

- **Previous:** [Sprint 6 - WS Other Modules](SPRINT_06_WS_Other_Modules.md)
- **Next:** Sprint 8 - LB Batch 1 (TBD)
- **Phase:** [Phase 2 - Component Migration](../phases/PHASE_2_COMPONENT_MIGRATION.md)
- **Overview:** [Executive Summary](../EXECUTIVE_SUMMARY.md)

---

**Sprint Status:** ⬜ Not Started
**Last Updated:** 2025-10-17
