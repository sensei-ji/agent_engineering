<!-- BEGIN 00_README.md -->
# Agent Engineering with Gemini, ADK & Antigravity

## Book 2: Advanced Architectures
### Build Stateful, Adaptive, Collaborative, and Governed Agent Systems on Google Cloud

This directory contains the manuscript blueprint for Book 2. Each major part of the book is maintained as a separate Markdown file, in the same pattern as Book 1, so chapters can be written, reviewed, taught, and released independently.

## Reading order

1. `01_Introduction.md`
2. `02_Chapter_01_From_Agent_Application_to_Agent_Platform.md`
3. `03_Chapter_02_Sessions_State_and_Long_Term_Memory.md`
4. `04_Chapter_03_Enterprise_Knowledge_and_RAG.md`
5. `05_Chapter_04_Context_Engineering_at_Scale.md`
6. `06_Chapter_05_Goals_Planning_and_Controlled_Loops.md`
7. `07_Chapter_06_Distributed_Agent_Collaboration.md`
8. `08_Chapter_07_Agent_Identity_and_Secure_Tool_Access.md`
9. `09_Chapter_08_Agent_Governance_and_Containment.md`
10. `10_Chapter_09_AgentOps_Observability_Cost_and_Quality.md`
11. `11_Chapter_10_Continuous_Evaluation_and_Enterprise_Capstone.md`
12. `12_Book_2_Conclusion.md`

## Prerequisite

Book 2 assumes the completed Book 1 system: a bounded WidgetWare SDR application built with Gemini, ADK, and Antigravity, wrapped in one engineered loop (Book 1, Chapter 11), evaluated, and deployed. Every chapter here extends that system in place. Nothing in Book 2 asks the reader to start over.

## The continuous lab

Book 2 continues the same reference implementation: **WidgetWare SDR Lab**. Book 1 proved the system could research, qualify, draft, and stop for approval — for one account, and for a bounded batch of accounts run on request. Book 2 asks what changes when the same system must serve many users, remember across long time periods, draw on enterprise-scale knowledge, plan over ambiguous goals, collaborate with independently deployed agents, and prove — continuously, not once at release — that it still behaves inside its boundaries.

## The Seven Steps to Agent Engineering

The same seven steps used throughout Book 1 and every edition of this series. Book 2 does not add an eighth step or invent a parallel framework — it deepens the same seven into enterprise capabilities:

1. **Frame the Use Case** — now framed for a platform serving many teams and use cases, not one bounded application.
2. **Build Context** — becomes a governed knowledge and memory architecture: long-term memory, enterprise retrieval, and context management under real token and cost constraints.
3. **Design Agent Capabilities** — extends to capabilities the system does not own outright: other agents, discovered and used through a standard protocol.
4. **Build the Harness** — extends from local Antigravity development to a managed runtime with real identity and secure tool access.
5. **Orchestrate Workflows** — extends across independently deployed agents that must discover and trust each other, not just coordinate within one process.
6. **Engineer Loops** — extends from Book 1's one bounded, fixed-plan loop into loops that decompose their own goals and still do not run indefinitely.
7. **Evaluate & Govern** — becomes continuous: production evaluation, observability, cost management, and organization-wide governance, not a release gate checked once.

## A note on Google Cloud product names

Book 2 names specific Google Cloud and Vertex AI products and features throughout — Memory Bank, RAG Engine, Agent Registry, Agent Gateway, Model Armor, Agent Identity, and others. Product names, exact capabilities, and GA/Preview status on Google Cloud change faster than a book's release cycle. Treat every named product as this series treats a specific ADK class or method: correct in spirit and current as of this edition's writing, but worth confirming against Google's own current documentation before it anchors a production decision.

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

The same principle from Book 1 still governs every design decision in this book:

> Is this behavior better expressed as model reasoning or deterministic software?

Scale does not change that question. It raises the cost of answering it wrong.
<!-- END 00_README.md -->

<!-- BEGIN 01_Introduction.md -->
# Introduction: From Agent Application to Enterprise Agent Platform

## Why this book exists

Book 1 ended with a complete, if deliberately small, system. The WidgetWare SDR application can research an account, preserve evidence, qualify the opportunity, draft an outreach message, and request human approval — for one account, or for a bounded queue of accounts inside an ADK `LoopAgent` that stops for a reason it can name. It is inspectable, evaluated, and deployable.

That success creates a new class of problems, none of which are solved by writing more of the same kind of code.

A single bounded application can keep its knowledge in a handful of YAML files, run a short workflow, and rely on a small, fixed team of agents. An enterprise platform must support many users without their information leaking into one another's sessions, draw on knowledge collections too large to fit in any prompt, plan over goals that were not handed to it pre-decomposed, collaborate with agents it did not build and does not control, prove which identity is acting on whose behalf, and demonstrate — continuously, in production, not once at a release gate — that it still behaves inside its boundaries.

Book 2 begins at that transition.

## The reference system: WidgetWare SDR, at scale

WidgetWare is still the same fictional company. Its SDR problem is still the same problem. What changes is scope: instead of one bounded application a single developer can run locally, WidgetWare now needs a platform that many sales teams, across many regions, can rely on — with memory that persists correctly across months, knowledge retrieval that spans an entire enterprise document collection, and agents that plan, collaborate, and operate largely unattended, while remaining exactly as accountable as the Book 1 system was.

Nothing about WidgetWare's business rules changes. The evidence policy, the ideal customer profile, the approval requirements, and the prohibition on autonomous external action all carry forward unmodified. What Book 2 adds is the infrastructure that makes those rules hold at a scale where a person can no longer read every output.

## How Book 2 progresses

Book 2 is organized around ten architectural questions, each one exposing a limitation of the Book 1 system that only becomes visible once the system has to operate beyond a single developer's laptop.

- Chapter 1 asks how the system should be divided into planes — control, runtime, knowledge, integration, governance — before any of the following chapters build inside one of them.
- Chapter 2 asks how the system remembers a user across sessions without remembering them forever, or remembering the wrong user.
- Chapter 3 asks how agents draw on enterprise knowledge too large for any context window.
- Chapter 4 asks how context itself is managed once memory, retrieval, and history all compete for the same limited space.
- Chapter 5 asks how an agent plans over a goal it was not handed pre-decomposed, without looping indefinitely.
- Chapter 6 asks how independently deployed agents discover and collaborate with each other.
- Chapter 7 asks which identity an agent uses, and which data it is actually permitted to touch.
- Chapter 8 asks how an organization registers, routes, and constrains agents it did not all build itself.
- Chapter 9 asks how operators observe a distributed agent system's latency, cost, and quality.
- Chapter 10 asks how the platform proves, continuously, that it is still behaving — and closes with an enterprise capstone.

Every chapter leaves the WidgetWare platform in a usable, testable state, the same discipline Book 1 established.

## What Book 2 deliberately does not do

Book 2 introduces enterprise thinking without attempting to solve every possible enterprise concern. It does not deeply implement:

- multi-region disaster recovery and active-active deployment topologies;
- a full organizational change-management or agent-lifecycle-approval process;
- fine-tuning or distilling custom models;
- multimodal or voice-based agent interfaces; or
- every Google Cloud governance product's complete configuration surface.

These either belong to a specialized, later part of this series, or are organization-specific enough that a general blueprint would mislead more than it would help.

## A principle for the entire series, restated

Book 1 asked one question repeatedly:

> Is this behavior better expressed as model reasoning or deterministic software?

Book 2 does not replace that question. It applies it at a scale where getting the answer wrong is far more expensive to discover after the fact. Memory that is model-decided rather than policy-bounded leaks across users. Retrieval that trusts a document's content as an instruction is prompt injection with better production values. A loop that plans its own steps without a budget is `while True` with a more impressive vocabulary. The engineering discipline does not change. What changes is how much damage the same mistake can now do, and how much further away from a human reviewer that mistake can occur before anyone notices.

That is the case for taking Book 2 exactly as seriously as Book 1 — not more autonomously, just at scale.
<!-- END 01_Introduction.md -->

<!-- BEGIN 02_Chapter_01_From_Agent_Application_to_Agent_Platform.md -->
# Chapter 1: From Agent Application to Agent Platform

## Chapter purpose

This chapter reviews what the Book 1 WidgetWare system actually is — one bounded application, run by one developer, against one small dataset — and establishes the architectural planes Book 2 builds inside for the rest of the book. The reader learns to see "add memory," "add retrieval," "add collaboration" not as a list of features, but as additions to specific, separated planes with different failure modes and different owners.

## Learning objectives

By the end of this chapter, the reader should be able to:

- explain why "it works on my laptop" and "it works as a platform" are different engineering claims;
- separate a system into control, runtime, knowledge, integration, and governance planes;
- identify which Book 1 components belong to which plane;
- state, precisely, what changes about WidgetWare's business rules at platform scale (nothing) versus what changes about its infrastructure (nearly everything); and
- write an enterprise target-state document the rest of Book 2 will build toward.

## Seven-Step mapping

**Primary:** Frame the Use Case  
**Supporting:** Build the Harness

## The WidgetWare increment

Produce an enterprise target-state document: the five architectural planes, what currently occupies each one from Book 1, and what Book 2 will add to each.

## 1.1 What Book 1 actually proved

It is worth being precise about this before adding anything. The Book 1 system proved that a bounded WidgetWare workflow, run by one developer against a small seed dataset, can research, qualify, draft, and stop for approval — reliably, evaluated, and deployed to one runtime. It did not prove that the same system tolerates a hundred concurrent users, a knowledge base too large to fit in context, or an agent built by a different team calling into it.

Confusing these two claims is a common and expensive mistake. A system that is correct at one scale is not automatically correct at another scale — new failure modes appear that were structurally impossible in the smaller system, not because the code got worse, but because concurrency, scale, and multi-tenancy create problems a single-user, single-session system never had to solve.

## 1.2 Five architectural planes

Separate the platform into planes with distinct responsibilities and distinct owners:

### Control plane

Decides what work happens and in what order: workflow definitions, the `LoopAgent` from Book 1, Chapter 11, planning logic, and the policies that route work to agents.

### Runtime plane

Executes agents: ADK's Runner, sessions, the compute the agents actually run on, and the deployment target — Cloud Run, or a managed agent runtime.

### Knowledge plane

Everything an agent reasons over that is not the immediate task: long-term memory, retrieved enterprise documents, and the business configuration Book 1 kept in `config/`.

### Integration plane

Everything that connects the system to other systems: tools, MCP servers, and other agents reached through A2A.

### Governance plane

Identity, permissions, registration, policy enforcement, observability, and evaluation — the plane responsible for proving the other four are behaving.

## 1.3 Mapping Book 1 onto the planes

Book 1 already has real components in every plane — just not enterprise-scale ones:

| Plane | Book 1 component | Book 2 extension |
|---|---|---|
| Control | Chapter 9 workflow, Chapter 11 `LoopAgent` | Chapter 5: goal decomposition, adaptive planning |
| Runtime | ADK sessions, local or Cloud Run deployment | Chapter 7: identity-aware managed runtime |
| Knowledge | `config/` YAML files, one evidence ledger per run | Chapters 2–4: memory, RAG, context management |
| Integration | Function tools, one MCP source | Chapter 6: A2A collaboration with other agents |
| Governance | `permissions.deny`, the approval gate, Chapter 10's evaluation | Chapters 8–10: registry, containment, AgentOps, continuous evaluation |

Nothing in this table is a rewrite. Every Book 2 chapter extends a plane that already exists; none of them start from nothing.

## 1.4 What does not change

