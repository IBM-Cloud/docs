{:screen: .screen}
{:new_window: target="_blank"}
{:codeblock: .codeblock}
{:shortdesc: .shortdesc}

#{{site.data.keyword.deliverypipeline}} 시작하기 {: #delivery-pipeline}  

*마지막 업데이트 날짜: 2016년 1월 21일*

{{site.data.keyword.Bluemix}}에 빌드와 배치를 자동화하려면 IBM Continuous {{site.data.keyword.deliverypipeline}} for {{site.data.keyword.Bluemix_notm}}({{site.data.keyword.deliverypipeline}} 서비스)를 사용하십시오.
{: shortdesc} 

클라우드에서 앱을
		개발할 때 몇 가지 빌드 유형 중에서 선택할 수 있습니다. 사용자가 빌드 스크립트를
		제공하면 {{site.data.keyword.Bluemix_notm}} {{site.data.keyword.jazzhub_short}}에서 이 스크립트를 실행합니다. 사용자가 빌드 시스템을 설정할
		필요는 없습니다. 그러면 한 번의 클릭으로 하나 또는 다수의 {{site.data.keyword.Bluemix_notm}} 영역, 공용 Cloud Foundry 서버 또는 IBM Containers for {{site.data.keyword.Bluemix_notm}}의 Docker 컨테이너에 앱을 자동적으로 배치할 수 있습니다.   

빌드 작업은 Git 또는 Jazz 소스 제어 관리(SCM) 저장소의 앱 소스 코드를 컴파일하고 패키지합니다. 빌드 작업을 통해 WAR 파일 또는 IBM Containers용 Docker 컨테이너와 같은 배치 가능한 아티팩트가 생성됩니다. 또한, 빌드 내에서 단위 테스트를
				자동으로 실행할 수 있습니다. 소스 코드가 변경될 때마다
				빌드가 트리거됩니다.   

배치 작업은 빌드 작업의 결과물을 가져와 IBM Containers 또는 {{site.data.keyword.Bluemix_notm}}와 같은 Cloud Foundry 서버에 배치합니다.   

하나 또는 다수의 지역과 서비스에 배치할 수 있습니다. 예를 들면, 개발 아티팩트가 IBM Containers를 사용하고 한 지역에서 테스트되며 여러 지역의 프로덕션에 배치되도록 {{site.data.keyword.deliverypipeline}} 서비스를 설정할 수 있습니다. 자세한 정보는
				[지역](../../overview/index.html#ov_intro__reg)을 참조하십시오.

1. {{site.data.keyword.Bluemix_notm}}에 로그인하고 앱의 조직 및 영역을 선택하십시오.
1. {{site.data.keyword.Bluemix_notm}} 대시보드에서 **앱 작성**을 클릭하십시오.
1. 웹 또는 모바일 앱 템플리트를 선택하고 스타터를 선택한 후 **계속**을 클릭하십시오. 앱 이름을 지정한 후 **완료**를 클릭하십시오.   
1. 코딩 시작 페이지에서 아래로 화면 이동하여 **앱 개요 보기**를 클릭하십시오.   
1. {{site.data.keyword.Bluemix_notm}} 앱 대시보드에서 **GIT 추가**를 클릭하여 앱에 대한 Git 호스팅 프로젝트를 작성하십시오. **저장소에 스타터 앱 패키지를 보관하고 {{site.data.keyword.deliverypipeline}} 사용(빌드 & 배치)** 선택란을 선택했는지 확인한 후에 **계속**을 클릭하십시오.    
1. Git 저장소가 작성된 후 **닫기**를 클릭하십시오. GIT 추가 링크가 코드 편집 링크 및 사용자의 Git URL로 바뀝니다.   
1. {{site.data.keyword.deliverypipeline}} 서비스를 연관된 영역(들)에 추가하십시오. 이 서비스를 추가한 후 빌드, 테스트, 배치 작업이 포함된 단계를 구성하고 실행하여 다단계 배치 파이프라인을 {{site.data.keyword.Bluemix_notm}} 영역에 작성할 수 있습니다. 
    1. {{site.data.keyword.Bluemix_notm}} 앱 대시보드에서 **서비스 또는 API 추가**를 클릭하십시오. 카테고리의 경우, **DevOps** 선택란을 선택하고 그 카탈로그에서 **Delivery Pipeline**을 클릭하십시오. 
    2. 플랜을 선택하고 **작성**을 클릭하십시오. {{site.data.keyword.deliverypipeline}} 대시보드가 열리면서 이전에 작성한 앱이 표시됩니다.     
  
{{site.data.keyword.deliverypipeline}} 대시보드에서 사용자의
{{site.data.keyword.jazzhub_short}} 프로젝트와 해당 프로젝트의 상태를 볼 수 있습니다. 빌드와 배치된 앱, 최근 배치의 상태를 검사하거나 가장 최신 로그 또는 배치 세부사항을 확인할 수 있습니다.   

<article class="topic reference nested1" aria-labelledby="d68e338" lang="en-us" id="rellinks">
<h2 class="topictitle2" id="d68e338">관련 링크</h2>
<aside>
<div class="linklist" id="general"><h3 class="linklistlabel">관련 링크</h3>
<ul>
<li><img src="./sout.gif" alt=""><a href="https://developer.ibm.com/bluemix/support/#prereqs" rel="external" title="(새 탭 또는 창에 열림)">{{site.data.keyword.Bluemix_notm}} 전제조건</a></li>
</ul>
</div>

<div class="linklist" id="samples">
<h3 class="linklistlabel">학습서 및 샘플</h3>
<ul>
<li><img src="./sout.gif" alt=""><a href="https://hub.jazz.net/tutorials/devopsweb/" rel="external" title="(새 탭 또는 창에 열림)">앱 복제, 편집 및 배치</a></li>
<li><img src="./sout.gif" alt=""><a href="https://hub.jazz.net/tutorials/jazzeditor" rel="external" title="(새 탭 또는 창에 열림)">Node.js 앱 개발 및 배치</a></li>
<li><img src="./sout.gif" alt=""><a href="https://hub.jazz.net/tutorials/jazzeditorjava" rel="external" title="(새 탭 또는 창에 열림)">Java 앱 개발 및 배치</a></li>
<li><img src="./sout.gif" alt=""><a href="http://www.ibm.com/developerworks/topics/delivery%20pipeline%20service" rel="external" title="(새 탭 또는 창에 열림)">developerWorks: {{site.data.keyword.Bluemix_notm}} {{site.data.keyword.deliverypipeline}} 서비스</a></li>
</ul>
</div>
</aside>
</article>
