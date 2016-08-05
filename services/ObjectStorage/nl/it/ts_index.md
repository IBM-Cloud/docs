{:new_window: target="_blank"}

# Risoluzione dei problemi di {{site.data.keyword.objectstorageshort}}
{: #troubleshooting}

*Ultimo aggiornamento: 24 giugno 2016*
{: .last-updated}

## È stato restituito un token contentpack non riconosciuto durante l'utilizzo di openstack4J con il profilo Liberty
{: #unrecognized_token}

### Sintomo 

È possibile che si verifichi la seguente traccia di stack quando utilizzi openstack4j con il profilo Liberty:

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

### Soluzione

Questo problema è causato da un errore di caricamento della classe, dove la libreria openstack4j contiene alcuni degli stessi pacchetti forniti nel profilo Liberty.  Ad esempio, OpenStack4j utilizza JERSEY, che può essere in conflitto con le librerie Wink.

Per risolvere il problema, utilizza la seguente procedura:

1. Utilizza il caricamento della classe inverso (parentLast).
2. Escludi jaxrs dalle funzioni abilitate.
