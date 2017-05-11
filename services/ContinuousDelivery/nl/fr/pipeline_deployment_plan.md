---

copyright:
  years: 2017
lastupdated: "2017-3-16"

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen:.screen}
{:codeblock:.codeblock}

# Personnalisation des plans de déploiement pour les pipelines composites
{: #tasks_overview}

Dans un plan de déploiement pour un pipeline composite, une tâche représente une activité métier pertinente qui est associée à un déploiement de logiciel. Les tâches sont définies dans des plans de déploiement. 

{:shortdesc}

La plupart des tâches comportent un point de départ, un point de fin et une durée mesurable. Une tâche peut être de l'un des types suivants :

<ul>
<li>Les tâches manuelles peuvent représenter toute activité qui est associée à un déploiement de logiciel, telles que la mise hors ligne d'un serveur ou la mise à jour d'une base de données.</li>
<li>Les tâches UrbanCode Deploy représentent des applications IBM UrbanCode. Vous pouvez exécuter des applications IBM UrbanCode Deploy avec des tâches de type IBM UrbanCode Deploy.</li>
<li>Les tâches Continuous Delivery Pipeline représentent des instances de {{site.data.keyword.deliverypipeline}}, qui fait partie intégrante de {{site.data.keyword.contdelivery_full}}. Vous pouvez gérer vos instances de {{site.data.keyword.deliverypipeline}} avec ce type de tâche.</li>
<li>Les tâches différées représentent des événements critiques qui se produisent à un moment donné.</li>
<li>Les tâches d'en-tête sont des éléments organisationnels. Par exemple, vous pouvez utiliser une tâche d'en-tête pour identifier un groupe de tâches.</li>
</ul>

<!-- You can add tasks to deployment plans by creating tasks or you can import tasks from CSV files that are created by IBM UrbanCode Release or another application. You can also copy tasks from other deployment plans. See [Importing tasks](/docs/services/UCCR/UCCR_deployPlan.html#plan_importTasks) for information about the format of the CSV file. -->

## Création de tâches
{: #tasks_create}

Lorsque vous créez une tâche, vous sélectionnez le plan de déploiement auquel vous voulez ajouter la tâche. Par défaut, les nouvelles tâches sont insérées à la fin du plan de déploiement. Une fois qu'une tâche est créée, vous pouvez la déplacer ou la copier et la coller dans un autre plan de déploiement. Vous pouvez également créer des dépendances avec d'autres [tâches](/docs/services/ContinuousDelivery/pipeline_deployment_plan.html#tasks_dependencies).

Une fois que vous avez sauvegardé une tâche, des icônes d'action s'affichent pour cette tâche. Vous pouvez utilisez les icônes d'action pour modifier le statut de la tâche lors d'un déploiement. Toutes les tâches ont l'icône d'action **Ignorer**. D'autres icônes, comme **Démarrer**, s'affichent lorsque le contexte le nécessite. 

![](../UCCR/images/deploy-plan-intro.png "Typical deployment plan")

*Figure 1. Un plan de déploiement simple avec des tâches et des icônes d'action*

Chaque tâche d'un plan de déploiement se trouve sur une ligne distincte. Les informations qui s'affichent pour chaque tâche sont décrites dans le tableau ci-dessous.

### Tableau 1. Propriétés de tâche

| Propriété  | Description  |
| ------------------ | ------------------ |
| Nom               |Nom de la tâche       |
| Type               |Type de tâche : Manuelle, Continuous Delivery Pipeline, différée, électronique, en-tête/remarque, UrbanCode Deploy|             
| Statut             |Statut de la tâche : Non démarrée, terminée, en échec, ignorée, non applicable |
| Propriétaire              |Personne à laquelle la tâche est affectée                                                        |
| Heure de début  |Heure de début ou heure de début attendue en fonction du début planifié ou de la durée estimée des autres tâches        |
| Heure de fin               |Heure à laquelle la tâche a été résolue        |
| Durée               |Durée entre le début de la tâche et sa résolution (en minutes)        |
| Dépendances               |Nombre de tâches requises au préalable pour la tâche et qui en dépendent        |

---
Une fois que des tâches sont ajoutées aux plans de déploiement, vous pouvez les gérer de plusieurs façons :

   * Pour déplacer une tâche, faites-la glisser vers un nouvel emplacement.

   * Pour copier une tâche ou un groupe, cliquez sur la tâche, puis sur l'icône **Copier** <img class="inline" src="../UCCR/images/copy-group.png"  alt="copy icon">, placez le curseur à l'endroit où vous souhaitez insérer la tâche copiée, puis cliquez sur l'icône **Coller** <img class="inline" src="../UCCR/images/paste-group.png"  alt="paste icon">.

   * Pour couper une tâche ou un groupe à partir d'un plan de déploiement, cliquez sur la tâche, puis sur l'icône **Couper** <img class="inline" src="../UCCR/images/cut-group.png"  alt="cut icon">.

   * Pour supprimer une tâche, cliquez dessus, puis sur l'icône **Supprimer** <img class="inline" src="../UCCR/images/trash-group.png"  alt="delete icon">. La tâche est supprimée du plan de déploiement.

<!-- ## Creating UrbanCode Deploy tasks
{: #tasks_UDTasks}

UrbanCode Deploy tasks manage UrbanCode Deploy applications. When you run an UrbanCode Deploy task, the associated UrbanCode Deploy application runs by using the process, version, and environment specified by the task. You can set the version and environment at design time or wait and select them at run time.

During deployments, UrbanCode Deploy tasks start automatically when they become eligible to run.   

**Important** Applications become available after {{site.data.keyword.uccr_short}} is integrated with UrbanCode Deploy. The applications that are available to a deployment plan depend on the team that is assigned to the plan. The applications that are managed by the team in UrbanCode Deploy are also available in {{site.data.keyword.uccr_short}}.

Complete the following tasks to create an UrbanCode Deploy task.

1. On the Deployment Plan Details page, click **Create Task**. If you want to insert a task at a specific position in the plan, select a task before using the **Create Task**. The new task is inserted above the selected task.

1. On the Create Task dialog box, in the **Type** list, select **UrbanCode Deploy**.

1. In the **Name** field, enter a name for the task.

3. In the **Duration (minutes)** field, enter the number of minutes that you expect the task to run until it is completed. The estimated duration is used to calculate expected deployment times.

3. In the **Tags** list, attach a tag to the task. You can select multiple tags. To create a tag, type the tag name in list's text field.

3. In the **Application Name** list, select an application.

3. In the **Process** list, select an application process. Processes that belong to the selected UrbanCode Deploy application are available.

3. In the **Environment** list, select an application environment. Environments that belong to the selected UrbanCode Deploy application are available.  To postpone selecting an environment until you are ready to run the deployment, select **Use Version Tab**.

3. In the **Version** list, select an application version. Versions refer to IBM UrbanCode Deploy application snapshots. Versions that belong to the selected application are available.  To postpone selecting a version, select **Use Version Tab**. If the application process does not require a version, select **No Version**. You might select this last option if you are running a configuration-type process that does not require components.

3. In the **Assigned groups and users** list, assign the task to a user or group. The assigned user runs the task during deployment.

3. In the **Owner** list, select the task owner. The default owner is the user who created the task. The **Owner** list is displayed after the task is assigned to a user or group.    

5. Click **Save**. The task is inserted into the deployment plan.

After the task is created, the plan's **Version** tab is updated with information about the application assigned to the task. If you selected **Use Version Tab** for the application environment and version, use the Version tab to set those options before running the deployment. -->

## Création de tâches manuelles
{: #tasks_manual}

En général, les tâches manuelles représentent les activités qui sont associées à une édition de logiciel et qui ont un point de départ, un point de fin et une durée mesurable.

Pour créer une tâche manuelle, procédez comme suit :

1. Sur la page Deployment Plan Details, cliquez sur **Create Task**. Pour insérer une tâche à un endroit spécifique du plan, sélectionnez une tâche avant de cliquer sur **Create Task**. La nouvelle tâche est insérée au-dessus de la tâche sélectionnée.

1. Dans la fenêtre Create Task, dans la liste **Type**, sélectionnez **Manual**.

1. Dans la zone **Name**, saisissez un nom pour la tâche.

3. Dans la zone **Duration (minutes)**, saisissez le nombre de minutes prévu avant la fin de l'exécution de la tâche. La durée estimée est utilisée pour calculer les délais de déploiement attendus. 

3. Dans la liste **Tags**, attachez une étiquette à la tâche. Vous pouvez sélectionner plusieurs étiquettes. Pour créer une étiquette, saisissez son nom dans la zone de texte de la liste. 

3. Dans la liste **Assigned groups and users**, affectez la tâche à un utilisateur ou un groupe. L'utilisateur affecté exécute la tâche lors du déploiement. 

3. Dans la liste **Owner**, sélectionnez le propriétaire de la tâche. Le propriétaire par défaut est l'utilisateur qui a créé la tâche. La liste **Owner** s'affiche une fois que la tâche est affectée à un utilisateur ou un groupe.     

5. Cliquez sur **Save**. La tâche est insérée dans le plan de déploiement.

## Création de tâches différées
{: #tasks_delayed}

Les tâches différées représentent des événements clés ou critiques lors d'un déploiement. Elles permettent de s'assurer que les tâches importantes commencent à l'heure prévue. En général, les tâches différées sont requises au préalable pour d'autres tâches importantes. 

Une tâche différée démarre dès qu'elle est éligible à l'exécution et se termine à une heure spécifiée par l'utilisateur. Une tâche démarrée de type différé a le statut "En cours" jusqu'à ce qu'elle atteigne l'heure à laquelle elle est planifiée, où son statut devient alors "Terminé". Lorsqu'une tâche différée est terminée, les tâches qui en
dépendent commencent à s'exécuter. 

Pour créer une tâche différée, procédez comme suit :

1. Sur la page Deployment Plan Details, cliquez sur **Create Task**. Si vous voulez insérer une tâche à un endroit spécifique du plan, sélectionnez une tâche avant de cliquer sur **Create Task**. La nouvelle tâche est insérée au-dessus de la tâche sélectionnée.

1. Dans la fenêtre de création de tâche, dans la liste **Type**, sélectionnez **Delayed**.

1. Dans la zone **Name**, saisissez un nom pour la tâche.

3. Dans la zone **Time**, saisissez ou sélectionnez l'heure à laquelle la tâche sera terminée.

3. Dans la liste **Time Zone**, sélectionnez le fuseau horaire pour la valeur saisie dans la zone **Time**.    

5. Cliquez sur **Save**. La tâche est insérée dans le plan de déploiement.

## Création de tâches d'en-tête
{: #tasks_header}

Les tâches d'en-tête représentent des éléments organisationnels que vous pouvez ajouter à des plans de déploiement. Si vous créez un groupe de tâches, vous pouvez l'identifier à l'aide d'une tâche d'en-tête. Les tâches d'en-tête peuvent avoir des dépendances comme n'importe quelle autre tâche. 

<!-- When you import a deployment plan from IBM UrbanCode Release, segment tasks are bracketed by note-type Start Segment and End Segment tasks. Segment dependencies are represented by dependencies to End Segment tasks. -->

Pour créer une tâche d'en-tête, procédez comme suit :

1. Sur la page Deployment Plan Details, cliquez sur **Create Task**. Si vous voulez insérer une tâche à un endroit spécifique du plan, sélectionnez une tâche avant de cliquer sur **Create Task**. La nouvelle tâche est insérée au-dessus de la tâche sélectionnée.

1. Dans la fenêtre de création de tâche, dans la liste **Type**, sélectionnez **Header**.

1. Dans la zone **Name**, saisissez un nom pour la tâche. Le nom peut représenter un groupe de tâches. 

3. Dans la zone **Description**, saisissez ou collez une description. Vous pouvez entrer une remarque, un rappel ou d'autres instructions.

5. Cliquez sur **Save**. La tâche est insérée dans le plan de déploiement.

## Création de tâches Delivery Pipeline
{: #tasks_pipelineCD}

Dans le service {{site.data.keyword.contdelivery_short}}, {{site.data.keyword.deliverypipeline}} automatise vos flux de travaux DevOps. Vous pouvez gérer vos instances de {{site.data.keyword.deliverypipeline}} avec des tâches de pipeline.

Pour créer une tâche Delivery Pipeline, procédez comme suit :

1. Sur la page Deployment Plan Details, cliquez sur **Create Task**. Si vous voulez insérer une tâche à un endroit spécifique du plan, sélectionnez une tâche avant de cliquer sur **Create Task**. La nouvelle tâche est insérée au-dessus de la tâche sélectionnée.

1. Dans la fenêtre de création de tâche, dans la liste **Type**, sélectionnez **Continuous Delivery Pipeline**.

1. Dans la zone **Name**, saisissez un nom pour la tâche. Le nom peut représenter un groupe de tâches. 

3. Dans la zone **Description**, saisissez ou collez une description. Vous pouvez entrer une remarque, un rappel ou d'autres instructions.

3. Dans la zone **Pipeline ID**, saisissez ou collez l'ID pipeline.

3. Dans la zone **Stage Name**, saisissez ou collez le nom de l'étape.

5. Cliquez sur **Save**. La tâche est insérée dans le plan de déploiement.

## Gestion des groupes de tâches
{: #tasks_groups}

Vous pouvez combiner deux tâches au minimum dans un groupe de tâches. Lorsque vous créez un groupe, vous définissez le masque d'exécution du groupe, qui est séquentiel ou parallèle. Vous pouvez exécuter les tâches d'un groupe de masque parallèle dans n'importe quel ordre et exécuter des tâches simultanément, sauf s'il existe des dépendances. Les tâches figurant dans des groupes séquentiels sont traitées dans l'ordre de la liste, en commençant par la première ou celle située au niveau le plus élevé.

Vous pouvez imbriquer des groupes dans d'autres groupes. Vous pouvez imbriquer un groupe de masque séquentiel dans un groupe de masque parallèle, et inversement. Toutefois, vous ne pouvez pas imbriquer un groupe de masque séquentiel dans un autre groupe séquentiel, ni un groupe de masque parallèle dans un autre groupe parallèle.  

Pour créer un groupe de tâches, procédez comme suit :

1. Sur la page Deployment Plan Detail, sélectionnez au moins deux tâches.

1. Selon le type de groupe à créer, exécutez l'une des étapes suivantes :

  <ul>
  <li>Pour créer un groupe parallèle, cliquez sur l'icône **Parallèle** <img class="inline" src="../UCCR/images/para-icon.png"  alt="parallel group icon">. Si vous ne pouvez pas créer un groupe parallèle avec les tâches sélectionnées, l'icône est désactivée. Par exemple, il se peut que vous ne puissiez pas créer un
groupe parallèle si toutes les tâches sélectionnées se trouvent déjà dans un groupe parallèle.  </li>
  <li>Pour créer un groupe séquentiel, cliquez sur l'icône **Séquentiel** <img class="inline" src="../UCCR/images/seq-icon.png"  alt="sequential group icon">.
  </li>
  </ul>

Le groupe est correct et une barre de sélection de groupe est ajoutée au plan de déploiement. Si vous avez sélectionné des tâches non contiguës, les tâches forment une liste contiguë qui commence par la tâche sélectionnée au niveau le plus élevé. 

La figure ci-dessous montre un groupe parallèle. La barre de sélection de groupe identifie le type de groupe : parallèle <img class="inline" src="../UCCR/images/para-select.png"  alt="parallel group select"> ou séquentiel <img class="inline" src="../UCCR/images/seq-select.png"  alt="sequential group select">.

(![](../UCCR/images/group-select.png "Typical deployment plan"))

*Figure 2. Un groupe parallèle*

Pour déplacer un groupe, cliquez sur la **barre de sélection de groupe** ou n'importe où dans le groupe et faites-le glisser vers un nouvel emplacement.

Pour copier un groupe, sélectionnez-le, cliquez sur l'icône **Copier** <img class="inline" src="../UCCR/images/copy-group.png"  alt="copy icon">, placez le curseur à l'endroit où vous souhaitez insérer le groupe copié, puis cliquez sur l'icône **Coller** <img class="inline" src="../UCCR/images/paste-group.png"  alt="paste icon">.

Pour couper un groupe, sélectionnez-le et cliquez sur l'icône **Couper** <img class="inline" src="../UCCR/images/cut-group.png"  alt="cut icon">.

Pour dissocier un groupe, sélectionnez-le et cliquez sur l'icône **Dissocier** <img class="inline" src="../UCCR/images/ungroup-icon.png"  alt="ungroup icon"> sur la barre de sélection de groupe.

Pour supprimer les tâches qui font partie d'un groupe, sélectionnez le groupe et cliquez sur l'icône **Supprimer**  <img class="inline" src="../UCCR/images/trash-group.png"  alt="delete icon">. Les tâches sont supprimées du plan de déploiement.

## Gestion des étiquettes de tâche
{: #tasks_tags}

Les étiquettes sont des éléments organisationnels que vous pouvez ajouter à des tâches. Vous pouvez filtrer des plans de déploiement par étiquette. Par exemple, lors d'un déploiement dans un environnement de production, vous pouvez désactiver des tâches incluant l'étiquette `DEV_only`, qui indique que les tâches sont destinées uniquement à l'environnement de développement. 

Pour ajouter une étiquette à une tâche, procédez comme suit :

1. Sur la page Deployment Plan Details, sélectionnez une tâche ou un groupe de tâches, puis cliquez sur **Manage Tags**  <img class="inline" src="../UCCR/images/task-tag.png"  alt="manage tags">. Vous pouvez sélectionner plusieurs tâches et groupes.

1. Dans la fenêtre "Manage Tags for Selected Tasks", sélectionnez des étiquettes dans la liste **Common Tags**. Vous pouvez créer une étiquette en saisissant un nom dans la zone de texte de la liste.

1. Cliquez sur **Save**.

Les étiquettes s'affichent sur les lignes de tâche de la page Deployment Plan Details. Dans la figure suivante, la tâche de déploiement WAR a deux étiquettes : `Deployment` et `Critical`. 

Les étiquettes qui sont utilisées par un plan de déploiement s'affichent sur l'onglet **Versions** de la page Deployment Plan Details. Pour rendre une tâche inapplicable à un déploiement, effacez ses étiquettes. Les tâches avec le statut "Not Applicable" ne peuvent pas être démarrées.   

![](../UCCR/images/task-tag-labels.png "Typical deployment plan")

*Figure 3. Etiquettes de tâche*

## Création de dépendances de tâche
{: #tasks_dependencies}

Vous pouvez faire d'une tâche une condition préalable requise pour d'autres tâches. Dans ce cas, les tâches qui en dépendent ne peuvent pas démarrer, même si elles sont éligibles par ailleurs, tant que la tâche prérequise n'est pas résolue. 

Une tâche peut avoir plusieurs tâches dépendantes et plusieurs tâches prérequises. Vous pouvez définir des dépendances pour une tâche par rapport à une autre tâche dans le plan de déploiement. Cependant, vous ne pouvez pas créer de dépendances circulaires. Par exemple, vous ne pouvez pas rendre une tâche dépendante d'une tâche qui dépend elle-même de la première tâche.

En contrôlant les dépendances de tâche, vous pouvez vérifier que les événements se produisent dans l'ordre attendu. 

Pour qu'une tâche devienne un prérequis pour d'autres tâches, procédez comme suit :

1. Sur la page Deployment Plan Details, sélectionnez une tâche ou un groupe de tâches, puis cliquez sur **Manage Prerequisites** <img class="inline" src="../UCCR/images/task-depend.png"  alt="task prerequisite">. Vous pouvez sélectionner plusieurs tâches et groupes.

1. Dans la fenêtre "Manage Prerequisites for Selected Tasks", sélectionnez la tâche prérequise dans la liste **Prerequisite tasks for selected tasks**. 

1. Cliquez sur **Save**.

Les dépendances de tâche s'affichent dans la colonne Dependencies de la page Deployment Plan Detail. Les flèches vers le haut indiquent les prérequis pour les tâches, tandis que les flèches vers le bas indiquent les dépendances de tâche.

Dans la figure suivante, la première tâche ne contient pas de prérequis et deux tâches en dépendent. La seconde tâche contient une tâche prérequise et aucune tâche n'en dépend.

(![](../UCCR/images/plan-w-depend.png "Typical deployment plan"))

*Figure 4. Dépendances de tâche*

Pour consulter ou modifier des dépendances, sélectionnez la tâche et cliquez sur **Manage Prerequisites** <img class="inline" src="../UCCR/images/task-depend.png"  alt="task prerequisite">.
