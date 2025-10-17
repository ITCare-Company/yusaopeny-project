# Content Type Modules

**Category:** Y Content Types
**Total Modules:** 10 modules
**Current Bootstrap:** 4.4.1
**Target Bootstrap:** 5.3.3
**Migration Phase:** Phase 4
**Sprints:** 14-17

---

## Overview

The Y Content Type modules provide Drupal content types (node types) for various YMCA-specific content like branches, programs, camps, facilities, articles, and donations. These modules define entity structures, form displays, view displays, and related functionality.

**Key Characteristics:**
- Drupal entity definitions (content types)
- Form displays (node edit forms)
- View displays (node view modes)
- Custom fields and field widgets
- Display templates (Twig)
- May integrate with Layout Builder
- Bootstrap used primarily in display templates

**Migration Focus:**
- Twig template updates
- Form widget styling
- View display rendering
- Integration with Layout Builder modules

---

## Module List by Category

### Branch-Related Modules (2 modules)

#### 1. y_branch

**Path:** `docroot/profiles/contrib/yusaopeny/modules/custom/openy_node/modules/openy_node_branch/`
**Bootstrap:** 4.4.1 → 5.3.3
**Sprint:** Sprint 14

**Description:**
Defines the Branch content type for YMCA branch/location pages. Includes location information, hours, amenities, and integration with mapping.

**Content Type:** `node--branch`

**Key Fields:**
- Branch location (address, map coordinates)
- Hours of operation
- Amenities (parking, childcare, pool, etc.)
- Contact information
- Branch image/gallery
- Description/about text

**Bootstrap Components Used:**
- Cards (amenity displays)
- Grid system (branch info layout)
- Tables (hours display)
- List groups (amenities list)
- Media objects (contact info with icons)

**Display Modes:**
- Full page display
- Teaser (location finder results)
- Card (branch selector)
- Embedded (in blocks)

**Key Templates:**
- `node--branch.html.twig`
- `node--branch--teaser.html.twig`
- `node--branch--card.html.twig`
- Field templates for hours, amenities, location

**Migration Complexity:** MEDIUM
**Integration:** Works with `ws_home_branch`, location finder

**Key Changes Needed:**
- Update media object markup (removed in BS5)
- Spacing utilities: `.ml-*` → `.ms-*`, `.mr-*` → `.me-*`
- Card structure updates
- Table responsive classes
- List group markup

---

#### 2. y_branch_menu

**Path:** `docroot/profiles/contrib/yusaopeny/modules/custom/openy_node/modules/openy_node_branch/`
**Alternate Path:** May be part of y_branch or separate custom module
**Bootstrap:** 4.4.1 → 5.3.3
**Sprint:** Sprint 14

**Description:**
Provides branch-specific menu functionality, allowing different branches to have customized navigation.

**Bootstrap Components Used:**
- Navbar
- Dropdowns
- Nav items

**Key Changes Needed:**
- Navbar structure updates (minor changes in BS5)
- Dropdown data attributes: `data-toggle="dropdown"` → `data-bs-toggle="dropdown"`
- Nav item classes

**Migration Complexity:** LOW-MEDIUM

**Note:** May be integrated directly into y_branch rather than separate module. Verify module structure during Sprint 14.

---

### Program-Related Modules (3 modules)

#### 3. y_program

**Path:** `docroot/profiles/contrib/yusaopeny/modules/custom/openy_node/modules/openy_node_program/`
**Bootstrap:** 4.4.1 → 5.3.3
**Sprint:** Sprint 15

**Description:**
Defines the Program content type for YMCA programs (fitness classes, swim lessons, youth sports, etc.). Core content type for Activity Finder integration.

**Content Type:** `node--program`

**Key Fields:**
- Program category/subcategory
- Age range
- Difficulty level
- Description
- Image/media
- Registration links
- Schedule/session information
- Instructor information
- Location (which branch)

**Bootstrap Components Used:**
- Cards (program display)
- Badges (category, difficulty, age labels)
- Grid system
- Buttons (registration CTAs)
- Tables (schedule display)

**Display Modes:**
- Full page
- Teaser (Activity Finder results)
- Card (program cards)
- Embedded

**Key Templates:**
- `node--program.html.twig`
- `node--program--teaser.html.twig`
- `node--program--card.html.twig`
- Field templates for category, schedule, instructor

**Migration Complexity:** MEDIUM-HIGH

