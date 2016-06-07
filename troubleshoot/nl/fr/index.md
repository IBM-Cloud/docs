---

copyright:
  2015, 2016

---

{:tsSymptoms: .tsSymptoms} 
{:tsCauses: .tsCauses} 
{:tsResolve: .tsResolve} 
{:new_window: target="_blank"}  
{:shortdesc: .shortdesc}
{:codeblock: .codeblock} 

# Traitement des incidents liés à l'accès à {{site.data.keyword.Bluemix_notm}} 
{: #accessing}

*Dernière mise à jour : 16 mai 2016*

Des problèmes d'ordre général liés à {{site.data.keyword.Bluemix}} peuvent survenir
: par exemple, un utilisateur ne parvient pas à établir une connexion dans
{{site.data.keyword.Bluemix_notm}},
un compte est bloqué à l'état en attente, etc. Toutefois, dans de nombreux cas, ces problèmes peuvent être résolus en quelques opérations simples. 
{:shortdesc}

## Connexion à {{site.data.keyword.Bluemix_notm}} impossible
{: #ts_logintobm}

Vous devez disposer d'un ID et d'un mot de passe IBM valides pour vous connecter à {{site.data.keyword.Bluemix_notm}}.


Lorsque vous tentez de vous connecter à {{site.data.keyword.Bluemix_notm}}, le message d'erreur suivant s'affiche : 
{: tsSymptoms} 

`The IBM id and/or password
entered below is incorrect. Please try again.`


L'ID
et le mot de passe IBM que vous utilisez pour vous connecter à {{site.data.keyword.Bluemix_notm}} ne sont pas valides.
{: tsCauses} 
 

Pour obtenir un ID et un mot de passe IBM valides, accédez à la page My IBM profile et procédez comme suit :
{: tsResolve}
  * Si vous disposez déjà d'un ID IBM et que vous voulez vérifier si l'ID et le mot de passe sont valides, cliquez sur **Sign in** et entrez vos ID et mot de passe dans la page qui s'affiche. Si vous avez oublié votre mot de passe, cliquez sur **Forgot your password** dans la partie droite de la page Sign in pour le réinitialiser. Si vous avez oublié votre ID IBM ou que vous continuez à avoir des problèmes avec le mot de passe, prenez contact avec le service Worldwide IBM
Registration Helpdesk pour de l'aide. 
  * Si vous ne disposez pas d'un ID IBM, cliquez sur **Register** pour enregistrer un ID et un mot de passe. 
  
**Remarque :** pour les employés IBM, l'ID IBM peut être différent de l'ID de connexion à l'intranet. 





## Des modifications n'ont pas été sauvegardées
{: #ts_unsaved_changes}


Lorsque vous naviguez dans la page des détails de l'application, vous ne pourrez peut-être pas effectuer d'action et vous serez invité à sauvegarder vos modifications pour pouvoir continuer. 


Lorsque vous essayez de vérifier votre appli ou vos services sur la page des détails de l'application, vous obtenez toujours le message d'erreur suivant :
{: tsSymptoms} 

`Des modifications n'ont pas été sauvegardées dans la page nom_appli. Sauvegardez ou annulez les modifications.`


Lorsque vous survolez avec la souris les zones **INSTANCES** ou **QUOTA DE MEMOIRE** dans le panneau du contexte d'exécution, les valeurs changent. Ce comportement est normal. Toutefois, le message d'erreur vous invite à sauvegarder les paramètres de mémoire ou d'instance avant de quitter la page. 
{: tsCauses}


Fermez la fenêtre de message, puis cliquez sur le bouton **REINITIALISER** de votre contexte d'exécution. 
{: tsResolve} 




    
    
## Le basculement automatique entre les régions {{site.data.keyword.Bluemix_notm}} n'est pas disponible
{: #ts_failover}

Vous ne pouvez pas utiliser le basculement automatique entre les régions
{{site.data.keyword.Bluemix_notm}}. Toutefois, vous pouvez utiliser un fournisseur DNS qui prend en charge
le basculement entre plusieurs adresses IP comme solution de contournement.
 

Lorsqu'une région {{site.data.keyword.Bluemix_notm}} n'est plus disponible, les applications qui sont exécutées dans cette région ne sont plus
disponibles non plus, même si les mêmes applications s'exécutent dans une autre région {{site.data.keyword.Bluemix_notm}}.
{: tsSymptoms}

 
{{site.data.keyword.Bluemix_notm}}
ne fournit pas encore le basculement automatique d'une région à une autre.
{: tsCauses}

 
Vous pouvez utiliser un fournisseur DNS qui prend en charge le basculement intelligent entre plusieurs adresses IP et configurer manuellement vos
paramètres DNS pour activer le basculement automatique entre des régions {{site.data.keyword.Bluemix_notm}}. NSONE, Akamai et Dyn sont des fournisseurs DNS qui proposent cette capacité.
{: tsResolve}

Lorsque vous configurez vos paramètres DNS, vous devez spécifier les adresses IP publiques des régions {{site.data.keyword.Bluemix_notm}}
dans lesquelles vos applications s'exécutent. Pour obtenir l'adresse IP publique d'une région {{site.data.keyword.Bluemix_notm}}, utilisez la
commande `nslookup`. Par exemple, vous pouvez entrer la commande suivante dans une fenêtre de ligne de commande :
```
nslookup mybluemix.net
```



## Compte en attente
{: #ts_accntpding}

Si votre compte est en attente, vous ne pouvez pas vous connecter à {{site.data.keyword.Bluemix_notm}}.

 
Après avoir procédé à votre inscription pour un compte d'essai {{site.data.keyword.Bluemix_notm}}, il est possible que vous ne puissiez pas vous connecter à {{site.data.keyword.Bluemix_notm}} et que le message suivant s'affiche :
{: tsSymptoms}

<code>Votre
compte est en attente. La confirmation par courrier électronique peut prendre jusqu'à 24 heures ; vérifiez également votre dossier de courrier indésirable. Si vous ne recevez pas votre confirmation par courrier électronique, envoyez un message au
<a href="http://ibm.biz/bluemixsupport.com" target="_blank">support Bluemix</a>.</code>


Après avoir procédé à votre inscription pour un compte d'essai {{site.data.keyword.Bluemix_notm}}, vous recevez une confirmation par courrier électronique. Cliquez
sur le lien que contient ce courrier électronique pour compléter le processus d'enregistrement.
{: tsCauses} 

La confirmation par courrier électronique est envoyée à l'adresse de courrier électronique que vous avez indiquée. Vérifiez votre boîte de réception et votre dossier de courrier indésirable. Si vous ne recevez pas de confirmation par courrier électronique, prenez contact avec le
[support {{site.data.keyword.Bluemix_notm}}](http://ibm.biz/bluemixsupport.com){: new_window}.  
{: tsResolve}



## Impossibilité d'ajouter des utilisateurs à une organisation
{: #ts_adduser}

Vous pouvez inviter plusieurs utilisateurs dans la même organisation. Vous pouvez inviter des utilisateurs dans votre organisation
uniquement si vous êtes propriétaire de compte ou si vous êtes à la fois responsable et membre de l'organisation.
 

Le lien **Inviter un nouvel
utilisateur** n'apparaît pas dans votre section **Gérer les organisations**. 
{: tsSymptoms}

 

Seuls les utilisateurs
{{site.data.keyword.Bluemix_notm}} suivants peuvent inviter des utilisateurs dans
une organisation :
{: tsCauses}
  * Le propriétaire de compte de l'organisation
  * Les responsables de l'organisation qui sont également membres, et non collaborateurs, de l'organisation
  
Dans {{site.data.keyword.Bluemix_notm}}, vous pouvez être membre ou collaborateur d'une organisation.

<dl><dt>Collaborateur</dt>
<dd>Vous êtes collaborateur d'une organisation si vous possédez déjà un compte
{{site.data.keyword.Bluemix_notm}} et que quelqu'un vous invite dans l'organisation.</dd>
<dt>Membre</dt>
<dd>Vous êtes membre d'une organisation si vous ne possédez pas de compte
{{site.data.keyword.Bluemix_notm}}, mais que quelqu'un vous invite dans l'organisation et que
vous vous inscrivez à {{site.data.keyword.Bluemix_notm}} depuis l'invitation.</dd>
</dl>


Vous ne pouvez pas inviter d'utilisateurs dans votre organisation si vous êtes un collaborateur de l'organisation, même si vous avez
été désigné comme responsable de l'organisation.

**Remarque :** tous les responsables de l'organisation, y compris ceux qui sont des collaborateurs d'une organisation, peuvent
ajouter, modifier et supprimer des
utilisateurs qui se trouvent déjà dans l'organisation.

 

Si vous ne pouvez pas inviter d'utilisateurs dans votre organisation et que vous avez besoin d'un autre rôle pour ce faire, prenez contact
avec le responsable de l'organisation afin qu'il change votre rôle. Pour identifier le responsable de votre organisation, procédez comme suit :
{: tsResolve}

  1. Accédez au tableau de bord {{site.data.keyword.Bluemix_notm}}, cliquez sur l'icône **Compte et support** ![Compte et support](images/account_support.svg) dans la barre de menu supérieure, et sélectionnez **Gérer les organisations**.
  2. Sélectionnez votre organisation et affichez les informations relatives au responsable dans l'onglet **Utilisateurs**.  
  
Si
vous ne parvenez pas à inviter des utilisateurs car vous êtes collaborateur et non membre, vous devez supprimer votre compte
{{site.data.keyword.Bluemix_notm}} précédent, puis être invité à rejoindre le compte en tant
que membre de l'organisation. Pour supprimer votre compte précédent et rejoindre le compte en tant que membre, procédez comme suit : 

  1. Contactez [{{site.data.keyword.Bluemix_notm}} Support](http://ibm.biz/bluemixsupport){: new_window} pour ouvrir un ticket de demande de service et demander la suppression de votre compte. Si vous voulez sauvegarder des données associées à votre ancien compte et les déplacer dans votre nouveau
compte, incluez ces informations dans votre courrier électronique. 
  2. Une fois votre compte supprimé, demandez à un utilisateur disposant du rôle de responsable de l'organisation de vous inviter dans l'organisation en
tant que responsable de l'organisation. Ensuite, inscrivez-vous à
{{site.data.keyword.Bluemix_notm}} à partir de l'invitation. 




## L'enregistrement d'utilisateurs par lots n'est pas pris en charge
{: #ts_batchregistration}

Lorsque
vous enregistrez des utilisateurs pour {{site.data.keyword.Bluemix_notm}}, vous devez
enregistrer chaque utilisateur individuellement.
 

{{site.data.keyword.Bluemix_notm}}
ne permet pas d'enregistrer plusieurs utilisateurs simultanément.
{: tsSymptoms}
 

{{site.data.keyword.Bluemix_notm}}
ne prend pas en charge l'enregistrement d'utilisateurs par lots. Pour enregistrer des utilisateurs pour
{{site.data.keyword.Bluemix_notm}}, vous devez enregistrer chaque utilisateur
individuellement.
{: tsCauses}
 

Pour enregistrer plusieurs utilisateurs pour
{{site.data.keyword.Bluemix_notm}}, vous devez effectuer les opérations suivantes pour chaque
utilisateur :
{: tsResolve}

  1. Cliquez sur **S'INSCRIRE** dans le coin supérieur droit de l'interface utilisateur
{{site.data.keyword.Bluemix_notm}}.
  2. Suivez les étapes de l'assistant.

    

## Une page {{site.data.keyword.Bluemix_notm}} ne peut pas être chargée
{: #ts_err}

Lorsque vous utilisez l'interface utilisateur {{site.data.keyword.Bluemix_notm}}, il est possible que vous ne puissiez pas charger une page
{{site.data.keyword.Bluemix_notm}}. A la place, un message d'erreur BXNUI0001E ou BXNUI0016E peut s'afficher.
 

Dans l'interface utilisateur {{site.data.keyword.Bluemix_notm}}, un des messages d'erreur suivants peut s'afficher :
{: tsSymptoms}

`BXNUI0001E: La page n'a pas été chargée car Bluemix n'a pas détecté s'il existait une session.`


`BXNUI0016E: Les applications et les services n'ont pas été extraits car une page Bluemix n'a pas été chargée.`

 

Pour remédier au problème, effectuez une ou plusieurs des actions suivantes :
{: tsResolve}

  * Actualisez ou redémarrez votre navigateur.
  * Déconnectez-vous de {{site.data.keyword.Bluemix_notm}}, puis reconnectez-vous.
  * Utilisez le mode de navigation privée de votre navigateur. 
  * Effacez les cookies et le cache du navigateur.
  * Utilisez un navigateur différent. Pour des informations sur les versions des navigateurs qui sont prises en charge par
{{site.data.keyword.Bluemix_notm}}, voir [{{site.data.keyword.Bluemix_notm}} Prerequisites](https://developer.ibm.com/bluemix/support/#prereqs){: new_window}.
  * Si vous avez installé l'interface de ligne de commande cf, entrez la commande `cf apps` pour déterminer si votre
application est en cours d'exécution.
  
  
  
  
  
## La barre de menu supérieure de {{site.data.keyword.Bluemix_notm}} disparaît
{: #ts_topmenubar}

Il se peut que la barre de menu supérieure de {{site.data.keyword.Bluemix_notm}}
disparaisse lorsque vous redimensionnez votre fenêtre de navigateur, ou qu'elle n'apparaisse pas lorsque vous utilisez un périphérique mobile.


Lorsque vous diminuez la taille de votre fenêtre de navigateur ou lorsque
vous utilisez un périphérique mobile, la barre de menu supérieure de
{{site.data.keyword.Bluemix_notm}} disparaît. Dans ce cas, le menu tiroir latéral, affiché
sous la forme d'une icône représentant des lignes empilées, apparaît dans le coin supérieur gauche. 
{: tsSymptoms}

 

L'interface utilisateur
{{site.data.keyword.Bluemix_notm}} possède une conception réactive. Lorsque l'environnement
d'affichage change, la présentation de l'interface utilisateur
{{site.data.keyword.Bluemix_notm}} peut également changer. 
{: tsCauses}
 

Utilisez à la place le menu tiroir latéral dans le coin supérieur gauche.
{: tsResolve}








# Traitement des incidents liés à la gestion des applications
{: #managingapps}

Des problèmes d'ordre général liés à la gestion des applications peuvent survenir : par exemple, les applications ne peuvent pas être mises à
jour, les caractères codés sur deux octets ne sont pas affichés. Toutefois, dans de nombreux cas, ces problèmes peuvent être résolus en quelques opérations simples.
{:shortdesc}





## Impossible de faire passer les applications en mode débogage
{: #ts_debug}

Il se peut que vous ne puissiez pas activer le mode débogage si votre version de machine virtuelle Java
(JVM) est la version 8 ou antérieure. 


Après avoir sélectionné **Activer le débogage d'application**, les outils tentent de faire passer l'application en mode débogage. Le plan
de travail Eclipse entame alors une session de débogage. Lorsque les outils parviennent à activer le mode débogage, le statut de l'application Web
affiche `Mise à jour du mode`, `Développement`, et `Débogage`. 
{: tsSymptoms}

Par contre, si les outils ne parviennent pas à activer le mode débogage, le statut de l'application Web indique uniquement `Mise à jour du
mode` et `Développement`, sans afficher `Débogage`. Les outils peuvent également afficher le message d'erreur suivant dans la vue Console :

```
bluemixMgmgClient - ???? [pool-1-thread-1] .... ERREUR  --- ClientProxyImpl : Impossible de créer les connexions websocket pour MyWebProj
com.ibm.ws.cloudoe.management.client.exception.ApplicationManagementException: javax.websocket.DeploymentException: La requête HTTP d'initialisation de la connexion
WebSocket a échoué à com.ibm.ws.cloudoe.management.client.impl.ClientProxyImpl.onNewClientSocket(ClientProxyImpl.java:161)
à com.ibm.ws.cloudoe.management.client.impl.ClientProxyImpl$RunServerTask.run(ClientProxyImpl.java:267)
à java.util.concurrent.Executors$RunnableAdapter.call(Executors.java:522)
à java.util.concurrent.FutureTask.run(FutureTask.java:277)
à java.util.concurrent.ThreadPoolExecutor.runWorker(ThreadPoolExecutor.java:1153)
à java.util.concurrent.ThreadPoolExecutor$Worker.run(ThreadPoolExecutor.java:628)
à java.lang.Thread.run(Thread.java:785)
Provoquée par : javax.websocket.DeploymentException: La requête HTTP d'initialisation de la connexion WebSocket a échoué à
org.apache.tomcat.websocket.WsWebSocketContainer.connectToServer(WsWebSocketContainer.java:315)
à com.ibm.ws.cloudoe.management.client.impl.ClientProxyImpl.onNewClientSocket(ClientProxyImpl.java:158)
... 6 autres
Provoquée par : java.util.concurrent.TimeoutException
à org.apache.tomcat.websocket.AsyncChannelWrapperSecure$WrapperFuture.get(AsyncChannelWrapperSecure.java:505)
à org.apache.tomcat.websocket.WsWebSocketContainer.processResponse(WsWebSocketContainer.java:542)
à org.apache.tomcat.websocket.WsWebSocketContainer.connectToServer(WsWebSocketContainer.java:296)
... 7 autres
[2016-01-15 13:33:51.075] bluemixMgmgClient - ????  [pool-1-thread-1] .... ERREUR  --- ClientProxyImpl : Impossible de créer les connexions websocket pour
MyWebProj com.ibm.ws.cloudoe.management.client.exception.ApplicationManagementException: javax.websocket.DeploymentException: La requête HTTP d'initialisation de la
connexion WebSocket a échoué à com.ibm.ws.cloudoe.management.client.impl.ClientProxyImpl.onNewClientSocket(ClientProxyImpl.java:161)
à com.ibm.ws.cloudoe.management.client.impl.ClientProxyImpl$RunServerTask.run(ClientProxyImpl.java:267)
à java.util.concurrent.Executors$RunnableAdapter.call(Executors.java:522)
à java.util.concurrent.FutureTask.run(FutureTask.java:277)
à java.util.concurrent.ThreadPoolExecutor.runWorker(ThreadPoolExecutor.java:1153)
à java.util.concurrent.ThreadPoolExecutor$Worker.run(ThreadPoolExecutor.java:628)
à java.lang.Thread.run(Thread.java:785)
Provoquée par : javax.websocket.DeploymentException: La requête HTTP d'initialisation de la connexion WebSocket a échoué à
org.apache.tomcat.websocket.WsWebSocketContainer.connectToServer(WsWebSocketContainer.java:315)
à com.ibm.ws.cloudoe.management.client.impl.ClientProxyImpl.onNewClientSocket(ClientProxyImpl.java:158)
... 6 autres
Provoquée par : java.util.concurrent.TimeoutException
à org.apache.tomcat.websocket.AsyncChannelWrapperSecure$WrapperFuture.get(AsyncChannelWrapperSecure.java:505)
à org.apache.tomcat.websocket.WsWebSocketContainer.processResponse(WsWebSocketContainer.java:542)
à org.apache.tomcat.websocket.WsWebSocketContainer.connectToServer(WsWebSocketContainer.java:296)
... 7 autres
```
 

Les versions de machine virtuelle Java (JVM) suivantes ne peuvent pas établir une session de débogage : IBM JVM 7, IBM
JVM 8, et versions antérieures d'Oracle JVM 8.
{: tsCauses}

Si la machine virtuelle Java (JVM) de votre plan de travail relève de ces versions, vous pouvez rencontrer des problèmes lorsque vous créez une session de
débogage. La version de machine virtuelle Java de votre plan de travail est généralement celle de la JVM système de votre ordinateur local. Ce n'est pas la même que
celle de votre application Java Bluemix en exécution. L'application Java Bluemix opère presque toujours sur la JVM IBM, et parfois sur la JVM
OpenJDK.
  

Pour vérifier la version Java utilisée par IBM Eclipse Tools for Bluemix, procédez comme suit :
{: tsResolve}

  1. Dans IBM Eclipse Tools for Bluemix, sélectionnez **Aide** > **A propos d'Eclipse** > **Détails
de l'installation** > **Configuration**.
  2. Localisez la propriété `eclipse.vm` dans la liste. La ligne suivante est un exemple de propriété
`eclipse.vm` :
	
	```
	eclipse.vm=C:\Program Files\IBM\ibm-java-sdk-80-win-x86_64\bin\..\jre\bin\j9vm\jvm.dll
	```

  3. Sur la ligne de commande, entrez `java -version` depuis le répertoire `bin` de votre installation Java. Les
informations de version de votre JVM IBM s'affichent.

Si la machine virtuelle Java de votre plan de travail utilise la JVM 7 ou 8 d'IBM, ou une version antérieure à la JVM 8 d'Oracle 8, procédez comme suit pour
passer à la JVM 8 d'Oracle :

  1. Téléchargez et installez la JVM 8 d'Oracle. Voir
[Java SE Downloads](http://www.oracle.com/technetwork/java/javase/downloads/index.html){: new_window} pour plus d'informations.
  2. Redémarrez Eclipse.
  3. Vérifiez que la propriété `eclipse.vm` pointe sur votre nouvelle installation de la JVM 8 d'Oracle.







## Impossible d'effectuer les actions demandées
{: #ts_authority}

Il se peut que vous ne puissiez pas effectuer des actions si vous ne disposez pas des droits d'accès appropriés.

 

Lorsque vous essayez d'effectuer des actions pour une instance de service ou une instance d'application, vous ne pouvez pas effectuer les actions
demandées et l'un des messages d'erreur suivants s'affiche : 
{: tsSymptoms}

`BXNUI0514E: Vous n'êtes développeur dans aucun des espaces de l'organisation <nom_organisation>.`


`Erreur de serveur, code de statut : 403, code d'erreur 10003, message : vous n'êtes pas autorisé à effectuer l'action demandée.`

 

Vous ne disposez pas du niveau de droits approprié requis pour effectuer les actions. 
{: tsCauses}

  

Pour obtenir le niveau de droits approprié, appliquez l'une des méthodes suivantes : 
{: tsResolve}
 * Sélectionnez une autre organisation et un autre espace pour laquelle ou lequel vous disposez du rôle Développeur. 
 * Demandez au responsable de l'organisation de vous attribuer le rôle Développeur ou de créer un espace, puis de vous attribuer le rôle
Développeur. Voir [Gestion de vos organisations](../admin/orgs_spaces.html) pour des détails.
 

 


## Impossible d'accéder à des services {{site.data.keyword.Bluemix_notm}} en raison d'erreurs d'autorisation
{: #ts_vcap}

Des erreurs d'autorisation peuvent survenir lorsque votre application accède à un service {{site.data.keyword.Bluemix_notm}} si les données
d'identification du service sont codées en dur dans votre application. 

Une fois que vous avez configuré votre application pour qu'elle communique avec un service {{site.data.keyword.Bluemix_notm}}, vous la
déployez dans {{site.data.keyword.Bluemix_notm}}. Toutefois, vous ne pouvez pas utiliser l'application pour accéder au service
{{site.data.keyword.Bluemix_notm}} et recevez une erreur d'autorisation.
{: tsSymptoms}

Il se peut que les données d'identification codées en dur dans l'application ne soient pas correctes. A chaque fois que le service est recréé, les
données d'identification permettant d'y accéder changent.
{: tsCauses}


Au lieu de coder en dur les données d'identification dans votre application, utilisez les paramètres de connexion de la variable
d'environnement VCAP_SERVICES. Les méthodes d'utilisation des paramètres de connexion de la variable d'environnement VCAP_SERVICES varient selon les
langages de programmation. Par exemple, pour les applications Node.js, vous pouvez utiliser la commande suivante : 
{: tsResolve}

```
process.env.VCAP_SERVICES
```
Pour plus d'informations sur les commandes que vous pouvez utiliser dans d'autres langages de programmation, voir
[Java](http://docs.run.pivotal.io/buildpacks/java/java-tips.html#env-var){: new_window} et [Ruby](http://docs.run.pivotal.io/buildpacks/ruby/ruby-tips.html#env-var){: new_window}. 
 

 
 




## Impossibilité de déployer des applications à l'aide des outils IBM Eclipse pour
{{site.data.keyword.Bluemix_notm}}
{: #ts_bm_tools_facet}

Lorsqu'une facette non prise en charge est appliquée à votre projet Eclipse, il se peut que vous ne puissiez pas déployer vos applications dans {{site.data.keyword.Bluemix_notm}} à l'aide d'IBM Eclipse Tools for {{site.data.keyword.Bluemix_notm}}. 

 

Votre application peut être déployée avec succès dans
{{site.data.keyword.Bluemix_notm}} à l'aide de l'interface de ligne de commande Cloud Foundry. Toutefois, vous ne pouvez pas déployer
l'application dans {{site.data.keyword.Bluemix_notm}} avec IBM Eclipse Tools for {{site.data.keyword.Bluemix_notm}} et le message d'erreur
suivant s'affiche : `La facette de projet <nom_facette> n'est pas prise en charge.` Exemple : `La facette de projet Cloud
Foundry Standalone Application version 1.0 n'est pas prise en charge.`
{: tsSymptoms}

 

Les outils IBM Eclipse pour
{{site.data.keyword.Bluemix_notm}} mappent des projets vers les contextes d'exécution
{{site.data.keyword.Bluemix_notm}} par facettes de projet. Les facettes définissent les exigences des projets
Java EE dans Eclipse et sont utilisées dans le cadre de la configuration du contexte d'exécution pour que différents contextes d'exécution soient associés à
différents projets. Si la facette qui est appliquée au projet n'est pas prise en charge par IBM Eclipse Tools for
{{site.data.keyword.Bluemix_notm}}, il se peut que vous ne puissiez pas déployer votre application à l'aide d'IBM Eclipse Tools for
{{site.data.keyword.Bluemix_notm}}.
{: tsCauses}


Vous devez supprimer la facette du projet Eclipse pour pouvoir déployer
votre application à l'aide des outils IBM Eclipse pour {{site.data.keyword.Bluemix_notm}}.
{: tsResolve} 

Pour supprimer la
facette, dans les outils IBM Eclipse pour {{site.data.keyword.Bluemix_notm}}, cliquez sur
**Projet>Propriétés>Facettes de projet** pour le projet concerné. Décochez
ensuite la case correspondant à la facette non prise en charge. 



## Réception d'erreurs 502 Bad Gateway
{: #ts_502_error}

Si vous recevez des erreurs 502 Bad Gateway lorsque vous interagissez avec des applications
sur {{site.data.keyword.Bluemix_notm}},
consultez la page de statut {{site.data.keyword.Bluemix_notm}}
et exécutez les actions en conséquence.

 

Vous recevez des messages d'erreur commençant par 502 Bad Gateway. Exemple : `502 Bad Gateway: Registered endpoint failed to handle the
request.`
{: tsSymptoms}

 

Une erreur
Bad Gateway se produit généralement lorsque vous visitez un site Web qui utilise
un serveur proxy pour stocker et relayer les données provenant du serveur principal
hébergeant le site. Le serveur principal et le serveur proxy peuvent ne pas se
connecter correctement, déclenchant l'affichage du code d'état HTTP 502 dans votre
fenêtre de navigateur. Ce code d'état indique que le serveur principal du site n'a pas
reçu l'implémentation HTTP attendue du serveur proxy.
{: tsCauses}

D'autres raisons moins fréquentes pour une erreur Bad Gateway
sont les décrochages du fournisseur d'accès Internet, des configurations de pare-feu incorrectes et des erreurs de
cache du navigateur. 

 

Si vous suspectez l'arrêt d'un service {{site.data.keyword.Bluemix_notm}}, consultez d'abord la page
de [statut de {{site.data.keyword.Bluemix_notm}}](https://developer.ibm.com/bluemix/support/#status){: new_window}. Vous pouvez souhaiter utiliser le service en tant que solution palliative dans une autre région {{site.data.keyword.Bluemix_notm}}. Des informations détaillées sont disponibles à la section [Utilisation des services dans une autre région](../services/reqnsi.html#cross_region_service){: new_window}. Si le statut du service est normal, essayez la procédure suivante pour résoudre le problème : 
{: tsResolve}

  * Exécutez à nouveau l'action :
    * Rechargez la page en appuyant sur la touche F5 de votre clavier ou en cliquant sur le bouton d'actualisation. Si cette étape ne fonctionne pas,  videz le cache de votre navigateur et supprimez les cookies, puis essayez de recharger la page à nouveau.
	* Utilisez un navigateur différent.
	* Rallumez votre routeur, votre modem et votre ordinateur. Le réamorçage de ces
unités peut éliminer diverses erreurs à l'origine de l'erreur 502. 
  * Attendez et recommencez ultérieurement. Dans certaines instances, des problèmes temporaires peuvent se produire
avec votre fournisseur d'accès Internet ou les services {{site.data.keyword.Bluemix_notm}}. Vous pouvez attendre jusqu'à ce que les problèmes temporaires soient résolus.
  * Si le problème existe toujours, contactez le support {{site.data.keyword.Bluemix_notm}}. Voir [Contacter le support {{site.data.keyword.Bluemix_notm}}](../support/index.html#contacting-bluemix-support){: new_window} pour plus d'informations. 




## Dépassement du quota de disque
{: #ts_disk_quota}

Si votre espace disque est insuffisant, vous pouvez modifier manuellement le quota de disque
pour obtenir de l'espace disque supplémentaire.

  

Lorsque votre espace disque devient insuffisant, un message indiquant que le quota de disque est dépassé peut s'afficher. Pour résoudre le problème,
vous pouvez tenter d'augmenter votre instance d'application pour obtenir davantage
d'espace disque. Par exemple, vous pouvez passer de 256 Mo à 1256 Mo en modifiant le quota de
mémoire sur la page de détails de l'application. Cependant, comme le quota de disque
est resté le même, vous n'avez pas obtenu plus d'espace disque. 
{: tsSymptoms}


Le quota de disque par défaut alloué à une application est de  1 Go. Si vous avez besoin de davantage d'espace disque, vous devez spécifier manuellement le quota de disque. 
{: tsCauses}

 
Utilisez l'une des méthodes suivantes pour spécifier votre quota de disque. Le quota de disque maximal que vous pouvez spécifier est de 2 Go. Si les 2 Go ne sont toujours pas suffisants, essayez un service externe
tel que [Object Store](../services/ObjectStorage/index.html){: new_window}.
{: tsResolve}

  * Dans le fichier manifest.yml, ajoutez l'élément suivant :
    ```
	disk_quota: <quota_disque>
	```
  * Utilisez l'option **-k** avec la commande `cf push` lorsque vous exécutez une commande push sur votre
application dans {{site.data.keyword.Bluemix_notm}} :
    ```
	cf push nom_app -p chemin_app -k <quota_disque>
	```

	
	
## Impossibilité d'ajouter un référentiel Git
{: #ts_cannot_addgit}

Après avoir créé une application dans le tableau de bord, vous cliquez sur Ajouter un référentiel Git afin de créer un référentiel Git, mais vous ne
pouvez pas continuer.



Lorsque vous cliquez sur **Ajouter un référentiel Git**,
une fenêtre s'ouvre et l'un des problèmes suivants survient :
{: tsSymptoms} 

  * La fenêtre est bloquée et affiche un écran blanc.
  * Un message signale qu'un problème lié à des cookies tiers existe.



Il se peut que votre navigateur soit configuré de sorte à empêcher la
définition d'un cookie. Ce cookie doit être défini depuis le site IBM® Bluemix DevOps Services dans le domaine Internet hub.jazz.net, dans le contexte de
la console {{site.data.keyword.Bluemix_notm}}.
{: tsCauses}  

 

Pour résoudre ce problème, procédez de l'une des manières suivantes :
{: tsResolve}

  * Suivez les instructions figurant dans la fenêtre qui s'ouvre depuis la console
{{site.data.keyword.Bluemix_notm}}. Cliquez sur le bouton. Une autre fenêtre de navigateur s'ouvre
provisoirement. Dans cette fenêtre, DevOps Services définit le cookie d'authentification.
  * Dans un autre onglet de navigateur, accédez à https://hub.jazz.net et connectez-vous. Revenez à la console {{site.data.keyword.Bluemix_notm}} et actualisez la page. Cliquez sur
**Ajouter un référentiel Git** à nouveau.
  * Changez les paramètres de votre navigateur pour autoriser les cookies tiers et cliquez sur Ajouter un référentiel Git à nouveau. Pour des détails sur la configuration des paramètres, voir la documentation de votre navigateur :
    * [Mozilla Firefox](https://support.mozilla.org/en-US/kb/enable-and-disable-cookies-website-preferences#w_how-do-i-change-cookie-settings){: new_window}
	* [Google
Chrome](https://support.google.com/chrome/answer/95647){: new_window}
	* [Apple Safari](https://support.apple.com/kb/PH17191){: new_window}
	* [Microsoft Internet
Explorer](http://windows.microsoft.com/en-us/internet-explorer/delete-manage-cookies#ie=ie-11){: new_window} Si ces solutions de contournement ne résolvent pas le problème, envoyez un courrier électronique à idslogin@jazz.net.



## Impossibilité de recevoir des notifications push pour les applications Android
{: #ts_push}

Dans certaines régions où Google n'est pas accessible, les applications Android
ne peuvent pas recevoir les notifications que vous envoyez via le service push d'IBM. Dans ce cas, vous pouvez utiliser des services de tiers comme solution palliative.

 

Vous liez un service push pour votre application Bluemix et envoyez un message aux unités enregistrées. Toutefois, les applications qui sont
développées sur la plateforme Android ne peuvent pas recevoir vos notifications
dans certaines régions. 
{: tsSymptoms}

 
Le service push IBM utilise le service de messagerie basée sur le cloud de Google  (GCM) pour transmettre les notifications aux applications mobiles développées sur la plateforme Android. Les applications mobiles doivent pouvoir accéder au service GCM pour que les applications Android puissent recevoir les notifications. Dans
les régions où le service GCM n'est pas accessible aux applications Android, ces applications ne peuvent pas recevoir de notifications push.
{: tsCauses}

 
Utilisez des services de tiers qui ne sont pas basés sur le service GCM comme solution palliative, par exemple [Pushy](https://pushy.me){: new_window}, [igetui](http://www.getui.com/){: new_window} et [jpush](https://www.jpush.cn/){: new_window}.
{: tsResolve}



## La limite des services de l'organisation est atteinte
{: #ts_servicelimit}

Si vous possédez un compte d'essai, il se peut que vous ne puissiez pas créer d'application dans
{{site.data.keyword.Bluemix_notm}} si vous avez atteint le nombre maximal de services pour
votre organisation.
 

Lorsque vous tentez de créer une application dans {{site.data.keyword.Bluemix_notm}}, le message d'erreur suivant s'affiche : 
{: tsSymptoms}

`BXNUI2032E: La ressource <instance_service> n'a pas été créée. Une erreur est survenue lors du contact de Cloud Foundry pour la création d'une ressource. Message Cloud
Foundry : "You have exceeded your organization's services limit."`



Cette erreur survient lorsque vous avez atteint le nombre maximal d'instances
de service dont vous pouvez disposer pour votre compte. Le nombre maximal d'instances de service pour un compte d'essai est 10.
{: tsCauses} 

 

Supprimez les instances de service dont vous n'avez pas besoin ou
supprimez la limite relative au nombre d'instances de service dont vous pouvez disposer.
{: tsResolve}
 
  * Pour supprimer une instance de service, vous pouvez utiliser l'interface utilisateur
{{site.data.keyword.Bluemix_notm}} ou l'interface de ligne de commande.
    Pour utiliser l'interface utilisateur {{site.data.keyword.Bluemix_notm}} afin de supprimer une instance de service, procédez comme suit :
	  1. Dans le tableau de bord {{site.data.keyword.Bluemix_notm}}, cliquez sur **Services** dans le panneau de gauche. Les vignettes des services s'affichent. 
	  2. Sur la vignette du service à supprimer, cliquez sur l'icône **Menu**.
	  3. Cliquez sur **Supprimer le service**. Une fois l'instance de service supprimée, vous êtes invité à reconstituer l'application à
laquelle l'instance de service était liée. 
    Pour utiliser l'interface de ligne de commande afin de supprimer une instance de service, procédez comme suit :
	  1. Supprimez la liaison de l'instance de service à une application en entrant `cf
unbind-service <nom_app> <nom_instance_service>`.
	  2. Supprimez l'instance de service en entrant `cf delete-service
<nom_instance_service>`.
	  3. Une fois l'instance de service supprimée, vous pouvez reconstituer l'application à laquelle l'instance de service était liée en entrant
`cf restage <nom_app>`.
  * Pour supprimer la limite relative au nombre d'instances de service dont vous pouvez disposer, convertissez votre compte d'essai en compte
payant. Pour des informations sur la conversion de votre compte d'essai en compte payant, voir [Comment
changer votre plan ?](../pricing/index.html#changing){: new_window}.

  
  
## Des fichiers exécutables ne peuvent pas être exécutés dans {{site.data.keyword.Bluemix_notm}}
{: #ts_executable}

Il peut être impossible d'exécuter des fichiers exécutables dans {{site.data.keyword.Bluemix_notm}}
si ces fichiers ont été développés et générés dans un environnement différent. 

 

Vous ne parvenez pas à exécuter des fichiers exécutables dans
{{site.data.keyword.Bluemix_notm}} lorsque ceux-ci ont été développés et générés dans un environnement différent.
{: tsSymptoms}

 

Si le contenu à envoyer par commande push dans
{{site.data.keyword.Bluemix_notm}} est déjà un fichier exécutable, il a déjà été généré et il n'est pas
nécessaire de le générer dans {{site.data.keyword.Bluemix_notm}}. Dans ce cas, aucun pack de construction n'est requis pour l'exécution du fichier exécutable dans {{site.data.keyword.Bluemix_notm}}. Toutefois,
vous devez indiquer explicitement à {{site.data.keyword.Bluemix_notm}} qu'aucun pack de construction n'est
nécessaire.
{: tsCauses}

 

Lorsque vous envoyez par commande push le fichier exécutable dans
{{site.data.keyword.Bluemix_notm}}, vous devez spécifier la valeur null-buildpack, qui indique qu'aucun pack de
construction n'est requis. Spécifiez la valeur null-buildpack avec l'option **-b** dans la commande `cf push` :
{: tsResolve}

```
cf push nom_app -p <chemin_app> -c <commande_démarrage> -b <null-buildpack>
```
Par exemple :
```
cf push nom_app -p <chemin_app> -c ./RunMeNow -b https://github.com/ryandotsmith/null-buildpack
```


## La limite de mémoire de l'organisation a été atteinte
{: #ts_outofmemory}

Si vous possédez un compte d'essai, il se peut que vous ne puissiez pas déployer une application dans {{site.data.keyword.Bluemix_notm}} si
vous avez
atteint la limite de mémoire définie pour votre organisation. Vous pouvez réduire la quantité de mémoire que vos applications utilisent ou augmenter le quota de mémoire de votre compte. 



Lorsque vous déployez une application dans {{site.data.keyword.Bluemix_notm}}, le message d'erreur suivant s'affiche :
{: tsSymptoms} 

`FAILED Server error, status code: 400, error code: 100005, message: You have exceeded your organization's memory limit.`

 

Cette erreur survient lorsque la quantité de mémoire restante pour votre organisation est inférieure à la quantité de mémoire requise par
l'application à déployer. Le quota de mémoire maximal pour un compte d'essai est 2 Go.
{: tsCauses}



Vous pouvez augmenter le quota de mémoire de votre compte ou réduire la mémoire que vos applications utilisent.
{: tsResolve} 

  * Pour augmenter le quota de mémoire de votre compte, convertissez votre compte d'essai en compte payant. Pour des informations sur la conversion
de votre compte d'essai en compte payant, voir [Comptes payants](../pricing/index.html#pay-accounts){: new_window}. 
  * Pour réduire la quantité de mémoire que vos applications utilisent, servez-vous de l'interface utilisateur {{site.data.keyword.Bluemix_notm}} ou
de l'interface de ligne de commande cf.
    Si vous employez l'interface utilisateur {{site.data.keyword.Bluemix_notm}}, procédez comme suit :
	  1. Dans le tableau de bord {{site.data.keyword.Bluemix_notm}}, sélectionnez votre application. La page des détails de l'application
s'ouvre.
	  2. Dans le panneau Contexte d'exécution, vous pouvez réduire la limite de mémoire maximal ou le nombre d'instances d'application, ou les deux,
pour votre application. 
	Si vous utilisez l'interface de ligne de commande cf, procédez comme suit :
	  1. Vérifiez la quantité de mémoire qui est utilisée par vos applications :
	  ```
	  cf apps
	  ```
	     La commande cf apps répertorie toutes les applications que vous avez déployées dans votre espace en cours. Le statut de chaque application est
également affiché.
      2. Pour réduire la quantité de mémoire qui est utilisée par votre application, réduisez le nombre d'instances d'application ou la limite de
mémoire
maximale, ou les deux :
	  ```
	  cf push <nom_app> -p <chemin_app> -i <nombre_instances> -m <limite_mémoire>
      ```
	  3. Redémarrez votre application pour que les modifications soient appliquées.



	  
## Les applications ne sont pas redémarrées automatiquement
{: #ts_apps_not_auto_restarted}


Une application n'est pas redémarrée automatiquement lorsqu'un service que vous liez à l'application s'arrête de fonctionner.	  
	  
 

Lorsqu'un service que vous liez à une application tombe en panne, des problèmes tels que des indisponibilités, des exceptions et des échecs de
connexion peuvent survenir sur l'application. {{site.data.keyword.Bluemix_notm}} ne redémarre pas automatiquement l'application pour assurer la
reprise suite à ces problèmes.
{: tsSymptoms}



Ce comportement est normal dans Cloud Foundry.
{: tsCauses} 

 

Vous pouvez redémarrer manuellement l'application en entrant la commande suivante dans l'interface de ligne de commande :
{: tsResolve}

```
cf push <nom_app> -p <chemin_app>
```
De plus, vous pouvez coder l'application afin d'identifier les problèmes et d'assurer la reprise après une indisponibilité, une exception ou un échec de
connexion. 

	  

## Les variables définies par l'utilisateur sont perdues lorsqu'une application est envoyée par commande push
{: #ts_varsnotretained}

Lorsque vous envoyez une application par commande push à {{site.data.keyword.Bluemix_notm}} depuis IBM Eclipse Tools for
{{site.data.keyword.Bluemix_notm}}, les variables que vous spécifiez sont réinitialisées sauf si vous les sauvegardez dans le fichier manifeste.



Les variables que vous spécifiez sont perdues une fois que vous avez envoyé une application par commande push à
{{site.data.keyword.Bluemix_notm}} depuis IBM Eclipse Tools for {{site.data.keyword.Bluemix_notm}}.
{: tsSymptoms} 


Les variables que vous spécifiez ne sont sauvegardées que si vous les
sauvegardez dans le fichier manifeste.
{: tsCauses} 

 

Lorsque vous envoyez une application par commande push à {{site.data.keyword.Bluemix_notm}} depuis IBM Eclipse Tools for
{{site.data.keyword.Bluemix_notm}}, sélectionnez la case à cocher **Save to the manifest file** dans la page des détails
de l'application de l'assistant Application. Ainsi, les variables que vous
spécifiez dans l'assistant sont sauvegardées dans le fichier manifeste de votre application. A la prochaine ouverture de l'assistant, elles seront
affichées automatiquement.
{: tsResolve}



## Les icônes de {{site.data.keyword.Bluemix_notm}} Live Sync ne s'affichent pas
{: #ts_llz_lkb_3r}

Vous avez créé une application dans IBM Bluemix DevOps Services, mais les icônes d'IBM Bluemix Live Sync ne s'affichent pas dans l'environnement de
développement intégré Web.

 

Lorsque vous éditez une application Node.js dans l'environnement de développement intégré Web DevOps Services, les icônes {{site.data.keyword.Bluemix_notm}} d'édition directe, de redémarrage rapide et de débogage ne s'affichent pas.
{: tsSymptoms}

 

Les icônes ne sont pas disponibles dans les cas suivants :
{: tsCauses}

  * Le fichier `manifest.yml` n'est pas stocké au niveau supérieur de votre projet.
  * Votre application est stockée dans un sous-répertoire plutôt qu'au niveau supérieur de votre projet, mais le chemin d'accès au sous-répertoire n'est
pas spécifié dans le fichier `manifest.yml`.
  * L'application ne contient pas de fichier `package.json`.


Utilisez l'une des méthodes suivantes pour résoudre le problème : 
{: tsResolve} 

  * Si le fichier `manifest.yml` n'est pas stocké au niveau supérieur de votre projet, stockez-le au niveau supérieur.
  * Si votre application est stockée dans un sous-répertoire, spécifiez le chemin d'accès au sous-répertoire dans le fichier
`manifest.yml`.
  ```
   path: chemin_application
   ```
  * Créez un fichier `package.json` dans le répertoire dans lequel se trouve votre application.

  
  
  

  
  

  
  
## Des organisations sont introuvables dans {{site.data.keyword.Bluemix_notm}}
{: #ts_orgs}

Il se peut que vous ne parveniez pas à localiser votre organisation dans
{{site.data.keyword.Bluemix_notm}} lorsque vous travaillez sur une région
{{site.data.keyword.Bluemix_notm}}.
  
 

Vous pouvez vous connecter à l'interface utilisateur {{site.data.keyword.Bluemix_notm}}, mais vous ne parvenez pas à envoyer vos applications par commande push à l'aide de
l'interface de ligne de commande cf ou du plug-in Eclipse.
{: tsSymptoms}

Lorsque vous essayez d'envoyer une application par commande push
à {{site.data.keyword.Bluemix_notm}} en utilisant l'interface de ligne de commande cf, l'un des messages
d'erreur
suivants, qui spécifie le nom de l'organisation, s'affiche : 

`Erreur lors de la recherche de l'organisation`

`Organization not found`


Lorsque vous essayez d'envoyer une application par commande push à
{{site.data.keyword.Bluemix_notm}} en utilisant le plug-in Eclipse Cloud Foundry, le message d'erreur suivant
s'affiche :

`cloudspace not found.`



Ce problème survient car le noeud final d'API de la région avec laquelle
vous travaillez n'est pas spécifié et l'organisation que vous recherchez peut se trouver dans une autre région.
{: tsCauses} 

   
  
Si vous envoyez votre application par commande push à {{site.data.keyword.Bluemix_notm}} en utilisant l'interface de ligne de commande cf, entrez la commande cf api et spécifiez le noeud final d'API de la région. Par exemple, entrez la commande suivante pour vous connecter à la
région {{site.data.keyword.Bluemix_notm}} Europe et Royaume-Uni :
{: tsResolve}

```
cf api https://api.eu-gb.bluemix.net
```
Si vous envoyez votre application par commande push à
{{site.data.keyword.Bluemix_notm}} en utilisant les outils Eclipse, vous devez d'abord créer un serveur
{{site.data.keyword.Bluemix_notm}} et spécifier le noeud final d'API de la région
{{site.data.keyword.Bluemix_notm}} dans laquelle votre organisation a été créée. Pour plus d'informations sur l'utilisation des outils Eclipse, voir
[Déploiement d'applications avec IBM Eclipse Tools for
Bluemix](../manageapps/eclipsetools/eclipsetools.html){: new_window}.
  
  


## La route d'application ne peut pas être créée
{: #ts_hostistaken}

Lorsque vous déployez une application dans {{site.data.keyword.Bluemix_notm}}, la route d'application ne peut pas être créée si le nom d'hôte
que
vous avez spécifié est déjà utilisé.



Lorsque vous déployez une application dans {{site.data.keyword.Bluemix_notm}}, le message d'erreur suivant s'affiche : 
{: tsSymptoms} 

`Creating route nom_hôte.nom_domaine ... FAILED Server error, status code: 400, error code: 210003, message: The host is taken:
nom_hôte`



Ce problème survient si le nom d'hôte que vous avez spécifié est déjà utilisé.
{: tsCauses} 


  
Le nom d'hôte que vous spécifiez doit être unique dans le domaine que vous
utilisez. Pour spécifier un autre nom d'hôte, utilisez l'une des méthodes suivantes :
{: tsResolve} 

  * Si vous déployez votre application avec le fichier `manifest.yml`, spécifiez le nom d'hôte dans l'option host.	 
    ```
    host: <nom_hôte>	
	```
  * Si vous déployez votre application depuis l'invite de commande, utilisez la commande `cf
push` avec l'option **-n**. 
    ```
    cf push <nom_app> -p <chemin_app> -n <nom_hôte>
    ```


## Une application WAR ne peut pas être envoyée par l'intermédiaire de la commande cf push
{: #ts_cf_war}

Il est possible que vous ne puissiez pas utiliser la commande cf push pour déployer une application Web archivée dans {{site.data.keyword.Bluemix_notm}} si l'emplacement de
l'application
n'est pas spécifié correctement.
	


Lorsque vous téléchargez une application WAR dans {{site.data.keyword.Bluemix_notm}} par l'intermédiaire de la commande `cf push`, le message d'erreur `Staging error: cannot get
instances since staging failed` s'affiche.
{: tsSymptoms} 

 

Ce problème peut se produire si le fichier WAR ou le chemin d'accès à ce fichier n'est pas spécifié. 
{: tsCauses}

 	
	
Utilisez l'option **-p** pour spécifier un fichier WAR ou ajouter un chemin d'accès. Par exemple :
{: tsResolve}

```
cf push MonNomAppUnique01 -p app.war
```

```
cf push MonNomAppUnique02 -p "./app.war"
```
Pour plus d'informations sur la commande `cf push`, entrez `cf push -h`. 	





## Les caractères codés sur deux octets ne s'affichent pas correctement lorsque les applications Liberty sont envoyées par commande push vers {{site.data.keyword.Bluemix_notm}}
{: #ts_doublebytes}

Il se peut que les caractères codés sur deux octets ne s'affichent pas correctement si la prise en charge Unicode n'est pas configurée correctement pour le servlet ou les fichiers JSP.

 

Lorsqu'une application Liberty est envoyée par commande push dans {{site.data.keyword.Bluemix_notm}}, les caractères codés sur deux octets
spécifiés dans l'application ne s'affichent pas correctement.
{: tsSymptoms}

 

Le problème peut se produire si la prise en charge Unicode n'est pas configurée correctement pour le servlet ou les fichiers JSP.
{: tsCauses}


Utilisez le code suivant dans votre servlet ou votre fichier JSP :
{: tsResolve} 

  * Dans le fichier source servlet 
    ```
	response.setContentType("text/html; charset=UTF-8");
	```
  * Dans le fichier JSP 
    ```
	<meta http-equiv="Content-Type" content="text/html; charset=UTF-8" />
	```
	
	
	

## Les applications Node.js ne peuvent pas être déployées
{: #ts_nodejs_deploy}

Des problèmes peuvent survenir lorsque vous mettez à jour ou déployez une application Node.js dans {{site.data.keyword.Bluemix_notm}}.



Lorsque vous mettez à jour une application Node.js ou déployez votre application
Node.js dans {{site.data.keyword.Bluemix_notm}}, l'un des messages d'erreur suivants peut s'afficher :
{: tsSymptoms} 

`An app was not successfully detected by any available buildpack.`


`Instance (index 0) failed to start accepting connections.`


`Cannot get instances since staging failed.`


 

Les causes possibles du problème sont les suivantes :
{: tsCauses}
 
  * La commande de démarrage n'est pas spécifiée.
  * Les fichiers requis pour déployer une application Node.js manquent dans l'application ou se trouvent dans un dossier autre que le répertoire racine.
  


	
Effectuez les opérations suivantes en fonction de l'origine du problème :
{: tsResolve} 

  * Spécifiez la commande de démarrage en appliquant l'une des méthodes suivantes : 
      * Utilisez l'interface de ligne de commande cf. Par exemple : 
        ```
		cf push MonNoeudJsUnique01 -p chemin_app -c "node app.js"
		```
	  * Utilisez le fichier [package.json](https://docs.npmjs.com/json){: new_window}. Exemple :
	    ```
		{
      ...
  	   "scripts": {
	 		 "start": "node app.js"
 	   }
	}
	    ```
	  * Utilisez le fichier `manifest.yml`. Exemple : 
	    ```
		applications:
  name: MonNoeudJsUnique01
  ...
  command: node app.js
  ...
        ```

  * Vérifiez qu'un fichier `package.json` existe dans votre application Node.js pour que le pack de construction Node.js puisse reconnaître
l'application. De plus, vous devez placer ce fichier dans le répertoire racine de votre application.	
    L'exemple suivant illustre un fichier `package.json` simple :  
	```
	{
        "name": "MonNoeudJsUnique01",
        "version": "0.0.1",
        "description": "Exemple de fichier package.json",
        "dependencies": {
                "express": "3.4.x",
                "jade": "1.1.x"
        },
        "engines": {
                "node": "0.10.x"
        },
        "scripts": {
                  "start": "node app.js"
        }
 }
    ```
	
Pour d'autres conseils relatifs aux applications Node.js, voir [Tips for Node.js Applications](http://docs.cloudfoundry.org/buildpacks/node/node-tips.html){: new_window}.	




## Des erreurs de configuration apparaissent dans le fichier `server.xml` après l'importation d'une application
{{site.data.keyword.Bluemix_notm}} Liberty depuis Bluemix DevOps Services dans Eclipse
{: #ts_eclipse}

Si des erreurs de configuration apparaissent dans le fichier `server.xml` après l'importation d'une application
{{site.data.keyword.Bluemix_notm}} Liberty depuis IBM Bluemix DevOps Services dans Eclipse, il peut être nécessaire de retirer le fichier
`server.xml` du projet. 

 

Après avoir importé une application {{site.data.keyword.Bluemix_notm}} Liberty depuis {{site.data.keyword.Bluemix_notm}}
DevOps Services dans Eclipse, vous constatez que le fichier `server.xml` contient des erreurs de configuration dans la vue Erreurs
d'Eclipse. 
{: tsSymptoms}

 

Le pack de construction Liberty utilise le fichier `server.xml` pour configurer l'application et génère un fichier
`runtime-vars.xml` lorsque l'application Liberty est envoyée par commande push dans {{site.data.keyword.Bluemix_notm}}. Lorsque
vous importez l'application dans Eclipse, le fichier `runtime-vars.xml` n'existe pas dans votre environnement local.
{: tsCauses}

 

Pou résoudre ce problème, supprimez le fichier server.xml du projet. Le pack de construction crée le fichier `server.xml` de manière
dynamique lorsque vous envoyez par commande push l'application sous forme d'application WAR. Pour plus d'informations, voir [Liberty for Java](../runtimes/liberty/index.html){: new_window}.
{: tsResolve}
	
	
## Une application ne peut pas être constituée avec un pack de construction personnalisé
{: #ts_bp_compilation}

Il se peut que vous ne puissiez pas déployer une application dans {{site.data.keyword.Bluemix_notm}} à l'aide d'un pack de construction
personnalisé, si les scripts que ce dernier contient ne sont pas exécutables.



Lorsque vous déployez une application dans {{site.data.keyword.Bluemix_notm}} à l'aide d'un pack de construction
personnalisé, le message d'erreur `La constitution de l'application
a échoué ; par conséquent, il n'y a pas d'instance à afficher` s'affiche.
{: tsSymptoms} 


Ce problème peut se produire si des scripts (tels que le script de détection, le script de compilation ou le script de publication) ne sont pas exécutables.
{: tsCauses}

 

Vous pouvez utiliser la commande
[git update](http://git-scm.com/docs/git-update-index){: new_window} pour activer le droit
d'exécution pour chaque script. Par exemple, vous pouvez entrer `git update --chmod=+x script.sh`.
{: tsResolve}
	
	
	
## Une application ne peut pas être déployée depuis DevOps Services dans {{site.data.keyword.Bluemix_notm}}
{: #ts_devops_to_bm}

Il se peut que vous ne puissiez pas envoyer votre application par commande push depuis IBM Bluemix DevOps
Services dans {{site.data.keyword.Bluemix_notm}} si le fichier `manifest.yml` n'est pas présent dans votre application.

 

Lorsque vous déployez une application depuis DevOps Services vers {{site.data.keyword.Bluemix_notm}}, le message d'erreur `Unable to
detect a supported application type` peut s'afficher.
{: tsSymptoms}

 

Ce problème peut survenir car DevOps Services requiert un fichier `manifest.yml` pour le déploiement d'une application dans {{site.data.keyword.Bluemix_notm}}.
{: tsCauses}

 

Pour remédier à ce problème, vous devez créer un fichier `manifest.yml`. Pour plus d'informations sur la création du fichier `manifest.yml`, voir [Manifeste d'application](../manageapps/depapps.html#appmanifest){: new_window}.
{: tsResolve}	
	




## Les applis Meteor ne peuvent pas être envoyées par commande push
{: #ts_meteor}

Il se peut que vous ne puissiez pas envoyer une application Meteor par commande push dans
{{site.data.keyword.Bluemix_notm}} si le pack de construction n'est pas spécifié correctement.

 

Lorsque vous déployez une appli Meteor dans {{site.data.keyword.Bluemix_notm}}, il se peut que le message d'erreur `La constitution de l'application a échoué ; par conséquent, il n'y a
pas d'instance à afficher` s'affiche.
{: tsSymptoms}


Ce problème survient car aucun pack de construction n'est fourni pour les applications Meteor. Vous devez utiliser un pack de construction personnalisé.
{: tsCauses} 


 

Afin d'utiliser un pack de construction personnalisé pour les applications Meteor, appliquez l'une des méthodes suivantes :
{: tsResolve}

  * Si vous déployez votre application avec le fichier `manifest.yml`, spécifiez l'adresse URL ou le nom de votre pack de construction personnalisé
avec l'option buildpack. Par exemple :
  ```
  buildpack: https://github.com/Sing-Li/bluemix-bp-meteor 
  ```
  * Si vous déployez votre application depuis l'invite de commande, utilisez la commande `cf
push` et spécifiez votre pack de construction personnalisé avec l'option **-b**. Par exemple :
    ```
	cf push nom_app -p chemin_app -b https://github.com/Sing-Li/bluemix-bp-meteor 
	```
	
  

    
## Le bouton Déployer dans {{site.data.keyword.Bluemix_notm}} ne déploie pas d'application
{: #deploytobluemixbuttondoesntdeployanapp}

Si vous cliquez sur le bouton Déployer dans {{site.data.keyword.Bluemix_notm}} et constatez que le
référentiel Git n'est pas cloné ou que l'application n'est pas déployée, essayez les méthodes de traitement des incidents proposées pour les problèmes
ci-après.
  * [Le projet Bluemix DevOps Services ne peut pas être créé](#project-cannot-be-created)
  * [Le référentiel Git est introuvable et ne peut pas être cloné dans DevOps Services](#repo-not-found)
  * [Le référentiel Git est cloné dans DevOps Services, mais l'application n'est pas déployée dans {{site.data.keyword.Bluemix_notm}}](#repo-cloned-app-not-deployed)
Pour plus d'informations sur la création du bouton, voir Création d'un bouton Déployer dans {{site.data.keyword.Bluemix_notm}}.

### Le projet Bluemix DevOps Services ne peut pas être créé
{: #project-cannot-be-created}

Si vous constatez que le projet DevOps Services ne peut pas être créé, cela peut signifier que votre compte IBM {{site.data.keyword.Bluemix_notm}} est arrivé à expiration.



Vous cliquez sur le bouton **Déployer dans Bluemix**, mais l'étape "Création du projet" n'aboutit pas.
{: tsSymptoms} 


Il se peut que votre compte
{{site.data.keyword.Bluemix_notm}} soit arrivé à expiration.
{: tsCauses} 

Utilisez l'une des méthodes suivantes pour résoudre le problème :
{: tsResolve}

  * Connectez-vous à {{site.data.keyword.Bluemix_notm}} et mettez à jour les informations relatives à votre
compte.
  * Cliquez à nouveau sur le bouton **Déployer dans Bluemix**.


### Le référentiel Git est introuvable et ne peut pas être cloné dans DevOps Services
{: #repo-not-found}

Si vous constatez que le référentiel Git n'est pas cloné, il peut y avoir un problème lié au référentiel ou au fragment du bouton.



Vous cliquez sur le bouton **Déployer dans Bluemix**, mais le référentiel Git est introuvable et ne peut pas être cloné dans DevOps Services. L'étape "Clonage du référentiel n'aboutit pas. Par conséquent, l'application ne peut pas être déployée dans {{site.data.keyword.Bluemix_notm}}. 
{: tsSymptoms} 

Ce problème peut survenir pour l'une des raisons suivantes :
{: tsCauses} 

  * Il se peut que le référentiel Git n'existe pas ou ne soit pas accessible.
  * Il peut y avoir un problème dans le code HTML ou Markdown du fragment du bouton.
  * Il se peut que les caractères spéciaux, les paramètres de requête ou les fragments dans l'adresse URL empêchent l'accès au référentiel Git.

Utilisez l'une des méthodes suivantes pour résoudre le problème :
{: tsResolve}

  * Vérifiez que votre référentiel Git existe, qu'il est accessible publiquement, et que l'adresse URL est correcte.
  * Vérifiez que le fragment ne contient pas d'erreur HTML ou Markdown.
  * Si des caractères spéciaux, des paramètres de requête ou des fragments génèrent un problème lié à l'adresse URL du référentiel Git, codez
l'adresse URL dans le fragment du bouton.
  

  
  
### Le référentiel Git est cloné dans DevOps Services, mais l'application n'est pas déployée dans {{site.data.keyword.Bluemix_notm}}
{: #repo-cloned-app-not-deployed}

Si vous constatez que l'application n'est pas déployée, il se peut que le code dans le référentiel contienne des erreurs.
     


Vous cliquez sur le bouton **Déployer dans Bluemix** et le référentiel Git est cloné dans DevOps Services, mais l'application n'est pas déployée dans {{site.data.keyword.Bluemix_notm}}. L'étape "Déploiement dans Bluemix" n'aboutit pas.
{: tsSymptoms} 

Ce problème peut survenir pour l'une des raisons suivantes :
{: tsCauses}  

  * Il se peut que l'espace disponible dans votre espace {{site.data.keyword.Bluemix_notm}} ne soit pas
suffisant pour déployer une application. 
  * Il se peut qu'un service requis ne soit pas déclaré dans le fichier `manifest.yml`.
  * Il se peut qu'un service requis soit déclaré dans le fichier `manifest.yml` alors qu'il se trouve déjà dans l'espace cible.
  * Le code dans le référentiel peut comporter des erreurs.
Pour diagnostiquer le problème, consultez les journaux de génération et de
déploiement depuis le déploiement :
  1. Si l'étape "Déploiement dans Bluemix" n'aboutit pas, cliquez sur le lien à l'étape "Configuration du pipeline" précédente
pour ouvrir Delivery Pipeline.
  2. Identifiez l'étape de génération ou de déploiement ayant échoué.
  3. A l'étape ayant échoué, cliquez sur **Afficher les journaux et l'historique**.
  4. Localisez le message d'erreur.
   
Utilisez l'une des méthodes suivantes pour résoudre le problème :
{: tsResolve}

  * Si le message d'erreur indique que l'espace dans l'espace {{site.data.keyword.Bluemix_notm}} n'est pas
suffisant pour déployer l'application, ciblez un autre espace.
  * Si le message d'erreur indique qu'un service requis n'est pas déclaré dans le fichier `manifest.yml`, signalez au propriétaire du référentiel que
le service requis doit être ajouté.
  * Si le message d'erreur indique qu'un service requis existe déjà dans l'espace cible, sélectionnez un autre espace à utiliser.
  * Si le message d'erreur indique qu'il existe un problème lié à la génération, corrigez le problème dans le code qui empêche la génération de
l'application. Pour vérifier que le code ne présente pas d'erreur, générez-le avec des commandes Git :
    1. Clonez le référentiel Git :
    ```
    git clone <URL_référentiel_git>
    ```
	2. Ouvrez le répertoire de l'application :
	```
	cd <nom_app>
	```
	3. Créez l'application :
	```
	<nom_app> create
	```
	4. Si nécessaire, mettez à disposition des additifs.
	5. Ajoutez les variables de configuration requises.
	6. Envoyez le code par commande push :
	```
	git push <nom_app> master
	```
	7. Vérifiez que l'application est générée correctement :
	8. Si nécessaire, exécutez la commande postérieure au déploiement :
	```
	<nom_app> run
	```
	9. Ouvrez l'application et vérifiez qu'elle fonctionne correctement :
	```
	<nom_app> open
	```
	



# Traitement des incidents liés à la gestion des comptes
{: #managingaccounts}

Vous pouvez rencontrer des problèmes lorsque vous gérez votre compte : par exemple, différentes applications partagent le même nom de domaine, les
administrateurs ne peuvent pas afficher toutes les organisations. Toutefois, dans de nombreux cas, ces problèmes peuvent être résolus en quelques opérations simples.
{:shortdesc}


## Le compte est inactif
{: #ts_accnt_inactive}

Vous ne pouvez pas créer d'application dans {{site.data.keyword.Bluemix_notm}} si votre compte est inactif. Vous devez prendre contact avec
l'équipe de support pour résoudre ce problème.



Lorsque vous tentez de créer une application dans {{site.data.keyword.Bluemix_notm}}, le message d'erreur suivant s'affiche :
{: tsSymptoms} 

`BXNUI0096E: L'application n'a pas été créée. Votre compte est inactif car il a été annulé ou suspendu.`


Le statut de votre compte {{site.data.keyword.Bluemix_notm}} devient inactif lorsque le compte est annulé ou suspendu.
{: tsCauses}

 

Pour réactiver votre compte, prenez contact avec le [support {{site.data.keyword.Bluemix_notm}}](http://ibm.biz/bluemixsupport.com){: new_window}. Dans le courrier électronique, incluez les informations
suivantes :
{: tsResolve}

  * L'ID IBM que vous utilisez pour vous connecter à {{site.data.keyword.Bluemix_notm}}.
  * Le nom de l'organisation dans laquelle votre application est créée. Ces informations peuvent être utiles à l'équipe de support pour déterminer si l'appartenance ou les rôles appropriés vous ont été affectés dans votre organisation.



## Aucun espace n'est associé à l'organisation en cours
{: #ts_no_space}

Vous ne pouvez pas créer d'application si aucun espace n'est associé à votre organisation en cours.



Lorsque vous tentez de créer une application dans {{site.data.keyword.Bluemix_notm}}, le message d'erreur suivant s'affiche :
{: tsSymptoms} 


`BXNUI0097E: Pour qu'une application puisse être ajoutée, un espace au moins doit être associé à votre organisation et à votre région. Dans le tableau de bord, cliquez sur **Créer un espace**. Une fois l'espace créé, essayez à nouveau.`



Les applications dans {{site.data.keyword.Bluemix_notm}} doivent être créées dans un espace sous votre organisation.
{: tsCauses} 

 

Pour créer un espace, appliquez l'une des méthodes suivantes : 
{: tsResolve}
 
  * Dans le tableau de bord {{site.data.keyword.Bluemix_notm}}, sélectionnez l'organisation dans laquelle créer l'espace, puis cliquez sur **Créer un espace**.
  * Dans l'interface de ligne de commande cf, entrez ```cf create-space <nom_espace> -o
<nom_organisation>```.
  
  
  
  
## Les noms de domaine de plusieurs applications sont identiques
{: #ts_domain_diff}

Il se peut que plusieurs applications partagent la même adresse URL dans {{site.data.keyword.Bluemix_notm}}.

 

Ce problème peut se produire lorsque vous affectez la même route d'adresse URL à plusieurs applications dans un espace.
{: tsCauses}

Par exemple, vous envoyez par commande push l'application mon_App1 dans {{site.data.keyword.Bluemix_notm}} et définissez le nom de domaine
"manouvelleapp.mybluemix.net". 
Puis, vous envoyez par commande push une autre application mon_App2 dans le même espace et définissez l'une de ses routes d'URL sur
"manouvelleapp.mybluemix.net".
La route est désormais mappée aux deux applications.

 

Il s'agit du comportement de
{{site.data.keyword.Bluemix_notm}} pris en charge ; il permet d'obtenir un temps
d'indisponibilité nul
pour la mise à niveau de votre application. Pour plus d'informations, voir Déploiements Blue-Green.
{: tsResolve}
  
	
	





## La carte de crédit ne peut pas être ajoutée
{: #ts_addcc}

Vous ne pouvez pas soumettre vos informations de carte de crédit pour convertir votre compte d'essai en compte Paiement à la carte.

 

Le bouton Soumettre dans la page Ajouter une carte de crédit est désactivé.
{: tsSymptoms}

 

Ce problème survient lorsque vos informations ne sont pas remplies correctement dans la page Ajouter une carte de crédit.
{: tsCauses}

 

Procédez comme suit pour résoudre ce problème :
{: tsResolve}

  1. Dans la page Ajouter une carte de crédit, remplissez toutes les zones requises qui se trouvent dans les sections relatives aux coordonnées, à
l'adresse de contact et à l'adresse de facturation.
  2. Sélectionnez **I have read and agree to IBM's Terms and Conditions**, puis cliquez sur **Soumettre**. La
section **Select a payment method** s'affiche.
  3. Entrez votre numéro de carte de crédit, la date d'expiration de votre carte et le code de sécurité qui se trouve sur votre carte. Ensuite, cliquez sur
**Soumettre**.





# Traitement des incidents liés aux contextes d'exécution
{: #runtimes}

Vous pouvez rencontrer des problèmes lorsque vous utilisez les contextes d'exécution IBM® Bluemix.. Toutefois, dans de nombreux cas, ces problèmes peuvent être résolus en quelques opérations simples.
{:shortdesc}


## Pack de construction obsolète chargé à partir du cache lorsqu'une application est envoyée par commande push
{: #ts_loading_bp}


Il est possible que vous ne puissiez pas utiliser les derniers composants du pack de construction
lorsque vous envoyez une application par commande push. Vous pouvez utiliser des packs de construction disposant de mécanismes intégrés
pour empêcher le chargement de composants obsolètes ou supprimer le contenu du répertoire cache de votre application avant
de l'envoyer par commande push ou de la reconstituer. 

 

Lorsque vous envoyez une application par commande push ou que vous la reconstituez une fois le pack de construction mis à jour, les composants les plus récents du pack de construction ne sont pas automatiquement chargés. Par conséquent, votre application utilise les composants obsolètes du pack de construction. Les mises à jour qui ont été appliquées au pack de construction depuis le dernier envoi de l'application par commande push ne sont pas implémentées. 
{: tsSymptoms}



Certains packs de construction ne sont pas configurés pour télécharger automatiquement sur internet tous les composants mis à jour afin de vous assurer de toujours utiliser la version la plus récente.
{: tsCauses} 

 

Vous pouvez utiliser des packs de construction disposant de mécanismes intégrés pour éviter de charger des composants obsolètes. Exemples de packs de construction : 
{: tsResolve}

  * [Pack de construction Java Cloud Foundry](https://github.com/cloudfoundry/java-buildpack){: new_window}. Ce pack de construction comporte un mécanisme intégré qui permet de s'assurer d'utiliser la version la plus récente. Pour plus d'informations sur le fonctionnement de ce mécanisme, voir [extending-caches.md](https://github.com/cloudfoundry/java-buildpack/blob/master/docs/extending-caches.md){: new_window}. 
  * [Pack de construction Node.js Cloud Foundry](https://github.com/cloudfoundry/nodejs-buildpack){: new_window}. Ce pack de construction a une fonctionnalité similaire qui utilise des variables d'environnement. Pour permettre au pack de construction Node.js de télécharger des modules de noeud sur internet à chaque fois, entrez la commande suivante dans l'interface de ligne de commande cf : 	
  ```
  set NODE_MODULES_CACHE=false
  ```
Si le pack de construction que vous utilisez ne dispose pas d'un mécanisme permettant de charger automatiquement les composants les plus récents,  vous pouvez supprimer manuellement le contenu du répertoire cache et envoyer à nouveau votre application par commande push en procédant comme suit :
  1. Réservez une branche d'un pack de construction null, par exemple https://github.com/ryandotsmith/null-buildpack. Pour plus d'informations sur la réservation d'une branche, voir [Git Basics - Getting a Git Repository](http://www.git-scm.com/book/en/v2/Git-Basics-Getting-a-Git-Repository){: new_window}.  
  2. Ajoutez la ligne suivante au fichier `null-buildpack/bin/compile` et validez les modifications. Pour plus d'informations sur la validation des modifications, voir [Git Basics - Recording Changes to the Repository](http://www.git-scm.com/book/en/v2/Git-Basics-Recording-Changes-to-the-Repository){: new_window}.
  ```
  rm -rfv $2/*
  ```
  3. Envoyez votre application par commande push avec le pack de construction null modifié pour supprimer
le cache à l'aide de la commande suivante. Une fois cette étape réalisée, l'intégralité du contenu du répertoire cache de votre application est supprimée.
  ```
  cf push nom_app -p chemin_app -b <pack_construction_null_modifié>
  ```
  4. Envoyez votre application par commande push avec le pack de construction le plus récent que vous souhaitez utiliser à l'aide de la commande suivante : 
  ```
  cf push nom_app -p chemin_app -b <pack_construction_le_plus_récent>
  ```
  
	


## Messages NOTICE du pack de construction PHP
{: #ts_phplog}

Des messages contenant le terme NOTICE peuvent apparaître dans les journaux. Vous pouvez arrêter la journalisation de ces
messages en changeant le niveau de journalisation.	
	
 

Lorsque vous envoyez par commande push une application dans Bluemix à l'aide d'un pack de construction PHP, des messages contenant le terme
`NOTICE` peuvent s'afficher :
{: tsSymptoms}

```
• 2015-01-26T15:00:59.70+0100 [App/0] ERR [26-Jan-2015 14:00:59] NOTICE: [pool www] 'user' directive is ignored when FPM is not running as root
• 2015-01-26T15:01:00.63+0100 [App/0] ERR [26-Jan-2015 14:00:59] NOTICE: [pool www] 'user' directive is ignored when FPM is not running as root
• 2015-01-26T15:01:00.63+0100 [App/0] ERR [26-Jan-2015 14:00:59] NOTICE: fpm is running, pid 93
• 2015-01-26T15:01:00.63+0100 [App/0] ERR [26-Jan-2015 14:00:59] NOTICE: ready to handle connections
```



Dans le pack de construction PHP, le paramètre error_log est utilisé pour définir le niveau de journalisation. Par défaut, la valeur du paramètre `error_log` est **stderr notice**. L'exemple
ci-dessous illustre la configuration du niveau de journalisation par défaut dans le fichier `nginx-defaults.conf` du pack de
construction PHP fourni par Cloud Foundry. Pour plus d'informations, voir [cloudfoundry/php-buildpack](https://github.com/cloudfoundry/php-buildpack/blob/ff71ea41d00c1226d339e83cf2c7d6dda6c590ef/defaults/config/nginx/1.5.x/nginx-defaults.conf){: new_window}.
{: tsCauses} 

```
daemon off;
error_log stderr notice;
pid @{HOME}/nginx/logs/nginx.pid;
```

 	
	
Les messages `NOTICE` sont informatifs et ne signalent pas nécessairement un problème. Vous pouvez arrêter la journalisation de ces
messages en remplaçant le niveau de journalisation stderr notice par stderr error dans le fichier nginx-defaults.conf de votre pack de construction. Exemple : 	
{: tsResolve}

```
daemon off;
error_log stderr error;
pid @{HOME}/nginx/logs/nginx.pid;
```
Pour plus d'informations sur la modification de la configuration de journalisation par défaut, voir [error_log](http://nginx.org/en/docs/ngx_core_module.html#error_log){: new_window}.
	

## Impossible d'importer une bibliothèque Python tierce dans {{site.data.keyword.Bluemix_notm}}
{: #ts_importpylib}

Il se peut que vous ne puissiez pas importer une bibliothèque Python tierce dans {{site.data.keyword.Bluemix_notm}}. Vous pouvez résoudre le problème en ajoutant des fichiers de configuration dans le répertoire racine de votre application Python.


Lorsque vous essayez d'importer une bibliothèque Python tierce, par
exemple la bibliothèque `web.py`, la commande `cf push` échoue.
{: tsSymptoms}


 

Ce problème survient lorsque les informations de configuration pour
l'application Python manquent.
{: tsCauses}


 

Pour résoudre le problème, ajoutez un fichier `requirements.txt` et un fichier `Procfile` dans le répertoire racine
de votre application Python. Les informations suivantes supposent que vous importez la bibliothèque web.py :
{: tsResolve}

  1. Ajoutez un fichier `requirements.txt` dans le répertoire racine de votre application Python.
     Le fichier
`requirements.txt` spécifie les packages de bibliothèque requis pour votre application Python ainsi que la version des packages. L'exemple
ci-après illustre le contenu du fichier `requirements.txt`, où `web.py==0.37` indique que la version de la bibliothèque
`web.py` qui sera téléchargée est la version 0.37 et `wsgiref==0.1.2` indique que la version de l'interface Web de
Secure Gateway requise par la bibliothèque web.py est la version 0.1.2.
	 ```
	 web.py==0.37
     wsgiref==0.1.2
	 ```
	Pour plus d'informations sur la configuration du fichier `requirements.txt`, voir [Requirements files](https://pip.readthedocs.org/en/1.1/requirements.html). 
	 
  2. Ajoutez un fichier `Procfile` dans le répertoire racine de votre application Python.
	Le fichier `Procfile`
contient la commande de démarrage de votre application Python. Dans la commande ci-dessous, *nom_de_votre_app* est le nom de votre application
Python et *PORT* est le numéro de port que votre application Python doit utiliser pour recevoir les demandes des utilisateurs de
l'application. *$PORT* est facultatif. Si vous ne spécifiez pas PORT dans la commande de démarrage, le numéro de port qui figure dans la
variable d'environnement `VCAP_APP_PORT` dans l'application est utilisé à la place. 
	```
	web: python <nom_de_votre_app>.py $PORT
	```
A présent, vous pouvez importer la bibliothèque Python tierce dans {{site.data.keyword.Bluemix_notm}}.	



## Le bouton Actions de la page Détails de l'instance est désactivé
{: #ts_actionsbutton}



Le bouton Actions de la page Détails de l'instance est désactivé.
{: tsSymptoms} 

 

Ce problème se produit pour l'une des raisons suivantes :
{: tsCauses}

  * L'application n'est pas une application Web Java™. L'utilitaire de gestion des ressources prend en charge uniquement les applications Web
déployées avec les packs de construction Liberty.
  * L'application n'est pas déployée avec le pack de construction Liberty imbriqué.
  * L'application a été déployée avec une ancienne version du pack de construction Liberty.



Si l'application a été déployée avec une ancienne version du pack de construction Liberty, redéployez l'application dans {{site.data.keyword.Bluemix_notm}}. Sinon, vous pouvez transmettre les fichiers journaux d'application client suivants à l'équipe de support :
{: tsResolve} 

  * logs/messages.log
  * logs/stdout.log
  * logs/stderr.log
  

  
  
## Les données d'identification sont requises lors de l'ouverture d'une fenêtre de trace ou de vidage
{: #ts_username}


 

Un nom d'utilisateur et un mot de passe sont requis lors de l'ouverture de la fenêtre de trace et de vidage.
{: tsSymptoms}

 

Ce problème se produit à cause du dépassement de délai d'attente de la session de connexion.
{: tsCauses}

 

Entrez à nouveau le nom d’utilisateur et le mot de passe.
{: tsResolve}




## Des erreurs surviennent lors de l'exécution d'opérations de trace ou de vidage
{: #ts_target}

 

Un message d'erreur s'affiche lorsque des opérations de trace ou de vidage sont en cours. Ce message indique qu'une instance cible d'une application n'est pas à l'état en cours :	
{: tsSymptoms}

```
Instance 0 : La définition de la spécification de trace a abouti
Instance 2 : La définition de la spécification de trace a abouti
Instance 1 : L'instance cible 1 pour l'application abcd n'est pas à l'état en cours.
Instance 3 : La définition de la spécification de trace a abouti
Instance 4 : La définition de la spécification de trace a abouti
```



Ce problème se produit pour l'une des raisons suivantes :
{: tsCauses} 

  * Les fonctionnalités de trace ou de vidage s'appliquent uniquement aux instances d'application en cours d'exécution. Les opérations de trace ou de vidage ne peuvent pas être utilisées sur des instances d'application arrêtées, en cours de démarrage ou en panne.
  * Le statut de l'instance d'application change lorsque la boîte de dialogue de trace ou de vidage est ouverte. 
  


La solution consiste à fermer la fenêtre, puis à la rouvrir.
{: tsResolve} 



## Les instances possèdent une configuration traceSpecification différente
{: #ts_different_config}

 

Il peut exister différentes configurations traceSpecification pour différentes instances d'une seule application.
{: tsSymptoms}

 

Ce problème se produit pour l'une des raisons suivantes :
{: tsCauses}

  * Il se peut que vous ayez changé la configuration pour une ou plusieurs instances précédemment. Si vous changez la configuration traceSpecification pour une instance, cette configuration ne s'applique pas aux autres instances de la même application. Par exemple, votre application utilise log4j et il existe deux instances pour cette application. Vous
pouvez remplacer le niveau de journalisation info de l'instance 0 par debug ; toutefois, le niveau de journalisation de l'instance 1 reste info. 
  * L'application s'étend et possède de nouvelles instances. L'utilitaire de gestion des ressources n'applique pas la configuration
traceSpecification de l'instance existante à la
nouvelle instance ajoutée. La nouvelle instance utilise la configuration par défaut. Par exemple, votre application utilise log4j et possède une instance. Vous
pouvez remplacer le niveau de journalisation info de cette instance par debug. Après cette modification, si vous étendez votre application à deux
instances, le niveau de journalisation de la nouvelle instance est info, et non debug.
  


Ce comportement est normal.
{: tsResolve} 





## Quota de disque dépassé
{: #ts_diskquota}

Vous pouvez constater, dans votre journal d'application, que le quota de disque est dépassé.

 

Le message d'erreur `Disk quota exceeded` figure dans le journal de votre application.
{: tsSymptoms}



Ce problème survient pour l'une des raisons suivantes : 
{: tsCauses} 

  * Les fichiers de vidage sont générés avec les instances d'application en cours d'exécution ; le quota de disque alloué est dépassé. Par défaut, le quota de disque pour une instance d'application est de 1 Go. Vous
pouvez vérifier l'utilisation de votre disque en cliquant sur **Tableau de
bord > Application > Contexte d'exécution de l'application**. L'exemple suivant montre
les informations de contexte d'exécution, notamment l'utilisation du disque, pour deux instances d'une application :
    ```
    Instance	State	CPU	Memory Usage	Disk Usage

	0		Running	1.0%	344.8MB/512MB	236.8MB/1GB
	2		Running	2.3%	361.2MB/512MB	235.7MB/1GB
    ```
  * Le quota de disque est limité par le quota de l'organisation.
  
  


Vous pouvez résoudre ce problème en suivant l'une des méthodes ci-dessous :
{: tsResolve} 

  * Supprimez les fichiers de vidage après les avoir téléchargés.
  * Redéployez l'application avec un quota de disque plus important en insérant l'entrée suivante dans le manifeste de déploiement :
    ```
	disk_quota: 2048
	```
	
	


