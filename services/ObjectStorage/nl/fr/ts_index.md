{:new_window: target="_blank"}

# Traitement des incidents liés à {{site.data.keyword.objectstorageshort}}
{: #troubleshooting}

*Dernière mise à jour : 24 juin 2016*
{: .last-updated}

## Jeeton contentpack non reconnu renvoyé lors de l'utilisation d'openstack4J avec le profil Liberty 
{: #unrecognized_token}

### Symptôme

La trace de pile suivante peut s'afficher lors de l'utilisation d'openstack4j avec le profil Liberty : 

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

### Solution

Ce problème est généré par une erreur de chargement des classes, où la bibliothèque openstack4j contient certains des packages qui sont fournis dans
le profil Liberty. Par
exemple, OpenStack4j utilise JERSEY, qui peut entrer en conflit avec les bibliothèques Wink. 

Pour résoudre le problème, procédez comme suit : 

1. Utilisez le chargement de classes inversé (parentLast).
2. Excluez jaxrs des fonctions activées. 
