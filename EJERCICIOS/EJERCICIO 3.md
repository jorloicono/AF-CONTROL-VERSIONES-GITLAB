# Ejercicio Conflictos y resolución de merges en Git

## Pasos a seguir:

1. Ve a la rama `master` y realiza un merge de la rama `pruebas2`.

2. Una vez fusionadas, observa el contenido del archivo modificado previamente.
   - ¿Qué ves?

3. Realiza un cambio en el archivo1 desde la rama `master` y otro diferente en el archivo2 desde la rama `pruebas2`. Haz commit en ambas ramas, asegurándote de estar en la rama correcta antes de cada cambio.

4. Vuelve a la rama `master` y haz un merge con la rama `pruebas2`. Observa el contenido de `archivo2`.
   - ¿Qué ves?

5. Revisa el contenido de `archivo1` tanto en la rama `master` como en la rama `pruebas`.
   - ¿Son diferentes?

6. Intenta llevar los cambios de la rama `pruebas` a `master` con un `merge`.
   - ¿Qué pasa?

7. Ejecuta `git status` y revisa el contenido de los archivos afectados.
   - ¿Qué ves?

8. Piensa: ¿cómo resolverías este conflicto? ¿Qué pasos tomarías?

9. Ejecuta `git merge --abort`.
   - ¿Qué ha pasado con el repositorio? ¿Se ha deshecho el intento de fusión?

10. Intenta nuevamente realizar la fusión con los siguientes comandos:

    ```bash
    git checkout master
    git merge pruebas
    ```

11. Abre el archivo en conflicto con un editor de texto (como `vim`) y resuelve manualmente los conflictos.

12. Añade el archivo corregido al área de preparación y realiza el commit correspondiente:

    ```bash
    git add archivo1.txt
    git commit
    ```

   - ¿Te permite completar el merge ahora?

---

Este ejercicio te ayuda a experimentar con situaciones reales de conflicto y resolución durante fusiones en Git.