WidgetWare's business rules are not infrastructure, and platform scale does not touch them:

- the evidence policy — fact, derived fact, inference, unknown, conflict;
- the ideal-customer-profile criteria;
- the prohibition on inventing account attributes;
- the requirement that external outreach and CRM writes stay human-approved; and
- the principle that a model's confidence score is not a calibrated probability.

A platform that quietly relaxes any of these under scale pressure — "we can't review every draft anymore, so let's auto-approve the high-confidence ones" — has not solved a scaling problem. It has abandoned the discipline Book 1 spent ten chapters establishing, exactly at the moment the consequences of abandoning it got larger.

## 1.5 New failure modes at platform scale

Scale does not just make existing problems bigger. It introduces problems that were structurally impossible in a single-user system:

- one user's session state leaking into another user's context;
- a retrieval result surfacing a document the requesting user was never authorized to see;
- two agents built by different teams disagreeing about which one owns a decision;
- a loop that plans its own next step consuming an unbounded budget because no one is watching it run; and
- a change that passed every Book 1-style test still causing a regression, because the production traffic pattern doesn't match any golden-dataset case.

Each of the next nine chapters exists because of one or more of these failure modes.

## Hands-on lab: Write the enterprise target-state document

Create `docs/enterprise-target-state.md` containing:

- the five planes, each with a one-paragraph description;
- every Book 1 component, mapped to its plane;
- for each plane, the specific Book 2 chapter that will extend it and what "done" will look like; and
- an explicit statement of which WidgetWare business rules must not change, addressed directly to whoever eventually maintains this system after this book.

## Evaluation checklist

- Does every Book 1 component have an assigned plane?
- Is at least one new, scale-specific failure mode identified per plane?
- Does the document distinguish "business rules that don't change" from "infrastructure that does"?
- Could a new team member read this document and understand what each subsequent chapter is for?

## Chapter checkpoint

The repository now has an explicit architectural map. Nothing has been built yet — this chapter is entirely Step 1, Frame the Use Case, applied one level up from where Chapter 1 of Book 1 applied it.

## Bridge to Chapter 2

The knowledge plane is the most immediately visible gap: WidgetWare cannot yet remember a user from one session to the next, or tell two different users apart. Chapter 2 fixes that first, because every later chapter — retrieval, planning, collaboration — assumes the system already knows whose context it is operating in.

## Exercises

1. Using §1.2's five planes, take a system you actually maintain and sort its components into the same five categories. Which plane, if any, turns out to have no clear owner at all?
2. §1.1 distinguishes "correct at one scale" from "correct at another scale." Describe one feature of your own that was proven correct in a small test but that you have never actually verified under concurrent, multi-tenant load. What is the smallest test that would tell you the truth?
3. §1.4 lists five WidgetWare business rules that must not change at platform scale. Pick one and describe a realistic scale-pressure scenario — a deadline, a cost target, an incident — under which a team might be tempted to quietly relax it, and what the honest alternative response should be instead.
4. §1.5 lists five new failure modes that are structurally impossible in a single-user system. Pick the one you find least intuitive, and explain in your own words why a single-user, Book 1-style system genuinely could not have this problem, no matter how buggy its code was.
5. Using §1.3's plane-to-chapter mapping table, before reading the rest of Book 2, predict which chapter you expect to be hardest to get right for a system you've actually worked on, and why. Revisit this prediction once you have read all ten chapters.
<!-- END 02_Chapter_01_From_Agent_Application_to_Agent_Platform.md -->

<!-- BEGIN 03_Chapter_02_Sessions_State_and_Long_Term_Memory.md -->
# Chapter 2: Sessions, State, and Long-Term Memory

## Chapter purpose

This chapter gives WidgetWare real memory: the ability to recognize a returning user, recall relevant prior interactions, and do so without leaking one user's information into another user's session or retaining information indefinitely. The reader learns that memory is not a longer conversation history — it is a designed, scoped, and governed system in its own right.

## Learning objectives

By the end of this chapter, the reader should be able to:

- distinguish a session's state from an agent's long-term memory;
- explain how ADK's `SessionService` and Agent Platform Memory Bank relate, and where the boundary between them sits;
- design what gets extracted into long-term memory, and what should never be extracted;
- scope memory per user so it cannot cross a tenant boundary;
- apply a retention and deletion policy; and
- test that a stale or contradicted memory does not silently override current evidence.

## Seven-Step mapping

**Primary:** Build Context  
**Supporting:** Build the Harness, Engineer Loops

## The WidgetWare increment

Give the WidgetWare agent identity-scoped session persistence and long-term memory: it should recognize a returning SDR user, recall which accounts they have already worked, and never surface one user's account notes to another user.

## 2.1 Session state versus long-term memory

Book 1 already used ADK's `Session` — the container for one conversation's event history and its `state`, a scratchpad of serializable values. Chapter 11's loop used a persistent `SessionService` so that batch progress survived a restart. That is session-scoped: it belongs to one run, for one purpose, and it is not designed to answer "what do we already know about this user, across every session they've ever had."

Long-term memory is a different, complementary system. ADK integrates with **Agent Platform Memory Bank** for persistent, identity-scoped memory: an agent equipped with the `PreloadMemoryTool` and deployed to **Agent Runtime** uses `VertexAiMemoryBankService` by default, and can generate memories from selected session events and retrieve relevant memories across sessions, scoped by user. The distinction matters operationally, not just conceptually — session state disappears (or persists) with the session's own service configuration; memory persists deliberately, across sessions, because the application chose, at a specific point, to submit that session for extraction.

## 2.2 What belongs in memory, and what does not

Not every fact in a session deserves to become a memory. A useful rule: memory should hold information that changes how a *future* interaction should be handled, not a transcript of what happened in this one.

Worth extracting:

- "This user prefers a one-paragraph summary before the full research brief."
- "This user has already worked Acme Manufacturing twice this quarter; do not reintroduce it as new."
- "This user's territory is North American manufacturing accounts."

Not worth extracting, and actively risky to extract:

- the full text of a researched account brief (that belongs in the knowledge plane, Chapter 3, retrievable on demand — duplicating it into memory creates two copies that can drift apart);
- anything containing another user's data, even in passing;
- a one-off correction that doesn't generalize ("skip this specific account" is a task instruction, not a durable preference); and
- unverified inferences promoted to memory as if they were settled facts — memory should carry the same fact/inference/hypothesis discipline Chapter 1 of Book 1 established for everything else.

## 2.3 Writing and searching memory

The write path is deliberate, not automatic on every turn: at a meaningful point — typically the end of a session — the application decides that session is worth submitting, and calls the memory service's add-to-memory operation with its contents. What happens next is a division of labor, not a single decision: the application controls *which* sessions get submitted at all, and the memory service controls *what gets extracted* from within a submitted session — it is not the model, mid-conversation, unilaterally deciding what to remember. The read path is a search, scoped to the current user, run before or during a new session so the agent's instructions can be grounded in what is already known about this specific person, not the whole memory store.

```python
# Illustrative shape, not a complete implementation.
await memory_service.async_add_session_to_memory(session)

results = await memory_service.async_search_memory(
    user_id=current_user_id,
    query="WidgetWare account preferences and history",
)
```

The `user_id` scope in the search call is not a convenience parameter. It is the boundary that prevents one user's memory from ever entering another user's context — the enterprise-scale form of the least-privilege principle Book 1, Chapter 7 applied to tools.

## 2.4 Memory can be wrong, stale, or contradicted

A memory written last quarter — "this account's champion is the VP of Operations" — can become false without anyone updating it. Design for this from the start, not as a later patch:

