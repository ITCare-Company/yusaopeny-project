# Phase 4: Content Type Modules

**Duration:** 8 weeks (Sprints 14-17)
**Status:** Not Started
**Goal:** Migrate all content type modules to Bootstrap 5

---

## Overview

Phase 4 focuses on migrating content type modules - the structured content types that power YMCA location pages, programs, camps, facilities, events, and donations. These modules provide the data models and display templates that integrate with Layout Builder modules from Phase 3.

**Key Challenge:** Content types rely heavily on Layout Builder modules, so Phase 3 must be stable before starting Phase 4.

**Key Strategy:** Group by functional domain (locations, programs, events) and migrate in logical batches.

---

## Sprints in This Phase

### Sprint 14: Location & Branch Modules
**Modules (3):** Core location functionality
- y_branch (YMCA branches/locations)
- y_branch_redirect (branch redirects)
- y_location (location taxonomy)

**See:** [sprints/SPRINT_14_Location_Branch.md](../sprints/SPRINT_14_Location_Branch.md)

### Sprint 15: Program & Activity Modules
**Modules (3):** Program and activity content
- y_program (programs content type)
- y_program_subcategory (program taxonomy)
- y_lb (Landing page content type)

**See:** [sprints/SPRINT_15_Program_Activity.md](../sprints/SPRINT_15_Program_Activity.md)

### Sprint 16: Events, Camps & Facilities
**Modules (3):** Additional content types
- y_camp (camp content type)
- y_event (event content type)
- y_facility (facility content type)

**See:** [sprints/SPRINT_16_Events_Camps_Facilities.md](../sprints/SPRINT_16_Events_Camps_Facilities.md)

### Sprint 17: Donation Module & Testing
**Modules (1):** Donation + integration testing
- y_donate (donation content type)
- Integration testing of all content types
- Testing with Layout Builder modules
- Phase 4 completion

**See:** [sprints/SPRINT_17_Donation_Testing.md](../sprints/SPRINT_17_Donation_Testing.md)

---

## Key Deliverables

### Sprint 14 Deliverables
- [ ] y_branch module migrated
- [ ] Branch finder functionality maintained
- [ ] Location pages display correctly
- [ ] Branch redirects work
- [ ] Location taxonomy updated

### Sprint 15 Deliverables
- [ ] y_program module migrated
- [ ] Program pages display correctly
- [ ] Program subcategory taxonomy works
- [ ] y_lb landing pages migrated
- [ ] Layout Builder integration tested

### Sprint 16 Deliverables
- [ ] y_camp module migrated
- [ ] y_event module migrated
- [ ] y_facility module migrated
- [ ] All content type displays working
- [ ] Content listings functional

### Sprint 17 Deliverables
- [ ] y_donate module migrated
- [ ] Donation forms styled correctly
- [ ] All 10 content type modules tested together
- [ ] Integration with Layout Builder verified
- [ ] Visual regression tests passed
- [ ] Accessibility tests passed
- [ ] Phase 4 documentation complete
- [ ] GO/NO-GO decision for Phase 5

---

## Components in This Phase

### Content Type Modules (10 modules)

**Location & Branch (3 modules) - Sprint 14:**
1. **y_branch** - Branch/location content type
   - Branch finder integration
   - Location pages
   - Branch-specific content
   - Integration with Activity Finder (still on BS4 - isolated)

2. **y_branch_redirect** - Branch redirect management
   - Redirect logic
   - User location detection

3. **y_location** - Location taxonomy
   - Location categories
   - Location filtering

**Program & Activity (3 modules) - Sprint 15:**
4. **y_program** - Program content type
   - Program pages
   - Program displays
   - Integration with Activity Finder (still on BS4 - isolated)

5. **y_program_subcategory** - Program subcategory taxonomy
   - Program categorization
   - Program filtering

6. **y_lb** - Landing page content type
   - Layout Builder integration (critical)
   - Custom landing pages
   - Uses LB modules from Phase 3

**Events, Camps & Facilities (3 modules) - Sprint 16:**
7. **y_camp** - Camp content type
   - Camp pages
   - Camp registration integration
   - Integration with Camp Finder (will migrate in Phase 5)

8. **y_event** - Event content type
   - Event pages
   - Event calendar integration
   - Event registration

9. **y_facility** - Facility content type
   - Facility pages
   - Facility amenities
   - Facility schedules

