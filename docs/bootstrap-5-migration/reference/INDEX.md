# Bootstrap 5 Migration - Reference Materials Index

**Total Reference Documents:** 4
**Purpose:** Quick reference guides, templates, patterns, troubleshooting
**Status:** Documentation complete
**Last Updated:** 2025-10-17

---

## Quick Navigation

| Document | Purpose | Lines | Use Case |
|----------|---------|-------|----------|
| [BOOTSTRAP_5_CHEATSHEET.md](BOOTSTRAP_5_CHEATSHEET.md) | Bootstrap 4 → 5 quick reference | ~1,056 | Daily reference during migration |
| [MIGRATION_CHECKLIST_TEMPLATE.md](MIGRATION_CHECKLIST_TEMPLATE.md) | Reusable module migration checklist | ~831 | Per-module migration workflow |
| [TROUBLESHOOTING.md](TROUBLESHOOTING.md) | Common issues & solutions | ~1,415 | When stuck or encountering errors |
| [LB_ACCORDION_PATTERNS.md](LB_ACCORDION_PATTERNS.md) | Reference implementation analysis | ~1,252 | Learning from completed migration |

---

## Reference Documents

### 1. Bootstrap 5 Cheatsheet

**Document:** [BOOTSTRAP_5_CHEATSHEET.md](BOOTSTRAP_5_CHEATSHEET.md)
**Lines:** ~1,056
**Status:** ✅ Complete

**Purpose:**
Quick reference guide for Bootstrap 4 → Bootstrap 5 breaking changes, replacements, and new features.

**Contents:**

#### Utility Class Changes
```scss
// Bootstrap 4 → Bootstrap 5
.ml-3 → .ms-3  // margin-left → margin-start
.mr-3 → .me-3  // margin-right → margin-end
.pl-3 → .ps-3  // padding-left → padding-start
.pr-3 → .pe-3  // padding-right → padding-end

.text-left   → .text-start
.text-right  → .text-end
.float-left  → .float-start
.float-right → .float-end
```

#### Data Attribute Changes
```html
<!-- Bootstrap 4 → Bootstrap 5 -->
data-toggle="modal"    → data-bs-toggle="modal"
data-target="#modal"   → data-bs-target="#modal"
data-dismiss="alert"   → data-bs-dismiss="alert"
data-ride="carousel"   → data-bs-ride="carousel"
data-slide-to="2"      → data-bs-slide-to="2"
```

#### Removed Components
- **Jumbotron** - Removed, use utilities or custom CSS
- **Card Deck** - Removed, use grid system
- **Card Columns** - Removed, use grid system
- **Media Object** - Removed, use flex utilities

#### JavaScript Changes
```javascript
// Bootstrap 4 (jQuery)
$('#modal').modal('show');
$('#dropdown').dropdown('toggle');

// Bootstrap 5 (Vanilla JS)
const modal = new bootstrap.Modal(document.getElementById('modal'));
modal.show();

const dropdown = new bootstrap.Dropdown(document.getElementById('dropdown'));
dropdown.toggle();
```

#### Badge Changes
```html
<!-- Bootstrap 4 -->
<span class="badge badge-primary">Primary</span>
<span class="badge badge-pill badge-secondary">Pill</span>

<!-- Bootstrap 5 -->
<span class="badge bg-primary">Primary</span>
<span class="badge rounded-pill bg-secondary">Pill</span>
```

#### Form Changes
```html
<!-- Bootstrap 4 -->
<div class="form-group">
  <label>Email</label>
  <input type="email" class="form-control">
  <small class="form-text text-muted">Help text</small>
</div>

<!-- Bootstrap 5 -->
<div class="mb-3">
  <label class="form-label">Email</label>
  <input type="email" class="form-control">
  <div class="form-text">Help text</div>
</div>
```

**Use This For:**
- Quick lookups during migration
- Training developers on Bootstrap 5 changes
- Code review reference
- Automated find/replace reference

**Key Sections:**
- Utility class mappings
- Data attribute changes
- Component replacements
- JavaScript API changes
- Form class updates
- Color system changes
- Grid system updates

