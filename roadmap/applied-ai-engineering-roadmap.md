# Applied AI Engineering Master Roadmap

Beginner → Intermediate → Advanced → Production-Ready AI Engineer

This roadmap combines the engineering depth of the original Applied AI Engineering Roadmap with all nine skills from the broader AI skills roadmap. It is designed to help you build, deploy, secure and maintain production-ready AI products and SaaS applications using existing hosted and open-source models—without training foundation models from scratch.

The roadmap follows one principle: learn a concept, implement it, evaluate it, and integrate it into a real product. You will progress from basic LLM API usage to retrieval systems, automation, tool-using agents, multimodal applications and production operations.

## Roadmap at a glance

<img width="477" height="176" alt="image" src="https://github.com/user-attachments/assets/6784564e-e20a-488b-9973-25771632cba3" />


Expected duration: approximately 6–9 months part-time, depending on your implementation time and prior experience. You can move faster through familiar Python, web and infrastructure topics, but do not skip production validation.

## Phase 1 — Applied AI and LLM fundamentals

Beginner

Objective: Understand how existing AI models work and select the right model and integration approach for a given problem.

### Main topics and subtopics

1\. AI and LLM foundations

- AI, machine learning, deep learning and generative AI: practical distinctions
- Foundation models, LLMs, vision-language models and embedding models
- Tokens, tokenization, context windows and output limits
- Training versus inference; pretraining versus fine-tuning
- Hosted models versus local inference
- Model limitations, hallucinations, nondeterminism and knowledge cutoffs

2\. Model selection

- General-purpose versus reasoning models
- Fast, low-cost models versus high-capability models
- Context length, latency, throughput and price
- Open-weight models and their deployment requirements
- Provider capabilities, data retention and usage terms
- Choosing models by measured task performance rather than popularity

3\. AI application patterns

- Direct model request and response
- Classification, extraction, summarization and generation
- Embeddings and semantic similarity
- Retrieval-augmented generation (RAG)
- Tool calling and agentic workflows
- When not to use an LLM: deterministic code, SQL queries and conventional search

4\. Practical API foundations

- API keys, environment variables and HTTP requests
- Request and response schemas
- Timeouts, error handling and rate limits
- Streaming responses
- Token usage and cost estimation

Technologies: Python, `httpx`, official provider SDKs, hosted LLM APIs, Ollama.

Practical project: Build a command-line AI utility that summarizes technical documents, classifies issues and extracts structured information.

Mastery gate: Explain why a task needs a particular model, measure its latency and cost, handle API failures, and identify cases where ordinary code is more appropriate.

## Phase 2 — Prompt engineering and context engineering

Beginner → Intermediate

Objective: Make model behavior more reliable, measurable and consistent.

### Main topics and subtopics

1\. Prompt engineering fundamentals

- System, developer and user instructions
- Role, objective, context, constraints and output format
- Zero-shot, few-shot and example-based prompting
- Task decomposition and explicit reasoning requirements
- Positive instructions, negative constraints and fallback behavior

2\. Context engineering

- Selecting relevant context rather than supplying everything
- Context ordering, summarization and compression
- Conversation history management
- Dynamic context construction
- Separating trusted instructions from untrusted user and retrieved content
- Managing context-window limits

3\. Structured generation

- JSON outputs and schema-constrained generation
- Pydantic models and field validation
- Enumerations, required fields and type constraints
- Handling malformed, incomplete or semantically invalid output
- Extraction and normalization pipelines

4\. Advanced prompting

- Prompt templates and reusable components
- Prompt versioning and change management
- Model-specific prompt adaptation
- Prompt injection and instruction-conflict testing
- Prompt optimization through controlled experiments
- Comparing prompts against a fixed evaluation dataset

Technologies: Provider SDKs, Pydantic, Jinja2 where appropriate, pytest, Git.

Practical project: Build a technical document analyzer that extracts technologies, prerequisites, commands, risks and troubleshooting steps into validated JSON.

Mastery gate: Demonstrate that a revised prompt improves measured task performance on a representative test set, rather than merely producing a better-looking example.

## Phase 3 — AI application engineering and model integration

Beginner → Intermediate

Objective: Turn individual model calls into maintainable backend services.

### Main topics and subtopics

1\. Backend integration

