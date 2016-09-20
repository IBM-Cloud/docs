---

copyright:
  years: 2015, 2016

---


# {{site.data.keyword.amashort}} 시작하기
{: #gettingstarted}
마지막 업데이트 날짜: 2016년 7월 21일
{: .last-updated}

{{site.data.keyword.amafull}} 서비스를 사용하여 모바일 앱에 보안을 추가하십시오. 사용자가 기존 Google 또는 Facebook 계정으로 앱에 로그인할 수 있도록 클라이언트 인증 및 ID 제공자를 구성할 수 있습니다.
{:shortdesc}

**참고:** {{site.data.keyword.amashort}} 서비스를 이전에는 Advanced Mobile Access라고 했습니다.


{{site.data.keyword.amashort}} 서비스를 시작하고 실행하려면 다음을 수행하십시오. 

1. {{site.data.keyword.Bluemix_notm}} 대시보드를 사용하여 모바일 백엔드 애플리케이션을 작성하거나, 기존 애플리케이션을 구성하십시오. 
  - {{site.data.keyword.Bluemix_notm}} 카탈로그에서 **MobileFirst Services Starter** 표준 유형을 선택할 수 있습니다. 
  - 또한 기존 애플리케이션에 서비스를 바인드하여 구성할 수 있습니다.

   MobileFirst Services Starter를 사용하는 경우 사용자 정의 백엔드 로직을 구현하기 위해 IBM {{site.data.keyword.Bluemix_notm}}에서 실행하는 Node.js 런타임의 인스턴스를 가져옵니다. 보안, 데이터, 푸시 및 모니터링 기능을 제공하는 코어 모바일 서비스 세트가 해당 Node.js 앱으로 바인드됩니다. {{site.data.keyword.Bluemix_notm}} Node.js 앱이 작성되면 개발 환경을 설정하고 {{site.data.keyword.Bluemix_notm}} 모바일 서비스 SDK를 시작할 수 있습니다. SDK를 사용하면 단순 API 호출로 사용자의 클라우드 앱에 바인드되는 서비스에 액세스할 수 있습니다.
  
2. 서버측 리소스를 보호하십시오. 

   모바일 사용 가능 OAuth 보안을 사용하여 Node.js 또는 Liberty for Java&trade; 런타임에서 실행 중인 모바일 백엔드 리소스를 보호하십시오. 자세한 정보는 [리소스 보호](protecting-resources.html)를 참조하십시오.
기본 모바일 백엔드 애플리케이션에 대해 자세히 보려면, [bms-hellotodo-strongloop](https://github.com/ibm-bluemix-mobile-services/bms-hellotodo-strongloop) 샘플 애플리케이션을 참조하십시오. 

3. 코어 {{site.data.keyword.amashort}} 개발 환경을 설정하십시오.
   
	####클라이언트 개발
   {: #client-development}
   
	{{site.data.keyword.amashort}} SDK를 기존 Android, iOS 또는 Cordova 앱에 다음과 같이 추가할 수 있습니다.
   * Android: ([Android SDK 설정](getting-started-android.html))([샘플](https://github.com/ibm-bluemix-mobile-services/bms-samples-android-helloauthentication))
  
   * iOS(Swift SDK): ([iOS Swift SDK 설정](getting-started-ios-swift-sdk.html))
      ([샘플](https://github.com/ibm-bluemix-mobile-services/bms-samples-swift-helloauthentication))
  
   * iOS(Objective-C SDK): ([iOS Object-C SDK 설정](getting-started-ios.html))([샘플](https://github.com/ibm-bluemix-mobile-services/bms-samples-ios-helloauthentication))

   * Cordova: ([Cordova 플러그인 설정](getting-started-cordova.html))([샘플](https://github.com/ibm-bluemix-mobile-services/bms-samples-cordova-helloauthentication))
   
   **참고:** Objective-C SDK는 그대로 완벽하게 지원되며 여전히 {{site.data.keyword.amashort}}에 대한 기본 SDK로 간주되지만, 새로운 Swift SDK를 위해 올해 말에 중단될 계획입니다. 애플리케이션을 작성할 때 Swift SDK를 사용하는 것이 좋습니다([iOS Swift SDK 설정](getting-started-ios-swift-sdk.html) 참조).

	####웹 개발
   {: #web-development}

   {{site.data.keyword.amashort}} 서비스는 웹 애플리케이션을 보호할 수 있으며 특수 SDK는 필요하지 않습니다. {{site.data.keyword.amashort}} 서비스에서 제공하는 보호 뿐만 아니라 다양한 ID 제공자를 활용할 수 있습니다. {{site.data.keyword.amashort}} 통합을 통해 웹 애플리케이션은 구현하는 기술과 관계없이 OAuth2 프로토콜을 이용할 수 있습니다. 다양한 ID 제공자를 사용하여 {{site.data.keyword.amashort}} 서비스에 액세스하도록 웹 애플리케이션을 설정하는 데 대한 정보는 다음을 참조하십시오. 

    * [웹 애플리케이션에서 Facebook 인증 사용](facebook-auth-web.html)
              
    * [웹 애플리케이션에서 Google 인증 사용](google-auth-web.html)
              
    * [웹 애플리케이션에서 사용자 정의 인증 사용](custom-auth-web.html)
              
4. **선택사항:** 애플리케이션의 ID 제공자를 구성하십시오. 애플리케이션당 하나의 ID 제공자를 구성할 수 있습니다. ID 제공자를 구성하면 모바일 앱 사용자가 기존 Facebook 또는 Google+ 계정으로 로그인할 수 있습니다. 또는 사용자 정의 인증을 작성하여 사용자의 로그인 방법을 정의할 수 있습니다.
   * [Facebook 신임 정보로 사용자 인증](facebook-auth-overview.html)
   * [Google 신임 정보로 사용자 인증](google-auth-overview.html)
   * [사용자 정의 ID 제공자로 사용자 인증](custom-auth.html)

5. 앱 모니터링 및 로깅을 구성하십시오. 

    자세한 정보는 [앱 모니터링](app-monitoring.html)을 참조하십시오. 

# 관련 링크
{: #rellinks}

## 튜토리얼 및 샘플
{: #samples}
* [android-helloauthentication 샘플](https://github.com/ibm-bluemix-mobile-services/bms-samples-android-helloauthentication){: new_window}
* [ios-helloauthentication 샘플(Swift SDK)](https://github.com/ibm-bluemix-mobile-services/bms-samples-swift-helloauthentication){: new_window}
* [ios-helloauthentication 샘플(Objective-C SDK)](https://github.com/ibm-bluemix-mobile-services/bms-samples-ios-helloauthentication){: new_window}

## SDK
{: #sdk}
* [코어 SDK(Android)](https://github.com/ibm-bluemix-mobile-services/bms-clientsdk-android-core){: new_window}
* [코어 SDK(Cordova 플러그인)](https://github.com/ibm-bluemix-mobile-services/bms-clientsdk-cordova-plugin-core){: new_window}
* [코어 SDK(iOS - Swift)](https://github.com/ibm-bluemix-mobile-services/bms-clientsdk-swift-core){: new_window}
* [코어 SDK(iOS - Objective-C - 더 이상 사용되지 않음)](https://hub.jazz.net/git/bluemixmobilesdk/imf-ios-sdk/archive?revstr=master){: new_window}
* [사용자 정의 인증 - 단순 샘플](https://github.com/ibm-bluemix-mobile-services/bms-mca-custom-identity-provider-sample){: new_window}
* [사용자 정의 인증 - 고급 샘플](https://github.com/ibm-bluemix-mobile-services/bms-mca-custom-identity-provider-with-user-management){: new_window}

## API 참조
{: api}
* [Android](https://console.{DomainName}/docs/api/content/api/mobilefirst/android/core-api-doc/overview-summary.html){: new_window}
* [iOS(Objective-C SDK) - 더 이상 사용되지 않음](https://console.{DomainName}/docs/api/content/api/mobilefirst/ios/IMFCore_api-doc/html/index.html){: new_window}


## 관련 링크
{: #general}
* [개요](overview.html){: new_window}
