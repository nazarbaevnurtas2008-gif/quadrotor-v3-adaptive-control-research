# Quadrotor V3 — Online Effective-Mass Estimation and Bumpless Integral Coordination

**Nurtas Nazarbayev** · Independent Grade 12 computational study · Kazakhstan · 2026

**Publication status:** Public, AI-assisted, reproducible *research artifact*. **Not peer reviewed**, not independently validated on an external flight simulator, and not tested on physical hardware.

## Research question

Under matched *synthetic* payload, sensing, and model uncertainty, can a causal effective-mass observer combined with bumpless altitude-integral coordination improve 3D position-tracking accuracy against a tuned PID baseline? Does conditional observer gating provide additional benefit?

## Main results (bounded in-house simulation)

A frozen-parameter evaluation compared **three** controller arms in **24 matched synthetic test scenarios** (72 test simulations). The mean position RMSE over the evaluation interval (4–12 s) was:

| Controller | Mean 3D position RMSE | Versus tuned PID |
| --- | ---: | ---: |
| Tuned conventional PID | 0.14818 m | Baseline |
| Online observer + bumpless coordination, **ungated** | **0.11133 m** | **24.9% lower** |
| Online observer + bumpless coordination, gated | 0.11886 m | 19.8% lower |

The ungated controller had lower RMSE than PID in **24/24 matched test conditions**. Adding conditional gating was *worse than the ungated variant in 22/24* tests. The comparison used a deliberately limited but equal search budget for the two jointly tuned parameters; other gains and previous development histories were **not** equally optimized. These outcomes do not establish that this method outperforms all possible well-tuned PID controllers or that gating is inherently harmful in other settings.

## Experiment structure

- **72 training runs:** 3 arms × 6 candidate settings × 4 synthetic conditions.
- **72 held-out test runs:** 3 frozen controllers × 24 new synthetic conditions.
- **96 additional stress runs:** 3 arms × 16 new hover-feasible synthetic conditions × two nominal motor-speed caps.
- **240 recorded runs in this release.** The actuator-cap study had only brief clipping events, not a sustained saturation-robustness validation.

The finite set of test scenarios comes from an **uncalibrated in-house Euler-state model**. The local protocol snapshots and distinct seeds document ordering, but do not constitute external preregistration or external model validation.

## Start here

- [Six-page English research report](paper/Nurtas_Quadrotor_V3_Research_Report.pdf)
- [Full experimental report (Kazakh)](benchmark/SCIENTIFIC_REPORT_KK.md)
- [Protocol, model source code, data, checksums, and portable rerun scripts](benchmark/)
- [Authorship and AI assistance disclosure](CONTRIBUTIONS_AND_AI.md)
- [Research scope and validation status](VALIDATION_STATUS.md)

### Reproducibility

From the repository root, using a Python environment with `numpy` installed:

```bash
python benchmark/verify_archive.py
```

Expected output:

```text
VERIFIED: model hashes, tuning selection, 72+72+96 rows, separate seeds, test arm means.
```

To independently **recompute** simulations, read [benchmark/README.md](benchmark/README.md), install the dependencies in [benchmark/source_model/requirements.txt](benchmark/source_model/requirements.txt), then run from the `benchmark/` directory:

```bash
python run_fair_benchmark.py
python run_feasible_stress.py
```

**Caution:** These rerun scripts overwrite CSVs in the folder in which they run. Use a new local copy/clone, and retain the tagged release as the frozen record. SHA-256 references document internal consistency; a checksum does not certify that physical dynamics are correct.

## PX4 / ROS 2 status

Exploratory integration established ROS 2 ↔ PX4 message connectivity and static motor-allocation feasibility for read-only shadow commands. **The V3 controller was not used to fly PX4/Gazebo in closed loop.** Therefore the main accuracy result is not independently confirmed by PX4/Gazebo, and no flight-safety or deployability claim is made.

## Attribution and limits

The author reports originating the research direction and conducting analysis, with material AI assistance in coding, simulation workflows, interpretation, and manuscript drafting. This is documented in [CONTRIBUTIONS_AND_AI.md](CONTRIBUTIONS_AND_AI.md). A third-party professor offered methodological suggestions on the separate V2 precursor, **not** a V3 peer review, collaboration, or endorsement. No formal independent V3 review is claimed.

This repository shares the computational artifact for inspection and reproducibility, **not** a peer-reviewed paper. **V3 archived release (v1.0.0):** [Zenodo DOI 10.5281/zenodo.23634343](https://doi.org/10.5281/zenodo.23634343). This DOI refers to the public computational research artifact, **not** to a peer-reviewed journal article or flight validation. The older V2 DOI applies only to V2. **Licenses:** Original Python source code is made available under the [MIT License](LICENSE); original research prose, report, figures, tables and experimental datasets are made available under [CC BY 4.0](LICENSE-CONTENT.md), each **only to the extent the author holds the relevant rights**. Third-party materials and dependencies retain their own terms; see [Licensing and rights](LICENSE_STATUS.md).
