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

# 管理環境中的資源
{: #managing}

{{site.data.keyword.bplong}} 能簡化環境的管理。您可以修改已部署的資源，並隨需應變反覆地重新部署變更。

{:shortdesc}

對您環境的變更可以使用輕量型處理程序進行部署。當您想要變更已配置的資源時，您會以宣告式語法撰寫配置變更的程式碼，這表示您只有指出您想要的結果。利用 {{site.data.keyword.bpshort}}，您可以在部署之前先預覽變更。


## 使用 GUI 更新資源
{: #gui}

如果您偏好使用圖形視圖來管理環境中的資源，可以使用 {{site.data.keyword.bpshort}} 儀表板。
{:shortdesc}

您在 GitHub 中發佈配置的程式碼變更，或在 GUI 修改變數之後，請完成下列步驟以將更新部署至您的環境：

1. 在 **{{site.data.keyword.bpshort}}** 儀表板中，選取**環境**。

2. 按一下您要更新的特定環境的那一列。

3. 按一下**方案**，然後檢查方案日誌是否有錯誤。環境會被鎖定，直到您或 {{site.data.keyword.Bluemix_notm}} 帳戶中的其他合作人員套用方案或取消它。 

4. 按一下**套用**以部署更新。 


## 使用 CLI 更新資源
{: #cli}

您可以透過程式設計方式，使用 {{site.data.keyword.bpshort}} CLI 更新您環境中的資源。
{:shortdesc}

您在 GitHub 中發佈配置的程式碼變更之後，請完成下列步驟以將更新部署至您的環境：

1. 執行 `plan` 指令。{{site.data.keyword.bpshort}} CLI 會從 GitHub 取回更新的環境配置，並輸出您的資源與現行部署不同之處的預覽。

  ```
  bx schematics action plan --id ENVIRONMENT_ID
  ```
  {: codeblock}

2. 在活動日誌中檢視 plan 輸出。

  ```
  bx schematics activity log --id ACTIVITY_ID
  ```
  {: codeblock}

3. 執行 `apply` 指令來部署您的方案。 

  ```
  bx schematics action apply --id ENVIRONMENT_ID
  ```
  {: codeblock}


## 使用 API 更新資源
{: #api}

您可以透過程式設計方式，使用 {{site.data.keyword.bpshort}} API 管理您環境中的資源。
{:shortdesc}

您在 GitHub 中發佈配置的程式碼變更之後，請完成下列步驟以將更新部署至您的環境：

1. 執行 `POST v1/environments/<environment_ID>/plan` 呼叫。{{site.data.keyword.bpshort}} API 會從 GitHub 取回更新的環境配置，並與 Terraform 狀態檔比較，以顯示您的資源與現行部署不同之處。

  ```
  curl -X POST \
    https://us-south.schematics.bluemix.net/v1/environments/<environment_ID>/plan \
    -H 'accept: application/json' \
    -H 'authorization: bearer <IAM_token>' \
    -H 'content-type: application/json'
  ```
  {: codeblock}

  範例回應：
  ```
  {
    "activityid": "<activity_ID>"
  }
  ```
  {: screen}

2. 在活動日誌中檢視 plan 輸出。

  ```
  curl -X GET \
    https://us-south.schematics.bluemix.net/v1/environments/<environment_ID>/activities/<activity_ID>/log \
    -H 'accept: text/html' \
    -H 'authorization: bearer <IAM_token>'
  ```
  {: codeblock}

3. 執行 `PUT /v1/environments/<environment_ID>/apply` 呼叫來部署您的方案。 

  ```
  curl -X PUT \
    https://us-south.schematics.bluemix.net/v1/environments/<environment_ID>/apply \
    -H 'accept: application/json' \
    -H 'authorization: bearer <IAM_token>' \
    -H 'content-type: application/json' \
  ```
  {: codeblock}


## 審核環境變更
{: #auditing}

配置可以在來源控制儲存庫的版本歷程中審核。為了監視對您環境的部署，或檢視先前部署的日誌，{{site.data.keyword.bpshort}} 提供下列選項，以檢視審核日誌。

### 從 {{site.data.keyword.bpshort}} 儀表板
{: #auditing-gui}

1. 選取環境的列，以存取環境詳細資料頁面。

2. 監視**最近的活動**區段。您也可以檢視先前方案和部署的歷程日誌。

### 使用 {{site.data.keyword.bpshort}} CLI
{: #auditing-cli}

1. 擷取您的環境 ID。

  ```
  bx schematics environment list
  ```
  {: codeblock}

2. 擷取環境的活動 ID。活動 ID 會指派給 plan、apply、destroy 和 delete 動作。下列指令會列出針對您的環境所執行的所有活動。

  ```
  bx schematics activity list --id ENVIRONMENT_ID
  ```
  {: codeblock}

3. 擷取特定活動的相關資料，例如誰變更了環境、何時變更。

  ```
  bx schematics activity show --id ACTIVITY_ID
  ```
  {: codeblock}

4. 選用項目：若要檢視詳細日誌，例如 plan 或 apply 輸出，請執行 `log` 指令。 

  ```
  bx schematics activity log --id ACTIVITY_ID
  ```
  {: codeblock}

### 使用 {{site.data.keyword.bpshort}} API
{: #auditing-api}

1. 擷取您的環境 ID。

  ```
  curl -X GET \
    https://us-south.schematics.bluemix.net/v1/environments \
    -H 'accept: application/json' \
    -H 'authorization: bearer <IAM_token>'
  ```
  {: codeblock}
  
  回應內文包含您 {{site.data.keyword.Bluemix_notm}} 帳戶中的所有環境。找到您要審核之特定環境的 `id` 值。

2. 擷取針對環境執行之動作的活動 ID。

  ```
  curl -X GET \
    https://us-south.schematics.bluemix.net/v1/environments/<environment_ID>/activities \
    -H 'accept: application/json' \
    -H 'authorization: bearer <IAM_token>'
  ```
  {: codeblock}

3. 取得環境的特定活動。 

  ```
  curl -X GET \
    https://us-south.schematics.bluemix.net/v1/environments/<environment_ID>/activities/<activity_ID> \
    -H 'accept: application/json' \
    -H 'authorization: bearer <IAM_token>'
  ```
  {: codeblock}

4. 檢查 Terraform 輸出的詳細日誌。

  ```
  curl -X GET \
    https://us-south.schematics.bluemix.net/v1/environments/<environment_ID>/activities/<activity_ID>/log \
    -H 'accept: text/html' \
    -H 'authorization: bearer <IAM_token>'
  ```
  {: codeblock}
