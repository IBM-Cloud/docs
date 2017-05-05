---

copyright:
  years: 2015, 2017
lastupdated: "2017-3-21"

---
 
{:shortdesc: .shortdesc}
{:new_window: target="_blank"}

# {{site.data.keyword.jazzhub_short}} 프로젝트를 도구 체인으로 업그레이드
{: #upgrade_projects}

{{site.data.keyword.jazzhub}}는 {{site.data.keyword.contdelivery_full}}로 진화 중입니다. 해당 변경사항의 일부로서 프로젝트는 도구 체인으로 업그레이드됩니다.  

사용자는 프로젝트를 업그레이드할 수 있으며, 또는 프로젝트가 자동으로 업그레이드될 때까지 대기할 수 있습니다. 최상의 환경을 위해서는 도구 체인의 이름인 무엇인지와 이 도구 체인이 작성되는 조직을 제어할 수 있도록 가급적 빨리 프로젝트를 업그레이드하십시오.   
{: shortdesc}

## 도구 체인
{: #compare_toolchains}

도구 체인은 프로젝트와 유사하지만 일부 중요한 차이점이 있습니다. 

- 프로젝트에는 오직 하나의 저장소(repo)와 파이프라인만 있을 수 있습니다. 도구 체인에는 필요한 수 만큼의 저장소와 파이프라인이 있을 수 있습니다. 
- 도구 체인에는 프로젝트에서 사용 가능하지 않은 도구가 포함될 수 있습니다(예: Slack, Sauce Labs, PagerDuty 및 {{site.data.keyword.DRA_full}}). 
- 도구 체인에 대한 액세스는 표준 Bluemix 조직을 통해 관리됩니다. 프로젝트 레벨에서 멤버십이 유지되는 프로젝트와는 달리, 멤버십이 조직 레벨에서 유지됩니다. 

[YouTube ![외부 링크 아이콘](../../icons/launch-glyph.svg "외부 링크 아이콘")](https://youtu.be/2SIPE1e7NJ4){: new_window}에서 또는 [{{site.data.keyword.contdelivery_short}} 시작하기](/docs/services/ContinuousDelivery/index.html)에서 도구 체인에 대해 알아볼 수 있습니다.
[![YouTube에 대한 외부 링크](images/CD_video.png)](https://youtu.be/2SIPE1e7NJ4){: new_window}    

## 전제조건
{: #upgrade_prereqs}    

- 업그레이드된 프로젝트의 도구 체인에 액세스하려면 Bluemix ID가 필요합니다. 업그레이드 전에 활성 Bluemix ID가 있는지 확인하십시오. ID가 없으면 이를 [등록](https://console.ng.bluemix.net/registration/)하십시오. 
- DevOps Services 프로젝트 소유자가 올바른지 확인하십시오. 프로젝트에서 작성되는 도구 체인은 해당 소유자의 Bluemix 조직의 일부가 됩니다. 

**중요:** 도구 체인의 Eclipse Orion {{site.data.keyword.webide}}는 사용자의 프로젝트와 연관된 {{site.data.keyword.webide}}와는 별개입니다. {{site.data.keyword.webide}}를 사용 중이며 커미트되지 않은 변경사항이 있는 경우에는 업그레이드 전에 이를 커미트하십시오.   


## 프로젝트에서 도구 체인으로 업그레이드
{: #project_to_toolchain}

프로젝트의 업그레이드가 준비되면 메시지가 프로젝트의 카드 및 개요 페이지에 표시됩니다. 

![업그레이드 준비 완료 레이블이 있는 카드의 이미지](images/card-project-to-upgrade.png)

![업그레이드할 시간 메시지](images/banner-ready-to-upgrade.png)

**팁:** 내 프로젝트 페이지의 메뉴에서 업그레이드가 준비된 프로젝트를 찾을 수 있습니다.  

![업그레이드할 프로젝트 메뉴 항목의 이미지](images/menu-projects-to-upgrade.png)

## 업그레이드 프로세스 시작
{: #start_upgrade}

업그레이드 프로세스를 시작하기 전에, 사용자는 [YouTube ![외부 링크 아이콘](../../icons/launch-glyph.svg "외부 링크 아이콘")](https://youtu.be/oaZVGveVxBg){: new_window}에서 업그레이드가 어떻게 진행되는지를 지켜볼 수 있습니다.
[![YouTube에 대한 외부 링크](images/migration-video2.png)](https://youtu.be/oaZVGveVxBg){: new_window}    
프로젝트를 도구 체인으로 업그레이드하려면 다음 단계를 따르십시오. 

1. 업그레이드 프로세스를 시작하려면 배너 메시지에서 **지금 업그레이드**를 클릭하십시오. "프로젝트 업그레이드 도구 체인" 페이지가 열립니다.  

   ![업그레이드 페이지의 예](images/project-upgrade-toolchain.png)

   업그레이드 프로세스의 개요를 보려면 해당 페이지의 설명을 읽으십시오. 이 경우에는 프로젝트가 GitHub.com에서 저장소를 사용했으므로 도구 체인이 동일한 GitHub 저장소에 연결됩니다. 도구 체인에는 프로젝트의 파이프라인과 동일한 단계 및 작업이 포함된 새 파이프라인이 포함됩니다. 또한 도구 체인에는 {{site.data.keyword.contdelivery_short}}에서 실행되는 Eclipse Orion {{site.data.keyword.webide}}에 대한 포인터가 포함됩니다. 

2. 도구 체인을 사용자 정의하기 위해 일부 설정을 구성할 수 있습니다. 

   - 도구 체인의 이름을 변경하려면 **이름** 필드를 편집하십시오. 

      ![이름 필드](images/name-change.png)

   -   도구 체인이 작성될 {{site.data.keyword.Bluemix_notm}} 조직을 변경하려면 계정 메뉴에서 조직을 선택하십시오. 

      ![Bluemix 조직 선택자](images/bluemix-organization-chooser.png)

   도구 체인이 조직 레벨에서 관리되므로, 도구 체인에 액세스해야 하는 프로젝트 구성원이 이미 존재하거나 별도로 추가될 수 있는 조직을 선택했는지 확인하십시오.  
  
3. **작성**을 클릭하십시오. 새 도구 체인이 작성되며 해당 개요 페이지가 표시됩니다. 

   ![업그레이드된 도구 체인의 개요](images/new-toolchain-page.png)

   - GitHub 저장소 또는 연관된 문제 트래커에 액세스하려면 **GitHub** 또는 **Issues**를 클릭하십시오. 
   
   - 파이프라인에 액세스하려면 **Delivery Pipeline**을 클릭하십시오.   
   
   - 작업공간으로 체크아웃된 저장소의 컨텐츠가 포함된 {{site.data.keyword.webide}}에 액세스하려면 **Eclipse Orion {{site.data.keyword.webide}}**를 클릭하십시오.  

## 프로젝트 재방문
{: #revisit_projects}

새 도구 체인을 사용할 준비가 되었습니다. 이제 프로젝트에는 "업그레이드됨"으로 레이블이 지정되어 있으며 개요 페이지에서 확인 메시지가 표시됩니다. 

!["업그레이드됨" 레이블이 있는 프로젝트 카드의 이미지](images/card-upgraded-project.png)

![업그레이드된 프로젝트](images/banner-upgraded.png)

내 프로젝트 페이지의 메뉴에서 **업그레이드된 프로젝트**를 선택하여 업그레이드된 프로젝트를 볼 수 있습니다. 

![업그레이드된 프로젝트 메뉴 항목의 이미지](images/menu-upgraded-projects.png)

업그레이드를 되돌려야 하는 경우에는 도구 체인을 삭제하십시오. 그리고 프로젝트의 개요 페이지로 돌아가면 업그레이드 메시지가 다시 표시되며, 준비가 되었을 때 다시 업그레이드가 가능합니다. 

## 다음 단계
{: #upgrade_next_steps}   

1. 프로젝트 개요 페이지에서 메시지를 확인하여 업그레이드가 완료되었는지 확인하십시오.     

   ![업그레이드된 프로젝트](images/banner-upgraded.png)    

2. 팀 구성원에게 도구 체인에 대한 액세스 권한을 부여하십시오.     
    - 각 팀 구성원은 유효한 Bluemix 계정을 보유해야 합니다. 계정이 없는 팀 구성원은 [등록 ![외부 링크 아이콘](../../icons/launch-glyph.svg "외부 링크 아이콘")](https://console.ng.bluemix.net/registration){:new_window}이 필요합니다. 
    - 도구 체인이 속한 조직(org)에 팀 구성원을 추가하십시오. 
3. {{site.data.keyword.jazzhub_short}} 프로젝트의 도구가 아닌 도구 체인의 도구를 사용하십시오. 예를 들어, 브라우저에서 코드를 편집하려면 도구 체인의 웹 IDE를 사용하십시오.     

## 문제점 해결
{: #upgrade_troubleshoot}    

질문이나 문제점이 있으면 [hub@jazz.net](mailto:hub@jazz.net) 주소로 이메일을 발송하십시오. 이메일에는 {{site.data.keyword.jazzhub_short}} 프로젝트 및 {{site.data.keyword.contdelivery_short}} 도구 체인의 URL을 포함하십시오. 