**Integration:** Critical for Activity Finder apps

**Key Changes Needed:**
- Card deck replacement (if used)
- Badge classes
- Button markup
- Table responsive classes
- Grid column classes
- Spacing utilities

**Special Considerations:**
- High volume content type (thousands of programs)
- Performance critical
- Activity Finder dependency

---

#### 4. y_program_subcategory

**Path:** `docroot/profiles/contrib/yusaopeny/modules/custom/openy_taxonomy/modules/openy_txnm_program_subcategory/`
**Type:** Taxonomy vocabulary module
**Bootstrap:** 4.4.1 → 5.3.3
**Sprint:** Sprint 15

**Description:**
Taxonomy vocabulary for program subcategories. Used for filtering and organizing programs.

**Taxonomy:** `program_subcategory`

**Bootstrap Components Used:**
- Badges (term labels)
- Nav pills (filter interface)
- Dropdowns (category selectors)

**Display Context:**
- Program filters
- Category pages
- Breadcrumbs

**Migration Complexity:** LOW

**Key Changes Needed:**
- Badge markup
- Nav pills structure
- Dropdown data attributes

---

#### 5. y_camp

**Path:** `docroot/profiles/contrib/yusaopeny/modules/custom/openy_node/modules/openy_node_camp/`
**Bootstrap:** 4.4.1 → 5.3.3
**Sprint:** Sprint 15

**Description:**
Defines the Camp content type for summer camps, day camps, and camp programs. Used by Camp Finder app.

**Content Type:** `node--camp`

**Key Fields:**
- Camp type (day, overnight, specialty)
- Age range
- Dates/sessions
- Description
- Activities included
- Cost/registration
- Location
- Image/media

**Bootstrap Components Used:**
- Cards (camp display)
- Badges (camp type, age labels)
- Grid system
- Buttons (registration)
- Collapse (session details)
- Modals (detailed info)

**Display Modes:**
- Full page
- Teaser (Camp Finder results)
- Card
- Embedded

**Key Templates:**
- `node--camp.html.twig`
- `node--camp--teaser.html.twig`
- `node--camp--card.html.twig`

**Migration Complexity:** MEDIUM-HIGH

**Integration:** Critical for Camp Finder app (openy_cf_vue_app)

**Key Changes Needed:**
- Card structure
- Badge markup
- Modal data attributes: `data-toggle="modal"` → `data-bs-toggle="modal"`
- Collapse data attributes: `data-toggle="collapse"` → `data-bs-toggle="collapse"`
- Button classes
- Grid system

---

### Facility & Content Modules (3 modules)

#### 6. y_facility

**Path:** `docroot/profiles/contrib/yusaopeny/modules/custom/openy_node/modules/openy_node_facility/`
**Bootstrap:** 4.4.1 → 5.3.3
**Sprint:** Sprint 16

**Description:**
Defines the Facility content type for specific facilities within branches (pools, gyms, studios, tracks, etc.).

**Content Type:** `node--facility`

**Key Fields:**
- Facility type
- Location (branch)
- Description
- Amenities
- Hours
- Image/media

**Bootstrap Components Used:**
- Cards
- List groups (amenities)
- Grid system
- Icons (font-based with Bootstrap utilities)

**Display Modes:**
- Full page
- Teaser
- Card
- Embedded in branch pages

**Key Templates:**
- `node--facility.html.twig`
- `node--facility--teaser.html.twig`

**Migration Complexity:** MEDIUM

**Key Changes Needed:**
- Card structure
- List group markup
- Grid classes
- Spacing utilities

---

#### 7. y_lb (Layout Builder Content)

**Path:** `docroot/profiles/contrib/yusaopeny/modules/custom/openy_node/modules/openy_node_lb/`
**Bootstrap:** 4.4.1 → 5.3.3
**Sprint:** Sprint 16

**Description:**
Generic Layout Builder content type allowing flexible page building with Layout Builder modules.

**Content Type:** `node--lb`

**Key Fields:**
- Layout Builder field (layout sections)
- Meta fields (title, summary, image)

**Bootstrap Components Used:**
- All Layout Builder components (lb_hero, lb_cards, lb_accordion, etc.)
- Grid system (via Layout Builder)
- Depends on Layout Builder module migrations

**Display Modes:**
- Full page (Layout Builder rendering)

**Migration Complexity:** LOW (depends on LB modules)

