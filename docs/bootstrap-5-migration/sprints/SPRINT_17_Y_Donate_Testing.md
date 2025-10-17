# Sprint 17: Donation Module & Phase 4 Integration Testing

**Phase:** [Phase 4 - Content Types](../phases/PHASE_4_CONTENT_TYPES.md)
**Resources:** 1 Developer + QA Support
**Status:** Not Started

---

## Sprint Goal

Migrate donation modules to Bootstrap 5 and complete comprehensive Phase 4 integration testing. Verify all 10 content type modules work together with Layout Builder modules. Make GO/NO-GO decision for Phase 5.

---

## Modules in This Sprint

### Primary Modules (2):
1. **y_donate** - Donation content type
   - Path: `docroot/modules/contrib/y_donate`
   - Donation pages and forms
   - Payment integration styling

2. **lb_donate** - Donation Layout Builder integration
   - Path: `docroot/modules/contrib/y_donate/modules/lb_donate`
   - Donation component for Layout Builder
   - Integration with Phase 3 LB modules

---

## Tasks

### Task 1: Migrate y_donate Module
**Owner:** Developer
**Priority:** CRITICAL

**Actions:**

**1.1 Audit donation module:**
```bash
cd docroot/modules/contrib/y_donate
grep -r "bootstrap" .
find . -name "*.twig"
grep -r "form" .
grep -r "payment" .
```

**1.2 Update donation page templates:**
```twig
{# Donation page #}
<article class="donate-page">
  <div class="donate-header">
    <h1>{{ title }}</h1>
    <p class="lead">{{ description }}</p>
  </div>

  <div class="donate-form-wrapper">
    {{ donation_form }}
  </div>
</article>
```

**1.3 Update donation form templates:**
```twig
{# Donation form #}
<div class="donation-form">
  {# Amount selection #}
  <div class="amount-selection">
    <div class="btn-group" role="group">
      <input type="radio" class="btn-check" name="amount" id="amount25" value="25">
      <label class="btn btn-outline-primary" for="amount25">$25</label>

      <input type="radio" class="btn-check" name="amount" id="amount50" value="50">
      <label class="btn btn-outline-primary" for="amount50">$50</label>

      <input type="radio" class="btn-check" name="amount" id="amount100" value="100">
      <label class="btn btn-outline-primary" for="amount100">$100</label>
    </div>
  </div>

  {# Frequency selection #}
  <div class="frequency-selection">
    <div class="btn-group" role="group">
      <input type="radio" class="btn-check" name="frequency" id="once" value="once">
      <label class="btn btn-outline-secondary" for="once">One-time</label>

      <input type="radio" class="btn-check" name="frequency" id="monthly" value="monthly">
      <label class="btn btn-outline-secondary" for="monthly">Monthly</label>
    </div>
  </div>

  {# Payment fields #}
  <div class="payment-fields">
    <div class="mb-3">
      <label for="cardName" class="form-label">Name on Card</label>
      <input type="text" class="form-control" id="cardName">
    </div>

    <div class="mb-3">
      <label for="cardNumber" class="form-label">Card Number</label>
      <input type="text" class="form-control" id="cardNumber">
    </div>

    <div class="row">
      <div class="col-md-6 mb-3">
        <label for="expiry" class="form-label">Expiry Date</label>
        <input type="text" class="form-control" id="expiry" placeholder="MM/YY">
      </div>
      <div class="col-md-6 mb-3">
        <label for="cvv" class="form-label">CVV</label>
        <input type="text" class="form-control" id="cvv">
      </div>
    </div>
  </div>

  {# Submit button #}
  <button type="submit" class="btn btn-primary btn-lg w-100">
    Complete Donation
  </button>
</div>
```

**1.4 Update donation form styling:**
```scss
@import "bootstrap/scss/functions";
@import "bootstrap/scss/variables";

.donation-form {
  // Update Bootstrap 5 form classes

  .amount-selection {
    margin-bottom: $spacer * 2;
  }

  .btn-check {
    // Bootstrap 5 radio button styling
  }

  .payment-fields {
    // Payment form styling
    // Ensure PCI compliance visual standards
  }
}

// Update form validation states
.was-validated .form-control:invalid {
  // Bootstrap 5 validation styles
}
```

