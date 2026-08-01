# README Conventions - TSN Ecosystem

> How to write a `README.md` for any repository in the TSN ecosystem

---

## Table of Contents

1. [Badges Banner](#1-badges-banner)
2. [Description / Overview](#2-description--overview)
3. [Main Features](#3-main-features)
4. [Repository Structure](#4-repository-structure)
5. [License Warning](#5-license-warning-conditional)
6. [Requirements](#6-requirements)
7. [Installation](#7-installation)
8. [Quick Start](#8-quick-start)
9. [License](#9-license)
10. [Documentation](#10-documentation-conditional)
11. [Contact](#11-contact)
12. [Copyright Footer](#12-copyright-footer)

Sections marked **(conditional)** are only included when they apply to the repo (e.g. no `Documentation` section if there's no wiki, no `License Warning` if the repo is fully public).

---

## 1. Badges Banner

Centered, top of the file. Language, platform, author, and profile link at minimum. Use `shields.io` flat-square badges.

```html
<p align="center">
  <img src="https://img.shields.io/badge/Language-MQL5-1B6CA8?style=flat-square"/>
  <img src="https://img.shields.io/badge/Platform-MetaTrader%205-0D1B2A?style=flat-square"/>
  <img src="https://img.shields.io/badge/Author-nique__372-C9D6DF?style=flat-square&logoColor=white"/>
  <img src="https://img.shields.io/badge/MQL5.com-nique__372-1B6CA8?style=flat-square"/>
</p>
```

If the repo has a defined license tag ([NL-NC], [NL-ND], [FPU], [ARR]...), the corresponding badge from [Badges/BADGES.md](../Badges/BADGES.md) can be added here too.

---

## 2. Description / Overview

One short paragraph, centered, directly under the badges. States **what** the repo does and **how** (architecture/approach in one line), not a marketing pitch.

```html
<p align="center">
A high-performance, memory-free JSON parser for MQL5, based on a flat tape architecture.<br/> Single-pass iterative state machine, no recursion, no dynamic memory fragmentation.
</p>
```

---

## 3. Main Features

`## Main Features` heading, bullet list, each feature bolded and explained in one line. This is the only section that is **always required in full**, since it's the core of the README.

```markdown
## Main Features

- **Tape-based zero-alloc model**: the entire JSON is parsed into a single contiguous `long[]` array
- **Single flat loop**: one `switch` over a token enum, strictly O(n)
- **Handle-based navigation**: `CJsonNode` is a lightweight struct, copying is free
```

### Sub-sections (add as needed, always with code)

- **Usage examples** (mandatory): one `###` sub-section per relevant use case, each with a working MQL5/SQL snippet. Never describe usage only in prose.
- **Benchmarks** (conditional): if performance is a selling point, include a results table (parser/lib, language, time), plus a `## Machine` section describing the test rig, and a `## Performance notes` section if runtimes differ (MQL5 build, Python/C++ versions).
- **Article references** (conditional): if the repo is tied to a published MQL5 article, link it here.

---

## 4. Repository Structure

Tree view of the top-level layout, each entry with a short inline comment. Follows [MqlFiles.md](MqlFiles.md) conventions for folder names.

```markdown
## Repository Structure

\`\`\`
RepoName/
├── Src/   # Full code
├── Test/  # Tests and benchmarks
└── Wf/    # Unit tests
\`\`\`
```

---

## 5. License Warning (conditional)

Only if the repo requires a purchase, unlock, or explicit request for access ([NL-ND-P], paid, or unlockable per [TSNReposIndex/README.md](../README.md) legend). State clearly what's required before the code is usable, and link to the product/unlock page.

```markdown
## ⚠️ License Notice

This repository requires a valid unlock/purchase of **FastNL** to compile. See [MQL5 Market](https://www.mql5.com/es/users/nique_372/seller) for details.
```

Skip this section entirely for `🌐 Public` repos.

---

## 6. Requirements

Points to `dependencies.json` as the source of truth, plus any non-dependency requirement (MT5 build, WebRequest whitelist, external service).

```markdown
## Requirements

See [dependencies.json](./dependencies.json) for the full list.

- MetaTrader 5, build 5430+
- WebRequest access enabled for `https://models.dev`
```

---

## 7. Installation

Always via `tsndep`, pointing at the repo's own `.git` URL.

```markdown
## Installation

\`\`\`bash
cd "C:\Users\YOUR_USER\AppData\Roaming\MetaQuotes\Terminal\YOUR_ID\MQL5\Shared Projects"
tsndep install "https://forge.mql5.io/nique_372/RepoName.git"
\`\`\`

Requires the \`tsndep\` package, available on [PyPI](https://pypi.org/project/tsndep). It automatically downloads and installs all declared dependencies.
```

---

## 8. Quick Start

Numbered steps (bold step titles), minimal working path from include to first result. 2-4 steps is the target; if it needs more, it probably belongs in `Documentation` instead.

```markdown
## Quick Start

**1. Include the library:**

\`\`\`mql5
#include "..\\RepoName\\Src\\Main.mqh"
\`\`\`

**2. Use it:**

\`\`\`mql5
TSN::CMyClass obj;
obj.Init();
\`\`\`
```

---

## 9. License

Always the same two lines, linking the repo's own `LICENSE` file — never re-explain the license terms inline.

```markdown
## License

**[Read Full License](./LICENSE)**
By downloading or using this repository, you accept the license terms.
```

---

## 10. Documentation (conditional)

Only a link out (wiki, docs site, article series) — never duplicate the wiki content into the README.

```markdown
## Documentation

Full API reference: [Wiki](https://forge.mql5.io/nique_372/RepoName/wiki)
```

Skip if there's no wiki/external doc; in that case the README + inline code comments are the documentation (see [MQL5.md § Comments and Documentation](MQL5.md#comments-and-documentation)).

---

## 11. Contact

Same block across all repos.

```markdown
## Contact

- **Platform:** [MQL5 Community](https://www.mql5.com/es/users/nique_372)
- **Profile:** https://www.mql5.com/es/users/nique_372
- **Articles:** https://www.mql5.com/es/users/nique_372/publications
```

---

## 12. Roadmap section (optional, place before Contact)

For active repos with a visible direction, add a `## Roadmap` with a flat bullet list, each item tagged with status/date when resolved:

```markdown
## Roadmap

- Add support for X [In progress]
- Add support for Y [Added 24/7/26]
```

---

## 13. Copyright Footer

Optional horizontal banner at the very end, used mainly for larger/product-grade repos. Small, centered, italic.

```html
<p align="center"><sub>Copyright © <YEAR> Niquel & Leo — TSN Ecosystem</sub></p>
```


---

**Questions or suggestions?** Open an issue or contact [@nique_372](https://www.mql5.com/es/users/nique_372)