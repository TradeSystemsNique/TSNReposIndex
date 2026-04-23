# File Conventions

This MD details how files should be named, project structure, etc.

## File Naming

- Type: PascalCase, examples:
```
Core.mqh
Main.mqh
```
This applies only to actual MQL5 code files. In case other ecosystems are combined (e.g., web/Python), naming conventions from those ecosystems may be accepted.

## Project Structure for Libraries

For projects that are modules/libraries, the following structure is recommended:

```
RepoName/
├── # Note: Folders for workflows, etc. may be included here
├── Src/           # Actual code of the repo
├── Validation/    # Folder for final repo tests (for CI)
└── Images/        # Images to be used in the wiki/MDs/banner of the repo
```

## Project Structure for EAs (Non-AI)

For projects that are modules/libraries, the following structure is recommended:

```
RepoName/
├── # Note: Folders for workflows, etc. may be included here
├── Core/          # Main + Defines + EAName + Global + (Functions if applicable)
├── Validation/    # Folder for final EA tests (for CI)
├── Resrc/         # Embedded resources (optional, only if applicable)
└── Images/        # Images to be used in the wiki/MDs/banner of the repo
```

## Project Structure for EAs Implementing AI (AiDataGenByLeo Convention)

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