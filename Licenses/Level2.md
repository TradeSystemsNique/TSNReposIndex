# SOFTWARE LICENSE AGREEMENT - RESTRICTED SOURCE
# Level 2 / NL-ND

---

Copyright 2026 Nique_372 and Leo.

---

## PREAMBLE

This license governs the terms of use, reproduction, distribution and modification of the software contained in this repository (hereinafter, "the Software"). It is inspired by the **OpenRAIL** (Open & Responsible AI License) framework from the RAIL Initiative, with additional restrictions to protect the author against unauthorized distribution, commercial exploitation of the source code, and the use of the Software in the training of text generation AI systems.

This license is **more restrictive** than the standard Nique_372 Custom No-LLM license. If you are looking for a less restrictive version, refer to the standard license available in other repositories by the same author.

By accessing, copying, modifying or using the Software, you agree to be bound by the terms of this Agreement.

---

## SECTION 1 - DEFINITIONS

- **"Software":** The source code, binaries, documentation and any related material available in this repository.

- **"Derivative Work":** Any work based in whole or in part on the Software, including modifications, adaptations, ports, wrappers, forks or repackaged versions, whether distributed as source code or compiled binaries.

- **"Library Derivative":** A Derivative Work whose primary purpose is to function as a reusable software library, module, framework or code component intended to be linked against or imported by other software.

- **"End-User Application":** A compiled, executable product (e.g. a trading bot, Expert Advisor, script or tool) that uses or links against the Software as a dependency, but does not expose or redistribute the Software's source code.

- **"Commercial Use":** Any use of the Software or Derivative Works that generates or is intended to generate economic benefit, whether direct or indirect.

- **"Public Repository":** Any version control hosting service or code platform accessible to the public or to uncontrolled third parties, including but not limited to GitHub, GitLab, Bitbucket, Codeberg, or any similar platform, regardless of whether the repository is indexed by search engines.

- **"Authorized Platform":** MQL5 Algo Forge (algforge.mql5.com), operated by the original authors of the Software.

- **"Text Generation Model":** Any artificial intelligence system specifically designed to generate, complete, summarize, translate or otherwise produce natural language text, including but not limited to Large Language Models (LLMs), generative pre-trained transformers, instruction-tuned models, chat models, and text-based foundation models (e.g. GPT, Claude, LLaMA, Mistral, Gemini, and similar architectures), whether proprietary or open source. This definition does NOT include machine learning systems whose primary purpose is unrelated to natural language text generation, such as classification models, regression models, recommendation systems, computer vision models, tabular data models, or audio processing models.

---

## SECTION 2 - PERMISSIONS

A limited, non-exclusive, non-transferable permission is granted to:

- Use and modify the Software for **personal, non-commercial purposes**.
- Store the Software in a **private repository** (not publicly accessible) for personal backup or version control purposes.
- Develop and **commercially sell End-User Applications** (e.g. trading bots, Expert Advisors) that use or link against the Software as a compiled dependency, provided the Software's source code is not included, exposed or redistributable within that product.
- Use the Software in machine learning pipelines, datasets or systems that are **not** Text Generation Models as defined in Section 1.

---

## SECTION 3 - SOURCE CODE DISTRIBUTION RESTRICTION

The distribution of the Software's source code is **strictly restricted** as follows:

**(a)** Redistributing, sharing, publishing or transmitting the Software's source code to any third party, in original or modified form, is **prohibited**.

**(b)** Uploading or hosting the Software's source code on any Public Repository is **prohibited**, even if the repository is marked as private on that platform, unless the platform guarantees that the content is inaccessible to the platform operator and to automated data collection systems.

**(c)** The only authorized public distribution channel for the Software is the **Authorized Platform** (MQL5 Algo Forge), exclusively under the control of the original authors.

**(d)** Storing the Software in a **genuinely private repository** (access restricted exclusively to the user) for personal backup purposes is **permitted**, provided no redistribution occurs.

