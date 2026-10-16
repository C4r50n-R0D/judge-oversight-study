# Literature search log: local-to-hosted LLM handoff and judge-based escalation

Searched 2026-10-08 and 2026-10-09. This is a targeted search log, not a systematic review. It did not query IEEE Xplore, ACM Digital Library, Scopus, or Semantic Scholar, and it did not read full texts (abstract pages only, unless stated). Several hits are preprints without a stated venue. **Re-run close to submission; the field is moving quickly.**

Purpose: test the claim "nobody has studied handoff from local to hosted models". Result: **the broad claim is false**; only a narrower combination remains unconfirmed.

## Queries
1. edge-cloud collaborative LLM inference, small on-device model escalating to a cloud model
2. local-remote LLM collaboration, small local model with hosted frontier model, cost reduction
3. LLM cascade with verifiable signal (unit tests) for code generation
4. hybrid on-device/cloud LLM routing surveys
5. model cascades and self-verification routing (AutoMix, speculative cascades, etc.)
6. local LLM coding assistant with cloud fallback after failed tests, Apple Silicon, Ollama
7. cost-aware escalation in agentic coding (cheap model first, retry, then escalate)
8. local inference benchmarks on consumer hardware versus theoretical bandwidth bounds
9. automated harness or workflow optimization (ADAS, AFlow, harness evolution)
10. planner/executor with heterogeneous models; Reflexion and Self-Refine
11. role assignment for heterogeneous agent teams; step-level and trajectory routing in coding agents; small-model-first agentic systems; retry budgets versus escalation; hybrid local/cloud agent frameworks; multi-LLM workflow search

## Closest prior work (verified against arXiv or venue pages)
| Work | What it does | Relation to this project |
|---|---|---|
| Minions (Narayan et al., ICML 2025) | On-device small model plus cloud frontier model on long-document tasks; reports 30.4x lower remote cost at 87% of frontier performance (naive), 5.7x at 97.9% (MinionS) | Overlaps the "local plus hosted" idea; different task type, no test-based escalation |
| Model Cascading for Code (Chen et al., 2024) | Cascades with self-generated tests for code; average 26% cost reduction, up to 70% | Overlaps test-based escalation; model-generated tests, no owned-hardware tiers |
| AutoMix (Aggarwal et al.) | Small model first, self-verification, escalate; over 50% cost reduction | Escalation logic; signal is self-verification, not execution |
| FrugalGPT, RouteLLM, Hybrid LLM | Cascades and routers across hosted models | Background |
| Moslem and Kelleher survey (2026) | Surveys routing and cascading | Per its abstract, does not mention local handoff, verifier-based escalation, or energy |
| G-Boost (Liu et al.) | Edge small model fused with private-cloud larger model | Different mechanism |
| SWARM-LLM (Dahshan et al., 2026) | Routes among edge small models and an optional cloud model | Edge routing prototype |
| Rajesh et al., 2025 | Compares five local runtimes on an M2 Ultra | Runtime choice matters |
| ADAS (Hu, Lu, Clune) | Meta agent programs new agents from an archive | Harness search as a research area |
| AFlow (Zhang et al.) | MCTS over code-represented workflows; smaller models beat GPT-4o on some tasks at 4.55% of cost | Workflow search with a cost angle |
| DarwinX, HarnessCompass, HarnessForge (2026) | Harness evolution with verifier fitness, task-agnostic edits, and joint harness and policy evolution | Harness optimization; none optimizes escalation with a cost objective on owned hardware |
| COPE (Lee et al.) | Small and large models alternate as planner and executor | Fixed cascade, hand-chosen thresholds |
| AgentOpt (Hua et al., 2026) | Model-per-role search; Pareto over accuracy, cost, latency | Hosted models, no held-out split, no runtime escalation |
| Specialize Roles, Mix Deployments (Jiang et al., 2026) | Planner/executor/verifier assignments across API, self-hosted, hybrid | Benchmark, not an optimizer; no retry/escalation |
| Resample or Reroute? (Chen, 2026) | After a weak verifier decision, resample or reroute; fixed rerouting beat resampling by about 2.9 points on MBPP+; no controller beat fixed rerouting | Direct predecessor of Study 1; no hosted tier, no latency |
| SWE-Router (Son et al., 2026) | Escalates after K weak-model turns using a value head | No hardware or latency |
| RSI-Router (Li et al., 2026) | Evolves subtask routing and skills; small model with hosted DeepSeek | No runtime retry/escalation |
| SLMs are the Future of Agentic AI (NVIDIA) | Position paper for heterogeneous agentic systems | Position paper, abstract only |

## Assessment
- Each axis of a joint "roles, retry budgets, feedback, and escalation" method is covered by at least one 2026 paper; **a claim of a novel joint method is not defensible.**
- What looks thin in what was read: owned consumer-class hardware plus a hosted model, hidden-test scoring with a reported visible/hidden gap, and measured latency validated against a bandwidth bound.
- The literature itself flags one question as unresolved: when to resample versus reroute (Chen, 2026).
- Not yet covered: the judge-reliability literature (LLM-as-judge bias, weak-to-strong oversight, evaluator manipulation). This matters directly for Study 2 and must be searched before a related-work section is written.

## About the Jev judge
Jev (TypeSafe) is described in OpenRouter community docs and a Langfuse docs page as a decision model that returns typed answers (a yes/no probability, an ordered score, or a choice) instead of free text, reachable through OpenRouter as `typesafe/jev-1.13` and priced on input tokens. Langfuse says access runs through a waitlist. Not found: model size, open weights, a published evaluation as a code verifier, or an exact response schema. Vendor-reported speed and cost comparisons are not independent evidence.

## Before submission
1. Repeat the search in IEEE Xplore, ACM DL, Scopus, and Semantic Scholar with the queries above and record counts.
2. Read the full texts of the closest papers (Minions, Chen et al. 2024, Chen 2026, SWARM-LLM, COPE, AgentOpt) to confirm what they do and do not evaluate.
3. Search the judge-reliability and weak-to-strong oversight literature.
4. Re-run the search close to the submission date.
