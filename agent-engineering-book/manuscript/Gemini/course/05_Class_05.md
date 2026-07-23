# Class 5 — Structured Outputs and Tool Engineering

**Manuscript source:** Book 1, Chapter 6 (Structured Outputs and Agent Contracts) and Chapter 7 (Tool Engineering)
**Seven-Step mapping:** Primary: Design Agent Capabilities / Supporting: Orchestrate Workflows, Build the Harness, Evaluate & Govern
**Golden solution produced:** `golden-solutions/class-05/`
**Starting checkpoint:** `golden-solutions/class-04/`

## 0:00–0:30 — Homework review, common mistakes, golden solution reveal

- **Review homework:** ask participants to demonstrate the Evidence Classification Skill fix and explain what made the ambiguous fact ambiguous.
- **Common mistakes to flag:** Skills that still leak procedure back into the agent's Python instructions "just this once"; boundary-condition test accounts (exactly 5,000 employees) that expose an off-by-one in the ICP check written in Class 3.
- **Golden solution reveal:** walk `class-04/`'s Skill-driven agent, then run it once and show the output is still just a paragraph of prose — the gap this class closes.

## Slide outline (0:30–0:55)

1. Current WidgetWare state: a Skill-driven agent whose output is prose
2. Today's dependency: a typed contract is what every future workflow stage (Class 7 onward) will actually consume
3. Business objective: a machine-validated qualification result, still readable to a person
4. Core concept: prose is for people, contracts are for systems (§6.1); then a tool lets the agent *do something outside the model* (§7.1, §5.3 recap)
5. Terminology: confidence is not probability (§6.3); tool descriptions are part of control (§7.2)
6. Architecture: the qualification schema (§6.2) and its enumerated states — `QUALIFIED`, `NOT_QUALIFIED`, `NEEDS_RESEARCH`, `BLOCKED`
7. Seven Steps mapping: both chapters are Design Agent Capabilities — a contract and a tool are both capability, engineered
8. Gemini vs. deterministic code: the model proposes a qualification; deterministic invariants (§6.2) enforce or reject it after the fact
9. Security: least privilege for tools (§7.5) — narrower than the underlying platform account
10. Today's increment: `contracts/qualification.py`, `contracts/evidence.py`, then `get_account_profile`, `get_widgetware_product`, `get_icp_policy`, `calculate_fit_score`
11. Lab architecture: validation and repair (§6.5); tool testing without the agent (§7.8)
12. Acceptance criteria: invalid model output fails safely to `BLOCKED`, never a guessed result

## Kahoot (6–8 questions)

- Terminology: What's the difference between a model's stated confidence and a calibrated probability (§6.3)?
- Terminology: What must a `NOT_QUALIFIED` result contain, structurally (§6.2's invariant)?
- Architecture: Why is `calculate_fit_score()` deterministic code and not a model judgment?
- Architecture: Why does a tool's description matter as much as its implementation (§7.2)?
- Failure analysis: The model returns malformed JSON for a qualification result — what should the system do?
- Security/governance: What does "permissions narrower than the underlying platform account" mean for `get_account_profile`?
- WidgetWare scenario: An account has zero missing-information items but was still labeled `NEEDS_RESEARCH` — what's wrong?
- Connecting back: How does this chapter's evidence-reference requirement build directly on Class 3's evidence-policy vocabulary?

## Build together (1:05–1:35)

**Chapter 6 portion:**
- `src/widgetware_sdr/contracts/evidence.py`, `contracts/qualification.py`
- schema validation tests and business-invariant tests (the four deterministic rules: `NOT_QUALIFIED` needs an exclusion/failed criterion, `QUALIFIED` needs an evidence reference, `NEEDS_RESEARCH` needs a missing-information item, any failure produces `BLOCKED`)
- wire the qualification agent to emit the typed contract instead of prose

**Chapter 7 portion, same class:**
- `get_account_profile(account_id)`, `get_widgetware_product(product_id)`, `get_icp_policy()`, `calculate_fit_score()`
- attach the read tools to the qualification agent
- update the contract so every retrieved fact carries an evidence identifier

## Test and diagnose (1:35–1:50)

1. Run the schema-validation happy path (a well-formed `QUALIFIED` result).
2. Run the business-invariant test (contract/schema check specific to this chapter): a `QUALIFIED` result with zero evidence references should be rejected.
3. Trigger a failure: feed the agent a scenario likely to produce malformed or borderline output and watch the repair-or-`BLOCKED` path (§6.5) fire.
4. Inspect the tool call sequence: did `get_account_profile` get called with a valid, typed `account_id`?
5. Diagnose using the Framework's seven categories — this class's failures are almost always **contract validation** or **tool implementation**, rarely context (that was Class 3's job).
6. Apply the smallest fix — usually a missing invariant check or a tool's output normalization (§7.4).
7. Re-run all contract and tool tests.

## Homework

| Level | Task |
| ----- | ---- |
| **Required** | Qualification agent emits a schema-valid, invariant-passing contract for all Class 4 scenario accounts, backed by the four internal tools |
| **Diagnostic** | One provided test case returns `QUALIFIED` with a evidence reference that doesn't actually trace to a tool-returned fact — find and fix the gap |
| **Extension** | Add tool-level tests per §7.8's full list (valid input, invalid input, missing record, dependency failure, permission failure, deterministic output shape, redaction of prohibited fields) for one tool of your choice |

- **Starting checkpoint:** `golden-solutions/class-04/`
- **Files participants may modify:** `src/widgetware_sdr/contracts/`, `src/widgetware_sdr/tools/`, `src/widgetware_sdr/agents/qualification_agent.py`, `tests/`
- **Expected behavior:** every qualification result is schema-valid, every decisive claim carries an evidence reference, invalid output never silently passes as a guess
- **Tests that must pass:** schema validation tests, business invariant tests, tool tests
- **Submission:** one full contract output (JSON) for a qualified account, with evidence references visibly traceable to tool calls
- **Constraints:** tools remain read-only; no send action, no CRM write — still Book 1's standing boundary from Class 1

## Golden solution: `class-05/`

Adds `contracts/`, the four internal tools, and their tests on top of `class-04/`. README highlights the Chapter 6 checkpoint's own framing: "This contract will become the interface between agents and workflow stages" — the payoff for that claim starts in Class 7.

## Bridge to Class 6

Class 6 takes the agent outside WidgetWare's own trusted data for the first time — evidence-backed external research through MCP, where retrieved content must be treated as untrusted until validated.
