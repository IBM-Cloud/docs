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

# 破壞暫存環境中的資源
{: #destroying}

您可以使用 {{site.data.keyword.bplong}} 來破壞資源。當您破壞資源時，會關閉環境及所有相關聯的資源。  
{:shortdesc}

**警告**：破壞資源時，無法反轉所執行的動作。破壞資源不建議用於正式作業環境，但可能適合暫存環境，例如測試或 QA。

在破壞資源之前，請考量下列準則： 
* 確認未將資料流量導向您的資源。
* 確認您可能需要的任何資料都已備份。 


## 使用 GUI 破壞資源
{: #gui}

您可以使用 {{site.data.keyword.bpshort}} 儀表板來啟動及關閉暫存環境。
{:shortdesc}

1. 在 **{{site.data.keyword.bpshort}}** 儀表板中，選取**環境**標籤。

2. 按一下您要移除之特定環境的那一列。 

3. 在選項功能表中，選取**破壞資源**或**刪除環境**。刪除及破壞動作都是不可逆的。若要決定選取哪一個選項，請考量您是否有作用中的資源。
  * 如果要停止並移除作用中的資源，請選取**破壞資源**。建議您在破壞之前先執行方案，以確認是否可以移除與環境相關聯的資源。
  * 如果要從 {{site.data.keyword.bpshort}} 服務移除環境配置，請選取**刪除環境**。這個選項通常用於環境未部署，且沒有作用中資源的情況下。如果您選取這個選項，且有作用中的資源，則無法再使用 {{site.data.keyword.bpshort}} 服務來追蹤或部署變更至您的環境。作用中的資源需要個別管理（從其服務儀表板）。
  
  請遵循畫面上的提示，確認您的選擇。 


## 使用 CLI 破壞資源
{: #cli}

您可以使用 {{site.data.keyword.bpshort}} CLI 來啟動及關閉暫存環境。
{:shortdesc}

1. 執行 `destroy` 指令，關閉您的環境及資源。

  ```
  bx schematics action destroy --id ENVIRONMENT_ID
  ```
  {: codeblock}
  
2. 選用項目：如果您要從服務移除配置，請執行 `delete` 指令。

  ```
  bx schematics environment delete --id ENVIRONMENT_ID
  ```
  {: codeblock}


## 使用 API 破壞資源
{: #api}

您可以使用 {{site.data.keyword.bpshort}} API 來啟動及關閉暫存環境。
{:shortdesc}

1. 執行 `PUT v1/environments/<environment_ID>/destroy` 呼叫，以破壞資源。

  ```
  curl -X PUT \
    https://us-south.schematics.bluemix.net/v1/environments/<environment_ID>/destroy \
    -H 'accept: application/json' \
    -H 'authorization: bearer <IAM_token>' \
    -H 'content-type: application/json'
  ```
  {: codeblock}

2. 選用項目：如果您要從 {{site.data.keyword.bpshort}} 服務移除配置，請執行 `DELETE v1/environments/<environment_ID>` 呼叫。

  ```
  curl -X DELETE \
    https://us-south.schematics.bluemix.net/v1/environments/<environment_ID> \
    -H 'accept: text/plain' \
    -H 'authorization: bearer <IAM_token>'
  ```
  {: codeblock}
