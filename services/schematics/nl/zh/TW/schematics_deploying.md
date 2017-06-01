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

# 將資源部署到您的環境
{: #deploying}

使用 {{site.data.keyword.bplong}} 時，您可以直接從原始碼部署最新的程式碼變更。當您部署環境時，您會部署配置檔中所定義的資源。然後，您可以從 {{site.data.keyword.bpshort}} 內管理環境的供應、編排及生命週期。
{:shortdesc}

## 使用 GUI 部署至您的環境
{: #gui}

如果您偏好使用圖形視圖來部署環境，可以使用 {{site.data.keyword.bpshort}} 儀表板。
{:shortdesc}


### 必要條件
{: #gui-prereq}

* 在來源控制儲存 Terraform 配置。配置可以用 HashiCorp 配置語言 (HCL) 或 JSON 語法撰寫。請參閱 <a href="https://www.terraform.io/docs/configuration/index.html">Terraform 配置文件 <img src="../../icons/launch-glyph.svg" alt="外部鏈結圖示"></a> 以取得 HCL 語法和如何撰寫配置的準則。請參閱 <a href="https://ibm-bluemix.github.io/tf-ibm-docs/">{{site.data.keyword.IBM_notm}} Cloud Provider <img src="../../icons/launch-glyph.svg" alt="外部鏈結圖示"></a> 以取得可用的資源。

儲存配置之後：

1. 在 **{{site.data.keyword.bpshort}}** 儀表板中，選取**環境**。

2. 按一下**建立環境**以新增環境，或選取您要部署之現有環境的列。

3. 按一下**方案**以預覽當您部署環境時，會供應哪些資源。當您執行方案時，{{site.data.keyword.bpshort}} 會從來源控制擷取您環境詳細資料中的變數，以及配置的最新版本。plan 輸出會顯示配置與根據 Terraform 狀態檔部署的內容相比較的結果。在方案套用到環境或是取消之前，您的環境會遭到鎖定，無法進行更多的變更。 

4. 在**最近的活動**區段中檢視日誌，來檢查 plan 輸出。plan 輸出顯示錯誤是否存在，以及服務計劃要建立、變更或破壞哪些資源。

5. 當您準備好啟動您的方案時，請按一下**套用**。您可以監視活動日誌，以確定方案已在最近一次的執行順利套用。 


## 使用 CLI 部署至您的環境
{: #cli}

您可以使用 {{site.data.keyword.Bluemix_notm}} CLI 的 {{site.data.keyword.bpshort}} 外掛程式來將更新部署至您的環境。
{:shortdesc}

### 必要條件
{: #cli-prereq}

* 在來源控制儲存 Terraform 配置。
* 如果您尚未完成，請從 [{{site.data.keyword.Bluemix_notm}} CLI 儲存庫](http://clis.ng.bluemix.net/ui/home.html)安裝適用於您的作業系統的 {{site.data.keyword.Bluemix_notm}} CLI。

登入 {{site.data.keyword.Bluemix_notm}} CLI 之後，請執行下列動作：

1. 執行下列指令，以安裝 {{site.data.keyword.bpshort}} CLI 外掛程式。
  
  ```
  bx plugin install schematics -r Bluemix
  ```
  {: codeblock}

  安裝成功的話，{{site.data.keyword.bpshort}} 外掛程式即會出現在 `bx plugin list` 下。 

2. 從配置建立環境。當您建立環境時，您會將服務指向來源控制，以便它可以擷取最新程式碼。 
  
  ```
  bx schematics environment create --file FILE_NAME
  ```
  {: codeblock}
  
  <table summary="environment create 指令的說明。">
  <caption>表 1. environment create 指令的說明。
  </caption>
  <thead>
  <th colspan="1">指令</th>
  <th colspan="1">作用</th>
  </thead>
  <tbody>
  <tr>
  <td>--file FILE_NAME</td>
  <td>儲存您環境相關詳細資料的 JSON 檔案。
  <p>
  <p>範例 JSON：
  <pre>{
      "description": "(Optional) Description of the environment",
      "frozen": false,
      "name": "Name of the environment",
      "sourceurl": "The GitHub URL that points to the Terraform configuration",
      "tags": ["(Optional) metadata_tag_1", "(Optional) metadata_tag_2"],
      "terraformversion": "0.9",
      "variablestore": [{
          "name": "(Optional) variable_1",
          "secure": false,
          "value": "Visible value"
      },
      {
          "name": "(Optional) variable_2_secret",
          "secure": true,
          "value": "Secured value"
      }]
  }</pre>
  </td>
  </tr>
  </tbody></table>
  
  記下傳回的 `ID` 值。`ID` 是指派給您的環境的唯一 ID，並且用於後續的指令。
  
3. 執行 `plan` 指令來預覽環境會如何變更。plan 指令會顯示哪些資源會變更、與已部署的資源相比會變更多少量，但是變更會等到您執行 `apply` 指令才會生效。
  
  ```
  bx schematics action plan --id ENVIRONMENT_ID
  ```
  {: codeblock}
  
  <table summary="plan 指令的說明。">
  <caption>表 2. plan 指令的說明。
  </caption>
  <thead>
  <th colspan="1">指令</th>
  <th colspan="1">作用</th>
  </thead>
  <tbody>
  <tr>
  <td>--id ENVIRONMENT_ID</td>
  <td>您要為其執行「執行方案」的特定環境。如需您需要擷取環境 ID 的值，可以執行 <code>bx schematics list</code>。
  </td>
  </tbody></table>
  
  `activity_id` 已指派給方案，並記錄在活動日誌中。 

4. 擷取活動日誌以檢視 Terraform plan 輸出。

  ```
  bx schematics activity log --id ACTIVITY_ID
  ```
  {: codeblock}

  <table summary="log 指令的說明。">
  <caption>表 3. log 指令的說明。
  </caption>
  <thead>
  <th colspan="1">指令</th>
  <th colspan="1">作用</th>
  </thead>
  <tbody>
  <tr>
  <td>--id ACTIVITY_ID</td>
  <td>您要檢視其日誌的特定活動。如需您需要擷取活動 ID 的值，可以執行 <code>bx schematics activity list --id ENVIRONMENT_ID</code>。
  </td>
  </tbody></table>
  
5. 執行 `apply` 指令將資源部署至您的環境。
  
  ```
  bx schematics action apply --id ENVIRONMENT_ID
  ```
  {: codeblock}
  
  <table summary="apply 指令的說明。">
  <caption>表 4. apply 指令的說明。
  </caption>
  <thead>
  <th colspan="1">指令</th>
  <th colspan="1">作用</th>
  </thead>
  <tbody>
  <tr>
  <td>--id ENVIRONMENT_ID</td>
  <td>您要部署更新到其中的特定環境。如需您需要擷取環境 ID 的值，可以執行 <code>bx schematics list</code>。
  </td>
  </tbody></table>
  
6. 監視 apply 輸出，以確保部署成功。 

  ```
  bx schematics activity log --id ACTIVITY_ID
  ```
  {: codeblock}

  順利完成部署會在輸出的結束處傳回下列這一行。
  
  ```
  Apply complete! Resources: N added, N changed, N destroyed.
  ```
  {: screen}
  
## 使用 API 部署至您的環境
{: #api}

您可以使用 {{site.data.keyword.bpshort}} API 透過程式設計方式來部署環境。
{:shortdesc}

對 <a href="https://us-south.schematics.bluemix.net/swagger-api/">{{site.data.keyword.bpshort}} API <img src="../../icons/launch-glyph.svg" alt="外部鏈結圖示"></a> 的呼叫會指向下列基礎端點：

```
https://us-south.schematics.bluemix.net
```
{: codeblock}

### 必要條件
{: #api-prereq}

* 在來源控制儲存 Terraform 配置。

請完成下列步驟以將資源部署至您的環境：

1. 產生 IAM OAuth 記號，以便用於您的鑑別標頭。指令會輸出 UAA 記號和 IAM 記號。
  
  ```
  bx iam oauth-tokens
  ```
  {: codeblock}
  
  輸出範例：
  ```
  IAM token:  Bearer eyJraWQ...
  ```
  {: screen}
    
  `Bearer eyJraWQ...` 輸出是 IAM 記號的已截斷範例。請在您的 API 呼叫的標頭中包含完整記號。
  
2. 執行 `POST v1/environments` 呼叫來建立環境。

  ```
  curl -X POST \
    https://us-south.schematics.bluemix.net/v1/environments \
    -H 'accept: text/plain' \
    -H 'authorization: bearer <IAM_token>' \
    -H 'content-type: application/json' \
    -d '{
    "description": "(Optional) Description of the environment",
    "frozen": false,
    "name": "Name of the environment",
    "sourceurl": "The GitHub URL that points to the Terraform configuration",
    "tags": [
      "(Optional) metadata_tag_1",
      "(Optional) metadata_tag_2"
    ],
    "terraformversion": "0.9",
    "variablestore": [{
        "name": "(Optional) variable_1",
        "secure": false,
        "value": "Visible value"
    },
    {
        "name": "(Optional) variable_2_secret",
        "secure": true,
        "value": "Secured value"
    }]
  }'
  ```
  {: codeblock}
    
  成功的回應會傳回下列輸出。
  ```
  {
    "id": "Environment ID",
    "name": "Environment name",
    "description": "Description of the environment",
    "account": "{{site.data.keyword.Bluemix_notm}} account GUID",
    "owner": "The IBMid of the user who created the environment",
    "creationtime": "YYYY-MM-DDTHH:MM:SSZ",
    "status": "CREATED",
    "frozen": false,
    "sourceurl": "The GitHub URL that points to the configuration",
    "statefile": "The reference to the Terraform state file",
    "terraformversion": "0.9",
    "tags": [
      "metadata_tag_1",
      "metadata_tag_2"
    ],
    "variablestore": [
      {
        "name": "(Optional) variable_1",
        "value": "Visible value"
      }
    ]
  }
  ```
  {: screen}
    
  記下傳回的 `id` 值。`id` 是指派給您的環境的唯一 ID，並且用於後續的呼叫。
  
3. 執行 `POST v1/environments/<environment_ID>/plan` 呼叫來預覽當您套用配置時，哪些資源將部署至您的環境。方案會在儲存庫的主節點分支擷取環境配置。
  
  ```
  curl -X POST \
    https://us-south.schematics.bluemix.net/v1/environments/<environment_ID>/plan \
    -H 'accept: application/json' \
    -H 'authorization: bearer <IAM_token>' \
    -H 'content-type: application/json'
  ```
  {: codeblock}
  
  成功的回應會傳回 `activityid`。需要活動 ID 值以檢視日誌，例如 plan 並 apply 輸出。
  ```
  {
    "activityid": "<activity_ID>"
  }
  ```
  {: screen}

4. 執行 `GET v1/environments/<environment_ID>/activities/<activity_ID>/log` 呼叫來檢視 plan 輸出。

  ```
  curl -X GET \
    https://us-south.schematics.bluemix.net/v1/environments/<environment_ID>/activities/<activity_ID>/log \
    -H 'accept: text/html' \
    -H 'authorization: bearer <IAM_token>'
  ```
  {: codeblock}

5. 執行 `PUT v1/environments/<environment_ID>/apply/` 呼叫來部署您的環境。
  
  ```
  curl -X PUT \
    https://us-south.schematics.bluemix.net/v1/environments/<environment_ID>/apply \
    -H 'accept: application/json' \
    -H 'authorization: bearer <IAM_token>' \
    -H 'content-type: application/json'
  ```
  {: codeblock}
  
6. 執行 `GET v1/environments/<environment_ID>/activities/<activity_ID>/log` 呼叫來檢視 apply 輸出，以便監視部署。

  ```
  curl -X GET \
    https://us-south.schematics.bluemix.net/v1/environments/<environment_ID>/activities/<activity_ID>/log \
    -H 'accept: text/html' \
    -H 'authorization: bearer <IAM_token>'
  ```
  {: codeblock}

  順利完成部署會在輸出的結束處傳回下列這一行。
  
  ```
  Apply complete! Resources: N added, N changed, N destroyed.
  ```
  {: screen}
