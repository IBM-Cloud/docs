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

# 컴퓨팅
{: #compute}

모바일 및 웹에 대한 클라우드 네이티브 디지털 채널 애플리케이션을 빌드하는 경우, 디지털 채널 전용이거나 웹 및 모바일 클라이언트 앱 둘 다에 동일한 데이터 및 로직 통합 지원을 제공하는 BFF(Backend for Frontend)를 보유하는 것이 좋습니다. 이 아키텍처에 대한 자세한 정보는 [Microservices for web and mobile ![외부 링크 아이콘](../icons/launch-glyph.svg)](https://www.ibm.com/devops/method/content/architecture/omnichannelArchitecture)을 참조하십시오. 

다음 다이어그램은 BFF 아키텍처의 개요를 표시합니다. 

![BFF 아키텍처](images/bff-arch.png)

그림 1: BFF 아키텍처

BFF의 개념은 마이크로서비스 또는 고가치 {{site.data.keyword.Bluemix}} 클라우드 서비스에서 공통 비즈니스 로직 및 통합 로직을 추출하는 것입니다. 

이 아키텍처를 사용하여 모바일 또는 웹 애플리케이션에 업데이트를 배치 및 릴리스하고 DevOps 서비스가 포함된 지속적 딜리버리 파이프라인을 사용하여 BFF의 새 버전을 배치할 수 있습니다. 

iOS에 대해 하나의 BFF가 있고 Android용으로 별도의 BFF가 있는 경우 이 앱에 대한 기능을 제공하는 엔지니어링 팀은 중앙 API 릴리스 스케줄에 의해 기능을 릴리스하도록 제한되지 않습니다. 이는 마이크로서비스 및 디지털 채널 아키텍처의 공통 목표입니다. 다른 팀의 릴리스 스케줄과 관계없이 팀에서 기능을 원하는 만큼 자유롭게 릴리스할 수 있습니다. 

<!--
## Backend for Frontends (BFF)
{: #bff}

Backend for Frontend patterns, commonly known as BFFs, really help you to focus on exposing business data and services in a form that matches the user interaction requirements. To optimize a user journey to your cloud solution, it may require a different user journey for the mobile application and a richer, more detailed journey for the Web application. With the introduction of voice-controlled devices like the [{{site.data.keyword.conversationfull}} ![External link icon](../icons/launch-glyph.svg "External link icon")](https://www.ibm.com/watson/developercloud/conversation.html) service, the interaction with a user could be controlled by voice. This digital channel will require a very different BFF for managing these voice intent-based interactions.

With {{site.data.keyword.Bluemix_notm}}, you can build a BFF by using polyglot programming approach to define the BFF. IBM recommends using Node, Swift, or Java and running them in a cloud native pattern with either Cloud Foundry, Container services, or serverless.

The BFF will manage the integration with services for data persistence, caching, and integration with high-value services like {{site.data.keyword.ibmwatson}}, {{site.data.keyword.iot_short_notm}}, {{site.data.keyword.weather_short}}, and data analytics like {{site.data.keyword.sparks}}.

The BFF will expose an API most commonly using a REST pattern, but you can design your BFF to work from a messaging architecture using {{site.data.keyword.messagehub}}.
-->


## 모바일 클라이언트를 BFF(Backend for Frontend)와 통합
{: #integration}

모바일 클라이언트와 BFF를 쉽게 통합할 수 있도록 {{site.data.keyword.Bluemix_notm}}는 Swift 및 Java 언어로 각각 iOS 및 Android용 모바일 클라이언트 SDK를 생성하도록 지원합니다. 이 기능을 사용하려면 Open API 스펙(Swagger) 문서를 사용하여 BFF 통합을 노출시켜야 합니다. 이 문서는 JSON 또는 YAML 양식일 수 있습니다. 

클라이언트 SDK 생성기는 Open API 정의 파일을 사용하여 네이티브 모바일 애플리케이션에서 이용하기 쉬운 클라이언트에 최적화된 개발자 SDK를 정의합니다. 이를 통해 BFF를 모바일 애플리케이션에 빠르게 통합할 수 있습니다. 


## API 정의
{: #definition}

BFF는 라이브 서버 엔드포인트에서 실행 중인 Open API 스펙을 준수하는 API 정의 파일을 노출시켜야 합니다. 이 엔드포인트를 검색하는 데 {{site.data.keyword.Bluemix_notm}} 개발자 경험 및 {{site.data.keyword.Bluemix_notm}} SDK CLI(Command Line Interface)를 사용하려면, 환경 변수를 `OPENAPI_SPEC`이라는 Cloud Foundry 애플리케이션에 추가해야 합니다. 이 환경 변수는 상대 경로를 사용하여 스펙을 참조해야 합니다. 

{{site.data.keyword.Bluemix_notm}}에서 `OPENAPI_SPEC` 환경 변수를 추가하려면 다음 단계를 따르십시오. 

1. [{{site.data.keyword.Bluemix_notm}} ![외부 링크 아이콘](../icons/launch-glyph.svg)](http://bluemix.net)에 로그인하십시오. 
2. Cloud Foundry 앱을 선택하십시오. 
3. **런타임**을 선택하십시오. 
4. **환경 변수**를 선택하십시오. 
5. **사용자 정의** 섹션에서 **추가**를 클릭하십시오. 
6. **NAME**에 대해 `OPENAPI_SPEC` 및 Open API 정의 파일에 대한 상대 URL 경로를 지정하십시오. 
7. **저장**을 클릭하십시오. 

<!--
To add the `OPENAPI_SPEC` environment variable locally and push your changes to {{site.data.keyword.Bluemix_notm}} with the [Cloud Foundry CLI ![External link icon](../icons/launch-glyph.svg)](https://github.com/cloudfoundry/cli#getting-started), follow these steps:

1. Open Terminal and navigate to your project directory.
2. Add the following code to the `manifest.yml` file.

   ```
   env:
       "OPENAPI_SPEC": "<relative URL path to your Open API definition file>"
   ```
   {: codeblock}
3. Save your changes to the `manifest.yml` file.
4. Run `cf push` to deploy the changes to {{site.data.keyword.Bluemix_notm}}.
-->

예를 들어, 

```
OPENAPI_SPEC='/explorer/swagger.json'
```
{: codeblock}

{{site.data.keyword.apiconnect_long}} 및 Loopback 애플리케이션은 특히 이 접근 방식을 사용할 때 잘 작동합니다. Loopback 및 {{site.data.keyword.apiconnect_short}}를 사용하여 지속적 모델을 정의하고 Open API 정의 파일을 사용하는 CRUD(작성, 읽기, 업데이트 및 삭제) 오퍼레이션을 노출시킬 수 있습니다. 

또한 비즈니스 로직 오퍼레이션도 정의할 수 있습니다. 


### Open API 스펙의 지원되는 요소
{: #supported-elements notoc}

Open API 스펙에서 완전히 지원되지 않는 유일한 부분은 파일 구조입니다. 스펙을 통해 정의의 부분이 서로 다른 파일로 분할되고 json `$ref` 필드를 사용하여 참조될 수 있습니다. 전체 정의는 한 파일 내에 포함되어야 합니다. 


## Bluegen을 사용하는 예제 BFF(Backen for Frontend)
{: #bff-bluegen}

{{site.data.keyword.Bluemix_notm}}는 {{site.data.keyword.apiconnect_short}} 및 Strongloop를 사용하여 참조 BFF를 작성했습니다. 이는 {{site.data.keyword.objectstorageshort}}의 이미지를 참조하도록 제품 모델을 {{site.data.keyword.cloudant}} 및 이미지 API에 맵핑합니다. 

이 BFF 패턴을 사용하여 완전히 작동하는 BFF를 {{site.data.keyword.Bluemix_notm}}에 신속하게 프로비저닝하기 시작할 수 있으며, 이를 통해 BFF를 모바일 프로젝트에 통합하고 iOS 및 Android용 네이티브 SDK를 각각 Swift 및 Java로 생성하는 것이 얼마나 쉬운지 이해할 수 있습니다. 

프로젝트 작성 및 설치에 대해서는 [README ![외부 링크 아이콘](../icons/launch-glyph.svg "외부 링크 아이콘")](https://github.com/ibm-bluemix-mobile-services/backend-for-frontend-node) 지시사항을 따르십시오. 


## 개발자 경험 프로젝트에서 BFF(Backend for Frontend) 사용
{: #bff-devex}

{{site.data.keyword.Bluemix_notm}} 모바일 개발자 경험은 연관된 클라우드 서비스가 많은 모바일 프로젝트의 정의를 간소화하도록 디자인되었습니다. [{{site.data.keyword.mobilepushshort}} ![외부 링크 아이콘](../icons/launch-glyph.svg)](/docs/services/mobilepush/index.html), [분석 ![외부 링크 아이콘](../icons/launch-glyph.svg)](/docs/services/mobileanalytics/index.html) 및 데이터 또는 스토리지 서비스를 쉽게 추가할 수 있습니다. 

{{site.data.keyword.Bluemix_notm}} {{site.data.keyword.dev_console}}은 **컴퓨팅** 페이지에서 모바일 프로젝트에 BFF를 통합하는 기능을 도입했습니다. 기존의 컴퓨팅 서비스 인스턴스를 모바일 프로젝트에 추가할 수 있습니다. 추가되고 나면 언어 선택사항에 대한 네이티브 SDK를 생성하거나 전체 프로젝트를 생성할 수 있으며 **코드** 페이지에서 프로젝트의 소스 패키지에 SDK가 통합됩니다. 이미 올바르게 정의된 BFF와 통합하는 경우에 특히 유용합니다. 

프로젝트를 다운로드한 후 Xcode 또는 Android Studio에서 프로젝트를 열 수 있으며 클라이언트 SDK를 사용하여 프로젝트를 컴파일할 수 있습니다. 


## CLI 사용
{: #cli}

BFF를 개발함에 따라 API 스펙도 변경될 수 있습니다. 이러한 변경사항을 지원하기 위해 다음 두 가지 옵션이 있습니다. 

* 전체 프로젝트를 새로운 GitHub 분기에 재생성하고 변경사항을 개발 분기로 병합합니다. 
* 명령행(CLI) 도구를 사용하여 SDK를 직접 재생성하고 모바일 프로젝트의 SDK 부분만 업데이트합니다. 

CLI를 사용하려면, CLI를 [설치](sdk_cli.html#installation)해야 합니다. 

수행할 수 있는 조치를 나열하려면 다음 명령을 사용하십시오. 

```
bluemix sdk
```
{: codeblock}

현재 {{site.data.keyword.Bluemix_notm}} 영역에서 실행 중인 Cloud Foundry 인스턴스를 나열하려면 다음 명령을 사용하십시오. 

```
bluemix sdk list
```
{: codeblock}

각 앱이 나열되고 `OPENAPI_SPEC` 환경 변수가 설정되어 있는 경우 API의 유효성이 검증됩니다. `VALID` 열에 초록색 확인 표시 또는 빨간색 `X`가 표시됩니다. 애플리케이션의 `VALID` 열에 있는 확인 표시는 올바른 Open API 정의가 있음을 의미합니다. 애플리케이션의 `VALID` 열에 있는 `X`는 다음 두 가지를 의미합니다. 

* `OPENAPI_SPEC` 환경 변수가 애플리케이션에 대해 정의되어 있지 않음 또는
* API 정의가 Open API 스펙에 대해 올바르지 않음

API에 대한 완전한 URL을 보려면 다음 명령을 사용하십시오. API 스펙에 대한 완전한 라우트 및 URI가 나열됩니다. 브라우저에서 원시 스펙을 보고, CLI에서 직접 이용하거나 BFF `OPENAPI_SPEC` 환경 변수가 올바르게 설정되어 있는지 확인할 수 있습니다. 

```
bluemix sdk list --url
```
{: codeblock}

SDK를 생성하는 데 사용될 수 있는지 판별하기 위해 `<AppName>`의 Open API 정의 파일의 유효성을 검증하려면 다음 명령을 사용하십시오. 명령은 현재 영역에서 `<AppName>`을 찾고 유효성 검증에 대한 스펙을 찾는 데 `OPENAPI_SPEC` 환경 변수의 상대 경로를 사용합니다. 

```
bluemix sdk validate <AppName>
```
{: codeblock}

선택한 네이티브 `<Platform>`에 대한 SDK를 생성하고 압축 파일을 현재 작업 디렉토리에 배치하려면 다음 명령을 사용하십시오. 

```
bluemix sdk generate <AppName> <SDKName> --<Platform>
```
{: codeblock}

`--unzip` 옵션을 사용하면 자동으로 SDK가 현재 작업 디렉토리에 추출됩니다. 또는 `--output` 옵션을 사용하여 SDK를 추출할 위치를 선택적으로 지정할 수 있습니다. GitHub를 사용하여 소스 코드를 관리하고 특히 SDK 업데이트를 위한 새로운 분기를 작성할 수 있습니다. 이 접근 방식을 사용하면 변경사항을 쉽게 확인하고 업데이트된 SDK를 개발 분기에 병합할 수 있습니다. 


## SDK 생성 모델 및 API 관련 작업
{: #models-apis}

이제 생성된 SDK를 사용하여 BFF가 모바일 앱에 통합되었으므로 이와 관련된 작업을 시작할 수 있습니다. 

SDK는 `docs` 디렉토리 및 `source` 디렉토리에서 완전히 생성된 문서를 제공됩니다. 문서의 웹 보기를 위해 `README.html` 파일을 열거나 문서의 Markdown 보기를 위해 `README.md` 파일을 열 수 있습니다. Markdown 문서는 SDK를 Cocoapods 또는 Maven Central에 공개하는 경우 유용합니다. 

문서 내에서 생성된 API의 목록을 확인할 수 있습니다. API를 클릭하여 모바일 앱에 직접 붙여넣을 수 있는 코드 스니펫을 볼 수 있습니다. 