- FastAPI endpoints and request validation
- Service layers and separation of concerns
- Dependency injection and configuration management
- Async I/O and concurrent requests
- Streaming responses and cancellation
- API documentation and error responses

2\. Provider abstraction

- Provider-specific API differences
- Common internal request and response interfaces
- Model configuration and selection
- Provider fallbacks and retry policies
- Hosted versus local model adapters
- Avoiding premature abstraction and unnecessary frameworks

3\. Reliability patterns

- Connect and read timeouts
- Exponential backoff and jitter
- Rate-limit handling
- Retry budgets and idempotency
- Circuit breakers where justified
- Partial failures, cancellation and graceful degradation

4\. Data and state

- SQL fundamentals and PostgreSQL
- Database schemas and migrations
- SQLAlchemy and Alembic
- Persisting tasks, results and model metadata
- File uploads and storage boundaries
- Background jobs and task status tracking

5\. Testing

- Unit tests for deterministic code
- Mocked provider responses
- API integration tests
- Schema and error-path tests
- Contract tests for provider adapters
- Regression testing against known examples

Technologies: FastAPI, Pydantic, PostgreSQL, SQLAlchemy, Alembic, pytest, `httpx`.

Practical project: Convert the Phase 2 utility into a REST API with persistent history, input validation, configurable models and automated tests.

Mastery gate: A model provider outage, malformed output or rate limit must not crash the entire application or corrupt stored results.

## Phase 4 — Retrieval-augmented generation (RAG)

Intermediate

Objective: Build AI applications that answer questions using private, changing or domain-specific information.

### Main topics and subtopics

1\. Document ingestion

- PDF, Markdown, HTML, DOCX and plain-text parsing
- OCR for scanned documents
- Preserving headings, tables, code blocks and document structure
- Metadata extraction and document identifiers
- Deduplication, versioning and content hashing
- Document updates, deletion and reindexing

2\. Chunking and embeddings

- Fixed-size and overlapping chunks
- Structure-aware and semantic chunking
- Parent-child retrieval patterns
- Embedding models and vector representations
- Vector distance and similarity
- Embedding model compatibility and reindexing

3\. Retrieval systems

- Vector databases and similarity search
- Metadata filtering
- Keyword and hybrid search
- Query rewriting and expansion
- Reranking
- Top-k selection and retrieval thresholds
- Context assembly and token budgeting

4\. Grounded generation

- Citation and source attribution
- Answers based on retrieved evidence
- Abstaining when evidence is insufficient
- Contradictory or stale source handling
- Separating retrieved data from trusted instructions
- Permission-aware retrieval

5\. RAG evaluation

- Retrieval precision and recall
- Context relevance
- Answer correctness and faithfulness
- Citation correctness
- Failure analysis across ingestion, retrieval and generation
- Regression tests for document updates

Technologies: PostgreSQL with pgvector, Chroma or Qdrant, PyMuPDF, Beautiful Soup, embedding APIs or compatible local embedding models. Use LangChain or LlamaIndex only when their abstractions materially help.

Practical project: Build a technical knowledge assistant that indexes documentation, answers questions with citations and respects document permissions.

Mastery gate: Diagnose whether an incorrect answer originates in parsing, chunking, retrieval, context construction or generation—and fix the actual failure.

## Phase 5 — AI workflow automation and integrations

Intermediate

Objective: Connect AI capabilities to repeatable business processes without making every step dependent on an LLM.

### Main topics and subtopics

1\. Workflow fundamentals

- Triggers, actions, conditions and branching
- Scheduled, event-driven and manual workflows
- Webhooks and REST API integrations
- Data mapping and transformation
- Sequential and parallel execution
- Workflow state and execution history

2\. AI-assisted workflow design

- LLM classification and extraction steps
- Deterministic validation before downstream actions
- Model routing and fallback logic
- Confidence thresholds and exception queues
- Human approval and review steps
- Separating business rules from AI decisions

3\. Reliability

- Idempotent execution
- Retries and dead-letter handling
- Duplicate event detection
- Rate limits and concurrency control
- Timeouts, checkpoints and resumable workflows
- Audit trails and failure notifications

4\. Integration engineering

- OAuth and API credentials
- Webhook verification
- Third-party API pagination
- Data synchronization
- Least-privilege access
- Vendor limits and API changes

5\. Workflow operations

- Execution logs and error dashboards
- Versioning and deployment
- Test environments
- Manual replay and recovery
- Workflow ownership and documentation
- Cost and execution monitoring

