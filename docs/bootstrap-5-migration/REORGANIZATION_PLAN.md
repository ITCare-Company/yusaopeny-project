# Bootstrap 5 Migration - Documentation Reorganization Plan

## Problem
Current documentation is too large and difficult to execute:
- MIGRATION_STRATEGY.md: **2,263 lines** ❌
- SPRINT_PLAN.md: **1,479 lines** ❌
- README.md: 293 lines ✅

**Solution:** Split into focused, actionable documents **< 300 lines each**

---

## Proposed New Structure

```
docs/bootstrap-5-migration/
├── README.md (< 300 lines) - Navigation hub
├── EXECUTIVE_SUMMARY.md (< 150 lines) - High-level overview
├── MODULE_INVENTORY.md (< 300 lines) - Complete list of 66+ modules
├── QUICK_START.md (< 200 lines) - How to start migration work
├── BREAKING_CHANGES.md (< 250 lines) - Bootstrap 4 → 5 changes
│
├── phases/
│   ├── PHASE_1_PREPARATION.md (< 300 lines)
│   ├── PHASE_2_CORE_THEME.md (< 300 lines)
│   ├── PHASE_3_LAYOUT_BUILDER.md (< 300 lines)
│   ├── PHASE_4_ACTIVITY_FINDER.md (< 300 lines)
│   ├── PHASE_5_WEBSITE_SERVICES.md (< 300 lines)
│   ├── PHASE_6_CONTENT_TYPES.md (< 300 lines)
│   ├── PHASE_7_SUPPORTING.md (< 300 lines)
│   └── PHASE_8_TESTING_ROLLOUT.md (< 300 lines)
│
├── sprints/
│   ├── SPRINT_01_Infrastructure.md (< 250 lines)
│   ├── SPRINT_02_Theme_Part1.md (< 250 lines)
│   ├── SPRINT_03_Theme_Part2_AF_Isolation.md (< 250 lines)
│   ├── SPRINT_04_WS_SmallY_Batch1.md (< 250 lines)
│   ├── SPRINT_05_WS_SmallY_Batch2.md (< 250 lines)
│   ├── SPRINT_06_WS_Other_Modules.md (< 250 lines)
│   ├── SPRINT_07_Testing_Catchup.md (< 250 lines)
│   ├── SPRINT_08_LB_HighPriority_Batch1.md (< 250 lines)
│   ├── SPRINT_09_LB_HighPriority_Batch2.md (< 250 lines)
│   ├── SPRINT_10_LB_MediumPriority_Batch1.md (< 250 lines)
│   ├── SPRINT_11_LB_MediumPriority_Batch2.md (< 250 lines)
│   ├── SPRINT_12_LB_LowerPriority.md (< 250 lines)
│   ├── SPRINT_13_LB_Integration_DatePicker.md (< 250 lines)
│   ├── SPRINT_14_Y_Branch_Related.md (< 250 lines)
│   ├── SPRINT_15_Y_Program_Camp.md (< 250 lines)
│   ├── SPRINT_16_Y_Facility_LB.md (< 250 lines)
│   ├── SPRINT_17_Y_Donate_Testing.md (< 250 lines)
│   ├── SPRINT_18_AF_Preparation_Audit.md (< 250 lines)
│   ├── SPRINT_19_AF_Camp_Finder.md (< 250 lines)
│   ├── SPRINT_20_AF_Activity_Finder.md (< 250 lines)
│   ├── SPRINT_21_AF_Activity_Finder4.md (< 250 lines)
│   ├── SPRINT_22_Comprehensive_Testing.md (< 250 lines)
│   ├── SPRINT_23_Documentation_Community.md (< 250 lines)
│   └── SPRINT_24_Staged_Rollout_Launch.md (< 250 lines)
│
├── modules/
│   ├── MODULES_THEME.md (< 150 lines) - openy_carnation details
│   ├── MODULES_LAYOUT_BUILDER.md (< 300 lines) - All 20 lb_* modules
│   ├── MODULES_WS_SMALL_Y.md (< 250 lines) - 16 small_y_* modules
│   ├── MODULES_CONTENT_TYPES.md (< 200 lines) - y_* modules
│   ├── MODULES_ACTIVITY_FINDER.md (< 250 lines) - 3 Vue apps
│   └── MODULES_OTHER.md (< 200 lines) - Supporting modules
│
├── decisions/
│   ├── QUESTIONNAIRE.md (existing - 497 lines → split)
│   ├── QUESTIONNAIRE_RESPONSES.md (existing - 291 lines ✅)
│   ├── DECISION_ACTIVITY_FINDER.md (< 250 lines)
│   ├── DECISION_DATE_PICKER.md (< 200 lines)
│   ├── DECISION_TESTING_STRATEGY.md (< 200 lines)
│   └── DECISION_ROLLOUT_STRATEGY.md (< 200 lines)
│
├── testing/
│   ├── TESTING_OVERVIEW.md (< 250 lines)
│   ├── TESTING_VISUAL_REGRESSION.md (< 250 lines)
│   ├── TESTING_ACCESSIBILITY.md (< 250 lines)
│   ├── TESTING_PERFORMANCE.md (< 200 lines)
│   └── TESTING_MATRIX.xlsx
│
└── reference/
    ├── BOOTSTRAP_5_CHEATSHEET.md (< 250 lines)
    ├── MIGRATION_CHECKLIST_TEMPLATE.md (< 200 lines)
    └── TROUBLESHOOTING.md (< 300 lines)
```

