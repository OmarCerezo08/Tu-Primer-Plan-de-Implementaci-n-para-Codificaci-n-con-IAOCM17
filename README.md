# Plan de Implementación: Script de Utilidad - Organizador Masivo de Archivos con IA

Este documento sirve como el plano maestro y guía de prompting estratégico para que un asistente de codificación de Inteligencia Artificial (IA) desarrolle el Producto Mínimo Viable (MVP) sin desviaciones técnicas.

---

## 1. Idea de Proyecto y Objetivo

### Descripción del Proyecto
El proyecto consiste en un **Script de Utilidad CLI (Command Line Interface)** diseñado para automatizar la limpieza, estandarización y renombrado masivo de archivos locales dentro de un directorio específico. El software analiza de manera inteligente patrones de texto confusos u organizados de forma caótica en los nombres de archivos y los unifica de forma inmediata.

### Problema que Resuelve
Evita la pérdida de tiempo manual y los errores humanos al renombrar cientos de recursos (como imágenes, reportes o documentos) que se descargan con nombres genéricos, caracteres especiales corruptos o espacios inválidos.

### Objetivo Principal
Proveer una herramienta automatizada ultraligera que reduzca el tiempo de organización de archivos de horas a segundos, aplicando reglas estrictas de nomenclatura segura para sistemas operativos y entornos de desarrollo.

---

## 2. Audiencia Objetivo

### Perfil del Usuario
Este script está diseñado para:
*   **Desarrolladores y Administradores de Sistemas (SysAdmins)**: Que necesitan normalizar directorios de assets, respaldos o repositorios de código de forma ágil mediante terminal.
*   **Creadores de Contenido / Analistas de Datos**: Que reciben crudos de información con formatos heterogéneos y requieren limpieza previa antes del procesamiento o ingesta de datos.

---

## 3. Selección del Stack Tecnológico

Para garantizar que el script sea rápido, altamente portátil y fácil de ejecutar por la IA, se han seleccionado las siguientes tecnologías:

*   **Entorno de Ejecución**: Node.js (Versión LTS 18 o superior).
*   **Lenguaje**: JavaScript (ES6+ moderno para modularidad nativa).
*   **Módulos Nativos (Sin dependencias externas)**:
    *   `fs/promises`: Para la manipulación asíncrona no bloqueante del sistema de archivos (File System).
    *   `path`: Para garantizar la resolución de rutas relativas y absolutas multiplataforma (Windows, macOS, Linux).
*   **Formato de Configuración**: JSON básico (`package.json`) solo para definir el tipo de módulo (`"type": "module"`).

---

## 4. Funcionalidades Principales (Alcance del MVP - Primera Iteración)

El asistente de IA debe limitarse estrictamente a implementar los siguientes submódulos funcionales:

*   **[MVP-01] Validación de Argumentos y Rutas**: El script debe capturar el directorio de origen mediante la línea de comandos, verificar que el argumento exista y confirmar que sea una carpeta válida en el disco.
*   **[MVP-02] Lectura Asíncrona de Archivos**: Listar exclusivamente los archivos del directorio de forma no bloqueante, filtrando de manera automática directorios internos y archivos ocultos del sistema (como `.DS_Store` o `.git`).
*   **[MVP-03] Motor de Limpieza (RegEx)**: Aplicar una función de filtrado con expresiones regulares que realice de manera secuencial:
    1.  Transformar todo el texto a minúsculas (`lowercase`).
    2.  Eliminar acentos y diéresis.
    3.  Reemplazar espacios y caracteres especiales por guiones medios (`-`).
    4.  Eliminar guiones repetidos consecutivos (`--` -> `-`).
*   **[MVP-04] Operación Segura de Renombrado**: Modificar físicamente los nombres en el almacenamiento utilizando `fs.rename`. Debe incluir una validación que añada un sufijo incremental (Ej: `-1`, `-2`) si el archivo final ya existe, evitando la sobreescritura accidental de datos.

---

## 5. Especificación del Enfoque de Front-End (Diseño de la UI/CLI)

Al ser un script de utilidad pura, la interfaz visual se traslada de forma íntegra a la consola del sistema (CLI):

*   **Interfaz de Entrada (Input)**: Los parámetros se envían como un argumento directo al ejecutar el comando en la terminal.
    *   *Sintaxis estándar*: `node script.js <ruta_del_directorio>`
*   **Flujo de Salida Visual (Output)**: La terminal debe imprimir logs interactivos limpios estructurados de la siguiente forma:
    *   `[INICIO]` Procesando directorio: `/workspaces/mi-carpeta`
    *   `[OK]` Renombrado exitoso: `Foto Proyecto 01!.JPG` -> `foto-proyecto-01.jpg`
    *   `[ERROR]` Archivo omitido por bloqueo: `reporte_bloqueado.pdf`
    *   `[RESUMEN]` Proceso finalizado. Archivos totales: X | Procesados con éxito: Y | Errores: Z.

---

## 6. Estrategia de Despliegue y Protocolo de Interacción con IA

### Estrategia de Despliegue Local
El script se diseñará para ejecutarse en entornos locales aislados de desarrollo:
1. Clonar el repositorio que aloja el archivo markdown y el script ejecutable.
2. Asegurar la presencia de Node.js en la máquina corriendo `node -v`.
3. Ejecución inmediata sin necesidad de correr un costoso o pesado comando `npm install` global.

### Protocolo de Interacción y Prompting con la IA
Para evitar que la IA genere código roto, incompleto o sobreestructurado, se seguirán estas reglas:
*   **Principio de Responsabilidad Única**: Se le solicitará a la IA programar una sola función a la vez (ej. primero el motor RegEx, probarlo, y después la lectura de archivos).
*   **Formato de Depuración**: Si el script falla, se le entregará a la IA el log de error exacto de Node.js junto con la línea exacta del código que falló.
*   **Validación Estricta**: Se prohibirá el uso de librerías externas (como `lodash` o `shelljs`) para asegurar que el MVP sea nativo y rápido de transferir.

---

## 7. Plan de Trabajo Paso a Paso para la IA (Flujo de Construcción)

Este es el orden secuencial cronológico en el que se le darán las instrucciones a la Inteligencia Artificial para el desarrollo:

*   **Fase 1: Andamiaje**: Crear el archivo `index.js`, inicializar el archivo `package.json` elemental con soporte para módulos ES y validar la captura de argumentos por consola (`process.argv`).
*   **Fase 2: Lectura de Disco**: Escribir la lógica asíncrona para abrir la carpeta seleccionada y mapear los nombres originales a un arreglo de cadenas de texto.
*   **Fase 3: Procesamiento de Cadenas**: Implementar la lógica puramente matemática y de expresiones regulares de limpieza de strings, añadiendo pruebas de consola simuladas.
*   **Fase 4: Modificación Física**: Acoplar la lógica de renombrado en disco, implementar bloques `try/catch` robustos para interceptar errores de permisos y añadir el validador de nombres duplicados.
*   **Fase 5: Cierre del Sistema**: Formatear estéticamente los textos de salida por pantalla y dar por concluido el MVP del plan de implementación.
