# Etapa 1: Compilación
FROM maven:3.8.8-eclipse-temurin-17 AS build
WORKDIR /app

COPY pom.xml .
COPY src ./src

RUN mvn clean package -DskipTests

# Etapa 2: Imagen final
FROM eclipse-temurin:17-jre-alpine
WORKDIR /app

COPY --from=build /app/target/*.jar app.jar

# Exponer el puerto interno
EXPOSE 8080

# NUEVA LÍNEA OPTIMIZADA: Control estricto de memoria RAM
CMD ["java", "-XX:+UseSerialGC", "-Xss512k", "-Xmx180m", "-jar", "app.jar"]