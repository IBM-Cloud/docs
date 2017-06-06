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

# 销毁临时环境中的资源
{: #destroying}

可以使用 {{site.data.keyword.bplong}} 来销毁资源。销毁资源时，会破坏环境以及所有关联的资源。  
{:shortdesc}

**警告**：销毁资源的操作不可撤销。建议不要在生产环境中销毁资源，但对于测试或 QA 之类的临时环境，此操作可能会很有用。

销毁资源之前，请考虑以下准则： 
* 确保流量未定向到您的资源。
* 确保您可能需要的任何数据均已备份。 


## 使用 GUI 销毁资源
{: #gui}

可以使用 {{site.data.keyword.bpshort}} 仪表板来启动和破坏临时环境。
{:shortdesc}

1. 在 **{{site.data.keyword.bpshort}}** 仪表板中，选择**环境**选项卡。

2. 单击要除去的特定环境所在的行。 

3. 在“选项”菜单中，选择**销毁资源**或**删除环境**。删除和销毁操作均不可撤销。要确定选择哪个选项，请考虑您是否有活动资源。
  * 如果要停止并除去活动资源，请选择**销毁资源**。建议在销毁之前先运行计划，以确认除去与环境关联的资源是否不会造成问题。
  * 如果要从 {{site.data.keyword.bpshort}} 服务中除去环境配置，请选择**删除环境**。如果环境未部署且没有活动资源，通常会使用此选项。如果在有活动资源的情况下选择此选项，那么您将无法再使用 {{site.data.keyword.bpshort}} 服务来跟踪或部署对环境的更改。活动资源需要在其服务仪表板中分别进行管理。
  
  遵循屏幕上的提示来确认选择。 


## 使用 CLI 销毁资源
{: #cli}

可以使用 {{site.data.keyword.bpshort}} CLI 来启动和破坏临时环境。
{:shortdesc}

1. 运行 `destroy` 命令以破坏您的环境和资源。

  ```
  bx schematics action destroy --id ENVIRONMENT_ID
  ```
  {: codeblock}
  
2. 可选：如果要从此服务中除去配置，请运行 `delete` 命令。

  ```
  bx schematics environment delete --id ENVIRONMENT_ID
  ```
  {: codeblock}


## 使用 API 销毁资源
{: #api}

可以使用 {{site.data.keyword.bpshort}} API 来启动和破坏临时环境。
{:shortdesc}

1. 运行 `PUT v1/environments/<environment_ID>/destroy` 调用以销毁资源。

  ```
  curl -X PUT \
    https://us-south.schematics.bluemix.net/v1/environments/<environment_ID>/destroy \
    -H 'accept: application/json' \
    -H 'authorization: bearer <IAM_token>' \
    -H 'content-type: application/json'
  ```
  {: codeblock}

2. 可选：如果要从 {{site.data.keyword.bpshort}} 服务中除去配置，请运行 `DELETE v1/environments/<environment_ID>` 调用。

  ```
  curl -X DELETE \
    https://us-south.schematics.bluemix.net/v1/environments/<environment_ID> \
    -H 'accept: text/plain' \
    -H 'authorization: bearer <IAM_token>'
  ```
  {: codeblock}
