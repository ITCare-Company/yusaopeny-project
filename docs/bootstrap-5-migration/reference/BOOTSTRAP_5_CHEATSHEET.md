# Bootstrap 5 Migration Cheatsheet

Quick reference guide for migrating from Bootstrap 4 to Bootstrap 5 in the YMCA Website Services distribution.

## Table of Contents

1. [Data Attributes](#data-attributes)
2. [Class Changes](#class-changes)
3. [JavaScript API Changes](#javascript-api-changes)
4. [Removed Components](#removed-components)
5. [New Features](#new-features)
6. [Grid System Changes](#grid-system-changes)
7. [Form Changes](#form-changes)
8. [Color System Changes](#color-system-changes)
9. [Utility Changes](#utility-changes)
10. [SCSS/Sass Changes](#scsssass-changes)

---

## Data Attributes

All Bootstrap JavaScript components now use namespaced data attributes with the `data-bs-*` prefix.

### Modal

```html
<!-- Bootstrap 4 -->
<button data-toggle="modal" data-target="#myModal">Open Modal</button>
<button data-dismiss="modal">Close</button>

<!-- Bootstrap 5 -->
<button data-bs-toggle="modal" data-bs-target="#myModal">Open Modal</button>
<button data-bs-dismiss="modal">Close</button>
```

### Collapse/Accordion

```html
<!-- Bootstrap 4 -->
<button data-toggle="collapse" data-target="#collapseOne" aria-expanded="false">
  Toggle
</button>
<div id="collapseOne" data-parent="#accordion"></div>

<!-- Bootstrap 5 -->
<button data-bs-toggle="collapse" data-bs-target="#collapseOne" aria-expanded="false">
  Toggle
</button>
<div id="collapseOne" data-bs-parent="#accordion"></div>
```

### Dropdown

```html
<!-- Bootstrap 4 -->
<button data-toggle="dropdown">Dropdown</button>

<!-- Bootstrap 5 -->
<button data-bs-toggle="dropdown">Dropdown</button>
```

### Tabs

```html
<!-- Bootstrap 4 -->
<button data-toggle="tab" data-target="#tab1">Tab 1</button>

<!-- Bootstrap 5 -->
<button data-bs-toggle="tab" data-bs-target="#tab1">Tab 1</button>
```

### Tooltip & Popover

```html
<!-- Bootstrap 4 -->
<button data-toggle="tooltip" title="Tooltip text">Hover me</button>
<button data-toggle="popover" data-content="Popover content">Click me</button>

<!-- Bootstrap 5 -->
<button data-bs-toggle="tooltip" title="Tooltip text">Hover me</button>
<button data-bs-toggle="popover" data-bs-content="Popover content">Click me</button>
```

### Toast

```html
<!-- Bootstrap 4 -->
<button data-dismiss="toast">Close</button>

<!-- Bootstrap 5 -->
<button data-bs-dismiss="toast">Close</button>
```

### Alert

```html
<!-- Bootstrap 4 -->
<button data-dismiss="alert">Close</button>

<!-- Bootstrap 5 -->
<button data-bs-dismiss="alert">Close</button>
```

### Complete Data Attribute Mapping

| Bootstrap 4         | Bootstrap 5           | Component        |
|--------------------|-----------------------|------------------|
| data-toggle        | data-bs-toggle        | All components   |
| data-target        | data-bs-target        | Modal, Collapse  |
| data-dismiss       | data-bs-dismiss       | Modal, Alert, Toast |
| data-parent        | data-bs-parent        | Collapse         |
| data-content       | data-bs-content       | Popover          |
| data-trigger       | data-bs-trigger       | Popover          |
| data-placement     | data-bs-placement     | Tooltip, Popover |
| data-offset        | data-bs-offset        | Dropdown, Popover |
| data-ride          | data-bs-ride          | Carousel         |
| data-slide         | data-bs-slide         | Carousel         |
| data-slide-to      | data-bs-slide-to      | Carousel         |
| data-interval      | data-bs-interval      | Carousel         |

---

## Class Changes

### Removed Classes

#### Form Classes

```html
<!-- Bootstrap 4 -->
<div class="form-group">
  <label>Label</label>
  <input class="form-control">
</div>

<!-- Bootstrap 5 -->
<div class="mb-3">
  <label class="form-label">Label</label>
  <input class="form-control">
</div>
```

**`.form-group` is REMOVED**. Use margin utilities like `.mb-3` instead.

```html
<!-- Bootstrap 4 -->
<div class="form-row">
  <div class="col">...</div>
</div>

<!-- Bootstrap 5 -->
<div class="row g-2">
  <div class="col">...</div>
</div>
```

**`.form-row` is REMOVED**. Use `.row` with gutter utilities (`.g-*`).

```html
<!-- Bootstrap 4 -->
<input class="form-control-plaintext">

<!-- Bootstrap 5 -->
<input class="form-control-plaintext"> <!-- Still exists, but less common -->
```

```html
<!-- Bootstrap 4 -->
<label class="form-check-label">
  <input type="checkbox" class="form-check-input">
</label>

<!-- Bootstrap 5 -->
<input type="checkbox" class="form-check-input" id="check1">
<label class="form-check-label" for="check1">Label</label>
```

#### Button Classes

```html
<!-- Bootstrap 4 -->
<button class="btn btn-primary btn-block">Full Width Button</button>

<!-- Bootstrap 5 -->
<button class="btn btn-primary w-100">Full Width Button</button>
<!-- OR with grid -->
<div class="d-grid">
  <button class="btn btn-primary">Full Width Button</button>
</div>
```

**`.btn-block` is REMOVED**. Use `.w-100` or `.d-grid` wrapper.

#### Utility Classes

```html
<!-- Bootstrap 4 -->
<div class="font-weight-bold">Bold text</div>
<div class="font-weight-normal">Normal text</div>

<!-- Bootstrap 5 -->
<div class="fw-bold">Bold text</div>
<div class="fw-normal">Normal text</div>
```

```html
<!-- Bootstrap 4 -->
<div class="text-left">Left aligned</div>
<div class="text-right">Right aligned</div>

<!-- Bootstrap 5 -->
<div class="text-start">Left aligned</div>
<div class="text-end">Right aligned</div>
```

```html
<!-- Bootstrap 4 -->
<div class="float-left">Float left</div>
<div class="float-right">Float right</div>

<!-- Bootstrap 5 -->
<div class="float-start">Float left</div>
<div class="float-end">Float right</div>
```

```html
<!-- Bootstrap 4 -->
<div class="border-left">Border left</div>
<div class="border-right">Border right</div>

<!-- Bootstrap 5 -->
<div class="border-start">Border left</div>
<div class="border-end">Border right</div>
```

```html
<!-- Bootstrap 4 -->
<div class="ml-3">Margin left</div>
<div class="mr-3">Margin right</div>
<div class="pl-3">Padding left</div>
<div class="pr-3">Padding right</div>

<!-- Bootstrap 5 -->
<div class="ms-3">Margin start</div>
<div class="me-3">Margin end</div>
<div class="ps-3">Padding start</div>
<div class="pe-3">Padding end</div>
```

#### Complete Class Mapping

| Bootstrap 4            | Bootstrap 5          | Notes                        |
|-----------------------|----------------------|------------------------------|
| .form-group           | .mb-3 (or similar)   | Use margin utilities         |
| .form-row             | .row .g-*            | Use row with gutter utils    |
| .btn-block            | .w-100 or .d-grid    | Use width or grid utils      |
| .font-weight-*        | .fw-*                | Renamed for brevity          |
| .text-left            | .text-start          | LTR/RTL support              |
| .text-right           | .text-end            | LTR/RTL support              |
| .float-left           | .float-start         | LTR/RTL support              |
| .float-right          | .float-end           | LTR/RTL support              |
| .border-left          | .border-start        | LTR/RTL support              |
| .border-right         | .border-end          | LTR/RTL support              |
| .rounded-left         | .rounded-start       | LTR/RTL support              |
| .rounded-right        | .rounded-end         | LTR/RTL support              |
| .ml-*                 | .ms-*                | Margin start                 |
| .mr-*                 | .me-*                | Margin end                   |
| .pl-*                 | .ps-*                | Padding start                |
| .pr-*                 | .pe-*                | Padding end                  |
| .font-italic          | .fst-italic          | Font style                   |
| .font-weight-normal   | .fw-normal           | Font weight                  |
| .font-weight-bold     | .fw-bold             | Font weight                  |
| .text-monospace       | .font-monospace      | Font family                  |
| .close                | .btn-close           | Close button                 |
| .custom-select        | .form-select         | Form controls                |
| .custom-file          | .form-control        | File input                   |
| .custom-range         | .form-range          | Range input                  |
| .custom-control       | .form-check          | Checkbox/radio wrapper       |
| .custom-control-input | .form-check-input    | Checkbox/radio input         |
| .custom-control-label | .form-check-label    | Checkbox/radio label         |
| .custom-switch        | .form-switch         | Switch toggle                |
| .input-group-append   | .input-group         | Simplified structure         |
| .input-group-prepend  | .input-group         | Simplified structure         |
| .media                | utility classes      | Use flex utilities           |
| .jumbotron            | utility classes      | Use spacing/background utils |
| .badge-*              | .bg-*                | Background colors            |
| .no-gutters           | .g-0                 | Grid gutters                 |

### Renamed Classes

```scss
// Font weight
.font-weight-light → .fw-light
.font-weight-lighter → .fw-lighter
.font-weight-normal → .fw-normal
.font-weight-bold → .fw-bold
.font-weight-bolder → .fw-bolder

// Font style
.font-italic → .fst-italic
.font-style-normal → .fst-normal

// Text decoration
.text-decoration-none → stays the same

// Line height
.lh-1, .lh-sm, .lh-base, .lh-lg → NEW in Bootstrap 5
```

---

## JavaScript API Changes

### Import Statements

```javascript
// Bootstrap 4
import 'bootstrap';

// Bootstrap 5 - Import only what you need
import Collapse from 'bootstrap/js/dist/collapse';
import Modal from 'bootstrap/js/dist/modal';
import Dropdown from 'bootstrap/js/dist/dropdown';
```

### Component Initialization

```javascript
// Bootstrap 4
$('[data-toggle="tooltip"]').tooltip();

// Bootstrap 5 - Vanilla JS (recommended)
const tooltipTriggerList = document.querySelectorAll('[data-bs-toggle="tooltip"]');
const tooltipList = [...tooltipTriggerList].map(el => new bootstrap.Tooltip(el));

// Bootstrap 5 - Still works with jQuery if loaded
$('[data-bs-toggle="tooltip"]').tooltip();
```

### Modal

```javascript
// Bootstrap 4
$('#myModal').modal('show');
$('#myModal').on('show.bs.modal', function() {});

// Bootstrap 5
const modal = new bootstrap.Modal(document.getElementById('myModal'));
modal.show();

document.getElementById('myModal').addEventListener('show.bs.modal', function() {});

// With jQuery (if loaded)
$('#myModal').modal('show');
$('#myModal').on('show.bs.modal', function() {});
```

### Collapse

```javascript
// Bootstrap 4
$('#collapseOne').collapse('show');

// Bootstrap 5
const collapse = new bootstrap.Collapse(document.getElementById('collapseOne'));
collapse.show();

// With jQuery
$('#collapseOne').collapse('show');
```

### Dropdown

```javascript
// Bootstrap 4
$('#myDropdown').dropdown('toggle');

// Bootstrap 5
const dropdown = new bootstrap.Dropdown(document.getElementById('myDropdown'));
dropdown.toggle();
```

### Toast (New in Bootstrap 4.2, improved in 5)

```javascript
// Bootstrap 5
const toast = new bootstrap.Toast(document.getElementById('myToast'));
toast.show();
```

### Popover & Tooltip

```javascript
// Bootstrap 4
$('[data-toggle="popover"]').popover();

// Bootstrap 5
const popoverTriggerList = document.querySelectorAll('[data-bs-toggle="popover"]');
const popoverList = [...popoverTriggerList].map(el => new bootstrap.Popover(el));
```

### Events

Events remain largely the same but work with vanilla JS:

```javascript
// Bootstrap 5 event handling
document.getElementById('myCollapse').addEventListener('show.bs.collapse', function(e) {
  console.log('Collapse is showing');
});

document.getElementById('myCollapse').addEventListener('shown.bs.collapse', function(e) {
  console.log('Collapse is shown');
});

// Available events for collapse:
// - show.bs.collapse
// - shown.bs.collapse
// - hide.bs.collapse
// - hidden.bs.collapse
```

---

## Removed Components

### Jumbotron

```html
<!-- Bootstrap 4 -->
<div class="jumbotron">
  <h1>Hello, world!</h1>
  <p>Lead text here.</p>
</div>

<!-- Bootstrap 5 - Use utilities -->
<div class="bg-light p-5 rounded">
  <h1>Hello, world!</h1>
  <p class="lead">Lead text here.</p>
</div>
```

### Media Object

```html
<!-- Bootstrap 4 -->
<div class="media">
  <img src="..." class="mr-3" alt="...">
  <div class="media-body">
    <h5>Media heading</h5>
    Content
  </div>
</div>

<!-- Bootstrap 5 - Use flex utilities -->
<div class="d-flex">
  <img src="..." class="me-3" alt="...">
  <div class="flex-grow-1">
    <h5>Media heading</h5>
    Content
  </div>
</div>
```

### Card Deck

```html
<!-- Bootstrap 4 -->
<div class="card-deck">
  <div class="card">...</div>
  <div class="card">...</div>
</div>

<!-- Bootstrap 5 - Use grid -->
<div class="row row-cols-1 row-cols-md-2 g-4">
  <div class="col">
    <div class="card">...</div>
  </div>
  <div class="col">
    <div class="card">...</div>
  </div>
</div>
```

### Input Group Append/Prepend

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

<!-- Bootstrap 5 - Simplified -->
<div class="input-group">
  <span class="input-group-text">@</span>
  <input type="text" class="form-control">
  <button class="btn btn-primary">Go</button>
</div>
```

---

## New Features

### Offcanvas

A new component for creating sidebars and drawers:

```html
<button class="btn btn-primary" type="button" data-bs-toggle="offcanvas" data-bs-target="#offcanvasExample">
  Open offcanvas
</button>

<div class="offcanvas offcanvas-start" tabindex="-1" id="offcanvasExample">
  <div class="offcanvas-header">
    <h5 class="offcanvas-title">Offcanvas</h5>
    <button type="button" class="btn-close" data-bs-dismiss="offcanvas"></button>
  </div>
  <div class="offcanvas-body">
    Content here...
  </div>
</div>
```

```javascript
const offcanvas = new bootstrap.Offcanvas(document.getElementById('offcanvasExample'));
offcanvas.show();
```

### Accordion with `accordion-flush`

```html
<div class="accordion accordion-flush" id="accordionFlush">
  <div class="accordion-item">
    <h2 class="accordion-header">
      <button class="accordion-button collapsed" data-bs-toggle="collapse" data-bs-target="#flush-collapseOne">
        Item #1
      </button>
    </h2>
    <div id="flush-collapseOne" class="accordion-collapse collapse" data-bs-parent="#accordionFlush">
      <div class="accordion-body">Content</div>
    </div>
  </div>
</div>
```

### Placeholder (Loading State)

```html
<div class="card">
  <div class="card-body">
    <h5 class="card-title placeholder-glow">
      <span class="placeholder col-6"></span>
    </h5>
    <p class="card-text placeholder-glow">
      <span class="placeholder col-7"></span>
      <span class="placeholder col-4"></span>
    </p>
  </div>
</div>
```

### New Utility Classes

```html
<!-- Gap utilities for flexbox and grid -->
<div class="d-flex gap-2">...</div>
<div class="row g-3">...</div>

<!-- Vertical alignment -->
<div class="align-items-start">...</div>

<!-- Line height -->
<p class="lh-1">Line height 1</p>
<p class="lh-sm">Small line height</p>
<p class="lh-base">Base line height</p>
<p class="lh-lg">Large line height</p>

<!-- Font size -->
<p class="fs-1">Font size 1 (largest)</p>
<p class="fs-6">Font size 6 (smallest)</p>
```

---

## Grid System Changes

### Gutter Classes

```html
<!-- Bootstrap 4 -->
<div class="row no-gutters">
  <div class="col">...</div>
</div>

<!-- Bootstrap 5 -->
<div class="row g-0">
  <div class="col">...</div>
</div>

<!-- New: Control horizontal and vertical gutters separately -->
<div class="row gx-4 gy-2">
  <div class="col">...</div>
</div>
```

Gutter utilities:
- `.g-*` - All gutters (horizontal and vertical)
- `.gx-*` - Horizontal gutters only
- `.gy-*` - Vertical gutters only
- Values: 0, 1, 2, 3, 4, 5

### New XXL Breakpoint

Bootstrap 5 adds a new `xxl` breakpoint at 1400px:

```scss
// Bootstrap 4
$grid-breakpoints: (
  xs: 0,
  sm: 576px,
  md: 768px,
  lg: 992px,
  xl: 1200px
);

// Bootstrap 5
$grid-breakpoints: (
  xs: 0,
  sm: 576px,
  md: 768px,
  lg: 992px,
  xl: 1200px,
  xxl: 1400px
);
```

Usage:
```html
<div class="col-xxl-6">Half width on XXL screens</div>
```

```scss
@include media-breakpoint-up(xxl) {
  // Styles for >= 1400px
}
```

### Row Columns

```html
<!-- Improved in Bootstrap 5 -->
<div class="row row-cols-1 row-cols-md-2 row-cols-lg-3 row-cols-xl-4">
  <div class="col">Column</div>
  <div class="col">Column</div>
  <div class="col">Column</div>
  <div class="col">Column</div>
</div>
```

---

## Form Changes

### Form Controls

```html
<!-- Bootstrap 4 -->
<div class="form-group">
  <label for="email">Email</label>
  <input type="email" class="form-control" id="email">
  <small class="form-text text-muted">Help text</small>
</div>

<!-- Bootstrap 5 -->
<div class="mb-3">
  <label for="email" class="form-label">Email</label>
  <input type="email" class="form-control" id="email">
  <div class="form-text">Help text</div>
</div>
```

### Custom Form Controls

```html
<!-- Bootstrap 4 -->
<div class="custom-control custom-checkbox">
  <input type="checkbox" class="custom-control-input" id="check1">
  <label class="custom-control-label" for="check1">Check me</label>
</div>

<div class="custom-control custom-radio">
  <input type="radio" class="custom-control-input" id="radio1" name="radios">
  <label class="custom-control-label" for="radio1">Radio</label>
</div>

<div class="custom-control custom-switch">
  <input type="checkbox" class="custom-control-input" id="switch1">
  <label class="custom-control-label" for="switch1">Switch</label>
</div>

<select class="custom-select">
  <option>Choose...</option>
</select>

<input type="file" class="custom-file-input" id="file">
<label class="custom-file-label" for="file">Choose file</label>

<input type="range" class="custom-range">

<!-- Bootstrap 5 -->
<div class="form-check">
  <input class="form-check-input" type="checkbox" id="check1">
  <label class="form-check-label" for="check1">Check me</label>
</div>

<div class="form-check">
  <input class="form-check-input" type="radio" id="radio1" name="radios">
  <label class="form-check-label" for="radio1">Radio</label>
</div>

<div class="form-check form-switch">
  <input class="form-check-input" type="checkbox" id="switch1">
  <label class="form-check-label" for="switch1">Switch</label>
</div>

<select class="form-select">
  <option>Choose...</option>
</select>

<input type="file" class="form-control" id="file">

<input type="range" class="form-range">
```

### Floating Labels (New)

```html
<!-- Bootstrap 5 - New feature -->
<div class="form-floating">
  <input type="email" class="form-control" id="floatingInput" placeholder="name@example.com">
  <label for="floatingInput">Email address</label>
</div>

<div class="form-floating">
  <textarea class="form-control" id="floatingTextarea" placeholder="Leave a comment"></textarea>
  <label for="floatingTextarea">Comments</label>
</div>
```

### Input Group

```html
<!-- Bootstrap 4 -->
<div class="input-group">
  <div class="input-group-prepend">
    <span class="input-group-text">$</span>
  </div>
  <input type="text" class="form-control">
  <div class="input-group-append">
    <span class="input-group-text">.00</span>
  </div>
</div>

<!-- Bootstrap 5 -->
<div class="input-group">
  <span class="input-group-text">$</span>
  <input type="text" class="form-control">
  <span class="input-group-text">.00</span>
</div>
```

---

## Color System Changes

### New Colors

Bootstrap 5 doesn't require a separate colors library. All colors are built-in.

### CSS Custom Properties

Bootstrap 5 uses CSS custom properties (CSS variables) extensively:

```css
/* Bootstrap 5 uses CSS variables */
--bs-blue: #0d6efd;
--bs-indigo: #6610f2;
--bs-purple: #6f42c1;
--bs-pink: #d63384;
--bs-red: #dc3545;
--bs-orange: #fd7e14;
--bs-yellow: #ffc107;
--bs-green: #198754;
--bs-teal: #20c997;
--bs-cyan: #0dcaf0;
```

You can override these:

```css
:root {
  --bs-primary: #ff5733;
  --bs-secondary: #333333;
}
```

---

## Utility Changes

### Spacing

Spacing utilities remain mostly the same but with the directional changes:

```html
<!-- Bootstrap 4 -->
<div class="mt-3 mr-2 mb-3 ml-2">Margins</div>
<div class="pt-3 pr-2 pb-3 pl-2">Padding</div>

<!-- Bootstrap 5 -->
<div class="mt-3 me-2 mb-3 ms-2">Margins</div>
<div class="pt-3 pe-2 pb-3 ps-2">Padding</div>
```

### Display

Display utilities work the same:

```html
<div class="d-none d-md-block">Hidden on small, visible on medium+</div>
<div class="d-flex justify-content-between align-items-center">Flex layout</div>
```

### Position

Position utilities are enhanced:

```html
<!-- Translate utilities (new in Bootstrap 5) -->
<div class="position-absolute top-0 start-0">Top left</div>
<div class="position-absolute top-50 start-50 translate-middle">Centered</div>
```

---

## SCSS/Sass Changes

### Import Structure

```scss
// Bootstrap 4
@import "bootstrap/scss/bootstrap";

// Bootstrap 5 - Recommended modular approach
// 1. Include functions first
@import "bootstrap/scss/functions";

// 2. Include any variable overrides here
$primary: #ff5733;
$enable-shadows: true;

// 3. Include variables and the rest
@import "bootstrap/scss/variables";
@import "bootstrap/scss/variables-dark"; // NEW in Bootstrap 5
@import "bootstrap/scss/maps";
@import "bootstrap/scss/mixins";
@import "bootstrap/scss/root";

// 4. Include only the components you need
@import "bootstrap/scss/reboot";
@import "bootstrap/scss/grid";
@import "bootstrap/scss/buttons";
@import "bootstrap/scss/accordion";
// ... etc

// 5. Include utilities API
@import "bootstrap/scss/utilities/api";
```

### Using Lean Imports

For optimal file size, import only what you need:

```scss
// Minimal Bootstrap 5
@import "bootstrap/scss/functions";
@import "bootstrap/scss/variables";
@import "bootstrap/scss/variables-dark";
@import "bootstrap/scss/maps";
@import "bootstrap/scss/mixins";
@import "bootstrap/scss/utilities";
@import "bootstrap/scss/utilities/api";

// Add specific components
@import "bootstrap/scss/buttons";
@import "bootstrap/scss/accordion";
```

### Mixins

Most mixins remain the same:

```scss
// Still work in Bootstrap 5
@include make-container();
@include make-row();
@include make-col-ready();
@include make-col(6);
@include media-breakpoint-up(md) { }
@include media-breakpoint-down(lg) { }
@include media-breakpoint-between(md, xl) { }
```

### Variables

Many variables are renamed or restructured. Check the Bootstrap 5 documentation for specifics.

```scss
// Bootstrap 4
$theme-colors: (
  "primary": $primary,
  "secondary": $secondary,
  // ...
);

// Bootstrap 5 - Same structure, but use map functions
$primary: tint-color($blue, 10%);
$secondary: $gray-600;
```

---

## jQuery Dependency

**Bootstrap 5 removes jQuery dependency** completely.

### If You Need jQuery

Bootstrap 5 still works with jQuery if it's loaded, but doesn't require it:

```javascript
// This still works if jQuery is loaded
$('#myModal').modal('show');

// But vanilla JS is preferred
const modal = new bootstrap.Modal(document.getElementById('myModal'));
modal.show();
```

### Drupal Behaviors

In Drupal, you can still use jQuery from `core/jquery`:

```javascript
(function ($, Drupal, bootstrap) {
  'use strict';

  Drupal.behaviors.myBehavior = {
    attach: function (context, settings) {
      // Use jQuery
      $('.my-element', context).once('myBehavior').each(function() {
        // Initialize Bootstrap 5 component with vanilla JS
        new bootstrap.Modal(this);
      });
    }
  };
})(jQuery, Drupal, bootstrap);
```

---

## Popper.js Version

Bootstrap 4 used Popper.js v1, Bootstrap 5 uses **@popperjs/core v2**.

```json
// package.json
{
  "dependencies": {
    "@popperjs/core": "^2.11.8",
    "bootstrap": "^5.3.3"
  }
}
```

When using dropdowns, tooltips, or popovers, ensure Popper is loaded first.

---

## Migration Tips

1. **Search and Replace**: Use global find/replace for data attributes
2. **Test Components Individually**: Migrate and test one component at a time
3. **Check CSS Specificity**: Your custom styles might override Bootstrap 5 differently
4. **Review JavaScript**: Update any direct Bootstrap JS API calls
5. **Update Dependencies**: Ensure all npm packages are Bootstrap 5 compatible
6. **Use PurgeCSS**: Remove unused CSS to keep bundle size small
7. **Test Responsive Layouts**: Check all breakpoints including new XXL
8. **Validate Forms**: Form markup changes significantly
9. **Check Accessibility**: Bootstrap 5 improves ARIA attributes
10. **Review Documentation**: Check official Bootstrap 5 migration guide

---

## Resources

- [Official Bootstrap 5 Migration Guide](https://getbootstrap.com/docs/5.3/migration/)
- [Bootstrap 5 Documentation](https://getbootstrap.com/docs/5.3/)
- [Bootstrap 5 Examples](https://getbootstrap.com/docs/5.3/examples/)
- [PurgeCSS Documentation](https://purgecss.com/)
- [YMCA WS Bootstrap 5 Migration Tracking Issue](https://github.com/YCloudYUSA/yusaopeny/issues/)

---

## Quick Reference Table

| Category | Bootstrap 4 | Bootstrap 5 | Change Type |
|----------|------------|------------|-------------|
| Data Attributes | data-toggle | data-bs-toggle | Rename |
| Data Attributes | data-target | data-bs-target | Rename |
| Data Attributes | data-dismiss | data-bs-dismiss | Rename |
| Forms | .form-group | .mb-3 | Remove |
| Forms | .form-row | .row .g-* | Remove |
| Forms | .custom-control | .form-check | Rename |
| Forms | .custom-select | .form-select | Rename |
| Buttons | .btn-block | .w-100 / .d-grid | Remove |
| Buttons | .close | .btn-close | Rename |
| Text | .text-left/right | .text-start/end | Rename |
| Text | .font-weight-* | .fw-* | Rename |
| Float | .float-left/right | .float-start/end | Rename |
| Spacing | .ml-*/mr-* | .ms-*/me-* | Rename |
| Spacing | .pl-*/pr-* | .ps-*/pe-* | Rename |
| Components | .jumbotron | utilities | Remove |
| Components | .media | flex utilities | Remove |
| Components | .card-deck | grid utilities | Remove |
| Input Group | .input-group-prepend/append | .input-group | Simplify |
| Grid | .no-gutters | .g-0 | Rename |
| Grid | - | .gx-*, .gy-* | New |
| Breakpoint | - | xxl (1400px) | New |
| Component | - | .offcanvas | New |
| Component | - | .placeholder | New |
| JavaScript | jQuery required | Vanilla JS | Remove dependency |
| JavaScript | import 'bootstrap' | import specific | Lean imports |

---

*Last Updated: 2025-10-17*
*Bootstrap Version: 5.3.3*
*For YMCA Website Services Distribution*
