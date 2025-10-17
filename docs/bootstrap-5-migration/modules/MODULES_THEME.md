# Bootstrap 5 Migration - Theme Module Details

**Module Category:** Core Theme
**Total Modules:** 1
**Priority:** CRITICAL
**Phase:** Phase 1 (Sprints 2-3)
**Status:** Not Started

---

## Overview

The openy_carnation theme is the foundation of the entire Y USA Open YMCA distribution. It provides the base Bootstrap framework, styling, and JavaScript for all other modules and components. This migration must be completed first before any other module migrations can proceed.

**Critical Path:** All other migrations depend on theme completion

---

## Module: openy_carnation

### Basic Information

- **Path:** `docroot/themes/contrib/openy_carnation`
- **Type:** Drupal theme (contrib)
- **Bootstrap Version:** 4.4.1 → 5.3.3
- **Popper Version:** popper.js 1.16.0 → @popperjs/core 2.11.8
- **Build Tool:** Webpack 4 → Webpack 5
- **Priority:** CRITICAL
- **Risk Level:** HIGH
- **Sprint Assignment:** Sprint 2-3
- **Estimated Effort:** 3-4 weeks (2 sprints)

### Dependencies

**Current package.json dependencies:**
```json
{
  "dependencies": {
    "bootstrap": "^4.4.1",
    "jquery": "^3.5.1"
  },
  "devDependencies": {
    "popper.js": "^1.16.0",
    "webpack": "^4.44.0",
    "webpack-cli": "^3.3.12",
    // ... other dev dependencies
  }
}
```

**Target package.json dependencies:**
```json
{
  "dependencies": {
    "bootstrap": "^5.3.3",
    "@popperjs/core": "^2.11.8",
    "jquery": "^3.5.1"  // Keep for Drupal core compatibility
  },
  "devDependencies": {
    "webpack": "^5.91.0",
    "webpack-cli": "^5.1.4",
    "sass": "^1.75.0",
    "sass-loader": "^14.2.0",
    "css-loader": "^7.1.1",
    "mini-css-extract-plugin": "^2.8.1",
    // ... other dev dependencies
  }
}
```

### File Inventory

**SCSS Files (~60 files):**
```
src/scss/
├── style.scss                    # Main entry point - imports Bootstrap
├── _init.scss                    # Bootstrap variable overrides
├── _variables.scss               # Theme-specific variables
├── _overrides.scss               # Component overrides
├── component/                    # Component-specific styles (~25 files)
│   ├── _alert.scss
│   ├── _buttons.scss
│   ├── _cards.scss
│   ├── _filter.scss
│   ├── _form.scss
│   └── ...
├── modules/                      # Module-specific styles (~20 files)
│   ├── _af4.scss                # Activity Finder 4 styles
│   ├── _columns.scss
│   ├── _dialog.scss
│   ├── _forms.scss
│   ├── _header.scss
│   ├── _menu.scss
│   ├── _mobile-menu.scss
│   └── ...
├── paragraphs/                   # Paragraph type styles (~10 files)
└── regions/                      # Region-specific styles
```

**Twig Templates (~50 files):**
```
templates/
├── block/                        # Block templates
├── form/                         # Form templates (form-element.html.twig)
├── menu/                         # Menu templates
│   ├── menu--main--primary-menu.html.twig
│   └── mobile/
│       └── menu--main--mobile-menu.html.twig
├── node/                         # Node templates
│   ├── alert/                   # Alert node templates
│   ├── facility/                # Facility templates
│   └── ...
├── page/                         # Page templates (page.html.twig)
├── modules/                      # Module-specific templates
│   └── openy-faq-item.html.twig
└── openy_*/                      # Custom module templates
    ├── openy-calc-form-header.html.twig
    └── openy-repeat-schedule-dashboard--sidebar.html.twig
```

**JavaScript Files:**
```
dist/js/
├── openy_carnation.js           # Main theme JavaScript
├── openy_carnation_mobile.js    # Mobile-specific JavaScript
└── ...
```

