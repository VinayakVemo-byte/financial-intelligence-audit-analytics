# Project Plan

## Problem framing

Financial statement analytics can help auditors and analysts prioritize review by surfacing unusual movements, inconsistent relationships, and indicators that merit further investigation. This project will prototype a reproducible workflow for such analysis.

## Key questions

1. Which companies or reporting periods show unusual financial movements?
2. Are revenue, receivables, operating cash flow, and reported earnings moving in unexpected ways?
3. Which financial ratios are most useful for descriptive risk screening?
4. Can anomaly-detection methods highlight observations that warrant human review?
5. How can findings be communicated clearly without overstating what the data proves?

## Work packages

| Stage | Deliverable | Status |
|---|---|---|
| Repository setup | README, folders, environment starter | In progress |
| Dataset discovery | Source review, schema, license, data dictionary | Not started |
| Data understanding | Profiling notebook and quality report | Not started |
| Data preparation | Reproducible cleaning workflow | Not started |
| Financial analysis | Ratios, trends, comparative analysis | Not started |
| SQL analytics | Schema and query library | Not started |
| Risk analytics | Explainable indicators and anomaly experiments | Not started |
| Dashboard | Power BI report and screenshots | Not started |
| Final documentation | Findings, limitations, reproducibility guide | Not started |

## Evaluation principles

- Split data by time and/or company where appropriate.
- Prevent company identifiers, future information, or derived target fields from leaking into predictors.
- Prefer precision-recall analysis when positive fraud labels are rare.
- Compare models against simple baselines and interpretable rules.
- Document class imbalance, label quality, and the limits of any proxy labels.
- Never interpret an anomaly score as a fraud verdict.
