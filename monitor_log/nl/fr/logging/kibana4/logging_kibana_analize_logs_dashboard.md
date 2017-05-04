---

copyright:
  years: 2015, 2017

lastupdated: "2017-03-08"

---


{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}
{:screen: .screen}

# Analyses des journaux dans Kibana via un tableau de bord
{:#kibana_analize_logs_dashboard}

Utilisez la page *Dashboard* dans Kibana pour afficher des collections de visualisations regroupées en tableaux de bord. Utilisez les tableaux de bord pour analyser les données des journaux et comparer les résultats.
{:shortdesc}

Dans {{site.data.keyword.Bluemix}}, vous pouvez définit et personnaliser différents types de tableaux de bord pour visualiser et analyser les données. Le tableau suivant, par exemple, recense divers tableaux de bord courants :

| Type de tableau de bord | Description |
|-------------------|-------------|
| Tableau de bord d'application cf unique | Ce tableau de bord affiche des informations sur une application Cloud Foundry unique. |
| Tableau de bord de conteneur unique  | Ce tableau de bord affiche des informations sur un conteneur unique.  |
| Tableau de bord de groupe de conteneurs  | Ce tableau de bord affiche des informations sur un groupe de conteneurs spécifique.  |
| Tableau de bord multi-applications cf | Ce tableau de bord affiche des informations sur toutes les applications Cloud Foundry déployées dans le même espace {{site.data.keyword.Bluemix_notm}}.  | 
| Tableau de bord multi-conteneurs | Ce tableau de bord affiche des informations sur tous les conteneurs déployés dans le même espace {{site.data.keyword.Bluemix_notm}}.  |
| Tableau de bord d'espace | Ce tableau de bord affiche les données de consignation au journal disponibles dans un espace {{site.data.keyword.Bluemix_notm}}.  | 

Pour visualiser les données dans un tableau de bord, vous devez configurer des panneaux. Kibana inclut différentes visualisations (telles que tableau, tendances et histogramme) que vous pouvez utiliser pour analyser les informations. Une visualisation est ajoutée à un tableau de bord sous forme de panneau. Vous pouvez ajouter, retirer et réorganiser des panneaux dans le tableau de bord. L'objectif de chaque panneau est différent. Certains panneaux sont organisés en lignes qui fournissent les résultats d'une ou de plusieurs requêtes. D'autres panneaux affichent des documents ou des informations personnalisées. Chaque panneau est basé sur une recherche. Le recherche définit le sous-ensemble de données qu'affiche le panneau. Par exemple, vous pouvez configurer un graphique à barres, un graphique circulaire ou un tableau pour visualiser les données et les analyser.  

Le tableau suivant répertorie différentes tâches que vous pouvez effectuer depuis la page Dashboard (Tableau de bord) :

| Tâche | Informations sur la tâche |
|------|------------------|
| [Create a new dashboard](logging_kibana_analize_logs_dashboard.html#K4_dashboard_new) (Créer un nouveau tableau de bord) | Vous pouvez créer plusieurs tableaux de bord. Chaque tableau de bord peut être conçu en vue d'inclure des recherches et des visualisations différentes, ainsi qu'un sous-ensemble distinct de données de journal.  |
| [Save a dashboard](logging_kibana_analize_logs_dashboard.html#k4_dashboard_save) (Sauvegarder un tableau de bord) | Vous pouvez sauvegarder un tableau de bord pour le réutiliser plus tard. |
| [Load a dashboard](logging_kibana_analize_logs_dashboard.html#k4_dashboard_reload) (Charger un tableau de bord) | Vous pouvez charger un tableau de bord pour mettre à jour les données, les modifier, ou les analyser. |
| [Delete a dashboard](logging_kibana_analize_logs_dashboard.html#k4_dashboard_delete) (Supprimer un tableau de bord) | Vous pouvez supprimer les tableaux de bord superflus. |
| [Export a dashboard](logging_kibana_analize_logs_dashboard.html#k4_dashboard_export) (Exporter un tableau de bord) | Vous pouvez exporter un tableau de bord sous forme de fichier JSON. |
| [Import a dashboard](logging_kibana_analize_logs_dashboard.html#k4_dashboard_import) (Importer un tableau de bord) | Vous pouvez importer un tableau de bord depuis un fichier JSON. |
| [Share a dashboard](logging_kibana_analize_logs_dashboard.html#k4_dashboard_share) (Partager un tableau de bord) | Vous pouvez partager un tableau de bord via votre source HTML ou via le tableau de bord Kibana. |
| [Add a visualization](logging_kibana_analize_logs_dashboard.html#k4_dashboard_add_visualization) (Ajouter une visualisation) | Vous pouvez ajouter une visualisation ou une recherche existante à un tableau de bord.|

Pour plus d'informations sur Kibana, reportez-vous au manuel [Kibana User Guide ![Icône de lien externe](../../../icons/launch-glyph.svg "Icône de lien externe")](https://www.elastic.co/guide/en/kibana/4.1/index.html){: new_window}.



## Création d'un nouveau tableau de bord Kibana
{: #K4_dashboard_new}

Pour créer un nouveau tableau de bord, procédez comme suit :

1. Dans la barre d'outils du tableau de bord, cliquez sur le bouton **New dashboard** (Nouveau tableau de bord) ![Nouveau tableau de bord](images/k4_dash_new_icon.jpg "Nouveau tableau de bord").

2. Ajoutez une ou plusieurs recherches et visualisations. Pour plus d'informations, voir [Ajout d'une nouvelle recherche ou visualisation](logging_kibana_analize_logs_dashboard.html#K4_dashboard_add_visualization).

    Lorsque vous ajoutez une recherche ou une visualisation, un panneau est ajouté au tableau de bord.

3. Faites glisser un panneau et déposez-le à l'emplacement où vous désirez le positionner sur le tableau de bord.
 
4. Sauvegardez le tableau de bord pour une réutilisation ultérieure. Pour plus d'informations, voir [Sauvegarde d'un tableau de bord Kibana](logging_kibana_analize_logs_dashboard.html#k4_dashboard_save).


## Ajout d'une nouvelle recherche ou visualisation
{: #k4_dashboard_add_visualization}

Pour ajouter une virtualisation ou une recherche existante, procédez comme suit :

1. Dans la barre d'outils de la page Dashboard, cliquez sur le bouton **Add visualization** (Ajouter une visualisation) ![Ajouter une visualisation](images/k4_dash_add_visualization_icon.jpg "Ajouter une visualisation").

    **Remarque **: vous pouvez ajouter des visualisations et des recherches. 

2. Sélectionnez l'onglet **Visualizations** pour ajouter une visualisation ou l'onglet **Searches** pour ajouter une recherche.

3. Cliquez sur la recherche ou la visualisation que vous désirez ajouter.

    Un panneau pour la recherche ou la visualisation concernée est ajouté au tableau de bord.



## Sauvegarde d'un tableau de bord Kibana
{: #k4_dashboard_save}

Procédez comme suit pour sauvegarder un tableau de bord Kibana après l'avoir personnalisé :

1. Dans la barre d'outils, cliquez sur le bouton **Save** (Sauvegarder) ![Sauvegarder le tableau de bord](images/k4_dash_save_icon.jpg "Sauvegarder le tableau de bord)").

2. Entrez un nom pour le tableau de bord.

    **Remarque :** Si vous tentez de sauvegarder un tableau de bord avec un nom contenant des espaces vides, l'opération échoue.

3. Cliquez sur l'icône **Save** (Sauvegarder) en regard de la zone de nom.


## Suppression d'un tableau de bord Kibana
{: #k4_dashboard_delete}

Pour supprimer une visualisation, procédez comme suit dans la page Settings (Paramètres) :

1. Dans la page Settings (Paramètres), sélectionnez l'onglet **Objects** (Objets).

2. Dans l'onglet **Visualizations**, sélectionnez les visualisations que vous désirez supprimer.

3. Cliquez sur **Delete** (Supprimer).


## Chargement d'un tableau de bord Kibana
{: #k4_dashboard_reload}

Pour charger un tableau de bord sauvegardé, procédez comme suit :

1. Dans la barre d'outils de la page Dashboard, cliquez sur le bouton **Load Saved Dashboard** (Charger un tableau de bord sauvegardé) ![Charger un tableau de bord sauvegardé](images/k4_dash_load_icon.jpg "Charger un tableau de bord sauvegardé").

2. Sélectionnez le tableau de bord que vous désirez charger. 


## Exportation d'un tableau de bord Kibana
{: #k4_dashboard_export}

Pour exporter un tableau de bord sous forme de fichier JSON, procédez comme suit dans la page Settings (Paramètres) :

1. Dans la page Settings (Paramètres), sélectionnez l'onglet **Objects** (Objets).

2. Dans l'onglet **Dashboard**, sélectionnez le tableau de bord que vous désirez exporter.

3. Cliquez sur **Export** (Exporter).

4. Sauvegardez le fichier. 


## Importation d'un tableau de bord Kibana
{: #k4_dashboard_import}

Pour importer un tableau de bord depuis un fichier JSON, procédez comme suit dans la page Settings (Paramètres) :

1. Dans la page Settings (Paramètres), sélectionnez l'onglet **Objects** (Objets).

2. Dans l'onglet **Dashboard**, sélectionnez **Import** (Importer).

3. Sélectionnez un fichier et cliquez sur **Open** (Ouvrir).

Le tableau de bord est ajouté à la liste des tableaux de bord.


## Partage d'un tableau de bord Kibana
{: #k4_dashboard_share}

Pour partager un tableau de bord, procédez comme suit :

1. Dans la barre d'outils de la page Dashboard, cliquez sur le bouton **Share dashboard** (Partager le tableau de bord) ![Partager le tableau de bord](images/k4_dash_share_icon.jpg "Partager le tableau de bord").

2. Sélectionnez l'une des options suivantes :

    * **Embed this dashboard** (Incorporer le tableau de bord): Sélectionnez cette option pour partager le tableau de bord via votre source HTML . 
    
        Cliquez sur le bouton Copy (Copier) ![Copier dans le presse-papiers](images/k4_copy_to_clipboard.jpg "Copier dans le presse-papiers") pour copier le code HTML que vous pouvez utiliser pour incorporer le tableau de bord dans votre source HTML. 
        
        **Remarque **: pour voir le tableau de bord, les utilisateurs doivent pouvoir accéder à Kibana.
	
    * **Share a link** (Partager un lien):  Sélectionnez cette option pour partager le tableau de bord dans Kibana avec d'autres utilisateurs.



