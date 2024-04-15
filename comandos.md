# COMANDOS TERMINAL

`cd` => me lleva al directorio por defecto "/Users/mac"
`/` => me lleva al directorio principal, afuera de todo "/"
`/Users` => me lleva directamente a esa carpeta, por ser el primer eslabon de la cadena
`cd .` => sigo en el directorio actual
`cd ..` => me lleva al directorio anterior
`pwd` => me muestra la ruta en la que me encuentro
`ls` => me muestra todas las carpetas y archivos que tengo en el directorio actual
`ls -l` => me muestra una lista y detalles de todos los archivos (menos los ocultos)
`ls -al` => me muestra una lista y detalles de todos los archivos (incluso los ocultos)
`ls -a` => me muestra los archivos (incluso los ocultos), pero no en una lista

`clear` => para limpiar la consola
`cmd+l` => tambien limpia la consola
`mkdir`+`nombre de la carpeta` => para crear una carpeta
`rm -r`+`nombre de la carpeta` => para eliminar una carpeta
`touch`+`nombre del archivo con la extensión` => para crear un archivo
`rm`+`nombre del archivo con la extensión` => para borrar un archivo
`cat`+`nombre del archivo con la extensión` => para ver el contenido del archivo
`history` => para ver la historia de comandos escrita hasta el momento
`!`+`número de comando en history` => para ejecutar nuevamente ese comando

`git init` => para crear un repositorio en git
`code` => para abrir Visual Studio Code
`code .` => para abrir Visual Studio Code con un folder en el directorio actual

## Para configurar VSC de tal manera que el comando `code` funcione siempre debemos seguir estos pasos:

1. Ubicar la ruta donde se encuentra el archivo `.zshrc`
- en el portatil dió esta ruta: `/Users/Mac/.zshrc`
- en el mac dió esta ruta: `/Users/imac/.zshrc`
2. Abrir VSC y entrar a `File/Open...`, navegar por la ruta del punto 1 para encontrar el archivo, usar `cmd+shift+.` para que se muestren los archivos ocultos, y entrar al archivo `.zshrc` desde VSC
3. Agregar al final del archivo el siguiente comando con la ruta dónde se encuentra la aplicación VSC en mi computador, hasta la carpeta bin:
`export PATH="$PATH:/Applications/Visual Studio Code.app/Contents/Resources/app/bin"`
4. Guardar y cerrar VSC

`git config` => para conocer todas las configuraciones que tiene git
`git config --list` => para entrar a las propiedades de usuario y correo
`q` => para salir de la pantalla intermedia que tiene END
`ctrl+c`, para salir del entorno "bquote>"
`git config --list --show-origin` => para ver donde estan las configuraciones guardadas
`git config --global user.name`+`"Luis Cantor"` => para cambiar el nombre
`git config --global user.email`+`"luiskentor@gmail.com"` => para cambiar el correo

`git status` => para ver el estado de los commits
`rm -rf .git` => para eliminar el repositorio de una carpeta, estando en la carpeta
`git add`+`nombre del archivo con la extensión` => para trackear un archivo, es decir, agregarlo al "Staging"
`git add .` => para trackear todos los archivos de la carpeta
`git rm --cached`+`nombre del archivo con la extensión` => para destrackear los archivos, es decir, quitarles el "Add", por si tuvimos un error, o sacarlos del "Staging"
`git commit -m`+`Mensaje que identifique los cambios que se estan subiendo al repositorio` => para actualizar los cambios efectuados en el repositorio
`git commit -am`+`Mensaje que identifique los cambios que se estan subiendo al repositorio` => automaticamente hace el git add y el git commit de los cambios, pero solo funsiona con archivos a los que yo le habia hecho `git add` previamente, si es un archivo completamente nuevo esto no va a funcionar
`git log`+`nombre del archivo con la extensión` => para ver los commits realizados, aqui se muestra el ID de cada commit y sus detalles
`git log --stat` => para ver los cambios específicos que se hicieron en cuales archivos a partir del commit
`git show`+`nombre del archivo con la extensión` => para ver la versión antes y después de cada commit del archivo
`git diff`+`ID del commit #1`+`ID del commit #2` => para comparar las versiones entre dos commits específicos, es mejor colocar primero el ID mas reciente y después el más antiguo
`git diff` => me permite ver los cambios que tengo en stagin (memoria ram) vs los cambios que tengo en el disco duro
`git checkout`+`ID del commit del archivo`+`nombre del archivo con la extensión` => para volver a la versión de ID del commit indicado, es decir, cambia el archivo real y lo devuelve al status de ese momento. Este cambio queda en el stage, si hago commit, me devuelve todo a la versión que quedo en el stage, pero si en vez de eso, hago otro checkout así:
`git checkout`+`rama dónde estaba la ultima versión`+`nombre del archivo con la extensión` => me regresa a la ultima versión antes de la reversión del primer checkout, o sea, es devolver la reversión. Esto queda en stage, si hago cambios manuales sobre el archivo, tendría que adicionarlos al staging y despues hacer commit de todo.

