# skills

An open-source collection of portable skills for building real things with AI coding agents.

Every skill follows the open `SKILL.md` standard and works across **Gemini CLI, Antigravity, Claude Code, OpenAI Codex, Cursor, Windsurf, GitHub Copilot, Cline, Roo Code, Kilo Code, OpenCode, Goose, Amp, Aider, Trae, Zed, Continue**, and web builders (**v0, Lovable, Bolt, Replit Agent**).

## Skills

| Skill | What it does |
|---|---|
| [frontend-unslop](skills/frontend-unslop/SKILL.md) | Plans before building (PRD, copy, tokens, design-system page) so AI-built frontends stop looking AI-built. Covers landing pages and app UIs built on a mapped backend. |

More coming. PRs welcome.

---

## Install

### 1. Universal CLI (`npx skills`) — Recommended

Automatically detects your installed coding agents and installs the skills you select:

```bash
npx skills add Demilade01/skills
```

Useful flags:

```bash
# Install a single skill directly
npx skills add Demilade01/skills --skill frontend-unslop

# Install globally (available across all projects)
npx skills add Demilade01/skills -g

# Target specific agent(s)
npx skills add Demilade01/skills -a claude-code -a cursor -a codex
```

### 2. Gemini CLI

Install directly with the built-in skills manager:

```bash
# Project-scoped or global install
gemini skills install https://github.com/Demilade01/skills.git --path skills/frontend-unslop
```

### 3. Manual Install (Native `SKILL.md` Directories)

Clone this repository and copy any folder from `skills/<skill-name>` into your agent's project or global skills directory:

```bash
git clone https://github.com/Demilade01/skills.git
```

| Agent | Project Path (Workspace) | Global Path (All Projects) |
|---|---|---|
| **Universal / Cross-Agent** | `.agents/skills/<skill-name>/` | `~/.agents/skills/<skill-name>/` |
| **Gemini CLI** | `.gemini/skills/<skill-name>/` | `~/.gemini/skills/<skill-name>/` |
| **Antigravity** | `.agents/skills/<skill-name>/` | `~/.gemini/antigravity/skills/<skill-name>/` |
| **Claude Code** | `.claude/skills/<skill-name>/` | `~/.claude/skills/<skill-name>/` |
| **OpenAI Codex** | `.agents/skills/<skill-name>/` or `.codex/skills/<skill-name>/` | `~/.codex/skills/<skill-name>/` |
| **Cursor** | `.cursor/skills/<skill-name>/` or `.agents/skills/<skill-name>/` | `~/.cursor/skills/<skill-name>/` |
| **Windsurf** | `.windsurf/skills/<skill-name>/` | `~/.codeium/windsurf/skills/<skill-name>/` |
| **GitHub Copilot** | `.github/skills/<skill-name>/` | `~/.copilot/skills/<skill-name>/` |
| **Cline** | `.cline/skills/<skill-name>/` or `.agents/skills/<skill-name>/` | `~/.cline/skills/<skill-name>/` |
| **Roo Code** | `.roo/skills/<skill-name>/` or `.agents/skills/<skill-name>/` | `~/.roo/skills/<skill-name>/` |
| **Kilo Code** | `.kilocode/skills/<skill-name>/` or `.agents/skills/<skill-name>/` | `~/.kilocode/skills/<skill-name>/` |
| **OpenCode** | `.opencode/skills/<skill-name>/` or `.agents/skills/<skill-name>/` | `~/.config/opencode/skills/<skill-name>/` |
| **Goose** | `.goose/skills/<skill-name>/` or `.agents/skills/<skill-name>/` | `~/.config/goose/skills/<skill-name>/` |
| **Amp** | `.agents/skills/<skill-name>/` | `~/.config/agents/skills/<skill-name>/` |
| **Trae** | `.trae/skills/<skill-name>/` | `~/.trae/skills/<skill-name>/` |

