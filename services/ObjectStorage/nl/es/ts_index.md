---

copyright:
  years: 2014, 2016

---
{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:tsSymptoms: .tsSymptoms}
{:tsCauses: .tsCauses}
{:tsResolve: .tsResolve}

# Resolución de problemas de {{site.data.keyword.objectstorageshort}}
{: #troubleshooting}

*Última actualización: 19 de octubre de 2016*
{: .last-updated}

A continuación, encontrará las respuestas a las preguntas sobre resolución de problemas más comunes sobre el uso de {{site.data.keyword.objectstoragefull}}.
{: shortdesc}

## Paquete de contenido de señal no reconocido devuelto al utilizar openstack4J con Perfil de Liberty
{: #unrecognized_token}


El siguiente seguimiento de pila se puede haber producido al utilizar openstack4j con el Perfil de Liberty:
```
Exception thrown by application class 'org.openstack4j.connectors.okhttp.HttpResponseImpl.readEntity:124'
org.openstack4j.api.exceptions.ClientResponseException: Unrecognized token 'contentpack': was expecting ('true', 'false' or 'null') at [Source: contentpack ; line: 1, column: 12]
at org.openstack4j.connectors.okhttp.HttpResponseImpl.readEntity(HttpResponseImpl.java:124)
at org.openstack4j.core.transport.HttpEntityHandler.handle(HttpEntityHandler.java:56)
at org.openstack4j.connectors.okhttp.HttpResponseImpl.getEntity(HttpResponseImpl.java:68)
at org.openstack4j.openstack.internal.BaseOpenStackService$Invocation.execute(BaseOpenStackService.java:169)
at org.openstack4j.openstack.internal.BaseOpenStackService$Invocation.execute(BaseOpenStackService.java:163)
at org.openstack4j.openstack.storage.object.internal.ObjectStorageContainerServiceImpl.list(ObjectStorageContainerServiceImpl.java:41)
at com.mimotic.SecureMessageApp.HelloResource.getInformation(HelloResource.java:47)
at sun.reflect.NativeMethodAccessorImpl.invoke0(Native Method)
    at sun.reflect.NativeMethodAccessorImpl.invoke(Unknown Source)
    at sun.reflect.DelegatingMethodAccessorImpl.invoke(Unknown Source)
    at java.lang.reflect.Method.invoke(Unknown Source)
```
{: screen}
{: tsSymptoms}


Este problema se produce a partir de un problema de carga de clases, donde la biblioteca openstack4j contiene algunos de los mismos paquetes que se proporcionan en el perfil de Liberty.  Por ejemplo, OpenStack4j utiliza JERSEY, lo que puede colisionar con las bibliotecas de Wink.
{: tsCauses}


Puede solucionar este problema mediante alguna de estas formas:
{: tsResolve}
  * Utilizando la carga de clases inversa (parentLast).
  * Excluyendo jaxrs de las características habilitadas.


## Obtención de ayuda y soporte para {{site.data.keyword.objectstorageshort}}
{: #gettinghelp}

Si tiene problemas o dudas al utilizar {{site.data.keyword.objectstoragefull}}, puede obtener ayuda buscando información o formulando preguntas en foros. También puede abrir una incidencia de soporte.

Al utilizar los foros para formular una pregunta, añada una etiqueta para que la vean los equipos de desarrollo de {{site.data.keyword.Bluemix_notm}}.

* Si tiene preguntas técnicas sobre {{site.data.keyword.objectstorageshort}}, publique su pregunta en [Stack Overflow](http://stackoverflow.com/search?q=object-storage+ibm-bluemix){: new_window} y añada las etiquetas "ibm-bluemix" y "object-storage".
* Para formular preguntas sobre el servicio y obtener instrucciones de iniciación, utilice el foro [IBM developerWorks dW Answers](https://developer.ibm.com/answers/topics/objectstorage/?smartspace=bluemix){: new_window}. Incluya las etiquetas "objectstorage" y "bluemix".

Consulte [Obtener ayuda](https://console.ng.bluemix.net/docs/support/index.html#getting-help){: new_window} para obtener más información sobre el uso de los foros.

Para obtener más información sobre cómo abrir una incidencia de soporte de IBM, o sobre los niveles de soporte y las gravedades de las incidencias, consulte [Contacto con soporte](https://console.ng.bluemix.net/docs/support/index.html#contacting-support){: new_window}.
