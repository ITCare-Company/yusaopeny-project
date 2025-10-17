# Visual Regression Testing with BackstopJS

## Overview

Visual regression testing compares screenshots of your site before and after the Bootstrap 5 migration to identify unintended visual changes. BackstopJS automates this process, making it easy to catch layout shifts, styling issues, and responsive design problems.

## Why BackstopJS?

- **Automated Screenshot Comparison:** Pixel-by-pixel comparison with configurable thresholds
- **Multiple Viewports:** Test responsive designs across devices
- **Headless Browser:** Fast, automated testing using Puppeteer
- **Interactive Reports:** HTML reports with side-by-side comparisons
- **CI/CD Integration:** Runs in continuous integration pipelines
- **Scenario-Based:** Test specific user interactions and states

## Installation

### Prerequisites

```bash
# Node.js 18+ and npm
node --version  # v18.0.0 or higher

# Chrome/Chromium (installed automatically with Puppeteer)
```

### Install BackstopJS

```bash
# Navigate to testing directory
cd /private/var/www/YMCAWS_11/testing

# Install BackstopJS
npm install --save-dev backstopjs

# Verify installation
npx backstop version
```

### Initialize BackstopJS

```bash
# Create backstop directory
mkdir -p backstop
cd backstop

# Initialize configuration
npx backstop init

# This creates:
# backstop/
# ├── backstop.json          # Main configuration file
# └── backstop_data/         # Test data and reports
#     ├── engine_scripts/    # Custom scripts
#     ├── html_report/       # HTML reports
#     ├── ci_report/         # CI reports
#     └── bitmaps_reference/ # Reference screenshots
#     └── bitmaps_test/      # Test screenshots
```

## Configuration

### Basic Configuration

Edit `backstop/backstop.json`:

```json
{
  "id": "ymca_bootstrap5_migration",
  "viewports": [
    {
      "label": "phone",
      "width": 375,
      "height": 667
    },
    {
      "label": "tablet",
      "width": 768,
      "height": 1024
    },
    {
      "label": "desktop",
      "width": 1920,
      "height": 1080
    }
  ],
  "scenarios": [],
  "paths": {
    "bitmaps_reference": "backstop_data/bitmaps_reference",
    "bitmaps_test": "backstop_data/bitmaps_test",
    "engine_scripts": "backstop_data/engine_scripts",
    "html_report": "backstop_data/html_report",
    "ci_report": "backstop_data/ci_report"
  },
  "report": ["browser", "CI"],
  "engine": "puppeteer",
  "engineOptions": {
    "args": ["--no-sandbox", "--disable-setuid-sandbox"]
  },
  "asyncCaptureLimit": 5,
  "asyncCompareLimit": 50,
  "debug": false,
  "debugWindow": false,
  "resembleOutputOptions": {
    "errorColor": {
      "red": 255,
      "green": 0,
      "blue": 255
    },
    "errorType": "movement",
    "transparency": 0.3,
    "ignoreAntialiasing": true,
    "scaleToSameSize": true
  }
}
```

### Advanced Configuration

For more control, create `backstop/backstop.config.js`:

