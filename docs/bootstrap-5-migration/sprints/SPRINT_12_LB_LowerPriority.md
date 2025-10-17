# Sprint 12: Layout Builder Lower Priority

**Phase:** [Phase 3 - Layout Builder](../phases/PHASE_3_LAYOUT_BUILDER.md)
**Resources:** 1 Developer
**Status:** Not Started

---

## Sprint Goal

Migrate remaining lower-priority Layout Builder modules and complete all Layout Builder component migrations before integration testing.

---

## Modules in This Sprint

### 1. lb_staff_members_blocks
- **Path:** `docroot/modules/contrib/lb_staff_members_blocks`
- **Priority:** LOW-MEDIUM
- **Complexity:** MEDIUM
- **Reason:** Staff directory display with images

### 2. lb_statistics
- **Path:** `docroot/modules/contrib/lb_statistics`
- **Priority:** LOW-MEDIUM
- **Complexity:** LOW-MEDIUM
- **Reason:** Number display with animations (if used)

### 3. lb_table
- **Path:** `docroot/modules/contrib/lb_table`
- **Priority:** MEDIUM
- **Complexity:** MEDIUM
- **Reason:** Nested tables no longer inherit styles in Bootstrap 5

### 4. lb_testimonial_blocks
- **Path:** `docroot/modules/contrib/lb_testimonial_blocks`
- **Priority:** LOW-MEDIUM
- **Complexity:** LOW-MEDIUM
- **Reason:** Quote display with images

---

## Tasks

### Task 1: Migrate lb_staff_members_blocks
**Owner:** Developer
**Priority:** MEDIUM

**Actions:**
```bash
cd docroot/modules/contrib/lb_staff_members_blocks

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
@import "bootstrap/scss/card";

// Staff member card styling
// Photo aspect ratio consistency
// Contact info styling
```

**1.4 Update Twig templates:**
```twig
{# Staff member grid #}
<div class="row row-cols-1 row-cols-md-2 row-cols-lg-3 g-4">
  {% for staff in staff_members %}
    <div class="col">
      <div class="card h-100 text-center">
        {% if staff.photo %}
          <img src="{{ staff.photo }}" class="card-img-top rounded-circle mx-auto mt-3"
               alt="{{ staff.name }}" style="width: 150px; height: 150px; object-fit: cover;">
        {% endif %}
        <div class="card-body">
          <h5 class="card-title">{{ staff.name }}</h5>
          {% if staff.title %}
            <p class="text-muted">{{ staff.title }}</p>
          {% endif %}
          {% if staff.bio %}
            <p class="card-text">{{ staff.bio }}</p>
          {% endif %}
          {% if staff.email or staff.phone %}
            <div class="mt-3">
              {% if staff.email %}
                <a href="mailto:{{ staff.email }}" class="btn btn-sm btn-outline-primary">
                  <i class="fas fa-envelope"></i> Email
                </a>
              {% endif %}
              {% if staff.phone %}
                <a href="tel:{{ staff.phone }}" class="btn btn-sm btn-outline-primary">
                  <i class="fas fa-phone"></i> Call
                </a>
              {% endif %}
            </div>
          {% endif %}
        </div>
      </div>
    </div>
  {% endfor %}
</div>
```

**1.5 Handle staff photo display:**
- Circular photos with consistent sizing
- Fallback for missing photos
- Photo aspect ratio (square)
- Photo quality/resolution

**1.6 Handle contact information:**
- Email/phone link styling
- Social media links (if applicable)
- Modal for full bio (if applicable)

**Deliverables:**
- [ ] `docs/bootstrap-5-migration/modules/lb_staff_members_blocks.md`
- [ ] Module built successfully

**Acceptance Criteria:**
- [ ] Staff members display correctly
- [ ] Photos circular and consistent size
- [ ] Contact links work
- [ ] Equal height cards
- [ ] Responsive layout
- [ ] Missing photos handled gracefully

---

### Task 2: Migrate lb_statistics
**Owner:** Developer
**Priority:** MEDIUM

**Actions:**
```bash
cd docroot/modules/contrib/lb_statistics

# Study current implementation
cat package.json
cat templates/*.html.twig
cat js/*.js
```

**Migration Steps:**

