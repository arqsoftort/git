#Laboratorio de Git

##Introducción
Hoy en día, los problemas como perder código no respaldado o mezclar versiones viejas y perder cambios, pueden ser solucionados fácilmente. Ni que hablar de los problemas a los que nos enfrentamos al desarrollar software en equipo, donde podemos pisar versiones de otra persona y muchos otros problemas.

Este laboratorio intenta introducir a los alumnos a la utilización de un VCS (Version Control System), enfocándose en Git ya que es actualmente el más usado por la comunidad. Además, el resto de los laboratorios del curso requieren conocimientos básicos sobre este tema.

##Sistemas de Control de Versiones
El control de versiones, como ya se estudió en otras materias, es un sistema que registra los cambios realizados sobre un archivo o conjunto de archivos a lo largo del tiempo. Su objetivo es poder mantener y administrar ese registro para poder consultar o incluso volver a las versiones anteriores de cada archivo. 

Existen sistemas de control de versiones centralizados y distribuidos. En el centralizado, existe un único repositorio que contiene todos los archivos y los clientes los descargan cuando quieren hacer un cambio. Por otro lado, en el distribuido, los clientes tienen una copia del repositorio entero, lo que permite tener varios respaldos y no depender de un único servidor. Además, en el distribuido se permite que dentro de un mismo proyecto, haya grupos de trabajo separados cuyos cambios en el repositorio no afecten a los de otros (branches). Para entender mejor la diferencia entre centralizado y distribuido, les recomendamos leer [acá](http://git-scm.com/book/es/Empezando-Acerca-del-control-de-versiones).

##Qué es Git?

###Manejo de archivos
El sistema de control de versiones distribuido más conocido hoy en día es Git. Nació en el 2005 para solucionar los problemas que el equipo de desarrollo de Linux estaba teniendo. Más info sobre la historia [acá](http://git-scm.com/book/es/Empezando-Una-breve-historia-de-Git).

La principal diferencia entre Git y cualquier otro VCS (Subversion y compañía incluidos) es cómo Git modela sus datos. Conceptualmente, la mayoría de los demás sistemas almacenan la información como una lista de cambios en los archivos. Estos sistemas (CVS, Subversion, Perforce, Bazaar, etc.) modelan la información que almacenan como un conjunto de archivos y las modificaciones hechas sobre cada uno de ellos a lo largo del tiempo, como muestra la siguiente figura.

![VCS viejos](http://git-scm.com/figures/18333fig0104-tn.png)

Git no modela ni almacena sus datos de este modo. En cambio, Git modela sus datos más como un conjunto de fotos de un mini sistema de archivos. Cada vez que confirmás un cambio, o guardás el estado de tu proyecto en Git, él básicamente hace una foto del aspecto de todos tus archivos en ese momento, y guarda una referencia a esa foto. Para ser eficiente, si los archivos no se han modificado, Git no almacena el archivo de nuevo, sino sólo un enlace al archivo anterior idéntico que ya tiene almacenado. Entonces Git modela sus datos más como en la figura siguiente.

![Git fotos](http://git-scm.com/figures/18333fig0105-tn.png)

Otra gran ventaja de Git, es que al tener una copia entera del repositorio en tu computadora, la mayoría de las operaciones son locales. Por lo tanto, todas son muy rápidas y se puede trabajar sin conexión, algo que con los sistemas centralizados era casi imposible.

###Estados de cambios
Git tiene tres estados principales en los que se pueden encontrar tus archivos: **committed**, **modified** y **staged**. Committed significa que los datos están almacenados de manera segura en tu base de datos local. Modified significa que modificaste el archivo pero todavía no lo "committeaste" a tu base de datos. Staged significa que marcaste un archivo modified en su versión actual para que vaya en tu próximo commit.

Esto nos lleva a las tres secciones principales de un proyecto de Git: el **Git directory**, el **working directory**, y la **staging area**.

![git areas](http://git-scm.com/figures/18333fig0106-tn.png)

El Git directory es donde Git almacena los metadatos y la base de datos de objetos para tu proyecto. Es la parte más importante de Git, y es lo que se copia cuando clonás un repositorio desde otra computadora.

El working directory es una copia de una versión del proyecto. Estos archivos se sacan de la base de datos comprimida en el Git directory, y se colocan en disco para que los puedas usar o modificar.

La staging area es un sencillo archivo, generalmente contenido en tu Git directory, que almacena información acerca de lo que va a ir en tu próximo commit. A veces se le denomina index, pero se está convirtiendo en estándar el referirse a ella como la staging area.

El flujo de trabajo básico en Git es algo así:

1. Modificás una serie de archivos en tu working directory.
2. Stageás los archivos, añadiendolos a tu staging area.
3. Committeás los cambios, lo que toma los archivos tal y como están en la staging area, y almacena esas fotos de manera permanente en tu Git directory.

Entonces:

- Si una versión concreta de un archivo está en el Git directory, se considera committeada. 
- Si ha sufrido cambios desde que se obtuvo del repositorio, pero ha sido añadida a la staging area, está stageada. 
- Si ha sufrido cambios desde que se obtuvo del repositorio, pero no se ha stageado, está modified.

##Instalando Git

Dependiendo del sistema operativo que uses, hay distintas formas de hacerlo. En [este link](http://git-scm.com/book/es/Empezando-Instalando-Git) hay información sobre cómo hacerlo para cada uno. Y en [este otro link](http://git-scm.com/book/es/Empezando-Configurando-Git-por-primera-vez) hay información sobre cómo configurarlo por primera vez.

##Usando Git

###Consola

Al principio, esta era la única manera de manejar Git y sigue siendo la más clara y menos propensa a problemas o acciones que no quedan claras. Para una guía básica de los comandos por consola para las operaciones en Git, les recomendamos estos dos tutoriales:

- https://www.atlassian.com/es/git/tutorial/git-basics
- http://git-scm.com/book/es/Fundamentos-de-Git

###GUI

También existe la posibilidad de usar aplicaciones que nos permiten ejecutar esas mismas operaciones manera más amigable. Sin embargo, a veces no queda muy claro cuáles son los comandos que la aplicación está ejecutando por detrás y eso puede generar alguna acción no deseada. Existe un gran número de aplicaciones para esto y en la página de Git están listadas la mayoría. Las oficiales de GitHub (para Windows y Mac), junto con SourceTree de Atlassian son las más recomendadas.

- http://git-scm.com/downloads/guis

##Branching

El manejo de branches es un aspecto muy interesante de Git y una de las grandes ventajas que lo diferencian de los demás VCS. Para conocer sobre este tema, les recomendamos leer la documentación oficial [acá](http://git-scm.com/book/es/Ramificaciones-en-Git).

##Hosting

Es recomendable que una de tus [remotes](http://git-scm.com/book/es/Fundamentos-de-Git-Trabajando-con-repositorios-remotos) esté en un servidor web al que se pueda acceder desde cualquier computadora, para no depender de una copia específica en algún servidor específico que puede romperse o simplemente apagarse.

Hoy en día existen varias empresas que se dedican a proveer este servicio. Entre las más conocidas están [GitHub](https://github.com/) y [BitBucket](https://bitbucket.org/). En GitHub, los repositorios privados son pagos, pero los proyectos Open Source pueden tener repositorios gratuitos e ilimitados. En BitBucket se pueden tener repositorios privados y gratuitos, pero el servicio no es tan bueno como el de GitHub.

GitHub además tiene muchísimo soporte por parte de ellos y de la comunidad. Es un excelente lugar para contribuir y cada vez más se está convirtiendo en parte esencial del CV de un desarrollador.

##Aprender más

Les recomendamos estos tutoriales interactivos que pasan por muchas de las operaciones del día a día con Git y otras no tan conocidas.

- https://try.github.io/levels/1/challenges/1
- http://pcottle.github.io/learnGitBranching/
