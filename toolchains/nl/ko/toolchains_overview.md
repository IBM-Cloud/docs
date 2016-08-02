---

copyright:
  years: 2016

---
 
{:shortdesc: .shortdesc}
{:new_window: target="_blank"}

# 도구 체인 시작하기(실험)
{: #toolchains_getting_started}

*마지막 업데이트 날짜: 2016년 6월 8일*
{: .last-updated}  

도구 체인은 개발, 배치 및 운영 태스크를 지원하는 도구 통합 세트입니다. 도구 체인의 전체 기능은 개별 도구 통합을 합한 기능보다 강합니다.
{: shortdesc}

템플리트를 사용하여 도구 체인을 작성하거나 앱에서 도구 체인을 작성하는 식의 두 방식으로 도구 체인을 작성할 수 있습니다. 사용하는 템플리트 또는 도구 체인에 따라 도구 체인에는 앱 스타터 코드 및 사전 구성된 Delivery Pipeline으로 채워진 GitHub 저장소(repo)가 포함될 수 있습니다. 도구 체인의 GitHub 저장소에 변경사항을 푸시하면 Delivery Pipeline에서 자동으로 앱을 빌드하여 {{site.data.keyword.Bluemix}}에 배포합니다.

시작점으로 도구 체인 템플리트를 사용하여 특정 도구 통합 세트가 있는 도구 체인 또는 도구 통합을 추가할 수 있는 비어 있는 도구 체인을 작성할 수 있습니다.

**중요**: 이 기능은 실험적으로 사용됩니다. 도구 체인이 안정적이지 않거나 이전 버전과 호환되지 않는 방식으로 변경될 수 있습니다. 프로덕션 환경에서는 사용하지 않는 것이 좋습니다. 도구 체인을 사용하려면 일회성 [액세스 요청](https://new-console.ng.bluemix.net/devops?cm_mmc=IBMBluemixGarageMethod-_-MethodSite-_-10-19-15::12-31-18-_-toolchains-welcome-page){: new_window}을 수행해야 합니다. 도구 체인은 미국 남부 지역에서만 사용할 수 있습니다.


##템플리트에서 도구 체인 작성   
{: #creating_a_toolchain_from_a_template}

도구 체인에 대한 액세스 요청이 승인되면 시작점으로 템플리트를 사용하여 특정 도구 통합 세트가 있는 도구 체인을 작성할 수 있습니다.

1. DevOps 대시보드의 **도구 체인** 탭에서 **도구 체인 작성**을 클릭하여 첫 번째 도구 체인을 작성하십시오. 이미 도구 체인이 있으면 추가 버튼(+)을 클릭하여 다른 도구 체인을 작성하십시오.
1. 도구 체인 템플리트를 클릭하십시오. 예를 들어, 온라인 상점 샘플을 사용하여 도구 체인을 작성하려면 **마이크로 서비스 도구 체인**을 클릭하십시오. 
1. 도구 체인 작성 페이지에서 작성할 도구 체인의 다이어그램을 검토하십시오. 다이어그램에서는 도구 체인의 라이프사이클 단계(Phase)에 있는 각 도구 통합을 보여줍니다. 다음 이미지의 다이어그램은 예입니다. 도구 체인을 작성할 때 다이어그램에서 도구 체인의 일부인 각 도구 통합을 보여줍니다.
![도구 체인 다이어그램](images/toolchain_diagram.png)

1. 도구 체인 설정의 기본 정보를 검토하십시오. 도구 체인의 이름을 통해 {{site.data.keyword.Bluemix}}에서 도구 체인을 식별합니다. 해당 이름의 도구 체인이 이미 있거나 다른 이름을 사용하려는 경우 도구 체인의 이름을 변경하십시오.  
1. 구성 가능한 통합 섹션에서 도구 체인에 대해 구성하려는 각 도구 통합을 선택하십시오. 도구 통합 구성에 대한 정보는 [도구 통합 구성](../toolchains/toolchains_integrations.html){: new_window}을 참조하십시오.
1. **작성**을 클릭하십시오. 도구 체인을 설정하기 위해 다음과 같은 여러 단계가 자동으로 실행됩니다.

 * 도구 체인이 작성됩니다.
 * Delivery Pipeline 도구 통합을 구성한 경우 파이프라인이 트리거됩니다.
 * Sauce Labs 도구 통합을 구성한 경우 파이프라인에 작업을 추가하고 테스트를 실행하도록 Sauce Labs 통합이 구성됩니다.
 * PagerDuty 도구 통합을 구성한 경우 Slack에서 구성한 채널에 알림을 보내도록 PagerDuty 통합이 구성됩니다. 이러한 알림은 문제가 발생한 시기를 나타냅니다.
 * Slack 도구 통합을 구성한 경우 Slack에서 구성한 채널에 알림을 보내도록 Slack 통합이 구성됩니다. 이러한 알림은 배치의 진행상태를 표시합니다(예: `프로젝트 XYZ와 연결됨`, `파이프라인이 구성됨` 및 `'빌드' 단계가 시작됨`).
 * GitHub 도구 통합을 구성한 경우 샘플 GitHub 저장소가 GitHub 계정에 복제됩니다.


##앱에서 도구 체인 작성
{: #creating_a_toolchain_from_an_app}

도구 체인에 대한 액세스 요청이 승인되면 앱에서 도구 체인을 작성할 수 있습니다. 도구 체인은 연속 개발, 배치, 모니터링 등을 지원할 수 있으며 앱과 연관되어 있습니다. 각 앱은 도구 체인과 연관될 수 있습니다. 도구 체인의 GitHub 저장소에 변경사항을 푸시하면 파이프라인에서 앱을 자동으로 빌드하여 배치합니다.  

1. 앱 개요 페이지의 Continuous Delivery 타일에서 **도구 체인 추가**를 클릭하십시오. 또는 Bluemix Class Experience에서 **GIT 추가**를 클릭하십시오. 앱 스타터 코드로 채워진 새 GitHub 저장소의 Continuous Delivery에 맞게 앱이 구성됩니다. 
1. 도구 체인 작성 페이지에서 작성할 도구 체인의 다이어그램을 검토하십시오. 다이어그램에서는 도구 체인의 라이프사이클 단계(Phase)에 있는 각 도구 통합을 보여줍니다. 
1. 도구 체인 설정의 기본 정보를 검토하십시오. 도구 체인의 이름을 통해 {{site.data.keyword.Bluemix}}에서 도구 체인을 식별합니다. 해당 이름의 도구 체인이 이미 있거나 다른 이름을 사용하려는 경우 도구 체인의 이름을 변경하십시오.
1. 구성 가능한 통합 섹션에서 도구 체인에 대해 구성하려는 각 도구 통합을 선택하십시오. 도구 통합 구성에 대한 정보는 [도구 통합 구성](../toolchains/toolchains_integrations.html){: new_window}을 참조하십시오.
1. **작성**을 클릭하십시오. 도구 체인을 설정하기 위해 다음과 같은 여러 단계가 자동으로 실행됩니다.

 * 도구 체인이 작성됩니다.
 * Delivery Pipeline 도구 통합을 구성한 경우 파이프라인이 트리거됩니다.
 * Sauce Labs 도구 통합을 구성한 경우 파이프라인에 작업을 추가하고 테스트를 실행하도록 Sauce Labs 통합이 구성됩니다.
 * PagerDuty 도구 통합을 구성한 경우 Slack에서 구성한 채널에 알림을 보내도록 PagerDuty 통합이 구성됩니다. 이러한 알림은 문제가 발생한 시기를 나타냅니다.
 * Slack 도구 통합을 구성한 경우 Slack에서 구성한 채널에 알림을 보내도록 Slack 통합이 구성됩니다. 이러한 알림은 배치의 진행상태를 표시합니다(예: `프로젝트 XYZ와 연결됨`, `파이프라인이 구성됨` 및 `'빌드' 단계가 시작됨`).
 * GitHub 도구 통합을 구성한 경우 샘플 GitHub 저장소가 GitHub 계정에 복제됩니다.

 
##도구 체인 보기
{: #viewing_a_toolchain}

도구 체인과 모든 도구 통합을 구성하고 나면 도구 통합 페이지에서 도구 체인의 시각적 표시를 볼 수 있습니다.

1. DevOps 대시보드의 **도구 체인** 탭에서 도구 체인을 클릭하여 도구 통합 페이지를 여십시오. 또는 앱 개요 페이지의 Continuous Delivery 타일에서 **도구 체인 보기**를 클릭한 다음 **도구 통합**을 클릭하십시오.
1. 페이지를 검토하여 도구 체인의 시각적 표시를 확인하십시오.
1. 도구 체인에 있는 도구 통합에 액세스하려면 도구 타일을 클릭하십시오. 
 
 **팁**: GitHub 저장소가 두 개 이상이면 각 저장소에 고유 파이프라인이 필요하므로 동일한 도구 통합에 여러 타일이 있을 수 있습니다.


 <!-- The toolchain in the following image is an example. When you create your own toolchain, the visual representation of the toolchain shows the tool integrations that you configure.
![Sample toolchain](images/toolchain.png) -->


# 관련 링크
{: #rellinks}

## 학습서 및 샘플
{: #samples}

* [세 개의 마이크로 서비스가 포함된 애플리케이션 작성](https://www.ibm.com/devops/method/tutorials/tutorial_microservices_part1){:new_window}

## 관련 링크
{: #general}

* [마이크로 서비스 도구 체인(실험)](https://www.ibm.com/devops/method/toolchains/microservices_toolchain){:new_window}
* [단순 도구 체인(실험)](https://www.ibm.com/devops/method/toolchains/simple_toolchain){:new_window}
* [IBM&reg; Bluemix&reg; Garage Method](https://www.ibm.com/devops/method){:new_window}
