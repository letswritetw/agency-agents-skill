---
name: agency-agents
description: Automatically select and delegate development, UI/UX, architecture, code review, DevOps, data, documentation, AI, and related tasks to the most appropriate installed Agency Agent subagent. Use when specialist expertise would materially improve the result. Prefer the minimum number of agents necessary and handle trivial tasks directly.
---

# Agency Agents Router for Claude Code

Automatically determine whether the user's request should be handled directly or delegated to one or more installed Agency Agents.

Agency Agents are installed as Claude Code subagents under:

`~/.claude/agents/`

Use Claude Code's native subagent delegation mechanism to invoke them.

The user should not need to manually specify an agent unless they want a particular specialist.

# Primary objective

For every task:

1. Understand the user's actual goal.
2. Determine whether specialist expertise would materially improve the result.
3. If not, handle the task directly.
4. If yes, select the best installed Agency Agent.
5. Use the minimum number of agents necessary.
6. For multi-discipline tasks, delegate sequentially when one specialist's output is needed by another.
7. Preserve the user's original requirements and constraints through every handoff.

# Critical rules

- Never delegate merely because an agent exists.
- Never invoke multiple agents when one specialist is sufficient.
- Never invent an Agency Agent that is not installed.
- Never claim that an agent was used unless it was actually invoked.
- Do not ask the user which agent to use when the task can be routed automatically.
- Honor an explicitly requested agent whenever possible.
- Do not let delegation expand the requested scope.
- Do not perform unnecessary refactoring.
- Prefer direct execution for trivial or mechanical work.
- For substantial implementation, review may be useful, but it is not mandatory for every change.

# Do not delegate

Normally handle these directly:

- fixing a typo
- changing text
- changing one obvious CSS value
- renaming a variable
- changing a simple configuration value
- explaining a straightforward function
- answering a basic technical question
- running a known command
- making a tiny mechanical edit
- performing an obvious single-file change with no meaningful design decision

Do not spend more effort routing than solving the task.

# Agent routing

## Frontend Developer

Use when the task primarily involves:

- Vue
- React
- Angular
- Svelte
- JavaScript
- TypeScript
- HTML
- CSS
- frontend components
- frontend state management
- forms
- browser APIs
- responsive implementation
- accessibility implementation
- Core Web Vitals
- frontend performance
- browser compatibility
- implementation of an existing UI design

If the design is already defined, normally use Frontend Developer directly.

---

## UI Designer

Use when the task involves meaningful visual design decisions:

- redesigning an interface
- dashboard design
- page layout
- visual hierarchy
- typography
- spacing systems
- color systems
- component appearance
- design systems
- visual consistency
- converting requirements into UI concepts

If implementation is also required:

UI Designer
→ Frontend Developer

Do not invoke UI Designer merely because frontend code is involved.

---

## UX Researcher

Use when the problem primarily involves:

- usability
- user flows
- information architecture
- navigation
- interaction problems
- user behavior
- UX evaluation
- identifying friction
- evaluating whether a feature is intuitive

Typical sequence:

UX Researcher
→ UI Designer

Add Frontend Developer only when implementation is requested.

---

## Software Architect

Use when the task involves:

- system architecture
- application architecture
- module boundaries
- architectural patterns
- major refactoring
- domain modeling
- system decomposition
- long-term maintainability
- architectural tradeoffs
- deciding how multiple subsystems should interact

If implementation follows:

Software Architect
→ appropriate implementation agent

Do not use Software Architect for routine feature implementation.

---

## Backend Architect

Use for:

- APIs
- backend services
- server-side architecture
- authentication backends
- authorization backends
- service boundaries
- backend business logic
- microservices
- backend scalability

Use Software Architect instead when the question concerns the entire system rather than primarily backend design.

---

## Code Reviewer

Use for:

- code review
- PR review
- diff review
- correctness review
- maintainability
- regressions
- implementation risks
- code quality
- identifying bugs in completed work

When the user explicitly requests a code review, prefer Code Reviewer.

For substantial implementation, Code Reviewer may be used after implementation.

Do not automatically invoke Code Reviewer after trivial changes.

---

## Minimal Change Engineer

Prefer for:

- narrowly scoped bug fixes
- production hotfixes
- fixing one known defect
- minimal-risk modifications
- avoiding scope creep
- preserving existing behavior
- requests such as "only fix this problem"
- requests where unrelated refactoring must be avoided

Typical flow:

Minimal Change Engineer

Do not add additional agents unless clearly necessary.

---

## DevOps Automator

Use for:

- Docker
- Docker Compose
- CI/CD
- Jenkins
- GitHub Actions
- deployment
- release automation
- infrastructure automation
- build pipelines
- container configuration

---

## SRE

Use for:

- production reliability
- observability
- monitoring
- SLOs
- SLAs
- error budgets
- capacity planning
- operational resilience
- incident prevention

Use DevOps Automator for deployment automation.
Use SRE for ongoing production reliability.

---

## Incident Response Commander

Use when there is an active or simulated production incident requiring:

- incident coordination
- containment
- mitigation
- incident communication
- restoration
- post-incident structure

Do not use for ordinary debugging.

---

## Git Workflow Master

Use for:

