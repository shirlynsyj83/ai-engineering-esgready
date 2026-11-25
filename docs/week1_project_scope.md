# Week 1 Project Scope — ESGReady (Revised)

**Project:** ESGReady — An Evidence-Grounded ESG Questionnaire Assistant for Malaysian SMEs
**Domain:** Sustainability disclosure support for Malaysian manufacturing SMEs.
**Revision date:** 5 November 2026.
**Status:** Planning specification; implementation and evaluation have not yet been conducted.

## Problem statement

An SME employee responding to a customer's ESG questionnaire must interpret the question, locate relevant guidance, find supporting company records and decide whether those records cover the requested information. A fluent draft may still rely on the wrong entity, a different reporting period or only part of the required evidence. ESGReady will assist this review and show the basis for each proposed answer, allowing the user to identify missing information before using a draft.

The intended workflow needs language interpretation and document retrieval, combined with explicit checks on fields and metadata. Whether this combination performs better than basic retrieval and drafting is an evaluation question, not an assumed result. Evidence checking is limited to the supplied records; it does not establish whether those records are true in the real world.

## Evidence of the problem

- **E1 — OECD:** Its CMM case study describes varied supply-chain requests and difficulties responding to them. This supports the need for a bounded disclosure-support workflow. See K3 in [source register](source_register.md).
- **E2 — CMM:** Its disclosure guide and reporting template provide an established reference for preparing responses. See K1 in the source register.

These sources do not quantify unsupported-answer rates or prove product-market demand. Such claims are excluded. The previous unverified newspaper statistics and broad regulatory deadline claim have been removed.

## Initial related work / existing approaches

| Approach | What it already offers | Implication for this project |
| --- | --- | --- |
| CMM SEDG guide and disclosure template [R1] | A structured manual reference. | Retain the official reference and compare AI outputs with explicitly labelled criteria. |
| Sunhat customer compliance review [R2] | Vendor-described document assessment and source-linked gaps. | Evidence checking is an existing capability; ESGReady cannot claim to invent it. |
| DitchCarbon AI Survey Responder [R3] | Vendor-described questionnaire completion using existing company data. | Reusing data and drafting answers alone are insufficient differentiation. |

References and access dates are in [source_register.md](source_register.md). These are desk-review findings, not hands-on vendor evaluations. There is no evidence here that the products lack SEDG support, nor that ESGReady will outperform them.

## Project / engineering gap

For the selected SME workflow, the engineering task is to connect each supported question, disclosure reference and company record to an explicit evidence assessment, then test whether those checks reduce unsupported drafting without excessive abstention. The contribution is a reproducible, narrowly scoped prototype and an openly described benchmark with source-linked error analysis. It is a practical engineering gap; no scientific novelty or absence of market alternatives is claimed.

## Project objectives

**O1:** To design a bounded questionnaire-review workflow that links supported questions to selected SEDG disclosures and company evidence, with explicit scope, source provenance and human review.

**O2:** To develop a prototype that identifies missing support, incomplete coverage and period/entity mismatches, and produces cited draft answers or requests for missing information.

**O3:** To evaluate mapping accuracy, evidence-checking performance, answer grounding, safe abstention and operational usability against a basic retrieval-and-drafting baseline using a documented held-out benchmark.

## Intended users and operating context

Primary users are owners and finance, administration or operations staff in Malaysian manufacturing SMEs. The course prototype uses a single-user review session with fictional company records and English questions. Procurement and sustainability practitioners may review future demonstrations; their participation is not assumed or claimed.

## Supported tasks and boundaries

- Accept pasted questions or a CSV containing up to 10 items and a declared company, reporting period and entity/site boundary.
- Accept up to 10 text-based PDF or CSV evidence files per session, at most 10 MB each and 100 PDF pages in total.
- Map questions to the eight disclosure IDs listed in the Week 2 requirements, or state that an item is ambiguous or outside the supported catalogue.
- Retrieve guidance and evidence separately; preserve document identity and page/row references.
- Assess three issue families: missing support, incomplete coverage and period/entity mismatch.
- Present cited draft answers, evidence gaps and clarification requests, with human review before export.
- Provide brief source-grounded background explanations from K2 and K3 where relevant; do not add their content to the evidence criteria.

