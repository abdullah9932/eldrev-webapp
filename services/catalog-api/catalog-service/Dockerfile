# Build the Spring Boot application from the repository root:
# docker build -f services/catalog-api/catalog-service/Dockerfile -t eldrev/catalog-service .
FROM maven:3.9-eclipse-temurin-21 AS build
WORKDIR /workspace

COPY services/catalog-api/catalog-service/pom.xml services/catalog-api/catalog-service/pom.xml
COPY services/catalog-api/catalog-service/src services/catalog-api/catalog-service/src
RUN mvn -B -f services/catalog-api/catalog-service/pom.xml -DskipTests package

FROM eclipse-temurin:21-jre
WORKDIR /app
RUN useradd --system --uid 10001 appuser
COPY --from=build /workspace/services/catalog-api/catalog-service/target/catalog-service-*.jar /app/app.jar
USER appuser
EXPOSE 8080
ENTRYPOINT ["java", "-jar", "/app/app.jar"]
