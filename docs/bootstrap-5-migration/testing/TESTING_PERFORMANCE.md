# Performance Testing - Bootstrap 5 Migration

## Overview

Performance testing ensures that the Bootstrap 5 migration maintains or improves site speed, user experience, and Core Web Vitals metrics. This guide covers performance testing with Lighthouse CI, bundle analysis, optimization strategies, and monitoring.

## Why Performance Testing?

- **User Experience:** Fast sites have better engagement and conversion rates
- **SEO Rankings:** Google uses Core Web Vitals as ranking signals
- **Business Impact:** 1-second delay can reduce conversions by 7%
- **Accessibility:** Performance is an accessibility concern for users with slow connections
- **Cost Savings:** Optimized sites reduce bandwidth and infrastructure costs

## Core Web Vitals

Google's Core Web Vitals measure real-world user experience:

### 1. Largest Contentful Paint (LCP)

**What:** Time until largest content element is visible
**Good:** ≤ 2.5 seconds
**Needs Improvement:** 2.5-4.0 seconds
**Poor:** > 4.0 seconds

**Measures:** Loading performance

### 2. First Input Delay (FID)

**What:** Time from first interaction to browser response
**Good:** ≤ 100 milliseconds
**Needs Improvement:** 100-300 milliseconds
**Poor:** > 300 milliseconds

**Measures:** Interactivity

**Note:** FID is being replaced by Interaction to Next Paint (INP) in 2024.

### 3. Cumulative Layout Shift (CLS)

**What:** Visual stability - how much content shifts during load
**Good:** ≤ 0.1
**Needs Improvement:** 0.1-0.25
**Poor:** > 0.25

**Measures:** Visual stability

### 4. Interaction to Next Paint (INP) - New in 2024

**What:** Responsiveness of all user interactions
**Good:** ≤ 200 milliseconds
**Needs Improvement:** 200-500 milliseconds
**Poor:** > 500 milliseconds

**Measures:** Overall responsiveness

## Lighthouse CI Setup

### Installation

```bash
# Navigate to testing directory
cd /private/var/www/YMCAWS_11/testing

# Install Lighthouse CI
npm install --save-dev @lhci/cli

# Verify installation
npx lhci --version
```

### Basic Configuration

Create `testing/lighthouse/lighthouserc.json`:

```json
{
  "ci": {
    "collect": {
      "url": [
        "http://yusaopeny.docksal.site/",
        "http://yusaopeny.docksal.site/about",
        "http://yusaopeny.docksal.site/programs",
        "http://yusaopeny.docksal.site/locations"
      ],
      "numberOfRuns": 3,
      "settings": {
        "preset": "desktop",
        "throttlingMethod": "simulate",
        "screenEmulation": {
          "mobile": false,
          "width": 1920,
          "height": 1080,
          "deviceScaleFactor": 1,
          "disabled": false
        },
        "formFactor": "desktop"
      }
    },
    "assert": {
      "preset": "lighthouse:recommended",
      "assertions": {
        "categories:performance": ["error", {"minScore": 0.9}],
        "categories:accessibility": ["error", {"minScore": 0.9}],
        "categories:best-practices": ["error", {"minScore": 0.9}],
        "categories:seo": ["error", {"minScore": 0.9}],
        "first-contentful-paint": ["warn", {"maxNumericValue": 2000}],
        "largest-contentful-paint": ["error", {"maxNumericValue": 2500}],
        "cumulative-layout-shift": ["error", {"maxNumericValue": 0.1}],
        "total-blocking-time": ["warn", {"maxNumericValue": 300}]
      }
    },
    "upload": {
      "target": "filesystem",
      "outputDir": "../reports/performance/lighthouse"
    }
  }
}
```

### Advanced Configuration

Create `testing/lighthouse/lighthouserc.js`:

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
  urls = [`${BASE_URL}/`];
}

