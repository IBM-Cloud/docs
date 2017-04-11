---

copyright:
  years: 2015, 2017
lastupdated: "2017-02-09"

---

<!-- Attribute definitions --> 
{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:codeblock: .codeblock}
{:screen: .screen}
{:pre: .pre}

#{{site.data.keyword.Bluemix_short}}에 스타터 애플리케이션 푸시
{: #pushing_starter_app}


 
스타터 애플리케이션을 배치하고 {{site.data.keyword.geospatialshort_Geospatial}} 서비스 사용 방법을 빠르게 학습합니다.
{:shortdesc}

1. [cf 명령행 도구를 설치](docs/starters/install_cli.html)하십시오(아직 설치하지 않은 경우). 
2. {{site.data.keyword.geospatialshort_Geospatial}} 스타터 앱의 [코드를 가져오십시오](https://hub.jazz.net/project/streamscloud/geo-starter/overview).  
3. 애플리케이션 파일을 포함하는 디렉토리의 이름을 {{site.data.keyword.Bluemix_short}}의 애플리케이션에 지정한 이름과 일치하도록 바꾸십시오. 예를 들어, 애플리케이션의 이름이 myapp이면 디렉토리의 이름을 myapp으로 바꾸십시오. 
4. 명령행에서 이름을 바꾼 디렉토리로 이동하십시오. 
<pre><code>cd myapp</code></pre>
5. {{site.data.keyword.Bluemix_short}}에 연결하십시오. 
<pre><code>cf api https://api.DomainName</code></pre>
6. 프롬프트가 표시되면 {{site.data.keyword.Bluemix_short}}에 로그인하고 대상 조직을 설정한 후 애플리케이션을 배치하십시오. 
<pre><code>
cf login
cf push myapp
</code></pre>

##다음에 수행할 작업

* {{site.data.keyword.Bluemix_short}} 대시보드를 통해 액세스할 수 있는, 애플리케이션 개요 페이지로 이동하여 애플리케이션이 성공적으로 시작되었는지 확인하십시오. 
* 애플리케이션을 시작하여 브라우저에서 보십시오. 애플리케이션 개요 페이지에서 애플리케이션의 URL(또는 "라우트")을 찾을 수 있습니다. 샘플 애플리케이션의 웹 페이지에는 애플리케이션 코드에 있는 REST API 호출의 상태 및 {{site.data.keyword.geospatialshort_Geospatial}}가 발견한 이벤트에 대한 정보가 표시됩니다. 
