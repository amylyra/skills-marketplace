# amy-skills

Claude Code skills.

## Install

**Skills CLI** — works across Claude Code, Cursor, Windsurf, VS Code, and JetBrains.
Requires Node 18+.

```bash
npx skills add REPLACE-ME/skills-marketplace@agent-prompt-author -g
```

Drop `-g` to install into the current project instead of globally.

**Claude Code plugin marketplace** — native, no Node required.

```
/plugin marketplace add REPLACE-ME/skills-marketplace
/plugin install agent-prompt-author@amy-skills
```

**Manual** — no tooling at all.

```bash
git clone https://github.com/REPLACE-ME/skills-marketplace
cp -r skills-marketplace/agent-prompt-author ~/.claude/skills/
```

**claude.ai** — Settings → Capabilities, upload `agent-prompt-author.skill`
(the folder zipped, renamed to `.skill`).

> Use `npx skills add` (plural). A separate `npx skill install` (singular) CLI
> writes to `~/.agents/skills/`, which Claude Code does not read — the install
> succeeds and the skill never appears.

## agent-prompt-author

For writing and diagnosing system prompts, orchestrator instructions, delegation
contracts, and tool descriptions for agents you build.

It routes to a diagnostic before it writes anything, because prompt work usually
fails for reasons that rewriting the prompt cannot fix:

1. The prompt was never the bottleneck.
2. The rule lives in a layer that cannot enforce it — prose is a request, hooks are a gate.
3. Rules written for an older model are still firing.
4. The revision loop has no external verifier, so it optimizes readability.

Five routes: enforcement, headroom, wrong-artifact, authoring, revision. Only the
matched route's reference file loads, so a diagnosis costs ~70 lines of context
rather than the whole skill.

Includes `references/portability.md` for prompts that must run across model
families — where several of the standard recommendations invert.

### Status

**v0.1.0 — unverified.** Written from published research; the routing has not been
tested against a real case set. A companion regression harness is at
[REPLACE-ME/prompt-evals]. Run it before relying on this in production, and
replace the sample cases with requests mined from your own sessions.

Every number in `references/evidence.md` is marked for whether the source was
read in full or via secondary coverage. Verify before citing.

## License

MIT
