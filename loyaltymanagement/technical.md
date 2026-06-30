---
repo: loyaltymanagement
spec_type: technical
commit: a0321cd4386bc946a394b585316e19a23f985828
model: anthropic:claude-sonnet-4-6
prompt_version: v1
input_hash: 223517456ad62115d22dfd391894f67014ce1b9e9a6d6184885c09a215615c83
generated_at: 2026-06-30T16:42:26.944976885+02:00
generator: specsync
---

## Tech Stack

| Component | Detail |
|---|---|
| Language | Java 21 |
| Runtime / Framework | Spring Boot 4.0.6 (via `spring-boot-starter-parent`) |
| Web Layer | Spring MVC (`spring-boot-starter-webmvc`) |
| Persistence | Spring Data JPA (`spring-boot-starter-data-jpa`) |
| In-memory Database | H2 (runtime scope) with H2 Console enabled (`spring-boot-h2console`) |
| API Documentation | SpringDoc OpenAPI UI 3.0.2 (`springdoc-openapi-starter-webmvc-ui`) |
| Code Generation | Lombok (annotation processor, excluded from final artifact) |
| Build Tool | Apache Maven (`spring-boot-maven-plugin`, `maven-compiler-plugin`) |
| Test Dependencies | `spring-boot-starter-data-jpa-test`, `spring-boot-starter-webmvc-test` |

## Architecture Patterns

The service follows a **layered, REST API** architectural style typical of Spring Boot applications:

- **Entry point**: Standard `@SpringBootApplication` bootstrap class (`LoyaltyManagementApplication`), enabling component scanning, auto-configuration, and JPA repositories across the `com.carrefour.loyalty` package.
- **Web layer**: Spring MVC controllers are expected to serve HTTP endpoints (no controllers were present in the sampled source at head commit).
- **Persistence layer**: Spring Data JPA abstractions over an H2 in-memory datastore; repository interfaces are implied by the JPA starter inclusion.
- **API discoverability**: SpringDoc OpenAPI integration suggests a contract-first or documentation-driven REST approach, exposing a Swagger UI at the standard `/swagger-ui.html` path.
- **No event-driven or CQRS patterns** are evident from the available code. The service appears to be a straightforward synchronous REST + JPA service.

> **Note:** Beyond the application bootstrap and a context-load test, no additional source files (controllers, services, repositories, entities) were present in the code snapshot. The architecture described reflects the configured dependencies rather than implemented classes.

## Database & Data Ownership

| Attribute | Detail |
|---|---|
| Datastore type | H2 in-memory relational database (runtime) |
| Persistence mechanism | Spring Data JPA / Hibernate (auto-DDL expected) |
| Schema/migrations | _Not determinable from code._ No Flyway, Liquibase, or SQL migration scripts detected |
| Owned tables/models | _Not determinable from code._ No JPA entity classes were present in the source snapshot |
| H2 Console | Enabled via `spring-boot-h2console`; accessible at `/h2-console` by default |

Because H2 is scoped `runtime` and is in-memory, **data does not persist across restarts**. This configuration is consistent with a development/prototype stage rather than production deployment.

## Dependencies

### Runtime Dependencies

| Dependency | Purpose |
|---|---|
| `spring-boot-starter-webmvc` | HTTP request handling via Spring MVC |
| `spring-boot-starter-data-jpa` | ORM and repository abstraction (Hibernate) |
| `spring-boot-h2console` | Embedded H2 web console |
| `h2` | In-memory relational database engine |
| `springdoc-openapi-starter-webmvc-ui` 3.0.2 | OpenAPI 3 spec generation and Swagger UI |
| `lombok` | Boilerplate reduction (annotation processor; not packaged in final JAR) |

### Test Dependencies

| Dependency | Purpose |
|---|---|
| `spring-boot-starter-data-jpa-test` | JPA slice testing support |
| `spring-boot-starter-webmvc-test` | MockMvc and web layer slice testing support |

### External Service / Broker / Cache Dependencies

_Not determinable from code._ No REST client configuration, message broker, cache abstraction, or third-party API integrations are present in the available source.

## Deployment Model

| Attribute | Detail |
|---|---|
| Dockerfile | _Not determinable from code._ No `Dockerfile` was present in the repository snapshot |
| Container orchestration | _Not determinable from code._ No Kubernetes manifests, Helm charts, or Docker Compose files detected |
| Build artifact | Executable JAR produced by `spring-boot-maven-plugin` via `mvn package` |
| Default HTTP port | Spring Boot default: **8080** (no override in `application.properties`) |
| Context path | `/` (default; not overridden) |
| Swagger UI | `http://<host>:8080/swagger-ui.html` (SpringDoc default) |
| OpenAPI spec | `http://<host>:8080/v3/api-docs` (SpringDoc default) |
| H2 Console | `http://<host>:8080/h2-console` (spring-boot-h2console default) |
| Health / readiness endpoints | _Not determinable from code._ Spring Boot Actuator is not listed as a dependency; no custom health endpoints detected |
| Environment configuration | Only `spring.application.name=loyalty-management` is set; all other configuration relies on Spring Boot auto-configuration defaults |
