# Sprint 19: Camp Finder Migration

**Phase:** [Phase 5 - Activity Finder](../phases/PHASE_5_ACTIVITY_FINDER.md)
**Resources:** 1 Frontend Developer (Vue.js experience required)
**Status:** Not Started

---

## Sprint Goal

Migrate Camp Finder (openy_cf_vue_app) from BootstrapVue 2 + Bootstrap 4 to custom components + Bootstrap 5. Remove isolation, verify functionality, and establish migration patterns for remaining Activity Finder apps.

---

## Module in This Sprint

**openy_cf_vue_app** - Camp Finder Vue.js Application
- Path: `docroot/modules/contrib/yusaopeny_activity_finder/openy_cf_vue_app`
- Current: Vue.js 2 + BootstrapVue 2 + Bootstrap 4.4.1 (isolated)
- Target: Vue.js 2 + Custom Components + Bootstrap 5.3.3
- Isolation: Remove after migration complete

---

## Tasks

### Task 1: Prepare Camp Finder for Migration
**Owner:** Developer
**Priority:** CRITICAL

**Actions:**

**1.1 Review current Camp Finder:**
```bash
cd docroot/modules/contrib/yusaopeny_activity_finder/openy_cf_vue_app

# Review structure
ls -la
cat package.json
cat webpack.config.js

# Review Vue components
find src/ -name "*.vue"
```

**1.2 Document current functionality:**
- Camp search functionality
- Filter options (location, age, date, category)
- Results display (list/grid view)
- Camp detail modal/popup
- Registration links
- Map integration (if present)

**1.3 Create migration checklist:**
```markdown
# Camp Finder Migration Checklist

## Dependencies
- [ ] Update package.json
- [ ] Remove BootstrapVue
- [ ] Add custom component library
- [ ] Update Bootstrap to 5.3.3

## Components
- [ ] Replace all b-* components
- [ ] Update imports
- [ ] Update component usage
- [ ] Test each component

## Styling
- [ ] Update Bootstrap classes
- [ ] Update SCSS imports
- [ ] Remove isolation scoping
- [ ] Test responsive design

## Functionality
- [ ] Camp search works
- [ ] Filters work
- [ ] Results display correct
- [ ] Detail modal works
- [ ] Registration links work

## Build & Deploy
- [ ] Build succeeds
- [ ] No console errors
- [ ] Production build optimized
```

**Deliverable:** Camp Finder migration plan

**Acceptance Criteria:**
- [ ] Current functionality documented
- [ ] Migration checklist created
- [ ] Risks identified

---

### Task 2: Update Camp Finder Dependencies
**Owner:** Developer
**Priority:** CRITICAL

**Actions:**

**2.1 Update package.json:**
```bash
cd docroot/modules/contrib/yusaopeny_activity_finder/openy_cf_vue_app
```

```json
{
  "name": "openy_cf_vue_app",
  "version": "2.0.0",
  "dependencies": {
    "vue": "^2.6.14",
    "bootstrap": "^5.3.3",
    "@popperjs/core": "^2.11.8",
    "axios": "^1.6.0"
  },
  "devDependencies": {
    "webpack": "^5.89.0",
    "webpack-cli": "^5.1.4",
    "vue-loader": "^15.10.1",
    "sass": "^1.69.5",
    "sass-loader": "^13.3.2"
  }
}
```

**2.2 Remove BootstrapVue:**
```bash
npm uninstall bootstrap-vue
```

**2.3 Install custom component library:**
```bash
# Link to shared component library from Sprint 18
npm link ../../shared/components
```

**Or copy components:**
```bash
cp -r ../../shared/components src/components/bootstrap
```

**2.4 Update Bootstrap version:**
```bash
npm uninstall bootstrap@4.4.1
npm install bootstrap@5.3.3 @popperjs/core
```

**2.5 Install dependencies:**
```bash
npm install
```

**Deliverable:** Updated package.json and dependencies

