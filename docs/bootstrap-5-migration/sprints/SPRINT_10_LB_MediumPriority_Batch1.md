# Sprint 10: Layout Builder Medium Priority - Batch 1

**Phase:** [Phase 3 - Layout Builder](../phases/PHASE_3_LAYOUT_BUILDER.md)
**Resources:** 1 Developer
**Status:** Not Started

---

## Sprint Goal

Migrate medium-priority Layout Builder modules focused on branch-specific components and promotional content.

---

## Modules in This Sprint

### 1. lb_branch_amenities_blocks
- **Path:** `docroot/modules/contrib/lb_branch_amenities_blocks`
- **Priority:** MEDIUM
- **Complexity:** LOW-MEDIUM
- **Reason:** Branch-specific, icon-based display

### 2. lb_branch_hours_blocks
- **Path:** `docroot/modules/contrib/lb_branch_hours_blocks`
- **Priority:** MEDIUM
- **Complexity:** LOW-MEDIUM
- **Reason:** Branch-specific, table/list display

### 3. lb_branch_social_links_blocks
- **Path:** `docroot/modules/contrib/lb_branch_social_links_blocks`
- **Priority:** MEDIUM
- **Complexity:** LOW
- **Reason:** Simple icon links

### 4. lb_ping_pong
- **Path:** `docroot/modules/contrib/lb_ping_pong`
- **Priority:** MEDIUM
- **Complexity:** MEDIUM
- **Reason:** Alternating content blocks with responsive behavior

### 5. lb_promo
- **Path:** `docroot/modules/contrib/lb_promo`
- **Priority:** MEDIUM
- **Complexity:** MEDIUM
- **Reason:** Promotional cards with images and CTAs

---

## Tasks

### Task 1: Migrate lb_branch_amenities_blocks
**Owner:** Developer
**Priority:** MEDIUM

**Actions:**
```bash
cd docroot/modules/contrib/lb_branch_amenities_blocks

# Study current implementation
cat package.json
cat templates/*.html.twig
cat assets/scss/*.scss
```

**Migration Steps:**

**1.1 Update package.json:**
```json
{
  "dependencies": {
    "bootstrap": "^5.3.3",
    "@popperjs/core": "^2.11.8"
  },
  "devDependencies": {
    "webpack": "^5.89.0",
    "webpack-cli": "^5.1.4",
    "sass": "^1.69.5",
    "sass-loader": "^13.3.2",
    "css-loader": "^6.8.1",
    "mini-css-extract-plugin": "^2.7.6"
  }
}
```

**1.2 Update webpack.config.js:**
- Follow lb_accordion pattern

**1.3 Update SCSS files:**
```scss
@import "bootstrap/scss/functions";
@import "bootstrap/scss/variables";
@import "bootstrap/scss/mixins";
@import "bootstrap/scss/utilities/api";

// Icon list styling
// Check for list-inline, list-unstyled usage
```

**1.4 Update Twig templates:**
- Review amenity icon layout
- Check for grid/flex usage
- Update icon spacing utilities
- Ensure responsive behavior

**1.5 Build and test:**
```bash
npm install
npm run build
```

**Deliverables:**
- [ ] `docs/bootstrap-5-migration/modules/lb_branch_amenities_blocks.md`
- [ ] Module built successfully

**Acceptance Criteria:**
- [ ] Amenity icons display correctly
- [ ] Grid layout responsive
- [ ] Icons align properly
- [ ] Tooltips work (if used)

---

### Task 2: Migrate lb_branch_hours_blocks
**Owner:** Developer
**Priority:** MEDIUM

**Actions:**
```bash
cd docroot/modules/contrib/lb_branch_hours_blocks

# Study current implementation
cat package.json
cat templates/*.html.twig
```

**Migration Steps:**

**2.1 Update package.json:**
- Same as Task 1

**2.2 Update webpack.config.js:**
- Follow lb_accordion pattern

**2.3 Update SCSS files:**
```scss
@import "bootstrap/scss/tables";
@import "bootstrap/scss/list-group";

// Bootstrap 5 changes:
// - Table borders: check customizations
// - List group: verify if used
```

**2.4 Update Twig templates:**
- Review hours display format (table vs. list)
- Check for table classes
- Update list group classes if used
- Ensure mobile-friendly display

