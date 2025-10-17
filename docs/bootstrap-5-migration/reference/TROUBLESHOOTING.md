# Bootstrap 5 Migration Troubleshooting Guide

Common issues encountered during Bootstrap 4 to Bootstrap 5 migration and their solutions.

## Table of Contents

1. [Build Errors](#build-errors)
2. [Runtime JavaScript Errors](#runtime-javascript-errors)
3. [Styling Issues](#styling-issues)
4. [Component Behavior Issues](#component-behavior-issues)
5. [Drupal Integration Issues](#drupal-integration-issues)
6. [Performance Issues](#performance-issues)
7. [Browser Compatibility Issues](#browser-compatibility-issues)
8. [Configuration Issues](#configuration-issues)

---

## Build Errors

### Error: Cannot find module 'bootstrap'

**Symptoms:**
```
Error: Cannot find module 'bootstrap'
```

**Cause:**
Bootstrap 5 is not installed in node_modules.

**Solution:**
```bash
npm install bootstrap@^5.3.3 @popperjs/core@^2.11.8
```

**Verify:**
```bash
npm list bootstrap
# Should show: bootstrap@5.3.3
```

---

### Error: Cannot find module 'bootstrap/scss/bootstrap'

**Symptoms:**
```
Module not found: Error: Can't resolve 'bootstrap/scss/bootstrap'
```

**Cause:**
Incorrect import path or Bootstrap not installed.

**Solution:**
Update your SCSS import:
```scss
// Instead of this:
@import "bootstrap/scss/bootstrap";

// Use modular imports:
@import "bootstrap/scss/functions";
@import "bootstrap/scss/variables";
@import "bootstrap/scss/variables-dark";
@import "bootstrap/scss/maps";
@import "bootstrap/scss/mixins";
@import "bootstrap/scss/accordion";
// ... other components
@import "bootstrap/scss/utilities/api";
```

---

### Error: SassError: Undefined variable

**Symptoms:**
```
SassError: Undefined variable: "$grid-breakpoints"
```

**Cause:**
Bootstrap SCSS files are imported in the wrong order.

**Solution:**
Always import in this order:
```scss
// 1. Functions first (required for everything)
@import "bootstrap/scss/functions";

// 2. Variable overrides (optional)
$primary: #ff5733;

// 3. Bootstrap variables
@import "bootstrap/scss/variables";
@import "bootstrap/scss/variables-dark";

// 4. Maps
@import "bootstrap/scss/maps";

// 5. Mixins
@import "bootstrap/scss/mixins";

// 6. Components
@import "bootstrap/scss/buttons";
// ... etc

// 7. Utilities (must be last)
@import "bootstrap/scss/utilities/api";
```

---

### Error: Module build failed: ModuleBuildError: Module not found: sass-loader

**Symptoms:**
```
Module build failed: ModuleBuildError
Module not found: Error: Can't resolve 'sass-loader'
```

**Cause:**
Missing webpack loaders.

**Solution:**
Install required loaders:
```bash
npm install --save-dev sass sass-loader css-loader style-loader mini-css-extract-plugin
```

Update webpack.config.js:
```javascript
module: {
  rules: [
    {
      test: /\.(scss)$/,
      use: [
        miniCssExtractPlugin.loader,
        'css-loader',
        'postcss-loader',
        'sass-loader'
      ]
    }
  ]
}
```

---

### Error: PurgeCSSPlugin is not a constructor

**Symptoms:**
```
TypeError: PurgeCSSPlugin is not a constructor
```

**Cause:**
Incorrect import syntax for PurgeCSS webpack plugin.

**Solution:**
```javascript
// Correct import:
const { PurgeCSSPlugin } = require("purgecss-webpack-plugin");

// NOT:
const PurgeCSSPlugin = require("purgecss-webpack-plugin");
```

---

### Error: postcss-loader: Error: No PostCSS Config found

**Symptoms:**
```
Error: No PostCSS Config found
```

**Cause:**
PostCSS configuration is not defined.

**Solution 1:** Add postcss config inline in webpack.config.js:
```javascript
{
  loader: 'postcss-loader',
  options: {
    postcssOptions: {
      plugins: [
        require('autoprefixer')
      ]
    }
  }
}
```

**Solution 2:** Create postcss.config.js:
```javascript
module.exports = {
  plugins: [
    require('autoprefixer')
  ]
}
```

---

### Error: PurgeCSS removes required styles

**Symptoms:**
Bootstrap styles are missing after build, or components look broken.

**Cause:**
PurgeCSS is too aggressive and removes styles that are actually used.

**Solution:**
Add safelist to PurgeCSS configuration:
```javascript
new PurgeCSSPlugin({
  paths: glob.sync(`${PATHS.src}/**/*`, { nodir: true }),
  safelist: {
    standard: ['show', 'collapsing', 'modal-backdrop', 'fade'],
    deep: [/^accordion/, /^collapse/, /^modal/, /^dropdown/],
    greedy: [/^btn-/, /^bg-/, /^text-/]
  }
})
```

Common classes to safelist:
- `show` - Used by collapsing/transitions
- `collapsing` - Used during collapse animation
- `fade` - Used for fade transitions
- `modal-backdrop` - Modal overlay
- `active` - Active states
- Dynamic classes added by JavaScript

---

### Error: Webpack build takes too long

**Symptoms:**
`npm run build` takes several minutes to complete.

**Cause:**
Webpack is watching or processing too many files.

**Solution:**
1. Add `.nvmrc` to use consistent Node version
2. Optimize webpack config:
```javascript
module.exports = {
  mode: 'production', // Use production mode
  optimization: {
    minimize: true
  },
  // Don't watch in production builds
  watch: false
}
```

3. Exclude node_modules from processing:
```javascript
module: {
  rules: [
    {
      test: /\.(scss)$/,
      exclude: /node_modules/,
      use: [...]
    }
  ]
}
```

---

## Runtime JavaScript Errors

### Error: bootstrap is not defined

**Symptoms:**
```
Uncaught ReferenceError: bootstrap is not defined
```

**Cause:**
Bootstrap JavaScript is not loaded or not exposed globally.

**Solution 1:** Import components explicitly:
```javascript
import Collapse from 'bootstrap/js/dist/collapse';

// Use directly
const collapse = new Collapse(element);
```

**Solution 2:** Expose bootstrap globally (if needed for Drupal):
```javascript
import * as bootstrap from 'bootstrap';
window.bootstrap = bootstrap;
```

---

### Error: $ is not defined (jQuery)

**Symptoms:**
```
Uncaught ReferenceError: $ is not defined
```

**Cause:**
jQuery is not loaded before your script.

**Solution:**
In Drupal, ensure jQuery dependency in .libraries.yml:
```yaml
module_name:
  js:
    assets/dist/module_name.js: { minified: true }
  dependencies:
    - core/jquery
    - core/drupal
```

In JavaScript, wrap in Drupal behavior:
```javascript
(function ($, Drupal) {
  'use strict';

  Drupal.behaviors.moduleName = {
    attach: function (context, settings) {
      // $ is available here
    }
  };
})(jQuery, Drupal);
```

---

### Error: Cannot read property 'Constructor' of undefined

**Symptoms:**
```
TypeError: Cannot read property 'Constructor' of undefined
```

**Cause:**
Trying to use Bootstrap component that isn't imported.

**Solution:**
Import the component:
```javascript
// Make sure to import the component
import Modal from 'bootstrap/js/dist/modal';

// Then use it
const modal = new Modal(document.getElementById('myModal'));
```

---

### Error: data-bs-toggle does nothing

**Symptoms:**
Clicking elements with `data-bs-toggle` doesn't trigger Bootstrap components.

**Cause:**
Bootstrap JavaScript isn't initialized for those elements.

**Solution 1:** Bootstrap 5 auto-initializes data-api elements. Ensure Bootstrap JS is loaded:
```javascript
// In your main JS file
import 'bootstrap';
```

**Solution 2:** Manual initialization:
```javascript
import Modal from 'bootstrap/js/dist/modal';

// Initialize all modals
const modals = document.querySelectorAll('[data-bs-toggle="modal"]');
modals.forEach(trigger => {
  new Modal(document.querySelector(trigger.dataset.bsTarget));
});
```

**Solution 3:** In Drupal with behaviors:
```javascript
(function ($, Drupal, bootstrap) {
  Drupal.behaviors.initBootstrap = {
    attach: function (context) {
      // Find and initialize modals
      $('[data-bs-toggle="modal"]', context).once('bs-modal').each(function() {
        const target = this.dataset.bsTarget;
        new bootstrap.Modal(document.querySelector(target));
      });
    }
  };
})(jQuery, Drupal, window.bootstrap);
```

---

### Error: Popper.js error

**Symptoms:**
```
Error: Popper: Invalid reference or popper element
```

**Cause:**
@popperjs/core is not installed or wrong version.

**Solution:**
```bash
npm install @popperjs/core@^2.11.8
```

Ensure Popper is loaded before Bootstrap dropdowns/tooltips/popovers:
```javascript
import '@popperjs/core';
import Dropdown from 'bootstrap/js/dist/dropdown';
```

---

### Error: TypeError: Converting circular structure to JSON

**Symptoms:**
Occurs when trying to log Bootstrap component instances.

**Cause:**
Bootstrap component instances contain circular references.

**Solution:**
Don't log the entire component instance:
```javascript
// Instead of:
console.log(collapse); // Error

// Do this:
console.log('Collapse initialized:', collapse._element);
```

---

## Styling Issues

### Issue: Forms look broken

**Symptoms:**
Form inputs have no spacing, labels overlap inputs.

**Cause:**
`.form-group` was removed in Bootstrap 5.

**Solution:**
Replace `.form-group` with margin utilities:
```html
<!-- Bootstrap 4 -->
<div class="form-group">
  <label>Email</label>
  <input class="form-control">
</div>

<!-- Bootstrap 5 -->
<div class="mb-3">
  <label class="form-label">Email</label>
  <input class="form-control">
</div>
```

---

### Issue: Buttons not full width

**Symptoms:**
Buttons are not stretching to full width.

**Cause:**
`.btn-block` was removed in Bootstrap 5.

**Solution:**
Use `.w-100` or `.d-grid`:
```html
<!-- Option 1: Width utility -->
<button class="btn btn-primary w-100">Full Width</button>

<!-- Option 2: Grid wrapper (recommended) -->
<div class="d-grid gap-2">
  <button class="btn btn-primary">Full Width</button>
  <button class="btn btn-secondary">Full Width</button>
</div>
```

---

### Issue: Text alignment is wrong

**Symptoms:**
Text that should be left/right aligned is centered or not aligned.

**Cause:**
`.text-left` and `.text-right` were renamed.

**Solution:**
```html
<!-- Bootstrap 4 -->
<div class="text-left">Left</div>
<div class="text-right">Right</div>

<!-- Bootstrap 5 -->
<div class="text-start">Left</div>
<div class="text-end">Right</div>
```

Use find/replace:
- Find: `text-left` → Replace: `text-start`
- Find: `text-right` → Replace: `text-end`

---

### Issue: Margin/padding utilities not working

**Symptoms:**
Left/right margins and paddings are not applied.

**Cause:**
Directional classes were renamed for RTL support.

**Solution:**
```html
<!-- Bootstrap 4 -->
<div class="ml-3 mr-2 pl-3 pr-2">Content</div>

<!-- Bootstrap 5 -->
<div class="ms-3 me-2 ps-3 pe-2">Content</div>
```

Mapping:
- `ml-*` → `ms-*` (margin-start)
- `mr-*` → `me-*` (margin-end)
- `pl-*` → `ps-*` (padding-start)
- `pr-*` → `pe-*` (padding-end)

---

### Issue: Custom checkbox/radio styles missing

**Symptoms:**
Checkboxes and radios look like default browser controls.

**Cause:**
Custom form control classes changed.

**Solution:**
```html
<!-- Bootstrap 4 -->
<div class="custom-control custom-checkbox">
  <input type="checkbox" class="custom-control-input" id="check1">
  <label class="custom-control-label" for="check1">Check me</label>
</div>

<!-- Bootstrap 5 -->
<div class="form-check">
  <input class="form-check-input" type="checkbox" id="check1">
  <label class="form-check-label" for="check1">Check me</label>
</div>
```

---

### Issue: Grid gutters not working

**Symptoms:**
`.no-gutters` class does nothing.

**Cause:**
Class was renamed to `.g-0`.

**Solution:**
```html
<!-- Bootstrap 4 -->
<div class="row no-gutters">
  <div class="col">Content</div>
</div>

<!-- Bootstrap 5 -->
<div class="row g-0">
  <div class="col">Content</div>
</div>
```

New gutter utilities:
- `.g-0` - No gutters
- `.g-1` through `.g-5` - Different gutter sizes
- `.gx-*` - Horizontal gutters only
- `.gy-*` - Vertical gutters only

---

### Issue: Input groups look broken

**Symptoms:**
Input group elements are misaligned or styled incorrectly.

**Cause:**
`.input-group-prepend` and `.input-group-append` were removed.

**Solution:**
```html
<!-- Bootstrap 4 -->
<div class="input-group">
  <div class="input-group-prepend">
    <span class="input-group-text">@</span>
  </div>
  <input type="text" class="form-control">
  <div class="input-group-append">
    <button class="btn btn-primary">Go</button>
  </div>
</div>

<!-- Bootstrap 5 - Remove wrapper divs -->
<div class="input-group">
  <span class="input-group-text">@</span>
  <input type="text" class="form-control">
  <button class="btn btn-primary">Go</button>
</div>
```

---

### Issue: Close button (X) missing or unstyled

**Symptoms:**
Close button in modals/alerts shows as text "×" or is invisible.

**Cause:**
`.close` class was renamed to `.btn-close`.

**Solution:**
```html
<!-- Bootstrap 4 -->
<button type="button" class="close" data-dismiss="modal">
  <span aria-hidden="true">&times;</span>
</button>

<!-- Bootstrap 5 -->
<button type="button" class="btn-close" data-bs-dismiss="modal"></button>
```

No need for the `&times;` span - it's built into the `.btn-close` class.

---

### Issue: Badge colors not working

**Symptoms:**
`.badge-primary`, `.badge-success` etc. are unstyled.

**Cause:**
Badge color classes changed.

**Solution:**
```html
<!-- Bootstrap 4 -->
<span class="badge badge-primary">Primary</span>
<span class="badge badge-success">Success</span>

<!-- Bootstrap 5 -->
<span class="badge bg-primary">Primary</span>
<span class="badge bg-success">Success</span>
```

Use `.bg-*` classes for badge colors.

---

### Issue: Accordion chevron not rotating

**Symptoms:**
Accordion chevron icon doesn't rotate when opened/closed.

**Cause:**
Custom CSS may be targeting wrong classes or selectors.

**Solution:**
Check your accordion button state:
```scss
.accordion-button {
  &[aria-expanded="true"] {
    .chevron {
      transform: rotate(180deg);
    }
  }
  &[aria-expanded="false"] {
    .chevron {
      transform: rotate(0deg);
    }
  }
}
```

Or use Bootstrap 5's default chevron and hide custom ones:
```scss
// Let Bootstrap handle the chevron
.accordion-button::after {
  // Bootstrap 5 default chevron
}
```

---

### Issue: Modal backdrop doesn't cover full screen

**Symptoms:**
Modal backdrop is positioned incorrectly or doesn't cover viewport.

**Cause:**
CSS conflicts or missing Bootstrap modal styles.

**Solution:**
1. Ensure modal HTML is correct:
```html
<div class="modal fade" id="myModal" tabindex="-1">
  <div class="modal-dialog">
    <div class="modal-content">
      <!-- content -->
    </div>
  </div>
</div>
```

2. Ensure Bootstrap modal CSS is imported:
```scss
@import "bootstrap/scss/modal";
```

3. Check for conflicting CSS:
```scss
// Remove if you have this
.modal-backdrop {
  // Don't override Bootstrap's styles
}
```

---

### Issue: PurgeCSS removed needed styles

**Symptoms:**
Styles work in development but break in production build.

**Cause:**
PurgeCSS removes classes that appear only in JavaScript or dynamic content.

**Solution:**
Add safelist to webpack.config.js:
```javascript
new PurgeCSSPlugin({
  paths: glob.sync(`${PATHS.src}/**/*`, { nodir: true }),
  safelist: {
    // Keep exact class names
    standard: ['show', 'collapsing', 'fade', 'active', 'disabled'],

    // Keep classes starting with...
    deep: [
      /^accordion/,
      /^collapse/,
      /^modal/,
      /^dropdown/,
      /^tooltip/,
      /^popover/
    ],

    // Keep classes containing pattern
    greedy: [
      /^btn-/,
      /^bg-/,
      /^text-/,
      /^border-/,
      /^rounded-/
    ]
  }
})
```

---

## Component Behavior Issues

### Issue: Accordion doesn't open/close

**Symptoms:**
Clicking accordion button does nothing.

**Cause:**
Missing data attributes or wrong selectors.

**Checklist:**
1. Check data attributes are correct:
```html
<button
  class="accordion-button"
  data-bs-toggle="collapse"
  data-bs-target="#collapse1"
  aria-expanded="false"
  aria-controls="collapse1">
  Accordion Item
</button>

<div
  id="collapse1"
  class="accordion-collapse collapse"
  data-bs-parent="#accordionExample">
  <div class="accordion-body">Content</div>
</div>
```

2. Check IDs match:
   - `data-bs-target="#collapse1"` must match `id="collapse1"`

3. Check parent reference:
   - `data-bs-parent="#accordionExample"` must match accordion container ID

4. Check Bootstrap JS is loaded:
```javascript
import Collapse from 'bootstrap/js/dist/collapse';
```

---

### Issue: Modal doesn't open

**Symptoms:**
Clicking modal trigger does nothing.

**Checklist:**
1. Check trigger button:
```html
<button
  type="button"
  class="btn btn-primary"
  data-bs-toggle="modal"
  data-bs-target="#myModal">
  Open Modal
</button>
```

2. Check modal markup:
```html
<div class="modal fade" id="myModal" tabindex="-1">
  <div class="modal-dialog">
    <div class="modal-content">
      <div class="modal-header">
        <h5 class="modal-title">Modal title</h5>
        <button type="button" class="btn-close" data-bs-dismiss="modal"></button>
      </div>
      <div class="modal-body">
        Content
      </div>
    </div>
  </div>
</div>
```

3. Check IDs match:
   - `data-bs-target="#myModal"` must match `id="myModal"`

4. Check Bootstrap Modal JS is loaded:
```javascript
import Modal from 'bootstrap/js/dist/modal';
```

5. Try manual initialization:
```javascript
const modal = new bootstrap.Modal(document.getElementById('myModal'));
modal.show();
```

---

### Issue: Dropdown doesn't open

**Symptoms:**
Clicking dropdown toggle does nothing.

**Checklist:**
1. Check Popper.js is loaded:
```bash
npm install @popperjs/core@^2.11.8
```

2. Check dropdown markup:
```html
<div class="dropdown">
  <button
    class="btn btn-secondary dropdown-toggle"
    type="button"
    data-bs-toggle="dropdown">
    Dropdown button
  </button>
  <ul class="dropdown-menu">
    <li><a class="dropdown-item" href="#">Action</a></li>
  </ul>
</div>
```

3. Import Popper before Dropdown:
```javascript
import '@popperjs/core';
import Dropdown from 'bootstrap/js/dist/dropdown';
```

---

### Issue: Tooltip doesn't show

**Symptoms:**
Hovering over elements with tooltip doesn't show tooltip.

**Cause:**
Tooltips require manual initialization in Bootstrap 5.

**Solution:**
```javascript
import Tooltip from 'bootstrap/js/dist/tooltip';

// Initialize all tooltips
const tooltips = document.querySelectorAll('[data-bs-toggle="tooltip"]');
[...tooltips].forEach(el => new Tooltip(el));
```

In Drupal:
```javascript
(function ($, Drupal, bootstrap) {
  Drupal.behaviors.initTooltips = {
    attach: function (context) {
      $('[data-bs-toggle="tooltip"]', context)
        .once('bs-tooltip')
        .each(function() {
          new bootstrap.Tooltip(this);
        });
    }
  };
})(jQuery, Drupal, window.bootstrap);
```

---

### Issue: Collapse animation is jerky

**Symptoms:**
Collapse/accordion animation stutters or jumps.

**Cause:**
Missing transitions import or height calculation issues.

**Solution:**
1. Import transitions:
```scss
@import "bootstrap/scss/transitions";
```

2. Avoid fixed heights in collapsible content:
```scss
// Avoid:
.accordion-body {
  height: 200px; // Don't do this
}

// Allow natural height:
.accordion-body {
  // Let content determine height
}
```

---

## Drupal Integration Issues

### Issue: Styles don't load in Layout Builder preview

**Symptoms:**
Components look unstyled in Layout Builder edit mode.

**Cause:**
Library not attached in preview mode.

**Solution:**
Ensure library is attached in template:
```twig
{{ attach_library('module_name/module_name') }}
```

Check that library is not conditional:
```php
// In .module file - check for this:
function module_name_page_attachments_alter(array &$page) {
  // Make sure library is attached everywhere
  $page['#attached']['library'][] = 'module_name/module_name';
}
```

---

### Issue: JavaScript doesn't work with AJAX

**Symptoms:**
Components work on initial page load but break after AJAX operations.

**Cause:**
Drupal behaviors not used correctly.

**Solution:**
Use Drupal behaviors with `.once()`:
```javascript
(function ($, Drupal, bootstrap) {
  'use strict';

  Drupal.behaviors.moduleName = {
    attach: function (context, settings) {
      // Use .once() to prevent double-initialization
      $('.accordion', context).once('moduleName').each(function() {
        // Initialize Bootstrap component
        new bootstrap.Collapse(this);
      });
    }
  };
})(jQuery, Drupal, window.bootstrap);
```

---

### Issue: Configuration not importing

**Symptoms:**
`drush cim` fails with errors about missing dependencies.

**Cause:**
Module dependencies or configuration mismatch.

**Solution:**
1. Check module dependencies in .info.yml:
```yaml
dependencies:
  - drupal:block_content
  - drupal:paragraphs
  - y_lb
```

2. Export config after changes:
```bash
drush cex -y
```

3. Check for UUID conflicts:
```bash
# Remove UUIDs if needed
sed -i '' '/^uuid:/d' config/sync/*.yml
```

---

### Issue: Cache not clearing

**Symptoms:**
Changes don't appear even after clearing cache.

**Cause:**
Multiple cache layers or library version not updated.

**Solution:**
1. Bump library version in .libraries.yml:
```yaml
module_name:
  version: 1.10  # Increment this
```

2. Clear all caches:
```bash
drush cr
```

3. Clear Drupal caches:
```bash
drush cc css-js
drush cc render
```

4. Check browser cache (hard refresh):
- Chrome: Ctrl+Shift+R (Windows) or Cmd+Shift+R (Mac)
- Firefox: Ctrl+Shift+R (Windows) or Cmd+Shift+R (Mac)

---

## Performance Issues

### Issue: Large CSS bundle size

**Symptoms:**
CSS file is several hundred KB or larger.

**Cause:**
Importing entire Bootstrap library.

**Solution:**
Use lean imports - import only what you need:
```scss
// Instead of:
@import "bootstrap/scss/bootstrap";

// Import only specific components:
@import "bootstrap/scss/functions";
@import "bootstrap/scss/variables";
@import "bootstrap/scss/variables-dark";
@import "bootstrap/scss/maps";
@import "bootstrap/scss/mixins";
@import "bootstrap/scss/accordion";  // Only if needed
@import "bootstrap/scss/buttons";   // Only if needed
@import "bootstrap/scss/utilities/api";
```

Use PurgeCSS to remove unused styles:
```javascript
// In webpack.config.js
const { PurgeCSSPlugin } = require("purgecss-webpack-plugin");

plugins: [
  new PurgeCSSPlugin({
    paths: glob.sync(`${PATHS.src}/**/*`, { nodir: true }),
  })
]
```

---

### Issue: Large JavaScript bundle size

**Symptoms:**
JS file is several hundred KB.

**Cause:**
Importing entire Bootstrap JS.

**Solution:**
Import only needed components:
```javascript
// Instead of:
import 'bootstrap';

// Import specific components:
import Collapse from 'bootstrap/js/dist/collapse';
import Modal from 'bootstrap/js/dist/modal';
// etc.
```

---

### Issue: Page load performance degraded

**Symptoms:**
Lighthouse performance score decreased after migration.

**Solution:**
1. Enable production build:
```javascript
// webpack.config.js
module.exports = {
  mode: 'production',
  optimization: {
    minimize: true
  }
}
```

2. Check bundle sizes:
```bash
npm run build
ls -lh assets/dist/
```

3. Consider code splitting (advanced):
```javascript
// Dynamic imports for large components
button.addEventListener('click', async () => {
  const Modal = await import('bootstrap/js/dist/modal');
  const modal = new Modal.default(element);
});
```

---

## Browser Compatibility Issues

### Issue: Styles broken in Safari

**Symptoms:**
Layout looks different in Safari compared to Chrome/Firefox.

**Cause:**
Missing vendor prefixes.

**Solution:**
Ensure autoprefixer is configured:
```javascript
// webpack.config.js
{
  loader: 'postcss-loader',
  options: {
    postcssOptions: {
      plugins: [
        require('autoprefixer')
      ]
    }
  }
}
```

Check browserslist in package.json:
```json
{
  "browserslist": [
    "last 2 versions",
    "> 1%",
    "not dead"
  ]
}
```

---

### Issue: JavaScript errors in IE11

**Symptoms:**
Site breaks in Internet Explorer 11.

**Cause:**
Bootstrap 5 **does not support IE11**.

**Solution:**
Bootstrap 5 officially dropped IE11 support. Options:
1. Don't support IE11 (recommended - IE11 is end-of-life)
2. Stay on Bootstrap 4
3. Use polyfills (not recommended, complex)

---

## Configuration Issues

### Issue: Colors don't match theme

**Symptoms:**
Bootstrap components use wrong colors.

**Solution:**
Override Bootstrap variables before importing:
```scss
// 1. Import functions first
@import "bootstrap/scss/functions";

// 2. Override variables
$primary: #your-color;
$secondary: #your-color;
$success: #your-color;
// etc.

// 3. Import rest of Bootstrap
@import "bootstrap/scss/variables";
@import "bootstrap/scss/variables-dark";
// ... etc
```

Or use CSS custom properties:
```css
:root {
  --bs-primary: #your-color;
  --bs-secondary: #your-color;
}
```

---

### Issue: Breakpoints not matching design

**Symptoms:**
Components break at wrong screen sizes.

**Solution:**
Override breakpoints:
```scss
@import "bootstrap/scss/functions";

// Override breakpoints
$grid-breakpoints: (
  xs: 0,
  sm: 576px,
  md: 768px,
  lg: 992px,
  xl: 1200px,
  xxl: 1400px  // Or your custom value
);

@import "bootstrap/scss/variables";
// ... etc
```

---

## Quick Troubleshooting Checklist

When something doesn't work, check these in order:

1. **Is Bootstrap 5 installed?**
   ```bash
   npm list bootstrap
   ```

2. **Is the build successful?**
   ```bash
   npm run build
   ```

3. **Are data attributes correct?**
   - Look for `data-bs-*` (not `data-*`)

4. **Are IDs matching?**
   - `data-bs-target="#id"` matches `id="id"`

5. **Are classes updated?**
   - Check for Bootstrap 4 classes that were removed/renamed

6. **Is JavaScript imported?**
   ```javascript
   import Collapse from 'bootstrap/js/dist/collapse';
   ```

7. **Is Popper.js loaded?** (for dropdowns/tooltips/popovers)
   ```bash
   npm list @popperjs/core
   ```

8. **Are Drupal behaviors used correctly?**
   ```javascript
   Drupal.behaviors.name = {
     attach: function(context) {
       $('.selector', context).once('name').each(...);
     }
   };
   ```

9. **Is cache cleared?**
   ```bash
   drush cr
   ```

10. **Is library version bumped?**
    ```yaml
    module_name:
      version: 1.X  # Increment
    ```

---

## Getting Help

If you're still stuck after trying these solutions:

1. **Check Bootstrap 5 documentation:**
   - https://getbootstrap.com/docs/5.3/

2. **Check Browser console for errors:**
   - Press F12 to open DevTools
   - Look in Console tab for JavaScript errors
   - Look in Network tab for failed resource loads

3. **Check Drupal logs:**
   ```bash
   drush watchdog:show --count=50
   ```

4. **Ask the team:**
   - Share specific error messages
   - Share relevant code snippets
   - Share what you've already tried

5. **Create a minimal reproduction:**
   - Isolate the issue to smallest possible example
   - Test in fresh environment

---

## Search Index

Quick search for common error messages:

- "Cannot find module" → [Build Errors](#build-errors)
- "Undefined variable" → [Build Errors](#build-errors)
- "is not defined" → [Runtime JavaScript Errors](#runtime-javascript-errors)
- "is not a function" → [Runtime JavaScript Errors](#runtime-javascript-errors)
- "data-bs-toggle does nothing" → [Runtime JavaScript Errors](#runtime-javascript-errors)
- "Forms look broken" → [Styling Issues](#styling-issues)
- "Buttons not full width" → [Styling Issues](#styling-issues)
- "Text alignment" → [Styling Issues](#styling-issues)
- "Accordion doesn't open" → [Component Behavior Issues](#component-behavior-issues)
- "Modal doesn't open" → [Component Behavior Issues](#component-behavior-issues)
- "Dropdown doesn't open" → [Component Behavior Issues](#component-behavior-issues)
- "Tooltip doesn't show" → [Component Behavior Issues](#component-behavior-issues)
- "Layout Builder" → [Drupal Integration Issues](#drupal-integration-issues)
- "AJAX" → [Drupal Integration Issues](#drupal-integration-issues)
- "Configuration" → [Drupal Integration Issues](#drupal-integration-issues)
- "Large bundle" → [Performance Issues](#performance-issues)
- "Safari" → [Browser Compatibility Issues](#browser-compatibility-issues)
- "Colors" → [Configuration Issues](#configuration-issues)
- "Breakpoints" → [Configuration Issues](#configuration-issues)

---

*Last Updated: 2025-10-17*
*For YMCA Website Services Bootstrap 5 Migration*
