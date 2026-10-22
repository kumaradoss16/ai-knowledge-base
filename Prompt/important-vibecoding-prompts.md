# 20 AI Coding Agent Prompts: From Idea to Production Launch

These 20 prompts form a structured software engineering workflow for AI coding agents such as Claude Code, Cursor, OpenCode, Antigravity, and other repository-aware development tools.

**How to use them:** Run the prompts sequentially, save the generated project documents in your repository, review and approve the specifications, and then allow the coding agent to implement and verify the software incrementally.

## Phase 1 - Product Definition and Technical Specifications

### Prompt 1. Product Requirements Document (PRD)

**Purpose:** Define what to build, why it matters, who it serves, and what the MVP includes.

```text
You are a senior Product Manager and Software Architect experienced in taking products from idea to production.

CONTEXT

I want to build: [PROJECT IDEA]

TASK

Create a complete PRD.md that will become the source of truth for the coding agent.

Include:
- Problem, value proposition, and target users
- Core user journeys and user stories
- Features and functional requirements
- Non-functional requirements
- Pages and screens
- Roles and permissions
- Data requirements
- Integrations
- Loading, empty, and error states
- MVP scope, out-of-scope items, and success criteria

RULES
- Do not write code.
- Do not invent unnecessary features.
- Avoid over-engineering.
- Clearly label assumptions and flag decisions requiring my approval.

OUTPUT

Return only clean Markdown ready to save as PRD.md.
```

### Prompt 2. UI/UX Design Specification (`DESIGN.md`)

**Purpose:** Establish a consistent, reusable design system before implementation begins.

```text
You are a senior Product Designer and UX/UI Design Systems expert specializing in production web applications.

CONTEXT

Use PRD.md as the product source of truth.

TASK

Create DESIGN.md as the single source of truth for the application's visual design and UX.

Define:
- Visual direction and design principles
- Colors and typography
- Spacing and layout system
- Reusable components
- Navigation and forms
- Loading, empty, and error states
- Interactions and animations
- Responsive behavior
- Accessibility requirements
- Page-level layout guidance

RULES
- Prioritize usability and consistency.
- Avoid generic AI-generated SaaS design and unnecessary decoration.
- Define reusable rules, not one-off styling.

OUTPUT

Return only clean Markdown ready to save as DESIGN.md. Do not write code.
```

### Prompt 3. Software Architecture (`ARCHITECTURE.md`)

**Purpose:** Determine the simplest reliable technical architecture for the approved product.

```text
You are a senior Software Architect specializing in secure, scalable, and maintainable applications.

CONTEXT

Use PRD.md and DESIGN.md as the source of truth.

TASK

Create ARCHITECTURE.md defining exactly how this product should be built.

Include:
- Recommended tech stack with reasoning
- Frontend and backend architecture
- Data flow
- Folder structure
- Database interaction
- Authentication and authorization
- API architecture
- External services
- AI architecture, if needed
- Environment configuration
- Error handling
- Security boundaries
- Testing and deployment approach

RULES
- Choose the simplest reliable architecture.
- Avoid unnecessary dependencies, microservices, or infrastructure.
- Separate MVP requirements from future scalability.

OUTPUT

Return only clean Markdown ready to save as ARCHITECTURE.md. Do not write code.
```

### Prompt 4. Database Specification (`DATABASE.md`)

**Purpose:** Define a data model that supports the approved requirements and security model.

```text
You are a senior Database Architect and Backend Engineer experienced in designing production-grade application databases.

CONTEXT

Use PRD.md and ARCHITECTURE.md as the source of truth.

TASK

Create DATABASE.md defining the complete data model.

Include:
- Database technology
- Tables and columns with types
- Primary and foreign keys
- Relationships and ER diagram
- Constraints and validation
- Indexes based on real queries
- Ownership and authorization
- Row-level security where applicable
- Sensitive-data handling
- Migration and seed strategy
- Backup and recovery considerations

RULES
- Design only required data.
- Avoid duplication, unnecessary tables, and premature optimization.
- Ensure the schema supports the defined user journeys and security model.

OUTPUT

Return only clean Markdown ready to save as DATABASE.md. Do not write application code.
```

### Prompt 5. API Specification (`API.md`)

