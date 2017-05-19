---

copyright:
  years: 2015, 2017
lastupdated: "2017-4-28"

---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}

# 도구 체인 작성
{: #toolchains_getting_started}

*도구 체인*은 개발, 배치 및 운영 태스크를 지원하는 도구 통합 세트입니다. 도구 체인의 전체 기능은 개별 도구 통합을 합한 것보다 강력합니다.
{: shortdesc}

오픈 도구 체인은 {{site.data.keyword.Bluemix}}의 퍼블릭 및 데디케이티드 환경에서 사용 가능합니다. 두 가지 방법으로 도구 체인을 작성할 수 있습니다. 즉, 템플리트를 사용하여 도구 체인을 작성하거나 앱에서 도구 체인을 작성할 수 있습니다.

각 도구 체인은 특정 조직(org)과 연관되어 있으며, 해당 조직의 구성원인 사용자는 이와 연관된 도구 체인의 액세스 제어 목록에 추가될 수 있습니다. 도구 체인의 액세스 제어에 대한 자세한 정보는 [액세스 관리](/docs/services/ContinuousDelivery/toolchains_using.html#managing_access){: new_window}를 참조하십시오. 도구 체인을 작성하기 전에 도구 체인을 작성하려는 조직에서 작업 중인지 확인하십시오. 작업 중인 조직은 메뉴 표시줄에 표시됩니다. 다른 조직으로 전환하려면 메뉴 표시줄에서 조직을 클릭하고 전환할 조직을 선택하십시오. 


##템플리트에서 도구 체인 작성   
{: #creating_a_toolchain_from_a_template}

특정 도구 통합 세트가 포함된 [도구 체인 작성 ![외부 링크 아이콘](../../icons/launch-glyph.svg "외부 링크 아이콘")](https://console.ng.bluemix.net/devops/create){: new_window}에 대한 시작점으로 템플리트를 사용할 수 있습니다. [IBM Cloud Garage Method ![외부 링크 아이콘](../../icons/launch-glyph.svg "외부 링크 아이콘")](https://www.ibm.com/devops/method/category/tools){:new_window}에서 템플리트 사용 방법에 대해 자세히 알아보십시오. 

1. {{site.data.keyword.Bluemix_notm}} 퍼블릭을 사용 중이면 [{{site.data.keyword.Bluemix_notm}} ![외부 링크 아이콘](../../icons/launch-glyph.svg "외부 링크 아이콘")](http://console.ng.bluemix.net){:new_window}에 로그인하십시오. 
1. {{site.data.keyword.Bluemix_notm}} 데디케이티드를 사용 중이면 {{site.data.keyword.Bluemix_notm}}의 데디케이티드 환경에 로그인하십시오. 
1. {{site.data.keyword.Bluemix_notm}} 메뉴 표시줄의 메뉴에서 **서비스**를 클릭한 후 **DevOps**를 클릭하십시오.
1. DevOps 대시보드의 **도구 체인** 페이지에서 **도구 체인 작성**을 클릭하십시오. 
1. **도구 체인 작성** 페이지에서 도구 체인 템플리트를 클릭하십시오. 
1. 작성하려는 도구 체인의 다이어그램을 검토하십시오. 다이어그램은 도구 체인에서 해당 라이프사이클 단계(Phase)에 있는 각 도구 통합을 보여줍니다. 

 **팁**: 일부 도구 체인 템플리트에는 도구 통합의 여러 인스턴스가 있습니다. 예를 들어, {{site.data.keyword.Bluemix_notm}} 퍼블릭의 마이크로서비스 도구 체인 템플리트에는 3개 마이크로서비스 각각에 대해 하나씩 GitHub의 3개 인스턴스와 Delivery Pipeline의 3개 인스턴스가 포함되어 있습니다. 

 다음 이미지의 다이어그램을 예로 들 수 있습니다. 도구 체인을 작성할 때 다이어그램은 도구 체인의 일부인 각 도구 통합을 표시합니다.
![도구 체인 다이어그램](images/toolchain_diagram.png)

1. 도구 체인 설정에 대한 기본 정보를 검토하십시오. 도구 체인의 이름은 {{site.data.keyword.Bluemix_notm}}에서 해당 도구 체인을 식별합니다. 다른 이름을 사용하려면 도구 체인의 이름을 변경하십시오.  
1. 도구 통합 섹션에서 도구 체인에 대해 구성할 각 도구 통합을 선택하십시오. 몇몇 도구 통합에서는 구성이 필요 없습니다. 도구 통합 구성에 대한 정보는 [도구 통합 구성](/docs/services/ContinuousDelivery/toolchains_integrations.html){: new_window}의 내용을 참조하십시오.
1. **작성**을 클릭하십시오. 여러 단계가 자동으로 실행되어 도구 체인을 설정합니다. 설정된 도구 통합은 선택된 도구 체인 템플리트 및 사용자가 {{site.data.keyword.Bluemix_notm}} 퍼블릭 또는 {{site.data.keyword.Bluemix_notm}} 데디케이티드를 사용 중인지 여부에 따라 다릅니다. 예를 들어, {{site.data.keyword.Bluemix_notm}} 퍼블릭에서 마이크로서비스 도구 체인을 작성하면 다음 단계가 실행됩니다. 

 * 도구 체인이 작성됩니다. 
 * Delivery Pipeline을 구성한 경우에는 파이프라인이 작성되고 트리거됩니다. 
 * Sauce Labs를 구성한 경우에는 Sauce Labs 테스트 작업을 파이프라인에 추가하도록 도구 체인이 설정됩니다. 
 * PagerDuty를 구성한 경우에는 경보 알림을 지정된 PagerDuty 서비스에 전송하도록 도구 체인이 설정됩니다. 
 * Slack을 구성한 경우에는 배치 상태에 대한 알림을 지정된 Slack 채널에 전송하도록 도구 체인이 설정됩니다. 
 * GitHub 등의 소스 코드 도구 통합을 구성한 경우에는 샘플 GitHub 저장소가 GitHub 계정으로 복제됩니다. 


##앱에서 도구 체인 작성
{: #creating_a_toolchain_from_an_app}

앱에서 도구 체인을 작성할 수 있습니다. 도구 체인은 지속적인 개발, 배치, 모니터링 등을 지원할 수 있으며 앱과 연관됩니다. 각 앱을 도구 체인과 연관시킬 수 있습니다. 도구 체인의 GitHub 또는 {{site.data.keyword.ghe_short}} 저장소에 변경사항을 푸시하면 파이프라인이 자동으로 앱을 빌드하고 배치합니다.   

1. 앱 개요 페이지의 지속적 딜리버리 카드에서 **사용**을 클릭하십시오. {{site.data.keyword.Bluemix_notm}} 퍼블릭을 사용 중이면 앱 스타터 코드로 채워진 새 GitHub 저장소에서 지속적 딜리버리를 위해 앱이 구성됩니다. {{site.data.keyword.Bluemix_notm}} 데디케이티드를 사용 중이면 앱 스타터 코드로 채워진 새 GitHub 또는 {{site.data.keyword.ghe_short}} 저장소에서 지속적 딜리버리를 위해 앱이 구성됩니다. 
1. 도구 체인 작성 페이지에서 작성하려는 도구 체인의 다이어그램을 검토하십시오. 다이어그램은 도구 체인에서 해당 라이프사이클 단계(Phase)에 있는 각 도구 통합을 보여줍니다. 
1. 도구 체인 설정에 대한 기본 정보를 검토하십시오. 도구 체인의 이름은 {{site.data.keyword.Bluemix_notm}}에서 해당 도구 체인을 식별합니다. 다른 이름을 사용하려면 도구 체인의 이름을 변경하십시오.
1. 도구 통합 섹션에서 도구 체인에 대해 구성할 각 도구 통합을 선택하십시오. 몇몇 도구 통합에서는 구성이 필요 없습니다. 도구 통합 구성에 대한 정보는 [도구 통합 구성](/docs/services/ContinuousDelivery/toolchains_integrations.html){: new_window}의 내용을 참조하십시오.
1. **작성**을 클릭하십시오. 여러 단계가 자동으로 실행되어 도구 체인을 설정합니다. 설정된 도구 통합은 사용자가 도구 체인을 {{site.data.keyword.Bluemix_notm}} 퍼블릭에서 또는 {{site.data.keyword.Bluemix_notm}} 데디케이티드에서 사용하는지 여부에 따라 다릅니다. 예를 들어, {{site.data.keyword.Bluemix_notm}} 퍼블릭의 앱에서 도구 체인을 작성하면 다음 단계가 실행됩니다. 

 * 도구 체인이 작성됩니다. 
 * Delivery Pipeline을 구성한 경우에는 파이프라인이 작성되고 트리거됩니다. 
 * GitHub를 구성한 경우에는 샘플 GitHub 저장소가 GitHub 계정으로 복제됩니다. 


##도구 체인 보기
{: #viewing_a_toolchain}

도구 체인과 해당 도구 통합을 구성한 후에는 도구 체인의 시각적 표현을 볼 수 있습니다. 

1. DevOps 대시보드의 **도구 체인** 페이지에서 도구 체인을 클릭하여 해당 개요 페이지를 여십시오. 또는 앱 개요 페이지의 지속적 딜리버리 카드에서 **도구 체인 보기**를 클릭하십시오. 그런 다음 **개요**를 클릭하십시오. 
2. 도구 체인에 있는 도구 통합에 액세스하려면 도구를 클릭하십시오. 

 **팁**: 둘 이상의 GitHub, {{site.data.keyword.ghe_short}} 또는 Git 저장소가 있는 경우, 각 저장소가 자체 카드에 의해 표시되므로 동일한 도구 통합에 대해 여러 개의 카드가 있을 수 있습니다. 둘 이상의 파이프라인이 있는 경우, 각 파이프라인이 자체 카드에 의해 표시되므로 동일한 도구 통합에 대해 여러 개의 카드가 있을 수 있습니다. 예를 들어, 사용자가 마이크로서비스 도구 체인을 작성하면 3개 마이크로서비스 각각에는 자체 GitHub, {{site.data.keyword.ghe_short}} 또는 Git 저장소 및 자체 파이프라인이 있습니다. 
