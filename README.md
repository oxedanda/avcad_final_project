# Agricultural Restructuring in Mainland Portugal (1989–2019)

Final project for *Analysis and Visualisation of Complex Agro-Environmental Data*, Master's in Green Data Science, Instituto Superior de Agronomia, Universidade de Lisboa (2025/2026).

This repository presents a reproducible analysis of structural change in mainland Portuguese agriculture using official Statistics Portugal (INE) data for four Agricultural Census reference years: 1989, 1999, 2009, and 2019. The pipeline starts from the original `.xls` exports and examines agricultural labour, total agricultural area, holdings reporting temporary and permanent crops, permanent grasslands, and crop productivity.

## Research question

**How did the structure of agriculture in mainland Portugal change between 1989 and 2019?**

The processed extracts contain totals for **Continente** only. The final analysis is therefore national and temporal rather than regional, and it does not identify regional effects or causal mechanisms.

## Main findings

Between 1989 and 2019:

- Agricultural labour decreased by **58.8%**.
- Total agricultural area decreased by only **3.3%**.
- Agricultural area per worker increased by **134.9%**.
- Holdings reporting temporary crops decreased by **72.1%**.
- Holdings reporting permanent crops decreased by **54.7%**.
- Permanent grasslands and pastures increased by **165.5%**.

Taken together, these results are more consistent with **agricultural restructuring** than with a simple disappearance of agriculture. The evidence points to a system managing a broadly similar land base with fewer workers, fewer holdings reporting crops, and a much larger area under permanent grasslands.

## Repository structure

```text
data/raw/                  Original INE .xls files
data/processed/            Harmonised mainland extracts
notebooks/01_data_loading_and_audit.ipynb
                           Initial extraction and audit notebook
notebooks/02_full_analysis.ipynb
                           Reproducible EDA and inferential analysis
src/prepare_data.py        Raw XLS extraction, cleaning, translation and validation
src/analysis.py            Authoritative analysis pipeline
outputs/figures/           Report-ready visualisations
outputs/tables/            Descriptive, inferential and provenance tables
report/                    Final report files
```

The repository should reflect the **final submitted version** of the project. Earlier text drafts may be kept only for archive or provenance purposes, but they should not appear as the main report version in the active project structure.

## Reproduce the analysis

```bash
python -m venv .venv
# Windows: .venv\Scripts\activate
# macOS/Linux: source .venv/bin/activate
pip install -r requirements.txt
python src/analysis.py
```

`src/analysis.py` first runs `src/prepare_data.py`, so the processed CSV files, audit table, descriptive tables, inferential outputs, and figures are rebuilt directly from the original INE files. The preparation step resolves merged headers, standardises labels, preserves missing values, and reduces the risk of values shifting into incorrect productivity columns.

The notebook `02_full_analysis.ipynb` contains an Open in Colab badge and reproduces the same pipeline.

## Statistical interpretation

OLS and Spearman trend statistics are included because inferential analysis is required by the project brief. Each census series contains only four observations, so p-values, confidence intervals, and fitted trends must be interpreted cautiously. They indicate simple temporal tendencies, not causality or stable population parameters.

Productivity comparisons are descriptive in cases where missing values prevent a complete four-year series. For the same reason, productivity results should be read as evidence of heterogeneous trajectories rather than as a complete ranking of all crop systems.

## Data notes

- Crop-holding indicators count holdings reporting a crop group and are **not mutually exclusive**.
- The project does **not** estimate average crop-specific holding size because the available data do not contain the necessary crop-area numerator.
- Long INE filenames may require `git config --global core.longpaths true` on Windows.
- `outputs/tables/data_provenance.csv` records the raw source, worksheet, geographic filter, years, and transformations used for each processed file.

## Team

- Andrea Dombe — 27119
- Dandara França — 27916
- Fernanda Chácara — 26298

## Sources

- Statistics Portugal (INE), Agricultural Census and agricultural statistics.
- Eurostat agriculture statistics for contextual interpretation.
