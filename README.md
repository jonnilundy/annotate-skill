# annotate

**Mark up a markdown doc in your browser. Hand the edits back to your AI.**

A skill that turns any markdown file into a self-contained review surface. Select text, leave a Suggest / Comment / Delete note, and watch it pin to the margin. When you're done, one click gives your AI a clean, structured list of every change to apply.

![annotate review surface: a markdown document with suggestions, comments, and deletions pinned as sidenotes in the right margin](docs/annotate-review.png)

## The problem it solves

Reviewing long text with an AI shouldn't feel like dictating edits over the phone.

You ask an AI for a draft. It writes a good one. Now you want to push back: tighten this sentence, cut that section, ask a question in the margin. So the copy-paste dance starts. Read in one window, type "in paragraph three, change X to Y" in another, lose your place, forget half of what you meant to flag.

**`annotate` makes the page itself the review surface.** You read and mark up in one place. The notes come back as structured markdown your AI can act on without you re-explaining a thing.

## What you get

- **Inline marks, margin notes.** Highlight a phrase, annotate, and your note anchors as a sidenote right beside the text. Suggest an edit, leave a comment, or strike something out.
- **A clean handoff.** Click **Copy Changes** and paste back a tidy `SUGGEST / COMMENT / DELETE` list, line-anchored to the source.
- **Zero infrastructure.** The output is one HTML file. Open it anywhere, no server.
- **Built to read in.** An [Edward Tufte](https://edwardtufte.github.io/tufte-css/)-inspired layout: warm off-white paper, a book serif, and a quiet right margin that exists for exactly this.

## Install

annotate is a standard `SKILL.md` skill, so it drops natively into whichever agent you use. Each tool auto-discovers it from a skills folder. No build, no runtime, just the folder and Python 3.

> **Seamless cross-tool tip:** Codex and Cursor both auto-discover the open-standard `~/.agents/skills/` folder. Install once there and it works in both.
>
> ```bash
> git clone https://github.com/jonnilundy/annotate-skill
> cp -r annotate-skill/plugins/annotate/skills/annotate ~/.agents/skills/annotate
> ```

<details>
<summary><b>Claude Code</b></summary>

One command, no cloning:

```
/plugin marketplace add jonnilundy/annotate-skill
/plugin install annotate@annotate-skill
```

</details>

<details>
<summary><b>Cursor</b></summary>

Cursor auto-discovers skills from `~/.cursor/skills/` (global) or `.cursor/skills/` (per project), then activates them on its own or on demand when you type `/` in Agent chat. Drop the folder in and reload the window (`Cmd/Ctrl+Shift+P` → "Developer: Reload Window"):

```bash
git clone https://github.com/jonnilundy/annotate-skill
cp -r annotate-skill/plugins/annotate/skills/annotate ~/.cursor/skills/annotate
```

</details>

<details>
<summary><b>Codex CLI (and ChatGPT's Codex)</b></summary>

Codex auto-discovers skills from `~/.agents/skills/` (global) or `.agents/skills/` anywhere between your working directory and the repo root. Drop the folder in and start a new session:

```bash
git clone https://github.com/jonnilundy/annotate-skill
cp -r annotate-skill/plugins/annotate/skills/annotate ~/.agents/skills/annotate
```

</details>

<details>
<summary><b>Claude Cowork & other Claude surfaces</b></summary>

Cowork shares Claude's Agent Skills. The Claude Code install above works, or drop the folder into your Claude skills directory:

```bash
git clone https://github.com/jonnilundy/annotate-skill
cp -r annotate-skill/plugins/annotate/skills/annotate ~/.claude/skills/annotate
```

</details>

## The loop

1. The skill writes `{file}.review.html` next to your original md file and opens it.
2. **Select text** → choose between **Suggest · Comment · Delete**.
3. Each note appears as a margin **sidenote** tied to a numbered mark.
4. Add high-level direction in **Notes for Claude** at the top.
5. Click **Copy Changes** (or **Export** for a file) and give it back to your LLM. It applies the edits and answers the comments.

## Three kinds of marks

| Type | Meaning | Looks like |
|------|---------|-----------|
| **Suggest** | replace the selected text | blue underline + the new text in the margin |
| **Comment** | a note or a question | yellow-gold highlight |
| **Delete** | remove the selected text | red strike-through |

## Why it looks like that

Most review tools are loud. This one is quiet on purpose. The text sits in a narrow, readable column and your edits live in the margin beside it, the way notes have lived on paper for centuries. You can scan a whole document and see every mark in context without a panel covering the words you're reviewing. Borrowed, gratefully, from [Tufte CSS](https://edwardtufte.github.io/tufte-css/).

## Simple by design

The whole tool is one HTML file. No build, no runtime, no dependencies to install, and nothing to keep running. It honors your original markdown exactly: the review file is generated straight from your `.md`, and the export maps back to it line by line. And because the handoff is a compact list of just the changes, not the whole document, it stays token-efficient when you give it back to your AI.

## Requirements

- Any coding agent that supports Agent Skills (Claude Code, Cursor, Codex CLI, and others)
- Python 3 (standard library only) to generate the review file

## License

MIT licensed. See the [MIT License](https://opensource.org/license/mit).
