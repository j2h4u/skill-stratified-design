# SICP: verbatim primary-source excerpt

**Work:** *Structure and Interpretation of Computer Programs*, second edition,
Harold Abelson and Gerald Jay Sussman, with Julie Sussman.
**Section:** 2.2.4, “Levels of language for robust design”.
**Edition:** Source Academy comparison sources, retaining original Scheme wording
and the JavaScript alternatives by Martin Henz and Tobias Wrigstad.

- [Readable section](https://sicp.sourceacademy.org/chapters/2.2.4.html).
- [Exact source revision and file](https://github.com/source-academy/sicp/blob/6ffbe026a461092cf358a8f8658dd0313c634daa/xml/chapter2/section2/subsection4.xml).
- [Publisher-maintained attribution and licensing](https://github.com/source-academy/sicp/blob/6ffbe026a461092cf358a8f8658dd0313c634daa/README.md#license).
- [CC BY-SA 4.0](https://creativecommons.org/licenses/by-sa/4.0/); [source license](https://raw.githubusercontent.com/source-academy/sicp/6ffbe026a461092cf358a8f8658dd0313c634daa/LICENSE).

This file contains all five prose blocks under the source subheading.
The excerpt ends before the exercise. It is not the complete chapter or book.
The XML fragment matches the linked source byte for byte.
It keeps the original markup, index entries, and language alternatives.

We added the attribution and the Markdown fence.
The fragment and its presentation here use CC BY-SA 4.0.
The other references contain our own guidance, not verbatim book text.

Fragment SHA-256: `0375833ffccdd9d955fef28f9e75127bc7784968912626af898c4f21c4122ca5`.

Read this file for comparison with the exact source text.
For task guidance, use [Design](design.md) and [Testing](testing.md).

```xml
  <SUBHEADING>
    <NAME>Levels of language for robust design</NAME>
  </SUBHEADING>

  <SHORT_PAGE lines="2"/>
  <TEXT>
    The picture language exploits some of the critical ideas we<APOS/>ve
    introduced about abstraction with
    <SPLITINLINE>
      <SCHEME>procedures</SCHEME>
      <JAVASCRIPT>functions</JAVASCRIPT>
    </SPLITINLINE>
    and data.  The fundamental data abstractions, painters, are implemented
    using
    <SPLITINLINE>
      <SCHEME>
        procedural
      </SCHEME>
      <JAVASCRIPT>
        functional
      </JAVASCRIPT>
    </SPLITINLINE>
    representations, which enables the language to handle different basic
    drawing capabilities in a uniform way.  The means of combination satisfy
    the closure property, which permits us to easily build up complex designs.
    Finally, all the tools for abstracting
    <SPLITINLINE>
      <SCHEME>procedures</SCHEME>
      <JAVASCRIPT>functions</JAVASCRIPT>
    </SPLITINLINE>
    are available to us for abstracting means of combination for painters.
  </TEXT>

  <TEXT>
    We have also obtained a glimpse of another crucial idea about languages and
    program design.  This is the approach of
    <INDEX>stratified design</INDEX>
    <INDEX>design, stratified</INDEX>
    <EM>stratified design</EM>, the notion that a complex system should be
    structured as a sequence of levels that are described using a sequence of
    languages. Each level is constructed by combining parts that are regarded
    as primitive at that level, and the parts constructed at each level are
    used as primitives at the next level.  The language used at each level
    of a stratified design has primitives, means of combination, and means
    of abstraction appropriate to that level of detail.
  </TEXT>

  <TEXT>
    Stratified design pervades the engineering of complex systems.  For
    example, in computer engineering, resistors and transistors are
    combined (and described using a language of analog circuits) to
    produce parts such as and-gates and or-gates, which form the
    primitives of a language for digital-circuit design.<FOOTNOTE>
    Section<SPACE/><REF NAME="sec:circuit-simulator"/> describes one such
    language.</FOOTNOTE> These parts are combined to build
    processors, bus structures, and memory systems, which are in turn
    combined to form computers, using languages appropriate to computer
    architecture.  Computers are combined to form distributed systems,
    using languages appropriate for describing network interconnections,
    and so on.
  </TEXT>

  <TEXT>
    As a tiny example of stratification, our picture language uses primitive
    elements (primitive painters) that specify points and lines to provide the
    shapes of a painter like <SCHEMEINLINE>rogers</SCHEMEINLINE>. The bulk of
    our description of the picture language focused on combining these
    primitives, using geometric combiners such as
    <SCHEMEINLINE>beside</SCHEMEINLINE> and <SCHEMEINLINE>below</SCHEMEINLINE>.
    We also worked at a higher level, regarding
    <SCHEMEINLINE>beside</SCHEMEINLINE> and <SCHEMEINLINE>below</SCHEMEINLINE>
    as primitives to be manipulated in a language whose operations, such as
    <SPLITINLINE>
      <SCHEME><SCHEMEINLINE>square-of-four</SCHEMEINLINE>,</SCHEME>
      <JAVASCRIPT><JAVASCRIPTINLINE>square_of_four</JAVASCRIPTINLINE>,
      </JAVASCRIPT>
    </SPLITINLINE>
    capture common patterns of combining geometric combiners.
  </TEXT>

  <TEXT>
    Stratified design helps make programs
    <INDEX>robustness</INDEX>
    <EM>robust</EM>, that is, it makes
    it likely that small changes in a specification will require
    correspondingly small changes in the program.  For instance, suppose we
    wanted to change the image based on <SCHEMEINLINE>wave</SCHEMEINLINE>
    shown in figure<SPACE/><REF NAME="fig:sqlimit-designs"/>.  We could work
    at the lowest level to change the detailed appearance of the
    <SCHEMEINLINE>wave</SCHEMEINLINE> element; we could work at the middle
    level to change the way
    <SPLITINLINE>
      <SCHEME><SCHEMEINLINE>corner-split</SCHEMEINLINE></SCHEME>
      <JAVASCRIPT><JAVASCRIPTINLINE>corner_split</JAVASCRIPTINLINE></JAVASCRIPT>
    </SPLITINLINE>
    replicates the <SCHEMEINLINE>wave</SCHEMEINLINE>; we could work at the
    highest level to change how
    <SPLITINLINE>
      <SCHEME><SCHEMEINLINE>square-limit</SCHEMEINLINE></SCHEME>
      <JAVASCRIPT><JAVASCRIPTINLINE>square_limit</JAVASCRIPTINLINE>
      </JAVASCRIPT>
    </SPLITINLINE>
    arranges the four copies of the corner. In general, each level of a
    stratified design provides a different vocabulary for expressing the
    characteristics of the system, and a different kind of ability to change it.
  </TEXT>

```
