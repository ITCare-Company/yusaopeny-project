# Bootstrap 5 Migration - Granular PR Strategy

**Created:** 2025-10-17
**GitHub Project:** https://github.com/orgs/ITCare-Company/projects/5
**Fork:** git@github.com:ITCare-Company/yusaopeny-project.git
**Total PRs:** 60+ PRs (maximum granularity)

---

## PR Naming Convention

```
docs(bs5): [Category] - [Specific Focus]
```

**Examples:**
- `docs(bs5): Core - Add main README and navigation hub`
- `docs(bs5): Phase 1 - Preparation documentation`
- `docs(bs5): Sprint 1 - Infrastructure and research`

---

## Project Attributes for Each PR

**Status:** Todo (all PRs start here)
**Team:** Squad 1 (documentation team)
**Labels:** `documentation`, `bootstrap-5`, `planning`
**Milestone:** `Bootstrap 5 Migration - Documentation`

**Sprint-specific PRs also get:**
- **Labels:** `sprint-X`, `phase-Y`
- **Linked to:** Issue tracking that sprint (if created)

---

## Priority Order - Tier 1: CRITICAL (Sprint 1 Needs)

These must be merged first as they're needed for Sprint 1 work:

### PR #1: Core Documentation Hub
**Branch:** `docs/bs5-core-hub`
**Files:**
- README.md
- EXECUTIVE_SUMMARY.md
- MODULE_INVENTORY.md

**Priority:** CRITICAL
**Reason:** Main entry point and navigation

---

### PR #2: Developer Quick Start
**Branch:** `docs/bs5-quick-start`
**Files:**
- QUICK_START.md

**Priority:** CRITICAL
**Reason:** Needed for developers starting Sprint 1

---

### PR #3: Progress Tracker
**Branch:** `docs/bs5-progress`
**Files:**
- PROGRESS.md

**Priority:** HIGH
**Reason:** Track migration progress

---

### PR #4: Top-Level Indexes
**Branch:** `docs/bs5-indexes-main`
**Files:**
- phases/INDEX.md
- sprints/INDEX.md
- modules/INDEX.md
- testing/INDEX.md
- decisions/INDEX.md
- reference/INDEX.md

**Priority:** CRITICAL
**Reason:** Navigation structure for all documentation

---

### PR #5: Phase 1 - Preparation
**Branch:** `docs/bs5-phase1`
**Files:**
- phases/PHASE_1_PREPARATION.md

**Priority:** CRITICAL
**Reason:** Current phase documentation

---

### PR #6: Sprint 1 - Infrastructure
**Branch:** `docs/bs5-sprint1`
**Files:**
- sprints/SPRINT_01_Infrastructure.md

**Priority:** CRITICAL
**Reason:** Current sprint, needed immediately

---

### PR #7: Testing Documentation
**Branch:** `docs/bs5-testing-all`
**Files:**
- testing/TESTING_OVERVIEW.md
- testing/TESTING_VISUAL_REGRESSION.md
- testing/TESTING_ACCESSIBILITY.md
- testing/TESTING_PERFORMANCE.md

**Priority:** CRITICAL
**Reason:** Needed for Sprint 1 (setup testing infrastructure)

**Note:** Could split into 4 PRs if preferred:
- PR #7a: TESTING_OVERVIEW.md
- PR #7b: TESTING_VISUAL_REGRESSION.md
- PR #7c: TESTING_ACCESSIBILITY.md
- PR #7d: TESTING_PERFORMANCE.md

---

### PR #8: Reference - Bootstrap 5 Cheatsheet
**Branch:** `docs/bs5-ref-cheatsheet`
**Files:**
- reference/BOOTSTRAP_5_CHEATSHEET.md

**Priority:** CRITICAL
**Reason:** Daily reference for developers

---

### PR #9: Reference - Migration Checklist
**Branch:** `docs/bs5-ref-checklist`
**Files:**
- reference/MIGRATION_CHECKLIST_TEMPLATE.md

**Priority:** CRITICAL
**Reason:** Needed for Sprint 1 (create checklist)

