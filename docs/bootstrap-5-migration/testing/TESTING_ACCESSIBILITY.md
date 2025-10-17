# Accessibility Testing - Bootstrap 5 Migration

## Overview

Accessibility testing ensures that the Bootstrap 5 migration maintains or improves compliance with WCAG 2.2 Level AA standards. This guide covers automated testing with Pa11y, manual testing procedures, and best practices for ensuring your YMCA site is accessible to all users.

## Why Accessibility Testing?

- **Legal Compliance:** Meet ADA and Section 508 requirements
- **Inclusive Design:** Ensure all users can access your content
- **Better UX:** Accessible sites are more usable for everyone
- **SEO Benefits:** Many accessibility improvements help search rankings
- **Brand Reputation:** Demonstrates commitment to inclusivity

## WCAG 2.2 Level AA Overview

### Four Principles (POUR)

#### 1. Perceivable
Information and UI components must be presentable to users in ways they can perceive.

- Provide text alternatives for non-text content
- Provide captions and alternatives for multimedia
- Create content that can be presented in different ways
- Make it easy for users to see and hear content

#### 2. Operable
User interface components and navigation must be operable.

- Make all functionality available from a keyboard
- Give users enough time to read and use content
- Do not use content that causes seizures
- Help users navigate and find content

#### 3. Understandable
Information and operation of UI must be understandable.

- Make text readable and understandable
- Make content appear and operate in predictable ways
- Help users avoid and correct mistakes

#### 4. Robust
Content must be robust enough to be interpreted by assistive technologies.

- Maximize compatibility with current and future tools
- Use valid, semantic HTML
- Provide proper ARIA attributes

## Automated Testing with Pa11y

### Installation

```bash
# Navigate to testing directory
cd /private/var/www/YMCAWS_11/testing

# Install Pa11y and Pa11y-CI
npm install --save-dev pa11y pa11y-ci

# Verify installation
npx pa11y --version
```

### Basic Configuration

Create `testing/pa11y/.pa11yci.json`:

```json
{
  "defaults": {
    "standard": "WCAG2AA",
    "timeout": 30000,
    "wait": 2000,
    "chromeLaunchConfig": {
      "args": [
        "--no-sandbox",
        "--disable-setuid-sandbox"
      ]
    },
    "runners": [
      "axe",
      "htmlcs"
    ],
    "ignore": [
      "notice",
      "warning"
    ]
  },
  "urls": [
    "http://yusaopeny.docksal.site/",
    "http://yusaopeny.docksal.site/about",
    "http://yusaopeny.docksal.site/programs",
    "http://yusaopeny.docksal.site/locations",
    "http://yusaopeny.docksal.site/news",
    "http://yusaopeny.docksal.site/events",
    "http://yusaopeny.docksal.site/contact"
  ]
}
```

### Advanced Configuration

Create `testing/pa11y/pa11y.config.js`:

```javascript
const fs = require('fs');

// Load environment variables
require('dotenv').config({ path: '../.env.testing' });

const BASE_URL = process.env.BASE_URL_AFTER || 'http://yusaopeny.docksal.site';

// Load URLs from file
const urlsFile = './urls.json';
let urls = [];

if (fs.existsSync(urlsFile)) {
  const urlData = JSON.parse(fs.readFileSync(urlsFile, 'utf8'));
  urls = urlData.map(item => `${BASE_URL}${item.path}`);
} else {
  // Default URLs if file doesn't exist
  urls = [
    `${BASE_URL}/`,
    `${BASE_URL}/about`,
    `${BASE_URL}/programs`
  ];
}

module.exports = {
  defaults: {
    // WCAG 2.2 Level AA standard
    standard: 'WCAG2AA',

    // Browser configuration
    timeout: 30000,
    wait: 2000,
    chromeLaunchConfig: {
      args: [
        '--no-sandbox',
        '--disable-setuid-sandbox',
        '--disable-dev-shm-usage'
      ],
      headless: 'new'
    },

    // Use multiple test runners
    runners: [
      'axe',      // Axe-core accessibility engine
      'htmlcs'    // HTML CodeSniffer
    ],

    // Ignore levels
    ignore: [
      'notice',   // Informational only
      'warning'   // Potential issues (can enable for stricter testing)
    ],

    // Include warnings for comprehensive testing
    includeWarnings: false,
    includeNotices: false,

    // Viewport size
    viewport: {
      width: 1920,
      height: 1080
    },

    // Screenshot on error (helpful for debugging)
    screenCapture: `${__dirname}/../reports/accessibility/screenshots/{{url}}-{{datetime}}.png`,

    // Reporters
    reporters: [
      [
        'json',
        { fileName: '../reports/accessibility/results.json' }
      ],
      [
        'html',
        { fileName: '../reports/accessibility/index.html' }
      ]
    ],

    // Hide/remove elements that cause false positives
    hideElements: '',
    removeElements: '.advertisement, .third-party-widget',

    // Custom headers (if authentication needed)
    headers: {},

    // Custom actions before testing
    actions: []
  },

  urls: urls
};
```

