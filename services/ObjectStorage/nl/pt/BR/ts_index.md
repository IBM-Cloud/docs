{:new_window: target="_blank"}

# Resolução de problemas do {{site.data.keyword.objectstorageshort}}
{: #troubleshooting}

*Última atualização: 24 de junho de 2016*
{: .last-updated}

## Pacote de conteúdo de token não reconhecido retornado ao usar a openstack4J com o perfil Liberty
{: #unrecognized_token}

### Sintoma

O rastreio de pilha a seguir pode ocorrer ao usar a openstack4j com o perfil Liberty:

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

### Solução

Esse é um problema resultante de um carregamento de classe, em que a biblioteca openstack4j contém alguns dos mesmos pacotes fornecidos no perfil Liberty. Por exemplo, a OpenStack4j usa JERSEY, que pode colidir com as bibliotecas Wink.

Para resolver o problema, siga estas etapas:

1. Use o carregamento de classe reverso (parentLast).
2. Exclua jaxrs dos recursos ativados.