- attach a timestamp to every memory the same way Book 1's evidence items carry `retrieved_at`;
- treat memory as a *hint to verify*, not a fact to restate as current without checking; and
- when current evidence (Chapter 3's retrieval, or fresh research) contradicts a memory, surface the conflict the same way Book 1's evidence ledger surfaced conflicting sources — never silently prefer the newer one without saying so.

A system that treats every old memory as still true is not remembering. It is accumulating stale certainty.

## 2.5 Retention and deletion

Memory that is useful indefinitely is also memory that accumulates risk indefinitely. WidgetWare's memory policy should state, explicitly:

- how long a memory is retained before it expires or requires reconfirmation;
- what happens when a user's access is revoked — memory scoped to that user must become unreachable, not merely unreferenced;
- how a user or an administrator can request that specific memories be deleted; and
- that memory extraction never captures secrets, credentials, or another user's data, even if the session transcript briefly contained them.

## 2.6 Testing a memory system

Memory is a probabilistic extraction process feeding a system that should behave deterministically about scope. Test both halves:

- **extraction quality** — does a representative session produce the memories a person would expect, and not extract noise;
- **scope enforcement** — a search for User A's memory must never return anything extracted from User B's session, tested with an actual cross-user query, not merely asserted; and
- **staleness handling** — a memory contradicted by fresh evidence should be flagged, not silently trusted.

## Hands-on lab: Add memory to the WidgetWare agent

Implement:

- `src/widgetware_sdr/memory/service_config.py` — configure a persistent `SessionService` and the Agent Platform Memory Bank-backed memory service;
- `src/widgetware_sdr/memory/extraction_policy.py` — the rules for what is and is not written to memory;
- an update to the qualification agent's instructions so it consults memory, scoped to the current user, before starting research; and
- tests for: cross-user isolation, a memory correctly surfacing a user's prior work on an account, and a stale memory being flagged rather than trusted outright.

## Evaluation checklist

- Is session state kept separate from long-term memory, both conceptually and in code?
- Does every memory write pass through an explicit extraction policy, not an unfiltered dump of the session?
- Does a cross-user memory search test actually attempt the leak and confirm it fails?
- Is there a retention and deletion policy, not just a storage mechanism?
- Does the system distinguish a memory from a currently verified fact?

## Chapter checkpoint

WidgetWare can now recognize a returning user and recall relevant, scoped history without treating old information as automatically current. The knowledge plane still lacks the other half of memory: access to enterprise information the system was never told directly.

## Bridge to Chapter 3

Memory answers "what do we already know about this user." It does not answer "what does the enterprise already know about this account." Chapter 3 connects WidgetWare to retrieval over a real knowledge collection.

## Exercises

1. §2.2 gives examples of what's worth extracting to memory and what's actively risky. Take a real conversation or session log from a system you use and sort five statements from it into "worth remembering," "not worth remembering," and "risky to remember."
2. §2.3 splits responsibility: the application decides which sessions get submitted; the memory service decides what gets extracted from within them. Describe a scenario where a bug in the *application's* submission decision, not the memory service's extraction, would be the actual root cause of a leaked or wrong memory.
3. §2.4 says memory is "a hint to verify, not a fact to restate as current." Using a specific stale-memory example from your own life or work — a colleague's role changed and your notes still say the old one — describe what the correct agent behavior should be the moment fresh evidence contradicts it.
4. §2.5 requires that memory scoped to a revoked user become unreachable, not merely unreferenced. What is the difference between those two, concretely, in terms of what a determined but unauthorized query could still retrieve?
5. §2.6 requires testing scope enforcement with an actual cross-user query, not an assertion that scoping exists. Write, in plain language, the exact query and the exact wrong result that test needs to attempt and fail to get, in order to actually prove anything.
<!-- END 03_Chapter_02_Sessions_State_and_Long_Term_Memory.md -->

<!-- BEGIN 04_Chapter_03_Enterprise_Knowledge_and_RAG.md -->
# Chapter 3: Enterprise Knowledge and RAG

## Chapter purpose

This chapter connects WidgetWare to a real, governed collection of enterprise knowledge — product documentation, prior account histories, competitive positioning — using Vertex AI RAG Engine. The reader learns that retrieval-augmented generation is an engineering architecture with real failure modes, not a single API call that makes a model "know more."

## Learning objectives

By the end of this chapter, the reader should be able to:

- explain the ingestion-to-retrieval pipeline: parsing, chunking, embedding, indexing, and retrieval;
- choose chunking parameters deliberately, understanding the precision-versus-context tradeoff;
- apply access control so retrieval never returns a document a user isn't authorized to see;
- attach citations from retrieved passages to specific claims, the same way Book 1 attached evidence to claims;
- evaluate retrieval quality separately from generation quality; and
- keep retrieved content subordinate to system policy, the same discipline Book 1 applied to any external content.

## Seven-Step mapping

**Primary:** Build Context  
**Supporting:** Design Agent Capabilities, Evaluate & Govern

## The WidgetWare increment

Ingest WidgetWare's product documentation, approved case studies, and prior account research into Vertex AI RAG Engine, and connect the Research Agent to it so qualification and drafting can cite enterprise sources, not only what a single research call happened to find that day.

## 3.1 Retrieval is a pipeline, not a call

"Add RAG" understates what actually has to work correctly:

1. **Ingestion** — documents enter the system from wherever they actually live.
2. **Parsing** — Vertex AI RAG Engine's layout parser turns unstructured documents (PDFs, slides, long-form text) into structured representations before anything else happens to them.
3. **Chunking** — the parsed content is split into retrievable units.
4. **Embedding** — each chunk becomes a vector, via the Vertex AI text embeddings API.
5. **Indexing** — chunk embeddings are indexed for retrieval, using Vector Search.
6. **Retrieval** — a query embedding is compared against the index to return the most relevant chunks.
7. **Grounded generation** — the model reasons over the retrieved chunks, with their source attached.

Each stage can fail independently, and a failure at stage 3 looks identical, from the outside, to a failure at stage 6 — both produce "the agent didn't know something it should have." Diagnosing which stage actually failed requires being able to inspect each one separately, which is the entire justification for treating this as a pipeline rather than a black box.

## 3.2 Chunking is a real design decision

Vertex AI RAG Engine's chunking transformation is controlled by two parameters: `CHUNK_SIZE`, the number of tokens per chunk, and `CHUNK_OVERLAP`, the token overlap between adjacent chunks. The tradeoff is concrete, not aesthetic: a smaller chunk size produces more precise embeddings, at the cost of losing surrounding context; a larger chunk size preserves more context, at the cost of embeddings that represent several ideas at once and retrieve less precisely for a narrow question.

For WidgetWare's document mix — short product fact sheets, longer case studies, dense compliance documents — a single chunk-size setting will not be right for every document type. Chunking policy belongs in configuration, not hardcoded once and forgotten, the same way Book 1 kept business rules out of code.

## 3.3 Access control is not optional

A retrieval system that returns any relevant chunk regardless of who asked has built a very effective way to leak information across account teams, regions, or customer confidentiality boundaries. Every retrieval call must be scoped to what the requesting user or agent is actually authorized to see — filtered at the index or corpus level, not by asking the model to please not mention what it just retrieved.

This is not a hypothetical risk unique to WidgetWare. It is the single most common way naively-built RAG systems fail in production: retrieval quality looks excellent in testing (because test users had broad access) and then leaks a document in front of a user who should never have seen it, the first time someone with narrower access asks a similar question.

## 3.4 Claims still need citations

Chapter 1 of Book 1 required every material claim to carry evidence. Retrieval does not relax that requirement — it gives the system a new, richer evidence source, with the same obligations:

```text
EvidenceItem
- evidence_id
- source_type: enterprise_document
- source_uri
- chunk_id
- retrieved_at
- claim
- excerpt
- reliability
```

A qualification result that says "WidgetWare has delivered similar transformations before" without a `chunk_id` pointing at the specific case study is exactly the floating, unsourced claim Book 1's evidence policy was built to catch. Retrieval makes it easier to produce a confident-sounding sentence with no traceable source; the discipline to prevent that has to get stronger, not weaker, as the knowledge base gets larger.

## 3.5 Retrieved content is still untrusted data

Chapter 8 of Book 1 already established that retrieved web content is data, not instruction. The same is true of enterprise documents, and it is easy to forget precisely because they feel more trustworthy — an internal case study or a colleague's notes are not adversarial the way a scraped webpage might be, but they can still be stale, contradictory, or (in a large enough organization) contain content someone pasted in that was never meant to be an instruction to a future agent. Isolate retrieved text from system instructions the same way, regardless of source.

## 3.6 Evaluating retrieval separately from generation

A disappointing final answer can come from bad retrieval, good retrieval used badly, or a genuinely hard question. Evaluate retrieval on its own terms before evaluating the full pipeline:

- **retrieval precision** — of the chunks returned, how many were actually relevant to the query;
- **retrieval recall** — of the chunks that should have been returned, how many actually were;
- **citation accuracy** — does every claim's cited chunk actually support the claim, checked by re-reading the chunk, not by trusting the model's own citation; and
- **freshness** — is the retrieved information current enough to support the claim being made, the same freshness discipline Book 1's evidence policy already required.

## Hands-on lab: Connect WidgetWare to enterprise retrieval

Implement:

- ingest a small representative document set (product sheets, two anonymized case studies, one compliance document) into Vertex AI RAG Engine;
- configure chunking parameters deliberately, with a written rationale for the choice;
- `src/widgetware_sdr/retrieval/access_filter.py` — enforce that retrieval results are scoped to the requesting user's authorized corpus;
- update the Research Agent to retrieve and cite enterprise sources alongside external evidence; and
- a retrieval evaluation set with known-relevant and known-irrelevant chunks per test query.

## Evaluation checklist

- Can retrieval precision and recall be measured independently of final-answer quality?
- Does every retrieved claim carry a checkable citation, down to the chunk?
- Does an access-control test attempt an actual unauthorized query and confirm it is blocked, not merely assert a policy exists?
- Is retrieved content still treated as untrusted data, isolated from system instructions?
- Is chunking configuration documented with a rationale, not left at a default no one chose deliberately?

## Chapter checkpoint

WidgetWare can now ground its reasoning in enterprise knowledge, with citations, access control, and the same evidence discipline Book 1 established for external research. The knowledge plane still has one more problem: even with memory and retrieval both working correctly, everything they supply competes for the same limited context window.

## Bridge to Chapter 4

Chapter 4 manages that competition directly — selecting, compressing, and refreshing context under real token, latency, and cost constraints, rather than letting every available source get appended until something breaks.

## Exercises

1. §3.1 breaks retrieval into seven pipeline stages. Pick a "the agent didn't know something it should have" failure you've seen, real or hypothetical, and, using the seven stages, list which two or three are the most likely culprits — and what you'd check first to tell them apart.
2. §3.2 frames chunk size as a genuine tradeoff, not an aesthetic choice. For one of WidgetWare's three document types — fact sheets, case studies, compliance documents — argue for a chunk-size choice and name the specific kind of query it would handle worse than the alternative choice would.
3. §3.3 says access-control failures often look fine in testing because test users have broad access. Describe how you would deliberately construct a test user with narrower access, specifically to surface this failure mode before a real customer does.
4. §3.4 requires a `chunk_id`, not just a source name, on every retrieved claim. What does having a chunk_id let you do, when auditing a disputed claim, that a source name alone would not?
5. §3.6 lists four retrieval-specific metrics. Pick the one you think WidgetWare's own team would be most tempted to skip under time pressure, and explain what specifically goes wrong downstream if it's skipped.
<!-- END 04_Chapter_03_Enterprise_Knowledge_and_RAG.md -->

<!-- BEGIN 05_Chapter_04_Context_Engineering_at_Scale.md -->
# Chapter 4: Context Engineering at Scale

## Chapter purpose

Chapters 2 and 3 gave WidgetWare two new sources of information: long-term memory and enterprise retrieval. Both now compete with session history, business configuration, and the immediate task for the same limited context window. This chapter builds the layer that decides, deliberately, what actually goes into a given call — and uses Gemini's context caching to keep the stable parts of that context cheap and fast.

## Learning objectives

By the end of this chapter, the reader should be able to:

- explain why more available context is not the same as better context;
- design a context-assembly pipeline that selects, ranks, and excludes rather than concatenating everything available;
- distinguish content worth caching from content that must be assembled fresh every call;
- configure Gemini's implicit and explicit caching correctly for WidgetWare's actual traffic pattern; and
- measure context cost and quality together, not cost alone.

## Seven-Step mapping

**Primary:** Build Context  
**Supporting:** Build the Harness, Evaluate & Govern

## The WidgetWare increment

Build a context-assembly layer that selects from memory, retrieval, and session state under an explicit token budget, and configure caching so WidgetWare's stable instructions and business configuration are not re-processed, and re-billed, on every call.

## 4.1 More context is not automatically better context

Chapter 3 of Book 1 already established this for a single account's evidence pool. At platform scale, the failure mode gets worse, not different in kind: a context assembled from unfiltered memory, unranked retrieval results, and full session history does not make Gemini reason better — it makes the genuinely relevant three facts compete for attention with forty tangentially related ones, and it costs more, and it is slower, on every single call.

The discipline is the same one Chapter 3.6 of Book 1 named: context engineering includes exclusion. At scale, exclusion has to be systematic rather than manual, because no person is reviewing what goes into every call.

## 4.2 A context budget, stated explicitly

Give every call an explicit token budget, allocated across sources rather than left to whatever accumulates:

```text
ContextBudget
- system_instructions: fixed, small
- business_configuration: fixed, small
- long_term_memory: top-k relevant, ranked
- retrieved_evidence: top-k relevant, ranked
- session_history: most recent N turns, or a summary beyond that
- task_context: the current request
```

When the budget is exceeded, the assembly layer — not the model — decides what to drop, using the same ranking that decided what to include. A model asked to "just use what's relevant" from an oversized context has no reliable way to know which excluded fact might have mattered; the exclusion decision belongs upstream, where it can be tested.

## 4.3 Selecting, not just fitting

Fitting inside a budget and selecting well are different problems. A context-assembly pipeline should:

1. retrieve candidates from each source (memory, retrieval, session);
2. score each candidate for relevance to the current task, not just recency or availability;
3. apply exclusion rules — WidgetWare's evidence policy, access control from Chapter 3, and any content flagged as stale; and
4. assemble the final context in a stable, predictable order, so caching (4.4) actually helps.

## 4.4 Caching the stable part of context

Gemini supports two kinds of context caching, and WidgetWare's context-assembly design should be built with both in mind from the start, not retrofitted later:

- **Implicit caching** is automatic for current Gemini models — cost savings apply whenever a request happens to share a cached prefix with a recent one, with nothing to configure.
- **Explicit caching** lets the application declare specific content — WidgetWare's system instructions, the ICP configuration, the evidence policy — as a cache with a controlled time-to-live, then reference it by name in every subsequent call instead of resending it.

The design implication is direct: put the stable, rarely-changing content — instructions, business configuration — at a consistent position, and keep it byte-identical across calls, so it can actually be cached. Content that changes every call — the current task, freshly retrieved evidence — belongs after the cached prefix, not interleaved with it. A context-assembly pipeline that reorders or slightly rephrases stable content on every call defeats caching for no benefit.

## 4.5 Summarization is compression, and compression loses information

When session history exceeds its budget, summarizing older turns is reasonable — but a summary is a compression, and compression can silently discard exactly the qualification that mattered. Chapter 6 of Book 1 already flagged this risk for the account-research workflow itself; it applies identically here. A summarization step should be tested the same way any other lossy transformation is tested: given a known input, does the summary retain the decisions, evidence, and unresolved questions, or only the narrative shape of the conversation?

## 4.6 Measuring context cost and quality together

Optimizing only for token cost produces a context-assembly layer that aggressively excludes anything not proven necessary — including information that was, in fact, necessary, just not yet shown to fail without it. Track both dimensions on the same dashboard:

- tokens per call, and estimated cost per call;
- cache hit rate, for both implicit and explicit caching;
- latency, broken out by context-assembly time versus model inference time; and
- the same quality metrics Chapter 10 of Book 1 already established (qualification accuracy, unsupported-claim rate), run against the *compressed* context, not only the full one.

A context-assembly change that lowers cost and also lowers qualification accuracy has not optimized the system. It has moved the cost from the cloud bill to the business outcome.

## Hands-on lab: Build the context-assembly layer

Implement:

- `src/widgetware_sdr/context/budget.py` — the explicit per-source token budget;
- `src/widgetware_sdr/context/assembler.py` — retrieval, scoring, exclusion, and stable ordering across memory, RAG results, and session history;
- explicit caching for system instructions and business configuration, with a defined TTL and a test confirming the cache is actually hit on a repeated call; and
- a benchmark comparing token cost, latency, and qualification accuracy before and after the assembly layer, against the same golden dataset Chapter 10 of Book 1 already built.

## Evaluation checklist

- Does every call's context stay within its declared budget?
- Is exclusion systematic — a testable function — rather than left to the model?
- Is stable content ordered consistently so caching actually applies?
- Does the benchmark measure quality alongside cost, not cost alone?
- Does a summarization test confirm decisions and evidence survive compression, not only prose fluency?

## Chapter checkpoint

WidgetWare now assembles context deliberately, under budget, with caching reducing the cost of what stays stable. The knowledge plane — memory, retrieval, and context management — is complete for this book. The control plane is next.

## Bridge to Chapter 5

Everything so far still assumes a workflow whose steps were decided in advance. Chapter 5 asks what changes when WidgetWare has to decompose a goal itself and adapt its own plan — without becoming the unbounded loop Book 1, Chapter 11 specifically taught the reader to avoid.

## Exercises

1. §4.2's `ContextBudget` allocates tokens per source rather than letting them accumulate. If you had to cut 20% from WidgetWare's current context budget, which source would you cut from first, and which would you protect at all costs? Justify both choices.
2. §4.4 requires stable content to be byte-identical and consistently positioned across calls for caching to work. Describe one realistic way a well-intentioned code change — a timestamp in a header, a reordered dictionary — could silently defeat caching without anyone noticing a "bug," only a cost increase.
3. §4.5 says a summarization step should be tested for whether it retains decisions and unresolved questions, not just narrative shape. Take a real multi-turn conversation you've had and summarize it in two sentences, then check: does your summary still contain the one detail that mattered most for what happens next?
4. §4.6 warns that optimizing only for token cost can silently degrade quality. Describe a context-exclusion rule that would look good on a cost dashboard while quietly removing something that turns out to matter — and what metric, tracked alongside cost, would have caught it.
5. Using §4.1's callback to Book 1, Chapter 3.6, explain in your own words why "context engineering includes exclusion" is the same discipline at both a single-account scale and a platform scale — and what specifically has to become systematic, rather than manual, to make that true at scale.
<!-- END 05_Chapter_04_Context_Engineering_at_Scale.md -->

<!-- BEGIN 06_Chapter_05_Goals_Planning_and_Controlled_Loops.md -->
# Chapter 5: Goals, Planning, and Controlled Loops

## Chapter purpose

Book 1's loop repeated a fixed plan — research, qualify, review, draft, approve — across a queue of accounts. The plan itself was decided in advance; only the account changed. This chapter asks what changes when WidgetWare is handed a goal that was not pre-decomposed, and has to plan its own steps toward it, while remaining exactly as bounded as the Book 1 loop. This is a deepening of Engineer Loops, not a different discipline.

## Learning objectives

By the end of this chapter, the reader should be able to:

- distinguish a fixed workflow from a goal an agent must decompose itself;
- use ADK's planner classes correctly, and know what each one actually guarantees;
- design a plan contract that a person or a downstream system can inspect before execution;
- detect non-progress and stop a plan that is looping without converging; and
- apply the same budget-and-decision discipline from Book 1, Chapter 11 to a plan whose steps are not known in advance.

## Seven-Step mapping

**Primary:** Engineer Loops  
**Supporting:** Frame the Use Case, Evaluate & Govern

## The WidgetWare increment

Give WidgetWare a **Territory Planning Agent**: handed a goal like "identify and prioritize the top prospects in the Northeast manufacturing territory this quarter," it decomposes that goal into a bounded plan, executes it using the Book 1 workflow as a sub-step, and stops — either because it finished, or because it hit a limit it can name.

## 5.1 A fixed workflow versus a goal

Book 1's Chapter 9 workflow, and the Chapter 11 loop built on top of it, both assume the sequence of steps is already known: research, then qualify, then review, then draft, then approve. A goal is different in kind — "prioritize the best prospects in this territory" does not arrive with its steps attached. The system has to decide how many accounts to consider, in what order, using what criteria, and when it has done enough to answer confidently.

This is a harder problem than looping over a known queue, and it deserves the same suspicion Chapter 1 of Book 1 applied to every claim of required agent behavior: does this genuinely require adaptive planning, or is it a fixed workflow wearing an open-ended goal as a disguise? Many apparently open-ended requests decompose into the same five or six steps every time — in which case, a workflow with a parameter is the right answer, not a planner.

## 5.2 ADK's planners

ADK provides planning as a first-class capability, not something the reader has to build from scratch:

- **`BuiltInPlanner`** uses Gemini's native extended-thinking capability — the model reasons internally before responding, without an explicit, inspectable plan artifact.
- **`PlanReActPlanner`** implements Plan → Reason → Act → Observe → Replan explicitly: the agent is constrained to produce a plan before it takes any action, then reasons, acts, observes the result, and replans if needed.

For WidgetWare's Territory Planning Agent, `PlanReActPlanner` is the right choice, not because it's more sophisticated, but because it produces an inspectable plan — the same reason Book 1 preferred explicit workflow state over an agent's own summary of what it had done. A `BuiltInPlanner`'s internal reasoning is not something a person can review before the agent acts on it.

## 5.3 A plan contract, not free-form steps

Whatever produces the plan, the plan itself should be a typed artifact, not a paragraph:

```text
TerritoryPlan
- goal
- candidate_accounts[]
- prioritization_criteria
- steps[]
  - step_id
  - action: research | qualify | compare | rank
  - target_account_id
  - depends_on[]
- budget
- stopping_conditions[]
```

A person reviewing this plan before execution can see exactly what the agent intends to do and why, and can reject or amend it — the same "review the plan before permitting implementation" discipline Antigravity itself already teaches in Book 1, Chapter 2, now applied to an agent's own plan instead of a coding agent's proposed changes.

## 5.4 Budgets apply to planning too

Book 1, Chapter 11 stated every loop's limits before it started running. A planning agent needs the same discipline, applied to the plan itself:

- maximum accounts the plan may consider;
- maximum re-planning iterations before the agent must stop and report, rather than keep revising;
- maximum total tool calls or estimated cost for the entire goal, not just one account; and
- a maximum wall-clock time for the whole planning-and-execution cycle.

A planner with no budget is `while True` with better vocabulary — the same principle Book 1, Chapter 11 stated about bare `max_iterations`, now applying to a system that also decides its own steps.

## 5.5 Detecting non-progress

A fixed loop can only fail to converge by exhausting its queue or its budget. A planning loop has a third failure mode a fixed loop cannot have: replanning repeatedly without making real progress — proposing a new plan that looks different but doesn't actually move the goal forward. Detect this explicitly:

- track a concrete progress signal (accounts fully evaluated, not accounts merely considered);
- if replanning occurs without the progress signal advancing across two consecutive cycles, stop and escalate rather than replan a third time; and
- record what each replan actually changed, so a person reviewing a stalled run can see whether the agent was refining its approach or spinning.

## 5.6 The same five decisions, applied to a plan

Book 1, Chapter 11's five-way decision — CONTINUE, RETRY, STOP, DEFER, ESCALATE — still applies, now evaluated after each planning cycle rather than after each account:

- **CONTINUE** — the plan is making measured progress; proceed to the next step.
- **RETRY** — one step failed recoverably; retry that step, not the whole plan.
- **STOP** — the goal is achieved, or a budget was reached.
- **DEFER** — a step depends on information not currently available; leave it and continue with independent steps.
- **ESCALATE** — non-progress was detected, or the plan proposes an action outside WidgetWare's authority table (Book 1, Chapter 11.10) — send to a person rather than replanning again.

## Hands-on lab: Build the Territory Planning Agent

Implement:

- `src/widgetware_sdr/planning/territory_agent.py` — an ADK agent configured with `PlanReActPlanner`;
- `src/widgetware_sdr/planning/plan_contract.py` — the typed plan artifact, validated before execution;
- `src/widgetware_sdr/planning/progress_tracker.py` — the non-progress detector;
- wiring so each plan step that reaches "qualify an account" invokes the unchanged Book 1 workflow; and
- scenario tests for: a goal that decomposes cleanly, a goal where two candidate accounts have no available evidence, and a deliberately unsolvable goal that should trigger non-progress detection and escalation rather than looping.

## Evaluation checklist

- Is every plan a typed, reviewable artifact before execution begins?
- Does the agent ever act without first producing a plan?
- Is there a real budget on replanning iterations, not just on total steps?
- Does the non-progress detector trigger on a genuinely stalled scenario, tested directly?
- Does the planner ever propose an action outside WidgetWare's authority table? (It must not, and a test should confirm it.)

## Chapter checkpoint

WidgetWare can now decompose an open-ended goal into a bounded, inspectable plan, execute it using the unchanged Book 1 workflow as a building block, and stop — for a reason it can name — whether it succeeds, runs out of budget, or detects it is not making progress.

## Bridge to Chapter 6

The Territory Planning Agent still does all of its own work. Chapter 6 asks what changes when part of a plan's work is better delegated to an agent WidgetWare's own team did not build — and how two independently deployed agents discover, trust, and collaborate with each other at all.

## Exercises

1. §5.1 asks whether an apparently open-ended request is genuinely open-ended or "a fixed workflow wearing an open-ended goal as a disguise." Take a request from your own domain that sounds like it needs a planning agent, and check: does it actually decompose into the same five or six steps every time?
2. §5.2 says `PlanReActPlanner` is preferred over `BuiltInPlanner` specifically because it produces an inspectable plan artifact, not because it's more sophisticated. Describe a task where you'd make the opposite choice, and be honest about what you'd be giving up by choosing inspectability.
3. §5.4 requires budgets on re-planning iterations, not just on the final execution. Using the `TerritoryPlan` contract from §5.3, describe what should happen when the planner has already re-planned twice and proposes a fourth, materially identical plan.
4. §5.5 distinguishes "refining an approach" from "spinning." Describe, concretely, what evidence in a replan log would convince you a plan is genuinely converging versus what evidence would convince you it isn't — using a real progress signal, not a vibe.
5. §5.6 applies the same five-way decision — CONTINUE, RETRY, STOP, DEFER, ESCALATE — to a plan instead of a single account. Write out which of the five applies when a planning agent's step depends on a remote agent (Chapter 6) that is currently unavailable, and why not one of the other four.
<!-- END 06_Chapter_05_Goals_Planning_and_Controlled_Loops.md -->

<!-- BEGIN 07_Chapter_06_Distributed_Agent_Collaboration.md -->
# Chapter 6: Distributed Agent Collaboration

## Chapter purpose

Every agent WidgetWare has used so far lives inside its own codebase, callable as a Python object. This chapter connects WidgetWare to agents it does not own — built by another team, another vendor, or another part of the organization — using the Agent2Agent (A2A) protocol. The reader learns to treat a remote agent as a capability with a contract, not a trusted extension of their own system.

## Learning objectives

By the end of this chapter, the reader should be able to:

- explain what A2A adds beyond MCP, and when each is the right integration mechanism;
- read and construct an Agent Card;
- design a task handoff to a remote agent with the same discipline Book 1 applied to handoffs between local subagents;
- decide when a capability should be delegated to a remote agent versus built in-house; and
- answer, honestly, whether a given multi-agent design is solving a real problem or just adding a diagram.

## Seven-Step mapping

**Primary:** Design Agent Capabilities  
**Supporting:** Orchestrate Workflows, Build the Harness

## The WidgetWare increment

Delegate one real capability — technographic enrichment (what technology stack a target account already runs) — to a remote, independently deployed agent discovered through its Agent Card, rather than building that capability into WidgetWare directly.

## 6.1 MCP versus A2A, precisely

Book 1, Chapter 8 already distinguished a function tool from an MCP integration: MCP standardizes how an agent calls a *tool* or a *data source*. A2A solves a different problem — how one *agent* discovers, addresses, and exchanges tasks with a genuinely separate agent, one that reasons on its own, may be built on a different framework entirely, and is not simply exposing a fixed set of callable operations.

The distinction matters for design, not just vocabulary. A weather API is a tool: call it, get data back, done. A partner organization's contract-analysis agent is a peer: hand it a task, it may ask clarifying questions, it decides how to approach the work, and it returns a result WidgetWare did not fully specify the shape of in advance. Reaching for A2A to call something that is really just a tool adds coordination overhead with no benefit; reaching for a function tool to integrate with something that genuinely reasons independently loses the task semantics A2A is built for.

## 6.2 Agent Cards

An Agent Card is the A2A equivalent of a Skill's concise discovery description in Book 1, Chapter 5.6 — the thing a caller inspects to decide whether this agent applies, before committing to a task with it. It is a structured document describing an agent's capabilities and how it can be reached, part of A2A's Layer 1 data model alongside `AgentSkill`, `Task`, and `Message`.

```text
AgentCard
- name
- description
- skills[]
  - id
  - description
  - input_modes
  - output_modes
- endpoint
- authentication_requirements
```

Reading a remote Agent Card is the same discipline as reading a Skill's discovery description in Book 1, Chapter 5.6: it is the only information available before the interaction starts, and a vague or overstated card is a live integration risk, not a minor documentation gap.

## 6.3 Sending a task, not a conversation

A2A defines three interchangeable protocol bindings for its Layer 2 operations — `SendMessage`, `ListTasks`, and related calls — over JSON-RPC 2.0, gRPC, or HTTP+JSON/REST; an Agent Card advertises which binding a given agent actually speaks. The example in this chapter uses JSON-RPC 2.0, but the binding is a transport choice — what matters for design is the task semantics underneath it, the same handoff discipline Book 1, Chapter 9.4 already established for local subagents: pass a compact, well-defined unit of work, not an open-ended conversation.

```text
TechnographicEnrichmentTask
- account_id
- company_name
- company_domain
- requested_facts[]: "primary_erp", "cloud_provider", "automation_platforms"
- evidence_requirements: "cite source and date for every fact returned"
```

WidgetWare states what it needs and what standard the answer must meet. The remote agent decides how to research it. What comes back should be evaluated exactly the way any other evidence source is evaluated — Chapter 1 of Book 1's fact/inference/hypothesis discipline does not relax because the source is another agent instead of a webpage.

## 6.4 A remote agent is not a trusted extension of your own

Everything Book 1, Chapter 8.6 said about retrieved content applies with more force to a remote agent's output: it is not your code, it does not share your evidence policy by default, and its result should be validated against WidgetWare's own contract before anything downstream consumes it. A remote agent claiming high confidence is not the same claim as a `support_type` your own evidence-policy enforcer has actually checked.

Treat every result from a remote agent as untrusted input to be validated, the same way a tool result or a retrieved document is validated — not as a peer's word taken on faith because it arrived through a more sophisticated protocol.

## 6.5 When multi-agent collaboration is the wrong answer

Book 1, Chapter 9.1 asked when a task justifies a new local subagent. The same skepticism applies here, with a sharper question, because remote collaboration adds real operational cost — network calls, authentication, a dependency on another team's or vendor's uptime:

> When is a multi-agent system genuinely better than one well-designed agent with good tools?

Technographic enrichment justifies delegation because a specialized vendor genuinely maintains better, fresher technology-stack data than WidgetWare could build cheaply itself — a real capability gap, not a diagram improvement. A capability WidgetWare could implement locally with one well-scoped tool should stay local. Distributed collaboration should solve a real problem: capability WidgetWare does not have, data WidgetWare does not maintain, or work that genuinely belongs to another system of record — not add architectural sophistication for its own sake.

## Hands-on lab: Delegate technographic enrichment

Implement:

- `src/widgetware_sdr/collaboration/agent_card_client.py` — discover and validate a remote agent's Agent Card before use;
- `src/widgetware_sdr/collaboration/enrichment_task.py` — construct and send a technographic-enrichment task;
- `src/widgetware_sdr/collaboration/result_validator.py` — validate the remote agent's response against WidgetWare's evidence contract before it enters the Account Brief;
- a mock remote agent for deterministic testing; and
- a decision record answering 6.5's question for this specific capability, in writing.

## Evaluation checklist

- Does the system validate an Agent Card's claims before trusting them?
- Is every task sent to the remote agent a bounded, typed handoff, not an open-ended conversation?
- Is the remote agent's result validated against WidgetWare's own evidence contract, not accepted on arrival?
- Is there a written justification for using distributed collaboration for this capability specifically, not a default assumption that multi-agent is more advanced?
- Does a test simulate the remote agent being unavailable, and confirm WidgetWare degrades gracefully rather than blocking indefinitely?

## Chapter checkpoint

WidgetWare can now delegate a real capability to an independently deployed agent, treat its output with the same scrutiny as any other evidence source, and justify the decision to collaborate rather than build. Every chapter so far has assumed WidgetWare's own team controls who can call what. Chapter 7 removes that assumption.

## Bridge to Chapter 7

Once WidgetWare calls agents it doesn't own, and once its own agents run unattended across many users, "which identity is acting" stops being obvious. Chapter 7 separates user, application, and agent identity, and applies least privilege to all three.

## Exercises

1. §6.1 distinguishes a tool — call it, get data, done — from a peer agent — hand it a task, it reasons on its own. Take an integration you've built or used and decide, honestly, which one it actually is, and whether it was built with the right protocol for what it actually is.
2. §6.2 compares an Agent Card's description to a Skill's discovery description (Book 1, Chapter 5.6). Write the Agent Card description you'd give WidgetWare's own qualification capability if a different team's agent needed to decide, from the card alone, whether to delegate a task to it.
3. §6.4 says a remote agent's high-confidence claim is "not the same claim as a `support_type` your own evidence-policy enforcer has actually checked." Describe what your validation code should actually do the moment a remote agent returns a claim with no citation at all.
4. §6.5 poses a sharper version of Book 1, Chapter 9.1's question, because remote collaboration adds real operational cost. Pick a capability you're tempted to delegate to a remote agent and argue against yourself: what would it cost to build locally instead, and is that cost actually higher than the coordination overhead of depending on someone else's uptime?
5. §6.3 notes that JSON-RPC, gRPC, and REST are all valid A2A bindings — a transport choice, not a design decision. What would actually change in your integration code if the remote enrichment agent switched bindings tomorrow, and what, if anything, should not have to change?
<!-- END 07_Chapter_06_Distributed_Agent_Collaboration.md -->

<!-- BEGIN 08_Chapter_07_Agent_Identity_and_Secure_Tool_Access.md -->
# Chapter 7: Agent Identity and Secure Tool Access

## Chapter purpose

Book 1's system ran as one developer, on one laptop, where "who is doing this" was never ambiguous. A platform serving many users, running agents that call other agents, breaks that assumption completely. This chapter separates the identities actually in play, and applies least privilege to each one rather than to "the agent" as an undifferentiated whole.

## Learning objectives

By the end of this chapter, the reader should be able to:

- distinguish user identity, application identity, and agent (workload) identity;
- explain what Google Cloud's Agent Identity adds beyond a general-purpose service account;
- explain why an agent acting "on behalf of" a user is not the same as the agent acting as itself;
- apply IAM roles and service accounts with least privilege to WidgetWare's own tools and data access;
- use Workload Identity Federation instead of long-lived credentials embedded anywhere in code or configuration; and
- audit which identity performed a specific consequential action, after the fact.

## Seven-Step mapping

**Primary:** Build the Harness  
**Supporting:** Design Agent Capabilities, Evaluate & Govern

## The WidgetWare increment

Give every WidgetWare component — the qualification agent, the research delegation from Chapter 6, the batch loop from Book 1, Chapter 11 — its own scoped identity, so that a permission audit can answer "what could this specific component do" without having to ask "what could the whole application do."

## 7.1 Three identities, not one

Book 1, Chapter 7.5 already applied least privilege to tools — each tool receiving only the permission it requires. At platform scale, that principle needs a third dimension it didn't need before — *whose* authority a given action is exercised under:

- **User identity** — the actual SDR whose request this is. Their access to accounts, territories, and CRM records is the outer bound of what any agent should be able to do on their behalf.
- **Application identity** — the WidgetWare platform itself, as a deployed service. It has its own service account, its own baseline permissions, independent of any specific user.
- **Agent (workload) identity** — a specific component — the Research Agent, the Territory Planning Agent, the batch loop — may warrant its own scoped identity, narrower than the application's overall identity, the same reasoning Book 1, Chapter 9 already applied when it gave the Research Agent and the Evidence Reviewer separate roles with separate responsibilities.

Conflating these is where identity design usually goes wrong: a system that runs every action under one broad application identity cannot distinguish "the platform did this" from "this specific user, through the platform, did this" — which matters enormously the first time an audit has to answer who actually approved an action.

## 7.2 Acting on behalf of, not acting as

When the qualification agent researches an account for a specific SDR, it should carry that user's identity through the request — visible in logs, enforced in access checks — rather than acting under one shared, undifferentiated application identity. This is what makes Chapter 2's memory-scoping and Chapter 3's retrieval-access-control actually enforceable rather than merely intended: a request that doesn't carry the user's identity has nothing for an access check to scope against.

Concretely, this means propagating user context through every layer — the workflow, the tool calls, the retrieval query — rather than authenticating once at the front door and then treating everything downstream as uniformly trusted.

## 7.3 Agent Identity: a named primitive, not just a service account

Google Cloud's **Agent Identity** is the platform's specific answer to the agent-workload dimension above — a distinct, cryptographically attested identity per agent, built on the SPIFFE standard, rather than a shared, general-purpose service account reused across every workload that happens to run under it. It matters for WidgetWare because it closes a gap a bare service account leaves open:

- it is tied to the agent's own lifecycle, not provisioned once and outliving the component it was meant for;
- it integrates with IAM, **Principal Access Boundary (PAB)**, and VPC Service Controls, so an agent's permissions can be bounded independently of the broader application identity it runs alongside; and
- when an agent acts on a user's behalf, the resulting log entry carries *both* identities — the agent's and the user's — rather than forcing an auditor to infer the user from application-level context that may not have been captured.

Treat Agent Identity as the concrete mechanism for the "agent (workload) identity" principle in 7.1, not a separate concept: where the platform supports it, prefer an Agent Identity over a general-purpose service account for any component whose actions need to be individually attributable.

## 7.4 Least privilege with IAM and service accounts

Apply the same least-privilege discipline Book 1, Chapter 7.5 stated for tools, using Google Cloud's identity primitives:

- give each component its own **service account** (or Agent Identity, where available), scoped to only the roles it needs — the batch loop's identity should not hold the same permissions as an interactive research session;
- grant **IAM roles** at the narrowest resource scope that works — a role granted at the project level when a dataset-level grant would do is a standing risk, not a convenience; and
- review granted roles periodically, the same discipline Book 1, Chapter 7.8 applied to testing a tool's permission failures — a permission granted once, and never revisited, tends to outlive the reason it was granted.

## 7.5 No long-lived credentials, anywhere

Book 1, Chapter 2.7 already established the pattern of keeping real secrets out of source and out of anything checked in. At platform scale, the stronger version of that rule is to avoid long-lived credentials entirely where possible. **Workload Identity Federation** lets a workload authenticate to Google Cloud using a short-lived, automatically rotated credential tied to its actual runtime identity, rather than a downloaded service-account key file that has to be protected, rotated manually, and can be exfiltrated. Any credential that has to be stored somewhere and remembered to be rotated is a standing liability; prefer federated, short-lived credentials wherever the runtime supports them.

## 7.6 Delegated authorization for the Chapter 6 case

When WidgetWare calls a remote agent through A2A, whose identity does that call carry? Not WidgetWare's application identity unconditionally — that would let any user's request exercise the platform's full authority against the remote agent. The call should carry a delegated, scoped credential: enough authority to make the specific request being made, tied back to the originating user where that matters, and nothing more. This is the same least-privilege principle from 7.3 and 7.4, applied across an organizational boundary instead of within one.

## 7.7 Auditing after the fact

Every consequential action — a qualification decision, an approval, a remote-agent delegation — should be traceable to a specific identity, not just "the system." A useful audit record answers, without ambiguity:

- which user's request originated this;
- which service account or Agent Identity actually executed it — captured automatically, per 7.3, when Agent Identity is in use;
- what data or capability it touched; and
- what decision was made, and by which authority (Book 1, Chapter 11.10's table — automatic, human-approved, or prohibited).

This is not a governance nicety layered on top. It is what makes Chapter 8's containment policies and Chapter 10's continuous evaluation possible at all — neither can function against actions that cannot be attributed to an identity.

## Hands-on lab: Separate and scope WidgetWare's identities

Implement:

- distinct service accounts for the interactive qualification path, the Chapter 5 planning agent, and the Chapter 11 batch loop, each with its own least-privilege IAM roles;
- user-identity propagation through the workflow, retrieval, and memory layers, so access checks have something real to scope against;
- Workload Identity Federation configuration for the platform's runtime, replacing any downloaded credential file; and
- an audit-log query that answers, for a specific qualification decision, exactly which user and which workload identity produced it.

## Evaluation checklist

- Can every consequential action be traced to a specific user identity and a specific workload identity?
- Does each component's service account hold only the roles it actually uses, verified rather than assumed?
- Is there a long-lived credential anywhere in the system that a short-lived, federated one could replace?
- Does a delegated call to a remote agent (Chapter 6) carry a scoped credential, not the platform's full authority?
- Would an external audit of IAM roles find any grant nobody can currently justify?

## Chapter checkpoint

WidgetWare's identities are now separated, scoped, and auditable. Individual components are secure. What is still missing is an organization-wide view: which agents exist at all, who registered them, and what happens when one of them attempts something outside its bounds.

## Bridge to Chapter 8

Chapter 8 adds that organization-wide view — registering agents so they can be discovered and governed centrally, and containing what a misbehaving or compromised one can actually do.

## Exercises

1. §7.1 separates user, application, and agent (workload) identity. Take an action your own system performs today and identify which of the three identities it currently runs under — and whether that's actually the right one, per §7.2's "acting on behalf of, not acting as" distinction.
2. §7.3 distinguishes Google Cloud's Agent Identity from a general-purpose service account specifically by its dual-identity audit logging. Describe an incident-investigation scenario where having both the agent's and the user's identity in the same log entry would have saved real time, versus having only one or the other.
3. §7.4 says a role granted at the project level "when a dataset-level grant would do is a standing risk, not a convenience." Audit one permission grant in a system you maintain and check: is it scoped as narrowly as it could be, or as narrowly as was fastest to set up?
4. §7.5 argues long-lived credentials are a standing liability even when they are never actually leaked. What is the difference in actual risk between a credential that was leaked and one that merely could have been, but wasn't rotated in two years?
5. §7.6 asks what identity a delegated call to a remote agent (Chapter 6) should carry. Using §7.1's three identities, write out specifically what should be in that delegated credential, and what should deliberately be left out.
<!-- END 08_Chapter_07_Agent_Identity_and_Secure_Tool_Access.md -->

<!-- BEGIN 09_Chapter_08_Agent_Governance_and_Containment.md -->
# Chapter 8: Agent Governance and Containment

## Chapter purpose

Chapter 7 secured WidgetWare's own identities. This chapter assumes WidgetWare is no longer the only agent system in the organization — other teams are building their own agents, some calling into WidgetWare, some being called by it — and builds the governance layer that keeps that ecosystem inspectable: a registry of what exists, a gateway that enforces policy on every call, and network-level containment as a backstop.

## Learning objectives

By the end of this chapter, the reader should be able to:

- explain what an Agent Registry adds beyond a team knowing its own agents exist;
- route agent-to-agent and agent-to-tool traffic through an Agent Gateway and explain what that buys over direct calls;
- apply Model Armor to defend against prompt injection and data leakage at the gateway, not only inside application code;
- use VPC Service Controls as a network-level containment boundary; and
- articulate the difference between an application-level guardrail and an organization-level one, and why WidgetWare needs both.

## Seven-Step mapping

**Primary:** Evaluate & Govern  
**Supporting:** Build the Harness, Orchestrate Workflows

## The WidgetWare increment

Register WidgetWare's agents in the organization's Agent Registry, route their traffic through an Agent Gateway with Model Armor protections enabled, and place the platform's data access inside a VPC Service Controls perimeter.

## 8.1 Why a registry, not just a team's own documentation

Book 1, Chapter 1's Working Vocabulary and every subagent definition file already document what WidgetWare's own agents do. That documentation does not help a different team evaluate whether it's safe to let their agent call into WidgetWare's, or whether WidgetWare should be allowed to call theirs. An **Agent Registry** solves that specific problem: a centralized, queryable catalog of an organization's own agents, Google's, and third-party agents and MCP servers, capturing version, framework, and capability metadata in one place a governance function can actually query.

Registering an agent is not paperwork for its own sake. It is what makes Chapter 6's "read the Agent Card before trusting it" discipline scale past two teams who happen to talk to each other — with a registry, discovery and vetting don't depend on knowing who to ask.

## 8.2 Routing through an Agent Gateway

Book 1's tools and Chapter 6's A2A calls have, so far, connected directly — WidgetWare's code calls the tool, or calls the remote agent's endpoint. An **Agent Gateway** sits between agents and the tools or other agents they call, enforcing consistent policy on every hop without every application having to reimplement that enforcement itself: authentication, authorization, rate limiting, and content protection applied at one chokepoint rather than scattered across every service that happens to make a call.

This is the organizational version of Book 1, Chapter 7.5's tool-permission boundary — instead of each subagent's own declared toolset being the only enforcement, the gateway enforces policy regardless of what any individual agent's code believes its own permissions are. A misconfigured or compromised agent cannot simply route around the gateway to reach something it shouldn't.

## 8.3 Model Armor at the gateway

Book 1, Chapter 8.6 defended against prompt injection inside the Research Agent's own code — isolating retrieved content, labeling its origin, refusing to execute instructions found in it. **Model Armor**, configured on the Agent Gateway, adds the same category of defense at the infrastructure layer: content sanitization and threat detection for prompt injection and sensitive-data leakage, applied to traffic passing through the gateway regardless of which application sent it.

The two layers are not redundant. Application-level defense (Book 1) is specific to WidgetWare's own context and can reason about WidgetWare's own business rules. Gateway-level defense (Model Armor) is generic, applies uniformly to every agent behind the gateway, and catches what an individual application might have implemented incorrectly or forgotten. Defense in depth means both layers exist, not that one replaces the other.

## 8.4 VPC Service Controls as a backstop

Identity and gateway policy answer "who is allowed to call what." **VPC Service Controls** answers a different question: even for an authorized call, can data cross a boundary it should never cross at all — WidgetWare's account evidence leaving the organization's network perimeter entirely, for instance, regardless of which identity requested it. A service perimeter is the containment layer that holds even if an identity or gateway policy is misconfigured — the same "defense in depth, not one control doing everything" principle as 8.3, moved to the network layer.

## 8.5 What governance changes about a WidgetWare release

Chapter 8 of Book 1 defined release gates for a single deployment. Governance adds requirements that exist above any single team's release process:

- the agent must be registered, with an accurate, current Agent Card, before it can be discovered by other teams;
- its traffic must route through the organization's Agent Gateway — no direct, ungated calls to production tools or other agents;
- Model Armor policies must be enabled on that traffic, not opted out of for convenience during development; and
- its data access must respect the organization's VPC Service Controls perimeter.

None of these replace Book 1's release gates. They sit above them, and a release that passes Book 1's gates but fails an organizational governance check is not ready to ship, regardless of how good its own tests look.

## 8.6 Governance is not a courtesy any single team can waive

The temptation, under deadline pressure, is to treat registry entries, gateway routing, and Model Armor as bureaucracy to route around "just for this one release." The reasoning that makes this dangerous is the same reasoning Book 1, Chapter 9.6 applied to a bare approval button: a control that can be quietly bypassed under pressure provides none of the protection it appears to promise. Governance exists specifically for the case where a team is confident nothing will go wrong — that is exactly the case it cannot be allowed to self-certify.

## Hands-on lab: Register and contain WidgetWare

Implement:

- an Agent Registry entry for each WidgetWare agent from Chapters 4 through 6 of Book 1 and Chapters 5 through 6 of Book 2, with accurate, current capability metadata;
- Agent Gateway routing for all tool calls and A2A traffic, replacing any direct connections;
- Model Armor policy configuration on that gateway traffic; and
- a VPC Service Controls perimeter around WidgetWare's data stores, with a test confirming a simulated exfiltration attempt is blocked.

## Evaluation checklist

- Is every WidgetWare agent discoverable in the registry, with metadata that is actually current?
- Does all inter-agent and agent-to-tool traffic route through the gateway, with no direct bypass path?
- Is Model Armor active on that traffic, not merely configured and disabled?
- Does a simulated data-exfiltration attempt actually get blocked by the service perimeter, tested directly rather than assumed?
- Could a different team discover, evaluate, and safely call into WidgetWare's agents using only what the registry exposes?

## Chapter checkpoint

WidgetWare is now a governed participant in the organization's agent ecosystem — discoverable, gated, and contained, with defense in depth rather than a single point of enforcement. The remaining gap is operational: once this system runs continuously, in production, who is watching it, and how do they know what it costs and how well it's actually performing?

## Bridge to Chapter 9

Chapter 9 builds that operational picture — logs, traces, metrics, and cost accounting across a distributed, multi-agent system, not just the deployment health checks Book 1, Chapter 10 already covered.

## Exercises

1. §8.1 says an Agent Registry solves a problem a team's own documentation cannot: helping a *different* team decide whether it's safe to call into your agent. Describe a real cross-team integration decision you've had to make with only informal documentation, and what specifically would have been faster or safer with a queryable registry entry instead.
2. §8.3 argues Model Armor and Book 1's application-level defenses are "not redundant" — one is specific, one is generic. Describe a prompt-injection attempt that application-level defense would catch but gateway-level defense would miss, and one that would be the reverse.
3. §8.4 distinguishes "who is allowed to call what" (identity, gateway) from "can data cross a boundary at all" (VPC Service Controls). Describe a scenario where an identity and gateway policy are both configured correctly, and the request is fully authorized, but VPC Service Controls is the only thing that should stop it.
4. §8.5 lists four governance requirements that sit above any single team's release gates. If your own team were under deadline pressure, which of the four would be most tempting to treat as "we'll register it properly next sprint" — and what §8.6 says about why that temptation is exactly the case governance can't self-certify.
5. Using §8.2's chokepoint argument, describe what a "misconfigured or compromised agent" routing around the gateway would actually look like in practice — what specific technical shortcut would it be taking, and what would have to be true of the network or IAM configuration for that shortcut to actually work?
<!-- END 09_Chapter_08_Agent_Governance_and_Containment.md -->

<!-- BEGIN 10_Chapter_09_AgentOps_Observability_Cost_and_Quality.md -->
# Chapter 9: AgentOps — Observability, Cost, and Quality

## Chapter purpose

Book 1, Chapter 10 gave WidgetWare basic logs and a deployment health check, sufficient for one bounded application. This chapter builds what operating a distributed, multi-agent, multi-user platform actually requires: distributed tracing across every agent and tool call, cost accounting that can be attributed to a specific user or workflow, and quality signals that operators — not just developers — can watch continuously.

## Learning objectives

By the end of this chapter, the reader should be able to:

- distinguish a log, a metric, and a trace, and know which question each one answers;
- trace one request across every agent, tool, and remote A2A call it touched;
- attribute token cost and latency to a specific user, workflow, and model tier;
- apply tiered model routing deliberately, not as an unexamined cost cut; and
- design dashboards an operator can actually use during an incident, not just a developer during debugging.

## Seven-Step mapping

**Primary:** Evaluate & Govern  
**Supporting:** Build the Harness, Engineer Loops

## The WidgetWare increment

Instrument the full WidgetWare platform — the Book 1 workflow, the Chapter 5 planning agent, the Chapter 6 remote delegation, and the batch loop — with distributed tracing, cost attribution, and operator-facing dashboards, so a person can answer "what is this system doing right now, and what is it costing" without reading source code.

## 9.1 Logs, metrics, and traces answer different questions

Book 1, Chapter 10.6 already listed what to capture: request identifiers, agent and stage names, tool calls, state transitions, latency. At platform scale, that list has to be organized into three distinct signal types, because they answer different operational questions:

- **Logs** answer "what happened, in detail, at this one point" — a specific tool call's input and result, a specific validation failure.
- **Metrics** answer "how is the system behaving in aggregate, over time" — request rate, error rate, p95 latency, cost per hour.
- **Traces** answer "what was the actual path this one request took, across every component it touched, and where did the time go."

A system with excellent logs and no traces can tell you a specific call failed, but not which upstream decision led to it. A system with excellent metrics and no traces can tell you latency degraded, but not which of twelve possible components caused it. WidgetWare needs all three, deliberately distinguished, using Cloud Logging, Cloud Monitoring, and Cloud Trace.

## 9.2 Tracing across a distributed request

A single WidgetWare qualification request, by this point in Book 2, may pass through: the context-assembly layer (Chapter 4), the qualification agent, a Chapter 6 A2A call to a remote enrichment agent, and the Chapter 8 gateway that call routed through. A trace ties every one of those spans together under one request identifier, so "why did this specific request take four seconds" has an answerable, inspectable path — not a guess.

```text
Trace: qualify-request-8f21
├── context_assembly        (120ms)
├── qualification_agent
│   ├── model_call            (900ms)
│   └── a2a_delegation: technographic_enrichment
│       ├── gateway_policy_check   (40ms)
│       └── remote_agent_call      (2100ms)   ← the actual bottleneck
└── evidence_review          (300ms)
```

Without the trace, "the remote agent call was the bottleneck" is a hypothesis. With it, it's a measurement.

## 9.3 Cost attribution, not just total spend

Chapter 4's context caching reduces cost, but a platform serving many users and workflows needs to know *whose* usage is driving spend, not only the total. Attribute token cost and tool-call cost to:

- the requesting user, so a small number of unusually expensive workflows are visible rather than averaged away;
- the workflow or agent (qualification, planning, remote delegation), so cost optimization efforts target the actual driver, not a guess; and
- the model tier used, so a routing decision's cost impact is measurable, not assumed.

## 9.4 Tiered model routing, examined

Book 1, Chapter 3.1 already said to centralize model selection and keep it configurable. At platform scale, that configuration point becomes a real routing decision: not every WidgetWare task needs the same model. A straightforward qualification against clear-cut criteria may be well served by a smaller, faster, cheaper model tier; the Chapter 5 planning agent's decomposition of an ambiguous, high-stakes goal may genuinely need a more capable one.

Route deliberately, with evidence, not by default:

- define which tasks are eligible for a lighter-weight tier, based on measured quality parity, not assumption;
- monitor the quality metrics from Book 1, Chapter 10 (qualification accuracy, unsupported-claim rate) separately per tier, so a cost-motivated routing change that quietly degrades quality is visible immediately, not discovered a quarter later; and
- treat routing as reversible — a tier assignment that data doesn't support should be easy to change back.

Cost optimization that isn't checked against quality is not optimization. It's a bet nobody is watching.

## 9.5 Dashboards for operators, not just developers

A developer debugging one failed request wants a trace. An operator watching the platform during business hours wants something different: a small number of signals that answer "is anything wrong right now, and where should I look first."

- overall error rate and p95 latency, with alerting thresholds tied to actual business impact, not arbitrary round numbers;
- cost run-rate, with an alert on any sudden deviation from the recent baseline;
- per-workflow health (qualification, planning, batch loop), so a degradation in one doesn't hide inside an aggregate that still looks fine; and
- a direct link from any alert to the relevant trace, so "something is wrong" leads immediately to "here is specifically what," rather than starting a fresh investigation from zero.

## 9.6 What AgentOps does not replace

Observability tells you what the system did and what it cost. It does not, by itself, tell you whether what it did was *correct* — a trace can show a qualification request completed quickly and cheaply while still producing a wrong recommendation. That question belongs to evaluation, and Chapter 10 makes it continuous rather than a one-time release gate.

## Hands-on lab: Instrument the platform

Implement:

- Cloud Trace instrumentation across the full request path, including the Chapter 6 A2A delegation and Chapter 8 gateway hop;
- cost attribution by user, workflow, and model tier, queryable after the fact;
- a tiered routing configuration for at least one WidgetWare task, with quality metrics tracked separately per tier; and
- an operator dashboard with the four signal categories from 9.5, and an alert wired to at least one of them.

## Evaluation checklist

- Can a single request's full path, across every agent and remote call, be reconstructed from its trace alone?
- Is cost attributable to a specific user and workflow, not only visible as a total?
- Is a tiered-routing decision backed by a measured quality comparison, not an assumption that a cheaper tier is "probably fine"?
- Does an alert lead directly to the relevant trace, rather than requiring a fresh investigation?
- Would an operator, with no access to source code, be able to answer "is anything wrong right now" from the dashboard alone?

## Chapter checkpoint

WidgetWare is now observable, cost-attributed, and operable in production. What remains is the discipline Book 1 could only apply once, at a release gate: proving, continuously, that the system is still behaving as intended as it keeps running and keeps changing.

## Bridge to Chapter 10

Chapter 10 closes Book 2 by making evaluation continuous — production golden datasets, trajectory scoring at scale, LLM-as-a-judge with human calibration, and online monitors — and assembles everything from both books into an enterprise capstone.

## Exercises

1. §9.1 distinguishes what a log, a metric, and a trace each answer. Take a real production incident you've experienced, or can imagine, and identify which of the three would have actually told you the root cause, and which would have only told you something was wrong.
2. §9.3 argues for attributing cost by user and workflow, not only tracking a total. Describe a cost anomaly that a total-spend dashboard would hide but a per-user, per-workflow breakdown would immediately surface.
3. §9.4 insists a cheaper model tier be backed by a measured quality comparison, "not an assumption that a cheaper tier is probably fine." Describe what evidence would actually convince you a tiered-routing decision is safe, versus what evidence people typically settle for instead.
4. §9.5 designs dashboards for an operator, not a developer. Take a dashboard you've actually used and evaluate it against §9.5's four signal categories — which one is missing, and what would an operator have to do instead, mid-incident, to get that missing signal?
5. §9.6 says observability "does not, by itself, tell you whether what the system did was correct." Describe a specific trace that would look completely healthy — fast, cheap, no errors — while the underlying qualification decision was still wrong.
<!-- END 10_Chapter_09_AgentOps_Observability_Cost_and_Quality.md -->

<!-- BEGIN 11_Chapter_10_Continuous_Evaluation_and_Enterprise_Capstone.md -->
# Chapter 10: Continuous Evaluation and Enterprise Capstone

## Chapter purpose

Book 1, Chapter 10 built a golden dataset and a release gate, checked once before deployment. That was correct for a bounded application evaluated before it shipped. A platform that keeps running, keeps changing, and keeps encountering production traffic no golden dataset anticipated needs evaluation that never stops. This closing chapter makes evaluation continuous, then assembles everything from both books into one enterprise capstone.

## Learning objectives

By the end of this chapter, the reader should be able to:

- explain why a release-gate evaluation, however thorough, is insufficient once a system runs continuously;
- build production evaluation that samples and scores live traffic, not only golden-dataset replay;
- score full trajectories, not only final answers, at production scale;
- calibrate an LLM-as-a-judge against human review, and know when to trust it and when not to;
- design online monitors that detect regression before a person notices; and
- assemble the full WidgetWare platform — both books — into one coherent, defensible system, and state honestly what it still does not do.

## Seven-Step mapping

**Primary:** Evaluate & Govern  
**Supporting:** Frame the Use Case, Build Context, Design Agent Capabilities, Build the Harness, Orchestrate Workflows, Engineer Loops

## The WidgetWare increment

Stand up continuous evaluation against production WidgetWare traffic, and produce the enterprise capstone release: every capability from both books, integrated, evaluated continuously, governed, and observable — with an honest maturity assessment of what remains.

## 10.1 A release gate is a snapshot; production is not

Book 1, Chapter 10.8's release gates asked whether the system was good enough to ship, measured against a golden dataset built before release. That dataset cannot anticipate every account, every phrasing, every edge case production traffic will actually produce — and the system itself keeps changing underneath it: new memory accumulates (Chapter 2), the knowledge base grows (Chapter 3), routing tiers shift (Chapter 9). A system that passed its release gate six months ago is not guaranteed to still deserve that judgment today.

## 10.2 Production evaluation, sampled and scored

Continuous evaluation does not mean scoring every request — that is rarely affordable and not necessary. It means a deliberate, representative sample of live traffic is captured, scored, and tracked over time:

```text
ProductionEvalSample
- request_id
- timestamp
- workflow: qualification | planning | batch_loop
- sampled_reason: random | flagged_by_monitor | user_reported
- trajectory_reference
- scores: {...}
```

Sample both randomly (to catch what nobody thought to test for) and deliberately (anything a Chapter 9 monitor flagged, anything a user reported). A production evaluation pipeline that only ever looks at flagged cases will systematically miss the failure modes nobody has flagged yet.

## 10.3 Trajectory scoring at scale

Book 1, Chapter 10.1 already argued that evaluation must cover the entire behavior — inputs, context assembly, tool calls, state transitions, not only the final answer. At production scale, this means the traces Chapter 9 built are not only an operational tool; they are the raw material evaluation scores against:

- did context assembly (Chapter 4) select genuinely relevant memory and retrieval results, or padding;
- did a Chapter 6 remote delegation get validated before its result was trusted, or accepted on arrival;
- did a Chapter 5 plan stay within its stated budget, or silently exceed it; and
- did the final output meet WidgetWare's evidence and approval requirements, unconditionally, regardless of how well everything upstream performed.

A trajectory that reaches the right final answer through a path that skipped evidence validation is not a passing trajectory. It got lucky, and continuous evaluation exists specifically to catch that distinction before it becomes a pattern.

## 10.4 LLM-as-a-judge, calibrated, not assumed

Book 1, Chapter 10.5 already warned that a model-based judge should use a specific rubric and should not be the sole authority for high-risk requirements. At production scale, add the discipline that makes a judge trustworthy enough to run continuously rather than only in a lab:

- calibrate the judge against a set of human-scored cases before trusting its scores in aggregate, and recalibrate periodically as the underlying system changes;
- track judge-versus-human agreement as its own metric, visible on the same dashboards Chapter 9 built — a drifting agreement rate is itself a signal something changed; and
- keep deterministic checks (schema validity, citation presence, approval recorded) as the non-negotiable layer no judge score can override, exactly as Book 1, Chapter 10.5 already established.

## 10.5 Online monitors: catching regression before a person does

A monitor is a standing, automated check against live metrics, not a one-time evaluation run:

- **quality monitors** — unsupported-claim rate, qualification-accuracy proxy, judge-agreement rate, each with a threshold and an alert;
- **safety monitors** — any prohibited action attempted (Book 1, Chapter 11.10's table), any Model Armor detection (Chapter 8.3), any access-control denial pattern that spikes; and
- **drift monitors** — the production traffic distribution itself changing shape (new account types, new request patterns) faster than the golden dataset represents it, a signal that the dataset itself needs updating, not only the system.

A monitor that fires and is routinely ignored is worse than no monitor — it trains the organization to distrust its own alerts. Every monitor needs an owner and a defined response, not just a dashboard tile.

## 10.6 The enterprise capstone

Assemble the complete system. By the end of this chapter, WidgetWare SDR Lab:

1. Researches, qualifies, drafts, and requests approval for one account (Book 1, Chapters 4–10).
2. Processes a bounded batch of accounts unattended, checkpointed, and budgeted (Book 1, Chapter 11).
3. Remembers a returning user, correctly scoped, without treating stale memory as current (Book 2, Chapter 2).
4. Grounds reasoning in enterprise knowledge, with citations and access control (Book 2, Chapter 3).
5. Assembles context deliberately under budget, with caching (Book 2, Chapter 4).
6. Decomposes an open-ended goal into a bounded, reviewable plan (Book 2, Chapter 5).
7. Delegates real capability to independently deployed agents, validated on return (Book 2, Chapter 6).
8. Acts under scoped, auditable identity — never one undifferentiated application identity (Book 2, Chapter 7).
9. Is registered, gated, and network-contained as a governed participant in a larger ecosystem (Book 2, Chapter 8).
10. Is traced, cost-attributed, and operable by someone who has never read its source code (Book 2, Chapter 9).
11. Is evaluated continuously, against production traffic, with a calibrated judge and standing monitors (this chapter).

## 10.7 An honest enterprise maturity assessment

State plainly what this capstone still does not do, the same discipline Book 1's own conclusion applied to itself:

- it does not autonomously send external communication or write to a CRM without human approval — that boundary from Book 1, Chapter 1.6 has not moved, at any point across either book;
- it does not fine-tune or distill its own models;
- it does not yet operate across multiple regions with active-active failover; and
- its continuous evaluation catches regression against what it currently knows to measure — it does not guarantee correctness against a failure mode nobody has yet imagined.

A platform this capable, still bounded this deliberately, is the actual argument of both books: capability and control were never in tension. They were built together, one chapter at a time.

## Hands-on lab: Ship the capstone

1. Stand up production sampling and trajectory scoring against live or realistic simulated traffic.
2. Calibrate an LLM-as-a-judge against a human-scored reference set; record the agreement rate.
3. Configure at least one quality monitor, one safety monitor, and one drift monitor, each with an owner and a defined response.
4. Assemble a capstone architecture diagram covering every numbered capability in 10.6.
5. Write the enterprise maturity assessment from 10.7 as a real document, not a formality — the next team to extend this system should be able to trust it.
6. Run the full test suite from both books against the assembled system and record the result as the Book 2 release.

## Evaluation checklist

- Does production evaluation sample both randomly and by monitor-flagged cases?
- Is trajectory scoring checking the path, not only the final answer?
- Is the LLM-as-a-judge's agreement with human scoring tracked as its own visible metric?
- Does every monitor have a defined owner and response, not just a threshold?
- Does the maturity assessment name real, current limitations rather than only accomplishments?

## Chapter checkpoint

WidgetWare SDR Lab is now a governed, observable, continuously evaluated enterprise platform, built from the same seven steps, the same evidence discipline, and the same human-approval boundary that Book 1 established on its very first page.

## Bridge to the Book 2 conclusion

The conclusion consolidates what changed between an application and a platform, restates the habits worth carrying into whatever comes next, and closes the WidgetWare story this series has followed since Chapter 1.

## Exercises

1. §10.1 argues a release gate is "a snapshot," not an ongoing guarantee, because the system keeps changing underneath it. List three things about WidgetWare that could change after a release gate passes, each from a different chapter of Book 2, that the original gate could not have anticipated.
2. §10.3 says a trajectory that reaches the right answer through a path that skipped evidence validation "got lucky," not passed. Describe a plausible way WidgetWare could produce a correct qualification while still skipping a required check somewhere in the pipeline — and what a trajectory-level score would catch that a final-answer-only score would miss.
3. §10.4 requires tracking judge-versus-human agreement as its own visible metric. If that agreement rate started drifting downward over a month, what are two different underlying causes it could indicate — one about the judge, one about the system itself — and how would you tell them apart?
4. §10.5 warns that a monitor which fires and is routinely ignored "trains the organization to distrust its own alerts." Describe a monitor you'd actually be tempted to silence rather than fix, and what the honest fix would look like instead.
5. §10.7 requires an honest maturity assessment naming real limitations. Using the enterprise capstone's eleven-item list in §10.6, pick one capability and write, in one paragraph, the honest limitation a marketing version of this same capstone would be tempted to leave out.
<!-- END 11_Chapter_10_Continuous_Evaluation_and_Enterprise_Capstone.md -->

<!-- BEGIN 12_Book_2_Conclusion.md -->
# Book 2 Conclusion: A System That Scales Without Loosening

Book 1 ended with a question answered modestly: an agent can research and qualify a prospective customer, and remain inspectable and under human control, while doing it. Book 2 asked a harder version of the same question: does that answer still hold once the system has to serve many users, remember across time, draw on enterprise-scale knowledge, plan over goals nobody pre-decomposed, collaborate with agents it doesn't own, and prove — continuously — that it is still behaving?

The answer is still yes. Not because scale is easy, but because nothing about scale required abandoning the discipline Book 1 built.

## What changed, and what didn't

Ten chapters added real capability:

- Sessions and Memory Bank gave WidgetWare a past, scoped correctly so one user's history never becomes another user's context.
- RAG Engine gave it enterprise knowledge, with the same citation discipline Book 1 required of any other evidence.
- Context engineering and caching gave it a way to afford all of that, deliberately, under a stated budget.
- Planning gave it the ability to decompose a goal it wasn't handed pre-solved, without becoming an unbounded loop.
- A2A gave it the ability to work with agents it doesn't own, validated the moment their output arrives, never trusted on arrival.
- Identity separated who is actually acting — user, application, or a specific workload — so an audit never has to guess.
- Registry, gateway, and containment made it a governed participant in something larger than itself.
- Tracing, cost attribution, and monitors made it operable by someone who has never read its source.
- Continuous evaluation replaced a release-gate snapshot with a standing, calibrated check against what the system is actually doing right now.

What did not change: the evidence policy. The prohibition on inventing a stakeholder. The requirement that external action and CRM writes stay behind human approval. The distinction between a model's confidence and a calibrated probability. Every one of these survived ten chapters of added capability completely intact, because none of Book 2's new infrastructure was built as an exception to them — each chapter extended a plane Chapter 1 named, under the same rules Book 1 established before Book 2 existed.

## Five habits that mattered more at scale, not less

### 1. Separate the planes before you build inside one

Chapter 1's five planes — control, runtime, knowledge, integration, governance — kept nine subsequent chapters from becoming an undifferentiated pile of "enterprise features." A memory bug and an identity bug are different problems, owned differently, and conflating them costs real time during an incident.

### 2. Scope, don't just secure

Least privilege, applied to tools in Book 1, had to be applied again — to memory, to retrieval, to identity, to gateway policy — at every layer Book 2 added. Security that stops at the application boundary is not security at platform scale; it is a boundary an attacker only has to go around once.

### 3. A remote result is still an unverified claim

Whether it came from a webpage, a retrieved document, or an independently deployed agent, external content earned trust the same way in every chapter: by being checked against WidgetWare's own contract, never by the confidence of its source.

### 4. Budgets apply to everything that repeats

Loops needed them in Book 1. Plans needed them in Chapter 5. Even context assembly needed one, in Chapter 4. Anything that can consume more resources than intended, given enough time, needs a stated limit before it runs — not a limit discovered after an incident.

### 5. Evaluate the path, continuously, not the answer, once

A release gate proves a system was good enough on the day it shipped. Chapter 10's continuous evaluation is the only honest claim that it still is, today, against traffic nobody anticipated when the gate was built.

## What Book 2 still does not do

Multi-region failover. Fine-tuning or distilling custom models. Voice and multimodal interfaces. A full organizational agent-lifecycle process. These are not oversights. They are the next architectural layer, and naming them honestly — rather than implying this capstone is more finished than it is — is the same discipline Book 1's own conclusion insisted on.

## The argument this whole series has been making

> Agent Engineering is the discipline of placing model intelligence inside an engineered system — and keeping that system engineered as it grows, not merely as it starts.

A capable model does not become a trustworthy platform by adding more capability to it. It becomes one by adding context, capabilities, structure, evidence, identity, governance, and continuous proof — in that order, deliberately, at every scale the system is asked to operate at.

WidgetWare began Book 1 as a question one developer could answer on a laptop: can an agent help, safely, with one account? It ends Book 2 as a platform an enterprise can actually depend on, answering the same question, at scale, without ever having had to loosen it to get there.
<!-- END 12_Book_2_Conclusion.md -->

