---

copyright:
  years: 2017
lastupdated: "2017-04-17"

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:pre: .pre}

# Node.js 리소스 보호
{: #protecting-resources-nodejs}

{{site.data.keyword.appid_short}} 서버 SDK를 사용하여 Node.js 앱의 리소스를 보호할 수 있습니다.
{:shortdesc}

## 시작하기 전에
{: #before-you-begin}

* {{site.data.keyword.Bluemix_notm}}에서 Node.js 애플리케이션 개발에 익숙해지십시오.
* {{site.data.keyword.appid_short_notm}} 서버 SDK를 사용하려면 Node.js 서버를 <a href="http://expressjs.com/" target="_blank">Express 프레임워크 <img src="../../icons/launch-glyph.svg" alt="외부 링크 아이콘"></a>으로 구현해야 합니다. 

**참고**: `Express` 프레임워크(예: LoopBack)를 사용하는 다른 프레임워크가 있습니다. 이러한 프레임워크와 함께 {{site.data.keyword.appid_short_notm}} 서버 SDK를 사용할 수 있습니다. 


## 서버 SDK 설치
{: #protecting-resources-serversdk}

1. 명령행을 사용하여 Node.js 앱이 있는 디렉토리를 여십시오. 
2. 다음 명령을 실행하십시오. 

  ```
  npm install -save express
  npm install -save passport
  npm install -save bluemix-appid
  ```
  {:pre}

## Node.js의 리소스 보호
{: #protecting-resources-nodesdk}

{{site.data.keyword.appid_short_notm}} 서버 SDK는 {{site.data.keyword.Bluemix_notm}}에 배치된 백엔드 애플리케이션에 사용된 ApiStrategy 패스포트 전략을 제공합니다. 권한이 없는 액세스에서 앱을 보호하려면 ApiStrategy로 Node.js 서버를 인스트루먼트해야 합니다. `appid-serversdk-nodejs npm module`은 {{site.data.keyword.appid_short_notm}}에서 발행한 액세스 토큰 및 ID 토큰의 유효성을 검증하도록 검증 방법과 ApiStrategy 패스포트 전략을 제공합니다. 

{{site.data.keyword.appid_short_notm}} 서버 SDK는 <a href="http://passportjs.org/" target="_blank">Passport 프레임워크 <img src="../../icons/launch-glyph.svg" alt="외부 링크 아이콘"></a>을 사용하여 권한 부여를 실행합니다. 

다음 스니펫은 `/protected` 엔드포인트 GET 메소드를 보호하기 위해
단순 Express 애플리케이션에서 `APIStrategy`를 사용하는 방법을 보여줍니다. 

  ```JavaScript

  var express = require('express');
  var passport = require('passport');
  var APIStrategy = require('bluemix-appid').APIStrategy;

  passport.use(new APIStrategy());
  var app = express();
  app.use(passport.initialize());

  app.get('/protected', passport.authenticate('APIStrategy.STRATEGY_NAME', {session: false }),
      function(request, response){
          console.log("Securty context", request.securityContext)    
          response.send(200, "Success!");
      }
  );

  app.listen(process.env.PORT);
```
  {:pre}

`WebAppStrategy`를 사용하여 웹 애플리케이션 리소스를 보호할 수 있습니다. 

  ```JavaScript

  var express = require('express');
  var passport = require('passport');
  var WebAppStrategy = require('bluemix-appid').WebAppStrategy;
  ```
  {:pre}

자세한 정보는 <a href="https://github.com/ibm-cloud-security/appid-serversdk-nodejs" target="_blank">{{site.data.keyword.appid_short_notm}} Node.js GitHub 저장소 <img src="../../icons/launch-glyph.svg" alt="외부 링크 아이콘"></a>을 참조하십시오. 
