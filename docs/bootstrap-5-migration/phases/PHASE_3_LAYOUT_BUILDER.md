# Phase 3: Layout Builder Modules

**Duration:** 12 weeks (Sprints 8-13)
**Status:** Not Started
**Goal:** Migrate all Layout Builder modules to Bootstrap 5

---

## Overview

Phase 3 focuses on migrating the Layout Builder module suite - the most complex and interactive components in the distribution. These modules provide page-building capabilities with advanced JavaScript functionality including modals, carousels, date pickers, and dynamic forms.

**Key Challenge:** Many LB modules use interactive Bootstrap JavaScript components that have API changes in Bootstrap 5.

**Key Strategy:** Group by complexity and JavaScript dependencies, tackle high-risk components early.

---

## Sprints in This Phase

### Sprint 8: LB Simple Components Batch 1
**Modules (6):** Low-risk, template-focused modules
- lb_banner
- lb_breaker
- lb_cards
- lb_header_footer
- lb_stat
- lb_text

**See:** [sprints/SPRINT_08_LB_Simple_Batch1.md](../sprints/SPRINT_08_LB_Simple_Batch1.md)

### Sprint 9: LB Simple Components Batch 2
**Modules (4):** Remaining simple modules
- lb_grid_content
- lb_icon_grid
- lb_ping_pong
- lb_table

**See:** [sprints/SPRINT_09_LB_Simple_Batch2.md](../sprints/SPRINT_09_LB_Simple_Batch2.md)

### Sprint 10: LB Interactive Components Batch 1
**Modules (4):** Medium-risk interactive modules
- lb_accordion (reference - already done)
- lb_carousel
- lb_tabs
- lb_gallery_cards

**See:** [sprints/SPRINT_10_LB_Interactive_Batch1.md](../sprints/SPRINT_10_LB_Interactive_Batch1.md)

### Sprint 11: LB Interactive Components Batch 2
**Modules (3):** High-risk interactive modules
- lb_modal
- lb_search
- lb_promo_card

**See:** [sprints/SPRINT_11_LB_Interactive_Batch2.md](../sprints/SPRINT_11_LB_Interactive_Batch2.md)

### Sprint 12: LB Form Components
**Modules (2):** Form-related modules with JavaScript
- lb_webform
- lb_group_schedules

**See:** [sprints/SPRINT_12_LB_Form_Components.md](../sprints/SPRINT_12_LB_Form_Components.md)

### Sprint 13: LB Testing & Date Picker Replacement
**Focus:**
- Integration testing all LB modules
- Replace tempusdominus date picker
- Bug fixes and documentation
- Phase 3 completion

**See:** [sprints/SPRINT_13_LB_Testing_DatePicker.md](../sprints/SPRINT_13_LB_Testing_DatePicker.md)

---

## Key Deliverables

### Sprint 8 Deliverables
- [ ] 6 simple LB modules migrated
- [ ] Templates updated to Bootstrap 5
- [ ] Visual appearance maintained
- [ ] Responsive at all breakpoints

### Sprint 9 Deliverables
- [ ] All 10 simple LB modules complete
- [ ] Grid and table layouts working
- [ ] Pattern library for simple modules

### Sprint 10 Deliverables
- [ ] 4 interactive modules migrated
- [ ] Carousel API updated to Bootstrap 5
- [ ] Tabs API updated to Bootstrap 5
- [ ] JavaScript components tested

### Sprint 11 Deliverables
- [ ] Modal API updated to Bootstrap 5
- [ ] Search functionality maintained
- [ ] All interactive components functional
- [ ] Cross-component testing complete

### Sprint 12 Deliverables
- [ ] Webform module migrated
- [ ] Group schedules module migrated
- [ ] Form styling consistent
- [ ] Date picker replacement tested

### Sprint 13 Deliverables
- [ ] Date picker replaced (tempusdominus removed)
- [ ] All 19 LB modules tested together
- [ ] Visual regression tests passed
- [ ] Accessibility tests passed
- [ ] Phase 3 documentation complete
- [ ] GO/NO-GO decision for Phase 4

---

## Components in This Phase

### Layout Builder Modules (19 modules)

