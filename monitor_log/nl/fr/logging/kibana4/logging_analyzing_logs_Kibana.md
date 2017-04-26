---

copyright:
  years: 2015, 2017

lastupdated: "2017-03-13"

---


{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}
{:screen: .screen}

# Analyse de journal avancée avec Kibana
{:#analyzing_logs_Kibana}

Dans {{site.data.keyword.Bluemix}}, vous pouvez utiliser la plateforme de visualisation et d'analyse open source Kibana pour surveiller, rechercher, analyser et visualiser des données dans différents graphiques, par exemple, des diagrammes et des tableaux. Utilisez Kibana pour effectuer des tâches analytiques avancées.
{:shortdesc}

Vous pouvez lancer Kibana en procédant de l'une des manières suivantes :

* Depuis {{site.data.keyword.Bluemix_notm}}

    Vous pouvez lancer vos journaux d'application CF spécifiques dans Kibana, dans le contexte de l'application concernée.
    
    Vous pouvez lancer vos journaux de conteneur Docker spécifiques dans Kibana, dans le contexte du conteneur concerné. 
    
    Pour les applications CF, la requête utilisée pour filtrer les données disponibles pour analyse dans Kibana extrait les entrées de journal de l'application Cloud Foundry. Les informations de journal affichées par défaut par Kibana ne concernent qu'une application Cloud Foundry unique et toutes ses instances. 
    
    Pour les conteneurs, la requête utilisée pour filtrer des données disponibles pour analyse dans Kibana extrait les entrées de journal pour toutes les instances du conteneur. Les informations de journal affichées par défaut par Kibana ne concernent qu'un conteneur unique, ou un groupe de conteneurs, et toutes ses instances. 
    
    Pour plus d'informations, voir [Accès au tableau de bord Kibana depuis le tableau de bord Bluemix](logging_analyzing_logs_Kibana.html#launch_Kibana_from_bluemix).

* A partir d'un lien de navigateur direct

    Vous souhaiterez peut-être lancer Kibana en agrégeant les journaux de services opérant au sein de l'espace {{site.data.keyword.Bluemix_notm}} désigné.
    
    La requête utilisée pour filtrer les données affichées dans le tableau de bord extrait des entrées de journal pour un espace dans l'organisation {{site.data.keyword.Bluemix_notm}}. Les informations de journal affichées par Kibana incluent des enregistrements sur toutes les ressources déployées dans l'espace de l'organisation {{site.data.keyword.Bluemix_notm}} à laquelle vous êtes connecté. 
    
    Pour plus d'informations, voir [Accès au tableau de bord Kibana depuis un navigateur Web](logging_analyzing_logs_Kibana.html#launch_Kibana_from_browser).
    
    Lorsque vous lancez Kibana depuis un navigateur, vous pouvez choisir d'utiliser Kibana 4 ou Kibana 3. **Remarque :** la version Kibana 3 est obsolète. Pour plus d'informations sur l'utilisation de Kibana 3 pour analyser vos journaux, voir [Analyse de journaux dans Kibana 3 (Obsolète)](../logging_view_kibana3.html#analyzing_logs_Kibana3).

<br>    

Kibana est une interface basée navigateur dans laquelle vous pouvez analyser de manière interactive vos données et personnaliser des tableaux de bord que vous pourrez ensuite utiliser pour analyser les données de journal et effectuer des tâches de gestion avancées. 

Les données qu'affiche une page Kibana sont circonscrites pas une recherche. Le jeu de données par défaut est défini par le canevas d'index préconfiguré. Pour filtrer les informations, vous pouvez ajouter de nouvelles requêtes de recherche et appliquer des filtres au jeu de données par défaut. Vous pouvez ensuite sauvegarder la recherche pour une réutilisation future. 

Kibana inclut différentes pages que vous pouvez utiliser pour analyser vos journaux :

| Page Kibana | Description |
|-------------|-------------|
| Discover (Reconnaître) | Utilisez cette page pour définir des recherches et analyser vos journaux de manière interactive via un tableau et un histogramme. |
| Visualize (Visualiser) | Utilisez cette page pour créer des visualisations (par exemple, des graphiques et des tableaux) que vous pourrez utiliser pour analyser vos données de journal et comparer les résultats.  |
| Dashboard (Tableau de bord) | Utilisez cette page pour analyser vos journaux via des collections de visualisations et de recherches sauvegardées.  |

**Remarque :** vous ne pouvez analyser qu'une journée entière à la fois via la page Visualize ou la page Dashboard, même si vous pouvez revenir 7 jours en arrière. Les données de journal sont conservées par défaut pendant 7 jours. 

| Page Kibana | Période de temps |
|-------------|-------------------------|
| Discover (Reconnaître) | Analyse des données sur 7 jours au maximum. |
| Visualize (Visualiser) | Analyse des données sur une période de 24 heures. <br> Vous pouvez filtrer les données de journal sur une période personnalisée couvrant 24 heures.  |
| Dashboard (Tableau de bord) | Analyse des données sur une période de 24 heures. <br> Vous pouvez filtrer les données de journal sur une période personnalisée couvrant 24 heures.<br> Le sélecteur de période que vous définissez s'applique à toutes les visualisations incluses dans le tableau de bord. |


Vous pourriez, par exemple, utiliser Kibana ainsi pour afficher des informations sur une application CF ou un conteneur dans votre espace via les différentes pages :

* Sur la page Discover, vous pouvez définir de nouvelles requêtes de recherche et appliquer des filtres par requête. Les données de journal sont affichées via un tableau et un histogramme. Vous pouvez utiliser ces visualisations pour analyser les données de manière interactive. Pour plus d'informations, voir [Analyses des données en mode interactif dans Kibana](logging_kibana_analize_logs_interactively.html#kibana_analize_logs_interactively).

    Vous pouvez configurer des filtres depuis les zones du journal, par exemple message_type (type de message) et instance_ID (ID d'instance), et définir une période de temps. Vous pouvez activer ou désactiver dynamiquement ces filtres. Le tableau et l'histogramme afficheront les entrées  de journal correspondant à la requête et aux critères de filtrage activés. Pour plus d'informations, voir [Filtrage des journaux dans Kibana](logging_kibana_filtering_logs.html#kibana_filtering_logs).
    
* Sur la page Visualize, vous pouvez définir de nouvelles requêtes de recherche et visualisations.

    Pour analyser les données, vous pouvez créer des visualisations basées sur une recherche existante ou une nouvelle recherche. Kibana inclut différents types de visualisations (comme un tableau, des tendances et un histogramme) que vous pouvez utiliser pour analyser les informations. L'objectif de chaque visualisation varie. Certaines sont organisées en lignes qui affichent les résultats d'une ou de plusieurs requêtes. D'autres affichent des documents ou des informations personnalisées. Les données dans une visualisation peuvent être fixes ou changer si une requête de recherche est modifiée. Vous pouvez incorporer la visualisation dans une page Web ou la partager. Pour plus d'informations, voir [Analyse des journaux à l'aide de visualisations](logging_kibana_visualizations.html#logging_kibana_visualizations).

* Sur la page Dashboard, vous pouvez personnaliser, sauvegarder et partager simultanément plusieurs visualisations et recherches. 

    Vous pouvez ajouter, retirer et réorganiser des visualisations dans le tableau de bord. Pour plus d'informations, voir [Analyse des journaux dans Kibana via un tableau de bord](logging_kibana_analize_logs_dashboard.html#kibana_analize_logs_dashboard).
    
    Après avoir personnalisé un tableau de bord Kibana, vous pouvez analyser les données par le biais de ses visualisations et le sauvegarder pour une réutilisation future. Pour plus d'informations, voir [Sauvegarde d'un tableau de bord Kibana](logging_kibana_analize_logs_dashboard.html#save_Kibana_dashboard).

Kibana comporte également une page *Settings* (Paramètres) que vous pouvez utiliser pour configurer Kibana et pour sauvegarder, supprimer, exporter et importer des recherches, des visualisations et des tableaux de bord.

Pour plus d'informations, reportez-vous au manuel [Kibana User Guide ![Icône de lien externe](../../../icons/launch-glyph.svg "Icône de lien externe")](https://www.elastic.co/guide/en/kibana/4.1/index.html){: new_window}.

**Remarque :** Kibana 3 et Kibana 4 sont pris en charge. Kibana 3 est obsolète.


##  Accès au tableau de bord Kibana depuis le tableau de bord Bluemix
{: #launch_Kibana_from_bluemix}

La requête utilisée pour filtrer les données affichées dans Kibana extrait les entrées de journal pour {{site.data.keyword.Bluemix_notm}} l'application CF ou le conteneur depuis lequel vous lancez Kibana. 

Pour consulter les journaux d'une application Cloud Foundry ou d'un conteneur Docker dans Kibana, procédez comme suit :

1. Connectez-vous à {{site.data.keyword.Bluemix_notm}}, puis cliquez sur le nom de l'application ou du conteneur dans le tableau de bord {{site.data.keyword.Bluemix_notm}}. 
    
2. Ouvrez l'onglet des journaux dans l'interface utilisateur de {{site.data.keyword.Bluemix_notm}}.

    * Pour les applications CF, cliquez sur **Journaux** dans la barre de navigation. 
    * Pour les conteneurs, sélectionnez **Surveillance et journaux** dans la barre de navigation, puis cliquez sur l'onglet **Journalisation**. 
    
    L'onglet Journaux s'affiche. 
    
3. Cliquez sur **Vue avancée**. Le tableau de bord **Kibana 4** s'ouvre.

    Par défaut, la page **Discover** (Reconnaître) est chargée avec le canevas d'index par défaut et un filtre temporel est défini sur les 30 dernières secondes. La requête de recherche est configurée pour porter sur toutes les entrées concernant votre application CF ou votre conteneur Docker.

    Si la page Discover n'affiche aucune entrée de journal, ajustez le sélecteur de période. Pour plus d'informations, voir [Définition d'un filtre temporel](logging_kibana_set_time_filter.html#set_time_filter).

Pour plus d'informations sur Kibana, reportez-vous au manuel [Kibana User Guide](https://www.elastic.co/guide/en/kibana/current/index.html).

##  Accès au tableau de bord Kibana depuis un navigateur Web
{: #launch_Kibana_from_browser}

La requête utilisée pour filtrer les données affichées dans Kibana extrait les entrées de journal pour un espace dans l'organisation {{site.data.keyword.Bluemix_notm}}. Les informations de journal affichées par Kibana incluent des enregistrements pour toutes les ressources déployées dans l'espace de l'organisation {{site.data.keyword.Bluemix_notm}} à laquelle vous êtes connecté.

Pour lancer Kibana depuis un navigateur, procédez comme suit :

1. Ouvrez [https://logmet.<span class="keyword" data-hd-keyref="DomainName">NomDomaine</span>](https://logmet.{DomainName}) pour vous connecter à l'interface utilisateur Kibana.

2. Sélectionnez la version Kibana à utiliser pour analyser vos journaux.
    * Sélectionnez l'onglet **Kibana 4** si vous désirez utiliser cette version. La page Discovery (Reconnaissance) s'ouvre. Pour plus d'informations, voir [logging_kibana_analize_logs_interactively.html#kibana_analize_logs_interactively).
    * Sélectionnez l'onglet **Kibana 3** si vous désirez utiliser cette version. Le tableau de bord Kibana par défaut s'ouvre. Pour plus d'informations sur la personnalisation d'un tableau de bord Kibana 3, voir cet [article de blogue](https://www.ibm.com/blogs/bluemix/2015/09/creating-custom-kibana-dashboard-in-bluemix/).
     
        **Remarque :** la version Kibana 3 est obsolète.

    Si la page Discover n'affiche aucune entrée de journal, ajustez le sélecteur de période. Pour plus d'informations, voir [Définition d'un filtre temporel](logging_kibana_set_time_filter.html#set_time_filter).

Pour plus d'informations sur Kibana, reportez-vous au manuel [Kibana User Guide ![Icône de lien externe](../../../icons/launch-glyph.svg "Icône de lien externe")](https://www.elastic.co/guide/en/kibana/4.1/index.html){: new_window}.