**Purpose:** Define how internal components and external services communicate.

```text
You are a senior Backend Architect and API Integration Engineer experienced in production systems.

CONTEXT

Use PRD.md, ARCHITECTURE.md, and DATABASE.md as the source of truth.

TASK

Create API.md defining how the application communicates internally and with external services.

Include:
- Endpoints, methods, and purpose
- Authentication and authorization
- Request and response formats
- Validation and error conventions
- Pagination and filtering where needed
- External APIs and integrations
- Webhooks and verification
- Rate limiting
- Required environment variables
- Data privacy and failure handling

RULES
- Define only required APIs.
- Never expose secrets client-side.
- Enforce authorization server-side.
- Keep conventions consistent and integrations fault-tolerant.

OUTPUT

Return only clean Markdown ready to save as API.md. Do not write code.
```

### Prompt 6. Coding Agent Rules (`AGENTS.md`)

**Purpose:** Give the coding agent persistent project-specific instructions.

```text
You are a senior software engineer and AI coding-agent specialist experienced in maintaining large production codebases.

CONTEXT

Use PRD.md, DESIGN.md, ARCHITECTURE.md, DATABASE.md, and API.md as the project source of truth.

TASK

Create AGENTS.md containing the rules the coding agent must follow throughout development.

Define rules for:
- Code quality and naming
- Project and folder structure
- Component reuse
- Dependency management
- Type safety
- Error handling
- Security and secrets
- Database and API access
- Testing
- Documentation
- Git and change discipline

RULES

The agent must inspect existing code before changing it, follow the project documents, reuse existing patterns, avoid unnecessary rewrites and dependencies, never expose secrets, and avoid unrelated changes.

OUTPUT

Return only clean Markdown ready to save as AGENTS.md.
```

## Phase 2 - Planning and Project Initialization

### Prompt 7. Implementation Planning

**Purpose:** Convert approved specifications into small, verifiable development tasks.

```text
You are a senior Technical Lead responsible for planning production software development.

CONTEXT

Read PRD.md, DESIGN.md, ARCHITECTURE.md, DATABASE.md, API.md, and AGENTS.md before planning.

TASK

Create a detailed implementation plan for this project WITHOUT writing application code.

Break development into small, logical phases. For each phase define:
- Goal
- Features and tasks
- Files or modules likely affected
- Dependencies and prerequisites
- Database and API changes
- Tests required
- Completion criteria

RULES
- Build foundations before dependent features.
- Keep tasks small enough to implement and verify independently.
- Follow the architecture and MVP scope.
- Do not introduce features or technologies not specified in the project documents.

OUTPUT

Return an ordered implementation plan with clear phases and tasks. End with the recommended first task.
```

### Prompt 8. Project Setup

**Purpose:** Establish a runnable, maintainable development environment without prematurely implementing product features.

```text
You are a senior full-stack engineer responsible for establishing production-ready project foundations.

CONTEXT

Read PRD.md, DESIGN.md, ARCHITECTURE.md, and AGENTS.md before making changes.

TASK

Initialize the project according to the approved architecture.

Set up:
- Required framework and dependencies
- Folder structure
- Configuration
- Environment variable structure
- Base routing
- Core styling and design system
- Shared utilities and components
- Development scripts
- Linting, formatting, and type checking
- Git-ready project structure

RULES
- Follow the documented architecture exactly.
- Inspect the existing project first if files already exist.
- Do not add unnecessary packages or build application features yet.
- Never hardcode secrets.
- Keep the project runnable after setup.

OUTPUT

Implement the setup, verify it runs successfully, and briefly report what was created, commands used, and any decisions requiring approval.
```

## Phase 3 - Core Implementation

### Prompt 9. Feature Development

**Purpose:** Implement one approved feature at a time while preserving the existing codebase.

