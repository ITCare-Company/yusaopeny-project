# Sprint 8: Layout Builder High Priority - Batch 1

**Phase:** [Phase 3 - Layout Builder](../phases/PHASE_3_LAYOUT_BUILDER.md)
**Resources:** 1 Developer
**Status:** Not Started

---

## Sprint Goal

Migrate critical Layout Builder modules to Bootstrap 5, focusing on high-visibility components: hero, cards, and carousel.

---

## Modules in This Sprint

### 1. lb_hero
- **Path:** `docroot/modules/contrib/lb_hero`
- **Priority:** CRITICAL
- **Complexity:** MEDIUM
- **Reason:** Homepage hero component, high visibility

### 2. lb_cards
- **Path:** `docroot/modules/contrib/lb_cards`
- **Priority:** CRITICAL
- **Complexity:** MEDIUM
- **Reason:** Commonly used card layouts throughout site

### 3. lb_carousel
- **Path:** `docroot/modules/contrib/lb_carousel`
- **Priority:** CRITICAL
- **Complexity:** HIGH
- **Reason:** JavaScript API changed significantly in Bootstrap 5

---

## Tasks

### Task 1: Migrate lb_hero
**Owner:** Developer
**Priority:** CRITICAL

**Actions:**
```bash
cd docroot/modules/contrib/lb_hero

# Study current implementation
cat package.json
cat webpack.config.js
ls assets/scss/
cat templates/*.html.twig
cat js/*.js
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
- Ensure proper CSS extraction
- Configure SCSS loader

**1.3 Update SCSS files:**
```scss
// Import Bootstrap 5
@import "bootstrap/scss/functions";
@import "bootstrap/scss/variables";
@import "bootstrap/scss/mixins";

// Hero-specific styles
// Check for deprecated variables:
// $font-size-base, $line-height-base, etc.
```

**1.4 Update Twig templates:**
- Review `templates/block--lb-hero.html.twig`
- Update class names if needed
- No data attributes needed (hero is static)
- Ensure responsive classes: `container`, `row`, `col-*`

**1.5 Build and test:**
```bash
npm install
npm run build

# Verify dist/ folder created
ls dist/
```

**Deliverables:**
- [ ] `docs/bootstrap-5-migration/modules/lb_hero.md` - Migration notes
- [ ] lb_hero built successfully
- [ ] Hero displays correctly on test page

**Acceptance Criteria:**
- [ ] Bootstrap 5.3.3 installed
- [ ] Webpack builds without errors
- [ ] Hero renders correctly
- [ ] Responsive at all breakpoints
- [ ] Text overlays positioned correctly
- [ ] Background images/videos work

---

### Task 2: Migrate lb_cards
**Owner:** Developer
**Priority:** CRITICAL

**Actions:**
```bash
cd docroot/modules/contrib/lb_cards

