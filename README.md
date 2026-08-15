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

## Hexagonal Architecture

## Clean Architecture

## Onion Architecture
