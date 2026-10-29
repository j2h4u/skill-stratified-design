# Sources and optional tools

## Primary sources

The [local author notes](author-notes.md) summarize the explanations below.
They give examples and source locations without external research.

- SICP, section 2.2.4: [Example: A Picture Language](https://sicp.sourceacademy.org/chapters/2.2.4.html).
  Its subsection, “Levels of language for robust design”, describes the sequence of languages.
  The [local excerpt](sicp-verbatim.md) includes the exact text, attribution, and license.
- Eric Normand, *Grokking Simplicity*: [chapter 8](https://livebook.manning.com/book/grokking-simplicity/chapter-8/)
  and [chapter 9](https://livebook.manning.com/book/grokking-simplicity/chapter-9/).
  These chapters describe the four design patterns.
- Normand's [Stratified design and functional architecture slides](https://ericnormand.me/slides/Stratified-design-and-functional-architecture.pdf).
  These slides connect semantic layers, change frequency, purity, and onion architecture.
- Normand on [calculations](https://ericnormand.me/podcast/what-is-a-calculation)
  and [stratified design](https://ericnormand.me/podcast/more-about-stratified-design).
- Normand's [interview about Grokking Simplicity and stratified design](https://ericnormand.me/speaking/grokking-simplicity-stratified-design-functional-programming-does-not-compute-podcast)
  explains domain levels and comfortable layers.
- Normand on [extraction and testability](https://livebook.manning.com/book/grokking-simplicity/chapter-4/page_85).

SICP gives a classic description. Normand gives practical patterns.
These sources do not establish a sole inventor or a universal test procedure.
Only the licensed SICP excerpt contains verbatim source text.
Other author material remains available through links.
The design and test guides contain our own guidance.

## Optional tool

[dundalek/stratify](https://github.com/dundalek/stratify) provides Python dependency
maps, call maps, and graph metrics. Its README identifies architecture checks
as work in progress. No local test results are available.

A graph can show dependencies. It cannot establish that semantic layers are
useful. Extra wrappers can increase graph depth without a better design.
Before a trial, do a check of current support. A reference to this tool does not
require installation or an additional project check.

## Related skills

[fluencer-ai/devmode testing-principles](https://github.com/fluencer-ai/devmode/blob/main/skills/testing-principles/SKILL.md)
provided the idea for explicit edge-case results in [testing.md](testing.md).
Its [functional-core-imperative-shell skill](https://github.com/fluencer-ai/devmode/blob/main/skills/functional-core-imperative-shell/SKILL.md)
describes the separation of decisions from effects.
It does not describe the complete stratified-design model.

We copied no passages from these skills. Neither skill is a dependency.
Reading all inputs first can change behavior. A small effectful component
can still need important tests. See [design.md](design.md).

## Language standard

[ASD-STE100 Simplified Technical English](https://www.asd-ste100.org/)
is the writing standard for our original guidance.
Domain terms and the authors' pattern names remain technical names.
Verbatim source text and standard license text keep their original wording.
