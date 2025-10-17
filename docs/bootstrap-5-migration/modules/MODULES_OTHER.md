# Other Supporting Modules

**Category:** Supporting & Miscellaneous Modules
**Total Modules:** 16+ modules
**Current Bootstrap:** 4.4.1 (most)
**Target Bootstrap:** 5.3.3
**Migration Phase:** Various (Phases 2-4)
**Priority:** MEDIUM-LOW (most are supporting modules)

---

## Overview

This category includes supporting modules, utility modules, and contributed modules that have Bootstrap dependencies but don't fit into the main categories (Theme, Layout Builder, WS, Activity Finder, Content Types).

**Module Types:**
- Website Services supporting modules (not small_y)
- CRM integrations (ActiveNet, Daxko, GroupEx Pro)
- Search and mapping modules
- Location finder
- Demo content and fixtures
- Admin/developer utilities
- Contributed modules requiring review

---

## Website Services - Other (6 modules)

### 1. ws_event

**Path:** `docroot/modules/contrib/openy_node/modules/openy_node_event/`
**Alternate:** May be under `ws_event/` depending on structure
**Bootstrap:** 4.4.1 → 5.3.3
**Sprint:** Sprint 6
**Phase:** Phase 2

**Description:**
Event management content type and display components for YMCA events (community events, fundraisers, special programs).

**Bootstrap Components Used:**
- Cards (event cards)
- Badges (event type, status)
- Buttons (registration, RSVP)
- Grid system
- Tables (event schedule)
- Modals (event details)

**Key Changes Needed:**
- Card structure updates
- Badge classes: `.badge-*` → `.badge.bg-*`
- Modal data attributes
- Button markup
- Grid classes

**Migration Complexity:** MEDIUM

---

### 2. ws_promotion

**Path:** `docroot/modules/contrib/ws_promotion/`
**Bootstrap:** 4.4.1 → 5.3.3
**Sprint:** Sprint 6
**Phase:** Phase 2

**Description:**
Promotional banner/modal system for highlighting special offers, announcements, and campaigns.

**Submodules:**
- ws_promotion_modal - Modal-based promotions
- ws_promotion_activity_finder - Activity Finder integration

**Bootstrap Components Used:**
- Modals (primary component)
- Cards
- Buttons
- Alerts
- Carousel (for rotating promotions)

**Key Changes Needed:**
- Modal data attributes: `data-toggle="modal"` → `data-bs-toggle="modal"`
- Modal backdrop and positioning
- Alert dismissal: `data-dismiss="alert"` → `data-bs-dismiss="alert"`
- Carousel data attributes
- Button classes

**Migration Complexity:** MEDIUM-HIGH (modals are critical)

**Special Considerations:**
- User-triggered modals must work correctly
- Modal timing/triggers
- Integration with Activity Finder

---

### 3. ws_colorway_canada

**Path:** `docroot/modules/contrib/ws_colorway_canada/`
**Bootstrap:** 4.4.1 → 5.3.3
**Sprint:** Sprint 6
**Phase:** Phase 2

**Description:**
Canada-specific theme variant with customized color scheme and components for YMCA Canada organizations.

**Submodules:**
- lb_hero_canada - Canadian hero component variant

**Bootstrap Components Used:**
- All standard components (theme variant)
- Custom color utilities
- Hero components

**Key Changes Needed:**
- SCSS variable updates for Bootstrap 5 color system
- Update color utility classes
- Test all components with Canada color scheme
- Hero component updates (see lb_hero migration)

**Migration Complexity:** MEDIUM

**Special Considerations:**
- Depends on main theme migration (Phase 1)
- Color scheme must be preserved
- Coordinate with lb_hero migration (Phase 3)

---

### 4. ws_lb_tabs

**Path:** `docroot/modules/contrib/ws_lb_tabs/`
**Bootstrap:** 4.4.1 → 5.3.3
**Sprint:** Sprint 6
**Phase:** Phase 2

**Description:**
Layout Builder tab component (alternative to standard lb_tabs if different).

**Bootstrap Components Used:**
- Tabs/Nav tabs
- Tab content
- Tab panes

**Key Changes Needed:**
- `data-toggle="tab"` → `data-bs-toggle="tab"`
- Nav structure
- Active tab classes
- Tab JavaScript initialization

