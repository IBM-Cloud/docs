---

copyright:
  years: 2016, 2017
lastupdated: "2017-3-3"

---

<!-- Common attributes used in the template are defined as follows: -->
{:new_window: target="_blank"}
{:shortdesc: .shortdesc}

# 關於 IBM {{site.data.keyword.product-insights_short}}
{: #about_product-insights}

{{site.data.keyword.product-insights_full}} 是一項 IBM Bluemix 服務，屬於 IBM Connect to Cloud 的一部分。它會將您的內部部署 IBM 軟體產品連接至 {{site.data.keyword.product-insights_short}} 服務，並提供執行中庫存與運行環境用量度量值的深入了解。

{:shortdesc}

{{site.data.keyword.product-insights_short}} 服務是進入點，未來可能會新增更多功能。

{{site.data.keyword.product-insights_short}} 提供下列特性：

* 向 IBM 登錄您的內部部署 IBM 軟體產品，尤其是 Bluemix 服務。
* 針對已連接的內部部署產品及相關聯用量資料的資料收集。
* 運行環境用量資料的儀表板，以便提供產品用量與工作負載的真實深入了解。


若要使用 {{site.data.keyword.product-insights_short}} 功能，請完成下列步驟：

1. 在 Bluemix 內為 {{site.data.keyword.product-insights_short}} 建立至少一個服務。
1. 將您的內部部署 IBM 軟體產品升級至必要的版次層次，以及新增每個產品安裝的啟用程式碼。 
1. 使用 {{site.data.keyword.product-insights_short}} 服務實例的 {{site.data.keyword.bluemix_short}} 認證配置軟體安裝。您的所有資料都會以這些認證安全地儲存。只有對服務具有適當許可權的人能夠使用該資料。



## 運作方式
{: #product-insights_howitworks}
{{site.data.keyword.product-insights_full}} 服務與您的內部部署 IBM 軟體產品整合，以便收集和顯示運行環境產品資訊與用量度量值。在一開始，會啟用一部分的 IBM 軟體產品以便與此服務整合。登錄並連接之後，內部部署軟體產品會定期傳送啟動與用量資訊。資訊透過已配置的認證與此服務實例進行相關的儲存。您可以使用服務實例儀表板，在 Bluemix 內檢視資訊。

{{site.data.keyword.product-insights_short}} 解決方案包含多個元件，如下所示：

![{{site.data.keyword.product-insights_full}} 架構](images/architecture_product-insights.png "{{site.data.keyword.product-insights_full}} 架構")。  


## 組織及空間
{: #product-insights_orgs}
您的 {{site.data.keyword.product-insights_full}} 服務與單一 Bluemix 組織及空間相關聯，並且有唯一的認證。您必須設定至少一個 Bluemix 組織及空間。如果您要區隔資料，例如，限制只有特定人能存取，則可以在組織內建立多個空間，在每個空間有一個服務實例。每個服務實例都有唯一的認證，您需要為您的 IBM 軟體產品提供此認證。

對於使用一組認證配置的產品，只能在服務內以那些認證看到其資訊。可以視需要建立多個服務來區隔資料，每個服務都具有唯一的認證。


## 服務儀表板
{: #service_dashboard}
建立服務實例之後，您會被導向服務儀表板。您隨時都可按一下組織儀表板中的服務圖示，回到服務儀表板。從服務儀表板，您可以存取下列項目：

* 開始使用文件
* 連接內部部署產品所需的服務認證
* 支援產品的庫存，以及向 {{site.data.keyword.product-insights_short}} 服務實例登錄的任何運行環境實例
* 已連接運行環境實例的用量資訊
* 已連接運行環境實例的產品及環境資訊

如果「管理」標籤中未列出任何產品，請按一下**登錄產品**，以檢視支援的產品清單，以及存取連接產品實例的特定詳細資料。
![沒有任何登錄產品的服務儀表板](images/NoRegisteredProducts.jpg "沒有任何登錄產品的服務儀表板")

## 登錄產品
{: #product-insights_register}
在**管理**標籤中，按一下**登錄產品**，以檢視支援的產品清單。捲動到您的產品，或使用搜尋欄位過濾產品的清單。
![可以登錄的已過濾產品清單](images/products-filtered.png "可以登錄的已過濾產品清單")

若要檢視登錄產品實例的指示，請從清單選取該產品。

當您將產品實例連接至 {{site.data.keyword.product-insights_short}} 服務時，它會顯示在儀表板的**管理**標籤。儀表板可以列出不同產品的多個已連接產品實例。

## 產品庫存
{: #product-insights_products}
啟用產品實例以傳送資料到 {{site.data.keyword.product-insights_short}} 之後，您可以在服務儀表板選取**管理**，來檢視您的庫存。

![具有產品及產品實例的服務儀表板](images/productinstances.png "具有產品及產品實例的服務儀表板") 

對於 {{site.data.keyword.product-insights_short}} 而言，產品與產品實例不同。產品有產品名稱，像是 IBM MQ 或 IBM WebSphere Application Server Liberty Network Deployment。產品實例用來在產品安裝並執行之後代表產品。部分產品有多個從相同產品安裝內執行的實例。例如，WebSphere Application Server Liberty Network Deployment 可以執行多個從單一產品安裝建立的伺服器。

在服務儀表板中，登錄產品的名稱會顯示在**產品**窗格中的*檢視全部* 選項下。已連接的實例列在**實例**窗格中。此窗格包含**產品**窗格中所選產品的實例。在下列範例中，所有產品實例都會顯示，因為在「產品」窗格中選取了*檢視全部* 選項。此範例顯示六個產品，部分已有多個連接實例。您可以使用**搜尋實例**欄位或選取產品項目來過濾實例清單。若要檢視產品實例的詳細資料，請在**實例**窗格中選取它的項目。

顯示的產品實例清單會在您瀏覽時過濾。為了輔助導覽，畫面上會顯示所選實例的瀏覽路徑。

![服務儀表板](images/products.png "服務儀表板") 



## 產品實例資訊
{: #product-insights_productinstances}
選取產品實例時，**實例詳細資料**窗格中會移入資料。窗格會顯示產品實例的用量資料、產品詳細資料，及透過**警告器**標籤顯示其建議。


## 用量資訊
{: #product-insights_usage}
用量資訊顯示在**用量**標籤上。使用兩個下拉清單可選取要顯示的度量值（如果產品實例傳送多個度量值），以及要顯示的時段。

如果產品實例傳送多個度量值，請使用第一個下拉清單選取要顯示哪個度量值。從第二個下拉清單選取要顯示的時段。各區段的時段選項有最近 24 小時、1 週、1 個月、6 個月、1 年。

第一個區段顯示在所選時段之度量值的平均最大值、平均值、平均最小值以及總計。第二個區段顯示具有 X 軸期間的時段內之值的圖形，X 軸期間會根據選取的時段而改變。例如，最近 24 小時會顯示一小時的圖形點，而 1 週則顯示該週內每天的圖形點。最後的區段顯示所選圖形點的最大值、平均值和最小值。若要在圖形上查看另一個點的值，請將時間列拖曳到新的位置。

如果該時段沒有資料，會顯示一則訊息。例如，已停止的實例不會提供資料，因此針對它已停止的時段便不會顯示任何資料。其他時段可能有用量可顯示。請在下拉清單中變更時段以查看其他時段。

**詳細資料**標籤會顯示產品實例資訊，這可能包括下列項目：

* 產品名稱及版本
* 產品安裝的位置，包括主機名稱及目錄
* 實例在啟動時傳送資訊的最後時間
* 實例 ID，如果產品可以在單一目錄內有多個實例的話

![產品實例詳細資料](images/instancedetail.png "產品實例詳細資料") 

產品實例也會提供下列選用性資訊：

* 已安裝的 APAR 清單。 
* 作業系統及其版本，顯示於**環境**標籤。
![產品實例詳細資料 - 環境標籤](images/instancedetails-env.png "產品實例詳細資料 - 環境標籤")
* 元件或已安裝的特性，顯示於**元件**標籤。範例不會顯示**元件**標籤，因為 IBM Product XYZ 的實例未提供任何其他元件資訊。
![產品實例詳細資料 - 元件標籤](images/instancedetails-comps.png "產品實例詳細資料 - 元件標籤")
* 產品實例的唯一 ID，這是主機名稱、目錄及實例 ID 的組合。

 


## 搜尋 
{: #product-insights_search}
**產品實例**窗格提供基本的搜尋功能，可以過濾產品清單。在搜尋欄位中，鍵入您要用於搜尋的字串。搜尋只能針對產品實例資料進行（亦即，**詳細資料**標籤中的資訊）。



<!-- If your service doc doesn't have a troubleshooting topic or section, you can add the following to your About: -->
<!-- Add a heading and content for how to get help and support. Use this template for beta and GA services:  -->
## 取得 {{site.data.keyword.product-insights_short}} 的協助
{: #gettinghelp}

關於建立服務、取得已啟用 IBM 軟體產品的更新，和安裝與配置步驟的詳細資訊，可以在 [{{site.data.keyword.product-insights_full}} 技術社群](https://developer.ibm.com/product-insights/)找到。如果您在使用 {{site.data.keyword.product-insights_short}} 時有問題或疑問，請在社群的論壇區段檢視或張貼問題。這些問題會由開發及客戶計畫團隊處理。

您也可以使用 Stack Overflow 及 IBM DeveloperWorks dw Answers 論壇來檢視或張貼問題。若為服務及開始使用指示的相關問題，請使用 IBM developerWorks dW Answers。當您在這兩個論壇張貼問題時，請套用下列標記規則以便 Bluemix 開發團隊能輕鬆看到您的問題。

* 按一下以在 [Stack Overflow](http://stackoverflow.com/search?q=hybrid-connect+ibm-bluemix){:new_window} 上張貼、使用 "ibm-bluemix" 和 "productinsights" 標記您的問題。
* 按一下以在 [IBM developerWorks dW Answers](https://developer.ibm.com/answers/smartspace/productinsights/){:new_window} 上張貼、使用 "productinsights" 或 "hybridconnect" 標記您的問題。

如需使用論壇的相關資訊，請參閱[取得協助](https://www.{DomainName}/docs/support/index.html#getting-help)主題。
