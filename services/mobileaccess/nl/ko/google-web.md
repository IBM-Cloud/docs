---

copyright:
  year: 2016, 2017
lastupdated: "2017-04-06"

---

**중요: {{site.data.keyword.amafull}} 서비스는 {{site.data.keyword.appid_full}} 서비스로 대체되었습니다. **

# 웹 앱에서 Google 인증 사용
{: #google-auth-web}

웹 앱에서 사용자를 인증하려면 Google 로그인을 사용하십시오.


## 시작하기 전에
{: #before-you-begin}

다음이 있어야 합니다.
* 웹 앱.
* {{site.data.keyword.amashort}} 서비스를 통해 보호하는 {{site.data.keyword.Bluemix_notm}} 애플리케이션의 인스턴스입니다. {{site.data.keyword.Bluemix_notm}} 백엔드 작성 방법에 대한 자세한 정보는 [시작하기](index.html)를 참조하십시오.  

## 웹 사이트에 맞게 Google 애플리케이션 구성
ID 제공자로 Google을 사용하기 시작하려면 [Google 개발자 콘솔](https://console.developers.google.com)에서 프로젝트를 작성하십시오. 프로젝트 작성의 일부로 Google 클라이언트 ID 및 본인확인정보를 확보합니다. Google 클라이언트 ID 및 본인확인정보는 Google 인증에서 사용하는 애플리케이션의 고유한 ID이며, {{site.data.keyword.Bluemix_notm}} 애플리케이션 설정에 필요합니다.

1. Google+ API를 사용하여 프로젝트를 작성하십시오.
1. **OAuth**를 사용하여 신임 정보를 작성하십시오. 신임 정보를 작성하려면 다음을 수행해야 합니다.
    * **웹 애플리케이션** 애플리케이션 유형을 선택하십시오.
    * 다음과 같이 **권한 부여된 경로 재지정 URI** 값을 제공하십시오.

     https://imf-newauthserver.bluemix.net/oauth/{bluemix_app_guid}/callback
1. 신임 정보 작성을 완료하고 Google 클라이언트 ID 및 본인확인정보를 기록해 두십시오.


## Google 인증을 위한 Mobile Client Access 구성
Google 애플리케이션 ID와 본인확인정보가 있으면 {{site.data.keyword.amashort}} 대시보드에서 Google 인증을 사용할 수 있습니다.

1. {{site.data.keyword.Bluemix_notm}} 대시보드에서 앱을 여십시오. 
1. {{site.data.keyword.amashort}} 타일을 클릭하십시오. {{site.data.keyword.amashort}} 대시보드가 로드됩니다. 
1. Google 타일을 클릭하십시오.
1. Google 클라이언트 ID 및 본인확인정보를 입력하고 저장하십시오.


## Google 웹 인증을 위한 Mobile Client Access 사용
권한 부여 프로세스를 시작하려면 다음을 수행하십시오. 

1. 웹 앱에서 권한 서버의 다음 엔드포인트로 경로를 재지정하십시오.  
  https://imf-newauthserver.bluemix.net/oauth/v2/authorization

  다음 조회 매개변수를 사용합니다. 
	```
   response_type='authorization_code'
   client_id= <bluemix_app_guid>
   redirect_uri= <uri which you want to return to after getting a grant code>
   scope= ‘openid’
   state= <state>
	```

  `state` 매개변수를 현재 사용 중이지 않으므로 빈 상태로 둘 수 있습니다. 

  `redirect_uri` 매개변수 uri는 Google로 인증하는 데 성공하거나 실패한 후 재지정되는 경로입니다.
  경로를 재지정한 후 리턴되는 응답에는 요청 조회 매개변수의 권한 코드가 포함되어 있습니다.
1. 권한 서버 토큰 엔드포인트에 대한 `POST` 요청을 수행하십시오.

 https://imf-newauthserver.bluemix.net/oauth/v2/token


  다음 조회 매개변수를 사용합니다. 

	```
  	grant_type=’authorization_code’
    client_id= < bluemix_app_guid >
    redirect_uri= <redirect_uri >
    code= <authorization code>
	```
  `redirect_uri` 매개변수는 1단계의 `redirect_uri`와 일치해야 하며 `<authorization code>` 값은 응답에서 받습니다.
  권한 부여 코드는 최대 10분 동안 유효하므로 이 `POST` 요청을 10분 내에 보내도록 하십시오.

`POST` 응답 본문에 base64로 인코딩된 `access_token` 및 `id_token`이 포함되어야 합니다.

## 인증 테스트

이제 보호 리소스 요청을 시작할 수 있습니다.
보호 리소스의 모든 요청은 권한 요청 헤더 필드에 있는 액세스 토큰을 포함해야 합니다.