> **Windows note**: `~` maps to `%USERPROFILE%` (e.g., `C:\Users\<you>\.gemini\skills\`).

---

### 4. Agents Without Native `SKILL.md` Support (Rules, Flags & Web Builders)

Every `SKILL.md` is plain Markdown. If your tool does not use a `skills/` folder yet, load it as a rule file, read-only context file, or project instruction:

| Tool / Environment | How to load a skill |
|---|---|
| **`AGENTS.md` / `CLAUDE.md` / `GEMINI.md`** | Append or copy `SKILL.md` into your root `AGENTS.md` (read by Codex, Cursor, Windsurf, Amp, OpenCode, Zed, Devin), `CLAUDE.md`, or `GEMINI.md`. |
| **Cursor Rules** | Copy to `.cursor/rules/<skill-name>.mdc` (or append to `.cursorrules`). |
| **Windsurf Rules** | Copy to `.windsurf/rules/<skill-name>.md` (or append to `.windsurfrules`). |
| **GitHub Copilot Instructions** | Copy to `.github/instructions/<skill-name>.instructions.md` or append to `.github/copilot-instructions.md`. |
| **Cline / Roo Rules** | Copy to `.clinerules/<skill-name>.md` or `.roorules/<skill-name>.md`. |
| **Aider** | Run `aider --read skills/frontend-unslop/SKILL.md` or add `read: [skills/frontend-unslop/SKILL.md]` to `.aider.conf.yml`. |
| **Continue.dev** | Copy to `.continue/rules/<skill-name>.md`. |
| **Zed** | Copy or append to `.rules` in the project root. |
| **v0 / Lovable / Bolt / Replit Agent** | Paste the body of `SKILL.md` into **Project Knowledge / Custom Instructions**, or attach `SKILL.md` on the first prompt. |
| **ChatGPT / Claude Projects / Gemini Gems** | Upload `SKILL.md` to Project Files / Knowledge or paste into System Instructions. |

---

## Use

### Automatic Activation
Agents with `SKILL.md` support read each skill's `description` frontmatter and activate it automatically when your prompt matches (e.g. asking to build a landing page, dashboard, design system, or frontend for an existing backend).

### Explicit Invocation

Name the skill in your prompt, trigger its slash command, or `@`-mention the file:

**Site mode (landing page or marketing site):**
```text
Use the frontend-unslop skill. Idea: [your idea]. Start at the PRD.
```

**App mode (dashboard, web app, or mobile UI on top of a backend):**
```text
Use the frontend-unslop skill in app mode. Inspect our backend routes and schema first, then start at the PRD and app-map.
```

**Slash command (Claude Code, Cursor, OpenCode, etc.):**
```text
/frontend-unslop Idea: [your idea]. Start at the PRD.
```

**File mention (Cursor, Windsurf, Copilot, Cline, Zed):**
```text
@skills/frontend-unslop/SKILL.md Build the frontend for this repo. Start at the PRD.
```

---

## Adding a Skill

Contributions are welcome! To keep skills portable across every AI coding agent:

1. **Create a folder**: `skills/<skill-name>/SKILL.md` (use lowercase `kebab-case`).
2. **Add minimal YAML frontmatter**:
   ```yaml
   ---
   name: your-skill-name
   description: Clear, specific description of what the skill does and exact trigger phrases/scenarios when the agent should load it.
   ---
   ```
   - `name` must match the folder name.
   - `description` is how agents decide when to auto-activate the skill—be explicit about trigger scenarios.
3. **Optional supporting files**: If your skill needs templates, scripts, or extra docs, place them inside `skills/<skill-name>/references/`, `scripts/`, or `assets/` and link to them using relative paths from `SKILL.md`.
4. **Stay agent-agnostic**: Avoid hardcoding one editor's proprietary tool names if a general instruction works across all agents.
5. **Update the README**: Add a row to the [Skills](#skills) table above and a credit in [Credits](#credits) if adapted from existing work.

---

## Credits

- **frontend-unslop**: workflow and design rules adapted from the "Unslop your AI-coded website" webinar (11 November 2026) by Naheem and Cybersmith (Oluwamurewa Abiodun). App mode, data-state rules and the API-contract layer are extensions. Not affiliated with or endorsed by the presenters.

## Licence

[MIT](LICENSE)
