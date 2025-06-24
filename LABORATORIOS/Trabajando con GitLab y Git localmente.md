# Trabajando con GitLab y Git localmente

---

## 1. Crear proyecto y repositorio local

```bash
# Ir a tu carpeta de trabajo
cd ~/proyectos

# Crear carpeta para el proyecto
mkdir demo-gitlab
cd demo-gitlab

# Inicializar git
git init
````

Creamos un archivo de ejemplo:

```bash
echo "<!DOCTYPE html>
<html>
<head><title>Demo GitLab</title></head>
<body><h1>Hola GitLab</h1></body>
</html>" > index.html
```

Agregamos y hacemos commit:

```bash
git add index.html
git commit -m "Agrega archivo index.html inicial"
```

---

## 2. Crear repositorio remoto en GitLab

* Entra a [https://gitlab.com](https://gitlab.com) y crea un nuevo proyecto llamado `demo-gitlab`.
* No inicialices con README ni .gitignore.
* Copia la URL SSH, por ejemplo:
  `git@gitlab.com:usuario/demo-gitlab.git`

---

## 3. Vincular repositorio local con remoto y subir el proyecto

```bash
git remote add origin git@gitlab.com:usuario/demo-gitlab.git

git push -u origin master
```

> `-u` configura la rama local `master` para que rastree la rama remota `origin/master`.

---

## 4. Modificar el proyecto directamente en GitLab

* Ve a tu repo en GitLab.
* Abre `index.html` con el editor web.
* Cambia el texto del `<h1>` a:
  `Hola GitLab - cambio remoto`
* Haz commit desde la interfaz (directo a `master`).

---

## 5. Traer cambios desde remoto a local

### 5.1 Usando `git pull` (trae y fusiona automáticamente)

```bash
git pull origin master
```

Este comando hace dos cosas:

* Trae los cambios del remoto (`git fetch`).
* Fusiona esos cambios con tu rama local activa (`git merge`).

---

### 5.2 Usando `git fetch` y `git merge` por separado

Vamos a simular que alguien hizo un cambio en GitLab (puedes hacerlo desde la web de GitLab, modificando `index.html`, por ejemplo cambiando el título a `Hola GitLab - cambio remoto FETCH` y haciendo commit).

Ahora en local:

```bash
git fetch origin
```

**¿Qué pasó?**

* `git fetch` descargó las actualizaciones del remoto y las guardó en la rama remota `origin/master`, pero **NO las fusionó** con tu rama local `master`.
* Puedes revisar qué cambios hay con:

  ```bash
  git diff master origin/master
  ```

Si estás de acuerdo con esos cambios, haz:

```bash
git merge origin/master
```

Esto fusionará manualmente los cambios remotos en tu rama local.

---

### Diferencia práctica

* `git pull` es un atajo para hacer `fetch` + `merge` automático.
* `git fetch` solo actualiza tus referencias remotas, dejándote decidir cuándo y cómo fusionar.
* `fetch` es útil si quieres revisar los cambios remotos primero antes de mezclarlos en tu trabajo local.

---

## 6. Trabajar con ramas

### Crear y cambiar a una rama nueva

```bash
git checkout -b feature-actualizar-titulo
```

### Modificar el archivo localmente

Edita `index.html` (con un editor de texto o desde terminal):

```bash
sed -i 's/Hola GitLab/Hola GitLab desde rama feature/' index.html
```

### Guardar cambios

```bash
git add index.html
git commit -m "Actualiza título en rama feature"
```

### Subir la rama a remoto

```bash
git push -u origin feature-actualizar-titulo
```

---

## 7. Revisar ramas remotas y locales

```bash
git branch       # ramas locales
git branch -r    # ramas remotas
git branch -a    # todas
```

---

## 8. Fusionar cambios de la rama feature a master (local)

```bash
git checkout master
git pull origin master  # Asegurar que master esté actualizado

git merge feature-actualizar-titulo
```

Si hay conflictos, resuélvelos editando los archivos afectados y luego:

```bash
git add <archivos_resueltos>
git commit
```

Luego sube los cambios fusionados:

```bash
git push origin master
```

---

## 9. Eliminar la rama feature (local y remoto)

```bash
git branch -d feature-actualizar-titulo
git push origin --delete feature-actualizar-titulo
```

---

## 10. Explicación rápida de comandos clave

| Comando                 | Qué hace                                    |
| ----------------------- | ------------------------------------------- |
| `git init`              | Crea repositorio git local                  |
| `git add <archivos>`    | Marca archivos para commit                  |
| `git commit -m "msg"`   | Guarda cambios locales en la historia       |
| `git remote add origin` | Vincula repositorio local con remoto        |
| `git push`              | Envía cambios locales al remoto             |
| `git pull`              | Trae y fusiona cambios del remoto           |
| `git fetch`             | Trae cambios del remoto pero no los fusiona |
| `git checkout -b rama`  | Crea y cambia a una rama nueva              |
| `git merge rama`        | Fusiona una rama a la rama actual           |

---



