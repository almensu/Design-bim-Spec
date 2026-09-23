# Changelog Maintenance

## Purpose

This reference defines how Design-bim-Spec records durable repository changes.

A changelog is not a marketing page and is not a task diary. It is a structured release/change record grounded in repository evidence.

## Required files

- `CHANGELOG.md` — English source of truth.
- `CHANGELOG.zh-CN.md` — natural Simplified Chinese mirror.

Update English first, then synchronize Chinese semantics. Do not translate mechanically sentence by sentence.

## Evidence rule

Only record changes that actually landed in the repository or in an explicitly identified candidate revision.

Good evidence:
- changed file paths;
- commit/diff evidence;
- schema/reference changes that can be read back;
- new examples or validators;
- a recorded maintenance decision.

Do not write future intentions as completed changes.

## Section vocabulary

Use only sections that contain entries:

| Type | English | Chinese |
|---|---|---|
| capability | Added | 新增 |
| bug correction | Fixed | 修复 |
| behavior/default | Changed | 调整 |
| documentation | Docs | 文档 |
| refactor | Refactored | 重构 |
| removal | Removed | 移除 |
| deprecation | Deprecated | 废弃 |
| breaking | Breaking Changes | 破坏性变更 |

## Unreleased first

New durable changes enter `[Unreleased]` first.

A repository release section is created only when a maintainer intentionally versions a release.

## Two version axes

Do not confuse:

1. repository release version, such as `v0.2.0`;
2. DRS machine-contract `spec_version`, such as `0.1.0`.

A schema-only version change does not automatically create a repository release, and a documentation-only repository release does not automatically require a DRS schema version bump.

## Improvement claims

Changelog wording must distinguish:
- infrastructure added;
- rule changed;
- bug fixed;
- improvement measured.

Do not write “improved accuracy” merely because a prompt/reference changed.

Use language such as:
- “Added a guard for …”
- “Changed the routing for …”
- “A later-task comparison showed …”

Only the last form claims measured benefit and requires an improvement record.

## Relation to learning

- Failure pattern memory → `Gotchas.md`
- How lessons are promoted → `evolution-loop.md`
- Strong claims of reusable/recursive improvement → `recursive-self-improvement-protocol.md`
- Comparable evidence → `improvement-record-template.md`

## One-line principle

Record what changed; do not let the changelog invent proof that the change worked.
