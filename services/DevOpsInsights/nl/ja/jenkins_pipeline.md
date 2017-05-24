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

# Jenkins パイプラインとの統合

{{site.data.keyword.DRA_full}} をオープン・ツールチェーンに追加し、それがモニターするポリシーを定義した後、それを Jenkins パイプライン・プロジェクトに統合することができます。
パイプラインは、Jenkins Web インターフェースの中、またはソース制御リポジトリーに保管する *Jenkinsfile* の中で定義します。
Jenkins パイプライン・プロジェクトは、Jenkins Web インターフェースから表示および管理することができます。
 

Jenkins 用 IBM Cloud DevOps プラグインは、Jenkins プロジェクトをツールチェーンに統合します。
*ツールチェーン*は、開発、デプロイメント、運用の作業をサポートするツール統合のセットです。
ツールチェーンの集合体としての能力は、それに含まれる個々のツール統合の総和よりも優れています。
オープン・ツールチェーンは、{{site.data.keyword.contdelivery_full}} サービスの一部です。
{{site.data.keyword.contdelivery_short}} サービスについて詳しくは、[そのドキュメンテーション](https://console.ng.bluemix.net/docs/services/ContinuousDelivery/cd_about.html)を参照してください。
 

IBM Cloud DevOps プラグインをインストールした後は、テスト結果を {{site.data.keyword.DRA_short}} に公開し、ゲートでビルドの品質を自動的に評価して、デプロイメント・リスクを追跡するために Jenkins プロジェクトを構成することができます。
また、ジョブ通知を、Slack や PagerDuty など、ツールチェーン内の他のツールに送信することもできます。
デプロイメントの追跡のために、Git コミットやそれに関連した Git または JIRA の問題に対して、ツールチェーンからデプロイメント・メッセージを追加することができます。
また、デプロイメントを「ツールチェーン接続」ページに表示することもできます。
 

このプラグインは、統合をサポートするためのビルド後アクションや CLI を提供します。
{{site.data.keyword.DRA_short}} は、単体テスト、機能テスト、コード・カバレッジ・ツール、静的セキュリティー・コード・スキャン、動的セキュリティー・コード・スキャンからの結果を集約し、分析することによって、デプロイメント・プロセス内のゲートにおいて、コードが事前定義されたポリシーを満たしているかどうかを判別します。
コードがポリシーを満たしていないか、ポリシーを超えていない場合、リスクのある変更版がリリースされないように、デプロイメントが停止されます。{{site.data.keyword.DRA_short}} は、継続的デリバリー環境のセーフティー・ネット、品質規格を実装して時間の経過とともに向上させるための方法、およびプロジェクトの正常性を把握するのに役立つデータ可視化ツールとして使用できます。

このトピックでは、読者に Jenkins パイプラインに関するある程度の知識があることを想定しています。
そうでない場合は、先に [Jenkins パイプラインのドキュメンテーション](https://jenkins.io/doc/book/pipeline/)を参照してください。


## 前提条件
{: #jenkins_prerequisites}

Jenkins パイプライン・プロジェクトを実行しているサーバーに対するアクセス権がなければなりません。
 

## ツールチェーンの作成
{: #jenkins_create}

{{site.data.keyword.DRA_short}} と Jenkins プロジェクトを統合するには、その前にツールチェーンを作成する必要があります。
 

1. ツールチェーンを作成するには、[「ツールチェーンの作成 (Create a Toolchain)」ページ](https://console.ng.bluemix.net/devops/create)に移動し、そのページに示されている手順を実行します。
 

2. ツールチェーンの作成後、それに {{site.data.keyword.DRA_short}} を追加します。
その手順については、[{{site.data.keyword.DRA_short}} のドキュメンテーション](https://console.ng.bluemix.net/docs/services/DevOpsInsights/index.html)を参照してください。
 

## プラグインのインストール
{: #jenkins_install}

まず、{{site.data.keyword.DRA_short}} からプラグインをダウンロードします。
  

1. ツールチェーンの概要ページから、**DevOps Insights** をクリックします。

2. **「設定」**、**「Jenkins プラグインのセットアップ (Jenkins Plugin Setup)」** の順にクリックします。

3. ページの指示に従い、プラグインをダウンロードします。


次に、Jenkins サーバーでプラグインをインストールします。


1. **「Jenkins の管理 (Manage Jenkins)」&gt;「プラグインの管理」**をクリックした後、**「詳細」**タブをクリックします。

2. **「ファイルの選択」**をクリックし、IBM Cloud DevOps プラグインのインストール・ファイルを選択します。
 
3. **「アップロード」**をクリックします。
4. Jenkins を再始動して、プラグインがインストールされたことを確認します。

## パイプラインの作成
{: #jenkinsfile_create}

Jenkins プロジェクト構成メニューか、リポジトリー内の Jenkinsfile のいずれかで、パイプラインを定義します。
先に進むには、{{site.data.keyword.DRA_short}} で使用する既存のスクリプトまたは Jenkinsfile を開くか、または作成します。
[宣言](https://jenkins.io/doc/book/pipeline/syntax/#declarative-pipeline)形式か、[スクリプト](https://jenkins.io/doc/book/pipeline/syntax/#scripted-pipeline)形式で作成することができます。


## 必要な環境変数の公開

次に、パイプライン定義を開きます。
 

定義の中で、以下の環境変数を追加します。
これらの変数は、パイプラインを {{site.data.keyword.DRA_short}} に統合するために必要です。


| 環境変数                    | 定義          |
| ----------------------------|---------------|
| `IBM_CLOUD_DEVOPS_CREDS`    | Jenkins 内で `credentials` コマンドを使用して定義する Bluemix 資格情報。例えば、`IBM_CLOUD_DEVOPS_CREDS = credentials('BM_CRED')`。このコマンドで変数を設定すると、ユーザー名とパスワードのそれぞれに対する 2 つの追加の環境変数 `IBM_CLOUD_DEVOPS_CREDS_USR` と `IBM_CLOUD_DEVOPS_CREDS_PSW` が自動的に設定されます。  |
| `IBM_CLOUD_DEVOPS_ORG`      | ツールチェーンの属する Bluemix 組織。     |
| `IBM_CLOUD_DEVOPS_APP_NAME` | ツールチェーンがデプロイするアプリケーションの名前。   |
| `IBM_CLOUD_DEVOPS_TOOCLHAIN_ID` | ツールチェーンの ID。ツールチェーンの概要を開き、URL を見て ID を判別します。ツールチェーン URL の形式は `https://console.ng.bluemix.net/devops/toolchains/[YOUR_TOOLCHAIN_ID]` です。   |
| `IBM_CLOUD_DEVOPS_WEBHOOKURL` | Jenkins をツールチェーンに追加した時点で提供された webhook。   |

`credentials` コマンドについて詳しくは、[Jenkins パイプラインのドキュメンテーション](https://jenkins.io/doc/pipeline/tour/environment/#credentials-in-the-environment)を参照してください。
{: tip}

スクリプト・パイプライン形式を使用する場合は、下記のサンプルで使用されている `credentials` と `environment` は使用せず、代わりに `withCredentials` で資格情報を設定し、`withEnv` で環境を設定します。
`withCredentials` については、[Jenkins のドキュメンテーション](https://jenkins.io/doc/pipeline/steps/credentials-binding/)を参照してください。
{: tip} 

これらの環境変数と資格情報は、DevOps Insights との対話のために IBM Cloud DevOps プラグインによって使用されます。
以下に、宣言パイプライン形式での設定方法のサンプルを示します。
 

```
environment {
        IBM_CLOUD_DEVOPS_CREDS = credentials('BM_CRED')
        IBM_CLOUD_DEVOPS_ORG = 'dlatest'
        IBM_CLOUD_DEVOPS_APP_NAME = 'Weather-App'
        IBM_CLOUD_DEVOPS_TOOLCHAIN_ID = '1111111-aaaa-2222-bbbb-333333333'
        IBM_CLOUD_DEVOPS_WEBHOOK_URL = 'https://jenkins:5a55555a-a555-5555-5555-a555aa55a555:55555555-5555-5555-5555-555555555555@devops-api.ng.bluemix.net/v1/toolint/messaging/webhook/publish'
    }
```


## Cloud DevOps のステップの追加
Cloud DevOps プラグインにより、使用する Jenkins パイプラインに 4 つのステップが追加されます。
これらのステップは、DevOps Insights との対話のためにパイプラインの中で使用します。
 

* `publishBuildRecord`。ビルド情報を DevOps Insights に公開します
* `publishTestResult`。テスト結果を DevOps Insights に公開します
* `publishDeployRecord`。デプロイメント・レコードを DevOps Insights に公開します
* `evaluateGate`。DevOps Insights ポリシーを適用します 

これらのステップを、パイプライン定義内のこれらのステップを実行する必要のある箇所に追加します。
例えば、テスト実行の後にテスト結果をアップロードし、アップロード後にゲートでそれらの結果を評価することができます。
 

### ビルド・レコードの公開

`publishBuildRecord` ステップでビルド・レコードを公開します。
このステップでは、4 つのパラメーターが必要です。


| パラメーター        | 定義    |
| ----------------------------|---------------|
| `gitBranch`    | ビルドで使用する Git ブランチの名前。  |
| `gitCommit`      | ビルドで使用する Git コミット ID。    |
| `gitRepo` | Git リポジトリーの URL。   |
| `result` | ビルド・ステージの結果。値は `SUCCESS` か `FAIL` でなければなりません。   |

サンプル・コマンドのパラメーターを以下に示します。


```
publishBuildRecord gitBranch: "${GIT_MASTER}", gitCommit: "${GIT_COMMIT}", gitRepo: "https://github.com/username/reponame", result:"SUCCESS"
```

Jenkins パイプラインは、Git 情報を環境変数として公開しません。
コマンド `sh(returnStdout: true, script: 'git rev-parse HEAD').trim()` を使用することにより、Git コミット ID を入手できます。
{: tip}

### テスト結果の公開
`publishTestResult` ステップでビルド・レコードを公開します。
このステップでは、2 つのパラメーターが必要です。


| パラメーター        | 定義    |
| ----------------------------|---------------|
| `type`    | テスト結果のタイプ。この値は、単体テストでは `unittest`、機能検証テストでは `fvt`、コード・カバレッジ・テストでは `code` でなければなりません。  |
| `fileLocation`      | テスト結果ファイルの場所。    |

サンプル・コマンドのパラメーターを以下に示します。
最初のコマンドで Mocha 単体テスト結果を公開し、2 番目のコマンドでコード・カバレッジ・テスト結果を公開しています。  

```
publishTestResult type:'unittest', fileLocation: './mochatest.json'
publishTestResult type:'code', fileLocation: './tests/coverage/reports/coverage-summary.json'
```

### デプロイメント・レコードの公開

`publishDeployRecord` ステップでデプロイメント・レコードを公開します。
このステップでは、2 つのパラメーターが必要です。
これには、1 つのオプション・パラメーターも指定できます。
 

| パラメーター        | 定義    |
| ----------------------------|---------------|
| `environment`    | アプリのデプロイ先となる環境。DevOps Insights が適切に機能するためには、1 つの環境を `STAGING` として、別の環境を `PRODUCTION` として識別する必要があります。 |
| `result`      | ビルド・ステージの結果。値は `SUCCESS` か `FAIL` でなければなりません。    |
| `appUrl`      | *オプション*: アプリケーションにアクセスするために使用する URL。    |

サンプル・コマンドのパラメーターを以下に示します。
最初のコマンドはステージング環境のデプロイメント・レコードを公開し、2 つ目のコマンドは実稼働環境のデプロイメント・レコードを公開します。


```
publishDeployRecord environment: "STAGING", appUrl: "http://staging-Weather-App.mybluemix.net", result:"SUCCESS"
publishDeployRecord environment: "PRODUCTION", appUrl: "http://Weather-App.mybluemix.net", result:"SUCCESS"
```

### ゲートの追加

`evaluateGate` コマンドを使用することにより、ゲートをパイプラインに追加します。
ゲートでは、ビルドのプロモーションのためのテストの要件を設定する DevOps Insights ポリシーが適用されます。
 

このステップでは、1 つのパラメーターが必要です。
これには、1 つのオプション・パラメーターも指定できます。
 

| パラメーター        | 定義    |
| ----------------------------|---------------|
| `policy`    | ゲートが実装するポリシーの名前。ポリシーの名前は、DevOps Insights の中で定義されます。 |
| `forceDecision`      | *オプション*: ゲートの決定に応じてパイプラインが停止するかどうか。ゲートの結果が不合格の場合にパイプラインの実行を停止する場合、このパラメーターを `true` に設定します。
ゲートの結果が不合格になった後もパイプラインが続行することを可能にするには、`false` に設定します。デフォルト値は `false` です。     |

サンプル・コマンドのパラメーターを以下に示します。
このコマンドでは、ゲートの決定には関係なくパイプラインの実行は続行します。
 

```
evaluateGate policy: 'Weather App Policy', forceDecision: 'true'
```

### ツールチェーンとの通信

パイプラインの状況を Bluemix ツールチェーンに送信するには、`notifyOTC` コマンドを使用します。
Jenkins をツールチェーンに統合することについては、[ドキュメンテーションを参照してください](https://console.ng.bluemix.net/docs/services/ContinuousDelivery/toolchains_integrations.html#jenkins)。
ステップ 6d から 6f までは、フリー・フォームの Jenkins プロジェクトにのみ当てはまるものであり、無視することができます。


このステップには 2 つのパラメーターが必要であり、付加的なオプション・パラメーターも 1 つ指定できます。
 

| パラメーター        | 定義    |
| ----------------------------|---------------|
| `stageName`    | 現在のパイプライン・ステージの名前。 |
| `status`    | 現在のパイプライン・ステージの状況。`SUCCESS`、`FAILURE`、または `ABORTED` を使用すると、Slack で色強調表示が自動的に起動します。  |
| `webhookUrl`      | *オプション*: ツールチェーンの Jenkins タイルに表示される webhook URL。このパラメーターを含める場合、その値により、`IBM_CLOUD_DEVOPS_WEBHOOKURL` 環境変数の値がオーバーライドされます。
   |

宣言とスクリプトの両方のパイプライン定義において `notifyOTC` ステップを使用する例を以下に示します。


#### 宣言パイプラインのサンプル:
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

#### スクリプト・パイプラインのサンプル:
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

どちらのサンプルについても、ツールチェーン webhook URL は失敗の場合にのみオーバーライドされることに注意してください。
 

## ツールチェーン統合を通じての追跡可能性の確認

Bluemix ツールチェーンと統合するように Jenkins 環境を構成するには、[Bluemix の資料](https://console.ng.bluemix.net/docs/services/ContinuousDelivery/toolchains_integrations.html#jenkins)にある以下の手順に従います。
ステップ 6d から 6f までは、フリー・フォームの Jenkins プロジェクトにのみ当てはまるものであり、無視することができます。


ツールチェーンと統合すると、エンドツーエンドの追跡やデプロイメント・マッピングが可能になります。
統合の手順を実行した後、デプロイメント・ステップの後にコマンド `cf icd --create-connection $IBM_CLOUD_DEVOPS_WEBHOOK_URL $CF_APP_NAME` を追加します。
このコマンドを実行すると、Jenkins 統合が、Bluemix 上で実行されているアプリに接続されます。
 

デプロイメント・ステップのフルサンプルを以下に示します。
最後のコマンドが `cf icd --create-connection` であることに注意してください。
 

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

Jenkins 統合のドキュメンテーションで説明されているように、CloudFoundry CLI と CloudFoundry ICD のプラグインが Jenkins サーバー上にインストールされていることが必要です。
そのサーバーから Bluemix にログインして接続する必要もあります。


## 宣言パイプラインのサンプル

宣言 Jenkinsfile として定義されているパイプライン全体を、サンプルとして以下に示します。
 

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










