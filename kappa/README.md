# Kappa Foundation — Initial Decision Record (22 Oct 2026)

BFIN WS2026 · Investments · Group Assignment · Lecturer: Dr. Omer Cayirli

Group: Võ Hoàng Ngọc Phú (106240420) · Trần Bình Minh (106240415) · Hoàng Trọng Đăng (103240490)

## Folder structure

```
kappa/
├── README.md
├── requirements.txt
├── docs/
│   ├── Initial_Decision_Record.pdf / .docx   ← the ≤ 2-page record
│   ├── Decision_Log.md
│   └── AI_Use_Disclosure.md
├── notebooks/
│   ├── 01_data_retrieval.ipynb               ← downloads raw data, writes data/raw/source_record.csv
│   └── 02_kappa_analysis.ipynb               ← full analysis from saved raw data (offline)
├── theory_and_sources/
│   ├── A_lecture_content_used.ipynb          ← lecture slides our methods are based on
│   └── B_external_sources_and_assumptions.ipynb  ← outside sources, links, values used
├── data/
│   ├── raw/        (yahoo/, french/, treasury/, sec/, damodaran/, source_record.csv)
│   └── processed/  (empty — all processing happens inside notebook 02)
└── outputs/
    └── original_22Oct/   ← tables T01–T15, figures F01–F03, frozen_policy.json
```

## How to reproduce

1. `pip install -r requirements.txt`
2. Open `notebooks/02_kappa_analysis.ipynb` and choose **Run All**. It reads only `data/raw/`, checks the SHA-256 hash of every file against `data/raw/source_record.csv`, and rewrites `outputs/original_22Oct/`.
3. Optional: `notebooks/01_data_retrieval.ipynb` with `REDOWNLOAD = False` (default) only re-checks the saved files and runs offline. With `REDOWNLOAD = True` it downloads again into a new dated folder `data/raw_redownload_YYYYMMDD/`, so the frozen files are never replaced.
4. The two notebooks in `theory_and_sources/` also run with Run All (offline).

Command line alternative:

```
jupyter nbconvert --to notebook --execute --inplace notebooks/02_kappa_analysis.ipynb
```

## Data record

* Retrieved on 22 Oct 2026 (UTC times per file in `data/raw/source_record.csv`): Yahoo Finance (yfinance 1.7.0, `auto_adjust=False`, daily, 2015-01-01 to 2025-12-31), Kenneth French Data Library (FF3 + momentum, monthly), U.S. Treasury nominal and real par yield curves 2015–2022, SEC EDGAR submissions JSON, Damodaran ERPJan23.xlsx.
* Decision data end on 31 Dec 2022. Data for 2023–2025 are saved but only used by the frozen evaluation rule (`RUN_EVALUATION = False` in this submission).
* Failed item: CSGS (no data on Yahoo; replaced by NSIT, see `docs/Decision_Log.md`).
