# 2AMD20 Exam Template

Minimal, opinionated LaTeX skeleton for the take-home final exam of
**2AMD20 Knowledge Engineering (Q4 2025-2026)**.

> Heads-up: this template is **not** an official course artifact. The course
> staff did not release a template — they only specified margins (`\usepackage{fullpage}`)
> and submission format (single PDF on Canvas). See
> [`docs/course_extracts/exam.md`](../../docs/course_extracts/exam.md) for the
> full exam rules and question catalogue.

## Files

| Path | Purpose |
|---|---|
| `exam.tex` | The main document. Sets up packages, the `question` environment, front matter, AI acknowledgement, and bibliography. Pulls in each answer via `\input{questions/...}`. |
| `questions/q1_lecture2_reification.tex` | Lecture 2 — Reification in property graphs (≥ 2 pages). |
| `questions/q2_lecture3_mpg_rdf.tex` | Lecture 3 — Converting between RDF and MPG reification (≥ 2 pages). |
| `questions/q3_lecture8_rdf_to_mpg_mapping.tex` | Lecture 8 — Direct mapping from reified RDF to reified MPG. |

> The exam requires **five** questions from five different weeks. Three are wired in (L2, L3, L8). Pick two more from L4, L5, L6, or L7 and add them as `questions/q4_*.tex` and `questions/q5_*.tex`, then uncomment the matching `\input` lines in `exam.tex`.
>
> **Overlap warning (L3 and L8):** both questions touch on RDF↔MPG reification. They are different prompts (L3 = both directions + motivation; L8 = one-direction direct mapping with soundness/completeness), but graders will penalise duplicated content. Each answer file already carries a `% NOTE:` reminder.
| `references.bib` | Pre-filled BibTeX entries for the papers most commonly cited across the questions (MPG, Cameron, Sequeda et al., etc.). Add more as you read. |
| `.gitignore` | Ignores LaTeX build artefacts so only sources are tracked. |

## Build

Any of the following work. **Tectonic** is recommended — single command, fetches missing packages automatically:

```bash
cd material/exam_template
tectonic exam.tex              # produces exam.pdf
```

With `latexmk`:

```bash
cd material/exam_template
latexmk -pdf exam.tex          # build
latexmk -c                     # clean intermediate files
latexmk -C                     # also remove exam.pdf
```

With plain `pdflatex` (run twice for ToC + citations):

```bash
pdflatex exam.tex && bibtex exam && pdflatex exam.tex && pdflatex exam.tex
```

### Expected warnings

A clean build still emits two harmless messages — ignore them:

- `I found no \citation commands` (BibTeX) — appears until you add your first `\cite{...}`. The References section will render empty in the meantime.
- `internal consistency problem when checking if exam.bbl changed` / `TeX rerun seems needed, but stopping at 6 passes` (Tectonic only) — Tectonic's `.bbl` rerun heuristic is over-sensitive with `natbib`. The PDF is correct and stable; the build exits 0.

## Customising

1. Fill in your name, student ID, and email on the `\author{...}` line in `exam.tex`.
2. **Pick five questions** from the seven released — the syllabus requires answers from five **different** weeks. To swap a question:
   - Drop a new file under `questions/` following the same `\begin{question}{N}{Lecture}{Topic}` shape.
   - Replace one of the `\input{questions/...}` lines in `exam.tex`.
3. Write your answer in the body of each `question` environment.
4. **Do not delete** the `AI usage acknowledgement` section in `exam.tex` — the course AI policy requires it. Fill it in honestly.
5. Add new entries to `references.bib` as you cite more papers.

## Length and margin requirements (per question)

| Lecture | Topic | Min. length |
|---|---|---|
| 2 | Property-graph reification | 2 A4 full pages |
| 3 | RDF ↔ MPG reification (both directions) | 2 A4 full pages |
| 4 | `CQ_k` containment proof | — (not specified) |
| 5 | Relational DB vs. KG for e-commerce | 1 A4 full page |
| 6 | Review of a data-context paper | 2 A4 full pages |
| 7 | Cameron's *Laws of Identity* and society | 1–2 A4 full pages |
| 8 | RDF → MPG direct mapping | — (not specified) |

The `\usepackage{fullpage}` package in `exam.tex` already enforces the required
margin convention.
