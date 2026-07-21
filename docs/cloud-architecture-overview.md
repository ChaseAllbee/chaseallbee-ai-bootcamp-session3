# Cloud Architecture Overview

## System Context

```mermaid
flowchart LR
    user[TODO App User]

    subgraph system[TODO App Monorepo]
        frontend[React Frontend<br/>Browser SPA]
        api[Express API<br/>Node.js, port 3030]
        store[(In-Memory SQLite Store<br/>better-sqlite3)]

        frontend -->|HTTP/JSON requests<br/>/api/tasks| api
        api -->|SQL queries| store
    end

    user -->|Creates and manages tasks| frontend
    api -->|HTTP/JSON responses| frontend
```

## Creating a TODO Sequence

```mermaid
sequenceDiagram
    actor User
    participant Frontend as React Frontend
    participant API as Express API
    participant Store as In-Memory SQLite

    User->>Frontend: Enter TODO details and submit
    Frontend->>Frontend: Validate required title
    Frontend->>API: POST /api/tasks (JSON)
    API->>API: Validate request
    API->>Store: INSERT task
    Store-->>API: New task ID
    API->>Store: SELECT created task
    Store-->>API: Created task
    API-->>Frontend: 201 Created (JSON)
    Frontend->>API: GET /api/tasks
    API->>Store: SELECT tasks
    Store-->>API: Task list
    API-->>Frontend: 200 OK (JSON)
    Frontend-->>User: Display created TODO
```

## Component Responsibilities

- **React frontend:** Renders the task interface and sends task operations to the API. During local development, the frontend proxy forwards `/api` requests to `http://localhost:3030`.
- **Express API:** Exposes task CRUD endpoints under `/api/tasks`, validates requests, and reads from or writes to the task store.
- **In-memory store:** Uses a `better-sqlite3` database created with `:memory:`. Data exists only within the backend process and is lost when that process stops or restarts.

## Deployment Boundary

The repository does not currently define cloud infrastructure or a production deployment topology. The diagram represents the application-level system context and current local runtime architecture.
