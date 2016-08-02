---

copyright:
  years: 2016

---
 
{:shortdesc: .shortdesc}
{:new_window: target="_blank"}

# Initiation aux chaînes d'outils (expérimental)
{: #toolchains_getting_started}

*Dernière mise à jour : 8 juin 2016*
{: .last-updated}  

Une chaîne d'outils est un ensemble d'intégrations d'outils prenant en charge des tâches de développement, de déploiement et d'opérations. La puissance collective d'une chaîne d'outils est supérieure à la somme de ses intégrations d'outils individuelles.
{: shortdesc}

Vous pouvez créer une chaîne d'outils de deux façons : à l'aide d'un modèle ou à partir d'une application. Selon le modèle ou la chaîne d'outils que vous utilisez, il est possible que la chaîne d'outils inclue un référentiel GitHub (repo) rempli avec le code de démarrage d'application et un pipeline de distribution préconfiguré. Lorsque vous envoyez des modifications par commande push au référentiel GitHub de la chaîne d'outils, le pipeline de distribution génère et déploie automatiquement l'application sur {{site.data.keyword.Bluemix}}.

Comme point de départ, vous pouvez utiliser un modèle de chaîne d'outils pour créer une chaîne d'outils possédant un ensemble spécifique d'intégrations d'outils ou une chaîne d'outils vide dans laquelle ajouter des intégrations d'outils. 

**Important **: Cette fonction est expérimentale. Les chaînes d'outils peuvent être instables et faire l'objet de modifications entraînant leur incompatibilité avec des versions antérieures. Elles ne sont pas recommandées pour une utilisation dans des environnements de production. Pour utiliser des chaînes d'outils, vous devez adresser une [demande d'accès](https://new-console.ng.bluemix.net/devops?cm_mmc=IBMBluemixGarageMethod-_-MethodSite-_-10-19-15::12-31-18-_-toolchains-welcome-page){: new_window} à usage unique.  Les chaînes d'outils sont disponibles uniquement dans la région sud des Etats-Unis. 


##Création d'une chaîne d'outils à partir d'un modèle   
{: #creating_a_toolchain_from_a_template}

Une fois votre demande d'accès aux chaînes d'outils approuvée, vous pouvez utiliser un modèle comme point de départ pour créer une chaîne d'outils incluant un ensemble spécifique d'intégrations d'outils. 

1. Dans le tableau de bord DevOps, onglet **Chaînes d'outils**, cliquez sur **Créer une chaîne d'outils** pour créer votre première chaîne d'outils. Si vous disposez déjà d'une chaîne d'outils, cliquez sur le bouton d'ajout (+) pour créer une autre chaîne d'outils. 
1. Cliquez sur un modèle de chaîne d'outils. Ainsi, pour utiliser un exemple de magasin en ligne, cliquez sur **Microservices Toolchain**. 
1. Sur la page de création de chaîne d'outils, passez en revue le diagramme de la chaîne d'outils que vous allez créer. Ce diagramme montre chaque intégration d'outil dans sa phase de cycle de vie au sein de la chaîne d'outils. L'image suivante fournit un exemple de diagramme. Lorsque vous créez une chaîne d'outils, le diagramme représente chaque intégration d'outil faisant partie de la chaîne d'outils.
![Diagramme de chaîne d'outils](images/toolchain_diagram.png)

1. Passez en revue les informations par défaut des paramètres de chaîne d'outils. Le nom de la chaîne d'outils l'identifie dans {{site.data.keyword.Bluemix}}. Si vous disposez déjà d'une chaîne d'outils portant ce nom, ou si vous souhaitez utiliser un nom différent, changez le nom de la chaîne d'outils.   
1. A la section Intégrations configurables, sélectionnez chaque intégration d'outil à configurer pour votre chaîne d'outils. Pour des informations sur la configuration des intégrations d'outils, voir [Configuration d'intégrations d'outils](../toolchains/toolchains_integrations.html){: new_window}.
1. Cliquez sur **Créer**. Plusieurs étapes s'exécutent automatiquement pour configurer votre chaîne d'outils. 

 * La chaîne d'outils est créée. 
 * Si vous avez configuré l'intégration d'outil Delivery Pipeline, les pipelines sont déclenchés. 
 * Si vous avez configuré l'intégration d'outil Sauce Labs, l'intégration de Sauce Labs est configurée pour ajouter des travaux aux pipelines et exécuter des tests.
 * Si vous avez configuré l'intégration d'outil PagerDuty, l'intégration de PagerDuty est configurée pour envoyer des notifications au canal configuré dans Slack. Ces notifications signalent quand un problème survient. 
 * Si vous avez configuré l'intégration d'outil Slack, l'intégration de Slack est configurée pour envoyer des notifications au canal configuré dans Slack. Ces notifications indiquent la progression du déploiement, par exemple `Connected with Project XYZ` (connecté au projet xyz), `Pipeline Configured` (pipeline configuré) ou `Stage 'build' started` (étape de génération lancée).
 * Si vous avez configuré l'intégration d'outil GitHub, le référentiel exemple GitHub est cloné dans votre compte GitHub. 


##Création d'une chaîne d'outils à partir d'une application
{: #creating_a_toolchain_from_an_app}

Une fois votre demande d'accès aux chaînes d'outils approuvée, vous pouvez créer une chaîne d'outils à partir de votre application. La chaîne d'outils peut prendre en charge le développement, le déploiement, la surveillance, etc. en continu, et elle est associée à votre application. Chaque application peut être associée à une chaîne d'outils. Lorsque vous envoyez des modifications par commande push au référentiel GitHub de la chaîne d'outils, le pipeline génère et déploie automatiquement l'application.   

1. Depuis la page de présentation de votre application, vignette de distribution continue, cliquez sur **Ajouter une chaîne d'outils**. Ou bien, depuis l'expérience Bluemix Classic Experience, cliquez sur **Ajouter un référentiel Git**. Votre application est configurée pour la distribution continue depuis un nouveau référentiel GitHub rempli avec le code de démarrage d'application. 
1. Sur la page de création de chaîne d'outils, passez en revue le diagramme de la chaîne d'outils que vous allez créer. Ce diagramme montre chaque intégration d'outil dans sa phase de cycle de vie au sein de la chaîne d'outils. 
1. Passez en revue les informations par défaut des paramètres de chaîne d'outils. Le nom de la chaîne d'outils l'identifie dans {{site.data.keyword.Bluemix}}. Si vous disposez déjà d'une chaîne d'outils portant ce nom, ou si vous souhaitez utiliser un nom différent, changez le nom de la chaîne d'outils. 
1. A la section Intégrations configurables, sélectionnez chaque intégration d'outil à configurer pour votre chaîne d'outils. Pour des informations sur la configuration des intégrations d'outils, voir [Configuration d'intégrations d'outils](../toolchains/toolchains_integrations.html){: new_window}.
1. Cliquez sur **Créer**. Plusieurs étapes s'exécutent automatiquement pour configurer votre chaîne d'outils. 

 * La chaîne d'outils est créée. 
 * Si vous avez configuré l'intégration d'outil Delivery Pipeline, les pipelines sont déclenchés. 
 * Si vous avez configuré l'intégration d'outil Sauce Labs, l'intégration de Sauce Labs est configurée pour ajouter des travaux aux pipelines et exécuter des tests.
 * Si vous avez configuré l'intégration d'outil PagerDuty, l'intégration de PagerDuty est configurée pour envoyer des notifications au canal configuré dans Slack. Ces notifications signalent quand un problème survient. 
 * Si vous avez configuré l'intégration d'outil Slack, l'intégration de Slack est configurée pour envoyer des notifications au canal configuré dans Slack. Ces notifications indiquent la progression du déploiement, par exemple `Connected with Project XYZ` (connecté au projet xyz), `Pipeline Configured` (pipeline configuré) ou `Stage 'build' started` (étape de génération lancée).
 * Si vous avez configuré l'intégration d'outil GitHub, le référentiel exemple GitHub est cloné dans votre compte GitHub. 

 
##Affichage d'une chaîne d'outils
{: #viewing_a_toolchain}

Une fois la chaîne d'outils et toutes les intégrations d'outils configurées, vous pouvez afficher une représentation de la chaîne d'outils dans la page Intégrations d'outils. 

1. Dans le tableau de bord DevOps, onglet **Chaînes d'outils**, cliquez sur une chaîne d'outils pour ouvrir la page d'intégration d'outil correspondante. Vous pouvez également, depuis la page de présentation de l'application, vignette de distribution continue, cliquer sur **Afficher la chaîne d'outils** puis sur **Intégrations d'outils**.
1. Examinez la page pour avoir une représentation de la chaîne d'outils. 
1. Pour accéder à une intégration d'outil de votre chaîne d'outils, cliquez sur la vignette de l'outil. 
 
 **Conseil **: Si vous disposez de plusieurs référentiels GitHub, plusieurs vignettes peuvent être disponibles pour une même intégration d'outil car chaque référentiel doit disposer de son propre pipeline.


 <!-- The toolchain in the following image is an example. When you create your own toolchain, the visual representation of the toolchain shows the tool integrations that you configure.
![Sample toolchain](images/toolchain.png) -->


# Liens connexes
{: #rellinks}

## Tutoriels et exemples
{: #samples}

* [Create an application with three microservices](https://www.ibm.com/devops/method/tutorials/tutorial_microservices_part1){:new_window}

## Liens connexes
{: #general}

* [Microservices toolchain (Experimental)](https://www.ibm.com/devops/method/toolchains/microservices_toolchain){:new_window}
* [Simple toolchain (Experimental)](https://www.ibm.com/devops/method/toolchains/simple_toolchain){:new_window}
* [IBM&reg; Bluemix&reg; Garage Method](https://www.ibm.com/devops/method){:new_window}
