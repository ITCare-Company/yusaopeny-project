# Decision: Activity Finder Migration Strategy

**Status:** Proposed
**Date:** 2025-10-17
**Decision Makers:** Development Team, Product Owner
**Affected Components:** Activity Finder Vue.js application, BootstrapVue components

---

## Problem Statement

The Activity Finder component is built with Vue.js 2 and BootstrapVue 2, which is fundamentally incompatible with Bootstrap 5. BootstrapVue 2 relies on Bootstrap 4's jQuery-based architecture and class structure, while Bootstrap 5 has removed jQuery dependency and restructured many components and utilities.

### Current Technical Debt

- **BootstrapVue 2:** Locked to Bootstrap 4.x, no official Bootstrap 5 support planned
- **Vue 2:** Approaching end-of-life (EOL December 31, 2023)
- **jQuery Dependency:** BootstrapVue 2 implicitly requires jQuery through Bootstrap 4
- **Component Count:** 85+ BootstrapVue components used across Activity Finder
- **Custom Overrides:** Extensive SCSS customizations tied to BS4 structure

### Business Impact

- **Security Risk:** Using EOL frameworks exposes sites to unpatched vulnerabilities
- **Browser Compatibility:** Modern browsers may break jQuery-dependent features
- **Performance:** jQuery and BootstrapVue add significant bundle size
- **Developer Experience:** Difficulty hiring developers for outdated stack
- **Feature Velocity:** New features blocked by framework limitations

---

## Options Analysis

### Option 1: Migrate to BootstrapVueNext

**Description:** Adopt BootstrapVueNext (community-maintained Bootstrap 5 port for Vue 3)

**Pros:**
- Maintains similar component API to BootstrapVue 2
- Reduces migration learning curve for developers familiar with BootstrapVue
- Community-driven project with active development
- Direct Bootstrap 5 class support

**Cons:**
- **Not production-ready:** Alpha/beta status as of October 2024
- **Incomplete component parity:** Missing 30%+ of BootstrapVue 2 components
- **Community maintenance risk:** No corporate backing, potential abandonment
- **Vue 3 migration required:** Must migrate Vue 2 → Vue 3 simultaneously
- **Limited documentation:** Sparse examples and migration guides
- **Breaking changes inevitable:** API still in flux

**Risk Level:** HIGH
**Long-term Viability:** UNCERTAIN

---

### Option 2: Direct Bootstrap 5 Migration (No Framework)

**Description:** Remove BootstrapVue entirely, use vanilla Bootstrap 5 with custom Vue components

**Pros:**
- **Full control:** No dependency on third-party component libraries
- **Performance:** Smaller bundle size without abstraction layer
- **Modern standards:** Leverage Bootstrap 5's native JavaScript API
- **Flexibility:** Build exactly what's needed, no unnecessary components
- **Long-term stability:** Direct dependency on Bootstrap (industry standard)

**Cons:**
- **Higher initial effort:** Must build/adapt all components manually
- **Custom components required:** Need to create Vue wrappers for BS5 JS components
- **Testing burden:** More extensive testing of custom implementations
- **Vue 3 migration required:** Still must migrate Vue 2 → Vue 3

**Risk Level:** MEDIUM
**Long-term Viability:** EXCELLENT

---

### Option 3: Keep Bootstrap 4 (Isolation Strategy)

**Description:** Maintain Activity Finder on Bootstrap 4 in isolated scope, migrate rest of site to BS5

**Pros:**
- **Zero immediate effort:** No Activity Finder changes required
- **Risk avoidance:** Defers complex migration
- **Buys time:** Can plan thorough migration later
- **Proven stability:** Current implementation works

**Cons:**
- **CSS conflicts:** Requires namespace isolation (`.bs4-scope`, `.bs5-scope`)
- **Dual maintenance:** Must maintain two Bootstrap versions indefinitely
- **Performance penalty:** Loading both Bootstrap 4 and 5 CSS (~400KB combined)
- **Technical debt compounds:** Problem gets harder over time
- **Developer confusion:** Context switching between BS4 and BS5 patterns
- **Limited lifespan:** Bootstrap 4 security support ends eventually

**Estimated Effort:** 2-3 weeks (isolation implementation)
**Risk Level:** MEDIUM
**Long-term Viability:** POOR (temporary solution only)

---

### Option 4: Hybrid Isolation + Gradual Migration

**Description:** Isolate Activity Finder on BS4 initially, then migrate to Direct BS5 over 2-3 phases

**Pros:**
- **Staged risk:** Allows main site to move to BS5 immediately
- **Time to plan:** Can thoroughly architect Activity Finder migration
- **Continuous delivery:** Site improvements not blocked by Activity Finder
- **Flexibility:** Can incorporate lessons learned from rest of site
- **Team capacity:** Spreads complex work across multiple sprints

