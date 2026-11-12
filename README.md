# skills

A collection of agent skills for building real things with AI coding agents. Works with Gemini CLI, Claude Code, Codex, Cursor, Antigravity and any agent that reads SKILL.md.

## Skills

| Skill | What it does |
|---|---|
| [frontend-unslop](skills/frontend-unslop/SKILL.md) | Plans before building (PRD, copy, tokens, design-system page) so AI-built frontends stop looking AI-built. Covers landing pages and app UIs built on a mapped backend. |

More coming. PRs welcome.

## Install

Pick the skills you want when prompted:

```bash
npx skills add Demilade01/skills
```

Gemini CLI, one skill:

```bash
gemini skills install https://github.com/Demilade01/skills.git --path skills/frontend-unslop
```

Manual: copy a folder from `skills/` into your agent's skills directory.

| Agent | Folder |
|---|---|
| Gemini CLI | `~/.gemini/skills/` or `.gemini/skills/` |
| Antigravity | `~/.gemini/antigravity/skills/` |
| Claude Code | `~/.claude/skills/` or `.claude/skills/` |
| Codex, Cursor, others | `.agents/skills/` |

No skills support? Paste the body of a `SKILL.md` into `AGENTS.md`, `GEMINI.md` or your rules file.

## Use

Name the skill in your prompt, for example:

```
Use the frontend-unslop skill. Idea: [your idea]. Start at the PRD.
```

## Adding a skill

1. Create `skills/<skill-name>/SKILL.md`.
2. Frontmatter needs only `name` (matches the folder) and `description`.
3. Keep the description specific about when to trigger.
4. Add a row to the table above and a credit below if the skill is adapted from someone else's work.

## Credits

- **frontend-unslop**: workflow and design rules adapted from the "Unslop your AI-coded website" webinar (11 November 2026) by Naheem and Cybersmith (Oluwamurewa Abiodun). App mode, data-state rules and the API-contract layer are extensions. Not affiliated with or endorsed by the presenters.

## Licence

MIT
