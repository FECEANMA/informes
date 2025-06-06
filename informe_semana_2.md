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

Para esta práctica, se debe tener claro:

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

- Documentación oficial de Docker
- Guía de asignatura
- Comandos de Linux
- Editor de texto: `nano` o `vi`

---

## 8. Procedimiento

### Paso 1: Crear el primer contenedor Nginx (nginx1)  
```bash
docker run -d --name nginx1 -p 8089:80 nginx
```
<img src="./img_semana_2/1.png" width="800">

### Paso 2: Crear el segundo contenedor Nginx (nginx2)  
```bash
docker run -d --name nginx2 -p 8090:80 nginx
```
<img src="./img_semana_2/2.png" width="800">

### Paso 3: Copiar el archivo index.html desde nginx1 al host  
```bash
docker cp nginx1:/usr/share/nginx/html/index.html ./index1.html
```
<img src="./img_semana_2/3.png" width="800">

### Paso 4: Editar el archivo index1.html  
```bash
vi index1.html
```
<img src="./img_semana_2/4.png" width="800">

### Paso 5: Copiar el archivo modificado de nuevo al contenedor nginx1  
```bash
docker cp index1.html nginx1:/usr/share/nginx/html/index.html
```
<img src="./img_semana_2/5.png" width="800">

### Paso 6: Copiar el archivo index.html desde nginx2 al host  
```bash
docker cp nginx2:/usr/share/nginx/html/index.html ./index2.html
```
<img src="./img_semana_2/6.png" width="800">

### Paso 7: Editar el archivo index2.html  
```bash
vi index2.html
```
<img src="./img_semana_2/7.png" width="800">

### Paso 8: Copiar el archivo modificado de nuevo al contenedor nginx2  
```bash
docker cp index2.html nginx2:/usr/share/nginx/html/index.html
```
<img src="./img_semana_2/8.png" width="800">

## 9. Resultados esperados
- Al acceder desde el navegador web al puerto 8089, se debería visualizar la página con la información institucional.
<img src="./img_semana_2/9.png" width="800">

- Al acceder al puerto 8090, debe mostrarse la página personalizada del estudiante.
<img src="./img_semana_2/10.png" width="800">

## 10. Bibliografía

- Susnjara, S., & Smalley, I. (2025, febrero 20). ¿Qué es Docker? Ibm.com. https://www.ibm.com/es-es/think/topics/docker

- Atlassian. (s/f). Comparación de contenedores y máquinas virtuales. Atlassian. Recuperado el 13 de abril de 2025, de https://www.atlassian.com/es/microservices/cloud-computing/containers-vs-vms
  
- Home. (2025, febrero 27). Docker Documentation. https://docs.docker.com/

- Stamp, M. (2023, diciembre 18). Top 100 comandos de Linux: una guía esencial para usuarios avanzados​. Guías para Sitios Web, Tips & Conocimiento; DreamHost. https://www.dreamhost.com/blog/es/comandos-linux-que-debes-conocer/
