# Changelog

All notable changes to this project will be documented in this file.

The format is based on [Keep a Changelog](https://keepachangelog.com/en/1.1.0/),
and this project adheres to [Semantic Versioning](https://semver.org/spec/v2.0.0.html).

## [2.0.0] - 2025-08-23

### Changed

- **Breaking:** Split monolithic SKILL.md into two-layer architecture:
  - `rules/reliability-core.md` — always-on behavioral rules
  - `skills/reliability-research/SKILL.md` — on-demand research methodology
- Rewrote all content for clarity and conciseness
- Converted source-matching examples to a structured table
- Fixed em-dash encoding corruption (`—` → proper Unicode)
- Added explicit activation guidance in skill description

### Added

- Comprehensive test scenarios (`examples/test-scenarios.md`)
- Architecture documentation (`docs/architecture.md`)
- Installation guide with multiple deployment options (`docs/installation.md`)
- README with visual design and quick-start guide
- MIT License

### Removed

- Monolithic single-file design
- Redundant prose across sections
- Sections 9 and 10 merged into core rule file as compact guardrails

## [1.0.0] - 2025-08-23

### Added

- Initial release as single SKILL.md file
- 11 sections covering reliability policy
- Non-negotiable rules, runtime procedure, evidence policy
- Uncertainty handling, code reliability, conflict resolution
