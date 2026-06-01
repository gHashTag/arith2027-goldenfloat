# ARITH 2027 Anonymisation Checklist

**Status:** v0.1, 2026-06-01
**Purpose:** Operational redaction list. Run this checklist before EVERY submission iteration (initial submission + every revision). ARITH 2027 review is **double-blind** — a single missed identifier is a desk-reject risk.

**Apply to:** the reviewer-facing PDF, all supplementary materials, and any URL that would resolve to author identity (GitHub, ORCID, personal site, Zenodo).

---

## 0. Hard rule

If in doubt, **redact**. A reviewer-facing PDF that is over-anonymised is recoverable at camera-ready; a leaked identity is not recoverable in the review cycle.

---

## 1. Identifying metadata (PDF level)

| Field | Action | Tool |
|---|---|---|
| PDF Author | Set to "Anonymous" or blank | `exiftool -Author= -Title="ARITH 2027 Submission" file.pdf` |
| PDF Title | Set to "ARITH 2027 Submission" or the paper title (no project name) | `exiftool` |
| PDF Subject | Blank or generic | `exiftool` |
| PDF Producer | Leave as LaTeX/pdfTeX default (revealing this is acceptable) | — |
| PDF Creator | Leave as LaTeX/pdfTeX default | — |
| PDF Keywords | Keep technical keywords only, no project names | `exiftool` |
| XMP metadata | Strip with `exiftool -all=` then add back only neutral fields | `exiftool` |
| Embedded comments / annotations | Remove all | `qpdf --remove-attachments`, manual review |
| Embedded fonts | Subset, no font-name leak | — |

**Verification command after redaction:**
```bash
exiftool reviewer_facing.pdf | grep -i -E "author|creator|title|subject|comments|keywords"
```
Should show no identifying string.

---

## 2. Identifying text content (manuscript body)

### 2.1 Author identity

| Item | Where to redact | Replace with |
|---|---|---|
| "Dmitrii Vasiliev" | Title page, acknowledgements, any footnote | "Anonymous Submission" |
| "Dmitrii Vasilev" (alt spelling) | Anywhere | Remove |
| "vibee_dev" (arXiv username) | Anywhere | Remove |
| `admin@t27.ai` | Title page, footnotes | Remove |
| `reactnativeinitru@gmail.com` | Anywhere | Remove |
| ORCID `0009-0008-4294-6159` | Title page, any cite | Remove |
| "Independent researcher, Ko Samui, Thailand" | Title page, body | Remove |
| "Ko Samui" / "Surat Thani" / "Thailand" | Body, footnotes | Remove or replace with neutral "the author's location" |
| "Russia" / "Russian Federation" (if cited as author nationality) | Body | Remove |
| "Perplexity Computer" (current PDF Author metadata) | PDF metadata | Replace with "Anonymous" |

### 2.2 Repository identifiers

| Item | Where | Replace with |
|---|---|---|
| `gHashTag/t27` | Body, captions, references | `[Repository A]` |
| `gHashTag/tt-trinity-gamma` | Body, §5.4 erratum reference | `[Repository B]` |
| `gHashTag/trinity-clara` | Body §5.6 | **Cut entire §5.6 paragraph** |
| `gHashTag/trios-trainer-igla` | If anywhere | Remove |
| `gHashTag/trios-mcp-rag` | If anywhere | Remove |
| `gHashTag/arith2027-goldenfloat` | If anywhere | Remove |
| Any `github.com/gHashTag/...` URL | Body, references, footnotes | Replace with `[anonymised URL]` or remove |
| Any `github.com/<other>` URL that belongs to user collaborators | Body, references | Replace with `[anonymised URL]` |
| Specific git commit hashes from gHashTag repos | Body | Replace with `[redacted hash]` |
| `gHashTag/tt-trinity-gamma#110` (PR reference) | §5.4 erratum text | Replace with `[redacted PR reference]` |

### 2.3 Other identifying artefacts

| Item | Where | Action |
|---|---|---|
| Zenodo DOI `10.5281/zenodo.19227877` | If cited | Remove (this DOI is the Pellis-Vasilev-Olsen phi-paper — wrong paper, wrong authorship, and identity leak) |
| Tiny Tapeout TTSKY26b shuttle username | Body §5.4 | Replace shuttle reference with neutral "a public open-shuttle service" |
| `pellis_vasilev_letter` | If anywhere | Remove (different paper, different authorship; mentioning links to user) |
| arXiv submission ID 7664437 | If cited | Remove |
| arXiv code QFHDTL | Not in paper but check footnotes / acknowledgements | Remove if present |
| "John Michell Symposium" / "Temenos Academy" | If anywhere | Remove (visa-track artefact, not arithmetic content) |
| "Wisdom Traditions Center" / "WTC" | If anywhere | Remove |
| DARPA / CLARA / "Dr. Grosof" | Body §5.6 | **Cut entire §5.6** |
| Scott Olsen / "Olsen" (the visa-track collaborator) | If anywhere | Remove |
| Sterling Pellis / Pellis | If anywhere | Remove |
| `t27.ai` domain | Anywhere | Remove |

### 2.4 Self-citations

| Item | Action |
|---|---|
| Cite of the arXiv preprint version of this paper | Cite as "an extended technical note by the authors, in preparation" with no arXiv ID |
| Cite of any author's prior work | Cite as "[Author1, 2026]" or "Anonymous, in preparation" |
| Cite of any gHashTag-hosted artefact | "[Repository A]" / "[Repository B]" |
| Cross-reference to "the author's earlier work" | Replace with passive voice: "earlier work has shown..." |

