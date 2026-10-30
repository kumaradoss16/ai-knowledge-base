# AI Agent-Ready Project Documentation System

> A practical documentation and context-management standard for AI-assisted software development ("vibe coding") with agents such as Cursor, Claude Code, Windsurf and GitHub Copilot.

## Purpose

Establish a controlled source of truth so coding agents understand product goals, technical boundaries, implementation state, known defects, verification requirements and release procedures throughout the project lifecycle.

Documentation cannot make an AI agent completely hallucination-free. It can substantially reduce unsupported assumptions and unauthorized changes when paired with repository inspection, explicit approval boundaries, tests and evidence-based completion criteria.

## Core recommendation

Use:
- One authoritative documentation directory: `docs/`.
- A root-level `AGENTS.md` as the primary agent instruction entry point.
- Tool-specific instruction files only where needed.
- Separate stable specifications from frequently changing development state.
- Automated quality gates to verify implementation rather than trusting generated claims.

---

# 1. BEFORE - Pre-Coding and Context Injection

Create the foundational specifications before implementation begins. They define what is being built, how it should work and which boundaries agents must respect.

## Foundational files

| File | Purpose | Required contents and agent usage |
|---|---|---|
| `docs/01-foundation/PRD.md` | Product requirements | Product vision, problem statement, target users, user journeys, functional and non-functional requirements, MVP scope, non-goals, assumptions and measurable acceptance criteria. Agents use it as the authority for what the product should do. |
| `docs/01-foundation/SCOPE.md` | Scope control | Included features, excluded features, deferred ideas, MVP boundaries and conditions for expanding scope. Agents must not silently add out-of-scope functionality. |
| `docs/01-foundation/ARCHITECTURE.md` | System architecture | Architecture style, component diagram, module responsibilities, technology boundaries, communication and data flows, integration boundaries, error handling, observability and deployment model. Agents must consult it before introducing services, dependencies or architectural layers. |
| `docs/01-foundation/TECH_STACK.md` | Technology constraints | Approved languages, frameworks, versions, libraries, tooling, runtime requirements and permitted alternatives. Agents must not substitute technologies or add major dependencies without approval. |
| `docs/01-foundation/DESIGN.md` | UI/UX specification | Design principles, color and typography tokens, spacing, components, navigation, layouts, responsive behavior, loading/empty/error states, accessibility and interaction patterns. Frontend agents consult it before creating or changing UI. |
| `docs/01-foundation/DATABASE.md` | Data architecture | Database engine, entities, relationships, keys, constraints, indexes, migrations, validation, transactions, backup/recovery and retention/deletion rules. Agents must read it before changing schemas or persistence behavior. |
| `docs/01-foundation/API_SPECIFICATION.md` | API contract | Endpoints, methods, request/response schemas, validation, authentication, authorization, error formats, versioning and compatibility rules. Agents must follow it when implementing or changing API contracts. |
| `docs/01-foundation/SECURITY.md` | Security requirements | Threat model, trust boundaries, authentication, authorization, secret handling, input validation, permissions, data protection, logging restrictions and prohibited operations. Agents must consult it before implementing security-sensitive features or tool execution. |
| `docs/01-foundation/AGENT_WORKFLOW.md` | Agent operating workflow | Task intake, context-loading order, planning/approval process, implementation boundaries, verification steps, handoff requirements and escalation conditions. Agents use it to follow the team's development process. |
| `AGENTS.md` | Primary agent instructions | Project summary, mandatory reading order, authoritative sources, coding conventions, directory boundaries, dependency policy, security rules, testing requirements, Git conventions, prohibited actions, approval boundaries and definition of done. Every coding agent should read it first. |

### Minimum content examples

#### PRD.md

```markdown
# Product Requirements Document

## Product Vision
Describe the product and the problem it solves.

## Target Users
Identify primary and secondary users.

## Functional Requirements
- FR-001:
- FR-002:
- FR-003:

## Non-Functional Requirements
- Performance
- Reliability
- Security
- Accessibility

## MVP Scope
Features required for the first usable release.

## Out of Scope
Features that must not be implemented in the MVP.

## Acceptance Criteria
Define objectively verifiable completion conditions.
```

