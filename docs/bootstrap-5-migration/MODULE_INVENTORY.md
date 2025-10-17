# Bootstrap 5 Migration - Complete Module Inventory

**Total Modules:** 66+ modules/themes with Bootstrap dependencies
**Date:** 2025-10-17
**Status:** Complete inventory from codebase scan

---

## Summary by Category

| Category | Count | Bootstrap Version | Status |
|----------|-------|-------------------|--------|
| **Theme** | 1 | 4.4.1 | ❌ Needs migration |
| **Layout Builder** | 20 | 4.4.1 (19), 5.3.3 (1) | ✅ 1 done, ❌ 19 pending |
| **WS Small Y** | 16 | 4.4.1 | ❌ Needs migration |
| **Activity Finder** | 3 | 4.6.1 + BootstrapVue 2 | ❌ Needs migration |
| **Content Types** | 10 | 4.4.1 | ❌ Needs migration |
| **Other WS** | 6 | 4.4.1 | ❌ Needs migration |
| **Other** | 10+ | 4.4.1 | ❌ Needs migration |

---

## 1. THEME (1 module)

### openy_carnation
- **Path:** `docroot/themes/contrib/openy_carnation`
- **Bootstrap:** 4.4.1
- **Dependencies:** popper.js 1.16.0
- **Priority:** CRITICAL (affects entire site)
- **Sprint:** Sprint 2-3
- **Notes:** Core theme, must be migrated first

---

## 2. LAYOUT BUILDER MODULES (20 modules)

### ✅ Already Migrated (1)

#### lb_accordion
- **Path:** `docroot/modules/contrib/lb_accordion`
- **Bootstrap:** 5.3.3 ✅
- **Dependencies:** @popperjs/core 2.11.8
- **Status:** Complete - use as reference implementation
- **Notes:** Migrated to Bootstrap 5, Webpack 5

### ❌ Need Migration (19 modules)

#### High Priority (5)
1. **lb_hero**
   - **Path:** `docroot/modules/contrib/lb_hero`
   - **Priority:** CRITICAL
   - **Sprint:** Sprint 8
   - **Notes:** Homepage hero component

2. **lb_cards**
   - **Path:** `docroot/modules/contrib/lb_cards`
   - **Priority:** CRITICAL
   - **Sprint:** Sprint 8
   - **Notes:** Commonly used card layouts

3. **lb_carousel**
   - **Path:** `docroot/modules/contrib/lb_carousel`
   - **Priority:** CRITICAL
   - **Sprint:** Sprint 8
   - **Notes:** JavaScript API changed significantly in BS5

4. **lb_modal**
   - **Path:** `docroot/modules/contrib/lb_modal`
   - **Priority:** CRITICAL
   - **Sprint:** Sprint 9
   - **Notes:** Modal API changed significantly in BS5

5. **lb_webform**
   - **Path:** `docroot/modules/contrib/lb_webform`
   - **Priority:** CRITICAL
   - **Sprint:** Sprint 9
   - **Notes:** Form class changes, coordinate with webform_bootstrap

#### Medium Priority (5)
6. **lb_branch_amenities_blocks**
   - **Path:** `docroot/modules/contrib/lb_branch_amenities_blocks`
   - **Sprint:** Sprint 10

7. **lb_branch_hours_blocks**
   - **Path:** `docroot/modules/contrib/lb_branch_hours_blocks`
   - **Sprint:** Sprint 10

8. **lb_branch_social_links_blocks**
   - **Path:** `docroot/modules/contrib/lb_branch_social_links_blocks`
   - **Sprint:** Sprint 10

9. **lb_ping_pong**
   - **Path:** `docroot/modules/contrib/lb_ping_pong`
   - **Sprint:** Sprint 10

10. **lb_promo**
    - **Path:** `docroot/modules/contrib/lb_promo`
    - **Sprint:** Sprint 10

#### Lower Priority (9)
11. **lb_grid_cta** + **lb_grid_icon** (submodule)
    - **Path:** `docroot/modules/contrib/lb_grid_cta`
    - **Sprint:** Sprint 11

12. **lb_partners_blocks**
    - **Path:** `docroot/modules/contrib/lb_partners_blocks`
    - **Sprint:** Sprint 11

13. **lb_related_articles_blocks**
    - **Path:** `docroot/modules/contrib/lb_related_articles_blocks`
    - **Sprint:** Sprint 11

14. **lb_related_events_blocks**
    - **Path:** `docroot/modules/contrib/lb_related_events_blocks`
    - **Sprint:** Sprint 11

