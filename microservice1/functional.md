---
repo: microservice1
spec_type: functional
commit: 954d85981a924722137ae7edea41a6ffbf5b2444
model: anthropic:claude-sonnet-4-6
prompt_version: v1
input_hash: 114709d469695148ac59001a0b6f4f67457be70d3909991cffcbd2766815b388
generated_at: 2026-06-30T16:42:35.812096619+02:00
generator: specsync
---

## Business Purpose

This service is a minimal "hello world" REST microservice built with the Quarkus framework. It exposes a single HTTP endpoint that returns a plain-text greeting, serving primarily as a baseline template or proof-of-concept for Quarkus-based Java microservices. It demonstrates the scaffolding, build tooling, and containerisation patterns used within the organisation.

## Domain Scope (DDD Bounded Context)

- **Bounded context:** Demonstration / scaffolding — no meaningful business domain is modelled.
- **Core domain entities / aggregates:** None. No domain objects, aggregates, or persistent state are present.
- **Relationships to neighbouring contexts:** None detectable. The service has no outbound HTTP calls, messaging, or database dependencies.

## Use Cases / User Stories

- **As a client** I want to call `GET /hello` so that I receive a plain-text greeting response confirming the service is reachable.
  - Backed by `HelloResource.hello()` → `GET /hello` → HTTP 200, `text/plain`.

## Business Rules

- The `GET /hello` endpoint must return HTTP 200 with a plain-text body. (inferred — validated by `HelloResourceTest` asserting status 200 and body `"Hello from Quarkus REST"`.)
- No authentication, authorisation, or input validation rules are present or enforced.
- No persistent state is written or read; the response is stateless and constant.
- The response content type is strictly `text/plain` (`MediaType.TEXT_PLAIN` declared via `@Produces`).
