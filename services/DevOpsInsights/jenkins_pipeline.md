---

copyright:
  years: 2016, 2017
lastupdated: "2017-05-11"

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}
{:tip: .tip}

# Integrating with Jenkins Pipeline

After you add {{site.data.keyword.DRA_full}} to an open toolchain and define the policies that it monitors, you can integrate it with a Jenkins Pipeline project. You define a pipeline in the Jenkins web interface or in a _Jenkinsfile_ that you store in your source control repository. You can view and administer Jenkins Pipelines projects from the Jenkins web interface. 

The IBM Cloud DevOps plugin for Jenkins integrates Jenkins projects with toolchains. A _toolchain_ is a set of tool integrations that support development, deployment, and operations tasks. The collective power of a toolchain is greater than the sum of its individual tool integrations. Open toolchains are part of the {{site.data.keyword.contdelivery_full}} service. To learn more about the {{site.data.keyword.contdelivery_short}} service, see [its documentation](https://console.ng.bluemix.net/docs/services/ContinuousDelivery/cd_about.html). 

After you install the IBM Cloud DevOps plugin, you can configure your Jenkins project to publish test results to {{site.data.keyword.DRA_short}}, automatically evaluate build quality at gates, and track your deployment risk. You can also send job notifications to other tools in your toolchain, such as Slack and PagerDuty. To help you track deployments, the toolchain can add deployment messages to Git commits and their related Git or JIRA issues. You can also view your deployments on the toolchain's Connections page. 

The plugin provides post-build actions and CLIs to support the integration. {{site.data.keyword.DRA_short}} aggregates and analyzes the results from unit tests, functional tests, code coverage tools, static security code scans, and dynamic security code scans to determine whether your code meets predefined policies at gates in your deployment process. If your code does not meet or exceed a policy, the deployment is halted, preventing risky changes from being released. You can use {{site.data.keyword.DRA_short}} as a safety net for your continuous delivery environment, a way to implement and improve quality standards over time, and a data visualization tool to help you understand your project's health.

This topic assumes that you are at least somewhat familiar with Jenkins Pipeline. If you are not, [see the Jenkins Pipeline documentation](https://jenkins.io/doc/book/pipeline/) before continuing.

## Prerequisites
{: #jenkins_prerequisites}

You must have access to a server that is running a Jenkins Pipeline project. 

## Creating a toolchain
{: #jenkins_create}

Before you can integrate {{site.data.keyword.DRA_short}} with a Jenkins project, you must create a toolchain. 

1. To create a toolchain, go to the [Create a Toolchain page](https://console.ng.bluemix.net/devops/create) and follow the instructions on that page. 

2. After you create the toolchain, add {{site.data.keyword.DRA_short}} to it. For instructions, see the [{{site.data.keyword.DRA_short}} documentation](https://console.ng.bluemix.net/docs/services/DevOpsInsights/index.html). 

## Installing the plugin
{: #jenkins_install}

First, install the plugin on your Jenkins server. Open the server interface, and then:

1. Click **Manage Jenkins**.
2. Click **Manage Plugins**. 
3. Click the **Available** tab
4. Filter for `IBM Cloud DevOps`. 
5. Select IBM Cloud DevOps.
6. Click **Download now and install after restart**. 

The plugin is available after the server restarts.  

## Creating a pipeline
{: #jenkinsfile_create}

You define pipelines either in the Jenkins project configuration menu or in a Jenkinsfile in your repository. To proceed, create or open an existing script or Jenkinsfile to use with {{site.data.keyword.DRA_short}}. You can follow the [declarative](https://jenkins.io/doc/book/pipeline/syntax/#declarative-pipeline) or [scripted](https://jenkins.io/doc/book/pipeline/syntax/#scripted-pipeline) formats.

## Exposing required environment variables

Next, open the pipeline definition. 

In the definition, add the following environment variables. These variables are required for the pipeline to integrate with {{site.data.keyword.DRA_short}}.

| Environment variable        | Definition    |
| ----------------------------|---------------|
| `IBM_CLOUD_DEVOPS_CREDS`    | Bluemix credentials that you define in Jenkins by using the `credentials` command. For example, `IBM_CLOUD_DEVOPS_CREDS = credentials('BM_CRED')`. Setting the variable with this command sets two additional environment variables automatically: `IBM_CLOUD_DEVOPS_CREDS_USR` and `IBM_CLOUD_DEVOPS_CREDS_PSW` for the user name and password, respectively.  |
| `IBM_CLOUD_DEVOPS_ORG`      | The Bluemix organization that your toolchain belongs to.     |
| `IBM_CLOUD_DEVOPS_APP_NAME` | The name of the application that your toolchain deploys.   |
| `IBM_CLOUD_DEVOPS_TOOCLHAIN_ID` | The ID of your toolchain. Open the toolchain Overview and see the URL to determine the ID. The toolchain URL format is `https://console.ng.bluemix.net/devops/toolchains/[YOUR_TOOLCHAIN_ID]`.   |
| `IBM_CLOUD_DEVOPS_WEBHOOKURL` | The webhook that you were provided when you added Jenkins to your toolchain.   |

See the [Jenkins pipeline documentation](https://jenkins.io/doc/pipeline/tour/environment/#credentials-in-the-environment) for more information about the `credentials` command. 
{: tip}

If you are using the the scripted pipeline format, set your credentials with `withCredentials` and your environment with `withEnv` instead of `credentials` and `environment`, which are used in the example below. See [the Jenkins documentation](https://jenkins.io/doc/pipeline/steps/credentials-binding/) for more about `withCredentials`.
{: tip} 

These environment variables and credentials are used by the IBM Cloud DevOps plugin to interact with DevOps Insights. Here is an example of setting them in the declarative pipeline format. 

```
environment {
        IBM_CLOUD_DEVOPS_CREDS = credentials('BM_CRED')
        IBM_CLOUD_DEVOPS_ORG = 'dlatest'
        IBM_CLOUD_DEVOPS_APP_NAME = 'Weather-App'
        IBM_CLOUD_DEVOPS_TOOLCHAIN_ID = '1111111-aaaa-2222-bbbb-333333333'
        IBM_CLOUD_DEVOPS_WEBHOOK_URL = 'https://jenkins:5a55555a-a555-5555-5555-a555aa55a555:55555555-5555-5555-5555-555555555555@devops-api.ng.bluemix.net/v1/toolint/messaging/webhook/publish'
    }
```


## Adding Cloud DevOps steps
The Cloud DevOps plugin adds four steps to Jenkins pipelines for you to use. Use these steps in your pipelines to interact with DevOps Insights. 

* `publishBuildRecord`, which publishes build information to DevOps Insights
* `publishTestResult`, which publishes test results to DevOps Insights
* `publishDeployRecord`, which publishes deployment records to DevOps Insights
* `evaluateGate`, which enforces DevOps Insights policies 

Add these steps to your pipeline definition wherever you need them to run. For example, you might upload test results after running a test, and then evaluate those results at a gate after they are uploaded. 

### Publishing build records

Publish build records with the `publishBuildRecord` step. This step requires four parameters.

| Parameter        | Definition    |
| ----------------------------|---------------|
| `gitBranch`    | The name of the Git Branch that the build uses.  |
| `gitCommit`      | The Git commit ID that the build uses.    |
| `gitRepo` | The URL of the Git repository.   |
| `result` | The result of the build stage. The value should be `SUCCESS` or `FAIL`.   |

Here are the parameters in an example command:

```
publishBuildRecord gitBranch: "${GIT_MASTER}", gitCommit: "${GIT_COMMIT}", gitRepo: "https://github.com/username/reponame", result:"SUCCESS"
```

Jenkins Pipeline does not expose Git information as environment variables. You can get the Git commit ID by using the command `sh(returnStdout: true, script: 'git rev-parse HEAD').trim()`.
{: tip}

### Publishing test results
Publish build records with the `publishTestResult` step. This step requires two parameters.

| Parameter        | Definition    |
| ----------------------------|---------------|
| `type`    | The type of test result. The value of this must be `unittest` for unit tests, `fvt` for functional verification tests, or `code` for code coverage tests.  |
| `fileLocation`      | The test result file's location.    |

Here are the parameters in example commands. The first command publishes Mocha unit test results, and the second command publishes code coverage test results. 

```
publishTestResult type:'unittest', fileLocation: './mochatest.json'
publishTestResult type:'code', fileLocation: './tests/coverage/reports/coverage-summary.json'
```

### Publishing deployment records

Publish deployment records with the `publishDeployRecord` step. This step requires two parameters. It can also accept one optional parameter. 

| Parameter        | Definition    |
| ----------------------------|---------------|
| `environment`    | The environment that you deploy your app to. For DevOps Insights to work properly, you must identify one environment as `STAGING` and another environment as `PRODUCTION`. |
| `result`      | The result of the build stage. The value should be `SUCCESS` or `FAIL`.    |
| `appUrl`      | _Optional_: The URL used to access your application.    |

Here are the parameters in example commands. The first command publishes the deployment record for a staging environment; the second command publishes the deployment record for a production environment.

```
publishDeployRecord environment: "STAGING", appUrl: "http://staging-Weather-App.mybluemix.net", result:"SUCCESS"
publishDeployRecord environment: "PRODUCTION", appUrl: "http://Weather-App.mybluemix.net", result:"SUCCESS"
```

### Adding gates

Add gates to your pipeline by using the `evaluateGate` command. Gates enforce DevOps Insights policies, which set test requirements for build promotion. 

This step requires one parameters. It can also accept one optional parameter. 

| Parameter        | Definition    |
| ----------------------------|---------------|
| `policy`    | The name of the policy that the gate implements. The policy's name is defined in DevOps Insights. |
| `forceDecision`      | _Optional_: Whether or not the pipeline stops depending on the gate's decision. Set this parameter to `true` to stop the pipeline from running if the gate fails. Set it to `false` to allow the pipeline to continue after a gate failure. By default, the value is `false`.     |

Here are the parameters in an example command. In this command, the pipeline will continue running regardless of the gate's decision. 

```
evaluateGate policy: 'Weather App Policy', forceDecision: 'true'
```

### Communicating with toolchains

Send pipeline status to Bluemix toolchains by using the `notifyOTC` command. To learn more about integrating Jenkins with toolchains, [see the documentation](https://console.ng.bluemix.net/docs/services/ContinuousDelivery/toolchains_integrations.html#jenkins). You can disregard steps 6d through 6f, as they only apply to freeform Jenkins projects.

This step requires two parameters and can take an additional optional one. 

| Parameter        | Definition    |
| ----------------------------|---------------|
| `stageName`    | The current pipeline stage's name. |
| `status`    | The current pipeline stage's status. Using `SUCCESS`, `FAILURE`, or `ABORTED` will automatically trigger color highlighting in Slack.  |
| `webhookUrl`      | _Optional_: The webhook URL that is shown on your toolchain's Jenkins tile. If you include this parameter, its value overrides that of the `IBM_CLOUD_DEVOPS_WEBHOOKURL` environment variable.   |

Here are examples of using the `notifyOTC` step in both declarative and scripted pipeline defintions:

#### Declarative Pipeline Example:
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

#### Scripted Pipeline Example:
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

In both of the examples, note that the toolchain webhook URL is overrided only in case of failure. 

## Ensuring traceability across toolchain integrations

Configure your Jenkins environment to integrate with your Bluemix toolchain by following the instructions in [the Bluemix Docs](https://console.ng.bluemix.net/docs/services/ContinuousDelivery/toolchains_integrations.html#jenkins). You can disregard steps 6d through 6f, as they only apply to freeform Jenkins projects.

Integrating with a toolchain gives you end to end traeceability and deployment mapping. After you follow the integration instructions, add the command `cf icd --create-connection $IBM_CLOUD_DEVOPS_WEBHOOK_URL $CF_APP_NAME` after your deployment steps. This command connects your Jenkins integration to an app that is running on Bluemix. 

Here is an example of a deployment step in full. Note that the last command is `cf icd --create-connection`. 

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

As described in the Jenkins integration documentation, you must have the CloudFoundry CLI and CloudFoundry ICD plugins installed on your Jenkins server. You also need to log in to Bluemix from the server to connect with it.

## An example declarative pipeline

As an example, here is a complete pipeline defined as a declarative Jenkinsfile. 

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







