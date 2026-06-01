# arith2027-goldenfloat

Working repository for the **ARITH 2027** (IEEE Symposium on Computer Arithmetic, 34th edition) submission of the **GoldenFloat** paper.

**Target venue:** ARITH 2027 — outside North America, summer 2027
**Format:** 8 pages two-column IEEE CS Conference, double-blind review
**Expected paper deadline:** ~29 Jan - 5 Feb 2027 (pattern-extrapolated)
**Status:** scaffold and pre-registered protocol, v0.1

---

## Repository layout

```
arith2027-goldenfloat/
├── PLAN.md                         # Full submission plan (timeline, decisions, risks)
├── README.md                       # This file
├── paper/
│   ├── OUTLINE.md                  # Section-by-section 8-page layout with word counts
│   ├── ANONYMISATION_CHECKLIST.md  # Double-blind redaction list (run before every iteration)
│   └── arith2027_paper.tex         # LaTeX scaffold in IEEEtran conference class
├── protocol/
│   └── MATCHED_SUBSTRATE_EXPERIMENT.md  # Pre-registered head-to-head experiment protocol
└── supplementary/
    └── (RTL, conformance vectors, replication scripts to be added)
```

---

## What is in scope

The paper describes **GoldenFloat (GF)**, a family of floating-point formats whose exponent:mantissa split is generated, for each total width N, by a single closed rule:

`e = round((N-1)/phi^2)`,  `m = N-1-e`

where phi = (1+sqrt(5))/2.

The contribution is three-fold:

1. **A rule** that reproduces nine realised widths (GF4 through GF256) exactly [Verified] and extends consistently to GF128, GF512, and GF1024.
2. **A classical integer identity** `phi^(2n) + phi^(-2n) = L_(2n)` (Lucas numbers), verified symbolically for n = 1..256 and numerically at 500 decimal places. Attribution to Lucas (1878) and Binet — not original to this work.
3. **One hardware artefact** — a GF16 codec on Artix-7 FPGA passing a 35-of-35 testbench at 323 MHz — plus a pre-registered matched-substrate head-to-head experiment against posit-16, takum-16, and binary16 on the same board.

---

## What is explicitly NOT claimed

Per the `goldenfloat-ladder` operating rules:

- **No uniqueness of base.** Phi is not claimed to be the unique algebraic base for a multi-width float family.
- **No per-rung superiority.** No GF rung is claimed to outperform posit, takum, MX, or LNS on any specific task at matched substrate.
- **No silicon validation.** No die has been returned from fabrication.
- **No software-BPB falsification.** Software-stack BPB measurements are insufficient to settle the breadth-as-moat hypothesis on their own — the matched-substrate experiment is required.

The breadth-as-moat hypothesis is **[Open-conjecture]** with an explicit F1/F2/F3 falsification path; see `protocol/MATCHED_SUBSTRATE_EXPERIMENT.md`.

---

## Closest live alternative

**Takum** (Hunhold, arXiv:2412.20273; Hunhold and Gustafson, arXiv:2504.21197, arXiv:2504.21130) is the closest live alternative with peer-reviewed multi-width hardware. Takum is cited as an **ally**, not a defeated competitor. The matched-substrate experiment in `protocol/MATCHED_SUBSTRATE_EXPERIMENT.md` uses an open-source takum-16 RTL as one of the four reference implementations.

---

## Anti-bundling

This work is **independent** of:

- Foundations of Physics manuscript (phi-structured physical constants, different track, different authorship).
- IGLA RACE training architecture (machine-learning training pipeline, different track).
- Any DARPA / CLARA programme submission (separate document, not a basis for any claim made here).
- All visa-track and immigration-track correspondence.

The paper stands on **computer-arithmetic content alone**: rule, identity, measurement.

---

## How to build the paper

```bash
cd paper/
pdflatex arith2027_paper.tex
bibtex arith2027_paper      # if a .bib file is added later
pdflatex arith2027_paper.tex
pdflatex arith2027_paper.tex
```

The scaffold is currently a skeleton with `% PLACEHOLDER` comments marking each subsection. Content is filled in iteratively from `gf_preprint-2.pdf` (the 32-page research-note version on arXiv cs.AR) following the page budget in `paper/OUTLINE.md`.

---

## Double-blind discipline

Before every submission iteration, run the checks in `paper/ANONYMISATION_CHECKLIST.md`. The reviewer-facing PDF must contain no author name, no email, no ORCID, no affiliation, no first-person repository identifiers, and no identifying URLs.

A single missed identifier is a desk-reject risk under ARITH double-blind policy.

---

## Honesty contract

Every section of the paper must satisfy the `goldenfloat-ladder` operating rules:

- Claim-status labels [Verified] / [Open] / [Open-conjecture] / [Retracted] visible in body text.
- No banned words: no "breakthrough", "revolutionary", "first-ever", "world-first", "industry-leading", "Nobel".
- ASCII-only headers and body where feasible.
- All raw data, RTL sources, conversion oracles, and synthesis reports published with the supplementary materials at camera-ready.

---

## References to the parent skill ecosystem

- `goldenfloat-ladder` skill — normative rules for claim status, breadth-as-moat, FL-002 ledger discipline.
- `quantization-research-canon` skill — literature canon and SOTA positioning.
- `task-status-board` skill — priority queue including this thread (3-bis).

These are user-side operating rules; they do not appear in the public paper.

---

## License

Source files in this repository are released under MIT (planned, to be confirmed before any external visibility of identifying information). The reviewer-facing PDF is submitted to ARITH 2027 under IEEE copyright terms upon acceptance.

---

## Status

| Milestone | Target | Status |
|---|---|---|
| Submission plan v0.1 | 01 Jun 2026 | Done |
| Paper outline v0.1 | 01 Jun 2026 | Done |
| Anonymisation checklist v0.1 | 01 Jun 2026 | Done |
| Matched-substrate protocol v0.1 | 01 Jun 2026 | Done |
| LaTeX scaffold v0.1 | 01 Jun 2026 | Done |
| Stand up reference RTL builds | 30 Jul 2026 | Pending |
| Testbench harness | 15 Aug 2026 | Pending |
| First synthesis runs | 30 Sep 2026 | Pending |
| Data audit | 15 Oct 2026 | Pending |
| Internal full-paper draft | 30 Nov 2026 | Pending |
| Final reviewer-facing PDF | 15 Jan 2027 | Pending |
| ARITH 2027 submission | ~29 Jan - 5 Feb 2027 | Pending |
