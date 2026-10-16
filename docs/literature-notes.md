# Literature notes (in progress)

Searched 2026-10-08 and 2026-10-09. These are targeted notes, not a systematic review. They did not query IEEE Xplore, ACM Digital Library, Scopus, or Semantic Scholar, and they did not read full texts (abstract pages only, unless stated). Several works are preprints without a stated venue. **The field moves quickly; re-run close to submission.**

## What has not been searched yet

The literature most central to this project: LLM-as-judge reliability and bias, weak-to-strong and scalable oversight, and evaluator manipulation or sycophancy toward persuasive but wrong answers. This must be searched, and its full texts read, before any related-work section is written or any novelty claim is made.

## Related work found so far: verifiers and judges used to gate code

These came from searches on cascades and routing. They matter here because each uses some verifier signal to decide whether to accept a model's output.

| Work | Verifier signal | Relevance |
|---|---|---|
| Model Cascading for Code (Chen et al., 2024) | Model-generated tests for code; average 26% cost reduction, up to 70% | Verifier quality for code, but with generated tests rather than outcome-blind judging |
| AutoMix (Aggarwal et al.) | Self-verification by the model; over 50% cost reduction | Self-verification as an acceptance signal |
| Resample or Reroute? (Chen, 2026) | Weak verifier decisions on MBPP+ with open-weight models; no controller beat fixed rerouting | Evidence that weak verifiers are a bottleneck; closest in setting |
| SWE-Router (Son et al., 2026) | Value head supervised by unit-test outcomes | Learned verifier trained on test results |
| Minions (Narayan et al., ICML 2025) | Small on-device model coordinating with a cloud model | Background on small-plus-large model systems |
| Specialize Roles, Mix Deployments (Jiang et al., 2026) | Planner/executor/verifier role assignments | Verifier as an explicit role |
| SLMs are the Future of Agentic AI (NVIDIA) | Position paper | Background (abstract only) |

Not claimed: that any of these studies judge failure modes under planted defects or false commentary, or how judge accuracy scales with generator strength. Those are the questions this project asks, and only a full search can establish whether they have been answered.

## About the Jev judge

Jev (TypeSafe) is described in OpenRouter community docs and a Langfuse docs page as a decision model that returns typed answers (a yes/no probability, an ordered score, or a choice) instead of free text, reachable through OpenRouter as `typesafe/jev-1.13` and priced on input tokens. Langfuse says access runs through a waitlist. Not found: model size, open weights, a published evaluation as a code verifier, or an exact response schema. Vendor-reported speed and cost comparisons are not independent evidence.

## Before submission

1. Search the judge-reliability, weak-to-strong oversight, and evaluator-manipulation literature, and record query counts.
2. Search IEEE Xplore, ACM DL, Scopus, and Semantic Scholar.
3. Read the full texts of the closest works to confirm what they do and do not evaluate.
4. Re-run the search close to the submission date.
