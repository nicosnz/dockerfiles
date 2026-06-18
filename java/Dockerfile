FROM maven:3.9-eclipse-temurin-21 AS dev
WORKDIR /app
COPY pom.xml ./
COPY src ./src
RUN mvn package -DskipTests -B

FROM eclipse-temurin:21-jre-alpine AS prod
WORKDIR /app
COPY --from=dev /app/target/*.jar app.jar
EXPOSE 8000
CMD ["java","-jar","app.jar"]
