---

copyright:
  years: 2015, 2017

lastupdated: "2017-03-11"

---


{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}
{:screen: .screen}

# Accès au tableau de bord Kibana depuis le tableau de bord Bluemix
{: #launch_Kibana_from_bluemix}

Pour visualiser les journaux spécifiques d'une application Cloud Foundry ou d'un conteneur Docker, lancez Kibana depuis l'interface utilisateur de {{site.data.keyword.Bluemix}}.
{:shortdesc}

La requête utilisée pour filtrer les données affichées dans Kibana extrait les entrées de journal pour {{site.data.keyword.Bluemix_notm}} l'application CF ou le conteneur depuis lequel vous lancez Kibana. 

Pour consulter les journaux d'une application Cloud Foundry ou d'un conteneur Docker dans Kibana, procédez comme suit :

1. Connectez-vous à {{site.data.keyword.Bluemix_notm}}, puis cliquez sur le nom de l'application ou du conteneur dans le tableau de bord {{site.data.keyword.Bluemix_notm}}. 
    
2. Ouvrez l'onglet Journal dans l'interface utilisateur de {{site.data.keyword.Bluemix_notm}}.

    * Pour les applications CF, cliquez sur **Journaux** dans la barre de navigation. 
    * Pour les conteneurs, sélectionnez **Surveillance et journaux** dans la barre de navigation, puis cliquez sur l'onglet **Journalisation**. 
    
    L'onglet Journaux s'affiche. 
    
3. Cliquez sur **Vue avancée**. Le tableau de bord **Kibana 4** s'ouvre.

    Par défaut, la page **Discover** (Reconnaître) est chargée avec le canevas d'index par défaut et un filtre temporel est défini sur les 30 dernières secondes. La requête de recherche est configurée pour porter sur toutes les entrées concernant votre application CF ou votre conteneur Docker.

    Si la page Discover n'affiche aucune entrée de journal, ajustez le sélecteur de période. Pour plus d'informations, voir [Définition d'un filtre temporel](logging_kibana_set_time_filter.html#set_time_filter).

Pour plus d'informations sur Kibana, reportez-vous au manuel [Kibana User Guide ![Icône de lien externe](../../../icons/launch-glyph.svg "Icône de lien externe")](https://www.elastic.co/guide/en/kibana/4.1/index.html){: new_window}.

