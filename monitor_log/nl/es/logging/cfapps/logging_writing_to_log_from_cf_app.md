---

copyright:
  years: 2015, 2017

lastupdated: "2017-02-06"

---


{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}
{:screen: .screen}

# Registro de la aplicación de tiempo de ejecución a través de las apps de CF
{: #logging_writing_to_log_from_cf_app}

En {{site.data.keyword.Bluemix}}, para mantener datos de registro para una app de Cloud Foundry y su tiempo de ejecución, debe escribir los registros en STDOUT y STDERR. 
{:shortdesc}

En {{site.data.keyword.Bluemix_notm}}, los registros de STDOUT y STDERR se recopilan automáticamente:

* STDOUT (salida estándar) proporciona información general.  
* STDERR (error estándar) proporciona información que incluye mensajes de error y otros avisos de diagnóstico. 

Loggregator recopila automáticamente los datos de error estándares y de salida estándar. Loggregator es el componente que reenvía registros desde dentro de Cloud Foundry. 

Por ejemplo, 

Para una **app de Liberty Cloud Foundry**, loggregator recopilará automáticamente el console.log para el servidor de liberty predeterminado. 

* El console.log contiene el STDOUT y STDERR redirigidos desde el proceso de JVM. La salida de la consola contiene sucesos principales y errores si utiliza la configuración predeterminada de consoleLogLevel. La salida de la consola también contiene los mensajes escritos en las secuencias system.out y system.err si utiliza la configuración predeterminada de copySystemStreams. La salida de la consola siempre contiene mensajes que graba directamente el proceso de la JVM, como por ejemplo la salida -verbose:gc. Puede ajustar el nivel de registro de liberty a través del server.xml.
* El consoleLogLevel establece el nivel de filtro del manejador de console.log. Al establecer el consoleLogLevel en INFO, configure todos los mensajes INFO, AUDIT, WARNING, y ERROR para que se graben en el archivo console.log. **Nota:** las entradas de registro FINE, FINER, FINEST sólo se graban en el archivo trace.log.

Para obtener más información sobre las aplicaciones de Liberty for Java, consulte [Liberty Profile: Registro y rastreo ![Icono de enlace externo](../../../icons/launch-glyph.svg "Icono de enlace externo")](http://www-01.ibm.com/support/knowledgecenter/was_beta_liberty/com.ibm.websphere.wlp.nd.multiplatform.doc/ae/rwlp_logging.html){: new_window}.

Para una **app de Node.js Cloud Foundry**, puede utilizar el módulo de registro de la consola incorporada para configurar el registro para el tiempo de ejecución en {{site.data.keyword.Bluemix}}. Puede poner mensajes tanto en stdout como en stderr:

* console.log('message') enviará el mensaje a la secuencia STDOUT
* console.error('error_message') enviará el error a la secuencia STDERR

Para obtener más información sobre aplicaciones Node.js, consulte [Cómo registrar en node.js ![Icono de enlace externo](../../../icons/launch-glyph.svg "Icono de enlace externo")](http://docs.nodejitsu.com/articles/intermediate/how-to-log){: new_window}.


Para obtener más información sobre las **aplicaciones Ruby on Rails**, consulte [El registrador ![Icono de enlace externo](../../../icons/launch-glyph.svg "Icono de enlace externo")](http://guides.rubyonrails.org/debugging_rails_applications.html#the-logger){: new_window}.

En la tabla siguiente se muestra la correlación entre algunos registros de tiempos de ejecución de aplicaciones y los registros que Loggregator selecciona automáticamente:

| **Tiempo de ejecución** |    **STDOUT**     | **STDERR** |
|-----------------|-------------------|-------------------|
| Liberty | system.out | system.err |
| Node.js | console.log, console.info | console.error, console.warn |
| Ruby | stdout| stderr |
{: caption="Tabla 1. Correlación entre algunos registros de tiempos de ejecución de aplicaciones y los registros que Loggregator selecciona automáticamente" caption-side="top"}

