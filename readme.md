# Respuestas al ejercicio 1

## ¿Qué comando utilizaste en el paso 11? ¿Por qué?

```
$ git reset --hard HEAD~1
```

- `reset` permite situar la copia de trabajo (working copy) en un commit concreto.
- La notación `HEAD~1` indica pa posición anterior al commit actual en la rama actual, por tanto `git reset HEAD~1` *deshace* el último commit situando el puntero HEAD en la posición anterior al comit actual.
- Por último, el flag `--hard` fuerza descartar los cambios en la working copy

## ¿Qué comando o comandos utilizaste en el paso 12? ¿Por qué?

```
$ git reflog
96af428 HEAD@{0}: reset: moving to HEAD~1
735ab5a HEAD@{1}: commit: Versión con estilo de git-nuestro.md
96af428 HEAD@{2}: checkout: moving from master to styled
96af428 HEAD@{3}: commit (initial): Creado archivo git-nuestro.md

$ git reset --hard 735ab5a
```

- Primero con `reflog` obtenemos los ID de los commits y vemos que el commit que acabamos de deshacer tiene un identificador que comienza por `735ab5a`
- Para volver a ese commit y rehacer la working copy usamos el comando `reset` con el modificador `--hard`

## El merge del paso 13, ¿Causó algún conflicto? ¿Por qué?

No hay conflicto. El resultado del comando `git merge master` devuelve el mensaje *Already up-to-date.* ya que todos los commits de la rama *master* forma parte de la rama *styled*.

## El merge del paso 19, ¿Causó algún conflicto? ¿Por qué?

Sí, el conflicto se prodice porque ambas ramas contienen modificaciones en las mimsas líneas del fichero `git-nuestro.md`. En este caso, git no es capaz de resolver el conflicto de forma automática y deja el archivo marcado para que la solución del conflicto se realice de forma manual.

## El merge del paso 21, ¿Causó algún conflicto? ¿Por qué?

No. En este caso el merge permite realizar un *fast forward* ya que los commits siguen una línea y basta con avanzar el puntero hasta el último commit de la rama styled.

## ¿Qué comando o comandos utilizaste en el paso 25?

```
$ git log --graph --abbrev-commit --decorate --all
```

Lo que devuelve el grafo siguiente:

```
* commit ee54734 (title)
| Author: Tony G. Bolaño <tonybolanyo@gmail.com>
| Date:   Thu Jun 22 14:43:29 2017 +0200
|
|     Agregado un título a git-nuestro
|
*   commit 08c3c5b (HEAD -> master, origin/styled, styled)
|\  Merge: 735ab5a e366fdc
| | Author: Tony G. Bolaño <tonybolanyo@gmail.com>
| | Date:   Thu Jun 22 13:45:28 2017 +0200
| |
| |     Unión de rama htmlify en styled. Resuelto conflicto
| |
| * commit e366fdc (origin/htmlify, htmlify)
| | Author: Tony G. Bolaño <tonybolanyo@gmail.com>
| | Date:   Thu Jun 22 13:07:26 2017 +0200
| |
| |     Cambiados estilos a HTML
| |
* | commit 735ab5a
|/  Author: Tony G. Bolaño <tonybolanyo@gmail.com>
|   Date:   Thu Jun 22 12:50:10 2017 +0200
|
|       Versión con estilo de git-nuestro.md
|
* commit 96af428 (origin/master)
  Author: Tony G. Bolaño <tonybolanyo@gmail.com>
  Date:   Thu Jun 22 12:46:13 2017 +0200

      Creado archivo git-nuestro.md
```

Básicamente solicitamos el log de manera gráfica (modificador `--graph`), con los IDs de los commits cortos, es decir, con solamente los primeros caracteres (modificador `abbrev-commit`), decorados con los nombres de las ramas y etiquetas (modificador `--decorate`) y mostrando todas las ramas, no sólo la actual en la que nos encontramos (modificador `--all`).

## El merge del paso 26, ¿Podría ser fast forward? ¿Por qué?

Sí, porque la rama *title* solamente tiene un commit por delante de la rama *master*, por tanto, bastaría con mover el puntero de la rama master a la misma posición de la rama *title*.

## ¿Qué comando o comandos utilizaste en el paso 27?

```
$ git reset HEAD~1
```

En este caso, el reset deja el archivo git-nuestro.md como modificado en el working copy, dejando el staging area vacío.

## ¿Qué comando o comandos utilizaste en el paso 28?

```
$ git checkout git-nuestro.md
```

De esta manera se descartan los cambios del archivo `git-nuestro.md` restableciendo el estado que tenía en el commit al que apunta HEAD.

## ¿Qué comando o comandos utilizaste en el paso 29?

```
$ git branch -d title
```

En mi caso, como ya tenía el repositorio sincronizado con github y había subido la rama, era necesario eliminar también la rama remota (para que la entrega coincidira con el estado final de mi repositorio local). Para esto he utilizado el comando `git push origin --delete title`

## ¿Qué comando o comandos utilizaste en el paso 30?

Al ejecutar el comando del paso 29, git devuelve el ID de la rama, que podemos usar para rehacer los pasos de esa rama.
En la consola podemos leer:

```
Deleted branch title (was ee54734)
```

Si utilizamos ese ID para hacer un merge, que en este caso puede ser fast forward, tenemos la solución con un sólo comando:

```
$ git merge ee54734
Updating 08c3c5b..ee54734
Fast-forward
 git-nuestro.md | 2 ++
 1 file changed, 2 insertions(+)```

## ¿Qué comando o comandos usaste en el paso 32?

$ git log
commit ee54734675debf3ad93cd68ae7b83ce75420c7c5
Author: Tony G. Bolaño <tonybolanyo@gmail.com>
Date:   Thu Jun 22 14:43:29 2017 +0200

    Agregado un título a git-nuestro

commit 08c3c5bb216e0d08733df51eb870eacd036218a8
Merge: 735ab5a e366fdc
Author: Tony G. Bolaño <tonybolanyo@gmail.com>
Date:   Thu Jun 22 13:45:28 2017 +0200

    Unión de rama htmlify en styled. Resuelto conflicto

commit e366fdc3f9714e55ff08947f4205485d66f8e2e2
Author: Tony G. Bolaño <tonybolanyo@gmail.com>
Date:   Thu Jun 22 13:07:26 2017 +0200

    Cambiados estilos a HTML

commit 735ab5a1e928e3ea00dbf7c53794637aa3cb5c53
Author: Tony G. Bolaño <tonybolanyo@gmail.com>
Date:   Thu Jun 22 12:50:10 2017 +0200

    Versión con estilo de git-nuestro.md

commit 96af428a6414884416f50add9e864df985ee2118
Author: Tony G. Bolaño <tonybolanyo@gmail.com>
Date:   Thu Jun 22 12:46:13 2017 +0200

    Creado archivo git-nuestro.md

$ git reset --hard 96af428
```

Primero usamos el comando `log` para *buscar* el ID del commit al que queremos volver, en este caso `96af428` y luego hacemos un hard reset para devolver la working copy al estado inicial.



## ¿Qué comando o comandos usaste en el punto 33?

De nuevo, hacemos un hard reset para dejar la working copy en el estado del commit al que queremos ir. En este caso, el ID es `ee54734`.

