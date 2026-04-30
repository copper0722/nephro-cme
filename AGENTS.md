# nephro-cme Agent Card

Scope: public nephrology board-review question bank and public-safe rationale.

## Public Boundary

- This repository is public.
- Do not commit patient data, private notes, exam recall originals, paywalled article text, textbook excerpts, PDFs, images from copyrighted sources, local paths, tokens, or internal automation logs.
- Source materials that are not clearly public/open-license stay in the private pipeline. Public output must be paraphrased, educational, and reviewed.
- Non-OA or subscription material may be cited as bibliographic metadata only unless license review permits more.

## Product Scope

- `cme/`: TSN-style 4-option A-D questions, answer reveal, rationale, and distractor analysis.
- `docs/qbank/`: static browser app generated from public-safe question files.
- `nephrology-cme-wiki/`: public-safe M2M rationale index. It must not contain raw textbook or paywalled source text.

## Question Rules

- Four options only: A-D.
- Single best answer.
- Use original wording; never copy exam stems or proprietary self-assessment questions.
- Every question needs source kind, public-safety status, topic, answer, rationale, and distractor analysis.
- If a source is private, the public question must be rewritten enough that it stands as an original educational vignette.

## Editing Rules

- Keep candidate-facing docs in zh-TW unless a file explicitly says M2M English.
- Keep machine-facing schema/protocol text concise and deterministic.
- Run validators after editing question files or generated qbank data.
- Generated caches, `.DS_Store`, `__pycache__`, PDFs, and local artifacts are banned.

## Validation

```bash
python3 scripts/validate_cme.py
python3 scripts/build_cme_index.py
```

Only publish when validation passes and the diff contains no private source material.