**1.5 Update donation confirmation template:**
```twig
{# Donation confirmation page #}
<div class="donation-confirmation">
  <div class="alert alert-success" role="alert">
    <h4 class="alert-heading">Thank You!</h4>
    <p>Your donation of ${{ amount }} has been received.</p>
  </div>

  <div class="card">
    <div class="card-body">
      <h5 class="card-title">Donation Details</h5>
      {# Donation receipt details #}
    </div>
  </div>
</div>
```

**Deliverable:** Migrated y_donate module

**Acceptance Criteria:**
- [ ] Donation pages display correctly
- [ ] Donation forms styled correctly
- [ ] Form validation works
- [ ] Payment integration styling maintained (no logic changes)
- [ ] Confirmation page works
- [ ] Bootstrap 5 classes used
- [ ] SCSS compiles without errors

---

### Task 2: Migrate lb_donate Module
**Owner:** Developer
**Priority:** HIGH

**Actions:**

**2.1 Update lb_donate component:**
```twig
{# Layout Builder donation component #}
<div class="lb-donate-block">
  <div class="donate-cta">
    <h3>{{ settings.title }}</h3>
    <p>{{ settings.description }}</p>

    {# Quick donate buttons #}
    <div class="quick-donate-buttons">
      <a href="/donate?amount=25" class="btn btn-primary">
        Donate $25
      </a>
      <a href="/donate?amount=50" class="btn btn-primary">
        Donate $50
      </a>
      <a href="/donate?amount=100" class="btn btn-primary">
        Donate $100
      </a>
    </div>

    <a href="/donate" class="btn btn-link">
      Custom Amount
    </a>
  </div>
</div>
```

**2.2 Update lb_donate styling:**
```scss
.lb-donate-block {
  // Update Bootstrap 5 classes
  // Match LB component styling patterns from Phase 3

  .quick-donate-buttons {
    display: flex;
    gap: $spacer;
    flex-wrap: wrap;
  }
}
```

**2.3 Test lb_donate in Layout Builder:**
- [ ] Add lb_donate to landing page
- [ ] Configure lb_donate settings
- [ ] Test donation links from component
- [ ] Test component display
- [ ] Test component responsive behavior

**2.4 Test lb_donate with other LB components:**
- [ ] lb_donate + lb_hero
- [ ] lb_donate + lb_modal (donate in modal)
- [ ] lb_donate + lb_testimonials
- [ ] Multiple lb_donate on same page

**Deliverable:** Migrated lb_donate module

**Acceptance Criteria:**
- [ ] lb_donate component works in Layout Builder
- [ ] Component configuration works
- [ ] Donation links work
- [ ] Component displays correctly
- [ ] Bootstrap 5 classes used
- [ ] Integration with other LB components works

---

### Task 3: Donation Form Testing
**Owner:** Developer
**Priority:** CRITICAL

**Actions:**

**3.1 Test form functionality:**
- [ ] Amount selection (preset amounts)
- [ ] Custom amount input
- [ ] Frequency selection (one-time, monthly)
- [ ] Form field validation
- [ ] Required fields
- [ ] Payment field validation
- [ ] Form submission
- [ ] Confirmation page display

**3.2 Test form styling:**
- [ ] Form layout responsive
- [ ] Button groups styled correctly
- [ ] Input fields styled correctly
- [ ] Validation messages display correctly
- [ ] Error states display correctly
- [ ] Submit button styled correctly

**3.3 Test payment integration styling:**
**IMPORTANT:** Only test styling, not payment logic
- [ ] Payment fields display correctly
- [ ] Payment field placeholders
- [ ] Payment field validation styling
- [ ] Payment error message styling
- [ ] PCI compliance visual standards maintained

**3.4 Test accessibility:**
- [ ] Form keyboard navigable
- [ ] Form labels correct
- [ ] Form ARIA attributes
- [ ] Form validation accessible
- [ ] Error messages accessible
- [ ] Screen reader compatible

**Deliverable:** Donation form test report

