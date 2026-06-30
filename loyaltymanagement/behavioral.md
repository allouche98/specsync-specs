---
repo: loyaltymanagement
spec_type: behavioral
commit: a0321cd4386bc946a394b585316e19a23f985828
model: anthropic:claude-sonnet-4-6
prompt_version: v1
input_hash: 223517456ad62115d22dfd391894f67014ce1b9e9a6d6184885c09a215615c83
generated_at: 2026-06-30T16:42:26.944976885+02:00
generator: specsync
---

## API Contracts

**Protocol:** REST over HTTP (Spring Web MVC), with OpenAPI/Swagger UI provided via `springdoc-openapi-starter-webmvc-ui` (v3.0.2). The Swagger UI is expected to be accessible at the default SpringDoc path (`/swagger-ui.html` or `/swagger-ui/index.html`) and the OpenAPI spec at `/v3/api-docs`.

No controller classes, request mappings, or route definitions are present in the source snapshot. All endpoint details are therefore:

_Not determinable from code._

| Method | Path | Purpose | Request | Response |
|--------|------|---------|---------|---------|
| — | — | _Not determinable from code._ | — | — |

## Event Schemas

_Not determinable from code._

No messaging broker dependencies (Kafka, RabbitMQ, Spring Cloud Stream, etc.) are declared in `pom.xml`, and no event producer or consumer classes are present in the source snapshot.

## Input / Output Formats

- **Serialization:** JSON is the expected default serialization format, as implied by `spring-boot-starter-webmvc` (which includes Jackson on the classpath by default via Spring Boot auto-configuration).
- **Content type:** `application/json` is the conventional default; no explicit `@Produces`/`@Consumes` or `MediaType` declarations are evidenced in the available source.
- **Pagination:** _Not determinable from code._
- **Request/response envelopes:** _Not determinable from code._
- **OpenAPI descriptor:** Available at runtime via SpringDoc at `/v3/api-docs` (JSON) and `/v3/api-docs.yaml` (YAML), consistent with springdoc-openapi-starter-webmvc-ui v3.0.2 defaults.

## Error Handling

No exception handlers (`@ControllerAdvice`, `@ExceptionHandler`), validation annotations, or custom error response classes are present in the source snapshot.

Spring Boot's default error handling behaviour applies by default:
- Standard Spring Boot `/error` endpoint returns a JSON error body with fields such as `timestamp`, `status`, `error`, `message`, and `path`.
- HTTP 500 for unhandled exceptions; HTTP 404 for unmapped routes; HTTP 400 for binding/validation failures — all via Spring Boot auto-configuration defaults.

Any customisation beyond these defaults is: _Not determinable from code._

## Versioning

No URI path versioning (e.g., `/v1/`, `/v2/`), request header versioning, or schema evolution strategy is evidenced in the source snapshot or configuration files.

The `pom.xml` declares artifact version `0.0.1-SNAPSHOT`, indicating the service is in early/pre-release development.

API versioning strategy: _Not determinable from code._
