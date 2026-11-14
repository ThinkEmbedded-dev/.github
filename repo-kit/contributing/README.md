# CONTRIBUTING kit

Every repository of the organization inherits the general
[`CONTRIBUTING.md`](../../CONTRIBUTING.md). Give a repository its own file only when it needs
extra rules: a repository-level `CONTRIBUTING.md` **replaces** the inherited one, so the template
here starts with a link back to the general rules.

1. Copy `CONTRIBUTING.md` (just the header with the link) into the root of the repository.
2. Append the modules that apply:

   | Module | For repositories that ... |
   |---|---|
   | `branching-gitflow.md` | use `main` + `develop` (and the on-develop labeler) |
   | `branching-simple.md` | work on `main` through pull requests only |
   | `firmware.md` | contain firmware for microcontrollers |
   | `hardware-kicad.md` | contain KiCad projects |

   ```sh
   cat CONTRIBUTING.md branching-gitflow.md firmware.md hardware-kicad.md > ../my-repo/CONTRIBUTING.md
   ```

3. Add anything specific to the repository by hand.