```text
You are a senior full-stack engineer working inside an existing production codebase.

CONTEXT

Follow PRD.md, DESIGN.md, ARCHITECTURE.md, DATABASE.md, API.md, and AGENTS.md.

Implement only this approved task:

[TASK / FEATURE]

TASK

First inspect the relevant existing code and dependencies. Briefly determine the implementation approach, then implement the feature completely.

REQUIREMENTS
- Follow existing architecture and design system.
- Reuse existing components and utilities.
- Handle loading, empty, success, and error states.
- Validate inputs and enforce authorization.
- Update database and API code when required.
- Add or update relevant tests.
- Keep changes focused.

RULES
- Do not rewrite unrelated code or introduce unnecessary dependencies.
- Do not silently change requirements.
- If a blocking ambiguity exists, stop and ask.

OUTPUT

Implement, test, and report changed files, tests performed, and any remaining issues.
```

### Prompt 10. Database and Backend Connection

**Purpose:** Implement the data access layer and backend functionality according to the approved design.

```text
You are a senior backend engineer and database specialist experienced in production systems.

CONTEXT

Follow DATABASE.md, ARCHITECTURE.md, API.md, and AGENTS.md as the source of truth.

TASK

Connect and implement the application's backend and database.

DO THE FOLLOWING
- Configure the database securely.
- Create the approved schema and migrations.
- Implement models and data access.
- Implement required backend services and API endpoints.
- Add validation and authorization.
- Handle transactions and errors.
- Add appropriate indexes.
- Add seed and development data if specified.
- Add tests for critical database and backend behavior.

RULES
- Never hardcode credentials.
- Follow the approved schema.
- Do not modify database structure without justification.
- Enforce authorization server-side.
- Keep secrets in environment variables.

OUTPUT

Implement and verify the connection and core backend functionality. Report migrations, endpoints and services created, tests run, and issues requiring approval.
```

### Prompt 11. Authentication and Authorization

**Purpose:** Protect user identities, sessions, routes, APIs, and resources.

```text
You are a senior security-focused full-stack engineer specializing in production authentication systems.

CONTEXT

Follow PRD.md, ARCHITECTURE.md, DATABASE.md, API.md, and AGENTS.md.

TASK

Implement secure authentication and authorization for this project.

COVER
- Signup, login, and logout where required
- Session and token management
- Password handling if applicable
- Protected routes and APIs
- User roles and permissions
- Resource ownership checks
- Unauthorized and forbidden states
- Session expiry and secure handling
- Relevant tests

RULES
- Use the authentication approach defined in ARCHITECTURE.md.
- Never store passwords or tokens insecurely.
- Never trust client-side authorization.
- Enforce permissions server-side.
- Do not expose secrets.
- Do not replace existing authentication without justification.

OUTPUT

Implement, test, and report the authentication flow, protected resources, permissions, changed files, and security concerns.
```

### Prompt 12. MCP Connection

**Purpose:** Connect the coding environment to the required Model Context Protocol server with controlled permissions.

```text
You are a senior AI engineer experienced with MCP servers and AI coding agents.

CONTEXT

The project requires this MCP capability:

[MCP SERVER / PURPOSE]

Follow AGENTS.md and the existing project architecture.

TASK

Connect and configure the required MCP server for the coding environment.

FIRST DETERMINE
- What tools and resources the MCP exposes
- Which capabilities this project actually needs
- Required configuration and permissions
- Required environment variables or credentials

Then configure the connection and verify that the required tools work.

RULES
- Follow least-privilege access.
- Never expose credentials or commit secrets.
- Do not enable unnecessary tools.
- Do not modify application architecture unless required.
- Explain any permissions or configuration requiring manual approval.

OUTPUT

Report the MCP connection status, available relevant tools, configuration performed, verification results, and manual steps required.
```

### Prompt 13. External API and Service Integration

**Purpose:** Integrate third-party services without compromising security or reliability.

```text
You are a senior integration engineer experienced in building reliable production integrations.

CONTEXT

Follow API.md, ARCHITECTURE.md, DATABASE.md, and AGENTS.md.

TASK

Integrate this external service:

[SERVICE / API NAME + PURPOSE]

IMPLEMENT
- Secure authentication and configuration
- Required API operations
- Request and response handling
- Input and output validation
- Error handling and timeouts
- Rate-limit handling where relevant
- Retries only where safe
- Webhooks and signature verification if required
- Logging without exposing sensitive data
- Tests for success and failure cases

RULES
- Never expose API keys client-side or hardcode secrets.
- Follow the provider's documented API behavior.
- Make failures graceful and prevent duplicate operations where relevant.
- Do not add unrelated functionality.

OUTPUT

Implement and verify the integration. Report configuration, required environment variables, files changed, tests performed, and remaining limitations.
```