**Acceptance Criteria:**
- [ ] All form functionality works
- [ ] Form styling correct
- [ ] Payment integration styling correct (no logic changes)
- [ ] Form accessible
- [ ] No critical issues

---

### Task 4: Phase 4 Integration Testing - All Content Types
**Owner:** Developer + QA
**Priority:** CRITICAL

**Actions:**

**4.1 Test all 10 content type modules together:**

**Content Type Modules:**
1. y_branch (Sprint 14)
2. y_branch_menu (Sprint 14)
3. y_program (Sprint 15)
4. y_program_subcategory (Sprint 15)
5. y_camp (Sprint 15)
6. y_facility (Sprint 16)
7. y_lb (Sprint 16)
8. y_lb_article (Sprint 16)
9. y_donate (Sprint 17)
10. lb_donate (Sprint 17)

**4.2 Test content type pages:**
- [ ] Branch page full
- [ ] Program page full
- [ ] Camp page full
- [ ] Facility page full
- [ ] Landing page with LB components
- [ ] Article landing page
- [ ] Donation page

**4.3 Test content type listings:**
- [ ] Branch listing/finder
- [ ] Program listing
- [ ] Camp listing
- [ ] Facility listing
- [ ] Article listing

**4.4 Test taxonomy integration:**
- [ ] Location taxonomy (y_branch)
- [ ] Program subcategory taxonomy
- [ ] Category filtering
- [ ] Category pages
- [ ] Category in content displays

**4.5 Test Layout Builder with content types:**
- [ ] LB components in y_lb (landing pages) - CRITICAL
- [ ] LB components in y_branch
- [ ] LB components in y_program
- [ ] LB components in y_camp
- [ ] LB components in y_facility
- [ ] lb_donate component on various pages

**4.6 Test Activity Finder integration:**
- [ ] Activity Finder on branch pages
- [ ] Activity Finder on program pages
- [ ] Activity Finder isolation maintained
- [ ] No style conflicts

**4.7 Test navigation between content types:**
- [ ] Branch → Programs
- [ ] Program → Branch
- [ ] Landing page → All content types
- [ ] Donation page from various pages

**4.8 Create comprehensive test site:**
```bash
# Create test content for all types
drush node:create branch
drush node:create program
drush node:create camp
drush node:create facility
drush node:create landing-page
drush node:create article
drush node:create donation

# Create realistic content (5-10 of each)
```

**Deliverable:** Phase 4 integration test report

**Acceptance Criteria:**
- [ ] All content types work together
- [ ] No conflicts between modules
- [ ] Layout Builder integration functional
- [ ] Activity Finder integration maintained
- [ ] Navigation works
- [ ] No console errors
- [ ] Realistic content tested

---

### Task 5: Visual Regression Testing - All Phase 4
**Owner:** Developer
**Priority:** HIGH

**Actions:**

**5.1 Update BackstopJS with all Phase 4 pages:**
```json
{
  "scenarios": [
    // Sprint 14
    {"label": "Branch Page", "url": "http://yusaopeny.docksal.site/branch/test"},
    {"label": "Branch Finder", "url": "http://yusaopeny.docksal.site/branch-finder"},

    // Sprint 15
    {"label": "Program Page", "url": "http://yusaopeny.docksal.site/program/test"},
    {"label": "Camp Page", "url": "http://yusaopeny.docksal.site/camp/test"},

    // Sprint 16
    {"label": "Facility Page", "url": "http://yusaopeny.docksal.site/facility/test"},
    {"label": "Landing Page Full", "url": "http://yusaopeny.docksal.site/landing/test"},

    // Sprint 17
    {"label": "Donation Page", "url": "http://yusaopeny.docksal.site/donate"},
    {"label": "Donation Confirmation", "url": "http://yusaopeny.docksal.site/donate/confirmation"}
  ]
}
```

**5.2 Run comprehensive visual tests:**
```bash
cd docs/bootstrap-5-migration/testing
npx backstop test
npx backstop openReport
```

**5.3 Review and document differences:**
- Expected differences (Bootstrap 5 improvements)
- Unexpected differences (investigate and fix)
- Acceptable differences (minor rendering)

