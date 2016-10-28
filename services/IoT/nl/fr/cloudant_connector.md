---

copyright :
  2016

---

{:new_window: target="\_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}

# Connexion et configuration d'un service historique à l'aide d'un service {{site.data.keyword.cloudant}}  
{: #cloudant_main}
Dernière mise à jour : 16 septembre 2016
{: .last-updated}

La connexion d'un service {{site.data.keyword.cloudantfull}} à votre service {{site.data.keyword.iot_full}} vous permet de stocker des données de terminal et d'y accéder. Les données de terminal sont stockées tous les jours, toutes les semaines ou tous les mois en fonction de l'intervalle que vous sélectionnez. 

Lorsque vous commencez à utiliser un service {{site.data.keyword.cloudant}} pour stocker des données de terminal, les trois bases de données suivantes sont automatiquement créées : une base de données pour l'intervalle en cours, une base de données pour l'intervalle à venir et une base de données de configuration. Des documents de conception peuvent être ajoutés à la base de données de configuration et seront copiés dans les nouvelles bases de données à mesure qu'elles seront créées. A la fin d'un intervalle, les données de terminal sont stockées dans la base de données pour le nouvel intervalle, et la nouvelle base de données est créée pour l'intervalle suivant. 

Lorsque des données de terminal sont envoyées à une base de données, elles peuvent être stockées de deux façons différentes. Si les données sont dans un format JSON valide et si le format de l'événement de terminal a pour valeur `JSON`, les données de terminal sont stockées dans le format suivant :

```json

{
  "_id": "78bf4380-3311-11e6-a747-d7b140d1a70a",
  "_rev": "2-d13912b7c089f060a4ba7369fa86e46f",
  "typeId": "t",
  "deviceType": "0",
  "eventType": "json_payload",
  "format": "json",
  "timestamp": "2016-06-15T16:54:41.464+01",
  "data": {
    "a": 22
  }
}

```

Si les données de terminal ne sont pas dans un format JSON valide et si le format n'a pas pour valeur `JSON`, les données de terminal sont stockées sous la forme d'une chaîne codée en base 64 sous la zone `payload` et dans le format suivant :

```json

{
  "_id": "80f1ce10-3311-11e6-a747-d7b140d1a70a",
  "_rev": "1-bfcbf1e74389fe4188a9425c0cd2575a",
  "payload": "eHh4eHg=",
  "typeId": "t",
  "deviceType": "0",
  "eventType": "non_json_payload",
  "format": "notjson",
  "timestamp": "2016-06-15T16:54:55.217+01"
}

```

## Avant de commencer  
{: #byb}

Avant de connecter un service {{site.data.keyword.cloudant}} à votre service {{site.data.keyword.iot_short}}, exécutez les tâches suivantes :

- Configurez un service {{site.data.keyword.cloudant}} dans le même espace Bluemix que votre instance {{site.data.keyword.iot_short_notm}} à l'aide du catalogue Bluemix. 

Vérifiez que vous disposez des privilèges de développeur dans l'organisation Bluemix et que vous êtes connecté via Bluemix. Si vous n'êtes pas connecté via Bluemix ou si vous ne disposez pas de privilèges de développeur dans cette organisation Bluemix, vous ne pourrez pas autoriser la liaison entre {{site.data.keyword.cloudant}} et {{site.data.keyword.iot_short_notm}}.

Procédez comme suit pour connecter un service {{site.data.keyword.cloudant}} :

1. Sur votre tableau de bord {{site.data.keyword.iot_short}}, cliquez sur **Extensions** dans la barre de navigation. 
2. Dans la vignette Stockage des données historiques, cliquez sur **Configuration**.
2. Tous les services {{site.data.keyword.cloudant}} disponibles au sein du même espace Bluemix que votre service {{site.data.keyword.iot_short}} sont répertoriés dans la section Configuration du stockage des données historiques. 
3. Sélectionnez le service {{site.data.keyword.cloudant}} que vous souhaitez connecter. 
4. Sélectionnez vos options de configuration {{site.data.keyword.cloudant}} :

  a. Sélectionnez un intervalle. L'intervalle contrôle la fréquence à laquelle de nouvelles bases de données sont créées pour stocker des données de terminal. De nouveaux intervalles sont créés à minuit dans le fuseau horaire sélectionné à l'aide de votre intervalle sélectionné. 

  b. Sélectionnez un fuseau horaire. L'heure définie dans le fuseau horaire sélectionné sera utilisée pour identifier les données de terminal d'intervalle à insérer et non l'heure locale sur le terminal. Les valeurs d'horodatage sur les données de terminal envoyées au service {{site.data.keyword.cloudant}} seront converties dans le fuseau horaire sélectionné au moment de définir la base de données dans laquelle les données seront saisies. 

  c. Choisissez un nom de base de données. Le nom de base de données sera `Iotp_<orgID>_<choice>_<bucket_name>`, où `<orgID>` est votre ID d'organisation, `<choice>` est le nom de base de données de votre choix, et `<bucket_name>` est une chaîne indiquant si la base de données utilise un intervalle quotidien, hebdomadaire ou mensuel. Le paramètre `<bucket_name>` utilise le format suivant :

  Pour les intervalles quotidiens, le format du paramètre `<bucket_name>` est `aaaa-mm-jj`.
  Pour les intervalles hebdomadaires, le format du paramètre `<bucket_name>` est `aaaa-sss` où `sss` indique un numéro de semaine, par exemple, `2016-s03`.
  Pour les intervalles mensuels, le format du paramètre `<bucket_name>` est `aaaa-mm`.

5. Cliquez sur **Autoriser**.
6. Cliquez sur **Confirmer** dans la boîte de dialogue d'autorisation. 

Vos données de terminal seront désormais stockées dans votre service {{site.data.keyword.cloudant}}.

## Création de nouveaux documents de conception  
{: #design_docs}

De nouveaux documents de conception sont contenus dans la base de données de configuration, et copiés sur chaque base de données créée. Le nom de la base de données de configuration est `Iotp_<orgid>_<choice>_configuration
` et reprend les mêmes paramètres que ceux relatifs aux noms de base de données décrits à l'étape 3b dans la section Avant de commencer. 

Les documents de conception par défaut contenus dans {{site.data.keyword.iot_short_notm}} implémentent les requêtes disponibles dans l'historique en cours, en plus de la fonction summarize. 

D'autres documents de conception peuvent être ajoutés à la base de données de configuration et seront copiés dans les nouvelles bases de données d'intervalle à mesure qu'elles seront créées. Pour ajouter des documents de conception à la base de données de configuration, voir la [documentation d'API Cloudant](https://docs.cloudant.com/document.html).

<!--  # Related links
{: #rellinks}
* [Querying your {{site.data.keyword.cloudant}}](link) -->