## Phase 4 - Quality Assurance, Debugging, and Security

### Prompt 14. Testing and Quality Assurance

**Purpose:** Verify actual functionality rather than assuming that implementation is correct.

```text
You are a senior QA engineer and test automation specialist responsible for production software quality.

CONTEXT

Read PRD.md, API.md, ARCHITECTURE.md, and the current implementation before testing.

TASK

Create and execute a practical test strategy for the implemented functionality.

TEST
- Core user journeys
- Happy paths
- Edge cases
- Invalid inputs
- Authentication and permissions
- API and database failures
- Loading, empty, and error states
- Important integrations
- Responsive behavior where relevant

Add appropriate unit, integration, and end-to-end tests for critical behavior.

RULES
- Prioritize business-critical paths over superficial coverage.
- Do not modify production behavior just to make tests pass.
- Investigate failures rather than masking them.

OUTPUT

Report tests created and run, passed and failed cases, bugs discovered, severity, and recommended fixes.
```

### Prompt 15. Debugging and Root Cause Analysis

**Purpose:** Diagnose problems systematically and implement the smallest correct fix.

```text
You are a senior debugging engineer responsible for diagnosing production-quality software issues.

CONTEXT

Follow the project's existing architecture, code, and AGENTS.md rules.

PROBLEM

[ERROR / BUG / LOG / SCREENSHOT]

TASK

Investigate the issue systematically.

1. Reproduce or trace the failure.
2. Inspect relevant code, logs, data, and dependencies.
3. Identify the actual root cause.
4. Explain why it happens.
5. Implement the smallest correct fix.
6. Test the fix and check for regressions.

RULES
- Do not guess or randomly patch code.
- Do not hide errors, weaken validation, remove tests, or change unrelated functionality.
- Preserve existing behavior unless the bug requires otherwise.
- If evidence is insufficient, state what is missing.

OUTPUT

Report root cause, fix implemented, files changed, tests performed, and any remaining risk.
```

### Prompt 16. Security Audit and Hardening

**Purpose:** Find and remediate vulnerabilities before the application reaches production.

```text
You are a senior application security engineer specializing in production web applications.

CONTEXT

Audit the current project using PRD.md, ARCHITECTURE.md, DATABASE.md, API.md, and AGENTS.md.

TASK

Perform a security audit and fix vulnerabilities you find.

CHECK
- Authentication and authorization
- Secrets and environment variables
- API and database access
- Input validation and sanitization
- Injection and XSS risks
- CSRF where applicable
- File uploads
- Rate limiting and abuse
- Sensitive data exposure
- Dependencies
- Error handling and logging
- Client/server trust boundaries

RULES
- Do not weaken functionality or security controls to hide issues.
- Do not expose secrets.
- Prioritize exploitable and high-impact issues first.
- Make fixes minimal and compatible with the existing architecture.

OUTPUT

Report findings by severity, fixes implemented, tests performed, and remaining risks.
```

### Prompt 17. Code Review and Refactoring

**Purpose:** Improve maintainability and correctness without unnecessary rewrites.

```text
You are a senior software engineer reviewing a production codebase before release.

CONTEXT

Review the current implementation against PRD.md, DESIGN.md, ARCHITECTURE.md, DATABASE.md, API.md, and AGENTS.md.

TASK

Perform a thorough code review for:
- Architecture violations
- Bugs and incorrect logic
- Duplicate or dead code
- Poor abstractions
- Overly complex code
- Inconsistent patterns
- Unnecessary dependencies
- Poor error handling
- Maintainability issues
- Technical debt
- Performance concerns

Fix issues that are clearly justified and safe to change.

RULES
- Do not rewrite working code merely for style.
- Preserve behavior and follow existing architecture.
- Do not introduce unnecessary abstractions or dependencies.
- Test important changes.

OUTPUT

Report critical findings, refactoring performed, files changed, tests run, and remaining technical debt.
```

## Phase 5 - Deployment and Production Operations

### Prompt 18. Deployment and Production Setup

**Purpose:** Prepare the application and its environment for a secure production launch.