---

### 2. Migration Checklist Template

**Document:** [MIGRATION_CHECKLIST_TEMPLATE.md](MIGRATION_CHECKLIST_TEMPLATE.md)
**Lines:** ~831
**Status:** ✅ Complete

**Purpose:**
Reusable step-by-step checklist for migrating any module from Bootstrap 4 to Bootstrap 5.

**Contents:**

#### Pre-Migration
- [ ] Review module structure and dependencies
- [ ] Identify Bootstrap components used
- [ ] Create feature branch
- [ ] Create BackstopJS baseline
- [ ] Document current behavior

#### Migration Steps
- [ ] Update package.json (Bootstrap 4 → 5, Webpack 4 → 5)
- [ ] Update webpack.config.js
- [ ] Update SCSS imports
- [ ] Update templates (Twig/HTML)
  - [ ] Data attributes
  - [ ] Utility classes
  - [ ] Component markup
- [ ] Update JavaScript
  - [ ] Remove jQuery dependencies (if possible)
  - [ ] Update Bootstrap JavaScript API calls
- [ ] Build and verify (no errors)

#### Testing
- [ ] Visual regression testing (BackstopJS)
- [ ] Accessibility testing (Pa11y)
- [ ] Functional testing (interactive components)
- [ ] Browser compatibility
- [ ] Mobile responsive testing
- [ ] Performance check (Lighthouse)

#### Documentation
- [ ] Update module README
- [ ] Document breaking changes
- [ ] Update CHANGELOG
- [ ] Add migration notes

#### Completion
- [ ] Code review
- [ ] QA approval
- [ ] Merge to main branch
- [ ] Update progress tracker

**Use This For:**
- Starting migration on any module
- Ensuring no steps are missed
- Tracking progress per module
- Onboarding new developers

**Customization:**
Template includes placeholders for:
- Module name
- Sprint number
- Phase
- Specific components used
- Custom testing requirements

**Example:**
```markdown
# Module Migration Checklist: lb_cards

**Sprint:** Sprint 8
**Phase:** Phase 3 - Layout Builder
**Developer:** [Your Name]
**Start Date:** [Date]

## Pre-Migration Checklist
- [x] Module reviewed: Uses cards, card-deck, grid
- [x] Feature branch created: feature/lb-cards-bs5
- [x] Baseline created: backstop reference
...
```

---

### 3. Troubleshooting Guide

**Document:** [TROUBLESHOOTING.md](TROUBLESHOOTING.md)
**Lines:** ~1,415
**Status:** ✅ Complete

**Purpose:**
Comprehensive troubleshooting guide for common issues encountered during Bootstrap 5 migration.

**Contents:**

#### Build Issues

**Issue:** Webpack build fails with Bootstrap 5
```
ERROR in ./node_modules/bootstrap/scss/bootstrap.scss
Module not found: Error: Can't resolve '@popperjs/core'
```
**Solution:**
```bash
npm install @popperjs/core
```
Bootstrap 5 uses Popper.js v2 (as `@popperjs/core`). Bootstrap 4 used Popper.js v1.

---

**Issue:** SCSS compilation errors after upgrading
```
Error: Undefined variable: "$enable-rounded"
```
**Solution:**
Import Bootstrap variables before using them:
```scss
@import "~bootstrap/scss/functions";
@import "~bootstrap/scss/variables";
```

---

#### Visual Issues

**Issue:** Cards display in single column instead of deck layout
**Cause:** `.card-deck` removed in Bootstrap 5
**Solution:**
Replace with grid system:
```html
<!-- Bootstrap 4 -->
<div class="card-deck">
  <div class="card">...</div>
  <div class="card">...</div>
</div>

<!-- Bootstrap 5 -->
<div class="row row-cols-1 row-cols-md-3 g-4">
  <div class="col"><div class="card h-100">...</div></div>
  <div class="col"><div class="card h-100">...</div></div>
</div>
```

---

