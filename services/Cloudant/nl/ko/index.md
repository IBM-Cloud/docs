---

copyright:

  years: 2015, 2016

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}

# Cloudant 시작하기
{: #getting-started-with-cloudant}
마지막 업데이트 날짜: 2016년 8월 12일
{: .last-updated}

{{site.data.keyword.cloudant}}는 문서 데이터베이스이며 JSON에 데이터를 저장하는 서비스(DBaaS)입니다.
확장성과 고가용성 및
지속성을 염두에 두고
빌드됩니다.
맵 축소, Cloudant 조회, 전체 텍스트
색인화 및 지리공간
색인화와 같은
다양한 색인화 옵션이 있습니다.
복제 기능을 사용하면 데이터베이스 클러스터,
데스크탑 PC 및 모바일 디바이스 간에 데이터 동기화를 쉽게 유지할 수 있습니다.
{:shortdesc}

Bluemix 대시보드의 서비스 시작 페이지에서 {{site.data.keyword.cloudant}} 콘솔을 시작할 수 있습니다. 

서비스를 사용하려면 다음 단계를 수행하십시오. 
<ol>
<li>Bluemix 대시보드 또는 CloudFoundry
명령행 인터페이스를 사용하여 서비스 인스턴스를 작성하십시오.
<p>대시보드를 사용하여 인스턴스를 작성하려면
다음 단계를 따르십시오.
<ol>
<li>Bluemix에 로그온하십시오.</li>
<li>대시보드의 데이터 및 분석 패널에서
'<code>데이터로 작업</code>' 링크를 클릭하십시오.&amp; Analytics panel.</li>
<li>'<code>새 서비스</code>' 단추를 클릭하십시오.</li>
<li>서비스 목록에서 {{site.data.keyword.cloudant}} 단추를 클릭하십시오.</li>
<li>{{site.data.keyword.cloudant}} 정보 페이지에서
'<code>선택 {{site.data.keyword.cloudant}}</code>' 단추를 클릭하십시오.</li>
<li>{{site.data.keyword.cloudant}} 카탈로그 페이지에서
필요한 서비스에 대한 세부사항을 채우십시오.
진행할 준비가 되면 '<code>작성</code>' 단추를 클릭하십시오.</li>
<li>Cloudant 인스턴스가 작성되면 해당 인스턴스에 대한
대시보드가 표시됩니다.
인스턴스에 액세스하는 데 필요한 모든 세부사항을 보려면 '<code>서비스 신임 정보</code>' 링크를 클릭하십시오.</li>
</ol>
</p>
<p>CloudFoundry 명령행 인터페이스를 사용하여 인스턴스를 작성하려면
다음 단계를 따르십시오.
<ol>
<li>시스템에 CloudFoundry <code>cf</code> 도구를 설치하십시오.
이 작업 방법에 대한 지시사항은 <a href="https://console.ng.bluemix.net/docs/cli/index.html">Bluemix CLI 및 dev 도구 안내서</a>에 나와 있습니다.</li>
<li>명령을 사용하여 새 서비스 인스턴스를 작성하십시오.<br/>
<pre><code>cf create-service</code></pre></li>
<li>사용 가능한 서비스 목록이 표시됩니다.
하나를 선택한 다음 고유한 인스턴스 이름 및
서비스에 대한 플랜을 입력하십시오.
인스턴스에 대한 랜덤 이름이 제안되나 사용자가
원하는 대로 이름을 변경할 수 있습니다.</li>
<li>서비스를 작성한 후에 작성한 모든 서비스에 대한
목록을 가져올 수 있습니다.<br/>
<pre><code>cf services</code></pre></li>
<li>애플리케이션에서
서비스를 사용하기 전에 해당 서비스를 애플리케이션에
바인드해야 합니다. 명령을 사용하여 수행하십시오.<br/>
<pre><code>cf bind-service</code></pre>
결과 목록에서 애플리케이션 중 하나와 서비스 중 하나를
선택하십시오.
<code>cf</code> 명령은 바인딩 조치가 성공하면 사용자에게 알립니다.</li>
</ol>
</p>
</li>
<li><p>서비스 인스턴스를 작성한 후 다음과 유사한 JSON 데이터가 표시되며 Bluemix 대시보드에서 볼 수 있습니다.<br/>
<pre><code>{
"cloudantNoSQLDB": {
"name": "Cloudant-3s",
"label": "cloudantNoSQLDB",
"plan": "shared",
"credentials": {
"username": "someusername",
"password": "secret",
"host": "myhost-bluemix.cloudant.com",
"port": 443,
"url": "https://someusername:secret@myhost-bluemix.cloudant.com"
    }
  }
}</code></pre></p>
{: screen}
<p>데이터는 서비스가 바인드된 모든 Bluemix 애플리케이션의 <code>VCAP_SERVICES</code> 환경 변수에도 추가됩니다. </p>
<p>서비스 신임 정보는 다음 필드를 포함하는 JSON 오브젝트에 저장됩니다. <ul>
<li><code>key</code>: 서비스의 이름(cloudantNoSQLDB)</li>
<li><code>name</code>: 사용자가 제공한 서비스 인스턴스의 이름</li>
<li><code>host</code>: 서버의 호스트 이름</li>
<li><code>port</code>: 서비스를 실행 중인 포트 번호(일반적으로 443)</li>
<li><code>username</code>: 인증에 사용되는 사용자 이름</li>
<li><code>password</code>: 인증에 사용되는 비밀번호</li>
<li><code>url</code>: 서비스 인스턴스의 URL</li>
</ul></li>
<li><p>Bluemix 애플리케이션에서, <code>VCAP_SERVICES</code> 환경 변수의 신임 정보를 읽으십시오.</p>
<p>Bluemix 외부 또는 Bluemix의 다른 지리적 지역에서 실행 중인 애플리케이션에서는
Bluemix 대시보드의 신임 정보를 검색하여 애플리케이션의 구성에 추가할 수 있습니다.</p>
</li>
<li>데이터베이스에 액세스하기 위한 기본 메커니즘은
인증할 사용자 이름 및 비밀번호를 사용하여 HTTPS를 통해 요청을 주어진 호스트 및 포트로 보내는 것입니다. 다음을 포함하여 다양한 애플리케이션
언어 및 플랫폼을 통해 요청을 보낼 수 있습니다.
<ul>
<li><a href="https://github.com/cloudant/sync-android">Android</a></li>
<li><a href="https://github.com/cloudant/CDTDatastore">Apple iOS</a></li>
<li><a href="https://github.com/cloudant/java-cloudant">Java</a></li>
<li><a href="https://github.com/cloudant/objective-cloudant">Objective C 및 Swift</a></li>
<li><a href="https://github.com/cloudant/python-cloudant">Python</a></li>
</ul>
이 외에도 여러 가지가 있습니다.
자세한 정보는 <a href="https://cloudant.com/for-developers/">Cloudant 개발자 홈 페이지</a> 및
<a href="http://docs.cloudant.com/libraries.html">클라이언트 라이브러리</a> 목록을 참조하십시오.
</li>
<li>애플리케이션이 준비되면 이를 확인하기 위해 Bluemix 환경에 배치할 수 있습니다.
애플리케이션을 배치하려면 명령을 사용하십시오.<br/>
<pre><code>cf push</code></pre></li>
<li>애플리케이션의 바인딩을 해제하려면 명령을 사용하십시오.<br/>
<pre><code>cf unbind-service</code></pre></li>
<li>서비스 인스턴스를 삭제하려면 명령을 사용하십시오.<br/>
<pre><code>cf delete-service</code></pre></li>
</ol>

데이터베이스 인증 및 요청 작성에 대한 추가 정보는 [API 참조](https://docs.cloudant.com/api.html)에서 볼 수 있습니다. 

# 관련 링크
{: #rellinks}

## 튜토리얼 및 샘플
{: #samples}

* [Cloudant 클라이언트 라이브러리](https://docs.cloudant.com/libraries.html)
* [Bluemix에서 Liberty에 대해 Cloudant 사용](https://developer.ibm.com/bluemix/2014/07/08/cloudant_on_bluemix/)
* [Cloudant 안내서](https://docs.cloudant.com/guides.html)

## API 참조
{: #api}

* [Cloudant API 참조](https://docs.cloudant.com/api.html)

## 관련 링크
{: #general}

* [Cloudant 웹 사이트 및 대시보드](https://cloudant.com/)
* [Cloudant 블로그](https://cloudant.com/blog)
