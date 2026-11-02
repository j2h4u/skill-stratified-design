# Stratified Design agent skill

This skill describes software as a sequence of semantic layers. It gives a
mental model, development procedures, test guidance, and common problems.
Its sources include SICP and Eric Normand's *Grokking Simplicity*.

Start with the outline in [SKILL.md](SKILL.md). If you need more information,
read [the full skill](FULL-SKILL.md). It links to detailed task guidance and
author material in the references.
The [verbatim SICP excerpt](references/sicp-verbatim.md) permits comparison with
the source text. Normal tasks do not require this comparison. The skill has
no runtime dependencies.

## Local installation

These commands install the skill for applications that read `~/.agents/skills`.

```bash
mkdir -p ~/.agents/skills
git clone https://github.com/j2h4u/skill-stratified-design.git ~/.agents/skills/stratified-design
```

The destination directory must not exist. If the skill is already installed,
update its existing checkout.

Update this clone to get new skill versions. The host application controls
skill discovery and reload.

## Sources and licenses

[Sources and optional tools](references/sources-and-tools.md) identifies the
source material and related research. Optional tools are not dependencies
or required checks.

The original guidance uses the [MIT license](LICENSE). The SICP excerpt keeps
its separate **CC BY-SA 4.0** license. Its reference file gives the attribution
and license links. External works keep their own licenses.

## Document changes

Use ASD-STE100 Simplified Technical English for all original guidance.
Keep verbatim source text and standard license text unchanged.
