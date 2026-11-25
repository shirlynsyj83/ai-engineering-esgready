# Reproducing the Lab 4 results

1. Copy the repository contents into a local working folder. For Google Colab, use `/content/ESGReady_Lab/`.
2. In the private supplement, locate `data/processed/prepared_text.jsonl`. Place it under the same path in the working folder. The public `data/week3_manifest.json` records its SHA-256. The worked assessment uses 26 input records.
3. Install the packages from `notebooks/week4_requirements.txt`. In Colab, run `%pip install -q -r /content/ESGReady_Lab/notebooks/week4_requirements.txt` in a setup cell. Restart the session if requested.
4. For the optional PDF-column comparison, place the matching SEDG Version 2 PDF at `data/raw/SEDG-v2.pdf` for permitted local use. See the [source register](source_register.md). The sample and quality calculations can run from the prepared input alone.
5. Run [the notebook](../notebooks/week4_quality.ipynb) from top to bottom. The final cell reloads the JSONL and PKL and compares IDs, text and metadata. The saved run produced eight matching passages. Use the [quality report](week4_data_quality_report.md) for the decisions and limitations.

The GitHub copy keeps the measured outcomes. The private supplement includes the unabridged executed notebooks and all original data exports. Rerunning in a private working folder may regenerate source-text previews.
