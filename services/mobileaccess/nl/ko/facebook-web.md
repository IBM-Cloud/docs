---

copyright:
  year: 2016, 2017
lastupdated: "2017-01-08"

---

# 웹 앱에서 Facebook 인증 사용
{: #facebook_web}

Facebook을 사용하여 웹 앱에서 사용자를 인증하십시오.

## 시작하기 전에
{: #facebook-auth-android-before}
다음이 있어야 합니다.
* 웹 앱.  
* {{site.data.keyword.amashort}} 서비스를 통해 보호하는 {{site.data.keyword.Bluemix_notm}} 애플리케이션의 인스턴스입니다. {{site.data.keyword.Bluemix_notm}} 백엔드 작성 방법에 대한 자세한 정보는 [시작하기](index.html)를 참조하십시오. 
* Facebook 애플리케이션 ID 및 앱 본인확인정보. 자세한 정보는 [Facebook 개발자 포털에서 Facebook 애플리케이션 ID 얻기](https://console.{DomainName}/docs/services/mobileaccess/facebook-auth-overview.html#facebook-appID)를 참조하십시오. 


## 웹 사이트에 맞게 Facebook 애플리케이션 구성
웹 사이트의 ID 제공자로 Facebook을 사용하려면 Facebook 애플리케이션에서 웹 사이트 플랫폼을 추가하여 구성해야 합니다.

1. Facebook 개발자 포털에서 Facebook 애플리케이션을 여십시오. 
1. 앱의 애플리케이션 ID 및 앱 본인확인정보를 기록해 두십시오. Facebook 인증용 웹 프로젝트를 구성할 때 해당 값이 필요합니다.
1. **설정** 페이지에서 **플랫폼 추가**를 클릭하고 **웹 사이트**를 선택하십시오.
1. 변경사항을 저장하십시오.
1. 왼쪽 표시줄에서 **Facebook 로그인**을 클릭하십시오.
1. **올바른 OAuth 경로 재지정 URI** 상자에서 권한 서버 콜백 엔드포인트를 입력하십시오. https://imf-newauthserver.bluemix.net/oauth/{bluemix_app_guid}/callback. 변경사항을 저장하십시오.




# Facebook 인증용 {{site.data.keyword.amashort}} 구성
Facebook 애플리케이션 ID 및 앱 본인확인정보가 있으며 Facebook 애플리케이션에서 웹 클라이언트에 서비스를 제공하도록 구성된 경우 {{site.data.keyword.Bluemix_notm}} 대시보드에서 Facebook 인증을 사용할 수 있습니다.

1. {{site.data.keyword.Bluemix_notm}} 대시보드에서 앱을 여십시오. 
1. {{site.data.keyword.amashort}} 타일을 클릭하십시오. {{site.data.keyword.amashort}} 대시보드가 로드됩니다. 
1. Facebook 타일을 클릭하십시오.
1. Facebook 애플리케이션 ID 및 앱 본인확인정보를 입력하고 저장하십시오.




## Facebook 웹 인증을 위해 모바일 클라이언트 액세스 사용

권한 부여 프로세스를 시작하려면 다음을 수행하십시오. 

1. 웹 앱에서 권한 서버의 다음 엔드포인트로 경로를 재지정하십시오. https://imf-newauthserver.bluemix.net/oauth/v2/authorization.

1. 다음 조회 매개변수를 추가하십시오.
   ```
    response_type='authorization_code'
    client_id= <bluemix_app_guid>
    redirect_uri= <권한 코드를 받은 후 경로를 재지정할 uri>
    scope= 'openid'
    state= <state>
    ```


  `state` 매개변수를 현재 사용 중이지 않으므로 빈 상태로 둘 수 있습니다.
 `redirect_uri` 매개변수는 Facebook으로 인증하는 데 성공하거나 실패한 후 경로를 재지정하는 데 사용하는 uri입니다.

1. 권한 엔드포인트로 경로 재지정한 후에는 Facebook에서 로그인 양식을       
   받게 됩니다. `redirect_uri`로 경로를 재지정할 사용자 이름 및 비밀번호를 입력하십시오.
   경로를 재지정한 후 리턴되는 응답에는 요청 조회 매개변수의 권한 코드가 포함되어 있습니다.

1. 권한 서버 토큰 엔드포인트에 대한 `POST` 요청을 수행하십시오.

  https://imf-newauthserver.bluemix.net/oauth/v2/token

  다음 조회 매개변수를 사용합니다. 
  ```
  grant_type='authorization_code'
  client_id= <bluemix_app_guid>
  code= <authorization code>
  ```
`redirect_uri` 매개변수는 2단계의 `redirect_uri`와 일치해야 합니다.
`code` 값은 3단계 끝의 응답에서 받는 권한 코드입니다.
권한 코드는 최대 10분 동안 유효하므로 이 `POST` 요청을 10분 내에 보내도록 하십시오.

  `POST` 응답 본문에 base64로 인코딩된 `access_token` 및 `id_token`이 포함되어야 합니다.

## 인증 테스트
이제 보호 리소스 요청을 시작할 수 있습니다.
보호 리소스의 모든 요청은 권한 요청 헤더 필드에 있는 `access_token`을 포함해야 합니다.