---

## Benefits of New Structure

### 1. **Actionable Documents**
- Each sprint = 1 file = 1 sprint's worth of work
- Developer can focus on current sprint only
- No need to scroll through 1,479 lines

### 2. **Easier Navigation**
- Clear folder structure by purpose
- Quick reference to specific areas
- README as central navigation hub

### 3. **Better for Execution**
- Can check off entire files as complete
- Easy to review specific phase/sprint
- Can assign specific files to team members

### 4. **Maintainable**
- Smaller files easier to update
- Changes don't affect entire plan
- Can version control changes better

### 5. **Scalable**
- Can add new sprints/phases easily
- Can add new modules to appropriate files
- Can extend without bloating

---

## Migration Steps

### Step 1: Create Core Documents
- [ ] EXECUTIVE_SUMMARY.md
- [ ] MODULE_INVENTORY.md
- [ ] QUICK_START.md
- [ ] BREAKING_CHANGES.md
- [ ] Update README.md with navigation

### Step 2: Split Phases
- [ ] Extract Phase 1 from MIGRATION_STRATEGY.md
- [ ] Extract Phase 2 from MIGRATION_STRATEGY.md
- [ ] Extract Phase 3 from MIGRATION_STRATEGY.md
- [ ] Extract Phase 4 from MIGRATION_STRATEGY.md
- [ ] Extract Phase 5 from MIGRATION_STRATEGY.md
- [ ] Extract Phase 6 from MIGRATION_STRATEGY.md
- [ ] Extract Phase 7 from MIGRATION_STRATEGY.md
- [ ] Extract Phase 8 from MIGRATION_STRATEGY.md

### Step 3: Split Sprints
- [ ] Create SPRINT_01 through SPRINT_24 files
- [ ] Extract content from SPRINT_PLAN.md
- [ ] Add navigation between sprints
- [ ] Add "Next Sprint" links

### Step 4: Create Module Documents
- [ ] MODULES_THEME.md
- [ ] MODULES_LAYOUT_BUILDER.md
- [ ] MODULES_WS_SMALL_Y.md
- [ ] MODULES_CONTENT_TYPES.md
- [ ] MODULES_ACTIVITY_FINDER.md
- [ ] MODULES_OTHER.md

### Step 5: Create Supporting Documents
- [ ] Testing documentation (4 files)
- [ ] Decision documents (4 files)
- [ ] Reference documents (3 files)

