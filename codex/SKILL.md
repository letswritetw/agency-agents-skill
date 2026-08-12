---
name: agency-agents
description: Automatically select and delegate software engineering, UI/UX, architecture, code review, DevOps, data, documentation, AI, and related tasks to the most appropriate installed Codex Agency Agent. Use when specialist expertise would materially improve the result. Prefer the minimum number of agents required and perform trivial tasks directly.
---

# Agency Agents Router for Codex

Automatically select the most appropriate installed Agency Agent for the user's task.

Agency Agents are installed as Codex custom agents under:

`~/.codex/agents/`

Each Agency Agent is represented by a TOML configuration containing its name, description, and developer instructions.

Use Codex's custom agent delegation capabilities when specialist expertise materially improves the result.

The user should normally be able to describe only the task. Agent selection should happen automatically.

# Core process

For every request:

1. Determine the user's desired outcome.
2. Determine the primary discipline involved.
3. Assess the task's complexity and risk.
4. Decide whether specialist delegation adds meaningful value.
5. If not, perform the task directly.
6. If yes, select the most appropriate installed Agency Agent.
7. Use additional agents only when the task genuinely crosses disciplines.
8. Preserve the user's requirements throughout all delegation.
9. Complete the original task rather than stopping after specialist analysis.

# Delegation threshold

Delegation is justified when specialist judgment improves:

- architecture
- design quality
- implementation quality
- code review
- production safety
- performance
- accessibility
- security
- reliability
- complex debugging
- maintainability

Delegation is usually not justified for trivial mechanical changes.

# Do not delegate

Handle directly when possible:

- typo corrections
- simple text replacement
- changing one obvious value
- simple CSS value changes
- variable renaming
- basic explanations
- simple shell commands
- tiny configuration edits
- mechanical formatting
- trivial one-file changes
- obvious fixes requiring no specialist judgment

Do not create agent overhead for simple work.

# General routing rules

## Frontend Developer

Primary specialist for:

- Vue
- React
- Angular
- Svelte
- JavaScript
- TypeScript
- HTML
- CSS
- frontend components
- frontend architecture
- state management
- forms
- frontend APIs
- responsive implementation
- accessibility implementation
- frontend performance
- Core Web Vitals
- browser compatibility

If visual requirements are already defined, prefer Frontend Developer alone.

---

## UI Designer

Use when meaningful interface design is required:

- UI redesign
- visual hierarchy
- layout
- spacing
- typography
- colors
- design systems
- component appearance
- dashboard design
- visual consistency
- translating requirements into interface design

If implementation is also requested:

UI Designer
→ Frontend Developer

---

## UX Researcher

Use when the core problem involves:

- usability
- user flows
- information architecture
- navigation
- interaction design
- user behavior
- friction analysis
- UX evaluation

Possible workflow:

UX Researcher
→ UI Designer
→ Frontend Developer

Only include each stage when necessary.

---

## Software Architect

Use for:

- application architecture
- system architecture
- architectural patterns
- system decomposition
- module boundaries
- major refactoring
- technical tradeoffs
- domain design
- long-term maintainability

For implementation:

Software Architect
→ appropriate implementation agent

Do not involve Software Architect in routine coding tasks.

---

## Backend Architect

Use for:

- backend APIs
- server-side systems
- service boundaries
- backend architecture
- backend business logic
- distributed services
- scalability
- authentication backends

Use Software Architect instead when the task spans the entire system.

---

## Code Reviewer

Primary specialist for:

- PR review
- code review
- diff review
- correctness
- maintainability
- implementation risks
- regression detection
- code quality
- completed feature review

When the user asks to review code, use Code Reviewer.

For substantial implementation:

implementation agent
→ Code Reviewer

when review materially adds value.

Do not review every trivial change.

---

## Minimal Change Engineer

Use for:

- targeted bug fixes
- hotfixes
- minimum viable diffs
- production fixes
- requests that explicitly prohibit unrelated changes
- preserving existing behavior
- high regression-risk legacy code
- narrowly scoped corrections

Default flow:

Minimal Change Engineer

Avoid extra specialists unless necessary.

---

## DevOps Automator

Use for:

- Docker
- Docker Compose
- CI/CD
- Jenkins
- GitHub Actions
- deployment automation
- container configuration
- build pipelines
- infrastructure automation
- release automation

---

## SRE

Use when the problem is centered on:

- reliability
- availability
- observability
- monitoring
- SLO
- SLA
- error budgets
- production resilience
- capacity planning

Distinguish:

deployment automation
→ DevOps Automator

production reliability
→ SRE

---

## Incident Response Commander

Use for active production incidents requiring:

- coordination
- incident triage
- mitigation
- recovery
- containment
- communication
- post-incident structure

Do not use for routine debugging.

---

## Git Workflow Master

Use for:

- branching strategies
- complex merges
- rebasing
- history cleanup
- repository migration
- release workflows
- advanced Git problems

Do not delegate basic Git commands unless a workflow problem exists.

---

## Database Optimizer

Use for:

- SQL
- database performance
- indexing
- slow queries
- schema optimization
- MySQL
- PostgreSQL
- query plans
- migration performance

---

## Database Reliability Engineer

Use for:

- replication
- failover
- HA
- backup
- restore
- PITR
- database operational reliability
- zero-downtime database operations

---

## AI Engineer

Use for:

- LLM integration
- AI application development
- AI features
- model integration
- inference
- embeddings
- AI pipelines
- ML-enabled application architecture

---

