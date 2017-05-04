---

copyright:
  years: 2016, 2017
lastupdated: "2017-04-06"

---

**중요: {{site.data.keyword.amafull}} 서비스는 {{site.data.keyword.appid_full}} 서비스로 대체되었습니다. **

# 웹 앱 사용자 정의 인증
{: #custom-web}

웹 앱에 사용자 정의 인증 추가

## 시작하기 전에
{: #before-you-begin}

다음이 있어야 합니다.
* 인증 성공 시 사용자 ID를 리턴하는 `/apps/:Guid/<RealmName>/handleChallengeAnswer`
엔드포인트가 있는 웹 앱. 사용자 ID JSON 구조는 다음과 같아야 합니다.

   ```json
  userIdentity: {
  userName: <username>,
  displayName: <displayName>;
 };
```
* {{site.data.keyword.amashort}} 서비스를 통해 보호하는 {{site.data.keyword.Bluemix_notm}} 애플리케이션의 인스턴스입니다. {{site.data.keyword.Bluemix_notm}} 백엔드 작성 방법에 대한 자세한 정보는 [시작하기](index.html)를 참조하십시오.  



## 사용자 정의 인증용 {{site.data.keyword.amashort}} 앱 구성


1. {{site.data.keyword.Bluemix_notm}} 대시보드에서 앱을 여십시오. 
1. {{site.data.keyword.amashort}} 타일을 클릭하십시오. {{site.data.keyword.amashort}}
대시보드가 로드됩니다. 
1. 사용자 정의 타일을 클릭하십시오. 
1. **사용자 정의 영역**, **사용자 정의 ID 제공자 URL** 및 **redirect_uri**를 입력하십시오. 저장을 클릭하십시오.

## 사용자 정의 웹 인증을 위해 {{site.data.keyword.amashort}} 사용

권한 부여 프로세스를 시작하려면 다음을 수행하십시오. 

1. 웹 앱에서 권한 서버의 다음 엔드포인트로
경로를 재지정하십시오.

    https://imf-newauthserver.bluemix.net/oauth/v2/authorization

  다음 조회 매개변수를 사용합니다. 
   ```
   response_type=’authorization_code’
   client_id= <bluemix\_app\_guid>
   redirect_uri= <권한 코드를 받은 후 경로를 재지정할 uri>
   scope= ‘openid’
   state= <state>
   ```

    `state` 매개변수는 현재 사용 중이지 않으므로 비워 둘 수 없습니다.

    사용자 정의 ID 제공자 인증에 성공 또는 실패한 후 `redirect_uri` 매개변수를 통해 경로 재지정을 판별합니다. 

1. 권한 엔드포인트로 경로를 재지정한 후 로그인 양식을
가져옵니다. ID 제공자에 대한 인증을 시작하고 `redirect_uri`로 경로가
재지정되도록 사용자 이름 및 비밀번호를 입력하십시오.
인증에 성공한 후 리턴된 응답에는 요청 조회 매개변수의 권한 코드가 포함되어 있습니다. 

4. 권한 서버 토큰 엔드포인트에 대한 `POST` 요청을 수행하십시오.

 https://imf-newauthserver.bluemix.net/*oauth/v2/token

 다음 조회 매개변수를 사용합니다. 
 ```
 grant_type = 'authorization_code'
 client_id = <bluemix_app_guid>
 redirect_uri = <redirect_uri>
 code = <authorization code>
 ```
  `redirect_uri` 매개변수는 1단계의 `redirect_uri`와 일치해야 합니다. 권한 코드는 2단계의 요청을 통해 리턴됩니다.

  권한 부여 코드는 최대 10분 동안 유효하므로 이 `POST` 요청을 10분 내에 보내도록 하십시오.

`POST` 응답 본문에 base64로 인코딩된 *access_token* 및
*id_token*이 포함되어 있습니다. 

## 인증 테스트


이제 보호 리소스 요청을 시작할 수 있습니다.
모든 보호 리소스 요청에는 `access_token`이 포함되어야 합니다.
`the-Authorization-request` 헤더 필드로 액세스 토큰을 보내십시오. 
