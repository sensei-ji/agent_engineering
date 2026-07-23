<!-- BEGIN 00_README.md -->
# Agent Engineering with Gemini, ADK & Antigravity

## Book 1: Foundations
### Build an Inspectable AI Agent with the WidgetWare SDR Lab

This directory contains the manuscript blueprint for Book 1. Each major part of the book is maintained as a separate Markdown file so that chapters can be written, reviewed, taught, and released independently.

## Reading order

1. `01_Foreword.md`
2. `02_Introduction.md`
3. `03_Chapter_01_From_Language_Models_to_Agent_Engineering.md`
4. `04_Chapter_02_Building_with_Antigravity.md`
5. `05_Chapter_03_Gemini_Models_and_Context_Engineering.md`
6. `06_Chapter_04_Your_First_Agent_with_ADK.md`
7. `07_Chapter_05_Skills_and_Reusable_Agent_Capabilities.md`
8. `08_Chapter_06_Structured_Outputs_and_Agent_Contracts.md`
9. `09_Chapter_07_Tool_Engineering.md`
10. `10_Chapter_08_Evidence_Backed_Research_with_MCP.md`
11. `11_Chapter_09_Multi_Agent_Workflows_and_Human_Approval.md`
12. `12_Chapter_10_Evaluate_Deploy_and_Demonstrate.md`
13. `13_Chapter_11_Loop_Engineering_with_ADK.md`
14. `14_Book_1_Conclusion.md`
15. `15_Introduction_to_Book_2.md`

## The continuous lab

Every chapter advances the same reference implementation: **WidgetWare SDR Lab**. WidgetWare is a fictional software company. Its Sales Development Representative workflow is a useful agent-engineering case study because it combines:

- business context;
- research and evidence;
- structured qualification;
- tool use;
- multi-agent collaboration;
- human judgment;
- external-action risk; and
- measurable evaluation criteria.

The Book 1 system remains deliberately bounded. It researches and qualifies accounts, drafts outreach, and requests human approval. It does not autonomously send external messages.

## The Seven Steps to Agent Engineering

This is the same methodology used across every edition of this book, regardless of which vendor's model, framework, or IDE implements it. The technology changes; the discipline does not.

