{:new_window: target="_blank"}

# FAQ {: #faq} 

*마지막 업데이트 날짜: 2016년 7월 18일*
{: .last-updated}


## 선택하는 플랜에 따라 가격이 달라짐 {: #plan-price}
가격 책정은 선택된 플랜에 따라 다릅니다. 자세한 가격 책정 정보를 보려면 [IBM Bluemix 가격 책정 시트](https://console.ng.bluemix.net/pricing/){: new_window}를 참조하거나 [계산기](https://console.ng.bluemix.net/?direct=classic/#/pricing/cloudOEPaneId=pricing&paneId=pricingSheet){: new_window}를 사용하여 자세한 추정 금액을 확인하십시오. 


## {{site.data.keyword.objectstorageshort}}에 사용할 수 있는 계정과 유료 플랜 {: #account-payment}
{{site.data.keyword.objectstorageshort}} 서비스에는 여러 플랜 옵션이 제공됩니다. IBM의 GA(General Availability) 릴리스의 경우 현재 두 개의 플랜(표준과 무료)이 제공됩니다. {{site.data.keyword.Bluemix_notm}} 유료 계정(종량과금제 또는 구독)과 IBM 내부 사용자만 표준 플랜을 사용할 수 있습니다. 표준 플랜은 계정당 스토리지 사용량에 대해 가입 기념 5GB의 무료 크레딧 사용량을 제공합니다. 

여전히 활성인 평가판 계정에서는 무료 사용제를 사용할 수 있으며 이 사용제는 {{site.data.keyword.Bluemix_notm}} 조직에 하나의 인스턴스만 있도록 허용합니다. {{site.data.keyword.Bluemix_notm}} 평가판 만료 후에는 연관된 {{site.data.keyword.objectstorageshort}} 서비스 인스턴스를 사용할 수 없습니다. 이는 {{site.data.keyword.Bluemix_notm}} 사용자 인터페이스 또는 명령행에서 스토리지 계정에 액세스할 수 없음을 의미합니다. 30일의 유예 기간 이후 {{site.data.keyword.Bluemix_notm}} 계정은 영구 제거되고 모든 데이터는 삭제됩니다. 데이터가 손실되지 않게 하려면 가능한한 빨리 {{site.data.keyword.Bluemix_notm}} 유료 계정으로 업그레이드하는 것이 좋습니다. 계정을 업그레이드하려면, 사용자 관리 메뉴를 클릭하고 **계정**을 선택하십시오. 업그레이드 프로세스에 대한 지시사항이 제공됩니다. 

## 내 플랜을 변경하는 방법 {: #changeplan}  
베타를 통해 작성되거나 무료 사용제에서 작성된 인스턴스는 표준 플랜으로 업그레이드할 수 있습니다. 연관된 조직이 {{site.data.keyword.Bluemix_notm}} 유료 계정이어야 합니다. {{site.data.keyword.objectstorageshort}} 인스턴스가 있는 평가판 계정을 표준 플랜으로 업그레이드할 수 없으며 표준 플랜의 인스턴스를 기타 플랜으로 다운그레이드할 수 없습니다. 업그레이드하는 경우, 서비스 인스턴스와 고객 데이터는 새 플랜으로 이동됩니다. 

플랜 업그레이드 방법: 
1.	{{site.data.keyword.objectstorageshort}} 사용자 인터페이스에서 **플랜**을 클릭하십시오. 
2.	**표준**을 새 플랜으로 선택한 후 **저장**을 클릭하십시오.

명령행 인터페이스를 사용하여 유료 플랜도 변경할 수 있습니다. 자세한 정보는 [플랜 변경 방법](../../pricing/index.html#changing)을 참조하십시오. 


## {{site.data.keyword.objectstorageshort}} 사용 요금 산정 및 청구 방법 {: #charge-bill}

{{site.data.keyword.objectstorageshort}} 서비스는 사용량에 대해서만 요금을 청구합니다. 서비스 사용을 시작하는 최소 요금, 설정 요금 또는 약정이 없습니다. API 요청 또는 인바운드 데이터 네트워크 트래픽에 대한 요금은 청구되지 않습니다.

{{site.data.keyword.objectstorageshort}} 사용량은 비용 청구 주기 동안 스토리지 사용량을 기반으로 요금이 청구됩니다. 여기에는 {{site.data.keyword.Bluemix_notm}} 조직 계정으로 작성한 컨테이너의 모든 오브젝트 데이터가 포함됩니다. 

공용 네트워크를 통해 오브젝트 컨테이너에서 데이터를 읽을 때마다 아웃바운드 데이터 전송 요금이 적용됩니다. 공용 아웃바운드 대역폭은 비용 청구 주기에 이용한 모든 대역폭에 대해 청구됩니다. 

{{site.data.keyword.objectstorageshort}} 가격 책정의 메트릭 컴포넌트는 다음과 같습니다.
* 스토리지 사용량  - 월별 GB당 $0.04
* 공용 아웃바운드 데이터 전송  - 월별 GB당 $0.09 

요금 청구 주기 종료 시, {{site.data.keyword.Bluemix_notm}}에서 현재 요금 청구 주기 동안 사용한 양에 대한 비용을 자동으로 청구합니다. {{site.data.keyword.Bluemix_notm}} 보고를 통해 현재 비용 청구 주기에 대해 청구된 요금을 볼 수 있습니다.

런던과 댈러스용으로 릴리스된 표준 서비스 플랜의 가격 책정은 동일합니다.

## {{site.data.keyword.objectstorageshort}}에서 데이터 복제 수행 방법 {: #replication}
{{site.data.keyword.objectstorageshort}} 서비스는 여러 스토리지 노드에 복제되는 데이터에 대해 3개의 사본을 유지보수합니다. 자세한 정보는 [OpenStack Swift Replication](http://docs.openstack.org/developer/swift/overview_replication.html){: new_window} 문서를 참조하십시오. 

