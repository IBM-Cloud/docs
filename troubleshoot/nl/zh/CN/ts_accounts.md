---

copyright:
  years: 2015, 2017
  
lastupdated: "2017-01-10"

---

{:tsSymptoms: .tsSymptoms} 
{:tsCauses: .tsCauses} 
{:tsResolve: .tsResolve} 
{:new_window: target="_blank"}  
{:shortdesc: .shortdesc}
{:codeblock: .codeblock} 


# 有关管理帐户的故障诊断
{: #managingaccounts}

管理帐户会发生的一般问题可能包括不同的应用程序共享同一域名或管理员无法查看所有组织。在许多情况下，只需执行几个简单的步骤即可解决这些问题。
{:shortdesc}


## 帐户不活动
{: #ts_accnt_inactive}

如果您的帐户处于不活动状态，那么无法在 {{site.data.keyword.Bluemix_notm}} 中创建应用程序。必须联系支持团队来解决此问题。

尝试在 {{site.data.keyword.Bluemix_notm}} 中创建应用程序时，您会看到以下错误消息：
{: tsSymptoms} 

`BXNUI0096E: 未创建应用程序。您的帐户处于不活动状态，因为它已被取消或暂挂。`

当您的 {{site.data.keyword.Bluemix_notm}} 帐户被取消或暂挂时，其状态会变为不活动。
{: tsCauses}


要重新激活您的帐户，请联系 [{{site.data.keyword.Bluemix_notm}} 支持 ![外部链接图标](../icons/launch-glyph.svg "外部链接图标")](http://ibm.biz/bluemixsupport.com){: new_window}。请在电子邮件中包含以下信息：
{: tsResolve}

  * 您用于登录到 {{site.data.keyword.Bluemix_notm}} 的 IBM 标识。
  * 要在其中创建应用程序的组织的名称。此信息可帮助支持团队确定在您组织内是否为您分配了正确的角色或成员资格。


## 没有空间与当前组织关联
{: #ts_no_space}

如果没有空间与您的当前组织关联，那么无法创建应用程序。

尝试在 {{site.data.keyword.Bluemix_notm}} 中创建应用程序时，您会看到以下错误消息：
{: tsSymptoms} 

`BXNUI0097E: 在添加应用程序之前，必须至少有一个空间与您的组织和区域相关联。在“仪表板”上，单击“创建空间”。创建空间后，请重试。`

{{site.data.keyword.Bluemix_notm}} 中的应用程序必须在组织下的空间内创建。
{: tsCauses} 

要创建空间，请使用以下某种方法： 
{: tsResolve}
 
  * 在 {{site.data.keyword.Bluemix_notm}}“仪表板”上，选择要在其中创建空间的组织，然后单击**创建空间**。
  * 在 cf 命令行界面中，键入 `cf create-space <space_name> -o <organization_name>`。

  
## 应用程序共享相同的域名
{: #ts_domain_diff}

您可能注意到数个应用程序在 {{site.data.keyword.Bluemix_notm}} 中共享同一 URL。

当您为空间内的不同应用程序分配相同 URL 路径时，可能会发生此问题。
{: tsCauses}

例如，将 myApp1 应用程序推送到 {{site.data.keyword.Bluemix_notm}}，并将域设置为“mynewapp.stage1.mybluemix.net”。然后，将另一个应用程序 myApp2 推送到同一空间，并将该应用程序的其中一个 URL 路径设置为“mynewapp.stage1.mybluemix.net”。现在，该路径映射到两个应用程序。

此行为受 {{site.data.keyword.Bluemix_notm}} 支持，您可以使用这一做法来杜绝应用程序升级时的停机状况。有关更多信息，请参阅 [Using Blue-Green Deployment to Reduce Downtime and Risk ![外部链接图标](../icons/launch-glyph.svg "外部链接图标")](https://docs.cloudfoundry.org/devguide/deploy-apps/blue-green.html){: new_window}。
{: tsResolve}
  

## 管理员无法使用 {{site.data.keyword.Bluemix_notm}} 用户界面查看所有组织
{: #ts_ui_org}

作为管理员，使用 {{site.data.keyword.Bluemix_notm}} 用户界面时，无法显示要管理的每一个组织。您仅可以显示和管理您所属的那些组织。

作为管理员，您无法使用 {{site.data.keyword.Bluemix_notm}} 用户界面查看所有组织。
{: tsSymptoms}

这是 {{site.data.keyword.Bluemix_notm}} 用户界面的限制。
{: tsCauses}

您可以通过 cf 命令行界面，使用命令（如 `cf orgs`、`cf create-org` 和 `cf delete-org`）来管理所有组织。要想获取 cf 命令的完整清单，请输入 `cf help`。
{: tsResolve}
	
## 无法添加信用卡
{: #ts_addcc}

无法提交信用卡信息以将试用帐户转换为“现买现付”帐户。

“添加信用卡”页面上的**提交**按钮已禁用。
{: tsSymptoms}

在“添加信用卡”页面中未正确填写您的信息时会发生此问题。
{: tsCauses}


请完成以下步骤：
{: tsResolve}

  1. 在“添加信用卡”页面上，填写联系人信息、联系人地址和帐单地址部分中的所有必填字段。
  2. 选择**我已阅读并同意 IBM 条款和条件**，然后单击**提交**。此时将显示**选择付款方式**部分。
  3. 输入您的信用卡卡号、信用卡到期日期以及信用卡上的安全代码。然后，单击**提交**。
