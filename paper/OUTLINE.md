# ARITH 2027 Paper Outline — 8-page IEEE CS Conference

**Status:** v0.1, 2026-06-01
**Target:** 8 pages two-column IEEE CS Conference format, double-blind
**Source manuscript:** `gf_preprint-2.pdf` v1.7 (32 pp single-column research note)
**Working title (anonymised):** "A Phi-Derived Static-Split Floating-Point Family from GF4 to GF256 with a Lucas-Exact Integer Identity"

---

## Page budget

Total: 8 pages including references. ARITH 2026 CFP: no extra pages.

| Block | Pages | Words (target, ~700 wpp two-col) |
|---|---|---|
| Title + Abstract + Keywords | 0.25 | ~175 |
| §1 Introduction | 0.75 | ~525 |
| §2 The ladder rule + look-elsewhere correction | 1.5 | ~1050 |
| §3 GRE multiplier-free anchor | 0.75 | ~525 |
| §4 Lucas-exact integer identity | 0.75 | ~525 |
| §5 Hardware status + matched-substrate experiment | 2.0 | ~1400 |
| §6 Prior art and positioning | 0.5 | ~350 |
| §7 Discussion: breadth-as-moat | 0.5 | ~350 |
| §8 Conclusions + falsification path | 0.25 | ~175 |
| References | 0.75 | 15-20 refs in IEEE format |
| **Total** | **8.0** | **~5075 + refs** |

---

## Title page

```
A Phi-Derived Static-Split Floating-Point Family
from GF4 to GF256 with a Lucas-Exact Integer Identity

Anonymous Submission
ARITH 2027 — Double-Blind Review
```

No author name, no email, no affiliation, no ORCID, no acknowledgements until camera-ready.

## Abstract (~175 words, ~5-7 sentences)

Single paragraph, IEEE conference style. Three-word contribution structure preserved.

**Draft:**

> We describe GoldenFloat (GF), a family of floating-point formats whose exponent:mantissa split is generated, for each total width N, by a single closed rule e = round((N-1)/phi^2) with mantissa m = N-1-e, where phi = (1+sqrt(5))/2. The rule reproduces the realised exponent widths of nine GF formats (GF4 through GF256) exactly and extends consistently to eight further rule-derived rungs: GF6, GF10, GF14, GF48, GF96, GF128 (no returned silicon) and GF512, GF1024 (bias 2^194-1, 2^390-1; exceeds u128 ROM record field, tracked symbolically). We verify a classical integer identity, phi^(2n) + phi^(-2n) = L_(2n) (Lucas numbers), symbolically for n = 1..256 and numerically at 500 decimal places. We report one hardware artefact: a GF16 codec on Artix-7 FPGA passing a 35-of-35 testbench at 323 MHz, and report a matched-substrate head-to-head experiment against posit-16, takum-16, and binary16 on the same board. We are explicit about non-claims: phi is not a uniqueness claim, no GF rung is claimed to outperform posit, takum, MX, or LNS at matched substrate, and no silicon has been validated.

**Keywords:** computer arithmetic, floating-point formats, golden ratio, Lucas numbers, FPGA, double-blind submission

---

## §1 Introduction (~525 words, 0.75 pg)

### §1.1 Motivation paragraph (~150 words)

Compress the current §1 intro: numerical formats have diversified beyond IEEE 754; posit (Gustafson-Yonemoto 2017) introduced regime-plus-exponent encoding; takum (Hunhold ARITH 2025) refined this with a tapered rule uniform across widths; OCP MX (Rouhani et al. 2023) standardised block-scaled 4/6/8-bit types; LNS trades exact multiplication for approximate addition. These are prior art and allies.

### §1.2 The three-word contribution (~200 words)

State the contribution: *a rule, an identity, and a measurement*.