**Acceptance Criteria:**
- [ ] BootstrapVue removed
- [ ] Bootstrap 5.3.3 installed
- [ ] Custom components accessible
- [ ] npm install succeeds

---

### Task 3: Remove Bootstrap 4 Isolation
**Owner:** Developer
**Priority:** HIGH

**Actions:**

**3.1 Remove webpack scoping:**
```javascript
// webpack.config.js

// REMOVE postcss-prefix-selector plugin
// Was added in Sprint 18 for isolation

module.exports = {
  module: {
    rules: [
      {
        test: /\.scss$/,
        use: [
          MiniCssExtractPlugin.loader,
          'css-loader',
          // REMOVE postcss-loader with prefix-selector
          'sass-loader'
        ]
      }
    ]
  }
};
```

**3.2 Update SCSS imports:**
```scss
// src/styles/main.scss

// OLD: Bootstrap 4
// @import "~bootstrap/scss/bootstrap";

// NEW: Bootstrap 5
@import "bootstrap/scss/functions";
@import "bootstrap/scss/variables";
@import "bootstrap/scss/mixins";
@import "bootstrap/scss/bootstrap";

// Camp Finder custom styles
.camp-finder {
  // No longer need .camp-finder-wrapper scoping
}
```

**3.3 Update template (remove wrapper):**
```twig
{# OLD: Isolated with wrapper #}
<div class="camp-finder-wrapper">
  <div id="camp-finder-app"></div>
</div>

{# NEW: Direct mount #}
<div id="camp-finder-app"></div>
```

**Deliverable:** Isolation removed

**Acceptance Criteria:**
- [ ] Webpack scoping removed
- [ ] SCSS updated to Bootstrap 5
- [ ] Template wrapper removed
- [ ] Build succeeds

---

### Task 4: Replace BootstrapVue Components
**Owner:** Developer
**Priority:** CRITICAL

**Actions:**

**4.1 Update main App.vue:**
```vue
<template>
  <div id="camp-finder-app" class="camp-finder">
    <!-- OLD: BootstrapVue components
    <b-container>
      <b-row>
        <b-col>
          <b-card>
    -->

    <!-- NEW: Custom components -->
    <div class="container">
      <div class="row">
        <div class="col">
          <bs-card>
            <bs-card-body>
              <search-form />
              <filter-panel />
              <results-list />
            </bs-card-body>
          </bs-card>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
// OLD: BootstrapVue imports
// import { BContainer, BRow, BCol, BCard } from 'bootstrap-vue';

// NEW: Custom component imports
import {
  BsCard,
  BsCardBody,
  BsButton,
  BsFormInput,
  BsFormSelect
} from './components/bootstrap';

export default {
  name: 'CampFinderApp',
  components: {
    BsCard,
    BsCardBody,
    BsButton,
    BsFormInput,
    BsFormSelect
  },
  // ... rest of component
}
</script>
```

**4.2 Update SearchForm.vue:**
```vue
<template>
  <div class="search-form">
    <!-- OLD: BootstrapVue form
    <b-form @submit.prevent="onSubmit">
      <b-form-group label="Search Camps">
        <b-form-input
          v-model="searchTerm"
          placeholder="Enter keywords..."
        />
      </b-form-group>
      <b-button type="submit" variant="primary">
        Search
      </b-button>
    </b-form>
    -->

    <!-- NEW: Custom components -->
    <form @submit.prevent="onSubmit" class="mb-4">
      <div class="mb-3">
        <label for="search" class="form-label">Search Camps</label>
        <bs-form-input
          id="search"
          v-model="searchTerm"
          placeholder="Enter keywords..."
        />
      </div>
      <bs-button type="submit" variant="primary">
        Search
      </bs-button>
    </form>
  </div>
</template>

<script>
import { BsFormInput, BsButton } from './components/bootstrap';

export default {
  name: 'SearchForm',
  components: {
    BsFormInput,
    BsButton
  },
  // ... rest of component
}
</script>
```

