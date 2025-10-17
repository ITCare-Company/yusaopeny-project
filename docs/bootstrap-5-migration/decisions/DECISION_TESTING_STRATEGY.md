# Decision: Bootstrap 5 Migration Testing Strategy

**Status:** Proposed
**Date:** 2025-10-17
**Decision Makers:** QA Lead, Development Team, Product Owner
**Scope:** All components affected by Bootstrap 4 to Bootstrap 5 migration

---

## Problem Statement

Migrating from Bootstrap 4 to Bootstrap 5 involves thousands of CSS class changes, JavaScript component updates, and potential DOM structure modifications across the entire Y USA Open YMCA platform. Without a comprehensive testing strategy, the migration risks:

### Migration Risks Without Proper Testing

1. **Visual Regressions:** Layout breaks, misaligned components, broken responsive designs
2. **Functional Failures:** JavaScript components not working (modals, dropdowns, tooltips)
3. **Accessibility Violations:** ARIA attributes broken, keyboard navigation failures
4. **Browser Inconsistencies:** Works in Chrome but broken in Safari/Firefox
5. **Mobile Breakage:** Desktop works but mobile layouts destroyed
6. **Performance Degradation:** Larger bundle sizes, slower page loads
7. **Integration Failures:** Third-party components conflicting with Bootstrap 5

### Scale of Testing Challenge

**Platform Scope:**
- **Modules:** 200+ custom and contrib modules
- **Themes:** 5+ themes (custom and contrib)
- **Page Types:** 30+ content types with unique layouts
- **Components:** 150+ paragraph types, blocks, and UI components
- **Views:** 100+ views with various display modes
- **Forms:** 80+ forms (content, user, configuration)
- **Admin Interfaces:** Extensive admin UI customization
- **Multi-site:** Testing must work across multiple site configurations

**Testing Complexity:**
- **Browsers:** Chrome, Firefox, Safari, Edge (latest 2 versions each)
- **Devices:** Desktop, tablet, mobile (iOS and Android)
- **Screen Sizes:** 320px to 4K (8+ breakpoints)
- **User Roles:** Anonymous, authenticated, content editor, admin
- **Content Variations:** Empty states, typical content, edge cases (very long text, many images)

### Business Constraints

- **Timeline Pressure:** Migration must complete within 6 months
- **Limited QA Resources:** 1-2 QA engineers, part-time developer testing
- **Production Uptime:** Cannot afford extended downtime or major bugs
- **User Impact:** 500+ YMCA sites depend on this distribution
- **Budget Constraints:** Cannot hire dedicated QA team for entire migration

---

## Testing Levels: Progressive Approach

Rather than applying the same exhaustive testing to every component, we propose a tiered approach based on **risk, usage, and complexity**.

### Tier System Overview

| Tier | Name | Coverage | Effort | When to Apply |
|------|------|----------|--------|---------------|
| **A** | Comprehensive | Visual + Functional + Accessibility + Performance + Cross-browser | 100% | Critical, high-traffic components |
| **B** | Standard | Visual + Functional + Basic accessibility | 75% | Moderate usage, moderate complexity |
| **C** | Basic | Visual regression + Smoke tests | 50% | Low-traffic, simple components |
| **D** | Minimal | Spot check + Manual review | 25% | Admin-only, rarely used components |

---

## Tier A: Comprehensive Testing

### When to Apply

**Criteria (must meet 2+ of these):**
- Used on >70% of pages across platform
- Critical to user workflows (registration, search, checkout)
- High complexity (JavaScript-heavy, interactive components)
- Accessibility-critical (forms, navigation, core content)
- Historical bug hotspot (frequent issues in past)

**Example Components:**
- Navigation menus (main nav, mobile nav)
- Forms (registration, contact, search)
- Modals (especially Activity Finder filters)
- Cards (program cards, event cards, news cards)
- Carousels and sliders
- Tables (pricing tables, schedule tables)
- Activity Finder (entire application)
- Location Finder
- Buttons (primary, secondary, all variants)
- Alerts and notifications
- Breadcrumbs
- Pagination

**Estimated Component Count:** 20-25 components

---

### Testing Activities

#### 1. Visual Regression Testing

