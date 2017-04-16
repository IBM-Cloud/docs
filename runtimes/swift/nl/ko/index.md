{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .pre}


# Swift용 IBM Bluemix 런타임
{: #swift_runtime}
마지막 업데이트 날짜: 2016년 9월 19일
{: .last-updated}

{{site.data.keyword.Bluemix}}의 Swift용 런타임은 [Swift용 IBM Bluemix 빌드팩](https://github.com/IBM-Swift/swift-buildpack)에서 제공됩니다(예: swift_buildpack).
이 빌드팩은 Swift 애플리케이션에 대한 전체 런타임 환경을 제공합니다.
{: shortdesc}

## 스타터 애플리케이션
{: #starter_application}

{{site.data.keyword.Bluemix}}는 Kitura 기반 Swift [스타터 애플리케이션](https://github.com/IBM-Swift/Kitura-Starter-Bluemix)을 제공합니다. Kitura 스타터 앱은 Swift 프로그래밍 언어를 사용하여 개발할 수 있는 서버 애플리케이션 유형에 대해 알아보기 위해 사용할 수 있는 단순한 Swift 앱입니다. 이 샘플 앱은 HTML 컨텐츠를 클라이언트로 리턴하는 기본 Kitura HTTP 서버를 작성합니다.

**참고:** Kitura 스타터 앱은 교육 용도로 사용됩니다. 개선사항을 작성하여 스타터 앱을 실험할 수 있으며 이러한 변경사항을 {{site.data.keyword.Bluemix}} 환경으로 푸시할 수 있습니다. 스타터 애플리케이션 사용에 대한 도움말은 [스타터 애플리케이션 사용](../../cfapps/starter_app_usage.html)을 참조하십시오. 

## 앱 이름 바꾸기
{: #renaming_your_app}

Kitura Starter에서 또는 더 일반적인 상황에서 앱의 이름을 바꾸려는 경우, 몇 가지 변경사항을 적용해야 합니다. 이를 통해 혼동을 피하고 오류 없이 배치를 진행할 수 있습니다.

- 앱의 이름과 일치하도록 앱의 프로젝트 폴더 이름을 바꾸십시오.
- `Package.swift` - 다음 항목을 변경하십시오.
    - `name` - 앱 이름과 일치해야 합니다.
    - `targets[Target(name:)]` - 앱 이름과 일치해야 합니다.
- `manifest.yml` - 다음 항목을 변경하십시오.
    - `name` - 앱 이름과 일치해야 합니다.
    - `host` - 앱의 URL의 기본 호스트 세그먼트를 나타냅니다.
- `Procfile` - `web`의 값은 앱의 디렉토리 이름과 일치해야 합니다. 이는 웹 앱을 시작하는 컴파일 후의 명령 실행입니다.


## 런타임 버전
{: #runtime_versions}

기본적으로 {{site.data.keyword.Bluemix}}에서 호스팅되는 Swift용 런타임(swift_buildpack)은 Swift 2진의 최신 GA 버전을 사용합니다. 이는 IBM에서 직접 지원되는 Swift의 유일한 버전이며 앱에서 사용할 권장 버전입니다. swift_buildpack의 [최신 릴리스 정보](https://github.com/IBM-Swift/swift-buildpack/releases)를 조사하여 이 지원되는 버전을 판별할 수 있습니다. 빌드팩의 [manifest.yml](https://github.com/IBM-Swift/swift-buildpack/blob/master/manifest.yml) 파일에서 다른 Swift 버전 목록을 확인할 수 있습니다. 공통적이지만 지원되지 않는 이러한 Swift 버전은 빌드팩 내에서 사전에 캐시되며, 이는 프로비저닝 시간을 줄여 줍니다.

{{site.data.keyword.Bluemix}}에서 애플리케이션에 대해 Swift의 다른 버전을 사용하려는 경우, 저장소의 루트에서 `.swift-version` 파일로 버전을 지정할 수 있습니다. 이 `.swift-version` 파일은 swift_buildpack에서 사용될 Swift 버전을 정의합니다.

```
$ cat .swift-version
3.0
```
{: pre}

Swift 언어는 자주 업데이트되므로 사용자의 앱이 작동하는 Swfit 버전에 사용자 앱을 "고정"시키도록 `.swift-version` 파일을 항상 포함해야 합니다.

`.swift-version` 파일에 올바른 버전의 모든 Swift를 지정할 수 있음을 기억하십시오. 이러한 대체 버전은 [Swift.org](https://swift.org/download/)의 이름 지정과 일치해야 하며 이곳으로부터 직접 가져옵니다. 캐시되지 않은 버전의 사용은 프로비저닝에 좀 더 시간이 걸리는 반면 Swift 앱의 런타임 성능 차이점은 없습니다.

{{site.data.keyword.Bluemix}}의 기본 swift_buildpack은 앱의 루트 디렉토리에 `Package.swift` 파일이 포함된 경우 사용됩니다. 대체 빌드팩을 사용하려는 경우, `buildpack: {buildpackUrl}` 항목을 앱의 manifest.yml 파일에 추가하여 이를 지정해야 합니다. 또는 `cf push -b {buildpackUrl}` 명령 인수를 사용하여 배치 시에 이를 정의할 수 있습니다.


## 개발자 환경

Swift로 서버 측 애플리케이션을 작성할 경우 개발자에게는 몇 가지 옵션이 있습니다. Apple의 MacOS 디바이스를 사용하는 개발자들은 비록 요구사항이 아니더라도 Xcode IDE의 사용을 선호할 수 있습니다. {{site.data.keyword.Bluemix}}에서 배치되고 실행되는 Swift 기반 앱은 모든 종류의 프로그래밍 편집기 또는 IDE를 사용할 수 있습니다. 인기 있는 편집기 대부분이 Swift에 대한 구문 강조표시 및 린트 기능을 지원합니다. [Swift.org](https://swift.org/)의 2진에 포함된 Swift REPL 명령행 도구를 사용하여 {{site.data.keyword.Bluemix}}에 배치하기 전에 로컬 컴파일 및 테스트를 할 수 있습니다.

MaxOS 사용자의 경우 {{site.data.keyword.Bluemix}}에서 실행 중인 서버 측 Swift 앱의 작성, 배치, 관리 및 제어를 간소화하는 [IBM Cloud Tools for Swift](http://cloudtools.bluemix.net/)를 사용할 수 있습니다.   


## 개선된 통합

[Kitura 웹 프레임워크](http://ibm-swift.github.io/Kitura/)로 작업하면 다양한 기능을 사용할 수 있습니다. 특성상 Kitura는 모듈이기 때문에 패키지화된 SDK를 통해 Kitura의 기능을 확장하여 인증, Watson 기반 서비스 액세스, 다양한 데이터베이스 등의 기능을 제공할 수 있습니다. Kitura는 직접 다양한 데이터베이스에 대한 지원을 제공하는 반면 기타 오픈 소스 프로젝트는 다양한 데이터베이스 플랫폼용 SDK 또한 제공합니다. 다음은 외부 리소스와 작업하도록 Kitura에서 제공되는 SDK의 목록(모든 항목을 포함하지는 않음)입니다.

- [IBM Watson](https://swiftpkgs.ng.bluemix.net/package/IBM-Swift/swift-watson-sdk)
- [IBM DB2 및 DashDB](https://swiftpkgs.ng.bluemix.net/package/IBM-DTeam/swift-for-db2)
- [IBM Cloudant 및 Couchbase](https://swiftpkgs.ng.bluemix.net/package/cloudant/swift-cloudant)
- [IBM ObjectStorage](https://swiftpkgs.ng.bluemix.net/package/ibm-bluemix-mobile-services/bluemix-objectstorage-serversdk-swift)
- [Apache Cassandra](https://swiftpkgs.ng.bluemix.net/package/IBM-Swift/Kassandra)
- [Aphid MQTT](https://swiftpkgs.ng.bluemix.net/package/IBM-Swift/Aphid)

애플리케이션에 포함시킬 추가 Swift 패키지를 찾으려면 [IBM Swift Package Catalog](https://swiftpkgs.ng.bluemix.net/)로 이동하여 대상 서비스 또는 데이터베이스에 대해 검색을 수행하십시오. Package Catalog는 Swift 애플리케이션에 포함시킬 수 있는 패키지를 찾는 쉬운 방법을 제공합니다. 패키지의 Git URL 및 버전 세부사항을 앱의 `Package.swift` 파일에 포함시킴으로써 해당 패키지를 Swift 애플리케이션에 추가할 수 있습니다. 패키지 관리에 대한 세부사항은 [Swift.org의 Package Manager 섹션](https://swift.org/package-manager/)을 참조하십시오.


## 관련 정보

Swift 개발자에게 제공되는 다른 IBM 온라인 도구도 있습니다.
- [IBM Swift DevCenter](https://developer.ibm.com/swift/) - 모든 IBM Swift 정보에 대한 기본 랜딩 사이트. 오퍼링, 블로그, 소셜 이벤트, 문서 등에 대한 정보를 찾을 수 있습니다.
- [IBM Swift Sandbox](https://swiftlang.ng.bluemix.net/) - 이 사이트는 Swift의 다양한 버전에 대해, 더 나아가 다른 Swift 런타임 플랫폼에서 Swift 코드 단편을 쉽고 빠르게 테스트할 수 있는 환경을 제공합니다. 또한 코드를 저장하고 다른 사용자와 공유하거나 다른 사용자가 제공하는 인기 있는 예제를 살펴볼 수도 있습니다.


# 관련 링크
{: #rellinks}
## 일반
{: #general}
* [IBM Swift DevCenter](https://developer.ibm.com/swift/)
* [IBM Cloud Tools for Swift](http://cloudtools.bluemix.net/)
* [IBM Swift Package Catalog](https://swiftpkgs.ng.bluemix.net/)
* [IBM Swift Sandbox](https://swiftlang.ng.bluemix.net/)
* [Kitura 문서 및 API](http://ibm-swift.github.io/Kitura/)
* [Bluemix용 Kitura 스타터 앱](https://github.com/IBM-Swift/Kitura-Starter-Bluemix)
* [Swift용 IBM Bluemix 빌드팩](https://github.com/IBM-Swift/swift-buildpack)
* [Swift용 IBM Bluemix 빌드팩 릴리스 정보](https://github.com/IBM-Swift/swift-buildpack/releases)
* [Swift.org](https://swift.org/)
* [Swift 언어 문서](https://swift.org/documentation)
