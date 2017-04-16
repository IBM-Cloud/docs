---

copyright:
  years: 2015, 2016
lastupdated: "2016-11-21"

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen:.screen}
{:codeblock:.codeblock}

# Decahose 和 PowerTrack 流 {: #decahose_powertrack}

{{site.data.keyword.twittershort}} 根据 {{site.data.keyword.Bluemix_notm}} 套餐注册，提供对 Twitter Decahose 和 PowerTrack 流的访问。这两种流都交付实时订阅源，但提供不同的特征以满足您的需求。
{:shortdesc}

Decahose 流是对 Twitter Firehose 的 10% 随机采样。推文实时从 Twitter 中衍生，而流由 Twitter 的采样算法确定。对于大多数统计分析，10% 的随机采样已足够准确。仅针对 2 年期间的 Decahose 数据建立索引，因此查询响应可能不会返回 2 年前的推文。免费套餐和入门套餐中都提供了对 Decahose 的访问，而对 PowerTrack 流的访问为入门套餐用户独享。

PowerTrack 流基于用户定义的基于规则的过滤器（称为跟踪），额外提供了过滤入站推文的优势功能。作为入门套餐的用户，您可以每个帐户最多创建 1000 条规则。
对于高级过滤，多个跟踪可以组合以形成聚合跟踪。以下各部分描述了跟踪状态、属性以及支持的可以对跟踪执行的操作，例如编辑、删除等。

**注**：对 PowerTrack 流建立索引限制为每个日历月 100 万个推文。达到该限制时，该月份的索引建立将停止。在下个月开始时，可以重新激活跟踪；跟踪不会自动激活。为了最充分地利用流，强烈建议对跟踪进行正确管理。例如，冗余跟踪的状态可以设为 Inactive。

## 跟踪类型 {: #track_types}

入门套餐用户可以创建可定制跟踪，以过滤在 PowerTrack 数据流中收集的消息。{{site.data.keyword.twittershort}} 支持以下两种跟踪类型。

<dl>
<dt>规则</dt>
<dd>此跟踪中收集到的所有消息都至少与和此跟踪关联的其中一条规则相匹配。可以添加、编辑和删除此跟踪类型中的规则。基于规则的跟踪中支持 [GNIP PowerTrack 规则语法](http://support.gnip.com/apis/powertrack2.0/rules.html)。所有查询必须符合 {{site.data.keyword.twittershort}} [查询语言](twitter_rest_apis.html#querylanguage "查询语言")。
</dd>

<dt>聚合</dt>
<dd>两个或更多规则或聚合跟踪的组合。聚合跟踪用于对多个跟踪随机分组。可以在聚合跟踪类型中添加和删除单个跟踪。
单个规则无法添加到聚合跟踪；请改为使用规则跟踪来执行此操作。
聚合跟踪是无状态的，但其构成规则跟踪的状态为 **Active** 或 **Inactive**。</dd>
</dl>

## 跟踪属性 {: #track_properties}
跟踪包含以下属性。某些属性并不都适用于基于规则的跟踪和聚合跟踪。例如，rules 属性不适用于聚合跟踪。

<dl>
<dt>createdDate</dt>
<dd>指示跟踪的创建时间；指定为 `YYYYMMDDHHMM`。</dd>

<dt>endDate</dt>
<dd>指示跟踪停止收集消息的时间。指定的值必须为未来时间，并且遵循下列其中一种格式：`YYYY-MM-DD` 或 `YYYY-MM-DDTHH:MM:SSZ`。指定过去的日期将返回 HTTP 400 错误。此属性不适用于聚合跟踪。</dd>

<dt>id</dt>
<dd>创建时分配给跟踪的唯一标识引用。对于规则和聚合跟踪，此标识以 GUID 字符串格式表示（例如，3F2504E0-4F89-41D3-9A0C-0305E82C3301）。</dd>

<dt>name</dt>
<dd>跟踪的描述性名称。不保证此属性的唯一性。</dd>

<dt>rules</dt>
<dd>用于定义跟踪过滤器的一组规则，包括查询关键字和其他参数。
此属性适用于基于规则的跟踪，但不适用于聚合跟踪。</dd>

<dt>state</dt>
<dd>必须为 **Active** 或 **Inactive**。活动跟踪将收集消息，而不活动跟踪不会收集消息。可以随时更改跟踪的状态。此属性不适用于聚合跟踪。</dd>

<dt>trackIds</dt>
<dd>一组跟踪标识。此属性仅适用于聚合跟踪。</dd>

<dt>type</dt>
<dd>指示跟踪类型是 **Rule** 还是 **Aggregated**。有关跟踪属性（包括跟踪操作和模型模式）的更多信息，请参阅 {{site.data.keyword.twittershort}} REST API 文档。</dd>
</dl>

