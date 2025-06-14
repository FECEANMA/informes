
# **Contenerización de una Aplicación React con Backend API REST usando Docker**

## 1. Título

**Contenerización de una Aplicación React con Backend API REST usando Docker**

## 2. Tiempo de duración

**45 minutos**

## 3. Fundamentos

Esta práctica tiene como objetivo contenerizar una aplicación React junto con un backend Express que expone una API REST. Ambas aplicaciones se ejecutarán en contenedores Docker y se comunicarán entre sí utilizando Docker Compose. La aplicación React mostrará una tabla con datos provenientes de una API que proporciona información sobre una entidad relacionada con el proyecto de la "regleta inteligente".

El propósito es entender cómo contenerizar aplicaciones, establecer la comunicación entre contenedores y manejar datos dinámicos en la interfaz de usuario.

## 4. Conocimientos previos

* **Docker**: Familiaridad con contenedores, imágenes y Docker Compose.
* **React**: Conocimiento básico de cómo funciona una aplicación frontend con React.
* **Node.js y Express**: Experiencia con la creación de APIs REST.
* **CORS**: Comprensión del manejo de solicitudes entre dominios.

## 5. Objetivos a alcanzar

1. Contenerizar dos aplicaciones (React y Express) usando Docker.
2. Establecer comunicación entre contenedores usando Docker Compose.
3. Crear una interfaz en React que consuma datos desde un backend Express.
4. Mostrar una tabla con datos dinámicos obtenidos desde la API.

## 6. Equipo necesario

* Computadora con Windows, Linux o macOS.
* Docker instalado.
* Acceso a Internet para clonar repositorios y descargar dependencias.

## 7. Material de apoyo

* [Documentación oficial de Docker](https://docs.docker.com/)
* [Documentación de React](https://react.dev/)
* [Documentación de Express](https://expressjs.com/)

## 8. Procedimiento

### Paso 1: backend/Dockerfile

```Dockerfile
FROM node:18
WORKDIR /app
COPY package*.json ./
RUN npm install
COPY . .
EXPOSE 4000
CMD ["npm", "start"]
```
<img src="./img_semana_9/4.png" width="800">


### Paso 2: frontend/Dockerfile

```Dockerfile
FROM node:18
WORKDIR /app
COPY package*.json ./
RUN npm install
COPY . .
EXPOSE 3000
CMD ["npm", "start"]
```
<img src="./img_semana_9/6.png" width="800">

### Paso 3: Docker Compose

```yaml
version: '3.9'

services:
  backend:
    build: ./backend
    ports:
      - "4000:4000"
    networks:
      - app-network

  frontend:
    build: ./frontend
    ports:
      - "3000:3000"
    depends_on:
      - backend
    networks:
      - app-network

networks:
  app-network:
```
<img src="./img_semana_9/8.png" width="800">

### Paso 4: Uso de Docker Compose

1. Construir y levantar los contenedores:

```bash
docker-compose up --build
```

2. Acceder a la aplicación en el navegador:

   * Frontend: [http://localhost:3000](http://localhost:3000)
   * API: [http://localhost:4000/api/voltage-events](http://localhost:4000/api/voltage-events)

## 9. Resultados esperados

* La aplicación React carga correctamente en el navegador.
* La API backend responde adecuadamente a las solicitudes del frontend.
* Los datos de la entidad "Eventos de Pico de Voltaje" se muestran correctamente en la tabla.
* La comunicación entre los contenedores funciona sin problemas.
  
<img src="./img_semana_9/11.png" width="800">

## 10. Bibliografía

* Docker, Inc. (2024). Docker Documentation
* Mikhalev, V. (2024, diciembre 10). How to dockerize a React app: A step-by-step guide for developers. Docker. https://www.docker.com/blog/how-to-dockerize-react-app/
* Koshta, P. (2021, marzo 5). Dockerize your React, Django Rest Api Application and serve using nginx. Medium. https://parthkoshta.medium.com/dockerize-your-react-django-rest-api-application-and-serve-using-nginx-6f9ccf17105b