1. **Frame the Use Case** — define the goal, the users, the boundaries, and the autonomy level before any code exists.
2. **Build Context** — assemble the instructions, business rules, and evidence Gemini reasons over.
3. **Design Agent Capabilities** — choose or build the Skills, contracts, and tools the agent needs.
4. **Build the Harness** — establish the operating environment (Antigravity, ADK's runtime, sessions, permissions) the agent runs inside.
5. **Orchestrate Workflows** — sequence steps, coordinate agents, and gate progress on human approval.
6. **Engineer Loops** — wrap a working, evaluated workflow in a bounded process that discovers work, persists state, and decides whether to continue, retry, stop, defer, or escalate.
7. **Evaluate & Govern** — measure whether the system is actually good, and keep it within its boundaries once it's running.

Book 1 builds one full pass through all seven steps, mapped onto Gemini, ADK, and Antigravity. Each chapter states which step it is primarily teaching.

## Editorial standard for every chapter

Each chapter includes:

- the problem the chapter solves;
- learning objectives;
- its relationship to the Seven Steps;
- the WidgetWare increment;
- a recommended conceptual narrative;
- an implementation and lab outline;
- evaluation criteria;
- a chapter checkpoint; and
- a bridge to the next chapter.

The manuscript is designed to support both self-study and a live instructor-led course. Code examples should use standard, readable Python and ADK patterns. Avoid unnecessary asynchronous programming, decorators, metaprogramming, or framework abstractions that obscure the engineering concepts.
<!-- END 00_README.md -->

<!-- BEGIN 01_Foreword.md -->
# Foreword

Software engineering has always been shaped by changes in abstraction.

We moved from machine instructions to programming languages, from individual programs to operating systems, from physical servers to cloud platforms, and from manually configured infrastructure to declarative automation. Each transition changed not only what we could build, but also what engineers needed to understand.

Agent engineering is another such transition.

A language model can generate text, analyze information, write code, and reason about unfamiliar situations. Yet a useful enterprise system requires much more than a capable model. It needs the right context, controlled access to tools, reusable procedures, deterministic workflows, secure execution, observable behavior, and evidence that it performs reliably. Without those layers, an impressive demonstration remains only a demonstration.

This book is about those layers.

I have spent more than three decades building, architecting, teaching, and advising on enterprise technology. Across data warehousing, business intelligence, cloud computing, machine learning, and generative AI, one lesson has remained constant: the technology that attracts attention is rarely the whole system. The real work lies in turning promising capability into something dependable, inspectable, and useful.

That is the central argument of this book:

> An agent is not merely a model with a prompt. It is an engineered system in which probabilistic intelligence operates inside deterministic boundaries.

The distinction matters. A model may suggest what to do. Software must still decide what it is allowed to do, what data it may access, which tools it can call, how outputs are validated, when a person must approve an action, and how success or failure will be measured.

The title names three important parts of the development experience:

- **Gemini** supplies the model intelligence.
- **Agent Development Kit**, or ADK, supplies a code-first framework for agents, tools, sessions, workflows, and evaluation.
- **Antigravity** supplies the agent-assisted engineering environment in which we specify, inspect, build, test, and improve the system.

But the book is not simply a product tutorial. Products change. Interfaces evolve. Commands are replaced. The durable subject is **Agent Engineering**: the discipline of designing systems that combine model reasoning with context, tools, skills, workflows, evaluation, and guardrails.

To keep the discussion concrete, we will build one system throughout the book: the **WidgetWare SDR Lab**. WidgetWare is a fictional software company. Its Sales Development Representative process gives us a realistic mixture of open-ended reasoning and controlled business execution. The system must understand an ideal customer profile, research target companies, distinguish evidence from inference, qualify opportunities, draft relevant outreach, and stop for human approval before any external action.

This is intentionally not a fully autonomous sales machine. Autonomy is not the objective. Business value under controlled risk is the objective.

The lab also gives us a cumulative learning path. We begin with a bounded problem and a clean development workspace. We add context, then an ADK agent, reusable Skills, structured outputs, tools, evidence-backed research, multi-agent workflows, approval gates, evaluation, and deployment. At every stage, the reader should be able to inspect what changed and explain why it was added.

The intended reader does not need to be an advanced Python programmer. The implementation favors clear, conventional code over clever code. The deeper challenge is architectural judgment:

- When should reasoning be delegated to a model?
- When should behavior remain deterministic?
- What context is necessary, and what context is dangerous noise?
- Is a capability better represented as an instruction, a Skill, a tool, or another agent?
- How should agents exchange information without losing meaning?
- Where must human approval remain mandatory?
- What evidence would convince us that the system is improving?

These questions are more durable than any particular API call.

Book 1 focuses on foundations. By the end, you will have an inspectable, evaluated, deployable agent application. Book 2 will extend that application into a stateful and governed enterprise agent platform with persistent memory, enterprise retrieval, controlled loops, distributed collaboration, identity, security, observability, cost management, and continuous evaluation.

My hope is that this book helps readers move beyond two common extremes: fear that agents are uncontrollable, and excitement that ignores engineering discipline. Both are incomplete. Agent systems can be useful and trustworthy when we design them with humility, explicit boundaries, and measurable expectations.

The model supplies intelligence. Engineering makes that intelligence usable.

— **Venkatesh Tadinada**  
Head AI Consulting, CloudKarya, Inc.
<!-- END 01_Foreword.md -->

<!-- BEGIN 02_Introduction.md -->
# Introduction: Building Intelligence Inside Boundaries

## Why this book exists

The easiest way to build an agent demonstration is to connect a model to a prompt and a few tools. The easiest way to misunderstand agent engineering is to assume that the demonstration is the system.

A production-minded agent application must answer questions that a prompt alone cannot answer:

- What business objective is the agent responsible for?
- Which decisions may the model make?
- Which actions must remain deterministic?
- What information should be placed in context?
- Which tools may be used, and with what permissions?
- How are outputs validated before downstream systems consume them?
- How do multiple agents divide work and exchange results?
- When must a human approve the next step?
- How do we test a system whose outputs are not always identical?
- How do we observe, deploy, and improve it?

This book develops a practical answer through a cumulative system.

## The reference system: WidgetWare SDR

WidgetWare is a fictional business-to-business software company. It needs help identifying and researching prospective customers. A human Sales Development Representative typically performs several related jobs:

1. Understand the company’s products and ideal customer profile.
2. Identify a target account.
3. Research recent, relevant evidence about that account.
4. Determine whether the account appears qualified.
5. Explain the qualification decision.
6. Draft a personalized outreach message.
7. Obtain approval before contacting the prospect.

These activities are well suited to Agent Engineering because they contain both predictable steps and judgment-intensive work. Research and synthesis benefit from model reasoning. Validation, permissions, state transitions, and approval gates benefit from deterministic software.

The goal is not to replace every human activity. The goal is to construct a system in which the model performs the work it is good at while software and people retain control over high-risk decisions.

## The Seven Steps to Agent Engineering

The book uses one seven-step framework, applied consistently across every technology this series covers. Gemini, ADK, and Antigravity are this edition's implementation; the steps themselves are vendor-independent, because they describe engineering activities, not product features.

### 1. Frame the Use Case

Define the business objective, the intended users, what the system may and may not do, and the autonomy level it is permitted before any code exists. This is a discipline, not a formality — Chapter 1's WidgetWare charter and acceptance criteria are this step made concrete.

### 2. Build Context

Assemble the information Gemini reasons over: system instructions, business rules, ideal-customer-profile data, retrieved evidence, and task-specific state, deliberately separated so each can be inspected, tested, and changed independently.

### 3. Design Agent Capabilities

Choose or build the Skills, structured contracts, and tools the agent needs to do real work — the reusable procedures, typed interfaces, and controlled integrations that turn "a model that can reason about this" into "a capability the system can actually invoke."

### 4. Build the Harness

Establish the operating environment the agent runs inside: Antigravity as the specification-driven development harness, and ADK's own runtime — agents, sessions, events, and permissions — as the execution harness the built system runs on.

### 5. Orchestrate Workflows

Sequence steps, coordinate specialized agents, manage state transitions explicitly, and gate progress on human approval before any external or consequential action.

### 6. Engineer Loops

Take a workflow that has already been evaluated on one case and wrap it in a bounded process that discovers the next unit of work, persists state across interruptions, and decides — explicitly — whether to continue, retry, stop, defer, or escalate. This is a discipline in its own right, distinct from orchestrating a single pass through a workflow, and it is where Book 1 closes.

### 7. Evaluate & Govern

Measure whether the system is actually good — not merely whether it runs — and keep it inside its boundaries once it is. Book 1 builds the evaluation half of this step in depth; production monitoring and governance, the other half, are Book 2's concern.

## How Book 1 progresses

Book 1 is organized as a build sequence, and that sequence does not track the seven steps in numeric order — Chapter 2 builds the harness (Step 4) before Chapter 3 builds context (Step 2), because a reader needs a working Antigravity workspace before there is anywhere to put business rules. The steps describe a dependency structure among engineering concerns, not a fixed reading order.

- Chapter 1 establishes the discipline and defines the WidgetWare problem (Step 1).
- Chapter 2 creates the Antigravity development harness (Step 4).
- Chapter 3 designs model and context behavior (Step 2).
- Chapter 4 implements the first ADK agent (Step 4, continued).
- Chapter 5 extracts reusable Skills (Step 3).
- Chapter 6 introduces structured outputs and contracts (Step 3, continued).
- Chapter 7 adds controlled tools (Step 3, continued).
- Chapter 8 connects evidence-backed research through tools and MCP (Step 3, continued).
- Chapter 9 introduces multi-agent workflows and human approval (Step 5).
- Chapter 10 evaluates and deploys the integrated, single-account system (Step 7).
- Chapter 11 wraps that evaluated system in a bounded ADK loop that processes many accounts (Step 6) — Book 1's closing chapter.

Every chapter leaves the repository in a usable state. A reader should be able to begin from the previous checkpoint, complete the chapter, run the tests, and inspect the new capability.

## What Book 1 deliberately does not do

Book 1 introduces production thinking without attempting to solve every enterprise concern. It does not deeply implement:

- long-term memory;
- production-scale retrieval-augmented generation;
- distributed Agent-to-Agent collaboration;
- enterprise Agent Registry and Gateway governance;
- network containment;
- comprehensive Model Armor policies;
- model-routing economics;
- production-scale observability; or
- continuous online evaluation.

These topics belong in Book 2 because they are easier to understand after the reader has built and evaluated one complete agent application.

## A principle for the entire series

The book repeatedly asks a simple question:

> Is this behavior better expressed as model reasoning or deterministic software?

Use deterministic software when the required behavior is known. Use model reasoning when interpretation, synthesis, or adaptive judgment is required. Connect the two through typed contracts, explicit state, narrow tools, and measurable evaluation.

That balance is the foundation of inspectable agents.
<!-- END 02_Introduction.md -->

<!-- BEGIN 03_Chapter_01_From_Language_Models_to_Agent_Engineering.md -->
# Chapter 1: From Language Models to Agent Engineering

## Chapter purpose

This chapter establishes the conceptual foundation for the book. The reader learns why a language model is not an agent, why an agent is not automatically a useful system, and how Agent Engineering combines probabilistic intelligence with deterministic control.

## Learning objectives

By the end of this chapter, the reader should be able to:

- distinguish a model, assistant, workflow, agent, and agentic system;
- identify tasks that require reasoning versus deterministic execution;
- explain the autonomy spectrum;
- describe the seven engineering layers used in this book;
- define the WidgetWare SDR problem and its boundaries; and
- write measurable success criteria for the Book 1 system.

## Seven-Step mapping

**Primary:** Frame the Use Case  
**Supporting:** Evaluate & Govern

## The WidgetWare increment

Create the initial product brief for the WidgetWare SDR system:

- business objective;
- intended users;
- inputs and outputs;
- activities the system may perform;
- activities it must not perform;
- approval requirements; and
- measurable acceptance criteria.

## 1.1 A model is a capability, not a system

A language model predicts and generates language based on its training and current context. It can summarize, classify, compare, draft, infer, and reason. Those abilities are powerful, but they do not define responsibility, permission, persistence, or correctness.

A useful system must surround the model with engineered components. It needs instructions, state, tools, validation, workflows, observability, and tests. When those components are absent, the model may still produce an impressive response, but the response is difficult to trust or integrate.

## 1.2 Assistants, workflows, agents, and agentic systems

Use precise terms:

- A **model** supplies language and reasoning capability.
- An **assistant** responds to a user within a conversational interface.
- A **workflow** follows a predefined sequence of steps.
- An **agent** selects or adapts actions in pursuit of a goal.
- An **agentic system** combines one or more agents with tools, state, policies, workflows, evaluation, and human oversight.

Not every application needs an agent. A fixed transformation with known rules should normally remain deterministic. Agent behavior is justified when the system must interpret ambiguous input, select among alternatives, synthesize evidence, or adapt its approach.

## 1.3 The autonomy spectrum

Autonomy should be designed, not assumed.

A practical spectrum is:

1. **Answer only** — the model provides information.
2. **Recommend** — the model proposes an action.
3. **Draft** — the model creates an artifact for review.
4. **Prepare** — the system assembles the data and action parameters.
5. **Execute with approval** — a human authorizes the external action.
6. **Execute within policy** — the system acts autonomously inside narrow limits.
7. **Open-ended autonomy** — the system chooses goals and actions broadly.

WidgetWare will stop at level five. It may research, qualify, and draft, but outbound communication requires human approval.

## 1.4 Probabilistic reasoning inside deterministic boundaries

The central design pattern is simple:

- Let the model interpret, synthesize, and draft.
- Let software validate, authorize, persist, route, and enforce.

For example, Gemini may judge whether a company fits WidgetWare’s ideal customer profile. A deterministic schema validates the result. A workflow decides which step follows. A policy prevents message sending until approval exists.

This is more robust than asking one large prompt to do everything.

## 1.5 Introducing SDR and WidgetWare

SDR stands for **Sales Development Representative**. An SDR identifies potential customers, researches them, determines whether there is a plausible fit, and begins a conversation that may lead to a sales opportunity.

WidgetWare sells software that helps manufacturing and industrial-automation companies modernize plant operations and adopt AI-enabled automation. Its SDR process requires the system to understand:

- what WidgetWare sells;
- which industries and company characteristics indicate fit;
- what evidence supports a qualification decision;
- what recent events create a relevant reason to contact an account; and
- which statements are approved for outreach.

The system will not scrape indiscriminately, fabricate claims, or contact people without review.

## 1.6 Initial system boundary

### In scope

- accept a target company;
- retrieve approved account information;
- research permitted public evidence;
- evaluate fit against configured criteria;
- produce a structured qualification;
- draft an evidence-backed outreach message; and
- request human approval.

### Out of scope

- autonomous prospecting across uncontrolled sources;
- sending email or social messages;
- modifying CRM records without approval;
- inventing customer facts;
- bypassing authentication or source restrictions; and
- making legal, contractual, or pricing commitments.

## 1.7 Define success before implementation

The first evaluation criteria should be written before code:

- Every qualification result conforms to a schema.
- Every material factual claim includes evidence or is labeled as inference.
- The system does not draft outreach when evidence is insufficient.
- The system never sends a message.
- The system explains the qualification decision.
- The system produces a usable result for representative test accounts.

These are stronger than “the response looks good.”

## Hands-on lab: Write the system charter

Create:

- `README.md` — project purpose and quick start;
- `SPEC.md` — system behavior and constraints;
- `docs/widgetware-business-brief.md` — products, ICP, and exclusions;
- `docs/acceptance-criteria.md` — measurable success conditions; and
- `tests/scenarios/` — initial scenario descriptions.

No agent code is required yet.

## Evaluation checklist

- Is the business objective explicit?
- Are external actions clearly bounded?
- Is human approval mandatory where required?
- Can each acceptance criterion be tested?
- Is the distinction between evidence and inference explicit?
- Does the architecture avoid using an agent where a deterministic rule is sufficient?

## Chapter checkpoint

The repository now contains a clear problem definition and system boundary. The reader should be able to explain what the system will do, what it will not do, and what evidence will demonstrate success.

## Bridge to Chapter 2

The next chapter builds the engineering harness in Antigravity. Before giving the model more capability, we create the workspace, repository conventions, specifications, permissions, and test discipline that will keep development inspectable.

## Exercises

1. Using the autonomy spectrum in §1.3, pick a task you currently automate (or wish you could) and decide honestly which of the seven levels it sits at today, and which level it *should* sit at given how much you currently trust its output. WidgetWare stops at level five; justify in one sentence why your task should stop at the same level, a lower one, or a higher one.
2. Using §1.2's precise vocabulary, describe — without using the word "agent" — what distinguishes an assistant from a workflow, and a workflow from an agent. If you find yourself hedging, that is a sign to revisit this section once Chapter 9 introduces a full multi-agent workflow.
3. WidgetWare's evidence policy is fully specified in Chapter 3 (§3.5) and exercised again in Chapter 8. Before reading either chapter, use §1.6's in-scope and out-of-scope boundary to predict two or three situations where "cite your source" will be harder than it sounds. Revisit this list after Chapter 8 and check how many you anticipated correctly.
4. Using §1.4's central pattern — the model interprets and drafts; software validates, authorizes, persists, routes, and enforces — pick one activity from §1.6's in-scope list and write, in one sentence each, what the model is trusted to decide and what deterministic code must never let it decide alone.
5. Write your own version of §1.7's six success criteria for a WidgetWare capability not yet built — for example, "flag accounts where the qualification score conflicts with the SDR's own instinct." Try to make every criterion something a person could test mechanically, without asking you a clarifying question.
6. Using the Seven Steps to Agent Engineering introduced in this book's Introduction, pick any chapter from Chapter 2 onward before you read it and predict which step it will map to. After reading the chapter's own Seven-Step mapping, check your prediction — where a chapter's *Supporting* steps surprise you, write one sentence on why that step needed revisiting there.
<!-- END 03_Chapter_01_From_Language_Models_to_Agent_Engineering.md -->

<!-- BEGIN 04_Chapter_02_Building_with_Antigravity.md -->
# Chapter 2: Building with Antigravity

## Chapter purpose

This chapter turns the Book 1 concept into an inspectable development workspace. Antigravity is treated not as a magic code generator, but as an engineering harness whose agent-assisted capabilities operate within repository rules, specifications, tests, and human review.

## Learning objectives

By the end of this chapter, the reader should be able to:

- explain the role of an agent-assisted development harness;
- initialize and inspect the WidgetWare repository;
- separate product specification from implementation detail;
- establish coding, testing, and security conventions;
- give a coding agent bounded tasks with observable deliverables; and
- review generated changes before accepting them.

## Seven-Step mapping

**Primary:** Build the Harness  
**Supporting:** Design Agent Capabilities, Evaluate & Govern

## The WidgetWare increment

Create a reproducible Antigravity workspace containing the project specification, directory structure, environment configuration, baseline tests, and development instructions.

## 2.1 The harness is part of the system

The harness includes everything that makes model-assisted engineering controlled and repeatable:

- the IDE and command-line environment;
- repository structure;
- project instructions;
- dependency management;
- environment variables and secrets handling;
- code-quality checks;
- tests;
- permissions; and
- review practices.

A strong harness improves both human and coding-agent performance because it makes expectations explicit.

## 2.2 Antigravity as an engineering partner

Antigravity can inspect a repository, propose plans, create or modify files, run commands, and help diagnose failures. These capabilities should be used with a disciplined cycle:

1. State the objective.
2. Provide the relevant specification.
3. Ask for a plan.
4. Review the plan.
5. Permit a bounded implementation.
6. Inspect the diff.
7. Run tests.
8. Accept, revise, or revert.

The coding agent should not be given an unrestricted instruction such as “build the entire application.” Large, ambiguous tasks hide mistakes and make evaluation difficult.

## 2.3 Repository structure

A recommended initial structure is:

```text
widgetware-sdr/
├── README.md
├── SPEC.md
├── pyproject.toml
├── .env.example
├── docs/
│   ├── widgetware-business-brief.md
│   ├── architecture.md
│   └── acceptance-criteria.md
├── config/
│   ├── products.yaml
│   ├── icp.yaml
│   └── policies.yaml
├── src/
│   └── widgetware_sdr/
├── tests/
│   ├── unit/
│   ├── contracts/
│   └── scenarios/
└── scripts/
```

The structure separates business knowledge, policy, implementation, and evaluation.

## 2.4 README versus SPEC

`README.md` serves the reader and contributor. It should explain the project, setup, commands, and current status.

`SPEC.md` serves the implementation. It should define:

- required behavior;
- prohibited behavior;
- inputs and outputs;
- state transitions;
- error behavior;
- approval rules; and
- completion criteria.

The specification should remain technology-aware but not technology-dependent. For example, it should state that qualification output must validate against a contract, not merely that a particular Python class must be used.

## 2.5 Development instructions

Create concise repository instructions for both humans and coding agents:

- use standard Python;
- avoid unnecessary async code, decorators, or metaprogramming;
- prefer small functions and explicit types;
- write tests with each behavior change;
- never place credentials in source files;
- do not broaden tool permissions without review;
- preserve evidence references;
- do not implement external message sending in Book 1; and
- update documentation when behavior changes.

## 2.6 Specification-driven tasks

A good Antigravity task contains:

- one bounded objective;
- the files or modules in scope;
- the relevant acceptance criteria;
- explicit exclusions;
- commands that should pass; and
- the expected deliverable.

Example:

> Create the initial Python package and a health-check test. Do not add an ADK agent yet. Use the repository conventions in `SPEC.md`. The task is complete when the package imports successfully and all tests pass.

This is easier to inspect than an open-ended request.

## 2.7 Trust and permissions

Development agents can execute commands and modify files. Apply least privilege:

- review shell commands before execution when appropriate;
- restrict access to production credentials;
- use `.env.example` rather than real secrets;
- isolate experiments;
- inspect dependency additions;
- verify generated scripts; and
- keep version-control checkpoints.

The development agent is a powerful collaborator, not an unquestioned authority.

## Hands-on lab: Build the workspace

1. Create the repository structure.
2. Add `pyproject.toml` and a minimal package.
3. Add `.env.example` and secret-handling instructions.
4. Add a health-check function and test.
5. Add commands for formatting, linting, and testing.
6. Ask Antigravity to inspect the project and produce a gap report against `SPEC.md`.
7. Review and record the accepted changes.

## Evaluation checklist

- Can another learner clone and understand the repository?
- Are business rules separated from code?
- Are secrets excluded from source control?
- Can all baseline checks run with one documented command?
- Are Antigravity tasks bounded and reviewable?
- Does the repository contain a clear rollback point?

## Chapter checkpoint

The project now has an inspectable engineering harness. No business intelligence has been added yet, but the repository is ready for controlled development.

## Bridge to Chapter 3

The next chapter defines how Gemini will receive instructions and business context. The goal is not to create a larger prompt. It is to design an explicit context architecture that keeps stable policies, task data, and retrieved evidence separate.

## Exercises

1. Following §2.2's disciplined cycle, give Antigravity one deliberately unrestricted instruction ("build the entire application") on a throwaway branch, and separately give it a properly scoped task per §2.6's example. Compare what each produces and how long it actually took you to review each one with confidence.
2. §2.4 distinguishes `README.md` from `SPEC.md`. Take a project you maintain today and check whether it has a document playing SPEC's role — required behavior, prohibited behavior, state transitions, completion criteria — or whether that information only lives in your head or in code comments. Write the single most important missing sentence such a `SPEC.md` would need.
3. §2.5's development instructions include "do not implement external message sending in Book 1." Using §2.7's least-privilege list, write the equivalent hard boundary you would set for a coding agent working on a codebase you maintain — one instruction whose violation would be serious enough that you'd want it caught in every review, not just remembered.
4. §2.7 calls the development agent "a powerful collaborator, not an unquestioned authority." Recall (or imagine) a specific moment a coding agent proposed a change you almost accepted without reading closely. What in the diff should have made you slow down?
5. Using §2.3's repository structure, predict which directory each of the next four chapters' work will land in — `config/`, `src/widgetware_sdr/`, `skills/`, `tests/` — before reading them. Check your predictions once you reach Chapter 5.
<!-- END 04_Chapter_02_Building_with_Antigravity.md -->

<!-- BEGIN 05_Chapter_03_Gemini_Models_and_Context_Engineering.md -->
# Chapter 3: Gemini Models and Context Engineering

## Chapter purpose

This chapter designs the information environment in which Gemini reasons. The reader learns that context is an engineered input assembled from instructions, business configuration, task data, state, and evidence—not a single growing prompt.

## Learning objectives

By the end of this chapter, the reader should be able to:

- choose a model according to quality, latency, and cost requirements;
- distinguish system instructions, business context, task context, and retrieved evidence;
- separate stable policy from dynamic data;
- design an evidence policy;
- identify context pollution and prompt-injection risks; and
- test whether the model follows the intended scope.

## Seven-Step mapping

**Primary:** Build Context  
**Supporting:** Frame the Use Case, Evaluate & Govern

## The WidgetWare increment

Create the first complete context package for the SDR agent: role, business rules, ideal-customer profile, product facts, evidence policy, output expectations, and prohibited behavior.

## 3.1 Model choice is an architectural decision

Different model configurations may provide different tradeoffs in reasoning depth, response time, context capacity, and cost. Book 1 should begin with one supported Gemini model and keep the model identifier configurable.

Do not scatter model names throughout the code. Centralize selection so that evaluation can compare alternatives later.

The correct question is not “Which model is best?” It is:

> Which model provides sufficient quality for this task under the required latency and cost constraints?

## 3.2 Layers of context

Use separate layers:

### System instructions

Stable behavioral rules:

- the agent’s role;
- scope;
- safety constraints;
- evidence requirements;
- communication style; and
- prohibited actions.

### Business context

WidgetWare-specific knowledge:

- product definitions;
- ideal-customer profile;
- qualification rules;
- excluded industries;
- approved claims; and
- escalation rules.

### Task context

Information specific to the current request:

- target account;
- user objective;
- current workflow stage;
- supplied notes; and
- requested deliverable.

### Retrieved evidence

Tool or MCP results that support the current decision. Evidence should include source identity, retrieval time, and a compact excerpt or normalized fact.

### State

Structured information produced by previous steps, such as an account identifier, research status, or approval decision.

## 3.3 Stable policy should not be buried in prompts

Store stable business rules in explicit configuration where possible. For example:

```yaml
minimum_employee_count: 5000
maximum_employee_count: null  # no upper bound
preferred_industries:
  - manufacturing
  - industrial_automation
preferred_regions:
  - united_states
  - europe
  - india
buying_signals:
  - new_ai_leadership
  - digital_transformation_program
  - genai_hiring
requires_human_approval:
  - external_outreach
  - crm_write
```

The agent can receive a rendered view of the configuration, while deterministic code enforces non-negotiable rules.

## 3.4 Instruction hierarchy

A useful instruction architecture answers:

1. Who is the agent?
2. What goal does it pursue?
3. What information may it use?
4. How should it reason about uncertainty?
5. What format must it return?
6. What must it never do?
7. When should it stop or escalate?

Avoid instructions that are merely aspirational, such as “always be accurate.” Replace them with observable requirements: “Do not present a factual claim unless it is supported by a supplied source or explicitly labeled as an inference.”

## 3.5 Evidence policy

The WidgetWare evidence policy should distinguish:

- **verified fact** — directly supported by an approved source;
- **derived fact** — deterministically calculated from verified facts;
- **inference** — a reasoned conclusion that remains uncertain;
- **unknown** — insufficient evidence; and
- **conflict** — credible sources disagree.

The agent should not convert inference into fact through confident wording.

## 3.6 Context quality failures

Common failures include:

- irrelevant documents crowding out useful information;
- contradictory versions of business rules;
- stale data presented as current;
- user content overriding system policy;
- tool output copied without provenance;
- excessive examples that bias the result; and
- prior conversation state leaking into a new account.

Context engineering includes exclusion. The system should supply only what the current task needs.

## Hands-on lab: Build the context package

Create:

- `config/products.yaml`;
- `config/icp.yaml`;
- `config/policies.yaml`;
- `src/widgetware_sdr/instructions.py`;
- `src/widgetware_sdr/context_builder.py`; and
- tests that confirm required policy language is present.

Create at least four context tests:

1. A clearly qualified account.
2. A clearly unqualified account.
3. An account with insufficient evidence.
4. A malicious note that attempts to override policy.

## Evaluation checklist

- Are stable policies separate from task data?
- Is model selection configurable?
- Does the context identify evidence provenance?
- Can the agent represent uncertainty?
- Do injected instructions fail to override system constraints?
- Is the context compact enough to inspect manually?

## Chapter checkpoint

The project now has a deliberate model and context architecture. The next step is to connect this context to a real ADK agent and run the first complete reasoning interaction.

## Bridge to Chapter 4

Chapter 4 introduces the core ADK abstractions and builds the first WidgetWare agent. The emphasis remains narrow: one agent, one responsibility, clear inputs, observable events, and no external tools yet.

## Exercises

1. §3.2 separates context into five layers. Take a system prompt you've written for a real task and sort its contents into these five layers. How much of it turns out to actually be business context or task context masquerading as a system instruction?
2. §3.3's `icp.yaml` example states policy as data, not prose. Pick one rule from your own domain that you currently only state in a prompt (for example, "prefer accounts in these industries") and write it the way §3.3 would — as a value deterministic code can read, not a sentence a model has to reparse every time.
3. §3.6 lists seven context quality failures. Pick the one most likely to occur unnoticed in a system you maintain, and describe what evidence would tell you it was actually happening — a log line, a test that should exist but doesn't, or a specific pattern of complaint.
4. Using §3.5's five evidence categories — verified fact, derived fact, inference, unknown, conflict — take three claims from a real piece of business writing (an email, a report, a slide) and classify each one. Was any inference originally presented with the confidence of a verified fact?
5. §3.4 warns against aspirational instructions such as "always be accurate." Find one aspirational instruction in a prompt you've written and rewrite it as an observable requirement, the way §3.4 rewrites "always be accurate" into an explicit citation rule.
<!-- END 05_Chapter_03_Gemini_Models_and_Context_Engineering.md -->

<!-- BEGIN 06_Chapter_04_Your_First_Agent_with_ADK.md -->
# Chapter 4: Your First Agent with ADK

## Chapter purpose

This chapter implements the first working WidgetWare agent with Google Agent Development Kit. The goal is not feature breadth. It is to understand the smallest complete agent lifecycle: configuration, invocation, session, events, response, and test.

## Learning objectives

By the end of this chapter, the reader should be able to:

- describe ADK’s core application abstractions;
- configure an LLM agent with Gemini and system instructions;
- run the agent locally;
- understand sessions, events, and state at a foundational level;
- capture and inspect agent output; and
- create deterministic tests around a probabilistic component.

## Seven-Step mapping

**Primary:** Build the Harness  
**Supporting:** Design Agent Capabilities, Evaluate & Govern

## The WidgetWare increment

Build an **Account Qualification Assistant** that accepts a supplied account profile and returns a reasoned, human-readable recommendation. Structured output arrives in Chapter 6; this chapter focuses on the execution lifecycle.

## 4.1 ADK as an application framework

ADK provides a code-first way to define agents, connect models, attach tools, manage sessions, compose workflows, and evaluate behavior. In Book 1, keep the implementation explicit and readable.

The first agent needs:

- a name;
- a description;
- a Gemini model configuration;
- system instructions;
- an entry point or runner; and
- a local interface for testing.

## 4.2 The first agent boundary

The Account Qualification Assistant may:

- read the supplied account profile;
- compare it with WidgetWare’s configured ICP;
- explain likely fit and missing information; and
- recommend `QUALIFY`, `DO_NOT_QUALIFY`, or `NEEDS_RESEARCH` in prose.

It may not:

- search the internet;
- call external services;
- update CRM data;
- draft outreach; or
- claim facts that were not supplied.

A narrow boundary makes early failures easier to diagnose.

## 4.3 Sessions and events

A **session** represents the interaction context for a user or workflow. It may hold conversation history and state. An **event** records something that happened during execution, such as a model request, response, tool call, or state change.

Even when the first implementation is simple, inspect the event stream. Agent systems become easier to debug when execution is treated as a sequence of observable events rather than a single opaque response.

## 4.4 Basic state

Book 1 uses minimal state:

- `account_id`;
- `workflow_status`;
- `qualification_status`; and
- `approval_status`.

At this stage, only `account_id` and the current interaction are necessary. The remaining fields establish the vocabulary that later chapters will use.

## 4.5 Testing an LLM-backed agent

Do not require exact word-for-word output. Test stable properties:

- the agent does not invent missing revenue or employee counts;
- the response identifies missing evidence;
- the response references the configured ICP;
- prohibited external actions are not proposed as completed; and
- the execution completes without an unhandled error.

Use fixed test inputs and record representative outputs for human review.

## 4.6 Local playground and inspection

Run the agent through the supported local interface. During development, inspect:

- the assembled instructions;
- the user input;
- model configuration;
- session identifier;
- generated response;
- event sequence; and
- latency.

The ability to explain an execution is more important than visual polish.

## Hands-on lab: Implement the qualification assistant

Create:

- `src/widgetware_sdr/agents/qualification_agent.py`;
- `src/widgetware_sdr/app.py`;
- a local run command;
- sample account profiles under `data/sample_accounts/`; and
- scenario tests for qualified, unqualified, and uncertain accounts.

Suggested account profile fields:

```yaml
account_id: acme-001
company_name: Acme Manufacturing
industry: manufacturing
employee_count: 22000
region: united_states
known_challenges:
  - legacy plant-floor systems with no path to AI-enabled automation
source_notes:
  - source: customer_note
    text: The operations team still runs approvals through paper checklists.
```

## Evaluation checklist

- Does the agent start and run reproducibly?
- Are model and instructions loaded from centralized configuration?
- Can the event sequence be inspected?
- Does the agent stay within its boundary?
- Does it say when information is missing?
- Do scenario tests evaluate behavior rather than exact phrasing?

## Chapter checkpoint

The project now contains its first working ADK agent. It can reason about supplied account data but does not yet expose its procedure as a reusable Skill or return a machine-validated contract.

## Bridge to Chapter 5

Chapter 5 separates repeatable qualification knowledge from the agent definition. This creates a reusable Skill that can later be shared by multiple agents and evaluated independently.

## Exercises

1. §4.2 draws a narrow first-agent boundary — five things the Account Qualification Assistant may do, five it may not. Before reading Chapter 7, predict which of the "may not" items get lifted first, and in what order. Check your prediction once tools are introduced.
2. §4.5 insists on testing stable properties, not exact wording. Take one of your own scenario tests (real or hypothetical) for an LLM-backed feature and check whether it's actually asserting exact phrasing in disguise — a string match that would fail if the model rephrased a correct answer.
3. Using §4.3's distinction between a session and an event, describe from memory — or by re-running the Hands-on Lab — what a single call to the qualification assistant actually produced as its event sequence. Could you explain, from the events alone, why it reached its conclusion?
4. §4.4 lists four state fields Book 1 will use, but says only `account_id` matters yet. Predict which chapter first makes real use of `workflow_status`, and which first makes real use of `approval_status`, before reading further.
5. §4.6 says "the ability to explain an execution is more important than visual polish." Run the local playground against one uncertain-evidence account from your Hands-on Lab and write, in plain language, exactly why the agent reached the recommendation it did — citing the actual assembled instructions and event sequence, not a paraphrase from memory.
<!-- END 06_Chapter_04_Your_First_Agent_with_ADK.md -->

<!-- BEGIN 07_Chapter_05_Skills_and_Reusable_Agent_Capabilities.md -->
# Chapter 5: Skills and Reusable Agent Capabilities

## Chapter purpose

This chapter introduces Skills as reusable, inspectable procedures. A Skill captures how a task should be performed without turning every business procedure into application code or embedding it permanently inside one agent prompt.

## Learning objectives

By the end of this chapter, the reader should be able to:

- distinguish a Skill from a prompt, tool, workflow, and agent;
- identify procedures worth extracting into Skills;
- design a Skill with inputs, steps, quality criteria, and examples;
- keep business procedures versionable and testable; and
- attach a Skill to the WidgetWare qualification agent.

## Seven-Step mapping

**Primary:** Design Agent Capabilities  
**Supporting:** Build Context, Build the Harness, Evaluate & Govern

## The WidgetWare increment

Extract the account-qualification procedure into a reusable **ICP Qualification Skill**. The agent remains responsible for the task, while the Skill supplies the repeatable method.

## 5.1 Why Skills matter

As agent systems grow, important procedures often become duplicated across instructions, prompts, notebooks, and code. Duplication creates inconsistent behavior and makes improvement difficult.

A Skill creates a named unit of reusable know-how. It may include:

- purpose;
- prerequisites;
- input expectations;
- ordered reasoning steps;
- rules and exceptions;
- examples;
- output expectations; and
- evaluation criteria.

Skills make procedures easier to discover, review, reuse, and version.

## 5.2 Skill versus prompt

A prompt is an invocation or instruction for a particular interaction. A Skill is a maintained capability that can support many interactions.

“Evaluate this company” is a prompt.

“WidgetWare ICP Qualification” is a Skill that describes how qualification should be performed, what evidence matters, how uncertainty is represented, and what quality standards apply.

## 5.3 Skill versus tool

A Skill tells the agent **how to perform a task**. A tool allows the agent to **do something outside the model**.

For example:

- The qualification Skill explains how to compare an account with ICP criteria.
- An account-data tool retrieves employee count and industry.

The two work together but solve different problems.

## 5.4 Skill versus workflow

A Skill is reusable procedure or expertise. A workflow coordinates stages and state.

“Assess evidence quality” can be a Skill.

“Research, qualify, draft, then request approval” is a workflow.

## 5.5 Anatomy of a useful Skill

The ICP Qualification Skill should contain:

### Identity

- Name
- Version
- Owner
- Purpose

### Inputs

- normalized account profile;
- current ICP configuration; and
- available evidence.

### Procedure

1. Check explicit exclusion criteria.
2. Compare company attributes with ICP thresholds.
3. Identify confirmed pain signals.
4. Identify missing evidence.
5. Distinguish fact from inference.
6. Select a provisional outcome.
7. Explain the outcome and uncertainty.

### Quality criteria

- no fabricated account attributes;
- all decisive claims trace to input evidence;
- exclusions override positive heuristics;
- insufficient evidence produces `NEEDS_RESEARCH`; and
- rationale is concise and actionable.

### Examples

Include one positive, one negative, and one ambiguous example. Examples should illustrate the rules rather than encourage imitation of irrelevant wording.

## 5.6 Progressive disclosure

Do not force every Skill detail into every model call. A Skill can expose a concise description for discovery and load detailed instructions only when selected. This reduces context consumption and keeps irrelevant procedures out of the reasoning window.

## 5.7 Versioning and ownership

A business Skill should have an owner and version because changing the procedure may change business outcomes. Record:

- why a change was made;
- which evaluation cases it affects;
- whether the output contract changed; and
- whether prior results must be revisited.

Skills are organizational assets, not anonymous prompt fragments.

## Hands-on lab: Create the qualification Skill

Create a Skill directory such as:

```text
skills/
└── icp_qualification/
    ├── skill.md
    ├── examples/
    │   ├── qualified.md
    │   ├── unqualified.md
    │   └── needs_research.md
    └── tests/
        └── cases.yaml
```

Update the qualification agent so that its procedure comes from the Skill rather than a large embedded instruction block.

Add a second lightweight Skill: **Evidence Classification**, which labels supplied information as verified fact, inference, unknown, or conflict.

## Evaluation checklist

- Is the Skill reusable by more than one agent?
- Are its inputs and outputs explicit?
- Does it contain a real procedure rather than generic advice?
- Are rules and exceptions testable?
- Are examples minimal and representative?
- Is ownership and version information present?

## Chapter checkpoint

The qualification procedure is now a reusable asset. The agent can apply consistent business judgment, but its output is still primarily natural language.

## Bridge to Chapter 6

Chapter 6 replaces ambiguous prose interfaces with typed contracts. This allows workflows, tests, and downstream components to consume agent results safely.

## Exercises

1. §5.3 distinguishes a Skill (how to perform a task) from a tool (doing something outside the model). Take one procedure and one external action from your own domain and confirm you can sort them correctly. Is there anything you currently implement as a tool that is actually a Skill in disguise, or the reverse?
2. Using §5.5's anatomy, draft only the "Procedure" section — the ordered steps — for a Skill you don't yet have: something you personally do by habit rather than by written rule. Where did you struggle to make step 2 or 3 explicit?
3. §5.6 (progressive disclosure) argues a Skill should expose a concise description for discovery and load full detail only when selected. Look at the `skill.md` you built in the Hands-on Lab: if a second, unrelated agent had to decide whether this Skill applies to its task, does the discovery description alone give it enough to decide correctly?
4. §5.7 requires an owner and version for a business Skill. Imagine the ICP thresholds in the qualification Skill change three months from now. Using §5.7's four record-keeping questions, write what that change's record would actually say.
5. Using §5.4's distinction between a Skill and a workflow, predict which of Chapter 9's five named agents will use the ICP Qualification Skill directly, and which will use a different Skill or none at all. Check your prediction once you reach Chapter 9.
<!-- END 07_Chapter_05_Skills_and_Reusable_Agent_Capabilities.md -->

<!-- BEGIN 08_Chapter_06_Structured_Outputs_and_Agent_Contracts.md -->
# Chapter 6: Structured Outputs and Agent Contracts

## Chapter purpose

This chapter converts agent responses from human-readable suggestions into validated system interfaces. Structured contracts allow probabilistic reasoning to participate safely in deterministic workflows.

## Learning objectives

By the end of this chapter, the reader should be able to:

- explain why free-form prose is an unsafe integration boundary;
- design typed output schemas;
- represent confidence, uncertainty, evidence, and errors explicitly;
- validate and reject malformed responses;
- distinguish semantic evaluation from schema validation; and
- create typed handoffs for later multi-agent workflows.

## Seven-Step mapping

**Primary:** Design Agent Capabilities  
**Supporting:** Orchestrate Workflows, Evaluate & Govern

## The WidgetWare increment

Replace the qualification assistant’s prose-only result with a validated `QualificationResult` contract.

## 6.1 Prose is for people; contracts are for systems

A response such as “Acme looks like a strong opportunity” may be understandable to a person, but software cannot reliably determine:

- the final status;
- the decisive criteria;
- which evidence supports the decision;
- what information is missing;
- whether confidence is sufficient; or
- what the next workflow step should be.

A contract makes those elements explicit.

## 6.2 Designing the qualification schema

A useful result may contain:

```text
QualificationResult
- account_id
- status
- score
- rationale
- matched_criteria[]
- exclusion_reasons[]
- evidence_refs[]
- missing_information[]
- confidence
- recommended_next_step
- errors[]
```

Use enumerations for stable states:

- `QUALIFIED`
- `NOT_QUALIFIED`
- `NEEDS_RESEARCH`
- `BLOCKED`

Do not encode workflow state in arbitrary prose.

## 6.3 Confidence is not probability

A model-provided confidence value is a self-assessment, not a calibrated probability. It can still be useful when combined with rules:

- low confidence always routes to research or review;
- missing decisive evidence prevents qualification;
- explicit exclusions override confidence; and
- evaluation measures whether confidence correlates with correctness.

Do not treat `0.92` as scientific certainty merely because it contains decimals.

## 6.4 Evidence references

The result should refer to evidence by stable identifiers rather than copying large passages. An evidence object may include:

```text
EvidenceItem
- evidence_id
- source_type
- source_uri or source_name
- retrieved_at
- claim
- excerpt
- freshness
- reliability
```

The qualification result then lists the evidence identifiers that support each decisive claim.

## 6.5 Validation and repair

A structured-output pipeline should:

1. request the expected schema;
2. parse the response;
3. validate types and required fields;
4. enforce deterministic business rules;
5. optionally request a bounded repair for format errors; and
6. fail safely if the contract remains invalid.

Never silently coerce a materially ambiguous status.

## 6.6 Semantic correctness remains separate

Schema validation can prove that `status` contains an allowed value. It cannot prove that the chosen value is justified.

Use two layers:

- **contract tests** for format, required fields, and invariants;
- **evaluation cases** for reasoning quality, evidence use, and business correctness.

Both are required.

## 6.7 Designing for handoffs

Contracts should be designed for the next component. The future research agent needs a list of missing questions. The outreach agent needs approved facts and positioning angles. The approval interface needs the draft, evidence, and risk flags.

A handoff contract should be sufficient but not bloated. Passing an entire conversation history increases coupling and context noise.

## Hands-on lab: Add typed contracts

Create:

- `src/widgetware_sdr/contracts/evidence.py`;
- `src/widgetware_sdr/contracts/qualification.py`;
- schema validation tests;
- business invariant tests; and
- a serialization format for chapter checkpoints.

Add deterministic rules such as:

- `NOT_QUALIFIED` requires at least one exclusion or failed criterion;
- `QUALIFIED` requires at least one evidence reference;
- `NEEDS_RESEARCH` requires at least one missing-information item; and
- any parsing or policy failure produces `BLOCKED` rather than a guessed result.

## Evaluation checklist

- Can downstream code consume the result without parsing prose?
- Are all workflow states enumerated?
- Are uncertainty and missing information explicit?
- Do decisive claims reference evidence?
- Are deterministic invariants enforced after model output?
- Does invalid output fail safely?

## Chapter checkpoint

The WidgetWare qualification agent now produces a machine-validated result that remains readable to a person. This contract will become the interface between agents and workflow stages.

## Bridge to Chapter 7

Chapter 7 gives the system controlled capabilities. The agent will retrieve account data through narrow tools whose inputs, permissions, errors, and outputs are as carefully engineered as the agent contract.

## Exercises

1. Take the prose result "Acme looks like a strong opportunity" from §6.1 and write out the six things §6.1 says software cannot reliably determine from it. Now look at your own `QualificationResult` output from the Hands-on Lab — does it actually answer all six?
2. §6.3 warns that a confidence value is a self-assessment, not a calibrated probability. Design one deterministic rule, in plain language, that would prevent your system from treating a 0.95 confidence score as sufficient justification on its own, mirroring the four rules in §6.3.
3. §6.5 lists six pipeline steps ending in "fail safely if the contract remains invalid." Deliberately feed your qualification agent an account likely to produce a borderline or malformed result. Does it reach `BLOCKED`, or does it silently produce something plausible-looking instead?
4. Using §6.7's handoff-design principle — sufficient but not bloated — look at your `QualificationResult` contract and identify one field a downstream agent genuinely needs that's currently missing, and one field that's present but that none of Chapter 9's agents will actually use.
5. §6.6 requires two separate layers: contract tests and evaluation cases. Write one evaluation case, in plain language — the account, the expected reasoning — that a contract test could never catch, because the schema would validate a wrong answer just as easily as a right one.
<!-- END 08_Chapter_06_Structured_Outputs_and_Agent_Contracts.md -->

<!-- BEGIN 09_Chapter_07_Tool_Engineering.md -->
# Chapter 7: Tool Engineering

## Chapter purpose

This chapter connects model reasoning to external capabilities through narrow, typed, permissioned tools. The reader learns that a tool is not merely a function exposed to a model; it is a security and reliability boundary.

## Learning objectives

By the end of this chapter, the reader should be able to:

- decide when a capability should be implemented as a tool;
- design clear tool names, descriptions, and schemas;
- validate tool inputs and normalize outputs;
- apply least privilege and isolation;
- handle timeouts, retries, and errors explicitly;
- mock tools for evaluation; and
- prevent tool output from bypassing evidence and policy rules.

## Seven-Step mapping

**Primary:** Design Agent Capabilities  
**Supporting:** Build the Harness, Evaluate & Govern

## The WidgetWare increment

Add controlled tools for retrieving internal account records, product facts, and approved business configuration. The system still does not use open web research or external message delivery.

## 7.1 When a tool is appropriate

A model should not pretend to know information that belongs in a system of record. Use a tool when the application needs to:

- retrieve current data;
- perform a deterministic calculation;
- interact with an external system;
- access a protected resource;
- execute a side effect; or
- obtain information too large or dynamic for static context.

Do not use a tool for behavior that can be expressed as a simple deterministic function within the application, unless isolation or reuse justifies it.

## 7.2 Tool descriptions are part of control

The model selects tools based on their names and descriptions. A good description states:

- what the tool does;
- when it should be used;
- when it should not be used;
- required inputs;
- important limitations; and
- whether it has side effects.

Avoid vague tools such as `get_data`. Prefer `get_account_profile(account_id)`.

## 7.3 Input schemas

Use narrow, typed inputs. Validate before execution.

For example:

```text
get_account_profile
- account_id: non-empty string
- include_fields: optional approved enumeration
```

Do not allow arbitrary query text to reach a database or command shell. The tool owns translation from safe parameters to the underlying operation.

## 7.4 Output normalization

Return compact, predictable results. A tool result should indicate:

- success or failure;
- normalized data;
- source identity;
- retrieval time;
- warnings;
- retryability; and
- error category.

Large raw payloads consume context and expose irrelevant data. Normalize before returning information to the model.

## 7.5 Least privilege

Each tool should receive only the permission it requires. A read-only account lookup should not use credentials capable of updating CRM data. Book 1 can demonstrate this principle with separate interfaces even when the backing data is local.

Least privilege applies to:

- cloud IAM;
- service credentials;
- file access;
- network access;
- data fields; and
- allowed operations.

## 7.6 Failures are part of the contract

Tools fail. Design for:

- invalid input;
- not found;
- permission denied;
- timeout;
- dependency unavailable;
- rate limit;
- malformed upstream data; and
- partial result.

The model should not convert a failed lookup into a fabricated answer. A retry should occur only when the error is retryable and within a bounded policy.

## 7.7 Side effects require stronger controls

A read tool and a write tool should not be treated equally. Side-effecting tools require:

- idempotency where possible;
- explicit confirmation;
- audit information;
- narrow scope;
- rollback or compensation strategy; and
- policy checks outside the model.

Book 1 intentionally omits the send-message tool. The architecture will represent approval without exposing autonomous outreach execution.

## 7.8 Tool testing

Test tools independently from agents:

- valid input;
- invalid input;
- missing record;
- dependency failure;
- permission failure;
- deterministic output shape; and
- redaction of prohibited fields.

Then test the agent with mock tools so that evaluation is reproducible.

## Hands-on lab: Add internal data tools

Implement:

- `get_account_profile(account_id)`;
- `get_widgetware_product(product_id)`;
- `get_icp_policy()`; and
- a deterministic `calculate_fit_score()` helper that remains outside model reasoning.

Attach the read tools to the qualification agent. Update the contract so that every retrieved fact receives an evidence identifier.

## Evaluation checklist

- Does every tool have a single clear responsibility?
- Are inputs typed and validated?
- Are permissions narrower than the underlying platform account?
- Are outputs compact and sourced?
- Are failures explicit and non-fabricating?
- Can the agent be evaluated with tool mocks?
- Are side effects absent or guarded?

## Chapter checkpoint

The agent can now obtain trusted internal data through controlled interfaces. Its next challenge is external evidence: researching a company without confusing web content, tool output, inference, and instruction.

## Bridge to Chapter 8

Chapter 8 builds an evidence-backed research pipeline and introduces MCP as a standardized integration mechanism. The focus is provenance, source quality, and resistance to malicious or irrelevant content.

## Exercises

1. §7.1 lists when a tool is appropriate. Take one capability from your own domain currently implemented as a tool and check it against the list — does it actually need to be a tool, or could it be a deterministic function called directly, per §7.1's closing caveat?
2. §7.2 says a model selects tools by name and description alone. Write the description you'd give `get_account_profile` if you were deliberately trying to get an agent to misuse it — call it with the wrong account, or use it when it shouldn't — then write the corrected version and identify exactly what changed.
3. §7.5 (least privilege) asks you to imagine a read-only tool sharing credentials with a write-capable one. Audit one tool from your Hands-on Lab: what is the most damaging action its current credentials would actually permit, whether or not the tool's code ever performs that action?
4. §7.6 lists eight tool failure modes. Pick the one your `get_account_profile` implementation currently handles worst, or wouldn't distinguish from success, and describe what a caller sees today versus what §7.6 says they should see.
5. §7.7 says Book 1 "intentionally omits the send-message tool." Predict what each of §7.7's five side-effect controls — idempotency, explicit confirmation, audit information, narrow scope, rollback — would concretely mean the day a send tool is finally added.
6. §7.8 requires testing tools independently from agents, then testing the agent with mocks. Run your qualification agent with a mock `get_account_profile` that returns a `permission_denied` error. Does the agent handle it the way §7.6 requires, or does it do something the chapter would call fabrication?
<!-- END 09_Chapter_07_Tool_Engineering.md -->

<!-- BEGIN 10_Chapter_08_Evidence_Backed_Research_with_MCP.md -->
# Chapter 8: Evidence-Backed Research with MCP

## Chapter purpose

This chapter teaches the system to research external information without turning retrieval into unverified context. It introduces an evidence pipeline and explains when standardized MCP integrations are preferable to custom function tools.

## Learning objectives

By the end of this chapter, the reader should be able to:

- design research as a sequence of claims, sources, and evidence;
- distinguish retrieval from reasoning;
- evaluate source quality, freshness, and conflict;
- explain function tools versus MCP;
- connect an ADK agent to an approved MCP service;
- prevent retrieved content from overriding system policy; and
- produce an inspectable evidence-backed account brief.

## Seven-Step mapping

**Primary:** Design Agent Capabilities  
**Supporting:** Build Context, Evaluate & Govern

## The WidgetWare increment

Add an Account Research capability that gathers approved public evidence, normalizes it into an evidence ledger, and produces a structured research brief for qualification.

## 8.1 Research is not one model call

A robust research process separates:

1. the questions to answer;
2. source discovery;
3. source retrieval;
4. evidence extraction;
5. source assessment;
6. contradiction detection;
7. synthesis; and
8. citation.

The model may assist at several stages, but the system should preserve provenance throughout.

## 8.2 Claims and evidence

Begin with explicit research questions, such as:

- What industry does the company operate in?
- Approximately how large is it?
- Does it show evidence of legacy plant-floor systems or automation gaps?
- Has it announced a digital-transformation or AI initiative?
- Is there a recent trigger event relevant to WidgetWare?

For every resulting claim, record the supporting evidence. A research brief should never contain a floating factual assertion whose source has been lost.

## 8.3 Source quality and freshness

Assess sources according to the claim:

- official company material is strong for product announcements;
- regulatory filings may be strong for financial or organizational facts;
- reputable reporting may provide context;
- directories and aggregators may be useful but require caution;
- social posts may indicate intent but may not establish fact.

Freshness should be explicit. A five-year-old employee count may not support a current qualification decision.

## 8.4 Contradictions

When sources disagree, do not choose the most convenient result. Record:

- the conflicting values;
- source dates;
- source types;
- likely explanation; and
- whether the conflict affects qualification.

The appropriate outcome may be `NEEDS_RESEARCH`.

## 8.5 Function tools versus MCP

Use a custom function tool when:

- the integration is application-specific;
- the interface is narrow;
- the application owns the implementation; or
- deterministic control is more important than portability.

Use MCP when:

- a standardized server already exposes the capability;
- multiple agents or clients need the integration;
- discovery and portability matter; or
- enterprise systems are exposed through governed MCP services.

MCP does not remove the need for permission, input validation, provenance, or output filtering.

## 8.6 Retrieved content is untrusted data

External content may contain instructions such as “ignore your rules” or “send this secret.” Treat retrieved text as data, not authority.

Controls include:

- isolate source text from system instructions;
- label its origin;
- extract only task-relevant evidence;
- avoid executing commands found in content;
- redact secrets and unnecessary personal data;
- restrict accessible MCP servers and methods; and
- validate the final brief against the evidence ledger.

## 8.7 The evidence ledger

Create a durable structure:

```text
ResearchBrief
- account_id
- research_questions[]
- evidence_items[]
- claims[]
- conflicts[]
- unknowns[]
- trigger_events[]
- summary
- recommended_next_step
```

Each claim links to one or more evidence items. Each evidence item records source, date, excerpt, and reliability assessment.

## Hands-on lab: Build account research

1. Add a `research_account` agent or capability.
2. Connect one approved research source through a function tool or MCP service.
3. Normalize results into `EvidenceItem` contracts.
4. Implement an Evidence Classification Skill.
5. Produce a `ResearchBrief`.
6. Add a validation check that rejects uncited material claims.
7. Test an input containing prompt-injection text.
8. Test two conflicting sources.

## Evaluation checklist

- Does every material claim link to evidence?
- Are source date and type preserved?
- Are conflicts visible rather than silently resolved?
- Does retrieved text remain subordinate to system policy?
- Are MCP permissions and methods restricted?
- Can the research brief be reproduced from mocked evidence?
- Does insufficient evidence stop the workflow appropriately?

## Chapter checkpoint

WidgetWare can now produce an inspectable account research brief. Research and qualification are still separate capabilities; the next chapter coordinates them as a multi-agent workflow and adds the human approval boundary.

## Bridge to Chapter 9

Chapter 9 introduces specialized agents, typed handoffs, workflow orchestration, partial-failure handling, bounded iteration, and an approval gate before outreach.

## Exercises

1. §8.5 gives four conditions favoring MCP over a function tool. Take the one research source you connected in the Hands-on Lab and argue, honestly, whether MCP was the right call for it under those four conditions — or whether a function tool would have been more honest about what the integration actually is.
2. §8.6 lists seven controls against untrusted retrieved content. Re-run your prompt-injection test, but change the injected instruction to something more subtle than "ignore your rules" — for example, retrieved text stating a false but plausible employee count as if it were the company's own official figure. Does your evidence pipeline catch a false *fact* as readily as it catches an obvious override attempt?
3. §8.4 says contradictions should not be resolved by picking the most convenient result. Using your two-conflicting-sources test, write out what "the most convenient result" would have been for a WidgetWare SDR eager to hit quota, and confirm your `ResearchBrief` actually resisted that pull.
4. §8.2 gives five research questions. Add a sixth, specific to a signal WidgetWare's ICP (Chapter 3) cares about but isn't already covered, and explain what evidence would actually answer it.
5. §8.3 treats a five-year-old employee count as potentially unusable for a current decision. Pick one evidence item from your `ResearchBrief` and write what "sufficiently current" should mean for that specific kind of fact — a number of days, months, or years — and why.
<!-- END 10_Chapter_08_Evidence_Backed_Research_with_MCP.md -->

<!-- BEGIN 11_Chapter_09_Multi_Agent_Workflows_and_Human_Approval.md -->
# Chapter 9: Multi-Agent Workflows and Human Approval

## Chapter purpose

This chapter composes the Book 1 capabilities into a controlled multi-agent workflow. Specialized agents perform narrow tasks, exchange typed results, and stop for human approval before any external action.

## Learning objectives

By the end of this chapter, the reader should be able to:

- decide when specialization justifies multiple agents;
- compare sequential, parallel, and manager-worker patterns;
- design typed handoffs and shared state;
- handle partial failure and bounded retries;
- separate workflow control from model judgment;
- implement a human approval gate; and
- explain why approval must be enforced outside natural-language instructions.

## Seven-Step mapping

**Primary:** Orchestrate Workflows  
**Supporting:** Design Agent Capabilities, Evaluate & Govern

## The WidgetWare increment

Build the Book 1 workflow:

**Account Intake → Research → Qualification → Evidence Review → Outreach Draft → Human Approval**

No send action is implemented.

## 9.1 Why multiple agents

A single agent can perform many tasks, but broad responsibility creates several problems:

- instructions become crowded;
- context becomes irrelevant or contradictory;
- evaluation cannot isolate failure;
- permissions become overly broad;
- outputs become difficult to contract; and
- changes to one procedure affect unrelated behavior.

Create another agent when the task has a distinct goal, context, tool set, contract, or evaluation standard.

WidgetWare uses:

- **Research Agent** — gathers and normalizes evidence;
- **Qualification Agent** — evaluates fit;
- **Evidence Reviewer** — checks support and contradictions;
- **Outreach Drafting Agent** — creates a message from approved facts; and
- **Workflow Coordinator** — manages state and transitions.

## 9.2 Workflow patterns

### Sequential

Each stage depends on the previous stage. WidgetWare’s Book 1 flow is primarily sequential.

### Parallel

Independent tasks run concurrently. Book 1 may mention this pattern but does not require complex parallel code.

### Manager-worker

A coordinator delegates work and combines results. The coordinator should manage task state, not become another unrestricted reasoning agent by default.

### Loop

A stage repeats until a condition is met. This chapter uses only bounded repair or research retries within one account's workflow — repeating a step, not repeating the whole workflow across many accounts. Chapter 11 wraps this entire workflow in that outer loop; adaptive, multi-agent loops that change their own strategy belong in Book 2.

## 9.3 State machine before agent prompt

Represent workflow state explicitly:

- `RECEIVED`
- `RESEARCHING`
- `RESEARCH_COMPLETE`
- `QUALIFYING`
- `REVIEW_REQUIRED`
- `DRAFT_READY`
- `AWAITING_APPROVAL`
- `APPROVED`
- `REJECTED`
- `BLOCKED`

A model may recommend the next step, but deterministic code validates whether the transition is allowed.

## 9.4 Typed handoffs

Pass contracts, not transcripts:

- Research Agent returns `ResearchBrief`.
- Qualification Agent consumes `ResearchBrief` and returns `QualificationResult`.
- Evidence Reviewer returns `EvidenceReview`.
- Outreach Agent consumes only approved evidence and returns `OutreachDraft`.

This reduces context coupling and makes each agent independently testable.

## 9.5 Evidence review before drafting

The Evidence Reviewer should verify:

- decisive qualification claims have citations;
- the sources are sufficiently current;
- contradictions are surfaced;
- the draftable facts are approved;
- unsupported claims are removed; and
- remaining uncertainty is disclosed.

An outreach agent should not independently browse for more persuasive facts after review. That would bypass the evidence gate.

## 9.6 Human-in-the-loop approval

Approval is a workflow state and policy decision, not merely an instruction saying “ask the user first.”

The approval package should contain:

- target account;
- qualification summary;
- supporting evidence;
- proposed outreach;
- uncertainty and risk flags;
- requested action; and
- approve, reject, or revise controls.

The system must remain unable to execute the external action without an approved state.

## 9.7 Partial failure

Possible failures include:

- research source unavailable;
- insufficient evidence;
- malformed agent output;
- reviewer rejects unsupported claims;
- drafting agent fails;
- user rejects the draft; and
- workflow is resumed after interruption.

Each failure should produce a visible state and next action. Avoid restarting the entire workflow when only one stage needs repair.

## Hands-on lab: Compose the workflow

Implement:

- agent modules for research, qualification, review, and drafting;
- workflow contracts;
- deterministic state transitions;
- an approval record;
- a simple local approval interface;
- checkpoint persistence; and
- scenario tests for success, insufficient evidence, source conflict, malformed output, and rejected approval.

The final stage should be `AWAITING_APPROVAL`. An approval may update state to `APPROVED`, but Book 1 does not contain a send tool.

## Evaluation checklist

- Does each agent have one primary responsibility?
- Are handoffs typed and minimal?
- Are state transitions enforced deterministically?
- Can one stage fail without losing prior successful work?
- Is outreach based only on reviewed evidence?
- Is human approval unavoidable before external action?
- Can the workflow resume from a checkpoint?

## Chapter checkpoint

WidgetWare is now a complete bounded agent system. It can research, qualify, review, and draft while preserving evidence and requiring human approval.

## Bridge to Chapter 10

The final chapter asks whether the system is actually good enough. We will build evaluation datasets, inspect trajectories, test failure conditions, add observability, and deploy the integrated application.

## Exercises

1. §9.1 lists six reasons a single agent's broad responsibility becomes a problem. Using your own qualification-and-research code as it stood at the end of Chapter 8, before this chapter's split, identify which one or two of those six reasons had already started to appear, even if you hadn't named the problem yet.
2. §9.3 requires the state machine to exist before the agent prompts. Draw, on paper, the ten states from §9.3, then trace by hand what happens to an account that fails research twice before succeeding on a third attempt — which states does it pass through, and how many times does it revisit `RESEARCHING`?
3. §9.5 says the outreach agent must not independently browse for more persuasive facts after review, calling that a bypass of the evidence gate. Describe a realistic, well-intentioned reason a future engineer might be tempted to add exactly that shortcut, and what you would say to talk them out of it.
4. §9.7 lists seven partial-failure modes. Pick the one your workflow currently handles by restarting more of the process than §9.7 says it should, and describe the smallest change that would let it resume from the actual point of failure instead.
5. §9.6 insists approval is "a workflow state and policy decision," not an instruction asking politely. Find the exact line of code — or the exact absence of one — that makes it *structurally* impossible to skip approval in your workflow, not just unlikely. If you cannot point to one, that is the gap this exercise is meant to surface.
<!-- END 11_Chapter_09_Multi_Agent_Workflows_and_Human_Approval.md -->

<!-- BEGIN 12_Chapter_10_Evaluate_Deploy_and_Demonstrate.md -->
# Chapter 10: Evaluate, Deploy, and Demonstrate

## Chapter purpose

This chapter turns a working application into an evaluated and deployable Book 1 release. The reader learns to measure final-answer quality, contract compliance, tool behavior, workflow trajectories, safety boundaries, latency, and operational readiness.

## Learning objectives

By the end of this chapter, the reader should be able to:

- build a representative golden dataset;
- separate unit, contract, scenario, and semantic evaluation;
- evaluate tool trajectories and workflow state transitions;
- define pass criteria and release gates;
- add basic logs and traces;
- compare deployment options at a high level;
- deploy the WidgetWare application; and
- demonstrate both success and controlled failure.

## Seven-Step mapping

**Primary:** Evaluate & Govern  
**Supporting:** Build the Harness, Orchestrate Workflows

## The WidgetWare increment

Create the Book 1 release candidate: an evaluated application deployed to Cloud Run or an appropriate managed agent runtime, with basic observability and a repeatable demonstration.

## 10.1 Evaluation is broader than the final answer

An agent can produce a plausible final message while using the wrong source, calling an unnecessary tool, ignoring an exclusion, or skipping approval. Evaluate the entire behavior:

- inputs;
- context assembly;
- model outputs;
- tool calls;
- contracts;
- state transitions;
- evidence usage;
- approval compliance; and
- final artifacts.

## 10.2 Evaluation layers

### Unit tests

Deterministic functions, validators, state transitions, and tools.

### Contract tests

Schema validity, required fields, enumerations, and invariants.

### Scenario tests

End-to-end behavior for representative business situations.

### Semantic evaluation

Whether research, qualification, reasoning, and drafting are useful and correct.

### Safety and boundary tests

Prompt injection, prohibited action requests, missing approval, secret exposure, and unsupported claims.

### Operational tests

Latency, dependency failure, retry behavior, logging, and deployment health.

## 10.3 Build the golden dataset

A useful Book 1 dataset should contain at least:

- clearly qualified accounts;
- clearly unqualified accounts;
- ambiguous accounts;
- missing data;
- contradictory sources;
- stale evidence;
- malicious retrieved instructions;
- unsupported outreach claims;
- approval rejection; and
- dependency failure.

Each case should define expected stable properties rather than one perfect paragraph.

## 10.4 Evaluation criteria

Possible metrics include:

- qualification accuracy;
- evidence coverage;
- unsupported-claim rate;
- contract-validity rate;
- correct workflow-transition rate;
- prohibited-action rate;
- approval-compliance rate;
- tool-selection accuracy;
- average latency; and
- cost per completed case.

Book 1 can begin with simple thresholds and human-reviewed rubrics. Book 2 will extend this into continuous evaluation.

## 10.5 LLM-as-a-judge with caution

A model-based evaluator can score relevance, clarity, grounding, or tone. It should use a specific rubric and structured output. It should not be the only authority for high-risk requirements.

Use deterministic checks for:

- schema validity;
- citations present;
- allowed state transition;
- approval recorded;
- prohibited tool not called; and
- secrets absent.

Use human review to calibrate judge behavior.

## 10.6 Basic observability

Capture:

- request and workflow identifiers;
- agent and stage names;
- model configuration;
- tool calls and outcomes;
- state transitions;
- validation failures;
- latency;
- token or usage information where available; and
- final status.

Avoid logging secrets, unnecessary personal data, or full sensitive payloads.

Tracing should make it possible to answer: “Why did this case end in `BLOCKED`?”

## 10.7 Deployment choices

Book 1 may deploy to:

- **Cloud Run** for a transparent containerized application model; or
- a supported **managed agent runtime** for tighter lifecycle integration.

The exact choice depends on the learning objective and available environment. The book should teach the tradeoff rather than imply that one target is universally correct.

Deployment requires:

- authenticated configuration;
- environment-specific secrets;
- least-privilege service identity;
- health checks;
- logging;
- versioning; and
- rollback.

## 10.8 Release gates

A Book 1 release candidate should not deploy unless:

- all unit and contract tests pass;
- scenario pass rate meets the threshold;
- no test demonstrates autonomous external action;
- evidence coverage meets the threshold;
- known limitations are documented;
- deployment identity is least privilege; and
- rollback instructions exist.

## 10.9 The final demonstration

Demonstrate more than the happy path.

### Success case

A qualified account produces a research brief, supported qualification, reviewed outreach draft, and approval request.

### Insufficient-evidence case

The workflow stops and requests more research.

### Conflict case

Contradictory evidence remains visible and prevents an unjustified claim.

### Safety case

Retrieved prompt-injection text fails to override policy.

### Approval case

A rejected draft does not proceed.

A trustworthy demonstration shows how the system fails safely.

## Hands-on lab: Release Book 1

1. Build the golden dataset.
2. Run unit, contract, and scenario tests.
3. Add an evaluation command and report.
4. Add structured logs and trace identifiers.
5. Containerize or package the application.
6. Deploy to the selected runtime.
7. Run smoke tests.
8. Record model, code, configuration, Skill, and dataset versions.
9. Deliver the five-case final demonstration.

## Evaluation checklist

- Are quality claims backed by a dataset?
- Are workflow trajectories evaluated, not only final prose?
- Are deterministic requirements checked deterministically?
- Can failures be traced to a stage?
- Are secrets and sensitive payloads excluded from logs?
- Is the deployment reproducible and reversible?
- Does the demonstration include safe failure?

## Chapter checkpoint

The reader has completed an inspectable, evaluated, and deployable agent application — for one account at a time, run on request. WidgetWare's SDR workflow combines Gemini reasoning, ADK orchestration, Antigravity-assisted development, reusable Skills, controlled tools, evidence-backed research, structured contracts, multi-agent collaboration, and human approval. What it does not yet know how to do is work through a queue of accounts unattended, recover from an interruption, or stop on its own for a reason it can name.

## Bridge to Chapter 11

A single evaluated run is not yet a system you can point at a backlog of accounts and trust to work through them. Chapter 11 takes this exact workflow, unchanged, and wraps it in a bounded ADK loop — durable session state, budgets, checkpoints, and an explicit decision after every account — before Book 1 closes.

## Exercises

1. §10.1 lists nine things evaluation should cover beyond the final answer. Pick one of your own past "it works" moments with an agent system, in this course or elsewhere, and check how many of the nine you actually verified versus simply assumed because the final output looked right.
2. §10.3 requires ten kinds of cases in the golden dataset. Look at your own dataset from the Hands-on Lab and identify which of the ten is currently thinnest or missing, and describe a specific WidgetWare account profile that would fill that gap.
3. §10.5 says an LLM-as-a-judge should never be the sole authority for high-risk requirements, listing six things that must stay deterministic instead. Pick one of the six and describe, concretely, what a judge model getting it "almost right" would look like — a plausible-sounding but wrong judgment a rubric alone might miss.
4. §10.8 lists seven release-gate conditions. If you had to ship WidgetWare today under deadline pressure and could honestly satisfy only five of the seven, which two would you refuse to waive, and why those two specifically?
5. §10.9's five-case demonstration ends with "a trustworthy demonstration shows how the system fails safely." Pick the one of the five cases — success, insufficient-evidence, conflict, safety, approval — you'd most want a skeptical buyer to see first, and justify your choice in terms of what it proves that the success case alone cannot.
<!-- END 12_Chapter_10_Evaluate_Deploy_and_Demonstrate.md -->

<!-- BEGIN 13_Chapter_11_Loop_Engineering_with_ADK.md -->
# Chapter 11: Loop Engineering with ADK

## Chapter purpose

This chapter takes the evaluated, single-account WidgetWare workflow from Chapter 10 and turns it into a bounded, unattended process that works through a queue of accounts. The reader learns that this is a distinct engineering discipline — Loop Engineering — not a bigger version of orchestration, and builds it using ADK's own loop primitives rather than a bare `while True`.

## Learning objectives

By the end of this chapter, the reader should be able to:

- distinguish the inner agent loop ADK already runs from the outer engineered loop this chapter adds;
- explain why a working, evaluated workflow is still not a safe thing to run unattended;
- use ADK's `LoopAgent`, `max_iterations`, and `exit_loop` correctly and understand what they do and do not guarantee;
- design durable session state that survives a restart without reprocessing settled work;
- represent a loop's control decision as one of five explicit outcomes; and
- build a loop-ready checklist and apply it honestly to their own implementation.

## Seven-Step mapping

**Primary:** Engineer Loops  
**Supporting:** Build the Harness, Evaluate & Govern

## The WidgetWare increment

Wrap the Chapter 9–10 workflow, unchanged, in an ADK loop that reads a queue of candidate accounts, processes one at a time, checkpoints durable state after each meaningful stage, and stops with a named reason — instead of running once when a human asks.

## 11.1 What Chapter 10 didn't answer

Chapter 10 answers one question well: given one account, produce one evaluated, approved-or-rejected recommendation. A person can ask the WidgetWare agent to research Acme Manufacturing, and it will. But a system meant to run WidgetWare's actual sales-development motion has to answer questions the single-account workflow was never designed to answer:

- Where does the *next* account come from?
- Has this account already been processed in an earlier run?
- Should a failed research call be retried, and how many times before giving up?
- Should the system move on to another account, or stop entirely?
- When must a person intervene rather than the system deciding on its own?

None of these questions are about researching or qualifying one account better. They are questions about *control* — what happens around the workflow, not inside it — and Chapters 1 through 10 deliberately left them unanswered, because answering them requires the evaluated workflow Chapter 10 just finished building. The WidgetWare agent, as built through Chapter 10, is a genuine agent. It is not yet a loop.

## 11.2 The inner loop ADK already runs

Every ADK agent already executes an inner loop the moment it reasons: it observes the current input and state, decides whether to call a tool or respond, acts, and observes the result — repeating until it has enough to answer. This is real, it works, and Chapters 4 through 9 already built on top of it without needing to touch it directly.

```
Observe → Reason → Act → Observe
```

This chapter does not change that inner loop. It adds a different one, around it.

## 11.3 The outer loop this chapter adds

The outer loop is what decides, across many separate invocations of the workflow, what to work on next and whether to keep going:

```
Trigger
   ↓
Discover work
   ↓
Select the next eligible account
   ↓
Invoke the Chapter 9 workflow for that account
   ↓
Verify the outcome
   ↓
Persist state
   ↓
Continue, retry, stop, defer, or escalate
```

ADK gives this outer loop a real, named home: the `LoopAgent`. A `LoopAgent` executes its sub-agents — here, the whole Research → Qualify → Review → Draft → Approve workflow from Chapter 9 — repeatedly, passing the same `InvocationContext` through each iteration so that state changes persist across iterations. It is deterministic in *how* it iterates, even though the sub-agents it iterates over reason with a model.

## 11.4 A loop is not `max_iterations` alone

It is tempting, having just finished an evaluated workflow, to wrap it in the smallest amount of ADK configuration that makes it run more than once:

```python
loop = LoopAgent(
    name="widgetware_batch",
    sub_agents=[workflow],
    max_iterations=50,
)
```

This runs. It is not yet an engineered loop. `max_iterations` bounds how many times the loop *can* run — it says nothing about which account comes next, whether one was already settled, whether the workflow's output was actually good, or what a person should see when something goes wrong. Every item on this list is something a real deployment cannot survive without, and none of them come from `max_iterations` alone:

- No work-selection policy — nothing says which account is next, or whether one was already handled.
- No durable state — an `InMemorySessionService` restart loses everything, including which accounts were already processed.
- No verification — a malformed or incomplete result is treated the same as a good one.
- No per-account attempt limit — one bad account can consume retries meant for the whole run.
- No cost or time budget — nothing bounds what the run actually costs.
- No escalation path — nothing routes an account the loop cannot resolve to a person.
- No recovery strategy — a restart has no way to resume, only to start over.

The principle worth carrying forward: **repetition creates a loop. State, verification, budgets, and control make it an engineered loop.** The rest of this chapter is that difference, built with ADK's real primitives.

## 11.5 Durable state with SessionService

ADK's `Session` already separates a durable record — its `state`, a scratchpad of serializable values — from the transient event stream of one conversation. Which `SessionService` implementation backs that session decides whether the record survives a restart:

- `InMemorySessionService` — state lives in process memory. Fine for a single lab run; gone the moment the process exits.
- `DatabaseSessionService` (or `VertexAiSessionService` in a managed deployment) — state is written durably and reloaded on restart.

Book 1 uses the persistent option for the batch loop's own bookkeeping, and keeps that bookkeeping simple and inspectable — two small structures, not a schema the reader has to reverse-engineer:

Run-level state:

- `run_id`, `status`, `started_at`
- `accounts_processed`, `successes`, `failures`
- `current_account_id`
- `stop_reason`

Per-account state:

- `account_id`, `status`, `attempts`
- `research_status`, `qualification_result`
- `draft_status`, `approval_required`

"Which stage is this account in" should never be a sentence buried in a model's response — it is one value from a small, explicit set, computable directly from session state, the same deterministic-versus-probabilistic boundary Chapter 1.4 already drew. A model may recommend a transition. Code decides whether it is allowed.

## 11.6 Explicit states and transitions

```
RECEIVED
  ↓
RESEARCHING
  ↓
RESEARCH_COMPLETE
  ↓
QUALIFYING
  ↓
REVIEW_REQUIRED
  ↓
DRAFT_READY
  ↓
AWAITING_APPROVAL
  ├── APPROVED
  ├── REJECTED
  └── BLOCKED
```

This is the same state machine Chapter 9.3 already built for one account. The loop does not replace it — it adds two states that only make sense once accounts are processed unattended, in a batch, rather than one at a time on request:

- `RETRY_PENDING` — a recoverable failure occurred and attempts remain.
- `NEEDS_HUMAN_REVIEW` — the loop is not authorized to resolve this account on its own.

An account that has failed twice and has one attempt left is in a different, nameable condition from one that has failed permanently. The session state should say which, not leave it implied by the absence of a result.

## 11.7 Verification before advancing

Every stage the loop advances past should be checked deterministically before the loop trusts it — the same principle Chapter 6 applied to the workflow's own output contract, now applied to the loop's own control flow:

- the workflow's output validates against its contract (Chapter 6);
- decisive claims carry evidence references (Chapter 8);
- this account has not already reached a settled status in an earlier run;
- the draft contains no claim the Evidence Reviewer did not approve (Chapter 9.5); and
- no external send action has occurred — Book 1 still contains no send tool.

A model-based judge that scores whether the *reasoning* was good is a real extension of this idea, but it belongs to Book 2's continuous-evaluation chapter. Book 1's loop verifies shape and policy compliance deterministically, for the same reason Chapter 10.5 kept schema checks and semantic evaluation in separate layers.

## 11.8 Budgets and the five-way decision

State every limit before the loop starts running, not after it has already spent the budget:

- maximum accounts per run;
- maximum attempts per account;
- maximum wall-clock runtime;
- maximum tool calls or estimated token cost; and
- maximum consecutive failures.

Any one of these being reached is a legitimate reason to stop, alongside simply running out of eligible accounts. After each account, the loop makes exactly one explicit decision — never an implicit fallthrough:

- **CONTINUE** — the account settled (approved, rejected, or cleanly disqualified); move to the next eligible account.
- **RETRY** — a recoverable failure occurred and attempts remain; requeue the account.
- **STOP** — a budget was reached, or no eligible accounts remain; end the run cleanly.
- **DEFER** — the account cannot proceed right now (a dependency is unavailable) but has not failed; leave it for the next run.
- **ESCALATE** — the account needs a decision the loop is not authorized to make; route it to `NEEDS_HUMAN_REVIEW` rather than retrying or discarding it.

ADK's own `exit_loop` tool and `EventActions.escalate` give the loop a real mechanism for ending the loop early — a sub-agent can signal "stop iterating" without the `LoopAgent` itself needing to inspect every field of every result to figure that out. What ADK's primitive does not do on its own is distinguish *why* the loop is stopping: that interpretation is WidgetWare's own code. The same `escalate` signal, paired with the account's session state, is what the loop's control-flow code reads to decide whether this is a clean STOP (budget reached, queue empty) or an ESCALATE (route to `NEEDS_HUMAN_REVIEW`) — the primitive hands back control; WidgetWare's decision logic assigns the reason.

## 11.9 Checkpoints and resume

A durable session is only useful if the loop actually writes to it at meaningful moments and actually reads it back on restart. Checkpoint after each of: an account being selected, research completing and passing verification, qualification completing, a draft being created, and the run's overall counters being updated. A process restarted against a `DatabaseSessionService`-backed session should read the last checkpoint and resume from there — it should not re-research a company whose profile is already saved, and it must not re-send anything, though Book 1 makes that guarantee structurally by never building a send tool in the first place rather than by trusting the loop to remember not to call one.

## 11.10 Human control does not change inside a loop

Every autonomy level from Chapter 1.3 still applies once work happens inside a loop instead of one account at a time on request. The loop does not get to renegotiate WidgetWare's approval requirements just because a person is not watching it run:

| Action | Authority |
|---|---|
| Research an account | automatic |
| Summarize evidence | automatic |
| Recommend a qualification status | automatic |
| Draft outreach | automatic |
| Send outreach | human approval required |
| Modify a CRM record | human approval required |
| Delete a business record | prohibited |

Everything above the line can run across as many accounts as the budget allows, unattended. Everything below it stops that account's progress at `AWAITING_APPROVAL` until a person acts — exactly what Chapter 9.6 already required for one account, now holding for every account the loop touches.

## 11.11 The loop-ready checklist

Before this loop is trusted to run unattended, it should answer yes to each of the following:

- Is there a defined goal for what the loop is trying to accomplish?
- Is there a clear source of work, and a policy for selecting from it?
- Is state durable — does it survive a restart?
- Are the states an account can be in explicit, not implied by prose?
- Does the loop checkpoint after meaningful stages, not only at the end?
- Is every stage verified deterministically before the loop trusts it?
- Is there an attempt limit per account?
- Are there time, cost, and tool-call budgets?
- Are there explicit stop conditions, checked every iteration?
- Is there a path to escalate to a person, distinct from simply failing?
- Does the run produce a report a person can audit after the fact?
- Is there a way for an operator to stop the loop from outside it?

A system that cannot answer yes to all twelve is not yet an engineered loop, whatever else it does well.

## Hands-on lab: Build the batch loop

Implement:

- `src/widgetware_sdr/loop/account_queue.py` — work discovery and the work-selection policy: the next account whose status is `RECEIVED` or `RETRY_PENDING`, never one already settled;
- `src/widgetware_sdr/loop/budget.py` — the budget dataclass and a stop-condition check run once per iteration, before any account is selected;
- `src/widgetware_sdr/loop/decision.py` — a function returning exactly one of `CONTINUE` / `RETRY` / `STOP` / `DEFER` / `ESCALATE`, given an account's state and the current budget check;
- `src/widgetware_sdr/loop/run_report.py` — a report every run produces, always including its `stop_reason` and per-status totals;
- a `LoopAgent` wired to the Chapter 9 workflow, backed by a persistent `SessionService`; and
- a small seed queue of at least four accounts, at least one deliberately outside WidgetWare's ICP.

Add scenario tests for: a fresh account gets selected and a settled one doesn't; a recoverable failure retries up to the configured limit and no further; a restarted run resumes from saved session state instead of reprocessing; the loop stops at both the account limit and a budget limit; and every run's report names a stop reason.

## Evaluation checklist

- Does the loop select a new account and skip a settled one correctly?
- Does session state survive a simulated restart?
- Is every stage verified before the loop advances past it?
- Does a recoverable failure retry only up to its configured limit?
- Does the loop stop at every budget it declares, not only the account limit?
- Does every run produce a report naming its stop reason?
- Does anything in the loop send an external message automatically? (It must not.)

## Chapter checkpoint

WidgetWare can now work through a queue of accounts unattended, within limits it states in advance, and it stops for a reason it can name. Nothing about the single-account workflow from Chapters 4 through 10 changed — this chapter added everything *around* it.

## Bridge to the Book 1 conclusion

The conclusion consolidates what this system can now do across all eleven chapters, and identifies what must change when one bounded, looping application becomes an enterprise agent platform.

## Exercises

1. Using §11.4's list of things `max_iterations` alone doesn't give you, pick a repeating process you already run today — a script, a cron job, a manual routine — and score it against the same list. How many of the seven are actually present?
2. Using §11.8's five-way decision (CONTINUE, RETRY, STOP, DEFER, ESCALATE), write out, in plain language, what should happen to a WidgetWare account whose research completes successfully but whose qualification cannot be computed because the ICP configuration is missing a required field. Which decision applies, and why not one of the other four?
3. Run the batch loop from the Hands-on Lab to completion, then interrupt it mid-run on a fresh copy and restart it. Confirm from the session state itself, not from re-reading the code, exactly which accounts were re-processed and which were correctly skipped.
4. Using §11.10's authority table, audit your own batch loop's code: is there a single line that makes "send outreach" structurally impossible without an approved state, the same way Chapter 9 required for one account — or does the loop's own code introduce a new path around it?
5. Using §11.11's twelve-item loop-ready checklist, audit your own Hands-on Lab implementation honestly. If you find one item it does not fully satisfy, what would closing that gap require?
6. §11.2 and §11.3 distinguish the inner agent loop ADK already runs from the outer loop this chapter adds. Before Book 2 Chapter 5 introduces planning, predict whether a planning agent will need a third loop layered on top of these two, or will reuse one of these two loops for a different purpose. Check your prediction once you reach that chapter.
<!-- END 13_Chapter_11_Loop_Engineering_with_ADK.md -->

<!-- BEGIN 14_Book_1_Conclusion.md -->
# Book 1 Conclusion: An Agent Is a System

The WidgetWare SDR application began with a deliberately modest question: can an agent help research and qualify a prospective customer while remaining inspectable and under human control?

The answer is yes—but not because the model was given one extraordinary prompt.

The system became useful through layers:

- Gemini supplied interpretation, synthesis, and drafting.
- Context architecture supplied WidgetWare’s business knowledge and task-specific evidence.
- ADK supplied the agent application model, sessions, tools, workflows, and evaluation structure.
- Antigravity supplied the development harness for specification-driven, agent-assisted engineering.
- Skills captured reusable business procedures.
- Structured contracts converted probabilistic outputs into deterministic interfaces.
- Tools supplied controlled access to current data.
- MCP provided a standardized path to external capabilities.
- Multi-agent workflows separated responsibilities.
- Human approval retained control over external action.
- Evaluations supplied evidence that the system behaved as intended.
- An ADK `LoopAgent`, backed by durable session state, turned one evaluated workflow into a bounded process that works through many accounts and stops for a reason it can name.

This is the central lesson of Book 1:

> Agent Engineering is the discipline of placing model intelligence inside an engineered system of context, capabilities, structure, evidence, and boundaries.

## What the system can now do

The Book 1 system can:

1. Accept a target account.
2. Retrieve controlled internal information.
3. Research approved external evidence.
4. Preserve provenance.
5. Compare the account with WidgetWare’s ideal-customer profile.
6. Represent uncertainty and missing information.
7. Review the evidence supporting a recommendation.
8. Draft outreach from approved facts.
9. Stop for human approval.
10. Produce logs, tests, and evaluation results.
11. Work through a queue of accounts unattended, within stated budgets, and stop with a named reason.

## What the system still cannot do

It does not yet provide:

- durable memory across users and long time periods;
- enterprise-scale document ingestion and retrieval;
- adaptive planning over complex goals;
- loops that revise their own strategy, run across distributed workers, or recover from more than the failure modes this book anticipated;
- collaboration with independently deployed agents;
- centralized agent identity and registration;
- enterprise gateway enforcement;
- network-level containment;
- production-grade semantic safety controls;
- model routing and cost optimization; or
- continuous evaluation from live telemetry.

These are not omissions caused by an incomplete foundation. They are the next architectural layer.

## Five engineering habits to retain

### 1. Define the boundary before the behavior

A system should state what it may and may not do before implementation begins.

### 2. Prefer contracts over interpretation

Whenever software consumes an agent result, use typed structures and deterministic validation.

### 3. Preserve evidence

A conclusion is only as inspectable as the path from claim to source.

### 4. Use autonomy selectively

The ability to act does not justify permission to act. External actions require policy, identity, auditability, and often human approval.

### 5. Evaluate trajectories, not demonstrations

A polished result can conceal unsafe or inefficient behavior. Test the route the system took, not only the final words.

## The transition from application to platform

Book 1 built one bounded application. Enterprise adoption raises broader questions:

- How do hundreds of users receive isolated memory?
- How is enterprise knowledge indexed and permissioned?
- How do agents plan and recover over long-running tasks?
- How can independently deployed agents discover and trust each other?
- Which identity does an agent use when accessing data?
- Where are agents registered and governed?
- How are prompts and responses screened?
- How do teams observe latency, quality, cost, and failures across the ecosystem?

Those questions define Book 2.
<!-- END 14_Book_1_Conclusion.md -->

<!-- BEGIN 15_Introduction_to_Book_2.md -->
# Introduction to Book 2: From Agent Application to Enterprise Agent Platform

*This chapter previews Book 2. The full manuscript — ten chapters plus its own introduction and conclusion — lives in [`../book-2-Advanced-Architectures/`](../book-2-Advanced-Architectures/00_README.md).*

Book 1 ended with a complete WidgetWare SDR application. It can research an account, preserve evidence, qualify the opportunity, draft an outreach message, and request human approval — for one account, or for a bounded queue of accounts inside an ADK `LoopAgent` that stops for a reason it can name. It is inspectable, evaluated, and deployable.

That success creates a new class of problems.

A single application can keep its knowledge in a small set of files, run a short workflow, and rely on a compact team of agents. An enterprise platform must support many users, many agents, large knowledge collections, persistent state, distributed execution, strict identity boundaries, cost controls, continuous evaluation, and centralized governance.

Book 2 begins at that transition.

# Agent Engineering with Gemini, ADK & Antigravity
## Book 2: Advanced Architectures
### Build Stateful, Adaptive, Collaborative, and Governed Agent Systems on Google Cloud

## The Book 2 objective

Book 2 transforms WidgetWare SDR from a bounded application into an enterprise agent platform. The system will learn to remember, retrieve, plan, iterate, collaborate, secure, observe, and improve.

The progression is organized around ten architectural questions.

## Chapter 1 — From Agent Application to Agent Platform

How should the system be divided into control, runtime, knowledge, integration, and governance planes? The chapter reviews the Book 1 architecture and creates an enterprise target state.

## Chapter 2 — Sessions, State, and Long-Term Memory

How can the system remember useful information across interactions without leaking data between users or preserving information indefinitely? The chapter introduces identity-scoped sessions, memory extraction, retention, conflict, and deletion.

## Chapter 3 — Enterprise Knowledge and RAG

How can agents access large, governed collections of enterprise information? The chapter covers ingestion, chunking, embeddings, retrieval, reranking, citations, access control, and retrieval evaluation using appropriate Google Cloud services.

## Chapter 4 — Context Engineering at Scale

How should the system select, compress, cache, and refresh context under token, latency, and cost constraints? The chapter develops a context-management layer rather than allowing prompts to grow without control.

## Chapter 5 — Goals, Planning, and Controlled Loops

Book 1's Chapter 11 built one bounded loop: a fixed workflow, a fixed queue, an ADK `LoopAgent`, and five explicit decisions. This chapter asks what changes when the loop must decompose a goal it wasn't handed pre-solved, adapt its own plan, and still not run indefinitely. It introduces plan contracts, budgets, stopping conditions, checkpointing, non-progress detection, and human interruption — deepening Engineer Loops, not replacing what Book 1 already proved.

## Chapter 6 — Distributed Agent Collaboration

How do independently deployed agents discover capabilities and exchange work? The chapter introduces Agent-to-Agent collaboration, Agent Cards, remote tasks, cross-language systems, and the distinction between A2A and MCP.

## Chapter 7 — Agent Identity and Secure Tool Access

Which identity does an agent use, and which data is it permitted to access? The chapter separates user, application, and agent identity and applies IAM, service accounts, secrets, delegated authorization, and least privilege.

## Chapter 8 — Agent Governance and Containment

How are agents registered, routed, inspected, and constrained across an organization? The chapter introduces Agent Registry, Agent Gateway, VPC Service Controls, Model Armor, semantic policies, and data boundaries.

## Chapter 9 — AgentOps: Observability, Cost, and Quality

How do operators understand what a multi-agent system is doing? The chapter uses logs, traces, metrics, topology, token accounting, context caching, and tiered model routing to manage latency and cost.

## Chapter 10 — Continuous Evaluation and Enterprise Capstone

How does the platform detect regressions and improve safely? The chapter introduces production evaluation, golden datasets, trajectory scoring, LLM-as-a-judge, human calibration, online monitors, release gates, and an enterprise maturity assessment.

## The expanded Seven Steps

The seven-step framework — the same one used throughout this series, regardless of vendor — remains unchanged. Each step deepens into an enterprise capability:

1. **Frame the Use Case** now spans many use cases at once, arbitrated by a control plane rather than one team's charter.
2. **Build Context** becomes a governed knowledge and memory architecture, with retrieval replacing hand-assembled context packages.
3. **Design Agent Capabilities** becomes reusable organizational assets — Skills and tools shared across teams, not owned by one application.
4. **Build the Harness** extends from local Antigravity development to managed lifecycle and runtime — model routing, identity, and secure tool access.
5. **Orchestrate Workflows** extends across independently deployed agents that must discover and trust each other, not just coordinate within one process.
6. **Engineer Loops** extends from Book 1's one bounded, fixed-plan loop into loops that decompose their own goals, run distributed, and recover from more than the failures a single team anticipated.
7. **Evaluate & Govern** becomes continuous — production evaluation, online monitors, and organization-wide governance, not a release gate checked once before deployment.

## The principle that carries forward

Book 2 adds scale and sophistication, but it does not abandon the Book 1 discipline.

The platform must remain inspectable. Memory must remain scoped. Retrieval must preserve evidence. Plans must remain bounded. Collaboration must use explicit contracts. Tools must remain least privilege. Governance must exist outside model persuasion. Evaluation must remain tied to business outcomes.

The objective is not maximal autonomy.

The objective is an enterprise system in which intelligent behavior can expand without control becoming weaker.
<!-- END 15_Introduction_to_Book_2.md -->

