---
name: TSN MQL5 Conventions
version: "1.1.1"
description: Apply TSN (Trade System Nique) MQL5 code conventions and standards. Use this skill whenever writing, editing, reviewing, or scaffolding MQL5 code (.mq5, .mqh files) — Expert Advisors, indicators, scripts, or libraries — especially within the TSN ecosystem or using nique_372 repositories (AiDataGenByLeo, ICTLibraryEasy, FastNL, TSNDep, etc.). Trigger on any MQL5 coding task, whether or not the user explicitly names TSN, since these conventions should apply by default to all MQL5 work in this environment.
---

# TSN MQL5 Code Conventions

This skill provides access to Trade System Nique's official MQL5 coding standards and best practices.

## When to use this skill

Apply these conventions whenever:
- Writing MQL5 code for the TSN ecosystem
- Using libraries from nique_372 repositories
- Reviewing code for TSN standards compliance
- Setting up MQL5 projects within the TSN ecosystem

## Naming Conventions

See: [MQL5 Conventions](Conventions/MQL5.md)

## Code Optimization for Final Apps

See: [MQL5 Apps Final Optimization](Opt/AppFinal.md)

## Project Structure

See: [MQL5 Project Structure](Conventions/MqlFiles.md)

## README Structure

See: [README Conventions](Conventions/Readmes.md)

## Storage\Commits

[See](Conventions/Storage.md)

## Dependency Management
- **[TSNDep](https://forge.mql5.io/nique_372/TSNDep/src/branch/main/README.md)**: Dependency management for TSN
- **[Commands Reference](https://forge.mql5.io/nique_372/TSNDep/wiki/Commands.md):** Detailed description of each command
- **[dependencies.json Format](https://forge.mql5.io/nique_372/TSNDep/wiki/DependenciesF.md):** Full dependencies.json specification
- **[Hooks Guide](https://forge.mql5.io/nique_372/TSNDep/wiki/Hooks.md):** Hook system and examples

## TSN Repositories

For a complete list of available TSN repositories and their status, license, etc., see:
[Dependency Management](README.md)

## Basic rules for getting started

Typically, a project that uses the ecosystem as a prerequisite should:
1. Identify the dependencies that are needed and install them
2. Have the MQH (proxies)
3. Generally, when working with the TSN ecosystem, we use GIT, so it's best to use a repository for the code...
   although the "traditional MQL5 style" can also be used — a folder under Expert\ or Include\ as the project...
   but the recommendation is to use GIT (either on github.com or MQL5 Algo Forge (recommended, although it depends on your needs))

Once the above is complete... another basic rule to mention is...
The separation of read/write access:

1. For repositories within the TSN ecosystem: Read-only. If you find a bug or something worth noting, report it to the user.
2. For project repositories: Full read and write access.