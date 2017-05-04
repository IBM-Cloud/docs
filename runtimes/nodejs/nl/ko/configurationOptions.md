---

copyright:
  years: 2015, 2017
lastupdated: "2017-03-23"

---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}

# 구성 옵션
{: #configuration_options}
{: shortdesc}

sdk-for-nodejs 빌드팩 구성에 다양한 옵션을
사용할 수 있습니다.

## NPM 스크립트
{: #npm_scripts}
NPM은 사용자 node_modules가 설치되기 전과 후에 적용되는 **preinstall** 및 **postinstall** 스크립트를 포함하여 스크립트를 실행할 수 있는 스크립팅 기능을 제공합니다. 전체 세부사항은 [npm-scripts ![외부 링크 아이콘](../../icons/launch-glyph.svg "외부 링크 아이콘")](https://docs.npmjs.com/misc/scripts)를 참조하십시오.

## 캐시 작동
{: #cache_behavior}
{{site.data.keyword.Bluemix}}는 노드 애플리케이션당 캐시 디렉토리를 유지보수하며, 이는 빌드 사이에서 지속됩니다. 캐시는 해결된 종속 항목을 저장하므로 이러한 항목은 앱이 배치될 때마다 다운로드 및 설치되지 않습니다. 예를 들어 myapp이 **express**에 종속된다고 가정합니다. 그러면 처음 myapp을 배치할 때 **express** 모듈이 다운로드됩니다. 이후에 myapp을 배치할 때는 **express**의 캐시된 인스턴스가 사용됩니다. 기본 동작은 NPM에서 설치한 모든 node_modules와 bower에서 설치한 bower_components를 캐시하는 것입니다. 

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
