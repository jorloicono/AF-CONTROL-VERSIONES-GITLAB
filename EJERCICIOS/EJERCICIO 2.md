
# Ejercicio Ramas, cambios y fusiones en Git

## Pasos a seguir:

1. Inicia un proyecto nuevo. Crea dos archivos y realiza dos commits: uno cada vez que agregues un archivo (usando `git add` en cada paso).
   - ¿Qué ramas tienes ahora?

2. Crea una nueva rama llamada `pruebas` y cámbiate a ella.

3. Modifica el primer archivo creado y realiza un commit con los cambios.

4. Vuelve a la rama `master` y examina el archivo que modificaste anteriormente.
   - ¿Cómo está? ¿Qué ves si consultas el historial de commits?

5. Regresa a la rama `pruebas` y revisa de nuevo el mismo archivo.
   - ¿Cómo está ahora?

6. Crea una nueva rama llamada `experimento`, partiendo desde `master`. En esa rama, añade otra línea al mismo archivo que modificaste en `pruebas`. Haz un commit con el cambio y vuelve luego a `pruebas`.
   - ¿Qué ves en el archivo en la rama `pruebas` ahora?

7. Cambia el nombre de la rama `experimento` a `pruebas2` usando el siguiente comando:

```

git branch -m experimento pruebas2

```

---

> **NO BORRES ESTE TEXTO**, lo utilizarás en el **Ejercicio 3**.

