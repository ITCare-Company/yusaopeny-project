# Sprint 2: Theme Migration Part 1

**Phase:** [Phase 1 - Preparation](../phases/PHASE_1_PREPARATION.md)
**Resources:** 1 Developer
**Status:** Not Started

---

## Sprint Goal

Begin migration of openy_carnation theme to Bootstrap 5, focusing on dependency updates, core SCSS files, and build system configuration.

---

## Tasks

### Task 1: Update Theme Dependencies
**Owner:** Developer
**Priority:** CRITICAL

**Actions:**
```bash
cd docroot/themes/contrib/openy_carnation

# Update package.json
# - Bootstrap: 4.x → 5.3.3
# - Popper.js: Update to @popperjs/core
# - Review all other dependencies
```

**Update package.json:**
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
    "style-loader": "^3.3.3",
    "mini-css-extract-plugin": "^2.7.6",
    "autoprefixer": "^10.4.16",
    "postcss": "^8.4.32",
    "postcss-loader": "^7.3.3"
  }
}
```

**Acceptance Criteria:**
- [ ] package.json updated with Bootstrap 5.3.3
- [ ] All webpack dependencies updated to latest versions
- [ ] Popper.js replaced with @popperjs/core
- [ ] package-lock.json regenerated

---

### Task 2: Update Webpack Configuration
**Owner:** Developer
**Priority:** CRITICAL

**Actions:**
```bash
# Update webpack.config.js based on lb_accordion pattern
cd docroot/themes/contrib/openy_carnation
```

**Create/Update webpack.config.js:**
```javascript
const path = require('path');
const MiniCssExtractPlugin = require('mini-css-extract-plugin');

module.exports = {
  mode: 'production',
  entry: {
    'openy-carnation': './assets/js/index.js',
    'openy-carnation-styles': './assets/scss/openy-carnation.scss'
  },
  output: {
    path: path.resolve(__dirname, 'dist'),
    filename: 'js/[name].min.js',
    clean: true
  },
  module: {
    rules: [
      {
        test: /\.scss$/,
        use: [
          MiniCssExtractPlugin.loader,
          'css-loader',
          {
            loader: 'postcss-loader',
            options: {
              postcssOptions: {
                plugins: [
                  require('autoprefixer')
                ]
              }
            }
          },
          'sass-loader'
        ]
      }
    ]
  },
  plugins: [
    new MiniCssExtractPlugin({
      filename: 'css/[name].min.css'
    })
  ]
};
```

**Acceptance Criteria:**
- [ ] webpack.config.js created/updated
- [ ] Entry points defined for JS and SCSS
- [ ] Output paths configured correctly
- [ ] SCSS compilation pipeline configured
- [ ] Autoprefixer configured

---

### Task 3: Update Core SCSS - Variables
**Owner:** Developer
**Priority:** HIGH

**Actions:**
```bash
cd docroot/themes/contrib/openy_carnation/assets/scss
```

**Update SCSS Files:**

**1. Create/Update `_variables.scss`:**
- Update Bootstrap 4 variable names to Bootstrap 5 equivalents
- Reference: https://getbootstrap.com/docs/5.3/migration/#sass

**Key Changes:**
```scss
// Bootstrap 4 → Bootstrap 5 variable changes

// Colors (no change, but verify)
$primary: #0060af;
$secondary: #6c757d;

// Spacing (verify scale matches)
$spacer: 1rem;

// Grid (check gutter changes)
$grid-gutter-width: 1.5rem; // Was 30px in BS4

// Typography
// $font-size-base remains 1rem
// Verify font stack updates

// Border radius
// No major changes, verify values

// Shadows
// Verify box-shadow variables
```

**2. Review BS5 Deprecated Variables:**
- Remove any references to removed variables
- Document custom variables that override BS5 defaults

**Acceptance Criteria:**
- [ ] All Bootstrap 4 variables updated to Bootstrap 5 equivalents
- [ ] Custom theme variables documented
- [ ] No deprecated variables used
- [ ] Color system matches Bootstrap 5

---

### Task 4: Update Core SCSS - Imports
**Owner:** Developer
**Priority:** HIGH

**Actions:**
```bash
cd docroot/themes/contrib/openy_carnation/assets/scss
```

**Update `openy-carnation.scss` (main file):**

```scss
// 1. Include custom variables BEFORE Bootstrap
@import 'variables';

// 2. Import Bootstrap 5
@import '~bootstrap/scss/bootstrap';

// 3. Import theme components
@import 'components/header';
@import 'components/footer';
@import 'components/navigation';
@import 'components/buttons';
@import 'components/forms';
@import 'components/cards';
// ... other components

