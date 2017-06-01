---

copyright:
  years: 2015, 2017

lastupdated: "2017-04-10"

---

{:tsSymptoms: .tsSymptoms}
{:tsCauses: .tsCauses}
{:tsResolve: .tsResolve}
{:new_window: target="_blank"}  
{:shortdesc: .shortdesc}
{:codeblock: .codeblock}





# Traitement des incidents liés à la gestion des applications
{: #managingapps}


Des problèmes d'ordre général liés à la gestion des applications peuvent survenir, par exemple, les applications ne peuvent pas être mises à jour ou les caractères codés sur deux octets ne sont pas affichés. Dans de nombreux cas, ces problèmes peuvent être résolus en quelques opérations simples.
{:shortdesc}


## Des modifications n'ont pas été sauvegardées
{: #ts_unsaved_changes}

Lorsque vous naviguez dans la page des détails de l'application, vous ne pourrez peut-être pas effectuer d'action et vous serez invité à sauvegarder vos modifications pour pouvoir continuer.

Lorsque vous essayez de vérifier votre appli ou vos services sur la page des détails de l'application, vous obtenez toujours le message d'erreur suivant :
{: tsSymptoms}

`Des modifications n'ont pas été sauvegardées dans la page nom_app. Sauvegardez ou annulez les modifications.`

Lorsque vous survolez avec la souris les zones **INSTANCES** ou **QUOTA DE MEMOIRE** dans le panneau du contexte d'exécution, les valeurs changent. Ce comportement est normal. Toutefois, le message d'erreur vous invite à sauvegarder les paramètres de mémoire ou d'instance avant de quitter la page.
{: tsCauses}

Fermez la fenêtre de message, puis cliquez sur le bouton **REINITIALISER** de votre contexte d'exécution.
{: tsResolve}

## Le basculement automatique entre les régions Bluemix n'est pas disponible
{: #ts_failover}

Vous ne pouvez pas utiliser le basculement automatique entre les régions {{site.data.keyword.Bluemix_notm}}. Toutefois, vous pouvez utiliser un fournisseur DNS qui prend en charge le basculement entre plusieurs adresses IP comme solution de contournement.

Lorsqu'une région {{site.data.keyword.Bluemix_notm}} n'est plus disponible, les applications qui sont exécutées dans cette région ne sont plus
disponibles non plus, même si les mêmes applications s'exécutent dans une autre région {{site.data.keyword.Bluemix_notm}}.
{: tsSymptoms}

{{site.data.keyword.Bluemix_notm}} ne fournit pas encore le basculement automatique d'une région vers une autre.
{: tsCauses}

Vous pouvez utiliser un fournisseur DNS qui prend en charge le basculement intelligent entre plusieurs adresses IP et configurer manuellement vos paramètres DNS pour activer le basculement automatique entre des régions {{site.data.keyword.Bluemix_notm}}. NSONE, Akamai et Dyn sont des fournisseurs DNS qui proposent cette capacité.
{: tsResolve}

Lorsque vous configurez vos paramètres DNS, vous devez spécifier les adresses IP publiques des régions {{site.data.keyword.Bluemix_notm}} dans lesquelles vos applications s'exécutent. Pour obtenir l'adresse IP publique d'une région {{site.data.keyword.Bluemix_notm}}, utilisez la commande `nslookup`. Par exemple, vous pouvez entrer la commande suivante dans une fenêtre de ligne de commande :
```
nslookup stage1.mybluemix.net
```

## Impossible de faire passer les applications en mode débogage
{: #ts_debug}

Il se peut que vous ne puissiez pas activer le mode débogage si votre version de machine virtuelle Java (JVM) est la version 8 ou antérieure.

Après que vous avez sélectionné **Activer le débogage d'application**, les outils tentent de faire passer l'application en mode débogage. Le plan de travail Eclipse entame alors une session de débogage. Lorsque les outils parviennent à activer le mode débogage, le statut de l'application Web affiche `Mise à jour du mode`, `Développement`, et `Débogage`.
{: tsSymptoms}

Par contre, si les outils ne parviennent pas à activer le mode débogage, le statut de l'application Web indique uniquement `Mise à jour du mode` et `Développement`, sans afficher `Débogage`. Les outils peuvent également afficher le message d'erreur suivant dans la vue Console :

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
... 7 more
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

Les versions de machine virtuelle Java (JVM) suivantes ne peuvent pas établir une session de débogage : IBM JVM 7, IBM JVM 8 et les versions antérieures d'Oracle JVM 8.
{: tsCauses}

Si la machine virtuelle Java (JVM) de votre plan de travail correspond à l'une de ces versions, vous pouvez rencontrer des problèmes lorsque vous créez une session de débogage. La version de machine virtuelle Java de votre plan de travail est généralement celle de la JVM système de votre ordinateur local. Ce n'est pas la même que celle de votre application Java&trade; {{site.data.keyword.Bluemix_notm}} en cours d'exécution. L'application Java {{site.data.keyword.Bluemix_notm}} Java opère presque toujours sur la machine virtuelle Java IBM, et parfois sur la machine virtuelle Java OpenJDK.

Pour vérifier la version Java utilisée par {{site.data.keyword.eclipsetoolsfull}}, procédez comme suit :
{: tsResolve}

  1. Dans IBM Eclipse Tools for Bluemix, sélectionnez **Aide** > **A propos d'Eclipse** > **Détails de l'installation** > **Configuration**.
  2. Localisez la propriété `eclipse.vm` dans la liste. La ligne suivante est un exemple de propriété `eclipse.vm` :

	```
	eclipse.vm=C:\Program Files\IBM\ibm-java-sdk-80-win-x86_64\bin\..\jre\bin\j9vm\jvm.dll
	```

  3. Sur la ligne de commande, entrez `java -version` depuis le répertoire `bin` de votre installation Java. Les informations de version de votre JVM IBM s'affichent.

Si la machine virtuelle Java de votre plan de travail utilise IBM JVM 7 ou IBM JVM 8, ou une version précédente d'Oracle JVM 8, procédez comme suit pour passer à Oracle JVM 8 :

  1. Téléchargez et installez Oracle JVM 8. Pour plus d'informations, voir [Java SE Downloads ![Icône de lien externe](../icons/launch-glyph.svg "External link icon")](http://www.oracle.com/technetwork/java/javase/downloads/index.html){: new_window}.
  2. Redémarrez Eclipse.
  3. Vérifiez que la propriété `eclipse.vm` pointe sur votre nouvelle installation d'Oracle JVM 8.


## Impossible de réutiliser le nom des applications supprimées
{: #ts_reuse_appname}

Après avoir supprimé une application, vous ne pouvez réutiliser le nom de cette dernière qu'après en avoir supprimé la route.

Lorsque vous essayez de réutiliser le nom de l'application, vous recevez le message suivant :
{: tsSymptoms}

`Le nom est déjà utilisé par une autre application.`

Lorsqu'une application est supprimée, sa route, autrement dit, son URL, n'est pas automatiquement supprimée. Par conséquent, elle n'est pas disponible pour être réutilisée. Vous devez accéder à l'espace où l'application a été créée afin de supprimer la route et pouvoir réutiliser l'application.
{: tsCauses}

Procédez comme suit pour supprimer la route inutilisée :
{: tsResolve}

  1. Vérifiez si la route appartient à l'espace en cours en entrant la commande suivante :
     ```
	 cf routes
	 ```
  2. Si la route n'appartient pas à l'espace en cours, accédez à l'espace ou à l'organisation auxquels elle appartient en entrant la commande suivante :
     ```
	 cf target -o nom_org -s nom_espace
	 ```
  3. Supprimez la route de l'application en entrant la commande suivante :
     ```
	 cf delete-route nom_domaine -n nom_hôte
	 ```
	 Exemple :
	 ```
	 cf delete-route mybluemix.net -n app001
	 ```

## Impossible d'extraire les espaces dans l'organisation
{: #ts_retrieve_space}

Vous ne pouvez pas créer une application ou un service si aucun espace n'est associé à votre organisation en cours.

Lorsque vous tentez de créer une application dans Bluemix, le message d'erreur suivant s'affiche :
{: tsSymptoms}

`BXNUI0515E: Les espaces dans l'organisation n'ont pas été extraits. Un problème de connexion réseau est survenu ou aucun espace n'est associé à l'organisation en cours.`

Cette erreur se produit souvent la première fois que vous tentez de créer une application ou un service à partir du catalogue lorsqu'un espace n'a pas encore été créé.
{: tsCauses}

Vérifiez que vous avez créé un espace dans votre organisation. Pour créer un espace, appliquez l'une des méthodes suivantes :
{: tsResolve}

  * Dans la barre de menu, cliquez sur **Gérer > Compte > Organisations**. Sélectionnez l'organisation dans laquelle vous souhaitez créer l'espace, puis cliquez sur **Créer un espace**.
  * Dans l'interface de ligne de commande cf, tapez `cf create-space <nom_espace> -o <nom_organisation>`.

Essayez à nouveau. Si ce message réapparaît, ouvrez la page de [statut Bluemix ![Icône de lien externe](../icons/launch-glyph.svg "External link icon")](http://ibm.biz/bluemixstatus){: new_window} pour déterminer si un service ou un composant présente un problème.


## Impossible d'effectuer les actions demandées
{: #ts_authority}

Il se peut que vous ne puissiez pas effectuer des actions si vous ne disposez pas des droits d'accès appropriés.

Lorsque vous essayez d'effectuer des actions pour une instance de service ou une instance d'application, vous ne pouvez pas effectuer les actions demandées et l'un des messages d'erreur suivants s'affiche :
{: tsSymptoms}

`BXNUI0514E: Vous n'êtes développeur dans aucun des espaces de l'organisation <nom_organisation>.`

`Erreur de serveur, code de statut : 403, code d'erreur 10003, message : vous n'êtes pas autorisé à effectuer l'action demandée.`

Vous ne disposez pas du niveau de droits approprié requis pour effectuer les actions.
{: tsCauses}

Pour obtenir le niveau de droits approprié, appliquez l'une des méthodes suivantes :
{: tsResolve}
 * Sélectionnez une autre organisation et un autre espace pour laquelle ou lequel vous disposez du rôle Développeur.
 * Demandez au responsable de l'organisation de vous attribuer le rôle Développeur ou de créer un espace, puis de vous attribuer le rôle Développeur. Pour plus d'informations, voir [Gestion des organisations et des espaces](/docs/admin/orgs_spaces.html).

## Impossible d'accéder à des services Bluemix en raison d'erreurs d'autorisation
{: #ts_vcap}

Des erreurs d'autorisation peuvent survenir lorsque votre application accède à un service {{site.data.keyword.Bluemix_notm}} si les données d'identification du service sont codées en dur dans votre application.

Une fois que vous avez configuré votre application pour qu'elle communique avec un service {{site.data.keyword.Bluemix_notm}}, vous la déployez dans {{site.data.keyword.Bluemix_notm}}. Toutefois, vous ne pouvez pas utiliser l'application pour accéder au service {{site.data.keyword.Bluemix_notm}} et recevez une erreur d'autorisation.
{: tsSymptoms}

Il se peut que les données d'identification codées en dur dans l'application ne soient pas correctes. A chaque fois que le service est recréé, les données d'identification permettant d'y accéder changent.
{: tsCauses}

Au lieu de coder en dur les données d'identification dans votre application, utilisez les paramètres de connexion de la variable d'environnement VCAP_SERVICES. Les méthodes d'utilisation des paramètres de connexion de la variable d'environnement VCAP_SERVICES varient selon les langages de programmation. Par exemple, pour les applications Node.js, vous pouvez utiliser la commande suivante :
{: tsResolve}

```
process.env.VCAP_SERVICES
```
Pour plus d'informations sur les commandes que vous pouvez utiliser dans d'autres langages de programmation, voir [Java ![Icône de lien externe](../icons/launch-glyph.svg "External link icon")](http://docs.run.pivotal.io/buildpacks/java/java-tips.html#env-var){: new_window} et [Ruby ![Icône de lien externe](../icons/launch-glyph.svg "External link icon")](http://docs.run.pivotal.io/buildpacks/ruby/ruby-tips.html#env-var){: new_window}.


## Impossibilité de déployer des applications à l'aide des outils IBM Eclipse pour Bluemix
{: #ts_bm_tools_facet}

Lorsqu'une facette non prise en charge est appliquée à votre projet Eclipse, il se peut que vous ne puissiez pas déployer vos applications dans {{site.data.keyword.Bluemix_notm}} à l'aide d'IBM Eclipse Tools for {{site.data.keyword.Bluemix_notm}}.

Votre application peut être déployée avec succès dans {{site.data.keyword.Bluemix_notm}} à l'aide de l'interface de ligne de commande Cloud Foundry. Toutefois, vous ne pouvez pas déployer l'application dans {{site.data.keyword.Bluemix_notm}} avec IBM Eclipse Tools for {{site.data.keyword.Bluemix_notm}} et le message d'erreur suivant s'affiche : `La facette de projet <nom_facette> n'est pas prise en charge.` Exemple :
{: tsSymptoms}
`La facette de projet Cloud Foundry Standalone Application version 1.0 n'est pas prise en charge.`

Les outils IBM Eclipse pour {{site.data.keyword.Bluemix_notm}} mappent des projets vers les contextes d'exécution {{site.data.keyword.Bluemix_notm}} par facettes de projet. Les facettes définissent les exigences des projets Java EE dans Eclipse et sont utilisées dans le cadre de la configuration du contexte d'exécution pour que différents contextes d'exécution soient associés à différents projets. Si la facette qui est appliquée au projet n'est pas prise en charge par IBM Eclipse Tools for {{site.data.keyword.Bluemix_notm}}, vous ne pourrez peut-être pas déployer votre application à l'aide d'IBM Eclipse Tools for {{site.data.keyword.Bluemix_notm}}.
{: tsCauses}

Vous devez supprimer la facette du projet Eclipse pour pouvoir déployer votre application à l'aide des outils IBM Eclipse pour {{site.data.keyword.Bluemix_notm}}.
{: tsResolve}

Pour supprimer la facette, dans les outils IBM Eclipse pour {{site.data.keyword.Bluemix_notm}}, cliquez sur **Projet>Propriétés>Facettes de projet** pour le projet concerné. Décochez ensuite la case correspondant à la facette non prise en charge.


## Réception d'erreurs 502 Bad Gateway
{: #ts_502_error}

Si vous recevez des erreurs 502 Bad Gateway lorsque vous interagissez avec des applications
sur {{site.data.keyword.Bluemix_notm}},
consultez la page de statut {{site.data.keyword.Bluemix_notm}}
et exécutez les actions en conséquence.

Vous recevez des messages d'erreur commençant par 502 Bad Gateway. Exemple : `502 Bad Gateway: Registered endpoint failed to handle the
request.`
{: tsSymptoms}

Une erreur Bad Gateway se produit généralement lorsque vous visitez un site Web qui utilise un serveur proxy pour stocker et relayer les données provenant du serveur principal hébergeant le site. Il se peut que le serveur principal et le serveur proxy ne se connectent pas correctement, ce qui déclenche l'affichage du code d'état HTTP 502 dans votre fenêtre de navigateur. Ce code d'état indique que le serveur principal du site n'a pas reçu l'implémentation HTTP attendue de la part du serveur proxy.
{: tsCauses}

D'autres raisons moins fréquentes pour une erreur Bad Gateway sont les décrochages du fournisseur d'accès Internet, des configurations de pare-feu incorrectes et des erreurs de cache du navigateur.

Si vous suspectez l'arrêt d'un service {{site.data.keyword.Bluemix_notm}}, consultez d'abord la page d'[état de {{site.data.keyword.Bluemix_notm}} ![Icône de lien externe](../icons/launch-glyph.svg "External link icon")](http://ibm.biz/bluemixstatus){: new_window}. Une solution de contournement peut consister à utiliser le service dans une autre région {{site.data.keyword.Bluemix_notm}}. Des informations détaillées sont disponibles dans [Utilisation des services dans une autre région ![Icône de lien externe](../icons/launch-glyph.svg "External link icon")](/docs/services/reqnsi.html#cross_region_service){: new_window}. Si le statut du service est normal, essayez la procédure suivante pour résoudre le problème :
{: tsResolve}

  * Exécutez à nouveau l'action :
    * Rechargez la page en appuyant sur la touche F5 de votre clavier ou en cliquant sur le bouton d'actualisation. Si cette étape ne fonctionne pas, videz le cache de votre navigateur et supprimez les cookies, puis rechargez la page.
    * Utilisez un navigateur différent.
    * Rallumez votre routeur, votre modem et votre ordinateur. Le réamorçage de ces
unités peut éliminer diverses erreurs à l'origine de l'erreur 502.
  * Attendez et recommencez ultérieurement. Dans certaines instances, des problèmes temporaires peuvent se produire
avec votre fournisseur d'accès Internet ou les services {{site.data.keyword.Bluemix_notm}}. Vous pouvez attendre jusqu'à ce que les problèmes temporaires soient résolus.
  * Si le problème existe toujours, contactez le support {{site.data.keyword.Bluemix_notm}}. Pour plus d'informations, voir [Contacter le support {{site.data.keyword.Bluemix_notm}} ![Icône de lien externe](../icons/launch-glyph.svg "External link icon")](/docs/support/index.html#contacting-bluemix-support){: new_window}.

## Dépassement du quota de disque
{: #ts_disk_quota}

Si votre espace disque est insuffisant, vous pouvez modifier manuellement le quota de disque
pour obtenir de l'espace disque supplémentaire.

Lorsque votre espace disque devient insuffisant, un message indiquant que le quota de disque est dépassé peut s'afficher. Pour résoudre le problème, vous pouvez tenter d'augmenter votre instance d'application pour obtenir davantage d'espace disque. Par exemple, vous pouvez passer de 256 Mo à 1256 Mo en modifiant le quota de mémoire sur la page de détails de l'application. Cependant, comme le quota de disque est resté le même, vous n'avez pas obtenu plus d'espace disque.
{: tsSymptoms}

Le quota de disque par défaut alloué à une application est de  1 Go. Si vous avez besoin de davantage d'espace disque, vous devez spécifier manuellement le quota de disque.
{: tsCauses}

Utilisez l'une des méthodes suivantes pour spécifier votre quota de disque. Le quota de disque maximal que vous pouvez spécifier est de 2 Go. Si les 2 Go ne sont toujours pas suffisants, essayez un service externe
tel que [Object Store](/docs/services/ObjectStorage/index.html).
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


## Impossibilité de recevoir des {{site.data.keyword.mobilepushshort}} pour les applications Android
{: #ts_push}

Dans certaines régions où Google n'est pas accessible, les applications Android ne peuvent pas recevoir les notifications que vous envoyez via le service {{site.data.keyword.mobilepushshort}} d'IBM. Dans ce cas, une solution de contournement consiste à utiliser des services tiers.

Vous liez un service {{site.data.keyword.mobilepushshort}} pour votre application Bluemix et envoyez un message aux unités enregistrées. Toutefois, les applications qui sont développées sur la plateforme Android ne peuvent pas recevoir vos notifications dans certaines régions.
{: tsSymptoms}

Le service IBM {{site.data.keyword.mobilepushshort}} utilise le service de messagerie basée sur le cloud de Google (GCM) pour transmettre les notifications aux applications mobiles développées sur la plateforme Android. Les applications mobiles doivent pouvoir accéder au service GCM pour que les applications Android puissent recevoir les notifications. Dans les régions où le service GCM n'est pas accessible aux applications Android, ces dernières ne peuvent pas recevoir de notifications {{site.data.keyword.mobilepushshort}}.
{: tsCauses}

Pour contourner ce problème, utilisez des services tiers qui ne reposent pas sur le service GCM, par exemple [Pushy ![Icône de lien externe](../icons/launch-glyph.svg "External link icon")](https://pushy.me){: new_window}, [igetui ![Icône de lien externe](../icons/launch-glyph.svg "External link icon")](http://www.getui.com/){: new_window} et [jpush ![Icône de lien externe](../icons/launch-glyph.svg "External link icon")](https://www.jpush.cn/){: new_window}.
{: tsResolve}


## La limite des services de l'organisation est atteinte
{: #ts_servicelimit}

Si vous possédez un compte d'essai, il se peut que vous ne puissiez pas créer d'application dans {{site.data.keyword.Bluemix_notm}} si vous avez atteint le nombre maximal de services pour votre organisation.

Lorsque vous tentez de créer une application dans {{site.data.keyword.Bluemix_notm}}, le message d'erreur suivant s'affiche :
{: tsSymptoms}

`BXNUI2032E: La ressource <instance_service> n'a pas été créée. Une erreur est survenue lors du contact de Cloud Foundry pour la création d'une ressource. Message Cloud Foundry : "You have exceeded your organization's services limit."`

Cette erreur survient lorsque vous avez atteint le nombre maximal d'instances de service dont vous pouvez disposer pour votre compte. Le nombre maximal d'instances de service pour un compte d'essai est 10.
{: tsCauses}

Supprimez les instances de service dont vous n'avez pas besoin ou retirez la limite relative au nombre d'instances de service dont vous pouvez disposer.
{: tsResolve}

  * Pour supprimer une instance de service, vous pouvez utiliser la console {{site.data.keyword.Bluemix_notm}} ou l'interface de ligne de commande.

    Pour utiliser la console {{site.data.keyword.Bluemix_notm}} afin de supprimer une instance de service, procédez comme suit :
	  1. Dans le tableau de bord Services, cliquez sur le menu **Actions** pour le service que vous souhaitez supprimer.
	  2. Cliquez sur **Supprimer le service**. Vous êtes invité à reconstituer l'application à laquelle l'instance de service était liée.

    Pour utiliser l'interface de ligne de commande afin de supprimer une instance de service, procédez comme suit :
	  1. Supprimez la liaison de l'instance de service à une application en entrant `cf unbind-service <nom_app> <nom_instance_service>`.
	  2. Supprimez l'instance de service en entrant `cf delete-service <nom_instance_service>`.
	  3. Une fois l'instance de service supprimée, vous pouvez reconstituer l'application à laquelle l'instance de service était liée en entrant `cf restage <nom_app>`.

  * Pour supprimer la limite relative au nombre d'instances de service dont vous pouvez disposer, convertissez votre compte d'essai en compte payant. Pour des informations sur la conversion de votre compte d'essai en compte payant, voir [Comment changer votre plan ?](/docs/pricing/index.html#changing).

## Impossibilité d'exécuter des fichiers exécutables sur Bluemix
{: #ts_executable}

Il peut être impossible d'exécuter des fichiers exécutables dans {{site.data.keyword.Bluemix_notm}} si ces fichiers ont été développés et générés dans un environnement différent.

Vous ne parvenez pas à exécuter des fichiers exécutables dans {{site.data.keyword.Bluemix_notm}} lorsque ceux-ci ont été développés et générés dans un environnement différent.
{: tsSymptoms}

Si le contenu à envoyer par commande push dans {{site.data.keyword.Bluemix_notm}} est déjà un fichier exécutable, il a déjà été généré et il n'est pas nécessaire de le générer dans {{site.data.keyword.Bluemix_notm}}. Dans ce cas, aucun pack de construction n'est requis pour l'exécution du fichier exécutable dans {{site.data.keyword.Bluemix_notm}}. Toutefois,
vous devez indiquer explicitement à {{site.data.keyword.Bluemix_notm}} qu'aucun pack de construction n'est
nécessaire.
{: tsCauses}

Lorsque vous envoyez par commande push le fichier exécutable dans
{{site.data.keyword.Bluemix_notm}}, vous devez spécifier la valeur null-buildpack, qui indique qu'aucun pack de
construction n'est requis. Spécifiez la valeur null-buildpack avec l'option **-b** dans la commande `cf push` :
{: tsResolve}

```
cf push nom_app -p chemin_app -c <commande_démarrage> -b <null-buildpack>
```
Exemple :
```
cf push nom_app -p chemin_app -c ./RunMeNow -b https://github.com/ryandotsmith/null-buildpack
```

## La limite de mémoire de l'organisation a été atteinte
{: #ts_outofmemory}

Si vous possédez un compte d'essai, il se peut que vous ne puissiez pas déployer une application dans {{site.data.keyword.Bluemix_notm}} si
vous avez
atteint la limite de mémoire définie pour votre organisation. Vous pouvez réduire la quantité de mémoire que vos applications utilisent ou augmenter le quota de mémoire de votre compte. Le quota de mémoire maximal pour un compte d'essai est 2 Go. Il ne peut être augmenté qu'en passant à un compte payant.

Lorsque vous déployez une application dans {{site.data.keyword.Bluemix_notm}}, le message d'erreur suivant s'affiche :
{: tsSymptoms}

`FAILED Server error, status code: 400, error code: 100005, message: You have exceeded your organization's memory limit.`

Cette erreur survient lorsque la quantité de mémoire restante pour votre organisation est inférieure à la quantité de mémoire requise par l'application à déployer. Le quota de mémoire maximal pour un compte d'essai est 2 Go.
{: tsCauses}

Vous pouvez augmenter le quota de mémoire de votre compte ou réduire la mémoire que vos applications utilisent.
{: tsResolve}

  * Pour augmenter le quota de mémoire de votre compte, convertissez votre compte d'essai en compte payant. Pour des informations sur la conversion de votre compte d'essai en compte payant, voir [Comptes payants](/docs/pricing/index.html#pay-accounts).
  * Pour réduire la quantité de mémoire que vos applications utilisent, servez-vous de la console {{site.data.keyword.Bluemix_notm}} ou de l'interface de ligne de commande cf.

    Si vous utilisez la console {{site.data.keyword.Bluemix_notm}}, procédez comme suit :

    1. Dans l'application Applications, sélectionnez votre application. La page des détails de l'application s'ouvre.
    2. Dans le panneau Contexte d'exécution, vous pouvez réduire la limite de mémoire maximal ou le nombre d'instances d'application, ou les deux, pour votre application.

    Si vous utilisez l'interface de ligne de commande cf, procédez comme suit :

    1. Vérifiez la quantité de mémoire qui est utilisée par vos applications :

	  ```
	  cf apps
	  ```

	  La commande cf apps répertorie toutes les applications que vous avez déployées dans votre espace en cours. Le statut de chaque application est également affiché.

    2. Pour réduire la quantité de mémoire qui est utilisée par votre application, réduisez le nombre d'instances d'application ou la limite de mémoire maximale, ou les deux :

	  ```
	  cf push nom_app -p chemin_app -i nombre_instances -m limite_mémoire
      ```

    3. Redémarrez votre application pour que les modifications soient appliquées.


## Les applications ne sont pas redémarrées automatiquement
{: #ts_apps_not_auto_restarted}

Une application n'est pas redémarrée automatiquement lorsqu'un service que vous liez à cette application cesse de fonctionner.	  

Lorsqu'un service que vous liez à une application tombe en panne, des problèmes tels que des indisponibilités, des exceptions et des échecs de connexion peuvent survenir sur l'application. {{site.data.keyword.Bluemix_notm}} ne redémarre pas automatiquement l'application pour assurer la reprise suite à ces problèmes.
{: tsSymptoms}

Ce comportement est normal dans Cloud Foundry.
{: tsCauses}

Vous pouvez redémarrer manuellement l'application en entrant la commande suivante dans l'interface de ligne de commande :
{: tsResolve}

```
cf push nom_app -p chemin_app
```
De plus, vous pouvez coder l'application afin d'identifier les problèmes et d'assurer la reprise après une indisponibilité, une exception ou un échec de connexion.

## Les variables définies par l'utilisateur sont perdues lorsqu'une application est envoyée par commande push
{: #ts_varsnotretained}

Lorsque vous envoyez une application par commande push à {{site.data.keyword.Bluemix_notm}} depuis IBM Eclipse Tools for {{site.data.keyword.Bluemix_notm}}, les variables que vous spécifiez sont réinitialisées sauf si vous les sauvegardez dans le fichier manifeste.

Les variables que vous spécifiez sont perdues une fois que vous avez envoyé une application par commande push à {{site.data.keyword.Bluemix_notm}} depuis IBM Eclipse Tools for {{site.data.keyword.Bluemix_notm}}.
{: tsSymptoms}

Les variables que vous spécifiez ne sont sauvegardées que si vous les sauvegardez dans le fichier manifeste.
{: tsCauses}

Lorsque vous envoyez une application par commande push à {{site.data.keyword.Bluemix_notm}} depuis IBM Eclipse Tools for {{site.data.keyword.Bluemix_notm}}, sélectionnez la case à cocher **Save to the manifest file** dans la page des détails de l'application de l'assistant Application. Ainsi, les variables que vous spécifiez dans l'assistant sont sauvegardées dans le fichier manifeste de votre application. A la prochaine ouverture de l'assistant, elles seront affichées automatiquement.
{: tsResolve}

<!-- begin STAGING ONLY -->

## Bluemix Live Sync Debug ne démarre pas à partir de la ligne de commande
{: #ts_no_debug}

Vous avez activé la fonction IBM Bluemix Live Sync Debug pour votre application à l'aide de la ligne de commande, mais vous ne pouvez pas accéder à l'interface de débogage.  

Vous avez activé la fonction de débogage pour votre application en définissant la variable d'environnement **BLUEMIX_APP_MGMT_ENABLE**. Toutefois, vous ne pouvez pas accéder à l'interface utilisateur de débogage sur `app_url/bluemix-debug/manage`.
{: tsSymptoms}

La fonction de débogage ne peut pas être activée dans les cas suivants :
{: tsCauses}

  * Lorsque le fichier `manifest.yml` contient l'attribut command
  * Lorsque vous utilisez l'option **-c** pour envoyer une application à {{site.data.keyword.Bluemix_notm}}

Utilisez l'une des options suivantes pour résoudre le problème :
{: tsResolve}

  * La pratique recommandée consiste à utiliser le pack de construction IBM Node.js pour démarrer l'application. Pour plus d'informations, voir la section sur la commande de démarrage dans la rubrique [Déploiement d'une application Node.js sur {{site.data.keyword.Bluemix_notm}}](/docs/runtimes/nodejs/index.html#nodejs_runtime).
  * Désactivez la commande pour votre application existante en modifiant l'attribut command dans le fichier `manifest.yml` par command: null ou en éditant votre commande push en y ajoutant `-c null`.
  * Retirez l'attribut **command** du fichier `manifest.yml`. Supprimez ensuite l'application en cours de {{site.data.keyword.Bluemix_notm}} et insérez de nouveau l'application.

<!-- end STAGING ONLY -->  


## Des organisations sont introuvables dans Bluemix
{: #ts_orgs}

Il se peut que vous ne parveniez pas à localiser votre organisation dans {{site.data.keyword.Bluemix_notm}} lorsque vous travaillez sur une région {{site.data.keyword.Bluemix_notm}}.

Vous pouvez vous connecter à la console {{site.data.keyword.Bluemix_notm}}, mais vous ne parvenez pas à envoyer vos applications par commande push à l'aide de l'interface de ligne de commande cf ou du plug-in Eclipse.
{: tsSymptoms}

Lorsque vous essayez d'envoyer une application par commande push à {{site.data.keyword.Bluemix_notm}} en utilisant l'interface de ligne de commande cf, l'un des messages d'erreur suivants, qui spécifie le nom de l'organisation, s'affiche :

`Erreur lors de la recherche de l'organisation`

`Organization not found`

Lorsque vous essayez d'envoyer une application par commande push à {{site.data.keyword.Bluemix_notm}} en utilisant le plug-in Eclipse Cloud Foundry, le message d'erreur suivant s'affiche :

`cloudspace not found.`

Ce problème survient car le noeud final d'API de la région avec laquelle vous travaillez n'est pas spécifié et l'organisation que vous recherchez peut se trouver dans une autre région.
{: tsCauses}

Si vous envoyez votre application par commande push à {{site.data.keyword.Bluemix_notm}} en utilisant l'interface de ligne de commande cf, entrez la commande cf api et spécifiez le noeud final d'API de la région. Par exemple, entrez la commande suivante pour vous connecter à la région {{site.data.keyword.Bluemix_notm}} Europe et Royaume-Uni :
{: tsResolve}

```
cf api https://api.eu-gb.bluemix.net
```
Si vous envoyez votre application par commande push à {{site.data.keyword.Bluemix_notm}} en utilisant les outils Eclipse, vous devez d'abord créer un serveur {{site.data.keyword.Bluemix_notm}} et spécifier le noeud final d'API de la région {{site.data.keyword.Bluemix_notm}} dans laquelle votre organisation a été créée. Pour plus d'informations sur l'utilisation des outils Eclipse, voir [Déploiement d'applications avec IBM Eclipse Tools for Bluemix](/docs/manageapps/eclipsetools/eclipsetools.html).  

## Impossible de créer les routes d'application
{: #ts_hostistaken}

Lorsque vous déployez une application dans {{site.data.keyword.Bluemix_notm}}, la route d'application ne peut pas être créée si le nom d'hôte que vous avez spécifié est déjà utilisé.

Lorsque vous déployez une application dans {{site.data.keyword.Bluemix_notm}}, le message d'erreur suivant s'affiche :
{: tsSymptoms}

`Creating route nom_hôte.nom_domaine ... FAILED Server error, status code: 400, error code: 210003, message: The host is taken:
nom_hôte`

Ce problème survient si le nom d'hôte que vous avez spécifié est déjà utilisé.
{: tsCauses}

Le nom d'hôte que vous spécifiez doit être unique dans le domaine que vous utilisez. Pour spécifier un autre nom d'hôte, utilisez l'une des méthodes suivantes :
{: tsResolve}

  * Si vous déployez votre application avec le fichier `manifest.yml`, spécifiez le nom d'hôte dans l'option host.	 
    ```
    host: nom_hôte
	```
  * Si vous déployez votre application depuis l'invite de commande, utilisez la commande `cf push` avec l'option **-n**.
    ```
    cf push nom_app -p chemin_app -n nom_hôte
    ```


## Les applications WAR ne peuvent pas être envoyées à l'aide de la commande cf push
{: #ts_cf_war}

Il est possible que vous ne puissiez pas utiliser la commande cf push pour déployer une application Web archivée dans {{site.data.keyword.Bluemix_notm}} si l'emplacement de l'application n'est pas spécifié correctement.

Lorsque vous téléchargez une application WAR dans {{site.data.keyword.Bluemix_notm}} par l'intermédiaire de la commande `cf push`, le message d'erreur suivant s'affiche :
{: tsSymptoms}
`Staging error: cannot get instances since staging failed.`

Ce problème peut se produire si le fichier WAR ou le chemin d'accès à ce fichier n'est pas spécifié.
{: tsCauses}

Utilisez l'option **-p** pour spécifier un fichier WAR ou ajouter un chemin d'accès. Exemple :
{: tsResolve}

```
cf push MonNomAppUnique01 -p app.war
```

```
cf push MonNomAppUnique02 -p "./app.war"
```
Pour plus d'informations sur la commande `cf push`, entrez `cf push -h`. 	


## Les caractères codés sur deux octets ne s'affichent pas correctement lorsque les applications Liberty sont envoyées par commande push vers Bluemix
{: #ts_doublebytes}

Il se peut que les caractères codés sur deux octets ne s'affichent pas correctement si la prise en charge Unicode n'est pas configurée correctement pour le servlet ou les fichiers JSP.

Lorsqu'une application Liberty est envoyée par commande push dans {{site.data.keyword.Bluemix_notm}}, les caractères codés sur deux octets spécifiés dans l'application ne s'affichent pas correctement.
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

Lorsque vous mettez à jour une application Node.js ou déployez votre application Node.js dans {{site.data.keyword.Bluemix_notm}}, l'un des messages d'erreur suivants peut s'afficher :
{: tsSymptoms}

`An app was not successfully detected by any available buildpack.`

`Instance (index 0) failed to start accepting connections.`

`Cannot get instances since staging failed.`

Les causes possibles sont les suivantes :
{: tsCauses}

  * La commande de démarrage n'est pas spécifiée.
  * Les fichiers requis pour déployer une application Node.js sont manquants dans l'application ou se trouvent dans un dossier autre que le répertoire racine.

Utilisez l'une des méthodes suivantes, selon la cause du problème à résoudre :
{: tsResolve}

  * Spécifiez la commande de démarrage en appliquant l'une des méthodes suivantes :
     * Utilisez l'interface de ligne de commande cf. Exemple :
        ```
		cf push MonNoeudJsUnique01 -p chemin_app -c "node app.js"
		```
    * Utilisez le fichier [package.json ![Icône de lien externe](../icons/launch-glyph.svg "External link icon")](https://docs.npmjs.com/json){: new_window}. Exemple :
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

  * Vérifiez qu'un fichier `package.json` existe dans votre application Node.js pour que le pack de construction Node.js puisse reconnaître l'application. Prenez soin de placer ce fichier dans le répertoire racine de votre application.
    L'exemple suivant représente un fichier `package.json` simple :  
	```
	{
        "name": "MyUniqueNodejs01",
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

Pour d'autres conseils relatifs aux applications Node.js, voir [Tips for Node.js Applications](http://docs.cloudfoundry.org/buildpacks/node/node-tips.html ![Icône de lien externe](../icons/launch-glyph.svg "External link icon"){: new_window}.


## Des erreurs de configuration figurent dans le fichier `server.xml` après l'importation d'une application Bluemix Liberty dans Eclipse
{: #ts_eclipse}

Si vous rencontrez des erreurs de configuration dans le fichier `server.xml` après avoir importé une application {{site.data.keyword.Bluemix_notm}} Liberty dans Eclipse, vous devrez peut-être supprimer du projet le fichier `server.xml`.

Après avoir importé une application {{site.data.keyword.Bluemix_notm}} Liberty dans Eclipse, vous rencontrez des erreurs de configuration dans le fichier `server.xml` dans la vue Erreurs d'Eclipse.
{: tsSymptoms}

Le pack de construction Liberty utilise le fichier `server.xml` pour configurer l'application et génère un fichier `runtime-vars.xml` lorsque l'application Liberty est envoyée par commande push dans {{site.data.keyword.Bluemix_notm}}. Lorsque vous importez l'application dans Eclipse, le fichier `runtime-vars.xml` n'existe pas dans votre environnement local.
{: tsCauses}

Pou résoudre ce problème, supprimez le fichier server.xml du projet. Le pack de construction crée le fichier `server.xml` de manière
dynamique lorsque vous envoyez par commande push l'application sous forme d'application WAR. Pour
plus d'informations, voir [Liberty for Java](/docs/runtimes/liberty/index.html).
{: tsResolve}


## Les applications ne peuvent pas être transférées à l'aide de packs de construction personnalisés
{: #ts_bp_compilation}

Il se peut que vous ne puissiez pas déployer une application dans {{site.data.keyword.Bluemix_notm}} à l'aide d'un pack de construction personnalisé, si les scripts que ce dernier contient ne sont pas exécutables.

Lorsque vous déployez une application dans {{site.data.keyword.Bluemix_notm}} à l'aide d'un pack de construction personnalisé, le message d'erreur `La constitution de l'application a échoué ; par conséquent, il n'y a pas d'instance à afficher` s'affiche.
{: tsSymptoms}

Ce problème peut se produire si des scripts (tels que le script de détection, le script de compilation ou le script de publication) ne sont pas exécutables.
{: tsCauses}

Vous pouvez utiliser la commande [git update ![](../icons/launch-glyph.svg " ")](http://git-scm.com/docs/git-update-index){: new_window} afin d'activer le droit d'exécution pour chaque script. Par exemple, vous pouvez entrer `git update --chmod=+x script.sh`.
{: tsResolve}

## Impossible de déployer une application depuis Delivery Pipeline dans IBM Bluemix Continuous Delivery
 {: #ts_devops_to_bm}

 Il se peut que vous ne puissiez pas déployer votre application à l'aide de {{site.data.keyword.deliverypipeline}} dans {{site.data.keyword.contdelivery_short}} si le fichier `manifest.yml` n'est pas présent dans votre application. 

 Lorsque vous déployez une application à l'aide de {{site.data.keyword.deliverypipeline}} dans {{site.data.keyword.contdelivery_short}}, il se peut que le message d'erreur `Unable to detect a supported application type` s'affiche.
 {: tsSymptoms}

 Ce problème peut survenir car le pipeline requiert un fichier `manifest.yml` pour déployer une application dans {{site.data.keyword.Bluemix_notm}}.
 {: tsCauses}

 Pour remédier à ce problème, vous devez créer un fichier `manifest.yml`. Pour plus d'informations sur la création du fichier `manifest.yml`, voir [Manifeste d'application](/docs/manageapps/depapps.html#appmanifest).
 {: tsResolve}

## Les applis Meteor ne peuvent pas être envoyées par commande push
{: #ts_meteor}

Il se peut que vous ne puissiez pas envoyer une application Meteor par commande push dans {{site.data.keyword.Bluemix_notm}} si le pack de construction n'est pas spécifié correctement.

Lorsque vous déployez une application Meteor dans {{site.data.keyword.Bluemix_notm}}, il se peut que le message d'erreur `La constitution de l'application a échoué ; par conséquent, il n'y a pas d'instance à afficher` s'affiche.
{: tsSymptoms}

Ce problème survient car aucun pack de construction n'est fourni pour les applications Meteor. Vous devez utiliser un pack de construction personnalisé.
{: tsCauses}

Afin d'utiliser un pack de construction personnalisé pour les applications Meteor, appliquez l'une des méthodes suivantes :
{: tsResolve}

  * Si vous déployez votre application avec le fichier `manifest.yml`, spécifiez l'adresse URL ou le nom de votre pack de construction personnalisé
avec l'option buildpack. Exemple :
  ```
  buildpack: https://github.com/Sing-Li/bluemix-bp-meteor
  ```
  * Si vous déployez votre application depuis l'invite de commande, utilisez la commande `cf
push` et spécifiez votre pack de construction personnalisé avec l'option **-b**. Exemple :
    ```
	cf push nom_app -p chemin_app -b https://github.com/Sing-Li/bluemix-bp-meteor
	```
