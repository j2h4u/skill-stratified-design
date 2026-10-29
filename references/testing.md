# Test strategy

Do tests of required behavior through stable semantic interfaces. This guidance is
our application of the design principles. It is not an official Normand test
pyramid. Layers do not require matching test folders or fixed test ratios.

| Boundary | Test purpose |
| --- | --- |
| Calculation | Do tests of input values and expected decisions without I/O or mocked domain logic. |
| Adapter | Do tests of actual storage or protocol behavior with isolated resources. |
| Composition | Do tests of effects, outcomes, and required operation order with controlled dependencies. |
| Integration or end to end | Connect real components through a public interface to find incorrect assumptions in isolated tests. |

Useful methods include **stable-interface tests, independent test oracles,
boundary fakes, fault injection, and property-based testing**.
Select a method for the failure it can detect.
A test unit is not necessarily one function.
Do not add separate tests for every private helper.

## New software

Derive test cases from the required behavior of the first complete path.
Do tests of decisions with pure calculations. Do tests of effects at actual system boundaries.
Use isolated resources for tests of storage and protocols.

## Changes to existing tests

Keep characterization and regression cases when behavior moves.
Add direct tests for calculations. Keep effect tests where the code still
controls persistence, recovery, and cancellation.

A private hook can provide useful fault injection. Change the hook when its
boundary moves. Keep the failure case that the test detects.
Do not make a hook public only for tests.
Do not keep a poor interface only because tests use it.

## Edge cases

Consider missing inputs, exact boundaries, contradictory states, scale,
operation order, concurrency, and partial failure.
Give each applicable case one of these results:

- **Tested:** A test confirms the required behavior.
- **Prevented:** A type or constraint prevents the case at the relevant boundary.
- **Not applicable:** The case does not apply, for a stated reason.
- **Unresolved:** The case remains a known gap.

Use these results during design and review. They do not require a separate
report file. Make sure that each stated constraint applies to the actual input.

## Test quality and common problems

Ask whether a likely implementation error would cause the test to fail.
Use an independent basis for expected results. A copy of the implementation
is not an independent test oracle.

Pure tests cannot establish storage durability. Two compatible fakes cannot
establish that real components work together.

Do a check of operation order when it protects a contract. Examples include durable
storage before acknowledgement and transaction boundaries.
Do not add checks of private call order without a required behavior.

Do tests of partial writes, ambiguous commits, restarts, and stale data where the component owns these conditions.
A small component can have important failure behavior.

Use events and controlled clocks for asynchronous tests where possible.
Keep a test timeout that stops a hang. Allow enough time for slow test
resources. A test timeout and a product timeout have different purposes.

Keep existing project checks for development and release.
This skill requires no additional tools, coverage minimum, or QA pipeline.