---

### PR #10: Reference - LB Accordion Patterns
**Branch:** `docs/bs5-ref-lb-accordion`
**Files:**
- reference/LB_ACCORDION_PATTERNS.md

**Priority:** CRITICAL
**Reason:** Reference implementation for Sprint 1

---

### PR #11: Reference - Troubleshooting
**Branch:** `docs/bs5-ref-troubleshooting`
**Files:**
- reference/TROUBLESHOOTING.md

**Priority:** HIGH
**Reason:** Needed when developers encounter issues

---

### PR #12: Decisions - Date Picker
**Branch:** `docs/bs5-decision-datepicker`
**Files:**
- decisions/DECISION_DATE_PICKER.md

**Priority:** CRITICAL
**Reason:** Sprint 1 decision

---

### PR #13: Decisions - Testing Strategy
**Branch:** `docs/bs5-decision-testing`
**Files:**
- decisions/DECISION_TESTING_STRATEGY.md

**Priority:** CRITICAL
**Reason:** Sprint 1 decision

---

## Priority Order - Tier 2: HIGH (Planning & Next Sprints)

### PR #14: Sprint 2 - Theme Part 1
**Branch:** `docs/bs5-sprint2`
**Files:**
- sprints/SPRINT_02_Theme_Part1.md

**Priority:** HIGH
**Reason:** Next sprint after Sprint 1

---

### PR #15: Sprint 3 - Theme Part 2 + AF Isolation
**Branch:** `docs/bs5-sprint3`
**Files:**
- sprints/SPRINT_03_Theme_Part2_AF_Isolation.md

**Priority:** HIGH
**Reason:** Completes Phase 1

---

### PR #16: Module - Theme
**Branch:** `docs/bs5-module-theme`
**Files:**
- modules/MODULES_THEME.md

**Priority:** HIGH
**Reason:** Relates to Sprints 2-3

---

### PR #17: Phase 2 - Website Services
**Branch:** `docs/bs5-phase2`
**Files:**
- phases/PHASE_2_WEBSITE_SERVICES.md

**Priority:** HIGH
**Reason:** Next phase after Phase 1

---

### PR #18-21: Sprints 4-7 (Phase 2 Sprints)
**Branches:** `docs/bs5-sprint4` through `docs/bs5-sprint7`
**Files:**
- sprints/SPRINT_04_WS_SmallY_Batch1.md
- sprints/SPRINT_05_WS_SmallY_Batch2.md
- sprints/SPRINT_06_WS_Other_Modules.md
- sprints/SPRINT_07_Testing_Catchup.md

**Priority:** HIGH
**Reason:** Phase 2 sprints

---

### PR #22: Module - WS Small Y
**Branch:** `docs/bs5-module-ws-small-y`
**Files:**
- modules/MODULES_WS_SMALL_Y.md

**Priority:** HIGH
**Reason:** Relates to Sprints 4-5

---

### PR #23: Module - Other/Supporting
**Branch:** `docs/bs5-module-other`
**Files:**
- modules/MODULES_OTHER.md

**Priority:** MEDIUM
**Reason:** Relates to Sprint 6

---

## Priority Order - Tier 3: MEDIUM (Phase 3-4)

### PR #24: Phase 3 - Layout Builder
**Branch:** `docs/bs5-phase3`
**Files:**
- phases/PHASE_3_LAYOUT_BUILDER.md

**Priority:** MEDIUM
**Reason:** Future phase

---

### PR #25-30: Sprints 8-13 (Phase 3 Sprints)
**Branches:** `docs/bs5-sprint8` through `docs/bs5-sprint13`
**Files:**
- sprints/SPRINT_08_LB_HighPriority_Batch1.md
- sprints/SPRINT_09_LB_HighPriority_Batch2.md
- sprints/SPRINT_10_LB_MediumPriority_Batch1.md
- sprints/SPRINT_11_LB_MediumPriority_Batch2.md
- sprints/SPRINT_12_LB_LowerPriority.md
- sprints/SPRINT_13_LB_Integration_DatePicker.md

