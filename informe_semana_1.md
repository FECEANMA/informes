#  Estructura de un proyecto angular con comandos linux

## 1. Título  
**Creación de la estructura base de un proyecto Angular usando comandos nativos de Linux**

---

## 2. Tiempo de duración  
**40 minutos**

---

## 3. Fundamentos

Angular es un framework frontend desarrollado por Google que permite la construcción de aplicaciones web de una sola página (SPA - Single Page Applications) de manera estructurada y mantenible. Esta práctica se enfoca en la creación manual de la estructura de directorios que normalmente genera Angular CLI, pero utilizando únicamente comandos de terminal en Linux. Esta aproximación permite comprender mejor la organización interna de un proyecto Angular y adquirir habilidades básicas en manejo de sistema de archivos y scripting en bash.

En el desarrollo frontend moderno, Angular estructura el código de manera modular, separando la lógica de componentes, vistas HTML, hojas de estilo CSS y archivos de configuración. La carpeta `src` contiene todo el código fuente y es donde reside el corazón de la aplicación. Dentro de esta, se organiza una carpeta `app/` que agrupa los componentes principales como `app.component.ts`, `app.module.ts`, etc. Además, se tiene una carpeta `assets/` para recursos como imágenes, fuentes y estilos globales.

A través del uso de comandos como `mkdir`, `touch` y `cd`, es posible replicar esta estructura sin depender de herramientas automatizadas, lo cual es útil en ambientes restringidos o para propósitos educativos.

> **Figura 3-1. Estructura de carpetas esperada del proyecto Angular**  
> ![Estructura de carpetas](https://i.imgur.com/VRm4JVu.png)

Este tipo de ejercicios también introduce conceptos clave sobre sistemas de archivos en Linux, uso de terminal, permisos de archivos y scripts de inicialización de proyectos, fundamentales para entornos DevOps, CI/CD y despliegue en servidores web como Nginx.

---

## 4. Conocimientos previos

Para realizar esta práctica, el estudiante necesita tener claros los siguientes conceptos:

- Uso básico de terminal en Linux (comandos como `mkdir`, `touch`, `cd`)
- Estructura de un proyecto frontend moderno
- Manejo básico de archivos y carpetas
- Conocimientos mínimos de HTML, TypeScript y CSS
- Comprensión del funcionamiento general de Angular

---

## 5. Objetivos a alcanzar

- Implementar manualmente la estructura de carpetas de un proyecto Angular
- Manipular archivos de configuración del proyecto (`angular.json`, `tsconfig.json`, etc.)
- Comprender el rol de cada archivo principal dentro de un proyecto Angular
- Fortalecer el uso de comandos básicos de Linux para automatización de tareas

---

## 6. Equipo necesario

- Computadora con sistema operativo Linux/Mac/Windows (WSL en caso de Windows)
- Terminal de comandos (Bash)
- Editor de texto (VSCode, Nano, Vim, etc.)
- Opcional: Cuenta en [Docker Play](https://labs.play-with-docker.com/)
- Versión recomendada de Docker (si se desea extender con contenedores): `v24.0.2`

---

## 7. Material de apoyo

- [Documentación oficial de Angular](https://angular.io/docs)
- [Cheat Sheet de comandos Linux](https://files.fosswire.com/2007/08/fwunixref.pdf)
- Guía de asignatura
- Documentación de `mkdir`, `touch` y `tree` (`man mkdir`)

---

## 8. Procedimiento

### Paso 1: Crear directorios base del proyecto
```bash
mkdir -p my-angular-project/{dist,public,src/{app/components,assets/{images,fonts,styles}}}
```


### Paso 2: Ingresar al directorio principal
```bash
cd my-angular-project
```

### Paso 3: Crear los archivos raíz del proyecto
```bash
touch README.md angular.json package.json tsconfig.json
```

### Paso 4: Crear archivos base en la carpeta src/
```bash
touch src/{index.html,main.ts,styles.css,favicon.ico}
```

### Paso 5: Crear archivos dentro de src/app/
```bash
touch src/app/{app.component.ts,app.component.html,app.component.css,app.module.ts}
```

## 9. Resultados esperados
Al finalizar la práctica, se espera contar con una estructura de carpetas completamente funcional que simule un proyecto Angular listo para desarrollarse, incluso sin haber usado Angular CLI. Esta estructura podrá ser usada posteriormente para compilar manualmente el proyecto, configurar servidores como Nginx, o implementar automatizaciones con Docker o CI/CD.

## 10. Bibliografía
- Angular. (2024). Angular Documentation. Retrieved from https://angular.io/docs

- GNU. (n.d.). GNU Core Utilities Manual. Retrieved from https://www.gnu.org/software/coreutils/manual/coreutils.html

- Gaddis, T. (2020). Starting Out with Programming Logic and Design. Pearson.

- Shotts, W. E. (2019). The Linux Command Line: A Complete Introduction. No Starch Press.
