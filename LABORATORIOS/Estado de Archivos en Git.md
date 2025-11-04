# Estado de Archivos en Git

## 1. Inicialización del Proyecto

Primero, debemos crear un directorio para nuestro proyecto e inicializarlo como un repositorio de Git.

```bash
$ mkdir mi_proyecto
$ cd mi_proyecto
$ git init
```

Esto crea un nuevo repositorio local de Git vacío.

---

## 2. Agregar un Archivo Nuevo

Creamos un archivo `README`:

```bash
$ echo 'Mi Proyecto' > README
```

Al ejecutar:

```bash
$ git status
```

Verás algo como:

```
Untracked files:
  (use "git add <file>..." to include in what will be committed)
    README
```

### ¿Qué significa "untracked"?

Significa que Git **detecta** el archivo, pero **no lo está rastreando** aún. No se incluirá en ningún commit a menos que lo agregues explícitamente.

---

## 3. Rastrear el Archivo

Para comenzar a rastrear el archivo:

```bash
$ git add README
```

Ahora, al usar `git status`:

```
Changes to be committed:
  new file:   README
```

El archivo está preparado para ser confirmado (commit).

---

## 4. Modificar Archivos Existentes

Supón que modificas un archivo ya rastreado, como `CONTRIBUTING.md`.

```bash
$ vim CONTRIBUTING.md
```

Al ejecutar `git status`:

```
Changes not staged for commit:
  modified:   CONTRIBUTING.md
```

Esto indica que el archivo fue **modificado pero no preparado** aún.

### Preparar el Archivo Modificado

```bash
$ git add CONTRIBUTING.md
```

Ahora, el archivo se mueve a la sección de "Changes to be committed".

---

## 5. ¿Qué pasa si vuelves a modificar antes de confirmar?

Si modificas `CONTRIBUTING.md` otra vez **después** de `git add`, tendrás dos versiones:

* La **preparada** (stage).
* La **modificada en disco** (working directory).

```bash
$ vim CONTRIBUTING.md
$ git status
```

Resultado:

```
Changes to be committed:
  modified:   CONTRIBUTING.md

Changes not staged for commit:
  modified:   CONTRIBUTING.md
```

➡Solución: vuelve a ejecutar `git add` para actualizar la versión preparada.

---

## 6. Ver Cambios con `git diff`

* Para ver cambios **no preparados**:

```bash
$ git diff
```

* Para ver cambios **preparados para commit**:

```bash
$ git diff --staged
```

También puedes usar:

```bash
$ git diff --cached
```

(`--cached` es sinónimo de `--staged`)

---

## 7. Confirmar los Cambios

Cuando todo esté listo en el área de preparación:

```bash
$ git commit
```

Esto abrirá el editor para escribir un mensaje de commit.

### Alternativa con mensaje en línea:

```bash
$ git commit -m "Agregar README y actualizar CONTRIBUTING.md"
```

Salida esperada:

```
[master 463dc4f] Agregar README y actualizar CONTRIBUTING.md
 2 files changed, 2 insertions(+)
 create mode 100644 README
```

---


## Recursos

* [Git Book en Español](https://git-scm.com/book/es/v2)
* Comandos útiles:

  * `git status` → Ver estado actual.
  * `git add <archivo>` → Preparar archivo.
  * `git commit -m "mensaje"` → Confirmar cambios.
  * `git diff` / `git diff --staged` → Ver diferencias.

---