**2.1 Update package.json:**
- Same as Task 1

**2.2 Update webpack.config.js:**
- Follow lb_accordion pattern

**2.3 Update SCSS files:**
```scss
@import "bootstrap/scss/functions";
@import "bootstrap/scss/variables";
@import "bootstrap/scss/mixins";

// Statistics display styling
// Large numbers
// Icons or graphics
// Counters (if animated)
```

**2.4 Update Twig templates:**
```twig
{# Statistics display #}
<div class="row row-cols-1 row-cols-md-2 row-cols-lg-4 g-4 text-center">
  {% for stat in statistics %}
    <div class="col">
      <div class="stat-item">
        {% if stat.icon %}
          <i class="{{ stat.icon }} fa-3x text-primary mb-3"></i>
        {% endif %}
        <div class="stat-number display-4 fw-bold text-primary">
          {{ stat.number }}
        </div>
        <div class="stat-label text-muted">
          {{ stat.label }}
        </div>
      </div>
    </div>
  {% endfor %}
</div>
```

**2.5 Handle number animations (if used):**
```javascript
// Bootstrap 5 - Count-up animation (if used)
// Check if CountUp.js or similar library is used
// Ensure animations work on scroll into view
```

**2.6 Number formatting:**
- Large numbers with commas (1,000 vs 1000)
- Percentages
- Currency
- Abbreviations (1K, 1M)

**Deliverables:**
- [ ] `docs/bootstrap-5-migration/modules/lb_statistics.md`
- [ ] Module built successfully

**Acceptance Criteria:**
- [ ] Statistics display correctly
- [ ] Numbers formatted properly
- [ ] Icons display correctly
- [ ] Animations work (if used)
- [ ] Responsive layout
- [ ] Accessible (screen reader friendly numbers)

---

### Task 3: Migrate lb_table
**Owner:** Developer
**Priority:** MEDIUM
**Complexity:** MEDIUM

**Actions:**
```bash
cd docroot/modules/contrib/lb_table

# Study current implementation
cat package.json
cat templates/*.html.twig
cat assets/scss/*.scss
```

**Migration Steps:**

**3.1 Update package.json:**
- Same as Task 1

**3.2 Update webpack.config.js:**
- Follow lb_accordion pattern

**3.3 Update SCSS files:**
```scss
@import "bootstrap/scss/tables";

// Bootstrap 5 changes:
// - Nested tables no longer inherit styles
// - Must explicitly opt-in nested tables
// - Table variants changed
```

**3.4 Update table classes:**
```twig
{# Bootstrap 4 #}
<table class="table table-striped">
  <thead>
    <tr>
      <th>Header</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td>Data</td>
    </tr>
  </tbody>
</table>

{# Bootstrap 5 - same, but nested tables need explicit class #}
<table class="table table-striped">
  <thead>
    <tr>
      <th>Header</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td>
        Data
        {# Nested table needs explicit class #}
        <table class="table">
          <tr><td>Nested</td></tr>
        </table>
      </td>
    </tr>
  </tbody>
</table>
```

**3.5 Handle table variants:**
```scss
// Bootstrap 5 table color variants changed
// .table-active, .table-primary, etc.
// Check if custom colors used
```

**3.6 Handle responsive tables:**
```twig
{# Responsive table wrapper #}
<div class="table-responsive">
  <table class="table">
    ...
  </table>
</div>
```

**3.7 Handle nested tables specifically:**
- Identify where nested tables are used
- Add explicit `.table` class to nested tables
- Test border styling
- Test striping behavior

**3.8 Mobile considerations:**
- Horizontal scrolling
- Column visibility
- Data table libraries (if used)

**Deliverables:**
- [ ] `docs/bootstrap-5-migration/modules/lb_table.md`
- [ ] Nested table handling documented
- [ ] Module built successfully

**Acceptance Criteria:**
- [ ] Tables display correctly
- [ ] Nested tables styled correctly
- [ ] Table variants work
- [ ] Responsive tables scroll horizontally on mobile
- [ ] Table borders correct
- [ ] Striping works correctly
- [ ] Accessible (proper th, scope attributes)

---

### Task 4: Migrate lb_testimonial_blocks
**Owner:** Developer
**Priority:** MEDIUM

