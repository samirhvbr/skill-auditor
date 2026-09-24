# Claude Code settings — AUDITOR

This project's `.claude/` follows the Blue3/samirhvbr house pattern: **effort
level + permissions posture**. Today the repository is documentation only — no
execution stack has been decided (see `docs/decisoes.md` §Pendentes), so the
allow-list is deliberately lean.

## Files

| File | Role |
|---------|-------|
| `settings.json` | The **active** profile (versioned). `defaultMode: plan`, minimal allow-list + safety deny-list. It chooses no model. |
| `README.md` | This file. |

No versioned `settings.local.json` — it is in `.gitignore` on purpose (house
standard since the sweep of 25/07/2026).

## The model is the user's choice, not this repository's

**Nothing here chooses the model** (repodocs ADR-027). `settings.json` carries no
`model` and no `fallbackModel`, and its `env` steers none: no `ANTHROPIC_MODEL`,
no `ANTHROPIC_DEFAULT_*_MODEL`, no `CLAUDE_CODE_SUBAGENT_MODEL`. There are no
stand-by profiles to copy over `settings.json` either.

- The model is chosen per session, by the user, with **`/model`**.
- A **subagent inherits the session's model**.
- Every pin this repository used to carry outlived the model it named: `opus[1m]`
  was a version pin wearing a window suffix — the 1M variant existed only for the
  previous Opus — and `CLAUDE_CODE_SUBAGENT_MODEL: opus` kept sending subagents
  to an older model than the session's.

## Active profile

```jsonc
"effortLevel": "xhigh",
```

## Rules worth remembering

- **Effort `max` goes per session** (`/effort max` or `CLAUDE_CODE_EFFORT_LEVEL=max`
  in the environment). The JSON `effortLevel` field only accepts `low`/`medium`/
  `high`/`xhigh`; `max` there is ignored.
- `defaultMode: plan` is intentional: in this repo the cost of a wrongly written
  decision is high (a normative document becomes agent behavior later).

## Permissions posture

**Allow** — only what is safe and repetitive: reading/writing files, inspection
git, delivery git (`add`/`commit`/`push`) and format validators.

**Ask** — everything that changes the machine or talks to the world: `sudo`,
`crontab`, `systemctl`, dependency installation and `gh pr/issue create`.

> `crontab` and `systemctl` are in `ask` **on purpose**: the very product this
> repo specifies installs scheduling triggers (T-04 of `SECURITY.md`). Nobody
> installs persistence here without Samir seeing it.

**Deny** — reading a secret, destructive removal, `push --force`, `reset --hard`,
history rewriting and `curl|bash`.

> `git filter-branch` / `filter-repo` are denied because the automatic process of
> `~/x` runs `git pull --rebase` and **undoes** a history rewrite in the live
> working copy — rewriting here only breaks the repo.

## Additional allow-list (once the stack is settled)

Paste into `permissions.allow` as the harness gets defined:

```jsonc
// Python
"Bash(python3 -m pytest:*)", "Bash(pytest:*)",
"Bash(ruff check:*)", "Bash(ruff format:*)", "Bash(mypy:*)",

// Node
"Bash(npm run build:*)", "Bash(npm test:*)", "Bash(npx tsc --noEmit:*)",

// Rust
"Bash(cargo check:*)", "Bash(cargo test:*)", "Bash(cargo clippy:*)", "Bash(cargo fmt:*)"
```