// 4. Import utilities and overrides
@import 'utilities';
@import 'overrides';
```

**Key Changes from Bootstrap 4:**
- No more `bootstrap/scss/functions` separate import (included in bootstrap)
- `bootstrap/scss/mixins` included in main bootstrap import
- Review if partial imports are needed (for optimization)

**Acceptance Criteria:**
- [ ] Main SCSS file updated with correct Bootstrap 5 import
- [ ] Custom variables imported before Bootstrap
- [ ] All component imports verified
- [ ] Import order correct

---

### Task 5: Update Core SCSS - Mixins and Utilities
**Owner:** Developer
**Priority:** HIGH

**Actions:**
```bash
cd docroot/themes/contrib/openy_carnation/assets/scss
```

**Update Mixin Usage:**

**Deprecated Mixins (Bootstrap 4 → 5):**
```scss
// Bootstrap 4
@include media-breakpoint-up(md) { }

// Bootstrap 5 (SAME - no change needed)
@include media-breakpoint-up(md) { }

// Bootstrap 4
@include make-col(6);

// Bootstrap 5 (SAME - no change needed)
@include make-col(6);

// Bootstrap 4 - DEPRECATED
@include hover { }
@include hover-focus { }

// Bootstrap 5 - Use pseudo-classes directly
&:hover { }
&:hover, &:focus { }
```

**Search and Replace:**
```bash
# Find all hover/hover-focus mixin usage
grep -r "@include hover" assets/scss/
grep -r "@include hover-focus" assets/scss/

# Replace with CSS pseudo-classes
```

**Acceptance Criteria:**
- [ ] All deprecated mixins identified
- [ ] hover and hover-focus mixins replaced
- [ ] Media query mixins verified (should work as-is)
- [ ] Grid mixins verified (should work as-is)

---

### Task 6: Update JavaScript - Bootstrap Imports
**Owner:** Developer
**Priority:** HIGH

**Actions:**
```bash
cd docroot/themes/contrib/openy_carnation/assets/js
```

**Create/Update `index.js`:**

```javascript
// Bootstrap 5 JavaScript imports

// Import Bootstrap components as needed
import { Dropdown } from 'bootstrap';
import { Modal } from 'bootstrap';
import { Collapse } from 'bootstrap';
import { Offcanvas } from 'bootstrap';
import { Tooltip } from 'bootstrap';
import { Popover } from 'bootstrap';

// Initialize tooltips
document.addEventListener('DOMContentLoaded', () => {
  // Initialize tooltips
  const tooltipTriggerList = document.querySelectorAll('[data-bs-toggle="tooltip"]');
  const tooltipList = [...tooltipTriggerList].map(tooltipTriggerEl => new Tooltip(tooltipTriggerEl));

  // Initialize popovers
  const popoverTriggerList = document.querySelectorAll('[data-bs-toggle="popover"]');
  const popoverList = [...popoverTriggerList].map(popoverTriggerEl => new Popover(popoverTriggerEl));
});

// Custom theme JavaScript
import './components/navigation.js';
import './components/search.js';
// ... other component JS
```

**Key Changes from Bootstrap 4:**
- Import individual components instead of full Bootstrap
- Use ES6 imports (not jQuery)
- Update data attributes: `data-toggle` → `data-bs-toggle`
- Update data attributes: `data-target` → `data-bs-target`

**Acceptance Criteria:**
- [ ] Bootstrap 5 components imported correctly
- [ ] Initialization code updated for Bootstrap 5 API
- [ ] jQuery dependencies removed (if possible)
- [ ] Custom JS imports organized

---

### Task 7: Update .libraries.yml
**Owner:** Developer
**Priority:** HIGH

**Actions:**
```bash
cd docroot/themes/contrib/openy_carnation
```

**Update `openy_carnation.libraries.yml`:**

```yaml
global-styling:
  version: VERSION
  css:
    theme:
      dist/css/openy-carnation-styles.min.css: { minified: true }
  js:
    dist/js/openy-carnation.min.js: { minified: true }
  dependencies:
    - core/drupal
    - core/drupalSettings

# Individual component libraries (if needed)
modal:
  version: VERSION
  js:
    dist/js/components/modal.min.js: { minified: true }
  dependencies:
    - openy_carnation/global-styling
```

**Key Changes:**
- Update paths to new `dist/` directory
- Remove references to Bootstrap 4 CDN (if any)
- Update jQuery dependencies (remove if possible)
- Ensure minified flags are correct

**Acceptance Criteria:**
- [ ] Library paths updated to dist/ directory
- [ ] CSS and JS files correctly referenced
- [ ] Dependencies correct
- [ ] No Bootstrap 4 CDN references

---

### Task 8: Initial Build and Test
**Owner:** Developer
**Priority:** CRITICAL

**Actions:**
```bash
cd docroot/themes/contrib/openy_carnation

# Install dependencies
npm install

# Build theme
npm run build

# Check output
ls -la dist/css/
ls -la dist/js/

# Test in browser
```

**Build Script (package.json):**
```json
{
  "scripts": {
    "build": "webpack --mode production",
    "dev": "webpack --mode development --watch",
    "clean": "rm -rf dist/"
  }
}
```

**Expected Build Output:**
```
dist/
├── css/
│   └── openy-carnation-styles.min.css
└── js/
    └── openy-carnation.min.js
