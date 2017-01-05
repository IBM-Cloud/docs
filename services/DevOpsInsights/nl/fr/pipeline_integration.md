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

# Intégration de {{site.data.keyword.DRA_short}} à {{site.data.keyword.deliverypipeline}}
{: #toolchain_configure_pipeline}

Une fois que vous avez ajouté {{site.data.keyword.DRA_full}} à une chaîne d'outils et défini les stratégies qu'il surveille, vous devez intégrer {{site.data.keyword.DRA_short}} à votre pipeline.
{:shortdesc}

<!--##Configuring the {{site.data.keyword.deliverypipeline}}

{: #toolchain_integration}
To use {{site.data.keyword.DRA_short}}, add it to any toolchain that uses the {{site.data.keyword.deliverypipeline}}.

1. In {{site.data.keyword.Bluemix_notm}}, on the **Toolchains** tab, open a toolchain.

2. On the toolchain's Overview page, click the add (+) button.

3. In the Tool Integrations section, select **{{site.data.keyword.DRA_short}}**.

4. Click **Create Integration**.

5. In your toolchain, click the {{site.data.keyword.deliverypipeline}} tile. You can configure {{site.data.keyword.DRA_short}} in any number of pipelines.-->

## Préparation des étapes de pipeline pour {{site.data.keyword.DRA_short}}
{: #toolchain_pipeline_props}

Vous devez créer plusieurs propriétés d'environnement dans chaque étape de pipeline contenant des travaux de génération ou de déploiement :

1. Cliquez sur **Configuration de l'étape** puis sur **Configurer l'étape**.

2. Cliquez sur **PROPRIETES D'ENVIRONNEMENT**.

3. Ajoutez les trois propriétés de texte suivantes, puis enregistrez les modifications apportées à l'étape :

<table><thead>
<tr>
<th>Propriété d'environnement</th>
<th>Description</th>
</tr>
</thead><tbody>
<tr>
<td><code>LOGICAL_APP_NAME</code></td>
<td>Nom d'application apparaissant sur les tableaux de bord {{site.data.keyword.DRA_short}}. </td>
</tr>
<tr>
<td><code>LOGICAL_ENV_NAME</code></td>
<td>Nom de l'environnement dans lequel l'application s'exécute. Cette propriété est utilisée pour catégoriser l'application dans les tableaux de bord {{site.data.keyword.DRA_short}}.</td>
</tr>
<tr>
<td><code>BUILD_PREFIX</code></td>
<td>Préfixe ajouté à des générations (voir les tableaux de bord {{site.data.keyword.DRA_short}}).</td>
</tr>
</tbody></table>


## Mise à jour des travaux de test pour {{site.data.keyword.DRA_short}}
{: #toolchain_pipeline_upload}

Pour commencer, extrayez les informations de configuration d'un travail de test.

1. Dans l'étape contenant un travail de test, cliquez sur l'icône **Configuration de l'étape** ![Icône de configuration d'étape de pipeline](images/pipeline-stage-configuration-icon.png). Cliquez sur **Configurer l'étape**.
2. Créez un travail. Pour le type de travail, sélectionnez **Tester**.
3. Sélectionnez un travail de test qui utilise le type de testeur Simple et copiez dans un éditeur les informations des zones **Commande de test** et **Répertoire de travail**. Vous aurez besoin de ces informations ultérieurement.
4. A partir du travail de test Simple, changez de type de testeur en sélectionnant **Testeur avancé**.
5. Dans la zone **Commande de test**, collez les commandes que vous avez collées à partir de la zone **Commande de test** du travail de test Simple.
6. Dans la zone **Répertoire de travail**, collez le chemin que vous avez copié de la zone **Répertoire de travail** du travail de test Simple.
7. Renseignez les autres zones pour télécharger les résultats d'un type de test déterminé. Si vous souhaitez télécharger les résultats pour un deuxième type de test dans le même travail, renseignez également les zones d'attribut *supplémentaire*.

 * Type d'indicateur
 * Format
 * Emplacement du fichier de résultats
8. Cliquez sur **Sauvegarder** pour revenir au pipeline.

Les valeurs des zones contenant le **type d'indicateur** et l'**emplacement du fichier de résultats** doivent correspondre au format correct.

<table><thead>
<tr>
<th>Type d'indicateur</th>
<th>Formats pris en charge</th>
</tr>
</thead><tbody>
<tr>
<td>Test de vérification fonctionnelle</td>
<td>Mocha, JUnit</td>
</tr>
<tr>
<td>Test unitaire</td>
<td>Mocha, JUnit, Karma/Mocha</td>
</tr>
<tr>
<td>Couverture de code</td>
<td>Istanbul, Blanket.js</td>
</tr>
</tbody></table>

La *figure 1* représente un travail de test configuré pour exécuter des tests unitaires, télécharger les résultats au format Mocha et télécharger les résultats de couverture de code au format Istanbul.

![Travail de téléchargement Deployment Risk Analytics](images/DRA_upload_job.png) *Figure 1. Télécharger les résultats dans DevOps Analytics*

## Définition de points de contrôle {{site.data.keyword.DRA_short}} dans le pipeline
{: #toolchain_pipeline_gates}

Les points de contrôle {{site.data.keyword.DRA_short}} vérifient si vos résultats de test sont conformes à la stratégie définie. Si la stratégie n'est pas respectée, le point de contrôle {{site.data.keyword.DRA_short}} signale un échec. Habituellement, les points de contrôle sont placés à la fin de chaque étape de votre pipeline. Cet emplacement est idéal pour vérifier la qualité de la génération en fonction de votre stratégie, dans le but de garantir la sécurité d'une promotion entre deux environnements. Toutefois, vous pouvez placer des points de contrôle dans le pipeline à tout emplacement auquel vous voulez vérifier un critère spécifique.

1. Dans une étape, cliquez sur l'icône **Configuration de l'étape** ![Icône de configuration d'étape de pipeline](images/pipeline-stage-configuration-icon.png), puis sur **Configurer l'étape**.
2. Cliquez sur **Ajouter un travail**. Pour le type de travail, sélectionnez **Tester**.
3. Entrez un nom pour le nouveau travail (par exemple, *Gate (Test unitaire)*).
4. Pour le type de testeur, sélectionnez **{{site.data.keyword.DRA_short}} Gate**.
5. Indiquez le nom d'environnement. Assurez-vous que cette valeur correspond à celle définie dans vos [propriétés d'environnement](#toolchain_pipeline_props).
6. Définissez le nom de la stratégie à vérifier ce point de contrôle.

 Ce nom doit correspondre à l'un des noms de stratégie que vous avez définis. Vous ne pouvez indiquer que les stratégies définies dans la même organisation {{site.data.keyword.Bluemix_notm}} que votre chaîne d'outils.

7. Facultatif : pour créer une fonction de point de contrôle en mode recommandation, décochez la case **Arrêter d'exécuter cette étape si ce travail échoue**. En mode recommandation, {{site.data.keyword.DRA_short}} effectue la même analyse de stratégie au point de contrôle et génère des rapports, mais en cas de panne, le pipeline n'est pas arrêté.
8. Cliquez sur **Sauvegarder** pour revenir au pipeline.
9. Configurez des points de contrôle pour toutes vos stratégies {{site.data.keyword.DRA_short}} en répétant ces étapes.

![Travail Mocha Deployment Risk Analytics](images/DRA_gate_job.png) *Figure 2. Point de contrôle DevOps Analytics*

Une fois que vous avez configuré le pipeline, commencez à utiliser {{site.data.keyword.DRA_short}}. Pour obtenir les instructions correspondantes, voir [Affichage de tableaux de bord et de rapports](./pipeline_decision_reports.html#toolchain_reports).