**Donation (1 module) - Sprint 17:**
10. **y_donate** - Donation content type
    - Donation pages
    - Donation forms
    - Payment integration (styling only - no payment logic changes)

---

## Success Criteria

### Technical
- [ ] All 10 content type modules migrated to Bootstrap 5.3.3
- [ ] All modules build without errors
- [ ] Content displays maintained
- [ ] Taxonomy terms display correctly
- [ ] Forms styled correctly
- [ ] No JavaScript console errors
- [ ] Layout Builder integration functional

### Quality
- [ ] Visual regression tests passed (all content types)
- [ ] Accessibility maintained (WCAG 2.2 AA)
- [ ] Content listings responsive
- [ ] Detail pages responsive
- [ ] Forms accessible and keyboard-navigable
- [ ] Cross-browser compatibility verified

### Integration
- [ ] Layout Builder modules work with content types
- [ ] Activity Finder integration maintained (still BS4 - isolated)
- [ ] Camp Finder integration maintained (still BS4 - isolated)
- [ ] Branch finder functional
- [ ] Event calendar functional
- [ ] Donation forms functional

### Process
- [ ] Content type migration patterns documented
- [ ] Field display templates documented
- [ ] Known issues documented
- [ ] Content type testing matrix complete

---

## Risks & Mitigation

### Risk 1: Layout Builder Integration Issues (HIGH)
**Impact:** HIGH - Content types may not render correctly
**Probability:** MEDIUM
**Affected Modules:** y_lb (primary), all others (secondary)
**Mitigation:**
- y_lb is most critical - test extensively with LB modules
- Verify Phase 3 LB modules are stable before starting Phase 4
- Test each content type with multiple LB components
- Create test pages with realistic content
- Document Layout Builder module dependencies
- Test in both edit and view modes

**Testing Checklist:**
- [ ] LB modules render in content type pages
- [ ] Multiple LB components on same page
- [ ] LB component configuration preserved
- [ ] LB inline editing works
- [ ] LB component reordering works

### Risk 2: Activity Finder / Camp Finder Conflicts (MEDIUM)
**Impact:** HIGH - Finders may break
**Probability:** LOW (with proper isolation)
**Affected Modules:** y_branch, y_program, y_camp
**Mitigation:**
- Activity Finder isolated in Phase 1 with scoped Bootstrap 4 CSS
- Camp Finder will be isolated in Phase 5
- Verify isolation still works in each sprint
- Test branch/program pages with Activity Finder embedded
- Test camp pages with placeholder for Camp Finder
- Document isolation requirements

**Isolation Verification:**
- [ ] Activity Finder still uses Bootstrap 4 styles
- [ ] No Bootstrap 5 styles leak into Activity Finder
- [ ] No Bootstrap 4 styles leak out of Activity Finder
- [ ] Activity Finder JavaScript still works
- [ ] Page layout not affected by Activity Finder isolation

### Risk 3: Form Styling Inconsistencies (MEDIUM)
**Impact:** MEDIUM - Forms may look inconsistent
**Probability:** MEDIUM
**Affected Modules:** y_donate (primary), y_event, y_camp (secondary)
**Mitigation:**
- Establish form styling standards in Sprint 14
- Use Drupal's form theming system consistently
- Test all form elements (text, select, checkbox, radio, date, etc.)
- Test form validation states
- Test error messages
- Document form styling patterns

**Form Testing Checklist:**
- [ ] Text inputs styled correctly
- [ ] Select dropdowns styled correctly
- [ ] Checkboxes and radios styled correctly
- [ ] Date inputs styled correctly
- [ ] Required field indicators visible
- [ ] Validation messages styled correctly
- [ ] Error states styled correctly
- [ ] Submit buttons styled correctly
- [ ] Form layout responsive

### Risk 4: Taxonomy Display Issues (LOW)
**Impact:** LOW - Taxonomy terms may not display correctly
**Probability:** LOW
**Affected Modules:** y_location, y_program_subcategory
**Mitigation:**
- Test taxonomy term pages
- Test taxonomy listings
- Test taxonomy filtering
- Test taxonomy in views
- Verify taxonomy term displays in content

