
---

copyright:
  years: 2016, 2017
lastupdated: "2017-03-17"

---
{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}
{:note:.deprecated}

# 패턴 유형
{: #patterns}

클라우드 네이티브 패턴은 애플리케이션의 일관성 있고, 확장 가능하며 신뢰할 수 있는 토폴로지를 확보하는 데 도움을 주는 검증된 디자인입니다. 프로젝트를 작성할 때는 선택할 수 있는 다양한 패턴 유형이 제공됩니다. 사용자는 프로젝트에 포함시킬 패턴 유형 및 기능을 선택하기만 하면 됩니다. 프로젝트 환경 설정을 정의하고 나면 편집하거나, 실행 또는 디버그하거나, 로컬 또는 {{site.data.keyword.Bluemix}}에 배치할 수 있는 스타터 프로젝트가 생성됩니다. 

## 웹 앱
{: #web}

웹 프로젝트는 HTML, JavaScript 및 스타일시트와 같은 웹 컨텐츠를 웹 서버에 제공하는 기능을 추가합니다. 

다음 웹 스타터가 사용 가능합니다. 

* 기본 웹: 정적 `index.html` 파일, 기본 스타일시트(비어 있음) 및 JavaScript 파일을 제공합니다. 
* Webpack: ES6(ECMAScript 6) 소스 파일이 `src/client`에 있으며 이러한 파일을 브라우저에서 사용할 수 있도록 축소하고 변환하기 위해 WebPack을 사용하여 컴파일하는 프로젝트를 작성합니다. 
* Webpack + React: 사용자 인터페이스 빌드에 사용되는 리치 프레임워크입니다. 소스 파일은 `src/client/app`에 있으며 WebPack을 사용해 컴파일되어 공용 디렉토리에서 제공됩니다. 


## 모바일 앱
{: #mobile}

모바일 앱 패턴은 {{site.data.keyword.mobilepushshort}}, {{site.data.keyword.mobileanalytics_short}}, {{site.data.keyword.appid_short}} 등과 같은 백엔드 서비스와 직접 연결하는 모바일 앱을 빌드하는 데 도움을 줍니다. 프로젝트는 sdkGen(BFF 등) 및 마이크로서비스를 통해 추가될 수도 있습니다. 

{{site.data.keyword.watson}} Conversation, {{site.data.keyword.visualrecognitionshort}}, {{site.data.keyword.openwhisk_short}} 등과 같은 스타터 목록에서 선택할 수 있습니다. 

Swift, Android 또는 Cordova를 사용하여 모바일 앱을 생성할 수 있습니다. 


## BFF(Backend for Frontend)
{: #bff}

BFF(Backend for Frontend) 패턴은 실제로 사용자 상호작용 요구사항과 일치하는 양식으로 비즈니스 데이터 및 서비스를 노출하는 데 집중할 수 있도록 도움을 줍니다. 클라우드 솔루션에 대한 사용자의 경험을 최적화하려면, 모바일 애플리케이션에 대한 색다른 사용자 경험과 웹 애플리케이션에 대한 더 풍부하고 자세한 경험이 필요할 수 있습니다. [{{site.data.keyword.conversationfull}} ![외부 링크 아이콘](../icons/launch-glyph.svg "외부 링크 아이콘")](https://www.ibm.com/watson/developercloud/conversation.html) 서비스와 같은 음성 제어 디바이스를 사용하면 사용자와의 상호작용이 음성으로 제어될 수 있습니다. 이 디지털 채널은 음성 집중 기반 상호작용을 관리하기 위해 매우 다양한 BFF가 필요할 것입니다. 

{{site.data.keyword.Bluemix_notm}}를 사용하면, 여러 언어를 사용하는 프로그래밍 접근 방식을 통해 BFF를 빌드하여 BFF를 정의할 수 있습니다. IBM에서는 Node.js, Swift 또는 Java를 사용하고, 이를 Cloud Foundry, 컨테이너 서비스 또는 서버리스(serverless)로 클라우드 네이티브 패턴에서 실행하는 것을 권장합니다. 

BFF는 데이터 지속성, 캐싱을 위한 서비스와의 통합 및 {{site.data.keyword.ibmwatson}}, {{site.data.keyword.iot_short_notm}}, {{site.data.keyword.weather_short}}와 같은 높은 가치를 제공하는 서비스 및 {{site.data.keyword.sparks}}와 같은 데이터 분석과의 통합을 관리합니다. 

BFF는 가장 일반적으로 REST 패턴을 사용하여 API를 노출하게 되지만, {{site.data.keyword.messagehub}}를 사용하여 메시징 아키텍처에서 작동하도록 BFF를 디자인할 수 있습니다. 

BFF 기본 스타터는 Node.js 또는 Swift를 사용하여 사용 가능합니다. 


## 마이크로서비스
{: #microservice}

마이크로서비스 프로젝트는 기본 상태 엔드포인트인 REST API를 포함한 백엔드 마이크로서비스를 빌드하기 위한 기초를 제공합니다. 생성되는 프로젝트는 마이크로서비스 자체 및 연결된 클라우드 서비스에서 필요로 하는 모든 종속 항목을 포함합니다. 

마이크로서비스 기본 스타터는 Java를 사용하여 이용 가능합니다. 

<!--
## Other
{: #other}

The Other pattern represents a project that consists of only the language-specific server-side web framework. It has all the other file assets to work with the project, such as needed libraries and config files.

Content to be provided by Karl Bishop.
-->


## 언어
{: #languages notoc}

지원되는 언어는 다음과 같습니다. 

   * [Java ![외부 링크 아이콘](../icons/launch-glyph.svg "외부 링크 아이콘")](../runtimes/liberty/getting-started.html){: new_window}
   * [Node.js ![외부 링크 아이콘](../icons/launch-glyph.svg "외부 링크 아이콘")](../runtimes/nodejs/getting-started.html){: new_window}
   * [Swift ![외부 링크 아이콘](../icons/launch-glyph.svg "외부 링크 아이콘")](../runtimes/swift/getting-started.html){: new_window}


### Java
{: #java notoc}

Java에는 엔터프라이즈급 애플리케이션을 빌드할 수 있는 검증된 기능이 있습니다. 그러나 Java 8의 새 기능을 통해, Java는 Liberty 등의 경량 런타임이나 Spring Boot와 같은 프레임워크와 함께 마이크로서비스를 빌드하는 경우에도 사용하기 적절한 언어가 되었습니다. 


### Node.js
{: #node notoc}

Node.js는 이벤트 중심의 비차단 I/O 모델을 사용하는 JavaScript 런타임으로, 경량이고 효율적이며 웹 애플리케이션, BFF 패턴 및 마이크로서비스의 처리량 및 확장성 측면에서 탁월합니다. Node.js의 패키지 에코시스템인 npm은 많은 오픈 소스 모듈에 대한 액세스를 제공함으로써 애플리케이션 개발 속도를 높일 수 있는 다양한 기능을 제공합니다. 


### Swift
{: #swift notoc}

Swift는 2014년에 Apple에서 만든 최신 프로그래밍 언어로, Objective C 사용을 대체하기 위해 디자인되었으며 2015년 12월 오픈 소스로 전환되었습니다. 현재는 x86, ARM 또는 Z 아키텍처를 사용하는 Linux 및 macOS 운영 체제의 iOS, macOS, 웹 서비스 및 시스템 소프트웨어를 빌드하는 데 사용됩니다. 이 언어는 스크립팅 언어처럼 작성되지만 낮은 오버헤드로 C와 유사한 고성능을 달성할 수 있도록 컴파일되어 클라우드 런타임에 적합합니다. 이 언어는 Java에서 볼 수 있는 강력하고 정적인 유형의 시스템을 사용하는 동시에 JavaScript에서 볼 수 있는 기능 스타일 및 비동기 루틴을 사용합니다. 이 언어는 성능이 뛰어나며, 소스는 LLVM 컴파일러 도구 체인을 사용하여 네이티브 코드로 컴파일되고 C로 작성된 외부 시스템 라이브러리를 쉽게 이용할 수 있습니다. 
