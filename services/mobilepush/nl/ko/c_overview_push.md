---

copyright:
 years: 2015, 2016

---

# {{site.data.keyword.mobilepushshort}} 정보
{: #overview-push}
마지막 업데이트 날짜: 2016년 8월 16일
{: .last-updated}

IBM {{site.data.keyword.mobilepushshort}}은 iOS 디바이스와 Android 디바이스에 알림을 보내는 데 사용할 수 있는 서비스입니다. 알림은 모든 애플리케이션 사용자와 태그를 사용하는 특정 디바이스 및 사용자 세트를 대상으로 할 수 있습니다. 디바이스, 태그 및 구독을 관리할 수 있습니다. 또한 SDK(software development kit) 및 REST(Representational State Transfer) API(application program interface)를 사용하여 클라이언트 애플리케이션을 추가적으로 개발할 수도 있습니다.  

{{site.data.keyword.mobilepushshort}}을 Bluemix 전용 서비스로 사용할 수도 있습니다. {{site.data.keyword.mobilepushshort}}을 전용 서비스로 사용하는 방법에 대한 정보는 [전용 서비스](../../dedicated/index.html)를 참조하십시오. {{site.data.keyword.mobilepushshort}} 모니터링 탭에는 분석 데이터가 표시되지 않습니다. 

이제 {{site.data.keyword.mobilepushshort}} 서비스에서 OpenWhisk를 사용할 수 있습니다. 자세한 정보는 [OpenWhisk](../../openwhisk/index.html)를 참조하십시오. 


## {{site.data.keyword.mobilepushshort}} 서비스 프로세스
{: #overview_push_process}

모바일 클라이언트는 {{site.data.keyword.mobilepushshort}} 서비스에 등록하고 구독을 신청할 수 있습니다. 시작 시 모바일 애플리케이션이 {{site.data.keyword.mobilepushshort}} 서비스에 등록하고 구독을 신청합니다. 알림은 APN(Apple Push Notification) 서비스 또는 GCM(Google Cloud Messaging)으로 디스패치된 후
등록된 모바일 클라이언트로 전송됩니다.

![푸시 개요](images/overview.jpg)


###모바일 애플리케이션
{: mobile-applications}

시작 시 모바일 애플리케이션이 {{site.data.keyword.mobilepushshort}} 서비스에 등록하고 구독을 신청하여 알림을 받습니다. 

###백엔드 애플리케이션
{: backend-applications}

백엔드 애플리케이션은 사내 구축 환경 또는 퍼블릭 클라우드에 있습니다. 백엔드 애플리케이션은 {{site.data.keyword.mobilepushshort}} 서비스를 사용하여 컨텍스트 알림을 모바일 사용자에게 보냅니다. 푸시 알림을 보내기 위해 백엔드 애플리케이션에서 모바일 디바이스와 사용자 정보를 유지보수하고 관리할 필요는 없습니다. 대신 백엔드 애플리케이션에서 {{site.data.keyword.mobilepushshort}} 서비스를 사용할 수 있습니다. 

###앱 백엔드 소유자
{: app-backend-owner}

앱 백엔드 소유자는 {{site.data.keyword.mobilepushshort}} 서비스의 인스턴스를 번들로 제공하는 모바일 백엔드 애플리케이션을 작성합니다. 또한 앱 백엔드 소유자는 {{site.data.keyword.mobilepushshort}}의 대상인 모바일 애플리케이션과 함께 서비스를 사용하는 백엔드 애플리케이션에 적합하도록 {{site.data.keyword.mobilepushshort}} 서비스를 구성하고 설정합니다. 

###{{site.data.keyword.mobilepushshort}} 서비스
{: push-notification-service}

{{site.data.keyword.mobilepushshort}} 서비스는 알림을 받도록 등록한 디바이스와 관련된 모든 정보를 관리합니다. 이 서비스는 이기종 모바일 플랫폼에 알림을 보내는 기술 세부사항을 애플리케이션에 적용할 수 있도록 알려주고 이 모든 사항을 내부에서 처리합니다. 

###게이트웨이
{: gateways}

모바일 디바이스 플랫폼별 클라우드 서비스(예: GCM(Google Cloud Messaging) 또는 APNs(Apple Push Notification Service))에서는 {{site.data.keyword.mobilepushshort}} 서비스를 사용하여 모바일 애플리케이션에 알림을 디스패치합니다. 

###푸시 보안
{: push-security}

{{site.data.keyword.mobilepushshort}} API는 i) appSecret ii) clientSecret이라는 두 가지 유형의 시크릿으로 보호됩니다. 'appSecret'은 설정을 구성하는 API 구성, {{site.data.keyword.mobilepushshort}}을 보내는 API와 같이 일반적으로 백엔드 애플리케이션에서 호출하는 API를 보호합니다. 'clientSecret'은 일반적으로 모바일 클라이언트 애플리케이션에서 호출하는 API를 보호합니다. 현재 이 'clientSecret'이 필요한 연관된 UserId가 있는 디바이스의 등록과 관련된 API는 하나뿐입니다. 모바일 클라이언트에서 호출된 기타 모든 API에는 clientSecret이 필요하지 않습니다. 'appSecret'과 'clientSecret'은 {{site.data.keyword.mobilepushshort}} 서비스와 애플리케이션을 바인드할 때 모든 서비스 인스턴스에 할당됩니다. 시크릿을 전달하는 방법과 시크릿을 전달할 API에 대한 자세한 정보는 ReST API 문서를 참조하십시오. 