**Migration Complexity:** MEDIUM

**Note:** Verify if this is duplicate of lb_tabs or different implementation.

---

### 5. ws_home_branch

**Path:** `docroot/modules/contrib/ws_home_branch/`
**Bootstrap:** 4.4.1 → 5.3.3
**Sprint:** Sprint 6
**Phase:** Phase 2

**Description:**
Home branch selector allowing users to choose their preferred YMCA location for personalized content.

**Bootstrap Components Used:**
- Modals (branch selection)
- Dropdowns (branch dropdown)
- Cards (branch options)
- Forms (selection form)
- Buttons

**Key Changes Needed:**
- Modal data attributes
- Dropdown data attributes: `data-toggle="dropdown"` → `data-bs-toggle="dropdown"`
- Form control classes
- Button classes
- Card structure

**Migration Complexity:** MEDIUM

**Special Considerations:**
- Integration with y_branch content type
- Cookie/localStorage for branch preference
- Works with location-based content

---

### 6. ws_blocks (If exists)

**Path:** `docroot/modules/contrib/ws_blocks/` or similar
**Bootstrap:** 4.4.1 → 5.3.3
**Sprint:** Various (based on block types)
**Phase:** Phase 2

**Description:**
Collection of custom blocks for Website Services.

**Bootstrap Components Used:**
- Various (depends on block types)

**Migration Complexity:** VARIES by block type

**Note:** Review individual blocks for Bootstrap usage.

---

## CRM Integration Modules (3+ modules)

### 7. openy_daxko

**Path:** `docroot/profiles/contrib/yusaopeny/modules/custom/openy_daxko/`
**Bootstrap:** Minimal direct usage
**Sprint:** Review only (Phase 4 or 6)
**Phase:** Phase 4-6

**Description:**
Daxko CRM integration for program registration, membership management, and data synchronization.

**Bootstrap Usage:**
- Minimal (mostly backend integration)
- May have form widgets or display components

**Action Required:**
- Review for any Bootstrap-dependent UI components
- Test integration after content type migrations
- Verify form styling if custom widgets exist

**Migration Complexity:** LOW (mostly backend)

**Testing Focus:**
- API integration maintained
- Data sync working
- Registration workflows intact

---

### 8. openy_activenet

**Path:** `docroot/profiles/contrib/yusaopeny/modules/custom/openy_activenet/`
**Bootstrap:** Minimal direct usage
**Sprint:** Review only (Phase 4 or 6)
**Phase:** Phase 4-6

**Description:**
ActiveNet CRM integration for program registration and membership.

**Bootstrap Usage:**
- Minimal (mostly backend integration)
- May have registration buttons/widgets

**Action Required:**
- Review for any Bootstrap-dependent components
- Test registration links and buttons
- Verify integration after Activity Finder migration

**Migration Complexity:** LOW (mostly backend)

---

### 9. openy_groupex_pro

**Path:** `docroot/profiles/contrib/yusaopeny/modules/custom/openy_groupex_pro/`
**Bootstrap:** Minimal direct usage
**Sprint:** Review only (Phase 4 or 6)
**Phase:** Phase 4-6

**Description:**
GroupEx Pro integration for group fitness class scheduling.

**Bootstrap Usage:**
- Class schedule displays may use Bootstrap grids/tables
- Calendar views

**Action Required:**
- Review schedule display templates
- Update table markup if needed
- Test calendar integration

**Migration Complexity:** LOW-MEDIUM

---

## Location & Mapping Modules (2+ modules)

### 10. openy_loc_finder / location_finder

**Path:** `docroot/profiles/contrib/yusaopeny/modules/custom/openy_loc_finder/`
**Bootstrap:** 4.4.1 → 5.3.3
**Sprint:** Sprint 6 or Sprint 14 (coordinate with y_branch)
**Phase:** Phase 2 or 4

**Description:**
Location finder interface for finding nearby YMCA branches with map integration.

**Bootstrap Components Used:**
- Cards (branch result cards)
- List groups (branch lists)
- Modals (branch details)
- Forms (search form)
- Buttons (directions, details)
- Grid system

**Key Changes Needed:**
- Card structure
- List group markup
- Modal data attributes
- Form control classes
- Button markup

