# Guía rápida - Git 

Comandos de Git usados en el día a día. Versión: Explicado rapidillo pa' ti y pa' mi...

## Diferentes estados de tu archivo
1. **Working area**: Pues como bien dice, el momento en el que estás trabajado. Escribiendo tus cosas, borrando...
2. **Stagin Area** o **Index**: Oye esto ya me mola, creo que lo debería guardar...
3. **Commited** o **HEAD**: ¡ Ala guardao !

![Flujo de trabajo](https://github.com/pablorgarcia/Guia-rapida-para-Git/blob/master/images/workflow.png "Flujo de trabajo")


### Mirar el estado de nuestros archivos 

`git status`
Nos dice el estado en el que se encuentran nuestros archivos. Si están sin seguimiento, si tienen seguimiento pero se han cambiado o si están en Stagin ya.

### Meter en Stagin Area

`git add <archivo>`
Añade el archivo que le pasemos a stagin area, y que luego estará en el commit.

`git add <archivo1> <archivo2>`
Añade varios archivos a stagin.
 
`git add .`
El "." agrega todo a stagin.

### Remover de Stagin Area

`git rm <archivo>`
Elimina un archivo de stagin.

### Hacer un commit

`git commit -m "Mensaje descriptivo del cambio"`
Con este comando hacemos un commit de los archivos que estén en stagin area.

Se hace una instantanea de los archivos en ese momento y se agrega a la cabecera (HEAD) quedando registrado y guardado como un punto en el tiempo. Pero aún no en tu repositorio remoto.

`git commit -m "Mensaje descriptivo del cambio" <archivo>`
Hacemos un commit de solo un archivo de stagin.

`git commit --amend -m "Mensaje descriptivo del cambio"`
Modificamos el último commit.

### Hacer un push
Tus cambios están ahora en el HEAD de tu copia local. Para enviar estos cambios a tu repositorio remoto ejecuta.
`git push origin master`

### Guardar rápido tus cambios, sin llegar a hacer un 'add'

Muchas veces, cuando has estado trabajando una parte del código, los archivos se pueden desordenar y al querer cambiar de rama un momento para hacer otra cosa hay un conflicto. Si no quieres hacer un commit de un trabajo porque va por la mitad y quieres volver a ese punto más tarde puedes hacer un:

`git stash`

`git stash list` si quieres ver una lista con los archivos que tienes 'staseados'

`git stash pop`
Los cambios guardados en stash vuelven.

`git status --show-stash`
Ver el status con los archivos en stash.

### ¿Cómo descartar los cambios 'unstaged'?

`git checkout -- .`
Para todos los archivos 'unstaged'. Esto reemplaza los cambios en tu directorio de trabajo con el último contenido de HEAD. Los cambios que ya han sido agregados al Index, así como también los nuevos archivos, se mantendrán sin cambio.

`git checkout -- path/to/file/to/revert`
Para un archivo en un path especifico.

### Listar los commits

`git log`
Nos mostrará un log o histórico de commits realizados en este repositorio.

Copiarlo en un archivo de texto o similar puede ser una gran idea si piensas viajar en el tiempo de tu histórico.

Para salir de ahí pulsa `q`.

### Viajar en el tiempo

`git checkout <codigo_sha>`
Nos lleva al estado del repositorio en ese momento. 

Para volver a donde estábamos tienes que coger el código SHA en el que te encontrabas.

### Desacer el commit volviendo al anterior, desaciendo los cambios

`git reset --hard`
No te han gustado los cambios y quieres volver al estado del último commit, eliminando de manera permanente todos los cambios a todos los archivos realizados.
La opción "--hard" provoca que si hubiera archivos que no se han agregado al repositorio permanecerán.

`git reset --soft`
Iguala tu 'staging area' con el 'repositorio', no afectará tu 'working directory' y hace un `add` a los archivos. No borra el código.

## Las ramas
Toma el estado en el que se encuentra el archivo y hace una derivación a otro espacio, de forma que se puede trabajar en él sin afectar al archivo inicial.

Más adelante podemos juntarlos.

### Crear una rama

`git branch <nombre_rama>`
Por ejemplo: `git branch someTest`

### Cambiarse a esa rama

`git checkout <nombre_rama>`
Por ejemplo: `git checkout mi-rama`

### Trabaja en tu rama 

Dentro de tu rama puedes trabajar normal, hacer tus commits y avanzar en el proyecto, pero lo que haces está sólo en esa rama. 

Si cambias de rama sin más lo que hayas hecho en esa rama no lo vas a ver.

Para poder juntar todo tienes que mergear (fundir o fusionar) las ramas.

## Merge

### Cuando mergeas pueden pasar dos cosas

1. Todo se ha hecho bien y no hay problemas.
2. Cada uno ha tocado el mismo archivo por su cuenta y al mergear las ramas dan conflicto. Git no sabe que cambios son los que han de permanecer, y lo junta pero con conflicto.

### Resolver conflicto

En un mundo ideal lo suyo es ponerse de acuerdo en que hace cada uno. En caso de conflicto sentarse con la persona con la que nos ha surgido y determinar qué es lo que vale. 

Pero si no es así toma la decisión de que es lo válido y "pa-lante". Intenta no romper nada... X)

