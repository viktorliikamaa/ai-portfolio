# Safe change to a live system

Two parts: prove the change is safe, then make exactly one change. Written for swapping the model a live system loads, but the shape works for any change to something running.

```text
TASK TYPE: ANALYZE then FIX. Part A is read-only. Part B is a bounded change that
happens only if Part A confirms every precondition.

PART A - verify before touching anything
1. Does the artifact we want to switch to still exist? Give path, file hash, training
   row count, training date range and the list of inputs it expects.
2. Do the inputs it expects MATCH what the live system produces at run time? List any
   input the new artifact expects that the live system does not produce, and vice
   versa. A mismatch here fails silently.
3. Does the live system load a hardcoded path or a configurable one?
Report all of this before changing anything. If the artifact is missing or the inputs
don't match, STOP and report. Do not attempt to retrain or work around it in this task.

PART B - only if Part A confirms everything
Make the live system load the new artifact. Add one startup log line stating which
file it loaded, its hash, its score and its training date range, so a stale artifact
can never hide again. Do not restart the service. Show me the diff.

OUT OF SCOPE: retraining automation, entry logic, filters, anything else.
One change, logged loudly.
```
