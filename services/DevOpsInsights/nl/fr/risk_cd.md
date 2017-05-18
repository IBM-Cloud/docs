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

# Intégration avec Continuous Delivery Pipeline

Après avoir ajouté {{site.data.keyword.DRA_short}} à une chaîne d'outils et avoir défini les politiques qu'il surveille, intégrez-le à {{site.data.keyword.deliverypipeline}}. Pour plus d'informations sur les pipelines, voir [la documentation officielle](/docs/services/ContinuousDelivery/pipeline_working.html).

## Préparation des étapes du pipeline
{: #integrate_pipeline}

Pour que Deployment Risk analyse votre projet, vous devez définir des étapes de préproduction et de production dans votre pipeline. Pour définir ces étapes, vous utilisez des propriétés d'environnement texte que vous trouvez dans le menu de configuration de chaque étape ![icône de configuration d'étape de pipeline](images/pipeline-stage-configuration-icon.png) sous **Propriétés d'environnement**.

1. A l'étape de préproduction, définissez la propriété `LOGICAL_ENV_NAME` sur `STAGING`. 

2. A l'étape de production, définissez la propriété `LOGICAL_ENV_NAME` sur `PRODUCTION`. 

Vous pouvez également ajouter les propriétés suivantes aux étapes qui génèrent ou déploient votre application : 

* `LOGICAL_APP_NAME`, qui définit le nom de l'application sur le tableau de bord. 
* `BUILD_PREFIX`, qui définit le texte ajouté en préfixe aux générations de l'étape. Ce texte s'affiche également sur le tableau de bord.  

## Ajout de travaux de test
{: #configure_pipeline_jobs}

Vous intégrez {{site.data.keyword.DRA_short}} dans votre pipeline grâce à deux sortes de travaux de test : les travaux qui téléchargent les résultats vers {{site.data.keyword.DRA_short}} en vue de l'analyse, et les jalons qui agissent sur cette analyse.  

Tout d'abord, vous ajoutez des travaux Advanced Tester à votre pipeline pour exécuter des tests et télécharger les résultats.  

**Remarque :** Si vous souhaitez mettre à jour un travail de test pour télécharger les résultats vers {{site.data.keyword.DRA_short}}, sauvegardez ses configurations dans un emplacement pratique avant de poursuivre. Ouvrez ensuite le menu de configuration du travail et passez à l'étape 3. 

1. A l'étape à laquelle vous souhaitez ajouter le travail qui télécharge les résultats, cliquez sur l'icône **Configuration de l'étape** ![Icône de configuration de l'étape de pipeline](images/pipeline-stage-configuration-icon.png). Cliquez sur **Configurer l'étape**.
2. Créez un travail de test et entrez un nom associé. 
3. Pour le type de travail, sélectionnez **Advanced Tester**.
4. Renseignez les zones **Commande de test** et **Répertoire de travail** comme vous le feriez pour un travail de test de pipeline normal. 
5. Renseignez les autres zones afin de télécharger les résultats de test pour un type de test particulier.  

 1. Choisissez le type de mesure qui correspond à ce que vous avez défini dans la politique {{site.data.keyword.DRA_short}} que vous voulez utiliser. 
 2. Indiquez l'emplacement du fichier de résultats. Cet emplacement est relatif par rapport au répertoire de travail.  

6. Si vous souhaitez télécharger les résultats d'un second type de test du même travail, renseignez les zones qui ont pour préfixe *Additional*.
7. Cliquez sur **Sauvegarder** pour revenir au pipeline.

Les valeurs des zones contenant le **type d'indicateur** et l'**emplacement du fichier de résultats** doivent correspondre au format correct.

<table><thead>
<tr>
<th>Type d'indicateur</th>
<th>Formats pris en charge</th>
</tr>
</thead><tbody>
<tr>
<td>Test de vérification fonctionnelle</td>
<td>Mocha, xUnit</td>
</tr>
<tr>
<td>Test d'unité</td>
<td>Mocha, xUnit, Karma/Mocha</td>
</tr>
<tr>
<td>Couverture de code</td>
<td>Istanbul, Blanket.js</td>
</tr>
</tbody></table>

La figure 1 représente un travail de test configuré pour exécuter des tests d'unité, télécharger les résultats au format Mocha et télécharger les résultats de couverture de code au format Istanbul. 

![Travail de téléchargement DevOps Insights](images/insights_upload_job.png) *Figure 1. Téléchargement des résultats dans DevOps Insights*

## Définition de jalons
{: #configure_pipeline_gates}

Les jalons {{site.data.keyword.DRA_short}} vérifient si vos résultats de test sont conformes à une politique définie. Si la politique n'est pas satisfaite, le jalon {{site.data.keyword.DRA_short}} échoue par défaut. Vous pouvez également configurer des jalons destinés à jouer un rôle de conseil pour autoriser la progression du pipeline même après un échec. 

Le tableau de bord Deployment Risk repose sur la présence d'un jalon après un travail de déploiement de préproduction. Si vous voulez utiliser le tableau de bord, vérifiez qu'il existe un jalon après le déploiement vers l'environnement de préproduction, mais avant le déploiement vers un environnement de production. 

Les jalons sont généralement placés avant la promotion de la génération dans votre pipeline. Ces emplacements sont parfaits pour le contrôle de la qualité de la génération par rapport aux politiques dans le but de garantir la sécurité de la promotion entre deux environnements. Toutefois, vous pouvez placer des jalons dans le pipeline à tout emplacement auquel vous voulez vérifier un critère spécifique. Les jalons placés avant le déploiement vers un environnement de préproduction appliquent les politiques, mais n'apparaissent pas dans le tableau de bord Deployment Risk.

1. Dans une étape, cliquez sur l'icône **Configuration de l'étape** ![Icône de configuration d'étape de pipeline](images/pipeline-stage-configuration-icon.png), puis sur **Configurer l'étape**.
2. Cliquez sur **Ajouter un travail**. Pour le type de travail, sélectionnez **Tester**.
3. Pour le type de testeur, sélectionnez **{{site.data.keyword.DRA_short}} Gate**.
4. Indiquez le nom d'environnement. Assurez-vous que cette valeur correspond à celle définie dans vos [propriétés d'environnement](#toolchain_pipeline_props).
5. Entrez le nom de la politique à vérifier à ce jalon. 

 Ce nom doit correspondre à l'un des noms de politique que vous avez définis. Vous ne pouvez indiquer que les politiques définies dans la même organisation {{site.data.keyword.Bluemix_notm}} que votre chaîne d'outils.

6. Facultatif : pour créer une fonction de jalon en mode recommandation, décochez la case **Arrêter d'exécuter cette étape si ce travail échoue**. En mode recommandation, {{site.data.keyword.DRA_short}} effectue la même analyse de politique au jalon et génère des rapports, mais en cas de panne, le pipeline n'est pas arrêté.
7. Cliquez sur **Sauvegarder** pour revenir au pipeline.
8. Configurez des jalons pour toutes vos politiques {{site.data.keyword.DRA_short}} en répétant ces étapes.

![Travail Mocha Deployment Risk](images/insights_gate_job.png) *Figure 2. Jalon DevOps Insights*

Une fois que vous avez configuré le pipeline, commencez à utiliser {{site.data.keyword.DRA_short}}. 
