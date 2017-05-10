---

copyright:
  years: 2016, 2017
lastupdated: "2017-02-06"

---


{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen:.screen}
{:codeblock:.codeblock}


# Filtrage de vos journaux d'application Cloud Foundry par période dans Kibana
{: #logging_kibana_time_filter}


Affichez et filtrez des journaux d'application {{site.data.keyword.Bluemix_notm}} par période sur le tableau de bord Kibana. Vous pouvez accéder au tableau de bord Kibana à partir de l'onglet **Journaux** de votre application Cloud Foundry. 
{:shortdesc}

Procédez comme suit pour afficher et filtrer vos journaux d'application Cloud Foundry par période sur le tableau de bord Kibana :

1. Accédez à l'onglet **Journaux** de votre application Cloud Foundry. 

    1. Cliquez sur le nom d'application dans le tableau de bord **Applications** de {{site.data.keyword.Bluemix_notm}}.
    2. Cliquez sur l'onglet **Journaux**. 
    
    Les journaux de votre application s'affichent.

2. Accédez au tableau de bord Kibana de votre application. Cliquez sur **Vue avancée** ![Lien Vue avancée](images/logging_advanced_view.jpg "Lien Vue avancée"). Le tableau de bord Kibana s'affiche.


3. Sur le tableau de bord Kibana, cliquez sur l'icône de **filtre temporel**![Filtre temporel Kibana](images/logging_kibana_time_filter.jpg "Filtre temporel Kibana"), puis sélectionnez **Personnalisé** dans le menu déroulant. La fenêtre suivante s'affiche :

    ![Filtre temporel personnalisé sur le tableau de bord Kibana](images/logging_custom_time_filter.jpg "Filtre temporel personnalisé sur le tableau de bord Kibana")

4. Cliquez sur les zones **De** et **A** pour éditer l'heure de début et l'heure de fin de votre filtre. 
    
    Pour inclure des journaux au moment présent, cliquez sur le lien **maintenant**. 
    Lorsque vous êtes satisfait de votre intervalle, cliquez sur **Appliquer**. 

Le tableau de bord Kibana affiche désormais des événements journalisés pour votre filtre temporel personnalisé.
