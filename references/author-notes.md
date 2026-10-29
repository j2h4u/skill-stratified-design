# Author explanations

These notes summarize Eric Normand's explanations in our own words.
They are not transcripts or copies of his slides. The links give the originals.
Use these notes when the meaning of a semantic layer is unclear, or when you
review this skill against its sources. Normal tasks do not require web research.

## Layers of meaning

Source: [More about Stratified Design](https://ericnormand.me/podcast/more-about-stratified-design).
Published on November 12, 2018. Updated on September 23, 2019.

Normand builds from language operations to more specific concepts.
Higher operations use those concepts to express a solution at a useful level.
His cooking example moves from chemistry to techniques, components, dishes,
and meals. A recipe should not need a description of chemical reactions.

He connects these levels to change frequency. General operations tend to stay
stable while business rules change. Dependencies point toward lower levels.
A business operation that uses language details directly can indicate a
missing concept. This is a design signal, not a required number of layers.

## Effects and architecture

Source: [Stratified design and functional architecture](https://ericnormand.me/slides/Stratified-design-and-functional-architecture.pdf).
Eric Normand, Oredev 2023. Page numbers below count from the first PDF page.

Pages 3-26 distinguish data, calculations, and actions. Pages 54-62 separate
email construction from delivery. The calculation returns an email value.
The action sends it. The example also uses pages of subscribers when the
input is too large to process at once.

Pages 69-77 show semantic levels through cooking, software domains, and string
operations. Pages 78-84 connect these levels and pure calculations to onion
architecture. This combination is more specific than semantic layers alone.
The slides do not make every semantic layer pure or require a folder per layer.

## Comfortable layers

Source: [Grokking Simplicity, Stratified Design and Functional Programming](https://ericnormand.me/speaking/grokking-simplicity-stratified-design-functional-programming-does-not-compute-podcast).
Interview published on March 29, 2021.

The discussion contrasts general array operations with domain concepts such
as prices and sales. A sale operation expressed only through arrays and
objects can omit a useful domain level. It also describes comfortable layers:
keep a design that is easy to work with. More layers do not establish a better
design. Working behavior can come before further design work.

## Application in this skill

The following checks are our application of these explanations.
They are not additional rules from Normand.

For a selected operation, identify the problem it solves and the concepts in
its implementation. Ask which representation or decision its callers can
ignore. A new name alone does not establish that boundary.

Compare a business-rule change with a representation change. Check which
callers and tests each change affects. Keep required effect order, resource
ownership, and failure behavior when code moves. The email example does not
justify reading all inputs before effects in every system.

For the complete procedures, use [design.md](design.md) and
[testing.md](testing.md). For the classic definition, use the
[licensed SICP excerpt](sicp-verbatim.md). For other sources and optional tools,
use [sources-and-tools.md](sources-and-tools.md).
