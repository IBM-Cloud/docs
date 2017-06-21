---

copyright:
  years: 2017
lastupdated: "2017-03-14"

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}

# Mappage d'environnements à des rapports
{: #uc_insights_mapping}

Les informations affichées dans Delivery Insights sont regroupées par *environnements logiques*, qui sont des collections d'environnements IBM UrbanCode Deploy (également appelés *environnements physiques*). Vous pouvez regrouper vos environnements en environnements logiques comme vous le souhaitez en fonction de votre organisation.
{:shortdesc}

## Environnements logiques

Delivery Insights regroupe vos environnements IBM UrbanCode Deploy en un ou plusieurs environnements logiques. Vous pouvez ainsi collecter des environnements en groupes qui sont pertinents pour vous et votre organisation. Par exemple, si vous disposez de plusieurs environnements de production pour plusieurs applications, vous pouvez regrouper tous ces environnements en un seul environnement logique et combiner les mesures de tous ces environnements en un seul tableau de bord d'environnement de production. Le mappage s'effectue par chaîne de recherche. Vous pouvez donc regrouper les environnements comme vous le souhaitez en fonction de vos serveurs IBM UrbanCode Deploy.

## Environnements logiques par défaut

Par défaut, vos rapports incluent des environnements logiques qui correspondent aux environnements IBM UrbanCode Deploy grâce à des chaînes. Par exemple, tous les environnements dont le nom comporte "dev" sont mappés à l'environnement logique DEV, et tous les environnements dont le nom inclut "prod" sont mappés à l'environnement logique PROD.

![Environnements logiques par défaut](images/uc_insights_mapping.gif)

## Mappage des environnements à des environnements logiques

Vous pouvez mapper manuellement des environnements physiques à des environnements logiques, ou vous pouvez utiliser des masques pour associer dynamiquement des environnements physiques à des environnements logiques.

Pour mapper des environnements physiques à des environnements logiques à l'aide d'un masque, procédez comme suit :

1. Dans {{site.data.keyword.DRA_short}}, cliquez sur **Delivery Insights > Map Environments**.
1. Cliquez sur un environnement logique existant ou sur **Add Logical Environment**.
1. Dans les paramètres de l'environnement logique, sous **Patterns**, cliquez sur **Add Pattern**.
1. Indiquez un masque pour les noms d'environnement. Vous pouvez utiliser l'astérisque (*) comme caractère générique. Par exemple, le masque `env` correspond aux environnements `env1`, `env2` et `env`.
1. Vérifiez que l'environnement logique contient les environnements que vous souhaitez.

Pour mapper manuellement des environnements à des environnements logiques, cliquez sur **Add Manually** et sélectionnez les environnements à ajouter ou à retirer.

![Configuration de l'intégration dans DevOps Connect](images/uc_insights_mapping_manually.gif)

Maintenant que vous avez mappé des environnements à des environnements logiques, vous pouvez afficher les informations des rapports regroupées en fonction de ces environnements logiques.
