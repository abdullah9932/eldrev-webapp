# eldrev-webapp

Monorepo for the Eldrev Next.js frontend and backend services.

## Layout

```text
frontend/                         Next.js application
services/
  catalog-api/
    pom.xml                       Maven reactor for catalog projects
    catalog-service/              Spring Boot catalog backend
    catalog-service-spec/         Versioned OpenAPI contract and TS client generation
```

Keep backend services under `services/`; add future services alongside `catalog-api/`. The service and OpenAPI contract are versioned independently. Each has its own Maven version; `services/catalog-api/pom.xml` only aggregates them. Spring Boot's dependency management supplies compatible dependency versions; avoid overriding managed versions without a specific reason.

## API contract and frontend client

`services/catalog-api/catalog-service-spec/src/main/openapi/catalog-service.yaml` is the source of truth for the catalog API. OpenAPI Generator generates a TypeScript `fetch` client. Publish the generated client as a versioned package to an npm-compatible Artifactory repository, then pin that package version in the frontend. The OpenAPI document can also be published as a Maven artifact. Configure publishing and credentials in CI; do not commit secrets.

## Build

From `services/catalog-api/`:

```bash
mvn verify
```

Frontend setup and commands will be documented after its Next.js project is initialized.
