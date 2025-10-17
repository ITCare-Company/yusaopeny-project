# Testing Overview - Bootstrap 5 Migration

## Purpose

This document outlines the testing strategy for the Bootstrap 4 to Bootstrap 5 migration in the Y USA Open YMCA distribution. The testing approach is designed to ensure visual consistency, accessibility compliance, and performance standards are maintained or improved during the migration.

## Testing Strategy

The testing strategy is structured in three progressive levels, allowing teams to scale their testing efforts based on project scope, timeline, and risk tolerance.

### Three Testing Levels

#### Level 1: Basic Testing (Minimum Viable)

**When to Use:**
- Small sites with limited custom components
- Low-risk migrations with minimal customization
- Tight timelines with limited resources
- Internal/staging deployments

**Coverage:**
- Smoke tests on critical pages
- Manual accessibility checks
- Basic responsive testing
- Core functionality verification

**Time Investment:** 4-8 hours

#### Level 2: Standard Testing (Recommended)

**When to Use:**
- Production sites with standard customization
- Medium-risk migrations with some custom components
- Standard project timelines
- Client-facing deployments

**Coverage:**
- Automated visual regression testing
- Automated accessibility scanning
- Performance baseline comparison
- Component-level testing
- Cross-browser testing (Chrome, Firefox, Safari, Edge)
- Mobile and tablet testing

**Time Investment:** 16-24 hours

#### Level 3: Comprehensive Testing (Enterprise)

**When to Use:**
- Large production sites with extensive customization
- High-risk migrations with complex custom components
- Mission-critical deployments
- Sites with legal accessibility requirements
- Multi-brand or white-label implementations

**Coverage:**
- Full automated visual regression suite
- Comprehensive accessibility testing (automated + manual)
- Performance monitoring and optimization
- Screen reader testing
- Keyboard navigation testing
- Cross-browser testing (including older versions)
- Multiple device testing (including tablets)
- Load testing
- Integration testing with CRMs (Daxko, ActiveNet)
- User acceptance testing (UAT)

**Time Investment:** 40-80 hours

## Testing Tools

### Visual Regression Testing

**Tool: BackstopJS**

BackstopJS captures screenshots of pages before and after migration, highlighting visual differences.

**Key Features:**
- Headless browser testing (Puppeteer)
- Screenshot comparison with pixel diffing
- Multiple viewport support
- Scenario-based testing
- CI/CD integration

**Setup Time:** 2-4 hours
**Documentation:** `TESTING_VISUAL_REGRESSION.md`

### Accessibility Testing

**Tool: Pa11y**

Pa11y automates accessibility testing against WCAG 2.2 AA standards.

**Key Features:**
- WCAG 2.2 Level AA compliance checking
- HTML CodeSniffer integration
- Command-line and CI integration
- JSON/CSV/HTML reporting
- Automated scanning of multiple pages

**Setup Time:** 1-2 hours
**Documentation:** `TESTING_ACCESSIBILITY.md`

### Performance Testing

**Tool: Lighthouse CI**

Lighthouse provides automated audits for performance, accessibility, SEO, and best practices.

**Key Features:**
- Performance metrics (Core Web Vitals)
- Progressive Web App auditing
- SEO analysis
- Accessibility scoring
- CI/CD integration with budgets

**Setup Time:** 2-3 hours
**Documentation:** `TESTING_PERFORMANCE.md`

### Additional Tools

**Manual Testing:**
- Browser DevTools (Chrome, Firefox)
- Screen readers (NVDA, JAWS, VoiceOver)
- Color contrast analyzers (Colour Contrast Analyser)
- Responsive design testing (Chrome DevTools, BrowserStack)

**Monitoring:**
- Google Analytics (user behavior)
- Sentry (error tracking)
- New Relic/DataDog (performance monitoring)

## Test Environment Setup

### Prerequisites

**System Requirements:**
```bash
# Node.js 18+ and npm
node --version  # v18.0.0 or higher
npm --version   # 9.0.0 or higher

# Git (for version control)
git --version

# Chrome/Chromium (for Puppeteer)
google-chrome --version
```

