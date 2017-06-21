---

copyright:
  years: 2016, 2017
lastupdated: "2017-04-07"

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}

# 與 Continuous Delivery 管線整合

將 {{site.data.keyword.DRA_short}} 新增至工具鏈並定義它所監視的原則之後，請將它與 {{site.data.keyword.deliverypipeline}} 整合。如需管線的相關資訊，請參閱[正式文件](/docs/services/ContinuousDelivery/pipeline_working.html)。

## 準備管線階段
{: #integrate_pipeline}

若要讓 Deployment Risk 分析您的專案，您必須在管線中定義編譯打包和正式作業的階段。您可以使用文字環境內容來定義階段（可在各階段配置功能表 ![「管線階段配置」圖示](images/pipeline-stage-configuration-icon.png) 的**環境內容**下找到文字環境內容）。

1. 在編譯打包階段，將 `LOGICAL_ENV_NAME` 內容設為 `STAGING`。 

2. 在正式作業階段，將 `LOGICAL_ENV_NAME` 內容設為 `PRODUCTION`。 

您也可以將下列內容新增至建置或部署應用程式的階段：

* `LOGICAL_APP_NAME`，可定義儀表板上的應用程式名稱。
* `BUILD_PREFIX`，可定義附加在階段的建置前面的文字。此文字也會顯示在儀表板上。 

## 新增測試工作
{: #configure_pipeline_jobs}

您可以使用以下兩種測試工作，將 {{site.data.keyword.DRA_short}} 整合至您的管線中：將結果上傳至 {{site.data.keyword.DRA_short}} 以進行分析的工作，以及對該分析採取行動的閘道。 

首先，將「進階測試者」工作新增至管線，以執行測試並上傳結果。 

**附註：**如果您要更新測試工作，以將結果上傳至 {{site.data.keyword.DRA_short}}，請先將其配置儲存在方便取得的地方，再繼續進行。然後，開啟其工作配置功能表，並跳到步驟 3。 

1. 在要新增上傳結果工作的階段，按一下**階段配置**圖示 ![「管線階段配置」圖示](images/pipeline-stage-configuration-icon.png)。按一下**配置階段**。
2. 建立測試工作，並鍵入其名稱。 
3. 針對工作類型，選取**進階測試者**。
4. 完成**測試指令**和**工作目錄**欄位，如同一般管線測試工作一樣。 
5. 完成其餘欄位，以上傳特定測試類型的測試結果。 

 1. 選擇度量值類型，需符合您要使用的 {{site.data.keyword.DRA_short}} 原則中定義的內容。
 2. 鍵入結果檔案位置。此位置相對於工作目錄。 

6. 如果您要上傳相同工作中第二個測試類型的結果，請完成前面加上*其他* 字首的欄位。
7. 按一下**儲存**，以回到管線。

**度量值類型**及**結果檔案位置**欄位的值必須符合正確的格式：

<table><thead>
<tr>
<th>度量值類型</th>
<th>支援的格式</th>
</tr>
</thead><tbody>
<tr>
<td>功能驗證測試</td>
<td>Mocha、xUnit</td>
</tr>
<tr>
<td>單元測試</td>
<td>Mocha、xUnit、Karma/Mocha</td>
</tr>
<tr>
<td>程式碼涵蓋面</td>
<td>Istanbul、Blanket.js</td>
</tr>
</tbody></table>

圖 1 顯示一個測試工作，其配置成執行單元測試、上傳 Mocha 格式的結果，以及上傳 Istanbul 格式的程式碼涵蓋面結果。

![DevOps Insights 上傳工作](images/insights_upload_job.png)
*圖 1. 將結果上傳至 DevOps Insights*

## 定義閘道
{: #configure_pipeline_gates}

{{site.data.keyword.DRA_short}} 閘道會檢查測試結果是否符合所定義的原則。如果不符合原則，依預設，{{site.data.keyword.DRA_short}} 閘道會失敗。您也可以將閘道配置為以諮詢角色運作，以允許管線即使失敗後仍可繼續進行。

在編譯打包部署工作之後，Deployment Risk 儀表板需要有閘道存在。如果您想要使用此儀表板，請確定在部署至編譯打包環境之後，且部署至正式作業環境之前，有閘道存在。

通常在管線中，閘道會放在建置升級前面。這些位置很適合用來根據原則檢查建置品質，以確保可以安心從某個環境升級至另一個環境。不過，您可以在管線中任何想要檢查特定準則的位置放置閘道。在您部署至編譯打包環境之前設置的閘道仍會強制執行原則，但不會出現在 Deployment Risk 儀表板上。

1. 在階段上，依序按一下**階段配置**圖示 ![「管線階段配置」圖示](images/pipeline-stage-configuration-icon.png) 及**配置階段**。
2. 按一下**新增工作**。針對工作類型，選取**測試**。
3. 針對測試者類型，選取 **{{site.data.keyword.DRA_short}} 閘道**。
4. 指定環境名稱。請確定此值符合[環境內容](#toolchain_pipeline_props)中所定義的值。
5. 輸入要在此閘道檢查的原則名稱。

 此名稱必須完全符合您定義的其中一個原則名稱。您只能指定在與工具鏈相同的 {{site.data.keyword.Bluemix_notm}} 組織中所定義的原則。

6. 選用項目：若要讓閘道以諮詢模式運作，請清除**此工作失敗時停止執行這個階段**勾選框。在諮詢模式中，{{site.data.keyword.DRA_short}} 會在閘道上完成相同的原則分析並產生報告，但是失敗時不會停止管線。
7. 按一下**儲存**，以回到管線。
8. 重複這些步驟，以設定所有 {{site.data.keyword.DRA_short}} 原則的閘道。

![Deployment Risk Mocha 工作](images/insights_gate_job.png)
*圖 2. DevOps Insights 閘道*

配置管線之後，請開始使用 {{site.data.keyword.DRA_short}}。 
