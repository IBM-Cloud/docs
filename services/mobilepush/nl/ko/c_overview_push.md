---

copyright:
 years: 2015, 2017

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen:.screen}
{:codeblock:.codeblock}

# Push Notification 서비스
{: #overview-push}
마지막 업데이트 날짜: 2017년 3월 31일
{: .last-updated}

IBM {{site.data.keyword.mobilepushshort}}는 디바이스와 플랫폼에 알림을 보내는 데 사용할 수 있는 서비스입니다. 알림은 모든 애플리케이션 사용자와 태그를 사용하는 특정 디바이스 및 사용자 세트를 대상으로 할 수 있습니다. 디바이스, 태그 및 구독을 관리할 수 있습니다.   

다음 옵션을 사용하여 바인드 또는 바인드 해제된 서비스를 작성할 수 있습니다.

- 카탈로그에서 MobileFirst Services Starter 표준 유형을 사용하여 Bluemix 애플리케이션을 작성하여 수행합니다. 그러면 Bluemix 백엔드 애플리케이션에 바인드된 Push Notifications 서비스가 작성됩니다.
- 모바일 카탈로그에서 직접 바인드 해제된 Push Notifications 서비스를 작성하여 수행합니다. 나중에 애플리케이션에 바인드할 수 있습니다. 또는 바인드 해제하는 데 사용하도록 선택할 수도 있습니다. 
- [모바일 대시보드 ![외부 링크 아이콘](../../icons/launch-glyph.svg "외부 링크 아이콘")](https://console.ng.bluemix.net/docs/mobile/services.html){: new_window}을 사용하여 수행합니다. 

{{site.data.keyword.mobilepushshort}} 모니터링 탭에는 분석 데이터가 표시되지 않습니다. 

이제 {{site.data.keyword.mobilepushshort}} 서비스에서 OpenWhisk를 사용할 수 있습니다. 자세한 정보는 [OpenWhisk](/docs/openwhisk/index.html)를 참조하십시오. 


## Push Notification 서비스 프로세스
{: #overview_push_process}

모바일, 웹 브라우저 클라이언트, Google Chrome 앱 및 확장 프로그램은 {{site.data.keyword.mobilepushshort}} 서비스를 구독하고 이 서비스에 등록할 수 있습니다. 시작 시 클라이언트 애플리케이션은 {{site.data.keyword.mobilepushshort}} 서비스에 등록하고 구독을 신청합니다. 알림은 APNs(Apple Push Notification Service) 또는 FCM(Firebase Cloud Messaging)/GCM(Google Cloud Messaging) 서버로 디스패치된 후 등록된 모바일 또는 브라우저 클라이언트에 전송됩니다. 

![푸시 개요](images/overview.jpg)


### 모바일 및 브라우저 애플리케이션
{: #mobile-applications}

시작 시 클라이언트 애플리케이션은 알림을 수신하도록 {{site.data.keyword.mobilepushshort}} 서비스에 등록하고 구독을 신청합니다. 

### 백엔드 애플리케이션
{: #backend-applications}

백엔드 애플리케이션은 온프레미스 또는 퍼블릭 클라우드에 있습니다. 백엔드 애플리케이션은 {{site.data.keyword.mobilepushshort}} 서비스를 사용하여 컨텍스트 알림을 모바일 및 브라우저 애플리케이션 사용자에게 전송합니다. 백엔드 애플리케이션은 푸시 알림을 전송하기 위해 모바일 디바이스, 브라우저 에이전트 및 사용자 정보를 유지보수하고 관리할 필요가 없습니다. 대신 백엔드 애플리케이션에서는 이들을 관리하고 유지보수하는 {{site.data.keyword.mobilepushshort}} 서비스를 사용할 수 있습니다.

### 앱 백엔드 소유자
{: #app-backend-owner}

앱 백엔드 소유자는 {{site.data.keyword.mobilepushshort}} 서비스의 인스턴스를 번들로 제공하는 모바일 백엔드 애플리케이션을 작성합니다. 앱 백엔드 소유자는 또한 {{site.data.keyword.mobilepushshort}}의 대상인 모바일 및 브라우저 애플리케이션과 함께 {{site.data.keyword.mobilepushshort}} 서비스를 사용하는 백엔드 애플리케이션에 적합하도록 이 서비스를 구성하고 설정합니다.

### Push Notification 서비스
{: #push-notification-service}

{{site.data.keyword.mobilepushshort}} 서비스는 알림을 수신하기 위해 등록한 모바일 디바이스 및 웹 브라우저 클라이언트와 관련된 모든 정보를 관리합니다. 이 서비스는 이기종 모바일 및 웹 브라우저 플랫폼에 알림을 보내는 기술 세부사항을 애플리케이션에 적용할 수 있도록 알려주고 이 모든 사항을 내부에서 처리합니다. 

### 게이트웨이
{: #gateways}

IBM {{site.data.keyword.mobilepushshort}} 서비스에서 모바일 애플리케이션과 브라우저 애플리케이션에 알림을 디스패치하는 데 사용하는 플랫폼별 Push Notifications 클라우드 서비스(예: FCM/GCM 또는 APNs(Apple Push Notification Service))입니다. 

### 푸시 보안
{: #push-security}

{{site.data.keyword.mobilepushshort}} API는 다음 두 유형의 시크릿으로 보호됩니다.

- **appSecret**: `appSecret`은 일반적으로 백엔드 애플리케이션에서 호출하는 API를 보호합니다(예: {{site.data.keyword.mobilepushshort}}를 전송하는 API 및 설정을 구성하는 API). 
- **clientSecret**: `clientSecret`은 일반적으로 모바일 클라이언트 애플리케이션에서 호출하는 API를 보호합니다. 오직 하나의 API만 이 `clientSecret`이 필요한 연관된 사용자 ID의 디바이스 등록과 관련되어 있습니다. 모바일 클라이언트에서 호출된 기타 API에서는 `clientSecret`이 필요하지 않습니다.  

`appSecret` 및 `clientSecret`은 애플리케이션을 {{site.data.keyword.mobilepushshort}} 서비스와 바인딩하는 시점에 모든 서비스 인스턴스에 할당됩니다. 시크릿을 전달하는 방법과 전달 대상 API에 대한 정보는 [REST API ![외부 링크 아이콘](../../icons/launch-glyph.svg "외부 링크 아이콘")](https://mobile.{DomainName}/imfpush/) 문서를 참조하십시오. 

**참고**: 이전 애플리케이션에서는 사용자 ID 필드에서 디바이스를 등록하거나 업데이트하는 경우에만 clientSecret을 전달해야 했습니다. 모바일 클라이언트와 브라우저 클라이언트에서 호출한 기타 모든 API에는 clientSecret이 필요하지 않았습니다. 이와 같은 이전 애플리케이션에서 디바이스 등록 또는 호출 업데이트에 선택적으로 clientSecret을 계속 사용할 수 있습니다. 그러나 모든 클라이언트 API 호출에 clientSecret 검사를 적용하는 것이 좋습니다. 기존 애플리케이션에서 이를 적용할 수 있도록 공개된 새 `verifyClientSecret` API가 있습니다. 새 애플리케이션의 경우에는 clientSecret 확인이 모든 클라이언트 API 호출에서 적용되며, 이 작동은 `verfiyClientSecret` API로 변경될 수 없습니다. 

기본적으로 클라이언트 시크릿 확인은 새 앱에서만 적용됩니다. 기존 앱과 새 앱 모두 verifyClientSecret REST API를 사용하여 클라이언트 시크릿 확인을 사용 또는 사용 안함으로 설정할 수 있습니다. applicationId와 deviceId를 아는 사용자에게 디바이스가 노출되지 않도록 클라이언트 시크릿 확인을 적용하는 것이 좋습니다. 

`clientSecret`의 기밀이 유지되며 모바일 앱으로 하드코드화되지 않았음을 확인하십시오. 애플리케이션 런타임 중에 동적으로 `clientSecret`의 가져오기에 사용될 수 있는 다양한 애플리케이션 초기화 패턴이 있습니다. 시퀀스 다이어그램에서 이와 같은 가능한 패턴을 간략히 보여줍니다.
![Enable_Push](images/init_client_secret.jpg) 

## Push Notifications 유형
{: #overview-push-types}

### 브로드캐스트
{: #broadcast}

클라이언트 애플리케이션이 {{site.data.keyword.mobilepushshort}} 서비스에 등록되면 브로드캐스트를 수신할 수 있습니다. 브로드캐스트 알림은 모바일 디바이스, 브라우저에 설치되거나 Chrome 앱 또는 확장 프로그램 인스턴스로 구현되고 {{site.data.keyword.mobilepushshort}} 서비스를 사용할 수 있도록 구성된 애플리케이션의 모든 인스턴스를 대상으로 전송되는 메시지입니다. 브로드캐스트 알림은 {{site.data.keyword.mobilepushshort}}가 사용으로 설정된 애플리케이션에서 기본적으로 사용됩니다. {{site.data.keyword.mobilepushshort}} 서비스가 사용 가능하도록 설정된 애플리케이션에는 Push.ALL 태그에 대한 구독이 사전 정의되어 있으며 서버에서 이 태그를 사용하여 알림 메시지를 모든 디바이스에 브로드캐스트합니다. REST Push API를 사용하는 브로드캐스트 알림을 전송하려면 메시지 리소스에 게시할 때 "대상"은 빈 JSON 파일이어야 합니다. 

### 태그 기반 알림
{: #tag-based-notifications}

태그 알림은 특정 태그를 구독하는 모든 디바이스를 대상으로 하는 메시지입니다. 태그 기반 알림을 사용하면 제목 영역 또는 주제를 기반으로 알림을 구분할 수 있습니다. 알림 수신인은 관심있는 제목 또는 주제에 대한 알림일 경우에만 알림을 수신하도록 선택할 수 있습니다. 따라서 태그 기반 알림은 수신인을 구분할 수 있는 수단을 제공합니다. 이 기능을 사용하면 태그를 정의한 다음 태그별로 메시지를 전송 및 수신할 수 있는 기능을 사용할 수 있습니다. 태그를 구독하는 클라이언트 애플리케이션 인스턴스(모바일, 브라우저에 있거나 앱 또는 확장 프로그램으로서의 인스턴스)만 메시지의 대상입니다. 먼저 애플리케이션의 태그를 작성하고 태그 구독을 설정한 후 태그 기반 알림을 시작해야 합니다. REST API를 사용하는 태그 기반 알림을 전송하려면 메시지 자원에 게시할 때 "tagNames"가 제공되는지 확인하십시오. 

### 유니캐스트 알림
{: #unicast-notifications}

유니캐스트 알림은 특정 디바이스 또는 사용자를 대상으로 하는 메시지입니다. 디바이스를 대상으로 하는 유니캐스트 알림에는 추가 설정이 필요하지 않으며 애플리케이션에서 {{site.data.keyword.mobilepushshort}}를 사용하는 경우 기본적으로 유니캐스트 알림이 사용됩니다. 

그러나 사용자를 대상으로 하는 유니캐스트 알림에서는 {{site.data.keyword.mobilepushshort}}를 수신하도록 클라이언트 모바일 디바이스나 웹 브라우저 또는 Chrome 앱 및 확장 프로그램을 등록할 때 사용자 ID와 디바이스를 연관시켜야 합니다.    

일반적으로 클라이언트 애플리케이션은 제일 먼저 인증 주기를 실행하며 여기서 모바일 앱 사용자가 인증 서비스(예: [Mobile Client Access](docs/services/mobileaccess/index.html))에 대해 인증됩니다. 인증에 성공하면 인증된 사용자 ID가 푸시 디바이스 등록 API에 전달됩니다.
REST API를 통해 유니캐스트 알림을 전송하려면 메시지 자원에 게시할 때 deviceIds 또는 userIds가 제공되는지 확인하십시오. 

### 플랫폼 기반 알림
{: #platform-based-notifications}

특정 디바이스 플랫폼에 도달하도록 알림의 대상을 설정할 수 있습니다. 예를 들어, 모든 Android 사용자 또는 Google Chrome 사용자에게만 알림을 전송할 수 있습니다. REST API를 사용하는 플랫폼 기반 알림을 전송하려면 메시지 리소스에 게시할 때 대상 플랫폼이 제공되는지 확인하십시오. 플랫폼을 어레이로 지정하십시오. 지원되는 플랫폼은 다음과 같습니다. 
* A(Apple)
* G(Google)
* WEB_CHROME(Google Chrome 브라우저 웹 푸시)
* WEB_FIREFOX(Mozilla Firefox 브라우저 웹 푸시)
* WEB_SAFARI(Safari 브라우저 웹 푸시)
* APPEXT_CHROME(Google Chrome 앱 및 확장 프로그램)

## Push Notification 메시지 크기
{: #push-message-size}

{{site.data.keyword.mobilepushshort}} 메시지 페이로드 크기는 게이트웨이(FCM/GCM, APNs)와 클라이언트 플랫폼의 제한조건에 따라 다릅니다.  

### iOS 및 Safari
{: #ios-message-size}

iOS 8 이상의 경우 허용된 최대 크기는 2KB입니다. Apple Push Notification 서비스는 이 한계를 초과하는 알림을 전송하지 않습니다. 

### Android, Firefox 브라우저, Chrome 브라우저, Chrome 앱 및 확장 프로그램
{: #android-message-size}

허용되는 최대 메시지 페이로드 크기는 4KB입니다.  
