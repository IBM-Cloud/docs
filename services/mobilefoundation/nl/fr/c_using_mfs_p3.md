---

copyright:
  years: 2016
lastupdated:  "2016-10-14"
---

#	Utilisation du plan Developer Pro
{: #using_mobilefoundation_p3}

<!--Last updated: 14 October 2016
{: .last-updated}-->

{{site.data.keyword.mobilefoundation_short}}: Developer
Pro convient aux opérations de développement et de tests en
équipe. Ce plan n'est pas destiné à une utilisation en production.  

Une fois l'instance de service
{{site.data.keyword.mobilefoundation_short}}: Developer Pro
créée, au bout de quelques secondes, vous pouvez accéder à la
`Présentation` du site
{{site.data.keyword.Bluemix_notm}} qui fournit des tutoriels
et des vidéos facilitant vos premiers pas avec le service
{{site.data.keyword.mobilefoundation_short}}.

## Conditions prérequises
{: #prerequisites_p3}

Prenez connaissance des éléments suivants avant de configurer
l'instance de service {{site.data.keyword.mobilefoundation_short}}: Developer Pro.
* {{site.data.keyword.mobilefoundation_short}}:
Developer Pro est pris en charge uniquement avec les
plans {{site.data.keyword.Bluemix_notm}}
{{site.data.keyword.dashdbshort_notm}}: Enterprise
Transactional (prenant en charge OLTP).

* Vous devez avoir accès aux données d'identification de l'instance de service {{site.data.keyword.dashdbshort_notm}} avant de pouvoir configurer les paramètres de votre instance de service {{site.data.keyword.mobilefoundation_short}}.

**Remarque** : L'instance de service {{site.data.keyword.dashdbshort_notm}} peut exister dans n'importe quel `espace` de votre {{site.data.keyword.Bluemix_notm}} `organisation` ou de n'importe quelle autre `organisation` à laquelle vous avez accès. Assurez-vous que vous disposez des droits nécessaires pour accéder à l'`espace` dans lequel l'instance de service {{site.data.keyword.dashdbshort_notm}} service existe.


## Ajout de la connexion à la base de données
{: #configure_dashdb_p3}

###  Premières étapes
{: #firststeps_p3}

Une fois que vous avez créé l'instance de service
{{site.data.keyword.mobilefoundation_short}}: Developer Pro, lisez la procédure ci-après pour commencer à l'utiliser.

### Configuration de la connexion à l'instance de service {{site.data.keyword.dashdbshort_notm}}
{: #connect_dashdb_p3}

Une fois l'instance de service
{{site.data.keyword.mobilefoundation_short}}: Developer Pro créée, la page *Overview* s'affiche et vous
permet d'indiquer les informations de connexion à l'instance de
service {{site.data.keyword.dashdbshort_notm}}: Enterprise
Transactional.

1. Sélectionnez l'{{site.data.keyword.Bluemix_notm}} `organisation` dans laquelle l'instance de service {{site.data.keyword.dashdbshort_notm}} existe.

+ Depuis la liste des espaces disponibles dans `Organisation`, sélectionnez l'élément `Espace` {{site.data.keyword.Bluemix_notm}} dans lequel se trouve l'instance de service {{site.data.keyword.dashdbshort_notm}},

**Remarque :** Si l'`organisation` et l'`espace` dans lesquels réside votre instance de service {{site.data.keyword.dashdbshort_notm}} ne figurent pas dans la liste, vérifiez que vous êtes membre de cette `organisation` et de cet `espace`.

+ Sélectionnez également le nom du service (`Service
Name`) et les données d'identification
(`Credentials`) {{site.data.keyword.dashdbshort_notm}}
pour la connexion à l'instance de service
{{site.data.keyword.dashdbshort_notm}}.

+  Testez la connexion à l'instance de service
{{site.data.keyword.dashdbshort_notm}}: Enterprise Transactional
indiquée.

+  Cliquez sur **Ajouter**.
Cela permet de créer les tables requises dans l'instance de service de base de
données {{site.data.keyword.dashdbshort_notm}} configurée.

**Remarque** : Vous ne pouvez pas modifier l'instance de service {{site.data.keyword.dashdbshort_notm}} configurée pour être utilisée par votre instance de service {{site.data.keyword.mobilefoundation_short}}. Vous pouvez toutefois utiliser la même instance de service {{site.data.keyword.dashdbshort_notm}} sur plusieurs instances de service {{site.data.keyword.mobilefoundation_short}}, car chaque instance de service {{site.data.keyword.mobilefoundation_short}} crée son propre schéma dans l'instance de service {{site.data.keyword.dashdbshort_notm}} sélectionnée.

* Après quelques secondes, vous pouvez accéder à la page `Overview` qui fournit des tutoriels et des vidéos facilitant vos premiers pas avec le service {{site.data.keyword.mobilefoundation_short}}.

## Démarrage du serveur {{site.data.keyword.mobilefirst}}
{: #start_mobilefoundation_p3}

* Pour démarrer {{site.data.keyword.mfserver_short_notm}} avec les paramètres par défaut, cliquez sur **Start Basic Server**.

* Cette option affecte les paramètres suivants à un serveur
{{site.data.keyword.mfserver_long_notm}} :
    - Noeud unique avec 1 Go de mémoire. Cette taille est
suffisante pour des activités de développement et des activités de
test sommaires et pour des charges de travail à faible échelle.

    -	Le `nom_d'utilisateur` et le
`mot_de_passe` sont générés automatiquement pour
vous. Vous pouvez y accéder une fois que le serveur est en opération.

L'implantation de votre serveur débute. Ce processus prend environ 10 minutes et une fenêtre de message indique la progression de l'opération. A son terme, un tableau de bord s'affiche et présente les éléments suivants :

  -	L'état du serveur que vous exécutez (état, taille).

  -	La route de serveur créée pour vous. Utilisez cette route dans votre application mobile pour vous connecter à {{site.data.keyword.mfserver_short_notm}}.

  -	Votre `nom_d'utilisateur` personnel et votre `mot_de_passe` pour accéder à la console {{site.data.keyword.mfp_oc_short_notm}}. Le `mot_de_passe` est masqué. Cliquez sur l'icône **Show Password** pour le visualiser.

*	Cliquez sur **Launch Console** pour ouvrir la console {{site.data.keyword.mfp_oc_short_notm}}.


<!--This console runs inside the container.--> 
Elle vous permet de gérer vos applications, adaptateurs et
périphériques mobiles, ainsi que l'utilisation de votre serveur en
tant que serveur dorsal mobile, l'envoi de notifications push, etc.

##  Ajout d'un serveur Mobile Analytics
{: #adding_analytics_server_p3}

 Vous pouvez maintenant surveiller votre application mobile sur un serveur {{site.data.keyword.mobilefirst}} en ajoutant un serveur Mobile Analytics à l'instance de service {{site.data.keyword.mobilefoundation_short}}.

 Le plan Developer Pro crée le serveur Mobile Analytics dans un
groupe de conteneurs, l'utilisateur peut personnaliser la
configuration en sélectionnant le nombre de noeuds de conteneur dans
le groupe de conteneurs.

 Les utilisateurs peuvent aussi connecter des volumes aux conteneurs pour conserver les données. Le volume une fois sélectionné ne peut être changé. L'espace de partage de fichiers par défaut disponible pour l'utilisateur est de 20 Go. Si l'utilisateur a besoin d'un espace de stockage supplémentaire pour conserver des données d'analyse, il est invité à acheter un partage de fichiers supplémentaire et à créer un volume en utilisant ce partage de fichier. Il peut ensuite sélectionner ce nouveau volume lors du déploiement du serveur d'analyse.

 Pour plus d'informations sur l'ajout de volumes dans {{site.data.keyword.containerlong}}, voir [Stockage de données persistantes dans un volume à l'aide du tableau de bord {{site.data.keyword.Bluemix_notm}} ](https://new-console.ng.bluemix.net/docs/containers/container_volumes_ui.html){: new_window}.

* Cliquez sur commande d'ajout d'analyse pour ajouter le serveur Mobile Analytics à l'instance de service {{site.data.keyword.mobilefoundation_short}}.

* Vous pouvez utiliser la configuration de serveur
Mobile Analytics, pour laquelle une mémoire de 1 Go au minimum et 2
Go au maximum est prise en charge. Le serveur d'analyse est pris
en charge uniquement sur un seul noeud de ce plan.

Le processus de mise à disposition commence. Ce processus prend environ 10 minutes et une fenêtre de
message indique la progression de l'opération.  

* Lancez MobileFirst Analytics depuis {{site.data.keyword.mfp_oc_short_notm}}.

* La connexion unique est activée entre {{site.data.keyword.mfserver_short_notm}} et le serveur Mobile Analytics. Le serveur Mobile Analytics est configuré avec les mêmes clés LTPA et données d'identification de l'utilisateur que celles de {{site.data.keyword.mfserver_short_notm}}. 
Vous pouvez vous servir des mêmes
`nom_d'utilisateur` et
`mot_de_passe` pour vous connecter à la console
Mobile Analytics que ceux utilisés pour la connexion à
{{site.data.keyword.mfp_oc_short_notm}}.

Pour plus d'informations sur MobileFirst Analytics, voir
[MobileFirst
Foundation Operational Analytics](https://mobilefirstplatform.ibmcloud.com/tutorials/en/foundation/8.0/analytics/).

**Remarque :** le serveur Mobile Analytics est retiré quand vous supprimez l'instance de service {{site.data.keyword.mobilefoundation_short}} ou si vous tentez de recréer le serveur {{site.data.keyword.mfserver_short_notm}}.

## Recréation du serveur
{{site.data.keyword.mobilefirst}}
{: #recreate_mobilefoundation_p3}

*	Cliquez sur **Recreate** pour recréer le
serveur.

* Cette action arrête votre serveur existant et supprime les données. Une nouvelle instance de serveur est créée avec une version mise à jour, si elle est disponible. Cette action prend quelques minutes avant de s'achever.

**Remarque** : Toutes les données provenant de votre instance de serveur précédente, y compris les informations sur les applications et les adaptateurs, sont conservées dans l'instance de service {{site.data.keyword.dashdbshort_notm}} configurée ; elles sont utilisées pour recréer le serveur.

##	Paramétrage d'une configuration avancée
{: #using_mfs_advanced_p3}

L'option **Start Server with Advanced Configuration** de la page `Overview` permet de créer le serveur avec des paramètres avancés ou personnalisés. Vous pouvez également mettre à jour les paramètres du serveur pour personnaliser sa configuration en cliquant sur l'onglet **Configuration**. {{site.data.keyword.mobilefoundation_short}} vous permet d'accéder à certains paramètres avancés.

*	Dans l'onglet **Topology**, vous pouvez
sélectionner la taille du serveur, ainsi que la mémoire dont vous avez besoin. Le
serveur par défaut est créé avec 1 Go de mémoire.
  - Vous pouvez modifier la mémoire de votre serveur en
fonction de vos besoins jusqu'à 2 Go au maximum.

  - **Nodes** affiche le nombre de noeuds créés. 
Cette zone n'est pas modifiable dans {{site.data.keyword.mobilefoundation_short}}: Developer Pro. 
Le nombre de noeuds
<!--in your {{site.data.keyword.IBM_notm}} container group-->
est par défaut de **1** dans le plan Developer Pro.

Pour plus de détails, voir la [documentation {{site.data.keyword.mobilefoundation_long}}](https://www.ibm.com/support/knowledgecenter/SSHS8R_8.0.0/wl_welcome.html){: new_window}.
