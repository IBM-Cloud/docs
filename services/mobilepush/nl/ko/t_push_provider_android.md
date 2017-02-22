---

copyright:
 years: 2015, 2017

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen:.screen}
{:codeblock:.codeblock}

# FCM의 신임 정보 구성
{: #create-push-enable-gcm}
마지막 업데이트 날짜: 2017년 1월 16일
{: .last-updated}

FCM(Firebase Cloud Messaging)은 Android 디바이스 및 Google Chrome에 푸시 알림을 전달하는 데 사용되는 게이트웨이입니다. FCM은 GCM(Google Cloud Messaging)의 새 버전입니다. 대시보드에서 {{site.data.keyword.mobilepushshort}} 서비스를 설정하려면 FCM 신임 정보를 가져와야 합니다. 새 앱에 FCM 구성을 사용하십시오. 기존 앱은 계속해서 GCM 구성으로 작동합니다. 

##발신인 ID 및 API 키 가져오기
{: #android-senderid-apikey}

API 키는 안전하게 저장되어 {{site.data.keyword.mobilepushshort}} 서비스에서 FCM 서버에 연결하는 데 사용되며 발신인 ID(프로젝트 번호)는 클라이언트 측의 Google Chrome 및 Mozilla Firefox용 Android SDK와 JS SDK에서 사용됩니다.  

FCM을 설정하려면 API 키와 발신인 ID를 생성하고 다음 단계를 완료하십시오. 

1. [Firebase 콘솔 ![외부 링크 아이콘](../../icons/launch-glyph.svg "외부 링크 아이콘")](https://console.firebase.google.com/?pli=1 "외부 링크 아이콘"){: new_window}을 방문하십시오.
2. **새 프로젝트 작성**을 선택하십시오.  
3. 프로젝트 작성 창에서 프로젝트 이름을 입력하고 국가/지역을 선택한 후 **프로젝트 작성**을 클릭하십시오. 
3. 탐색 분할창에서 설정 아이콘을 클릭한 후 **프로젝트 설정**을 선택하십시오. 
4. 클라우드 메시징 탭을 선택하여 서버 API 키와 발신인 ID를 생성하십시오. 

##Android와 Chrome 앱 및 확장 프로그램의 {{site.data.keyword.mobilepushshort}} 서비스 설정
{: #setup-push-android}

**참고:** FCM/GCM API 키와 발신인 ID(프로젝트 번호)가 필요합니다. 

1. Bluemix 대시보드를 연 후 작성한 {{site.data.keyword.mobilepushfull}} 서비스 인스턴스를 클릭하여 대시보드를 여십시오. 푸시 대시보드가 표시됩니다. 바인딩되지 않은 Android용 {{site.data.keyword.mobilepushshort}} 서비스를 설정하려면 바인딩되지 않은 {{site.data.keyword.mobilepushshort}} 서비스 아이콘을 선택하여 {{site.data.keyword.mobilepushshort}} 서비스 대시보드를 여십시오. 

![푸시 대시보드](images/push_unbound.jpg)

2. **푸시 설정** 단추를 클릭하여 Android 애플리케이션과 Google Chrome 앱 및 확장 프로그램의 FCM/GCM 신임 정보를 구성하십시오. 
3. **구성** 페이지에서, Android의 경우 **모바일** 탭으로 이동하여 발신인 ID(GCM 프로젝트 번호)와 API 키를 구성하십시오. Google Chrome 앱 및 확장 프로그램의 경우 **웹** 탭으로 이동하여 발신인 ID(FCM/GCM 프로젝트 번호)와 API 키를 적절히 구성하십시오. 
4. **저장**을 클릭하십시오.
5. 다음 단계. [Android의 알림 사용](c_enable_push.html) 또는 [Google Chrome 앱 및 확장 프로그램의 알림 사용](c_enable_push.html)을 설정하십시오. 