**Build Configuration:**
```
webpack.build.js                 # Production build config
webpack.dev.js                   # Development build config
package.json                     # Dependencies and scripts
```

**Drupal Configuration:**
```
openy_carnation.info.yml         # Theme info file
openy_carnation.libraries.yml    # Asset libraries
openy_carnation.theme            # Theme preprocessors
```

---

## Migration Tasks

### 1. Update Dependencies (Sprint 2, Week 1)

**package.json:**
```bash
cd docroot/themes/contrib/openy_carnation

# Update Bootstrap
npm install bootstrap@^5.3.3 --save

# Update Popper
npm uninstall popper.js
npm install @popperjs/core@^2.11.8 --save

# Update Webpack
npm install webpack@^5.91.0 webpack-cli@^5.1.4 --save-dev

# Update Sass
npm install sass@^1.75.0 sass-loader@^14.2.0 --save-dev

# Update CSS loaders
npm install css-loader@^7.1.1 mini-css-extract-plugin@^2.8.1 --save-dev

# Install all dependencies
npm install
```

### 2. Update Webpack Configuration (Sprint 2, Week 1)

**webpack.build.js changes:**
- Update to Webpack 5 syntax
- Update MiniCssExtractPlugin configuration
- Update sass-loader configuration
- Remove deprecated options

**Example:**
```javascript
const MiniCssExtractPlugin = require('mini-css-extract-plugin');

module.exports = {
  mode: 'production',
  entry: {
    style: './src/scss/style.scss',
  },
  output: {
    path: path.resolve(__dirname, 'dist'),
    filename: '[name].js',
    clean: true  // Webpack 5 feature
  },
  module: {
    rules: [
      {
        test: /\.scss$/,
        use: [
          MiniCssExtractPlugin.loader,
          'css-loader',
          'sass-loader'
        ]
      }
    ]
  },
  plugins: [
    new MiniCssExtractPlugin({
      filename: 'css/[name].css'
    })
  ]
};
```

### 3. Update SCSS Files (Sprint 2, Weeks 1-2)

**Priority order:**
1. **Core files first**
   - `_init.scss` - Bootstrap variable overrides
   - `_variables.scss` - Theme variables
   - `style.scss` - Main entry point

2. **Component overrides**
   - `_overrides.scss` - Global overrides

3. **Component files**
   - `component/*.scss` (~25 files)
   - `modules/*.scss` (~20 files)
   - `paragraphs/*.scss` (~10 files)

**Common replacements needed:**

| Bootstrap 4 | Bootstrap 5 | Context |
|-------------|-------------|---------|
| `.ml-*` | `.ms-*` | Margin left → start |
| `.mr-*` | `.me-*` | Margin right → end |
| `.pl-*` | `.ps-*` | Padding left → start |
| `.pr-*` | `.pe-*` | Padding right → end |
| `.text-left` | `.text-start` | Text alignment |
| `.text-right` | `.text-end` | Text alignment |
| `.float-left` | `.float-start` | Float left |
| `.float-right` | `.float-end` | Float right |
| `.close` | `.btn-close` | Close button |
| `.custom-select` | `.form-select` | Select element |
| `.form-group` | `.mb-3` | Form spacing |
| `.media` | flexbox utilities | Media object |
| `.no-gutters` | `.g-0` | Grid gutters |
| `$grid-gutter-width` | Updated calculation | Grid system |

**Files requiring special attention:**
- `modules/_af4.scss` - Activity Finder 4 styles (coordinate with AF isolation)
- `modules/_forms.scss` - Form class changes
- `modules/_menu.scss` - Navigation dropdowns
- `modules/_mobile-menu.scss` - Mobile navigation
- `component/_buttons.scss` - Button classes
- `component/_form.scss` - Form components

### 4. Update Twig Templates (Sprint 2, Week 2)

