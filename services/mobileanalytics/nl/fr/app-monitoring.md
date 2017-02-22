---

copyright:
  years: 2015, 2017
lastupdated: "2017-01-10"

---
{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen:.screen}
{:codeblock:.codeblock}

# Surveillance d'applications à l'aide de {{site.data.keyword.mobileanalytics_short}}
{: #monitoringapps}

{{site.data.keyword.mobileanalytics_full}} fournit des fonctions de surveillance et d'analyse pour vos applications mobiles. Le logiciel SDK
du client {{site.data.keyword.mobileanalytics_short}} vous permet d'enregistrer des journaux d'application et de surveiller les données. Les développeurs peuvent contrôler le moment auquel ces données doivent être envoyées au service {{site.data.keyword.mobileanalytics_short}}. Lorsque
des données sont envoyées à {{site.data.keyword.mobileanalytics_short}}, vous pouvez utiliser la console
{{site.data.keyword.mobileanalytics_short}} pour dégager des enseignements des analyses de vos applications mobiles, de vos appareils et des journaux
de l'application.
{: shortdesc}

<!--

## Visualizing data with custom charts
{: #custom-charts}

You can visualize the collected analytics data in your analytics repository. This visualization is a powerful way to inspect data for specific use cases. You can create charts with data that is already collected by Operational Analytics, in addition to custom data that you report.


### Creating custom charts for app logs
{: #custom-charts-client-logs}

You can create a custom chart for app logs that contain log information that is sent with the Logger API for the platform. The log information also includes contextual information about the device, including environment, app name, and app version.

In this example, you use app log data to create a flow chart. The final graph shows the distribution of log levels in a specific app. You also have the following data available to show in a chart:

* Specific data
  * Log level
* Message data
  * Timestamp
* Device OS contextual data
  * Application name
  * Application version
  * Device OS
* Device contextual data
  * Device ID
  * Device model
  * Device OS version


1. Make sure that you have an application that is collecting device logs or gathering analytics.
2. In the {{site.data.keyword.mobileanalytics_short}} console, click the **Custom Charts** tab on the **Dashboard** page. You can create a chart that is based on the analytics messages that were sent to the server.
3. Click **Create Chart** to create a new custom chart and provide the following values:
  * Chart Title: Application and Log Levels
  * Event Type: App Logs
  * Chart Type: Flow Chart
5. Click the **Chart Definition** tab and provide the following values:
  * Source: Application Name
  * Destination: Log Level
  * Property: your application name
7. Click **Save**

### Exporting custom data
{: #export-custom-data}

You can export the data from each custom chart into JSON, XML, or CSV format.

The structure of the exported data depends on the chart that is being exported. To export data, click the export icon at the upper right of the custom chart.



### Exporting and importing custom chart definitions
{: #export-import-custom}

You can import and export custom chart definitions programmatically or manually in the {{site.data.keyword.mobileanalytics_short}} Dashboard.

Ensure that you have at least one custom chart in the {{site.data.keyword.mobileanalytics_short}} Dashboard.
In this example, you manually export and import custom chart definitions.

1. In the {{site.data.keyword.mobileanalytics_short}} console, click the **Custom Charts** tab in the **Dashboard** page.
2. To export the custom chart definitions, click **Export Charts**. This action displays a dialog to save a `customChartsDefinition.json` file.
3. Choose a location to save the file.
4. Click the **Delete Chart** icon next to each custom chart to delete all custom charts.
5. To import a custom chart definition, click **Import Charts**. This action displays a dialog to choose a file.
6. Choose the `customChartsDefinition.json` file that you previously exported to open.

You can also export and import custom chart definitions programmatically by using your HTTP client of choice (for example, CURL or postman):
* The GET endpoint for export is `http://mobile-analytics-dashboard.ng.bluemix.net/analytics-service/rest/data/customCharts/`.
* The POST endpoint for import is `http://mobile-analytics-dashboard.ng.bluemix.net/analytics-service/rest/data/customCharts/import`.

**Note**: If you import a custom chart definition that exists, you end up with duplicate definitions, which also means that the {{site.data.keyword.mobileanalytics_short}} Dashboard shows duplicate custom charts.

-->

## Définition d'alertes
{: #alerts}

Vous pouvez définir des seuils dans les définitions d'alerte dans la console {{site.data.keyword.mobileanalytics_short}} pour un meilleur contrôle
de vos activités.

Vous pouvez configurer des seuils qui, s'ils sont dépassés, déclenchent des alertes et entraînent l'envoi de notifications au moniteur de la console
{{site.data.keyword.mobileanalytics_short}}. Les alertes déclenchées peuvent être visualisées dans la console ou gérées par un webhook
personnalisé. <!-- This feature provides a proactive means of detecting app log errors, server log errors, extended periods of network latency, and authentication failures.--> Cette fonction permet de détecter de façon proactive les erreurs dans les journaux d'application, ainsi que les erreurs dans les journaux serveur signalant
des pannes d'application. La mise en place d'alertes et de seuils réactifs vous évite d'avoir à parcourir vos données et à définir des seuils avec un niveau de granularité élevé.

### Création d'une définition d'alerte pour les journaux d'application
{: #alert-def-client-logs}

Vous pouvez créer une définition d'alerte qui repose sur des journaux d'application.

Dans cet exemple, vous utilisez des données de journal d'application pour créer une définition d'alerte. L'alerte surveille tous les journaux
d'application qui
ont été reçus au cours des 5 dernières minutes, et procède à une vérification toutes les 5 minutes, jusqu'à ce que la définition d'alerte soit
désactivée ou supprimée. Une alerte est déclenchée pour chaque périphérique qui a envoyé au moins 3 journaux d'erreurs d'application avec le même nom et la même version
d'application.

1. Dans la console {{site.data.keyword.mobileanalytics_short}}, cliquez sur **Définitions** pour accéder à la page Définitions
d'alerte.
2. Cliquez sur **Créer une alerte** pour créer une alerte.
3. Indiquez les valeurs suivantes :
	* Nom de l'alerte : Alerte pour les journaux d'application
	* Message : Alerte de message d'erreur
	* Fréquence des requêtes : 5 minutes
	* Type d'événement : Journaux d'application
		* Propriété : Niveau de journalisation
			* Valeur : Erreur
			* Seuil
				* Type de seuil : Total pour instance d'application

					**Remarque** : si vous choisissez l'option Moyenne pour application, la moyenne de journaux d'application est calculée en
fonction du nombre de
périphériques. Par exemple, si vous possédez deux périphériques et que l'un d'eux envoie six journaux d'application tandis que l'autre en envoie trois, la
moyenne est de
4,5 journaux d'application.
				* Opérateur : Est supérieur ou égal à 3
	<!-- insert alert definition tab image? -->

4. Cliquez sur **Suivant** et indiquez la valeur suivante :
	* Méthode : Console Analytics uniquement

		**Remarque** : Choisissez l'option Console Analytics et publication sur le réseau si vous souhaitez envoyer
également un message POST avec un contenu JSON à votre URL personnalisée. Les zones suivantes sont disponibles lorsque vous choisissez cette option :
		* Adresse URL de publication sur le réseau
        * En-têtes
        * Type d'authentification
5. Cliquez sur **Sauvegarder**.

Vous avez créé une définition d'alerte qui déclenche une alerte toutes les 5 minutes si le nombre de journaux d'erreurs d'application est supérieur ou
égal
à 3.

### Création d'une définition d'alerte pour les pannes d'application
{: #alert-def-app-crash}

Vous pouvez créer une définition d'alerte basée sur les pannes d'application.

Dans cet exemple, vous utilisez des données de panne d'application pour créer une définition d'alerte. L'alerte surveille toutes les pannes d'application qui se sont produites au cours des 2 dernières minutes, et continue la vérification toutes les 2 minutes, jusqu'à ce que la définition d'alerte soit désactivée ou supprimée. Une alerte est déclenchée pour chaque application qui est tombée en panne au moins 5 fois. Pour plus d'informations sur les pannes d'application, voir [Pannes d'application](#app_crash).

1. Dans la console {{site.data.keyword.mobileanalytics_short}}, cliquez sur **Définitions** pour afficher la page
Définitions d'alertes.
2. Cliquez sur **Créer une alerte**.
3. Indiquez les valeurs suivantes :
	* Nom d'alerte : Alerte pour les pannes d'application
	* Message : Alerte de panne d'application
	* Fréquence des requêtes : Pannes d'application
		* Fréquence des requêtes : 2 minutes
	* Type d'événement : Pannes d'application
		* Nom d'application : N'importe quelle application
		* Version d'application : N'importe quelle version
    * Seuil
      * Type de seuil : Nombre de pannes
      * Opérateur : Est supérieur ou égal à 5
4. Cliquez sur l'onglet **Méthode de distribution** et indiquez la valeur suivante :
  * Méthode : Console Analytics uniquement

    **Remarque** : Choisissez l'option **Console Analytics et publication sur le réseau** si vous souhaitez envoyer également un message POST avec un contenu JSON à votre URL personnalisée. Les zones suivantes sont disponibles lorsque vous choisissez cette option :
      * Adresse URL de publication sur le réseau (obligatoire)
      * En-têtes (facultative)
      * Type d'authentification (obligatoire)
5. Cliquez sur **Sauvegarder**.

### Gestion des définitions d'alerte
{: #managing-alert-definitions}

Dans cet exemple, vous gérez vos définitions d'alerte à partir de la page Gestion des alertes.

1. Dans la console {{site.data.keyword.mobileanalytics_short}}, cliquez sur **Journaux**. Cette action ouvre la page
Journaux des alertes.
2. Facultatif : Sélectionnez ou désélectionnez la case à cocher située sous la colonne **Activé** pour activer ou désactiver une définition d'alerte donnée.
3. Facultatif : Cliquez sur l'icône **Dupliquer** si vous souhaitez créer une copie d'une définition d'alerte et modifier certaines valeurs.
4. Facultatif : Cliquez sur l'icône **Crayon** si vous souhaitez éditer une définition d'alerte.
5. Facultatif : Cliquez sur l'icône **Corbeille** si vous souhaitez supprimer une définition d'alerte.

### Affichage des détails d'alerte
{: #viewing-alert-details}

Dans cet exemple, vous affichez les détails de vos alertes déclenchées à partir de la page Journal des alertes.

1. Dans la console {{site.data.keyword.mobileanalytics_short}}, cliquez sur **Journaux**. Cette action permet d'afficher la page Journal des alertes.
2. Cliquez sur l'icône **+** pour n'importe laquelle des alertes. Cette action permet d'afficher les sections **Définition d'alerte** et **Instances d'alerte**.

    **Remarque** : Si la définition d'alerte correspondante n'a pas été supprimée ou modifiée, vous pouvez l'éditer en cliquant sur **Editer une alerte**. Sinon, le bouton **Editer une alerte** n'est pas disponible et le message suivant s'affiche :

    `Depuis, cette définition d'alerte a été modifiée ou supprimée. `

3. Facultatif : Sélectionnez une alerte et cliquez sur l'icône **Corbeille** pour la supprimer.

## Surveillance de pannes d'application
{: #monitor-app-crash}

Vous pouvez consulter des informations sur les pannes de votre application dans la console
{{site.data.keyword.mobileanalytics_short}} pour mieux surveiller vos applications et résoudre leurs incidents.

### Surveillance des pannes d'application
{: #app-crash}

Sur la page **Pannes**, le tableau **Présentation des pannes** affiche les colonnes de données suivantes :

* Application : Nom d'application
* Pannes : Nombre total de pannes pour cette application
* Nombre total d'utilisations : Nombre total de fois qu'un utilisateur ouvre et ferme cette application
* Taux de pannes : Pourcentage de pannes par utilisation

Vous pouvez afficher rapidement des informations sur les pannes d'application dans le tableau **Crashes**. <!--In the **Overview** page of the **Dashboard** section,--> Le diagramme à barres
**Crashes** affiche un histogramme des pannes au fil du temps.

Vous pouvez afficher les données de panne de deux façons :

1. Afficher le taux de pannes : taux de pannes au fil du temps
2. Afficher le nombre total de pannes : nombre total de pannes au fil du temps

### Traitement des incidents liés aux pannes d'application
{: #app-crash-troubleshooting}

La page **Traitement des incidents** dans la console <!-- **Applications** section of the -->
{{site.data.keyword.mobileanalytics_short}} offre une vue granulaire des pannes de votre application grâce au tableau **Récapitulatif des pannes**. 

Le tableau **Récapitulatif des pannes** inclut les colonnes de données suivantes et peut être trié :

* Pannes
* Périphériques
* Dernière panne
* Application
* Système d'exploitation
* Message

Cliquez sur l'icône + située en regard de n'importe quelle entrée pour afficher le tableau **Détails des pannes**, qui inclut les colonnes suivantes :

* Heure de la panne
* Version de l'application
* Version du système d'exploitation
* Modèle de périphérique
* ID du périphérique
* Télécharger : lien permettant de télécharger les journaux qui ont conduit à la panne

Développez n'importe quelle entrée du tableau **Détails des pannes** pour obtenir plus de détails, y compris une trace de pile.

**Remarque** : vous remplissez le tableau **Récapitulatif des pannes** en exécutant une requête
sur les journaux d'application de niveau Fatal. Si votre application ne collecte pas de journaux d'application de niveau Fatal, aucune donnée n'est disponible.

## Surveillance des demandes de réseau
{: #monitor-network-requests}


Vous pouvez examiner les données des demandes réseau pour vos applications dans la console
{{site.data.keyword.mobileanalytics_short}}. 

Les données sont disponibles pour les mesures suivantes :
	
* Durée de la boucle - définit la durée, mesurée en ms, nécessaire pour que votre application effectue des demandes de réseau.
* Nombre de demandes - affiche la fréquence à laquelle une application effectue des demandes de réseau. Les données sont également affichées en tant que moyenne.

## Exportation de données dans dashDB
{: #dashdb}

Les données que vous voyez dans la console {{site.data.keyword.mobileanalytics_short}} ne sont qu'un exemple des enseignements
que vous pouvez glaner depuis vos données mobiles. Vous pouvez acheminer automatiquement vos données mobiles à l'entrepôt de données
{{site.data.keyword.IBM}} dashDB dans lequel vous pouvez personnaliser vos analyses, agréger vos données avec celles
de sources de données publiques et privées, et procéder à des analyses de pointe afin de dégager des informations approfondies, détaillées et sophistiquées
pour mieux comprendre et diriger votre activité.

Installez dashDB dans la console {{site.data.keyword.mobileanalytics_short}} en cliquant sur **DashDB** sur la page
**Exporter**. Une fois que vous l'avez configuré, les nouvelles données envoyées à
{{site.data.keyword.mobileanalytics_short}} sont également acheminées à dashDB sous 1 à 2 heures. 

<!--
If you have existing DashDB instances, those instances will no longer accept new data because the incoming data no longer matches the schema. Manually add columns for the new data to resume incoming data. Modifying {{site.data.keyword.mobileanalytics_short}} collection tables by adding new columns also breaks the stream of incoming data.
-->

