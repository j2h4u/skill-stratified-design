# Primary sources and optional tools

## Concept and author material

- SICP, section 2.2.4, [Example: A Picture Language](https://sicp.sourceacademy.org/chapters/2.2.4.html), subsection “Levels of language for robust design”: the classic stack-of-languages formulation. [Verbatim local excerpt, attribution, and license](sicp-verbatim.md).
- Eric Normand, *Grokking Simplicity*, [chapter 8](https://livebook.manning.com/book/grokking-simplicity/chapter-8/) and [chapter 9](https://livebook.manning.com/book/grokking-simplicity/chapter-9/): the four practical patterns.
- Normand's [Stratified design and functional architecture slides](https://ericnormand.me/slides/Stratified-design-and-functional-architecture.pdf): semantic levels, stability, and how stratification relates to purity and onion architecture.
- Normand on [calculations](https://ericnormand.me/podcast/what-is-a-calculation), [stratified design](https://ericnormand.me/podcast/more-about-stratified-design), and [extraction/testability](https://livebook.manning.com/book/grokking-simplicity/chapter-4/page_85).

SICP supplies a classic formulation; Normand supplies practical patterns.
Do not claim a sole inventor or an official universal testing handbook.
Only the licensed SICP fragment is reproduced verbatim locally; other author
materials remain links. The operational guides are our synthesis.

## Optional tooling

[dundalek/stratify](https://github.com/dundalek/stratify) offers Python dependency
and call maps and graph metrics. Its README marks architecture checks as work
in progress. It has not been tried here. Graph structure can expose coupling,
but cannot establish coherent semantic layers; wrappers can improve apparent
graph depth without improving design. Check current support before considering
an isolated trial. No installation or new gate is implied.

## Adjacent skill research

[fluencer-ai/devmode testing-principles](https://github.com/fluencer-ai/devmode/blob/main/skills/testing-principles/SKILL.md)
inspired the explicit edge-case dispositions in [testing.md](testing.md).
Its [functional-core-imperative-shell skill](https://github.com/fluencer-ai/devmode/blob/main/skills/functional-core-imperative-shell/SKILL.md)
covers a related effect boundary, not the full stratified-design model. We
borrow no verbatim passages and require neither skill nor their surrounding
workflow. Read-all-inputs-first and trivial-shell assumptions need the
qualifications in [design.md](design.md).
