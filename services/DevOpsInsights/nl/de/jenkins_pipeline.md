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

# Integration mit Jenkins Pipeline

Nach dem Hinzufügen von {{site.data.keyword.DRA_full}} zu einer offenen Toolchain und dem Definieren der von dieser Komponente überwachten Richtlinien können Sie sie mit einem Jenkins Pipeline-Projekt integrieren. Sie definieren eine Pipeline in der Jenkins-Webschnittstelle oder in einer *Jenkinsfile*, die Sie in Ihrem Repository für die Quellcodeverwaltung speichern. Sie können Jenkins Pipeline-Projekte über die Jenkins-Webschnittstelle anzeigen und verwalten. 

Das IBM Cloud DevOps-Plug-in für Jenkins integriert Jenkins-Projekte mit Toolchains. Eine *Toolchain* ist eine Gruppe von Toolintegrationen, die Entwicklungs-, Bereitstellungs- und Operationsaufgaben unterstützen. Das Gesamtpotenzial einer Toolchain ist größer als die Summe ihrer einzelnen Toolintegrationen. Offene Toolchains sind Teil des {{site.data.keyword.contdelivery_full}}-Service. Weitere Informationen zum {{site.data.keyword.contdelivery_short}}-Service finden Sie in der [entsprechenden Dokumentation](https://console.ng.bluemix.net/docs/services/ContinuousDelivery/cd_about.html). 

Nach der Installation des IBM Cloud DevOps-Plug-ins können Sie das Jenkins-Projekt so konfigurieren, dass Testergebnisse in {{site.data.keyword.DRA_short}} publiziert werden, die Build-Qualität automatisch an Gates bewertet wird und Ihre Bereitstellungsrisiken überwacht werden. Außerdem können Sie Jobbenachrichtigungen an andere Tools, wie Slack und PagerDuty, in Ihrer Toolchain senden. Damit Sie Ihre Bereitstellungen besser überwachen können, können über die Toolchain Bereitstellungsnachrichten zu Git-Commits und deren zugehörige Git- oder JIRA-Probleme hinzugefügt werden. Zudem können Sie Ihre Bereitstellungen auf der Verbindungsseite der Toolchain anzeigen. 

Das Plug-in stellt Aktionen für den Buildabschluss sowie Befehlszeilenschnittstellen für die Unterstützung der Integration zur Verfügung. {{site.data.keyword.DRA_short}} aggregiert und analysiert die Ergebnisse aus Komponententests, Funktionstests, Codeabdeckungstools und dynamischen Sicherheitsscans, um zu bestimmen, ob Ihr Code den vordefinierten Richtlinien an Gates in Ihrem Bereitstellungsprozess entspricht. Entspricht Ihr Code keiner Richtlinie oder überschreitet Ihr Code eine Richtlinie, wird die Bereitstellung angehalten; dadurch wird verhindert, dass sicherheitsbedenkliche Änderungen freigegeben werden. Sie können {{site.data.keyword.DRA_short}} als Sicherheitsnetz für Ihre Continuous Delivery-Umgebung, als Möglichkeit der Implementierung und Verbesserung der Qualitätsstandards über einen Zeitraum hinweg sowie als Datenvisualisierungstool für Informationen zum Projektstatus verwenden.

Wenn Sie mit Jenkins Pipeline vertraut sind, lesen Sie weiter. Andernfalls lesen Sie die Dokumentation zu [Jenkins Pipeline](https://jenkins.io/doc/book/pipeline/), bevor Sie weitere Schritte ausführen.

## Voraussetzungen
{: #jenkins_prerequisites}

Sie müssen über Zugriff auf den Server verfügen, auf dem ein Jenkins Pipeline-Projekt ausgeführt wird. 

## Eine Toolchain erstellen
{: #jenkins_create}

Bevor Sie {{site.data.keyword.DRA_short}} mit einem Jenkins-Projekt integrieren können, müssen Sie eine Toolchain erstellen. 

1. Rufen Sie zum Erstellen einer Toolchain die [Seite zum Erstellen einer Toolchain](https://console.ng.bluemix.net/devops/create) auf und befolgen Sie die Anweisungen auf dieser Seite. 

2. Nachdem Sie die Toolchain erstellt haben, fügen Sie {{site.data.keyword.DRA_short}} zu dieser Toolchain hinzu. Anweisungen hierzu finden Sie in der [{{site.data.keyword.DRA_short}}-Dokumentation](https://console.ng.bluemix.net/docs/services/DevOpsInsights/index.html). 

## Plug-in installieren
{: #jenkins_install}

Installieren Sie das Plug-in auf dem Jenkins-Server, indem Sie die Serverschnittstelle öffnen und die folgenden Schritte ausführen: 

1. Klicken Sie auf **Jenkins verwalten**.
2. Klicken Sie auf **Plug-ins verwalten**. 
3. Klicken Sie auf die Registerkarte **Verfügbar**.
4. Filtern Sie nach `IBM Cloud DevOps`. 
5. Wählen Sie **IBM Cloud DevOps** aus.
6. Klicken Sie auf **Jetzt herunterladen und nach dem Neustart installieren**. 

Das Plug-in ist nach dem Neustart des Servers verfügbar.   

## Eine Pipeline erstellen
{: #jenkinsfile_create}

Sie definieren Pipelines entweder im Konfigurationsmenü des Jenkins-Projekts oder in einer Jenkinsfile in Ihrem Repository. Erstellen oder öffnen Sie als nächsten Schritt ein Script oder eine Jenkinsfile zur Verwendung mit {{site.data.keyword.DRA_short}}. Sie können dabei das [deklarative](https://jenkins.io/doc/book/pipeline/syntax/#declarative-pipeline) oder das [scriptgesteuerte](https://jenkins.io/doc/book/pipeline/syntax/#scripted-pipeline) Format befolgen.

## Erforderliche Umgebungsvariablen bereitstellen

Öffnen Sie die Pipelinedefinition.  

Fügen Sie in der Definition die folgenden Umgebungsvariablen hinzu. Diese Variablen werden für die Pipeline für die Integration mit {{site.data.keyword.DRA_short}} benötigt.

| Umgebungsvariable        | Definition    |
| ----------------------------|---------------|
| `IBM_CLOUD_DEVOPS_CREDS`    | Bluemix-Berechtigungsnachweise, die Sie mithilfe des Befehls `credentials` in Jenkins definieren. Beispiel: `IBM_CLOUD_DEVOPS_CREDS = credentials('BM_CRED')`. Durch das Festlegen der Variablen mit diesem Befehl werden automatisch zwei weitere Umgebungsvariablen festgelegt: `IBM_CLOUD_DEVOPS_CREDS_USR` und `IBM_CLOUD_DEVOPS_CREDS_PSW` für den Benutzernamen und das Kennwort.   |
| `IBM_CLOUD_DEVOPS_ORG`      | Die Bluemix-Organisation, zu der Ihre Toolchain gehört.     |
| `IBM_CLOUD_DEVOPS_APP_NAME` | Der Name der Anwendung, die Ihre Toolchain bereitstellt.   |
| `IBM_CLOUD_DEVOPS_TOOCLHAIN_ID` | Die ID Ihrer Toolchain. Öffnen Sie die Übersicht der Toolchain und sehen Sie sich die URL an, um die ID zu bestimmen. Das URL-Format der Toolchain ist `https://console.ng.bluemix.net/devops/toolchains/[IHRE_TOOLCHAIN-ID]`.   |
| `IBM_CLOUD_DEVOPS_WEBHOOKURL` | Der Webhook, der Ihnen beim Hinzufügen von Jenkins zur Toolchain bereitgestellt wurde.   |

Weitere Informationen zum Befehl `credentials` finden Sie in der Dokumentation zu [Jenkins Pipeline](https://jenkins.io/doc/pipeline/tour/environment/#credentials-in-the-environment).
{: tip}

Wenn Sie das scriptbasierte Pipelineformat verwenden, verwenden Sie für das Festlegen der Berechtigungsnachweise `withCredentials` und für das Festlegen der Umgebung `withEnv` anstelle von `credentials` bzw. `environment`, die im folgenden Beispiel verwendet werden. Weitere Informationen zu `withCredentials` finden Sie in [der Jenkins-Dokumentation](https://jenkins.io/doc/pipeline/steps/credentials-binding/).
{: tip} 

Diese Umgebungsvariablen und Berechtigungsnachweise werden vom IBM Cloud DevOps-Plug-in für die Interaktion mit DevOps Insights verwendet. In diesem Beispiel werden sie im deklarativen Pipelineformat festgelegt.  

```
environment {
        IBM_CLOUD_DEVOPS_CREDS = credentials('BM_CRED')
        IBM_CLOUD_DEVOPS_ORG = 'dlatest'
        IBM_CLOUD_DEVOPS_APP_NAME = 'Weather-App'
        IBM_CLOUD_DEVOPS_TOOLCHAIN_ID = '1111111-aaaa-2222-bbbb-333333333'
        IBM_CLOUD_DEVOPS_WEBHOOK_URL = 'https://jenkins:5a55555a-a555-5555-5555-a555aa55a555:55555555-5555-5555-5555-555555555555@devops-api.ng.bluemix.net/v1/toolint/messaging/webhook/publish'
    }
```


## Cloud DevOps-Schritte hinzufügen
Das Cloud DevOps-Plug-in fügt vier Schritte zu Jenkins-Pipelines hinzu. Sie können diese Schritte in Ihren Pipelines für die Interaktion mit DevOps Insights verwenden. 

* `publishBuildRecord`, mit dem Buildinformationen in DevOps Insights publiziert werden.
* `publishTestResult`, mit dem Testergebnisse in DevOps Insights publiziert werden.
* `publishDeployRecord`, mit dem Bereitstellungsdatensätze in DevOps Insights publiziert werden.
* `evaluateGate`, mit dem DevOps Insights-Richtlinien durchgesetzt werden. 

Fügen Sie die Schritte zu Ihrer Pipelinedefinition an den Stellen hinzu, an denen sie ausgeführt werden sollen. Beispielsweise können Sie Testergebnisse nach dem Ausführen eines Tests hochladen und dann diese Ergebnisse nach dem Hochladen an einem Gate bewerten.  

### Builddatensätze publizieren

Publizieren Sie Builddatensätze mit dem Schritt `publishBuildRecord`. Für diesen Schritt sind vier Parameter erforderlich.

| Parameter        | Definition    |
| ----------------------------|---------------|
| `gitBranch`    | Der Name des Git-Branch, den der Build verwendet.  |
| `gitCommit`      | Die Git-Commit-ID, die der Build verwendet.    |
| `gitRepo` | Die URL des Git-Repositorys.   |
| `result` | Das Ergebnis der Buildstufe. Der Wert lautet `SUCCESS` oder `FAIL`.   |

Dieses Beispiel veranschaulicht die Verwendung dieser Parameter in einem Befehl: 

```
publishBuildRecord gitBranch: "${GIT_MASTER}", gitCommit: "${GIT_COMMIT}", gitRepo: "https://github.com/username/reponame", result:"SUCCESS"
```

Jenkins Pipeline stellt Git-Informationen nicht in Form von Umgebungsvariablen bereit. Sie können die Git-Commit-ID mithilfe des Befehls `sh(returnStdout: true, script: 'git rev-parse HEAD').trim()` abrufen.
{: tip}

### Testergebnisse publizieren
Publizieren Sie Builddatensätze mit dem Schritt `publishTestResult`. Für diesen Schritt sind zwei Parameter erforderlich.

| Parameter        | Definition    |
| ----------------------------|---------------|
| `type`    | Der Typ des Testergebnisses. Der Wert für diesen Parameter muss `unittest` für Komponententests, `fvt` für Funktionstests oder `code` für Codeabdeckungstests sein.  |
| `fileLocation`      | Die Speicherposition der Testergebnisdatei.    |

Das folgende Beispiel veranschaulicht die Verwendung dieser Parameter in Befehlen. Mit dem ersten Befehl werden Mocha-Komponententestergebnisse publiziert. Mit dem zweiten Befehl werden Testergebnisse für die Codeabdeckung publiziert.  

```
publishTestResult type:'unittest', fileLocation: './mochatest.json'
publishTestResult type:'code', fileLocation: './tests/coverage/reports/coverage-summary.json'
```

### Bereitstellungsdatensätze publizieren

Publizieren Sie Bereitstellungsdatensätze mit dem Schritt `publishDeployRecord`. Für diesen Schritt sind zwei Parameter erforderlich. Es ist auch ein optionaler Parameter möglich. 

| Parameter        | Definition    |
| ----------------------------|---------------|
| `environment`    | Die Umgebung, in der die App bereitgestellt wurde. Damit DevOps Insights ordnungsgemäß funktioniert, müssen Sie eine Umgebung als `STAGING` und eine andere Umgebung als `PRODUCTION` angeben. |
| `result`      | Das Ergebnis der Buildstufe. Der Wert sollte `SUCCESS` oder `FAIL` lauten.    |
| `appUrl`      | *Optional*: Die URL für den Zugriff auf Ihre Anwendung.    |

Das folgende Beispiel veranschaulicht die Verwendung dieser Parameter in Befehlen. Mit dem ersten Befehl wird der Bereitstellungsdatensatz für eine Staging-Umgebung publiziert. Mit dem zweiten Befehl wird der Bereitstellungsdatensatz für eine Produktionsumgebung publiziert. 

```
publishDeployRecord environment: "STAGING", appUrl: "http://staging-Weather-App.mybluemix.net", result:"SUCCESS"
publishDeployRecord environment: "PRODUCTION", appUrl: "http://Weather-App.mybluemix.net", result:"SUCCESS"
```

### Gates hinzufügen

Fügen Sie mithilfe des Befehls `evaluateGate` Gates zu Ihrer Pipeline hinzu. Gates setzen DevOps Insights-Richtlinien durch, mit denen Testanforderungen für die Hochstufung von Builds festgelegt werden. 

Für diesen Schritt ist ein Parameter erforderlich. Es ist auch ein optionaler Parameter möglich. 

| Parameter        | Definition    |
| ----------------------------|---------------|
| `policy`    | Der Name der Richtlinie, die das Gate implementiert. Der Name der Richtlinie wird in DevOps Insights definiert. |
| `forceDecision`      | *Optional*: Gibt an, ob die Pipeline in Abhängigkeit der Gate-Entscheidung gestoppt wird oder nicht. Legen Sie diesen Parameter auf `true` fest, um die Ausführung der Pipeline zu stoppen, falls das Gate fehlschlägt. Legen Sie den Wert `false` fest, wenn die Pipeline nach dem Fehlschlagen des Gates weiter ausgeführt werden soll. Der Standardwert hierfür ist `false`.     |

Das folgende Beispiel veranschaulicht die Verwendung dieser Parameter in einem Befehl. Mit diesem Befehl wird die Pipeline unabhängig davon, wie die Gate-Entscheidung ist, weiter ausgeführt. 

```
evaluateGate policy: 'Weather App Policy', forceDecision: 'true'
```

### Kommunikation mit Toolchains

Senden Sie den Pipelinestatus mithilfe des Befehls `notifyOTC` an Bluemix-Toolchains. Weitere Informationen zur Integration von Jenkins mit Toolchains [finden Sie in der Dokumentation](https://console.ng.bluemix.net/docs/services/ContinuousDelivery/toolchains_integrations.html#jenkins). Sie können die Schritte 6d bis 6f ignorieren, da sie nur für unformatierte Jenkins-Projekte gelten.

Für diesen Schritt sind zwei Parameter erforderlich. Darüber hinaus ist ein optionaler Parameter möglich.  

| Parameter        | Definition    |
| ----------------------------|---------------|
| `stageName`    | Der Stufenname der aktuellen Pipeline. |
| `status`    | Der Stufenstatus der aktuellen Pipeline. Durch die Verwendung von `SUCCESS`, `FAILURE` oder `ABORTED` wird automatisch eine farbige Hervorhebung in Slack angewendet.  |
| `webhookUrl`      | *Optional*: Die Webhook-URL, die auf der Jenkins-Kachel der Toolchain angezeigt wird. Wenn Sie diesen Parameter einschließen, überschreibt sein Wert den Wert der Umgebungsvariablen `IBM_CLOUD_DEVOPS_WEBHOOKURL`.   |

Die folgenden Beispiele veranschaulichen die Verwendung des Schritts `notifyOTC` sowohl in deklarativen als auch in scriptbasierten Pipelinedefinitionen.

#### Deklarative Pipeline
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

#### Scriptbasierte Pipeline
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

In beiden Beispielen wird die Toolchain-Webhook-URL nur im Falle eines Fehlers überschrieben. 

## Verfolgbarkeit bei Toolchainintegrationen sicherstellen

Konfigurieren Sie die Jenkins-Umgebung für die Integration mit der Bluemix-Toolchain, indem Sie die entsprechenden Anweisungen in [der Bluemix-Dokumentation](https://console.ng.bluemix.net/docs/services/ContinuousDelivery/toolchains_integrations.html#jenkins) befolgen. Sie können die Schritte 6d bis 6f ignorieren, da sie nur für unformatierte Jenkins-Projekte gelten. 

Durch die Integration mit einer Toolchain stehen Ihnen verschiedene Möglichkeiten für eine durchgängige Verfolgbarkeit und Bereitstellungszuordnung zur Verfügung. Nachdem Sie die Integrationsanweisungen implementiert haben, fügen Sie den Befehl `cf icd --create-connection $IBM_CLOUD_DEVOPS_WEBHOOK_URL $CF_APP_NAME` nach Ihren Bereitstellungsschritten hinzu. Mit diesem Befehl wird eine Verbindung der Jenkins-Integration mit einer App hergestellt, die in Bluemix ausgeführt wird. 

Dieses Beispiel veranschaulicht einen vollständigen Bereitstellungsschritt. Der letzte Befehl lautet `cf icd --create-connection`. 

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

Wie in der Dokumentation zur Jenkins-Integration beschrieben, müssen die Plug-ins für die Cloud Foundry-CLI und die CloudFoundry-ICD auf dem Jenkins-Server installiert sein. Außerdem müssen Sie sich zum Herstellen einer Verbindung vom Server aus bei Bluemix anmelden.

## Beispiel für eine deklarative Pipeline

Dieses Beispiel zeigt eine vollständige Pipeline, die als deklarative Jenkinsfile definiert ist. 

```
#!groovy
/*
    Dies ist eine Beispiel-Jenkinsfile für die Wetter-App, bei der es sich um eine Node.js-Anwendung handelt, die über Komponenten-, Funktions- und Codeabdeckungstests verfügt, für Staging- und Produktionsumgebungen bereitgestellt wird und IBM Cloud DevOps-Gates verwendet.
    Dies wird als Beispiel für die Verwendung des Plug-ins in der Jenkinsfile verwendet.
    Sie müssen die erforderlichen 4 Umgebungsvariablen angeben und können dann die 4 verschiedenen Methoden
    für die Stufen 'Build/Test/Deploy' und das Gate verwenden.
 */
pipeline {
    agent any
    environment {
        // Sie müssen zunächst 4 erforderliche Umgebungsvariablen angeben, welche für die folgenden IBM Cloud DevOps-Schritte verwendet werden.
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
                // get git commit from Jenkins
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
            // Buildabschlussabschnitt für die Verwendung der Methode "publishBuildRecord" zum Publizieren von Builddatensätzen
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
            // Buildabschlussabschnitt für die Verwendung der Methode "publishTestResult" zum Publizieren des Testergebnisses
            post {
                always {
                    publishTestResult type:'unittest', fileLocation: './mochatest.json'
                    publishTestResult type:'code', fileLocation: './tests/coverage/reports/coverage-summary.json'
                }
            }
        }
        stage('Deploy to Staging') {
            steps {
                // Wetter-App mit Push-Operation an Bluemix übertragen, Staging-Bereich
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
            // Buildabschlussabschnitt für die Verwendung der Methode "publishDeployRecord" zum Publizieren des Bereitstellungsdatensatzes und Benachrichtigen von OTC über den Stufenstatus
            post {
                success {
                    publishDeployRecord environment: "STAGING", appUrl: "http://staging-${IBM_CLOUD_DEVOPS_APP_NAME}.mybluemix.net", result:"SUCCESS"
                    // use "notifyOTC" method to notify otc of stage status
                    notifyOTC stageName: "Deploy to Staging", status: "SUCCESS"
                }
                failure {
                    publishDeployRecord environment: "STAGING", appUrl: "http://staging-${IBM_CLOUD_DEVOPS_APP_NAME}.mybluemix.net", result:"FAIL"
                    // use "notifyOTC" method to notify otc of stage status
                    notifyOTC stageName: "Deploy to Staging", status: "FAILURE"
                }
            }
        }
        stage('FVT') {
            //APP_URL als Umgebungsvariable für fvt festlegen
            environment {
                APP_URL = "http://staging-${IBM_CLOUD_DEVOPS_APP_NAME}.mybluemix.net"
            }
            steps {
                sh 'grunt fvt-test --no-color -f'
            }
            // Buildabschlussabschnitt für die Verwendung der Methode "publishTestResult" zum Publizieren des Testergebnisses
            post {
                always {
                    publishTestResult type:'fvt', fileLocation: './mochafvt.json', environment: 'STAGING'
                }
            }
        }
        stage('Gate') {
            steps {
                // Verwendung der Methode "evaluateGate" zur Nutzung des IBM Cloud DevOps-Gates
                evaluateGate policy: 'Weather App Policy', forceDecision: 'true'
            }
        }
        stage('Deploy to Prod') {
            steps {
                // Wetter-App mit Push-Operation an Bluemix übertragen, Produktionsbereich
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
            // Buildabschlussabschnitt für die Verwendung der Methode "publishDeployRecord" zum Publizieren des Bereitstellungsdatensatzes und Benachrichtigen von OTC über den Stufenstatus
            post {
                success {
                    publishDeployRecord environment: "PRODUCTION", appUrl: "http://prod-${IBM_CLOUD_DEVOPS_APP_NAME}.mybluemix.net", result:"SUCCESS"
                    // use "notifyOTC" method to notify otc of stage status
                    notifyOTC stageName: "Deploy to Prod", status: "SUCCESS"
                }
                failure {
                    publishDeployRecord environment: "PRODUCTION", appUrl: "http://prod-${IBM_CLOUD_DEVOPS_APP_NAME}.mybluemix.net", result:"FAIL"
                    // use "notifyOTC" method to notify otc of stage status
                    notifyOTC stageName: "Deploy to Prod", status: "FAILURE"
                }
            }
        }
    }
}
``` 










