---

copyright:
  years: 2016, 2017
lastupdated: "2017-04-11"

---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}


# Modo fuera de línea para node.js
{: #offline_mode}

Cuando se envía por push una aplicación node.js a {{site.data.keyword.Bluemix}}, el paquete de compilación de SDK for Node.js
descargará normalmente artefactos desde recursos externos como módulos de nodos desde NPM.  En algunas situaciones
como con [Bluemix dedicado](/docs/dedicated/index.html#dedicated) y
[Bluemix local](/docs/local/index.html#local), es posible que desee no basarse en,
o tener más control explícito sobre, el acceso a sitios externos a Bluemix.  
{: shortdesc}

A continuación se muestran los sitios externos a los que puede acceder el paquete de compilación de node.js.  En los entornos de Bluemix [Bluemix dedicado](/docs/dedicated/index.html#dedicated) y
[Bluemix local](/docs/local/index.html#local), es posible que estos sitios necesiten incluirse en una *lista blanca*.

* http://nodejs.org/ se puede utilizar para comprobar las versiones del motor del nodo disponibles.
* https://s3pository.heroku.com se utiliza para recuperar versiones del motor del nodo no incluidas en el paquete de compilación.
*  https://www.npmjs.com/package/npm y https://semver.herokuapp.com se utilizan para recuperar versiones de npm no incluidas en el paquete de compilación.
* https://iojs.org se utiliza para recuperar versiones anteriores de nodos que no están contenidas en el paquete de compilación o que no están disponibles en https://semver.herokuapp.com.
* https://registry.npmjs.org se utiliza para recuperar módulos de nodos como por ejemplo express.

Para minimizar el conjunto de sitios incluidos en la lista blanca, configure las aplicaciones de nodos para utilizar una versión del motor de nodos que esté incluida en el paquete de compilación SDK for Node.js.  Consulte [Últimas actualizaciones](./updates.html) para obtener el conjunto de versiones del motor de nodos incluido en el paquete de compilación.  Si se hace esto, solo será necesario el sitio https://registry.npmjs.org para descargar módulos de nodos.

Tenga en cuenta que cuando se instalen las versiones nuevas del paquete de compilación SDK for Node.js, el conjunto de versiones del motor de nodos disponible con frecuencia
se mueve a nuevas versiones.  Esto puede que necesite que vuelva a configurar la app del nodo para especificar una versión del motor de nodos más reciente.


## Aplicaciones fuera de línea
{: #offline_applications}

Para eliminar la necesidad de acceder a https://registry.npmjs.org, puede incluir todos los módulos de nodos que necesita su aplicación dentro de la aplicación.  Para ello, ejecute **npm install** para todos los módulos que necesite su aplicación e incluya el directorio *node_modules* resultante con la aplicación enviada por push.

Tenga en cuenta que sus dependencias pueden tener dependencias y que ellas pueden tener dependencias, y así sucesivamente, pero package.json
solo contiene las dependencias de nivel superior. Si una de las dependencias utiliza un rango del package.json y se lanza una nueva versión del mismo, los módulos del directorio node_modules pueden quedarse obsoletos. *Shrinkwrap* le ayuda a bloquear todas las versiones de dependencias para que esto no ocurra.  Para utilizar shrinkwrap, empiece con un directorio node_modules vacío o limpio y, a continuación, en el directorio raíz del proyecto, ejecute:
0. npm install
1. npm dedupe
2. npm shrinkwrap

Esto puede cambiar el *package.json* y añadir *npm-shrinkwrap.json* en el directorio raíz.
Siempre que realice un cambio en las dependencias del archivo *package.json*, repita los pasos *dedupe* y *shringwrap*.

## Cómo trabajar con un proxy
{: #working_with_proxy}

En algunos entornos como por ejemplo [Bluemix dedicado](/docs/dedicated/index.html#dedicated) y
[Bluemix local](/docs/local/index.html#local), se puede configurar un proxy. Consulte [Cómo trabajar con un proxy](/docs/manageapps/workingWithProxy.html) para obtener más detalles.
