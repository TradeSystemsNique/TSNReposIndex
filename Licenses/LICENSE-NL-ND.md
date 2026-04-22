# SOFTWARE LICENSE AGREEMENT - RESTRICTED SOURCE
# Level 2 / NL-ND

---

Copyright 2026 Nique_372 and Leo.

---

## PREAMBLE

This license governs the terms of use, reproduction, distribution and modification of the software contained in this repository (hereinafter, "the Software"). It is inspired by the **OpenRAIL** (Open & Responsible AI License) framework from the RAIL Initiative, with additional restrictions to protect the author against unauthorized distribution, commercial exploitation of the source code, and the use of the Software in the training of text generation AI systems.

This license is **more restrictive** than the Level 1 / NL-NC license. If you are looking for a less restrictive version, refer to the NL-NC license available in other repositories by the same author.

By accessing, copying, modifying or using the Software, you agree to be bound by the terms of this Agreement.

---

## SECTION 1 - DEFINITIONS

- **"Software":** The source code, binaries, documentation and any related material available in this repository.

- **"Derivative Work":** Any work based in whole or in part on the Software, including modifications, adaptations, ports, wrappers, forks or repackaged versions, whether distributed as source code or compiled binaries.

- **"End-User Application":** A single compiled executable product (e.g. a trading bot or Expert Advisor) whose binary incorporates the Software compiled within it, such that the Software's source code is not exposed, separable, or independently redistributable from the product. A product that ships the Software as a separate compiled binary (e.g. a standalone .ex5 library file) does NOT qualify as an End-User Application under this definition.

- **"Commercial Use":** Any use of the Software or Derivative Works that generates or is intended to generate economic benefit, whether direct or indirect.

- **"Public Repository":** Any version control hosting service or code platform accessible to the public or to uncontrolled third parties, including but not limited to GitHub, GitLab, Bitbucket, Codeberg, or any similar platform, regardless of whether the repository is indexed by search engines.

- **"Authorized Platform":** MQL5 Algo Forge (https://forge.mql5.io/), operated by the original authors of the Software.

- **"Text Generation Model":** Any artificial intelligence system specifically designed to generate, complete, summarize, translate or otherwise produce natural language text, including but not limited to Large Language Models (LLMs), generative pre-trained transformers, instruction-tuned models, chat models, and text-based foundation models (e.g. GPT, Claude, LLaMA, Mistral, Gemini, and similar architectures), whether proprietary or open source. This definition does NOT include machine learning systems whose primary purpose is unrelated to natural language text generation, such as classification models, regression models, recommendation systems, computer vision models, tabular data models, or audio processing models.

---

## SECTION 2 - PERMISSIONS

A limited, non-exclusive, non-transferable permission is granted to:

- Use and modify the Software for **personal use**, whether commercial or non-commercial, without prior authorization.
- Store the Software in a private repository for personal backup or version control purposes, subject to the conditions of Section 3(a).
- Create Derivative Works for **personal use only**, subject to the conditions of this Agreement.
- Develop and **commercially sell End-User Applications** as defined in Section 1, provided the conditions of Section 4(c) are met.
- Use the Software in machine learning pipelines, datasets or systems that are **not** Text Generation Models as defined in Section 1.

---

## SECTION 3 - DISTRIBUTION

Distribution of the Software's source code is governed as follows:

**(a)** Storage and hosting of the Software's source code is permitted under the following conditions:

  - On the **Authorized Platform** (MQL5 Algo Forge): public or private repositories are permitted, subject to the distribution conditions of sections (b) and (c).
  - On **any other platform**: storage is permitted exclusively in private repositories that guarantee no public access, no indexing by search engines, and no access by automated crawlers or data collection systems.
  - Hosting the Software on any other platform in a publicly accessible form is **strictly prohibited**.

**(b)** Free redistribution of the Software — original or modified — is **permitted**, provided:
  - The storage and hosting conditions of section (a) are met.
  - The original license is preserved and included in full.
  - The original authors (Nique_372 and Leo) are clearly attributed.
  - The redistributed version is not presented as an original independent work.
  - Forks are only permitted on the Authorized Platform or in strictly private repositories meeting the conditions of section (a).

**(c)** Any commercial redistribution, sale, or monetization of the Software's source code —
  original or modified — is **strictly and absolutely prohibited**, without exception and
  without possibility of authorization. This prohibition is non-waivable.

---

## SECTION 4 - COMMERCIAL USE RESTRICTION

Commercial use of the Software is **conditioned** as follows:

**(a)** The sale, licensing or commercialization of the Software's source code in its original or modified form is **strictly and absolutely prohibited**, without exception.

**(b)** The sale, licensing or commercialization of any Derivative Work distributed as source code or as a separately compiled binary (e.g. a standalone .ex5 library file) is **strictly prohibited**, regardless of the degree of modification or innovation introduced.

**(c)** The sale of End-User Applications as defined in Section 1 is **permitted**, provided:
  - The Software is compiled within the End-User Application as a single binary and is not shipped as a separate file.
  - The Software's source code is not included, exposed, or independently redistributable within the product.
  - The product is not itself a library, module, or reusable code component.
  - This license is referenced in the product's documentation.

**Example:** Selling a trading bot or Expert Advisor (EA) as a single compiled .ex5 file that incorporates this library's code within it is permitted. Selling the library's source code, a modified version of it, or shipping the library as a separate .ex5 file alongside any product is prohibited.

**(d)** Unlike the Level 1 / NL-NC license, there is **no review or authorization process** available for commercial use of the source code or any Derivative Work. This restriction is absolute and non-negotiable.

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

## Trademarks and Brand Identity

The following names, usernames, aliases, and all associated logos, icons,
and visual assets included in this repository are the exclusive property
of their respective authors:

- "Nique"
- "Leo"
- "Nique-Leo"
- "NiqueAndLeo"
- "nique_372"
- "TSN"
- "Trade Systems Nique"
- The name and title of the specific product or repository
  to which this license file is attached

The following are strictly PROHIBITED:

* Using any of the above names, usernames, or logos to endorse, promote,
  or misrepresent any product, service, or derivative work
* Presenting any modified or unmodified version of this software
  as being officially created, endorsed, or affiliated with the authors
* Reproducing or distributing any logo, icon, or brand asset
  included in this repository for any purpose other than running
  the software as originally intended
* Using any of the above names in domain names, social media handles,
  product names, or commercial offerings without explicit written
  permission from the authors

No trademark or brand rights of any kind are granted under this license.

---

## SECTION 6 - DISCLAIMER OF WARRANTIES

THE SOFTWARE IS PROVIDED "AS IS", WITHOUT WARRANTY OF ANY KIND, EXPRESS OR IMPLIED, INCLUDING BUT NOT LIMITED TO THE WARRANTIES OF MERCHANTABILITY, FITNESS FOR A PARTICULAR PURPOSE AND NON-INFRINGEMENT. IN NO EVENT SHALL THE AUTHORS BE LIABLE FOR ANY DIRECT, INDIRECT, INCIDENTAL OR CONSEQUENTIAL DAMAGES ARISING FROM THE USE OF THE SOFTWARE.

---

## REFERENCES

This instrument is inspired by:
- [BigScience OpenRAIL-M License](https://www.licenses.ai/blog/2022/8/26/bigscience-open-rail-m-license)
- [RAIL Initiative](https://www.licenses.ai)
- [Business Source License (BUSL)](https://mariadb.com/bsl11/)