# Etapa 1: construir el .jar con Maven
FROM maven:3.9.6-eclipse-temurin-17 AS build
WORKDIR /app

COPY pom.xml .
COPY src ./src

RUN mvn clean package -DskipTests

# Etapa 2: imagen mínima con solo el JRE
FROM eclipse-temurin:17-jre-alpine
WORKDIR /app

# IMPORTANTE: cambia el nombre del jar si es diferente
COPY --from=build /app/target/demo-0.0.1-SNAPSHOT.jar app.jar

ENV PORT=8080

EXPOSE 8080

ENTRYPOINT ["java", "-jar", "app.jar"]
