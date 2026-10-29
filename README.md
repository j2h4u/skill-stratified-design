# Stratified design agent skill

A concise guide to software as a stack of semantic languages: a mental model,
greenfield and brownfield workflows, test strategy, and refactoring traps.
Based on SICP and Eric Normand's practical treatment in *Grokking Simplicity*.

Start with [SKILL.md](SKILL.md). It routes to focused references; the
[verbatim SICP excerpt](references/sicp-verbatim.md) is for source verification,
not required reading on every task. The skill has no runtime dependencies.

## Install locally

For agents that discover skills in `~/.agents/skills`:

```bash
git clone https://github.com/j2h4u/skill-stratified-design.git ~/repos/j2h4u/skill-stratified-design
mkdir -p ~/.agents/skills
ln -s ~/repos/j2h4u/skill-stratified-design ~/.agents/skills/stratified-design
```

The destination must not already exist. If the skill is already installed,
reconcile its contents before replacing it. Edit and update the repository;
the symlink makes the same files available to local agents without a copy step.
Agent discovery and reload behavior depend on the host application.

## Sources and licensing

[Sources and optional tools](references/sources-and-tools.md) distinguishes
primary sources, our synthesis, and adjacent skill research. Optional analyzers
are references, not installed dependencies or required gates.

Original guidance is [MIT licensed](LICENSE). The attributed SICP excerpt
retains its separate **CC BY-SA 4.0** license; see its source and licensing
notice. Linked external works retain their respective licenses.