15. **lb_simple_menu**
    - **Path:** `docroot/modules/contrib/lb_simple_menu`
    - **Sprint:** Sprint 11

16. **lb_staff_members_blocks**
    - **Path:** `docroot/modules/contrib/lb_staff_members_blocks`
    - **Sprint:** Sprint 12

17. **lb_statistics**
    - **Path:** `docroot/modules/contrib/lb_statistics`
    - **Sprint:** Sprint 12

18. **lb_table**
    - **Path:** `docroot/modules/contrib/lb_table`
    - **Sprint:** Sprint 12
    - **Notes:** Nested tables no longer inherit styles in BS5

19. **lb_testimonial_blocks**
    - **Path:** `docroot/modules/contrib/lb_testimonial_blocks`
    - **Sprint:** Sprint 12

20. **lb_activity_finder**
    - **Path:** `docroot/modules/contrib/yusaopeny_activity_finder/modules/lb_activity_finder`
    - **Sprint:** Sprint 21 (with Activity Finder)
    - **Notes:** Coordinate with Activity Finder migration

---

## 3. WEBSITE SERVICES - SMALL Y (16 modules)

**Parent Module:** ws_small_y
- **Path:** `docroot/modules/contrib/ws_small_y`
- **Bootstrap:** 4.4.1

### Submodules

**High Priority (6):**
1. **small_y_hero** - Sprint 4
2. **small_y_cards** - Sprint 4
3. **small_y_carousels** - Sprint 4
4. **small_y_accordions** - Sprint 4
5. **small_y_alerts** - Sprint 4
6. **small_y_tabs** - Sprint 4

**Medium Priority (10):**
7. **small_y_articles** - Sprint 5
8. **small_y_branch** - Sprint 5
9. **small_y_editor** - Sprint 5
10. **small_y_events** - Sprint 5
11. **small_y_icon_grid** - Sprint 5
12. **small_y_ping_pongs** - Sprint 5
13. **small_y_search** - Sprint 5
14. **ws_small_y_staff** - Sprint 5
15. **ws_small_y_statistics** - Sprint 5
16. **ws_small_y_testimonials** - Sprint 5

---

## 4. ACTIVITY FINDER SYSTEM (3 Vue apps)

⚠️ **CRITICAL:** BootstrapVue 2 NOT compatible with Bootstrap 5

### Activity Finder Apps

1. **openy_af_vue_app** (Activity Finder)
   - **Path:** `docroot/modules/contrib/yusaopeny_activity_finder/openy_af_vue_app`
   - **Bootstrap:** Implicit via BootstrapVue 2.22.0
   - **Vue:** 2.6.10
   - **Sprint:** Sprint 20
   - **Strategy:** Remove BootstrapVue, use Bootstrap 5 vanilla JS

2. **openy_cf_vue_app** (Camp Finder)
   - **Path:** `docroot/modules/contrib/yusaopeny_activity_finder/openy_cf_vue_app`
   - **Bootstrap:** Implicit via BootstrapVue 2.22.0
   - **Vue:** 2.6.10
   - **Sprint:** Sprint 19
   - **Strategy:** Remove BootstrapVue, use Bootstrap 5 vanilla JS

3. **openy_af4_vue_app** (Activity Finder 4)
   - **Path:** `docroot/modules/contrib/yusaopeny_activity_finder/openy_af4_vue_app`
   - **Bootstrap:** 4.6.1 + BootstrapVue 2.22.0
   - **Vue:** 2.6.14
   - **Sprint:** Sprint 21
   - **Strategy:** Remove BootstrapVue, use Bootstrap 5 vanilla JS
   - **Notes:** Most modern implementation

### Activity Finder Isolation
- **Sprint 3:** Isolate with scoped Bootstrap 4 CSS
- **Sprints 19-21:** Full migration to Bootstrap 5

---

## 5. CONTENT TYPE MODULES (10 modules)

### Y Branch & Related (2)
1. **y_branch**
   - **Path:** `docroot/modules/contrib/y_branch`
   - **Sprint:** Sprint 14

2. **y_branch_menu**
   - **Path:** `docroot/modules/contrib/y_branch_menu`
   - **Sprint:** Sprint 14

### Y Program & Camp (3)
3. **y_program**
   - **Path:** `docroot/modules/contrib/y_program`
   - **Sprint:** Sprint 15

4. **y_program_subcategory**
   - **Path:** `docroot/modules/contrib/y_program_subcategory`
   - **Sprint:** Sprint 15

5. **y_camp**
   - **Path:** `docroot/modules/contrib/y_camp`
   - **Sprint:** Sprint 15

