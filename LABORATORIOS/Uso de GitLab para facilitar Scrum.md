# Uso de GitLab para facilitar Scrum

---

## Introducción

Según el Agile Fluency Model de Martin Fowler, los equipos que practican Scrum:

> "...piensan y planifican en términos de los beneficios que sus patrocinadores, clientes y usuarios verán en su software."

Lo logran demostrando su progreso mensualmente y reflexionando regularmente para mejorar sus procesos y hábitos de trabajo, con el fin de entregar mayor valor al negocio y a los clientes.

---

## Temas que cubre este tutorial

- Configuración de grupos y proyectos  
- Gestión del backlog de funcionalidades  
- Gestión del backlog de historias  
- Seguimiento del progreso del sprint  

---

## Configuración de grupos y proyectos

Para facilitar las prácticas Scrum en GitLab, primero hay que configurar la estructura base de grupos y proyectos.

- **Grupos:** Se usan para crear tableros y etiquetas que pueden heredarse por los proyectos dentro de ese grupo.
- **Proyectos:** Contienen los issues y tareas que conforman el trabajo real de cada sprint.

### Modelo de herencia en GitLab

GitLab tiene una estructura jerárquica donde los grupos contienen proyectos. Las configuraciones hechas a nivel grupo se aplican también a los proyectos hijos, lo que permite estandarizar etiquetas, tableros e iteraciones.

**Ejemplo de objetos y su relación:**

| Grupo       | Proyecto | Épicas | Etiquetas | Tableros | Iteraciones | Hitos | Roadmaps | Issues | Plantillas | Tareas | Listas |
|-------------|----------|--------|-----------|----------|-------------|-------|----------|--------|------------|--------|--------|
| Contiene    | Contiene | Contiene | Contiene  | Contiene | Contiene    | Contiene | Contiene | Contiene | Contiene  | Contiene | Contiene |

Los miembros del grupo heredan permisos en los proyectos anidados. Se recomienda crear tableros y etiquetas a nivel grupo para estandarizar la planificación y los reportes.

---

### Crear un grupo

1. En la barra lateral izquierda, selecciona **Crear nuevo** (  ) y luego **Nuevo grupo**.  
2. Haz clic en **Crear grupo**.  
3. Ingresa el nombre del grupo y la URL para el namespace.  
4. Selecciona el nivel de visibilidad del grupo.  
5. Opcionalmente, personaliza tu experiencia seleccionando el rol y uso del grupo.  
6. Invita miembros si quieres.  
7. Presiona **Crear grupo**.

Este grupo será el contenedor principal para tableros, épicas, historias y etiquetas.

---

### Crear proyectos

Dentro del grupo creado, crea uno o varios proyectos que contendrán las historias.

Pasos para crear un proyecto en blanco:

1. En la barra lateral izquierda, selecciona **Crear nuevo** (  ) y luego **Nuevo proyecto/repositorio**.  
2. Selecciona **Crear proyecto en blanco**.  
3. Completa los detalles: nombre del proyecto, slug (ruta URL), nivel de visibilidad, y si quieres, inicializa con un README.  
4. Haz clic en **Crear proyecto**.

---

### Crear etiquetas con alcance para las fases Scrum

Las etiquetas con alcance (*scoped labels*) permiten evitar que dos etiquetas del mismo tipo se usen simultáneamente.

Por ejemplo, si un issue tiene la etiqueta `status::in progress` y se le agrega `status::ready`, la primera se elimina automáticamente.

Para crear etiquetas:

1. Busca tu grupo en la barra lateral y ve a **Administrar > Etiquetas**.  
2. Haz clic en **Nueva etiqueta**.  
3. Define el nombre (por ejemplo, `priority::now`).  
4. Asigna color si deseas.  
5. Presiona **Crear etiqueta**.

**Etiquetas recomendadas:**

- Prioridad (para planificación a nivel épico):  
  `priority::now`, `priority::next`, `priority::later`

