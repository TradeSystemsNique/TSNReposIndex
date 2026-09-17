# Trade Systems Nique (TSN) Ecosystem Index

> Index of repositories, licenses, projects, etc..

---

## Ecosystem Conventions:
- MQL5 Code: https://forge.mql5.io/nique_372/TSNReposIndex/src/branch/main/Conventions/MQL5.md
- MQL5 Files: https://forge.mql5.io/nique_372/TSNReposIndex/src/branch/main/Conventions/MqlFiles.md
- Dependency management: https://forge.mql5.io/nique_372/TSNDep/src/branch/main/README.md

## Ecosystem Extra

- MQL5 Include: https://forge.mql5.io/nique_372/TSNReposIndex/src/branch/main/Conventions/MqlIncludes.md

## Philosophy
1. Performance-first: reaching the execution speed limits achievable in pure MQL5, across parsing, VM, math, collections, ICT, news, utils, crypto, UI, I/O, and more.
2. Contextual balance: prioritizing maximum speed in critical areas, and a reasonable balance elsewhere — but always leaning toward speed when in doubt.
3. Elegant, usable API: a clean and open interface that never sacrifices developer experience in the name of speed.
  
---

## About TSN

- **Creator:** nique_372
- **Organization:** TSN
- **Platform:** [MQL5 Algo Forge as main platform](https://forge.mql5.io) and [GitHub as a mirror for certain repos (web, mcp, etc.)](https://github.com/TradeSystemsNique) 
- **Products:** [MQL5 Market](https://www.mql5.com/es/users/nique_372/seller) and [TheBotPlace](https://www.thebotplace.com/user/46vILTzIIBbqDhugEvqWGlc8rl52)
- **Contact:**
> - [MQL5 Chats](https://www.mql5.com/es/users/nique_372)
> - [Telegram](http://t.me/trade_system_nique)
  

### Authors
- nique_372: Ecosystem creator & maintainer. Architecture, core libraries, and overall direction.
- Redscam: Author of (QuantumErnLeo, PracticeCode) and co-author of several repositories (such as Gurus 1.2, ICT Estrategias, etc..) focused on ICT bots.

---

## Repositories

> - For the current maintenance/usability status of each repo, see [STATUS.md](./STATUS.md).
> - For pending items regarding the ecosystem with a medium- to long-term horizon, see [GOALS.md](./GOALS.md).

| Repo | Description | Language | License | Access | Type |
|------|-------------|----------|---------|--------|------|
| AiDataGenByLeo | Build AI-powered trading systems with automatic feature generation, via a declarative YAML config schema, and 85+ built-in features. | MQL5, Python, YAML | [NL-ND] | 🌐 Public | Lib |
| AiDataGenByLeoFeaturesDocs | Website for documentation of the features offered by AiDataGenByLeo | MQL5, CSS, JS, HTML, JSON, FGBLC | [NL-ND] | 🌐 Public | Web |
| AiDataTaskRuner | AiDataTaskRuner is a bot with a complex GUI that facilitates data generation and training of ML models based on the AiDataGenByLeo library. | MQL5, C++, Bat, FGBLC, JSON, YAML | [NL-ND] | 🌐 Public | Lib |
| AiDataTaskRunerMcp | MCP server for AiDataTaskRunner Panel (MT5) - Control AiDataTaskRuner Panel for data generation and ML model training via MCP | JSON | [NL-ND] | 🌐 Public | Lib |
| AiFeatureEval | A simple library that allows you to analyze and evaluate the best features for an ML model using correlations, etc. | MQL5 | [NL-NC] | 🌐 Public | Lib |
| AiMcpServ | Part of MQL5 for the MCP server (Complete Orchestrator) | MQL5 | [ARR] | ⛔ Unavailable | Lib |
| AiFullTab | This library simplifies the integration of a subtab (allowing you to configure a Tlgram bot or launch an MCP server) into the desired panel. The idea is to enable a panel to have a tab where the user can configure everything related to an LLM AI model so that it "controls" the panel. | MQL5 | [NL-ND] | 🌐 Public | Lib |
| AiModels | Ai models (Linear regression, etc) in pure MQL5 | MQL5 | [NL-ND-P] | 🔒 Request access | Lib |
| AoByLeo | Genetic and slow optimization algorithms and OpenCL support, useful for implementing self-optimization of EAs in any strategy. | CL, MQL5 | [NL-ND-P] | 🔒 Request access | Lib |
| BasesParserSLan | Base repository for parsers of structured languages (json, yaml, etc.) | MQL5 | [NL-NC] | 🌐 Public | Lib |
| BigNumberByLeo | Fast TSN library for large numbers of X number of bits (unsigned and signed) | MQL5 | [NL-NC] | 🌐 Public | Lib |
| BotKr4v3n5 | MQL5 CRT Trading bot | MQL5 | ? | ⛔ Unavailable | Bot |
| CLByLeo | OpenCL Wrrpers in MQL5 | MQL5 | [NL-ND-P] | 🔒 Request access | Lib |
| ChallangeSimulator | Simulate funding tests in MQL5, useful for validating whether a bot passes a funding test or not. | MQL5 | ? | ⛔ Unavailable | Lib |
| CppBases | Basic utilities for C++, base repository for TSN C++ projects | C++, CMake | [NL-NC] | 🌐 Public | Lib |
| CryptoByLeo | Fast cryptographic library for MQL5 (Hashes [SHA3, SHA2, BLAK2]) (HMAC) (Simetric Cipher - AES - CHACHA20) (Asymetric Chiper ) (Padding (OAEP)) (MaskFunction (MGF1)) | MQL5 | [NL-NC] | 🌐 Public | Lib |
| EAFModExtra | Extra utilities for graphical interfaces (panels) based on the EasyAndFastMod library | MQL5 | [NL-ND-P] | 🔒 Request access | Lib |
| EasyAndFastMod | This repository is a modified version of EasyAndFastGUI. | MQL5 | [NL-ND-P] | 🔒 Request access | Lib |
| EasySbAi | EA that implements the Silver Bullet strategy (easy version) implemented with AI that filters signals and predicts the TP/SL | MQL5, YAML | [FPU] | 🌐 Public | Bot |
| ExpressEvalByLeo | Base language code for the DSLs of the TSN ecosystem, the language supports evaluating mathematical expressions, boolean expressions (with the help of AST), with variables, functions, etc. | MQL5 | [NL-ND] | ⛔ Unavailable | Lib |
| ExtraCodes | Utility codes, such as compiling eas, etc. | MQL5 | [NL-ND-P] | 🔒 Request access | Lib |
| FastCollectionsByLeo | Generic collection library (HashMap, etc.) Fast | MQL5 | [NL-NC] | 🌐 Public | Lib |
| FastNL | Pure MQL5 news library without DLL\WebRequeset, works in tester\live (EX5 Wrraper Library + Extra libs) | MQL5 | [NL-ND-P] | 💰 Paid | Lib |
| FullMt5McpByLeo | Complete MCP server for MT5: Through the MCP protocol, it allows [Trades, Orders, History, Graphic Objects, Terminal Logs, Compilation, etc.] | MQL5, JSON | [NL-ND] | 🌐 Public | Bot\Py server |
| GameTestLib | Simple video games implemented in mql5 | MQL5, CL | ? | 🌐 Public | Bots |
| GeneralByLeo | Indicators, and trailing stop | MQL5 | [NL-ND-P] | 🔗 Unlockable (requires FastNL or ICTLibrary) | Lib + Indicators |
| GrapichsByLeo | framework that contains several libraries for creating graphics in MQL5, such as histograms, text, etc., using a class derived from CCanvas | MQL5 | ? | 🌐 Public | Lib |
| Gurus1.2 | Trading bots, ICT, Price action, Statistics, etc. | MQL5 | ? | ⛔ Unavailable | Bots |
| ICTEstrategias | ICT Trading bots | MQL5 | ? | ⛔ Unavailable | Bots |
| ICTLibrary | Fast ICT library with more than 35 concepts (EX5 Wrraper Library + Extra concepts) | MQL5 | [NL-ND-P] | 💰 Paid | Lib |
| ICTLibraryEasy | ICTLibraryEasy is a fast and simple ICT library that allows you to work with the most well-known ICT concepts such as FVG, Boschoch, Swing, etc. through classes and using the MQLArticles base framework. | MQL5 | Apache 2.0 (with modifications) + [FPU] Only for examples | 🌐 Public | Libs + Bots |
| ICTLibraryExamples | Examples of ICT library usage include more than 50 example bots and implementations of ICT YouTuber strategies in MQL5 | MQL5 | [NL-ND-P] | 🔗 Unlockable (requires ICTLibrary) | Bots |
| IctKiller | Complex AI bot with more than 8 strategies | MQL5 | Custom | ⛔ Unavailable | Bots |
| Introsort | Fork of [amrali/Introsort](https://forge.mql5.io/amrali/Introsort) | MQL5 | [INHERITED] | 🌐 Public | Lib |
| JsonParserByLeo | Fast JSON parser from the TSN ecosystem | MQL5 | [NL-NC] | 🌐 Public | Lib |
| LLmAgentsByLeo | Library that allows you to integrate the LLM agent API as GPT, with memory and tools. (Internal implementation) | MQL5 | [ARR] | ⛔ Unavailable | Lib |
| LLmAgentsFinal | Fast library to integrate any LLM model with MT5... with access to tools, memory, etc. | MQL5 | [NL-ND-P] | 💰 Paid | Lib |
| LLmRegiteryByLeo | models.dev service via DB for MT5 | MQL5, SQL | [NL-NC] | 🌐 Public | Lib |
| LitCycleKiller | Bot ict based on the LitCycle strategy | MQL5 | ? | ⛔ Unavailable | Bot |
| MQL5Book | Fork of [rosh/MQL5Book](https://forge.mql5.io/rosh/MQL5Book) | MQL5 | [INHERITED] | 🌐 Public | All |
| MQLArticles | MQL Articles is a repository that contains the basic structure of the complete framework by Leo\Nique_372, in addition to containing the codes that nique_372 implemented in his MQL5 articles (Ict, Risk Management, Position Management). | MQL5, SFILTER | [NL-NC] | 🌐 Public | Lib + Bots + Indicators |
| McpServer | Library that facilitates the connection of any tool that supports the MCP protocol with functions defined by you for MQL5. | MQL5 | [NL-ND-P] | 💰 Paid | Lib |
| McpServerImp | Implementation of a complete MCP server in C++. This server supports stdin and stdou, and http (using mcp-remote). | C++, CMake | [ARR] | ⛔ Unavailable | Lib + Exe |
| MqlCIByLeo | CI framework for MQL5. Automatically compiles and validates EAs and libraries. | MQL5, Python | [NL-ND] | 🌐 Public | Lib |
| MqlLlmCoderByLeo | LLM model trained with ecosystem code with over 500k lines of very high quality MQL5 code | Python | [ARR] | ⛔ Unavailable | LLM Model |
| MultirangesInd | MetaTrader 5 Indicator that detects consolidation ranges and generates signals based on three customizable strategies | MQL5 | [FPU] | 🌐 Public | Indicator |
| NewsAiEa | AI news trading bot with more than 38 onnx models for predicting current value\movement\dd of events and trading it. | MQL5 | [ARR] | ⛔ Unavailable | Bot |
| PNRGByLeo | Fast library for generating pseudo-random numbers PRNG | MQL5 | [NL-NC] | 🌐 Public | Lib |
| PerfectHashByLeo | Lib to generate perfect hashes | MQL5 | [NL-NC] | 🌐 Public | Lib |
| PracticeCode | Extra practice code | MQL5 | ? | 🌐 Public | Lib + Bots |
| PyBase | PyBase is a base repository that contains basic utilities for simple logging and basic functions. | Python | [NL-NC] | 🌐 Public | Lib |
| QuantumErnLeo | Quantum exploration | MQL5 | ? | ⛔ Unavailable | Lib |
| ScalerByLeo | ScalerByLeo is a library for preprocessing data for ML models using scalers such as maxmin, robust, standard scaler, and also OpenCL can be used for bulk data scaling. | MQL5, OpenCL | [NL-NC] | 🌐 Public | Lib |
| SetFileByLeo | Fast parser of SetFile format | MQL5 | [NL-NC] | 🌐 Public | Lib |
| ShemaJson | Validation JSON\YAML using Shema Json Lib | MQL5 | [NL-NC] | 🌐 Public | Lib |
| SimPHash | Simple perfect hash generator via YAML file | MQL5 | [NL-NC] | 🌐 Public | Lib |
| StatTrading | Patterns Statics | MQL5 | ? | 🌐 Public | Lib |
| StrategyBuilder | Building strategies in MQL5 using a custom language | MQL5, CMODEL, CPATTERN | [ARR] | ⛔ Unavailable | Lib |
| StrategyBuilderApp | CMODEL code editor for building strategies in MQL5 | MQL5, CMODEL, CPATTERN | [ARR] | ⛔ Unavailable | Bots |
| TSNDep | TSNDep - Dependency Manager for TSN MQL5 Ecosystem. Manages dependencies recursively with hooks support | Python | [NL-NC] | 🌐 Public | Lib |
| TSNReposIndex | Index of all my repositories, licenses and projects. TSN Ecosystem | MD | [MIT] | 🌐 Public | Doc |
| TbpWrraper | A set of wrapper classes that make using TheBotPlace API easier. | MQL5, YAML, C++, Python, TOML, CMake | [NL-NC] | 🌐 Public | Lib |
| Team9 | Simple EMA trading bots/Chart patterns | MQL5 | ? | ⛔ Unavailable | Bot |
| TelegramByLeo | Modified and fast Telegram library based on MQL5 article codes | MQL5 | [NL-ND-P] | 🔗 Unlockable (requires FastNL) | Lib |
| TelegramComplex | Telegram bot to send screenshots\messages at OnTradeTransaction events | MQL5 | [NL-NC] | ⛔ Unavailable | Bot |
| TelegramControler | Bot that allows control of MT5 through LLM APIs and commands | MQL5 | ? | ⛔ Unavailable | Bot |
| TheSmcIctIndEx | MQL5 EA examples using The Smc Ict Indicator buffers | MQL5 | [MIT] | 🌐 Public | Bots |
| TheSmcIctindicator | Part of the code for TheSmcIctIndicator | MQL5 | ? | ⛔ Unavailable | Indicator |
| TimeUtils | Fork of [amrali/TimeUtils](https://forge.mql5.io/amrali/TimeUtils) | MQL5 | [INHERITED] | 🌐 Public | Lib |
| TsnTables | Global arrays of the TSN ecosystem | MQL5 | MIT | 🌐 Public | Lib |
| VmByLeo | Complete functional Fast language made in Pure MQL5. Functions, ifs, loops, all MQL5 data types (int, datetime, color, string) | MQL5 | ? | ⛔ Unavailable | Lib |
| WorkflowsByLeo | A library that allows you to run workflows in an MT5 bot. Both asynchronous and synchronous jobs that require OnTimer\OnChartEvent to function... all through a YAML file where the user defines each step of the flow. | MQL5, YAML | [NL-NC] | 🌐 Public | Lib |
| Xoshiro256 | Fork of [amrali/Xoshiro256](https://forge.mql5.io/amrali/Xoshiro256) | MQL5 | [INHERITED] | 🌐 Public | Lib |
| YamlParserByLeo | Fast parser of the YAML format in pure MQL5. With the possibility of fast reading and partial writing. | MQL5, YAML | [NL-ND-P] | 🔗 Unlockable (requires FastNL) | Lib |
| fast_json | Fork of [14134597/fast_json](https://forge.mql5.io/14134597/fast_json) | MQL5, JSON | [INHERITED] | 🌐 Public | Lib |
| ICT | ICT concept library in MQL5 | MQL5 | [ARR] | ⛔ Unavailable | Lib |
| NewsLibrary | News Library | MQL5 | [ARR] | ⛔ Unavailable | Lib |
| Distribuciones | Library of statistical distributions, for predicting events in probability and studying patterns | MQL5 | [ARR] | ⛔ Unavailable | Lib |

---

## Usage rules (summary)

If you use any of my projects, please keep in mind:

1. Always include the original license when redistributing.
2. Accept the license of the repository you wish to use with all its conditions.... if you do not agree, do not use the code from that repository for any purpose.
3. If in doubt about whether your use case is allowed, open an issue or contact me.

---

## Legends

### Licenses

| Tag | Name | Description |
|-----|------|-------------|
| [NL-NC] | Custom No-LLM Non-Commercial | Personal use and free redistribution permitted. Commercial sale of source code requires substantial innovation and written authorization. Selling a compiled End-User Application that incorporates the Software is permitted without authorization. |
| [NL-ND] | Custom No-LLM No-Derivatives | Like NL-NC but commercial sale of source code or any Derivative Work is absolutely prohibited with no exceptions or authorization process. Selling a compiled End-User Application that incorporates the Software as a single binary is permitted. |
| [NL-ND-P] | Custom No-LLM No-Derivatives P=(Requerid acces for Private repos or Paid or Unlocked) | Applies to Software obtained through purchase or unlock or (requerid acces, private) mechanism. Source code must remain strictly private on any platform including Forge. No public redistribution permitted under any circumstance. Selling a compiled End-User Application that incorporates the Software as a single binary is permitted. |
| [FPU] | For Personal Use | Personal use only. Modifications allowed but must remain strictly private. No redistribution or commercial use permitted. |
| [ARR] | All Rights Reserved | No use, access, copying, modification or distribution permitted in any form. |
| [INHERITED] | Inherited License | License defined by the original/parent repository. Refer to the parent repo for full terms. |
| ? | None | The license has not yet been defined for that repository |

### Access
| Badge | Meaning |
|-------|---------|
| 🌐 Public | Freely accessible |
| 💰 Paid | Available for purchase |
| 🔗 Unlockable | Access granted by purchasing a linked repo |
| 🔒 Request access | Private — contact me to get access |
| ⛔ Unavailable | Not accessible at this time |


---

## License
The contents of this index repository are licensed under [MIT](./LICENSE).
Note: Each repository listed above is governed by its own license.