`git reset`+`ID del commit al que queremos regresar`+`--hard` => para regresar todo al estado anterior, es decir, devuelve los cambios tanto en el log de commits, asi como en el archivo real, se pierden todos los cambios que se habian hecho, es muy peligroso, pues es una manera agresiva de volver al pasado 
`git reset`+`ID del commit al que queremos regresar`+`--soft` => volvemos a la versión anterior, pero lo que tengamos en staging sigue en staging

PASOS LOGICOS
1. ![Crear repositorio local](./Image/Imagen%201.png)
Cuando tenemos una carpeta con archivos iniciales, y damos `git init` creamos dos espacios
- Preparación o Staging
- Repositorio Local
La magia de Git es que al hacer esto, en todos los computadores de las personas que desarrollan, hay una copia exacta de toda la historia del proyecto, entonces nunca jamas se va a perder algo

2. ![Pasar a preparación](./Image/Imagen%202.png)
Cuando queremos agregar una carpeta de nuestro directorio al repositorio local, lo primero que hacemos es ponerlo en un área de preparación o staging con `git add`, esto le permite a git hacer un tracking, o un rastreo o seguimiento de los cambios que sufran los archivos en nuestra carpeta. Si un archivo "Tracked" no se le hace nada, eventualmente va a pasar el garbage collector y lo va a borrar.

3. ![Pasar los cambios](./Image/Imagen%203.png)
Cuando queremos enviar la versión final y definitiva a nuestro repositorio, usamos `git commit` para enviar todo que esté en staging a nuestro repositorio local.

4. ![Traer del repositorio remoto hacia repositorio local](./Image/Imagen%204.png)
Pero que pasa cuando tu tienes un equipo de trabajo con multiples desarrolladores?, necesitas un servidor o repositorio remoto (GITHUB), que es un lugar dónde tienes el mismo repositorio en el que tu estas trabajando, pero todo el mundo le manda datos para alla, es decir, trabajan en local y cuando terminan actualizan los cambios en el repositorio remoto para que el resto del equipo los pueda ver.

Para traernos datos de un repositorio remoto ` git clone url`, y lo que hacemos es que con la dirección de nuestro repositorio remoto, nos traemos los archivos a dos lugares, nos traemos una copia de la rama master a nuestro directorio de trabajo y crea la base de datos de todos los cambios históricos en el repositorio local, y deja Staging quieto y listo.

5. ![Actualizar hacia repositorio remoto](./Image/Imagen%205.png)
Entonces sigo trabajando en mi repositorio local con `git add` y `git commit` y cuando estoy listo para que la última versión de esos commit "el HEAD" de la rama "Master", se envíe al repositorio remoto dónde todo el mundo trabaja hago `git push`, y si hay conflictos aprendo a resolverlos. 

6. ![Actualizar hacia el repositorio local en dos pasos](./Image/Imagen%206.png)
Que pasa cuando ya estoy conectado al repositorio remoto, ya lo cloné, pero quiero traer una actualización porque alguien más cambió algo, hacemos un `git fetch` y esto me lo trae al repositorio local, pero no me lo copia en mis archivos, para que me lo copie en mis archivos tengo que fusionar la última versión que está en el repositorio local con mi versión actual, y eslo lo hago con `git merge`.

7. ![Actualizar hacia el repositorio local en un solo paso](./Image/Imagen%207.png)
Pero para que tengo hacer fetch y merge al mismo tiempo, si en general lo que yo quiero es que me traiga al repositorio y al directorio, tal cual como lo hice cuando cloné el repositorio remoto por primera vez, el comando que fusiona los dos conceptos es `git pull`.

