{:new_window: target="_blank"}
{:codeblock: .codeblock}

*마지막 업데이트 날짜: 2016년 1월 18일*

# Node.js 빌드팩의 최신 업데이트
{: #latest_updates}

Node.js 빌드팩의 최신 업데이트 목록입니다.

## 2015년 12월 16일: 업데이트된 Node.js 빌드팩 v2.8-20151209-1403 및 v3.0beta-20151211-2041 

이 Node.js 빌드팩 릴리스는 두 가지 버전, v2.8 및 v3.0beta로 제공됩니다. 이 두 버전 모두에는 다음 변경사항이 포함되어 있습니다.

모니터링 및 분석 서비스에 대한 버그 수정
IBM SDK for Node.js v4.2.3.0, v4.2.2.0, v1.2.0.8 및 v1.2.0.7(각각 커뮤니티 Node.js v4.2.3, v4.2.2, v0.12.9 및 v0.12.8 기반)에 대한 캐시된 런타임 포함
또한 v3.0beta에서 기본 Node.js 런타임이 v4.2.3으로 변경됨. 

IBM Node.js 빌드팩 v3.0beta는 Node.js v4.2.3을 기본 런타임으로 사용하여 Bluemix에서 기본이 아닌 빌드팩으로 릴리스되었습니다. 앱과 서비스가 Bluemix에서 계속 작동할 수 있도록 빌드팩의 베타 버전으로 애플리케이션을 푸시하십시오. 30일 이후에 v3가 기본 빌드팩이 됩니다.

v3.0beta로 애플리케이션을 푸시하려면 다음을 수행하십시오.

* 다음과 같이 'cf push' 명령에서 "-b" 옵션을 사용하십시오.
```
 cf push -b sdk-for-nodejs-v3beta
```
{: codeblock}
* 또는 manifest.yml 파일에서 "buildpack" 옵션을 사용하십시오.
```
buildpack: sdk-for-nodejs-v3beta
```
{: codeblock}

애플리케이션의 package.json에서 특정 버전의 Node.js를 구성한 경우
이와 같이 기본 런타임을 변경해도 애플리케이션에 영향을 미치지 않습니다. [사용 가능한
버전](index.html#available_versions)에서 설명한 대로 package.json의 engines.node 항목을 사용하여 애플리케이션을 실행할 Node.js의 버전을 항상 지정할 수 있습니다. 

## 2015년 11월 23일: 업데이트된 Node.js 빌드팩 v2.7-20151118-1003

2.7과 함께 Node.js용 IBM SDK의 버전 4.2.1.0이 포함되었습니다(Node v4.2.1 LTS 기반).
이 버전은 기본값이 아니지만 사용하도록 지정할 수 있습니다. 이 버전이 이전에 사용 가능했던 open-source
빌드를 대체합니다. 서비스 확장 프레임워크에 대한 버그도 약간
수정되었습니다.

## 2015년 10월 19일: 업데이트된 Node.js 빌드팩 v2.6.1-20151015-1326

Node.js v2.6.1에서는 [StrongPM 앱
관리 핸들러](https://developer.ibm.com/bluemix/2015/10/15/strongloop-devops-on-bluemix/) 및 더 일관된 NPM 버전에 버그 수정을 도입합니다.

## 2015년 10월 15일: 업데이트된 Node.js 빌드팩 v2.6-20151006-1309

Node.js buildpack의 이 릴리스는 앱 관리 기능에 [StrongLoop Process Manager](https://strong-pm.io)를 통합한 특징을 지니고 있습니다.
자세한 정보는 블로그 게시물 [StrongLoop DevOps for Node.js Applications on Bluemix](https://developer.ibm.com/bluemix/2015/10/15/strongloop-devops-on-bluemix/)를 참조하십시오.

## 2015년 6월 15일: 업데이트된 Node.js 빌드팩 v2.0-20150608-1503

이 릴리스에서는 CF 커뮤니티로부터 가져온 여러 가지 새로운 기능과 함께 제공되는 최신 [CF 커뮤니티
Node.js 빌드팩](https://github.com/cloudfoundry/nodejs-buildpack)과 Node.js 빌드팩을 동기화했습니다.또한 Node.js 빌드팩의 앱 관리 기능을 쇄신하여 shell, node-inspector, Bluemix Live Sync 등의 유틸리티를 사용할 수 있게 합니다. 자세한 내용은 [앱 관리](../../manageapps/app_mng.html)를 참조하십시오. 

## 2015년 5월 5일: 업데이트된 Node.js 빌드팩 v1.17-20150429-1033

* 이제 Node.js 빌드팩에 [IBM SDK for Node.js v0.12.1](https://developer.ibm.com/node/sdk/)이 제공됩니다. 
* 애플리케이션이 package.json 파일에 런타임을 지정하지 않으면 이제 v0.10.x 대신 v0.12.1을 사용하여 앱이 시작됩니다. 이전 버전을 사용해야 하는 경우에는 아래와 같이 package.json에 v0.10.x를 지정하십시오. ```
   "engines": {
"node": "0.10.x"
}
```
{: codeblock}
* v0.12.1에는 다음과 같은 알려진 문제가 있습니다.
   * Bluemix Live Sync에서 제공하는 Debug Tools 기능을 사용할 때 "일시중단" 기능이 중단됩니다.
   * MQ Light 서비스를 위해 사용되는 mqlight 모듈은 v0.12.x에서 지원되지 않습니다.

* 다음과 같은 여러 가지 보안 취약점이 해결되었습니다.
  * IBM SDK for Node.js에 영향을 주는 OpenSSL의 취약점 해결. 자세한 내용은 [security bulletin](http://www-01.ibm.com/support/docview.wss?uid=swg21701494)에 설명되어 있습니다. 
  * IBM SDK for Node.js에 영향을 주는 RC4 Stream Ciphe의 취약점 해결. 자세한 내용은 [security bulletin](http://www-01.ibm.com/support/docview.wss?uid=swg21882778)에 설명되어 있습니다. 

##  2015년 4월 2일: 업데이트된 Node.js 빌드팩 v1.15-20150331-2231

* 이제 Node.js 빌드팩은 재배치하지 않고도 데스크탑에서 개발할 수 있는 것처럼 Bluemix에서 빠른 개발을 도와주는 세 가지 새로운 기능을 포함합니다.
  * Desktop Sync: (Windows) 데스크탑 트리를 클라우드 기반의 프로젝트 작업공간으로 동기화합니다. 
  * Live Edit: Bluemix에서 실행 중인 Node.js 애플리케이션에 대한 변경사항을 작성하고 브라우저에서 해당 변경사항을 즉시 테스트할 수 있습니다. 
  * Debug: 사용자 환경을 분석하고 디버그합니다! 노드 검사기 디버거를 사용하여 동적으로 코드 편집, 중단점 삽입, 코드 스텝 스루, 런타임 다시 시작 등을 수행할 수 있습니다.
  * 자세한 정보는 [앱 관리](../../manageapps/app_mng.html#Utilities)를 참조하십시오. 
* [Cloud Foundry의 Node.js 빌드팩](https://github.com/cloudfoundry/nodejs-buildpack)에서 최신 변경사항을 가져왔습니다.
따라서 커뮤니티에서 작성한 여러 가지 버그 수정과 개선사항을 제공합니다.
* 이제 Node.js 빌드팩에 [IBM SDK for Node.js v1.1.0.13](https://developer.ibm.com/node/sdk/)이 제공됩니다. 

## 2015년 1월 5일: 업데이트된 Node.js 빌드팩 v1.9.1-20141208-1221

* 이제 이 Node.js 빌드팩은 동적 로그 설정을 지원합니다. 애플리케이션이 로깅을 위해 log4js, bunyan 또는 ibmbluemix 모듈을 사용 중인 경우 개발자는
이 기능을 사용하여 애플리케이션의 로그 레벨을 즉석에서 변경할 수 있습니다.
* 이제 Node.js 빌드팩에 [IBM SDK for Node.js v0.10.33](https://developer.ibm.com/node/sdk/)이 제공됩니다. 이 빌드팩에는 POODLE 문제에 대한 수정사항이 포함되어 있습니다.

## 2014년 10월 23일: 업데이트된 Node.js 빌드팩 v1.6-20141013-1736

* 이제 Node.js 빌드팩에 [IBM SDK for Node.js v1.1.0.8](https://developer.ibm.com/node/sdk/)이 제공됩니다. 이는 애플리케이션 v0.10.32에 안정적인 최신 Node.js 런타임을 지정하면 전체 지원되는 IBM Node.js 런타임을 사용할 수 있다는 의미입니다. 이번 최신 SDK에는 서비스 거부(DoS)를 일으키는
임베디드 qs 모듈 문제의 수정사항이 포함되어 있습니다.
또한 npm 모듈의 업데이트된 버전과 http 및 url 모듈의 다른 개선사항도
포함합니다. 자세한 내용은 [v0.10.32 변경 로그](https://raw.githubusercontent.com/joyent/node/v0.10.32/ChangeLog)를 참조하십시오. 
* 배치하는 동안 고객 애플리케이션에 올바르지 않은
index.html 파일을 추가하는 버그에 대한 수정사항도
포함되어 있습니다.

## 2014년 9월 30일: 업데이트된 Node.js 빌드팩 v1.4-20140908-1746

* 이제 Node.js 빌드팩에 [IBM SDK for Node.js v1.1.0.7](https://developer.ibm.com/node/sdk/)이 제공됩니다. 이는 애플리케이션 v0.10.31에 안정적인 최신 Node.js 런타임을 지정하면 전체 지원되는 IBM Node.js 런타임을 사용할 수 있다는 의미입니다. 전체 지원되는 Node.js 런타임을 사용하는 고객은 IBM 제품과 동일한 수준의 지원이 보장되므로 안정적으로 이 런타임에서 빌드할 수 있습니다. 
* 빌드팩에 향상된 서비스 프레임워크가 포함되어 있습니다. 특히,
Monitoring and Analytics 서비스를 바인딩할 때 더 효과적이고 장애 발생 시
추가 진단 정보를 제공합니다.

## 2014년 8월 28일: 업데이트된 Node.js 빌드팩 v1.3-20140821-1143

* 이제 최신 Node.js 빌드팩에 IBM SDK for Node.js v1.1.0.6이 제공됩니다. 이는 애플리케이션 v0.10.30에 안정적인 최신 Node.js 런타임을 지정하면 전체 지원되는 IBM Node.js 런타임을 사용할 수 있다는 의미입니다. 이 런타임은 [ V8 메모리 손상 취약성](http://blog.nodejs.org/2014/07/31/v8-memory-corruption-stack-overflow)을 수정해 줍니다.
* Monitoring and Analytics 서비스 확장에 대한 개선 기능과 버그 수정사항도
포함되어 있으므로 서비스를 통해 성능 및 오류 조건을
진단할 수 있습니다. 

## 2014년 6월 29일: 업데이트된 Node.js 빌드팩 v1.1-20140717-1447

이제 Node.js 빌드팩에 IBM SDK for Node.js v1.1.0.5가 제공됩니다. 이는 애플리케이션 v0.10.29에 안정적인 최신 Node.js 런타임을 지정하면 전체 지원되는 IBM Node.js 런타임을 사용할 수 있다는 의미입니다. [여기](https://developer.ibm.com/node/sdk/)에서 IBM Node.js SDK에 대해 자세히 알아보십시오. 
