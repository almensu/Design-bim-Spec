# Improvement Record Template

Use one record per improvement hypothesis.

Do not fill this template with a success story after the fact. Freeze the important evaluation fields before comparing the candidate when possible.

## Metadata

- Record ID:
- Date:
- Maintainer:
- Claim target: L0 / L1 candidate / L2 candidate
- Status: proposed / running / accepted / rejected / inconclusive / rolled_back

## Problem Evidence

- Task/material type:
- Input snapshot or stable reference:
- Baseline repository revision:
- Baseline DRS spec_version:
- Baseline output/evidence:
- User/downstream correction:
- Failure category:
  - material
  - geometry
  - topology
  - provenance
  - attention
  - style
  - serialization
  - semantic_integrity
  - routing
  - improvement_mechanism

## Hypothesis

What single change is expected to improve what measurable behavior?

## Candidate

- Candidate revision:
- Changed files:
- Explicitly unchanged surfaces:
- Why this is the smallest useful intervention:

## Evaluation Contract

### Dataset / tasks
- Discovery sample(s):
- Regression sample(s):
- Held-out or later real task(s):

### Metrics / rubric
- Primary metric:
- Secondary metric:
- Minimum useful gain:
- Maximum allowed cost increase:
- Non-regression invariants:

### Evaluator
- Evaluator/rubric version:
- Human reviewer, validator, downstream consumer, or mixed:
- Was evaluator changed during this experiment? yes/no

## Raw Results

Record all candidates, not only the winner.

| Run | Revision | Task | Result | Cost | Regression? | Notes |
|---|---|---|---|---|---|---|

## Decision

- accepted / rejected / inconclusive / rolled_back
- evidence:
- limitations:
- what cannot be claimed:

## Learning Landing

Choose the smallest justified landing:
- no durable change
- Gotcha
- checklist
- focused reference
- schema
- validator
- regression fixture
- SKILL routing
- changelog
- retirement/split

Paths changed:

## Later-task Verification

- Which later task consumed the change?
- Was it unseen during candidate tuning?
- Baseline comparison:
- Candidate comparison:
- Did the benefit persist?
- New failure modes?

## Recursive Mechanism Lineage

Only for L2 candidates:

- Improvement mechanism old revision:
- Improvement mechanism new revision:
- How did the new mechanism produce/select/validate the next improvement?
- Next-generation candidate:
- External acceptance result:
- Budget comparison:

## Rollback

- Stable revision:
- Rollback steps:
- Evidence that must be preserved:

## Final Claim

Write the strongest claim actually supported:

- L0 current issue repaired
- L1 reusable improvement supported for the recorded task class
- L2 bounded recursive improvement supported under the recorded conditions
- evidence insufficient; candidate only
