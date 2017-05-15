---

copyright:
  years: 2015, 2017

lastupdated: "2017-04-06"

---


{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}
{:screen: .screen}

# Analyse de journal avancée avec Kibana
{:#analyzing_logs_Kibana}

Dans {{site.data.keyword.Bluemix}}, vous pouvez utiliser la plateforme de visualisation et d'analyse open source Kibana pour surveiller, rechercher, analyser et visualiser des données dans différents graphiques, par exemple, des diagrammes et des tableaux. Utilisez Kibana pour effectuer des tâches analytiques avancées.
{:shortdesc}

Kibana est une interface basée navigateur dans laquelle vous pouvez analyser de manière interactive vos données et personnaliser des tableaux de bord que vous pourrez ensuite utiliser pour analyser les données de journal et effectuer des tâches de gestion avancées. Pour plus d'informations, voir le document [Kibana User Guide ![Icône de lien externe](../../../icons/launch-glyph.svg "Icône de lien externe")](https://www.elastic.co/guide/en/kibana/4.1/index.html){: new_window}.

Les données qu'affiche une page Kibana sont circonscrites pas une recherche. Le jeu de données par défaut est défini par le canevas d'index préconfiguré. Pour filtrer les informations, vous pouvez ajouter de nouvelles requêtes de recherche et appliquer des filtres au jeu de données par défaut. Vous pouvez ensuite sauvegarder la recherche pour une réutilisation future. 

Kibana inclut différentes pages que vous pouvez utiliser pour analyser vos journaux :

| Page Kibana | Description |
|-------------|-------------|
| Discover (Reconnaître) | Utilisez cette page pour définir des recherches et analyser vos journaux de manière interactive via un tableau et un histogramme. |
| Visualize (Visualiser) | Utilisez cette page pour créer des visualisations (par exemple, des graphiques et des tableaux) que vous pourrez utiliser pour analyser vos données de journal et comparer les résultats.  |
| Dashboard (Tableau de bord) | Utilisez cette page pour analyser vos journaux via des collections de visualisations et de recherches sauvegardées.  |
{: caption="Tableau 1. Pages Kibana" caption-side="top"}

**Remarque :** vous ne pouvez analyser qu'une journée entière à la fois via la page Visualize ou la page Dashboard, même si vous pouvez revenir 7 jours en arrière. Les données de journal sont conservées par défaut pendant 7 jours. 

| Page Kibana | Période de temps |
|-------------|-------------------------|
| Discover (Reconnaître) | Analyse des données sur 7 jours au maximum. |
| Visualize (Visualiser) | Analyse des données sur une période de 24 heures. <br> Vous pouvez filtrer les données de journal sur une période personnalisée couvrant 24 heures.  |
| Dashboard (Tableau de bord) | Analyse des données sur une période de 24 heures. <br> Vous pouvez filtrer les données de journal sur une période personnalisée couvrant 24 heures. <br> Le sélecteur de période que vous définissez s'applique à toutes les visualisations incluses dans le tableau de bord. |
{: caption="Tableau 2. Informations de période" caption-side="top"}

Vous pourriez, par exemple, utiliser Kibana ainsi pour afficher des informations sur une application CF ou un conteneur dans votre espace via les différentes pages :

## Accédez au tableau de bord Kibana
{: #launch_Kibana}

Vous pouvez lancer Kibana en procédant de l'une des manières suivantes :

* Depuis {{site.data.keyword.Bluemix_notm}}

    Vous pouvez lancer vos journaux d'application CF spécifiques dans Kibana, dans le contexte de l'application concernée.
    
    Vous pouvez lancer vos journaux de conteneur Docker spécifiques dans Kibana, dans le contexte du conteneur concerné. 
    
    Pour les applications CF, la requête utilisée pour filtrer les données disponibles pour analyse dans Kibana extrait les entrées de journal de l'application Cloud Foundry. Les informations de journal affichées par défaut par Kibana ne concernent qu'une application Cloud Foundry unique et toutes ses instances. 
    
    Pour les conteneurs, la requête utilisée pour filtrer des données disponibles pour analyse dans Kibana extrait les entrées de journal pour toutes les instances du conteneur. Les informations de journal affichées par défaut par Kibana ne concernent qu'un conteneur unique, ou un groupe de conteneurs, et toutes ses instances. 
    
    Pour plus d'informations, voir [Accès au tableau de bord Kibana depuis le tableau de bord Bluemix](k4_launch.html#launch_Kibana_from_bluemix).

* A partir d'un lien de navigateur direct

    Vous souhaiterez peut-être lancer Kibana en agrégeant les journaux de services opérant au sein de l'espace {{site.data.keyword.Bluemix_notm}} désigné.
    
    La requête utilisée pour filtrer les données affichées dans le tableau de bord extrait des entrées de journal pour un espace dans l'organisation {{site.data.keyword.Bluemix_notm}}. Les informations de journal affichées par Kibana incluent des enregistrements sur toutes les ressources déployées dans l'espace de l'organisation {{site.data.keyword.Bluemix_notm}} à laquelle vous êtes connecté. 
    
    Pour plus d'informations, voir [Accès au tableau de bord Kibana depuis un navigateur Web](k4_launch.html#launch_Kibana_from_browser).
    
    Lorsque vous lancez Kibana depuis un navigateur, vous pouvez choisir d'utiliser Kibana 4 ou Kibana 3. **Remarque :** la version Kibana 3 est obsolète. Pour plus d'informations sur l'utilisation de Kibana 3 pour analyser vos journaux, voir [Analyse de journaux dans Kibana 3 (Obsolète)](../logging_view_kibana3.html#analyzing_logs_Kibana3).


## Analyse des données de manière interactive
{: #analyze_discover}

Sur la page Discover, vous pouvez définir de nouvelles requêtes de recherche et appliquer des filtres par requête. Les données de journal sont affichées via un tableau et un histogramme. Vous pouvez utiliser ces visualisations pour analyser les données de manière interactive. Pour plus d'informations, voir [Analyses des données en mode interactif dans Kibana](logging_kibana_analize_logs_interactively.html#kibana_analize_logs_interactively).

Vous pouvez configurer des filtres depuis les zones du journal, par exemple message_type (type de message) et instance_ID (ID d'instance), et définir une période de temps. Vous pouvez activer ou désactiver dynamiquement ces filtres. Le tableau et l'histogramme afficheront les entrées  de journal correspondant à la requête et aux critères de filtrage activés. Pour plus d'informations, voir [Filtrage des journaux dans Kibana](k4_filter_logs.html#k4_filter_logs).

## Analyse des données via une visualisation
{: #analyze_visualize}
    
Sur la page Visualize, vous pouvez définir de nouvelles requêtes de recherche et visualisations.

Pour analyser les données, vous pouvez créer des visualisations basées sur une recherche existante ou une nouvelle recherche. Kibana inclut différents types de visualisations (comme un tableau, des tendances et un histogramme) que vous pouvez utiliser pour analyser les informations. L'objectif de chaque visualisation varie. Certaines sont organisées en lignes qui affichent les résultats d'une ou de plusieurs requêtes. D'autres affichent des documents ou des informations personnalisées. Les données dans une visualisation peuvent être fixes ou changer si une requête de recherche est modifiée. Vous pouvez incorporer la visualisation dans une page Web ou la partager. Pour plus d'informations, voir [Analyse des journaux à l'aide de visualisations](logging_kibana_visualizations.html#logging_kibana_visualizations).

## Analyse des données dans un tableau de bord
{: #analyze_dashboard}

Sur la page Dashboard, vous pouvez personnaliser, sauvegarder et partager simultanément plusieurs visualisations et recherches. 

Vous pouvez ajouter, retirer et réorganiser des visualisations dans le tableau de bord. Pour plus d'informations, voir [Analyse des journaux dans Kibana via un tableau de bord](logging_kibana_analize_logs_dashboard.html#kibana_analize_logs_dashboard).
    
Après avoir personnalisé un tableau de bord Kibana, vous pouvez analyser les données par le biais de ses visualisations et le sauvegarder pour une réutilisation future. Pour plus d'informations, voir [Sauvegarde d'un tableau de bord Kibana](logging_kibana_analize_logs_dashboard.html#k4_dashboard_save).

Kibana comporte également une page *Settings* (Paramètres) que vous pouvez utiliser pour configurer Kibana et pour sauvegarder, supprimer, exporter et importer des recherches, des visualisations et des tableaux de bord.


