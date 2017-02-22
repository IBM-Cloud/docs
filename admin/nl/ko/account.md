---



copyright:

  years: 2015, 2017
lastupdated: "2017-01-09"


---

{:shortdesc: .shortdesc}
{:codeblock: .codeblock}
{:screen: .screen}
{:new_window: target="_blank"}

# {{site.data.keyword.Bluemix_notm}} 계정 관리
{: #mngacct}

알림을 설정하거나 계정 사용량 또는 청구서를 보려면 **계정** 링크로 이동하십시오.
{:shortdesc}

## {{site.data.keyword.Bluemix_notm}} 등록
{: #signup}

기존 IBM ID를 사용하거나, 새 IBM ID를 작성하거나, 연합 ID를 사용하여 {{site.data.keyword.Bluemix_notm}} 계정에 등록할 수 있습니다. 연합 ID는 도메인과 사용자 신임 정보를 사용하여 IBM 웹 애플리케이션에 액세스할 수 있도록 IBM에 등록된 회사의 도메인 내에서 사용되는 ID입니다.   

사용자 회사에서 등록할 수 있도록 IBM과 이미 작업을 한 경우에만 연합 ID를 사용하여 {{site.data.keyword.Bluemix_notm}}에 등록할 수 있습니다. 회사의 도메인을 IBM에 등록하면 사용자가 기존 회사 사용자 신임 정보를 사용하여 IBM 제품과 서비스에 로그인할 수 있습니다. 그런 다음 회사의 ID 제공자가 인증을 처리합니다. 연합 ID를 사용하여 {{site.data.keyword.Bluemix_notm}}에 로그인하는 경우 회사의 로그인 페이지를 통해 로그인하도록 프롬프트가 표시됩니다. 회사 또는 조직의 도메인을 IBM에 등록하도록 요청하는 방법에 대한 정보 또는 프로세스에 대한 자세한 정보는 [IBMid Enterprise Federation Adoption Guide ![외부 링크 아이콘](../icons/launch-glyph.svg)](https://ibm.box.com/v/IBMid-Federation-Guide){: new_window}를 참조하십시오. 연합 ID 등록을 요청하는 경우 오퍼링 중재자 또는 클라이언트 중재자와 같은 IBM 스폰서가 필요합니다. 

| 등록 방법       | 세부사항 |    
|-----------------|---------|
|기존 IBM ID | IBM ID가 이미 있는 경우 기타 IBM 제품과 서비스에 사용하는 기존 신임 정보로 {{site.data.keyword.Bluemix_notm}}에 등록하십시오. 등록할 때 전화번호를 입력해야 합니다.  |
|새 IBM ID | IBM ID가 없는 경우에는 이를 작성할 수 있습니다. IBM ID를 사용하면 {{site.data.keyword.Bluemix_notm}}를 비롯하여 사용하는 모든 IBM 제품과 서비스에 하나의 로그인 사용자 이름을 사용할 수 있습니다. 이름과 성, 전화번호, 새 신임 정보의 비밀번호를 포함한 개인 정보를 입력해야 합니다. 기타 IBM 제품과 서비스 사용 시 이 IBM ID를 사용하여 로그인할 수 있습니다.   |
|연합 ID | 사용자 회사가 회사 도메인에서 생성된 사용자 신임 정보를 IBM에 등록하도록 요청한 경우 회사의 로그인에 이미 사용하고 있는 신임 정보를 이용해 {{site.data.keyword.Bluemix_notm}}에 등록할 수 있습니다. 등록할 때 전화번호를 입력해야 합니다.  |
{:caption="표 1. 등록 방법" caption-side="top"}

## 알림 설정
{: #notifications}

일반 계정과 지출 알림을 설정하려면 **계정** &gt; **알림**을 클릭하십시오. 지출 알림은 구독 및 종량과금제 {{site.data.keyword.Bluemix_notm}} 계정 소유자에 대해서만 사용 가능합니다.

{{site.data.keyword.Bluemix_notm}} 인시던트 및 계획된 유지보수에 대해 플랫폼 이메일 알림을 설정할 수 있으며, 사용자 계정이 사용자가 지정한 지출 임계값과 근사하면 사용자에게 경보를 보내는 지출 알림을 설정할 수 있습니다. 다음 태스크를 완료하여 사용자 계정의 서로 다른 알림 유형을 설정하십시오.

### 플랫폼 알림 설정

{{site.data.keyword.Bluemix_notm}} 인시던트와 계획된 유지보수에 대한 이메일 알림을 설정하려면 **계정** &gt; **알림** &gt; **플랫폼**을 클릭하십시오. 각 옵션을 선택하거나 선택 취소하여 이메일 알림을 사용 또는 사용 안함으로 설정할 수 있습니다.

<!-- staging only

**Note**: You are always alerted by email about emergencies and pricing changes.

On the **Platform** tab you can also customize notifications for your orgs, spaces, or applications. Complete the following steps to add a customized notification:

<ol>
<li>Select **Add a Notification**.</li>
<li>Use the search field to find the org, application, service, or resource that you want to set a notification for, or expand the item in the pre-populated list.</li>
<li>Select *Email* to set the notification type.</li>
</ol>

staging only end -->

### 지출 알림 설정
{: #spendingnotifications}

구독 또는 종량과금제 {{site.data.keyword.Bluemix_notm}} 계정 소유자인 경우 이메일 지출 알림을 설정할 수 있습니다. 써드파티 서비스를 제외하고 개별 서비스에 대한 지출뿐만 아니라 총 계정, 런타임, 컨테이너 및 서비스 지출에 대한 알림을 설정하십시오. 지정한 지출 임계값의 80%, 90%, 및 100% 에 도달하면 알림을 받게 됩니다. 요구가 변경되면 언제든지 각 지출 알림을 편집할 수 있습니다.

지출 한계에 대한 이메일 알림을 설정하려면 다음 단계를 완료하십시오.

<ol>
<li>**계정** &gt; **알림** &gt; **지출**을 클릭하십시오.</li>
<li>숫자 값을 입력하여 각 유형의 알림마다 알림을 트리거하기 위한 지출 임계값을 설정하십시오.<br />
<ul>
<li>총 금액</li>
<li>총 런타임</li>
<li>총 서비스</li>
<li>총 컨테이너</li>
<li>특정 서비스에 대한 지출</li>
</ul>
</li>
<li>완료되면 **저장**을 클릭하십시오.</li>
</ol>

**참고**: 평가판 계정을 보유한 경우 구독 또는 종량과금제 계정으로 업그레이드하여 지출 한계를 설정할 수 있습니다. 종량과금제 및 구독 계정에 대한 자세한 정보는 [비용 청구 방법](/docs/pricing/index.html#pay-accounts)을 참조하십시오.

## 사용량 보기
{: #acctusage}

조직의 계정 소유자 또는 청구 관리자는 사용량 대시보드 페이지를 사용하여 조직에서 매달 사용하는 런타임, 컨테이너, 서비스 및 지원에 대한 실시간 요금을 확인할 수 있습니다. 모든 지역의 런타임 GB-시간 및 서비스 사용량을 확인하거나 특정 지역을 확인하도록 선택할 수 있습니다.

사용량 대시보드 페이지를 열려면 **계정** &gt; *your_account_name* &gt; **사용량 대시보드**를 클릭하십시오. 청구 관리자는 청구 관리자를 맡고 있는 조직에 대한 세부사항만 확인할 수 있습니다. 

각 청구 주기가 끝날 때 모든 조직에서 발생한 총 사용량이 계정 소유자에게 청구됩니다. 계정 소유자는 지역 및 조직별로 사용량 요약을 필터링할 수 있습니다. 특정 월을 클릭하여 해당 월의 사용량을 확인할 수도 있습니다. 계정의 모든 조직에 대한 사용량을 확인하려면 **조직** 목록에서 **모든 조직**을 선택하십시오. 

## 청구 정보 업데이트
{: #account_billing}

계정 소유자는 {{site.data.keyword.Bluemix_notm}} 계정과 연관되어 있는 저장된 신용카드 정보를 편집, 추가 또는 제거할 수 있습니다. **계정** &gt; *your_account_name* &gt; **비용 청구**를 클릭하십시오.

SoftLayer 계정이 {{site.data.keyword.Bluemix_notm}} 계정과 연결된 경우, 청구 방법에 대한 자세한 정보는 [계정 연결 시 {{site.data.keyword.Bluemix_notm}} 사용에 대한 청구](/docs/admin/softlayerlink.html#bill_usage)를 참조하십시오. 
