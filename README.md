# Workflow library

System-provided workflows, agents and rules for [Devel Central](https://develcentral.com).

In Devel Central, open a board column's **Workflow** menu and pick one under **Default workflows**,
or use **Apply default workflows** on a new board. Either way the organization gets its own copy of
the workflow, the agent that runs it and any rules that target them. A copy is fully editable and
never changes when this repository does; the next pick copies whatever is here then.

The app reads the `main` branch through `raw.githubusercontent.com`, which caches files for about
five minutes, so a change merged here shows in the picker within a few minutes.

## Namespaces

| Folder | Shown as | Workflows |
| --- | --- | --- |
| [`default/`](default/) | Default workflows | Scoping, Design, Plan, Implement, Review, Merge |

Each top-level folder holding a `namespace.json` is a namespace in this layout. Devel Central shows
only `default/` today, as the Default workflows group; a new namespace folder does not appear in the
picker yet.

## Layout

```
<namespace>/
  namespace.json
  workflows/<workflow>/
    workflow.json
    stages/<file>.md
  agents/<agent>/
    agent.json
    instructions/<file>.md
  rules/<file>.md
```

Folder names under `workflows/` and `agents/` are keys: lowercase letters, digits and dashes
(`implement`, `software-engineer`). Workflows and rules refer to each other by these keys. Every
`file` path is relative to the JSON file that names it, ends in `.md` and stays inside the
namespace (no `..`). Markdown bodies are copied as written, trimmed of surrounding blank lines.

### namespace.json

```json
{
  "name": "Default workflows",
  "workflows": ["scoping", "design", "plan", "implement", "review", "merge"],
  "rules": [
    { "name": "Ship small", "file": "rules/ship-small.md", "appliesTo": "workflows", "targets": ["implement"] }
  ]
}
```

| Field | Required | Meaning |
| --- | --- | --- |
| `name` | yes | The group's title in the picker. |
| `workflows` | yes | Workflow keys, in the order the picker lists them. A workflow folder not listed here is ignored. |
| `rules` | no | Rules that target workflows or agents of this namespace; see below. Defaults to none. |

### workflows/&lt;workflow&gt;/workflow.json

```json
{
  "name": "Implement",
  "description": "Build the ticket as scoped and designed upstream.",
  "agent": "software-engineer",
  "model": "opus",
  "permissions": "auto",
  "stages": [
    { "name": "Understand", "file": "stages/1-understand.md" },
    { "name": "Build", "file": "stages/2-build.md" }
  ]
}
```

| Field | Required | Meaning |
| --- | --- | --- |
| `name` | yes | The workflow's name. When the organization already has one by that name, the copy is named "Implement (Default)", then "Implement (Default 2)". |
| `description` | no | One paragraph: what the workflow is for. |
| `agent` | yes | The key of the agent under `agents/` that runs it. Several workflows may share one agent; applying them all copies that agent once. |
| `model` | no | `inherit` (the member's Settings default, the default), an alias such as `opus` or `sonnet`, or a full model ID. |
| `permissions` | no | `auto` (the default) or `ask`. Auto needs a model that can run it. |
| `stages` | yes | At least one, in order. Each stage's Markdown says what the agent does in it. |

### agents/&lt;agent&gt;/agent.json

```json
{
  "name": "Software Engineer",
  "description": "Builds changes in the codebase.",
  "instructions": [
    { "name": "Software Engineer: working discipline", "file": "instructions/working-discipline.md" }
  ]
}
```

| Field | Required | Meaning |
| --- | --- | --- |
| `name` | yes | The agent's name; a taken name gets the same "(Default)" suffix as a workflow. |
| `description` | no | One paragraph: who the agent is. |
| `instructions` | no | The agent's own instructions, in order. Every session the agent runs gets them. |

### Rules

A rule is Markdown in `rules/`, listed in `namespace.json` with the workflows or agents it targets:

| Field | Required | Meaning |
| --- | --- | --- |
| `name` | yes | The rule's name. |
| `file` | yes | Its Markdown, relative to the namespace folder. |
| `appliesTo` | yes | `workflows` or `agents`. |
| `targets` | yes | Workflow keys or agent keys of this namespace. |

A rule is copied with any workflow or agent it targets, and targets only the copies made in that
pick. The copy belongs to the member who made it, like any rule they write. Organization-wide rules
(ones that apply to every session) are not part of a library.

## Adding a workflow by hand

1. Make `default/workflows/<key>/workflow.json` and its stage files.
2. Name an existing agent key, or add `default/agents/<key>/agent.json` with its instructions.
3. Add the key to `workflows` in `default/namespace.json`, where it should appear in the list.
4. Merge to `main`. Within a few minutes the workflow shows under Default workflows in every
   column's Workflow menu.

If any file is missing or does not follow this layout, the app says Default workflows cannot be
reached, so check the JSON and every `file` path before merging.
