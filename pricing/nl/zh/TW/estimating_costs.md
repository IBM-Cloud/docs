---



copyright:

  years: 2015, 2017
lastupdated: "2017-04-12"

---

{:shortdesc: .shortdesc}
{:codeblock: .codeblock}
{:screen: .screen}
{:new_window: target="_blank"}

# 預估成本
{: #cost}

您可以使用不同方法來知道使用
{{site.data.keyword.Bluemix_notm}} 建置及管理您的應用程式，需要支付多少錢。

* {{site.data.keyword.Bluemix_notm}} {{site.data.keyword.pricing_sheet}}上的成本預估器會根據您的應用程式大小提供約略的成本預估。
* {{site.data.keyword.Bluemix_notm}}「定價」頁面上的成本計算機會根據您輸入的運行環境及服務用量來提供正確的應用程式價格。
* 您也可以手動計算成本。

## 使用成本計算機
{: #calculator}

您可以使用 {{site.data.keyword.Bluemix_notm}} 所提供的成本計算機快速地為應用程式計算價格。

1. 移至 {{site.data.keyword.Bluemix_notm}} {{site.data.keyword.pricing_sheet}}。
2. 使用其中一個「基礎架構」小組件，或按一下**定價計算機**。

若要使用計算機，請鍵入所列出資源的預測每月用量；例如，實例數或推送通知數。按一下**每月用量**欄位以取得欄位中所預期單位的提示。計算機會立即顯示輸入值的價格。您也可以調整計算機以顯示每年成本，而非每月成本。

## 手動計算成本
{: #manual}

您可能要自行估計 {{site.data.keyword.Bluemix_notm}} 成本，以更充分地瞭解 {{site.data.keyword.Bluemix_notm}} 成本的計算方式。您可以透過考量應用程式所使用運行環境及服務的價格，來計算使用 {{site.data.keyword.Bluemix_notm}} 建置及管理應用程式的總價格。運行環境及服務的價格有時會變更，因此，您必須在計算總價格時參照 {{site.data.keyword.Bluemix_notm}} 定價單的最新資訊。

## 範例：定價範例應用程式
{: #sample}

假設您具有含可擴充性功能的 Node.js Web 應用程式，而且應用程式使用 {{site.data.keyword.Bluemix_notm}} 所提供的數個服務。您可以瞭解在此範例中如何計算應用程式的實際成本。Web 應用程式使用下列 {{site.data.keyword.Bluemix_notm}} 服務及項目：

* 四個 256 MB Node.js 運行環境實例
* 兩個 {{site.data.keyword.autoscaling}} 原則：處理器及記憶體
* {{site.data.keyword.datacshort}} 每個月 2 GB
* NoSQL 資料庫每個月 150 GB、100,000 次重量型 API 呼叫，及 500,000 次輕量型 API 呼叫
* 20 GB 入埠或出埠網路資料流量

## Bluemix 資源的價格
{: #sample_resources}

為了保持範例的簡單性，假設下表中的價格不會在時間範圍（例如，一個月）內或之間波動。此範例中的所有定價都是美國貨幣。

|服務 |	特性 |	價格 |
|--------|-----------|--------|
|SDK for Node.js |	每個月有 375 GB-小時免費（跨所有運行環境共用） |	$0.07 USD/GB-小時|
|Auto-Scaling |	Auto-Scaling 服務的免費服務方案 |	免費|
|Data Cache - Starter |	1 GB 的快取空間及一個抄本 |	$55.00 USD/實例 |
|Data Cache - Standard |	5 GB 的快取空間及一個抄本  |	$155.00 USD/實例 |
|Data Cache - Premium |	25 GB 的快取空間及一個抄本 |	$505.00 USD/實例|
|IBM Cloudant® NoSQL DB for {{site.data.keyword.Bluemix_notm}} |	2 GB 的可用資料儲存空間<br/>每個月有 50,000 次輕量型 API 呼叫免費<br/>每個月有 10,000 次重量型 API 呼叫免費 | $1.00 USD/GB<br/>$0.03 USD/1000 次輕量型 API 呼叫<br/>$0.15 USD/1000 次重量型 API 呼叫 |
{:caption="表 1. 定價單" caption-side="top"}

## 計算應用程式價格

應用程式的價格可以使用下列方式進行計算：

<dl>
<dt>四個 256 MB Node.js 運行環境實例</dt>
<dd>Bluemix 是依 GB-小時針對運行環境計費。每個月所使用的 GB 數目為 <code>4 x 256 = 1024 MB 或 1 GB（每個月）</code>。假設<code>一個月有 24 x 30 = 720 小時</code>，因此，會依 <code>1 x 720 = 720 GB-小時</code>收取應用程式的費用。
<p>
每個月的免費額度包含 375 GB-小時（跨所有 {{site.data.keyword.Bluemix_notm}} 運行環境共用）。因此，運行環境的總成本是 <code>$0.07 x (720-375) = $24.15</code>。</p></dd>

<dt>兩個 Auto-Scaling 原則（處理器及記憶體）</dt>
<dd>Auto-Scaling 原則是免費的。</dd>

<dt>Data Cache 每個月 2 GB</dt>
<dd>Data Cache 服務提供的 50 MB 方案是免費的。不過，免費方案不包含您的預估每月 2 GB 用量。Data Cache 的三項付費方案會針對特定空間量收取已設定的金額，不論您實際使用多少空間。因此，請選擇符合您預估用量的最低方案，也就是 5 GB 的標準方案。每個月的總成本為 $155。</dd>

<dt>NoSQL 資料庫每個月 150 GB</dt>
<dd>IBM Cloudant NoSQL DB for {{site.data.keyword.Bluemix_notm}} 服務費用是根據資料儲存空間以及透過不同 API 方法存取該資料的能力。<strong>PUT</strong> 及 <strong>POST</strong> 指令視為重量型 API 呼叫，但是 <strong>GET</strong> 指令視為輕量型 API 呼叫。<p>
增加 GB 數目並扣除 2 GB 免費額度。每個月收費 148 GB。請扣除免費額度 50,000（針對輕量型 API 呼叫）及 10,000（針對重量型 API 呼叫）。總儲存空間價格包含下列部分：</p>
<pre class="codeblock">
<codeblock>
    148 x 1 = $148
    (450,000 / 1000) x 0.03 = $13.5
    (90,000 / 1000) x 0.15 = $13.5
</codeblock>
</pre>
<p>
總價格是 148 + 13.5 + 13.5 = $175。</p></dd>

<dt>20 GB 入埠或出埠網路資料流量</dt>
<dd>入埠及出埠網路資料流量免費。</dd>

</dl>

新增所有項目時，應用程式的總價格是 $354.15。

## 支援的貨幣

雖然價格範例中使用美元 (USD)，但是 {{site.data.keyword.Bluemix_notm}} 中也支援其他貨幣。下表列出支援的不同貨幣。

|ISO 4217 代碼| 貨幣|
|-------------|---------|
|AUD |	  澳幣|
|BRL |	  巴西小銀幣|
|CAD |	  加拿大幣|
|CHF |	  瑞士法郎|
|DKK |	  丹麥克朗|
|EUR |	  歐元|
|GBP |	  英鎊|
|INR |	  印度盧比|
|JPY |	  日圓|
|KRW |	  韓圜|
|NOK |	  挪威克朗|
|NZD |	  紐元|
|SEK |	  瑞典克朗|
|USD |    美元|
|ZAR |	  南非幣|
{:caption="表 2. 支援的貨幣" caption-side="top"}

**附註：**如果您已鏈結 {{site.data.keyword.Bluemix_notm}} 與 SoftLayer 帳戶，則所收到的單一發票的計價單位僅為美元 (USD)。
