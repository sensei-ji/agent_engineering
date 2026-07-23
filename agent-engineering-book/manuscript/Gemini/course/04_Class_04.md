# Class 4 — First ADK Agent and Reusable Skill

**Manuscript source:** Book 1, Chapter 4 (Your First Agent with ADK) and Chapter 5 (Skills and Reusable Agent Capabilities)
**Seven-Step mapping:** Primary: Build the Harness (Ch4) and Design Agent Capabilities (Ch5) / Supporting: Design Agent Capabilities, Evaluate & Govern
**Golden solution produced:** `golden-solutions/class-04/`
**Starting checkpoint:** `golden-solutions/class-03/`

This is the first two-chapter class. Chapter 4 gets a working agent on screen; Chapter 5 immediately extracts its procedure into a reusable Skill, so participants never see "an agent with a big embedded prompt" presented as a stable end state.

## 0:00–0:30 — Homework review, common mistakes, golden solution reveal

- **Review homework:** ask participants to show their injection-attempt test and explain, in their own words, why it was failing before the fix.
- **Common mistakes to flag:** context builders that block the specific injection phrase used in class instead of the general pattern (trusting account-note content as instruction); model selection hardcoded in three places instead of one.
- **Golden solution reveal:** walk `class-03/`'s `context_builder.py`, then explicitly say: "today this context finally reaches a real agent."

## Slide outline (0:30–0:55)

1. Current WidgetWare state: real context, no agent yet
2. Today's dependency: Class 3's context package becomes this agent's instructions
3. Business objective: a qualification assistant that reasons over one account, reproducibly
4. Core concept: ADK as an application framework (§4.1) — Agent, Session, Event, Runner
5. Terminology: sessions and events (§4.3), basic state (§4.4); then Skill vs. prompt vs. tool (§5.2–5.3)
6. Architecture: the first agent boundary (§4.2) — then how a Skill directory (§5.5) replaces an embedded prompt block
7. Seven Steps mapping: Build the Harness → Design Agent Capabilities, the first real handoff between two steps
8. Gemini vs. deterministic code: the agent reasons; `app.py` and the Skill's typed sections stay deterministic
9. Security: the agent must stay within its boundary and say when information is missing (Evaluation checklist, §4)
10. Today's increment: `qualification_agent.py`, then `skills/icp_qualification/`
11. Lab architecture: local playground inspection (§4.6) — assembled instructions, event sequence, latency
12. Acceptance criteria: scenario tests evaluate behavior, not exact phrasing

## Kahoot (6–8 questions)

- Terminology: What is the difference between a Skill and a tool (§5.3)?
- Terminology: What does an ADK `Session` separate that a raw conversation history doesn't?
- Architecture: Why does progressive disclosure (§5.6) matter for context consumption?
- Architecture: Why move the qualification procedure out of the agent's embedded instructions and into a Skill?
- Failure analysis: The agent confidently qualifies an account with clearly insufficient evidence — where's the fix, agent code or Skill procedure?
- Security/governance: What should the agent do when required account information is simply missing?
- WidgetWare scenario: A second agent needs the same qualification logic — what does the Skill's reusability buy you here?
- Connecting back: How does §3.5's evidence-policy vocabulary (Class 3) show up inside the Skill's procedure?

## Build together (1:05–1:35)

**Chapter 4 portion:**
- `src/widgetware_sdr/agents/qualification_agent.py`
- `src/widgetware_sdr/app.py`
- a local run command
- sample account profiles under `data/sample_accounts/` (build the Acme Manufacturing profile live: 22,000 employees, `region: united_states`, plant-modernization challenges)
- scenario tests for qualified, unqualified, and uncertain accounts

**Chapter 5 portion, same class:**
- `skills/icp_qualification/skill.md`, `examples/{qualified,unqualified,needs_research}.md`, `tests/cases.yaml`
- refactor `qualification_agent.py` to read its procedure from the Skill instead of an embedded instruction block
- add the lightweight **Evidence Classification** Skill (verified fact / inference / unknown / conflict)

## Test and diagnose (1:35–1:50)

1. Run the qualified-account scenario test (happy path).
2. Run the uncertain-account test (this chapter's contract-equivalent check: does the agent correctly say "insufficient evidence" instead of guessing?).
3. Trigger a failure: run the *pre-refactor* agent (embedded prompt) against a scenario, then the *post-refactor* Skill-driven agent against the same scenario, and diff the reasoning.
4. Inspect the event sequence and assembled instructions via the local playground (§4.6).
5. Diagnose: is a discrepancy caused by context (missing Skill content), model behavior, or the Skill's procedure itself being under-specified?
6. Apply the smallest fix — usually tightening the Skill's procedure or examples, not the agent's Python code.
7. Re-run all three scenario tests.

## Homework

| Level | Task |
| ----- | ---- |
| **Required** | Qualification agent runs reproducibly against all three scenario accounts, driven entirely by the Skill (no embedded procedure left in Python) |
| **Diagnostic** | The Evidence Classification Skill misclassifies one deliberately ambiguous fact in the provided test case — fix the Skill, not the agent |
| **Extension** | Add a fourth sample account profile and a matching scenario test, chosen to stress a boundary condition (exactly at the 5,000-employee ICP threshold) |

- **Starting checkpoint:** `golden-solutions/class-03/`
- **Files participants may modify:** `src/widgetware_sdr/agents/qualification_agent.py`, `src/widgetware_sdr/app.py`, `data/sample_accounts/`, `skills/icp_qualification/`, `tests/`
- **Expected behavior:** the agent's qualification procedure lives entirely in the Skill; the agent code only wires context, Skill, and model together
- **Tests that must pass:** all three (or four, with the extension) scenario tests
- **Submission:** local-playground event-sequence printout for one scenario, plus test output
- **Constraints:** no structured/typed output yet (Chapter 6) — the agent's result is still prose at this stage, on purpose

## Golden solution: `class-04/`

Adds the ADK agent, `app.py`, sample accounts, and both Skills on top of `class-03/`. README notes the Chapter 4 checkpoint explicitly: "It can reason about supplied account data but does not yet expose its procedure as a reusable Skill or return a machine-validated contract" — then shows how this checkpoint already closes the first half of that gap.

## Bridge to Class 5

Class 5 replaces the agent's prose output with a typed, validated contract, and gives it its first real tool — the two changes that make the agent's output safe for another piece of software to consume.
