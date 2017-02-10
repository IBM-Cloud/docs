---

copyright:
 years: 2015, 2017

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen:.screen}
{:codeblock:.codeblock}

# 모바일 디바이스의 알림 사용
{: #c_enable_push-notifications}
마지막 업데이트 날짜: 2017년 1월 18일
{: .last-updated}

[알림 제공자의 신임 정보 구성](t__main_push_config_provider.html)을 수행했는지 확인하십시오.

이 섹션에서는 모바일, 웹 브라우저 애플리케이션과 같은 클라이언트 애플리케이션과 Chrome 앱 및 확장 프로그램에서 푸시 알림을 수신하도록 설정하는 방법, 기본 알림을 작성하고 SDK 또는 플러그인을 가져와서 초기화하는 방법, 푸시 알림을 수신하기 위해 디바이스 또는 브라우저를 등록하는 방법에 대해 설명합니다. [REST API](t_restapi.html)를 사용하여 모바일 및 웹 브라우저 애플리케이션이 푸시 알림을 수신하도록 설정할 수도 있습니다.

**참고**: 디바이스, 브라우저, Chrome 앱 및 확장 프로그램 등록의 경우 {{site.data.keyword.mobilepushshort}} 서비스는 알림 제공자(Apple의 경우 APNs 또는 Google의 경우 FCM)가 발행한 토큰에 대한
고유 참조를 유지보수합니다. 몇 가지 이유로 {{site.data.keyword.mobilepushshort}} 서비스 알림 제공자가 토큰을 무효화할 수 있습니다.  

예를 들어, 디바이스에서 앱을 설치 제거하는 경우입니다. 이와 같은 시나리오에서 디바이스가 무효화되는 제공자 응답을 기반으로 알림을 전달하려고 하면 {{site.data.keyword.mobilepushshort}} 서비스가 디바이스 또는 웹 브라우저 등록을 제거합니다. 그런 다음 이러한 무효화된 디바이스에 알림을 전송하려는 시도를 제한합니다. 
