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

# Resolução de problemas do {{site.data.keyword.objectstorageshort}}
{: #troubleshooting}

*Última atualização: 19 de outubro de 2016*
{: .last-updated}

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

* Se você tiver questões técnicas sobre o {{site.data.keyword.objectstorageshort}}, poste a sua pergunta em
[Estouro
da capacidade](http://stackoverflow.com/search?q=object-storage+ibm-bluemix){: new_window} e marque a sua pergunta com "ibm-bluemix" e "object-storage".
* Para perguntas sobre o serviço e obter informações de introdução, use o fórum do [IBM developerWorks dW Answers](https://developer.ibm.com/answers/topics/objectstorage/?smartspace=bluemix){: new_window}. Inclua
as tags "objectstorage" e "bluemix".

Consulte [Obtendo ajuda](https://console.ng.bluemix.net/docs/support/index.html#getting-help){: new_window} para obter mais detalhes sobre o uso dos fóruns.

Para obter informações sobre como abrir um chamado de suporte IBM ou sobre níveis de suporte e severidades de chamado, consulte
[Entrando
em contato com o suporte](https://console.ng.bluemix.net/docs/support/index.html#contacting-support){: new_window}.
