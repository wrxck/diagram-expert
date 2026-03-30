# /diagram:readme

Analyse a project and improve its README with detailed Mermaid diagrams.

## Usage

```
/diagram:readme [path]
```

- `/diagram:readme` — Analyse current project
- `/diagram:readme ./packages/api` — Analyse a specific subproject

## Flow

### 1. Read the existing README

```bash
# Check for README
ls README.md readme.md README.MD 2>/dev/null
```

If no README exists, tell the user: "No README found. Want me to create one with diagrams?"

### 2. Detect git provider

```bash
git remote get-url origin 2>/dev/null
```

Determine Mermaid support (GitHub/GitLab/Azure DevOps = native, Bitbucket = limited).

### 3. Analyse the project

Use the **codebase-analyzer** agent to understand:
- Project type (web app, API, CLI, library, monorepo)
- Architecture (frontend/backend split, microservices, monolith)
- Key components and their relationships
- Database models and relationships
- API endpoints and flows
- Deployment setup (Docker, CI/CD)
- Dependencies and integrations

### 4. Identify diagram opportunities

For each area, assess whether a diagram would genuinely help understanding:

| Project aspect | Diagram type | When to suggest |
|----------------|-------------|-----------------|
| Overall architecture | Flowchart (TD) | Always — every project benefits from this |
| API request flow | Sequence diagram | If the project has API endpoints |
| Database schema | ERD | If there are database models (3+ entities) |
| Component hierarchy | Flowchart or class | If frontend with 5+ components |
| Deployment/infra | Flowchart | If Docker/CI/CD configs exist |
| State management | State diagram | If clear state machines exist |
| Data pipeline | Flowchart (LR) | If data processing/ETL exists |

### 5. Present proposals to the user

Do NOT silently modify the README. Present each proposal:

```
I've analysed your project and found these opportunities to improve the README:

1. **Architecture Overview** — Your project has a React frontend, Express API, and PostgreSQL database. A high-level architecture diagram would help new contributors understand the structure.

2. **API Request Flow** — The auth flow (login → JWT → refresh) involves 4 services. A sequence diagram would make this clearer than the current text description.

3. **Database Schema** — You have 8 models with relationships. An ERD would replace the current bullet-point list of models.

Which of these would you like me to add? (all / 1,2 / none)
```

### 6. Generate approved diagrams

For each approved diagram:
1. Read `${CLAUDE_PLUGIN_ROOT}/skills/diagram-expert/references/mermaid-patterns.md`
2. Generate the Mermaid diagram
3. Show it to the user for approval
4. On approval, edit the README:
   - Add or update the appropriate section heading
   - Insert the diagram with a brief text introduction
   - Preserve all existing content — only add, never remove

### 7. README section placement

Follow this order when adding sections:
1. Title + badges (existing)
2. One-line description (existing)
3. **Architecture** ← diagrams go here
4. Features (existing)
5. Getting Started / Installation (existing)
6. Usage / API (existing)
7. **Database Schema** ← ERD goes here if relevant
8. Contributing (existing)
9. Licence (existing)

If the README doesn't follow this structure, insert diagrams after the description/overview section.
