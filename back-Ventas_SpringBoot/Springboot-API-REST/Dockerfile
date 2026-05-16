# Etapa 1: Compilación (Docker descarga Maven interno para compilar el .jar)
FROM maven:3.8.8-eclipse-temurin-17 AS build
WORKDIR /app

# Copiar el archivo de configuración y el código fuente
COPY pom.xml .
COPY src ./src

# Compilar y empaquetar el .jar saltándose los tests
RUN mvn clean package -DskipTests

# Etapa 2: Imagen final ligera de ejecución
FROM eclipse-temurin:17-jre-alpine
WORKDIR /app

# Copiar el archivo .jar generado en la Etapa 1
COPY --from=build /app/target/*.jar app.jar

# Exponer el puerto estándar del Backend de Ventas
EXPOSE 8080

# Comando para ejecutar la aplicación
CMD ["java", "-jar", "app.jar"]