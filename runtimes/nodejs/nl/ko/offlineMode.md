---

copyright:
  years: 2016, 2017
lastupdated: "2017-04-11"

---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}


# node.js의 오프라인 모드
{: #offline_mode}

node.js 애플리케이션이 {{site.data.keyword.Bluemix}}에 푸시될 때 SDK for Node.js 빌드팩은
일반적으로 NPM의 노드 모듈 등 외부 리소스에서 아티팩트를 다운로드합니다. 일부
상황(예: [Bluemix 데디케이티드](/docs/dedicated/index.html#dedicated) 및
[Bluemix 로컬](/docs/local/index.html#local) 포함)에서,
Bluemix의 외부에 있는 액세스 사이트를 신뢰하지 않거나 이를 더 명시적으로 제어할 수도 있습니다.  
{: shortdesc}

다음은 node.js 빌드팩이 액세스할 수 있는 외부 사이트입니다. [Bluemix 데디케이티드](/docs/dedicated/index.html#dedicated) 및
[Bluemix 로컬](/docs/local/index.html#local) Bluemix 환경에서 이러한 사이트는 *화이트리스트에 나열*되어 있어야 할 수 있습니다.

* 다음은 사용 가능한 노드 엔진 버전을 확인하는 데 사용될 수 있습니다. http://nodejs.org/
* 다음은 빌드팩에 포함되지 않은 노드 엔진 버전을 검색하는 데 사용됩니다. https://s3pository.heroku.com
*  다음은 빌드팩에 포함되지 않은 npm의 버전을 검색하는 데 사용됩니다. https://www.npmjs.com/package/npm 및 https://semver.herokuapp.com
* https://iojs.org 사이트가 빌드팩에 포함되어 있지 않거나 다음에서 사용 가능하지 않은 이전 버전의 노드를 검색하는 데 사용됩니다. https://semver.herokuapp.com
* 다음은 express 등의 노드 모듈을 검색하는 데 사용됩니다. https://registry.npmjs.org

화이트리스트에 나열된 사이트의 세트를 최소화하려면, SDK for Node.js 빌드팩에 포함되는 노드 엔진 버전을 사용하도록 노드 애플리케이션을 구성하십시오. 빌드팩에 포함된 노드 엔진 버전의 세트는 [최신 업데이트](./updates.html)를 참조하십시오. 이를 완료하면 노드 모듈을 다운로드하는 데 https://registry.npmjs.org 사이트만 필요합니다.

새 버전의 SDK for Node.js 빌드팩이 설치될 때 사용 가능한 노드 엔진 버전의 세트는 종종
최신 버전으로 전진합니다. 이러한 경우 사용자는 최신 노드 엔진 버전을 지정하도록 노드 앱을 다시 구성해야 할 수 있습니다.


## 오프라인 애플리케이션
{: #offline_applications}

https://registry.npmjs.org 여기에 액세스할 필요성을 제거하기 위해 사용자의 애플리케이션에 필요한 모든 노드 모듈을 사용자의 애플리케이션 내에 포함할 수 있습니다. 이를 수행하려면 애플리케이션에 필요한 모든 모듈에 대해 **npm install**을 실행하고 결과 *node_modules* 디렉토리를 푸시된 애플리케이션과 함께 포함하십시오.

참고로, 해당 종속 항목에 종속 항목이 있을 수 있으며 이들에도 종속 항목이 있을 수 있는 식이나 package.json에는
최상위 레벨 종속 항목만 포함됩니다. 종속 항목 중 하나가 릴리스되는 새 버전 및 package.json의 범위를 사용하는 경우, node_modules 디렉토리의 모듈은 더 이상 사용할 수 없습니다. 이를 막기 위해 *Shrinkwrap*이 모든 종속 항목 버전을 잠그는 데 도움이 됩니다. shrinkwrap을 사용하려면 비어 있거나 정리된 node_modules 디렉토리로 시작한 후 프로젝트의 루트 디렉토리에서 다음을 실행하십시오.
0. npm install
1. npm dedupe
2. npm shrinkwrap

그러면 루트 디렉토리에서 *package.json*이 변경되고 *npm-shrinkwrap.json*이 추가될 수 있습니다.
*package.json* 파일에서 종속 항목을 변경하는 경우 항상 *dedupe* 및 *shringwrap* 단계를 반복하십시오.

## 프록시 작업
{: #working_with_proxy}

[Bluemix 데디케이티드](/docs/dedicated/index.html#dedicated) 및
[Bluemix 로컬](/docs/local/index.html#local) 등의 일부 환경에서 프록시를 구성할 수 있습니다. 자세한 내용은
[프록시 작업](/docs/manageapps/workingWithProxy.html)을 참조하십시오.
