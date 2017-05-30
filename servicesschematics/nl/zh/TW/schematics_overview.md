---

copyright:
  years: 2017
lastupdated: "2017-05-16"

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}

# 關於
{: #about}

{{site.data.keyword.bplong}} 可用來建立基礎架構構成要素。您可以將 {{site.data.keyword.IBM_notm}} Cloud 服務放在一起，以建立可部署且可重複使用的基礎架構。
{:shortdesc}

{{site.data.keyword.bpshort}} 使用 Terraform 來簡化基礎架構管理。例如，如果您想要啟動多份的服務，而它們使用應用程式伺服器的叢集、負載平衡器和資料庫伺服器，您可能會撰寫 Bash Script 來執行指令啟動這些元件。但是，若是有配置，以及取用該配置並將它變成真實資源的執行器，會更輕鬆、更快速且更井然有序。使用 Terraform，您可以同時啟動眾多的資源（作為一個群體群組），並且在其中對映相依關係。 

## 使用 {{site.data.keyword.bpshort}} 的原因
{: #reasons}

在下列情境下，您可能會想要使用編碼的基礎架構：
{:shortdesc}

| 情境     | 原因    |
| :------------- | :------------- |
| 您想要重建和重複使用基礎架構。 | 您可以使用 {{site.data.keyword.bpshort}} 來管理基礎架構。使用 {{site.data.keyword.bpshort}}，您可以透過程式化方式佈建、修改和破壞資源。當您編碼和配置資源時，可以建置一個資源庫，一再地加以重複使用以獲得相同的結果。|
| 您想要環境設定具有透通性。 | {{site.data.keyword.bpshort}} 會使用來源控制中的配置，它們可促成協同作業、檢閱，並提供您審核追蹤以便查看進行變更的方法與時間。如果您需要回復至先前的配置，您也可以檢視變更。 |
| 您想要簡化環境變更的執行。 | {{site.data.keyword.bpshort}} 遵循宣告模型，此模型會提供單一的事實來源。當您計劃變更環境時，您會陳述想要的結果。 |
| 您已使用配置管理 (CM) 工具，但是想要更自動的方法來設定環境。 | {{site.data.keyword.bpshort}} 可以搭配 CM 工具一起工作。使用 {{site.data.keyword.bpshort}} 部署的環境是高階的抽象概念，可以建立基礎架構資源。然後，您可以使用 CM 工具，在 {{site.data.keyword.bpshort}} 佈建的資源上安裝與配置軟體。  
  
## 運作方式
{: #how}

您可以使用 {{site.data.keyword.bpshort}} 將資源部署至您的環境。
{:shortdesc}

{{site.data.keyword.bpshort}} 使用 Terraform 作為基礎工具，來啟用基礎架構即程式碼 (infrastructure as code)，以便您可以將 {{site.data.keyword.IBM}} Cloud 資源定義為程式碼。雲端資源可以是基礎架構的不同元件，例如裸機伺服器、虛擬伺服器、負載平衡器、軟體定義的網路元件等。 

### 定義資源用的配置
{: #how-define}

配置，或 Terraform 配置，是定義哪些資源構成您的基礎架構的檔案。配置是可部署的架構，可以套用至一個以上的環境。下圖顯示構成配置的內容，以及各個部分如何一起運作，以在 {{site.data.keyword.bpshort}} 建立可部署的環境。


![{{site.data.keyword.bpshort}} 架構圖](/images/anatomy_of_a_schematic.png)

圖 1. {{site.data.keyword.bpshort}} 架構圖

### 啟用協同作業用的來源控制
{: #how-collaborate}

配置儲存在 GitHub，以便團隊可以檢閱程式碼並分工合作。使用 GitHub，您會有內建的審核追蹤，並且可以檢視對配置所做變更的完整確定歷程。您可以使用 readme 檔儲存使用資訊，多個團隊才能共用和使用該配置。

### 佈建資源用的 {{site.data.keyword.bpshort}} 環境
{: #how-provision}

您可以使用 {{site.data.keyword.bpshort}} 來掃描 GitHub 中的程式碼，並將資源部署至環境。環境可以共用一般的配置。例如，您可以啟動類似正式作業的暫存 QA 環境，然後在完成測試時關閉它。您可以建置一個一般環境配置庫，{{site.data.keyword.Bluemix_notm}} 帳戶中的所有使用者都可以標記和搜尋它。
