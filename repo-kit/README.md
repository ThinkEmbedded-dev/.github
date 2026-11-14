# Repository kit

Files that are **not** inherited from this `.github` repository. Workflows are offered as
**workflow templates** instead: in a repository open *Actions > New workflow* and look for the
section with the organization name.

| File | Copy to | Purpose |
|---|---|---|
| `contributing/` | repository root | Extra rules for a single repository, see [contributing/README.md](contributing/README.md) |
| `.github/dependabot.yml` | `.github/` | Weekly updates of the actions used by the workflows |
| `.github/release.yml` | `.github/` | Categories for generated release notes |
| `kicad.gitignore` | append to `.gitignore` | Files that must not be committed |

Workflows that use the project need the `PROJECT_TOKEN` secret: create it once as an
**organization secret**.
