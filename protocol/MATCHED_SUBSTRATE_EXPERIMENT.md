# Matched-Substrate Head-to-Head Experiment Protocol

**Status:** v0.1, 2026-06-01 — pre-registered protocol
**Purpose:** Provide the single new measurement that elevates the ARITH 2027 submission from research note to full conference paper.
**Source:** Appendix D of `gf_preprint-2.pdf` v1.7, expanded for the ARITH §5.4 main-body slot.
**Companion files:** `arith2027_paper_outline.md` §5.4, `goldenfloat-ladder` skill (F1/F2/F3 falsification protocol).

---

## 1. Research question

**Q1.** On a fixed FPGA substrate, does GF16 achieve a measurable advantage, parity, or disadvantage relative to posit-16, takum-16, and binary16 on a defined arithmetic workload?

**Q2.** Does the breadth-as-moat hypothesis (one rule covers GF4 to GF256) survive when at least one rung (GF16) is head-to-head against the closest live alternative (takum-16) on matched substrate?

The current status is **[Open-conjecture]** per `goldenfloat-ladder` skill. This experiment moves the status to one of: [Verified-coexistence], [Verified-advantage], [Verified-disadvantage], or [Insufficient-evidence], with all four outcomes acceptable for honest reporting in the ARITH paper.

---

## 2. Pre-registration principles

This is a **pre-registered protocol**. The decision rules below are fixed before any measurement is taken. Selective reporting after the fact is a hard violation of the `goldenfloat-ladder` claim-status discipline.

1. **All four formats reported**, no dropout.
2. **All four metrics reported** (cycles, LUTs, FFs, Fmax, accuracy), no selective reporting.
3. **Negative results disclosed** with the same prominence as positive results.
4. **All testbench seeds and pseudo-random inputs fixed and published** in supplementary materials.
5. **Bugs found during the experiment** disclosed as engineering corrections (per preprint §5.5 precedent — the f32_to_paretoq audit lesson).

---

## 3. Hardware substrate

- **FPGA board:** Xilinx Artix-7 (xc7a35t or xc7a100t — match whichever the existing GF16 323 MHz result used).
- **Toolchain:** Xilinx Vivado (record exact version).
- **Synthesis target:** speed-optimised for Fmax, area-optimised for LUTs+FFs (two runs per format).
- **Constraint files:** identical `.xdc` for all four formats (same clock target, same I/O pin map for the testbench harness).
- **Implementation strategy:** default Performance_Explore for the Fmax run, AreaOptimized_high for the area run.

---

## 4. The four formats — reference implementations

| Format | RTL source | Origin | Verification |
|---|---|---|---|
| GF16 | Existing in [Repository A] | Author's own work, already passing 35-of-35 testbench at 323 MHz on Artix-7 [Verified] | Conformance vectors (532-line JSON) |
| posit-16 (es=1) | PERCIVAL / Big-PERCIVAL | Mallasen et al., UCM Madrid, open-source GitHub | PERCIVAL test vectors |
| takum-16 | Open-source RTL accompanying arXiv:2412.20273 | Hunhold, 2024 | Hunhold's published conformance set |
| binary16 (IEEE 754) | FloPoCo-generated or open IEEE FP16 RTL | de Dinechin et al. or equivalent | IEEE 754-2019 test vectors |

**Constraint:** all four RTL implementations must be **independent, open-source, and synthesisable by the same Vivado flow**. No proprietary IP cores. No vendor-specific primitives (DSP48 blocks allowed if all four formats can use them equivalently — record the count per format).

**Anonymisation note for the ARITH paper:** the "Repository A" reference replaces the author's actual GitHub URL. The reference implementations for posit-16, takum-16, and binary16 are cited by their public paper / repository (these are not author repositories, so they may be cited normally in the reviewer-facing PDF).

---

## 5. Testbench harness

### 5.1 Three workload categories

Three orthogonal workloads, each in scope for a single ARITH paper section:

**W1 — Dot product (linear algebra primitive).**
- Compute the dot product of two fixed 1024-element vectors of pseudo-random values drawn from a fixed seed.
- Output: single scalar.
- Tests: throughput (cycles per output), accuracy (vs binary64 reference).

**W2 — Quadratic form evaluation (HPC primitive).**
- Compute x^T A x for a fixed 32x32 matrix A and a fixed 32-element vector x.
- Output: single scalar.
- Tests: throughput, accuracy, accumulator behaviour.

**W3 — Newton-Raphson iteration (transcendental primitive).**
- Compute sqrt(x) by Newton-Raphson, 8 iterations, on a fixed batch of 256 input values spanning [1, 100].
- Output: 256-element vector.
- Tests: throughput, accuracy, convergence (any non-convergent points reported).

### 5.2 Common harness across all four formats

- **Input loading:** identical bit-level seed for all four formats; format-specific conversion at the boundary.
- **Output capture:** clock-cycle counter, output register dump, BRAM accumulator dump.
- **Conversion at boundaries:** the GF16 / posit-16 / takum-16 / binary16 representation of each pseudo-random scalar is computed offline (Python) and loaded into the testbench memory; the FPGA never sees binary64 input.
- **Reference:** the binary64 software computation in NumPy / mpmath at 200-digit precision provides the ground truth for accuracy.
- **No mixed-format paths.** Each format's run is fully isolated to avoid the f32_to_paretoq class of bugs (preprint §5.5 lesson).