**Automated replacements (use sed/grep):**
```bash
cd templates/

# Data attribute updates
find . -name "*.twig" -type f -exec sed -i.bak \
  -e 's/data-toggle="/data-bs-toggle="/g' \
  -e 's/data-target="/data-bs-target="/g' \
  -e 's/data-dismiss="/data-bs-dismiss="/g' \
  -e 's/data-slide="/data-bs-slide="/g' \
  -e 's/data-parent="/data-bs-parent="/g' \
  -e 's/data-ride="/data-bs-ride="/g' \
  {} +

# Class name updates (simple replacements)
find . -name "*.twig" -type f -exec sed -i.bak \
  -e 's/"close"/"btn-close"/g' \
  -e 's/"text-left"/"text-start"/g' \
  -e 's/"text-right"/"text-end"/g' \
  -e 's/"float-left"/"float-start"/g' \
  -e 's/"float-right"/"float-end"/g' \
  {} +
```

**Manual updates required:**

**Templates with `.btn-block`:**
```twig
{# Bootstrap 4 #}
<button class="btn btn-primary btn-block">Submit</button>

{# Bootstrap 5 #}
<div class="d-grid">
  <button class="btn btn-primary">Submit</button>
</div>
```

**Templates with `.form-group`:**
```twig
{# Bootstrap 4 #}
<div class="form-group">
  <label for="email">Email</label>
  <input type="email" class="form-control" id="email">
</div>

{# Bootstrap 5 #}
<div class="mb-3">
  <label for="email" class="form-label">Email</label>
  <input type="email" class="form-control" id="email">
</div>
```

**Templates with `.custom-select`:**
```twig
{# Bootstrap 4 #}
<select class="custom-select">
  <option>Select...</option>
</select>

{# Bootstrap 5 #}
<select class="form-select">
  <option>Select...</option>
</select>
```

**Templates with `.input-group-prepend` / `.input-group-append`:**
```twig
{# Bootstrap 4 #}
<div class="input-group">
  <div class="input-group-prepend">
    <span class="input-group-text">$</span>
  </div>
  <input type="text" class="form-control">
</div>

{# Bootstrap 5 - Simplified #}
<div class="input-group">
  <span class="input-group-text">$</span>
  <input type="text" class="form-control">
</div>
```

**Priority templates for manual review:**
1. `menu/menu--main--primary-menu.html.twig` - Main navigation dropdowns
2. `menu/mobile/menu--main--mobile-menu.html.twig` - Mobile menu
3. `form/form-element.html.twig` - Form elements
4. `page/page.html.twig` - Page structure
5. `node/alert/*.html.twig` - Alert components
6. `modules/openy-faq-item.html.twig` - FAQ accordions
7. `openy_calc/openy-calc-form-header.html.twig` - Calculator forms
8. `openy_repeat/openy-repeat-schedule-dashboard--sidebar.html.twig` - Schedule dashboard

### 5. Update JavaScript (Sprint 3, Week 1)

**Files to update:**
- `dist/js/openy_carnation.js`
- `dist/js/openy_carnation_mobile.js`

**Bootstrap 4 jQuery patterns → Bootstrap 5 vanilla JS:**

```javascript
// ============================================
// BOOTSTRAP 4 (jQuery-based)
// ============================================

// Modals
$('#myModal').modal('show');
$('#myModal').modal('hide');

// Dropdowns
$('.dropdown-toggle').dropdown();

// Collapse
$('#myCollapse').collapse('toggle');

// Tooltips
$('[data-toggle="tooltip"]').tooltip();

// Popovers
$('[data-toggle="popover"]').popover();

// Tabs
$('#myTab a').on('click', function (e) {
  e.preventDefault();
  $(this).tab('show');
});

// Carousels
$('.carousel').carousel();


// ============================================
// BOOTSTRAP 5 (Vanilla JS)
// ============================================

// Import Bootstrap components
import { Modal, Dropdown, Collapse, Tooltip, Popover, Tab } from 'bootstrap';

// Modals
const myModal = new Modal(document.getElementById('myModal'));
myModal.show();
myModal.hide();

// Or use getInstance for existing modals
const existingModal = Modal.getInstance(document.getElementById('myModal'));
if (existingModal) {
  existingModal.show();
}

// Dropdowns - auto-initialized via data attributes
// Manual initialization:
document.querySelectorAll('.dropdown-toggle').forEach(el => {
  new Dropdown(el);
});

// Collapse
const myCollapse = new Collapse(document.getElementById('myCollapse'));
myCollapse.toggle();

// Tooltips - must be manually initialized
document.querySelectorAll('[data-bs-toggle="tooltip"]').forEach(el => {
  new Tooltip(el);
});

// Popovers - must be manually initialized
document.querySelectorAll('[data-bs-toggle="popover"]').forEach(el => {
  new Popover(el);
});

// Tabs
document.querySelectorAll('#myTab button').forEach(tabEl => {
  tabEl.addEventListener('click', e => {
    e.preventDefault();
    const tab = new Tab(tabEl);
    tab.show();
  });
});

// Carousels - auto-initialized via data attributes
// Manual initialization:
import { Carousel } from 'bootstrap';
document.querySelectorAll('.carousel').forEach(el => {
  new Carousel(el);
});
```

