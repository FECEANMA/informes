---

# Implementación de Backend Java con PostgreSQL y pgAdmin usando Docker Compose

## 1. Título

**Implementación de Backend Java con PostgreSQL y pgAdmin usando Docker Compose**

## 2. Tiempo de duración

**40 minutos**

## 3. Fundamentos

Se utiliza Docker y Docker Compose para automatizar el despliegue de una aplicación backend Java (Spring Boot), acompañada de una base de datos PostgreSQL y un panel de administración pgAdmin. Este entorno permite levantar los servicios de forma rápida y aislada, ideal para desarrollo y pruebas locales.

**Docker Compose** permite definir y ejecutar múltiples contenedores como un solo servicio, con sus redes, volúmenes y dependencias claramente especificadas en un archivo YAML (`docker-compose.yml`).

Este entorno incluye:

* Un contenedor con la aplicación backend Java (compilada con Maven).
* Un contenedor con PostgreSQL como sistema de gestión de base de datos.
* Un contenedor con pgAdmin para la administración gráfica de PostgreSQL.

Se definen también una **red personalizada** (`backend_network`) para la comunicación entre servicios, y **volúmenes persistentes** (`postgres_data`, `pgadmin_data`) para garantizar la conservación de datos.

![Diagrama de servicios Docker backend]()

### Imagen 1-1: Diagrama de contenedores en Docker

## 4. Conocimientos previos

* **Docker**: Imágenes, contenedores, volúmenes, redes.
* **Docker Compose**: Uso básico de `docker-compose.yml`.
* **Spring Boot / Java**: Comprensión general de aplicaciones backend.
* **PostgreSQL y pgAdmin**: Nociones de base de datos relacional y su gestión.

## 5. Objetivos a alcanzar

* Desplegar un entorno backend completo usando `docker-compose`.
* Configurar PostgreSQL y pgAdmin con volúmenes persistentes.
* Construir la imagen del backend con Docker (multi-stage).
* Verificar conectividad entre aplicación y base de datos.
* Acceder a pgAdmin para administración de datos.

## 6. Equipo necesario

* Computadora con Windows, Linux o macOS.
* Docker y Docker Compose instalados.
* Conexión a Internet para descargar las imágenes base.
* Repositorio base: [https://github.com/maguaman2/tendencias-mar22-security.git](https://github.com/maguaman2/tendencias-mar22-security.git)

## 7. Material de apoyo

* [Documentación oficial de Docker](https://docs.docker.com/)
* [Guía Multi-stage Builds en Docker](https://docs.docker.com/build/building/multi-stage/)
* [DockerHub - PostgreSQL](https://hub.docker.com/_/postgres)
* [DockerHub - pgAdmin](https://hub.docker.com/r/dpage/pgadmin4)
* [Guía oficial de Spring Boot](https://spring.io/projects/spring-boot)

## 8. Procedimiento

### Paso 1: Crear archivo `.env`

```env
POSTGRES_USER=admin
POSTGRES_PASSWORD=admin
POSTGRES_DB=mydb
PGADMIN_EMAIL=admin@pgadmin.com
PGADMIN_PASSWORD=admin
```

### Paso 2: Crear archivo `docker-compose.yml`

```yaml
version: '3.9'

services:
  postgres:
    image: postgres:15
    container_name: postgres_db
    environment:
      POSTGRES_USER: ${POSTGRES_USER}
      POSTGRES_PASSWORD: ${POSTGRES_PASSWORD}
      POSTGRES_DB: ${POSTGRES_DB}
    volumes:
      - postgres_data:/var/lib/postgresql/data
    networks:
      - backend_network
    restart: always

  pgadmin:
    image: dpage/pgadmin4
    container_name: pgadmin
    environment:
      PGADMIN_DEFAULT_EMAIL: ${PGADMIN_EMAIL}
      PGADMIN_DEFAULT_PASSWORD: ${PGADMIN_PASSWORD}
    ports:
      - "5050:80"
    volumes:
      - pgadmin_data:/var/lib/pgadmin
    networks:
      - backend_network
    depends_on:
      - postgres
    restart: always

  backend:
    build:
      context: .
      dockerfile: Dockerfile
    container_name: backend
    environment:
      SPRING_DATASOURCE_URL: jdbc:postgresql://postgres:5432/${POSTGRES_DB}
      SPRING_DATASOURCE_USERNAME: ${POSTGRES_USER}
      SPRING_DATASOURCE_PASSWORD: ${POSTGRES_PASSWORD}
      SPRING_PROFILES_ACTIVE: dev
    ports:
      - "8080:8080"
    networks:
      - backend_network
    depends_on:
      - postgres
    restart: always

networks:
  backend_network:
    driver: bridge

volumes:
  postgres_data:
  pgadmin_data:
```

### Paso 3: Crear `Dockerfile` con multi-stage build

```dockerfile
# Etapa de construcción
FROM maven:3.8.6-openjdk-17-slim AS build

WORKDIR /app
COPY backend/pom.xml .
RUN mvn dependency:go-offline

COPY backend/src ./src
RUN mvn clean package -DskipTests

# Etapa de ejecución
FROM openjdk:17-jdk-slim

WORKDIR /app
COPY --from=build /app/target/backend-1.0.jar backend.jar

EXPOSE 8080
ENTRYPOINT ["java", "-jar", "backend.jar"]
```

### Paso 4: Levantar los contenedores

```bash
docker-compose up --build -d
```

### Paso 5: Verificar conectividad

* Acceder a [http://localhost:5050](http://localhost:5050) con el correo y contraseña de `.env`.
* Crear un nuevo servidor con:

  * Host: `postgres`
  * Base de datos: `mydb`
  * Usuario: `admin`
  * Contraseña: `admin`
* Acceder a [http://localhost:8080](http://localhost:8080) para verificar el backend.

## 9. Resultados esperados

* El backend Java estará corriendo en el puerto 8080, conectado a la base de datos.
* pgAdmin accesible para la administración visual de la base de datos PostgreSQL.
* Los datos se conservan aunque se apaguen los contenedores, gracias a los volúmenes `postgres_data` y `pgadmin_data`.
* Imagen del backend optimizada gracias a la técnica multi-stage build.

## 10. Bibliografía

* Docker, Inc. (2023). [Docker Documentation](https://docs.docker.com/)
* PostgreSQL Docker Image. [DockerHub](https://hub.docker.com/_/postgres)
* pgAdmin Docker Image. [DockerHub](https://hub.docker.com/r/dpage/pgadmin4)
* OpenJDK Base Images. [DockerHub](https://hub.docker.com/_/openjdk)
* Spring Boot Docs. [https://spring.io/](https://spring.io/)
* Guía Multi-stage builds. [https://docs.docker.com/build/building/multi-stage/](https://docs.docker.com/build/building/multi-stage/)

---
