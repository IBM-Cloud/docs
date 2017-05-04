---

copyright:
  years: 2015, 2017

lastupdated: "2017-03-13"

---


{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}
{:screen: .screen}

# Filtrage de vos journaux d'application CF par type de message
{:#k4_filter_cf_logs_by_msg_type}

Vous pouvez visualiser et filtrer les journaux de Cloud Foundry par type de message dans Kibana.
{:shortdesc}


Pour rechercher des entrées incluant un type de message spécifique, procédez comme suit :

1. Examinez la page Discover de Kibana pour identifier le sous-ensemble de données qu'elle affiche. Pour plus d'informations, voir  [Identification des données affichées dans votre page Kibana Discover](logging_kibana_analize_logs_interactively.html#k4_identify_data).

2. Dans la section *Field List* (Liste des zones), sélectionnez la zone **message_type** (type de message).

    L'illustration suivante présente les valeurs identifiées pour la zone *message_type* dans les journaux d'une application CF :
    
    ![Filtrage de liste présentant la zone message_type](images/k4_filter_by_msg_type_f1.jpg "Filtrage de liste présentant la zone message_type")     

3. Pour ajouter un filtre recherchant des entrées incluant un *message_type* spécifique, sélectionnez la loupe ![Loupe en mode inclusif](images/k4_include_field_icon.jpg "Loupe en mode inclusif") en regard de cette valeur.

    Par exemple, pour ajouter un filtre afin d'inclure les entrées de journal avec le type de message *OUT*, sélectionnez la loupe ![Loupe en mode inclusif](images/k4_include_field_icon.jpg "Loupe en mode inclusif") en regard de la valeur *OUT* dans la section *Fields list* (Liste des zones). L'illustration suivante présente le filtre avec la valeur message_type *OUT* activée.
    
    ![Filtre incluant la valeur de zone](images/k4_filter_by_msg_type_f2.jpg "Filtre incluant la valeur de zone")

    Pour ajouter un filtre recherchant des entrées n'incluant pas un élément *message_type* spécifique, sélectionnez la loupe ![Loupe en mode exclusif](images/k4_exclude_field_icon.jpg "Loupe en mode exclusif") en regard de cette valeur.
    
    Par exemple, pour ajouter un filtre afin d'exclure les entrées de journal de l'élément message_type *OUT*, sélectionnez la loupe ![Loupe en mode exclusif](images/k4_exclude_field_icon.jpg "Loupe en mode exclusif") en regard de la valeur *CELL* dans la section *Fields list* (Liste des zones). L'illustration suivante présente le filtre excluant les entrées associées à la valeur message_type *OUT*.

    ![Filtre excluant la valeur de zone](images/k4_filter_by_msg_type_f3.jpg "Filtre excluant la valeur de zone")

