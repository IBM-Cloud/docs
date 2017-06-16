---



copyright:

  years: 2015, 2017
lastupdated: "2017-04-12"

---

{:shortdesc: .shortdesc}
{:codeblock: .codeblock}
{:screen: .screen}
{:new_window: target="_blank"}

# Bluemix 및 SoftLayer 계정 연결
{: #unifyingaccounts}

{{site.data.keyword.Bluemix_notm}} 및 SoftLayer 계정을 연결하여 결합된 리소스를 활용할 수 있습니다. {{site.data.keyword.Bluemix_notm}}와 Softlayer 계정을 연결한 경우 단일 {{site.data.keyword.Bluemix_notm}} 송장을 받게 됩니다. 기존 {{site.data.keyword.Bluemix_notm}} 계정을 보유하는 경우, {{site.data.keyword.Bluemix_notm}}를 통한 SoftLayer 리소스의 청구는 계정이 연결된 이후 시작되는 새 청구 주기에 적용됩니다. 

**중요사항:** {{site.data.keyword.Bluemix_notm}}의 모든 연결된 계정은 종량과금제 계정이어야 합니다. 종량과금제 계정을 새로 작성하거나, 기존 종량과금제 계정을 연결하거나, 기존 평가판 계정을 연결할 수 있습니다(이는 다시 종량과금제 계정으로 업그레이드됨). 구독 {{site.data.keyword.Bluemix_notm}} 계정을 연결할 수는 없습니다. 

계정을 연결하려면 SoftLayer 계정의 마스터 사용자여야 합니다. 

계정이 연결된 경우: 

* IBM ID 신임 정보를 사용하여 SoftLayer 계정과 {{site.data.keyword.Bluemix_notm}} 계정에 액세스하십시오. 
* 기존 SoftLayer 할인은 {{site.data.keyword.Bluemix_notm}} 비용에 적용됩니다. 
* 미국 달러(USD)로 된 송장을 받게 됩니다. 
* {{site.data.keyword.Bluemix_notm}} 콘솔에서 {{site.data.keyword.BluSoftlayer}} 리소스의 사용량을 모니터링할 수 있습니다. 

**주의:** 일단 계정이 연결되면 해당 연결을 해제할 수 없습니다.   

마스터 사용자로서 다음 단계를 완료하여 {{site.data.keyword.Bluemix_notm}} 및 SoftLayer 계정을 연결하십시오. 

 1. {{site.data.keyword.slportal}}에서 **{{site.data.keyword.Bluemix_notm}} 계정 연결**을 클릭하십시오. 
 2. SoftLayer 및 {{site.data.keyword.Bluemix_notm}} 계정의 연결과 관련된 이용 약관을 읽고 이에 동의하십시오. 
 3. 요청이 있으면 {{site.data.keyword.Bluemix_notm}} 계정과 연관된 이메일 주소를 입력하십시오. {{site.data.keyword.Bluemix_notm}} 계정이 없으면, 사용하고자 하는 이메일 주소를 입력한 후에 지시사항에 따라 {{site.data.keyword.Bluemix_notm}}에 방문하여 계정을 작성하십시오. 

계정이 연결되면 SoftLayer 콘솔 메뉴 표시줄에서 **{{site.data.keyword.Bluemix_notm}}로 이동**을 사용할 수 있습니다. 이 링크를 클릭하면 {{site.data.keyword.Bluemix_notm}} 로그인 페이지로 이동됩니다. 

## 계정 연결 시 {{site.data.keyword.Bluemix_notm}} 사용에 대한 청구
{: #bill_usage}

{{site.data.keyword.Bluemix_notm}} 및 SoftLayer 청구 계정을 연결한 이후, 다음 청구 주기는 단일 {{site.data.keyword.Bluemix_notm}} 청구로 부과됩니다.
{:shortdesc}

{{site.data.keyword.Bluemix_notm}} 사용 주기가 달력 월 기반이므로, 사용자 계정은 비용 계약에 대해 설정된 청구일에 매월 청구됩니다. SoftLayer에서 사용 주기는 SoftLayer가 시작된 시점에서 시작됩니다. 따라서 사용자에게는 매월 SoftLayer 계정에 서명한 날과 동일한 날에 청구됩니다.  

계정이 연결되면, {{site.data.keyword.Bluemix_notm}} 사용량이 계속해서 당월 주기에 대해 측정되며 사용자는 {{site.data.keyword.Bluemix_notm}} 송장에서 해당 사용량에 대해 청구됩니다. 다음 달 초에 시작하여, {{site.data.keyword.Bluemix_notm}} 및 SoftLayer 비용은 {{site.data.keyword.Bluemix_notm}} 송장에서 통합됩니다. 

예를 들어, 2017년 4월 16일에 계정을 연결한 경우에는 4월 사용량에 대해 Bluemix 송장을 받습니다. 연결된 계정에 따라 SoftLayer 사용량에 대해 별도로 청구될 수 있습니다. SoftLayer 및 {{site.data.keyword.Bluemix_notm}}의 사용량이 {{site.data.keyword.Bluemix_notm}} 계정을 통해 청구될 수 있습니다. 

![Bluemix 및 SoftLayer 계정 연결 요약](/docs/pricing/BluemixSoftLayerBill.svg)

청구서가 연결된 후에 {{site.data.keyword.Bluemix_notm}} 송장은 사용한 각 리소스마다 서로 다른 비용을 나열합니다. 
