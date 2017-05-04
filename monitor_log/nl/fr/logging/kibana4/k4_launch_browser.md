---

copyright:
  years: 2015, 2017

lastupdated: "2017-03-11"

---


{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}
{:screen: .screen}

# Accès au tableau de bord Kibana depuis un navigateur Web
{: #launch_Kibana_from_browser}

Lancez Kibana depuis un navigateur si vous avez besoin d'analyser les entrées de journal dans un espace {{site.data.keyword.Bluemix}}.
{:shortdesc}

La requête utilisée pour filtrer les données affichées dans Kibana extrait les entrées de journal pour un espace dans l'organisation {{site.data.keyword.Bluemix_notm}}. Les informations de journal affichées par Kibana incluent des enregistrements pour toutes les ressources déployées dans l'espace de l'organisation {{site.data.keyword.Bluemix_notm}} à laquelle vous êtes connecté.

Pour lancer Kibana depuis un navigateur, procédez comme suit :

1. Ouvrez [https://logmet.<span class="keyword" data-hd-keyref="DomainName">NomDomaine</span>](https://logmet.{DomainName}) pour vous connecter à l'interface utilisateur Kibana.

2. Sélectionnez la version Kibana à utiliser pour analyser vos journaux.
    * Sélectionnez l'onglet **Kibana 4** si vous désirez utiliser cette version. La page Discovery (Reconnaissance) s'ouvre. Pour plus d'informations, voir [logging_kibana_analize_logs_interactively.html#kibana_analize_logs_interactively).
    * Sélectionnez l'onglet **Kibana 3** si vous désirez utiliser cette version. Le tableau de bord Kibana par défaut s'ouvre. Pour plus d'informations sur la personnalisation d'un tableau de bord Kibana 3, voir cet [article de blogue](https://www.ibm.com/blogs/bluemix/2015/09/creating-custom-kibana-dashboard-in-bluemix/).
     
        **Remarque :** la version Kibana 3 est obsolète.

    Si la page Discover n'affiche aucune entrée de journal, ajustez le sélecteur de période. Pour plus d'informations, voir [Définition d'un filtre temporel](logging_kibana_set_time_filter.html#set_time_filter).

Pour plus d'informations sur Kibana, reportez-vous au manuel [Kibana User Guide ![Icône de lien externe](../../../icons/launch-glyph.svg "Icône de lien externe")](https://www.elastic.co/guide/en/kibana/4.1/index.html){: new_window}.
