---

copyright:
  years: 2016, 2017
lastupdated: "2017-04-21"

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}
{:tip: .tip}

# Jenkins Pipeline과 통합

개방형 도구 체인에 {{site.data.keyword.DRA_full}}를 추가하고 이를 모니터하는 정책을 정의한 후에 Jenkins Pipeline 프로젝트와 통합할 수 있습니다. 소스 제어 저장소에 저장하는 *Jenkinsfile* 또는 Jenkins 웹 인터페이스에 파이프라인을 정의합니다. Jenkins 웹 인터페이스에서 Jenkins Pipeline 프로젝트를 보고 관리할 수 있습니다. 

Jenkins용 IBM Cloud DevOps 플러그인은 Jenkins 프로젝트를 도구 체인과 통합합니다. *도구 체인*은 개발, 배치 및 운영 태스크를 지원하는 도구 통합 세트입니다. 도구 체인의 전체 기능은 개별 도구 통합을 합한 것보다 강력합니다. 개방형 도구 체인은 {{site.data.keyword.contdelivery_full}} 서비스의 일부입니다. {{site.data.keyword.contdelivery_short}} 서비스에 대한 자세한 정보는 [해당 문서](https://console.ng.bluemix.net/docs/services/ContinuousDelivery/cd_about.html)를 참조하십시오. 

IBM Cloud DevOps 플러그인을 설치하고 나면 {{site.data.keyword.DRA_short}}에 테스트 결과를 공개하고 게이트에서 자동으로 빌드 품질을 평가하며 Deployment Risk를 추적하도록 Jenkins 프로젝트를 구성할 수 있습니다. 또한 도구 체인에서 Slack 및 PagerDuty와 같은 기타 도구에 작업 알림을 보낼 수 있습니다. 배치를 추적할 수 있도록 도구 체인은 Git 커미트와 관련 Git 또는 JIRA 문제에 배치 메시지를 추가할 수 있습니다. 도구 체인의 연결 페이지에서도 배치를 볼 수 있습니다. 

플러그인은 통합을 지원하는 사후 빌드 조치 및 CLI를 제공합니다. {{site.data.keyword.DRA_short}}에서는 단위 테스트, Functional Test, 코드 적용 범위 도구, 정적 보안 코드 스캔 및 동적 보안 코드 스캔의 결과를 집계하고 분석하여 코드가 배치 프로세스의 게이트에서 사전 정의된 정책을 만족하는지 판별합니다. 코드가 정책을 충분히 준수하지 못하는 경우, 위험한 변경이 릴리스되지 않도록 배치가 정지됩니다. {{site.data.keyword.DRA_short}}를 Continuous Delivery 환경의 안전망으로 사용할 수 있는데 이를 통해 시간 경과에 따라 품질 표준을 구현 및 개선하고 프로젝트 상황을 파악하는 데이터 시각화 도구로 사용할 수 있습니다. 

이 주제에서는 사용자가 Jenkins Pipeline에 어느 정도 익숙하다고 간주합니다. 그렇지 않으면 계속하기 전에 [Jenkins Pipeline 문서를 참조](https://jenkins.io/doc/book/pipeline/)하십시오.

## 전제조건
{: #jenkins_prerequisites}

Jenkins Pipeline 프로젝트를 실행하는 서버에 액세스할 수 있어야 합니다. 

## 도구 체인 작성
{: #jenkins_create}

도구 체인을 작성해야 {{site.data.keyword.DRA_short}}를 Jenkins 프로젝트와 통합할 수 있습니다. 

1. 도구 체인을 작성하려면 [도구 체인 페이지 작성](https://console.ng.bluemix.net/devops/create)으로 이동하여 해당 페이지의 지시사항을 따르십시오. 

2. 도구 체인을 작성한 다음 {{site.data.keyword.DRA_short}}를 추가하십시오. 지시사항은 [{{site.data.keyword.DRA_short}}문서](https://console.ng.bluemix.net/docs/services/DevOpsInsights/index.html)를 참조하십시오. 

## 플러그인 설치
{: #jenkins_install}

먼저 {{site.data.keyword.DRA_short}}에서 플러그인을 다운로드하십시오.  

1. 도구 체인의 개요 페이지에서 **DevOps Insights**를 클릭하십시오.
2. **설정**을 클릭한 다음 **Jenkins 플러그인 설정**을 클릭하십시오.
3. 페이지의 지시사항을 따라 플러그인을 다운로드하십시오.

그런 다음 Jenkins 서버에서 플러그인을 설치하십시오.

1. **Jenkins 관리 &gt; 플러그인 관리**를 클릭하고 **고급** 탭을 클릭하십시오.
2. **파일 선택**을 클릭하고 IBM Cloud DevOps 플러그인 설치 파일을 선택하십시오. 
3. **업로드**를 클릭하십시오. 
4. Jenkins를 다시 시작하고 플러그인이 설치되었는지 확인하십시오.

## 파이프라인 생성
{: #jenkinsfile_create}

Jenkins 프로젝트 구성 메뉴 또는 저장소의 Jenkinsfile에 파이프라인을 정의합니다. 계속하려면 {{site.data.keyword.DRA_short}}와 사용할 기존 스크립트 또는 Jenkinsfile을 작성하거나 여십시오. [선언](https://jenkins.io/doc/book/pipeline/syntax/#declarative-pipeline) 또는 [스크립트](https://jenkins.io/doc/book/pipeline/syntax/#scripted-pipeline) 형식을 따를 수 있습니다.

## 필수 환경 변수 노출

다음으로 파이프라인 정의를 여십시오. 

정의에서 다음 환경 변수를 추가하십시오. 이러한 변수는 파이프라인을 {{site.data.keyword.DRA_short}}와 통합하기 위해 필요합니다.

| 환경 변수        | 정의    |
| ----------------------------|---------------|
| `IBM_CLOUD_DEVOPS_CREDS`    | `credentials` 명령을 사용하여 Jenkins에 정의하는 Bluemix 신임 정보입니다. 예를 들어 `IBM_CLOUD_DEVOPS_CREDS = credentials('BM_CRED')`입니다. 이 명령으로 변수를 설정하면 각각 사용자 이름과 비밀번호용으로 두 개의 추가 환경 변수, `IBM_CLOUD_DEVOPS_CREDS_USR` 및 `IBM_CLOUD_DEVOPS_CREDS_PSW`가 자동으로 설정됩니다.  |
| `IBM_CLOUD_DEVOPS_ORG`      | 도구 체인이 속한 Bluemix 조직입니다.     |
| `IBM_CLOUD_DEVOPS_APP_NAME` | 도구 체인이 배치하는 애플리케이션의 이름입니다.   |
| `IBM_CLOUD_DEVOPS_TOOCLHAIN_ID` | 도구 체인의 ID입니다. 도구 체인 개요를 열고 URL을 참조하여 ID를 판별하십시오. 도구 체인 URL 형식은 `https://console.ng.bluemix.net/devops/toolchains/[YOUR_TOOLCHAIN_ID]`입니다.   |
| `IBM_CLOUD_DEVOPS_WEBHOOKURL` | 도구 체인에 Jenkins를 추가할 때 제공된 Webhook입니다.   |

`credentials` 명령에 대한 자세한 정보는 [Jenkins Pipeline 문서](https://jenkins.io/doc/pipeline/tour/environment/#credentials-in-the-environment)를 참조하십시오.
{: tip}

스크립트된 파이프라인 형식을 사용하는 경우 아래 예에서 사용되는 `credentials` 및 `environment` 대신 `withCredentials`로 신임 정보를 설정하고 `withEnv`로 환경을 설정하십시오. `withCredentials`에 대한 자세한 정보는 [Jenkins 문서](https://jenkins.io/doc/pipeline/steps/credentials-binding/)를 참조하십시오.
{: tip} 

이러한 환경 변수와 신임 정보는 IBM Cloud DevOps 플러그인에서 DevOps Insight와 상호작용하기 위해 사용합니다. 다음은 선언 파이프라인 형식으로 설정하는 예입니다. 

```
environment {
        IBM_CLOUD_DEVOPS_CREDS = credentials('BM_CRED')
        IBM_CLOUD_DEVOPS_ORG = 'dlatest'
        IBM_CLOUD_DEVOPS_APP_NAME = 'Weather-App'
        IBM_CLOUD_DEVOPS_TOOLCHAIN_ID = '1111111-aaaa-2222-bbbb-333333333'
        IBM_CLOUD_DEVOPS_WEBHOOK_URL = 'https://jenkins:5a55555a-a555-5555-5555-a555aa55a555:55555555-5555-5555-5555-555555555555@devops-api.ng.bluemix.net/v1/toolint/messaging/webhook/publish'
    }
```


## Cloud DevOps 단계 추가
Cloud DevOps 플러그인은 사용자용으로 Jenkins 파이프라인에 4단계를 추가합니다. 파이프라인에서 이러한 단계를 사용하여 DevOps Insights와 상호작용하십시오. 

* `publishBuildRecord` - DevOps Insights에 빌드 정보를 공개합니다.
* `publishTestResult` - DevOps Insights에 테스트 결과를 공개합니다.
* `publishDeployRecord` - DevOps Insights에 배치 레코드를 공개합니다.
* `evaluateGate` - DevOps Insights 정책을 적용합니다. 

실행해야 하는 경우 항상 파이프라인 정의에 이 단계를 추가합니다. 예를 들어 테스트를 실행한 후 테스트 결과를 업로드한 다음 게이트에서 해당 결과를 평가할 수 있습니다. 

### 빌드 레코드 공개

`publishBuildRecord` 단계로 빌드 레코드를 공개하십시오. 이 단계에는 4개의 매개변수가 필요합니다.

| 매개변수        | 정의    |
| ----------------------------|---------------|
| `gitBranch`    | 빌드에서 사용하는 Git Branch의 이름입니다.  |
| `gitCommit`      | 빌드에서 사용하는 Git 커미트 ID입니다.    |
| `gitRepo` | Git 저장소의 URL입니다.   |
| `result` | 빌드 단계의 결과입니다. 값은 `SUCCESS` 또는 `FAIL`이어야 합니다.   |

다음은 예제 명령의 매개변수입니다.

```
publishBuildRecord gitBranch: "${GIT_MASTER}", gitCommit: "${GIT_COMMIT}", gitRepo: "https://github.com/username/reponame", result:"SUCCESS"
```

Jenkins Pipeline에서 Git 정보를 환경 변수로 노출하지 않습니다. `sh(returnStdout: true, script: 'git rev-parse HEAD').trim()` 명령을 사용하여 Git 커미트 ID를 가져올 수 있습니다.
{: tip}

### 테스트 결과 공개
`publishTestResult` 단계로 빌드 레코드를 공개하십시오. 이 단계에는 2개의 매개변수가 필요합니다.

| 매개변수        | 정의    |
| ----------------------------|---------------|
| `type`    | 테스트 결과의 유형입니다. 이 값은 단위 테스트의 경우 `unittest`이고, 기능 검증 테스트의 경우 `fvt`이며, 코드 적용 범위 테스트의 경우 `code`여야 합니다.  |
| `fileLocation`      | 테스트 결과 파일의 위치입니다.    |

다음은 예제 명령의 매개변수입니다. 첫 번째 명령은 Mocha 단위 테스트 결과를 공개하고 두 번째 명령은 코드 적용 범위 테스트 결과를 공개합니다. 

```
publishTestResult type:'unittest', fileLocation: './mochatest.json'
publishTestResult type:'code', fileLocation: './tests/coverage/reports/coverage-summary.json'
```

### 배치 레코드 공개

`publishDeployRecord` 단계로 배치 레코드를 공개하십시오. 이 단계에는 2개의 매개변수가 필요합니다. 선택적 매개변수 하나도 승인할 수 있습니다. 

| 매개변수        | 정의    |
| ----------------------------|---------------|
| `environment`    | 앱을 배치할 환경입니다. DevOps Insights가 제대로 작동하려면 한 환경을 `STAGING`으로 식별하고 다른 환경은 `PRODUCTION`으로 식별해야 합니다. |
| `result`      | 빌드 단계의 결과입니다. 값은 `SUCCESS` 또는 `FAIL`이어야 합니다.    |
| `appUrl`      | *선택사항*: 애플리케이션에 액세스하는 데 사용한 URL입니다.    |

다음은 예제 명령의 매개변수입니다. 첫 번째 명령은 스테이징 환경의 배치 레코드를 공개하고, 두 번째 명령은 프로덕션 환경의 배치 레코드를 공개합니다.

```
publishDeployRecord environment: "STAGING", appUrl: "http://staging-Weather-App.mybluemix.net", result:"SUCCESS"
publishDeployRecord environment: "PRODUCTION", appUrl: "http://Weather-App.mybluemix.net", result:"SUCCESS"
```

### 게이트 추가

`evaluateGate` 명령을 사용하여 파이프라인에 게이트를 추가합니다. 게이트는 빌드 승격을 위한 테스트 요구사항을 설정하는 DevOps Insights 정책을 적용합니다. 

이 단계에는 매개변수가 하나 필요합니다. 선택적 매개변수 하나도 승인할 수 있습니다. 

| 매개변수        | 정의    |
| ----------------------------|---------------|
| `policy`    | 게이트에서 구현하는 정책의 이름입니다. 정책의 이름은 DevOps Insights에 정의됩니다. |
| `forceDecision`      | *선택사항*: 게이트의 의사결정에 따른 파이프라인 중지 여부입니다. 게이트가 실패하는 경우 이 매개변수를 `true`로 설정하여 파이프라인이 실행되지 못하게 하십시오. 게이트 실패 후에 파이프라인이 계속될 수 있도록 `false`로 설정하십시오. 기본값은 `false`입니다.     |

다음은 예제 명령의 매개변수입니다. 이 명령에서 게이트의 의사결정과 상관없이 파이프라인이 계속 실행됩니다. 

```
evaluateGate policy: 'Weather App Policy', forceDecision: 'true'
```

### 도구 체인과 통신

`notifyOTC` 명령을 사용하여 Bluemix 도구 체인에 파이프라인 상태를 보내십시오. 도구 체인과 Jenkins를 통합하는 데 대해 자세히 알아보려면 [문서를 참조](https://console.ng.bluemix.net/docs/services/ContinuousDelivery/toolchains_integrations.html#jenkins)하십시오. 자유 양식 Jenkins 프로젝트에만 적용되므로 6d - 6f 단계는 무시할 수 있습니다.

이 단계에는 2개의 매개변수가 필요하며 추가로 선택적인 매개변수 하나를 사용할 수 있습니다. 

| 매개변수        | 정의    |
| ----------------------------|---------------|
| `stageName`    | 현재 파이프라인 단계의 이름입니다. |
| `status`    | 현재 파이프라인 단계의 상태입니다. `SUCCESS`, `FAILURE` 또는 `ABORTED`를 사용하면 Slack에서 색상 강조표시가 자동으로 트리거됩니다.   |
| `webhookUrl`      | *선택사항*: 도구 체인의 Jenkins 타일에 표시되는 Webhook URL입니다. 이 매개변수를 포함하면 해당 값이 `IBM_CLOUD_DEVOPS_WEBHOOKURL` 환경 변수의 값을 대체합니다.   |

다음은 선언 및 스크립트 파이프라인 정의 둘 다에서 `notifyOTC` 단계를 사용하는 예입니다.

#### 선언 파이프라인 예:
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

#### 스크립트 파이프라인 예:
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

이 두 예제 모두에서 도구 체인 Webhook URL은 실패하는 경우에만 대체됩니다. 

## 도구 체인 통합에서 추적성 보장

[Bluemix 문서](https://console.ng.bluemix.net/docs/services/ContinuousDelivery/toolchains_integrations.html#jenkins)의 지시사항을 따라 Bluemix 도구 체인과 통합하도록 Jenkins 환경을 구성하십시오. 자유 양식 Jenkins 프로젝트에만 적용되므로 6d - 6f 단계는 무시할 수 있습니다.

도구 체인과 통합하면 엔드-투-엔드 추적성 및 배치 맵핑을 제공합니다. 통합 지시사항을 따른 다음  배치 단계 후에 `cf icd --create-connection $IBM_CLOUD_DEVOPS_WEBHOOK_URL $CF_APP_NAME` 명령을 추가하십시오. 이 명령은 Bluemix에서 실행 중인 앱에 Jenkins 통합을 연결합니다. 

다음은 전체 배치 단계의 예입니다. 마지막 명령은 `cf icd --create-connection`입니다. 

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

Jenkins 통합 문서에 설명된 대로 Jenkins 서버에 CloudFoundry CLI 및 CloudFoundry ICD 플러그인이 설치되어야 합니다. 연결하려면 서버에서 Bluemix에 로그인해야 합니다.

## 예제 선언 파이프라인

예를 들어 다음은 선언 Jenkinsfile로 정의된 전체 파이프라인입니다. 

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