Technologies: n8n as the primary workflow tool, plus FastAPI, webhooks, PostgreSQL and background-job infrastructure when needed. Make and Zapier are alternatives, not mandatory additional tools.

Practical project: Build an AI-assisted technical content pipeline: collect a topic, retrieve references, generate a draft, run quality checks, request approval and publish only after confirmation.

Mastery gate: A duplicate trigger must not create duplicate side effects, and a failed step must be diagnosable and recoverable without silently losing work.

## Phase 6 — AI agents and tool calling

Intermediate → Advanced

Objective: Build controlled AI systems that can choose tools and perform multi-step tasks within explicit limits.

### Main topics and subtopics

1\. Tool-calling fundamentals

- Function definitions and JSON schemas
- Model-generated tool arguments
- Input validation and output normalization
- Tool execution and result feedback
- Multiple tool selection
- Errors, retries and unsupported tool requests

2\. Agent architecture

- Model, tools, state and control loop
- Planning and execution
- Single-agent versus multi-agent designs
- Stateful workflows
- Checkpoints and resumable execution
- Termination conditions and maximum-step limits

3\. Agent orchestration

- Sequential and conditional workflows
- Parallel task execution
- Delegation and result aggregation
- Shared-state risks
- Framework-based orchestration
- Avoiding unnecessary multi-agent complexity

4\. Safety and control

- Tool allowlists and permission boundaries
- Read-only versus write-capable tools
- Human approval for consequential actions
- Sandboxing and resource limits
- Prompt injection through tool results
- Preventing arbitrary command execution and unauthorized data access

5\. Agent reliability

- Tracing each tool call
- Tool-output validation
- Detecting loops and repeated failures
- Budget limits for tokens, time and tool calls
- Partial results and safe stopping
- Testing agent trajectories, not just final answers

Technologies: Native provider tool calling, Pydantic, LangGraph where stateful orchestration is justified, and CrewAI or AutoGen for evaluating alternative multi-agent approaches.

Practical project: Build a bounded technical research agent that searches approved sources, consults your RAG knowledge base, produces cited findings and asks for approval before any external write action.

Mastery gate: The agent cannot bypass tool permissions, exceed configured budgets indefinitely or claim that an action succeeded when it failed.

## Phase 7 — Fine-tuning and customized AI assistants

Intermediate → Advanced

Objective: Customize existing models when prompting and retrieval alone cannot meet a demonstrated requirement.

### Main topics and subtopics

1\. Customization strategy

- Prompting versus RAG versus fine-tuning
- Hosted customization versus open-weight model adaptation
- Distinguishing knowledge problems from behavior problems
- Defining a measurable baseline
- Model capability and provider constraints

2\. Dataset engineering

- Curating task-specific examples
- Data cleaning and normalization
- Labeling guidelines and consistency
- Train, validation and held-out test splits
- Data leakage and duplicate detection
- Privacy, consent and licensing

3\. Fine-tuning fundamentals

- Supervised fine-tuning
- Training objectives and task-specific formats
- Parameters, epochs and overfitting
- Evaluation before and after customization
- Hosted fine-tuning APIs
- Hugging Face tooling and parameter-efficient methods such as LoRA/QLoRA, where hardware and model licensing permit

4\. Custom assistants

- Custom GPT configuration and instructions
- Knowledge sources and approved actions
- Tool configuration and permission design
- Versioning and reproducibility
- Evaluating custom assistants against a baseline
- Portability and vendor lock-in

5\. Deployment and governance

- Model registry and version tracking
- Rollback to previous models
- Dataset provenance
- Cost-benefit analysis
- Drift and regression monitoring
- Responsible use of domain-specific data

Technologies: OpenAI GPT Builder and supported fine-tuning APIs where available, Hugging Face, provider-specific customization services and evaluation tooling.

Practical project: Customize an assistant for a stable technical extraction task. Compare the base model, prompt-engineered model and customized model on the same held-out dataset.

Mastery gate: Fine-tuning must produce a measurable improvement that justifies its data preparation, maintenance and operational cost. Do not fine-tune merely to teach a model changing facts that belong in RAG.

## Phase 8 — Multimodal AI engineering

Advanced

Objective: Process text, images, documents, audio and video in a coherent application.

### Main topics and subtopics

1\. Vision and document understanding

