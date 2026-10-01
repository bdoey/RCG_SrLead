# Alaska provisioning assessment

Read [the standalone report](outputs/analysis_report.html), or open
`Alaska_Provisioning_Analysis.ipynb` for the executed walkthrough. The VP memo is
`outputs/vp_memo.md` (183 words including its header).

The age/activity hypothesis is unsupported. The candidate saves unused-inventory
value in a five-voyage holdout but increases shortage frequency. Unresolved
records can reverse the proposed purchase saving. This is a provisional pilot
candidate, not approved Alaska operating standards.

## Run once

```sh
conda run -n dev1 python analysis.py
```

The script regenerates the report, memo, quantities, decision register, chart and
all supporting CSV/JSON outputs. It never changes either original input file.
To rebuild and execute the notebook as well:

```sh
conda run -n dev1 python build_notebook.py
```

The notebook was executed using dev1's Python 3.12 environment. Select dev1 if
your notebook editor asks for a kernel.

## Another planning profile

```sh
conda run -n dev1 python analysis.py --nights 7 --passengers 2800 --load-factor 0.85 --sea-days-percent 0.65
```

Sea-day share is a fraction, so pass `0.65`, not `65`. Each input is checked
against the Alaska training range; joint support is not guaranteed. The selected
model uses nights and passengers for exposure and sea-day share for demand rate.
Load factor is validated, but does not multiply actual passengers again.
Changing profile inputs replaces generated outputs; the supplied notebook has
the default 10-night, 2,600-passenger, 85%-load, 65%-sea profile until rebuilt.

## Deliverables

- `analysis.py`: explicit DQ01–DQ18 rules, voyage split, training-only selection,
  product forecasts, primary/stress comparisons and independent reconciliation.
- `reporting.py`: report and memo generated from verified outputs.
- `Alaska_Provisioning_Analysis.ipynb`: 13 executed code cells, no errors.
- `outputs/analysis_report.html`: full standalone readable report with embedded chart.
- `outputs/analysis_report.md`: Markdown equivalent.
- `outputs/vp_memo.md`: VP memo below the 200-word limit.
- `outputs/alaska_product_recommendations.csv`: all 24 product quantities,
  expected unused quantities and costs, empirical CV risk, held-out events and
  upper bounds, and conditional stress-fit quantities.
- `outputs/data_quality_decisions.csv`: every problem, decision, reason and count.
- `outputs/audited_rows.csv`: original records, source row IDs and audit flags.
- `outputs/voyage_split.csv`: 20 training and 5 held-out Alaska voyages.
- `outputs/holdout_*`: product/voyage-level primary and conditional stress results.
- `outputs/headline_reconciliation.json`: independent pandas and Decimal results.
- `outputs/model_parameters.csv`: coefficients, scaling definitions and reserves.
- `outputs/risk_frontier.csv`: reserve sensitivities; no test-driven retuning.
- `agent_worklog.md`: prompt excerpts and a factual work log, **not a full native
  chat transcript**. Export this chat from the app and add that transcript if
  submitting under the brief's transcript requirement.

## Definitions and limitations

User clarification: zero waste is invalid; negative waste needs a valid use case.
78 zero and 36 unexplained negative rows are quarantined. All 114 have consumption
above recorded loading. Original signed waste is preserved. A matching negative
difference is not automatically valid. The helper `match` is replaced as a check
by arithmetic tolerance, not used as model input.

`expected_unused_qty` is expected leftover inventory, not confirmed destroyed
food. Units and case sizes are missing. `empirical_shortage_risk=0` reflects a
small training residual sample and is not a future service guarantee; use the
held-out evidence and uncertainty alongside it. The primary historical deficit
count is zero by construction; the all-consumption stress shows selection bias.
The primary and stress demand fits are conditional on their different record
interpretations. The latter reverses profile purchase savings.

Purchase savings and unused-inventory savings overlap; never add them. No actual
shortage penalties, activity, carryover, plate waste, menus, forecast prices or
2026 schedule are supplied. The data are synthetic per the brief. Source
quantity sums mix native units and are source checks only.

Dependencies already present in dev1: numpy, pandas, scipy, scikit-learn,
statsmodels, matplotlib, markdown; notebook building also uses nbformat and
IPython. No dependencies were installed. No external research was needed.
No email or submission was sent. The archive uses `Candidate` as a name
placeholder; rename it with your name if submitting.
