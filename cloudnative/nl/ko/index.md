---

copyright:
  years: 2016, 2017
lastupdated: "2016-04-10"

---
{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}
{:note:.deprecated}

# 클라우드 네이티브 프로젝트 빌드
{: #web-mobile}

{{site.data.keyword.Bluemix}} {{site.data.keyword.dev_console}} [프로젝트](projects.html) 개념을 통해 클라우드 네이티브 앱을 관리할 수 있습니다. [{{site.data.keyword.dev_console}}](devex.html) 또는 {{site.data.keyword.IBM_notm}} {{site.data.keyword.Bluemix_notm}} CLI의 [{{site.data.keyword.dev_cli_notm}}](dev_cli.html)을 사용하여 프로젝트를 작성할 수 있습니다. {{site.data.keyword.Bluemix_notm}} {{site.data.keyword.dev_console}}은 클라우드 네이티브 애플리케이션 개발자가 필요로 하는 대부분의 일반적 서비스 기능을 개발자에게 최적화된 하나의 연결된 경험으로 제공합니다. 

{{site.data.keyword.Bluemix_notm}} {{site.data.keyword.dev_console}}은 클라우드 네이티브 애플리케이션 개발자가 다양한 [패턴 유형](patterns.html) 및 [스타터](starters.html)로부터 프로젝트를 작성하고, 주요 {{site.data.keyword.Bluemix_notm}} 최적화 서비스를 작성하여 프로젝트에 연결하고, SDK를 사용하여 작동하는 코드를 빠르게 다운로드할 수 있게 해 줍니다. SDK는 이를 신속히 실행할 수 있게 해 주는 기능 신임 정보 및 종속 항목과 완전히 통합되어 있습니다. 애플리케이션이 실행 중이며 기능을 구성한 경우에는 프로젝트로 돌아가 애플리케이션 사용자와의 상호관계를 모니터하고 관리할 수 있습니다. {{site.data.keyword.dev_console}}을 통해 서비스를 구성하고 관리할 수도 있습니다. 

<!--
While the {{site.data.keyword.Bluemix_notm}} {{site.data.keyword.dev_console}} provides an integrated development experience, some developers might still want to have finer-grained control and wire services together manually. If this is your preferred approach, you might want to consider using the [{{site.data.keyword.mobilefirstbp}} Starter boilerplate](try_mobile.html).
-->

<!--With {{site.data.keyword.Bluemix}} Mobile services, you can incorporate pre-built, managed, and scalable cloud services into your mobile applications. You can focus on building your mobile apps, instead of the complexities of managing the back-end infrastructure.

The Mobile dashboard provides an integrated experience on {{site.data.keyword.Bluemix_notm}} where you can create mobile projects easily from within the dashboard.
-->


## 프로젝트
{: #projects}

{{site.data.keyword.Bluemix}} {{site.data.keyword.dev_console}}은 앱 사용자 인터페이스, 데이터 및 서비스를 하나의 완전한 *프로젝트*로 결합합니다. 프로젝트를 작성하여 앱의 모든 필수 파트와 추가된 기능을 {{site.data.keyword.Bluemix_notm}} 서버에서 유지보수합니다. 사용자는 앱 코드를 다운로드할 수 있으며 서비스가 프로젝트 내에 구성된 경우에는 필수 신임 정보 및 초기자(initializer)도 다운로드할 수 있습니다. **프로젝트**를 선택하여 모든 프로젝트를 볼 수 있습니다.   

**프로젝트** 페이지에서 프로젝트를 선택하여 하나의 프로젝트에 대한 추가 정보를 볼 수 있습니다. 이를 수행하면 **프로젝트 개요** 페이지가 표시되며, 이 페이지는 해당 프로젝트용으로 구성되고 사용 가능한 서비스를 포함합니다. 서비스는 기능을 추가하여 앱을 확장하는 별도의 기능입니다. 서비스는 개별적으로 추가되므로 푸시 서비스, 인증, 데이터 및 스토리지 또는 기타 서비스 등 필요한 서비스를 추가할 수 있습니다. **프로젝트 개요** 페이지에서 프로젝트에 서비스를 추가하고 지시사항에 따라 이를 구성하면 해당 서비스가 자동으로 앱과 연관됩니다. 프로젝트 개요 페이지에 대한 자세한 정보는 [프로젝트 개요 페이지](project_overview_page.html)를 참조하십시오. 

프로젝트를 작성하려면 [패턴](patterns.html) 및 [스타터](starters.html)를 선택해야 합니다. 


### 프로젝트 개요 페이지
{: #project_overview}

**프로젝트** 페이지에서 프로젝트를 선택하여 하나의 {{site.data.keyword.Bluemix}} {{site.data.keyword.dev_console}} 프로젝트를 보고 이에 대한 작업을 수행할 수 있으며, 이렇게 선택하면 프로젝트 개요 페이지가 열립니다.
{: shortdesc}

**프로젝트 개요** 페이지는 선택한 프로젝트에 대해 구성되거나 구성하는 데 사용 가능한 각 기능에 대해 하나의 타일을 표시합니다. 타일은 기능의 유형과 3개의 수직 정렬된 점이 있는 *조치* 단추를 표시합니다. 사용 가능하거나 구성된 서비스의 예에는 {{site.data.keyword.mobilepushshort}}, 분석 또는 데이터 및 스토리지가 포함됩니다. 호환 가능한 기능은 프로젝트 유형 및 해당 지역에서 사용 가능한 기능에 따라 달라지므로, 모든 기능을 모든 프로젝트와 연관시킬 수는 없습니다.  

기능 유형이 아직 프로젝트와 연관되지 않은 경우에는 **작성** 단추가 타일에 표시됩니다. 이 조치 단추 옵션은 기능이 아직 연관되지 않은 경우 서비스의 인스턴스를 작성하거나 기존 서비스 인스턴스를 추가하는 용도로 사용됩니다. **기존 추가**를 선택하면 사용자의 영역에 있는 해당 유형의 서비스 인스턴스 목록이 제공됩니다. 

기능이 이 프로젝트와 이미 연관된 경우에는 기능 유형 뒤에, 연관된 서비스 인스턴스의 이름이 타일에 표시됩니다. 이를 통해 {{site.data.keyword.dev_console}}에서 이 프로젝트와 관련된 서비스 인스턴스를 쉽게 찾을 수 있습니다. 기능이 이미 프로젝트와 연관된 경우, 조치 단추에서 사용 가능한 조치는 **보기** 및 **제거**입니다. 서비스 인스턴스를 제거하면 이 프로젝트에 대한 연관만 제거되며 {{site.data.keyword.dev_console}}에서 서비스 인스턴스가 삭제되지는 않습니다. 서비스 인스턴스를 삭제하려면, 서비스 인스턴스를 보고 삭제할 수 있도록 **웹 및 모바일 > 서비스** 페이지를 클릭하십시오. 

**코드** 타일에서 **코드 가져오기**를 선택하여 프로젝트의 코드를 다운로드하십시오. 코드 다운로드에 대한 자세한 정보는 [코드 가져오기](get_code.html)를 참조하십시오. 


### 새 스타터를 사용하도록 프로젝트 업데이트
{: #update-starter}

1. **프로젝트** 또는 **프로젝트 개요** 페이지에서 **오버플로우 메뉴** 아이콘을 클릭하고 **스타터 업데이트**를 선택하십시오. 

2. 새 스타터를 선택하고 **업데이트**를 클릭하십시오. 

3. **프로젝트 개요** 페이지에서 **코드 가져오기**를 클릭하여 언어를 선택하십시오. 

   또는 **코드** 페이지를 클릭할 수 있습니다.


### 새 언어를 생성하도록 프로젝트 업데이트
{: #update-language}

1. **프로젝트** 또는 **프로젝트 개요** 페이지에서 **오버플로우 메뉴** 아이콘을 클릭하고 **스타터 업데이트**를 선택하십시오. 

2. 새 언어를 선택하고 **업데이트**를 클릭하십시오. 

3. **프로젝트 개요** 페이지에서 **코드 가져오기**를 클릭하여 언어를 선택하십시오. 


## 패턴 유형
{: #patterns}

클라우드 네이티브 패턴은 애플리케이션의 일관성 있고, 확장 가능하며 신뢰할 수 있는 토폴로지를 확보하는 데 도움을 주는 검증된 디자인입니다. 프로젝트를 작성할 때는 선택할 수 있는 다양한 패턴 유형이 제공됩니다. 사용자는 프로젝트에 포함시킬 패턴 유형 및 기능을 선택하기만 하면 됩니다. 프로젝트 환경 설정을 정의하고 나면 편집하거나, 실행 또는 디버그하거나, 로컬 또는 {{site.data.keyword.Bluemix}}에 배치할 수 있는 스타터 프로젝트가 생성됩니다. 


### 웹 앱
{: #web}

웹 프로젝트는 HTML, JavaScript 및 스타일시트와 같은 웹 컨텐츠를 웹 서버에 제공하는 기능을 추가합니다. 

다음 웹 스타터가 사용 가능합니다. 

* 기본 웹: 정적 `index.html` 파일, 기본 스타일시트(비어 있음) 및 JavaScript 파일을 제공합니다. 
* Webpack: ES6(ECMAScript 6) 소스 파일이 `src/client`에 있으며 이러한 파일을 브라우저에서 사용할 수 있도록 축소하고 변환하기 위해 WebPack을 사용하여 컴파일하는 프로젝트를 작성합니다. 
* Webpack + React: 사용자 인터페이스 빌드에 사용되는 리치 프레임워크입니다. 소스 파일은 `src/client/app`에 있으며 WebPack을 사용해 컴파일되어 공용 디렉토리에서 제공됩니다. 


### 모바일 앱
{: #mobile}

모바일 앱 패턴은 {{site.data.keyword.mobilepushshort}}, {{site.data.keyword.mobileanalytics_short}}, {{site.data.keyword.appid_short}} 등과 같은 백엔드 서비스와 직접 연결하는 모바일 앱을 빌드하는 데 도움을 줍니다. 프로젝트는 sdkGen(BFF 등) 및 마이크로서비스를 통해 추가될 수도 있습니다. 

{{site.data.keyword.watson}} Conversation, {{site.data.keyword.visualrecognitionshort}}, {{site.data.keyword.openwhisk_short}} 등과 같은 스타터 목록에서 선택할 수 있습니다. 

Swift, Android 또는 Cordova를 사용하여 모바일 앱을 생성할 수 있습니다. 


### BFF(Backend for Frontend)
{: #bff}

BFF(Backend for Frontend) 패턴은 실제로 사용자 상호작용 요구사항과 일치하는 양식으로 비즈니스 데이터 및 서비스를 노출하는 데 집중할 수 있도록 도움을 줍니다. 클라우드 솔루션에 대한 사용자의 경험을 최적화하려면, 모바일 애플리케이션에 대한 색다른 사용자 경험과 웹 애플리케이션에 대한 더 풍부하고 자세한 경험이 필요할 수 있습니다. [{{site.data.keyword.conversationfull}} ![외부 링크 아이콘](../icons/launch-glyph.svg "외부 링크 아이콘")](https://www.ibm.com/watson/developercloud/conversation.html) 서비스와 같은 음성 제어 디바이스를 사용하면 사용자와의 상호작용이 음성으로 제어될 수 있습니다. 이 디지털 채널은 음성 집중 기반 상호작용을 관리하기 위해 매우 다양한 BFF가 필요할 것입니다. 

{{site.data.keyword.Bluemix_notm}}를 사용하면, 여러 언어를 사용하는 프로그래밍 접근 방식을 통해 BFF를 빌드하여 BFF를 정의할 수 있습니다. IBM에서는 Node.js, Swift 또는 Java를 사용하고, 이를 Cloud Foundry, 컨테이너 서비스 또는 서버리스(serverless)로 클라우드 네이티브 패턴에서 실행하는 것을 권장합니다. 

BFF는 데이터 지속성, 캐싱을 위한 서비스와의 통합 및 {{site.data.keyword.ibmwatson}}, {{site.data.keyword.iot_short_notm}}, {{site.data.keyword.weather_short}}와 같은 높은 가치를 제공하는 서비스 및 {{site.data.keyword.sparks}}와 같은 데이터 분석과의 통합을 관리합니다. 

BFF는 가장 일반적으로 REST 패턴을 사용하여 API를 노출하게 되지만, {{site.data.keyword.messagehub}}를 사용하여 메시징 아키텍처에서 작동하도록 BFF를 디자인할 수 있습니다. 

BFF 기본 스타터는 Node.js 또는 Swift를 사용하여 사용 가능합니다. 


### 마이크로서비스
{: #microservice}

마이크로서비스 프로젝트는 기본 상태 엔드포인트인 REST API를 포함한 백엔드 마이크로서비스를 빌드하기 위한 기초를 제공합니다. 생성되는 프로젝트는 마이크로서비스 자체 및 연결된 클라우드 서비스에서 필요로 하는 모든 종속 항목을 포함합니다. 

마이크로서비스 기본 스타터는 Java를 사용하여 이용 가능합니다. 

<!--
## Other
{: #other}

The Other pattern represents a project that consists of only the language-specific server-side web framework. It has all the other file assets to work with the project, such as needed libraries and config files.

Content to be provided by Karl Bishop.
-->


### 언어
{: #languages notoc}

지원되는 언어는 다음과 같습니다. 

   * [Java ![외부 링크 아이콘](../icons/launch-glyph.svg "외부 링크 아이콘")](../runtimes/liberty/getting-started.html){: new_window}
   * [Node.js ![외부 링크 아이콘](../icons/launch-glyph.svg "외부 링크 아이콘")](../runtimes/nodejs/getting-started.html){: new_window}
   * [Swift ![외부 링크 아이콘](../icons/launch-glyph.svg "외부 링크 아이콘")](../runtimes/swift/getting-started.html){: new_window}


#### Java
{: #java notoc}

Java에는 엔터프라이즈급 애플리케이션을 빌드할 수 있는 검증된 기능이 있습니다. 그러나 Java 8의 새 기능을 통해, Java는 Liberty 등의 경량 런타임이나 Spring Boot와 같은 프레임워크와 함께 마이크로서비스를 빌드하는 경우에도 사용하기 적절한 언어가 되었습니다. 


#### Node.js
{: #node notoc}

Node.js는 이벤트 중심의 비차단 I/O 모델을 사용하는 JavaScript 런타임으로, 경량이고 효율적이며 웹 애플리케이션, BFF 패턴 및 마이크로서비스의 처리량 및 확장성 측면에서 탁월합니다. Node.js의 패키지 에코시스템인 npm은 많은 오픈 소스 모듈에 대한 액세스를 제공함으로써 애플리케이션 개발 속도를 높일 수 있는 다양한 기능을 제공합니다. 


#### Swift
{: #swift notoc}

Swift는 2014년에 Apple에서 만든 최신 프로그래밍 언어로, Objective C 사용을 대체하기 위해 디자인되었으며 2015년 12월 오픈 소스로 전환되었습니다. 현재는 x86, ARM 또는 Z 아키텍처를 사용하는 Linux 및 macOS 운영 체제의 iOS, macOS, 웹 서비스 및 시스템 소프트웨어를 빌드하는 데 사용됩니다. 이 언어는 스크립팅 언어처럼 작성되지만 낮은 오버헤드로 C와 유사한 고성능을 달성할 수 있도록 컴파일되어 클라우드 런타임에 적합합니다. 이 언어는 Java에서 볼 수 있는 강력하고 정적인 유형의 시스템을 사용하는 동시에 JavaScript에서 볼 수 있는 기능 스타일 및 비동기 루틴을 사용합니다. 이 언어는 성능이 뛰어나며, 소스는 LLVM 컴파일러 도구 체인을 사용하여 네이티브 코드로 컴파일되고 C로 작성된 외부 시스템 라이브러리를 쉽게 이용할 수 있습니다. 


## 스타터
{: #starters}

{{site.data.keyword.Bluemix}} {{site.data.keyword.dev_console}}을 사용하면 각 패턴 유형에 대해 다양한 스타터를 선택할 수 있습니다. 

스타터는 고가치 서비스와 {{site.data.keyword.Bluemix_notm}}의 주요 통합을 보여주는 데 초점을 맞춘, 프로덕션 준비가 완료된 스타터 코드로서 최적화되어 있습니다. 각 스타터는 하나의 서비스에 초점을 맞추고 코드에 대한 서비스 SDK의 통합을 표시합니다. 스타터에서 서비스 데이터의 통합 또는 사용자와의 상호작용을 강조하는 단순 사용자 경험을 제공하는 경우도 있습니다. 각 스타터는 사용자가 인증, 데이터 및 기타 기능을 프로젝트에 구성하고자 하는 경우 이를 사용할 수 있도록 구성됩니다. 
