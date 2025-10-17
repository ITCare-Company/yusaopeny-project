# Bootstrap 5 Migration - Quick Start Guide

**For Developers Starting Migration Work**
**Last Updated:** 2025-10-17

---

## Prerequisites

Before starting, ensure you have:
- [ ] Node.js 16+ installed
- [ ] npm or yarn
- [ ] Git
- [ ] Docksal (or DDEV) environment set up
- [ ] Access to codebase repository
- [ ] Familiarity with Bootstrap 4 and 5
- [ ] Basic knowledge of SCSS, Webpack, Drupal theming

---

## Quick Reference

### Key Documents
- [EXECUTIVE_SUMMARY.md](EXECUTIVE_SUMMARY.md) - Project overview
- [MODULE_INVENTORY.md](MODULE_INVENTORY.md) - All 66+ modules
- [REORGANIZATION_PLAN.md](REORGANIZATION_PLAN.md) - Documentation structure

### Reference Implementation
**lb_accordion** - Already migrated to Bootstrap 5.3.3
- Path: `docroot/modules/contrib/lb_accordion`
- Use as template for all other modules

---

## Step-by-Step: Migrating a Module

### Step 1: Study the Reference (5 minutes)

```bash
cd docroot/modules/contrib/lb_accordion

# Review key files:
cat package.json          # Bootstrap 5.3.3, @popperjs/core 2.11.8
cat webpack.config.js     # Webpack 5 configuration
ls assets/scss/           # SCSS structure
ls assets/js/             # JavaScript structure
ls templates/             # Twig templates
```

**Key Observations:**
- Bootstrap 5.3.3 in package.json
- Webpack 5 with modern loaders
- SCSS imports specific Bootstrap components (not full framework)
- Templates use `data-bs-*` attributes
- JavaScript imports Bootstrap components directly

---

### Step 2: Update package.json (2 minutes)

```bash
cd docroot/modules/contrib/[YOUR_MODULE]

# Update dependencies
npm install bootstrap@^5.3.3 @popperjs/core@^2.11.8 --save

# Update dev dependencies (if needed)
npm install webpack@^5.91.0 webpack-cli@^5.1.4 --save-dev
npm install sass@^1.75.0 sass-loader@^14.2.0 --save-dev
npm install css-loader@^7.1.1 mini-css-extract-plugin@^2.8.1 --save-dev

# Remove old dependencies
npm uninstall popper.js

# Install
npm install
```

**package.json changes:**
```json
{
  "dependencies": {
    "bootstrap": "^5.3.3",     // was ^4.4.1
    "@popperjs/core": "^2.11.8" // was popper.js ^1.16.0
  }
}
```

---

### Step 3: Update webpack.config.js (5 minutes)

Copy pattern from `lb_accordion/webpack.config.js`:

```javascript
const path = require('path');
const MiniCssExtractPlugin = require('mini-css-extract-plugin');

module.exports = {
  mode: 'production',
  entry: './assets/scss/[your-module].scss',
  output: {
    path: path.resolve(__dirname, 'dist'),
    filename: 'bundle.js'
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
      filename: 'style.css'
    })
  ]
};
```

---

### Step 4: Update SCSS Files (10-20 minutes)

#### 4a. Update Bootstrap Imports

**Before (Bootstrap 4):**
```scss
@import "bootstrap";  // Imports entire Bootstrap 4
```

**After (Bootstrap 5 - Selective Imports):**
```scss
// Import only what you need
@import "bootstrap/scss/functions";
@import "bootstrap/scss/variables";
@import "bootstrap/scss/variables-dark";
@import "bootstrap/scss/maps";
@import "bootstrap/scss/mixins";
@import "bootstrap/scss/utilities";

// Import specific components
@import "bootstrap/scss/buttons";
@import "bootstrap/scss/cards";
@import "bootstrap/scss/modal";
// ... etc

@import "bootstrap/scss/utilities/api";
```

#### 4b. Update Deprecated Classes