## Data sources

- **K1:** [SEDG Version 2](https://sedg.capitalmarketsmalaysia.com/wp-content/uploads/2025/07/SEDG-v2.pdf), disclosure guidance.
- **K2:** [NSRF FAQ, 14 January 2026](https://www.sc.com.my/api/documentms/download.ashx?id=2efe731e-20cf-4710-8104-d07762a4637b), background context.
- **K3:** [OECD CMM case study](https://www.oecd.org/en/publications/scaling-up-public-financial-and-non-financial-support-for-sme-sustainability_4b79ddf3-en/capital-markets-malaysia-simplified-esg-disclosure-guide-for-smes-in-supply-chains_250ebf4a-en.html), background context.

The application uses the three public knowledge documents K1–K3 registered in [source_register.md](source_register.md). The disclosure catalogue is pinned to K1. Company evidence consists of authored fictional manufacturing-SME packs containing utility summaries, training records, incident registers, governance summaries and policies. Each record is labelled synthetic and assigned a company/session ID.

Public corporate reports may later form a separate exploratory challenge set. They must remain attached to their actual entity and must never be presented as evidence for a fictional SME. They are not required for the primary benchmark and are not included in the current package.

## Similar to EduAdvisor

Both use approved document sources, cited responses, explicit scope controls and later evaluation of usefulness and reliability.

## Different from EduAdvisor

ESGReady handles a short questionnaire and an evidence pack, keeps guidance separate from company records, flags evidence gaps, and returns a structured review table. It evaluates defect detection and the risk of marking unsupported responses as ready for review.

## Responsible AI risks

| Risk | Planned control |
| --- | --- |
| Unsupported company claims | Evidence citations, explicit gaps and withholding unsupported assertions. |
| False assurance | “Draft for human review” label; no compliance/certification claims; measure false-ready rate. |
| Wrong entity or period | Explicit metadata, session isolation and boundary checks. |
| Instructions hidden in evidence | Treat retrieved text as untrusted data; constrain outputs and test malicious documents. |
| Confidentiality | Synthetic inputs for the course, no real personal records, no secrets or evidence text in public logs. |
| Misleading evaluation | Held-out company packs, valid negative examples, independent label review and results reported with denominators. |

## Scope exclusions and stretch goals

**Excluded from V1:** all-sector/all-language coverage; full-standard compliance assessment; legal advice; authenticity verification; scanned-document OCR; proprietary questionnaires; autonomous submission; emissions calculations and factor registries; multi-user production deployment; comprehensive contradiction detection.

**Stretch goals only after core evaluation:** evidence reuse across questionnaires, a limited contradiction check, and a separately specified deterministic calculation module. None is required to pass the V1 evaluation.

## Proposed AI approach and expected outcomes

A pretrained language model will interpret questions and assess whether supplied passages support the requested information. Deterministic metadata/schema checks will constrain the result. Separate retrieval provides context for this semantic assessment; the task is not solely finding documents. Candidate model/provider choices remain open, and no large model needs training.

The expected later outcomes are a demonstrator, a documented synthetic benchmark and a baseline comparison that reports failures as well as successes. The current deliverables are the Lab 1 project documents and Topic 2 plan; the application and benchmark are not implemented.

## Evaluation focus

Can explicit evidence checks help produce supported, traceable drafts and actionable information requests, compared with the same retrieval-and-drafting workflow without the checker? The evaluation plan specifies a 160-case held-out synthetic test set plus separate safety and usability checks. These are planned datasets, not completed experiments. See [week2_evaluation_criteria.md](week2_evaluation_criteria.md).

## Constraints and feasibility

The project assumes an undergraduate course timeline, no confidential customer data, a modest model-service budget and no model training requirement. The implementation should begin with one orchestrated workflow and a small versioned criteria catalogue; specific frameworks and model choices remain open. English/manufacturing-only coverage limits generalisability. A peer usability check cannot establish adoption by real SMEs.

## Changes from the earlier draft

The revision narrows the domain and disclosure coverage, replaces the evidence-validation title, acknowledges competing evidence-checking products, separates background context from disclosure criteria, removes mandatory emissions tooling, simplifies the objectives and strengthens the evaluation plan.
