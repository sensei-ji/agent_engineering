# Class 8 — Evaluation, Deployment, and Bounded Loops

**Manuscript source:** Book 1, Chapter 10 (Evaluate, Deploy, and Demonstrate) and Chapter 11 (Loop Engineering with ADK)
**Seven-Step mapping:** Primary: Evaluate & Govern (Ch10) and Engineer Loops (Ch11) / Supporting: Build the Harness, Orchestrate Workflows
**Golden solution produced:** `golden-solutions/class-08/`
**Starting checkpoint:** `golden-solutions/class-07/`

This class closes Book 1. It has two distinct halves with a hard boundary between them: Chapter 10 proves the single-account workflow is good enough to ship; Chapter 11 only then wraps that *unchanged* workflow in a bounded loop. Do not let the loop discussion bleed into the evaluation discussion — the manuscript's own ordering argument (evaluate one unit before you automate it) is the lesson, not just the schedule.

## 0:00–0:30 — Homework review, common mistakes, golden solution reveal

- **Review homework:** ask participants to walk through their fixed rejected-approval state and show the checkpoint-resume output.
- **Common mistakes to flag:** state machines that allow a "silent" transition with no corresponding test; checkpoints that persist research and qualification results but not which stage the workflow was actually in.
- **Golden solution reveal:** walk `class-07/`'s full workflow, run all five scenarios live, then ask: is this good enough to actually ship? — the class's first real question.

## Slide outline (0:30–0:55)

1. Current WidgetWare state: a complete bounded workflow, ending at `AWAITING_APPROVAL`
2. Today's dependency: Chapter 10 proves this workflow is ready; Chapter 11 only then automates it
3. Business objective, part 1: prove quality with a golden dataset and release gate; part 2: run unattended across a queue, safely
4. Core concept: evaluation is broader than the final answer (§10.1) — then, a loop is not `max_iterations` alone (§11.4)
5. Terminology: evaluation layers (§10.2) and release gates (§10.8); the inner ADK loop vs. the outer engineered loop (§11.2–11.3)
6. Architecture: the golden dataset and LLM-as-a-judge with caution (§10.3, §10.5); `LoopAgent` wired to the Chapter 9 workflow (§11.3)
7. Seven Steps mapping: Evaluate & Govern, then Engineer Loops — the first time two entire steps map to one class
8. Gemini vs. deterministic code: a judge model scores reasoning quality; deterministic checks (schema, citations, approval recorded) are non-negotiable regardless of judge score
9. Security: the five-way decision (§11.8) — CONTINUE, RETRY, STOP, DEFER, ESCALATE — and that human approval authority (§11.10) does not change inside a loop
10. Today's increment: the golden dataset and evaluation command, then durable session state (§11.5) and the batch loop
11. Lab architecture: the final five-case demonstration (§10.9); explicit states and transitions for the loop (§11.6)
12. Acceptance criteria: the deployment is reproducible and reversible; the loop stops for a reason it can name

## Kahoot (6–8 questions)

- Terminology: What's the difference between a schema check and a semantic (LLM-as-a-judge) check, and why keep them in separate layers (§10.5)?
- Terminology: What are the five outcomes of the loop's per-account decision (§11.8)?
- Architecture: Why is `max_iterations` alone not an engineered loop (§11.4)?
- Architecture: What's the difference between the inner agent loop ADK already runs and the outer loop this chapter adds (§11.2–11.3)?
- Failure analysis: A restarted batch run re-researches an account it already finished — what's missing from session state?
- Security/governance: Does an account processed inside an unattended batch loop get less approval scrutiny than one processed on request? What does §11.10 say?
- WidgetWare scenario: The loop hits its maximum-attempts limit for one account — CONTINUE, RETRY, STOP, DEFER, or ESCALATE?
- Connecting back: How does the loop's verification-before-advancing step (§11.7) reuse the typed contracts from Class 5 and the state machine from Class 7?

## Build together (1:05–1:35)

**Chapter 10 portion (roughly first half):**
1. Build the golden dataset.
2. Run unit, contract, and scenario tests together.
3. Add an evaluation command and report.
4. Add structured logs and trace identifiers.
5. Package the application; run smoke tests.
6. Deliver the five-case final demonstration live: success, insufficient-evidence, conflict, safety (injection resisted), approval-rejected.

**Chapter 11 portion (second half):**
- `loop/account_queue.py` — work discovery and selection policy
- `loop/budget.py` — the budget dataclass and stop-condition check
- `loop/decision.py` — the five-way decision function
- `loop/run_report.py` — a report every run produces, with `stop_reason`
- wire a `LoopAgent` to the Chapter 9 workflow, backed by a persistent `SessionService`
- a small seed queue of at least four accounts, at least one outside WidgetWare's ICP

## Test and diagnose (1:35–1:50)

1. Run the golden-dataset evaluation report (happy path for Chapter 10's half).
2. Run the loop's scenario tests: a fresh account gets selected, a settled one doesn't.
3. Trigger a failure: restart the process mid-batch and confirm the loop resumes from saved session state instead of reprocessing.
4. Inspect the run report's `stop_reason` and per-status totals.
5. Diagnose: a restart that reprocesses a settled account is almost always a **workflow state** or missing-**permissions**-to-persist issue (an `InMemorySessionService` used where a durable one was needed).
6. Apply the smallest fix — usually swapping in the persistent `SessionService` or fixing what gets checkpointed.
7. Re-run the full scenario suite from both halves of the class.

## Homework

| Level | Task |
| ----- | ---- |
| **Required** | Golden-dataset evaluation report runs clean; the batch loop processes the four-account seed queue and produces a run report naming its `stop_reason` |
| **Diagnostic** | The provided budget test currently lets one bad account consume retries meant for the whole run — enforce the per-account attempt limit correctly |
| **Extension** | Add a fifth account to the seed queue chosen specifically to trigger `DEFER` (a dependency temporarily unavailable), and confirm it doesn't get discarded |

- **Starting checkpoint:** `golden-solutions/class-07/`
- **Files participants may modify:** `src/widgetware_sdr/eval/`, `src/widgetware_sdr/loop/`, `tests/`
- **Expected behavior:** the single-account workflow passes its release gate unchanged; the loop then runs that same workflow across a queue, unattended, within stated budgets, stopping for a nameable reason
- **Tests that must pass:** the golden-dataset evaluation suite; the loop scenario tests (fresh-account selection, settled-account skip, restart-resume, budget stop, attempt-limit stop)
- **Submission:** the five-case final demonstration output, plus one full batch-loop run report
- **Constraints:** nothing about the single-account workflow changes in this chapter — the loop wraps it, it does not modify it; still no send tool anywhere

## Golden solution: `class-08/`

Adds the evaluation harness, golden dataset, deployment packaging, and the full batch loop on top of `class-07/`. README closes with Book 1's own conclusion framing: the system now works "for one account at a time, run on request," **and** across a bounded, unattended batch — but still cannot decompose its own goals, collaborate with agents it doesn't own, or prove continuously (not just once) that it still behaves. That gap is Book 2, and Classes 9–10.

## Bridge to Class 9

Book 1 is complete. Class 9 begins Book 2: the same WidgetWare system, now asked to serve many users, remember across time, draw on enterprise knowledge, plan over ambiguous goals, and collaborate with agents it doesn't own.
