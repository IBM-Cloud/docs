---

copyright:
  years: 2015, 2017

lastupdated: "2017-03-13"

---


{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}
{:screen: .screen}

# Filtrage des journaux dans Kibana
{:#kibana_filtering_logs}

Sur la page Discover, vous pouvez définir de nouvelles requêtes de recherche et appliquer des filtres pour circonscrire les informations affichées pour analyse.
{:shortdesc}

* Vous pouvez définir une ou plusieurs requêtes de recherche dans la barre de recherche de la page Discover. Une requête de recherche définit un sous-ensemble d'entrées de journal. Utilisez le langage d'interrogation Lucene pour définir une requête de recherche. 

* Vous pouvez ajouter des filtres depuis la section *Fields list* (Liste de zones) ou depuis les entrées de la table. Un filtre affine la sélection de données en incluant ou en excluant des informations. Vous pouvez activer ou désactiver un filtre, inverser l'opération de filtrage, basculer l'état du filtre ou le supprimer complètement. 

Lorsque vous définissez une nouvelle recherche, enregistrez-la pour pouvoir la réutiliser dans une requête future dans la page Discover ou pour créer des visualisations dans des tableaux de bord personnalisés. Pour plus d'informations, voir [Sauvegarde d'une recherche](logging_kibana_filtering_logs.html#k4_save_search).

Lorsque vous lancez une nouvelle recherche, l'histogramme, le tableau et la section Fields list (Liste des zones) sont mis à jour automatiquement en affichant les résultats de la recherche. Pour déterminer quelles données sont affichées, voir [Identification des données affichées sur la page Discover](k4_identify_data.html#k4_identify_data).

La liste suivante décrit des scénarios de filtrage des données de vos journaux :

* Vous pouvez créer des recherches personnalisées pour filtrer vos journaux. Pour plus d'informations, voir [Filtrage des journaux en définissant des requêtes personnalisées](k4_filter_queries.html#k4_filter_queries).

* Vous pouvez rechercher dans vos journaux des entrées contenant un texte spécifique dans la valeur d'une zone. Pour plus d'informations, voir [Filtrage de vos journaux d'après un texte spécifique dans la valeur d'une zone](k4_filter_logs_spec_text.html#k4_filter_logs_spec_text).
 
* Vous pouvez rechercher dans votre journal une valeur de zone spécifique ou exclure les entrées de journal contenant une valeur de zone spécifique. Pour plus d'informations, voir [Filtrage de vos journaux d'après une valeur de zone spécifique](k4_filter_logs_spec_field.html#k4_filter_logs_spec_field).

    * Vous pouvez filtrer vos journaux d'après un type de journal. Pour plus d'informations, voir [Filtrage de vos journaux d'après le type de journal](k4_filter_logs_by_log_type.html#k4_filter_logs_by_log_type).
    * Vous pouvez filtrer vos journaux d'application CF d'après la source. Pour plus d'informations, voir [Filtrage de vos journaux d'application CF d'après la source](k4_filter_logs_by_source.html#k4_filter_logs_by_source).
    * Vous pouvez filtrer vos journaux d'après l'ID d'instance. Pour plus d'informations, voir [Filtrage de vos journaux d'après l'ID d'instance](k4_filter_logs_by_instance_id.html#k4_filter_logs_by_instance_id).   
    * Vous pouvez filtrer vos journaux d'après le type de message. Pour plus d'informations, voir [Filtrage de vos journaux d'après l'ID de type de message](k4_filter_cf_logs_by_msg_type.html#k4_filter_cf_logs_by_msg_type).  
 
* Vous pouvez filtrer vos journaux afin d'afficher les entrées correspondant à une période donnée. Pour plus d'informations, voir [Définition d'un filtre temporel](logging_kibana_set_time_filter.html#set_time_filter).
     

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


## Rechargement d'une recherche
{: #k4_reload_search}

Pour charger une recherche sauvegardée, procédez comme suit :

1. Dans la barre d'outils de la page Discover, cliquez sur le bouton **Load Search** (Charger une recherche) ![Charger une recherche](images/k4_load_icon.jpg "Charger une recherche").

2. Sélectionnez la recherche que vous désirez charger. 


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