**2.5 Handle responsive hours display:**
```twig
{# Ensure hours are readable on mobile #}
<table class="table table-sm">
  <tbody>
    <tr>
      <td>Monday</td>
      <td class="text-end">9am - 5pm</td>
    </tr>
  </tbody>
</table>
```

**Deliverables:**
- [ ] `docs/bootstrap-5-migration/modules/lb_branch_hours_blocks.md`
- [ ] Module built successfully

**Acceptance Criteria:**
- [ ] Hours display correctly
- [ ] Table/list responsive
- [ ] Readable on mobile
- [ ] Special hours highlighted (if applicable)

---

### Task 3: Migrate lb_branch_social_links_blocks
**Owner:** Developer
**Priority:** MEDIUM

**Actions:**
```bash
cd docroot/modules/contrib/lb_branch_social_links_blocks

# Study current implementation
cat package.json
cat templates/*.html.twig
```

**Migration Steps:**

**3.1 Update package.json:**
- Same as Task 1

**3.2 Update webpack.config.js:**
- Follow lb_accordion pattern

**3.3 Update SCSS files:**
```scss
// Social icon styling
// Check for custom icon colors
// Verify hover states
```

**3.4 Update Twig templates:**
- Review social icon layout
- Check for button vs. link styling
- Update icon spacing
- Ensure accessibility (aria-labels)

**3.5 Icon sizing and alignment:**
```twig
{# Social icons with proper sizing #}
<a href="#" class="btn btn-outline-primary btn-sm" aria-label="Facebook">
  <i class="fab fa-facebook-f"></i>
</a>
```

**Deliverables:**
- [ ] `docs/bootstrap-5-migration/modules/lb_branch_social_links_blocks.md`
- [ ] Module built successfully

**Acceptance Criteria:**
- [ ] Social icons display correctly
- [ ] Links work
- [ ] Hover states work
- [ ] Icons accessible (aria-labels present)
- [ ] Responsive layout

---

### Task 4: Migrate lb_ping_pong
**Owner:** Developer
**Priority:** MEDIUM

**Actions:**
```bash
cd docroot/modules/contrib/lb_ping_pong

# Study current implementation
cat package.json
cat templates/*.html.twig
cat assets/scss/*.scss
```

**Migration Steps:**

**4.1 Update package.json:**
- Same as Task 1

**4.2 Update webpack.config.js:**
- Follow lb_accordion pattern

**4.3 Update SCSS files:**
```scss
@import "bootstrap/scss/grid";

// Bootstrap 5 changes:
// - Grid system: verify column ordering
// - Order utilities: check for .order-* classes
```

**4.4 Update Twig templates:**
```twig
{# Alternating content blocks #}
<div class="row mb-4">
  <div class="col-md-6">
    <img src="..." class="img-fluid">
  </div>
  <div class="col-md-6">
    <h2>Title</h2>
    <p>Content</p>
  </div>
</div>

<div class="row mb-4">
  <div class="col-md-6 order-md-2">
    <img src="..." class="img-fluid">
  </div>
  <div class="col-md-6 order-md-1">
    <h2>Title</h2>
    <p>Content</p>
  </div>
</div>
```

**4.5 Handle responsive column ordering:**
- Verify `.order-*` utilities work correctly
- Test image/text alignment
- Check vertical centering (if used)

**Deliverables:**
- [ ] `docs/bootstrap-5-migration/modules/lb_ping_pong.md`
- [ ] Module built successfully

**Acceptance Criteria:**
- [ ] Alternating layout works
- [ ] Column ordering correct on desktop
- [ ] Stacks correctly on mobile
- [ ] Images scale properly
- [ ] Vertical alignment correct

---

### Task 5: Migrate lb_promo
**Owner:** Developer
**Priority:** MEDIUM

**Actions:**
```bash
cd docroot/modules/contrib/lb_promo

# Study current implementation
cat package.json
cat templates/*.html.twig
cat assets/scss/*.scss
```

**Migration Steps:**

**5.1 Update package.json:**
- Same as Task 1

**5.2 Update webpack.config.js:**
- Follow lb_accordion pattern

**5.3 Update SCSS files:**
```scss
@import "bootstrap/scss/card";
@import "bootstrap/scss/buttons";

// Promo card styling
// Check for card overlays
// Verify CTA button styling
```

