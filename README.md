# ThinkEmbedded-dev/.github

Default community files for every repository of the organization that does not define its own.

| Path | What it does |
|---|---|
| `.github/ISSUE_TEMPLATE/` | Issue templates (Markdown, with issue types) and chooser configuration. **Inherited.** |
| `.github/pull_request_template.md` | Default pull request description. **Inherited.** |
| `CONTRIBUTING.md` | Contribution rules, linked when opening issues and pull requests. **Inherited.** |
| `profile/README.md` | Organization page on github.com/ThinkEmbedded-dev |
| `workflow-templates/` | Workflows offered in *Actions > New workflow* |
| `labels.tsv`, `scripts/sync-labels.sh` | Labels grouped in tiers, and the script that creates them in the repositories you list |
| `repo-kit/` | Files to copy into single repositories |

## Notes

- This repository must stay **public**, otherwise the defaults and workflow templates are not
  applied.
- A repository with **any** file in its own `.github/ISSUE_TEMPLATE/` ignores all the templates
  here. A repository with its own `CONTRIBUTING.md` ignores only the inherited `CONTRIBUTING.md`.
- The issue types used by the templates (Bug, Feature, Task) must exist in
  *Organization settings > Planning > Issue types*.

## Labels

Labels are not inherited. They are defined in `labels.tsv`, grouped in tiers, and created with
`scripts/sync-labels.sh` in the repositories you list. A label set by a template that does not
exist in a repository is simply not applied, so each repository can have only what it needs.

| Tier | Labels |
|---|---|
| `base` | bug, enhancement, task, documentation, testing, question, duplicate, invalid, wontfix, on develop |
| `area` | area: sw, area: fw, area: hw |
| `hw` | hw: next rev |
| `advanced` | needs triage, breaking change, dependencies, do not close |
| `community` | good first issue, help wanted |

### Usage

```text
scripts/sync-labels.sh [--tier TIERS] [--label NAMES] [--dry-run] OWNER/REPO [OWNER/REPO ...]
scripts/sync-labels.sh --list
```

| Option | Meaning |
|---|---|
| `OWNER/REPO ...` | One or more repositories to update. Required, there is no "all repositories" option. |
| `--tier TIERS` | Comma-separated tiers to apply, e.g. `base,area,hw`. |
| `--label NAMES` | Comma-separated label names to apply, e.g. `"on develop,do not close"`. Case-insensitive, can be repeated. |
| `--dry-run` | Print what would be done without changing anything. |
| `--list` | Print every tier with its labels and descriptions, then exit. |
| `-h`, `--help` | Print the help, then exit. |

- `--tier` and `--label` can be combined: their union is applied. With neither, `base` is applied.
- An unknown tier or label stops the script before any change.
- Existing labels get the color and description from the file; labels not in the file are never
  touched or deleted.
- Output is colored by tier in a terminal. `NO_COLOR=1` disables colors, `FORCE_COLOR=1` forces
  them (e.g. `| less -R`). `LABELS_FILE=path` uses another labels file.
- Requires the GitHub CLI (`gh`), logged in with access to the repositories.

### Examples

```sh
scripts/sync-labels.sh --list                                          # tiers and labels
scripts/sync-labels.sh alanmasu/my-repo                                # base tier only
scripts/sync-labels.sh --tier base,area,hw alanmasu/my-board alanmasu/my-fw
scripts/sync-labels.sh --label "on develop,do not close" alanmasu/my-repo
scripts/sync-labels.sh --tier base --label "do not close" --dry-run alanmasu/my-repo
```