```javascript
const fs = require('fs');

// Load environment variables
require('dotenv').config({ path: '../.env.testing' });

const BASE_URL_BEFORE = process.env.BASE_URL_BEFORE || 'http://yusaopeny.docksal.site';
const BASE_URL_AFTER = process.env.BASE_URL_AFTER || 'http://yusaopeny-bs5.docksal.site';

// Determine which URL to use based on command
const isReference = process.argv.includes('reference');
const BASE_URL = isReference ? BASE_URL_BEFORE : BASE_URL_AFTER;

module.exports = {
  id: 'ymca_bootstrap5_migration',
  viewports: [
    {
      label: 'phone',
      width: 375,
      height: 667
    },
    {
      label: 'tablet',
      width: 768,
      height: 1024
    },
    {
      label: 'desktop',
      width: 1920,
      height: 1080
    },
    {
      label: 'desktop_xl',
      width: 2560,
      height: 1440
    }
  ],
  scenarios: loadScenarios(BASE_URL),
  paths: {
    bitmaps_reference: 'backstop_data/bitmaps_reference',
    bitmaps_test: 'backstop_data/bitmaps_test',
    engine_scripts: 'backstop_data/engine_scripts',
    html_report: 'backstop_data/html_report',
    ci_report: 'backstop_data/ci_report'
  },
  report: ['browser', 'CI'],
  engine: 'puppeteer',
  engineOptions: {
    args: [
      '--no-sandbox',
      '--disable-setuid-sandbox',
      '--disable-dev-shm-usage'
    ],
    executablePath: process.env.CHROME_PATH || undefined,
    headless: 'new'
  },
  asyncCaptureLimit: 5,
  asyncCompareLimit: 50,
  debug: false,
  debugWindow: false,
  resembleOutputOptions: {
    errorColor: {
      red: 255,
      green: 0,
      blue: 255
    },
    errorType: 'movement',
    transparency: 0.3,
    ignoreAntialiasing: true,
    scaleToSameSize: true
  },
  misMatchThreshold: 0.1  // 0.1% difference allowed
};

function loadScenarios(baseUrl) {
  // Load scenarios from external file for easier management
  const scenariosPath = './scenarios.json';
  if (fs.existsSync(scenariosPath)) {
    const scenarios = JSON.parse(fs.readFileSync(scenariosPath, 'utf8'));
    return scenarios.map(scenario => ({
      ...scenario,
      url: `${baseUrl}${scenario.path}`
    }));
  }
  return [];
}
```

## Scenario Creation

### Basic Scenarios

Create `backstop/scenarios.json`:

```json
[
  {
    "label": "Homepage",
    "path": "/",
    "delay": 2000,
    "misMatchThreshold": 0.1
  },
  {
    "label": "About Page",
    "path": "/about",
    "delay": 2000
  },
  {
    "label": "Programs Page",
    "path": "/programs",
    "delay": 2000
  },
  {
    "label": "Locations Page",
    "path": "/locations",
    "delay": 2000
  },
  {
    "label": "News Listing",
    "path": "/news",
    "delay": 2000
  },
  {
    "label": "Events Listing",
    "path": "/events",
    "delay": 2000
  },
  {
    "label": "Contact Page",
    "path": "/contact",
    "delay": 2000
  }
]
```

### Advanced Scenarios with Interactions

```json
[
  {
    "label": "Homepage - Mobile Menu",
    "path": "/",
    "delay": 1000,
    "clickSelector": ".navbar-toggler",
    "postInteractionWait": 1000,
    "viewports": [
      {
        "label": "phone",
        "width": 375,
        "height": 667
      }
    ]
  },
  {
    "label": "Programs - Accordion Expanded",
    "path": "/programs",
    "delay": 1000,
    "clickSelectors": [
      "#accordion-item-1 .accordion-button",
      "#accordion-item-2 .accordion-button"
    ],
    "postInteractionWait": 500
  },
  {
    "label": "Homepage - Modal Open",
    "path": "/",
    "delay": 1000,
    "clickSelector": "[data-bs-toggle='modal']",
    "postInteractionWait": 1000
  },
  {
    "label": "Search Results",
    "path": "/search?query=swim",
    "delay": 2000
  },
  {
    "label": "Form - Focus States",
    "path": "/contact",
    "delay": 1000,
    "focusSelector": "#edit-name",
    "postInteractionWait": 500
  },
  {
    "label": "Carousel - Second Slide",
    "path": "/",
    "delay": 2000,
    "clickSelector": ".carousel-control-next",
    "postInteractionWait": 1000
  },
  {
    "label": "Dropdown - Expanded",
    "path": "/",
    "delay": 1000,
    "hoverSelector": ".nav-item.dropdown",
    "postInteractionWait": 500
  }
]
```

### Custom Scenarios with Engine Scripts

For complex interactions, use custom Puppeteer scripts.

Create `backstop/backstop_data/engine_scripts/custom/login.js`:

