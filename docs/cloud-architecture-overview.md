# Cloud Architecture Overview

This monorepo contains a React frontend and a Node/Express backend that exposes a task API backed by an in-memory SQLite database. The following context diagram shows the high-level components and their interactions.

```mermaid
graph TD
  U[End User (Browser)] --> FE[Frontend Web App (React)]
  FE --> API[Backend Service (Node/Express /api/tasks)]
  API --> DB[(SQLite Task Store)]

  subgraph Monorepo / Deployment
    FE
    API
    DB
  end
```

## Sequence: Creating a TODO

The following sequence diagram illustrates the main steps when a user creates a new TODO item.

```mermaid
sequenceDiagram
  actor U as User (Browser)
  participant FE as Frontend (React TODO App)
  participant API as Backend (Node/Express /api/tasks)
  participant DB as SQLite Task Store

  U->>FE: Enter task details and submit form
  FE->>API: POST /api/tasks { title, description, due_date }
  API->>DB: INSERT new task record
  DB-->>API: Return new task row (id, fields)
  API-->>FE: 201 Created with task JSON
  FE-->>U: Update task list with new TODO
```
