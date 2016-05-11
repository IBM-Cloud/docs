---

copyright:
  years: 2015, 2016

---

{:new_window: target="_blank"}
{:codeblock: .codeblock}


# Configuración automática de servicios enlazados
{: #auto_config}

*Última actualización: 31 de marzo de 2016*

Puede enlazar diversos servicios a su aplicación Liberty. Los servicios se pueden gestionar mediante contenedor, mediante aplicación o ambos, en función de lo que desee el desarrollador.

Un servicio gestionado por la aplicación es un servicio que gestionan por completo la aplicación, sin ayuda de Liberty. La aplicación normalmente lee VCAP_SERVICES para obtener información sobre el servicio enlazado y accede directamente al servicio. La aplicación proporciona todo el código de acceso de cliente necesario. No hay dependencia de las características de Liberty ni de la configuración del archivo server.xml. La configuración automática del paquete de compilación de Liberty no se aplica a los servicios de este tipo.

Un servicio gestionado por contenedor es un servicio que gestionan por completo el tiempo de ejecución de Liberty. En algunos casos, es posible que la aplicación busque el servicio enlazado en JNDI, mientras que en otros el propio Liberty utiliza directamente el servicio. El paquete de compilación de Liberty lee VCAP_SERVICES para obtener información sobre los servicios enlazados. Para cada servicio gestionados por contenedor, el paquete de compilación lleva a cabo tres funciones.

* Genera [variables de nube](optionsForPushing.html#accessing_info_of_bound_services) para el servicio enlazado.
* Instala las características de Liberty y el código de acceso de cliente necesario para acceder al servicio enlazado.
* Genera o actualiza las stanzas del archivo server.xml que requiere el servicio.

Este proceso se conoce como configuración automática.
El paquete de compilación de Liberty proporciona configuración automática para los siguientes tipos de servicio:

* [ SQL Database](../../services/SQLDB/index.html#SQLDB)
* ClearDB MySQL Database
* [ MySQL](../../services/MySQL/index.html#MySQL)
* ElephantSQL
* [ PostgreSQL](../../services/PostgreSQL/index.html#PostgreSQL)
* [Base de datos Cloudant NoSQL](../../services/Cloudant/index.html#Cloudant)
* MongoLab
* [dashDB](../../services/dashDB/index.html#dashDB)
* [ Data
Cache](../../services/DataCache/index.html#data_cache)
* [ Session Cache](../../services/SessionCache/index.html#session_cache)
* [ MQ
Light](../../services/MQLight/index.html#mqlight010)
* [Monitoring and Analytics](../..//services/monana/index.html#gettingstartedtemplate)
* [Auto-Scaling](../../services/Auto-Scaling/index.html#autoscaling)
* [Single Sign On](../../services/SingleSignOn/index.html#sso_gettingstarted)
* [New Relic](newRelic.html)
* [Dynatrace](dynatrace.html)

Tal como se ha indicado, algunos servicios se pueden gestionar mediante aplicación o mediante contenedor. Mongo y SQLDB son ejemplos de dichos servicios. De forma predeterminada, el paquete de compilación de Liberty da por supuesto que estos servicios se gestionan mediante contenedor y los configura de forma automática. Si desea que la aplicación gestione el servicio, puede renunciar a la configuración automática del servicio estableciendo la variable de entorno services_autoconfig_excludes. Para obtener más información, consulte [Renuncia a la configuración automática del servicio](autoConfig.html#opting_out).

## Instalación de las características de Liberty y del código de acceso de cliente
{: #installation_of_liberty_features}

Cuando establece un enlace con un servicio gestionado por contenedor, es posible que el servicio necesite que se configuren las características de Liberty en la stanza featureManager del archivo server.xml. El paquete de compilación de Liberty actualiza la stanza featureManager e instala los binarios de soporte necesarios. Si el servicio necesita los archivos jar del controlador del cliente, estos archivos se descargan en una ubicación conocida de la instalación de Liberty.

Consulte la documentación del tipo de servicio enlazado para ver más detalles.

## Generación o actualización de stanzas de configuración de server.xml
{: #generating_or_updating_serverxml}

Cuando envía una aplicación autónoma, el paquete de compilación de Liberty genera la stanza server.xml, tal como se describe en [Opciones para enviar aplicaciones Liberty](optionsForPushing.html#options_for_pushing) a Bluemix. Cuando envía una aplicación autónoma y la enlaza a servicios gestionados por contenedor, el paquete de compilación de Liberty genera las stanzas necesarias de server.xml para los servicios enlazados.

Cuando el usuario especifica un archivo server.xml y lo enlaza a servicios gestionados por contenedor,
el paquete de compilación de Liberty:

* Genera la configuración correspondiente a los servicios enlazados si el archivo server.xml proporcionado no contiene stanzas de configuración para los servicios enlazados.
* Actualiza Genera la configuración correspondiente a los servicios enlazados si el archivo server.xml proporcionado contiene una stanza de configuración para los servicios enlazados.

Consulte la documentación del tipo de servicio enlazado para ver más detalles.

## Renuncia a la configuración automática del servicio
{: #opting_out}

En algunos casos, puede que no desee que el paquete de compilación de Liberty configure automáticamente los servicios ha enlazado. Vamos a examinar los casos de ejemplo.

* Mi aplicación utiliza MongoDB, pero deseo que la aplicación gestione directamente la conexión con la base de datos. La aplicación contiene el archivo jar de controlador de cliente necesario. No quiero que el paquete de compilación de Liberty configure automáticamente el servicio Mongo.
* Proporciono un archivo server.xml y he proporcionado las stanzas de configuración para la instancia de SQLDB porque necesito una configuración de fuente de datos no estándar. No quiero que el paquete de compilación de Liberty actualice mi archivo server.xml, pero necesito de todas formas el paquete de compilación de Liberty para asegurarme de que se instala el software de soporte adecuado.

Para renunciar a la configuración automática del servicio, utilice la variable de entorno services_autoconfig_excludes. Puede incluir esta variable de entorno en un archivo manifest.yml o la puede establecer mediante el cliente cf.

Puede renunciar a la configuración automática de servicios uno por uno. Puede renunciar a la configuración automática completa (como en el caso de ejemplo de Mongo) o sólo a las actualizaciones en la configuración del archivo server.xml (como en el caso de ejemplo de SQLDB). El valor que especifique para la variable de entorno services_autoconfig_excludes debe ser una serie, tal como se muestra a continuación.

* La serie puede contener especificaciones opt-out para uno o varios servicios.
* La especificación opt out para un servicio específico es service_type=option, donde:
  * service_type es la etiqueta del servicio, tal como se muestra en
VCAP_SERVICES.
  * El valor de option puede ser all o config.
* Si la serie contiene una especificación opt-out para más de un servicio,
las especificaciones opt out individuales deben ir separadas por un solo carácter de espacio en blanco.

Es decir, la gramática de la serie es la siguiente:

```
    Opt_out_string :: <service_type_specification[<delimiter>service_type_specification]*
    <service_type_specification> :: <service_type>=<option>
    <service_type> :: service type (service label as it appears in VCAP_SERVICES)
    <option> :: all | config
    <delimiter> :: one white space character
```
{: #codeblock}

**Importante**: El tipo de servicio que especifique debe coincidir con la etiqueta de servicio que aparece en la variable de entorno VCAP_SERVICES. No se permiten espacios en blanco.
**Importante**: No se permiten espacios en blanco en <service_type_specification>. Sólo se permiten espacios en blanco para separar varias instancias de <service_type_specification>.

Utilice la opción "all" para renunciar a todas las acciones de configuración automática para un servicio, como en el caso de ejemplo de Mongo anterior. Utilice la opción "config" para renunciar únicamente a las acciones de actualización de la configuración, como en el caso de ejemplo de SQLDB anterior.

A continuación se muestra un ejemplo de especificaciones opt-out en un archivo manifest.yml para los casos de ejemplo de Mongo y de SQLDB.

```
    env:
      services_autoconfig_excludes: mongodb-2.2=all

    env:
      services_autoconfig_excludes: sqldb=config

    env:
      services_autoconfig_excludes: sqldb=config mongodb-2.2=all
```
{: #codeblock}

A continuación se muestran ejemplos de cómo establecer la variable
de entorno services_autoconfig_excludes para la aplicación
myapp mediante la interfaz de línea de mandatos.

```
    $ cf set-env myapp services_autoconfig_excludes sqldb=config
    $ cf set-env myapp services_autoconfig_excludes "sqldb=config mongodb-2.2=all"
```
{: #codeblock}

# rellinks
## general
* [Tiempo de ejecución de Liberty](index.html)
* [Visión general del perfil de Liberty](http://www-01.ibm.com/support/knowledgecenter/SSAW57_8.5.5/com.ibm.websphere.wlp.nd.doc/ae/cwlp_about.html)
