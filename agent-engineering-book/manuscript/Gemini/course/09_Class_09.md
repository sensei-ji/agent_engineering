# Class 9 — Memory, RAG, A2A, Identity, and Governance

**Manuscript source:** Book 2, Chapters 2–8 (Sessions/Memory, Enterprise Knowledge/RAG, Context Engineering at Scale, Goals/Planning, Distributed Agent Collaboration, Agent Identity, Agent Governance)
**Seven-Step mapping:** Build Context (Ch2–4), Engineer Loops (Ch5), Design Agent Capabilities (Ch6), Build the Harness (Ch7), Evaluate & Govern (Ch8)
**Golden solution produced:** `golden-solutions/class-09/`
**Starting checkpoint:** `golden-solutions/class-08/`

This is deliberately a **survey class**, not seven classes compressed into one. A two-hour class cannot build enterprise memory, RAG, adaptive planning, A2A, identity, and governance and have every one of them be real, tested code. The lecture segment covers all seven chapters at landscape depth — enough that a participant can explain what each capability is, why Book 2 sequences them this way, and where to go deepen any one of them later. The hands-on build stays narrow: **Memory Bank only**, using Book 2 Chapter 2's own Hands-on Lab. The homework's Extension level is where participants who want more can reach into Chapters 3, 6, or 7 individually.

## 0:00–0:30 — Homework review, common mistakes, golden solution reveal

- **Review homework:** ask participants to demonstrate their `DEFER` scenario account and confirm it wasn't silently discarded.
- **Common mistakes to flag:** budget checks that stop the whole run instead of just the offending account; run reports that record `stop_reason` as free text instead of one of the five named outcomes.
- **Golden solution reveal:** walk `class-08/`'s full batch loop, then say explicitly: this is where Book 1 ends and Book 2 begins — same system, harder question. "Does this still hold once many users depend on it?"

## Slide outline (0:30–0:55) — landscape depth, seven chapters

1. Current WidgetWare state: a bounded, evaluated, looping single-tenant application (end of Book 1)
2. Today's dependency: everything from here on assumes one running system serving *many* users, not one developer on one laptop
3. Business objective: survey the five architectural planes Book 2 Chapter 1 named — control, runtime, knowledge, integration, governance
4. Core concept, Ch2: session state vs. long-term memory — Agent Platform Memory Bank, identity-scoped, extraction is deliberate not automatic (§2.1, §2.3)
5. Core concept, Ch3: retrieval as a seven-stage pipeline, not one call — chunking as a design decision, access control not optional, retrieved content still untrusted (§3.1–3.5)
6. Core concept, Ch4: a context budget stated explicitly; selecting, not just fitting; caching the stable part; summarization is lossy compression (§4.2–4.5)
7. Core concept, Ch5: a fixed workflow vs. a goal the agent must decompose itself; ADK's `PlanReActPlanner`; a typed plan contract; the same five-way decision, now applied to a plan (§5.1–5.6)
8. Core concept, Ch6: MCP vs. A2A precisely; Agent Cards as the A2A equivalent of a Skill's discovery description; a remote agent is not a trusted extension of your own (§6.1–6.4)
9. Core concept, Ch7: three identities — user, application, agent (workload); Google Cloud's **Agent Identity**, SPIFFE-based, distinct from a bare service account, with dual-identity audit logging (§7.1–7.3)
10. Core concept, Ch8: Agent Registry, Agent Gateway, Model Armor, VPC Service Controls as a network backstop (§8.1–8.4)
11. Seven Steps mapping across all seven chapters at a glance — nothing new is added to the framework; every chapter deepens a step already named in Book 1
12. Today's actual build: Memory Bank only — acceptance criteria from Book 2 §2's evaluation checklist

## Kahoot (6–8 questions)