- Image inputs and model-supported formats
- OCR versus vision-language models
- Screenshot and diagram interpretation
- Tables, charts and visual layouts
- Image resizing and resolution limits
- Confidence, ambiguity and visual grounding

2\. Audio

- Speech-to-text and transcription
- Text-to-speech
- Speaker and timestamp handling where supported
- Audio classification and summarization
- Streaming audio pipelines
- Consent and sensitive-data handling

3\. Video

- Frame extraction and sampling
- Timestamp-aware summaries
- Combining transcripts with visual evidence
- Scene segmentation and temporal context
- Processing large files efficiently
- Separating model limitations from media-processing errors

4\. Multimodal system design

- File validation and secure processing
- Asynchronous jobs for long-running tasks
- Object storage and metadata
- Model selection by modality
- Structured outputs and evidence references
- Cost, latency and file-size limits

5\. Evaluation

- Image and OCR accuracy
- Transcription quality
- Temporal and contextual correctness
- Unsupported visual claims
- Uncertainty handling
- Representative test collections

Technologies: Supported multimodal APIs from providers such as OpenAI and Google Gemini, compatible open-weight models, PyMuPDF, FFmpeg and Python media-processing libraries.

Practical project: Build a visual troubleshooting assistant that accepts screenshots, logs and optional audio explanations, then produces evidence-based diagnostic steps.

Mastery gate: The application must distinguish observed evidence from inference, handle unsupported formats gracefully and avoid presenting uncertain visual interpretations as facts.

## Phase 9 — AI-assisted content and media production

Advanced specialization

Objective: Integrate generative media into a product or repeatable publishing workflow when there is a clear use case.

### Main topics and subtopics

1\. AI video generation

- Text-to-video and image-to-video workflows
- Storyboards, shot planning and scene continuity
- Prompt iteration and reference images
- Clip length, resolution and generation limits
- Consistency across multiple shots
- Model and provider capability comparison

2\. Editing and post-production

- Voice-over generation
- Captions and subtitles
- Audio cleanup
- Timeline editing and clip assembly
- FFmpeg-based processing and automation
- Export formats and quality control

3\. Technical content quality

- Fact-checking generated explanations
- Verifying commands and demonstrations
- Consistent terminology and visual identity
- Source attribution and licensing
- Disclosure and synthetic-media policies where applicable
- Human editorial review

4\. Production workflow

- Topic brief and script generation
- Asset creation and storage
- Review checkpoints
- Versioned source assets
- Reusable templates
- Cost per finished output and failure rates

Technologies: Runway, Pika and similar video-generation services, OpusClip for suitable repurposing workflows, FFmpeg and conventional video-editing tools. Capabilities, pricing and availability vary by provider.

Practical project: Create a repeatable pipeline for producing accurate technical tutorials from a brief through script, visual assets, captions, human review and final export.

Mastery gate: Produce repeatable, fact-checked content within a defined quality standard and budget. Treat this as an optional specialization unless media generation is central to your product.

## Phase 10 — LLM evaluation, observability and model management

Advanced · Essential for production

Objective: Measure AI quality systematically, diagnose failures and prevent regressions as prompts, models, retrieval and workflows change.

### Main topics and subtopics

1\. Evaluation fundamentals

- Building representative evaluation datasets
- Golden examples and expected outputs
- Deterministic assertions versus model-based judging
- Exact-match, classification and extraction metrics
- Human review and expert evaluation
- Test-set coverage, sampling bias and data leakage

2\. LLM-specific evaluation

- Factual correctness and relevance
- Instruction adherence
- Structured-output validity
- Hallucination and unsupported-claim rates
- RAG retrieval quality, groundedness and citation correctness
- Tool-selection accuracy and agent task completion
- Safety, refusal and prompt-injection resistance

3\. Tracing and observability

- Request, model-call and workflow traces
- Latency and token usage
- Provider errors and retry rates
- Retrieval results and tool-call history
- Cost by user, tenant, task and feature
- Sensitive-data redaction and retention controls

4\. Model and prompt lifecycle

- Versioned prompts, models and evaluation datasets
- Regression testing before release
- Shadow testing and controlled rollouts where appropriate
- Model comparison and routing decisions
- Quality, latency and cost trade-offs
- Rollback and incident investigation

5\. Production quality gates