**Priority:** MEDIUM
**Reason:** Phase 3 sprints

---

### PR #31: Module - Layout Builder
**Branch:** `docs/bs5-module-lb`
**Files:**
- modules/MODULES_LAYOUT_BUILDER.md

**Priority:** MEDIUM
**Reason:** Relates to Sprints 8-13

---

### PR #32: Phase 4 - Content Types
**Branch:** `docs/bs5-phase4`
**Files:**
- phases/PHASE_4_CONTENT_TYPES.md

**Priority:** MEDIUM
**Reason:** Future phase

---

### PR #33-36: Sprints 14-17 (Phase 4 Sprints)
**Branches:** `docs/bs5-sprint14` through `docs/bs5-sprint17`
**Files:**
- sprints/SPRINT_14_Y_Branch_Related.md
- sprints/SPRINT_15_Y_Program_Camp.md
- sprints/SPRINT_16_Y_Facility_LB.md
- sprints/SPRINT_17_Y_Donate_Testing.md

**Priority:** MEDIUM
**Reason:** Phase 4 sprints

---

### PR #37: Module - Content Types
**Branch:** `docs/bs5-module-content-types`
**Files:**
- modules/MODULES_CONTENT_TYPES.md

**Priority:** MEDIUM
**Reason:** Relates to Sprints 14-17

---

## Priority Order - Tier 4: MEDIUM-LOW (Phase 5-6)

### PR #38: Phase 5 - Activity Finder
**Branch:** `docs/bs5-phase5`
**Files:**
- phases/PHASE_5_ACTIVITY_FINDER.md

**Priority:** MEDIUM
**Reason:** Critical phase but later in timeline

---

### PR #39-42: Sprints 18-21 (Phase 5 Sprints)
**Branches:** `docs/bs5-sprint18` through `docs/bs5-sprint21`
**Files:**
- sprints/SPRINT_18_AF_Preparation_Audit.md
- sprints/SPRINT_19_AF_Camp_Finder.md
- sprints/SPRINT_20_AF_Activity_Finder.md
- sprints/SPRINT_21_AF_Activity_Finder4.md

**Priority:** MEDIUM
**Reason:** Phase 5 sprints

---

### PR #43: Module - Activity Finder
**Branch:** `docs/bs5-module-af`
**Files:**
- modules/MODULES_ACTIVITY_FINDER.md

**Priority:** MEDIUM
**Reason:** Relates to Sprints 18-21

---

### PR #44: Decision - Activity Finder Strategy
**Branch:** `docs/bs5-decision-af`
**Files:**
- decisions/DECISION_ACTIVITY_FINDER.md

**Priority:** MEDIUM
**Reason:** Sprint 18 decision

---

### PR #45: Phase 6 - Testing & Rollout
**Branch:** `docs/bs5-phase6`
**Files:**
- phases/PHASE_6_TESTING_ROLLOUT.md

**Priority:** MEDIUM
**Reason:** Final phase

---

### PR #46-48: Sprints 22-24 (Phase 6 Sprints)
**Branches:** `docs/bs5-sprint22` through `docs/bs5-sprint24`
**Files:**
- sprints/SPRINT_22_Comprehensive_Testing.md
- sprints/SPRINT_23_Documentation_Community.md
- sprints/SPRINT_24_Staged_Rollout_Launch.md

**Priority:** MEDIUM
**Reason:** Phase 6 sprints

---

### PR #49: Decision - Rollout Strategy
**Branch:** `docs/bs5-decision-rollout`
**Files:**
- decisions/DECISION_ROLLOUT_STRATEGY.md

**Priority:** MEDIUM
**Reason:** Sprint 23 decision

---

## Priority Order - Tier 5: LOW (Supporting Documents)

### PR #50-51: Questionnaires
**Branch:** `docs/bs5-questionnaires`
**Files:**
- decisions/QUESTIONNAIRE.md
- decisions/QUESTIONNAIRE_RESPONSES.md