**Common replacements:**
```scss
// Spacing direction (LTR to logical)
.ml-3 → .ms-3  // margin-left → margin-start
.mr-3 → .me-3  // margin-right → margin-end
.pl-3 → .ps-3  // padding-left → padding-start
.pr-3 → .pe-3  // padding-right → padding-end

// Text alignment
.text-left → .text-start
.text-right → .text-end

// Other common changes
.close → .btn-close
.media → (use flexbox utilities)
.form-group → .mb-3 (or other margin utility)
.custom-select → .form-select
```

**Automated find/replace (use with caution):**
```bash
# In your SCSS directory
find . -name "*.scss" -exec sed -i.bak \
  -e 's/\.ml-/\.ms-/g' \
  -e 's/\.mr-/\.me-/g' \
  -e 's/\.text-left/\.text-start/g' \
  -e 's/\.text-right/\.text-end/g' \
  {} +
```

#### 4c. Update Bootstrap Mixins (if used)

Bootstrap 5 mixins are mostly the same, but check documentation for changes.

---

### Step 5: Update Twig Templates (10-15 minutes)

#### 5a. Update Data Attributes (Bootstrap JavaScript)

**Automated replacement:**
```bash
cd templates/

# Update data attributes
find . -name "*.twig" -exec sed -i.bak \
  -e 's/data-toggle="/data-bs-toggle="/g' \
  -e 's/data-target="/data-bs-target="/g' \
  -e 's/data-dismiss="/data-bs-dismiss="/g' \
  -e 's/data-slide="/data-bs-slide="/g' \
  -e 's/data-parent="/data-bs-parent="/g' \
  {} +

# Review changes
git diff templates/
```

#### 5b. Update Class Names (Manual Review Required)

**Examples:**

**Before (Bootstrap 4):**
```twig
<button type="button" class="btn btn-primary btn-block">
  Full Width Button
</button>

<button type="button" class="close" data-dismiss="alert">
  <span aria-hidden="true">&times;</span>
</button>

<div class="form-group">
  <label>Email</label>
  <input type="email" class="form-control">
</div>
```

**After (Bootstrap 5):**
```twig
<div class="d-grid gap-2">
  <button type="button" class="btn btn-primary">
    Full Width Button
  </button>
</div>

<button type="button" class="btn-close" data-bs-dismiss="alert" aria-label="Close"></button>

<div class="mb-3">
  <label class="form-label">Email</label>
  <input type="email" class="form-control">
</div>
```

---

### Step 6: Update JavaScript (if applicable, 5-10 minutes)

#### 6a. Update Bootstrap Imports

**Before (Bootstrap 4 - jQuery):**
```javascript
$('.modal').modal('show');
$('.dropdown').dropdown();
```

**After (Bootstrap 5 - Vanilla JS):**
```javascript
import { Modal, Dropdown } from 'bootstrap';

// Initialize modal
const modalEl = document.getElementById('myModal');
const modal = new Modal(modalEl);
modal.show();

// Initialize dropdown
const dropdownEl = document.querySelector('[data-bs-toggle="dropdown"]');
const dropdown = new Dropdown(dropdownEl);
```

#### 6b. Common JavaScript Migrations

**Modals:**
```javascript
// Bootstrap 4
$('#myModal').modal('show');

// Bootstrap 5
const modal = new bootstrap.Modal(document.getElementById('myModal'));
modal.show();
```

**Tooltips:**
```javascript
// Bootstrap 4
$('[data-toggle="tooltip"]').tooltip();

// Bootstrap 5
const tooltipTriggerList = document.querySelectorAll('[data-bs-toggle="tooltip"]');
const tooltipList = [...tooltipTriggerList].map(el => new bootstrap.Tooltip(el));
```

---

### Step 7: Update .libraries.yml (2 minutes)

```yaml
# [module_name].libraries.yml

[module_name]:
  version: 1.x  # Increment version
  css:
    theme:
      dist/style.css: { minified: true }
  js:
    dist/bundle.js: { minified: true }
  dependencies:
    - core/jquery  # Keep for Drupal compatibility
    - core/drupal
```

---

### Step 8: Build and Test (10-15 minutes)

