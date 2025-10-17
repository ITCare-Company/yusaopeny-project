# Sprint 1: Infrastructure & Research

**Week:** Weeks 1-2
**Duration:** 2 weeks (10 working days)
**Phase:** [Phase 1 - Preparation](../phases/PHASE_1_PREPARATION.md)
**Resources:** 1 Developer
**Status:** Not Started

---

## Sprint Goal

Set up migration infrastructure, study reference implementation, and prepare for theme migration.

---

## Tasks

### Task 1: Migration Branch & Documentation Setup
**Estimate:** 2 hours
**Owner:** Developer
**Priority:** HIGH

**Actions:**
```bash
# Create migration branch
git checkout -b feature/bootstrap-5-migration

# Create documentation structure
mkdir -p docs/bootstrap-5-migration/{phases,sprints,modules,decisions,testing,reference}

# Initialize migration log
touch docs/bootstrap-5-migration/MIGRATION_LOG.md
```

**Acceptance Criteria:**
- [ ] Migration branch created
- [ ] Documentation structure exists
- [ ] MIGRATION_LOG.md template created

---

### Task 2: Study lb_accordion Reference Implementation
**Estimate:** 4 hours
**Owner:** Developer
**Priority:** CRITICAL

**Actions:**
```bash
cd docroot/modules/contrib/lb_accordion

# Study key files
cat package.json
cat webpack.config.js
ls assets/scss/
ls assets/js/
cat templates/block--lb-accordion.html.twig
```

**Document:**
- Bootstrap version used (5.3.3)
- Webpack configuration pattern
- SCSS import strategy
- Template patterns (data-bs-* attributes)
- JavaScript import patterns
- Build process

**Deliverable:** Create `docs/bootstrap-5-migration/reference/LB_ACCORDION_PATTERNS.md`

**Acceptance Criteria:**
- [ ] All lb_accordion files reviewed
- [ ] Key patterns documented
- [ ] Migration checklist template created
- [ ] Build process understood

---

### Task 3: Install and Configure BackstopJS (Visual Regression)
**Estimate:** 3 hours
**Owner:** Developer
**Priority:** HIGH

**Actions:**
```bash
# Install BackstopJS
npm install -D backstopjs

# Initialize
cd docs/bootstrap-5-migration/testing
npx backstop init

# Create scenarios
```

**Configure backstop.json:**
```json
{
  "id": "yusaopeny_bootstrap_migration",
  "viewports": [
    {"label": "phone", "width": 320, "height": 480},
    {"label": "tablet", "width": 768, "height": 1024},
    {"label": "desktop", "width": 1280, "height": 1024}
  ],
  "scenarios": [
    {
      "label": "Homepage",
      "url": "http://yusaopeny.docksal.site/",
      "delay": 1000
    },
    {
      "label": "Branch Page",
      "url": "http://yusaopeny.docksal.site/branch/example",
      "delay": 1000
    }
    // Add more scenarios
  ]
}
```

**Create baseline (Bootstrap 4):**
```bash
# Switch to main branch (Bootstrap 4)
git checkout main

# Create reference screenshots
cd docs/bootstrap-5-migration/testing
npx backstop reference
```

**Acceptance Criteria:**
- [ ] BackstopJS installed
- [ ] backstop.json configured with key pages
- [ ] Baseline screenshots captured (Bootstrap 4)
- [ ] Documentation: How to run visual tests

---

### Task 4: Install and Configure Pa11y (Accessibility Testing)
**Estimate:** 2 hours
**Owner:** Developer
**Priority:** MEDIUM

**Actions:**
```bash
# Install Pa11y
npm install -D pa11y-ci

# Create configuration
```

**Create .pa11yci.json:**
```json
{
  "defaults": {
    "standard": "WCAG2AA",
    "runners": ["axe", "htmlcs"],
    "timeout": 10000
  },
  "urls": [
    "http://yusaopeny.docksal.site/",
    "http://yusaopeny.docksal.site/branch/example",
    "http://yusaopeny.docksal.site/program/example",
    "http://yusaopeny.docksal.site/class/example"
  ]
}
```

**Run baseline:**
```bash
npx pa11y-ci --reporter html > docs/bootstrap-5-migration/testing/pa11y-baseline.html
```

**Acceptance Criteria:**
- [ ] Pa11y installed
- [ ] .pa11yci.json configured
- [ ] Baseline accessibility report generated
- [ ] Documentation: How to run accessibility tests

---

### Task 5: Date Picker Investigation & Decision
**Estimate:** 4 hours
**Owner:** Developer
**Priority:** MEDIUM

**Background:**
- Current: bootstrap-datepicker 1.3.0 (Bootstrap 3/4 only, NOT compatible with BS5)
- Need: Replacement for openy_repeat module

**Options to Test:**

**Option A: Flatpickr** (Recommended)
```bash
npm install flatpickr

# Test integration
# - No Bootstrap dependency
# - Lightweight (~15KB)
# - Good accessibility
# - Mobile-friendly
```