**Event listeners also change:**
```javascript
// Bootstrap 4
$('#myModal').on('show.bs.modal', function (e) {
  // Do something...
});

// Bootstrap 5 - same event names, different syntax
const myModalEl = document.getElementById('myModal');
myModalEl.addEventListener('show.bs.modal', event => {
  // Do something...
});
```

**Important notes:**
- Keep jQuery for Drupal core compatibility
- Use vanilla JS for new Bootstrap-specific code
- Test all interactive components thoroughly
- Watch for jQuery vs vanilla JS context issues

### 6. Update Libraries Configuration (Sprint 3, Week 1)

**openy_carnation.libraries.yml:**

**Before (Bootstrap 4):**
```yaml
global-styling:
  version: 1.11
  css:
    base:
      //cdnjs.cloudflare.com/ajax/libs/font-awesome/5.14.0/css/all.css: {type: external}
      dist/css/style.css: {}
  js:
    dist/main.js: {}
    dist/bootstrap.bundle.min.js: {}  # Bootstrap 4 bundle
    dist/js/openy_carnation.js: {}
    dist/js/openy_carnation_mobile.js: {}
  dependencies:
    - core/jquery
    - core/jquery.ui.datepicker
    - core/once
    - core/drupal
```

**After (Bootstrap 5):**
```yaml
global-styling:
  version: 2.0  # Increment major version for Bootstrap 5
  css:
    base:
      //cdnjs.cloudflare.com/ajax/libs/font-awesome/5.14.0/css/all.css: {type: external}
      dist/css/style.css: {}
  js:
    dist/main.js: {}
    dist/bootstrap.bundle.min.js: {}  # Bootstrap 5 bundle (includes @popperjs/core)
    dist/js/openy_carnation.js: {}
    dist/js/openy_carnation_mobile.js: {}
  dependencies:
    - core/jquery      # Keep for Drupal compatibility
    - core/jquery.ui.datepicker
    - core/once
    - core/drupal
```

**Key changes:**
- Increment version to 2.0 (major change)
- Bootstrap bundle now includes @popperjs/core (no separate popper.js)
- Keep jQuery dependency for Drupal core
- No other library changes needed

### 7. Build and Test (Sprint 3, Weeks 1-2)

**Build process:**
```bash
cd docroot/themes/contrib/openy_carnation

# Clean old build
rm -rf dist/

# Run production build
npm run build

# Check for errors
# Should see Bootstrap 5 in build output
```

**Clear Drupal cache:**
```bash
# Using Docksal
fin drush cr

# Using Drush directly
vendor/bin/drush cr
```

**Test checklist:**

See detailed testing checklist in "Testing Requirements" section below.

---

## Files to Migrate

### Critical Files (Must update)
- [ ] `package.json` - Dependencies
- [ ] `webpack.build.js` - Build configuration
- [ ] `webpack.dev.js` - Dev configuration
- [ ] `src/scss/style.scss` - Main SCSS entry
- [ ] `src/scss/_init.scss` - Bootstrap variable overrides
- [ ] `src/scss/_variables.scss` - Theme variables
- [ ] `src/scss/_overrides.scss` - Component overrides
- [ ] `dist/js/openy_carnation.js` - Main JavaScript
- [ ] `dist/js/openy_carnation_mobile.js` - Mobile JavaScript
- [ ] `openy_carnation.libraries.yml` - Asset libraries

