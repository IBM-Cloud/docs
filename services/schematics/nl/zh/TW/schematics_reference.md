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

# {{site.data.keyword.Bluemix_notm}} CLI 的 {{site.data.keyword.bpshort}} CLI 外掛程式
{: #cli}

請參閱 {{site.data.keyword.Bluemix}} CLI 的 {{site.data.keyword.bpshort}} 指令，以在 {{site.data.keyword.Bluemix_notm}} 內管理環境及執行其他作業。
{: shortdesc}

使用 CLI 指令之前，請執行下列動作：

* 使用 `bx login [--sso]` 登入 {{site.data.keyword.Bluemix_notm}} 以鑑別您的階段作業。具有聯合 ID 的使用者需要使用 `--sso` 旗標，來產生一次性的通行碼。

若要檢視指令的清單，您可以執行 `bx schematics help`。

<table id="manage_environments" summary="使用 bx schematics environment 指令管理環境。">
<caption>表 1. 管理環境的可用指令。指令遵循 <code>bx schematics environment</code> 語法。
</caption>
 <thead>
 <th colspan="5">管理環境</th>
 </thead>
 <tbody>
 <tr>
 <td>[bx schematics environment create](#environment-create)</td>
 <td>[bx schematics environment delete](#environment-delete)</td>
 <td>[bx schematics environment list](#environment-list)</td>
 <td>[bx schematics environment show](#environment-show)</td>
 <td>[bx schematics environment update](#environment-update)</td>
 </tr>
</tbody></table>
 
 <table id="update_resources" summary="使用 bx schematics action 指令更新由您的環境所佈建的資源。">
 <caption>表 2. 更新環境中資源的可用指令。指令遵循 <code>bx schematics action</code> 語法。
  </caption>
  <thead>
  <th colspan="5">更新資源</th>
  </thead>
  <tbody>
  <td>[bx schematics action apply](#action-apply)</td>
  <td>[bx schematics action destroy](#action-destroy)</td>
  <td>[bx schematics action plan](#action-plan)</td>
  </tr></tbody></table>
  
  <table id="audit_environment" summary="使用 bx schematics activity 指令審核針對您的環境執行的活動。">
  <caption>表 3. 審核針對您的環境執之活動的可用指令。指令遵循 <code>bx schematics activity</code> 語法。
  </caption>
   <thead>
   <th colspan="5">審核環境</th>
   </thead>
   <tbody>
   <td>[bx schematics activity list](#activity-list)</td>
   <td>[bx schematics activity log](#activity-log)</td>
   <td>[bx schematics activity planfile](#activity-planfile)</td>
   <td>[bx schematics activity show](#activity-show)</td>
   </tr></tbody></table>

## bx schematics environment create
{: #environment-create notoc}

在 {{site.data.keyword.Bluemix_notm}} 中從您的配置建立環境。

```
bx schematics environment create --file FILE_NAME [--json]
```
{: codeblock}

### 參數

<dl>
<dt>--file FILE_NAME</dt>
<dd>用來傳遞您的環境詳細資料的 JSON 檔案。
<p>
<p>範例 JSON 與所有可用的值：
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
}</pre></dd>
<dt>--json</dt>
<dd>以 JSON 格式列印輸出。</dd>
</dl>

## bx schematics environment delete
{: #environment-delete notoc}

從 {{site.data.keyword.Bluemix_notm}} 移除您的環境配置。這個指令僅建議用於沒有執行中資源的環境。如果您刪除具有執行中資源的環境，您需要在個別服務儀表板中管理每個資源。

```
bx schematics environment delete --id ENVIRONMENT_ID [--force]
```
{: codeblock}

### 參數

<dl>
<dt>--id ENVIRONMENT_ID</dt>
<dd>環境的唯一 ID。您可以透過執行 <code>bx schematics environment list</code> 擷取此值。</dd>
<dt>--force</dt>
<dd>強制推進指令執行而不進行 yes/no 確認。</dd>
</dl>

## bx schematics environment list
{: #environment-list notoc}

擷取 {{site.data.keyword.Bluemix_notm}} 帳戶中所有現有環境的清單。

```
bx schematics environment list [--count VALUE] [--offset VALUE] [--json] 
```
{: codeblock}

### 參數
<dl>
<dt>--count VALUE</dt>
<dd>要在傳回中限制的環境數目。</dd>
<dt>--offset VALUE</dt>
<dd>環境清單中的偏移。</dd>
<dt>--json</dt>
<dd>以 JSON 格式列印輸出。</dd>
</dl>

## bx schematics environment show
{: #environment-show notoc}

擷取現有環境的相關詳細資料。

```
bx schematics environment show --id ENVIRONMENT_ID [--json]
```
{: codeblock}

### 參數
<dl>
<dt>--id ENVIRONMENT_ID</dt>
<dd>環境的唯一 ID。您可以透過執行 <code>bx schematics environment list</code> 擷取此值。</dd>
<dt>--json</dt>
<dd>以 JSON 格式列印輸出。</dd>
</dl>
  
## bx schematics environment update
{: #environment-update notoc}

更新現有環境的相關詳細資料，例如環境名稱或 GitHub URL。若要更新環境中已配置的資源數目，請參閱 [bx schematics action plan](#action-plan)。

```
bx schematics environment update --id ENVIRONMENT_ID --file FILE_NAME [--json]
```
{: codeblock}

### 參數
<dl>
<dt>--id ENVIRONMENT_ID</dt>
<dd>環境的唯一 ID。您可以透過執行 <code>bx schematics environment list</code> 擷取此值。</dd>
<dt>--file FILE_NAME</dt>
<dd>用來傳遞您的環境詳細資料的 JSON 檔案。如需範例 JSON Snippet 與接受的值，請參閱 [bx schematics environment create](#environment-create)。</dd>
<dt>--json</dt>
<dd>以 JSON 格式列印輸出。</dd>
</dl>

## bx schematics action apply
{: #action-apply notoc}

部署環境配置。`apply` 指令會掃描並執行 GitHub 儲存庫中儲存的配置。

```
bx schematics action apply --id ENVIRONMENT_ID [--force] [--json]
```
{: codeblock}

### 參數
<dl>
<dt>--id ENVIRONMENT_ID</dt>
<dd>環境的唯一 ID。您可以透過執行 <code>bx schematics environment list</code> 擷取此值。</dd>
<dt>--force</dt>
<dd>強制推進指令執行而不進行 yes/no 確認。</dd>
<dt>--json</dt>
<dd>以 JSON 格式列印 apply 輸出。</dd>
</dl>

## bx schematics action destroy
{: #action-destroy notoc}

破壞您的環境和資源。`destroy` 指令會關閉您的環境，包括執行中的資源。此動作只通常用於暫存環境，例如 QA 環境，其目的是要維持該環境一段有限的期間。不建議您破壞正式作業環境。`destroy` 動作無法回復，應該小心使用。

```
bx schematics action destroy --id ENVIRONMENT_ID [--force] [--json]
```
{: codeblock}

### 參數
<dl>
<dt>--id ENVIRONMENT_ID</dt>
<dd>環境的唯一 ID。您可以透過執行 <code>bx schematics environment list</code> 擷取此值。</dd>
<dt>--force</dt>
<dd>強制推進指令執行而不進行 yes/no 確認。</dd>
<dt>--json</dt>
<dd>以 JSON 格式列印 destroy 輸出。</dd>
</dl>
</dl>

## bx schematics action plan
{: #action-plan notoc}

比較您的環境配置與已部署的配置。`plan` 指令會掃描 GitHub 儲存庫中的配置，並針對與您的已部署環境相關聯的狀態檔執行 diff。plan 輸出會顯示如果您已使用 `apply` 指令部署環境配置，要新增或移除哪些資源。 

```
bx schematics action plan --id ENVIRONMENT_ID [--file FILE_NAME] [--json]
```
{: codeblock}

### 參數
<dl>
<dt>--id ENVIRONMENT_ID</dt>
<dd>環境的唯一 ID。您可以透過執行 <code>bx schematics environment list</code> 擷取此值。</dd>
<dt>--file FILE_NAME</dt>
<dd>用來傳遞 plan 動作之參數的選用性 JSON 檔案。您可以傳遞參數 <code>sourcesha</code> 來參照環境之 Terraform 配置的特定 Git 分支。Git 分支必須指定為 head 參照，例如 <code>refs/heads/BRANCH_NAME</code>。如果沒有指定任何參數，預設值是主要分支的 head，也就是 <code>refs/heads/master</code>。<p>
<p>範例 JSON Snippet 與值：
<pre>{
  "sourcesha": "refs/heads/BRANCH_NAME"
}</pre></dd>
<dt>--json</dt>
<dd>以 JSON 格式列印 plan 輸出。</dd>
</dl>

## bx schematics activity list
{: #activity-list notoc}

列出從針對環境執行之 Terraform 活動的資料。

```
bx schematics activity list --id ENVIRONMENT_ID [--count VALUE] [--offset VALUE] [--json]
```
{: codeblock}

### 參數
<dl>
<dt>--id ENVIRONMENT_ID</dt>
<dd>環境的唯一 ID。您可以透過執行 <code>bx schematics environment list</code> 擷取此值。</dd>
<dt>--count VALUE</dt>
<dd>要傳回的活動數目。</dd>
<dt>--offset VALUE</dt>
<dd>清單中的偏移。</dd>
<dt>--json</dt>
<dd>以 JSON 格式列印 plan 輸出。</dd>
</dl>

## bx schematics activity log
{: #activity-log notoc}

檢視針對環境執行之動作的詳細活動日誌。

```
bx schematics activity log --id ACTIVITY_ID
```
{: codeblock}

### 參數
<dl>
<dt>--id ACTIVITY_ID</dt>
<dd>用來傳回特定活動相關詳細資料的旗標。您可以使用 <code>bx schematics activity list --id ENVIRONMENT_ID</code> 指令擷取每個環境的活動 ID 清單。</dd>
</dl>

## bx schematics activity planfile
{: #activity-planfile notoc}

檢視環境的方案檔案。

```
bx schematics activity planfile --id ACTIVITY_ID
```
{: codeblock}

### 參數
<dl>
<dt>--id ACTIVITY_ID</dt>
<dd>用來傳回特定活動相關詳細資料的旗標。您可以使用 <code>bx schematics activity list --id ENVIRONMENT_ID</code> 指令擷取每個環境的活動 ID 清單。</dd>
</dl>

## bx schematics activity show
{: #activity-show notoc}

擷取針對環境執行之特定活動的相關詳細資料。

```
bx schematics activity show --id ACTIVITY_ID [--json]
```
{: codeblock}

### 參數
<dl>
<dt>--id ACTIVITY_ID</dt>
<dd>用來傳回特定活動相關詳細資料的旗標。您可以使用 <code>bx schematics activity list --id ENVIRONMENT_ID</code> 指令擷取每個環境的活動 ID 清單。</dd>
<dt>--json</dt>
<dd>以 JSON 格式列印 plan 輸出。</dd>
</dl>
