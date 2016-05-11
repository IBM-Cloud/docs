---

copyright:
  years: 2015, 2016

---

# 사용자 정의 ID 제공자 작성
{: #custom-create}
사용자 정의 ID 제공자를 작성하려면 RESTful API를 표시하는 웹 애플리케이션을
개발하십시오. 

```
POST <base_url>/apps/<tenant_id>/<realm_name>/<request_type>
```

* `base_url`: 사용자 정의 ID 제공자 웹 애플리케이션의 기본 URL입니다.
기본 URL은 {{site.data.keyword.amashort}} 대시보드에 등록할 URL입니다. 
* `tenant_id`: 테넌트의 고유 ID입니다. {{site.data.keyword.amashort}}는 이 API를 호출할 때 항상 {{site.data.keyword.Bluemix}} 앱 GUID(`applicationGUID`)를 제공합니다.
* `realm_name`: {{site.data.keyword.amashort}} 대시보드에 정의된
사용자 정의 영역 이름을 지정합니다. 
* `request_type`: 다음 중 하나를 지정합니다. 
	* `startAuthorization`: 인증 프로세스의 첫 번째 단계를 지정합니다.
사용자 정의 ID 제공자는 "challenge", "success", "failure" 상태 중 하나로 응답해야 합니다. 
	* `handleChallengeAnswer`: 모바일 클라이언트에서 인증 확인 응답을
처리합니다. 

## `startAuthorization` API
{: #custom-startauthorization}

`POST <base_url>/apps/<tenant_id>/<realm_name>/startAuthorization`

`startAuthorization` API는 인증 프로세스의 첫 번째 단계로 사용됩니다. 사용자 정의 ID 제공자는 "challenge", "success", "failure" 상태 중 하나로 응답해야 합니다. 

인증 프로세스의 최대 유연성을 고려하려면 사용자 정의 ID 제공자가 요청 본문에서
모바일 클라이언트가 전송하는 모든 HTTP 헤더에 액세스할 수 있어야 합니다. 헤더는
다음과 같은 형식으로 제공됩니다. 

```JavaScript
{
    "headers" : {
    	"header1": "value1",  
    	"header2" : "value2"
    }
}
```

사용자 정의 ID 제공자는 인증 확인, 즉각적 성공, 실패 중 하나로 응답할 수 있습니다.
응답 HTTP 상태는 `HTTP 200`이어야 하고 응답 JSON이
다음과 같은 특성을 포함해야 합니다. 

* `status`: 요청의 `success`, `challenge`, `failure`
중 하나를 지정합니다. 
* `stateId`(선택사항): 모바일 클라이언트에서 인증 세션을 식별하기 위해
무작위로 생성된 문자열 ID를 지정합니다. 사용자 정의 ID 제공자가 상태를 저장하지 않는 경우
이 속성을 생략할 수 있습니다. 
* `challenge`: 모바일 클라이언트로 다시 전송할 인증 확인을 나타내는
JSON 오브젝트를 지정합니다. 상태가 `challenge`로 설정된 경우에만 이 속성이 전송됩니다. 
* `userIdentity`: 사용자 ID를 나타내는 JSON 오브젝트를 지정합니다.
사용자 ID는 `userName`, `displayName`, 속성 등의
특성으로 구성됩니다. 자세한 정보는 [사용자 ID 오브젝트](#custom-user-identity)를
참조하십시오. 상태가 `success`로 설정된 경우에만 이 특성이
모바일 클라이언트로 전송됩니다. 

예를 들면 다음과 같습니다.


```
{
	"status":"challenge",
	"stateId":"some-random-guid"
	"challenge":{
		message:"Enter username and password",
		attemptsLeft: 3
	}
}
```

## `handleChallengeAnswer` API
{: #custom-handleChallengeAnswer}

`POST <base_url>/apps/<tenant_id>/<realm_name>/handleChallengeAnswer`

`handleChallengeAnswer` API는 모바일 클라이언트에서 인증 확인 응답을
처리합니다. `startAuthorization` API와 마찬가지로,
`handleChallengeAnswer` API는 `challenge`, `success`,
`failure` 상태 중 하나로 응답합니다. 

`startAuthorization` 요청과 마찬가지로, 사용자 정의 ID 제공자가
요청 본문에서 모바일 클라이언트가 전송하는 모든 HTTP 헤더에 액세스할 수 있어야 합니다.
모바일 클라이언트 요청 헤더뿐만 아니라, `handleChallengeAnswer` 요청의 본문에는
`stateId` 및 `challengeAnswer` 특성도 포함됩니다. 

### `handleChallengeAnswer` 요청 본문의 예
{: #custom-handleChallengeAnswer-example}

```JavaScript
{
    "headers" : {
    	"header1": "value1",  
    	"header2" : "value2"
	},
    "stateId" : "123123123",
    "challengeAnswer" : {
    	"pinCode":12345
 	}
}
```

`handleChallengeAnswer` API의 응답은 `startAuthorization` API의
응답과 동일한 구조여야 합니다. 

## 사용자 ID 오브젝트
{: #custom-user-identity}

성공적인 인증 요청에 대한 응답에는 다음 속성이 들어 있는 사용자 ID 오브젝트가
포함되어야 합니다. 
* `userName`: 고유한 사용자 이름을 지정합니다. 
* `displayName`: 사용자의 표시 이름을 지정합니다. 
* `attributes`(선택사항): 사용자 정의 속성이 포함된
JSON 오브젝트를 지정합니다. 

### 사용자 ID 오브젝트 예
{: #custom-user-identity-example}
```JavaScript
{
    "userName" : "janesmith",
    "displayName" : "Jane Smith",
    "attributes" : {
        "Language" : "French",
        "Country" : "Canada"
    }
}
```

사용자 ID 오브젝트는 {{site.data.keyword.amashort}} 서비스가 모바일 클라이언트에
권한 헤더의 일부로 전송할 ID 토큰을 생성하는 데 사용됩니다. 인증에 성공하면
모바일 클라이언트가 사용자 ID 오브젝트에 대한 전체 액세스 권한을 갖게 됩니다. 

## 보안 고려사항
{: #custom-security}

요청의 출처가 권한이 부여된 소스임을 사용자 정의 ID 제공자가 확인할 수 있도록
{{site.data.keyword.amashort}} 서비스에서 사용자 정의 ID 제공자로 전송되는
각 요청에는 권한 헤더가 포함되어 있습니다. 필수적인 사항은 아니지만, 사용자 정의 ID 제공자에
{{site.data.keyword.amashort}} 서버 SDK를 제공하여 권한 헤더의 유효성을
검증하십시오. 이 SDK를 사용하려면 사용자 정의 ID 제공자 애플리케이션이 Node.js 또는 Liberty for Java&trade;&trade;를 사용하여 구현되고 {{site.data.keyword.Bluemix_notm}}에서 실행되어야 합니다.

권한 헤더에는 인증 프로세스를 트리거한 모바일 클라이언트 및 모바일 앱에 대한 정보가
포함되어 있습니다. 보안 컨텍스트를 사용하여 이 데이터를 검색할 수 있습니다.
자세한 정보는 [자원 보호](protecting-resources.html)를 참조하십시오. 

## 사용자 정의 ID 제공자의 샘플 구현
{: #custom-sample}
사용자 정의 ID 제공자를 개발할 때는 사용자 정의 ID 제공자의 다음 Node.js 샘플 구현을 참조로 사용할 수 있습니다. 
GitHub 저장소에서 전체 애플리케이션 코드를 다운로드하십시오. 

* [단순 샘플](https://github.com/ibm-bluemix-mobile-services/bms-mca-custom-identity-provider-sample)
* [고급 샘플](https://github.com/ibm-bluemix-mobile-services/bms-mca-custom-identity-provider-with-user-management)

<!---
 ### JSON structure (simple sample)
{: #custom-sample-json}
This implementation assumes that the supplied authentication challenge answer is a JSON object with the following structure:

```
{
 	username: "my.username",
 	password: "my.password"
 }
 ```

### Custom identity provider sample code (simple sample)
{: #custom-sample-code}
```JavaScript
var express = require('express');
var cfenv = require('cfenv');
var log4js = require('log4js');
var jsonParser = require('body-parser').json();

// Using hardcoded user repository
var userRepository = {
	"john.lennon":      { password: "12345", displayName:"John Lennon", dob:"October 9, 1940"},
	"paul.mccartney":   { password: "67890", displayName:"Paul McCartney", dob:"June 18, 1942"},
	"ringo.starr":      { password: "abcde", displayName:"Ringo Starr", dob: "July 7, 1940"},
	"george.harrison":  { password: "fghij", displayName: "George Harrison", dob:"Feburary 25, 1943"}
}

var app = express();
var logger = log4js.getLogger("CustomIdentityProviderApp");
logger.info("Starting up");

app.post('/apps/:tenantId/:realmName/startAuthorization', jsonParser, function(req, res){
	var tenantId = req.params.tenantId;
	var realmName = req.params.realmName;
	var headers = req.body.headers;

	logger.debug("startAuthorization", tenantId, realmName, headers);

	var responseJson = {
		status: "challenge",
		challenge: {
			text: "Enter username and password"
		}
	};

	res.status(200).json(responseJson);
});

app.post('/apps/:tenantId/:realmName/handleChallengeAnswer', jsonParser, function(req, res){
	var tenantId = req.params.tenantId;
	var realmName = req.params.realmName;
	var challengeAnswer = req.body.challengeAnswer;


	logger.debug("handleChallengeAnswer", tenantId, realmName, challengeAnswer);

	var username = req.body.challengeAnswer["username"];
	var password = req.body.challengeAnswer["password"];

	var userObject = userRepository[username];

	var responseJson = { status: "failure" };

	if (userObject && userObject.password == password ){
		logger.debug("Login success for userId ::", username);
		responseJson.status = "success";
		responseJson.userIdentity = {
			userName: username,
			displayName: userObject.displayName,
			attributes: {
				dob: userObject.dob
			}
		}
	} else {
		logger.debug("Login failure for userId ::", username);
	}

	res.status(200).json(responseJson);
});

app.use(function(req, res, next){
	res.status(404).send("This is not the URL you're looking for");
});

var server = app.listen(cfenv.getAppEnv().port, function () {
	var host = server.address().address;
	var port = server.address().port;
	logger.info('Server listening at %s:%s', host, port);
});
```
--->

## 다음 단계
{: #next-steps}
* [사용자 정의 인증을 사용하도록 {{site.data.keyword.amashort}} 구성](custom-auth-config-mca.html)
* [Android에 대해 사용자 정의 인증 구성](custom-auth-android.html)
* [iOS에 대해 사용자 정의 인증 구성](custom-auth-ios.html)
* [Cordova에 대해 사용자 정의 인증 구성](custom-auth-cordova.html)
