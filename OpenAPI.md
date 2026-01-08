# OpenAPI Documentation
OpenAPI is a specification (a standard) for describing HTTP APIs in a machine-readable format (usually YAML/JSON). It describes things like endpoints, parameters, request/response bodies, auth, and error formats.

Swagger historically was both:
- the original name of the spec (pre-2016), and
- a set of tools that work with the OpenAPI spec.

Today, people often say "Swagger" when they mean "OpenAPI + Swagger tooling".

## Quick start
- Create `openapi.yaml` (or `openapi.json`) in your repo.
- Document one endpoint end-to-end (path, request, response, and error).
- Serve the spec with Swagger UI or Redoc so you can browse it in a browser.

## Why you care

With an OpenAPI document you can:

- Generate interactive docs (Swagger UI / Redoc).
- Generate client SDKs (TypeScript, Java, C#, etc.).
- Generate server stubs (Spring, Express, FastAPI, etc.).
- Validate requests/responses automatically (contract enforcement).
- Improve testing (contract tests, mocking).
- Drive API governance (linting rules, versioning, review).

## The core artifact: the OpenAPI document

An OpenAPI file typically contains:

- **openapi**: the spec version (e.g., 3.0.3 or 3.1.0)
- **info**: title/version/description
- **servers**: base URLs
- **paths**: endpoints and operations (GET/POST/…)
- **components**: reusable schemas, parameters, responses, security schemes
- **security**: auth requirements (global or per-operation)
- **tags**: grouping/organization

Minimal example (OpenAPI 3.x YAML)
```yaml
openapi: 3.0.3
info:
  title: Example API
  version: 1.0.0
servers:
  - url: https://api.example.com
paths:
  /users/{id}:
    get:
      summary: Get a user
      parameters:
        - name: id
          in: path
          required: true
          schema:
            type: string
      responses:
        "200":
          description: OK
          content:
            application/json:
              schema:
                $ref: "#/components/schemas/User"
        "404":
          description: Not found
components:
  schemas:
    User:
      type: object
      required: [id, name]
      properties:
        id:
          type: string
        name:
          type: string
```

## Schemas: how OpenAPI models data

OpenAPI schemas are based on JSON Schema concepts.

Common constructs:
- **Primitive types**: `string`, `integer`, `number`, `boolean`
- **Objects** with properties + required
- **Arrays** with items
- **Constraints** like `minLength`, `maxLength`, `minimum`, `pattern`, `format` (e.g., `date-time`, `uuid`)
- **Composition**:
  - `oneOf` (exactly one matches, used for unions)
  - `anyOf` (any can match)
  - `allOf` (merge/compose, common for inheritance-like modeling)

### Example schema patterns

#### Enum
```yaml
type: string
enum: [ACTIVE, DISABLED]
```

#### Array
```yaml
type: array
items:
  $ref: "#/components/schemas/User"
```

#### Union
```yaml
oneOf:
  - $ref: "#/components/schemas/CardPayment"
  - $ref: "#/components/schemas/BankPayment"
```
### Requests and responses
*where people often get tripped up*

`Parameters` (in `path`, `query`, `header`, `cookie`) are not the same as a body.

Request bodies use `requestBody` and have content types.

`Responses` are keyed by status code strings like "200", "400".

POST example
```yaml
/users:
  post:
    requestBody:
      required: true
      content:
        application/json:
          schema:
            $ref: "#/components/schemas/CreateUserRequest"
    responses:
      "201":
        description: Created
```
### Auth (security schemes)
Typical entries live in `components.securitySchemes`, then you reference them in `security`.

OpenAPI supports many auth types; the most common is

- **Bearer JWT**
```yaml
components:
  securitySchemes:
    bearerAuth:
      type: http
      scheme: bearer
      bearerFormat: JWT
security:
  - bearerAuth: []
```

- **apiKey** (header/query)

- **oauth2** (authorizationCode, clientCredentials, etc.)

## Swagger tooling
Swagger tooling (what "Swagger" usually refers to now)

- **Swagger UI**: serves an interactive webpage for your OpenAPI file.

- **Swagger Editor**: browser editor with validation + preview.

- **Swagger Codegen** (older) / **OpenAPI Generator** (widely used): generates SDKs, docs, stubs.
- **Swagger Hub**: hosted platform for managing APIs.
- **Swagger Inspector**: testing and validating APIs.
- **Swagger CLI**: command-line tools for linting, bundling, validating OpenAPI files.
- **OpenAPI Linting tools**: e.g., Spectral, OpenAPI-Lint for enforcing style and best practices.
- **Mock servers**: e.g., Prism, Stoplight for simulating APIs based on OpenAPI.
- **Contract testing tools**: e.g., Dredd for validating API implementations against OpenAPI specs.
- **Documentation generators**: e.g., Redoc, ReDocly for publishing beautiful API docs.
- **API gateways**: e.g., Kong, Tyk that can import OpenAPI for routing and validation.
- **CI/CD integrations**: many CI tools have plugins/extensions for OpenAPI validation, linting, and publishing.
- **API management platforms**: e.g., Apigee, AWS API Gateway that leverage OpenAPI for API lifecycle management.
- **IDE plugins**: e.g., VSCode OpenAPI extension for editing and validating OpenAPI files directly in your IDE.
- **Runtime validation libraries**: e.g., express-openapi-validator for validating requests/responses in your application based on OpenAPI specs.
- **API design platforms**: e.g., Stoplight Studio for collaborative API design using OpenAPI.
- **Versioning tools**: e.g., OpenAPI Diff for comparing different versions of OpenAPI specs.
- **Security analysis tools**: e.g., 42Crunch for analyzing OpenAPI specs for security vulnerabilities.
- **API mocking services**: e.g., Mockoon for quickly creating mock APIs from OpenAPI specs.

In practice:
- You keep an openapi.yaml in your repo.
- CI lints/validates it.
- Swagger UI (or Redoc) publishes docs.
- Generators produce client libraries.

## Design strategies
#### Design-first (contract-first)
- Write OpenAPI first.
- Generate server stubs / clients.
- Implement behind the contract.

Best when: you want strong governance, multiple teams, or stable public APIs.

#### Code-first
- Write code (controllers/models) and generate OpenAPI from annotations or runtime introspection.

Best when: fast iteration and you trust code as source of truth.

#### Hybrid
- Generate OpenAPI from code, then manually edit/curate it.
Best when: you want some automation but still need control over the spec.

#### Versioning strategy
- Put major version in the URL: /v1/...
- Or use headers (more complex)
- Keep OpenAPI versions aligned with release tags (e.g., info.version: 1.4.2)

### Common pitfalls
- Forgetting to document error responses (400/401/403/404/409/500).
- Not defining consistent error schema (hard for clients).
- Overusing allOf and making generated clients weird.
- Not specifying nullable/required correctly (especially for codegen).
- Divergence between implementation and spec (fix via CI validation/tests).

## OpenAPI in Spring Boot
### Use Springdoc (Spring Boot 3.x) as your OpenAPI source of truth

For a Spring MVC app, the standard approach is `springdoc-openapi` (the starter gives you the OpenAPI endpoint + Swagger UI).

Maven dependency
```xml
<dependency>
  <groupId>org.springdoc</groupId>
  <artifactId>springdoc-openapi-starter-webmvc-ui</artifactId>
  <version><!-- pin a springdoc 2.8.x or newer compatible version --></version>
</dependency>
```

#### Notes on versions:
- Springdoc 2.8.14 is a recent Spring Boot 3.x-era release.
- Springdoc 3.x exists and is tied to Spring Boot 4.x support (RCs mention SB 4.0.0-RC1).

### Lock down the exact OpenAPI + UI endpoints (and only document /api/**)

Because defaults can shift across springdoc versions (recent release notes mention disabling /v3/api-docs and /swagger-ui.html defaults), set these explicitly.

application.yml
```yaml
springdoc:
  api-docs:
    enabled: true
    path: /api-docs       # instead of the default /v3/api-docs
  swagger-ui:
    enabled: true
    path: /swagger-ui.html
  paths-to-match: /api/** # only document your API endpoints
```

`Property names` and `defaults` are documented by **springdoc** (e.g., `springdoc.api-docs.path`, `springdoc.api-docs.enabled`, `springdoc.paths-to-match`, `springdoc.swagger-ui.path`). 

Resulting URLs (in dev/prod, same domain):
- OpenAPI JSON: `GET /api-docs`
- Swagger UI: `GET /swagger-ui.html`

#### Create a small “contract-first” discipline while staying code-first

A practical pattern is:

- Every controller lives under /api
- Every request/response type is a DTO (records are fine)
- You annotate only where inference isn’t enough (summaries, examples, edge-case params, error responses)

**Controller example** (minimal but “OpenAPI-clean”)
```java
@RestController
@RequestMapping("/api/users")
@Tag(name = "Users")
public class UserController {

  @GetMapping("/{id}")
  @Operation(summary = "Get a user by id")
  @ApiResponses({
    @ApiResponse(responseCode = "200", description = "OK"),
    @ApiResponse(responseCode = "404", description = "Not found")
  })
  public UserDto get(@PathVariable String id) {
    ...
  }

  @PostMapping
  @Operation(summary = "Create a user")
  @ApiResponses({
    @ApiResponse(responseCode = "201", description = "Created"),
    @ApiResponse(responseCode = "400", description = "Validation error")
  })
  @ResponseStatus(HttpStatus.CREATED)
  public UserDto create(@Valid @RequestBody CreateUserRequest req) {
    ...
  }
}
```

**DTO example**
```java
public record CreateUserRequest(
  @NotBlank
  @Schema(example = "Ada Lovelace")
  String name
) {}

public record UserDto(
  String id,
  String name
) {}
```
### Spring Security, with Spring Doc
You must explicitly allow docs (at least in dev)

If you secure your app, Swagger UI and the OpenAPI JSON endpoint will also be secured unless you permit them.

Typical dev-only allow-list (adjust paths to match what you set in application.yml):
- `/api-docs/**`
- `/swagger-ui/**`
- `/swagger-ui.html`

Then disable the UI in prod using springdoc.swagger-ui.enabled=false if desired; springdoc documents that property. 

### React/Vite integration spec-driven (recommended)

You have two good options:

#### Option A (classic): **generate a typed client via OpenAPI Generator**

Use the `typescript-fetch generator`

Workflow:
- Backend exposes `GET /api-docs`
- Frontend runs a script to generate `src/generated/...`
- Your React code imports the generated client/types

#### Option B (lightweight): **generate types + use a tiny type-safe fetch wrapper**

Libraries like openapi-fetch consume an OpenAPI schema and give you typed fetch calls.

### Make dev feel “same-origin” with a Vite proxy

Even though prod is same-domain, dev is usually localhost:5173 vs localhost:8080. Proxying avoids CORS and keeps URLs consistent.

vite.config.ts
```typescript
import { defineConfig } from "vite";
import react from "@vitejs/plugin-react";

export default defineConfig({
  plugins: [react()],
  server: {
    proxy: {
      "/api": "http://localhost:8080",
      "/api-docs": "http://localhost:8080",
      "/swagger-ui": "http://localhost:8080",
      "/swagger-ui.html": "http://localhost:8080",
    },
  },
});
```

Vite's server.proxy behavior is documented in the Vite docs.

Now your frontend can call fetch("/api/whatever") in both dev and prod.

### Generate and archive the OpenAPI file during builds

If you want a stable artifact (for CI diffs, publishing, client generation without a running server), springdoc provides build-time plugins that generate JSON/YAML during the build (runs during integration-test phase)

### Recommended “do this first” checklist

Add springdoc starter dependency.

Add the springdoc.* properties above (explicit paths + /api/** match). 

Hit:
- `/api-docs`
- `/swagger-ui.html`

Add Vite proxy so your frontend always calls /api/....

Pick client strategy:
- `OpenAPI Generator typescript-fetch` 
- `openapi-fetch`

