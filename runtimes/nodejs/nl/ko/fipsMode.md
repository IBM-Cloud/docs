---

copyright:
  years: 2015, 2017
lastupdated: "2017-03-23"

---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}

# FIPS 모드
{: #fips_mode}

Nodejs 빌드팩 버전 v3.2-20160315-1257 이상은 [FIPS ![외부 링크 아이콘](../../icons/launch-glyph.svg "외부 링크 아이콘")](https://en.wikipedia.org/wiki/Federal_Information_Processing_Standards)를 지원합니다.  
{: shortdesc}

FIPS 사용 노드 엔진을 사용하려면 환경 변수 FIPS_MODE를 true로 설정하십시오.
예: 

```
    $ cf set-env myapp FIPS_MODE true
```
{: codeblock}

FIPS_MODE가 true일 때 일부 노드 모듈이 작동하지 않을 수도 있음을 인지하는 것이 중요합니다. 예를 들어, **[MD5 ![외부 링크 아이콘](../../icons/launch-glyph.svg "외부 링크 아이콘")](https://en.wikipedia.org/wiki/MD5)를 사용하는 노드 모듈은 실패합니다**(예: [Express ![외부 링크 아이콘](../../icons/launch-glyph.svg "외부 링크 아이콘")](http://expressjs.com/)). Express의 경우, Express 앱에서 [etag ![외부 링크 아이콘](../../icons/launch-glyph.svg "외부 링크 아이콘")](http://expressjs.com/en/api.html)를 false로 설정하면
해결될 수도 있습니다. 예를 들면, 코드에서 다음과 같이 할 수 있습니다. 
```
    app.set('etag', false);
```
{: codeblock}
자세한 정보는 이 [stackoverflow 게시물 ![외부 링크 아이콘](../../icons/launch-glyph.svg "외부 링크 아이콘")](http://stackoverflow.com/questions/15191511/disable-etag-header-in-express-node-js)을
참조하십시오.

**참고** [앱 관리](/docs/manageapps/app_mng.html) 및 FIPS_MODE는 동시에 지원되지 *않습니다*.  BLUEMIX_APP_MGMT_ENABLE 환경 변수가 설정되고 FIPS_MODE 환경 변수가 true로 설정되면 앱이 스테이징에 실패합니다.

FIPS_MODE의 상태를 확인하는 여러 방법이 있습니다. 
<ul>
<li> 다음과 유사한 메시지는 애플리케이션의 로그에서 확인할 수 있습니다.    

  <pre>
  Installing FIPS-enabled IBM SDK for Node.js (4.4.3) from cache
  </pre>
  {: codeblock}

이 메시지는 FIPS 사용 node.js 엔진이 실행 중이지만 FIPS가 실행 중일 필요는 없음을 표시합니다. 
</li>

<li> **process.versions.openssl**의 값을 확인할 수 있습니다. 예:

  <pre>
  console.log('ssl version is [' +process.versions.openssl +']');
  </pre>
  {: codeblock}

SSL 버전에 "fips"가 포함되어 있다면 사용 중인 SSL의 버전이 FIPS 모드를 지원하는 것입니다.   
</li>

<li> node.js 버전 6 이상의 경우, 다음과 유사한 코드에서 crypto.fips가 리턴하는 값을 확인할 수 있습니다.

  <pre>
  console.log('crypto.fips== [' +crypto.fips +']');
  </pre>
  {: codeblock}

리턴된 값이 1일 경우 FIPS가 사용 중입니다. crypto.fips는 node.js 버전 6보다 이전일 경우 *undefined*를 리턴합니다.
</li>
</ul>

## Nodejs v4
{: #nodejs_v4_fips}

다음 표에서는 FIPS를 사용하는 node.js v4의 동작을 설명합니다. 

|                 | 결과        |
| :-------------- | :------------ |
|FIPS_MODE=true   |success (1)    |
|FIPS_MODE !=true |success (2)    |

* success (1)
  * FIPS가 사용 중입니다.
  * 로그에 *Installing FIPS-enabled IBM SDK for Node.js*메시지가 포함됩니다.
  * process.versions.openssl에서 리턴한 값은 "fips"를 포함합니다.
* success (2)
  * FIPS가 사용 중이 *아닙니다*.
  * 로그에 *Installing FIPS-enabled IBM SDK for Node.js*메시지가 포함되지 *않습니다*.
  * process.versions.openssl에서 리턴한 값은 "fips"를 포함하지 *않습니다*. 

## Nodejs v6
{: #nodejs_v6_fips}

Node.js 버전 6과 함께 FIPS 모드를 실행하려면 **FIPS_MODE=true**로 설정하는 것 외에도
다음 예제에서처럼 시작 명령에 **--enable-fips**를 포함해야 합니다. 
```
{
    ...   
    "scripts": {
      "start": "node --enable-fips app.js"
    }
}
```
{: codeblock}

다음 표에서는 FIPS를 사용하는 node.js v6의 동작을 설명합니다. 

|                 |--enable-fips  |NO --enable-fips |
| :-------------- | :------------ | :-------------- |
|FIPS_MODE=true   |success (1)    |success (2)      |
|FIPS_MODE !=true |failure (3)    |success (4)      |

* success (1)
  * FIPS가 사용 중입니다.
  * 로그에 *Installing FIPS-enabled IBM SDK for Node.js*메시지가 포함됩니다.
  * process.versions.openssl에서 리턴한 값은 "fips"를 포함합니다. 
  * crypto.fips는 1을 리턴하며 이는 FIPS가 사용 중임을 표시합니다. 
* success (2)
  * FIPS가 사용 중이 *아닙니다*.
  * 로그에 *Installing FIPS-enabled IBM SDK for Node.js*메시지가 포함됩니다.
  * process.versions.openssl에서 리턴한 값은 "fips"를 포함합니다. 
  * crypto.fips는 0을 리턴하며 이는 FIPS가 사용 중이 *아님*을 표시합니다. 
* failure (3)
  * FIPS가 사용 중이 *아닙니다*.
  * 로그에 *Installing FIPS-enabled IBM SDK for Node.js*메시지가 포함되지 *않습니다*.
  * 스테이징은 "ERR node: bad option: --enable-fips" 메시지와 함께 실패합니다. 
* success (4)
  * FIPS가 사용 중이 *아닙니다*.
  * 로그에 *Installing FIPS-enabled IBM SDK for Node.js*메시지가 포함되지 *않습니다*.
  * process.versions.openssl에서 리턴한 값은 "fips"를 포함하지 *않습니다*. 
  * crypto.fips는 0을 리턴하며 이는 FIPS가 사용 중이 *아님*을 표시합니다. 