**Migration Complexity:** MEDIUM-HIGH

**Integration:**
- Works with y_branch content type
- Map library integration (Leaflet or Google Maps)
- Geolocation API

**Testing:**
- Map display
- Branch search and filtering
- Distance calculations
- Mobile responsive
- Geolocation permissions

---

### 11. openy_map

**Path:** `docroot/profiles/contrib/yusaopeny/modules/custom/openy_map/`
**Bootstrap:** Minimal
**Sprint:** Review only
**Phase:** Phase 2 or 4

**Description:**
Map rendering module (Leaflet or Google Maps integration).

**Bootstrap Usage:**
- Map container styling
- Info windows/popups may use Bootstrap cards

**Action Required:**
- Review info window/popup templates
- Update card markup if used

**Migration Complexity:** LOW

---

## Search Modules (2 modules)

### 12. openy_search

**Path:** `docroot/profiles/contrib/yusaopeny/modules/custom/openy_search/`
**Bootstrap:** 4.4.1 → 5.3.3
**Sprint:** Various (Phase 2-4)
**Phase:** Phase 2-4

**Description:**
Site-wide search functionality with Search API integration.

**Bootstrap Components Used:**
- Forms (search form)
- Input groups (search input with button)
- Cards (search result cards)
- Pagination
- Buttons

**Key Changes Needed:**
- Input group structure changes
- Form control classes
- Card structure
- Pagination markup
- Button classes

**Migration Complexity:** MEDIUM

**Integration:**
- Search API
- Solr (if used)
- View modes for search results

---

### 13. openy_search_api (If separate)

**Path:** `docroot/profiles/contrib/yusaopeny/modules/custom/openy_search_api/`
**Bootstrap:** Minimal
**Sprint:** Review only
**Phase:** Phase 2-4

**Description:**
Search API configuration and integration.

**Bootstrap Usage:**
- Minimal (backend configuration)

**Action Required:**
- Verify search result templates use updated Bootstrap

**Migration Complexity:** LOW

---

## Demo & Development Modules (3+ modules)

### 14. openy_demo_content

**Path:** `docroot/profiles/contrib/yusaopeny/modules/custom/openy_demo_content/`
**Bootstrap:** Indirect usage (creates content)
**Sprint:** Review only (Phase 6)
**Phase:** Phase 6

**Description:**
Demo content for testing and demonstrations.

**Action Required:**
- Regenerate demo content after migration complete
- Test all demo content displays correctly
- Update demo content fixtures if needed

**Migration Complexity:** LOW (content, not code)

**Testing:**
- Install demo content in Bootstrap 5 environment
- Verify all content types display correctly
- Check for any hardcoded Bootstrap 4 markup in fixtures

---

### 15. openy_fixtures

**Path:** `docroot/profiles/contrib/yusaopeny/modules/custom/openy_fixtures/`
**Bootstrap:** Indirect usage
**Sprint:** Review only (Phase 6)
**Phase:** Phase 6

**Description:**
Fixtures and base configurations.

**Action Required:**
- Update fixtures after migration
- Test clean installs with fixtures

**Migration Complexity:** LOW

---

### 16. openy_development

**Path:** `docroot/profiles/contrib/yusaopeny/modules/custom/openy_development/`
**Bootstrap:** N/A
**Sprint:** N/A
**Phase:** N/A

**Description:**
Developer utilities and tools.

**Action Required:**
- None (no Bootstrap dependencies)

**Migration Complexity:** N/A

---

## Contributed Modules to Review

### Modules with Potential Bootstrap Dependencies

The following contributed modules may have Bootstrap-related configuration, theming, or templates that need review:

#### 1. Views Bootstrap (If used)

**Package:** `drupal/views_bootstrap`
**Current:** Check if installed
**Action:** Update to latest version compatible with Bootstrap 5

If installed, this module provides Bootstrap-styled Views display plugins.

**Migration:**
- Update to latest version
- Review all Views using Views Bootstrap display formats
- Test grid displays, carousels, accordions

---

#### 2. Webform Bootstrap (If used)

**Package:** `drupal/webform_bootstrap` or theme-level webform styling
**Current:** Check if used
**Action:** Update templates or disable if theme provides styling

