# Judge-gated oversight of AI-written code

An empirical, pre-registered research project on when an automated LLM judge that **cannot run the code** can be trusted to approve AI-written code, and where it fails.

**Status (read this first):** early stage. Study designs and a draft pre-registration are public here. Experiment code will be released after the pre-registration is frozen. **No test-split data has been collected or analyzed.** Nothing here is a result.

## The two studies

**Study 1: judge-gated escalation.** A small local model (Qwen 2.5 Coder 7B on a MacBook) writes a draft, and an outcome-blind judge decides whether to accept it or escalate to a hosted model (Claude Sonnet). Can a judge keep accuracy near always using the hosted model while spending less? After a rejection, is it better to retry locally or to escalate? Extends Chen (2026). Pre-registration draft: [`docs/study-1-preregistration-draft.md`](docs/study-1-preregistration-draft.md).

**Study 2: judge reliability as oversight.** Three questions on tasks with exact ground truth: does judge accuracy fall as the code writer outgrows the judge; which planted defects does the judge miss; and how much does confident but false commentary shift its approvals? Design outline: [`docs/study-2-companion-design.md`](docs/study-2-companion-design.md).

## What exists today

- A tested evaluation pipeline (generation, sandboxed EvalPlus scoring, cached judge labeling, spend ledger, cluster-bootstrap analysis), not yet released in this repository.
- A draft pre-registration for Study 1, revised after an independent methods and code review.
- Phase 0 setup findings on the real benchmark data: two reference solutions fail in the pinned environment (HumanEval/32, Mbpp/255) and are excluded, and a default memory cap made correct solutions fail at random, so scoring uses explicit memory limits.
- A literature search log: [`docs/literature-notes.md`](docs/literature-notes.md). The broad claim that nobody has studied local-to-hosted handoff is false; the open gap is narrower.

## What does not exist yet

The calibration pilot, the main data collection, the Study 2 defect-planting and annotation module, and the Study 2 pre-registration.

## Scope and limitations

Short Python coding problems, small open-weight models plus Claude, and public benchmarks that are probably in training data. This is a cheap, reproducible testbed, not a general claim about scalable oversight.

## Principles

Hypotheses and decision rules are fixed in writing before test data is touched. Deviations are logged in [`DEVIATIONS.md`](DEVIATIONS.md). Null and negative results will be reported in full.

## Documents

- [Study 1 pre-registration (draft)](docs/study-1-preregistration-draft.md)
- [Study 2 design outline](docs/study-2-companion-design.md)
- [Literature notes](docs/literature-notes.md)
- [Budget estimate](docs/budget.md)

## License

Code (when released): MIT. Documents: CC BY 4.0. See [`LICENSE`](LICENSE).

## Author

Carson Rodriguez.
