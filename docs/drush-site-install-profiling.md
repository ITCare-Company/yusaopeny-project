# Drush Site Install Profiling Research

> [!NOTE]
> This research was conducted on YMCA Website Services 4.0 with Drupal 11.1.9 to identify performance bottlenecks during `drush site:install`.

## Executive Summary

| Metric | Value |
|--------|-------|
| Modules Installed | 265 |
| Total Time | 537 seconds (9 min) |
| Peak Memory | 4.38 GB |
| Container Rebuilds | 279 |

> [!IMPORTANT]
> **Primary finding**: Upgrading to Drupal 11.2+ will significantly reduce install time and memory usage through batched module installation.

---

## Profiling Environment

- **Profile**: `openy` with `standard` preset
- **Drupal Core**: 11.1.9
- **PHP**: 8.3
- **Profiler**: XHProf with XHGui
- **Platform**: DDEV on macOS

---

## Memory Growth Analysis

```mermaid
graph LR
    A[Module 1: 25MB] --> B[Module 50: 65MB]
    B --> C[Module 100: 123MB]
    C --> D[Module 150: 776MB]
    D --> E[Module 200: 1.92GB]
    E --> F[Module 249: 3.5GB]
```

### Memory Growth Rate by Phase

| Phase | Modules | Memory | Growth Rate |
|-------|---------|--------|-------------|
| Initial | 1-50 | 25MB → 65MB | ~0.8 MB/module |
| Early | 50-100 | 65MB → 123MB | ~1.2 MB/module |
| Mid | 100-150 | 123MB → 776MB | **~13 MB/module** |
| Late | 150-200 | 776MB → 1.92GB | **~23 MB/module** |
| Final | 200-249 | 1.92GB → 3.5GB | **~32 MB/module** |

> [!WARNING]
> Memory growth becomes exponential after ~100 modules due to repeated container rebuilds scanning all previously installed modules.

---

## Top Memory Consumers

### By Total Memory Allocated

| Function | Calls | Memory |
|----------|-------|--------|
| `StaticReflectionParser::parse` | 69,093 | 13,037 MB |
| `TokenParser::__construct` | 67,807 | 12,419 MB |
| `Connection::query` | 331,108 | 6,863 MB |
| `StatementWrapperIterator::execute` | 360,648 | 6,745 MB |
| `Select::execute` | 277,855 | 5,374 MB |
| `MenuTreeStorage::safeExecuteSelect` | 245,444 | 4,615 MB |

### By Wall Time

| Function | Calls | Time (sec) |
|----------|-------|------------|
| `ModuleInstaller::install` | 249 | 461s |
| `openy_enable_module` | 120 | 333s |
| `ModuleInstaller::updateKernel` | 279 | 310s |
| `InstallerKernel::initializeContainer` | 282 | 308s |

---

## Root Cause Analysis

<details>
<summary><strong>Why does memory grow exponentially?</strong></summary>

### The Problem Chain

```
265 module installs
  → 279 kernel updates
    → 282 container rebuilds
      → 69,093 StaticReflectionParser::parse calls
        → 13+ GB memory churn
```

### Drupal 11.1 Behavior

In Drupal 11.1, `ModuleInstaller::install()` processes modules **one at a time**:

```php
// core/lib/Drupal/Core/Extension/ModuleInstaller.php (11.1)
foreach ($module_list as $module) {
    // ... installs one module
    // ... rebuilds container EACH TIME
    $this->updateKernel($module_filenames);
}
```

Each container rebuild triggers:
1. Full plugin discovery across ALL installed modules
2. `AttributeClassDiscovery::getDefinitions()` scans every PHP file
3. `StaticReflectionParser::parse()` called for each class

**Result**: Installing module #200 scans 199 previously installed modules.

</details>

<details>
<summary><strong>What changed in Drupal 11.2+?</strong></summary>

### Batched Module Installation

Drupal 11.2 introduced batched installation via [#3416522](https://www.drupal.org/project/drupal/issues/3416522):

```php
// core/lib/Drupal/Core/Extension/ModuleInstaller.php (11.2+)
$module_groups = [];
foreach ($module_list as $module) {
    $module_groups[$index][] = $module;
    // Group up to 20 modules together
    if (count($module_groups[$index]) === Settings::get('core.multi_module_install_batch_size', 20)) {
        $index++;
    }
}

// Install each GROUP with single container rebuild
foreach ($module_groups as $modules) {
    $this->doInstall($modules, ...);
}
```

### Expected Improvement

| Metric | Drupal 11.1 | Drupal 11.2+ |
|--------|-------------|--------------|
| Container Rebuilds | 265 | ~14 |
| `StaticReflectionParser` calls | 69,093 | ~5,000 |
| Expected Time Reduction | - | 60-80% |

</details>

---

## Recommendations

### 1. Upgrade to Drupal 11.2+

> [!TIP]
> This is the **highest impact** optimization - no code changes required.

- Batched module installation (20 modules per container rebuild)
- Expected: ~14 container rebuilds instead of 265
- Estimated time reduction: 60-80%

### 2. Review `openy_enable_module` Usage

The function is called 120 times separately during install:

```
[info] openy_enable_module called 120 times
[info] Total time: 333 seconds
```

Consider batching these calls where dependencies allow.

### 3. Investigate MenuTreeStorage Queries

245,444 queries during install:

| Function | Queries |
|----------|---------|
| `MenuTreeStorage::safeExecuteSelect` | 245,444 |
| `MenuTreeStorage::doSave` | 82,943 |

This may indicate opportunities for query batching or caching.

---

## Configuration Options (Drupal 11.2+)

### `core.multi_module_install_batch_size`

Add to `settings.php` to tune batch size:

```php
$settings['core.multi_module_install_batch_size'] = 20; // default
```

### `container_rebuild_required`

Modules can declare in `.info.yml`:

```yaml
container_rebuild_required: true
```

> [!CAUTION]
> Only set this if your module decorates services used during the install process itself.

---

## Related Issues

- [#3416522: Add ability to install multiple modules with single container rebuild](https://www.drupal.org/project/drupal/issues/3416522)
- [#3395260: Performance improvements for AttributeClassDiscovery](https://www.drupal.org/project/drupal/issues/3395260)
- [#3473563: Change record for container_rebuild_required](https://www.drupal.org/node/3473563)

---

## Appendix: Profiling Data

<details>
<summary><strong>Full memory growth log</strong></summary>

```
Module 1:    2.6s,   25 MB
Module 50:   29s,    65 MB
Module 100:  77s,   123 MB
Module 150: 148s,   776 MB
Module 200: 261s, 1,920 MB
Module 249: 426s, 3,500 MB
Module 265: 537s, 4,380 MB (final)
```

</details>

<details>
<summary><strong>Call counts for key functions</strong></summary>

| Function | Calls |
|----------|-------|
| `Composer\Autoload\ClassLoader::findFile` | 89,717,207 |
| `Composer\Autoload\ClassLoader::loadClass` | 89,690,445 |
| `Doctrine\Annotations\TokenParser::next` | 51,708,912 |
| `Symfony\DI\Definition::hasTag` | 18,940,089 |
| `StatementWrapperIterator::execute` | 360,648 |
| `Connection::query` | 331,108 |
| `Select::execute` | 277,855 |
| `MenuTreeStorage::safeExecuteSelect` | 245,444 |

</details>