**Migration:**
- Update webform templates to Bootstrap 5 form classes
- Test form validation styling
- Check multi-step forms

---

#### 3. Admin Themes (If using Bootstrap-based)

**Packages:** Various (Claro is default, but check for contrib admin themes)
**Action:** Verify admin theme Bootstrap compatibility

Bootstrap 5 migration should not affect admin interface unless custom admin theme is used.

---

#### 4. Paragraphs with Bootstrap Styling

**Package:** `drupal/paragraphs`
**Current:** Core dependency
**Action:** Review paragraph templates

If paragraph types use Bootstrap markup in templates, update those templates.

---

## Migration Strategy for Other Modules

### Approach 1: Batch by Phase

**Phase 2 (Sprints 4-7):**
- ws_event
- ws_promotion (+ submodules)
- ws_colorway_canada
- ws_lb_tabs
- ws_home_branch
- openy_loc_finder (if scheduling allows)

**Phase 4 (Sprints 14-17):**
- openy_loc_finder (if not in Phase 2)
- openy_search
- CRM integration reviews

**Phase 6 (Sprints 22-24):**
- Demo content regeneration
- Fixture updates
- Final contrib module reviews

---

### Approach 2: Review-Only vs Active Migration

**Active Migration (Sprints 4-6):**
Modules requiring code/template changes:
- ws_event
- ws_promotion
- ws_colorway_canada
- ws_lb_tabs
- ws_home_branch
- openy_loc_finder
- openy_search

**Review-Only (Sprints 14-24):**
Modules requiring verification but minimal changes:
- CRM integrations (openy_daxko, openy_activenet, openy_groupex_pro)
- Map modules
- Demo content modules
- Admin/developer utilities

---

## Common Migration Patterns

### Pattern 1: Modal-Heavy Modules (ws_promotion, ws_home_branch)

**Bootstrap 4:**
```html
<button data-toggle="modal" data-target="#promoModal">Open</button>
<div class="modal" id="promoModal" tabindex="-1">
  ...
</div>
```

**Bootstrap 5:**
```html
<button data-bs-toggle="modal" data-bs-target="#promoModal">Open</button>
<div class="modal" id="promoModal" tabindex="-1">
  ...
</div>
```

**JavaScript:**
```javascript
// Bootstrap 4
$('#promoModal').modal('show');

// Bootstrap 5
const modal = new bootstrap.Modal(document.getElementById('promoModal'));
modal.show();
```

---

### Pattern 2: Event Listing Displays (ws_event)

**Bootstrap 4:**
```html
<div class="card-deck">
  <div class="card">...</div>
</div>
```

**Bootstrap 5:**
```html
<div class="row row-cols-1 row-cols-md-3 g-4">
  <div class="col">
    <div class="card h-100">...</div>
  </div>
</div>
```

---

### Pattern 3: Location Finder Results

**Bootstrap 4:**
```html
<div class="list-group">
  <a href="#" class="list-group-item list-group-item-action">
    <div class="media">
      <img class="mr-3" src="...">
      <div class="media-body">...</div>
    </div>
  </a>
</div>
```

**Bootstrap 5:**
```html
<div class="list-group">
  <a href="#" class="list-group-item list-group-item-action">
    <div class="d-flex">
      <img class="me-3 flex-shrink-0" src="...">
      <div class="flex-grow-1">...</div>
    </div>
  </a>
</div>
```

---

## Testing Requirements

### Integration Testing Focus

**For CRM Modules:**
- Test registration workflows end-to-end
- Verify API integrations maintained
- Check button/link styling
- Test error handling and messages

**For Location Finder:**
- Map display and interaction
- Branch search and filtering
- Geolocation functionality
- Mobile responsive
- Distance calculations

**For Search:**
- Search form functionality
- Result display
- Pagination
- Filtering
- Autocomplete (if present)

**For Promotion Modals:**
- Modal triggers (page load, user action, delay)
- Modal display and dismissal
- Cookie/localStorage for "don't show again"
- Mobile display

---

### Visual Regression Testing

**Key Scenarios:**
- Event listings (card and list views)
- Location finder results + map
- Search results page
- Promotion modals
- Branch selector

**Breakpoints:**
- Mobile: 375px, 414px
- Tablet: 768px, 1024px
- Desktop: 1280px, 1920px

