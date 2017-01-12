---



copyright:

  years: 2015, 2016



---


{:screen: .screen}
{:new_window: target="_blank"}
{:codeblock: .codeblock}
{:shortdesc: .shortdesc}

# {{site.data.keyword.deliverypipeline}}에 대한 작업 {: #pipeline-working}  

마지막 업데이트 날짜: 2016년 11월 18일
{: .last-updated}

빌드와 {{site.data.keyword.Bluemix}}에 대한 배치를 자동화하려면 {{site.data.keyword.deliverypipeline}} for {{site.data.keyword.Bluemix_notm}}를 사용하십시오.
{: shortdesc}

{{site.data.keyword.deliverypipeline}}을 사용하면 여러 빌드 유형 중에서 선택할 수 있습니다. 사용자가 빌드 스크립트를
		제공하면 {{site.data.keyword.Bluemix_notm}} {{site.data.keyword.jazzhub_short}}에서 이 스크립트를 실행합니다. 사용자가 빌드 시스템을 설정할
		필요는 없습니다. 그러면 한 번의 클릭으로 하나 또는 다수의 {{site.data.keyword.Bluemix_notm}} 영역, 공용 Cloud Foundry 서버 또는 IBM Containers for {{site.data.keyword.Bluemix_notm}}의 Docker 컨테이너에 앱을 자동적으로 배치할 수 있습니다.   

빌드 작업은 Git 저장소에서 앱 소스 코드를 컴파일하고 패키지합니다. 빌드 작업을 통해 WAR 파일 또는 IBM Containers용 Docker 컨테이너와 같은 배치 가능한 아티팩트가 생성됩니다. 또한, 빌드 내에서 단위 테스트를
				자동으로 실행할 수 있습니다. 커미트가 푸시될 때마다 빌드가 트리거되도록 빌드 작업을 설정할 수 있습니다.

배치 작업은 빌드 작업의 결과물을 가져와 IBM Containers 또는 {{site.data.keyword.Bluemix_notm}}와 같은 Cloud Foundry 서버에 배치합니다.   