8. ![Fusionar la rama principal como rama secundaria - HEAD](./Image/Imagen%208.png)
"Master" es nuestra rama principal, en esa rama nosotros tenemos toda nuestra historia de commits, cada vez que nosotros hemos hecho un cambio a esos archivos, podemos verlo en esos commits. El commit mas reciente es el que nosotros llamamos la cabecera "HEAD", pero que pasa si creamos una nueva rama llamada "Cabecera", cuando uno crea una rama, lo que hace es crear una copia del último commit en otro lado, y todos los cambios que hagamos en esta rama, no los va a ver la rama "Master", hasta que lo volvamos a fusionar las dos ramas, en un proceso que se llama "merge".

`git show` => me muestra cual fue el último cambio que hice y la rama donde lo hice, es decir el HEAD
`git branch`+`nombre nueva rama` => me cambia a una nueva rama
`git show` => me muestra en ahora como último commit un "HEAD" que le apunta a la rama "master" y tambien a la rama "cabecera", es decir, el último commit ahora esta pegado a dos ramas distintas
`git status` => veo que sigo en la rama master
`git checkout`+`nombre de la rama` => para cambiarme a otra rama, en este caso a la rama "cabecera"
Hago cambios en el archivo
`git add blogpost.html` => paso a staging
`git commit -m "Estructura inicial de la cabecera"` => hago commit
`git show` => me muestra que el cambio esta en la cabecera, y cual fue el cambio que se hizo
`git log` => me muestra el penultimo commit en la rama master, y el ultimo commit en la rama cabecera, dónde ahora se encuentra el "HEAD"
`git checkout master` => al cambiarme a la rama master, me muestra el archivo sin los cambios, osea me devuelve a la versión original
`git checkout cabecera` => y al cambiarme de nuevo a la rama cabecera, vuelve y me muestra el archivo con los cambios. Esta es la magia de git, porque podemos tener múltiples archivos cambiando
`HEAD` al final del día es un indicador de cual versión de commit estoy viendo de los últimos archivos, los archivos se muestran dependiendo de dónde esta el HEAD. Si hago cambios en los archivos, y me cambio de rama sin haber hecho commit, puedo perder los cambios que haya hecho en los archivos.

Para hacer un merge tengo que cambiar en dónde estoy, el merge siempre va a ocurrir en la rama donde estoy que es de donde me voy a pegar, si estando en "cabecera" hago un merge con "master", lo que hago es mandar los archivos principales hacia la rama de desarrollo, y esta se volvería la rama principal, pero eso no es lo que yo quiero, lo que quiero es traerme a master lo que hice en cabecera, llevar a la rama principal, los cambios hechos en la rama de desarrollo, entonces tengo que hacer un checkout de master, y traerme el HEAD a master, y ahí invoco el comando "merge" de cabecera, y eso lo que va a hacer es crear un commit nuevo dentro de master, que me va a traer el último commit de master y el último commit de cabecera y los va a fusionar.

Si llega a haber un conflicto que por ejemplo dos líneas hayan sido afectadas por la misma persona, me va a disparar un conflicto, y alguien lo tiene que arreglar, y no me va a permitir hacer el merge. Pero si no hay conflicto, la fusión sería el final de la rama cabecera y la continuación de la rama master.

`git checkout master` => después de hacer cambios en los archivos, en las dos ramas, y hacer commit en ellas, cambio a la rama master, que es mi rama principal
`git branch` => me ayuda a saber las ramas qu tengo y en que rama estoy
`git merge cabecera`+`mensaje` => para fusionar las ramas, recuerda que como esto es un commit, se debe colocar siempre un mensaje, de lo contrario me lleva a la pantalla intermedia, y para forzar el commit es `esc+shift+zz`
`git log` => vemos que me trae los ultimos cambios hechos en la rama master, y tambien me trae los ultimos cambios hechos en la rama master, entonces esta el último commit de la rama cabecera, tambien esta el último commit de la rama master, y un commit más reciente que sería la fusión entre los dos

Si después hago un cambio más estando en la rama "master", sencillamente hago un commit normal desde la rama master.

## Para configurar tus llaves públicas y privadas SSH en local
Las llaves SSH no son por repositorio o por proyecto, sino por persona.
Para crear las llaves correctamente, lo primero que debo hacer es verificar el correo que tengo en Github como usuario, y debo homologar en mi computadora este mismo correo.
`git config -l` para verificar el usuario y correo que tiene mi computadora, desde la terminal.
`git config --global user.email`+`"luiskentor@gmail.com"` => si el correo esta diferente lo cambio de esta manera