### Y Facility & LB (4)
6. **y_facility**
   - **Path:** `docroot/modules/contrib/y_facility`
   - **Sprint:** Sprint 16

7. **y_lb** + **y_lb_main_menu_cta_block** (submodule)
   - **Path:** `docroot/modules/contrib/y_lb`
   - **Sprint:** Sprint 16

8. **y_lb_article**
   - **Path:** `docroot/modules/contrib/y_lb_article`
   - **Sprint:** Sprint 16

### Y Donate (1)
9. **y_donate** + **lb_donate** (submodule)
   - **Path:** `docroot/modules/contrib/y_donate`
   - **Sprint:** Sprint 17

---

## 6. OTHER WEBSITE SERVICES (6 modules)

1. **ws_event**
   - **Path:** `docroot/modules/contrib/ws_event`
   - **Sprint:** Sprint 6

2. **ws_promotion** + submodules
   - **Path:** `docroot/modules/contrib/ws_promotion`
   - **Submodules:** ws_promotion_modal, ws_promotion_activity_finder
   - **Sprint:** Sprint 6

3. **ws_colorway_canada** + **lb_hero_canada**
   - **Path:** `docroot/modules/contrib/ws_colorway_canada`
   - **Sprint:** Sprint 6

4. **ws_lb_tabs**
   - **Path:** `docroot/modules/contrib/ws_lb_tabs`
   - **Sprint:** Sprint 6

5. **ws_home_branch**
   - **Path:** `docroot/modules/contrib/openy_custom/openy_home_branch/modules/ws_home_branch`
   - **Sprint:** Sprint 6

---

## 7. OTHER SUPPORTING MODULES (10+ modules)

### Core Functionality
1. **openy_node_alert**
   - **Path:** `docroot/modules/contrib/openy_node_alert`
   - **Sprint:** Sprint 13

2. **openy_repeat** + **lb_repeat_schedules**
   - **Path:** `docroot/modules/contrib/openy_repeat`
   - **Sprint:** Sprint 13
   - **Notes:** Replace bootstrap-datepicker

3. **openy_map** / **openy_map_lb**
   - **Path:** `docroot/modules/contrib/openy_map`
   - **Sprint:** Sprint 13

4. **openy_calc**
   - **Path:** `docroot/modules/contrib/openy_custom/openy_calc`
   - **Sprint:** Sprint 13

### Contrib Modules (Review for Drupal updates)
5. **bootstrap_layout_builder**
   - **Path:** `docroot/modules/contrib/bootstrap_layout_builder`
   - **Notes:** Uses Bootstrap via SCSS, should inherit from theme

6. **bootstrap_styles**
   - **Path:** `docroot/modules/contrib/bootstrap_styles`
   - **Notes:** Uses Bootstrap via SCSS, should inherit from theme

7. **webform_bootstrap**
   - **Path:** Drupal contrib
   - **Notes:** Check for Bootstrap 5 compatible version

---

## Dependencies Summary

### NPM Dependencies to Update

**From:**
```json
{
  "bootstrap": "^4.4.1",
  "popper.js": "^1.16.0"
}
```

**To:**
```json
{
  "bootstrap": "^5.3.3",
  "@popperjs/core": "^2.11.8"
}
```

### Remove:
- `bootstrap-vue: ^2.22.0` (from 3 Activity Finder apps)
- `popper.js: ^1.16.0` (replaced by @popperjs/core)

---

## Migration Checklist Per Module

For each module, update:
- [ ] `package.json` - Bootstrap 5.3.3, @popperjs/core 2.11.8
- [ ] `webpack.config.js` - Webpack 5 (follow lb_accordion pattern)
- [ ] SCSS files - Bootstrap 5 syntax, deprecated class replacements
- [ ] Twig templates - data-bs-* attributes, class name updates
- [ ] JavaScript - Bootstrap 5 vanilla JS API
- [ ] `.libraries.yml` - Version updates
- [ ] Build and test - `npm run build`

---

## Notes

- **Reference Implementation:** lb_accordion is fully migrated to Bootstrap 5.3.3
- **Unused Modules:** Audit to identify any unused modules that can be skipped
- **Parallel Work:** Modules can be migrated in parallel by multiple developers

---

**Next Steps:**
1. Review this inventory
2. Confirm which modules are actually in use
3. Identify any additional modules not captured
4. Begin Phase 1 (Theme migration)

---

**See Also:**
- [EXECUTIVE_SUMMARY.md](EXECUTIVE_SUMMARY.md)
- [QUICK_START.md](QUICK_START.md)
- [phases/PHASE_1_PREPARATION.md](phases/PHASE_1_PREPARATION.md)
