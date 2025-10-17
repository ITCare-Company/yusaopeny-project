# Bootstrap 5 Migration - Testing Index

**Total Documents:** 4 testing documents
**Testing Strategy:** 3-tier progressive approach
**Current Status:** Documentation complete
**Last Updated:** 2025-10-17

---

## Quick Navigation

| Document | Purpose | Lines | Priority |
|----------|---------|-------|----------|
| [TESTING_OVERVIEW.md](TESTING_OVERVIEW.md) | Complete testing strategy | ~854 | ⭐⭐⭐ CRITICAL |
| [TESTING_VISUAL_REGRESSION.md](TESTING_VISUAL_REGRESSION.md) | BackstopJS setup & usage | ~1,009 | ⭐⭐⭐ CRITICAL |
| [TESTING_ACCESSIBILITY.md](TESTING_ACCESSIBILITY.md) | Pa11y, WCAG 2.2 AA | ~967 | ⭐⭐⭐ CRITICAL |
| [TESTING_PERFORMANCE.md](TESTING_PERFORMANCE.md) | Lighthouse, bundle size | ~1,136 | ⭐⭐ HIGH |

---

## Testing Strategy Overview

### 3-Tier Progressive Testing Approach

**Tier 1: Basic Testing (Per Module)**
- Build verification (Webpack compiles successfully)
- Visual spot-checks at 3 breakpoints
- Interactive component smoke tests
- Run during: All sprints, per module

**Tier 2: Standard Testing (Per Sprint/Batch)**
- Visual regression testing (BackstopJS, 10 scenarios)
- Accessibility testing (Pa11y, WCAG 2.2 AA)
- Functional testing (all interactive elements)
- Browser compatibility (Chrome, Firefox, Safari, Edge)
- Run during: End of each sprint

**Tier 3: Comprehensive Testing (Phase-End & Launch)**
- Full visual regression (all scenarios, all breakpoints)
- Comprehensive accessibility audit
- Performance testing (Lighthouse 90+)
- Cross-browser testing (including mobile browsers)
- Integration testing (all modules together)
- Security review (for forms, payment components)
- Run during: End of each phase, Sprint 22 (final testing)

**See:** [TESTING_OVERVIEW.md](TESTING_OVERVIEW.md) for complete details

---

## Testing Documents

### 1. Testing Overview

**Document:** [TESTING_OVERVIEW.md](TESTING_OVERVIEW.md)
**Lines:** ~854
**Status:** ✅ Complete

**Contents:**
- 3-tier testing strategy explained
- Testing timeline by phase/sprint
- Tools and setup instructions
- Test execution workflow
- Issue tracking and triage
- Success criteria per tier

**Key Sections:**
- **Tier Definitions:** When to use which testing level
- **Testing Schedule:** Per sprint, per phase, launch
- **Team Responsibilities:** Who runs which tests
- **Automation Strategy:** CI/CD integration
- **Issue Management:** Bug triage and prioritization

**Use This For:**
- Understanding overall testing approach
- Planning testing per sprint
- Setting up testing infrastructure (Sprint 1)
- Coordinating QA team activities

---

### 2. Visual Regression Testing

**Document:** [TESTING_VISUAL_REGRESSION.md](TESTING_VISUAL_REGRESSION.md)
**Lines:** ~1,009
**Status:** ✅ Complete

**Contents:**
- BackstopJS installation and configuration
- Scenario definition guide
- Baseline creation process
- Test execution and review
- Troubleshooting common issues
- CI/CD integration

**Key Sections:**
- **Installation:** Node.js, BackstopJS setup
- **Configuration:** backstop.json structure
- **Scenarios:** How to define test scenarios
- **Baseline Creation:** Pre-migration screenshots
- **Running Tests:** Commands and options
- **Reviewing Results:** Analyzing diffs
- **Approving Changes:** When diffs are intentional

**Example Configuration:**
```json
{
  "viewports": [
    { "label": "mobile", "width": 375, "height": 667 },
    { "label": "tablet", "width": 768, "height": 1024 },
    { "label": "desktop", "width": 1920, "height": 1080 }
  ],
  "scenarios": [
    {
      "label": "Homepage",
      "url": "http://yusaopeny.docksal.site",
      "selectors": ["body"]
    }
  ]
}
```

**Use This For:**
- Setting up BackstopJS (Sprint 1)
- Creating baselines before migration
- Running visual tests per module/sprint
- Analyzing and approving visual changes

---

### 3. Accessibility Testing

**Document:** [TESTING_ACCESSIBILITY.md](TESTING_ACCESSIBILITY.md)
**Lines:** ~967
**Status:** ✅ Complete

**Contents:**
- WCAG 2.2 Level AA requirements
- Pa11y installation and usage
- Automated testing setup
- Manual testing checklists
- Keyboard navigation testing
- Screen reader testing
- Color contrast verification
- Form accessibility

