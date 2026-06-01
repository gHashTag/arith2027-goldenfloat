# ARITH 2027 Submission Plan — GoldenFloat

**Document status:** WORKING PLAN, v0.1, 2026-06-01
**Owner:** Dmitrii Vasiliev (admin@t27.ai)
**Source manuscript:** /home/user/workspace/project_canon/gf_preprint-2.pdf (32 pp, v1.7, arXiv preprint, English+ASCII)
**Companion skill:** goldenfloat-ladder (claim-status discipline, FL-002 ledger, breadth-as-moat framing)

---

## 1. ARITH 2027 — what we know, what we assume

### 1.1 Verified facts (as of 2026-06-01)

- ARITH is **annual**, not bi-annual ([ARITH Bylaws, 2025-09-16](https://www.arithsymposium.org/index.php/bylaws/)). [Verified]
- ARITH alternates location: **North American countries in even years, outside in odd years**. ARITH 2027 will therefore be **outside North America**, summer 2027. [Verified — from bylaws]
  - **Correction to goldenfloat-ladder skill:** earlier skill text said "bi-annual" — that is wrong. Update the skill row 3-bis-3 to "annual" and note that ARITH 2027 is the odd-year (outside-North-America) edition.
- ARITH 2026 (33rd edition): Fulda, Germany, 28 June - 1 July 2026. Abstract deadline 23 Jan 2026; paper deadline 30 Jan 2026; decisions 10 Apr 2026. ([Google Groups CFP](https://groups.google.com/g/unum-computing/c/4OSilJ6MusI)) [Verified]
- ARITH 2026 page limits: **8 pages full / 4 pages short** in IEEE CS Conference two-column format, including references. ([ARITH 2026 CFP](https://groups.google.com/g/unum-computing/c/4OSilJ6MusI)) [Verified]
- ARITH 2026 review process: **double-blind**, author names + affiliations + grants must be anonymised. [Verified]
- Submission site: EasyChair (URL will be `easychair.org/conferences/?conf=arith2027`). [Pattern-extrapolated from 2025/2026]
- Review submission allows: **up to 20 pages, 12pt, single column, double spacing** for the reviewer-facing PDF; **final camera-ready must be 8 pages two-column** for full papers. [Verified for 2025/2026, pattern stable]

### 1.2 Working assumptions for ARITH 2027

| Assumption | Source / basis | Confidence |
|---|---|---|
| Annual cadence holds | Bylaws | High |
| ARITH 2027 = odd-year, outside North America | Bylaws | High |
| Symposium dates: June-July 2027 | Pattern (2023 Sep, 2024 Sep, 2025 May, 2026 Jun-Jul) | Medium |
| Abstract deadline: **~22-29 Jan 2027** | Pattern from 2025 (Dec 13, 2024) and 2026 (Jan 23, 2026) | Medium-high |
| Paper deadline: **~29 Jan - 5 Feb 2027** | Pattern from 2025 (Dec 23, 2024) and 2026 (Jan 30, 2026) | Medium-high |
| Decision notification: **~10 Apr 2027** | Pattern from 2026 | Medium |
| Page limit and format identical to 2025/2026 | Format stable since 2017 | High |
| Double-blind review continues | Stable policy since at least 2023 | High |

**Practical deadline target:** finish camera-ready-quality submission by **15 Jan 2027** to leave a 2-week safety margin. Working clock: ~7.5 months from today (01 Jun 2026).

### 1.3 Open questions to resolve as soon as `arith2027.arithsymposium.org` goes live

1. Exact location (likely Europe — France / UK / Italy / Spain candidates given Florent de Dinechin INSA Lyon was a 2017 chair and the European posit/takum community is active).
2. Program chairs.
3. Exact dates and EasyChair submission link.
4. Whether the Emerging Topics in Computing special section partnership (used in 2023) returns.
5. Tutorial day / workshop options that might suit a short-paper variant.

### 1.4 Action when site goes live

Set a monitoring check (cron or manual weekly) on `arithsymposium.org` and `arith2027.arithsymposium.org` starting **September 2026**. The CFP for the next edition is historically posted September-October of the year before the symposium.

---

## 2. What we have now and what ARITH wants

### 2.1 Current preprint (`gf_preprint-2.pdf` v1.7)

- 32 pages, single column, Author = "Perplexity Computer" (metadata), single author Dmitrii Vasiliev.
- Structure: Abstract, §1 Introduction + "What This Note Does Not Claim" (10 anti-claims), §2 Ladder rule + look-elsewhere correction, §3 GRE multiplier-free anchor, §4 Lucas-exact identity, §5 Hardware (per-width status, FPGA GF16 result, software BPB experiment, CLARA methodology paragraph, multi-language code-gen Table 3, 77-format SSOT catalog), §6 Prior art, §7 Pre-registration of open hypotheses, §8 FL-002 falsification ledger, Appendices A-E.
- Tone: research note, conservative, claim-status labelled. Strong on epistemic discipline, weak on conventional "results table" framing that ARITH reviewers expect.
- Already cites Daubechies IEEE TIT 2010, Gustafson SFI 2017, Hunhold ARITH 2025 (takum), OCP-MX 2023, Lucas 1878, Binet — the core ARITH literature.

### 2.2 ARITH-2027 8-page full-paper requirements (from 2025/2026 CFPs)

- **8 pages two-column IEEE CS Conference**, including references. **No extra pages.**
- **Double-blind**: author names, affiliations, grants, self-references must be removed or anonymised.
- **In scope topics** (from 2025 CFP, all directly relevant to GF):
  - Arithmetic foundations, systems and formats
  - Theory of computer arithmetic (integer, fixed/floating-point, interval, finite-field)
  - Novel arithmetic systems and application-specific number formats
  - Implementation of arithmetic (FPGA, optical, quantum included)
  - Design tools and methodologies, including testing and formal verification
  - AI/ML and signal processing applications

GoldenFloat hits four of these slots directly.

### 2.3 The page-budget gap

From 32 single-column pages (~12-14k words) to 8 two-column pages (~6-7k words including references and figures). Compression ratio ~4-5x. This forces ruthless cuts. Most of the "what this is not" anti-claim list, the FL-002 ledger, the appendices, and the 77-format catalog have to be **deferred to supplementary material or to the arXiv version**, not in the ARITH paper.

---

## 3. Strategic decision: full vs short paper

### 3.1 Full paper (8 pages) — recommended

**Pros:**
- The ladder rule + GRE anchor + Lucas identity + GF16 FPGA 323 MHz result is a coherent "rule + identity + measurement" story that fills 8 pages cleanly.
- Double-blind format does not penalise an independent researcher — affiliation is hidden from reviewers anyway.
- Takum (Hunhold ARITH 2025) is the closest live alternative and is itself an 8-page ARITH paper — direct comparable.
- An ARITH 2027 full paper would be the strongest single peer-reviewed credential for the GF work to date.

**Cons:**
- Requires real ablation results vs posit / takum at matched substrate. Current preprint has the **GF16 323 MHz FPGA bitstream** [Verified] but no comparable matched-substrate posit/takum number. Section 5.3 explicitly flags the substrate-confound problem.
- Without at least one matched-substrate head-to-head on a controlled benchmark, the ARITH reviewers' "what's new" question is harder to answer.

### 3.2 Short paper (4 pages) — fallback

**Pros:**
- Lower bar for novelty — short papers are explicitly for "work-in-progress ideas, interim results, or industry applications" (ARITH 2023 CFP).
- The "rule + identity" core + the GF16 FPGA result fits 4 pages comfortably.
- Industry-track route avoids the matched-substrate head-to-head requirement.

**Cons:**
- Shorter slot, less visibility.
- Less weight for EB-1A Criterion 6 (scholarly authorship).
- ARITH full papers are more cited.

### 3.3 Recommendation

**Aim full paper. Hold short paper as fallback if we cannot stage one matched-substrate head-to-head against posit or takum by Dec 2026.**

The gating experiment is described below in §5.

---

## 4. Eight-page paper outline (full-paper target)

Two columns, IEEE CS Conference, including references.

| Section | Working title | Page budget | Content |
|---|---|---|---|
| Abstract | (existing abstract, trimmed) | 0.25 pg | Rule + identity + measurement, ~200 words |
| §1 | Introduction | 0.75 pg | Context (posit, takum, MX, LNS), the three-word contribution (rule, identity, measurement), explicit non-claims (one paragraph, condensed from current §1.1) |
| §2 | Ladder rule and look-elsewhere correction | 1.5 pg | Definition (eq. 1), Table 1 (12 widths), look-elsewhere correction (83-of-80000 result, Bonferroni, Bayes factor, narrowing with 12 formats). This is the "negative result first" honesty signature — strong reviewer signal. |
| §3 | GRE multiplier-free anchor | 0.75 pg | Daubechies IEEE TIT 2010 result, what it does and does not establish, the narrow defensible link. |
| §4 | Lucas-exact integer identity | 0.75 pg | Equation 2, classical provenance (Lucas 1878, Binet), application to GoldenFloat bias derivation, 500-digit numerical verification statement. Honest attribution. |
| §5 | Hardware status and the matched-substrate experiment | 2.0 pg | Per-width status table (compressed from current §5.2), GF16 323 MHz Artix-7 result [Verified], substrate-confound statement, **matched-substrate FPGA experiment** (Appendix D in preprint, pre-registered head-to-head GF16 vs posit-16 vs takum-16) — describe the protocol and report results if measured by submission. |
| §6 | Prior art and positioning | 0.5 pg | Posit, takum, OCP-MX, LNS as precedents and allies. Takum as closest live alternative. No accuracy or superiority claim. |
| §7 | Discussion: breadth-as-moat | 0.5 pg | Toolchain-coherence framing (one rule, 12 widths, multi-language codegen). Honest moat framing per goldenfloat-ladder skill: breadth, not per-rung superiority. |
| §8 | Conclusions and falsification path | 0.25 pg | FL-002 ledger pointer, F1/F2/F3 falsification protocol, what would change the conclusion. |
| References | (compressed) | 0.75 pg | 15-20 references, IEEE format |

**Total: 8.0 pages.**

**Cut from current preprint (move to arXiv version + supplementary material):**

- The 10-item "What This Note Does Not Claim" list → one short paragraph in §1.
- §5.6 CLARA-style assurance methodology → cut entirely (anonymisation risk + space).
- §5.7 Multi-language code-gen Table 3 → compressed to one sentence in §5.
- §5.8 77-format SSOT catalog → one sentence pointer to companion artefact.
- §7 Pre-registration of open hypotheses → cut, one-sentence pointer.
- §8 FL-002 ledger → one paragraph in §8.
- Appendices A-E → not in ARITH version. Available in arXiv version.

---

## 5. The gating experiment for a full-paper submission

ARITH reviewers expect a measurement. Current preprint has one [Verified] FPGA measurement (GF16 35-of-35 testbench at 323 MHz on Artix-7) but no head-to-head against a competing format on the same substrate. To make the full paper compelling, we need one matched-substrate measurement before submission.

### 5.1 Pre-registered experiment (from Appendix D of preprint)

**Protocol:** GF16 vs posit-16 vs takum-16 vs binary16 (IEEE 754), all four implemented as RTL on the same Artix-7 FPGA. Same testbench (e.g., a fixed 1k-vector dot product, or a quadratic-form evaluator). Report: cycles per op, area in LUTs + FFs, max clock frequency post-PAR, and accuracy (BPB or RMSE) on a fixed evaluation set.

**Outcome interpretation:**
- If GF16 wins on any axis at matched substrate: strong ARITH result, full paper viable.
- If GF16 ties: still publishable (a new viable point in the design space).
- If GF16 loses on all axes: report it honestly, frame as breadth-via-toolchain-coherence (the F-ladder is the contribution, not the per-rung win), or fall back to short paper.

### 5.2 Tooling already in place

- GF16 Verilog RTL: in `gHashTag/t27`.
- Artix-7 board access: confirmed (323 MHz measurement on hand).
- Reference RTL for posit-16: PERCIVAL / Big-PERCIVAL (Mallasen UCM Madrid, GitHub open-source).
- Reference RTL for takum-16: Hunhold's open-source repo accompanying arXiv:2412.20273.
- Reference RTL for binary16: any open IEEE 754 FP16 implementation (e.g., FloPoCo).

### 5.3 Experiment timeline

- **Jun-Jul 2026:** Stand up the four RTL implementations side-by-side. Standardise the testbench.
- **Aug-Sep 2026:** Run on the same Artix-7 board. Collect data with paired seeds for accuracy comparison.
- **Oct 2026:** Analyse, write up Section 5 of the ARITH paper.
- **Nov-Dec 2026:** Iterate based on internal review.
- **15 Jan 2027:** Submit (assuming pattern-extrapolated deadline ~29 Jan 2027).

---

## 6. Anti-bundling and conflict-of-interest discipline

### 6.1 vs the arXiv preprint

- The arXiv preprint (32 pp v1.7) is **not** "under review elsewhere" in the ARITH sense — arXiv preprints are explicitly permitted.
- The ARITH 8-page version must materially extend the preprint with the matched-substrate experiment of §5. A pure compression is acceptable but weak; an extension is what reviewers want.

### 6.2 vs Foundations of Physics

- Completely separate work, no scientific overlap. No bundling risk.

### 6.3 vs IGLA RACE / TRIOS

- Same author, different repositories, different scientific questions. Cite as related work where relevant (the IGLA gardener-harvest negative result on phi-as-optimiser is interesting context but **out of scope** for the ARITH paper; mention only in passing if at all).

### 6.4 Author list

- **Sole author** for the ARITH submission: Dmitrii Vasiliev.
- Anonymisation removes name from the reviewer-facing PDF (per double-blind policy).
- Camera-ready (if accepted) restores name + email + affiliation "Independent Researcher, Ko Samui, Thailand".

---

## 7. Anonymisation checklist (double-blind compliance)

Items in the current preprint that **must be redacted or rephrased** before submission:

### 7.1 Author identity
- Author name on title page → "Anonymous submission to ARITH 2027".
- Email `admin@t27.ai` → remove.
- ORCID `0009-0008-4294-6159` → remove (ORCID is identifying).
- Affiliation "Independent researcher, Ko Samui, Thailand" → remove.

### 7.2 Repository and artefact references
- `gHashTag/t27` → replace with neutral placeholder `[Repository A]`.
- `gHashTag/tt-trinity-gamma` → `[Repository B]`.
- `gHashTag/trinity-clara` → cut (CLARA methodology paragraph is removed entirely).
- `gHashTag/trios-trainer-igla` → not currently in preprint, do not add.
- All GitHub URLs → remove or replace with `[anonymised URL]`.
- Zenodo DOI `10.5281/zenodo.19227877` → remove (linking to author).
- `pellis_vasilev_letter` references → remove (different paper, different authorship; mentioning it links to user).

### 7.3 Self-citations
- Any cite of an author's own prior work → cite it as "[Author1, 2026]" or "Anonymous, in preparation".
- The arXiv preprint version of this paper → cite as "an extended technical note by the authors, currently in preparation" without the arXiv ID.

### 7.4 Specific identifying claims to soften
- "Independent researcher" framing → neutralise to passive voice where possible.
- Tiny Tapeout TTSKY26b submission with the gHashTag username → de-identify the shuttle ID and username.
- Geography "Ko Samui, Thailand" → remove from all metadata and text.
- The IGLA gardener-harvest negative result on phi-as-optimiser (preprint §1.1 anti-claim 8) → cut, it links to a separate author repository.
- Any DARPA / CLARA reference → cut entirely (preprint §5.6 — both anonymisation risk and a topic ARITH reviewers will not consider relevant).

### 7.5 Metadata
- PDF Author field → set to "Anonymous" or blank.
- PDF Title → "ARITH 2027 Submission" (no project name).
- PDF Producer → leave as the LaTeX compiler default.
- Camera-ready (if accepted): metadata Author = "Perplexity Computer" (current preprint convention) OR "Dmitrii Vasiliev" (depending on which is the user's preference at that time).

---

## 8. License and prior-publication compliance

### 8.1 ARITH policy
- "Papers under review elsewhere are not acceptable for submission to ARITH 2027" (CFP).
- arXiv preprints are explicitly permitted (industry standard).

### 8.2 arXiv license already chosen for `gf_preprint-2.pdf`
- **arXiv non-exclusive license** (chosen during Submit Step Add License on 2026-06-01).
- This preserves the option to submit to IEEE venues including ARITH proceedings + IEEE Transactions on Computers + IEEE Trans. Emerging Topics in Computing.
- CC BY would have blocked the IEEE route; non-exclusive does not.

### 8.3 IEEE copyright at acceptance
- Standard IEEE Copyright Form signed at camera-ready.
- ARITH 2026 partnered with IEEE Transactions on Emerging Topics in Computing for a special section (per 2023 CFP). Watch for whether ARITH 2027 does the same — could be a path for an extended journal version.

---

## 9. Submission packet — file list

When 15 Jan 2027 arrives, the packet that needs to be ready:

| File | Purpose | Source / status |
|---|---|---|
| `arith2027_paper.tex` | LaTeX source, IEEEtran conference class, two-column | NEW — build from `gf_preprint-2.pdf` source if available |
| `arith2027_paper.pdf` | Camera-ready 8-page PDF, anonymised | Compiled from .tex |
| `arith2027_supplementary.zip` (optional) | Verilog RTL, conformance vectors, replication scripts | Curated subset of `gHashTag/t27` |
| `arith2027_anonymisation_audit.md` | Internal record of every redaction | NEW — to be built |
| EasyChair metadata | Title, abstract, keywords, topic categories | NEW |

If we do not have the LaTeX source of `gf_preprint-2.pdf` in the workspace, the first prep task is recovering or reconstructing the .tex file from the PDF (or rewriting in IEEEtran from scratch — this is actually fine because the paper structure changes significantly in compression).

---

## 10. Risk register

| Risk | Likelihood | Impact | Mitigation |
|---|---|---|---|
| arXiv endorsement fails or delays | Medium | Low for ARITH (arXiv is optional for ARITH) | ARITH submission does not depend on arXiv being live |
| Matched-substrate experiment yields a negative GF result | Medium | Medium | Fall back to short-paper format; honest reporting is consistent with skill discipline |
| ARITH 2027 site does not post CFP until Nov-Dec 2026 | Medium-high | Low | Working timeline already assumes a Jan 2027 deadline |
| Double-blind anonymisation leaks identity through repo references | High if not careful | High (desk reject) | Run `arith2027_anonymisation_checklist.md` before every submission iteration |
| RTL parity bug surfaces between GF16 and the reference implementations | Medium | Medium | Replay the train/val mismatch lesson from preprint §5.5: log every cross-format conversion, audit before any comparative claim |
| Authorship dispute (e.g. Pellis interested in being added) | Low | Medium | GF paper is sole-author by design (computer arithmetic content, no Pellis contribution); phi-paper authorship is entirely separate |
| Travel feasibility for in-person presentation (Russian passport in Europe in summer 2027) | High | Low for submission, Medium for camera-ready | Most ARITH editions allow virtual presentation; check ARITH 2027 specific policy when announced |

---

## 11. What the user has to decide first

| Decision | Default if no explicit answer | When it matters |
|---|---|---|
| Full paper or short paper | Full paper; switch to short if no matched-substrate experiment by Dec 2026 | Q4 2026 |
| Sole author or invite Pellis/Olsen | Sole author (no Pellis/Olsen contribution to GF content) | Now |
| Re-use existing .tex source if available, or rewrite in IEEEtran | Rewrite in IEEEtran (8-page format is structurally different) | Jul-Aug 2026 |
| Run the matched-substrate experiment in-house or contract to a third party | In-house, using existing Artix-7 access | Jul 2026 |
| Submit a supplementary materials zip | Yes, with RTL + conformance vectors | Jan 2027 |
| arXiv version timing | arXiv-post AFTER ARITH submission, not before (avoids identity leak during double-blind review) | Jan-Feb 2027 |

---

## 12. Immediate next sub-tasks (next 30 days)

In priority order:

1. **Confirm whether the .tex source of `gf_preprint-2.pdf` exists** in any workspace or repo. If yes, fork it. If no, schedule a one-day session to set up IEEEtran scaffolding for the 8-page version.
2. **Set up the matched-substrate experiment workspace**: clone PERCIVAL (posit-16), takum (Hunhold), and a binary16 reference into a sibling directory of the GF16 RTL. Standardise the testbench harness.
3. **Build `arith2027_paper_outline.md`** — section-by-section content allocation with word counts.
4. **Build `arith2027_anonymisation_checklist.md`** — operational redaction list, to be run before every submission iteration.
5. **Update `goldenfloat-ladder` skill** to correct the bi-annual / annual confusion and to add an explicit ARITH 2027 target window.
6. **Monitor `arithsymposium.org`** for the ARITH 2027 announcement (likely Sep-Oct 2026).

---

## 13. Honesty and claim-status discipline (carry from skill)

Per `goldenfloat-ladder` skill:

- No claim of per-rung superiority over posit / takum / MX / LNS.
- No claim of base uniqueness for phi.
- No claim of silicon validation (no die has returned).
- The breadth-as-moat claim stays **[Open-conjecture]** with the F1/F2/F3 falsification path.
- "What This Note Does Not Claim" survives into the ARITH paper as a condensed paragraph in §1.
- Takum is "the closest live alternative" — cite Hunhold ARITH 2025 explicitly and treat as ally, not competitor.

---

## 14. References (already in preprint, retain for ARITH version)

Core ARITH-relevant literature already cited in `gf_preprint-2.pdf` v1.7:

- Daubechies, I., Gunturk, C. S., Wang, Y., Yilmaz, O. "The Golden Ratio Encoder", IEEE Transactions on Information Theory 56(10):5097-5110, 2010. arXiv:0809.1257.
- Gustafson, J. L., Yonemoto, I. "Beating Floating Point at its Own Game: Posit Arithmetic", Supercomputing Frontiers and Innovations 4(2), 2017.
- Hunhold, L. "Takum Arithmetic: A Tapered Floating-Point Format", arXiv:2412.20273, 2024.
- Hunhold, L., Gustafson, J. L. "Numerical analysis of FFT using takum arithmetic", arXiv:2504.21197, 2025.
- Hunhold, L., Gustafson, J. L. "An Arnoldi-style method for takum arithmetic", arXiv:2504.21130, 2025.
- Rouhani, B. et al. "Microscaling Data Formats for Deep Learning", OCP MX White Paper, 2023.
- Mallasen, R. M., et al. "PERCIVAL: Open-Source Posit RISC-V Core with Quire Capability", IEEE Trans. Emerging Topics in Computing.
- Lucas, E. "Théorie des fonctions numériques simplement périodiques", American Journal of Mathematics 1, 1878.

---

**End of plan v0.1.** Update freely; new versions overwrite this file with the same `name` parameter when shared.
