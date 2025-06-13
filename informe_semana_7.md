# Contenerización de Aplicación React y Backend Simulado

## 1. Título

**Contenerización de una Aplicación React y un Backend Simulado**

## 2. Tiempo de duración

**30 minutos**

## 3. Fundamentos

En esta práctica se utiliza Docker para desplegar manualmente un entorno de desarrollo compuesto por:

Un contenedor con una aplicación React (frontend),

Un contenedor con un backend simulado (mockAPI).

A diferencia del uso de Docker Compose, aquí se levantan los contenedores de forma manual e individual, permitiendo mayor control sobre el proceso de construcción y ejecución de cada componente. 

Este enfoque proporciona un entorno portable, reproducible y controlado, ideal para comprender cómo se construyen y ejecutan contenedores.

![Diagrama Docker React + Backend](https://miro.medium.com/v2/resize\:fit:1400/1*eZkzxE0RWDXgRyfVdfMHbw.png)

### Imagen 1-1: Diagrama conceptual de los contenedores React y mockAPI

## 4. Conocimientos previos

* **Docker**: Creación de imágenes, contenedores y volúmenes.
* **React.js**: Conocimiento básico de aplicaciones frontend.
* **Node.js y npm**: Instalación y ejecución de proyectos.

## 5. Objetivos a alcanzar

* Clonar y verificar el correcto funcionamiento de una aplicación React y un backend simulado.
* Crear una imagen Docker personalizada para el frontend.
* Levantar manualmente ambos contenedores.
* Comprobar la correcta comunicación entre frontend y backend.

## 6. Equipo necesario

* Computadora con Windows, Linux o macOS.
* Docker instalado.
* Acceso a Internet para clonar repositorios y descargar imágenes.

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
# Imagen base
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

### Paso 4: Construir la imagen Docker

```bash
docker build -t suda-frontend .
```

### Paso 5: Ejecutar los contenedores (mockAPI + frontend)

```bash
docker run -d -p 3001:3001 node:18-alpine sh -c "apk add --no-cache git && git clone https://github.com/Daviddotcoms/mockAPI.git && cd mockAPI && npm install && npm start"
```

```bash
docker run -d -p 80:80 suda-frontend
```

* Acceder a la aplicación React en: [http://localhost](http://localhost)
* El backend simulado estará disponible en: [http://localhost:3001](http://localhost:3001)

## 9. Resultados esperados

* La aplicación React carga correctamente en el navegador.
* El contenedor de backend responde a solicitudes del frontend.
* Los datos de prueba del backend se visualizan correctamente en la interfaz.
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