Ahora si podemos crear la llave SSH:
`pwd` => verifica que estas el home de tu equipo
`cd` => si no estas en el home, te sales para allá así
`ssh-keygen -t rsa -b 4096 -C "luiskentor@gmail.com"` => para empezar a generar la llave pública y privada
`enter` => al preguntarnos si estamos de acuerdo en guardar las llaves en la carpeta que propone el sistema
`enter`(2 veces) => al pedirme passphrase o passwword con espacios, que es una contraseña adicional de texto que le pondriamos a nuestras llavés pública y privada, es buena práctica pero para efectos del curso no lo vamos a hacer.

`cd` => vamos al home en la terminal
`.ssh` => en la terminal buscamos el lugar dónde fueron creadas nuestras llaves
`ls -al` => veo los archivos ocultos, y encuentro mi archivo de llave pública
`cat`+`nombre archivo llave pública` => y puedo ver mi llave pública desde la terminal, la copio para llevarla a GitHub

`cmd+shift+.` => vamos al directorio local en el finder, nos ubicamos en el home, y visualizamos los archivos ocultos, entrando a la carpeta `.ssh`, donde encontraremos los archivos reales de nuestras llaves
`clic derecho`+`abrir con VSC` => abro el archivo de la llave pública y la copio para llevarla a Github

`cd` => vamos al home de la terminal
`eval "$(ssh-agent -s)"` => par evaluar si el ssh-agent esta corriendo, y lo confirma arrojando un pid 3265 (process id)
`cd+.ssh` => vamos a la carpeta donde estan mis archivos de llaves
`ls -al` => y verificamos que se encuentre el archivo `config`, si no está hay que crearlo, usualmente está, para computadores después de macOS Sierra
`vim config` => para inciar la creación del archivo config, y me lleva a una pantalla intermedia
`Host *`+`Enter`+`Tab` => y me pasa a la segunda línea, donde escribo...
`AddKeysToAgent yes`+`Enter`+`Tab` => y me pasa a la tercera línea, donde escribo...
`UseKeychain yes`+`Enter`+`Tab` => y me pasa a la cuarta línea, donde escribo...
`IdentityFile ~/.ssh/id_rsa`+`Enter`
`ESC+shift+zz` => para guardarlo y sale de la pantalla intermedia
`ls -al` => y aparece el archivo `config`
`cat config` => para verificar lo que yo escribi

`cd` => para volver al home
`ssh-add -K ~/.ssh/id_rsa` => para agregar la llave privada, el archivo que no tiene extensión ".pub", y listo, queda la identidad añadida!

## Vamos a crear nuestro repositorio en Github
1. Entramos a nuestra cuenta en la página de Github
2. Creamos un nuevo repositorio
3. Le damos un nombre a nuestro nuevo repositorio `hyperblogV2`
4. Le damos una descripción `Un blog increible para el curso de Git y Github de Platzi`
5. Le definimos que sea público, para que todo el mundo lo pueda ver
6. Le añadimos un archivo de README, que es un archivo que se va a ver en el instante que una persona entre al repositorio en Github, es una muy buena práctica, es básicamente crear en la raiz de tu proyecto un archivo que se llama `README.md`, que es un archivo de texto que te permite explicar a las personas que abren tu repositorio, ¿qué es el repositorio?
7. Añadimos un archivo `.gitignore`
8. Añadimos una licencia de `MIT`, hay muchas licencias a través de las cuales podemos publicar nuestro código, licencias de código abierto, de código semiabierto, cerrado, etc.
9. Y creamos el repositorio
10. Una vez adentro del repositorio de Github, damos clic en el `boton verde Code`+`SSH`, y copiamos la url para conectar las llaves de nuestro repositorio local `git@github.com:creacionfinanciera/curso-profesional-git-github.git`

- Nota: Es importante destacar que cada usuario o cada computadora, debe tener una llave única, si tienes tres laptops, tienes que tener 3 llaves conectadas con tu repositorio de github, de lo contrario no va a funcionar, no es buena idea compartir estas llaves. Create una llave pública y una llave privada por cada computadora que uses.

