# Can an AI judge be trusted to approve code it can't run?

An empirical research project on how far an automated LLM judge that **cannot run the code** can be trusted to approve AI-written code, which kinds of defects it misses, and how easily confident but false commentary sways it.

**Status (read this first):** early stage. The study design is public here. The hypotheses and decision rules will be written down and frozen before any test data is touched. **No test data has been collected or analyzed, and nothing here is a result.**

## Why

As AI systems get more capable, people and weaker models will increasingly have to check work they cannot easily verify themselves. Code is a useful small-scale stand-in for that problem, because correctness can be measured exactly with hidden test suites. This project measures where judge-based oversight of code breaks, using a cheap and reproducible testbed.

## Three questions

1. **Weak-to-strong oversight.** Does judge accuracy fall as the code-writing model gets stronger than the judge?
2. **Subtle-flaw detection.** Which planted defects (off-by-one errors, boundary mistakes, dropped edge cases) does the judge miss, including defects the visible tests would also catch and defects they would not?
3. **Manipulation robustness.** How much does confident but false commentary ("verified against all edge cases") shift the judge's approvals of wrong code?

Details: [`docs/study-design.md`](docs/study-design.md).

## What exists today

- An evaluation pipeline, not yet released in this repository: generation, sandboxed scoring with the official EvalPlus harness in a container, cached judge labeling, spend tracking, and cluster-bootstrap statistics. It passes unit tests and a mock end-to-end run.
- Setup findings on the real benchmark data: two reference solutions (HumanEval/32 and Mbpp/255) fail in the pinned environment and are excluded, and a default memory cap made correct solutions fail at random, so scoring uses explicit memory limits.
- Early literature notes: [`docs/literature-notes.md`](docs/literature-notes.md).

## What does not exist yet

The calibration pilot, the defect-planting and annotation module, the frozen pre-registration, and all data collection.

## Plan

1. Run a calibration-only pilot (up to 20 tasks) to measure real cost, speed, and judge behavior, and finalize the design before any test data is touched.
2. Build the defect-planting and annotation module on top of the existing scoring and judging code.
3. Freeze the pre-registration, run the full collection, and publish the code, the pre-registration, and the results, including null and negative ones.

## Scope and limitations

Short Python coding problems, small open-weight models plus Claude, and public benchmarks that are probably in training data. This is a cheap, reproducible testbed that produces concrete numbers and a reusable method. It does not claim to settle scalable oversight.

## Documents

- [Study design](docs/study-design.md)
- [Literature notes](docs/literature-notes.md)
- [Budget estimate](docs/budget.md)
- [Deviations log](DEVIATIONS.md)

## License

Code (when released): MIT. Documents: CC BY 4.0. See [`LICENSE`](LICENSE).

## Author

Carson Rodriguez.
