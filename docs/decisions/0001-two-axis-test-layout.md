---
status: accepted
date: 2026-06-14
---

# Owed tests and earned tests are laid out on different axes

Backfilled on 2026-11-12 from one of my projects, where this was decided on the date above, when the rule became a standard.

## Context and Problem Statement

An architecture with a functional core and adapters around it creates a fixed set of things to verify per slice: the assembled slice through its entry point, the pure mappings at the transport, and the adapters against real-ish infrastructure. These tests are owed: every slice has them, whether or not its logic is hard. The hard logic worth a fast, targeted unit test can sit in any layer, so those tests are earned, one by one. One directory axis cannot express both "what coverage is owed" and "where the hard bit lives" without lying about one of them.

How are the two kinds of test laid out?

## Considered Options

- A single axis: mirror the source tree, or the unit/integration/e2e pyramid
- Two levels on two axes: owed tests cut by architectural role, unit tests cut by source location

## Decision Outcome

Chosen option: two levels on two axes. Owed tests are grouped by what they cover, unit tests by where their subject lives. The two axes are not unified.

A single axis lost because it forces the mandatory set and the supplementary set into one taxonomy, and an empty directory becomes ambiguous: a test owed and missing, or nothing to test. On two axes, an empty directory for an owed test means the test is owed and missing, and a directory for unit tests has to be earned.

### Consequences

- Good, because what a slice still owes is visible from its directories, and an empty one is a marker of the debt.
- Bad, because the same signal means opposite things on the two levels: an empty directory for an owed test is kept, one for unit tests is forbidden. A project using the layout has to say so where its tests live.
- Bad, because proving that a fake matches its real adapter, and tests through the real transport, sit outside this layout and stay open.
- Neutral, because the nesting is for readers. Whether it is free depends on the test runner: one that discovers tests wherever they sit pays nothing for it.
