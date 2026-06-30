---
repo: microservice1
spec_type: technical
commit: 954d85981a924722137ae7edea41a6ffbf5b2444
model: anthropic:claude-sonnet-4-6
prompt_version: v1
input_hash: 114709d469695148ac59001a0b6f4f67457be70d3909991cffcbd2766815b388
generated_at: 2026-06-30T16:42:35.812096619+02:00
generator: specsync
---

## Tech Stack

| Component | Detail |
|---|---|
| Language | Java 21 (`maven.compiler.release=21`) |
| Runtime | JVM (OpenJDK 21) or GraalVM native executable |
| Framework | Quarkus 3.37.0 |
| REST layer | `quarkus-rest` (Jakarta REST / JAX-RS) |
| DI container | `quarkus-arc` (CDI-based) |
| Build tool | Apache Maven (Maven Wrapper included) with `quarkus-maven-plugin` 3.37.0 |
| Test frameworks | `quarkus-junit` (unit + integration), `rest-assured` (HTTP assertion) |
| Compiler plugin | `maven-compiler-plugin` 3.15.0 |
| Surefire / Failsafe | `maven-surefire-plugin` / `maven-failsafe-plugin` 3.5.6 |

## Architecture Patterns

- **Simple layered REST API** — a single-tier service with no persistence or messaging layer.
- **JAX-RS resource class** (`HelloResource`) acts as the sole HTTP entry point; CDI (`quarkus-arc`) wires beans.
- No CQRS, event-driven, or worker patterns are present; the service is a minimal request/response microservice.
- **Key internal component:**
  - `com.example.HelloResource` — a JAX-RS `@Path("/hello")` resource that handles `GET` requests and returns a plain-text response.

## Database & Data Ownership

This service owns no datastores. No database drivers, ORM frameworks, migration tools, or table definitions are present anywhere in the codebase. `application.properties` is empty.

## Dependencies

### Runtime
| Dependency | Purpose |
|---|---|
| `io.quarkus:quarkus-rest` | Jakarta REST (JAX-RS) implementation for serving HTTP endpoints |
| `io.quarkus:quarkus-arc` | CDI dependency injection container |
| `io.quarkus.platform:quarkus-bom` 3.37.0 | Quarkus BOM for dependency version alignment |

### Test (scope: `test`)
| Dependency | Purpose |
|---|---|
| `io.quarkus:quarkus-junit` | Quarkus test harness (`@QuarkusTest`, `@QuarkusIntegrationTest`) |
| `io.rest-assured:rest-assured` | Fluent HTTP client for integration assertions |

No external services, message brokers, caches, or third-party APIs are called.

## Deployment Model

### Container images
Four Dockerfile variants are provided under `src/main/docker/`:

| Dockerfile | Base image | Mode |
|---|---|---|
| `Dockerfile.jvm` | `ubi9/openjdk-21-runtime:1.24` | JVM — layered fast-jar |
| `Dockerfile.legacy-jar` | `ubi9/openjdk-21-runtime:1.24` | JVM — legacy über-jar |
| `Dockerfile.native` | `ubi9/ubi-minimal:9.7` | GraalVM native executable |
| `Dockerfile.native-micro` | `quay.io/quarkus/ubi9-quarkus-micro-image:2.0` | GraalVM native (micro image) |

All variants:
- **Expose port `8080`** (HTTP).
- Set `quarkus.http.host=0.0.0.0` via `JAVA_OPTS_APPEND` (or native entrypoint arg).
- Run as non-root user (`185` for JVM images, `1001` for native images).
- Use `/opt/jboss/container/java/run/run-java.sh` as the entrypoint for JVM variants; native variants execute the binary directly.

### Build
```bash
./mvnw package                          # JVM jar
./mvnw package -Dnative                 # native executable (requires GraalVM or container build)
```
Native build is activated via the `native` Maven profile (`-Dnative` system property).

### Orchestration
_Not determinable from code._ No Kubernetes manifests, Helm charts, or Docker Compose files are present in the repository.

### Environment configuration
`application.properties` is empty; no environment variables beyond those consumed by `run-java.sh` (heap tuning, proxy, debug) are defined.

### Health / readiness endpoints
_Not determinable from code._ The `quarkus-smallrye-health` extension is not declared; Quarkus default liveness/readiness probes are therefore not available unless provided by the platform BOM automatically, which cannot be confirmed from the manifests alone.
