# Bootstrap 5 Migration - Decisions Index

**Total Decision Documents:** 4 (+ 2 questionnaire documents)
**Status:** Documented, decisions pending
**Last Updated:** 2025-10-17

---

## Quick Navigation

| Decision | Document | Status | Sprint | Priority |
|----------|----------|--------|--------|----------|
| **Activity Finder Strategy** | [DECISION_ACTIVITY_FINDER.md](DECISION_ACTIVITY_FINDER.md) | ⬜ Pending | Sprint 18 | ⭐⭐⭐ CRITICAL |
| **Date Picker Replacement** | [DECISION_DATE_PICKER.md](DECISION_DATE_PICKER.md) | ⬜ Pending | Sprint 1 | ⭐⭐ HIGH |
| **Testing Strategy** | [DECISION_TESTING_STRATEGY.md](DECISION_TESTING_STRATEGY.md) | ⬜ Pending | Sprint 1 | ⭐⭐ HIGH |
| **Rollout Strategy** | [DECISION_ROLLOUT_STRATEGY.md](DECISION_ROLLOUT_STRATEGY.md) | ⬜ Pending | Sprint 23 | ⭐⭐ HIGH |

**Supporting Documents:**
- [QUESTIONNAIRE.md](QUESTIONNAIRE.md) - Initial project questions (✅ Complete)
- [QUESTIONNAIRE_RESPONSES.md](QUESTIONNAIRE_RESPONSES.md) - Responses analysis (✅ Complete)

---

## Critical Decisions Overview

### Decision Timeline

```
Sprint 1: Date Picker + Testing Strategy
   ↓
Sprint 18: Activity Finder Strategy (before Phase 5)
   ↓
Sprint 23: Rollout Strategy (before launch)
```

---

## Decision Documents

### 1. Activity Finder Strategy (CRITICAL)

**Document:** [DECISION_ACTIVITY_FINDER.md](DECISION_ACTIVITY_FINDER.md)
**Lines:** ~587
**Status:** ⬜ Pending Decision
**Required By:** Sprint 18 (before Activity Finder migration starts)
**Priority:** ⭐⭐⭐ CRITICAL

**Problem:**
BootstrapVue 2 is **NOT compatible** with Bootstrap 5. The Activity Finder apps (Camp Finder, Activity Finder, Activity Finder 4) currently use:
- Vue 2.6.x
- Bootstrap 4.6.1
- BootstrapVue 2.22.0

BootstrapVue 3 is in alpha and not production-ready.

**Options:**

#### Option 1: Remove BootstrapVue, Use Bootstrap 5 Vanilla JS (RECOMMENDED)
**Approach:**
- Keep Vue 2
- Remove BootstrapVue completely
- Replace with Bootstrap 5 vanilla JavaScript + custom Vue wrappers
- Build shared component library

**Pros:**
- Full control over components
- Best performance (no extra framework)
- Keeps Vue 2 (stable)
- Reusable components across all 3 apps

**Cons:**
- Development effort required (~4 sprints)
- Need to build ~27 component replacements
- Testing burden

**Effort:** 4 sprints (18-21)

#### Option 2: Upgrade to Vue 3 + Custom Components
**Approach:**
- Upgrade Vue 2 → Vue 3
- Remove BootstrapVue
- Use Bootstrap 5 vanilla JS + Vue 3 Composition API

**Pros:**
- Modern Vue 3 (Composition API, better performance)
- Future-proof

**Cons:**
- Vue 2 → 3 migration significant effort
- Breaking changes in Vue 3
- Higher risk
- Longer timeline

**Effort:** 6-8 sprints

#### Option 3: Use Third-Party Bootstrap 5 + Vue Library
**Approach:**
- Try libraries like vue-bootstrap-next, bootstrap-vue-next

**Pros:**
- Less development effort (potentially)

**Cons:**
- Limited maturity (all in beta/alpha)
- Uncertain maintenance
- May not cover all needed components
- Risk of library abandonment

