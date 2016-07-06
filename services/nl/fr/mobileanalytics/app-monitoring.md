---

copyright:
  years: 2015, 2016

---
# Surveillance d'applications à l'aide de {{site.data.keyword.mobileanalytics_short}}
{: #monitoringapps}
*Dernière mise à jour jour : 6 mai 2016*
{: .last-updated}

{{site.data.keyword.mobileanalytics_full}} fournit des fonctions de surveillance et d'analyse pour vos applications mobiles. Le logiciel SDK du client {{site.data.keyword.mobileanalytics_short}} vous permet d'enregistrer les journaux client et de surveiller les données. Les développeurs peuvent contrôler le moment auquel ces données doivent être envoyées au service {{site.data.keyword.mobileanalytics_short}}. Lorsque les données sont fournies à {{site.data.keyword.mobileanalytics_short}}, vous pouvez utiliser le tableau de bord {{site.data.keyword.mobileanalytics_short}} pour obtenir des perspectives d'analyse relatives à vos applications et périphériques mobiles, ainsi que les journaux client.
{: shortdesc}

## Visualisation de données à l'aide de graphiques personnalisés
{: #custom-charts}

Vous pouvez visualiser les données d'analyse collectées dans votre référentiel d'analyse. Cette visualisation est un moyen très efficace d'examiner les données relatives à des scénarios d'utilisation spécifiques. Vous pouvez créer des graphiques avec des données déjà collectées par une analyse opérationnelle, en plus des données personnalisées que vous communiquez.

### Création de graphiques personnalisés pour les journaux client
{: #custom-charts-client-logs}

Vous pouvez créer un diagramme personnalisé pour les journaux client contenant des informations de journal qui sont envoyées à l'API de journal d'événements pour la plateforme. Les informations de journal contiennent également des informations contextuelles sur le périphérique, à savoir l'environnement, ainsi que le nom et la version de l'application.

Dans cet exemple, vous utilisez des données de journal client pour créer un graphique de flux. Le graphique final affiche la distribution des niveaux de journalisation dans une application spécifique. Les données suivantes peuvent également être représentées dans un graphique :

* Données spécifiques
  * Niveau de journalisation
* Données de message
  * Horodatage
* Données contextuelles relatives au système d'exploitation du périphérique
  * Nom de l'application
  * Version de l'application
  * Système d'exploitation du périphérique
* Données contextuelles relatives au périphérique
  * ID du périphérique
  * Modèle de périphérique
  * Version du système d'exploitation du périphérique


1. Assurez-vous que vous disposez d'une application qui collecte des journaux de périphérique ou regroupe des données d'analyse.
2. Dans la console {{site.data.keyword.mobileanalytics_short}}, cliquez sur l'onglet **Graphiques personnalisés** sur la page du **tableau de bord** . Vous pouvez créer un graphique à partir des messages d'analyse qui ont été envoyés au serveur.
3. Cliquez sur **Créer un graphique** pour créer un nouveau graphique personnalisé et indiquez les valeurs suivantes :
  * Titre de graphique : Application et niveaux de journalisation
  * Type d'événement : Journaux client
  * Type de graphique : Graphique de flux
5. Cliquez sur l'onglet **Définition de graphique** et indiquez les valeurs suivantes :
  * Source : Nom d'application
  * Destination : Niveau de journalisation
  * Propriété : nom de votre application
7. Cliquez sur **Sauvegarder**

### Exportation de données personnalisées
{: #export-custom-data}

Vous pouvez exporter les données de chaque graphique personnalisé au format JSON, XML ou CSV.

La structure des données exportées du graphique exporté. Pour exporter des données, cliquez sur l'icône Exporter située dans l'angle supérieur droit du graphique personnalisé.



### Exportation et importation de définitions de graphique personnalisé
{: #export-import-custom}

Vous pouvez importer et exporter des définitions de graphique personnalisé à l'aide d'un programme ou manuellement dans le tableau de bord {{site.data.keyword.mobileanalytics_short}}.

Assurez-vous que vous disposez d'au moins un graphique personnalisé dans le tableau de bord {{site.data.keyword.mobileanalytics_short}}.
Dans cet exemple, vous exportez et importez manuellement des définitions de graphique personnalisé.

1. Dans la console {{site.data.keyword.mobileanalytics_short}}, cliquez sur l'onglet **Graphiques personnalisés** sur la page du **tableau de bord** .
2. Pour exporter les définitions de graphique personnalisé, cliquez sur **Exporter les graphiques**. Cette action affiche une boîte de dialogue permettant de sauvegarder un fichier `customChartsDefinition.json`.
3. Choisissez l'emplacement de sauvegarde du fichier.
4. Cliquez sur l'icône **Supprimer un graphique** située en regard de chaque graphique personnalisé pour supprimer tous les graphiques personnalisés.
5. Pour importer une définition de graphique personnalisé, cliquez sur **Importer des graphiques**. Cette action affiche une boîte de dialogue permettant de sélectionner un fichier.
6. Choisissez le fichier `customChartsDefinition.json` que vous avez précédemment exporté afin de l'ouvrir.

Vous pouvez également exporter et importer les définitions de graphique personnalisé à l'aide d'un programme en utilisant le client HTTP de votre choix (par exemple, CURL ou postman) :
* Le noeud final GET pour l'exportation est `http://mobile-analytics-dashboard.ng.bluemix.net/analytics-service/rest/data/customCharts/`.
* Le noeud final POST pour l'importation est `http://mobile-analytics-dashboard.ng.bluemix.net/analytics-service/rest/data/customCharts/import/`.

**Remarque** : Si vous importez une définition de graphique personnalisé qui existe déjà, une définition en double est créée, et, par conséquent, le tableau de bord {{site.data.keyword.mobileanalytics_short}} affiche des graphiques personnalisés dupliqués.

## Définition d'alertes
{: #alerts}

Vous pouvez définir des seuils dans les définitions d'alerte dans la console
{{site.data.keyword.mobileanalytics_short}} pour un meilleur contrôle de vos
activités.

Vous pouvez configurer des seuils, qui, s'ils sont dépassés, déclenchent des alertes et entraînent l'envoi de notifications à la console {{site.data.keyword.mobileanalytics_short}}. Les alertes déclenchées peuvent être visualisées sur la console ou gérées par un webhook personnalisé. Cette fonction offre un moyen proactif de détecter des erreurs de journal client, des erreurs de journal serveur, des périodes prolongées de temps d'attente du réseau et des échecs d'authentification. La mise en place d'alertes et de seuils réactifs vous évite d'avoir à parcourir vos données et à définir des seuils avec un niveau de granularité élevé.

### Création d'une définition d'alerte pour les journaux client
{: #alert-def-client-logs}

Vous pouvez créer une définition d'alerte basée sur les journaux client.

Dans cet exemple, vous utilisez des données de journal client pour créer une définition d'alerte. L'alerte surveille tous les journaux client qui ont été reçus au cours des 5 dernières minutes, et continue la vérification toutes les 5 minutes, jusqu'à ce que la définition d'alerte soit désactivée ou supprimée. Une alerte est déclenchée pour chaque périphérique qui a envoyé au moins 3 journaux d'erreurs client avec le même nom et la même version d'application.

1. Dans la console {{site.data.keyword.mobileanalytics_short}}, cliquez sur l'icône qui représente une sonnette pour accéder à la page **Journal des alertes**.
2. Accédez à la page **Gestion des alertes** et cliquez sur **Créer une alerte**.
3. Indiquez les valeurs suivantes :
	* Nom d'alerte : Alerte pour les journaux client
	* Message : Alerte de message d'erreur
	* Fréquence des requêtes : 5 minutes
	* Type d'événement : Journaux client
		* Propriété : Niveau de journalisation
			* Valeur : Erreur
			* Seuil
				* Type de seuil : Total pour instance d'application

					**Remarque** : Si vous choisissez l'option Moyenne pour application, la moyenne de journaux client est calculée en fonction du nombre de périphériques. Par exemple, si vous possédez deux périphériques et l'un d'eux envoie six journaux client tandis que l'autre en envoie trois, la moyenne est de 4,5 journaux client.
				* Opérateur : Est supérieur ou égal à 3
	<!-- insert alert definition tab image? -->

4. Cliquez sur **Suivant** ou sur l'onglet **Méthode de distribution** et indiquez la valeur suivante :
	* Méthode : Console Analytics uniquement

		Remarque : Choisissez l'option Console Analytics et publication sur le réseau si vous souhaitez envoyer également un message POST avec un contenu JSON à votre URL personnalisée. Les zones suivantes sont disponibles lorsque vous choisissez cette option :
		* Adresse URL de publication sur le réseau
        * En-têtes
        * Type d'authentification
5. Cliquez sur **Sauvegarder**.

Vous avez créé une définition d'alerte qui déclenche une alerte toutes les 5 minutes si le nombre de journaux d'erreurs client est supérieur ou égal à 3.

### Création d'une définition d'alerte pour les pannes d'application
{: #alert-def-app-crash}

Vous pouvez créer une définition d'alerte basée sur les pannes d'application.

Dans cet exemple, vous utilisez des données de panne d'application pour créer une définition d'alerte. L'alerte surveille toutes les pannes d'application qui se sont produites au cours des 2 dernières minutes, et continue la vérification toutes les 2 minutes, jusqu'à ce que la définition d'alerte soit désactivée ou supprimée. Une alerte est déclenchée pour chaque application qui est tombée en panne au moins 5 fois. Pour plus d'informations sur les pannes d'application, voir [Pannes d'application](app_crash/c_op_analytics_crashes.html).

1. Dans la console {{site.data.keyword.mobileanalytics_short}}, cliquez sur l'icône **Alertes**. Cette action permet d'afficher la page Journal des alertes.
2. Cliquez sur l'onglet **Gestion des alertes**, puis sur **Créer une alerte**.
3. Indiquez les valeurs suivantes :
	* Nom d'alerte : Alerte pour les pannes d'application
	* Message : Alerte de panne d'application
	* Fréquence des requêtes : Pannes d'application
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

Dans cet exemple, vous gérez vos définitions d'alerte à partir de la page Gestion des alerte.

1. Dans la console {{site.data.keyword.mobileanalytics_short}}, cliquez sur l'icône **Alertes**. Cette action permet d'afficher la page Journal des alertes.
2. Cliquez sur l'onglet **Gestion des alertes**.
3. Facultatif : Sélectionnez ou désélectionnez la case à cocher située sous la colonne **Activé** pour activer ou désactiver une définition d'alerte donnée.
4. Facultatif : Cliquez sur l'icône **Dupliquer** si vous souhaitez créer une copie d'une définition d'alerte et modifier certaines valeurs.
5. Facultatif : Cliquez sur l'icône **Crayon** si vous souhaitez éditer une définition d'alerte.
6. Facultatif : Cliquez sur l'icône **Corbeille** si vous souhaitez supprimer une définition d'alerte.

### Affichage des détails d'alerte
{: #viewing-alert-details}

Dans cet exemple, vous affichez les détails de vos alertes déclenchées à partir de la page Journal des alertes.

1. Dans la console {{site.data.keyword.mobileanalytics_short}}, cliquez sur l'icône **Alertes**. Cette action permet d'afficher la page Journal des alertes.
2. Cliquez sur l'icône **+** pour n'importe laquelle des alertes. Cette action permet d'afficher les sections **Définition d'alerte** et **Instances d'alerte**.

    **Remarque** : Si la définition d'alerte correspondante n'a pas été supprimée ou modifiée, vous pouvez l'éditer en cliquant sur **Editer une alerte**. Sinon, le bouton **Editer une alerte** n'est pas disponible et le message suivant s'affiche :

    `Depuis, cette définition d'alerte a été modifiée ou supprimée. `

3. Facultatif : Sélectionnez une alerte et cliquez sur l'icône **Corbeille** pour la supprimer.

## Pannes d'application
{: #monitor-app-crash}

Vous pouvez afficher les informations relatives à vos pannes d'application dans la console {{site.data.keyword.mobileanalytics_short}} afin d'améliorer la surveillance et l'identification et la résolution des problèmes liés à vos applications.

### Surveillance de pannes d'application
{: #app-crash}

Vous pouvez afficher rapidement les informations relatives à vos pannes d'application dans la section **Tableau de bord** de la console {{site.data.keyword.mobileanalytics_short}}.

Sur la page **Présentation** de la section **Tableau de bord**, le diagramme à barres **Pannes** illustre un histogramme des pannes au fil du temps.

Vous pouvez afficher les données de deux façons :

1. Afficher le taux de pannes : taux de pannes au fil du temps
2. Afficher le nombre total de pannes : nombre total de pannes au fil du temps


### Traitement des incidents liés aux pannes d'application
{: #app-crash-troubleshooting}

Vous pouvez afficher la page **Pannes** qui se trouve dans la section **Applications** de la console {{site.data.keyword.mobileanalytics_short}} pour mieux administrer vos applications.

Le tableau **Présentation des pannes** affiche les colonnes de données suivantes :

* Application : Nom d'application
* Pannes : Nombre total de pannes pour cette application
* Nombre total d'utilisations : Nombre total de fois qu'un utilisateur ouvre et ferme cette application
* Taux de pannes : Pourcentage de pannes par utilisation

Le tableau **Récapitulatif des pannes** inclut les colonnes de données suivantes et peut être trié :

* Pannes
* Périphériques
* Dernière panne
* Application
* Système d'exploitation
* Message

Vous pouvez cliquer sur l'icône + située en regard de n'importe quelle entrée pour afficher le tableau **Détails des pannes**, qui inclut les colonnes suivantes :

* Heure de la panne
* Version de l'application
* Version du système d'exploitation
* Modèle de périphérique
* ID du périphérique
* Télécharger : lien permettant de télécharger les journaux qui ont conduit à la panne

Vous pouvez développer n'importe quelle entrée du tableau **Détails des pannes** pour obtenir plus de détails, y compris une trace de pile.

**Remarque** : Le tableau **Récapitulatif des pannes** est renseigné en exécutant une requête sur les journaux client de niveau Fatal. Si votre application ne collecte pas de journaux client de niveau Fatal, aucune donnée n'est disponible.