## RAG Pipeline Engineer

Use instead of generic AI Engineer when primarily working on:

- RAG
- vector retrieval
- document retrieval
- chunking
- hybrid search
- reranking
- retrieval evaluation
- retrieval quality

---

## Prompt Engineer

Use for:

- prompts
- system prompts
- developer instructions
- prompt optimization
- AI agent instructions
- structured prompts
- prompt reliability
- instruction design

---

## Multi-Agent Systems Architect

Use when designing:

- multi-agent architecture
- agent routers
- orchestration
- agent communication
- handoffs
- context boundaries
- failure recovery
- agent topology

Do not use merely because this Skill itself performs routing.

---

## Data Engineer

Use for:

- ETL
- ELT
- pipelines
- ingestion
- transformation
- warehouses
- lakes
- data infrastructure

---

## Data Visualization Engineer

Use when visualization itself requires specialist judgment:

- dashboard visualization
- chart choice
- D3
- Vega
- perceptual accuracy
- visualization performance
- misleading visualization prevention

---

## Technical Writer

Use for substantial:

- README documentation
- technical documentation
- API docs
- architecture docs
- installation guides
- migration guides
- developer guides

Do not use for minor wording changes.

---

## Identity & Access Engineer

Use for:

- authentication
- authorization
- OAuth
- OIDC
- SAML
- SSO
- RBAC
- ABAC
- IAM
- tokens
- sessions

---

## Privacy Engineer

Use for:

- PII
- consent
- data minimization
- privacy controls
- deletion pipelines
- data retention
- DSAR
- right-to-be-forgotten

# Selection priorities

When several agents match, select according to the actual requested outcome rather than keywords alone.

Example:

"Build this Figma design in Vue"

Primary task:

Frontend implementation

Use:

Frontend Developer

Do not automatically use UI Designer because the design already exists.

---

Example:

"Redesign this dashboard and implement it in Vue"

Use:

UI Designer
→ Frontend Developer

---

Example:

"Users can't understand this checkout flow"

Use:

UX Researcher

Potentially:

UX Researcher
→ UI Designer

Implementation only if requested.

---

Example:

"Fix this Vue bug without changing anything else"

Use:

Minimal Change Engineer

rather than Frontend Developer plus multiple reviewers.

---

Example:

"Design the architecture for a new authentication platform"

Use:

Software Architect
→ Identity & Access Engineer

Implementation agents only if implementation is requested.

---

Example:

"Our Docker deployment pipeline is broken"

Use:

DevOps Automator

---

Example:

"Production latency keeps increasing and we need monitoring and SLOs"

Use:

SRE

# Multi-agent workflows

Use multi-agent workflows only when specialties are dependent.

Preferred pattern:

Agent A analyzes a bounded concern.
↓
Agent B consumes Agent A's useful conclusions.
↓
Implementation is completed.
↓
Optional review.

Do not have multiple agents repeat the same codebase exploration unless genuinely necessary.

# Common workflows

## UI implementation

If design already exists:

Frontend Developer

If design must first be created:

UI Designer
→ Frontend Developer

---

## Complex frontend change

Frontend Developer

Optionally:

→ Code Reviewer

Only add Software Architect when architecture decisions are significant.

---

## UX redesign

UX Researcher
→ UI Designer

If implementation requested:

→ Frontend Developer

---

## Major refactoring

Software Architect
→ implementation specialist
→ Code Reviewer

---

## Small bug

Minimal Change Engineer

---

## Code review

Code Reviewer

---

## CI/CD

DevOps Automator

---

## Production reliability

SRE

---

## Authentication architecture

Identity & Access Engineer

Use Software Architect first only if broader system architecture is involved.

---

## RAG system

RAG Pipeline Engineer

Use AI Engineer as an additional specialist only when broader AI-system concerns exist.

# Codex custom agent selection

Before delegation:

1. Determine which custom agents are available to Codex.
2. Match the desired Agency Agent against installed agents in `~/.codex/agents/`.
3. Use the installed agent's canonical name.
4. Delegate through Codex's custom-agent mechanism.

Do not rely solely on expected filenames.

Agent names are authoritative.

If a preferred agent is unavailable:

1. Select the nearest suitable installed specialist if there is a clear substitute.
2. Otherwise handle the task directly.

Never fabricate an unavailable agent.

# Explicit agent requests

If the user explicitly asks for an agent, for example:

"Use the Frontend Developer agent"

then use that agent when available.

Do not replace explicit user intent merely because another agent appears slightly more suitable.

# Scope control

Agency Agent delegation must not create unnecessary work.

Agents should not:

- add unrelated features
- redesign unrelated UI
- refactor unrelated code
- introduce technologies the user did not request without justification
- change project conventions unnecessarily
- expand a small fix into a rewrite

The user's original request is always the primary scope.

# Review policy

Do not automatically use Code Reviewer for every implementation.

Consider review when:

- multiple files changed substantially
- architecture changed
- security-sensitive code changed
- authentication changed
- data handling changed
- complex business logic changed
- the user explicitly asks for review

Skip review for trivial modifications unless requested.

# Routing transparency

Do not turn every response into a routing report.

The user primarily cares about the result.

Mention delegation briefly only when it helps explain the workflow or when the user asks which agents were used.

# Final principle

The best routing decision is often:

no delegation.

When delegation adds meaningful value:

choose the smallest number of specialists capable of producing a better result.

Optimize for:

quality
→ correctness
→ scope control
→ efficient use of agents
→ completion of the user's request.
