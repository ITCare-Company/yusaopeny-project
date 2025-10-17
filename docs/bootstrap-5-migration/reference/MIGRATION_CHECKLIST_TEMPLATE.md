# Bootstrap 5 Migration Checklist Template

Use this checklist for each module being migrated from Bootstrap 4 to Bootstrap 5. Copy this entire document for each module and track progress.

---

## Module Information

**Module Name:** `_______________________`
**Module Path:** `/path/to/module`
**Migration Branch:** `bootstrap5/MODULE_NAME`
**Issue/Ticket:** `#_____`
**Assigned To:** `_______________________`
**Started:** `YYYY-MM-DD`
**Completed:** `YYYY-MM-DD`

---

## Pre-Migration Assessment

### Scope Analysis

- [ ] **Identify Bootstrap 4 usage**
  - [ ] Scan templates for Bootstrap 4 classes
  - [ ] Scan templates for data attributes (data-toggle, data-target, etc.)
  - [ ] Scan JavaScript for Bootstrap component initialization
  - [ ] Scan SCSS for Bootstrap imports
  - [ ] Document all Bootstrap components used

- [ ] **List affected files**
  ```
  Templates (.twig):
  -

  JavaScript (.js):
  -

  SCSS (.scss):
  -

  Libraries (.libraries.yml):
  -

  PHP (.module, .install):
  -

  Other:
  -
  ```

- [ ] **Identify dependencies**
  - [ ] Check if module depends on other Bootstrap 4 modules
  - [ ] Check if other modules depend on this module
  - [ ] List parent theme dependencies
  - [ ] List JavaScript library dependencies

- [ ] **Estimate complexity**
  - [ ] Simple (1-2 templates, minimal JS): ☐
  - [ ] Medium (3-5 templates, moderate JS): ☐
  - [ ] Complex (6+ templates, complex JS, custom components): ☐

### Backup

- [ ] **Create backup**
  - [ ] Create feature branch: `git checkout -b bootstrap5/MODULE_NAME`
  - [ ] Ensure original code is committed
  - [ ] Tag original state if needed

---

## Phase 1: Build System Setup

### Node/NPM Configuration

- [ ] **Create/update package.json**
  - [ ] Add Bootstrap 5 dependency: `"bootstrap": "^5.3.3"`
  - [ ] Add Popper.js dependency: `"@popperjs/core": "^2.11.8"`
  - [ ] Add webpack or build tools
  - [ ] Add PurgeCSS for optimization
  - [ ] Add required loaders (sass-loader, css-loader, etc.)

- [ ] **Create/update .nvmrc**
  - [ ] Specify Node version (e.g., `18` or `20`)

- [ ] **Create/update webpack.config.js**
  - [ ] Configure entry points (JS and SCSS)
  - [ ] Configure output paths
  - [ ] Add MiniCssExtractPlugin
  - [ ] Add PurgeCSSPlugin
  - [ ] Configure SCSS/SASS loader
  - [ ] Configure PostCSS with autoprefixer

- [ ] **Set up build scripts**
  - [ ] Add `npm run build` script
  - [ ] Add `npm run watch` script
  - [ ] Test build process works

- [ ] **Create assets directory structure**
  ```
  module/
    assets/
      js/
        module_name.js
      scss/
        module_name.scss
      dist/
        module_name.css
        module_name.js
  ```

### Initial Build

- [ ] **Install dependencies**
  - [ ] Run `nvm install` (if using nvm)
  - [ ] Run `npm install`
  - [ ] Verify no errors

- [ ] **Create initial SCSS file**
  - [ ] Import Bootstrap 5 functions
  - [ ] Import Bootstrap 5 variables
  - [ ] Import variable overrides (if needed)
  - [ ] Import required Bootstrap components
  - [ ] Import utilities API
  - [ ] Add custom styles

- [ ] **Create initial JavaScript file**
  - [ ] Import required Bootstrap JS components
  - [ ] Add Drupal behaviors wrapper
  - [ ] Add component initialization code

- [ ] **Test initial build**
  - [ ] Run `npm run build`
  - [ ] Verify CSS is generated in dist/
  - [ ] Verify JS is generated in dist/
  - [ ] Check for build errors

