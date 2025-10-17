# Phase 1: Preparation & Foundation

**Duration:** 6 weeks (Sprints 1-3)
**Status:** Not Started
**Goal:** Set up infrastructure, migrate core theme, isolate Activity Finder

---

## Overview

Phase 1 establishes the foundation for the entire Bootstrap 5 migration. This phase is critical as it:
1. Sets up testing infrastructure
2. Studies reference implementation (lb_accordion)
3. Migrates the core theme (openy_carnation) which affects the entire site
4. Isolates Activity Finder to prevent breaking while theme migrates

**Critical Path:** Theme migration must succeed before moving to Phase 2.

---

## Sprints in This Phase

### Sprint 1: Infrastructure & Research
- Set up migration infrastructure
- Study lb_accordion reference
- Configure testing tools
- Make date picker decision
- Create module inventory

**See:** [sprints/SPRINT_01_Infrastructure.md](../sprints/SPRINT_01_Infrastructure.md)

### Sprint 2: Core Theme Migration - Part 1
- Update theme dependencies to Bootstrap 5.3.3
- Update core SCSS files
- Update build system to Webpack 5
- Initial build and testing

**See:** [sprints/SPRINT_02_Theme_Part1.md](../sprints/SPRINT_02_Theme_Part1.md)

### Sprint 3: Core Theme Migration - Part 2 + Activity Finder Isolation
- Complete theme SCSS/template updates
- Update theme JavaScript
- Isolate Activity Finder with scoped Bootstrap 4 CSS
- Test theme + Activity Finder coexistence

**See:** [sprints/SPRINT_03_Theme_Part2_AF_Isolation.md](../sprints/SPRINT_03_Theme_Part2_AF_Isolation.md)

---

## Key Deliverables

### Sprint 1 Deliverables
- [ ] Migration branch created (`feature/bootstrap-5-migration`)
- [ ] lb_accordion patterns documented
- [ ] BackstopJS installed and configured
- [ ] Pa11y installed and configured
- [ ] Date picker replacement chosen
- [ ] Module inventory complete (66+ modules)

### Sprint 2 Deliverables
- [ ] openy_carnation dependencies updated to Bootstrap 5.3.3
- [ ] Core SCSS files migrated
- [ ] Webpack 5 build system working
- [ ] Theme builds successfully
- [ ] Homepage renders without major breaks

### Sprint 3 Deliverables
- [ ] All theme SCSS/templates updated to Bootstrap 5
- [ ] Interactive components functional (modals, dropdowns)
- [ ] Activity Finder isolated with scoped Bootstrap 4 CSS
- [ ] Theme + Activity Finder work together
- [ ] Phase 1 testing complete

---

## Components in This Phase

### 1. Theme (CRITICAL)
**openy_carnation**
- Path: `docroot/themes/contrib/openy_carnation`
- Current: Bootstrap 4.4.1 + popper.js 1.16.0
- Target: Bootstrap 5.3.3 + @popperjs/core 2.11.8
- Impact: Affects entire site
- Priority: Must succeed

---

## Success Criteria

### Technical
- [ ] Theme uses Bootstrap 5.3.3
- [ ] Theme builds without errors
- [ ] All interactive components work (modals, dropdowns, tooltips, etc.)
- [ ] Responsive at all breakpoints (sm, md, lg, xl, xxl)
- [ ] No JavaScript console errors
- [ ] Activity Finder still works (isolated on Bootstrap 4)

### Quality
- [ ] Visual appearance matches Bootstrap 4 version
- [ ] No visual regressions on key pages
- [ ] Accessibility maintained (WCAG 2.2 AA)
- [ ] Performance maintained or improved

### Process
- [ ] Testing infrastructure working
- [ ] Documentation up to date
- [ ] Migration patterns documented for Phase 2

---

## Risks & Mitigation

### Risk 1: Theme Migration Breaks Site (HIGH)
**Impact:** CRITICAL - Entire site affected
**Probability:** MEDIUM
**Mitigation:**
- Start with openy_carnation only (isolated testing)
- Use BackstopJS for visual regression testing
- Test incrementally (core SCSS first, then components)
- Keep Bootstrap 4 branch available for rollback