* Resolver el conflicto.
* Comitear cambios.
* Subirlos.
* Comprueba que todo está ok y que en tu rama están los cambios finales.

#### Nombres de ramas famosos

* develop ó dev
* feature/loquesea
* bugfix/esePeasoBug
* hotfix/ayQueEstáEnProducción
* master

![Image of git branch schema](https://s3.amazonaws.com/media-p.slid.es/uploads/843308/images/4760613/git-flow-commands-without-flow.png)


### Ya has acabado commit y hay que subirlo.

`git commit -m "blablablaa #nºissue"`
Para que el commit que vas a hacer quede ligado a un Issue en concreto:

`git commit -m "blablablaa Fix #nºissue"`
Para que el commit que vas a hacer cierre un Issue en concreto:

`git push origin <nombre-rama>`
A la rama donde estás... ¿vale?

Una vez tienes ya todo guardado y subido, mergea tu rama a donde corresponda, por ejemplo develop:

1. Hazte pull de la rama donde vas a meter tu rama. 
2. Muévete a la rama donde vas a llevar tus cambios.
3. Haz merge de tu rama a la rama donde estás.

`git merge <mi-rama>`
Estando en develop

Las ramas molan pero no seas Diógenes.
Mantener la higiene de ramas es algo importante. Si no vas a desarrollar una segunda release, o incluso un proyecto paralelo... cuando acabes con el trabajo de una rama... ¡¡¡MÁTALA!!! muaaahahahahahha.

`git branch` para ver la lista de las ramas que has creado en local.

`git branch -D <nombre-rama>` utilizamos el '-D' para eliminar la rama.


## Cuando tienes un repo en remoto

`git pull origin <nombre_de_la_rama>`

Si hay conflicto resuelve y comitea.

`git push origin <nombre_de_la_rama>` 

En resumen:
Cuanto más acutalizada tengas la rama donde estás y tu repo, menos conflictos tendrás. ANTES DE HACER PUSH HAZ PULL.

`git fetch` Descarga el historial del repo remoto.


### Creando un projecto desde cero
git init
git add README.md
git add .
git commit -m "first commit"
git remote add origin https:// github.com / <userName> / <repoName>.git
git push --force origin master

### ¿Tu repositorio local no está apuntando al repositorio remoto?

`git remote add <nombre_para_remoto> <url>`
Ejemplo: `git remote add origin https://github.com/usuario/nombre_del_repositorio.git`

`git push -u origin master`

Cuando hagas push, recuerda hacerlo a ambos (o tendrás un bonito caos...)

### Quieres apuntar a un nuevo proyecto en Github?

`git remote set-url <remote_name> <remote_url>` 

`git remote set-url origin nombre-app`

## Configurar Git

`git config --global user.name "nombre"`

`git config --global user.email "tu_mail@example.com"`

`git config --list`
Comprobar q está todo ok.

## Crear un repositorio en local

`git init`
Navegar con la terminal hasta dentro de la carpeta que queremos.

## Clonar un repositorio de GitHub en local

`git clone <url del proyecto>`
Crear un repositorio en local dentro de la carpeta que queremos, pero trayéndolo de GitHub.

La url la cogemos de la ventana que sale al pulsar el botón de 'Clone or download'.

Hay una opción para mejorar la velocidad y el espacio en disco al clonar un repositorio
`git clone <url del proyecto> --depth 1` con el valor a 1
No te descargará todo el historial del repositorio, a veces, ni siquiera lo necesitas. Especialmente interesante para procesos en CI.

## Elimina Git del proyecto para empezar de nuevo
`rm -rf .git`

En la carpeta raiz del proyecto. Después:

`git init`

## Gestión de conflictos

Lo ideal es que no se den... pero se van a dar.

Si tienes un conflicto ¡No entres en pánico!
Es bueno tener papel a mano para anotar cosas.
Intenta siempre hablar con la persona que ha hecho el código con el que has tenido conflicto.
Fíjate SIEMPRE en lo que dice la consola, da muchas pistas.
Un plugin en el editor que uses puede ser una gran ayuda.

Ten siempre MUY en cuenta que es lo que has hecho tu, y que es lo que viene de afuera.
Si no lo haces puedes tener un buen lío. Y recuerda CASI TODO EN GIT tiene solución.

Evitar conflictos absurdos antes de que se den:

La guía de estilos para el código no es tonteria. Esos espacios vs. tabs.
Comillas simples, comillas dobles, mejor todos igual, en css ni te cuento.

PONERSE DE ACUERDO TE QUITARÁ DOLORES DE CABEZA

No tiene solución en git:
`git checkout`

No se puede deshacer, porque se pierde la referencia totalmente, si haces eso sin haber guardado un commit, perderás todos los cambios que hayas hecho.



## Buenas prácticas para escribir mejores commits:

### 1. Usa el verbo imperativo (`Add`, `Change`, `Fix`, `Remove`, …)

Estamos tentados a escribir “Added…”, “Fixed…” o “Removed…”
¡Pero cada commit es una instrucción para cambiar el estado del proyecto!

Fíjate cómo los añade Git (al hacer merge de una rama usa "Merge branch").

### 2. No uses punto final ni suspensivos en tus mensajes

El primer mensaje del commit es el título y no se puntúan.

`git commit -m "Add new search feature."` ❌

`git commit -m "Fix a problem with the topbar..."` ❌

`git commit -m "Change the default system color"` ✅

### 3. Usa como máximo 50 carácteres para tu mensaje de commit

Si tienes que explicar demasiadas cosas, seguramente es que has hecho demasiadas cosas en tu commit.

Haz que el mensaje sea claro, directo y que realmente refleje los cambios que lleva.

### 4. Usa el cuerpo del commit

Si el primer mensaje del commit es el título, los siguientes serían el cuerpo.

Ahí puedes usar la puntuación y además describir qué hace el commit:

`git commit -m "Add summary of commit" -m "This is a message to add more context."`

### 5. Usa commits semánticos

Cuando un proyecto crece, es necesario que existan ciertas reglas para que el historial sea legible o para poder hacer releases automáticas.

[scope]: mensaje del commit

### 6. Aprovecha los mensajes

❌ `"Remove CSS unused"`

✅ `"Remove unused button styles from landing page /cities"`

❌ `"Add new feature"`

✅ `"Add search functionality by city for registered users"`

❌ `"Fix bug"`

✅ `"Fix auth flow adding a redirection to home page"`

### 7. Considera usar utilidades para hacer commit

Usa husky para ejecutar scripts o comandos antes de realizar diferentes acciones sobre el repositorio, gracias a los hooks de git.

Y commitlint para asegurarte que tus commits siguen ciertas reglas.




**Fuentes**:

https://gitexplorer.com/

https://slides.com/elenam-lopez/no-liarla-parda-con-git-x-2#/

https://github.com/ElenaMLopez/taller_git

https://rogerdudler.github.io/git-guide/index.es.html

https://stackoverflow.com/

https://git-scm.com/

