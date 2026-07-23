# Class 10 — AgentOps, Optimization, and Capstone

**Manuscript source:** Book 2, Chapter 9 (AgentOps: Observability, Cost, and Quality) and Chapter 10 (Continuous Evaluation and Enterprise Capstone)
**Seven-Step mapping:** Primary: Evaluate & Govern / Supporting: all six other steps
**Golden solution produced:** `golden-solutions/class-10/`
**Starting checkpoint:** `golden-solutions/class-09/`

This is the final class. It closes both books: instrument what's been built, make evaluation continuous instead of a one-time gate, then assemble everything from Class 1 through Class 9 into one capstone demonstration.

## 0:00–0:30 — Homework review, common mistakes, golden solution reveal

- **Review homework:** ask participants which Extension they chose (RAG, A2A, or Identity) and to demonstrate the cross-user isolation test's terminal output.
- **Common mistakes to flag:** extraction policies that block a full account brief from being duplicated into memory, but don't yet stop a one-off task instruction from sneaking in as a "durable preference."
- **Golden solution reveal:** walk `class-09/`'s memory integration, then ask: with memory, and possibly RAG, A2A, or Identity added, how would anyone actually *operate* this system in production, or know if it's still behaving?

## Slide outline (0:30–0:55)

1. Current WidgetWare state: a memory-aware, identity-scoped agent — the full Book 2 landscape from Class 9, one piece actually built
2. Today's dependency: nine classes of capability now need to be observable, cost-attributed, and continuously proven correct
3. Business objective: instrument the platform, then close with the enterprise capstone
4. Core concept: logs, metrics, and traces answer different questions (§9.1); a release gate is a snapshot, production is not (§10.1)
5. Terminology: distributed tracing across an A2A delegation and a gateway hop (§9.2); trajectory scoring, not just final-answer scoring (§10.3)
6. Architecture: cost attribution by user, workflow, and model tier (§9.3); tiered model routing, examined not assumed (§9.4)
7. Seven Steps mapping: Evaluate & Govern, now explicitly supported by every one of the other six steps — the whole framework, closing the loop
8. Gemini vs. deterministic code: an LLM-as-a-judge scores trajectory quality; deterministic checks (schema, citations, approval recorded) remain the non-negotiable layer no judge score overrides (§10.4)
9. Security: online monitors — quality, safety, and drift — each with an owner and a defined response (§10.5)
10. Today's increment: Cloud Trace instrumentation, cost attribution, an operator dashboard; then production sampling, a calibrated judge, and the capstone assembly
11. Lab architecture: the enterprise capstone's eleven-item checklist (§10.6)
12. Acceptance criteria: an honest maturity assessment — what the capstone still does not do (§10.7)

## Kahoot (6–8 questions)

- Terminology: What question does a trace answer that a log and a metric each cannot (§9.1)?
- Terminology: Why is a release gate "a snapshot" rather than an ongoing guarantee (§10.1)?
- Architecture: Why attribute cost to a specific user and workflow instead of only tracking a total (§9.3)?
- Architecture: What must be calibrated before an LLM-as-a-judge's scores can be trusted in aggregate (§10.4)?
- Failure analysis: A monitor fires repeatedly and the team starts ignoring it — what does §10.5 say this trains the organization to do?
- Security/governance: Name one thing the enterprise maturity assessment must state honestly, even though it's a limitation (§10.7).
- WidgetWare scenario: A trajectory reaches the right final qualification but skipped evidence validation along the way — is it a passing trajectory (§10.3)?
- Connecting back: How does this class's five-way-decision-adjacent monitor design echo the loop's CONTINUE/RETRY/STOP/DEFER/ESCALATE from Class 8?

## Build together (1:05–1:35)

**Chapter 9 portion:**
- Cloud Trace instrumentation across the full request path, including the Class 9 memory lookup and, if built, the A2A delegation and gateway hop
- cost attribution by user, workflow, and model tier
- a tiered routing configuration for one WidgetWare task (e.g., route straightforward qualifications to a lighter tier), with quality tracked separately per tier
- an operator dashboard with the four signal categories (§9.5), and one alert wired to it

**Chapter 10 portion:**
- stand up production sampling and trajectory scoring against realistic simulated traffic
- calibrate an LLM-as-a-judge against a small human-scored reference set; record the agreement rate
- configure one quality monitor, one safety monitor, and one drift monitor, each with an owner and a defined response
- assemble the capstone architecture: walk the eleven-item list from §10.6 against the actual codebase built across all ten classes, checking off what's real
- write the honest maturity assessment from §10.7 as a real document

## Test and diagnose (1:35–1:50)

1. Run a traced request end to end and reconstruct its full path from the trace alone (happy path).
2. Run the cost-attribution query for a specific user and workflow (this chapter's contract-equivalent check).
3. Trigger a deliberate quality regression (feed a judge-scored trajectory that skips evidence validation) and confirm the drift/quality monitor fires.
4. Inspect the fired alert and confirm it links directly to the relevant trace, per §9.5's evaluation criterion.
5. Diagnose using the Framework's seven categories — by this class, failures can come from any of them, which is the point: everything built across ten classes is now one system to reason about together.
6. Apply the smallest fix.
7. Re-run the full ten-class scenario suite, one final time, top to bottom.

## Homework — the final assignment

There is no Class 11. The final assignment is the capstone demonstration itself.

| Level | Task |
| ----- | ---- |
| **Required** | Run the full ten-class test suite against the assembled system and produce the capstone release: every numbered capability in §10.6, an architecture diagram covering all of them, and the honest maturity assessment from §10.7 |
| **Diagnostic** | Find one place where a chapter's own "what this doesn't do yet" boundary quietly got crossed somewhere in the accumulated ten classes of code, and either fix it or document it honestly in the maturity assessment |
| **Extension** | Present the five-case final demonstration from Class 8 (§10.9 of Book 1) *and* one Book 2 capability of the participant's choice, back to back, as a single narrative: "here is what one account gets, and here is what changes at scale" |

- **Starting checkpoint:** `golden-solutions/class-09/`
- **Files participants may modify:** anything, this is the capstone
- **Expected behavior:** the system observable, cost-attributed, continuously evaluated, and its own limitations named in writing
- **Tests that must pass:** the full accumulated test suite, Class 1 through Class 10
- **Submission:** the capstone architecture diagram, the maturity assessment document, and one full instrumented-trace output
- **Constraints:** the maturity assessment must name real, current limitations — a document that only lists accomplishments does not pass

## Golden solution: `class-10/`

The final, complete reference implementation — every prior `class-NN/` checkpoint's work, integrated, instrumented, and continuously evaluated. README is the course's own closing statement, adapted from Book 2's conclusion: capability and control were never in tension across these ten classes — they were built together, one class at a time.

## Course closing note

The same principle that opened Class 1 closes Class 10: *is this behavior better expressed as model reasoning or deterministic software?* Ten classes, two books, and one running system later, that is still the only question that matters — scale just raised the cost of answering it wrong.
