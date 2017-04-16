---

copyright:
  years: 2016, 2017
lastupdated: "2017-03-18"

---
{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen:.screen}
{:codeblock: .codeblock}

# 코드 가져오기
{: #Get_Code}

선택한 기능을 사용하여 프로젝트의 구성 및 설정을 완료하면 코드를 다운로드하여 실행할 수 있습니다. 다운로드한 프로젝트는 사용자가 구성한 각 기능의 신임 정보와 필수 SDK 종속 항목을 사용하여 사전 구성됩니다. 

다운로드한 프로젝트에서 구성할 수 없는 서비스의 신임 정보를 완료해야 합니다. 스타터 프로젝트의 `README.md` 파일에 지시사항이 포함되어 있습니다. Markdown 뷰어에서 `README.md` 파일을 보고 설정을 완료하십시오. 

## 전제조건 개발자 도구
{: #prereq-dev-tools}

{{site.data.keyword.Bluemix_notm}} {{site.data.keyword.dev_console}}에서 생성된 코드에 대한 작업을 수행할 경우 다음 개발자 도구가 필요합니다. 


### 일반
{: #general notoc}

* [Homebrew ![외부 링크 아이콘](../icons/launch-glyph.svg "외부 링크 아이콘")](http://brew.sh/)
	* Apple 개발자가 기타 도구와 런타임(예: CocoaPods, Carthage)을 설치할 수 있도록 지원하는 명령행 도구입니다. 

* [Docker ![외부 링크 아이콘](../icons/launch-glyph.svg "외부 링크 아이콘")](https://www.docker.com/get-docker)
	* 컨테이너 내 애플리케이션의 실행 및 디버깅을 지원하는 오픈 소스 프로젝트입니다. 비모바일 프로젝트의 경우에만 필수입니다. 

### {{site.data.keyword.Bluemix_notm}}
{: #bluemix notoc}

* {{site.data.keyword.apiconnect_short}} Loopback 및 기타 {{site.data.keyword.Bluemix_notm}} Productivity 도구 실행을 지원하는 Node.js(Node 및 npm 런타임). 

	{{site.data.keyword.apiconnect_short}} 도구를 로컬로 실행하려면 Node 5.x를 사용하십시오. 
	
	```
	$ brew install Node5
	```

* [Bluemix CLI 도구 ![외부 링크 아이콘](../icons/launch-glyph.svg "외부 링크 아이콘")](http://clis.ng.bluemix.net/ui/home.html)

   {{site.data.keyword.Bluemix_notm}}에 대한 명령행 인터페이스에서 Cloud Foundry 런타임을 배치하는 데 필요한 명령행 도구입니다.   

* [{{site.data.keyword.dev_cli_notm}} ![외부 링크 아이콘](../icons/launch-glyph.svg "외부 링크 아이콘")](dev_cli.html)

	웹 및 모바일 프로젝트를 작성하고, 실행하고, 테스트하고, 배치하는 데 필요한 {{site.data.keyword.Bluemix_notm}} CLI 플러그인입니다. 
	
* [SDK Generator 플러그인 ![외부 링크 아이콘](../icons/launch-glyph.svg "외부 링크 아이콘")](sdk_cli.html)

	[Open API 스펙 ![외부 링크 아이콘](../icons/launch-glyph.svg "외부 링크 아이콘")](https://www.openapis.org/) 준수 REST API 정의로부터 SDK를 생성하는 데 필요한 {{site.data.keyword.Bluemix_notm}} CLI 플러그인입니다. 

### Android
{: #android notoc}

* [Android Studio 2.2 이상![외부 링크 아이콘](../icons/launch-glyph.svg "외부 링크 아이콘")](https://developer.android.com/studio)
	* 최신 [Android 7.0 ![외부 링크 아이콘](../icons/launch-glyph.svg "외부 링크 아이콘")](https://www.android.com/versions/nougat-7-0/) 런타임을 설치하십시오. 

### iOS
{: #ios notoc}

* [Xcode 8 ![외부 링크 아이콘](../icons/launch-glyph.svg "외부 링크 아이콘")](https://developer.apple.com/xcode/)(권장)

<!-- * Install the latest [iOS 10 ![External link icon](../icons/launch-glyph.svg "External link icon")](http://www.apple.com/ios/ios-10/) runtime.
-->
* iOS SDK 종속 항목 설치를 위한 [CocoaPods ![외부 링크 아이콘](../icons/launch-glyph.svg "외부 링크 아이콘")](https://cocoapods.org/) 종속 항목 관리자. 최신 버전을 사용하십시오. 

	```
	$ sudo gem install cocoapods --pre
	```
* {{site.data.keyword.watson}} Developer Cloud SDK를 설치하는 데 사용되는 [Carthage ![외부 링크 아이콘](../icons/launch-glyph.svg "외부 링크 아이콘")](https://github.com/Carthage/Carthage) 종속 항목 관리자. 

	```
	$ brew install carthage
	```