#### ARCHITECTURE.md

Include:
- System architecture and component diagram.
- Technology stack and versions.
- Module responsibilities and ownership.
- Frontend/backend boundaries.
- Data and execution flows.
- Integration boundaries.
- Error-handling and observability strategy.
- Deployment model and architecture constraints.

#### DESIGN.md

Include:
- Design philosophy and visual hierarchy.
- Design tokens, colors, typography and spacing.
- Component specifications and page layouts.
- Navigation and interaction behavior.
- Responsive rules.
- Accessibility requirements.
- Loading, empty, error and success states.

#### DATABASE.md

Include:
- Database engine and supported version.
- Entity definitions and relationships.
- Primary/foreign keys and constraints.
- Indexing and query expectations.
- Migration and rollback policy.
- Validation and transaction requirements.
- Backup, recovery, retention and deletion rules.

#### AGENTS.md

Example baseline:

```markdown
# Agent Instructions

## 1. Mandatory Reading
Read this file first, then the relevant product and engineering
specifications in docs/ before implementation.

## 2. Engineering Rules
- Inspect existing implementation before modifying it.
- Follow the approved architecture and technology stack.
- Reuse existing components and services.
- Avoid unnecessary dependencies and duplicated functionality.
- Do not silently change public interfaces.

## 3. Security Rules
- Never hardcode credentials.
- Never expose secrets in logs.
- Validate untrusted inputs.
- Follow least-privilege principles.

## 4. Development Rules
- Plan changes before implementation.
- Write or update tests for changed behavior.
- Run relevant tests and report actual results.
- Do not claim tests passed if they were not executed.

## 5. Approval Requirements
Obtain human approval before:
- Changing the architecture.
- Adding major dependencies.
- Performing destructive operations.
- Removing existing features.
- Changing production data or migration strategy.

## 6. Completion Report
Report changed files, behavior implemented, tests executed,
test results, known limitations and remaining work.
```

---

# 2. DURING - Active Development and State Tracking

The repository, not conversation history, must preserve the current project state. Update state documents after meaningful milestones and verify them against the actual codebase.

## Development tracking files

| File | Purpose | Agent usage |
|---|---|---|
| `docs/02-development/TASKS.md` | Milestone roadmap and task breakdown | Read before selecting work. Each task should have an ID, priority, dependencies, acceptance criteria, status and validation evidence. Update after implementation and verification. |
| `docs/02-development/TODO.md` | Short-term follow-ups | Track small outstanding actions and immediate next steps. Keep it concise; move substantial work into TASKS.md. |
| `docs/02-development/BUGS.md` | Reproducible defects | Record environment, reproduction steps, expected/actual behavior, severity, status and resolution. Check it before changing affected components. |
| `docs/02-development/KNOWN_ISSUES.md` | Accepted limitations | Record current limitations and their impact. Agents must distinguish accepted limitations from defects and avoid treating workarounds as permanent fixes. |
| `docs/02-development/CURRENT_STATE.md` | Current implementation snapshot | Read at the start of each new session. Summarize completed work, active task, blockers, recent decisions, validation status and next actions. Verify against source code before relying on it. |
| `docs/02-development/TEST_PLAN.md` | Validation strategy | Define unit, integration, end-to-end, security, recovery and performance tests. Agents use it to determine how changes must be validated. |
| `docs/02-development/DECISIONS.md` | Decision index | Record significant engineering choices and link to detailed ADRs. Agents consult it before revisiting previously settled decisions. |
| `docs/02-development/CHANGELOG.md` | Change history | Record meaningful changes by version or date. Do not use it as a substitute for task status or session memory. |

### TASKS.md example

```markdown
# Development Tasks

## Phase 1: Foundation
- [x] Initialize repository
- [x] Configure frontend
- [x] Configure backend
- [ ] Implement application shell

## Phase 2: Core Features
- [ ] Implement authentication
- [ ] Implement project management
- [ ] Implement persistence
```

Every substantial task should include:
- Unique ID and title.
- Priority and status.
- Description and dependencies.
- Acceptance criteria.
- Relevant files or modules.
- Validation commands and evidence.

