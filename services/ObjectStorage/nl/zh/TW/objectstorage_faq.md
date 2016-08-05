{:new_window: target="_blank"}

# 常見問題 (FAQ) {: #faq} 

*前次更新：2016 年 7 月 18 日*
{: .last-updated}


## 價格如何視選擇的方案而改變？ {: #plan-price}
定價會視選擇的方案而改變。如需其他定價資訊，請參閱 [IBM Bluemix 定價單](https://console.ng.bluemix.net/pricing/){: new_window}，或使用[計算機](https://console.ng.bluemix.net/?direct=classic/#/pricing/cloudOEPaneId=pricing&paneId=pricingSheet){: new_window}以取得其他詳細的預估值。


## 可以用於 {{site.data.keyword.objectstorageshort}} 的帳戶及付款方案為何？ {: #account-payment}
{{site.data.keyword.objectstorageshort}} 服務隨附了多個方案選項。從通用版次開始，目前提供了兩個方案（標準及免費）。「標準」方案僅適用於「{{site.data.keyword.Bluemix_notm}} 付費帳戶」（隨收隨付制或訂閱）以及 IBM 內部使用者。「標準」方案包含針對每個帳戶儲存空間用量的介紹性 5 GB 免費信用額度。

仍然有效的試用帳戶可以使用「免費」方案， 該方案在「{{site.data.keyword.Bluemix_notm}} 組織」中只容許有一個實例。在 {{site.data.keyword.Bluemix_notm}} 的試用時間到期之後，將會停用相關聯的 {{site.data.keyword.objectstorageshort}} 服務實例，這表示不論透過 {{site.data.keyword.Bluemix_notm}} 使用者介面或指令行都無法存取儲存空間帳戶。在 30 天的寬限期過後，將會清除您的 {{site.data.keyword.Bluemix_notm}} 帳戶，並刪除所有資料。為了避免資料流失，建議您儘快升級為「{{site.data.keyword.Bluemix_notm}} 付費帳戶」。若要升級您的帳戶，請按一下使用者管理功能表，然後選取**帳戶**，這會提供升級程序的相關指示。

## 如何變更方案？ {: #changeplan}  
透過測試版或在「免費」方案中建立的實例可以升級至「標準」方案。相關聯的組織必須是 {{site.data.keyword.Bluemix_notm}} 付費帳戶。{{site.data.keyword.objectstorageshort}} 實例的試用帳戶無法升級至「標準」方案，而「標準」方案中的實例無法降級至其他方案。當您升級時，您的服務實例與客戶資料會移至新方案。

如果要升級您的方案，請執行下列動作：
1.	在 {{site.data.keyword.objectstorageshort}} 使用者介面，按一下**方案**。
2.	選取**標準**作為新方案，然後按一下**儲存**。

您也可以使用指令行介面來變更付款方案。如需相關資訊，請參閱[如何變更您的方案](../../pricing/index.html#changing)。


## {{site.data.keyword.objectstorageshort}} 的使用如何付費及計費？ {: #charge-bill}

{{site.data.keyword.objectstorageshort}} 服務只會向您收取所使用項目的費用。沒有最低費用、沒有設定費用，也沒有開始使用服務的承諾。API 要求或入埠資料網路資料流量不需付費。

使用 {{site.data.keyword.objectstorageshort}} 的計費是根據您在計費週期內的儲存空間用量。這包括透過 {{site.data.keyword.Bluemix_notm}} 組織帳戶所建立的容器中的所有物件資料。 

只要透過公用網路從任何物件容器讀取資料，就會收取「出埠資料傳送」費用。「公用出埠頻寬」的計費是針對計費週期中耗用的所有頻寬。

{{site.data.keyword.objectstorageshort}} 的度量值元件定價如下：
* 儲存空間用量 - 1 個月 1 GB $0.04
* 公用出埠資料傳送 - 1 個月 1 GB $0.09 

在計費週期結束時，{{site.data.keyword.Bluemix_notm}} 會自動計算現行計費期間的用量的費用。您可以透過 {{site.data.keyword.Bluemix_notm}} 報告來檢視現行計費期間的費用。

倫敦及達拉斯的標準服務方案的定價相同。

## 如何在 {{site.data.keyword.objectstorageshort}} 中執行資料抄寫？ {: #replication}
{{site.data.keyword.objectstorageshort}} 服務會針對您的資料維護三份副本，它們會跨多個儲存節點進行抄寫。如需相關資訊，請參閱 [OpenStack Swift Replication](http://docs.openstack.org/developer/swift/overview_replication.html){: new_window} 文件。

