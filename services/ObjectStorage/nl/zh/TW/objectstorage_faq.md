---

copyright:
  years: 2014, 2016

---
{:new_window: target="_blank"}
{:shortdesc: .shortdesc}

# 常見問題 (FAQ) {: #faq}

*前次更新：2016 年 10 月 19 日*
{: .last-updated}

此常見問題 (FAQ) 提供 {{site.data.keyword.objectstorageshort}} 服務常見問題的回答。
{: shortdesc}


## 可以用於 {{site.data.keyword.objectstorageshort}} 的帳戶及付款方案為何？ {: #account-payment}

{{site.data.keyword.objectstorageshort}} 服務提供兩個方案選項：「免費」及「標準」。[定價](https://console.ng.bluemix.net/pricing/)視選擇的方案而定。

<table>
  <tr>
    <th> 免費方案</th>
    <th> 標準方案</th>
  </tr>
  <tr>
    <td> {{site.data.keyword.Bluemix_notm}} 組織中一次僅容許一個服務實例。</td>
    <td> 無限制的服務實例</td>
  </tr>
  <tr>
    <td> 所有人都可以使用</td>
    <td> 只有 {{site.data.keyword.Bluemix_notm}} 付費帳戶及 IBM 內部使用者才能使用</td>
  </tr>
  <tr>
    <td> 免費</td>
    <td> 隨收隨付制或訂閱付款方案</td>
  </tr>
  <tr>
    <td> 包括入門的 5 GB 儲存空間用量限制</td>
    <td> 無限制的儲存空間</td>
  </tr>
</table>

*表 1：免費與標準方案的比較*

**注意**：使用 {{site.data.keyword.Bluemix_notm}} 試用帳戶的使用者可以使用「免費」方案。試用時間到期之後，將會停用關聯的 {{site.data.keyword.objectstorageshort}} 服務實例，這表示您將無法存取儲存空間帳戶。在 30 天之後，將會清除您的 {{site.data.keyword.Bluemix_notm}} 帳戶，並刪除所有資料。為了避免資料流失，請儘快升級為[付費 {{site.data.keyword.Bluemix_notm}} 帳戶](https://new-console.ng.bluemix.net/docs/admin/account.html)。

## 如何變更方案？ {: #changeplan}  
透過測試版或在「免費」方案中建立的實例可以升級至「標準」方案。相關聯的組織必須是 {{site.data.keyword.Bluemix_notm}} 付費帳戶。Object Storage 實例的試用帳戶無法升級至「標準」方案，「標準」方案中的實例也無法降級至其他方案。當您升級時，您的服務實例與客戶資料會移至新方案。

若要升級，請執行下列動作：
1.	在 {{site.data.keyword.objectstorageshort}} 使用者介面，按一下**方案**。
2.	選取**標準**作為新方案，然後按一下**儲存**。

您也可以使用指令行介面來[變更付款方案](../../pricing/index.html#changing)。

## {{site.data.keyword.objectstorageshort}} 的使用如何付費及計費？ {: #charge-bill}

{{site.data.keyword.objectstorageshort}} 服務只會向您收取所使用項目的費用。沒有設定費用，也沒有開始使用服務的承諾。API 要求或入埠資料網路資料流量不需付費。

{{site.data.keyword.objectstorageshort}} 的計費是根據您在計費週期內的儲存空間用量。這包括在 {{site.data.keyword.Bluemix_notm}} 組織內建立之容器中的所有物件資料。

只要透過公用網路從任何物件容器讀取資料，就會收取「出埠資料傳送」費用。計費週期中耗用的所有頻寬都會被當成「公用出埠頻寬」計費。

在計費週期結束時，{{site.data.keyword.Bluemix_notm}} 會自動計算該計費期間之用量的費用。您可以透過 {{site.data.keyword.Bluemix_notm}} 報告來檢視現行計費期間的費用。