**Integration:** Depends on all Phase 3 Layout Builder module migrations

**Key Changes Needed:**
- Ensure Layout Builder modules are migrated first (Phase 3)
- Test all Layout Builder components together
- Check for any custom templates

**Dependencies:**
- Phase 3 (Layout Builder modules) must be complete

---

#### 8. y_lb_article

**Path:** `docroot/profiles/contrib/yusaopeny/modules/custom/openy_node/modules/openy_node_article/`
**Bootstrap:** 4.4.1 → 5.3.3
**Sprint:** Sprint 16

**Description:**
Article content type with Layout Builder support for rich blog/news content.

**Content Type:** `node--article`

**Key Fields:**
- Layout Builder field
- Article body
- Author
- Date
- Category/tags
- Featured image
- Related content

**Bootstrap Components Used:**
- Cards (article teasers)
- Grid system (article lists)
- Media objects (author info - deprecated in BS5)
- Breadcrumbs
- Pagination (article lists)

**Display Modes:**
- Full page (Layout Builder)
- Teaser (article lists)
- Card

**Key Templates:**
- `node--article.html.twig`
- `node--article--teaser.html.twig`

**Migration Complexity:** MEDIUM

**Key Changes Needed:**
- Replace media objects with flex utilities
- Card structure updates
- Grid classes
- Breadcrumb markup (minor changes)
- Pagination classes

---

### Donation Module (2 modules)

#### 9. y_donate

**Path:** `docroot/profiles/contrib/yusaopeny/modules/custom/openy_node/modules/openy_node_donate/`
**Bootstrap:** 4.4.1 → 5.3.3
**Sprint:** Sprint 17

**Description:**
Donation form content type for YMCA fundraising and giving campaigns.

**Content Type:** `node--donate`

**Key Fields:**
- Donation description
- Suggested amounts
- Custom amount option
- Payment processor integration
- Thank you message
- Goal tracking

**Bootstrap Components Used:**
- Forms (donation form)
- Input groups (currency input)
- Buttons (amount selection, submit)
- Cards (donation tiers)
- Progress bars (campaign goals)
- Modals (confirmation, thank you)

**Display Modes:**
- Full page
- Embedded (donation blocks)

**Key Templates:**
- `node--donate.html.twig`
- Form templates for donation form

**Migration Complexity:** MEDIUM-HIGH

**Special Considerations:**
- Payment integration critical (must not break)
- Security-sensitive (form validation)
- Accessibility critical (form fields, labels, errors)

**Key Changes Needed:**
- Form control classes
- Input group structure
- Button classes
- Card structure
- Progress bar markup
- Modal data attributes: `data-toggle="modal"` → `data-bs-toggle="modal"`
- Focus on form validation styling

---

#### 10. y_donate_form (If separate)

**Path:** May be integrated into y_donate or separate form module
**Bootstrap:** 4.4.1 → 5.3.3
**Sprint:** Sprint 17

**Description:**
Dedicated donation form builder/handler.

**Bootstrap Components Used:**
- All form components
- Form validation styles
- Input groups
- Buttons

**Migration Complexity:** MEDIUM

**Key Changes Needed:**
- Form validation classes (`.was-validated`, `.is-invalid`)
- Form control sizing
- Input group addon structure
- Button states

---

## Migration Patterns for Content Types

### Pattern 1: Node Template Updates

**Bootstrap 4 Template:**
```twig
<article{{ attributes.addClass('node', 'node--' ~ node.bundle) }}>
  <div class="node__content">
    <div class="media">
      <img class="mr-3" src="{{ image_url }}">
      <div class="media-body">
        {{ content.body }}
      </div>
    </div>
  </div>
</article>
```

**Bootstrap 5 Template:**
```twig
<article{{ attributes.addClass('node', 'node--' ~ node.bundle) }}>
  <div class="node__content">
    <div class="d-flex">
      <img class="me-3 flex-shrink-0" src="{{ image_url }}">
      <div class="flex-grow-1">
        {{ content.body }}
      </div>
    </div>
  </div>
</article>
```

**Changes:**
- `.media` → `.d-flex`
- `.mr-3` → `.me-3`
- `.media-body` → `.flex-grow-1`
- Add `.flex-shrink-0` to image

---

### Pattern 2: Card-Based Displays