## {{site.data.keyword.mobilepushshort}} 유형
{: #overview-push-types}

###브로드캐스트
{: broadcast}

모바일 애플리케이션이 {{site.data.keyword.mobilepushshort}} 서비스에 등록되면 브로드캐스트를 수신할 수 있습니다. 브로드캐스트 알림은 {{site.data.keyword.mobilepushshort}} 서비스를 사용할 수 있도록 설치되고 구성된 애플리케이션이 있는 모든 디바이스를 대상으로 보내는 메시지입니다. 브로드캐스트 알림은 {{site.data.keyword.mobilepushshort}}이 사용으로 설정된 애플리케이션에서 기본적으로 사용됩니다. {{site.data.keyword.mobilepushshort}} 서비스가 사용 가능하도록 설정된 애플리케이션에는 Push.ALL 태그에 대한 구독이 사전 정의되어 있으며 서버에서 이 태그를 사용하여 알림 메시지를 모든 디바이스에 브로드캐스트합니다. REST Push API를 사용하는 브로드캐스트 알림을 전송하려면 메시지 리소스에 게시할 때 "대상"은 빈 JSON 파일이어야 합니다. 

###태그 기반 알림
{: tag-based-notifications}

태그 알림은 특정 태그를 구독하는 모든 디바이스를 대상으로 하는 메시지입니다. 태그 기반 알림을 사용하면 제목 영역 또는 주제를 기반으로 알림을 구분할 수 있습니다. 알림 수신인은 관심있는 제목 또는 주제에 대한 알림일 경우에만 알림을 수신하도록 선택할 수 있습니다. 따라서 태그 기반 알림은 수신인을 구분할 수 있는 수단을 제공합니다. 이 기능을 사용하면 태그를 정의한 다음 태그별로 메시지를 전송 및 수신할 수 있는 기능을 사용할 수 있습니다. 메시지는 태그에 구독된 디바이스만 대상으로 합니다. 먼저 애플리케이션의 태그를 작성하고 태그 구독을 설정한 후 태그 기반 알림을 시작해야 합니다. REST API를 사용하는 태그 기반 알림을 전송하려면 메시지 자원에 게시할 때 "tagNames"가 제공되는지 확인하십시오. 

###유니캐스트 알림
{: unicast-notifications}

유니캐스트 알림은 특정 디바이스 또는 사용자를 대상으로 하는 메시지입니다. 디바이스를 대상으로 하는 유니캐스트 알림에는 추가 설정이 필요하지 않으며 애플리케이션에서 {{site.data.keyword.mobilepushshort}}을 사용하는 경우 기본적으로 유니캐스트 알림이 사용됩니다. 

그러나 사용자가 대상인 유니캐스트 알림에는 다음 설정이 필요합니다. 

- 푸시 알림을 사용하도록 모바일 디바이스를 등록할 때 사용자 ID와 디바이스를 연관시켜야 합니다.   

- 백엔드 애플리케이션을 {{site.data.keyword.mobilepushshort}} 서비스에 바인드할 때 할당된 'clientSecret'을 전달하여 해당 사용자 ID 등록을 인증해야 합니다.  

일반적으로 모바일 애플리케이션은 제일 먼저 인증 주기를 실행하며 여기서 모바일 앱 사용자가 인증 서비스([Mobile Client Access 시작하기](https://console.ng.bluemix.net/docs/services/mobileaccess/index.html))에 대해 인증됩니다. 인증에 성공하면 인증된 사용자 ID가 clientSecret과 함께 푸시 디바이스 등록 API에 전달됩니다. clientSecret이 있으면 사용자 ID와 모바일 디바이스 등록의 인증된 연관만 적용됩니다.
REST API를 통해 유니캐스트 알림을 전송하려면 메시지 자원에 게시할 때 deviceIds 또는 userIds가 제공되는지 확인하십시오. 

###플랫폼 기반 알림
{: platform-based-notifications}

특정 디바이스 플랫폼에 도달하도록 알림의 대상을 설정할 수 있습니다. 예를 들어, 모든 Android 사용자에게만 알림을 전송할 수 있습니다. REST API를 사용하는 플랫폼 기반 알림을 전송하려면 메시지 리소스에 게시할 때 대상 플랫폼이 제공되는지 확인하십시오. 플랫폼을 어레이로 지정하십시오. 지원되는 플랫폼은 다음과 같습니다. 
* A(Apple)
* G(Google)

## {{site.data.keyword.mobilepushshort}} 메시지 크기
{: #push-message-size}

{{site.data.keyword.mobilepushshort}} 메시지 페이로드 크기는 중개자에 따라 다릅니다.  

###iOS
{: ios-message-size}

iOS 8 이상의 경우 허용된 최대 크기는 2KB입니다. Apple 푸시 알림 서비스는 이 한계를 초과하는 알림을 전송하지 않습니다. 

###Android
{: android-message-size}

Android 플랫폼에는 제한사항이 없습니다. 
