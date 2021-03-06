Acerca de npm, node package module, su web es https://npmjs.com.

Para instalar npm en windows es necesario instalar nodeJS, para eso vamos a la web de node. la web https://nodejs.org/es/.

En la web de nodejs vemos dos versiones una LTS y una Current, la LTS le da mas soporte a los feature que estan en esa version, es mas para entornos de desarrollo y produccion, luego la Current tiene las fuature version mas actuales.

Esto esta bien, pero mas ideal es instalar nvm, node version manager. Un gestor para gestionar versiones de nodeJS, lo podemos descargar desde su github. https://github.com/coreybutler/nvm-windows

Para ver las versiones de node
node -v
npm -v

Para ver si tenemos actualizaciones pendientes
npm install -g npm@latest

Para iniciar un proyecto:
Nos movemos con la terminal al proyecto que vamos a empezar a trabajar.

Lo primero iniciamos el proyecto en git
git init

Luego iniciamos nuestro archivo package.json
npm init, nos va a pedir varios datos que debemos rellenar para completar la configuracion

Lo datos que nos pedira
package name: (jsmpn)
version: (1.0.0)
description: Ponemos una descripcion del proyecto
entry point: .src/index.js
test command:
git repositorio: poner el enlace al repo
keywords: Palabras claves del proyecto separadas por coma
author: Alfredo Sánchez <alfred3ks@gmail.com>
license: MIT

y listo aceptamos.

Como podemos ver se ha creado un archivo package.json y podemos modificar las veces que sea necesario.

Ahora existe una forma mas rapida de crear este archivo package.json ya que lo modificaremos mas adelante

git init -y

Ahora tambien podemos establecer una configuracion estandar en npm que cuando creemos el .json ya aparezcan

Para establecer el correo:
npm set init.author.email "alfred3ks@gmail.com"

Para establecer el nombre:
npm set init.author.name "Alfredo Sánchez"

Para la licencia:
npm set init.license "MIT"

Esto es bastante interesante sobre todo cuando hacemos la instalacion rapida.



Ahora veremos como podemos instalar dependencias o paquetes:

// Como dependencia requerida del proyecto:
npm install (paquete)

npm install (paquete) --save
npm i (paquete) -S

npm install (paquete) --save-dev
npm i (paquete) -D

npm install (paquete) -g


// Explicacion:

- El --save le dice que esta dependencia es necesaria para vivir en produccion
- -S es el shorcode del anterior

- El --save-dev le dice que solo para desarrollo, tambienlo podemos hacer como a continuacion y es lo mismo
- -D el shorcode, le dice tambien que es una dependencia de desarrollo

- El -g le decimos que la instalacion del paquete es de manera global osea en nuestro pc, en el caso de nodemon

Al instalar un paquete se nos genera en nuestro proyecto la carpeta node_modules y un archivo package-lock.json

En la carpeta node_modules es donde se van a instalar todos los modulos que necesite nuestro proyecto

OJO importante esta carpeta node_module no debe ser enviada a ningun repositorio ni a produccion y debe ser ignorada con el archivo .gitignore el cual procedemos a crear

Para saber los paquetes instalados de manera global:
npm list -g --depth 0

- El --depth es para buscar en la profundidad de instalacion.

OJO tambien podemos instalar paquetes de manera opcional:
npm install eslint -o

OJO algunos paquetes cuando se instalan nos muestra una forma para que les ayudemos (financiacion) para que les aportemos y ayudemos ecnomicamica en el proyecto lo puedes ver con el comando:

npm fund

Este se ve al final cuando se instala el paquete.

// si queremos ver el la salida de un paquete lo podemos hacer hacer, osea simular su instalacion:

npm install (paquete) --dry-run

Existe otra forma de instalar paquetes, de manera forzada, desde el ultimo recurso del servidor de npm

npm install webpack -f

Ahora si queremos instalar todas las dependencias de nuevo aunque no tengamos la carpeta node_modules pero con el archivo package.json las podemos instalar

npm install

Ahora si queremos instalar una version particular de un paquete, por ejemplo para dar mantenimiento a un proyecto antiguo:

npm install json-server@0.15.0

la version que queremos la ponemos a partir del @


ACTUALIZAR dependencias o paquetes, muy importante en temas de seguridad

// para listar los paquetes del proyecto con su arbol de jerarquia
npm list

// Para poder ver que paquetes pueden llegar a estar desactualizados
npm outdate
npm outdate --dd

- El flag --dd para ver un output mas detallado

// Para actualizar los paquetes a su ultima version
npm update

// Para instalar de manera particular un paquete
npm install json-server@latest

DESINTALAR PAQUETES-----
Para eliminar un paquete en concreto
npm uninstall (paquete)

Para eliminar un paquete de node-modules pero no del package.json
npm unistall (paquete) --no-save

//RECOMENDACION
Un paquete para vscode que analiza el package.json y lo compara con node-modules y te avisa si algun paquete no esta instalados

la extension npm egamma

//PACKAGE LOCK Y LOS SIMBOLOS  ^ Y  ~

