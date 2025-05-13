# Implementación de WordPress con MySQL y phpMyAdmin usando Docker Compose

## 1. Título

**Implementación de WordPress con MySQL y phpMyAdmin usando Docker Compose**

## 2. Tiempo de duración

**30 minutos**

## 3. Fundamentos

Se utiliza Docker y Docker Compose para levantar un entorno completo de WordPress de forma automatizada, usando contenedores. Este entorno incluye:

- Un contenedor con WordPress,
- Un contenedor con MySQL como base de datos,
- Un contenedor con phpMyAdmin para administrar MySQL gráficamente.

**Docker Compose** permite definir todos los servicios requeridos en un archivo YAML (`docker-compose.yml`), lo que facilita la creación, configuración y ejecución del entorno completo con un solo comando.

Se definen también una **red personalizada** (`wp-network`) que conecta todos los servicios, y **volúmenes persistentes** (`wordpress_data`, `db_data`) para garantizar que los datos no se pierdan al reiniciar o eliminar los contenedores.

Este enfoque proporciona una solución portátil, reproducible y aislada del sistema operativo anfitrión, ideal para entornos de desarrollo.

![Diagrama Docker](https://miro.medium.com/v2/resize:fit:1400/1*eZkzxE0RWDXgRyfVdfMHbw.png)

### Imagen 1-1: Diagrama de contenedores en Docker

## 4. Conocimientos previos

- **Docker**: Fundamentos de contenedores, imágenes, redes y volúmenes.
- **Docker Compose**: Uso básico de archivos YAML y el comando `docker-compose`.
- **WordPress y phpMyAdmin**: Conocimiento general de cómo se utilizan en desarrollo web.

## 5. Objetivos a alcanzar

- Construir un entorno WordPress usando `docker-compose`.
- Crear y conectar contenedores WordPress, MySQL y phpMyAdmin.
- Configurar una red y volúmenes persistentes.
- Acceder a WordPress y gestionar la base de datos con phpMyAdmin.

## 6. Equipo necesario

- Computadora con Windows, Linux o macOS.
- Docker instalado.
- Acceso a Internet para descargar las imágenes oficiales.

## 7. Material de apoyo

- [Documentación oficial de Docker](https://docs.docker.com/)
- Guía de práctica de la asignatura
- [Cheat sheet de comandos Linux y Docker](https://dockerlabs.collabnix.com/docker/cheatsheet/)

## 8. Procedimiento

### Paso 1: Crear el archivo `docker-compose.yml`

Crear un archivo `docker-compose.yml` con el siguiente contenido:

```yaml
version: '3.8'

services:
  wordpress:
    image: wordpress:latest
    restart: always
    ports:
      - "8000:80"
    environment:
      WORDPRESS_DB_HOST: db:3306
      WORDPRESS_DB_USER: wordpress
      WORDPRESS_DB_PASSWORD: wordpress
      WORDPRESS_DB_NAME: wordpress
    volumes:
      - wordpress_data:/var/www/html
    networks:
      - wp-network

  db:
    image: mysql:5.7
    restart: always
    environment:
      MYSQL_DATABASE: wordpress
      MYSQL_USER: wordpress
      MYSQL_PASSWORD: wordpress
      MYSQL_ROOT_PASSWORD: rootpass
    volumes:
      - db_data:/var/lib/mysql
    networks:
      - wp-network

  phpmyadmin:
    image: phpmyadmin/phpmyadmin
    restart: always
    ports:
      - "8080:80"
    environment:
      PMA_HOST: db
      MYSQL_ROOT_PASSWORD: rootpass
    networks:
      - wp-network

networks:
  wp-network:

volumes:
  wordpress_data:
  db_data:
```
### Paso 2: Ejecutar los contenedores
Ejecutar el siguiente comando en la misma carpeta donde está ubicado el archivo docker-compose.yml:

```
docker-compose up -d
```
**Esto descargará las imágenes necesarias y levantará los contenedores en segundo plano.**

### Paso 3: Verificar el entorno

- Acceder a WordPress desde http://localhost:8000.

- Acceder a phpMyAdmin desde http://localhost:8080.

## 9. Resultados esperados
- WordPress funcional: Se puede acceder desde el navegador, completar la instalación y comenzar a usarlo.

- phpMyAdmin: Permite gestionar la base de datos de WordPress gráficamente.

- Datos persistentes: Gracias a los volúmenes wordpress_data y db_data, los datos se conservan tras reiniciar los contenedores.

## 10. Bibliografía
- Docker, Inc. (2023). Docker Documentation. Recuperado de https://docs.docker.com/

- Gómez, S. (s/f). Levantar un WordPress con Compose - Taller de Docker. Github.io. Recuperado el 13 de mayo de 2025, de https://aulasoftwarelibre.github.io/taller-de-docker/docker-compose/

- DockerHub (phpMyAdmin). Recuperado de https://hub.docker.com/_/phpmyadmin

- DockerHub (WordPress). Recuperado de https://hub.docker.com/_/wordpress

- DockerHub (MySQL). Recuperado de https://hub.docker.com/_/mysql
