# Architecture checks

## Python: Tach

This skill is used mainly with Python. Use [Tach](https://docs.gauge.sh/)
to enforce the selected module boundaries. It supports individual Python
files and packages. Keep an existing suitable checker when the project has one.

Select semantic operations and their interfaces first. Express the permitted
imports in the project's `tach.toml`. Set source roots to match the project's
import paths. Review which files the configuration covers.

Use [dependency rules](https://docs.gauge.sh/usage/configuration/) to restrict
imports between modules. Use [public interfaces](https://docs.gauge.sh/usage/interfaces/)
to restrict access to implementation details. Optional
[layers](https://docs.gauge.sh/usage/layers/) can enforce dependency direction
when the module structure matches the selected semantic layers.

Run `tach check`. Use `tach check --exact` when the contract must also reject
declared dependencies that the code no longer uses. Keep the configuration
with the code. Run the check during refactoring and in the project's normal
validation workflow.

Review changes from `tach sync`: it can add existing imports to the permitted
dependencies. Do not approve an unwanted dependency only to make the check pass.
See the [command reference](https://docs.gauge.sh/usage/commands/).

A dependency check enforces the declared architecture. Review semantic
usefulness through callers and change examples from [design.md](design.md).
Keep behavior tests from [testing.md](testing.md). One module can still contain
several semantic layers.

## Other languages

The design principles also apply to other languages. Use a suitable dependency
or architecture checker for that language and build system. Prefer existing
project tooling. Check that it covers the relevant imports and interfaces.
Keep the same separation between semantic design, structural checks, and
behavior tests. This skill does not require a particular tool for every language.
