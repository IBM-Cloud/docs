---

copyright:
years: 2015, 2017

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen:.screen}
{:codeblock:.codeblock}

# 웹 브라우저에 기본 알림 전송
{: #web_notifications}
마지막 업데이트 날짜: 2017년 1월 11일
{: .last-updated}

애플리케이션을 개발한 후에는 푸시 알림을 전송할 수 있습니다.  

1. **알림 전송**을 선택하고 **받는 사람** 옵션으로 **웹 알림**을 선택하여 메시지를 작성하십시오.  
2. **메시지** 필드에 전달할 메시지를 입력하십시오.
3. 다음과 같은 선택적 설정을 제공하도록 선택할 수 있습니다.
  - **알림 제목**: 메시지 경보 표제로 표시할 텍스트입니다.
  - **알림 아이콘 URL**: 메시지를 앱 알림 아이콘과 함께 전달해야 하는 경우 필드에서 아이콘에 대한 링크를 제공하십시오.
  - **유효 기간**: 서버에 메시지 유효 기간을 알립니다. 
4. Safari 브라우저에 발송된 웹 알림의 경우, 필요한 추가 정보가 있습니다. 
  - **조치**: 조치 단추의 레이블입니다. 
  - **URL 인수**: 이 알림에 사용할 URL 인수입니다. JSON 배열 양식으로 제공해야 합니다.  
 
다음 이미지는 대시보드의 웹 알림 옵션을 표시합니다.

  ![알림 화면](images/DashboardWebpush.jpg)


## 다음 단계
  {: #next_steps_tags}

정상적으로 기본 알림을 설정한 후에는 태그 기반 알림 및 고급 옵션을 구성할 수 있습니다. 

이러한 {{site.data.keyword.mobilepushshort}} 서비스 기능을 앱에 추가하십시오. 태그 기반 알림을 사용하려면 [태그 기반 알림](c_tag_basednotifications.html)을 참조하십시오. 고급 알림 옵션을 사용하려면 [고급 알림](t_advance_badge_sound_payload.html)을 참조하십시오. 