Respuesta a:
Package lock y el uso los símbolos ^ y ~
^ = Si mantenemos el caret dentro de la configuración de nuestro package estamos garantizando que cuando realicemos una actualización o tengamos un cambio que podamos realizar, vamos a hacer actualización de los cambios menores y de los parches o bug fixes.
Para quedarnos en una sola versión eliminamos el caret.

~ = Establece que vamos a recibir actualizaciones o cambios solamente de los cambios que son parches o bug fixes.

// para entender los package.jon ver la carpeta de react base que nos clonamos del repo de gndx Oscar Barajas
git clone https://github.com/gndx/react-base.git

Tambien podemos la imagen agregada donde se puede ver todo sobre las actualizaciones de las versiones.

Si tenemos ^ solo recibiremos actualizaciones minor
Si tenemos ~ solo recibiremos actualizaciones de tipo pach
Si le quitamos dejamos el paquete en la version y no se actualizara

// COMO CREAR SCRIPT DENTRO DE PACKAGE.json

Dentro del package.json podemos ver que tenemos un apartado que dice script, estos en npm son  comandos que podemos establecer y que podemos ejecutar desde la consola y nos dara una serie de salidas segun sea el caso

Para el caso de nodemon
"start": "nodemon index.js"

Y en la consola lo ejecutamos npm run start

Esto es muy interesante y seria bueno profundizar mas

// SOLUCION DE PROBLEMAS con paquetes de npm

Debemos activar la version de verbose, lo cual nos va a permitir ver que esta pasando

npm run dev --dd

//Para eliminar la cache de los paquetes
npm cache clean --force
npm cache verify

// Si tenemos algun modulo corrupto o incompleto que nos da problemos debemos eliminar la carpeta node-module y volverla a instalar, la eliminamos bien sea borrando directamente la carpeta o por medio de la terminal

rm -rf node-modules/

La volvemos a instalar
npm install

Tambien mas facil si instalamos un paquete global para borrar las carpetas que queramos en el caso de node_module

npm install -g rimraf

y luego podemos borrar asi:
rimraf node_modules

// Seguridad de los paquetes

Con el comando npm audit podemos ver los cambios que puede afectar a nuestro proyecto

npm install y instalamos todos los paquetes del proyecto
aqui ya nos dice las vulnerabilidades que tenemos, lo podemos ver en el proyecto de Oscar Barajas:
git clone https://github.com/gndx/react-base.git

Luego podemos hacer audit y lo veremos mas explicado
npm audit

Tambien si queremos la informacion en formato json los podemos hacer:

npm audit --json

Para actualizar los paquetes que poseen las vulnerabilidades:

npm update <nombre del paquete> --depth 2
npm update eslint-utils --depth 2

Pero si quiero reparar todo el proyecto y quitar todas las vulnerabilidades usare el comando:

npm audit fix

Tambien existe una web que puede monitorizar nuestro proyecto y ayudarnos en el tema de la vulnerabilidades:

https://snyk.io/

Como actualizar dependencias npm con npm-check-update:

Podemos utilizar una dependencia llamada npm-check-updates, se encargará de checkear nuestros paquetes y comprobar sus versiones vs su última versión. Para instalarlo:

npm install -g npm-check-updates

A partir de ese momento dispondremos de un comando global del mismo nombre (npm-check-updates), o mejor áun, abreviado como ncu, que nos permitirá hacer todo lo indicado.

ncu

Al ejecutarlo nos mostrará las versiones actuales de nuestros paquetes y, separadas con una flecha, las más recientes.

Si queremos que se actualicen todos entonces usaremos:

ncu -u

Video 12 Crear un paquete para npm

Crearemos un paquete de randon de mensajes, lo crearemos con mkdir random-messages

// Cuando creamos un paquete y para poderlo probar en nuestro pc osea que se instale de manera global y poderlo probar usaremos:

npm link

Si hacemos cambios en nuestro paquete cada vez tenemos que hacer npm link para que actualicen esos cambios

Existe otra forma de hacer la instalacion o la actualizacion del paquete dentro del pc, debemos dentro del proyecto buscar su Ruta 

pwd
/Users/alfsa/Desktop/curso-de-gestion-de-dependencias-y-paquetes-npm/random-messages

y Luego:

npm install -g /Users/alfsa/Desktop/name-random-messages

// Ahora para publicar paquetes a npm debemos crear un cuenta en npm,

una vez creada debemos loguearno a travez de la terminal:

npm adduser

nos pedira nuestro usuario y nuestra contraseña y un correo preferiblemente el que usamos para darnos de alta 

y listo ya estamos conectados y podemos publicar nuestro paquete.

Para publicar el paquete:

npm publish

// Para borrar un paquete subido a npm

npm unpublish --force

// nuestro paquete debe tener un minimo paraque sea considerado un buen paquete:

- debemos tener un buen readme.md
- conectarlo con un repositorio de github, para esto creamos el repo en github y conectamos con nuestro repo en local
- Luego debemos hacer npm init para que reconosca los cambios y nos coloque en el package .json la direccion del repo

-Antes de actualizar en npm debemos hacer un cambio a la version porque nuestro packete le hemos realizado cambios:


npm version major para versiones mayores
npm version patch para versiones sin grandes cambios(pequeños)
npm version minor para cambios menores

- y actualizarlo en npm con:

npm publish y listo







