### URL Configuration

Create `testing/pa11y/urls.json`:

```json
[
  {
    "path": "/",
    "label": "Homepage",
    "priority": "critical"
  },
  {
    "path": "/about",
    "label": "About Page",
    "priority": "high"
  },
  {
    "path": "/programs",
    "label": "Programs Listing",
    "priority": "critical"
  },
  {
    "path": "/programs/youth-development",
    "label": "Program Detail",
    "priority": "high"
  },
  {
    "path": "/locations",
    "label": "Locations Page",
    "priority": "critical"
  },
  {
    "path": "/locations/downtown-ymca",
    "label": "Location Detail",
    "priority": "high"
  },
  {
    "path": "/news",
    "label": "News Listing",
    "priority": "medium"
  },
  {
    "path": "/events",
    "label": "Events Listing",
    "priority": "medium"
  },
  {
    "path": "/contact",
    "label": "Contact Form",
    "priority": "critical"
  },
  {
    "path": "/search",
    "label": "Search Page",
    "priority": "medium"
  },
  {
    "path": "/user/login",
    "label": "Login Page",
    "priority": "high"
  },
  {
    "path": "/user/register",
    "label": "Registration Page",
    "priority": "high"
  }
]
```

## Running Pa11y Tests

### Test Single URL

```bash
cd /private/var/www/YMCAWS_11/testing

# Test single URL
npx pa11y http://yusaopeny.docksal.site/

# Test with specific standard
npx pa11y --standard WCAG2AA http://yusaopeny.docksal.site/

# Test with specific runner
npx pa11y --runner axe http://yusaopeny.docksal.site/

# Include warnings
npx pa11y --include-warnings http://yusaopeny.docksal.site/

# Output to JSON
npx pa11y --reporter json http://yusaopeny.docksal.site/ > report.json
```

### Test Multiple URLs

```bash
# Run Pa11y-CI with configuration file
npx pa11y-ci --config pa11y/.pa11yci.json

# Or using JavaScript config
npx pa11y-ci --config pa11y/pa11y.config.js

# With JSON output
npx pa11y-ci --config pa11y/.pa11yci.json --json > reports/accessibility/results.json
```

### Generate Reports

```bash
# Generate HTML report
npx pa11y-ci \
  --config pa11y/.pa11yci.json \
  --reporter html > reports/accessibility/index.html

# Generate CSV report
npx pa11y-ci \
  --config pa11y/.pa11yci.json \
  --reporter csv > reports/accessibility/results.csv

# Generate multiple report formats
npx pa11y-ci \
  --config pa11y/.pa11yci.json \
  --reporter json > reports/accessibility/results.json && \
npx pa11y-ci \
  --config pa11y/.pa11yci.json \
  --reporter html > reports/accessibility/index.html
```

## Understanding Pa11y Results

### Issue Severity Levels

**Error (Must Fix):**
- Definite WCAG violations
- Will fail compliance audits
- Examples: Missing alt text, insufficient contrast, keyboard traps

**Warning (Should Fix):**
- Potential WCAG violations
- Need manual verification
- Examples: Suspicious link text, possible heading hierarchy issues

**Notice (Review):**
- Best practice suggestions
- Not WCAG violations
- Examples: Recommendations for improvements

### Common WCAG 2.2 AA Issues

#### 1. Missing Alternative Text

```
Error: Images must have alternative text
Code: WCAG2AA.Principle1.Guideline1_1.1_1_1.H37
Element: <img src="/images/banner.jpg">
```

**Fix:**
```html
<!-- Before -->
<img src="/images/banner.jpg">

<!-- After -->
<img src="/images/banner.jpg" alt="Children playing basketball at the YMCA gym">
```

#### 2. Insufficient Color Contrast

```
Error: Text color contrast is less than 4.5:1
Code: WCAG2AA.Principle1.Guideline1_4.1_4_3.G18
Element: <p style="color: #777; background: #fff;">Text</p>
```

