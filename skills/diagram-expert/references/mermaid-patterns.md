# Mermaid Diagram Patterns

Quick reference for generating correct Mermaid syntax. Always test that the syntax is valid before presenting to the user.

## Flowchart (Architecture / System Overview)

```mermaid
---
title: System Architecture
---
graph TD
    subgraph Frontend["Frontend (React)"]
        App[App Component]
        Pages[Page Router]
        Store[State Store]
    end

    subgraph Backend["Backend (Express)"]
        API[API Gateway]
        Auth[Auth Service]
        Business[Business Logic]
    end

    subgraph Data["Data Layer"]
        DB[(PostgreSQL)]
        Cache[(Redis)]
        Queue[Message Queue]
    end

    App --> Pages
    Pages --> Store
    Store -->|API calls| API
    API --> Auth
    API --> Business
    Business --> DB
    Business --> Cache
    Auth --> Cache
    Business --> Queue
```

Direction options:
- `TD` or `TB` — top to bottom (best for hierarchies)
- `LR` — left to right (best for flows and pipelines)
- `RL` — right to left
- `BT` — bottom to top

Node shapes:
- `[text]` — rectangle
- `(text)` — rounded rectangle
- `{text}` — diamond (decision)
- `[(text)]` — cylinder (database)
- `([text])` — stadium (terminal)
- `[[text]]` — subroutine
- `>text]` — flag

Edge types:
- `-->` — solid arrow
- `-.->` — dotted arrow
- `==>` — thick arrow
- `-->|label|` — labelled edge
- `--- ` — solid line (no arrow)

## Sequence Diagram

```mermaid
sequenceDiagram
    actor User
    participant Client as React App
    participant API as Express API
    participant Auth as Auth Service
    participant DB as PostgreSQL

    User->>Client: Click login
    Client->>API: POST /auth/login
    API->>Auth: Validate credentials
    Auth->>DB: Query user
    DB-->>Auth: User record
    Auth-->>API: JWT token
    API-->>Client: 200 + token
    Client-->>User: Redirect to dashboard
```

Arrow types:
- `->>` — solid with arrowhead
- `-->>` — dotted with arrowhead
- `-x` — solid with cross
- `--x` — dotted with cross

Features:
- `activate/deactivate` — lifeline activation
- `Note over A,B: text` — spanning note
- `alt/else/end` — conditional
- `loop/end` — repetition
- `par/and/end` — parallel

## Entity-Relationship Diagram

```mermaid
erDiagram
    User ||--o{ Order : places
    User {
        uuid id PK
        string email UK
        string name
        timestamp created_at
    }
    Order ||--|{ OrderItem : contains
    Order {
        uuid id PK
        uuid user_id FK
        decimal total
        string status
        timestamp created_at
    }
    OrderItem }|--|| Product : references
    OrderItem {
        uuid id PK
        uuid order_id FK
        uuid product_id FK
        int quantity
        decimal price
    }
    Product {
        uuid id PK
        string name
        decimal price
        string category
    }
```

Relationship types:
- `||--||` — one to one
- `||--o{` — one to many (zero or more)
- `||--|{` — one to many (one or more)
- `}o--o{` — many to many

## State Diagram

```mermaid
stateDiagram-v2
    [*] --> Draft
    Draft --> PendingReview: Submit
    PendingReview --> Approved: Approve
    PendingReview --> Rejected: Reject
    Rejected --> Draft: Revise
    Approved --> Published: Publish
    Published --> Archived: Archive
    Archived --> [*]
```

## Class Diagram (Component Structure)

```mermaid
classDiagram
    class AuthService {
        -jwtSecret: string
        -tokenExpiry: number
        +login(email, password) Promise~Token~
        +verify(token) Promise~User~
        +refresh(token) Promise~Token~
    }
    class UserRepository {
        -db: Database
        +findByEmail(email) Promise~User~
        +create(data) Promise~User~
        +update(id, data) Promise~User~
    }
    AuthService --> UserRepository: uses
    AuthService --> TokenCache: caches
```

## C4 Model (using flowchart)

Mermaid doesn't have native C4 support, so use flowcharts with styling:

```mermaid
graph TD
    User["User<br/><i>Web browser</i>"]

    subgraph System["My Application"]
        WebApp["Web App<br/><i>React SPA</i>"]
        API["API Server<br/><i>Express + Node.js</i>"]
        DB[("Database<br/><i>PostgreSQL</i>")]
    end

    External["Email Service<br/><i>SendGrid API</i>"]

    User -->|HTTPS| WebApp
    WebApp -->|REST API| API
    API -->|SQL| DB
    API -->|SMTP/API| External
```

## Gitgraph

```mermaid
gitgraph
    commit id: "init"
    branch develop
    checkout develop
    commit id: "feat: base setup"
    branch feature/auth
    checkout feature/auth
    commit id: "feat: login"
    commit id: "feat: jwt"
    checkout develop
    merge feature/auth
    branch feature/api
    checkout feature/api
    commit id: "feat: endpoints"
    checkout develop
    merge feature/api
    checkout main
    merge develop tag: "v1.0.0"
```

## Gantt / Timeline

```mermaid
gantt
    title Project Timeline
    dateFormat YYYY-MM-DD
    section Phase 1
        Design           :done,    des,  2024-01-01, 2024-01-14
        Implementation   :active,  impl, 2024-01-15, 2024-02-15
    section Phase 2
        Testing          :         test, after impl, 30d
        Deployment       :         dep,  after test, 7d
```

## Pie Chart

```mermaid
pie title Code Distribution
    "TypeScript" : 45
    "React Components" : 30
    "Tests" : 15
    "Configuration" : 10
```

## Common Mistakes to Avoid

1. **Special characters in labels** — Wrap in quotes: `A["Label with (parens)"]`
2. **Long labels** — Use `<br/>` for line breaks, not `\n`
3. **Too many nodes** — Split into multiple diagrams if >30 nodes
4. **Single-letter IDs** — Use descriptive: `AuthService` not `A`
5. **Missing direction** — Always specify `graph TD` or `graph LR`
6. **Unlabelled edges** — Add labels to non-obvious connections
7. **Subgraph nesting** — Mermaid supports 1 level of nesting; avoid deeper
8. **Reserved words** — `end`, `graph`, `subgraph` cannot be node IDs; wrap in quotes
