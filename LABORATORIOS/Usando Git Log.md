# Usando Git Log

## Inicialización de un Repositorio

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
    [cite\_start]Clonar un repositorio te proporciona automáticamente su historial completo de confirmaciones[cite: 2].

### Uso Básico de `git log`

[cite\_start]Por defecto, cuando ejecutas `git log` sin ningún parámetro, lista las confirmaciones en orden cronológico inverso, lo que significa que las confirmaciones más recientes aparecen primero[cite: 4]. Cada entrada de confirmación muestra la siguiente información:

  * [cite\_start]**Suma de comprobación SHA-1:** Un identificador único para la confirmación[cite: 5].
  * [cite\_start]**Autor:** El nombre y la dirección de correo electrónico de la persona que escribió el trabajo[cite: 5].
  * [cite\_start]**Fecha:** La fecha y hora en que se realizó la confirmación[cite: 5].
  * [cite\_start]**Mensaje de confirmación:** Una descripción de los cambios introducidos por la confirmación[cite: 5].

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

[cite\_start]`git log` ofrece una variedad de opciones para personalizar el formato de su salida[cite: 6, 7].

  * [cite\_start]**`-p` o `--patch`**: Muestra el parche (las diferencias) introducido en cada confirmación[cite: 8]. [cite\_start]Esto es muy útil para revisiones de código o para visualizar rápidamente lo que ha sucedido en las confirmaciones enviadas por un colaborador[cite: 11].

    ```bash
    git log -p
    ```

  * [cite\_start]**`-<n>`**: Muestra solo las últimas `n` confirmaciones[cite: 38].

    ```bash
    [cite_start]git log -p -2 # Muestra las últimas 2 confirmaciones con parches [cite: 8]
    ```

  * [cite\_start]**`--stat`**: Muestra estadísticas sobre los archivos modificados en cada confirmación, incluyendo el número de archivos cambiados y las líneas añadidas/eliminadas[cite: 13, 16].

    ```bash
    git log --stat
    ```

  * [cite\_start]**`--pretty`**: Modifica el formato de la salida[cite: 17].

      * [cite\_start]**`oneline`**: Imprime cada confirmación en una única línea, lo que puede resultar útil si estás analizando gran cantidad de confirmaciones[cite: 18].

        ```bash
        git log --pretty=oneline
        ```

      * [cite\_start]**`short`, `full`, `fuller`**: Muestran una salida similar con menos o más información, respectivamente[cite: 20].

      * [cite\_start]**`format`**: Te permite especificar tu propio formato personalizado utilizando marcadores de posición[cite: 21]. [cite\_start]Esto es especialmente útil si estás generando una salida para que sea analizada por otro programa[cite: 21].

        | Opción | [cite\_start]Descripción de la salida [cite: 22, 23, 24] |
        | :----- | :------------------------------------------- |
        | `%H` | [cite\_start]Hash de la confirmación [cite: 22] |
        | `%h` | [cite\_start]Hash de la confirmación abreviado [cite: 22] |
        | `%T` | [cite\_start]Hash del árbol [cite: 22] |
        | `%t` | [cite\_start]Hash del árbol abreviado [cite: 22] |
        | `%P` | [cite\_start]Hashes de las confirmaciones padre [cite: 22] |
        | `%p` | [cite\_start]Hashes de las confirmaciones padre abreviados [cite: 22] |
        | `%an` | [cite\_start]Nombre del autor [cite: 22] |
        | `%ae` | [cite\_start]Dirección de correo del autor [cite: 22] |
        | `%ad` | [cite\_start]Fecha de autoría (el formato respeta la opción `--date`) [cite: 22] |
        | `%ar` | [cite\_start]Fecha de autoría, relativa [cite: 22] |
        | `%cn` | [cite\_start]Nombre del confirmador [cite: 24] |
        | `%ce` | [cite\_start]Dirección de correo del confirmador [cite: 24] |
        | `%cd` | [cite\_start]Fecha de confirmación [cite: 24] |
        | `%cr` | [cite\_start]Fecha de confirmación, relativa [cite: 24] |
        | `%s` | [cite\_start]Asunto (título del mensaje de confirmación) [cite: 24] |

        **Ejemplo usando `--pretty=format`:**

        ```bash
        git log --pretty=format:"%h %an, %ar: %s"
        ```

        [cite\_start]**Autor vs. Confirmador:** El autor es la persona que escribió originalmente el trabajo, mientras que el confirmador es quien lo aplicó[cite: 26]. [cite\_start]Por lo tanto, si envías un parche a un proyecto y uno de sus miembros lo aplica, ambos recibiréis reconocimiento: tú como autor y el miembro del proyecto como confirmador[cite: 27].

  * [cite\_start]**`--graph`**: Añade un pequeño gráfico ASCII mostrando tu historial de ramificaciones y uniones[cite: 30]. [cite\_start]Esta opción es especialmente útil combinada con `oneline` o `format`[cite: 29].

    ```bash
    git log --pretty=format:"%h %s" --graph
    ```