**Simple Components (10 modules) - Sprints 8-9:**
1. **lb_banner** - Banner component
2. **lb_breaker** - Visual section breaks
3. **lb_cards** - Card displays
4. **lb_grid_content** - Grid layouts
5. **lb_header_footer** - Header/footer components
6. **lb_icon_grid** - Icon grids
7. **lb_ping_pong** - Alternating content blocks
8. **lb_stat** - Statistics display
9. **lb_table** - Table components
10. **lb_text** - Text blocks

**Interactive Components (7 modules) - Sprints 10-11:**
11. **lb_accordion** - Accordion (REFERENCE - already migrated)
12. **lb_carousel** - Image/content carousels (Bootstrap JS API changes)
13. **lb_gallery_cards** - Gallery with lightbox
14. **lb_modal** - Modal dialogs (Bootstrap JS API changes)
15. **lb_promo_card** - Promotional cards with interactions
16. **lb_search** - Search components
17. **lb_tabs** - Tab navigation (Bootstrap JS API changes)

**Form Components (2 modules) - Sprint 12:**
18. **lb_group_schedules** - Schedule forms with date picker
19. **lb_webform** - Webform integration

---

## Success Criteria

### Technical
- [ ] All 19 LB modules migrated to Bootstrap 5.3.3
- [ ] All modules build without errors
- [ ] All JavaScript components functional
- [ ] Modal API updated (Bootstrap 5 syntax)
- [ ] Carousel API updated (Bootstrap 5 syntax)
- [ ] Tabs API updated (Bootstrap 5 syntax)
- [ ] Date picker replaced (tempusdominus removed)
- [ ] No JavaScript console errors
- [ ] No jQuery dependencies added

### Quality
- [ ] Visual regression tests passed (all modules)
- [ ] Accessibility maintained (WCAG 2.2 AA)
- [ ] Interactive components keyboard-accessible
- [ ] Focus states maintained
- [ ] Responsive at all breakpoints (sm, md, lg, xl, xxl)
- [ ] Cross-browser compatibility verified (Chrome, Firefox, Safari, Edge)

### Performance
- [ ] JavaScript bundle size not increased significantly
- [ ] No memory leaks in interactive components
- [ ] Smooth animations maintained

### Process
- [ ] Interactive component migration patterns documented
- [ ] JavaScript API changes documented
- [ ] Testing matrix complete
- [ ] Known issues documented

---

## Risks & Mitigation

### Risk 1: Bootstrap JavaScript API Changes Breaking Components (HIGH)
**Impact:** CRITICAL - Interactive components may not work
**Probability:** HIGH
**Affected Modules:** lb_modal, lb_carousel, lb_tabs, lb_accordion
**Mitigation:**
- Study Bootstrap 5 migration guide for JavaScript changes
- Test each interactive component thoroughly
- Use lb_accordion as reference (already migrated)
- Create test pages for all interactive components
- Document API changes for each component type
- Allocate extra time for JavaScript debugging

**Key API Changes:**
- Data attributes: `data-toggle` → `data-bs-toggle`
- JavaScript methods: `.modal('show')` → `bootstrap.Modal.getInstance().show()`
- Events: `show.bs.modal` naming stays same but event object changes
- jQuery removed from Bootstrap 5 (but still in Drupal core)

### Risk 2: Date Picker Replacement Fails (MEDIUM)
**Impact:** HIGH - Schedule forms break
**Probability:** MEDIUM
**Affected Modules:** lb_group_schedules
**Mitigation:**
- Date picker replacement decided in Phase 1 Sprint 1
- Test date picker early in Sprint 12
- Have fallback option ready (Flatpickr most likely)
- Test date picker with all form contexts
- Test accessibility of date picker
- Test touch/mobile interactions

**Replacement Options (from Phase 1 decision):**
- Flatpickr (recommended - lightweight, accessible)
- Tempus Dominus 6 (Bootstrap 5 version)
- Native HTML5 date input (fallback)

### Risk 3: Modal Conflicts with Drupal (MEDIUM)
**Impact:** MEDIUM - Modal may not work with Drupal dialogs
**Probability:** MEDIUM
**Affected Modules:** lb_modal, ws_promotion (from Phase 2)
**Mitigation:**
- Test modal with Drupal's dialog system
- Check for event listener conflicts
- Test modal with AJAX forms
- Verify z-index stacking works
- Test nested modals (if used)