**Priority:** LOW
**Reason:** Historical/reference only

---

### PR #52: Reorganization Plan
**Branch:** `docs/bs5-reorg-plan`
**Files:**
- REORGANIZATION_PLAN.md

**Priority:** LOW
**Reason:** Meta-documentation

---

## PR Creation Process

### Step 1: Create Branch
```bash
git checkout bs_4_to_5
git pull origin bs_4_to_5
git checkout -b docs/bs5-[category]-[focus]
```

### Step 2: Copy/Move Files
```bash
# Files are already created, just need to stage
git add [files for this PR]
```

### Step 3: Commit (NO CLAUDE CREDITS)
```bash
git commit -m "docs(bs5): [Category] - [Specific Focus]

[Brief description of what's included]

Related: #49"
```

### Step 4: Push to Fork
```bash
git push fork docs/bs5-[category]-[focus]
```

### Step 5: Create PR via GitHub CLI
```bash
gh pr create \
  --repo ITCare-Company/yusaopeny-project \
  --base bs_4_to_5 \
  --head docs/bs5-[category]-[focus] \
  --title "docs(bs5): [Category] - [Specific Focus]" \
  --body "## Summary

[Description]

## Files Included
- file1.md
- file2.md

## Related
- Issue: #49
- Phase: X
- Sprint: Y

## Checklist
- [x] All files < 999 lines
- [x] No time estimates
- [x] No Claude credits
- [x] Links verified" \
  --label "documentation,bootstrap-5,planning"
```

### Step 6: Attach to GitHub Project
```bash
# Use gh CLI or web interface
gh project item-add 5 --owner ITCare-Company --url [PR_URL]
```

---

## Recommended Execution Order

**Week 1 - Tier 1 (PRs #1-13):**
- Day 1: PRs #1-4 (Core docs + indexes)
- Day 2: PRs #5-6 (Phase 1 + Sprint 1)
- Day 3: PR #7 (Testing docs - could split into 4)
- Day 4: PRs #8-11 (Reference docs)
- Day 5: PRs #12-13 (Decisions)

**Week 2 - Tier 2 (PRs #14-23):**
- Sprints 2-7 + Phase 2 + related modules

**Week 3 - Tier 3 (PRs #24-37):**
- Phases 3-4 + related sprints and modules

**Week 4 - Tier 4 (PRs #38-49):**
- Phases 5-6 + related sprints, modules, decisions

**Week 5 - Tier 5 (PRs #50-52):**
- Supporting/historical documents

---

## Alternative: Batch Some PRs

If 60+ PRs is too many, here's a consolidation strategy:

**Consolidation Option 1: Group Sprints by Phase**
- PR: "Sprints 1-3 (Phase 1)" - 3 files
- PR: "Sprints 4-7 (Phase 2)" - 4 files
- PR: "Sprints 8-13 (Phase 3)" - 6 files
- PR: "Sprints 14-17 (Phase 4)" - 4 files
- PR: "Sprints 18-21 (Phase 5)" - 4 files
- PR: "Sprints 22-24 (Phase 6)" - 3 files

**This reduces from 24 sprint PRs to 6 PRs**

**Consolidation Option 2: Group Testing Docs**
- PR: "Testing Documentation" - 4 files (instead of 4 PRs)

**Consolidation Option 3: Group Reference Docs**
- PR: "Reference Documentation" - 4 files (instead of 4 PRs)

**With all consolidations: ~35 PRs instead of 60+**

---

## Recommendation

**For maximum granularity (as requested):**
Go with the full 60+ PR strategy broken into tiers.

**For balanced approach:**
Use consolidations for sprints (group by phase) but keep everything else granular.

**My suggestion:**
- Keep Tier 1 (PRs #1-13) fully granular - these are CRITICAL
- Consolidate Tiers 2-4 sprints by phase (reduces 24 → 6)
- Keep phases, modules, decisions, reference granular

**Total: ~38 PRs with this approach**

---

**Created:** 2025-10-17
**Status:** Planning complete, ready for execution
