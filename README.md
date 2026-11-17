# Financial Intelligence: Audit Analytics & Fraud Risk Detection

An analytics-first portfolio project exploring how financial statement data can support audit planning, unusual-pattern detection, and evidence-led risk assessment.

> **Important:** This is an educational analytical prototype. It identifies risk indicators that may warrant investigation; it does not establish that a company has committed fraud.

## Project objectives

- Understand and profile financial statement datasets.
- Clean and validate financial data using Python.
- Analyze profitability, liquidity, leverage, and operating performance.
- Use SQL to investigate trends, exceptions, and company-level patterns.
- Explore explainable anomaly-detection techniques.
- Communicate findings through an interactive Power BI dashboard.
- Translate analytical results into practical audit-investigation questions.

## Planned workflow

1. **Data understanding:** document source, licensing, fields, coverage, labels, and limitations.
2. **Data preparation:** inspect data quality, missingness, duplicates, outliers, and entity/time keys.
3. **Exploratory and financial analysis:** calculate financial ratios and examine trends and relationships.
4. **SQL analytics:** build analysis-ready tables and reusable audit queries.
5. **Risk indicators and anomaly detection:** develop interpretable rules and compare them with unsupervised methods.
6. **Dashboard and reporting:** present trends, exceptions, and investigation priorities.
7. **Evaluation and documentation:** assess limitations, avoid data leakage, and document reproducible results.

## Technology

- **Python:** pandas, NumPy, matplotlib, seaborn, scikit-learn
- **Data access:** Hugging Face Hub and fsspec
- **SQL:** PostgreSQL
- **BI:** Power BI and DAX
- **Development:** Jupyter, Git, GitHub

Tools may be adjusted as the dataset and project requirements become clearer.

## Repository structure

```text
financial-intelligence-audit-analytics/
├── data/
│   ├── raw/                 # Local source files; not committed
│   ├── processed/           # Reproducible derived data; not committed by default
│   └── external/            # External reference files; not committed by default
├── notebooks/
│   └── 01_data_understanding.ipynb
├── sql/                     # Schema and analytical queries
├── src/                     # Reusable Python modules
├── dashboards/              # Power BI files and exported screenshots
├── reports/                 # Findings, methodology, and project notes
├── docs/
│   ├── DATASET_REVIEW.md
│   ├── INITIAL_DATA_PROFILE.md
│   └── PROJECT_PLAN.md
├── tests/                   # Data and logic checks
├── requirements.txt
└── README.md
```

## Current status

**Stage:** Dataset discovery and initial profiling.

The primary dataset candidate is the [Financial Statement Fraud Detection Dataset](https://huggingface.co/datasets/WaguyMZ/Financial_statements_fraud_dataset). Its documentation describes quarterly financial reports, summarized MD&A reports, AAER records, and prepared train/test splits.

- [Dataset review and source limitations](docs/DATASET_REVIEW.md)
- [Initial data profile — first successful load](docs/INITIAL_DATA_PROFILE.md)
- [Notebook 01 — Data Understanding](notebooks/01_data_understanding.ipynb)

The selected time-split, fold 1 files loaded successfully: **11,364 training rows** and **3,507 testing rows**, each with **34 columns**. These are initial load counts, not model results. Detailed schema, missingness, duplicate, target-distribution, and company/time checks are still pending.

## Data and responsible-use principles

- Respect dataset licenses, terms, and attribution requirements.
- Do not commit confidential, personal, or restricted financial information.
- Keep large raw datasets outside Git unless redistribution is explicitly permitted and practical.
- Record data provenance, transformations, assumptions, and limitations.
- Treat anomalies and risk scores as prompts for human review, not proof of misconduct.
- Separate known labels from model predictions and prevent target leakage during evaluation.

## Reproducibility

From the repository root, create an environment and install dependencies:

```bash
python -m venv .venv
# Windows PowerShell:
.venv\Scripts\Activate.ps1
# macOS/Linux:
# source .venv/bin/activate

python -m pip install --upgrade pip
python -m pip install -r requirements.txt
```

Open the notebook with Jupyter:

```bash
jupyter notebook
```

The project will document its Python environment, data sources, cleaning steps, SQL logic, and model evaluation as these are developed.

## Author

**Vinayak Mishra**

- GitHub: [@VinayakVemo-byte](https://github.com/VinayakVemo-byte)

---

This repository is actively developed as a flagship data analytics portfolio project.
