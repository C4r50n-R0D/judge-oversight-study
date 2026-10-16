# Study design: how far can an outcome-blind judge be trusted, and where does it fail?

**Status: design outline. Not yet pre-registered, and no data collected.** This document will be replaced by a full pre-registration, with its own task split and manifest, before any test-split data is collected.

## Motivation

As models become more capable, people and weaker models will increasingly have to check work they cannot easily verify. Code is a useful small-scale stand-in, because correctness can be measured exactly by hidden test suites. This study measures how far a judge that cannot run the code can be trusted, which kinds of defects it misses, and how easily it is swayed by confident but false commentary.

## Research questions

1. **Weak-to-strong oversight.** Does judge accuracy degrade as the code-writing model gets stronger than the judge? Three code writers (Qwen 2.5 3B, Qwen 2.5 Coder 7B, Claude Sonnet) are crossed with judges (a local 7B model, Claude Haiku, and TypeSafe's Jev if access is granted). Outcomes: discrimination (AUROC against hidden-test correctness) and false-accept rate.
2. **Subtle-flaw detection.** Take known-correct solutions and plant controlled defects (off-by-one errors, boundary mistakes, dropped edge cases). Confirm each planted defect fails the hidden tests. Measure detection rate by defect type, and separately for defects the visible tests would also catch and defects they would not.
3. **Manipulation robustness.** Add confident but false commentary ("verified against all edge cases") to wrong solutions, in several wording variants. Measure how much the judge's acceptance rate shifts relative to the same solutions without commentary.

## Design

- **Benchmarks:** HumanEval+ and MBPP+ (542 problems minus two known-invalid reference tasks), plus self-authored tasks as a contamination check, since both public suites are likely in the training data of every model used.
- **Ground truth:** correctness is scored by the official EvalPlus harness in a network-less container. Hidden-test correctness is the outcome for every question.
- **Judges:** a judge sees only the task text and the candidate code, never tests, test output, or other solutions.
- **Statistics:** confidence intervals from cluster bootstraps over tasks.
- **Pre-registration:** hypotheses, thresholds, and decision rules are written down and frozen in git before test data is touched. Deviations are logged with a date and reason in [DEVIATIONS.md](../DEVIATIONS.md).
- **Reporting:** null and negative results are reported in full.

## Existing infrastructure

Generation across local and hosted models, sandboxed scoring, judge labeling with caching, spend tracking, and bootstrap statistics are built and tested but not yet released in this repository. New code needed for this study: a defect-planting module that checks each planted defect fails the hidden tests, and an annotation module for the false-commentary conditions.

## Plan

1. Calibration-only pilot of up to 20 tasks to measure real cost, speed, and judge behavior, and to finalize the design.
2. Build the defect-planting and annotation modules.
3. Freeze the pre-registration, run the full collection, and publish code, pre-registration, and results.

## Scope and limitations

One task family (short Python functions), small open-weight models plus Claude, and one benchmark lineage that is probably in training data. This is a cheap, reproducible testbed that produces calibrated numbers and a reusable method. It does not claim to settle scalable oversight.
