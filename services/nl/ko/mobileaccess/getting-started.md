---

copyright:
  years: 2015, 2016

---

# 시작하기
{: #getting-started}
{{site.data.keyword.amashort}}를 시작하려면, {{site.data.keyword.amashort}} 서비스를 기존 {{site.data.keyword.Bluemix}} 애플리케이션에 추가하거나 표준 유형을 사용하여 새 앱을 작성할 수 있습니다.   

## {{site.data.keyword.amashort}} 서비스의 인스턴스 작성
{: #service-instance}

{{site.data.keyword.Bluemix}} 카탈로그에서 {{site.data.keyword.amashort}} 서비스의 새 인스턴스를 작성할 수 있습니다. 새 모바일 백엔드를 작성하는 데 표준 유형을 사용하지 않는 경우 기존 백엔드에 있는 서버 SDK를 구성해야 합니다. 


  * **새 앱**: 다음 섹션의 지시사항은 모바일 백엔드를 작성하고 {{site.data.keyword.amashort}} 서버 SDK를 사용하여 보호하는 새 앱의 작성 방법에 대해 설명합니다. **MobileFirst Services Starter** 표준 유형을 클릭하여 {{site.data.keyword.amashort}} 서비스로 새 애플리케이션을 작성하십시오. 
  * **기존 앱**: {{site.data.keyword.amashort}} 아이콘을 클릭하고 기존 애플리케이션에 바인드되는 새 서비스 인스턴스를 작성하십시오. 기존 앱에서 서버 SDK를 구성하려면 [클라우드 자원 보호](protecting-resources.html)를 참조하십시오. 


## MobileFirst Services Starter 표준 유형을 사용하여 모바일 백엔드 작성
{: #create-backend}
MobileFirst Services Starter를 사용하는 경우 사용자 정의 백엔드 로직을 구현하기 위해 IBM {{site.data.keyword.Bluemix_notm}}에서 실행하는 Node.js 런타임의 인스턴스를 가져옵니다. 보안, 데이터, 푸시 및 모니터링 기능을 제공하는 코어 모바일 서비스 세트가 해당 Node.js 앱으로 바인드됩니다. {{site.data.keyword.Bluemix_notm}} Node.js 앱이 작성되면 개발 환경을 설정하고 {{site.data.keyword.Bluemix_notm}} 모바일 서비스 SDK를 시작할 수 있습니다. SDK를 사용하면 단순 API 호출로 사용자의 클라우드 앱에 바인드되는 서비스에
액세스할 수 있습니다.

1. {{site.data.keyword.Bluemix_notm}} 카탈로그에서 **표준 유형** 섹션으로 이동하고 **MobileFirst Services Starter**를 클릭하십시오. 
1. 영역, 이름, 호스트 및 서비스 플랜을 포함하여 모바일 백엔드에 대한 정보를 추가하십시오. 
1. **작성**을 클릭하십시오. 



## 다음 단계
{: #next-steps}
표준 유형으로 작성된 Node.js 애플리케이션의 여러 엔드포인트는 {{site.data.keyword.amashort}}로 보호됩니다. 기본 모바일 백엔드 애플리케이션에 대해 자세히 알아보려면, [bms-hellotodo-strongloop](https://github.com/ibm-bluemix-mobile-services/bms-hellotodo-strongloop)를 참조하십시오. 

{{site.data.keyword.amashort}} SDK를 사용하기 위해 모바일 앱을 설정할 수 있습니다. SDK를 설정하면 앱에서 인증 및 모니터링 설정을 시작할 수 있습니다. 사용자 모바일 개발 플랫폼에 대한 지시사항을 따르십시오. 

* [Android](getting-started-android.html)
* [iOS(Swift SDK)](getting-started-ios.html)
* [iOS(Objective-C SDK)](getting-started-ios.html)
* [Cordova](getting-started-cordova.html)
