# AI Bug Hunting Framework

An AI-native bug hunting workspace designed for modern Bug Bounty Programs (BBP).

This repository is **not** a collection of random prompts or Claude Skills. It is a complete operating system for AI-assisted security research where the human researcher leads the investigation and AI accelerates reasoning, analysis, and documentation.

---

# Philosophy

The goal is **not** to let AI autonomously find vulnerabilities.

The goal is to combine:

- Human intuition
- Threat modeling
- Manual verification
- AI reasoning
- Reusable methodology

into a repeatable workflow.

AI proposes hypotheses.

The researcher validates them.

---

# Repository Structure

```
bug-hunting/

├── framework/
├── skills/
├── playbooks/
├── prompts/
├── knowledge/
├── payloads/
├── checklists/
├── engagements/
├── reports/
├── notes/
├── templates/
├── tools/
├── scripts/
└── README.md
```

---

# Folder Overview

## framework/

Core methodology for every engagement.

Contains the standard workflow followed during bug hunting.

Examples:

- Recon
- Feature Mapping
- Threat Modeling
- Hypothesis Generation
- Verification
- Exploit Chaining
- Reporting

---

## skills/

Claude Code Skills.

### community/

Community-maintained skills used as references.

Examples:

- Claude-BugHunter

These should rarely be modified.

### my/

Personal skills.

These represent my own methodology and improve after every engagement.

Organized by:

- Web
- API
- Source Code
- Binary
- Automation
- Reporting
- Feature Analysis
- Hypothesis Generation
- Methodology

---

## playbooks/

Feature-centric attack guides.

Examples:

- Authentication
- Authorization
- Payments
- Organizations
- File Upload
- GraphQL
- OAuth
- JWT

A playbook explains:

- Trust boundaries
- Business logic
- Attack surface
- Common mistakes
- Exploit ideas

---

## prompts/

Reusable prompts for Claude.

Examples:

- Feature Mapping
- Burp Analysis
- Source Review
- API Review
- Threat Modeling
- Generate Hypotheses

---

## knowledge/

Personal security knowledge base.

Examples:

- HackerOne writeups
- PortSwigger research
- CVEs
- Research papers
- Personal notes

Claude should reference this before relying on the internet.

---

## payloads/

Reusable payload collections.

Examples:

- JWT
- SSRF
- GraphQL
- HTTP Smuggling
- Unicode
- Cache Poisoning

---

## checklists/

Manual testing checklists.

Each checklist represents things that should never be forgotten.

Examples:

- Authentication
- IDOR
- File Upload
- OAuth
- Admin Panel
- Business Logic

---

## engagements/

Every bug bounty program gets its own workspace.

Example:

```
engagements/

GitLab/

├── scope.md
├── recon.md
├── hypotheses.md
├── findings.md
├── burp/
├── screenshots/
├── source/
├── notes.md
└── reports/
```

Everything related to one target stays inside its own directory.

---

## reports/

Submitted reports.

Organized by platform.

Examples:

- HackerOne
- Bugcrowd
- Intigriti

---

## notes/

Lessons learned.

Organized by outcome.

Examples:

- Accepted
- Duplicate
- Informative
- N/A

Each note should answer:

- Why did this happen?
- What assumption failed?
- What should be improved?

---

## templates/

Templates for:

- Engagements
- Reports
- Scope
- Threat Models
- Hypothesis Documents

---

## tools/

Tool configuration.

Examples:

- Burp MCP
- Ghidra MCP
- MCP configuration
- Custom utilities

---

## scripts/

Automation scripts.

Examples:

- Recon automation
- Data conversion
- Parsing
- Reporting helpers

---

# Standard Workflow

```
1. Read Program Policy

↓

2. Build Attack Surface

↓

3. Feature Mapping

↓

4. Threat Modeling

↓

5. Generate Hypotheses

↓

6. Manual Testing

↓

7. Exploit Chaining

↓

8. Report Writing

↓

9. Lessons Learned
```

AI assists every stage.

The human researcher makes all final decisions.

---

# Guiding Principles

- AI is a research assistant, not an autonomous hacker.
- Every hypothesis must be manually verified.
- Quality is preferred over quantity.
- Focus on business logic and novel attack paths.
- Reusable methodology is more valuable than reusable prompts.
- Every engagement should improve the framework.

---

# Claude Usage

## Initializing the repository

Run `/init` once at the repository root after major framework changes.

This allows Claude to understand:

- Repository structure
- Methodology
- Folder responsibilities
- Long-term workflow

---

## Working on a target

Do **not** work directly from the repository root.

Create a new directory under:

```
engagements/<platform>-<program>/
```

Example:

```
engagements/hackerone-atlassian/
```

Open Claude from inside that directory.

This keeps context focused on the current engagement while still allowing access to the shared framework.

---

# Continuous Improvement

Every engagement should contribute back to the framework.

Possible improvements include:

- New Claude Skills
- Better prompts
- Better playbooks
- Improved payloads
- New methodologies
- Lessons learned
- Accepted reports
- Research notes

The framework should continuously evolve with experience.

---

# Goal

Build a personal AI-assisted bug hunting platform that improves after every engagement and amplifies human reasoning rather than replacing it.