### Risk 4: Carousel Performance Issues (LOW)
**Impact:** LOW - Carousels may be slower
**Probability:** LOW
**Affected Modules:** lb_carousel, small_y_carousels (from Phase 2)
**Mitigation:**
- Test carousel with many slides
- Profile JavaScript performance
- Test on mobile devices
- Consider lazy loading for carousel images
- Test touch/swipe gestures

### Risk 5: Testing Complexity Increases (MEDIUM)
**Impact:** MEDIUM - Testing takes longer than expected
**Probability:** MEDIUM
**Mitigation:**
- Create reusable test scenarios for interactive components
- Automate what can be automated (BackstopJS)
- Focus manual testing on interactions
- Use Sprint 13 as buffer for testing overflow
- Document test cases for reuse

---

## Testing Strategy

### Standard Testing (Sprints 8-9)
**For Simple Components:**
- Visual regression testing (BackstopJS)
- Accessibility testing (Pa11y)
- Responsive testing (all breakpoints)
- Manual cross-browser testing

### Enhanced Testing (Sprints 10-12)
**For Interactive Components - ADD:**
- JavaScript functionality testing (manual + automated)
- Keyboard navigation testing
- Touch/gesture testing (mobile)
- Event listener testing
- Memory leak testing (Chrome DevTools)
- State management testing (open/close, show/hide)

### Integration Testing (Sprint 13)
**All LB Modules Together:**
- Multiple components on same page
- Nested components testing
- Modal + carousel + tabs on same page
- Form submissions with date picker
- AJAX interactions
- Drupal dialog interactions

### Test Matrix for Interactive Components

**lb_modal:**
- [ ] Open/close via JavaScript
- [ ] Open/close via data attributes
- [ ] Keyboard ESC closes modal
- [ ] Click backdrop closes modal
- [ ] Focus trap works
- [ ] Multiple modals on page
- [ ] Modal with form
- [ ] Modal with AJAX

**lb_carousel:**
- [ ] Auto-play works
- [ ] Manual navigation (arrows)
- [ ] Manual navigation (indicators)
- [ ] Touch/swipe gestures
- [ ] Keyboard navigation
- [ ] Pause on hover
- [ ] Multiple carousels on page
- [ ] Responsive images

**lb_tabs:**
- [ ] Tab switching via click
- [ ] Tab switching via keyboard
- [ ] Deep linking to tab
- [ ] Multiple tab sets on page
- [ ] Nested tabs (if used)
- [ ] Tab content lazy loading

**lb_webform + Date Picker:**
- [ ] Date picker opens
- [ ] Date selection works
- [ ] Keyboard date entry
- [ ] Date validation
- [ ] Min/max date constraints
- [ ] Mobile date picker
- [ ] Form submission

---

## Resources

### Team
- 1 Full-time Frontend Developer
- Optional: Frontend Contractor (recommended for parallel work)
- Part-time QA for testing support (Sprint 13)

### Tools
- Node.js 16+
- Webpack 5
- Bootstrap 5.3.3 documentation (JavaScript section)
- BackstopJS (visual regression)
- Pa11y (accessibility)
- Chrome DevTools (performance profiling)
- BrowserStack or similar (cross-browser testing)

### Reference Materials
- Bootstrap 5 JavaScript API documentation
- Bootstrap 4 to 5 migration guide (JavaScript section)
- lb_accordion module (reference implementation)
- Date picker library documentation (from Phase 1 decision)

### Time
- Sprint 8: 2 weeks (6 simple modules)
- Sprint 9: 2 weeks (4 simple modules)
- Sprint 10: 2 weeks (4 interactive modules)
- Sprint 11: 2 weeks (3 high-risk interactive modules)
- Sprint 12: 2 weeks (2 form modules)
- Sprint 13: 2 weeks (testing + date picker)
- **Total: 12 weeks**

---

## Dependencies

### Before Phase 3 Can Start:
- [x] Phase 1 complete (theme migrated)
- [x] Phase 2 complete (WS modules migrated)
- [x] Testing infrastructure working
- [x] Date picker replacement chosen (from Phase 1 Sprint 1)
- [ ] GO/NO-GO decision from Phase 2

### Before Phase 4 Can Start:
- [ ] All 19 LB modules migrated
- [ ] Interactive components fully functional
- [ ] Date picker replaced and tested
- [ ] Integration testing passed
- [ ] Visual regression tests passed
- [ ] Accessibility tests passed
- [ ] GO/NO-GO decision approved

