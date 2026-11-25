# Week 3 Data Preparation

The Topic 2 submission is a planning package. It does not include downloaded third-party PDFs, a constructed benchmark or real company records.

## Two PDF references to prepare

1. K1: SEDG Version 2 (July 2025), [official PDF download](https://sedg.capitalmarketsmalaysia.com/wp-content/uploads/2025/07/SEDG-v2.pdf).
2. K2: NSRF FAQ (14 January 2026), [official PDF download](https://www.sc.com.my/api/documentms/download.ashx?id=2efe731e-20cf-4710-8104-d07762a4637b). Only the selected context sections are used by this project.

K3 is a public HTML case study used for contextual explanations. Preserve its URL, access date and section headings when preparing a local snapshot. It is not counted as one of the two PDF files.

Download references into a local/private `data/reference_private/` directory. Add that directory to the repository's `.gitignore` unless reuse terms allow public redistribution. If the lecturer requires the PDF bytes in GitHub, confirm permitted sharing and the appropriate repository visibility; a private repository does not itself grant copyright permission. The lab's data requirement and source rights both need to be respected; a public URL alone is not a redistribution licence.

## PDF Reading and Parsing Observations — 5 November 2026

- K1 uses multi-column disclosure layouts, tables, repeated headers and a distinction between printed and physical PDF pages. Extraction must preserve the relationship between an ID and its description; do not join columns indiscriminately.
- K2 contains numbered questions, repeated headers, tables and footnotes. Preserve question numbers and avoid mixing timeline tables into the selected context answers.
- The OECD page includes navigation text around its case study; select the relevant article sections before chunking.

K1 was downloaded for source review, its selected disclosure locations were checked through text extraction, and physical PDF page 26 (printed page 25) was visually inspected. Its basic/intermediate/advanced columns place E2.1 beside E2.2: a parser must preserve the column boundaries so requirements are not merged. The related-reference table below is distinct from the disclosure text. Printed and physical page numbers differ by one on this page. These checks are source inspection, not a completed application parser. K2 was read through the public PDF viewer; a separate file download failed, so its local acquisition is not marked complete. No third-party PDF bytes are bundled for redistribution.

## Planned synthetic evidence

Create fictional manufacturing-company packs with neutral filenames and explicit company/period/site metadata. Possible records: energy/water summaries, waste registers, training summaries, incident records, governance registers and policy documents. A policy is not proof that an activity occurred. A missing incident entry is not a nil declaration.

Keep benchmark gold labels outside the application retrieval folders. Separate company packs and question families across development/test. See `docs/week2_evaluation_criteria.md` for counts and labelling requirements. All records must be clearly identified as synthetic; no real identities, account numbers or credentials are needed.

## Other preparation

Set up Google Colab for Topic 3. No local model installation is required for Topic 2. Keep a source manifest with local filenames, actual download dates and computed checksums once downloads occur.

## Topic 3 document pipeline output

The executed Pathway A notebook used eight physical K1 pages. The [Part B manifest](week3_manifest.json) and [Part C manifest](pipeline_v1/text/pipeline_manifest.json) identify the two copies of the prepared JSONL. Both contain the same 26 records. The [decision record](../docs/week3_pipeline_decisions.md) explains the method and subsequent layout review. Keep extracted text in the approved course location.


## Private assessment files

| Path inside the private supplement | Purpose |
|---|---|
| `data/processed/prepared_text.jsonl` | Lab 3 Part B prepared export and Lab 4 input, 26 records |
| `data/pipeline_v1/text/prepared_text.jsonl` | Lab 3 Part C export, matching the Part C manifest |
| `data/prepared_chunks.jsonl` and `data/chunks.pkl` | Lab 4 input compatibility pair, 26 records |
| `data/prepared_chunks_clean.jsonl` and `data/chunks_clean.pkl` | Lab 4 required reviewed corpus, eight records in each format |
| `notebooks/week3_pipeline.ipynb` and `notebooks/week4_quality.ipynb` | Original executed copies with source previews |

The GitHub versions of both notebooks retain code and measured outputs. Restore private data to these relative paths for local reproduction. The publisher PDF is referenced in the source register.
