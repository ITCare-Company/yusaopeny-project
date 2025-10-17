# Phase 2: Website Services Modules

**Duration:** 8 weeks (Sprints 4-7)
**Status:** Not Started
**Goal:** Migrate all Website Services modules to Bootstrap 5

---

## Overview

Phase 2 focuses on migrating the Website Services module suite - primarily the ws_small_y collection and related WS modules. These modules provide content display components and should follow the patterns established in Phase 1.

**Key Strategy:** Batch process similar modules for efficiency.

---

## Sprints in This Phase

### Sprint 4: WS Small Y Batch 1
**Modules (6):** High-priority small_y modules
- small_y_hero
- small_y_cards
- small_y_carousels
- small_y_accordions
- small_y_alerts
- small_y_tabs

**See:** [sprints/SPRINT_04_WS_SmallY_Batch1.md](../sprints/SPRINT_04_WS_SmallY_Batch1.md)

### Sprint 5: WS Small Y Batch 2
**Modules (10):** Remaining small_y modules
- small_y_articles through ws_small_y_testimonials

**See:** [sprints/SPRINT_05_WS_SmallY_Batch2.md](../sprints/SPRINT_05_WS_SmallY_Batch2.md)

### Sprint 6: Other WS Modules
**Modules (6):** ws_event, ws_promotion, ws_colorway_canada, ws_lb_tabs, ws_home_branch

**See:** [sprints/SPRINT_06_WS_Other_Modules.md](../sprints/SPRINT_06_WS_Other_Modules.md)

### Sprint 7: Testing & Catchup
**Focus:** Integration testing, bug fixes, documentation

**See:** [sprints/SPRINT_07_Testing_Catchup.md](../sprints/SPRINT_07_Testing_Catchup.md)

---

## Key Deliverables

### Sprint 4 Deliverables
- [ ] 6 high-priority small_y modules migrated
- [ ] Modules build successfully
- [ ] Visual appearance maintained
- [ ] Interactive components work

### Sprint 5 Deliverables
- [ ] All 16 small_y modules complete
- [ ] Batch migration patterns documented
- [ ] Common issues identified and resolved

### Sprint 6 Deliverables
- [ ] All other WS modules migrated
- [ ] ws_promotion modal tested
- [ ] ws_colorway_canada theme variant works

### Sprint 7 Deliverables
- [ ] All WS modules tested together
- [ ] Visual regression tests passed
- [ ] Accessibility tests passed
- [ ] Phase 2 documentation complete

---

## Components in This Phase

### WS Small Y Suite (16 modules)
**Parent:** ws_small_y (`docroot/modules/contrib/ws_small_y`)
**Bootstrap:** 4.4.1 → 5.3.3

**All submodules:**
1. small_y_accordions
2. small_y_alerts
3. small_y_articles
4. small_y_branch
5. small_y_cards
6. small_y_carousels
7. small_y_editor
8. small_y_events
9. small_y_hero
10. small_y_icon_grid
11. small_y_ping_pongs
12. small_y_search
13. small_y_tabs
14. ws_small_y_staff
15. ws_small_y_statistics
16. ws_small_y_testimonials

### Other WS Modules (6 modules)

**ws_event** - Event management
**ws_promotion** + 2 submodules (modal, activity_finder)
**ws_colorway_canada** + lb_hero_canada submodule
**ws_lb_tabs** - Tab components
**ws_home_branch** - Home branch selector

---

## Success Criteria

### Technical
- [ ] All 22 WS modules migrated to Bootstrap 5.3.3
- [ ] All modules build without errors
- [ ] Visual appearance matches Bootstrap 4
- [ ] Interactive components functional
- [ ] No JavaScript console errors

### Quality
- [ ] Visual regression tests passed
- [ ] Accessibility maintained (WCAG 2.2 AA)
- [ ] Responsive at all breakpoints
- [ ] Cross-browser compatibility verified

### Process
- [ ] Migration patterns reusable
- [ ] Documentation updated
- [ ] Issues documented for future reference

---

## Risks & Mitigation

### Risk 1: Batch Processing Issues (MEDIUM)
**Impact:** One broken module could block entire batch
**Mitigation:**
- Test each module individually before integration
- Keep modules independent
- Use contractor for parallel work

### Risk 2: Small Y Suite Interdependencies (LOW)
**Impact:** Modules may depend on each other
**Probability:** LOW
**Mitigation:**
- Review module dependencies first
- Test together after individual migration

---

## Testing Strategy

**Standard Testing (Upgrade from Phase 1):**
- Visual regression (BackstopJS) - Run for each batch
- Accessibility (Pa11y) - Run for each batch
- Manual testing per module
- Integration testing in Sprint 7

---

## Resources

**Team:** 1 Developer + Contractor (recommended)
**Tools:** Node.js, Webpack 5, BackstopJS, Pa11y

---

## Dependencies

**Before Phase 2:**
- [x] Phase 1 complete (theme migrated)
- [x] Testing infrastructure ready

**Before Phase 3:**
- [ ] All WS modules migrated
- [ ] Integration testing passed
- [ ] GO/NO-GO decision

---

## Decision Points

### End of Sprint 5:
- [ ] Are batch migration patterns working?
- [ ] Should we continue with contractor support?

### End of Sprint 7 (End of Phase 2):
- [ ] **GO/NO-GO for Phase 3**
- [ ] Are WS modules stable enough?
- [ ] Ready for Layout Builder modules?

---

## Next Phase

**Phase 3:** Layout Builder Modules (Sprints 8-13)

See: [PHASE_3_LAYOUT_BUILDER.md](PHASE_3_LAYOUT_BUILDER.md)

---

## Related Documents

- [../EXECUTIVE_SUMMARY.md](../EXECUTIVE_SUMMARY.md)
- [../MODULE_INVENTORY.md](../MODULE_INVENTORY.md)
- [PHASE_1_PREPARATION.md](PHASE_1_PREPARATION.md)
- [PHASE_3_LAYOUT_BUILDER.md](PHASE_3_LAYOUT_BUILDER.md)

---

**Phase Status:** ⬜ Not Started
**Last Updated:** 2025-10-17