### Limitar la Salida de `git log`

[cite\_start]Además del formateo, puedes limitar la salida de `git log` para mostrar solo un subconjunto de confirmaciones[cite: 36].

  * [cite\_start]**`--since` o `--after`**: Muestra aquellas confirmaciones hechas después de la fecha especificada[cite: 40, 51]. [cite\_start]Puedes indicar una fecha concreta ("2008-01-15") o relativa ("hace 2 años, 1 día y 3 minutos")[cite: 42].
    ```bash
    [cite_start]git log --since="2.weeks" [cite: 41]
    ```
  * [cite\_start]**`--until` o `--before`**: Muestra aquellas confirmaciones hechas antes de la fecha especificada[cite: 40, 51].
    ```bash
    git log --until="2008-01-15"
    ```
  * [cite\_start]**`--author`**: Filtra las confirmaciones por autor, mostrando solo aquellas confirmaciones cuyo autor coincide con la cadena especificada[cite: 44, 51].
    ```bash
    git log --author="Scott Chacon"
    ```
  * [cite\_start]**`--committer`**: Muestra solo aquellas confirmaciones cuyo confirmador coincide con la cadena especificada[cite: 51].
    ```bash
    git log --committer="John Doe"
    ```
  * [cite\_start]**`--grep`**: Permite buscar palabras clave entre los mensajes de confirmación[cite: 44]. [cite\_start]Ten en cuenta que si quieres aplicar `--author` y `--grep` simultáneamente, tienes que añadir `--all-match`, o el comando mostrará las confirmaciones que cumplan cualquiera de las dos, no necesariamente las dos a la vez[cite: 45].
    ```bash
    git log --grep="bugfix"
    ```
  * [cite\_start]**`-S <cadena>`**: Muestra solo aquellas confirmaciones que añaden o eliminan código que corresponda con la cadena especificada[cite: 46, 51]. [cite\_start]Por ejemplo, si quieres encontrar la última confirmación que añadió o eliminó una referencia a una función específica[cite: 46]:
    ```bash
    git log -Sfunction_name
    ```
  * [cite\_start]**`-- <ruta>`**: Limita la salida a aquellas confirmaciones que introdujeron un cambio en un directorio o archivo específico[cite: 47]. [cite\_start]Esta debe ser siempre la última opción y suele ir precedida de dos guiones (`--`) para separar la ruta del resto de opciones[cite: 48].
    ```bash
    git log -- README.md
    ```

### Ejemplo Combinado

[cite\_start]Para ver cuáles de las confirmaciones hechas sobre archivos de prueba del código fuente de Git fueron enviadas por Junio Hamano, y no fueron uniones, en el mes de octubre de 2008, ejecutarías algo así[cite: 52]:

```bash
git log --pretty="%h %s" --author="gitster" --since="2008-10-01" \
[cite_start]--before="2008-11-01" --no-merges t/ [cite: 53]
```