module.exports = {
  ci: {
    collect: {
      url: urls,
      numberOfRuns: 3,
      settings: {
        preset: 'desktop',
        throttlingMethod: 'simulate',
        throttling: {
          rttMs: 40,
          throughputKbps: 10 * 1024,
          cpuSlowdownMultiplier: 1,
          requestLatencyMs: 0,
          downloadThroughputKbps: 0,
          uploadThroughputKbps: 0
        },
        screenEmulation: {
          mobile: false,
          width: 1920,
          height: 1080,
          deviceScaleFactor: 1,
          disabled: false
        },
        formFactor: 'desktop',
        onlyCategories: ['performance', 'accessibility', 'best-practices', 'seo'],
        skipAudits: ['uses-http2']  // Skip audits not relevant to local testing
      },
      startServerCommand: null,  // Set if need to start local server
      startServerReadyPattern: null,
      startServerReadyTimeout: 10000
    },
    assert: {
      preset: 'lighthouse:recommended',
      assertions: {
        // Performance category
        'categories:performance': ['error', { minScore: 0.9 }],
        'categories:accessibility': ['error', { minScore: 0.9 }],
        'categories:best-practices': ['error', { minScore: 0.9 }],
        'categories:seo': ['error', { minScore: 0.9 }],

        // Core Web Vitals
        'first-contentful-paint': ['warn', { maxNumericValue: 1800 }],
        'largest-contentful-paint': ['error', { maxNumericValue: 2500 }],
        'cumulative-layout-shift': ['error', { maxNumericValue: 0.1 }],
        'total-blocking-time': ['warn', { maxNumericValue: 300 }],
        'speed-index': ['warn', { maxNumericValue: 3400 }],

        // Resource budgets
        'resource-summary:script:size': ['error', { maxNumericValue: 153600 }], // 150 KB
        'resource-summary:stylesheet:size': ['error', { maxNumericValue: 51200 }], // 50 KB
        'resource-summary:image:size': ['warn', { maxNumericValue: 512000 }], // 500 KB
        'resource-summary:total:size': ['warn', { maxNumericValue: 1024000 }], // 1 MB

        // Best practices
        'errors-in-console': 'off',  // Can be noisy, enable if needed
        'uses-optimized-images': 'warn',
        'modern-image-formats': 'warn',
        'uses-text-compression': 'error',
        'uses-responsive-images': 'warn',
        'offscreen-images': 'warn',
        'unminified-css': 'error',
        'unminified-javascript': 'error',
        'unused-css-rules': 'warn',
        'unused-javascript': 'warn',
        'server-response-time': ['error', { maxNumericValue: 600 }]
      }
    },
    upload: {
      target: 'filesystem',
      outputDir: '../reports/performance/lighthouse',
      reportFilenamePattern: '%%PATHNAME%%-%%DATETIME%%.report.%%EXTENSION%%'
    }
  }
};
```

### Performance Budget

Create `testing/lighthouse/lighthouse-budget.json`:

```json
{
  "budgets": [
    {
      "path": "/*",
      "resourceSizes": [
        {
          "resourceType": "stylesheet",
          "budget": 50
        },
        {
          "resourceType": "script",
          "budget": 150
        },
        {
          "resourceType": "image",
          "budget": 500
        },
        {
          "resourceType": "font",
          "budget": 100
        },
        {
          "resourceType": "total",
          "budget": 1000
        }
      ],
      "resourceCounts": [
        {
          "resourceType": "script",
          "budget": 10
        },
        {
          "resourceType": "stylesheet",
          "budget": 5
        },
        {
          "resourceType": "third-party",
          "budget": 10
        }
      ],
      "timings": [
        {
          "metric": "first-contentful-paint",
          "budget": 2000
        },
        {
          "metric": "largest-contentful-paint",
          "budget": 2500
        },
        {
          "metric": "cumulative-layout-shift",
          "budget": 0.1
        },
        {
          "metric": "total-blocking-time",
          "budget": 300
        },
        {
          "metric": "speed-index",
          "budget": 3400
        },
        {
          "metric": "interactive",
          "budget": 3800
        }
      ]
    }
  ]
}
```

Use budget in configuration:

```json
{
  "ci": {
    "collect": {
      "settings": {
        "budgets": "lighthouse-budget.json"
      }
    }
  }
}
```

## Running Performance Tests

### Run Lighthouse CI

```bash
cd /private/var/www/YMCAWS_11/testing

# Run with default configuration
npx lhci autorun --config=lighthouse/lighthouserc.json

# Run and upload to temporary public storage
npx lhci autorun --upload.target=temporary-public-storage

# Run specific URLs only
npx lhci collect --url=http://yusaopeny.docksal.site/
```

### Run Individual Lighthouse Audits

```bash
# Single URL audit
npx lighthouse http://yusaopeny.docksal.site/ \
  --output html \
  --output-path reports/performance/homepage.html