**Tool:** Percy, Chromatic, or BackstopJS

**Coverage:**
- All viewport sizes (320px, 375px, 768px, 1024px, 1440px, 1920px)
- All component states (default, hover, focus, active, disabled, error)
- All color schemes (default, high contrast if applicable)
- All content variations (empty, typical, edge cases)

**Process:**
1. Capture baseline screenshots in Bootstrap 4
2. Migrate component to Bootstrap 5
3. Capture new screenshots
4. Review diffs, approve or fix
5. Update baseline

**Example Test Cases:**
```javascript
// Percy example
describe('Navigation Component', () => {
  it('renders correctly on mobile', async () => {
    await page.goto('/');
    await page.setViewport({ width: 375, height: 667 });
    await percySnapshot(page, 'Navigation - Mobile - Default');

    await page.click('.navbar-toggler');
    await percySnapshot(page, 'Navigation - Mobile - Expanded');
  });

  it('renders correctly on desktop', async () => {
    await page.goto('/');
    await page.setViewport({ width: 1440, height: 900 });
    await percySnapshot(page, 'Navigation - Desktop - Default');

    await page.hover('.nav-item.dropdown');
    await percySnapshot(page, 'Navigation - Desktop - Dropdown Hover');
  });
});
```

**Acceptance Criteria:**
- Zero unintended visual changes
- All intentional changes documented and approved
- All viewports pass

---

#### 2. Functional Testing

**Tool:** Behat (Drupal standard), Playwright, or Cypress

**Coverage:**
- All user interactions (clicks, hovers, keyboard navigation)
- All component states and transitions
- Form validation and submission
- AJAX interactions
- Error handling
- Edge cases

**Example Test Cases:**
```gherkin
# Behat example - Modal functionality
Feature: Bootstrap 5 Modal Component
  As a user
  I want to interact with modals
  So I can view additional content without leaving the page

  @javascript
  Scenario: Open modal by clicking button
    Given I am on "/programs"
    When I click "Learn More" in the "Swimming" program card
    Then I should see a modal with title "Swimming Program Details"
    And the modal should have a close button
    And the page behind the modal should be dimmed

  @javascript @accessibility
  Scenario: Close modal with keyboard
    Given I am on "/programs"
    And I opened the "Swimming" program modal
    When I press the "Escape" key
    Then the modal should close
    And focus should return to the "Learn More" button

  @javascript
  Scenario: Prevent page scroll when modal open
    Given I am on "/programs"
    When I open the "Swimming" program modal
    Then the page body should have class "modal-open"
    And scrolling should be disabled on the page body

  @javascript
  Scenario: Multiple modals (stacking)
    Given I am on "/programs"
    When I open the "Swimming" program modal
    And I click "View Schedule" in the modal
    Then I should see a second modal with schedule details
    And the first modal should still be visible behind it
    When I close the schedule modal
    Then I should see the "Swimming" program modal again
```

**Playwright Example:**
```javascript
test.describe('Bootstrap 5 Dropdown', () => {
  test('opens on click and closes on outside click', async ({ page }) => {
    await page.goto('/');

    // Dropdown should be closed initially
    const dropdown = page.locator('.dropdown-menu');
    await expect(dropdown).not.toBeVisible();

    // Open dropdown
    await page.click('.dropdown-toggle');
    await expect(dropdown).toBeVisible();

    // Close by clicking outside
    await page.click('body', { position: { x: 0, y: 0 } });
    await expect(dropdown).not.toBeVisible();
  });

  test('keyboard navigation works', async ({ page }) => {
    await page.goto('/');

    // Focus dropdown toggle with keyboard
    await page.keyboard.press('Tab');
    await page.keyboard.press('Tab'); // Navigate to dropdown

    // Open with Enter
    await page.keyboard.press('Enter');
    const dropdown = page.locator('.dropdown-menu');
    await expect(dropdown).toBeVisible();

    // Navigate menu items with arrow keys
    await page.keyboard.press('ArrowDown');
    await expect(page.locator('.dropdown-item:first-child')).toBeFocused();

    // Close with Escape
    await page.keyboard.press('Escape');
    await expect(dropdown).not.toBeVisible();
  });
});
```

