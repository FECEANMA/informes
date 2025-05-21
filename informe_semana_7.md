# **Contenerización de una Aplicación React con Backend Simulado usando Docker**

## 1. Título

**Contenerización de una Aplicación React con Backend Simulado usando Docker**

## 2. Tiempo de duración

**45 minutos**

## 3. Fundamentos

En esta práctica se utilizó **Docker** para contenerizar una aplicación frontend desarrollada en **React**, la cual depende de un servicio backend simulado, también empaquetado en un contenedor independiente. Esta estrategia permite ejecutar ambos servicios de manera aislada, reproducible y sin depender del sistema operativo anfitrión.

Se creó un **Dockerfile** para generar la imagen del frontend y se definió un contenedor separado para el backend. Ambos contenedores se ejecutan en una **red Docker personalizada**, permitiendo la comunicación directa entre frontend y backend sin necesidad de exponer puertos innecesarios.

Este enfoque es muy útil para entornos de desarrollo y pruebas, ya que permite ejecutar proyectos full-stack de forma sencilla, segura y portátil.

---

## 4. Conocimientos previos

* **Docker**: Creación de imágenes, ejecución de contenedores, redes personalizadas.
* **Node.js y React**: Conocimientos básicos de desarrollo frontend con React.
* **Backend API REST**: Familiaridad con servicios backend simulados y consumo de APIs desde React.

---

## 5. Objetivos a alcanzar

* Clonar y ejecutar una aplicación React dependiente de un backend simulado.
* Crear un Dockerfile para la aplicación frontend.
* Generar imágenes Docker tanto para frontend como backend.
* Ejecutar ambos servicios en contenedores conectados mediante una red Docker personalizada.
* Verificar el correcto funcionamiento del sistema completo desde el navegador.

---

## 6. Equipo necesario

* Computadora con Windows, Linux o macOS.
* Docker instalado.
* Acceso a Internet para clonar los repositorios y descargar las imágenes base.

---

## 7. Material de apoyo

* [Documentación oficial de Docker](https://docs.docker.com/)
* Documentación oficial de React y Node.js
* Guías y referencias de prácticas anteriores de la asignatura
* [Cheat sheet de comandos Docker](https://dockerlabs.collabnix.com/docker/cheatsheet/)

---

## 8. Procedimiento

### Paso 1: Clonar los repositorios

```bash
git clone https://github.com/usuario/frontend-app
git clone https://github.com/usuario/backend-mock
```

---

### Paso 2: Verificar funcionamiento local

**Frontend:**

```bash
cd frontend-app
npm install
npm start
```

**Backend simulado:**

```bash
cd backend-mock
npm install
npm start
```

---

### Paso 3: Crear el Dockerfile para el frontend
```
Dockerfile
```
# Etapa de construcción
```
FROM node:18 AS build
WORKDIR /app
COPY . .
RUN npm install
RUN npm run build
```
# Etapa de producción
```
FROM nginx:alpine
COPY --from=build /app/build /usr/share/nginx/html
COPY nginx.conf /etc/nginx/conf.d/default.conf

EXPOSE 80
CMD ["nginx", "-g", "daemon off;"]
```

**nginx.conf:**
```
nginx
server {
  listen 80;
  server_name localhost;

  location / {
    root /usr/share/nginx/html;
    index index.html index.htm;
    try_files $uri /index.html;
  }
}

```
---

### Paso 4: Crear Dockerfile para el backend simulado
```
Dockerfile
FROM node:18
WORKDIR /app
COPY . .
RUN npm install
EXPOSE 3001
CMD ["npm", "start"]

```
---

### Paso 5: Construir las imágenes

```bash
# Frontend
cd frontend-app
docker build -t react-frontend-app .

# Backend
cd backend-mock
docker build -t mock-backend .
```

---

### Paso 6: Crear red personalizada y ejecutar contenedores

```bash
docker network create react-network

docker run -d --name backend --network react-network -p 3001:3001 mock-backend

docker run -d --name frontend --network react-network -p 80:80 react-frontend-app
```

*Importante:* Asegúrarse de que el frontend esté configurado para comunicarse con el backend usando http://backend:3001.

---

### Paso 7: Verificar funcionamiento

Abrir en el navegador:

* **Frontend React**: http://localhost
* El frontend debe poder comunicarse correctamente con el backend simulado.

---

## 9. Resultados esperados

* La aplicación React se visualiza correctamente en el navegador.
* La interacción con el backend simulado (consultas, carga de datos, etc.) funciona de forma fluida.
* Ambos contenedores están aislados pero conectados mediante red Docker.
* Las imágenes creadas pueden ser reutilizadas en otros entornos sin necesidad de reinstalación o configuración adicional.

---

## 10. Bibliografía

* Docker Inc. (2024). *Docker Documentation*. Recuperado de [https://docs.docker.com/](https://docs.docker.com/)
* ReactJS.org. (2024). *Documentación oficial de React*. Recuperado de [https://reactjs.org/](https://reactjs.org/)
* Node.js Foundation. (2024). *Node.js Documentation*. Recuperado de [https://nodejs.org/en/docs/](https://nodejs.org/en/docs/)
* DockerHub (Nginx). [https://hub.docker.com/\_/nginx](https://hub.docker.com/_/nginx)
* DockerHub (Node.js). [https://hub.docker.com/\_/node](https://hub.docker.com/_/node)