### High Priority Files (~30 files)
- [ ] All files in `src/scss/component/` (~25 files)
- [ ] All files in `src/scss/modules/` (~20 files)
- [ ] `templates/menu/menu--main--primary-menu.html.twig`
- [ ] `templates/menu/mobile/menu--main--mobile-menu.html.twig`
- [ ] `templates/form/form-element.html.twig`
- [ ] `templates/page/page.html.twig`
- [ ] All files in `templates/node/alert/`

### Medium Priority Files (~40 files)
- [ ] All files in `src/scss/paragraphs/` (~10 files)
- [ ] All files in `templates/node/` (various content types)
- [ ] All files in `templates/block/`
- [ ] Custom module templates in `templates/openy_*/`

### Lower Priority Files
- [ ] Documentation files (README.md)
- [ ] Configuration files (.editorconfig, etc.)

**Total files to review/update: ~100 files**

---

## Build Process

### Current Build Process (Bootstrap 4)
```bash
npm run build      # Webpack 4 production build
npm run dev        # Webpack 4 development build with watch
```

### Updated Build Process (Bootstrap 5)
```bash
npm run build      # Webpack 5 production build
npm run dev        # Webpack 5 development build with watch
```

**Build outputs:**
```
dist/
├── css/
│   └── style.css              # Compiled Bootstrap 5 + theme styles
├── js/
│   ├── openy_carnation.js     # Main theme JavaScript
│   └── openy_carnation_mobile.js  # Mobile JavaScript
├── bootstrap.bundle.min.js    # Bootstrap 5 bundle (includes Popper)
└── main.js                    # Webpack entry
```

**Build time:**
- Expected: 30-60 seconds (production)
- Watch mode: 5-10 seconds per change

---

## Testing Checklist

### Automated Tests
- [ ] Build completes without errors
- [ ] No SCSS compilation warnings
- [ ] No JavaScript console errors
- [ ] BackstopJS visual regression tests passed
- [ ] Pa11y accessibility tests passed

### Manual Testing - Pages
- [ ] Homepage
- [ ] Branch listing page
- [ ] Branch detail page
- [ ] Program listing page
- [ ] Program detail page
- [ ] Class listing page
- [ ] Class detail page
- [ ] Event listing page
- [ ] Event detail page
- [ ] News/Blog listing page
- [ ] News/Blog detail page
- [ ] Landing page (with Layout Builder)
- [ ] Search results page

### Manual Testing - Components
- [ ] **Navigation (Desktop)**
  - [ ] Main menu dropdowns work
  - [ ] Dropdown keyboard navigation (Tab, Enter, Esc)
  - [ ] Dropdown hover behavior
  - [ ] Active states
  - [ ] Submenu positioning

- [ ] **Navigation (Mobile)**
  - [ ] Hamburger menu opens/closes
  - [ ] Mobile menu slides in/out
  - [ ] Mobile submenu expand/collapse
  - [ ] Tap/touch responsiveness
  - [ ] Off-canvas overlay

- [ ] **Alerts**
  - [ ] Alert displays correctly
  - [ ] Alert colors (success, info, warning, danger)
  - [ ] Close button works (`.btn-close`)
  - [ ] Alert dismissal animation
  - [ ] Alert auto-dismiss (if configured)

- [ ] **Modals**
  - [ ] Modal opens via button click
  - [ ] Modal opens via JavaScript
  - [ ] Modal closes via close button
  - [ ] Modal closes via ESC key
  - [ ] Modal closes via backdrop click
  - [ ] Focus trap works (Tab cycles within modal)
  - [ ] Background scroll disabled
  - [ ] Modal transitions smooth

- [ ] **Forms**
  - [ ] Text inputs styled correctly
  - [ ] Select dropdowns styled (`.form-select`)
  - [ ] Checkboxes styled
  - [ ] Radio buttons styled
  - [ ] File inputs styled
  - [ ] Input groups work (no prepend/append wrappers)
  - [ ] Form validation states (valid/invalid)
  - [ ] Required field indicators
  - [ ] Help text positioning
  - [ ] Button styling (primary, secondary, etc.)
  - [ ] Full-width buttons (`.d-grid` wrapper)

