---

copyright:
  years: 2016
lastupdated: "2016-10-06"

---

<!-- Common attributes used in the template are defined as follows: -->
{:new_window: target="\_blank"}
{:shortdesc: .shortdesc}
{:screen:.screen}
{:codeblock:.codeblock}


# 문제점 해결
{: #troubleshooting}

{{site.data.keyword.Bluemix_notm}}에서 {{site.data.keyword.iotinsurance_full}} 사용에 대한 공통 문제점 해결 질문에 대한 답변입니다.
{:shortdesc}

## 앱 배치 문제점
{: #deployingapps}

{{site.data.keyword.Bluemix_notm}} 조직에 충분한 여유 메모리가 없으면 {{site.data.keyword.iotinsurance_short}}에 대한 앱을 배치하지 못할 수도 있습니다. 앱이 사용하는 메모리를 줄이거나 사용자 계정에 할당된 메모리를 늘릴 수 있습니다.

### 발생하는 문제

{{site.data.keyword.iotinsurance_short}} 서비스를 열 때 배치 기능이 사용 가능하지 않으면 앱을 배치할 수 없습니다.

### 발생 이유

배치 기능을 사용하기 위해서는 최소 2GB의 여유 메모리가 사용자의 조직에 있어야 합니다. 시험판 계정에는 최대 2GB 메모리가 할당되어 있습니다. {{site.data.keyword.iotinsurance_short}}가 아닌 서비스 또는 앱을 작성한 경우 조직에 {{site.data.keyword.iotinsurance_short}} 앱을 배치할 수 있는 충분한 메모리가 없습니다. 

### 해결 방법

계정의 메모리 할당을 늘리거나 서비스 및 앱에서 사용하는 메모리를 줄일 수 있습니다.

  - 계정의 메모리 할당을 늘리기 위해 [시험판 계정을 유료 계정으로 전환](https://console.ng.bluemix.net/docs/pricing/index.html#pay-accounts)할 수 있습니다.

  - 사용 중인 메모리를 빠르게 줄이려면 {{site.data.keyword.iotinsurance_short}}가 아닌 모든 서비스와 앱을 제거하십시오. 변경이 적용되도록 {{site.data.keyword.iotinsurance_short}} 서비스를 다시 시작하십시오. 

  - 총 2GB가 넘는 메모리를 유료 계정의 경우 기타 앱이나 서비스에서 사용하는 메모리 양을 조정하여 기타 앱 또는 서비스를 제거하는 것을 피할 수 있습니다. 자세한 정보는 [조직의 메모리 한계 초과](https://console.ng.bluemix.net/docs/troubleshoot/ts_apps.html#ts_outofmemory)를 참조하십시오.
