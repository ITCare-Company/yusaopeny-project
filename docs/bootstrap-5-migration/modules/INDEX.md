# Bootstrap 5 Migration - Modules Index

**Total Modules:** 66+ modules across 6 categories
**Current Status:** Documentation complete, migration planned
**Last Updated:** 2025-10-17

---

## Quick Navigation

| Category | Document | Count | Status |
|----------|----------|-------|--------|
| **Theme** | [MODULES_THEME.md](MODULES_THEME.md) | 1 | ✅ Documented |
| **Layout Builder** | [MODULES_LAYOUT_BUILDER.md](MODULES_LAYOUT_BUILDER.md) | 20 | ✅ Documented |
| **WS Small Y** | [MODULES_WS_SMALL_Y.md](MODULES_WS_SMALL_Y.md) | 16 | ✅ Documented |
| **Activity Finder** | [MODULES_ACTIVITY_FINDER.md](MODULES_ACTIVITY_FINDER.md) | 3 | ✅ Documented |
| **Content Types** | [MODULES_CONTENT_TYPES.md](MODULES_CONTENT_TYPES.md) | 10 | ✅ Documented |
| **Other/Supporting** | [MODULES_OTHER.md](MODULES_OTHER.md) | 16+ | ✅ Documented |

**Total:** 66+ modules

---

## Module Categories Overview

### 1. Theme Module (1 module)

**Document:** [MODULES_THEME.md](MODULES_THEME.md)

**Module:** openy_carnation
- Base theme for all Y USA Open Y sites
- Bootstrap 4.4.1 → 5.3.3
- Phase 1, Sprints 2-3
- **Status:** ⬜ Not Started

**Priority:** ⭐⭐⭐ CRITICAL (must complete first)

---

### 2. Layout Builder Modules (20 modules)

**Document:** [MODULES_LAYOUT_BUILDER.md](MODULES_LAYOUT_BUILDER.md)

**Summary:**
- 19 modules to migrate (1 already complete: lb_accordion)
- Phase 3, Sprints 8-13
- High-priority modules: lb_hero, lb_cards, lb_carousel, lb_modal, lb_webform

**Module List:**
- ✅ **lb_accordion** (Bootstrap 5.3.3) - Complete
- ❌ **lb_hero** - High Priority
- ❌ **lb_cards** - High Priority
- ❌ **lb_carousel** - High Priority
- ❌ **lb_modal** - High Priority
- ❌ **lb_webform** - High Priority
- ❌ **lb_branch_blocks_menu** - Medium Priority
- ❌ **lb_branch_header** - Medium Priority
- ❌ **lb_branch_hours** - Medium Priority
- ❌ **lb_ping_pong** - Medium Priority
- ❌ **lb_promo** - Medium Priority
- ❌ **lb_grid_content** - Lower Priority
- ❌ **lb_grid_cta** - Lower Priority
- ❌ **lb_partners** - Lower Priority
- ❌ **lb_related_content** - Lower Priority
- ❌ **lb_staff_members** - Lower Priority
- ❌ **lb_statistics** - Lower Priority
- ❌ **lb_table** - Lower Priority
- ❌ **lb_testimonials** - Lower Priority
- ❌ **lb_tabs** - Lower Priority (verify vs ws_lb_tabs)

**Priority:** ⭐⭐ HIGH

---

### 3. Website Services - Small Y (16 modules)

**Document:** [MODULES_WS_SMALL_Y.md](MODULES_WS_SMALL_Y.md)

**Summary:**
- Parent module: ws_small_y
- 16 submodules providing content display components
- Phase 2, Sprints 4-5
- Batch migration approach recommended

**High Priority Batch (Sprint 4 - 6 modules):**
1. small_y_hero (jumbotron removal - complex)
2. small_y_cards (card deck removal - complex)
3. small_y_carousels (interactive)
4. small_y_accordions (interactive)
5. small_y_alerts (commonly used)
6. small_y_tabs (interactive)

**Medium Priority Batch (Sprint 5 - 10 modules):**
7. small_y_articles
8. small_y_branch
9. small_y_editor
10. small_y_events
11. small_y_icon_grid
12. small_y_ping_pongs
13. small_y_search
14. ws_small_y_staff
15. ws_small_y_statistics
16. ws_small_y_testimonials

