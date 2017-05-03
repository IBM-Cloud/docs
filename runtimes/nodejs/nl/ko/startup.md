---

copyright:
  years: 2015, 2017
lastupdated: "2017-03-23"

---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}


# 시작 명령
{: #startup_commmand}

Bluemix Node.js 애플리케이션에 대한 시작 명령을 지정하는 방법으로 **Procfile** 또는 **package.json** 파일을 사용할 것을 권장합니다.
{: shortdesc}

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

**Procfile** 및 **package.json** 파일에 대한 자세한 정보는 [Tips for Node.js Applications ![외부 링크 아이콘](../../icons/launch-glyph.svg "외부 링크 아이콘")](https://docs.cloudfoundry.org/buildpacks/node/node-tips.html)를 참조하십시오.
