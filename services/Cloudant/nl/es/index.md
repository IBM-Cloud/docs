---

copyright:

  years: 2015, 2016

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}

# Iniciación a Cloudant
{: #getting-started-with-cloudant}
Última actualización: 12 de agosto de 2016
{: .last-updated}

{{site.data.keyword.cloudant}} es una base de datos de documentos como servicio (DBaaS) que almacena datos en JSON.
Para su creación, se tienen en cuenta la escalabilidad, la alta disponibilidad y la durabilidad.
Incluye una amplia gama de opciones de indexación, como map-reduce, Cloudant Query, indexación de texto completo e indexación geoespacial.
Las capacidades de réplica permiten mantener fácilmente los datos sincronizados entre los clústeres de bases de datos, los equipos de sobremesa y los dispositivos móviles.
{:shortdesc}

La consola {{site.data.keyword.cloudant}} se puede lanzar desde la página de lanzamiento del servicio en el panel de control de Bluemix. 

Para utilizar el servicio, siga estos pasos:
<ol>
<li>Cree una instancia de servicio utilizando el panel de control de Bluemix o la interfaz de línea de mandatos de CloudFoundry.
<p>Para crear una instancia utilizando el panel de control, siga estos pasos:
<ol>
<li>Inicie sesión en Bluemix.</li>
<li>En el panel de control, pulse el enlace <code>Trabajar con datos</code> en el panel Data &amp; Analytics. </li>
<li>Pulse el botón <code>Nuevo servicio</code>. </li>
<li>En la lista de servicios, pulse el botón {{site.data.keyword.cloudant}}.</li>
<li>En la página de información de {{site.data.keyword.cloudant}},
pulse el botón <code>Elegir {{site.data.keyword.cloudant}}</code>. </li>
<li>En la página de catálogo de {{site.data.keyword.cloudant}},
especifique los detalles del servicio que necesite.
Pulse el botón <code>Crear</code> cuando esté listo para continuar. </li>
<li>Una vez que se haya creado la instancia de Cloudant, se abrirá el panel de control para dicha instancia.
Pulse el enlace <code>Credenciales del servicio</code> para ver todos los detalles que necesita para acceder a la instancia. </li>
</ol>
</p>
<p>Para crear una instancia utilizando la interfaz de línea de mandatos de CloudFoundry, siga estos pasos:
<ol>
<li>Instale la herramienta CloudFoundry <code>cf</code> en el sistema.
Encontrará instrucciones sobre cómo hacerlo en la <a href="https://console.ng.bluemix.net/docs/cli/index.html">CLI de Bluemix y en la guía de herramientas de desarrollo</a>.</li>
<li>Cree una nueva instancia de servicio utilizando este mandato: <br/>
<pre><code>cf create-service</code></pre></li>
<li>Se mostrará una lista de los servicios disponibles.
Elija uno de los servicios e introduzca un nombre de instancia y un plan exclusivos para el servicio.
Se sugiere un nombre aleatorio para la instancia, pero puede cambiarlo por el nombre que prefiera. </li>
<li>Una vez que haya creado el servicio, podrá obtener una lista de todos los servicios que ha creado.<br/>
<pre><code>cf services</code></pre></li>
<li>Para poder utilizar un servicio en una aplicación, es preciso que enlace primero el servicio a la aplicación.
Puede hacerlo con este mandato: <br/>
<pre><code>cf bind-service</code></pre>
En la lista resultante, seleccione una de las aplicaciones y uno de los servicios.
El mandato <code>cf</code> indica el memento en que la acción de enlace es satisfactoria. </li>
</ol>
</p>
</li>
<li><p>Tras crear una instancia de servicio, se mostrarán datos JSON similares a los siguientes, que podrá ver en el panel de control de Bluemix:<br/>
<pre><code>{
  "cloudantNoSQLDB": {
    "name": "Cloudant-3s",
    "label": "cloudantNoSQLDB",
    "plan": "shared",
    "credentials": {
      "username": "someusername",
      "password": "secret",
      "host": "myhost-bluemix.cloudant.com",
      "port": 443,
      "url": "https://someusername:secret@myhost-bluemix.cloudant.com"
    }
  }
}</code></pre></p>
{: screen}
<p>Los datos también se añaden a la variable de entorno <code>VCAP_SERVICES</code> de cualquier aplicación Bluemix a la que está enlazado el servicio.</p>
<p>Las credenciales del servicio se almacenan en un objeto JSON que contiene los campos siguientes:
<ul>
<li><code>key</code>: El nombre del servicio (cloudantNoSQLDB)</li>
<li><code>name</code>: El nombre proporcionado por el usuario de la instancia de servicio</li>
<li><code>host</code>: El nombre de host del servidor</li>
<li><code>port</code>: El número de puerto en el que se ejecuta el servicio, normalmente 443</li>
<li><code>username</code>: El nombre de usuario de la autenticación</li>
<li><code>password</code>: La contraseña de la autenticación</li>
<li><code>url</code>: El URL de la instancia de servicio</li>
</ul></li>
<li><p>En las aplicaciones Bluemix, lea las credenciales desde la variable de entorno <code>VCAP_SERVICES</code>.</p>
<p>En aplicaciones que se ejecutan fuera de Bluemix o en una región geográfica distinta en Bluemix, puede recuperar las credenciales desde el panel de control de Bluemix y añadirlas a la configuración de la aplicación.</p>
</li>
<li>Para acceder a la base de datos, el mecanismo básico consiste en enviar solicitudes al host y al puerto proporcionados mediante HTTPS, utilizando el nombre de usuario y la contraseña para autenticarse. Las solicitudes pueden enviarse utilizando distintos lenguajes y plataformas de aplicaciones, tales como:
<ul>
<li><a href="https://github.com/cloudant/sync-android">Android</a></li>
<li><a href="https://github.com/cloudant/CDTDatastore">Apple iOS</a></li>
<li><a href="https://github.com/cloudant/java-cloudant">Java</a></li>
<li><a href="https://github.com/cloudant/objective-cloudant">Objective C y Swift</a></li>
<li><a href="https://github.com/cloudant/python-cloudant">Python</a></li>
</ul>
entre muchas otras.
Para obtener más información, consulte la <a href="https://cloudant.com/for-developers/">página de inicio de Cloudant Developer</a> y las <a href="http://docs.cloudant.com/libraries.html">bibliotecas de cliente</a>.
</li>
<li>Cuando la aplicación ya esté lista, puede desplegarla en el entorno Bluemix para verificarla.
Para desplegar una aplicación, utilice el siguiente mandato:<br/>
<pre><code>cf push</code></pre></li>
<li>Para anular el enlace de un servicio, utilice el siguiente mandato:<br/>
<pre><code>cf unbind-service</code></pre></li>
<li>Para eliminar la instancia de un servicio, utilice el siguiente mandato: <br/>
<pre><code>cf delete-service</code></pre></li>
</ol>

Hay disponible más información sobre la autenticación en la base de datos y la realización de solicitudes en la [referencia de la API](https://docs.cloudant.com/api.html).

# Enlaces relacionados
{: #rellinks}

## Guías de aprendizaje y ejemplos
{: #samples}

* [Bibliotecas de cliente de Cloudant](https://docs.cloudant.com/libraries.html)
* [Utilización de Cloudant con Liberty en Bluemix](https://developer.ibm.com/bluemix/2014/07/08/cloudant_on_bluemix/)
* [Guías de Cloudant](https://docs.cloudant.com/guides.html)

## Referencia de API
{: #api}

* [Referencia de la API de Cloudant](https://docs.cloudant.com/api.html)

## Enlaces relacionados
{: #general}

* [Sitio web y panel de control de Cloudant](https://cloudant.com/)
* [Blog de Cloudant](https://cloudant.com/blog)