**Acceptance Criteria:**
- 100% of user paths tested
- All interactions work as expected
- No JavaScript console errors
- Performance within acceptable limits (<100ms for interactions)

---

#### 3. Accessibility Testing

**Tools:** axe-core, WAVE, Lighthouse, manual screen reader testing

**Coverage:**
- WCAG 2.1 AA compliance (minimum)
- Keyboard navigation (all interactive elements reachable and usable)
- Screen reader compatibility (NVDA, JAWS, VoiceOver)
- Focus management (visible focus indicators, logical tab order)
- ARIA attributes (correct roles, states, properties)
- Color contrast (4.5:1 for text, 3:1 for UI components)
- Semantic HTML (headings, landmarks, lists)

**Automated Testing:**
```javascript
// axe-core integration
import { injectAxe, checkA11y } from 'axe-playwright';

test.describe('Accessibility - Navigation', () => {
  test.beforeEach(async ({ page }) => {
    await page.goto('/');
    await injectAxe(page);
  });

  test('main navigation is accessible', async ({ page }) => {
    await checkA11y(page, '.main-navigation', {
      detailedReport: true,
      detailedReportOptions: { html: true }
    });
  });

  test('mobile navigation is accessible', async ({ page }) => {
    await page.setViewport({ width: 375, height: 667 });
    await page.click('.navbar-toggler');
    await checkA11y(page, '.navbar-collapse', {
      detailedReport: true
    });
  });
});
```

**Manual Testing Checklist:**
```markdown
## Screen Reader Testing
- [ ] Component announced correctly (type, role, label)
- [ ] All interactive elements announced
- [ ] State changes announced (expanded/collapsed, selected/unselected)
- [ ] Error messages announced
- [ ] Loading states announced
- [ ] Dynamic content changes announced

## Keyboard Testing
- [ ] All interactive elements keyboard accessible
- [ ] Logical tab order
- [ ] Visible focus indicators (3px outline, high contrast)
- [ ] Enter/Space activate buttons
- [ ] Arrow keys navigate menus/lists
- [ ] Escape closes modals/dropdowns
- [ ] No keyboard traps

## Focus Management
- [ ] Focus moves logically through page
- [ ] Focus returns to trigger after modal close
- [ ] Focus trapped inside modal when open
- [ ] Skip links work correctly
- [ ] Focus visible on all interactive elements
```

**Acceptance Criteria:**
- Zero WCAG 2.1 AA violations (axe-core)
- All keyboard interactions work
- Screen reader testing passes on 3 major readers (NVDA, JAWS, VoiceOver)
- Focus indicators meet 3px minimum and high contrast
- No accessibility regressions from Bootstrap 4 version

---

#### 4. Performance Testing

**Tools:** Lighthouse CI, WebPageTest, Speedcurve, Bundle Analyzer

**Metrics:**
- First Contentful Paint (FCP): <1.5s
- Largest Contentful Paint (LCP): <2.5s
- Time to Interactive (TTI): <3.5s
- Total Blocking Time (TBT): <200ms
- Cumulative Layout Shift (CLS): <0.1
- Bundle size: No more than 10% increase from Bootstrap 4

**Testing:**
```javascript
// Lighthouse CI configuration
// lighthouserc.js
module.exports = {
  ci: {
    collect: {
      url: [
        'http://localhost:8080/',
        'http://localhost:8080/programs',
        'http://localhost:8080/locations',
        'http://localhost:8080/activity-finder'
      ],
      numberOfRuns: 3
    },
    assert: {
      assertions: {
        'first-contentful-paint': ['error', { maxNumericValue: 1500 }],
        'largest-contentful-paint': ['error', { maxNumericValue: 2500 }],
        'interactive': ['error', { maxNumericValue: 3500 }],
        'total-blocking-time': ['error', { maxNumericValue: 200 }],
        'cumulative-layout-shift': ['error', { maxNumericValue: 0.1 }],
        'categories:performance': ['error', { minScore: 0.9 }],
        'categories:accessibility': ['error', { minScore: 0.95 }]
      }
    }
  }
};
```

