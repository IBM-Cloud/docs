---

 

copyright:

  years: 2015 2016

 

---

{:shortdesc: .shortdesc} 
{:new_window: target="_blank"}
{:codeblock: .codeblock}
{:screen: .screen}

#Alojamiento de apps en {{site.data.keyword.Bluemix_notm}}

*Última actualización: 9 de mayo de 2016*

<!--The whole topic is staging only -->

Con {{site.data.keyword.Bluemix}},
puede crear apps, así como alojar sus apps existentes. Puede migrar sus apps a {{site.data.keyword.Bluemix_notm}} siempre que estén preparadas para la nube. {{site.data.keyword.Bluemix_notm}} proporciona distintos modos para ejecutar las apps, como por ejemplo Cloud Foundry, IBM Containers y Virtual Machines.

##Haciendo que sus apps estén listas para la nube
{: #cloud-readyapps}

Una app lista para la nube sigue los principios de la plataforma
de nube en su diseño y construcción. Una app lista para la nube puede utilizar
las prestaciones proporcionadas por la plataforma de nube.

Si su app cumple todos los principios siguientes, será una app
lista para la nube y se puede migrar a {{site.data.keyword.Bluemix_notm}}. Si su app infringe algún principio, por lo general podrá modificarla para
que lo cumpla.

* No codifique su app directamente en una topología específica.

  En un
entorno que no sea de nube, la app podría utilizar una topología de despliegue
concreta. No obstante, la topología de app podría cambiar en apps de nube,
porque las apps y servicios listos para la nube permite cambios de escalabilidad
inmediata. Los cambios de escalabilidad incluyen escalado dinámico y cambio manual del tamaño del
número de instancias de una app.

  Construya su app de forma que sea lo más
genérica e independiente posible de estado, para evitar que se vea afectada por cambios
de escalabilidad.

* No presuponga que el sistema de archivos local es permanente.

  Como una instancia de
app en la nube se puede mover, suprimir o duplicar en cualquier momento,
no se base en archivos que se graben en el sistema de archivos. Si una app
utiliza el sistema de archivos local como memoria caché de
información usada con frecuencia incluyendo los registros de app, la
información se pierde cuando se cierra la instancia y se reinicia en una ubicación
distinta o en otra MV.

  En lugar del sistema de archivos local, puede almacenar
información en un servicio, como una base de datos SQL o NoSQL. En un entorno de nube dinámico, también es fundamental tener sus registros
disponibles en un servicio que sobreviva a la instancia de la app
desde la que se generan los registros.

* No almacene el estado de sesión en su app.

  El estado de
su sistema lo definen sus bases de datos y almacenamientos compartidos,
y no cada instancia individual de app en ejecución. El uso de
estados de cualquier tipo limita la escalabilidad de su app. Intente
minimizar el impacto del estado de sesión almacenándolo en una ubicación
centralizada en el servidor.

  Si no puede eliminar el estado de sesión
por completo, colóquelo en un almacén de alta disponibilidad externo a
su servidor de apps. Los almacenes pueden ser IBM WebSphere Extreme Scale, Redis o
Memcached, o bien una base de datos externa.

* No utilice dependencia de infraestructura específica.

  Este es un principio general que tiene varias
manifestaciones. Por ejemplo, no presuponga que los servicios que utiliza su
app están en nombres de host o direcciones IP concretas. Como los
servicios podrían cambiar de lugar o volverse a generar en su entorno de nube,
los nombres de host y direcciones IP también podrían cambiar.

  La
extracción de las dependencias específicas del entorno a un conjunto de archivos
de propiedades mejora la situación, pero sigue sin ser adecuado. Lo recomendable es utilizar un registro de servicio externo para resolver
puntos finales de servicio, o delegar la función de direccionamiento completa
en un bus de servicio o un equilibrador de carga con un nombre virtual.

* No utilice las API de infraestructura en su app.

  Si se basa
en una API de infraestructura específica en su app, al cambiar
la infraestructura podría haber problemas, ya que la API de la infraestructura
puede hacer referencia a distintas capas en su pila de software.

  En su lugar,
puede basarse en código abierto existente o productos comerciales, y dejar
las soluciones PaaS en la capa PaaS para mantenerlas fuera de su código de
app.

* No utilice protocolos complejos.

  No utilice protocolos complejos que
necesiten de configuración adicional para su capacidad de
resistencia.

  Las aplicaciones basadas en protocolos estándar son
más resistentes con los elementos de configuración delegados a la
plataforma. Los protocolos estándar principales son HTTP, SSL,
base de datos estándar, consultas y conexiones de servicio web.

* No se base en características específicas del sistema operativo.

  Si ya
ha utilizado características específicas del sistema operativo, puede
solucionarlo mediante el uso de bibliotecas de compatibilidad, como
Cygwin y Mono. Cygwin es una biblioteca de compatibilidad que proporciona un conjunto de herramientas Linux en un entorno Windows. Mono es una biblioteca de compatibilidad que proporciona capacidades de Windows .NET en Linux.

  Evite las dependencias
de un sistema operativo específico; en su lugar, utilice servicios proporcionados
por la infraestructura middleware o proveedores de servicios.

* No instale su app manualmente.

  Su app se podría
instalar con frecuencia a demanda en el entorno de nube dinámico. El proceso de instalación debe ser mediante script y fiable, y los datos
de configuración se deben externalizar de los scripts.

  Como mínimo,
capture la instalación de su app como un conjunto uniforme de scripts
que sean independientes del sistema operativo. Mantenga la instalación de su app
en un tamaño reducido y portable, para adaptarse a las distintas técnicas de
automatización. Además, minimice las dependencias necesarias para la instalación
de apps.

Para obtener más información sobre apps listas para la nube, consulte
[The 12-factor
application](http://12factor.net/){:new_window}.

##Migración de sus apps
{: #ht_hostapp}

Puede migrar sus apps a {{site.data.keyword.Bluemix_notm}} de forma incremental,
en lugar de desplazarla completamente al entorno de nube. Primero puede migrar una parte de
sus apps y conectar a los datos existentes o sistema de registros mediante el
servicio Cloud integration.

En sus apps de nube, podría necesitar acceso a los datos o servicios de fondo, por ejemplo,
un sistema de registros. En {{site.data.keyword.Bluemix_notm}},
puede utilizar el servicio Secure Gateway para establecer un túnel seguro entre una
organización de {{site.data.keyword.Bluemix_notm}} y la red principal de fondo empresarial. El servicio permite a las
apps en {{site.data.keyword.Bluemix_notm}} acceder a los datos y servicios de la red principal de fondo. Para obtener detalles, consulte [Alcanzar el elemento de fondo empresarial con Bluemix Secure Gateway a través de la consola](https://developer.ibm.com/bluemix/2015/04/01/reaching-enterprise-backend-bluemix-secure-gateway/){:new_window}.

Para desplegar su app en {{site.data.keyword.Bluemix_notm}} como una app de Cloud Foundry,
seleccione un ejecutable del Catálogo de {{site.data.keyword.Bluemix_notm}}. El ejecutable contiene una app Hello World iniciadora que puede sustituir por su propia app. Si no encuentra un iniciador que proporcione
el ejecutable que quiere, puede aportar un paquete de compilación personalizado
compatible con Cloud Foundry a {{site.data.keyword.Bluemix_notm}}, utilizando la opción -b con el
mandato cf push. Para obtener detalles, consulte [Utilización de paquetes de compilación de la comunidad](../cfapps/byob.html).

Puede utilizar las herramientas y servicios siguientes que {{site.data.keyword.Bluemix_notm}} proporciona:

*Tabla 1. Herramientas de {{site.data.keyword.Bluemix_notm}}*

| Herramienta	| Método |
|:------|:--------|
|Interfaz de línea de mandatos de Cloud Foundry (cf cli)	|Gestione su código en el cliente local y utilizar la
interfaz de línea de mandatos de Cloud Foundry para enviar por push su app manualmente a
{{site.data.keyword.Bluemix_notm}}. Para obtener más información, consulte [Subir sus apps](../starters/upload_app.html).|
|Eclipse	|Gestione su código en Eclipse y utilice IBM Eclipse tools for {{site.data.keyword.Bluemix_notm}} para
enviar por push su app.|
|Integración con Git	|Gestione su código en GitHub e integre Git en {{site.data.keyword.Bluemix_notm}}. Puede colaborar con otros desarrolladores. Su app se despliega automáticamente en
{{site.data.keyword.Bluemix_notm}} cuando confirma los cambios en el código. No necesita enviar por push manualmente
la app.|
|{{site.data.keyword.Bluemix_notm}} DevOps
Delivery Pipeline	|Gestione su código en el repositorio DevOps GitHub y despliegue su app en
{{site.data.keyword.Bluemix_notm}} utilizando DevOps Delivery Pipeline.|


Si la plataforma Cloud Foundry no admite los requisitos de su app,
puede utilizar un contenedor o MV en la que el tiempo de ejecución se establezca,
configure y mantenga con opciones más personalizadas.

##Subir sus apps mediante la CLI de cf
{: #ht_cfcli}

Puede gestionar su código en el cliente local y utilizar la
interfaz de línea de mandatos de Cloud Foundry para subir su app manualmente a
{{site.data.keyword.Bluemix_notm}}. Si cambia el código, debe enviar por push su app otra vez a {{site.data.keyword.Bluemix_notm}}
para ejecutar el código actualizado.

Realice los pasos siguientes para migrar su app:

<ol>
<li>Instalar la interfaz de línea de mandatos de Cloud Foundry. Asegúrese de utilizar la versión
más reciente de la interfaz de línea de mandatos de cf.
<ol>
<li>Descargue el programa de instalación para su sistema operativo.</li>
<li>Siga el asistente de la herramienta para instalar la línea de mandatos.</li>
<li>Utilice el mandato siguiente para comprobar la versión de la interfaz de línea de mandatos de cf:
<pre>cf -v</pre></li>
</ol>
</li>

<li>Opcional: Si quiere especificar y guardar los detalles de despliegue antes de enviar por push
una app a {{site.data.keyword.Bluemix_notm}},
puede añadir el manifiesto de la app realizando los pasos siguientes:
<ol>
<li>Acceda al directorio de trabajo de su app y cree un archivo llamado manifest.yml, que es el nombre predeterminado.</li>
<li>Especifique los detalles de despliegue en el archivo de manifiesto. El ejemplo siguiente muestra un archivo de manifiesto de una app Java™.
<pre class="pre codeblock"><code>applications:
- disk_quota: 1024M
  host: myjavatest
  name: MyJavaTest
  path: webStarterApp.war
  domain: mybluemix.net
  instances: 1
  memory: 512M</code></pre>
<p>Para obtener más información sobre las opciones admitidas que puede utilizar en este archivo, consulte
[manifiesto de la app](../manageapps/depapps.html#appmanifest).

</p></li></ol>
</li>

<li>Envíe su app por Push. Puede subir su app utilizando el mandato push de cf.
<ol>
<li>Conecte e inicie sesión en {{site.data.keyword.Bluemix_notm}} ejecutando el mandato siguiente. Seleccione su
organización y espacio cuando se le solicite.
<pre>cf login -a https://api.ng.bluemix.net</pre></li>
<li>En el directorio de la app, escriba el mandato cf push
con el nombre de la app. El nombre de la app debe ser exclusivo en el entorno {{site.data.keyword.Bluemix_notm}}.
<pre>cf push nombre_app</pre></li>
<li>Opcional: Si utiliza un paquete de compilación externo, debe usar la opción -b
con el mandato push de cf. Por ejemplo:
<pre>cf push appname -b buildpack_URL</pre>
<p>Para obtener detalles, consulte Uso de paquetes de compilación.</p>
</li></ol>
</li>

<li>Opcional: Si modifica la app, debe cargar los cambios volviendo a especificar el mandato cf push. La interfaz de línea de mandatos cf utiliza sus opciones anteriores y las respuestas a las solicitudes para actualizar las instancias en ejecución de la app con los nuevos bits de código.</li>
</ol>

**Notas:**

* Cuando se utiliza el mandato cf push, la interfaz de línea de mandatos de copia todos los archivos y directorios del directorio actual en {{site.data.keyword.Bluemix_notm}}. Asegúrese de tener solo los archivos necesarios en su directorio de app.
* Asegúrese de que su organización dispone de memoria suficiente para todas las instancias de su
app. Para ver la cuota de memoria para su organización, utilice cf org org_name.
* Para obtener más información sobre cf push, consulte [Mandatos cf](../cli/reference/cfcommands/index.html).

##Migración de sus datos y uso de servicios
{: #ht_service}

Tras subir su app a
{{site.data.keyword.Bluemix_notm}},
seleccione en el Catálogo de {{site.data.keyword.Bluemix_notm}} el servicio al que está conectado su app,
cree una instancia de servicio, enlace la instancia a su app y luego reinicie su app.

La variable de entorno VCAP_SERVICES de su app es un
objeto JSON que contiene información sobre cómo interactuar con una instancia de servicio en
{{site.data.keyword.Bluemix_notm}}. La información incluye el nombre de instancia de servicio, credenciales y el URL de conexión
a la instancia de servicio.

Para ejecutar su código en {{site.data.keyword.Bluemix_notm}},
debe añadir la lógica de código para el análisis de la variable VCAP_SERVICES
para obtener información sobre la conexión de servicio. Modifique su app para
obtener el host y puerto asignados dinámicamente para la instancia de servicio
por medio de variables de entorno. El ejemplo siguiente muestra cómo obtener las credenciales de una
instancia de servicio de Postgre SQL en una app de Ruby:

```
services = JSON.parse(ENV['VCAP_SERVICES'], :symbolize_names => true)
        url = services.values.map do |srvs|
          srvs.map do |srv|
            if srv[:credentials][:uri] =~ /^postgres/
              srv[:credentials][:uri]
            else
              []
            end
          end
        end.flatten!.first
```		
{:codeblock}

Para asegurarse de que su app se pueda ejecutar en un entorno local tras modificarla para
{{site.data.keyword.Bluemix_notm}},
compruebe la presencia de la variable de entorno VCAP_SERVICES, que se establece para todas las
apps de {{site.data.keyword.Bluemix_notm}} Cloud
Foundry.


# Enlaces relacionados
{: #rellinks}

## Enlaces relacionados
{: #general}

* [IBM Containers](../containers/container_cli_ov.html)
* [Virtual Machines](../virtualmachines/vm_index.html)
* [Cómo empezar con Delivery Pipeline](../services/DeliveryPipeline/index.html)
* [Despliegue de apps con IBM Eclipse Tools for Bluemix](../manageapps/eclipsetools/eclipsetools.html)
* [La app de factor doce (twelve-factor)](http://12factor.net/){:new_window}
* [Alcanzar el elemento de fondo empresarial con Bluemix Secure Gateway a través de la consola](https://developer.ibm.com/bluemix/2015/04/01/reaching-enterprise-backend-bluemix-secure-gateway/){:new_window}
