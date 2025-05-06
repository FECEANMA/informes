# Implementación de un entorno WordPress utilizando contenedores Docker

## 1. Título

**Implementación de un entorno WordPress utilizando contenedores Docker**

## 2. Tiempo de duración

**45 minutos**

## 3. Fundamentos

Se utiliza Docker para crear un entorno aislado y flexible para ejecutar un sitio web basado en WordPress, con MySQL y phpMyAdmin, sin necesidad de instalar software directamente en el sistema operativo. Docker es una plataforma de software que permite automatizar la implementación de aplicaciones dentro de contenedores. Un contenedor es una unidad estándar de software que empaqueta el código y todas sus dependencias, lo que permite ejecutar aplicaciones de manera rápida y confiable en cualquier entorno.

Docker usa imágenes, que son plantillas inmutables de sistemas de archivos, para crear contenedores. En este caso, se utilizaron imágenes oficiales de MySQL y WordPress, junto con la imagen de phpMyAdmin para gestionar la base de datos de MySQL.

Un concepto clave es la creación de redes y volúmenes. Docker permite crear redes virtuales que conectan contenedores, facilitando la comunicación entre ellos. En esta práctica, se creó una red `wordpress-network` para que los contenedores de WordPress, MySQL y phpMyAdmin pudieran interactuar entre sí. Además, se utilizaron volúmenes para almacenar de manera persistente los datos de la base de datos MySQL y los archivos de WordPress, lo que garantiza que la información no se pierda cuando los contenedores se detengan o eliminen.

Docker también simplifica la administración de contenedores, permitiendo iniciar, detener y gestionar contenedores de manera eficiente utilizando comandos simples, como `docker run`, `docker volume create` y `docker network create`. Este enfoque facilita el desarrollo, despliegue y mantenimiento de aplicaciones sin tener que preocuparse por las dependencias del sistema operativo subyacente.

### Imagen 1-1: Diagrama de contenedores en Docker

<img src="[https://dondocker.com/wp-content/uploads/2016/05/redes_aisladas_dondocker.png](https://miro.medium.com/v2/resize:fit:1400/1*eZkzxE0RWDXgRyfVdfMHbw.png)" width="800">

## 4. Conocimientos previos

Para realizar esta práctica, el estudiante necesita tener claros los siguientes temas:

- **Docker**: Conocimiento básico sobre la creación y gestión de contenedores con Docker.
- **Comandos de Docker**: Uso de comandos como `docker run`, `docker network create`, `docker volume create`, entre otros.
- **Redes y Volúmenes en Docker**: Comprender la importancia de las redes para la comunicación entre contenedores y el uso de volúmenes para persistencia de datos.
- **Gestión básica de bases de datos**: Conocimientos sobre bases de datos MySQL, creación de usuarios y bases de datos.

## 5. Objetivos a alcanzar

- Crear y configurar contenedores Docker para WordPress, MySQL y phpMyAdmin.
- Implementar una red Docker para permitir la comunicación entre los contenedores.
- Usar volúmenes Docker para asegurar la persistencia de datos.
- Acceder a WordPress a través de un navegador y administrar la base de datos mediante phpMyAdmin.

## 6. Equipo necesario

- Computadora con sistema operativo **Windows/Linux/Mac**.
- **Docker Desktop** instalado en el equipo (versión 20.x o superior).
- Conexión a internet para descargar las imágenes necesarias de Docker.
- Editor de texto para ver los comandos y realizar modificaciones si es necesario.

## 7. Material de apoyo

- **Documentación oficial de Docker**: [https://docs.docker.com/](https://docs.docker.com/)
- **Guía de asignatura**: Documento proporcionado por el docente con detalles adicionales de la práctica.
- **Cheat sheet de Linux**: Guía rápida de comandos de Linux que puede ser útil durante el proceso de ejecución de Docker.
- **Tutoriales de WordPress**: [https://wordpress.org/support/](https://wordpress.org/support/)

## 8. Procedimiento

### Paso 1: Crear una red Docker para los contenedores

Se comienza creando una red personalizada para que los contenedores puedan comunicarse entre sí:

```bash
docker network create wordpress-network