**Cons:**
- **Extended timeline:** Full migration takes 4-6 months total
- **Temporary complexity:** Dual Bootstrap period still exists
- **Coordination overhead:** Must manage isolation boundaries carefully

**Estimated Effort:** 3 weeks (isolation) + 12-16 weeks (migration)
**Risk Level:** LOW
**Long-term Viability:** EXCELLENT

---

## Detailed Comparison Matrix

| Criteria | BootstrapVueNext | Direct BS5 | Keep BS4 | Hybrid Approach |
|----------|------------------|------------|----------|----------------|
| **Production Readiness** | Poor | Good | Excellent | Excellent |
| **Development Effort** | Medium | High | Low | Medium-High |
| **Performance Impact** | Medium | Excellent | Poor | Good |
| **Maintenance Burden** | High | Low | High | Medium |
| **Security Posture** | Medium | Excellent | Poor | Good |
| **Framework Risk** | High | Low | Medium | Low |
| **Team Familiarity** | Medium | Low | High | Medium |
| **Code Reusability** | Medium | High | High | High |
| **Testing Complexity** | Medium | High | Low | Medium |
| **Long-term Cost** | Medium | Low | High | Low |

---

## Recommendation: Option 4 (Hybrid Isolation + Gradual Migration)

### Rationale

1. **Unblocks Site-Wide Migration:** The rest of the site (90%+ of codebase) can migrate to Bootstrap 5 immediately without waiting for Activity Finder resolution.

2. **Reduces Risk:** Staged approach prevents "big bang" migration failures. Each phase can be tested and validated independently.

3. **Optimal End State:** Direct Bootstrap 5 implementation provides best performance, maintainability, and long-term viability.

4. **Resource Management:** Spreads complex Activity Finder work across multiple sprints, preventing team burnout.

5. **Learning Opportunity:** Team gains BS5 experience on simpler components before tackling Activity Finder.

6. **Flexibility:** If BootstrapVueNext matures significantly during Phase 1, we can pivot strategy.

---

## Implementation Plan

### Phase 1: Isolation

**Objective:** Enable Activity Finder to coexist with Bootstrap 5 on the same pages

**Technical Approach:**

1. **CSS Namespacing:**
   ```scss
   // Wrap all Bootstrap 4 styles
   .activity-finder-bs4-scope {
     @import 'bootstrap-4/bootstrap';
     @import 'bootstrap-vue-2/bootstrap-vue';
   }
   ```

2. **Component Scoping:**
   ```vue
   <template>
     <div class="activity-finder-bs4-scope">
       <!-- All BootstrapVue components here -->
       <b-card>...</b-card>
     </div>
   </template>
   ```

3. **Build Configuration:**
   - Separate Webpack entry for Activity Finder with BS4 dependencies
   - Code splitting to prevent BS4/BS5 conflict in shared bundles

4. **Testing:**
   - Visual regression tests for Activity Finder
   - Cross-component integration tests
   - Browser compatibility verification (Chrome, Firefox, Safari, Edge)

**Deliverables:**
- Isolated Activity Finder CSS bundle (~180KB)
- Updated build configuration
- Documentation on isolation boundaries
- Test suite for isolated component

**Success Criteria:**
- Activity Finder renders correctly on BS5 pages
- No visual regressions
- No JavaScript console errors
- Performance budget maintained (<3s Time to Interactive)

---

### Phase 2: Vue 3 Migration

**Objective:** Upgrade Activity Finder to Vue 3 while maintaining Bootstrap 4

**Technical Approach:**

1. **Dependencies Update:**
   ```json
   {
     "vue": "^3.4.0",
     "@vue/compat": "^3.4.0",
     "vue-router": "^4.0.0",
     "pinia": "^2.1.0"
   }
   ```

2. **Compatibility Build:**
   - Use Vue 3 compatibility mode initially
   - Identify and fix breaking changes incrementally
   - Replace deprecated APIs ($on, $off, $once)

3. **State Management Migration:**
   - Migrate Vuex → Pinia
   - Update all store modules
   - Refactor component imports

4. **Router Migration:**
   - Update to Vue Router 4
   - Fix route guard syntax changes
   - Update navigation patterns

5. **Component Refactoring:**
   - Replace `$listeners` with `v-bind="$attrs"`
   - Update `v-model` to use multiple v-models syntax
   - Fix functional component signatures
   - Update custom directive hooks

6. **Testing:**
   - Update Jest configuration for Vue 3
   - Migrate component tests to `@vue/test-utils` v2
   - Add Composition API tests

**Deliverables:**
- Vue 3 compatible Activity Finder (still on Bootstrap 4)
- Migrated test suite
- Updated developer documentation
- Performance benchmarks

**Success Criteria:**
- All existing features work identically
- Test coverage maintained at 80%+
- No performance regression
- Bundle size reduced by 15%+ (due to Vue 3 improvements)