**Issue:** Jumbotron styling missing
**Cause:** `.jumbotron` removed in Bootstrap 5
**Solution Option 1 (Utilities):**
```html
<div class="bg-light p-5 rounded-3">
  <h1 class="display-4">Hello, world!</h1>
</div>
```

**Solution Option 2 (Custom CSS):**
```scss
.jumbotron {
  padding: 2rem 1rem;
  background-color: #e9ecef;
  border-radius: 0.3rem;

  @media (min-width: 576px) {
    padding: 4rem 2rem;
  }
}
```

---

**Issue:** Media object layout broken
**Cause:** `.media` and `.media-body` removed in Bootstrap 5
**Solution:**
```html
<!-- Bootstrap 4 -->
<div class="media">
  <img class="mr-3" src="...">
  <div class="media-body">...</div>
</div>

<!-- Bootstrap 5 -->
<div class="d-flex">
  <img class="me-3 flex-shrink-0" src="...">
  <div class="flex-grow-1">...</div>
</div>
```

---

#### JavaScript Issues

**Issue:** Modal won't open
**Error:** `Uncaught TypeError: $(...).modal is not a function`
**Cause:** Bootstrap 5 removed jQuery dependency
**Solution:**
```javascript
// Bootstrap 4 (jQuery)
$('#myModal').modal('show');

// Bootstrap 5 (Vanilla JS)
const modal = new bootstrap.Modal(document.getElementById('myModal'));
modal.show();

// Or with data attributes (still works)
<button data-bs-toggle="modal" data-bs-target="#myModal">
```

---

**Issue:** Dropdown not working
**Cause:** Data attributes changed in Bootstrap 5
**Solution:**
```html
<!-- Bootstrap 4 -->
<button data-toggle="dropdown">Dropdown</button>

<!-- Bootstrap 5 -->
<button data-bs-toggle="dropdown">Dropdown</button>
```

---

**Issue:** Popper.js errors in console
```
Uncaught ReferenceError: Popper is not defined
```
**Solution:**
Import Popper before Bootstrap:
```javascript
// webpack entry point
import '@popperjs/core';
import 'bootstrap';
```

Or use Bootstrap bundle (includes Popper):
```javascript
import 'bootstrap/dist/js/bootstrap.bundle.min.js';
```

---

#### Accessibility Issues

**Issue:** Pa11y reports missing alt attributes
**Solution:**
Ensure all images have alt text:
```html
<!-- Decorative image -->
<img src="icon.png" alt="">

<!-- Meaningful image -->
<img src="photo.jpg" alt="Staff member Jane Doe">
```

---

**Issue:** Color contrast failures
**Error:** `Element has insufficient color contrast (WCAG AA)`
**Solution:**
Adjust colors to meet contrast ratios:
- Normal text: 4.5:1
- Large text (18pt+ or 14pt+ bold): 3:1
- UI components: 3:1