**Fix:**
```scss
// Before (contrast ratio: 4.47:1 - fails)
.text-muted {
  color: #777777;
}

// After (contrast ratio: 7.0:1 - passes)
.text-muted {
  color: #6c757d;
}
```

#### 3. Missing Form Labels

```
Error: Form input must have an associated label
Code: WCAG2AA.Principle1.Guideline1_3.1_3_1.H44
Element: <input type="text" name="email">
```

**Fix:**
```html
<!-- Before -->
<input type="text" name="email" placeholder="Email">

<!-- After -->
<label for="email">Email Address</label>
<input type="text" id="email" name="email">
```

#### 4. Incorrect Heading Hierarchy

```
Warning: Heading levels should not skip
Code: WCAG2AA.Principle1.Guideline1_3.1_3_1.H42
Element: <h1>Title</h1><h3>Subtitle</h3>
```

**Fix:**
```html
<!-- Before -->
<h1>Our Programs</h1>
<h3>Youth Development</h3>

<!-- After -->
<h1>Our Programs</h1>
<h2>Youth Development</h2>
```

#### 5. Missing ARIA Labels

```
Error: Button has no accessible name
Code: WCAG2AA.Principle4.Guideline4_1.4_1_2.H91
Element: <button><i class="icon-close"></i></button>
```

**Fix:**
```html
<!-- Before -->
<button><i class="icon-close"></i></button>

<!-- After -->
<button aria-label="Close modal">
  <i class="icon-close" aria-hidden="true"></i>
</button>
```

#### 6. Keyboard Accessibility

```
Error: Interactive element is not keyboard accessible
Code: WCAG2AA.Principle2.Guideline2_1.2_1_1
Element: <div onclick="handleClick()">Click me</div>
```

**Fix:**
```html
<!-- Before -->
<div onclick="handleClick()">Click me</div>

<!-- After -->
<button type="button" onclick="handleClick()">Click me</button>

<!-- Or with div (not recommended) -->
<div role="button" tabindex="0" onclick="handleClick()" onkeypress="handleClick()">
  Click me
</div>
```

## Manual Testing Checklist

Automated tools catch ~30-50% of accessibility issues. Manual testing is essential.

### Keyboard Navigation Testing

**Test all pages for:**

- [ ] **Tab Navigation:** Can you reach all interactive elements with Tab key?
- [ ] **Logical Order:** Does tab order follow visual flow?
- [ ] **Focus Indicators:** Are focused elements clearly visible?
- [ ] **No Keyboard Traps:** Can you tab out of all components?
- [ ] **Enter/Space Activation:** Do buttons/links activate with keyboard?
- [ ] **Escape to Close:** Do modals/dropdowns close with Escape key?
- [ ] **Arrow Keys:** Do custom controls (sliders, tabs) work with arrows?
- [ ] **Skip Links:** Can you skip to main content?

**Testing Procedure:**

```
1. Open page in browser
2. Do NOT use mouse - keyboard only
3. Press Tab repeatedly, verify:
   - Focus moves to all interactive elements
   - Focus indicator is visible (outline or custom style)
   - Order makes sense
4. Press Enter/Space on buttons and links
5. Press Escape on modals and dropdowns
6. Use Arrow keys on carousels, tabs, accordions
7. Verify you can reach and use all functionality
```

### Screen Reader Testing

**Recommended Screen Readers:**

- **Windows:** NVDA (free) or JAWS (paid)
- **macOS:** VoiceOver (built-in)
- **Linux:** Orca (free)
- **Mobile:** TalkBack (Android), VoiceOver (iOS)

**NVDA Testing (Windows):**

```
1. Download NVDA: https://www.nvaccess.org/download/
2. Install and restart computer
3. Launch NVDA (Ctrl + Alt + N)
4. Open site in Firefox or Chrome
5. Navigate with:
   - Down Arrow: Read next item
   - H: Jump to next heading
   - K: Jump to next link
   - F: Jump to next form field
   - Insert + F7: List all elements
6. Verify:
   - All content is announced
   - Images have meaningful alt text
   - Headings describe content
   - Links make sense out of context
   - Form fields have labels
   - Errors are announced
```

**VoiceOver Testing (macOS):**

