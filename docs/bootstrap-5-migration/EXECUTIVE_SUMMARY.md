# Bootstrap 5 Migration - Executive Summary

**Project:** Y USA Open YMCA Bootstrap 4 → Bootstrap 5 Migration
**Timeline:** 9-12 months (Gradual approach recommended)
**Status:** Planning Phase
**Last Updated:** 2025-10-17

---

## Overview

The Y USA Open YMCA distribution currently uses Bootstrap 4.4.1 across **66+ modules and themes**. This project will upgrade to Bootstrap 5.3.3 to ensure:
- Modern CSS framework support
- Better accessibility (WCAG 2.2 AA)
- Improved performance (15-20% smaller bundle size)
- Security updates and long-term maintainability
- Drupal 11 compatibility alignment

---

## Scope

### Components to Migrate: 66+ Total

**1. Core Theme (1):**
- openy_carnation (Bootstrap 4.4.1)

**2. Layout Builder Modules (20):**
- ✅ lb_accordion (already Bootstrap 5.3.3)
- ❌ 19 modules on Bootstrap 4.4.1

**3. Website Services Small Y (16):**
- All 16 small_y_* modules (Bootstrap 4.4.1)

**4. Activity Finder System (3 Vue apps):**
- openy_af_vue_app (BootstrapVue 2.22.0)
- openy_cf_vue_app (BootstrapVue 2.22.0)
- openy_af4_vue_app (Bootstrap 4.6.1 + BootstrapVue 2.22.0)
- ⚠️ **Critical:** BootstrapVue 2 NOT compatible with Bootstrap 5

**5. Content Type Modules (10+):**
- y_branch, y_camp, y_facility, y_program, etc. (Bootstrap 4.4.1)

**6. Other Modules (15+):**
- ws_event, ws_promotion, openy_node_alert, openy_repeat, etc.

---

## Timeline: 24 Sprints (48 Weeks ~ 11 Months)

| Phase | Sprints | Weeks | Focus |
|-------|---------|-------|-------|
| **Phase 1: Preparation** | 1-3 | 1-6 | Infrastructure, theme, AF isolation |
| **Phase 2: WS Modules** | 4-7 | 7-14 | Website Services modules (~16) |
| **Phase 3: LB Modules** | 8-13 | 15-26 | Layout Builder modules (~20) |
| **Phase 4: Content Types** | 14-17 | 27-34 | Y content type modules (~10) |
| **Phase 5: Activity Finder** | 18-21 | 35-42 | Vue app migrations (3 apps) |
| **Phase 6: Testing & Rollout** | 22-24 | 43-48 | Comprehensive testing, docs, launch |

**Total Duration:** 48 weeks (11-12 months) ✅

---

## Resources Required

**Primary Team:**
- 1 Full-time Frontend Developer (48 weeks)
- Contractor Support (recommended for 16-20 weeks)
- QA Engineer (optional, 2 weeks for comprehensive testing)
- Project Manager (coordination, tracking)

**Skills Needed:**
- Bootstrap 4 & 5 expertise
- SCSS/Sass
- JavaScript (ES6+), Vue.js 2
- Webpack
- Drupal theming
- Accessibility (WCAG 2.2)
- Testing (BackstopJS, Pa11y, Behat)

---

## Key Challenges

### 1. Activity Finder - BootstrapVue Incompatibility ⚠️
**Problem:** BootstrapVue 2 ONLY supports Bootstrap 4
**Solution:**
- Phase 1: Isolate Activity Finder with scoped Bootstrap 4 CSS
- Phase 5: Migrate to Bootstrap 5 vanilla JS (remove BootstrapVue)
**Risk:** High - Requires significant Vue component rewrite
**Timeline:** 8 weeks dedicated

### 2. Breaking Changes Across 66+ Modules
**Problem:** Bootstrap 5 has many breaking changes (data attributes, class names, components)
**Solution:** Systematic migration using lb_accordion as reference
**Risk:** Medium - Visual regressions possible
**Mitigation:** Progressive testing (Basic → Standard → Comprehensive)

### 3. Community Resistance (#1 Failure Condition)
**Problem:** Large community needs to adopt Bootstrap 5
**Solution:** Multi-tier rollout (New sites → Safe sites → Flagged → Staged)
**Risk:** High if not managed carefully
**Mitigation:** Extensive docs, beta testing, support, opt-in flag

