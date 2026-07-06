# Solar TPM Model 4 (Ranger) — Disk-Level Budget Alerts

Daily global solar disk probability scores with rolling 30-day budget thresholds
for M-class, strong M-class (M5+), and X-class flare prediction.

## Folders

- `predictions/` — Daily disk-level alert JSON (one file per day)
- `performance/` — Daily disk-level budget performance report JSON (one file per day)

## Budget Levels

Alerts are issued at 1%, 5%, 10%, 20%, and 30% rolling 30-day budgets.
A 10% budget means: alert fires when today's probability ranks in the top 10%
of the prior 30 days — zero forward bias, fully production-realistic.

## Blind Test

Live since March 2026. All predictions published before the 06:00 UTC
prediction window opens.

FAR in our metrics is False Alarm Rate, defined as:
FAR = FP / (FP + TN)
The proportion of non-event days on which the model fired an alert. It answers: "Out of all the days when nothing happened, how often did we cry wolf?"

This is distinct from two other commonly confused metrics:
False Alarm Ratio = FP / (FP + TP) — out of all days we did alert, how many were wrong. This is the complement of Precision.
Miss Rate = FN / (FN + TP) — out of all event days, how many did we miss. This is the complement of Recall.

In the context of TSS:
TSS = Recall − FAR = TP/(TP+FN) − FP/(FP+TN)
