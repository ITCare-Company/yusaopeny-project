# Sprint 18: Activity Finder Preparation & Component Library

**Phase:** [Phase 5 - Activity Finder](../phases/PHASE_5_ACTIVITY_FINDER.md)
**Resources:** 1 Frontend Developer (Vue.js experience required)
**Status:** Not Started

---

## Sprint Goal

Prepare for Activity Finder migration by auditing BootstrapVue usage, creating custom Bootstrap 5 Vue component library, and isolating Camp Finder. This foundational work enables successful migration of all 3 Vue.js applications.

---

## Focus Areas

### 1. BootstrapVue Audit
- Audit all BootstrapVue components used across 3 apps
- Document component usage patterns
- Identify migration challenges

### 2. Custom Component Library
- Create Bootstrap 5 Vue component library
- Replace BootstrapVue functionality
- Test components in isolation

### 3. Camp Finder Isolation
- Isolate Camp Finder with scoped Bootstrap 4 CSS
- Same approach as Activity Finder (Phase 1)
- Prepare for Sprint 21 migration

---

## Tasks

### Task 1: BootstrapVue Component Audit
**Owner:** Developer
**Priority:** CRITICAL

**Actions:**

**1.1 Audit Activity Finder 4 (openy_activity_finder):**
```bash
cd docroot/modules/contrib/yusaopeny_activity_finder/openy_af4_vue_app

# Find all BootstrapVue components
grep -r "b-" src/
grep -r "BButton\|BCard\|BModal" src/
grep -r "bootstrap-vue" package.json

# List all Vue component files
find src/ -name "*.vue"
```

**1.2 Audit Activity Finder (openy_af_vue_app):**
```bash
cd docroot/modules/contrib/yusaopeny_activity_finder/openy_af_vue_app

# Same audit as above
grep -r "b-" src/
grep -r "bootstrap-vue" .
```

**1.3 Audit Camp Finder (openy_cf_vue_app):**
```bash
cd docroot/modules/contrib/yusaopeny_activity_finder/openy_cf_vue_app

# Same audit as above
grep -r "b-" src/
grep -r "bootstrap-vue" .
```

**1.4 Create comprehensive component inventory:**

**Common BootstrapVue Components (estimated):**
- `b-button` - Button component
- `b-button-group` - Button group
- `b-card`, `b-card-body`, `b-card-title` - Card components
- `b-form`, `b-form-input`, `b-form-select` - Form components
- `b-form-checkbox`, `b-form-radio` - Form input components
- `b-form-group` - Form group wrapper
- `b-modal` - Modal dialog
- `b-dropdown`, `b-dropdown-item` - Dropdown menus
- `b-collapse` - Collapse/expand component
- `b-badge` - Badge component
- `b-spinner` - Loading spinner
- `b-alert` - Alert messages
- `b-table` (maybe) - Data table
- `b-pagination` (maybe) - Pagination

**1.5 Document usage patterns:**
```javascript
// Example: b-button usage patterns
<b-button variant="primary" @click="handleClick">
  Click Me
</b-button>

// Example: b-modal usage patterns
<b-modal v-model="showModal" title="Details">
  <p>Modal content here</p>
</b-modal>

// Example: b-form-input usage patterns
<b-form-input
  v-model="searchTerm"
  placeholder="Search..."
  @input="onSearch"
/>
```

**1.6 Identify migration challenges:**
- Components with complex logic
- Components using BootstrapVue-specific APIs
- Components with custom styling
- Components with accessibility features

**Deliverable:** Create `docs/bootstrap-5-migration/reference/BOOTSTRAPVUE_AUDIT.md`

**Acceptance Criteria:**
- [ ] All BootstrapVue components documented
- [ ] Usage patterns documented
- [ ] Migration challenges identified
- [ ] Component inventory complete

---

### Task 2: Create Custom Bootstrap 5 Component Library
**Owner:** Developer
**Priority:** CRITICAL

**Actions:**

