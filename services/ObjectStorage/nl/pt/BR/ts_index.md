---

copyright:
  years: 2014, 2017
lastupdated: "2017-02-10"

---
{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:tsSymptoms: .tsSymptoms}
{:tsCauses: .tsCauses}
{:tsResolve: .tsResolve}

# Resolução de problemas do {{site.data.keyword.objectstorageshort}}
{: #troubleshooting}


Aqui estão as respostas para perguntas comuns de resolução de problemas sobre como usar o {{site.data.keyword.objectstoragefull}}.
{: shortdesc}

## Pacote de conteúdo de token não reconhecido retornado ao usar a openstack4J com o perfil Liberty
{: #unrecognized_token}


O rastreio de pilha a seguir poderá ocorrer ao usar openstack4j com o perfil Liberty:
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


Esse é um problema resultante de um carregamento de classe, em que a biblioteca openstack4j contém alguns dos mesmos pacotes fornecidos no perfil Liberty.  Por exemplo, a OpenStack4j usa JERSEY, que pode colidir com as bibliotecas Wink.
{: tsCauses}


É possível corrigir esse problema de uma das seguintes formas:
{: tsResolve}
  * Usando carregamento de classe reverso (parentLast).
  * Excluindo jaxrs dos recursos ativados.


## Obtendo ajuda e suporte para o {{site.data.keyword.objectstorageshort}}
{: #gettinghelp}

Se você tiver problemas ou perguntas ao usar o {{site.data.keyword.objectstoragefull}}, poderá obter ajuda procurando por informações ou fazendo perguntas através de um fórum. Também é possível abrir um chamado de suporte.

Ao usar os fóruns para fazer uma pergunta, marque a sua pergunta para que ela possa ser vista pelas equipes de desenvolvimento do {{site.data.keyword.Bluemix_notm}}.

* Se você tiver questões técnicas sobre o {{site.data.keyword.objectstorageshort}}, poste sua pergunta no <a href="http://stackoverflow.com/search?q=object-storage+ibm-bluemix" target="_blank">Stack Overflow <img src="../../icons/launch-glyph.svg" alt="Ícone de link externo"></a> e identifique-a com "ibm-bluemix" e "object-storage".
* Para perguntas sobre o serviço e sobre as instruções de introdução, use o fórum <a href="https://developer.ibm.com/answers/topics/objectstorage/?smartspace=bluemix" target="_blank">Respostas do IBM developerWorks dW <img src="../../icons/launch-glyph.svg" alt="Ícone de link externo"></a>. Inclua
as tags "objectstorage" e "bluemix".

Consulte [Obtendo ajuda](/docs/support/index.html#getting-help) para obter mais detalhes sobre o uso dos fóruns.

Para obter informações sobre como abrir um chamado de suporte IBM ou sobre níveis de suporte e severidades de chamado, consulte
[Entrando
em contato com o suporte](/docs/support/index.html#contacting-support).
