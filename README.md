# eldrev-webapp

Monorepo for the Eldrev Next.js frontend and backend services.

## Layout

```text
frontend/                         Next.js application and Dockerfile
services/
  catalog-api/
    pom.xml                       Maven reactor for catalog projects
    catalog-service/              Spring Boot backend and Dockerfile
    catalog-service-spec/         Versioned OpenAPI contract and TS client generation
compose.yaml                      Local frontend + backend orchestration
```

The catalog service and OpenAPI contract are versioned independently. Each has its own Maven version; `services/catalog-api/pom.xml` only aggregates them. Spring Boot's dependency management supplies compatible dependency versions; avoid overriding managed versions without a specific reason.

## API contract and frontend client

`services/catalog-api/catalog-service-spec/src/main/openapi/catalog-service.yaml` is the source of truth for the catalog API. OpenAPI Generator generates a TypeScript `fetch` client. Publish the generated client as a versioned package to an npm-compatible Artifactory repository, then pin that package version in the frontend. The OpenAPI document can also be published as a Maven artifact. Configure publishing and credentials in CI; do not commit secrets.

## Docker

The backend image can be built now from the repository root:

```bash
docker build -f services/catalog-api/catalog-service/Dockerfile -t eldrev/catalog-service .
```

The frontend Dockerfile is ready for the Next.js app, but `frontend/` currently contains only its README, so it cannot build until the app's `package.json`, lockfile, and source are added. Once initialized, build and run both via Compose:

```bash
docker compose up --build
```

The frontend is exposed on port 3000 and the catalog service on port 8080. The Docker Compose environment variable `NEXT_PUBLIC_CATALOG_API_URL` defaults to `http://localhost:8080`; set it as needed for your deployment. Never bake secrets into images.

## Maven build

From `services/catalog-api/`:

```bash
mvn verify
```
