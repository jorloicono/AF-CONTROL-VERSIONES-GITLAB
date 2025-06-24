Este ejercicio está diseñado para practicar el flujo GitFlow en un proyecto realista. Incluye la creación de nuevas funcionalidades, manejo de versiones, solución de errores y resolución de conflictos. No se proporcionan comandos; dedúcelos por tu cuenta.

---

## 1. Inicialización del proyecto

- Crea un nuevo repositorio.
- Inicializa GitFlow en el repositorio. Acepta los nombres por defecto (`main`, `develop`, etc.).
- Asegúrate de tener al menos un archivo de inicio en el repositorio (por ejemplo, `README.md`) y realiza una primera confirmación.

---

## 2. Desarrollo de una funcionalidad

- Comienza una nueva funcionalidad llamada `login`.
- Crea un archivo llamado `login.html` y escribe una estructura básica de formulario (usuario y contraseña).
- Realiza al menos **dos confirmaciones**: una para la estructura base y otra para los estilos o validaciones.
- Finaliza la funcionalidad y asegúrate de que se integre correctamente en la rama de desarrollo.

---

## 3. Agregar una segunda funcionalidad

- Inicia otra funcionalidad llamada `registro`.
- Crea un archivo `registro.html` con un formulario de registro de usuario.
- Antes de terminar esta funcionalidad, cambia a la rama de desarrollo y modifica el archivo `login.html` (por ejemplo, cambia un texto del botón).
- Luego vuelve a la funcionalidad `registro` y modifica **el mismo fragmento** del archivo `login.html`.
- Finaliza la funcionalidad.

> **Nota:** Esto debe generar un **conflicto** al finalizar la funcionalidad. Resuélvelo manualmente, elige el contenido correcto y realiza la confirmación para completar la integración.

---

## 4. Preparar una versión de lanzamiento

- Inicia una rama de `release` con la versión `1.0.0`.
- En la rama de `release`, realiza tareas como:
  - Actualizar el archivo `README.md` con información del proyecto.
  - Crear un archivo `CHANGELOG.md` con la lista de cambios.
- Finaliza la `release`. Esto debe integrar los cambios en `main` y crear una etiqueta de versión.

---

## 5. Detectar y corregir un error en producción

- Imagina que se detectó un error crítico en el formulario de login ya publicado.
- Inicia una rama de `hotfix` para corregir el error.
- Realiza la corrección directamente en la rama correspondiente.
- Finaliza el hotfix.
  - Asegúrate de que los cambios se integren tanto en `main` como en `develop`.

---

## 6. Validar la historia del proyecto

- Visualiza el historial de ramas y confirmaciones del proyecto.
- Comprueba cómo los cambios de cada rama (feature, release, hotfix) se integraron correctamente en `develop` y `main`.

---

## 7. Buenas prácticas y limpieza

- Elimina las ramas locales que ya han sido fusionadas.
- Asegúrate de que `develop` y `main` estén sincronizadas con los últimos cambios.

---

Este ejercicio te ayudará a entender cómo se gestiona un proyecto completo con **GitFlow**, desde el desarrollo de nuevas funcionalidades hasta la entrega y mantenimiento post-lanzamiento. Practica la resolución de conflictos y mantén una historia limpia y coherente.