- Minimum quality thresholds
- Release-blocking tests
- Monitoring for quality degradation
- Feedback collection and failure categorization
- Regression reproduction
- Documented remediation and re-evaluation

Technologies: pytest, promptfoo, Ragas for relevant RAG evaluations, Langfuse, Helicone, PromptLayer, TruLens and OpenTelemetry. Select a small compatible set rather than installing every tool.

Practical project: Add an evaluation and observability layer to the existing knowledge assistant and agent. Record traces, test a fixed dataset and compare two model or prompt versions.

Mastery gate: Identify a real failure from traces, reproduce it with a test, correct it, demonstrate the improvement and ensure that the fix does not regress other tasks.

Important: Begin basic evaluation in Phase 2 and continue throughout every phase. Phase 10 formalizes the evaluation and operations system.

## Phase 11 — Production SaaS architecture, security and reliability

Advanced → Production

Objective: Convert the AI application into a secure, maintainable, multi-user service that can operate reliably outside your development machine.

### Main topics and subtopics

1\. SaaS application architecture

- Frontend, API, application service and data layers
- Modular monolith versus microservices
- Tenant isolation and user ownership
- Authentication, authorization and session management
- API versioning and backward compatibility
- Background workers and asynchronous task processing

2\. Security engineering

- Secret management and credential rotation
- Least-privilege permissions
- Input validation and upload restrictions
- Prompt injection and indirect prompt injection
- Data exfiltration through tools and retrieved documents
- SSRF, insecure file processing and unsafe deserialization
- Rate limiting, abuse prevention and quotas
- Audit logs, privacy, retention and deletion

3\. Data integrity

- Database transactions and constraints
- Migration discipline
- Idempotent write operations
- File and object-storage lifecycle
- Backup and restore testing
- Consistent deletion across source documents, indexes and caches
- Recoverable workflows and durable task state

4\. Cost and performance

- Per-user and per-feature budgets
- Token, embedding and media-generation costs
- Caching with correct invalidation
- Batching and bounded concurrency
- Model routing by task and quality requirement
- Queue management and backpressure
- Performance testing and capacity estimates

5\. Deployment and operations

- Docker and container configuration
- Environment separation
- CI/CD using GitHub Actions
- Automated tests, linting and dependency checks
- TLS, domain configuration and secure networking
- Health checks, metrics and structured logs
- Deployment rollback and incident response
- Recovery objectives and operational documentation

6\. SaaS product fundamentals

- User onboarding and access control
- Usage metering
- Free versus paid limits
- Subscription and billing integration when required
- Entitlement checks and billing-webhook idempotency
- Support, feedback and account deletion
- Service-level expectations and operational cost tracking

Technologies: FastAPI, PostgreSQL, Docker, GitHub Actions, pytest, Ruff, Semgrep, Trivy, an appropriate authentication solution, and an observability stack.

Practical project: Deploy the integrated AI application with authentication, tenant isolation, usage limits, secure secrets, monitoring, backups and documented recovery procedures.

Mastery gate: Demonstrate that one tenant cannot access another tenant's data, credentials are not exposed, failures are observable, and the service can be restored from a tested backup.

## Phase 12 — AI product integration, architecture and engineering mastery

Mastery

Objective: Demonstrate that you can design, build, evaluate, ship and maintain a complete AI product—not merely assemble model APIs.

### Main topics and subtopics

1\. End-to-end system design

- Translating user problems into product requirements
- Defining functional and non-functional requirements
- Choosing between direct LLM calls, RAG, workflows and agents
- Data-flow diagrams and trust boundaries
- API and database design
- Failure-mode analysis and architectural trade-offs

2\. AI gateway and provider strategy

- Unified model interfaces
- Provider capability differences
- Model selection and routing
- Controlled fallback on provider errors or usage limits
- Timeout, retry and duplicate-request handling
- Usage tracking and budget enforcement
- Secure local-model integration
- Avoiding a single point of failure in the gateway

3\. Integration standards and portability

- REST APIs and webhooks
- Model Context Protocol (MCP) concepts and implementation
- MCP clients and servers
- Tool discovery and explicit permissions
- Authentication and trust boundaries
- Compatibility testing and protocol versioning
- Choosing MCP only when interoperable tool access provides value

4\. Product and business validation