```javascript
module.exports = async (page, scenario, viewport, isReference, Engine, config) => {
  const loginUrl = scenario.loginUrl;

  if (loginUrl) {
    // Navigate to login page
    await page.goto(loginUrl, { waitUntil: 'networkidle0' });

    // Fill in login form
    await page.type('#edit-name', 'testuser');
    await page.type('#edit-pass', 'testpassword');

    // Submit form
    await page.click('#edit-submit');

    // Wait for redirect
    await page.waitForNavigation({ waitUntil: 'networkidle0' });
  }

  // Continue with regular scenario
  await require('./puppet/onBefore')(page, scenario, viewport, isReference, Engine, config);
};
```

Use in scenario:

```json
{
  "label": "User Dashboard (Authenticated)",
  "path": "/user/dashboard",
  "loginUrl": "http://yusaopeny.docksal.site/user/login",
  "onBeforeScript": "engine_scripts/custom/login.js",
  "delay": 2000
}
```

### Selector-Based Scenarios

Test specific components:

```json
[
  {
    "label": "Header Component",
    "path": "/",
    "selectors": ["header.site-header"],
    "delay": 1000
  },
  {
    "label": "Footer Component",
    "path": "/",
    "selectors": ["footer.site-footer"],
    "delay": 1000
  },
  {
    "label": "Hero Banner",
    "path": "/",
    "selectors": [".hero-banner"],
    "delay": 2000
  },
  {
    "label": "News Card",
    "path": "/news",
    "selectors": [".news-card:first-child"],
    "delay": 1000
  },
  {
    "label": "All Buttons",
    "path": "/",
    "selectors": [
      ".btn-primary",
      ".btn-secondary",
      ".btn-success",
      ".btn-danger",
      ".btn-warning",
      ".btn-info"
    ],
    "delay": 1000
  }
]
```

### Scenarios with Hide/Remove Selectors

Hide dynamic content that changes between tests:

```json
{
  "label": "Homepage - No Dynamic Content",
  "path": "/",
  "hideSelectors": [
    ".social-feed",
    ".twitter-timeline",
    ".instagram-feed",
    ".live-chat-widget",
    "[data-dynamic='true']"
  ],
  "removeSelectors": [
    ".advertisement",
    ".third-party-widget"
  ],
  "delay": 2000
}
```

## Running Tests

### Generate Reference Screenshots (Baseline)

Before migrating to Bootstrap 5, capture reference screenshots:

```bash
cd /private/var/www/YMCAWS_11/testing/backstop

# Ensure you're pointing to BS4 site
export BASE_URL_BEFORE=http://yusaopeny.docksal.site

# Generate reference screenshots
npx backstop reference

# This creates screenshots in:
# backstop_data/bitmaps_reference/
```

### Run Visual Regression Tests

After migrating to Bootstrap 5, run tests to compare:

```bash
# Point to BS5 site
export BASE_URL_AFTER=http://yusaopeny-bs5.docksal.site

# Run tests
npx backstop test

# This creates:
# - Test screenshots in backstop_data/bitmaps_test/
# - HTML report in backstop_data/html_report/
# - Opens report in browser automatically
```

### Approve Changes

If differences are intentional (e.g., design improvements):

```bash
# Approve all changes (updates reference screenshots)
npx backstop approve

# Approve specific scenarios (interactive mode)
npx backstop approve --filter="Homepage"
```

### Test Specific Scenarios

```bash
# Test only scenarios matching filter
npx backstop test --filter="Homepage"

# Test multiple scenarios
npx backstop test --filter="Homepage|About"

# Test by viewport
npx backstop test --filter="phone"
```

### CI/CD Mode

For automated testing in CI/CD pipelines:

```bash
# Run tests without opening browser report
npx backstop test --config=backstop.json

# Generate only CI report (JSON)
# Set "report": ["CI"] in backstop.json
```

## Reviewing Results

### HTML Report

After running tests, BackstopJS generates an interactive HTML report:

```bash
# Open report manually
open backstop_data/html_report/index.html

# Or use npm script
npm run report:open:visual
```

