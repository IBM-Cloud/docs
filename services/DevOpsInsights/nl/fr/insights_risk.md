---

copyright:
  years: 2016, 2017
lastupdated: "2017-03-31"

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}

# Deployment Risk
{: #gettingstarted}

{{site.data.keyword.DRA_short}} fournit un grand nombre d'informations sur vos déploiements, et en particulier sur les risques. Vous pouvez l'utiliser pour automatiser la protection de la qualité dans votre pipeline de distribution à l'aide de politiques et de jalons. 
{:shortdesc}

Après avoir ouvert {{site.data.keyword.DRA_short}} à partir de la chaîne d'outils, cliquez sur **Deployment Risk**. A partir de là, vous obtenez une présentation des applications de vos environnements de préproduction et de production, et vous pouvez effectuer une exploration en aval pour comprendre la couverture de code, les performances du test et les rapports de sécurité. Les tableaux de bord sont automatiquement remplis avec les informations les plus récentes provenant des tests {{site.data.keyword.DRA_short}} de vos pipelines.

## A propos de Deployment Risk
{: #about}

Vous pouvez utiliser Deployment Risk pour appliquer des normes de qualité dans votre chaîne d'outils grâce à des politiques et des jalons. Les politiques sont des ensembles de règles ; les jalons appliquent les politiques. Vous pouvez ainsi créer une politique "Test d'unité et couverture de test" qui exige des générations qu'elles répondent à des normes de test d'unité et de couverture de test. Vous pouvez ensuite ajouter un jalon qui se réfère à cette politique dans votre processus de distribution continue. Les générations qui ne satisfont pas la politique sont arrêtées au jalon. 

Deployment Risk fonctionne avec {{site.data.keyword.deliverypipeline}}, qui fait partie d'{{site.data.keyword.contdelivery_full}}, et avec les projets Jenkins. A un niveau élevé, les instructions d'utilisation de l'un ou de l'autre sont similaires.  

Si vous utilisez {{site.data.keyword.deliverypipeline}}, suivez les étapes ci-après :

1. [Créez des politiques et des règles](#policies_and_rules) qui seront gérées par {{site.data.keyword.DRA_short}}.
2. [Préparez les étapes de votre pipeline](#integrate_pipeline) en vue de l'intégration avec {{site.data.keyword.DRA_short}}.

3. [Créez ou éditez des travaux de test](#configure_pipeline_jobs) dans le pipeline qui téléchargent les résultats vers {{site.data.keyword.DRA_short}}.
4. [Ajoutez des jalons](#configure_pipeline_gates) au pipeline qui prend les décisions de promotion en fonction de ces résultats et de vos politiques.
5. Exécutez le pipeline et [affichez les résultats](#view_results).

Si vous utilisez Jenkins, procédez comme suit :

1. [Créez des politiques et des règles](#policies_and_rules) qui seront gérées par {{site.data.keyword.DRA_short}}.
2. [Installez et configurez le plug-in Jenkins](#integrate_jenkins).
3. [Créez les travaux de test et les jalons comme décrit dans les instructions du plug-in](#integrate_jenkins). Les tests téléchargent les résultats vers {{site.data.keyword.DRA_short}} en vue de l'analyse et les jalons utilisent ces résultats pour prendre les décisions quant aux promotions.
4. Exécutez le projet et [affichez les résultats](#view_results). 

Peu importe la manière dont vous générez et déployez votre code, les résultats sont identiques : les générations qui satisfont les normes passent les jalons Deployment Risk et les générations qui ne répondent pas aux normes sont arrêtées. 

## Prérequis
{: #prerequisites}

Deployment Risk requiert une configuration plus poussée que la configuration décrite dans [Initiation à {{site.data.keyword.DRA_short}}](/docs/services/DevOpsInsights/index.html).

Pour utiliser Deployment Risk, vous avez besoin de deux éléments :

* Une instance de {{site.data.keyword.deliverypipeline}} ou un projet Jenkins
* Les tests que vous souhaitez utiliser pour évaluer votre projet

## Création de politiques et de règles
{: #policies_and_rules}

Les politiques sont des ensembles de règles qui contrôlent les jalons de votre pipeline de distribution. Si votre code ne satisfait pas, dans un sens ou dans l'autre, une politique appliquée à un jalon particulier, le déploiement est arrêté dans le but d'empêcher la publication de changements risqués.

Vous définissez les politiques dans {{site.data.keyword.DRA_short}}. Les politiques sont créées dans l'organisation {{site.data.keyword.Bluemix_notm}} qui contient {{site.data.keyword.DRA_short}}. Toutes les applications qui se trouvent dans la même organisation peuvent utiliser la politique. 

### Création de politiques
{: #create_policies}

Pour créer une politique :

1. Dans la navigation de gauche, cliquez sur **Paramètres**.

2. Cliquez sur **Politiques**.

3. Cliquez sur **Créer une politique**, puis indiquez un nom et une description pour la nouvelle politique.

4. Cliquez sur **Suivant**.

4. Ajoutez au moins une règle à la politique :
  1. Cliquez sur **Ajouter une règle à la politique**.
  2. Sélectionnez le type de règle.
  3. Entrez les détails et les conditions de la règle.
  4. Cliquez sur **Sauvegarder**.

5. Lorsque vous avez terminé l'ajout de règles à la politique, cliquez sur **Terminer**.

### Création de règles
{: #creating_rules}

Les règles définissent les critères utilisés par vos politiques pour juger du succès ou de l'échec. Vous pouvez créer une politique "Test d'unité et couverture de test" qui contient une règle de test d'unité qui requiert 80 % de réussite au test d'unité et une règle de couverture de test qui requiert 100 % de couverture du code. Si vous ajoutez un jalon qui se réfère à cette règle dans un pipeline, le jalon empêche les générations qui ne satisfont pas les deux règles. 

Vous pouvez exiger la réussite inconditionnelle en marquant les tests comme critiques. Pour créer une règle, sélectionnez une politique, puis cliquez sur **Ajouter une règle à la politique**. 

#### Création de règles de test de vérification fonctionnelle
{: #criteria_fvt}

1. Entrez une description et sélectionnez un format.

2. Indiquez le pourcentage de scénarios de test à réussir pour que la vérification aboutisse.

3. Définissez les scénarios de test critiques.

4. Pour surveiller les régressions de scénario de test, cochez la case **Contrôle pour la régression de scénario de test**.

5. Cliquez sur **Sauvegarder**.


#### Création de règles de test d'unité
{: #criteria_ut}

1. Entrez une description et sélectionnez un format.

2. Indiquez le pourcentage de scénarios de test à réussir pour que la vérification aboutisse.

3. Définissez les scénarios de test critiques.

4. Pour surveiller les régressions de scénario de test, cochez la case **Contrôle pour la régression de scénario de test**.

5. Cliquez sur **Sauvegarder**.


#### Création de règles de couverture de code
{: #criteria_codecoverage}

1. Entrez une description et sélectionnez un format.

2. Indiquez le pourcentage de couverture de code nécessaire pour que la vérification aboutisse.

3. Pour surveiller les régressions de couverture de code, cochez la case **Contrôle pour la régression de scénario de test**.

4. Cliquez sur **Sauvegarder**.

#### Création de règles d'examen de sécurité statique
{: #criteria_static}

Vous pouvez intégrer {{site.data.keyword.DRA_short}} à IBM Application Security on Cloud pour exécuter des examens de code statique et d'application dynamique. Pour plus d'informations sur Application Security on Cloud,voir la [documentation officielle](/docs/services/ApplicationSecurityonCloud/index.html).

1. Entrez une description.

2. Indiquez le nombre maximal de problèmes de gravité élevée, moyenne et faible autorisés par la règle. 

3. Cliquez sur **Sauvegarder**.

#### Création de règles d'examen de sécurité dynamique
{: #criteria_dynamic}

Vous pouvez intégrer {{site.data.keyword.DRA_short}} à {{site.data.keyword.appseccloudfull}} pour exécuter des examens d'application dynamiques. Pour plus d'informations sur Application Security on Cloud,voir la [documentation officielle](/docs/services/ApplicationSecurityonCloud/index.html).

1. Entrez une description.

2. Indiquez le nombre maximal de problèmes de gravité élevée, moyenne et faible autorisés par la règle. 

3. Cliquez sur **Sauvegarder**.

## Configuration de {{site.data.keyword.deliverypipeline}} 
{: #configuration}

Après avoir ajouté {{site.data.keyword.DRA_short}} à une chaîne d'outils et avoir défini les politiques qu'il surveille, intégrez-le à {{site.data.keyword.deliverypipeline}}. Pour plus d'informations sur les pipelines, voir [la documentation officielle](/docs/services/ContinuousDelivery/pipeline_working.html).

### Préparation des étapes du pipeline
{: #integrate_pipeline}

Pour que Deployment Risk analyse votre projet, vous devez définir des étapes de préproduction et de production dans votre pipeline. Pour définir ces étapes, vous utilisez des propriétés d'environnement texte que vous trouvez dans le menu de configuration de chaque étape ![icône de configuration d'étape de pipeline](images/pipeline-stage-configuration-icon.png) sous **Propriétés d'environnement**.

1. A l'étape de préproduction, définissez la propriété `LOGICAL_ENV_NAME` sur `STAGING`. 

2. A l'étape de production, définissez la propriété `LOGICAL_ENV_NAME` sur `PRODUCTION`. 

Vous pouvez également ajouter les propriétés suivantes aux étapes qui génèrent ou déploient votre application :

* `LOGICAL_APP_NAME`, qui définit le nom de l'application sur le tableau de bord.
* `BUILD_PREFIX`, qui définit le texte ajouté en préfixe aux générations de l'étape. Ce texte s'affiche également sur le tableau de bord. 

### Ajout de travaux de test
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

### Définition de jalons
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

Une fois que vous avez configuré le pipeline, commencez à utiliser {{site.data.keyword.DRA_short}}. Pour obtenir les instructions correspondantes, voir [Affichage de tableaux de bord et de rapports](/docs/services/DevOpsInsights/pipeline_decision_reports.html#toolchain_reports).

## Configuration d'un projet Jenkins
{: #integrate_jenkins}

Après avoir ajouté {{site.data.keyword.DRA_full}} à une chaîne d'outils ouverte et défini les politiques qu'il surveille, vous pouvez l'intégrer à votre projet Jenkins. 

Le plug-in IBM Cloud DevOps pour Jenkins intègre des projets Jenkins à des chaînes d'outils. Une *chaîne d'outils* est un ensemble d'intégrations d'outils prenant en charge des tâches de développement, de déploiement et d'opérations. La puissance collective d'une chaîne d'outils est supérieure à la somme de ses intégrations d'outils individuelles. Les chaînes d'outils ouvertes font partie du service {{site.data.keyword.contdelivery_full}}. Pour en savoir plus sur le service {{site.data.keyword.contdelivery_short}}, voir [la documentation associée](https://console.ng.bluemix.net/docs/services/ContinuousDelivery/cd_about.html).

Après avoir installé le plug-in IBM Cloud DevOps, vous pouvez publier les résultats de test dans {{site.data.keyword.DRA_short}}, ajouter des jalons de qualité automatisés et effectuer le suivi des risques de déploiement. Vous pouvez également envoyer des notifications de travail à d'autres outils de la chaîne d'outils, tels que Slack et PagerDuty. Afin de faciliter le suivi des déploiements, la chaîne d'outils peut ajouter des messages de déploiement aux validations Git, ainsi qu'aux problèmes Git ou JIRA associés. Vous pouvez également afficher vos déploiements sur la page Connexions de votre chaîne d'outils. 

Le plug-in fournit des actions et des interfaces de ligne de commande post-génération pour la prise en charge de l'intégration. {{site.data.keyword.DRA_short}} agrège et analyse les résultats des tests d'unité, des tests fonctionnels, des outils de couvertures de code, des examens du code de sécurité statique et des examens du code de sécurité dynamique afin de déterminer si votre code répond aux politiques prédéfinies aux jalons de votre processus de déploiement. Si votre code ne satisfait pas ou dépasse une politique, le déploiement est interrompu afin de prévenir toute modification à risque. Vous pouvez utiliser {{site.data.keyword.DRA_short}} comme filet de sécurité pour votre environnement de distribution continue en vue d'implémenter et d'améliorer les normes qualité au fil du temps, ainsi que comme outil de visualisation de données pour vous aider à comprendre la santé de votre projet.

### Prérequis
{: #jenkins_prerequisites}

Vous devez avoir accès à un serveur qui exécute un projet Jenkins.

### Création d'une chaîne d'outils
{: #jenkins_create}

Avant de pouvoir intégrer {{site.data.keyword.DRA_short}} à un projet Jenkins, vous devez créer une chaîne d'outils. 

1. Pour créer une chaîne d'outils, accédez à la [page Créer une chaîne d'outils](https://console.ng.bluemix.net/devops/create) et suivez les instructions. 

2. Après avoir créé la chaîne d'outils, ajoutez-y{{site.data.keyword.DRA_short}}. Pour plus d'instructions, voir la [documentation {{site.data.keyword.DRA_short}}](https://console.ng.bluemix.net/docs/services/DevOpsInsights/index.html). 

### Installation du plug-in
{: #jenkins_install}

Téléchargez d'abord le plug-in à partir de {{site.data.keyword.DRA_short}}.  

1. Sur la page de présentation de la chaîne d'outils, cliquez sur **DevOps Insights**.
2. Cliquez sur **Settings**, puis sur **Jenkins Plugin Setup**.
3. Suivez les instructions de la page pour télécharger le plug-in.

Ensuite, sur votre serveur Jenkins, installez le plug-in.

1. Cliquez sur **Manage Jenkins &gt; Manage Plugins**, puis sélectionnez l'onglet **Advanced**.
2. Cliquez sur **Choose File** et sélectionnez le fichier d'installation du plug-in IBM Cloud DevOps. 
3. Cliquez sur **Upload**.
4. Redémarrez Jenkins et vérifiez que le plug-in a été installé.

### Configuration des travaux Jenkins pour les tableaux de bord Deployment Risk
{: #jenkins_configure}

Une fois le plug-in installé, vous pouvez intégrer {{site.data.keyword.DRA_short}} dans votre projet Jenkins. 

Suivez la procédure ci-après pour utiliser les jalons et le tableau de bord de Deployment Risk avec votre projet.

1. Ouvrez la configuration de n'importe quel travail dont vous disposez, comme une génération, un test ou un déploiement.

2. Ajoutez une action post-génération pour le type correspondant :

   * Pour les travaux de génération, utilisez **Publish build information to IBM Cloud DevOps**.
   
   * Pour les travaux de test, utilisez **Publish test result to IBM Cloud DevOps**.
   
   * Pour les travaux de déploiement, utilisez **Publish deployment information to IBM Cloud DevOps**.
   
3. Renseignez les zones requises. Elles varient selon le type de travail. 

   * Dans la liste **Credentials**, sélectionnez votre ID et votre mot de passe {{site.data.keyword.Bluemix_notm}}. S'ils ne sont pas sauvegardés dans Jenkins, cliquez sur **Add** pour les sauvegarder. Testez votre connexion à {{site.data.keyword.Bluemix_notm}} en cliquant sur **Test Connection**.
   
   * Dans la zone **Build Job Name**, indiquez le nom de votre travail de génération exactement tel qu'il apparaît dans Jenkins. Si la génération s'effectue en même temps que le travail de test, laissez cette zone vide. Si le travail de génération s'effectue hors de Jenkins, cochez la case **Builds are being done outside of Jenkins**, puis indiquez le numéro de version et l'URL de génération.
   
   * Pour l'environnement, si les tests sont exécutés lors de l'étape de génération, ne sélectionnez que l'environnement de génération. Si les tests sont exécutés à l'étape de déploiement, sélectionnez l'environnement de déploiement et indiquez le nom de l'environnement. Deux valeurs sont prises en charge : `STAGING` et `PRODUCTION`.
   
   * Pour la zone **Result File Location**, indiquez l'emplacement du fichier de résultats. Si le test ne génère aucun fichier de résultats, laissez cette zone vide. Le plug-in télécharge un fichier de résultats par défaut en fonction du statut du travail de test en cours.

   Les images suivantes représentent des exemples de configuration :
   
   ![Téléchargement des informations de génération](images/Upload-Build-Info.png "Publication des informations de génération dans DRA") *Publication des informations de génération*
   
   ![Téléchargement des résultats de test](images/Upload-Test-Result.png "Publication des résultats de test dans DRA") *Publication des résultats de test*
   
   ![Téléchargement des informations de déploiement](images/Upload-Deployment-Info.png "Publication des informations de déploiement dans DRA") *Publication des informations de déploiement*

4. Si vous voulez utiliser des jalons de politique {{site.data.keyword.DRA_short}} pour contrôler un travail de déploiement en aval, ajoutez une action post-génération **IBM Cloud DevOps Gate**. Choisissez une politique et indiquez la portée des résultats de test. Pour autoriser les jalons de politique à empêcher les déploiements en aval, cochez la case **Fail the build based on the policy rules**. L'image suivante représente un exemple de configuration :

    ![Jalon DevOps Insights](images/DRA-Gate.png "Jalon DevOps Insights")

5. Exécutez votre travail de génération Jenkins.

6. Affichez le tableau de bord Deployment Risk en accédant à [IBM Bluemix DevOps](https://console.ng.bluemix.net/devops), en sélectionnant votre chaîne d'outils et en cliquant sur **DevOps Insights**.

Le tableau de bord Deployment Risk repose sur la présence d'un jalon après un travail de déploiement de préproduction. Si vous voulez utiliser le tableau de bord, vérifiez qu'il existe un jalon après le déploiement vers l'environnement de préproduction, mais avant le déploiement vers un environnement de production.
    
### Configuration des notifications
{: #jenkins_notifications}

Vous pouvez configurer vos travaux Jenkins pour qu'ils envoient les notifications à des outils tels que Slack ou PagerDuty en suivant les instructions de la [documentation Bluemix](https://console.ng.bluemix.net/docs/services/ContinuousDelivery/toolchains_integrations.html#jenkins).

Cet exemple montre comment configurer `ICD_WEBHOOK_URL` pour les configurations de travail : ![Définition du paramètre ICD_WEBHOOK_URL](images/Set-Parameterized-Webhook.png "Définition d'un webhook paramétré")

Cet exemple montre comment configurer des actions post-génération pour les notifications des travaux : ![Actions post-génération pour une notification webhook](images/PostBuild-WebHookNotification.png "Configuration d'une notification webhook dans des actions post-génération")

## Affichage des résultats
{: #view_results}

Après l'exécution d'un pipeline, {{site.data.keyword.DRA_short}} commence à collecter et à analyser les résultats de test correspondants pour établir une base de référence. Les données de chaque exécution ultérieure sont collectées et comparées aux résultats précédents. Des jalons de décision utilisent ces données pour déterminer le moment auquel un déploiement doit être arrêté. 

Le tableau de bord Deployment Risk vous permet d'afficher vos données de déploiement et d'évaluation au jalon. Pour ouvrir le tableau de bord, ouvrez {{site.data.keyword.DRA_short}}, puis, dans le menu latéral, cliquez sur **Deployment Risk**.

Si vous utilisez un pipeline {{site.data.keyword.contdelivery_short}}, vous pouvez afficher des rapports d'exécution de jalon individuels à partir du pipeline lui-même. Pour afficher le rapport de décision d'un jalon à partir du pipeline :

1. A l'étape qui contient le jalon à vérifier, cliquez sur **Afficher les journaux et l'historique**.

2. Dans le travail qui contient le jalon, cliquez sur le nom du jalon.

3. Dans la vue du journal, recherchez le message `Check {{site.data.keyword.DRA_short}} report here` et cliquez sur le lien pour ouvrir le rapport.