### Risk 2: Activity Finder Conflicts with Bootstrap 5 Theme (HIGH)
**Impact:** HIGH - Activity Finder breaks
**Probability:** HIGH without mitigation
**Mitigation:**
- Isolate Activity Finder early (Sprint 3)
- Scope Bootstrap 4 CSS to `.activity-finder-wrapper`
- Test both Bootstrap versions on same page
- Document isolation approach for other teams

### Risk 3: Testing Infrastructure Not Ready (MEDIUM)
**Impact:** MEDIUM - Can't validate changes
**Probability:** LOW
**Mitigation:**
- Set up testing in Sprint 1 (before migration work)
- Start with basic manual testing, add automation progressively
- Use lb_accordion as test case for tools

### Risk 4: Date Picker Replacement Fails (LOW)
**Impact:** MEDIUM - Affects scheduling features
**Probability:** LOW
**Mitigation:**
- Test multiple options (Flatpickr, Tempus Dominus, native)
- Choose in Sprint 1, implement in Sprint 13
- Have fallback option ready

---

## Testing Strategy

### Sprint 1: Basic Manual
- Visual inspection only
- Test infrastructure setup

### Sprint 2: Basic Manual
- Homepage visual inspection
- Basic interactive component testing

### Sprint 3: Standard (Upgrade from Basic)
- Visual regression testing (BackstopJS) - baseline creation
- Accessibility testing (Pa11y) - baseline run
- Manual testing matrix started
- All content types tested
- Navigation tested (desktop & mobile)
- Activity Finder tested (isolation)

---

## Dependencies

### Before Phase 1 Can Start:
- [ ] Project approval
- [ ] Resources assigned (1 developer)
- [ ] Development environment ready (Docksal)
- [ ] Access to codebase repository

### Before Phase 2 Can Start:
- [ ] Phase 1 complete (theme migrated)
- [ ] Testing infrastructure working
- [ ] Activity Finder isolated
- [ ] GO/NO-GO decision approved

---

## Resources

### Team
- 1 Full-time Frontend Developer
- Optional: Part-time QA for testing setup

### Tools
- Node.js 16+
- Docksal or DDEV
- BackstopJS (visual regression)
- Pa11y (accessibility)
- Git

### Time
- Sprint 1: 2 weeks
- Sprint 2: 2 weeks
- Sprint 3: 2 weeks
- **Total: 6 weeks**

---

## Decision Points

### End of Sprint 1:
- [ ] **Date Picker Decision:** Which replacement to use?
- [ ] **Module Inventory:** Any modules can be skipped?

### End of Sprint 2:
- [ ] **Theme Feasibility:** Can theme be migrated successfully?
- [ ] **Continue/Stop:** Is this migration viable?

### End of Sprint 3 (End of Phase 1):
- [ ] **GO/NO-GO for Phase 2:** Is theme stable enough?
- [ ] **Activity Finder Isolation:** Does isolation strategy work?
- [ ] **Testing Infrastructure:** Is testing ready for Phase 2?

---

## Notes

### Important Considerations:
1. **Theme is Priority #1:** Everything else depends on theme success
2. **Activity Finder Isolation:** Critical to prevent breaking while theme migrates
3. **Testing Setup:** Invest time early to save time later
4. **Documentation:** Document patterns for reuse in Phase 2

### Reference Implementation:
- Study `lb_accordion` module extensively
- It's already migrated to Bootstrap 5.3.3
- Use it as template for all future migrations

---

## Next Phase

After Phase 1 is complete:
- **Phase 2:** Website Services Modules (Sprints 4-7)

See: [PHASE_2_WEBSITE_SERVICES.md](PHASE_2_WEBSITE_SERVICES.md)

---

## Related Documents

- [../EXECUTIVE_SUMMARY.md](../EXECUTIVE_SUMMARY.md)
- [../MODULE_INVENTORY.md](../MODULE_INVENTORY.md)
- [../QUICK_START.md](../QUICK_START.md)
- [../sprints/SPRINT_01_Infrastructure.md](../sprints/SPRINT_01_Infrastructure.md)
- [../sprints/SPRINT_02_Theme_Part1.md](../sprints/SPRINT_02_Theme_Part1.md)
- [../sprints/SPRINT_03_Theme_Part2_AF_Isolation.md](../sprints/SPRINT_03_Theme_Part2_AF_Isolation.md)

---

**Phase Status:** ⬜ Not Started
**Last Updated:** 2025-10-17
