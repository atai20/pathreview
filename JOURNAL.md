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
