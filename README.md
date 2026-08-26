# Audit ur Harness

An [Agent Skill](https://www.anthropic.com/engineering/equipping-agents-for-the-real-world-with-agent-skills) that audits a project's AI **harness** — the guardrails, memory, verification, observability, and tool-design scaffolding around a model, not the model itself — and produces an evidence-cited maturity report. It never edits your project and never applies its own suggestions; it only ever reads files and writes a report.

## What it does

Point it at a project folder and ask it to audit the harness. It reads through the project, scores each of 8 fixed layers (State & Memory, Execution Environment, Control & Enforcement, Context Management, Reasoning & Verification, Tool Design, Long-Horizon Execution, Observability & Learning) on a 0–3 scale, and writes a self-contained interactive HTML report — every score backed by a citation to the actual file and line it came from. "No evidence found" is a valid, complete answer for any layer; nothing is invented.

It can also notice a real, evidenced pattern specific to your project that doesn't fit any of the 8 fixed layers, score it the same way, and suggest — never apply — adding it as a permanent custom layer for future audits.

## Why

Most "AI harness" advice is generic. This turns it into a repeatable, grounded audit: concrete citations instead of vibes, absence treated as a real finding instead of being glossed over, and every improvement suggestion left as a copy-pasteable draft for a human to review and apply through their own agent — never auto-applied, under any setting.

## Install

This is a standard [Agent Skill](https://www.anthropic.com/engineering/equipping-agents-for-the-real-world-with-agent-skills) — a `SKILL.md` file plus a `references/` folder. It works in any tool that loads Agent Skills (Claude Code, Cowork, Codex, Cursor, and others).

1. Download this repository (or the latest [release](../../releases)).
2. Copy the `Audit_ur_Harness/` folder into wherever your tool looks for skills (for Claude Code, that's typically `.claude/skills/` in your project or `~/.claude/skills/` for a personal skill available everywhere; check your tool's own docs for its skills directory).
3. In that tool, ask it to audit your project's harness, rate your guardrails, or check your project's AI harness — the skill's description is written to match phrasing like that.

No network access, no API keys, and no special platform extensions are required — anything that can read files and write a new file can run this.

## What it produces

Everything lands inside a `harness/` folder in your project, gitignored by default:

- `harness/report.html` — a self-contained, dark-themed interactive report. Click any layer to expand its evidence and suggestions.
- `harness/reports/<date>-full.md` — the same audit in plain markdown.
- `harness/config.md` — where you (not the agent) define any project-specific custom layers.
- `harness/rules.md` — a "ratchet" file: past failures turned into standing rules.
- `harness/suggestions/open/` — the current backlog of open, unapplied suggestions.

`harness/reports/`, `harness/report.html`, and `harness/suggestions/` are gitignored automatically on first run, since a full audit is, by design, a list of your project's weak points. `harness/rules.md` and `harness/config.md` are left out of `.gitignore` on purpose — they're conventions worth sharing with collaborators.

## Known limitation

This audit is self-attested: whatever agent runs it is reporting on its own reading of the project, with no independent verification that its citations are accurate. Treat the report as a strong starting point for your own review, not a certified audit. See `SKILL.md` for the full limitation notes, including a narrower one specific to agent-identified custom layers.

## License

Add your chosen license here before publishing (see the setup notes you were given alongside this folder).

## Contributing / forking

This is an open format — a fork is expected, not a problem. If you're working from a copy of this repository, check the canonical source noted at the top of `SKILL.md` to see whether your copy is current.