**Bundle Analysis:**
```bash
# Compare Bootstrap 4 vs Bootstrap 5 bundle sizes
webpack-bundle-analyzer stats-bs4.json
webpack-bundle-analyzer stats-bs5.json

# Expected changes:
# - Bootstrap CSS: ~150KB (BS4) → ~160KB (BS5) [+7%]
# - Bootstrap JS: ~60KB (BS4) → ~55KB (BS5) [-8%]
# - jQuery: ~90KB (BS4) → 0KB (BS5) [-100%]
# - Total: ~300KB (BS4) → ~215KB (BS5) [-28%]
```

**Acceptance Criteria:**
- All Core Web Vitals in "Good" range
- No performance regression on key user paths
- Bundle size reduced by 20%+ (due to jQuery removal)
- Lighthouse performance score >90

---

#### 5. Cross-Browser Testing

**Tools:** BrowserStack, Sauce Labs, or manual testing

**Browser Matrix:**
| Browser | Versions | Priority | Notes |
|---------|----------|----------|-------|
| Chrome | Latest 2 | P0 | Most users |
| Firefox | Latest 2 | P0 | Second most users |
| Safari | Latest 2 | P0 | iOS users |
| Edge | Latest 2 | P1 | Chromium-based |
| Chrome Android | Latest | P0 | Mobile users |
| Safari iOS | Latest 2 | P0 | iPhone users |

**Testing Approach:**
```javascript
// Playwright cross-browser example
const { chromium, firefox, webkit } = require('playwright');

const browsers = [
  { name: 'chromium', instance: chromium },
  { name: 'firefox', instance: firefox },
  { name: 'webkit', instance: webkit }
];

for (const { name, instance } of browsers) {
  test.describe(`${name} - Navigation`, () => {
    let browser, page;

    test.beforeAll(async () => {
      browser = await instance.launch();
      page = await browser.newPage();
    });

    test.afterAll(async () => {
      await browser.close();
    });

    test('dropdown works correctly', async () => {
      await page.goto('/');
      await page.click('.dropdown-toggle');
      const dropdown = page.locator('.dropdown-menu');
      await expect(dropdown).toBeVisible();
    });
  });
}
```

**Acceptance Criteria:**
- 100% functionality on all P0 browsers
- 95%+ functionality on P1 browsers (graceful degradation acceptable)
- No browser-specific bugs

---

#### 6. Responsive Design Testing

**Breakpoints:**
- **Mobile:** 320px, 375px, 414px
- **Tablet:** 768px, 1024px
- **Desktop:** 1280px, 1440px, 1920px

**Testing Checklist:**
```markdown
## Mobile (320-767px)
- [ ] Content readable without horizontal scroll
- [ ] Touch targets minimum 44x44px
- [ ] Navigation collapses to hamburger menu
- [ ] Forms usable with on-screen keyboard
- [ ] Images scale appropriately
- [ ] Text remains readable (min 16px)

## Tablet (768-1023px)
- [ ] Layout adapts appropriately
- [ ] Touch and mouse both work
- [ ] Navigation works in tablet mode
- [ ] Multi-column layouts adjust

## Desktop (1024px+)
- [ ] Full desktop layout displays
- [ ] Hover states work
- [ ] Multi-column layouts fully expanded
- [ ] Content doesn't stretch too wide (max-width)
```

**Automated Testing:**
```javascript
const viewports = [
  { name: 'Mobile Small', width: 320, height: 568 },
  { name: 'Mobile Medium', width: 375, height: 667 },
  { name: 'Mobile Large', width: 414, height: 896 },
  { name: 'Tablet', width: 768, height: 1024 },
  { name: 'Desktop Small', width: 1280, height: 800 },
  { name: 'Desktop Large', width: 1920, height: 1080 }
];

for (const viewport of viewports) {
  test(`Navigation responsive - ${viewport.name}`, async ({ page }) => {
    await page.setViewport(viewport);
    await page.goto('/');
    await percySnapshot(page, `Navigation - ${viewport.name}`);
  });
}
```

**Acceptance Criteria:**
- All breakpoints tested and approved
- No horizontal scroll at any viewport
- Touch targets meet 44x44px minimum on mobile
- Content readable at all sizes

---

## Tier B: Standard Testing

### When to Apply