**4.3 Update FilterPanel.vue:**
```vue
<template>
  <div class="filter-panel">
    <!-- Replace b-form-select with bs-form-select -->
    <div class="row g-3">
      <div class="col-md-3">
        <label class="form-label">Location</label>
        <bs-form-select v-model="filters.location">
          <option value="">All Locations</option>
          <option v-for="loc in locations" :key="loc.id" :value="loc.id">
            {{ loc.name }}
          </option>
        </bs-form-select>
      </div>

      <div class="col-md-3">
        <label class="form-label">Age Group</label>
        <bs-form-select v-model="filters.age">
          <option value="">All Ages</option>
          <option v-for="age in ageGroups" :key="age" :value="age">
            {{ age }}
          </option>
        </bs-form-select>
      </div>

      <div class="col-md-3">
        <label class="form-label">Category</label>
        <bs-form-select v-model="filters.category">
          <option value="">All Categories</option>
          <option v-for="cat in categories" :key="cat.id" :value="cat.id">
            {{ cat.name }}
          </option>
        </bs-form-select>
      </div>

      <div class="col-md-3">
        <label class="form-label">&nbsp;</label>
        <bs-button variant="secondary" @click="clearFilters" class="w-100">
          Clear Filters
        </bs-button>
      </div>
    </div>
  </div>
</template>
```

**4.4 Update ResultsList.vue:**
```vue
<template>
  <div class="results-list">
    <!-- Replace b-card with bs-card -->
    <div class="row">
      <div
        v-for="camp in camps"
        :key="camp.id"
        class="col-md-4 mb-4"
      >
        <bs-card>
          <img
            v-if="camp.image"
            :src="camp.image"
            class="card-img-top"
            :alt="camp.title"
          >
          <bs-card-body>
            <bs-card-title>{{ camp.title }}</bs-card-title>
            <p class="card-text">{{ camp.description }}</p>

            <div class="camp-meta">
              <div class="mb-2">
                <bs-badge variant="primary">{{ camp.ageGroup }}</bs-badge>
                <bs-badge variant="secondary">{{ camp.category }}</bs-badge>
              </div>
              <div class="camp-dates">
                {{ formatDates(camp.startDate, camp.endDate) }}
              </div>
            </div>

            <bs-button
              variant="primary"
              @click="showDetails(camp)"
              class="w-100"
            >
              View Details
            </bs-button>
          </bs-card-body>
        </bs-card>
      </div>
    </div>

    <!-- No results message -->
    <bs-alert v-if="camps.length === 0" variant="info">
      No camps found. Try adjusting your filters.
    </bs-alert>

    <!-- Loading spinner -->
    <div v-if="loading" class="text-center">
      <bs-spinner />
    </div>
  </div>
</template>
```

**4.5 Update CampDetailModal.vue:**
```vue
<template>
  <!-- Replace b-modal with bs-modal -->
  <bs-modal
    v-model="showModal"
    :title="camp.title"
    size="lg"
  >
    <div class="camp-details">
      <img
        v-if="camp.image"
        :src="camp.image"
        class="img-fluid mb-3"
        :alt="camp.title"
      >

      <div class="camp-info">
        <h5>Description</h5>
        <p>{{ camp.description }}</p>

        <h5>Dates</h5>
        <p>{{ formatDates(camp.startDate, camp.endDate) }}</p>

        <h5>Location</h5>
        <p>{{ camp.location }}</p>

        <h5>Age Group</h5>
        <p>{{ camp.ageGroup }}</p>

        <h5>Price</h5>
        <p>{{ formatPrice(camp.price) }}</p>
      </div>
    </div>

    <template #footer>
      <bs-button variant="secondary" @click="closeModal">
        Close
      </bs-button>
      <bs-button
        variant="primary"
        :href="camp.registrationUrl"
        target="_blank"
      >
        Register Now
      </bs-button>
    </template>
  </bs-modal>
</template>
```

