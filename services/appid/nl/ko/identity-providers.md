---

copyright:
  years: 2017
lastupdated: "2017-04-17"

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:pre: .pre}

# ID 제공자 구성
{: #setting-up-idp}

사용자에 대한 싱글 사인온 환경을 설정하도록 Facebook, Google 또는 둘 모두를 구성할 수 있습니다. ID 제공자를 사용하여 사용자는 이미 친숙한 신임 정보로 사인인할 수 있습니다.
{:shortdesc}


## Facebook 인증 구성
{: #facebook}

ID 제공자로 Facebook을 사용하도록 {{site.data.keyword.appid_short}} 서비스를 구성하십시오. 

<!--- ### Sequence diagram
{: #facebook-sequence-diagram}--->

### Facebook에서 앱 ID 및 본인확인정보 가져오기
{: #getting-facebook-appid}

모바일 또는 웹 앱에서 ID 제공자로 Facebook을 사용하려면 Facebook 애플리케이션에서 웹 사이트 플랫폼을 추가하고 구성해야 합니다. 

1. <a href="https://developers.facebook.com/docs/apps/register" target="_blank">Facebook for Developers 사이트 <img src="../../icons/launch-glyph.svg" alt="외부 링크 아이콘"></a>의 사용자 계정에 로그인하십시오. 
2. Facebook 앱 ID 및 본인확인정보를 기록해 두십시오. 이러한 값은 서비스 대시보드에서 인증을 위해 웹 프로젝트를 구성하는 데 필요합니다. 
3. 웹 플랫폼을 추가하고 사이트 URL을 입력하십시오.
4. 제품 목록에서 **Facebook 로그인**을 선택하십시오.
5. 올바른 OAuth 경로 재지정 URL 필드에서 권한 서버 콜백 엔드포인트 URL을 입력하십시오. 이후 단계에서 {{site.data.keyword.appid_short_notm}} 서비스를 구성한 후에 이 값을 추가할 수 있습니다. 
6. **변경사항 저장**을 클릭하십시오.

### Facebook 인증용 {{site.data.keyword.appid_short_notm}} 구성
{: #configuring-facebook-appid}

Facebook 앱 ID와 본인확인정보가 있으며 개발자용 Facebook 앱이 웹 클라이언트를 제공하도록 구성되어 있으면 서비스 대시보드에서 Facebook 인증을 편집할 수 있습니다. 

1. 서비스 대시보드의 **관리** 탭에서 **Facebook**을 선택하고 **편집**을 클릭하십시오. 
2. 개발자용 Facebook 웹 사이트에서 확보한 Facebook 앱 ID 및 본인확인정보를 입력하십시오. 
3. **개발자용 Facebook의 경로 재지정 URI** 필드에 있는 URI를 복사하십시오. Facebook 개발자 포털의 **Facebook 로그인** 섹션에서 **올바른 OAuth 경로 재지정 URI** 필드에 URI를 붙여넣기하십시오. 
4. **저장**을 클릭하십시오.
5. 선택사항: 웹 앱에 대한 인증을 구성하려면 웹 애플리케이션 경로 재지정 URL에 경로 재지정 URL을 입력하십시오. 이 값은 개발자가 판별하며 권한 부여 프로세스가 완료된 후에 경로 재지정 URL에 액세스하는 데 사용됩니다. 


## Google 인증 구성
{: #google}

ID 제공자로 Google을 사용하도록 {{site.data.keyword.appid_short_notm}} 서비스를 구성하십시오. 

<!--- ### Sequence diagram
{: #google-sequence-diagram}--->

### Google에서 클라이언트 ID 및 본인확인정보 가져오기
{: #google-client-id}

ID 제공자로 Google을 사용하려면 Google 클라이언트 ID 및 본인확인정보를 확보하고 Google 개발자 콘솔에서 프로젝트를 작성하십시오. 

1. <a href="https://console.developers.google.com/apis/library" target="_blank">Google 개발자 콘솔 <img src="../../icons/launch-glyph.svg" alt="외부 링크 아이콘"></a>에서 Google 애플리케이션을 여십시오. 
2. Google+ API를 추가하십시오.
3. OAuth를 사용하여 신임 정보를 작성하십시오. **애플리케이션 유형** 필드에서 **웹 애플리케이션**을 선택하십시오. **권한 부여된 경로 재지정 URI** 필드에 App ID 경로 재지정 URI를 입력하십시오. 서비스 대시보드의 Google 구성 화면에서 App ID 경로 재지정 권한 URI를 확보할 수 있습니다. 
4. 변경사항을 저장하십시오. Google 클라이언트 ID 및 본인확인정보를 기록해 두십시오.



### Google 인증용 {{site.data.keyword.appid_short_notm}} 구성
{: #google-client-appid}

Google 클라이언트와 본인확인정보가 있으며 Google 개발자 콘솔이 웹 클라이언트를 제공하도록 구성되어 있으면 서비스 대시보드에서 Google 인증을 편집할 수 있습니다. 

1. 서비스 대시보드의 **관리** 탭에서 **Google**을 선택하고 **편집**을 클릭하십시오. 
3. Google 개발자 콘솔에서 확보한 Google 클라이언트 ID 및 본인확인정보를 입력하십시오.
4. **개발자용 Google의 경로 재지정 URI** 필드에 있는 URI를 복사하십시오. Google 개발자 포털의 **웹 애플리케이션용 클라이언트 ID** 섹션에서 **제한사항** 아래의 **권한 부여된 경로 재지정 URI** 필드에 URI를 붙여넣기하십시오. 
5. **저장**을 클릭하십시오.
6. 선택사항: 웹 앱에 대한 인증을 구성하려면 웹 애플리케이션 경로 재지정 URI 필드에 경로 재지정 URI를 입력하십시오. 이 값은 개발자가 판별하며 권한 부여 프로세스 완료 후에 경로 재지정 URI에 액세스하는 데 사용됩니다. 



<!---[## Bring your own OAuth2/OIDC identity provider
{: #oauth2}

### About
{: #oauth2-about}
### Sequence diagram
{: #oauth2-sequence-diagram}
### Configuring AppID for BYOIDP OAuth2 authentication
{: #oauth2-appid} SHAWNA: Is this Interconnect?]--->