- [ ] **Buttons**
  - [ ] Button variants (primary, secondary, success, danger, etc.)
  - [ ] Button sizes (sm, default, lg)
  - [ ] Button states (hover, active, disabled)
  - [ ] Button groups
  - [ ] Split button dropdowns

- [ ] **Cards**
  - [ ] Card layouts
  - [ ] Card headers/footers
  - [ ] Card images
  - [ ] Card grids (no more `.card-deck`)

- [ ] **Typography**
  - [ ] Headings (h1-h6)
  - [ ] Body text
  - [ ] Text alignment (`.text-start`, `.text-end`)
  - [ ] Text utilities (`.text-muted`, `.text-primary`, etc.)
  - [ ] Links (underlined by default in BS5)
  - [ ] Font weights (`.fw-bold`, not `.font-weight-bold`)

- [ ] **Utilities**
  - [ ] Spacing utilities (`.ms-*`, `.me-*` instead of `.ml-*`, `.mr-*`)
  - [ ] Display utilities
  - [ ] Flexbox utilities
  - [ ] Grid utilities
  - [ ] Position utilities
  - [ ] Border utilities (`.border-start`, `.border-end`)

### Responsive Testing
Test at all Bootstrap 5 breakpoints:
- [ ] **sm (576px)** - Mobile portrait
- [ ] **md (768px)** - Tablet portrait
- [ ] **lg (992px)** - Tablet landscape / small desktop
- [ ] **xl (1200px)** - Desktop
- [ ] **xxl (1400px)** - Large desktop (NEW in Bootstrap 5)

**Responsive checks:**
- [ ] Mobile menu at sm/md
- [ ] Desktop menu at lg/xl/xxl
- [ ] Grid columns collapse correctly
- [ ] Images scale properly
- [ ] Typography scales appropriately
- [ ] Touch targets adequate on mobile (44x44px minimum)

### Browser Testing
- [ ] **Chrome** (latest stable)
- [ ] **Firefox** (latest stable)
- [ ] **Safari** (latest stable)
- [ ] **Edge** (latest stable)
- [ ] **Mobile Safari** (iOS 15+)
- [ ] **Mobile Chrome** (Android 10+)

### Accessibility Testing
- [ ] **Color contrast** ≥ 4.5:1 (normal text), ≥ 3:1 (large text, UI)
- [ ] **Keyboard navigation** works throughout
- [ ] **Focus indicators** visible on all interactive elements
- [ ] **Skip links** present and functional
- [ ] **ARIA labels** present where needed
- [ ] **Form labels** properly associated
- [ ] **Alt text** present on images
- [ ] **Heading hierarchy** logical (h1 → h2 → h3)
- [ ] **Screen reader testing** (NVDA, JAWS, or VoiceOver)

### Performance Testing
- [ ] **Lighthouse audit** (target 90+ in all categories)
  - [ ] Performance: 90+
  - [ ] Accessibility: 95+
  - [ ] Best Practices: 90+
  - [ ] SEO: 90+
- [ ] **Bundle size** reduced (Bootstrap 5 is ~15-20% smaller)
- [ ] **Page load time** maintained or improved
- [ ] **Time to Interactive (TTI)** < 3.8s
- [ ] **Largest Contentful Paint (LCP)** < 2.5s
- [ ] **Cumulative Layout Shift (CLS)** < 0.1

---

## Testing Requirements

### Phase 1: Basic Testing (Sprint 2)
During development, run basic tests after each major change:
- Manual visual inspection
- Browser console check (no errors)
- Quick responsive check (mobile/desktop)

### Phase 2: Standard Testing (Sprint 3)
Before completing the sprint:
- Full manual testing checklist (above)
- BackstopJS visual regression
- Pa11y accessibility tests
- Cross-browser testing (Chrome, Firefox, Safari, Edge)
- Mobile testing (iOS, Android)