**Drupal Environment:**
- Docksal or DDEV local environment
- Staging environment matching production
- Database snapshot from production (anonymized)

### Environment Setup Steps

#### 1. Clone Repository and Install Dependencies

```bash
# Navigate to project root
cd /private/var/www/YMCAWS_11

# Create testing directory
mkdir -p testing
cd testing

# Initialize npm project
npm init -y

# Install testing dependencies
npm install --save-dev \
  backstopjs \
  pa11y \
  pa11y-ci \
  lighthouse \
  @lhci/cli
```

#### 2. Configure Test Environment Variables

Create `.env.testing` in the testing directory:

```bash
# .env.testing

# Base URLs
BASE_URL_BEFORE=https://bs4-site.docksal.site
BASE_URL_AFTER=https://bs5-site.docksal.site

# Testing configuration
BACKSTOP_ENGINE=puppeteer
BACKSTOP_DEBUG=false
LIGHTHOUSE_BUDGET_FILE=./lighthouse-budget.json

# Pa11y configuration
PA11Y_STANDARD=WCAG2AA
PA11Y_TIMEOUT=30000

# CI/CD flags
CI=false
GENERATE_REPORTS=true
REPORTS_DIR=./reports
```

#### 3. Create Testing Directory Structure

```bash
# Create directory structure
mkdir -p testing/{backstop,pa11y,lighthouse,reports}
mkdir -p testing/reports/{visual,accessibility,performance}

# Directory structure:
# testing/
# ├── backstop/           # BackstopJS configuration and data
# ├── pa11y/              # Pa11y configuration and reports
# ├── lighthouse/         # Lighthouse configuration and budgets
# ├── reports/            # Generated test reports
# │   ├── visual/         # Visual regression reports
# │   ├── accessibility/  # Accessibility reports
# │   └── performance/    # Performance reports
# ├── .env.testing        # Environment variables
# └── package.json        # npm dependencies
```

#### 4. Initialize Tool Configurations

```bash
# Initialize BackstopJS
cd testing/backstop
npx backstop init

# Create Pa11y configuration
cd ../pa11y
touch .pa11yci.json

# Create Lighthouse configuration
cd ../lighthouse
touch lighthouserc.json
```

### Docksal Environment Setup

For teams using Docksal, create parallel environments for before/after comparison:

```bash
# Create BS4 environment
cd /private/var/www/YMCAWS_11
git checkout main  # or your BS4 branch
fin up
fin init

# Note the URL (e.g., yusaopeny.docksal.site)

# Create BS5 environment in separate directory
cd /private/var/www
git clone https://github.com/YCloudYUSA/yusaopeny-project.git YMCAWS_11_BS5
cd YMCAWS_11_BS5
git checkout bs_4_to_5  # or your BS5 branch

# Update .docksal/docksal.env with different virtual host
echo "VIRTUAL_HOST=yusaopeny-bs5.docksal.site" >> .docksal/docksal-local.env

fin up
fin init

# Now you have:
# BS4: http://yusaopeny.docksal.site
# BS5: http://yusaopeny-bs5.docksal.site
```

### DDEV Environment Setup

For teams using DDEV:

```bash
# Create BS4 environment
cd /private/var/www/YMCAWS_11
git checkout main
ddev start
ddev composer install
ddev drush si openy -y

# Create BS5 environment
cd /private/var/www
git clone https://github.com/YCloudYUSA/yusaopeny-project.git YMCAWS_11_BS5
cd YMCAWS_11_BS5
git checkout bs_4_to_5

# Configure different project name
ddev config --project-name=ymcaws-bs5

ddev start
ddev composer install
ddev drush si openy -y

# Now you have:
# BS4: https://ymcaws-11.ddev.site
# BS5: https://ymcaws-bs5.ddev.site
```

## CI/CD Integration

### GitHub Actions Workflow