```

**Testing:**
1. Clear Drupal cache: `fin drush cr`
2. Load homepage in browser
3. Check browser console for errors
4. Verify basic styles are applied
5. Test responsive breakpoints

**Acceptance Criteria:**
- [ ] npm install succeeds without errors
- [ ] npm run build completes successfully
- [ ] dist/ directory contains expected files
- [ ] CSS file size reasonable (< 500KB)
- [ ] JS file size reasonable (< 200KB)
- [ ] No build warnings (or documented if unavoidable)
- [ ] Theme loads in browser without console errors

---

### Task 9: Document Migration Progress
**Owner:** Developer
**Priority:** MEDIUM

**Actions:**
```bash
# Update migration log
cd docs/bootstrap-5-migration
```

**Update MIGRATION_LOG.md:**
- Document what was changed in theme
- Document any issues encountered
- Document any deviations from lb_accordion pattern
- Document build output file sizes

**Create THEME_MIGRATION_NOTES.md:**
- Bootstrap 4 → 5 variable changes specific to theme
- Custom SCSS that needed updates
- JavaScript changes required
- Known issues or incomplete work

**Acceptance Criteria:**
- [ ] MIGRATION_LOG.md updated with Sprint 2 progress
- [ ] THEME_MIGRATION_NOTES.md created
- [ ] All changes documented
- [ ] Known issues listed

---

## Testing

### Build Testing:
- [ ] `npm install` succeeds
- [ ] `npm run build` succeeds
- [ ] No build errors
- [ ] Output files exist in dist/

### Visual Testing:
- [ ] Homepage loads
- [ ] No console errors
- [ ] Basic layout intact
- [ ] Colors correct
- [ ] Fonts correct

### Manual Testing:
- [ ] Test on phone viewport (320px)
- [ ] Test on tablet viewport (768px)
- [ ] Test on desktop viewport (1280px)
- [ ] Navigation works
- [ ] Dropdowns work (if using Bootstrap dropdowns)

**Note:** Full visual regression testing will happen in Sprint 3 after template updates.

---

## Deliverables

### Must Have:
- [ ] openy_carnation package.json updated
- [ ] webpack.config.js created/updated
- [ ] Core SCSS files updated for Bootstrap 5
- [ ] JavaScript updated for Bootstrap 5 API
- [ ] Theme builds successfully
- [ ] Theme loads without errors

### Nice to Have:
- [ ] Build optimization (code splitting, etc.)
- [ ] Dev mode with watch enabled
- [ ] Source maps configured

---

## Decision Points

### Decision: Full or Partial Bootstrap Import
**Options:**
1. Import full Bootstrap (`@import 'bootstrap'`)
2. Import only needed components

**Recommendation:** Start with full import, optimize later in Phase 3

**Decision Required By:** Task 4
**Decision Maker:** Developer
**Documentation:** Add to THEME_MIGRATION_NOTES.md

---

## Risks

### Risk: Build Configuration Issues
**Likelihood:** Medium
**Impact:** High
**Mitigation:** Follow lb_accordion webpack.config.js closely, test incrementally

### Risk: SCSS Compilation Errors
**Likelihood:** Medium
**Impact:** Medium
**Mitigation:** Update one SCSS file at a time, test compilation after each change

### Risk: Unexpected Bootstrap 5 Breaking Changes
**Likelihood:** Low
**Impact:** High
**Mitigation:** Reference Bootstrap 5 migration guide, test each component

---

## Notes

### Important:
- This sprint focuses on infrastructure (build system + core SCSS)
- Component templates NOT updated yet (Sprint 3)
- Visual appearance may be broken - that's expected
- Goal is successful build, not pixel-perfect rendering

### Tips:
- Keep Bootstrap 4 theme in separate branch for reference
- Commit after each major task
- Test build after each SCSS file update
- Document all custom variables

### References:
- Bootstrap 5 Migration Guide: https://getbootstrap.com/docs/5.3/migration/
- Bootstrap 5 Sass Documentation: https://getbootstrap.com/docs/5.3/customize/sass/
- lb_accordion reference: `docroot/modules/contrib/lb_accordion/`

---

## Sprint Review Checklist

At end of sprint, verify:
- [ ] All tasks completed
- [ ] Theme builds successfully
- [ ] All deliverables created
- [ ] Documentation updated
- [ ] Next sprint ready to start
- [ ] Known issues documented

---

## Navigation

- **Previous:** [Sprint 1 - Infrastructure & Research](SPRINT_01_Infrastructure.md)
- **Next:** [Sprint 3 - Theme Part 2 + Activity Finder Isolation](SPRINT_03_Theme_Part2_AF_Isolation.md)
- **Phase:** [Phase 1 - Preparation](../phases/PHASE_1_PREPARATION.md)
- **Overview:** [Executive Summary](../EXECUTIVE_SUMMARY.md)

---

**Sprint Status:** ⬜ Not Started
**Last Updated:** 2025-10-17
