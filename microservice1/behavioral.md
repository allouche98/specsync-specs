---
repo: microservice1
spec_type: behavioral
commit: 67a1a3cf92762515763f4e7d8cea0cfc4eeb30c1
model: anthropic:claude-sonnet-4-6
prompt_version: v1
input_hash: 50ee4e55544c2ceaf0a54f62861f4c7d0de3a524a44ec92fd862370af5bb0606
generated_at: 2026-06-30T16:52:40.120538861+02:00
generator: specsync
---

## API Contracts

**Protocol:** REST (HTTP) over Jakarta REST (JAX-RS), implemented with Quarkus REST (`quarkus-rest`). The service listens on port `8080`.

| Method | Path | Purpose | Request | Response |
|--------|------|---------|---------|----------|
| `GET` | `/greeting` | Returns a plain-text greeting string | No request body; no path/query parameters | `200 OK` — body: plain-text string (e.g., `"Hello"`) |
| `GET` | `/greeting` | Returns a numeric value as a string | No request body; no path/query parameters | `200 OK` — body: JSON string (e.g., `"2"`) |

> **Note:** Both handlers are mapped to `GET /greeting` within `HelloResource.java`. The two `@GET` methods differ only in their declared `@Produces` media type (`text/plain` vs. `application/json`). At runtime, JAX-RS content negotiation (via the `Accept` request header) determines which variant is invoked. The effective behaviour of content negotiation and any conflict resolution is _not determinable from code_ beyond what the annotations indicate.

---

## Event Schemas

_Not determinable from code._

---

## Input / Output Formats

- **Content negotiation:** The `/greeting` endpoint declares two producer variants:
  - `text/plain` — returns a bare string (`"Hello"`).
  - `application/json` — returns a JSON-encoded string (`"2"`, i.e., the integer `2` serialised as a string).
- **Serialization:** Plain-text and JSON; no Protobuf or Avro involved.
- **Request body:** None required for any documented endpoint.
- **Pagination:** Not applicable — single-value responses only.
- **Envelope:** No wrapper envelope; responses are bare scalar values.

---

## Error Handling

No custom error-handling code, exception mappers, or validation logic is present in the source snapshot. Default Quarkus/JAX-RS framework behaviour applies:

- A `GET /greeting` request with an `Accept` header that cannot be satisfied by either `text/plain` or `application/json` will result in a framework-generated `406 Not Acceptable`.
- Other standard HTTP error codes (e.g., `404`, `500`) are governed entirely by the Quarkus REST runtime defaults.

The exact error payload structure for framework-generated errors is _not determinable from code._

---

## Versioning

No URI versioning prefix (e.g., `/v1/`), version-bearing request/response headers, or schema-evolution mechanism is present in the source. The artifact version is `1.0.0-SNAPSHOT` (declared in `pom.xml`) but this is not surfaced in the API path or any header. _No API versioning strategy is evident from the code._

## Drift Alignment (auto-suggested)
- [ ] Add endpoint `PATH /hello`
