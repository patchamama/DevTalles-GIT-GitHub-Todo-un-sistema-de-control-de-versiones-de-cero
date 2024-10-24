## dev/Talles: GIT+GitHub: Todo un sistema de control de versiones de cero

_https://cursos.devtalles.com/courses/take/git-github-control-versiones_

## Más referenciado

- Solucionar error que no me permite hacer un `git push` pues mi punto de actualización está atrasado (behind) en relación al remoto.

> Lo mejor pudiera hacer un rebase con un git pull y solucionar los conflictos en local y después el push.
> Si prefieres mantener un historial más limpio, puedes usar rebase en lugar de merge.
> Esto aplicará tus cambios locales encima de los cambios remotos.
> Asegúrate de estar en la rama correcta:
> 
> `git checkout <nombre_de_rama>`
> 
> Ejecuta el siguiente comando para hacer un pull con rebase:
> 
> `git pull --rebase origin <nombre_de_rama>`
> 
> Resuelve cualquier conflicto que pueda surgir, luego continúa con el rebase usando:
> 
> `git rebase --continue`
> 
> Finalmente, intenta hacer el push nuevamente:
> 
> `git push origin <nombre_de_rama>`

## Secciones

### [Sección 1: Inicio del curso]()

- [Instalaciones necesarias](https://cursos.devtalles.com/courses/take/git-github-control-versiones/lessons/35323631-objetivos-del-curso)

### [Sección 2: Git - Fundamentos](https://cursos.devtalles.com/courses/take/git-github-control-versiones/lessons/35324134-introduccion-a-los-fundamentos-de-git)

```
# Conocer la versión de git instalada
git --version

# Ayuda de git
git --help
git --help commit
git --help config

# configurar git
git config --global user.name "Armando Urquiola"
git config --global user.email "miemail@gmail.com"
# para verificar la configuración existente
git config --global -e
```

- [Nuestro primer repositorio]()

```
# Crear repo
git init

# conocer información (rama, archivo no actualizados,...)
git status

# añadir archivos para darle seguimiento
git add <archivo o carpeta a agregar>
# añadir todo
git add .
# añadir todos los html y los js de la carpeta js
git add *.html js/*.js
# Sí una carpeta está vacía, git no la agrega a los untracked, para que git agregue la carpeta,
# dentro de esta se agrega un archivo de nombre .gitkeep vacío

# eliminar archivo del seguimiento (stage)
git reset <archivo o carpeta>

# eliminar solo el archivo o carpeta del staged y no de local
git rm -r --cached nombre_de_la_carpeta_o_archivo/

# agregar archivos al stage local
git commit -m "Primer commit"

#Error o warning: LF will be replaced by CRLF in browserconfig.xml. Corrección:
git config core.autocrlf true

# Restaurar el proyecto a como estaba en el último commit, reconstruyendo los directorios y archivos que tenían seguimiento
git checkout -- .
# Solo restaurar un archivo modificado
git checkout -- <archivo-a-restaurar>
```

- Ramas / Branches (lugar donde nos encontramos trabajando)

```
# Conocer rama activa
git branch
# cambiar el nombre de la rama (renombrar). En este caso renombra "master" a "main":
git branch -m master main
# definir el nombre de la rama principal por defecto: main, master...
git config --global init.defaultBranch <name>

# Agregar y hacer commit de archivos con seguimiento (tracked)
git commit -am "mensaje"

# ver commits hechos de más reciente a más viejo
git log
```

# Creando Alias para nuestros comandos

```
# git s > git status --short
git config --global alias.s "status -sb"
# git lg > git log --online --decorate --all --graph ...
git config --global alias.lg "log --graph --abbrev-commit --decorate --format=format:'%C(bold blue)%h%C(reset) - %C(bold green)(%ar)%C(reset) %C(white)%s%C(reset) %C(dim white)- %an%C(reset)%C(bold yellow)%d%C(reset)' --all"
# modificar los alias en el archivo de configuración
git config --global -e
```

### [Sección 3: Un poco más allá de los fundamentos de GIT](https://cursos.devtalles.com/courses/take/git-github-control-versiones/lessons/35329546-introduccion-a-la-seccion)

- Cambios en los archivos

```
# ver los cambios de archivos antes del staged (commit)
git diff
# ver lo que se cambió en el staged en relación al último push
git diff --staged
```

- Actualizar mensaje del commit y revertir commits

```
# Actualizar el mensaje del último commit para corregirlo
git commit --amend -m "nuevo mensaje actualizado"
# Editar el último mensaje y corregir el texto
git commit --amend
# La forma larga sería moverse al git anterior sin perder los cambios, agregar archivos y hacer nuevamente el commit
git reset --soft HEAD^
git add .
git commit -m "nuevo mensaje actualizado"

# Moverse a un commit determinado y hacer uso de esa versión
git reset --soft <hash>
```

- Viajes en el tiempo, resets y reflog

```
# Moverse a un determinado cambio sin eliminar los cambios
git reset --soft <hash>

# Cuidado! Dejar el respositorio exactamente a como estaba en un punto del tiempo y se pierde del git log el historial pero puede verse todo lo hecho con git reflog
git reset --hard <hash>

# Ver todos los cambios realizados o historial completamente que permite acceder a cualquier hash incluso los que no aparecen "git status" usando git reset...
git reflog
```

- Cambiar el nombre y eliminar archivos mediante git

```
# Renombrar un archivo en que estamos trabajando en la carpeta local y en el staged
git mv <archivo-inicial> <nuevo-nombre>

# Eliminar un archivo local y marcarlo como eliminado en el staged (que ya está en el staged), es necesario hacer un commit para que se elimine completamente en el staged
git rm <nombre-de-archivo>
```

- Ignorando archivos que no deseamos

Se debe de crear una archivo de nombre `.gitignore` donde se especifican todos los archivos y directorios a los que no se desea dar seguimiento, por ejemplo:

```
dist/
node_modules/
.env
.env.py
*.log
```

- [Ejercicios a resolver y ayuda](https://patchamama.github.io/DevTalles-GIT-GitHub-Todo-un-sistema-de-control-de-versiones-de-cero/)

### Sección 4: Ramas, uniones, conflictos y tags

```
# Crear rama
git branch <nueva-rama>
# Cambiar de rama
git checkout <rama>
# con un solo comando crear y cambiar de rama
git checkout -b <nueva-rama>

# Hacer un merge de una rama en otra. Hay que ubicarse en la rama de destino como activa
git checkout <rama-destino>
git merge <rama-fuente>

# Eliminar una rama
git branch -d <nombre-de-rama>
```

- Creando etiquetas - Tags

Los _tags_ son mensajes o etiqueta que se le pone al último commit tal como una versión información de un release.

```
# Ver todos los tag que existen
git tag
# Agregar un tag
git tag <nombre-del-tag>
# Eliminar un tag
git tag -d <nombre-del-tag>

# Usando versión semántica
git tag -a v1.0.0 -m "Version 1.0.0 lista"
# Poner una versión a un commit determinado usando el hash
git tag -a v0.1.0 <hash> -m "version Alpha de nuestra app"

# Ver detalles de una etiqueta
git show <nombre-del-tag>

# Subir todos los tags con push
git push --tags
```

### Introducción a la sección - Stash

_Permite tener todos los cambios seguros, guardándolos en un espacio temporal local para posteriormente retomarlo, incluso lo que no se han grabado en la rama_
_WIP: work in progress al hacer un git lg significa que es un stash hecho en ese punto_

```
# Guardar el estado actual del proyecto en la rama activa solamente
git stash
# Listar los stash realizados
git stash list
# Restaurar el último stash guardado y borra el estado actual del proyecto
git stash pop
# Eliminar todos los stash creados (solo serían visibles con git reflog)
git stash clear
# Eliminar un stash
git stash drop <stash>
# Restaurar un stash determinado tras listarlo (git stash list). stash@{0} es como un hash
git stash apply <stash>
# Ver los cambios de un determinado stash (el stash@{1})
git stash show <stash>
# Grabar un stash con un nombre determinado
git stash save "mensaje del stash"
# Listar con más detalles los stash realizados y cambios
git stash list --stat
```

- Rebase - Actualizando ramas

_Muchas veces se crea una rama features-branch para desarrollar algunas funcionalidades y a la vez en la rama master-main se agregan después otros cambios pero deseamos que los cambios de la rama main se pasen a la feature-branch pues los necesitamos (esto también ayuda muchas veces para solucionar conflictos). En este caso, lo mejor es ubicarnos en la feature-branch y después insertar los cambios de la rama main: git rebase main. Después es muy fácil hacer un merge a la rama master al no haber conflictos_

```
# Ubicarse en la rama feature-branch
git checkout <branch>
# Insertar los cambios de la rama main a esta
git rebase main
# Sí se desea hacer un merge del feature-branch a master-main ahora es  muy fácil al no haber conflictos y se haría un "fast-forward" con:
git checkout main
git merge <feature-branch>
```

- Unir ramas (squash) o renombrarlas

_El git rebase -i... lo que hace es editar manualmente varias commits y permite borrar algún commit, unirlos, cambiar el mensaje..._
_El pick no hace nada, lo tiene (el commit) en cuenta o lo toma simplemente. Para acambiar el nombre del mensaje hay que cambiar el pick por reword_

```
# Trabajar con los últimos 4 commits para unir una rama en otra. Se cambia el pick por squash frente a la línea y esto permite que este commit se una con el anterior.
git rebase -i HEAD~4
```

### Documentation

- https://git-scm.com/docs/git-stash
- https://git-scm.com/book/es/v2/Ramificaciones-en-Git-Reorganizar-el-Trabajo-Realizado (git rebase...)

## Sección 6: Inicios en GitHub, Git Remote, Push & Pull

- Hosted services:
  - BitBucket
  - GitHub

* Manejados por nosotros mismos:
  - Gitosis

```
# Agregar un repositorio remoto
git remote add origin <URL>
# Conocer los repo remotos que tenemos configurados
git remote -v
# Copiar un cambio al servidor remoto
git push -u origin master
    _(-u permite que se especifique por defecto en que rama se llevarán los cambios a realizar y master es la rama a actualizar)_
```

- Obtener últimos cambios del repositorio remoto

```
# Obtener cambios existentes en el remote de la rama main (github u otro, se puede ver con git remote -v)
git pull origin main
git pull <remote> <rama> (remote puede ser origin u otro agregado con git add <remote> <url>)
```

- Definir forma de resolver el pull

```
git config --global pull.ff only (fast-forward only)
git config --global rebase off   (merge)
git config --global rebase on    (rebase)

git config -e                    (para comprobar la configuración existente)
```

- Clonar un proyecto

```
git clone <url-del-proyecto>
```

¡Importante! _Al hacer un git pull pueden haber conflictos y de estar especificado por defecto hacer un "fast-foward", no se ejecutará el git pull y sería necesario cambiar el tipo de pull en el config por merge o rebase tal como `git config rebase on` y después haciendo un `git pull` se haría y automáticamente se generarían los archivos con conflictos que podemos abrir y manualmente resolver los conflictos. Después estaríamos en medio de un rebase o git interactivo y no de una rama (esto se ve haciendo un `git status` por lo que habría que hacer un `git rebase --continue` para continuar (o --abort sí se desea abordar) y después es necesario hacer un `git add <archivo-modificado>` y `git commit -m` ... para comentar la acción del conflicto resuelto o merge realizado y después un git pull para que se lleve a cabo. También es posible al hacer un `git push` que se generen errores por haber cambios en el servidor remoto y en ese caso lo mejor sería hacer un àgit pull`y resolver localmente los conflictos y después el`git push`._

### Documentación

- ¿Qué es Gitosis? https://wiki.archlinux.org/title/gitosis#:~:text=Gitosis%20is%20a%20tool%20which,system%20accounts%20on%20the%20server.
- Instalación y configuración https://github.com/res0nat0r/gitosis
- Guardar su usuario y contraseña en la máquina LINUX
  - Para usuario de OSx 10.0 o superior, el KeyChain se los maneja automáticamente. https://docs.github.com/en/get-started/getting-started-with-git/caching-your-github-credentials-in-git#platform-linux

## Sección 7: GitHub - básico

- MarkDown y GitHub markdown

  - Tutorial de Markdown: [Markdown Tutorial](https://www.markdowntutorial.com/)
  - GitHub Markdown sheet: [GitHub Markdown Style Sheet](https://docs.github.com/en)
  - Emojis de GitHub: [Emojis](https://www.webfx.com/tools/emoji-cheat-sheet/)
  - [Markdown cheatsheet](https://import.cdn.thinkific.com/643563/courses/1870146/markdowncheatsheetonline-220524-152537.pdf) o [aquí](docs/markdowncheatsheetonline.pdf)

- git pull vs git fetch

git fetch solo actualiza las referencias remotas sin modificar tu directorio de trabajo.
git pull actualiza tu directorio de trabajo y la rama actual con los cambios remotos.

    git pull = git fetch + git merge/rebase

Ejemplo práctico:
Supongamos que estás trabajando en la rama main y deseas actualizarla con los últimos cambios del repositorio remoto.

Usando git fetch:

```
git fetch origin
git log origin/main   # Revisa los cambios disponibles
git diff origin/main  # Ver cambios
git merge origin/main # Integra los cambios en tu rama actual
```

Usando git pull:

```
git pull origin main
```

En resumen, git fetch te permite tener un mayor control y planificación sobre la integración de cambios remotos, mientras que git pull ofrece una forma rápida y conveniente de mantener tu trabajo sincronizado con el repositorio remoto.

- Flujo de github

https://blog.mergify.com/understanding-the-github-pull-request-workflow/

## Sección 8: GitHub - Avanzado

Sí deseamos restableceer solamente un archivo de un determinado commit o branch en la rama actual es posible con:

`git checkout <branch o hash commit> <archivo-a-restaurar>`

- Feature branch - Revisando el trabajo de los compañeros

Con `git pull --all` a veces no se obtienen las ramas. Para listar las ramas locales y en remoto podemos usar:

`git branch --all` o `git branch -a`

Para obtener la rama en remoto y trabajar con ella hay que pasarse a ella y esto obliga a que se descargue con sus contenidos:

`git checkout <nombre-de-la-rama-remota>`

En ocasiones, no aparece localmente sincronizado o actualizado el nombre de las ramas con relación al remote y por ejemplo, sí listamos todas las ramas puede que aparezcan ramas que se borraron en el remote. Para actualizar todo esto se puede usar:

`git remote prune origin`

Al borrar una rama localmente, para poder borrarla en el remote (se pone :rama-borrada):

`git push origin :rama-borrada`

- Proteger rama en producción

Sí deseamos mantener una rama legacy o importante en producción, una forma de protegerla y tenerla accesible es asociarla a su vez a un Tag y de esa forma sí se borrara la rama, como el Tag está asociado a un commit es posible siempre usando el hash del commit, volver a crear la rama (también es posible usando `git reflog` para localizar el hash y después moverse a ese commit con `git checkout <hash>` y recrear la rama con `git checkout -b <nombre-rama-recuperada>`): Crear un Tag relacionado co la rama a proteger o de producción:

```
# Listar los tags
git tag
# Crear el tag nuevo relacionado con el feature-branch (producción)
git tag -a v0.0.1 -m "Versión 0.0.1 - Stable"
# Subir el tag
git push --tags
```

Recuperar rama a proteger o de producción importante borrada accidentalmente y que tiene asociada un Tag:

```
# Buscar tags existentes
git tag
# Activar el commit asociado con la versión que nos interesa, ejemplo: v0.0.1
git checkout v0.0.1
# El HEAD se ubicaría en el tag (lo podemos ver con un git s) pero sin una rama asociada (se había borrado)
git checkout -b <rama-a-recuperar>
# Actualizar la rama previamente borrada
git push
```

_También con `git reflog` podemos ver todo el historial y ramas y commits creados o borrados y localizar el punto en que se borró, ubicarse en este commit (`git checkout <hash-commit>`) y después crear nuevamente la rama borrada (`git checkout -b <rama-a-recuperar>` y hacer el git push. También visualmente desde github o gitlab podemos seleccionar el Tag, después desde ahí nos vamos al hash del último commit y en ese punto podemos crear una rama nueva._

## Sección 9: GitHub Issues, MileStones y Colaboradores

### Documentación

- https://guides.github.com/features/issues/

## Sección 10: Wikis, Proyectos y GitHub Pages

## Sección 11: Organizaciones y Equipos

## Sección 12: Gist

https://gist.github.com

VSCode Extension: https://marketplace.visualstudio.com/items?itemName=kenhowardpdx.vscode-gist
_Con esta extensión es posible hacer búsquedas e insertar código/snippets de mis gists personales. Para usarlo antes hay que generar un token desde el setting de github y en vscode hay que acceder desde el command palette (Ctrl-Shift-P) a "gist: Profile... > github.com" e ingresar al token que genereremos desde github > settings > Developer Settings > Personal access tokens > Tokens (classic) > generate new token > ponerle un nombre y solo marcar la opción de Select Scopes: gist. Una vez configurado, accediendo al command palette > gist : open gist podemos hacer búsquedas y seleccionar alguno._

## Sección 13: Fin del curso
