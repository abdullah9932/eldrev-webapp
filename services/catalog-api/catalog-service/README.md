# Catalog service

Spring Boot application for catalog functionality. Its Maven version is managed independently from `catalog-service-spec`.

## Build and run

```bash
mvn verify
mvn spring-boot:run
```

The API contract is maintained in the sibling `../catalog-service-spec` project. Add endpoints here alongside corresponding contract changes and tests.
