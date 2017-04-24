---

copyright:
  years: 2015, 2017
lastupdated: "2017-3-31"

---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}

# Initiation à Continuous Delivery
{: #cd_getting_started}

Adoptez une approche DevOps en utilisant {{site.data.keyword.contdelivery_full}}, qui inclut une chaîne d'outils ouverte automatisant la génération et le déploiement d'applications. Vous
pouvez commencer en créant une chaîne d'outils de déploiement simple qui prend en charge les tâches de développement, de déploiement et les opérations.
{: shortdesc}

Après avoir créé une instance de {{site.data.keyword.contdelivery_short}} en la sélectionnant dans le catalogue {{site.data.keyword.Bluemix_notm}}, vous pouvez choisir la manière dont vous souhaitez démarrer avec le service.
 ![Page d'accueil de Continuous Delivery](images/cd_landing_page.png)

 * Pour commencer rapidement et déployer votre application à l'aide d'un pipeline automatisé, dans la section
"Démarrage avec un pipeline", cliquez sur **[Commencer ici](#starting_with_a_pipeline)**. Vous pourrez ajouter d'autres outils ultérieurement.
 * Pour créer et configurer une chaîne d'outils de distribution continue depuis un modèle, dans la section "Démarrage depuis un modèle de chaîne d'outils", cliquez sur **[Commencer ici](#starting_from_a_toolchain_template)**. La chaîne d'outils intègre des outils destinés à la planification, au développement, au déploiement de pipelines et à la gestion de vos applications. Vous pouvez toujours ajouter ou retirer des outils dans vos chaînes d'outils.
 * Si vous disposez déjà de chaînes d'outils, dans la section "Démarrage depuis un modèle de chaîne d'outils", cliquez sur **Afficher vos chaînes
d'outils**. Pour plus d'informations sur l'utilisation des chaînes d'outils, voir [Utilisation de chaînes d'outils](/docs/services/ContinuousDelivery/toolchains_using.html){: new_window}.

**Astuce** : Les pipelines sont gérés par des chaînes d'outils. Vous pouvez ajouter un pipeline à une chaîne d'outils existante. Si vous créez un pipeline et qu'il n'existe pas de chaînes d'outils, une chaîne d'outils avec un nom par défaut est automatiquement créée. Grâce à la chaîne d'outils, vous pouvez développer les capacités de votre pipeline par une intégration avec d'autres outils et services. 

##Démarrage avec un pipeline
{: #starting_with_a_pipeline}

Les pipelines automatisent les générations, les déploiements, etc. Pour commencer avec un pipeline automatisé, sélectionnez un modèle et indiquez l'emplacement de votre référentiel GitHub. 

Pour [créer un pipeline ![Icône de lien externe](../../icons/launch-glyph.svg "External link icon")](https://console.ng.bluemix.net/devops/pipelines/dashboard/create){:new_window} configuré pour déployer une application Cloud Foundry, procédez comme suit : 

1. Cliquez sur **Cloud Foundry**.
1. Si vous désirez utiliser un nom différent pour le pipeline, modifiez son nom par défaut. Le nom du pipeline l'identifie dans {{site.data.keyword.Bluemix_notm}}.
1. Si vous désirez utiliser un nom différent pour l'application, modifiez son nom par défaut. Le nom de l'application l'identifie dans {{site.data.keyword.Bluemix_notm}}. Ce nom est celui de l'application où est déployé le pipeline.
1. Si vous n'avez pas de chaînes d'outils, une chaîne d'outils portant le nom par défaut est créée pour vous. Si vous désirez utiliser un autre nom pour la chaîne d'outils, modifiez son nom. Les pipelines sont gérés par des chaînes d'outils. Grâce à la chaîne d'outils, vous pouvez étendre les capacités de votre pipeline par une intégration avec d'autres outils et services.

 **Conseil **: les pipelines et les chaînes d'outils appartiennent à des organisations (orgs). Si vous appartenez à une organisation disposant de chaînes d'outils, vous pouvez utiliser ces chaînes d'outils même si vous ne les avez pas créées.

1. Sélectionnez la chaîne d'outils que vous désirez utiliser ou entrez le nom de la nouvelle chaîne d'outils à créer.
1. Sélectionnez votre fournisseur Git.

 **Conseil **: Si vous n'avez pas autorisé {{site.data.keyword.Bluemix_notm}} à accéder à GitHub, vous êtes invité à cliquer sur **Autoriser** pour accéder au site Web GitHub. Si vous n'avez pas de session GitHub active, vous êtes invité à vous connecter. Cliquez sur **Authorize Application** pour autoriser {{site.data.keyword.Bluemix_notm}} à accéder à votre compte GitHub. Si vous disposez d'une session GitHub active mais n'avez pas saisi votre mot de passe récemment, vous êtes invité à entrer votre mot de passe GitHub pour confirmation.

 Si vous n'êtes pas autorisé à accéder au référentiel {{site.data.keyword.ghe_short}}, une personne disposant de droits d'administrateur pour le référentiel doit vous ajouter. Pour obtenir des instructions sur une autorisation avec {{site.data.keyword.Bluemix_notm}} Dédié pour {{site.data.keyword.ghe_short}}, voir [Initiation à {{site.data.keyword.Bluemix_notm}} Dédié pour {{site.data.keyword.ghe_short}}](/docs/services/ghededicated/index.html){: new_window}. Si vous devez accorder l'autorisation avec votre propre version gérée de {{site.data.keyword.ghe_short}}, suivez vos procédures internes. 

   * Si vous disposez d'un référentiel et désirez l'utiliser, sélectionnez **Lien** pour le type de référentiel. Recherchez l'emplacement du référentiel ou sélectionnez le référentiel dans la liste des référentiels disponibles.

   * Si vous désirez créer un référentiel vide, sélectionnez **Nouveau** pour le type de référentiel. Entrez un nom pour le référentiel.

   * Si vous désirez créer un clone d'un référentiel, sélectionnez **Copie** pour le type de référentiel. Recherchez l'emplacement du référentiel ou sélectionnez le référentiel dans la liste des référentiels disponibles.

   * Si vous désirez dévier un référentiel pour pouvoir contribuer à des modifications via des demandes d'extraction, sélectionnez **Déviation**. Recherchez l'emplacement du référentiel ou sélectionnez le référentiel dans la liste des référentiels disponibles.

1. Sélectionnez un référentiel ou entrez une URL de référentiel.
1. Cliquez sur **Créer**. Le pipeline est créé, configuré et affiché sur la page Présentation de la chaîne d'outils.
 ![Carte du pipeline](images/cd_pipeline.png)

Pour créer un [pipeline vide ![Icône de lien externe](../../icons/launch-glyph.svg "External link icon")](https://console.ng.bluemix.net/devops/pipelines/dashboard/create){: new_window} sans étapes préconfigurées :

1. Cliquez sur **Personnalisé**.
1. Si vous désirez utiliser un nom différent pour le pipeline, modifiez son nom par défaut. Le nom du pipeline l'identifie dans {{site.data.keyword.Bluemix_notm}}.
1. Si vous n'avez pas de chaînes d'outils, une chaîne d'outils portant le nom par défaut est créée pour vous. Si vous désirez utiliser un autre nom pour la chaîne d'outils, modifiez son nom. Les pipelines sont gérés par des chaînes d'outils. Grâce à la chaîne d'outils, vous pouvez étendre les capacités de votre pipeline par une intégration avec d'autres outils et services.
1. Sélectionnez la chaîne d'outils que vous désirez utiliser ou entrez le nom de la nouvelle chaîne d'outils à créer.
1. Cliquez sur **Créer**. Un pipeline vide est créé et représenté sous forme de carte sur la page Présentation de la chaîne d'outils.

##Démarrage depuis un modèle de chaîne d'outils
{: #starting_from_a_toolchain_template}

Pour créer et configurer une chaîne d'outils de distribution continue depuis un [modèle ![Icône de lien externe](../../icons/launch-glyph.svg "External link icon")](https://console.ng.bluemix.net/devops/create){: new_window} :

1. Sur la page **Créer une chaîne d'outils**, cliquez sur un modèle de chaîne d'outils.  
1. Examinez le diagramme de la chaîne d'outils que vous être sur le point de créer. Ce diagramme montre chaque intégration d'outils dans sa phase de cycle de vie au sein de la chaîne d'outils.

 **Astuce** : Quelques modèles de chaîne d'outils possèdent plusieurs instances d'intégration d'outils. Par exemple, le modèle de chaîne d'outils Microservices sur {{site.data.keyword.Bluemix_notm}} Public contient trois instances de GitHub et trois instances de Delivery Pipeline, une pour chacun des trois microservices.

 L'image suivante fournit un exemple de diagramme. Lorsque vous créez une chaîne d'outils, le diagramme représente chaque intégration d'outils faisant partie de la chaîne d'outils.
 ![Diagramme de chaîne d'outils](images/toolchain_diagram.png)
1. Passez en revue les informations par défaut des paramètres de chaîne d'outils. Le nom de la chaîne d'outils l'identifie dans {{site.data.keyword.Bluemix_notm}}. Si vous désirez utiliser un nom différent, modifiez le nom de la chaîne d'outils.
1. Dans la section Intégrations d'outils, sélectionnez chaque intégration d'outils à configurer pour votre chaîne d'outils. Quelques intégrations d'outils ne nécessitent pas de configuration. Pour des informations sur la configuration des intégrations d'outils, voir [Configuration d'intégrations d'outils](/docs/services/ContinuousDelivery/toolchains_integrations.html){: new_window}.
1. Cliquez sur **Créer**. Plusieurs étapes s'exécutent automatiquement pour configurer votre chaîne d'outils. Les intégrations d'outils configurées varient en fonction du modèle de chaîne d'outils que vous avez sélectionné et selon que vous utilisez {{site.data.keyword.Bluemix_notm}} Public ou {{site.data.keyword.Bluemix_notm}} Dédié. Par exemple, lorsque vous créez une chaîne d'outils Microservices sur {{site.data.keyword.Bluemix_notm}} Public, les étapes suivantes sont exécutées : 

 * La chaîne d'outils est créée.
 * Si vous avez configuré Delivery Pipeline, les pipelines sont créés et exécutés. 
 * Si vous avez configuré Sauce Labs, la chaîne d'outils est configurée pour ajouter des travaux de test Sauce Labs aux pipelines.
 * Si vous avez configuré PagerDuty, la chaîne d'outils est configurée pour envoyer des notifications d'alerte au service PagerDuty que vous avez indiqué.
 * Si vous avez configuré Slack, la chaîne d'outils est configurée pour envoyer au canal Slack que vous avez spécifié des notifications sur le statut de déploiement.
 * Si vous avez configuré une intégration d'outils de code source, comme GitHub, le référentiel exemple GitHub est cloné dans votre compte GitHub.