**Option B: Tempus Dominus**
```bash
npm install @eonasdan/tempus-dominus

# Test integration
# - Built for Bootstrap 5
# - Comprehensive features
# - Heavier (~80KB)
```

**Option C: Native HTML5 Date Input**
```html
<input type="date" class="form-control">

# Test:
# - No dependencies
# - Good browser support (98%+)
# - Limited styling options
```

**Testing:**
- Install each option
- Test with openy_repeat module
- Test styling with Bootstrap 5
- Test accessibility
- Test mobile behavior
- Compare file sizes

**Deliverable:** Create `docs/bootstrap-5-migration/decisions/DECISION_DATE_PICKER.md`

**Acceptance Criteria:**
- [ ] All 3 options tested
- [ ] Pros/cons documented
- [ ] **Decision made and documented**
- [ ] Implementation plan for Sprint 13

---

### Task 6: Module Inventory Audit
**Estimate:** 3 hours
**Owner:** Developer
**Priority:** MEDIUM

**Actions:**
```bash
# Find all package.json files with Bootstrap
find docroot/ -name "package.json" -exec grep -l "bootstrap" {} \;

# Count modules
find docroot/modules/contrib/lb_* -type d -maxdepth 0 | wc -l
find docroot/modules/contrib/ws_small_y/modules/ -type d -maxdepth 1 | wc -l
```

**Audit:**
1. Verify MODULE_INVENTORY.md is accurate
2. Identify which modules are actually enabled/used
3. Identify any modules that can be skipped
4. Document module priorities

**Deliverable:** Update `MODULE_INVENTORY.md` with audit findings

**Acceptance Criteria:**
- [ ] All Bootstrap dependencies verified
- [ ] Unused modules identified (if any)
- [ ] Module priorities documented
- [ ] Total count confirmed (66+ modules)

---

### Task 7: Create Migration Checklist Template
**Estimate:** 2 hours
**Owner:** Developer
**Priority:** MEDIUM

**Deliverable:** `docs/bootstrap-5-migration/reference/MIGRATION_CHECKLIST_TEMPLATE.md`

**Template should include:**
- [ ] Study module structure
- [ ] Update package.json
- [ ] Update webpack.config.js
- [ ] Update SCSS files
- [ ] Update Twig templates
- [ ] Update JavaScript
- [ ] Update .libraries.yml
- [ ] Build module
- [ ] Test functionality
- [ ] Test responsive
- [ ] Test accessibility
- [ ] Document changes
- [ ] Update module README

**Acceptance Criteria:**
- [ ] Template created
- [ ] Checklist comprehensive
- [ ] Easy to copy/paste for each module

---

## Testing

### Manual Testing Only (This Sprint)
- [ ] BackstopJS can capture screenshots
- [ ] Pa11y can run accessibility tests
- [ ] Date picker options testable
- [ ] lb_accordion builds successfully

---

## Deliverables

### Must Have:
- [x] Migration branch created
- [x] lb_accordion patterns documented
- [x] BackstopJS installed and configured
- [x] Pa11y installed and configured
- [x] Date picker decision made
- [x] Module inventory complete

### Nice to Have:
- [ ] Troubleshooting guide started
- [ ] FAQ document started

---

## Decision Points

### Decision: Date Picker Replacement
**Options:** Flatpickr, Tempus Dominus, Native HTML5
**Decision Required By:** End of Sprint 1
**Decision Maker:** Developer + Project Lead
**Documentation:** `decisions/DECISION_DATE_PICKER.md`

---

## Risks

### Risk: BackstopJS Setup Issues
**Mitigation:** Allow extra time, use default configuration if complex setup fails

### Risk: Date Picker Testing Takes Too Long
**Mitigation:** Focus on Flatpickr first (most recommended), test others only if time permits

---

## Notes

### Important:
- This sprint is research and setup - no migration work yet
- Take time to understand lb_accordion thoroughly
- Document everything - will save time later
- Test infrastructure now prevents issues later

### Tips:
- Run BackstopJS on small set of pages initially
- Pa11y may find existing accessibility issues - don't fix now, just document
- Date picker implementation happens in Sprint 13, just decide now

---

## Sprint Review Checklist

At end of sprint, verify:
- [ ] All tasks completed
- [ ] All deliverables created
- [ ] Decisions documented
- [ ] Next sprint ready to start
- [ ] Blockers identified (if any)

---

## Navigation

- **Previous:** N/A (First sprint)
- **Next:** [Sprint 2 - Theme Migration Part 1](SPRINT_02_Theme_Part1.md)
- **Phase:** [Phase 1 - Preparation](../phases/PHASE_1_PREPARATION.md)
- **Overview:** [Executive Summary](../EXECUTIVE_SUMMARY.md)

---

**Sprint Status:** ⬜ Not Started
**Last Updated:** 2025-10-17
