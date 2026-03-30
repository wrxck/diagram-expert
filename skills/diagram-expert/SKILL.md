# diagram-expert

Create detailed, accurate Mermaid diagrams for software architecture, data flows, ERDs, sequences, and more. Improve READMEs with visual documentation.

## Routing

| Command | Action |
|---------|--------|
| `/diagram <description>` | Generate a Mermaid diagram from a description or codebase analysis |
| `/diagram:readme [path]` | Analyse a project and suggest README improvements with diagrams |

## Git Provider Support

Mermaid is natively rendered by:
- **GitHub** — fenced code blocks in markdown (```mermaid)
- **GitLab** — fenced code blocks in markdown (```mermaid)
- **Azure DevOps** — fenced code blocks in markdown (```mermaid)
- **Bitbucket** — no native support; generate SVG or link to mermaid.live

Detect the provider from git remotes:
```bash
git remote get-url origin 2>/dev/null
```
- Contains `github.com` → GitHub
- Contains `gitlab` → GitLab
- Contains `dev.azure.com` or `visualstudio.com` → Azure DevOps
- Contains `bitbucket.org` → Bitbucket
- Default → Mermaid (most widely supported)

## References

Load on demand:
- `${CLAUDE_PLUGIN_ROOT}/skills/diagram-expert/references/mermaid-patterns.md` — Diagram type patterns and syntax
- `${CLAUDE_PLUGIN_ROOT}/skills/diagram-expert/references/diagram-types.md` — When to use which diagram type
- `${CLAUDE_PLUGIN_ROOT}/skills/diagram-expert/references/readme-patterns.md` — README improvement patterns

## Agents

- **codebase-analyzer** — Analyses project structure, dependencies, and flows to suggest diagrams
- **readme-improver** — Reviews and improves READMEs with visual documentation
