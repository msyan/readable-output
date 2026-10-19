# readable-output

让 AI 的解释更好懂 · Makes LLM output easier to understand — an agent skill built on Karpathy's "understanding ladder". English + 中文.

## What it does

Given an explanation request, the skill classifies the content and picks the **lowest rung that fully answers**, then produces it:

| Rung | Format | Trigger content |
|---|---|---|
| 1 | Plain controlled text (~80% ASD-STE100 in English; built-in 15-rule plain-Chinese set) | definitions, facts, procedures |
| 2 | Diagram (single-file SVG first, Mermaid when chat rendering matters; labeled arrows, `Figure N:` captions) | processes, causality, hierarchies |
| 3 | Interactive HTML page (single file, zero dependencies, offline; fixed anatomy: summary → interactive area → explanation → try-this → assumptions box → glossary → footer) | a parameter changes an outcome |
| 4 | Explainer-video storyboard (no rendering here; ready for showtime/Manim) | derivations that unfold over time |

House rules on every rung: **nothing cut** (every fact, number, condition, hedge survives), **draft first**, and a mandatory **"What to check"** section — clear is not the same as correct.

Forked from [ChangWenC/understanding-ladder](https://github.com/ChangWenC/understanding-ladder) (MIT), merged into one skill and extended with: task-reply structure, SVG-first diagram discipline, ruled HTML anatomy, and explicit risk countermeasures.

## Install

```bash
# Any agent that supports Agent Skills (Claude Code, Codex, Cursor, …)
npx skills add <your-username>/readable-output

# GitHub CLI (preview)
gh skill install <your-username>/readable-output

# Manual — Kimi Code
cp -r skills/readable-output ~/.agents/skills/

# Manual — Claude Code
cp -r skills/readable-output ~/.claude/skills/
```

(The `<your-username>/readable-output` commands work once this repo is pushed to GitHub.)

No install? Paste this into a prompt for the core writing style:

```text
Write about 80% of the way to ASD-STE100: one idea per sentence, one term per meaning, active voice, no filler. Cut nothing — keep every fact, number, condition, and hedge; just make the sentences clean.
```

## Files

- `SKILL.md` — the skill: rung selection, triggers, house rules
- `references/level-2-diagram.md` · `references/level-3-html.md` · `references/level-4-video.md` — per-rung rules
- `references/plain-chinese.md` — the 15-rule plain-Chinese set, loaded for Chinese output
- `references/plain-chinese-examples.md` — 5 before/after pairs

Full documentation (Chinese version, demo, related work): see the repository root README.

## License

MIT — copyright (c) 2026 ChangWenC, retained per the license; fork modifications by the repo owner. ASD-STE100 is a trademark of ASD; this skill is inspired by it and reproduces no standard text.
