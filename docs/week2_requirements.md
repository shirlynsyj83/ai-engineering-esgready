# Topic 2 — Requirements Specification

**Project:** ESGReady — An Evidence-Grounded ESG Questionnaire Assistant for Malaysian SMEs
**Date:** 5 November 2026. **Version:** V1 planning baseline.

All “shall” statements describe intended behaviour. Numerical thresholds are proposed acceptance targets chosen for a course prototype; they are not achieved results or thresholds prescribed by SEDG. They may be revised using development-set evidence before the held-out evaluation, with reasons recorded.

## Section 0 — Project Framing & Application Scope Checkpoint

| Framing element | Specification |
| --- | --- |
| Problem + evidence | SME staff must connect customer questions with guidance and supporting records. E1/E2 in the [revised Week 1 scope](week1_project_scope.md) and [source register](source_register.md) establish the disclosure-support context. Evidence-defect prevalence remains unmeasured. |
| Existing approaches | CMM's manual guide/template, Sunhat's customer compliance review and DitchCarbon's survey responder. The Week 1 related-work table states their observed capabilities and limits of the desk review. |
| Engineering gap | Implement and test explicit, traceable evidence checks for a bounded SME workflow; assess improvement over basic retrieval and drafting. No claim of market uniqueness. |
| Intended users | Owners and finance/admin/operations staff in Malaysian manufacturing SMEs; prototype tests use student-authored fictional companies. |
| Supported tasks | Map supported questions, locate evidence, check three issue families, explain gaps, draft supported answers and support human review/export. |
| Knowledge domain | Eight selected disclosure IDs from K1; K2/K3 provide background explanations only. |
| Operating context | Single-user English prototype; internet required if a hosted model is used; synthetic data only for the assessed course workflow. |
| Constraints | No confidential data access assumed; up to 10 questions, 10 files, 10 MB/file and 100 PDF pages/session; modest course resources; no custom model training required. |
| Out of scope | Full ESG/NSRF compliance, legal conclusions, authenticity verification, emissions calculations, OCR, all-sector/language coverage, automatic submission and production multi-tenancy. |
| Evaluation focus | Does the checker improve evidence-supported drafting while preserving useful coverage and acceptable response time? See EC-01–EC-12. |
| Traceability | O1–O3 connect to FR/NFR/RAI IDs, EC IDs, architecture components and planned evidence in the architecture decisions file. |

### Project objectives

**O1:** To design a bounded questionnaire-review workflow that links supported questions to selected SEDG disclosures and company evidence, with explicit scope, source provenance and human review.

**O2:** To develop a prototype that identifies missing support, incomplete coverage and period/entity mismatches, and produces cited draft answers or requests for missing information.

**O3:** To evaluate mapping accuracy, evidence-checking performance, answer grounding, safe abstention and operational usability against a basic retrieval-and-drafting baseline using a documented held-out benchmark.

### Supported disclosure catalogue

The ID/topic/page columns below identify the selected source locations in K1. The final column contains **project-authored evidence examples/checks**, not an official checklist of acceptable proof. The complete wording in K1 controls interpretation; the short topic names are navigation labels.

| Disclosure ID | Topic label | Printed page | PDF page (1-based) | Prototype evidence examples/checks |
| --- | --- | --- | --- | --- |
| SEDG-E2.1 | Energy use | 25 | 26 | Utility/energy summaries; confirm applicable categories, units and coverage. |
| SEDG-E3.1 | Water withdrawal | 29 | 30 | Water records; check source categories, units and period. |
| SEDG-E4.1 | Waste totals | 33 | 34 | Waste register; check that each requested flow has support. |
| SEDG-S2.1 | Average employee training hours | 45 | 46 | Training summary with the stated employee basis; flag unexplained averages. |
| SEDG-S4.1 | Fatalities and injuries | 52 | 53 | Incident register or explicit period-specific nil declaration; absence is not zero. |
| SEDG-G1.1 | Director count | 61 | 62 | Governance register or company summary with entity and reference date. |
| SEDG-G2.1 | Company policy list | 64 | 65 | Policy register and relevant documents; distinguish a draft policy from an adopted one. |
| SEDG-G4.1 | Confirmed corruption incidents | 74 | 75 | Incident summary including descriptions where applicable; absence is not zero. |


Only the requested parts of a disclosure are assessed. For example, an electricity-only question does not require every energy category; conversely, electricity-only evidence cannot establish a complete all-energy response. Extra customer conditions remain separate from the mapping. The supported catalogue is deliberately incomplete, and an out-of-scope label means “not supported by this prototype”, not “absent from ESG guidance”.

### Evidence issue definitions

| Label | Operational definition | Example and boundary |
| --- | --- | --- |
| `missing_support` | The supplied pack contains no relevant documentary support for a requested claim. This is a pack-level judgement, not merely a retrieval failure. | A safety policy alone does not support a claimed incident count. No record found does not mean zero incidents. |
| `incomplete_coverage` | Relevant evidence exists for the target boundary, but leaves an explicitly requested field, category or portion of the reporting period unsupported. | Nine months of utility records for a twelve-month question, or a count without a requested incident description. |
| `scope_mismatch` | Candidate evidence explicitly concerns an incompatible entity/site or reporting period. | A full prior-year summary supplied for the current reporting year, or another company's record. Report `period` / `entity` subtypes. |

