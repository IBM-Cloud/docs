---

copyright:
  years: 2016, 2017
lastupdated: "2017-04-07"

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}

# A propos de Deployment Risk

{{site.data.keyword.DRA_short}} fournit un grand nombre d'informations sur vos déploiements, et en particulier sur les risques. Vous pouvez l'utiliser pour automatiser la protection de la qualité dans votre pipeline de distribution à l'aide de politiques et de jalons. 
{:shortdesc}

Après avoir ouvert {{site.data.keyword.DRA_short}} à partir de la chaîne d'outils, cliquez sur **Deployment Risk**. A partir de là, vous obtenez une présentation des applications de vos environnements de préproduction et de production, et vous pouvez effectuer une exploration en aval pour comprendre la couverture de code, les performances du test et les rapports de sécurité. Les tableaux de bord sont automatiquement remplis avec les informations les plus récentes provenant des tests {{site.data.keyword.DRA_short}} de vos pipelines.

Vous pouvez utiliser Deployment Risk pour appliquer des normes de qualité dans votre chaîne d'outils grâce à des politiques et des jalons. Les politiques sont des ensembles de règles ; les jalons appliquent les politiques. Vous pouvez ainsi créer une politique "Test d'unité et couverture de test" qui exige des générations qu'elles répondent à des normes de test d'unité et de couverture de test. Vous pouvez ensuite ajouter un jalon qui se réfère à cette politique dans votre processus de distribution continue. Les générations qui ne satisfont pas la politique sont arrêtées au jalon. 

## Informations sur l'intégration

Deployment Risk s'intègre avec {{site.data.keyword.deliverypipeline}}, qui fait partie d'{{site.data.keyword.contdelivery_full}}, et avec les projets Jenkins. A un niveau élevé, les instructions d'utilisation de l'un ou de l'autre sont similaires.  

Si vous utilisez {{site.data.keyword.deliverypipeline}}, suivez les étapes ci-après :

1. [Créez des politiques et des règles](risk_policies.html) qui seront gérées par {{site.data.keyword.DRA_short}}.
2. [Préparez les étapes de votre pipeline](risk_cd.html) en vue de l'intégration avec {{site.data.keyword.DRA_short}}.
3. [Créez ou éditez des travaux de test](risk_cd.html) dans le pipeline qui téléchargent les résultats vers {{site.data.keyword.DRA_short}}.
4. [Ajoutez des jalons](risk_cd.html) au pipeline qui prend les décisions de promotion en fonction de ces résultats et de vos politiques.
5. Exécutez le pipeline et [affichez les résultats](results.html).

Si vous utilisez Jenkins, procédez comme suit :

1. [Créez des politiques et des règles](risk_policies.html) qui seront gérées par {{site.data.keyword.DRA_short}}.
2. [Installez et configurez le plug-in Jenkins](risk_jenkins.html).
3. [Créez les travaux de test et les jalons comme décrit dans les instructions du plug-in](risk_jenkins.html). Les tests téléchargent les résultats vers {{site.data.keyword.DRA_short}} en vue de l'analyse et les jalons utilisent ces résultats pour prendre les décisions quant aux promotions.
4. Exécutez le projet et [affichez les résultats](results.html). 

Peu importe la manière dont vous générez et déployez votre code, les résultats sont identiques : les générations qui satisfont les normes passent les jalons Deployment Risk et les générations qui ne répondent pas aux normes sont arrêtées. 

## Prérequis
{: #prerequisites}

Deployment Risk requiert une configuration plus poussée que la configuration décrite dans [Initiation à {{site.data.keyword.DRA_short}}](/docs/services/DevOpsInsights/index.html).

Pour utiliser Deployment Risk, vous avez besoin de deux éléments :

* Une instance de {{site.data.keyword.deliverypipeline}} ou un projet Jenkins
* Les tests que vous souhaitez utiliser pour évaluer votre projet
