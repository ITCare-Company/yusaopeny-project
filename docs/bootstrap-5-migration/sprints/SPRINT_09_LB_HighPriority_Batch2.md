# Sprint 9: Layout Builder High Priority - Batch 2

**Phase:** [Phase 3 - Layout Builder](../phases/PHASE_3_LAYOUT_BUILDER.md)
**Resources:** 1 Developer
**Status:** Not Started

---

## Sprint Goal

Migrate the most complex Layout Builder modules: modal (critical JavaScript API changes) and webform (form styling and integration).

---

## Modules in This Sprint

### 1. lb_modal
- **Path:** `docroot/modules/contrib/lb_modal`
- **Priority:** CRITICAL
- **Complexity:** HIGH
- **Reason:** Modal API changed significantly in Bootstrap 5, heavily used for CTAs

### 2. lb_webform
- **Path:** `docroot/modules/contrib/lb_webform`
- **Priority:** CRITICAL
- **Complexity:** MEDIUM-HIGH
- **Reason:** Form class changes, integration with webform_bootstrap module

---

## Tasks

### Task 1: Migrate lb_modal
**Owner:** Developer
**Priority:** CRITICAL
**Complexity:** HIGH

**Actions:**
```bash
cd docroot/modules/contrib/lb_modal

# Study current implementation
cat package.json
cat webpack.config.js
cat js/*.js
cat templates/*.html.twig
ls assets/scss/
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
- Ensure Bootstrap JavaScript is properly bundled

**1.3 Update SCSS files:**
```scss
@import "bootstrap/scss/modal";
@import "bootstrap/scss/transitions";

