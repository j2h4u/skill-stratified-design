# Mental model and workflows

## A stack of languages

Each level has **primitives, means of combination, and means of abstraction**.
An operation built at one level becomes a primitive for a higher level.
For example: byte operations → framed records → recording intervals → publishable
recording. These are illustrative vocabularies, not prescribed modules.

Judge a layer by what callers can stop knowing. Renaming low-level mechanics
without hiding them does not create an abstraction barrier. Multiple semantic
levels may fit in one module; one level may span modules.

Normand's four patterns, from *Grokking Simplicity* chapters 8–9:

| Pattern | Design question |
| --- | --- |
| Straightforward implementation | Can this operation be read in a coherent vocabulary, without switching repeatedly between business intent and representation details? |
| Abstraction barrier | Can callers use the operation without knowing the representation beneath it? |
| Minimal interface | Is the barrier's interface small but sufficient, with other operations composed outside it? |
| Comfortable layers | Do these boundaries make actual work easier, or add indirection without reducing reasoning? |

**Actions / calculations / data** are an orthogonal lens. Actions depend on
when or how often they execute; calculations map explicit values to results
without effects; data records facts or plans. Passing a database client or
clock callable as an argument does not make a calculation pure. Pass a time
value to pure rules; inject clocks into effectful coordination where useful.

General, stable operations often sit below specific, frequently changing
policies. Rehearse a policy change and a representation change: which callers
and tests must understand each? This tests locality, without demanding exactly
one changed file or a universally acyclic call graph.

## Greenfield

Start with scenarios, invariants, and the vocabulary callers need. Sketch a
meaningful operation and implement its lower-level primitives as needed.
Extract calculations where decisions become clearer; compose effects around
them while keeping transactions and ordering explicit. Deliver a working
vertical slice with tests at its meaningful boundaries, then grow the
vocabulary from actual use. Avoid speculative frameworks and predetermined
layer counts. Test strategy: [testing.md](testing.md).

## Brownfield, including poorly understood code

Map actual callers, effects, and failure/recovery contracts before choosing
boundaries. Characterize uncertain behavior first. Select a vertical slice,
introduce a useful semantic operation, move behavior and tests together, and
update real callers. Compare the result using the two change rehearsals above.
Continue across the agreed scope after the pilot; a pilot is a feedback step,
not an automatic permanent limit.

## Traps and edge cases

- **False barriers:** pass-through wrappers, renamed mechanics, or a helper
  that accepts an already-made decision. A meaningful boolean predicate can
  still be a good abstraction.
- **Eager extraction:** moving all reads up front changes short-circuiting,
  error order, memory use, and I/O cost. Preserve lazy reads and stream behavior
  where they matter; do not add parsing or hash passes to fit a diagram.
- **Changed error boundaries:** preserve which read errors mean unknown,
  retry, or fatal. Moving a read across a catch changes behavior even if the
  success-path result is identical.
- **Stale plans:** gathering facts and later applying a decision can race.
  Retain required revalidation, atomicity, durability, and cancellation.
- **Over-purification:** orchestration still owns partial effects, retries,
  backpressure, and recovery where applicable. A thin shell is not automatically
  trivial or safe. Hide incidental mechanics, not business-critical sequencing.
- **Representation leaks:** keep opaque identities opaque; preserve conversion
  and validation semantics. DTOs help only when their fields express a useful
  contract rather than mirror mutable state without ownership.
