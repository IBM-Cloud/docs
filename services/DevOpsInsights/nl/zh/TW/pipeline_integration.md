---

copyright:
  years: 2016
lastupdated: "2016-11-11"

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}

# 整合 {{site.data.keyword.DRA_short}} 與 {{site.data.keyword.deliverypipeline}}
{: #toolchain_configure_pipeline}

將 {{site.data.keyword.DRA_full}} 新增至工具鏈並定義它所監視的原則之後，您必須整合 {{site.data.keyword.DRA_short}} 與管線。
{:shortdesc}

<!--##Configuring the {{site.data.keyword.deliverypipeline}}

{: #toolchain_integration}
To use {{site.data.keyword.DRA_short}}, add it to any toolchain that uses the {{site.data.keyword.deliverypipeline}}.

1. In {{site.data.keyword.Bluemix_notm}}, on the **Toolchains** tab, open a toolchain.

2. On the toolchain's Overview page, click the add (+) button.

3. In the Tool Integrations section, select **{{site.data.keyword.DRA_short}}**.

4. Click **Create Integration**.

5. In your toolchain, click the {{site.data.keyword.deliverypipeline}} tile. You can configure {{site.data.keyword.DRA_short}} in any number of pipelines.-->

## 準備 {{site.data.keyword.DRA_short}} 的管線階段
{: #toolchain_pipeline_props}

您必須在每一個包含建置或部署工作的管線階段中建立數個環境內容：

1. 依序按一下**階段配置**及**配置階段**。

2. 按一下**環境內容**。

3. 新增下列三個文字內容，然後儲存階段的變更：

<table><thead>
<tr>
<th>環境內容</th>
<th>說明</th>
</tr>
</thead><tbody>
<tr>
<td><code>LOGICAL_APP_NAME</code></td>
<td>應用程式出現在 {{site.data.keyword.DRA_short}} 儀表板上的名稱。</td>
</tr>
<tr>
<td><code>LOGICAL_ENV_NAME</code></td>
<td>應用程式在其中執行的環境名稱。此內容是用來分類 {{site.data.keyword.DRA_short}} 儀表板中的應用程式。</td>
</tr>
<tr>
<td><code>BUILD_PREFIX</code></td>
<td>新增至 {{site.data.keyword.DRA_short}} 儀表板上所顯示的建置的字首。</td>
</tr>
</tbody></table>


## 更新 {{site.data.keyword.DRA_short}} 的測試工作
{: #toolchain_pipeline_upload}

若要開始使用，請透過測試工作來擷取安裝資訊。

1. 在包含測試工作的階段上，按一下**階段配置**圖示 ![「管線階段配置」圖示](images/pipeline-stage-configuration-icon.png)。按一下**配置階段**。
2. 建立工作。針對工作類型，選取**測試**。
3. 選取使用「簡式測試者」類型的測試工作，然後將**測試指令**及**工作目錄**欄位中的資訊複製到編輯器中。您稍後需要該資訊。
4. 從相同的「簡式測試工作」中，選取**進階測試者**來變更測試者類型。
5. 在**測試指令**欄位中，貼上您從「簡式測試工作」的**測試指令**欄位中所複製的指令。
6. 在**工作目錄**欄位中，貼上您從「簡式測試工作」的**工作目錄**欄位中所複製的路徑。
7. 完成其餘的欄位，以上傳特定測試類型的測試結果。如果您要上傳相同工作中第二個測試類型的結果，也請完成前面加上*其他* 字首的欄位。

 * 度量值類型
 * 格式
 * 結果檔案位置
8. 按一下**儲存**，以回到管線。

**度量值類型**及**結果檔案位置**欄位的值必須符合正確的格式：

<table><thead>
<tr>
<th>度量值類型</th>
<th>支援的格式</th>
</tr>
</thead><tbody>
<tr>
<td>功能驗證測試</td>
<td>Mocha、JUnit</td>
</tr>
<tr>
<td>單元測試</td>
<td>Mocha、JUnit、Karma/Mocha</td>
</tr>
<tr>
<td>程式碼涵蓋面</td>
<td>Istanbul、Blanket.js</td>
</tr>
</tbody></table>

*圖 1* 顯示一個測試工作，其配置成執行單元測試、上傳 Mocha 格式的結果，以及上傳 Istanbul 格式的程式碼涵蓋面結果。

![部署風險分析上傳工作](images/DRA_upload_job.png) *圖 1. 將結果上傳至 DevOps Analytics*

## 在管線中定義 {{site.data.keyword.DRA_short}} 閘道
{: #toolchain_pipeline_gates}

{{site.data.keyword.DRA_short}} 閘道會檢查測試結果是否符合所定義的原則。如果不符合原則，則 {{site.data.keyword.DRA_short}} 閘道會失敗。閘道通常放置在管線的每一個階段結尾。此位置最適合用來根據原則檢查建置品質，以確保從某個環境安心地升級至另一個環境。不過，您可以在管線中任何想要檢查特定準則的位置放置閘道。

1. 在階段上，依序按一下**階段配置**圖示 ![「管線階段配置」圖示](images/pipeline-stage-configuration-icon.png) 及**配置階段**。
2. 按一下**新增工作**。針對工作類型，選取**測試**。
3. 輸入新工作的名稱，例如 *Gate (Unit Test)*。
4. 針對測試者類型，選取 **{{site.data.keyword.DRA_short}} 閘道**。
5. 指定環境名稱。請確定此值符合[環境內容](#toolchain_pipeline_props)中所定義的值。
6. 定義要在此閘道上檢查的原則名稱。

 此名稱必須完全符合您定義的其中一個原則名稱。您只能指定在與工具鏈相同的 {{site.data.keyword.Bluemix_notm}} 組織中所定義的原則。

7. 選用項目：若要在諮詢模式中製作閘道功能，請清除**此工作失敗時停止執行這個階段**勾選框。在諮詢模式中，{{site.data.keyword.DRA_short}} 會在閘道上完成相同的原則分析，並產生報告，但是，失敗時不會停止管線。
8. 按一下**儲存**，以回到管線。
9. 重複這些步驟，以設定所有 {{site.data.keyword.DRA_short}} 原則的閘道。

![部署風險分析 Mocha 工作](images/DRA_gate_job.png) *圖 2. DevOps Analytics 閘道*

配置管線之後，請開始使用 {{site.data.keyword.DRA_short}}。如需指示，請參閱[執行 Delivery Pipeline](./pipeline_decision_reports.html#toolchain_reports)。
