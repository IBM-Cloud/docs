---

copyright:
  years: 2015, 2017
lastupdated: "2017-03-23"

---

{:new_window: target="_blank"}
{:codeblock: .codeblock}

# SDK for Nodejs 빌드팩의 최신 업데이트
{: #latest_updates}

sdk-for-nodejs 빌드팩의 최신 업데이트 목록

## 2017년 3월 10일: 업데이트된 Node.js 빌드팩 v3.11
이 릴리스의 빌드팩은 IBM SDK for Node.js 런타임 버전 0.10.47, 0.10.48, 0.12.17, 0.12.18, 4.7.3, 4.8.0, 6.9.5 및 6.10.0을 지원합니다. 현재 기본 버전은 4.8.0입니다.

새 런타임 외에 이 릴리스에는 devconsole UI를 사용하는 쉘 앱 관리 핸들러를 사용할 때 발생한 버그에 대한 수정사항이 포함됩니다. 또한 이 빌드팩은 Monitoring and Analytics 서비스에 대한 자동 구성 작동 방법을 변경합니다. 무료 사용제를 사용하는 애플리케이션에는 더 이상 로그 기능이 추가되지 않습니다. 이는 logmet으로 대체됩니다.

## 2017년 1월 20일: 업데이트된 Node.js 빌드팩 v3.10
이 릴리스의 빌드팩은 IBM SDK for Node.js 런타임 버전 0.10.47, 0.10.48, 0.12.17, 0.12.18, 4.7.0, 4.7.2, 6.9.2 및 6.9.4를 지원합니다. 현재 기본 버전은 4.7.2입니다.

애플리케이션 시작을 위한 "npm start"가 호출되지 않는 경우의 버그에 대한 수정사항이 포함됩니다.

## 2016년 11월 17일: 업데이트된 Node.js 빌드팩 v3.9
이 릴리스의 빌드팩은 IBM SDK for Node.js 런타임 버전 0.10.47, 0.10.48, 0.12.16, 0.12.17, 4.6.1, 4.6.2, 6.7.0 및 6.9.1을 지원합니다. 현재 기본 버전은 4.6.2입니다.

Node.js v6가 2016년 10월 18일에 LTS 상태로 승격되었으며 곧 빌드팩의 기본 런타임이 됩니다. Node.js v0.10이 2016년 10월 31일에 종료되었으며 빌드팩에 더 이상 포함되지 않습니다. 세부사항은 [Node.js version long-term support and the SDK for Node.js buildpack](https://www.ibm.com/blogs/bluemix/2016/11/node-version-support-and-sdk-buildpack/)을 참조하십시오.

Node.js v6와 함께 사용되는 추적 및 검사기 앱 관리 핸들러에 영향을 주는 버그가 이 릴리스에서 해결되었습니다. Node.js v6의 검사기 기능 통합으로 인해 검사기 핸들러가 변경되는 방식에 대한 자세한 정보는 [Liberty 및 Node.js 앱 관리](/docs/manageapps/app_mng.html#inspector)를 참조하십시오.

## 2016년 10월 7일: 업데이트된 Node.js 빌드팩 v3.8-20161006-1211
이 릴리스의 빌드팩은 IBM SDK for Node.js 런타임 버전 0.10.46, 0.10.47, 0.12.15, 0.12.16, 4.5.0, 4.6.0, 6.6.0, 6.7.0을 지원합니다. 현재 기본 버전은 4.6.0입니다.

이 릴리스에는 새 런타임뿐만 아니라 빌드팩 버그 수정사항이 포함되어 있습니다. v3.7-20160826-1101 릴리스 업데이트에서 언급된 Node.js 6.x와 개발 모드를 사용하는 경우 알려진 문제점의 수정사항이 그 중 하나입니다. 또한 이 릴리스는 [Cloud Foundry Node.js 빌드팩 v1.5.20](https://github.com/cloudfoundry/nodejs-buildpack/tree/v1.5.20)과 동기화됩니다.

## 2016년 8월 26일: 업데이트된 Node.js 빌드팩 v3.7-20160826-1101
이 릴리스의 빌드팩은 IBM SDK for Node.js 런타임 버전 0.10.45, 0.10.46, 0.12.14, 0.12.15, 4.4.7, 4.5.0, 6.2.2 및 6.4.0을 지원합니다. 현재 기본 버전은 4.5.0입니다.

이 릴리스는 버그 수정([Cloud Foundry의 Node.js 빌드팩 1.5.18](https://github.com/cloudfoundry/nodejs-buildpack/tree/v1.5.18)의 버그 수정 포함)을 포함합니다. 

이 릴리스에서는 [Bluemix Node.js 빌드팩 v3.3 – FIPS 모드 및 그 외](https://developer.ibm.com/bluemix/2016/05/05/node-buildpack-update-fips-mode/)에 공지된 대로 strongpm 앱 관리 핸들러에 대한 지원이 제거되었습니다. 

Node.js 6.x와 [개발 모드](/docs/manageapps/app_mng.html#devmode)를 사용할 때 알려진 문제가 있음에 주의하십시오. 개발 모드를 사용하려면 먼저 임시 해결책으로서 개발 모드를 사용 가능하게 설정한 후 애플리케이션을 다시 스테이징해야 합니다. 

## 2016년 7월 22일: 업데이트된 Node.js 빌드팩 v3.6-20160715-0749
이 릴리스의 빌드팩은 IBM SDK for Node.js 런타임 버전 0.10.45, 0.10.46, 0.12.14, 0.12.15, 4.4.6, 4.4.7, 6.2.1 및 6.2.2를 지원합니다. 현재 기본 버전은 4.4.7입니다.

이 릴리스에는 연합 로그인을 지원하는 업데이트된 앱 관리 프록시가 포함됩니다.

다음 보안 취약점에 대한 수정사항이 포함되었습니다. 
* [CVE-2016-1669](http://www-01.ibm.com/support/docview.wss?uid=swg21986383)

## 2016년 6월 22일: 업데이트된 Node.js 빌드팩 v3.5-20160609-1608

이 릴리스의 빌드팩은 IBM SDK for Node.js 런타임 버전 4.4.5 및 6.2.0을 추가합니다. 기본 버전은 4.4.5입니다. 

이 릴리스에서는 [Bluemix Node.js 빌드팩 v3.3 – FIPS 모드 및 그 외](https://developer.ibm.com/bluemix/2016/05/05/node-buildpack-update-fips-mode/)의 발표에 따라 오래된 런타임 버전에 대한 지원이 제거되었습니다. 이제 빌드팩은 0.10.44, 0.10.45, 0.12.13, 0.12.14, 4.4.4, 4.4.5, 6.1.0, 6.2.0을 지원합니다.

이 릴리스는 [Cloud Foundry의 Node.js 빌드팩 1.5.14](https://github.com/cloudfoundry/nodejs-buildpack/tree/v1.5.14)에서 버그 수정을 포함합니다. 

## 2016년 5월 20일: 업데이트된 Node.js 빌드팩 v3.4-20160518-1653

이 릴리스의 빌드팩은 IBM SDK for Node.js 런타임 버전 0.10.45, 0.12.14, 4.4.4, 6.0.0, 6.1.0을 추가합니다. 현재 기본 버전은 4.4.4입니다.

다음 보안 취약점에 대한 수정사항이 포함되었습니다. 
* [CVE-2015-8855](http://www-01.ibm.com/support/docview.wss?uid=swg21982852)
* [CVE-2016-2108 CVE-2016-2107 CVE-2016-2105 CVE-2016-2106 CVE-2016-2109 CVE-2016-2176 ![외부 링크 아이콘](../../icons/launch-glyph.svg "외부 링크 아이콘")](https://www.openssl.org/news/secadv/20160503.txt)

npm v3 및 앱 관리 검사기 유틸리티와 관련하여 알려진 문제가 있음을 주의하십시오. npm 3.8.6은 6.0.0 및 6.1.0 런타임에서 기본 기능입니다.  6.x 런타임 및 검사기 유틸리티를 사용하려면 임시 해결책으로 package.json에 2.x npm 버전을 지정해야 합니다.

## 2016년 4월 29일: 업데이트된 Node.js 빌드팩 v3.3-20160428-1409

이 릴리스의 빌드팩은 IBM SDK for Node.js 런타임 버전 0.10.44, 0.12.13, 4.4.0, 4.4.1, 4.4.2, 4.4.3을 추가합니다. 현재 기본 버전은
4.4.3입니다.
4.3.1 이상의 경우, 이제 사용자의 앱에 `FIPS_MODE=true` 환경 변수를 설정하여 FIPS 사용 버전의 런타임을 사용하는 것이 가능합니다. 

업데이트된 빌드팩과 새 런타임 버전에는 보안 취약점에 대한 수정사항도 포함되어 있습니다. 
* [CVE-2016-2515](http://www-01.ibm.com/support/docview.wss?uid=swg21977578)
* [CVE-2016-2537](http://www-01.ibm.com/support/docview.wss?uid=swg21977578)
* [CVE-2016-3956](http://www-01.ibm.com/support/docview.wss?uid=swg21980827)

업데이트된 빌드팩에는 여러 개의 버그에 대한 수정사항도 포함되어 있습니다. 
* 이제 요청된 범위와 일치하는 것이 사용 가능한 경우 IBM SDK for Node.js 빌드가 항상 사용됩니다. 이전에는 4.x 런타임 버전의 경우에만 적용되었습니다. 
* 이제 앱 관리 검사기 유틸리티가 4.x 런타임 버전에서 작동하게 됩니다. 
* strongpm 앱 관리 유틸리티에서 회귀가 수정되었습니다. 

## 2016년 3월 18일: 업데이트된 Node.js 빌드팩 v3.2-20160315-1257

이 릴리스의 빌드팩은 기본 IBM SDK for Node.js 런타임을 버전 4.3.0에서 4.3.2로 변경합니다. 또한 IBM SDK for Node.js 버전 0.10.43, 0.12.12 및 4.3.1을 포함합니다. 이러한 최근 Node.js 버전을 사용하여 몇 가지 보안 취약점에 대한 수정사항을 가져와야 합니다. 

## 2016년 3월 4일: 업데이트된 Node.js 빌드팩 v3.1-20160222-1123

이 릴리스의 빌드팩은 기본 IBM SDK for Node.js 런타임을 버전 4.2.4에서 4.3.0으로 변경합니다. 또한 IBM SDK for Node.js 버전 0.10.42, 0.12.10 및 4.2.6을 포함합니다. 이러한 최근 Node.js 버전을 사용하여 몇 가지 보안 취약점에 대한 수정사항을 가져와야 합니다. 

## 2016년 2월 4일: 업데이트된 Node.js 빌드팩 v3.0-20160125-1224

이 릴리스는 [Cloud Foundry 커뮤니티 Node.js](https://github.com/cloudfoundry/nodejs-buildpack) 빌드팩과 완전히 동기화됩니다. 커뮤니티 변경사항을 비롯하여 스테이징 시간을 줄이기 위한 최적화, 앱 관리 기능의 업데이트 및 특정 기본값에 대한 수정도 포함됩니다. 

* 빌드팩 업데이트:

  * Node.js v4.2.4(IBM SDK for Node.js 버전 4)가 Bluemix의 기본 런타임이 됩니다(v0.12.9 대체). 이 변경으로 인해 특정한 애플리케이션 버전을 지정하지 않은 경우 애플리케이션이 다르게 작동할 수 있습니다. Bluemix 애플리케이션의 Node.js 버전을 지정하는 방법에 대해 알아보려면 [Node.js 런타임](index.html) 문서를 참조하십시오. 

  * 기본적으로 NODE_ENV가 *production*으로 설정됩니다. 이 변경으로 인해 몇 가지 노드 종속 항목이 다르게 작동할 수 있습니다. 예를 들어 Express 프레임워크가 웹 브라우저에서 더 이상 결함 엔드포인트에 대한 스택 추적을 리턴하지 않고 대신 *내부 서버 오류*를 표시합니다. NPM_CONFIG_PRODUCTION이 *true*로 설정되면 NPM이 npm 설치 단계의 subshell 스크립트에 대해서만 NODE_ENV를 *production*으로 설정합니다. 이 기능을 통해 사용자가 애플리케이션 런타임에 대해 NODE_ENV를 *development*와 같은 다른 값으로 설정할 수 있습니다. 명확하게 하기 위해 npm 스크립트에서 **NODE_ENV=production** 메시지를 확인합니다.

  * Monitoring and Analytics 서비스에 대한 버그 수정사항이 포함됩니다. 

* 캐싱 업데이트:

  * 캐시를 사용 안함으로 설정한 경우(NODE_MODULES_CACHE=false) 빌드팩이 모듈/컴포넌트를 캐시하려고 시도하지 않습니다. 이전에는 이 설정을 사용하여 캐시가 팝되지 않도록 설정했지만 이후의 배치에서 설치된 모듈이 여전히 캐시되었습니다. 이제 캐시가 팝되지도 않고 캐시를 저장하려고 시도하지도 않습니다. 

  * node_modules 뿐 아니라 Bower_components도 기본적으로 캐시됩니다. 

* 기타 업데이트:

  * gulp, bower 및 angular와 같이 누락된 종속 항목에 대해 도움이 되는 경고가 추가되었습니다.

  * 발견 스크립트가 빌드팩 버전 정보로 업데이트됩니다.

  * Bluemix에서 메모리 판별이 정확하지 않아서 처음에 커뮤니티에서 소개된 클러스터링 권장사항(WEB_CONCURRENCY)이 제거됩니다. 


## 2015년 12월 16일: 업데이트된 Node.js 빌드팩 v2.8-20151209-1403 및 v3.0beta-20151211-2041

이 릴리스의 Node.js 빌드팩은 두 버전 v2.8 및 v3.0beta와 함께 제공됩니다. 두 버전 모두에 다음 변경사항이 포함되어 있습니다.

Monitoring and Analytics 서비스에 대한 버그 수정
IBM SDK for Node.js v4.2.3.0, v4.2.2.0, v1.2.0.8, v1.2.0.7(커뮤니티 버전 Node.js v4.2.3, v4.2.2, v0.12.9, v0.12.8을 기반으로 함)에 대한 캐시된 런타임을 포함합니다..
또한 v3.0beta에서 기본 Node.js 런타임이 v4.2.3으로 변경되었습니다. 

이제, IBM Node.js 빌드팩 v3.0beta는 기본 런타임 Node.js v4.2.3과 함께 Bluemix의 기본이 아닌 빌드팩으로 릴리스됩니다. 사용자 앱과 서비스가 계속해서 Bluemix에서 작동되도록 하려면 이 베타 버전의 빌드팩을 사용하여 사용자 애플리케이션을 푸시하십시오. 30일 이후 v3가 기본 빌드팩이 됩니다.

v3.0beta를 사용하여 사용자 애플리케이션을 푸시하려면 다음을 수행하십시오. 
* "-b" 옵션을 'cf push' 명령에서 사용하십시오. 

```
        cf push -b sdk-for-nodejs-v3beta
```
{: codeblock}

* 또는 manifest.yml 파일에서 "buildpack" 옵션을 사용하십시오. 

```
        buildpack: sdk-for-nodejs-v3beta
```
{: codeblock}

애플리케이션의 package.json에 특정 버전의 Node.js를 구성한 경우에는 기본 런타임에 대한 이러한 변경이 애플리케이션에 영향을 미치지 않습니다. 

**참고:** [사용 가능한 버전](index.html#available_versions)에서 설명된 대로 package.json의 engines.node를 사용하여 애플리케이션을 실행하도록 Node.js 버전을 항상 지정할 수 있습니다. 

## 2015년 11월 23일: 업데이트된 Node.js 빌드팩 v2.7-20151118-1003

2.7에서는 IBM SDK for Node.js 버전 4.2.1.0(Node v4.2.1 LTS를 기반으로 함)이 포함됩니다. 이는 기본값이 아니지만 사용하도록 지정할 수 있습니다. **참고:** 이 버전은 이전에 사용 가능했던 오픈 소스 필드를 대체합니다. 또한 서비스 확장 프레임워크에 대한 약간의 버그 수정사항을 작성했습니다.

## 2015년 10월 19일: 업데이트된 Node.js 빌드팩 v2.6.1-20151015-1326

Node.js v2.6.1은 [StrongPM 앱 관리 핸들러](https://developer.ibm.com/bluemix/2015/10/15/strongloop-devops-on-bluemix/)와 더 일치하는 NPM 버전에 대한 버그 수정사항을 소개합니다. 

## 2015년 10월 15일: 업데이트된 Node.js 빌드팩 v2.6-20151006-1309

이 릴리스의 Node.js 빌드팩은 앱 관리 기능에 대한 [StrongLoop Process Manager ![외부 링크 아이콘](../../icons/launch-glyph.svg "외부 링크 아이콘")](https://strong-pm.io) 통합을 제공합니다. 자세한 정보는 블로그 게시물 [StrongLoop DevOps for Node.js Applications on Bluemix](https://developer.ibm.com/bluemix/2015/10/15/strongloop-devops-on-bluemix/)를 참조하십시오.

## 2015년 6월 15일: 업데이트된 Node.js 빌드팩 v2.0-20150608-1503

이 릴리스에서는 Node.js 빌드팩이 최신 [CF 커뮤니티 Node.js 빌드팩](https://github.com/cloudfoundry/nodejs-buildpack)과 동기화되었습니다. 이 빌드팩은 커뮤니티의 몇 가지 새로운 기능과 함께 제공됩니다.
또한 Node.js 빌드팩에서 앱 관리 기능을 개선하였으며 이로 인해 shell, node-inspector, Bluemix Live Sync 등의 유틸리티를 사용할 수 있게 되었습니다. 세부사항은 [앱 관리](/docs/manageapps/app_mng.html)를 참조하십시오. 

## 2015년 5월 5일: 업데이트된 Node.js 빌드팩 v1.17-20150429-1033

* 이제 Node.js 빌드팩은 [IBM SDK for Node.js v0.12.1](https://developer.ibm.com/node/sdk/)과 함께 제공됩니다.
* 애플리케이션이 해당 package.json 파일에서 런타임을 지정하지 않은 경우 사용자 앱은 v0.10.x가 아닌 v0.12.1을 사용하여 시작됩니다. 이전 버전을 사용해야 하는 경우 다음에서 표시된 대로 package.json에 v0.10.x를 지정하십시오. 

```
        "engines": {
            "node": "0.10.x"
        }
```
{: codeblock}

* v0.12.1에 대해 알려진 문제점:
   * Bluemix Live Sync에서 제공하는 디버그 도구 기능을 사용하는 경우 "일시중단”기능이 중단됩니다. 
   * MQ Light 서비스에 사용되는 mqlight 모듈이 v0.12.x에서는 지원되지 않습니다. 

* 다음과 같이 여러 보안 취약점이 해결되었습니다. 
  * IBM SDK for Node.js에 영향을 미치는 OpenSSL의 취약점이 해결되었습니다. 자세한 내용은 [보안 공고](http://www-01.ibm.com/support/docview.wss?uid=swg21701494)에 있습니다.
  * IBM SDK for Node.js에 영향을 미치는 RC4 Stream Cipher의 취약점이 해결되었습니다. 자세한 내용은 [보안 공고](http://www-01.ibm.com/support/docview.wss?uid=swg21882778)에 있습니다.

##  2015년 4월 2일: 업데이트된 Node.js 빌드팩 v1.15-20150331-2231

* Node.js 빌드팩에는 세 개의 새로운 기능이 있으며 사용자가 데스크탑에 있는 것과 같이 다시 배치하지 않고 Bluemix에서 신속하게 개발하도록 도움을 줍니다. 
  * 데스크탑 동기화: (Windows) 데스크탑 트리를 클라우드 기반 프로젝트 작업공간과 동기화합니다. 
  * 라이브 편집: Bluemix에서 실행 중인 Node.js 애플리케이션을 변경하고 브라우저에서 즉시 테스트할 수 있습니다. 
  * 디버그: 환경으로 쉘(shell)하여 디버그합니다! 노드 검사기 디버거를 사용하여 코드의 동적 편집, 중단점 삽입, 코드 스텝 스루, 런타임 다시 시작 등을 수행할 수 있습니다. 
  * 자세한 정보는 [앱 관리](/docs/manageapps/app_mng.html#Utilities)를 참조하십시오. 
* [Cloud Foundry의 Node.js 빌드팩](https://github.com/cloudfoundry/nodejs-buildpack)에서 최신 변경사항을 가져왔습니다. 이러한 변경은 커뮤니티에서 작성한 몇 가지 버그 수정 및 개선사항과 함께 제공됩니다. 
* 이제 Node.js 빌드팩은 [IBM SDK for Node.js v1.1.0.13](https://developer.ibm.com/node/sdk/)과 함께 제공됩니다.

## 2015년 1월 5일: 업데이트된 Node.js 빌드팩 v1.9.1-20141208-1221

* Node.js 빌드팩에 동적 로그 설정 지원이 포함됩니다. 이러한 지원을 통해, 애플리케이션이 로깅에 log4js, bunyan 또는 ibmbluemix 모듈을 사용 중인 경우 개발자가 동적으로 애플리케이션 로그 레벨을 변경할 수 있습니다. 
* 이제 Node.js 빌드팩은 [IBM SDK for Node.js v0.10.33](https://developer.ibm.com/node/sdk/)과 함께 제공됩니다. 이 업데이트에는 POODLE 문제에 대한 수정사항도 포함됩니다. 

## 2014년 10월 23일: 업데이트된 Node.js 빌드팩 v1.6-20141013-1736

* 이제 Node.js 빌드팩은 [IBM SDK for Node.js v1.1.0.8](https://developer.ibm.com/node/sdk/)과 함께 제공됩니다. 이 업데이트는 애플리케이션에 안정적인 최신 Node.js 런타임 v0.10.32를 지정하면 완전히 지원되는 IBM Node.js 런타임을 사용할 수 있다는 의미입니다. 이번 최신 SDK에는 서비스 거부(DoS)를 일으키는 임베디드 qs 모듈 문제의 수정사항이 포함되어 있습니다. 또한 npm 모듈의 업데이트된 버전과 http 및 url 모듈의 다른 개선사항도 포함합니다. 자세한 내용은 [v0.10.32 변경 로그](https://raw.githubusercontent.com/joyent/node/v0.10.32/ChangeLog)를 참조하십시오. 
* 배치하는 동안 고객 애플리케이션에 올바르지 않은 index.html 파일을 추가하는 버그에 대한 수정사항도 포함되어 있습니다. 

## 2014년 9월 30일: 업데이트된 Node.js 빌드팩 v1.4-20140908-1746

* 이제 Node.js 빌드팩은 [IBM SDK for Node.js v1.1.0.7](https://developer.ibm.com/node/sdk/)과 함께 제공됩니다. 이 업데이트는 애플리케이션에 안정적인 최신 Node.js 런타임 v0.10.31을 지정하면 완전히 지원되는 IBM Node.js 런타임을 사용할 수 있다는 의미입니다. 완전히 지원되는 Node.js 런타임을 통해 고객은 일관된 지원 경험을 받게 됩니다.
* 이 빌드팩에는 개선된 서비스 프레임워크가 포함됩니다. 특히 Monitoring and Analytics 서비스를 바인드할 때 유용하며 서비스가 실패하는 경우 추가 진단 정보를 제공합니다.

## 2014년 8월 28일: 업데이트된 Node.js 빌드팩 v1.3-20140821-1143

* 이제 최신 Node.js 빌드팩이 IBM SDK for Node.js v1.1.0.6과 함께 제공됩니다. 이 업데이트는 애플리케이션에 안정적인 최신 Node.js 런타임 v0.10.30을 지정하면 완전히 지원되는 IBM Node.js 런타임을 사용할 수 있다는 의미입니다. 이 런타임은 [V8 메모리 손상 취약성 ![외부 링크 아이콘](../../icons/launch-glyph.svg "외부 링크 아이콘")](http://blog.nodejs.org/2014/07/31/v8-memory-corruption-stack-overflow)을 수정합니다.
* 또한 이 빌드팩에는 Monitoring and Analytics 서비스 확장에 대한 개선사항과 버그 수정사항이 포함되어, 이를 사용하면 서비스에서의 성능 및 오류 조건을 진달할 수 있습니다.

## 2014년 7월 29일: 업데이트된 Node.js 빌드팩 v1.1-20140717-1447

이제 이 Node.js 빌드팩에 IBM SDK for Node.js v1.1.0.5가 제공됩니다. 이 업데이트는 애플리케이션에 안정적인 최신 Node.js 런타임 v0.10.29를 지정하면 완전히 지원되는 IBM Node.js 런타임을 사용할 수 있다는 의미입니다. 자세한 정보는 [IBM Node.js SDK](https://developer.ibm.com/node/sdk/)에서 확인하십시오.

# rellinks
{: #rellinks notoc}
## general
{: #general notoc}
* [node.js 런타임](index.html)