- Customer discovery and problem validation
- Competitive differentiation
- Usability and onboarding
- Time-to-value and task completion
- Cost per successful task
- Retention, adoption and support metrics
- Pricing and unit economics
- Prioritizing features from actual user feedback

5\. Release engineering

- Architecture decision records
- Versioned configurations and migrations
- Threat modeling and security review
- Evaluation and regression gates
- Release notes and rollback plans
- User documentation and support procedures
- Post-release monitoring and incident learning

6\. Engineering independence

- Reading model and framework documentation critically
- Debugging provider, retrieval and agent failures
- Reviewing AI-generated code
- Replacing dependencies when needed
- Explaining design decisions and trade-offs
- Maintaining a reproducible development environment
- Planning upgrades without breaking existing users

Technologies: Reuse the stack established in earlier phases. Add MCP, a model gateway, billing, caching or other infrastructure only when justified by concrete product requirements.

Practical project: Release one complete AI SaaS product with a documented architecture, automated tests, an evaluation suite, security controls, deployment instructions, monitoring and a recovery plan.

Mastery gate: Another developer can deploy the project from its documentation, reproduce its tests, understand its limitations, diagnose a failure and safely release an update.

## 5. The single evolving capstone product

Instead of building 12 unrelated projects, evolve one application through the roadmap. A suitable capstone is a Technical Knowledge and Workflow SaaS.

