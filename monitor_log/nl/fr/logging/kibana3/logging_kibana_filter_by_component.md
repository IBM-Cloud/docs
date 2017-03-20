---

copyright:
  years: 2016, 2017
lastupdated: "2017-02-06"

---

<!-- Common attributes used in the template are defined as follows: -->
{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen:.screen}
{:codeblock:.codeblock}

# Filtrage de vos journaux d'application Cloud Foundry par type de journal dans Kibana
<!-- for example, Uploading your data -->
{: #logging_kibana_component_filter}
<!-- Provide an appropriate ID above -->

Affichez et filtrez des journaux d'application {{site.data.keyword.Bluemix_notm}} par composant (type de journal) sur le tableau de bord Kibana. Vous pouvez accéder au tableau de bord Kibana à partir de l'onglet **Journaux** de votre application Cloud Foundry.
{:shortdesc}

<!-- Include a sentence to briefly introduce the steps/subtopics. Example: -->
Procédez comme suit pour afficher et filtrer vos journaux d'application Cloud Foundry par type de journal sur le tableau de bord Kibana :

1. Accédez à l'onglet **Journaux** de votre application Cloud Foundry.  

    1. Cliquez sur le nom d'application dans le tableau de bord **Applications** de {{site.data.keyword.Bluemix_notm}}. 
    2. Cliquez sur l'onglet **Journaux**. 
    
    Les journaux de votre application s'affichent. 

2. Accédez au tableau de bord Kibana de votre application. Cliquez sur **Vue avancée** ![](images/logging_advanced_view.jpg). Le tableau de bord Kibana s'affiche. 

3. Dans la fenêtre **Tous les événements**, cliquez sur l'icône en forme de flèche vers la droite pour afficher toutes les zones.  

    ![Fenêtre Tous les événements avec l'icône en forme de flèche vers la droite](images/logging_all_events_no_fields.jpg)

4. Dans la sous-fenêtre **Zones**, sélectionnez **source_id** pour afficher le composant ayant généré chaque entrée de journal dans la fenêtre **Tous les événements**. 

    ![Fenêtre Tous les événements avec la zone source_id sélectionnée](images/logging_component.png)

5. Dans la fenêtre **Tous les événements**, cliquez sur une ligne d'événement de journal pour afficher les détails relatifs à l'événement. Choisissez un événement qui affiche la valeur source_id que vous souhaitez filtrer. 

    ![Fenêtre Tous les événements affichant les détails relatifs à un événement de journal sélectionné](images/logging_component_add_filter.png)

6. Ajoutez un filtre pour inclure ou exclure des informations concernant un composant (type de journal).  

    * Pour ajouter un filtre incluant une valeur de composant, cliquez sur l'icône en forme de **loupe** ![](images/logging_magnifying_glass.jpg) dans la ligne source_id du tableau.  

        ![Condition de filtre incluant la zone source_id](images/logging_component_filter.png) 

    * Pour ajouter un filtre excluant une valeur de composant, cliquez sur l'icône d'**exclusion** ![](images/logging_exclusion_icon.png) dans la ligne source_id du tableau.  
    
         ![Condition de filtre excluant la zone source_id](images/logging_component_add_exclusion_filter.png) 
     
     Une nouvelle condition de filtre est ajoutée au tableau de bord Kibana. 

7. Vous pouvez éventuellement répéter l'étape précédente et ajouter des filtres pour chaque composant. Pour afficher la liste complète de tous les composants, voir [Format de journal](../logging_view_kibana3.html#kibana_log_format_cf).

    L'image suivante illustre le tableau de bord avec plusieurs filtres pour différents composants :
    
    ![Plusieurs conditions de filtre pour la zone source_id](images/logging_component_multiple_filters.png)

8. Sauvegardez le tableau de bord. 

    Lorsque vous avez terminé d'ajouter des filtres et de personnaliser le tableau de bord, cliquez sur l'icône de **sauvegarde** ![](images/logging_save.jpg) et entrez un nom pour votre tableau de bord.  
      
    **Remarque :** Si vous tentez de sauvegarder un tableau de bord avec un nom contenant des espaces vides, l'opération échoue. Entrez un nom ne contenant pas d'espaces et cliquez sur l'icône de **sauvegarde**. 
    
    ![Sauvegarde d'un nom de tableau de bord](images/logging_save_dashboard.jpg)

Vous avez créé un tableau de bord qui filtre vos entrées de journal par composant (type de journal). Vous pouvez charger votre tableau de bord sauvegardé à tout moment en cliquant sur l'icône **Dossier** ![](images/logging_folder.jpg) et en sélectionnant votre tableau de bord par nom. 


