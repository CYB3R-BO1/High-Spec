# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## What this repository is

This is **not** a software project — there is no build, lint, or test suite. It is a personal, AI-assisted bug bounty / red-team operating workspace: a structured knowledge base, methodology framework, and per-engagement workspace for security research. The human researcher leads every investigation; Claude proposes hypotheses and accelerates recon/analysis/documentation, but every finding must be manually verified before it is reported.

## Repository structure

```
bug-hunting/
├── framework/       # Core methodology: recon → feature mapping → threat modeling →
│                     hypothesis generation → verification → exploit chaining → reporting
├── skills/
│   ├── community/    # Vendored third-party skill bundles — rarely modified directly
│   │   └── Claude-BugHunter/   # Full plugin: 82 skills, 15 slash commands, `cbh` CLI (see below)
│   └── my/           # Personal skills, organized by: web, api, source, binary, automation,
│                      # reporting, feature-analysis, hypothesis, methodology
├── playbooks/        # Feature-centric attack guides (auth, authz, payments, OAuth, JWT, etc.)
├── prompts/          # Reusable prompts (feature mapping, Burp analysis, source review, threat modeling)
├── knowledge/         # Personal security knowledge base — HackerOne writeups, PortSwigger
│                      # research, CVEs, attack-patterns, frameworks, technologies. Check here
│                      # before relying on the open internet.
├── payloads/          # Reusable payload sets: jwt, ssrf, graphql, http-smuggling, unicode, cache
├── checklists/        # Manual testing checklists (auth, IDOR, file upload, OAuth, business logic)
├── engagements/       # One directory per bug bounty program/target (see below)
├── reports/           # Submitted reports, organized by platform (HackerOne, Bugcrowd, intigriti)
├── notes/             # Lessons learned, organized by outcome: accepted, duplicates, informative, na
├── templates/         # Templates for engagements, reports, scope docs, threat models
├── tools/             # Tool configuration (Burp MCP, Ghidra MCP, custom utilities)
└── scripts/           # Automation: recon, data conversion, parsing, reporting helpers
```

Most top-level directories (`framework/`, `playbooks/`, `prompts/`, `checklists/`, `templates/`, `tools/`, `scripts/`, `skills/my/*`) are currently empty scaffolding — they define where content *should* go as the framework matures with each engagement, not where content currently lives. The one fully populated subtree is `skills/community/Claude-BugHunter/`.

## `skills/community/Claude-BugHunter/`

A vendored, self-contained community skill bundle (82 skills, 15 slash commands, plus a standalone `cbh` CLI). Treat it as a third-party dependency — avoid editing its files directly; if the framework needs different behavior, prefer building it under `skills/my/` instead. Its own docs are authoritative for its internals (`README.md`, `docs/cbh-cli.md`, `docs/architecture.md`, `INSTALL.md`).

Two ways to drive it once installed/loaded:
- **Slash commands inside Claude Code** (primary interface) — `/hunt`, `/recon`, `/scope`, `/surface`, `/triage`, `/validate`, `/report`, `/chain`, `/autopilot`, `/pickup`, `/intel`, `/remember`, `/memory-gc`, `/token-scan`, `/web3-audit`. These use the LLM's judgment and keep state across the conversation.
- **`cbh` CLI** (`skills/community/Claude-BugHunter/scripts/cbh.py`) — deterministic, non-LLM runner for scripted/CI use (bulk passive recon, reproducible lab verification, pre-submit triage gating). Run inline via `python3 scripts/cbh.py <cmd>` from within that directory, or install standalone (`pipx install git+https://github.com/elementalsouls/Claude-BugHunter`). No build step required (stdlib + optional `subfinder`).

Skills in this bundle auto-load by topic based on what's being discussed — they generally don't need to be invoked by name.

## Working on a target

Do not work directly from the repository root when hunting on a real target. Create (or `cd` into) a dedicated workspace first:

```
engagements/<platform>-<program>/
```

e.g. `engagements/hackerone-atlassian/`. Each engagement directory is expected to hold its own `scope.md`, `recon.md`, `hypotheses.md`, `findings.md`, `notes.md`, plus `burp/`, `screenshots/`, `source/`, and `reports/` subfolders. This keeps the working context scoped to the current target while still having access to the shared framework, knowledge base, and skills above it.

## Standard workflow

1. Read program policy / scope
2. Build attack surface (recon)
3. Feature mapping
4. Threat modeling
5. Generate hypotheses
6. Manual testing (AI-assisted, human-verified)
7. Exploit chaining
8. Report writing
9. Lessons learned → feed back into `notes/`, `knowledge/`, and `skills/my/`

## Guiding principles

- AI is a research assistant, not an autonomous hacker — never claim a finding is confirmed without manual verification.
- Quality over quantity; favor business logic and novel attack paths over checklist-only findings.
- Prefer referencing `knowledge/` (personal writeups/CVE notes) before searching the open internet.
- Every engagement should contribute something back to the framework (a new skill, better prompt/playbook, a payload, a lesson in `notes/`) rather than staying siloed in its `engagements/` folder.
