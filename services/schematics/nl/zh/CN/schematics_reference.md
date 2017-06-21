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

# {{site.data.keyword.Bluemix_notm}} CLI 的 {{site.data.keyword.bpshort}} CLI 插件
{: #cli}

请参阅 {{site.data.keyword.Bluemix}} CLI 的 {{site.data.keyword.bpshort}} 命令，以在 {{site.data.keyword.Bluemix_notm}} 中管理环境和执行其他操作。
{: shortdesc}

使用 CLI 命令之前，请执行以下操作：

* 使用 `bx login [--sso]` 登录到 {{site.data.keyword.Bluemix_notm}} 以认证会话。使用联合标识的用户需要使用 `--sso` 标志来生成一次性密码。

要查看命令的列表，可以运行 `bx schematics help`。

<table id="manage_environments" summary="使用 bx schematics environment 命令管理环境。">
<caption>表 1. 可用于管理环境的命令。这些命令均遵循 <code>bx schematics environment</code> 语法。
</caption>
 <thead>
 <th colspan="5">管理环境</th>
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
 
 <table id="update_resources" summary="使用 bx schematics action 命令更新环境供应的资源。">
 <caption>表 2. 可用于更新环境中资源的命令。这些命令均遵循 <code>bx schematics action</code> 语法。</caption>
  <thead>
  <th colspan="5">更新资源</th>
  </thead>
  <tbody>
  <td>[bx schematics action apply](#action-apply)</td>
  <td>[bx schematics action destroy](#action-destroy)</td>
  <td>[bx schematics action plan](#action-plan)</td>
  </tr></tbody></table>
  
  <table id="audit_environment" summary="使用 bx schematics activity 命令审计对环境运行的活动。">
  <caption>表 3. 可用于审计对环境运行的活动的命令。这些命令均遵循 <code>bx schematics activity</code> 语法。</caption>
   <thead>
   <th colspan="5">审计环境</th>
   </thead>
   <tbody>
   <td>[bx schematics activity list](#activity-list)</td>
   <td>[bx schematics activity log](#activity-log)</td>
   <td>[bx schematics activity planfile](#activity-planfile)</td>
   <td>[bx schematics activity show](#activity-show)</td>
   </tr></tbody></table>

## bx schematics environment create
{: #environment-create notoc}

在 {{site.data.keyword.Bluemix_notm}} 中通过配置来创建环境。

```
bx schematics environment create --file FILE_NAME [--json]
```
{: codeblock}

### 参数

<dl>
<dt>--file FILE_NAME</dt>
<dd>用于传递环境相关详细信息的 JSON 文件。
<p>
<p>具有所有可用值的示例 JSON：
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
<dd>以 JSON 格式显示输出。</dd>
</dl>

## bx schematics environment delete
{: #environment-delete notoc}

从 {{site.data.keyword.Bluemix_notm}} 中除去环境配置。此命令仅建议用于没有运行中资源的环境。如果删除具有运行中资源的环境，那么需要在不同服务仪表板中分别管理各个资源。

```
bx schematics environment delete --id ENVIRONMENT_ID [--force]
```
{: codeblock}

### 参数

<dl>
<dt>--id ENVIRONMENT_ID</dt>
<dd>环境的唯一标识。可以通过运行 <code>bx schematics environment list</code> 来检索此值。</dd>
<dt>--force</dt>
<dd>强制推进命令，而不进行 yes/no 确认。</dd>
</dl>

## bx schematics environment list
{: #environment-list notoc}

检索您的 {{site.data.keyword.Bluemix_notm}} 帐户中所有现有环境的列表。

```
bx schematics environment list [--count VALUE] [--offset VALUE] [--json] 
```
{: codeblock}

### 参数
<dl>
<dt>--count VALUE</dt>
<dd>要在返回中限制的环境数。</dd>
<dt>--offset VALUE</dt>
<dd>环境列表中的偏移量。</dd>
<dt>--json</dt>
<dd>以 JSON 格式显示输出。</dd>
</dl>

## bx schematics environment show
{: #environment-show notoc}

检索有关现有环境的详细信息。

```
bx schematics environment show --id ENVIRONMENT_ID [--json]
```
{: codeblock}

### 参数
<dl>
<dt>--id ENVIRONMENT_ID</dt>
<dd>环境的唯一标识。可以通过运行 <code>bx schematics environment list</code> 来检索此值。</dd>
<dt>--json</dt>
<dd>以 JSON 格式显示输出。</dd>
</dl>
  
## bx schematics environment update
{: #environment-update notoc}

更新有关现有环境的详细信息，例如环境名称或 GitHub URL。要更新环境中分配的资源数，请参阅 [bx schematics action plan](#action-plan)。

```
bx schematics environment update --id ENVIRONMENT_ID --file FILE_NAME [--json]
```
{: codeblock}

### 参数
<dl>
<dt>--id ENVIRONMENT_ID</dt>
<dd>环境的唯一标识。可以通过运行 <code>bx schematics environment list</code> 来检索此值。</dd>
<dt>--file FILE_NAME</dt>
<dd>用于传递环境相关详细信息的 JSON 文件。有关具有允许值的示例 JSON 片段，请参阅 [bx schematics environment create](#environment-create)。</dd>
<dt>--json</dt>
<dd>以 JSON 格式显示输出。</dd>
</dl>

## bx schematics action apply
{: #action-apply notoc}

部署环境配置。`apply` 命令可扫描和执行存储在 GitHub 存储库中的配置。

```
bx schematics action apply --id ENVIRONMENT_ID [--force] [--json]
```
{: codeblock}

### 参数
<dl>
<dt>--id ENVIRONMENT_ID</dt>
<dd>环境的唯一标识。可以通过运行 <code>bx schematics environment list</code> 来检索此值。</dd>
<dt>--force</dt>
<dd>强制推进命令，而不进行 yes/no 确认。</dd>
<dt>--json</dt>
<dd>以 JSON 格式显示 apply 输出。</dd>
</dl>

## bx schematics action destroy
{: #action-destroy notoc}

销毁环境和资源。`destroy` 命令将破坏您的环境，包括运行中的资源。此操作通常仅用于旨在保留有限时间段的临时环境，例如 QA 环境。建议不要销毁生产环境。`destroy` 操作不可撤销，因此使用时应谨慎。

```
bx schematics action destroy --id ENVIRONMENT_ID [--force] [--json]
```
{: codeblock}

### 参数
<dl>
<dt>--id ENVIRONMENT_ID</dt>
<dd>环境的唯一标识。可以通过运行 <code>bx schematics environment list</code> 来检索此值。</dd>
<dt>--force</dt>
<dd>强制推进命令，而不进行 yes/no 确认。</dd>
<dt>--json</dt>
<dd>以 JSON 格式显示 destroy 输出。</dd>
</dl>
</dl>

## bx schematics action plan
{: #action-plan notoc}

将您的环境配置与部署的配置进行比较。`plan` 命令会扫描 GitHub 存储库中的配置，并比较与已部署环境关联的状态文件的差异。plan 输出会显示使用 `apply` 命令部署环境配置时将添加或除去的资源。 

```
bx schematics action plan --id ENVIRONMENT_ID [--file FILE_NAME] [--json]
```
{: codeblock}

### 参数
<dl>
<dt>--id ENVIRONMENT_ID</dt>
<dd>环境的唯一标识。可以通过运行 <code>bx schematics environment list</code> 来检索此值。</dd>
<dt>--file FILE_NAME</dt>
<dd>用于传递 plan 操作参数的可选 JSON 文件。可以传递 <code>sourcesha</code> 参数以引用环境的 Terraform 配置的特定 Git 分支。该 Git 分支必须指定为头引用，例如 <code>refs/heads/BRANCH_NAME</code>。如果未指定任何参数，那么缺省值为主分支的头，即 <code>refs/heads/master</code>。
<p>
<p>具有值的示例 JSON 片段：
<pre>{
  "sourcesha": "refs/heads/BRANCH_NAME"
}</pre></dd>
<dt>--json</dt>
<dd>以 JSON 格式显示 plan 输出。</dd>
</dl>

## bx schematics activity list
{: #activity-list notoc}

列出来自对环境运行的 Terraform 活动的数据。

```
bx schematics activity list --id ENVIRONMENT_ID [--count VALUE] [--offset VALUE] [--json]
```
{: codeblock}

### 参数
<dl>
<dt>--id ENVIRONMENT_ID</dt>
<dd>环境的唯一标识。可以通过运行 <code>bx schematics environment list</code> 来检索此值。</dd>
<dt>--count VALUE</dt>
<dd>要返回的活动数。</dd>
<dt>--offset VALUE</dt>
<dd>列表中的偏移量。</dd>
<dt>--json</dt>
<dd>以 JSON 格式显示 plan 输出。</dd>
</dl>

## bx schematics activity log
{: #activity-log notoc}

查看对环境运行的操作的详细活动日志。

```
bx schematics activity log --id ACTIVITY_ID
```
{: codeblock}

### 参数
<dl>
<dt>--id ACTIVITY_ID</dt>
<dd>用于返回有关特定活动的详细信息的标志。可以使用 <code>bx schematics activity list --id ENVIRONMENT_ID</code> 命令来检索每个环境的活动标识的列表。</dd>
</dl>

## bx schematics activity planfile
{: #activity-planfile notoc}

查看环境的计划文件。

```
bx schematics activity planfile --id ACTIVITY_ID
```
{: codeblock}

### 参数
<dl>
<dt>--id ACTIVITY_ID</dt>
<dd>用于返回有关特定活动的详细信息的标志。可以使用 <code>bx schematics activity list --id ENVIRONMENT_ID</code> 命令来检索每个环境的活动标识的列表。</dd>
</dl>

## bx schematics activity show
{: #activity-show notoc}

检索有关对环境运行的特定活动的详细信息。

```
bx schematics activity show --id ACTIVITY_ID [--json]
```
{: codeblock}

### 参数
<dl>
<dt>--id ACTIVITY_ID</dt>
<dd>用于返回有关特定活动的详细信息的标志。可以使用 <code>bx schematics activity list --id ENVIRONMENT_ID</code> 命令来检索每个环境的活动标识的列表。</dd>
<dt>--json</dt>
<dd>以 JSON 格式显示 plan 输出。</dd>
</dl>