- **Rule.** e = round((N-1)/phi^2), m = N-1-e. Reproduces 9 realised widths [Verified]; extends to 8 further rule-derived rungs GF6, GF10, GF14, GF48, GF96, GF128 [Conj] and GF512, GF1024 [Conj, bias > u128, symbolic].
- **Identity.** phi^(2n) + phi^(-2n) = L_(2n), Lucas (1878) attribution explicit. Motivates integer-backed accumulation. We do not claim authorship of the identity.
- **Measurement.** GF16 codec at 323 MHz on Artix-7 [Verified] plus a matched-substrate head-to-head (Section 5).

### §1.3 What this paper does not claim (~175 words)

Condensed from the 10-item anti-claim list of the preprint. Keep the four most reviewer-relevant items, fold the rest into footnotes or cut:

1. Phi is not claimed unique among algebraic bases.
2. No per-rung superiority over posit / takum / MX / LNS at matched substrate.
3. No silicon validation — no die has returned.
4. The breadth-as-moat hypothesis is **[Open-conjecture]** with an explicit falsification path (Section 8).

Cut from the preprint anti-claim list for the ARITH paper:
- TTSKY26b multiplier correctness (too project-specific)
- phi-as-optimiser falsification (different repository, anonymisation risk)
- CLARA-style methodology (anonymisation risk + irrelevant to ARITH)
- Originality of the Lucas identity (stays as a sentence in §4)

---

## §2 The ladder rule and look-elsewhere correction (~1050 words, 1.5 pg)

### §2.1 Definition (~250 words)

Direct lift of preprint §2.1 (Equation 1, the phi^2 = phi+1 derivation, convergence as N→∞).

Include **Table 1** (12-format ladder, N / e / m / (N-1)/phi^2 / e/(N-1)). Two-column friendly — fits in a half-column textbox.

### §2.2 Retraction of "2-to-256" wording (~100 words)

Direct lift of preprint §2.2. Signals epistemic discipline to reviewers.

### §2.3 Look-elsewhere correction (~500 words)

Full preprint §2.3 — *negative result first*, the 83-of-80000 rational search, family-wise probability ≈ 7.1×10^-3, Bonferroni saturation at 1, Bayes factor 964 with the structural caveat, narrowing from 392 to 47 ratios when extending to 12 formats. **This is the strongest reviewer-signal section** — preserve in full. NOTE: 17-format narrowing is OPEN (claim-audit-lab CASE-09); do not cite a 17-format figure until that case closes.

### §2.4 Rounding mode (~100 words)

Half-sentence in body + the footnote from preprint §2.4 explaining that the choice is immaterial for all nine verified widths because the raw value is never a half-integer.

### §2.5 Compression cut

- Equation derivation length: condense from 4 paragraphs to 2.
- The mpmath 200-digit precision statement: one sentence with a reference to supplementary material.

---

## §3 GRE multiplier-free anchor (~525 words, 0.75 pg)

Direct lift of preprint §3 with minor compression:

- **Anchor statement** (~150 words): Daubechies et al. IEEE TIT 2010 result + the multiplier-free property derived from phi^2 = phi+1.
- **No claim base is forced** (~150 words): explicit non-claim that phi is unique.
- **No point-robustness at beta = phi** (~150 words): Daubechies Theorem 8 caveat, no conflation with Ward 2008.
- **Conclusion paragraph** (~75 words): the narrow, defensible link.

**No cuts needed** — this section is already compact.

---

## §4 Lucas-exact integer identity (~525 words, 0.75 pg)

Direct lift of preprint §4 with these adjustments:

- **§4.1 Statement and classical provenance** (~250 words): Equation 2, Lucas L_(2n) attribution, Binet formula. Keep the explicit "we do not claim authorship".
- **§4.2 Numerical verification** (~150 words): symbolic verification for n = 1..256 + 500-digit mpmath numerical check.
- **§4.3 Application to GF** (~125 words): the bias derivation that uses the identity, with the integer-accumulator description (and the non-claim that the hardware accumulator exists).

**Cut:** the lengthy derivation chain — move to supplementary material.

---

