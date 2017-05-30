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

# 開始使用 {{site.data.keyword.bpfull_notm}}（測試版）
{: #gettingstarted}

{{site.data.keyword.bplong}} 是一項自動化工具，您可以用來以單一的單位定義及部署雲端基礎架構，並在不限數目的環境中重複使用那些雲端資源定義。
{:shortdesc}

{{site.data.keyword.bpshort}} 使用 HashiCorp 的 Terraform 編撰基礎架構。基礎架構的元件會分解為個別資源，這些資源可能是從實體硬體到使用者帳戶的任何東西。藉由將高階和低階資源抽象化，您可以像軟體一樣地將基礎架構視為程式碼。 

當您使用 {{site.data.keyword.bpshort}} 時，您會以宣告式語法撰寫環境的配置。您會陳述希望的環境外觀，例如有 10 台 {{site.data.keyword.virtualmachinesshort}} 在正式作業。服務會比較您的配置與 Terraform 先前建立的內容，並且視需要新增或移除資源。

{{site.data.keyword.bpshort}} 是協同的 DevOps 工具，它為基礎架構提供單一的事實來源。您可以在來源控制中儲存環境配置，讓您的團隊能夠進行程式碼複查、將基礎架構版本化、透過確定歷程追蹤變更，以及更輕鬆地回復變更。

{{site.data.keyword.bpshort}} 自動可供您 {{site.data.keyword.Bluemix_notm}} 帳戶中的所有使用者使用。


## 建立配置
{: #configuration}

當您建立配置時，您會將構成環境的雲端資源編碼。
{:shortdesc}


如果您要在 {{site.data.keyword.bpshort}} 嘗試搭配使用範例配置，請完成下列步驟。在範例中，您可以佈建 SSH 金鑰，以便在 {{site.data.keyword.BluSoftlayer}} 中使用。 

**附註：**範例配置需要 {{site.data.keyword.BluSoftlayer}} 帳戶。如果您有現有的帳戶，請參閱[鏈結 {{site.data.keyword.Bluemix_notm}} 與 SoftLayer 帳戶文件](../../pricing/linking_accounts.html#unifyingaccounts)，否則可以[註冊帳戶](https://console.ng.bluemix.net/docs/pricing/index.html#pay-accounts)。

1. 在本端產生 SSH 金鑰組。
  ```
  ssh-keygen -t rsa
  ```
  {:codeblock}

2. 分出 <a href="https://github.com/IBM-Bluemix/tf-bluemix-ssh-key" target="_blank">GitHub <img src="../../icons/launch-glyph.svg" alt="外部鏈結圖示"></a> 中的範例配置。 

  下列範例顯示範例配置中的不同類型區塊。您可以在 GitHub 儲存庫的 `main.tf` 檔中看到完整配置。
  
  * provider 區塊會設定 {{site.data.keyword.IBM_notm}} Cloud 提供者及登入認證。

    ```
    provider "ibmcloud" {
      ibmid                    = "${var.ibmid}"
      ibmid_password           = "${var.ibmidpw}"
      softlayer_account_number = "${var.slaccountnum}"
    }
    ```
    {:screen}
  
  * resource 區塊會定義基礎架構的元件，在此範例中為 SSH 金鑰。
  
    ```
    resource "ibmcloud_infra_ssh_key" "ssh_key" {
      label = "${var.key_label}"
      notes = "${var.key_note}"
      public_key = "${var.public_key}"
    }
    ```
    {:screen}
  
  * variable 區塊會定義您的變數，您可以在 {{site.data.keyword.bpshort}} GUI 中為這個範例輸入。
  
    ```
    variable ibmid {
      type = "string"
      description = "Your IBM-ID."
    }
    ```
    {:screen}
  
  * output 區塊會定義在使用配置建立您的環境且建立資源（SSH 金鑰）之後，Terraform 輸出中顯示的內容。
  
    ```
    output "ssh_key_id" {
      value = "${ibmcloud_infra_ssh_key.ssh_key.id}"
    }
    ```
    {:screen}
  
現在，您可以從配置建立環境。 

{:codeblock}

## 建立環境
{: #environment}

當您建立環境時，您會將服務指至配置，以便服務能擷取您最新的程式碼變更。
{:shortdesc}

使用範例配置，完成下列步驟以建立環境。

1. 在功能表中，選取**服務**，然後選取 **{{site.data.keyword.bpshort}}**。您會移至 {{site.data.keyword.bpshort}} 儀表板。

2. 在左側導覽功能表中，選取**環境**，然後按一下**建立環境**，以說明配置的相關內容。建立環境會定義 {{site.data.keyword.bpshort}} 佈建及更新雲端資源的方式，但還不會建立資源。

3. 輸入環境的相關詳細資料。範例配置需要下表中所列出的值。

  <table summary="使用範例配置作為環境來源時所需要的值。">
  <caption>表 1. 使用範例配置作為環境來源時所需要的值。
  </caption>
  <thead>
  <th colspan="1">設定</th>
  <th colspan="1">說明</th>
  </thead>
  <tbody>
  <tr>
  <td>來源控制 URL</td>
  <td>輸入您分出範例配置之處的 GitHub URL。</td>
  </tr>
  <tr>
  <td>名稱</td>
  <td>請輸入唯一名稱，以指派給您的環境。</td>
  </tr>
  <td>Terraform 版本</td>
  <td>輸入 Terraform 的版本，以確定針對您的環境執行相容的 Terraform 版本。對於範例配置，請使用 <code>0.9.1</code> 版。</td>
  </tr>
  <tr>
  <td>變數</td>
  <td>您可以在服務中定義變數，或置換在 <code>.tf</code> 檔案中的環境變數。按一下鎖定圖示時可以遮罩機密的變數。遮罩變數可避免其他使用者在環境詳細資料頁面中看到隱藏的值。
  <p>
  <p>請新增下列變數和值來使用範例配置：
  <ul>
  <li><code>ibmid</code> - 輸入您的完整 {{site.data.keyword.ibmid}} 作為值。</li>
  <li><code>ibmidpw</code> - 輸入與您的 {{site.data.keyword.ibmid}} 相關聯的密碼，然後按一下鎖定圖示來遮罩值。</li>
  <li><code>slaccountnum</code> - 輸入您的 {{site.data.keyword.BluSoftlayer}} 帳號。
   <li><code>datacenter</code> - 輸入您要將 SSH 金鑰資源部署至其中的資料中心。請參閱 <a href="https://github.com/IBM-Bluemix/tf-bluemix-ssh-key/blob/master/README.md" target="_blank">readme 檔 <img src="../../icons/launch-glyph.svg" alt="外部鏈結圖示"></a> 以取得可用值的完整清單。</li> 
   <li><code>public_key</code> - 輸入公用 SSH 金鑰。若要將公開金鑰複製到剪貼簿，您可以執行 <code>pbcopy < ~/.ssh/id_rsa.pub</code> 指令。
   <li><code>key_label</code> - 以唯一名稱來識別金鑰。
   <li><code>key_note</code> - 選用項目：新增關於 SSH 金鑰的說明文字。</ul></td>
   </tr></tbody></table>

4. 填寫完環境的詳細資料時，請按一下**建立**。畫面上會顯示新建立的環境。 
5. 若要查看在您部署環境時會佈建或移除哪些資源的預覽，請按一下**方案**。 
6. 檢視方案日誌，以檢查輸出是否有任何錯誤。 
7. 當您準備好部署您的環境時，請按一下**套用**。您可以監視套用日誌，以查看是否已順利部署金鑰。順利完成部署會在輸出的結束處顯示下列這一行：

  ```
  Apply complete! Resources: 1 added, 0 changed, 0 destroyed.
  ```
  {: screen}

  您也可以在 [{{site.data.keyword.slportal}}](https://control.bluemix.net/devices/sshkeys) 中檢視 SSH 金鑰。
8. 選用項目：若要移除 SSH 金鑰並從 {{site.data.keyword.Bluemix_notm}} 中移除環境，請從動作功能表選取**破壞資源**。

### 下一步為何？
{: #next}

* 若要進一步瞭解如何以程式化的方式部署您的環境，[請查看 CLI 或 API](schematics_deploying.html)。
* 若要從頭開始建立您自己的配置，請參閱<a href="https://ibm-bluemix.github.io/tf-ibm-docs/">{{site.data.keyword.IBM_notm}} Cloud 資源 <img src="../../icons/launch-glyph.svg" alt="外部鏈結圖示"></a>。{{site.data.keyword.IBM_notm}} Cloud 資源提供為 Terraform 外掛程式提供者。
