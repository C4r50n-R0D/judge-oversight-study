# Budget (estimate, $2,300)

These are planning estimates, not measured costs. Per-call prices and some counts are assumptions and will be replaced with measured figures after the calibration pilot. Local generation and scoring run on hardware already owned (a MacBook Air M3 and a Debian server).

| Item | Detail | Estimate |
|---|---|---|
| Claude Sonnet code generation | 1,620 generations (3 draws for each of 540 usable problems), adaptive thinking, about $0.18 per draw | $300 |
| Claude Haiku judging | About 41,000 calls (5 votes per solution) over about 5,100 original, 1,600 defect-planted, and 1,500 annotated solutions, about $0.016 per call | $650 |
| Pilot and prompt development | Calibration-only pilot of up to 20 tasks, plus reruns while tuning judge prompts and templates, before any test data is touched | $250 |
| Jev judge via OpenRouter | One labeling pass over about 15,000 solutions, at most about $0.012 per label; reallocated to Haiku if access is not granted | $200 |
| Generating candidate defects | About 2,700 Sonnet calls; each candidate is run through the scoring harness and kept only if it fails the hidden tests | $135 |
| Authoring original coding tasks | About 30 new tasks (to reach 40 self-written), each with a reference solution and extra tests, about $5 per task | $150 |
| Annotation text generation | False-commentary variants in several wordings | $65 |
| Cloud scoring VM | Keeps load-sensitive EvalPlus time limits undisturbed while local generation runs elsewhere | $90 |
| Cloud backup storage | Six months of backup for run data, judge caches, and logs | $60 |
| Contingency for reruns | Pre-registered re-collection if a model version changes mid-run (a full rerun of the Sonnet tier is about $300) | $400 |
| **Total** | | **$2,300** |

No stipend, living expenses, hardware, or publication fees are included.
