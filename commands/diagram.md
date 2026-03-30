# /diagram

Generate a Mermaid diagram from a description or by analysing the current codebase.

## Usage

```
/diagram <description or type>
```

Examples:
- `/diagram architecture` — Architecture overview of the current project
- `/diagram sequence for the auth flow` — Sequence diagram for authentication
- `/diagram erd` — Entity-relationship diagram from database models
- `/diagram deployment` — Deployment/infrastructure diagram
- `/diagram data flow from API to UI` — Data flow for a specific path

## Flow

### 1. Determine diagram type

If the user specified a type, use it. Otherwise, infer from context:

| Context clue | Suggested type |
|--------------|----------------|
| Database models, schemas, Prisma/Drizzle/TypeORM files | Entity-Relationship (erDiagram) |
| API endpoints, request handling | Sequence diagram |
| Component hierarchy, imports | Class or flowchart |
| Docker, nginx, deployment configs | Deployment/architecture (C4 or flowchart) |
| State machines, status fields | State diagram |
| CI/CD, pipelines | Flowchart (LR) |
| Git branching strategy | Gitgraph |
| Timeline, roadmap | Timeline or Gantt |

### 2. Detect git provider

```bash
git remote get-url origin 2>/dev/null
```

- `github.com` / `gitlab` / `dev.azure.com` → Use fenced Mermaid blocks
- `bitbucket.org` → Warn user that Bitbucket doesn't render Mermaid natively; offer to generate a mermaid.live link or SVG alternative
- No remote → Default to fenced Mermaid blocks

### 3. Analyse the codebase

Use the **codebase-analyzer** agent to:
- Read relevant source files (models, routes, components, configs)
- Extract relationships, dependencies, and flows
- Build a mental model of the system

Do NOT read the entire codebase. Target files relevant to the requested diagram type.

### 4. Generate the diagram

Read `${CLAUDE_PLUGIN_ROOT}/skills/diagram-expert/references/mermaid-patterns.md` for syntax patterns.

Rules:
- Use descriptive node IDs, not single letters (e.g., `AuthService` not `A`)
- Add meaningful labels on edges
- Group related nodes with subgraphs where it helps clarity
- Keep diagrams readable — split into multiple diagrams if >30 nodes
- Use appropriate direction: TD for hierarchies, LR for flows/sequences
- Include a title using `---` frontmatter or `accTitle`

### 5. Present to user

Show the diagram in a fenced code block:

````markdown
```mermaid
graph TD
    ...
```
````

Ask: "Want me to add this to a file (e.g., README.md, docs/architecture.md), or iterate on it?"

### 6. If adding to a file

- Check if the target file exists
- If adding to README.md, find an appropriate section (## Architecture, ## Overview, etc.)
- If no section exists, suggest adding one
- Use the Edit tool — never rewrite the whole file