---

## SECTION 4 - COMMERCIAL USE RESTRICTION

Commercial use of the Software is **conditioned** as follows:

**(a)** The sale, licensing or commercialization of the Software's source code in its original or modified form is **prohibited**.

**(b)** The sale, licensing or commercialization of any Library Derivative — whether distributed as source code or as compiled binaries whose primary purpose is to serve as a reusable library or module — is **prohibited**, regardless of the degree of modification or innovation introduced.

**(c)** The sale of End-User Applications (e.g. trading bots, Expert Advisors, scripts or tools) that use or link against the Software as a compiled dependency is **permitted**, provided:
  - The Software's source code is not included or exposed in the product.
  - The product is not itself a library, module or reusable code component.
  - This license is referenced in the product's documentation.

**Example:** Selling an Expert Advisor (EA) that imports this library as a compiled dependency is permitted. Selling a modified or extended version of this library's source code, or a compiled library derived from it, is prohibited.

---

## SECTION 5 - PROHIBITION ON USE IN TEXT GENERATION AI MODELS

The following is expressly **prohibited** under any circumstance and without exception, specifically with respect to Text Generation Models as defined in Section 1:

**(a)** Using the Software, in its original form or as a Derivative Work, to train, fine-tune, evaluate or improve any Text Generation Model.

**(b)** Including the Software, or any Derivative Work thereof, in datasets intended for the training of Text Generation Models.

**(c)** Using the outputs, results or artifacts generated by the execution of the Software as training data for Text Generation Models.

**(d)** Performing any of the above acts indirectly, through third parties, intermediary services, automated pipelines or any other mechanism.

This prohibition is explicitly **limited to Text Generation Models** and does not restrict the use of the Software in any other type of machine learning system (e.g. classification, regression, recommendation, computer vision, tabular data, or audio models).

**This prohibition extends to all Derivative Works and is non-waivable.**

---

## SECTION 5B - USER OBLIGATIONS WHEN USING TEXT GENERATION PLATFORMS

Any individual or entity that uses the Software (or Derivative Works) in conjunction with a hosted Text Generation Model (e.g. Claude, ChatGPT, Gemini, Copilot, or similar cloud-based services) MUST:

**(a)** Disable any data retention, training opt-in, or conversation logging feature offered by the platform BEFORE using the Software in that context.

**(b)** Use the platform's official "privacy mode", "incognito mode", or equivalent feature if available (e.g. Claude's conversation opt-out, ChatGPT's "Improve the model" toggle).

**(c)** NOT use the Software through platforms that offer no mechanism whatsoever to opt out of training data collection.

Failure to comply with this section constitutes a violation of Section 5(d) of this Agreement.

**Note on local/open-source models:** The use of the Software as input to locally-run Text Generation Models operating solely in inference mode (i.e. no training, fine-tuning or dataset collection occurs) is NOT prohibited by Section 5, provided no training activity as described in Section 5(a)-(c) takes place.

---

## SECTION 6 - DISCLAIMER OF WARRANTIES

THE SOFTWARE IS PROVIDED "AS IS", WITHOUT WARRANTY OF ANY KIND, EXPRESS OR IMPLIED, INCLUDING BUT NOT LIMITED TO THE WARRANTIES OF MERCHANTABILITY, FITNESS FOR A PARTICULAR PURPOSE AND NON-INFRINGEMENT. IN NO EVENT SHALL THE AUTHORS BE LIABLE FOR ANY DIRECT, INDIRECT, INCIDENTAL OR CONSEQUENTIAL DAMAGES ARISING FROM THE USE OF THE SOFTWARE.

---

## REFERENCES

This instrument is inspired by:
- [BigScience OpenRAIL-M License](https://www.licenses.ai/blog/2022/8/26/bigscience-open-rail-m-license)
- [RAIL Initiative](https://www.licenses.ai)
- [Business Source License (BUSL)](https://mariadb.com/bsl11/)