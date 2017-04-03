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

# {{site.data.keyword.dev_cli_short}}
{: #developercli}	

{{site.data.keyword.dev_cli_long}}은 `dev` 플러그인을 사용하여 웹 프로젝트를 작성하고 개발하고 배치할 수 있는 확장 가능한 명령 중심 접근법을 제공합니다. 이는 엔드-투-엔드 마이크로서비스 애플리케이션을 개발할 때 명령행 제어를 사용하고자 하는 개발자에게 적합합니다. 

{: shortdesc}

{{site.data.keyword.dev_cli_notm}}은 애플리케이션 빌드 및 테스트를 위해 두 개의 컨테이너를 사용합니다. 첫 번째는 애플리케이션을 빌드하고 테스트하는 데 필요한 유틸리티를 포함하는 도구 컨테이너입니다. 이 컨테이너에 대한 Dockerfile은 [dockerfile-tools](#command-parameters) 매개변수에 의해 정의됩니다. 이는 일반적으로 특정 런타임의 개발에 유용한 도구를 포함하고 있으므로 개발 컨테이너라 생각할 수도 있습니다. 

두 번째 컨테이너는 실행 컨테이너입니다. 이 컨테이너는 {{site.data.keyword.Bluemix}} 등에서 사용할 수 있도록 배치하는 데 적합한 양식입니다. 따라서 이 컨테이너에는 일반적으로 애플리케이션을 시작하는 시작점이 정의됩니다. {{site.data.keyword.dev_cli_short}}을 통해 애플리케이션을 실행하도록 선택하면 이 플러그인은 이 컨테이너를 사용합니다. 이 컨테이너에 대한 Dockerfile은 [dockerfile-run](#run-parameters) 매개변수에 의해 정의됩니다. 


## {{site.data.keyword.dev_cli_notm}} 추가
{: #add-cli}


### 전제조건
{: #prereq}

{{site.data.keyword.dev_cli_short}}은 확장성이 높으며 추가 보완 기술을 이용할 수 있게 해 주므로, 이를 완전히 활용하고 적절하게 이용하려면 몇 가지 전제조건을 만족해야 합니다. 

1. [Cloud Foundry CLI ![외부 링크 아이콘](../icons/launch-glyph.svg "외부 링크 아이콘")](https://github.com/cloudfoundry/cli#getting-started)를 설치하십시오. 

2. [{{site.data.keyword.Bluemix}} CLI ![외부 링크 아이콘](../icons/launch-glyph.svg "외부 링크 아이콘")](http://clis.ng.bluemix.net/ui/home.html)를 설치하십시오. 

3. [{{site.data.keyword.Bluemix_notm}}](https://www.bluemix.net) ID를 확보하십시오. 

4. 선택사항: 로컬에서 애플리케이션을 실행하고 디버그하려는 경우에는 [Docker ![외부 링크 아이콘](../icons/launch-glyph.svg "외부 링크 아이콘")](https://www.docker.com/get-docker) 또한 설치해야 합니다. 이는 비모바일 프로젝트의 경우에만 필수입니다. 


### 설치
{: #installation}

1. 다음 명령을 실행하여 [{{site.data.keyword.dev_cli_short}} ![외부 링크 아이콘](../icons/launch-glyph.svg "외부 링크 아이콘")](/docs/cli/reference/bluemix_cli/index.html#install_plug-in){: new_window}을 설치하십시오. 
 
	```
	bx plugin install dev -r Bluemix
	```
	{: codeblock}

2. 	다음 명령을 실행하여 설치가 완료되었는지 유효성 검증하십시오.   
 
	```
	bx dev
	```
	{: codeblock}
	

### 시작하기 전에
{: #before-install}
	
1. {{site.data.keyword.Bluemix_notm}}에 로그인하십시오. 

	```
	bx login
	```
	{: codeblock}
	
	**참고:** 신임 정보가 거부된 경우에는 연합 ID를 사용하고 있을 수 있습니다. 연합 ID를 사용하여 인증하려면 다음 단계를 따르십시오. 
	
	<!-- 
	POINT TO BLUEMIX CLI LOG IN DOCUMENTATION !!!
	
	This link does not work in production yet --> 
	
	1. [{{site.data.keyword.iamshort}} ![외부 링크 아이콘](../icons/launch-glyph.svg "외부 링크 아이콘")](https://www.bluemix.net/iam/#/apikeys){: new_window}에 로그인하십시오. 
	2. **API 키 작성**을 선택하십시오. 
		* apiKey 이름 및 설명을 입력하십시오. 
	3. apiKey를 다운로드하십시오. 
	4. 파일을 열고 `apiKey` 필드에서 값을 복사하십시오. 
	5. 다음 명령을 사용하여 로그인하십시오. 
	 
		```
		bx login --apikey <value>
		```
		{: codeblock}


## 명령
{: #commands}

다음 명령을 사용하여 프로젝트를 작성하고, 배치하고, 디버그하고, 테스트하십시오. 

### build
{: #build}

`build` 명령을 사용하여 애플리케이션을 빌드할 수 있습니다. 애플리케이션을 빌드하는 데 `build-cmd-run` 구성 요소가 사용됩니다. `test`, `debug` 및 `run` 명령은 정상 조작의 일환으로 이 명령과 동일한 방식의 빌드를 실행하므로 이러한 명령을 실행하기 전에 이 명령을 실행할 필요는 없습니다. 

애플리케이션을 빌드하려면 현재 프로젝트 디렉토리에서 다음 명령을 실행하십시오.   

```
bx dev build
```
{: codeblock}


[build 명령 매개변수](#command-parameters)


### code
{: #code}

`code` 명령은 로컬에서 검토하거나 추가 변경을 수행할 수 있도록 애플리케이션 코드를 배치 후 다운로드할 수 있게 해 줍니다. 

지정된 프로젝트에서 코드를 다운로드하려면 다음 명령을 실행하십시오. 

```
bx dev code <projectName>
```
{: codeblock}


### create
{: #create}

언어, 프로젝트 이름 및 앱 패턴 유형을 포함한 모든 필수 정보에 대한 프롬프트를 표시하며 새 프로젝트를 작성합니다. 프로젝트는 현재 디렉토리에 작성됩니다.  

현재 프로젝트 디렉토리에 새 프로젝트를 작성하고 여기에 서비스를 연관시키려면 다음 명령을 실행하십시오. 

```
bx dev create
```
{: codeblock}


### debug
{: #debug}

`debug` 명령을 통해 애플리케이션을 디버그할 수 있습니다. 먼저 `build-cmd-debug` 구성 요소를 빌드 지시사항으로 사용하여 프로젝트에 대한 빌드가 완료됩니다. 그 후 컨테이너가 시작되고 `container-port-map-debug`에 정의되어 있는 바와 같이 디버그 포트가 노출됩니다. 원하는 디버그 도구를 포트에 연결하면 여느 때와 같이 애플리케이션을 디버그할 수 있습니다. 

**제한사항**: 현재 Swift 프로젝트는 디버그할 수 없습니다. 

애플리케이션을 디버그하려면 현재 프로젝트 디렉토리에서 다음 명령을 실행하십시오. 

```
bx dev debug
```
{: codeblock}	

디버그 세션을 종료하려면 `CTRL-C`를 사용하십시오. 


#### debug 명령 매개변수
{: #debug-parameters}

다음 매개변수는 `debug` 명령 전용이며 애플리케이션 디버깅에 도움을 줍니다. 

##### `container-port-map-debug`
{: #port-map-debug}

* 디버그 포트의 포트 맵핑입니다. 첫 번째 값은 호스트 OS에서 사용할 포트이며 두 번째 값은 컨테이너의 포트입니다(호스트:컨테이너). 
* 사용법: `bx dev debug container-port-map-debug [7777:7777]`
 
##### `build-cmd-debug`
{: #build-cmd-debug}

* DEBUG용 코드를 빌드하는 데 사용됩니다. 
* 사용법: `bx dev debug build-cmd-debug build.command.sh`

##### `debug-cmd`
{: #debug-cmd}

* 도구 컨테이너 내의 코드를 디버그하는 데 사용됩니다. 이는 `build-cmd-debug`가 애플리케이션을 디버그 모드로 시작하는 경우 선택사항입니다. 
* 사용법: `bx dev debug debug-cmd /the/debug/command`

#### 로컬 애플리케이션 디버깅
{: #local-app-dev}

로컬 애플리케이션 디버깅에 대한 자세한 정보는 [로컬 애플리케이션 디버깅](docs/cloudnative/dev_cli_local_debug.html#local-debug)을 참조하십시오. 


### delete
{: #delete}

이 명령은 {{site.data.keyword.Bluemix}} 영역에서 프로젝트를 제거할 수 있게 해 줍니다. 

{{site.data.keyword.Bluemix}}에서 프로젝트를 삭제하려면 다음 명령을 실행하십시오. 

```
bx dev delete <projectName>
```
{: codeblock}
 

**참고**: {{site.data.keyword.Bluemix}} 서비스는 제거되지 **않습니다**. 


### help
{: #help}

기본적으로 조치 또는 인수가 전달되지 않거나 'help' 조치가 제공된 경우 이 명령은 일반 "도움말" 텍스트를 표시합니다. 표시되는 일반 도움말에는 기본 인수와 사용 가능한 조치 목록이 포함됩니다.   

일반 도움말 정보를 표시하려면 다음 명령을 실행하십시오. 

```
bx dev help
```
{: codeblock}


### list
{: #list}

영역의 모든 {{site.data.keyword.Bluemix_notm}} 프로젝트를 나열할 수 있습니다. 

프로젝트를 나열하려면 다음 명령을 실행하십시오. 

```
bx dev list
```
{: codeblock}


<!--
### Editing a project
{: #edit}

You can edit a project, such as changing the name, pattern or starter type, or adding services to your project. Run the following command:

```
bx dev edit
```
{: codeblock}
-->


### run
{: #run}

`run` 명령을 통해 애플리케이션을 실행할 수 있습니다. 먼저 `build-cmd-run` 구성 요소를 빌드 지시사항으로 사용하여 프로젝트에 대한 빌드가 완료됩니다. 그 후 실행 컨테이너가 시작되며 `container-port-map`에 정의되어 있는 바와 같이 포트를 노출합니다. 실행 컨테이너에 이 단계를 완료하는 데 필요한 시작점이 포함되지 않은 경우에는 애플리케이션을 호출하기 위해 `run-cmd`를 사용할 수 있습니다.  

애플리케이션을 시작하려면 현재 프로젝트 디렉토리에서 다음 명령을 실행하십시오. 

```
bx dev run
```
{: codeblock}

세션을 종료하려면 `CTRL-C`를 사용하십시오. 


#### run 매개변수
{: #run-parameters}

다음 매개변수는 `run` 명령 전용이며 실행 컨테이너 내의 애플리케이션을 관리하는 데 도움을 줍니다. 

##### `container-name-run`
{: #container-name-run}
	
* 실행 컨테이너의 컨테이너 이름입니다. 
* 사용법: `bx dev run container-name-run <projectName>`

##### `container-path-run`
{: #container-path-run}

* 실행 시 공유할 컨테이너 내의 위치입니다. 
* 사용법: `bx dev run container-path-run [/path/to/app]`

##### `host-path-run`
{: #host-path-run}

* 실행 시 컨테이너 내에서 공유할 호스트 시스템 내의 위치입니다. 
* 사용법: `bx dev run host-path-run [/path/to/app/bin]`

##### `dockerfile-run`
{: #dockerfile-run}

* 실행 컨테이너에 대한 Docker 파일입니다. 
* 사용법: `bx dev run dockerfile-run [/path/to/Dockerfile.yml]`

##### `image-name-run`
{: #image-name-run}

* dockerfile-run으로부터 작성할 이미지입니다. 
* 사용법: `bx dev run image-name-run [/path/to/image-name]`

##### `run-cmd`
{: #run-cmd}

* 실행 컨테이너 내의 코드를 실행하는 데 사용되는 선택적 매개변수입니다. 이미지가 애플리케이션을 시작하는 경우에는 선택사항입니다. 
* 사용법: `bx dev run run-cmd [/the/run/command]`
	
### status
{: #status}

`container-name-run` 및 `container-name-tools`로 정의된, {{site.data.keyword.dev_cli_short}}에서 사용하는 컨테이너의 상태를 조회할 수 있습니다.  

컨테이너 상태를 확인하려면 현재 프로젝트 디렉토리에서 다음 명령을 실행하십시오. 

```
bx dev status
```
{: codeblock}


[status 명령 매개변수](#command-parameters)


### stop
{: #stop}

`stop` 명령을 통해 컨테이너를 중지할 수 있습니다. `container-name` 매개변수는 중지할 컨테이너를 지정할 수 있게 해 줍니다. 이 매개변수가 지정되지 않은 경우 stop 명령은 `container-name-run`으로 정의된 실행 컨테이너를 중지합니다.  

컨테이너를 중지하려면 현재 프로젝트 디렉토리에서 다음 명령을 실행하십시오. 

```
bx dev stop
```
{: codeblock}


#### 추가 stop 매개변수: 
{: #stop-parameter}

##### `container-name`
{: #container-name}

* 도구 컨테이너의 컨테이너 이름입니다. 
* 사용법: `bx dev stop container-name <demo-tools>` 

### test
{: #test}

`test` 명령을 통해 애플리케이션을 테스트할 수 있습니다. 먼저 `build-cmd-run` 구성 요소를 빌드 지시사항으로 사용하여 프로젝트에 대한 빌드가 완료됩니다. 그 후 애플리케이션에 대해 `test-cmd`를 호출하기 위해 도구 컨테이너가 사용됩니다. 

애플리케이션을 테스트하려면 다음 명령을 실행하십시오.  

```
bx dev test
```
{: codeblock}


[test 명령 매개변수](#command-parameters)


## build, debug, run 및 test의 매개변수
{: #command-parameters}

다음 매개변수는 `build|debug|run|test` 명령과 함께 사용할 수 있으며 명령행을 통해 지정하거나 프로젝트의 `cli-config.yml` 파일을 직접 업데이트하여 지정할 수 있습니다. [`debug`](#debug-parameters) 및 [`run`](#run-parameters) 명령에는 추가 매개변수가 사용 가능하며 이는 해당 절에 기록되어 있습니다. 

**참고**: 명령행에 입력된 명령 매개변수는 `cli-config.yml` 구성보다 우선합니다. 

##### `container-name-tools`  
{: #container-name-tools}

* 도구 컨테이너의 컨테이너 이름입니다. 
* 사용법: `bx dev <build|debug|run|test> container-name-tools [<demo-tools>]`
 
##### `host-path-tools`
{: #host-path-tools}

* build, debug, test에 대해 공유할 호스트 내의 위치입니다. 
* 사용법: `bx dev <build|debug|run|test> host-path-tools [/path/to/build/tools]`

##### `container-path-tools`
{: #container-path-tools}

* build, debug, test에 대해 공유할 컨테이너 내의 위치입니다. 
* 사용법: `bx dev <build|debug|run|test> container-path-tools [/path/for/build]`

##### `container-port-map`
{: #container-port-map}

* 컨테이너의 포트 맵핑입니다. 첫 번째 값은 호스트 OS에서 사용할 포트이며 두 번째 값은 컨테이너의 포트입니다(호스트:컨테이너). 
* 사용법: `bx dev <build|debug|run|test> container-port-map [8090:8090,9090,9090]`

##### `dockerfile-tools`
{: #dockerfile-tools}

* 도구 컨테이너에 대한 Docker 파일입니다. 
* 사용법: `bx dev <build|debug|run|test> dockerfile-tools [path/to/dockerfile]`

##### `image-name-tools`
{: #image-name-tools}

* dockerfile-tools로부터 작성할 이미지입니다. 
* 사용법: `bx dev <build|debug|run|test> image-name-tools [path/to/image-name]`

##### `build-cmd-run`
{: #build-cmd-run}

* DEBUG 외의 모든 용도를 위한 코드를 빌드하는 명령입니다. 
* 사용법: `bx dev <build|debug|run|test> build-cmd-run [some.build.command]`

##### `test-cmd`
{: #test-cmd}

* 도구 컨테이너 내의 코드를 테스트하는 명령입니다. 
* 사용법: `bx dev <build|debug|run|test> test-cmd [/the/test/command]`

