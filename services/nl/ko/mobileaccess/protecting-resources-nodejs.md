---

copyright:
  years: 2015, 2016

---

# {{site.data.keyword.amashort}}를 사용하여 Node.js 자원 보호
{: #protecting-resources-nodejs}

{{site.data.keyword.amashort}} 서버 SDK를 사용하여 Node.js 앱의 자원을 보호할 수 있습니다. 

### 시작하기 전에
{: #before-you-begin}

* {{site.data.keyword.Bluemix_notm}}에서 Node.js 애플리케이션을 개발하는 데 익숙해야 합니다. 자세한 정보는 [Node.js용 SDK를 사용하여 앱 작성](https://console.{DomainName}/docs/runtimes/nodejs/index.html#nodejs_runtime)을 참조하십시오. 
* {{site.data.keyword.amashort}} 서버 SDK에서는 Node.js 서버를 `Express` 프레임워크로 구현해야 합니다. LoopBack과 같이 `Express` 프레임워크를 사용하는 여러 가지 다른 프레임워크가 있습니다. 해당 프레임워크로 {{site.data.keyword.amashort}} 서버 SDK를 사용할 수 있습니다. Express 프레임워크에 대한 자세한 정보는 [Expressjs.com](http://expressjs.com/)을 참조하십시오. 

### {{site.data.keyword.amashort}} 서버 SDK 정보
{: #about}

{{site.data.keyword.amashort}} 서버 SDK는 IBM {{site.data.keyword.Bluemix_notm}}에서 배치된 백엔드 애플리케이션에 사용될 `MCABackendStrategy` 패스포트 전략을 제공합니다. 권한이 없는 액세스에서 사용자 앱을 보호하고 모니터링 정보를 가져오려면, `MCABackendStrategy`로 Node.js 서버를 계측해야 합니다. `bms-mca-token-validation-strategy` npm 모듈은 {{site.data.keyword.amashort}}에서 발행한 액세스 토큰 및 ID 토큰의 유효성을 검증하도록 `MCABackendStrategy` 패스포트 전략 및 검증 방법을 제공합니다. 또한 이 모듈은 보안 이벤트에 대한 모니터링 정보를 자동으로 제공합니다. 

{{site.data.keyword.amashort}} 서버 SDK는 권한 부여를 강화하기 위해 `Passport` 프레임워크를 제공합니다. 자세한 정보는 [Passportjs.org](http://passportjs.org/)를 참조하십시오. 

### {{site.data.keyword.amashort}} 서버 SDK 설치
{: #protecting-resources-serversdk}

명령행에서 Node.js 애플리케이션이 포함된 디렉토리를 열고 다음 명령을 실행하십시오. 

```
npm install -save express
npm install -save passport
npm install -save bms-mca-token-validation-strategy
```

### Node.js의 자원 보호
{: #protecting-resources-nodesdk}

다음 스니펫은 단순 Express 애플리케이션에서 `MCABackendStrategy`를 사용하는 방법 및 `/protected` 엔드포인트 GET 메소드를 보호하는 방법을 보여줍니다. 

```JavaScript
var express = require('express');
var passport = require('passport');
var MCABackendStrategy = require('bms-mca-token-validation-strategy').MCABackendStrategy;

passport.use(new MCABackendStrategy());

var app = express();
app.use(passport.initialize());

app.get('/protected', passport.authenticate('mca-backend-strategy', {session: false }),
    function(request, response){
		console.log("Securty context", request.securityContext)    
		response.send(200, "Success!");
    }
);

app.listen(process.env.PORT);
```