**Bootstrap 4:**
```twig
<div class="card-deck">
  {% for item in items %}
    <div class="card">
      <img class="card-img-top" src="{{ item.image }}">
      <div class="card-body">
        <h5 class="card-title">{{ item.title }}</h5>
        <p class="card-text">{{ item.body }}</p>
      </div>
    </div>
  {% endfor %}
</div>
```

**Bootstrap 5:**
```twig
<div class="row row-cols-1 row-cols-md-3 g-4">
  {% for item in items %}
    <div class="col">
      <div class="card h-100">
        <img class="card-img-top" src="{{ item.image }}">
        <div class="card-body">
          <h5 class="card-title">{{ item.title }}</h5>
          <p class="card-text">{{ item.body }}</p>
        </div>
      </div>
    </div>
  {% endfor %}
</div>
```

**Changes:**
- `.card-deck` removed → use grid system
- Add `.row`, `.row-cols-*`, `.g-4` for grid
- Wrap cards in `.col`
- Add `.h-100` to cards for equal height

---

### Pattern 3: Form Display Updates

**Bootstrap 4 Field Widget:**
```twig
<div class="form-group">
  <label for="edit-title">{{ 'Title'|t }}</label>
  <input type="text" id="edit-title" class="form-control">
  <small class="form-text text-muted">{{ description }}</small>
</div>
```

**Bootstrap 5 Field Widget:**
```twig
<div class="mb-3">
  <label for="edit-title" class="form-label">{{ 'Title'|t }}</label>
  <input type="text" id="edit-title" class="form-control">
  <div class="form-text">{{ description }}</div>
</div>
```

**Changes:**
- `.form-group` → `.mb-3` (or other spacing utility)
- Add `.form-label` to labels
- `.form-text.text-muted` → `.form-text` (muted is default)

---

### Pattern 4: Badge Usage

**Bootstrap 4:**
```twig
<span class="badge badge-primary">{{ category }}</span>
<span class="badge badge-pill badge-secondary">{{ age_range }}</span>
```

**Bootstrap 5:**
```twig
<span class="badge bg-primary">{{ category }}</span>
<span class="badge rounded-pill bg-secondary">{{ age_range }}</span>
```

**Changes:**
- `.badge-primary` → `.badge.bg-primary`
- `.badge-pill` → `.badge.rounded-pill`
- All contextual `.badge-*` → `.badge.bg-*`

---

## Sprint Groupings

### Sprint 14: Branch-Related (Modules: 2)

**Modules:**
1. y_branch
2. y_branch_menu

**Focus:**
- Location display templates
- Hours/amenities formatting
- Integration with location finder
- Branch selector components

**Testing:**
- Location finder integration
- Branch page layouts
- Amenity displays
- Contact information display

---

### Sprint 15: Program & Camp (Modules: 3)

**Modules:**
1. y_program
2. y_program_subcategory
3. y_camp

**Focus:**
- Program display cards
- Camp Finder integration
- Activity Finder integration
- Category/filter displays

**Testing:**
- Activity Finder integration (critical)
- Camp Finder integration (critical)
- Program listings
- Category filtering
- Performance with large datasets

**Special Attention:**
- These are high-volume content types
- Critical for Activity/Camp Finder apps

---

### Sprint 16: Facility & Layout Builder Content (Modules: 3)

**Modules:**
1. y_facility
2. y_lb
3. y_lb_article

**Focus:**
- Facility displays
- Layout Builder integration
- Article layouts

**Testing:**
- Layout Builder integration (depends on Phase 3)
- Article listings
- Facility embeds in branch pages

**Dependencies:**
- Phase 3 Layout Builder modules must be complete

---

### Sprint 17: Donation & Testing (Modules: 2)

**Modules:**
1. y_donate
2. y_donate_form (if separate)

**Focus:**
- Donation forms (critical - payment integration)
- Form validation
- Payment processor integration
- Security testing

**Testing:**
- Form submissions
- Payment integration (sandbox/test mode)
- Validation error displays
- Accessibility (forms are critical)
- Security review

**Special Attention:**
- Payment-sensitive forms
- Must not break existing donations
- Accessibility is critical
- Security review required

---

## Testing Requirements

### Visual Regression Testing
**Tool:** BackstopJS

**Test Scenarios per Content Type:**
- Full page display
- Teaser display
- Card display
- Embedded display
- Edit form (if Bootstrap-styled)

**Breakpoints:**
- Mobile: 375px
- Tablet: 768px
- Desktop: 1920px

