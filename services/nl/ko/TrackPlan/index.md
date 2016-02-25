{:shortdesc: .shortdesc}
{:screen: .screen}
{:new_window: target="_blank"}
{:codeblock: .codeblock}

#{{site.data.keyword.trackplan}} 서비스 시작하기 {: #track-plan}  

*마지막 업데이트 날짜: 2016년 1월 21일*

태스크를 보고 편집, 계획하려면 {{site.data.keyword.trackplanlong}}({{site.data.keyword.trackplan}} 서비스)를 사용하십시오. 사용자의 작업과 사용자 팀의 작업을 추적하고, 결함을 작성하고, 수신되는 내용을 확인하고, 백로그를 관리하고, 		앞으로 진행할 작업을 계획할 수 있습니다.
{: shortdesc}

{{site.data.keyword.trackplan}} 서비스는 개발 팀의 진행상태가
				플랜에 반영되도록 계획과 코드를 연결합니다. 이 서비스를 사용하는 경우,
				스토리와 태스크, 결함을 작성하여 프로젝트 작업을 설명하고 추적할 수 있습니다. 또한
				제품 백로그, 릴리스, 스프린트를 계획하고 관리할 수도 있습니다.

1. {{site.data.keyword.Bluemix_notm}}에 로그인하고 앱의 조직 및 영역을 선택하십시오.
1. {{site.data.keyword.Bluemix_notm}} 대시보드에서 **앱 작성**을 클릭하십시오.
1. 웹 또는 모바일 앱 템플리트를 선택하고 스타터를 선택한 후 **계속**을 클릭하십시오. 앱 이름을 지정한 후
**완료**를 클릭하십시오.
1. 코딩 시작 페이지에서 아래로 화면 이동하여 **앱 개요 보기**를 클릭하십시오. 
1. {{site.data.keyword.Bluemix_notm}} 앱 대시보드에서 **GIT 추가**를 클릭하여 앱에 대한 Git 호스팅 프로젝트를 작성하십시오. **저장소에 스타터 앱 패키지를 보관하고 Delivery Pipeline 사용(빌드 & 배치)** 선택란을 선택했는지 확인한 후에 **계속**을 클릭하십시오. Git 저장소가 작성된 후 **닫기**를 클릭하십시오. GIT 추가 링크가 코드 편집 링크 및 사용자의 Git URL로 바뀝니다. 
1. 팀 작업을 관리할 수 있도록 {{site.data.keyword.trackplan}} 서비스를 영역에 추가하십시오. 
    1. {{site.data.keyword.Bluemix_notm}} 앱 대시보드에서 **서비스 또는 API 추가**를 클릭하십시오. 카테고리에서
**DevOps**를 선택하고 카탈로그에서 **Track & Plan**을 클릭하십시오.
    2. {{site.data.keyword.trackplan}} 페이지에서 플랜을 선택하고 **작성**을 클릭하십시오.    
1. 앱 목록의 상태 열에서 현재 상태(이 경우 **해제**임)를 클릭하여 {{site.data.keyword.trackplan}}
					서비스의 상태를 변경하십시오. 프로젝트 설정 페이지가 {{site.data.keyword.Bluemix_notm}} {{site.data.keyword.jazzhub_short}}에 열립니다. 
    1. {{site.data.keyword.trackplan}} 서비스를 사용으로 설정하는 옵션을 선택하십시오. 필요한 경우 지역, 조직 또는 영역을 업데이트하십시오. 
    2. **저장**을 클릭하십시오.  
1. {{site.data.keyword.Bluemix_notm}} 대시보드로 돌아가서 {{site.data.keyword.trackplan}} 서비스 타일을 클릭하십시오. 사용 중인 앱에서 {{site.data.keyword.trackplan}} 서비스의 상태가 **설정**으로 변경됩니다.
1. 앱 목록의 작업 항목 열에서
					**작성**을 클릭하여 {{site.data.keyword.trackplan}} 서비스 사용을 시작하십시오.  

{{site.data.keyword.Bluemix_notm}} 대시보드에서 {{site.data.keyword.jazzhub_short}} 프로젝트와 그 구성원 수, 가시성 및 {{site.data.keyword.trackplan}} 서비스가 사용 가능한지 여부를 볼 수 있습니다. 사용자의 {{site.data.keyword.jazzhub_short}}
			프로젝트에 대한 작업 항목을 작성하거나 계획 도구로 돌아갈 수 있습니다.  

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
<li><img src="./sout.gif" alt=""><a href="http://www.ibm.com/developerworks/topics/track%20and%20plan%20service" rel="external" title="(새 탭 또는 창에 열림)">developerWorks: {{site.data.keyword.Bluemix_notm}} {{site.data.keyword.trackplan}} 서비스</a></li>
</ul>
</div>
</aside>
</article>
