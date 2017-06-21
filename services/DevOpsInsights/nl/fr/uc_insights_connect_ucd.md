---

copyright:
  years: 2017
lastupdated: "2017-05-15"

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}

# Affichage des données des serveurs IBM UrbanCode Deploy
{: #connect_ucd}

Pour afficher les données d'un serveur IBM UrbanCode Deploy dans Delivery Insights, vous devez configurer une instance de DevOps Connect, installer un correctif sur le serveur, puis connecter ce serveur à DevOps Connect.
{:shortdesc}

## Prérequis
{: #prereqs}

Pour afficher des informations provenant de vos serveurs IBM UrbanCode Deploy dans {{site.data.keyword.DRA_short}}, vous devez héberger une instance de DevOps Connect sur un système qui peut se connecter à vos serveurs IBM UrbanCode Deploy. Ce système peut être un ordinateur physique ou une machine virtuelle. 

Le système qui héberge DevOps Connect doit satisfaire les conditions requises suivantes :
- Le système doit disposer d'un environnement JRE (Java Runtime Environment) version 8 ou ultérieure.
- La variable `PATH` du système doit inclure l'emplacement du JRE.
- Le système doit autoriser DevOps Connect à créer des connexions sortantes vers IBM Bluemix.

Votre serveur IBM UrbanCode Deploy doit également être à la version 6.2 ou ultérieure. 

## Configuration du service {{site.data.keyword.DRA_short}}
{: #configure_service}

Si vous ne disposez pas d'une chaîne d'outils ou de {{site.data.keyword.DRA_short}}, vous devez d'abord configurer {{site.data.keyword.DRA_short}} :
1. Dans le catalogue {{site.data.keyword.Bluemix}}, cliquez sur **{{site.data.keyword.DRA_short}}**, sélectionnez un plan de tarification et cliquez sur **Créer**.
1. Cliquez sur l'onglet **Gérer** et, sous **Obtenez des analyses sur les déploiements effectués par UrbanCode Deploy**, cliquez sur **Commencez ici**. Delivery Insights crée en arrière-plan une chaîne d'outils pour votre organisation. Les chaînes d'outils sont des collections d'intégrations d'outil et, dans ce cas, IBM UrbanCode Deploy et {{site.data.keyword.DRA_short}} font partie de votre chaîne d'outils. Pour plus d'informations sur les chaînes d'outils, voir [Utilisation des chaînes d'outils](../ContinuousDelivery/toolchains_working.html).

Si vous disposez déjà d'une chaîne d'outils, procédez comme suit pour ajouter Delivery Insights :
1. Si vous ne disposez pas de l'outil {{site.data.keyword.DRA_short}}, ajoutez-le à votre chaîne d'outils.
1. Sur votre chaîne d'outils, cliquez sur l'outil {{site.data.keyword.DRA_short}}.
1. Accédez à la page **Settings > Delivery Insights Setup**. 

Suivez les instructions de la page **Delivery Insights Setup** pour installer DevOps Connect et le connecter à {{site.data.keyword.DRA_short}}, comme indiqué dans la section qui suit. 

## Installation de DevOps Connect et connexion à {{site.data.keyword.DRA_short}}
{: #install_connect}

1. Sur la page **Delivery Insights Setup**, suivez la procédure pour configurer DevOps Connect et connecter vos serveurs IBM UrbanCode Deploy. Procédez comme suit :
{: #set_up_connect}
  1. Configurez un système pour exécuter DevOps Connect, comme décrit dans [Prérequis](uc_insights_connect_ucd.html#prereqs).
  1. Téléchargez DevOps Connect, qui est fourni sous la forme d'un fichier JAR exécutable. 
  1. Copiez le script à partir de la page **Delivery Insights Setup** et exécutez-le. Cette commande démarre DevOps Connect avec un jeton qui l'autorise à se connecter à votre organisation sur {{site.data.keyword.Bluemix}}.
  1. Connectez vos serveurs IBM UrbanCode Deploy à DevOps Connect, comme indiqué dans la section suivante. 

## Connexion des serveurs IBM UrbanCode Deploy à DevOps Connect
{: #connect_ucd_to_connect}

1. Installez le correctif sur votre serveur IBM UrbanCode Deploy. Toutes les versions d'IBM UrbanCode Deploy requièrent un correctif pour communiquer avec DevOps Connect. 
  1. Téléchargez le correctif adapté à votre version d'IBM UrbanCode Deploy en accédant à la page suivante : [http://public.dhe.ibm.com/software/products/UrbanCode/plugins/ucsync/patches/ibmucd/](http://public.dhe.ibm.com/software/products/UrbanCode/plugins/ucsync/patches/ibmucd/)

  1. Procédez à l'extraction du fichier. Il contient un ou plusieurs fichiers correctifs que vous devez ajouter au serveur.

  1. Arrêtez le serveur. Voir [Démarrage et arrêt du serveur](https://www.ibm.com/support/knowledgecenter/SS4GSP_6.2.4/com.ibm.udeploy.install.doc/topics/run_server.html).

  1. Placez les fichiers correctifs dans le dossier <code><em>application_data</em>/patches</code>, où <code><em>application_data</em></code> est le dossier des données d'application. Le dossier des données d'application par défaut est `/opt/ibm-ucd/server/appdata` sur Linux et `C:\Program Files\ibm-ucd\server\appdata` sous Windows. Sur les systèmes à haute disponibilité, le dossier des données d'application se trouve toujours sur une unité réseau partagée à laquelle chaque serveur peut accéder.

  1. Facultatif : lorsque le serveur est arrêté, si vous souhaitez augmenter ses performances, exécutez les commandes SQL suivantes sur la base de données :  
  `create index rt_cpr_submitted_time on MyUCDDatabase.rt_app_process_request(submitted_time);`  
  `create index rt_cpr_submitted_time on MyUCDDatabase.rt_comp_process_request(component_id, submitted_time);`  
  Indiquez le nom de votre base de données pour `MyUCDDatabase`.
  
  <!-- Ross says that this will not be necessary for versions 6.2.4.1 and later if he gets his code changes in. -->

  1. Démarrez le serveur. 

    **Remarque :** Le démarrage du serveur IBM UrbanCode Deploy risque de prendre plus de temps que d'habitude. S'il ne démarre pas, ou s'il ne fonctionne pas normalement, supprimez les fichiers correctifs et redémarrez-le. Les fichiers correctifs n'affectent pas le serveur de manière définitive.

1. Certaines versions d'IBM UrbanCode Deploy requièrent un correctif supplémentaire pour que le serveur puisse se connecter à DevOps Connect. Si vous utilisez IBM UrbanCode Deploy versions 6.2 à 6.2.1.2, vous devez installer le correctif supplémentaire suivant sur le serveur :
  1. Téléchargez le correctif : [http://public.dhe.ibm.com/software/products/UrbanCode/plugins/ucsync/patches/ibmucd/ucd-6.2.1.1-WI149200-CLI-Updates-for-UCSync.jar](http://public.dhe.ibm.com/software/products/UrbanCode/plugins/ucsync/patches/ibmucd/ucd-6.2.1.1-WI149200-CLI-Updates-for-UCSync.jar).
  1. Arrêtez le serveur.
  1. Placez le fichier correctif dans le dossier <code><em>application_data</em>/patches</code>.
  1. Démarrez le serveur.

1. Créez une intégration entre DevOps Connect et le serveur IBM UrbanCode Deploy :  

  **Important :** Lors de la première exécution de l'intégration, DevOps Connect extrait les données des 90 jours précédents. Si vous disposez d'un grand volume de données de déploiement, ce processus peut durer longtemps. Pour extraire les données sur une durée inférieure à 90 jours, voir [Traitement des incidents](uc_insights_connect_ucd.html#troubleshooting).
  1. Dans IBM UrbanCode Deploy, créez un jeton d'authentification. Voir [Jetons](https://www.ibm.com/support/knowledgecenter/SS4GSP_6.2.4/com.ibm.udeploy.admin.doc/topics/security_token.html).
  1. Dans DevOps Connect, cliquez sur **Integrations**, puis sur **Add New**.
  1. Indiquez un nom et une description pour l'intégration. L'emplacement par défaut de DevOps Connect est `https://hostname:8443/`, où `hostname` est le nom d'hôte du système qui héberge DevOps Connect.
  1. Dans la liste **Integration Type**, sélectionnez **IBM UrbanCode Deploy for Cloud Reporting**.
  1. Dans la zone **Server URI**, entrez l'URL publique du serveur IBM UrbanCode Deploy, par exemple `https://my_UCD.example.com:8447`.
  1. Dans la zone **Authentication Token**, entrez ou collez le jeton d'authentification généré par IBM UrbanCode Deploy.
  1. Dans la zone **Admin User**, entrez une liste d'IBMid séparés par des virgules pour donner accès à l'interface DevOps Connect.
  1. Facultatif : cliquez sur **Run Integration** pour exécuter l'intégration immédiatement. Par défaut, les intégrations s'exécutent toutes les minutes.
  1. Cliquez sur **Save**.

  ![Configuration de l'intégration dans DevOps Connect](images/uc_insights_dc_integration.gif)

Vos données sont maintenant synchronisées avec Delivery Insights. Vous pouvez désormais créer et afficher des rapports qui reposent sur ces données. Mappez ensuite les environnements de vos serveurs IBM UrbanCode Deploy à des environnements logiques dans Delivery Insights.

## Mappage d'environnements à des rapports
{: #mapping}

### Environnements logiques

Delivery Insights regroupe vos environnements IBM UrbanCode Deploy (également appelés *environnements physiques*) en un ou plusieurs environnements logiques. Vous pouvez ainsi collecter des environnements en groupes qui sont pertinents pour vous et votre organisation. Par exemple, si vous disposez de plusieurs environnements de production pour plusieurs applications, vous pouvez regrouper tous ces environnements en un seul environnement logique et combiner les mesures de tous ces environnements en un seul tableau de bord d'environnement de production. Le mappage s'effectue par chaîne de recherche. Vous pouvez donc regrouper les environnements comme vous le souhaitez en fonction de vos serveurs IBM UrbanCode Deploy.

### Environnements logiques par défaut

Par défaut, vos rapports incluent des environnements logiques qui correspondent aux environnements IBM UrbanCode Deploy grâce à des chaînes. Par exemple, tous les environnements dont le nom comporte "dev" sont mappés à l'environnement logique DEV, et tous les environnements dont le nom inclut "prod" sont mappés à l'environnement logique PROD.

![Environnements logiques par défaut](images/uc_insights_mapping.gif)

### Mappage des environnements à des environnements logiques

Vous pouvez mapper manuellement des environnements physiques à des environnements logiques, ou vous pouvez utiliser des masques pour associer dynamiquement des environnements physiques à des environnements logiques.

Pour mapper des environnements physiques à des environnements logiques à l'aide d'un masque, procédez comme suit :

1. Dans {{site.data.keyword.DRA_short}}, cliquez sur **Delivery Insights > Map Environments**.
1. Cliquez sur un environnement logique existant ou sur **Add Logical Environment**.
1. Dans les paramètres de l'environnement logique, sous **Patterns**, cliquez sur **Add Pattern**.
1. Indiquez un masque pour les noms d'environnement. Vous pouvez utiliser l'astérisque (*) comme caractère générique. Par exemple, le masque `env` correspond aux environnements `env1`, `env2` et `env`.
1. Vérifiez que l'environnement logique contient les environnements que vous souhaitez.

Pour mapper manuellement des environnements à des environnements logiques, cliquez sur **Add Manually** et sélectionnez les environnements à ajouter ou à retirer.

![Configuration de l'intégration dans DevOps Connect](images/uc_insights_mapping_manually.gif)

Maintenant que vous avez mappé des environnements à des environnements logiques, vous pouvez agréger les informations des rapports en fonction de ces environnements logiques.

## Création de rapports

Pour créer un rapport, ouvrez {{site.data.keyword.DRA_short}}, cliquez sur **Delivery Insights > Reports**, puis sur **Add Report**. 

Dans le rapport, vous pouvez ajouter des cartes dans la section **Metrics**, filtrer l'activité sous **Recent application activity** et ajouter des graphiques dans la section **Report Details**. Vous pouvez appliquer un filtre et une personnalisation individuelle à chaque graphique de la section **Report Details**. Pour afficher les données brutes derrière un graphique, cliquez sur le bouton des paramètres du graphique en haut à droite de ce dernier, puis cliquez sur **Report Data**.

Pour modifier l'ordre des graphiques, cliquez sur le bouton des paramètres en haut à droite de la page, puis cliquez sur **Edit Chart Layout**. Vous pouvez ensuite faire glisser et déposer les graphiques pour définir l'ordre du rapport.

## Partage de rapports
Par défaut, vous ne pouvez afficher que vos rapports Delivery Insights. Vous pouvez partager un rapport avec d'autres utilisateurs de votre organisation Bluemix. Pour ce faire, ouvrez le rapport et cliquez sur le bouton des paramètres situé en haut à droite de ce dernier, puis cliquez sur **Share**.  

![Partage d'un rapport](images/uc_insights_sharing.gif).

## Création de rapports d'audit

Les rapports d'audit affichent une liste complète de toutes les activités qui correspondent aux filtres que vous avez définis, sous forme de PDF. Pour créer un rapport d'audit, cliquez sur **Delivery Insights > Create Audit Report**. Indiquez ensuite les informations relatives au rapport, notamment un nom. Définissez également le contexte du rapport, par exemple, pour une application, un environnement logique ou un environnement sur un serveur IBM UrbanCode Deploy (un environnement physique). A partir de là, sélectionnez les données à afficher dans le rapport et cliquez sur **Create**. 

## Traitement des incidents
{: #troubleshooting}

Si de nombreuses demandes de processus de composant et d'application sont stockées dans votre base de données sur le serveur IBM UrbanCode Deploy, des erreurs sont susceptibles de se produire lors du processus d'extraction. Un message similaire au texte suivant est enregistré dans le journal de sortie du serveur :

`ORA-01652: unable to extend temp segment by 128 in tablespace TEMP`

Pour contourner ce comportement, éditez le fichier `plugin.properties` pour que le plug-in réduise la valeur du nombre de jours de données à extraire. Le fichier `plugin.properties` se trouve dans le répertoire `~/.ibm/cloud-sync/plugins/settings/reporting-ucd-plugin/` sur l'ordinateur sur lequel vous avez installé DevOps Connect. Editez la ligne suivante pour supprimer le signe dièse (#) et réduire le nombre de jours :

`#numDaysToRetrieve=90`

Par exemple, modifiez la ligne comme suit pour n'extraire les données que sur les 30 derniers jours :

`numDaysToRetrieve=30`

Sauvegardez le fichier, puis exécutez à nouveau l'intégration. Examinez les journaux du serveur pour vérifier que l'erreur ne se produit plus.
