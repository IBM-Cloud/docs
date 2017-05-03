---

copyright:
  years: 2015, 2017
lastupdated: "2017-03-23"
---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}

# Swift용 IBM Bluemix 런타임
{: #swift_runtime}

{{site.data.keyword.Bluemix}}의 Swift용 런타임은 [Swift용 IBM Bluemix 빌드팩](https://github.com/IBM-Swift/swift-buildpack)(즉, swift_buildpack)으로 구현됩니다.
이 빌드팩에서는 Swift 애플리케이션을 위한 완전한 런타임 환경을 제공합니다.
{: shortdesc}

## 스타터 애플리케이션
{: #starter_application}

{{site.data.keyword.Bluemix}}에서는 Kitura 기반 Swift [스타터 애플리케이션](https://github.com/IBM-Bluemix/Kitura-Starter)을 제공합니다. Kitura 스타터 앱은 Swift 프로그래밍 언어를 사용하여 개발할 수 있는 서버 애플리케이션 유형에 대해 학습하는 데 사용할 수 있는 단순한 Swift 앱니다. 이 샘플 앱은 클라이언트에 HTML 컨텐츠를 리턴하는 기본 Kitura HTTP 서버를 작성합니다. 

**참고:** Kitura 스타터 앱은 교육용으로 사용됩니다. 변경을 수행하여 스타터 앱을 시험해 보고 이러한 변경사항을 {{site.data.keyword.Bluemix}} 환경에 푸시할 수 있습니다. 스타터 애플리케이션 사용에 대한 도움말은 [스타터 애플리케이션 사용](../../cfapps/starter_app_usage.html)을 참조하십시오. 

## 앱 이름 바꾸기
{: #renaming_your_app}

Kitura 스타터에서 또는 일반적인 상황에서 앱의 이름을 바꾸려는 경우 몇 가지 변경을 수행해야 합니다. 그러면 혼란을 피하고 오류 없이 개발을 수행할 수 있습니다. 

- 앱의 이름과 일치하도록 앱의 프로젝트 폴더 이름을 바꾸십시오.
- `Package.swift` - 다음 항목을 변경하십시오.
    - `name` - 앱 이름과 일치해야 합니다.
    - `targets[Target(name:)]` - 앱 이름과 일치해야 합니다.
- `manifest.yml` - 다음 항목을 변경하십시오.
    - `name` - 앱 이름과 일치해야 합니다.
    - `command` - 앱을 시작할 실행 파일의 이름입니다(Package.swift 파일에 지정된 이름과 일치해야 함).

## 런타임 버전
{: #runtime_versions}

기본적으로 {{site.data.keyword.Bluemix}}에 호스팅되는 Swift용 런타임(swift_buildpack)에서는 Swift 바이너리의 최신 GA 버전을 사용합니다. 이 버전은 IBM에서 직접 지원하는 유일한 Swift 버전이며 앱에서 사용하도록 권장되는 버전입니다. swift_buildpack의 [최신 릴리스 정보](https://github.com/IBM-Swift/swift-buildpack/releases)를 검토하여 이러한 지원되는 버전을 판별할 수 있습니다. 빌드팩은 해당 [manifest.yml](https://github.com/IBM-Swift/swift-buildpack/blob/master/manifest.yml) 파일 내에 표시된 다른 Swift 버전을 나열할 수도 있습니다. 일반적이지만 지원되지는 않는 이러한 Swift 버전은 빌드팩에서 미리 캐시되며 이는 프로비저닝 시간을 줄여줍니다.

{{site.data.keyword.Bluemix}}에 있는 다른 버전의 Swift를 애플리케이션에 사용하려는 경우 저장소의 루트에 `.swift-version` 파일과 해당 버전을 지정할 수 있습니다. 이 `.swift-version` 파일은 swift_buildpack에서 사용하는 Swift 버전을 정의합니다. 

```
$ cat .swift-version
3.0
```
{: pre}

Swift 언어는 자주 변경되므로 사용하는 애플리케이션과 함께 작동하는 것으로 알려진 Swift 버전에 앱이 "고정"되도록 항상 `.swift-version` 파일을 포함시켜야 합니다. 

`.swift-version` 파일에서 올바른 버전의 Swift를 지정할 수 있습니다. 이러한 대체 버전은 [Swift.org ![외부 링크 아이콘](../../icons/launch-glyph.svg "외부 링크 아이콘")](https://swift.org/download/)의 이름 지정 방식과 일치해야 하며 이 사이트에서 직접 가져와야 합니다. 비캐시 버전을 사용하는 경우 프로비저닝하는 데 시간이 좀 더 걸리지만 Swift 앱의 런타임 성능에는 차이가 없습니다. 

앱의 루트 디렉토리에 `Package.swift` 파일이 있으면 {{site.data.keyword.Bluemix}}의 기본 swift_buildpack이 사용됩니다. 대체 빌드팩을 사용하려면 앱의 manifest.yml 파일에 `buildpack: {buildpackUrl}` 항목을 추가하여 대체 빌드팩을 지정해야 합니다. 또는 배치 시 `cf push -b {buildpackUrl}` 명령 인수를 사용하여 대체 빌드팩을 정의할 수 있습니다. 


## 개발자 환경

개발자는 Swift로 서버 측 애플리케이션을 작성할 때 몇 가지 옵션을 사용할 수 있습니다. Apple의 MacOS 디바이스를 사용하는 개발자는 Xcode IDE가 요구사항이 아님에도 불구하고 이를 사용하는 것을 선호할 수 있습니다. {{site.data.keyword.Bluemix}}에서 배치되고 실행되는 Swift 기반 앱은 모든 프로그래밍 편집기 또는 IDE를 사용할 수 있습니다. Swift의 구문 강조표시 및 린팅(linting)을 다수의 인기있는 편집기에 사용할 수 있습니다. [Swift.org ![외부 링크 아이콘](../../icons/launch-glyph.svg "외부 링크 아이콘")](https://swift.org/)의 바이너리에 포함된 Swift REPL 명령행 도구를 통해 {{site.data.keyword.Bluemix}}에 배치하기 전에 로컬 컴파일과 테스트를 수행할 수 있습니다.

MaxOS 사용자는 {{site.data.keyword.Bluemix}}에서 실행되는 서버 측 Swift 앱을 쉽게 작성, 개발, 관리 및 제어할 수 있는 [IBM Cloud Tools for Swift](http://cloudtools.bluemix.net/)를 사용할 수 있습니다.   


## 향상된 통합

[Kitura 웹 프레임워크](http://ibm-swift.github.io/Kitura/)를 함께 사용하면 다수의 기능을 제공합니다. Kitura는 모듈러 특성을 가지므로 곧 패키지된 SDK로 해당 기능을 확장하여 다양한 데이터베이스, Watson 기반 서비스에 대한 액세스 및 인증과 같은 기능을 제공하려 할 것입니다. Kitura는 직접 여러 데이터베이스에 대한 지원을 제공하는 반면 기타 오픈 소스 프로젝트는 여러 데이터베이스 플랫폼용 SDK도 제공합니다. 다음은 Kitura에서 제공하며 외부 리소스와 연동되는 일부 SDK 목록입니다.

- [IBM Watson](https://swiftpkgs.ng.bluemix.net/package/IBM-Swift/swift-watson-sdk)
- [IBM DB2 and DashDB](https://swiftpkgs.ng.bluemix.net/package/IBM-DTeam/swift-for-db2)
- [IBM Cloudant 및 CouchDB](https://swiftpkgs.ng.bluemix.net/package/cloudant/swift-cloudant)
- [IBM ObjectStorage](https://swiftpkgs.ng.bluemix.net/package/ibm-bluemix-mobile-services/bluemix-objectstorage-serversdk-swift)
- [Apache Cassandra](https://swiftpkgs.ng.bluemix.net/package/IBM-Swift/Kassandra)
- [Aphid MQTT](https://swiftpkgs.ng.bluemix.net/package/IBM-Swift/Aphid)

애플리케이션에 포함시킬 추가 Swift 패키지를 찾으려면 [IBM Swift Package Catalog](https://swiftpkgs.ng.bluemix.net/)로 이동하여 대상 서비스 또는 데이터베이스에 대해 검색을 수행하십시오. Package Catalog에서는 Swift 애플리케이션에 포함시킬 수 있는 패키지를 쉽게 찾을 수 있는 방법을 제공합니다. 패키지의 Git URL 및 버전 세부사항을 앱의 `Package.swift` 파일에 포함시킴으로써 Swift 애플리케이션에 패키지를 추가할 수 있습니다. 패키지 관리에 대한 세부사항은 [Swift.org의 Package Manager 섹션](https://swift.org/package-manager/)을 참조하십시오. 


## 관련 정보

Swift 개발자가 사용할 수 있는 IBM의 다른 온라인 도구도 있습니다. 
- [IBM Swift DevCenter](https://developer.ibm.com/swift/) - 모든 IBM Swift 정보의 기본 랜딩 사이트입니다. 오퍼링, 블로그, 소셜 이벤트, 문서 등에 대한 정보를 찾을 수 있습니다. 
- [IBM Swift Sandbox](https://swiftlang.ng.bluemix.net/) - 이 사이트에서는 다양한 버전의 Swift에 대해, 그리고 서로 다른 Swift 런타임 플랫폼에서 Swift 코드 단편을 빠르고 쉽게 시험해 볼 수 있는 환경을 제공합니다. 또한 코드 샘플을 저장하고 다른 사용자와 공유할 수 있으며, 다른 사용자가 제공한 인기있는 예를 탐색할 수도 있습니다. 


# rellinks
{: #rellinks notoc}
## general
{: #general notoc}
* [IBM Swift DevCenter](https://developer.ibm.com/swift/)
* [IBM Cloud Tools for Swift](http://cloudtools.bluemix.net/)
* [IBM Swift Package Catalog](https://swiftpkgs.ng.bluemix.net/)
* [IBM Swift Sandbox](https://swiftlang.ng.bluemix.net/)
* [Kitura 문서 및 API](http://ibm-swift.github.io/Kitura/)
* [Bluemix용 Kitura 스타터 앱](https://github.com/IBM-Bluemix/Kitura-Starter)
* [Swift용 IBM Bluemix 빌드팩](https://github.com/IBM-Swift/swift-buildpack)
* [Swift용 IBM Bluemix 빌드팩 릴리스 정보](https://github.com/IBM-Swift/swift-buildpack/releases)
* [Swift.org ![외부 링크 아이콘](../../icons/launch-glyph.svg "외부 링크 아이콘")](https://swift.org/)
* [Swift 언어 문서 ![외부 링크 아이콘](../../icons/launch-glyph.svg "외부 링크 아이콘")](https://swift.org/documentation)
