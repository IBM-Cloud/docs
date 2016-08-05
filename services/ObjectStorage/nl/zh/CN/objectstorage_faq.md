{:new_window: target="_blank"}

# 常见问题 {: #faq} 

*上次更新时间：2016 年 7 月 18 日*
{: .last-updated}


## 价格是如何根据所选套餐变化的？ {: #plan-price}
定价根据所选套餐而变化。有关更多定价信息，请参阅 [IBM Bluemix 价格表](https://console.ng.bluemix.net/pricing/){: new_window}或使用[计算器](https://console.ng.bluemix.net/?direct=classic/#/pricing/cloudOEPaneId=pricing&paneId=pricingSheet){: new_window}，以获取更详细的估算。


## 对于 {{site.data.keyword.objectstorageshort}}，我可以使用哪些帐户和付款套餐？ {: #account-payment}
{{site.data.keyword.objectstorageshort}} 服务随附多个套餐选项。自一般可用性发行版以来，目前提供两种套餐：标准套餐和免费套餐。标准套餐只适用于 {{site.data.keyword.Bluemix_notm}} 付费帐户（即现买现付或预订帐户）和 IBM 内部用户。标准套餐包括每一个帐户存储使用量入门级 5 GB 免费信用额度。

仍有效的试用帐户可以使用免费套餐，免费套餐只允许 {{site.data.keyword.Bluemix_notm}} 组织中存在一个实例。在 {{site.data.keyword.Bluemix_notm}} 试用时间到期后，将禁用关联的 {{site.data.keyword.objectstorageshort}} 服务实例，即无法通过 {{site.data.keyword.Bluemix_notm}} 用户界面或命令行来访问存储帐户。在 30 天宽限期后，将清除 {{site.data.keyword.Bluemix_notm}} 帐户，并且删除所有数据。要避免数据丢失，建议尽快升级到 {{site.data.keyword.Bluemix_notm}} 付费帐户。要升级帐户，请单击用户管理菜单，然后选择**帐户**，这将提供有关升级过程的指示信息。

## 如何更改套餐？ {: #changeplan}  
在 Beta 或免费套餐中创建的实例可以升级到标准套餐。关联的组织必须为 {{site.data.keyword.Bluemix_notm}} 付费帐户。具有 {{site.data.keyword.objectstorageshort}} 实例的试用帐户无法升级到标准套餐，而标准套餐上的实例也无法降级到其他套餐。升级时，服务实例和客户数据将迁移到新套餐。

要升级套餐：
1.	在 {{site.data.keyword.objectstorageshort}} 用户界面中，单击**套餐**。
2.	选择**标准**作为新套餐，然后单击**保存**。

还可以使用命令行界面来更改付款套餐。有关更多信息，请参阅[如何更改套餐](../../pricing/index.html#changing)。


## 使用 {{site.data.keyword.objectstorageshort}} 如何计费和收费？ {: #charge-bill}

{{site.data.keyword.objectstorageshort}} 服务仅按使用内容收费。要开始使用此服务，无需支付最低费用、设置费或保证金。无需为 API 请求或入站数据网络流量付费。

按 {{site.data.keyword.objectstorageshort}} 使用量计费的依据是在整个计费周期内存储使用量。包括在 {{site.data.keyword.Bluemix_notm}} 组织帐户下创建的容器中的所有对象数据。 

出站数据传输收费适用于通过公用网络从您的任何对象容器中读取数据的情况。公用出站带宽的计费是针对计费周期内耗用的所有带宽。

{{site.data.keyword.objectstorageshort}} 定价的度量组件如下所示：
* 存储使用量  - $0.04/GB/月
* 公共出站数据传输  - $0.09/GB/月 

在计费周期结束后，{{site.data.keyword.Bluemix_notm}} 将对当前计费周期的使用量进行自动计费。您可以通过 {{site.data.keyword.Bluemix_notm}} 报告查看当前计费周期的费用。

为伦敦和达拉斯发布的标准服务套餐定价相同。

## 在 {{site.data.keyword.objectstorageshort}} 中如何执行数据复制？ {: #replication}
{{site.data.keyword.objectstorageshort}} 服务从多个存储节点复制数据并维护这些数据的三个副本。有关更多信息，请参阅 [OpenStack Swift 复制](http://docs.openstack.org/developer/swift/overview_replication.html){: new_window}文档。

