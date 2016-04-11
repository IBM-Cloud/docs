---

copyright:
  years: 2015, 2016

---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}

# Registro y rastreo
{: #logging_tracing}

*Última actualización: 23 de marzo de 2016*

## Archivos de registro
{: #log_files}

Los registros estándares de Liberty, como messages.log o el directorio ffdc, están disponibles en IBM Bluemix en el directorio de registros de cada instancia de aplicación. Se puede acceder a estos registros desde la consola de IBM Bluemix o mediante los mandatos cf logs y cf files.
Por ejemplo, para ver el archivo messages.log, ejecute el mandato:
```
    $ cf files <yourappname> logs/messages.log
```
{: codeblock}

El nivel de registro y otras opciones de rastreo se pueden establecer mediante el archivo de configuración de Liberty. Para obtener más información, consulte el tema sobre [Perfil de Liberty: rastreo y registro](http://www.ibm.com/support/knowledgecenter/SSAW57_8.5.5/com.ibm.websphere.wlp.nd.multiplatform.doc/ae/rwlp_logging.html?cp=SSAW57_8.5.5%2F3-17-0-0). El rastreo también se puede ajustar en una instancia de aplicación en ejecución mediante la consola de IBM Bluemix.

## Utilización de las funciones de rastreo y volcado
{: #using_trace_and_dump}

En la interfaz de usuario de IBM Bluemix, dispone de funciones de rastreo y volcado.
* Utilice Trace para ver y actualizar el registro de Liberty
traceSpecification en instancias de la aplicación en ejecución.
* Utilice Dump para crear y manipular volcados de hebras y de almacenamiento dinámico en instancias de la aplicación en ejecución.

Para realizar esta acción, seleccione una aplicación de Liberty en la interfaz de usuario. Bajo Tiempo de ejecución en el panel de navegación de la izquierda, puede abrir los detalles de la instancia. Seleccione una o varias instancias. Bajo el menú Acciones, puede elegir TRACE o DUMP.

# rellinks
## general
* [Tiempo de ejecución de Liberty](index.html)
* [Visión general del perfil de Liberty](http://www-01.ibm.com/support/knowledgecenter/SSAW57_8.5.5/com.ibm.websphere.wlp.nd.doc/ae/cwlp_about.html)