**Actions:**
```bash
cd docroot/modules/contrib/lb_testimonial_blocks

# Study current implementation
cat package.json
cat templates/*.html.twig
```

**Migration Steps:**

**4.1 Update package.json:**
- Same as Task 1

**4.2 Update webpack.config.js:**
- Follow lb_accordion pattern

**4.3 Update SCSS files:**
```scss
@import "bootstrap/scss/card";

// Testimonial styling
// Quote marks
// Author photo
// Attribution
```

**4.4 Update Twig templates:**
```twig
{# Testimonial cards #}
<div class="row row-cols-1 row-cols-md-2 row-cols-lg-3 g-4">
  {% for testimonial in testimonials %}
    <div class="col">
      <div class="card h-100">
        <div class="card-body">
          <div class="mb-3">
            <i class="fas fa-quote-left fa-2x text-muted"></i>
          </div>
          <p class="card-text">{{ testimonial.quote }}</p>
        </div>
        <div class="card-footer bg-transparent">
          <div class="d-flex align-items-center">
            {% if testimonial.photo %}
              <img src="{{ testimonial.photo }}" class="rounded-circle me-3"
                   alt="{{ testimonial.author }}"
                   style="width: 50px; height: 50px; object-fit: cover;">
            {% endif %}
            <div>
              <div class="fw-bold">{{ testimonial.author }}</div>
              {% if testimonial.title %}
                <div class="text-muted small">{{ testimonial.title }}</div>
              {% endif %}
            </div>
          </div>
        </div>
      </div>
    </div>
  {% endfor %}
</div>

{# Or single featured testimonial #}
<div class="card text-center">
  <div class="card-body p-5">
    <i class="fas fa-quote-left fa-3x text-primary mb-4"></i>
    <p class="lead">{{ testimonial.quote }}</p>
    <div class="mt-4">
      <div class="fw-bold">{{ testimonial.author }}</div>
      {% if testimonial.title %}
        <div class="text-muted">{{ testimonial.title }}</div>
      {% endif %}
    </div>
  </div>
</div>
```

**4.5 Handle testimonial variations:**
- Grid of testimonials
- Single featured testimonial
- Carousel of testimonials (if used - coordinate with lb_carousel)
- With/without photos
- Star ratings (if applicable)

**Deliverables:**
- [ ] `docs/bootstrap-5-migration/modules/lb_testimonial_blocks.md`
- [ ] Module built successfully

**Acceptance Criteria:**
- [ ] Testimonials display correctly
- [ ] Quote marks styled appropriately
- [ ] Author photos circular and consistent
- [ ] Attribution formatted correctly
- [ ] Equal height cards (if grid)
- [ ] Responsive layout

---

### Task 5: Phase 3 Module Review & Documentation
**Owner:** Developer
**Priority:** HIGH

**Actions:**
```bash
# Review all Phase 3 modules (Sprints 8-12)
# Ensure consistency across modules
# Document patterns and best practices
```

**Review checklist:**

**5.1 Build verification:**
```bash
# Verify all LB modules build successfully
cd docroot/modules/contrib/

for module in lb_*/; do
  echo "Building $module..."
  cd $module
  if [ -f package.json ]; then
    npm install
    npm run build
    if [ $? -eq 0 ]; then
      echo "✓ $module built successfully"
    else
      echo "✗ $module build failed"
    fi
  fi
  cd ..
done
```

**5.2 Documentation review:**
- [ ] All module migration notes created
- [ ] Bootstrap 5 changes documented
- [ ] API changes documented (JavaScript components)
- [ ] Breaking changes documented

**5.3 Pattern library:**
- [ ] Common patterns identified
- [ ] Reusable components documented
- [ ] Best practices documented

**5.4 Create Phase 3 summary:**
```bash
# Create comprehensive summary
touch docs/bootstrap-5-migration/phases/PHASE_3_SUMMARY.md
```

**Deliverables:**
- [ ] Build verification report
- [ ] Phase 3 summary document
- [ ] Pattern library entries
- [ ] Known issues log

**Acceptance Criteria:**
- [ ] All 19 LB modules build successfully
- [ ] All migration notes complete
- [ ] Phase 3 summary created
- [ ] Ready for Sprint 13 integration testing