### 5.3 Replication artefact

The full testbench (Verilog testbench + Python driver + reference oracle) is published as supplementary material with the ARITH paper. Anyone with an Artix-7 board and a Vivado licence can reproduce the experiment.

---

## 6. Metrics

For each (format, workload) pair, report:

| Metric | Unit | Source |
|---|---|---|
| Cycles per output | clock cycles | Cycle counter in testbench |
| LUT count (post-PAR) | LUTs | Vivado utilisation report |
| FF count (post-PAR) | FFs | Vivado utilisation report |
| DSP48 count (if used) | DSP48 blocks | Vivado utilisation report |
| Maximum clock frequency | MHz | Vivado timing report, post-PAR |
| Accuracy: RMSE vs binary64 reference | dimensionless | Output capture + Python diff |
| Accuracy: Max relative error | dimensionless | Output capture + Python diff |
| Accuracy: Worst-case input (which input caused max error) | scalar | Output capture + Python diff |

**No composite "score" metric.** Each metric reported independently. The trade-off is for the reader to interpret.

---

## 7. Statistical discipline

- **Paired seeds:** for any randomised input, all four formats see the same bit-level random input. Variance is then a within-format property only.
- **Multiple seeds:** at least n = 11 seeds per workload (per preprint §5.5 minimum-detectable-effect target for MDE = 0.05 BPB at α = 0.05, power = 0.80).
- **Confidence intervals:** report 95% CI on RMSE estimates, not point estimates.
- **No p-hacking:** the seeds are fixed and published before any synthesis run begins. The pseudo-random number generator state and the bit-level inputs are part of the supplementary materials.

---

## 8. Decision rule (pre-registered)

After all data is collected:

| Outcome | Definition | Paper framing |
|---|---|---|
| **GF16 wins on at least one axis at matched substrate** | GF16 strictly better on cycles OR LUTs OR Fmax OR RMSE, no axis strictly worse | [Verified-advantage] on the winning axis; full paper viable; emphasise the win without overclaiming the others |
| **GF16 ties** | All four metrics within 5% of the median across the four formats | [Verified-coexistence]; full paper viable; emphasise GF16 as a viable point in the design space |
| **GF16 loses on all axes** | All four metrics strictly worse than the best of the three competitors | [Verified-disadvantage] on per-rung axis; full paper still viable via breadth-as-moat framing — the contribution is the ladder, not the per-rung win. Falls back to short paper if the loss is large (>50% worse on any single metric) |
| **Insufficient evidence** | Variance too high or replication failures | [Insufficient-evidence]; short paper or workshop-track submission only |

All four outcomes are publishable in some form. There is no "experiment failed" outcome that would silence the submission.

---

## 9. Timeline

| Milestone | Target date | Owner |
|---|---|---|
| Stand up posit-16 RTL build (PERCIVAL) | 30 Jun 2026 | Author |
| Stand up takum-16 RTL build (Hunhold) | 15 Jul 2026 | Author |
| Stand up binary16 RTL build (FloPoCo) | 30 Jul 2026 | Author |
| Testbench harness W1/W2/W3 written and unit-tested | 15 Aug 2026 | Author |
| First synthesis run all four formats × W1 | 31 Aug 2026 | Author |
| First synthesis run all four formats × W2 + W3 | 30 Sep 2026 | Author |
| Data audit + internal review | 15 Oct 2026 | Author |
| §5.4 of ARITH paper written | 31 Oct 2026 | Author |
| First internal full-paper draft | 30 Nov 2026 | Author |
| Final reviewer-facing PDF | 15 Jan 2027 | Author |
| ARITH 2027 submission deadline (pattern-extrapolated) | ~29 Jan - 5 Feb 2027 | — |

**Slip plan:** if the matched-substrate experiment is not complete by 15 Dec 2026, fall back to short-paper format with the pre-registered protocol as the contribution.

---

## 10. Risks

| Risk | Likelihood | Mitigation |
|---|---|---|
| PERCIVAL / takum RTL does not synthesise cleanly on Artix-7 | Medium | Allow 2-3 days per format to debug; have a fallback to a different open-source posit/takum RTL |
| Timing closure fails at the GF16 323 MHz target on one or more formats | Medium | Lower target Fmax; report Fmax achieved per format |
| GF16 loses badly on all axes | Medium | Honest reporting; fall back to short paper if loss is large |
| Train/val mismatch class of bug (preprint §5.5 lesson) | Low if disciplined | Audit every cross-format conversion; publish the harness |
| Vivado licence expiry / hardware access | Low | Existing Artix-7 access already confirmed |

---

## 11. Honesty contract

This experiment is run under `goldenfloat-ladder` skill rules:

1. No claim of per-rung superiority is made before the data is collected.
2. The hypothesis is **[Open-conjecture]** at the start.
3. The four outcomes above are all acceptable; the experiment is designed to be **falsifiable**.
4. Takum is the **closest live alternative**, cited as ally not competitor.
5. All raw data, RTL sources, conversion oracles, and the Vivado reports are published with the supplementary materials.

---

**End of protocol v0.1.**
