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

# {{site.data.keyword.objectstorageshort}} - Fehlerbehebung
{: #troubleshooting}


Im Folgenden finden Sie die Antworten auf häufige Fragen zur Fehlerbehebung bei der Verwendung von {{site.data.keyword.objectstoragefull}}.
{: shortdesc}

## Nicht erkanntes Token-Content-Pack bei der Verwendung von openstack4J mit Liberty-Profil zurückgegeben
{: #unrecognized_token}


Bei der Verwendung von openstack4j mit dem Liberty-Profil kann es zu folgendem Stack-Trace kommen:
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


Die Ursache des Problems ist ein Klassenladeproblem, bei dem die Bibliothek 'openstack4j' einige derselben Pakete enthält, die im Liberty-Profil bereitgestellt werden.  So verwendet OpenStack4j beispielsweise JERSEY; dies kann zu Konflikten mit den Wink-Bibliotheken führen.
{: tsCauses}


Dieses Problem kann auf einem der folgenden Wege behoben werden:
{: tsResolve}
  * Umgekehrtes Laden von Klassen nutzen (parentLast)
  * jaxrs aus aktivierten Features ausschließen


## Hilfe und Unterstützung für {{site.data.keyword.objectstorageshort}} erhalten
{: #gettinghelp}

Hilfe zu Problemen oder Fragen bei Verwendung von {{site.data.keyword.objectstoragefull}} finden Sie, indem Sie in einem Forum nach Informationen suchen oder dort Fragen stellen. Sie haben außerdem die Möglichkeit, ein Support-Ticket zu öffnen.

Wenn Sie in Foren eine Frage stellen, versehen Sie Ihre Frage mit einem Tag, sodass sie von den {{site.data.keyword.Bluemix_notm}}-Entwicklungsteams registriert wird.

* Wenn Sie technische Fragen zu {{site.data.keyword.objectstorageshort}} haben, posten Sie Ihre Frage bei <a href="http://stackoverflow.com/search?q=object-storage+ibm-bluemix" target="_blank">Stack Overflow <img src="../../icons/launch-glyph.svg" alt="Symbol für externen Link"></a> und versehen Sie sie mit den Tags "ibm-bluemix" und "object-storage".
* Bei Fragen zum Service sowie zum Abruf von Einführungsanweisungen wenden Sie sich an das Forum <a href="https://developer.ibm.com/answers/topics/objectstorage/?smartspace=bluemix" target="_blank">IBM developerWorks dW Answers <img src="../../icons/launch-glyph.svg" alt="Symbol für externen Link"></a>. Versehen Sie Ihre Anfrage mit den Tags "objectstorage" und "bluemix".

Unter [Hilfe anfordern](/docs/support/index.html#getting-help) finden Sie weitere Informationen zur Nutzung der Foren.

Informationen zum Öffnen eines IBM Support-Tickets oder zu den Supportebenen und Ticket-Prioritätsstufen finden Sie unter [Support kontaktieren](/docs/support/index.html#contacting-support).
