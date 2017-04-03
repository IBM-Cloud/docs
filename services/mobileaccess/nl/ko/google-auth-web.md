---

copyright:
  year: 2016, 2017
lastupdated: "2017-03-15"

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}

{{site.data.keyword.amafull}} 서비스가 {{site.data.keyword.appid_full}} 서비스로 대체되었습니다.

# 웹 애플리케이션에서 Google 인증 사용
{: #google-auth-web}

Google 로그인을 사용하여 웹 애플리케이션의 사용자를 인증하십시오.  {{site.data.keyword.amafull}} 보안 기능을 추가하십시오.


## 시작하기 전에
{: #before-you-begin}

다음이 있어야 합니다.

* 웹 앱. 
* {{site.data.keyword.amashort}} 서비스를 통해 보호하는 {{site.data.keyword.Bluemix_notm}} 애플리케이션의 인스턴스입니다. {{site.data.keyword.Bluemix_notm}} 백엔드 애플리케이션 작성 방법에 대한 자세한 정보는 [시작하기](index.html)를 참조하십시오.
* 최종 경로 재지정을 위한 URI(권한 부여 프로세스가 완료된 이후).


## 웹 사이트에 맞게 Google 애플리케이션 구성
{: #google-auth-config}

ID 제공자로 Google 사용을 시작하려면 [Google 개발자 콘솔 ![외부 링크 아이콘](../../icons/launch-glyph.svg "외부 링크 아이콘")](https://console.developers.google.com){: new_window}에서 프로젝트를 작성하십시오. 프로젝트 작성의 일부로 **Google 클라이언트 ID** 및 **본인확인정보**를 확보하십시오. Google 클라이언트 ID 및 본인확인정보는 Google 인증에서 사용하는 애플리케이션에 대한 고유 ID이며, {{site.data.keyword.amashort}} 대시보드 설정에 필요합니다. 

1. Google 개발자 콘솔에서 Google 애플리케이션을 여십시오. 
3. **Google+** API를 추가하십시오. 
3. OAuth를 사용하여 신임 정보를 작성하십시오. 애플리케이션 유형으로 웹 애플리케이션을 선택하십시오. 권한 부여된 경로 재지정 URI 상자에 {{site.data.keyword.amashort}} 경로 재지정 URI를 입력하십시오. {{site.data.keyword.amashort}} 대시보드의 Google 구성 화면에서 {{site.data.keyword.amashort}} 경로 재지정 권한 URI를 얻으십시오(아래 단계 참조). 
4. 변경사항을 저장하십시오. **Google 클라이언트 ID** 및 **애플리케이션 본인확인정보**를 기록해 두십시오.


## Google 인증용 {{site.data.keyword.amashort}} 구성
{: #google-auth-config-ama}

Google 애플리케이션 ID와 본인확인정보가 있으면 {{site.data.keyword.amashort}} 대시보드에서 Google 인증을 사용할 수 있습니다.

1. {{site.data.keyword.amashort}} 서비스 대시보드를 여십시오. 
1. **관리** 탭에서 **권한**을 토글하여 켜십시오. 
1. **Google** 섹션을 여십시오. 
1. **웹 앱에 Google 추가**를 선택하십시오. 
4. **웹에 대해 구성** 섹션에서:    
    * **Google 개발자 콘솔에 대한 Mobile Client Access 경로 재지정 URI** 텍스트 상자의 값을 기록해 두십시오. 이는 **Google 개발자 포털**의 **웹 애플리케이션에 대한 클라이언트 ID의 제한사항** 아래에 있는 **권한 부여된 경로 재지정 URI** 상자에 추가해야 하는 값입니다.
    * **클라이언트 ID** 및 **클라이언트 본인확인정보**를 입력하십시오. 
    * 경로 재지정 URI를 **웹 애플리케이션 경로 재지정 URI**에 입력하십시오. 이 값은 권한 부여 프로세스가 완료된 후에 액세스할 경로 재지정 URI용 값이며 개발자가 판별합니다. 
5. **저장**을 클릭하십시오.


## ID 제공자로 Google을 사용하여 {{site.data.keyword.amashort}} 권한 부여 플로우 구현
{: #google-auth-flow}

`VCAP_SERVICES` 환경 변수는 각 {{site.data.keyword.amashort}} 서비스 인스턴스에 대해 자동으로 작성되며 권한 부여 프로세스에 필요한 특성을 포함합니다. JSON 오브젝트로 구성되며 {{site.data.keyword.amashort}} 서비스 대시보드의 **서비스 신임 정보** 탭을 클릭하면 표시됩니다. 

권한 부여 프로세스를 시작하려면 다음을 수행하십시오. 

1. 권한 엔드포인트(`authorizationEndpoint`) 및 클라이언트 ID(`clientId`)를 `VCAP_SERVICES` 환경 변수에 저장된 서비스 신임 정보에서 검색하십시오. 

	`var cfEnv = require("cfenv");`

	`var mcaCredentials = cfEnv.getAppEnv().services.AdvancedMobileAccess[0].credentials;`

	**참고:** 웹 지원을 추가하기 전에 애플리케이션에 {{site.data.keyword.amashort}} 서비스를 추가한 경우 서비스 신임 정보에 토큰 엔드포인트가 없을 수 있습니다. 대신, {{site.data.keyword.Bluemix_notm}} 지역에 따라 다음 URL을 사용하십시오.

	미국 남부: 

	`https://mobileclientaccess.ng.bluemix.net/oauth/v2/authorization`

	런던:

	`https://mobileclientaccess.eu-gb.bluemix.net/oauth/v2/authorization`

	시드니:

	`https://mobileclientaccess.au-syd.bluemix.net/oauth/v2/authorization`

2. 조회 매개변수로 `response_type("code")`, `client_id` 및 `redirect_uri`를 사용하여 권한 서버 URI를 빌드하십시오. 

3. 웹 앱에서 생성된 URI로 경로를 재지정하십시오. 

	다음 예에서는 `VCAP_SERVICES` 변수에서 매개변수를 검색하여 URL을 빌드하고 경로 재지정 요청을 전송합니다.

	```Java
	var cfEnv = require("cfenv");
	app.get("/protected", checkAuthentication, function(req, res, next) {
		res.send("Hello from protected endpoint");
	});

	function checkAuthentication(req, res, next) {
		// Check if user is authenticated
		if (req.session.userIdentity) {
			next()
		} else {
			// If not - redirect to authorization server
			var mcaCredentials = cfEnv.getAppEnv().services.AdvancedMobileAccess[0].credentials;
			var authorizationEndpoint = mcaCredentials.authorizationEndpoint;
			var clientId = mcaCredentials.clientId;
			var redirectUri = "http://some-server/oauth/callback"; // Your Web application redirect URI
			var redirectUrl = authorizationEndpoint + "?response_type=code";
			redirectUrl += "&client_id=" + clientId;
			redirectUrl += "&redirect_uri=" + redirectUri;
			res.redirect(redirectUrl);
		}
	}
	```
	{: codeblock}

	`redirect_uri` 매개변수는 웹 애플리케이션 경로 재지정 URI를 나타내며 {{site.data.keyword.amashort}} 대시보드에 정의된 URI와 동일해야 합니다.

	권한 엔드포인트로 경로 재지정 후 사용자는 Google로부터 로그인 양식을 받게 됩니다. 사용자에게 Google ID를 사용하여 로그인할 수 있는 권한이 부여되면 {{site.data.keyword.amashort}} 서비스는 조회 매개변수로 권한 부여 코드를 제공하여 웹 애플리케이션 경로 재지정 URI를 호출합니다.

## 토큰 확보
{: #google-auth-tokens}

다음 단계는 이전에 받은 권한 부여 코드를 사용하여 액세스 토큰 및 ID 토큰을 확보하는 것입니다. 

1. `VCAP_SERVICES` 환경 변수에 저장된 서비스 신임 정보의 토큰 `tokenEndpoint`, `clientId` 및 `secret`을 검색하십시오.

	**참고:** 웹 지원이 추가되기 전에 {{site.data.keyword.amashort}}를 사용한 경우 서비스 신임 정보에 토큰 엔드포인트가 없을 수 있습니다. 대신, Bluemix 지역에 따라 다음 URL을 사용하십시오.

	미국 남부: 

	`https://mobileclientaccess.ng.bluemix.net/oauth/v2/token`

	런던:

	`https://mobileclientaccess.eu-gb.bluemix.net/oauth/v2/token`

	시드니:

	`https://mobileclientaccess.au-syd.bluemix.net/oauth/v2/token`

2. 양식 매개변수로 grant_type("authorization_code"), client_id, redirect_uri 및 코드를 사용하여 post 요청을 토큰 서버 URI로 전송하십시오. 기본 HTTP 인증 신임 정보로 `clientId` 및 `clientSecret`을 전송하십시오. 

	다음 코드는 필요한 값을 검색하고 post 요청을 사용하여 값을 전송합니다. 

	```Java    
	var cfEnv = require("cfenv");
	var base64url = require("base64url ");
	var request = require('request');

	app.get("/oauth/callback", function(req, res, next) {
		var mcaCredentials = cfEnv.getAppEnv().services.AdvancedMobileAccess[0].credentials;
		var tokenEndpoint = mcaCredentials.tokenEndpoint;
		var formData = {
			grant_type: "authorization_code",
			client_id: mcaCredentials.clientId,
			redirect_uri: "http://some-server/oauth/callback",// Your Web application redirect uri
			code: req.query.code
		}

		request.post({
			url: tokenEndpoint,
			formData: formData
		}, function (err, response, body) {
			var parsedBody = JSON.parse(body);
			req.session.accessToken = parsedBody.access_token;
			req.session.idToken = parsedBody.id_token;
			var idTokenComponents = parsedBody.id_token.split("."); // [header, payload, signature]
			var decodedIdentity= base64url.decode(idTokenComponents[1]);
			req.session.userIdentity = JSON.parse(decodedIdentity)["imf.user"];
			res.redirect("/");
			}
			).auth(mcaCredentials.clientId, mcaCredentials.secret);
		}
	);
	```
	{: codeblock}

	`redirect_uri` 매개변수는 Google+를 사용하는 인증 성공 또는 실패 이후 경로 재지정을 위한 URI이며, {{site.data.keyword.amashort}} 대시보드에서 정의된 `redirect_uri`와 일치해야 합니다.   

	권한 부여 코드가 만료되기 10분 전 이내에 이 POST 요청을 전송해야 합니다. 10분이 지나면 새 코드가 필요합니다.

	POST 응답 본문에는 base64로 인코딩된 `access_token` 및 `id_token`이 포함됩니다.

	액세스 및 ID 토큰을 받은 후에는 웹 세션을 인증됨으로 플래그 지정할 수 있으며 선택적으로 이러한 토큰을 유지할 수 있습니다.   


##확보한 액세스 권한 및 ID 토큰 사용
{: #google-auth-using-token}

ID 토큰에는 사용자 ID에 대한 정보가 포함되어 있습니다. Google 인증의 경우 토큰에는 사용자가 공유하도록 동의한 모든 정보가 포함됩니다(예: 전체 이름, 프로파일 사진의 URL 등).  

액세스 토큰을 통해 {{site.data.keyword.amashort}} 권한 필터에서 보호하는 리소스와 통신할 수 있습니다. [리소스 보호](protecting-resources.html)를 읽어보십시오.

보호 리소스에 대한 요청을 작성하려면 다음 구조를 사용하여 권한 헤더를 요청에 추가하십시오.

`Authorization=Bearer <accessToken> <idToken>`

####팁:
{: #tips}

* `accessToken` 및 `idToken`은 공백으로 구분해야 합니다. 

* `idToken`은 선택사항입니다. ID 토큰을 제공하지 않는 경우 보호 리소스에 액세스할 수 있지만, 권한 부여된 사용자에 대한 정보는 수신하지 않습니다.