---

## Phase 2: Template Migration

### HTML/Twig Updates

- [ ] **Update data attributes** (Find & Replace)
  - [ ] `data-toggle` → `data-bs-toggle`
  - [ ] `data-target` → `data-bs-target`
  - [ ] `data-dismiss` → `data-bs-dismiss`
  - [ ] `data-parent` → `data-bs-parent`
  - [ ] `data-content` → `data-bs-content`
  - [ ] `data-placement` → `data-bs-placement`
  - [ ] `data-trigger` → `data-bs-trigger`
  - [ ] Other data-* attributes specific to your module

- [ ] **Update class names**
  - [ ] Form classes:
    - [ ] Remove `.form-group` → add `.mb-3` or similar
    - [ ] Remove `.form-row` → use `.row .g-*`
    - [ ] `.custom-control` → `.form-check`
    - [ ] `.custom-control-input` → `.form-check-input`
    - [ ] `.custom-control-label` → `.form-check-label`
    - [ ] `.custom-switch` → `.form-switch`
    - [ ] `.custom-select` → `.form-select`
    - [ ] `.custom-file` → `.form-control` (for file inputs)
    - [ ] `.custom-range` → `.form-range`
    - [ ] Add `.form-label` to label elements

  - [ ] Button classes:
    - [ ] `.btn-block` → `.w-100` or wrap with `.d-grid`
    - [ ] `.close` → `.btn-close`

  - [ ] Text/Typography classes:
    - [ ] `.text-left` → `.text-start`
    - [ ] `.text-right` → `.text-end`
    - [ ] `.font-weight-bold` → `.fw-bold`
    - [ ] `.font-weight-normal` → `.fw-normal`
    - [ ] `.font-italic` → `.fst-italic`
    - [ ] `.text-monospace` → `.font-monospace`

  - [ ] Float classes:
    - [ ] `.float-left` → `.float-start`
    - [ ] `.float-right` → `.float-end`

  - [ ] Spacing classes:
    - [ ] `.ml-*` → `.ms-*`
    - [ ] `.mr-*` → `.me-*`
    - [ ] `.pl-*` → `.ps-*`
    - [ ] `.pr-*` → `.pe-*`

  - [ ] Border classes:
    - [ ] `.border-left` → `.border-start`
    - [ ] `.border-right` → `.border-end`
    - [ ] `.rounded-left` → `.rounded-start`
    - [ ] `.rounded-right` → `.rounded-end`

  - [ ] Grid classes:
    - [ ] `.no-gutters` → `.g-0`

  - [ ] Input group:
    - [ ] Remove `.input-group-prepend` and `.input-group-append` wrappers
    - [ ] Keep elements directly in `.input-group`

- [ ] **Update component markup**
  - [ ] Modal markup (if used)
  - [ ] Accordion markup (if used)
  - [ ] Dropdown markup (if used)
  - [ ] Tabs markup (if used)
  - [ ] Collapse markup (if used)
  - [ ] Cards markup (if used)
  - [ ] Forms markup
  - [ ] Buttons markup

- [ ] **Replace removed components**
  - [ ] Replace `.jumbotron` with utility classes
  - [ ] Replace `.media` with flex utilities
  - [ ] Replace `.card-deck` with grid utilities
  - [ ] Replace `.badge-*` with `.bg-*`

- [ ] **Review each template file**

  File: `_______________________`
  - [ ] Data attributes updated
  - [ ] Classes updated
  - [ ] Markup structure updated
  - [ ] Tested visually

  File: `_______________________`
  - [ ] Data attributes updated
  - [ ] Classes updated
  - [ ] Markup structure updated
  - [ ] Tested visually

  File: `_______________________`
  - [ ] Data attributes updated
  - [ ] Classes updated
  - [ ] Markup structure updated
  - [ ] Tested visually

  *(Add more as needed)*

---

## Phase 3: SCSS Migration

### Bootstrap Imports

