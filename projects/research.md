---
name: project-research
description: Researches similar projects, open-source implementations, libraries, APIs, and architectural patterns at project kickoff. Produces concise findings in .cursor/research.md without writing code. Use when starting a new project, greenfield work, stack selection, architecture discovery, or when the user asks for project research, tech survey, or options analysis.
---

# Project Research

Research-only workflow for the start of a project. **Do not write, edit, or scaffold application code.** The only file you may create or update is `.cursor/research.md`.

## Before you search

1. Read the user's goal, constraints, and stack preferences from the conversation and any existing project docs (`README`, `AGENTS.md`, `.cursor/rules`, prior `research.md`).
2. If scope is unclear, ask one focused question (platform, scale, must-use tech, timeline) before searching.
3. Define 3–6 research questions tied to the project (e.g. auth approach, data store, deployment target).

## What to search for

Use web search and official docs. Cover as relevant:

| Category | Look for |
|----------|----------|
| Similar projects | Products or repos solving the same problem |
| Open source | Mature repos, license, maintenance, adoption |
| Libraries | SDKs and packages that fit constraints |
| APIs | Hosted services, pricing model, rate limits |
| Patterns | Architecture, folder structure, infra patterns |

Prefer primary sources: official docs, GitHub repos, release notes. Cross-check claims when sources conflict.

## Hard rules

- **Never write code** — no implementation files, configs, scripts, tests, or boilerplate.
- **Only output file**: `.cursor/research.md` (create `.cursor/` if missing).
- **No secrets** — do not paste API keys or credentials into research.
- Stay concise; skip generic advice the team already knows.

## Update `.cursor/research.md`

- If the file exists, **merge**: keep still-valid findings, update changed items, mark superseded options.
- If new, create from the template below.
- End with a short **Recommendations** section: 1–3 concrete next steps (e.g. "Prototype X first", "Avoid Y because Z").

### Document template

```markdown
# Project Research

**Project:** [one-line goal]
**Researched:** [YYYY-MM-DD]
**Questions:** [bulleted list of what you investigated]

## Executive summary

[2–4 sentences: top options and suggested direction]

## Findings

### [Finding title — e.g. "Supabase vs custom Postgres"]

**Summary:** [1–2 sentences]

**Advantages:**
- ...

**Disadvantages:**
- ...

**Links:**
- [Name](https://...)

**Relevance:** [How this applies to this project; fit/misfit with stated constraints]

---

[Repeat ### block per finding]

## Recommendations

1. ...
2. ...

## Open questions

- [Items that need a product or technical decision from the user]
```

Each finding is one `###` section. Group related items (e.g. all auth options) only when it keeps the doc shorter without losing clarity.

## Quality bar

- **Actionable**: every finding should inform a decision, not pad the doc.
- **Honest tradeoffs**: advantages and disadvantages must be specific to this project, not marketing copy.
- **Relevance required**: if something is a poor fit, say why in **Relevance** instead of omitting it.
- **Links**: at least one authoritative link per finding; prefer docs and repos over blog spam.
- Cap at **~8–12 findings** unless the user asks for exhaustive coverage; link out for depth.

## Workflow checklist

```
- [ ] Clarify project goal and constraints
- [ ] Run targeted searches (projects, OSS, libs, APIs, patterns)
- [ ] Draft findings with summary / pros / cons / links / relevance
- [ ] Write or update .cursor/research.md
- [ ] Add Recommendations and Open questions
- [ ] Confirm: no code was written
```

## Example finding (abbreviated)

### TanStack Query for server state

**Summary:** Client library for caching, syncing, and updating async server data in React apps.

**Advantages:**
- Mature ecosystem; reduces bespoke fetch/cache code
- Devtools and stale-while-revalidate fit dashboard UIs

**Disadvantages:**
- Learning curve for cache keys and invalidation
- Less value if the app is mostly static or SSR-only with no client mutations

**Links:**
- [TanStack Query docs](https://tanstack.com/query/latest)

**Relevance:** Strong fit if the app is a React SPA with many API-backed lists and forms; skip if you standardize on React Server Components only with no client mutations.
