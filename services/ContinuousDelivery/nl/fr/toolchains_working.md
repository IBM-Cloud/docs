---

copyright:
  years: 2015, 2017
lastupdated: "2017-4-7"

---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}

# Création de chaînes d'outils
{: #toolchains_getting_started}

Une *chaîne d'outils* est un ensemble d'intégrations d'outils prenant en charge des tâches de développement, de déploiement et d'opérations. La puissance collective d'une chaîne d'outils est supérieure à la somme de ses intégrations d'outils individuelles.
{: shortdesc}

Des chaînes d'outils ouvertes sont disponibles dans les environnements {{site.data.keyword.Bluemix}} Public et Dédié. Vous pouvez créer une chaîne d'outils de deux façons : à l'aide d'un modèle ou à partir d'une application. Sur {{site.data.keyword.Bluemix_notm}} public, les chaînes d'outils sont disponibles uniquement dans la région sud des Etats-Unis.

Chaque chaîne d'outils est associée à une organisation (org) spécifique, et tout membre de cette organisation peut être ajouté à la liste de contrôle d'accès de l'une de ses chaînes d'outils associées. Pour plus d'informations sur le contrôle d'accès pour les chaînes d'outils,  voir [Gestion de l'accès](/docs/services/ContinuousDelivery/toolchains_using.html#managing_access){: new_window}.Avant de créer une chaîne d'outils, assurez-vous de travailler dans l'organisation dans laquelle vous voulez créer la chaîne d'outils. L'organisation au sein de laquelle vous travaillez s'affiche dans la barre de menus. Pour passer à une autre organisation, cliquez sur l'organisation dans la barre de menus, puis sélectionnez l'organisation souhaitée.


##Création d'une chaîne d'outils à partir d'un modèle   
{: #creating_a_toolchain_from_a_template}

Vous pouvez utiliser un modèle comme point de départ pour [créer une chaîne d'outils![Icône de lien externe](../../icons/launch-glyph.svg "External link icon")](https://console.ng.bluemix.net/devops/create){: new_window} incluant un ensemble spécifique d'intégrations d'outils. Pour en savoir plus sur l'utilisation des modèles, consultez [IBM Cloud Garage Method ![Icône de lien externe](../../icons/launch-glyph.svg "External link icon")](https://www.ibm.com/devops/method/category/tools){:new_window}.

1. Si vous utilisez {{site.data.keyword.Bluemix_notm}} Public, connectez-vous à [{{site.data.keyword.Bluemix_notm}} ![Icône de lien externe](../../icons/launch-glyph.svg "External link icon")](http://console.ng.bluemix.net){:new_window}.
1. Si vous utilisez {{site.data.keyword.Bluemix_notm}} Dédié, connectez-vous à votre environnement Dédié sur {{site.data.keyword.Bluemix_notm}}.
1. Depuis le menu en hamburger, cliquez sur **Services**, puis sur **DevOps**.
1. Dans le tableau de bord DevOps, sur la page **Chaînes d'outils**, cliquez sur **Créer une chaîne d'outils**.
1. Sur la page **Créer une chaîne d'outils**, cliquez sur un modèle de chaîne d'outils.
1. Examinez le diagramme de la chaîne d'outils que vous être sur le point de créer. Ce diagramme montre chaque intégration d'outils dans sa phase de cycle de vie au sein de la chaîne d'outils.

 **Astuce** : Quelques modèles de chaîne d'outils possèdent plusieurs instances d'intégration d'outils. Par exemple, le modèle de chaîne d'outils Microservices sur {{site.data.keyword.Bluemix_notm}} Public contient trois instances de GitHub et trois instances de Delivery Pipeline, une pour chacun des trois microservices.

 L'image suivante fournit un exemple de diagramme. Lorsque vous créez une chaîne d'outils, le diagramme représente chaque intégration d'outils faisant partie de la chaîne d'outils.
![Diagramme de chaîne d'outils](images/toolchain_diagram.png)

1. Passez en revue les informations par défaut des paramètres de chaîne d'outils. Le nom de la chaîne d'outils l'identifie dans {{site.data.keyword.Bluemix_notm}}. Si vous désirez utiliser un nom différent, modifiez le nom de la chaîne d'outils.  
1. Dans la section Intégrations d'outils, sélectionnez chaque intégration d'outils à configurer pour votre chaîne d'outils. Quelques intégrations d'outils ne nécessitent pas de configuration. Pour des informations sur la configuration des intégrations d'outils, voir [Configuration d'intégrations d'outils](/docs/services/ContinuousDelivery/toolchains_integrations.html){: new_window}.
1. Cliquez sur **Créer**. Plusieurs étapes s'exécutent automatiquement pour configurer votre chaîne d'outils. Les intégrations d'outils configurées varient en fonction du modèle de chaîne d'outils que vous avez sélectionné et selon que vous utilisez {{site.data.keyword.Bluemix_notm}} Public ou {{site.data.keyword.Bluemix_notm}} Dédié. Par exemple, lorsque vous créez une chaîne d'outils Microservices sur {{site.data.keyword.Bluemix_notm}} Public, les étapes suivantes sont exécutées : 

 * La chaîne d'outils est créée.
 * Si vous avez configuré Delivery Pipeline, les pipelines sont créés et déclenchés. 
 * Si vous avez configuré Sauce Labs, la chaîne d'outils est configurée pour ajouter des travaux de test Sauce Labs aux pipelines.
 * Si vous avez configuré PagerDuty, la chaîne d'outils est configurée pour envoyer des notifications d'alerte au service PagerDuty que vous avez indiqué.
 * Si vous avez configuré Slack, la chaîne d'outils est configurée pour envoyer au canal Slack que vous avez spécifié des notifications sur le statut de déploiement.
 * Si vous avez configuré une intégration d'outils de code source, comme GitHub, le référentiel exemple GitHub est cloné dans votre compte GitHub.


##Création d'une chaîne d'outils à partir d'une application
{: #creating_a_toolchain_from_an_app}

Vous pouvez créer une chaîne d'outils à partir de votre application. La chaîne d'outils peut prendre en charge le développement, le déploiement, la surveillance, etc. en continu, et elle est associée à votre application. Chaque application peut être associée à une chaîne d'outils. Lorsque vous envoyez des modifications au référentiel GitHub ou {{site.data.keyword.ghe_short}} de la chaîne d'outils, le pipeline génère et déploie automatiquement l'application.  

1. Depuis la page de présentation de votre application, sur la carte Distribution continue, cliquez sur **Activer**. Si vous utilisez {{site.data.keyword.Bluemix_notm}} Public, votre application est configurée pour la distribution continue depuis un nouveau référentiel GitHub rempli avec le code de démarrage d'application. Si vous utilisez {{site.data.keyword.Bluemix_notm}} Dédié, votre application est configurée pour la distribution continue depuis un nouveau référentiel GitHub ou {{site.data.keyword.ghe_short}} rempli avec le code de démarrage d'application. 
1. Sur la page de création de chaîne d'outils, passez en revue le diagramme de la chaîne d'outils que vous allez créer. Ce diagramme montre chaque intégration d'outils dans sa phase de cycle de vie au sein de la chaîne d'outils.
1. Passez en revue les informations par défaut des paramètres de chaîne d'outils. Le nom de la chaîne d'outils l'identifie dans {{site.data.keyword.Bluemix_notm}}. Si vous désirez utiliser un nom différent, modifiez le nom de la chaîne d'outils.
1. Dans la section Intégrations d'outils, sélectionnez chaque intégration d'outils à configurer pour votre chaîne d'outils. Quelques intégrations d'outils ne nécessitent pas de configuration. Pour des informations sur la configuration des intégrations d'outils, voir [Configuration d'intégrations d'outils](/docs/services/ContinuousDelivery/toolchains_integrations.html){: new_window}.
1. Cliquez sur **Créer**.  Plusieurs étapes s'exécutent automatiquement pour configurer votre chaîne d'outils. Les intégrations d'outils configurées varient selon que vous utilisez des chaînes d'outils sur {{site.data.keyword.Bluemix_notm}} Public ou {{site.data.keyword.Bluemix_notm}} Dédié. Par exemple, lorsque vous créez une chaîne d'outils à partir d'une application sur {{site.data.keyword.Bluemix_notm}} Public, les étapes suivantes sont exécutées : 

 * La chaîne d'outils est créée.
 * Si vous avez configuré Delivery Pipeline, les pipelines sont créés et déclenchés. 
 * Si vous avez configuré GitHub, le référentiel exemple GitHub est cloné dans votre compte GitHub.


##Affichage d'une chaîne d'outils
{: #viewing_a_toolchain}

Une fois que vous avez configuré la chaîne d'outils et ses intégrations d'outils, vous pouvez afficher une représentation visuelle de la
chaîne
d'outils.

1. Dans le tableau de bord DevOps, dans la page **Chaînes d'outils**, cliquez sur la chaîne d'outils afin d'ouvrir sa page Vue
d'ensemble. Vous pouvez également, depuis la page de présentation de l'application, sur la carte Distribution continue, cliquer sur **Afficher la chaîne d'outils**. Ensuite, cliquez sur **Vue d'ensemble**.
2. Pour accéder à une intégration d'outils de votre chaîne d'outils, cliquez sur l'outil.

 **Conseil **: Si vous disposez de plusieurs référentiels GitHub, {{site.data.keyword.ghe_short}} ou Git, plusieurs cartes peuvent être disponibles pour une même intégration d'outils car chaque référentiel dispose de sa propre carte. Si vous disposez de plusieurs pipelines, plusieurs cartes peuvent être disponibles pour la même intégration d'outils car chaque pipeline est représenté par sa propre carte. Par exemple, lorsque vous créez une chaîne d'outils Microservices,
chacun des trois microservices dispose de son propre référentiel GitHub, {{site.data.keyword.ghe_short}} ou Git et de son propre pipeline.