**Deliverable:** All BootstrapVue components replaced

**Acceptance Criteria:**
- [ ] All b-* components replaced with bs-* or HTML
- [ ] All imports updated
- [ ] App builds successfully
- [ ] No BootstrapVue references remain

---

### Task 5: Update Styling and Classes
**Owner:** Developer
**Priority:** HIGH

**Actions:**

**5.1 Update Bootstrap class names:**
```vue
<!-- OLD: Bootstrap 4 classes -->
<div class="form-group">
  <label>Label</label>
  <input class="form-control">
</div>

<!-- NEW: Bootstrap 5 classes -->
<div class="mb-3">
  <label class="form-label">Label</label>
  <input class="form-control">
</div>
```

**5.2 Update utility classes:**
```scss
// OLD: Bootstrap 4
.ml-2 { } // margin-left
.mr-2 { } // margin-right
.pr-3 { } // padding-right
.float-left { }

// NEW: Bootstrap 5
.ms-2 { } // margin-start
.me-2 { } // margin-end
.pe-3 { } // padding-end
.float-start { }
```

**5.3 Update grid gutters:**
```html
<!-- OLD: Bootstrap 4 -->
<div class="row">
  <div class="col-md-4">

<!-- NEW: Bootstrap 5 -->
<div class="row g-3">
  <div class="col-md-4">
```

**5.4 Update button classes:**
```html
<!-- OLD: Bootstrap 4 -->
<button class="btn btn-primary">Button</button>

<!-- NEW: Bootstrap 5 (mostly same) -->
<button class="btn btn-primary">Button</button>
```

**5.5 Update data attributes:**
```html
<!-- OLD: Bootstrap 4 -->
<button data-toggle="modal" data-target="#myModal">

<!-- NEW: Bootstrap 5 -->
<button data-bs-toggle="modal" data-bs-target="#myModal">
```

**Deliverable:** Updated styles and classes

**Acceptance Criteria:**
- [ ] All Bootstrap 4 classes updated to Bootstrap 5
- [ ] All data-* attributes updated to data-bs-*
- [ ] Responsive design maintained
- [ ] Visual appearance correct

---

### Task 6: Build and Test
**Owner:** Developer
**Priority:** CRITICAL

**Actions:**

**6.1 Build Camp Finder:**
```bash
cd docroot/modules/contrib/yusaopeny_activity_finder/openy_cf_vue_app

# Development build
npm run dev

# Production build
npm run build
```

**6.2 Test functionality:**
- [ ] Camp search works
- [ ] Search with keywords
- [ ] Search with no results
- [ ] Search with many results

**6.3 Test filters:**
- [ ] Location filter
- [ ] Age group filter
- [ ] Category filter
- [ ] Date range filter (if present)
- [ ] Multiple filters together
- [ ] Clear filters

**6.4 Test results display:**
- [ ] Results list view
- [ ] Results grid view
- [ ] Camp cards display correctly
- [ ] Camp images display
- [ ] Camp metadata displays
- [ ] No results message

**6.5 Test camp details:**
- [ ] Click camp to view details
- [ ] Detail modal opens
- [ ] Detail content displays correctly
- [ ] Registration link works
- [ ] Modal closes correctly

**6.6 Test responsive:**
- [ ] Desktop view (> 992px)
- [ ] Tablet view (768px - 992px)
- [ ] Mobile view (< 768px)
- [ ] Touch interactions
- [ ] Mobile keyboard

**6.7 Test on camp pages:**
- [ ] Camp Finder on camp content type pages
- [ ] No style conflicts with page
- [ ] Camp Finder data loads from Drupal
- [ ] Integration with Drupal API

**Deliverable:** Test report

**Acceptance Criteria:**
- [ ] Build succeeds without errors
- [ ] All functionality works
- [ ] Responsive design works
- [ ] Integration with Drupal works
- [ ] No console errors

---

### Task 7: Visual Regression Testing
**Owner:** Developer
**Priority:** HIGH