### Step 6: Archive Old Documents
- [ ] Move MIGRATION_STRATEGY.md to archive/
- [ ] Move SPRINT_PLAN.md to archive/
- [ ] Update all references to new structure

---

## Document Templates

### Phase Document Template (< 300 lines)
```markdown
# Phase X: [Name]

**Duration:** X weeks
**Sprints:** Sprint N - Sprint M
**Goal:** [Clear goal]

## Overview
[2-3 paragraphs]

## Key Deliverables
- [ ] Deliverable 1
- [ ] Deliverable 2

## Modules in This Phase
1. Module 1 (priority)
2. Module 2 (priority)

## Success Criteria
- [ ] Criterion 1
- [ ] Criterion 2

## Risks & Mitigation
**Risk:** [Risk]
**Mitigation:** [How to mitigate]

## Next Phase
See: [PHASE_X+1_NAME.md](PHASE_X+1_NAME.md)
```

### Sprint Document Template (< 250 lines)
```markdown
# Sprint X: [Name]

**Week:** Week X-Y
**Phase:** Phase N
**Resources:** X developers + Y contractors

## Sprint Goal
[1-2 sentences]

## Tasks

### Task 1: [Name]
**Estimate:** X hours
**Owner:** [Name]
**Description:** [Details]

**Acceptance Criteria:**
- [ ] Criterion 1
- [ ] Criterion 2

### Task 2: [Name]
[Same format]

## Testing
- [ ] Test 1
- [ ] Test 2

## Deliverables
- [ ] Deliverable 1
- [ ] Deliverable 2

## Notes
[Important notes]

## Navigation
- Previous: [Sprint X-1](SPRINT_0X_Name.md)
- Next: [Sprint X+1](SPRINT_0X_Name.md)
- Phase: [Phase N](../phases/PHASE_N_NAME.md)
```

### Module Document Template (< 50 lines per module)
```markdown
# Module: [module_name]

**Category:** Layout Builder / WS / Content Type / Other
**Bootstrap Version:** 4.4.1 / 5.3.3
**Priority:** High / Medium / Low
**Sprint:** Sprint X

## Location
`docroot/modules/contrib/[path]`

## Dependencies
- bootstrap: ^4.4.1
- Other dependencies

## Files to Update
- [ ] package.json
- [ ] webpack.config.js
- [ ] scss/*.scss (X files)
- [ ] templates/*.twig (X files)
- [ ] js/*.js (X files)

## Migration Notes
[Special considerations]

## Testing Checklist
- [ ] Build successful
- [ ] Visual appearance matches
- [ ] Interactive features work
- [ ] Responsive at all breakpoints
```

---

## Success Metrics

### Documentation Quality
- [ ] All documents < 300 lines
- [ ] Clear navigation between documents
- [ ] Easy to find information
- [ ] Actionable tasks in each document

### Execution
- [ ] Developers can work from sprint documents directly
- [ ] No confusion about what to do next
- [ ] Easy to track progress (file by file)
- [ ] Team can work in parallel (different files)

### Maintenance
- [ ] Easy to update specific sections
- [ ] Changes don't require editing massive files
- [ ] Version control diffs are meaningful
- [ ] Can review changes quickly

---

## Timeline for Reorganization

**Total Time:** 3-4 weeks (can be done in parallel with Sprint 1-2 of actual migration)

- Week 1: Core documents + Phase documents
- Week 2: Sprint documents (1-12)
- Week 3: Sprint documents (13-24) + Module documents
- Week 4: Testing/Decision/Reference documents + Archive old

---

## Questions?

This reorganization should happen **before** or **during** the first 2 sprints of actual migration work.

**Recommendation:** Start with creating the core documents (EXECUTIVE_SUMMARY, MODULE_INVENTORY, QUICK_START) and Phase 1-2 documents, then create sprint documents as needed (just-in-time approach).

---

**Status:** PROPOSED
**Last Updated:** 2025-10-17
**Next Action:** Review with team, get approval, start creating core documents
