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

# 与 Jenkins Pipeline 集成

将 {{site.data.keyword.DRA_full}} 添加到开放工具链并定义其监视的策略之后，可以将其与 Jenkins Pipeline 项目相集成。您可在 Jenkins Web 界面中定义管道，也可在源代码控制存储库中存储的 *Jenkinsfile* 中定义管道。可以在 Jenkins Web 界面中查看和管理 Jenkins Pipeline 项目。 

IBM Cloud DevOps for Jenkins 插件可将 Jenkins 项目与工具链相集成。*工具链*是一组工具集成，用于支持开发、部署和操作任务。工具链的整体能力大于其各个单独工具集成的总和。开放工具链是 {{site.data.keyword.contdelivery_full}} 服务的组成部分。要了解有关 {{site.data.keyword.contdelivery_short}} 服务的更多信息，请参阅[其服务文档](https://console.ng.bluemix.net/docs/services/ContinuousDelivery/cd_about.html)。 

安装 IBM Cloud DevOps 插件后，可以配置 Jenkins 项目，以将测试结果发布到 {{site.data.keyword.DRA_short}}，自动在检测点对构建质量进行评估以及跟踪部署风险。您还可以将作业通知发送给工具链中的其他工具，例如 Slack 和 PagerDuty。为了帮助您跟踪部署，工具链可以将部署消息添加到 Git 落实及其相关的 Git 或 JIRA 问题。此外，还可以在工具链的“连接”页面上查看部署。 

该插件提供了构建后操作和 CLI 以支持集成。{{site.data.keyword.DRA_short}} 聚集和分析单元测试、功能测试、代码覆盖工具、静态安全代码扫描和动态安全代码扫描的结果，以确定您的代码是否符合部署过程中检测点处的预定义策略。如果您的代码不满足或超出策略，那么会暂停部署以防止发布有风险的更改。您可以使用 {{site.data.keyword.DRA_short}} 作为持续交付环境的安全网、作为随时间实现和提高质量标准的方法，以及作为帮助您了解项目运行状况的数据可视化工具。

如果您熟悉 Jenkins Pipeline，请继续阅读。否则，请先参阅 [Jenkins Pipeline 文档](https://jenkins.io/doc/book/pipeline/)，然后再继续。

## 先决条件
{: #jenkins_prerequisites}

您必须有权访问正在运行 Jenkins Pipeline 项目的服务器。 

## 创建工具链
{: #jenkins_create}

必须创建工具链后，才能将 {{site.data.keyword.DRA_short}} 与 Jenkins 项目相集成。 

1. 要创建工具链，请转至[创建工具链页面](https://console.ng.bluemix.net/devops/create)并按照该页面上的指示信息进行操作。 

2. 创建工具链后，向其添加 {{site.data.keyword.DRA_short}}。有关指示信息，请参阅 [{{site.data.keyword.DRA_short}} 文档](https://console.ng.bluemix.net/docs/services/DevOpsInsights/index.html)。 

## 安装插件
{: #jenkins_install}

通过打开服务器界面并遵循以下步骤，在 Jenkins 服务器上安装插件：

1. 单击**管理 Jenkins**。
2. 单击**管理插件**。 
3. 单击**可用**选项卡。
4. 对 `IBM Cloud DevOps` 进行过滤。 
5. 选择 **IBM Cloud DevOps**。
6. 单击**立即下载并在重新启动后安装**。 

在服务器重新启动后即可使用该插件。  

## 创建管道
{: #jenkinsfile_create}

您可在 Jenkins 项目配置菜单中定义管道，也可在存储库的 Jenkinsfile 中定义管道。要继续，请创建或打开脚本或 Jenkinsfile 以用于 {{site.data.keyword.DRA_short}}。您可以采用[声明式](https://jenkins.io/doc/book/pipeline/syntax/#declarative-pipeline)或[脚本式](https://jenkins.io/doc/book/pipeline/syntax/#scripted-pipeline)格式。

## 公开必需的环境变量

打开管道定义。 

在定义中，添加以下环境变量。这些是管道与 {{site.data.keyword.DRA_short}} 集成所必需的变量。

| 环境变量        | 定义    |
| ----------------------------|---------------|
| `IBM_CLOUD_DEVOPS_CREDS`    | 使用 `credentials` 命令在 Jenkins 中定义的 Bluemix 凭证。例如，`IBM_CLOUD_DEVOPS_CREDS = credentials('BM_CRED')`。使用此命令设置该变量将自动设置另外两个环境变量：`IBM_CLOUD_DEVOPS_CREDS_USR` 和 `IBM_CLOUD_DEVOPS_CREDS_PSW`，分别表示用户名和密码。  |
| `IBM_CLOUD_DEVOPS_ORG`      | 工具链所属的 Bluemix 组织。     |
| `IBM_CLOUD_DEVOPS_APP_NAME` | 工具链部署的应用程序的名称。   |
| `IBM_CLOUD_DEVOPS_TOOCLHAIN_ID` | 工具链的标识。打开工具链“概述”，并查看相关 URL 以确定标识。工具链 URL 格式为 `https://console.ng.bluemix.net/devops/toolchains/[YOUR_TOOLCHAIN_ID]`。   |
| `IBM_CLOUD_DEVOPS_WEBHOOKURL` | 将 Jenkins 添加到工具链时为您提供的 WebHook。   |

有关 `credentials` 命令的更多信息，请参阅 [Jenkins Pipeline 文档](https://jenkins.io/doc/pipeline/tour/environment/#credentials-in-the-environment)。
{: tip}

如果使用的是脚本式管道格式，请使用 `withCredentials` 设置凭证，并使用 `withEnv` 设置环境，而不要使用以下示例中所用的 `credentials` 和 `environment` 进行设置。有关 `withCredentials` 的更多信息，请参阅 [Jenkins 文档](https://jenkins.io/doc/pipeline/steps/credentials-binding/)。
{: tip} 

IBM Cloud DevOps 插件使用这些环境变量和凭证来与 DevOps Insights 进行交互。在此示例中，以声明式管道格式进行设置。 

```
environment {
        IBM_CLOUD_DEVOPS_CREDS = credentials('BM_CRED')
        IBM_CLOUD_DEVOPS_ORG = 'dlatest'
        IBM_CLOUD_DEVOPS_APP_NAME = 'Weather-App'
        IBM_CLOUD_DEVOPS_TOOLCHAIN_ID = '1111111-aaaa-2222-bbbb-333333333'
        IBM_CLOUD_DEVOPS_WEBHOOK_URL = 'https://jenkins:5a55555a-a555-5555-5555-a555aa55a555:55555555-5555-5555-5555-555555555555@devops-api.ng.bluemix.net/v1/toolint/messaging/webhook/publish'
    }
```


## 添加 Cloud DevOps 步骤
Cloud DevOps 插件会向 Jenkins Pipeline 添加四个步骤供您使用。在管道中使用这四个步骤可与 DevOps Insights 进行交互。 

* `publishBuildRecord`，用于将构建信息发布到 DevOps Insights
* `publishTestResult`，用于将测试结果发布到 DevOps Insights
* `publishDeployRecord`，用于将部署记录发布到 DevOps Insights
* `evaluateGate`，用于强制实施 DevOps Insights 策略 

将这些步骤添加到管道定义中需要运行这些步骤的每个位置。例如，在运行测试后可上传测试结果，然后在检测点对上传的结果进行评估。 

### 发布构建记录

使用 `publishBuildRecord` 步骤发布构建记录。此步骤需要四个参数。

| 参数        | 定义    |
| ----------------------------|---------------|
| `gitBranch`    | 构建使用的 Git 分支的名称。  |
| `gitCommit`      | 构建使用的 Git 落实标识。    |
| `gitRepo` | Git 存储库的 URL。   |
| `result` | 构建阶段的结果。值为 `SUCCESS` 或 `FAIL`。   |

此示例显示命令中的这些参数：

```
publishBuildRecord gitBranch: "${GIT_MASTER}", gitCommit: "${GIT_COMMIT}", gitRepo: "https://github.com/username/reponame", result:"SUCCESS"
```

Jenkins Pipeline 不会将 Git 信息作为环境变量公开。可以使用 `sh(returnStdout: true, script: 'git rev-parse HEAD').trim()` 命令来获取 Git 落实标识。
{: tip}

### 发布测试结果
使用 `publishTestResult` 步骤发布测试结果。此步骤需要两个参数。

| 参数        | 定义    |
| ----------------------------|---------------|
| `type`    | 测试结果的类型。此参数的值必须为 `unittest`（对于单元测试）、`fvt`（对于功能验证测试）或 `code`（对于代码覆盖测试）。  |
| `fileLocation`      | 测试结果文件的位置。    |

以下示例显示命令中的这些参数。第一个命令发布 Mocha 单元测试结果。第二个命令发布代码覆盖测试结果。 

```
publishTestResult type:'unittest', fileLocation: './mochatest.json'
publishTestResult type:'code', fileLocation: './tests/coverage/reports/coverage-summary.json'
```

### 发布部署记录

使用 `publishDeployRecord` 步骤发布部署记录。此步骤需要两个参数。此外，它还可接受一个可选参数。 

| 参数        | 定义    |
| ----------------------------|---------------|
| `environment`    | 将应用程序部署到的环境。要使 DevOps Insights 正常运行，必须将一个环境识别为 `STAGING`，另一个环境识别为 `PRODUCTION`。 |
| `result`      | 构建阶段的结果。值应该为 `SUCCESS` 或 `FAIL`。    |
| `appUrl`      | *可选*：用于访问应用程序的 URL。    |

以下示例显示命令中的这些参数。第一个命令发布编译打包环境的部署记录。第二个命令发布生产环境的部署记录。

```
publishDeployRecord environment: "STAGING", appUrl: "http://staging-Weather-App.mybluemix.net", result:"SUCCESS"
publishDeployRecord environment: "PRODUCTION", appUrl: "http://Weather-App.mybluemix.net", result:"SUCCESS"
```

### 添加检测点

使用 `evaluateGate` 命令向管道添加检测点。检测点将强制实施 DevOps Insights 策略，策略用于设置构建升级的测试需求。 

此步骤需要一个参数。此外，它还可接受一个可选参数。 

| 参数        | 定义    |
| ----------------------------|---------------|
| `policy`    | 检测点实施的策略的名称。策略的名称在 DevOps Insights 中进行定义。 |
| `forceDecision`      | *可选*：管道是否停止取决于检测点的决策。将此参数设置为 `false` 可在检测点失败时停止运行管道。将此参数设置为 `true` 将允许管道在检测点失败后继续运行。缺省情况下，此值为 `false`。     |

以下示例显示命令中的这些参数。在此命令中，不管检测点的决策是什么，管道都将继续运行。 

```
evaluateGate policy: 'Weather App Policy', forceDecision: 'true'
```

### 与工具链通信

使用 `notifyOTC` 命令将管道状态发送到 Bluemix 工具链。要了解有关将 Jenkins 与工具链相集成的更多信息，[请参阅文档](https://console.ng.bluemix.net/docs/services/ContinuousDelivery/toolchains_integrations.html#jenkins)。可以忽略步骤 6d 到 6f，因为这些步骤仅适用于自由格式的 Jenkins 项目。

此步骤需要两个参数，还可以采用一个可选参数。 

| 参数        | 定义    |
| ----------------------------|---------------|
| `stageName`    | 当前管道阶段的名称。 |
| `status`    | 当前管道阶段的状态。使用 `SUCCESS`、`FAILURE` 或 `ABORTED` 将在 Slack 中自动触发颜色突出显示。  |
| `webhookUrl`      | *可选*：在工具链的 Jenkins 磁贴上显示的 WebHook URL。如果包含此参数，其值将覆盖 `IBM_CLOUD_DEVOPS_WEBHOOKURL` 环境变量的值。   |

以下示例显示如何在声明式和脚本式管道定义中使用 `notifyOTC` 步骤。

#### 声明式管道
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

#### 脚本式管道
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

在这两个示例中，仅在失败时才会覆盖工具链 WebHook URL。 

## 确保跨工具链集成的可跟踪性

通过遵循 [Bluemix 文档](https://console.ng.bluemix.net/docs/services/ContinuousDelivery/toolchains_integrations.html#jenkins)中的指示信息，将 Jenkins 环境配置为与 Bluemix 工具链相集成。可以忽略步骤 6d 到 6f，因为这些步骤仅适用于自由格式的 Jenkins 项目。

通过与工具链相集成，可以提供端到端可跟踪性和部署映射。遵循集成指示信息进行操作后，在部署步骤后添加 `cf icd --create-connection $IBM_CLOUD_DEVOPS_WEBHOOK_URL $CF_APP_NAME` 命令。此命令将 Jenkins 集成连接到正在在 Bluemix 上运行的应用程序。 

此示例显示完整的部署步骤。最后一个命令是 `cf icd --create-connection`。 

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

如 Jenkins 集成文档中所述，必须在 Jenkins 服务器上安装 CloudFoundry CLI 和 CloudFoundry ICD 插件。您还需要从服务器登录到 Bluemix 才能与其建立连接。

## 声明式管道示例

此示例显示定义为声明式 Jenkinsfile 的完整管道。 

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