Create `.github/workflows/bootstrap-migration-tests.yml`:

```yaml
name: Bootstrap 5 Migration Tests

on:
  push:
    branches: [ bs_4_to_5 ]
  pull_request:
    branches: [ main ]

jobs:
  visual-regression:
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

      - name: Install Chrome
        run: |
          wget -q -O - https://dl-ssl.google.com/linux/linux_signing_key.pub | sudo apt-key add -
          sudo sh -c 'echo "deb [arch=amd64] http://dl.google.com/linux/chrome/deb/ stable main" >> /etc/apt/sources.list.d/google.list'
          sudo apt-get update
          sudo apt-get install -y google-chrome-stable

      - name: Run BackstopJS tests
        run: |
          cd testing
          npm run test:visual

      - name: Upload visual regression reports
        if: failure()
        uses: actions/upload-artifact@v3
        with:
          name: backstop-reports
          path: testing/backstop/backstop_data/html_report/
          retention-days: 30

  accessibility:
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
          npm run test:a11y

      - name: Upload accessibility reports
        if: always()
        uses: actions/upload-artifact@v3
        with:
          name: pa11y-reports
          path: testing/reports/accessibility/
          retention-days: 30

  performance:
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
          npm run test:performance
        env:
          LHCI_GITHUB_APP_TOKEN: ${{ secrets.LHCI_GITHUB_APP_TOKEN }}

      - name: Upload performance reports
        if: always()
        uses: actions/upload-artifact@v3
        with:
          name: lighthouse-reports
          path: testing/reports/performance/
          retention-days: 30
```

### NPM Scripts

Add these scripts to `testing/package.json`:

```json
{
  "scripts": {
    "test": "npm run test:visual && npm run test:a11y && npm run test:performance",
    "test:visual": "cd backstop && backstop test",
    "test:visual:reference": "cd backstop && backstop reference",
    "test:visual:approve": "cd backstop && backstop approve",
    "test:a11y": "pa11y-ci --config pa11y/.pa11yci.json",
    "test:performance": "lhci autorun --config=lighthouse/lighthouserc.json",
    "report:open": "npm run report:open:visual",
    "report:open:visual": "open backstop/backstop_data/html_report/index.html",
    "report:open:a11y": "open reports/accessibility/index.html",
    "report:open:performance": "open reports/performance/index.html"
  }
}
```

### Jenkins Pipeline (Alternative)

Create `Jenkinsfile` in testing directory:

```groovy
pipeline {
    agent any

    environment {
        BASE_URL_BEFORE = "${env.BASE_URL_BEFORE}"
        BASE_URL_AFTER = "${env.BASE_URL_AFTER}"
    }

    stages {
        stage('Setup') {
            steps {
                dir('testing') {
                    sh 'npm ci'
                }
            }
        }

        stage('Visual Regression') {
            steps {
                dir('testing') {
                    sh 'npm run test:visual'
                }
            }
            post {
                always {
                    publishHTML([
                        reportDir: 'testing/backstop/backstop_data/html_report',
                        reportFiles: 'index.html',
                        reportName: 'BackstopJS Report'
                    ])
                }
            }
        }

        stage('Accessibility') {
            steps {
                dir('testing') {
                    sh 'npm run test:a11y'
                }
            }
            post {
                always {
                    publishHTML([
                        reportDir: 'testing/reports/accessibility',
                        reportFiles: 'index.html',
                        reportName: 'Pa11y Report'
                    ])
                }
            }
        }

        stage('Performance') {
            steps {
                dir('testing') {
                    sh 'npm run test:performance'
                }
            }
            post {
                always {
                    publishHTML([
                        reportDir: 'testing/reports/performance',
                        reportFiles: 'index.html',
                        reportName: 'Lighthouse Report'
                    ])
                }
            }
        }
    }

    post {
        failure {
            emailext(
                subject: "Bootstrap 5 Migration Tests Failed - ${env.JOB_NAME} #${env.BUILD_NUMBER}",
                body: "Tests failed. Check console output: ${env.BUILD_URL}",
                to: "${env.NOTIFICATION_EMAIL}"
            )
        }
    }
}
```

