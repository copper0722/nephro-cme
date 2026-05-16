# nephro-cme/cme - CME question bank card

GitHub: `copper0722/nephro-cme` (public). **Status: legacy / no new writes** (Law L21 deprecated list). Card retained as spec for historical regeneration only; new CME authoring not dispatched here. Public-safe CME layer over `wiki/` for TSN board prep: wiki = source knowledge, cme = retrieval practice + exam-style reasoning. All items original — no copied exam stems, no patient identifiers, no paywall/textbook text, no private annotations.

## Folder layout

| path | role |
|---|---|
| `cme/README.md` | public candidate guide (zh-TW), maintains module checklist |
| `cme/_template-v2.md` | canonical v2 template (one-Q-per-file) |
| `cme/_template.md` | deprecated redirect to v2 |
| `cme/nephrology-<topic>-<focus>.md` | CME module, one topic per file |
| `cme/AGENTS.md` | this protocol card |

Naming: lowercase kebab-case, `nephrology-` prefix, one module = one coherent exam unit (staging, anemia dx, HD adequacy, ...).

## Required frontmatter

```yaml
---
module: nephrology-<topic>-<focus>
topic: <zh-TW module title>
difficulty: <recall|application|analysis|mixed>
bloom_level: <recall|application|analysis|mixed>
wiki_source:
  - ../wiki/<source-file>.md
author: <Claude Opus|Codex|Gemma>
date: YYYY-MM-DD
question_count: <integer>
---
```

## Question format (TSN-style)

Two types:
- **Part A 基礎** — short stem; concept/definition/threshold/association/equation recall.
- **Part B 臨床** — short fictionalized clinical vignette (age/sex/comorbidity only, no real patient data), then interpretation / next-step / risk-stratification question.

Both: 4 options `A-D` only, single best answer.

Every question block must include:
1. `Type` (Part A / Part B)
2. `Difficulty`
3. `Bloom`
4. Stem in zh-TW
5. Four options `A-D`
6. `Correct answer`
7. `Explanation`
8. `Source` citation back to `../wiki/...`
9. Distractor analysis for every wrong option

## Difficulty map

| difficulty | Bloom | use case |
|---|---|---|
| `recall` | remember/understand | definitions, cutoffs, formula identity, one-step classification |
| `application` | apply | vignette staging, choosing confirmatory equation, assigning risk cell |
| `analysis` | analyze | compare cases, resolve discordant data, explain why CGA beats GFR-only |

Modules should mix levels. Default for 10 Q ≈ 4 recall / 4 application / 2 analysis unless topic warrants otherwise.

## Explanation standard

Explanation must (1) state why the keyed answer is best, (2) cite the exact public source file with relative path + section title, (3) explain why each distractor is wrong (not just why the key is right). Citation style:

```md
Source: [../nephrology-cme-wiki/wiki_nephrology_ckd_part1.md](../nephrology-cme-wiki/wiki_nephrology_ckd_part1.md)
Section: "Uses of GFR and Albuminuria Level in Acute and Chronic Kidney Disease (2022)"
```

## Auto-generation protocol (Claude Opus / Codex / Gemma)

1. Read one source wiki file end-to-end.
2. Extract examable units: definitions, thresholds, equations/biomarkers, risk signals, guideline logic.
3. Build a balanced Part A + Part B set; original stems only, never paraphrase copyrighted exam-bank wording.
4. Build distractors from nearby-but-wrong concepts: wrong threshold / wrong stage / wrong equation / true fact in wrong context.
5. Add explanations with source citation + distractor analysis.
6. Verify every claim traces to the linked wiki file; re-read for public safety and Taiwan terminology.

## Review process

Same editorial model as `wiki/`: any of the 3 authors may draft/revise; Claude Opus runs a daily audit on modified `cme/*.md` checking methodology consistency, Guyatt EBM logic, Hernán causal-language discipline, answer-key accuracy, distractor quality, public-safety compliance. Minor errors → fix directly. Major disagreement → flag inline `<!-- EDITOR: ... -->` or escalate to Copper. Never delete another author's work wholesale; revise in place, preserve git attribution.

## Integration with wiki

CME is downstream from wiki (wiki explains; cme tests retrieval + application). Every module declares `wiki_source`; every explanation links back to its source wiki file; prefer topic-level cross-links near the top. If wiki changes materially, linked CME modules are regenerated or audited.

## Progress tracking

Local-only: `docs/qbank/` SPA stores answered IDs / score / weak topics in `localStorage` — no server DB. Each module frontmatter declares `question_count`; `cme/README.md` keeps the public module checklist. Optional module footer: quick self-audit (done / wrong items / wiki to revisit).

## Validation

```bash
python3 scripts/validate_cme.py
python3 scripts/build_cme_index.py
```

Only publish when validation passes and the diff contains no private source material.

## Public-safety rules

No patient identifiers. No copied board questions. No paywall excerpts. No private annotations. Original educational content only.

## TODO

- [ ] Build first-pass module map from existing `wiki/` coverage — dispatch:auto (2026-04-08)
- [ ] Add CKD management module from `../wiki/wiki_nephrology_ckd_part2.md` — dispatch:auto (2026-04-08)
- [ ] Define module checklist growth rules in `README.md` as coverage expands — plan:auto (2026-04-08)
