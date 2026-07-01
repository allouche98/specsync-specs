---
repo: microservice1
spec_type: functional
commit: fc1d6e6323f710ab16190abe9550bf81c2b36f23
model: anthropic:claude-sonnet-4-6
prompt_version: v1
input_hash: d184f820c48574690a1a274d278aa6d784a7a22a7d9a0daa5ad2cff964993cfa
generated_at: 2026-07-01T10:15:30.385244656+02:00
generator: specsync
---

## Business Purpose

This service is a lightweight Quarkus-based REST API that exposes three independent utility capabilities: arithmetic calculation, a greeting endpoint, and mock weather information retrieval. It appears to be a demonstration or hackathon prototype rather than a production business service, combining unrelated concerns in a single deployable unit. It provides consumers with simple on-demand computation and weather data (currently backed by hardcoded mock data) over HTTP.

## Domain Scope (DDD Bounded Context)

- **Bounded context:** Utility / Demo Services — no single cohesive business domain is owned; the service aggregates unrelated capabilities.
- **Core domain entities / aggregates:**
  - `CalculationResult` — represents the outcome of an arithmetic operation (operands, operation name, optional error).
  - `WeatherInfo` — represents current weather conditions for a named city (temperature, condition, humidity).
  - `WeatherForecast` / `DayForecast` — represents a multi-day weather forecast for a city.
- **Neighbouring contexts:** No upstream or downstream service integrations are evident; `quarkus-rest-client` is declared as a dependency (suggesting outbound HTTP calls were planned or partially scaffolded), but no actual REST client interfaces appear in the source snapshot.

## Use Cases / User Stories

- **As a consumer, I want to add two numbers** so that I receive their sum — served by `GET /calculator/add?a={a}&b={b}`.
- **As a consumer, I want to subtract two numbers** so that I receive their difference — served by `GET /calculator/subtract?a={a}&b={b}`.
- **As a consumer, I want to multiply two numbers** so that I receive their product — served by `GET /calculator/multiply?a={a}&b={b}`.
- **As a consumer, I want to divide two numbers** so that I receive their quotient — served by `GET /calculator/divide?a={a}&b={b}` (with division-by-zero protection).
- **As a consumer, I want to retrieve current weather for a city** so that I can display temperature, condition, and humidity — served by `GET /weather?city={city}`.
- **As a consumer, I want to retrieve a multi-day weather forecast for a city** so that I can plan ahead — served by `GET /weather/forecast?city={city}&days={days}`.
- **As a consumer, I want to call a health/greeting endpoint** so that I can verify the service is reachable — served by `GET /hello`.

## Business Rules

- **Division by zero is guarded:** When `b == 0`, `GET /calculator/divide` returns a result of `0` with an error message `"Error: Division by zero"` rather than throwing an exception.
- **City parameter is mandatory for weather endpoints:** If the `city` query parameter is absent or empty, both `GET /weather` and `GET /weather/forecast` return an error payload (`"Error: city parameter is required"`) instead of weather data.
- **Forecast day range is constrained to 1–7:** `GET /weather/forecast` rejects requests where `days <= 0` or `days > 7` with an error message `"Error: days must be between 1 and 7"`. (inferred: the upper bound of 7 implies a one-week forecast window design intent.)
- **Weather data is mocked:** Current weather responses for cities other than `paris`, `london`, `new york`, and `tokyo` return a default/unknown condition; no real external API is called.
- **All calculator operations accept `double` inputs:** Operands `a` and `b` are typed as `double`, allowing decimal values.
- **All responses are JSON except `/hello`:** The `/hello` endpoint produces `text/plain`; all calculator and weather endpoints produce `application/JSON`.
- **Error information is carried in-band:** Errors are returned as fields within the normal response body (not as HTTP error status codes). (inferred: no non-200 status codes are set in error paths visible in the source.)