```
1. Enable VoiceOver: Cmd + F5
2. Open site in Safari
3. Navigate with:
   - VO + Right Arrow: Read next item
   - VO + Cmd + H: Jump to next heading
   - VO + Cmd + L: Jump to next link
   - Tab: Jump to next form field
   - VO + U: Open rotor (element list)
4. Verify same items as NVDA testing above
```

**Screen Reader Checklist:**

- [ ] **All Content Announced:** No silent sections
- [ ] **Meaningful Alt Text:** Images described appropriately
- [ ] **Heading Structure:** Logical heading hierarchy (H1 > H2 > H3)
- [ ] **Link Context:** Link text makes sense without surrounding content
- [ ] **Form Labels:** All inputs have associated labels
- [ ] **Error Announcements:** Form errors are announced
- [ ] **Dynamic Content:** ARIA live regions announce updates
- [ ] **Button Labels:** Buttons have descriptive text or ARIA labels
- [ ] **Navigation Landmarks:** Header, nav, main, footer properly marked

### Color Contrast Testing

**Tools:**

- **Browser Extensions:**
  - WebAIM Color Contrast Checker
  - axe DevTools (Chrome/Firefox)
  - WAVE (Chrome/Firefox)

- **Desktop Apps:**
  - Colour Contrast Analyser (free, Windows/Mac)
  - https://webaim.org/resources/contrastchecker/

**Testing Procedure:**

```
1. Install Colour Contrast Analyser
2. Open site in browser
3. For each text element:
   a. Use eyedropper to select foreground color
   b. Use eyedropper to select background color
   c. Verify contrast ratio:
      - Normal text: ≥ 4.5:1
      - Large text (18pt+/14pt+ bold): ≥ 3:1
      - UI components: ≥ 3:1
4. Test all states:
   - Default
   - Hover
   - Focus
   - Active
   - Disabled
```

**Contrast Checklist:**

- [ ] **Body Text:** Passes 4.5:1 ratio
- [ ] **Headings:** Pass 4.5:1 or 3:1 (if large)
- [ ] **Links:** Pass 4.5:1 ratio
- [ ] **Buttons:** Pass 3:1 for boundaries, 4.5:1 for text
- [ ] **Form Inputs:** Pass 3:1 for borders
- [ ] **Icons:** Pass 3:1 if conveying information
- [ ] **Error Messages:** Pass 4.5:1 ratio
- [ ] **Placeholder Text:** Not relied upon (should pass if used)

### Focus State Testing

**Checklist:**

- [ ] **All Interactive Elements:** Links, buttons, inputs, custom controls
- [ ] **Visible Indicator:** Focus outline or custom style clearly visible
- [ ] **Color Independence:** Don't rely only on color (use outline/underline)
- [ ] **Sufficient Contrast:** Focus indicator has ≥3:1 contrast
- [ ] **No Removal:** Default focus styles not removed without replacement

**Testing:**

```scss
/* BAD - Removes focus outline */
a:focus, button:focus {
  outline: none;
}

/* GOOD - Replaces with custom style */
a:focus, button:focus {
  outline: 2px solid #0056b3;
  outline-offset: 2px;
}

/* BETTER - Enhanced focus style */
a:focus-visible, button:focus-visible {
  outline: 3px solid #0056b3;
  outline-offset: 2px;
  box-shadow: 0 0 0 4px rgba(0, 86, 179, 0.25);
}
```

### Responsive Testing

**Checklist:**

- [ ] **Touch Targets:** Minimum 44x44 pixels on mobile
- [ ] **Text Sizing:** Text readable without zoom at mobile sizes
- [ ] **No Horizontal Scroll:** Content fits viewport width
- [ ] **Reflow:** Content reflows properly at 320px width
- [ ] **Orientation:** Works in portrait and landscape
- [ ] **Zoom:** Usable at 200% zoom (up to 400% for low vision)

### Forms Testing

**Checklist:**

- [ ] **Labels:** All inputs have visible labels
- [ ] **Required Fields:** Marked with asterisk AND aria-required
- [ ] **Error Messages:** Descriptive, announced to screen readers
- [ ] **Error Association:** Errors linked to fields (aria-describedby)
- [ ] **Fieldsets:** Related fields grouped with <fieldset> and <legend>
- [ ] **Autocomplete:** Appropriate autocomplete attributes
- [ ] **Instructions:** Help text available and announced

**Example Accessible Form:**