### 2.5 Acknowledgements

**Remove the entire Acknowledgements section** from the reviewer-facing PDF.

Restore at camera-ready (if accepted).

---

## 3. Identifying text content (supplementary materials)

If submitting supplementary materials (RTL, conformance vectors, replication scripts):

| Item | Action |
|---|---|
| All `LICENSE` files with author name | Replace author name with "Anonymous" temporarily; restore at camera-ready |
| `README.md` author name | Anonymise |
| Git history with commit messages from author | **Strip git history**: provide a flat tarball, not a git clone |
| Any inline file headers `// Author: Dmitrii Vasiliev` | Anonymise |
| Repository remote URLs in `.git/config` | Strip entirely (flat tarball, no `.git`) |
| File paths containing `gHashTag/...` | Rename to `arith2027-supplementary/...` |
| Hard-coded paths to user home directories | Make relative |
| Email addresses in code comments | Remove |
| ORCID in any header | Remove |

**Verification command for supplementary tarball:**
```bash
grep -r -i -E "vasiliev|vasilev|ghashTag|admin@t27|reactnativeinitru|ko samui|thailand|orcid|zenodo|0009-0008-4294-6159|pellis|olsen|temenos|wtc|darpa|clara" supplementary/
```
Should return no matches.

---

## 4. URL audit

Every URL in the paper (body and references) must be one of:

- A neutral third-party reference (IEEE, arXiv non-self, Springer, journal homepage, classical book).
- An anonymous mirror (e.g., an anonymous figshare upload).
- `[anonymised URL]` placeholder.

URLs to **strip or anonymise**:
- `github.com/gHashTag/*`
- `arxiv.org/abs/<self>` (any of the user's own arXiv IDs)
- `zenodo.org/record/19227877` or any Zenodo DOI linking to user
- `t27.ai` and any subdomain
- Personal homepage URLs
- Tiny Tapeout shuttle pages that show the user's submission name

---

## 5. Figures and tables

| Item | Action |
|---|---|
| Figure captions referencing repo names | Strip repo names |
| Screenshots showing GitHub URL bar or repo header | Crop or recapture without the URL bar |
| Synthesis reports showing user-specific paths (e.g., `/home/user/...`) | Sanitise paths |
| Logo or watermark from any author institution | Remove |
| EXIF data on embedded PNG/JPEG figures | Strip with `exiftool -all= figure.png` |
| Footer / header text in plots showing run hostnames | Remove |

---

## 6. Build chain

If using LaTeX:

| Item | Action |
|---|---|
| `\author{...}` in source | `\author{Anonymous Submission \\\\ ARITH 2027 — Double-Blind Review}` |
| `\thanks{...}` footnotes | Remove or comment out |
| `\affiliation{...}` | Remove |
| `\orcid{...}` | Remove |
| Acknowledgements environment | Comment out, restore at camera-ready |
| `\bibliography{...}` self-cites | Audit `.bib` file: anonymise self-cite keys, drop self-cite entries that are not essential |
| Git commit info embedded by some build tools (`gitinfo2`) | Disable for reviewer-facing build |
| Custom `\thanks{}` showing funding | Cut (no funding to disclose for this paper anyway, but check) |

---

## 7. Final verification pipeline (run before every submission)

```bash
# 1. Metadata audit
exiftool reviewer_facing.pdf | grep -i -E "author|creator|title|subject|comments"

# 2. Body text audit
pdftotext reviewer_facing.pdf - | grep -i -E "vasiliev|vasilev|vibee_dev|ghashTag|admin@t27|reactnativeinitru|ko samui|thailand|orcid|zenodo|0009-0008-4294-6159|pellis|olsen|temenos|wtc|darpa|clara|t27.ai"

# 3. URL audit
pdftotext reviewer_facing.pdf - | grep -i -E "github|gitlab|zenodo|t27|arxiv"
# Then manually verify every URL is neutral.

# 4. Supplementary materials audit (if submitting)
grep -r -i -E "vasiliev|vasilev|ghashTag|admin@t27|reactnativeinitru|ko samui|thailand|orcid|0009-0008-4294-6159|pellis|olsen|temenos|wtc|darpa|clara" supplementary/

# 5. Git history strip (if submitting code)
rm -rf supplementary/.git
tar -czf arith2027_supplementary.tar.gz supplementary/
```

**All four greps must return no matches** before submission.

---

## 8. Restoration at camera-ready (if accepted)

If the paper is accepted, the camera-ready version restores:
- Author name(s) on title page
- Email + affiliation
- ORCID
- Acknowledgements (with funding disclosure — note: no DARPA funding to disclose, this paper is independent of any contract)
- Public repository URLs (gHashTag/arith2027-goldenfloat to be made public at this stage)
- Zenodo DOI for the supplementary materials archive

Maintain a **separate camera-ready branch** in the local repo so the restoration is a clean diff, not a manual re-edit.

---

## 9. Sign-off

Before submission, the user signs off this checklist with an explicit "anonymisation audit passed" entry in the workspace log. Date and PDF hash recorded.

| Iteration | Date | Reviewer-facing PDF SHA-256 | Sign-off |
|---|---|---|---|
| Initial submission | — | — | — |
| Revision 1 (if any) | — | — | — |
| Camera-ready (after acceptance) | — | — | — |

---

**End of checklist v0.1.**
