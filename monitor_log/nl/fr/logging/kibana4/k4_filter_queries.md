---

copyright:
  years: 2015, 2017

lastupdated: "2017-03-13"

---


{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}
{:screen: .screen}

# Filtrage de journaux en définissant des requêtes de recherche personnalisées
{:#k4_filter_queries}

Dans la barre de recherche de la page Discover,  vous pouvez définir et enregistrer des requêtes de recherche en utilisant le langage de requête Lucene. Pour chaque recherche, vous pouvez appliquer des filtres pour affiner les entrées disponibles pour analyse.{:shortdesc}

Pour filtrer vos journaux à l'aide d'une recherche personnalisée, procédez comme suit :

1. Accédez à l'onglet **Journaux** de votre application ou de votre conteneur Cloud Foundry (CF). 

    1. Cliquez sur le nom de l'application ou du conteneur dans le tableau de bord {{site.data.keyword.Bluemix}}.
    2. Pour les applications CF, cliquez sur l'onglet **Journaux**. Pour les conteneurs, cliquez sur **Surveillance et journaux**, puis sélectionnez l'onglet **Journalisation**.
    
    Les journaux s'affichent.

2. Accédez à Kibana. Cliquez sur **Vue avancée** ![](images/logging_advanced_view.jpg). Le tableau de bord Kibana s'affiche.

    Lorsque vous accédez à Kibana, la recherche par défaut est appliquée. Vous pouvez voir les journaux de la liste d'instances de la ressource pour laquelle vous avez lancé Kibana. Vous pouvez filtrer les journaux d'après n'importe quelle ressource {{site.data.keyword.Bluemix_notm}} (ou toutes) dans cet espace.

A la place de "mot clé", l'appellation correcte est "terme" pour Lucene.

3. Examinez la page Discover pour déterminer le sous-ensemble de données qu'elle affiche. Pour plus d'informations, voir  [Identification des données affichées dans votre page Kibana Discover](logging_kibana_analize_logs_interactively.html#k4_identify_data).Modifiez ensuite la recherche par défaut pour filtrer les entrées.

    **Remarque :** utilisez le langage Lucene pour définir votre requête par défaut. Pour plus d'informations, voir [Apache Lucene - Query Parser Syntax  ![Icône de lien externe](../../../icons/launch-glyph.svg "Icône de lien externe")](https://lucene.apache.org/core/2_9_4/queryparsersyntax.html){: new_window}
    
    Lorsque Kibana est lancé depuis {{site.data.keyword.Bluemix_notm}}, pour modifier la requête et définir plusieurs critères de recherche, vous pouvez utiliser les opérateurs logiques **AND** et **OR**. Ces opérateurs doivent être en majuscules.    
    
    * Pour rechercher un mot clé ou une partie d'un mot clé, entrez un mot, suivi d'un symbole de caractère générique \* ; par exemple, `Java*`. 
    * Pour rechercher une expression en particulier, entrez cette expression en prenant soin de la placer entre guillemets ; par exemple, `"Java/1.8.0"`.
    * Pour créer des recherches plus complexes, vous pouvez utiliser les termes logiques AND et OR ; par exemple, `"Java/1.8.0" OR "Java/1.7.0"`.
    * Pour rechercher une valeur dans une zone spécifique, entrez votre recherche sous le format suivant : *nom_zone_journal:terme_recherche* ; par exemple, `instance_id:"1"`.
    * Pour rechercher une plage de valeurs dans une zone de journal spécifique, entrez votre recherche sous le format suivant : *nom_zone_journal:[début_plage TO fin_plage]* ; par exemple, `instance_id:["1" TO "2"]`.

     Par exemple, pour une application CF, vous pourriez créer une requête `application_id:9d222152-8834-4bab-8685-3036cd25931a AND instance_id:["0" TO "1"]` qui ne répertorie que des entrées pour les instances *0* et *1*. 

4. Enregistrez la requête pour pouvoir la réutiliser ultérieurement. Pour plus d'informations, voir [Sauvegarde d'une recherche](logging_kibana_filtering_logs.html#k4_save_search). 

**Remarque :** si vous devez supprimer une requête, voir [Suppression d'une recherche](logging_kibana_filtering_logs.html#k4_delete_search).