### Report Sections

**Summary:**
- Total scenarios tested
- Pass/fail counts
- Overall pass rate

**Failed Tests:**
- Side-by-side comparison (reference vs. test)
- Difference overlay (highlighted in magenta)
- Mismatch percentage
- Viewport information

**Passed Tests:**
- Confirmation of matching screenshots

### Interpreting Results

**Acceptable Differences:**
- Font rendering variations (< 0.5% mismatch)
- Anti-aliasing differences (< 0.3% mismatch)
- Minor color shifts due to rounding (< 0.2% mismatch)
- Intentional design improvements

**Unacceptable Differences:**
- Layout shifts or broken grids
- Missing content
- Overlapping elements
- Incorrect spacing/margins
- Color scheme changes (unless intentional)
- Responsive design issues

### CI Report (JSON)

For programmatic analysis:

```bash
# CI report located at:
# backstop_data/ci_report/xunit.xml
# backstop_data/ci_report/jsonReport.json
```

Parse JSON report:

```javascript
const fs = require('fs');
const report = JSON.parse(
  fs.readFileSync('backstop_data/ci_report/jsonReport.json', 'utf8')
);

console.log(`Total Tests: ${report.tests.length}`);
console.log(`Passed: ${report.tests.filter(t => t.status === 'pass').length}`);
console.log(`Failed: ${report.tests.filter(t => t.status === 'fail').length}`);

// List failed tests
report.tests
  .filter(t => t.status === 'fail')
  .forEach(test => {
    console.log(`FAILED: ${test.pair.label} - ${test.pair.viewportLabel}`);
    console.log(`  Mismatch: ${test.pair.diff.misMatchPercentage}%`);
  });
```

## Common Issues and Solutions

### Issue 1: Dynamic Content Causing Failures

**Problem:** Dates, timestamps, or live feeds change between tests.

**Solution:** Hide or remove dynamic selectors:

```json
{
  "label": "Homepage",
  "path": "/",
  "hideSelectors": [
    ".current-date",
    ".timestamp",
    ".live-feed"
  ],
  "delay": 2000
}
```

### Issue 2: Fonts Not Loading

**Problem:** Custom fonts fail to load, causing text rendering differences.

**Solution:** Increase delay or wait for fonts:

```json
{
  "label": "Homepage",
  "path": "/",
  "delay": 3000,
  "readySelector": "body.fonts-loaded"
}
```

Or use custom script:

```javascript
// backstop_data/engine_scripts/custom/waitForFonts.js
module.exports = async (page, scenario, viewport, isReference, Engine, config) => {
  await page.evaluateOnNewDocument(() => {
    document.fonts.ready.then(() => {
      document.body.classList.add('fonts-loaded');
    });
  });

  await require('./puppet/onBefore')(page, scenario, viewport, isReference, Engine, config);
};
```

### Issue 3: Animations Causing Mismatches

**Problem:** CSS animations or transitions create inconsistent screenshots.

**Solution:** Disable animations globally:

Create `backstop_data/engine_scripts/custom/disableAnimations.js`:

```javascript
module.exports = async (page, scenario, viewport, isReference, Engine, config) => {
  // Disable CSS animations and transitions
  await page.evaluateOnNewDocument(() => {
    const style = document.createElement('style');
    style.innerHTML = `
      *, *::before, *::after {
        animation-duration: 0s !important;
        animation-delay: 0s !important;
        transition-duration: 0s !important;
        transition-delay: 0s !important;
      }
    `;
    document.head.appendChild(style);
  });

  await require('./puppet/onBefore')(page, scenario, viewport, isReference, Engine, config);
};
```

Apply to all scenarios:

```json
{
  "onBeforeScript": "engine_scripts/custom/disableAnimations.js"
}
```

### Issue 4: Images Not Loading

**Problem:** External images fail to load, causing differences.

**Solution:** Wait for images to load:

```json
{
  "label": "Homepage",
  "path": "/",
  "delay": 2000,
  "readyEvent": "load",
  "readySelector": "img[src]"
}
```

