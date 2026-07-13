# SOFTWARE LICENSE AGREEMENT
# Level 1 / NL-NC

---

Copyright 2026 Nique_372 and Leo.

---

## PREAMBLE

This license governs the terms of use, reproduction, distribution and modification of the software contained in this repository (hereinafter, "the Software"). It is inspired by the **OpenRAIL** (Open & Responsible AI License) framework from the RAIL Initiative, with additional restrictions to protect the author against commercial use without added value, against unauthorized public distribution, and against the use of the Software in the training of text generation AI systems.

By accessing, copying, modifying or distributing the Software, you agree to be bound by the terms of this Agreement.

---

## SECTION 1 - DEFINITIONS

- **"Software":** The source code, binaries, documentation and any related material available in this repository.

- **"Derivative Work":** Any work based in whole or in part on the Software, including modifications, adaptations or integrations.

- **"Library Derivative":** Any Derivative Work whose primary purpose is to function as a library, framework, module, or reusable infrastructure component — i.e., a Derivative Work that other developers would incorporate into their own software, rather than a finished end-user application. This includes forks of the Software, wrappers around the Software, and any repackaging of the Software (in whole or in substantial part) as a reusable component, regardless of renaming.

- **"Compiled End-User Product":** A compiled, binary executable (including but not limited to `.ex5` files) whose primary function is to act as a finished trading bot, Expert Advisor, indicator, or similar end-user application — where the Software is used solely as an internal dependency and is not exposed, extracted, or redistributed as a library, and is not itself the product being marketed or sold. A Compiled End-User Product ceases to qualify as such, and is instead treated as a Library Derivative, if its primary practical function is to expose, wrap, or make the Software (or its functionality) separately usable as a library by third parties.

- **"Commercial Use":** Any use of the Software or Derivative Works that generates or is intended to generate economic benefit, whether direct or indirect.

- **"Substantial Innovation":** Addition of new functionalities, significant technical improvements or original developments that provide differential value compared to the original Software. Cosmetic changes, renaming, minor configuration changes or any trivial modification do not constitute Substantial Innovation.

- **"Public Repository":** Any version control hosting service or code platform accessible to the public or to uncontrolled third parties, including but not limited to GitHub, GitLab, Bitbucket, Codeberg, or any similar platform, regardless of whether the repository is indexed by search engines.

- **"Authorized Platform":** MQL5 Algo Forge (https://forge.mql5.io), operated by the original authors of the Software.

- **"Text Generation Model":** Any artificial intelligence system specifically designed to generate, complete, summarize, translate or otherwise produce natural language text, including but not limited to Large Language Models (LLMs), generative pre-trained transformers, instruction-tuned models, chat models, and text-based foundation models (e.g. GPT, Claude, LLaMA, Mistral, Gemini, Grok, QWen, GPT OSS, GLM, Gemini, and similar architectures), whether proprietary or open source. This definition does NOT include machine learning systems whose primary purpose is unrelated to natural language text generation, such as classification models, regression models, recommendation systems, computer vision models, tabular data models, or audio processing models.

---

## SECTION 2 - PERMISSIONS

A limited, non-exclusive permission is granted to:

- Use, copy and modify the Software for **personal use**, whether commercial or non-commercial, without prior authorization.
- Modify the Software for **personal, non-commercial use** without prior authorization.
- Create Derivative Works, subject to the conditions set forth in this Agreement.
- Use the Software in machine learning pipelines, datasets or systems that are **not** Text Generation Models as defined in Section 1.
- Store the Software in a **private repository** (not publicly accessible) for personal backup or version control purposes.
- **Freely redistribute** the Software — original or modified — at no cost, on any platform, provided the conditions of Section 3(c) are met.
- **Build and commercialize a Compiled End-User Product** that uses the Software solely as an internal dependency, without prior authorization, subject to the conditions of Section 4(4).

---

## SECTION 3 - DISTRIBUTION

Distribution of the Software's source code is governed as follows:

**(a)** Storage and hosting of the Software's source code is permitted under the following conditions:
  - On the **Authorized Platform** (MQL5 Algo Forge): public or private repositories are permitted,
    subject to the distribution conditions of sections (b) and (c).
  - On **any other platform**: storage is permitted exclusively in private repositories that
    guarantee no public access, no indexing by search engines, and no access by automated
    crawlers or data collection systems.
  - Hosting the Software on any other platform in a publicly accessible form is **strictly prohibited**.

**(b)** Free redistribution of the Software — original or modified — is **permitted**,
  provided:
  - The storage and hosting conditions of section (a) are met.
  - The original license is preserved and included in full.
  - The original authors (Nique_372 and Leo) are clearly attributed.
  - The redistributed version is not presented as an original independent work.
  - Forks are only permitted on the Authorized Platform or in strictly private
    repositories meeting the conditions of section (a).

**(c)** Any commercial redistribution, sale, or monetization of the Software, or of any
  Library Derivative, requires prior contact with the original authors and explicit written
  authorization. Full conditions are defined in Section 4.

  This subsection (c) does **not** apply to the sale or commercialization of a Compiled
  End-User Product, which is governed exclusively by Section 4(4).

---

## SECTION 4 - COMMERCIAL USE RESTRICTION

Commercial Use of the Software is **conditioned** as follows:

1. The sale, licensing or commercialization of the Software in its original form is **prohibited**.

2. The commercialization of a Library Derivative that does not incorporate Substantial Innovation
   over the original Software is **prohibited**.

3. Commercialization of a Library Derivative is **permitted** only where it incorporates verifiable
   and documented Substantial Innovation, and only with **explicit written authorization
   by the original authors**, who reserve the sole right to determine whether Substantial
   Innovation has been achieved.

4. The sale or commercialization of a **Compiled End-User Product** that uses the Software
   solely as an internal dependency is **permitted without prior authorization**, regardless
   of whether the seller is an individual, company, or any other type of entity, **provided
   that all of the following conditions are met**:
   - The Software, and any Library Derivative of it, is not distributed, exposed, extracted,
     or made separately usable as a library within or alongside the Compiled End-User Product.
   - The source code of the Software is not included or distributed together with the
     Compiled End-User Product.
   - The Compiled End-User Product does not present itself as, replace, or compete with the
     Software as a library or infrastructure offering.

   Paragraphs 1, 2 and 3 of this Section do not apply to a Compiled End-User Product that
   satisfies the conditions above.

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