# Software Architecture Patterns

## 1. Introduction

A good architecture tries to control:

Coupling — how much one part depends on another\
Cohesion — how well the responsibilities of a component fit together\
Dependency direction — who is allowed to depend on whom\
Changeability — how easy it is to change DB, framework, API, etc.\
Testability — how easy it is to test business logic\
Separation of concerns — keeping different responsibilities apart

## 2. Layered Architecture

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

### 1.3 Where Layered Architecture Excels



## 2. Hexagonal Architecture

The purpose of Hexagonal Architecture (also known as the Ports and Adapters pattern, introduced by Alistair Cockburn) is to isolate core business logic from external dependencies, frameworks, delivery mechanisms, and databases.

In a traditional setup, database models and HTTP frameworks leak into your business rules. Hexagonal Architecture flips this on its head by turning the core application into a self-contained engine that doesn't care how it's triggered (via REST, CLI, Kafka, or tests) or where it stores data (PostgreSQL, MongoDB, or in-memory).


<img width="799" height="582" alt="Screenshot from 2026-08-14 22-17-39" src="https://github.com/user-attachments/assets/24014732-5b1e-43d6-9973-e3e1376590ac" />
Driving (Primary) vs Driven (Secondary) Ports and Adapters. Source: @hgraca

### 2.1 The Core Purpose & Key Mechanisms

Hexagonal Architecture achieves isolation using three main concepts:

- The Application Core (The Inside): Pure domain logic and use cases written in plain language features (POJOs / pure classes). It contains zero framework annotations (e.g., no JPA/Hibernate tags, no Spring Web dependencies).

- Ports (The Interfaces): Entry and exit points defined by the core:

   - Driving Ports (Inbound): Define how the outside world calls the core (e.g., OrderUseCase interface).

   - Driven Ports (Outbound): Define what the core needs from the outside world (e.g., SaveOrderPort interface).

- Adapters (The Outside Implementation): Concrete code translating between the outside world and the Ports:

   - Driving Adapters: REST Controllers, CLI commands, Kafka message listeners.

   - Driven Adapters: Database repositories (Spring Data JPA, JDBC), REST clients, AWS S3 adapters.

### 2.2 Main Strengths (Why Use It?)

- Framework & Infrastructure Independence: You can swap databases (e.g., PostgreSQL to DynamoDB) or messaging tools (Kafka to RabbitMQ) without touching a single line of core business logic.

- Blazing-Fast Unit Testing: Because the core application has no database or HTTP dependencies, you can unit-test 100% of your business rules using pure in-memory mocks without booting up Spring containers or Testcontainers.

- Multiple Delivery Mechanisms: A single core use case can easily be triggered by a REST API, a background cron job, a gRPC call, or a CLI tool just by plugging in new Driving Adapters.

### 2.3 Weaknesses & Trade-Offs

While Hexagonal Architecture solves structural coupling, it introduces non-trivial friction that makes it unsuitable for every project:

- Significant Indirection & Class Explosion
- High Mapping Overhead (Boilerplate)
- Steep Learning Curve & Team Friction
- Over-Engineering Simple Domains


## Clean Architecture

## Onion Architecture



