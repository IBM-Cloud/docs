---

copyright:
  years: 2015, 2017

lastupdated: "2017-04-06"

---


{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}
{:screen: .screen}


# Accès au tableau de bord Kibana
{: #k4_launch}

Vous pouvez lancer Kibana depuis l'interface utilisateur {{site.data.keyword.Bluemix}} ou directement depuis un navigateur Web. {:shortdesc}

Lancez Kibana depuis {{site.data.keyword.Bluemix_notm}} pour visualiser et analyser des données en contexte sur la ressource à partir de laquelle vous lancez Kibana. Par exemple, vous pouvez lancer les journaux d'une application CF spécifique dans Kibana, dans le contexte de cette application, ou vous pouvez lancer les journaux d'un conteneur Docker spécifique dans Kibana, dans le contexte de ce conteneur.  
    
Lancez Kibana depuis un lien de navigateur direct si vous souhaitez voir les données de journal agrégées à partir des services d'un espace {{site.data.keyword.Bluemix_notm}} fourni. La requête utilisée pour filtrer les données affichées dans le tableau de bord extrait des entrées de journal pour un espace dans l'organisation {{site.data.keyword.Bluemix_notm}}. Les informations de journal affichées par Kibana incluent des enregistrements pour toutes les ressources déployées dans l'espace de l'organisation {{site.data.keyword.Bluemix_notm}} à laquelle vous êtes connecté. 

Pour plus d'informations sur Kibana, reportez-vous au manuel [Kibana User Guide ![Icône de lien externe](../../../icons/launch-glyph.svg "Icône de lien externe")](https://www.elastic.co/guide/en/kibana/4.1/index.html){: new_window}.
    

##  Accès au tableau de bord Kibana depuis le tableau de bord Bluemix
{: #launch_Kibana_from_bluemix}

La requête utilisée pour filtrer les données affichées dans Kibana extrait les entrées de journal pour {{site.data.keyword.Bluemix_notm}} l'application CF ou le conteneur depuis lequel vous lancez Kibana. 

Pour consulter les journaux d'une application Cloud Foundry ou d'un conteneur Docker dans Kibana, procédez comme suit :

1. Connectez-vous à {{site.data.keyword.Bluemix_notm}}, puis cliquez sur le nom de l'application ou du conteneur dans le tableau de bord {{site.data.keyword.Bluemix_notm}}. 
    
2. Ouvrez l'onglet des journaux dans l'interface utilisateur {{site.data.keyword.Bluemix_notm}}.

    * Pour les applications CF, cliquez sur **Journaux** dans la barre de navigation. 
    * Pour les conteneurs, sélectionnez **Surveillance et journaux** dans la barre de navigation, puis cliquez sur l'onglet **Journalisation**. 
    
    L'onglet Journaux s'affiche. 
    
3. Cliquez sur **Vue avancée**. Le tableau de bord **Kibana 4** s'ouvre.

    Par défaut, la page **Discover** (Reconnaître) est chargée avec le canevas d'index par défaut et un filtre temporel est défini sur les 30 dernières secondes. La requête de recherche est configurée pour porter sur toutes les entrées concernant votre application CF ou votre conteneur Docker.

    Si la page Discover n'affiche aucune entrée de journal, ajustez le sélecteur de période. Pour plus d'informations, voir [Configuration d'un filtre temporel](logging_kibana_set_time_filter.html#set_time_filter).


##  Accès au tableau de bord Kibana depuis un navigateur Web
{: #launch_Kibana_from_browser}

La requête utilisée pour filtrer les données affichées dans Kibana extrait les entrées de journal pour un espace dans l'organisation {{site.data.keyword.Bluemix_notm}}. Les informations de journal affichées par Kibana incluent des enregistrements pour toutes les ressources déployées dans l'espace de l'organisation {{site.data.keyword.Bluemix_notm}} à laquelle vous êtes connecté.

Pour lancer Kibana depuis un navigateur, procédez comme suit :

1. Ouvrez [https://logmet.<span class="keyword" data-hd-keyref="DomainName">NomDomaine</span>](https://logmet.{DomainName}) pour vous connecter à l'interface utilisateur Kibana.

2. Sélectionnez la version Kibana à utiliser pour analyser vos journaux.
    * Sélectionnez l'onglet **Kibana 4** si vous désirez utiliser cette version. La page Discovery (Reconnaissance) s'ouvre. Pour plus d'informations, voir [logging_kibana_analize_logs_interactively.html#kibana_analize_logs_interactively).
    * Sélectionnez l'onglet **Kibana 3** si vous désirez utiliser cette version. Le tableau de bord Kibana par défaut s'ouvre. Pour plus d'informations sur l'utilisation de Kibana 3 pour analyser vos journaux, voir [Analyse de journaux dans Kibana 3 (Obsolète)](../logging_view_kibana3.html#analyzing_logs_Kibana3). Pour plus d'informations sur la personnalisation d'un tableau de bord Kibana 3, voir cet [article de blogue ![Icône de lien externe](../../../icons/launch-glyph.svg "Icône de lien externe")](https://www.ibm.com/blogs/bluemix/2015/09/creating-custom-kibana-dashboard-in-bluemix/).
     
        **Remarque :** la version Kibana 3 est obsolète.

    Si la page Discover n'affiche aucune entrée de journal, ajustez le sélecteur de période. Pour plus d'informations, voir [Configuration d'un filtre temporel](logging_kibana_set_time_filter.html#set_time_filter).