- [ ] **Update Bootstrap SCSS imports**
  - [ ] Import functions first: `@import "bootstrap/scss/functions";`
  - [ ] Add variable overrides
  - [ ] Import variables: `@import "bootstrap/scss/variables";`
  - [ ] Import dark mode variables: `@import "bootstrap/scss/variables-dark";`
  - [ ] Import maps: `@import "bootstrap/scss/maps";`
  - [ ] Import mixins: `@import "bootstrap/scss/mixins";`
  - [ ] Import only required components (lean imports)
  - [ ] Import utilities: `@import "bootstrap/scss/utilities";`
  - [ ] Import utilities API: `@import "bootstrap/scss/utilities/api";`

- [ ] **Verify required Bootstrap components are imported**
  - [ ] Accordion: ☐
  - [ ] Buttons: ☐
  - [ ] Cards: ☐
  - [ ] Collapse: ☐
  - [ ] Dropdown: ☐
  - [ ] Forms: ☐
  - [ ] Grid: ☐
  - [ ] Modal: ☐
  - [ ] Nav/Navbar: ☐
  - [ ] Transitions: ☐
  - [ ] Utilities: ☐
  - [ ] Other: _______________

### Custom Styles

- [ ] **Update custom SCSS**
  - [ ] Remove references to removed Bootstrap variables
  - [ ] Update mixin usage if needed
  - [ ] Update color variables
  - [ ] Check for @extend usage (ensure extended classes exist in BS5)
  - [ ] Update media query usage
  - [ ] Test responsive breakpoints (including new XXL)

- [ ] **Variable overrides**
  - [ ] Document all Bootstrap variable overrides
  - [ ] Verify variables still exist in Bootstrap 5
  - [ ] Update variable names if changed
  - [ ] Add new variables as needed

- [ ] **Custom component styles**
  - [ ] Review each custom component for Bootstrap 4 dependencies
  - [ ] Update to use Bootstrap 5 patterns
  - [ ] Test component styling

### Build and Optimization

- [ ] **Configure PurgeCSS**
  - [ ] Set correct paths to scan (templates/)
  - [ ] Add safelist for dynamic classes if needed
  - [ ] Test that required styles aren't purged

- [ ] **Build optimized CSS**
  - [ ] Run production build: `npm run build`
  - [ ] Check output file size
  - [ ] Verify CSS is minified
  - [ ] Check that unused styles are removed

- [ ] **Review generated CSS**
  - [ ] Open dist/MODULE_NAME.css
  - [ ] Verify expected styles are present
  - [ ] Check for any unexpected Bootstrap components
  - [ ] Ensure no duplicate styles

---

## Phase 4: JavaScript Migration

### Bootstrap JS Imports

- [ ] **Update JavaScript imports**
  - [ ] Change from: `import 'bootstrap';`
  - [ ] Change to: `import ComponentName from 'bootstrap/js/dist/component';`
  - [ ] Import only needed components:
    - [ ] Collapse: `import Collapse from 'bootstrap/js/dist/collapse';`
    - [ ] Modal: `import Modal from 'bootstrap/js/dist/modal';`
    - [ ] Dropdown: `import Dropdown from 'bootstrap/js/dist/dropdown';`
    - [ ] Tab: `import Tab from 'bootstrap/js/dist/tab';`
    - [ ] Toast: `import Toast from 'bootstrap/js/dist/toast';`
    - [ ] Tooltip: `import Tooltip from 'bootstrap/js/dist/tooltip';`
    - [ ] Popover: `import Popover from 'bootstrap/js/dist/popover';`
    - [ ] Offcanvas: `import Offcanvas from 'bootstrap/js/dist/offcanvas';`
    - [ ] Other: _______________

### Component Initialization

- [ ] **Update component initialization**
  - [ ] Identify all places where Bootstrap components are initialized
  - [ ] Update from jQuery syntax to vanilla JS (if preferred)
  - [ ] Or keep jQuery syntax if jQuery is loaded
  - [ ] Ensure Drupal behaviors work correctly
  - [ ] Test component initialization on dynamically added content

- [ ] **Event listeners**
  - [ ] Update event listeners for Bootstrap events
  - [ ] Verify event names (should be the same: `show.bs.collapse`, etc.)
  - [ ] Update selectors to use `data-bs-*` attributes
  - [ ] Test all event handlers