## Test Execution Workflow

### 1. Pre-Migration (Baseline Creation)

```bash
cd /private/var/www/YMCAWS_11/testing

# Set environment to BS4 site
export BASE_URL_BEFORE=http://yusaopeny.docksal.site

# Generate visual baselines
npm run test:visual:reference

# Run baseline accessibility audit
npm run test:a11y > reports/accessibility/baseline-report.json

# Run baseline performance audit
npm run test:performance
cp reports/performance/latest.json reports/performance/baseline-performance.json
```

### 2. Post-Migration (Comparison Testing)

```bash
# Set environment to BS5 site
export BASE_URL_AFTER=http://yusaopeny-bs5.docksal.site

# Run visual regression tests
npm run test:visual

# Review visual differences
npm run report:open:visual

# Run accessibility tests
npm run test:a11y

# Review accessibility report
npm run report:open:a11y

# Run performance tests
npm run test:performance

# Review performance report
npm run report:open:performance
```

### 3. Issue Resolution

When tests fail:

1. **Visual Regression Failures:**
   - Review BackstopJS report in browser
   - Identify intentional vs. unintentional changes
   - Fix CSS issues or approve changes
   - Run `npm run test:visual:approve` for intentional changes

2. **Accessibility Failures:**
   - Review Pa11y report for specific violations
   - Fix HTML/CSS/JavaScript issues
   - Re-run tests to verify fixes
   - Document any deferred issues

3. **Performance Failures:**
   - Review Lighthouse report for performance bottlenecks
   - Optimize CSS/JS bundle sizes
   - Implement caching strategies
   - Re-run tests to verify improvements

### 4. Final Validation

```bash
# Run complete test suite
npm test

# Generate summary report
npm run report:summary

# Archive reports for documentation
tar -czf test-reports-$(date +%Y%m%d).tar.gz reports/
```

## Testing Checklist

### Pre-Migration Checklist

- [ ] Environment setup complete (before/after sites running)
- [ ] Testing tools installed and configured
- [ ] Baseline screenshots captured
- [ ] Baseline accessibility audit completed
- [ ] Baseline performance audit completed
- [ ] Test scenarios documented
- [ ] Critical user paths identified
- [ ] Test data prepared (content, users, configurations)

### During Migration Checklist

- [ ] Component-level testing after each migration
- [ ] Visual regression tests run incrementally
- [ ] Accessibility issues addressed immediately
- [ ] Performance monitored throughout migration
- [ ] Documentation updated with issues/resolutions

### Post-Migration Checklist

- [ ] Full visual regression test suite passed
- [ ] Accessibility audit shows no regressions
- [ ] Performance metrics meet or exceed baseline
- [ ] Cross-browser testing completed
- [ ] Mobile/tablet testing completed
- [ ] Screen reader testing completed
- [ ] Keyboard navigation testing completed
- [ ] User acceptance testing completed
- [ ] Test reports archived and documented
- [ ] Known issues documented with resolution plan

## Testing Best Practices

### 1. Start Early

Begin testing setup before migration starts. Generate baselines early to establish clear comparison points.

### 2. Test Incrementally

Don't wait until the end of migration to test. Test each component/page as it's migrated to catch issues early.

### 3. Automate Where Possible

Automate repetitive tests (visual regression, accessibility scanning, performance auditing) to save time and ensure consistency.

### 4. Document Everything

Document test scenarios, configurations, known issues, and resolutions. This knowledge is valuable for future migrations.

### 5. Use Real Data

Test with production-like data and content. Edge cases and real-world scenarios reveal issues that test data might miss.

### 6. Test Multiple Viewports

Bootstrap is responsive. Test mobile, tablet, and desktop viewports for every scenario.

### 7. Include Stakeholders

Involve content editors, designers, and stakeholders in UAT. They often catch issues that technical testing misses.

### 8. Set Clear Pass/Fail Criteria

