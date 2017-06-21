---

copyright:
  years: 2016, 2017
lastupdated: "2017-05-19"

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}
{:tip: .tip}

# Intégration avec Jenkins Pipeline

Après avoir ajouté {{site.data.keyword.DRA_full}} à une chaîne d'outils ouverte et défini les politiques qu'il surveille, vous pouvez l'intégrer à un projet Jenkins Pipeline. Vous définissez un pipeline dans l'interface Web Jenkins ou dans un fichier *Jenkinsfile* que vous stockez dans votre référentiel de contrôle des sources. Vous pouvez afficher et administrer des projets Jenkins Pipeline à partir de l'interface Web Jenkins. 

Le plug-in IBM Cloud DevOps pour Jenkins intègre des projets Jenkins à des chaînes d'outils. Une *chaîne d'outils* est un ensemble d'intégrations d'outils prenant en charge des tâches de développement, de déploiement et d'opérations. La puissance collective d'une chaîne d'outils est supérieure à la somme de ses intégrations d'outils individuelles. Les chaînes d'outils ouvertes font partie du service {{site.data.keyword.contdelivery_full}}. Pour en savoir plus sur le service {{site.data.keyword.contdelivery_short}}, voir [la documentation associée](https://console.ng.bluemix.net/docs/services/ContinuousDelivery/cd_about.html). 

Après avoir installé le plug-in IBM Cloud DevOps, vous pouvez configurer votre projet Jenkins afin de publier les résultats de test sur {{site.data.keyword.DRA_short}}, évaluer automatiquement la qualité de la génération aux jalons et effectuer le suivi des risques de déploiement. Vous pouvez également envoyer des notifications de travail à d'autres outils de la chaîne d'outils, tels que Slack et PagerDuty. Afin de faciliter le suivi des déploiements, la chaîne d'outils peut ajouter des messages de déploiement aux validations Git, ainsi qu'aux problèmes Git ou JIRA associés. Vous pouvez également afficher vos déploiements sur la page Connexions de votre chaîne d'outils. 

Le plug-in fournit des actions et des interfaces de ligne de commande post-génération pour la prise en charge de l'intégration. {{site.data.keyword.DRA_short}} agrège et analyse les résultats des tests d'unité, des tests fonctionnels, des outils de couvertures de code, des examens du code de sécurité statique et des examens du code de sécurité dynamique afin de déterminer si votre code répond aux politiques prédéfinies aux jalons de votre processus de déploiement. Si votre code ne satisfait pas ou dépasse une politique, le déploiement est interrompu afin de prévenir toute modification à risque. Vous pouvez utiliser {{site.data.keyword.DRA_short}} comme filet de sécurité pour votre environnement de distribution continue en vue d'implémenter et d'améliorer les normes qualité au fil du temps, ainsi que comme outil de visualisation de données pour vous aider à comprendre la santé de votre projet.

