---

copyright:
  years: 2014, 2017
lastupdated: "2017-01-17"

---
{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:tsSymptoms: .tsSymptoms}
{:tsCauses: .tsCauses}
{:tsResolve: .tsResolve}

# Traitement des incidents liés à {{site.data.keyword.objectstorageshort}}
{: #troubleshooting}


Cette rubrique fournit les réponses aux questions courantes relatives au traitement des incidents d'utilisation d'{{site.data.keyword.objectstoragefull}}.
{: shortdesc}

## Jeton contentpack non reconnu renvoyé lors de l'utilisation d'openstack4J avec le profil Liberty
{: #unrecognized_token}


La trace de pile suivante peut s'afficher lors de l'utilisation d'openstack4j avec le profil Liberty :
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


Ce problème est généré par une erreur de chargement des classes, où la bibliothèque openstack4j contient certains des packages qui sont fournis dans
le profil Liberty.  Par
exemple, OpenStack4j utilise JERSEY, qui peut entrer en conflit avec les bibliothèques Wink.
{: tsCauses}


Vous pouvez résoudre ce problème en :
{: tsResolve}
  * Utilisant le chargement de classes inversé (parentLast).
  * Excluant jaxrs des fonctions activées.


## Aide et support pour {{site.data.keyword.objectstorageshort}}
{: #gettinghelp}

Si vous avez des problèmes ou des questions quand vous utilisez {{site.data.keyword.objectstoragefull}}, vous pouvez obtenir de l'aide en recherchant des informations précises ou en posant des questions via un forum. Vous pouvez aussi ouvrir un ticket de demande de service.

Quand vous utilisez les forums pour poser une question, prenez soin d'étiqueter cette dernière de façon à ce qu'elle soit vue par les équipes de développement {{site.data.keyword.Bluemix_notm}}.

* Si vous avez des questions techniques sur le développement ou le déploiement d'une application avec {{site.data.keyword.objectstorageshort}}, postez votre question sur [stackoverflow](http://stackoverflow.com/search?q=object-storage+ibm-bluemix){: new_window} et marquez votre question avec les étiquettes "ibm-bluemix" et "object-storage".
* Pour des questions relatives au service et aux instructions de mise en route, utilisez le forum [IBM developerWorks - dW Answers](https://developer.ibm.com/answers/topics/objectstorage/?smartspace=bluemix){: new_window}. Incluez les étiquettes "objectstorage" et "bluemix".

Voir la rubrique expliquant comment [obtenir de l'aide](/docs/support/index.html#getting-help) pour plus de détails sur l'utilisation des forums.

Pour plus d'informations sur l'ouverture d'un ticket de demande de service IBM, sur les niveaux de support disponibles ou les niveaux de gravité des tickets, voir la rubrique décrivant [comment contacter le support](/docs/support/index.html#contacting-support).
