# Creando un repositorio Git

## Crear un repositorio local con `git init`

Para usar el comando `git init` y crear un repositorio local en tu computadora, sigue los siguientes pasos:

1. Abre la terminal en tu computadora y navega hasta el directorio donde deseas crear el repositorio. Puedes usar el comando `cd` para cambiar de directorio.
2. Una vez en el directorio adecuado, ejecuta el comando:

   ```bash
   git init
````

Esto creará un nuevo repositorio Git en el directorio actual.

3. Después de ejecutar el comando, deberías ver un mensaje que indica que se ha creado un repositorio Git vacío. Ahora puedes comenzar a agregar archivos a este repositorio.

4. Para agregar archivos al repositorio, usa el comando `git add`. Por ejemplo, si deseas agregar un archivo llamado `archivo.txt`, ejecuta:

   ```bash
   git add archivo.txt
   ```

5. Luego de agregar los archivos, usa el comando `git commit` para confirmar los cambios. Por ejemplo:

   ```bash
   git commit -m "Mensaje de confirmación"
   ```

Con estos pasos, deberías tener un repositorio Git inicializado y listo para usar.

---

## Clonar un repositorio existente con `git clone`

Si deseas obtener una copia de un repositorio Git existente —por ejemplo, un proyecto en el que te gustaría contribuir— el comando que necesitas es:

```bash
git clone [url]
```

Si estás familiarizado con otros sistemas de control de versiones como Subversion, notarás que en Git el comando es `clone` en vez de `checkout`. Esta distinción es importante, ya que Git recibe una copia de casi todos los datos que tiene el servidor.

Cada versión de cada archivo en la historia del proyecto se descarga por defecto cuando ejecutas `git clone`. De hecho, si el disco del servidor se corrompe, puedes usar cualquiera de los clones para restaurar el estado completo del proyecto, incluyendo su historial (aunque podrías perder algunos hooks del lado del servidor).

### Ejemplo de uso:

```bash
git clone https://github.com/libgit2/libgit2
```

Este comando:

* Crea un directorio llamado `libgit2`.
* Inicializa un directorio `.git` en su interior.
* Descarga toda la información del repositorio.
* Extrae una copia de trabajo de la última versión.

Si deseas clonar el repositorio a un directorio con otro nombre, puedes especificarlo así:

```bash
git clone https://github.com/libgit2/libgit2 mylibgit
```

Este comando hace lo mismo que el anterior, pero el directorio de destino se llamará `mylibgit`.

---

## Protocolos de transferencia en Git

Git te permite usar distintos protocolos de transferencia. El ejemplo anterior usa `https://`, pero también puedes utilizar:

* `git://`
* `usuario@servidor:ruta/del/repositorio.git` (protocolo SSH)



¿Quieres que lo guarde como archivo `.md` también?
```
