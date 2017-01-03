---

copyright:
  years: 2016

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen:.screen}
{:codeblock:.codeblock}

# 도구 통합 구성
{: #integrations}

마지막 업데이트 날짜: 2016년 11월 17일
{: .last-updated}

도구 체인을 작성할 때 개발, 배치 및 운영을 지원하는 도구 통합을 구성하거나 기존 도구 체인에 도구 통합을 추가하고 구성하여 기존 도구 체인을 사용자 정의할 수 있습니다.   
{:shortdesc}

**중요**: {{site.data.keyword.Bluemix_notm}} 퍼블릭에서는 미국 남부 지역에서만 도구 체인을 사용할 수 있습니다. 

사용하는 도구 체인에 추가하고 구성할 수 있는 도구 통합은 도구 체인을 {{site.data.keyword.Bluemix_notm}} 퍼블릭에서 사용 중인지 또는 {{site.data.keyword.Bluemix_notm}} 데디케이티드에서 사용 중인지 여부에 따라 달라집니다. {{site.data.keyword.Bluemix_notm}} 데디케이티드의 도구 체인을 사용 중인 경우 사용 가능한 도구 통합은 사용자의 특정 환경에 {{site.data.keyword.jazzhub_title}}가 설정되는 방법에 따라 달라집니다.

*표 1. {{site.data.keyword.Bluemix_notm}} 퍼블릭 및 데디케이티드에서 도구 체인에 사용 가능한 도구 통합*

|도구 통합 |{{site.data.keyword.Bluemix_notm}} 퍼블릭에서 사용 가능	|{{site.data.keyword.Bluemix_notm}} 데디케이티드에서 사용 가능(환경에 따라 다름)|
|:----------|:------------------------------|:------------------|
|{{site.data.keyword.deliverypipeline}} 		|예	   	|예  		|
|{{site.data.keyword.DRA_short}} 		|예		|아니오			|
|Eclipse Orion {{site.data.keyword.webide}}		|예		|예			|
|GitHub		|예		|예		|
|Dedicated GitHub Enterprise			|아니오		|예		|
|기타 도구			|예		|예		|
|PagerDuty			|예		|예		|
|Sauce Labs		|예		|아니오		|
|Slack			|예		|예		|

**팁**: {{site.data.keyword.Bluemix_notm}} 퍼블릭에서 소스 코드를 사용하여 개발을 시작하려는 경우, {{site.data.keyword.deliverypipeline}}을 구성하기 전에 GitHub 도구 통합을 구성하십시오. {{site.data.keyword.Bluemix_notm}} 데디케이티드에서 코드로 개발을 시작하려는 경우, {{site.data.keyword.deliverypipeline}}을 구성하기 전에 {{site.data.keyword.ghe_short}} 도구 통합 또는 GitHub 도구 통합을 구성하십시오.  


## Delivery Pipeline 구성
{: #deliverypipeline}

{{site.data.keyword.deliverypipeline}}은 입력을 검색하고 빌드, 테스트 및 배치 등의 작업을 실행하는 일련의 단계를 통해 프로젝트의 연속 배치를 자동화합니다.  

앱의 연속 빌드, 테스트 및 배치를 자동화하도록 {{site.data.keyword.deliverypipeline}}을 구성하십시오.  

1. 도구 체인을 작성하면서 이 도구 통합을 구성하는 경우, 구성 가능한 통합 섹션에서 **Delivery Pipeline**을 클릭하십시오. 사용하는 템플리트에 따라 사용 가능한 필드가 다를 수 있습니다. 기본 필드 값을 검토하고 필요한 경우 해당 설정을 변경하십시오. 
1. {{site.data.keyword.Bluemix_notm}} 퍼블릭에 있는 도구 체인에 이 도구 통합을 추가하는 경우 DevOps 대시보드의 **도구 체인** 페이지에서 도구 체인을 클릭하여 해당 개요 페이지를 여십시오. 또는 앱 개요 페이지의 Continuous Delivery 타일에서 **도구 체인 보기**를 클릭하십시오. 그런 다음 **개요**를 클릭하십시오. {{site.data.keyword.Bluemix_notm}} 데디케이티드에서 도구 체인을 사용 중인 경우, 대시보드의 **DEVOPS** 탭에서 도구 체인을 클릭하여 해당 도구 통합 페이지를 여십시오. 또는 앱 개요 페이지의 오른쪽 상단에서 **도구 체인 보기**를 클릭하십시오. 그런 다음 **도구 통합**을 클릭하십시오.  
1. **도구에 추가**를 클릭하십시오.
1. 도구 통합 섹션에서 **Delivery Pipeline**을 클릭하십시오.
1. 새 파이프라인의 이름을 지정하십시오. 
1. 파이프라인을 사용하여 사용자 인터페이스를 배치하려는 경우 **앱 보기 메뉴에 앱 표시** 선택란을 선택하십시오. 파이프라인에서 작성하는 모든 앱이 도구 체인의 개요 페이지에 있는 **앱 보기** 목록에 표시됩니다.
1. **통합 작성**을 클릭하여 도구 체인에 {{site.data.keyword.deliverypipeline}}을 추가하십시오. 
1. {{site.data.keyword.deliverypipeline}}의 타일을 클릭하여 파이프라인을 보고 구성하십시오. 파이프라인 구성의 기본사항을 알아보려면 [파이프라인 빌드 및 배치](/docs/services/ContinuousDelivery/pipeline_build_deploy.html){: new_window}의 내용을 참조하십시오.

  **팁**: GitHub 또는 {{site.data.keyword.ghe_short}} 저장소(repo)에 변경사항을 푸시할 때 파이프라인을 트리거하려는 경우, 파이프라인의 단계를 정의하기 전에 도구 체인의 GitHub 또는 {{site.data.keyword.ghe_short}}를 구성해야 합니다. 파이프라인 단계에는 사용하는 저장소의 Git URL이 필요합니다. 각 파이프라인 단계는 도구 체인과 연관된 GitHub 또는 {{site.data.keyword.ghe_short}} 저장소 중 하나만 참조할 수 있습니다. GitHub 구성에 대한 지시사항은 [GitHub](#github) 섹션을 참조하십시오. Dedicated GitHub Enterprise 구성에 대한 지시사항은 [{{site.data.keyword.ghe_long}} 시작하기](/docs/services/ghededicated/index.html){: new_window}의 내용을 참조하십시오.
  
1. 선택사항: {{site.data.keyword.Bluemix_notm}} 퍼블릭에서 도구 체인을 사용 중이고 Sauce Labs에서 앱에 대한 테스트를 실행하도록 하려면 Sauce Labs 테스트 작업을 추가하도록 {{site.data.keyword.deliverypipeline}}을 구성하십시오. 테스트 작업을 구성하는 데 관한 지시사항은 [파이프라인에서 Sauce Labs 테스트 작업 구성](#config_saucelabs) 절을 참조하십시오. 

### 파이프라인에서 Sauce Labs 테스트 작업 구성
{: #config_saucelabs}

파이프라인에서 Sauce Labs 테스트 작업을 구성하기 전, 앱을 빌드하고 배치하는 단계가 포함된 정상으로 작동하는 파이프라인이 필요하며 사용하는 도구 체인에 적합하게 Sauce Labs를 구성해야 합니다. Sauce Labs를 구성하는 데 관한 지시사항은 [Sauce Labs](#saucelabs) 절을 참조하십시오. 

Sauce Labs 테스트 작업을 추가하도록 {{site.data.keyword.deliverypipeline}}을 구성하십시오. 

1. 앱의 테스트 버전을 배치하는 단계가 없으면 하나를 작성하십시오. 
1. 이 단계에서 배치 작업 뒤에 테스트 작업을 추가하십시오. 동일한 단계에 이러한 작업을 배치하면 해당 작업이 동일한 환경 특성 세트에 액세스할 수 있습니다.
  ![테스트 작업](images/toolchain_test_job.png) 

1. 단계를 구성하십시오.  

  a. **환경 특성** 탭에서 세 개의 특성 CF_APP_NAME, SAUCE_USERNAME 및 SAUCE_ACCESS_KEY를 작성하십시오. 
  
  b. Sauce Labs 사용자 이름과 액세스 키를 입력하십시오. 그렇게 하면 해당 값이 테스트에서 사용할 수 있도록 구체화됩니다. 
  
1. 배치 작업을 구성하십시오. **배치 스크립트** 필드에 다음 명령을 포함시키십시오. `export CF_APP_NAME="$CF_APP"`. 이 명령은 앱 이름을 환경 특성으로서 내보냅니다. 
1. 테스트 작업을 구성하십시오. 다음 이미지의 값은 예입니다. **서비스 인스턴스**, **대상**, **조직** 및 **영역** 필드는 사용 중인 Sauce Labs 사용자 이름, 지역, 조직 및 영역으로 채워집니다.
![작업 구성](images/toolchain_configure_job.png)

  a. 테스터 유형으로 **Sauce Labs**를 선택하십시오. 
  
  b. 서비스 인스턴스에 대해, 도구 체인에 Sauce Labs를 구성할 때 사용한 Sauce Labs 사용자 이름을 선택하십시오.  
  
   **팁**: 도구 체인에 Sauce Labs를 구성할 때 사용한 사용자 이름 및 액세스 키를 보려면 **구성**을 클릭하십시오.  
  
  c. **테스트 실행 명령** 필드에 테스트에 필요한 종속 항목을 설치하는 명령을 입력한 후 테스트를 실행하십시오. 예를 들어, Node.js 앱의 경우 다음 명령을 입력할 수 있습니다. 
     ```
     npm install
     node_modules/grunt-cli/bin/grunt test:sauce:parallel
     ```
  
    d. 테스트 작업 로그에서 테스트 보고서를 보려는 경우, **테스트 보고서 사용** 선택란을 선택하고 테스트 결과 파일 패턴을 `test/*.xml`로 설정하십시오. 
  
1. **저장**을 클릭하십시오. 파이프라인을 실행할 때마다 Sauce Labs 테스트가 실행됩니다. 

자세한 정보는 [Delivery Pipeline(링크가 새 창에서 열림)](https://www.ibm.com/devops/method/content/deliver/tool_build_and_deploy/){: new_window}을 참조하십시오.


## {{site.data.keyword.DRA_short}} 추가
{: #dra}

{{site.data.keyword.DRA_full}}는 단위 테스트, 기능 테스트 및 코드 검사 도구로부터의 결과를 수집하고 분석하여 코드가 배치 프로세스의 지정된 게이트에서 사전 정의된 기준을 충족하는지 여부를 판별합니다. 코드가 기준을 충족하지 않거나 기준을 초과하면 위험이 표출되지 않도록 배치가 중지됩니다. {{site.data.keyword.DRA_short}}를 Continuous Delivery 환경의 안전망으로서 또는 품질 표준을 구현하고 향상시키는 방법으로서 사용할 수 있습니다.  

 **참고**: 이 도구 통합은 사전 구성됩니다. 구성 매개변수가 필요 없으며 재구성할 수 없습니다. 
 
{{site.data.keyword.DRA_short}}를 추가하여 배치를 모니터하고 위험이 표출되기 전에 위험을 식별함으로써 {{site.data.keyword.Bluemix_notm}}의 코드 품질을 유지하고 향상시킬 수 있습니다. 

1. 도구 체인이 있고 여기에 이 도구 통합을 추가하는 경우 DevOps 대시보드의 **도구 체인** 페이지에서 도구 체인을 클릭하여 해당 개요 페이지를 여십시오. 또는 앱 개요 페이지의 Continuous Delivery 타일에서 **도구 체인 보기**를 클릭하십시오. 그런 다음 **개요**를 클릭하십시오.  
1. **도구에 추가**를 클릭하십시오.
1. 도구 통합 섹션에서 **{{site.data.keyword.DRA_short}}**를 클릭하십시오. 
1. **통합 작성**을 클릭하십시오.
1. {{site.data.keyword.DRA_short}}의 타일을 클릭한 후 시작하기 단계(기준 작성, 파이프라인에 기준 연결 및 파이프라인 실행)를 완료하십시오. 자세한 정보는 [{{site.data.keyword.DRA_short}}(링크가 새 창에서 열림)](https://www.ibm.com/devops/method/content/learn/tool_devops_insights/){: new_window}를 참조하십시오.


## Eclipse Orion {{site.data.keyword.webide}} 추가
{: #webide}

Eclipse Orion {{site.data.keyword.webide}}는 소스 제어 태스크를 작성, 편집, 실행, 디버그 및 완료할 수 있는 통합된 웹 기반 환경입니다. 편집에서 실행, 제출 및 배치까지 원활하게 이동할 수 있습니다.  

 **참고**: 이 도구 통합은 사전 구성됩니다. 구성 매개변수가 필요 없으며 재구성할 수 없습니다. 
 
소스 제어 태스크를 완료하려면 Eclipse Orion {{site.data.keyword.webide}} 도구 통합을 추가하십시오. 

1. {{site.data.keyword.Bluemix_notm}} 퍼블릭에 있는 도구 체인에 이 도구 통합을 추가하는 경우 DevOps 대시보드의 **도구 체인** 페이지에서 도구 체인을 클릭하여 해당 개요 페이지를 여십시오. 또는 앱 개요 페이지의 Continuous Delivery 타일에서 **도구 체인 보기**를 클릭하십시오. 그런 다음 **개요**를 클릭하십시오. {{site.data.keyword.Bluemix_notm}} 데디케이티드에서 도구 체인을 사용 중인 경우, 대시보드의 **DEVOPS** 탭에서 도구 체인을 클릭하여 해당 도구 통합 페이지를 여십시오. 또는 앱 개요 페이지의 오른쪽 상단에서 **도구 체인 보기**를 클릭하십시오. 그런 다음 **도구 통합**을 클릭하십시오. 
1. **도구에 추가**를 클릭하십시오.
1. 도구 통합 섹션에서 **Eclipse Orion Web IDE**를 클릭하십시오. 
1. **통합 작성**을 클릭하십시오.
1. 새 Eclipse Orion {{site.data.keyword.webide}}의 타일을 클릭하십시오. 작업공간이 GitHub 또는 {{site.data.keyword.ghe_short}} 저장소로 미리 채워집니다. 현재 도구 체인과 연관된 저장소가 강조표시됩니다. 

자세히 알아보려면 [Eclipse Orion {{site.data.keyword.webide}}로 코드 편집](/docs/services/ContinuousDelivery/web_ide.html){: new_window}의 내용을 참조하십시오.


## GitHub 구성
{: #github}

GitHub는 Git 저장소의 웹 기반 호스팅 서비스입니다. 쉽게 협업할 수 있도록 저장소의 로컬 및 원격 사본을 모두 보유할 수 있습니다.  

GitHub Issues는 작업과 플랜을 모두 한 위치에 보관하는 추적 도구입니다. 개발 저장소에 통합되므로 중요한 태스크에 집중할 수 있습니다. 

클라우드에서 소스 코드를 관리하도록 GitHub를 구성하십시오. 

1. 도구 체인을 작성할 때 이 도구 통합을 구성하는 경우 다음 단계를 따르십시오. 

 a. 구성 가능한 통합 섹션에서 **GitHub**를 클릭하십시오. {{site.data.keyword.Bluemix_notm}} 퍼블릭에 도구 체인을 작성 중이고 GitHub에 액세스하는 권한을 {{site.data.keyword.Bluemix_notm}}에 부여하지 않은 경우 **권한 부여**를 클릭하여 GitHub 웹 사이트로 이동하십시오. 활성 GitHub 세션이 없으면 로그인을 요구하는 프롬프트가 표시됩니다. **애플리케이션에 권한 부여**를 클릭하여 {{site.data.keyword.Bluemix_notm}}에서 사용자의 GitHub 계정에 액세스할 수 있도록 허용하십시오. 활성 GitHub 세션이 있지만 최근에 비밀번호를 입력하지 않은 경우 확인을 위해 GitHub 비밀번호 입력을 요구하는 프롬프트가 표시될 수 있습니다. 
 
 b. GitHub 저장소의 기본 대상 저장소 위치를 검토하십시오. 해당 저장소는 샘플 저장소에서 복제됩니다. 필요한 경우 대상 저장소의 이름을 변경하십시오.
 ![기본 대상 저장소 위치](images/toolchain_github_config.png)
   
1. 도구 체인이 있고 여기에 이 도구 통합을 추가하는 경우 DevOps 대시보드의 **도구 체인** 페이지에서 도구 체인을 클릭하여 해당 개요 페이지를 여십시오. 또는 앱 개요 페이지의 Continuous Delivery 타일에서 **도구 체인 보기**를 클릭하십시오. 그런 다음 **개요**를 클릭하십시오.  
1. **도구에 추가**를 클릭하십시오.
1. 도구 통합 섹션에서 **GitHub**를 클릭하십시오.
1. GitHub 저장소가 있으며 이 저장소를 사용하려는 경우 저장소 유형에서 **기존**을 클릭하십시오. 그런 다음 URL을 입력하십시오. 
1. 새 GitHub 저장소를 사용하려는 경우, 해당 GitHub 저장소의 이름을 입력하고 복제하거나 분기시킬 저장소의 URL을 입력하며 저장소 유형을 선택하십시오.  

 a. 빈 저장소를 작성하려면 **새로 작성**을 클릭하십시오.  
 
 b. GitHub 저장소의 사본을 작성하려면 **복제**를 클릭하십시오. 
 
 c. 가져오기 요청을 통해 변경사항을 컨트리뷰션할 수 있도록 GitHub 저장소를 분기시키려면 **분기**를 클릭하십시오.
 
1. 문제 추적에 GitHub Issues를 사용하려면 **GitHub Issues 사용** 선택란을 선택하십시오.
1. **통합 작성**을 클릭하십시오.
1. 작업할 GitHub 저장소의 타일을 클릭하십시오. GitHub 웹 사이트가 열리고 여기서 저장소의 컨텐츠를 볼 수 있습니다. 
 
  **팁**: Eclipse Orion {{site.data.keyword.webide}}의 통합된 소스 코드 관리 도구를 사용하여 GitHub 저장소를 편집하고 작업공간에서 앱을 배치할 수 있습니다. 

1. GitHub Issues를 사용 가능하게 설정한 경우 GitHub Issues의 타일을 클릭하여 이를 여십시오. 

자세한 정보는 [GitHub(링크가 새 창에서 열림)](https://www.ibm.com/devops/method/content/code/tool_github/){: new_window} 및 [GitHub Issues(링크가 새 창에서 열림)](https://www.ibm.com/devops/method/content/think/tool_github_issues/){: new_window}를 참조하십시오.


## Dedicated GitHub Enterprise 구성
{: #configghe}

{{site.data.keyword.ghe_long}}는 Git 저장소를 위한 온프레미스 웹 기반 호스팅 서비스입니다. Dedicated GitHub Enterprise는 {{site.data.keyword.Bluemix_notm}} 데디케이티드 고객만을 대상으로 합니다. GitHub Issues는 작업과 플랜을 한 위치에 보관하는 추적 도구입니다. 개발 저장소에 통합되므로 중요한 태스크에 집중할 수 있습니다. Dedicated GitHub Enterprise와 GitHub 문제에 대한 자세한 정보는 [{{site.data.keyword.ghe_long}} 시작하기](/docs/services/ghededicated/index.html){: new_window}, [GitHub 문제(링크가 새 창에서 열림)](https://www.ibm.com/devops/method/content/think/tool_github_issues/){: new_window}의 내용을 참조하십시오. 

회사의 [{{site.data.keyword.Bluemix_notm}} 데디케이티드](/docs/dedicated/index.html#dedicated){: new_window} 인스턴스에서 소스 코드를 관리할 수 있도록 {{site.data.keyword.ghe_short}}를 도구 체인의 도구 통합으로 구성할 수 있습니다. 

1. 도구 체인을 작성할 때 이 도구 통합을 구성하는 경우 다음 단계를 따르십시오. 

 a. 처음 Dedicated GitHub Enterprise에 로그인하기 전, 회사의 지역 관리자에게 LDAP을 사용하여 회사의 사용자 레지스트리에서 사용하는 {{site.data.keyword.Bluemix_notm}} 데디케이티드 인스턴스에 사용자 ID를 추가하도록 요청하십시오. {{site.data.keyword.ghe_short}} 계정 설정에 대한 정보는 [{{site.data.keyword.ghe_long}} 시작하기](/docs/services/ghededicated/index.html){: new_window}의 내용을 참조하십시오. 
 
 b. 구성 가능한 통합 섹션에서 **{{site.data.keyword.ghe_short}}**를 클릭하십시오.     
 
 c. 새 {{site.data.keyword.ghe_short}} 저장소의 기본 이름을 검토하십시오. 필요한 경우 새 저장소의 이름을 변경하십시오. 다음 이미지는 샘플 저장소에서 복제된 저장소의 예를 보여줍니다. 기존 저장소 또는 새 저장소를 사용할 수 있습니다. 새 저장소를 사용하려면 비어 있는 저장소를 작성하거나 저장소를 복제하거나 또는 저장소를 분기시킬 수 있습니다.
![기본 저장소 위치](images/toolchain_ghe_config.png)
   
1. {{site.data.keyword.Bluemix_notm}} 퍼블릭에 보유한 도구 체인에 도구 통합을 추가하는 경우 DevOps 대시보드의 **도구 체인** 페이지에서 도구 체인을 클릭하여 해당 도구 통합 페이지를 여십시오. 또는 앱 개요 페이지의 Continuous Delivery 타일에서 **도구 체인 보기**를 클릭하십시오. 그런 다음 **도구 통합**을 클릭하십시오. {{site.data.keyword.Bluemix_notm}} 데디케이티드에서 도구 체인을 사용 중인 경우, 대시보드의 **DEVOPS** 탭에서 도구 체인을 클릭하여 해당 도구 통합 페이지를 여십시오. 또는 앱 개요 페이지의 오른쪽 상단에서 **도구 체인 보기**를 클릭하십시오. 그런 다음 **도구 통합**을 클릭하십시오. 
1. 추가 단추(+)를 클릭하십시오. 
1. 도구 통합 섹션에서 **{{site.data.keyword.ghe_short}}**를 클릭하십시오.
1. 사용할 {{site.data.keyword.ghe_short}} 저장소가 있는 경우 해당 저장소의 URL을 입력하십시오. 저장소 유형으로 **기존**을 클릭하십시오. 
1. 새 {{site.data.keyword.ghe_short}} 저장소를 사용하려는 경우, 해당 저장소의 이름을 입력하고 복제하거나 분기시킬 저장소의 URL을 입력하며 저장소 유형을 선택하십시오.  

 a. 빈 저장소를 작성하려면 **새로 작성**을 클릭하십시오.  
 
 b. 저장소의 사본을 작성하려면 **복제**를 클릭하십시오. 
 
 c. 가져오기 요청을 통해 변경사항을 컨트리뷰션할 수 있도록 저장소를 분기시키려면 **분기**를 클릭하십시오.
 
1. 문제 추적에 GitHub Issues를 사용하려면 **GitHub Issues 사용** 선택란을 선택하십시오.
1. **통합 작성**을 클릭하십시오.
1. 작업할 {{site.data.keyword.ghe_short}} 저장소의 타일을 클릭하십시오. 회사의 [{{site.data.keyword.Bluemix_notm}} 데디케이티드](/docs/dedicated/index.html#dedicated){: new_window} 인스턴스가 열리며 여기서 저장소의 컨텐츠를 볼 수 있습니다. 
 
  **팁**: Eclipse Orion {{site.data.keyword.webide}}의 통합된 소스 코드 관리 도구를 사용하여 {{site.data.keyword.ghe_short}} 저장소를 편집하고 작업공간에서 앱을 배치할 수 있습니다. 

1. GitHub Issues를 사용 가능하게 설정한 경우 GitHub Issues의 타일을 클릭하십시오. 

<!-- 8/23/2016: The GHE Dedicated content has been moved to docs-staging/services/ghededicated/index.md -->

## 사용자 정의 도구(기타 도구) 구성
{: #othertool}

사용자의 팀이 도구 체인 통합 목록에 포함되지 않은 도구를 사용하는 경우 사용자 정의 도구를 통합할 수 있습니다.  

사용자 정의 도구를 구성하면 도구 체인에서 다른 도구와 함께 작동하며 사용자의 팀에 사용 가능합니다. 

1. 도구 체인을 작성할 때 이 도구 통합을 구성하는 경우, 구성 가능한 통합 섹션에서 **기타 도구**를 클릭하십시오. 
1. {{site.data.keyword.Bluemix_notm}} 퍼블릭에 있는 도구 체인에 이 도구 통합을 추가하는 경우 DevOps 대시보드의 **도구 체인** 페이지에서 도구 체인을 클릭하여 해당 개요 페이지를 여십시오. 또는 앱 개요 페이지의 Continuous Delivery 타일에서 **도구 체인 보기**를 클릭하십시오. 그런 다음 **개요**를 클릭하십시오. {{site.data.keyword.Bluemix_notm}} 데디케이티드에서 도구 체인을 사용 중인 경우, 대시보드의 **DEVOPS** 탭에서 도구 체인을 클릭하여 해당 도구 통합 페이지를 여십시오. 또는 앱 개요 페이지의 오른쪽 상단에서 **도구 체인 보기**를 클릭하십시오. 그런 다음 **도구 통합**을 클릭하십시오. 
1. **도구에 추가**를 클릭하십시오.
1. 도구 통합 섹션에서 **기타 도구**를 클릭하십시오.
1. 도구 이름을 입력하십시오.
1. 도구와 가장 연관된 라이프사이클 단계를 선택하십시오. 선택한 라이프사이클 단계에 따라 개요 페이지에 표시되는 도구의 카테고리가 달라집니다. 
1. 아이콘 URL을 추가하십시오. 아이콘은 도구의 통합 카드에 표시됩니다. 
1. 문서 URL을 추가하십시오.
1. 도구 인스턴스 이름을 지정하십시오. 예: My Team Tool. 
1. 도구 인스턴스 URL을 추가하십시오. 도구 통합 카드를 클릭하면 도구 인스턴스를 위해 표시한 URL로 연결됩니다. 
1. 도구에 대한 설명을 추가하십시오.
1. (고급) 필요 시 추가 특성을 추가하십시오. 예를 들어, 도구 체인의 기타 도구와 통합하는 도구에 필요한 속성 또는 정보를 나열하십시오.   
1. **통합 작성**을 클릭하십시오.

## PagerDuty 구성
{: #pagerduty}

PagerDuty는 여러 모니터링 시스템의 데이터를 단일 보기로 통합합니다. 문제가 발생하면 PagerDuty는 당시에 해당 문제를 가장 잘 수정할 수 있는 팀 구성원에게 알림이 전송되도록 합니다. 해당 팀 구성원이 문제점에 응답하지 않는 경우 해당 문제점을 두 번째 엔지니어 또는 운영 관리자에게 라우트하도록 에스컬레이션을 구성할 수 있습니다. 

문제점을 보다 빨리 수정하여 가동중단시간을 줄이려면 파이프라인 단계 장애가 발생할 경우 알림을 전송하도록 PagerDuty를 구성하십시오. 

1. 도구 체인을 작성할 때 이 도구 통합을 구성하는 경우, 구성 가능한 통합 섹션에서 **PagerDuty**를 클릭하십시오. 
1. {{site.data.keyword.Bluemix_notm}} 퍼블릭에 있는 도구 체인에 이 도구 통합을 추가하는 경우 DevOps 대시보드의 **도구 체인** 페이지에서 도구 체인을 클릭하여 해당 개요 페이지를 여십시오. 또는 앱 개요 페이지의 Continuous Delivery 타일에서 **도구 체인 보기**를 클릭하십시오. 그런 다음 **개요**를 클릭하십시오. {{site.data.keyword.Bluemix_notm}} 데디케이티드에서 도구 체인을 사용 중인 경우, 대시보드의 **DEVOPS** 탭에서 도구 체인을 클릭하여 해당 도구 통합 페이지를 여십시오. 또는 앱 개요 페이지의 오른쪽 상단에서 **도구 체인 보기**를 클릭하십시오. 그런 다음 **도구 통합**을 클릭하십시오.  
1. **도구에 추가**를 클릭하십시오.
1. 도구 통합 섹션에서 **PagerDuty**를 클릭하십시오.
1. 사용하는 PagerDuty 계정과 연관된 PagerDuty 사이트 이름을 입력하십시오. PagerDuty 계정이 없는 경우 [계정을 등록(링크가 새 창에서 열림)](https://signup.pagerduty.com/accounts/new){: new_window}하십시오. 
1. PagerDuty 계정의 API 액세스 키를 입력하십시오. 이 키를 찾기 위한 지시사항은 [API 인증(링크가 새 창에서 열림)](https://signup.pagerduty.com/accounts/new){: new_window}을 참조하십시오.
1. 사용하는 PagerDuty 서비스의 이름을 입력하십시오. 
1. 1차 PagerDuty 담당자의 이메일 주소를 입력하십시오. 
1. 1차 PagerDuty 담당자의 전화번호를 입력하십시오. 
1. **통합 작성**을 클릭하십시오.
1. PagerDuty의 타일을 클릭하여 pagerduty.com으로 이동하십시오. 도구 체인에 대해 이 도구 통합을 구성할 때 지정한 PagerDuty 서비스와 연관된 이벤트를 볼 수 있습니다.  

자세한 정보는 [PagerDuty(링크가 새 창에서 열림)](https://www.ibm.com/devops/method/content/manage/tool_pagerduty/){: new_window}를 참조하십시오.


## Sauce Labs 구성
{: #saucelabs}

Sauce Labs는 기능 단위 테스트를 실행합니다. {{site.data.keyword.deliverypipeline}}에서 Sauce Labs 테스트 스위트가 테스트 작업으로 구성되어 있는 경우, 이 테스트 스위트는 Continuous Delivery 프로세스의 일부로 웹 또는 모바일 앱에 대해 테스트를 실행할 수 있습니다. 이러한 테스트는 프로젝트의 중요한 플로우 제어를 제공할 수 있으며 잘못된 코드의 배치를 방지하는 게이트 역할을 합니다. 

여러 운영 체제 및 브라우저에서 자동화된 기능 테스트를 실행하도록 Sauce Labs를 구성하십시오. 그러면 사용자가 웹 사이트 또는 애플리케이션을 사용할 가능성이 있는 방법을 에뮬레이트할 수 있습니다. 

1. 도구 체인을 작성할 때 이 도구 통합을 구성하는 경우, 구성 가능한 통합 섹션에서 **Sauce Labs**를 클릭하십시오. 
1. 도구 체인이 있고 여기에 이 도구 통합을 추가하는 경우 DevOps 대시보드의 **도구 체인** 페이지에서 도구 체인을 클릭하여 해당 개요 페이지를 여십시오. 또는 앱 개요 페이지의 Continuous Delivery 타일에서 **도구 체인 보기**를 클릭하십시오. 그런 다음 **개요**를 클릭하십시오.  
1. **도구에 추가**를 클릭하십시오.
1. 도구 통합 섹션에서 **Sauce Labs**를 클릭하십시오.
1. 사용하는 Sauce Labs 계정과 연관된 사용자 이름을 입력하십시오. [Sauce Labs 계정 페이지의 맨 위에 있는 시작 메시지에서 사용자 이름 찾기(링크가 새 창에서 열림)](https://saucelabs.com/account){: new_window}를 수행할 수 있습니다. 
1. Sauce Labs 계정의 액세스 키를 입력하십시오. [Sauce Labs 계정 페이지에서 키 찾기(링크가 새 창에서 열림)](https://saucelabs.com/account){: new_window}를 수행할 수 있습니다.
1. **통합 작성**을 클릭하십시오.
1. Sauce Labs의 타일을 클릭하여 saucelabs.com으로 이동하고 도구 체인의 테스트 활동을 보십시오. 

 **팁**: {{site.data.keyword.deliverypipeline}}에 Sauce Labs 테스트 작업을 추가한 경우 해당 서비스 인스턴스를 선택할 수 있습니다. 

자세한 정보는 [Sauce Labs(링크가 새 창에서 열림)](https://www.ibm.com/devops/method/content/code/tool_sauce_labs/){: new_window}를 참조하십시오.


## Slack 구성
{: #slack}

**중요**: 공용 Slack 채널에 게시되는 알림은 팀의 모든 구성원에게 표시됩니다. 컨텐츠를 게시한 사람이 해당 컨텐츠에 대한 책임을 집니다. 

Slack은 클라우드 기반의 실시간 메시징 및 알림 시스템입니다. Slack은 팀 협업을 위해 이메일 대신 사용할 수 있는 대화성이 뛰어난 지속적 대화를 제공합니다. 전용 채널이나 작업과 직접 관련이 있는 채널 세트에서 팀과 통신할 수 있습니다. 채널을 통해 또는 둘 이상의 사용자 간의 직접 메시지에서 파일 및 이미지를 공유할 수도 있습니다. 직접 메시지 및 채널에서의 통신은 검색이 가능하도록 유지됩니다.  

도구 통합에서 도구 체인에 대한 알림(예: 테스트 및 배치 활동)을 수신하도록 Slack을 구성하십시오. 

1. 도구 체인을 작성할 때 이 도구 통합을 구성하는 경우, 구성 가능한 통합 섹션에서 **Slack**을 클릭하십시오. 
1. {{site.data.keyword.Bluemix_notm}} 퍼블릭에 있는 도구 체인에 이 도구 통합을 추가하는 경우 DevOps 대시보드의 **도구 체인** 페이지에서 도구 체인을 클릭하여 해당 개요 페이지를 여십시오. 또는 앱 개요 페이지의 Continuous Delivery 타일에서 **도구 체인 보기**를 클릭하십시오. 그런 다음 **개요**를 클릭하십시오. {{site.data.keyword.Bluemix_notm}} 데디케이티드에서 도구 체인을 사용 중인 경우, 대시보드의 **DEVOPS** 탭에서 도구 체인을 클릭하여 해당 도구 통합 페이지를 여십시오. 또는 앱 개요 페이지의 오른쪽 상단에서 **도구 체인 보기**를 클릭하십시오. 그런 다음 **도구 통합**을 클릭하십시오. 
1. **도구에 추가**를 클릭하십시오.
1. 도구 통합 섹션에서 **Slack**을 클릭하십시오.
1. Slack 계정의 API 인증 토큰을 입력하십시오. Slack에서 인증을 수행하려면 생성된 전체 액세스 토큰을 사용해야 합니다. 이 토큰을 찾기 위한 지시사항은 [Slack authentication(링크가 새 창에서 열림)](https://api.slack.com/web#authentication){: new_window}을 참조하십시오.
1. 알림을 전송할 Slack 채널의 이름을 입력하십시오. 지정한 채널이 없는 경우 해당 채널이 작성됩니다. 채널이 아카이브되었으면 다시 활성화됩니다. 
1. **통합 작성**을 클릭하십시오.
1. Slack의 타일을 클릭하십시오. 구성된 Slack 채널에서 도구 체인의 모든 활동을 볼 수 있습니다. 

자세한 정보는 [Slack(링크가 새 창에서 열림)](https://www.ibm.com/devops/method/content/culture/tool_slack/){: new_window}을 참조하십시오.


# 관련 링크
{: #rellinks}

## 튜토리얼 및 샘플
{: #samples}

* [Create and use your first toolchain(링크가 새 창에서 열림)](https://www.ibm.com/devops/method/tutorials/tutorial_toolchain_flow){:new_window}
* [Create a custom toolchain(링크가 새 창에서 열림)](https://www.ibm.com/devops/method/tutorials/tutorial_toolchain_custom){:new_window}
* [Create an application with three microservices(링크가 새 창에서 열림)](https://www.ibm.com/devops/method/tutorials/tutorial_toolchain_microservices){:new_window}
* [Create a toolchain from a template on {{site.data.keyword.Bluemix_notm}} Dedicated(Beta)(링크가 새 창에서 열림)](https://www.ibm.com/devops/method/tutorials/tutorial_dedicated_toolchain_template_flow){:new_window}
* [Create a toolchain from an app on {{site.data.keyword.Bluemix_notm}} Dedicated(Beta)(링크가 새 창에서 열림)](https://www.ibm.com/devops/method/tutorials/tutorial_dedicated_toolchain_app_flow){:new_window}

## 관련 링크
{: #general}

* [Microservices toolchain(링크가 새 창에서 열림)](https://www.ibm.com/devops/method/toolchains/microservices_toolchain){:new_window}
* [Simple toolchain(링크가 새 창에서 열림)](https://www.ibm.com/devops/method/toolchains/simple_toolchain){:new_window}
* [IBM Bluemix Garage Method(링크가 새 창에서 열림)](https://www.ibm.com/devops/method){:new_window}