### Drupal Behaviors

- [ ] **Update Drupal behavior code**
  ```javascript
  (function ($, Drupal, bootstrap) {
    'use strict';

    Drupal.behaviors.moduleName = {
      attach: function (context, settings) {
        // Updated code here
      }
    };
  })(jQuery, Drupal, bootstrap);
  ```

- [ ] **Test behavior attachment**
  - [ ] Test on initial page load
  - [ ] Test with AJAX content
  - [ ] Test with Layout Builder preview
  - [ ] Test with Drupal.attachBehaviors() calls

### Build JavaScript

- [ ] **Build optimized JavaScript**
  - [ ] Run production build: `npm run build`
  - [ ] Check output file size
  - [ ] Verify JS is bundled correctly
  - [ ] Check for console errors

- [ ] **Review generated JavaScript**
  - [ ] Open dist/MODULE_NAME.js
  - [ ] Verify Bootstrap components are included
  - [ ] Check for any syntax errors
  - [ ] Test in browser console

---

## Phase 5: Drupal Library Updates

### Update .libraries.yml

- [ ] **Update library definitions**
  - [ ] Bump version number (e.g., 1.8 → 1.9)
  - [ ] Verify CSS path: `assets/dist/MODULE_NAME.css`
  - [ ] Verify JS path: `assets/dist/MODULE_NAME.js`
  - [ ] Update dependencies if needed
  - [ ] Remove old Bootstrap 4 dependencies
  - [ ] Keep `core/jquery` if using jQuery
  - [ ] Keep `core/drupal` for Drupal behaviors

- [ ] **Example library definition:**
  ```yaml
  module_name:
    version: 1.9
    css:
      theme:
        assets/dist/module_name.css: { preprocess: true }
    js:
      assets/dist/module_name.js: { minified: true }
    dependencies:
      - core/jquery
      - core/drupal
  ```

### Update PHP Files

- [ ] **Review .module file**
  - [ ] Check for any Bootstrap 4 specific code
  - [ ] Update comments if needed
  - [ ] Verify hook implementations work with Bootstrap 5

- [ ] **Review .install file**
  - [ ] Check update hooks
  - [ ] Add new update hook if configuration changes needed
  - [ ] Test install/uninstall

---

## Phase 6: Documentation

### Code Documentation

- [ ] **Update README.md**
  - [ ] Update build instructions
  - [ ] Document Bootstrap 5 migration
  - [ ] Update dependencies list
  - [ ] Add examples if needed
  - [ ] Update version numbers

- [ ] **Update inline comments**
  - [ ] Remove Bootstrap 4 references in comments
  - [ ] Add Bootstrap 5 references where helpful
  - [ ] Document any workarounds or gotchas

- [ ] **Document breaking changes**
  - [ ] List any API changes
  - [ ] List any template changes
  - [ ] List any class changes that affect themes
  - [ ] Document upgrade path for existing sites

### Migration Notes

- [ ] **Create migration notes document**
  ```markdown
  # Bootstrap 5 Migration - MODULE_NAME

  ## Changes Made
  -

  ## Breaking Changes
  -

  ## Testing Notes
  -

  ## Known Issues
  -
  ```

---

## Phase 7: Testing

### Visual Testing

- [ ] **Test all components visually**
  - [ ] Desktop view (1920x1080)
  - [ ] Laptop view (1366x768)
  - [ ] Tablet view (768x1024)
  - [ ] Mobile view (375x667)
  - [ ] Large desktop (1400px+) - NEW XXL breakpoint

- [ ] **Test component states**
  - [ ] Default state
  - [ ] Hover state
  - [ ] Active state
  - [ ] Focus state
  - [ ] Disabled state
  - [ ] Error state (for forms)
  - [ ] Success state (for forms)

- [ ] **Test component interactions**
  - [ ] Accordion: expand/collapse
  - [ ] Modal: open/close
  - [ ] Dropdown: open/close
  - [ ] Tabs: switch tabs
  - [ ] Collapse: toggle
  - [ ] Forms: input/validation
  - [ ] Other: _______________