**Actions:**

**7.1 Update BackstopJS scenarios:**
```json
{
  "scenarios": [
    {
      "label": "Camp Finder - Initial Load",
      "url": "http://yusaopeny.docksal.site/camp-finder"
    },
    {
      "label": "Camp Finder - Search Results",
      "url": "http://yusaopeny.docksal.site/camp-finder?search=summer"
    },
    {
      "label": "Camp Finder - Filters Applied",
      "url": "http://yusaopeny.docksal.site/camp-finder?location=1&age=6-8"
    },
    {
      "label": "Camp Finder - No Results",
      "url": "http://yusaopeny.docksal.site/camp-finder?search=xyz123"
    }
  ]
}
```

**7.2 Run visual tests:**
```bash
cd docs/bootstrap-5-migration/testing
npx backstop test
npx backstop openReport
```

**7.3 Review differences:**
- Expected differences (Bootstrap 5 styling improvements)
- Unexpected differences (investigate)

**Deliverable:** Visual regression report

**Acceptance Criteria:**
- [ ] Visual tests run successfully
- [ ] Differences documented
- [ ] Critical visual issues fixed

---

### Task 8: Accessibility Testing
**Owner:** Developer
**Priority:** HIGH

**Actions:**

**8.1 Run Pa11y tests:**
```bash
npx pa11y-ci
```

**8.2 Manual accessibility testing:**
- [ ] Keyboard navigation (all interactive elements)
- [ ] Tab order logical
- [ ] Enter key submits search
- [ ] Escape key closes modal
- [ ] Arrow keys navigate filters (if applicable)

**8.3 Screen reader testing:**
- [ ] Search form accessible
- [ ] Filter labels announced
- [ ] Results announced (live region)
- [ ] Camp details announced
- [ ] Loading state announced

**8.4 Test ARIA attributes:**
- [ ] Form labels correct
- [ ] Button labels correct
- [ ] Modal ARIA attributes
- [ ] Live regions for dynamic content
- [ ] Focus management in modal

**8.5 Test color contrast:**
- [ ] All text passes WCAG 2.2 AA
- [ ] Button colors pass contrast
- [ ] Link colors pass contrast

**Deliverable:** Accessibility test report

**Acceptance Criteria:**
- [ ] WCAG 2.2 AA compliance
- [ ] Keyboard navigation works
- [ ] Screen reader compatible
- [ ] No critical accessibility issues

---

### Task 9: Documentation
**Owner:** Developer
**Priority:** MEDIUM

**Actions:**

**9.1 Document Camp Finder migration:**
```bash
touch docs/bootstrap-5-migration/modules/openy_cf_vue_app.md
```

**Content:**
- Migration process
- BootstrapVue components replaced
- Styling changes
- Known issues
- Testing results

**9.2 Document migration patterns:**
- Component replacement patterns
- Common issues and solutions
- Lessons learned
- Tips for next migrations

**9.3 Update migration log:**
```bash
vim docs/bootstrap-5-migration/MIGRATION_LOG.md
```

**Deliverable:** Complete documentation

**Acceptance Criteria:**
- [ ] Module documentation complete
- [ ] Migration patterns documented
- [ ] Known issues documented
- [ ] Migration log updated

---

## Testing

### Comprehensive Testing Checklist

**Search Functionality:**
- [ ] Search with keywords
- [ ] Search with no results
- [ ] Search with many results
- [ ] Search with special characters
- [ ] Clear search

**Filters:**
- [ ] Location filter
- [ ] Age group filter
- [ ] Category filter
- [ ] Date filter (if present)
- [ ] Multiple filters
- [ ] Clear filters
- [ ] Filter persistence (URL params)

**Results:**
- [ ] List view
- [ ] Grid view (if present)
- [ ] Camp cards display
- [ ] Camp images
- [ ] Camp metadata
- [ ] Registration links
- [ ] No results message
- [ ] Loading spinner