Use tools:
- Chrome DevTools (Inspect → Accessibility)
- [WebAIM Contrast Checker](https://webaim.org/resources/contrastchecker/)

---

**Issue:** Form fields without labels
**Solution:**
```html
<!-- Bad -->
<input type="text" placeholder="Email">

<!-- Good -->
<label for="email">Email</label>
<input type="text" id="email">

<!-- Or with aria-label -->
<input type="text" aria-label="Email">
```

---

#### Performance Issues

**Issue:** Large bundle size after Bootstrap 5
**Solution:**
Import only needed components:
```javascript
// Instead of:
import 'bootstrap';

// Import selectively:
import { Modal, Dropdown, Collapse } from 'bootstrap';
```

And in SCSS:
```scss
// Instead of:
@import "~bootstrap/scss/bootstrap";

// Import selectively:
@import "~bootstrap/scss/functions";
@import "~bootstrap/scss/variables";
@import "~bootstrap/scss/mixins";
@import "~bootstrap/scss/grid";
@import "~bootstrap/scss/utilities";
// ... only what you need
```

---

**Issue:** Lighthouse performance score dropped
**Cause:** May be unrelated to Bootstrap, but check:
1. Bundle size increased
2. Unused CSS
3. Unoptimized images

**Solution:**
- Use Webpack Bundle Analyzer
- Remove unused CSS (PurgeCSS)
- Optimize images
- Lazy load below-the-fold content

---

#### Activity Finder Specific Issues

**Issue:** BootstrapVue component not working
**Cause:** BootstrapVue 2 incompatible with Bootstrap 5
**Solution:**
Must replace BootstrapVue components with custom components or Bootstrap 5 vanilla JS. See [Activity Finder Strategy Decision](../decisions/DECISION_ACTIVITY_FINDER.md).

---

**Key Sections:**
- Build/compilation issues
- Visual rendering issues
- JavaScript errors
- Data attribute problems
- Component replacement issues
- Accessibility failures
- Performance degradation
- Activity Finder specific
- Testing issues
- Deployment problems

**Use This For:**
- When encountering errors during migration
- Debugging visual issues
- Resolving JavaScript errors
- Fixing accessibility failures
- Performance optimization

---

### 4. LB Accordion Patterns (Reference Implementation)

**Document:** [LB_ACCORDION_PATTERNS.md](LB_ACCORDION_PATTERNS.md)
**Lines:** ~1,252
**Status:** ✅ Complete

**Purpose:**
In-depth analysis of the `lb_accordion` module - the ONLY module already migrated to Bootstrap 5 - as a reference implementation for other modules.

**Contents:**

#### Module Structure
```
docroot/modules/contrib/openy_lb/modules/lb_accordion/
├── css/
│   └── lb_accordion.css
├── js/
│   └── lb_accordion.js
├── src/
│   └── Plugin/
│       └── Block/
│           └── AccordionBlock.php
├── templates/
│   └── block--lb-accordion.html.twig
├── lb_accordion.info.yml
├── lb_accordion.libraries.yml
├── package.json
└── webpack.config.js
```

#### Webpack Configuration
```javascript
// webpack.config.js
const path = require('path');

module.exports = {
  entry: {
    'lb_accordion': './js/lb_accordion.js'
  },
  output: {
    path: path.resolve(__dirname, 'dist'),
    filename: '[name].min.js'
  },
  module: {
    rules: [
      {
        test: /\.scss$/,
        use: ['style-loader', 'css-loader', 'sass-loader']
      }
    ]
  }
};
```

#### Package.json
```json
{
  "dependencies": {
    "bootstrap": "^5.3.3",
    "@popperjs/core": "^2.11.8"
  },
  "devDependencies": {
    "webpack": "^5.88.0",
    "webpack-cli": "^5.1.4"
  }
}
```

#### Twig Template Patterns
```twig
{# block--lb-accordion.html.twig #}
<div class="accordion" id="accordion-{{ block_id }}">
  {% for item in items %}
    <div class="accordion-item">
      <h2 class="accordion-header" id="heading-{{ loop.index }}">
        <button
          class="accordion-button{% if not loop.first %} collapsed{% endif %}"
          type="button"
          data-bs-toggle="collapse"
          data-bs-target="#collapse-{{ loop.index }}"
          aria-expanded="{% if loop.first %}true{% else %}false{% endif %}"
          aria-controls="collapse-{{ loop.index }}"
        >
          {{ item.title }}
        </button>
      </h2>
      <div
        id="collapse-{{ loop.index }}"
        class="accordion-collapse collapse{% if loop.first %} show{% endif %}"
        aria-labelledby="heading-{{ loop.index }}"
        data-bs-parent="#accordion-{{ block_id }}"
      >
        <div class="accordion-body">
          {{ item.body }}
        </div>
      </div>
    </div>
  {% endfor %}
</div>
```

#### JavaScript Patterns
```javascript
// lb_accordion.js
import { Collapse } from 'bootstrap';

document.addEventListener('DOMContentLoaded', () => {
  // Initialize all accordions
  const accordions = document.querySelectorAll('.accordion');

  accordions.forEach(accordion => {
    // Bootstrap 5 Collapse API
    const collapseElements = accordion.querySelectorAll('.accordion-collapse');

    collapseElements.forEach(element => {
      new Collapse(element, { toggle: false });
    });
  });
});
```

#### Key Patterns to Replicate

**1. Data Attribute Updates:**
- ✅ `data-toggle` → `data-bs-toggle`
- ✅ `data-target` → `data-bs-target`
- ✅ `data-parent` → `data-bs-parent`

**2. JavaScript Initialization:**
- ✅ Import specific Bootstrap components: `import { Collapse } from 'bootstrap';`
- ✅ Use vanilla JS (no jQuery)
- ✅ Initialize with `new Collapse(element, options)`

**3. SCSS Structure:**
- ✅ Import Bootstrap selectively
- ✅ Custom overrides in separate file
- ✅ Use Bootstrap variables and mixins

**4. Webpack Setup:**
- ✅ Webpack 5
- ✅ Proper loaders (sass-loader, css-loader, style-loader)
- ✅ Output minified files

**5. Template Structure:**
- ✅ Proper ARIA attributes
- ✅ Unique IDs for accessibility
- ✅ Semantic HTML

**Use This For:**
- Understanding how to structure Bootstrap 5 modules
- Learning Webpack 5 configuration
- Seeing working Bootstrap 5 JavaScript integration
- Template structure reference
- Accessibility patterns

**Key Learnings:**
1. Always use `data-bs-*` prefixed attributes
2. Import only needed Bootstrap JS components
3. Initialize components with vanilla JS API
4. Proper ARIA attributes are critical
5. Webpack 5 setup is straightforward
6. No jQuery needed

---

## How to Use These References

### Daily Development:
1. **Start with:** [MIGRATION_CHECKLIST_TEMPLATE.md](MIGRATION_CHECKLIST_TEMPLATE.md) for structure
2. **Reference:** [BOOTSTRAP_5_CHEATSHEET.md](BOOTSTRAP_5_CHEATSHEET.md) for quick lookups
3. **Learn from:** [LB_ACCORDION_PATTERNS.md](LB_ACCORDION_PATTERNS.md) for patterns

### When Stuck:
1. **Check:** [TROUBLESHOOTING.md](TROUBLESHOOTING.md) first
2. **Search:** For your specific error message
3. **Follow:** Step-by-step solutions

### For New Modules:
1. **Copy:** Migration checklist template
2. **Review:** lb_accordion patterns
3. **Follow:** Checklist steps
4. **Reference:** Cheatsheet for specific changes

### For Code Review:
1. **Verify:** All checklist items completed
2. **Check:** Against cheatsheet (data attributes, utilities)
3. **Compare:** To lb_accordion patterns

---

## Related Documents

**Core Documentation:**
- [README.md](../README.md) - Main documentation hub
- [QUICK_START.md](../QUICK_START.md) - Developer onboarding guide

**Module Documentation:**
- [Modules Index](../modules/INDEX.md) - All module details
- [Layout Builder Modules](../modules/MODULES_LAYOUT_BUILDER.md) - lb_accordion context

**Testing Documentation:**
- [Testing Index](../testing/INDEX.md) - Testing strategy and tools

**Decision Documentation:**
- [Decisions Index](../decisions/INDEX.md) - Key decisions

---

## Navigation

- **← Back to:** [Main Documentation Hub](../README.md)
- **→ View Modules:** [Modules Index](../modules/INDEX.md)
- **→ View Testing:** [Testing Index](../testing/INDEX.md)

### Direct Links to Reference Documents:
- [Bootstrap 5 Cheatsheet](BOOTSTRAP_5_CHEATSHEET.md) - Quick reference
- [Migration Checklist](MIGRATION_CHECKLIST_TEMPLATE.md) - Per-module workflow
- [Troubleshooting](TROUBLESHOOTING.md) - Common issues
- [LB Accordion Patterns](LB_ACCORDION_PATTERNS.md) - Reference implementation

---

**Index Version:** 1.0
**Last Updated:** 2025-10-17
**Reference Documents:** 4
**Status:** ✅ All documents complete
