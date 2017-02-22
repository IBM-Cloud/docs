---

copyright:
  years: 2016, 2017
lastupdated: "2017-01-08"

---
{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}

#{{site.data.keyword.amashort}} 웹 애플리케이션용 사용자 정의 인증 구성
{: #custom-web}

사용자 정의 인증 및 {{site.data.keyword.amafull}} 보안 기능을 웹 앱에 추가하십시오.

## 시작하기 전에
{: #before-you-begin}

시작하기 전에 다음이 있어야 합니다. 

* 웹 앱. 
* 사용자 정의 ID 제공자를 사용하도록 구성된 {{site.data.keyword.amashort}} 서비스 인스턴스에 의해 보호되는 리소스([사용자 정의 인증 구성 참조](custom-auth-config-mca.html)).  
* **테넌트 ID** 값. {{site.data.keyword.amashort}} 대시보드에서 서비스를 여십시오. **모바일 옵션** 단추를 클릭하십시오. **앱 GUID / TenantId** 필드에 `tenantId`(`appGUID`라고도 함) 값이 표시됩니다. 이 값은 권한 관리자를 초기화하는 데 필요합니다. 
* **영역** 이름. 이 값은 {{site.data.keyword.amashort}} 대시보드의 **관리** 탭에서 **사용자 정의** 섹션의 **영역 이름** 필드에 지정한 값입니다. 
* 백엔드 애플리케이션의 URL(**앱 라우트**). 이 값은 백엔드 애플리케이션의 보호 엔드포인트에 요청을 전송하는 데 필요합니다. 
* {{site.data.keyword.Bluemix_notm}} **지역**. 헤더에서 **아바타** 아이콘 ![아바타 아이콘](images/face.jpg "아바타 아이콘") 옆에 현재 {{site.data.keyword.Bluemix_notm}} 지역이 표시됩니다. 표시되는 지역 값은 `US South`, `United Kingdom` 및 `Sydney` 중 하나여야 하며 Javascript 코드 `BMSClient.REGION_US_SOUTH`, `BMSClient.REGION_SYDNEY` 또는 `BMSClient.REGION_UK`에 필요한 SDK 값에 해당해야 합니다. 이 값은 {{site.data.keyword.amashort}} 클라이언트를 초기화하는 데 필요합니다. 
* 최종 경로 재지정을 위한 URI(권한 부여 프로세스가 완료된 이후).이 값은 **관리** 탭의 **사용자 정의** 섹션에 입력한 **웹 애플리케이션 경로 재지정 URI** 값입니다. 

자세한 정보: 

* [{{site.data.keyword.amashort}}](getting-started.html) 시작하기
* [사용자 정의 ID 제공자 사용](custom-auth.html)
* [사용자 정의 ID 제공자 작성](custom-auth-identity-provider.html)
* [사용자 정의 인증용 {{site.data.keyword.amashort}} 구성](custom-auth-config-mca.html)


##사용자 정의 ID 제공자 구성
{: #custom-auth-config}

사용자 정의 ID 제공자를 작성하는 경우 다음 구조의 라우트를 사용하여 POST 메소드를 정의해야 합니다. 

`/apps/:tenantID/<your-realm-name>/handleChallengeAnswer`

`tenantID`는 URL 매개변수이며 `<your-realm-name>`은 사용자가 선택한 영역 이름입니다. 

요청 본문에는 `username` 및 `password`가 있는 `challengeAnswer` 오브젝트가 포함됩니다.

사용자의 유효성을 검증한 후 이 라우트에서 다음 구조의 JSON 오브젝트를 리턴해야 합니다. 

```json
{
	status: "success",
	userIdentity: {
		userName: <user name>,
		displayName: <display name>
		attributes: <additional attributes json>
	}
}
```
{: codeblock}

**참고:** `attributes` 필드는 선택사항입니다. 

다음 코드는 POST 요청을 보여줍니다. 

```Java
var app = express();
var bodyParser = require('body-parser');
app.use(bodyParser.json());

var users = {
	"John": {
		password: "123",
		displayName: "John Doe"
	}
};

app.post('/apps/:tenantID/customAuthRealm_1/handleChallengeAnswer', function(req, res) {
	console.log ("tenantID " + req.params.tenantID);

	var challengeAnswer = req.body.challengeAnswer;
	console.log ("challengeAnswer " + JSON.stringify(challengeAnswer));

	if (challengeAnswer && users[challengeAnswer.username] && challengeAnswer.password === users[challengeAnswer.username].password) {
		res.json({
			status: "success",
			userIdentity: {
				userName: challengeAnswer.username,
				displayName: users[challengeAnswer.username].displayName
			}
		});
	} else {
		res.json({
			status: "failure"
		});
	}

});
```
{: codeblock}


##사용자 정의 인증용 {{site.data.keyword.amashort}} 구성
{: #custom-auth-config-mca}

사용자 정의 ID 제공자를 구성하면 {{site.data.keyword.amashort}} 대시보드에서 사용자 정의 인증을 사용으로 설정할 수 있습니다. 

1. {{site.data.keyword.amashort}} 대시보드에서 서비스를 여십시오. 
1. **관리** 탭에서 **권한**을 토글하여 켜십시오. 
1. **사용자 정의** 섹션을 펼치십시오. 
1. **영역 이름**, **사용자 정의 ID 제공자 URL**을 입력하십시오. 
1. **웹 애플리케이션 경로 재지정 URI** 값을 입력하십시오. 이 값은 인증에 성공한 후의 최종 경로 재지정 URI입니다. 
1. **저장**을 클릭하십시오.


##사용자 정의 ID 제공자를 사용하여 {{site.data.keyword.amashort}} 권한 부여 플로우 구현
{: #custom-auth-flow}

`VCAP_SERVICES` 환경 변수는 각 {{site.data.keyword.amashort}} 서비스 인스턴스에 대해 자동으로 작성되며 권한 부여 프로세스에 필요한 특성을 포함합니다. JSON 오브젝트로 구성되며 {{site.data.keyword.amashort}} 대시보드의 **서비스 신임 정보** 탭에 표시됩니다. 

사용자 권한 부여를 요청하려면, 브라우저를 권한 서버 엔드포인트로 경로를 재지정하십시오. 이를 위해 다음을 수행하십시오. 

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

   다음 예는 `VCAP_SERVICES` 변수에서 매개변수를 검색하고, URL을 빌드하고, 경로 재지정 요청을 전송합니다. 

	```Java
	var cfEnv = require("cfenv");
	app.get("/protected", checkAuthentication, function(req, res, next) {
		res.send("Hello from protected endpoint");
	}
	);

	function checkAuthentication(req, res, next) {
		// Check if user is authenticated
		if (req.session.userIdentity) {
			next()
		} else {
			// If not - redirect to authorization server
			var mcaCredentials = cfEnv.getAppEnv().services.AdvancedMobileAccess[0].credentials;
			var authorizationEndpoint = mcaCredentials.authorizationEndpoint;
			var clientId = mcaCredentials.clientId;
			var redirectUri = "http://some-server/oauth/callback"; // Your web application redirect uri
			var redirectUrl = authorizationEndpoint + "?response_type=code";
			redirectUrl += "&client_id=" + clientId;
			redirectUrl += "&redirect_uri=" + redirectUri;
			res.redirect(redirectUrl);
		}
	}
	```
	{: codeblock}

	`redirect_uri` 매개변수는 웹 애플리케이션 경로 재지정 URI를 나타내며 {{site.data.keyword.amashort}} 대시보드에 정의된 URI와 동일해야 합니다.  

	`state` 매개변수를 요청과 함께 전달할 수 있습니다. 이 매개변수는 사용자 정의 ID 제공자 POST 메소드에 전파되며, 요청 본문에서 액세스할 수 있습니다(`req.body.stateId`).   

	권한 엔드포인트로 경로 재지정 후 사용자는 로그인 양식을 받게 됩니다. 사용자의 신임 정보가 사용자 정의 ID 제공자에 의해 인증되면 {{site.data.keyword.amashort}} 서비스는 조회 매개변수로 권한 부여 코드를 제공하여 웹 애플리케이션 경로 재지정 URI를 호출합니다.   

	경로 재지정 후 사용자는 로그인 양식을 받습니다. 사용자의 신임 정보가 사용자 정의 ID 제공자에 의해 인증되면 {{site.data.keyword.amashort}} 서비스는 조회 매개변수로 권한 부여 코드를 제공하여 웹 애플리케이션 경로 재지정 URI를 호출합니다. 

##토큰 확보
{: custom-auth-tokens}

다음 단계는 이전에 받은 권한 부여 코드를 사용하여 액세스 토큰 및 ID 토큰을 확보하는 것입니다. 이를 위해 다음을 수행하십시오. 

1. `authorizationEndpoint`, `clientId` 및 `secret`을 `VCAP_SERVICES` 환경 변수에 저장된 서비스 신임 정보에서 검색하십시오. 

	**참고:** 웹 지원을 추가하기 전에 애플리케이션에 {{site.data.keyword.amashort}} 서비스를 추가한 경우 서비스 신임 정보에 토큰 엔드포인트가 없을 수 있습니다. 대신, {{site.data.keyword.Bluemix_notm}} 지역에 따라 다음 URL을 사용하십시오.

	미국 남부: 

	`https://mobileclientaccess.ng.bluemix.net/oauth/v2/token`

	런던:

	`https://mobileclientaccess.eu-gb.bluemix.net/oauth/v2/token`

	시드니:

	`https://mobileclientaccess.au-syd.bluemix.net/oauth/v2/token`

2. 양식 매개변수로 `grant_type`, `client_id`, `redirect_uri` 및 `code`를 사용하고 기본 HTTP 인증 신임 정보로 `clientId` 및 `secret`을 사용하여 POST 요청을 토큰 서버 URI에 전송하십시오. 

	아래 예에서는 다음 코드가 필요한 값을 검색하고 POST 요청을 사용하여 값을 전송합니다. 

	```Java
	var cfEnv = require("cfenv");
	var base64url = require("base64url");
	app.get("/oauth/callback", function(req, res, next) {
		var mcaCredentials = cfEnv.getAppEnv().services.AdvancedMobileAccess[0].credentials;
		var tokenEndpoint = mcaCredentials.tokenEndpoint;

		var formData = {
			grant_type: "authorization_code",
			client_id: mcaCredentials.clientId,
			redirect_uri: "http://some-server/oauth/callback",   // Your Web application redirect uri
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

	`redirect_uri` 매개변수는 이전 권한 부여 요청에 사용된 `redirect_uri`와 일치해야 합니다. 코드 매개변수 값은 권한 부여 요청 종료 시 응답에 수신된 권한 부여 코드여야 합니다. 권한 부여 코드는 10분 동안만 유효합니다. 이후에는 새 코드를 확보해야 합니다.

	응답 본문에는 JWT 형식의 `access_token` 및 `id_token`이 포함됩니다. [JWT 웹 사이트 ![외부 링크 아이콘](../../icons/launch-glyph.svg "외부 링크 아이콘")](https://jwt.io "외부 링크 아이콘"){: new_window}를 참조하십시오. 

	액세스 및 ID 토큰을 받은 후에는 웹 세션을 인증됨으로 플래그 지정할 수 있으며 선택적으로 이러한 토큰을 유지할 수 있습니다. 


##확보한 액세스 권한 및 ID 토큰 사용
{: #custom-auth-using-token}

ID 토큰에는 사용자 ID에 대한 정보가 포함되어 있습니다. 사용자 정의 인증의 경우 토큰에는 인증 시 사용자 정의 ID 제공자가 리턴하는 모든 정보가 포함됩니다. `imf.user` 필드 아래 `displayName` 필드에는 사용자 정의 ID 제공자가 리턴하는 `displayName`이 포함되고, `id` 필드에는 `userName`이 포함됩니다. 사용자 정의 ID 제공자가 리턴하는 다른 모든 값은 `imf.user` 아래의 `attributes` 필드 내에 리턴됩니다.   

액세스 토큰을 통해 {{site.data.keyword.amashort}} 권한 필터에서 보호하는 리소스와 통신할 수 있습니다([리소스 보호](protecting-resources.html) 참조). 보호 리소스에 대한 요청을 작성하려면 다음 구조를 사용하여 권한 헤더를 요청에 추가하십시오.

`Authorization=Bearer <accessToken> <idToken>`

####팁:
{: #tips_token}

* `<accessToken>` 및 `<idToken>`은 공백으로 구분해야 합니다.

* ID 토큰은 선택사항입니다. ID 토큰을 제공하지 않는 경우 보호 리소스에 액세스할 수 있지만, 권한 부여된 사용자에 대한 정보는 수신하지 않습니다.
