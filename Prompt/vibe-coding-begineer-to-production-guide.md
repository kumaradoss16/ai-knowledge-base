# Vibe Coding: A Complete Beginner-to-Production Guide

Based on your uploaded Markdown file, the guide should take you through the entire software development lifecycle-from defining an idea to operating a deployed application. The key is to combine AI-assisted coding with engineering practices: documentation, incremental implementation, testing, security, version control, and production monitoring.

I'll preserve the source's core workflow and examples while organizing it into a practical, visually structured guide with clear stages, checklists, and reusable prompts.

## The complete workflow

<img width="560" height="403" alt="image" src="https://github.com/user-attachments/assets/17bc4de7-036f-4b7a-8431-1b4b0dd712cf" />


## Phase 1 - Define the product

Before asking an AI coding tool to build anything, answer five questions.

<img width="562" height="327" alt="image" src="https://github.com/user-attachments/assets/d3a1cb3b-ba15-4516-b99b-5d0a08d80b7b" />


Research users, competing products, technical feasibility, APIs, authentication, database needs, hosting and operating costs. Prefer official technical documentation when making implementation decisions.

## Phase 2 - Choose your tools and stack

The uploaded guide identifies these AI coding tools and their typical use cases.

| Tool        | Typical use                                          |
| ----------- | ---------------------------------------------------- |
| Replit      | Browser-based development and prototypes             |
| Lovable     | UI-focused web apps and SaaS MVPs                    |
| Bolt        | Rapid web application prototypes                     |
| Cursor      | Local development and existing repositories          |
| Claude Code | Terminal-based, repository-level agentic development |

Its recommended example stack is:

<img width="555" height="310" alt="image" src="https://github.com/user-attachments/assets/8e22e0f6-d7c8-479d-ba2d-8a0cc02cee02" />


This is the guide's suggested stack, not a universal requirement. Choose the simplest stack that satisfies your application's actual needs.

### Set up your development environment

Install the required tools for this example stack:

- Cursor or VS Code
- Git
- Node.js LTS and npm
- A GitHub account
- A modern web browser

Optional tools include Docker, GitHub CLI, Postman or Bruno, a database client and Vercel CLI.

Verify the installation:

```
node --version
npm --version
git --version
```

Create a project and initialize version control:

```
mkdir student-dashboard
cd student-dashboard
git init
```

Create a GitHub repository and connect it to your local project. Use Git from the beginning so that you can inspect changes and recover from unwanted AI modifications.

## Phase 3 - Create the project documentation

The guide treats project documentation as persistent context for the AI coding agent.

### Recommended project structure

student-dashboard/ ├── docs/ │   ├── PRD.md │   ├── ARCHITECTURE.md │   ├── DESIGN.md │   ├── TEST_PLAN.md │   ├── SECURITY.md │   ├── DECISIONS.md │   └── MEMORY.md ├── .cursor/ │   └── rules/ ├── src/ ├── tests/ │   ├── unit/ │   ├── integration/ │   └── e2e/ ├── public/ ├── .env.example ├── .gitignore ├── README.md ├── RULES.md └── TASKS.md

The structure is illustrative. Add folders and files as the project requires.

### What each document must define

| Document          | Responsibility                                                           |
| ----------------- | ------------------------------------------------------------------------ |
| `PRD.md`          | What you are building and why                                            |
| `ARCHITECTURE.md` | Components, data flow, folder structure and technical boundaries         |
| `DESIGN.md`       | Colors, typography, reusable components and UX behavior                  |
| `RULES.md`        | Coding standards and AI constraints                                      |
| `TASKS.md`        | Prioritized tasks, dependencies and completion status                    |
| `DECISIONS.md`    | Important technical decisions and their rationale                        |
| `MEMORY.md`       | Current project state, known issues and next step                        |
| `TEST_PLAN.md`    | Test scenarios and acceptance checks                                     |
| `SECURITY.md`     | Authentication, authorization, secrets and input-validation requirements |
| `.env.example`    | Required configuration variable names, without real secrets              |
| `README.md`       | Setup instructions and project documentation                             |

For a small beginner project, start with `PRD.md`, `RULES.md`, `TASKS.md`, `README.md`, `.env.example` and `.gitignore`. Expand the documentation when complexity justifies it.

### Example: define the product in `PRD.md`

```
# Product Requirements Document

## Product
StudentHub

## Problem
Students struggle to manage academic notes,
assignments and deadlines.

## Target Users
BCA, BSc CS and BTech students.

## Core Features
1. Authentication
2. Dashboard
3. Notes
4. Assignments
5. Deadlines

## MVP
- Sign up and log in
- Create, edit and delete notes
- Create assignments
- Mark assignments complete

## Out of Scope
- Payments
- AI tutor
- Social feed
- Mobile application

## Success Criteria
Users can authenticate, manage notes,
create assignments and mark them complete.
```