---

### Phase 3: Bootstrap 5 Migration

**Objective:** Migrate Activity Finder to Bootstrap 5 with custom Vue components

**Technical Approach:**

1. **Component Inventory & Mapping:**
   ```
   BootstrapVue Component → Bootstrap 5 Equivalent
   ----------------------------------------
   b-card → Custom <Card> component using .card classes
   b-modal → Custom <Modal> component using BS5 Modal JS
   b-form-input → Native <input> with .form-control
   b-button → Native <button> with .btn classes
   b-dropdown → Custom <Dropdown> using BS5 Dropdown JS
   b-pagination → Custom <Pagination> component
   b-table → Custom <Table> component with sorting/filtering
   b-spinner → Simple .spinner-border div
   b-alert → Simple .alert div with reactivity
   ... (full mapping in separate document)
   ```

2. **Custom Component Library:**
   Create `@yusa/vue-bootstrap5-components` package:
   - Wrapper components for BS5 JavaScript components
   - Composables for common patterns (modals, tooltips, popovers)
   - TypeScript definitions
   - Unit tests for each component
   - Storybook documentation

3. **Progressive Migration Strategy:**
   - **Week 11-12:** Build component library foundation
   - **Week 13-14:** Migrate simple components (cards, alerts, badges)
   - **Week 15-16:** Migrate complex components (modals, dropdowns, tables)
   - **Week 17-18:** Migrate forms and validation
   - **Week 19:** Final integration, polish, and testing

4. **Class Name Migration:**
   ```javascript
   // Automated migration where possible
   const classMapping = {
     'ml-': 'ms-',  // margin-left → margin-start
     'mr-': 'me-',  // margin-right → margin-end
     'pl-': 'ps-',  // padding-left → padding-start
     'pr-': 'pe-',  // padding-right → padding-end
     'form-group': 'mb-3',
     'custom-control': 'form-check',
     'custom-select': 'form-select',
     // ... (full mapping in migration script)
   };
   ```

5. **SCSS Migration:**
   - Replace Bootstrap 4 variables with Bootstrap 5 equivalents
   - Update custom theme to use BS5 variable names
   - Migrate mixins and utilities
   - Remove jQuery dependencies from custom scripts

6. **JavaScript Component Integration:**
   ```javascript
   // Example: Modal wrapper component
   import { Modal } from 'bootstrap';
   import { onMounted, onUnmounted, ref } from 'vue';

   export function useModal(elementRef) {
     const modalInstance = ref(null);

     onMounted(() => {
       modalInstance.value = new Modal(elementRef.value);
     });

     onUnmounted(() => {
       modalInstance.value?.dispose();
     });

     return {
       show: () => modalInstance.value?.show(),
       hide: () => modalInstance.value?.hide(),
     };
   }
   ```

7. **Testing Strategy:**
   - Visual regression tests for every component
   - Interaction tests for dropdowns, modals, tooltips
   - Form validation testing
   - Accessibility testing (WCAG 2.1 AA compliance)
   - Cross-browser testing
   - Mobile responsive testing

**Deliverables:**
- Fully migrated Activity Finder on Bootstrap 5
- Custom Vue 3 + Bootstrap 5 component library
- Comprehensive test suite
- Developer documentation
- Migration guide for future similar projects

**Success Criteria:**
- 100% feature parity with current Activity Finder
- No visual regressions
- Accessibility score maintained or improved
- Performance improvement of 20%+ (smaller bundle, faster rendering)
- Test coverage at 85%+
- Documentation complete

---

### Phase 4: Cleanup & Optimization

**Objective:** Remove Bootstrap 4 dependencies and optimize final implementation

**Tasks:**

1. **Dependency Removal:**
   - Remove Bootstrap 4 packages from package.json
   - Remove BootstrapVue from package.json
   - Clean up isolation CSS scoping
   - Remove compatibility shims

2. **Build Optimization:**
   - Tree-shake unused Bootstrap 5 components
   - Optimize CSS bundle (PurgeCSS)
   - Lazy load non-critical components
   - Implement route-based code splitting

3. **Performance Tuning:**
   - Optimize Vue component rendering
   - Implement virtual scrolling for large lists
   - Add service worker caching
   - Optimize image loading

4. **Documentation:**
   - Component usage examples
   - Migration lessons learned
   - Architecture decision records
   - Troubleshooting guide

5. **Knowledge Transfer:**
   - Team training sessions
   - Code walkthrough
   - Q&A documentation
   - Video tutorials

---

## Risks and Mitigation

### Risk 1: Longer Timeline Than Expected

**Likelihood:** Medium
**Impact:** Medium

**Mitigation:**
- Build buffer into timeline (add 20% contingency)
- Identify scope cut candidates early (nice-to-have features)
- Conduct spike stories for complex components before full implementation
- Use feature flags to deploy partially complete work

