# Etapa 1: construir el JAR con Maven
FROM maven:3.9.6-eclipse-temurin-17 AS build

WORKDIR /app

# Copiamos solo lo mínimo para resolver dependencias primero
COPY pom.xml .
COPY src ./src
COPY mvnw .
COPY .mvn ./.mvn

# Construimos el JAR (sin tests)
RUN chmod +x mvnw
RUN ./mvnw clean package -DskipTests

# Etapa 2: imagen mínima solo con el JRE
FROM eclipse-temurin:17-jre-alpine

WORKDIR /app

# IMPORTANTE: nombre correcto del JAR generado
COPY --from=build /app/target/demo-0.0.1-SNAPSHOT.jar app.jar

EXPOSE 8080

ENTRYPOINT ["java", "-jar", "app.jar"]