### Define the architecture and design

`ARCHITECTURE.md` should describe the selected stack, component responsibilities, data flow and security boundaries. The source's example architecture is:

<img width="561" height="332" alt="image" src="https://github.com/user-attachments/assets/ba8750bf-6b01-4bed-9381-b2b30ae07f8d" />


Document boundaries such as:

- UI components should not contain database access logic.
- Database operations belong in a defined service or data-access layer.
- Authentication and authorization must be enforced server-side.
- Business logic should remain separate from presentation code.

`DESIGN.md` should define consistent typography, color tokens, buttons, cards, responsive layouts, loading states, empty states, error states and accessible forms.

## Phase 4 - Establish AI coding rules and tasks

Use `RULES.md` as the project's AI rulebook. The source recommends rules such as:

- Read relevant documentation and inspect existing code before editing.
- Reuse existing components and functionality.
- Avoid duplicate logic and unrelated file changes.
- Follow the documented design system and architecture.
- Never expose API keys.
- Validate input and enforce authorization server-side.
- Add and run tests for important functionality.
- Use small, descriptive Git commits.

For Cursor, these rules can also be split into `.cursor/rules/` files, such as `general.mdc`, `frontend.mdc`, `backend.mdc` and `testing.mdc`.

### Break work into small tasks

Example `TASKS.md`:

```
# Tasks

## Phase 1: Setup
- [ ] Initialize project
- [ ] Configure TypeScript
- [ ] Configure Tailwind
- [ ] Configure Git

## Phase 2: Authentication
- [ ] Create signup page
- [ ] Create login page
- [ ] Configure authentication
- [ ] Protect dashboard
- [ ] Test authentication

## Phase 3: Notes
- [ ] Create database table
- [ ] Create notes service
- [ ] Create notes UI
- [ ] Add note creation
- [ ] Add edit functionality
- [ ] Add delete functionality
- [ ] Add tests
```

Maintain a separate `DECISIONS.md` for durable technical decisions and `MEMORY.md` for the current task, completed work, known issues and next step.

## Phase 5 - Give the AI the right context

Do not start with “Build my entire application.”

Use a planning-only prompt first:

# Initial AI Project Review

You are the coding agent responsible for implementing this project.

Before making any changes, read:

- `PRD.md`
- `ARCHITECTURE.md`
- `DESIGN.md`
- `RULES.md`
- `TASKS.md`

First:

1. Explain your understanding of the product and MVP.
2. Summarize the architecture and design requirements.
3. Identify missing requirements, contradictions and technical risks.
4. Inspect the existing repository and identify reusable functionality.
5. Review the dependencies and development environment.
6. Propose an implementation plan for the first incomplete task.

**Constraints**

- Do not write or modify code yet.
- Do not install dependencies or change configuration.
- Do not invent missing requirements.
- Identify assumptions and request clarification where necessary.

Return the findings, risks and proposed plan for review before implementation.

Once the plan is approved, proceed one task at a time.

## Phase 6 - Implement one feature at a time

The source recommends this development loop:

<img width="560" height="397" alt="image" src="https://github.com/user-attachments/assets/549e973b-24e5-4232-be81-28e534820183" />


### Use vertical slices

Instead of completing the entire frontend, then the entire backend and then the database, implement complete user workflows.

For a notes application:

1. Create a note form.
2. Validate the submitted fields.
3. Save the note through the server-side data layer.
4. Display the saved note.
5. Edit and save an existing note.
6. Delete a note and update the interface.
7. Test the complete flow.

This approach makes errors easier to isolate and ensures that each increment delivers usable functionality.

### Reusable feature implementation prompt

# Implement One Feature

## Context

We are building a student notes application. Read the relevant project documentation and inspect the existing implementation before editing.

## Task

Implement: [ONE SPECIFIC FEATURE]

## Relevant Files

[LIST RELEVANT FILES OR DIRECTORIES]

## Constraints

- Follow `PRD.md`, `ARCHITECTURE.md`, `DESIGN.md` and `RULES.md`.
- Reuse existing components and services where appropriate.
- Do not introduce a duplicate data-access layer.
- Do not modify unrelated files.
- Validate inputs and enforce server-side authorization.
- Do not add dependencies unless necessary and approved.

## Acceptance Criteria

- [LIST OBSERVABLE EXPECTED BEHAVIORS]
- Invalid input produces appropriate errors.
- Loading, success, empty and failure states are handled where applicable.
- Data persists correctly where persistence is required.
- Users cannot access resources they do not own.

## Verification

1. Add or update appropriate tests.
2. Run linting, type checking and relevant tests.
3. Run a production build when appropriate.
4. Report actual command results and any failures.

