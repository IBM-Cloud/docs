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

#{{site.data.keyword.Bluemix_short}}에 대한 스타터 애플리케이션 수정
{: #modifying_starter_app}

스타터 애플리케이션을 수정한 다음 이를 {{site.data.keyword.Bluemix_short}}에 다시 배치하여 결과를 확인할 수 있습니다.
{:shortdesc}


단순히 스타터 애플리케이션의 이벤트 한계를 높이거나 제거하여 이를 더 오래 실행할 수 있습니다. 

1. 문서 편집기 또는 개발 환경에서 app.js를 여십시오. 
2. eventTarget 변수를 변경하거나, 이벤트 한계를 완전히 제거하려는 경우 이 행을 삭제하십시오.
	 <pre><code>var eventTarget = 100;</code></pre>
3. 이벤트 한계를 제거하려면 다음 if문도 삭제해야 합니다.
	 <pre><code>  
	if (eventCount >= eventTarget) {
		    status_step[3] = "Completed";
		    console.log("\nTarget event count has been reached.  Geospatial Analytics service will be stopped.\n");
		    callback(null, null);
		    } 
	</code></pre> 
4. cf push 명령을 사용하여 {{site.data.keyword.Bluemix_short}}에 수정된 애플리케이션을 다시 배치하십시오.
	 <pre><code>  
	cf push myapp
	</code></pre>
5. 애플리케이션의 URL 또는 "라우트"를 브라우저에 입력하거나 {{site.data.keyword.Bluemix_short}} 대시보드에서 시작하십시오. 