**Effort:** Unknown, risky

**Recommendation:** Option 1 - Remove BootstrapVue, Use Bootstrap 5 Vanilla JS

**See:** [DECISION_ACTIVITY_FINDER.md](DECISION_ACTIVITY_FINDER.md) for complete analysis

---

### 2. Date Picker Replacement

**Document:** [DECISION_DATE_PICKER.md](DECISION_DATE_PICKER.md)
**Lines:** ~996
**Status:** ⬜ Pending Decision
**Required By:** Sprint 1 (research), Sprint 21 (Activity Finder 4 implementation)
**Priority:** ⭐⭐ HIGH

**Problem:**
BootstrapVue provided `<b-form-datepicker>` and `<b-form-timepicker>` components. Bootstrap 5 has NO native date/time pickers. Activity Finder apps use date/time pickers extensively.

**Options:**

#### Option 1: Flatpickr (RECOMMENDED)
**Pros:**
- Lightweight (~10KB gzipped)
- Framework-agnostic
- Excellent documentation
- Actively maintained
- Time picker included
- Good accessibility
- Mobile-friendly

**Cons:**
- Not Bootstrap-native
- Requires Vue wrapper
- Custom styling needed for Bootstrap 5 look

**Bundle Size:** ~10KB gzipped
**Maintenance:** Active (last update recent)
**Accessibility:** Good
**Mobile Support:** Excellent

**Installation:**
```bash
npm install flatpickr vue-flatpickr-component
```

**Effort:** LOW-MEDIUM (2-3 days to integrate and style)

#### Option 2: Vuejs Datepicker
**Pros:**
- Vue-native
- Good documentation

**Cons:**
- Vue 2 only (uncertain Vue 3 support)
- Heavier (~15KB gzipped)
- Less actively maintained
- Separate time picker needed

**Bundle Size:** ~15KB gzipped
**Maintenance:** Uncertain
**Effort:** MEDIUM

#### Option 3: Litepicker
**Pros:**
- Very lightweight (~5KB gzipped)
- No dependencies
- Modern API

**Cons:**
- Less mature
- Smaller community
- Requires more custom work

**Bundle Size:** ~5KB gzipped
**Maintenance:** Active but smaller community
**Effort:** MEDIUM-HIGH

#### Option 4: Build Custom Picker
**Pros:**
- Full control
- Exactly what we need
- No dependencies

**Cons:**
- Significant development time
- Maintenance burden
- Accessibility complexity
- Mobile complexity

**Effort:** HIGH (5-7 days per picker type)

**Recommendation:** Option 1 - Flatpickr with Bootstrap 5 styling

**See:** [DECISION_DATE_PICKER.md](DECISION_DATE_PICKER.md) for complete analysis, demos, and styling examples

---

### 3. Testing Strategy

**Document:** [DECISION_TESTING_STRATEGY.md](DECISION_TESTING_STRATEGY.md)
**Lines:** ~1,183
**Status:** ⬜ Pending Decision
**Required By:** Sprint 1 (setup testing infrastructure)
**Priority:** ⭐⭐ HIGH

**Problem:**
With 66+ modules, 24 sprints, and ~11 months timeline, we need an efficient yet thorough testing approach that balances quality with velocity.

**Options:**

#### Option 1: 3-Tier Progressive Testing (RECOMMENDED)
**Approach:**
- **Tier 1 (Basic):** Per module - Quick checks (build, visual spot-check, smoke tests)
- **Tier 2 (Standard):** Per sprint - Visual regression (10 scenarios), accessibility (Pa11y), functional tests
- **Tier 3 (Comprehensive):** Phase-end + launch - Full suite (all scenarios, all breakpoints, security)

**Pros:**
- Efficient (not over-testing)
- Scales with project (more testing as you go)
- Catches issues early (Tier 1 per module)
- Thorough when needed (Tier 3 at milestones)

