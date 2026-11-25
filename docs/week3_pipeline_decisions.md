# ESGReady — Topic 3 V1 Pipeline Decisions, Contracts and Traceability

**Execution record.** The saved Colab run on 12 November 2026 processed eight physical pages from K1 into 26 disclosure-guidance records. Both run manifests are included in this repository. The two prepared outputs are in the private assessment supplement. The final section distinguishes the original run from the later layout review.

## Relationship to the existing project

- **Project:** ESGReady — An Evidence-Grounded ESG Questionnaire Assistant for Malaysian SMEs.
- **Objective:** O1 (source-grounded workflow) and O3 (reproducible evidence), with future support for O2.
- **Requirement IDs:** FR-03 (selected SEDG disclosure mapping); FR-04 (traceable source locations and separated evidence roles); NFR-03 (grounding); NFR-06 (version/reproducibility); RAI-06 (authority/provenance). FR-02 applies when future user evidence ingestion is implemented.
- **Architecture link:** Lab 2 **C0** prepares guidance for **D1**. It does not implement C3 mapping, C4 evidence assessment, C5 model drafting or D2 company-case records.

## Data selection and inspection

The project used PDF Pathway A with Capital Markets Malaysia’s SEDG Version 2 (July 2025). The source register designates K1 as disclosure guidance for D1. The input was an 82-page PDF of 1,928,183 bytes. The notebook selected physical pages 26, 30, 34, 46, 53, 62, 65 and 75. The initial inspection extracted 1,114 characters on page 26 and 1,123 on page 30. K2, K3 and D2 company evidence were outside this run.

## Preparation decision and evidence

| Observation | Fixed-size method | Paragraph-aware method |
|---|---|---|
| Configuration | Split each physical page into segments of up to 500 characters. | Keep extracted paragraphs together where they fit, with a 500-character limit. Split longer paragraphs within the same page. |
| Output count on the same eight pages | 25 chunks | 26 chunks |
| First energy-page preview | The preview included merged column headings followed by E2.2. | The same leading text appeared, including E2.2 before the Basic E2.1 criterion. |

**Decision.** The pipeline used the paragraph-aware method to retain available paragraph boundaries and physical page references. The count difference establishes that the methods segmented the text differently. Semantic quality was assessed separately through the later source-layout review. Each chunk retained its own ID, source role, version, source hash, physical page and a candidate disclosure ID for navigation.

**Outputs.** The 26-record JSONL is 24,313 bytes. Part B and Part C record the same prepared SHA-256. The copy placed at the Part C path was restored from the supplied JSONL after verifying its bytes against the original Part C manifest.

| Item | SHA-256 |
|---|---|
| K1 PDF recorded by the run | `c7699997922c6735ceb1ae494eb2511841c66bd03a228807ae15eba3730ace19` |
| Prepared JSONL verified in both output folders | `45f826424139dd72dbe2efa8f5de2505b88e7a31e33c53dbb642ec28ae5e7680` |

## ETL / ELT and batch / streaming

- **ETL:** Extract PDF text, transform/segment it with page metadata, then load prepared JSONL into local storage. The original raw PDF remains unchanged.
- **Batch:** the pinned public guidance is a versioned, infrequently updated reference. Live streaming is unnecessary for Topic 3 and would complicate reproducibility. A source update requires intentional re-ingestion and regression review.
- **Repeatability:** run the same source and configuration twice; compare raw and prepared SHA-256 fingerprints, record counts and source-to-output mapping. Execution timestamps are allowed to differ.

## Stage contracts and failure responses

| Stage | Input → output contract | Failure response |
|---|---|---|
| Ingest | Approved `data/raw/SEDG-v2.pdf` is a nonempty, accessible PDF | Stop on missing file or invalid PDF; do not invent rows |
| Inspect | Required selected pages are within PDF page range and contain extractable text | Fail/flag unreadable pages; unsupported OCR reported |
| Prepare | Page-aware fixed/paragraph chunks are nonempty and have declared maximum length | Fail if empty; visually review source columns |
| Validate | Output JSONL exists, parses, has unique record IDs and correct roles/pages | Stop on mismatch and recheck transformation |
| Store | Part B under `data/processed/`; Part C under `data/pipeline_v1/text/` | Stop/report storage or empty-output failure |
| Record lineage | `week3_manifest.json` and `pipeline_manifest.json` link exact source hash and prepared output hash | Stop on missing mapping, missing/changed input or checksum mismatch |

## Required diagram failure points

1. **Missing/unreadable PDF or selected page:** stop execution, show source/page error; do not treat non-extraction as missing company evidence.
2. **Multi-column mixing or broken source-to-disclosure mapping:** flag for page-level visual review and revise the preparation, not silently accept wrong source context.

## Responsible AI and project boundary

- Guidance (K1) explains disclosure expectations but cannot prove company activity or legal compliance.
- K2/K3 cannot override the eight pinned K1 disclosure criteria. Future company evidence must remain separate by case/entity/period.
- Full text from third-party references may be restricted to local private study; preserve link/version/hash even when bytes cannot be committed.
- There is **no model-performance result**, citation-accuracy test, trained model, evidence-gap classification or human-review evaluation in this lab.

## Verification and follow-up

| Evidence | Outcome |
|---|---|
| Part B | JSONL validation and the source-to-output lineage check passed in the saved notebook. |
| Part C | The run manifest records execution at 15:46:19 UTC on 12 November 2026. A repeat run produced matching source and output fingerprints, record counts and file mappings. |
| Diagram | The PNG and editable Draw.io diagram show the executed C0-to-D1 workflow and two failure responses. |
| Layout at the end of Lab 3 | Visual verification was still pending when the manifest was written. Its recorded status has been preserved. |
| Later Lab 4 review | The first energy chunk on physical page 26 contained both E2.2 and E2.1, and a fuel category continued into the next chunk. On physical page 30, the water categories also continued into the next chunk. Lab 4 joined the relevant spans and checked the selected Basic entries against the source layout. |
| Sharing and submission | The prepared text is included for private course review. Permission to publish extracted text and a remote submission receipt have yet to be verified. |

[Executed notebook](../notebooks/week3_pipeline.ipynb) · [Observed inventory](week3_data_inventory.md) · [Part B manifest](../data/week3_manifest.json) · [Part C manifest](../data/pipeline_v1/text/pipeline_manifest.json) · [Lab 4 review](week4_data_quality_report.md)