- Estado (para seguimiento de historias):  
  `status::triage`, `status::refine`, `status::ready`, `status::in progress`, `status::in review`, `status::acceptance`, `status::done`

- Tipo (para clasificar trabajo en la iteración):  
  `type::story`, `type::bug`, `type::maintenance`

---

### Crear una cadencia de iteraciones (sprints)

En GitLab, los sprints se llaman **iteraciones**.

Para crear una cadencia:

1. Busca tu grupo y ve a **Plan > Iteraciones**.  
2. Haz clic en **Nueva cadencia de iteraciones**.  
3. Ingresa título y descripción.  
4. Activa **Programación automática**.  
5. Configura fecha de inicio, duración (2 semanas recomendadas), y número de iteraciones futuras (4).  
6. Activa **Permitir continuación automática** para mover issues incompletos.  
7. Haz clic en **Crear cadencia**.

---

## Gestión del backlog de funcionalidades (épicas)

### Estructura recomendada

- **Funcionalidad (Épica):** característica que el equipo entregará en una iteración.  
- **Historia (Issue):** representa una tarea o historia de usuario que aporta valor tangible.  
- **Tarea:** pasos de implementación para completar una historia.

### Ejemplo de descomposición vertical de una funcionalidad

**Épica:** Cuando uso la aplicación, necesito crear una cuenta para poder usar sus funcionalidades.  
**Historias:**  
- Especificar correo electrónico para recibir actualizaciones.  
- Especificar contraseña para seguridad.  
- Finalizar creación de cuenta para iniciar sesión.

### Crear un tablero de planificación de lanzamientos (épico)

1. Busca tu grupo, ve a **Plan > Tableros épicos**.  
2. En la esquina superior izquierda, selecciona **Crear nuevo tablero**.  
3. Nombra el tablero: *Release Planning*.  
4. Crea listas usando las etiquetas `priority::later`, `priority::next`, y `priority::now`.  
5. Utiliza estas listas para mover épicas según su prioridad y estado.

---

## Gestión del backlog de historias

### Crear historias dentro de una épica

1. Abre un tablero épico y selecciona la épica.  
2. En la sección **Issues e épicas hijas**, selecciona **Agregar > Agregar nuevo issue**.  
3. Ingresa el título y asigna el proyecto.  
4. Crea los issues para cada historia de usuario.

### Refinar backlog de historias con un tablero de issues

1. Crea un tablero de issues nuevo llamado **Backlog** en tu grupo.  
2. Crea listas para cada iteración futura.  
3. Marca los issues para refinamiento con la etiqueta `status::refine`.  
4. Organiza las historias en las iteraciones según prioridad y estimación.

---

## Ceremonia de planificación del sprint

### Planificación síncrona

- Usa el tablero Backlog con el equipo.  
- Revisa criterios de aceptación, divide historias en tareas, estima esfuerzo (campo Weight).  
- Marca las historias listas con `status::ready`.

### Planificación asíncrona

- Crea un issue para planificación en el tablero Backlog.  
- Crea hilos de discusión para cada historia.  
- Los miembros discuten, votan estimaciones con emojis, ajustan criterios.  
- Actualiza historias y marca como listas.  
- Resuelve las discusiones al terminar.

---

## Seguimiento del progreso del sprint

### Crear tablero para sprint actual

1. Crea un tablero llamado **Current Sprint** filtrado por la iteración actual.  
2. Crea listas con las etiquetas de estado para reflejar el progreso:  
   `status::refine`, `status::ready`, `status::in progress`, `status::review`, `status::acceptance`, `status::done`.  
3. Mueve issues entre listas para reflejar su estado.

### Consultar gráficos burndown y burnup

- En el menú de Iteraciones, selecciona una cadencia y una iteración para ver reportes y métricas.

---

Con esta guía, puedes aprovechar GitLab para facilitar la implementación de Scrum, aumentando la transparencia, la colaboración y la entrega continua en tus proyectos ágiles.