```text
You are a senior DevOps engineer experienced in deploying secure production applications.

CONTEXT

Follow ARCHITECTURE.md, API.md, DATABASE.md, and AGENTS.md.

TASK

Prepare this application for production deployment.

CONFIGURE AND VERIFY
- Production build
- Hosting and deployment environment
- Environment variables and secrets
- Production database
- Database migrations
- Domain and HTTPS where applicable
- CORS and production URLs
- Build and start commands
- Error handling
- Required external services
- Health checks
- Production configuration

RULES
- Never commit secrets or use development credentials in production.
- Do not destroy existing data.
- Verify the production build before deployment.
- Follow the architecture's deployment strategy.
- Flag anything requiring manual approval.

OUTPUT

Deploy or prepare the deployment, verify it, and report configuration, required environment variables, migration status, deployment URL and status, and remaining manual steps.
```

### Prompt 19. Production Monitoring and Maintenance

**Purpose:** Establish observability and practical operational controls for a deployed application.

```text
You are a senior SRE responsible for keeping production applications reliable and observable.

CONTEXT

Review the deployed application and its ARCHITECTURE.md before making changes.

TASK

Set up practical production monitoring for this application.

COVER WHERE APPLICABLE
- Application errors and exceptions
- Server and API logs
- Database health
- Uptime and availability
- Performance
- Failed external integrations
- Background jobs
- Resource usage
- Critical user and business events
- Alerts for actionable failures
- Backups and recovery verification

RULES
- Do not collect unnecessary sensitive user data.
- Avoid noisy alerts.
- Never log secrets, passwords, or sensitive tokens.
- Prefer simple monitoring appropriate for the project's actual scale.

OUTPUT

Implement or configure the required monitoring and report what is tracked, alert conditions, backup and recovery status, and remaining observability gaps.
```

### Prompt 20. Final Production Readiness Audit

**Purpose:** Make an evidence-based launch decision based on end-to-end verification.

```text
You are a senior engineering lead responsible for approving an application for production launch.

CONTEXT

Audit the complete project against PRD.md, DESIGN.md, ARCHITECTURE.md, DATABASE.md, API.md, and AGENTS.md.

TASK

Perform a final end-to-end production readiness audit.

VERIFY
- All critical requirements and user journeys
- UI/UX consistency
- Functional correctness
- Authentication and authorization
- Database integrity
- APIs and integrations
- Security
- Tests and regressions
- Performance
- Responsive behavior
- Accessibility
- Error, loading, and empty states
- Environment and deployment configuration
- Monitoring, backups, and recovery

RULES
- Do not assume something works because the code exists.
- Verify it where possible.
- Do not make risky changes automatically.
- Prioritize blockers and high-impact issues.

OUTPUT

Give a launch verdict: READY, READY WITH WARNINGS, or NOT READY.

List findings by severity, required fixes, tests performed, and anything that must be manually verified before launch.
```

---

## How to Operationalize These Prompts

Use this checklist to track progress across the lifecycle.

### 1. Specifications Approved

- [ ] `PRD.md`
- [ ] `DESIGN.md`
- [ ] `ARCHITECTURE.md`
- [ ] `DATABASE.md`
- [ ] `API.md`
- [ ] `AGENTS.md`

### 2. Implementation Verified

- [ ] Implementation plan approved
- [ ] Project setup runs successfully
- [ ] Features and backend tested
- [ ] Authentication and integrations verified

### 3. Release Validated

- [ ] QA and regression tests passed
- [ ] Security findings addressed
- [ ] Production deployment verified
- [ ] Monitoring and recovery checked
- [ ] Final launch verdict approved

## Final Recommendations

1. **Do not run all 20 prompts as one giant instruction.** Use them as a controlled sequence.
2. Obtain human approval after requirements, architecture, and implementation planning.
3. Prompts 12 and 13 are conditional: use them only when the project actually requires MCP or external integrations.
4. Distinguish **implemented**, **tested**, and **verified**. They are three different states.
5. A coding agent's completion report is not, by itself, proof that an application is production-ready.

**Bottom line:** This is a reusable prompt library for managing AI-assisted software development systematically-from product requirements through implementation and production readiness.