### Phase 3: Integration Testing (Sprint 7)
After all WS modules migrated:
- Theme + WS modules together
- All content types with theme
- All paragraph types with theme
- Complex page layouts

---

## Special Considerations

### 1. Activity Finder Coordination
The theme migration MUST coordinate with Activity Finder isolation (Sprint 3).

**Approach:**
- Theme uses Bootstrap 5 globally
- Activity Finder uses scoped Bootstrap 4 CSS (temporary)
- Test pages with both theme (BS5) and Activity Finder (BS4)
- Ensure no CSS conflicts

**See:** `modules/MODULES_ACTIVITY_FINDER.md` for Activity Finder isolation details.

### 2. jQuery Retention
**Keep jQuery** for Drupal core compatibility:
- Drupal 11 still ships with jQuery
- Many Drupal core systems rely on jQuery
- Other contrib modules may require jQuery
- Only Bootstrap-specific code should move to vanilla JS

**Do NOT remove jQuery from:**
- `package.json` dependencies
- `openy_carnation.libraries.yml` dependencies

### 3. Date Picker (Addressed Later)
The theme includes some date picker usage via Drupal core's jQuery UI Datepicker.

**Action:** No changes needed in theme migration. Date picker replacement happens in Phase 3 (Sprint 13) as part of Layout Builder modules.

### 4. Font Awesome
Font Awesome is loaded via CDN and doesn't depend on Bootstrap version.

**Action:** No changes needed. Keep as-is.

### 5. Custom Drupal JavaScript
Some JavaScript may use Drupal behaviors and jQuery:
```javascript
(function ($, Drupal) {
  Drupal.behaviors.myBehavior = {
    attach: function (context, settings) {
      // jQuery code here
    }
  };
})(jQuery, Drupal);
```

**Action:** Keep Drupal behaviors as-is. Only update Bootstrap-specific code.

### 6. Backwards Compatibility
Once theme is migrated to Bootstrap 5:
- No backwards compatibility with Bootstrap 4 modules
- All other modules MUST be migrated to Bootstrap 5
- Cannot mix Bootstrap 4 and 5 (except Activity Finder isolation)

**This is why theme migration is Phase 1 - everything depends on it.**

---

## Dependencies

### Before Theme Migration Can Start:
- [x] Phase 1 Sprint 1 complete (infrastructure, testing setup)
- [x] lb_accordion studied (reference implementation)
- [x] Decision made on Activity Finder approach
- [x] Testing tools installed (BackstopJS, Pa11y)
- [x] Baseline screenshots captured

### Before Other Phases Can Start:
- [ ] Theme migration complete (Sprints 2-3)
- [ ] Theme builds without errors
- [ ] Theme tested on all major pages
- [ ] Activity Finder isolated on Bootstrap 4
- [ ] No critical bugs in theme

---

## Sprint Assignments

### Sprint 2: Theme Migration Part 1
**Focus:** Dependencies, build system, core SCSS files

