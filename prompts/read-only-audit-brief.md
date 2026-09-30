# Read-only audit brief

Used for the [crypto scanner post-mortem](../projects/crypto-volatility-scanner/). Adapt the hypotheses to your system.

```text
TASK TYPE: ANALYZE. Read-only. Do not modify code, data, config or running services.

CONTEXT:
<System> ran live from <date> to <date>. Live results were poor. I want to know why
before changing anything. Work only from what is preserved: databases, logs, model
files and prediction logs on the server. If the local copy and the server disagree,
the server wins, and say so.

HYPOTHESES (judge each one; do not add fixes):
H1 - Weak prediction: the model did not predict the target well in live conditions.
H2 - Entry timing: the model predicted correctly but the system acted too late.
H3 - Regime dependence: the signal works in some market conditions and loses in others.
H4 - <your fourth candidate>.

PART A - establish what actually ran
- Which model file was served live, over which dates? Give path, file hash, training
  date range, training row count and offline score. Confirm by hash, not by filename.
- Was the model ever retrained during the run? Show the evidence.

PART B - live vs offline
- Grade the live prediction log against realised outcomes. Report live AUC per week.

PART C - timing
- For each alert, how much of the eventual move had already happened when it fired?
- Compare immediate entry with waiting 15, 30 and 60 minutes.

PART D - regimes
- Split results by market regime. Report hit rate and average return per regime.

PART E - collapse check
- Did predicted probabilities ever collapse into a narrow band so that no threshold
  produced alerts? Over which dates?

REPORT: for each hypothesis state SUPPORTED / REJECTED / INSUFFICIENT DATA with the
specific numbers behind the verdict. Rank the hypotheses by how much they explain.
Flag anything you could not check instead of guessing. Numbers only, no fixes proposed.
```
