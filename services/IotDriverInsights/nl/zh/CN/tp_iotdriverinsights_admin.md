---

copyright:
  years: 2016

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}

# 管理轨迹模式分析
{: #tp_iotdriverinsights_admin}

上次更新时间：2016 年 7 月 22 日
{: .last-updated}

要管理“轨迹模式分析”服务，请使用 {{site.data.keyword.Bluemix_notm}} 仪表板上的管理控制台。从管理控制台，您可以配置“轨迹模式分析”的参数，并管理存储在服务中的数据。您还可以查看租户信息并重置租户密码。

{:shortdesc}

## 启动管理控制台
{: #start-admin-console}

要访问 {{site.data.keyword.iotdriverinsights_full}} 的“轨迹模式分析”服务的管理控制台

1. 在 {{site.data.keyword.Bluemix_notm}} 仪表板上，单击 {{site.data.keyword.iotdriverinsights_short}} 服务磁贴。
2. 选择服务实例的**管理**视图。记下用户名和密码凭证，因为之后您需要这些凭证。要访问管理控制台，需要 IBM 标识，该标识可能与 {{site.data.keyword.Bluemix_notm}} 凭证不同。
3. 单击**启动**，系统提示时，输入 IBM 标识凭证。
4. 单击**登录**。**管理控制台**窗口即会打开。


## 管理租户信息
{: #viewtenantinfo}

要查看租户信息，请单击**租户信息**。

### 重置租户密码
{: #resettenantpassword}

要重置租户密码：

1. 从**租户信息**窗口中，单击**重置**。
2. 在确认对话框中单击**确定**。此时将在**租户信息**视图中生成并显示新密码。
**重要信息：**确保在访问 {{site.data.keyword.iotdriverinsights_short}} API 的所有应用程序中都更新密码。

## 配置服务参数
{: #configureparameters}

服务参数会控制如何分析行程数据。要修改“轨迹模式分析”服务参数：

1. 打开**参数**视图。
2. 单击**轨迹模式的参数**选项卡，并更新[轨迹模式分析参数](#tp_parameters)，以符合您的需求。
3. 单击**保存**。
4. 单击**确定**。

更新的参数值即会应用到所提交的下一个作业。

### 支持阈值参数

下表描述可以在**轨迹模式的参数**选项卡上配置的支持阈值参数。

|参数名称|描述|缺省值|
|:--------|:--------|:-------|
|O/D 的最小支持行程数|O/D（始发地/目的地）模式所需的最小绝对支持行程数|4（必须大于零）|
|路线的最小支持行程数|路线模式所需的最小绝对支持行程数|2（必须大于零）|

## 管理结果数据
{: #managedata}

在您删除“轨迹模式分析”服务的分析所生成的结果数据之前，这些数据存储在系统中。

要删除结果数据：

1. 单击**数据管理** > **轨迹模式的结果**。此时将显示结果数据。
2. 选择记录，然后单击**删除**。
