# Catalog service

Spring Boot application for catalog functionality. Its Maven version is managed independently from `catalog-service-spec`.

## Build and run

```bash
mvn verify
mvn spring-boot:run
```

The API contract is maintained in the sibling `../catalog-service-spec` project. Add endpoints here alongside corresponding contract changes and tests.

## Docker

From the repository root:

```bash
docker build -f services/catalog-api/catalog-service/Dockerfile -t eldrev/catalog-service .
docker run --rm -p 8080:8080 eldrev/catalog-service
```
