---

copyright:
  years: 2015, 2017
lastupdated: "2017-4-28"

---


{:screen: .screen}
{:new_window: target="_blank"}
{:codeblock: .codeblock}
{:shortdesc: .shortdesc}

# {{site.data.keyword.deliverypipeline}}에 대한 작업 {: #pipeline-working}

빌드와 {{site.data.keyword.Bluemix}}에 대한 배치를 자동화하려면 {{site.data.keyword.deliverypipeline}} for {{site.data.keyword.Bluemix_notm}}를 사용하십시오.
{: shortdesc}

{{site.data.keyword.deliverypipeline}}을 사용하면 여러 빌드 유형 중에서 선택할 수 있습니다. 사용자가 빌드 스크립트를
		제공하면 {{site.data.keyword.Bluemix_notm}} {{site.data.keyword.jazzhub_short}}에서 이 스크립트를 실행합니다. 사용자가 빌드 시스템을 설정할
		필요는 없습니다. 그러면 한 번의 클릭으로 하나 또는 다수의 {{site.data.keyword.Bluemix_notm}} 영역, 공용 Cloud Foundry 서버 또는 IBM Containers for {{site.data.keyword.Bluemix_notm}}의 Docker 컨테이너에 앱을 자동적으로 배치할 수 있습니다. 

빌드 작업은 Git 저장소에서 앱 소스 코드를 컴파일하고 패키지합니다. 빌드 작업을 통해 WAR 파일 또는 IBM Containers용 Docker 컨테이너와 같은 배치 가능한 아티팩트가 생성됩니다. 또한, 빌드 내에서 단위 테스트를
				자동으로 실행할 수 있습니다. 커미트가 푸시될 때마다 빌드가 트리거되도록 빌드 작업을 설정할 수 있습니다.

배치 작업은 빌드 작업의 결과물을 가져와 IBM Containers 또는 {{site.data.keyword.Bluemix_notm}}와 같은 Cloud Foundry 서버에 배치합니다. 

