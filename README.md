# diagram-expert

[![CI](https://github.com/wrxck/diagram-expert/actions/workflows/ci.yml/badge.svg)](https://github.com/wrxck/diagram-expert/actions/workflows/ci.yml)

A Claude Code plugin that generates detailed, accurate Mermaid diagrams from your codebase and improves READMEs with visual documentation.

## What it does

- Analyses your project structure, database models, API flows, and deployment config
- Generates Mermaid diagrams that render natively on GitHub, GitLab, and Azure DevOps
- Identifies where your README could benefit from diagrams and proposes improvements
- Always asks before making changes

## Installation

```bash
claude plugin marketplace add wrxck/claude-plugins
claude plugin install diagram-expert@wrxck-claude-plugins
```

## Commands

### `/diagram <description>`

Generate a Mermaid diagram from a description or by analysing your codebase.

```
/diagram architecture
/diagram sequence for the auth flow
/diagram erd
/diagram deployment
```

### `/diagram:readme [path]`

Analyse a project and suggest README improvements with diagrams.

```
/diagram:readme
/diagram:readme ./packages/api
```

## Supported diagram types

| Type | Mermaid keyword | Best for |
|------|----------------|----------|
| Flowchart | `graph TD/LR` | Architecture, deployment, data pipelines |
| Sequence | `sequenceDiagram` | API flows, auth chains, multi-service interactions |
| ERD | `erDiagram` | Database schemas, data models |
| State | `stateDiagram-v2` | Order flows, document lifecycles |
| Class | `classDiagram` | Service interfaces, component APIs |
| Gantt | `gantt` | Project timelines |
| Gitgraph | `gitgraph` | Branching strategies |
| Pie | `pie` | Proportional breakdowns |

## Git provider support

| Provider | Mermaid support |
|----------|----------------|
| GitHub | Native rendering |
| GitLab | Native rendering |
| Azure DevOps | Native rendering |
| Bitbucket | No native support (plugin offers alternatives) |

## Agents

The plugin includes two specialised agents:

- **codebase-analyzer** -- Read-only agent that analyses project structure, dependencies, and flows
- **readme-improver** -- Reviews READMEs and proposes diagram improvements (always asks first)

## Licence

MIT
