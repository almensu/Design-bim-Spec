# Changelog

All notable changes to Design-bim-Spec are recorded here.

This file is the English source of truth. The Simplified Chinese mirror is `CHANGELOG.zh-CN.md`.

The repository release version and the DRS `spec_version` are separate version axes. A schema version such as `0.1.0` does not by itself mean that the repository has published a `v0.1.0` release.

## [Unreleased]

### Added
- Added a thin-`SKILL.md` / thick-`references/` architecture for multimodal design reconstruction.
- Added the canonical DRS JSON Schema, material taxonomy, visual-analysis protocol, layout constraints, attention model, style tokens, output contract, and example Human/Machine specifications.
- Added repository learning infrastructure derived from `yanghoo-reference`: a Gotchas memory, evolution loop, bounded recursive self-improvement protocol, improvement record template, DRS output review checklist, and a bootstrap decision record.
- Added bilingual changelog maintenance rules so durable repository changes are recorded from evidence rather than aspiration.

### Changed
- Routed normal DRS execution through relevant Gotchas and the DRS output review before acceptance.
- Separated normal specification generation from repository self-improvement: ordinary runs still end at Human View + Machine View + STOP; repository mutation requires an explicit maintenance task.
- Added lifecycle and evidence rules so a documentation change is not automatically treated as proven improvement.

### Fixed
- Kept detailed execution rules out of `SKILL.md` and moved them into focused references, preventing the main skill file from becoming a handbook.
