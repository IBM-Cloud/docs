{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}

*마지막 업데이트 날짜: 2016년 1월 12일*

# Node.js 런타임
{: #nodejs_runtime}

{{site.data.keyword.Bluemix}}의 Node.js 런타임은 sdk-for-nodejs 빌드팩 기반입니다.
sdk-for-nodejs 빌드팩은 Node.js 앱을 위한 전체 런타임 환경을 제공합니다.
{: shortdesc}

애플리케이션의 루트 디렉토리에 **package.json** 파일이 있는 경우 Node.js 빌드팩이 사용됩니다. 

## 스타터 애플리케이션
{: #starter_application}

{{site.data.keyword.Bluemix}}는 Node.js 스타터 애플리케이션을 제공합니다. Node.js 스타터 애플리케이션은 단순 Node.js 앱으로 사용자가 앱에 사용할 수 있는 템플리트를 제공합니다. 스타터 앱을 사용해 보고 필요한 변경사항을 작성하고 이를 Bulemix 환경에 푸시할 수 있습니다. 스타터 애플리케이션 사용에 대한 지원이 필요한 경우 [스타터 애플리케이션 사용](../../cfapps/starter_app_usage.html)을 참조하십시오. 

## 스타트업 명령
{: #starup_commmand}

Bluemix Node.js 애플리케이션에 대한 시작 명령을 지정하는 경우 **Procfile** 또는 **package.json** 파일을 사용하는 것이 좋습니다. 

다음과 같은 양식으로 **Procfile**에서 스타트업 명령을 지정하십시오. 여기서 app.js는 애플리케이션의
스타트업 js 스크립트입니다. ```
web: node app.js```
{: codeblock}

애플리케이션의 루트 디렉토리에 **Procfile**을 저장하십시오.

**Procfile**이 없는 경우 IBM Bluemix Node.js 빌드팩은 **package.json** 파일에서 scripts.start 항목이 있는지 확인합니다. 아래 예에서도 app.js는 애플리케이션의 js 스타트업
스크립트입니다.```
{
  ...   
"scripts": {

    "start": "node app.js"
}
}
```
{: codeblock}

시작 스크립트 항목이 **package.json**에 있으면 **Procfile**이 자동으로 생성됩니다.
자동 생성된 **Procfile**의 컨텐츠는 아래와 같습니다.
```
web: npm start```
{: codeblock}

**Procfile** 및 **package.json** 파일에 대한 자세한 정보는 [Tips for Node.js Applications](https://docs.cloudfoundry.org/buildpacks/node/node-tips.html)의 내용을 참조하십시오. 

## Node.js 애플리케이션의 로컬 실행에 대한 힌트
{: #hints}

이 정보를 사용하여 Node.js 애플리케이션을 로컬에서뿐만 아니라 Bluemix에서 쉽게 실행할 수 있습니다. 

다음 예제는 **js** 파일에 대한 소스의 일부를 보여줍니다.
```
var port = (process.env.VCAP_APP_PORT || 3000);
var host = (process.env.VCAP_APP_HOST || 'localhost');
```
{: codeblock}

이 코드를 사용하여 애플리케이션을 Bluemix에서 실행 중인 경우, VCAP_APP_HOST 및 VCAP_APP_PORT 환경 변수에는 Bluemix의 내부 요소인 호스트 및 포트 값이 포함되어 있으며 이를 통해 앱이 수신 연결을 청취합니다. 애플리케이션이 로컬에서 실행되는 경우에는 VCAP_APP_HOST 및 VCAP_APP_PORT가 정의되어 있지 않으므로 **localhost**가 호스트로 사용되고 **3000**이 포트 번호로 사용됩니다. 이렇게 작성된 경우 애플리케이션을 테스트 목적으로 로컬에서 실행하고 추가 변경사항 없이 Bluemix에서 실행할 수 있습니다. 

## App Management
{{site.data.keyword.Bluemix}}는 Node.js 앱의 관리 및 디버깅을 위한 다양한 유틸리티를 제공합니다. 자세한 내용은 [앱 관리](../../manageapps/app_mng.html)를 참조하십시오. 

## 사용 가능한 버전
{: #available_versions}

{{site.data.keyword.Bluemix}}는 [현재 사용 가능한 Node.js 런타임](http://nodejs.org/dist/)을
모두 제공합니다. IBM은 개선사항과 버그 수정을 포함하는 버전을 제공합니다. 자세한 정보는 [Node.js 빌드팩의 최신 업데이트](updates.html)를 참조하십시오. 

IBM Node.js 빌드팩은 모든 IBM 런타임 버전을 캐시합니다. 따라서 애플리케이션에서 IBM SDK for Node.js 런타임을 사용하는 경우 애플리케이션이 Bluemix로 푸시되면 애플리케이션 성능이 더 빨라집니다. 

**package.json** 파일의 **engines** 섹션에 있는 **node** 매개변수를 사용하여 실행하려는 Node.js 런타임의 버전을 지정하십시오. 

Node.js에 번들로 포함된 버전 외에 npm 버전을 지정해야 하는 경우 **package.json** 파일의 **engines** 섹션에 있는 **npm** 매개변수를 사용하십시오.   

다음 예제를 참조하십시오. 

```
{
  "name": "myapp",
  "description": "this is my app",
  "version": "0.1",
  "engines": {
     "node": "4.2.4"
     "npm": "2.11.3"
  }
}
```
{: codeblock}

노드 버전은 항상 **package.json** 파일에 지정되어 있어야 합니다. 지정되지 않은 경우 최신 노드 버전이 사용됩니다. 

## 구성 옵션
{: #configuration_options}

### NPM 스크립트
{: #npm_scripts}
NPM은 node_modules가 설치되는 전후에 적용되는 **preinstall** 및 **postinstall** 스크립트를 포함하여 스크립트를 실행할 수 있는 스크립팅 기능을 제공합니다. 자세한 내용은 [npm-scripts](https://docs.npmjs.com/misc/scripts)를 참조하십시오. 

### 캐시 동작
{: #cache_behavior}
{{site.data.keyword.Bluemix}}는 빌드 간에 지속되는 노드 애플리케이션당 하나의 캐시 디렉토리를 유지보수합니다. 캐시는 해결된 종속 항목을 저장하므로 앱이 배치될 때마다 종속 항목이 다운로드되거나 설치되지 않습니다. 예를 들어, myapp은 **express**에 의존한다고 가정합니다. 처음으로 myapp이 배치되면 **expess** 모듈이 다운로드됩니다. 그 다음에 myapp이 배치되는 경우 **express**의 캐시된 인스턴스가 사용됩니다. 

Node 빌드팩이 이전 빌드의 캐시를 사용하거나 무시하는지를 판별하려면 NODE_MODULES_CACHE 변수를 사용하십시오. 기본값은 true입니다. 캐싱을 사용 안함으로 설정하려면 다음 예제와 같이 cf 명령행을 통해 NODE_MODULES_CACHE를 false로 설정하십시오.
```
cf set-env myapp NODE_MODULES_CACHE false
```
{: codeblock}

애플리케이션에 포함되어 있는 node_modules는 캐시되지 않습니다. 

상위 레벨 **package.json**의 **cacheDirectories** 배열을 사용하여 캐시되는 모듈을 미세하게 제어할 수 있습니다. **cacheDirectories** 요소가 **package.json**에 있는 경우 **cacheDirectories** 배열에 있는 모듈만 캐시됩니다. 다음 예제에서 node_modules 및 bower_components만 캐시됩니다.
```
{
  "cacheDirectories": ["node_modules","bower_components"],
  ...
}
```
{: codeblock}

## Node.js 빌드팩

Bluemix는 Node.js 빌드팩의 여러 버전을 제공합니다. 
* IBM 작성 **sdk-for-nodejs** 빌드팩은 Bluemix의 Node.js 애플리케이션에 사용되는 기본 빌드팩입니다. 
* **nodejs_buildpack**은 Cloud Foundry 커뮤니티에서 제공하는 외부 빌드팩입니다. 

**sdk-for-nodejs** 빌드팩은 Bluemix의 **nodejs_buildpack**보다 우선권을 갖습니다. **sdk-for-nodejs** 빌드팩 대신에 **nodejs_buildpack**을 애플리케이션과 함께 사용하려는 경우 **cf push** 명령에 -b 옵션을 사용하여 사용자 빌드팩을 지정해야 합니다. 

일반적으로 현재 **sdk-for-nodejs** 빌드팩 및 이전 레벨 버전을 사용할 수 있습니다. 사용 가능한 모든 빌드팩을 보려면 **cf buildpacks** 명령을 사용하십시오. 예를 들어, 다음과 같습니다. ```
cf buildpacks
Getting buildpacks...

buildpack                      position          enabled          locked          filename	
   
...
sdk_for_nodejs                            2          true      false    buildpack_sdk-for-nodejs_v2.8-20151209-1403.zip   
nodejs_buildpack                          5          true      false    nodejs_buildpack-cached-v1.5.0.zip   
sdk-for-nodejs_v2_7-20151118-1003         17         true      false    buildpack_sdk-for-nodejs_v2.7-20151118-1003.zip
```
{: codeblock}


## 관련 링크
{: #related_links}
* [Node.js 빌드팩의 최신 업데이트](updates.html)
* [App Management](../../manageapps/app_mng.html)
* [Node.js](https://nodejs.org)
* [StrongLoop](https://strongloop.com)
