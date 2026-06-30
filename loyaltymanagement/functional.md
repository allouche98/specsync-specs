---
repo: loyaltymanagement
spec_type: functional
commit: a0321cd4386bc946a394b585316e19a23f985828
model: anthropic:claude-sonnet-4-6
prompt_version: v1
input_hash: 223517456ad62115d22dfd391894f67014ce1b9e9a6d6184885c09a215615c83
generated_at: 2026-06-30T16:42:26.944976885+02:00
generator: specsync
---

## Business Purpose

This service, owned by Carrefour (`com.carrefour`), is intended to manage a customer loyalty programme. Based on its name, group ID, and technology stack (Spring Boot + JPA + REST MVC), it is designed to expose a REST API for managing loyalty-related domain data (e.g. points, tiers, rewards, members) persisted via a relational database. The service appears to be in an early scaffolding stage; no business logic has been committed beyond the Spring Boot application entry point.

## Domain Scope (DDD Bounded Context)

- **Bounded context:** Loyalty Management — encapsulates all concerns related to customer loyalty within the Carrefour retail domain.
- **Core domain entities / aggregates:** _Not determinable from code._ (No entity classes, repositories, or DB schema are present in the snapshot.)
- **Neighbouring contexts:** _Not determinable from code._ No inter-service calls, event topics, or explicit context-mapping artefacts are present.

## Use Cases / User Stories

No controllers, endpoints, or domain service classes are present in the snapshot; the following are inferred solely from the service name and declared technology stack.

- _(Inferred)_ As a loyalty platform, I want to manage customer loyalty records so that customers can accumulate and redeem points at Carrefour.
- _(Inferred)_ As an API consumer, I want to explore the loyalty API via a Swagger/OpenAPI UI (provided by `springdoc-openapi-starter-webmvc-ui`) so that I can integrate with the service without reading source code.
- _(Inferred)_ As a developer, I want to inspect the in-memory H2 database via the H2 console so that I can verify data during local development.

> No concrete endpoints could be tied to these stories; all are inferred from dependencies.

## Business Rules

- _Not determinable from code._ No domain logic, validation, or constraint definitions are present in the committed source. The only verifiable rule is:
  - The application context must load successfully (enforced by the `contextLoads` smoke test).
- The service uses an embedded H2 database (runtime scope), indicating it is **not yet configured for a production-grade persistent store** — persistence beyond process lifetime is not guaranteed in the current state. (inferred)
- The `spring.application.name` is set to `loyalty-management`, which will be used for service discovery and logging identification.