- Terminology: What's the difference between ADK session state and Agent Platform Memory Bank (§2.1)?
- Terminology: What does an Agent Card's discovery description do, and what Book 1 concept is it the A2A equivalent of (§6.2)?
- Architecture: Why does retrieved enterprise content still need the same untrusted-data treatment as retrieved web content (§3.5, connecting back to Class 6)?
- Architecture: What does Google Cloud's Agent Identity add beyond a general-purpose service account (§7.3)?
- Failure analysis: A planning agent replans three times without its progress signal advancing — what should happen (§5.5)?
- Security/governance: Why can't a team "just this once" route around the Agent Gateway under deadline pressure (§8.6)?
- WidgetWare scenario: A remote enrichment agent returns a high-confidence claim with no citation — is it trusted?
- Connecting back: How does the five-way decision (CONTINUE/RETRY/STOP/DEFER/ESCALATE) from Class 8's loop reappear, applied to a plan, in Chapter 5?

## Build together (1:05–1:35) — Memory Bank only, following Book 2 §2's Hands-on Lab exactly

- `src/widgetware_sdr/memory/service_config.py` — configure a persistent `SessionService` and the Agent Platform Memory Bank-backed memory service
- `src/widgetware_sdr/memory/extraction_policy.py` — the explicit rules for what is and is not written to memory
- update the qualification agent's instructions so it consults memory, scoped to the current user, before starting research
- tests for: cross-user isolation, a memory correctly surfacing a user's prior work on an account, and a stale memory being flagged rather than trusted outright

Build the cross-user isolation test live and make it actually attempt the leak (one user's session searching under another user's `user_id`) rather than merely asserting scoping exists in code — the Evaluation checklist's own phrasing is explicit: "does a cross-user memory search test actually attempt the leak and confirm it fails?"

## Test and diagnose (1:35–1:50)

1. Run the happy-path memory test: a returning user's prior work on an account is correctly surfaced.
2. Run the extraction-policy test (this chapter's contract-equivalent): only content passing the explicit policy gets written.
3. Trigger the cross-user isolation attempt and confirm it fails to leak.
4. Inspect a stale-memory case: does the agent flag it as "previously noted" rather than treating it as currently verified (the fact/inference/hypothesis discipline from Class 1, applied to memory)?
5. Diagnose: a leak here is almost always a **permissions** failure (missing or wrong `user_id` scope on the search call), not a model-behavior issue.
6. Apply the smallest fix — scope the search call correctly.
7. Re-run all four memory tests.

## Homework

| Level | Task |
| ----- | ---- |
| **Required** | Memory Bank integration passes all four tests: happy path, extraction policy, cross-user isolation, stale-memory flagging |
| **Diagnostic** | The provided extraction-policy test currently lets a one-off task instruction ("skip this specific account") get written to memory as if it were a durable preference — fix the policy so it doesn't |
| **Extension** | Choose one: (a) add a single RAG-backed enterprise document lookup per Book 2 Ch3, with a citation on every returned fact; (b) add one A2A delegation to a mock remote agent per Book 2 Ch6, validated before its result is trusted; or (c) add a scoped service account or Agent Identity per Book 2 Ch7 for the memory service specifically |

- **Starting checkpoint:** `golden-solutions/class-08/`
- **Files participants may modify:** `src/widgetware_sdr/memory/`, `tests/`, plus whichever files the chosen Extension touches
- **Expected behavior:** memory is identity-scoped, policy-filtered, and never silently treated as a currently verified fact
- **Tests that must pass:** the four required memory tests
- **Submission:** the cross-user isolation test's terminal output (showing the leak attempt and its failure), plus a one-paragraph note on which Extension was attempted, if any
- **Constraints:** memory remains read/write for the agent's own scoped store only — no change to WidgetWare's approval boundary from Class 1

## Golden solution: `class-09/`

Adds `memory/service_config.py`, `memory/extraction_policy.py`, and the four memory tests on top of `class-08/`. README includes a short landscape map of Book 2 Chapters 3, 4, 5, 6, 7, and 8 — one paragraph each, pointing to the actual chapter for anyone who picked a different Extension or wants to go deeper after the course ends.

## Bridge to Class 10

Class 10 closes the program: AgentOps observability across everything built so far, then the enterprise capstone — assembling both books' capabilities into one evaluated, governed, continuously-monitored system, and stating honestly what still isn't there.
