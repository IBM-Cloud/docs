---

copyright:
  years: 2015, 2017

lastupdated: "2017-03-16"

---


{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}
{:screen: .screen}


# Journalisation pour IBM Bluemix Container Service
{: #logging_containers_ov}

Dans {{site.data.keyword.Bluemix}}, vous pouvez visualiser, filtrer et analyser des journaux de conteneurs via le tableau de bord {{site.data.keyword.Bluemix_notm}}, Kibana, et l'interface de ligne de commande.
{:shortdesc}

Les journaux de conteneurs sont surveillés et retransmis depuis l'extérieur du conteneur par le biais de moteurs de balayage. Les données sont envoyés par les moteurs de balayage à un service partagé Elasticsearch dans {{site.data.keyword.Bluemix_notm}}.

**Remarque :** Vous pouvez analyser des journaux de conteneur dans {{site.data.keyword.Bluemix_notm}} pour les conteneurs Docker qui sont déployés dans l'infrastructure de cloud gérée par {{site.data.keyword.IBM}}.

Le diagramme suivant offre une vue d'ensemble de la journalisation pour {{site.data.keyword.containershort}}:

![Vue d'ensemble des composants pour les conteneurs](images/logging_containers_ov.jpg "Vue d'ensemble des composants pour les conteneurs")

La journalisation des conteneurs est automatiquement activée lorsque vous déployez ce conteneur dans {{site.data.keyword.Bluemix_notm}}.


## Méthodes pour l'analyse des journaux de conteneurs
{: #logging_containers_ov_methods}
 
Vous pouvez choisir l'une des méthodes suivantes pour analyser les journaux de votre conteneur :

* Analyser le journal dans {{site.data.keyword.Bluemix_notm}} pour visualiser l'activité la plus récente du conteneur.
    
    Vous pouvez visualiser, filtrer et analyser des journaux via l'onglet **Surveillance et journaux** présent pour chaque conteneur. Pour plus d'informations, voir [Analyse des journaux depuis le tableau de bord Bluemix](../logging_view_dashboard.html#analyzing_logs_bmx_ui).
    
* Analyser les journaux dans Kibana pour effectuer des tâches analytiques avancées.
    
    Vous pouvez utiliser la plateforme de visualisation et d'analyse open source Kibana pour surveiller, rechercher, analyser et visualiser des données dans différents graphiques, par exemple, dans des diagrammes et des tableaux. Pour plus d'informations, voir [Analyse des journaux dans Kibana](../kibana4/logging_analyzing_logs_Kibana.html#analyzing_logs_Kibana).

* Analyser des journaux via l'interface de ligne de commande pour utiliser des commandes permettant de gérer des journaux à l'aide d'un programme.
    
    Vous pouvez visualiser, filtrer et analyser des journaux via l'interface de ligne de commande en utilisant la commande **cf ic logs**. Pour plus d'informations, voir [Analyse de journaux depuis l'interface de ligne de commande](../logging_view_cli.html#analyzing_logs_cli).

## Journaux collectés pour les conteneurs
{: #logging_containers_ov_logs_collected}

Par défaut, les journaux suivants sont collectés :

<table>
  <caption>Tableau 1. Journaux</caption>
  <tbody>
    <tr>
      <th align="center">Journal</th>
      <th align="center">Description</th>
    </tr>
    <tr>
      <td align="left" width="30%">/var/log/messages</td>
      <td align="left" width="70%"> Par défaut, les messages Docker sont consignés dans le dossier /var/log/messages du conteneur. Ce journal inclut les messages système.
      </td>
    </tr>
    <tr>
      <td align="left">./docker.log</td>
      <td align="left">Il s'agit du journal Docker. <br> Le fichier journal Docker n'est pas stocké sous la forme d'un fichier dans le conteneur mais il est quand même collecté. Ce fichier journal est collecté par défaut vu qu'il s'agit de la convention Docker standard pour exposition des informations du fichier stdout (sortie standard) et du fichier stderr (erreur standard) pour le conteneur. Si un processus de conteneur consigne des informations dans le fichier stdout ou stderr, ces informations sont collectées. 
      </td>
     </tr>
  </tbody>
</table>

Pour collecter des informations de journaux supplémentaires, ajoutez la variable d'environnement **LOG_LOCATIONS** en spécifiant le chemin d'accès du fichier journal concerné lorsque vous créez le conteneur. Vous pouvez ajouter plusieurs fichiers journaux en les séparant par des virgules. Pour plus d'informations, voir [Collecte de données de journaux autres que ceux par défaut d'un conteneur](logging_containers_other_logs.html#logging_containers_collect_data).



## Conservation des journaux
{: #logging_containers_ov_log_retention}

Prenez en compte les informations suivantes sur la conservation des journaux :

* Un maximum de 1 Go par espace de données est stocké chaque jour. Les journaux dépassant ce plafond sont supprimés. Les allocations de plafond sont réinitialisées chaque jour à 00h30 (temps universel coordonné). 

    Vous pouvez rehausser votre plafond en contactant le support. Dans le ticket de demande de service, incluez votre ID d'espace pour la demande d'augmentation du plafond, le nouveau plafond demandé et la raison de la demande.

* Jusqu'à 7 Go de données sont disponibles pour recherches pendant 7 jours maximum. Les données de journal sont écrasées (sur la base Premier entré, premier sorti) une fois que la limite de 7 Go de données est atteinte ou au bout de 7 jours.

