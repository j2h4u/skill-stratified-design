# Mental model and development procedures

## Semantic layers

Each layer has **primitives, means of combination, and means of abstraction**.
An operation from one layer becomes a primitive for a higher layer.
For example, byte operations support framed records. Framed records support
recording intervals. Recording intervals support a recording that is ready
for publication. These are examples of languages, not required modules.

An abstraction barrier hides details that callers do not need.
A different name for the same details does not create a barrier.
One module can contain several semantic layers. One layer can use several modules.

Normand describes four patterns in *Grokking Simplicity*, chapters 8 and 9.

| Pattern | Design question |
| --- | --- |
| Straightforward implementation | Does the operation use a consistent level of detail? |
| Abstraction barrier | Can callers use the operation without knowing its data representation? |
| Minimal interface | Can callers express their needs through a small set of operations? |
| Comfortable layers | Do the layers make the work easier, without unnecessary steps? |

Operations outside a minimal interface can combine its basic operations.
An additional wrapper is useful only if it hides details or expresses a useful concept.

## Effects and information

**Actions, calculations, and data** are separate from semantic layers.
Actions depend on when or how often they run.
Calculations produce results from explicit inputs without side effects.
They do not change their inputs.
Data records facts or plans.

A database client argument does not make a function pure.
A clock function argument does not make a function pure.
Give time values to pure calculations. Use a controlled clock in code that
performs effects when tests need control of time.

General operations that change infrequently usually support specific rules
that change more often. Consider a business-rule change and a data-representation
change. Identify the callers and tests that each change affects.
This comparison shows whether changes stay within suitable boundaries.
It does not require a fixed number of files or layers.

## Greenfield: new software

1. Identify the scenarios, invariants, and operations that callers need.
2. Identify effects, transaction boundaries, and required operation order.
3. Implement one useful operation with its lower-level primitives.
4. Separate calculations when this makes decisions easier to understand.
5. Do tests of a complete path through the new behavior.
6. Add operations and layers as actual use requires them.

Do not select a framework or layer count before the problem requires it.
See [testing.md](testing.md) for the test strategy.

## Brownfield: existing or poorly understood code

1. Find actual callers, effects, and failure-recovery behavior.
2. Do tests of uncertain behavior before a change.
3. Select one complete path through the existing behavior.
4. Use an existing operation with a useful semantic boundary.
   Add one only when needed.
5. Move behavior and tests together.
6. Update callers where the interface changes.
7. Evaluate the design with the two change examples above.
8. Continue through the agreed scope after evaluation of the pilot.

The pilot provides feedback. It does not automatically limit the agreed scope.

## Traps and edge cases

**False barriers.** A wrapper that only forwards calls can leave all details
with the caller. A helper that receives an existing decision might hide no
useful behavior. A boolean predicate can still express a useful concept.

**Reads that occur too early.** Reading all inputs first can change error order,
memory use, and I/O cost. Keep conditional reads and stream behavior where
required. Do not add parsing or hash passes only to match a diagram.

**Changed error handling.** Some read errors require an unknown result.
Others require a retry or a fatal error. Moving a read across an exception
handler can change this behavior. Keep the required error handling and read order.

**Stale data.** Data can change between a read and the use of a decision.
Keep required checks, atomic operations, durability, and cancellation behavior.

**Effects that remain complex.** Code that performs effects can own retries,
backpressure, partial failures, and recovery. Few lines do not make this code
safe. Hide internal details without removing required operation order.
When you move effects into a helper, keep required resource lifetimes and
cleanup order.

**Data representation.** Keep opaque identifiers opaque. Keep conversion and
validation behavior. Use a record when related values need an explicit contract.
Avoid copies of mutable state without a clear owner.
