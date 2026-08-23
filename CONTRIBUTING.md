# Contributing to Reliability Guard

Thanks for your interest in improving AI agent reliability! Here's how to
contribute effectively.

## How to Contribute

1. **Fork** this repository
2. **Create a branch** for your change (`git checkout -b improve-source-policy`)
3. **Make your changes** following the guidelines below
4. **Add test scenarios** if you're modifying rules or skill behavior
5. **Submit a pull request** with a clear description of what changed and why

## Guidelines

### Keep the Core Rules Compact

Every line in `rules/reliability-core.md` is loaded into the agent's context on
**every interaction**. Lines cost tokens. Be ruthless about conciseness:

- If a rule can be expressed in fewer words without losing meaning, tighten it.
- Do not add examples or explanations to the rule file — put those in the docs.
- Before adding a new rule, check if an existing rule already covers it.

### Maintain the Two-Layer Architecture

- **Rules** = behavioral constraints (what the agent must never do).
- **Skills** = methodology (how to do research well).

Don't move procedural methodology into the rules file, and don't move
non-negotiable constraints into the skill file.

### Add Test Scenarios

If your change affects agent behavior, add one or more test scenarios to
`examples/test-scenarios.md`. Each scenario should include:

- **User prompt** — the example input
- **Expected behavior** — what the agent should do
- **Component** — which rule or skill section handles it
- **Anti-pattern** — what the agent should NOT do

### Writing Style

- Use plain, direct language.
- Prefer actionable instructions over abstract principles.
- When in doubt, read the existing files and match their tone.

## Reporting Issues

Found a failure mode that the rules don't cover? Open an issue with:

1. The prompt that triggered the problem
2. What the agent did (the bad behavior)
3. What it should have done instead

## Code of Conduct

Be respectful and constructive. Focus on improving the framework.
