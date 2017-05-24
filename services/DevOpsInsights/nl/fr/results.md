---

copyright:
  years: 2016, 2017

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}

# Affichage des résultats

## Evaluation des risques de déploiement

Après l'exécution d'un pipeline, {{site.data.keyword.DRA_short}} commence à collecter et à analyser les résultats de test correspondants pour établir une base de référence. Les données de chaque exécution ultérieure sont collectées et comparées aux résultats précédents. Des jalons de décision utilisent ces données pour déterminer le moment auquel un déploiement doit être arrêté. 

Le tableau de bord Deployment Risk vous permet d'afficher vos données de déploiement et d'évaluation au jalon. Pour ouvrir le tableau de bord, ouvrez {{site.data.keyword.DRA_short}}, puis, dans le menu latéral, cliquez sur **Deployment Risk**.

Si vous utilisez un pipeline {{site.data.keyword.contdelivery_short}}, vous pouvez afficher des rapports d'exécution de jalon individuels à partir du pipeline lui-même. Pour afficher le rapport de décision d'un jalon à partir du pipeline :

1. A l'étape qui contient le jalon à vérifier, cliquez sur **Afficher les journaux et l'historique**.

2. Dans le travail qui contient le jalon, cliquez sur le nom du jalon. 

3. Dans la vue du journal, recherchez le message `Check {{site.data.keyword.DRA_short}} report here` et cliquez sur le lien pour ouvrir le rapport.

## Rapports Developer Insights et Team Dynamics

Vous pouvez afficher des tableaux de bord sur votre équipe et votre code après une période d'exploration de données initiale. Dans le menu de navigation du service, cliquez sur **Developer Insights** ou sur **Team Dynamics**, puis sélectionnez une catégorie de donnée pour afficher ces informations.
