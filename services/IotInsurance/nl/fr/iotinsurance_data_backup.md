---

copyright:
  years: 2016, 2017
lastupdated: "2017-03-22"
---

<!-- Common attributes used in the template are defined as follows: -->
{:new_window: target="blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}



<!-- {{site.data.keyword.iotinsurance_full}}  {{site.data.keyword.iotinsurance_short}}  -->

# Sauvegarde de données
Vous pouvez sauvegarder vos données {{site.data.keyword.iotinsurance_full}} en répliquant la base de données {{site.data.keyword.cloudantfull}}.
{:shortdesc}

Le tableau suivant illustre les bases de données {{site.data.keyword.iotinsurance_short}} qui sont stockées dans {{site.data.keyword.iotinsurance_full}}.

*Tableau 1 : Bases de données {{site.data.keyword.iotinsurance_short}}*

Noms de base de données| Fréquence de modification| Raison de la modification | Sauvegarde requise | Commentaires
------------- | -------------| -------------| -------------| -------------
favorites|Administration|Nouvelle action d'administrateur|OUI|-
Devices|Administration|Ajout ou retrait de nouveaux terminaux ou utilisateurs|OUI| Le transformateur génère dynamiquement une table en mémoire et la remplit avec les données issues du fournisseur de terminaux. Pour les passerelles connectées directement, cette table stocke les terminaux.
hazardevents|Aléatoire|Détection d'un nouvel événement de bouclier|OUI|-
Jscode|Administration|Déploiement d'un nouveau code JS pour les boucliers|OUI*| L'administrateur a la possibilité d'ignorer la sauvegarde et de déployer une nouvelle version du code JS.
Promotions|Administration|Ajout d'une nouvelle promotion|OUI|-
shieldassociations|Administration|Ajout d'un nouvel utilisateur ou d'un nouveau bouclier|OUI|-
Shields|Administration|Ajout d'un nouveau bouclier|OUI|-
Users|Administration|Ajout d'un nouvel utilisateur|OUI|-
aggregation|-|-|NON|Peut être régénérée.
aggregationschedule|-|-| NON|Peut être régénérée.

Pour sauvegarder les données {{site.data.keyword.iotinsurance_short}}, procédez comme suit :

## Création d'une réplique d'instance {{site.data.keyword.cloudant_short_notm}}
{: #createinstance}
Créez une réplique d'instance {{site.data.keyword.cloudant}} à l'aide des [instructions de réplication {{site.data.keyword.cloudant}} ![Icône de lien externe](../../icons/launch-glyph.svg)](https://docs.cloudant.com/replication.html). Pour la reprise après incident, créez la réplique à un autre emplacement que celui de votre service {{site.data.keyword.iotinsurance_short}} d'origine. Par exemple, si votre instance d'origine est à Dallas, la réplique peut se trouver à Londres.

## Localisation des données d'identification et des URL
{: #locate_credentials}
Localisez les données d'identification et les URL de votre instance {{site.data.keyword.cloudant}} d'origine et de votre instance répliquée.
1. Ouvrez le service {{site.data.keyword.cloudant}}.
2. Cliquez sur l'onglet **Données d'identification pour le service** qui figure sous le nom du service.
3. Cliquez sur **Afficher les données d'identification**.
4. Prenez note du nom d'utilisateur, du mot de passe et de l'URL.

## Création de nouvelles tâches de réplication
{: #create_replication}
Créez une tâche de réplication pour chaque base de données qui doit être sauvegardée. Les bases de données qui doivent être sauvegardées sont répertoriées dans le tableau 1 de la section précédente.

1. Ouvrez votre console {{site.data.keyword.Bluemix_notm}}.

2. Ouvrez le service {{site.data.keyword.cloudant}} d'origine.

3. Cliquez sur **Lancer** pour ouvrir le tableau de bord {{site.data.keyword.cloudant}}.

4. Dans le menu, sélectionnez **Réplication**.

5. Entrez l'URL de la base de données d'origine dans la section Base de données source. Chaque URL de base de données est au format https://<CloudantbaseURL>/<database_name>.  Par exemple, l'URL de la base de données hazardevents est https://<CloudantbaseURL>/hazardevents.

6. Entrez l'URL de la nouvelle base de données dans la section Base de données cible.

7. **Important :** Ne sélectionnez pas **Définir cette réplication comme continue**.  En effet, la réplication continue dégrade considérablement les performances.

8. Cliquez sur **Répliquer des données**.  

9. (Facultatif) Etant donné que les tâches de réplication suivantes écrasent les données précédentes, il peut être judicieux d'exporter les données dans un fichier CSV.  Pour obtenir les instructions correspondantes, voir [Export Cloudant JSON as CSV, RSS, or iCal ![Icône de lien externe](../../icons/launch-glyph.svg)](https://developer.ibm.com/clouddataservices/2015/09/22/export-cloudant-json-as-csv-rss-or-ical/){: new_window}.

10. Répétez ces étapes pour chaque base de données.

## Exécution d'une sauvegarde
{: #run_backup}
Après avoir créé les tâches de réplication, vous pouvez relancer l'exécution des sauvegardes à tout moment.
1. Ouvrez votre console {{site.data.keyword.Bluemix_notm}}.
2. Ouvrez votre service {{site.data.keyword.cloudant}} d'origine.
3. Cliquez sur **Lancer** pour ouvrir le tableau de bord {{site.data.keyword.cloudant}}.
4. Dans le menu, cliquez sur **Réplication**, puis sélectionnez **Toutes les réplications**.
5. Sélectionnez toutes les bases de données, puis relancez chaque réplication. Vous pouvez vérifier le statut des travaux en cours en cliquant sur **Réplications actives**.
6. Lorsque toutes les réplications sont terminées, vous pouvez exporter les données dans un fichier à plat CSV.

## Restauration des données
{: #restore_data}
Vous pouvez restaurer les données à partir d'une base de données répliquée ou en chargeant un fichier CSV sauvegardé.
1. Ouvrez votre console {{site.data.keyword.Bluemix_notm}}.
2. Arrêtez le service {{site.data.keyword.iotinsurance_short}}.
3. Restaurez les données en procédant de l'une des façons suivantes :
  - Chargez les données depuis un fichier de sauvegarde CSV directement dans l'instance Cloudant principale.
  - Créez une tâche de réplication ayant pour source la base de données répliquée et pour cible la base de données d'origine. Cette tâche déplace les données répliquées dans la base de données d'origine.
4. Exécutez les scripts suivants pour recréer des documents de conception et restaurer l'intégrité référentielle.  Les scripts se trouvent sur le [site GitHub des exemples d'API {{site.data.keyword.iotinsurance_short}} ![Icône de lien externe](../../icons/launch-glyph.svg)](https://github.com/IBM-Bluemix/iot4i-api-examples-nodejs/){: new_window}.
  - iot4i-api/wearable-framework/auto-create/create.sh - Ce script recrée les documents de conception dans {{site.data.keyword.cloudant}}.
  - iot4i-api/wearable-framework/health/check-relations - Ce script réétablit l'intégrité référentielle. Par exemple, il effectue les modifications nécessaires lorsqu'un bouclier est supprimé mais que l'association à un utilisateur existe toujours.
