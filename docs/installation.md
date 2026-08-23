# Installation Guide

## Quick Install

### Option 1: Global (All Projects)

Copy the files to your global Gemini config directory:

```bash
# Clone the repo
git clone https://github.com/kais-aljammal/reliability-guard.git
cd reliability-guard

# Copy rule (always-on)
cp rules/reliability-core.md ~/.gemini/config/rules/reliability-core.md

# Copy skill (on-demand)
cp -r skills/reliability-research ~/.gemini/config/skills/reliability-research
```

### Option 2: Per-Project (Single Workspace)

Copy the files to your project's `.agents` directory:

```bash
# From your project root
mkdir -p .agents/rules .agents/skills

# Copy rule
cp path/to/reliability-guard/rules/reliability-core.md .agents/rules/reliability-core.md

# Copy skill
cp -r path/to/reliability-guard/skills/reliability-research .agents/skills/reliability-research
```

### Option 3: Rule Only (Lightweight)

If you only want the core anti-fabrication rules without the research
methodology:

```bash
cp rules/reliability-core.md ~/.gemini/config/rules/reliability-core.md
```

This gives you the always-on fabrication prevention with zero on-demand
overhead.

---

## Verify Installation

After installation, start a new conversation with your AI agent and ask:

```
What customizations are active?
```

You should see `reliability-core` in the rules and `reliability-research` in the
available skills.

You can also test with a fabrication-prone question:

```
What's the `maxRetries` parameter in the native fetch() API?
```

The agent should correctly state that `fetch()` does not have a `maxRetries`
parameter, rather than inventing documentation for it.

---

## File Locations Reference

### Global Config (applies to all projects)

```
~/.gemini/config/
├── rules/
│   └── reliability-core.md          # Always-on behavioral rules
└── skills/
    └── reliability-research/
        └── SKILL.md                 # On-demand research methodology
```

### Per-Project (applies to one workspace)

```
your-project/
└── .agents/
    ├── rules/
    │   └── reliability-core.md
    └── skills/
        └── reliability-research/
            └── SKILL.md
```

---

## Updating

Pull the latest version and re-copy the files:

```bash
cd reliability-guard
git pull
cp rules/reliability-core.md ~/.gemini/config/rules/reliability-core.md
cp -r skills/reliability-research ~/.gemini/config/skills/reliability-research
```

---

## Uninstall

Remove the files:

```bash
rm ~/.gemini/config/rules/reliability-core.md
rm -rf ~/.gemini/config/skills/reliability-research
```
