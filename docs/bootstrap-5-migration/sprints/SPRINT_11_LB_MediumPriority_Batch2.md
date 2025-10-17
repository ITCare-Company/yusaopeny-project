# Sprint 11: Layout Builder Medium Priority - Batch 2

**Phase:** [Phase 3 - Layout Builder](../phases/PHASE_3_LAYOUT_BUILDER.md)
**Resources:** 1 Developer
**Status:** Not Started

---

## Sprint Goal

Migrate remaining medium-priority Layout Builder modules focused on grid layouts, content relationships, and navigation.

---

## Modules in This Sprint

### 1. lb_grid_cta (with lb_grid_icon submodule)
- **Path:** `docroot/modules/contrib/lb_grid_cta`
- **Priority:** MEDIUM
- **Complexity:** MEDIUM
- **Reason:** Grid layouts, icon grids, CTA buttons

### 2. lb_partners_blocks
- **Path:** `docroot/modules/contrib/lb_partners_blocks`
- **Priority:** MEDIUM
- **Complexity:** LOW-MEDIUM
- **Reason:** Logo grid display

### 3. lb_related_articles_blocks
- **Path:** `docroot/modules/contrib/lb_related_articles_blocks`
- **Priority:** MEDIUM
- **Complexity:** LOW-MEDIUM
- **Reason:** Article teaser display

### 4. lb_related_events_blocks
- **Path:** `docroot/modules/contrib/lb_related_events_blocks`
- **Priority:** MEDIUM
- **Complexity:** LOW-MEDIUM
- **Reason:** Event teaser display

### 5. lb_simple_menu
- **Path:** `docroot/modules/contrib/lb_simple_menu`
- **Priority:** MEDIUM
- **Complexity:** MEDIUM
- **Reason:** Menu navigation component

---

## Tasks

### Task 1: Migrate lb_grid_cta + lb_grid_icon
**Owner:** Developer
**Priority:** MEDIUM

**Actions:**
```bash
cd docroot/modules/contrib/lb_grid_cta

# Study current implementation
cat package.json
cat templates/*.html.twig
cat assets/scss/*.scss

# Check submodule
ls modules/lb_grid_icon/
cat modules/lb_grid_icon/templates/*.html.twig
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
@import "bootstrap/scss/grid";
@import "bootstrap/scss/buttons";

// Grid CTA styling
// Check for grid gutters
// Verify button styling
```

**1.4 Update Twig templates - Grid CTA:**
```twig
{# Grid of CTA cards #}
<div class="row row-cols-1 row-cols-md-2 row-cols-lg-3 g-4">
  {% for item in items %}
    <div class="col">
      <div class="card h-100 text-center">
        <div class="card-body d-flex flex-column">
          <h5 class="card-title">{{ item.title }}</h5>
          <p class="card-text">{{ item.description }}</p>
          <a href="{{ item.url }}" class="btn btn-primary mt-auto">{{ item.cta }}</a>
        </div>
      </div>
    </div>
  {% endfor %}
</div>
```

**1.5 Update Twig templates - Icon Grid (submodule):**
```twig
{# Grid of icons with text #}
<div class="row row-cols-2 row-cols-md-3 row-cols-lg-4 g-4 text-center">
  {% for item in items %}
    <div class="col">
      <div class="icon-grid-item">
        <i class="{{ item.icon_class }} fa-3x mb-3"></i>
        <h6>{{ item.title }}</h6>
        <p class="small text-muted">{{ item.description }}</p>
      </div>
    </div>
  {% endfor %}
</div>
```

**1.6 Handle responsive grid:**
- Test with different numbers of items (1-12)
- Verify equal height cards
- Test icon sizing and spacing
- Check button alignment

**Deliverables:**
- [ ] `docs/bootstrap-5-migration/modules/lb_grid_cta.md`
- [ ] Both main module and submodule migrated
- [ ] Module built successfully

**Acceptance Criteria:**
- [ ] CTA grid displays correctly
- [ ] Icon grid displays correctly
- [ ] Equal height cards work
- [ ] Buttons align at bottom
- [ ] Responsive at all breakpoints
- [ ] Icons sized appropriately

---

### Task 2: Migrate lb_partners_blocks
**Owner:** Developer
**Priority:** MEDIUM

**Actions:**
```bash
cd docroot/modules/contrib/lb_partners_blocks

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
@import "bootstrap/scss/grid";

// Partner logo styling
// Ensure logos scale properly
// Check for grayscale/hover effects
```