Si vous connaissez déjà Jenkins Pipeline, poursuivez votre lecture. Sinon, [consultez la documentation de Jenkins Pipeline](https://jenkins.io/doc/book/pipeline/) avant de continuer.

## Prérequis
{: #jenkins_prerequisites}

Vous devez avoir accès à un serveur qui exécute un projet Jenkins Pipeline. 

## Création d'une chaîne d'outils
{: #jenkins_create}

Avant de pouvoir intégrer {{site.data.keyword.DRA_short}} à un projet Jenkins, vous devez créer une chaîne d'outils. 

1. Pour créer une chaîne d'outils, accédez à la [page Créer une chaîne d'outils](https://console.ng.bluemix.net/devops/create) et suivez les instructions. 

2. Après avoir créé la chaîne d'outils, ajoutez-y{{site.data.keyword.DRA_short}}. Pour plus d'instructions, voir la [documentation {{site.data.keyword.DRA_short}}](https://console.ng.bluemix.net/docs/services/DevOpsInsights/index.html). 

## Installation du plug-in
{: #jenkins_install}

Installez le plug-in sur votre serveur Jenkins en ouvrant l'interface du serveur et en procédant comme suit : 

1. Cliquez sur **Manage Jenkins**.
2. Cliquez sur **Manage Plugins**. 
3. Cliquez sur l'onglet **Available**.
4. Activez le filtre en fonction d'`IBM Cloud DevOps`. 
5. Sélectionnez **IBM Cloud DevOps**.
6. Cliquez sur **Download now and install after restart**. 

Le plug-in est disponible après le redémarrage du serveur.   

## Création d'un pipeline
{: #jenkinsfile_create}

Vous définissez les pipelines dans le menu de configuration du projet Jenkins ou dans un fichier Jenkinsfile du référentiel. Pour ce faire, créez ou ouvrez un script ou le fichier Jenkinsfile à utiliser avec {{site.data.keyword.DRA_short}}. Vous pouvez suivre le format [déclaratif](https://jenkins.io/doc/book/pipeline/syntax/#declarative-pipeline) ou [script](https://jenkins.io/doc/book/pipeline/syntax/#scripted-pipeline).

## Exposition des variables d'environnement requises

Ouvrez la définition de pipeline. 

Dans la définition, ajoutez les variables d'environnement suivantes. Ces variables sont requises pour l'intégration du pipeline avec {{site.data.keyword.DRA_short}}.

| Variable d'environnement        | Définition    |
| ----------------------------|---------------|
| `IBM_CLOUD_DEVOPS_CREDS`    | Données d'identification Bluemix que vous définissez dans Jenkins à l'aide de la commande `credentials`. Par exemple, `IBM_CLOUD_DEVOPS_CREDS = credentials('BM_CRED')`. Cette commande définit automatiquement deux variables d'environnement supplémentaires : `IBM_CLOUD_DEVOPS_CREDS_USR` et `IBM_CLOUD_DEVOPS_CREDS_PSW` pour le nom d'utilisateur et le mot de passe.   |
| `IBM_CLOUD_DEVOPS_ORG`      | Organisation Bluemix à laquelle votre chaîne d'outils appartient.     |
| `IBM_CLOUD_DEVOPS_APP_NAME` | Nom de l'application déployée par votre chaîne d'outils.   |
| `IBM_CLOUD_DEVOPS_TOOCLHAIN_ID` | ID de votre chaîne d'outils. Ouvrez la présentation de la chaîne d'outils et examinez son URL pour connaître l'ID. L'URL de la chaîne d'outils est au format suivant : `https://console.ng.bluemix.net/devops/toolchains/[ID_VOTRE_CHAINE_OUTILS]`.   |
| `IBM_CLOUD_DEVOPS_WEBHOOKURL` | Webhook que vous avez fourni lorsque vous avez ajouté Jenkins à votre chaîne d'outils.   |

Pour plus d'informations sur la commande `credentials`, voir la [documentation sur le pipeline Jenkins](https://jenkins.io/doc/pipeline/tour/environment/#credentials-in-the-environment).
{: tip}

Si vous utilisez le format de pipeline script, définissez vos données d'identification avec `withCredentials` et votre environnement avec `withEnv` à la place de `credentials` et `environment`, qui sont employés dans l'exemple ci-après. Pour plus d'informations sur `withCredentials`, voir la [documentation Jenkins](https://jenkins.io/doc/pipeline/steps/credentials-binding/).
{: tip} 

Ces variables d'environnement et ces données d'identification sont utilisées par le plug-in IBM Cloud DevOps pour interagir avec DevOps Insights. Voici un exemple de définition au format de pipeline déclaratif. 

```
environment {
        IBM_CLOUD_DEVOPS_CREDS = credentials('BM_CRED')
        IBM_CLOUD_DEVOPS_ORG = 'dlatest'
        IBM_CLOUD_DEVOPS_APP_NAME = 'Weather-App'
        IBM_CLOUD_DEVOPS_TOOLCHAIN_ID = '1111111-aaaa-2222-bbbb-333333333'
        IBM_CLOUD_DEVOPS_WEBHOOK_URL = 'https://jenkins:5a55555a-a555-5555-5555-a555aa55a555:55555555-5555-5555-5555-555555555555@devops-api.ng.bluemix.net/v1/toolint/messaging/webhook/publish'
    }
```


## Ajout d'étapes Cloud DevOps
Le plug-in Cloud DevOps ajoute quatre étapes aux pipelines Jenkins. Vous pouvez utiliser ces étapes dans vos pipelines pour interagir avec DevOps Insights. 

* `publishBuildRecord`, qui publie des informations de génération dans DevOps Insights
* `publishTestResult`, qui publie des résultats de test dans DevOps Insights
* `publishDeployRecord`, qui publie des enregistrements de déploiement dans DevOps Insights
* `evaluateGate`, qui applique des politiques DevOps Insights 

Ajoutez ces étapes à votre définition de pipeline là où vous avez besoin de les exécuter. Par exemple, vous pouvez transférer des résultats de test après avoir exécuté un test, puis évaluer ces résultats à un jalon une fois qu'ils sont transférés.  

### Publication d'enregistrements de génération

Publiez des enregistrements de génération avec l'étape `publishBuildRecord`. Cette étape requiert quatre paramètres.

| Paramètre        | Définition    |
| ----------------------------|---------------|
| `gitBranch`    | Nom de la branche Git utilisée par la génération.  |
| `gitCommit`      | ID de validation Git utilisé par la génération.    |
| `gitRepo` | URL du référentiel Git.   |
| `result` | Résultat de l'étape de génération. Valeur : `SUCCESS` ou `FAIL`.   |

Voici un exemple de commande employant ces paramètres : 

```
publishBuildRecord gitBranch: "${GIT_MASTER}", gitCommit: "${GIT_COMMIT}", gitRepo: "https://github.com/username/reponame", result:"SUCCESS"
```

Jenkins Pipeline n'expose pas les informations Git en tant que variables d'environnement. Vous pouvez obtenir l'ID de validation Git à l'aide de la commande `sh(returnStdout: true, script: 'git rev-parse HEAD').trim()`.
{: tip}

### Publication de résultats de test
Publiez des enregistrements de génération avec l'étape `publishTestResult`. Cette étape requiert deux paramètres.

| Paramètre        | Définition    |
| ----------------------------|---------------|
| `type`    | Type du résultat de test. La valeur doit être `unittest` pour les tests d'unité, `fvt` pour les tests de vérification fonctionnelle, ou `code` pour les tests de couverture de code.  |
| `fileLocation`      | Emplacement du fichier de résultats de test.    |

Voici quelques exemples de commande comportant ces paramètres. La première commande publie les résultats d'un test d'unité Mocha, la seconde publie les résultats d'un test de couverture de code. 

```
publishTestResult type:'unittest', fileLocation: './mochatest.json'
publishTestResult type:'code', fileLocation: './tests/coverage/reports/coverage-summary.json'
```

### Publication d'enregistrements de déploiement

Publiez des enregistrements de déploiement avec l'étape `publishDeployRecord`. Cette étape requiert deux paramètres. Elle peut également accepter un paramètre facultatif.  

| Paramètre        | Définition    |
| ----------------------------|---------------|
| `environment`    | Environnement dans lequel vous déployez votre application. Pour que DevOps Insights fonctionne correctement, vous devez identifier un environnement en tant que `STAGING` et un autre environnement en tant que `PRODUCTION`. |
| `result`      | Résultat de l'étape de génération. Valeur admise : `SUCCESS` ou `FAIL`.    |
| `appUrl`      | *Facultatif* : URL employée pour l'accès à votre application.    |

Voici quelques exemples de commande comportant ces paramètres. La première commande publie l'enregistrement de déploiement pour un environnement de constitution, la seconde publie l'enregistrement de déploiement pour un environnement de production. 

```
publishDeployRecord environment: "STAGING", appUrl: "http://staging-Weather-App.mybluemix.net", result:"SUCCESS"
publishDeployRecord environment: "PRODUCTION", appUrl: "http://Weather-App.mybluemix.net", result:"SUCCESS"
```

### Ajout de jalons

Ajoutez des jalons à votre pipeline à l'aide de la commande `evaluateGate`. Les jalons appliquent les politiques DevOps Insights, qui définissent les exigences en matière de test pour la promotion de la génération. 

Cette étape requiert un paramètre. Elle peut également accepter un paramètre facultatif.  

| Paramètre        | Définition    |
| ----------------------------|---------------|
| `policy`    | Nom de la politique implémentée par le jalon. Le nom de la politique est défini dans DevOps Insights. |
| `forceDecision`      | *Facultatif* : indique si le pipeline s'arrête ou non, en fonction de la décision du jalon. Définissez ce paramètre sur `true` pour arrêter l'exécution du pipeline en cas d'échec au jalon. Définissez-le sur `false` pour autoriser le pipeline à poursuivre après un échec au jalon. Par défaut, la valeur est définie sur `false`.     |

Voici un exemple de commande employant ces paramètres. Dans cette commande, le pipeline continue à s'exécuter quelle que soit la décision du jalon.  

```
evaluateGate policy: 'Weather App Policy', forceDecision: 'true'
```

### Communication avec les chaînes d'outils

Envoyez le statut du pipeline aux chaînes d'outils Bluemix à l'aide de la commande `notifyOTC`. Pour en savoir plus sur l'intégration de Jenkins avec des chaînes d'outils, voir la [documentation](https://console.ng.bluemix.net/docs/services/ContinuousDelivery/toolchains_integrations.html#jenkins). Vous pouvez ignorer les étapes 6d à 6f, car elles s'appliquent uniquement aux projets Jenkins à structure libre.

Cette étape requiert deux paramètres et peut également admettre un paramètre facultatif.  

| Paramètre        | Définition    |
| ----------------------------|---------------|
| `stageName`    | Nom de l'étape en cours du pipeline. |
| `status`    | Statut de l'étape du pipeline en cours. Si vous utilisez `SUCCESS`, `FAILURE` ou `ABORTED`, une mise en évidence en couleur est automatiquement déclenchée dans Slack.  |
| `webhookUrl`      | *Facultatif* : URL du webhook qui s'affiche dans la mosaïque Jenkins de votre chaîne d'outils. Si vous incluez ce paramètre, sa valeur écrase celle de la variable d'environnement `IBM_CLOUD_DEVOPS_WEBHOOKURL`.   |

Voici quelques exemples d'utilisation de l'étape `notifyOTC` dans des définitions de pipeline déclaratives et script . 

#### Pipeline déclaratif
```
stage('Deploy') {
    steps {
      ...
    }

    post {
        success {
            notifyOTC stageName: "Deploy", status: "SUCCESS"
        }
        failure {
            notifyOTC stageName: "Deploy", status: "FAILURE", webhookUrl: "https://different-webhook-url@devops-api.ng.bluemix.net/v1/toolint/messaging/webhook/publish"
        }
    }
}
```

#### Pipeline script
```
stage('Deploy') {
  try {
      ... (deploy steps)

      notifyOTC stageName: "Deploy", status: "SUCCESS"
  }
  catch (Exception e) {
      notifyOTC stageName: "Deploy", status: "FAILURE", webhookUrl: "https://different-webhook-url@devops-api.ng.bluemix.net/v1/toolint/messaging/webhook/publish"
  }
}
```

Dans ces deux exemple, l'URL du webhook de la chaîne d'outils est remplacée uniquement en cas d'échec.  

## Garantie de traçabilité dans les intégrations de chaîne d'outils

Configurez votre environnement Jenkins de manière à l'intégrer à votre chaîne d'outils Bluemix en suivant les instructions figurant dans la [documentation Bluemix](https://console.ng.bluemix.net/docs/services/ContinuousDelivery/toolchains_integrations.html#jenkins). Vous pouvez ignorer les étapes 6d à 6f, car elles s'appliquent uniquement aux projets Jenkins à structure libre.

L'intégration à une chaîne d'outils vous garantit une traçabilité de bout en bout et un mappage de déploiement. Après avoir suivi les instructions d'intégration, ajoutez la commande `cf icd --create-connection $IBM_CLOUD_DEVOPS_WEBHOOK_URL $CF_APP_NAME` après vos étapes de déploiement. Cette commande connecte votre intégration Jenkins à une application qui s'exécute sur Bluemix. 

Voici un exemple d'étape de déploiement complète. La dernière commande est `cf icd --create-connection`. 

<pre>
sh '''
    echo "CF Login..."
    cf api https://api.ng.bluemix.net
    cf login -u $IBM_CLOUD_DEVOPS_CREDS_USR -p $IBM_CLOUD_DEVOPS_CREDS_PSW -o $IBM_CLOUD_DEVOPS_ORG -s staging
    echo "Deploying...."
    export CF_APP_NAME="staging-$IBM_CLOUD_DEVOPS_APP_NAME"
    cf delete $CF_APP_NAME -f
    cf push $CF_APP_NAME -n $CF_APP_NAME -m 64M -i 1
    <b>cf icd --create-connection $IBM_CLOUD_DEVOPS_WEBHOOK_URL $CF_APP_NAME</b>
'''
</pre>

Comme décrit dans la documentation de l'intégration Jenkins, les plug-in de l'interface de ligne de commande CloudFoundry et CloudFoundry ICD doivent être installés sur votre serveur Jenkins. Vous devez également vous connecter à Bluemix à partir du serveur afin de vous y connecter.

## Exemple de pipeline déclaratif

Cet exemple illustre un pipeline complet défini en tant que fichier Jenkinsfile déclaratif. 

```
#!groovy
/*
    Voici un exemple de fichier Jenkins pour l'application météo Weather, une application node.js avec un test d'unité, des tests de
    couverture de code et des tests de vérification fonctionnelle, qui est déployée dans un environnement de préproduction et de
    production et qui utilise le jalon IBM Cloud DevOps.
    Nous l'utilisons comme exemple pour notre plug-in dans le fichier Jenkinsfile.
    Vous devez spécifier 4 variables d'environnement requises pour pouvoir utiliser 4
    méthodes différentes pour l'étape de génération/test/déploiement et le jalon.
 */
pipeline {
    agent any
    environment {
        // Vous devez d'abord indiquer 4 variables d'environnement requises qui seront utilisées pour les étapes IBM Cloud DevOps suivantes
        IBM_CLOUD_DEVOPS_CREDS = credentials('BM_CRED')
        IBM_CLOUD_DEVOPS_ORG = 'dlatest'
        IBM_CLOUD_DEVOPS_APP_NAME = 'Weather-V1'
        IBM_CLOUD_DEVOPS_TOOLCHAIN_ID = '1320cec1-daaa-4b63-bf06-7001364865d2'
        IBM_CLOUD_DEVOPS_WEBHOOK_URL = 'WEBHOOK_URL_PLACEHOLDER'
    }
    tools {
        nodejs 'recent'
    }
    stages {
        stage('Build') {
            environment {
                // Obtenez la validation git depuis Jenkins
                GIT_COMMIT = sh(returnStdout: true, script: 'git rev-parse HEAD').trim()
                GIT_BRANCH = 'master'
                GIT_REPO = 'GIT_REPO_URL_PLACEHOLDER'
            }
            steps {
                checkout scm
                sh 'npm --version'
                sh 'npm install'
                sh 'grunt dev-setup --no-color'
            }
            // Indiquez à la section build d'utiliser la méthode "publishBuildRecord" pour publier l'enregistrement de génération
            post {
                success {
                    publishBuildRecord gitBranch: "${GIT_BRANCH}", gitCommit: "${GIT_COMMIT}", gitRepo: "${GIT_REPO}", result:"SUCCESS"
                }
                failure {
                    publishBuildRecord gitBranch: "${GIT_BRANCH}", gitCommit: "${GIT_COMMIT}", gitRepo: "${GIT_REPO}", result:"FAIL"
                }
            }
        }
        stage('Unit Test and Code Coverage') {
            steps {
                sh 'grunt dev-test-cov --no-color -f'
            }
            // Indiquez à la section build d'utiliser la méthode "publishTestResult" pour publier les résultats de test
            post {
                always {
                    publishTestResult type:'unittest', fileLocation: './mochatest.json'
                    publishTestResult type:'code', fileLocation: './tests/coverage/reports/coverage-summary.json'
                }
            }
        }
        stage('Deploy to Staging') {
            steps {
                // Envoyez par commande push l'application météo Weather à Bluemix, dans l'espace de transfert
                sh '''
                        echo "CF Login..."
                        cf api https://api.ng.bluemix.net
                        cf login -u $IBM_CLOUD_DEVOPS_CREDS_USR -p $IBM_CLOUD_DEVOPS_CREDS_PSW -o $IBM_CLOUD_DEVOPS_ORG -s staging

                        echo "Deploying...."
                        export CF_APP_NAME="staging-$IBM_CLOUD_DEVOPS_APP_NAME"
                        cf delete $CF_APP_NAME -f
                        cf push $CF_APP_NAME -n $CF_APP_NAME -m 64M -i 1

                        # use "cf icd --create-connection" to enable traceability
                        cf icd --create-connection $IBM_CLOUD_DEVOPS_WEBHOOK_URL $CF_APP_NAME

                        export APP_URL=http://$(cf app $CF_APP_NAME | grep urls: | awk '{print $2}')
                    '''
            }
            // Indiquez à la section build d'utiliser la méthode "publishDeployRecord" pour publier l'enregistrement de déploiement et notifier OTC du statut de l'étape
            post {
                success {
                    publishDeployRecord environment: "STAGING", appUrl: "http://staging-${IBM_CLOUD_DEVOPS_APP_NAME}.mybluemix.net", result:"SUCCESS"
                    // Utilisez la méthode "notifyOTC" pour notifier otc du statut de l'étape
                    notifyOTC stageName: "Deploy to Staging", status: "SUCCESS"
                }
                failure {
                    publishDeployRecord environment: "STAGING", appUrl: "http://staging-${IBM_CLOUD_DEVOPS_APP_NAME}.mybluemix.net", result:"FAIL"
                    // Utilisez la méthode "notifyOTC" pour notifier otc du statut de l'étape
                    notifyOTC stageName: "Deploy to Staging", status: "FAILURE"
                }
            }
        }
        stage('FVT') {
            //Définissez APP_URL comme variable d'environnement pour fvt
            environment {
                APP_URL = "http://staging-${IBM_CLOUD_DEVOPS_APP_NAME}.mybluemix.net"
            }
            steps {
                sh 'grunt fvt-test --no-color -f'
            }
            // Indiquez à la section build d'utiliser la méthode "publishTestResult" pour publier les résultats de test
            post {
                always {
                    publishTestResult type:'fvt', fileLocation: './mochafvt.json', environment: 'STAGING' }
            }
        }
        stage('Gate') {
            steps {
                // Utilisez la méthode "evaluateGate" pour optimiser le jalon IBM Cloud DevOps
                evaluateGate policy: 'Weather App Policy', forceDecision: 'true'
            }
        }
        stage('Deploy to Prod') {
            steps {
                // Envoyez par commande push l'application météo Weather à Bluemix, dans l'espace de production
                sh '''
                        echo "CF Login..."
                        cf api https://api.ng.bluemix.net
                        cf login -u $IBM_CLOUD_DEVOPS_CREDS_USR -p $IBM_CLOUD_DEVOPS_CREDS_PSW -o $IBM_CLOUD_DEVOPS_ORG -s production

                        echo "Deploying...."
                        export CF_APP_NAME="prod-$IBM_CLOUD_DEVOPS_APP_NAME"
                        cf delete $CF_APP_NAME -f
                        cf push $CF_APP_NAME -n $CF_APP_NAME -m 64M -i 1

                        # use "cf icd --create-connection" to enable traceability
                        cf icd --create-connection $IBM_CLOUD_DEVOPS_WEBHOOK_URL $CF_APP_NAME
                        
                        export APP_URL=http://$(cf app $CF_APP_NAME | grep urls: | awk '{print $2}')
                    '''
            }
            // Indiquez à la section build d'utiliser la méthode "publishDeployRecord" pour publier l'enregistrement de déploiement et notifier OTC du statut de l'étape
            post {
                success {
                    publishDeployRecord environment: "PRODUCTION", appUrl: "http://prod-${IBM_CLOUD_DEVOPS_APP_NAME}.mybluemix.net", result:"SUCCESS"
                    // Utilisez la méthode "notifyOTC" pour notifier otc du statut de l'étape
                    notifyOTC stageName: "Deploy to Prod", status: "SUCCESS"
                }
                failure {
                    publishDeployRecord environment: "PRODUCTION", appUrl: "http://prod-${IBM_CLOUD_DEVOPS_APP_NAME}.mybluemix.net", result:"FAIL"
                    // Utilisez la méthode "notifyOTC" pour notifier otc du statut de l'étape
                    notifyOTC stageName: "Deploy to Prod", status: "FAILURE"
                }
            }
        }
    }
}
``` 










