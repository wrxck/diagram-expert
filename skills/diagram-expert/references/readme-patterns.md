# README Improvement Patterns

Patterns for adding diagrams to existing READMEs without disrupting structure.

## Section placement

Insert diagrams in context, near the text they illustrate:

| Diagram type | Best section | Fallback |
|-------------|-------------|----------|
| Architecture overview | ## Architecture / ## Overview | After project description |
| Sequence diagrams | ## How It Works / ## API | After API docs |
| ERD | ## Database / ## Data Model | Before API docs |
| Deployment | ## Deployment / ## Infrastructure | After installation |
| State diagrams | Inline with feature docs | ## How It Works |

## Introduction text

Always add a brief sentence before the diagram:

Good:
```markdown
## Architecture

The application follows a three-tier architecture with a React frontend,
Express API layer, and PostgreSQL database.

` ``mermaid
graph TD
    ...
` ``
```

Bad (no context):
```markdown
## Architecture

` ``mermaid
graph TD
    ...
` ``
```

## Proposing changes

When presenting proposals to the user, be specific about what you'd add and where:

```
I found 3 opportunities to improve your README:

1. **Architecture diagram** (flowchart)
   Your README mentions "React frontend and Node.js backend" in the description
   but doesn't show how they connect. I'd add a system diagram after the
   description showing: React -> API -> DB with the nginx reverse proxy.

2. **Auth flow** (sequence diagram)
   The "Authentication" section has a 12-line text description of the login flow.
   A sequence diagram would make this much clearer and shorter.

3. **Database schema** (ERD)
   You have 6 Prisma models. Currently undocumented. I'd add an ERD in a new
   "Data Model" section before the API docs.
```

## Common README structures

### Minimal README (needs the most help)
```
# Project Name
Description
## Installation
## Usage
```
Add: Architecture overview after description.

### Standard README
```
# Project Name
Description + badges
## Features
## Installation
## Usage / API
## Contributing
## Licence
```
Add: Architecture after Features, specific flow diagrams in Usage/API sections.

### Comprehensive README
```
# Project Name
Description + badges
## Architecture  <-- diagram goes here
## Features
## Getting Started
## API Reference  <-- sequence diagrams here
## Database  <-- ERD here
## Deployment  <-- deployment diagram here
## Contributing
## Licence
```
Enhance existing sections with diagrams.

## What NOT to do

- Don't add diagrams that just repeat what's already clear from text
- Don't add a diagram section with 10 diagrams — pick the 2-3 most valuable
- Don't remove existing text to replace with diagrams
- Don't add diagrams for trivial projects (single-file scripts, simple configs)
- Don't guess at architecture — only diagram what's verifiable from the code
- Don't add diagrams to CHANGELOG, CONTRIBUTING, or other non-README docs unless asked