**Criteria:**
- Moderate usage (on 30-70% of pages)
- Medium complexity (some JavaScript, moderate styling)
- Important but not critical to core workflows
- Standard accessibility requirements

**Example Components:**
- Blog post layouts
- News article layouts
- Staff directory listings
- Testimonials
- FAQ accordions
- Embedded videos
- Social media widgets
- Sidebar widgets
- Footer components
- Secondary navigation
- Breadcrumbs (non-critical pages)

**Estimated Component Count:** 40-50 components

---

### Testing Activities

#### 1. Visual Regression Testing

**Coverage:**
- Key viewport sizes (375px, 768px, 1440px)
- Primary states (default, error)
- Typical content only

**Reduced Scope:**
- Skip hover/focus states (manual check only)
- Skip edge cases (very long text, etc.)
- One color scheme only

---

#### 2. Functional Testing

**Coverage:**
- Happy path user interactions
- Basic error handling
- Key AJAX interactions

**Reduced Scope:**
- Skip edge cases
- Skip complex state transitions
- Manual testing acceptable for some scenarios

**Example:**
```gherkin
Feature: Accordion Component (Standard Testing)

  Scenario: Expand and collapse accordion item
    Given I am on "/faq"
    When I click the first accordion header
    Then the first accordion panel should expand
    When I click the first accordion header again
    Then the first accordion panel should collapse

  # Skip complex scenarios like:
  # - Multiple accordions open simultaneously
  # - Nested accordions
  # - Accordion with AJAX-loaded content
```

---

#### 3. Accessibility Testing

**Coverage:**
- Automated axe-core testing
- Basic keyboard navigation check
- Focus indicator verification

**Reduced Scope:**
- Skip comprehensive screen reader testing
- Skip manual ARIA verification (rely on automated tools)
- WCAG 2.1 AA compliance (automated only)

**Example:**
```javascript
test('Accordion accessibility - automated only', async ({ page }) => {
  await page.goto('/faq');
  await injectAxe(page);

  // Automated check only
  await checkA11y(page, '.accordion');

  // Basic keyboard check
  await page.keyboard.press('Tab');
  await page.keyboard.press('Enter');
  const panel = page.locator('.accordion-collapse');
  await expect(panel).toBeVisible();
});
```

---

#### 4. Performance Testing

**Coverage:**
- Lighthouse audit on one representative page
- Bundle size check

**Reduced Scope:**
- No detailed WebPageTest analysis
- No Real User Monitoring
- No load testing

---

#### 5. Cross-Browser Testing

**Coverage:**
- Chrome and Safari only (most common)
- Desktop and mobile

**Reduced Scope:**
- Skip Firefox and Edge (unless component known to have issues)
- Accept minor visual differences

---

#### 6. Responsive Design Testing

**Coverage:**
- Mobile (375px), tablet (768px), desktop (1440px)

**Reduced Scope:**
- Skip extreme sizes (320px, 1920px)
- Accept minor layout quirks at edge sizes

---

## Tier C: Basic Testing

### When to Apply

**Criteria:**
- Low usage (<30% of pages)
- Low complexity (mostly CSS, minimal JavaScript)
- Non-critical functionality
- Limited accessibility requirements

**Example Components:**
- Badge components
- Labels and tags
- Tooltips (non-critical)
- Popovers (supplementary info)
- List groups
- Progress bars
- Spinners
- Dividers
- Print styles
- Utility classes

**Estimated Component Count:** 60-80 components

---

### Testing Activities

#### 1. Visual Regression Testing

**Coverage:**
- Desktop only (1440px)
- Default state only
- Typical content only

**Process:**
- Capture one screenshot before/after
- Quick visual review
- Approve or fix obvious issues

---

#### 2. Smoke Testing

**Coverage:**
- Basic "does it render" test
- One quick interaction test

**Example:**
```javascript
test('Badge renders correctly', async ({ page }) => {
  await page.goto('/test-components');
  const badge = page.locator('.badge');
  await expect(badge).toBeVisible();
  await expect(badge).toHaveClass(/badge-primary/);
});
```

---

#### 3. Automated Accessibility Check

**Coverage:**
- One axe-core automated scan

**No Manual Testing:**
- Trust automated tools
- Fix only critical violations

---

#### 4. Spot Check Performance