**Tasks:**
1. Update package.json dependencies
2. Update webpack configuration
3. Update core SCSS files (_init.scss, _variables.scss, style.scss, _overrides.scss)
4. Update component SCSS files (component/*.scss)
5. Initial build and test

**Deliverable:** Theme compiles successfully with Bootstrap 5

### Sprint 3: Theme Migration Part 2 + Activity Finder Isolation
**Focus:** Templates, JavaScript, Activity Finder isolation, testing

**Tasks:**
1. Update all component SCSS files (modules/*.scss, paragraphs/*.scss)
2. Update Twig templates (data-bs-* attributes, class changes)
3. Update JavaScript (Bootstrap 5 vanilla JS API)
4. Update libraries.yml
5. Activity Finder isolation (scoped Bootstrap 4 CSS)
6. Build and comprehensive testing
7. Documentation

**Deliverable:** Theme fully migrated, Activity Finder isolated, all tests passing

---

## Success Criteria

### Technical
- [ ] Theme builds without errors (Webpack 5)
- [ ] Bootstrap 5.3.3 loaded correctly
- [ ] @popperjs/core 2.11.8 loaded correctly
- [ ] All SCSS files compile successfully
- [ ] All templates use Bootstrap 5 syntax (data-bs-*)
- [ ] All JavaScript uses Bootstrap 5 API
- [ ] No JavaScript console errors
- [ ] Libraries.yml updated and versioned

### Quality
- [ ] Visual appearance matches Bootstrap 4 version (or approved differences)
- [ ] All interactive components functional (modals, dropdowns, etc.)
- [ ] Responsive at all breakpoints (sm, md, lg, xl, xxl)
- [ ] Cross-browser compatible (Chrome, Firefox, Safari, Edge)
- [ ] Mobile responsive (iOS, Android)
- [ ] WCAG 2.2 AA compliant
- [ ] Performance maintained or improved (Lighthouse 90+)

### Process
- [ ] BackstopJS visual regression tests passed
- [ ] Pa11y accessibility tests passed
- [ ] Manual testing checklist complete
- [ ] Migration log updated
- [ ] Documentation updated
- [ ] Known issues documented

### Integration
- [ ] Activity Finder isolated on Bootstrap 4
- [ ] No conflicts between theme (BS5) and Activity Finder (BS4)
- [ ] Ready for Phase 2 (WS modules migration)

---

## Risk Assessment

### Risk 1: Visual Regressions (HIGH)
**Impact:** HIGH - Poor user experience
**Probability:** HIGH - Many class changes

**Mitigation:**
- Comprehensive visual regression testing (BackstopJS)
- Manual testing of all major pages
- Cross-browser testing
- Responsive testing at all breakpoints
- Address issues before moving to Phase 2

### Risk 2: JavaScript Breakage (MEDIUM)
**Impact:** HIGH - Interactive features broken
**Probability:** MEDIUM - API changes significant

**Mitigation:**
- Study Bootstrap 5 JavaScript API changes
- Test all interactive components thoroughly
- Keep jQuery for Drupal compatibility
- Use vanilla JS for Bootstrap-specific code
- Test event listeners carefully

### Risk 3: Build System Issues (MEDIUM)
**Impact:** MEDIUM - Development workflow disrupted
**Probability:** LOW - Webpack 5 well-documented

**Mitigation:**
- Follow lb_accordion webpack config pattern
- Test build process early
- Document any issues
- Have rollback plan ready

### Risk 4: Activity Finder Conflicts (MEDIUM)
**Impact:** CRITICAL - Activity Finder breaks
**Probability:** MEDIUM - CSS scoping can leak

**Mitigation:**
- Isolate Activity Finder with scoped CSS
- Test Activity Finder extensively
- Test pages with both theme and Activity Finder
- Monitor for CSS specificity conflicts
- Have rollback plan ready

### Risk 5: Timeline Slippage (MEDIUM)
**Impact:** MEDIUM - Delays other phases
**Probability:** MEDIUM - Large scope, many files

**Mitigation:**
- Prioritize critical files
- Batch similar changes
- Use automated tools where possible
- Buffer time in Sprint 3
- Regular progress check-ins

---

## Related Documents

- [../EXECUTIVE_SUMMARY.md](../EXECUTIVE_SUMMARY.md) - Project overview
- [../MODULE_INVENTORY.md](../MODULE_INVENTORY.md) - All modules inventory
- [../phases/PHASE_1_PREPARATION.md](../phases/PHASE_1_PREPARATION.md) - Phase 1 details
- [../sprints/SPRINT_02_Theme_Part1.md](../sprints/SPRINT_02_Theme_Part1.md) - Sprint 2 details
- [../sprints/SPRINT_03_Theme_Part2_AF_Isolation.md](../sprints/SPRINT_03_Theme_Part2_AF_Isolation.md) - Sprint 3 details
- [MODULES_ACTIVITY_FINDER.md](MODULES_ACTIVITY_FINDER.md) - Activity Finder isolation
- [Bootstrap 5 Migration Guide](https://getbootstrap.com/docs/5.3/migration/)

---

**Module Status:** ⬜ Not Started
**Last Updated:** 2025-10-17
