---
repo: microservice1
spec_type: functional
commit: 67a1a3cf92762515763f4e7d8cea0cfc4eeb30c1
model: anthropic:claude-sonnet-4-6
prompt_version: v1
input_hash: 50ee4e55544c2ceaf0a54f62861f4c7d0de3a524a44ec92fd862370af5bb0606
generated_at: 2026-06-30T16:52:40.120538861+02:00
generator: specsync
---

## Business Purpose

This service is a minimal Quarkus-based REST microservice that exposes a greeting endpoint. It appears to be a scaffolded starter or proof-of-concept application generated from the Quarkus project bootstrap tooling. Its primary capability is responding to HTTP GET requests at `/hello` with a simple text or JSON response. No meaningful business domain logic beyond the scaffold is present in the codebase.

## Domain Scope (DDD Bounded Context)

- **Bounded context:** _Not determinable from code._ The service contains only scaffold-level code with no domain modelling.
- **Core entities/aggregates:** None detected. No domain entities, aggregates, or persistence models are present.
- **Relationships to neighbouring contexts:** None detected. No upstream or downstream integrations are evident (no HTTP clients, messaging, or database access).

## Use Cases / User Stories

- **As a caller**, I want to send `GET /hello` so that I receive a plain-text `"Hello"` response confirming the service is reachable.
  - Implemented by `HelloResource#hello()` → `GET /hello`, produces `text/plain`.
- **As a caller**, I want to send `GET /hello` accepting JSON so that I receive a numeric value (`"2"`) as a JSON string.
  - Implemented by `HelloResource#calculate()` → `GET /hello`, produces `application/json`.
  > Note: both methods share the same path and HTTP verb; content-type negotiation (`Accept` header) is the differentiator.

## Business Rules

- The `/hello` endpoint accepts only HTTP `GET` requests; other methods are not handled. (inferred)
- Response content is selected by content-type negotiation: `Accept: text/plain` returns the string `"Hello"`; `Accept: application/json` returns the string `"2"`. (inferred from `@Produces` annotations)
- The service binds to all network interfaces (`0.0.0.0`) on port `8080` as configured in the Docker entrypoints.
- No authentication, authorisation, or input validation logic is present. (inferred)
- No persistent state is maintained; both responses are hardcoded constants. (inferred)
- Integration tests (`HelloResourceIT`) execute the same test suite against the packaged artifact, requiring the service to pass unit tests before integration verification.
- The test suite asserts that `GET /hello` returns HTTP `200` with body `"Hello from Quarkus REST"` — this contradicts the current source implementation which returns `"Hello"`, indicating the test may be misaligned with the implementation. _Not determinable from code_ whether this is intentional or a defect.