### Browser Testing

- [ ] **Test in modern browsers**
  - [ ] Chrome (latest)
  - [ ] Firefox (latest)
  - [ ] Safari (latest)
  - [ ] Edge (latest)

- [ ] **Test in mobile browsers**
  - [ ] iOS Safari
  - [ ] Chrome Mobile
  - [ ] Firefox Mobile

### Functional Testing

- [ ] **Test Drupal integration**
  - [ ] Layout Builder: Add/edit/remove block
  - [ ] Content editing: Create/edit/view content
  - [ ] Configuration: Export/import config
  - [ ] Cache: Clear cache and verify
  - [ ] AJAX: Test AJAX functionality
  - [ ] Forms: Submit/validate forms

- [ ] **Test JavaScript functionality**
  - [ ] All Bootstrap components work correctly
  - [ ] Drupal behaviors attach correctly
  - [ ] No console errors
  - [ ] No JavaScript warnings
  - [ ] Performance is acceptable

### Accessibility Testing

- [ ] **Test keyboard navigation**
  - [ ] Tab through all interactive elements
  - [ ] Test Enter/Space on buttons
  - [ ] Test Escape on modals/dropdowns
  - [ ] Test arrow keys on appropriate components

- [ ] **Test screen reader**
  - [ ] ARIA attributes are correct
  - [ ] Labels are associated correctly
  - [ ] Focus management works
  - [ ] Announcements are appropriate

- [ ] **Run automated accessibility tests**
  - [ ] axe DevTools browser extension
  - [ ] WAVE browser extension
  - [ ] Lighthouse accessibility audit
  - [ ] Fix any issues found

### Performance Testing

- [ ] **Check bundle sizes**
  - [ ] CSS file size: _______ KB
  - [ ] JS file size: _______ KB
  - [ ] Compare to Bootstrap 4 version
  - [ ] Optimize if too large

- [ ] **Check page load performance**
  - [ ] Run Lighthouse performance audit
  - [ ] Check Time to Interactive
  - [ ] Check First Contentful Paint
  - [ ] Optimize if needed

### Regression Testing

- [ ] **Test that nothing broke**
  - [ ] Check other modules using this module
  - [ ] Check theme integration
  - [ ] Check other Bootstrap components on page
  - [ ] Test full page layouts

---

## Phase 8: Code Review

### Self Review

- [ ] **Review your own code**
  - [ ] Remove debugging code
  - [ ] Remove commented-out code
  - [ ] Check code formatting
  - [ ] Check for console.log() statements
  - [ ] Verify all TODOs are addressed

- [ ] **Check coding standards**
  - [ ] Run PHPCS on PHP files
  - [ ] Run ESLint on JS files (if configured)
  - [ ] Run Stylelint on CSS files (if configured)
  - [ ] Fix any issues

- [ ] **Verify commit history**
  - [ ] Commits are logical and atomic
  - [ ] Commit messages are clear
  - [ ] No merge commits (if rebasing)
  - [ ] No accidentally committed files

### Peer Review

- [ ] **Request code review**
  - [ ] Create pull request
  - [ ] Add reviewers
  - [ ] Link to issue/ticket
  - [ ] Provide testing instructions

- [ ] **Address review feedback**
  - [ ] Respond to all comments
  - [ ] Make requested changes
  - [ ] Re-request review if needed

---

## Phase 9: Deployment Preparation

### Build for Production

- [ ] **Create production build**
  - [ ] Run `npm run build` in production mode
  - [ ] Verify files are minified
  - [ ] Verify files are optimized
  - [ ] Commit built files to git

- [ ] **Update library version**
  - [ ] Bump version in .libraries.yml
  - [ ] Update README with new version
  - [ ] Document changes in CHANGELOG (if exists)

### Configuration Management

- [ ] **Export configuration**
  - [ ] Run `drush cex` to export config
  - [ ] Review changes in config files
  - [ ] Commit config changes

- [ ] **Test configuration import**
  - [ ] Test on fresh site
  - [ ] Run `drush cim` to import config
  - [ ] Verify no errors
  - [ ] Verify module works after import

### Update Hooks

