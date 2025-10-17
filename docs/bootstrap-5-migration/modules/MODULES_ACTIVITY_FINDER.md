# Activity Finder - Vue.js Applications

**Category:** Activity Finder Applications
**Total Apps:** 3 Vue.js applications
**Current Stack:** Vue 2 + Bootstrap 4.6.1 + BootstrapVue 2.22.0
**Target Stack:** Vue 2 + Bootstrap 5.3.3 + Vanilla JS
**Migration Phase:** Phase 5
**Sprints:** 18-21
**Risk Level:** ⚠️ CRITICAL - BootstrapVue 2 NOT compatible with Bootstrap 5

---

## Overview

The Activity Finder suite consists of three Vue.js applications that provide program and camp search functionality for Y USA sites. These applications present the most significant challenge in the Bootstrap 5 migration due to **BootstrapVue 2's incompatibility with Bootstrap 5**.

**Critical Issue:**
BootstrapVue 2 was built specifically for Bootstrap 4 and is **NOT compatible** with Bootstrap 5. BootstrapVue 3 is in alpha and not production-ready.

**Migration Strategy:**
Remove BootstrapVue components and replace with:
- Bootstrap 5 vanilla JavaScript
- Vue 2-compatible custom components
- Headless UI approach where applicable

---

## Application Details

### 1. Camp Finder (openy_cf_vue_app)

**Path:** `docroot/modules/contrib/openy_cf_vue_app/`
**Current Tech Stack:**
- Vue.js 2.6.x
- Bootstrap 4.6.1
- BootstrapVue 2.22.0
- Webpack 4

**Target Tech Stack:**
- Vue.js 2.6.x (maintained)
- Bootstrap 5.3.3
- Bootstrap 5 vanilla JS (no BootstrapVue)
- Webpack 5

**Sprint:** Sprint 19

**Description:**
Camp Finder provides search and filter functionality for summer camps and day camps. Users can search by location, age, dates, and program type.

**Key Features:**
- Map-based search with location filters
- Date range picker for camp sessions
- Age-based filtering
- Camp detail modals
- Registration links

**BootstrapVue Components Used:**
- `<b-modal>` - Camp detail modals
- `<b-form>` - Search forms
- `<b-form-input>` - Text inputs
- `<b-form-select>` - Dropdown selects
- `<b-form-checkbox>` - Filter checkboxes
- `<b-button>` - Action buttons
- `<b-card>` - Camp result cards
- `<b-collapse>` - Expandable sections
- `<b-pagination>` - Results pagination
- `<b-tooltip>` - Hover tooltips
- `<b-spinner>` - Loading indicators

**Migration Complexity:** HIGH

**Replacement Strategy:**
1. Replace `<b-modal>` with Bootstrap 5 Modal + custom Vue wrapper
2. Replace form components with native HTML + Bootstrap 5 classes
3. Replace `<b-card>` with HTML + `.card` classes
4. Replace `<b-collapse>` with Bootstrap 5 Collapse API
5. Replace `<b-pagination>` with custom Vue component
6. Replace `<b-tooltip>` with Bootstrap 5 Tooltip API
7. Replace `<b-spinner>` with Bootstrap 5 Spinner classes

**Testing Requirements:**
- Map integration (Leaflet/Google Maps)
- Date picker functionality
- Filter interactions
- Modal open/close
- Registration workflow
- Mobile responsive behavior

---

### 2. Activity Finder (openy_af_vue_app)

**Path:** `docroot/modules/contrib/openy_af_vue_app/`
**Current Tech Stack:**
- Vue.js 2.6.x
- Bootstrap 4.6.1
- BootstrapVue 2.22.0
- Webpack 4

**Target Tech Stack:**
- Vue.js 2.6.x (maintained)
- Bootstrap 5.3.3
- Bootstrap 5 vanilla JS (no BootstrapVue)
- Webpack 5

**Sprint:** Sprint 20

**Description:**
Activity Finder provides comprehensive program search across all YMCA offerings (fitness classes, swim lessons, sports, etc.). More complex than Camp Finder with additional filter options and schedule views.

**Key Features:**
- Multi-faceted search and filtering
- Location-based results
- Schedule views (calendar, list, grid)
- Program comparison
- Waitlist functionality
- Direct registration integration

