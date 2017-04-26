---

copyright:
  years: 2015, 2017
lastupdated: "2017-3-31"

---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}

# Continuous Delivery 시작하기
{: #cd_getting_started}

애플리케이션의 빌드와 배치를 자동화하는 오픈 도구 체인이 포함된 {{site.data.keyword.contdelivery_full}}를 사용하여 DevOps 접근 방법을 채택합니다. 개발, 배치, 운영 태스크를 지원하는 단순 배치 도구 체인을 작성하여 시작할 수 있습니다.
{: shortdesc}

{{site.data.keyword.contdelivery_short}}의 인스턴스를 {{site.data.keyword.Bluemix_notm}} 카탈로그에서 선택하여 이를 작성한 후에는 서비스를 시작하는 방법을 선택할 수 있습니다.
 ![Continuous Delivery 시작 페이지](images/cd_landing_page.png)

 * 자동화된 파이프라인을 사용하여 애플리케이션을 빨리 시작하고 배치하려면 "파이프라인을 사용하여 시작" 섹션에서 **[여기서 시작](#starting_with_a_pipeline)**을 클릭하십시오. 나중에 도구를 추가할 수 있습니다.
 * 템플리트를 사용하여 Continuous Delivery 도구 체인을 작성하고 구성하려면 "도구 체인 템플리트에서 시작" 섹션에서 **[여기서 시작](#starting_from_a_toolchain_template)**을 클릭하십시오. 도구 체인은 파이프라인의 계획, 개발, 배치와 애플리케이션의 관리에 사용할 도구를 통합합니다. 언제나 도구 체인에서 도구를 추가하거나 제거할 수 있습니다.
 * 도구 체인이 이미 있는 경우에는 "도구 체인 템플리트에서 시작" 섹션에서 **도구 체인 보기**를 클릭하십시오. 도구 체인 관련 작업에 대한 자세한 정보는 [도구 체인 사용](/docs/services/ContinuousDelivery/toolchains_using.html){: new_window}을 참조하십시오. 

**팁**: 파이프라인은 도구 체인에 의해 관리됩니다. 기존 도구 체인에 파이프라인을 추가할 수 있습니다. 파이프라인을 작성하며 기존 도구 체인이 없는 경우에는 기본 이름의 도구 체인이 사용자를 위해 작성됩니다. 도구 체인을 사용하면 기타 도구 및 서비스와 통합하여 파이프라인의 기능을 확장할 수 있습니다. 

##파이프라인을 사용하여 시작
{: #starting_with_a_pipeline}

파이프라인은 빌드와 배치 등을 자동화합니다. 자동화된 파이프라인을 사용하여 시작하려면 템플리트를 선택하고 GitHub 저장소(repo)의 위치를 제공하십시오.

Cloud Foundry 애플리케이션을 배치하도록 구성된 [파이프라인 작성 ![외부 링크 아이콘](../../icons/launch-glyph.svg "외부 링크 아이콘")](https://console.ng.bluemix.net/devops/pipelines/dashboard/create){:new_window}을 수행하려면 다음 단계를 따르십시오. 

1. **Cloud Foundry**를 클릭하십시오.
1. 파이프라인에 다른 이름을 사용하려면 파이프라인의 기본 이름을 변경하십시오. 파이프라인의 이름은 {{site.data.keyword.Bluemix_notm}}에서 해당 파이프라인을 식별합니다.
1. 애플리케이션에 다른 이름을 사용하려면 애플리케이션의 기본 이름을 변경하십시오. 애플리케이션의 이름은 {{site.data.keyword.Bluemix_notm}}에서 해당 애플리케이션을 식별합니다. 이 이름은 파이프라인이 배치하는 대상 애플리케이션입니다.
1. 도구 체인이 없는 경우에는 기본 이름의 도구 체인이 작성됩니다. 도구 체인에 다른 이름을 사용하려면 도구 체인의 기본 이름을 변경하십시오. 도구 체인에서 파이프라인을 관리합니다. 도구 체인을 사용하면 기타 도구 및 서비스와 통합하여 파이프라인의 기능을 확장할 수 있습니다.

 **팁**: 파이프라인과 도구 체인은 조직(orgs)에 속합니다. 사용자가 도구 체인이 있는 조직에 속해 있으면 도구 체인을 작성하지 않은 경우에도 조직의 도구 체인을 사용할 수 있습니다.

1. 사용할 도구 체인을 선택하거나 작성하려는 새 도구 체인의 이름을 입력하십시오.
1. Git 제공자를 선택하십시오. 

 **팁**: {{site.data.keyword.Bluemix_notm}}에 GitHub에 액세스하는 권한을 부여하지 않은 경우 **권한 부여**를 클릭하여 GitHub 웹 사이트로 이동하도록 프롬프트가 표시됩니다. 활성 GitHub 세션이 없으면 로그인을 요구하는 프롬프트가 표시됩니다. **애플리케이션에 권한 부여**를 클릭하여 {{site.data.keyword.Bluemix_notm}}에서 사용자의 GitHub 계정에 액세스할 수 있도록 허용하십시오. 활성 GitHub 세션이 있지만 최근에 비밀번호를 입력하지 않은 경우 확인을 위해 GitHub 비밀번호 입력을 요구하는 프롬프트가 표시될 수 있습니다. 

 {{site.data.keyword.ghe_short}} 저장소에 액세스할 권한이 없으면 저장소에 대한 관리자 권한이 있는 사용자에 의해 추가되어야 합니다. {{site.data.keyword.ghe_short}}용 {{site.data.keyword.Bluemix_notm}} 데디케이티드의 권한 부여에 대한 지시사항은 [{{site.data.keyword.ghe_short}}용 {{site.data.keyword.Bluemix_notm}} 데디케이티드 시작하기](/docs/services/ghededicated/index.html){: new_window}를 참조하십시오. {{site.data.keyword.ghe_short}}의 자체 관리 버전의 권한 부여가 필요하면 내부 프로시저를 따르십시오. 

   * 저장소가 있으며 이를 사용하려면 저장소 유형에 대해 **링크**를 선택하십시오. 저장소의 위치를 검색하거나 사용 가능한 저장소 목록에서 저장소를 선택하십시오.

   * 비어 있는 저장소를 작성하려면 저장소 유형에 대해 **새로 작성**을 선택하십시오. 저장소의 이름을 입력하십시오.

   * 저장소의 복제본을 작성하려면 저장소 유형에 대해 **복사**를 선택하십시오. 저장소의 위치를 검색하거나 사용 가능한 저장소 목록에서 저장소를 선택하십시오.

   * 가져오기 요청을 통해 변경사항을 제공할 수 있도록 저장소를 분기하려면 **분기**를 선택하십시오. 저장소의 위치를 검색하거나 사용 가능한 저장소 목록에서 저장소를 선택하십시오.

1. 저장소를 선택하거나 저장소 URL을 입력하십시오. 
1. **작성**을 클릭하십시오.  도구 체인의 개요 페이지에 파이프라인이 작성되고 구성되어 표시됩니다.
 ![파이프라인 카드](images/cd_pipeline.png)

사전 구성된 단계 없이 [비어 있는 파이프라인 ![외부 링크 아이콘](../../icons/launch-glyph.svg "외부 링크 아이콘")](https://console.ng.bluemix.net/devops/pipelines/dashboard/create){: new_window}을 작성하려면 다음을 수행하십시오. 

1. **사용자 정의**를 클릭하십시오.
1. 파이프라인에 다른 이름을 사용하려면 파이프라인의 기본 이름을 변경하십시오. 파이프라인의 이름은 {{site.data.keyword.Bluemix_notm}}에서 해당 파이프라인을 식별합니다.
1. 도구 체인이 없는 경우에는 기본 이름의 도구 체인이 작성됩니다. 도구 체인에 다른 이름을 사용하려면 도구 체인의 기본 이름을 변경하십시오. 도구 체인에서 파이프라인을 관리합니다. 도구 체인을 사용하면 기타 도구 및 서비스와 통합하여 파이프라인의 기능을 확장할 수 있습니다.
1. 사용할 도구 체인을 선택하거나 작성하려는 새 도구 체인의 이름을 입력하십시오.
1. **작성**을 클릭하십시오. 비어 있는 파이프라인이 작성되며 도구 체인의 개요 페이지에 카드로서 표시됩니다. 

##도구 체인 템플리트에서 시작
{: #starting_from_a_toolchain_template}

[템플리트 ![외부 링크 아이콘](../../icons/launch-glyph.svg "외부 링크 아이콘")](https://console.ng.bluemix.net/devops/create){: new_window}에서 지속적 딜리버리 도구 체인을 작성하고 구성하려면 다음을 수행하십시오. 

1. **도구 체인 작성** 페이지에서 도구 체인 템플리트를 클릭하십시오.   
1. 작성하려는 도구 체인의 다이어그램을 검토하십시오. 다이어그램은 도구 체인에서 해당 라이프사이클 단계(Phase)에 있는 각 도구 통합을 보여줍니다. 

 **팁**: 일부 도구 체인 템플리트에는 도구 통합의 여러 인스턴스가 있습니다. 예를 들어, {{site.data.keyword.Bluemix_notm}} 퍼블릭의 마이크로서비스 도구 체인 템플리트에는 3개 마이크로서비스 각각에 대해 하나씩 GitHub의 3개 인스턴스와 Delivery Pipeline의 3개 인스턴스가 포함되어 있습니다. 

 다음 이미지의 다이어그램을 예로 들 수 있습니다. 도구 체인을 작성할 때 다이어그램은 도구 체인의 일부인 각 도구 통합을 표시합니다.
![Toolchain_diagram](images/toolchain_diagram.png)
1. 도구 체인 설정에 대한 기본 정보를 검토하십시오. 도구 체인의 이름은 {{site.data.keyword.Bluemix_notm}}에서 해당 도구 체인을 식별합니다. 다른 이름을 사용하려면 도구 체인의 이름을 변경하십시오.
1. 도구 통합 섹션에서 도구 체인에 대해 구성할 각 도구 통합을 선택하십시오. 몇몇 도구 통합에서는 구성이 필요 없습니다. 도구 통합 구성에 대한 정보는 [도구 통합 구성](/docs/services/ContinuousDelivery/toolchains_integrations.html){: new_window}의 내용을 참조하십시오.
1. **작성**을 클릭하십시오. 여러 단계가 자동으로 실행되어 도구 체인을 설정합니다. 설정된 도구 통합은 선택된 도구 체인 템플리트 및 사용자가 {{site.data.keyword.Bluemix_notm}} 퍼블릭 또는 {{site.data.keyword.Bluemix_notm}} 데디케이티드를 사용 중인지 여부에 따라 다릅니다. 예를 들어, {{site.data.keyword.Bluemix_notm}} 퍼블릭에서 마이크로서비스 도구 체인을 작성하면 다음 단계가 실행됩니다. 

 * 도구 체인이 작성됩니다. 
 * Delivery Pipeline을 구성한 경우에는 파이프라인이 작성되고 실행됩니다. 
 * Sauce Labs를 구성한 경우에는 Sauce Labs 테스트 작업을 파이프라인에 추가하도록 도구 체인이 설정됩니다. 
 * PagerDuty를 구성한 경우에는 경보 알림을 지정된 PagerDuty 서비스에 전송하도록 도구 체인이 설정됩니다. 
 * Slack을 구성한 경우에는 배치 상태에 대한 알림을 지정된 Slack 채널에 전송하도록 도구 체인이 설정됩니다. 
 * GitHub 등의 소스 코드 도구 통합을 구성한 경우에는 샘플 GitHub 저장소가 GitHub 계정으로 복제됩니다. 
