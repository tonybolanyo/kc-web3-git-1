1) Crear un repositorio

```
$ git init
```

2) Crear un archivo git-nuestro.md con el contenido:
>Git nuestro
>Git nuestro que estas en los repos
>Comprimidos sean tus commits
>Venga a nosotros tu log
>En el local como en el remote
>Danos hoy nuestro pull de cada día
>Perdona nuestros conflictos
>Como también perdonamos los de otros geeks
>No nos dejes caer en detached HEAD
>y líbranos de SVN
>git commit --amend

3) Añadir git-nuestro.md al staging area

```
$ git add git-nuestro.md
```

4) Mover lo que hay en el staging area al repositorio

```
$ git commit -m “Creado archivo git-nuestro.md”
```

5) Crear una rama llamada “styled”

```
$ git branch styled
```

6) Listar las ramas que hay en el repositorio

```
$ git branch
* master
  styled
```

7) Moverse a la rama “styled”

```
$ git checkout styled

8) Comprobar que se está en la rama correcta

```
$ git status
```

9) Modificar en el archivo git-nuestro.md:

>*Git* nuestro que estas en los repos
>Comprimidos sean tus *commits*
>Venga a nosotros tu *log*
>En el local como en el *remote*
>Danos hoy nuestro *pull* de cada día
>Perdona nuestros *conflictos*
>Como también perdonamos los de otros geeks
>No nos dejes caer en *detached HEAD*
>y líbranos de *SVN*
>`git commit --amend`

10) Añadir los cambios al staging área y luego pasarlos al repositorio

```
$ git add git-nuestro.md
$ git commit -m “Versión con estilos de git-nuestro.md”
```

11) Deshacer el último commit (perdiendo los cambios realizados en el working copy)

```
$ git reset --hard HEAD~1
HEAD is now at 96af428 Creado archivo git-nuestro.md
```

12) Rehacer el último commit (el que acabamos de deshacer)

```
$ git reflog
96af428 HEAD@{0}: reset: moving to HEAD~1
735ab5a HEAD@{1}: commit: Versión con estilo de git-nuestro.md
96af428 HEAD@{2}: checkout: moving from master to styled
96af428 HEAD@{3}: commit (initial): Creado archivo git-nuestro.md

$ git reset --hard 735ab5a
```

13) Hacer un merge con ‘master’ (styled absorbe a master)

```
$ git merge master
Already up-to-date.
```

14) Volver a la rama master

```
$ git checkout master
```

15) Crear una nueva rama llamada “htmlify”
16) Cambiar a la rama htmlify

Uno la 15 y 16 en un solo comando

```
$ git checkout -b "htmlify"
Switched to a new branch 'htmlify'
```

17) Modificar en el archivo git-nuestro.md:

><p><em>Git</em> nuestro que estas en los repos<br />
>Comprimidos sean tus <em>commits</em><br />
>Venga a nosotros tu <em>log</em><br />
>En el local como en el <em>remote</em><br />
>Danos hoy nuestro <em>pull</em> de cada día<br />
>Perdona nuestros <em>conflictos</em><br />
>Como también perdonamos los de otros geeks<br />
>No nos dejes caer en <em>detached HEAD</em><br />
>y líbranos de <em>SVN</em><br />
><code>git commit --amend</code></p>

18) Hacer un commit

```
$ git add git-nuestro.md
$ git commit -m "Cambiados estilos a HTML"
[htmlify e366fdc] Cambiados estilos a HTML
 1 file changed, 11 insertions(+), 12 deletions(-)
 rewrite git-nuestro.md (99%)
```

19) Hacer un merge de “htmlify” en “styled” (styled absorbe a htmlify)

```
$ git checkout styled
Switched to branch 'styled'

$ git merge htmlify
Auto-merging git-nuestro.md
CONFLICT (content): Merge conflict in git-nuestro.md
Automatic merge failed; fix conflicts and then commit the result.
```

20) Si hay conflictos, deberemos resolverlos quedándonos con el contenido de la rama “styled”.

```
$ vim git-nuestro.md
$ git add git-nuestro.md

$ git commit -m "Unión de rama htmlify en styled. Resuelto conflicto"
[styled 08c3c5b] Unión de rama htmlify en styled. Resuelto conflicto
```

21) Desde “master”, hacer un merge con “styled”

```
$ git checkout master
$ git merge styled
Updating 96af428..08c3c5b
Fast-forward
 git-nuestro.md | 19 +++++++++----------
 1 file changed, 9 insertions(+), 10 deletions(-)
```

22) Crear una rama “title” y cambiarse a esa rama

```
$ git checkout -b title
```

23) Añadir un título (a tu gusto) al archivo git-nuestro.md y hacer un commit.
```
$ vim git-nuestro.md
$ git add git-nuestro.md
$ git commit -m “Agregado un título a git-nuestro”
```

24) Volver a la rama master

```
$ git checkout master
```

25) Dibujar el diagrama

```
$ git log --graph --abbrev-commit --decorate --all
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

26) Hacer un merge “no fast-forward” de “title” en “master” (master absorbe a title)

```
$ git merge --no-ff title
Merge made by the 'recursive' strategy.
 git-nuestro.md | 2 ++
 1 file changed, 2 insertions(+)
```

27) Deshacer el merge (sin perder los cambios del working copy)

```
$ git reset HEAD~1
Unstaged changes after reset:
M       git-nuestro.md
```

28) Descartar los cambios

```
$ git checkout git-nuestro.md
```

29) Eliminar la rama “title”

```
$ git branch -d title
warning: deleting branch 'title' that has been merged to
         'refs/remotes/origin/title', but not yet merged to HEAD.
Deleted branch title (was ee54734).
$ git push origin --delete title
```

30) Rehacer el merge que hemos deshecho
Usando el id del commit, que devuelve el resultado anterior. En este caso podemos hacer fast forward.

```
$ git merge ee54734
Updating 08c3c5b..ee54734
Fast-forward
 git-nuestro.md | 2 ++
 1 file changed, 2 insertions(+)
```

31) Volver a master y eliminar el resto de ramas

```
$ git branch -d htmlify
Eliminada la rama htmlify (era e366fdc)
$ git push origin --delete htmlify
$ git branch -d styled
Eliminada la rama styled (era 08c3c5b)
$ git push origin --delete styled
```

32) Volver al commit inicial cuando se creó el poema

```
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

33) Volver al estado final, cuando pusimos título al poema

```
$ git reset --hard ee54734
```

34) Crear los siguientes tags:

>inicial: en el primer commit
>styled: modificación del paso 10
>htmlify: modificación del paso 17-18
>title: modificación del paso 30

```
$ git tag inicial 96af428
$ git tag styled 735ab5a
$ git tag htmlify e366fdc
$ git tag title ee54734
$ git push --tags
```

35) Ir al tag htmlify

```
$ git reset --hard htmlify
```