**BootstrapVue Components Used:**
- `<b-modal>` - Program detail modals, comparison modals
- `<b-form>` - Complex search forms
- `<b-form-input>` - Text search, location input
- `<b-form-select>` - Category, location, age dropdowns
- `<b-form-checkbox>` - Multiple filter types
- `<b-form-radio>` - View mode selection
- `<b-button>` - Search, filter, action buttons
- `<b-button-group>` - View toggles (list/grid/calendar)
- `<b-card>` - Program result cards
- `<b-collapse>` - Filter sections, program details
- `<b-pagination>` - Results pagination
- `<b-tooltip>` - Information tooltips
- `<b-spinner>` - Loading states
- `<b-tabs>` - Program detail tabs
- `<b-table>` - Schedule tables
- `<b-badge>` - Status indicators (waitlist, full, etc.)

**Migration Complexity:** VERY HIGH

**Replacement Strategy:**
1. Create Bootstrap 5 Modal wrapper component for Vue
2. Build custom form component library
3. Implement Bootstrap 5 Tabs API wrapper
4. Create custom table component with sorting/filtering
5. Replace button groups with Bootstrap 5 Button Group
6. Implement Bootstrap 5 Collapse API for filters
7. Build custom pagination component
8. Replace badges with Bootstrap 5 Badge classes

**Testing Requirements:**
- All view modes (list, grid, calendar)
- Filter combinations (location + age + category + availability)
- Program comparison feature
- Waitlist workflow
- Registration integration
- Schedule display accuracy
- Mobile/tablet/desktop responsive
- Performance with large datasets

---

### 3. Activity Finder 4 (openy_af4_vue_app)

**Path:** `docroot/modules/contrib/openy_af4_vue_app/`
**Current Tech Stack:**
- Vue.js 2.6.x
- Bootstrap 4.6.1
- BootstrapVue 2.22.0
- Webpack 4
- Vue Router
- Vuex (state management)

**Target Tech Stack:**
- Vue.js 2.6.x (maintained)
- Bootstrap 5.3.3
- Bootstrap 5 vanilla JS (no BootstrapVue)
- Webpack 5
- Vue Router (maintained)
- Vuex (maintained)

**Sprint:** Sprint 21

**Description:**
Activity Finder 4 is the most advanced version with enhanced features, improved performance, and better architecture. Includes state management, routing, and more sophisticated UI.

**Key Features:**
- Advanced search with autocomplete
- Saved searches and favorites
- User preferences persistence
- Enhanced mobile UI
- Deep linking to specific programs
- Share functionality
- Advanced filtering with saved filter sets
- Program recommendations

**BootstrapVue Components Used:**
All components from Activity Finder plus:
- `<b-dropdown>` - Advanced menu actions
- `<b-nav>` - Navigation between views
- `<b-navbar>` - Mobile navigation
- `<b-popover>` - Extended information
- `<b-progress>` - Loading progress
- `<b-toast>` - Notifications
- `<b-sidebar>` - Mobile filter panel
- `<b-input-group>` - Search with addon buttons
- `<b-form-tags>` - Multi-select filters
- `<b-form-datepicker>` - Date selection
- `<b-form-timepicker>` - Time selection

**Migration Complexity:** CRITICAL - Highest complexity

**Replacement Strategy:**
All replacements from Activity Finder plus:
1. Create Bootstrap 5 Dropdown wrapper
2. Build custom Nav component
3. Implement Bootstrap 5 Offcanvas for sidebar (replaces b-sidebar)
4. Build custom toast notification system
5. Create Bootstrap 5 Popover wrapper
6. Replace date/time pickers with Flatpickr or similar
7. Build custom tags input component
8. Implement Bootstrap 5 Progress classes

**Testing Requirements:**
- All features from Activity Finder
- Routing and deep linking
- State persistence (Vuex)
- Autocomplete functionality
- Saved searches/favorites
- Share functionality
- Mobile navigation and offcanvas
- Toast notifications
- Advanced date/time pickers

---

## BootstrapVue Component Migration Matrix

### Complete Component List to Replace

