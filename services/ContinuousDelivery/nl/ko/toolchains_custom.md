---

copyright:
  years: 2016

---
{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}


# 사용자 정의 도구 체인 설정(시범)
{: #toolchains-custom}
마지막 업데이트 날짜: 2016년 4월 27일
{: .last-updated}

사용자 정의 도구 체인을 작성하면 DevOps 워크플로우를 개선하는 데 유용합니다. 기존 도구 체인 템플리트 중 하나를 빨리 시작하거나 템플리트 중 하나를 사용자 정의해서 사용자 조정된 도구 체인을 작성하여 시작할 수 있습니다.
{:shortdesc}

여러 가지 방법으로 [도구 체인 작성 및 배치](https://daily-console.stage1.ng.bluemix.net/docs/toolchains/toolchains_setup.html){: new_window}를 수행할 수 있습니다. 이 안내서에서는 [{{site.data.keyword.Bluemix_notm}}에 배치](https://daily-console.stage1.ng.bluemix.net/docs/develop/deploy_button.html){: new_window} 단추를 사용하여 배치할 수 있는 사용자 정의 도구 체인을 작성하는 단계에 대해 설명합니다. 몇몇 구성을 수행한 후 {{site.data.keyword.Bluemix_notm}}에서 GitHub 프로젝트를 배치 가능한 도구 체인과 간편하게 공유할 수 있습니다.


## 시작하기
{: #toolchains_custom_gettingstarted}

사용자 정의 도구 체인을 작성하기 위해 먼저 도구 체인 템플리트를 복제합니다. 기존 템플리트를 복제하면 사용자 정의를 시작할 수 있는 시작점이 빨리 제공됩니다.

1. 선택한 Git 클라이언트를 사용하여 다음 명령을 입력해 [단순 도구 체인](https://github.com/open-toolchain/simple-toolchain){: new_window} 템플리트를 GitHub에서 복제하십시오.

 ```
 git clone https://github.com/open-toolchain/simple-toolchain.git
 ```
 {: pre}

 이 템플리트는 단일 GitHub 저장소에서 기본 Hello World 애플리케이션을 배치하며 Continuous Delivery, 소스 제어, 문제 추적, 온라인 편집을 수행할 수 있게 사전 구성된 단순 도구 체인을 포함합니다.

2. **(선택사항)**: 복잡한 도구 체인 템플리트를 사용하여 시작하는 것을 선호하는 경우에는 [마이크로서비스용 클라우드 고유 도구 체인](https://github.com/open-toolchain/toolchain-demo){: new_window}을 복제하여 시작할 수 있습니다.

 ```
 git clone https://github.com/open-toolchain/toolchain-demo.git
 ```
 {: pre}

 이 템플리트는 세 개의 마이크로서비스로 구성된 온라인 상점을 배치하며 각 마이크로서비스는 해당 GitHub 저장소에 있습니다. Continuous Delivery, 소스 제어, blue-green 배치, 기능 테스트, 문제 추적, 온라인 편집, 메시징을 수행할 수 있게 사전 구성된 복잡한 도구 체인도 포함되어 있습니다.

선택된 템플리트에 관계 없이 사용자 정의 도구 체인 작성에 대해 이 안내서에 간략히 설명된 프린시펄은 비슷합니다.

템플리트를 복제하면 도구 체인을 작동하는 데 필요한 모든 구성 파일이 포함된 `.bluemix` 디렉토리와 *Readme* 파일이 있는 기본 GitHub 저장소가 생깁니다. `.bluemix` 디렉토리에 최소한 다음 항목이 있어야 합니다.

* toolchain.yml
* deploy.json
* pipeline.yml

각 파일에 대해서는 도구 체인이 전개됨에 따라 추가해야 하는 몇몇 추가 구성과 함께 다음 섹션에서 설명합니다.

## 구성 파일 이해
{: #toolchains_custom_config_files}

도구 체인 템플리트 구성 파일은 기본적으로 YAML로 형식화된 파일로 구성됩니다. 각 파일에는 도구 체인의 여러 측면을 설명하는 메타데이터가 들어 있습니다. 여기에는 도구 체인에 대한 일반적인 구체적 정보, 포함할 GitHub 저장소, 코드를 빌드하는 방법과 코드를 배치할 위치에 대한 상세 정보, 도구 체인에 포함할 다양한 도구에 대한 구성 세부사항이 포함됩니다. 도구 체인이 복잡해지면 구성 파일도 복잡해집니다. 오류가 발생할 위험성을 줄이기 위해 파일을 올바른 형식으로 유지하는 것이 중요합니다.

YAML 파일에서 작업하는 경우 유념할 몇 가지 가이드라인은 다음과 같습니다.

* 탭은 허용되지 않습니다. 공백만 사용할 수 있습니다.
* 모든 특성과 목록을 하나 이상의 공백으로 들여쓰기해야 합니다.
* 모든 키와 특성은 대소문자를 구분합니다.

작업을 이중으로 검사하기 위해 이 [YAML 구문 분석기](http://wiki.ess3.net/yaml/){: new_window}와 같은 단순 YAML 유효성 검증기를 사용하여 해당 오류가 발생하지 않도록 할 수 있습니다.

  
## toolchain.yml
{: #toolchains_custom_toolchain_yml}

`toolchain.yml` 파일은 도구 체인의 핵심입니다. 가져올 저장소, 포함할 서비스, 빌드 상세 정보를 비롯한 도구 체인의 세부사항이 모두 이 파일에 설명되어 있습니다. 파일의 내용을 이해하기 위해 파일을 여러 섹션으로 구분할 수 있습니다.

1\. **도구 체인 소개 정보**

 이 섹션에서는 도구 체인 작성 페이지에서 사용자에게 표시되는 도구 체인에 대한 간략한 상세 정보를 제공합니다. 도구 체인의 용도와 배치되는 경우 수행할 작업에 대한 설명과 함께 도구 체인의 이름을 포함해야 합니다. 도구 체인에 대한 시각적 설명 또는 로고를 표시하는 이미지를 포함할 수도 있습니다.

 도구 체인에 대한 소개 컨텐츠를 제공하는 외에 이 섹션에는 도구 체인 작성 페이지에서 작성 시 구성할 수 있는 도구 통합을 정의하는 `required` 키도 포함될 수 있습니다. 작성 시 도구를 구성하도록 허용하면 쉽게 재사용하거나 용도를 재설정할 수 있는 도구 체인을 작성할 수 있습니다. 도구 체인 작성 페이지에서 구성할 수 있는 각 도구의 경우 `toolchain.yml` 파일에 정의된 대로 도구 상위 키를 `required` 키의 특성으로 추가하십시오.

 다음 스니펫은 이 섹션의 예를 표시합니다.

 ```
 ---
 name: "Simple Toolchain"
 description: "This Hello World application uses Node.js and includes a toolchain that is preconfigured for continuous delivery, source control, issue tracking, and online editing.\n\nTo get started, click **Create**."
 version: 0.1
 # Generate base64 representation of image at http://www.askapache.com/online-tools/base64-image-converter/
 image: data:image/png;base64,iVBORw0KGgoAAAANSUhEUgAAAY4AAA...
 required: 
  - deploy
  - hello-world-repo
  ```
 {: codeblock}

 **참고:** 먼저 [AskApache](http://www.askapache.com/online-tools/base64-image-converter/)와 같은 도구를 사용하여 이미지를 base-64 표시로 변환해야 합니다.

2\. **GitHub 저장소 정의**

 도구 체인은 여러 GitHub 저장소에 대한 Continuous Delivery를 제공할 수 있습니다. `toolchain.yml` 파일의 이 섹션에 각 저장소를 정의해야 합니다.

 시작하려면 도구 체인에 추가할 GitHub 저장소마다 다음 특성을 사용하여 GitHub 저장소의 이름을 나타내는 상위 키를 추가하십시오.

| 항목 | 키/특성 | 값 | 설명 |
|------|--------------|-------|-------------|
| repo-name | 키 |  | 저장소 이름 |
| service_id | 특성 | <`githubpublic`, `githubprivate`> | GitHub 저장소의 유형 |
| parameters: | 키 |  |  |
| repo_name | 특성 |  | **주석: 정의 방법** |
| repo_url | 특성 |  | GitHub 저장소의 URL |
| type | 특성 | <`new`, `fork`, `clone`, `link`> | 저장소 작성 방법 |
| has_issues | 특성 | <`true`, `false`> | GitHub 사용 문제 |

 **참고:** 여러 저장소를 정의하고 저장소를 `has_issues: true`로 구성하는 경우 GitHub 문제 추적기의 단일 인스턴스가 `true`로 설정된 모든 저장소의 문제를 추적할 도구 체인에 추가됩니다.

 다음 스니펫은 이 섹션의 예를 표시합니다.

 ```
 # Github repos
 hello-world-repo:
   service_id: githubpublic
   parameters:
 	repo_name: "hello-world-{{name}}"
 	repo_url: https://github.com/open-toolchain/node-hello-world
 	type: clone
 	has_issues: true
 ```
 {: codeblock}

3\. **파이프라인 정보**

 파이프라인을 통해 Continuous Delivery가 가능해집니다. 이 섹션에서는 각 GitHub 저장소에서 코드를 빌드하고 배치하는 데 사용되는 구성 세부사항을 정의합니다.

 시작하려면 도구 체인에서 정의된 GitHub 저장소마다 해당 파이프라인의 이름을 나타내는 상위 키를 추가하십시오. GitHub 저장소의 이름에서 이 키를 추출하는 것이 좋습니다. 다음 특성을 추가하십시오.

| 항목 | 키/특성 | 값 | 설명 |
|------|--------------|-------|-------------|
| pipeline-name | 키 |  | 파이프라인의 이름 |
| service_id | 특성 | <`pipeline`> | 사용할 서비스의 이름 |
| parameters | 키 |  |  |
| name | 특성 | <`repo_name`> | #Github 저장소 섹션에 정의된 이름과 동일함 |
| ui-pipeline | 특성 | <`true`, `false`> |  |
| configuration | 키 |  |  |
| content | 특성 | <`$file(pipeline.yml)`> | 파이프라인 정의를 정의하는 파일 |
| env | 키 |  |  |
| REPO_NAME | 키 | <`repo-name-key`> | GitHub 저장소 상위 키와 동일한 이름 |
| CF_APP_NAME |  특성 | <`"{{deploy.parameters.repo-name-key}}"`> | Cloud Foundry에서 사용되는 이름. GitHub 저장소 상위 키 이름을 포함해야 함 |
| PROD_SPACE_NAME | 특성 | <`"{{deploy.parameters.prod-space}}"`> | 배치할 {{site.data.keyword.Bluemix_notm}} 영역의 이름 |
| PROD_ORG_NAME | 특성 | <`"{{deploy.parameters.prod-organization}}"`> | 배치할 {{site.data.keyword.Bluemix_notm}} 조직의 이름 |
| PROD_REGION_ID | 특성 | <`"{{deploy.parameters.prod-region}}"`> | 배치할 {{site.data.keyword.Bluemix_notm}} 지역의 이름 |
| execute | 특성 | <`true`, `false`> | 작성 후 파이프라인 시작 |
| services | 특성 | <`repo-name-key`> |  GitHub 저장소 상위 키 |
| hidden | 특성 | <`[form, description]`> |  |

 `pipeline.yml` 파일 작성에 대한 정보는 [나중 섹션](#toolchains_custom_pipeline_yml)에 있습니다.

 다음 스니펫은 이 섹션의 예를 표시합니다.

 ```
 # Pipelines
 hello-world-build:
   service_id: pipeline
   parameters:
 	name: "hello-world-{{name}}"
 	ui-pipeline: true
 	configuration: 
 	 content: $file(hello-world.pipeline.yml)
 	 env:
 	  HELLO_WORLD_REPO: "hello-world-repo"
 	  CF_APP_NAME: "{{deploy.parameters.hello-world-name}}"
 	  PROD_SPACE_NAME: "{{deploy.parameters.prod-space}}"
 	  PROD_ORG_NAME: "{{deploy.parameters.prod-organization}}"
 	  PROD_REGION_ID: "{{deploy.parameters.prod-region}}"
 	 execute: true
 	services: ["hello-world-repo"]
   hidden: [form, description]
 ```
 {: codeblock}

4\. **배치 세부사항**

 Continuous Delivery 프로세스의 일부로 도구 체인을 배치하는 사용자가 액세스 권한을 갖고 있는 {{site.data.keyword.Bluemix_notm}} 지역, 조직 또는 영역에 애플리케이션을 배치하도록 도구 체인을 설정할 수 있습니다. 도구 체인 작성 페이지에서 애플리케이션을 배치할 위치에 대한 구체적인 세부사항을 선택할 수 있습니다.  

 ![Delivery Pipeline 구성 설정](images/deploy_configuration.png)

 `toolchain.yml` 파일의 이 섹션에서는 도구 체인 작성 페이지에서 구성하는 데 사용할 수 있는 파이프라인 단계를 정의합니다.

 시작하려면 상위 키 `deploy`를 사용하여 배치 구성 특성을 식별하십시오. 다음 특성이 나머지 섹션을 구성합니다.

| 항목 | 키/특성 | 값 | 설명 |
|------|--------------|-------|-------------|
| deploy | 키 |  | 배치 섹션의 이름 |
| schema | 특성 | <`deploy.json`> | 배치 세부사항을 구성하는 데 사용할 UI의 레이아웃을 정의하는 파일 |
| service-category | 특성 | <`pipeline`> | 배치 구성을 사용할 서비스 |
| parameters | 키 |  |  |
| prod-region | 특성 | <`"{{region}}"`> | 프로덕션 단계의 {{site.data.keyword.Bluemix_notm}} 지역 정의 |
| prod-organization | 특성 | <`"{{organization}}"`> | 프로덕션 단계의 {{site.data.keyword.Bluemix_notm}} 조직 정의 |
| prod-space | 특성 | <`prod`> | 프로덕션 단계의 {{site.data.keyword.Bluemix_notm}} 영역 정의 |
| github-repo-name | 특성 | <`"{{repo-name-key.parameters.repo_name}}"`> | GitHub 저장소 이름을 도구 체인 작성 페이지에 전달할 변수 |

 `deploy.json` 파일 작성에 대한 정보는 [나중 섹션](#toolchains_custom_deploy_json)에 있습니다.

 아래에 제공된 예제에서는 프로덕션 환경에 배치하는 단일 단계를 정의합니다.

 ```
 #Deployment
 deploy:
   schema: deploy.json
   service-category: pipeline
   parameters:
 	prod-region: "{{region}}"
 	prod-organization: "{{organization}}"
 	prod-space: prod
 	hello-world-name: "{{hello-world-repo.parameters.repo_name}}"
 ```
 {: codeblock}

 코드 예제는 대부분의 경우 그대로 사용될 수 있으며 약간만 수정하면 됩니다. 이 섹션을 사용자 정의하려면 `github-repo-name`을 저장소 이름과 일치하도록 업데이트해야 합니다. [`deploy.json`](#toolchains_custom_deploy_json) 파일 내의 세부사항도 업데이트해야 합니다.

 dev, QA, Prod 단계를 포함하는 복잡한 파이프라인을 작성하기 위해 `parameters` 키에서 다음 특성을 대체할 수 있습니다.

 ```
   parameters:
 	dev-region: "{{region}}"
 	qa-region: "{{region}}"
 	prod-region: "{{region}}"
 	dev-organization: "{{organization}}"
 	qa-organization: "{{organization}}"
 	prod-organization: "{{organization}}"
 	dev-space: dev
 	qa-space: qa
 	prod-space: prod
 ```
 {: codeblock}

5\. **도구 구성**

 도구 체인의 핵심 컴포넌트를 구성한 후 도구 체인에 추가 기능과 유용성을 추가하는 데 유용한 기타 도구 통합을 포함할 수 있습니다. 모든 도구에는 `toolchain.yml` 파일에 추가되어야 하는 항목이 있으며 일부 도구에는 `.bluemix` 디렉토리에 작성되어야 하는 별도의 YAML 구성 파일도 필요합니다.

 * **Slack**

	toolchain.yml
	```
	messaging:
	  service_id: slack
	  include: slack.yml
	```
	{: codeblock}
	
	slack.yml
	```
	---
	parameters:
	  api_token: ""
	  channel_name: ""
	```
	{: codeblock}
	
 * **Sauce Labs**

	toolchain.yml
	```
	test:
	  service_id: saucelabs
	  include: saucelabs.yml
	```
	{: codeblock}
	
	saucelabs.yml
	```
	---
	parameters:
	  username: ""
	  key: ""
	```
	{: codeblock}
	
 * **PagerDuty**

	toolchain.yml
	```
	alerting:
	  service_id: pagerduty
	  include: pagerduty.yml
	```
	{: codeblock}

	pagerduty.yml
	```
	---
	parameters:
	  site_name: ""
	  api_key: ""
	  service_name: ""
	  user_email: ""
	  user_phone: ""
	```
	{: codeblock}
	
 * **Eclipse Orion Web IDE**

	toolchain.yml
	```
	webide:
	  service_id: orion
	```
	{: codeblock}


## pipeline.yml
{: #toolchains_custom_pipeline_yml}

`pipeline.yml` 파일에는 파이프라인의 단계와 관련된 모든 구성 세부사항이 포함되어 있습니다. 두 가지 서로 다른 방법으로 `pipeline.yml` 파일을 작성할 수 있습니다.

1. `pipeline.yml` 파일을 수동으로 작성하십시오. `pipeline.yml` 파일 작성에 대한 세부사항과 구문은 [DevOps Services 샘플 프로젝트에서 텍스트 기반 파이프라인 공유](https://new-console.ng.bluemix.net/docs/develop/sharetextpipelines.html){: new_window}에 있습니다.

2. 기존 DevOps Services 프로젝트에서 `pipeline.yml` 파일을 생성하십시오. 다음과 같이 수행하십시오. 
	
	1. 새 [DevOps Services 프로젝트](https://hub.jazz.net/create){: new_window}를 작성하십시오.
	
	2. 프로젝트를 열고 **빌드 및 배치**를 클릭하십시오.
	
	3. 파이프라인에 필요한 모든 단계를 구성하십시오.
	
	4. 브라우저의 주소 표시줄에서 프로젝트의 URL에 `/yaml`을 추가하고 Enter를 누르십시오.
	
	5. 결과 `pipeline.yml` 파일을 GitHub 저장소의 `.bluemix` 디렉토리에 저장하십시오.

도구 체인에 둘 이상의 파이프라인이 있는 경우 각 `pipeline.yml` 파일에 고유한 이름을 제공하십시오.

다음은 `pipeline.yml` 파일의 예입니다.

```
---
stages:
- name: BUILD
  inputs:
  - type: git
	branch: master
	service: ${HELLO_WORLD_REPO}
  triggers:
  - type: commit
  jobs:
  - name: Build
	type: builder
- name: DEPLOY
  inputs:
  - type: job
	stage: BUILD
	job: Build
  triggers:
  - type: stage
  properties:
  - name: CF_APP_NAME
	value: undefined
	type: text
  - name: APP_URL
	value: undefined
	type: text
  jobs:
  - name: Deploy
	type: deployer
	target:
	  region_id: ${PROD_REGION_ID}
	  organization: ${PROD_ORG_NAME}
	  space: ${PROD_SPACE_NAME}
	  application: ${CF_APP_NAME}
	script: |
	  #!/bin/bash
	  # Push app
	  export CF_APP_NAME="$CF_APP"
	  cf push "${CF_APP_NAME}"
	  export APP_URL=http://$(cf app $CF_APP_NAME | grep urls: | awk '{print $2}')
	  # View logs
	  #cf logs "${CF_APP_NAME}" --recent
```
{: codeblock}		


## deploy.json
{: #toolchains_custom_deploy_json}

도구 체인 작성 페이지의 구성 가능한 통합 섹션에서 Delivery Pipeline을 선택하면 섹션이 펼쳐져 해당 도구에 적합하게 구성할 수 있는 다음 항목이 표시됩니다.

	* 애플리케이션 이름
	* 파이프라인 단계에서도 배치할 지역, 조직, 영역

![Delivery Pipeline 구성 설정](images/deploy_configuration.png)

UI에서 이 섹션의 레이아웃은 `deploy.json` 스키마로 정의됩니다.

스키마에서 사용자 애플리케이션의 세부사항과 일치하도록 다음 특성을 업데이트해야 합니다.

	* Title
	* Description
	* LongDescription
	* `hello-world-name`의 모든 인스턴스와 연관 세부사항을 사용자 애플리케이션과 일치하도록 수정해야 합니다.

다음은 `deploy.json` 파일의 예입니다.

```
{
    "$schema": "http://json-schema.org/draft-04/schema#",
    "title": "Hello World Deploy Stage",
    "description": "hello-world simple toolchain",
    "longDescription": "The Delivery Pipeline for Devops Services allows you to automate your continuous deployment setup hello-world.",
    "type": "object",
    "properties": {
        "prod-region": {
            "description": "The bluemix region",
            "type": "string"
        },
        "prod-organization": {
            "description": "The bluemix org",
            "type": "string"
        },
       "prod-space": {
            "description": "The bluemix space",
            "type": "string"
        },
       "hello-world-name": {
            "description": "hello world app name",
            "type": "string"
        }
    },
    "required": ["prod-region", "prod-organization", "prod-space", "hello-world-name"],
    "form": [
       {
          "type": "validator",
          "url": "/devops/setup/bm-helper/helper.html"
       },        
        {
          "type": "text",
          "readonly": false,
          "title": "Hello World App Name",
          "key": "hello-world-name"
        },
        {
            "type": "table",
            "columnCount": 4,
            "widths": ["15%", "28%", "28%", "28%"],
            "items": [
                {
                  "type": "label",
                  "title": ""
                },
                {
                  "type": "label",
                  "title": "Region"
                },
                {
                  "type": "label",
                  "title": "Organization"
                },
                {
                  "type": "label",
                  "title": "Space"
                },
                {
                  "type": "label",
                  "title": "Prod Stage"
                },
                {
                  "type": "select",
                  "key": "prod-region"
                },
                {
                  "type": "select",
                  "key": "prod-organization"
                },
                {
                  "type": "select",
                  "key": "prod-space",
                  "readonly": false
                }
            ]
        }
    ]
}
```
{: codeblock}
