---

copyright:
  years: 2015, 2017

lastupdated: "2017-03-01"

---


{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}
{:screen: .screen}

# Ajout d'un filtre pour une valeur non répertoriée dans la section *Fields list* (Liste des zones)
{:#k4_add_filter_out_value}

Pour ajouter un filtre pour une valeur ne figurant pas dans la section *Field list* (Liste des zones), recherchez par le biais d'une requête les enregistrements contenant cette valeur. Ajoutez ensuite le filtre depuis l'entrée de table figurant dans la page Discover.
{:shortdesc}

Pour ajouter un filtre pour une valeur ne figurant pas dans la section *Fields list* (Liste des zones), procédez comme suit :

1. Examinez la page Discover de Kibana pour identifier le sous-ensemble de données qu'elle affiche. Pour plus d'informations, voir  [Identification des données affichées dans votre page Kibana Discover](logging_kibana_analize_logs_interactively.html#k4_identify_data).

    L'illustration ci-dessous, par exemple, présente les valeurs des instances pour une application CF dans la section *Fields list* (Liste des zones). 
    
    ![Affichage des valeurs dans la liste des zones](images/k4_add_filter_f1.jpg "Affichage des valeurs dans la liste des zones")
    
    Supposons que vous êtes intéressé par l'instance numéro *3*, mais qu'elle ne figure pas dans la liste.

2. Dans la page Discover, modifiez la requête afin de rechercher une valeur de zone spécifique.

    Par exemple, pour rechercher l'instance *3*, la requête à saisir serait la suivante :
   `application_id:9d222152-8834-4bab-8685-3036cd25931a AND instance_id:"3"`
    
    ![Modification de la requête](images/k4_add_filter_f2.jpg "Modification de la requête")
    
    Dans le tableau, vous pouvez voir les enregistrements éventuels correspondant à votre requête. 
    
 3. Développez un enregistrement et sélectionnez la loupe ![Loupe en mode inclusif](images/k4_include_field_icon.jpg "Loupe en mode inclusif") afin d'ajouter un filtre.
 
     Par exemple, pour ajouter un filtre pour l'ID d'instance avec la valeur *3*, cliquez sur la loupe ![Loupe en mode inclusif](images/k4_include_field_icon.jpg "Loupe en mode inclusif") en regard de la zone *instance_id* (ID d'instance).
     
     ![Affichage du tableau](images/k4_add_filter_f3.jpg "Affichage du tableau")
     
4. Vérifiez que le filtre a été ajouté.

    L'illustration suivante, par exemple, indique que le filtre a été activé après son ajout depuis le tableau.
    
    ![Affichage du filtre](images/k4_add_filter_f4.jpg "Affichage du filtre")
    
    
