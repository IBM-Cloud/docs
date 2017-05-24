---

copyright:
  years: 2017
lastupdated: "2017-03-14"

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}

# Connexion de serveurs IBM UrbanCode Deploy à Delivery Insights
{: #connect_ucd}

Pour afficher les données d'un serveur IBM UrbanCode Deploy dans Delivery Insights, vous devez installer un correctif sur le serveur, puis connecter ce serveur à DevOps Connect.
{:shortdesc}

## Avant de commencer

- Reportez-vous aux [conditions requises](uc_insights_prereqs.html), et notamment à la description de la configuration de DevOps Connect.
- Votre serveur IBM UrbanCode Deploy doit être à la version 6.2 ou ultérieure. 

## Procédure

1. Installez le correctif sur votre serveur IBM UrbanCode Deploy. Toutes les versions d'IBM UrbanCode Deploy requièrent un correctif pour communiquer avec DevOps Connect. 
  1. Téléchargez le correctif adapté à votre version d'IBM UrbanCode Deploy en accédant à la page suivante : [http://public.dhe.ibm.com/software/products/UrbanCode/plugins/ucsync/patches/ibmucd/](http://public.dhe.ibm.com/software/products/UrbanCode/plugins/ucsync/patches/ibmucd/)

  1. Procédez à l'extraction du fichier. Il contient un ou plusieurs fichiers correctifs que vous devez ajouter au serveur. 

  1. Arrêtez le serveur. Voir [Démarrage et arrêt du serveur](https://www.ibm.com/support/knowledgecenter/SS4GSP_6.2.3/com.ibm.udeploy.install.doc/topics/run_server.html).

  1. Placez les fichiers correctifs dans le dossier <code><em>application_data</em>/patches</code>, où <code><em>application_data</em></code> est le dossier des données d'application. Le dossier des données d'application par défaut est `/opt/ibm-ucd/server/appdata` sur Linux et `C:\Program Files\ibm-ucd\server\appdata` sous Windows. Sur les systèmes à haute disponibilité, le dossier des données d'application se trouve toujours sur une unité réseau partagée à laquelle chaque serveur peut accéder. 

  1. Facultatif : lorsque le serveur est arrêté, si vous souhaitez augmenter ses performances, exécutez les commandes SQL suivantes sur la base de données :   
  ```
  create index rt_cpr_submitted_time on MyUCDDatabase.rt_app_process_request(submitted_time);
  create index rt_cpr_submitted_time on MyUCDDatabase.rt_comp_process_request(component_id, submitted_time);
  ```
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
  1. Dans IBM UrbanCode Deploy, créez un jeton d'authentification. Voir [Jetons](https://www.ibm.com/support/knowledgecenter/SS4GSP_6.2.3/com.ibm.udeploy.admin.doc/topics/security_token.html).
  1. Dans DevOps Connect, cliquez sur **Integrations**, puis sur **Add New**.
  1. Indiquez un nom et une description pour l'intégration. L'emplacement par défaut de DevOps Connect est `https://hostname:8443/`, où `hostname` est le nom d'hôte du système qui héberge DevOps Connect.
  1. Dans la liste **Integration Type**, sélectionnez **IBM UrbanCode Deploy for Cloud Reporting**.
  1. Dans la zone **Server URI**, entrez l'URL publique du serveur IBM UrbanCode Deploy, par exemple `https://my_UCD.example.com:8447`.
  1. Dans la zone **Authentication Token**, entrez ou collez le jeton d'authentification généré par IBM UrbanCode Deploy.
  1. Dans la zone **Admin User**, entrez une liste d'IBMid séparés par des virgules pour donner accès à l'interface DevOps Connect.
  1. Facultatif : cliquez sur **Run Integration** pour exécuter l'intégration immédiatement. Par défaut, les intégrations s'exécutent toutes les minutes.
  1. Cliquez sur **Save**.

  ![Configuration de l'intégration dans DevOps Connect](images/uc_insights_dc_integration.gif)

Vos données sont maintenant synchronisées avec Delivery Insights. Vous pouvez désormais créer et afficher des rapports qui reposent sur ces données. 

## Traitement des incidents
{: #troubleshooting}

Si de nombreuses demandes de processus de composant et d'application sont stockées dans votre base de données sur le serveur IBM UrbanCode Deploy, des erreurs sont susceptibles de se produire lors du processus d'extraction. Un message similaire au texte suivant est enregistré dans le journal de sortie du serveur : 

`ORA-01652: unable to extend temp segment by 128 in tablespace TEMP`

Pour contourner ce comportement, éditez le fichier `plugin.properties` pour que le plug-in réduise la valeur du nombre de jours de données à extraire. Le fichier `plugin.properties` se trouve dans le répertoire `~/.ibm/cloud-sync/plugins/settings/reporting-ucd-plugin/` sur l'ordinateur sur lequel vous avez installé DevOps Connect. Editez la ligne suivante pour supprimer le signe dièse (#) et réduire le nombre de jours : 

`#numDaysToRetrieve=90`

Par exemple, modifiez la ligne comme suit pour n'extraire les données que sur les 30 derniers jours : 

`numDaysToRetrieve=30`

Sauvegardez le fichier, puis exécutez à nouveau l'intégration. Examinez les journaux du serveur pour vérifier que l'erreur ne se produit plus. 
