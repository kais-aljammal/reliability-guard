# Architecture

## Why a Two-Layer Design?

The reliability-guard system uses a **rule + skill** split architecture. This is
an intentional design decision, not arbitrary modularization.

### The Problem with a Single File

The original v1.0 was a single 339-line SKILL.md file. This created two issues:

1. **Wrong loading behavior.** Skills are loaded on-demand — the agent decides
   whether to activate them. But anti-fabrication rules should be *always
   active*. A skill can be skipped; a rule cannot.

2. **Context waste.** Loading 339 lines of detailed research methodology on
   every interaction — including routine coding, creative writing, and simple
   questions — consumes context window for no benefit.

### The Solution

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
│    reliability-research/SKILL.md (Skill)  ~200 lines        │
│  │ ○ Loaded on-demand                                  │   │
│    ○ Research methodology                                   │
│  │ ○ Evidence policy, source matching                  │   │
│    ○ Only when research is needed                           │
│  └ ─ ─ ─ ─ ─ ─ ─ ─ ─ ─ ─ ─ ─ ─ ─ ─ ─ ─ ─ ─ ─ ─ ─ ─ ┘   │
│                                                             │
└─────────────────────────────────────────────────────────────┘
```

### Layer Details

| Layer | File | Type | Loaded | Purpose | Lines |
|:------|:-----|:-----|:-------|:--------|:------|
| **Core** | `rules/reliability-core.md` | Rule | Always | Behavioral constraints that prevent fabrication, false certainty, and unsupported claims | ~80 |
| **Research** | `skills/reliability-research/SKILL.md` | Skill | On-demand | Detailed methodology for research, verification, evidence evaluation, and conflict resolution | ~200 |

### What Goes Where?

**Core Rule (always-on):**
- Never fabricate information
- Challenge doubtful user premises
- Distinguish fact from inference
- Never pretend a tool succeeded
- Don't manufacture certainty
- Efficiency guardrails
- Host system integration notes

**Research Skill (on-demand):**
- Step-by-step verification procedure
- Evidence and source matching policy
- Uncertainty and abstention guidelines
- Recommendation methodology
- Code and calculation reliability
- User-provided file handling
- Source conflict resolution
- Output behavior guidelines

### Design Principles

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
