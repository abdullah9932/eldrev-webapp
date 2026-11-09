# Catalog service OpenAPI contract

This project owns the versioned OpenAPI contract for `catalog-service`. Edit `src/main/openapi/catalog-service.yaml` as the API evolves; do not commit generated output.

## Generate the TypeScript client

From this directory, run:

```bash
mvn generate-sources
```

OpenAPI Generator writes a `typescript-fetch` client under `target/generated-client`. Publish that output as a versioned npm package to an npm-compatible Artifactory repository for the Next.js frontend to consume. Configure publishing in CI and keep registry credentials out of the repository. The OpenAPI document itself is packaged as a Maven artifact.

This project's Maven version is independent of the Spring Boot service version. Coordinate compatible contract changes with the service and publish a new spec/client version when the contract changes.