| BootstrapVue Component | Usage Count (All Apps) | Bootstrap 5 Replacement | Migration Complexity |
|------------------------|------------------------|-------------------------|---------------------|
| `<b-modal>` | Very High | Bootstrap 5 Modal API + Vue wrapper | HIGH |
| `<b-form>` | Very High | Native `<form>` + BS5 classes | LOW |
| `<b-form-input>` | Very High | Native `<input class="form-control">` | LOW |
| `<b-form-select>` | High | Native `<select class="form-select">` | LOW |
| `<b-form-checkbox>` | High | Native `<input type="checkbox" class="form-check-input">` | LOW |
| `<b-form-radio>` | Medium | Native `<input type="radio" class="form-check-input">` | LOW |
| `<b-button>` | Very High | Native `<button class="btn">` | LOW |
| `<b-button-group>` | Medium | `<div class="btn-group">` | LOW |
| `<b-card>` | Very High | HTML + `.card` classes | LOW |
| `<b-collapse>` | High | Bootstrap 5 Collapse API | MEDIUM |
| `<b-pagination>` | High | Custom Vue component | MEDIUM |
| `<b-tooltip>` | Medium | Bootstrap 5 Tooltip API | MEDIUM |
| `<b-spinner>` | Medium | `<div class="spinner-border">` | LOW |
| `<b-tabs>` | Medium | Bootstrap 5 Tabs API + Vue wrapper | MEDIUM-HIGH |
| `<b-table>` | High | Custom Vue table component | HIGH |
| `<b-badge>` | Medium | `<span class="badge">` | LOW |
| `<b-dropdown>` | High | Bootstrap 5 Dropdown API | MEDIUM-HIGH |
| `<b-nav>` | Medium | `<nav>` + `.nav` classes | LOW |
| `<b-navbar>` | Medium | Bootstrap 5 Navbar | MEDIUM |
| `<b-popover>` | Low | Bootstrap 5 Popover API | MEDIUM |
| `<b-progress>` | Low | `<div class="progress">` | LOW |
| `<b-toast>` | Low | Custom Vue toast component | MEDIUM-HIGH |
| `<b-sidebar>` | Medium | Bootstrap 5 Offcanvas | MEDIUM-HIGH |
| `<b-input-group>` | High | `<div class="input-group">` | LOW |
| `<b-form-tags>` | Low | Custom Vue component | HIGH |
| `<b-form-datepicker>` | Medium | Flatpickr or similar | HIGH |
| `<b-form-timepicker>` | Low | Flatpickr or similar | HIGH |

---

## Recommended Component Library

### Custom Vue + Bootstrap 5 Components

Create a shared component library for all three apps:

**Location:** `docroot/modules/contrib/openy_activity_finder/components/`

**Core Components to Build:**

#### 1. Modal Component (`AFModal.vue`)
```vue
<template>
  <div class="modal" tabindex="-1" ref="modalElement">
    <div class="modal-dialog">
      <div class="modal-content">
        <div class="modal-header" v-if="title">
          <h5 class="modal-title">{{ title }}</h5>
          <button type="button" class="btn-close" @click="hide"></button>
        </div>
        <div class="modal-body">
          <slot></slot>
        </div>
        <div class="modal-footer" v-if="$slots.footer">
          <slot name="footer"></slot>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
import { Modal } from 'bootstrap';

export default {
  name: 'AFModal',
  props: {
    title: String,
    modelValue: Boolean
  },
  mounted() {
    this.modal = new Modal(this.$refs.modalElement);
    if (this.modelValue) this.show();
  },
  methods: {
    show() { this.modal.show(); },
    hide() { this.modal.hide(); }
  },
  watch: {
    modelValue(newVal) {
      newVal ? this.show() : this.hide();
    }
  }
}
</script>
```

**Complexity:** MEDIUM
**Reusable:** Yes, across all 3 apps

---