---

## Risk Assessment

### Risk 1: CRM Integration Breaks (MEDIUM)
**Impact:** Registration and membership workflows broken
**Mitigation:**
- Test in sandbox environments
- Coordinate with CRM vendors if possible
- Verify API requests unchanged
- Focus on UI changes only

### Risk 2: Location Finder Mapping Issues (MEDIUM)
**Impact:** Branch search and map display broken
**Mitigation:**
- Test with real map APIs (Leaflet/Google Maps)
- Check geolocation permissions
- Test on mobile devices
- Verify distance calculations

### Risk 3: Promotion Modal Timing (LOW)
**Impact:** Modals may not display correctly or at right time
**Mitigation:**
- Test all trigger types (page load, scroll, delay)
- Check cookie/localStorage logic
- Test dismissal functionality

### Risk 4: Search Relevance Changes (LOW)
**Impact:** Search may behave differently (unlikely from Bootstrap change)
**Mitigation:**
- Test search functionality thoroughly
- Compare results before/after
- Check Search API configuration

---

## Success Criteria

### Technical Requirements:
- [ ] All WS other modules migrated (ws_event, ws_promotion, etc.)
- [ ] CRM integrations tested and working
- [ ] Location finder functional with map
- [ ] Search functionality maintained
- [ ] No JavaScript errors

### Integration Requirements:
- [ ] CRM registration workflows intact
- [ ] Location finder works with y_branch
- [ ] Search works with all content types
- [ ] Promotion modals trigger correctly

### Quality Requirements:
- [ ] Visual appearance matches Bootstrap 4
- [ ] Mobile responsive
- [ ] Accessibility maintained
- [ ] Performance maintained

---

## Dependencies

### Before Other Modules Migration:
- [ ] Phase 1 complete (theme)
- [ ] Theme provides Bootstrap 5.3.3

### Specific Dependencies:
- **ws_colorway_canada:** Depends on theme and lb_hero
- **ws_home_branch:** Depends on y_branch (Phase 4)
- **openy_loc_finder:** Depends on y_branch (Phase 4)
- **CRM integrations:** Depend on y_program, y_camp (Phase 4)

---

## Module-Specific Notes

### ws_promotion Notes:
- Critical for marketing campaigns
- Modal timing is sensitive
- Test with real campaigns if possible
- Coordinate with marketing team for testing

### openy_loc_finder Notes:
- High visibility feature (branch finder)
- Mobile usage is primary
- Geolocation permissions testing required
- Map API costs (if using Google Maps)

### CRM Integration Notes:
- Revenue-impacting (registration workflows)
- Vendor coordination may be needed
- Test in sandbox/staging only
- Have rollback plan

### ws_colorway_canada Notes:
- Canada-specific, affects subset of sites
- Color customization is critical
- Test with actual Canada sites if possible

---

## Related Documents

**Phase Documentation:**
- [Phase 2: Website Services](../phases/PHASE_2_WEBSITE_SERVICES.md)
- [Phase 4: Content Types](../phases/PHASE_4_CONTENT_TYPES.md)
- [Phase 6: Testing & Rollout](../phases/PHASE_6_TESTING_ROLLOUT.md)

**Sprint Documentation:**
- [Sprint 6: Other WS Modules](../sprints/SPRINT_06_WS_Other_Modules.md)
- [Sprint 14-17: Content Types](../sprints/) (for CRM testing)
- [Sprint 22-24: Testing & Rollout](../sprints/)

**Related Module Documentation:**
- [Content Type Modules](MODULES_CONTENT_TYPES.md) - y_branch, y_program dependencies
- [Theme Module](MODULES_THEME.md) - ws_colorway_canada dependency

**Reference Materials:**
- [Bootstrap 5 Cheatsheet](../reference/BOOTSTRAP_5_CHEATSHEET.md)
- [Migration Checklist Template](../reference/MIGRATION_CHECKLIST_TEMPLATE.md)
- [Troubleshooting Guide](../reference/TROUBLESHOOTING.md)

---

**Document Status:** ✅ Complete
**Last Updated:** 2025-10-17
**Modules Documented:** 16+
**Priority:** MEDIUM-LOW (supporting modules)
**Total Lines:** < 999