**Priority:** ⭐⭐ HIGH

---

### 4. Activity Finder Applications (3 Vue.js apps)

**Document:** [MODULES_ACTIVITY_FINDER.md](MODULES_ACTIVITY_FINDER.md)

**Summary:**
- Vue 2 + Bootstrap 4.6.1 + BootstrapVue 2.22.0
- Target: Vue 2 + Bootstrap 5.3.3 (NO BootstrapVue)
- Phase 5, Sprints 18-21
- **Risk Level:** ⚠️ CRITICAL

**Applications:**
1. **Camp Finder** (openy_cf_vue_app) - Sprint 19
2. **Activity Finder** (openy_af_vue_app) - Sprint 20
3. **Activity Finder 4** (openy_af4_vue_app) - Sprint 21

**Critical Issue:**
BootstrapVue 2 is **NOT compatible** with Bootstrap 5. Must replace all BootstrapVue components with Bootstrap 5 vanilla JavaScript + custom Vue components.

**Priority:** ⭐⭐⭐ CRITICAL (BootstrapVue incompatibility)

---

### 5. Content Type Modules (10 modules)

**Document:** [MODULES_CONTENT_TYPES.md](MODULES_CONTENT_TYPES.md)

**Summary:**
- Drupal content types (node types)
- Phase 4, Sprints 14-17
- Focus on display templates and form widgets

**Module Groups:**

**Branch-Related (Sprint 14):**
1. y_branch
2. y_branch_menu

**Program & Camp (Sprint 15):**
3. y_program (Activity Finder integration)
4. y_program_subcategory
5. y_camp (Camp Finder integration)

**Facility & Layout Builder Content (Sprint 16):**
6. y_facility
7. y_lb (generic Layout Builder content)
8. y_lb_article

**Donation (Sprint 17):**
9. y_donate (payment integration - critical)
10. y_donate_form (if separate)

**Priority:** ⭐ MEDIUM (depends on Phase 3)

---

### 6. Other/Supporting Modules (16+ modules)

**Document:** [MODULES_OTHER.md](MODULES_OTHER.md)

**Summary:**
- Supporting modules, CRM integrations, utilities
- Various phases and sprints
- Mostly review-only or minimal changes

**Website Services - Other (Phase 2, Sprint 6):**
1. ws_event
2. ws_promotion (+ 2 submodules)
3. ws_colorway_canada (+ lb_hero_canada)
4. ws_lb_tabs
5. ws_home_branch

**CRM Integrations (Phase 4-6, Review):**
6. openy_daxko
7. openy_activenet
8. openy_groupex_pro

**Location & Mapping (Phase 2 or 4):**
9. openy_loc_finder
10. openy_map

**Search (Phase 2-4):**
11. openy_search
12. openy_search_api

**Demo & Development (Phase 6):**
13. openy_demo_content
14. openy_fixtures
15. openy_development

**Contributed Modules:**
16. Various contrib modules (views_bootstrap, webform, paragraphs, etc.)

**Priority:** ⭐ MEDIUM-LOW (supporting modules)

---

## Migration Progress by Category

### Overall Progress: 1.5% (1/66 modules)

| Category | Complete | Total | Progress | Phase | Status |
|----------|----------|-------|----------|-------|--------|
| Theme | 0 | 1 | 0% | Phase 1 | ⬜ Not Started |
| Layout Builder | 1 | 20 | 5% | Phase 3 | ⬜ Not Started |
| WS Small Y | 0 | 16 | 0% | Phase 2 | ⬜ Not Started |
| Activity Finder | 0 | 3 | 0% | Phase 5 | ⬜ Not Started |
| Content Types | 0 | 10 | 0% | Phase 4 | ⬜ Not Started |
| Other | 0 | 16+ | 0% | Various | ⬜ Not Started |

---

## Migration Order (Phase Sequence)

### Critical Path:

```
Phase 1: Theme (openy_carnation)
   ↓ BLOCKS Phase 2 and 3
Phase 2: WS Small Y + Other WS Modules
   ↓ Can overlap with Phase 3
Phase 3: Layout Builder Modules
   ↓ BLOCKS Phase 4 (y_lb, y_lb_article depend on LB modules)
Phase 4: Content Types
   ↓ BLOCKS Phase 5 (y_program and y_camp needed for Activity Finder)
Phase 5: Activity Finder (Vue.js apps)
   ↓
Phase 6: Final Testing & Rollout
```