#### 2. Pagination Component (`AFPagination.vue`)
```vue
<template>
  <nav aria-label="Page navigation">
    <ul class="pagination">
      <li class="page-item" :class="{ disabled: currentPage === 1 }">
        <a class="page-link" @click="changePage(currentPage - 1)">Previous</a>
      </li>
      <li
        v-for="page in pages"
        :key="page"
        class="page-item"
        :class="{ active: page === currentPage }"
      >
        <a class="page-link" @click="changePage(page)">{{ page }}</a>
      </li>
      <li class="page-item" :class="{ disabled: currentPage === totalPages }">
        <a class="page-link" @click="changePage(currentPage + 1)">Next</a>
      </li>
    </ul>
  </nav>
</template>

<script>
export default {
  name: 'AFPagination',
  props: {
    totalItems: Number,
    itemsPerPage: { type: Number, default: 10 },
    currentPage: { type: Number, default: 1 }
  },
  computed: {
    totalPages() {
      return Math.ceil(this.totalItems / this.itemsPerPage);
    },
    pages() {
      // Logic to show limited page numbers
      const pages = [];
      for (let i = 1; i <= this.totalPages; i++) {
        pages.push(i);
      }
      return pages;
    }
  },
  methods: {
    changePage(page) {
      if (page >= 1 && page <= this.totalPages) {
        this.$emit('update:currentPage', page);
      }
    }
  }
}
</script>
```

**Complexity:** MEDIUM
**Reusable:** Yes, across all 3 apps

---

#### 3. Toast Component (`AFToast.vue`)
```vue
<template>
  <div class="toast-container position-fixed bottom-0 end-0 p-3">
    <div
      v-for="toast in toasts"
      :key="toast.id"
      class="toast show"
      role="alert"
    >
      <div class="toast-header">
        <strong class="me-auto">{{ toast.title }}</strong>
        <button type="button" class="btn-close" @click="remove(toast.id)"></button>
      </div>
      <div class="toast-body">
        {{ toast.message }}
      </div>
    </div>
  </div>
</template>

<script>
export default {
  name: 'AFToast',
  data() {
    return {
      toasts: []
    }
  },
  methods: {
    add(toast) {
      const id = Date.now();
      this.toasts.push({ ...toast, id });
      setTimeout(() => this.remove(id), toast.duration || 3000);
    },
    remove(id) {
      this.toasts = this.toasts.filter(t => t.id !== id);
    }
  }
}
</script>
```

**Complexity:** MEDIUM
**Reusable:** Yes, across all 3 apps (especially AF4)

---

## Migration Workflow

### Sprint 18: Preparation & Audit

**Goals:**
1. Audit all BootstrapVue component usage
2. Design component library architecture
3. Create migration plan per app
4. Set up testing infrastructure

**Deliverables:**
- Component usage audit spreadsheet
- Component library design doc
- Migration order (which app first)
- Testing baseline established

---

### Sprint 19: Camp Finder Migration

**Order of Operations:**
1. Upgrade Webpack 4 → 5
2. Upgrade Bootstrap 4.6.1 → 5.3.3 (CSS only)
3. Build core components (Modal, Pagination)
4. Replace BootstrapVue components incrementally
5. Test each replacement
6. Final integration testing

**Component Replacement Order:**
1. Simple components first (b-button, b-card, b-badge)
2. Form components (b-form-input, b-form-select, b-form-checkbox)
3. Interactive components (b-collapse, b-modal)
4. Complex components (b-pagination, b-tooltip)

**Testing per Replacement:**
- Unit tests for new components
- Visual regression tests
- Functional tests for interactive elements
- Cross-browser testing

---

### Sprint 20: Activity Finder Migration

**Goals:**
- Leverage components built in Sprint 19
- Handle additional complexity (tabs, tables, button groups)
- Focus on performance (larger dataset)

**Additional Components to Build:**
- Tabs wrapper
- Table component with sorting/filtering
- Button group utilities

**Testing Focus:**
- Performance testing with large datasets
- Filter combination testing
- View mode switching (list/grid/calendar)

---

### Sprint 21: Activity Finder 4 Migration

**Goals:**
- Complete component library
- Handle most advanced features (offcanvas, toast, advanced pickers)
- Ensure state management works with new components

**Additional Components to Build:**
- Offcanvas wrapper (replaces b-sidebar)
- Toast notification system
- Dropdown wrapper
- Date/time picker integration (Flatpickr)
- Tags input component

**Testing Focus:**
- Full application flow testing
- State management (Vuex) with new components
- Routing and deep linking
- Mobile-specific features (offcanvas, mobile nav)
- Notification system

---

## Date Picker Decision

### Critical Decision: Date/Time Picker Replacement

**Current:** BootstrapVue `<b-form-datepicker>` and `<b-form-timepicker>`
**Problem:** No Bootstrap 5 equivalent

