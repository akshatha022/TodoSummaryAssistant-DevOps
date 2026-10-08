# Build stage
FROM eclipse-temurin:17-jdk AS build

WORKDIR /app

COPY . .

RUN chmod +x mvnw
RUN ./mvnw clean package -DskipTests

# Runtime stage
FROM eclipse-temurin:17-jre

WORKDIR /app

COPY --from=build --chown=1001:1001 /app/target/*.jar app.jar

USER 1001

EXPOSE 8080

ENTRYPOINT ["java", "-jar", "app.jar"]