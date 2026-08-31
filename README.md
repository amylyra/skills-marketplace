# amy-skills — a Claude Code skill marketplace

Claude Code skills for agent and prompt engineering.
Each skill lives in its own repository; this repo is the marketplace index that installs them.

| Skill | What it does | Source |
|---|---|---|
| [`agent-prompt-author`](https://github.com/amylyra/agent-prompt-author) | Writes and diagnoses system prompts, orchestrator instructions, delegation contracts, and tool descriptions. Routes to a diagnostic before it rewrites anything. | [amylyra/agent-prompt-author](https://github.com/amylyra/agent-prompt-author) |

## Install

**Claude Code plugin marketplace** — native, no Node required.

```
/plugin marketplace add amylyra/skills-marketplace
/plugin install agent-prompt-author@amy-skills
```

**Skills CLI** — works across Claude Code, Cursor, Windsurf, VS Code, and JetBrains.
Requires Node 18+.
Install from the skill's own repo, not from this marketplace:

```bash
npx skills add amylyra/agent-prompt-author -g
```

Drop `-g` to install into the current project instead of globally.

**Manual** — no tooling at all.

```bash
git clone https://github.com/amylyra/agent-prompt-author
cp -r agent-prompt-author ~/.claude/skills/
```

**claude.ai** — Settings → Capabilities → Skills, upload a `.zip` of the skill
folder with that folder as the zip root. Requires a Pro, Max, Team, or Enterprise
plan with code execution enabled.

> `npx skills add` (plural) is the [vercel-labs](https://github.com/vercel-labs/skills)
> CLI. It keeps one canonical copy in `.agents/skills/` and symlinks it into
> `~/.claude/skills/`, which is what makes Claude Code see it. A separate `npx
> skill install` (singular) CLI writes to `~/.agents/skills/` without the
> symlink — the install reports success and the skill never appears.

## Adding a skill to this marketplace

Skills are referenced, not vendored, so there is no copy here to drift out of
sync with its source repo. Add an entry to `.claude-plugin/marketplace.json`:

```json
{
  "name": "your-skill",
  "source": { "source": "url", "url": "https://github.com/amylyra/your-skill.git" },
  "strict": false,
  "skills": ["./"]
}
```

`skills: ["./"]` points at the repo root, for a repo whose `SKILL.md` sits at the
top level. Use the `url` source rather than the `github` source: `github` clones
over SSH and fails for anyone without a GitHub SSH key configured.

Validate before pushing:

```bash
claude plugin validate .
```

## License

MIT — see [LICENSE](LICENSE).
