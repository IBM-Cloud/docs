---

copyright:
  years: 2016

---
 
{:shortdesc: .shortdesc}
{:new_window: target="_blank"}

# 도구 체인 시작하기(베타)
{: #toolchains_getting_started}

마지막 업데이트 날짜: 2016년 10월 7일
{: .last-updated}  

도구 체인은 {{site.data.keyword.Bluemix}}의 퍼블릭 및 데디케이티드 환경에서 사용할 수 있습니다. 템플리트를 사용하여 도구 체인을 작성하거나 앱에서 도구 체인을 작성하는 식의 두 방식으로 도구 체인을 작성할 수 있습니다. {{site.data.keyword.Bluemix_notm}} 퍼블릭에서 도구 체인은 미국 남부 지역에서만 사용할 수 있습니다.
{: shortdesc}

##도구 체인 시작하기: 퍼블릭
{: #getting_started_public}

**참고:** 맨 위 배너를 확인하여 새 Bluemix 인터페이스에서 작업 중인지 확인하십시오.

 * 새 Bluemix에 대한 메시지가 표시되면 기존 Bluemix 인터페이스에서 작업하고 있는 것입니다. 링크를 클릭하여 새 Bluemix 인터페이스를 여십시오.
 * 메시지가 표시되지 않으면 새 Bluemix 인터페이스에서 작업하고 있는 것입니다.

각 도구 체인은 특정 조직과 연관되며 해당 조직의 구성원인 사용자가 연관된 도구 체인에 액세스할 수 있습니다. 도구 체인을 작성하기 전에 도구 체인을 작성할 조직에서 작업 중인지 확인하십시오. 현재 작업 중인 조직이 메뉴 표시줄에 표시됩니다. 다른 조직으로 전환하려면 메뉴 표시줄에서 조직을 클릭한 다음 전환할 조직을 선택하십시오.

###템플리트에서 도구 체인 작성   
{: #creating_a_toolchain_from_a_template}

템플리트를 시작점으로 사용하여 특정 도구 통합 세트가 포함된 도구 체인을 작성할 수 있습니다.

1. 첫 번째 도구 체인을 작성하는 경우 조직에서 도구 체인이 사용되는지 확인하십시오.
   1. DevOps 대시보드를 열고 **도구 체인** 페이지를 클릭하십시오.
   2. **도구 체인 사용** 단추가 표시되면 클릭한 다음 프롬프트를 따라 도구 체인을 작성하십시오.
   3. **도구 체인 사용** 단추가 표시되지 않으면 도구 체인이 이미 사용되는 것입니다. 2단계를 진행하십시오.
1. DevOps 대시보드의 **도구 체인** 페이지에서 추가 단추(+)를 클릭하여 도구 체인을 작성하십시오.
1. 도구 체인 템플리트를 클릭하십시오. 예를 들어, 온라인 상점 샘플을 사용하여 도구 체인을 작성하려면 **마이크로 서비스 도구 체인**을 클릭하십시오. 
1. 도구 체인 작성 페이지에서 작성할 도구 체인의 다이어그램을 검토하십시오. 다이어그램에서는 도구 체인의 라이프사이클 단계(Phase)에 있는 각 도구 통합을 보여줍니다. 다음 이미지의 다이어그램은 예입니다. 도구 체인을 작성할 때 다이어그램에서 도구 체인의 일부인 각 도구 통합을 보여줍니다.
![도구 체인 다이어그램](images/toolchain_diagram.png)

1. 도구 체인 설정의 기본 정보를 검토하십시오. 도구 체인의 이름을 통해 {{site.data.keyword.Bluemix_notm}}에서 도구 체인을 식별합니다. 해당 이름의 도구 체인이 이미 있거나 다른 이름을 사용하려는 경우 도구 체인의 이름을 변경하십시오.  
1. 구성 가능한 통합 섹션에서 도구 체인에 대해 구성하려는 각 도구 통합을 선택하십시오. 일부 도구 통합의 경우 구성할 필요가 없습니다. 도구 통합 구성에 대한 정보는 [도구 통합 구성(링크가 새 창에서 열림)](../toolchains/toolchains_integrations.html){: new_window}을 참조하십시오.
1. **작성**을 클릭하십시오. 도구 체인을 설정하기 위해 다음과 같은 여러 단계가 자동으로 실행됩니다.

 * 도구 체인이 작성됩니다.
 * Delivery Pipeline 도구 통합을 구성한 경우 파이프라인이 트리거됩니다.
 * Sauce Labs 도구 통합을 구성한 경우 파이프라인에 작업을 추가하고 테스트를 실행하도록 Sauce Labs 통합이 구성됩니다.
 * PagerDuty 도구 통합을 구성한 경우 Slack에서 구성한 채널에 알림을 보내도록 PagerDuty 통합이 구성됩니다. 이러한 알림은 문제가 발생한 시기를 나타냅니다.
 * Slack 도구 통합을 구성한 경우 Slack에서 구성한 채널에 알림을 보내도록 Slack 통합이 구성됩니다. 이러한 알림은 배치의 진행상태를 표시합니다(예: `프로젝트 XYZ와 연결됨`, `파이프라인이 구성됨` 및 `'빌드' 단계가 시작됨`).
 * GitHub 도구 통합을 구성한 경우 샘플 GitHub 저장소가 GitHub 계정에 복제됩니다.


###앱에서 도구 체인 작성
{: #creating_a_toolchain_from_an_app}

앱에서 도구 체인을 작성할 수 있습니다. 도구 체인은 연속 개발, 배치, 모니터링 등을 지원할 수 있으며 앱과 연관되어 있습니다. 각 앱은 도구 체인과 연관될 수 있습니다. 도구 체인의 GitHub 저장소에 변경사항을 푸시하면 파이프라인에서 앱을 자동으로 빌드하여 배치합니다.  

1. 첫 번째 도구 체인을 작성하는 경우 조직에서 도구 체인이 사용되는지 확인하십시오.
   1. DevOps 대시보드를 열고 **도구 체인** 페이지를 클릭하십시오.
   2. **도구 체인 사용** 단추가 표시되면 클릭한 다음 프롬프트를 따라 도구 체인을 작성하십시오.
   3. **도구 체인 사용** 단추가 표시되지 않으면 도구 체인이 이미 사용되는 것입니다. 2단계를 진행하십시오.
1. 앱 개요 페이지의 Continuous Delivery 타일에서 **사용**을 클릭하십시오. 또는 {{site.data.keyword.Bluemix_notm}} 기존 인터페이스에서 앱의 개요 페이지 오른쪽 상단에 있는 **도구 체인 추가**를 클릭하십시오. 앱 스타터 코드로 채워진 새 GitHub 저장소의 Continuous Delivery에 맞게 앱이 구성됩니다. 
1. 도구 체인 작성 페이지에서 작성할 도구 체인의 다이어그램을 검토하십시오. 다이어그램에서는 도구 체인의 라이프사이클 단계(Phase)에 있는 각 도구 통합을 보여줍니다. 
1. 도구 체인 설정의 기본 정보를 검토하십시오. 도구 체인의 이름을 통해 {{site.data.keyword.Bluemix_notm}}에서 도구 체인을 식별합니다. 해당 이름의 도구 체인이 이미 있거나 다른 이름을 사용하려는 경우 도구 체인의 이름을 변경하십시오.
1. 구성 가능한 통합 섹션에서 도구 체인에 대해 구성하려는 각 도구 통합을 선택하십시오. 일부 도구 통합의 경우 구성할 필요가 없습니다. 도구 통합 구성에 대한 정보는 [도구 통합 구성(링크가 새 창에서 열림)](../toolchains/toolchains_integrations.html){: new_window}을 참조하십시오.
1. **작성**을 클릭하십시오. 도구 체인을 설정하기 위해 다음과 같은 여러 단계가 자동으로 실행됩니다.

 * 도구 체인이 작성됩니다.
 * Delivery Pipeline 도구 통합을 구성한 경우 파이프라인이 트리거됩니다.
 * Sauce Labs 도구 통합을 구성한 경우 파이프라인에 작업을 추가하고 테스트를 실행하도록 Sauce Labs 통합이 구성됩니다.
 * PagerDuty 도구 통합을 구성한 경우 Slack에서 구성한 채널에 알림을 보내도록 PagerDuty 통합이 구성됩니다. 이러한 알림은 문제가 발생한 시기를 나타냅니다.
 * Slack 도구 통합을 구성한 경우 Slack에서 구성한 채널에 알림을 보내도록 Slack 통합이 구성됩니다. 이러한 알림은 배치의 진행상태를 표시합니다(예: `프로젝트 XYZ와 연결됨`, `파이프라인이 구성됨` 및 `'빌드' 단계가 시작됨`).
 * GitHub 도구 통합을 구성한 경우 샘플 GitHub 저장소가 GitHub 계정에 복제됩니다.


##도구 체인 시작하기: 데디케이티드
{: #getting_started_dedicated}

각 도구 체인은 특정 조직과 연관되며 해당 조직의 구성원인 사용자가 연관된 도구 체인에 액세스할 수 있습니다. 도구 체인을 작성하기 전에 메뉴 표시줄에서 **{{site.data.keyword.avatar}}** 아이콘 ![아바타 아이콘](../icons/i-avatar-icon.svg)을 클릭하여 계정 및 지원 위젯을 열고 작업 중인 조직을 확인하십시오. 해당 조직이 도구 체인을 작성하려는 조직이 아니면 다른 조직으로 전환하십시오.

###템플리트에서 도구 체인 작성   
{: #creating_a_toolchain_from_a_template_dedicated}

템플리트를 시작점으로 사용하여 특정 도구 통합 세트가 포함된 도구 체인을 작성할 수 있습니다.

1. 첫 번째 도구 체인을 작성하는 경우 조직에서 도구 체인이 사용되는지 확인하십시오.
   1. DevOps 대시보드를 열고 **도구 체인** 탭을 클릭하십시오.
   2. **도구 체인 사용** 단추가 표시되면 클릭한 다음 프롬프트를 따라 도구 체인을 작성하십시오.
   3. **도구 체인 사용** 단추가 표시되지 않으면 도구 체인이 이미 사용되는 것입니다. 2단계를 진행하십시오.
1. {{site.data.keyword.Bluemix_notm}} 대시보드의 **DEVOPS** 탭에서 추가 단추(+)를 클릭하여 도구 체인을 작성하십시오.
1. 도구 체인 템플리트를 클릭하십시오. 예를 들어 새 Cloud Foundry 앱을 배치하기 위해 단순 도구 체인을 작성하려면 **단순 Cloud Foundry 도구 체인**을 클릭하십시오. 
1. 도구 체인 작성 페이지에서 작성할 도구 체인의 다이어그램을 검토하십시오. 다이어그램에서는 도구 체인의 라이프사이클 단계(Phase)에 있는 각 도구 통합을 보여줍니다. 다음 이미지의 다이어그램은 예입니다. 도구 체인을 작성할 때 다이어그램에서 도구 체인의 일부인 각 도구 통합을 보여줍니다.
![데디케이티드 도구 체인 다이어그램](images/toolchain_dedicated_diagram.png)

1. 도구 체인 설정의 기본 정보를 검토하십시오. 도구 체인의 이름을 통해 {{site.data.keyword.Bluemix_notm}}에서 도구 체인을 식별합니다. 해당 이름의 도구 체인이 이미 있거나 다른 이름을 사용하려는 경우 도구 체인의 이름을 변경하십시오.  
1. 구성 가능한 통합 섹션에서 도구 체인에 대해 구성하려는 각 도구 통합을 선택하십시오. 일부 도구 통합의 경우 구성할 필요가 없습니다. 도구 통합 구성에 대한 정보는 [도구 통합 구성(링크가 새 창에서 열림)](../toolchains/toolchains_integrations.html){: new_window}을 참조하십시오.
1. **작성**을 클릭하십시오. 도구 체인을 설정하기 위해 다음과 같은 여러 단계가 자동으로 실행됩니다.

 * 도구 체인이 작성됩니다.
 * Delivery Pipeline 도구 통합을 구성한 경우 파이프라인이 트리거됩니다.
 * GitHub Enterprise 도구 통합을 구성한 경우 샘플 GitHub Enterprise 저장소가 GitHub Enterprise 계정에 복제됩니다.


###앱에서 도구 체인 작성
{: #creating_a_toolchain_from_an_app_dedicated}

앱에서 도구 체인을 작성할 수 있습니다. 도구 체인은 연속 개발, 배치, 모니터링 등을 지원할 수 있으며 앱과 연관되어 있습니다. 각 앱은 도구 체인과 연관될 수 있습니다. 도구 체인의 GitHub Enterprise 저장소에 변경사항을 푸시하면 파이프라인에서 앱을 자동으로 빌드하여 배치합니다.  

1. 첫 번째 도구 체인을 작성하는 경우 조직에서 도구 체인이 사용되는지 확인하십시오.
   1. DevOps 대시보드를 열고 **도구 체인** 탭을 클릭하십시오.
   2. **도구 체인 사용** 단추가 표시되면 클릭한 다음 프롬프트를 따라 도구 체인을 작성하십시오.
   3. **도구 체인 사용** 단추가 표시되지 않으면 도구 체인이 이미 사용되는 것입니다. 2단계를 진행하십시오.
1. 앱 개요 페이지의 오른쪽 상단에서 **도구 체인 추가**를 클릭하십시오. 앱 스타터 코드로 채워진 새 GitHub Enterprise 저장소의 Continuous Delivery에 맞게 앱이 구성됩니다. 
1. 도구 체인 작성 페이지에서 작성할 도구 체인의 다이어그램을 검토하십시오. 다이어그램에서는 도구 체인의 라이프사이클 단계(Phase)에 있는 각 도구 통합을 보여줍니다. 
1. 도구 체인 설정의 기본 정보를 검토하십시오. 도구 체인의 이름을 통해 {{site.data.keyword.Bluemix_notm}}에서 도구 체인을 식별합니다. 해당 이름의 도구 체인이 이미 있거나 다른 이름을 사용하려는 경우 도구 체인의 이름을 변경하십시오.
1. 구성 가능한 통합 섹션에서 도구 체인에 대해 구성하려는 각 도구 통합을 선택하십시오. 일부 도구 통합의 경우 구성할 필요가 없습니다. 도구 통합 구성에 대한 정보는 [도구 통합 구성(링크가 새 창에서 열림)](../toolchains/toolchains_integrations.html){: new_window}을 참조하십시오.
1. **작성**을 클릭하십시오. 도구 체인을 설정하기 위해 다음과 같은 여러 단계가 자동으로 실행됩니다.

 * 도구 체인이 작성됩니다.
 * Delivery Pipeline 도구 통합을 구성한 경우 파이프라인이 트리거됩니다.
 * GitHub Enterprise 도구 통합을 구성한 경우 샘플 GitHub Enterprise 저장소가 GitHub Enterprise 계정에 복제됩니다.


##도구 체인 보기
{: #viewing_a_toolchain}

도구 체인과 해당 도구 통합을 구성하고 나면 도구 통합 페이지에서 도구 체인의 시각적 표시를 볼 수 있습니다.

* {{site.data.keyword.Bluemix_notm}} 퍼블릭을 사용하는 경우 DevOps 대시보드의 **도구 체인** 페이지에서 도구 체인을 클릭하여 도구 통합 페이지를 여십시오. 또는 앱 개요 페이지의 Continuous Delivery 타일에서 **도구 체인 보기**를 클릭하십시오. 그런 다음 **도구 통합**을 클릭하십시오. 
   
* {{site.data.keyword.Bluemix_notm}} 데디케이티드를 사용하는 경우 대시보드의 **DEVOPS** 탭에서 도구 체인을 클릭하여 도구 통합 페이지를 여십시오. 또는 앱 개요 페이지의 오른쪽 상단에서 **도구 체인 보기**를 클릭하십시오.

* 도구 체인에 있는 도구 통합에 액세스하려면 도구 타일을 클릭하십시오. 
 
 **팁**: GitHub 또는 GitHub Enterprise 저장소가 두 개 이상이면 각 저장소는 고유 타일로 표시되므로 동일한 도구 통합에 여러 타일이 있을 수 있습니다.


 <!-- The toolchain in the following image is an example. When you create your own toolchain, the visual representation of the toolchain shows the tool integrations that you configure.
![Sample toolchain](images/toolchain.png) -->


# 관련 링크
{: #rellinks}

## 튜토리얼 및 샘플
{: #samples}

* [세 개의 마이크로 서비스가 포함된 애플리케이션(베타) 작성(링크가 새 창에서 열림)](https://www.ibm.com/devops/method/tutorials/tutorial_microservices_part1){:new_window}
* [Create a toolchain from a template on {{site.data.keyword.Bluemix_notm}} Dedicated (Beta)(링크가 새 창에서 열림)](https://www.ibm.com/devops/method/tutorials/tutorial_dedicated_toolchain_template_flow){:new_window}
* [Create a toolchain from an app on {{site.data.keyword.Bluemix_notm}} Dedicated (Beta)(링크가 새 창에서 열림)](https://www.ibm.com/devops/method/tutorials/tutorial_dedicated_toolchain_app_flow){:new_window}

## 관련 링크
{: #general}

* [마이크로 서비스 도구 체인(베타)(링크가 새 창에서 열림)](https://www.ibm.com/devops/method/toolchains/microservices_toolchain){:new_window}
* [단순 도구 체인(베타)(링크가 새 창에서 열림)](https://www.ibm.com/devops/method/toolchains/simple_toolchain){:new_window}
* [IBM Bluemix Garage Method(링크가 새 창에서 열림)](https://www.ibm.com/devops/method){:new_window}
