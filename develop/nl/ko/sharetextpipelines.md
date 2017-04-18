---

copyright:
  years: 2015, 2016
lastupdated: "2016-12-21"

---

{:shortdesc: .shortdesc}
{:screen: .screen}
{:new_window: target="_blank"}
{:codeblock: .codeblock}

# {{site.data.keyword.jazzhub_short}} 샘플 프로젝트에서 텍스트 기반 파이프라인 공유 {: #share-pipeline}

{{site.data.keyword.Bluemix_notm}}에 배치 단추를 통해 {{site.data.keyword.Bluemix_notm}}에 배치된 샘플 프로젝트의 경우 {{site.data.keyword.jazzhub_short}} 파이프라인 구성을 YAML 파일로 정의할 수 있습니다. 프로젝트를 분기 실행하는 사용자가 고유 파이프라인을 구성할 필요가 없도록 텍스트로 정의된 파이프라인을 공유할 수 있습니다. 이 기능은 개발 중입니다. YAML 형식과 구현은 언제든 변경될 수 있습니다. 현재 이 기능은 {{site.data.keyword.Bluemix_notm}}를 대상으로 하는 Git 및 GitHub 저장소가 있는 프로젝트에서만 사용할 수 있습니다.
{: shortdesc} 

샘플 프로젝트의 루트 디렉토리에는 `pipeline.yml` 파일이 포함된 `.bluemix`라는 폴더가 있습니다.

{{site.data.keyword.Bluemix_notm}}에 배치 단추를 사용하여 프로젝트를 복제하는 경우, {{site.data.keyword.jazzhub_short}}에서 `pipeline.yml` 파일을 기반으로 하는 파이프라인을 작성합니다. 

예:  
``` 
<sample root>
	.bluemix
		pipeline.yml
	<other sample content>
```
{: codeblock} 

YAML 파일 형식은 파이프라인 사양을 포함하는 단일 YAML 문서입니다. 다음 샘플 {{site.data.keyword.jazzhub_short}} 파이프라인은 한 단계에서 Ant 포함 Java 앱을 빌드합니다. 그런 다음 다른 단계에서 파이프라인이 앱을 {{site.data.keyword.Bluemix_notm}}에 배치합니다. 

``` 
---
stages:
- name: Build Stage
  inputs:
  - type: git
    branch: master
  triggers:
  - type: commit
  properties:
  - name: APP_VERSION
    value: '1.0'
    type: text
  jobs:
  - name: Build
    type: builder
    artifact_dir: output
    build_type: ant
    script: |-
      #!/bin/bash
      ant
    enable_tests: true
    test_file_pattern: tests/TEST-*.xml
- name: Deploy Stage
  inputs:
  - type: job
    stage: Build Stage
    job: Build
  triggers:
  - type: stage
  jobs:
  - name: Deploy to dev
    type: deployer
    target:
      url: https://api.ng.bluemix.net
      organization: uateam@ca.ibm.com
      space: dev
      application: JavaSampleUnitTest
    script: |
      cf push "${CF_APP}"
      # View logs
      #cf logs "${CF_APP}" --recent
```
{: codeblock} 

## YAML 파일 구문 {: #yaml-syntax}

파이프라인은 다음 구문을 사용하여 텍스트로 표시할 수 있습니다.

Pipeline: 
```
---
stages:
<sequence of stages>
```
{: codeblock} 

Stage:  
```
---
name: <name>
[inputs: 
	<sequence of inputs>] 
[triggers:   
	<sequence of triggers>] 
[properties:   
	<sequence of properties>] 
[jobs:   
	<sequence of jobs>]
```
{: codeblock} 

Input: 
```
type: 'git' | 'job'
[branch: <branch name>] ;only for Git inputs
stage: <stage name>		  ;only for job inputs
job: <job name>			   	;only for job inputs
```
{: codeblock} 