**Coverage:**
- Include in bundle size analysis
- No dedicated performance testing

---

#### 5. Chrome Desktop Only

**Coverage:**
- Test in Chrome desktop only
- Assume cross-browser compatibility (Bootstrap handles it)

---

#### 6. Responsive Spot Check

**Coverage:**
- Quick manual check at mobile and desktop
- No screenshots or formal testing

---

## Tier D: Minimal Testing

### When to Apply

**Criteria:**
- Admin-only interfaces
- Rarely used features (<5% of users)
- Very simple components
- Low risk of user impact

**Example Components:**
- Admin form elements (non-content)
- Configuration pages
- Developer tools
- Status pages
- Diagnostic components
- Internal documentation pages
- Deprecated components (to be removed)

**Estimated Component Count:** 30-40 components

---

### Testing Activities

#### Manual Review Only

**Process:**
1. Developer tests during implementation
2. Code review by peer
3. Quick manual spot check by QA
4. No automated tests required

**Checklist:**
- [ ] Component renders without errors
- [ ] Basic functionality works
- [ ] No obvious visual breaks
- [ ] No console errors

---

## When to Upgrade Testing Levels

### Trigger for C → B Upgrade

**Upgrade if:**
- Usage increases (component now on >30% of pages)
- JavaScript added (component becomes interactive)
- Accessibility issues discovered
- User-reported bugs

---

### Trigger for B → A Upgrade

**Upgrade if:**
- Usage becomes critical (>70% of pages)
- Component becomes part of core user workflow
- Accessibility becomes critical
- Historical pattern of bugs
- Performance issues discovered

---

### Trigger for D → C Upgrade

**Upgrade if:**
- Component moves from admin to public-facing
- Usage increases
- Complexity increases

---

## Tools Selection Rationale

### Visual Regression: Percy (Recommended)

**Why Percy:**
- Excellent Drupal/PHP support
- Automatic screenshot comparison
- Good diff visualization
- Integrates with CI/CD
- Reasonable pricing ($349/month for 35k snapshots)

**Alternatives:**
- **Chromatic:** Great for Storybook, but we don't use Storybook extensively
- **BackstopJS:** Free, but requires more setup and maintenance
- **Applitools:** Expensive ($199/month), overkill for our needs

**Decision:** Percy for Tier A components, BackstopJS for Tier B/C

---

### Functional Testing: Behat + Playwright

**Why Both:**
- **Behat:** Already used in Drupal ecosystem, team familiar, good for Drupal-specific testing
- **Playwright:** Modern, fast, better for JavaScript-heavy components (Activity Finder)

**Division:**
- Behat: Drupal content, forms, views, server-side functionality
- Playwright: Activity Finder, interactive JavaScript components, client-side behavior

**Alternatives Considered:**
- **Cypress:** Great tool, but similar to Playwright; no need for two modern tools
- **Selenium:** Outdated, slower, more flaky

---

### Accessibility Testing: axe-core + Manual

**Why axe-core:**
- Industry standard
- Catches 57% of WCAG issues (according to Deque)
- Easy integration (Playwright, Behat, browser extension)
- Free and open source

**Why Manual Testing Still Needed:**
- Automated tools miss 43% of issues
- Screen reader testing cannot be automated reliably
- Keyboard navigation needs human verification
- Context-dependent issues require judgment

**Tools:**
- Automated: axe-core
- Browser extension: axe DevTools
- Screen readers: NVDA (Windows), JAWS (Windows), VoiceOver (macOS)

---

### Performance Testing: Lighthouse CI

**Why Lighthouse CI:**
- Free
- Industry-standard metrics (Core Web Vitals)
- Easy CI/CD integration
- Comprehensive (performance, accessibility, SEO)

**Supplementary Tools:**
- **WebPageTest:** For detailed waterfall analysis (Tier A components only)
- **Speedcurve:** For long-term performance tracking (after migration)
- **webpack-bundle-analyzer:** For bundle size tracking

---

### Cross-Browser Testing: BrowserStack

**Why BrowserStack:**
- Real devices (not emulators)
- Wide browser/OS coverage
- Integrates with Playwright
- Reasonable pricing ($299/month for team plan)