## Vamos a conectar nuestras llaves con nuestro repositorio de Github
1. Entramos al archivo donde esta la llave pública y la copiamos, podemos hacerlo desde la terminal, `cat id_rsa.pub` desde el home, para ver el contenido y copiarlo
2. Vamos a nuestra cuenta en Github, `perfil/settings/SSH and GPG keys`
3. Visualizamos las llaves existentes, y creamos la nueva llave que queremos, boton verde `New SSH key`
4. Le damos nombre al computador que hace referencia las llave que estamos creando, `Estación de trabajo MacBook Air KENTOR`
5. Pegamos la llave pública que habiamos copiado del archivo local
6. Y le damos agregar a la llave, y queda agregada al repositorio remoto de Github
7. `git branch -M main` => 'git branch' nos ayuda a crear una nueva rama dentro de nuestro repositorio local y '-M' nos ayuda a mover todo el historial que tengamos en master (en caso de que lo haya), a la nueva rama que estamos creando que en este caso se llama "main"
8. `git remote add origin git@github.com:creacionfinanciera/curso-profesional-git-github.git` => ahora vamos a decirle a git que vamos a agregarle un origen remoto de nuestros archivos
9. `git remote` => para confirmar que existe ahora algo que se llama 'origin'
10. `git remote -v` => para verificar  de forma verbal

Nos muestra que tenemos un origin para hacer fetch (traernos cosas) y un origin para hacer un push (enviar cosas)
'origin	git@github.com:creacionfinanciera/curso-profesional-git-github.git (fetch)'
'origin	git@github.com:creacionfinanciera/curso-profesional-git-github.git (push)'

Y con esto ya estamos listos!

## Vamos a enviar de nuestro repositorio local a nuestro repositorio remoto los cambios

1. `git push origin main` => para enviar nuestros cambios del repositorio local al repositorio remoto, con esto guarda las credenciales y empieza a hacer el push. Para este ejemplo nos sale un error: "Las actualizaciones fueron rechazadas porque el repositorio remoto contiene trabajo que no tienes localmente", y esto es porque creamos directamente en GitHub el archivo README y ese archivo no está en el repositorio local, lo primero que hay que hacer es integrar los cambios en Github al repositorio local, para después poder hacer un push de todo desde el repositorio local hacia el repositorio remoto.
2. `git pull origin main` => para traernos los cambios que hay en el repositorio remoto hacia el repositorio local, en este caso me confirma que estoy conectado a la nueva rama 'origin/main', pero me saca un error fatal en el cual me dice "Necesita especificar cómo reconciliar las ramas divergentes", a través de tres opciones:
- git config pull.rebase false
- git config pull.rebase true
- git config pull.ff only
- Se puede reemplazar "git config" con "git config --global" para aplicar
ayuda: la preferencia en todos los repositorios

3. `git config --global pull.rebase false` => para fusionar entonces las ramas divergentes, y ahora me saca este error: "me rehuso a fusionar historias no relacionadas", eso significa que que la historia de commits del repositorio local no tiene nada que ver con la historia de commits del repositorio remoto, pero nosotros podemos forzar a que esto ocurra
4. `git pull origin main --allow-unrelated-histories` => para forzar a que si me permita hacer el merge con rama main del repositorio local, me saca a la pantalla intermedia y allá le doy `ESC+shift+zz`, y queda hecho el merge
5. `ls -al` => para verificar que me haya traido los cambios del repositorio remoto hacia el respositorio local, en este caso vemos qye trajo el achivo "README.md"
6. `git status`, para verificar que no haya nada que hacer commit en el repositorio local, si hay cambios pendientes enviarlos al repositorio local
7. `git push origin main` => ahora si para enviar los cambios al repositorio remoto

## Si hacemos cambios en nuestro repositorio remoto y queremos llevar los cambios en nuestro repositorio local
1. Vamos al repositorio en Github, entramos al archivo blogpost.html
2. `edit this file` => para activar la funcionalidad de edición en el archivo
3. Hago los cambios en el código en el mismo github
4. `Preview` => para visualizar previamente como quedan los cambios
5. `Commit changes` => para hacer el commit desde github, coloco el mensaje, una descripción más amplia, selecciono el usuario que hizo el cambio, y que quiero hacer directamente el commit a la rama main
6. Visualizo los cambios dentro de Github en el archivo
7. `git pull origin main` => para llevar los cambios al repositorio local
8. Si le damos clic a `commits`, podemos ver todos los cambios realizados hasta el momento

## Si hacemos cambios en nuestro repositorio local y queremos llevar los cambios a nuestro repositorio remoto
1. Hacemos los cambios en nuestros archivos, en nuestra computadora
2. `git pull origin main` => Lo primero que hay que hacer antes de hacer un commit en nuestro repositorio local, es traernos del repositorio remoto la última versión




















