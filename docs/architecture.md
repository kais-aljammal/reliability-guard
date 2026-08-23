# Architecture

## Design Philosophy

Reliability Guard uses a **rule + skill** split architecture. This is an
intentional design decision optimized for how modern AI agent systems load
instructions.

---

## Why Two Layers?

AI agent platforms distinguish between two types of instructions:

- **Rules** — loaded into the agent's context on every interaction. They
  cannot be skipped. Best for behavioral constraints that must always apply.
- **Skills** — loaded on-demand when the agent determines they are relevant.
  Best for detailed methodologies that only apply to certain tasks.

Anti-fabrication rules must **always** be active — you never want an agent that
fabricates in some conversations but not others. That makes them rules. Research
methodology, however, is only relevant during research, verification, or
fact-checking tasks. Loading it during routine coding or creative writing wastes
context window for no benefit. That makes it a skill.

```
┌─────────────────────────────────────────────────────────────┐
│                     Agent Context Window                     │
├─────────────────────────────────────────────────────────────┤
│                                                             │
│  ┌─────────────────────────────────────────────────────┐    │
│  │  reliability-core.md (Rule)          ~80 lines      │    │
│  │  ✓ Always loaded                                    │    │
│  │  ✓ Anti-fabrication rules                           │    │
│  │  ✓ Efficiency guardrails                            │    │
│  │  ✓ Minimal context cost                             │    │
│  └─────────────────────────────────────────────────────┘    │
│                                                             │
│  ┌ ─ ─ ─ ─ ─ ─ ─ ─ ─ ─ ─ ─ ─ ─ ─ ─ ─ ─ ─ ─ ─ ─ ─ ─ ┐   │
│    reliability-research/SKILL.md (Skill) ~200 lines         │
│  │ ○ Loaded on-demand                                  │   │
│    ○ Research methodology                                   │
│  │ ○ Evidence policy, source matching                  │   │
│    ○ Only when research is needed                           │
│  └ ─ ─ ─ ─ ─ ─ ─ ─ ─ ─ ─ ─ ─ ─ ─ ─ ─ ─ ─ ─ ─ ─ ─ ─ ┘   │
│                                                             │
└─────────────────────────────────────────────────────────────┘
```

---

## Layer Details

| Layer | File | Type | Loaded | Purpose | Size |
|:------|:-----|:-----|:-------|:--------|:-----|
| **Core** | `rules/reliability-core.md` | Rule | Always | Behavioral constraints that prevent fabrication, false certainty, and unsupported claims | ~80 lines |
| **Research** | `skills/reliability-research/SKILL.md` | Skill | On-demand | Methodology for research, verification, evidence evaluation, and conflict resolution | ~200 lines |

---

## What Goes Where?

**Core Rule (always-on):**

- Never fabricate information
- Challenge doubtful user premises
- Distinguish fact from inference
- Never pretend a tool succeeded
- Don't manufacture certainty
- Efficiency guardrails
- Host system integration

**Research Skill (on-demand):**

- Step-by-step verification procedure (A → B → C → D → E)
- Evidence and source matching policy
- Uncertainty and abstention guidelines
- Recommendation methodology
- Code and calculation reliability
- User-provided file handling
- Source conflict resolution
- Output behavior guidelines

---

## Design Principles

1. **Separation of concerns.** Rules define *what* the agent must never do.
   Skills define *how* to do research well.

2. **Minimal context cost.** The always-on rules are compact (~80 lines). The
   full methodology (~200 lines) is loaded only when needed.

3. **Correct loading semantics.** Rules cannot be skipped. Skills can be
   activated selectively. Anti-fabrication rules belong in the "cannot skip"
   category.

4. **Composability.** Either layer can be used independently. The core rules
   work without the research skill. The research skill is enhanced by the core
   rules but doesn't strictly require them.
