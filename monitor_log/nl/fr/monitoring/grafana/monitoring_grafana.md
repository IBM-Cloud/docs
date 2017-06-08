---

copyright:
  years: 2015, 2017

lastupdated: "2017-04-06"

---


{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}
{:screen: .screen}

# Création d'un tableau de bord Grafana
{:#monitoring_grafana}

Vous pouvez créer un tableau de bord Grafana personnalisé afin d'afficher des métriques pour tous les conteneurs s'exécutant dans un espace de votre organisation {{site.data.keyword.Bluemix}}.
{:shortdesc}

Pour créer un tableau de bord Grafana, procédez comme suit :

1. Lancez Grafana depuis un navigateur Web. Pour plus d'informations, voir [Accès au tableau de bord Grafana depuis un navigateur Web](monitoring_analyzing_metrics_grafana.html#launch_grafana_from_browser).

2. Sauvegardez le tableau de bord par défaut.

    1. Dans la barre d'outils, cliquez sur l'icône Save (Sauvegarder).
    2. Entrez un nom pour le tableau de bord.
    3. En regard de la zone du nom, cliquez sur l'icône Save (Sauvegarder).
   
3. Désactivez l'actualisation automatique de page lorsque vous travaillez dans votre tableau de bord. 

    1. Cliquez sur le sélecteur de période situé dans l'en-tête.
    2. Sélectionnez **Actualisation automatique**.
    3. Cliquez sur **Désactivée**.
 
 5. Supprimez les lignes d'exemple.
 
     1. En regard de l'en-tête *Welcome to Grafana* (Bienvenue dans Grafana), positionnez le curseur sur le menu Row (Ligne) et cliquez sur le menu Row qui apparaît.
     2. Cliquez sur **Delete row** (Supprimer la ligne), puis sur **Yes** (Oui).
     
     Répétez ces étapes pour supprimer les liens vers la documentation et les lignes associées à First Graph (Premier graphique). 
     
     Dans l'en-tête de la page, modifiez le sélecteur d'heure pour vous assurer que vous pouvez voir les données. La valeur par défaut va de 6 heures à quelques secondes auparavant. Sélectionnez
**Last 30d**.
     
6. Ajoutez une visualisation.

    * Pour ajouter une visualisation d'UC inactive, voir [Ajout d'une visualisation d'UC inactive](monitoring_grafana.html#grafana_add_cpu).
    * Pour ajouter une visualisation de la mémoire utilisée, voir [Ajout d'une visualisation de la mémoire utilisée](monitoring_grafana.html#grafana_add_mem).
        
7. Sauvegardez le tableau de bord personnalisé.

    1. Dans la barre d'outils, cliquez sur l'icône Save (Sauvegarder).
    2. Entrez un nom pour le tableau de bord.
    3. En regard de la zone du nom, cliquez sur l'icône Save (Sauvegarder).
    

## Ajout d'une visualisation d'UC inactive
{:#grafana_add_cpu}

Pour ajouter un graphique d'UC inactive pour tous les conteneurs dans votre espace, procédez comme suit :

1. Cliquez sur le bouton **Ajouter une ligne**. Un curseur de menu Row (Ligne) est affiché sur le côté de la ligne.
    
2. Positionnez-vous sur le curseur du menu ligne, puis cliquez sur l'icône de menu Row (Ligne) qui apparaît.

3. Cliquez sur **Add Panel** (Ajouter un panneau). Cliquez ensuite sur **graph** (graphique).

4. Cliquez sur le titre du graphique pour ouvrir le menu du panneau, puis cliquez sur **Edit** (Editer). 

    Le reste du tableau de bord est masqué ; seul l'éditeur de ce graphique et un aperçu de celui-ci sont affichés.
    
5. Dans l'onglet Metrics (Métriques), construisez une requête pour collecter les données du graphique. 

    Par exemple, lorsque vous travaillez avec des conteneurs, la requête inclut l'ID de l'espace, l'ID d'un groupe de conteneurs et l'ID d'une instance de conteneur unique, sous le format suivant : `ID_espace.ID_groupe.ID_instance.métrique`
        
    1. Sur la ligne A, cliquez sur **Select metric** (Sélectionner une métrique). Sélectionnez ensuite votre ID d'espace.
    2. Cliquez sur **Select metric** (Sélectionner une métrique) et sélectionnez l'astérisque (\*).
    
    Lorsque vous sélectionnez l'astérisque (\*), les données incluent des métriques de chaque groupe de conteneurs dans l'espace. Vous avez la possibilité d'adapter ce format en utilisant une expression régulière afin de n'inclure les métriques que de certains conteneurs. Par exemple, si vous ne
désirez examiner que les métriques de conteneurs uniques et non de groupes de conteneurs, cliquez sur
**Sélectionner une métrique** et sélectionnez **0000**.
        
    3. Cliquez sur **Select metric** (Sélectionner une métrique) et sélectionnez à nouveau l'astérisque (\*). Ce format inclut des métriques pour chaque conteneur unique dans l'espace.
        
    4. Cliquez sur **Sélectionner une métrique**, puis sur **cpu-0**.
        
    5. Cliquez sur **Sélectionner une métrique**, puis sur **cpu-idle**. L'aperçu du graphique est actualisé et affiche les métriques correspondant à cette requête.
    
6. Facultatif : Personnalisez l'affichage du graphique.
    
    * Pour attribuer un nom au graphique, cliquez sur l'onglet General (Général) et dans la zone Title (Titre), entrez un nom pour le graphique (par exemple, UC inactive).
    * Pour attribuer un libellé à l'axe vertical, cliquez sur l'onglet Axes and grid (Axes et grilles) et dans la section Left Y Axis (Axe Y gauche), dans l'onglet Label (Libellé), entrez UC.
    * Pour modifier la couleur d'arrière-plan du graphique, dans la section Grid threshholds (Seuils de grille), pour Level 2 (Niveau 2), cliquez sur l'icône de sélection de couleur d'arrière-plan en sélectionnant la couleur blanche ou gris clair.
    
    Dans l'en-tête, cliquez sur **Retour au tableau de bord**.
    
7. Pour sauvegarder les modifications apportées à ce tableau de bord, dans l'en-tête, cliquez sur l'icône Save (Sauvegarder), puis cliquez sur l'icône Save dans le menu.


## Ajout d'une visualisation de la mémoire utilisée
{:#grafana_add_mem}

Pour ajouter une visualisation de la mémoire utilisée, procédez comme suit :

1. Cliquez sur le bouton Add a row (Ajouter une ligne). Un curseur de menu Row (Ligne) est affiché sur le côté de la ligne.
   
2. Positionnez-vous sur le curseur du menu ligne, puis cliquez sur l'icône de menu Row (Ligne) qui apparaît.

    1. Cliquez sur Add Panel > graph (Ajouter un panneau : graphique).
    2. Cliquez sur Edit (Editer). Le reste du tableau de bord est masqué ; seul l'éditeur de ce graphique et un aperçu de celui-ci sont affichés.
    
3. Dans l'onglet Metrics (Métriques), construisez une requête pour collecter les données du graphique. 

    Par exemple, lorsque vous travaillez avec des conteneurs, la requête inclut l'ID de l'espace, l'ID d'un groupe de conteneurs et l'ID d'une instance de conteneur unique, sous le format suivant : ID_espace.ID_groupe.ID_instance.métrique
        
    1. Sur la ligne A, cliquez sur **Select metric** (Sélectionner une métrique). Sélectionnez ensuite votre ID d'espace.
    2. Cliquez sur **Select metric** (Sélectionner une métrique) et sélectionnez l'astérisque (\*).
    
    Lorsque vous sélectionnez l'astérisque (\*), les données incluent des métriques de chaque groupe de conteneurs dans l'espace. Vous pouvez également adapter ce format en utilisant une expression régulière afin de n'inclure les métriques que de certains conteneurs. Par exemple, si vous ne
désirez examiner que les métriques de conteneurs uniques et non de groupes de conteneurs, cliquez sur
**Sélectionner une métrique** et sélectionnez **0000**.
    
    3. Cliquez sur **Select metric** (Sélectionner une métrique) et sélectionnez à nouveau l'astérisque (\*). Ce format inclut des métriques pour chaque conteneur unique dans l'espace.
        
    4. Cliquez sur **Select metric** (Sélectionner une métrique) et sur **memory** (mémoire).
        
    5. Cliquez sur **Select metric** (Sélectionner une métrique) et sur **memory-used** (mémoire utilisée). L'aperçu du graphique est actualisé et affiche les métriques correspondant à cette requête.
    
6. Facultatif : Personnalisez l'affichage du graphique.
    
    * Pour attribuer un nom au graphique, cliquez sur l'onglet General (Général) et dans la zone Title (Titre), entrez un nom pour le graphique (par exemple, Mémoire utilisée).
    *  Pour modifier le format des valeurs de l'axe X, cliquez sur l'onglet Axes and grid (Axes et grilles) et dans la section Left Y Axis (Axe Y gauche), pour Format, sélectionnez "bytes" (octets).
    * Pour attribuer un libellé à l'axe vertical, dans la zone Label (Label), entrez Mémoire.
    * Pour modifier la couleur d'arrière-plan du graphique, dans la section Grid threshholds (Seuils de grille), pour Level 2 (Niveau 2), cliquez sur l'icône de sélection de couleur d'arrière-plan en sélectionnant la couleur blanche ou gris clair.
    
    Dans l'en-tête, cliquez sur **Retour au tableau de bord**.

7. Pour sauvegarder les modifications apportées à ce tableau de bord, dans l'en-tête, cliquez sur l'icône Save (Sauvegarder), puis cliquez sur l'icône Save dans le menu.

