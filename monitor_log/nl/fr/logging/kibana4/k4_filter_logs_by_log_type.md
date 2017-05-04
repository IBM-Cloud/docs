---

copyright:
  years: 2015, 2017

lastupdated: "2017-03-01"

---


{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}
{:screen: .screen}

# Filtrage de vos journaux par type de journal
{:#k4_filter_logs_by_log_type}

Vous pouvez visualiser et filtrer les journaux {{site.data.keyword.Bluemix}} par type de journal.
{:shortdesc}

Pour rechercher des entrées incluant un type de journal spécifique, procédez comme suit :

1. Examinez la page Discover de Kibana pour identifier le sous-ensemble de données qu'elle affiche. Pour plus d'informations, voir  [Identification des données affichées dans votre page Kibana Discover](logging_kibana_analize_logs_interactively.html#k4_identify_data).

2. Dans la section *Field List* (Liste des zones), sélectionnez la zone **type**.

    Par exemple, dans la figure suivante, un seul type de journal est disponible : *syslog*
    
    ![Filtre de liste affichant la zone log type (type de journal)](images/k4_filter_log_type_F1.jpg "Filtre de liste affichant la zone log type (type de journal)")
   
3. Pour ajouter un filtre recherchant un type de journal spécifique, sélectionnez la loupe ![Loupe en mode inclusif](images/k4_include_field_icon.jpg "Loupe en mode inclusif") associée au type de journal que vous désirez analyser.

    Par exemple, pour ajouter un filtre afin d'inclure les entrées de journal *syslog*, sélectionnez la loupe ![Loupe en mode inclusif](images/k4_include_field_icon.jpg "Loupe en mode inclusif") en regard de la valeur *syslog* dans la section *Fields list* (Liste des zones). L'illustration suivante présente le filtre incluant les entrées associées au type de journal *syslog*.

    ![Filtre incluant les entrées de type de journal syslog](images/k4_filter_log_type_F2.jpg "Filtre incluant les entrées de type de journal syslog")

    Pour ajouter un filtre recherchant des entrées n'incluant pas un type de journal spécifique, sélectionnez la loupe ![Loupe en mode exclusif](images/k4_exclude_field_icon.jpg "Loupe en mode exclusif") en regard de la valeur concernée.

     Par exemple, pour ajouter un filtre afin d'exclure les entrées de journal *syslog*, sélectionnez la loupe ![Loupe en mode exclusif](images/k4_exclude_field_icon.jpg "Loupe en mode exclusif") en regard de la valeur *syslog* dans la section *Fields list* (Liste des zones). L'illustration suivante présente le filtre excluant les entrées du type de journal *syslog*.
     
     ![Filtre excluant les entrées du type de journal syslog](images/k4_filter_log_type_F3.jpg "Filtre excluant les entrées du type de journal syslog")