# With specific categories
npx lighthouse http://yusaopeny.docksal.site/ \
  --only-categories=performance,accessibility \
  --output json \
  --output-path reports/performance/homepage.json

# Mobile audit
npx lighthouse http://yusaopeny.docksal.site/ \
  --preset=mobile \
  --output html \
  --output-path reports/performance/homepage-mobile.html

# Desktop audit
npx lighthouse http://yusaopeny.docksal.site/ \
  --preset=desktop \
  --output html \
  --output-path reports/performance/homepage-desktop.html
```

### Compare Before/After

```bash
# Capture baseline (Bootstrap 4)
export BASE_URL_BEFORE=http://yusaopeny.docksal.site
npx lhci autorun --config=lighthouse/lighthouserc.js
mv reports/performance/lighthouse reports/performance/baseline

# Capture after migration (Bootstrap 5)
export BASE_URL_AFTER=http://yusaopeny-bs5.docksal.site
npx lhci autorun --config=lighthouse/lighthouserc.js

# Compare results
node scripts/compare-performance.js
```

Create comparison script at `testing/scripts/compare-performance.js`:

```javascript
const fs = require('fs');
const path = require('path');

const baselineDir = path.join(__dirname, '../reports/performance/baseline');
const currentDir = path.join(__dirname, '../reports/performance/lighthouse');

function getLatestReport(dir) {
  const files = fs.readdirSync(dir).filter(f => f.endsWith('.json'));
  const latest = files.sort().reverse()[0];
  return JSON.parse(fs.readFileSync(path.join(dir, latest), 'utf8'));
}

function compareMetrics(baseline, current) {
  const metrics = [
    'first-contentful-paint',
    'largest-contentful-paint',
    'total-blocking-time',
    'cumulative-layout-shift',
    'speed-index'
  ];

  console.log('\n=== Performance Comparison ===\n');

  metrics.forEach(metric => {
    const baselineValue = baseline.audits[metric].numericValue;
    const currentValue = current.audits[metric].numericValue;
    const diff = currentValue - baselineValue;
    const diffPercent = ((diff / baselineValue) * 100).toFixed(2);
    const emoji = diff < 0 ? '✅' : diff > 0 ? '❌' : '➖';

    console.log(`${emoji} ${metric}:`);
    console.log(`   Baseline: ${baselineValue.toFixed(2)}`);
    console.log(`   Current:  ${currentValue.toFixed(2)}`);
    console.log(`   Diff:     ${diff.toFixed(2)} (${diffPercent}%)`);
    console.log('');
  });

  // Overall scores
  console.log('\n=== Category Scores ===\n');

  ['performance', 'accessibility', 'best-practices', 'seo'].forEach(category => {
    const baselineScore = baseline.categories[category].score * 100;
    const currentScore = current.categories[category].score * 100;
    const diff = currentScore - baselineScore;
    const emoji = diff > 0 ? '✅' : diff < 0 ? '❌' : '➖';

    console.log(`${emoji} ${category}: ${baselineScore} → ${currentScore} (${diff > 0 ? '+' : ''}${diff})`);
  });
}

try {
  const baseline = getLatestReport(baselineDir);
  const current = getLatestReport(currentDir);
  compareMetrics(baseline, current);
} catch (error) {
  console.error('Error comparing reports:', error.message);
}
```

## Understanding Lighthouse Results

### Performance Score Breakdown

**Weighting (as of Lighthouse 10):**

- First Contentful Paint: 10%
- Speed Index: 10%
- Largest Contentful Paint: 25%
- Total Blocking Time: 30%
- Cumulative Layout Shift: 25%

### Common Performance Issues

#### 1. Large JavaScript Bundles

```
Opportunity: Reduce JavaScript execution time
Savings: 2.4 s
```

**Solutions:**

```bash
# Analyze bundle size
npm install --save-dev webpack-bundle-analyzer

# Add to webpack config
const BundleAnalyzerPlugin = require('webpack-bundle-analyzer').BundleAnalyzerPlugin;

module.exports = {
  plugins: [
    new BundleAnalyzerPlugin({
      analyzerMode: 'static',
      openAnalyzer: false,
      reportFilename: 'bundle-report.html'
    })
  ]
};

