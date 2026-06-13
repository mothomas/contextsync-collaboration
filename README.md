# ContextSync Collaboration Repo

Shared **team brain** for ContextSync. This repo holds what the team agrees on — roles, contracts, decisions, workflows — plus the relationship graph that links intent to code in your product repo.

Clone this alongside your product repo and point the ContextSync MCP server at both paths.

## Folder structure

```
contextsync-collaboration/
├── README.md                     # This file
│
├── identity/
│   └── roles.md                  # Team roles, scopes, AI boundaries
│
├── contracts/
│   └── example-schema.md         # API / schema / interface definitions
│
├── decisions/
│   ├── ADR-template.md           # Template for architecture decision records
│   └── handoffs/                 # Agent handoff packets (auto-written)
│       └── .gitkeep
│
├── playbooks/
│   └── workflow.md               # How the team works with ContextSync
│
├── skills/
│   └── approved-skills.md        # AI capabilities approved for this team
│
└── graph/
    └── graph.json                # Auto-maintained relationship graph
```

## What each folder is for

| Folder | Contents | Who updates it |
|--------|----------|----------------|
| `identity/` | Role definitions — scope, boundaries, owned contracts, AI instructions | Team lead / architects |
| `contracts/` | Interface definitions (API, gRPC, events, data schemas) | Contract owners |
| `decisions/` | ADRs and handoff notes | Anyone via `update_graph` / `handoff` MCP tools |
| `playbooks/` | Team workflow rules (when to call get_context, validate, etc.) | Team lead |
| `skills/` | Allowed AI skill boundaries for this project | Team lead |
| `graph/` | Machine-readable links between all of the above + product code | ContextSync (auto) |

## File conventions

### Roles — `identity/roles.md`

One section per role:

```markdown
## [Role Name]
- Scope: what this role owns
- Boundaries: what it must not touch
- Contracts owned: list
- Notified when: triggers
- AI instructions: guidance for agents in this role
```

### Contracts — `contracts/[name].md`

```markdown
# Contract: [Name]
## Type       API | gRPC | Data Schema | Event | Interface
## Version    1.0.0
## Owner      [Role]
## Definition  [schema]
## Consumers   [roles/components]
## Change Protocol
```

### Decisions — `decisions/ADR-[number]-[title].md`

Copy from `ADR-template.md`. Link related contracts under **Related Contracts**.

### Graph — `graph/graph.json`

Do not edit by hand unless bootstrapping. ContextSync maintains nodes and edges:

- **Nodes** — files in this repo or the product repo (`intent`, `decision`, `contract`, `code`, …)
- **Edges** — `satisfies`, `implements`, `owned_by`, `depends_on`, `notifies`, …

## How it connects to your product repo

```
┌─────────────────────────┐         ┌─────────────────────────┐
│  contextsync-collaboration │         │     product repo        │
│  (this repo)            │         │  (your application)     │
│                         │         │                         │
│  contracts/  ───────────┼─ satisfies ──►  src/api/...     │
│  decisions/  ───────────┼─ implements ──►  src/...        │
│  graph/graph.json ◄─────┼──────── ContextSync MCP ────────┤
└─────────────────────────┘         └─────────────────────────┘
```

ContextSync reads contracts and decisions here, maps them to files in the product repo, and flags drift or violations in CI.

## Getting started

1. Clone this repo next to your product repo.
2. Edit `identity/roles.md` for your team.
3. Add real contracts under `contracts/` (remove or replace the example).
4. Configure ContextSync to point at both repo paths.
5. Run `sync-graph` (when available) to bootstrap `graph/graph.json`.

## Example layout on disk

```
~/Projects/
├── contextsync/                    # MCP server
├── contextsync-collaboration/      # this repo
└── my-product/                     # your app
```

## Status

Template repo — populate `identity/`, `contracts/`, and `decisions/` for your team. The seed `graph/graph.json` links the example contract to the Backend Engineer role.
