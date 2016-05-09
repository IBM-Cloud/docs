---

 

copyright:

  years: 2015, 2016

 

---

{:shortdesc: .shortdesc}
{:screen: .screen}
{:new_window: target="_blank"}
{:codeblock: .codeblock}

#{{site.data.keyword.Bluemix_notm}} iFrame에 배치 플로우 임베드 {: #embed-d2bm-iframe} 

*마지막 업데이트 날짜: 2015년 12월 8일* 

{{site.data.keyword.Bluemix_notm}}에 배치 플로우를 iFrame으로 마크업을 지원하는 다양한 종류의 컨텐츠에 임베드할 수 있습니다. 예를 들어, iFrame을 readme 파일, 블로그 및 웹 페이지에 임베드할 수 있습니다. 

{: shortdesc} 

iFrame 플로우는 회사 브랜드를 유지하려는 경우에 유용합니다. 사용자가 임베디드 iFrame을 클릭하면, bluemix.net 웹 사이트로 경로 재지정되는 대신 사용자 컨텐츠에 머무르게 됩니다. 회사 브랜드에 관심이 없는 경우, iFrame 대신 표준 [{{site.data.keyword.Bluemix_notm}}에 배치 단추](../develop/deploy_button.html)를 사용자 컨텐츠에 삽입할 수 있습니다. 

##iFrame 플로우의 단계 {: #iframe-steps} 

1. 활성 {{site.data.keyword.Bluemix_notm}} 계정이 없는 경우, 평가판 계정을
작성합니다.  

2. 지역, 조직, 영역 및 앱 이름을 선택할 수 있습니다.
제시된 앱 이름은 이전 앱 이름, 사용자 이름 및 시간을 바탕으로
구성됩니다. 

3. 원래 공용 Git 저장소의 마스터 분기가 새 전용 {{site.data.keyword.jazzhub_short}}
프로젝트에 새 Git 저장소로 복제됩니다. 

4. 앱에 빌드 파일이 필요한 경우 빌드 파일이 자동으로 검색되어 앱이
빌드됩니다. 

5. 앱이 사용자의 {{site.data.keyword.Bluemix_notm}} 조직에 배치됩니다. 

##iFrame 플로우의 예 {: #iframe-example} 

<p>
<a class="xref" href="http://d2bm-iframe-sample.ng.bluemix.net/" target="_blank" title="(새 탭 또는 창에서 열림)">IBM Bluemix D2BM iFrame 샘플</a>은
공용 Git 저장소용 iFrame 플로우 예제를 제공합니다.<div class="image"><img class="image" src="images/d2bm_iframe_sample2.png" alt="Bluemix에 배치 iFrame 플로우 샘플" /></div>
</p> 

<p>
이 샘플에 대한 소스를 보려면 <a class="xref" href="https://hub.jazz.net/project/idsorg/d2bm-iframe-sample/overview" target="_blank" title="(새 탭 또는 창에서 열림)">소스</a>를
클릭하십시오.
</p>

##iFrame 플로우 임베드  {: #embed-iframe}  

<ol>
<li><a href="https://bluemix.net/deploy/embed.js" target="_blank">https://bluemix.net/deploy/embed.js</a>에서 JavaScript 유틸리티를 로드하십시오. 이 유틸리티는 jQuery에 따라 달라지며, 다음 스크립트 태그를
사용자 문서에 추가하여 로드됩니다. 
<pre class="pre">
<code>&lt;script type="text/javascript" src="https://bluemix.net/deploy/embed.js"&gt;&lt;/script&gt;</code>
</pre>
</li>
<li> 다음 인수를 사용하여 <code>DeployToBluemixIFrame</code> 생성자를
시작하십시오.<dl class="parml">
<dt class="pt dlterm">domNodeId</dt>
<dd class="pd">iFrame을 사용자 컨텐츠에 삽입할 수 있는 domNode의 ID입니다.</dd>

<dt class="pt dlterm">callback</dt>
<dd class="pd">이 인수는 iFrame 플로우가 완료되거나 오류가 발생할 경우
호출됩니다. 인수는 결과와 함께 응답합니다. 다음 코드 스니펫은
성공적인 결과 콜백을 보여줍니다.</dd>

<dt class="pt dlterm">args</dt>
<dd class="pd">위젯에 대한 입력 매개변수가 포함된 오브젝트입니다. 다음 매개변수가
사용 가능합니다.<dl class="parml">

<dt class="pt dlterm">repository</dt>
<dd class="pd">복제 및 배치를 위한 소스로 사용할 Git 저장소입니다.
이 값은 필수입니다. </dd>
	
<dt class="pt dlterm">app_name</dt>
<dd class="pd">iFrame 내의 <strong>app_name</strong> 필드에 지정된 값으로 사용할
기본 앱 이름입니다. 이 값은 선택사항입니다.</dd>
	
    
<dt class="pt dlterm">region_id</dt>
<dd class="pd">기본 대상 지역의 ID입니다. 예: <code>ibm:yp:us-south</code>.
이 값은 선택사항입니다.</dd>
	
<dt class="pt dlterm">organization_guid</dt>
<dd class="pd">기본 대상 조직의 GUID입니다. 이 값을 찾으려면 <strong>조직 관리</strong> > <i>organization_name</i>을(를) 클릭하십시오. 조직의 URL에는 해당 조직의 GUID가 포함됩니다.
이 값은 선택사항입니다.</dd>
	
<dt class="pt dlterm">space_guid</dt>
<dd class="pd">기본 대상 영역의 GUID입니다. 이 값을 찾으려면 <strong>조직 관리</strong> > <i>space_name</i>을(를) 클릭하십시오. 영역의 URL에는 해당 영역의 GUID가 포함됩니다.
이 값은 선택사항입니다.</dd>
	
<dt class="pt dlterm">auto_login</dt>
<dd class="pd">사용자가 iFrame에 자동으로 로그인하는지 여부를 지정합니다. 기본값은
<code>true</code>입니다. 이 값은 선택사항입니다.</dd>
	
<dt class="pt dlterm">width</dt>
<dd class="pd">iFrame의 너비입니다. 이 값은 선택사항입니다. 기본값은
<code>620</code>입니다.</dd>
	
<dt class="pt dlterm">height</dt>
<dd class="pd">iFrame의 높이입니다. 이 값은 선택사항입니다. 기본값은
<code>470</code>입니다.</dd>
</dl>

</dd>
</dl>
</li>
</ol>  

**팁:** iFrame과의 상호작용을 최소화하기 위해
**app_name**, **region_id**, **organization_guid**, **space_guid** 및
**auto_login** 필드를 미리 채울 수 있습니다.