**Options:**

#### Option 1: Flatpickr (Recommended)
- **Pros:** Lightweight, framework-agnostic, actively maintained
- **Cons:** Not Bootstrap-native, requires wrapper
- **Bundle Size:** ~10KB gzipped

**Installation:**
```bash
npm install flatpickr
npm install vue-flatpickr-component
```

**Usage:**
```vue
<template>
  <flat-pickr
    v-model="date"
    :config="config"
    class="form-control"
  />
</template>

<script>
import flatPickr from 'vue-flatpickr-component';
import 'flatpickr/dist/flatpickr.css';

export default {
  components: { flatPickr },
  data() {
    return {
      date: null,
      config: {
        dateFormat: 'Y-m-d',
        altInput: true,
        altFormat: 'F j, Y'
      }
    }
  }
}
</script>
```

#### Option 2: Vuejs Datepicker
- **Pros:** Vue-native, good documentation
- **Cons:** Vue 2 only, uncertain maintenance
- **Bundle Size:** ~15KB gzipped

#### Option 3: Build Custom
- **Pros:** Full control, no dependencies
- **Cons:** Significant development time, maintenance burden
- **Effort:** 2-3 days per picker type

**Recommendation:** Use Flatpickr with custom Bootstrap 5 styling.

**See:** [DECISION_DATE_PICKER.md](../decisions/DECISION_DATE_PICKER.md) for full analysis

---

## Technical Architecture

### Shared Component Library Structure

```
docroot/modules/contrib/openy_activity_finder/
├── components/
│   ├── AFModal.vue
│   ├── AFPagination.vue
│   ├── AFToast.vue
│   ├── AFTabs.vue
│   ├── AFTable.vue
│   ├── AFOffcanvas.vue
│   ├── AFDropdown.vue
│   ├── AFDatePicker.vue
│   └── AFTimePicker.vue
├── mixins/
│   ├── bootstrap-modal.js
│   ├── bootstrap-collapse.js
│   ├── bootstrap-tooltip.js
│   └── bootstrap-popover.js
├── utils/
│   ├── bootstrap-helpers.js
│   └── vue-bootstrap-bridge.js
└── styles/
    ├── activity-finder-bootstrap5.scss
    └── components.scss
```

### Bootstrap 5 JavaScript Integration

**Import Bootstrap 5 components:**
```javascript
// webpack entry point
import { Modal, Collapse, Dropdown, Tab, Toast, Tooltip, Popover, Offcanvas } from 'bootstrap';

// Make available globally for Vue components
window.bootstrap = { Modal, Collapse, Dropdown, Tab, Toast, Tooltip, Popover, Offcanvas };
```

**Or import per component:**
```javascript
// In AFModal.vue
import { Modal } from 'bootstrap';
```

---

## Testing Strategy

### Unit Testing
**Tool:** Jest + Vue Test Utils

**Focus:**
- Component props and events
- Component methods
- Computed properties
- Watchers

**Coverage Target:** 80%+

---

### Integration Testing
**Tool:** Cypress

**Focus:**
- Search and filter workflows
- Modal interactions
- Form submissions
- Pagination
- View mode switching
- Registration workflows

**Critical Paths:**
1. Search → Filter → View Details → Register
2. Location-based search → Map interaction → Results
3. Date selection → Available programs → Waitlist

---

### Visual Regression Testing
**Tool:** BackstopJS

**Scenarios:**
- All view modes (list, grid, calendar)
- Modal open/closed states
- Filter panel expanded/collapsed
- Mobile navigation
- Loading states
- Empty states
- Error states

**Breakpoints:**
- Mobile: 375px, 414px
- Tablet: 768px, 1024px
- Desktop: 1280px, 1920px

---

### Accessibility Testing
**Tool:** Pa11y + axe-core

**Requirements:**
- WCAG 2.2 Level AA
- Keyboard navigation for all interactive elements
- Screen reader compatibility
- Focus management in modals
- Aria labels for icons/actions
- Color contrast compliance

---

### Performance Testing
**Tool:** Lighthouse

**Targets:**
- Performance: 90+
- Accessibility: 100
- Best Practices: 100
- SEO: 90+

