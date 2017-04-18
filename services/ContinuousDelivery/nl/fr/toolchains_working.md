---

copyright:
  years: 2016

---
 
{:shortdesc: .shortdesc}
{:new_window: target="_blank"}

# Utilisation de chaînes d'outils
{: #toolchains_getting_started}

Dernière mise à jour : 17 novembre 2016
{: .last-updated}  

Une *chaîne d'outils* est un ensemble d'intégrations d'outils prenant en charge des tâches de développement, de déploiement et d'opérations. La puissance collective d'une chaîne d'outils est supérieure à la somme de ses intégrations d'outils individuelles.
{: shortdesc}

Les chaînes d'outils sont disponibles dans les environnements {{site.data.keyword.Bluemix}} public et dédié. Vous pouvez créer une chaîne d'outils de deux façons : à l'aide d'un modèle ou à partir d'une application. Sur {{site.data.keyword.Bluemix_notm}} Public, les chaînes d'outils ne sont disponibles que dans la région Su des Etats-Unis.

## Initiation aux chaînes d'outils : public
{: #getting_started_public}

Chaque chaîne d'outils est associée à une organisation spécifique (org) et tout membre de cette organisation peut accéder aux chaînes d'outils associées. Avant de créer une chaîne d'outils, assurez-vous de travailler dans l'organisation dans laquelle vous voulez créer la chaîne d'outils. L'organisation au sein de laquelle vous travaillez actuellement s'affiche dans la barre de menus. Pour passer à une autre organisation, cliquez sur l'organisation dans la barre de menus, puis sélectionnez l'organisation souhaitée.

### Création d'une chaîne d'outils à partir d'un modèle   
{: #creating_a_toolchain_from_a_template}

Vous pouvez utiliser un modèle comme point de départ pour [créer une chaîne d'outils
(Lien s'ouvrant dans une nouvelle fenêtre)](https://console.ng.bluemix.net/devops/create){: new_window} incluant un ensemble spécifique d'intégrations d'outils. Pour en savoir plus sur
l'utilisation des modèles, voir la page [IBM Bluemix Garage Method (Lien s'ouvrant dans une
nouvelle fenêtre)](https://www.ibm.com/devops/method/category/tools){:new_window}.

1. Connectez-vous à [{{site.data.keyword.Bluemix_notm}} (ce lien ouvre une nouvelle fenêtre)](http://console.ng.bluemix.net){:new_window}. Le Tableau de bord {{site.data.keyword.Bluemix_notm}} s'affiche et présente l'espace {{site.data.keyword.Bluemix_notm}} actif pour votre organisation.
1. Depuis le menu en hamburger, cliquez sur **Services**, puis sur **DevOps**.
1. Dans le tableau de bord DevOps, sur la page **Chaînes d'outils**, cliquez sur **Créer une chaîne d'outils**.
1. Sur la page **Créer une chaîne d'outils**, cliquez sur un modèle de chaîne d'outils.
1. Examinez le diagramme de la chaîne d'outils que vous être sur le point de créer. Ce diagramme montre chaque intégration d'outil dans sa phase de cycle de vie au sein de la chaîne d'outils. L'image suivante fournit un exemple de diagramme. Lorsque vous créez une chaîne d'outils, le diagramme représente chaque intégration d'outil faisant partie de la chaîne d'outils.
![Diagramme de chaîne d'outils](images/toolchain_diagram.png)

1. Passez en revue les informations par défaut des paramètres de chaîne d'outils. Le nom de la chaîne d'outils l'identifie dans {{site.data.keyword.Bluemix_notm}}. Si vous désirez utiliser un nom différent, modifiez le nom de la chaîne d'outils.  
1. A la section Intégrations configurables, sélectionnez chaque intégration d'outil à configurer pour votre chaîne d'outils. Quelques intégrations d'outils ne nécessitent pas de configuration. Pour des informations sur la configuration des intégrations d'outils, voir [Configuration d'intégrations d'outils](/docs/services/ContinuousDelivery/toolchains_integrations.html){: new_window}.
1. Cliquez sur **Créer**.  Plusieurs étapes s'exécutent automatiquement pour configurer votre chaîne d'outils.

 * La chaîne d'outils est créée.
 * Si vous avez configuré l'intégration de l'outil Delivery Pipeline, les pipelines sont créés et déclenchés.
 * Si vous avez configuré l'intégration de l'outil Sauce Labs, celui-ci est configuré pour ajouter des travaux aux pipelines et exécuter des tests.
 * Si vous avez configuré l'intégration de l'outil PagerDuty, PagerDuty est configuré pour envoyer des notifications d'alerte au service que vous avez spécifié.
 * Si vous avez configuré l'intégration de l'outil Slack, Slack est configuré pour envoyer au canal que vous avez spécifié des notifications sur le statut de déploiement.
 * Si vous avez configuré l'intégration d'outil GitHub, le référentiel exemple GitHub est cloné dans votre compte GitHub.


### Création d'une chaîne d'outils à partir d'une application
{: #creating_a_toolchain_from_an_app}

Vous pouvez créer une chaîne d'outils depuis votre application. La chaîne d'outils peut prendre en charge en continu le développement, le déploiement, la surveillance, etc. et elle est associée à votre application. Chaque application peut être associée à une chaîne d'outils. Lorsque vous envoyez des modifications au référentiel GitHub de la chaîne d'outils, le pipeline génère et déploie automatiquement l'application.  

1. Depuis la page de présentation de votre application, sur la vignette Continuous Delivery, cliquez sur **Activer**. Votre application est configurée pour la distribution continue depuis un nouveau référentiel GitHub rempli avec le code de démarrage d'application.
1. Sur la page de création de chaîne d'outils, passez en revue le diagramme de la chaîne d'outils que vous allez créer. Ce diagramme montre chaque intégration d'outil dans sa phase de cycle de vie au sein de la chaîne d'outils.
1. Passez en revue les informations par défaut des paramètres de chaîne d'outils. Le nom de la chaîne d'outils l'identifie dans {{site.data.keyword.Bluemix_notm}}. Si vous désirez utiliser un nom différent, modifiez le nom de la chaîne d'outils.
1. A la section Intégrations configurables, sélectionnez chaque intégration d'outil à configurer pour votre chaîne d'outils. Quelques intégrations d'outils ne nécessitent pas de configuration. Pour des informations sur la configuration des intégrations d'outils, voir [Configuration d'intégrations d'outils](/docs/services/ContinuousDelivery/toolchains_integrations.html){: new_window}.
1. Cliquez sur **Créer**.  Plusieurs étapes s'exécutent automatiquement pour configurer votre chaîne d'outils.

 * La chaîne d'outils est créée.
 * Si vous avez configuré l'intégration de l'outil Delivery Pipeline, les pipelines sont créés et déclenchés.
 * Si vous avez configuré l'intégration de l'outil Sauce Labs, celui-ci est configuré pour ajouter des travaux aux pipelines et exécuter des tests.
 * Si vous avez configuré l'intégration de l'outil PagerDuty, PagerDuty est configuré pour envoyer des notifications d'alerte au service que vous avez spécifié.
 * Si vous avez configuré l'intégration de l'outil Slack, Slack est configuré pour envoyer au canal que vous avez spécifié des notifications sur le statut de déploiement.
 * Si vous avez configuré l'intégration d'outil GitHub, le référentiel exemple GitHub est cloné dans votre compte GitHub.


## Initiation aux chaînes d'outils : dédié
{: #getting_started_dedicated}

Chaque chaîne d'outils est associée à une organisation spécifique, et tout utilisateur membre de cette organisation peut accéder aux chaînes d'outils associées. Avant
de créer une chaîne d'outils, cliques sur l'icône **{{site.data.keyword.avatar}}** dans la barre de menu pour ouvrir le widget Compte et support et afficher l'organisation dans laquelle vous opérez. Si cette organisation n'est pas celle dans laquelle vous voulez créer la chaîne d'outils, passez à une autre organisation.

### Création d'une chaîne d'outils à partir d'un modèle   
{: #creating_a_toolchain_from_a_template_dedicated}

Vous pouvez utiliser un modèle comme point de départ pour créer une chaîne d'outils incluant un ensemble spécifique d'intégrations d'outils.

1. Dans le tableau de bord {{site.data.keyword.Bluemix_notm}}, onglet **DEVOPS**, cliquez sur le bouton d'ajout (+) pour créer une chaîne d'outils.
1. Sur la page **Créer une chaîne d'outils**, cliquez sur un modèle de chaîne d'outils. 
1. Examinez le diagramme de la chaîne d'outils que vous être sur le point de créer. Ce diagramme montre chaque intégration d'outil dans sa phase de cycle de vie au sein de la chaîne d'outils. L'image suivante fournit un exemple de diagramme. Lorsque vous créez une chaîne d'outils, le diagramme représente chaque intégration d'outil faisant partie de la chaîne d'outils.
![Diagramme des chaînes d'outils dédiées](images/toolchain_dedicated_diagram.png)

1. Passez en revue les informations par défaut des paramètres de chaîne d'outils. Le nom de la chaîne d'outils l'identifie dans {{site.data.keyword.Bluemix_notm}}. Si vous disposez déjà d'une chaîne d'outils portant ce nom, ou si vous souhaitez utiliser un nom différent, changez le nom de la chaîne d'outils.  
1. A la section Intégrations configurables, sélectionnez chaque intégration d'outil à configurer pour votre chaîne d'outils. Quelques intégrations d'outils ne nécessitent pas de configuration. Pour des informations sur la configuration des intégrations d'outils, voir [Configuration d'intégrations d'outils](/docs/services/ContinuousDelivery/toolchains_integrations.html){: new_window}.
1. Cliquez sur **Créer**.  Plusieurs étapes s'exécutent automatiquement pour configurer votre chaîne d'outils.

 * La chaîne d'outils est créée.
 * Si vous avez configuré l'intégration de l'outil Delivery Pipeline, les pipelines sont créés et déclenchés.
 * Si vous avez configuré l'intégration de l'outil PagerDuty, PagerDuty est configuré pour envoyer des notifications d'alerte au service que vous avez spécifié.
 * Si vous avez configuré l'intégration de l'outil Slack, Slack est configuré pour envoyer au canal que vous avez spécifié des notifications sur le statut de déploiement.
 * Si vous avez configuré l'intégration d'outil GitHub Enterprise, le référentiel exemple GitHub Enterprise est cloné dans votre compte GitHub Enterprise.


### Création d'une chaîne d'outils à partir d'une application
{: #creating_a_toolchain_from_an_app_dedicated}

Vous pouvez créer une chaîne d'outils depuis votre application. La chaîne d'outils peut prendre en charge en continu le développement, le déploiement, la surveillance, etc. et elle est associée à votre application. Chaque application peut être associée à une chaîne d'outils. Lorsque vous envoyez des modifications au référentiel GitHub Enterprise de la chaîne d'outils, le pipeline génère et déploie automatiquement l'application.  

1. Dans le coin supérieur droit de la page de présentation de votre application, cliquez sur **Ajouter une chaîne d'outils**. Votre application est configurée pour la distribution continue depuis un nouveau référentiel GitHub Enterprise rempli avec le code de démarrage d'application.
1. Sur la page de création de chaîne d'outils, passez en revue le diagramme de la chaîne d'outils que vous allez créer. Ce diagramme montre chaque intégration d'outil dans sa phase de cycle de vie au sein de la chaîne d'outils.
1. Passez en revue les informations par défaut des paramètres de chaîne d'outils. Le nom de la chaîne d'outils l'identifie dans {{site.data.keyword.Bluemix_notm}}. Si vous disposez déjà d'une chaîne d'outils portant ce nom, ou si vous souhaitez utiliser un nom différent, changez le nom de la chaîne d'outils.
1. A la section Intégrations configurables, sélectionnez chaque intégration d'outil à configurer pour votre chaîne d'outils. Quelques intégrations d'outils ne nécessitent pas de configuration. Pour des informations sur la configuration des intégrations d'outils, voir [Configuration d'intégrations d'outils](/docs/services/ContinuousDelivery/toolchains_integrations.html){: new_window}.
1. Cliquez sur **Créer**.  Plusieurs étapes s'exécutent automatiquement pour configurer votre chaîne d'outils.

 * La chaîne d'outils est créée.
 * Si vous avez configuré l'intégration de l'outil Delivery Pipeline, les pipelines sont créés et déclenchés.
 * Si vous avez configuré l'intégration de l'outil PagerDuty, PagerDuty est configuré pour envoyer des notifications d'alerte au service que vous avez spécifié.
 * Si vous avez configuré l'intégration de l'outil Slack, Slack est configuré pour envoyer au canal que vous avez spécifié des notifications sur le statut de déploiement.
 * Si vous avez configuré l'intégration d'outil GitHub Enterprise, le référentiel exemple GitHub Enterprise est cloné dans votre compte GitHub Enterprise.


## Affichage d'une chaîne d'outils
{: #viewing_a_toolchain}

Une fois que vous avez configuré la chaîne d'outils et ses intégrations d'outils, vous pouvez afficher une représentation visuelle de la
chaîne
d'outils.

* Si vous utilisez l'environnement {{site.data.keyword.Bluemix_notm}} public, dans le tableau de bord DevOps, dans la page **Chaînes
d'outils**, cliquez sur une chaîne d'outils pour ouvrir sa page Vue d'ensemble. Vous pouvez également, depuis la page de présentation de l'application, sur la vignette Continuous Delivery, cliquer sur **Afficher la chaîne d'outils**. Ensuite,
cliquez sur **Vue d'ensemble**. 
   
* Si vous utilisez {{site.data.keyword.Bluemix_notm}} dédié, dans le tableau de bord, onglet **DEVOPS**, cliquez sur la chaîne d'outils pour ouvrir la page d'intégration d'outil correspondante. Vous pouvez également, dans le coin supérieur droit de la page de présentation de l'application, cliquer sur **Afficher la chaîne d'outils**.

* Pour accéder à une intégration d'outil de votre chaîne d'outils, cliquez sur la vignette de l'outil. 
 
 **Conseil **: Si vous disposez de plusieurs référentiels GitHub ou GitHub Enterprise, plusieurs vignettes peuvent être disponibles pour une même intégration d'outil car chaque référentiel dispose de sa propre vignette.


# Liens connexes
{: #rellinks}

## Tutoriels et exemples
{: #samples}

* [Créer et utiliser votre première chaîne d'outils (ce lien ouvre une
nouvelle fenêtre)](https://www.ibm.com/devops/method/tutorials/tutorial_toolchain_flow){:new_window}
* [Créer une chaîne d'outils personnalisée (ce lien ouvre une nouvelle
fenêtre)](https://www.ibm.com/devops/method/tutorials/tutorial_toolchain_custom){:new_window}
* [Créer une application avec trois microservices (ce lien ouvre une
nouvelle fenêtre)](https://www.ibm.com/devops/method/tutorials/tutorial_toolchain_microservices){:new_window}
* [Create a toolchain from a template on {{site.data.keyword.Bluemix_notm}} Dedicated (Beta) (Lien s'ouvrant dans une nouvelle fenêtre)](https://www.ibm.com/devops/method/tutorials/tutorial_dedicated_toolchain_template_flow){:new_window}
* [Create a toolchain from an app on {{site.data.keyword.Bluemix_notm}} Dedicated (Beta) (Lien s'ouvrant dans une nouvelle fenêtre)](https://www.ibm.com/devops/method/tutorials/tutorial_dedicated_toolchain_app_flow){:new_window}

## Liens connexes
{: #general}

* [Chaîne d'outils de microservices (ce lien ouvre une nouvelle
fenêtre)](https://www.ibm.com/devops/method/toolchains/microservices_toolchain){:new_window}
* [Chaîne d'outils simple (ce lien ouvre une nouvelle
fenêtre)](https://www.ibm.com/devops/method/toolchains/simple_toolchain){:new_window}
* [IBM Bluemix Garage Method (Lien s'ouvrant dans une nouvelle fenêtre)](https://www.ibm.com/devops/method){:new_window}
