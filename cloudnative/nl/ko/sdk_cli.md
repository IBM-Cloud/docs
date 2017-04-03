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

# SDK Generator 플러그인
{: #sdk-cli}

{{site.data.keyword.IBM}} SDK Generator 플러그인은 [{{site.data.keyword.Bluemix_notm}} CLI ![외부 링크 아이콘](../icons/launch-glyph.svg "외부 링크 아이콘")](/docs/cli/reference/bluemix_cli/index.html)에서 설치할 수 있습니다. 

{{site.data.keyword.Bluemix_notm}}의 개발자는 이 플러그인을 사용하여 [Open API 스펙 ![외부 링크 아이콘](../icons/launch-glyph.svg "외부 링크 아이콘")](https://www.openapis.org/)을 준수하는 REST API 정의에서 SDK를 생성할 수 있습니다. REST API 정의에 대한 변경사항을 작성하는 경우, 전체 프로젝트를 재생성하는 대신 이 플러그인을 사용하여 SDK만 재생성할 수 있습니다. 

또한 지정된 영역의 Cloud Foundry 앱에 SDK 생성에 유효한 REST API 정의가 있는지도 확인할 수 있습니다. 마지막으로, {{site.data.keyword.IBM_notm}} SDK Generator 플러그인으로 REST API 정의의 유효성을 검증하여 해당 REST API가 SDK 생성기의 요구사항에 부합하는지 확인할 수 있습니다. 

이 {{site.data.keyword.IBM_notm}} SDK Generator 플러그인을 사용할 경우, 생성된 SDK를 통해 백엔드 서비스를 앱으로 쉽게 통합할 수 있습니다. REST API에 대한 변경사항이 발생하면 SDK를 재생성하고 이를 이전 SDK와 대체하여 원할하게 SDK를 업그레이드할 수 있습니다. 또한 CLI를 DevOps 파이프라인에 통합할 수 있으며 앱이 빌드될 때마다 SDK가 항상 API 스펙과 일치하도록 할 수 있습니다. 

REST API 정의는 유효해야 하며 라이브 서버 엔드포인트에서 호스팅되거나 사용자 시스템의 로컬 파일이어야 합니다. REST API 정의가 호스팅되는 경우 상대 URL은 `OPENAPI_SPEC` 환경 변수에 정의되어야 합니다. 


## 요구사항
{: #prereqs}

다음 요구사항을 충족하는지 확인하십시오. 

* [{{site.data.keyword.Bluemix_notm}} ![외부 링크 아이콘](../icons/launch-glyph.svg "외부 링크 아이콘")](http://bluemix.net) 계정 소유
* [Open API ![외부 링크 아이콘](../icons/launch-glyph.svg "외부 링크 아이콘")](https://www.openapis.org/) 스펙을 준수하는 유효한 API 정의


## 설치
{: #installation}

1. [{{site.data.keyword.Bluemix}} CLI ![외부 링크 아이콘](../icons/launch-glyph.svg "외부 링크 아이콘")](http://clis.ng.bluemix.net/ui/home.html)를 설치하십시오. 

2. [플러그인 ![외부 링크 아이콘](../icons/launch-glyph.svg "외부 링크 아이콘")](/docs/cli/reference/bluemix_cli/index.html#install_plug-in)을 설치하십시오. 

	```
	bx plugin install sdk-gen -r Bluemix
	```
	{: codeblock}


## 명령
{: #commands}

다음 명령을 사용하여 SDK를 생성하거나 Open API 정의 파일의 유효성을 검증하거나 Cloud Foundry 앱을 나열하십시오. 


### SDK 생성
{: #gen}

`bluemix sdk generate [arguments...][command options]`를 사용하십시오. 


#### 인수
{: #gen-args}

* `APP_NAME` - 현재 영역에 있는 Cloud Foundry 앱의 이름
* `OPENAPI_DOC_LOCATION` - 원시 REST API 정의 JSON 또는 Yaml에 대한 URL 또는 상대 파일 경로
* `GENERATED_SDK_NAME`(선택사항) - 생성된 SDK의 이름


#### 옵션
{: #gen-options}

* `PLATFORM`(필수)
   * `--android` - Android SDK 생성
   * `--ios` - iOS Swift SDK 생성
   * `--swift` - Swift 서버 SDK 생성
* `--output "YOUR_RELATIVE_PATH"`(선택사항) - 생성된 SDK를 `YOUR_RELATIVE_PATH`에서 지정한 디렉토리에 배치(기존의 SDK가 있는 경우 겹쳐씀)
* `--unzip`(선택사항) - 생성된 SDK 추출(기존의 SDK 아티팩트가 있는 경우 겹쳐씀)


#### 사용법
{: #gen-usage}

{{site.data.keyword.Bluemix_notm}}에서 실행 중인 Cloud Foundry에서 SDK를 생성하기 위해 CLI에 대한 매개변수로 앱의 이름을 사용할 수 있습니다. 다음 명령은 앱의 이름을 `SDK_Name`으로 사용합니다. 

```
bluemix sdk generate [APP_NAME] [PLATFORM]
```
{: codeblock}

로컬 JSON 또는 Yaml 파일이나 Open API 정의 파일에 대한 URL에서 SDK를 생성하려면 다음 명령을 사용하십시오. 

```
bluemix sdk generate [OPENAPI_DOC_LOCATION] [SDK_Name] [Platform]
```
{: codeblock}


### Open API 정의 유효성 검증
{: #validating}

`bluemix sdk validate [argument]`를 사용하십시오. 


#### 인수
{: #val-args}

* `APP_NAME` - 현재 영역에 있는 Cloud Foundry 앱의 이름
* `OPENAPI_DOC_LOCATION` - 원시 REST API 정의 JSON 또는 Yaml에 대한 URL 또는 상대 파일 경로


#### 사용법
{: #val-usage}

{{site.data.keyword.Bluemix_notm}}에서 실행 중인 Cloud Foundry 앱의 API 스펙의 유효성을 검증하기 위해 CLI에 대한 매개변수로 앱의 이름을 사용할 수 있습니다. 

```
bluemix sdk validate [APP_NAME]
```
{: codeblock}

로컬 JSON 또는 Yaml 파일이나 API 스펙 문서에 대한 URL의 SDK 유효성을 검증하려면 다음 명령을 사용하십시오. 

```
bluemix sdk validate [OPENAPI_DOC_LOCATION]
```
{: codeblock}



### 앱 나열(Cloud Foundry)
{: #list-apps}

`bluemix sdk list [argument][option]`를 사용하여 앱을 나열하고 API 스펙의 유효성을 검증하십시오. `OPENAPI_SPEC` 환경 변수가 스펙을 호스팅하는 상대 URL로 설정되어 있어야 합니다. 


#### 인수
{: #list-args}

* `SPACE_NAME`(선택사항) - 앱을 검색하려는 현재 조직 내에 있는 Cloud Foundry 영역의 이름. 제공되지 않는 경우 현재 영역이 검색됩니다. 


#### 옵션
{: #list-options}

* `--url`(선택사항) - 목록에서 각 앱의 Open API 정의에 대한 완전한 URL을 표시


#### 사용법
{: #list-usage}

현재 영역에 있는 앱을 나열하려면 다음 명령을 사용하십시오. 

```
bluemix sdk list
```
{: codeblock}

현재 영역에 있는 앱을 나열하고 API 스펙 URL을 표시하려면 다음 명령을 사용하십시오. 

```
bluemix sdk list --url
```
{: codeblock}

특정 영역에 있는 앱을 나열하려면 다음 명령을 사용하십시오. 

```
bluemix sdk list [SPACE_NAME]
```
{: codeblock}

특정 영역에 있는 앱을 나열하고 API 스펙 URL을 표시하려면 다음 명령을 사용하십시오. 

```
bluemix sdk list [SPACE_NAME] --url
```
{: codeblock}