**2.1 Create component library structure:**
```bash
# Create shared component library
mkdir -p docroot/modules/contrib/yusaopeny_activity_finder/shared/components

cd docroot/modules/contrib/yusaopeny_activity_finder/shared

# Initialize package.json
npm init -y

# Install Bootstrap 5
npm install bootstrap@5.3.3 @popperjs/core
```

**2.2 Create Button component (b-button replacement):**
```vue
<!-- components/BsButton.vue -->
<template>
  <button
    :class="buttonClasses"
    :type="type"
    :disabled="disabled"
    @click="$emit('click', $event)"
  >
    <slot></slot>
  </button>
</template>

<script>
export default {
  name: 'BsButton',
  props: {
    variant: {
      type: String,
      default: 'primary'
    },
    size: {
      type: String,
      default: ''
    },
    disabled: Boolean,
    type: {
      type: String,
      default: 'button'
    },
    block: Boolean
  },
  computed: {
    buttonClasses() {
      const classes = ['btn', `btn-${this.variant}`];
      if (this.size) classes.push(`btn-${this.size}`);
      if (this.block) classes.push('w-100');
      return classes;
    }
  }
}
</script>
```

**2.3 Create Card components (b-card replacement):**
```vue
<!-- components/BsCard.vue -->
<template>
  <div class="card">
    <slot></slot>
  </div>
</template>

<!-- components/BsCardBody.vue -->
<template>
  <div class="card-body">
    <slot></slot>
  </div>
</template>

<!-- components/BsCardTitle.vue -->
<template>
  <h5 class="card-title">
    <slot></slot>
  </h5>
</template>
```

**2.4 Create Form components (b-form-* replacements):**
```vue
<!-- components/BsFormInput.vue -->
<template>
  <input
    :type="type"
    :class="inputClasses"
    :value="value"
    :placeholder="placeholder"
    :disabled="disabled"
    @input="$emit('input', $event.target.value)"
    @change="$emit('change', $event.target.value)"
  >
</template>

<script>
export default {
  name: 'BsFormInput',
  props: {
    value: [String, Number],
    type: {
      type: String,
      default: 'text'
    },
    placeholder: String,
    disabled: Boolean,
    size: String,
    state: Boolean // for validation
  },
  computed: {
    inputClasses() {
      const classes = ['form-control'];
      if (this.size) classes.push(`form-control-${this.size}`);
      if (this.state === false) classes.push('is-invalid');
      if (this.state === true) classes.push('is-valid');
      return classes;
    }
  }
}
</script>

<!-- components/BsFormSelect.vue -->
<template>
  <select
    class="form-select"
    :value="value"
    :disabled="disabled"
    @change="$emit('input', $event.target.value)"
  >
    <slot></slot>
  </select>
</template>

<!-- components/BsFormCheckbox.vue -->
<template>
  <div class="form-check">
    <input
      type="checkbox"
      class="form-check-input"
      :id="id"
      :checked="checked"
      @change="$emit('input', $event.target.checked)"
    >
    <label class="form-check-label" :for="id">
      <slot></slot>
    </label>
  </div>
</template>
```

**2.5 Create Modal component (b-modal replacement):**
```vue
<!-- components/BsModal.vue -->
<template>
  <teleport to="body">
    <div v-if="modelValue" class="modal-backdrop fade show" @click="hide"></div>
    <div
      v-if="modelValue"
      class="modal fade show"
      style="display: block;"
      tabindex="-1"
      role="dialog"
      aria-modal="true"
    >
      <div class="modal-dialog" role="document">
        <div class="modal-content">
          <div class="modal-header">
            <h5 class="modal-title">{{ title }}</h5>
            <button
              type="button"
              class="btn-close"
              @click="hide"
              aria-label="Close"
            ></button>
          </div>
          <div class="modal-body">
            <slot></slot>
          </div>
          <div v-if="$slots.footer" class="modal-footer">
            <slot name="footer"></slot>
          </div>
        </div>
      </div>
    </div>
  </teleport>
</template>

<script>
export default {
  name: 'BsModal',
  props: {
    modelValue: Boolean,
    title: String
  },
  methods: {
    hide() {
      this.$emit('update:modelValue', false);
    }
  },
  watch: {
    modelValue(newVal) {
      if (newVal) {
        document.body.classList.add('modal-open');
      } else {
        document.body.classList.remove('modal-open');
      }
    }
  }
}
</script>
```