## §5 Hardware status and matched-substrate experiment (~1400 words, 2.0 pg)

**This is the section that materially extends the preprint and makes the ARITH paper viable.**

### §5.1 Per-width status (~300 words)

Compressed version of preprint §5.2. **Table 2** (compact per-width readiness ladder): GF4/8/12/16/20/24/32 generated end-to-end (.t27 spec + C + Verilog + JSON vectors); GF16 has FPGA bitstream; GF64/128/256 are partial or sibling-repo.

### §5.2 The GF16 result (~250 words)

Direct lift of preprint result: GF16 codec passing 35-of-35 testbench at 323 MHz on Artix-7 after one-line rounding fix. [Verified].

### §5.3 The substrate-confound problem (~150 words)

Why software BPB measurements are insufficient on their own (preprint §5.3 compressed). Sets up §5.4 as the resolution.

### §5.4 Matched-substrate head-to-head experiment (~500 words) — **NEW for ARITH**

Pre-registered protocol (preprint Appendix D, brought into the main body):

- **Setup:** GF16, posit-16 (PERCIVAL reference, Mallasen UCM), takum-16 (Hunhold reference), binary16 (FloPoCo or equivalent). Same Artix-7 board, same testbench harness, same evaluation set.
- **Testbench:** fixed 1k-vector dot product + a quadratic-form evaluator + a small Newton-Raphson iteration on a known function.
- **Metrics:** cycles per op, LUT count, FF count, max clock frequency post-PAR, accuracy (RMSE on a fixed corpus, BPB on a small language-model proxy).
- **Pre-registered stop conditions:** report all four, no selective reporting. Include negative results.
- **Results (if available by submission):** Table 3 with all four formats side-by-side.
- **Result-not-yet-available fallback:** present as pre-registered protocol with the testbench code in supplementary material; reviewer feedback on the protocol is itself a contribution.

### §5.5 Implications (~200 words)

How the matched-substrate result (or its pre-registration) resolves the substrate-confound. Whether the breadth-as-moat hypothesis stays [Open-conjecture] or moves to [Verified] / [Falsified] depending on the data.

### §5.6 Cuts from preprint

- §5.6 CLARA-style assurance methodology → **cut entirely** (anonymisation risk).
- §5.7 Multi-language code-gen Table → one-sentence pointer to supplementary materials.
- §5.8 77-format SSOT catalog → one-sentence pointer.

---

## §6 Prior art and positioning (~350 words, 0.5 pg)

Compressed from preprint §6:

- **Posit** (Gustafson-Yonemoto 2017) — regime-plus-exponent encoding, adaptive precision.
- **Takum** (Hunhold ARITH 2025) — tapered rule uniform across widths, **closest live alternative** with peer-reviewed multi-width hardware.
- **OCP MX** (Rouhani et al. 2023) — block-scaled 4/6/8-bit microscaling.
- **LNS** — logarithmic number systems, exact multiplication, approximate addition.
- **GoldenFloat positioning** — different point in design space: static split, single closed rule keyed to phi, spans a 17-rung ladder GF4 to GF1024 (9 with returned silicon/RTL, 6 rule-derived without silicon, 2 symbolic-bias extensions).

Explicit: no accuracy or superiority claim over any of them. Treat as precedents and allies.

---

## §7 Discussion: breadth-as-moat (~350 words, 0.5 pg)

Honest moat framing per `goldenfloat-ladder` skill:

- **What the moat is:** breadth (one rule covers GF4 through GF1024, 17 rungs total) and toolchain coherence (one .t27 spec → C / Verilog / JSON conformance vectors from a single source of truth, seven widths end-to-end).
- **What the moat is not:** per-rung superiority; phi being unique among bases; per-rung accuracy claim.
- **Falsification path:** F1 (arithmetic correctness — already [Verified] 9/9), F2 (matched-substrate per-rung — §5.4 protocol), F3 (multi-rung composition — open).
- **Status:** **[Open-conjecture]** with the F1/F2/F3 protocol.

