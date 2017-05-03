---

copyright:
  years: 2015, 2017
lastupdated: "2017-02-06"

---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}

# 사용 가능한 버전
{: #available_versions}

{{site.data.keyword.Bluemix}}는 모든 [현재 사용 가능한 Node.js 런타임](http://nodejs.org/dist/)을 제공합니다. 이 중에서 IBM은 개선사항과 버그 수정사항이 포함된 버전을 제공합니다. 자세한 정보는 [Node.js 빌드팩의 최신 업데이트](/docs/runtimes/nodejs/updates.html)를 참조하십시오.
{: shortdesc}

IBM Node.js 빌드팩은 IBM 런타임 버전을 캐시합니다. 애플리케이션에서 IBM SDK for Node.js 런타임을 사용하는 경우 애플리케이션을 Bluemix에 푸싱할 때 애플리케이션 성능이 더 빨라집니다. 

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
     "npm": "3.10.10"
  }
}
```
{: codeblock}

노드 버전은 항상 **package.json** 파일에 지정되어야 합니다. 이를 지정하지 않으면 최신 노드 버전이 사용됩니다.