## Final Report

List changed files, implemented behavior, tests executed, known limitations and remaining issues. Distinguish verified results from unverified assumptions.

## Phase 7 - Test and debug systematically

After each meaningful implementation, run the checks supported by the project:

```
npm run lint
npm run typecheck
npm test
npm run build
```

These are example commands from the guide; the project must define the corresponding scripts. Do not report a check as passed if it was not actually executed.

### Testing layers

<img width="551" height="156" alt="image" src="https://github.com/user-attachments/assets/fc4efdd5-fab8-4cbb-a4ec-d77e6ce0f5de" />


An example end-to-end test should cover signup, login, note creation, page refresh, note persistence, editing, deletion and logout.

### Debug with evidence

When something fails, provide the actual error, expected behavior, observed behavior, reproduction steps and constraints.

# Debugging Prompt

Investigate the following issue without changing code initially.

## Error

[PASTE THE ACTUAL ERROR]

## Expected Behavior

[WHAT SHOULD HAPPEN]

## Actual Behavior

[WHAT HAPPENS INSTEAD]

## Reproduction Steps

[MINIMAL STEPS TO REPRODUCE]

## Constraints

[FILES, DATABASE SCHEMA OR BEHAVIOR THAT MUST NOT CHANGE]

First identify the root cause. Explain the failing component, supporting evidence, smallest appropriate fix and how to verify it.

Do not refactor unrelated code.

Wait for approval before implementing the fix. After approval, implement the minimal change and run the relevant tests.

## Phase 8 - Review security and code quality

Before production, review the implementation against the PRD, architecture, design system, rules, test plan and security requirements.

The review should cover:

- Functional correctness and business logic
- Authentication and server-side authorization
- Database access policies and ownership checks
- Input validation and API request validation
- Secret management and accidental exposure
- Error handling and logging
- Accessibility and keyboard navigation
- Responsive behavior and performance
- Duplicate code and unnecessary complexity

Ask the AI to report problems before asking it to fix them. Review proposed changes, then test the fixes.

### Protect secrets

Keep real values in local environment files and the deployment platform's secret configuration. Commit only a placeholder template.

Example `.env.example`:

```
DATABASE_URL=
SUPABASE_URL=
SUPABASE_ANON_KEY=
OPENAI_API_KEY=
STRIPE_SECRET_KEY=
```

Never place actual credentials in source code or commit local secret files. Client-side environment variables must not contain secrets.

## Phase 9 - Version control and release preparation

After a working, verified feature:

```
git status
git add .
git commit -m "feat: add note creation"
git push
```

Review changes before staging them. For larger projects, use feature branches and review changes before merging.

### Pre-deployment checklist

### Functionality

Signup, login and logout work

CRUD operations and forms work

Errors, loading and empty states work

### User experience

Mobile, tablet and desktop checked

Accessibility and keyboard navigation checked

### Security

No secrets committed to Git

Authentication and authorization verified

Database policies and input validation checked

### Engineering

Lint and type checks pass

Relevant automated tests pass

Production build succeeds

## 0 / 11

Release checks marked complete

Reset

This checklist tracks your selections; it does not execute tests or independently certify release readiness.

## Phase 10 - Preview, deploy and verify production

The source's deployment pipeline is:
<img width="558" height="325" alt="image" src="https://github.com/user-attachments/assets/dd8893e2-5ee7-42ce-bd8c-f5ca1e1e9506" />


For the example Next.js stack, the guide describes connecting GitHub to Vercel, configuring environment variables, deploying a preview, testing it and then promoting the verified version to production.

Keep development, preview and production configuration separate. Test the actual live URL rather than relying only on localhost.

### Production QA

Check the deployed application for:

- Signup, login and core features
- Database reads and writes
- Direct URLs and page refreshes
- Logged-out access to protected routes
- Invalid input and incorrect credentials
- Slow network behavior and error handling
- Empty database states
- Mobile and desktop layouts

### Monitor and maintain

After release, establish appropriate error tracking, performance monitoring, uptime checks and database backups. Collect feedback, fix issues, test changes and redeploy.

Update `TASKS.md`, `MEMORY.md`, `DECISIONS.md`, `README.md` and `ARCHITECTURE.md` whenever the implementation materially changes.

## Final reference: the complete engineering loop

## For every feature

<img width="556" height="273" alt="image" src="https://github.com/user-attachments/assets/38c09e7e-3f61-4a91-8d85-7aab40becab3" />


The standard for production readiness: requirements are met, relevant tests have actually passed, security controls are verified, deployment has been tested, and operational monitoring and recovery procedures are in place. AI-generated code is a starting point for verification-not proof that the application is production-ready.
