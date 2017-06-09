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

# 與 Jenkins 管線整合

將 {{site.data.keyword.DRA_full}} 新增至開放式工具鏈並定義它所監視的原則之後，可將它與「Jenkins 管線」專案整合。您可以在 Jenkins Web 介面中，或是儲存在來源控制儲存庫內的 *Jenkinsfile* 中定義管線。您可以從 Jenkins Web 介面來檢視及管理「Jenkins 管線」專案。 

適用於 Jenkins 的 IBM Cloud DevOps 外掛程式會將 Jenkins 專案與工具鏈整合。*工具鏈* 是一組支援開發、部署及操作作業的工具整合。工具鏈的群體力量大於其個別工具整合的總和。開放式工具鏈是 {{site.data.keyword.contdelivery_full}} 服務的一部分。若要進一步瞭解 {{site.data.keyword.contdelivery_short}} 服務，請參閱[其文件](https://console.ng.bluemix.net/docs/services/ContinuousDelivery/cd_about.html)。 

安裝 IBM Cloud DevOps 外掛程式之後，您可以配置 Jenkins 專案，以將測試結果發佈至 {{site.data.keyword.DRA_short}}、自動在閘道評估建置品質，以及追蹤佈署風險。您也可以將工作通知傳送給工具鏈中的其他工具，例如 Slack 和 PagerDuty。為了協助您追蹤部署，工具鏈可以將部署訊息新增至 Git 確定及其相關 Git 或 JIRA 問題。您也可以在工具鏈的「連線」頁面上檢視您的部署。 

外掛程式提供後建置動作和 CLI 來支援整合。{{site.data.keyword.DRA_short}} 會聚集並分析單元測試、功能測試、程式碼涵蓋面工具、靜態安全程式碼掃描及動態安全程式碼掃描的結果，以在部署程序中判斷您的程式碼是否符合閘道的預先定義原則。如果您的程式碼不符合或超出原則，則會中止部署，以防止釋出有風險的變更。您可以使用 {{site.data.keyword.DRA_short}} 當作持續交付環境的安全網、持續實作與改善品質標準的方式，以及協助您瞭解專案性能的資料視覺化工具。

如果您熟悉 Jenkins Pipeline，請繼續閱讀。否則，[請先參閱 Jenkins Pipeline 文件](https://jenkins.io/doc/book/pipeline/)，然後再繼續進行。

## 必要條件
{: #jenkins_prerequisites}

您必須能夠存取執行「Jenkins 管線」專案的伺服器。 

## 建立工具鏈
{: #jenkins_create}

您必須先建立工具鏈，才能將 {{site.data.keyword.DRA_short}} 與 Jenkins 專案整合。 

1. 若要建立工具鏈，請移至[「建立工具鏈」頁面](https://console.ng.bluemix.net/devops/create)，然後遵循該頁面上的指示。 

2. 建立工具鏈之後，將 {{site.data.keyword.DRA_short}} 新增至此工具鏈。如需相關指示，請參閱 [{{site.data.keyword.DRA_short}} 文件](https://console.ng.bluemix.net/docs/services/DevOpsInsights/index.html)。 

## 安裝外掛程式
{: #jenkins_install}

開啟伺服器介面並遵循下列步驟，在 Jenkins 伺服器上安裝外掛程式：

1. 按一下**管理 Jenkins**。
2. 按一下**管理外掛程式**。 
3. 按一下**可用的**標籤。
4. 過濾 `IBM Cloud DevOps`。 
5. 選取 **IBM Cloud DevOps**。
6. 按一下**立即下載並在重新啟動之後安裝**。 

伺服器重新啟動之後即可使用外掛程式。  

## 建立管線
{: #jenkinsfile_create}

您可以在 Jenkins 專案配置功能表中，或是在儲存庫內的 Jenkinsfile 中定義管線。若要繼續進行，請建立或開啟 Script 或 Jenkinsfile 來與 {{site.data.keyword.DRA_short}} 搭配使用。您可以採用[宣告式](https://jenkins.io/doc/book/pipeline/syntax/#declarative-pipeline)或 [Script 化](https://jenkins.io/doc/book/pipeline/syntax/#scripted-pipeline)格式。

## 公開必要的環境變數

開啟管線定義。 

在定義中，新增下列環境變數。這些是管線與 {{site.data.keyword.DRA_short}} 整合的必要變數。

| 環境變數        | 定義    |
| ----------------------------|---------------|
| `IBM_CLOUD_DEVOPS_CREDS`    | 您使用 `credentials` 指令在 Jenkins 中定義的 Bluemix 認證。例如，`IBM_CLOUD_DEVOPS_CREDS = credentials('BM_CRED')`。使用此指令來設定變數會自動多設定兩個環境變數：`IBM_CLOUD_DEVOPS_CREDS_USR` 和 `IBM_CLOUD_DEVOPS_CREDS_PSW`，代表使用者名稱和密碼。  |
| `IBM_CLOUD_DEVOPS_ORG`      | 工具鏈所屬的 Bluemix 組織。     |
| `IBM_CLOUD_DEVOPS_APP_NAME` | 工具鏈部署之應用程式的名稱。   |
| `IBM_CLOUD_DEVOPS_TOOCLHAIN_ID` | 工具鏈的 ID。請開啟工具鏈的「概觀」，查看 URL 來判斷 ID。工具鏈 URL 的格式為 `https://console.ng.bluemix.net/devops/toolchains/[YOUR_TOOLCHAIN_ID]`。   |
| `IBM_CLOUD_DEVOPS_WEBHOOKURL` | 當您將 Jenkins 新增至工具鏈時，提供給您的 Webhook。   |

如需 `credentials` 指令的相關資訊，請參閱 [Jenkins 管線文件](https://jenkins.io/doc/pipeline/tour/environment/#credentials-in-the-environment)。
{: tip}

如果您是使用 Script 化管線格式，請使用 `withCredentials` 來設定認證，並使用 `withEnv` 來設定環境，而不要使用下列範例所使用的 `credentials` 和 `environment`。如需 `withCredentials` 的相關資訊，請參閱 [Jenkins 文件](https://jenkins.io/doc/pipeline/steps/credentials-binding/)。
{: tip} 

這些是 IBM Cloud DevOps 外掛程式用來與 DevOps Insights 互動的環境變數和認證。在此範例中，它們是以宣告式管線格式進行設定。 

```
environment {
        IBM_CLOUD_DEVOPS_CREDS = credentials('BM_CRED')
        IBM_CLOUD_DEVOPS_ORG = 'dlatest'
        IBM_CLOUD_DEVOPS_APP_NAME = 'Weather-App'
        IBM_CLOUD_DEVOPS_TOOLCHAIN_ID = '1111111-aaaa-2222-bbbb-333333333'
        IBM_CLOUD_DEVOPS_WEBHOOK_URL = 'https://jenkins:5a55555a-a555-5555-5555-a555aa55a555:55555555-5555-5555-5555-555555555555@devops-api.ng.bluemix.net/v1/toolint/messaging/webhook/publish'
    }
```


## 新增 Cloud DevOps 步驟
Cloud DevOps 外掛程式在 Jenkins 管線中新增四個步驟，以供您使用。請在您的管線中使用這些步驟來與 DevOps Insights 互動。 

* `publishBuildRecord`，此步驟會將建置資訊發佈至 DevOps Insights
* `publishTestResult`，此步驟會將測試結果發佈至 DevOps Insights
* `publishDeployRecord`，此步驟會將部署記錄發佈至 DevOps Insights
* `evaluateGate`，此步驟會強制執行 DevOps Insights 原則 

請將這些步驟新增至管線定義中需要執行這些步驟的任何地方。例如，您可能會在執行測試之後上傳測試結果，然後在上傳之後於閘道上評估那些結果。 

### 發佈建置記錄

使用 `publishBuildRecord` 步驟來發佈建置記錄。此步驟需要四個參數。

| 參數        | 定義    |
| ----------------------------|---------------|
| `gitBranch`    | 建置使用之「Git 分支」的名稱。  |
| `gitCommit`      | 建置使用的 Git 確定 ID。    |
| `gitRepo` | Git 儲存庫的 URL。   |
| `result` | 建置階段的結果。該值是 `SUCCESS` 或 `FAIL`。   |

此範例顯示指令中的這些參數：

```
publishBuildRecord gitBranch: "${GIT_MASTER}", gitCommit: "${GIT_COMMIT}", gitRepo: "https://github.com/username/reponame", result:"SUCCESS"
```

「Jenkins 管線」不會將 Git 資訊公開為環境變數。若要取得 Git 確定 ID，您可以使用 `sh(returnStdout: true, script: 'git rev-parse HEAD').trim()` 指令。
{: tip}

### 發佈測試結果
使用 `publishTestResult` 步驟來發佈建置記錄。此步驟需要兩個參數。

| 參數        | 定義    |
| ----------------------------|---------------|
| `type`    | 測試結果的類型。若為單元測試，此參數的值必須是 `unittest`；若為功能驗證測試，此參數的值必須是 `fvt`；若為程式碼涵蓋面測試，此參數的值必須是 `code`。  |
| `fileLocation`      | 測試結果檔案的位置。    |

下列範例顯示指令中的這些參數。第一個指令會發佈 Mocha 單元測試結果。第二個指令會發佈程式碼涵蓋面測試結果。 

```
publishTestResult type:'unittest', fileLocation: './mochatest.json'
publishTestResult type:'code', fileLocation: './tests/coverage/reports/coverage-summary.json'
```

### 發佈部署記錄

使用 `publishDeployRecord` 步驟來發佈部署記錄。此步驟需要兩個參數。它也可以接受一個選用性參數。 

| 參數        | 定義    |
| ----------------------------|---------------|
| `environment`    | 要部署應用程式的環境。為了讓 DevOps Insights 適當運作，您必須將一個環境識別為 `STAGING`，將另一個環境識別為 `PRODUCTION`。 |
| `result`      | 建置階段的結果。該值應該是 `SUCCESS` 或 `FAIL`。    |
| `appUrl`      | *選用項目*：用來存取應用程式的 URL。    |

下列範例顯示指令中的這些參數。第一個指令會發佈編譯打包環境的部署記錄。第二個指令會發佈正式作業環境的部署記錄。

```
publishDeployRecord environment: "STAGING", appUrl: "http://staging-Weather-App.mybluemix.net", result:"SUCCESS"
publishDeployRecord environment: "PRODUCTION", appUrl: "http://Weather-App.mybluemix.net", result:"SUCCESS"
```

### 新增閘道

使用 `evaluateGate` 指令來新增閘道至管線。閘道會強制執行 DevOps Insights 原則，這些原則會設定建置升級的測試需求。 

此步驟需要一個參數。它也可以接受一個選用性參數。 

| 參數        | 定義    |
| ----------------------------|---------------|
| `policy`    | 閘道實作之原則的名稱。原則名稱定義在 DevOps Insights 中。 |
| `forceDecision`      | *選用*：管線是否要依閘道決策停止執行。如果將此參數設為 `true`，當閘道失敗時，管線會停止執行。如果設為 `false`，在閘道失敗之後，可容許管線繼續執行。預設值為 `false`。     |

下列範例顯示指令中的這些參數。在此指令中，管線會繼續執行，不論閘道的決策為何。 

```
evaluateGate policy: 'Weather App Policy', forceDecision: 'true'
```

### 與工具鏈通訊

使用 `notifyOTC` 指令，將管線狀態傳送至 Bluemix 工具鏈。若要進一步瞭解如何將 Jenkins 與工具鏈整合，[請參閱文件](https://console.ng.bluemix.net/docs/services/ContinuousDelivery/toolchains_integrations.html#jenkins)。您可以不處理步驟 6d 到 6f，因為它們僅適用於開放式 Jenkins 專案。

此步驟需要兩個參數，並且也可以接受一個選用參數。 

| 參數        | 定義    |
| ----------------------------|---------------|
| `stageName`    | 現行管線階段的名稱。 |
| `status`    | 現行管線階段的狀態。使用 `SUCCESS`、`FAILURE` 或 `ABORTED` 會在 Slack 中自動觸發色彩強調顯示。  |
| `webhookUrl`      | *選用*：工具鏈的 Jenkins 磚上顯示的 Webhook URL。如果包括此參數，其值會置換 `IBM_CLOUD_DEVOPS_WEBHOOKURL` 環境變數的值。   |

下列範例說明在宣告式和 Script 化管線定義中如何使用 `notifyOTC` 步驟。

#### 宣告式管線
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

#### Script 化管線
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

在這兩個範例中，只有在失敗時，才會置換工具鏈 Webhook URL。 

## 確保跨工具鏈整合的可追蹤性

遵循 [Bluemix 文件](https://console.ng.bluemix.net/docs/services/ContinuousDelivery/toolchains_integrations.html#jenkins)中的指示，配置 Jenkins 環境來與 Bluemix 工具鏈整合。您可以不處理步驟 6d 到 6f，因為它們僅適用於開放式 Jenkins 專案。

與工具鏈整合可讓您進行端對端追蹤和部署對映。遵循整合指示之後，將 `cf icd --create-connection $IBM_CLOUD_DEVOPS_WEBHOOK_URL $CF_APP_NAME` 指令新增在部署步驟後面。此指令會將 Jenkins 整合連接至在 Bluemix 上執行的應用程式。 

此範例顯示完整的部署步驟。最後一個指令是 `cf icd --create-connection`。 

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

如 Jenkins 整合說明文件所述，您的 Jenkins 伺服器上必須已安裝 CloudFoundry CLI 及 CloudFoundry ICD 外掛程式。您也必須從該伺服器登入 Bluemix，才能與其連線。

## 宣告式管線範例

此範例顯示定義為宣告式 Jenkinsfile 的完整管線。 

```
#!groovy
/*
    This is an sample Jenkins file for the Weather App, which is a node.js application that has unit test, code coverage
    and functional verification tests, deploy to staging and production environment and use IBM Cloud DevOps gate.
    We use this as an example to use our plugin in the Jenkinsfile
    Basically, you need to specify required 4 environment variables and then you will be able to use the 4 different methods
    for the build/test/deploy stage and the gate
 */
pipeline {
    agent any
    environment {
        // You need to specify 4 required environment variables first, they are going to be used for the following IBM Cloud DevOps steps
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
            // post build section to use "publishBuildRecord" method to publish build record
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
            // post build section to use "publishTestResult" method to publish test result
            post {
                always {
                    publishTestResult type:'unittest', fileLocation: './mochatest.json'
                    publishTestResult type:'code', fileLocation: './tests/coverage/reports/coverage-summary.json'
                }
            }
        }
        stage('Deploy to Staging') {
            steps {
                // Push the Weather App to Bluemix, staging space
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
            // post build section to use "publishDeployRecord" method to publish deploy record and notify OTC of stage status
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
            //set the APP_URL as the environment variable for the fvt
            environment {
                APP_URL = "http://staging-${IBM_CLOUD_DEVOPS_APP_NAME}.mybluemix.net"
            }
            steps {
                sh 'grunt fvt-test --no-color -f'
            }
            // post build section to use "publishTestResult" method to publish test result
            post {
                always {
                    publishTestResult type:'fvt', fileLocation: './mochafvt.json', environment: 'STAGING'
                }
            }
        }
        stage('Gate') {
            steps {
                // use "evaluateGate" method to leverage IBM Cloud DevOps gate
                evaluateGate policy: 'Weather App Policy', forceDecision: 'true'
            }
        }
        stage('Deploy to Prod') {
            steps {
                // Push the Weather App to Bluemix, production space
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
            // post build section to use "publishDeployRecord" method to publish deploy record and notify OTC of stage status
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










