# Initial Data Profile — Time Split, Fold 1

**Status:** First successful load completed. Detailed profiling is still in progress.

## Load confirmation

The initial notebook successfully loaded the explicit time-split, fold 1 CSV files.

| Dataset | Rows | Columns |
|---|---:|---:|
| Training | 11,364 | 34 |
| Testing | 3,507 | 34 |
| Combined | 14,871 | 34 |

These counts were reported by the first successful notebook run. They should be rechecked if the source files or selected split change.

## Preview observations

The displayed training preview includes the following kinds of fields:

- **Report/company identifiers:** `report_id`, `cik`
- **Reporting period:** `year`, `quarter`, `period`, `mda_quarter_id`
- **Industry descriptors:** `sic`, `sicagg`
- **Fraud/enforcement-related fields:** `aaer_no`, `labels`, `glabels`, `is_fraud`
- **Narrative fields:** `summary`, `complaints`
- **Feature metadata/counts:** `n_tags`, `n_tags_augmented`, `n_tags_total`, `n_important_tags`, `n_ratios`, `n_diff_features`, `n_aggregates`, `n_benish_features`, `n_extended_features`
- **Company/report history fields:** `serial_count`, `total_serial_count`, `cik_reports_count`

The preview suggests that each observation represents a company/reporting-period record, but the exact row grain and uniqueness key must be verified from the full data and source documentation.

## Initial interpretation notes

1. `cik` is the company identifier used in SEC filing contexts.
2. `sic` and `sicagg` are industry classification fields.
3. `period` looks like a date encoded as YYYYMMDD in the sample (for example, 20150930). This must be validated across all records before conversion.
4. `mda_quarter_id` appears to combine a company identifier and reporting period, for example `1316944_2015q3`.
5. The `n_*` columns are counts or metadata about constructed feature groups. They should not be interpreted as the underlying financial ratios or values themselves.
6. The prepared modelling table does not visibly expose common raw financial statement amounts (for example, revenue, total assets, receivables, or operating cash flow) in the preview. We should inspect the underlying quarterly financials source separately if we want to calculate our own ratios.
7. The preview shows `is_fraud` as `False` for the displayed first five records only. This does **not** establish the overall class distribution.
8. Some narrative and AAER-related columns are null in the preview. Global missingness must be measured before deciding whether those fields are sparse or unusable.
9. The source column is spelled `aeer_date` in the displayed header. Preserve the original name until verified; do not silently rename it.

## Not yet established

The following must be measured using the full training and test data:

- Data types and null percentages for all 34 columns.
- Exact duplicate-row counts.
- Uniqueness and suitability of `report_id` and any composite key.
- Fraud/non-fraud counts and prevalence in each split.
- Company overlap between train and test.
- Actual year/period coverage in both splits.
- Meaning and provenance of `labels` and `glabels`.
- Potential target leakage in feature and metadata columns.

## Next action

Continue with the schema, missing-value, duplicate, target-distribution, and company/time checks in `notebooks/01_data_understanding.ipynb`. No rows have been cleaned, removed, or transformed at this stage.


## Column-set compatibility check

The first comparison of the selected fold's training and testing files returned:

- Columns only in train: none.
- Columns only in test: none.
- Same column set: `True`.

Both files therefore expose the same 34 column names. This confirms column-set compatibility for the selected pair, but does not by itself prove identical column ordering, data types, value formats, or semantic definitions. Those checks remain part of the schema review.


## Full training-table schema and missingness review

The initial `train.info()` and per-column profile were shared after successfully loading fold 1.

### Training dataset structure

- Rows: 11,364
- Columns: 34
- Reported memory usage: approximately 2.7 MB
- Data types reported by pandas: 3 boolean, 4 float64, 16 int64, and 11 string columns.
- Unique CIK values: 5,821
- Unique report_id values: 11,364
- Unique year values: 10
- Unique period values: 104
- Unique mda_quarter_id values: 11,184
- Unique sic values: 414
- Unique sicagg values: 10
- Unique quarter values: 4
- is_fraud is non-null for all rows and has two distinct values; its class counts have not yet been measured.

These are training-table observations only. The test table still needs equivalent profiling.

### Missingness findings

One column is entirely null in training:

| Column | Non-null | Missing | Missing % |
|---|---:|---:|---:|
| mda_year_id | 0 | 11,364 | 100.00% |

Twelve additional columns each have 666 non-null and 10,698 missing values (94.14% missing):

`aaer_no`, `aeer_date`, `role`, `fiscal_quarter`, `url`, `labels`, `summary`, `complaints`, `glabels`, `num_glabels`, `serial_count`, and `total_serial_count`.

The matching non-null counts suggest these fields may describe the same subset of observations. This is a hypothesis, not yet a confirmed relationship. Check row-level co-occurrence and cross-tabulate against `is_fraud` before assigning meaning or using these fields.

### Constant-column warning

The training profile reports one unique non-null value for both `has_nt_mda_year` and `has_nt_mda_quarter`. A constant feature has no variation in this training split and ordinarily cannot help distinguish observations. The actual constant values and whether this also holds in test must be verified.

### Potentially important key observations

- `report_id` has 11,364 unique values across 11,364 rows in training. This is consistent with a unique report identifier in this split, but verify uniqueness in test and confirm its documented meaning.
- `mda_quarter_id` has 11,184 unique values, fewer than the 11,364 rows. This suggests repeated company-quarter identifiers may exist; inspect duplicate groups before deciding the row grain.
- `period` is stored as an integer and looks date-like in the sample (YYYYMMDD). Validate all values and parse carefully before date analysis.
- `aeer_date` is a string and appears only in the sparse subset. Its meaning, chronology, and availability at prediction time must be investigated.

### Analytical and leakage cautions

- Do not drop sparse fields simply because they have many missing values. Missingness may carry information, but it can also reflect the way enforcement records were joined to financial observations.
- Do not use `aaer_no`, `aeer_date`, `labels`, `glabels`, `summary`, or `complaints` as model predictors until their label construction, chronology, and availability at prediction time are understood.
- Do not assume null means negative, non-fraudulent, or zero.
- Check constant flags in both splits.
- Check duplicate report and company-period keys before aggregation.
- Compare train and test dtypes and value domains; matching column names do not prove schema equivalence.

### Next profiling steps

1. Compare every train and test column dtype.
2. Measure missing counts and percentages in test.
3. Verify constant columns in both splits.
4. Count exact duplicate rows.
5. Check uniqueness of `report_id` and duplicates of `mda_quarter_id`.
6. Measure `is_fraud` class counts and percentages separately in train and test.
7. Check company overlap and year/period coverage.
8. Investigate whether the 666-row sparse-field cohort overlaps with the fraud target and whether its information could be available at prediction time.

No data has been removed, imputed, or transformed at this stage.