### External Dependencies:
- Bootstrap 5.3.3 JavaScript library
- Date picker library (chosen in Phase 1)
- Drupal core's jQuery (still present in D11)

---

## Decision Points

### End of Sprint 9:
- [ ] Are simple components working well?
- [ ] Is batch migration pattern still efficient?
- [ ] Should we continue with same approach?

### End of Sprint 11:
- [ ] Are interactive components stable?
- [ ] Modal API fully migrated?
- [ ] Carousel/Tabs working correctly?
- [ ] Any blockers for form components?

### End of Sprint 12:
- [ ] Is date picker replacement working?
- [ ] Are form components functional?
- [ ] Ready for integration testing?

### End of Sprint 13 (End of Phase 3):
- [ ] **GO/NO-GO for Phase 4**
- [ ] Are all LB modules production-ready?
- [ ] Is testing coverage sufficient?
- [ ] Ready to migrate content type modules?
- [ ] Any critical issues remaining?

---

## Notes

### Important Considerations:

1. **lb_accordion is the Template:** Use it as reference for all interactive components
2. **JavaScript API Changes are Critical:** Bootstrap 5 changed many JavaScript methods and data attributes
3. **Date Picker is Special:** Only module requiring external library replacement
4. **Testing is Extensive:** Interactive components need more testing than simple modules
5. **Sprint 13 is Buffer:** Use for testing overflow and critical bug fixes

### Bootstrap 5 JavaScript API Changes Summary:

**Data Attributes:**
- All `data-*` attributes now prefixed with `data-bs-*`
- Example: `data-toggle="modal"` → `data-bs-toggle="modal"`

**JavaScript Initialization:**
```javascript
// Bootstrap 4
$('#myModal').modal('show');

// Bootstrap 5
var myModal = new bootstrap.Modal(document.getElementById('myModal'));
myModal.show();
// OR
var myModal = bootstrap.Modal.getInstance(document.getElementById('myModal'));
myModal.show();
```

**Events:**
- Event names unchanged but event object structure changed
- Still use: `show.bs.modal`, `hide.bs.modal`, etc.

**jQuery:**
- No longer required by Bootstrap 5
- Still available in Drupal core (11.x still ships jQuery)
- Prefer vanilla JavaScript for new code

### Module Grouping Rationale:

**Simple Modules (Sprints 8-9):**
- Primarily template changes
- Minimal or no JavaScript
- Low risk, high throughput

**Interactive Modules (Sprints 10-11):**
- Significant JavaScript changes
- Bootstrap API updates required
- Medium to high risk

**Form Modules (Sprint 12):**
- Combines templates + JavaScript
- Date picker replacement
- Medium risk but special focus needed

---

## Next Phase

After Phase 3 is complete:
- **Phase 4:** Content Type Modules (Sprints 14-17)

See: [PHASE_4_CONTENT_TYPES.md](PHASE_4_CONTENT_TYPES.md)

---

## Related Documents

- [../EXECUTIVE_SUMMARY.md](../EXECUTIVE_SUMMARY.md)
- [../MODULE_INVENTORY.md](../MODULE_INVENTORY.md)
- [PHASE_1_PREPARATION.md](PHASE_1_PREPARATION.md)
- [PHASE_2_WEBSITE_SERVICES.md](PHASE_2_WEBSITE_SERVICES.md)
- [PHASE_4_CONTENT_TYPES.md](PHASE_4_CONTENT_TYPES.md)
- [../sprints/SPRINT_08_LB_Simple_Batch1.md](../sprints/SPRINT_08_LB_Simple_Batch1.md)
- [../sprints/SPRINT_09_LB_Simple_Batch2.md](../sprints/SPRINT_09_LB_Simple_Batch2.md)
- [../sprints/SPRINT_10_LB_Interactive_Batch1.md](../sprints/SPRINT_10_LB_Interactive_Batch1.md)
- [../sprints/SPRINT_11_LB_Interactive_Batch2.md](../sprints/SPRINT_11_LB_Interactive_Batch2.md)
- [../sprints/SPRINT_12_LB_Form_Components.md](../sprints/SPRINT_12_LB_Form_Components.md)
- [../sprints/SPRINT_13_LB_Testing_DatePicker.md](../sprints/SPRINT_13_LB_Testing_DatePicker.md)

---

**Phase Status:** ⬜ Not Started
**Last Updated:** 2025-10-17
