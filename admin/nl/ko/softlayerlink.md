---

 

copyright:

  years: 2016
lastupdated: "2016-12-01"
 

---

{:shortdesc: .shortdesc}
{:codeblock: .codeblock}
{:screen: .screen}
{:new_window: target="_blank"}

# {{site.data.keyword.Bluemix_notm}} 및 SoftLayer 청구 계정 업그레이드 및 통합
{: #softlayerlink}

{{site.data.keyword.Bluemix_notm}} 평가판 계정을 보유하고 있으며 인프라 대시보드에 액세스하려는 경우 {{site.data.keyword.Bluemix_notm}} 종량과금제 계정으로 업그레이드해야 합니다. 또한 평가판 계정에서 사용할 수 없는 다른 유료 리소스를 사용하려는 경우에도 업그레이드해야 합니다. 그렇지 않으면 평가판 계정이 완료됩니다. 

계정을 연결하여 기존 {{site.data.keyword.Bluemix_notm}} 및 SoftLayer 청구 계정을 통합할 수 있습니다. 계정을 연결하면, {{site.data.keyword.Bluemix_notm}} 및 SoftLayer 리소스 모두가 {{site.data.keyword.Bluemix_notm}}를 통해 청구됩니다.


**주의:** {{site.data.keyword.Bluemix_notm}} 구독 계정을 SoftLayer 계정과 연결할 수 없습니다. 인프라 대시보드에 액세스하려면 SoftLayer 계정과 자동으로 연결되는 두 번째 계정인 종량과금제 계정을 작성해야 합니다. {{site.data.keyword.Bluemix_notm}} 계정에 대해 한 개, 즉 두 개의 송장을 수신합니다. 인프라 리소스에 개별 종량과금제 계정에서 송장을 보내는 경우에도, 구독 계정의 앱과 서비스에 자원을 사용할 수 있습니다. 예를 들어, 구독 계정에서 Watson 서비스를 활성화하는 경우, 서비스 신임 정보를 복사하여 종량과금제 계정에서 제공되는 베어메탈 애플리케이션에 추가할 수 있습니다.
{:shortdesc}

## {{site.data.keyword.Bluemix_notm}} 종량과금제 계정으로 업그레이드
{: #upgradetopayg}

평가판 계정을 사용하여 {{site.data.keyword.Bluemix_notm}}에 로그인하는 경우 {{site.data.keyword.Bluemix_notm}} 인프라 대시보드에 액세스할 수 없습니다. 앱에서 인프라 리소스를 사용하려는 경우 종량과금제 계정으로 업그레이드해야 합니다. 

평가판 계정을 {{site.data.keyword.Bluemix_notm}} 종량과금제 계정으로 업그레이드하려면 다음 단계를 따르십시오. 

 1. **계정** &gt; **비용 청구**를 클릭하십시오.
 2. 그런 다음 **신용카드 추가**를 클릭하십시오. 
 3. 필수 비용 청구 세부사항을 입력하십시오.  
 4. 종량과금제 계정에 대한 이용약관을 읽은 후 동의하십시오.  
 5. 완료하면 **업그레이드**를 클릭하십시오.  
 
종량과금제 계정으로 업그레이드한 후 **인프라** 옵션이 {{site.data.keyword.Bluemix_notm}} **카탈로그**에 표시됩니다. 무료 사용량을 초과하여 사용한 경우 매달 {{site.data.keyword.Bluemix_notm}} 송장을 받게 됩니다. 송장은 미국 달러(USD)로 청구되며 리소스 비용에 대한 세부사항이 기재되어 있습니다.  

## {{site.data.keyword.Bluemix_notm}} 및 SoftLayer 계정 통합
{: #unifyingaccounts}

{{site.data.keyword.Bluemix_notm}} 및 SoftLayer 계정을 통합하여 결합된 리소스를 이용할 수 있습니다. {{site.data.keyword.Bluemix_notm}}와 Softlayer 계정을 연결한 경우 단일 {{site.data.keyword.Bluemix_notm}} 송장을 받게 됩니다. 기존 {{site.data.keyword.Bluemix_notm}} 계정을 보유하는 경우, {{site.data.keyword.Bluemix_notm}}를 통한 SoftLayer 리소스의 청구는 계정이 연결된 이후 시작되는 새 청구 주기에 적용됩니다.


**중요사항:** {{site.data.keyword.Bluemix_notm}}의 모든 연결된 계정은 종량과금제 계정이어야 합니다. 종량과금제 계정을 새로 작성하거나 기존 종량과금제 계정을 연결할 수 있습니다. 또는 기존 시험판 계정을 연결할 수 있지만, 이는 종량과금제 계정으로 업그레이드됩니다. 구독 {{site.data.keyword.Bluemix_notm}} 계정을 연결할 수 없습니다.   

계정이 연결된 후 다음을 수행하십시오. 

* IBM ID 신임 정보를 사용하여 SoftLayer 계정과 {{site.data.keyword.Bluemix_notm}} 계정에 액세스하십시오. 
* 기존 SoftLayer 할인은 {{site.data.keyword.Bluemix_notm}} 비용에 적용됩니다.  
* 미국 달러(USD)로 된 송장을 받게 됩니다. 
* {{site.data.keyword.BluSoftlayer}} 사용자 인터페이스에서 {{site.data.keyword.Bluemix_notm}} 리소스의 사용량을 모니터링할 수 있습니다.  

**주의:** 일단 계정이 연결되면 연결을 해제할 수 없습니다.  

SoftLayer 계정을 보유 중이며 {{site.data.keyword.Bluemix_notm}} 계정을 연결하려면 다음 단계를 완료하십시오. 

 1. {{site.data.keyword.slportal}}에서 **{{site.data.keyword.Bluemix_notm}} 계정 연결**을 클릭하십시오. 
 2. SoftLayer 및 {{site.data.keyword.Bluemix_notm}} 계정의 연결과 관련된 이용 약관을 읽고 이에 동의하십시오. 
 3. 요청이 있으면 {{site.data.keyword.Bluemix_notm}} 계정과 연관된 이메일 주소를 입력하십시오. {{site.data.keyword.Bluemix_notm}} 계정이 없으면, 사용하고자 하는 이메일 주소를 입력한 후에 지시사항에 따라 {{site.data.keyword.Bluemix_notm}}에 방문하여 계정을 작성하십시오. 

계정을 연결하려면 SoftLayer 계정의 마스터 사용자여야 합니다. 

계정이 연결되면, SoftLayer 글로벌 헤더에서 **{{site.data.keyword.Bluemix_notm}}로 이동** 링크를 사용할 수 있습니다. 이 링크를 클릭하면 {{site.data.keyword.Bluemix_notm}} 로그인 페이지로 이동됩니다. 또한 {{site.data.keyword.Bluemix_notm}} 헤더에서 이제 **SoftLayer** 링크를 사용할 수 있습니다. 링크를 클릭하면 새 창에서 {{site.data.keyword.slportal}}의 홈 페이지로 이동됩니다. 

{{site.data.keyword.Bluemix_notm}} 인프라 오퍼링은 3계층 네트워크, 퍼블릭, 사설 및 관리 트래픽 세분화에 연결됩니다. 고객의 {{site.data.keyword.Bluemix_notm}} 계정에 대한 인프라 오퍼링은 무료로 사설 네트워크에서 데이터를 서로 전송할 수 있습니다.
베어메탈 서버, 가상 서버 및 클라우드 스토리지와 같은 인프라 오퍼링은 퍼블릭 네트워크를 통해 {{site.data.keyword.Bluemix_notm}} 카탈로그(예: Watson 서비스, 컨테이너 또는 런타임)의 다른 애플리케이션 및 서비스에 연결합니다. 두 유형의 오퍼링 간의 데이터 전송은 표준 퍼블릭 네트워크 대역폭 비율로 측정되고 청구됩니다. 

## {{site.data.keyword.Bluemix_notm}}에 SoftLayer 팀 구성원 초대
{: #invite_users}

{{site.data.keyword.Bluemix_notm}} 및 SoftLayer 계정을 연결할 때 {{site.data.keyword.Bluemix_notm}}에 가입하도록 SoftLayer SoftLayer 팀 구성원을 초대할 수 있습니다. 또는 {{site.data.keyword.Bluemix_notm}} 사용자 인터페이스에서 나중에 SoftLayer SoftLayer 팀 구성원을 초대할 수 있습니다.
{:shortdesc}

{{site.data.keyword.Bluemix_notm}} 사용자 인터페이스에서, SoftLayer 계정의 모든 구성원을 초대하도록 선택하거나 개별 구성원을 선택할 수 있습니다. 팀 구성원을 초대할 때는 초대되는 사용자의 {{site.data.keyword.Bluemix_notm}} 계정 역할을 설정해야 합니다. {{site.data.keyword.Bluemix_notm}}의 다양한 역할에 대한 자세한 정보는 [사용자 역할](https://console.ng.bluemix.net/docs/admin/users_roles.html#userrolesinfo)을 참조하십시오. 

{{site.data.keyword.Bluemix_notm}} 계정에 팀 구성원을 초대하려면 SoftLayer 계정의 마스터 사용자이어야 합니다. 

{{site.data.keyword.Bluemix_notm}}를 통해 팀 구성원을 초대하려면 다음 단계를 완료하십시오. 

 1. **계정** &gt; **팀 구성원 초대**를 클릭하십시오.
 2. **추가**를 클릭하여 SoftLayer 계정으로 인증하고 {{site.data.keyword.BluSoftlayer}} 계정에서 팀 구성원의 목록을 보십시오. 
 3. 초대할 팀 구성원을 선택하고 **전송**을 클릭하십시오. 
 
팀 구성원은 **조직 가입** 링크가 포함된 이메일을 받습니다. 팀 구성원에게 IBM ID가 없으면 팀 구성원이 등록 페이지로 경로 재지정됩니다. 그리고 팀 구성원은 일부 기본 정보를 입력하고 {{site.data.keyword.Bluemix_notm}} 계정을 작성할 수 있습니다. 

{{site.data.keyword.Bluemix_notm}} 사용자 인터페이스를 통한 팀 구성원 초대에 대한 자세한 정보는 [팀 구성원 초대](https://console.ng.bluemix.net/docs/admin/users_roles.html#inviteteammembers)를 참조하십시오. 

## IBM ID로 전환
{: #ibmid_switch}

이제 SoftLayer의 인증은 {{site.data.keyword.Bluemix_notm}}에 대한 단일 로그인을 제공하는 IBM ID를 사용합니다. 기존 SoftLayer 계정이 있는 경우 IBM ID로 전환할 수 있습니다. 마이그레이션 마법사가 이 전환을 통해 사용자를 안내합니다.
{:shortdesc}

IBM ID로의 전환을 시작한 후 프로세스를 완료하지 않은 경우에는 이를 취소할 수 있습니다. 그러나 다음 번에 로그인할 때 전환하라는 메시지가 계속해서 표시될 것입니다. 

기존 SoftLayer 사용자 이름을 IBM ID로 전환하는 작업을 시작하려면 다음 단계를 완료하십시오. 

 1. {{site.data.keyword.slportal}}에서 사용자 프로파일 편집으로 이동한 후 **IBM ID로 전환**을 클릭하십시오.
 2. 마이그레이션 마법사 프롬프트를 따라 IBM ID를 작성하십시오. IBM ID를 작성하면 이메일 주소인 ID를 변경할 수 없습니다. 사용자의 프로파일과 연관된 이메일을 업데이트할 수 있으나 기본적으로 이 값은 IBM ID에 대해 정의한 값으로 설정됩니다. 마법사를 완료하면 이메일이 전송됩니다. 
 3. 이메일을 수신하면 링크를 따르거나 URL을 브라우저로 복사하고 등록 코드를 입력하십시오. 코드는 7일간 유효하며 한 번만 사용 가능합니다. 사용한 후에는 다시 사용할 수 없습니다. IBM ID를 SoftLayer 사용자 링크로 설정한 후 IBM ID로만 계정에 로그인할 수 있습니다. SoftLayer 사용자 이름 및 비밀번호를 입력하는 대신에 로그인 대화 상자에서 **IBM ID로 로그인** 단추를 사용해야 합니다. 
 
신규 고객인 경우 주문을 완료할 때 기존 IBM ID 계정에 대한 이메일 주소 또는 새 IBM ID 계정 생성을 요청 받습니다.  

### 여러 SoftLayer 계정을 하나의 IBM ID로 맵핑
{: #map_multiple_accounts}

주문을 설정할 때 기존 IBM ID 이메일 주소를 사용하여 하나의 IBM ID를 여러 SoftLayer 계정과 연관시킬 수 있습니다. 각 계정에 대한 한 명의 SoftLayer 사용자만 단일 IBM ID로 맵핑될 수 있습니다. IBM ID는 각 SoftLayer 계정 내에서 고유해야 합니다. 그러나 여러 SoftLayer 계정에 대한 액세스 권한이 있는 한 명의 사용자가 여러 SoftLayer 계정에 액세스할 수 있는 하나의 IBM ID를 사용할 수 있습니다. 

예를 들어, IBM ID는 계정 A 및 B의 마스터 사용자 및 계정 C 및 계정 D의 추가 사용자로 맵핑할 수 있습니다. 해당 IBM ID로 맵핑되는 계정 중 하나가 기본 계정이 됩니다. 일반적으로 기본 계정은 IBM ID로 처음 맵핑되는 계정입니다. 그러나 고객 포털의 계정 전환 기능을 통해 계정(기본 계정)을 전환할 수 있습니다. 

2단계 인증이 사용된 여러 계정에 대한 IBM ID 액세스 권한이 있는 사용자의 경우 계정 로그인 및 계정 전환 중에 적절한 2단계 인증 확인 코드(계좌당)가 필요합니다. 

## SoftLayer 자산으로 {{site.data.keyword.Bluemix_notm}} 서비스 사용
{: #bluemix_services}

SoftLayer 자산으로 API 기반 퍼블릭 {{site.data.keyword.Bluemix_notm}} 서비스를 손쉽게 사용할 수 있습니다. 모든 API는 사용자 데이터의 보호를 위해 보안이 유지되고 암호화됩니다.
{:shortdesc}

예를 들어, Watson의 코그너티브 기능을 SoftLayer의 베어메탈 서버에서 실행 중인 앱에 추가하고자 한 적이 있습니까? {{site.data.keyword.personalityinsightsshort}} 등의 서비스를 추가하면 4개의 간편한 단계로 앱 사용자를 파악하는 데 도움이 될 수 있습니다. 

1. {{site.data.keyword.Bluemix_notm}} 카탈로그에서 서비스를 찾으십시오. 
2. 수 차례의 클릭만으로 서비스의 인스턴스를 제공하십시오. 
3. 서비스 신임 정보를 복사하고 이를 사용자 애플리케이션에 추가하여 기존 코드로 실행할 서비스를 설정하십시오. 
4. 앱을 업데이트한 후에 SoftLayer 인프라에 새 버전을 배치하십시오. 

SoftLayer에서 사용자 앱의 Watson API를 호출하여 이를 보다 개인화함으로써 *Insights 및 코그너티브* 지식을 얻을 수 있습니다. 또는 *데이터 및 분석* 서비스를 사용하여 앱에 대한 고성능 분석을 활용할 수 있습니다. 또는 {{site.data.keyword.Bluemix_notm}}에 관리를 맡길 수 있는 DaaS(Database-as-a-Service)를 선택하십시오. 

{{site.data.keyword.activedeployshort}} 및 {{site.data.keyword.deliverypipeline}} 등의 서비스와 함께 컨테이너를 사용하여 애플리케이션 개발을 현대화하십시오. SoftLayer와 통신하는 데 {{site.data.keyword.vpn_short}} 서비스를 사용하여 사설 네트워크의 컨테이너와 SoftLayer 사설 네트워크를 연결할 수 있습니다.
to the SoftLayer private network. 컴퓨팅 리소스 및 서비스에 대한 모든 사용 비용은 {{site.data.keyword.Bluemix_notm}} 청구서에 반영됩니다.  

### API 기반 {{site.data.keyword.Bluemix_notm}} 서비스
일부 {{site.data.keyword.Bluemix_notm}} 서비스는 SoftLayer에서 사용될 수 없습니다. 
다음 서비스를 사용자의 애플리케이션 코드에서 실행되도록 설정할 수 있습니다. 
* {{site.data.keyword.alchemyapishort}}
* {{site.data.keyword.alertnotificationshort}}
* {{site.data.keyword.sparks}}
* {{site.data.keyword.appseccloudshort}}
* {{site.data.keyword.blockchain}}
* {{site.data.keyword.cloudant}}
* {{site.data.keyword.conceptinsightsshort}}
* {{site.data.keyword.iotmapinsights_short}}
* {{site.data.keyword.dashdbshort}}
* {{site.data.keyword.dialogshort}}
* {{site.data.keyword.documentconversionshort}}
* {{site.data.keyword.twittershort}}
* {{site.data.keyword.weather_short}}
* {{site.data.keyword.iotdriverinsights_short}}
* {{site.data.keyword.geospatialshort_Geospatial}}
* {{site.data.keyword.graphshort}}
* {{site.data.keyword.iotelectronics}}
* {{site.data.keyword.languagetranslationshort}}
* {{site.data.keyword.messagehub}}
* {{site.data.keyword.mqa}}
* {{site.data.keyword.mobileappbuilder_short}}
* {{site.data.keyword.mql}}
* {{site.data.keyword.nlclassifierlshort}}
* {{site.data.keyword.objectstorageshort}}
* {{site.data.keyword.personalityinsightsshort}}
* {{site.data.keyword.presenceinsightsshort}}
* {{site.data.keyword.relationshipextractionshort}}
* {{site.data.keyword.retrieveandrankshort}}
* {{site.data.keyword.servicediscoveryshort}}
* {{site.data.keyword.speechtotextshort}}
* {{site.data.keyword.sqldb}}
* {{site.data.keyword.streaminganalyticsshort}}
* {{site.data.keyword.texttospeechshort}}
* {{site.data.keyword.toneanalyzershort}}
* {{site.data.keyword.tradeoffanalyticsshort}}
* {{site.data.keyword.visualinsightsshort}}
* {{site.data.keyword.visualrecognitionshort}}
* {{site.data.keyword.workflow}}
* {{site.data.keyword.workloadscheduler}}

**참고:** 이 서비스의 일부 플랜은 사용 가능하지 않습니다. 종량과금제 계정에 사용되는 플랜만 연결된 계정에서 사용될 수 있습니다. 그러나 별도로 청구되는 별도의 {{site.data.keyword.Bluemix_notm}} 계정이 있으면 이러한 서비스에 대해 임의의 플랜을 사용할 수 있습니다. 

## 계정 연결 시 {{site.data.keyword.Bluemix_notm}} 사용에 대한 청구
{: #bill_usage}

{{site.data.keyword.Bluemix_notm}} 및 SoftLayer 청구 계정을 연결한 이후, 다음 청구 주기는 단일 {{site.data.keyword.Bluemix_notm}} 청구로 부과됩니다.
{:shortdesc}

{{site.data.keyword.Bluemix_notm}} 사용 주기가 달력 월 기반이므로, 사용자 계정은 비용 계약에 대해 설정된 청구일에 매월 청구됩니다. SoftLayer에서 사용 주기는 SoftLayer가 시작된 시점에서 시작됩니다. 따라서 사용자에게는 매월 SoftLayer 계정에 서명한 날과 동일한 날에 청구됩니다.  

계정이 연결되면, {{site.data.keyword.Bluemix_notm}} 사용량이 계속해서 당월 주기에 대해 측정되며 사용자는 {{site.data.keyword.Bluemix_notm}} 송장에서 해당 사용량에 대해 청구됩니다. 다음 달 초에 시작하여, {{site.data.keyword.Bluemix_notm}} 및 SoftLayer 비용은 {{site.data.keyword.Bluemix_notm}} 송장에서 통합됩니다. 

예를 들어, 4월 16일에 계정을 연결한 경우에는 4월 사용량에 대해 Bluemix 송장을 받습니다. 연결된 계정에 따라 SoftLayer 사용량에 대해 별도로 청구될 수 있습니다. SoftLayer 및 {{site.data.keyword.Bluemix_notm}}의 사용량이 {{site.data.keyword.Bluemix_notm}} 계정을 통해 청구될 수 있습니다. 

![Bluemix 및 SoftLayer 계정 연결 요약](images/BluemixSoftLayerBill.svg)

청구서가 연결된 후 {{site.data.keyword.Bluemix_notm}} 송장이 사용한 각 리소스에 대한 개별 비용을 다음 표제 아래에 표시합니다. 

* **베어메탈 서버 및 첨부된 서비스**
* **가상 서버 및 첨부된 서비스**
* **첨부되지 않은 서비스**

{{site.data.keyword.Bluemix_notm}} 사용량을 보는 방법에 대한 정보는 [사용량 세부사항 보기](https://console.ng.bluemix.net/docs/pricing/index.html#usage)를 참조하십시오. 