하나 또는 다수의 지역과 서비스에 배치할 수 있습니다. 예를 들면, {{site.data.keyword.deliverypipeline}}이 하나 이상의 서비스를 사용하고 한 지역에서 테스트되며 여러 지역의 프로덕션에 배치되도록 설정할 수 있습니다. 자세한 정보는
				[지역](/docs/overview/whatisbluemix.html#ov_intro_reg)을 참조하십시오.

파이프라인 작성 방법은 기존 애플리케이션에 파이프라인을 추가하거나 기존 애플리케이션 없이 파이프라인을 작성하는 등 여러 가지가 있습니다. 조직에 {{site.data.keyword.deliverypipeline}} 서비스가 아직 없는 경우에는 카탈로그로 이동하여 {{site.data.keyword.deliverypipeline}}을 클릭하고 작성을 클릭하십시오.

기존 애플리케이션에 맞게 {{site.data.keyword.deliverypipeline}}을 설정하려면 다음 단계를 완료하십시오.     

1. {{site.data.keyword.Bluemix_notm}} 앱 대시보드에서 앱을 클릭하십시오.
1. {{site.data.keyword.Bluemix_notm}} 메뉴 표시줄의 햄버거 메뉴에서 **서비스**를 클릭한 후 **DevOps**를 클릭하십시오.
1. **파이프라인**을 클릭한 후 **파이프라인 작성**을 클릭하십시오.

Cloud Foundry 애플리케이션을 배치하도록 구성된 [파이프라인 작성(링크가 새 창에서 열림)](https://console.ng.bluemix.net/devops/pipelines/dashboard/create){: new_window}을 수행하려면 다음 단계를 수행하십시오.    

1. **Cloud Foundry**를 클릭하십시오.  
1. 파이프라인에 다른 이름을 사용하려면 파이프라인의 기본 이름을 변경하십시오.  
1. 애플리케이션에 다른 이름을 사용하려면 애플리케이션의 기본 이름을 변경하십시오. 이 이름은 파이프라인이 배치하는 대상 애플리케이션입니다. 
1. 도구 체인이 없는 경우에는 기본 이름의 도구 체인이 작성됩니다. 도구 체인에 다른 이름을 사용하려면 도구 체인의 기본 이름을 변경하십시오. 도구 체인을 사용하면 기타 도구 및 서비스와 통합하여 파이프라인의 기능을 확장할 수 있습니다.

 **팁**: 파이프라인과 도구 체인은 조직(orgs)에 속합니다. 사용자가 도구 체인이 있는 조직에 속해 있으면 도구 체인을 작성하지 않은 경우에도 조직의 도구 체인을 사용할 수 있습니다.
 
1. 사용할 도구 체인을 선택하거나 작성하려는 새 도구 체인의 이름을 입력하십시오.
1. GitHub 저장소의 위치를 제공하십시오.

 **팁**: {{site.data.keyword.Bluemix_notm}}에 GitHub에 액세스하는 권한을 부여하지 않은 경우 **권한 부여**를 클릭하여 GitHub 웹 사이트로 이동하도록 프롬프트가 표시됩니다. 활성 GitHub 세션이 없으면 로그인을 요구하는 프롬프트가 표시됩니다. **애플리케이션에 권한 부여**를 클릭하여 {{site.data.keyword.Bluemix_notm}}에서 사용자의 GitHub 계정에 액세스할 수 있도록 허용하십시오. 활성 GitHub 세션이 있지만 최근에 비밀번호를 입력하지 않은 경우 확인을 위해 GitHub 비밀번호 입력을 요구하는 프롬프트가 표시될 수 있습니다. 

   * GitHub 저장소가 있으며 이 저장소를 사용하려는 경우 저장소 유형에서 **링크**를 선택하십시오. 저장소의 위치를 검색하거나 사용 가능한 저장소 목록에서 저장소를 선택하십시오.
   
   * 빈 GitHub 저장소를 작성하려면 저장소 유형에서 **새로 작성**을 선택하십시오. 저장소의 이름을 입력하십시오.
   
   * GitHub 저장소의 복제본을 작성하려면 저장소 유형에서 **복사**를 선택하십시오. 저장소의 위치를 검색하거나 사용 가능한 저장소 목록에서 저장소를 선택하십시오.
   
   * 가져오기 요청을 통해 변경사항을 컨트리뷰션할 수 있도록 GitHub 저장소를 분기시키려면 **분기**를 선택하십시오. 저장소의 위치를 검색하거나 사용 가능한 저장소 목록에서 저장소를 선택하십시오.
 
1. **작성**을 클릭하십시오. 도구 체인의 개요 페이지에 파이프라인이 작성되고 구성되어 표시됩니다.
 ![파이프라인 타일](images/cd_pipeline.png)

사전 구성된 단계 없이 [빈 파이프라인(링크가 새 창에서 열림)](https://console.ng.bluemix.net/devops/pipelines/dashboard/create){: new_window}을 작성하려면 다음을 수행하십시오.

1. **사용자 정의**를 클릭하십시오.
1. 파이프라인에 다른 이름을 사용하려면 파이프라인의 기본 이름을 변경하십시오.  
1. 도구 체인이 없는 경우에는 기본 이름의 도구 체인이 작성됩니다. 도구 체인에 다른 이름을 사용하려면 도구 체인의 기본 이름을 변경하십시오. 도구 체인을 사용하면 기타 도구 및 서비스와 통합하여 파이프라인의 기능을 확장할 수 있습니다.
1. 사용할 도구 체인을 선택하거나 작성하려는 새 도구 체인의 이름을 입력하십시오.
1. **작성**을 클릭하십시오. 도구 체인의 개요 페이지에 빈 파이프라인이 작성되고 타일로 표시됩니다.

{{site.data.keyword.deliverypipeline}} 타일에서 구성을 변경하십시오. 빌드, 배치된 앱, 최근 배치의 상태를 검사하고 최신 로그와 배치 세부사항을 확인하거나 파이프라인을 삭제하십시오.  

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
