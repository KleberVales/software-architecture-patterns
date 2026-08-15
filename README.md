# Software Architecture Patterns

## 1. Layered Architecture

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

### 1.1 The core principles driving this architecture are:

- Isolation of Roles: Developers can modify UI components without breaking database logic, or rewrite SQL queries without affecting business rules.
- Standardized Control Flow: Request execution flows strictly top-to-bottom ($Presentation \rightarrow Business \rightarrow Data$). A lower layer never knows about or calls an upper layer.
- Simplicity and Familiarity: It is intuitive to set up and aligns naturally with most web frameworks out of the box.
 
### 1.2 Major Weaknesses of Layered Architecture

While Layered Architecture is great for getting simple applications off the ground, it reveals several critical flaws as system complexity scales:

- Database-Centric Coupling (The Transitive Dependency Problem)
- The "Pass-Through" Sinkhole Antipattern
- Testing Friction (Slow, Integrated Unit Tests)
- Monolithic Bloat ("Big Ball of Mud" Risk)



## Hexagonal Architecture

## Clean Architecture

## Onion Architecture

A good architecture tries to control:

Coupling — how much one part depends on another\
Cohesion — how well the responsibilities of a component fit together\
Dependency direction — who is allowed to depend on whom\
Changeability — how easy it is to change DB, framework, API, etc.\
Testability — how easy it is to test business logic\
Separation of concerns — keeping different responsibilities apart

