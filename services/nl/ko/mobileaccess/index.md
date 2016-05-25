---

copyright:
  years: 2015, 2016

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen:.screen}
{:codeblock:.codeblock}

# {{site.data.keyword.amashort}} 시작하기
{: #gettingstarted}
*마지막 업데이트 날짜: 2016년 3월 21일*

{{site.data.keyword.amafull}} 서비스를 사용하여 모바일 앱에 보안 및 모니터링 기능을 추가하십시오. 사용자가 기존 Google 또는 Facebook 계정으로 앱에 로그인할 수 있도록 클라이언트 인증 및 ID 제공자를 구성할 수 있습니다. 또한 모니터링 기능을 사용자 앱에 추가하여 클라이언트 로깅 및 사용 통계를 둘 다 사용할 수 있습니다.
{:shortdesc}

**참고:** {{site.data.keyword.amashort}} 서비스를 이전에는 Advanced Mobile Access라고 했습니다.


{{site.data.keyword.amashort}} 서비스를 시작하고 실행하려면 다음 단계를 따르십시오.

1. 클라이언트측 개발 환경을 설정하십시오.
{{site.data.keyword.amashort}} SDK를 기존 Android, Cordova 또는 iOS 앱에 추가할 수 있습니다. 또한 HelloAuthentication 샘플 애플리케이션도 다운로드할 수 있습니다.
   * **Android**: ([SDK](getting-started-android.html)) ([샘플](https://github.com/ibm-bluemix-mobile-services/bms-samples-android-helloauthentication))
   * **Cordova**: ([SDK](getting-started-cordova.html)) ([샘플](https://github.com/ibm-bluemix-mobile-services/bms-samples-cordova-helloauthentication))
   * **iOS(Swift SDK)**: ([SDK](getting-started-ios-swift-sdk.html)) ([샘플](https://github.com/ibm-bluemix-mobile-services/bms-samples-swift-helloauthentication))
   * **iOS(Objective-C SDK)**: ([SDK](getting-started-ios.html)) ([샘플](https://github.com/ibm-bluemix-mobile-services/bms-samples-ios-helloauthentication))

1. 서버측 자원을 보호하십시오. 모바일 사용 가능 OAuth 보안을 사용하여 Node.js 또는 Liberty for Java&trade; 런타임에서 실행 중인 모바일 백엔드 자원을 보호하십시오. 자세한 정보는 [자원 보호](protecting-resources.html)를 참조하십시오. 

1. 선택사항: 애플리케이션에 대해 ID 제공자를 구성하십시오. 애플리케이션당 하나의 ID 제공자를 구성할 수 있습니다. ID 제공자를 구성하면 모바일 앱 사용자가 기존 Facebook 또는 Google+ 계정으로 로그인할 수 있습니다. 또는 사용자 정의 인증을 작성하여 사용자의 로그인 방법을 정의할 수 있습니다.
   * [Facebook](facebook-auth-overview.html)
   * [Google](google-auth-overview.html)
   * [사용자 정의 ](custom-auth.html)

1. 앱 모니터링 및 로깅을 구성하십시오. 자세한 정보는 [앱 모니터링](app-monitoring.html)을 참조하십시오. 

# 관련 링크
{: #rellinks}

## 학습서 및 샘플
{: #samples}
* [android-helloauthentication 샘플](https://github.com/ibm-bluemix-mobile-services/bms-samples-android-helloauthentication){: new_window}
* [ios-helloauthentication 샘플(Swift SDK)](https://github.com/ibm-bluemix-mobile-services/bms-samples-swift-helloauthentication){: new_window}
* [ios-helloauthentication 샘플(Objective-C SDK)](https://github.com/ibm-bluemix-mobile-services/bms-samples-ios-helloauthentication){: new_window}

## SDK
{: #sdk}
* [코어 SDK(Android)](https://github.com/ibm-bluemix-mobile-services/bms-clientsdk-android-core){: new_window}
* [코어 SDK(Cordova 플러그인)](https://github.com/ibm-bluemix-mobile-services/bms-clientsdk-cordova-plugin-core){: new_window}
* [코어 SDK(iOS - Swift)](https://github.com/ibm-bluemix-mobile-services/bms-clientsdk-swift-core){: new_window}
* [코어 SDK(iOS - Objective-C) ](https://hub.jazz.net/git/bluemixmobilesdk/imf-ios-sdk/archive?revstr=master){: new_window}
* [사용자 정의 인증 - 단순 샘플](https://github.com/ibm-bluemix-mobile-services/bms-mca-custom-identity-provider-sample){: new_window}
* [사용자 정의 인증 - 고급 샘플](https://github.com/ibm-bluemix-mobile-services/bms-mca-custom-identity-provider-with-user-management){: new_window}

## API 참조
{: api}
* [Android](https://console.{DomainName}/docs/api/content/api/mobilefirst/android/core-api-doc/overview-summary.html){: new_window}
* [iOS(Objective-C SDK)](https://console.{DomainName}/docs/api/content/api/mobilefirst/ios/IMFCore_api-doc/html/index.html){: new_window}


## 관련 링크
{: #general}
* [개요](overview.html){: new_window}
