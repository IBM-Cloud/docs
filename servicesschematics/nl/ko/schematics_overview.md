---

copyright:
  years: 2017
lastupdated: "2017-05-16"

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}

# 정보
{: #about}

{{site.data.keyword.bplong}}를 사용하여 인프라 구성 요소를 작성할 수 있습니다. {{site.data.keyword.IBM_notm}} 클라우드 서비스를 조합하여 배치 가능하고 재사용 가능한 인프라를 작성할 수 있습니다.
{:shortdesc}

{{site.data.keyword.bpshort}}에서는 Terraform을 사용하여 인프라 관리를 간소화합니다. 예를 들어, 앱 서버의 클러스터, 로드 밸런서 및 데이터베이스 서버를 사용하는 서비스의 사본을 여러 개 만드는 경우, 해당 컴포넌트를 생성하는 명령을 실행하는 bash 스크립트를 작성할 수 있습니다. 하지만 이보다는 구성 도구를 사용하여 구성 파일에서 실제 리소스를 생성하는 방식이 더 쉽고, 더 빠르며, 더 체계적입니다. Terraform을 사용하면 여러 리소스를 동시에 집합적 그룹으로 작성할 수 있으며 여기에 종속 항목을 맵핑할 수도 있습니다. 

## {{site.data.keyword.bpshort}}를 사용할 수 있는 경우
{: #reasons}

다음과 같은 시나리오에서 코드화된 인프라를 사용할 수 있습니다.
{:shortdesc}

| 시나리오     | 이유    |
| :------------- | :------------- |
| 인프라를 재작성하고 재사용하려고 합니다. | 인프라 관리에 {{site.data.keyword.bpshort}}를 사용할 수 있습니다. {{site.data.keyword.bpshort}}를 사용하여 프로그래밍 방식으로 리소스를 프로비저닝하고, 수정하고, 영구 삭제할 수 있습니다. 리소스를 코드화하고 구성할 때, 리소스 라이브러리를 구축하고 이를 재사용하여 동일한 결과를 만들 수 있습니다.|
| 투명한 방식으로 환경을 설정하려고 합니다. | {{site.data.keyword.bpshort}}는 소스 제어의 구성에 대한 작업을 수행하므로 협업 및 검토 기능을 제공하고 변경사항이 언제, 어떻게 발생했는지 확인할 수 있는 감사 추적 기능을 제공합니다. 이전 구성으로 롤백해야 하는 경우 변경사항을 확인할 수도 있습니다. |
| 환경 변경사항에 대한 실행을 간소화하려고 합니다. | {{site.data.keyword.bpshort}}는 SSOT(Single Source of Truth)를 제공하는 선언 모델을 따릅니다. 환경에 대한 변경 플랜이 있을 경우, 원하는 출력을 명시하면 됩니다. |
| 이미 구성 관리(CM) 도구를 사용하고 있지만, 더 자동화된 방식으로 환경을 설정하려고 합니다. | CM 도구와 함께 {{site.data.keyword.bpshort}}를 작동할 수 있습니다. {{site.data.keyword.bpshort}}로 배치된 환경은 인프라 리소스를 작성할 수 있는 상위 레벨 추상입니다. CM 도구를 사용하여 {{site.data.keyword.bpshort}}에서 프로비저닝한 리소스에 소프트웨어를 설치하고 구성할 수 있습니다.  
  
## 작동 방식
{: #how}

{{site.data.keyword.bpshort}}를 사용하여 환경에 리소스를 배치할 수 있습니다.
{:shortdesc}

{{site.data.keyword.bpshort}}는 IaC(Infrastructure as Code)를 위한 기본 도구로 Terraform을 사용하여 {{site.data.keyword.IBM}} 클라우드 리소스를 코드로 정의할 수 있게 합니다. 클라우드 리소스는 베어메탈 서버, 가상 서버, 로드 밸런서, 소프트웨어 정의 네트워킹 컴포넌트와 같은 다양한 종류의 인프라 컴포넌트입니다. 

### 리소스를 정의하는 구성
{: #how-define}

구성 또는 Terraform 구성은 인프라를 구성하는 리소스를 정의하는 파일입니다. 구성은 하나 이상의 환경에 적용할 수 있는 배치 가능한 아키텍처입니다. 다음 다이어그램에서는 구성을 이루는 요소와 {{site.data.keyword.bpshort}}에 배치 가능한 환경을 작성하기 위해 각 요소가 함께 작동하는 방식을 보여줍니다.


![{{site.data.keyword.bpshort}} 아키텍처 다이어그램](/images/anatomy_of_a_schematic.png)

그림 1. {{site.data.keyword.bpshort}} 아키텍처 다이어그램

### 협업을 가능하게 하는 소스 제어
{: #how-collaborate}

팀에서 코드를 검토하고 협업할 수 있도록 구성은 GitHub에 저장됩니다. GitHub를 사용하면 감사 추적 기능이 기본으로 제공되며 구성 변경사항의 전체 커미트 히스토리를 볼 수 있습니다. 여러 팀에서 구성을 공유하고 사용할 수 있도록 readme 파일에 사용 정보를 저장할 수 있습니다.

### 리소스를 프로비저닝하는 {{site.data.keyword.bpshort}} 환경
{: #how-provision}

{{site.data.keyword.bpshort}}를 사용하여 GitHub의 코드를 스캔하고 환경에 리소스를 배치할 수 있습니다. 환경에서 공통 구성을 공유할 수 있습니다. 예를 들어, 프로덕션 환경과 비슷한 임시 QA 환경을 작성한 후, 테스트가 완료되면 이를 해체할 수 있습니다. {{site.data.keyword.Bluemix_notm}} 계정의 모든 사용자가 태그를 지정하고 검색할 수 있는, 공통 환경 구성의 라이브러리를 빌드할 수 있습니다.
