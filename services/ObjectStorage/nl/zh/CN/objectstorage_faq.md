---

copyright:
  years: 2014, 2016

---
{:new_window: target="_blank"}
{:shortdesc: .shortdesc}

# 常见问题 {: #faq}

*上次更新时间：2016 年 10 月 19 日*
{: .last-updated}

此常见问题提供了对 {{site.data.keyword.objectstorageshort}} 服务相关常见问题的解答。
{: shortdesc}


## 对于 {{site.data.keyword.objectstorageshort}}，我可以使用哪些帐户和付款套餐？ {: #account-payment}

{{site.data.keyword.objectstorageshort}} 服务提供了两个套餐选项：免费和标准。[定价](https://console.ng.bluemix.net/pricing/)根据所选套餐而变化。

<table>
  <tr>
    <th> 免费套餐</th>
    <th> 标准套餐</th>
  </tr>
  <tr>
    <td> 同一时间只允许 {{site.data.keyword.Bluemix_notm}} 组织中存在一个服务实例</td>
    <td> 服务实例数不限</td>
  </tr>
  <tr>
    <td> 所有人可用</td>
    <td> 仅 {{site.data.keyword.Bluemix_notm}} 付费帐户和 IBM 内部用户可用</td>
  </tr>
  <tr>
    <td> 免费</td>
    <td> 现买现付或预订付费套餐</td>
  </tr>
  <tr>
    <td> 包含入门级 5 GB 存储使用限制</td>
    <td> 存储量不限</td>
  </tr>
</table>

*表 1：免费套餐与标准套餐的比较*

**注意**：使用 {{site.data.keyword.Bluemix_notm}} 试用帐户的用户可以使用免费套餐。在试用时间到期后，将禁用关联的 {{site.data.keyword.objectstorageshort}} 服务实例，就是说您将无法访问存储帐户。30 天后，将清除 {{site.data.keyword.Bluemix_notm}} 帐户，并且删除所有数据。要避免数据丢失，请尽快升级到[付费 {{site.data.keyword.Bluemix_notm}} 帐户](https://new-console.ng.bluemix.net/docs/admin/account.html)。

## 如何更改套餐？ {: #changeplan}  
在 Beta 或免费套餐中创建的实例可以升级到标准套餐。关联的组织必须为 {{site.data.keyword.Bluemix_notm}} 付费帐户。具有 Object Storage 实例的试用帐户无法升级到标准套餐，而标准套餐上的实例也无法降级到其他套餐。升级时，服务实例和客户数据将迁移到新套餐。

要升级，请执行以下操作：
1.	在 {{site.data.keyword.objectstorageshort}} 用户界面中，单击**套餐**。
2.	选择**标准**作为新套餐，然后单击**保存**。

还可以使用命令行界面来[更改付费套餐](../../pricing/index.html#changing)。

## 使用 {{site.data.keyword.objectstorageshort}} 如何计费和收费？ {: #charge-bill}

{{site.data.keyword.objectstorageshort}} 服务仅按使用内容收费。要开始使用此服务，无需支付设置费或保证金。也无需为 API 请求或入站数据网络流量付费。

{{site.data.keyword.objectstorageshort}} 计费的依据是在整个计费周期内的存储使用量。这包括在 {{site.data.keyword.Bluemix_notm}} 组织内创建的容器中的所有对象数据。

出站数据传输收费适用于通过公用网络从您的任何对象容器中读取数据的情况。在计费周期内使用的所有带宽都会计入“公共出站带宽”。

在计费周期结束后，{{site.data.keyword.Bluemix_notm}} 将对该计费周期内的使用量进行自动计费。您可以通过 {{site.data.keyword.Bluemix_notm}} 报告查看当前计费周期的费用。
