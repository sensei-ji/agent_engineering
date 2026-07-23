# Agent Engineering with Gemini, ADK & Antigravity — Instructor Course

A ten-class, cumulative delivery of the Gemini edition of this series — two hours per class, same instructional rhythm every class, one running WidgetWare SDR Lab codebase from Class 1 to the enterprise capstone in Class 10.

This directory is the instructor's companion to the manuscript in [`../book-1-Foundations/`](../book-1-Foundations/) and [`../book-2-Advanced-Architectures/`](../book-2-Advanced-Architectures/). It does not replace either book — it sequences them into a live, cohort-paced program with a fixed classroom cadence, a golden-solution checkpoint per class, and a three-level homework pattern.

## Start here

- [`00_Course_Framework.md`](00_Course_Framework.md) — the fixed cadence, the learning loop, the golden-solution specification, the homework pattern, and the slide/Kahoot/testing cadences that apply to every class without exception.

## The ten classes

| Class | Manuscript source | Main capability | Materials |
| ----: | ------------------ | ---------------------------------------------------------- | --- |
| [1](classes/class-01/) | Book 1, Ch. 1 | Agent Engineering foundations and the WidgetWare specification | ✅ full |
| [2](classes/class-02/) | Book 1, Ch. 2 | Antigravity workspace and repository harness | ✅ full |
| [3](classes/class-03/) | Book 1, Ch. 3 | Gemini context and instruction architecture | ✅ full |
| [4](04_Class_04.md) | Book 1, Ch. 4–5 | First ADK agent and reusable Skill | narrative only |
| [5](05_Class_05.md) | Book 1, Ch. 6–7 | Structured outputs and tool engineering | narrative only |
| [6](06_Class_06.md) | Book 1, Ch. 8 | MCP and evidence-backed research | narrative only |
| [7](07_Class_07.md) | Book 1, Ch. 9 | Multi-agent workflow and human approval | narrative only |
| [8](08_Class_08.md) | Book 1, Ch. 10–11 | Evaluation, deployment, and bounded loops | narrative only |
| [9](09_Class_09.md) | Book 2, Ch. 2–8 | Memory, RAG, A2A, identity, and governance (survey) | narrative only |
| [10](10_Class_10.md) | Book 2, Ch. 9–10 | AgentOps, optimization, and capstone | narrative only |

Classes 1–8 track Book 1 at close to a one-to-one pace, closing the book at Class 8. Class 9 is an explicit survey — it covers seven Book 2 chapters at landscape depth but keeps the hands-on build to one capability (Memory Bank), because a two-hour class cannot build seven platform capabilities and a ten-class program is an accelerated path through Book 2, not a substitute for reading it. Class 10 closes with Book 2's own capstone chapter and the course's final assignment.

Classes with **full** materials have their own folder under [`classes/`](classes/) containing the narrative lesson plan, slides, Kahoot questions, homework, and a verified, runnable golden-solution checkpoint. Classes marked **narrative only** currently exist just as the flat lesson-plan file linked above (`0N_Class_0N.md`) — the same content that will move into `classes/class-0N/lesson-plan.md` once that class's full materials are built.

## What you need before Class 1

- The manuscript itself, both books, for reference during lecture prep.
- Kahoot (or an equivalent live-quiz tool) set up for the 0:55–1:05 segment.
- A shared conventions document for participants: Python version, package manager, how `.env.example` works, and how to submit homework artifacts.
- Nothing to seed for Class 1 itself — `classes/class-01/golden-solution/` is the from-scratch starting point, and each subsequent class's golden solution builds on the previous one cumulatively.

## A note on scope

This program does not invent a different pedagogy from the manuscript — it applies the manuscript's own "probabilistic reasoning inside deterministic boundaries" discipline to the classroom itself. The cadence is deterministic and fixed; what participants build with it is where the reasoning happens.
