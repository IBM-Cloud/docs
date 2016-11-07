---

copyright:
  years: 2016
lastupdated: "2016-10-18"

---
{:new_window: target="_blank"}

# 모바일 대시보드의 새로운 기능
{: #what_is_new}

마지막 업데이트 날짜: 2016년 10월 18일
{: .last-updated}

{{site.data.keyword.Bluemix}} 모바일 대시보드의 10월 업데이트에서 다음 변경사항이 도입되었습니다. 

   * 대시보드에서 직접 프로젝트에 Push Notifications 기능과 분석 기능을 추가할 수 있습니다. 
   * [코드 스타터](starters.html#Code_Starter)를 사용할 수 있습니다. 
   * Swift가 지원됩니다. 


### 분석
{: #analytics}

   * 분석 기능을 추가하면 기본적으로 데모 모드가 사용됩니다. 앱을 실행한 후 분석을 보기 위해 데모 모드를 토글하여 끌 수 있습니다. 


### UI 빌더
{: #ui_builder}

   * 프로젝트에서 **Push Notifications** 기능에 액세스할 수 있습니다. 
   * **프로젝트 설정** 탭의 이름이 **설정** 탭으로 바뀌었습니다. 
   * **인증** 탭의 이름이 **사용자 액세스** 탭으로 바뀌었습니다. 


### 코드
{: #code}

   * 생성된 iOS용 Objective-C 코드와 Swift 코드에서 CocoaPods를 사용하여 종속 항목을 관리합니다. 이는 CocoaPods를 설치해야 함을 의미합니다. 이를 설치하려면 `sudo gem install cocoapods`를 실행하십시오. CocoaPods 설치 후 `pod setup`을 실행하여 구성하십시오(아직 구성되지 않은 경우). 마지막으로 Xcode에서 `.xcworkspace` 파일을 열기 전에 `pod install`을 실행하여 필수 프로젝트 종속 항목을 다운로드하고 설치하십시오. 추가 세부사항은 다운로드된 코드 아카이브의 `README.md` 파일에 있습니다. 자세한 정보는 [전제조건 개발자 도구](get_code.html#prereq-dev-tools)를 살펴보십시오. 

자주 방문하여 추가되는 새 업데이트를 확인하십시오. 


# 관련 링크
{: #rellinks}

<!-- links to internal services don't work
## {{site.data.keyword.Bluemix_notm}} Mobile services
{: #general}
* [Mobile Analytics (Beta)](../services/mobileanalytics/index.html){: new_window}
* [Mobile Client Access](../services/mobileaccess/index.html){: new_window}
* [Mobile Foundation](../services/mobilefoundation/index.html){: new_window}
* [Mobile Quality Assurance)](../services/MobileQualityAssurance/index.html){: new_window}
* [Push Notifications](../services/mobilepush/index.html){: new_window}
-->

## 블로그 게시물
{: #general}
* [블로그 게시물: Introducing the Bluemix Mobile dashboard](https://developer.ibm.com/bluemix/2016/07/08/new-bluemix-mobile-dashboard/){: new_window}
* [블로그 게시물: Introducing the next generation of the Bluemix Mobile dashboard](https://ibm.com/blogs/bluemix/2016/10/introducing-the-next-generation-of-the-bluemix-mobile-dashboard/){: new_window}
* [블로그 게시물: Introducing Bluemix Mobile Code Starters](https://www.ibm.com/blogs/bluemix/2016/10/rapid-dev-with-mobile-code-starters/){: new_window}
* [블로그 게시물: Bluemix Mobile, Part 1: Creating a Store Catalog application](https://developer.ibm.com/bluemix/2016/07/13/bluemix-mobile-creating-store-catalog-app-part1/){: new_window}
* [블로그 게시물: Bluemix Mobile, Part 2: Integrating custom Bluemix backend into the Store Catalog app](https://developer.ibm.com/bluemix/2016/07/14/bluemix-mobile-integrating-custom-backend-part2/){: new_window}

## 튜토리얼 및 샘플
{: #samples}
* [Mobile Backend for Bluemix](https://github.com/ibm-bluemix-mobile-services/mobiledashboard-storecatalog-backend){: new_window}
