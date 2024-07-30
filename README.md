## dev/Talles: GIT+GitHub: Todo un sistema de control de versiones de cero

_https://cursos.devtalles.com/courses/take/git-github-control-versiones_

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

# agregar archivos al stage local
git commit -m "Primer commit"

#Error o warning: LF will be replaced by CRLF in browserconfig.xml. Corrección:
git config core.autocrlf true

# Restaurar el proyecto a como estaba en el último commit, reconstruyendo los directorios y archivos que tenían seguimiento
git checkout -- .
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
# La forma larga sería moverse al git anterior sin perder los cambios, agregar archivos y hacer nuevamente el commit
git reset --soft HEAD^
git add .
git commit -m "nuevo mensaje actualizado"

# Moverse a un commit determinado
git reset --soft <hash>
```

### Documentación