**2.6 Create remaining components:**
- BsDropdown.vue
- BsCollapse.vue
- BsBadge.vue
- BsSpinner.vue
- BsAlert.vue
- BsButtonGroup.vue
- BsFormGroup.vue

**2.7 Create component index:**
```javascript
// components/index.js
export { default as BsButton } from './BsButton.vue';
export { default as BsCard } from './BsCard.vue';
export { default as BsCardBody } from './BsCardBody.vue';
export { default as BsCardTitle } from './BsCardTitle.vue';
export { default as BsFormInput } from './BsFormInput.vue';
export { default as BsFormSelect } from './BsFormSelect.vue';
export { default as BsFormCheckbox } from './BsFormCheckbox.vue';
export { default as BsModal } from './BsModal.vue';
export { default as BsDropdown } from './BsDropdown.vue';
export { default as BsCollapse } from './BsCollapse.vue';
export { default as BsBadge } from './BsBadge.vue';
export { default as BsSpinner } from './BsSpinner.vue';
export { default as BsAlert } from './BsAlert.vue';
// ... other components
```

**Deliverable:** Custom Bootstrap 5 Vue component library

**Acceptance Criteria:**
- [ ] All needed components created
- [ ] Components match BootstrapVue API where possible
- [ ] Components use Bootstrap 5 classes
- [ ] Components work with Vue 2
- [ ] Component library documented

---

### Task 3: Test Component Library in Isolation
**Owner:** Developer
**Priority:** HIGH

**Actions:**

**3.1 Create test application:**
```bash
cd docroot/modules/contrib/yusaopeny_activity_finder/shared

# Create test app
mkdir test-app
cd test-app

# Initialize Vue app
npm create vue@2 .
npm install
```

**3.2 Test each component:**
```vue
<!-- TestApp.vue -->
<template>
  <div id="app">
    <h1>Component Library Test</h1>

    <!-- Test BsButton -->
    <section>
      <h2>Buttons</h2>
      <bs-button variant="primary">Primary</bs-button>
      <bs-button variant="secondary">Secondary</bs-button>
      <bs-button variant="success">Success</bs-button>
      <bs-button size="lg">Large</bs-button>
      <bs-button size="sm">Small</bs-button>
      <bs-button disabled>Disabled</bs-button>
    </section>

    <!-- Test BsCard -->
    <section>
      <h2>Cards</h2>
      <bs-card>
        <bs-card-body>
          <bs-card-title>Card Title</bs-card-title>
          <p>Card content here</p>
        </bs-card-body>
      </bs-card>
    </section>

    <!-- Test BsModal -->
    <section>
      <h2>Modal</h2>
      <bs-button @click="showModal = true">Show Modal</bs-button>
      <bs-modal v-model="showModal" title="Test Modal">
        <p>Modal content here</p>
      </bs-modal>
    </section>

    <!-- Test other components -->
  </div>
</template>

<script>
import * as BsComponents from '../components';

export default {
  components: BsComponents,
  data() {
    return {
      showModal: false
    }
  }
}
</script>
```

**3.3 Test component functionality:**
- [ ] All components render correctly
- [ ] Component props work
- [ ] Component events work
- [ ] Component slots work
- [ ] Component styling correct (Bootstrap 5)

**3.4 Test accessibility:**
- [ ] Keyboard navigation works
- [ ] Focus management works
- [ ] ARIA attributes correct
- [ ] Screen reader compatible

**Deliverable:** Component library test results

