# Week 7 — Issue Selection

**Issue link:** https://github.com/ascherj/pathreview/issues/152

**Issue title:** Faithfulness checker can never mark short claims as supported

**Tier:** ☑ Tier 1 ☐ Tier 2 ☐ Tier 3

## Problem summary

The issue affects the faithfulness checker on the review page. Currently, very short claims cannot be marked as **Supported**, even when the provided evidence clearly supports them. This causes the review results to be inaccurate for short claims. The goal of this issue is to update the faithfulness checking logic so that short claims are evaluated correctly and can be marked as supported when appropriate.

**Branch name:** `fix/152-review-card-update`

**Setup confirmation:** ☑ App runs locally at `localhost:5173`

**Cohort ledger:** ☐ Issue added to cohort ledger

## Selection notes ("Is this right for me?" checklist)

I selected this Tier 1 issue because it has a clearly defined scope and focuses on fixing a single bug rather than implementing a new feature. Based on the issue description, I expect to locate the relevant files without needing to understand the entire codebase and modify only a small number of files. The issue uses technologies I am already familiar with, and I can verify the fix by running the application locally and testing that short claims are correctly marked as supported. This makes it an appropriate first open-source contribution that I can complete within the expected timeframe.

## Week 8 — Reproduction & solution planning

**Reproduction commit link:** https://github.com/atai20/pathreview/commit/1525aecc44db2930c43003eb595f5b7f337dde65

**Reproduction summary:**
I reproduced issue #152 locally by running the exact snippet from the GitHub issue against the pre-fix `_is_supported` / `_extract_claims` logic in `rag/evaluator/faithfulness_checker.py`. For feedback `Knows Python. Knows SQL.` with context chunks `python expert` and `sql expert`, only `Knows Python` was extracted (because `Knows SQL` is ≤10 characters), meaningful overlap was a single token `python`, and `check()` returned `0.0` even though both skills are clearly present in context. The same root cause also explains the related failing unit tests `test_partial_support_returns_middle_score`, `test_multiple_context_chunks`, and `test_multiple_claims_varying_support`.

**Reproduction evidence (observed locally):**
```text
claims extracted: ['Knows Python']
  claim='Knows Python' supported=False
    meaningful overlap: {'python'}
old check score: 0.0
expected if supported: 1.0
```

**PLAN.md link:** https://github.com/atai20/pathreview/blob/fix/152-review-card-update/PLAN.md

**Walkthrough video (recommended):**

**Blockers or open questions:**
Need to keep the two-token rule for longer material claims so lowering the floor globally does not create false positives (for example `Python expert` matching on `python` alone). Partial-score calibration for middle-range tests is the main tuning risk going into implementation.
