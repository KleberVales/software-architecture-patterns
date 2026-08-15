# Software Architecture Patterns

## Layered Architecture

It divides an application horizontally into distinct layers, where each layer has a specialized role and only communicates with adjacent layers.

```text
┌─────────────────────────────────────────┐
│        Presentation Layer (UI/API)      │  Handles HTTP requests, JSON serialization
└────────────────────┬────────────────────┘
                     │ (Calls down)
┌────────────────────▼────────────────────┐
│      Business / Domain Layer            │  Contains core logic, rules, orchestration
└────────────────────┬────────────────────┘
                     │ (Calls down)
┌────────────────────▼────────────────────┐
│    Data Access / Persistence Layer      │  Executes database queries, ORM mappings
└─────────────────────────────────────────┘
```

- The core principles driving this architecture are:

   - Isolation of Roles: Developers can modify UI components without breaking database logic, or rewrite SQL queries without affecting business rules.
   - Standardized Control Flow: Request execution flows strictly top-to-bottom ($Presentation \rightarrow Business \rightarrow Data$). A lower layer never knows about or calls an upper layer.
   - Simplicity and Familiarity: It is intuitive to set up and aligns naturally with most web frameworks out of the box.



## Hexagonal Architecture

## Clean Architecture

## Onion Architecture
