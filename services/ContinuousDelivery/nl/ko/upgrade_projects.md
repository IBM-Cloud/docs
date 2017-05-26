---

copyright:
  years: 2015, 2017
lastupdated: "2017-5-10"

---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}

# {{site.data.keyword.jazzhub_short}} 프로젝트를 도구 체인으로 업그레이드
{: #upgrade_projects}

{{site.data.keyword.jazzhub}}는 {{site.data.keyword.contdelivery_full}}로 진화 중입니다. 해당 변경사항의 일부로서 프로젝트는 도구 체인으로 업그레이드됩니다. 

사용자는 프로젝트를 업그레이드할 수 있으며, 또는 프로젝트가 자동으로 업그레이드될 때까지 대기할 수 있습니다. 최상의 환경을 위해서는 [필수 소프트웨어](#upgrade_prereqs)를 만족하는지 확인하고 도구 체인의 이름이 무엇인지와 이 도구 체인이 작성되는 조직을 제어할 수 있도록 가급적 빨리 프로젝트를 업그레이드하십시오.
{: shortdesc}

## 도구 체인
{: #compare_toolchains}

도구 체인은 프로젝트와 유사하지만 일부 중요한 차이점이 있습니다. 

- 프로젝트에는 오직 하나의 저장소(repo)와 파이프라인만 있을 수 있습니다. 도구 체인에는 필요한 수 만큼의 저장소와 파이프라인이 있을 수 있습니다. 
- 도구 체인에는 프로젝트에서 사용 가능하지 않은 도구가 포함될 수 있습니다(예: Slack, Sauce Labs, PagerDuty 및 {{site.data.keyword.DRA_full}}). 
- 도구 체인에 대한 액세스는 표준 {{site.data.keyword.Bluemix_notm}} 조직을 통해 관리됩니다. 프로젝트 레벨에서 멤버십이 유지되는 프로젝트와는 달리, 멤버십이 조직 레벨에서 유지됩니다. 

[YouTube ![외부 링크 아이콘](../../icons/launch-glyph.svg "외부 링크 아이콘")](https://youtu.be/2SIPE1e7NJ4){: new_window}에서 또는 [{{site.data.keyword.contdelivery_short}} 시작하기](/docs/services/ContinuousDelivery/index.html)에서 도구 체인에 대해 알아볼 수 있습니다.
[![YouTube에 대한 외부 링크](images/CD_video.png)](https://youtu.be/2SIPE1e7NJ4){: new_window}

## 전제조건
{: #upgrade_prereqs}

- 업그레이드된 프로젝트의 도구 체인에 액세스하려면 {{site.data.keyword.Bluemix_notm}} ID가 필요합니다. 업그레이드 전에 활성 {{site.data.keyword.Bluemix_notm}} ID가 있는지 확인하십시오. ID가 없으면 이를 [등록](https://console.ng.bluemix.net/registration/)하십시오. 
- {{site.data.keyword.jazzhub_short}} 프로젝트 소유자가 올바른지 확인하십시오. 프로젝트에서 작성되는 도구 체인은 해당 소유자의 {{site.data.keyword.Bluemix_notm}} 조직의 일부가 됩니다. 
- 업그레이드를 시작하려는 경우 사용자가 파이프라인이 배치하는 모든 조직과 공간의 구성원인지 확인하십시오. 임의의 프로젝트 관리자가 업그레이드를 시작할 수 있습니다. 그러나 업그레이드를 시작하는 관리자가 파이프라인이 배치하는 모든 조직과 공간의 구성원이 아니면 파이프라인을 작성할 수 없습니다. 업그레이드를 시작하는 사용자가 도구 체인에서 저장소의 소유자가 됩니다.
- 도구 체인의 Eclipse Orion {{site.data.keyword.webide}}는 사용자의 프로젝트와 연관된 {{site.data.keyword.webide}}와는 별개입니다. {{site.data.keyword.webide}}를 사용 중이며 커미트되지 않은 변경사항이 있는 경우에는 업그레이드 전에 이를 커미트하십시오. 


## 프로젝트에서 도구 체인으로 업그레이드
{: #project_to_toolchain}

**중요:** hub.jazz.net의 프로젝트와 도구 체인은 모두 미국 남부 지역에서 호스팅됩니다. 다른 지역에 앱을 배치하도록 프로젝트가 구성된 경우 도구 체인으로 업그레이드한 후에도 앱이 해당 지역으로 배치됩니다.

프로젝트의 업그레이드가 준비되면 메시지가 프로젝트의 카드 및 개요 페이지에 표시됩니다. 

![업그레이드 준비 완료 레이블이 있는 카드의 이미지](images/card-project-to-upgrade.png)

![업그레이드할 시간 메시지](images/banner-ready-to-upgrade.png)

**팁:** 내 프로젝트 페이지의 메뉴에서 업그레이드가 준비된 프로젝트를 찾을 수 있습니다. 

![업그레이드할 프로젝트 메뉴 항목의 이미지](images/menu-projects-to-upgrade.png)

업그레이드를 시작하면 프로젝트의 파이프라인 스테이지가 잠깁니다. 스테이지를 실행하거나 수정할 수 없습니다. 도구 체인을 삭제하여 업그레이드를 되돌리면 파이프라인의 잠금이 해제됩니다.

프로젝트에서 JazzHub에서 호스팅된 Git 저장소를 사용하는 경우 업그레이드를 시작하고 나면 도구 체인으로 이동된 데이터의 무결성을 위해 저장소가 잠깁니다. 도구 체인을 삭제하여 업그레이드를 되돌리면 JazzHub의 저장소가 잠금 해제됩니다.

## 업그레이드 프로세스 시작
{: #start_upgrade}

업그레이드 프로세스를 시작하기 전에, 사용자는 [YouTube ![외부 링크 아이콘](../../icons/launch-glyph.svg "외부 링크 아이콘")](https://youtu.be/LSr2e3uvyLs){: new_window}에서 업그레이드가 어떻게 진행되는지를 지켜볼 수 있습니다.
[![YouTube에 대한 외부 링크](images/migration-video2.png)](https://youtu.be/LSr2e3uvyLs){: new_window}

프로젝트를 도구 체인으로 업그레이드하려면 다음 단계를 따르십시오. 

1. 업그레이드 프로세스를 시작하려면 배너 메시지에서 **지금 업그레이드**를 클릭하십시오. "프로젝트 업그레이드 도구 체인" 페이지가 열립니다. 

   ![업그레이드 페이지의 예](images/project-upgrade-toolchain.png)

   업그레이드 프로세스의 개요를 보려면 해당 페이지의 설명을 읽으십시오. 도구 체인에는 프로젝트의 파이프라인과 동일한 단계 및 작업이 포함된 새 파이프라인이 포함됩니다. 또한 도구 체인에는 {{site.data.keyword.contdelivery_short}}에서 실행되는 Eclipse Orion {{site.data.keyword.webide}}에 대한 포인터가 포함됩니다. 

   이 예에서는 프로젝트가 github.com의 공용 저장소를 사용하므로 도구 체인이 동일한 GitHub 저장소에 연결됩니다. 프로젝트가 JazzHub에서 호스팅된 Git 저장소를 사용하는 경우 해당 저장소의 컨텐츠가 {{site.data.keyword.contdelivery_short}}의 일부인 {{site.data.keyword.gitrepos}}의 새 저장소에 복제됩니다. 각 저장소 유형을 취급하는 방법에 대한 자세한 정보는 다음 테이블을 참조하십시오.

|프로젝트 저장소 |프로젝트 유형	|도구 체인 저장소 |
|:----------|:------------------------------|:------------------|
|github.com 		|사설 또는 공용 		|{{site.data.keyword.Bluemix_notm}} Public과 동일한 github.com 저장소.	|
|hub.jazz.net/git		|사설 또는 공용 		|{{site.data.keyword.Bluemix_notm}} Public이 있는 {{site.data.keyword.gitrepos}}의 새 저장소.	|
{: caption="표 1. 도구 체인 저장소에 맵핑된 프로젝트 저장소" caption-side="top"}

2. 도구 체인을 사용자 정의하기 위해 일부 설정을 구성할 수 있습니다. 

   - 도구 체인의 이름을 변경하려면 **이름** 필드를 편집하십시오. 

      ![이름 필드](images/name-change.png)

   -   도구 체인이 작성될 {{site.data.keyword.Bluemix_notm}} 조직을 변경하려면 계정 메뉴에서 조직을 선택하십시오. 

      ![Bluemix 조직 선택자](images/bluemix-organization-chooser.png)

   도구 체인이 조직 레벨에서 관리되므로, 도구 체인에 액세스해야 하는 프로젝트 구성원이 이미 존재하거나 별도로 추가될 수 있는 조직을 선택했는지 확인하십시오. 

3. 프로젝트에서 추적 및 플랜을 사용한 경우 추적 및 플랜 데이터를 GitHub Issues에 전송할 수 있습니다.

   ![추적 및 플랜 옵션](images/upgrade-tutorial-track-and-plan.png)

   - 추적 및 플랜 데이터를 마이그레이션할지 표시합니다.
   - 기본적으로 모든 추적 및 플랜 데이터가 마이그레이션됩니다. 특정 조회의 일부인 작업 항목만 마이그레이션하려면 해당 조회를 지정하십시오.
   - GitHub Issues의 레이블에 맵핑할 작업 항목 속성을 선택하십시오.

4. **작성**을 클릭하십시오. 새 도구 체인이 작성되며 해당 개요 페이지가 표시됩니다. 

   ![업그레이드된 도구 체인의 개요](images/new-toolchain-page.png)

   - GitHub 저장소 또는 연관된 문제 트래커에 액세스하려면 **GitHub** 또는 **Issues**를 클릭하십시오. 
   - 파이프라인에 액세스하려면 **Delivery Pipeline**을 클릭하십시오. 
   - 작업공간으로 체크아웃된 저장소의 컨텐츠가 포함된 {{site.data.keyword.webide}}에 액세스하려면 **Eclipse Orion {{site.data.keyword.webide}}**를 클릭하십시오. 

   업그레이드 중에 프로젝트로 돌아가려고 하면 배너 메시지에 업그레이드가 진행 중임을 표시할 수 있습니다. 특히 업그레이드 프로세스에서 소스 코드를 새 저장호로 가져오거나 추적 및 계획 작업 항목을 문제로 가져오는 경우가 해당됩니다.

   ![도구 체인으로 업그레이드하는 프로젝트에 대한 메시지](images/project-being-upgraded-banner.png)

## 프로젝트 재방문
{: #revisit_projects}

새 도구 체인을 사용할 준비가 되었습니다. 이제 프로젝트에는 "업그레이드됨"으로 레이블이 지정되어 있으며 개요 페이지에서 확인 메시지가 표시됩니다. 

!["업그레이드됨" 레이블이 있는 프로젝트 카드의 이미지](images/card-upgraded-project.png)

![업그레이드된 프로젝트](images/banner-upgraded.png)

내 프로젝트 페이지의 메뉴에서 **업그레이드된 프로젝트**를 선택하여 업그레이드된 프로젝트를 볼 수 있습니다. 

![업그레이드된 프로젝트 메뉴 항목의 이미지](images/menu-upgraded-projects.png)

업그레이드를 되돌려야 하는 경우에는 도구 체인을 삭제하십시오. 도구 체인의 개요 페이지에 있는 **추가 조치** 메뉴에서 도구 체인을 삭제할 수 있습니다.

![추가 조치 메뉴의 삭제 조치 이미지](images/upgrade-tutorial-delete-toolchain.png)

프로젝트로 돌아가면 업그레이드 메시지가 다시 표시되며, 준비가 되었을 때 다시 업그레이드가 가능합니다. 

## 다음 단계
{: #upgrade_next_steps}

1. 브라우저를 새로 고치고 프로젝트 개요 페이지에서 프로젝트가 "이 도구 체인으로 업그레이드"되었다는 메시지를 확인하여 업그레이드가 완료되었는지 확인하십시오.

   ![프로젝트가 업그레이드되었음을 나타내는 배너의 메시지](images/banner-upgraded.png)

   **참고:** 메시지에서 "지금 업그레이드"를 표시하면 업그레이드에 실패한 것입니다. **지금 업그레이드** 링크를 클릭하여 다시 시도하십시오.

   ![프로젝트를 업그레이드할 준비가 되었음을 표시하는 배너의 메시지](images/banner-ready-to-upgrade.png)

2. 팀 구성원에게 도구 체인에 대한 액세스 권한을 부여하십시오. 
    - 각 팀 구성원은 유효한 {{site.data.keyword.Bluemix_notm}} 계정을 보유해야 합니다. 계정이 없는 팀 구성원은 [등록 ![외부 링크 아이콘](../../icons/launch-glyph.svg "외부 링크 아이콘")](https://console.ng.bluemix.net/registration){:new_window}이 필요합니다. 
    - 도구 체인 관리 페이지에서 조직(org) 구성원에게 도구 체인에 액세스하는 권한을 부여하십시오. 도구 체인의 액세스 제어에 대한 자세한 정보는 [액세스 관리 ![외부 링크 아이콘](../../icons/launch-glyph.svg "외부 링크 아이콘")](/docs/services/ContinuousDelivery/toolchains_using.html#managing_access){:new_window}을 참조하십시오.
    - 사용자가 도구 체인이 속한 조직의 구성원이 아니면 조직 관리 페이지에서 조직에 사용자를 추가하십시오.
      조직 관리에 대한 자세한 정보는 [조직 및 공간 관리 ![외부 링크 아이콘](../../icons/launch-glyph.svg "외부 링크 아이콘")](/docs/admin/orgs_spaces.html#orgsspacesusers){:new_window}을 참조하십시오.

3. {{site.data.keyword.jazzhub_short}} 프로젝트의 도구가 아닌 도구 체인의 도구를 사용하십시오. 예를 들어, 브라우저에서 코드를 편집하려면 도구 체인의 Web IDE를 사용하십시오. 

4. {{site.data.keyword.gitrepos}}를 사용하는 경우 개인 액세스 토큰 또는 SSH 키를 사용하여 인증하십시오. SSH 키에 대한 자세한 정보는 [인증을 위한 개인 액세스 토큰 또는 SSH 키 작성](/docs/services/ContinuousDelivery/git_working.html#git_authentication)을 참조하십시오. https를 통해 외부 Git 클라이언트에서 인증하려면 다음 단계를 따르십시오.
    1. {{site.data.keyword.gitrepos}} 사용자 설정의 [액세스 토큰 페이지 ![외부 링크 아이콘](../../icons/launch-glyph.svg "외부 링크 아이콘")](https://git.ng.bluemix.net/profile/personal_access_tokens){:new_window}로 이동하십시오.
    2. **api**를 범위로 사용하는 개인 액세스 토큰을 작성하십시오.
    3. [계정 페이지 ![외부 링크 아이콘](../../icons/launch-glyph.svg "외부 링크 아이콘")](https://git.ng.bluemix.net/profile/account){:new_window}으로 이동하고 {{site.data.keyword.gitrepos}}의 사용자 이름을 찾으십시오. 사용자 이름이 "사용자 이름 변경" 섹션에 나열되며 사용자가 작성한 개인 저장소 URL의 첫 번째 부분으로 표시됩니다.
    4. https를 통해 외부 Git 클라이언트에서 {{site.data.keyword.gitrepos}}를 인증하려면 사용자 이름과 개인 액세스 토큰을 사용하십시오.
    5. JazzHub Git 저장소의 로컬 저장소를 재사용하려면 저장소가 {{site.data.keyword.gitrepos}}의 새 저장소를 가리키게 지정하십시오. 터미널의 쉘에서 JazzHub Git 저장소가 복제된 디렉토리로 변경하십시오. `git remote set-url` 명령을 입력하십시오. `git remote set-url origin https://git.ng.bluemix.net/<userid>/<name-of-new-repo>`

        **팁:** 어떤 원격 URL이 어떤 원격 이름으로 설정되었는지 확인하려면 `git remote -v` 명령을 사용하십시오. 기본 원격 이름은 `origin`입니다. 고급 설정이 있으면 명령의 형식은 다음과 같습니다. `git remote set-url <remote-name-that-uses-jazzhub-repo> https://git.ng.bluemix.net/<userid>/<name-of-new-repo>`

5. 도구 체인이 설정되어 있고 이 도구 체인을 사용하도록 시작한 경우 다른 사용자가 프로젝트를 사용하지 않도록 다음 단계 중 일부 또는 모두를 수행하십시오.
    - 프로젝트 이름에 접미부를 추가하여 해당 프로젝트를 사용하지 않아야 함을 표시하십시오. 프로젝트 이름의 끝에 `_DO_NOT_USE`를 추가할 수 있습니다.
    - 프로젝트의 설명을 업데이트하여 프로젝트가 더 이상 사용되지 않음을 표시하고 도구 체인의 포인터를 추가하십시오.
    - 프로젝트에서 구성원을 제거하십시오.
    - 더 이상 프로젝트가 필요하지 않으면 삭제하십시오.

6. 선택사항: 프로젝트의 개발 성숙도, 팀의 사례 및 코드 베이스 품질을 탐색하려면 IBM Cloud {{site.data.keyword.DRA_short}}를 도구 체인에 추가하십시오. {{site.data.keyword.DRA_short}}에서는 개발자, 팀 및 배치 분석을 DevOps 프로젝트에 적용합니다. 자세한 정보는 [{{site.data.keyword.DRA_short}} 시작하기](/docs/services/DevOpsInsights/index.html)를 참조하십시오.


## 문제점 해결
{: #upgrade_troubleshoot}

질문이나 문제점이 있으면 [지원 포럼](https://developer.ibm.com/answers/questions/ask/?smartspace=devops-services)에 문의하십시오. 포럼 게시물에 {{site.data.keyword.jazzhub_short}} 프로젝트와 {{site.data.keyword.contdelivery_short}} 도구 체인의 URL을 포함시키고 `devops-services` 태그로 게시물의 태그를 지정하십시오.