**Key Sections:**
- **WCAG 2.2 AA:** What it means and requirements
- **Pa11y Setup:** Installation and configuration
- **Automated Tests:** Running Pa11y on pages
- **Manual Testing:** What automation can't catch
- **Keyboard Navigation:** Tab order, focus, shortcuts
- **Screen Readers:** NVDA, JAWS, VoiceOver testing
- **Color Contrast:** Tools and requirements (4.5:1 normal, 3:1 large)
- **Common Issues:** Bootstrap 5 accessibility gotchas

**WCAG 2.2 AA Requirements:**
- Color contrast: 4.5:1 (normal text), 3:1 (large text, UI components)
- Keyboard navigation: All interactive elements accessible
- Focus indicators: Visible and clear
- Form labels: Proper label associations
- Alt text: All images have meaningful alternatives
- Semantic HTML: Proper heading hierarchy, landmarks

**Use This For:**
- Understanding accessibility requirements
- Setting up Pa11y (Sprint 1)
- Running accessibility tests per module/sprint
- Manual accessibility testing checklist
- Ensuring WCAG 2.2 AA compliance

---

### 4. Performance Testing

**Document:** [TESTING_PERFORMANCE.md](TESTING_PERFORMANCE.md)
**Lines:** ~1,136
**Status:** ✅ Complete

**Contents:**
- Lighthouse setup and usage
- Performance targets (Lighthouse 90+)
- Bundle size monitoring
- Core Web Vitals tracking
- JavaScript performance
- CSS optimization
- Image optimization
- Performance budgets

**Key Sections:**
- **Lighthouse:** Installation and running tests
- **Performance Targets:** Score 90+
- **Core Web Vitals:** LCP, FID, CLS metrics
- **Bundle Size:** Tracking and limits
- **Webpack Optimization:** Code splitting, tree shaking
- **CSS Optimization:** Unused CSS removal
- **JavaScript Optimization:** Lazy loading, deferring
- **Image Optimization:** Formats, lazy loading

**Performance Targets:**
- **Lighthouse Performance:** 90+
- **Lighthouse Accessibility:** 100
- **Lighthouse Best Practices:** 100
- **Lighthouse SEO:** 90+

**Core Web Vitals:**
- **LCP (Largest Contentful Paint):** < 2.5s
- **FID (First Input Delay):** < 100ms
- **CLS (Cumulative Layout Shift):** < 0.1

**Bundle Size Limits:**
- Total JavaScript: < 250KB gzipped
- Total CSS: < 50KB gzipped
- Bootstrap 5: ~22KB gzipped (CSS), ~12KB gzipped (JS)

**Use This For:**
- Setting up Lighthouse (Sprint 1)
- Monitoring bundle size growth
- Performance testing per sprint
- Optimizing slow modules
- Ensuring performance targets met

---

## Testing Timeline

### Sprint 1: Infrastructure Setup
- [ ] Install BackstopJS
- [ ] Install Pa11y
- [ ] Install Lighthouse
- [ ] Create baseline tests
- [ ] Document testing procedures

### Sprints 2-21: Per-Sprint Testing
- [ ] Run Tier 1 (Basic) tests per module
- [ ] Run Tier 2 (Standard) tests at sprint end
- [ ] Document issues and fixes
- [ ] Update baselines if intentional changes

### Sprint 7, 13, 17, 21: Phase-End Testing
- [ ] Run Tier 3 (Comprehensive) tests
- [ ] Full visual regression suite
- [ ] Complete accessibility audit
- [ ] Performance testing
- [ ] Integration testing

### Sprint 22: Comprehensive Testing
- [ ] Full site testing (all modules together)
- [ ] Complete visual regression (all pages)
- [ ] Complete accessibility audit (all pages)
- [ ] Performance testing (all pages)
- [ ] Cross-browser testing (all browsers)
- [ ] Security review (forms, payments)

### Sprint 23-24: Rollout Testing
- [ ] Demo environment testing
- [ ] Staging environment testing
- [ ] Small production site testing (Tier D)
- [ ] Monitor and fix issues
- [ ] Proceed to larger sites

---

## Testing Tools

### Required Tools

**Visual Regression:**
- BackstopJS (v6+)
- Node.js (LTS)
- Headless Chrome

**Accessibility:**
- Pa11y (v6+)
- axe-core (included in Pa11y)
- Manual testing tools:
  - NVDA (Windows screen reader)
  - JAWS (Windows screen reader)
  - VoiceOver (Mac/iOS screen reader)
  - Colour Contrast Analyser

**Performance:**
- Lighthouse (Chrome DevTools)
- Lighthouse CLI
- Webpack Bundle Analyzer
- Chrome DevTools Performance tab

### Optional Tools

**Cross-Browser Testing:**
- BrowserStack (paid)
- Sauce Labs (paid)
- Local browser testing (free)

**Automated Testing:**
- Cypress (E2E testing)
- Jest (unit testing)
- Behat (Drupal functional testing)

