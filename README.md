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

## Backfill Note (2026-03-10 to 2026-05-10)

Predictions and performance reports covering March 10 to May 10, 2026 were
generated retrospectively on May 11, 2026 using a backfill process. The
rolling 30-day budget thresholds for this period were computed using only
the predictions that existed prior to each date — zero forward bias was
applied at every step. The underlying daily probability scores used for
the backfill are the same live predictions produced by the model during
that period and stored in predictions_log.csv. No predictions were altered
or regenerated; the backfill only applied the rolling budget calculation
to already-existing prediction data and wrote the resulting JSON artifacts
to this repository in a single signed commit on May 11, 2026.

## Sync Gap Note (2026-07-06 to 2026-07-08)

Commits dated July 6–8 were synced to this repository on July 8, 2026.
A direct edit to this README on GitHub created a commit on the remote that
the Google Compute Engine instance was not aware of, causing a temporary
divergence that prevented automatic pushes. The prediction and performance
JSON files for those three dates were generated on schedule at 05:20 UTC
on their respective dates, as confirmed by the generated_at timestamp
inside each file. No prediction data was altered. The divergence was
resolved by pulling the remote change and re-syncing on July 8.
