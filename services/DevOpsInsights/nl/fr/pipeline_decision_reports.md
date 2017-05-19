---

copyright:
  years: 2016, 2017
lastupdated: "2017-02-13"

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}

# Affichage de tableaux de bord et de rapports
{: #DRA_toolchain_reports}

{{site.data.keyword.DRA_short}} vous fournit une multitude d'informations exploitables sur vos projets.
{:shortdesc}

## Tableaux de bord {{site.data.keyword.DRA_short}}    
{: #DI_toolchain_dashboards}

{{site.data.keyword.DRA_short}} fournit des tableaux de bord qui affichent des informations sur les performances de votre organisation Bluemix. Pour les afficher après l'ouverture de {{site.data.keyword.DRA_short}}, cliquez sur **Build Verification** ou **Deploy Verification**.

Les tableaux de bord sont automatiquement remplis avec les informations les plus récentes des travaux de test {{site.data.keyword.DRA_short}} de vos pipelines. Cliquez sur les éléments inclus dans les tableaux de bord pour en afficher des informations détaillées.

### Indicateurs clés de performance dans les générations    
{: #DI_key_performance_indicators}

La page **Build Verification** contient trois graphiques d'informations sur la santé de la branche de développement sélectionnée :

<table>
<thead>
<tr>
<th>Graphique</th>
<th>Description</th>
</tr>
</thead>

<tbody>
<tr>
<td>Latest Builds</td>
<td>Nombre de générations récentes terminées par rapport au nombre total de générations récentes.</td>
</tr>
<tr>
<td>Tests</td>
<td>Nombre de tests ayant abouti par rapport au nombre total de tests.</td>
</tr>
<tr>
<td>Code Coverage</td>
<td>Pourcentages d'instructions et de fonctions du code appelées par les tests.</td>
</tr>
</tbody></table>

## Affichage de rapports de décision    
{: #DI_decision_reports}

Après l'exécution d'un pipeline, {{site.data.keyword.DRA_short}} commence à collecter et à analyser les résultats de test correspondants pour établir une base de référence. Les données de chaque exécution ultérieure sont collectées et comparées aux résultats précédents. Des jalons de décision utilisent ces données pour déterminer le moment auquel un déploiement doit être arrêté. 

Pour afficher le rapport de décision pour un jalon du pipeline, procédez comme suit :

   1. A l'étape qui contient le jalon à vérifier, cliquez sur **Afficher les journaux et l'historique**.

   2. Dans la fenêtre de travaux de l'étape, cliquez sur le nom du jalon.

   3. Dans la vue du journal, recherchez le message 'Check {{site.data.keyword.DRA_short}} report here' et cliquez sur le lien fourni pour ouvrir le rapport.