```html
<form>
  <fieldset>
    <legend>Personal Information</legend>

    <div class="form-group">
      <label for="name">
        Full Name <span aria-label="required">*</span>
      </label>
      <input
        type="text"
        id="name"
        name="name"
        autocomplete="name"
        required
        aria-required="true"
        aria-describedby="name-error"
      >
      <div id="name-error" class="error" role="alert" aria-live="polite">
        <!-- Error message inserted here -->
      </div>
    </div>

    <div class="form-group">
      <label for="email">
        Email Address <span aria-label="required">*</span>
      </label>
      <input
        type="email"
        id="email"
        name="email"
        autocomplete="email"
        required
        aria-required="true"
        aria-describedby="email-help email-error"
      >
      <small id="email-help" class="form-text">
        We'll never share your email with anyone else.
      </small>
      <div id="email-error" class="error" role="alert" aria-live="polite">
        <!-- Error message inserted here -->
      </div>
    </div>
  </fieldset>

  <button type="submit">Submit Form</button>
</form>
```

## Bootstrap 5 Specific Accessibility Testing

### Components to Test

#### 1. Modals

```html
<!-- Ensure proper ARIA attributes -->
<div class="modal fade" id="exampleModal" tabindex="-1" aria-labelledby="exampleModalLabel" aria-hidden="true">
  <div class="modal-dialog">
    <div class="modal-content">
      <div class="modal-header">
        <h5 class="modal-title" id="exampleModalLabel">Modal Title</h5>
        <button type="button" class="btn-close" data-bs-dismiss="modal" aria-label="Close"></button>
      </div>
      <div class="modal-body">
        Modal content
      </div>
    </div>
  </div>
</div>
```

**Test:**
- [ ] Focus trapped in modal when open
- [ ] Escape key closes modal
- [ ] Focus returns to trigger element when closed
- [ ] Screen reader announces modal open/close
- [ ] Close button has accessible name

#### 2. Dropdowns

```html
<div class="dropdown">
  <button class="btn btn-secondary dropdown-toggle" type="button" id="dropdownMenuButton" data-bs-toggle="dropdown" aria-expanded="false">
    Dropdown button
  </button>
  <ul class="dropdown-menu" aria-labelledby="dropdownMenuButton">
    <li><a class="dropdown-item" href="#">Action</a></li>
    <li><a class="dropdown-item" href="#">Another action</a></li>
  </ul>
</div>
```

**Test:**
- [ ] Keyboard accessible (Enter/Space to open, Arrow keys to navigate)
- [ ] Escape closes dropdown
- [ ] aria-expanded updates correctly
- [ ] Focus management correct

#### 3. Accordions

```html
<div class="accordion" id="accordionExample">
  <div class="accordion-item">
    <h2 class="accordion-header" id="headingOne">
      <button class="accordion-button" type="button" data-bs-toggle="collapse" data-bs-target="#collapseOne" aria-expanded="true" aria-controls="collapseOne">
        Accordion Item #1
      </button>
    </h2>
    <div id="collapseOne" class="accordion-collapse collapse show" aria-labelledby="headingOne" data-bs-parent="#accordionExample">
      <div class="accordion-body">
        Content
      </div>
    </div>
  </div>
</div>
```

**Test:**
- [ ] Buttons keyboard accessible
- [ ] aria-expanded updates correctly
- [ ] aria-controls properly set
- [ ] Content announced when expanded

#### 4. Carousels

```html
<div id="carouselExample" class="carousel slide" data-bs-ride="carousel">
  <div class="carousel-indicators">
    <button type="button" data-bs-target="#carouselExample" data-bs-slide-to="0" class="active" aria-current="true" aria-label="Slide 1"></button>
    <button type="button" data-bs-target="#carouselExample" data-bs-slide-to="1" aria-label="Slide 2"></button>
  </div>
  <div class="carousel-inner">
    <div class="carousel-item active">
      <img src="..." class="d-block w-100" alt="Description of slide 1">
    </div>
    <div class="carousel-item">
      <img src="..." class="d-block w-100" alt="Description of slide 2">
    </div>
  </div>
  <button class="carousel-control-prev" type="button" data-bs-target="#carouselExample" data-bs-slide="prev">
    <span class="carousel-control-prev-icon" aria-hidden="true"></span>
    <span class="visually-hidden">Previous</span>
  </button>
  <button class="carousel-control-next" type="button" data-bs-target="#carouselExample" data-bs-slide="next">
    <span class="carousel-control-next-icon" aria-hidden="true"></span>
    <span class="visually-hidden">Next</span>
  </button>
</div>
```

