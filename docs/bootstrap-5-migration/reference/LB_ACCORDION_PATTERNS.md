# lb_accordion Bootstrap 5 Patterns

Detailed analysis of the `lb_accordion` module as a reference implementation for Bootstrap 5 migration.

## Table of Contents

1. [Overview](#overview)
2. [File Structure](#file-structure)
3. [Build System](#build-system)
4. [SCSS Architecture](#scss-architecture)
5. [JavaScript Implementation](#javascript-implementation)
6. [Drupal Integration](#drupal-integration)
7. [Template Patterns](#template-patterns)
8. [Migration Changes (Bootstrap 4 → 5)](#migration-changes-bootstrap-4--5)
9. [Reusable Patterns](#reusable-patterns)
10. [Testing Approach](#testing-approach)
11. [Best Practices](#best-practices)

---

## Overview

**Module:** `lb_accordion`
**Location:** `/docroot/modules/contrib/lb_accordion/`
**Purpose:** Layout Builder accordion component using Bootstrap 5
**Bootstrap Version:** 5.3.3
**Node Version:** Specified in `.nvmrc`

### Key Features

- Uses Bootstrap 5.3.3 Accordion component
- Webpack-based build system
- PurgeCSS for CSS optimization
- Lean Bootstrap imports (only required components)
- Drupal behaviors for dynamic content
- Schema.org FAQPage structured data support
- Responsive design with custom breakpoints

---

## File Structure

```
lb_accordion/
├── .git/                          # Git repository
├── .gitignore                     # Git ignore patterns
├── .nvmrc                         # Node version specification
├── assets/
│   ├── js/
│   │   └── lb_accordion.js       # JavaScript entry point
│   ├── scss/
│   │   └── lb_accordion.scss     # SCSS entry point
│   ├── svg/
│   │   ├── chevron-up.svg        # Custom chevron icons
│   │   └── chevron-down.svg
│   └── dist/
│       ├── lb_accordion.css      # Built CSS (committed)
│       └── lb_accordion.js       # Built JS (committed)
├── config/
│   ├── optional/                  # Optional configuration
│   └── outdated/                  # Migration configs
├── templates/
│   └── block--lb-accordion.html.twig  # Main template
├── composer.json                  # Composer dependencies
├── lb_accordion.info.yml          # Module metadata
├── lb_accordion.install           # Install/update hooks
├── lb_accordion.libraries.yml     # Drupal library definition
├── lb_accordion.module            # Module hooks
├── package.json                   # npm dependencies
├── webpack.config.js              # Build configuration
└── README.md                      # Documentation
```

### Key Characteristics

1. **Self-contained**: All assets within module directory
2. **Build artifacts committed**: `dist/` folder is committed to git
3. **Lean imports**: Only imports required Bootstrap components
4. **Optimized**: Uses PurgeCSS to remove unused styles
5. **Documented**: Clear README with build instructions

---

## Build System

### package.json

```json
{
  "name": "lb-accordion",
  "description": "LB Accordion styles.",
  "author": "YMCA Website Services",
  "private": true,
  "version": "1.0.0",
  "scripts": {
    "watch": "webpack --watch",
    "build": "webpack build --mode=production"
  },
  "dependencies": {
    "@popperjs/core": "^2.11.8",
    "bootstrap": "^5.3.3",
    "breakpoint-sass": "^3.0.0",
    "node-sass": "^8.0.0",
    "nodemon": "^3.1.0",
    "postcss-cli": "^11.0.0",
    "purgecss": "^6.0.0"
  },
  "devDependencies": {
    "autoprefixer": "^10.4.19",
    "css-loader": "^7.1.1",
    "mini-css-extract-plugin": "^2.8.1",
    "postcss-loader": "^8.1.1",
    "purgecss-webpack-plugin": "^6.0.0",
    "sass": "^1.75.0",
    "sass-loader": "^14.2.0",
    "style-loader": "^4.0.0",
    "webpack": "^5.91.0",
    "webpack-cli": "^5.1.4",
    "webpack-dev-server": "^5.0.4"
  }
}
```

#### Key Dependencies

**Production:**
- `bootstrap@^5.3.3` - Bootstrap 5 framework
- `@popperjs/core@^2.11.8` - Required for dropdowns/tooltips (though not used in accordion)
- `breakpoint-sass@^3.0.0` - SCSS breakpoint mixins

**Development:**
- `webpack` - Module bundler
- `sass` + `sass-loader` - SCSS compilation
- `css-loader` - CSS processing
- `mini-css-extract-plugin` - CSS extraction
- `postcss-loader` + `autoprefixer` - CSS post-processing
- `purgecss-webpack-plugin` - Unused CSS removal

### webpack.config.js

```javascript
'use strict'

const path = require('path');
const glob = require("glob");
const autoprefixer = require('autoprefixer');
const miniCssExtractPlugin = require('mini-css-extract-plugin');
const { PurgeCSSPlugin } = require("purgecss-webpack-plugin");

const PATHS = {
  src: path.join(__dirname, "templates"),
};

module.exports = {
  mode: 'development',
  watchOptions: {
    // Set polling so watch works in docker.
    poll: 1000,
  },
  entry: ['./assets/js/lb_accordion.js', './assets/scss/lb_accordion.scss'],
  output: {
    filename: 'lb_accordion.js',
    path: path.resolve(__dirname, 'assets/dist')
  },
  plugins: [
    // Output CSS to its own file.
    new miniCssExtractPlugin({
      filename: 'lb_accordion.css',
    }),
    // Purge CSS of any unused styles.
    new PurgeCSSPlugin({
      paths: glob.sync(`${PATHS.src}/**/*`, { nodir: true }),
    }),
  ],
  module: {
    rules: [
      {
        test: /\.(scss)$/,
        use: [
          {
            // Extracts CSS for each JS file that includes CSS
            loader: miniCssExtractPlugin.loader
          },
          {
            // Interprets `@import` and `url()` like `import/require()` and will resolve them
            loader: 'css-loader'
          },
          {
            // Loader for webpack to process CSS with PostCSS
            loader: 'postcss-loader',
            options: {
              postcssOptions: {
                plugins: [
                  autoprefixer
                ]
              }
            }
          },
          {
            // Loads a SASS/SCSS file and compiles it to CSS
            loader: 'sass-loader'
          }
        ]
      }
    ]
  }
}
```

#### Webpack Patterns

1. **Dual Entry Point**: JS and SCSS in same entry array
2. **Single Output**: Both compile to `dist/` directory
3. **PurgeCSS Scans Templates**: Looks at `templates/` to determine used classes
4. **Autoprefixer**: Automatically adds vendor prefixes
5. **Production Mode**: Set via `--mode=production` in npm script
6. **Docker Support**: Polling enabled for file watching in containers

### .nvmrc

```
18
```

Specifies Node.js version 18 for consistent builds.

### Build Commands

```bash
# Install dependencies
npm install

# Development build (watch mode)
npm run watch

# Production build (optimized)
npm run build
```

---

## SCSS Architecture

### assets/scss/lb_accordion.scss

```scss
// 1. Include functions first (so you can manipulate colors, SVGs, calc, etc)
@import "bootstrap/scss/functions";

// 2. Include any default variable overrides here
// (none in this case)

// 3. Include remainder of required Bootstrap stylesheets
@import "bootstrap/scss/variables";
@import "bootstrap/scss/variables-dark";

// 4. Include any default map overrides here
// (none in this case)

// 5. Include remainder of required parts
@import "bootstrap/scss/maps";
@import "bootstrap/scss/mixins";
//@import "bootstrap/scss/root";  // Commented out to reduce CSS

// 6. Optionally include any other parts as needed
@import "bootstrap/scss/buttons";
@import "bootstrap/scss/utilities";
@import "bootstrap/scss/grid";
@import "bootstrap/scss/accordion";
@import "bootstrap/scss/transitions";

// 7. Optionally include utilities API last to generate classes based on the Sass map in `_utilities.scss`
@import "bootstrap/scss/utilities/api";

// Custom component styles below...
```

### SCSS Patterns

#### 1. Lean Imports

**Only imports required Bootstrap components:**
- functions (required)
- variables (required)
- variables-dark (required for color modes)
- maps (required)
- mixins (required)
- buttons (for .btn styles)
- utilities (for utility classes)
- grid (for layout)
- accordion (for accordion component)
- transitions (for animations)
- utilities/api (for generating utilities)

**Does NOT import:**
- root (commented out to save bytes)
- reboot (global resets - assumes theme handles this)
- type (typography)
- images
- containers
- tables
- forms
- other components

**Result:** Minimal CSS bundle with only what's needed.

#### 2. Container/Grid Mixins

```scss
.block-accordion {
  @include make-container();

  &-row {
    @include make-row();
  }

  &-title {
    @include make-col-ready();
    @include media-breakpoint-up(lg) {
      @include make-col(4);
    }
    @extend .mb-4;
  }

  .accordion {
    @include make-col-ready();
    @extend .d-grid;
    @extend .gap-3;

    @include media-breakpoint-up('lg'){
      @include make-col(12);

      &.with-label {
        @include make-col(8);
      }
    }
  }
}
```

**Pattern:**
- Uses Bootstrap mixins for grid layout
- Avoids utility classes in markup (semantic CSS)
- Responsive breakpoints with `media-breakpoint-up()`
- Some utility classes via `@extend` (`.mb-4`, `.d-grid`, `.gap-3`)

#### 3. Custom Properties Integration

```scss
.accordion-item {
  .card-header {
    border-radius: var(--wsBorderRadius, unset);
    border: 2px solid var(--wsSecondaryColor, black);
    background: var(--ylb-color-white);

    &.active, &:hover {
      background: var(--wsPrimaryColor, var(--gray-400));
      border-color: transparent;

      .accordion-button {
        color: var(--white);
      }
    }
  }
}
```

**Pattern:**
- Uses CSS custom properties for theme integration
- Provides fallback values
- Allows theme-level color customization
- Namespaced variables (`--ws*`, `--ylb-*`)

#### 4. Utility Extensions

```scss
.accordion-header {
  @extend .mb-0;
  @extend .d-grid;
}

.accordion-button {
  @extend .btn;
  @extend .btn-link;
  @extend .text-start;
}

.card-body {
  @extend .px-3;
  @extend .py-4;
}
```

**Pattern:**
- Uses `@extend` to apply Bootstrap utility classes
- Keeps HTML clean and semantic
- Reduces template complexity

#### 5. Custom Icon Handling

```scss
.chevron {
  width: 12px;
  height: 8px;
  position: absolute;
  top: 16px;
  right: 0.5em;
  transform: rotate(180deg);

  &.chevron-up {
    mask: url("../svg/chevron-up.svg");
    background: white;
  }
  &.chevron-down {
    mask: url("../svg/chevron-down.svg");
    background: black;
  }
}

.accordion-button.btn {
  i.chevron {
    display: none;
    float: right;
  }
  &[aria-expanded="false"] {
    i.chevron-down {
      display: inline;
    }
  }
  &[aria-expanded="true"] {
    i.chevron-up {
      display: inline;
    }
  }
}
```

**Pattern:**
- Uses CSS `mask` for colorizable SVG icons
- Toggles icon based on `aria-expanded` attribute
- No JavaScript required for icon switching
- Accessible (doesn't interfere with screen readers)

---

## JavaScript Implementation

### assets/js/lb_accordion.js

```javascript
// Import Bootstrap Collapse JS. Will get triggered automagically.
import Collapse from "bootstrap/js/dist/collapse";

(function ($, Drupal){
  // Layout Builder - Accordion behavior
  Drupal.behaviors.lbAccordion = {
    attach: function (context) {
      $(document)
          .on('show.bs.collapse', '.accordion-item', function(e) {
            $('.card-header', this).addClass('active');
          })
          .on('hide.bs.collapse', '.accordion-item', function(e) {
            $('.card-header', this).removeClass('active');
          });
    }
  };
})(jQuery, Drupal);
```

### JavaScript Patterns

#### 1. Lean Import

```javascript
import Collapse from "bootstrap/js/dist/collapse";
```

**Pattern:**
- Only imports the specific component needed
- Not `import 'bootstrap'` (would be huge)
- Tree-shaking friendly
- Reduces bundle size

#### 2. Auto-Initialization

Bootstrap 5's Collapse component auto-initializes elements with `data-bs-toggle="collapse"` attribute. No manual initialization needed:

```javascript
// NOT needed:
// const collapses = document.querySelectorAll('.collapse');
// collapses.forEach(el => new Collapse(el));

// Bootstrap 5 does this automatically
```

#### 3. Drupal Behaviors Pattern

```javascript
(function ($, Drupal){
  Drupal.behaviors.lbAccordion = {
    attach: function (context) {
      // Code here runs on page load and after AJAX
    }
  };
})(jQuery, Drupal);
```

**Why this pattern:**
- Works with Drupal's AJAX system
- Re-runs when new content is added via AJAX
- Integrates with Layout Builder preview
- Standard Drupal pattern

#### 4. Event Delegation

```javascript
$(document)
  .on('show.bs.collapse', '.accordion-item', function(e) {
    $('.card-header', this).addClass('active');
  })
  .on('hide.bs.collapse', '.accordion-item', function(e) {
    $('.card-header', this).removeClass('active');
  });
```

**Pattern:**
- Event listener on `document` (highest level)
- Delegates to `.accordion-item` elements
- Works for dynamically added accordions
- No need to re-bind after AJAX

#### 5. Bootstrap Events

```javascript
'show.bs.collapse'  // Fires when collapse starts opening
'hide.bs.collapse'  // Fires when collapse starts closing
```

Other available events:
- `shown.bs.collapse` - After fully opened
- `hidden.bs.collapse` - After fully closed

**Pattern:**
- Uses Bootstrap's native events
- Adds custom behavior (active class toggle)
- Doesn't interfere with Bootstrap functionality

---

## Drupal Integration

### lb_accordion.info.yml

```yaml
name: 'Y Layout Builder - Accordion Block'
description: 'Helper module for the custom "Accordion" block type.'
type: module
core_version_requirement: ^9 || ^10 || ^11
package: 'YMCA Website Services'
dependencies:
  - drupal:paragraphs
  - drupal:block_content
  - y_lb
```

**Pattern:**
- Multi-version support (Drupal 9, 10, 11)
- Clear dependencies
- Descriptive name and package

### lb_accordion.libraries.yml

```yaml
lb_accordion:
  version: 1.9
  css:
    theme:
      assets/dist/lb_accordion.css: { preprocess: true }
  js:
    assets/dist/lb_accordion.js: { minified: true }
  dependencies:
    - core/jquery
    - core/drupal
```

**Patterns:**

1. **Version Number**: Bumped with each change (forces cache clear)
2. **Preprocess CSS**: Allows aggregation
3. **Minified JS**: Indicates JS is already minified
4. **Dependencies**: Ensures jQuery and Drupal are loaded first

### lb_accordion.module

Key hooks:

#### 1. hook_theme()

```php
function lb_accordion_theme($existing, $type, $theme, $path) {
  return [
    'block__lb_accordion' => [
      'base hook' => 'block',
      'template' => 'block--lb-accordion',
    ]
  ];
}
```

**Pattern:**
- Registers custom template
- Uses base hook for inheritance
- Template name matches file

#### 2. hook_block_view_inline_block_alter()

```php
function lb_accordion_block_view_inline_block_alter(array &$build, \Drupal\Core\Block\BlockPluginInterface $block)
{
  if ($block->getPluginId() == 'inline_block:lb_accordion' && !$build["#in_preview"]) {
    $is_faq = $build["content"]["#block_content"]->field_is_faq->value;

    if (!$is_faq) { return; }

    // Build FAQ schema...
  }
}
```

**Pattern:**
- Only alters specific block type
- Checks for preview mode (don't add schema in preview)
- Conditional feature (FAQPage schema)
- Adds structured data to page head

#### 3. hook_preprocess_block__lb_accordion()

```php
function lb_accordion_preprocess_block__lb_accordion(&$variables) {
  $variables['block_content'] = $variables['elements']['content']['#block_content'];
}
```

**Pattern:**
- Makes block content entity available in template
- Simplifies template code
- Standard Drupal preprocessing

#### 4. hook_ENTITY_TYPE_presave()

```php
function lb_accordion_block_content_presave(EntityInterface $block) {
  if ($block->bundle() === 'accordion_item') {
     $block->setInfo($block->get('field_title')->value);
  }
}
```

**Pattern:**
- Auto-generates block label from field
- Improves admin UX
- Runs before save

---

## Template Patterns

### templates/block--lb-accordion.html.twig

```twig
{% set classes = [
  'block',
  'block--spacing',
  'block-' ~ configuration.provider|clean_class,
  'block-' ~ plugin_id|clean_class,
  'block-accordion',
] %}

{% set accordion_id = 'accordion-' ~ configuration['block_revision_id'] %}

{{ attach_library('lb_accordion/lb_accordion') }}

<div{{ attributes.addClass(classes).setAttribute('id', plugin_id|clean_class ~ configuration['block_revision_id']) }}>
  <div class="block-accordion-row">
    <!-- Title section -->
    {% if label or block_content.field_section_subtitle %}
      <div class="block-accordion-title">
        {% if label %}
          <h3{{ title_attributes }}>{{ label }}</h3>
        {% endif %}
        {% if block_content.field_section_subtitle.value %}
          <p class="subtitle">{{ block_content.field_section_subtitle.value }}</p>
        {% endif %}
      </div>
    {% endif %}

    <!-- Accordion items -->
    <div class="accordion {{ label ? "with-label" }}" id="{{ accordion_id }}">
      {% for key, item in content.field_block_item|default([])|filter((item, key) => key|first != '#') %}
        {% set safe_hash = configuration['block_revision_id'] ~ '--' ~ loop.index %}

        <div class="accordion-item">
          <div class="card-header {{ loop.index == 1 ? 'active' : ''}}" id="heading-{{ safe_hash }}">
            <h4 class="accordion-header">
              <button
                class="accordion-button"
                type="button"
                data-bs-toggle="collapse"
                data-bs-target="#collapse-{{ safe_hash }}"
                aria-expanded="{{ loop.index == 1 ? 'true' : 'false'}}"
                aria-controls="collapse-{{ safe_hash }}">
                {{ item.field_title|render }}
                <i class="chevron chevron-down" aria-hidden="true"></i>
                <i class="chevron chevron-up" aria-hidden="true"></i>
              </button>
            </h4>
          </div>

          <div
            id="collapse-{{ safe_hash }}"
            class="accordion-collapse collapse {{ loop.index == 1 ? 'show' : ''}}"
            aria-labelledby="heading-{{ safe_hash }}"
            data-bs-parent="#{{ accordion_id }}">
            <div class="card-body">
              {{ item.body|render }}
            </div>
          </div>
        </div>
      {% endfor %}
    </div>
  </div>
</div>
```

### Template Patterns

#### 1. Library Attachment

```twig
{{ attach_library('lb_accordion/lb_accordion') }}
```

**Pattern:**
- Attaches library in template (always loads with component)
- Alternative: attach in module or theme (conditional loading)

#### 2. Unique IDs Generation

```twig
{% set accordion_id = 'accordion-' ~ configuration['block_revision_id'] %}
{% set safe_hash = configuration['block_revision_id'] ~ '--' ~ loop.index %}
```

**Pattern:**
- Uses block revision ID for uniqueness
- Multiple accordions on same page won't conflict
- IDs are stable across renders

#### 3. Bootstrap 5 Data Attributes

```twig
data-bs-toggle="collapse"
data-bs-target="#collapse-{{ safe_hash }}"
data-bs-parent="#{{ accordion_id }}"
```

**Pattern:**
- All use `data-bs-*` prefix (Bootstrap 5)
- Bootstrap 4 used `data-*` (would break)
- `data-bs-parent` enables accordion behavior (only one open at a time)

#### 4. ARIA Attributes

```twig
aria-expanded="{{ loop.index == 1 ? 'true' : 'false'}}"
aria-controls="collapse-{{ safe_hash }}"
aria-labelledby="heading-{{ safe_hash }}"
aria-hidden="true"
```

**Pattern:**
- First item expanded by default (`loop.index == 1`)
- Proper ARIA relationships
- Icons hidden from screen readers
- Accessible by default

#### 5. BEM-like Naming

```twig
.block-accordion
.block-accordion-row
.block-accordion-title
```

**Pattern:**
- Component name as prefix
- Subcomponent names with dashes
- Not strict BEM, but similar concept
- Avoids conflicts with other modules

#### 6. Conditional Classes

```twig
<div class="accordion {{ label ? "with-label" }}">
<div class="card-header {{ loop.index == 1 ? 'active' : ''}}">
<div class="accordion-collapse collapse {{ loop.index == 1 ? 'show' : ''}}">
```

**Pattern:**
- Conditional layout class (`with-label`)
- First item has different state (active/show)
- JavaScript adds/removes `active` class dynamically

#### 7. Render Array Filtering

```twig
{% for key, item in content.field_block_item|default([])|filter((item, key) => key|first != '#') %}
```

**Pattern:**
- Filters out Drupal render array metadata (keys starting with `#`)
- Uses `|default([])` to handle empty fields
- Standard Drupal Twig pattern

---

## Migration Changes (Bootstrap 4 → 5)

### What Changed from Bootstrap 4

If `lb_accordion` was previously using Bootstrap 4, here's what would have changed:

#### 1. Data Attributes (Templates)

```diff
- data-toggle="collapse"
+ data-bs-toggle="collapse"

- data-target="#collapse-1"
+ data-bs-target="#collapse-1"

- data-parent="#accordion"
+ data-bs-parent="#accordion"
```

**Find & Replace:**
- `data-toggle` → `data-bs-toggle`
- `data-target` → `data-bs-target`
- `data-parent` → `data-bs-parent`

#### 2. JavaScript Import (JS)

```diff
- import 'bootstrap';
+ import Collapse from "bootstrap/js/dist/collapse";
```

**Pattern:**
- Lean imports instead of entire library
- Tree-shaking friendly

#### 3. SCSS Imports (SCSS)

```diff
- @import "bootstrap/scss/bootstrap";
+ @import "bootstrap/scss/functions";
+ @import "bootstrap/scss/variables";
+ @import "bootstrap/scss/variables-dark";  // NEW
+ @import "bootstrap/scss/maps";
+ @import "bootstrap/scss/mixins";
+ @import "bootstrap/scss/accordion";
+ // ... only needed components
+ @import "bootstrap/scss/utilities/api";
```

**Pattern:**
- Modular imports
- Only include what's needed
- New: `variables-dark` for color modes

#### 4. Close Button (if used)

```diff
- <button class="close">×</button>
+ <button class="btn-close"></button>
```

Not used in accordion, but pattern for other components.

#### 5. npm Dependencies

```diff
{
  "dependencies": {
-   "bootstrap": "^4.6.0",
+   "bootstrap": "^5.3.3",
+   "@popperjs/core": "^2.11.8"
  }
}
```

#### 6. Webpack Config

No major changes needed. PurgeCSS integration is the same.

---

## Reusable Patterns

### For Other Modules Migrating to Bootstrap 5

#### 1. Build System Setup

**Copy these files as starting point:**
```
package.json        → Update name and dependencies for your module
webpack.config.js   → Update entry/output paths for your module
.nvmrc             → Copy as-is
```

**Installation:**
```bash
npm install bootstrap@^5.3.3 @popperjs/core@^2.11.8 \
  sass sass-loader css-loader style-loader \
  mini-css-extract-plugin postcss-loader autoprefixer \
  purgecss-webpack-plugin webpack webpack-cli
```

#### 2. SCSS Structure

**Start with this template:**
```scss
// 1. Functions
@import "bootstrap/scss/functions";

// 2. Variable overrides (optional)
// $primary: #your-color;

// 3. Variables
@import "bootstrap/scss/variables";
@import "bootstrap/scss/variables-dark";

// 4. Maps and mixins
@import "bootstrap/scss/maps";
@import "bootstrap/scss/mixins";

// 5. Components (import only what you need)
@import "bootstrap/scss/buttons";
@import "bootstrap/scss/utilities";
@import "bootstrap/scss/grid";
// Add others as needed

// 6. Utilities API
@import "bootstrap/scss/utilities/api";

// 7. Your custom styles
.your-component {
  // ...
}
```

#### 3. JavaScript Structure

**Pattern to follow:**
```javascript
// Import only needed Bootstrap components
import ComponentName from "bootstrap/js/dist/component-name";

(function ($, Drupal, bootstrap) {
  'use strict';

  Drupal.behaviors.yourModuleName = {
    attach: function (context, settings) {
      // Use event delegation for dynamic content
      $(document)
        .on('show.bs.component', '.your-selector', function(e) {
          // Handle show event
        })
        .on('hide.bs.component', '.your-selector', function(e) {
          // Handle hide event
        });

      // OR manual initialization with .once()
      $('.your-component', context).once('yourModuleName').each(function() {
        new bootstrap.ComponentName(this);
      });
    }
  };
})(jQuery, Drupal, window.bootstrap || {});
```

#### 4. Template Data Attributes

**Always use `data-bs-*` prefix:**
```twig
<button
  data-bs-toggle="collapse"
  data-bs-target="#target"
  aria-expanded="false">
</button>

<div
  id="target"
  class="collapse"
  data-bs-parent="#parent">
</div>
```

#### 5. Library Definition

```yaml
your_module:
  version: 1.0  # Increment with changes
  css:
    theme:
      assets/dist/your_module.css: { preprocess: true }
  js:
    assets/dist/your_module.js: { minified: true }
  dependencies:
    - core/jquery    # If using jQuery
    - core/drupal    # Always include for behaviors
```

#### 6. PurgeCSS Configuration

```javascript
// In webpack.config.js
const { PurgeCSSPlugin } = require("purgecss-webpack-plugin");

plugins: [
  new PurgeCSSPlugin({
    paths: glob.sync(`${PATHS.src}/**/*`, { nodir: true }),
    safelist: {
      standard: ['show', 'collapsing', 'fade', 'active'],
      deep: [/^your-component/, /^collapse/, /^modal/],
      greedy: [/^btn-/, /^bg-/, /^text-/]
    }
  })
]
```

---

## Testing Approach

### Manual Testing Checklist

Based on lb_accordion, test these scenarios:

1. **Visual Testing**
   - [ ] Desktop layout (1920x1080)
   - [ ] Laptop layout (1366x768)
   - [ ] Tablet layout (768x1024)
   - [ ] Mobile layout (375x667)
   - [ ] XXL breakpoint (1400px+)

2. **Interaction Testing**
   - [ ] Click first item (should expand)
   - [ ] Click second item (first should collapse)
   - [ ] Click same item twice (should toggle)
   - [ ] Active state styling appears
   - [ ] Chevron icon rotates correctly

3. **Accessibility Testing**
   - [ ] Tab through buttons
   - [ ] Enter/Space activates buttons
   - [ ] Screen reader announces correctly
   - [ ] ARIA attributes update correctly

4. **Drupal Integration**
   - [ ] Works in Layout Builder edit mode
   - [ ] Works after saving Layout Builder
   - [ ] Works on content view page
   - [ ] Survives cache clear
   - [ ] Works with AJAX operations

5. **Multiple Instances**
   - [ ] Add 2+ accordions to same page
   - [ ] Each works independently
   - [ ] IDs don't conflict
   - [ ] JavaScript works for all

6. **Browser Testing**
   - [ ] Chrome (latest)
   - [ ] Firefox (latest)
   - [ ] Safari (latest)
   - [ ] Edge (latest)
   - [ ] Mobile Safari (iOS)
   - [ ] Chrome Mobile (Android)

### Automated Testing

Consider adding:

```javascript
// Behat test example
@javascript
Scenario: Accordion expands and collapses
  Given I am on "/node/123"
  When I click ".accordion-button:first-child"
  Then I should see ".accordion-collapse.show"
  When I click ".accordion-button:nth-child(2)"
  Then I should not see ".accordion-collapse:first-child.show"
  And I should see ".accordion-collapse:nth-child(2).show"
```

---

## Best Practices

### Based on lb_accordion Implementation

1. **Commit Built Assets**
   - Commit `dist/` folder to git
   - Don't rely on build during deployment
   - Ensures assets are always available

2. **Version Library Files**
   - Bump version in `.libraries.yml` with each change
   - Forces browser cache clear
   - Critical for seeing changes

3. **Use Lean Imports**
   - Import only needed Bootstrap components
   - Reduces bundle size significantly
   - Better performance

4. **Use PurgeCSS**
   - Removes unused Bootstrap CSS
   - Scans templates to determine usage
   - Add safelist for JavaScript-added classes

5. **Document Build Process**
   - Clear README with build instructions
   - Specify Node version in `.nvmrc`
   - List all npm scripts

6. **Use Drupal Behaviors**
   - Always wrap JS in Drupal.behaviors
   - Use `.once()` to prevent double-initialization
   - Works with AJAX and Layout Builder

7. **Event Delegation**
   - Attach event listeners to parent element
   - Works for dynamically added content
   - More performant

8. **Semantic CSS**
   - Use Bootstrap mixins in SCSS
   - Keep markup clean
   - Avoid utility class soup in templates

9. **Unique IDs**
   - Use block revision ID or similar
   - Prevents conflicts with multiple instances
   - Stable across renders

10. **Accessibility First**
    - Use proper ARIA attributes
    - Test with keyboard
    - Test with screen reader
    - Hide decorative elements from assistive tech

---

## Key Takeaways

### What Makes lb_accordion a Good Reference

1. **Complete**: Has all pieces (build, templates, JS, CSS, Drupal)
2. **Optimized**: Uses lean imports and PurgeCSS
3. **Modern**: Uses Bootstrap 5 best practices
4. **Documented**: Clear README and inline comments
5. **Tested**: In production use across YMCA sites
6. **Maintained**: Part of active YMCA WS distribution

### Apply These Patterns To

- `lb_banner`
- `lb_card`
- `lb_carousel`
- `lb_modal`
- Any custom Bootstrap component module

### Different Patterns Needed For

- **Themes**: May want single build for all Bootstrap components
- **Base modules**: May need to expose Bootstrap globally
- **Non-Layout-Builder**: Different template structure

---

## Migration Workflow

### Recommended Steps for Migrating Another Module

1. **Analyze** (lb_accordion as reference)
   - Compare current module to lb_accordion
   - List differences
   - Identify Bootstrap 4 usage

2. **Setup Build System**
   - Copy package.json (modify for your module)
   - Copy webpack.config.js (update paths)
   - Copy .nvmrc
   - Run `npm install`

3. **Update Templates**
   - Find/replace data attributes
   - Update classes
   - Test markup

4. **Update SCSS**
   - Convert to modular imports
   - Import only needed components
   - Test styles

5. **Update JavaScript**
   - Import specific components
   - Update initialization if needed
   - Test functionality

6. **Build and Test**
   - Run `npm run build`
   - Test in Drupal
   - Test all scenarios

7. **Document**
   - Update README
   - Document breaking changes
   - Update version in .libraries.yml

8. **Deploy**
   - Commit built assets
   - Export configuration
   - Test on staging

---

## Additional Resources

- **lb_accordion README**: `/docroot/modules/contrib/lb_accordion/README.md`
- **Bootstrap 5 Accordion Docs**: https://getbootstrap.com/docs/5.3/components/accordion/
- **Bootstrap 5 Migration Guide**: https://getbootstrap.com/docs/5.3/migration/
- **Webpack Documentation**: https://webpack.js.org/
- **PurgeCSS Documentation**: https://purgecss.com/

---

*Last Updated: 2025-10-17*
*Based on lb_accordion version 1.9*
*For YMCA Website Services Bootstrap 5 Migration*