- complex Git workflows
- branching strategy
- merge strategy
- rebase strategy
- repository migration
- history cleanup
- release branching
- advanced Git problems

Do not invoke for ordinary:

- git add
- git commit
- git pull
- git push

unless a larger workflow issue exists.

---

## Database Optimizer

Use for:

- SQL performance
- indexing
- query optimization
- schema performance
- slow queries
- PostgreSQL
- MySQL
- migration performance
- database tuning

---

## Database Reliability Engineer

Use when the database problem is primarily operational:

- high availability
- replication
- failover
- backup
- recovery
- PITR
- zero-downtime database operations

---

## AI Engineer

Use for:

- AI application features
- LLM integration
- model integration
- inference workflows
- AI application architecture
- embeddings
- AI pipelines

---

## RAG Pipeline Engineer

Prefer over general AI Engineer for:

- RAG
- document retrieval
- chunking
- embeddings retrieval
- hybrid search
- reranking
- vector search
- retrieval evaluation
- retrieval quality

---

## Prompt Engineer

Use for:

- system prompts
- developer prompts
- AI instructions
- prompt optimization
- structured prompting
- agent prompts
- reducing prompt ambiguity
- improving instruction reliability

---

## Multi-Agent Systems Architect

Use for:

- multi-agent architecture
- agent orchestration
- agent routing
- agent handoffs
- multi-agent context strategy
- trust boundaries between agents
- agent failure recovery
- multi-agent workflows

Use this when designing the agent system itself rather than merely routing a normal development task.

---

## Data Engineer

Use for:

- ETL
- ELT
- data pipelines
- ingestion
- transformation
- warehouses
- data lakes
- data infrastructure

---

## Data Visualization Engineer

Use for:

- charts
- dashboards where data visualization itself is central
- visualization selection
- D3
- Vega
- perceptual accuracy
- visualization performance

Do not use merely because a dashboard contains a simple chart.

---

## Technical Writer

Use for:

- README
- technical documentation
- API documentation
- installation guides
- migration guides
- architecture documentation
- developer documentation

Do not delegate tiny wording corrections.

---

## Identity & Access Engineer

Use for:

- OAuth
- OIDC
- SAML
- SSO
- RBAC
- ABAC
- authentication
- authorization
- tokens
- sessions
- IAM

Prefer this over general Backend Architect when identity and access control are the primary concern.

---

## Privacy Engineer

Use for:

- PII
- data minimization
- privacy controls
- retention
- consent
- deletion workflows
- DSAR
- right-to-be-forgotten implementation

# Routing patterns

## Existing design → implementation

Use:

Frontend Developer

Not:

UI Designer
→ Frontend Developer

unless visual decisions are still unresolved.

---

## UI redesign + implementation

Use:

UI Designer
→ Frontend Developer

For substantial changes, optionally:

→ Code Reviewer

---

## UX problem + redesign

Use:

UX Researcher
→ UI Designer

If implementation is requested:

→ Frontend Developer

---

## Normal frontend feature

Use:

Frontend Developer

Do not automatically create a multi-agent workflow.

---

## Architecture-heavy frontend feature

Use:

Software Architect
→ Frontend Developer

---

## Small bug fix

Prefer:

Minimal Change Engineer

Avoid:

Software Architect
→ Frontend Developer
→ Code Reviewer

unless the defect reveals a broader architectural problem.

---

## Significant refactor

Possible flow:

Software Architect
→ appropriate implementation agent
→ Code Reviewer

---

## Docker / CI/CD issue

Use:

DevOps Automator

If the root issue is production reliability rather than automation:

SRE

---

## Explicit PR review

Use:

Code Reviewer

Add a security specialist only when security is materially involved.

# Multi-agent delegation

When multiple agents are necessary:

1. Delegate each specialist a specific responsibility.
2. Do not ask multiple agents to solve the same problem independently unless comparison is explicitly useful.
3. Pass conclusions from an earlier specialist to the next specialist.
4. Do not make later agents repeat already completed discovery.
5. Keep the original user request as the source of truth.
6. Stop delegating once specialist expertise no longer adds meaningful value.

Prefer sequential delegation:

Specialist A
→ Specialist B
→ implementation

rather than unnecessary parallel fan-out.

# Agent availability

Before selecting an agent:

1. Check Claude Code's available subagents.
2. Match against actually installed Agency Agents.
3. Use exact installed agent names when delegating.

If the ideal specialist is unavailable:

1. Use the nearest suitable installed agent, or
2. handle the task directly.

Never stop the task solely because an Agency Agent is unavailable.

# Explicit user choice

If the user says:

"Use Frontend Developer"

or names another Agency Agent:

- prefer that agent
- do not silently replace it
- only choose differently when the requested agent is unavailable or clearly inappropriate
- explain the deviation only when materially relevant

# Output behavior

Do not burden the user with internal routing details unless they ask.

A short indication of meaningful specialist delegation is acceptable when useful.

Focus the final response on:

- what was found
- what was decided
- what changed
- remaining risks or next actions

not on the mechanics of agent routing.

# Final principle

Agency Agents exist to improve quality, not to add ceremony.

Always prefer:

the minimum useful specialization
→ the clearest responsibility
→ the smallest appropriate scope
→ completion of the user's actual request.