---

## §8 Conclusions and falsification path (~175 words, 0.25 pg)

Short close:
1. Restate the rule, identity, measurement contributions.
2. Restate the non-claims.
3. Point to FL-002 ledger (supplementary material) and the F1/F2/F3 protocol.
4. One sentence on next steps: matched-substrate experiment completion, multi-width ablation at fixed budget, silicon validation pending Tiny Tapeout returns.

---

## References (~0.75 pg, 15-20 refs in IEEE format)

Curated from preprint's 24-reference set. Drop the references that are tangential (CLARA, gardener-harvest negative result repos, IGLA internal docs) for anonymisation reasons. Keep:

1. Daubechies, Gunturk, Wang, Yilmaz. "The Golden Ratio Encoder." IEEE Transactions on Information Theory, 56(10):5097-5110, 2010.
2. Gustafson, Yonemoto. "Beating Floating Point at its Own Game: Posit Arithmetic." Supercomputing Frontiers and Innovations, 4(2), 2017.
3. Hunhold. "Takum Arithmetic: A Tapered Floating-Point Format." arXiv:2412.20273, 2024.
4. Hunhold, Gustafson. "Numerical analysis of FFT using takum arithmetic." arXiv:2504.21197, 2025.
5. Hunhold, Gustafson. "An Arnoldi-style method for takum arithmetic." arXiv:2504.21130, 2025.
6. Rouhani et al. "Microscaling Data Formats for Deep Learning." OCP MX White Paper, 2023.
7. Mallasen et al. "PERCIVAL: Open-Source Posit RISC-V Core with Quire Capability." IEEE Trans. Emerging Topics in Computing.
8. Lucas. "Théorie des fonctions numériques simplement périodiques." American Journal of Mathematics, 1, 1878.
9. Binet (classical attribution for the Lucas numbers formula).
10. IEEE 754-2019 standard.
11. Ahlbach, Usatine, Pippenger. "Efficient Algorithms for Zeckendorf Arithmetic." (cited in preprint).
12. de Dinechin et al. — a posit or floating-point hardware reference relevant to FloPoCo.
13. Microsoft / NVIDIA OCP MX implementation papers (one or two).
14. BitNet (if relevant to the BPB experiment framing).
15. Scaling laws reference (Hoffmann et al. "Chinchilla" 2022) — only if cited in the BPB framing.

**Drop from preprint reference list:** any self-references to gHashTag repos; any reference to Pellis-Vasilev-Olsen phi-paper; any DARPA / CLARA citation.

---

## Word-budget summary

| Section | Words | Pages (two-col, ~700 wpp) |
|---|---|---|
| Title + Abstract + Keywords | ~175 | 0.25 |
| §1 Introduction | ~525 | 0.75 |
| §2 Ladder rule + look-elsewhere | ~1050 | 1.5 |
| §3 GRE anchor | ~525 | 0.75 |
| §4 Lucas identity | ~525 | 0.75 |
| §5 Hardware + matched-substrate | ~1400 | 2.0 |
| §6 Prior art | ~350 | 0.5 |
| §7 Discussion | ~350 | 0.5 |
| §8 Conclusions | ~175 | 0.25 |
| References (15-20 refs) | — | 0.75 |
| **Total** | **~5075 words** | **8.0 pages** |

---

## Honesty discipline (carry from skill)

Every section above must satisfy `goldenfloat-ladder` skill rules:
- Claim-status labels [Verified] / [Open] / [Open-conjecture] / [Retracted] visible in body text.
- Breadth-as-moat is **[Open-conjecture]** with explicit F1/F2/F3 path.
- Takum cited as the **closest live alternative**, not a defeated competitor.
- No banned words: no "breakthrough", "revolutionary", "first-ever", "world-first", "industry-leading", "Nobel".
- No DARPA / CLARA references (anonymisation + irrelevance).
- ASCII-only headers and body where feasible.

---

**End of outline v0.1.**
