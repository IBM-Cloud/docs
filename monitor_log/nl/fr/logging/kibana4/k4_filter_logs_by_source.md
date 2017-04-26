---

copyright:
  years: 2015, 2017

lastupdated: "2017-03-01"

---


{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}
{:screen: .screen}

# Filtrage de vos applications CF par source
{:#k4_filter_logs_by_source}

Vous pouvez afficher et afficher vos journaux d'application Cloud Foundry par type de source via le tableau de bord Kibana.
{:shortdesc}

Pour rechercher des entrées de journal se rapportant à une source de journal spécifique, procédez comme suit :

1. Examinez la page Discover de Kibana pour identifier le sous-ensemble de données qu'elle affiche. Pour plus d'informations, voir  [Identification des données affichées dans votre page Kibana Discover](logging_kibana_analize_logs_interactively.html#k4_identify_data).

2. Dans la section *Field List* (Liste des zones), sélectionnez la zone **source_id** (ID source).

    ![Filtre de liste affichant la zone source_id](images/k4_filter_sourceid_F1.jpg "Filtre de liste affichant la zone source_id")     

3. Pour ajouter un filtre recherchant des entrées incluant une valeur source_id spécifique, sélectionnez la loupe ![Bouton Loupe en mode inclusif](images/k4_include_field_icon.jpg "Bouton Loupe en mode inclusif") en regard de cette valeur.

    Pour consulter la liste des sources de journal disponibles pour les applications CF, voir [Sources de journal pour les applications CF](../logging_cf_apps.html#logging_bluemix_cf_apps_log_sources).

    Par exemple, pour ajouter un filtre renvoyant les entrées de journal sur le démarrage, l'arrêt ou les pannes d'une application CF, sélectionnez la loupe ![Loupe en mode inclusif](images/k4_include_field_icon.jpg "Loupe en mode inclusif") en regard de la valeur *CELL* dans la section *Fields list* (Liste des zones). L'illustration suivante présente le filtre avec activation de la valeur source_id *CELL*.
    
    ![Filtre incluant la valeur de la zone](images/k4_filter_sourceid_F2.jpg "Filtre incluant la valeur de la zone")

    Pour ajouter un filtre recherchant des entrées n'incluant pas un élément source_id spécifique, sélectionnez la loupe ![Loupe en mode exclusif](images/k4_exclude_field_icon.jpg "Loupe en mode exclusif") en regard de cette valeur.
    
    Par exemple, pour ajouter un filtre afin d'exclure les entrées concernant le démarrage, l'arrêt ou les pannes d'une application CF, sélectionnez la loupe ![Loupe en mode exclusif](images/k4_exclude_field_icon.jpg "Loupe en mode exclusif") en regard de la valeur *CELL* dans la section *Fields list* (Liste des zones). L'illustration suivante présente le filtre excluant les entrées associées à la valeur source_id *CELL*.

    ![Filtre d'exclusion de valeur de zone'](images/k4_filter_sourceid_F3.jpg "Filtre d'exclusion de valeur de zone")