---

## Breaking Changes Highlights

### Data Attributes (ALL CHANGED)
```html
<!-- Bootstrap 4 -->
<button data-toggle="modal" data-target="#myModal">

<!-- Bootstrap 5 -->
<button data-bs-toggle="modal" data-bs-target="#myModal">
```

### Common Class Changes
- `.btn-block` → `.d-grid` wrapper
- `.form-group` → `.mb-3`
- `.custom-select` → `.form-select`
- `.close` → `.btn-close`
- `.ml-*` / `.mr-*` → `.ms-*` / `.me-*`
- `.text-left` / `.text-right` → `.text-start` / `.text-end`

### JavaScript API
```javascript
// Bootstrap 4 (jQuery)
$('#myModal').modal('show');

// Bootstrap 5 (Vanilla JS)
const modal = new bootstrap.Modal(document.getElementById('myModal'));
modal.show();
```

---

## Success Metrics

**Technical (Priority #1):**
- [ ] All 66+ modules migrated to Bootstrap 5.3+
- [ ] Zero Bootstrap 4 dependencies
- [ ] WCAG 2.2 AA compliance maintained
- [ ] Lighthouse scores 90+
- [ ] 15-20% bundle size reduction

**Operational (Priority #2):**
- [ ] Completed within 9-12 months
- [ ] Zero site downtime
- [ ] < 10 critical support issues

**Community (Priority #3 - Avoid Resistance):**
- [ ] Positive community feedback
- [ ] Successful beta testing
- [ ] Smooth adoption

---

## Rollout Strategy (Multi-Tier)

**D → C → B → A Approach:**

1. **D - New Sites Only** (Day 1-2)
   - New installations default to Bootstrap 5
   - Existing sites unchanged

2. **C - Safe Sites Direct** (Day 3-4)
   - 3-5 "safe" volunteer sites
   - Technical teams available
   - Direct deployment

3. **B - Activity Finder Flag** (Day 5-7)
   - Feature flag for opt-in
   - Sites can migrate when ready

4. **A - Distribution Staged** (Day 8-14)
   - Internal testing
   - Beta partners
   - Stable release to main branch

---

## Documentation Structure

New documentation is split into **< 300 line documents** for easier execution:

```
docs/bootstrap-5-migration/
├── README.md - Navigation hub
├── EXECUTIVE_SUMMARY.md - This file
├── MODULE_INVENTORY.md - Complete module list
├── QUICK_START.md - Developer guide
├── phases/ - 8 phase documents (< 300 lines each)
├── sprints/ - 24 sprint documents (< 250 lines each)
├── modules/ - Module-specific details
├── decisions/ - Key decisions documented
├── testing/ - Testing strategies
└── reference/ - Cheatsheets, troubleshooting
```

See: [REORGANIZATION_PLAN.md](REORGANIZATION_PLAN.md)

---

## Next Steps

### Immediate Actions:
1. **Review this summary** with stakeholders
2. **Get approval** for timeline and resources
3. **Assign primary developer**
4. **Create remaining core documents** (MODULE_INVENTORY, QUICK_START)
5. **Begin Sprint 1** - Infrastructure & Research

### Before Starting Migration:
- [ ] Primary developer assigned?
- [ ] Contractor identified?
- [ ] Budget approved?
- [ ] Stakeholders aligned?
- [ ] Community notified?

---

## Key Documents

- **Full Details:** See `phases/` and `sprints/` folders
- **Module List:** [MODULE_INVENTORY.md](MODULE_INVENTORY.md)
- **Get Started:** [QUICK_START.md](QUICK_START.md)
- **Reorganization:** [REORGANIZATION_PLAN.md](REORGANIZATION_PLAN.md)
- **Original Strategy:** [archive/MIGRATION_STRATEGY.md](archive/MIGRATION_STRATEGY.md) (2263 lines)
- **Original Sprint Plan:** [archive/SPRINT_PLAN.md](archive/SPRINT_PLAN.md) (1479 lines)

---

**Status:** ✅ READY FOR PLANNING
**Next Action:** Review with team, get approval, start Sprint 1 planning
