---

copyright:
  years: 2016, 2017
lastupdated: "2017-02-07"

---

<!-- Common attributes used in the template are defined as follows: -->
{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen:.screen}
{:codeblock:.codeblock}

<!-- Additional task topic: OPTIONAL
This is the template for additional task topics that are needed beyond the basic tasks in the getting started index.md.  As needed, other task topics can be included, with titles such as "Configuring x", "Administering y", "Managing z", etc. This topic is a peer of the getting started index.md in the <servicename>.ditamap. This topic can have one level of children and they also can be referenced in <servicename>.ditamap -->

# Création de tableaux et de graphiques à partir de requêtes dans Kibana
<!-- for example, Uploading your data -->
{: #logging_kibana_tables_graphs}
<!-- Provide an appropriate ID above -->

<!-- The short description section should include a sentence describing why this task is needed. For search engine optimization, include the service long name and "Bluemix". For example: -->

Utilisez Kibana pour créer des graphiques et des tableaux relatifs à vos requêtes afin de visualiser vos données de journal et comparer des résultats. Vous pouvez accéder au tableau de bord Kibana à partir de l'onglet **Journaux** de votre application Cloud Foundry.
{:shortdesc}

<!-- Include a sentence to briefly introduce the steps/subtopics. Example: -->
Le tableau de bord Kibana se présente sous la forme d'une série de lignes, chacune d'elles contenant un ou plusieurs panneaux. Vous pouvez configurer des panneaux de manière à afficher des représentations graphiques de vos données. Utilisez des requêtes pour déterminer les données à afficher. Pour créer un graphique ou un tableau, vous devez d'abord créer une ligne vide, puis créer un panneau. Si vous accédez au tableau de bord Kibana à partir de l'onglet **Tableaux de bord** de votre application CF, le tableau de bord affiche automatiquement deux panneaux : un histogramme et un tableau. 

Procédez comme suit pour ajouter un graphique ou un tableau sur le tableau de bord Kibana :

1. Pour accéder à l'onglet **Journaux** de votre application Cloud Foundry, cliquez sur le nom d'application dans le tableau **Applications Cloud Foundry** du tableau de bord **Applications** de {{site.data.keyword.Bluemix_notm}}, puis cliquez sur l'onglet **Journaux**. Les journaux de votre application s'affichent. 

2. Pour accéder au tableau de bord Kibana pour votre application, cliquez sur **Vue avancée** ![](images/logging_advanced_view.jpg). Le tableau de bord Kibana s'affiche. 

3. Sur le tableau de bord Kibana, faites défiler l'écran vers le bas, puis cliquez sur l'icône d'**ajout d'une ligne** ![](images/logging_add_row.jpg) afin de créer une ligne pour le panneau que vous souhaitez ajouter. La sous-fenêtre Paramètres du tableau de bord s'affiche.  
	
	![Sous-fenêtre Paramètres du tableau de bord](images/logging_dashboard_settings.jpg)
	
	Dans la sous-fenêtre Ajouter une ligne, entrez un nom pour votre ligne dans la zone **Titre**, puis cliquez sur **Créer une ligne**. Une nouvelle ligne est ajoutée. Vous pouvez ajuster l'ordre des lignes en cliquant sur les icônes représentant une **flèche vers le haut** ou une **flèche vers le bas** en regard des titres de ligne. Lorsque vous avez défini l'ordre des lignes, cliquez sur **Sauvegarder**. Une ligne vide est créée sur le tableau de bord Kibana. 

4. Ajoutez un panneau en cliquant sur **Ajouter un panneau à une ligne vide**. La sous-fenêtre Paramètres de ligne s'affiche. 

    ![Sous-fenêtre Paramètres de ligne](images/logging_row_settings.jpg)
	
	Vous pouvez choisir d'autres types de panneau, tels que **Tableau**, **Histogramme** ou **Dispositions** dans la liste déroulante **Sélectionner un type de panneau**. Sélectionnez **Dispositions** pour créer un graphique à barres, un graphique circulaire ou un tableau en fonction de vos requêtes. Une plage d'options de configuration s'affiche dans la sous-fenêtre Paramètres de ligne. 
	
	![Ajout d'un panneau dans la sous-fenêtre Paramètres de ligne](images/logging_add_panel.jpg)
	
	Configurez votre panneau. Entrez un **titre** pour votre représentation graphique. Sélectionnez l'**étendue** de votre panneau dans la liste déroulante ; l'**étendue** détermine la largeur de votre panneau dans le tableau de bord. Dans la section Paramètres, supprimez le contenu de **Zone** et entrez une zone de journal valide ; par exemple, `instance_id`. 

5. Dans la section Options d'affichage, sélectionnez **Barres**, **Circulaire** ou **Tableau** dans la liste déroulante **Style** pour choisir un graphique à barres, un graphique circulaire ou un tableau. Dans la section Requêtes, choisissez **Sélectionné** dans la liste déroulante **Requêtes** pour utiliser les données de journal de vos requêtes de tableau de bord. Pour terminer, cliquez sur **Sauvegarder**. Votre nouveau panneau s'affiche sur le tableau de bord.

	![Panneau contenant un graphique à barres affiché dans le tableau de bord](images/logging_bar_chart_panel.jpg)
	
6. Pour modifier ce panneau de sorte qu'il affiche un tableau, cliquez sur l'icône de **configuration** ![](images/logging_dashboard_config_panel.jpg). La sous-fenêtre Paramètres de dispositions s'affiche.  

	![Sous-fenêtre Paramètres de dispositions](images/logging_terms_settings.jpg)
	
	Cliquez sur l'onglet **Panneau**, puis sélectionnez **Tableau** dans la liste déroulante **Style**. Cliquez sur **Sauvegarder** pour mettre à jour le panneau et revenir au tableau de bord. 

7. Ajoutez d'autres lignes et panneaux à votre tableau de bord. Lorsque vous avez terminé, sauvegardez les modifications apportées à ce tableau de bord en cliquant sur l'icône de **sauvegarde**. 

    **Remarque :** Si vous tentez de sauvegarder un tableau de bord avec un nom contenant des espaces vides, l'opération échoue. Entrez un nom ne contenant pas d'espaces et cliquez sur l'icône de **sauvegarde**. 

    ![Sauvegarde d'un nom du tableau de bord](images/logging_save_dashboard.jpg).