### Risk 5: Branch Finder Regression (LOW)
**Impact:** MEDIUM - Branch finder may not work
**Probability:** LOW
**Affected Modules:** y_branch, y_branch_redirect
**Mitigation:**
- Test branch finder early in Sprint 14
- Verify geolocation still works
- Test branch finder on mobile
- Test branch redirect logic
- Document branch finder dependencies

---

## Testing Strategy

### Standard Testing (All Sprints)
**For All Content Types:**
- Visual regression testing (BackstopJS)
- Accessibility testing (Pa11y)
- Responsive testing (all breakpoints)
- Manual cross-browser testing

### Content Type Specific Testing

**Per Content Type:**
- [ ] Content type add/edit forms
- [ ] Content type display (full view)
- [ ] Content type display (teaser view)
- [ ] Content type listings
- [ ] Content type search/filtering
- [ ] Field displays (all field formatters)
- [ ] Responsive displays

**y_branch Specific:**
- [ ] Branch finder functionality
- [ ] Branch pages with Activity Finder
- [ ] Branch redirects
- [ ] Location taxonomy filtering
- [ ] Branch amenities display
- [ ] Branch hours display
- [ ] Branch contact information

**y_program Specific:**
- [ ] Program pages with Activity Finder
- [ ] Program category filtering
- [ ] Program subcategory filtering
- [ ] Program schedules
- [ ] Program registration links

**y_lb Specific (CRITICAL):**
- [ ] Layout Builder module integration
- [ ] Multiple LB components on page
- [ ] LB component configuration
- [ ] LB inline editing
- [ ] LB component library
- [ ] Custom layouts
- [ ] Responsive layouts

**y_camp Specific:**
- [ ] Camp pages
- [ ] Camp session display
- [ ] Camp registration links
- [ ] Camp finder placeholder (will be migrated in Phase 5)

**y_event Specific:**
- [ ] Event pages
- [ ] Event calendar views
- [ ] Event registration
- [ ] Event date/time display
- [ ] Event location display

**y_facility Specific:**
- [ ] Facility pages
- [ ] Facility amenities
- [ ] Facility schedules
- [ ] Facility location information

**y_donate Specific:**
- [ ] Donation form display
- [ ] Donation amount selection
- [ ] Donation frequency selection
- [ ] Donation payment integration (styling only)
- [ ] Donation confirmation page

### Integration Testing (Sprint 17)
**All Content Types Together:**
- [ ] Multiple content types on site
- [ ] Content type listings
- [ ] Content type search
- [ ] Content type views
- [ ] Layout Builder across content types
- [ ] Activity Finder on multiple content types
- [ ] Navigation across content types
- [ ] Taxonomy across content types

---

## Resources

### Team
- 1 Full-time Frontend Developer
- Optional: Content Editor for test content creation
- Part-time QA for testing support (Sprint 17)

### Tools
- Node.js 16+
- Webpack 5
- BackstopJS (visual regression)
- Pa11y (accessibility)
- Docksal/DDEV (local environment)

### Reference Materials
- Phase 3 Layout Builder modules (integration)
- Drupal field theming documentation
- Drupal form theming documentation
- Activity Finder isolation documentation (from Phase 1)

### Test Content
- Sample branches (at least 5)
- Sample programs (at least 10)
- Sample camps (at least 3)
- Sample events (at least 5)
- Sample facilities (at least 3)
- Sample landing pages with LB components (at least 5)
- Sample donation pages (at least 2)

### Time
- Sprint 14: 2 weeks (3 location/branch modules)
- Sprint 15: 2 weeks (3 program/activity modules)
- Sprint 16: 2 weeks (3 events/camps/facilities modules)
- Sprint 17: 2 weeks (1 donation module + testing)
- **Total: 8 weeks**

---

## Dependencies

### Before Phase 4 Can Start:
- [x] Phase 1 complete (theme migrated)
- [x] Phase 2 complete (WS modules migrated)
- [x] Phase 3 complete (LB modules migrated - CRITICAL)
- [x] Activity Finder isolated
- [x] Testing infrastructure working
- [ ] GO/NO-GO decision from Phase 3

### Before Phase 5 Can Start:
- [ ] All 10 content type modules migrated
- [ ] Layout Builder integration verified
- [ ] Activity Finder integration verified
- [ ] Integration testing passed
- [ ] Visual regression tests passed
- [ ] Accessibility tests passed
- [ ] Test content created for all types
- [ ] GO/NO-GO decision approved

