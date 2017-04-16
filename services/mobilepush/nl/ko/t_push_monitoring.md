---

copyright:
 years: 2015, 2017

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen:.screen}
{:codeblock:.codeblock}

# 푸시 알림 모니터링 
{: #monitor-notifications}
마지막 업데이트 날짜: 2017년 1월 16일
{: .last-updated}


IBM {{site.data.keyword.mobilepushshort}} 서비스가 확장되어 이제 사용자 데이터에서 그래프를 생성하여 푸시 성능을 모니터할 수 있는 기능을 제공합니다. 유틸리티를 사용하여 일별, 주별 또는 월별 기준으로 전송된 푸시 알림을 모두 나열하거나 등록된 디바이스를 모두 나열하여 정보를 분석할 수 있습니다. 

전송된 모든 알림에 대한 보고서를 생성하려면 [REST API](https://mobile.{DomainName}/imfpush/){: new_window}에 있는 푸시 메시지 GET 메소드를 사용하십시오.  

![발송된 알림 보고서](images/monitoring_messages.jpg)


등록된 모든 디바이스에 관한 보고서를 생성하려면 [REST API](https://mobile.{DomainName}/imfpush/){: new_window}의 푸시 디바이스 등록 GET 보고서 메소드를 사용하십시오. 

![등록된 디바이스 보고서](images/monitoring_devices.jpg)

Android SDK를 업데이트하여 알림 정보를 모니터하는 방법은 [Android 디바이스에서 푸시 알림 모니터링](c_android_enable.html#android_monitor)을 참조하십시오. 


 
