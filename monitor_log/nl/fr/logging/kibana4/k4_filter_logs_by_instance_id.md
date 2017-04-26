---

copyright:
  years: 2015, 2017

lastupdated: "2017-03-01"

---


{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}
{:screen: .screen}

# Filtrage de vos journaux par ID d'instance
{:#k4_filter_logs_by_instance_id}

Vous pouvez visualiser et filtrer vos journaux {{site.data.keyword.Bluemix}} par ID d'instance.
{:shortdesc}

Pour visualiser et filtrer vos journaux par ID d'instance dans le tableau de bord Kibana, procédez comme suit :

1. Examinez la page Discover de Kibana pour identifier le sous-ensemble de données qu'elle affiche. Pour plus d'informations, voir  [Identification des données affichées dans votre page Kibana Discover](logging_kibana_analize_logs_interactively.html#k4_identify_data).

2. Dans la liste des zones (*Field List*), sélectionnez l'une des zones suivantes pour rechercher un ID d'instance spécifique :

    * **instance_ID** : Cette zone répertorie les différents ID d'instance disponibles dans le journal pour une application Cloud Foundry. 
    * **instance** : Cette zone répertorie les différents identificateurs globaux uniques (GUID) de toutes les instances d'un groupe de conteneurs. 

    L'illustration ci-dessous, par exemple, présente différentes valeurs d'instances pour une application CF :
    
    ![Liste de filtres présentant la zone instance_id](images/k4_filter_instanceid_f1.jpg "Liste de filtres présentant la zone instance_id")
   
3. Pour ajouter un filtre recherchant un type de journal spécifique, sélectionnez la loupe ![Loupe en mode inclusif](images/k4_include_field_icon.jpg "Loupe en mode inclusif") en regard du type de journal que vous désirez analyser.

   Par exemple, pour ajouter un filtre afin d'inclure les entrées pour l'instance d'application CF *2*, sélectionnez la loupe ![Loupe en mode inclusif](images/k4_include_field_icon.jpg "Loupe en mode inclusif") en regard de la valeur *2* dans la section Fields list (Liste des zones). L'illustration suivante présente le filtre incluant les entrées pour l'instance *2*.
    
    ![Filtre incluant les entrées instance_id pour l'instance 2](images/k4_filter_instanceid_f2.jpg "Filtre incluant les entrées instance_id pour l'instance 2")

    Pour ajouter un filtre afin de rechercher des entrées n'incluant pas un ID d'instance spécifique, sélectionnez la loupe ![Loupe en mode exclusif](images/k4_exclude_field_icon.jpg "Loupe en mode exclusif") en regard de cette valeur.

     Par exemple, pour ajouter un filtre excluant les entrées de l'application CF *2*, sélectionnez la loupe ![Loupe en mode exclusif](images/k4_exclude_field_icon.jpg "Loupe en mode exclusif") en regard de la valeur *2* dans la section Fields list (Liste des zones). L'illustration suivante présente le filtre excluant les entrées pour l'instance *2*.
     
      ![Filtre excluant les entrées instance_id pour l'instance 2](images/k4_filter_instanceid_f3.jpg "Filtre excluant les entrées instance_id pour l'instance 2")

