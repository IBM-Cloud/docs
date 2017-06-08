---



copyright:

  years: 2015, 2017
lastupdated: "2017-04-12"

---

{:shortdesc: .shortdesc}
{:codeblock: .codeblock}
{:screen: .screen}
{:new_window: target="_blank"}

# 비용 추정
{: #cost}

다른 방법을 통해 {{site.data.keyword.Bluemix_notm}}를 사용하여 앱을 빌드하고 호스팅하기 위해 지불해야 하는 비용을 확인할 수 있습니다. 

* {{site.data.keyword.Bluemix_notm}} {{site.data.keyword.pricing_sheet}}의 비용 추정기는
앱의 크기를 기반으로 비용의 대략적인 추정치를 제공합니다. 
* {{site.data.keyword.Bluemix_notm}} 가격 책정 페이지의 비용 계산기는 런타임 및 서비스 사용에 대한 입력 내용을 기반으로 정확한 앱 가격을 제공합니다.
* 또한 비용을 수동으로 계산할 수도 있습니다.

## 비용 계산기 사용
{: #calculator}

{{site.data.keyword.Bluemix_notm}}에서 제공하는 비용 계산기를 사용하면 앱의 비용을 신속하게 계산할 수 있습니다.

1. {{site.data.keyword.Bluemix_notm}} {{site.data.keyword.pricing_sheet}}로 이동하십시오.
2. 인프라 위젯 중 하나를 사용하거나 **가격 책정 계산기**를 클릭하십시오. 

계산기를 사용하려면 나열된 리소스(예: 인스턴스 수 또는 푸시 알림 수)의 매월 예상 사용량을 입력하십시오. **월별 사용량** 필드 안쪽을 클릭하면 필드에서 예상되는 단위에 대한 힌트를 볼 수 있습니다. 계산기는 입력 내용에 대한 비용을 즉시 표시합니다. 월간 비용 대신 연간 비용을 표시하도록 계산기를 조정할 수도 있습니다.

## 수동으로 비용 계산
{: #manual}

{{site.data.keyword.Bluemix_notm}}의 비용 계산 방식을 더 잘 이해하도록 {{site.data.keyword.Bluemix_notm}} 비용을 직접 추정하고자 할 수 있습니다. 사용되는 런타임과 서비스의 가격을 고려하여 {{site.data.keyword.Bluemix_notm}}를 사용하여 앱을 빌드하고 호스팅하는 데 드는 총 비용을 계산할 수 있습니다. 런타임과 서비스의 가격은 종종 변경되므로, 총 가격을 계산할 경우 {{site.data.keyword.Bluemix_notm}} 가격 책정 시트에서 최신 정보를 참조해야 합니다. 

## 예: 샘플 앱 가격 책정
{: #sample}

확장 기능이 있는 Node.js 웹 앱이 있으며 이 앱이 {{site.data.keyword.Bluemix_notm}}에서 제공하는 여러 서비스를 사용한다고 가정하겠습니다. 이 예제를 통해 앱의 실제 비용이 어떻게 계산되는지 이해할 수 있습니다. 웹 앱이 사용하는 {{site.data.keyword.Bluemix_notm}} 서비스와 항목은 다음과 같습니다. 

* 256MB Node.js 런타임 인스턴스 4개
* 2개의 {{site.data.keyword.autoscaling}} 정책, 프로세서 및 메모리
* 매월 2GB의 {{site.data.keyword.datacshort}}
* 매월 150GB의 NoSQL 데이터베이스, Heavy API 호출 100,000개 및 Light API 호출 500,000개
* 20GB의 인바운드 또는 아웃바운드 네트워크 트래픽

## Bluemix 리소스의 가격
{: #sample_resources}

예를 단순화하기 위해 다음 표의 가격은 특정 시간 범위(예: 한 달) 내에서 또는 시간 범위 간에 변동되지 않는다고 가정합니다. 이 예의 모든 가격은 미국 통화입니다. 

|서비스 |	기능 |	가격 |
|--------|-----------|--------|
|SDK for Node.js |	매월 375GB-시간 무료(모든 런타임에서 공유됨) |	$0.07 USD/GB-시간|
|Auto-Scaling |	Auto-Scaling 서비스에 대한 무료 서비스 플랜 |	무료|
|데이터 캐시 - 스타터 |	1GB의 캐시 공간 및 복제본 |	$55.00 USD/인스턴스 |
|데이터 캐시 - 표준 |	5GB의 캐시 공간 및 복제본 |	$155.00 USD/인스턴스 |
|데이터 캐시 - 프리미엄 |	25GB의 캐시 공간 및 복제본 |	$505.00 USD/인스턴스|
|IBM Cloudant® NoSQL DB for {{site.data.keyword.Bluemix_notm}} |	2GB의 사용 가능한 데이터 스토리지<br/>매월 50,000개의 Light API 호출 무료<br/>매월 10,000개의 Heavy API 호출 무료 | $1.00 USD/GB<br/>$0.03 USD/1000개의 Light API 호출<br/>$0.15 USD/1000개의 Heavy API 호출 |
{:caption="표 1. 가격 책정 시트" caption-side="top"}

## 앱 가격 계산

앱 가격은 다음과 같은 방법으로 계산될 수 있습니다. 

<dl>
<dt>256MB Node.js 런타임 인스턴스 4개</dt>
<dd>Bluemix에서는 런타임 비용을 GB-시간 단위로 청구합니다. 매월 사용량(GB)은 <code>월별 4 x 256 = 1024MB 또는 1GB</code>입니다. <code>한 달은 24 x 30 = 720시간</code>으로 가정하므로 애플리케이션의 비용이 <code>1 x 720 = 720GB-시간</code>으로 청구됩니다.
<p>
375GB-시간은 매달 무료 사용량에 포함되며, 모든 {{site.data.keyword.Bluemix_notm}} 런타임에서 공유됩니다. 런타임의 총 비용은 <code>$0.07 x (720-375) = $24.15</code>입니다. </p></dd>

<dt>2개의 Auto-Scaling 정책(프로세서 및 메모리)</dt>
<dd>Auto-Scaling 정책은 무료입니다.</dd>

<dt>매월 2GB의 데이터 캐시</dt>
<dd>데이터 캐시 서비스에서 50MB 플랜을 무료로 제공합니다. 그러나 무료 사용제로는 매달 2GB의 예상 사용량을 충당할 수 없습니다. 데이터 캐시에 대한 3개의 유료 사용제를 사용할 경우 실제로 사용하는 공간의 양에 관계없이 특정 공간량에 대해 정해진 비용이 듭니다. 따라서 예상 사용량을 충족하는 최소 플랜을 선택할 수 있는데, 이것이 표준 플랜(5GB)입니다. 총 비용은 매달 $155입니다. </dd>

<dt>매월 150GB의 NoSQL 데이터베이스</dt>
<dd>IBM Cloudant NoSQL DB for {{site.data.keyword.Bluemix_notm}} 서비스 비용은 데이터 스토리지 및 여러 API 메소드로 데이터에 액세스할 수 있는지에 따라 달라집니다. <strong>PUT</strong> 및 <strong>POST</strong> 명령은 Heavy API 호출로 간주되지만, <strong>GET</strong> 명령은 Light API 호출로 간주됩니다.
<p>
GB 수를 더한 다음 2GB 무료 사용량을 빼십시오. 매달 148GB가 청구됩니다. Light API 호출의 경우 무료 사용량인 50,000을 빼고, Heavy API 호출의 경우 10,000을 빼십시오. 총 스토리지 가격에는 다음과 같은 파트가 포함됩니다. </p>
<pre class="codeblock">
<codeblock>
    148 x 1 = $148
    (450,000 / 1000) x 0.03 = $13.5
    (90,000 / 1000) x 0.15 = $13.5
</codeblock>
</pre>
<p>
총 가격은 148 + 13.5 + 13.5 = $175입니다. </p></dd>

<dt>20GB의 인바운드 또는 아웃바운드 네트워크 트래픽</dt>
<dd>인바운드 및 아웃바운드 네트워크 트래픽은 무료입니다. </dd>

</dl>

모든 항목을 더할 경우 총 애플리케이션 가격은 $354.15입니다. 

## 지원되는 통화

가격 책정 예에서는 미국 달러(USD)가 사용되지만 {{site.data.keyword.Bluemix_notm}}에서는 다른 통화도 지원됩니다. 다음 표는 지원되는 다양한 통화를 나열합니다. 

|ISO 4217 코드| 통화|
|-------------|---------|
|AUD |	  호주 달러|
|BRL |	  브라질 레알|
|CAD |	  캐나다 달러|
|CHF |	  스위스 프랑|
|DKK |	  덴마크 크로네|
|EUR |	  유로|
|GBP |	  파운드 스털링|
|INR |	  인도 루피|
|JPY |	  일본 엔|
|KRW |	  한국 원|
|NOK |	  노르웨이 크로네|
|NZD |	  뉴질랜드 달러|
|SEK |	  스웨덴 크로나|
|USD |    미국 달러|
|ZAR |	  남아프리카공화국 란드|
{:caption="표 2. 지원되는 통화" caption-side="top"}

**참고:** 연결된 {{site.data.keyword.Bluemix_notm}} 및 SoftLayer 계정이 있으면 발급되는 단일 송장은 미국 달러(USD)만 사용됩니다.