**Deliverable:** Phase 4 visual regression report

**Acceptance Criteria:**
- [ ] Visual tests run successfully
- [ ] All content types tested
- [ ] Differences documented
- [ ] Critical issues fixed

---

### Task 6: Accessibility Testing - All Phase 4
**Owner:** Developer + QA
**Priority:** HIGH

**Actions:**

**6.1 Run Pa11y tests on all content types:**
```bash
npx pa11y-ci
```

**6.2 Manual accessibility testing:**
- [ ] Keyboard navigation (all content types)
- [ ] Screen reader testing (all content types)
- [ ] Focus indicators visible
- [ ] Form labels correct (donation form critical)
- [ ] ARIA attributes correct
- [ ] Color contrast WCAG 2.2 AA

**6.3 Test specific accessibility concerns:**
- [ ] Donation form accessible (critical)
- [ ] Branch finder accessible
- [ ] Program filtering accessible
- [ ] LB component accessibility in content types
- [ ] Navigation accessible

**Deliverable:** Phase 4 accessibility report

**Acceptance Criteria:**
- [ ] WCAG 2.2 AA compliance maintained
- [ ] No critical accessibility issues
- [ ] Keyboard navigation works
- [ ] Screen reader compatible
- [ ] Donation form accessible

---

### Task 7: Phase 4 Documentation & GO/NO-GO
**Owner:** Developer
**Priority:** CRITICAL

**Actions:**

**7.1 Document module migrations:**
```bash
touch docs/bootstrap-5-migration/modules/y_donate.md
touch docs/bootstrap-5-migration/modules/lb_donate.md
```

**7.2 Create Phase 4 summary:**
```bash
touch docs/bootstrap-5-migration/phases/PHASE_4_SUMMARY.md
```

**Phase 4 Summary should include:**
- All 10 modules migrated
- Integration testing results
- Layout Builder integration results
- Activity Finder integration results
- Visual regression results
- Accessibility results
- Known issues
- Recommendations

**7.3 Update executive summary:**
```bash
vim docs/bootstrap-5-migration/EXECUTIVE_SUMMARY.md

# Update progress:
# - Phase 4: Complete
# - 10 content type modules migrated
# - Layout Builder integration verified
```

**7.4 Create GO/NO-GO decision document:**
```bash
touch docs/bootstrap-5-migration/decisions/DECISION_PHASE_4_GO_NO_GO.md
```

**GO/NO-GO Criteria:**
- [ ] All 10 content type modules migrated
- [ ] All modules build without errors
- [ ] Integration testing passed
- [ ] Layout Builder integration functional
- [ ] Activity Finder integration maintained
- [ ] Visual regression tests passed
- [ ] Accessibility tests passed
- [ ] No critical bugs
- [ ] Documentation complete

**Deliverable:** Phase 4 completion documentation

**Acceptance Criteria:**
- [ ] All documentation complete
- [ ] Phase 4 summary created
- [ ] GO/NO-GO decision made
- [ ] Executive summary updated
- [ ] Phase 5 ready to start (if approved)

---

## Testing

### Comprehensive Testing Matrix

**Content Type Pages:**
| Content Type | Display | Forms | LB Integration | AF Integration | Responsive | Accessibility |
|--------------|---------|-------|----------------|----------------|------------|---------------|
| Branch | ✓ | ✓ | ✓ | ✓ | ✓ | ✓ |
| Program | ✓ | ✓ | ✓ | ✓ | ✓ | ✓ |
| Camp | ✓ | ✓ | ✓ | N/A | ✓ | ✓ |
| Facility | ✓ | ✓ | ✓ | N/A | ✓ | ✓ |
| Landing Page | ✓ | N/A | ✓ (CRITICAL) | N/A | ✓ | ✓ |
| Article | ✓ | ✓ | ✓ | N/A | ✓ | ✓ |
| Donation | ✓ | ✓ (CRITICAL) | ✓ | N/A | ✓ | ✓ |

**Test Environment:**
- [ ] Desktop (Chrome, Firefox, Safari, Edge)
- [ ] Tablet (iPad, Android)
- [ ] Mobile (iPhone, Android)
- [ ] Screen readers (NVDA, JAWS, VoiceOver)

