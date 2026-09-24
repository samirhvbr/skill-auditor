# Technical documentation — AUDITOR

Index of `docs/`. **Durable** documentation lives here; working notes, scope and
state live in [`.continue/`](../.continue/); the command/configuration contract
lives in [`SPEC.md`](../SPEC.md) at the root; the product's runtime prompt lives
in [`prompts/`](../prompts/).

> ⚠️ The project is in the **proposal phase**. There is no implementation. Whatever
> is marked as a skeleton or pending is exactly that — do not treat it as decided.

---

## In this folder

| File | What it is |
|---|---|
| [decisoes.md](decisoes.md) | **ADRs.** ADR-001 to ADR-009 (closed decisions) + the table of the 11 open pendencies. A new decision goes in here. |
| [revisao-inicial.md](revisao-inicial.md) | **Review of 2026-07-28.** 23 findings about the proposal, each with its status. Recommended reading before proposing architecture. |
| [contrato-subagente.md](contrato-subagente.md) | **Partial.** Specification of the subagent's input/output contract, finding format, model catalog and adapters. |

## Outside this folder

| File | What it is |
|---|---|
| [../README.md](../README.md) | The product proposal: goal, v1 scope, structure of `.auditor/`, cycle flow. |
| [../SPEC.md](../SPEC.md) | **Partial.** Canonical command syntax and the `config.yml` / `state.json` schema. |
| [../prompts/auditor-system.md](../prompts/auditor-system.md) | The subagent's **runtime prompt** — what the platform loads when it runs the skill. A product artifact. |
| [../SECURITY.md](../SECURITY.md) | Threat model (T-01 to T-08) and repository policy. **Required reading.** |
| [../version.md](../version.md) | Source of truth for the version, bump triggers and commit format. |
| [../CLAUDE.md](../CLAUDE.md) / [../AGENTS.md](../AGENTS.md) | Rules for whoever **develops** this repository. Mirrored — edit both. |
| [../skill/README.md](../skill/README.md) | The skill for Claude Code: installation, what the gate guarantees and what it does not. |
| [../schemas/](../schemas/) | JSON Schema for `config.yml`, `state.json` and the cycle output. |
| [../tests/](../tests/) | 43 tests, no external dependency. `python3 -m unittest discover -s tests` |
| [../.continue/escopo-projeto.md](../.continue/escopo-projeto.md) | Phases F0–F6 — a **proposal**, awaiting approval. |
| [../.continue/estado-atual.md](../.continue/estado-atual.md) | Where the project is and what comes next. |
| [../.claude/README.md](../.claude/README.md) | Effort level and permissions posture. The repository chooses no model — that is the user's call, with `/model` (repodocs ADR-027). |

---

## Where to start

- **Understand the product** → `../README.md`, then `decisoes.md`.
- **Going to propose architecture** → `revisao-inicial.md` first. The open findings
  already cover most of the traps, and A-13 may change the whole design.
- **Going to edit an agent file** → check the target. `CLAUDE.md` + `AGENTS.md`
  (root, mirrored) belong to the **repository**; `prompts/auditor-system.md` and
  `contrato-subagente.md` belong to the **product**. Table in `../CLAUDE.md` (ADR-007).
- **Going to touch writing, PR/issue or the scheduler** → `../SECURITY.md`, required.
- **Going to deliver** → `../version.md` (bump + changelog + commit format).

## Conventions

- This repository's documentation is in **PT-BR**. Artifacts AUDITOR produces in
  the audited repos are in **en-US** (see `../CLAUDE.md`).
- A new document here goes **into this index** in the same commit.
- No link to a file that does not exist: if it is future work, say so in prose,
  without a link.
- Distinguish **observed fact**, **inference** and **recommendation** — the same
  rule AUDITOR imposes on the repositories it audits.