# Study current implementation
cat package.json
ls templates/
cat assets/scss/*.scss
```

**Migration Steps:**

**2.1 Update package.json:**
- Same as lb_hero (Bootstrap 5.3.3)

**2.2 Update webpack.config.js:**
- Follow lb_accordion pattern

**2.3 Update SCSS files:**
```scss
// Import Bootstrap 5 card component
@import "bootstrap/scss/card";

// Bootstrap 5 changes:
// - .card-deck removed (use grid instead)
// - .card-columns removed (use grid instead)
// - Card borders: check if customizations needed
```

**2.4 Update Twig templates:**
- Review all card templates
- Check for `.card-deck` usage → replace with grid
- Check for `.card-columns` → replace with grid
- Update card structure if needed:
```twig
<div class="card">
  <img src="..." class="card-img-top" alt="...">
  <div class="card-body">
    <h5 class="card-title">Title</h5>
    <p class="card-text">Text</p>
    <a href="#" class="btn btn-primary">Link</a>
  </div>
</div>
```

**2.5 Handle grid layouts:**
```twig
{# Replace card-deck with grid #}
<div class="row row-cols-1 row-cols-md-2 row-cols-lg-3 g-4">
  <div class="col">
    <div class="card">...</div>
  </div>
</div>
```

**Deliverables:**
- [ ] `docs/bootstrap-5-migration/modules/lb_cards.md` - Migration notes
- [ ] lb_cards built successfully
- [ ] Card layouts documented

**Acceptance Criteria:**
- [ ] All card templates updated
- [ ] Grid layouts replace card-deck/card-columns
- [ ] Cards responsive at all breakpoints
- [ ] Card spacing consistent
- [ ] Images scale correctly
- [ ] Equal height cards work

---

### Task 3: Migrate lb_carousel
**Owner:** Developer
**Priority:** CRITICAL
**Complexity:** HIGH - JavaScript API changes

**Actions:**
```bash
cd docroot/modules/contrib/lb_carousel

# Study current implementation
cat package.json
cat js/*.js
cat templates/*.html.twig
```

**Migration Steps:**

**3.1 Update package.json:**
- Same as lb_hero (Bootstrap 5.3.3)

**3.2 Update webpack.config.js:**
- Follow lb_accordion pattern

**3.3 Update SCSS files:**
```scss
@import "bootstrap/scss/carousel";

// Check for carousel customizations
// Bootstrap 5 changes:
// - Carousel controls: check SVG icons
// - Carousel indicators: check styling
```

**3.4 Update Twig templates - Data attributes:**
```twig
{# Bootstrap 4 #}
<div class="carousel slide" data-ride="carousel">
  <div class="carousel-inner">
    <div class="carousel-item active">...</div>
  </div>
  <a class="carousel-control-prev" data-slide="prev">
  <a class="carousel-control-next" data-slide="next">
</div>

{# Bootstrap 5 #}
<div class="carousel slide" data-bs-ride="carousel">
  <div class="carousel-inner">
    <div class="carousel-item active">...</div>
  </div>
  <button class="carousel-control-prev" data-bs-slide="prev">
  <button class="carousel-control-next" data-bs-slide="next">
</div>
```

**Key Changes:**
- `data-ride` → `data-bs-ride`
- `data-slide` → `data-bs-slide`
- `data-target` → `data-bs-target`
- `<a>` controls → `<button>` controls (better accessibility)

**3.5 Update JavaScript:**
```javascript
// Bootstrap 4
$('#myCarousel').carousel({
  interval: 5000,
  pause: 'hover'
});

// Bootstrap 5
var myCarousel = new bootstrap.Carousel(document.getElementById('myCarousel'), {
  interval: 5000,
  pause: 'hover'
});

// OR use getInstance for existing carousel
var myCarousel = bootstrap.Carousel.getInstance(document.getElementById('myCarousel'));
myCarousel.next();
```

**3.6 Update events:**
```javascript
// Bootstrap 4
$('#myCarousel').on('slide.bs.carousel', function (e) {
  // e.direction, e.relatedTarget, e.from, e.to
});

// Bootstrap 5 - same events, different initialization
document.getElementById('myCarousel').addEventListener('slide.bs.carousel', function (event) {
  // event.direction, event.relatedTarget, event.from, event.to
});
```

**3.7 Test thoroughly:**
- Auto-play functionality
- Manual controls (prev/next)
- Indicators
- Touch/swipe on mobile
- Keyboard navigation
- Pause on hover
- Multiple carousels on same page

**Deliverables:**
- [ ] `docs/bootstrap-5-migration/modules/lb_carousel.md` - Migration notes
- [ ] JavaScript API changes documented
- [ ] lb_carousel built successfully

**Acceptance Criteria:**
- [ ] Carousel auto-plays correctly
- [ ] Prev/next controls work
- [ ] Indicators work
- [ ] Touch/swipe works on mobile
- [ ] Keyboard navigation works (arrow keys)
- [ ] Pause on hover works
- [ ] No JavaScript console errors
- [ ] Multiple carousels don't conflict

---

## Testing

### Manual Testing Required

**For each module:**
1. **Visual Testing:**
   - [ ] Create test page with component
   - [ ] Verify appearance matches Bootstrap 4 version
   - [ ] Test all viewport sizes (sm, md, lg, xl, xxl)
   - [ ] Screenshot baseline vs. new version

2. **Functional Testing (lb_carousel):**
   - [ ] Auto-play starts automatically
   - [ ] Controls advance slides
   - [ ] Indicators show current slide
   - [ ] Touch/swipe works on tablet/phone
   - [ ] Keyboard navigation works
   - [ ] Pause on hover works

3. **Responsive Testing:**
   - [ ] 320px (mobile portrait)
   - [ ] 768px (tablet portrait)
   - [ ] 1024px (tablet landscape)
   - [ ] 1280px (desktop)
   - [ ] 1920px (large desktop)

4. **Accessibility Testing:**
   - [ ] Run Pa11y on test pages
   - [ ] Check keyboard navigation
   - [ ] Check screen reader announcements (carousel)
   - [ ] Check ARIA attributes

### Automated Testing

**BackstopJS scenarios:**
```bash
cd docs/bootstrap-5-migration/testing

# Add scenarios for each module
npx backstop reference  # Bootstrap 4 baseline
npx backstop test       # Bootstrap 5 comparison
```

**Pa11y testing:**
```bash
npx pa11y-ci --reporter html > reports/sprint-8-pa11y.html
```

---

## Deliverables

### Must Have:
- [ ] lb_hero migrated and tested
- [ ] lb_cards migrated and tested
- [ ] lb_carousel migrated and tested
- [ ] All modules build without errors
- [ ] Module migration notes created
- [ ] Test pages created for each module

### Nice to Have:
- [ ] Video demo of carousel functionality
- [ ] Side-by-side comparison screenshots
- [ ] Pattern library entry for each module

---

## Decision Points

### Decision: Card Layout Strategy
**Options:**
- A) Use Bootstrap 5 grid with row-cols
- B) Use CSS Grid (custom)
- C) Mix of both based on use case

**Decision Required By:** End of Task 2
**Recommendation:** Option A (Bootstrap 5 grid) for consistency

### Decision: Carousel Control Element
**Options:**
- A) Keep `<a>` tags (backward compatible)
- B) Switch to `<button>` tags (better accessibility)

**Decision Required By:** End of Task 3
**Recommendation:** Option B (buttons) for accessibility

---

## Risks

### Risk: Carousel Touch Events May Not Work
**Mitigation:**
- Test on real devices (iPad, iPhone)
- Test touch-action CSS property
- Verify pointer events work
- Have fallback to button controls

### Risk: Card Grid Layouts Break Existing Designs
**Mitigation:**
- Document all card layout variants
- Test with different numbers of cards (1, 2, 3, 4, 6, 12)
- Review existing sites for card usage patterns
- Create migration guide for content editors

### Risk: Hero Background Images Don't Scale Correctly
**Mitigation:**
- Test with various image aspect ratios
- Check object-fit properties
- Test with video backgrounds
- Verify responsive behavior

---

## Notes

### Important:
- lb_carousel is the most complex module in this sprint due to JavaScript changes
- Test carousel extensively - it's a critical component
- Card layouts may need content editor documentation
- Hero components are often customized per-site - document customization points

### Tips:
- Use lb_accordion as reference for webpack/build setup
- Test carousel on real mobile devices, not just browser DevTools
- Document any Bootstrap 4 to 5 class name changes
- Take screenshots before/after for comparison

### Bootstrap 5 Carousel API Reference:
- [Bootstrap 5 Carousel Docs](https://getbootstrap.com/docs/5.3/components/carousel/)
- [Bootstrap 4 to 5 Migration Guide](https://getbootstrap.com/docs/5.3/migration/#carousel)

---

## Sprint Review Checklist

At end of sprint, verify:
- [ ] All 3 modules migrated
- [ ] All tasks completed
- [ ] All deliverables created
- [ ] Testing complete
- [ ] No blocking issues
- [ ] Sprint 9 ready to start

---

## Navigation

- **Previous:** [Sprint 7 - WS Other Modules](SPRINT_07_WS_Other.md)
- **Next:** [Sprint 9 - LB High Priority Batch 2](SPRINT_09_LB_HighPriority_Batch2.md)
- **Phase:** [Phase 3 - Layout Builder](../phases/PHASE_3_LAYOUT_BUILDER.md)
- **Overview:** [Executive Summary](../EXECUTIVE_SUMMARY.md)

---

**Sprint Status:** ⬜ Not Started
**Last Updated:** 2025-10-17
