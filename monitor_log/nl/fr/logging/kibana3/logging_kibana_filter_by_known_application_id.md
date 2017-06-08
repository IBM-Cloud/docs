---

copyright:
  years: 2016, 2017
lastupdated: "2017-02-06"

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen:.screen}
{:codeblock:.codeblock}


# Filtrage de vos journaux d'application Cloud Foundry par ID d'application dans Kibana
{: #logging_kibana_known_application_id}

Si vous connaissez l'ID d'application de votre application Cloud Foundry, vous pouvez afficher et filtrer rapidement les journaux à l'aide de l'ID d'application (application_id) de votre application sur le tableau de bord Kibana. Vous pouvez accéder au tableau de bord Kibana à partir de l'onglet **Journaux** de votre application Cloud Foundry. 
{:shortdesc}


Procédez comme suit pour afficher et filtrer vos journaux d'application Cloud Foundry par ID d'application connu sur le tableau de bord Kibana :

1. Accédez à l'onglet **Journaux** de votre application Cloud Foundry. 

    1. Cliquez sur le nom d'application dans le tableau de bord **Applications** de {{site.data.keyword.Bluemix_notm}}.
    2. Cliquez sur l'onglet **Journaux**. 
    
    Les journaux de votre application s'affichent.

2. Accédez au tableau de bord Kibana de votre application. Cliquez sur **Vue avancée** ![Lien Vue avancée](images/logging_advanced_view.jpg "Lien Vue avancée"). Le tableau de bord Kibana s'affiche.

3. Sur le tableau de bord Kibana, cliquez sur l'icône de **dossier** ![Icône de dossier](images/logging_folder.jpg "Icône de dossier") pour afficher un menu répertoriant tous les tableaux de bord récents. 

    **Remarque :** Outre les tableaux de bord que vous avez sauvegardés par nom, le menu répertorie les tableaux de bord sans nom selon le format suivant : *ALCH_TENANT_ID_application_id*. 

    ![Liste de tableaux de bord](images/logging_list_of_dashboards.jpg "Liste de tableaux de bord")

4. Sélectionnez le tableau de bord portant un nom qui contient votre ID d'application connu. 

    Le tableau de bord se charge et affiche des informations filtrées pour votre ID d'application.

5. Vous pouvez éventuellement ajouter d'autres zones à votre section de filtre, par exemple, **instance_id**, pour activer ou désactiver le filtrage d'enregistrements par ID d'instance. 
  
    1. Dans la fenêtre **Tous les événements**, cliquez sur une ligne d'événement de journal pour afficher les détails relatifs à l'événement. 
	
        ![Fenêtre Tous les événements affichant les détails relatifs à un événement de journal sélectionné](images/logging_selected_log_event.jpg "Fenêtre Tous les événements affichant les détails relatifs à un événement de journal sélectionné")
	
    2. Choisissez un événement qui affiche la valeur de zone que vous souhaitez filtrer.
	
    3. Ajoutez un filtre.
    
        Pour ajouter un filtre incluant des informations sur cette valeur de zone spécifique, cliquez sur l'icône en forme de **loupe** ![Icône en forme de loupe](images/logging_magnifying_glass.jpg "Icône en forme de loupe") dans la ligne du tableau contenant la zone que vous souhaitez filtrer. 
	
        Pour ajouter un filtre excluant des informations sur cette valeur de zone spécifique, cliquez sur l'icône d'**exclusion** ![Icône d'exclusion](images/logging_exclusion_icon.png "Icône d'exclusion") dans la ligne du tableau contenant la zone que vous souhaitez filtrer.  

        Une nouvelle condition de filtre est ajoutée au tableau de bord Kibana.
	
	    ![Condition de filtre incluant la zone instance_id](images/logging_instance_id_filter.jpg "Condition de filtre incluant la zone instance_id")
	
6. Sauvegardez le tableau de bord sous un nom reconnaissable. 

    Cliquez sur l'icône de **sauvegarde** ![Icône de sauvegarde](images/logging_save.jpg "Icône de sauvegarde") et entrez un nom pour votre tableau de bord. 

    **Remarque :** Si vous tentez de sauvegarder un tableau de bord avec un nom contenant des espaces vides, l'opération échoue. Entrez un nom ne contenant pas d'espaces et cliquez sur l'icône de **sauvegarde**.

    ![Sauvegarde d'un nom de tableau de bord](images/logging_save_dashboard.jpg "Sauvegarde d'un nom de tableau de bord").


Vous avez créé un tableau de bord qui filtre vos entrées de journal par ID d'application et ID d'instance. Vous pouvez charger votre tableau de bord sauvegardé à tout moment en cliquant sur l'icône de **dossier** ![Icône de dossier](images/logging_folder.jpg "Icône de dossier") et en sélectionnant votre tableau de bord par nom.