**2.4 Update Twig templates:**
```twig
{# Partner logo grid #}
<div class="row row-cols-2 row-cols-md-3 row-cols-lg-4 g-4 align-items-center">
  {% for partner in partners %}
    <div class="col text-center">
      <a href="{{ partner.url }}" class="partner-logo">
        <img src="{{ partner.logo }}" alt="{{ partner.name }}" class="img-fluid">
      </a>
    </div>
  {% endfor %}
</div>
```

**2.5 Handle logo display:**
- Ensure logos scale proportionally
- Check for max-width constraints
- Verify alignment (vertical centering)
- Test with different logo sizes/aspect ratios

**Deliverables:**
- [ ] `docs/bootstrap-5-migration/modules/lb_partners_blocks.md`
- [ ] Module built successfully

**Acceptance Criteria:**
- [ ] Partner logos display correctly
- [ ] Logos scale proportionally
- [ ] Grid responsive
- [ ] Logos align vertically
- [ ] Links work
- [ ] Hover effects work (if used)

---

### Task 3: Migrate lb_related_articles_blocks
**Owner:** Developer
**Priority:** MEDIUM

**Actions:**
```bash
cd docroot/modules/contrib/lb_related_articles_blocks

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
@import "bootstrap/scss/card";

// Article teaser styling
// Check for card styling
// Verify image aspect ratios
```

**3.4 Update Twig templates:**
```twig
{# Related articles #}
<div class="row row-cols-1 row-cols-md-2 row-cols-lg-3 g-4">
  {% for article in articles %}
    <div class="col">
      <div class="card h-100">
        {% if article.image %}
          <img src="{{ article.image }}" class="card-img-top" alt="{{ article.title }}">
        {% endif %}
        <div class="card-body">
          <h5 class="card-title">{{ article.title }}</h5>
          <p class="card-text text-muted small">{{ article.date }}</p>
          <p class="card-text">{{ article.summary }}</p>
          <a href="{{ article.url }}" class="stretched-link">Read more</a>
        </div>
      </div>
    </div>
  {% endfor %}
</div>
```

**3.5 Handle article display:**
- Equal height cards
- Image aspect ratio consistency
- Truncated summaries
- Date formatting
- "Read more" link styling

**Deliverables:**
- [ ] `docs/bootstrap-5-migration/modules/lb_related_articles_blocks.md`
- [ ] Module built successfully

**Acceptance Criteria:**
- [ ] Article teasers display correctly
- [ ] Images scale properly
- [ ] Cards equal height
- [ ] Links work
- [ ] Date formatting correct
- [ ] Responsive layout

---

### Task 4: Migrate lb_related_events_blocks
**Owner:** Developer
**Priority:** MEDIUM

**Actions:**
```bash
cd docroot/modules/contrib/lb_related_events_blocks

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

// Event teaser styling
// Similar to articles but with date prominence
```

**4.4 Update Twig templates:**
```twig
{# Related events #}
<div class="row row-cols-1 row-cols-md-2 row-cols-lg-3 g-4">
  {% for event in events %}
    <div class="col">
      <div class="card h-100">
        {% if event.image %}
          <img src="{{ event.image }}" class="card-img-top" alt="{{ event.title }}">
        {% endif %}
        <div class="card-body">
          <div class="badge bg-primary mb-2">{{ event.date }}</div>
          <h5 class="card-title">{{ event.title }}</h5>
          <p class="card-text">{{ event.summary }}</p>
          <a href="{{ event.url }}" class="stretched-link">Learn more</a>
        </div>
      </div>
    </div>
  {% endfor %}
</div>
```

**4.5 Handle event display:**
- Prominent date badge
- Time display
- Location display (if applicable)
- Registration CTA (if applicable)

**Deliverables:**
- [ ] `docs/bootstrap-5-migration/modules/lb_related_events_blocks.md`
- [ ] Module built successfully

**Acceptance Criteria:**
- [ ] Event teasers display correctly
- [ ] Date badges prominent
- [ ] Images scale properly
- [ ] Cards equal height
- [ ] Links work
- [ ] Responsive layout

---

### Task 5: Migrate lb_simple_menu
**Owner:** Developer
**Priority:** MEDIUM

**Actions:**
```bash
cd docroot/modules/contrib/lb_simple_menu

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
@import "bootstrap/scss/nav";
@import "bootstrap/scss/list-group";

// Bootstrap 5 changes:
// - Nav styles: verify variants
// - List group: check if used
```

