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

# 将资源部署到环境
{: #deploying}

使用 {{site.data.keyword.bplong}}，您可以直接从源代码部署最新的代码更改。部署环境时，将部署的是配置文件定义的资源。然后，可以在 {{site.data.keyword.bpshort}} 中管理环境的供应、编排和生命周期。
{:shortdesc}

## 使用 GUI 部署到环境
{: #gui}

如果更希望使用图形视图来部署环境，那么可以使用 {{site.data.keyword.bpshort}} 仪表板。
{:shortdesc}


### 先决条件
{: #gui-prereq}

* 在源代码控制中存储 Terraform 配置。配置可以使用 HashiCorp 配置语言 (HCL) 或 JSON 语法进行编写。有关如何编写配置的 HCL 语法和准则，请参阅 <a href="https://www.terraform.io/docs/configuration/index.html">Terraform 配置文档 <img src="../../icons/launch-glyph.svg" alt="外部链接图标"></a>。有关可用资源的信息，请参阅 <a href="https://ibm-bluemix.github.io/tf-ibm-docs/">{{site.data.keyword.IBM_notm}} Cloud 提供者 <img src="../../icons/launch-glyph.svg" alt="外部链接图标"></a>。

存储配置后，请执行以下操作：

1. 在 **{{site.data.keyword.bpshort}}** 仪表板中，选择**环境**。

2. 单击**创建环境**以添加环境，或者选择要部署的现有环境所在的行。

3. 单击**计划**以预览部署环境时供应的资源。运行计划时，{{site.data.keyword.bpshort}} 会抽取环境详细信息中的变量，并从源代码控制中抽取最新版本的配置。计划输出会显示配置与根据 Terraform 状态文件部署的内容相比较的结果。环境会一直锁定，直到将计划应用到环境或取消计划之后才接受更多更改。 

4. 在**最近的活动**部分中查看日志来检查计划输出。计划输出会显示是否存在错误，以及服务计划创建、更改或销毁的资源。

5. 准备好启动计划时，单击**应用**。可以监视活动日志以确保在最新的运行中成功应用计划。 


## 使用 CLI 部署到环境
{: #cli}

可以使用 {{site.data.keyword.Bluemix_notm}} CLI 的 {{site.data.keyword.bpshort}} 插件将更新部署到环境。
{:shortdesc}

### 先决条件
{: #cli-prereq}

* 在源代码控制中存储 Terraform 配置。
* 如果尚未安装适合您操作系统的 {{site.data.keyword.Bluemix_notm}} CLI，请通过 [{{site.data.keyword.Bluemix_notm}} CLI 存储库](http://clis.ng.bluemix.net/ui/home.html)进行安装。

登录到 {{site.data.keyword.Bluemix_notm}} CLI 后，请执行以下操作：

1. 通过运行以下命令，安装 {{site.data.keyword.bpshort}} CLI 插件。
  
  ```
  bx plugin install schematics -r Bluemix
  ```
  {: codeblock}

  如果安装成功，{{site.data.keyword.bpshort}} 插件会显示在 `bx plugin list` 下。 

2. 通过配置来创建环境。创建环境时，您会将此服务指向源代码控制，以便它可以抽取最新的代码。 
  
  ```
  bx schematics environment create --file FILE_NAME
  ```
  {: codeblock}
  
  <table summary="environment create 命令的描述。">
  <caption>表 1. environment create 命令的描述。</caption>
  <thead>
  <th colspan="1">命令</th>
  <th colspan="1">执行的操作</th>
  </thead>
  <tbody>
  <tr>
  <td>--file FILE_NAME</td>
  <td>存储有关环境的详细信息的 JSON 文件。<p>
  <p>示例 JSON：
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
  
  请注意返回的 `ID` 值。`ID` 是为环境指定的唯一标识，会在后续命令中使用。
  
3. 运行 `plan` 命令以预览环境将如何更改。plan 命令显示哪些资源将更改，以及相对于已部署的资源将更改的数量，但更改要到运行 `apply` 命令后才会生效。
  
  ```
  bx schematics action plan --id ENVIRONMENT_ID
  ```
  {: codeblock}
  
  <table summary="plan 命令的描述。">
  <caption>表 2. plan 命令的描述。</caption>
  <thead>
  <th colspan="1">命令</th>
  <th colspan="1">执行的操作</th>
  </thead>
  <tbody>
  <tr>
  <td>--id ENVIRONMENT_ID</td>
  <td>要对其运行执行计划的特定环境。如果需要检索环境标识的值，可以运行 <code>bx schematics list</code>。</td>
  </tbody></table>
  
  `activity_id` 会分配给计划，并在活动日志中进行记录。 

4. 检索活动日志以查看 Terraform 计划输出。

  ```
  bx schematics activity log --id ACTIVITY_ID
  ```
  {: codeblock}

  <table summary="log 命令的描述。">
  <caption>表 3. log 命令的描述。</caption>
  <thead>
  <th colspan="1">命令</th>
  <th colspan="1">执行的操作</th>
  </thead>
  <tbody>
  <tr>
  <td>--id ACTIVITY_ID</td>
  <td>要查看其日志的特定活动。如果需要检索活动标识的值，可以运行 <code>bx schematics activity list --id ENVIRONMENT_ID</code>。</td>
  </tbody></table>
  
5. 运行 `apply` 命令以将资源部署到环境。
  
  ```
  bx schematics action apply --id ENVIRONMENT_ID
  ```
  {: codeblock}
  
  <table summary="apply 命令的描述。">
  <caption>表 4. apply 命令的描述。</caption>
  <thead>
  <th colspan="1">命令</th>
  <th colspan="1">执行的操作</th>
  </thead>
  <tbody>
  <tr>
  <td>--id ENVIRONMENT_ID</td>
  <td>要将更新部署到的特定环境。如果需要检索环境标识的值，可以运行 <code>bx schematics list</code>。</td>
  </tbody></table>
  
6. 监视 apply 输出，以确保部署成功。 

  ```
  bx schematics activity log --id ACTIVITY_ID
  ```
  {: codeblock}

  如果成功部署，会在输出末尾附近返回以下行。
  
  ```
  Apply complete! Resources: N added, N changed, N destroyed.
  ```
  {: screen}
  
## 使用 API 部署到环境
{: #api}

可以使用 {{site.data.keyword.bpshort}} API 以编程方式部署环境。
{:shortdesc}

对 <a href="https://us-south.schematics.bluemix.net/swagger-api/">{{site.data.keyword.bpshort}} API <img src="../../icons/launch-glyph.svg" alt="外部链接图标"></a> 的调用将指向以下基本端点：

```
https://us-south.schematics.bluemix.net
```
{: codeblock}

### 先决条件
{: #api-prereq}

* 在源代码控制中存储 Terraform 配置。

完成以下步骤以将资源部署到环境：

1. 生成要在认证头中使用的 IAM OAuth 令牌。该命令会输出 UAA 令牌和 IAM 令牌。
  
  ```
  bx iam oauth-tokens
  ```
  {: codeblock}
  
  示例输出：
  ```
  IAM token:  Bearer eyJraWQ...
  ```
  {: screen}
    
  `Bearer eyJraWQ...` 输出是截断的 IAM 令牌示例。请在 API 调用的头中包含完整令牌。
  
2. 通过运行 `POST v1/environments` 调用来创建环境。

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
    
  成功的响应会返回以下输出。
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
    
  请注意返回的 `id` 值。`id` 是为环境指定的唯一标识，会在后续调用中使用。
  
3. 运行 `POST v1/environments/<environment_ID>/plan` 调用以预览在应用配置时将部署到环境的资源。计划会抽取存储库主分支中的环境配置。
  
  ```
  curl -X POST \
    https://us-south.schematics.bluemix.net/v1/environments/<environment_ID>/plan \
    -H 'accept: application/json' \
    -H 'authorization: bearer <IAM_token>' \
    -H 'content-type: application/json'
  ```
  {: codeblock}
  
  成功的响应会返回 `activityid`。需要活动标识值才可查看日志，例如 plan 和 apply 输出。
  ```
  {
    "activityid": "<activity_ID>"
  }
  ```
  {: screen}

4. 运行 `GET v1/environments/<environment_ID>/activities/<activity_ID>/log` 调用以查看 plan 输出。

  ```
  curl -X GET \
    https://us-south.schematics.bluemix.net/v1/environments/<environment_ID>/activities/<activity_ID>/log \
    -H 'accept: text/html' \
    -H 'authorization: bearer <IAM_token>'
  ```
  {: codeblock}

5. 通过运行 `PUT v1/environments/<environment_ID>/apply/` 调用以部署环境。
  
  ```
  curl -X PUT \
    https://us-south.schematics.bluemix.net/v1/environments/<environment_ID>/apply \
    -H 'accept: application/json' \
    -H 'authorization: bearer <IAM_token>' \
    -H 'content-type: application/json'
  ```
  {: codeblock}
  
6. 通过运行 `GET v1/environments/<environment_ID>/activities/<activity_ID>/log` 调用以查看 apply 输出，从而监视部署。

  ```
  curl -X GET \
    https://us-south.schematics.bluemix.net/v1/environments/<environment_ID>/activities/<activity_ID>/log \
    -H 'accept: text/html' \
    -H 'authorization: bearer <IAM_token>'
  ```
  {: codeblock}

  如果成功部署，会在输出末尾附近返回以下行。
  
  ```
  Apply complete! Resources: N added, N changed, N destroyed.
  ```
  {: screen}
