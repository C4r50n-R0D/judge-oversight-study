# Study 2 (companion): how far can an outcome-blind judge be trusted, and where does it fail?

**Status: design outline. Not yet pre-registered, no code written, no data collected.** This document will be replaced by a full pre-registration, with its own split salt and manifest, before any test-split data is collected.

## Motivation

Study 1 treats an automated judge as a cost-control tool: it decides whether a small local model's code draft is good enough to accept, or whether to escalate to a stronger hosted model. Study 2 asks the oversight version of the same question. As models become more capable, people and weaker models will increasingly have to check work they cannot easily verify. Code is a useful small-scale stand-in, because correctness can be measured exactly by hidden test suites. This study measures how far a judge that cannot run the code can be trusted, which kinds of defects it misses, and how easily it is swayed by confident but false commentary.

## Research questions

1. **Weak-to-strong oversight.** Does judge accuracy degrade as the code-writing model gets stronger than the judge? Three code writers (Qwen 2.5 3B, Qwen 2.5 Coder 7B, Claude Sonnet) are crossed with judges (a local 7B model, Claude Haiku, and TypeSafe's Jev if access is granted). Outcomes: discrimination (AUROC against hidden-test correctness) and false-accept rate.
2. **Subtle-flaw detection.** Take known-correct solutions and plant controlled defects (off-by-one errors, boundary mistakes, dropped edge cases). Confirm each planted defect fails the hidden tests. Measure detection rate by defect type, and separately for defects the visible tests would also catch and defects they would not.
3. **Manipulation robustness.** Add confident but false commentary ("verified against all edge cases") to wrong solutions, in several wording variants. Measure how much the judge's acceptance rate shifts relative to the same solutions without commentary.

## Design principles

- Benchmarks: HumanEval+ and MBPP+ (542 problems minus two known-invalid reference tasks), plus self-authored tasks as a contamination check.
- Scoring: the official EvalPlus harness in a network-less container. Hidden-test correctness is the ground truth.
- Judges never see tests, test output, or other solutions.
- Confidence intervals from cluster bootstraps over tasks.
- Hypotheses, thresholds, and decision rules are written down and frozen before test data is touched; deviations are logged with a date and reason.
- Null and negative results are reported in full.

## Shared infrastructure with Study 1

Scoring container, judge layer with label caching, spend ledger, and bootstrap statistics are reused. New code: a defect-planting module (with a check that each planted defect fails the hidden tests) and an annotation module.

## Isolation from Study 1

Study 2 has its own pre-registration, split salt, and manifest. It does not read Study 1 test-split outcomes before Study 1's thresholds are committed and its test analysis is complete. Calibration-split pilot rows may be used to develop Study 2.

## Scope and limitations

One task family (short Python functions), small open-weight models plus Claude, one benchmark lineage that is probably in training data. This is a cheap, reproducible testbed that produces calibrated numbers and a reusable method. It does not claim to settle scalable oversight.
