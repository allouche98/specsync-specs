---
repo: microservice1
spec_type: behavioral
commit: 954d85981a924722137ae7edea41a6ffbf5b2444
model: anthropic:claude-sonnet-4-6
prompt_version: v1
input_hash: 114709d469695148ac59001a0b6f4f67457be70d3909991cffcbd2766815b388
generated_at: 2026-06-30T16:42:35.812096619+02:00
generator: specsync
---

## API Contracts

**Protocol:** REST (HTTP) via Jakarta REST (JAX-RS), implemented with Quarkus REST (`io.quarkus:quarkus-rest`). The service listens on port `8080`.

| Method | Path     | Purpose                        | Request                  | Response                                      |
|--------|----------|--------------------------------|--------------------------|-----------------------------------------------|
| GET    | `/hello` | Returns a plain-text greeting  | No request body or parameters | `200 OK` — plain-text string (e.g. `"Hello"`) |

> **Note:** The production resource (`HelloResource.java`) returns the literal string `"Hello"`. The test (`HelloResourceTest.java`) asserts the body is `"Hello from Quarkus REST"`, which suggests a possible discrepancy between the captured source sample and the tested artifact; the verified contract response body from the test assertion is `Hello from Quarkus REST`.

## Event Schemas

_Not determinable from code._

No message broker integration, event topics, or asynchronous messaging constructs are present in the codebase.

## Input / Output Formats

- **Content type (response):** `text/plain` — declared via `@Produces(MediaType.TEXT_PLAIN)` on the `GET /hello` handler.
- **Serialization:** Plain string; no JSON, Protobuf, or Avro serialization is used.
- **Request body:** None. The single endpoint accepts no request body, query parameters, or path parameters.
- **Pagination:** Not applicable — the endpoint returns a single scalar value.
- **Request/response envelope:** None. The response is a bare plain-text string with no wrapper structure.

## Error Handling

No explicit error handling, exception mappers, or custom error payload structures are defined in the source code. Behaviour for error conditions is governed entirely by the Quarkus/JAX-RS runtime defaults:

| Condition | Expected behaviour (framework default) |
|-----------|----------------------------------------|
| Method not allowed (e.g. `POST /hello`) | `405 Method Not Allowed` |
| Path not found | `404 Not Found` |
| Unhandled server exception | `500 Internal Server Error` |

No custom `ExceptionMapper`, `@ServerExceptionMapper`, or validation annotations are evidenced in the captured source.

## Versioning

No API versioning strategy is implemented. There is no URI version prefix (e.g. `/v1/`), version header, or schema evolution mechanism present in the codebase. The artifact version is `1.0.0-SNAPSHOT` (Maven coordinate `com.example:hello-quarkus:1.0.0-SNAPSHOT`), but this is a build version only and is not surfaced in the API path or headers.