Or use custom script:

```javascript
module.exports = async (page, scenario, viewport, isReference, Engine, config) => {
  await page.goto(scenario.url, { waitUntil: 'networkidle0' });

  // Wait for all images to load
  await page.evaluate(() => {
    return Promise.all(
      Array.from(document.images)
        .filter(img => !img.complete)
        .map(img => new Promise(resolve => {
          img.addEventListener('load', resolve);
          img.addEventListener('error', resolve);
        }))
    );
  });

  await require('./puppet/onBefore')(page, scenario, viewport, isReference, Engine, config);
};
```

### Issue 5: Cookie Banners or Popups

**Problem:** Cookie consent banners appear inconsistently.

**Solution:** Dismiss or hide banners:

```javascript
// backstop_data/engine_scripts/custom/dismissPopups.js
module.exports = async (page, scenario, viewport, isReference, Engine, config) => {
  await page.goto(scenario.url, { waitUntil: 'networkidle0' });

  // Dismiss cookie banner
  const cookieBanner = await page.$('.cookie-banner .accept-button');
  if (cookieBanner) {
    await cookieBanner.click();
    await page.waitForTimeout(500);
  }

  // Close any modals
  const closeButton = await page.$('[data-bs-dismiss="modal"]');
  if (closeButton) {
    await closeButton.click();
    await page.waitForTimeout(500);
  }

  await require('./puppet/onBefore')(page, scenario, viewport, isReference, Engine, config);
};
```

### Issue 6: Viewport Height Differences

**Problem:** Page height varies between reference and test.

**Solution:** Use full-page screenshots:

```json
{
  "label": "Homepage",
  "path": "/",
  "requireSameDimensions": false,
  "delay": 2000
}
```

Or set specific viewport height:

```json
{
  "viewports": [
    {
      "label": "desktop",
      "width": 1920,
      "height": 5000
    }
  ]
}
```

### Issue 7: Slow Network Requests

**Problem:** Third-party scripts delay page load.

**Solution:** Block unnecessary requests:

```javascript
module.exports = async (page, scenario, viewport, isReference, Engine, config) => {
  // Block analytics and tracking scripts
  await page.setRequestInterception(true);

  page.on('request', request => {
    const blockedDomains = [
      'google-analytics.com',
      'googletagmanager.com',
      'facebook.com',
      'twitter.com'
    ];

    const url = request.url();
    const shouldBlock = blockedDomains.some(domain => url.includes(domain));

    if (shouldBlock) {
      request.abort();
    } else {
      request.continue();
    }
  });

  await require('./puppet/onBefore')(page, scenario, viewport, isReference, Engine, config);
};
```

### Issue 8: Tests Failing in CI but Passing Locally

**Problem:** Environment differences between local and CI.

**Solution:** Ensure consistent Chrome version and settings:

```json
{
  "engineOptions": {
    "args": [
      "--no-sandbox",
      "--disable-setuid-sandbox",
      "--disable-dev-shm-usage",
      "--disable-gpu",
      "--force-device-scale-factor=1"
    ],
    "headless": "new"
  }
}
```

Use specific Chrome version in CI:

```yaml
# .github/workflows/visual-regression.yml
- name: Install Chrome
  run: |
    wget -q https://dl.google.com/linux/chrome/deb/pool/main/g/google-chrome-stable/google-chrome-stable_114.0.5735.90-1_amd64.deb
    sudo dpkg -i google-chrome-stable_114.0.5735.90-1_amd64.deb
```

## Best Practices

### 1. Organize Scenarios by Priority

```json
{
  "scenarios": [
    // Critical pages (must pass)
    { "label": "Homepage", "path": "/", "critical": true },
    { "label": "Programs", "path": "/programs", "critical": true },

    // Important pages (should pass)
    { "label": "About", "path": "/about" },
    { "label": "Contact", "path": "/contact" },

    // Nice-to-have (can defer)
    { "label": "Archive", "path": "/news/archive" }
  ]
}
```

