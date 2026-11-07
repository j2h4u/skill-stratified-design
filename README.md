# Stratified Design agent skill

This skill describes software as a sequence of semantic layers. It gives a
mental model, development procedures, test guidance, and common problems.
Its sources include SICP and Eric Normand's *Grokking Simplicity*.

## What it does

This repository is an experiment in progressive disclosure for agent skills.
A semantic anchor is a short name for a set of concepts. The hypothesis is
that capable models can apply familiar concepts from these names without
loading a full explanation.

[SKILL.md](SKILL.md) is the main entrypoint. It contains an outline of the
concepts and procedures. Start there. If a concept is unclear or the task
needs more guidance, read [the full skill](FULL-SKILL.md). Its links lead to
detailed references and author material. Load that detail only as needed.

Small coding and refactoring trials with Astra, Sol, and Terra found no clear
advantage for the full text. This supports the outline-first format for the
tested tasks. Other models and tasks can still need the full guidance.

The [verbatim SICP excerpt](references/sicp-verbatim.md) permits comparison with
the source text. Normal tasks do not require this comparison. The skill has
no runtime dependencies.

## Install

These commands install the skill for applications that read `~/.agents/skills`.

```bash
mkdir -p ~/.agents/skills
git clone https://github.com/j2h4u/skill-stratified-design.git ~/.agents/skills/stratified-design
```

The destination directory must not exist. If the skill is already installed,
update its existing checkout.

## Update

```bash
git -C ~/.agents/skills/stratified-design pull --ff-only
```

The host application controls skill discovery and whether a reload or new session is needed.

## Use

Ask your agent:

> Use $stratified-design to organize this code into semantic layers with small interfaces.

See [SKILL.md](SKILL.md) for the outline and [FULL-SKILL.md](FULL-SKILL.md) for the full guidance.

## License

[Sources and optional tools](references/sources-and-tools.md) identifies the
source material and related research. Optional tools are not dependencies
or required checks.

The original guidance uses the [MIT license](LICENSE). The SICP excerpt keeps
its separate **CC BY-SA 4.0** license. Its reference file gives the attribution
and license links. External works keep their own licenses.

## Document changes

Use ASD-STE100 Simplified Technical English for all original guidance.
Keep verbatim source text and standard license text unchanged.
