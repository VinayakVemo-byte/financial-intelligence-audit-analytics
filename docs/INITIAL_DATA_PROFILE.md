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
