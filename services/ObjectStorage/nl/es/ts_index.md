{:new_window: target="_blank"}

# Resolución de problemas de {{site.data.keyword.objectstorageshort}}
{: #troubleshooting}

*Última actualización: 24 de junio de 2016*
{: .last-updated}

## Paquete de contenido de señal no reconocido devuelto al utilizar openstack4J con Perfil de Liberty
{: #unrecognized_token}

### Síntoma

El siguiente seguimiento de pila se puede haber producido al utilizar openstack4j con el Perfil de Liberty:

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

### Solución

Este problema se produce a partir de un problema de carga de clases, donde la biblioteca openstack4j contiene algunos de los mismos paquetes que se proporcionan en el perfil de Liberty. Por ejemplo, OpenStack4j utiliza JERSEY, lo que puede colisionar con las bibliotecas de Wink.

Para resolver el problema, siga estos pasos:

1. Utilice la carga de clases inversa (parentLast).
2. Excluya jaxrs de las características habilitadas.
