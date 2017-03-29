---

copyright:
  years: 2016, 2017
lastupdated: "2017-02-02"

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen:.screen}
{:codeblock:.codeblock}


# Filtrage de vos journaux d'application Cloud Foundry à l'aide de requêtes dans Kibana
{: #logging_kibana_query}

Utilisez Kibana pour créer des requêtes afin de rechercher des termes clés dans vos journaux et effectuer un filtrage à l'aide de ces termes. Kibana vous permet de comparer visuellement des requêtes sur le tableau de bord. Vous pouvez accéder au tableau de bord Kibana à partir de l'onglet **Journaux** de votre application Cloud Foundry. 
{:shortdesc}

Procédez comme suit pour créer une requête relative à vos journaux d'application Cloud Foundry sur le tableau de bord Kibana :

1. Accédez à l'onglet **Journaux** de votre application Cloud Foundry. 

    1. Cliquez sur le nom d'application dans le tableau de bord **Applications** de {{site.data.keyword.Bluemix_notm}}.
    2. Cliquez sur l'onglet **Journaux**. 
    
    Les journaux de votre application s'affichent.

2. Accédez au tableau de bord Kibana de votre application. Cliquez sur **Vue avancée** ![](images/logging_advanced_view.jpg). Le tableau de bord Kibana s'affiche.

3. Sur le tableau de bord Kibana, cliquez sur l'icône de **requête** ![](images/logging_query.jpg) pour afficher la zone. Lorsque vous accédez à Kibana pour afficher vos journaux d'application à partir de l'onglet **Journaux** pour votre application, une requête est créée afin d'afficher tous les journaux pour l'ID d'application de votre application.
	
    Pour éditer votre requête, cliquez dans la zone **Requête** et entrez un terme de recherche.

    * Pour rechercher un mot clé ou une partie d'un mot clé, entrez un mot, suivi d'un symbole de caractère générique \* ; par exemple, `Java*`. 
	* Pour rechercher une expression en particulier, entrez cette expression en prenant soin de la placer entre guillemets ; par exemple, `"Java/1.8.0"`.
	* Pour créer des recherches plus complexes, vous pouvez utiliser les termes logiques AND et OR ; par exemple, `"Java/1.8.0" OR "Java/1.7.0"`.
	* Pour rechercher une valeur dans une zone en particulier, entrez votre recherche en respectant le format suivant : *log_field_name:search_term* ; par exemple, `instance_id:1`.
	* Pour rechercher une plage de valeurs pour une zone de journal en particulier, entrez votre recherche en respectant le format suivant : *log_field_name:[start_of_range TO end_of_range]* ; par exemple, `instance_id:[1 TO 2]`.

4. Si vous souhaitez comparer les résultats de deux requêtes distinctes, vous pouvez ajouter un autre terme de requête à votre tableau de bord. Pour ajouter une autre requête, cliquez sur l'icône **+** située à la fin de la zone **Requête**.

    ![Zone de requête](images/logging_query_field.jpg)
	
    Une nouvelle zone **Requête** contenant le caractère générique \* s'affiche. Cette requête indique à Kibana d'inclure toutes les entrées.
	
    ![Zone de requête supplémentaire](images/logging_additional_query_field.jpg)
	
    Votre tableau de bord est mis à jour avec les résultats de votre nouvelle requête. La sous-fenêtre **Evénements par période** affiche une représentation graphique des deux requêtes, ainsi que le nombre de termes pour chacune d'elles entre parenthèses. 
	
    ![Graphique représentant les deux requêtes affiché dans le tableau de bord](images/logging_dashboard_queries.jpg)
	
5. Cliquez dans la nouvelle zone **Requête** pour éditer son contenu et ajouter une condition de requête ; par exemple, `instance_id:1`. Utilisez la sous-fenêtre **Evénements par période** pour comparer les résultats de vos requêtes.

    ![Graphique représentant les deux requêtes affiché dans le tableau de bord](images/logging_dashboard_queries2.jpg)

6. Pour supprimer une requête, faites passer votre souris au-dessus de la zone **Requête** à supprimer pour faire apparaître l'icône de **suppression**. Cliquez sur l'icône de **suppression**.

    ![Zone de requête avec l'icône de suppression](images/logging_delete_query.jpg)

7. Pour sauvegarder ce tableau de bord sous un nom significatif, cliquez sur l'icône de **sauvegarde** ![](images/logging_save.jpg) et entrez un nom pour votre tableau de bord. 

    **Remarque :** Si vous tentez de sauvegarder un tableau de bord avec un nom contenant des espaces vides, l'opération échoue. Entrez un nom ne contenant pas d'espaces et cliquez sur l'icône de **sauvegarde**.

    ![Sauvegarde d'un nom de tableau de bord](images/logging_save_dashboard.jpg)


