# File Conventions

This MD details how files should be named, project structure, etc.

## File Naming

- Type: PascalCase, examples:
```
Core.mqh
Main.mqh
```

> By the way, I usually use names like Main, Defines, or Functions for small EAs or those with simple logic; if you have more than 4 or 5 
> .mqh files, it's better to use more descriptive names—like Core, Logger, 
> or something informative—rather than generic ones, to improve readability.

## Language
- English, preferably... but only if it comes naturally to you; otherwise, use whichever language you prefer.

> In the case of TSN Ecosystem, I’d say that around 60–80% of the files are in EN, and the rest are in ES.


## Extra files (in the root directory)
1. CHANGELOG.md: Not mandatory, but good to have.
2. CONTRIBUTING.md: Also not mandatory; it’s optional. In the case of TSN—since it’s a bit more niche—we don’t include one.
3. SECURITY.md: Depends on the nature of your project; it’s rarely used in MQL5.
4. AI-related files (e.g., CLAUDE.md, AGENTS.md): Place these in an `Agents/` directory at the root level, or in subfolders if necessary.


## Templates

Below are some specific templates for organizing files, depending on the type of project.
It is also worth noting that, beyond this, the ecosystem depends on the specific repository structure—there may be a few additional folders—but
in summary:
- Final Apps: An `src` folder for the main code and class tests (containing defines, functions, classes, GUIs, and all logic-related elements);
 a `Market` or `Images` folder for repository assets (such as screenshots of the running app, logs, etc.); 
 and the EA itself at the project root, alongside repository dependencies, the license, and any other necessary Markdown files 
 (changelog, contributing guidelines, notices, LLMs, etc.).
- Libraries: An `src` folder (for logic); a `Validate` or `Wf` folder (for CI workflows); a `Test` or `Examples` folder (
for benchmarks or additional examples); and the dependencies, README, license, and any other required files at the root.

### Project Structure for EAs (Utils - App)

```
RepoName/
├── # Note: Folders for workflows, etc. may be included here
├── Src/         # Actual code of the repo
└── Images/      # Images to be used in the wiki/MDs/banner of the repo
```

### Project Structure for Libraries

For projects that are modules/libraries, the following structure is recommended:

```
RepoName/
├── # Note: Folders for workflows, etc. may be included here
├── Docs/          # Extra documentacion por doxygen (extra pages)
├── Agents/        # Skills\AGENTS.md\CLUADE.md, etc..
├── Src/           # Actual code of the repo
├── Validation/    # Folder for final repo tests (for CI)
└── Images/        # Images to be used in the wiki/MDs/banner of the repo
```

### Project Structure for EAs (Trading) (Non-AI)

For projects that are modules/libraries, the following structure is recommended:

```
RepoName/
├── # Note: Folders for workflows, etc. may be included here
├── Core/          # Main + Defines + EAName + Global + (Functions if applicable)
├── Validation/    # Folder for final EA tests (for CI)
├── Resrc/         # Embedded resources (optional, only if applicable)
└── Images/        # Images to be used in the wiki/MDs/banner of the repo
```

### Project Structure for EAs Implementing AI (AiDataGenByLeo Convention)

For projects that are modules/libraries, the following structure is recommended:

```
RepoName/
├── # Note: Folders for workflows, etc. may be included here
├── AiAd/          # Folder for prediction classes
├── Models/        # Integration of specific ONNX models
├── Core/          # Main + Defines + EAName + Global + (Functions if applicable)
├── Resrc/         # Embedded resources of the EA
├── Validation/    # Folder for final EA tests (for CI)
└── Images/        # Images to be used in the wiki/MDs/banner of the repo
```