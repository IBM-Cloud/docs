{:new_window: target="_blank"}

# {{site.data.keyword.objectstorageshort}} - Fehlerbehebung
{: #troubleshooting}

*Letzte Aktualisierung: 24. Juni 2016*
{: .last-updated}

## Nicht erkanntes Token-Content-Pack bei der Verwendung von openstack4J mit Liberty-Profil zurückgegeben
{: #unrecognized_token}

### Symptom

Bei der Verwendung von openstack4j mit dem Liberty-Profil kann es zu folgendem Stack-Trace kommen:

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

### Lösung

Die Ursache des Problems ist ein Klassenladeproblem, bei dem die Bibliothek 'openstack4j' einige derselben Pakete aufweist, die im Liberty-Profil bereitgestellt werden.  So verwendet OpenStack4j beispielsweise JERSEY; dies kann zu Konflikten mit den Wink-Bibliotheken führen.

Führen Sie die folgenden Schritte aus, um das Problem zu beheben:

1. Umgekehrtes Laden von Klassen nutzen (parentLast).
2. jaxrs aus aktivierten Features ausschließen.
