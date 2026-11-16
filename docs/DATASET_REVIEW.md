# Dataset Review: Financial Statement Fraud Detection

**Review status:** Primary candidate selected; hands-on schema and data-quality validation pending.

## Selected source

- **Dataset:** [Financial Statement Fraud Detection Dataset](https://huggingface.co/datasets/WaguyMZ/Financial_statements_fraud_dataset)
- **Host:** Hugging Face
- **Dataset owner:** WaguyMZ
- **Associated research:** *Read Between the Lines: A Robust Financial Statement Fraud Detection Framework* by Guy Stephane Waffo Dzuyo, Gaël Guibon, Christophe Cerisara, and Luis Belmar-Letelier.
- **Declared dataset license:** The Hugging Face dataset card currently displays GPL. Review the exact license text and terms before redistribution or reuse in a commercial context.
- **Access:** The dataset is hosted externally. Do not copy its large source files into this GitHub repository.

## Documented scope

The dataset documentation describes:

- 269,097 quarterly financial reports.
- 13,323 companies in the financial configuration.
- 17,863 summarized quarterly MD&A reports.
- 3,300 AAER reports.
- Prepared datasets with fraud labels and multiple train/test strategies.

These are source-documented figures, not results independently reproduced by this project. Counts may refer to different layers of the dataset (source financial reports, text summaries, enforcement records, and prepared modelling splits).

## Why this source is a strong candidate

It combines structured financial information with enforcement-related labels and summarized narrative disclosures. That supports an analytics-first project:

1. Profile and understand quarterly financial data.
2. Build descriptive company and period-level analyses.
3. Calculate or validate financial indicators where the underlying fields support them.
4. Study labelled observations and the limits of those labels.
5. Develop an explainable risk-screening workflow and, later, carefully evaluated anomaly-detection models.

## Split strategy

The dataset documentation describes these evaluation approaches:

| Strategy | Documented design | Intended use in this project |
|---|---|---|
| Time split | Train on 2009–2019 and test on 2020–2021 | Primary first evaluation, to approximate prediction on later reporting periods |
| Company-isolated | Five folds; companies in train are separated from companies in test | Additional generalization check |
| Random | Five folds with shuffled observations | Baseline/reference only; not the main evidence of real-world generalization |

We will begin with the provided **time-split, fold 1** files for the first data-understanding exercise. We will not train a model until the schema, label meaning, time coverage, missing values, duplicates, and possible leakage fields have been reviewed.

## Important data-loading caveat

The Hugging Face dataset viewer currently reports a schema-casting issue when it attempts to combine files from different split configurations. The error describes columns that appear in some CSVs but not others.

For the initial notebook, load the explicit train and test CSV files for one split directly. Do not attempt to load every CSV in the repository as one combined dataset. Treat the source schema as provisional until we inspect the actual files.

## First files to inspect

The source repository includes:

- `FINANCIALS_PREPROCESSED/sec_financials_quarterly.csv` — underlying quarterly financial information.
- `FINAL_DATASETS/time_splitting/fold_1/train.csv` — prepared training split.
- `FINAL_DATASETS/time_splitting/fold_1/test.csv` — prepared test split.
- `AAER_PREPROCESSED/` — enforcement-related records and associated misstatement labels.
- `SEC_MDA_SUMMARIZED/` — summarized MD&A text.

We will initially use the prepared train/test files to learn the schema. The larger underlying financial file may be considered for a separate descriptive-analysis track after reviewing its columns and storage requirements.

## Class imbalance and evaluation

The dataset documentation reports a fraud prevalence of approximately 5% in the prepared data. We must calculate the exact ratio for the selected training and test files rather than assume it is identical across splits.

Accuracy alone will be misleading when positive labels are rare. Later model evaluation should include precision, recall, F1, confusion matrix, PR-AUC, and an appropriate baseline. The split design and label construction must be described alongside every metric.

## Label interpretation and limitations

- A fraud-related label is a dataset annotation linked to the source's enforcement-related records; it is not a complete census of all fraud.
- An unlabelled or negative observation must not automatically be interpreted as proof that no misconduct occurred.
- A statistical outlier is not proof of fraud.
- The project will use terms such as **risk indicator**, **unusual pattern**, and **requires further review**, not definitive accusations.
- We will record data coverage, annotation assumptions, time-period limitations, and any fields that could leak the target.

## Source links

1. [Original Hugging Face dataset](https://huggingface.co/datasets/WaguyMZ/Financial_statements_fraud_dataset)
2. [Prepared time-split files](https://huggingface.co/datasets/WaguyMZ/Financial_statements_fraud_dataset/tree/main/FINAL_DATASETS/time_splitting)
3. [Underlying quarterly financial data](https://huggingface.co/datasets/WaguyMZ/Financial_statements_fraud_dataset/tree/main/FINANCIALS_PREPROCESSED)
4. [SEC Financial Statement Data Sets](https://www.sec.gov/dera/data/financial-statement-data-sets.html) — official reference source for structured SEC filing data.

## Research citation

Waffo Dzuyo, G. S., Guibon, G., Cerisara, C., & Belmar-Letelier, L. (2025). *Read Between the Lines: A Robust Financial Statement Fraud Detection Framework*. Preprint/version information should be checked against the authors' current research record before final academic citation.

The dataset card also provides a BibTeX citation. We will retain the citation required by the version actually used and verify publication metadata before final submission.