- [ ] **Create update hooks if needed**
  - [ ] Add to .install file
  - [ ] Test update hook execution
  - [ ] Document update hook in comments

### Create Release

- [ ] **Prepare release**
  - [ ] Tag version in git
  - [ ] Create release notes
  - [ ] Update documentation
  - [ ] Create changelog entry

---

## Phase 10: Deployment

### Pre-Deployment Checklist

- [ ] **Verify everything is ready**
  - [ ] All tests pass
  - [ ] Code review approved
  - [ ] Documentation updated
  - [ ] Built assets committed
  - [ ] Configuration exported

### Staging Deployment

- [ ] **Deploy to staging**
  - [ ] Deploy code to staging environment
  - [ ] Run database updates
  - [ ] Import configuration
  - [ ] Clear all caches
  - [ ] Test functionality

- [ ] **Staging smoke test**
  - [ ] Verify module appears in module list
  - [ ] Verify components render correctly
  - [ ] Verify JavaScript works
  - [ ] Verify no console errors
  - [ ] Test a few key workflows

### Production Deployment

- [ ] **Deploy to production**
  - [ ] Deploy code to production
  - [ ] Run database updates
  - [ ] Import configuration
  - [ ] Clear all caches
  - [ ] Test functionality

- [ ] **Production smoke test**
  - [ ] Verify module appears in module list
  - [ ] Verify components render correctly
  - [ ] Verify JavaScript works
  - [ ] Verify no console errors
  - [ ] Monitor error logs

### Post-Deployment

- [ ] **Monitor for issues**
  - [ ] Check error logs (first hour)
  - [ ] Check error logs (first day)
  - [ ] Check error logs (first week)
  - [ ] Address any issues quickly

- [ ] **Gather feedback**
  - [ ] Ask team for feedback
  - [ ] Ask users for feedback
  - [ ] Document any issues
  - [ ] Create follow-up tickets if needed

---

## Phase 11: Post-Migration Cleanup

### Cleanup Code

- [ ] **Remove Bootstrap 4 code**
  - [ ] Remove old package.json dependencies (if separate)
  - [ ] Remove old webpack config (if separate)
  - [ ] Remove old build artifacts
  - [ ] Remove migration notes from code

### Update Tracking

- [ ] **Update project tracking**
  - [ ] Mark issue/ticket as complete
  - [ ] Update migration tracking document
  - [ ] Update project board
  - [ ] Close related issues

### Knowledge Sharing

- [ ] **Share knowledge**
  - [ ] Present to team (if major module)
  - [ ] Document lessons learned
  - [ ] Update team documentation
  - [ ] Create training materials if needed

---

## Rollback Plan

### If Something Goes Wrong

- [ ] **Prepare rollback**
  - [ ] Document rollback procedure
  - [ ] Keep backup of old code
  - [ ] Keep backup of old database
  - [ ] Test rollback procedure

- [ ] **Rollback steps**
  1. Revert code deployment
  2. Restore previous database (if needed)
  3. Clear all caches
  4. Verify site works
  5. Investigate issue
  6. Plan fix

---

## Notes and Issues

### Migration Notes

```
(Add any notes here during migration)



```

### Issues Encountered

```
Issue:
Solution:

Issue:
Solution:
```

### Decisions Made

```
Decision:
Rationale:

Decision:
Rationale:
```

### Follow-up Tasks

- [ ] Task 1: _______________________
- [ ] Task 2: _______________________
- [ ] Task 3: _______________________

---

## Sign-Off

### Developer Sign-Off

- [ ] Migration complete
- [ ] All tests pass
- [ ] Documentation updated
- [ ] Code reviewed

**Developer:** _______________
**Date:** _______________

### QA Sign-Off

- [ ] Tested on staging
- [ ] Tested on production
- [ ] No critical issues

**QA:** _______________
**Date:** _______________

### Product Owner Sign-Off

- [ ] Functionality verified
- [ ] Ready for production

**Product Owner:** _______________
**Date:** _______________

---

*Template Version: 1.0*
*Last Updated: 2025-10-17*
*For YMCA Website Services Bootstrap 5 Migration*
