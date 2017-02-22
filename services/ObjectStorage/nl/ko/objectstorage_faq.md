---

copyright:
  years: 2014, 2017
lastupdated: "2017-01-17"

---
{:new_window: target="_blank"}
{:shortdesc: .shortdesc}

# FAQ {: #faq}

이 FAQ에서는 {{site.data.keyword.objectstorageshort}} 서비스에 대한 일반적인 질문의 답을 제공합니다.
{: shortdesc}


## {{site.data.keyword.objectstorageshort}}에서 사용할 수 있는 계정과 결제 플랜은 무엇입니까? {: #account-payment}

{{site.data.keyword.objectstorageshort}} 서비스는 무료와 표준이라는 두 개의 플랜 옵션을 제공합니다. [가격 책정](https://www.ibm.com/cloud-computing/bluemix/pricing/)은 선택된 플랜에 따라 다릅니다. 

<table>
<caption> 표 1. 무료 사용제와 표준 플랜 비교</caption>
  <tr>
    <th> 무료 사용제 </th>
    <th> 표준 플랜 </th>
  </tr>
  <tr>
    <td> {{site.data.keyword.Bluemix_notm}} 조직에 한 번에 하나의 서비스 인스턴스만 있도록 허용 </td>
    <td> 무제한 서비스 인스턴스 </td>
  </tr>
  <tr>
    <td> 모든 사용자가 사용할 수 있음 </td>
    <td> {{site.data.keyword.Bluemix_notm}} 유료 계정과 IBM 내부 사용자만 사용할 수 있음 </td>
  </tr>
  <tr>
    <td> 무료 </td>
    <td> 종량과금제 또는 구독 결제 플랜 </td>
  </tr>
  <tr>
    <td> 기본 5GB 스토리지 사용 제한 포함 </td>
    <td> 무제한 스토리지 </td>
  </tr>
</table>

**주의**: {{site.data.keyword.Bluemix_notm}} 평가판 계정을 사용하여 작업하는 사용자는 무료 사용제를 사용할 수 있습니다. 평가판 만료 후에는 연관된 {{site.data.keyword.objectstorageshort}} 서비스 인스턴스를 사용할 수 없습니다. 이는 스토리지 계정에 액세스할 수 없음을 의미합니다. 30일 후 {{site.data.keyword.Bluemix_notm}} 계정이 영구 제거되고 모든 데이터는 삭제됩니다. 데이터가 손실되지 않게 하려면 가능한 한 빨리 [유료 {{site.data.keyword.Bluemix_notm}} 계정](/docs/admin/account.html)으로 업그레이드하십시오. 

## 내 플랜을 어떻게 변경합니까? {: #changeplan}  
베타를 통해 작성되거나 무료 사용제에서 작성된 인스턴스는 표준 플랜으로 업그레이드할 수 있습니다. 연관된 조직이 {{site.data.keyword.Bluemix_notm}} 유료 계정이어야 합니다. Object Storage 인스턴스가 있는 평가판 계정을 표준 플랜으로 업그레이드할 수 없으며 표준 플랜의 인스턴스를 기타 플랜으로 다운그레이드할 수 없습니다. 업그레이드하는 경우, 서비스 인스턴스와 고객 데이터는 새 플랜으로 이동됩니다. 

업그레이드하려면 다음을 수행하십시오. 
1.	{{site.data.keyword.objectstorageshort}} 사용자 인터페이스에서 **플랜**을 클릭하십시오. 
2.	**표준**을 새 플랜으로 선택한 후 **저장**을 클릭하십시오.

명령행 인터페이스를 사용하여 [결제 플랜 변경](/docs/pricing/index.html#changing)을 수행할 수도 있습니다. 

## {{site.data.keyword.objectstorageshort}} 사용에 대한 요금 산정 및 청구 방법은 무엇입니까? {: #charge-bill}

{{site.data.keyword.objectstorageshort}} 서비스는 사용량에 대해서만 요금을 청구합니다. 서비스 사용을 시작하는 데 필요한 요금 또는 약정이 없습니다. API 요청 또는 인바운드 데이터 네트워크 트래픽에 대한 요금은 청구되지 않습니다. 

{{site.data.keyword.objectstorageshort}}는 청구 주기 동안 스토리지 사용량을 기반으로 요금이 청구됩니다. 여기에는 {{site.data.keyword.Bluemix_notm}} 조직에서 작성한 컨테이너의 모든 오브젝트 데이터가 포함됩니다. 

공용 네트워크를 통해 오브젝트 컨테이너에서 데이터를 읽을 때마다 아웃바운드 데이터 전송 요금이 적용됩니다. 청구 주기에서 이용되는 모든 대역폭은 공용 아웃바운드 대역폭으로 요금이 청구됩니다. 

청구 주기 종료 시 {{site.data.keyword.Bluemix_notm}}에서 해당 청구 기간 동안의 사용량에 대해 자동으로 요금을 청구합니다. {{site.data.keyword.Bluemix_notm}} 보고를 통해 현재 청구 주기에 대해 청구된 요금을 볼 수 있습니다.

## 내 {{site.data.keyword.Bluemix_notm}} 지역과 내 스토리지 지역은 같습니까? {: #region}

{{site.data.keyword.objectstorageshort}} 서비스에서는 댈러스 스토리지 지역과 런던 스토리지 지역을 지원합니다. 해당 스토리지 지역은 {{site.data.keyword.objectstorageshort}} 서비스 인스턴스가 작성되는 {{site.data.keyword.Bluemix_notm}} 지역(예: 미국 남부와 영국)에 독립적입니다. 미국 남부 {{site.data.keyword.Bluemix_notm}} 지역에서 인스턴스를 작성하는 경우 댈러스 또는 런던 스토리지 지역에서 데이터를 읽고 쓸 수 있습니다. 스토리지 지역은 {{site.data.keyword.Bluemix_notm}} 지역을 기반으로 기본값이 설정됩니다. UI의 드롭 다운 목록에서 다른 지역을 선택하여 지역을 전환할 수 있습니다. 
