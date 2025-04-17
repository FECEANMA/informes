#  Estructura de un proyecto angular con comandos linux

## 1. Título  
**Creación de la estructura base de un proyecto Angular usando comandos nativos de Linux**

---

## 2. Tiempo de duración  
**20 minutos**

---

## 3. Fundamentos

El sistema operativo Linux es ampliamente utilizado en entornos de desarrollo, servidores y procesos de automatización debido a su estabilidad, seguridad y la potencia de su terminal de comandos. Una de sus grandes ventajas es la posibilidad de gestionar archivos y estructuras de carpetas mediante comandos nativos, sin depender de interfaces gráficas. 

A través del uso de comandos como `mkdir`, `touch` y `cd`, es posible replicar esta estructura sin depender de herramientas automatizadas, lo cual es útil en ambientes restringidos o para propósitos educativos.

---

## 4. Conocimientos previos

Para realizar esta práctica, se debe tener claro los siguientes conceptos:

- Uso básico de terminal en Linux (comandos como `mkdir`, `touch`, `cd`)
- Estructura de un proyecto Angulaar
- Manejo básico de archivos y carpetas

---

## 5. Objetivos a alcanzar

- Implementar manualmente la estructura de carpetas de un proyecto Angular mediante comandos basicos de Linux.
- Fortalecer el uso de comandos básicos de Linux para automatización de tareas como la creacion de carpetas y archivos.

---

## 6. Equipo necesario

- Computadora con sistema operativo Linux
- Terminal de comandos (Bash)
---

## 7. Material de apoyo

- Guía de asignatura
- Documentación de comandos basicos de Linux `mkdir`, `touch` y `tree` (`man mkdir`)
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
Al finalizar la práctica, se espera contar con una estructura de carpetas completamente funcional que simule un proyecto Angular, incluso sin haber usado Angular CLI. Ademas de haber fortalecido el dominio de comandos básicos de Linux como mkdir, touch y cd.

## 10. Bibliografía
- Comando mkdir de Linux: para crear nuevos directorios. (s/f). IONOS Digital Guide. Recuperado el 17 de abril de 2025, de https://www.ionos.com/es-us/digitalguide/servidores/configuracion/comando-mkdir-de-linux/
- Bigelow, S. J. (2021, abril 9). Sistema operativo Linux. ComputerWeekly.es; TechTarget. https://www.computerweekly.com/es/definicion/Sistema-operativo-Linux
- Terminal de Linux - Linux en español. (s/f). Terminaldelinux.com. Recuperado el 17 de abril de 2025, de https://terminaldelinux.com/terminal/
