---

copyright:
  years: 2016, 2017
lastupdated: "2017-01-17"

---
{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen:.screen}
{:codeblock: .codeblock}

# 코드 가져오기
{: #Get_Code}

선택한 기능을 사용하여 모바일 프로젝트의 구성과 설정을 완료하면 코드를 다운로드하여 Xcode 또는 Android Studio에서 실행할 수 있습니다. 다운로드한 프로젝트는 사용자가 구성한 각 기능의 신임 정보와 필수 SDK 종속 항목을 사용하여 사전 구성됩니다. 

다운로드한 프로젝트에서 구성할 수 없는 서비스의 신임 정보를 완료해야 합니다. 스타터 프로젝트의 `README.md` 파일에 지시사항이 포함되어 있습니다. Markdown 뷰어에서 `README.md` 파일을 보고 설정을 완료하십시오. 

### 전제조건 개발자 도구
{: #prereq-dev-tools}

{{site.data.keyword.Bluemix_notm}} 모바일 대시보드에서 생성된 코드에 대한 작업을 수행할 경우 다음 개발자 도구가 필요합니다. 

#### Android
* [Android Studio 2.2 ![외부 링크 아이콘](../icons/launch-glyph.svg "외부 링크 아이콘")](https://developer.android.com/studio "외부 링크 아이콘")
	* 최신 [Android 7.0 ![외부 링크 아이콘](../icons/launch-glyph.svg "외부 링크 아이콘")](https://www.android.com/versions/nougat-7-0/ "외부 링크 아이콘") 런타임을 설치하십시오. 

#### iOS
* [Xcode 8.0 ![외부 링크 아이콘](../icons/launch-glyph.svg "외부 링크 아이콘")](https://developer.apple.com/xcode/ "외부 링크 아이콘")(권장)
	* 최신 [iOS 10 ![외부 링크 아이콘](../icons/launch-glyph.svg "외부 링크 아이콘")](http://www.apple.com/ios/ios-10/ "외부 링크 아이콘") 런타임을 설치하십시오. 
* [Homebrew ![외부 링크 아이콘](../icons/launch-glyph.svg "외부 링크 아이콘")](http://brew.sh/ "외부 링크 아이콘")
	* Apple 개발자가 기타 도구와 런타임(예: CocoaPods, Carthage)을 설치할 수 있도록 지원하는 명령행 도구입니다. 
* iOS SDK 종속 항목 설치에 필요한 [CocoaPods ![외부 링크 아이콘](../icons/launch-glyph.svg "외부 링크 아이콘")](https://cocoapods.org/ "외부 링크 아이콘") 종속 항목 관리자. 최신 버전을 사용하십시오. 

	```
	$ sudo gem install cocoapods --pre
	```
* Watson Developer Cloud SDK 설치에 필요한 [Carthage ![외부 링크 아이콘](../icons/launch-glyph.svg "외부 링크 아이콘")](https://github.com/Carthage/Carthage "외부 링크 아이콘") 종속 항목 관리자. 

	```
	$ brew install carthage
	```

#### {{site.data.keyword.Bluemix_notm}}
* API Connect Loopback 및 기타 Bluemix Productivity 도구 실행을 지원하는 NodeJS(노드 및 NPM 런타임). 

	API Connect 도구를 로컬로 실행하려면 Node 5.x를 사용하십시오. 
	```
	$ brew install Node5
	```

* [Bluemix CLI 도구 ![외부 링크 아이콘](../icons/launch-glyph.svg "외부 링크 아이콘")](http://clis.ng.bluemix.net/ui/home.html "외부 링크 아이콘").
Bluemix를 사용하여 명령행 인터페이스에서 Cloud Foundry 런타임을 간편하게 배치하는 명령행 도구입니다.   
