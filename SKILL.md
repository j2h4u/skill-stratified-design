---
name: stratified-design
description: Use when a project or task adopts stratified design for greenfield work or brownfield refactoring into coherent semantic layers with small interfaces.
---

# Stratified design

Think of a system as a stack of small languages. At each level, meaningful
operations combine primitives from lower levels; those operations become the
vocabulary of the next level. A reader should understand an operation without
mentally executing its lower-level mechanics. The payoff is local reasoning
and local change, not a particular directory tree or fewer lines.

Normand's four anchors: **straightforward implementation, abstraction barrier,
minimal interface, comfortable layers**. Stratification concerns semantic
levels; **actions / calculations / data** concern effects. These are separate
axes: actions can be stratified, and purity alone does not create useful layers.

- For the mental model, greenfield/brownfield workflows, and design traps,
  read [design.md](references/design.md).
- When designing or migrating tests, read [testing.md](references/testing.md).
- For exact classic wording, consult [the attributed verbatim SICP excerpt](references/sicp-verbatim.md).
- For author material and optional tooling, consult [sources-and-tools.md](references/sources-and-tools.md).

Use the local guide without repeating introductory web research. Discover
layers from the problem; do not impose a fixed stack or turn every helper into
a layer. Preserve the agreed scope and behavioral guarantees. Extra records
and lines are acceptable when they reduce what a reader must keep in mind.