**Cons:**
- Requires discipline to follow tiers
- May miss some issues until later

**Effort:** 10-15% of development time

#### Option 2: Comprehensive Testing Always
**Approach:**
- Run full test suite for every module

**Pros:**
- Maximum quality
- Catches everything

**Cons:**
- Very slow (weeks per module)
- Over-testing (not all modules need full suite)
- Unsustainable for 66 modules

**Effort:** 40-50% of development time

#### Option 3: Minimal Testing (Build + Spot Check)
**Approach:**
- Only verify builds work and basic visual checks

**Pros:**
- Fast
- Low effort

**Cons:**
- High risk of bugs in production
- No accessibility verification
- No performance monitoring
- Could require major rework later

**Effort:** 2-5% of development time

**Recommendation:** Option 1 - 3-Tier Progressive Testing

**See:** [DECISION_TESTING_STRATEGY.md](DECISION_TESTING_STRATEGY.md) for complete tiers, tools, and timeline

---

### 4. Rollout Strategy

**Document:** [DECISION_ROLLOUT_STRATEGY.md](DECISION_ROLLOUT_STRATEGY.md)
**Lines:** ~1,539
**Status:** ⬜ Pending Decision
**Required By:** Sprint 23 (before staged rollout begins)
**Priority:** ⭐⭐ HIGH

**Problem:**
How do we safely deploy Bootstrap 5 migration to 100+ production YMCA sites without causing widespread issues? Need phased approach to minimize risk.

**Options:**

#### Option 1: Multi-Tier Staged Rollout (RECOMMENDED)
**Approach:**
4-tier rollout based on site criticality and risk tolerance:

**Tier D - Demo/Internal:**
- Internal demo sites
- Developer sites
- QA environments
- **Sites:** 2-5 sites
- **Purpose:** Final validation

**Tier C - Staging/Beta:**
- Customer staging sites
- Beta testers
- Low-traffic production sites
- **Sites:** 5-10 sites
- **Purpose:** Real-world validation

**Tier B - Small Production:**
- Small YMCAs (< 10K monthly visitors)
- Less complex sites
- **Sites:** 20-30 sites
- **Purpose:** Production validation at scale

**Tier A - Major Production:**
- Large YMCAs (> 10K monthly visitors)
- Complex sites with many customizations
- High-traffic sites
- **Sites:** 60-80+ sites
- **Purpose:** Full production rollout

**Rollback Plan:** Immediate rollback capability at each tier

**Pros:**
- Low risk (catches issues early on small sites)
- Controlled (can pause between tiers)
- Rollback is easy (smaller blast radius)
- Confidence builds with each tier

**Cons:**
- Longer timeline (6 weeks vs 1 week)
- More coordination needed
- Some sites wait longer

**Effort:** MEDIUM (coordination)

#### Option 2: Big Bang (All Sites at Once)
**Approach:**
- Deploy to all sites simultaneously
- Have support team ready

**Pros:**
- Fast (1 week)
- No tier management

**Cons:**
- Very high risk
- If issues found, affects ALL sites
- Rollback affects ALL sites
- Support overwhelmed if problems

**Effort:** HIGH (intense support)
**Risk:** CRITICAL

#### Option 3: Feature Flag Rollout
**Approach:**
- Deploy code to all sites
- Use feature flags to enable Bootstrap 5 per site
- Gradually enable

**Pros:**
- Code deployed once
- Fine-grained control
- Easy rollback (just disable flag)

**Cons:**
- Requires feature flag infrastructure
- Code must support both Bootstrap 4 and 5 simultaneously
- More complex codebase
- Additional development effort

**Duration:** 4-6 weeks
**Effort:** HIGH (infrastructure + dual support)

**Recommendation:** Option 1 - Multi-Tier Staged Rollout (D → C → B → A)

**See:** [DECISION_ROLLOUT_STRATEGY.md](DECISION_ROLLOUT_STRATEGY.md) for complete site tiers, rollout schedule, communication plan, and rollback procedures

