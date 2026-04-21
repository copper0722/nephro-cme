# /nephrology-cme-wiki/ — placeholder (renamed from /cc-wiki/ on 2026-04-19)

CC-oriented M2M English wiki articles, **strictly derived downstream from `/note/`**.

## Strict rule (2026-04-19)

All content in this folder **MUST be generated from** `/note/` source notes. No hand-editing. No independent writing. Wiki is a pure derivative.

Status: **empty, deferred**. Activation begins once `/note/` accumulates sufficient complete notes (target ≥30) and `nephrology-cme-wiki-gen.py` synthesizer is deployed.

## Pipeline

```
/note/{book}_ch{NN}_{topic}.md  or  journal review note (publish: true, publish_to: nephro-cme)
  ↓ nephrology-cme-wiki-gen.py: aggregate by wiki_topic, translate to M2M English
/nephrology-cme-wiki/wiki_{topic}.md
```

Regeneration is overwrite-style: script reads all `publish: true + publish_to: nephro-cme` notes, aggregates by `wiki_topic:` frontmatter, emits wiki pages. Hand-edits are wiped on next run. To change wiki content → change the source note.

## Archives (pre-rule content, preserved for cross-ref only)

- `_archive/nephrology-wiki-old-wiki-20260413/` — 75 files, early review/book-topic pages
- `_archive/nephrology-wiki-pre-strict-rule-2026-04-19.zip` — 37 files, last state before retroactive rule application
