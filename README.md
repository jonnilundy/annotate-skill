# annotate

A Claude Code skill that turns any markdown file into a **self-contained, Tufte-styled HTML review surface**. Select text in the browser to leave **Suggest / Comment / Delete** annotations that anchor as margin sidenotes, then export structured markdown an AI can apply back to the source.

No server, no build step, no dependencies beyond Python 3 (standard library). The generated review file is a single `.html` you can open anywhere; annotations persist in `localStorage` and export on demand.

![Edward Tufte–inspired layout: off-white paper, italic serif headlines, annotations as right-margin sidenotes.](https://edwardtufte.github.io/tufte-css/)

## Install

This repo is a Claude Code plugin marketplace. From inside Claude Code:

```
/plugin marketplace add jonnilundy/annotate-skill
/plugin install annotate@annotate-skill
```

Then browse `/plugin` → Discover, or just start using it.

## Use

Ask Claude Code to make a markdown file reviewable:

> "annotate ./draft.md" · "make this reviewable" · "create an annotation page for X"

The skill writes `draft.review.html` next to the source and opens it. In the browser:

1. **Select text** → a small toolbar offers **Suggest edit · Comment · Delete**.
2. Each annotation appears as a **sidenote** in the right margin, tied to a superscript number, and in a toggleable **Annotations** list (top bar).
3. Add high-level direction in **Notes for Claude** at the top.
4. Click **Copy for Claude** (or **Export**) to get a structured `draft.annotations.md`.
5. Paste it back to Claude — it applies `SUGGEST` and `DELETE` edits to the source and answers `COMMENT`s.

## Annotation types

| Type | Meaning |
|------|---------|
| **Suggest** | replace the selected text with something else |
| **Comment** | a note or question, no edit needed |
| **Delete** | remove the selected text |

## How it works

The skill ships a single HTML template. A short inline command (see `SKILL.md`) injects the source markdown, computes a content hash, and writes the review file. Everything else — the markdown renderer, the annotation engine, sidenote layout, export — lives in the template and runs client-side.

Anchoring is resilient by design: annotations anchor to the leaf block where the selection starts, re-locate by text on load (not just line number), clamp cross-block selections to the start block, and visibly flag anything that can't be located rather than failing silently.

## Requirements

- Claude Code (for the skill workflow)
- Python 3 (standard library only) to generate the review file

## License

MIT © Jonni Lundy. See [LICENSE](./LICENSE).
