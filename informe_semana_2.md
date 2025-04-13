# Práctica Servidor Web con Nginx en Docker

## 1. Título  
**Despliegue de dos servidores web Nginx personalizados en contenedores Docker**

---

## 2. Tiempo de duración  
**40 minutos**

---

## 3. Fundamentos

La virtualización ha evolucionado hacia contenedores, donde Docker se ha convertido en una de las herramientas más utilizadas para la creación, distribución y ejecución de aplicaciones en entornos aislados. Docker posibilita encapsular una aplicación y todas sus dependencias en un contenedor, asegurando que opere de igual manera en cualquier ambiente.

En este ejercicio, utilizamos **Nginx**, un servidor web altamente eficiente, famoso por su eficacia al servir contenido estático, su reducido uso de recursos y su sencilla configuración.

Cada contenedor ejecuta su propio servidor Nginx escuchando en diferentes puertos del sistema anfitrión. Uno muestra información institucional y el otro, información personal del estudiante. La manipulación del archivo `index.html` permite personalizar la salida web que cada contenedor entrega al navegar por los puertos correspondientes.

**Conceptos importantes:**

- **Docker**: Plataforma para desarrollar, enviar y ejecutar aplicaciones en contenedores.
- **Contenedor**: Unidad estandarizada de software que agrupa código y todas sus dependencias.
- **Nginx**: Servidor web liviano y de alto rendimiento, también usado como balanceador de carga o proxy inverso.
- **HTML**: Lenguaje de marcado usado para crear el contenido visible de las páginas web.
- **Volúmenes y comandos Docker**: Permiten copiar archivos entre el host y los contenedores.

---

## 4. Conocimientos previos

Para esta práctica, el estudiante debe tener claro:

- Comandos básicos de Linux (ls, vi, nano, etc.)
- Uso de terminal o consola
- Conocimientos básicos de HTML
- Manejo de Docker: instalación, imágenes, contenedores

---

## 5. Objetivos a alcanzar

- Implementar contenedores web con Nginx usando Docker.
- Personalizar contenido web dentro de contenedores mediante archivos HTML.
- Manipular archivos de configuración dentro de un contenedor.

---

## 6. Equipo necesario

- Computadora con sistema operativo
- Docker Playground
- Conexión a Internet
- Navegador web 

---

## 7. Material de apoyo

- [Documentación oficial de Docker](https://docs.docker.com/)
- Guía de asignatura
- Comandos de Linux
- Editor de texto: `nano` o `vi`

---

## 8. Procedimiento

### Paso 1: Crear el primer contenedor Nginx (nginx1)  
```bash
docker run -d --name nginx1 -p 8089:80 nginx