**Alternatives:**
- **Sauce Labs:** Similar, but more expensive
- **Local device lab:** Expensive to maintain, limited coverage
- **Manual testing only:** Too time-consuming

**Decision:** BrowserStack for Tier A, manual local testing for Tier B/C

---

## Resource Requirements

### Team Composition

**Required Roles:**
- **QA Lead (1):** Test strategy, tool selection, quality gates - 100% dedicated
- **QA Engineers (2):** Test execution, automation, bug triage - 100% dedicated
- **Developers (6):** Component migration, fix bugs, write tests - 50% on testing
- **Accessibility Specialist (1):** Manual a11y testing, remediation - 25% dedicated

**Total FTE:** ~5 FTE for 6-month migration

---

### Tool Costs

| Tool | Cost/Month | Annual | Tier Usage |
|------|------------|--------|------------|
| Percy | $349 | $4,188 | A, B |
| BrowserStack | $299 | $3,588 | A |
| Playwright | $0 | $0 | A, B, C |
| Behat | $0 | $0 | A, B, C |
| axe-core | $0 | $0 | A, B, C |
| Lighthouse CI | $0 | $0 | A, B |
| **Total** | **$648** | **$7,776** | |

**Budget:** ~$8,000/year for tools

---

### Time Estimates

**Per Component Testing Time:**

| Tier | Time/Component | Components | Total Time |
|------|----------------|------------|------------|
| A - Comprehensive | 16 hours | 25 | 400 hours |
| B - Standard | 6 hours | 50 | 300 hours |
| C - Basic | 2 hours | 70 | 140 hours |
| D - Minimal | 30 minutes | 40 | 20 hours |
| **Total** | | **185** | **860 hours** |

**Additional Time:**
- Test infrastructure setup: 80 hours
- CI/CD integration: 40 hours
- Documentation: 40 hours
- Bug fixes (estimated 20% of migration): 200 hours
- **Total Testing Effort:** ~1,220 hours (7 person-months)

---

## Testing Workflow

### Pre-Migration

1. **Component Inventory:** Catalog all components, assign tiers
2. **Baseline Capture:** Capture Bootstrap 4 screenshots, performance metrics
3. **Test Suite Setup:** Configure Percy, Playwright, Behat, axe-core
4. **CI/CD Integration:** Add quality gates to PR pipeline

---

### During Migration

1. **Component Migration:** Developer migrates component to Bootstrap 5
2. **Self-Test:** Developer runs local tests, fixes obvious issues
3. **Pull Request:** Developer creates PR with migration
4. **Automated Tests:** CI runs appropriate tier tests
5. **Code Review:** Peer reviews code and test results
6. **QA Review:** QA engineer reviews visual diffs, runs manual tests
7. **Approval:** PR merged only if all tests pass

---

### Post-Migration

1. **Regression Testing:** Full platform regression test
2. **Performance Audit:** Comprehensive performance comparison
3. **Accessibility Audit:** Final WCAG 2.1 AA compliance check
4. **User Acceptance Testing:** Internal users test key workflows
5. **Soft Launch:** Deploy to staging, monitor for issues
6. **Production Deploy:** Deploy to production with monitoring
7. **Post-Launch Monitoring:** Track errors, performance, user feedback

---

## Quality Gates (CI/CD)

### Pull Request Checks

**All PRs Must Pass:**
- Linting (ESLint, Stylelint)
- Unit tests (PHPUnit, Jest)
- Component tier tests (based on tier)

**Tier-Specific Gates:**

**Tier A:**
- [ ] Visual regression (Percy) - zero unapproved diffs
- [ ] Functional tests (Behat/Playwright) - 100% pass
- [ ] Accessibility (axe-core) - zero violations
- [ ] Performance (Lighthouse) - scores >90
- [ ] Cross-browser (BrowserStack) - all P0 browsers pass

**Tier B:**
- [ ] Visual regression - zero critical diffs
- [ ] Functional tests - 100% pass
- [ ] Accessibility - zero critical violations
- [ ] Performance - no regressions >10%

**Tier C:**
- [ ] Smoke tests - 100% pass
- [ ] Accessibility - zero critical violations

**Tier D:**
- [ ] Code review approval
- [ ] Manual spot check