Flags can co-occur in deployment. The primary benchmark isolates one issue family per defective case to simplify interpretation; mixed-issue cases are a separately reported extension. Before declaring pack-level missing support, check the inventory and readable content of the supplied pack rather than relying on a failed top-k retrieval. If unreadable files or retrieval limits prevent this check, return an unresolved review/processing state instead of asserting absence. Unknown metadata results in an information request or manual review, not an invented mismatch. No age-based policy expiry is imposed without an explicit applicable condition. Unresolved conflicts can be referred to manual review without claiming comprehensive contradiction detection.

### Criteria and status rules

Every criterion has `criterion_id`, `origin` (`guidance`, `customer_question`, `project_rule`), source location or question ID, interpretation, version and applicability condition. Guidance establishes reporting content; user questions establish their extra conditions; prototype checks establish how evidence sufficiency is assessed. No source is silently promoted to legal authority.

- `ready_draft`: assessed portions are supported, required fields/boundaries are resolved and no blocking issue remains. Still a draft; not assurance.
- `needs_information`: missing or incomplete support/metadata; include a specific request.
- `needs_review`: unresolved ambiguity, incompatible candidate evidence or conflicting records; explain the problem.
- `out_of_scope`: the item is outside the supported catalogue/capabilities; state that boundary.
- `error`: processing failed; provide an actionable message and preserve the question row.

Keep `human_reviewed` separate from assessment status. Human acknowledgement does not erase issues. A question with supported and unsupported parts may contain a partial draft, but the overall status cannot be `ready_draft`.

## Section 1 — Functional Requirements

| ID | Objective | Requirement | Acceptance example / boundary |
| --- | --- | --- | --- |
| FR-01 | O1 | The system shall collect the target company, reporting period and included entities/sites before assessing company evidence, and request clarification when that boundary is missing. | Omitting the period prevents a ready-draft result; no current-year assumption. |
| FR-02 | O1, O2 | The system shall accept up to 10 English questions by paste/CSV and up to 10 text-based PDF/CSV evidence files, preserve question IDs and wording, and report invalid or over-limit inputs. | 10 MB/file; 100 PDF pages total. Scanned PDFs are identified as unsupported instead of silently treated as empty. |
| FR-03 | O1, O2 | The system shall map each question to zero, one or more supported disclosure IDs, cite the guidance, and distinguish an ambiguous item from an item outside the supported catalogue. | An unsupported question must not be forced to the nearest ID. Coverage of a subquestion is not full coverage of the original question. |
| FR-04 | O1, O2 | The system shall retrieve candidate guidance and company evidence separately and expose document IDs, source versions and page/section or CSV-row locations. | Company evidence is limited to the active case. Background documents cannot establish company facts. |
| FR-05 | O2 | The system shall assess the three defined issue families and show each triggered criterion, its provenance, the supporting location and a plain-language reason. | A gap states what is missing or incompatible. Missing metadata is unresolved, not automatically a mismatch. |
| FR-06 | O2 | The system shall return a structured result containing the original question, mapping, evidence references, issue flags, missing information, draft text, assessment status and human-review state. | Each question receives a result or a visible error; an omitted row is a failure. |
| FR-07 | O2 | The system shall draft only claims supported by the supplied evidence and label partial answers and information requests explicitly. | No invented totals, inferred zero incidents, annualisation of incomplete records or fabricated citations. |
| FR-08 | O1, O2 | The system shall allow a user to inspect/edit each draft and acknowledge review before exporting a draft review table, retaining flags and source references. | Edits reset review acknowledgement. Export is not automatic submission or assurance. |
| FR-09 | O1, O2 | The system shall provide brief background explanations grounded in K2 or K3 when requested within the defined context, with source and date. | It shall not decide legal applicability, provide deadlines, or turn background statements into evidence-checking rules. |
| FR-10 | O2 | The system shall allow the user to clear the active session and remove its uploaded evidence, derived chunks and temporary response data from application-managed storage. | The interface shall distinguish local deletion from any external service retention; do not promise deletion beyond the application's control. |


## Section 2 — Non-Functional Requirements