하나 또는 다수의 지역과 서비스에 배치할 수 있습니다. 예를 들면, {{site.data.keyword.deliverypipeline}}이 하나 이상의 서비스를 사용하고 한 지역에서 테스트되며 여러 지역의 프로덕션에 배치되도록 설정할 수 있습니다. 자세한 정보는
				[지역](/docs/overview/whatisbluemix.html#ov_intro_reg){: new_window}을 참조하십시오.

오픈 도구 체인에서 여러 개의 파이프라인을 사용하는 경우에는 컴포지트 파이프라인을 작성하여 단일 위치에서 모든 파이프라인의 배치를 관리할 수 있습니다. 

파이프라인 작성 방법은 기존 애플리케이션에 파이프라인을 추가하거나 기존 애플리케이션 없이 파이프라인을 작성하는 등 여러 가지가 있습니다. 조직에 {{site.data.keyword.deliverypipeline}} 서비스가 아직 없는 경우에는 카탈로그로 이동하여 {{site.data.keyword.deliverypipeline}}을 클릭하고 작성을 클릭하십시오.

기존 애플리케이션에 맞게 {{site.data.keyword.deliverypipeline}}을 설정하려면 다음 단계를 완료하십시오. 

1. {{site.data.keyword.Bluemix_notm}} 앱 대시보드에서 앱을 클릭하십시오.
1. {{site.data.keyword.Bluemix_notm}} 메뉴 표시줄의 메뉴에서 **서비스**를 클릭한 후 **DevOps**를 클릭하십시오.
1. **파이프라인**을 클릭한 후 **파이프라인 작성**을 클릭하십시오.

Cloud Foundry 애플리케이션을 배치하도록 구성된 [파이프라인 작성 ![외부 링크 아이콘](../../icons/launch-glyph.svg "외부 링크 아이콘")](https://console.ng.bluemix.net/devops/pipelines/dashboard/create){: new_window}을 수행하려면 다음 단계를 따르십시오. 

1. **Cloud Foundry**를 클릭하십시오.
1. 파이프라인에 다른 이름을 사용하려면 파이프라인의 기본 이름을 변경하십시오. 
1. 애플리케이션에 다른 이름을 사용하려면 애플리케이션의 기본 이름을 변경하십시오. 이 이름은 파이프라인이 배치하는 대상 애플리케이션입니다.
1. 도구 체인이 없는 경우에는 기본 이름의 도구 체인이 작성됩니다. 도구 체인에 다른 이름을 사용하려면 도구 체인의 기본 이름을 변경하십시오. 도구 체인을 사용하면 기타 도구 및 서비스와 통합하여 파이프라인의 기능을 확장할 수 있습니다.도구 체인에 대한 자세한 정보는 [도구 체인 관련 작업](/docs/services/ContinuousDelivery/toolchains_working.html){: new_window}을 참조하십시오. 

 **팁**: 파이프라인과 도구 체인은 조직(orgs)에 속합니다. 도구 체인이 있는 조직에 속하는 경우, 사용자는 이와 연관된 도구 체인의 액세스 제어 목록에 추가될 수 있습니다. 도구 체인의 액세스 제어 목록에 추가되면 직접 작성하지 않았어도 해당 도구 체인 및 이와 연관된 파이프라인을 사용할 수 있습니다. 도구 체인의 액세스 제어에 대한 자세한 정보는 [액세스 관리](/docs/services/ContinuousDelivery/toolchains_using.html#managing_access){: new_window}를 참조하십시오. 

1. 사용할 도구 체인을 선택하거나 작성하려는 새 도구 체인의 이름을 입력하십시오.
1. Git 제공자를 선택하십시오. 

 **팁**: {{site.data.keyword.Bluemix_notm}}에 GitHub에 액세스하는 권한을 부여하지 않은 경우 **권한 부여**를 클릭하여 GitHub 웹 사이트로 이동하도록 프롬프트가 표시됩니다. 활성 GitHub 세션이 없으면 로그인을 요구하는 프롬프트가 표시됩니다. **애플리케이션에 권한 부여**를 클릭하여 {{site.data.keyword.Bluemix_notm}}에서 사용자의 GitHub 계정에 액세스할 수 있도록 허용하십시오. 활성 GitHub 세션이 있지만 최근에 비밀번호를 입력하지 않은 경우 확인을 위해 GitHub 비밀번호 입력을 요구하는 프롬프트가 표시될 수 있습니다. 

   * 저장소가 있으며 이를 사용하려면 저장소 유형에 대해 **링크**를 선택하십시오. 저장소의 위치를 검색하거나 사용 가능한 저장소 목록에서 저장소를 선택하십시오.

   * 비어 있는 저장소를 작성하려면 저장소 유형에 대해 **새로 작성**을 선택하십시오. 저장소의 이름을 입력하십시오.

   * 저장소의 복제본을 작성하려면 저장소 유형에 대해 **복사**를 선택하십시오. 저장소의 위치를 검색하거나 사용 가능한 저장소 목록에서 저장소를 선택하십시오.

   * 가져오기 요청을 통해 변경사항을 제공할 수 있도록 저장소를 분기하려면 **분기**를 선택하십시오. 저장소의 위치를 검색하거나 사용 가능한 저장소 목록에서 저장소를 선택하십시오.

1. 저장소를 선택하거나 저장소 URL을 입력하십시오. 
1. **작성**을 클릭하십시오.  도구 체인의 개요 페이지에 파이프라인이 작성되고 구성되어 표시됩니다.
 ![파이프라인 카드](images/cd_pipeline.png)
1. 컴포지트 파이프라인이 포함된 도구 체인에서 파이프라인을 작성한 경우에는 새 파이프라인이 컴포지트 파이프라인에 추가됩니다. 새 파이프라인의 배치 태스크가 포함되도록 배치 플랜을 수정하십시오. [Delivery Pipeline 작성 태스크](/docs/services/ContinuousDelivery/pipeline_deployment_plan.html#tasks_pipelineCD){: new_window}를 참조하십시오. 

사전 구성된 단계 없이 [비어 있는 파이프라인 ![외부 링크 아이콘](../../icons/launch-glyph.svg "외부 링크 아이콘")](https://console.ng.bluemix.net/devops/pipelines/dashboard/create){: new_window}을 작성하려면 다음을 수행하십시오. 

1. **사용자 정의**를 클릭하십시오.
1. 파이프라인에 다른 이름을 사용하려면 파이프라인의 기본 이름을 변경하십시오. 
1. 도구 체인이 없는 경우에는 기본 이름의 도구 체인이 작성됩니다. 도구 체인에 다른 이름을 사용하려면 도구 체인의 기본 이름을 변경하십시오. 도구 체인을 사용하면 기타 도구 및 서비스와 통합하여 파이프라인의 기능을 확장할 수 있습니다.
1. 사용할 도구 체인을 선택하거나 작성하려는 새 도구 체인의 이름을 입력하십시오.
1. **작성**을 클릭하십시오. 비어 있는 파이프라인이 작성되며 도구 체인의 개요 페이지에 카드로서 표시됩니다. 

{{site.data.keyword.deliverypipeline}}에서 구성을 변경하십시오. 빌드 상태, 배치된 앱 및 최근 배치를 확인하십시오. 최신 로그와 배치 세부사항을 확인하거나 파이프라인을 삭제하십시오. 
