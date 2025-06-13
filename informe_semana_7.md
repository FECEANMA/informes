# Contenerización de Aplicación React y Backend Simulado

## 1. Título

**Contenerización de una Aplicación React y un Backend Simulado**

## 2. Tiempo de duración

**30 minutos**

## 3. Fundamentos

En esta práctica se utiliza Docker y Docker Compose para desplegar de forma automatizada un entorno de desarrollo compuesto por:

* Un contenedor con una **aplicación React (frontend)**,
* Un contenedor con un **backend simulado (mockAPI)**.

Este entorno está definido mediante un archivo `docker-compose.yml` que facilita la construcción y puesta en marcha de los servicios con un solo comando. También se define una **red personalizada** para la comunicación entre contenedores.

La aplicación React depende del backend para funcionar correctamente, por lo que el entorno permite levantar ambos componentes de manera coordinada.

Este enfoque asegura un entorno portable, reproducible y fácil de ejecutar en cualquier máquina con Docker instalado.

![Diagrama Docker React + Backend](https://miro.medium.com/v2/resize\:fit:1400/1*eZkzxE0RWDXgRyfVdfMHbw.png)

### Imagen 1-1: Diagrama conceptual de los contenedores React y mockAPI

## 4. Conocimientos previos

* **Docker**: Creación de imágenes, redes, contenedores y volúmenes.
* **Docker Compose**: Configuración de múltiples servicios con archivos YAML.
* **React.js**: Conocimiento básico de aplicaciones frontend.
* **Node.js y npm**: Instalación y ejecución de proyectos.

## 5. Objetivos a alcanzar

* Clonar y verificar el correcto funcionamiento de una aplicación React y un backend simulado.
* Crear una imagen Docker personalizada para el frontend.
* Crear un entorno multi-contenedor con `docker-compose`.
* Ejecutar y conectar ambos servicios en una red Docker.

## 6. Equipo necesario

* Computadora con Windows, Linux o macOS.
* Docker y Docker Compose instalados.
* Acceso a Internet para clonar repositorios e imágenes.

## 7. Material de apoyo

* [Documentación oficial de Docker](https://docs.docker.com/)
* [Documentación de React](https://react.dev/)
* Repositorio del frontend: [https://github.com/Daviddotcoms/suda-frontend-s6](https://github.com/Daviddotcoms/suda-frontend-s6)
* Repositorio del backend simulado: [https://github.com/Daviddotcoms/mockAPI](https://github.com/Daviddotcoms/mockAPI)

## 8. Procedimiento

### Paso 1: Clonar los proyectos

```bash
git clone https://github.com/Daviddotcoms/suda-frontend-s6.git
git clone https://github.com/Daviddotcoms/mockAPI.git
```

### Paso 2: Crear el archivo Dockerfile para el frontend

Ubicado en `suda-frontend-s6/`:

```Dockerfile
FROM node:18-alpine AS build
WORKDIR /app
COPY package*.json ./
RUN npm install
COPY . .
RUN npm run build

FROM nginx:stable-alpine
COPY --from=build /app/dist /usr/share/nginx/html
EXPOSE 80
CMD ["nginx", "-g", "daemon off;"]
```

### Paso 3: Crear el archivo `docker-compose.yml`

```yaml
version: '3.8'

services:
  frontend:
    build: ./suda-frontend-s6
    ports:
      - "80:80"
    depends_on:
      - mockapi
    networks:
      - react-network

  mockapi:
    image: node:18-alpine
    working_dir: /app
    volumes:
      - ./mockAPI:/app
    command: sh -c "npm install && npm start"
    ports:
      - "3001:3001"
    networks:
      - react-network

networks:
  react-network:
```

### Paso 4: Ejecutar los servicios

Ubicarse en el directorio donde se encuentra `docker-compose.yml` y ejecutar:

```bash
docker-compose up --build -d
```

### Paso 5: Verificar funcionamiento

* Acceder a la aplicación React en: [http://localhost](http://localhost)
* El backend simulado estará disponible en: [http://localhost:3001](http://localhost:3001)

## 9. Resultados esperados

* La aplicación React funciona correctamente y se comunica con el backend.
* Ambos servicios están activos y visibles en `docker ps`.
* El contenedor frontend responde en el navegador.
* La API mock funciona y entrega datos esperados.

## 10. Bibliografía

* Docker, Inc. (2024). [Docker Documentation](https://docs.docker.com/)
* React.js (2024). [Documentación oficial de React](https://react.dev/)
* GitHub: Repositorio frontend - [https://github.com/Daviddotcoms/suda-frontend-s6](https://github.com/Daviddotcoms/suda-frontend-s6)
* GitHub: Repositorio mockAPI - [https://github.com/Daviddotcoms/mockAPI](https://github.com/Daviddotcoms/mockAPI)
* DockerHub (Nginx) - [https://hub.docker.com/\_/nginx](https://hub.docker.com/_/nginx)
* DockerHub (Node) - [https://hub.docker.com/\_/node](https://hub.docker.com/_/node)

---