```bash
# Build the module
npm run build

# Check build output
ls dist/

# Clear Drupal cache
fin drush cr  # or drush cr

# Test in browser
# - Visual appearance
# - Interactive components (modals, dropdowns, etc.)
# - Responsive behavior (all breakpoints: sm, md, lg, xl, xxl)
# - Accessibility (keyboard navigation)
```

### Testing Checklist
- [ ] Module builds without errors
- [ ] Visual appearance matches Bootstrap 4 version
- [ ] Interactive components work (if applicable)
- [ ] Responsive at all breakpoints (sm, md, lg, xl, xxl)
- [ ] No console errors
- [ ] Accessibility maintained (keyboard navigation, screen reader)

---

### Step 9: Document Changes (5 minutes)

Update module's README.md:
```markdown
## Bootstrap Version
- **Current:** Bootstrap 5.3.3
- **Migrated:** 2025-10-XX
- **Reference:** lb_accordion module

## Building
\`\`\`bash
npm install
npm run build
\`\`\`

## Breaking Changes from Bootstrap 4
- Updated data attributes to data-bs-*
- Replaced deprecated classes (btn-block, form-group, etc.)
- Updated JavaScript to Bootstrap 5 vanilla JS API

## Testing
- [ ] Visual regression tested
- [ ] Accessibility tested (WCAG 2.2 AA)
- [ ] Interactive features verified
```

---

## Common Issues and Solutions

### Issue 1: Build Fails with "Cannot find module 'bootstrap'"
**Solution:** Run `npm install` to install dependencies

### Issue 2: Styles Not Applied
**Solution:** Check that dist/style.css is generated and .libraries.yml references it correctly

### Issue 3: JavaScript Components Not Working
**Solution:**
- Verify data-bs-* attributes (not data-*)
- Check console for errors
- Ensure Bootstrap JS is loaded

### Issue 4: Modal/Dropdown Doesn't Open
**Solution:**
- Bootstrap 5 requires @popperjs/core for positioning
- Verify @popperjs/core is installed
- Check JavaScript initialization

### Issue 5: Grid Layout Broken
**Solution:**
- Bootstrap 5 gutter changes: 30px → 1.5rem (~24px)
- Check for `.no-gutters` (now `.g-0`)
- Review custom grid overrides

---

## Quick Reference: Breaking Changes

| Bootstrap 4 | Bootstrap 5 | Notes |
|-------------|-------------|-------|
| `data-toggle` | `data-bs-toggle` | All data attributes |
| `.btn-block` | `.d-grid` wrapper | Structural change |
| `.form-group` | `.mb-3` | Use margin utility |
| `.custom-select` | `.form-select` | Renamed |
| `.close` | `.btn-close` | Renamed |
| `.ml-*` | `.ms-*` | Logical property |
| `.mr-*` | `.me-*` | Logical property |
| `.text-left` | `.text-start` | Logical property |
| `.text-right` | `.text-end` | Logical property |
| `.media` | Removed | Use flexbox |
| `.jumbotron` | Removed | Custom styles |

---

## Resources

### Official Documentation
- [Bootstrap 5 Migration Guide](https://getbootstrap.com/docs/5.3/migration/)
- [Bootstrap 5 Documentation](https://getbootstrap.com/docs/5.3/)

### Project Documentation
- [EXECUTIVE_SUMMARY.md](EXECUTIVE_SUMMARY.md)
- [MODULE_INVENTORY.md](MODULE_INVENTORY.md)
- [phases/](phases/) - Phase documents
- [sprints/](sprints/) - Sprint documents

### Reference Implementation
- `docroot/modules/contrib/lb_accordion` - Complete example

---

## Need Help?

- Check [TROUBLESHOOTING.md](reference/TROUBLESHOOTING.md)
- Review [BREAKING_CHANGES.md](BREAKING_CHANGES.md)
- Ask in GitHub Discussions
- Refer to Bootstrap 5 official documentation

---

**Ready to Start?**

1. Pick a module from [MODULE_INVENTORY.md](MODULE_INVENTORY.md)
2. Follow steps 1-9 above
3. Test thoroughly
4. Document your work
5. Move to next module!

**Estimated Time Per Module:** 1-3 hours (depending on complexity)
