# Testing strategy

Test contracts at stable semantic boundaries. This is practical synthesis,
not an official Normand test pyramid. Layers need neither matching test folders
nor fixed test ratios.

| Boundary | Useful evidence |
| --- | --- |
| Calculation | Table of values and expected decisions; properties when an invariant warrants them. No I/O or mocked domain logic. |
| Adapter | Real isolated storage/protocol semantics: transactions, framing, serialization, replacement, and error propagation. |
| Composition | Meaningful effects and outcomes through controlled dependencies; order where it protects the contract. |
| Integration / end to end | Representative production components joined through a real public boundary, catching assumptions that isolated tests share. |

**Stable-interface tests, independent oracles, boundary fakes, fault injection,
property-based testing** are the anchors; choose them by the failure they expose.
Do not equate a unit with a function or test every new private helper.

## Greenfield and existing tests

For greenfield, derive contract cases with the first working vertical slice;
use pure tests for decisions and real boundary tests for effects.
For brownfield, retain characterization and regression cases while moving
behavior. Add direct calculation tests, but keep effect tests at the boundary
that still owns persistence, recovery, and cancellation. A private hook may be
a useful fault-injection seam: retarget it rather than losing the failure case
or making it public merely for tests.

## Make edge cases explicit

For applicable categories—empty/missing, exact boundary, contradictory state,
scale, ordering/concurrency, partial failure—distinguish **tested**, **excluded
by a type or constraint**, **not applicable (why)**, and **unresolved**.
Use this during design/review, not as a mandatory new report artifact. A claimed
constraint must actually hold at the relevant trust boundary.

Ask whether a plausible wrong implementation would fail the test. Expected
results need an independent basis; reproducing the implementation is not an
oracle. Pure tests cannot establish storage durability, and two compatible
fakes cannot establish real integration.

## Traps

- Treat ordering as observable when it enforces persistence-before-acknowledgement,
  transaction boundaries, or another promise; otherwise avoid private call traces.
- Exercise required partial-write, ambiguous-commit, restart, and stale-snapshot
  cases through the component that owns them. A small shell can carry large risk.
- For async coordination prefer events and controlled clocks; retain a generous
  watchdog for hangs. Distinguish a test watchdog from a product timeout.
- Do not delete regression coverage because a helper moved. Do not preserve a
  bad interface solely because tests name it. Move tests with behavior.

Use the project's existing iteration and release gates; this skill adds no
mandatory tools, coverage floor, or separate QA pipeline.
