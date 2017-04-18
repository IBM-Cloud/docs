---

copyright:
  years: 2015, 2016
lastupdated: "2016-11-21"

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen:.screen}
{:codeblock:.codeblock}

# Decahose 及 PowerTrack 串流 {: #decahose_powertrack}

{{site.data.keyword.twittershort}} 可讓您根據 {{site.data.keyword.Bluemix_notm}} 計劃登記存取 Twitter Decahose 及 PowerTrack 串流。這兩個串流提供即時資訊來源及不同性質來符合您的需求。
{:shortdesc}

Decahose 串流是 Twitter Firehose 的 10% 隨機取樣。推文是即時從 Twitter 衍生而來，且串流是由 Twitter 的取樣演算法所決定。對於大部分統計分析來說，10% 隨機樣本已相當精確。Decahose 資料會以 2 年的期間編製索引，因此查詢回應可能不會傳回超過 2 年的推文。可在「免費方案」及「入門方案」中存取 Decahose，但只有「入門方案」使用者才能存取 PowerTrack 串流。

PowerTrack 串流提供新增的好處，根據使用者定義的規則型過濾器（稱為追蹤）過濾送入的推文。作為「入門方案」使用者，您可以每個帳戶建立高達 1,000 個規則。如需進階過濾，可以結合多項追蹤，以構成聚集的追蹤。下列各節說明追蹤狀態、內容，以及您可以對追蹤執行的支援動作，例如編輯、刪除以及其他動作。

**附註**：編製 PowerTrack 串流的索引限制為每個行事曆月 1 百萬篇推文。一旦達到限制，就會停止該月份的檢索。在下個月開始時，您可以重新啟動您的追蹤；它們不會自動啟動。若要極致使用串流，高度建議適當地管理您的追蹤。例如，可以讓冗餘追蹤成為非作用中。

## 追蹤類型 {: #track_types}

「入門方案」使用者可以建立自訂的追蹤，來過濾 PowerTrack 資料串流中收集的訊息。{{site.data.keyword.twittershort}} 支援下列兩種追蹤類型。

<dl>
<dt>Rule</dt>
<dd>在此追蹤中收集的所有訊息都符合至少一個與追蹤相關聯的規則。您可以在此追蹤類型內新增、編輯及刪除規則。規則型追蹤內支援完整的 [GNIP PowerTrack 規則語法](http://support.gnip.com/apis/powertrack2.0/rules.html)。所有查詢必須符合 {{site.data.keyword.twittershort}} [查詢語言](twitter_rest_apis.html#querylanguage "查詢語言")。
</dd>

<dt>Aggregated</dt>
<dd>兩個以上規則追蹤或聚集的追蹤的組合。聚集的追蹤用於將多個追蹤任意分組。您可以從聚集的追蹤類型新增及刪除個別追蹤。個別規則無法新增至聚集的追蹤；基於這個目的，請改用規則追蹤。聚集的追蹤沒有狀態，但其組成規則追蹤不是 **Active** 就是 **Inactive**。</dd>
</dl>

## 追蹤內容 {: #track_properties}
追蹤包含下列內容。部分內容無法同時適用於規則型追蹤和聚集的追蹤。例如，rules 內容不適用於聚集的追蹤。

<dl>
<dt>createdDate</dt>
<dd>指出追蹤的建立日期；指定為 `YYYYMMDDHHMM`。</dd>

<dt>endDate</dt>
<dd>指出追蹤停止收集訊息的時間。指定值必須是未來日期，並遵循下列其中一個格式：`YYYY-MM-DD` 或 `YYYY-MM-DDTHH:MM:SSZ`。指定過去日期會傳回 HTTP 400 錯誤。此內容不適用於聚集的追蹤。</dd>

<dt>id</dt>
<dd>建立時指派給追蹤的唯一 ID 參照。規則追蹤及聚集的追蹤的 ID 是以 GUID 字串格式（例如 3F2504E0-4F89-41D3-9A0C-0305E82C3301）表示。</dd>

<dt>name</dt>
<dd>追蹤的敘述性名稱。不保證此內容是唯一的。</dd>

<dt>rules</dt>
<dd>一連串定義追蹤過濾器的規則，包括查詢關鍵字及其他參數。此內容適用於規則型追蹤，但不適用於聚集的追蹤。</dd>

<dt>state</dt>
<dd>必須是 **Active** 或 **Inactive**。作用中追蹤會收集訊息，而非作用中追蹤則不會。您可以隨時變更追蹤的狀態。此內容不適用於聚集的追蹤。</dd>

<dt>trackIds</dt>
<dd>一連串的追蹤 ID。此內容僅適用於聚集的追蹤。</dd>

<dt>type</dt>
<dd>指出追蹤類型是 **Rule** 還是 **Aggregated**。如需追蹤內容的相關資訊，包括追蹤作業及模型綱目，請參閱 {{site.data.keyword.twittershort}} REST API 文件。</dd>
</dl>

