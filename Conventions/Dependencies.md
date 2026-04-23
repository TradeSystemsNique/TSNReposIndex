# Dependencies Format - TSN Ecosystem

> Standard for documenting dependencies in TSN repositories using `dependencies.json`

---

## 📋 Table of Contents

1. [Overview](#overview)
2. [JSON Structure](#json-structure)
3. [Field `repos`](#field-repos)
4. [Field `min_mt5_build`](#field-min_mt5_build)
5. [Field `py` (Python)](#field-py-python)
6. [Field `opencl`](#field-opencl)
7. [Complete Examples](#complete-examples)
8. [Special Comments](#special-comments)
9. [Automation](#automation)

---

## Overview

Each repository in the TSN ecosystem that uses any part of the ecosystem **must have** a `dependencies.json` file in the root that declares:

- **Dependencies on other repos**
- **Minimum requirements** (MT5 build, Python version, OpenCL) - depends on what languages are used
- **Comment on access status** (public, private, purchase-required, etc.)

### Location
Always located in the repo root with the name: `/dependencies.json`.

### Purpose:
- Document requirements in a machine-readable format.
- Enable automation (installation scripts, CI/CD) - PyBase manages this easily.
- Generate dependency tables automatically.
- Validate consistency between repos.

---

## JSON Structure

### Basic Schema

```json
{
  "repos": [
    {
      "name": "RepoName",
      "url": "https://forge.mql5.io/your_username/RepoName",
      "rama": "main",
      "comment": "Description of access or purpose"
    }
  ],
  "min_mt5_build": 5430,
  "py": {
    "min_version": "3.10.9",
    "requirements": "requirements.txt"
  },
  "opencl": {
    "support_double": true
  }
}
```

### Required Fields

```json
{
  "repos": [],          // REQUIRED - Array of dependencies
  "min_mt5_build": 5430 // RECOMMENDED - Minimum MT5 build
}
```

### Optional Fields

```json
{
  "py": { },       // If the repo uses Python
  "opencl": { }    // If the repo uses OpenCL
}
> In the future, if the ecosystem expands to other languages, the standard of that language will be used. For example, if JS is used, npm would be used, etc. Currently, the ecosystem covers MQL5, CL, PY, and to a lesser extent (full vanilla, without complex dependencies) JS/CSS/HTML/C++
```

---

## Field `repos`

### Structure of each repo

```json
{
  "name": "string",      // Exact repo name
  "url": "string",       // Complete repo URL (can be on forge\github, etc., anything that accepts git)
  "rama": "string",      // Recommended branch (usually "main")
  "comment": "string"    // Description of access/purpose
}
```

### Field `name`

- **Type:** `string`
- **Format:** Exact repository name (no spaces)
- **Examples:**
  ```json
  "name": "ICTLibrary"
  "name": "AiDataGenByLeo"
  "name": "TimeUtils"
  ```

### Field `url`

- **Type:** `string (URL)`
- **Format:** Repo URL
- **Pattern:** `https://forge.mql5.io/nique_372/[RepoName]`
- **Examples:**
  ```json
  "url": "https://forge.mql5.io/nique_372/ICTLibrary"
  "url": "https://forge.mql5.io/nique_372/AiDataGenByLeo"
  "url": "https://github.com/TradeSystemsNique/AiDataGenByLeoFeaturesDocs"
  ```

### Field `rama`

- **Type:** `string`
- **Common values:** `"main"`, `"dev"`, `"stable"`, `"master"`
- **Usage:** Specifies which branch to clone
- **Examples:**
  ```json
  "rama": "main"       // Latest version
  "rama": "stable"     // Stable version
  "rama": "dev"        // Development (less stable)
  ```

### Field `comment`

Describes the **access status** or **purpose** of the dependency.

#### Standard values for `comment`

| Value | Meaning | Example |
|-------|---------|---------|
| `"public"` | Public access | TimeUtils is public |
| `"private"` | Private repo | ICTLibrary is private |
| `"private + instructions"` | Private with how to access | "private repository, Write to me..." |
| `"purchase + link"` | Requires purchase + URL | "private repository, To access..." |
| `"internal"` | TSN internal use only | For internal utilities |
| `"optional"` | Optional dependency | "optional - improves features" |

#### Examples of `comment`

```json
// Public repo - free access
"comment": "public"

// Private repo - clear instructions
"comment": "private repository, Write to me privately (via MQL5.com), my username is nique_372"

// Purchase repo - with link
"comment": "private repository, To access the repository, purchase the product: https://www.thebotplace.com/bot/ict-fastlibrary"

// Optional
"comment": "optional - Telegram notifications"

// Combined
"comment": "private, required for AI features. Contact: nique_372 on MQL5"
```

---

## Field `min_mt5_build`

Specifies the **minimum MetaTrader 5 version** required.

### Structure

```json
"min_mt5_build": 5430
```

### When to Update

- If you use features requiring a minimum MT5
- If your libraries use new classes/syntax
- Don't do it unnecessarily (limits users)

### Examples

```json
// Very old repo, compatible with old builds
"min_mt5_build": 5200

// Modern repo, requires recent MT5
"min_mt5_build": 5430

// Repo with very new features
"min_mt5_build": 5830
```

---

## Field `py` (Python)

If the repo **uses Python** (scripts, ML models, data generation).

### Structure

```json
"py": {
  "min_version": "3.10.9",
  "requirements": "requirements.txt"
}
```

### Field `min_version`

- **Type:** `string`
- **Format:** Semver: `MAJOR.MINOR.PATCH`
- **Examples:**
  ```json
  "min_version": "3.8.0"    // Compatible with Python 3.8+
  "min_version": "3.10.9"   // Requires 3.10.9 minimum
  "min_version": "3.11.0"   // Python 3.11+ features
  ```

### Field `requirements`

- **Type:** `string`
- **Value:** Relative path to the requirements file (should be located in the project root)
- **Format:** Typically `"requirements.txt"`

### Examples

```json
// Simple project
"py": {
  "min_version": "3.10.0",
  "requirements": "requirements.txt"
}

// Complex project
"py": {
  "min_version": "3.11.0",
  "requirements": "requirements.txt"
}

// Multiple requirements (specify the main one)
"py": {
  "min_version": "3.10.0",
  "requirements": "requirements.txt"
}
```

---

## Field `opencl`

If the repo **uses OpenCL** (GPU acceleration, parallel computing).

### Structure

```json
"opencl": {
  "support_double": true
}
```

### Field `support_double`

- **Type:** `boolean`
- **Meaning:** Does it require support for double precision numbers (64-bit)?
- **Impact:** Older GPUs may not support doubles

### Values

```json
// Requires double support (more precise)
"opencl": {
  "support_double": true
}

// Works without double (compatible with more GPUs)
"opencl": {
  "support_double": false
}
```

### When to Use

```json
// ScalerByLeo - uses OpenCL for scaling
"opencl": {
  "support_double": true
}

// Library without GPU
// (don't include this field)
```

---

## Complete Examples

### Example 1: Simple MQL5 Library (no dependencies)

**Repo:** TimeUtils

```json
// No need to define the file
```

### Example 2: MQL5 Library with Private Dependencies

**Repo:** ICTLibraryExamples (requires purchase of ICTLibrary)

```json
{
  "repos": [
    {
      "name": "ICTLibrary",
      "url": "https://forge.mql5.io/nique_372/ICTLibrary",
      "rama": "main",
      "comment": "private repository, To access the repository, purchase the product: https://www.thebotplace.com/bot/ict-fastlibrary"
    }
  ],
  "min_mt5_build": 5430
}
```

### Example 3: Library with Multiple Dependencies

**Repo:** EasySbAi (Complex EA with multiple dependencies)

```json
{
  "repos": [
    {
      "name": "ICTLibraryEasy",
      "url": "https://forge.mql5.io/nique_372/ICTLibraryEasy",
      "rama": "main",
      "comment": "public - core ICT library"
    },
    {
      "name": "AiDataGenByLeo",
      "url": "https://forge.mql5.io/nique_372/AiDataGenByLeo",
      "rama": "main",
      "comment": "public - AI feature generation"
    },
    {
      "name": "TelegramByLeo",
      "url": "https://forge.mql5.io/nique_372/TelegramByLeo",
      "rama": "main",
      "comment": "optional - for Telegram notifications"
    }
  ],
  "min_mt5_build": 5430
}
```

### Example 4: Python Project

**Repo:** AiDataGenByLeo (Data generator with Python)

```json
{
  "repos": [
    {
      "name": "PyBase",
      "url": "https://forge.mql5.io/nique_372/PyBase",
      "rama": "main",
      "comment": "public - logging utilities"
    },
    {
      "name": "ScalerByLeo",
      "url": "https://forge.mql5.io/nique_372/ScalerByLeo",
      "rama": "main",
      "comment": "public - data preprocessing"
    },
    {
      "name": "AiModels",
      "url": "https://forge.mql5.io/nique_372/AiModels",
      "rama": "main",
      "comment": "private repository, Write to me privately (via MQL5.com), my username is nique_372"
    }
  ],
  "min_mt5_build": 5430,
  "py": {
    "min_version": "3.10.9",
    "requirements": "requirements.txt"
  }
}
```

### Example 5: Project with OpenCL

**Repo:** CLByLeo (OpenCL wrappers)

```json
{
  "repos": [
    {
      "name": "TimeUtils",
      "url": "https://forge.mql5.io/nique_372/TimeUtils",
      "rama": "main",
      "comment": "public - utility functions"
    }
  ],
  "min_mt5_build": 5430,
  "opencl": {
    "support_double": true
  }
}
```

### Example 6: Complex (MQL5 + Python + OpenCL)

**Repo:** AiTaskRunner (Complex data generator)

```json
{
  "repos": [
    {
      "name": "AiDataGenByLeo",
      "url": "https://forge.mql5.io/nique_372/AiDataGenByLeo",
      "rama": "main",
      "comment": "core AI library"
    },
    {
      "name": "PyBase",
      "url": "https://forge.mql5.io/nique_372/PyBase",
      "rama": "main",
      "comment": "Python utilities"
    },
    {
      "name": "CLByLeo",
      "url": "https://forge.mql5.io/nique_372/CLByLeo",
      "rama": "main",
      "comment": "OpenCL GPU acceleration"
    }
  ],
  "min_mt5_build": 5430,
  "py": {
    "min_version": "3.10.9",
    "requirements": "requirements.txt"
  },
  "opencl": {
    "support_double": true
  }
}
```

---

## Special Comments

### Standard for `comment` by type

#### Public repos
```json
"comment": "public"
```

#### Private repos (request access)
```json
"comment": "private repository, Write to me privately (via MQL5.com), my username is nique_372"
```

#### Private repos (purchase)
```json
"comment": "private repository, To access the repository, purchase the product: [URL]"
```

#### Optional repos
```json
"comment": "optional - for enhanced features"
```

#### Internal repos
```json
"comment": "internal - TSN ecosystem only"
```

### Comment Templates

Use these templates for consistency:

```
PUBLIC:
"comment": "public"

PRIVATE - REQUEST:
"comment": "private repository, Write to me privately (via MQL5.com), my username is nique_372"

PRIVATE - PURCHASE:
"comment": "private repository, To access the repository, purchase the product: https://www.thebotplace.com/bot/[product-name]"

OPTIONAL:
"comment": "optional - [what it provides]"

INTERNAL:
"comment": "internal - TSN ecosystem only"
```

---

## Automation

### Python Script to Read Dependencies
In the PyBase repository, in the file https://forge.mql5.io/nique_372/PyBase/src/branch/main/DepenciesIns/Main.py you can find the CLeoDepencies class that clones/pulls (updates) the repos of a specific repo based on this standard. Example application in the py file: https://forge.mql5.io/nique_372/MqlCIByLeo/src/branch/main/Src/Py/repo_update.py

This py file can be executed and will ask you as parameters the terminal path, repo URL, and the branch. When executed, it will clone and pull automatically.

### CI/CD Validation

You can visit the repo: https://forge.mql5.io/nique_372/MqlCIByLeo for more info on how it's done there.

---

## Migration of Old Repos

If a repo **doesn't have** `dependencies.json`:

1. **Identify all dependencies**
2. **Create the file** with the format above
3. **Validate** with Python script
4. **Document in README** that it uses this standard

---

## Final Notes
This is a custom and simple standard, perhaps not comparable to professional package managers like pip/npm, etc., given that it doesn't use specific versions of certain repos. Certainly in the last weeks of February 2026, a dependency manager for MQL5 has already been released. We believe it doesn't fit our mixed ecosystem of private and public code. Also note that MQL5 has plans to have a package manager, where the final result is an EX5. If that arrives in MQL5, we will likely migrate most of the libraries to that system.