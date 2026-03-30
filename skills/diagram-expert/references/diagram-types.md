# Diagram Type Selection Guide

Choose the right diagram type based on what you need to communicate.

## Decision Matrix

| What you're showing | Diagram type | Mermaid keyword |
|---------------------|-------------|-----------------|
| System components and how they connect | Flowchart | `graph TD` or `graph LR` |
| Step-by-step interaction between services | Sequence | `sequenceDiagram` |
| Database tables and relationships | ERD | `erDiagram` |
| Object/class structure and methods | Class | `classDiagram` |
| Lifecycle states and transitions | State | `stateDiagram-v2` |
| Project timeline and milestones | Gantt | `gantt` |
| Git branching strategy | Gitgraph | `gitgraph` |
| Proportional breakdown | Pie | `pie` |
| User journey through a system | User Journey | `journey` |
| Requirement traceability | Requirement | `requirementDiagram` |

## When to use each

### Flowchart (`graph`)
**Best for:** Architecture overviews, deployment topology, data pipelines, decision trees.
**Use when:** You need to show how parts of a system relate to each other.
**Direction:** Use `TD` for hierarchies (top-down), `LR` for processes (left-right).

### Sequence Diagram
**Best for:** API call chains, authentication flows, webhook sequences, multi-service interactions.
**Use when:** Time ordering matters — "first this happens, then that."
**Tip:** Keep to 5-6 participants max. Split complex flows into multiple diagrams.

### Entity-Relationship Diagram
**Best for:** Database schema documentation, data model overview.
**Use when:** There are 3+ entities with relationships between them.
**Tip:** Include field types and key constraints. Group related entities visually.

### State Diagram
**Best for:** Order status flows, document lifecycles, UI state machines.
**Use when:** An entity moves through defined states with clear transitions.
**Tip:** Include the trigger/event name on each transition arrow.

### Class Diagram
**Best for:** Service interfaces, component APIs, module structure.
**Use when:** You need to show the public interface of components and their dependencies.
**Tip:** Focus on key methods and relationships, not every field.

### Gantt Chart
**Best for:** Project timelines, sprint planning, release schedules.
**Use when:** Tasks have durations and dependencies.

### Gitgraph
**Best for:** Branching strategies, release workflows.
**Use when:** Documenting git workflow conventions for a team.

## Combining diagrams

For comprehensive documentation, combine multiple types:

1. **Architecture overview** (flowchart) — the 10,000-foot view
2. **Key flows** (sequence) — how the important processes work
3. **Data model** (ERD) — what's stored and how it relates
4. **Deployment** (flowchart) — how it runs in production

This combination covers most questions a new contributor would have.

## Complexity guidelines

| Complexity | Nodes | Recommendation |
|-----------|-------|----------------|
| Simple | 3-10 | Single diagram, no subgraphs needed |
| Medium | 10-20 | Use subgraphs to group related nodes |
| Complex | 20-30 | Consider splitting into overview + detail diagrams |
| Very complex | 30+ | Must split — create a high-level overview and linked detail diagrams |
