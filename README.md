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

# eliminar archivo del seguimiento (stage)
git reset <archivo o carpeta>

# agregar archivos al stage local
git commit -m "Primer commit"

#Error o warning: LF will be replaced by CRLF in browserconfig.xml. Corrección:
git config core.autocrlf true

# Restaurar el proyecto a como estaba en el último commit, reconstruyendo los directorios y archivos que tenían seguimiento
git checkout -- .
```

### Documentación