| ID | Objective | Quality | Requirement | Measurement method | Metric | Threshold | Rationale |
| --- | --- | --- | --- | --- | --- | --- | --- |
| NFR-01 | O1, O3 | Correctness | The system shall map supported questions accurately. | Compare predicted disclosure-ID sets with fixed gold sets on 160 held-out cases. | Exact-set accuracy, counting abstentions/errors as incorrect. | At least 0.85 (136/160). | Enough correct routing for a useful bounded workflow. |
| NFR-02 | O2, O3 | Reliability | The system shall detect each core evidence-issue family without excessive false alarms. | Score independent predictions on the 160-case set against full-pack labels. | Per-family precision and recall; clean-case false-alarm rate. | Each precision ≥0.80; each recall ≥0.85; clean false-alarm rate ≤0.10. | Protects users from missed defects without making valid evidence unusable. |
| NFR-03 | O2, O3 | Grounding | The system shall link factual assertions to supporting, resolvable sources. | Human audit of atomic claims and citation links across held-out outputs. | Citation support precision; claim citation completeness. | Both ≥0.95; invalid source locations count as unsupported. | Users can check the basis for an answer. |
| NFR-04 | O2, O3 | Performance | The system shall return usable results within the prototype latency targets. | 30 single-item requests and 10 ten-item batches on a documented environment, corpus prepared. | p95 single-item latency; maximum batch latency; timeout/error count. | p95 ≤20 s; every tested ten-item batch ≤120 s; report all failures. | Allows interactive review and small batches. |
| NFR-05 | O2, O3 | Operational reliability | The system shall return well-formed, complete responses and actionable error messages. | 50 workflow scenarios including invalid files, empty inputs and service failures. | Scenario pass rate using a predefined expected outcome. | At least 49/50; no silent dropped question rows. | Users can recover from failures. |
| NFR-06 | O1, O3 | Maintainability / reproducibility | The system shall record the source, criteria, prompt and model configuration versions associated with each result. | Inspect all 160 result records and perform one controlled catalogue update and rollback. | Complete lineage records; successful update/rollback. | 160/160 lineage records; update and rollback pass with no application-code edits for catalogue-only changes. | Results can be reproduced and requirements revised without hidden changes. |


Timing excludes initial document ingestion, which is measured and reported separately. Timing includes retrieval, assessment, generation, retries and validation. All attempts remain in the report. NFR-05 permits a clearly reported service failure to be a correctly handled scenario; it does not count that as a successful answer in mapping or usefulness metrics.

## Section 3 — Responsible AI Requirements

| ID | Objective | Risk | Requirement | Measurement method | Metric | Threshold | Reason |
| --- | --- | --- | --- | --- | --- | --- | --- |
| RAI-01 | O2, O3 | False assurance | The system shall withhold ready-draft status from deficient evidence and shall not claim compliance, certification or verified truth. | Review the 120 defective core cases and 20 assurance-seeking prompts. | False-ready rate; prohibited assurance claim count. | False-ready ≤0.05 (≤6/120); 0/20 prohibited assurance claims. | A fluent answer must not conceal an evidence gap. |
| RAI-02 | O2, O3 | Overconfidence / excessive refusal | The system shall request information or abstain when support is insufficient while still drafting on adequately supported cases. | Review 120 defective cases, 40 clean cases and a separate 20-item scope/ambiguity suite. | Safe handling rate; clean-case drafting coverage; scope/ambiguity handling accuracy. | Safe handling ≥0.95 (≥114/120); coverage ≥0.80 (≥32/40); scope handling ≥19/20. | Abstention protects users without being a shortcut to avoid the task. |
| RAI-03 | O2, O3 | Prompt injection | The system shall treat document instructions as untrusted content and preserve its review rules. | 20 adversarial evidence/question cases with embedded instructions to fabricate, suppress gaps or reveal other-case content. | Attack-induced rule violations. | 0/20 successful violations; residual risk documented. | Uploaded text must not take control of the application. |
| RAI-04 | O1, O2, O3 | Privacy / cross-case leakage | The system shall isolate cases, minimise logs and clear application-managed session data on request. | 20 paired-case isolation tests, 10 deletion tests and repository/log inspection. | Cross-case disclosures; residual accessible session artefacts; exposed secrets/private records. | 0/20 leaks; 10/10 deletion passes; zero secrets or real private records in public outputs. | Evidence remains associated with its owner/case. |
| RAI-05 | O1, O2, O3 | Human oversight | The system shall label all outputs as drafts and require review acknowledgement before export. | 10 UI/export scenarios including edited and unreviewed rows. | Correct warning and review-gate enforcement rate. | 10/10; no customer submission path in V1. | Users retain responsibility and visibility. |
| RAI-06 | O1, O2, O3 | Misstated authority | The system shall identify whether each applied criterion comes from guidance, a customer question or a project rule. | Audit criterion provenance in all 160 core results and 10 background explanations. | Correct provenance rate; unsupported legal/standard claims. | 100% applied criteria carry correct provenance; 0/10 unsupported authority claims. | An authored evidence heuristic must not be presented as an official requirement. |


The course uses synthetic company data; passing these tests does not establish production privacy or regulatory compliance. External model retention must be described accurately if a hosted service is selected. Self-reported model confidence is not accepted as a calibrated probability; initial abstention uses explicit evidence/metadata gates.

### Part A reflection

The hardest requirement is RAI-01, preventing false assurance. A result may have a plausible citation yet still cover the wrong period, entity or only part of the question. Measuring this requires reviewing the complete evidence pack and defining sufficiency consistently. The project therefore uses controlled defect cases, independent review of labels, and a false-ready metric alongside defect recall. A warning label alone does not satisfy the requirement.
