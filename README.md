# git-useful-commands
Most useful commands for Git

## Diferentes estados de tu archivo
1. Working area: Pues como bien dice, el momento en el que estás trabajado. Escribiendo tus cosas, borrando...
2. Stagin Area: Oye esto ya me mola, creo que lo debería guardar...
3. Commit: ¡¡¡ Ala guardao !!!!

### Meter en Stagin Area

`git status`
Git status nos dice el estado en el que se encuentran nuestros archivos. Si están sin seguimiento, si tienen seguimiento pero se han cambiado o si están en Stagin ya.

### Meter en Stagin Area

`git add <archivo>`
Git add añade el archivo que le pasemos a stagin area, y que luego estará en el commit. 
 
`git add .`
El "." agrega todo a stagin.

### Hacer un commit

`git commit -m "Mensaje descriptivo del cambio"`
Con este comando hacemos un commit de los archivos que estén en stagin area.

Se hace una instantanea de los archivos en ese momento y se agrega a la cabecera (HEAD) quedando registrado y guardado como un punto en el tiempo.

### Listar los commits

`git log`
Nos mostrará un log o histórico de commits realizados en este repositorio.

Copiarlo en un archivo de texto o similar puede ser una gran idea si piensas viajar en el tiempo de tu histórico.

Para salir de ahí pulsa `q`.

### Viajar en el tiempo

`git checkout <codigo_sha>`
Nos lleva al estado del repositorio en ese momento. 

Para volver a donde estábamos tienes que coger el código SHA en el que te encontrabas.


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

`git branch -D <nombre-rama>`

## Cuando tienes un repo en remoto

`git pull origin <nombre_de_la_rama>`

Si hay conflicto resuelve y comitea.

`git push origin <nombre_de_la_rama>` 

En resumen:
Cuanto más acutalizada tengas la rama donde estás y tu repo, menos conflictos tendrás. ANTES DE HACER PUSH HAZ PULL.

### ¿Agregar repos remotos?

`git remote add <nombre_para_remoto> <url>`

Cuando hagas push, recuerda hacerlo a ambos (o tendrás un bonito caos...)

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




**Fuente**:
https://slides.com/elenam-lopez/no-liarla-parda-con-git-x-2#/
https://github.com/ElenaMLopez/taller_git

