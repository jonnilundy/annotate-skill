# annotate

**Mark up a markdown doc in your browser. Hand the notes back to your AI.**

A Claude Code skill that turns any markdown file into a self-contained review surface. Select text, leave a Suggest / Comment / Delete note, and watch it pin to the margin like a copy editor's pencil. When you're done, one click gives your AI a clean, structured list of every change to apply.

![annotate review surface: a markdown agenda with Suggest, Comment, and Delete notes pinned as sidenotes in the right margin, each tied to a numbered mark in the text](docs/annotate-review.png)

## The problem it solves

You ask Claude for a draft. It writes a good one. Now you want to push back: tighten this sentence, cut that section, ask a question in the margin. So the copy-paste dance starts. Read in one window, type "in paragraph three, change X to Y" in another, lose your place, forget half of what you meant to flag.

Reviewing long text with an AI shouldn't feel like dictating edits over the phone.

`annotate` makes the page itself the review surface. You read and mark up in one place. The notes come back as structured markdown your AI can act on without you re-explaining a thing.

## What you get

- **Inline marks, margin notes.** Highlight a phrase, pick a type, and your note anchors as a sidenote right beside the text. Suggest an edit, leave a comment, or strike something out.
- **A clean handoff.** Click **Copy for Claude** and paste back a tidy `SUGGEST / COMMENT / DELETE` list, line-anchored to the source.
- **Zero infrastructure.** The output is one HTML file. No server, no build step, no account, no network calls after the fonts load. Open it anywhere.
- **Built to read in.** An Edward Tufte–inspired layout: warm off-white paper, a book serif, and a quiet right margin that exists for exactly this.

## Quick start

From inside Claude Code:

```
/plugin marketplace add jonnilundy/annotate-skill
/plugin install annotate@annotate-skill
```

Then point it at a file:

> "annotate ./draft.md" · "make this reviewable" · "create an annotation page for X"

## The loop

1. The skill writes `draft.review.html` next to your file and opens it.
2. **Select text** → a small toolbar offers **Suggest edit · Comment · Delete**.
3. Each note appears as a margin **sidenote** tied to a numbered mark, and in a toggleable **Annotations** list.
4. Add high-level direction in **Notes for Claude** at the top.
5. Click **Copy for Claude** (or **Export** for a file), and paste it back. Claude applies the edits and answers the comments.

## Three kinds of marks

| Type | Meaning | Looks like |
|------|---------|-----------|
| **Suggest** | replace the selected text | blue underline + the new text in the margin |
| **Comment** | a note or a question, no edit | yellow-gold highlight |
| **Delete** | remove the selected text | red strike-through |

## Why it looks like that

Most review tools are loud. This one is quiet on purpose. The text sits in a narrow, readable column and your edits live in the margin beside it, the way notes have lived on paper for centuries. You can scan a whole document and see every mark in context without a panel covering the words you're reviewing. Borrowed, gratefully, from [Tufte CSS](https://edwardtufte.github.io/tufte-css/).

## Reliable by design

Annotations anchor to the block where your selection starts and re-locate themselves by text on load, not by a fragile line number. A note that can't be found in the document is flagged in the list rather than vanishing. Clicking a toolbar button never loses your selection. The behavior is meant to be boring, which is the point.

## Requirements

- Claude Code (for the skill workflow)
- Python 3, standard library only, to generate the review file

## Install it as a plain skill instead

Prefer no plugin wrapper? A skill is just a folder:

```bash
git clone https://github.com/jonnilundy/annotate-skill
cp -r annotate-skill/plugins/annotate/skills/annotate ~/.claude/skills/annotate
```

You give up one-command updates and Discover listing, but it works identically.

## License

MIT © Jonni Lundy. See [LICENSE](./LICENSE).