Trigger: 
```
type: 'commit' | 'stage'
[enabled: 'true | 'false'] ;true is assumed if not specified
```
{: codeblock} 	
	
Property: 
```
name: <property name>
value: <property value>
[type: 'text' | 'secure' | 'text_area' | 'file'] ;text is assumed if not specified
```
{: codeblock} 

Job: 
```
[name: <job name>]
type: 'builder' | 'deployer' | 'tester'
fail_stage: 'true' | 'false'
[extension_id: <extension id>] ;extension jobs only
[working_dir: <working dir path>] ;builder and tester only
[artifact_dir: artifact path>] ;builder only
[build_type: <build type>] ;builder only
[script: <script>] ;not for extension jobs
[enable_tests: 'true' | 'false'] ;builder and tester only
[test_file_pattern: <pattern>] ;builder and tester only
[target: <target>] ;deployer and extension jobs only
*[<extension property name>: <value>] ;extension jobs only
```
{: codeblock} 

Target: 
```
url: <target url>
organization: <org name>
space: <space name>
[application: <application name>]
```
{: codeblock} 

## 확장 작업 및 확장 정의 {: #extension-jobs} 

확장 정의는 확장 작업에 사용 가능한 특성 세트를 정의합니다. `extension_id ` 특성이 지정된 경우 작업이 확장 작업으로 처리됩니다. 확장에 사용 가능한 특성을 찾으려면 해당 문서를 참조하십시오. 

## YAML 파일을 사용하여 파이프라인과 상호작용 {: #pipeline-yaml} 

**환경 변수 및 해상도** 
<!-- Formating for this? -->

`pipeline.yml`파일에서 파이프라인을 작성하기 전에 {{site.data.keyword.Bluemix_notm}}에 배치 기능은 파일 내의 환경 변수를 사용자가 {{site.data.keyword.Bluemix_notm}} 인터페이스(예: 사용자의 조직)에서 지정하는 정보로 대체합니다. YAML 값은 모두 환경 변수로 구성된 경우에만 대체됩니다. 

```
{
  "project_id": "_ljkahfliasdlk",
  "env": {
     "CF_ORGANIZATION" : "user@se.ibm.com"
  },
  "config": {
    "format" : "yaml",
    "content" : "
      ...
        target:
          url: http://api.ng.bluemix.net
          organization: ${CF_ORGANIZATION}
        script: \"echo ${CF_ORGANIZATION}\"
      ...
    "
  }
}
```
{: codeblock} 

이 예에서 대상 조직은 대상 URL에 따라 분석되며 파이프라인 구성에 유지되는 값은 조직 GUID입니다. 배치 스크립트에서 있는 값은 대체되지 않습니다.

대상 URL은 환경 변수 또는 실제 값으로 지정되어야 하며, 조직 및 영역의 GUID나 이름이 제공되어야 합니다. 한 값이 제공되면 다른 값도 대체됩니다.

변수 | 설명 
---------------- | ---------------- 
CF_TARGET_URL |	Bluemix 대상 URL
CF_ORGANIZATION	| 조직 이름
CF_ORGANIZATION_ID	| 조직 GUID
CF_SPACE |	영역 이름
CF_SPACE_ID |	영역 GUID
CF_APP	| 앱 이름
{: caption="표 1. 환경 변수" caption-side="top"}

**파이프라인에서 YAML 파일 생성** 

파이프라인에서 YAML 파일을 생성할 수 있습니다. 

다음 형식의 URL을 사용하여 기존 파이프라인에서 파일을 생성하십시오.

```
<DevOps Services domain>/pipeline/user/project/yaml
```
{: codeblock} 

이 호출에는 승인 헤더가 필요하지 않습니다. 이 호출은 브라우저에서 사용할 수 있습니다. 

**참고:** 안전을 위해 생성된 파이프라인 YAML 파일에서 secure-stage 환경 특성 값은 생략됩니다. 
