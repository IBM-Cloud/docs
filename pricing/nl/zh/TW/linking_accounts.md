---



copyright:

  years: 2015, 2017
lastupdated: "2017-04-12"

---

{:shortdesc: .shortdesc}
{:codeblock: .codeblock}
{:screen: .screen}
{:new_window: target="_blank"}

# 鏈結 Bluemix 與 SoftLayer 帳戶
{: #unifyingaccounts}

您可以鏈結 {{site.data.keyword.Bluemix_notm}} 與 SoftLayer 帳戶，以利用結合的資源。當您鏈結 {{site.data.keyword.Bluemix_notm}} 與 Softlayer 帳戶時，會收到一張 {{site.data.keyword.Bluemix_notm}} 發票。如果您有現有的 {{site.data.keyword.Bluemix_notm}} 帳戶，則會在帳戶鏈結之後開始的新計費週期，透過 {{site.data.keyword.Bluemix_notm}} 收取 SoftLayer 資源的費用。

**重要事項：**{{site.data.keyword.Bluemix_notm}} 中所有鏈結的帳戶都必須是「隨收隨付制」帳戶。您可以建立新的「隨收隨付制」帳戶、鏈結現有「隨收隨付制」帳戶，或鏈結現有試用帳戶（然後會升級至「隨收隨付制」帳戶）。您無法鏈結訂閱 {{site.data.keyword.Bluemix_notm}} 帳戶。

您必須是 SoftLayer 帳戶的主要使用者，才能鏈結帳戶。

鏈結帳戶時：

* 您必須使用 IBM ID 認證來存取 SoftLayer 及 {{site.data.keyword.Bluemix_notm}} 帳戶。
* 任何現有 SoftLayer 折扣都會套用至 {{site.data.keyword.Bluemix_notm}} 費用。
* 您將收到一張計價單位為美元 (USD) 的發票。
* 您可以在 {{site.data.keyword.Bluemix_notm}} 主控台中監視 {{site.data.keyword.BluSoftlayer}} 資源的用量。

**注意：**帳戶在鏈結之後，即無法解除鏈結。  

身為主要使用者，請完成下列步驟來鏈結 {{site.data.keyword.Bluemix_notm}} 與 SoftLayer 帳戶：

 1. 從 {{site.data.keyword.slportal}}，按一下**鏈結 {{site.data.keyword.Bluemix_notm}} 帳戶**。
 2. 閱讀並接受將 SoftLayer 帳戶與 {{site.data.keyword.Bluemix_notm}} 帳戶鏈結所適用的條款。
 3. 當系統要求時，提供與 {{site.data.keyword.Bluemix_notm}} 帳戶相關聯的電子郵件位址。如果您沒有 {{site.data.keyword.Bluemix_notm}} 帳戶，請提供您要使用的電子郵件位址，然後遵循指示，以受邀加入 {{site.data.keyword.Bluemix_notm}} 並建立帳戶。

鏈結帳戶之後，SoftLayer 主控台功能表列中即會提供**移至 {{site.data.keyword.Bluemix_notm}}**。按一下此鏈結，即可讓您進入 {{site.data.keyword.Bluemix_notm}} 登入頁面。

## 帳戶鏈結後的 {{site.data.keyword.Bluemix_notm}} 用量計費
{: #bill_usage}

鏈結 {{site.data.keyword.Bluemix_notm}} 與 SoftLayer 計費帳戶之後，將以一張 {{site.data.keyword.Bluemix_notm}} 帳單收取下一個計費週期的費用。
{:shortdesc}

您的 {{site.data.keyword.Bluemix_notm}} 使用週期是以行事曆月份為基準，所以會在收費合約成立的帳單日，每個月向您的帳戶收費。使用 SoftLayer 時，您的使用週期是從 SoftLayer 起始使用日開始，所以會以 SoftLayer 帳戶註冊當月的相同日期，每月向您收費。 

帳戶鏈結之後，會繼續計算當月週期的 {{site.data.keyword.Bluemix_notm}} 用量，並且會在 {{site.data.keyword.Bluemix_notm}} 發票上向您收取該用量的費用。從下個月 1 日開始，{{site.data.keyword.Bluemix_notm}} 及 SoftLayer 費用將會結合到 {{site.data.keyword.Bluemix_notm}} 發票。

例如，如果您在 2017 年 4 月 16 日鏈結帳戶，則會收到 4 月用量的 Bluemix 發票。視鏈結帳戶的時間而定，您可能會收到 SoftLayer 用量的個別帳單。SoftLayer 及 {{site.data.keyword.Bluemix_notm}} 的五月用量將會透過 {{site.data.keyword.Bluemix_notm}} 帳戶向您收費。

![Bluemix 帳戶與 SoftLayer 帳戶的鏈結摘要](/docs/pricing/BluemixSoftLayerBill.svg)

鏈結帳單之後，{{site.data.keyword.Bluemix_notm}} 發票即會針對您所使用的每一項資源列出不同費用：
