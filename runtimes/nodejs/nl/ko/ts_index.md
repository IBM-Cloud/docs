---

copyright:
  years: 2017
lastupdated: "2017-02-06"

---

{:tsSymptoms: .tsSymptoms}
{:tsCauses: .tsCauses}
{:tsResolve: .tsResolve}
{:new_window: target="_blank"}
{:shortdesc: .shortdesc}

# SDK for Nodejs 문제점 해결
{: #ts}


다음은 {{site.data.keyword.Bluemix}}의 SDK for Nodejs 사용과 관련된 일반적인 문제점 해결 질문에 대한 답입니다.
{:shortdesc}

## 애플리케이션이 시작에 실패하며 “No space left on device” 오류 발생
{: #no_space_left_on_device}


Nodejs 애플리케이션이 시작에 실패하며 “No space left on device” 오류가 나타납니다. 예를 들면, 로그에 다음과 같은 오류가 표시됩니다.
{: tsSymptoms}

```
   2017-01-16T14:25:14.61-0500 [CELL/0]     ERR tar: ./app/node_modules/pm2/node_modules/cron/node_modules/moment-timezone/LICENSE: Cannot write: No space left on device

```
{: #codeblock}

버전 3 이전의 NPM 버전을 사용하는 Nodejs 애플리케이션은 종속 항목 다운로드에 추가 공간을 사용합니다.
{: tsCauses}

애플리케이션의 package.json 파일을 수정하여 NPM 버전 3 이상을 사용하십시오.
{: tsResolve}

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
