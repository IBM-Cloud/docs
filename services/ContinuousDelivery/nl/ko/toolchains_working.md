---

copyright:
  years: 2016

---
 
{:shortdesc: .shortdesc}
{:new_window: target="_blank"}

# 도구 체인에 대한 작업
{: #toolchains_getting_started}

마지막 업데이트 날짜: 2016년 11월 17일
{: .last-updated}  

*도구 체인*은 개발, 배치 및 운영 태스크를 지원하는 도구 통합 세트입니다. 도구 체인의 전체 기능은 개별 도구 통합을 합한 것보다 강력합니다.
{: shortdesc}

도구 체인은 {{site.data.keyword.Bluemix}}의 퍼블릭 및 데디케이티드 환경에서 사용 가능합니다. 두 가지 방법으로 도구 체인을 작성할 수 있습니다. 즉, 템플리트를 사용하여 도구 체인을 작성하거나 앱에서 도구 체인을 작성할 수 있습니다. {{site.data.keyword.Bluemix_notm}} 퍼블릭에서는 미국 남부 지역에서만 도구 체인을 사용할 수 있습니다. 

## 도구 체인 시작하기: 퍼블릭
{: #getting_started_public}

각 도구 체인은 특정 조직(org)과 연관되어 있으며 해당 조직의 구성원인 사용자는 누구나 조직과 연관된 도구 체인에 액세스할 수 있습니다. 도구 체인을 작성하기 전에 도구 체인을 작성하려는 조직에서 작업 중인지 확인하십시오. 현재 작업 중인 조직이 메뉴 표시줄에 표시됩니다. 다른 조직으로 전환하려면 메뉴 표시줄에서 조직을 클릭하고 전환하려는 조직을 선택하십시오.

### 템플리트에서 도구 체인 작성   
{: #creating_a_toolchain_from_a_template}

템플리트를 시작점으로 사용하여 특정 도구 통합 세트를 포함하는 [도구 체인을 작성(링크가 새 창에서 열림)](https://console.ng.bluemix.net/devops/create){: new_window}할 수 있습니다. [IBM Bluemix Garage Method(링크가 새 창에서 열림)](https://www.ibm.com/devops/method/category/tools){:new_window}에서 템플리트 사용 방법을 자세히 알아보십시오. 

1. [{{site.data.keyword.Bluemix_notm}}(링크가 새 창에서 열림)](http://console.ng.bluemix.net){:new_window}에 로그인하십시오. {{site.data.keyword.Bluemix_notm}} 대시보드가 열리고 조직에서 사용할 수 있는 활성 {{site.data.keyword.Bluemix_notm}} 공간의 개요를 표시합니다. 
1. 햄버거 메뉴에서 **서비스**를 클릭한 후 **DevOps**를 클릭하십시오. 
1. DevOps 대시보드의 **도구 체인** 페이지에서 **도구 체인 작성**을 클릭하십시오. 
1. **도구 체인 작성** 페이지에서 도구 체인 템플리트를 클릭하십시오. 
1. 작성하려는 도구 체인의 다이어그램을 검토하십시오. 다이어그램은 도구 체인에서 해당 라이프사이클 단계(Phase)에 있는 각 도구 통합을 보여줍니다. 다음 이미지의 다이어그램을 예로 들 수 있습니다. 도구 체인을 작성할 때 다이어그램은 도구 체인의 일부인 각 도구 통합을 표시합니다.
![도구 체인 다이어그램](images/toolchain_diagram.png)

1. 도구 체인 설정에 대한 기본 정보를 검토하십시오. 도구 체인의 이름은 {{site.data.keyword.Bluemix_notm}}에서 해당 도구 체인을 식별합니다. 다른 이름을 사용하려면 도구 체인의 이름을 변경하십시오.  
1. 구성 가능한 통합 섹션에서 도구 체인에 구성하려는 각 도구 통합을 선택하십시오. 몇몇 도구 통합에서는 구성이 필요 없습니다. 도구 통합 구성에 대한 정보는 [도구 통합 구성](/docs/services/ContinuousDelivery/toolchains_integrations.html){: new_window}의 내용을 참조하십시오.
1. **작성**을 클릭하십시오.다음과 같은 여러 단계가 자동으로 실행되어 도구 체인을 설정합니다. 

 * 도구 체인이 작성됩니다. 
 * Delivery Pipeline 도구 통합을 구성한 경우 파이프라인이 작성되고 트리거됩니다.
 * Sauce Labs 도구 통합을 구성한 경우에는 파이프라인에 작업을 추가하고 테스트를 실행하도록 Sauce Labs가 설정됩니다.
 * PagerDuty 도구 통합을 구성한 경우에는 지정한 서비스에 경보 알림을 보내도록 PagerDuty가 설정됩니다.
 * Slack 도구 통합을 구성한 경우 지정한 채널에 배치 상태에 대한 알림을 보내도록 Slack이 설정됩니다.
 * GitHub 도구 통합을 구성한 경우, 사용하는 GitHub 계정에 샘플 GitHub 저장소가 복제됩니다. 


### 앱에서 도구 체인 작성
{: #creating_a_toolchain_from_an_app}

앱에서 도구 체인을 작성할 수 있습니다. 도구 체인은 지속적인 개발, 배치, 모니터링 등을 지원할 수 있으며 앱과 연관됩니다. 각 앱을 도구 체인과 연관시킬 수 있습니다. 도구 체인의 GitHub 저장소에 변경사항을 푸시하면 파이프라인이 자동으로 앱을 빌드하고 배치합니다.  

1. 앱 개요 페이지의 Continuous Delivery 타일에서 **사용**을 클릭하십시오. 앱 스타터 코드로 채워지는 새 GitHub 저장소에서 Continuous Delivery가 가능하도록 앱이 구성됩니다. 
1. 도구 체인 작성 페이지에서 작성하려는 도구 체인의 다이어그램을 검토하십시오. 다이어그램은 도구 체인에서 해당 라이프사이클 단계(Phase)에 있는 각 도구 통합을 보여줍니다. 
1. 도구 체인 설정에 대한 기본 정보를 검토하십시오. 도구 체인의 이름은 {{site.data.keyword.Bluemix_notm}}에서 해당 도구 체인을 식별합니다. 다른 이름을 사용하려면 도구 체인의 이름을 변경하십시오.
1. 구성 가능한 통합 섹션에서 도구 체인에 구성하려는 각 도구 통합을 선택하십시오. 몇몇 도구 통합에서는 구성이 필요 없습니다. 도구 통합 구성에 대한 정보는 [도구 통합 구성](/docs/services/ContinuousDelivery/toolchains_integrations.html){: new_window}의 내용을 참조하십시오.
1. **작성**을 클릭하십시오.다음과 같은 여러 단계가 자동으로 실행되어 도구 체인을 설정합니다. 

 * 도구 체인이 작성됩니다. 
 * Delivery Pipeline 도구 통합을 구성한 경우 파이프라인이 작성되고 트리거됩니다.
 * Sauce Labs 도구 통합을 구성한 경우에는 파이프라인에 작업을 추가하고 테스트를 실행하도록 Sauce Labs가 설정됩니다.
 * PagerDuty 도구 통합을 구성한 경우에는 지정한 서비스에 경보 알림을 보내도록 PagerDuty가 설정됩니다.
 * Slack 도구 통합을 구성한 경우 지정한 채널에 배치 상태에 대한 알림을 보내도록 Slack이 설정됩니다.
 * GitHub 도구 통합을 구성한 경우, 사용하는 GitHub 계정에 샘플 GitHub 저장소가 복제됩니다. 


## 도구 체인 시작하기: 데디케이티드
{: #getting_started_dedicated}

각 도구 체인은 특정 조직과 연관되어 있으며 해당 조직의 구성원인 사용자는 누구나 연관된 도구 체인에 액세스할 수 있습니다. 도구 체인을 작성하기 전에 메뉴 표시줄에서 **{{site.data.keyword.avatar}}** 아이콘을 클릭하여 계정 및 지원 위젯을 열고 작업 중인 조직을 보십시오. 해당 조직이 도구 체인을 작성하려는 조직이 아닌 경우 다른 조직으로 전환하십시오. 

### 템플리트에서 도구 체인 작성   
{: #creating_a_toolchain_from_a_template_dedicated}

템플리트를 시작점으로 사용하여 특정 도구 통합 세트를 포함하는 도구 체인을 작성할 수 있습니다. 

1. {{site.data.keyword.Bluemix_notm}} 대시보드의 **DEVOPS** 탭에서 추가 단추(+)를 클릭하여 도구 체인을 작성하십시오. 
1. **도구 체인 작성** 페이지에서 도구 체인 템플리트를 클릭하십시오.  
1. 작성하려는 도구 체인의 다이어그램을 검토하십시오. 다이어그램은 도구 체인에서 해당 라이프사이클 단계(Phase)에 있는 각 도구 통합을 보여줍니다. 다음 이미지의 다이어그램을 예로 들 수 있습니다. 도구 체인을 작성할 때 다이어그램은 도구 체인의 일부인 각 도구 통합을 표시합니다.
![데디케이티드 도구 체인 다이어그램](images/toolchain_dedicated_diagram.png)

1. 도구 체인 설정에 대한 기본 정보를 검토하십시오. 도구 체인의 이름은 {{site.data.keyword.Bluemix_notm}}에서 해당 도구 체인을 식별합니다. 해당 이름을 가진 도구 체인이 이미 있거나 다른 이름을 사용하려는 경우에는 도구 체인의 이름을 변경하십시오.   
1. 구성 가능한 통합 섹션에서 도구 체인에 구성하려는 각 도구 통합을 선택하십시오. 몇몇 도구 통합에서는 구성이 필요 없습니다. 도구 통합 구성에 대한 정보는 [도구 통합 구성](/docs/services/ContinuousDelivery/toolchains_integrations.html){: new_window}의 내용을 참조하십시오.
1. **작성**을 클릭하십시오.다음과 같은 여러 단계가 자동으로 실행되어 도구 체인을 설정합니다. 

 * 도구 체인이 작성됩니다. 
 * Delivery Pipeline 도구 통합을 구성한 경우 파이프라인이 작성되고 트리거됩니다.
 * PagerDuty 도구 통합을 구성한 경우에는 지정한 서비스에 경보 알림을 보내도록 PagerDuty가 설정됩니다.
 * Slack 도구 통합을 구성한 경우 지정한 채널에 배치 상태에 대한 알림을 보내도록 Slack이 설정됩니다.
 * GitHub Enterprise 도구 통합을 구성한 경우, 사용하는 GitHub Enterprise 계정에 샘플 GitHub Enterprise 저장소가 복제됩니다. 


### 앱에서 도구 체인 작성
{: #creating_a_toolchain_from_an_app_dedicated}

앱에서 도구 체인을 작성할 수 있습니다. 도구 체인은 지속적인 개발, 배치, 모니터링 등을 지원할 수 있으며 앱과 연관됩니다. 각 앱을 도구 체인과 연관시킬 수 있습니다. 도구 체인의 GitHub Enterprise 저장소에 변경사항을 푸시하면 파이프라인이 자동으로 앱을 빌드하고 배치합니다.  

1. 앱의 개요 페이지 오른쪽 위에서 **도구 체인 추가**를 클릭하십시오. 앱 스타터 코드로 채워지는 새 GitHub Enterprise 저장소에서 Continuous Delivery가 가능하도록 앱이 구성됩니다. 
1. 도구 체인 작성 페이지에서 작성하려는 도구 체인의 다이어그램을 검토하십시오. 다이어그램은 도구 체인에서 해당 라이프사이클 단계(Phase)에 있는 각 도구 통합을 보여줍니다. 
1. 도구 체인 설정에 대한 기본 정보를 검토하십시오. 도구 체인의 이름은 {{site.data.keyword.Bluemix_notm}}에서 해당 도구 체인을 식별합니다. 해당 이름을 가진 도구 체인이 이미 있거나 다른 이름을 사용하려는 경우에는 도구 체인의 이름을 변경하십시오. 
1. 구성 가능한 통합 섹션에서 도구 체인에 구성하려는 각 도구 통합을 선택하십시오. 몇몇 도구 통합에서는 구성이 필요 없습니다. 도구 통합 구성에 대한 정보는 [도구 통합 구성](/docs/services/ContinuousDelivery/toolchains_integrations.html){: new_window}의 내용을 참조하십시오.
1. **작성**을 클릭하십시오.다음과 같은 여러 단계가 자동으로 실행되어 도구 체인을 설정합니다. 

 * 도구 체인이 작성됩니다. 
 * Delivery Pipeline 도구 통합을 구성한 경우 파이프라인이 작성되고 트리거됩니다.
 * PagerDuty 도구 통합을 구성한 경우에는 지정한 서비스에 경보 알림을 보내도록 PagerDuty가 설정됩니다.
 * Slack 도구 통합을 구성한 경우 지정한 채널에 배치 상태에 대한 알림을 보내도록 Slack이 설정됩니다.
 * GitHub Enterprise 도구 통합을 구성한 경우, 사용하는 GitHub Enterprise 계정에 샘플 GitHub Enterprise 저장소가 복제됩니다. 


## 도구 체인 보기
{: #viewing_a_toolchain}

도구 체인과 해당 도구 통합을 구성한 후에는 도구 체인의 시각적 표시를 볼 수 있습니다. 

* {{site.data.keyword.Bluemix_notm}} 퍼블릭을 사용하는 경우 DevOps 대시보드의 **도구 체인** 페이지에서 도구 체인을 클릭하여 해당 개요 페이지를 여십시오. 또는 앱 개요 페이지의 Continuous Delivery 타일에서 **도구 체인 보기**를 클릭하십시오. 그런 다음 **개요**를 클릭하십시오.  
   
* {{site.data.keyword.Bluemix_notm}} 데디케이티드를 사용하는 경우, 대시보드의 **DEVOPS** 탭에서 도구 체인을 클릭하여 해당 도구 통합 페이지를 여십시오. 또는 앱 개요 페이지의 오른쪽 상단에서 **도구 체인 보기**를 클릭하십시오. 

* 도구 체인에 있는 도구 통합에 액세스하려면 도구의 타일을 클릭하십시오.  
 
 **팁**: 둘 이상의 GitHub 또는 GitHub Enterprise 저장소가 있는 경우, 각 저장소는 자체 고유의 타일로 표시되므로 동일한 도구 통합에 대해 여러 개의 타일이 있을 수 있습니다. 


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
