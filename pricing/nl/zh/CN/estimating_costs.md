---



copyright:

  years: 2015, 2017
lastupdated: "2017-04-12"

---

{:shortdesc: .shortdesc}
{:codeblock: .codeblock}
{:screen: .screen}
{:new_window: target="_blank"}

# 估算成本
{: #cost}

您可以使用不同的方法来了解通过 {{site.data.keyword.Bluemix_notm}} 构建和托管应用程序所需的费用。

* {{site.data.keyword.Bluemix_notm}} {{site.data.keyword.pricing_sheet}} 上的成本估算工具根据您应用程序的大小来提供粗略的成本估算。
* {{site.data.keyword.Bluemix_notm}}“定价”页面上的成本计算器根据您输入的运行时和服务使用量来提供准确的应用程序价格。
* 您还可以手动计算成本。

## 使用成本计算器
{: #calculator}

您可以通过使用 {{site.data.keyword.Bluemix_notm}} 提供的成本计算器，对应用程序进行快速定价。

1. 转至 {{site.data.keyword.Bluemix_notm}} {{site.data.keyword.pricing_sheet}}。
2. 使用其中一个 Infrastructure 窗口小部件，或者单击**定价计算器**。

要使用该计算器，请键入所列资源的每月计划使用量；例如，实例数或推送通知数。单击**每月的使用情况**字段，以获取有关字段中预期的单元的提示。计算器会针对您的输入立即显示价格。您还可以调整计算器，以显示每年成本，而不是每月成本。

## 手动计算成本
{: #manual}

您可能想要自己估算 {{site.data.keyword.Bluemix_notm}} 成本，以更好地了解 {{site.data.keyword.Bluemix_notm}} 成本的计算方式。您可以考虑运行时和它使用的服务的价格，计算使用 {{site.data.keyword.Bluemix_notm}} 构建和托管应用程序的总价格。由于运行时和服务的价格有时会更改，因此在计算总价格时必须参考 {{site.data.keyword.Bluemix_notm}} 价格表上的最新信息。

## 示例：对样本应用程序定价
{: #sample}

假定您拥有具有可扩展能力的 Node.js Web 应用程序，并且该应用程序使用 {{site.data.keyword.Bluemix_notm}} 提供的多个服务。在此示例中，您可以了解如何计算应用程序的实际成本。Web 应用程序使用以下 {{site.data.keyword.Bluemix_notm}} 服务和项：

* 四个 256 MB Node.js 运行时实例
* 两个 {{site.data.keyword.autoscaling}} 策略、处理器和内存
* 每月 2 GB（针对 {{site.data.keyword.datacshort}}）
* NoSQL 数据库每月 150 GB、100,000 个频繁 API 调用和 500,000 个稀少 API 调用
* 20 GB 入站或出站网络流量

## Bluemix 资源的价格
{: #sample_resources}

为简化示例，假设下表中的价格在某个时间范围（例如，一个月）内不波动。此示例中的所有定价使用美元。

|服务 |	功能 |	价格 |
|--------|-----------|--------|
|SDK for Node.js |	每月 375 GB-小时可用（在所有运行时共享） |	0.07 美元/GB-小时|
|Auto-Scaling |	Auto-Scaling 服务的免费服务套餐 |	免费|
|Data Cache - 入门级 |	1 GB 高速缓存空间和副本 |	55.00 美元/实例 |
|Data Cache - 标准 |	5 GB 高速缓存空间和副本 |	155.00 美元/实例 |
|Data Cache - 高级 |	25 GB 高速缓存空间和副本 |	505.00 美元/实例|
|IBM Cloudant® NoSQL DB for {{site.data.keyword.Bluemix_notm}} |	2 GB 免费数据存储<br/>每月 50,000 个免费稀少 API 调用<br/>每月 10,000 个免费频繁 API 调用 | 1.00 美元/GB<br/>0.03 美元/1000 个稀少 API 调用<br/>0.15 美元/1000 个频繁 API 调用 |
{:caption="表 1. 价格表" caption-side="top"}

## 计算应用程序价格

可以使用以下方式来计算应用程序的价格：

<dl>
<dt>四个 256 MB Node.js 运行时实例</dt>
<dd>Bluemix 对运行时按 GB-小时收费。每月使用的 GB 数是 <code>4 x 256 = 1024 MB 或 1 GB/月</code>。假设<code>一个月有 24 x 30 = 720 小时</code>，那么应用程序按 <code>1 x 720 = 720 GB-小时</code>收费。<p>
375 GB-小时包括在每月免费限额中，在所有 {{site.data.keyword.Bluemix_notm}} 运行时共享。因此，运行时的总成本为 <code>0.07 美元 x (720-375) = 24.15 美元</code>。</p></dd>

<dt>两个 Auto-Scaling 策略（处理器和内存）</dt>
<dd>Auto-Scaling 策略免费。</dd>

<dt>每月 2 GB（针对 Data Cache）</dt>
<dd>Data Cache 服务提供的 50 MB 套餐免费。然而，免费套餐可能难以满足您每月计划使用的 2 GB。Data Cache 的 3 个付费套餐都是以固定金额购买特定的空间量，而不管您实际使用的空间量是多少。因此，您希望选择符合您计划使用量（标准套餐为 5 GB）的最低限度套餐。每月总开销为 155 美元。</dd>

<dt>NoSQL 数据库每月 150 GB</dt>
<dd>IBM Cloudant NoSQL DB for {{site.data.keyword.Bluemix_notm}} 服务费用基于数据存储和按不同 API 方法访问该数据的能力。<strong>PUT</strong> 和 <strong>POST</strong> 命令被视为频繁 API 调用，但 <strong>GET</strong> 命令被视为稀少 API 调用。<p>
加总 GB 数并减去 2 GB 免费限额。每月对 148 GB 收费。减去 50,000 稀少 API 调用和 10,000 频繁 API 调用的免费限额。存储价格总计包括以下部分：</p>
<pre class="codeblock">
<codeblock>
148 x 1 = 148 美元
    (450,000 / 1000) x 0.03 = 13.5 美元
    (90,000 / 1000) x 0.15 = 13.5 美元
</codeblock>
</pre>
<p>
总价格为 148 + 13.5 + 13.5 = 175 美元。</p></dd>

<dt>20 GB 入站或出站网络流量</dt>
<dd>入站和出站网络流量免费。</dd>

</dl>

加总所有项时，应用程序的总价格为 354.15 美元。

## 支持的货币

虽然定价示例中使用的是美元 (USD)，但 {{site.data.keyword.Bluemix_notm}} 中还支持其他货币。下表列出了支持的不同货币。

|ISO 4217 代码| 货币|
|-------------|---------|
|AUD |	  澳元|
|BRL |	  巴西雷亚尔|
|CAD |	  加拿大元|
|CHF |	  瑞士法郎|
|DKK |	  丹麦克郎|
|EUR |	  欧元|
|GBP |	  英镑|
|INR |	  印度卢比|
|JPY |	  日元|
|KRW |	  韩元|
|NOK |	  挪威克朗|
|NZD |	  新西兰元|
|SEK |	  瑞典克朗|
|USD |    美元|
|ZAR |	  南非兰特|
{:caption="表 2. 支持的货币" caption-side="top"}

**注：**如果已链接您的 {{site.data.keyword.Bluemix_notm}} 和 SoftLayer 帐户，那么您收到的单个发票只使用美元 (USD)。
