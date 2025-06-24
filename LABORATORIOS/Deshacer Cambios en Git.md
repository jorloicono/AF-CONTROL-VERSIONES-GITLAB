## Deshacer Cambios en Git

En este laboratorio, exploraremos cómo deshacer diversas acciones en Git utilizando ejemplos prácticos. 
Recuerda, siempre ten cuidado al deshacer, ya que a veces es difícil recuperar algo una vez deshecho. 
Esta es una de las pocas áreas donde Git puede resultar en la pérdida de trabajo si cometes un error.

### Laboratorio 1: Inicialización del Repositorio

Primero, vamos a crear un nuevo directorio para nuestro laboratorio e inicializar un repositorio Git en él.

```bash
# Crea un nuevo directorio para el laboratorio
mkdir git_lab
cd git_lab

# Inicializa un repositorio Git vacío
git init
```

**Resultado Esperado:**

```
Initialized empty Git repository in /ruta/a/tu/directorio/git_lab/.git/
```

Ahora estamos listos para empezar a trabajar con Git.

### Laboratorio 2: Deshacer la Última Confirmación (`git commit --amend`)

[cite\_start]Imagina que confirmas un cambio antes de tiempo y olvidas agregar algún archivo, o te equivocas en el mensaje de confirmación[cite: 4]. [cite\_start]Si quieres rehacer la confirmación, puedes reconfirmar con la opción `--amend`[cite: 5].

**Paso 1: Crear un archivo y hacer una confirmación inicial.**

```bash
echo "Este es el contenido del archivo_1.txt" > archivo_1.txt
git add archivo_1.txt
git commit -m "Confirmación inicial"
```

**Resultado Esperado:**

```
[master (root-commit) <hash_commit>] Confirmación inicial
 1 file changed, 1 insertion(+)
 create mode 100644 archivo_1.txt
```

**Paso 2: Darse cuenta de que olvidaste un archivo y el mensaje no es el correcto.**

Ahora, crea un nuevo archivo que debió haber estado en la confirmación inicial y "corrige" el mensaje de confirmación.

```bash
echo "Este es el contenido del archivo_olvidado.txt" > archivo_olvidado.txt
git add archivo_olvidado.txt
git commit --amend
```

[cite\_start]Al ejecutar `git commit --amend`, se abrirá tu editor de texto predeterminado con el mensaje de confirmación anterior ("Confirmación inicial") ya cargado[cite: 7]. Edítalo para que diga "Confirmación inicial con todos los archivos" y guarda y cierra el editor.

**Resultado Esperado (después de editar el mensaje y cerrar el editor):**

```
[master <hash_commit_nuevo>] Confirmación inicial con todos los archivos
 Date: <fecha_hora>
 2 files changed, 2 insertions(+)
 create mode 100644 archivo_1.txt
 create mode 100644 archivo_olvidado.txt
```

**Verificación:**

```bash
git log --oneline
```

Verás que solo hay una confirmación en el historial, y su mensaje es "Confirmación inicial con todos los archivos". [cite\_start]La segunda confirmación reemplaza el resultado de la primera[cite: 9].

### Laboratorio 3: Deshacer un Archivo Preparado (`git reset HEAD <file>...`)

[cite\_start]Las siguientes dos secciones demuestran cómo lidiar con los cambios de tu área de preparación y tu directorio de trabajo[cite: 10]. [cite\_start]Afortunadamente, el comando que usas para determinar el estado de esas dos áreas también te recuerda cómo deshacer los cambios en ellas[cite: 11].

**Paso 1: Modificar dos archivos y prepararlos accidentalmente.**

```bash
echo "Nueva línea para archivo_1.txt" >> archivo_1.txt
echo "Nueva línea para archivo_2.txt" > archivo_2.txt
git add . # [cite_start]¡Ups, preparamos ambos! [cite: 12]
```

**Paso 2: Verificar el estado y ver cómo despreparar.**

```bash
git status
```

**Resultado Esperado:**

```
On branch master
Changes to be committed:
  [cite_start](use "git reset HEAD <file>..." to unstage) [cite: 15]
        modified:   archivo_1.txt
        new file:   archivo_2.txt
```

[cite\_start]Justo debajo del texto "Changes to be committed", verás que dice que uses `git reset HEAD <file>...` para deshacer la preparación[cite: 15, 16].

**Paso 3: Despreparar un archivo.**

Vamos a despreparar `archivo_2.txt`.

```bash
git reset HEAD archivo_2.txt
```

**Resultado Esperado:**

```
Unstaged changes after reset:
M       archivo_2.txt
```

**Verificación:**

```bash
git status
```

**Resultado Esperado:**

```
On branch master
Changes to be committed:
        modified:   archivo_1.txt

Changes not staged for commit:
  (use "git add <file>..." to update what will be committed)
  (use "git checkout -- <file>..." to discard changes in working directory)
        modified:   archivo_2.txt
```

[cite\_start]Ahora `archivo_2.txt` está modificado y, nuevamente, no preparado[cite: 17]. El `archivo_1.txt` sigue preparado.

### Laboratorio 4: Deshacer un Archivo Modificado (`git checkout -- <file>...`)

[cite\_start]¿Qué tal si te das cuenta de que no quieres mantener los cambios de un archivo? [cite: 19] [cite\_start]¿Cómo puedes restaurarlo fácilmente al estado en el que estaba en la última confirmación? [cite: 20]

**Paso 1: Modificar un archivo y no prepararlo.**

Si continuamos desde el laboratorio anterior, `archivo_2.txt` está modificado pero no preparado. Si no, puedes modificarlo manualmente:

```bash
echo "Más cambios en archivo_2.txt que quiero descartar" >> archivo_2.txt
git status
```

**Resultado Esperado (parte relevante):**

```
Changes not staged for commit:
  (use "git add <file>..." to update what will be committed)
 (use "git checkout -- <file>..." to discard changes in working directory) 
        modified:   archivo_2.txt
```

Allí se te indica explícitamente cómo descartar los cambios que has hecho.

**Paso 2: Descartar los cambios en el archivo.**

```bash
git checkout -- archivo_2.txt
```

**Verificación:**

```bash
git status
```

**Resultado Esperado:**

```
On branch master
Changes to be committed:
        modified:   archivo_1.txt
```

Ahora puedes ver que los cambios en `archivo_2.txt` se han revertido. Si abres `archivo_2.txt`, notarás que la última línea que agregaste ha desaparecido.

**Concepto Clave:** Recuerda, todo lo que esté confirmado en Git puede recuperarseIncluso confirmaciones que estuvieron en ramas eliminadas o confirmaciones que fueron sobrescritas con `amend` pueden recuperarse
Sin embargo, es posible que no vuelvas a ver jamás cualquier cosa que pierdas y que nunca haya sido confirmada