---

## Success Criteria

### Overall Migration Success

**Technical Criteria:**
- [ ] 100% of components migrated (185 components)
- [ ] Zero critical visual regressions
- [ ] Zero critical functional bugs
- [ ] Zero WCAG 2.1 AA violations (Tier A)
- [ ] Performance improved by 15%+ (or no regression)
- [ ] All cross-browser tests pass

**Process Criteria:**
- [ ] Testing documentation complete
- [ ] All tests automated (where appropriate)
- [ ] CI/CD quality gates functional
- [ ] Team trained on testing tools

**Business Criteria:**
- [ ] Zero customer-reported critical bugs post-launch
- [ ] Support tickets unchanged or reduced
- [ ] User satisfaction maintained or improved
- [ ] Timeline met (6 months)

---

### Per-Tier Success Criteria

**Tier A:**
- 100% test coverage
- Zero regressions
- Full documentation

**Tier B:**
- 90% test coverage
- <5 minor issues post-launch
- Basic documentation

**Tier C:**
- Smoke tests pass
- <10 minor issues post-launch
- Minimal documentation

**Tier D:**
- No critical issues
- Issues addressed within 2 weeks

---

## Risk Management

### Risk: Insufficient Testing Time

**Likelihood:** High
**Impact:** High

**Mitigation:**
- Build 20% buffer into timeline
- Prioritize Tier A components first
- Accept lower coverage on Tier D if needed
- Add QA contractors if falling behind

**Contingency:**
- Reduce Tier C to Tier D testing if necessary
- Extend timeline by 1 month
- Deploy in phases (core components first)

---

### Risk: Tool License Costs

**Likelihood:** Low
**Impact:** Medium

**Mitigation:**
- Budget approved upfront
- Use free alternatives where possible (BackstopJS, Playwright)
- Negotiate annual discounts

**Contingency:**
- Substitute Percy with BackstopJS if budget cut
- Use free BrowserStack open source plan
- Increase manual testing time

---

### Risk: False Positives (Flaky Tests)

**Likelihood:** Medium
**Impact:** Medium

**Mitigation:**
- Use stable, deterministic tests
- Wait for animations to complete
- Use Percy's anti-flicker technology
- Implement retry logic for network-dependent tests

**Contingency:**
- Quarantine flaky tests
- Fix or disable tests that can't be stabilized
- Increase manual testing for problematic components

---

### Risk: Team Learning Curve

**Likelihood:** Medium
**Impact:** Medium

**Mitigation:**
- Training sessions for all tools (Percy, Playwright, axe-core)
- Pair programming during initial tests
- Clear documentation and examples
- Office hours for Q&A

**Contingency:**
- Extend timeline for training
- Hire contractor with tool expertise
- Start with simpler tests, increase complexity gradually

---

## Decision

**Status:** Pending approval
**Recommended Strategy:** Progressive tiered testing (A/B/C/D)
**Timeline:** 6 months (includes setup, execution, post-launch monitoring)
**Budget:** $8,000 tools + 7 person-months QA effort

**Next Steps:**

1. Component inventory and tier assignment (1 week)
2. Tool procurement and setup (2 weeks)
3. Team training (1 week)
4. Begin Tier A testing (ongoing)

**Approval Required By:**
- [ ] QA Lead
- [ ] Technical Lead
- [ ] Product Owner
- [ ] Budget Approval (Finance/Product Owner)

---

## References

- [Bootstrap 5 Testing Guide](https://getbootstrap.com/docs/5.3/getting-started/testing/)
- [Percy Documentation](https://docs.percy.io/)
- [Playwright Documentation](https://playwright.dev/)
- [Behat Documentation](https://docs.behat.org/)
- [axe-core Documentation](https://github.com/dequelabs/axe-core)
- [WCAG 2.1 Guidelines](https://www.w3.org/WAI/WCAG21/quickref/)
- [Web.dev Performance](https://web.dev/performance/)
- [Drupal Testing Documentation](https://www.drupal.org/docs/testing)

---

**Document History:**

| Version | Date | Author | Changes |
|---------|------|--------|---------|
| 1.0 | 2025-10-17 | QA Lead + Development Team | Initial decision document |