**5.4 Update Twig templates:**
```twig
{# Promotional card #}
<div class="card">
  <img src="..." class="card-img-top" alt="...">
  <div class="card-body">
    <h5 class="card-title">Promo Title</h5>
    <p class="card-text">Promo description</p>
    <a href="#" class="btn btn-primary">Learn More</a>
  </div>
</div>

{# Or with image overlay #}
<div class="card text-white">
  <img src="..." class="card-img" alt="...">
  <div class="card-img-overlay">
    <h5 class="card-title">Promo Title</h5>
    <p class="card-text">Promo description</p>
    <a href="#" class="btn btn-light">Learn More</a>
  </div>
</div>
```

**5.5 Handle promo card variations:**
- Card with image on top
- Card with image overlay
- Card with background color
- Card with shadow/hover effects
- Grid of promo cards

**5.6 CTA button styling:**
- Verify button classes
- Check button sizes
- Test hover states

**Deliverables:**
- [ ] `docs/bootstrap-5-migration/modules/lb_promo.md`
- [ ] Module built successfully

**Acceptance Criteria:**
- [ ] Promo cards display correctly
- [ ] Images scale properly
- [ ] CTA buttons styled correctly
- [ ] Card layouts responsive
- [ ] Hover effects work
- [ ] Grid layouts work

---

## Testing

### Manual Testing Required

**For each module:**
1. **Visual Testing:**
   - [ ] Create test page with component
   - [ ] Verify appearance matches Bootstrap 4 version
   - [ ] Test all viewport sizes
   - [ ] Screenshot comparison

2. **Responsive Testing:**
   - [ ] 320px (mobile portrait)
   - [ ] 768px (tablet portrait)
   - [ ] 1024px (tablet landscape)
   - [ ] 1280px (desktop)

3. **Branch-Specific Modules:**
   - [ ] Test with real branch data
   - [ ] Verify amenity icons display
   - [ ] Verify hours formatting
   - [ ] Verify social links work

4. **Accessibility Testing:**
   - [ ] Run Pa11y on test pages
   - [ ] Check icon accessibility
   - [ ] Check link accessibility
   - [ ] Check heading hierarchy

### Automated Testing

**BackstopJS scenarios:**
```bash
cd docs/bootstrap-5-migration/testing

# Add scenarios for each module
npx backstop test
```

**Pa11y testing:**
```bash
npx pa11y-ci --reporter html > reports/sprint-10-pa11y.html
```

---

## Deliverables

### Must Have:
- [ ] All 5 modules migrated and tested
- [ ] Module migration notes created
- [ ] Test pages created
- [ ] All modules build without errors

### Nice to Have:
- [ ] Branch component pattern library
- [ ] Icon usage guide
- [ ] Promo card variations documented

---

## Decision Points

### Decision: Branch Hours Display Format
**Options:**
- A) Keep table format
- B) Switch to list format
- C) Support both

**Decision Required By:** End of Task 2
**Recommendation:** Keep existing format for consistency

---

## Risks

### Risk: Branch-Specific Data May Not Be Available for Testing
**Mitigation:**
- Use example/demo branch data
- Create test branch if needed
- Document required data structure

### Risk: Icon Libraries May Have Changed
**Mitigation:**
- Verify icon library versions (Font Awesome, etc.)
- Check for icon class name changes
- Update icon references if needed

---

## Notes

### Important:
- Branch modules are commonly customized per-site
- Test with real branch data if possible
- Document customization points
- Ping pong layout is tricky on mobile - test thoroughly

### Tips:
- These modules are simpler than Sprint 8-9
- Focus on responsive behavior
- Icon accessibility is important
- Card layouts from Sprint 8 can be referenced

---

## Sprint Review Checklist

At end of sprint, verify:
- [ ] All 5 modules migrated
- [ ] All tasks completed
- [ ] Testing complete
- [ ] No blocking issues
- [ ] Sprint 11 ready to start

---

## Navigation

- **Previous:** [Sprint 9 - LB High Priority Batch 2](SPRINT_09_LB_HighPriority_Batch2.md)
- **Next:** [Sprint 11 - LB Medium Priority Batch 2](SPRINT_11_LB_MediumPriority_Batch2.md)
- **Phase:** [Phase 3 - Layout Builder](../phases/PHASE_3_LAYOUT_BUILDER.md)
- **Overview:** [Executive Summary](../EXECUTIVE_SUMMARY.md)

---

**Sprint Status:** ⬜ Not Started
**Last Updated:** 2025-10-17