**Key Dependencies:**
- Phase 1 must complete before ALL other phases
- Phase 3 must complete before Sprint 16 (y_lb, y_lb_article)
- Phase 4 (Sprint 15: y_program, y_camp) must complete before Phase 5

---

## Bootstrap Version Matrix

| Current Version | Target Version | Module Count |
|-----------------|----------------|--------------|
| 4.4.1 | 5.3.3 | 62 modules |
| 4.6.1 + BootstrapVue 2 | 5.3.3 (no BV) | 3 apps (Activity Finder) |
| 5.3.3 | 5.3.3 | 1 module (lb_accordion ✅) |

---

## Key Challenges by Category

### Theme (openy_carnation):
- **Challenge:** Base theme affects all other modules
- **Impact:** Blocking for all phases
- **Mitigation:** Complete in Phase 1 (Sprints 2-3)

### Layout Builder:
- **Challenge:** 19 modules, various complexity levels
- **Impact:** Blocks content type modules (y_lb, y_lb_article)
- **Mitigation:** Prioritize high-use modules (hero, cards, carousel, modal)

### WS Small Y:
- **Challenge:** Jumbotron removal, card deck removal
- **Impact:** Visual layout changes
- **Mitigation:** Batch processing, test thoroughly, provide migration guide

### Activity Finder:
- **Challenge:** BootstrapVue 2 incompatibility (CRITICAL)
- **Impact:** Complete UI rewrite required
- **Mitigation:** Build custom component library, phase migration per app

### Content Types:
- **Challenge:** Integration with Activity/Camp Finder
- **Impact:** Could break search/filter functionality
- **Mitigation:** Test with Activity Finder apps, maintain field compatibility

### Other:
- **Challenge:** CRM integration breaks, payment processing
- **Impact:** Revenue-affecting workflows
- **Mitigation:** Extensive testing, sandbox mode, rollback plan

---

## Testing Strategy

### Per-Module Testing:
- Visual regression (BackstopJS)
- Accessibility (Pa11y, WCAG 2.2 AA)
- Functional testing (interactive components)
- Browser compatibility

### Integration Testing:
- Test modules together within each phase
- Test dependencies between phases
- Performance testing (bundle size, load times)

### System Testing:
- Full site testing after all migrations
- Comprehensive testing (Phase 6, Sprint 22)
- Staged rollout (D → C → B → A)

**See:** [Testing Documentation](../testing/INDEX.md)

---

## Resources for Module Migration

### Reference Implementation:
- **lb_accordion** - Only module already migrated to Bootstrap 5
- Study patterns and approach
- Replicate for other modules

### Migration Tools:
- Webpack 5
- Bootstrap 5.3.3
- Node.js LTS
- BackstopJS (visual regression)
- Pa11y (accessibility)
- Lighthouse (performance)

### Key Documentation:
- [Bootstrap 5 Migration Guide](https://getbootstrap.com/docs/5.3/migration/)
- [Bootstrap 5 Cheatsheet](../reference/BOOTSTRAP_5_CHEATSHEET.md)
- [Migration Checklist Template](../reference/MIGRATION_CHECKLIST_TEMPLATE.md)
- [Troubleshooting Guide](../reference/TROUBLESHOOTING.md)

---

## Navigation

- **← Back to:** [Main Documentation Hub](../README.md)
- **→ View Phases:** [Phases Index](../phases/INDEX.md)
- **→ View Sprints:** [Sprints Index](../sprints/INDEX.md)
- **→ View Progress:** [Progress Tracker](../PROGRESS.md)

### Quick Links to Module Documents:
- [Theme Module](MODULES_THEME.md)
- [Layout Builder Modules](MODULES_LAYOUT_BUILDER.md)
- [WS Small Y Modules](MODULES_WS_SMALL_Y.md)
- [Activity Finder Apps](MODULES_ACTIVITY_FINDER.md)
- [Content Type Modules](MODULES_CONTENT_TYPES.md)
- [Other/Supporting Modules](MODULES_OTHER.md)

---

**Index Version:** 1.0
**Last Updated:** 2025-10-17
**Total Modules:** 66+
**Documentation Status:** ✅ All category documents complete
