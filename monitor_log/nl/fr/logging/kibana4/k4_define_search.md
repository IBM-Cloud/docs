---

copyright:
  years: 2015, 2017

lastupdated: "2017-03-13"

---


{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}
{:screen: .screen}

# Définition de requêtes de recherche personnalisées
{:#k4_define_search}

Dans la barre de recherche de la page Discover,  vous pouvez définir et enregistrer des requêtes de recherche en utilisant le langage de requête Lucene. Pour chaque recherche, vous pouvez appliquer des filtres pour affiner les entrées disponibles pour analyse.
{:shortdesc}

Pour définir une recherche personnalisée, procédez comme suit :

1. Accédez à l'onglet **Journaux** de votre application ou de votre conteneur Cloud Foundry (CF). 

    1. Cliquez sur le nom de l'application ou du conteneur dans le tableau de bord {{site.data.keyword.Bluemix}}.
    2. Pour les applications CF, cliquez sur l'onglet **Journaux**. Pour les conteneurs, cliquez sur **Surveillance et journaux**, puis sélectionnez l'onglet **Journalisation**.
    
    Les journaux s'affichent.

2. Accédez à Kibana. Cliquez sur **Vue avancée** ![Lien Vue avancée](images/logging_advanced_view.jpg "Lien Vue avancée"). Le tableau de bord Kibana s'affiche.

    Lorsque vous accédez à Kibana, la recherche par défaut est appliquée. Vous pouvez voir les journaux de la liste d'instances de la ressource pour laquelle vous avez lancé Kibana. Vous pouvez filtrer les journaux d'après n'importe quelle ressource {{site.data.keyword.Bluemix_notm}} (ou toutes) dans cet espace.

3. Examinez la page Discover pour déterminer le sous-ensemble de données qu'elle affiche. Pour plus d'informations, voir  [Identification des données affichées dans votre page Kibana Discover](logging_kibana_analize_logs_interactively.html#k4_identify_data). Modifiez ensuite la recherche par défaut pour filtrer les entrées.

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



## Suppression d'une recherche
{: #k4_delete_search}

Pour supprimer une recherche, procédez comme suit dans la page Settings (Paramètre) :

1. Dans la page Settings (Paramètres), sélectionnez l'onglet **Objects** (Objets).

2. Dans l'onglet **Searches** (Recherches), sélectionnez celle que vous désirez supprimer.

3. Cliquez sur **Delete** (Supprimer).


## Exportation d'une recherche
{: #k4_export_search}

Pour exporter une recherche, procédez comme suit dans la page Settings (Paramètre) :

1. Dans la page Settings (Paramètres), sélectionnez l'onglet **Objects** (Objets).

2. Dans l'onglet **Searches** (Recherches), sélectionnez celle que vous désirez exporter.

3. Cliquez sur **Export** (Exporter).

4. Sauvegardez le fichier.

 
## Importation d'une recherche
{: #k4_import_search}

Pour importer une recherche, procédez comme suit dans la page Settings (Paramètre) :

1. Dans la page Settings (Paramètres), sélectionnez l'onglet **Objects** (Objets).

2. Dans l'onglet **Searches** (Recherches), sélectionnez **Import** (Importer).

3. Sélectionnez un fichier et cliquez sur **Open** (Ouvrir).

La recherche est ajouté eà la liste des recherches.

## Actualisation du contenu d'une recherche
{: #k4_refresh_search}

Pour actualiser manuellement le contenu d'une recherche, vous pouvez cliquer sur l'icône de loupe située dans la barre de recherche. 

Pour actualiser automatiquement les données affichées dans la page Discover, vous pouvez configurer un intervalle d'actualisation. La valeur actuelle de cet intervalle est affichée dans la barre de menu de la page Discover. Par défaut, l'actualisation automatique est définie à **OFF** (Désactivée).

Pour définir un intervalle d'actualisation, procédez comme suit :

1. Dans la page Discover, cliquez sur l'option **Time Filter** (Filtre temporel) située dans la barre de menu.

2. Cliquez sur le bouton **Auto Refresh** (Actualisation automatique)![Actualisation automatique](images/k4_auto_refresh_icon.jpg "Actualisation automatique").

3. Sélectionnez dans la liste un intervalle d'actualisation. 

    ![Options d'intervalle d'actualisation](images/k4_change_autorefresh.jpg "Options d'intervalle d'actualisation")


**Remarque **: après avoir activé un intervalle d'actualisation automatique, vous pouvez la mettre en pause en cliquant sur le bouton Pause ![Pause](images/k4_auto_refresh_pause_icon.jpg "Pause").


## Rechargement d'une recherche
{: #k4_reload_search}

Pour charger une recherche sauvegardée, procédez comme suit :

1. Dans la barre d'outils de la page Discover, cliquez sur le bouton **Load Search** (Charger une recherche) ![Charger une recherche](images/k4_load_icon.jpg "Charger une recherche").

2. Sélectionnez la recherche que vous désirez charger. 

## Lancement d'une nouvelle recherche
{: #k4_new_search}

Pour lancer une nouvelle recherche, cliquez sur le bouton **New Search** (Nouvelle recherche) ![Nouvelle recherche](images/k4_new_search_icon.jpg "Nouvelle recherche") dans la barre d'outils de la page Discover.

## Sauvegarde d'une recherche 
{: #k4_save_search}

Lorsque vous sauvegardez une recherche, la chaîne de requête de recherche et le canevas d'index sélectionné actuellement sont enregistrés.

Pour sauvegarder la recherche actuelle dans la page Discovery, procédez comme suit :

1. Dans la barre d'outils de la page Discover, cliquez sur le bouton **Save Search** (Sauvegarder la recherche) ![Sauvegarder la recherche](images/k4_save_search_icon.jpg "Sauvegarder la recherche").

2. Entrez un nom pour la recherche.

3. Cliquez sur Save (Sauvegarder). 
