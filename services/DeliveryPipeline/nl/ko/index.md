---



copyright:

  years: 2015, 2016



---


{:screen: .screen}
{:new_window: target="_blank"}
{:codeblock: .codeblock}
{:shortdesc: .shortdesc}

# {{site.data.keyword.deliverypipeline}} 시작하기 {: #delivery-pipeline}  

마지막 업데이트 날짜: 2016년 9월 15일
{: .last-updated}

빌드와 {{site.data.keyword.Bluemix}}로의 배치를 자동화하려면 IBM Continuous {{site.data.keyword.deliverypipeline}} for {{site.data.keyword.Bluemix_notm}}를 사용하십시오.
{: shortdesc}

이 정보는 {{site.data.keyword.deliverypipeline}} 및 {{site.data.keyword.deliverypipeline}} Next 모두에 적용됩니다. 

{{site.data.keyword.deliverypipeline}} 서비스에서는 여러 빌드 유형 중에서 선택할 수 있습니다. 사용자가 빌드 스크립트를
		제공하면 {{site.data.keyword.Bluemix_notm}} {{site.data.keyword.jazzhub_short}}에서 이 스크립트를 실행합니다. 사용자가 빌드 시스템을 설정할
		필요는 없습니다. 그러면 한 번의 클릭으로 하나 또는 다수의 {{site.data.keyword.Bluemix_notm}} 영역, 공용 Cloud Foundry 서버 또는 IBM Containers for {{site.data.keyword.Bluemix_notm}}의 Docker 컨테이너에 앱을 자동적으로 배치할 수 있습니다.   

빌드 작업은 Git 또는 Jazz 소스 제어 관리(SCM) 저장소의 앱 소스 코드를 컴파일하고 패키지합니다. 빌드 작업을 통해 WAR 파일 또는 IBM Containers용 Docker 컨테이너와 같은 배치 가능한 아티팩트가 생성됩니다. 또한, 빌드 내에서 단위 테스트를
				자동으로 실행할 수 있습니다. 소스 코드가 변경될 때마다
				빌드가 트리거됩니다. 

배치 작업은 빌드 작업의 결과물을 가져와 IBM Containers 또는 {{site.data.keyword.Bluemix_notm}}와 같은 Cloud Foundry 서버에 배치합니다.   

하나 또는 다수의 지역과 서비스에 배치할 수 있습니다. 예를 들면, 개발 아티팩트가 IBM Containers를 사용하고 한 지역에서 테스트되며 여러 지역의 프로덕션에 배치되도록 {{site.data.keyword.deliverypipeline}} 서비스를 설정할 수 있습니다. 자세한 정보는
				[지역](../../overview/index.html#ov_intro__reg)을 참조하십시오.

파이프라인 작성 방법은 기존 애플리케이션에 파이프라인을 추가하거나 기존 애플리케이션 없이 파이프라인을 작성하는 등 여러 가지가 있습니다. 조직에 {{site.data.keyword.deliverypipeline}} 서비스가 없으면 카탈로그로 이동하여 {{site.data.keyword.deliverypipeline}} 또는 {{site.data.keyword.deliverypipeline}} Next를 클릭하고 작성을 클릭하십시오. 

기존 애플리케이션에 맞게 {{site.data.keyword.deliverypipeline}}을 설정하려면 다음 단계를 완료하십시오.     

1. {{site.data.keyword.Bluemix_notm}} 앱 대시보드의 개요 탭에 있는 **Continuous Delivery**에서 컨텍스트에 따라 **Git 저장소 및 파이프라인 추가** 또는 **Git 추가**를 클릭하여 Git에 호스팅되는 앱의 프로젝트를 작성하십시오. 
1. **저장소를 스타터 앱 패키지로 채우기 및 파이프라인 빌드 및 배치 사용** 선택란이 선택되어 있는지 확인한 다음 **계속**을 클릭하십시오. 계속하기 위해 이메일 주소를 확인해야 할 수도 있습니다.   
1. Git 저장소가 작성된 후 **닫기**를 클릭하십시오. Git 추가 단추가 코드 편집 단추 및 사용자의 Git URL로 바뀝니다.   
1. 파이프라인을 열려면 **코드 편집**을 클릭한 후 **빌드 & 배치**를 클릭하십시오. 처음 파이프라인을 실행하려면 변경사항을 Git 저장소로 푸시하십시오. 

이 서비스를 추가한 후 빌드, 테스트, 배치 작업이 포함된 단계를 구성하고 실행하여 다단계 배치 파이프라인을 {{site.data.keyword.Bluemix_notm}} 영역에 작성할 수 있습니다. {{site.data.keyword.deliverypipeline}} 대시보드에서 사용자의
{{site.data.keyword.jazzhub_short}} 프로젝트와 해당 프로젝트의 상태를 볼 수 있습니다. 빌드와 배치된 앱, 최근 배치의 상태를 검사하거나 가장 최신 로그 또는 배치 세부사항을 확인할 수 있습니다.   

<article class="topic reference nested1" aria-labelledby="d68e338" lang="en-us" id="rellinks" role="article">
<h2 class="topictitle2" id="d68e338">관련 링크</h2>
<aside role="complementary" aria-labelledby="related_links">
<div class="linklist" id="general"><h3 class="linklistlabel" id="related_links">관련 링크</h3>
<ul>
<li><img src="./sout.gif" alt=""><a href="https://developer.ibm.com/bluemix/support/#prereqs" rel="external" title="(새 탭 또는 창에서 열림)">{{site.data.keyword.Bluemix_notm}} 전제조건</a></li>
<li><img src="./sout.gif" alt=""><a href="https://www.ibm.com/devops/method/content/deliver/practice_delivery_pipeline/" rel="external" title="(새 탭 또는 창에서 열림)">IBM Bluemix Garage Method: Delivery Pipeline</a></li>
</ul>
</div>

<div class="linklist" id="samples">
<h3 class="linklistlabel">튜토리얼 및 샘플</h3>
<ul>

<!--
<li><img src="./sout.gif" alt=""><a href="https://hub.jazz.net/tutorials/devopsweb/" rel="external" title="(Opens in a new tab or window)">Clone, edit, and deploy an app</a></li>
<li><img src="./sout.gif" alt=""><a href="https://hub.jazz.net/tutorials/jazzeditor" rel="external" title="(Opens in a new tab or window)">Develop and deploy a Node.js app</a></li>
<li><img src="./sout.gif" alt=""><a href="https://hub.jazz.net/tutorials/jazzeditorjava" rel="external" title="(Opens in a new tab or window)">Develop and deploy a Java app</a></li>
-->

<li><img src="./sout.gif" alt=""><a href="http://www.ibm.com/developerworks/topics/delivery%20pipeline%20service" rel="external" title="(새 탭 또는 창에서 열림)">developerWorks: {{site.data.keyword.Bluemix_notm}} {{site.data.keyword.deliverypipeline}} 서비스</a></li>
</ul>
</div>
</aside>
</article>