---

### Functional Testing
**Tool:** Behat (if exists) or manual QA

**Test Cases:**
- Content creation (node add forms)
- Content editing
- Content display (all view modes)
- Integration with Activity/Camp Finder
- Integration with Layout Builder
- Donation form submissions (y_donate)

---

### Accessibility Testing
**Tool:** Pa11y

**Focus:**
- Form labels and descriptions
- Keyboard navigation
- Screen reader compatibility
- Color contrast (especially badges, buttons)
- Donation forms (critical)

---

## Risk Assessment

### Risk 1: Activity/Camp Finder Integration (HIGH)
**Impact:** Breaks program/camp search if content type changes break Activity Finder
**Mitigation:**
- Test with Activity Finder apps during Sprint 15
- Coordinate with Phase 5 (Activity Finder migration)
- Maintain field structure compatibility
- Test API responses if Activity Finder uses JSON:API

### Risk 2: Layout Builder Dependencies (MEDIUM)
**Impact:** y_lb and y_lb_article depend on Layout Builder modules
**Mitigation:**
- Complete Phase 3 (Layout Builder) before Sprint 16
- Test all Layout Builder components with these content types
- Integration testing required

### Risk 3: Donation Form Breaks (HIGH)
**Impact:** Payment processing could break, affecting revenue
**Mitigation:**
- Extensive testing in Sprint 17
- Test payment processor integration in sandbox mode
- Security review required
- Accessibility testing critical
- Have rollback plan ready

### Risk 4: High-Volume Content Performance (MEDIUM)
**Impact:** Programs and camps have thousands of nodes
**Mitigation:**
- Performance testing with realistic datasets
- Test view displays with large result sets
- Check for N+1 query issues
- Monitor bundle size increases

---

## Success Criteria

### Technical Requirements:
- [ ] All 10 content type modules migrated
- [ ] All view displays render correctly
- [ ] All form displays styled correctly
- [ ] No JavaScript errors
- [ ] No CSS rendering issues

### Integration Requirements:
- [ ] Activity Finder integration maintained
- [ ] Camp Finder integration maintained
- [ ] Layout Builder integration working
- [ ] Branch/facility relationships working

### Quality Requirements:
- [ ] Visual appearance matches Bootstrap 4
- [ ] Accessibility maintained (WCAG 2.2 AA)
- [ ] Form validation working correctly
- [ ] Payment integration working (y_donate)
- [ ] Performance maintained

### Content Requirements:
- [ ] All view modes work (full, teaser, card, embedded)
- [ ] Content migration not required (templates only)
- [ ] Existing content displays correctly

---

## Dependencies

### Before Content Type Migration:
- [ ] Phase 1 complete (theme)
- [ ] Phase 2 complete (WS modules)
- [ ] Phase 3 complete (Layout Builder modules) - before Sprint 16

### Before Phase 5 (Activity Finder):
- [ ] y_program and y_camp migrated (Sprint 15)
- [ ] Content type display templates working
- [ ] Field API compatibility maintained

---

## Related Documents

**Phase Documentation:**
- [Phase 4: Content Types](../phases/PHASE_4_CONTENT_TYPES.md)

**Sprint Documentation:**
- [Sprint 14: Y Branch & Related](../sprints/SPRINT_14_Y_Branch.md)
- [Sprint 15: Y Program & Camp](../sprints/SPRINT_15_Y_Program_Camp.md)
- [Sprint 16: Y Facility & LB](../sprints/SPRINT_16_Y_Facility_LB.md)
- [Sprint 17: Y Donate & Testing](../sprints/SPRINT_17_Y_Donate.md)

**Related Module Documentation:**
- [Layout Builder Modules](MODULES_LAYOUT_BUILDER.md) - Phase 3 dependency
- [Activity Finder Apps](MODULES_ACTIVITY_FINDER.md) - Phase 5 integration

**Reference Materials:**
- [Bootstrap 5 Cheatsheet](../reference/BOOTSTRAP_5_CHEATSHEET.md)
- [Migration Checklist Template](../reference/MIGRATION_CHECKLIST_TEMPLATE.md)
- [Troubleshooting Guide](../reference/TROUBLESHOOTING.md)

---

**Document Status:** ✅ Complete
**Last Updated:** 2025-10-17
**Modules Documented:** 10
**Total Lines:** < 999
