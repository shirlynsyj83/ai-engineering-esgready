# Source Register — ESGReady

Checked: 5 November 2026. External sources support domain statements; the prototype scope, evaluation design and thresholds are project decisions. Web review is not hands-on product testing. No test performance or customer interviews are claimed.

## Knowledge documents used by the proposed application

These three public documents have explicit roles in the explanation component. Only K1 supplies the selected disclosure criteria. K2 and K3 support bounded background explanations and must never be used as evidence of a company's activities.

| ID | Document / publisher | Version or date | Relevant location | Runtime role and example |
| --- | --- | --- | --- | --- |
| K1 | Simplified ESG Disclosure Guide for SMEs in Supply Chains, Capital Markets Malaysia | Version 2, July 2025 | Printed pp. 3–5, 11–15 and selected disclosure pages listed in `week2_requirements.md` | Explain the mapped disclosure and cite its source; example: explain which reporting fields a question concerns. |
| K2 | Frequently Asked Questions on the National Sustainability Reporting Framework, Securities Commission Malaysia | Issued 14 January 2026 | Q1.2 and Q2.1–2.2, printed pp. 1 and 4 | Explain reporting context and the distinction between covered entities and other businesses; do not determine an individual firm's legal obligations or provide reporting deadlines. |
| K3 | Capital Markets Malaysia – Simplified ESG Disclosure Guide for SMEs in Supply Chains, OECD | 5 November 2025; HTML case study | “Key characteristics” and “Design and implementation lessons learned” | Explain why buyers may ask different questions and why a request can exceed the guide's coverage. Treat its historical framework descriptions as context, not the current disclosure catalogue. |

### Exact access links

- **K1:** https://sedg.capitalmarketsmalaysia.com/wp-content/uploads/2025/07/SEDG-v2.pdf
- **K1 official landing page:** https://sedg.capitalmarketsmalaysia.com/
- **K2:** https://www.sc.com.my/api/documentms/download.ashx?id=2efe731e-20cf-4710-8104-d07762a4637b
- **K2 official index:** https://www.sc.com.my/nsrf/resources/policy-documents
- **K3:** https://www.oecd.org/en/publications/scaling-up-public-financial-and-non-financial-support-for-sme-sustainability_4b79ddf3-en/capital-markets-malaysia-simplified-esg-disclosure-guide-for-smes-in-supply-chains_250ebf4a-en.html

## Evidence and related-work sources

| ID | Source and link | Supported observation | Limit of evidence |
| --- | --- | --- | --- |
| E1 | K3, OECD case study | SMEs face varied supply-chain sustainability data requests; some requests extend beyond the guide. | Does not measure ESGReady demand, evidence-error prevalence or willingness to pay. |
| E2 | K1, overview and instructions | A standardised disclosure reference and reporting template exist for this workflow. | Does not demonstrate that the proposed AI checker improves outcomes. |
| R1 | CMM guide and template, K1 landing page | An established manual, document-led approach. | A guide is not an evaluated competing AI system. |
| R2 | Sunhat, Customer Compliance / Compliance Readiness Check: https://www.getsunhat.com/use-cases/compliance-readiness-check | Vendor describes checking customer requirements against company documents and returning cited gaps/conflicts. | No account-based testing; accuracy, SEDG coverage and pricing are not established here. |
| R3 | DitchCarbon, AI Survey Responder: https://ditchcarbon.com/survey-responder | Vendor describes reusing company data to complete sustainability questionnaires with human review. | No account-based testing; no claim that it lacks evidence validation or Malaysian support. |

R2 and R3 are undated product pages, accessed 5 November 2026. Use these pages for related work only, not for validating SME disclosures.

## Source handling rules for implementation

1. Record document ID, publisher, exact URL, title, version/date, access date, file checksum and page/section for each ingested reference. Checksums are generated after downloading; none are fabricated here.
2. Freeze the reference snapshots for evaluation. A source change requires a new corpus version and regression checks.
3. Preserve printed page numbers and physical PDF page indices as separate fields. For K1, printed p. 25 corresponds to physical PDF page 26; do not assume all documents use that offset.
4. Tag source purpose as `disclosure_guidance`, `background_context` or `company_evidence`. Context cannot override the pinned disclosure catalogue or establish company facts.
5. Each customer-specific condition is separately tagged `customer_question`. Each prototype rule is tagged `project_rule`, not represented as wording prescribed by SEDG.
6. Public accessibility is not permission to redistribute. Keep downloaded third-party PDFs in a local/private reference folder unless redistribution is permitted. Commit source links and the student's own synthetic records. Follow the lecturer's instructions for any required private submission of PDFs.

## Known boundaries

The source review supports the disclosure-support problem, but not the prevalence of specific evidence defects or a claim that ESGReady is commercially superior. Those are hypotheses to investigate. The project does not reproduce full standards, proprietary questionnaires or vendor software.


## Assignment and revision references

The uploaded ESGReady proposal (`week1_project_scope(8).md`) is the project reference. The Topic 1 Lab brief supplies the original README/Part C requirements; the supplied Topic 2 Lab brief supplies Parts A–C, reflections, four required filenames, GitHub checkpoints and Week 3 preparation. The earlier MeterInsight delivery was based on the wrong project and is superseded by this ESGReady package.

Rechecked on 5 November 2026: the official K1 PDF/version, K2 FAQ issue date and selected context, K3 problem context, and R2/R3 vendor descriptions. The review supports these bounded descriptions; it does not validate the proposed implementation, establish evidence-defect prevalence or prove a competitive advantage. K2's publicly accessible PDF carries a “Restricted (Terhad)” footer; public hosting is not treated as permission to redistribute it.


K1 source review: downloaded 5 November 2026, 82 pages, SHA-256 `c7699997922c6735ceb1ae494eb2511841c66bd03a228807ae15eba3730ace19`. All eight selected disclosure/page pairs were checked; physical page 26 was visually inspected. K2 was accessible to the public PDF reader, but separate local download failed; no local-file checksum is claimed for K2.