---

## Testing

### Manual Testing Required

**For each module:**
1. **Visual Testing:**
   - [ ] Create test page with component
   - [ ] Verify appearance matches Bootstrap 4 version
   - [ ] Test all viewport sizes
   - [ ] Screenshot comparison

2. **Content Testing:**
   - [ ] Test with real content
   - [ ] Test with missing content (graceful degradation)
   - [ ] Test with excessive content

3. **Responsive Testing:**
   - [ ] 320px (mobile portrait)
   - [ ] 768px (tablet portrait)
   - [ ] 1024px (tablet landscape)
   - [ ] 1280px (desktop)

4. **Accessibility Testing:**
   - [ ] Run Pa11y on test pages
   - [ ] Check table accessibility (task 3)
   - [ ] Check image alt text
   - [ ] Check link accessibility

### Automated Testing

**BackstopJS scenarios:**
```bash
cd docs/bootstrap-5-migration/testing

# Add scenarios for each module
npx backstop test
```

**Pa11y testing:**
```bash
npx pa11y-ci --reporter html > reports/sprint-12-pa11y.html
```

---

## Deliverables

### Must Have:
- [ ] All 4 modules migrated and tested
- [ ] Module migration notes created
- [ ] Build verification complete
- [ ] Phase 3 summary document
- [ ] All modules build without errors
- [ ] Ready for Sprint 13 integration testing

### Nice to Have:
- [ ] Pattern library complete
- [ ] Video demos of components
- [ ] Migration guide for content editors

---

## Decision Points

### Decision: Statistics Animation Library
**Options:**
- A) Keep existing animation library (if any)
- B) Switch to modern alternative
- C) Remove animations (simplest)

**Decision Required By:** End of Task 2
**Recommendation:** Option A or C based on complexity

---

## Risks

### Risk: Nested Tables May Break Existing Content (HIGH)
**Mitigation:**
- Identify all uses of nested tables
- Add explicit `.table` class to nested tables
- Test thoroughly with real content
- Create migration guide for content with nested tables
- Consider automated fix if many instances

### Risk: Staff Photos May Have Inconsistent Aspect Ratios
**Mitigation:**
- Use `object-fit: cover` for consistency
- Set fixed width/height
- Provide photo upload guidelines
- Consider cropping tool

### Risk: Statistics Animations May Conflict with Bootstrap 5
**Mitigation:**
- Test animation library compatibility early
- Have fallback to static numbers
- Check for JavaScript conflicts
- Consider removing animations if problematic

---

## Notes

### Important:
- This is the last sprint before integration testing
- Nested table changes in Bootstrap 5 are significant - test thoroughly
- These modules often use real organizational data - test with production content
- Phase 3 summary is critical for documentation

### Tips:
- Test nested tables extensively - this is a breaking change in Bootstrap 5
- Use consistent photo aspect ratios across all modules
- Equal height cards are important for testimonials and staff
- Document all patterns for reuse

### Bootstrap 5 Table Reference:
- [Bootstrap 5 Tables Docs](https://getbootstrap.com/docs/5.3/content/tables/)
- [Bootstrap 4 to 5 Table Migration](https://getbootstrap.com/docs/5.3/migration/#tables)

---

## Sprint Review Checklist

At end of sprint, verify:
- [ ] All 4 modules migrated
- [ ] All Phase 3 modules (Sprints 8-12) complete
- [ ] All tasks completed
- [ ] Build verification passed
- [ ] Phase 3 summary created
- [ ] No blocking issues
- [ ] Sprint 13 ready to start (integration testing)

---

## Navigation

- **Previous:** [Sprint 11 - LB Medium Priority Batch 2](SPRINT_11_LB_MediumPriority_Batch2.md)
- **Next:** [Sprint 13 - LB Integration & Date Picker](SPRINT_13_LB_Integration_DatePicker.md)
- **Phase:** [Phase 3 - Layout Builder](../phases/PHASE_3_LAYOUT_BUILDER.md)
- **Overview:** [Executive Summary](../EXECUTIVE_SUMMARY.md)

---

**Sprint Status:** ⬜ Not Started
**Last Updated:** 2025-10-17
