# Etapa 1: construir el JAR con Maven
FROM maven:3.9-eclipse-temurin-21 AS build
WORKDIR /app

# Copiamos pom y código fuente
COPY pom.xml .
COPY src ./src

# Construimos el proyecto sin tests
RUN mvn clean package -DskipTests

# Etapa 2: imagen ligera solo con el JAR
FROM eclipse-temurin:21-jdk
WORKDIR /app

# Copiamos el jar generado desde la etapa build
COPY --from=build /app/target/demo-0.0.1-SNAPSHOT.jar app.jar

EXPOSE 8080
ENV PORT=8080

ENTRYPOINT ["java","-jar","app.jar"]
