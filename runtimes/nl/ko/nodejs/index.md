---

copyright:
  years: 2015, 2016

---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}


# SDK for Nodejs
{: #nodejs_runtime}
*마지막 업데이트 날짜: 2016년 3월 16일*

{{site.data.keyword.Bluemix}}의 Node.js 런타임은 sdk-for-nodejs 빌드팩을 통해 제공됩니다.
sdk-for-nodejs 빌드팩은 Node.js 앱을 위한 완전한 런타임 환경을 제공합니다.
{: shortdesc}

sdk-for-nodejs 빌드팩은 애플리케이션의 루트 디렉토리에 **package.json** 파일이 있는 경우에 사용됩니다. 

## 스타터 애플리케이션
{: #starter_application}

{{site.data.keyword.Bluemix}}는 Node.js 스타터 애플리케이션을 제공합니다. Node.js 스타터 애플리케이션은 앱에 사용할 수 있는 템플리트를 제공하는 단순한 Node.js 앱입니다. 스타터 앱을 사용하여 시험해 볼 수 있으며 Bluemix 환경을 변경하고 변경사항을 푸시할 수 있습니다. 스타터 애플리케이션 사용에 대한 도움말은 [스타터 애플리케이션 사용](../../cfapps/starter_app_usage.html)을 참조하십시오. 

## 시작 명령
{: #starup_commmand}

Bluemix Node.js 애플리케이션에 대한 시작 명령을 지정하는 방법으로 **Procfile** 또는 **package.json** 파일을 사용할 것을 권장합니다. 

**Procfile**에서 시작 명령을 다음 양식으로 지정하십시오. 여기서 app.js는 애플리케이션의 시작 js 스크립트입니다.
```
web: node app.js
```
{: codeblock}

애플리케이션의 루트 디렉토리에 **Procfile**을 저장하십시오. 

**Procfile**이 없는 경우 IBM Bluemix Node.js 빌드팩은 **package.json** 파일에서 scripts.start 항목을 검사합니다. 다음 예에서도 app.js는 애플리케이션의 시작 js 스크립트입니다.
```
{
    ...   
    "scripts": {
      "start": "node app.js"
    }
}
```
{: codeblock}

시작 스크립트 항목이 **package.json**에 있는 경우 **Procfile**이 자동으로 생성됩니다. 자동 생성된 **Procfile**의 컨텐츠는 다음과 같습니다.
```
    web: npm start
```
{: codeblock}

**Procfile** 및 **package.json** 파일에 대한 자세한 정보는 [Node.js 애플리케이션을 위한 팁](https://docs.cloudfoundry.org/buildpacks/node/node-tips.html)을 참조하십시오.

## 로컬에서 Node.js 애플리케이션 실행을 위한 힌트
{: #hints}

로컬과 Bluemix 모두에서 Node.js 애플리케이션 실행을 용이하게 하려면 이 정보를 사용하십시오. 

다음 예에서는 **js** 파일의 소스 파트를 보여줍니다.
```
var port = (process.env.VCAP_APP_PORT || 3000);
var host = (process.env.VCAP_APP_HOST || 'localhost');
```
{: codeblock}

애플리케이션이 Bluemix에서 실행되는 경우 이 코드를 사용하여 VCAP_APP_HOST 및 VCAP_APP_PORT 환경 변수에 Bluemix 내부에 있고 앱이 수신 연결을 위해 청취하는 호스트와 포트 값을 포함시키십시오. 애플리케이션이 로컬에서 실행되는 경우 VCAP_APP_HOST 및 VCAP_APP_PORT가 정의되지 않으므로 **localhost**가 호스트로 사용되고 **3000**이 포트 번호로 사용됩니다. 이런 방식으로 작성하면 애플리케이션을 테스트 목적으로 실행하고 Bluemix에서는 추가 변경 없이 실행할 수 있습니다. 

## 앱 관리
{{site.data.keyword.Bluemix}}는 Node.js 앱을 관리하고 디버깅하는 몇 가지 유틸리티를 제공합니다. 전체 세부사항은 [앱 관리](../../manageapps/app_mng.html)를 참조하십시오. 

## 사용 가능한 버전
{: #available_versions}

{{site.data.keyword.Bluemix}}는 모든 [현재 사용 가능한 Node.js 런타임](http://nodejs.org/dist/)을 제공합니다. 이 중에서 IBM은 개선사항과 버그 수정사항이 포함된 버전을 제공합니다. 자세한 정보는 [Node.js 빌드팩의 최신 업데이트](../../runtimes/nodejs/updates.html)를 참조하십시오. 

IBM Node.js 빌드팩은 모든 IBM 런타임 버전을 캐싱합니다. 애플리케이션에서 IBM SDK for Node.js 런타임을 사용하는 경우 애플리케이션을 Bluemix에 푸싱할 때 애플리케이션 성능이 더 빨라집니다. 

**package.json** 파일의 **engines** 섹션에서 **node** 매개변수를 사용하여 실행하려는 Node.js 런타임 버전을 지정하십시오. 

Node.js에 번들된 버전이 아닌 다른 버전의 npm을 지정해야 하는 경우 **package.json** 파일의 **engines** 섹션에서 **npm** 매개변수를 사용하십시오.   

다음 예를 참조하십시오.

```
{
  "name": "myapp",
  "description": "this is my app",
  "version": "0.1",
  "engines": {
     "node": "4.2.4",
     "npm": "2.11.3"
  }
}
```
{: codeblock}

노드 버전은 항상 **package.json** 파일에 지정되어야 합니다. 이를 지정하지 않으면 최신 노드 버전이 사용됩니다.

## 구성 옵션
{: #configuration_options}

### NPM 스크립트
{: #npm_scripts}
NPM은 사용자 node_modules가 설치되기 전과 후에 적용되는 **preinstall** 및 **postinstall** 스크립트를 포함하여 스크립트를 실행할 수 있는 스크립팅 기능을 제공합니다. 전체 세부사항은 [npm-scripts](https://docs.npmjs.com/misc/scripts)를 참조하십시오. 

### 캐시 작동
{: #cache_behavior}
{{site.data.keyword.Bluemix}}는 노드 애플리케이션당 캐시 디렉토리를 유지보수하며, 이는 빌드 사이에서 지속됩니다. 캐시는 해결된 종속 항목을 저장하므로 이러한 항목은 앱이 배치될 때마다 다운로드 및 설치되지 않습니다. 예를 들어 myapp이 **express**에 종속된다고 가정합니다. myapp을 처음 배치할 때 **expess** 모듈이 다운로드됩니다. 이후에 myapp을 배치할 때는 **express**의 캐시된 인스턴스가 사용됩니다. 기본 동작은 NPM에서 설치한 모든 node_modules와 bower에서 설치한 bower_components를 캐시하는 것입니다. 

Node 빌드팩이 이전 빌드의 캐시를 사용할지 또는 무시할지를 판별하려면 NODE_MODULES_CACHE 변수를 사용하십시오. 기본값은 true입니다. 캐싱을 사용 안함으로 설정하려면 NODE_MODULES_CACHE를 false로 설정하십시오. 예를 들어 cf 명령행을 사용하는 경우 다음과 같습니다.
```
    $ cf set-env myapp NODE_MODULES_CACHE false
```
{: codeblock}

애플리케이션에 포함된 node_modules는 캐시되지 않음을 참고하십시오. 

최상위 레벨 **package.json**에서 **cacheDirectories** 배열(array)을 사용하여 캐시되는 모듈에 대해 세분화된 제어를 수행할 수 있습니다. **cacheDirectories** 요소가 **package.json**에 표시된 경우 **cacheDirectories** 배열에 있는 해당 모듈만 캐시됩니다. 다음 예에서는 node_modules와 bower_components만 캐시됩니다.
```
{
  "cacheDirectories": ["node_modules","bower_components"],
  ...
}
```
{: codeblock}

### FIPS 모드
{: #fips_mode}

Nodejs 빌드팩 버전 v3.2-20160315-1257 이상에서 [FIPS](https://en.wikipedia.org/wiki/Federal_Information_Processing_Standards)를 지원합니다. FIPS를 사용하려면 환경 변수 FIPS_MODE를 true로 설정하십시오.
예: 

```
    $ cf set-env myapp FIPS_MODE true
```
{: codeblock}

FIPS_MODE가 true일 때 **[MD5](https://en.wikipedia.org/wiki/MD5)를 사용하는 노드 모듈이 실패하게 됨**을 인지하는 것이 중요합니다. 예를 들면,
[Express](http://expressjs.com/) 모듈이 실패하게 됩니다. Expess 앱에서 [etag](http://expressjs.com/en/api.html)를 false로 설정하면
그 문제를 임시로 해결하도록 도울 수 있습니다. 예를 들면, 코드에서 다음과 같이 할 수 있습니다.
```
    app.set('etag', false);
```
{: codeblock}
자세한 정보는 이 [스택오버플로우 포스트](http://stackoverflow.com/questions/15191511/disable-etag-header-in-express-node-js)를
참조하십시오. 

앱에서 FIPS_MODE가 true인지 확인하려면 **process.versions.openssl**의 값을 확인하십시오. 예:
```
    console.log('ssl version is [' +process.versions.openssl +']');
```
{: codeblockd}

SSl 버전에 "fips"가 포함되어 있는 경우에는 앱이 FIPS 모드에서 실행 중입니다.    


## Node.js 빌드팩

Bluemix는 여러 버전의 Node.js 빌드팩을 제공합니다. 
* IBM 작성 **sdk-for-nodejs** 빌드팩은 Bluemix의 Node.js 애플리케이션에 사용되는 기본 빌드팩입니다. 
* **nodejs_buildpack**은 Cloud Foundry 커뮤니티에서 제공되는 외부 빌드팩입니다. 

**sdk-for-nodejs** 빌드팩은 Bluemix의 **nodejs_buildpack**에 우선합니다. 애플리케이션에 **sdk-for-nodejs** 대신 **nodejs_buildpack**을 사용하려면 사용자 빌드팩을 지정해야 합니다. 예를 들어 **cf push** 명령에서 -b 옵션을 사용하여 지정하십시오. 

일반적으로 현재 **sdk-for-nodejs** 빌드팩과 이전 레벨 버전이 사용 가능합니다. 사용 가능한 모든 빌드팩을 보려면 **cf buildpacks** 명령을 사용하십시오. 예: 
<pre>
      cf buildpacks
      Getting buildpacks...

      buildpack                                 position   enabled   locked   filename   

      sdk_for_nodejs                            2          true      false    buildpack_sdk-for-nodejs_v2.8-20151209-1403.zip   
      nodejs_buildpack                          5          true      false    nodejs_buildpack-cached-v1.5.0.zip   
      sdk-for-nodejs_v2_7-20151118-1003         17         true      false    buildpack_sdk-for-nodejs_v2.7-20151118-1003.zip
</pre>
{: codeblock}

# 관련 링크
## 일반
* [Node.js 빌드팩의 최신 업데이트](../../runtimes/nodejs/updates.html)
* [앱 관리](../../manageapps/app_mng.html)
* [Node.js](https://nodejs.org)
* [StrongLoop](https://strongloop.com)
