# ESGReady — An Evidence-Grounded ESG Questionnaire Assistant for Malaysian SMEs

> A proposed assistant that maps supplier ESG questions to selected disclosure guidance, checks supporting company evidence and prepares cited drafts for human review.

**Project status.** Labs 1 and 2 establish the project and its design. The separate executed Lab 3 notebook records a 26-chunk K1 run. Lab 4 reviewed those chunks and produced eight verified guidance passages. See [the quality report](docs/week4_data_quality_report.md) and [the reproduction guide](docs/week4_guide.md). Assistant runtime, company-evidence assessment and model evaluation remain planned.

## Problem Statement

SME staff responding to customer ESG questionnaires must interpret varied questions, locate relevant guidance and determine whether their records support the requested answers. ESGReady will connect questions, selected SEDG disclosures and company evidence, identify specific gaps and prepare traceable drafts. It checks the sufficiency of supplied evidence; it cannot establish that a record is authentic or that a company complies with every applicable requirement.

## Evidence of the Problem

- The [OECD CMM case study](https://www.oecd.org/en/publications/scaling-up-public-financial-and-non-financial-support-for-sme-sustainability_4b79ddf3-en/capital-markets-malaysia-simplified-esg-disclosure-guide-for-smes-in-supply-chains_250ebf4a-en.html) describes varied supply-chain sustainability data requests and challenges faced by SMEs.
- [Capital Markets Malaysia’s SEDG](https://sedg.capitalmarketsmalaysia.com/) provides a structured disclosure reference and reporting template for this context. Its existence does not prove demand for ESGReady or a particular rate of evidence errors.

## Initial Related Work / Existing Approaches

| Approach | Existing capability | Limitation / implication for this project |
|---|---|---|
| [CMM SEDG guide and template](https://sedg.capitalmarketsmalaysia.com/) | Standardised manual disclosure guidance | A reference for the workflow, not evidence that the proposed AI checker is effective |
| [Sunhat compliance readiness check](https://www.getsunhat.com/use-cases/compliance-readiness-check) | Vendor-described assessment of customer requirements against company records, with cited gaps/conflicts | Evidence checking already exists; internal performance and SEDG coverage have not been tested here |
| [DitchCarbon AI Survey Responder](https://ditchcarbon.com/survey-responder) | Vendor-described reuse of company data for questionnaire completion and review | Drafting/reuse alone are insufficient differentiation; no claim that it lacks Malaysian support or evidence validation |

These are source-based descriptions, not hands-on product tests.

## Engineering Gap / Limitation

The practical task is to build and evaluate a small, reproducible workflow that links each supported question to criteria and evidence, exposes missing information, and reduces unsupported drafting without excessive refusal. Market uniqueness and superiority over commercial tools have not been established.

## Project Objectives

**O1:** To design a bounded questionnaire-review workflow that links supported questions to selected SEDG disclosures and company evidence, with explicit scope, source provenance and human review.

**O2:** To develop a prototype that identifies missing support, incomplete coverage and period/entity mismatches, and produces cited draft answers or requests for missing information.

**O3:** To evaluate mapping accuracy, evidence-checking performance, answer grounding, safe abstention and operational usability against a basic retrieval-and-drafting baseline using a documented held-out benchmark.

## Target Users

Owners and finance, administration or operations staff in Malaysian manufacturing SMEs. The course prototype will use English questions and fictional company records. Peer testing does not constitute validation by actual SME staff.

## Data Sources

- **K1 — Disclosure guidance:** [SEDG Version 2, July 2025](https://sedg.capitalmarketsmalaysia.com/wp-content/uploads/2025/07/SEDG-v2.pdf). Eight selected disclosure IDs define the V1 catalogue.
- **K2 — Background context:** [SC NSRF FAQ, issued 14 January 2026](https://www.sc.com.my/api/documentms/download.ashx?id=2efe731e-20cf-4710-8104-d07762a4637b). Selected explanatory sections only; no individual legal-applicability decision or deadlines.
- **K3 — Background context:** [OECD CMM case study](https://www.oecd.org/en/publications/scaling-up-public-financial-and-non-financial-support-for-sme-sustainability_4b79ddf3-en/capital-markets-malaysia-simplified-esg-disclosure-guide-for-smes-in-supply-chains_250ebf4a-en.html). Explains the supply-chain questionnaire context.
- **Company evidence:** planned, student-authored synthetic manufacturing-SME records, with company/period/site metadata. Guidance is not proof of company activity.

See the [source register](docs/source_register.md) for source roles, versions and verification boundaries. Reference PDFs are linked rather than redistributed in this package; public access does not by itself establish permission to republish them.

## Proposed AI Approach

A pretrained language model will interpret differently worded questions, map them to selected disclosures, compare requested information with relevant evidence, and explain gaps in plain language. Deterministic checks will enforce dates/entity metadata, output schemas, source locations and review state. These checks support the semantic AI assessment; they do not replace it. One orchestrated application is sufficient; model training, a dedicated NLI model and multiple agents are not required.

The evaluated issue families are **missing support**, **incomplete coverage** and **period/entity mismatch**. Missing metadata triggers a request for information. Absence of an incident record is not evidence of zero incidents. Evidence that is merely old is not automatically invalid.

## V1 Scope and Expected Outcomes

English; manufacturing examples; eight selected SEDG disclosure IDs; up to 10 questions, 10 text-PDF/CSV evidence files, 10 MB per file and 100 evidence PDF pages per session. Output: mapped disclosure, evidence references, issue flags, missing information, cited draft, assessment status and separate human-review state.

Expected later deliverables are a working demonstrator, labelled synthetic benchmark, fair baseline comparison and a report of measured outcomes and failures. Emissions calculation/factor registries, comprehensive contradiction detection, OCR, production deployment and automatic submissions are excluded from V1. These are deliberate scope choices, not claims that those features already work.

## Weekly Progress

| Week | Focus | Deliverable | Status |
|---|---|---|---|
| W1 | Group observation and individual project framing | README + ESGReady scope | Project documents revised; original group evidence and remote submission not verified |
| W2 | Requirements, evaluation and architecture | Four required planning files | All four core planning files are present |
| W3 | Document preparation (C0 → D1) | Executed notebook, observed inventory, K1 prepared text and manifest | 26 paragraph-aware chunks across eight physical pages. The saved repeatability check passed. |
| W4 | Data quality and responsible data | Notebook, report, two clean corpora, flags, duplicate ledger and chart | 8/8 selected K1 entries verified. GO WITH CONDITIONS for private use of this pinned guidance. |
| W5 onward | Model selection, implementation and evaluation | Later application and benchmark evidence | Planned. |

## Submission index

| Lab | Files in this repository | Other assessment material |
|---|---|---|
| 1 · Project scope | [Individual scope](docs/week1_project_scope.md) and this README | Original group observation sheet and map belong at `docs/week1_observation_sheet.md` and `docs/week1_system_map.png`. Both are outstanding in this package. |
| 2 · Requirements and design | [Requirements](docs/week2_requirements.md), [evaluation criteria](docs/week2_evaluation_criteria.md), [architecture PNG](docs/week2_architecture_v1.png), [decisions and traceability](docs/week2_architecture_decisions.md) | [Editable architecture](docs/week2_architecture_v1.drawio) and [source register](docs/source_register.md) support these deliverables. |
| 3 · Data pipeline | [Executed notebook with source previews omitted](notebooks/week3_pipeline.ipynb), [inventory](docs/week3_data_inventory.md), [pipeline diagram](docs/week3_pipeline_diagram.png), [decisions](docs/week3_pipeline_decisions.md), [Part B manifest](data/week3_manifest.json), [Part C manifest](data/pipeline_v1/text/pipeline_manifest.json) | The two 26-record JSONL exports and original executed notebook are in the private assessment files. |
| 4 · Data quality and governance | [Quality notebook](notebooks/week4_quality.ipynb), [quality report](docs/week4_data_quality_report.md), [validation findings](docs/week4_validation_failures.csv), [duplicate review](docs/week4_duplicate_review.csv), [coverage plot](docs/week4_coverage_by_source.png) | The two required cleaned data files are in the private assessment files. The [source-disposition ledger](docs/week4_source_dispositions.csv) accounts for all 26 input chunks. |

## Data access and later use

The private supplement is named `ESGReady_private_assessment.zip`. Its files use the same repository-relative paths. The [data inventory and access instructions](data/README.md) list each location. Provide the supplement to the lecturer through the authorised course channel.

For Topic 7 (Week 9), use `data/prepared_chunks_clean.jsonl` or `data/chunks_clean.pkl` as the D1 guidance input. Each contains the same eight reviewed passages. Record the edition check from the [quality report](docs/week4_data_quality_report.md) before indexing.
