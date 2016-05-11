---

copyright:
  years: 2015, 2016

---


{:tsSymptoms: .tsSymptoms} 
{:tsCauses: .tsCauses} 
{:tsResolve: .tsResolve} 
{:new_window: target="_blank"}  
{:shortdesc: .shortdesc}

# SendGrid 故障诊断
{: #ts_sendgrid}

*上次更新时间：2015 年 12 月 9 日*

以下是关于在 {{site.data.keyword.Bluemix}} 中使用 SendGrid 的问题解答。
{:shortdesc}


## 无法使用 SendGrid 发送电子邮件
{: #ts_sendgrid_email}

如果无法使用 SendGrid 服务发送电子邮件，那么可能是因为已达到每个服务实例所允许的电子邮件数限制。
{:shortdesc}


如果所发送的电子邮件数达到所允许的最大电子邮件数，那么就无法再使用 SendGrid 服务发送更多电子邮件。
{: tsSymptoms}


使用 SendGrid 服务发送电子邮件时，每月每个服务实例只能发送 25,000 封电子邮件。达到该限制后，SendGrid 会停止发送电子邮件，而且使用此服务将不会发生进一步的费用。
{: tsCauses}

要检查剩余的允许发送电子邮件数，请从 {{site.data.keyword.Bluemix_notm}}“仪表板”单击 SendGrid 服务实例，然后单击**打开 SENDGRID 仪表板**。在**剩余信用值**字段中，可以查看该数量。


在达到每个月每个服务实例 25,000 个电子邮件的限制之后，如果您还要发送更多电子邮件，那么可以添加另一个服务实例。有关 SendGrid 的更多信息，请参阅 [Getting Started with SendGrid](https://sendgrid.com/docs/index.html){: new_window}。    
{: tsResolve}

