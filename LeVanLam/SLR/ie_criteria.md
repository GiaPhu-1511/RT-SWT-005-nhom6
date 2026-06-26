# IE Criteria — LLM-based REST API Test Generation and Testing

**Member:** [Le Van Lam]

**RQ:**
For REST APIs with OpenAPI specifications, do LLM-generated API test cases achieve higher coverage and bug detection compared with traditional/manual approaches?

**PICO:**
P = REST APIs with OpenAPI specifications
I = LLM-generated API test cases
C = Manual test design / Traditional testing approaches
O = Coverage, bug detection, test effectiveness

---

## 1. Inclusion Criteria (IC)
To be included in the review, a study must satisfy ALL of the following conditions:
* **IC1 (Domain):** The study must explicitly target RESTful APIs, Web APIs, Microservices, or Web Services.
* **IC2 (Task):** The core contribution must involve software quality assurance activities, specifically automated test case generation, fuzzing, test script synthesis, assertion generation, or vulnerability/bug detection.
* **IC3 (Technology):** The methodology must utilize Generative AI, Large Language Models (LLMs), Machine Learning (ML), Deep Learning (DL), or Natural Language Processing (NLP) techniques.
* **IC4 (Study Type):** The paper must be a peer-reviewed journal article, conference proceeding, or a rigorous academic preprint/thesis available with full-text access.

## 2. Exclusion Criteria (EC)
A study is excluded if it meets ANY of the following conditions:
* **EC1 (System/Empty Records):** The record is an empty system artifact, search portal index placeholder, or citation metadata missing a title/abstract (e.g., "Works search | OpenAlex").
* **EC2 (Out of Scope Domain):** The paper focuses on general software testing (e.g., UI testing, mobile app testing, general unit testing like Java/C++ code without an API context), embedded systems, or automotive PLC testing.
* **EC3 (Out of Scope Task):** The study uses LLMs/AI for API design, documentation generation (e.g., OpenAPI specification generation from natural language), or code refactoring, rather than active execution testing or quality evaluation.
* **EC4 (No AI/LLM Component):** The paper relies strictly on traditional black-box, white-box, or search-based testing techniques (e.g., pure genetic algorithms, random partition testing) without integrating any modern Machine Learning or LLM frameworks.

## 3. Screening Summary (V1 Phase)
* **Total Records Evaluated:** 39
* **Records Included:** 20 (Met all ICs)
* **Records Excluded:** 19 (Failed on one or more ECs)

## 4. Full-Text Quality Assessment Criteria (V2 Screening)
To ensure the selected papers provide rigorous evidence, each of the 20 included papers must satisfy the following Quality Assessment (QA) criteria during full-text reading:

* **QA1 (Methodology Clarity):** Does the paper clearly describe the prompt engineering strategy, agent architecture, or fine-tuning process used for the LLM?
* **QA2 (Evaluation Metrics):** Does the study evaluate the outcomes using concrete metrics such as API endpoint coverage, line/branch coverage, or the number of valid bugs/vulnerabilities detected?
* **QA3 (Empirical Grounding):** Is the method tested on real-world REST APIs, open-source benchmarks (e.g., benchmark tools, microservice systems), or industrial case studies?
* **QA4 (Completeness):** Is the paper a full-length research contribution (typically > 5 pages for conferences/journals, or a complete thesis), excluding short abstracts or presentation slides?