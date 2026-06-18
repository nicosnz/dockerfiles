FROM maven:3.9-eclipse-temurin-21 AS build
WORKDIR /app
COPY ./app/pom.xml ./
COPY ./app/src ./src
RUN mvn package -DskipTests -B

FROM eclipse-temurin:21-jre AS runner
RUN apt-get update && apt-get install -y --no-install-recommends curl && rm -rf /var/lib/apt/lists/*
WORKDIR /app
COPY --from=build /app/target/*.jar app.jar
EXPOSE 8080
HEALTHCHECK --interval=10s --timeout=5s --start-period=30s --retries=3 CMD curl -f http://localhost:8080/health || exit 1
CMD [ "java","-jar","app.jar" ]
