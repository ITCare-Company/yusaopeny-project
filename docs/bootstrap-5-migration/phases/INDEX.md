# Bootstrap 5 Migration - Phases Index

**Total Phases:** 6 phases
**Total Duration:** 48 weeks (11-12 months)
**Current Phase:** Phase 1 - Preparation

---

## Phase Overview

| Phase | Duration | Sprints | Status | Priority |
|-------|----------|---------|--------|----------|
| [Phase 1: Preparation](#phase-1-preparation) | 6 weeks | 1-3 | ✅ Documented | ⭐⭐⭐ CRITICAL |
| [Phase 2: Website Services](#phase-2-website-services) | 8 weeks | 4-7 | ⬜ To Document | ⭐⭐ HIGH |
| [Phase 3: Layout Builder](#phase-3-layout-builder) | 12 weeks | 8-13 | ⬜ To Document | ⭐⭐ HIGH |
| [Phase 4: Content Types](#phase-4-content-types) | 8 weeks | 14-17 | ⬜ To Document | ⭐ MEDIUM |
| [Phase 5: Activity Finder](#phase-5-activity-finder) | 8 weeks | 18-21 | ⬜ To Document | ⭐⭐⭐ CRITICAL |
| [Phase 6: Testing & Rollout](#phase-6-testing--rollout) | 6 weeks | 22-24 | ⬜ To Document | ⭐⭐⭐ CRITICAL |

**Total: 48 weeks**

---

## Phase 1: Preparation

**Duration:** 6 weeks (Sprints 1-3)
**Focus:** Infrastructure, Core Theme, Activity Finder Isolation

### Goals:
- Set up testing infrastructure (BackstopJS, Pa11y)
- Study lb_accordion reference implementation
- Migrate openy_carnation theme to Bootstrap 5.3.3
- Isolate Activity Finder with scoped Bootstrap 4 CSS

### Key Deliverables:
- [x] Testing tools configured
- [x] Theme migrated to Bootstrap 5
- [x] Activity Finder isolated
- [x] Documentation patterns established

### Sprints:
- [Sprint 1: Infrastructure & Research](../sprints/SPRINT_01_Infrastructure.md) ✅
- [Sprint 2: Theme Migration Part 1](../sprints/SPRINT_02_Theme_Part1.md) ⬜
- [Sprint 3: Theme Part 2 + AF Isolation](../sprints/SPRINT_03_Theme_Part2_AF_Isolation.md) ⬜

**[📄 Full Phase 1 Documentation](PHASE_1_PREPARATION.md)**

---

## Phase 2: Website Services

**Duration:** 8 weeks (Sprints 4-7)
**Focus:** WS Small Y Modules + Other WS Modules

### Goals:
- Migrate all 16 ws_small_y submodules
- Migrate ws_event, ws_promotion, ws_colorway_canada, etc.
- Batch process similar modules for efficiency

### Key Modules (22 total):
- 16 small_y_* modules
- 6 other WS modules

### Sprints:
- Sprint 4: WS Small Y Batch 1 (6 modules)
- Sprint 5: WS Small Y Batch 2 (10 modules)
- Sprint 6: Other WS Modules (6 modules)
- Sprint 7: Testing & Catchup

**[📄 Full Phase 2 Documentation](PHASE_2_WEBSITE_SERVICES.md)** ⬜ To Create

---

## Phase 3: Layout Builder

**Duration:** 12 weeks (Sprints 8-13)
**Focus:** Layout Builder Modules

### Goals:
- Migrate 19 remaining lb_* modules to Bootstrap 5
- Follow lb_accordion pattern
- Special attention to interactive components (modal, carousel)

### Key Modules (19 total):
- **High Priority (5):** lb_hero, lb_cards, lb_carousel, lb_modal, lb_webform
- **Medium Priority (5):** Branch blocks, ping_pong, promo
- **Lower Priority (9):** Grid, partners, related content, staff, stats, table, testimonials

### Sprints:
- Sprints 8-9: High Priority LB Modules
- Sprints 10-11: Medium Priority LB Modules
- Sprint 12: Lower Priority LB Modules
- Sprint 13: LB Integration Testing + Date Picker

**[📄 Full Phase 3 Documentation](PHASE_3_LAYOUT_BUILDER.md)** ⬜ To Create

---

## Phase 4: Content Types

**Duration:** 8 weeks (Sprints 14-17)
**Focus:** Y Content Type Modules

### Goals:
- Migrate all y_* content type modules
- Ensure integration with Layout Builder
- Test content display across all types

### Key Modules (10 total):
- y_branch, y_branch_menu
- y_program, y_program_subcategory, y_camp
- y_facility
- y_lb, y_lb_article
- y_donate

### Sprints:
- Sprint 14: Y Branch & Related
- Sprint 15: Y Program & Camp
- Sprint 16: Y Facility & LB
- Sprint 17: Y Donate & Testing

**[📄 Full Phase 4 Documentation](PHASE_4_CONTENT_TYPES.md)** ⬜ To Create

---

## Phase 5: Activity Finder

**Duration:** 8 weeks (Sprints 18-21)
**Focus:** Activity Finder Vue.js Applications

### Goals:
- Remove BootstrapVue dependencies
- Migrate to Bootstrap 5 vanilla JS
- Maintain functionality across all 3 apps

### Key Challenges:
⚠️ **CRITICAL:** BootstrapVue 2 NOT compatible with Bootstrap 5

### Strategy:
1. Create Bootstrap 5 component library
2. Audit BootstrapVue usage
3. Replace components incrementally
4. Test extensively

### Apps (3 total):
- Camp Finder (openy_cf_vue_app)
- Activity Finder (openy_af_vue_app)
- Activity Finder 4 (openy_af4_vue_app)

### Sprints:
- Sprint 18: Preparation & BootstrapVue Audit
- Sprint 19: Camp Finder Migration
- Sprint 20: Activity Finder Migration
- Sprint 21: Activity Finder 4 Migration

**[📄 Full Phase 5 Documentation](PHASE_5_ACTIVITY_FINDER.md)** ⬜ To Create

---

## Phase 6: Testing & Rollout

**Duration:** 6 weeks (Sprints 22-24)
**Focus:** Comprehensive Testing, Documentation, Staged Rollout

### Goals:
- Comprehensive testing (visual, accessibility, performance)
- Complete documentation updates
- Execute multi-tier rollout strategy
- Provide community support

### Key Activities:
- Visual regression testing (BackstopJS)
- Accessibility testing (Pa11y, WCAG 2.2 AA)
- Performance testing (Lighthouse 90+)
- Cross-browser testing
- Documentation updates
- Staged rollout (D → C → B → A)

### Sprints:
- Sprint 22: Comprehensive Testing & Bug Fixes
- Sprint 23: Documentation & Community Preparation
- Sprint 24: Staged Rollout & Launch

**[📄 Full Phase 6 Documentation](PHASE_6_TESTING_ROLLOUT.md)** ⬜ To Create

---

## Dependencies Between Phases

```
Phase 1 (Theme) → MUST complete before Phase 2
    ↓
Phase 2 (WS Modules) → Can partially overlap with Phase 3
    ↓
Phase 3 (LB Modules) → Can partially overlap with Phase 4
    ↓
Phase 4 (Content Types) → Depends on Phase 3 (LB modules)
    ↓
Phase 5 (Activity Finder) → Independent, can start earlier if resources allow
    ↓
Phase 6 (Testing) → Requires all previous phases complete
```

---

## Critical Success Factors

### Phase 1:
- ✅ Theme must migrate successfully
- ✅ Activity Finder isolation must work

### Phases 2-4:
- Follow established patterns from Phase 1
- Maintain quality through testing
- Keep documentation updated

### Phase 5:
- BootstrapVue replacement must be functional
- No breaking changes to Activity Finder features

### Phase 6:
- Zero visual regressions
- WCAG 2.2 AA compliance
- Community accepts changes

---

## Navigation

- **← Back to:** [Main Documentation Hub](../README.md)
- **→ Start Migration:** [Phase 1 - Preparation](PHASE_1_PREPARATION.md)
- **→ View Sprints:** [Sprints Index](../sprints/INDEX.md)

---

**Last Updated:** 2025-10-17
**Status:** Phase 1 documented, Phases 2-6 to be created