# Run build and review report
npm run build
open dist/bundle-report.html
```

**Optimization strategies:**

```javascript
// 1. Code splitting
// Before: All code in one bundle
import { Modal } from 'bootstrap';

// After: Dynamic imports
const modal = document.querySelector('#myModal');
if (modal) {
  import('bootstrap/js/dist/modal').then(({ default: Modal }) => {
    new Modal(modal);
  });
}

// 2. Tree shaking - Import only what you need
// Before: Entire Bootstrap
import 'bootstrap';

// After: Specific components
import Modal from 'bootstrap/js/dist/modal';
import Collapse from 'bootstrap/js/dist/collapse';

// 3. Remove unused dependencies
npm uninstall unused-package
```

#### 2. Render-Blocking Resources

```
Opportunity: Eliminate render-blocking resources
Savings: 1.2 s
```

**Solutions:**

```html
<!-- Before: Blocking CSS -->
<link rel="stylesheet" href="/css/bootstrap.min.css">
<link rel="stylesheet" href="/css/custom.css">

<!-- After: Critical CSS inline, defer non-critical -->
<style>
  /* Critical CSS inlined here */
  body { margin: 0; font-family: sans-serif; }
  header { background: #000; color: #fff; }
</style>

<link rel="preload" href="/css/bootstrap.min.css" as="style" onload="this.onload=null;this.rel='stylesheet'">
<noscript><link rel="stylesheet" href="/css/bootstrap.min.css"></noscript>

<!-- Defer JavaScript -->
<script src="/js/bootstrap.bundle.min.js" defer></script>
```

#### 3. Unoptimized Images

```
Opportunity: Properly size images
Savings: 800 KB
```

**Solutions:**

```html
<!-- Before: Full-size image -->
<img src="/images/hero-banner.jpg" alt="YMCA Gym">

<!-- After: Responsive images with srcset -->
<img
  src="/images/hero-banner-800w.jpg"
  srcset="
    /images/hero-banner-400w.jpg 400w,
    /images/hero-banner-800w.jpg 800w,
    /images/hero-banner-1200w.jpg 1200w,
    /images/hero-banner-1600w.jpg 1600w
  "
  sizes="(max-width: 768px) 100vw, (max-width: 1200px) 50vw, 33vw"
  alt="YMCA Gym"
  loading="lazy"
  width="1600"
  height="900"
>

<!-- Use modern formats -->
<picture>
  <source srcset="/images/hero-banner.webp" type="image/webp">
  <source srcset="/images/hero-banner.jpg" type="image/jpeg">
  <img src="/images/hero-banner.jpg" alt="YMCA Gym" loading="lazy">
</picture>
```

#### 4. Cumulative Layout Shift (CLS)

```
Metric: Cumulative Layout Shift
Value: 0.25 (Poor)
```

**Causes:**
- Images without dimensions
- Ads/embeds/iframes without space reserved
- Web fonts causing FOIT/FOUT
- Dynamic content insertion

**Solutions:**

```html
<!-- Always set image dimensions -->
<img src="image.jpg" width="800" height="600" alt="Description">

<!-- Reserve space for embeds -->
<div style="aspect-ratio: 16/9; width: 100%;">
  <iframe src="..." style="width: 100%; height: 100%;"></iframe>
</div>

<!-- Font loading strategy -->
<link rel="preload" href="/fonts/font.woff2" as="font" type="font/woff2" crossorigin>

<style>
  /* Use font-display: swap */
  @font-face {
    font-family: 'CustomFont';
    src: url('/fonts/font.woff2') format('woff2');
    font-display: swap;
  }
</style>
```

```css
/* CSS for aspect ratio boxes */
.video-container {
  aspect-ratio: 16 / 9;
  width: 100%;
}

.card-image {
  aspect-ratio: 4 / 3;
  width: 100%;
  object-fit: cover;
}
```

#### 5. Unused CSS

```
Opportunity: Remove unused CSS
Savings: 45 KB
```

**Solutions:**

```bash
# Install PurgeCSS
npm install --save-dev @fullhuman/postcss-purgecss

# Configure in postcss.config.js
module.exports = {
  plugins: [
    require('@fullhuman/postcss-purgecss')({
      content: [
        './docroot/themes/custom/*/templates/**/*.html.twig',
        './docroot/themes/custom/*/js/**/*.js'
      ],
      safelist: [
        /^modal/,
        /^dropdown/,
        /^collapse/,
        /data-bs-/
      ]
    })
  ]
};
```

## Bundle Size Analysis

### Webpack Bundle Analyzer

```bash
# Install
npm install --save-dev webpack-bundle-analyzer

# Add to webpack config
const BundleAnalyzerPlugin = require('webpack-bundle-analyzer').BundleAnalyzerPlugin;

module.exports = {
  plugins: [
    new BundleAnalyzerPlugin({
      analyzerMode: 'static',
      reportFilename: '../reports/performance/bundle-analysis.html',
      openAnalyzer: false,
      generateStatsFile: true,
      statsFilename: '../reports/performance/bundle-stats.json'
    })
  ]
};

# Build and analyze
npm run build
open reports/performance/bundle-analysis.html
```

### Measuring Bootstrap Impact

Compare bundle sizes before and after Bootstrap 5 migration:

```bash
# Create analysis script
cat > testing/scripts/analyze-bundles.js << 'EOF'
const fs = require('fs');
const path = require('path');
const gzipSize = require('gzip-size');

function analyzeFile(filePath) {
  const content = fs.readFileSync(filePath);
  const size = content.length;
  const gzipped = gzipSize.sync(content);

  return {
    raw: (size / 1024).toFixed(2) + ' KB',
    gzipped: (gzipped / 1024).toFixed(2) + ' KB'
  };
}

const files = {
  'Bootstrap CSS': 'docroot/themes/custom/ymca/dist/css/bootstrap.min.css',
  'Custom CSS': 'docroot/themes/custom/ymca/dist/css/style.min.css',
  'Bootstrap JS': 'docroot/themes/custom/ymca/dist/js/bootstrap.bundle.min.js',
  'Custom JS': 'docroot/themes/custom/ymca/dist/js/main.min.js'
};

console.log('\n=== Bundle Size Analysis ===\n');

Object.entries(files).forEach(([name, filePath]) => {
  if (fs.existsSync(filePath)) {
    const sizes = analyzeFile(filePath);
    console.log(`${name}:`);
    console.log(`  Raw: ${sizes.raw}`);
    console.log(`  Gzipped: ${sizes.gzipped}`);
    console.log('');
  }
});
EOF

# Run analysis
node testing/scripts/analyze-bundles.js
```

### Expected Bootstrap 5 Improvements

**Bootstrap 4 vs Bootstrap 5 (minified + gzipped):**

```
CSS:
  Bootstrap 4: ~23 KB
  Bootstrap 5: ~22 KB (5% smaller)

JavaScript:
  Bootstrap 4: ~18 KB (with Popper.js)
  Bootstrap 5: ~20 KB (with Popper.js v2)

Note: Bootstrap 5 dropped jQuery (~30 KB saved if jQuery not needed)
```

## Network Optimization

### Resource Hints

```html
<!-- DNS prefetch for third-party domains -->
<link rel="dns-prefetch" href="//www.google-analytics.com">
<link rel="dns-prefetch" href="//fonts.googleapis.com">

<!-- Preconnect for critical third-party origins -->
<link rel="preconnect" href="//fonts.gstatic.com" crossorigin>

<!-- Prefetch for likely next navigation -->
<link rel="prefetch" href="/programs">

<!-- Preload critical resources -->
<link rel="preload" href="/fonts/main-font.woff2" as="font" type="font/woff2" crossorigin>
<link rel="preload" href="/css/critical.css" as="style">
<link rel="preload" href="/images/hero.jpg" as="image">
```

### HTTP/2 and HTTP/3

Ensure server supports HTTP/2 or HTTP/3 for:
- Multiplexing (parallel requests)
- Header compression
- Server push

**Test HTTP/2 support:**

```bash
curl -I --http2 https://your-site.com

# Or use online tool
# https://tools.keycdn.com/http2-test
```

### Compression

Enable gzip or brotli compression on server:

**Apache (.htaccess):**

```apache
<IfModule mod_deflate.c>
  AddOutputFilterByType DEFLATE text/html
  AddOutputFilterByType DEFLATE text/css
  AddOutputFilterByType DEFLATE text/javascript
  AddOutputFilterByType DEFLATE application/javascript
  AddOutputFilterByType DEFLATE application/json
  AddOutputFilterByType DEFLATE image/svg+xml
</IfModule>

<IfModule mod_brotli.c>
  AddOutputFilterByType BROTLI_COMPRESS text/html
  AddOutputFilterByType BROTLI_COMPRESS text/css
  AddOutputFilterByType BROTLI_COMPRESS text/javascript
  AddOutputFilterByType BROTLI_COMPRESS application/javascript
  AddOutputFilterByType BROTLI_COMPRESS application/json
</IfModule>
```

**Nginx:**

```nginx
gzip on;
gzip_vary on;
gzip_types text/plain text/css application/json application/javascript text/xml application/xml image/svg+xml;
gzip_min_length 256;

# Brotli (if module installed)
brotli on;
brotli_comp_level 6;
brotli_types text/plain text/css application/json application/javascript text/xml application/xml image/svg+xml;
```

## Caching Strategies

### Browser Caching

```apache
# Apache .htaccess
<IfModule mod_expires.c>
  ExpiresActive On

  # Images
  ExpiresByType image/jpg "access plus 1 year"
  ExpiresByType image/jpeg "access plus 1 year"
  ExpiresByType image/png "access plus 1 year"
  ExpiresByType image/webp "access plus 1 year"
  ExpiresByType image/svg+xml "access plus 1 year"

  # CSS and JavaScript
  ExpiresByType text/css "access plus 1 month"
  ExpiresByType application/javascript "access plus 1 month"

  # Fonts
  ExpiresByType font/woff2 "access plus 1 year"
  ExpiresByType font/woff "access plus 1 year"

  # HTML (no cache for dynamic pages)
  ExpiresByType text/html "access plus 0 seconds"
</IfModule>

<IfModule mod_headers.c>
  # Cache static assets
  <FilesMatch "\.(jpg|jpeg|png|webp|svg|css|js|woff|woff2)$">
    Header set Cache-Control "max-age=31536000, public"
  </FilesMatch>

  # Don't cache HTML
  <FilesMatch "\.(html|htm)$">
    Header set Cache-Control "no-cache, no-store, must-revalidate"
  </FilesMatch>
</IfModule>
```

### Drupal Caching

```bash
# Enable Drupal caching
fin drush config-set system.performance css.preprocess 1 -y
fin drush config-set system.performance js.preprocess 1 -y
fin drush cache:rebuild

# Configure BigPipe for progressive rendering
fin drush config-set system.performance css.gzip 1 -y
fin drush config-set system.performance js.gzip 1 -y
```

## Monitoring and Alerts

### Real User Monitoring (RUM)

**Google Analytics 4 Web Vitals:**

```html
<script type="module">
  import {onCLS, onFID, onLCP, onINP} from 'https://unpkg.com/web-vitals@3?module';

  function sendToGoogleAnalytics({name, delta, value, id}) {
    gtag('event', name, {
      event_category: 'Web Vitals',
      event_label: id,
      value: Math.round(name === 'CLS' ? delta * 1000 : delta),
      non_interaction: true,
    });
  }

  onCLS(sendToGoogleAnalytics);
  onFID(sendToGoogleAnalytics);
  onLCP(sendToGoogleAnalytics);
  onINP(sendToGoogleAnalytics);
</script>
```

### Performance Observer API

```javascript
// Monitor LCP
const observer = new PerformanceObserver((list) => {
  const entries = list.getEntries();
  const lastEntry = entries[entries.length - 1];
  console.log('LCP:', lastEntry.renderTime || lastEntry.loadTime);
});
observer.observe({entryTypes: ['largest-contentful-paint']});

// Monitor CLS
let clsValue = 0;
const clsObserver = new PerformanceObserver((list) => {
  for (const entry of list.getEntries()) {
    if (!entry.hadRecentInput) {
      clsValue += entry.value;
      console.log('Current CLS:', clsValue);
    }
  }
});
clsObserver.observe({entryTypes: ['layout-shift']});
```

### Automated Monitoring

**Lighthouse CI Server:**

```bash
# Install Lighthouse CI server
npm install -g @lhci/server

# Start server
lhci server --port=9001

# Configure to upload to server
# In lighthouserc.json:
{
  "ci": {
    "upload": {
      "target": "lhci",
      "serverBaseUrl": "http://localhost:9001",
      "token": "your-build-token"
    }
  }
}
```

## CI/CD Integration

### GitHub Actions

Create `.github/workflows/performance-tests.yml`:

```yaml
name: Performance Tests

on:
  push:
    branches: [ bs_4_to_5 ]
  pull_request:
    branches: [ main ]
  schedule:
    - cron: '0 0 * * 0'  # Weekly

jobs:
  lighthouse:
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

      - name: Run Lighthouse CI
        run: |
          cd testing
          npx lhci autorun --config=lighthouse/lighthouserc.json
        env:
          LHCI_GITHUB_APP_TOKEN: ${{ secrets.LHCI_GITHUB_APP_TOKEN }}

      - name: Upload performance reports
        if: always()
        uses: actions/upload-artifact@v3
        with:
          name: lighthouse-reports
          path: testing/reports/performance/
          retention-days: 30

      - name: Comment PR with results
        if: github.event_name == 'pull_request'
        uses: treosh/lighthouse-ci-action@v9
        with:
          configPath: './testing/lighthouse/lighthouserc.json'
          uploadArtifacts: true
          temporaryPublicStorage: true
```

### NPM Scripts

Add to `testing/package.json`:

```json
{
  "scripts": {
    "test:perf": "lhci autorun --config=lighthouse/lighthouserc.json",
    "test:perf:mobile": "lighthouse --preset=mobile --output html --output-path reports/performance/mobile.html",
    "test:perf:desktop": "lighthouse --preset=desktop --output html --output-path reports/performance/desktop.html",
    "analyze:bundle": "webpack --config webpack.config.js --profile --json > reports/performance/stats.json && webpack-bundle-analyzer reports/performance/stats.json",
    "report:perf": "open reports/performance/lighthouse/index.html"
  }
}
```

## Best Practices

### 1. Set Realistic Budgets

Base budgets on current performance, not ideal targets:

```json
{
  "budgets": [
    {
      "timings": [
        {
          "metric": "largest-contentful-paint",
          "budget": 2500  // Start here, improve to 2000 over time
        }
      ]
    }
  ]
}
```

### 2. Test on Real Devices

Lighthouse simulates mobile, but test on real devices:

```bash
# Use Chrome DevTools Remote Debugging
# Connect Android device via USB
# Navigate to chrome://inspect
# Inspect and run Lighthouse
```

### 3. Test Multiple Pages

Don't just test homepage - test:
- Homepage
- Landing pages
- Content-heavy pages
- Form pages
- Search results

### 4. Monitor Trends

Performance can degrade over time:

```bash
# Run weekly performance tests
# Track trends in Lighthouse CI server or analytics
# Set alerts for regressions
```

### 5. Optimize Images

Images are often the largest resources:

```bash
# Optimize images before committing
npm install -g @squoosh/cli

squoosh-cli --webp auto images/*.jpg
squoosh-cli --resize '{width: 1200}' --webp auto images/hero.jpg
```

## Performance Checklist

### Before Migration (Baseline)

- [ ] Run Lighthouse on critical pages
- [ ] Document current Core Web Vitals
- [ ] Measure bundle sizes
- [ ] Capture network waterfall
- [ ] Note current performance score

### During Migration

- [ ] Monitor bundle size changes
- [ ] Test each component after migration
- [ ] Verify lazy loading still works
- [ ] Check for unused CSS/JS
- [ ] Validate resource loading

### After Migration

- [ ] Run full Lighthouse audit
- [ ] Compare Core Web Vitals to baseline
- [ ] Verify performance budgets met
- [ ] Test on real devices
- [ ] Monitor RUM data for 1-2 weeks

### Ongoing

- [ ] Weekly automated Lighthouse tests
- [ ] Monthly performance reviews
- [ ] Quarterly budget adjustments
- [ ] Continuous image optimization
- [ ] Regular dependency updates

## Resources

### Tools

- Lighthouse: https://developers.google.com/web/tools/lighthouse
- WebPageTest: https://www.webpagetest.org/
- PageSpeed Insights: https://pagespeed.web.dev/
- web.dev: https://web.dev/measure/

### Documentation

- Web Vitals: https://web.dev/vitals/
- Chrome DevTools: https://developer.chrome.com/docs/devtools/
- Lighthouse CI: https://github.com/GoogleChrome/lighthouse-ci

## Conclusion

Performance testing ensures your Bootstrap 5 migration maintains fast, responsive user experiences. Use Lighthouse CI for automated testing, set realistic budgets, and monitor Core Web Vitals to track improvements over time. Remember that performance is an ongoing commitment requiring regular monitoring and optimization.