**5.4 Update Twig templates:**
```twig
{# Simple navigation menu #}
<nav class="nav flex-column">
  {% for item in menu_items %}
    <a class="nav-link{% if item.active %} active{% endif %}" href="{{ item.url }}">
      {{ item.title }}
    </a>
  {% endfor %}
</nav>

{# Or horizontal variant #}
<nav class="nav">
  {% for item in menu_items %}
    <a class="nav-link{% if item.active %} active{% endif %}" href="{{ item.url }}">
      {{ item.title }}
    </a>
  {% endfor %}
</nav>

{# Or as list group #}
<div class="list-group">
  {% for item in menu_items %}
    <a href="{{ item.url }}" class="list-group-item list-group-item-action{% if item.active %} active{% endif %}">
      {{ item.title }}
    </a>
  {% endfor %}
</div>
```

**5.5 Handle menu variations:**
- Vertical menu
- Horizontal menu
- Menu with icons
- Menu with badges
- Active state styling
- Hover states

**5.6 Responsive behavior:**
- Mobile menu display
- Touch targets
- Scrollable menus (if long)

**Deliverables:**
- [ ] `docs/bootstrap-5-migration/modules/lb_simple_menu.md`
- [ ] Module built successfully

**Acceptance Criteria:**
- [ ] Menu displays correctly (vertical/horizontal)
- [ ] Active states work
- [ ] Hover states work
- [ ] Links work
- [ ] Responsive behavior correct
- [ ] Touch-friendly on mobile
- [ ] Keyboard navigation works

---

## Testing

### Manual Testing Required

**For each module:**
1. **Visual Testing:**
   - [ ] Create test page with component
   - [ ] Verify appearance matches Bootstrap 4 version
   - [ ] Test all viewport sizes
   - [ ] Screenshot comparison

2. **Grid Testing (Tasks 1-4):**
   - [ ] Test with different numbers of items
   - [ ] Verify equal heights
   - [ ] Check alignment
   - [ ] Test image scaling

3. **Navigation Testing (Task 5):**
   - [ ] Test active states
   - [ ] Test hover states
   - [ ] Test keyboard navigation
   - [ ] Test touch interactions

4. **Responsive Testing:**
   - [ ] 320px (mobile portrait)
   - [ ] 768px (tablet portrait)
   - [ ] 1024px (tablet landscape)
   - [ ] 1280px (desktop)

5. **Accessibility Testing:**
   - [ ] Run Pa11y on test pages
   - [ ] Check link accessibility
   - [ ] Check image alt text
   - [ ] Check keyboard navigation (menu)

### Automated Testing

**BackstopJS scenarios:**
```bash
cd docs/bootstrap-5-migration/testing

# Add scenarios for each module
npx backstop test
```

**Pa11y testing:**
```bash
npx pa11y-ci --reporter html > reports/sprint-11-pa11y.html
```

---

## Deliverables

### Must Have:
- [ ] All 5 modules migrated and tested
- [ ] Module migration notes created
- [ ] Test pages created
- [ ] All modules build without errors

### Nice to Have:
- [ ] Grid pattern library
- [ ] Menu variations documented
- [ ] Content relationship patterns documented

---

## Decision Points

### Decision: Menu Style Variant
**Options:**
- A) Keep existing nav style
- B) Switch to list-group style
- C) Support both

**Decision Required By:** End of Task 5
**Recommendation:** Keep existing style for consistency

---

## Risks

### Risk: Equal Height Cards May Not Work with Variable Content
**Mitigation:**
- Use flexbox (`.h-100` on cards)
- Test with varying content lengths
- Consider max-height + overflow for very long content
- Document content length recommendations

### Risk: Partner Logos May Have Different Aspect Ratios
**Mitigation:**
- Set max-width and max-height on logos
- Use object-fit if needed
- Consider adding padding/background
- Document logo requirements

---

## Notes

### Important:
- Grid layouts are core to these modules - test thoroughly
- Equal height cards are critical for visual consistency
- Menu accessibility is important (keyboard navigation)
- These modules often display dynamic content

### Tips:
- Use `.row-cols-*` for consistent grid layouts
- Use `.h-100` for equal height cards
- Use `.stretched-link` for clickable cards
- Test with real content, not just placeholder data

---

## Sprint Review Checklist

At end of sprint, verify:
- [ ] All 5 modules migrated
- [ ] All tasks completed
- [ ] Testing complete
- [ ] No blocking issues
- [ ] Sprint 12 ready to start

---

## Navigation

- **Previous:** [Sprint 10 - LB Medium Priority Batch 1](SPRINT_10_LB_MediumPriority_Batch1.md)
- **Next:** [Sprint 12 - LB Lower Priority](SPRINT_12_LB_LowerPriority.md)
- **Phase:** [Phase 3 - Layout Builder](../phases/PHASE_3_LAYOUT_BUILDER.md)
- **Overview:** [Executive Summary](../EXECUTIVE_SUMMARY.md)

---

**Sprint Status:** ⬜ Not Started
**Last Updated:** 2025-10-17