// Bootstrap 5 changes:
// - Modal backdrop now uses CSS variables
// - Modal-dialog-scrollable: check if used
// - Modal-dialog-centered: verify positioning
```

**1.4 Update Twig templates - Data attributes:**
```twig
{# Bootstrap 4 #}
<button data-toggle="modal" data-target="#myModal">Open Modal</button>

<div class="modal fade" id="myModal" tabindex="-1" role="dialog">
  <div class="modal-dialog" role="document">
    <div class="modal-content">
      <div class="modal-header">
        <h5 class="modal-title">Title</h5>
        <button type="button" class="close" data-dismiss="modal">
          <span aria-hidden="true">&times;</span>
        </button>
      </div>
      <div class="modal-body">Content</div>
      <div class="modal-footer">
        <button type="button" class="btn btn-secondary" data-dismiss="modal">Close</button>
      </div>
    </div>
  </div>
</div>

{# Bootstrap 5 #}
<button data-bs-toggle="modal" data-bs-target="#myModal">Open Modal</button>

<div class="modal fade" id="myModal" tabindex="-1" aria-labelledby="myModalLabel" aria-hidden="true">
  <div class="modal-dialog">
    <div class="modal-content">
      <div class="modal-header">
        <h5 class="modal-title" id="myModalLabel">Title</h5>
        <button type="button" class="btn-close" data-bs-dismiss="modal" aria-label="Close"></button>
      </div>
      <div class="modal-body">Content</div>
      <div class="modal-footer">
        <button type="button" class="btn btn-secondary" data-bs-dismiss="modal">Close</button>
      </div>
    </div>
  </div>
</div>
```

**Key Changes:**
- `data-toggle` → `data-bs-toggle`
- `data-target` → `data-bs-target`
- `data-dismiss` → `data-bs-dismiss`
- `.close` → `.btn-close` (new button style)
- Remove `role="dialog"` and `role="document"` (redundant)
- Add `aria-labelledby` and `aria-hidden` for accessibility

**1.5 Update JavaScript:**
```javascript
// Bootstrap 4
$('#myModal').modal('show');
$('#myModal').modal('hide');
$('#myModal').modal('toggle');

// Bootstrap 5 - Method 1: Create new instance
var myModal = new bootstrap.Modal(document.getElementById('myModal'), {
  keyboard: false,  // Disable ESC key
  backdrop: 'static'  // Click outside doesn't close
});
myModal.show();
myModal.hide();
myModal.toggle();

// Bootstrap 5 - Method 2: Get existing instance
var myModal = bootstrap.Modal.getInstance(document.getElementById('myModal'));
if (myModal) {
  myModal.show();
} else {
  // Create if doesn't exist
  myModal = new bootstrap.Modal(document.getElementById('myModal'));
  myModal.show();
}

// Bootstrap 5 - Method 3: getOrCreateInstance (recommended)
var myModal = bootstrap.Modal.getOrCreateInstance(document.getElementById('myModal'));
myModal.show();
```

**1.6 Update event listeners:**
```javascript
// Bootstrap 4
$('#myModal').on('show.bs.modal', function (e) {
  console.log('Modal is about to be shown');
});

$('#myModal').on('shown.bs.modal', function (e) {
  console.log('Modal is now visible');
});

// Bootstrap 5
var modalElement = document.getElementById('myModal');

modalElement.addEventListener('show.bs.modal', function (event) {
  console.log('Modal is about to be shown');
  // event.relatedTarget - element that triggered the modal
});

modalElement.addEventListener('shown.bs.modal', function (event) {
  console.log('Modal is now visible');
});

// Other events: hide.bs.modal, hidden.bs.modal, hidePrevented.bs.modal
```

**1.7 Test modal-specific functionality:**
- Modal opens/closes correctly
- Backdrop click behavior (if enabled)
- ESC key closes modal (if enabled)
- Focus trap works (tab navigation stays in modal)
- Multiple modals (if used)
- Modal with forms
- Modal with AJAX content
- Nested modals (if used)

**1.8 Test Drupal integration:**
```bash
# Test modal with Drupal behaviors
# Test modal with Views
# Test modal with Webform (coordinate with Task 2)
# Test modal with CTools
```

**Deliverables:**
- [ ] `docs/bootstrap-5-migration/modules/lb_modal.md` - Migration notes
- [ ] JavaScript API changes documented
- [ ] Modal test page created
- [ ] lb_modal built successfully

**Acceptance Criteria:**
- [ ] Modal opens via button click
- [ ] Modal opens via JavaScript
- [ ] Modal closes via close button
- [ ] Modal closes via backdrop click (if enabled)
- [ ] Modal closes via ESC key (if enabled)
- [ ] Focus trap works
- [ ] No JavaScript console errors
- [ ] Multiple modals don't conflict
- [ ] Modal works with Drupal AJAX
- [ ] Accessibility maintained (keyboard, screen reader)

---

### Task 2: Migrate lb_webform
**Owner:** Developer
**Priority:** CRITICAL

**Actions:**
```bash
cd docroot/modules/contrib/lb_webform

# Study current implementation
cat package.json
cat templates/*.html.twig
cat assets/scss/*.scss

# Check webform_bootstrap module
drush pm:list | grep webform
```

**Migration Steps:**

**2.1 Update package.json:**
- Same as lb_modal (Bootstrap 5.3.3)

**2.2 Update webpack.config.js:**
- Follow lb_accordion pattern

**2.3 Update SCSS files:**
```scss
@import "bootstrap/scss/forms";
@import "bootstrap/scss/buttons";
@import "bootstrap/scss/utilities/api";

// Bootstrap 5 form changes:
// - .form-group removed (use margin utilities instead)
// - .form-row removed (use row/col grid)
// - Custom form controls redesigned
// - Floating labels (new feature)
```

**2.4 Review webform_bootstrap module:**
```bash
# Check if webform_bootstrap is installed
drush pm:list | grep webform_bootstrap

# If installed, check its Bootstrap version compatibility
# May need to update webform_bootstrap to Bootstrap 5 version
```

**2.5 Update form class names:**
```twig
{# Bootstrap 4 #}
<form>
  <div class="form-group">
    <label for="email">Email</label>
    <input type="email" class="form-control" id="email">
    <small class="form-text text-muted">Help text</small>
  </div>
  <div class="form-group">
    <label for="select">Select</label>
    <select class="form-control" id="select">
      <option>1</option>
    </select>
  </div>
  <div class="form-group form-check">
    <input type="checkbox" class="form-check-input" id="check">
    <label class="form-check-label" for="check">Check</label>
  </div>
</form>

{# Bootstrap 5 #}
<form>
  <div class="mb-3">
    <label for="email" class="form-label">Email</label>
    <input type="email" class="form-control" id="email">
    <div class="form-text">Help text</div>
  </div>
  <div class="mb-3">
    <label for="select" class="form-label">Select</label>
    <select class="form-select" id="select">
      <option>1</option>
    </select>
  </div>
  <div class="mb-3 form-check">
    <input type="checkbox" class="form-check-input" id="check">
    <label class="form-check-label" for="check">Check</label>
  </div>
</form>
```

**Key Changes:**
- `.form-group` → `.mb-3` (or other margin utility)
- `.form-text` class added for help text
- `<select class="form-control">` → `<select class="form-select">`
- `<label>` → `<label class="form-label">`
- `.form-row` → `.row` + `.g-*` (gutter utilities)
- Custom file input completely redesigned
- Input group structure changed (if used)

**2.6 Handle custom form controls:**
```scss
// Custom checkbox/radio styling
// Bootstrap 5 uses CSS for custom controls (no extra markup)

// Custom file input
// Bootstrap 5 uses standard file input with .form-control
```

**2.7 Update input groups (if used):**
```twig
{# Bootstrap 4 #}
<div class="input-group">
  <div class="input-group-prepend">
    <span class="input-group-text">@</span>
  </div>
  <input type="text" class="form-control">
</div>

{# Bootstrap 5 #}
<div class="input-group">
  <span class="input-group-text">@</span>
  <input type="text" class="form-control">
</div>
```

**Key Changes:**
- `.input-group-prepend` removed
- `.input-group-append` removed
- Addons placed directly inside `.input-group`

**2.8 Test form functionality:**
- All input types render correctly
- Checkboxes and radios work
- Select dropdowns work
- Validation states work (valid/invalid)
- Help text displays correctly
- Required field indicators
- Error messages display correctly
- Form submission works

**2.9 Test webform integration:**
```bash
# Create test webform with various field types
drush webform:create test_form

# Test rendering in Layout Builder
# Test submission
# Test validation
```

**Deliverables:**
- [ ] `docs/bootstrap-5-migration/modules/lb_webform.md` - Migration notes
- [ ] Form class mapping documented
- [ ] Test webform created
- [ ] lb_webform built successfully

**Acceptance Criteria:**
- [ ] All input types styled correctly
- [ ] Form validation works
- [ ] Error messages display correctly
- [ ] Help text positioned correctly
- [ ] Required indicators show
- [ ] Forms responsive at all breakpoints
- [ ] Accessibility maintained (labels, ARIA)
- [ ] Webform integration works
- [ ] Coordinate with webform_bootstrap if installed

---

### Task 3: Test Modal + Webform Integration
**Owner:** Developer
**Priority:** HIGH

**Actions:**
```bash
# Create test page with modal containing webform
# This is a common pattern in Y USA sites
```

**Test scenarios:**
1. **Modal with embedded webform:**
   - Open modal with webform inside
   - Fill out form
   - Submit form
   - Verify form submission
   - Check AJAX behavior

2. **Validation in modal:**
   - Trigger validation errors
   - Verify error messages display
   - Check focus management

3. **Form submission in modal:**
   - Submit form successfully
   - Verify modal closes (or stays open based on config)
   - Check success message

4. **Accessibility:**
   - Keyboard navigation through form in modal
   - Focus trap with form fields
   - Screen reader announcements

**Deliverables:**
- [ ] Integration test page created
- [ ] Test scenarios documented
- [ ] Known issues documented (if any)

**Acceptance Criteria:**
- [ ] Modal + webform integration works
- [ ] Form submission in modal works
- [ ] Validation errors display correctly
- [ ] Focus management correct
- [ ] No JavaScript conflicts

---

## Testing

### Manual Testing Required

**lb_modal:**
1. **Basic functionality:**
   - [ ] Modal opens via button
   - [ ] Modal opens via JavaScript
   - [ ] Modal closes via X button
   - [ ] Modal closes via backdrop click
   - [ ] Modal closes via ESC key
   - [ ] Modal closes via JavaScript

2. **JavaScript API:**
   - [ ] `new bootstrap.Modal()` works
   - [ ] `.show()` method works
   - [ ] `.hide()` method works
   - [ ] `.toggle()` method works
   - [ ] `.getInstance()` works
   - [ ] `.getOrCreateInstance()` works

3. **Events:**
   - [ ] `show.bs.modal` fires
   - [ ] `shown.bs.modal` fires
   - [ ] `hide.bs.modal` fires
   - [ ] `hidden.bs.modal` fires

4. **Advanced:**
   - [ ] Multiple modals on page
   - [ ] Modal with AJAX content
   - [ ] Modal with forms
   - [ ] Nested modals (if used)

**lb_webform:**
1. **Form rendering:**
   - [ ] Text inputs styled
   - [ ] Textareas styled
   - [ ] Select dropdowns styled
   - [ ] Checkboxes styled
   - [ ] Radio buttons styled
   - [ ] File uploads styled
   - [ ] Buttons styled

2. **Form states:**
   - [ ] Valid state styling
   - [ ] Invalid state styling
   - [ ] Disabled state styling
   - [ ] Required field indicators

3. **Form functionality:**
   - [ ] Form submits correctly
   - [ ] Validation works
   - [ ] Error messages display
   - [ ] Success messages display
   - [ ] AJAX submission works (if used)

4. **Responsive:**
   - [ ] Forms readable on mobile
   - [ ] Touch targets adequate
   - [ ] Labels don't overlap

### Automated Testing

**BackstopJS scenarios:**
```json
{
  "scenarios": [
    {
      "label": "Modal Closed",
      "url": "http://yusaopeny.docksal.site/test/lb-modal"
    },
    {
      "label": "Modal Open",
      "url": "http://yusaopeny.docksal.site/test/lb-modal",
      "clickSelector": "[data-bs-toggle='modal']",
      "delay": 1000
    },
    {
      "label": "Webform",
      "url": "http://yusaopeny.docksal.site/test/lb-webform"
    }
  ]
}
```

**Pa11y testing:**
```bash
# Test accessibility
npx pa11y-ci http://yusaopeny.docksal.site/test/lb-modal
npx pa11y-ci http://yusaopeny.docksal.site/test/lb-webform
```

---

## Deliverables

### Must Have:
- [ ] lb_modal migrated and tested
- [ ] lb_webform migrated and tested
- [ ] Modal + webform integration tested
- [ ] Module migration notes created
- [ ] JavaScript API changes documented
- [ ] Form class mapping guide created

### Nice to Have:
- [ ] Video demo of modal functionality
- [ ] Form styling pattern library
- [ ] Migration guide for custom webforms

---

## Decision Points

### Decision: webform_bootstrap Module Strategy
**Options:**
- A) Wait for webform_bootstrap Bootstrap 5 update
- B) Replace webform_bootstrap with custom styling
- C) Contribute Bootstrap 5 patch to webform_bootstrap

**Decision Required By:** Start of Task 2
**Investigation:** Check webform_bootstrap issue queue for Bootstrap 5 support

---

## Risks

### Risk: Modal Focus Trap May Conflict with Drupal (HIGH)
**Mitigation:**
- Test modal with Drupal AJAX
- Test modal with Drupal dialogs
- Check for focus management conflicts
- Test with CTools modals (if used)
- Document any conflicts found

### Risk: webform_bootstrap Not Compatible with Bootstrap 5 (HIGH)
**Mitigation:**
- Check issue queue early
- Have custom styling fallback ready
- Consider contributing patch
- Test without webform_bootstrap if needed

### Risk: Form Validation Styling May Break (MEDIUM)
**Mitigation:**
- Test all validation states
- Test server-side validation messages
- Test client-side validation
- Check Drupal's form API integration

---

## Notes

### Important:
- Modal API changes are extensive - allocate sufficient testing time
- Modal + webform is a critical use case for Y USA sites
- Test modal with real content, not just demos
- Form styling affects entire site, not just webforms

### Tips:
- Use `bootstrap.Modal.getOrCreateInstance()` for simplest initialization
- Test modal events extensively - many sites rely on them
- Document all form class changes for content editors
- Consider creating form styling guide for theme

### Bootstrap 5 Modal API Reference:
- [Bootstrap 5 Modal Docs](https://getbootstrap.com/docs/5.3/components/modal/)
- [Bootstrap 5 Forms Docs](https://getbootstrap.com/docs/5.3/forms/overview/)
- [Bootstrap 4 to 5 Modal Migration](https://getbootstrap.com/docs/5.3/migration/#modal)
- [Bootstrap 4 to 5 Forms Migration](https://getbootstrap.com/docs/5.3/migration/#forms)

---

## Sprint Review Checklist

At end of sprint, verify:
- [ ] Both modules migrated
- [ ] All tasks completed
- [ ] Integration testing complete
- [ ] No blocking issues
- [ ] Sprint 10 ready to start
- [ ] Any issues documented for Sprint 13

---

## Navigation

- **Previous:** [Sprint 8 - LB High Priority Batch 1](SPRINT_08_LB_HighPriority_Batch1.md)
- **Next:** [Sprint 10 - LB Medium Priority Batch 1](SPRINT_10_LB_MediumPriority_Batch1.md)
- **Phase:** [Phase 3 - Layout Builder](../phases/PHASE_3_LAYOUT_BUILDER.md)
- **Overview:** [Executive Summary](../EXECUTIVE_SUMMARY.md)

---

**Sprint Status:** ⬜ Not Started
**Last Updated:** 2025-10-17