Define what constitutes a test failure vs. an acceptable change. Not all visual differences are bugs.

### 9. Prioritize Fixes

Triage issues by severity and impact. Not all issues need to be fixed before launch.

### 10. Plan for Regression

Expect some issues to slip through. Have a plan for post-launch monitoring and rapid response.

## Performance Budgets

Set performance budgets to ensure Bootstrap 5 migration improves or maintains performance:

```json
{
  "budgets": [
    {
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
          "resourceType": "total",
          "budget": 500
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
        }
      ]
    }
  ]
}
```

## Accessibility Standards

All testing must ensure WCAG 2.2 Level AA compliance:

### Key Requirements

- **Perceivable:** Content must be presentable to users in ways they can perceive
- **Operable:** Interface components must be operable
- **Understandable:** Information and operation must be understandable
- **Robust:** Content must be robust enough for assistive technologies

### Common Bootstrap 5 Accessibility Considerations

- Form labels and ARIA attributes
- Focus states for interactive elements
- Color contrast ratios (minimum 4.5:1 for text)
- Keyboard navigation for all interactive components
- Screen reader announcements for dynamic content
- Skip navigation links
- Landmark regions properly defined

## Reporting and Documentation

### Test Report Template

Create a standardized report for each testing cycle:

```markdown
# Bootstrap 5 Migration Test Report

**Date:** YYYY-MM-DD
**Tester:** Name
**Environment:** Staging/Production
**Test Level:** Basic/Standard/Comprehensive

## Executive Summary

Brief overview of test results, pass/fail status, and key findings.

## Visual Regression Testing

- **Total Scenarios:** X
- **Passed:** X
- **Failed:** X
- **Pass Rate:** X%

### Notable Issues

1. Issue description, severity, status
2. Issue description, severity, status

## Accessibility Testing

- **Pages Tested:** X
- **Total Issues:** X
- **Critical:** X
- **Moderate:** X
- **Minor:** X

### Notable Issues

1. Issue description, WCAG criterion, status
2. Issue description, WCAG criterion, status

## Performance Testing

- **Pages Tested:** X
- **Average LCP:** X ms (baseline: X ms)
- **Average FID:** X ms (baseline: X ms)
- **Average CLS:** X (baseline: X)
- **Performance Score:** X/100 (baseline: X/100)

### Notable Issues

1. Issue description, impact, status
2. Issue description, impact, status

## Recommendations

1. Priority 1 recommendations
2. Priority 2 recommendations
3. Priority 3 recommendations

## Next Steps

- [ ] Action item 1
- [ ] Action item 2
- [ ] Action item 3

## Appendix

- Links to detailed reports
- Screenshots of key issues
- Test configurations used
```

## Support and Resources

### Documentation

- BackstopJS: https://github.com/garris/BackstopJS
- Pa11y: https://github.com/pa11y/pa11y
- Lighthouse: https://developers.google.com/web/tools/lighthouse
- WCAG 2.2: https://www.w3.org/WAI/WCAG22/quickref/
- Bootstrap 5: https://getbootstrap.com/docs/5.3/

### Internal Resources

- `TESTING_VISUAL_REGRESSION.md` - Visual regression testing guide
- `TESTING_ACCESSIBILITY.md` - Accessibility testing guide
- `TESTING_PERFORMANCE.md` - Performance testing guide
- `MIGRATION_GUIDE.md` - Bootstrap 5 migration guide
- `COMPONENT_MAPPING.md` - Component changes reference

### Getting Help

For questions or issues with testing:

1. Check documentation in `docs/bootstrap-5-migration/testing/`
2. Review tool-specific documentation (links above)
3. Contact the Y USA development team
4. File an issue in the project repository

## Conclusion

Testing is critical to a successful Bootstrap 5 migration. Choose the testing level appropriate for your project, follow the guidelines in this document, and refer to the detailed testing guides for each tool. Early and consistent testing will catch issues before they reach production, ensuring a smooth migration experience for your users.
