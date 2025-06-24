# Usando Git Log

Para ver eficazmente tu historial de confirmaciones en Git, utilizarás principalmente el comando `git log`. Este comando es muy versátil y ofrece numerosas opciones para adaptar su salida a tus necesidades específicas.

### Inicialización de un Repositorio

Antes de poder ver el historial de confirmaciones, necesitas un repositorio Git. Si no tienes uno, puedes:

  * **Inicializar un nuevo repositorio:**
    ```bash
    git init
    ```
    Este comando crea un nuevo repositorio Git vacío en el directorio actual.
  * **Clonar un repositorio existente:**
    ```bash
    git clone [url_del_repositorio]
    ```
    Por ejemplo, para clonar el proyecto "simplegit" utilizado en la documentación:
    ```bash
    git clone https://github.com/schacon/simplegit-progit
    ```
    Clonar un repositorio te proporciona automáticamente su historial completo de confirmaciones.

### Uso Básico de `git log`

Por defecto, cuando ejecutas `git log` sin ningún parámetro, lista las confirmaciones en orden cronológico inverso, lo que significa que las confirmaciones más recientes aparecen primero. Cada entrada de confirmación muestra la siguiente información:

  * **Suma de comprobación SHA-1:** Un identificador único para la confirmación.
  * **Autor:** El nombre y la dirección de correo electrónico de la persona que escribió el trabajo.
  * **Fecha:** La fecha y hora en que se realizó la confirmación.
  * **Mensaje de confirmación:** Una descripción de los cambios introducidos por la confirmación.

**Ejemplo:**

```bash
$ git log
commit ca82a6dff817ec66f44342007202690a93763949
Author: Scott Chacon <schacon@gee-mail.com>
Date: Mon Mar 17 21:52:11 2008 -0700

    changed the version number

commit 085bb3bcb608e1e8451d4b2432f8ecbe6306e7e7
Author: Scott Chacon <schacon@gee-mail.com>
Date: Sat Mar 15 16:40:33 2008 -0700

    removed unnecessary test

commit allbef06a3f659402fe7563abf99ad00de2209e6
Author: Scott Chacon <schacon@gee-mail.com>
Date: Sat Mar 15 10:31:28 2008 -0700

    first commit
```

### Opciones Útiles de `git log` para Formatear la Salida

`git log` ofrece una variedad de opciones para personalizar el formato de su salida.

  * **`-p` o `--patch`**: Muestra el parche (las diferencias) introducido en cada confirmación. Esto es muy útil para revisiones de código o para visualizar rápidamente lo que ha sucedido en las confirmaciones enviadas por un colaborador.

    ```bash
    git log -p
    ```

  * **`-<n>`**: Muestra solo las últimas `n` confirmaciones.

    ```bash
    git log -p -2 # Muestra las últimas 2 confirmaciones con parches
    ```

  * **`--stat`**: Muestra estadísticas sobre los archivos modificados en cada confirmación, incluyendo el número de archivos cambiados y las líneas añadidas/eliminadas.

    ```bash
    git log --stat
    ```

  * **`--pretty`**: Modifica el formato de la salida.

      * **`oneline`**: Imprime cada confirmación en una única línea, lo que puede resultar útil si estás analizando gran cantidad de confirmaciones.

        ```bash
        git log --pretty=oneline
        ```

      * **`short`, `full`, `fuller`**: Muestran una salida similar con menos o más información, respectivamente.

      * **`format`**: Te permite especificar tu propio formato personalizado utilizando marcadores de posición. Esto es especialmente útil si estás generando una salida para que sea analizada por otro programa.

        | Opción | Descripción de la salida |
        | :----- | :------------------------------------------- |
        | `%H` | Hash de la confirmación |
        | `%h` | Hash de la confirmación abreviado |
        | `%T` | Hash del árbol |
        | `%t` | Hash del árbol abreviado |
        | `%P` | Hashes de las confirmaciones padre |
        | `%p` | Hashes de las confirmaciones padre abreviados |
        | `%an` | Nombre del autor |
        | `%ae` | Dirección de correo del autor |
        | `%ad` | Fecha de autoría (el formato respeta la opción `--date`) |
        | `%ar` | Fecha de autoría, relativa |
        | `%cn` | Nombre del confirmador |
        | `%ce` | Dirección de correo del confirmador |
        | `%cd` | Fecha de confirmación |
        | `%cr` | Fecha de confirmación, relativa |
        | `%s` | Asunto (título del mensaje de confirmación) |

        **Ejemplo usando `--pretty=format`:**

        ```bash
        git log --pretty=format:"%h %an, %ar: %s"
        ```

        **Autor vs. Confirmador:** El autor es la persona que escribió originalmente el trabajo, mientras que el confirmador es quien lo aplicó. Por lo tanto, si envías un parche a un proyecto y uno de sus miembros lo aplica, ambos recibiréis reconocimiento: tú como autor y el miembro del proyecto como confirmador.

  * **`--graph`**: Añade un pequeño gráfico ASCII mostrando tu historial de ramificaciones y uniones. Esta opción es especialmente útil combinada con `oneline` o `format`.

    ```bash
    git log --pretty=format:"%h %s" --graph
    ```

### Limitar la Salida de `git log`

Además del formateo, puedes limitar la salida de `git log` para mostrar solo un subconjunto de confirmaciones.

  * **`--since` o `--after`**: Muestra aquellas confirmaciones hechas después de la fecha especificada. Puedes indicar una fecha concreta ("2008-01-15") o relativa ("hace 2 semanas", "hace 2 años, 1 día y 3 minutos").
    ```bash
    git log --since="2.weeks"
    ```
  * **`--until` o `--before`**: Muestra aquellas confirmaciones hechas antes de la fecha especificada.
    ```bash
    git log --until="2008-01-15"
    ```
  * **`--author`**: Filtra las confirmaciones por autor, mostrando solo aquellas confirmaciones cuyo autor coincide con la cadena especificada.
    ```bash
    git log --author="Scott Chacon"
    ```
  * **`--committer`**: Muestra solo aquellas confirmaciones cuyo confirmador coincide con la cadena especificada.
    ```bash
    git log --committer="John Doe"
    ```
  * **`--grep`**: Permite buscar palabras clave entre los mensajes de confirmación. Ten en cuenta que si quieres aplicar `--author` y `--grep` simultáneamente, tienes que añadir `--all-match`, o el comando mostrará las confirmaciones que cumplan cualquiera de las dos, no necesariamente las dos a la vez.
    ```bash
    git log --grep="bugfix"
    ```
  * **`-S <cadena>`**: Muestra solo aquellas confirmaciones que añaden o eliminan código que corresponda con la cadena especificada. Por ejemplo, si quieres encontrar la última confirmación que añadió o eliminó una referencia a una función específica:
    ```bash
    git log -Sfunction_name
    ```
  * **`-- <ruta>`**: Limita la salida a aquellas confirmaciones que introdujeron un cambio en un directorio o archivo específico. Esta debe ser siempre la última opción y suele ir precedida de dos guiones (`--`) para separar la ruta del resto de opciones.
    ```bash
    git log -- README.md
    ```

### Ejemplo Combinado

Para ver cuáles de las confirmaciones hechas sobre archivos de prueba del código fuente de Git fueron enviadas por Junio Hamano, y no fueron uniones, en el mes de octubre de 2008, ejecutarías algo así:

```bash
git log --pretty="%h %s" --author="gitster" --since="2008-10-01" \
--before="2008-11-01" --no-merges t/
```