---

## Supporting Documents

### Questionnaire (Complete)

**Document:** [QUESTIONNAIRE.md](QUESTIONNAIRE.md)
**Status:** ✅ Complete
**Purpose:** Initial project discovery questions

**Contents:**
- Project scope questions
- Timeline and resources
- Technical constraints
- Testing requirements
- Rollout considerations

**Use:** Reference for understanding initial project parameters

---

### Questionnaire Responses (Complete)

**Document:** [QUESTIONNAIRE_RESPONSES.md](QUESTIONNAIRE_RESPONSES.md)
**Status:** ✅ Complete
**Purpose:** Analyzed responses and recommendations

**Contents:**
- Response analysis
- Initial recommendations
- Risk assessment
- Resource needs
- Timeline estimates

**Use:** Reference for project planning decisions

---

## Decision-Making Process

### When Decisions Are Needed

1. **Sprint 1 Decisions:**
   - Date Picker replacement (research, decide by end of Sprint 1)
   - Testing Strategy (implement in Sprint 1)

2. **Sprint 18 Decision:**
   - Activity Finder Strategy (finalize before starting Phase 5)

3. **Sprint 23 Decision:**
   - Rollout Strategy (finalize before rollout begins)

### Decision Approval Process

**Recommended Process:**
1. Review decision document
2. Discuss pros/cons with team
3. Prototype/POC if needed (especially date picker)
4. Make decision
5. Document decision in project log
6. Proceed with implementation

### Decision Updates

As decisions are made:
- Update decision document with "Decision: [APPROVED/REJECTED]"
- Add decision date
- Add rationale for choice
- Link to any prototypes or POCs

---

## Related Documents

**Core Documentation:**
- [README.md](../README.md) - Main documentation hub
- [EXECUTIVE_SUMMARY.md](../EXECUTIVE_SUMMARY.md) - Project overview

**Phase Documentation:**
- [Phase 1: Preparation](../phases/PHASE_1_PREPARATION.md) - Sprint 1 decisions
- [Phase 5: Activity Finder](../phases/PHASE_5_ACTIVITY_FINDER.md) - Activity Finder decision
- [Phase 6: Testing & Rollout](../phases/PHASE_6_TESTING_ROLLOUT.md) - Rollout decision

**Sprint Documentation:**
- [Sprint 1](../sprints/SPRINT_01_Infrastructure.md) - Date picker & testing decisions
- [Sprint 18](../sprints/SPRINT_18_AF_Preparation.md) - Activity Finder decision
- [Sprint 23](../sprints/SPRINT_23_Documentation_Community.md) - Rollout decision

**Module Documentation:**
- [Activity Finder Apps](../modules/MODULES_ACTIVITY_FINDER.md) - Context for Activity Finder decision

**Testing Documentation:**
- [Testing Index](../testing/INDEX.md) - Context for testing strategy decision

---

## Navigation

- **← Back to:** [Main Documentation Hub](../README.md)
- **→ View Phases:** [Phases Index](../phases/INDEX.md)
- **→ View Sprints:** [Sprints Index](../sprints/INDEX.md)

### Direct Links to Decision Documents:
- [Activity Finder Strategy](DECISION_ACTIVITY_FINDER.md) - CRITICAL decision
- [Date Picker Replacement](DECISION_DATE_PICKER.md) - Sprint 1
- [Testing Strategy](DECISION_TESTING_STRATEGY.md) - Sprint 1
- [Rollout Strategy](DECISION_ROLLOUT_STRATEGY.md) - Sprint 23

### Supporting Documents:
- [Questionnaire](QUESTIONNAIRE.md) - Initial questions
- [Questionnaire Responses](QUESTIONNAIRE_RESPONSES.md) - Initial analysis

---

**Index Version:** 1.0
**Last Updated:** 2025-10-17
**Decision Documents:** 4
**Status:** All documented, decisions pending approval
