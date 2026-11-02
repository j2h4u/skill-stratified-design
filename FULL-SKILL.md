---
name: stratified-design
description: Use Stratified Design (SICP; Eric Normand, Grokking Simplicity) to design new code or refactor existing code into semantic layers.
---

# Stratified Design

A system has a sequence of semantic layers. Each layer has a language for its
level of detail. Operations combine primitives from lower layers. These
operations become primitives for the next layer. This structure helps readers
understand and change one layer without following all lower-level details.

Apply this approach first within functions and modules. It also applies to
larger structures. It supports hexagonal architecture, layered architecture,
and domain-driven design. It does not require their replacement.

Normand names four patterns: **straightforward implementation, abstraction
barrier, minimal interface, comfortable layers**. Semantic layers describe
levels of meaning. **Actions, calculations, and data** describe effects and
information. These distinctions are separate. Actions can have semantic layers.
Pure functions alone do not create useful layers.

- For the mental model and development procedures, read [design.md](references/design.md).
- For test strategy and test changes, read [testing.md](references/testing.md).
- For a complete before-and-after refactor, read [worked-example.md](references/worked-example.md).
- For architecture checks with Python and other languages, read [architecture-checks.md](references/architecture-checks.md).
- For local author explanations and examples, read [author-notes.md](references/author-notes.md).
- For the exact source text, read [the SICP excerpt](references/sicp-verbatim.md).
- For author material and optional tools, read [sources-and-tools.md](references/sources-and-tools.md).
- For installation and licenses, read [README.md](README.md).

Use these local references for normal work. Do not repeat basic web research.
Select layers from the problem. Do not prescribe a folder structure or make
every helper a layer. Keep the agreed scope and required behavior. More lines
and records are acceptable when they make the code easier to understand.

## Brownfield boundary review

Use these signals to select boundaries for review. They are not automatic
defects. Evaluate the knowledge that callers need and the behavior to preserve.

| Signal | Review question |
| --- | --- |
| A caller imports an internal name from another module. | Does the caller need a stable operation instead of this implementation detail? |
| A lower semantic layer imports a higher-level concept. | Does the dependency direction match the intended levels of meaning? |
| Configuration, transport, encoding, and orchestration share a module. | Are their boundaries clear to callers? One module can contain several useful layers. |
| An adapter reads configuration files or environment variables. | Does it own that input boundary? Can tests control those inputs without unrelated services? |
| Imports occur inside function bodies. | Are the dependencies included in architecture checks? Is deferred loading required? |
| A wrapper only forwards arguments or an existing decision. | Which representation detail or rule can its caller now ignore? |

Keep required effect order, exception handling, and resource ownership when
you change a boundary. Use the procedures in [design.md](references/design.md)
and the [worked example](references/worked-example.md) for the next step.

## Writing rules

Use **ASD-STE100 Simplified Technical English** for all original text in this
skill, including its references. Use short sentences, direct instructions,
and consistent technical terms. Keep Cyrillic characters out of file names
and contents. Keep verbatim source text and standard license text unchanged.