---

## Test Coverage Requirements

### Visual Regression Coverage

**Per Module:**
- All display modes (full, teaser, card, embedded)
- All interactive states (open/closed, active/inactive)
- All breakpoints (mobile, tablet, desktop)
- Minimum: 3 scenarios per module

**Per Sprint:**
- All modules in sprint
- Integration between modules
- Minimum: 10-20 scenarios per sprint

**Phase-End:**
- All modules in phase
- All pages using phase modules
- All breakpoints and states

### Accessibility Coverage

**Per Module:**
- All interactive components keyboard-accessible
- All form fields properly labeled
- All images have alt text
- Color contrast checked
- Minimum: Pa11y scan + manual check

**Per Sprint:**
- All modules in sprint pass Pa11y
- Manual testing of interactive components
- Keyboard navigation flow tested

**Phase-End:**
- Complete accessibility audit
- Manual testing of all workflows
- Screen reader testing

### Performance Coverage

**Per Module:**
- Bundle size measured
- Lighthouse score checked (if has demo page)

**Per Sprint:**
- Total bundle size for sprint modules
- Lighthouse scores for key pages

**Phase-End:**
- Complete performance audit
- All key pages meet targets
- Bundle size within budget

---

## Success Criteria

### Testing Infrastructure (Sprint 1):
- [ ] BackstopJS installed and configured
- [ ] Pa11y installed and configured
- [ ] Lighthouse available
- [ ] Baselines created for key pages
- [ ] Testing documentation complete

### Per-Sprint Testing:
- [ ] All modules pass Tier 1 (Basic) tests
- [ ] All modules pass Tier 2 (Standard) tests
- [ ] Visual regressions documented and approved
- [ ] Accessibility issues resolved (or documented)
- [ ] No JavaScript console errors

### Phase-End Testing:
- [ ] All modules pass Tier 3 (Comprehensive) tests
- [ ] Visual regression approved for entire phase
- [ ] Accessibility 100% WCAG 2.2 AA compliant
- [ ] Performance targets met (Lighthouse 90+)
- [ ] Integration testing passed

### Launch Testing (Sprint 22):
- [ ] Full site visual regression approved
- [ ] Full site accessibility audit passed
- [ ] Full site performance targets met
- [ ] All browsers tested and working
- [ ] Security review completed
- [ ] Ready for staged rollout

---

## Common Issues and Solutions

### Visual Regression Issues

**Issue:** Too many false positives (minor pixel differences)
**Solution:** Adjust BackstopJS `misMatchThreshold` setting

**Issue:** Dynamic content causes failures (timestamps, random images)
**Solution:** Use `removeSelectors` to exclude dynamic elements

**Issue:** Font rendering differences across systems
**Solution:** Use Docker container for consistent rendering

### Accessibility Issues

**Issue:** Missing alt text on images
**Solution:** Ensure all images have alt attributes (empty for decorative)

**Issue:** Low color contrast
**Solution:** Adjust colors to meet 4.5:1 (normal) or 3:1 (large) ratios

**Issue:** Form fields without labels
**Solution:** Add proper `<label>` elements or `aria-label` attributes

### Performance Issues

**Issue:** Large bundle size
**Solution:** Code splitting, tree shaking, remove unused dependencies

**Issue:** Slow page load
**Solution:** Lazy load images, defer non-critical JavaScript

**Issue:** Layout shift (poor CLS)
**Solution:** Reserve space for images, avoid injecting content above the fold

---

## Related Documents

**Core Documentation:**
- [README.md](../README.md) - Main documentation hub
- [QUICK_START.md](../QUICK_START.md) - Developer guide

**Phase Documentation:**
- [Phases Index](../phases/INDEX.md)
- Individual phase documents

**Sprint Documentation:**
- [Sprints Index](../sprints/INDEX.md)
- Individual sprint documents

**Reference Materials:**
- [Troubleshooting Guide](../reference/TROUBLESHOOTING.md)
- [Migration Checklist](../reference/MIGRATION_CHECKLIST_TEMPLATE.md)

---

## Navigation

- **← Back to:** [Main Documentation Hub](../README.md)
- **→ View Phases:** [Phases Index](../phases/INDEX.md)
- **→ View Sprints:** [Sprints Index](../sprints/INDEX.md)

### Direct Links to Testing Documents:
- [Testing Overview](TESTING_OVERVIEW.md) - Start here
- [Visual Regression Testing](TESTING_VISUAL_REGRESSION.md) - BackstopJS
- [Accessibility Testing](TESTING_ACCESSIBILITY.md) - Pa11y + WCAG 2.2
- [Performance Testing](TESTING_PERFORMANCE.md) - Lighthouse + optimization

---

**Index Version:** 1.0
**Last Updated:** 2025-10-17
**Testing Documents:** 4
**Documentation Status:** ✅ Complete