Example:

```markdown
## TASK-014: Implement workflow persistence

Status: IN_PROGRESS
Priority: P0

### Requirements
- Persist workflow definitions.
- Persist task execution states.
- Recover interrupted workflows.

### Acceptance Criteria
- Workflow survives application restart.
- Invalid transitions are rejected.
- Recovery tests pass.

### Dependencies
- TASK-008: Database initialization
```

### CURRENT_STATE.md example

```markdown
# Current Project State

## Last Updated
YYYY-MM-DD

## Current Phase
Phase 2 - Core Features

## Completed
- Repository initialized.
- Frontend application shell implemented.
- Database initialized.

## Currently Working On
- Workflow persistence.

## In Progress
- Workflow state transitions.

## Known Problems
- Recovery after interrupted execution is incomplete.

## Recent Decisions
- SQLite is the authoritative workflow metadata store.

## Next Actions
1. Complete workflow persistence.
2. Add restart recovery tests.
3. Validate state transitions.

## Validation Status
- Unit tests: PASS
- Integration tests: PENDING
- Security checks: PENDING
```

If this file conflicts with the implementation, the agent must investigate and report the discrepancy rather than assume the documentation is correct.

### BUGS.md example

```markdown
# Known Bugs

## BUG-001: Workflow execution stops after restart

Status: OPEN
Severity: HIGH

### Environment
- OS: Windows 10
- Application version: 0.1.0

### Steps to Reproduce
1. Start workflow.
2. Close application during execution.
3. Restart application.

### Expected Result
Workflow state is recovered.

### Actual Result
Workflow remains stuck.

### Suspected Cause
Recovery handler does not restore execution state.

### Resolution
Pending investigation.
```

### DECISIONS.md and ADRs

Use a concise decision index in DECISIONS.md and store substantial records in `docs/adr/`.

Example ADR:

```markdown
# ADR-001: Use SQLite

Status: ACCEPTED

## Context
The application is local-first.

## Decision
Use SQLite for workflow metadata and execution state.

## Alternatives
- PostgreSQL
- MongoDB

## Reason
SQLite provides persistent local storage without requiring
an external database service.

## Consequences
- Database migrations are required.
- Concurrent writes must be controlled.
```

## Memory management

Use a small, structured memory directory. Memory documents are supporting context, not architectural authority.

| File | Purpose |
|---|---|
| `docs/03-memory/PROJECT_CONTEXT.md` | Stable project facts, constraints and terminology. |
| `docs/03-memory/SESSION_LOG.md` | Brief summaries of completed development sessions. |
| `docs/03-memory/TECHNICAL_NOTES.md` | Implementation discoveries and important technical details. |
| `docs/03-memory/WORKAROUNDS.md` | Temporary fixes, why they exist and conditions for removing them. |
| `docs/03-memory/NEXT_SESSION.md` | Exact handoff instructions for the next coding session. |

Example NEXT_SESSION.md:

```markdown
# Next Session Handoff

## Current Objective
Complete workflow persistence.

## Last Completed Work
Database repository and workflow models implemented.

## Remaining Work
- Implement transaction handling.
- Add recovery tests.
- Verify interrupted execution behavior.

## Important Files
- backend/app/domain/workflow.py
- backend/app/infrastructure/database.py

## Known Blockers
Recovery logic does not yet restore pending tasks.

## First Action
Inspect the workflow repository and recovery tests
before modifying implementation.
```

If session notes conflict with the PRD, architecture or actual code, investigate and flag the discrepancy.

---

# 3. AFTER - Production, Handoff and Maintenance

Create and verify these documents before the corresponding release or handoff activity.