**Acceptance Criteria:**
- [ ] All components tested
- [ ] All components functional
- [ ] Accessibility verified
- [ ] Test app demonstrates all components

---

### Task 4: Isolate Camp Finder (openy_cf_vue_app)
**Owner:** Developer
**Priority:** HIGH

**Actions:**

**4.1 Review Activity Finder isolation (Phase 1 reference):**
```bash
# Check how Activity Finder was isolated
cd docroot/modules/contrib/yusaopeny_activity_finder/openy_af4_vue_app

# Check webpack config for scoping
cat webpack.config.js

# Check SCSS scoping
find . -name "*.scss"
```

**4.2 Isolate Camp Finder with scoped Bootstrap 4:**
```bash
cd docroot/modules/contrib/yusaopeny_activity_finder/openy_cf_vue_app
```

**4.3 Update webpack.config.js for scoping:**
```javascript
// Add CSS scoping plugin
const MiniCssExtractPlugin = require('mini-css-extract-plugin');

module.exports = {
  // ... existing config

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
                  // Scope all CSS to .camp-finder-wrapper
                  require('postcss-prefix-selector')({
                    prefix: '.camp-finder-wrapper',
                    exclude: ['.camp-finder-wrapper']
                  })
                ]
              }
            }
          },
          'sass-loader'
        ]
      }
    ]
  }
};
```

**4.4 Update Camp Finder SCSS:**
```scss
// Keep Bootstrap 4 imports
@import "~bootstrap/scss/bootstrap";

// All Camp Finder styles will be scoped to .camp-finder-wrapper
.camp-finder {
  // Camp Finder styles
}
```

**4.5 Update Camp Finder template:**
```twig
{# Wrap Camp Finder in scoping div #}
<div class="camp-finder-wrapper">
  <div id="camp-finder-app"></div>
</div>
```

**4.6 Test Camp Finder isolation:**
- [ ] Camp Finder still uses Bootstrap 4
- [ ] Bootstrap 4 styles scoped to .camp-finder-wrapper
- [ ] No Bootstrap 4 styles leak out
- [ ] No Bootstrap 5 styles leak in
- [ ] Camp Finder functionality works

**Deliverable:** Isolated Camp Finder

**Acceptance Criteria:**
- [ ] Camp Finder isolated with scoped Bootstrap 4
- [ ] Isolation working correctly
- [ ] No style conflicts
- [ ] Camp Finder functional
- [ ] Ready for migration in Sprint 21

---

### Task 5: Documentation
**Owner:** Developer
**Priority:** MEDIUM

**Actions:**

**5.1 Document BootstrapVue audit:**
```bash
touch docs/bootstrap-5-migration/reference/BOOTSTRAPVUE_AUDIT.md
```

**Content:**
- All BootstrapVue components found
- Usage patterns
- Migration challenges
- Component frequency/importance

**5.2 Document component library:**
```bash
touch docs/bootstrap-5-migration/reference/CUSTOM_COMPONENT_LIBRARY.md
```

**Content:**
- Component library architecture
- How to use components
- Component API documentation
- Examples for each component
- Migration guide (BootstrapVue → Custom components)

**5.3 Document Camp Finder isolation:**
```bash
touch docs/bootstrap-5-migration/modules/openy_cf_vue_app_isolation.md
```

**5.4 Update migration log:**
```bash
vim docs/bootstrap-5-migration/MIGRATION_LOG.md
```

**Deliverable:** Complete Phase 5 preparation documentation

**Acceptance Criteria:**
- [ ] BootstrapVue audit documented
- [ ] Component library documented
- [ ] Camp Finder isolation documented
- [ ] Migration log updated

---

## Testing

### Component Library Testing

**Each Component Must Be Tested For:**
- [ ] Renders correctly
- [ ] Props work as expected
- [ ] Events emit correctly
- [ ] Slots work correctly
- [ ] Styling matches Bootstrap 5
- [ ] Responsive behavior
- [ ] Accessibility (keyboard, screen reader, ARIA)