[Wiki — Knowledge Base — Monolynx](https://images.openai.com/static-rsc-4/niJa5Jgb5LdCn-9rBlUFSnbhfZq8pHNbBJNB3d5TFRBy5_s0H-HStTN1sJp-HetIFrBLXwabcYoK85Z9SM8eWdp_9YUMUyWwipL3kTdJ01OzZPRHAkHigCcTxaFYJqO9A29dpwCfMDd4_oBYqf0Z0METmL--xXwGVPO1k3E9y7I?purpose=inline)

Stage A — AI utility

Phases 1–3

Summarize documents, extract structured data and expose capabilities through a tested API.

[AI Internal Knowledge Search by Mohammed TAYOR on Dribbble](https://images.openai.com/static-rsc-4/UQmigjAZukVk01CB-45P5nBMldyJGulBRvGELdEpQ4ygClyyuEInDWrcU3YDosOZdGDFRk9fKZ3izMZz0jNwoBFhxz0grSPkb3JOAzENtbDiqTG06dhKXcue7_UtYPsJ50zPo3G9H9jE2xK3VHMYCu-1rdDU-pv8K6awdFTO_-0?purpose=inline)

Stage B — Knowledge assistant

Phase 4

Ingest documentation, search relevant passages, cite sources and manage document versions.

[Module 1 Lesson 4: The n8n UI & Node Anatomy | ShShell.com](https://images.openai.com/static-rsc-4/7m7q53lHPO1Pl8hWGZWzZ-S-TE8NIg1gPOAvyTKVBBep0crxaB0mem5lhMsqcdHKcRGSLdOPwY9PYMK6gF1oj3HAii3nczSnKCBzL0Inom0OEy1Ka5WZ8_zWKuFNOMbid8etYiPVTajXw9p3DfHrUY--JBOCt1mB6MfhI6_Fi0Y?purpose=inline)

Stage C — Workflow and agent layer

Phases 5–6

Automate tasks, call approved tools, track execution and request approval for consequential actions.

[Tracekit - Find What Broke in Production](https://images.openai.com/static-rsc-4/2MfTO4bPwRdkxWTw49-ueU9My2o8iwZnFqq6UuYrBt7B0_FVlj7qtoc-UABGp9dDos9mj-ctk1rKvUD7ZiC-A7Jlx9c0XuDBnM_6xiY1u8nu9v1k9oWDJb1_ZSsJYC13mgjABvWsAnt5dHxcEwIU-noyLwP_OKozIGN4daPzxes?purpose=inline)

Stage D — Advanced AI capabilities

Phases 7–10

Add justified customization or multimodal features, then integrate systematic evaluation and tracing.

[Overview](https://images.openai.com/static-rsc-4/odO-tO8mlT4KZoVR3PvE4W0wX9OTcHCdC6T4juY-9_CpqM_A8JrFRkP7U5bTZaTeA2Lk2KAgOlBDwf_9zEfAIHkQlZ1RT1tM4dmFZL2Ru6kow4lp0gapPAbrEewGv4af7ZyJCjNxRHkofjPFcgHAFyXy6zqY7d-8bJWtNKVn8io?purpose=inline)

Stage E — Production SaaS

Phases 11–12

Add authentication, tenant isolation, usage controls, deployment, documentation and operational recovery.

The product's exact domain can change. The important part is that each stage reuses and strengthens the same codebase, test suite and architecture.

## 6. Recommended technology stack

Start with a small, maintainable stack. Do not learn several competing frameworks simultaneously.

| Layer            | Recommended starting point                            | Add later when needed                                |
| ---------------- | ----------------------------------------------------- | ---------------------------------------------------- |
| Language         | Python                                                | TypeScript for frontend or specific integrations     |
| API              | FastAPI + Pydantic                                    | Separate services only when justified                |
| Model access     | One hosted LLM API + Ollama for local experimentation | Provider gateway and fallback routing                |
| Data             | PostgreSQL + SQLAlchemy + Alembic                     | Redis for appropriate caching or queues              |
| RAG              | PostgreSQL + pgvector                                 | Qdrant or a dedicated retrieval service              |
| AI workflows     | n8n                                                   | Custom workers for complex application logic         |
| Agents           | Native tool calling                                   | LangGraph for stateful orchestration                 |
| Interoperability | REST APIs and webhooks                                | MCP when standardized tool integration helps         |
| Evaluation       | pytest + versioned test dataset                       | promptfoo, Ragas or additional evaluation tooling    |
| Observability    | Structured logs and traces                            | Langfuse or another compatible platform              |
| Frontend         | HTML, CSS, JavaScript or your existing frontend       | A framework only when product complexity warrants it |
| Deployment       | Docker + GitHub Actions                               | Managed cloud services as demand grows               |
| Security         | Authentication, least privilege, secret management    | Additional security scanning and policy enforcement  |

This stack is compatible with a practical, Python-centered learning path and supports both hosted models and local inference.&#x20;

## 7. Suggested part-time study schedule

Use the following as a planning estimate, not a deadline. Spend roughly 1–2 hours on a normal study day, adjusting the pace to your workload.

| Period     | Phases         | Primary outcome                                            |
| ---------- | -------------- | ---------------------------------------------------------- |
| Month 1    | 1–3            | Tested LLM API application                                 |
| Month 2    | 4              | RAG knowledge assistant                                    |
| Month 3    | 5–6            | Reliable workflows and bounded agent                       |
| Month 4    | 7–8            | Model customization and multimodal prototype               |
| Month 5    | 9–10           | Content workflow and AI evaluation system                  |
| Month 6    | 11             | Secured and deployed SaaS foundation                       |
| Months 7–9 | 12 + hardening | Complete product, user testing and production improvements |

Phase 9 is a specialization and can be postponed. If your available time is limited, prioritize RAG, controlled tool calling, evaluation, security and deployment over video generation or complex multi-agent systems.

A useful weekly allocation is:

- 20% — Learn: concepts, documentation and architecture.
- 60% — Build: implement the current phase in the capstone.
- 20% — Verify: tests, debugging, evaluation and documentation.

## 8. Definition of production-ready

Before calling the final project production-ready, verify these areas.

## Production-readiness checklist

Core functionality
- [ ] Defined requirements and API contracts
- [ ] Validated inputs and structured outputs
- [ ] Documented failure and fallback behavior

AI quality
- [ ] Versioned evaluation dataset
- [ ] Measured quality and regression tests
- [ ] Grounded answers and citations where required

Security and data
- [ ] Authentication and tenant isolation
- [ ] Secret management and permission boundaries
- [ ] Data deletion, backups and restore testing

Operations
- [ ] Deployment and migration procedure
- [ ] Logs, traces, latency and cost monitoring
- [ ] Usage limits, recovery and rollback plan

Product readiness
- [ ] Clear user workflow and documentation
- [ ] Realistic pilot testing and feedback
- [ ] Known limitations and support procedure

A checked item means you have verified it, not simply implemented it. For example, a backup is not verified until you have successfully restored from it.

## Final recommendation

Treat this as a single engineering curriculum with 12 progressive phases, not a checklist of tools to collect.

Your central objective is to become capable of taking an AI product from a real user problem through architecture, implementation, evaluation, security, deployment and ongoing maintenance. The strongest evidence of mastery will be one complete product with reproducible tests, measured AI quality, documented trade-offs and a reliable operating process.
