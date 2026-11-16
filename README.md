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
│   ├── 01_data_understanding.ipynb
│   ├── 02_data_cleaning.ipynb
│   ├── 03_exploratory_analysis.ipynb
│   └── 04_financial_analysis.ipynb
├── sql/                     # Schema and analytical queries
├── src/                     # Reusable Python modules
├── dashboards/              # Power BI files and exported screenshots
├── reports/                 # Findings, methodology, and project notes
├── docs/                    # Data dictionary and source documentation
├── tests/                   # Data and logic checks
├── requirements.txt
└── README.md
```

## Current status

**Stage:** Initial setup and dataset discovery.

No dataset has been selected or validated yet. Dataset selection will be documented before analysis begins. No model performance or fraud-detection results are claimed at this stage.

## Data and responsible-use principles

- Respect dataset licenses, terms, and attribution requirements.
- Do not commit confidential, personal, or restricted financial information.
- Keep large raw datasets outside Git unless redistribution is explicitly permitted and practical.
- Record data provenance, transformations, assumptions, and limitations.
- Treat anomalies and risk scores as prompts for human review, not proof of misconduct.
- Separate known labels from model predictions and prevent target leakage during evaluation.

## Reproducibility

The project will document its Python environment, data sources, cleaning steps, SQL logic, and model evaluation as these are developed. Setup instructions will be added once the first reproducible analysis is in place.

## Author

**Vinayak Mishra**

- GitHub: [@VinayakVemo-byte](https://github.com/VinayakVemo-byte)

---

This repository is actively developed as a flagship data analytics portfolio project.