**Test Environment:**
- [ ] Desktop browsers (Chrome, Firefox, Safari)
- [ ] Mobile browsers (iOS Safari, Chrome Android)
- [ ] Screen readers (NVDA, VoiceOver)

---

## Deliverables

### Must Have (Critical):
- [ ] BootstrapVue audit complete
- [ ] Custom Bootstrap 5 component library created
- [ ] All needed components implemented
- [ ] Component library tested
- [ ] Camp Finder isolated
- [ ] Documentation complete

### Should Have (High Priority):
- [ ] Component library examples
- [ ] Migration guide (BootstrapVue → Custom)
- [ ] Test application

### Nice to Have:
- [ ] Component Storybook
- [ ] Component unit tests
- [ ] Performance benchmarks

---

## Decision Points

### Decision: Component Library Approach
**Options:**
- Option A: Thin wrapper components (recommended)
- Option B: Full JavaScript components
- Option C: Hybrid approach

**Recommendation:** Option C (Hybrid)
- Use thin wrappers for simple components (button, card)
- Use full JavaScript for complex components (modal, dropdown)

---

## Risks

### Risk: Component Library Incomplete (CRITICAL)
**Impact:** CRITICAL - Cannot migrate apps without components
**Mitigation:**
- Complete audit before building library
- Build all components before migrating apps
- Test thoroughly in isolation
- Allocate buffer time
- Have fallback plan (vanilla Bootstrap 5)

### Risk: Component API Mismatch (HIGH)
**Impact:** HIGH - Migration will be harder
**Mitigation:**
- Match BootstrapVue API closely where possible
- Document API differences
- Create migration examples
- Test with real app code snippets

### Risk: Vue 2 Compatibility Issues (MEDIUM)
**Impact:** MEDIUM - Components may not work
**Mitigation:**
- Test all components with Vue 2
- Avoid Vue 3-specific features
- Use Vue 2 composition patterns
- Document Vue 2 requirements

### Risk: Camp Finder Isolation Fails (LOW)
**Impact:** MEDIUM - Camp Finder may conflict during migration
**Mitigation:**
- Use same approach as Activity Finder (proven)
- Test isolation thoroughly
- Document isolation requirements
- Have rollback plan

---

## Notes

### Important:
- This sprint is foundation for Sprints 19-21
- Component library quality critical for success
- Don't skip testing - will save time later
- BootstrapVue audit must be comprehensive
- Vue.js expertise required for this sprint

### Tips:
- Start with BootstrapVue audit - understand scope
- Build simple components first, complex later
- Test each component immediately after building
- Document as you go - don't delay
- Create examples for each component

### Phase 5 Context:
- Sprint 18: Preparation & component library (this sprint)
- Sprint 19: Camp Finder migration
- Sprint 20: Activity Finder migration
- Sprint 21: Activity Finder 4 migration + testing

### Why This Order:
1. Audit first - understand requirements
2. Build library - create tools
3. Test library - verify tools work
4. Then migrate apps - use tools

---

## Sprint Review Checklist

At end of sprint, verify:
- [ ] BootstrapVue audit complete
- [ ] Component library created
- [ ] All components tested
- [ ] Camp Finder isolated
- [ ] Documentation complete
- [ ] Next sprint ready (can start migrating apps)
- [ ] No blockers for Sprints 19-21

---

## Navigation

- **Previous:** [Sprint 17 - Donate & Testing](SPRINT_17_Y_Donate_Testing.md)
- **Next:** [Sprint 19 - Camp Finder](SPRINT_19_AF_Camp_Finder.md)
- **Phase:** [Phase 5 - Activity Finder](../phases/PHASE_5_ACTIVITY_FINDER.md)
- **Overview:** [Executive Summary](../EXECUTIVE_SUMMARY.md)

---

**Sprint Status:** ⬜ Not Started
**Last Updated:** 2025-10-17