### 2. Use Reasonable Delays

```json
// Too short - content may not load
{ "delay": 100 }

// Good - allows content to load
{ "delay": 1000 }

// Too long - wastes time
{ "delay": 10000 }
```

### 3. Set Appropriate Mismatch Thresholds

```json
{
  "scenarios": [
    {
      "label": "Static Content",
      "path": "/about",
      "misMatchThreshold": 0.1  // Strict
    },
    {
      "label": "Dynamic Feed",
      "path": "/news",
      "misMatchThreshold": 2.0  // Lenient
    }
  ]
}
```

### 4. Test Component States

```json
{
  "scenarios": [
    { "label": "Button - Default", "selectors": [".btn-primary"] },
    { "label": "Button - Hover", "selectors": [".btn-primary"], "hoverSelector": ".btn-primary" },
    { "label": "Button - Focus", "selectors": [".btn-primary"], "focusSelector": ".btn-primary" },
    { "label": "Button - Active", "selectors": [".btn-primary"], "clickSelector": ".btn-primary" }
  ]
}
```

### 5. Use Descriptive Labels

```json
// Bad
{ "label": "Test 1", "path": "/" }

// Good
{ "label": "Homepage - Desktop - Logged Out", "path": "/" }
```

### 6. Version Control Reference Screenshots

```bash
# Add reference screenshots to git
git add backstop/backstop_data/bitmaps_reference/
git commit -m "Add visual regression baselines for Bootstrap 4"

# After migration approval
git add backstop/backstop_data/bitmaps_reference/
git commit -m "Update visual regression baselines for Bootstrap 5"
```

### 7. Regular Baseline Updates

```bash
# Periodically update baselines to reflect approved changes
npx backstop approve

# Commit updated baselines
git add backstop/backstop_data/bitmaps_reference/
git commit -m "Update visual regression baselines - $(date +%Y-%m-%d)"
```

## Integration Examples

### NPM Scripts

Add to `testing/package.json`:

```json
{
  "scripts": {
    "backstop:ref": "cd backstop && backstop reference",
    "backstop:test": "cd backstop && backstop test",
    "backstop:approve": "cd backstop && backstop approve",
    "backstop:report": "open backstop/backstop_data/html_report/index.html",
    "backstop:clean": "rm -rf backstop/backstop_data/bitmaps_test backstop/backstop_data/html_report"
  }
}
```

### Makefile

Create `testing/Makefile`:

```makefile
.PHONY: backstop-ref backstop-test backstop-approve backstop-clean

backstop-ref:
	cd backstop && npx backstop reference

backstop-test:
	cd backstop && npx backstop test

backstop-approve:
	cd backstop && npx backstop approve

backstop-clean:
	rm -rf backstop/backstop_data/bitmaps_test
	rm -rf backstop/backstop_data/html_report

backstop-full: backstop-clean backstop-ref backstop-test
```

### Docker Integration

Create `testing/Dockerfile.backstop`:

```dockerfile
FROM node:18-alpine

RUN apk add --no-cache \
    chromium \
    nss \
    freetype \
    freetype-dev \
    harfbuzz \
    ca-certificates \
    ttf-freefont

ENV PUPPETEER_SKIP_CHROMIUM_DOWNLOAD=true \
    PUPPETEER_EXECUTABLE_PATH=/usr/bin/chromium-browser

WORKDIR /app

COPY package*.json ./
RUN npm ci

COPY backstop/ ./backstop/

CMD ["npx", "backstop", "test"]
```

Run in Docker:

```bash
docker build -t ymca-backstop -f Dockerfile.backstop .
docker run --rm -v $(pwd)/backstop:/app/backstop ymca-backstop
```

## Conclusion

Visual regression testing with BackstopJS ensures your Bootstrap 5 migration maintains visual consistency while catching unintended layout changes. Follow this guide to set up comprehensive visual testing, create meaningful scenarios, and integrate tests into your development workflow.

For questions or advanced use cases, refer to the official BackstopJS documentation: https://github.com/garris/BackstopJS