**Key Metrics:**
- First Contentful Paint (FCP): < 1.8s
- Time to Interactive (TTI): < 3.8s
- Total Blocking Time (TBT): < 200ms
- Bundle size: < 250KB gzipped

---

## Risk Assessment

### Risk 1: BootstrapVue Removal (CRITICAL)
**Impact:** Entire application UI depends on BootstrapVue
**Probability:** 100% (known issue)
**Mitigation:**
- Phased approach (one app at a time)
- Comprehensive component library
- Extensive testing at each step
- Rollback plan if needed

### Risk 2: Breaking Changes (HIGH)
**Impact:** User workflows may break during migration
**Mitigation:**
- Maintain feature parity
- Test all user flows
- QA approval before deployment
- Staged rollout per app

### Risk 3: Performance Regression (MEDIUM)
**Impact:** Apps may be slower with new components
**Mitigation:**
- Benchmark before migration
- Monitor bundle size
- Optimize new components
- Performance testing required

### Risk 4: Date Picker Choice (MEDIUM)
**Impact:** Wrong choice could require re-work
**Mitigation:**
- Evaluate options in Sprint 18
- Build proof of concept
- Get stakeholder approval
- See DECISION_DATE_PICKER.md

### Risk 5: Mobile Functionality (MEDIUM)
**Impact:** Mobile-specific features may break (offcanvas, touch interactions)
**Mitigation:**
- Test on real devices
- Focus on mobile-first approach
- Touch interaction testing

---

## Success Criteria

### Functional Requirements:
- [ ] All search and filter features work
- [ ] All view modes functional (list, grid, calendar)
- [ ] Modals open/close correctly
- [ ] Forms validate and submit
- [ ] Pagination works
- [ ] Registration workflows complete
- [ ] Mobile navigation functional

### Technical Requirements:
- [ ] Webpack 5 builds successfully
- [ ] Bootstrap 5.3.3 installed
- [ ] BootstrapVue completely removed
- [ ] No console errors
- [ ] Bundle size maintained or reduced
- [ ] Performance targets met (Lighthouse 90+)

### Quality Requirements:
- [ ] Visual appearance matches Bootstrap 4 version
- [ ] Accessibility maintained (WCAG 2.2 AA)
- [ ] All browsers supported (Chrome, Firefox, Safari, Edge)
- [ ] Mobile responsive at all breakpoints
- [ ] Unit test coverage 80%+

### Documentation Requirements:
- [ ] Component library documented
- [ ] Migration guide created
- [ ] Breaking changes documented
- [ ] API documentation for new components

---

## Dependencies

### Before Activity Finder Migration:
- [x] Phase 1 complete (theme migrated)
- [x] Date picker decision made (Sprint 1)
- [ ] Phases 2-4 complete (all other modules working with BS5)

### After Activity Finder Migration:
- [ ] All 3 apps tested and working
- [ ] Component library published
- [ ] Performance validated
- [ ] Ready for production rollout

---

## Related Documents

**Phase Documentation:**
- [Phase 5: Activity Finder](../phases/PHASE_5_ACTIVITY_FINDER.md)

**Sprint Documentation:**
- [Sprint 18: AF Preparation & Audit](../sprints/SPRINT_18_AF_Preparation.md)
- [Sprint 19: Camp Finder Migration](../sprints/SPRINT_19_Camp_Finder.md)
- [Sprint 20: Activity Finder Migration](../sprints/SPRINT_20_Activity_Finder.md)
- [Sprint 21: Activity Finder 4 Migration](../sprints/SPRINT_21_Activity_Finder_4.md)

**Decision Documentation:**
- [DECISION_ACTIVITY_FINDER.md](../decisions/DECISION_ACTIVITY_FINDER.md) - Full strategy analysis
- [DECISION_DATE_PICKER.md](../decisions/DECISION_DATE_PICKER.md) - Date picker options

**Reference Materials:**
- [Bootstrap 5 Cheatsheet](../reference/BOOTSTRAP_5_CHEATSHEET.md)
- [Troubleshooting Guide](../reference/TROUBLESHOOTING.md)

---

**Document Status:** ✅ Complete
**Last Updated:** 2025-10-17
**Applications Documented:** 3
**Risk Level:** CRITICAL
**Total Lines:** < 999
