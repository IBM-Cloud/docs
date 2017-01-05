---

copyright:
  years: 2016
lastupdated: "2016-11-11"

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}

# Initiation à {{site.data.keyword.DRA_short}} (Expérimental)
{: #gettingstarted}

Utilisez {{site.data.keyword.DRA_full}} pour identifier les risques associés à vos générations et déploiements.
{:shortdesc}

{{site.data.keyword.DRA_short}} agrège et analyse les résultats provenant de tests unitaires, de tests fonctionnels et d'outils de couverture de code afin de déterminer si votre code satisfait les stratégies prédéfinies à des points de contrôle spécifiques de votre processus de déploiement. Si votre code ne satisfait pas ou dépasse une stratégie, le déploiement est interrompu afin de prévenir toute modification à risque. Vous pouvez utiliser {{site.data.keyword.DRA_short}} comme filet de sécurité pour votre environnement de distribution continue en vue d'implémenter et d'améliorer les normes qualité au fil du temps, ainsi que comme outil de visualisation de données pour vous aider à comprendre la santé de votre projet.

{{site.data.keyword.DRA_short}} est une offre expérimentale et est fourni en l'état à des fins de développement et d'expérimentation uniquement. Pour utiliser {{site.data.keyword.DRA_short}}, ajoutez-le à toute chaîne d'outils qui emploie {{site.data.keyword.deliverypipeline}}.

{: #catalog}
Pour accéder à l'interface utilisateur de {{site.data.keyword.DRA_short}}, procédez comme suit à partir d'une chaîne d'outils existante :

1. Cliquez sur le bouton **Ajouter un outil**.

2. Cliquez sur **{{site.data.keyword.DRA_short}}**.

3. Cliquez sur **Créer une intégration**.

4. Cliquez sur la vignette **{{site.data.keyword.DRA_short}}**.

5. Terminez votre configuration en effectuant les tâches restantes :

	1. [Configurez l'intégration à {{site.data.keyword.deliverypipeline}}](./pipeline_integration.html).
	2. Exécutez le pipeline et [passez en revue les tableaux de bord {{site.data.keyword.deliverypipeline}}](./pipeline_decision_reports.html).
	3. [Définissez les stratégies](./create_criteria.html) que {{site.data.keyword.DRA_short}} doit gérer.
	4. Réexécutez le pipeline pour vérifier que votre projet satisfait à vos stratégies.


# Liens connexes
{: #rellinks}

## Tutoriels et exemples
{: #samples}

* [Using analytics to advise on the likelihood of successful deployments](https://www.ibm.com/devops/method/content/deliver/tool_deployment_risk_analytics/){:new_window}

## Liens connexes
{: #general}

* [Initiation aux chaînes d'outils](https://new-console.ng.bluemix.net/docs/toolchains/toolchains_overview.html){:new_window}
* [Initiation à Delivery Pipeline](https://new-console.ng.bluemix.net/docs/services/DeliveryPipeline/index.html){:new_window}
* [Fiche des prix IBM Bluemix](https://new-console.ng.bluemix.net/pricing/){:new_window}
* [Prérequis IBM Bluemix](https://developer.ibm.com/bluemix/support/?cm_mc_uid=96503159749414585876298&cm_mc_sid_50200000=1462802909#prereqs){:new_window}
