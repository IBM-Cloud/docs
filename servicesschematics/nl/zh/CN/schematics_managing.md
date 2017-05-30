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

# 管理环境中的资源
{: #managing}

{{site.data.keyword.bplong}} 简化了环境管理。您可以修改已部署的资源，并根据需要反复重新部署更改。

{:shortdesc}

对环境的更改可以通过一个轻量级进程进行部署。如果希望更改分配哪些资源，可使用声明式语法对配置更改编写代码，即仅声明所需的结果。使用 {{site.data.keyword.bpshort}}，可以在部署前预览更改。


## 使用 GUI 更新资源
{: #gui}

如果更希望使用图形视图来管理环境中的资源，那么可以使用 {{site.data.keyword.bpshort}} 仪表板。
{:shortdesc}

在 GitHub 中发布了对配置的代码更改或在 GUI 中修改了变量后，请完成以下步骤来将更新部署到环境：

1. 在 **{{site.data.keyword.bpshort}}** 仪表板中，选择**环境**。

2. 单击要更新的特定环境所在的行。

3. 单击**计划**并检查计划日志中是否有错误。环境会一直锁定，直到您或您 {{site.data.keyword.Bluemix_notm}} 帐户中的合作者应用计划或将其取消为止。 

4. 单击**应用**以部署更新。 


## 使用 CLI 更新资源
{: #cli}

可以使用 {{site.data.keyword.bpshort}} CLI 通过编程方式更新环境中的资源。
{:shortdesc}

在 GitHub 中发布了对配置的代码更改后，请完成以下步骤来将更新部署到环境：

1. 运行 `plan` 命令。{{site.data.keyword.bpshort}} CLI 会从 GitHub 中拉取更新的环境配置，并输出预览以显示资源相对于当前部署有哪些不同。

  ```
  bx schematics action plan --id ENVIRONMENT_ID
  ```
  {: codeblock}

2. 查看活动日志中的计划输出。

  ```
  bx schematics activity log --id ACTIVITY_ID
  ```
  {: codeblock}

3. 通过运行 `apply` 命令部署计划。 

  ```
  bx schematics action apply --id ENVIRONMENT_ID
  ```
  {: codeblock}


## 使用 API 更新资源
{: #api}

可以使用 {{site.data.keyword.bpshort}} API 通过编程方式管理环境中的资源。
{:shortdesc}

在 GitHub 中发布了对配置的代码更改后，请完成以下步骤来将更新部署到环境：

1. 运行 `POST v1/environments/<environment_ID>/plan` 调用。{{site.data.keyword.bpshort}} API 会从 GitHub 中拉取更新的环境配置，并将其与 Terraform 状态文件进行比较，以显示资源相对于当前部署有哪些不同。

  ```
  curl -X POST \
    https://us-south.schematics.bluemix.net/v1/environments/<environment_ID>/plan \
    -H 'accept: application/json' \
    -H 'authorization: bearer <IAM_token>' \
    -H 'content-type: application/json'
  ```
  {: codeblock}

  示例响应：
  ```
  {
    "activityid": "<activity_ID>"
  }
  ```
  {: screen}

2. 查看活动日志中的计划输出。

  ```
  curl -X GET \
    https://us-south.schematics.bluemix.net/v1/environments/<environment_ID>/activities/<activity_ID>/log \
    -H 'accept: text/html' \
    -H 'authorization: bearer <IAM_token>'
  ```
  {: codeblock}

3. 通过运行 `PUT /v1/environments/<environment_ID>/apply` 调用以部署计划。 

  ```
  curl -X PUT \
    https://us-south.schematics.bluemix.net/v1/environments/<environment_ID>/apply \
    -H 'accept: application/json' \
    -H 'authorization: bearer <IAM_token>' \
    -H 'content-type: application/json' \
  ```
  {: codeblock}


## 审计对环境的更改
{: #auditing}

可以在源代码控制存储库的版本历史记录中对配置进行审计。为了监视对环境的部署或查看先前部署的日志，{{site.data.keyword.bpshort}} 提供了以下选项用于查看审计日志。

### 在 {{site.data.keyword.bpshort}} 仪表板中
{: #auditing-gui}

1. 选择环境所在的行以访问环境详细信息页面。

2. 监视**最近的活动**部分。还可以查看先前计划和部署的历史日志。

### 使用 {{site.data.keyword.bpshort}} CLI
{: #auditing-cli}

1. 检索环境标识。

  ```
  bx schematics environment list
  ```
  {: codeblock}

2. 检索环境的活动标识。会为 plan、apply、destroy 和 delete 操作分配活动标识。以下命令会列出对环境运行的所有活动。

  ```
  bx schematics activity list --id ENVIRONMENT_ID
  ```
  {: codeblock}

3. 检索有关特定活动的数据，例如谁对环境进行了更改以及何时进行的更改。

  ```
  bx schematics activity show --id ACTIVITY_ID
  ```
  {: codeblock}

4. 可选：要查看详细日志（例如 plan 或 apply 输出），请运行 `log` 命令。 

  ```
  bx schematics activity log --id ACTIVITY_ID
  ```
  {: codeblock}

### 使用 {{site.data.keyword.bpshort}} API
{: #auditing-api}

1. 检索环境标识。

  ```
  curl -X GET \
    https://us-south.schematics.bluemix.net/v1/environments \
    -H 'accept: application/json' \
    -H 'authorization: bearer <IAM_token>'
  ```
  {: codeblock}
  
  响应主体包含您 {{site.data.keyword.Bluemix_notm}} 帐户中的所有环境。找到要审计的特定环境的 `id` 值。

2. 检索对环境运行的操作的活动标识。

  ```
  curl -X GET \
    https://us-south.schematics.bluemix.net/v1/environments/<environment_ID>/activities \
    -H 'accept: application/json' \
    -H 'authorization: bearer <IAM_token>'
  ```
  {: codeblock}

3. 获取对环境执行的特定活动。 

  ```
  curl -X GET \
    https://us-south.schematics.bluemix.net/v1/environments/<environment_ID>/activities/<activity_ID> \
    -H 'accept: application/json' \
    -H 'authorization: bearer <IAM_token>'
  ```
  {: codeblock}

4. 检查 Terraform 输出的详细日志。

  ```
  curl -X GET \
    https://us-south.schematics.bluemix.net/v1/environments/<environment_ID>/activities/<activity_ID>/log \
    -H 'accept: text/html' \
    -H 'authorization: bearer <IAM_token>'
  ```
  {: codeblock}