### External Dependencies:
- Layout Builder modules (Phase 3) - CRITICAL
- Activity Finder (isolated on Bootstrap 4 - from Phase 1)
- Camp Finder (not yet isolated - will be in Phase 5)

---

## Decision Points

### End of Sprint 14:
- [ ] Is Layout Builder integration working?
- [ ] Are location/branch modules stable?
- [ ] Is Activity Finder isolation still working?
- [ ] Any blockers for program modules?

### End of Sprint 15:
- [ ] Are program modules working well?
- [ ] Is y_lb (landing page) fully functional with LB modules?
- [ ] Ready for events/camps/facilities?

### End of Sprint 16:
- [ ] Are all content types rendering correctly?
- [ ] Any issues with forms?
- [ ] Ready for donation module?

### End of Sprint 17 (End of Phase 4):
- [ ] **GO/NO-GO for Phase 5**
- [ ] Are all content types production-ready?
- [ ] Is Layout Builder integration stable?
- [ ] Is Activity Finder integration maintained?
- [ ] Ready to migrate Vue.js Activity Finder apps?
- [ ] Any critical issues remaining?

---

## Notes

### Important Considerations:

1. **Phase 3 Must Be Stable:** Layout Builder modules are heavily used by content types
2. **y_lb is Most Critical:** Landing page content type uses Layout Builder extensively
3. **Activity Finder Isolation:** Must maintain isolation from Phase 1
4. **Camp Finder Not Yet Isolated:** Will be isolated in Phase 5 (before migration)
5. **Forms Need Consistent Styling:** Establish patterns early
6. **Test Content is Essential:** Need realistic content for proper testing

### Content Type Grouping Rationale:

**Sprint 14 - Location/Branch:**
- Core functionality for YMCA sites
- Branch finder is critical feature
- Tests Activity Finder isolation

**Sprint 15 - Program/Activity:**
- Closely related modules
- y_lb is most critical (Layout Builder integration)
- Tests LB integration extensively

**Sprint 16 - Events/Camps/Facilities:**
- Supporting content types
- Less critical than branches/programs
- Tests form styling patterns

**Sprint 17 - Donation:**
- Special module (payment integration)
- Needs careful testing
- Buffer sprint for integration testing

### Layout Builder Integration:

Content types use Layout Builder in different ways:
- **y_lb:** Primary use case - entire page built with LB
- **y_branch:** May use LB for custom sections
- **y_program:** May use LB for custom sections
- **Others:** May use LB for custom sections or not at all

All content types must be tested with Layout Builder components from Phase 3.

### Activity Finder Integration Points:

- **y_branch:** Branch pages may embed Activity Finder
- **y_program:** Program pages may embed Activity Finder
- **y_camp:** Camp pages will embed Camp Finder (Phase 5)

Must verify isolation still works when Activity Finder is embedded in migrated content type pages.

---

## Next Phase

After Phase 4 is complete:
- **Phase 5:** Activity Finder Vue.js Apps (Sprints 18-21)

See: [PHASE_5_ACTIVITY_FINDER.md](PHASE_5_ACTIVITY_FINDER.md)

---

## Related Documents

- [../EXECUTIVE_SUMMARY.md](../EXECUTIVE_SUMMARY.md)
- [../MODULE_INVENTORY.md](../MODULE_INVENTORY.md)
- [PHASE_1_PREPARATION.md](PHASE_1_PREPARATION.md)
- [PHASE_2_WEBSITE_SERVICES.md](PHASE_2_WEBSITE_SERVICES.md)
- [PHASE_3_LAYOUT_BUILDER.md](PHASE_3_LAYOUT_BUILDER.md)
- [PHASE_5_ACTIVITY_FINDER.md](PHASE_5_ACTIVITY_FINDER.md)
- [../sprints/SPRINT_14_Location_Branch.md](../sprints/SPRINT_14_Location_Branch.md)
- [../sprints/SPRINT_15_Program_Activity.md](../sprints/SPRINT_15_Program_Activity.md)
- [../sprints/SPRINT_16_Events_Camps_Facilities.md](../sprints/SPRINT_16_Events_Camps_Facilities.md)
- [../sprints/SPRINT_17_Donation_Testing.md](../sprints/SPRINT_17_Donation_Testing.md)

---

**Phase Status:** ⬜ Not Started
**Last Updated:** 2025-10-17