---

## Deliverables

### Must Have (Critical):
- [ ] y_donate module migrated
- [ ] lb_donate module migrated
- [ ] Donation forms working
- [ ] Payment integration styling correct
- [ ] Phase 4 integration testing complete
- [ ] All 10 content types tested together
- [ ] Layout Builder integration verified
- [ ] Visual regression tests passed
- [ ] Accessibility tests passed
- [ ] Phase 4 documentation complete
- [ ] GO/NO-GO decision made

### Should Have (High Priority):
- [ ] Integration test matrix complete
- [ ] Known issues documented
- [ ] Phase 4 summary created
- [ ] Recommendations documented

### Nice to Have:
- [ ] Performance comparison
- [ ] Optimization opportunities
- [ ] Content editor training materials

---

## Decision Points

### Decision: Phase 4 GO/NO-GO (END OF SPRINT)
**Criteria:**
- All 10 content type modules functional
- Layout Builder integration working
- Activity Finder integration maintained
- No critical bugs
- Acceptable performance
- Accessibility standards met

**Options:**
- GO: Proceed to Phase 5 (Activity Finder Vue.js apps)
- NO-GO: Additional sprint for bug fixes and testing

**Decision Maker:** Project Lead + Stakeholders
**Documentation:** `decisions/DECISION_PHASE_4_GO_NO_GO.md`

---

## Risks

### Risk: Donation Form Payment Integration Issues (HIGH)
**Impact:** CRITICAL - Donations may not work
**Mitigation:**
- Only modify styling, not payment logic
- Test payment integration thoroughly
- Verify PCI compliance maintained
- Have payment integration expert review
- Test in staging environment first
- Document all changes

### Risk: Integration Issues Not Discovered Until Late (MEDIUM)
**Mitigation:**
- Start integration testing early
- Test content types together throughout sprint
- Run tests continuously
- Prioritize critical issues
- Allocate buffer time

### Risk: Layout Builder Integration Regression (MEDIUM)
**Impact:** HIGH - Landing pages may break
**Mitigation:**
- Test LB integration continuously
- Verify Phase 3 LB modules stable
- Test all LB components
- Document LB issues immediately

---

## Notes

### Important:
- This is Phase 4 completion sprint - be thorough
- Donation forms involve payment integration - be careful
- Integration testing is critical - don't skip
- GO/NO-GO decision crucial for project success
- Layout Builder integration must be stable

### Tips:
- Start with donation module migration
- Test payment integration styling carefully
- Run integration tests continuously
- Document all issues, even minor ones
- Save buffer time for unexpected issues
- Create comprehensive test content

### Phase 4 Success Metrics:
- 10 content type modules migrated ✓
- Bootstrap 5.3.3 throughout ✓
- Layout Builder integration functional ✓
- Activity Finder integration maintained ✓
- All tests passing ✓
- Accessibility maintained ✓

### What's Next (Phase 5):
- Activity Finder Vue.js apps migration
- BootstrapVue removal
- Custom Bootstrap 5 component library
- Most technically complex phase

---

## Sprint Review Checklist

At end of sprint, verify:
- [ ] Donation modules migrated
- [ ] Donation forms working
- [ ] Integration testing complete
- [ ] All content types tested together
- [ ] Layout Builder integration verified
- [ ] Visual regression tests passed
- [ ] Accessibility tests passed
- [ ] Documentation complete
- [ ] GO/NO-GO decision made
- [ ] Phase 5 ready (if approved)

---

## Navigation

- **Previous:** [Sprint 16 - Facility & LB](SPRINT_16_Y_Facility_LB.md)
- **Next:** [Sprint 18 - AF Preparation & Audit](SPRINT_18_AF_Preparation_Audit.md)
- **Phase:** [Phase 4 - Content Types](../phases/PHASE_4_CONTENT_TYPES.md)
- **Overview:** [Executive Summary](../EXECUTIVE_SUMMARY.md)

---

**Sprint Status:** ⬜ Not Started
**Last Updated:** 2025-10-17