**Contingency:**
- Extend Phase 3 by 2-4 weeks if needed
- Prioritize critical user paths first
- Accept technical debt on low-usage features if necessary

---

### Risk 2: Custom Component Library Bugs

**Likelihood:** High
**Impact:** Medium

**Mitigation:**
- Comprehensive test coverage (85%+ unit, integration, e2e)
- Visual regression testing with Percy or Chromatic
- Beta testing period with internal users
- Gradual rollout using feature flags
- Maintain rollback capability

**Contingency:**
- Quick hotfix process for critical bugs
- Fallback to Bootstrap 4 isolated version if catastrophic issues
- Dedicated bug triage during first 2 weeks post-launch

---

### Risk 3: Performance Regression

**Likelihood:** Low
**Impact:** High

**Mitigation:**
- Establish performance baselines before migration
- Monitor bundle size throughout development (budget: <500KB gzipped)
- Lighthouse CI in pull request pipeline
- Real User Monitoring (RUM) on staging
- Load testing with realistic data volumes

**Contingency:**
- Performance sprint if metrics degrade >10%
- Emergency optimizations (lazy loading, code splitting)
- CDN optimization for static assets

---

### Risk 4: Accessibility Regressions

**Likelihood:** Medium
**Impact:** High

**Mitigation:**
- Automated accessibility testing (axe-core, WAVE)
- Manual screen reader testing (NVDA, JAWS, VoiceOver)
- Keyboard navigation testing for all interactions
- ARIA attribute validation
- Color contrast verification

**Contingency:**
- Accessibility audit by external expert if issues found
- Dedicated accessibility remediation sprint
- User testing with assistive technology users

---

### Risk 5: Team Capacity Constraints

**Likelihood:** Medium
**Impact:** Medium

**Mitigation:**
- Cross-train team members on Vue 3 and Bootstrap 5
- Pair programming for knowledge sharing
- External contractor support if needed
- Clear documentation for asynchronous collaboration

**Contingency:**
- Adjust timeline if key team members unavailable
- Reduce scope to MVP feature set
- Extend migration across more sprints

---

### Risk 6: Breaking Changes in Dependencies

**Likelihood:** Low
**Impact:** Medium

**Mitigation:**
- Lock dependency versions during active development
- Monitor security advisories
- Test upgrades in isolated branch before merging
- Maintain changelog of dependency updates

**Contingency:**
- Emergency patch process for critical security issues
- Temporary workarounds for breaking changes
- Consider forking dependencies if unmaintained

---

## Success Metrics

### Technical Metrics

- **Bundle Size:** Reduce JavaScript bundle by 30%+ (target: <500KB gzipped)
- **Load Time:** First Contentful Paint <1.5s, Time to Interactive <3s
- **Test Coverage:** Maintain 85%+ code coverage
- **Accessibility:** WCAG 2.1 AA compliance (zero critical violations)
- **Browser Support:** 100% functionality on Chrome, Firefox, Safari, Edge (latest 2 versions)

### Business Metrics

- **User Satisfaction:** No increase in support tickets related to Activity Finder
- **Feature Velocity:** Maintain or improve sprint velocity after migration complete
- **Developer Experience:** Reduce onboarding time for new developers by 40%
- **Security:** Zero known vulnerabilities in dependencies

### Operational Metrics

- **Deployment Frequency:** No regression in deployment cadence
- **Mean Time to Recovery:** <1 hour for critical Activity Finder bugs
- **Monitoring Coverage:** 100% of critical user paths instrumented

---

## Decision

**Status:** Pending approval
**Recommended Option:** Option 4 - Hybrid Isolation + Gradual Migration
**Timeline:** 20 weeks (5 months)
**Budget:** 2 senior developers @ 50% capacity + 1 QA engineer @ 25% capacity

**Next Steps:**

1. Stakeholder approval (Product Owner, Tech Lead)
2. Resource allocation confirmation
3. Kickoff meeting and team alignment
4. Phase 1 implementation start

**Approval Required By:**
- [ ] Product Owner
- [ ] Technical Lead
- [ ] QA Lead
- [ ] UX/Design Lead

---

## References

- [Bootstrap 5 Migration Guide](https://getbootstrap.com/docs/5.3/migration/)
- [Vue 3 Migration Guide](https://v3-migration.vuejs.org/)
- [BootstrapVueNext Documentation](https://bootstrap-vue-next.github.io/bootstrap-vue-next/)
- [YMCA Activity Finder Architecture Documentation](../architecture/activity-finder.md)
- [Performance Budget Policy](../standards/performance-budget.md)

---

**Document History:**

| Version | Date | Author | Changes |
|---------|------|--------|---------|
| 1.0 | 2025-10-17 | Development Team | Initial decision document |