**Test:**
- [ ] All images have alt text
- [ ] Controls keyboard accessible
- [ ] Indicators have labels
- [ ] Can pause auto-play
- [ ] Screen reader announces slide changes

#### 5. Toasts

```html
<div class="toast" role="alert" aria-live="assertive" aria-atomic="true">
  <div class="toast-header">
    <strong class="me-auto">Bootstrap</strong>
    <button type="button" class="btn-close" data-bs-dismiss="toast" aria-label="Close"></button>
  </div>
  <div class="toast-body">
    Hello, world! This is a toast message.
  </div>
</div>
```

**Test:**
- [ ] aria-live="assertive" or "polite" set
- [ ] Screen reader announces content
- [ ] Close button accessible

## CI/CD Integration

### GitHub Actions Workflow

Create `.github/workflows/accessibility-tests.yml`:

```yaml
name: Accessibility Tests

on:
  push:
    branches: [ bs_4_to_5 ]
  pull_request:
    branches: [ main ]

jobs:
  pa11y:
    runs-on: ubuntu-latest

    steps:
      - uses: actions/checkout@v3

      - name: Setup Node.js
        uses: actions/setup-node@v3
        with:
          node-version: '18'
          cache: 'npm'
          cache-dependency-path: testing/package-lock.json

      - name: Install dependencies
        run: |
          cd testing
          npm ci

      - name: Run Pa11y tests
        run: |
          cd testing
          npx pa11y-ci --config pa11y/.pa11yci.json --json > reports/accessibility/results.json
        continue-on-error: true

      - name: Generate HTML report
        if: always()
        run: |
          cd testing
          npx pa11y-ci --config pa11y/.pa11yci.json --reporter html > reports/accessibility/index.html

      - name: Upload accessibility reports
        if: always()
        uses: actions/upload-artifact@v3
        with:
          name: accessibility-reports
          path: testing/reports/accessibility/
          retention-days: 30

      - name: Check for critical issues
        run: |
          cd testing
          ERROR_COUNT=$(jq '[.[] | select(.issues != null) | .issues | length] | add' reports/accessibility/results.json)
          echo "Total accessibility errors: $ERROR_COUNT"
          if [ "$ERROR_COUNT" -gt 0 ]; then
            echo "::error::Found $ERROR_COUNT accessibility errors"
            exit 1
          fi
```

### NPM Scripts

Add to `testing/package.json`:

```json
{
  "scripts": {
    "test:a11y": "pa11y-ci --config pa11y/.pa11yci.json",
    "test:a11y:json": "pa11y-ci --config pa11y/.pa11yci.json --json > reports/accessibility/results.json",
    "test:a11y:html": "pa11y-ci --config pa11y/.pa11yci.json --reporter html > reports/accessibility/index.html",
    "test:a11y:single": "pa11y --standard WCAG2AA",
    "report:a11y": "open reports/accessibility/index.html"
  }
}
```

## Best Practices

### 1. Test Early and Often

```bash
# Test during development
npm run test:a11y:single -- http://localhost:3000/new-component

# Test before committing
npm run test:a11y
```

### 2. Fix Issues at the Source

Don't just fix Pa11y errors - understand the underlying issue and fix it properly.

### 3. Use Semantic HTML

```html
<!-- Bad -->
<div class="button" onclick="submit()">Submit</div>

<!-- Good -->
<button type="submit">Submit</button>
```

### 4. Progressive Enhancement

Build accessible foundation first, then enhance.

### 5. Test with Real Users

Automated and manual testing don't catch everything. Test with users who rely on assistive technology.

## Resources

### Testing Tools

- Pa11y: https://github.com/pa11y/pa11y
- axe DevTools: https://www.deque.com/axe/devtools/
- WAVE: https://wave.webaim.org/
- Lighthouse: https://developers.google.com/web/tools/lighthouse

### Guidelines

- WCAG 2.2: https://www.w3.org/WAI/WCAG22/quickref/
- WebAIM: https://webaim.org/
- A11y Project: https://www.a11yproject.com/

### Screen Readers

- NVDA: https://www.nvaccess.org/
- JAWS: https://www.freedomscientific.com/products/software/jaws/
- VoiceOver: Built into macOS/iOS

## Conclusion

Accessibility testing ensures your Bootstrap 5 migration maintains WCAG 2.2 Level AA compliance. Use Pa11y for automated testing, but supplement with manual keyboard, screen reader, and color contrast testing. Remember that accessibility is an ongoing commitment, not a one-time checklist.
