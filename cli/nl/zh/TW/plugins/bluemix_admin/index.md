---

 

copyright:

  years: 2015, 2016

 

---

{:shortdesc: .shortdesc}
{:codeblock: .codeblock}
{:screen: .screen}
{:new_window: target="_blank"}

# {{site.data.keyword.Bluemix_notm}} 管理 CLI
{: #bluemixadmincli}

*前次更新：2016 年 3 月 3 日*

您可以使用 Cloud Foundry 指令行介面與 {{site.data.keyword.Bluemix_notm}} 管理 CLI 外掛程式搭配，來管理「{{site.data.keyword.Bluemix_notm}} 本端」或「{{site.data.keyword.Bluemix_notm}} 專用」環境的使用者。例如，您可以從 LDAP 登錄新增使用者。如果您要尋找管理「{{site.data.keyword.Bluemix_notm}} 公用」帳戶的相關資訊，請參閱[管理](../../../admin/adminpublic.html#administer)。

在開始之前，請先安裝 cf 指令行介面。{{site.data.keyword.Bluemix_notm}} 管理 CLI 外掛程式需要 cf 6.11.2 版或更新版本。[下載 Cloud Foundry 指令行介面](https://github.com/cloudfoundry/cli/releases){: new_window}

**限制：**Cygwin 不支援 Cloud Foundry 指令行介面。請在非 Cygwin 指令行視窗的指令行視窗中使用 Cloud Foundry 指令行介面。

## 新增 {{site.data.keyword.Bluemix_notm}} 管理 CLI 外掛程式

安裝 cf 指令行介面之後，您可以新增 {{site.data.keyword.Bluemix_notm}} 管理 CLI 外掛程式。

**附註**：如果您先前已安裝「{{site.data.keyword.Bluemix_notm}} 管理」外掛程式，則可能需要解除安裝外掛程式，刪除儲存庫，然後重新安裝以取得最新更新。

完成下列步驟以新增儲存庫並安裝外掛程式：

<ol>
<li>若要新增 {{site.data.keyword.Bluemix_notm}} 管理外掛程式儲存庫，請執行下列指令：<br/><br/>
<code>
cf add-plugin-repo BluemixAdmin https://console.&lt;subdomain&gt;.bluemix.net/cli
</code><br/><br/>
<dl class="parml">
<dt class="pt dlterm">&lt;subdomain&gt;</dt>
<dd class="pd">您的 {{site.data.keyword.Bluemix_notm}} 實例 URL 的子網域。</dd>
</dl>
</li>
<li>若要安裝 {{site.data.keyword.Bluemix_notm}} 管理 CLI 外掛程式，請執行下列指令：<br/><br/>
<code>
cf install-plugin bluemix-admin-cli -r BluemixAdmin
</code>
</li>
</ol>

## 使用 {{site.data.keyword.Bluemix_notm}} 管理 CLI 外掛程式

您可以使用 {{site.data.keyword.Bluemix_notm}} 管理 CLI 外掛程式來新增或移除使用者、對組織指派或取消指派使用者，以及執行其他管理作業。若要查看指令清單，請執行下列指令：


```
cf plugins
```
{: codeblock}

如需指令的其他說明，請使用 `-help` 選項。

### 連接及登入 {{site.data.keyword.Bluemix_notm}}

您必須先連接並登入（如果尚未完成的話），才能使用管理 CLI 外掛程式來管理使用者。

<ol>
<li>若要連接至 {{site.data.keyword.Bluemix_notm}} API 端點，請執行下列指令：<br/><br/>
<code>
cf ba api https://console.&lt;subdomain&gt;.bluemix.net
</code>
<dl class="parml">
<dt class="pt dlterm">&lt;subdomain&gt;</dt>
<dd class="pd">您的 {{site.data.keyword.Bluemix_notm}} 實例 URL 的子網域。<br />
</dd>
</dl>
<p>您可以查看「管理主控台」的「資源及資訊」頁面，以取得正確的 URL。URL 顯示在「API 資訊」區段的 **API URL** 欄位中。</p>
</li>
<li>使用下列指令來登入 {{site.data.keyword.Bluemix_notm}}：<br/><br/>
<code>
cf login
</code>
</li>
</ol>

### 新增使用者

您可以從 LDAP 登錄，將使用者新增至您的 {{site.data.keyword.Bluemix_notm}} 環境。輸入下列指令： 

```
cf ba add-user <user_name> <organization>
```
{: codeblock}

<dl class="parml">
<dt class="pt dlterm">&lt;user_name&gt;</dt>
<dd class="pd">LDAP 登錄中的使用者名稱。</dd>
<dt class="pt dlterm">&lt;organization&gt;</dt>
<dd class="pd">要新增使用者之 {{site.data.keyword.Bluemix_notm}} 組織的名稱或 GUID。</dd>
</dl>

**提示：**您也可以使用 **ba au** 作為較長的 **ba add-user** 指令名稱的別名。

<!-- staging-only commands start. Live for interconnect -->

### 搜尋使用者

您可以搜尋使用者。輸入下列指令： 

```
cf ba search-users <user_name>
```
{: codeblock}

<dl class="parml">

<dt class="pt dlterm">&lt;user_name&gt;</dt>
<dd class="pd">{{site.data.keyword.Bluemix_notm}} 中的使用者名稱。</dd>

</dl>

**提示：**您也可以使用 **ba su** 作為較長的 **ba search-users** 指令名稱的別名。

### 設定使用者的許可權

您可以設定所指定使用者的許可權。輸入下列指令： 

```
cf ba set-permissions <user_name> <permission> <access>
```
{: codeblock}

**附註**：一次可以設定一個許可權。

<dl class="parml">
<dt class="pt dlterm">&lt;user_name&gt;</dt>
<dd class="pd">{{site.data.keyword.Bluemix_notm}} 中的使用者名稱。</dd>
<dt class="pt dlterm">&lt;permission&gt;</dt>
<dd class="pd">設定使用者的許可權：Admin、Login、Catalog（讀取或寫入權）、Reports（讀取或寫入權）或 Users（讀取或寫入權）。</dd>
<dt class="pt dlterm">&lt;access&gt;</dt>
<dd class="pd">對於 Catalog、Reports 或 Users 許可權，您還必須將存取層次設定為 <code>read</code> 或 <code>write</code>。</dd>
</dl>

**提示：**您也可以使用 **ba sp** 作為較長的 **ba set-permissions** 指令名稱的別名。

<!-- staging-only commands end -->

### 移除使用者

您可以輸入下列指令，從您的 {{site.data.keyword.Bluemix_notm}} 環境中移除使用者：

```
cf ba remove-user <user_name>
```
{: codeblock}

<dl class="parml">

<dt class="pt dlterm">&lt;user_name&gt;</dt>
<dd class="pd">{{site.data.keyword.Bluemix_notm}} 中的使用者名稱。</dd>

</dl>

**提示：**您也可以使用 **ba ru** 作為較長的 **ba remove-user** 指令名稱的別名。

### 新增及刪除組織

您可以新增及刪除組織。

* 若要新增組織，請輸入下列指令：

```
cf ba create-organization <organization> <manager>
```
{: codeblock}

<dl class="parml">
<dt class="pt dlterm">&lt;organization&gt;</dt>
<dd class="pd">要新增之 {{site.data.keyword.Bluemix_notm}} 組織的名稱或 GUID。</dd>
<dt class="pt dlterm">&lt;manager&gt;</dt>
<dd class="pd">組織管理員的使用者名稱。</dd>
</dl>

**提示：**您也可以使用 **ba co** 作為較長的 **ba create-organization** 指令名稱的別名。

* 若要刪除組織，請輸入下列指令：

```
cf ba delete-organization <organization>
```
{: codeblock}

<dl class="parml">
<dt class="pt dlterm">&lt;organization&gt;</dt>
<dd class="pd">要刪除之 {{site.data.keyword.Bluemix_notm}} 組織的名稱或 GUID。</dd>
</dl>

**提示：**您也可以使用 **ba do** 作為較長的 **ba delete-organization** 指令名稱的別名。

### 將使用者指派至組織

您可以將 {{site.data.keyword.Bluemix_notm}} 環境中的使用者指派給特定組織。輸入下列指令： 

```
cf ba set-org <user_name> <organization> [<role>]
```
{: codeblock}

<dl class="parml">
<dt class="pt dlterm">&lt;user_name&gt;</dt>
<dd class="pd">{{site.data.keyword.Bluemix_notm}} 中的使用者名稱。</dd>
<dt class="pt dlterm">&lt;organization&gt;</dt>
<dd class="pd">要指派使用者之 {{site.data.keyword.Bluemix_notm}} 組織的名稱或 GUID。</dd>
<dt class="pt dlterm">&lt;role&gt;</dt>
<dd class="pd">請參閱[角色](../../../admin/adminpublic.html#orgsandspaces)，以取得 {{site.data.keyword.Bluemix_notm}} 使用者的角色及說明。</dd>
</dl>

**提示：**您也可以使用 **ba so** 作為較長的 **ba set-org** 指令名稱的別名。

### 從組織取消指派使用者

您可以從特定組織取消指派 {{site.data.keyword.Bluemix_notm}} 環境中的使用者。輸入下列指令： 

```
cf ba unset-org <user_name> <organization> [<role>]
```
{: codeblock}

<dl class="parml">
<dt class="pt dlterm">&lt;user_name&gt;</dt>
<dd class="pd">{{site.data.keyword.Bluemix_notm}} 中的使用者名稱。</dd>
<dt class="pt dlterm">&lt;organization&gt;</dt>
<dd class="pd">要指派使用者之 {{site.data.keyword.Bluemix_notm}} 組織的名稱或 GUID。</dd>
<dt class="pt dlterm">&lt;role&gt;</dt>
<dd class="pd">請參閱[角色](../../../admin/adminpublic.html#orgsandspaces)，以取得 {{site.data.keyword.Bluemix_notm}} 使用者的角色及說明。</dd>
</dl>

**提示：**您也可以使用 **ba uo** 作為較長的 **ba unset-org** 指令名稱的別名。

### 角色

<dl class="parml">
<dt class="pt dlterm">OrgManager</dt>
<dd class="pd">組織管理員。組織管理員具有執行下列動作的權限：<ul>
<li>在組織內建立或刪除空間。</li>
<li>邀請使用者加入組織及管理使用者。</li>
<li>管理組織的網域。</li>
</ul>
</dd>
<dt class="pt dlterm">BillingManager</dt>
<dd class="pd">帳單管理員。帳單管理員可以檢視組織的執行時期及服務用量資訊。</dd>
<dt class="pt dlterm">OrgAuditor</dt>
<dd class="pd">組織審核員。組織審核員可以檢視空間中的應用程式及服務內容。</dd>
</dl>

### 設定組織的配額

您可以設定特定組織的使用配額。

```
cf ba set-quota <organization> <plan>
```
{: codeblock}

<dl class="parml">
<dt class="pt dlterm">&lt;organization&gt;</dt>
<dd class="pd">要設定配額之 {{site.data.keyword.Bluemix_notm}} 組織的名稱或 GUID。</dd>
<dt class="pt dlterm">&lt;plan&gt;</dt>
<dd class="pd">組織的配額方案。</dd>
</dl>

**提示：**您也可以使用 **ba sq** 作為較長的 **ba set-quota** 指令名稱的別名。

### 新增、刪除及擷取報告

您可以新增、刪除及擷取安全報告。
* 若要新增報告，請輸入下列指令：

```
cf ba add-report <category> <date> <PDF|TXT|LOG> <RTF>
```
{: codeblock}

<dl class="parml">
<dt class="pt dlterm">&lt;category&gt;</dt>
<dd class="pd">報告的種類。如果名稱中有空格，請使用引號括住該名稱。</dd>
<dt class="pt dlterm">&lt;date&gt;</dt>
<dd class="pd">報告日期，格式為 <samp class="ph codeph">YYYYMMDD</samp>。</dd>
<dt class="pt dlterm">&lt;PDF|TXT|LOG&gt;</dt>
<dd class="pd">要上傳之報告 PDF、文字檔或日誌檔的路徑。</dd>
<dt class="pt dlterm">&lt;RTF&gt;</dt>
<dd class="pd">用來包含 PDF 之「Rich Text 格式 (RTF)」版本的選項。只有在您包含報告 PDF 的路徑時，此選項才適用。RTF 版本用於編製索引及進行搜尋。</dd>
</dl>

**提示：**您也可以使用 **ba ar** 作為較長的 **ba add-report** 指令名稱的別名。

* 若要刪除報告，請輸入下列指令：

```
cf ba delete-report <category> <date> <name>
```
{: codeblock}

<dl class="parml">
<dt class="pt dlterm">&lt;category&gt;</dt>
<dd class="pd">報告的種類。如果名稱中有空格，請使用引號括住該名稱。</dd>
<dt class="pt dlterm">&lt;date&gt;</dt>
<dd class="pd">報告日期，格式為 <samp class="ph codeph">YYYYMMDD</samp>。</dd>
<dt class="pt dlterm">&lt;name&gt;</dt>
<dd class="pd">報告的名稱。</dd>
</dl>

**提示：**您也可以使用 **ba dr** 作為較長的 **ba delete-report** 指令名稱的別名。

* 若要擷取報告，請輸入下列指令：

```
cf ba retrieve-report <category> <date> <name>
```
{: codeblock}

<dl class="parml">
<dt class="pt dlterm">&lt;category&gt;</dt>
<dd class="pd">報告的種類。如果名稱中有空格，請使用引號括住該名稱。</dd>
<dt class="pt dlterm">&lt;date&gt;</dt>
<dd class="pd">報告日期，格式為 <samp class="ph codeph">YYYYMMDD</samp>。</dd>
<dt class="pt dlterm">&lt;name&gt;</dt>
<dd class="pd">報告的名稱。</dd>
</dl>

**提示：**您也可以使用 **ba rr** 作為較長的 **ba retrieve-report** 指令名稱的別名。

### 啟用及停用所有組織的服務

您可以針對所有組織，啟用或停用服務在 {{site.data.keyword.Bluemix_notm}}「型錄」中的顯示。

* 若要讓所有組織可在 {{site.data.keyword.Bluemix_notm}}「型錄」中看見服務，請輸入下列指令：

```
cf ba enable-service-plan <plan_identifier>
```
{: codeblock}

<dl class="parml">
<dt class="pt dlterm">&lt;plan_identifier&gt;</dt>
<dd class="pd">您要啟用之服務的名稱或 GUID。如果輸入非唯一的服務名稱，系統會提示您服務方案以從中進行選擇。</dd>
</dl>

**提示：**您也可以使用 **ba esp** 作為較長的 **ba enable-service-plan** 指令名稱的別名。

* 若要讓所有組織在 {{site.data.keyword.Bluemix_notm}}「型錄」中看不見服務，請輸入下列指令：

```
cf ba disable-service-plan <plan_identifier>
```
{: codeblock}

<dl class="parml">
<dt class="pt dlterm">&lt;plan_identifier&gt;</dt>
<dd class="pd">您要停用之服務的名稱或 GUID。如果輸入非唯一的服務名稱，系統會提示您服務方案以從中進行選擇。</dd>
</dl>

**提示：**您也可以使用 **ba dsp** 作為較長的 **ba disable-service-plan** 指令名稱的別名。

### 新增、移除及編輯組織的服務可見性

您可以從組織清單中新增或移除可在 {{site.data.keyword.Bluemix_notm}}「型錄」中看見特定服務的組織。您也可以編輯及取代特定組織可在 {{site.data.keyword.Bluemix_notm}}
的「型錄」中看到的服務清單。

* 若要容許組織檢視 {{site.data.keyword.Bluemix_notm}}「型錄」中的特定服務，請輸入下列指令：

```
cf ba add-service-plan-visibility <plan_identifier> <organization>
```
{: codeblock}

<dl class="parml">
<dt class="pt dlterm">&lt;plan_identifier&gt;</dt>
<dd class="pd">您要新增可見性之服務的名稱或 GUID。如果輸入非唯一的服務名稱，系統會提示您服務方案以從中進行選擇。</dd>
<dt class="pt dlterm">&lt;organization&gt;</dt>
<dd class="pd">要新增至服務可見性清單的 {{site.data.keyword.Bluemix_notm}} 組織的名稱或 GUID。</dd>
</dl>

**提示：**您也可以使用 **ba aspv** 作為較長的 **ba add-service-plan-visibility** 指令名稱的別名。

* 若要針對組織移除 {{site.data.keyword.Bluemix_notm}}「型錄」中的服務可見性，請輸入下列指令：

```
cf ba remove-service-plan-visibility <plan_identifier> <organization>
```
{: codeblock}

<dl class="parml">
<dt class="pt dlterm">&lt;plan_identifier&gt;</dt>
<dd class="pd">您要移除可見性之服務的名稱或 GUID。如果輸入非唯一的服務名稱，系統會提示您服務方案以從中進行選擇。</dd>
<dt class="pt dlterm">&lt;organization&gt;</dt>
<dd class="pd">要從服務的可見性清單中移除之 {{site.data.keyword.Bluemix_notm}} 組織的名稱或 GUID。</dd>
</dl>

**提示：**您也可以使用 **ba rspv** 作為較長的 **ba remove-service-plan-visibility** 指令名稱的別名。

* 若要取代一個組織或多個組織的所有現有可見服務，請使用下列指令：

```
cf ba edit-service-plan-visibilities <plan_identifier> <organization_1> <optional_organization_2>
```
{: codeblock}

**附註：**此指令會將所指定組織的現有可見服務取代為您在指令中指定的服務。

<dl class="parml">
<dt class="pt dlterm">&lt;plan_identifier&gt;</dt>
<dd class="pd">您要使其可見之服務的名稱或 GUID。如果輸入非唯一的服務名稱，系統會提示您服務方案以從中進行選擇。</dd>
<dt class="pt dlterm">&lt;organization&gt;</dt>
<dd class="pd">要新增可見性之 {{site.data.keyword.Bluemix_notm}} 組織的名稱或 GUID。您可以在指令中輸入其他組織名稱或 GUID，針對多個組織啟用服務的可見性。</dd>
</dl>

**提示：**您也可以使用 **ba espv** 作為較長的 **ba edit-service-plan-visibility** 指令名稱的別名。

### 使用服務分配管理系統

下列指令可用來列出所有服務分配管理系統、新增或刪除服務分配管理系統，或更新服務分配管理系統。

* 您可以輸入下列指令來列出服務分配管理系統：

```
cf ba service-brokers <broker_name>
```
{: codeblock}

**附註**：若要列出所有服務分配管理系統，請輸入不含 `broker_name` 參數的指令。 

<dl class="parml">
<dt class="pt dlterm">&lt;broker_name&gt;</dt>
<dd class="pd">選用項目：自訂服務分配管理系統的名稱。如果您要取得特定服務分配管理系統的資訊，請使用此參數。</dd>
</dl>

**提示：**您也可以使用 **ba sb** 作為較長的 **ba service-brokers** 指令名稱的別名。

* 您可以輸入下列指令來新增服務分配管理系統，以將自訂服務新增至 {{site.data.keyword.Bluemix_notm}}「型錄」：

```
cf ba add-service-broker <broker_name> <user_name> <password> <broker_url>
```
{: codeblock}

<dl class="parml">
<dt class="pt dlterm">&lt;broker_name&gt;</dt>
<dd class="pd">自訂服務分配管理系統的名稱。</dd>
<dt class="pt dlterm">&lt;user_name&gt;</dt>
<dd class="pd">可存取服務分配管理系統的帳戶的使用者名稱。</dd>
<dt class="pt dlterm">&lt;password&gt;</dt>
<dd class="pd">可存取服務分配管理系統的帳戶的密碼。</dd>
<dt class="pt dlterm">&lt;broker_url&gt;</dt>
<dd class="pd">服務分配管理系統的 URL。</dd>
</dl>

**提示：**您也可以使用 **ba asb** 作為較長的 **ba add-service-broker** 指令名稱的別名。

* 您可以輸入下列指令來刪除服務分配管理系統，以從 {{site.data.keyword.Bluemix_notm}}「型錄」中移除自訂服務：

```
cf ba delete-service-broker <service_broker>
```
{: codeblock}

<dl class="parml">
<dt class="pt dlterm">&lt;service_broker&gt;</dt>
<dd class="pd">自訂服務分配管理系統的名稱或 GUID。</dd>
</dl>

**提示：**您也可以使用 **ba dsb** 作為較長的 **ba delete-service-broker** 指令名稱的別名。

* 您可以輸入下列指令來更新服務分配管理系統：

`cf ba update-service-broker <broker_name> <user_name> <password> <broker_url>`
{: codeblock}

<dl class="parml">
<dt class="pt dlterm">&lt;broker_name&gt;</dt>
<dd class="pd">自訂服務分配管理系統的名稱。</dd>
<dt class="pt dlterm">&lt;user_name&gt;</dt>
<dd class="pd">可存取服務分配管理系統的帳戶的使用者名稱。</dd>
<dt class="pt dlterm">&lt;password&gt;</dt>
<dd class="pd">可存取服務分配管理系統的帳戶的密碼。</dd>
<dt class="pt dlterm">&lt;broker_url&gt;</dt>
<dd class="pd">服務分配管理系統的 URL。</dd>
</dl>

**提示：**您也可以使用 **ba usb** 作為較長的 **ba update-service-broker** 指令名稱的別名。