| File | Purpose | Required contents and agent usage |
|---|---|---|
| `README.md` | Project entry point | Product overview, features, screenshots, stack, prerequisites, setup, development/test commands, project structure and links to detailed docs. Keep it accurate as the first point of entry. |
| `docs/04-release/INSTALLATION.md` | Installation guide | Supported platforms, prerequisites, installation steps, configuration, verification and uninstall/update instructions. Agents use it to produce reproducible setup instructions. |
| `docs/04-release/DEPLOYMENT.md` | Build and release operations | Build prerequisites, environment configuration, packaging, migrations, secret management, versioning, rollback and release verification. Consult before packaging or deploying. |
| `docs/04-release/TROUBLESHOOTING.md` | Diagnostic guide | Verified error messages, affected environments, root causes, diagnostic commands and confirmed resolutions. Do not add speculative fixes as facts. |
| `docs/04-release/USER_GUIDE.md` | User documentation | Application concepts, features, workflows, settings and safe operating instructions. Keep it aligned with released behavior. |
| `docs/04-release/CONTRIBUTING.md` | Contribution standards | Branching, coding conventions, testing, commit messages, pull requests and review requirements. |
| `docs/04-release/TEST_REPORT.md` | Release validation evidence | Build status, test results, security checks, performance results, known defects and release recommendation. Report actual evidence. |
| `docs/04-release/RELEASE_NOTES.md` | Release communication | New features, fixes, breaking changes, migration notes and known limitations by release. |
| `docs/04-release/SUPPORT.md` | Support and maintenance | Issue reporting, support boundaries, maintenance ownership and escalation expectations. |
| `LICENSE` | Legal terms | License governing use, modification and redistribution. Choose intentionally; do not invent licensing terms. |

### DEPLOYMENT.md checklist

- Build prerequisites and supported environments.
- Environment configuration.
- Build and packaging commands.
- Database migration and rollback procedures.
- Secret management.
- Release versioning.
- Backup and recovery.
- Post-deployment verification.

### TROUBLESHOOTING.md entry format

- Error message and symptoms.
- Affected version and environment.
- Diagnostic steps and commands.
- Verified root cause.
- Confirmed resolution.
- Workaround and removal condition, if applicable.

### TEST_REPORT.md checklist

- Build status.
- Unit test results.
- Integration test results.
- End-to-end test results.
- Security validation.
- Performance and reliability results.
- Known defects and release risks.
- Release recommendation.

---

# 4. Recommended directory structure

This is a target structure for a mature AI-assisted project. It does not mean every file must be created on day one.

```text
project-root/
│
├── .github/
│   ├── workflows/
│   │   ├── ci.yml
│   │   └── release.yml
│   └── copilot-instructions.md
│
├── .cursor/
│   └── rules/
│       ├── general.mdc
│       ├── frontend.mdc
│       ├── backend.mdc
│       ├── database.mdc
│       └── security.mdc
│
├── .claude/
│   └── rules/
│       ├── frontend.md
│       ├── backend.md
│       └── security.md
│
├── docs/
│   ├── 01-foundation/
│   │   ├── PRD.md
│   │   ├── SCOPE.md
│   │   ├── ARCHITECTURE.md
│   │   ├── TECH_STACK.md
│   │   ├── DESIGN.md
│   │   ├── DATABASE.md
│   │   ├── API_SPECIFICATION.md
│   │   ├── SECURITY.md
│   │   └── AGENT_WORKFLOW.md
│   │
│   ├── 02-development/
│   │   ├── TASKS.md
│   │   ├── TODO.md
│   │   ├── BUGS.md
│   │   ├── KNOWN_ISSUES.md
│   │   ├── CURRENT_STATE.md
│   │   ├── TEST_PLAN.md
│   │   ├── DECISIONS.md
│   │   └── CHANGELOG.md
│   │
│   ├── 03-memory/
│   │   ├── PROJECT_CONTEXT.md
│   │   ├── SESSION_LOG.md
│   │   ├── TECHNICAL_NOTES.md
│   │   ├── WORKAROUNDS.md
│   │   └── NEXT_SESSION.md
│   │
│   ├── 04-release/
│   │   ├── INSTALLATION.md
│   │   ├── DEPLOYMENT.md
│   │   ├── TROUBLESHOOTING.md
│   │   ├── USER_GUIDE.md
│   │   ├── CONTRIBUTING.md
│   │   ├── TEST_REPORT.md
│   │   ├── RELEASE_NOTES.md
│   │   └── SUPPORT.md
│   │
│   └── adr/
│       ├── ADR-001-example.md
│       └── ADR-002-example.md
│
├── apps/
│   └── desktop/
│
├── backend/
│
├── frontend/
│
├── tests/
│   ├── unit/
│   ├── integration/
│   └── e2e/
│
├── scripts/
│
├── .env.example
├── .gitignore
├── AGENTS.md
├── README.md
├── LICENSE
└── pyproject.toml / package.json
```

