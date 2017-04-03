---

copyright:
  years: 2017
lastupdated: "2017-03-17"

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}
{:note:.deprecated}

# 문제점 해결
{: #ts}

{{site.data.keyword.dev_cli_notm}}의 몇 가지 알려진 문제가 임시 해결책과 함께 기록되어 있습니다.
{:shortdesc}

<!-- Add a headings and paragraphs about troubleshooting for your service, or a list of known issues and workarounds. -->

## 알려진 문제
{: #knownissues}

다음 절에는 알려진 문제와 가능한 해결책이 설명되어 있습니다. 


### 비모바일 패턴을 사용하여 프로젝트를 작성하는 중에 hostname is taken 오류 발생
{: #hostname}

웹 앱, BFF 또는 마이크로서비스 패턴으로부터 프로젝트를 작성하는 데 {{site.data.keyword.dev_cli_short}}을 사용하는 경우 다음 오류가 표시될 수 있습니다. 

```
The hostname <myHostname> is taken.
```
{: codeblock}


#### 원인
{: #hostname-cause}
   
이 오류는 만료된 로그인 토큰으로 인해 발생합니다. 


#### 해결
{: #hostname-resolution}

다시 로그인하십시오. 

```
bx login
```
{: codeblock}


### {{site.data.keyword.dev_cli_short}}의 일반적 실패
{: #general}

{{site.data.keyword.dev_cli_short}} create, delete, list 또는 code 명령을 사용하는 경우 다음 오류가 표시될 수 있습니다. 

```
Failed to <command> project.
```
{: codeblock}


#### 원인
{: #hostname-cause}
   
이 오류는 만료된 로그인 토큰으로 인해 발생합니다. 


#### 해결
{: #hostname-resolution}

다시 로그인하십시오. 

```
bx login
```
{: codeblock}


### {{site.data.keyword.objectstorageshort}} 기능 추가 중 서비스 브로커 오류 발생
{: #os}

{{site.data.keyword.objectstorageshort}} 기능이 있는 두 프로젝트를 작성하는 데 {{site.data.keyword.dev_cli_short}}을 사용하는 경우 다음 오류가 표시될 수 있습니다. 

```
FAILED
Service broker error: {"description"=>"You can not create this Object Storage instance. Each organization using the Object Storage service is limited to one instance of the Free plan."}
```
{: codeblock}


#### 원인
{: #os-cause}
   
이 오류는 하나의 {{site.data.keyword.objectstorageshort}} 무료 플랜 인스턴스만을 허용하는 {{site.data.keyword.objectstorageshort}} 서비스로 인해 발생합니다. 


#### 해결
{: #os-resolution}

이 오류를 방지하기 위해 다른 플랜을 선택하라는 프롬프트가 표시됩니다. 


### 프로젝트 작성 중 코드 가져오기 실패
{: #code}

프로젝트를 작성하는 데 {{site.data.keyword.dev_cli_short}}을 사용하는 경우 다음 오류가 표시될 수 있습니다. 
	
```
FAILED                            
Project created, but could not get code
https://console.ng.bluemix.net/developer/projects/b22165f3-cbc6-4f73-876f-e33cbec199d4/code
```
{: codeblock}
	

#### 원인
{: #code-cause}

이 오류는 내부 제한시간 초과로 인해 발생합니다. 
	

#### 해결
{: #code-resolution}

다음 방법 중 하나를 사용하여 코드를 가져올 수 있습니다. 

* CLI를 사용하여 다음 명령을 실행합니다. 

	```
	bx dev code <your-project-name>
	```
	{: codeblock}
	
	`<your-project-name>`은 프로젝트 작성 중에 사용한 프로젝트 이름으로 대체해야 합니다. 

* {{site.data.keyword.dev_console}}을 사용합니다. 

	1. {{site.data.keyword.dev_console}}에서 [프로젝트 ![외부 링크 아이콘](../icons/launch-glyph.svg "외부 링크 아이콘")](https://console.{DomainName}/developer/projects)를 선택하고 **코드 가져오기**를 클릭하십시오. 

	2. **코드 생성**을 클릭하십시오. 

	3. 코드가 생성되면 **코드 다운로드**를 클릭하십시오. 


### Node.js 프로젝트에 대한 `bx dev run` 실행 오류
{: #node}

Node.js Web 또는 BFF 프로젝트의 {{site.data.keyword.dev_cli_short}}에 대해 `bx dev run`을 실행하는 경우 다음 오류가 표시될 수 있습니다. 

```
module.js:597
  return process.dlopen(module, path._makeLong(filename));
                 ^

Error: /app/node_modules/bluemix-autoscaling-agent/node_modules/appmetrics/appmetrics.node: invalid ELF header
    at Error (native)
    at Object.Module._extensions..node (module.js:597:18)
    at Module.load (module.js:487:32)
    at tryModuleLoad (module.js:446:12)

    at Function.Module._load (module.js:438:3)
    at Module.require (module.js:497:17)
    at require (internal/module.js:20:19)
    at Object.<anonymous> (/app/node_modules/bluemix-autoscaling-agent/node_modules/appmetrics/index.js:25:13)
    at Module._compile (module.js:570:32)
    at Object.Module._extensions..js (module.js:579:10)
```
{: codeblock}


#### 원인
{: #node-cause}
   
이 오류는 `appmetrics` 모듈이 다른 아키텍처에 설치되어 발생합니다. 한 아키텍처에 설치된 네이티브 npm 모듈은 다른 아키텍처에서 작동하지 않습니다. 포함된 Docker 이미지는 Linux 커널을 기반으로 합니다. 


#### 해결
{: #node-resolution}

`node_modules` 폴더를 삭제하고 `bx dev run`을 다시 실행하십시오. 


<!--
## Troubleshooting techniques
{: #tstechniques}
-->

<!-- Add a heading and content for how to get help and support. Use this template for beta and GA services:  -->


## 도움 및 지원 받기
{: #gettinghelp}

{{site.data.keyword.Bluemix_notm}} {{site.data.keyword.dev_console}} 또는 {{site.data.keyword.dev_cli_notm}} 사용 중에 문제점이 있거나 질문이 있는 경우에는 정보를 검색하거나 포럼에 질문하여 도움을 받을 수 있습니다. 또는 지원 티켓을 열 수도 있습니다. 

포럼을 통해 질문하는 경우 {{site.data.keyword.Bluemix_notm}} 개발 팀이 볼 수 있도록 질문에 태그를 지정하십시오. 

<!--Insert the appropriate Stack Overflow tag for your service for <service_keyword> in URL and text below:  -->

{{site.data.keyword.dev_console}} 또는 {{site.data.keyword.dev_cli_notm}}을 사용하여 앱을 개발하거나 배치하는 데 대한 기술 관련 질문이 있는 경우:

* 질문을 [Stack Overflow ![외부 링크 아이콘](../icons/launch-glyph.svg "외부 링크 아이콘")](http://stackoverflow.com/search?q=bluemix-dev-services+ibm-bluemix)에 게시하고 질문에 `bluemix-dev-services` 및 `ibm-bluemix` 태그를 지정하십시오. 
* 질문을 [Slack ![외부 링크 아이콘](../icons/launch-glyph.svg "외부 링크 아이콘")](http://ibm-cloud-tech.slack.com/)의 `bluemix-dev-services` 채널에 게시하십시오. [지금 등록 ![외부 링크 아이콘](../icons/launch-glyph.svg "외부 링크 아이콘")](http://ibm.biz/IBMCloudNativeSlack)하십시오. 


<!--Insert the appropriate dW Answers tag for your service for <service_keyword> in URL below:  -->
<!--
* For questions about the service and getting started instructions, use the [IBM developerWorks dW Answers ![External link icon](../icons/launch-glyph.svg "External link icon")](https://developer.ibm.com/answers/topics/bluemix-dev-services/?smartspace=bluemix) forum. Include the  "bluemix-dev-services" and "bluemix" tags.
* -->

포럼 사용에 대한 세부사항은 [도움 받기 ![외부 링크 아이콘](../icons/launch-glyph.svg "외부 링크 아이콘")](/docs/support/index.html#getting-help)를 참조하십시오. 

{{site.data.keyword.IBM}} 지원 티켓 열기, 또는 지원 레벨 및 티켓 심각도에 대한 정보는 [지원 문의 ![외부 링크 아이콘](../icons/launch-glyph.svg "외부 링크 아이콘")](/docs/support/index.html#contacting-support)를 참조하십시오. 

<!--Add a heading and content for how to get help. (Support not available for experimental.) Use this template for experimental services:  -->

