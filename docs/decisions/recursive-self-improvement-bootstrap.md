# Recursive Self-Improvement Bootstrap — 2026-09-23

## Purpose

Bootstrap bounded learning infrastructure in Design-bim-Spec using patterns studied from `almensu/yanghoo-reference`.

## Source-derived patterns adopted

The source repository separates durable memory into:
- changelog: what actually changed;
- Gotchas: repeated/high-cost failure patterns;
- evolution loop: where a lesson should land;
- recursive self-improvement protocol: what evidence is required before claiming L1/L2 improvement.

It also emphasizes:
- preserve failure evidence before hardening;
- pair negative regression cases with valid positive controls;
- route entrypoints to focused references instead of duplicating rules;
- later-task use is required to show reusable benefit;
- rewriting the improvement process alone is not recursive improvement.

## Local adaptation

Design-bim-Spec applies those ideas specifically to:
- multimodal design recognition;
- DRS geometry/topology;
- provenance;
- attention;
- style tokens;
- Human/Machine synchronization;
- semantic integrity.

Normal DRS generation remains non-mutating and ends at specification.

Repository evolution occurs only under an explicit maintenance task.

## Baseline

Before this change the repository had:
- thin SKILL / references architecture;
- canonical JSON Schema;
- examples;
- output contract.

It did not yet have:
- persistent Gotcha memory;
- post-task evolution routing;
- an improvement evidence template;
- L0/L1/L2 claim boundaries;
- changelog rules for measured-vs-unmeasured improvement.

## Claim boundary

This bootstrap is **learning infrastructure**, not proof that DRS accuracy has improved.

Current strongest claim:

> L0: the repository now has a bounded mechanism for recording and evaluating future improvements.

No L1 claim is made because a later unseen design task has not yet demonstrated benefit from this mechanism.

No L2 claim is made because the modified improvement mechanism has not yet participated in two connected improvement cycles under stable external evaluation.

## Next valid evidence

A future L1 candidate should:
1. capture a real DRS failure;
2. preserve baseline output;
3. make the smallest rule/guard change;
4. test the known failure plus a valid control;
5. use the change on a later design task not used for tuning;
6. compare outcome and cost;
7. record the result with `references/improvement-record-template.md`.

Only then should the changelog claim measured reusable benefit.