### Structural rules

- Keep root `AGENTS.md` discoverable and concise.
- Keep tool-specific rules in the corresponding tool configuration directory.
- Do not duplicate complete specifications across agent instruction files.
- Keep stable product/engineering requirements separate from changing development state.
- Keep ADRs durable and individually addressable.
- Use the conventions supported by each coding tool; do not assume every tool automatically reads every instruction file.
- Add only the application directories and build files that match the chosen stack.

---

# 5. Golden rules for the human orchestrator

## Rule 1 - Maintain one source of truth

Do not maintain competing versions of the same requirement.

- PRD.md owns product requirements.
- ARCHITECTURE.md owns system architecture.
- DESIGN.md owns UI/UX decisions.
- DATABASE.md owns data constraints.
- CURRENT_STATE.md owns the latest development status.

Other documents should link to authoritative sources rather than copying them wholesale.

## Rule 2 - Require context injection before every task

A task-start procedure should require the agent to:
1. Read root AGENTS.md.
2. Read relevant foundation documents.
3. Read CURRENT_STATE.md.
4. Inspect the actual source files involved.
5. Identify dependencies and risks.
6. Propose an implementation plan.
7. Obtain approval when a change crosses an approval boundary.

Do not let an agent implement a substantial change based only on a short natural-language request.

## Rule 3 - Never mark work complete without evidence

Require relevant automated tests, build verification, lint/type checks where applicable, manual verification for uncovered behavior, changed-file reporting and known limitations. A task is complete only when its acceptance criteria are satisfied.

## Rule 4 - Update state after meaningful milestones

Update the documents whose information changed:
- TASKS.md for task status.
- CURRENT_STATE.md for implementation status and next actions.
- BUGS.md for reproducible defects.
- CHANGELOG.md for significant changes.
- DECISIONS.md/ADRs for important decisions.
- NEXT_SESSION.md when work will continue in another session.

Do not mechanically update every file after every small code edit.

## Rule 5 - Separate planning, implementation and verification

Use three controlled stages:

### PLAN
Inspect requirements and code, identify dependencies, propose changes and define acceptance criteria.

### IMPLEMENT
Modify approved files, follow architecture rules and add tests.

### VERIFY
Run tests, inspect the diff, review security implications and update project state and documentation.

---

# 6. Minimum set to create before the first line of application code

The full directory structure is a lifecycle target, not a day-one checklist.

| # | File | Before coding? |
|---:|---|---|
| 1 | `AGENTS.md` | Yes |
| 2 | `docs/01-foundation/PRD.md` | Yes |
| 3 | `docs/01-foundation/ARCHITECTURE.md` | Yes |
| 4 | `docs/01-foundation/TECH_STACK.md` | Yes |
| 5 | `docs/01-foundation/DESIGN.md` | Before UI implementation |
| 6 | `docs/01-foundation/SECURITY.md` | Yes, baseline rules |
| 7 | `docs/02-development/TASKS.md` | Yes |
| 8 | `docs/02-development/TEST_PLAN.md` | Yes |
| 9 | `.gitignore` | Yes |
| 10 | `README.md` | Basic version |

Create DATABASE.md and API_SPECIFICATION.md before implementing their respective subsystems. For database-heavy or API-first systems, define them during initial design.

For products where a subsystem is central to product behavior, its specification is foundational. For example, an AI workflow orchestrator should define execution states, transitions, retries, persistence, interruption recovery and approval gates before implementing the execution engine.

## Final principle

Treat documentation as a living engineering control system:
- Define boundaries before coding.
- Track verified reality during development.
- Require evidence before marking work complete.
- Document reproducible operations before release.

The goal is not maximum documentation volume. The goal is the smallest accurate set of documents that keeps every human and AI contributor aligned.
