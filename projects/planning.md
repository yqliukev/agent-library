---
name: project-planning
description: Plans projects and records broad architectural decisions in spec.md, splitting work into distinct implementation steps. Use when starting a new project, defining architecture, scoping phases, writing a project spec, or when the user asks for project planning, roadmap, or high-level design before implementation.
---

# Project Planning

Planning-only workflow. **Do not write, edit, or scaffold application code.** The only file you may create or update is `spec.md` at the project root (unless the user specifies another path).

## Inputs

Before planning, read:

1. The user's goal, constraints, and preferences from the conversation
2. Existing project docs: `README`, `AGENTS.md`, `.cursor/rules`, prior `spec.md`
3. `.cursor/research.md` if it exists — treat its recommendations as starting points, not final decisions

If research is missing and stack or approach is still wide open, suggest running project research first. Do not block planning on it unless the user wants research done first.

## Scope of this skill

**In scope (broad):**

- Project goal and success criteria
- Major components and how they interact
- Technology choices at the category level (e.g. "Postgres", "React SPA", "REST API")
- Data flow, deployment target, auth model, integration boundaries
- Splitting work into ordered, distinct steps for later implementation

**Out of scope (defer to implementation agents):**

- File structure, class names, API route shapes
- Library versions, config values, error message copy
- Test strategy details, CI pipeline steps, lint rules
- Step-internal design (schemas, component trees, algorithms)

When a decision is too detailed for this stage, record it under the relevant step as **Deferred decisions** for the implementing agent.

## When to ask the user

Ask **only when needed** — do not questionnaire every choice upfront.

| Ask when | Skip when |
|----------|-----------|
| Two or more viable approaches with meaningful tradeoffs for *this* project | One option clearly fits stated constraints |
| A missing constraint would change component boundaries or tech category | Detail can safely default to common practice and be reversed later |
| Build vs buy, hosted vs self-hosted, or similar product-level forks | Choice is an implementation detail inside an already-agreed boundary |
| User preference matters and is not inferable from prior messages | Research or spec already documents the decision |

**How to ask:**

- One focused question (or a small set of tightly related options) at a time
- Present 2–4 options with brief tradeoffs tied to the project — not generic pros/cons
- After the user answers, update `spec.md` and continue; do not re-ask settled items

If several decisions are independent, you may batch them in one message. If decisions depend on each other, resolve the blocking one first.

## Workflow

```
- [ ] Read goal, constraints, and existing docs (including research.md)
- [ ] Identify architectural decision points still open
- [ ] Ask user for clarification only where needed
- [ ] Define broad architecture (components, boundaries, key tech categories)
- [ ] Split project into distinct, ordered steps
- [ ] Write or update spec.md
- [ ] Confirm: no application code was written
```

### Splitting into steps

Each step should be:

- **Distinct** — one coherent slice of work (e.g. "Auth and user model", not "Auth + billing + admin UI")
- **Implementable** — a future agent can execute it using this spec without re-planning the whole project
- **Ordered** — note dependencies; later steps may depend on earlier ones
- **Broad** — outcome described, not file-by-file instructions

Per step, include:

- **Goal** — what exists when the step is done
- **Scope** — what's in and out
- **Depends on** — step IDs or "none"
- **Deferred decisions** — detailed choices left to the implementing agent

Target **3–8 steps** for most projects. Split further only if the user asks or complexity clearly requires it.

## Hard rules

- **Never write code** — no implementation files, configs, scripts, tests, or boilerplate
- **Only output file**: `spec.md` (create or merge; preserve still-valid content when updating)
- **Broad decisions only** — push detail to step-level **Deferred decisions**
- **No secrets** — do not paste API keys or credentials into the spec

## Update spec.md

- If the file exists, **merge**: keep valid decisions, update changed items, mark superseded sections
- If new, create from the template below
- Write for **both humans and agents**: clear headings, stable step IDs, explicit constraints

### Document template

```markdown
# Project Spec

**Project:** [one-line goal]
**Status:** [draft | approved]
**Last updated:** [YYYY-MM-DD]

## Goal

[What we're building and why — 2–4 sentences]

## Success criteria

- [Measurable or verifiable outcomes]

## Constraints

- [Hard limits: platform, timeline, budget, compliance, must-use/must-avoid tech]

## Architecture overview

[High-level description: major components, data flow, deployment. A simple diagram in mermaid is optional but helpful.]

### Key decisions

| Decision | Choice | Rationale |
|----------|--------|-----------|
| [e.g. Database] | [e.g. Postgres] | [Why, tied to project constraints] |

## Steps

### Step 1: [Short title]

**ID:** `step-1`
**Goal:** [Outcome when complete]
**Scope:** [In scope / out of scope bullets]
**Depends on:** none

**Deferred decisions:**
- [Detail for implementing agent to resolve]

---

### Step 2: [Short title]

**ID:** `step-2`
**Goal:** ...
**Scope:** ...
**Depends on:** `step-1`

**Deferred decisions:**
- ...

## Open questions

- [Unresolved items needing user input before or during implementation]

## References

- [Links to research.md, external docs, or prior art — optional]
```

Use stable step IDs (`step-1`, `step-2`, …) so implementation agents and issues can reference them.

## Quality bar

- **Actionable**: every section should guide a developer or agent; avoid filler
- **Honest tradeoffs**: recorded decisions include rationale, not buzzwords
- **Separation of concerns**: architecture here, implementation detail in **Deferred decisions**
- **Stable**: prefer renaming sections over duplicating conflicting content when updating

## Handoff to implementation

When a step is ready to build, the implementing agent should read:

1. This `spec.md` (full context)
2. The specific step section (scope and deferred decisions)
3. `.cursor/research.md` if relevant to that step

Do not re-litigate broad decisions locked in **Key decisions** unless the user explicitly changes direction.