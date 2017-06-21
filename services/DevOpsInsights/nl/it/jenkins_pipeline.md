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

# Integrazione con la pipeline Jenkins

Dopo aver aggiunto {{site.data.keyword.DRA_full}} a una toolchain aperta e definito le politiche che monitora, puoi integrarlo con un progetto della pipeline Jenkins. Definisci una pipeline nell'interfaccia web Jenkins o in un *Jenkinsfile* che archivi nel tuo repository di controllo dell'origine. Puoi visualizzare e gestire i progetti della pipeline Jenkins dall'interfaccia web Jenkins. 

Il plugin IBM Cloud DevOps per Jenkins integra i progetti Jenkins con le toolchain. Una *toolchain* è una serie di integrazioni dello strumento che supporta le attività di operazioni, sviluppo e distribuzione. La potenza collettiva di una toolchain è superiore alla somma delle relative integrazioni dello strumento. Le toolchain aperte fanno parte del servizio {{site.data.keyword.contdelivery_full}}. Per ulteriori informazioni sul servizio {{site.data.keyword.contdelivery_short}}, consulta [la sua documentazione](https://console.ng.bluemix.net/docs/services/ContinuousDelivery/cd_about.html). 

Dopo aver installato il plugin IBM Cloud DevOps, puoi configurare il tuo progetto Jenkins per pubblicare i risultati del test in {{site.data.keyword.DRA_short}}, la qualità di build viene valutata automaticamente ai gate e tracciato il tuo rischio di distribuzione. Puoi anche inviare notifiche del lavoro ad altri strumenti nella tua toolchain, come Slack e PagerDuty. Per aiutarti a tracciare le distribuzioni, la toolchain può aggiungere i messaggi di distribuzione ai commit Git e ai relativi problemi Git e JIRA. Puoi anche visualizzare le distribuzioni nella pagina delle connessioni della toolchain. 

Il plugin fornisce le azioni di post creazione e le CLI per supportare l'integrazione. {{site.data.keyword.DRA_short}} aggrega e analizza i risultati dagli strumenti di verifica di unità, di test funzionali, di copertura del codice, delle scansioni del codice di sicurezza statico per determinare se il tuo codice soddisfa le politiche predefinite nei gate nel tuo processo di distribuzione. Se il tuo codice non soddisfa o supera una politica, la distribuzione viene arrestata, per prevenire che vengano rilasciati dei rischi. Puoi utilizzare {{site.data.keyword.DRA_short}} come una rete di sicurezza per il tuo ambiente di fornitura continua, come un modo per implementare e migliorare gli standard nel tempo e come uno strumento di visualizzazione dei dati per aiutarti nella comprensione dello stato del tuo progetto.

Se hai dimestichezza con la pipeline Jenkins, continua a leggere. Altrimenti, [consulta la documentazione della pipeline Jenkins](https://jenkins.io/doc/book/pipeline/) prima di continuare.

## Prerequisiti
{: #jenkins_prerequisites}

Devi avere accesso a un server in esecuzione in un progetto della pipeline Jenkins. 

## Creazione di una toolchain
{: #jenkins_create}

Prima di poter integrare {{site.data.keyword.DRA_short}} con un progetto Jenkins, devi creare una toolchain. 

1. Per creare una toolchain, passa alla [Pagina Crea una toolchain](https://console.ng.bluemix.net/devops/create) e segui le istruzioni in tale pagina. 

2. Dopo aver creato la toolchain, aggiungi {{site.data.keyword.DRA_short}} ad essa. Per istruzioni, consulta la [documentazione {{site.data.keyword.DRA_short}}](https://console.ng.bluemix.net/docs/services/DevOpsInsights/index.html). 

## Installazione del plugin
{: #jenkins_install}

Installa il plugin sul tuo server Jenkins aprendo l'interfaccia server e attenendoti alla seguente procedura:

1. Fai clic su **Manage Jenkins**.
2. Fai clic su **Manage Plugins**. 
3. Fai clic sulla scheda **Available**
4. Imposta un filtro per `IBM Cloud DevOps`. 
5. Seleziona **IBM Cloud DevOps**.
6. Fai clic su **Download now and install after restart**. 

Il plugin è disponibile dopo i riavvii del server.  

## Creazione di una pipeline
{: #jenkinsfile_create}

Definisci le pipeline nel menu di configurazione del progetto Jenkins o in un Jenkinsfile nel tuo repository. Per procedere, crea o apri uno script o un Jenkinsfile da utilizzare con {{site.data.keyword.DRA_short}}. Puoi seguire i formati [dichiarativa](https://jenkins.io/doc/book/pipeline/syntax/#declarative-pipeline) o [con script](https://jenkins.io/doc/book/pipeline/syntax/#scripted-pipeline).

## Esposizione delle variabili di ambiente richieste

Apri la definizione della pipeline. 

Nella definizione, aggiungi le seguenti variabili di ambiente. Queste variabili sono obbligatorie per la pipeline per l'integrazione con {{site.data.keyword.DRA_short}}.

| Variabile di ambiente        | Definizione    |
| ----------------------------|---------------|
| `IBM_CLOUD_DEVOPS_CREDS`    | Le credenziali Bluemix che definisci in Jenkins utilizzando il comando `credentials`. Ad esempio, `IBM_CLOUD_DEVOPS_CREDS = credentials('BM_CRED')`. La configurazione della variabile con questo comando imposta due variabili di ambiente automaticamente: `IBM_CLOUD_DEVOPS_CREDS_USR` e `IBM_CLOUD_DEVOPS_CREDS_PSW` per il nome utente e la password.  |
| `IBM_CLOUD_DEVOPS_ORG`      | L'organizzazione Bluemix a cui appartiene la tua toolchain.     |
| `IBM_CLOUD_DEVOPS_APP_NAME` | Il nome dell'applicazione distribuita dalla tua toolchain.   |
| `IBM_CLOUD_DEVOPS_TOOCLHAIN_ID` | L'ID della tua toolchain. Apri la panoramica della toolchain e visualizza l'URL per determinare l'ID. Il formato dell'URL della toolchain è: `https://console.ng.bluemix.net/devops/toolchains/[YOUR_TOOLCHAIN_ID]`.   |
| `IBM_CLOUD_DEVOPS_WEBHOOKURL` | Il webhook che ti è stato fornito quando hai aggiunto Jenkins alla tua toolchain.   |

Per ulteriori informazioni sul comando `credentials`, consulta la [documentazione della pipeline Jenkins](https://jenkins.io/doc/pipeline/tour/environment/#credentials-in-the-environment).
{: tip}

Se stai utilizzando un formato della pipeline con script, imposta le tue credenziali con `withCredentials` e il tuo ambiente con `withEnv` invece di `credentials` e `environment`, che sono stati utilizzati nel seguente esempio. Per ulteriori informazioni su `withCredentials`, consulta [la documentazione di Jenkins](https://jenkins.io/doc/pipeline/steps/credentials-binding/).
{: tip} 

Queste variabili di ambiente e credenziali sono utilizzate dal plugin IBM Cloud DevOps per interagire con DevOps Insights. In questo esempio, sono impostate nel formato della pipeline dichiarativa. 

```
environment {
        IBM_CLOUD_DEVOPS_CREDS = credentials('BM_CRED')
        IBM_CLOUD_DEVOPS_ORG = 'dlatest'
        IBM_CLOUD_DEVOPS_APP_NAME = 'Weather-App'
        IBM_CLOUD_DEVOPS_TOOLCHAIN_ID = '1111111-aaaa-2222-bbbb-333333333'
        IBM_CLOUD_DEVOPS_WEBHOOK_URL = 'https://jenkins:5a55555a-a555-5555-5555-a555aa55a555:55555555-5555-5555-5555-555555555555@devops-api.ng.bluemix.net/v1/toolint/messaging/webhook/publish'
    }
```


## Aggiunta delle fasi Cloud DevOps
Il plugin Cloud DevOps aggiunge quattro fasi alle pipeline Jenkins per il tuo utilizzo. Utilizza queste fasi nelle tue pipeline per interagire con DevOps Insights. 

* `publishBuildRecord`, che pubblica le informazioni di build in DevOps Insights
* `publishTestResult`, che pubblica i risultati del test in DevOps Insights
* `publishDeployRecord`, che pubblica i record di distribuzione in DevOps Insights
* `evaluateGate`, che definisce le politiche DevOps Insights 

Aggiungi queste fasi alla tua definizione della pipeline ovunque hai bisogno di eseguirle. Ad esempio, potresti caricare i risultati del test dopo che hai eseguito un test e quindi valutare questi risultati in un gate dopo che sono stati caricati. 

### Pubblicazione dei record di build

Pubblica i record di build con la fase `publishBuildRecord`. Questa fase richiede quattro parametri.

| Parametro        | Definizione    |
| ----------------------------|---------------|
| `gitBranch`    | Il nome del ramo Git che utilizza la build.  |
| `gitCommit`      | L'ID del commit Git che utilizza la build.    |
| `gitRepo` | L'URL del repository Git.   |
| `result` | Il risultato della fase di build. Il valore è `SUCCESS` o `FAIL`.   |

Questo esempio mostra questi parametri in un comando:

```
publishBuildRecord gitBranch: "${GIT_MASTER}", gitCommit: "${GIT_COMMIT}", gitRepo: "https://github.com/username/reponame", result:"SUCCESS"
```

La pipeline Jenkins non espone le informazioni Git come le variabili di ambiente. Puoi ottenere l'ID del commit Git utilizzando il comando `sh(returnStdout: true, script: 'git rev-parse HEAD').trim()`.
{: tip}

### Pubblicazione dei risultati del test
Pubblica i record di build con la fase `publishTestResult`. Questa fase richiede due parametri.

| Parametro        | Definizione    |
| ----------------------------|---------------|
| `type`    | Il tipo di risultato del test. Questo valore deve essere `unittest` per i test di unità, `fvt` per i test di verifica funzionale o `code` per i test di copertura del codice.  |
| `fileLocation`      | L'ubicazione del file del risultato del test.    |

Il seguente esempio mostra questi parametri nei comandi. Il primo comando pubblica i risultati del test di unità Mocha. Il secondo comando pubblica i risultati del test di copertura del codice. 

```
publishTestResult type:'unittest', fileLocation: './mochatest.json'
publishTestResult type:'code', fileLocation: './tests/coverage/reports/coverage-summary.json'
```

### Pubblicazione dei record di distribuzione

Pubblica i record di distribuzione con la fase `publishDeployRecord`. Questa fase richiede due parametri. Accetta anche un parametro facoltativo. 

| Parametro        | Definizione    |
| ----------------------------|---------------|
| `environment`    | L'ambiente a cui distribuisci la tua applicazione. Per un corretto funzionamento di DevOps, devi definire un ambiente come `STAGING` e un altro come `PRODUCTION`. |
| `result`      | Il risultato della fase di build. Il valore dovrebbe essere `SUCCESS` o `FAIL`.    |
| `appUrl`      | *Facoltativo*: l'URL utilizzato per accedere alla tua applicazione.    |

Il seguente esempio mostra questi parametri nei comandi. Il primo comando pubblica il record di distribuzione per un ambiente di preparazione. Il secondo comando pubblica il record di distribuzione per un ambiente di produzione.

```
publishDeployRecord environment: "STAGING", appUrl: "http://staging-Weather-App.mybluemix.net", result:"SUCCESS"
publishDeployRecord environment: "PRODUCTION", appUrl: "http://Weather-App.mybluemix.net", result:"SUCCESS"
```

### Aggiunta di gate

Aggiungi i gate alla tua pipeline utilizzando il comando `evaluateGate`. I gate applicano le politiche DevOps Insights, che impostano i requisiti del test per la promozione della build. 

Questa fase richiede un parametro. Accetta anche un parametro facoltativo. 

| Parametro        | Definizione    |
| ----------------------------|---------------|
| `policy`    | Il nome della politica che implementa il gate. Il nome della politica viene definito in DevOps Insights. |
| `forceDecision`      | *Facoltativo*: se la pipeline viene arrestata o meno a seconda della decisione del gate. Imposta questo parametro su `true` per arrestare la pipeline dall'esecuzione se il gate ha esito negativo. Impostalo su `false` per consentire alla pipeline di continuare dopo un esito negativo del gate. Per impostazione predefinita, il valore è `false`.     |

Il seguente esempio mostra questi parametri in un comando. In questo comando, la pipeline continua l'esecuzione indipendentemente dalla decisione del gate. 

```
evaluateGate policy: 'Weather App Policy', forceDecision: 'true'
```

### Comunicazione con le toolchain

Invia lo stato della pipeline alle toolchain Bluemix utilizzando il comando `notifyOTC`. Per ulteriori informazioni sull'integrazione di Jenkins con le toolchain, [consulta la documentazione](https://console.ng.bluemix.net/docs/services/ContinuousDelivery/toolchains_integrations.html#jenkins). Puoi ignorare i passi da 6d a 6f, dato che si applicano solo ai progetti Jenkins a formato libero.

Questa fase richiede due parametri e può anche utilizzarne uno facoltativo. 

| Parametro        | Definizione    |
| ----------------------------|---------------|
| `stageName`    | Il nome della fase della pipeline corrente. |
| `status`    | Lo stato della fase della pipeline corrente. Utilizzando `SUCCESS`, `FAILURE` o `ABORTED` sarà attivata automaticamente l'evidenziazione del colore in Slack.  |
| `webhookUrl`      | *Facoltativo*: l'URL del webhook visualizzato nel tile Jenkins della tua toolchain. Se includi questo parametro, il suo valore sovrascrive quello della variabile di ambiente `IBM_CLOUD_DEVOPS_WEBHOOKURL`.   |

I seguenti esempi illustrano come utilizzare la fase `notifyOTC` sia nella definizione della pipeline dichiarativa che in quella con script.

#### Pipeline dichiarativa
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

#### Pipeline con script
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

In entrambi gli esempi, l'URL del webhook della toolchain viene sovrascritto solo in caso di malfunzionamento. 

## Garantire la tracciabilità tra le integrazioni toolchain

Configura il tuo ambiente Jenkins per l'integrazione con la tua toolchain Bluemix seguendo le istruzioni nei [Documenti Bluemix](https://console.ng.bluemix.net/docs/services/ContinuousDelivery/toolchains_integrations.html#jenkins). Puoi ignorare i passi da 6d a 6f, dato che si applicano solo ai progetti Jenkins a formato libero.

L'integrazione con una toolchain ti fornisce la tracciabilità end-to-end e l'associazione della distribuzione. Dopo aver eseguito le istruzioni di integrazione, aggiungi il comando `cf icd --create-connection $IBM_CLOUD_DEVOPS_WEBHOOK_URL $CF_APP_NAME` dopo le fasi di distribuzione. Questo comando collega la tua integrazione Jenkins a un'applicazione in esecuzione su Bluemix. 

Questo esempio mostra una fase di distribuzione completa. L'ultimo comando è `cf icd --create-connection`. 

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

Come descritto nella documentazione di integrazione di Jenkins, sul tuo server Jenkins devono essere installati i plugin CLI CloudFoundry e ICD CloudFoundry. Hai anche bisogno di accedere a Bluemix dal server da collegare.

## Esempio di una pipeline dichiarativa

Questo esempio mostra una piepline completa definita come un Jenkinsfile dichiarativo. 

```
#!groovy
/*
    Questo è un esempio di un file Jenkins per Weather App, che è un'applicazione node.js con un test dell'unità e i test
    di verifica funzionale e copertura del codice, che distribuisce nell'ambiente di produzione e di preparazione e utilizza il gate IBM Cloud DevOps.
    Utilizziamo questo esempio per sfruttare il nostro plugin nel Jenkinsfile
    Sostanzialmente, devi specificare le 4 variabili di ambiente necessarie e quindi sarai in grado di utilizzare 4 metodi differenti per
    la fase di creazione/verifica/distribuzione al gate
 */
pipeline {
    agent any
    environment {
        // Devi prima specificare le 4 variabili di ambiente richieste, che saranno utilizzate nelle seguenti fasi IBM Cloud DevOps
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
                // ottieni il commit git da Jenkins
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
            // sezione di post creazione per utilizzare il metodo "publishBuildRecord" per pubblicare i record di build
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
            // sezione di post creazione per utilizzare il metodo "publishTestResult" per pubblicare il risultato del test
            post {
                always {
                    publishTestResult type:'unittest', fileLocation: './mochatest.json'
                    publishTestResult type:'code', fileLocation: './tests/coverage/reports/coverage-summary.json'
                }
            }
        }
        stage('Deploy to Staging') {
            steps {
                // Trasmetti la Weather App a Bluemix, spazio di preparazione
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
            // sezione di post creazione per utilizzare il metodo "publishDeployRecord" per pubblicare il record di distribuzione e notificare a OTC lo stato della fase
            post {
                success {
                    publishDeployRecord environment: "STAGING", appUrl: "http://staging-${IBM_CLOUD_DEVOPS_APP_NAME}.mybluemix.net", result:"SUCCESS"
                    // utilizza il metodo "notifyOTC" per notificare a otc lo stato della fase
                    notifyOTC stageName: "Deploy to Staging", status: "SUCCESS"
                }
                failure {
                    publishDeployRecord environment: "STAGING", appUrl: "http://staging-${IBM_CLOUD_DEVOPS_APP_NAME}.mybluemix.net", result:"FAIL"
                    // utilizza il metodo "notifyOTC" per notificare a otc lo stato della fase
                    notifyOTC stageName: "Deploy to Staging", status: "FAILURE"
                }
            }
        }
        stage('FVT') {
            //imposta APP_URL come la variabile di ambiente per fvt
            environment {
                APP_URL = "http://staging-${IBM_CLOUD_DEVOPS_APP_NAME}.mybluemix.net"
            }
            steps {
                sh 'grunt fvt-test --no-color -f'
            }
            // sezione di post creazione per utilizzare il metodo "publishTestResult" per pubblicare il risultato del test
            post {
                always {
                    publishTestResult type:'fvt', fileLocation: './mochafvt.json', environment: 'STAGING'
                }
            }
        }
        stage('Gate') {
            steps {
                // utilizza il metodo "evaluateGate" per utilizzare il gate IBM Cloud DevOps
                evaluateGate policy: 'Weather App Policy', forceDecision: 'true'
            }
        }
        stage('Deploy to Prod') {
            steps {
                // Trasmetti la Weather App a Bluemix, spazio di produzione
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
            // sezione di post creazione per utilizzare il metodo "publishDeployRecord" per pubblicare il record di distribuzione e notificare a OTC lo stato della fase
            post {
                success {
                    publishDeployRecord environment: "PRODUCTION", appUrl: "http://prod-${IBM_CLOUD_DEVOPS_APP_NAME}.mybluemix.net", result:"SUCCESS"
                    // utilizza il metodo "notifyOTC" per notificare a otc lo stato della fase
                    notifyOTC stageName: "Deploy to Prod", status: "SUCCESS"
                }
                failure {
                    publishDeployRecord environment: "PRODUCTION", appUrl: "http://prod-${IBM_CLOUD_DEVOPS_APP_NAME}.mybluemix.net", result:"FAIL"
                    // utilizza il metodo "notifyOTC" per notificare a otc lo stato della fase
                    notifyOTC stageName: "Deploy to Prod", status: "FAILURE"
                }
            }
        }
    }
}
``` 