**Camp Details:**
- [ ] Modal opens
- [ ] Content displays
- [ ] Images display
- [ ] Registration link works
- [ ] Modal closes

**Responsive:**
- [ ] Desktop (> 992px)
- [ ] Tablet (768px - 992px)
- [ ] Mobile (< 768px)
- [ ] Touch interactions

**Integration:**
- [ ] Works on camp pages
- [ ] Drupal data loads correctly
- [ ] No style conflicts

---

## Deliverables

### Must Have (Critical):
- [ ] Camp Finder migrated to Bootstrap 5
- [ ] BootstrapVue completely removed
- [ ] Custom components integrated
- [ ] Isolation removed
- [ ] All functionality working
- [ ] Build succeeds
- [ ] Visual regression tests passed
- [ ] Accessibility tests passed
- [ ] Module documentation complete

### Should Have (High Priority):
- [ ] Migration patterns documented
- [ ] Test report complete
- [ ] Known issues documented

### Nice to Have:
- [ ] Performance comparison (BS4 vs BS5)
- [ ] Bundle size comparison
- [ ] Video demo

---

## Decision Points

### Decision: Migration Success Criteria
**Question:** Is Camp Finder ready for production?
**Criteria:**
- [ ] All functionality works
- [ ] No critical bugs
- [ ] Accessibility maintained
- [ ] Performance acceptable
- [ ] Visual appearance approved

**Decision Maker:** Developer + Project Lead

---

## Risks

### Risk: BootstrapVue Removal Breaks Functionality (HIGH)
**Impact:** CRITICAL - Camp Finder may not work
**Mitigation:**
- Test thoroughly after each component replacement
- Keep Bootstrap 4 version as backup
- Use component library from Sprint 18 (tested)
- Allocate buffer time for debugging

### Risk: Style Conflicts After Isolation Removal (MEDIUM)
**Impact:** MEDIUM - Visual issues may occur
**Mitigation:**
- Test on actual camp pages
- Check for style conflicts
- Use visual regression testing
- Fix conflicts immediately

### Risk: Integration with Drupal Breaks (MEDIUM)
**Impact:** HIGH - Data may not load
**Mitigation:**
- Don't modify Drupal integration code
- Test data loading early
- Verify API endpoints still work
- Test with realistic data

---

## Notes

### Important:
- First Vue app migration - establishes patterns
- Component library from Sprint 18 is critical
- Don't modify Drupal integration logic
- Test thoroughly before declaring success
- Document everything for Sprints 20-21

### Tips:
- Replace components incrementally
- Test after each major change
- Use component library consistently
- Document any issues for next sprints
- Keep development build running for fast iteration

### Phase 5 Context:
- Sprint 18: Preparation & component library (complete)
- Sprint 19: Camp Finder migration (this sprint)
- Sprint 20: Activity Finder migration
- Sprint 21: Activity Finder 4 migration + testing

### Success Metrics:
- Camp Finder fully functional ✓
- BootstrapVue removed ✓
- Bootstrap 5.3.3 ✓
- No console errors ✓
- Accessible ✓
- Migration patterns documented ✓

---

## Sprint Review Checklist

At end of sprint, verify:
- [ ] Camp Finder migrated
- [ ] All functionality works
- [ ] Testing complete
- [ ] Documentation complete
- [ ] Migration patterns documented
- [ ] Next sprint ready (can start Activity Finder)
- [ ] No blockers for Sprint 20

---

## Navigation

- **Previous:** [Sprint 18 - AF Preparation & Audit](SPRINT_18_AF_Preparation_Audit.md)
- **Next:** [Sprint 20 - Activity Finder](SPRINT_20_AF_Activity_Finder.md)
- **Phase:** [Phase 5 - Activity Finder](../phases/PHASE_5_ACTIVITY_FINDER.md)
- **Overview:** [Executive Summary](../EXECUTIVE_SUMMARY.md)

---

**Sprint Status:** ⬜ Not Started
**Last Updated:** 2025-10-17
