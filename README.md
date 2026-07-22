# FGT AL Developer Plugin

A GitHub Copilot agent plugin for Microsoft Dynamics 365 Business Central AL development. Provides a suite of role-based agents, composable skills, reusable workflows, and coding instructions — all wired together for spec-driven, test-first BC extension development.

## What's Included

### Agents

Four public agents cover the full development lifecycle:

| Agent | Purpose |
|-------|---------|
| `@AL Development Conductor` | Orchestrates the full TDD cycle: Planning → Implementation → Review → Commit |
| `@AL Architecture & Design Specialist` | Solution architecture, data modelling, integration strategy |
| `@AL Implementation Specialist` | Tactical implementation with full AL tooling (debug, API, events, pages, permissions) |
| `@AL Pre-Sales & Project Estimation Specialist` | PERT estimation, SWOT analysis, project sizing |

Three internal subagents are managed automatically by the Conductor:

- **AL Planning Subagent** — research and context gathering
- **AL Implementation Subagent** — RED → GREEN → REFACTOR TDD cycles
- **AL Code Review Subagent** — quality gates and code review

A standalone auditor agent is also provided:

- **`@Dredd`** — Independent, on-demand AL codebase auditor. Judges code against BCQuality, generates reports under `.github/audits/`. Read-only; never modifies AL source.

### Skills (11 composable knowledge modules)

| Skill | Domain |
|-------|--------|
| `skill-api` | API design, OData/REST, versioning |
| `skill-copilot` | Copilot capability lifecycle |
| `skill-debug` | Debugging, profiling, root cause analysis |
| `skill-performance` | Performance patterns and triage |
| `skill-events` | Event subscriber/publisher patterns |
| `skill-permissions` | Permission sets and security |
| `skill-testing` | Test strategy, Given/When/Then |
| `skill-migrate` | Version migration and breaking changes |
| `skill-pages` | Page types and UX patterns |
| `skill-translate` | XLF multi-language support |
| `skill-estimation` | Project estimation and SWOT |

Skills are loaded automatically by agents based on task context — no manual `@file` references needed.

### Workflows (18 prompt-driven workflows)

Activate any workflow with `@workspace use <name>`:

| Workflow | Purpose |
|----------|---------|
| `al-initialize` | Complete environment and workspace setup |
| `al-context.create` | Generate project context for AI assistants |
| `al-memory.create` | Create session memory for continuity |
| `al-build` | Build and deploy extensions |
| `al-spec.create` | Functional-technical specifications |
| `al-diagnose` | Runtime debugging and troubleshooting |
| `al-performance` | Deep performance analysis with CPU profiling |
| `al-performance.triage` | Quick performance diagnosis |
| `al-permissions` | Permission set management |
| `al-pr-prepare` | Pull request preparation |
| `al-translate` | XLF translation file management |
| `al-migrate` | Version migration |
| `al-copilot-capability` | Register a Copilot capability |
| `al-copilot-promptdialog` | Create PromptDialog pages |
| `al-copilot-generate` | AI-assisted code generation |
| `al-copilot-test` | Test with the AI Test Toolkit |

### Instructions

Coding instructions are automatically applied to all `.al` files in your workspace:

- `al-naming-conventions` — Object and field naming rules
- `al-code-style` — Code style and formatting
- `al-error-handling` — Error handling patterns
- `al-events` — Event-driven architecture conventions
- `al-guidelines` — General AL best practices
- `al-performance` — Performance guidance
- `al-testing` — Test codeunit conventions

## Core Principles

- **Extension-only** — Never modifies base application objects. Uses tableextensions, pageextensions, and event subscribers.
- **TDD / spec-driven** — Features follow: `spec.create → architecture → test-plan → implementation → review`.
- **Human-in-the-Loop (HITL)** — All critical decisions require explicit user confirmation.
- **Least privilege** — Generates only the minimum permissions required.
- **BCQuality-cited** — Dredd audits are grounded in BCQuality as the primary authority.

## Quick Routing Guide

```
New feature (complex)?     → @AL Architecture & Design Specialist → al-spec.create → @AL Development Conductor
New feature (simple)?      → al-spec.create → @AL Implementation Specialist
Bug fix / debugging?       → @AL Implementation Specialist
Architecture review?       → @AL Architecture & Design Specialist
Full TDD cycle?            → @AL Development Conductor
Project estimation?        → @AL Pre-Sales & Project Estimation Specialist
Code audit?                → @Dredd
```

## Installation via GitHub Copilot Extensions Marketplace

1. Go to the [GitHub Marketplace](https://github.com/marketplace) and search for **FGT-Developer-Plugin**, or navigate directly to the extension page.
2. Click **Install it for free** (or **Set up a plan** if prompted).
3. Select the GitHub account or organisation to install it on, then click **Install**.
4. Once installed, the plugin becomes available inside GitHub Copilot Chat in VS Code.
5. Open the Copilot Chat panel and type `@` to see the available agents (`@AL Development Conductor`, `@AL Architecture & Design Specialist`, etc.).

> The plugin requires GitHub Copilot (Individual, Business, or Enterprise). Skills and instructions are loaded automatically — no additional configuration is needed after installation.
