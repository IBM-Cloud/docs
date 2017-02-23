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

# Risoluzione dei problemi di {{site.data.keyword.objectstorageshort}}
{: #troubleshooting}


Queste sono le risposte alle domande sulla risoluzione dei problemi comuni riguardanti l'utilizzo di {{site.data.keyword.objectstoragefull}}.
{: shortdesc}

## È stato restituito un token contentpack non riconosciuto durante l'utilizzo di openstack4J con il profilo Liberty
{: #unrecognized_token}


È possibile che si verifichi la seguente traccia di stack quando utilizzi openstack4j con il profilo Liberty:
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


Questo problema è causato da un errore di caricamento della classe, dove la libreria openstack4j contiene alcuni degli stessi pacchetti forniti nel profilo Liberty.  Ad esempio, OpenStack4j utilizza JERSEY, che può essere in conflitto con le librerie Wink.
{: tsCauses}


Puoi risolvere questo problema nei seguenti modi:
{: tsResolve}
  * Utilizzando il caricamento della classe inverso (parentLast).
  * Escludendo jaxrs dalle funzioni abilitate.


## Come ottenere aiuto e supporto per {{site.data.keyword.objectstorageshort}}
{: #gettinghelp}

Se hai dei problemi o delle domande quando utilizzi {{site.data.keyword.objectstoragefull}},
puoi ottenere aiuto ricercando le informazioni o facendo delle domande in un forum. Puoi inoltre aprire un ticket di supporto.

Quando utilizzi i forum per fare una domanda, contrassegna con una tag la tua domanda in modo che sia visualizzabile dai team di sviluppo {{site.data.keyword.Bluemix_notm}}.

* Se hai domande tecniche sullo sviluppo o la distribuzione di un'applicazione con {{site.data.keyword.objectstorageshort}},
inserisci la tua domanda in <a href="http://stackoverflow.com/search?q=object-storage+ibm-bluemix" target="_blank">Stack Overflow
<img src="../../icons/launch-glyph.svg" alt="icona link esterno"></a> e contrassegnala con le  tag "ibm-bluemix" e "object-storage".
* Per domande sul servizio e sulle istruzioni per l'utilizzo iniziale, utilizza il forum
<a href="https://developer.ibm.com/answers/topics/objectstorage/?smartspace=bluemix" target="_blank">IBM developerWorks dW Answers
<img src="../../icons/launch-glyph.svg" alt="icona link esterno"></a>. Includi le tag "objectstorage" e "bluemix".

Consulta [Come ottenere supporto](/docs/support/index.html#getting-help) per ulteriori dettagli sull'utilizzo dei forum.

Per informazioni su come aprire un ticket di supporto IBM o sui livelli di supporto e sulla gravità dei ticket, consulta
[Come contattare il supporto](/docs/support/index.html#contacting-support).
