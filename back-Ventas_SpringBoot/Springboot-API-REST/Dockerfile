# ETAPA 1: Construcción (Build)
FROM maven:3.9-eclipse-temurin-17-alpine AS build
WORKDIR /app

# Copiar el archivo de dependencias
COPY pom.xml .
# Descargar dependencias para aprovechar la caché de Docker
RUN mvn dependency:go-offline

# Copiar el código fuente y compilar el proyecto
COPY src ./src
RUN mvn clean package -DskipTests

# ETAPA 2: Imagen de ejecución (Runtime)
FROM eclipse-temurin:17-jre-alpine
WORKDIR /app

# Crear grupo y usuario no-root para cumplir con el estándar de seguridad (IE6)
RUN addgroup -S springgroup && adduser -S springuser -G springgroup

# Copiar el archivo JAR desde la etapa de compilación
COPY --from=build /app/target/*.jar app.jar

# Dar permisos al usuario sobre el archivo ejecutable
RUN chown springuser:springgroup app.jar

# Cambiar al usuario no-root
USER springuser

# Puerto (Usa 8080 para Ventas / 8081 para Despachos)
EXPOSE 8080

ENTRYPOINT ["java", "-jar", "app.jar"]