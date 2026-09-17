[1mdiff --git a/README.md b/README.md[m
[1mindex bf79e3c..495400d 100644[m
[1m--- a/README.md[m
[1m+++ b/README.md[m
[36m@@ -1,109 +1,96 @@[m
 # sustainability-score[m
 [m
[31m-A static-analysis tool that scores a code repository's **sustainability posture**[m
[31m-across five weighted pillars, grounded in the Green Software Foundation[m
[31m-[Software Carbon Intensity (SCI)](https://sci.greensoftware.foundation/)[m
[31m-specification. Think "code-quality scanner, but for carbon and cost efficiency."[m
[32m+[m[32m[![GitHub stars](https://img.shields.io/github/stars/srinathgopinath-code/sustainability-score?style=flat-square)](https://github.com/srinathgopinath-code/sustainability-score/stargazers)[m
[32m+[m[32m[![GitHub forks](https://img.shields.io/github/forks/srinathgopinath-code/sustainability-score?style=flat-square)](https://github.com/srinathgopinath-code/sustainability-score/network/members)[m
[32m+[m[32m[![License: MIT](https://img.shields.io/badge/license-MIT-green?style=flat-square)](LICENSE)[m
 [m
[31m-It reads only what is in the repository (source, Dockerfiles, CI workflows,[m
[31m-Terraform, Kubernetes manifests, dependency files). It never runs the code and[m
[31m-never measures live infrastructure, so it is **honest about confidence**: every[m
[31m-finding is stamped with a data-quality tier, and the report says plainly that[m
[31m-the score is directional, not a measurement.[m
[32m+[m[32m**A transparent static-analysis scanner for the sustainability posture of software repositories.**[m
 [m
[31m-## Scope[m
[32m+[m[32m`sustainability-score` reviews source code and engineering configuration, then produces a directional score across five weighted pillars: algorithm efficiency, cloud infrastructure, containerization, CI/CD, and SRE/operations. It is grounded in the Green Software Foundation's [Software Carbon Intensity (SCI)](https://sci.greensoftware.foundation/) specification—but it does not pretend that a static scan is live carbon measurement.[m
 [m
[31m-This is an early **prototype / proof-of-concept**. It is deliberately narrow:[m
[31m-one working end-to-end path from a repo to a scored, dual-format report. It is[m
[31m-advisory only. It does not gate builds, and every recommendation that could[m
[31m-affect capacity or resiliency states the SLO trade-off explicitly.[m
[32m+[m[32m> **The honest part:** every finding includes a data-quality tier. The tool never runs the target code, never measures live infrastructure, and clearly separates engineering signals from measured energy or carbon.[m
 [m
[31m-**In scope:** static repo/PR-level scoring across the five pillars below.[m
[31m-**Out of scope:** runtime measurement, carbon accounting/reporting, live[m
[31m-telemetry, and any commercialization/SaaS concerns.[m
[32m+[m[32m## Why use it?[m
 [m
[31m-## The five pillars[m
[31m-[m
[31m-| Pillar | Weight | SCI terms it moves |[m
[31m-|---|---:|---|[m
[31m-| Code / Algorithm Efficiency | 30% | E, R |[m
[31m-| Cloud Infrastructure Choices | 25% | E, I, M |[m
[31m-| Containerization | 15% | E, M |[m
[31m-| CI/CD Practices | 15% | E |[m
[31m-| SRE / Operations | 15% | E, R |[m
[31m-[m
[31m-`SCI = ((E x I) + M) / R` — a static scan cannot measure E, I, M or R, but it[m
[31m-can assess the engineering choices that push each term up or down.[m
[31m-[m
[31m-## Data-quality tiers[m
[32m+[m[32m- **Scan a repository without executing it.** Inspects source, Dockerfiles, CI workflows, Terraform, Kubernetes manifests, and dependency files.[m
[32m+[m[32m- **Get a dual-format report.** Emit Markdown for humans and JSON for automation.[m
[32m+[m[32m- **See where the score comes from.** Findings are tied to pillars, severity, SCI terms, and evidence quality.[m
[32m+[m[32m- **Keep operational trade-offs visible.** Recommendations that could affect capacity or resiliency state the SLO trade-off explicitly.[m
[32m+[m[32m- **Use it as advisory tooling.** It does not gate builds or claim to compute full SCI from static evidence alone.[m
 [m
[31m-Every finding declares the highest tier its evidence supports:[m
[31m-[m
[31m-1. **Static analysis only** — directional; inferred from source and config.[m
[31m-2. **Static + declared infra** — corroborated by IaC (region, instance types).[m
[31m-3. **Static + operational telemetry** — backed by observability data.[m
[31m-4. **Direct measurement** — energy/carbon measured; full SCI computable.[m
[31m-[m
[31m-A static-only scan never claims above Tier 1 on its own; Tier 2 is reached only[m
[31m-when the repo declares its own infrastructure.[m
[31m-[m
[31m-## Install[m
[32m+[m[32m## Quick start[m
 [m
 ```bash[m
 pip install -e .[m
[32m+[m[32msustainability-score /path/to/repo[m
 ```[m
 [m
[31m-## Usage[m
[32m+[m[32mWrite both report formats to files:[m
 [m
 ```bash[m
[31m-# Print a Markdown report to stdout[m
[31m-sustainability-score /path/to/repo[m
[31m-[m
[31m-# Write both formats to files[m
 sustainability-score /path/to/repo --json report.json --md report.md[m
 ```[m
 [m
[31m-Or from Python:[m
[32m+[m[32mUse it from Python:[m
 [m
 ```python[m
[31m-from sustainability_score import scan, to_json, to_markdown[m
[32m+[m[32mfrom sustainability_score import scan[m
[32m+[m
 result = scan("/path/to/repo")[m
 print(result.composite_score, result.grade)[m
 ```[m
 [m
[32m+[m[32m## The five pillars[m
[32m+[m
[32m+[m[32m| Pillar | Weight | SCI terms it can influence |[m
[32m+[m[32m|---|---:|---|[m
[32m+[m[32m| Code / Algorithm Efficiency | 30% | E, R |[m
[32m+[m[32m| Cloud Infrastructure Choices | 25% | E, I, M |[m
[32m+[m[32m| Containerization | 15% | E, M |[m
[32m+[m[32m| CI/CD Practices | 15% | E |[m
[32m+[m[32m| SRE / Operations | 15% | E, R |[m
[32m+[m
[32m+[m[32m`SCI = ((E × I) + M) / R`. A static scan cannot measure E, I, M, or R directly; it assesses engineering choices that may push those terms up or down.[m
[32m+[m
[32m+[m[32m## Confidence, not false precision[m
[32m+[m
[32m+[m[32mEvery finding declares the highest evidence tier it supports:[m
[32m+[m
[32m+[m[32m1. **Static analysis only** — directional; inferred from source and configuration.[m
[32m+[m[32m2. **Static + declared infrastructure** — corroborated by IaC such as region and instance type.[m
[32m+[m[32m3. **Static + operational telemetry** — backed by observability data.[m
[32m+[m[32m4. **Direct measurement** — energy or carbon measured; full SCI may be computable.[m
[32m+[m
[32m+[m[32mA static-only scan never claims above Tier 1 on its own. Tier 2 is reached only when the repository declares its own infrastructure.[m
[32m+[m
 ## Example[m
 [m
[31m-Run against the bundled fixture (a deliberately wasteful sample service):[m
[32m+[m[32mRun against the bundled deliberately wasteful sample service:[m
 [m
 ```bash[m
 sustainability-score tests/fixtures/sample_service --md docs/sample-report.md[m
 ```[m
 [m
[31m-A rendered sample report lives at [`docs/sample-report.md`](docs/sample-report.md).[m
[32m+[m[32mSee the rendered [sample report](docs/sample-report.md).[m
[32m+[m
[32m+[m[32m## Scope and status[m
[32m+[m
[32m+[m[32mThis is an early **v0.1 prototype / proof of concept**: one working end-to-end path from a repository to a scored, dual-format report. It is advisory only.[m
 [m
[31m-## How scoring works[m
[32m+[m[32m**In scope:** static repository/PR-level scoring across the five pillars.[m
 [m
[31m-Each applicable pillar starts at 100 and loses points per finding by severity[m
[31m-(high 20 / medium 10 / low 4 / info 0), floored at 0. The composite is the[m
[31m-weighted mean over **applicable** pillars only — a pillar with no relevant[m
[31m-artifacts (e.g. no Dockerfile) is marked *not applicable* and its weight is[m
[31m-renormalized away rather than counted as a free 100.[m
[32m+[m[32m**Out of scope:** runtime measurement, carbon accounting or reporting, live telemetry, and commercialization/SaaS concerns.[m
 [m
[31m-## Tests[m
[32m+[m[32mNear-term roadmap items include broader per-language efficiency checks, a JSON schema for the output, an optional GitHub Action for advisory PR comments, and a path from Tier 1 toward Tier 3 confidence when declared infrastructure and telemetry are available.[m
[32m+[m
[32m+[m[32m## Development[m
 [m
 ```bash[m
 python -m pytest[m
 ```[m
 [m
[32m+[m[32mThe project is intended as an upstream/canonical implementation, with a version proposed for the Green Software Foundation reference-implementations collection.[m
[32m+[m
 ## License[m
 [m
 MIT. See [LICENSE](LICENSE).[m
[31m-[m
[31m-## Status & roadmap[m
[31m-[m
[31m-This is a v0.1 prototype. Near-term direction: broaden per-language efficiency[m
[31m-checks, add a JSON schema for the output, wire an optional GitHub Action that[m
[31m-posts the advisory PR comment, and (with declared infra + telemetry) climb from[m
[31m-Tier 1 toward Tier 3 confidence. It is intended as the upstream/canonical[m
[31m-implementation, with a version proposed to the GSF reference-implementations[m
[31m-collection referencing this repo.[m
