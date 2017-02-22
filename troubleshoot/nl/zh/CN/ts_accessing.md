---

copyright:
  years: 2015, 2017
  
lastupdated: "2017-01-11"

---

{:tsSymptoms: .tsSymptoms} 
{:tsCauses: .tsCauses} 
{:tsResolve: .tsResolve} 
{:new_window: target="_blank"}  
{:shortdesc: .shortdesc}
{:codeblock: .codeblock} 



# 有关访问 {{site.data.keyword.Bluemix_notm}} 的故障诊断 
{: #accessing}


访问 {{site.data.keyword.Bluemix}} 的一般性问题可能包括用户无法登录到 {{site.data.keyword.Bluemix_notm}} 和帐户困于暂挂状态等。然而，在许多情况下，只需执行几个简单的步骤即可解决这些问题。
{:shortdesc}

## 无法登录到 {{site.data.keyword.Bluemix_notm}}
{: #ts_unabletologin}

您必须具有有效的 {{site.data.keyword.Bluemix_notm}} 帐户才能登录。


在尝试登录到 {{site.data.keyword.Bluemix_notm}} 时，您看到以下其中一条错误消息：
{: tsSymptoms} 

 * 在客户门户网站中
  
   `由于认证成功，您已位于此页面中，但是此 IBM 标识未与任何 IBM Cloud 帐户关联。如果您认为这是错误，请联系帐户所有者或主用户。`

 * 在 {{site.data.keyword.Bluemix_notm}} 控制台中
  
  `由于认证成功，您已位于此页面中，但是此 IBM 标识未与任何 {{site.data.keyword.Bluemix_notm}} 帐户关联。`


最有可能导致收到此错误消息的一个原因是，您尚未创建 {{site.data.keyword.Bluemix_notm}} 帐户，或者您需要切换到 IBM 标识认证。
{: tsCauses} 
 

执行注册流程以创建 {{site.data.keyword.Bluemix_notm}} 帐户，或者联系主用户或帐户管理员来切换到 IBM 标识。
{: tsResolve}

根据帐户的设置方式，下面的一些登录选项可能适用： 
 * 使用 SoftLayer 标识的 SoftLayer 用户必须通过[客户门户网站 ![外部链接图标](../icons/launch-glyph.svg)](https://control.softlayer.com){: new_window} 登录。
 * 使用 IBM 标识且具有或不具有链接 Bluemix 帐户的 SoftLayer 用户可以通过[客户门户网站 ![外部链接图标](../icons/launch-glyph.svg)](https://control.softlayer.com){: new_window} 登录来打开 SoftLayer 客户门户网站，也可以通过 [Bluemix 控制台 ![外部链接图标](../icons/launch-glyph.svg)](https://console.{DomainName}){: new_window} 登录来打开“基础架构”仪表板。 
 * 没有链接 SoftLayer 帐户的 Bluemix 用户必须通过 Bluemix 控制台登录。
 * 具有链接 SoftLayer 帐户的 Bluemix 用户可以通过 [Bluemix 控制台 ![外部链接图标](../icons/launch-glyph.svg)](https://console.{DomainName}){: new_window} 或[客户门户网站 ![外部链接图标](../icons/launch-glyph.svg)](https://control.softlayer.com){: new_window} 登录。
 

## 密码无效
{: #ts_logintobm}

您必须具有有效的 IBM 标识才能登录到 {{site.data.keyword.Bluemix_notm}} 控制台。

在尝试登录到 {{site.data.keyword.Bluemix_notm}} 时，您看到以下错误消息：
{: tsSymptoms} 

`输入的密码不正确。`

用于登录到 {{site.data.keyword.Bluemix_notm}} 的 IBM 标识和密码无效。
{: tsCauses} 
 
要获取有效的 IBM 标识和密码，请转至“我的 IBM 个人档案”页面，然后完成以下某个步骤：
{: tsResolve}
  * 如果已注册 IBM 标识并且想要检查标识和密码是否有效，请单击**登录**，并在“登录”页面中输入 IBM 标识和密码。如果忘记密码，请单击“登录”页面上的**忘记密码**以重置密码。如果忘记 IBM 标识或密码问题仍未解决，请联系全球 IBM 注册帮助台来获取帮助。 
  * 如果没有 IBM 标识，请单击**注册**以注册 IBM 标识和密码。 



## 无法使用 SoftLayer 用户名登录
{: #ts_softlayer_username}

您必须具有有效的 IBM 标识和密码才能登录到 {{site.data.keyword.Bluemix_notm}}。


尝试使用 SoftLayer 用户名登录到 {{site.data.keyword.Bluemix_notm}} 控制台时，收到以下消息：
{: tsSymptoms} 

`无法识别此 IBM 标识或电子邮件。`

您必须通过 IBM 标识登录才能使用 Bluemix 控制台中的“基础架构”仪表板。
{: tsCauses} 
 
如果您是使用 SoftLayer 标识的 SoftLayer 用户，那么必须切换到客户门户网站以在您有权访问的每个帐户内进行 IBM 认证，然后才能使用 IBM 标识认证进行登录。 

联系主用户或帐户管理员来切换到 IBM 标识。
{: tsResolve}



## 您有未保存的更改
{: #ts_unsaved_changes}


在应用程序详细信息页面上进行浏览时，可能无法执行任何操作，系统可能会提示您保存更改后才能继续。 


在应用程序详细信息页面上尝试检查应用程序或服务时，总是提示以下错误消息：
{: tsSymptoms} 

`您在页面 app_name 中有未保存的更改。请保存或取消这些更改。`


在运行时窗格中的**实例**或**内存配额**字段上滚动鼠标时，值会更改。这是故意这样设计的；但是，当您要离开该页面时，会有错误消息提示您保存内存或实例设置。
{: tsCauses}


关闭消息窗口，然后单击运行时窗格中的**重置**按钮。
{: tsResolve} 

  
    
## {{site.data.keyword.Bluemix_notm}} 区域之间的自动故障转移不可用
{: #ts_failover}

无法使用 {{site.data.keyword.Bluemix_notm}} 区域之间的自动故障转移。但可以使用支持多个 IP 地址间故障转移的 DNS 提供程序来作为变通方法。
 

当某个 {{site.data.keyword.Bluemix_notm}} 区域变为不可用时，在该区域运行的应用程序也不可用，即使在另一个 {{site.data.keyword.Bluemix_notm}} 区域中有相同的应用程序正在运行，也是如此。
{: tsSymptoms}

 
{{site.data.keyword.Bluemix_notm}} 尚不提供从一个区域到另一个区域的自动故障转移。
{: tsCauses}

 
您可以使用支持多个 IP 地址间智能故障转移的 DNS 提供程序，并手动配置 DNS 设置，以启用 {{site.data.keyword.Bluemix_notm}} 区域之间的自动故障转移。具有此功能的 DNS 提供程序包括 NSONE、Akamai 和 Dyn。
{: tsResolve}

配置 DNS 设置时，必须指定应用程序运行所在 {{site.data.keyword.Bluemix_notm}} 区域的公共 IP 地址。要获取 {{site.data.keyword.Bluemix_notm}} 区域的公共 IP 地址，请使用 `nslookup` 命令。例如，可以在命令行窗口中键入以下命令：
```
nslookup stage1.mybluemix.net
```



## 帐户暂挂
{: #ts_accntpding}

如果帐户暂挂，那么无法登录到 {{site.data.keyword.Bluemix_notm}}。

 
在注册 {{site.data.keyword.Bluemix_notm}} 试用帐户后，可能无法登录到 {{site.data.keyword.Bluemix_notm}}。相反，会看到以下消息：
{: tsSymptoms}

<code>帐户暂挂。请等待最多 24 小时以获取电子邮件确认并请检查垃圾邮件文件夹。如果仍未收到确认电子邮件，请联系 <a href="http://ibm.biz/bluemixsupport.com" target="_blank">Bluemix 支持 <img src="../icons/launch-glyph.svg" alt="外部链接图标"></a>。</code>



在注册 {{site.data.keyword.Bluemix_notm}} 试用帐户后，您将收到确认电子邮件。必须单击确认电子邮件中的链接以完成注册过程。
{: tsCauses} 

确认电子邮件将发送到提供的电子邮件地址。请检查收件箱和垃圾邮件文件夹。如果未收到确认电子邮件，请联系 [{{site.data.keyword.Bluemix_notm}} 支持 ![外部链接图标](../icons/launch-glyph.svg)](http://ibm.biz/bluemixsupport.com){: new_window}。  
{: tsResolve}



## 无法向组织添加用户
{: #ts_adduser}

您可以邀请多个用户在同一组织下工作。只有帐户所有者或组织管理员兼组织成员，才能邀请用户加入组织。
 

在**管理组织**部分中看不到**邀请新用户**链接。 
{: tsSymptoms}

 

只有以下 {{site.data.keyword.Bluemix_notm}} 用户才能邀请用户加入组织：
{: tsCauses}
  * 组织的帐户所有者
  * 组织管理员兼组织成员，而不是组织的合作者
  
在 {{site.data.keyword.Bluemix_notm}} 中，您可以是组织的成员，也可以是组织的合作者：

<dl><dt>合作者</dt>
<dd>如果您已有 {{site.data.keyword.Bluemix_notm}} 帐户，并且有其他人邀请您加入组织，那么您就是组织的合作者。</dd>
<dt>成员</dt>
<dd>如果您没有 {{site.data.keyword.Bluemix_notm}} 帐户，但有人邀请您加入组织，并且您通过邀请注册了 {{site.data.keyword.Bluemix_notm}}，那么您就是组织的成员。</dd>
</dl>


如果您是组织的合作者，即使被指定为组织管理员，也不能邀请用户加入组织。

**注：**所有组织管理员（包括组织的合作者）都可以添加、修改和除去组织中的已有用户。

 

如果您无法邀请用户加入组织，并需要其他角色来完成此操作，请联系组织管理员来更改您的角色。要识别组织管理员，请完成以下步骤：
{: tsResolve}

  1. 转至 {{site.data.keyword.Bluemix_notm}} 仪表板。在菜单栏中，单击**支持**菜单项，然后单击**管理组织**。
  2. 转至您的组织，并查看**用户**选项卡上的组织管理员信息。  
  
如果由于您是合作者（并非成员）而无法邀请用户，那么您必须删除您先前的 {{site.data.keyword.Bluemix_notm}} 帐户，然后被邀请以组织成员身份加入帐户。要删除您先前的帐户并以成员身份加入帐户，请完成以下步骤： 

  1. 联系 [{{site.data.keyword.Bluemix_notm}} 支持 ![外部链接图标](../icons/launch-glyph.svg)](http://ibm.biz/bluemixsupport){: new_window}，以开具一个支持凭单，请求删除您的帐户。如果存在与旧帐户相关联的数据并且想要将其保存并移动到新帐户，请在您的电子邮件中包含此信息。 
  2. 在您的帐户被删除后，让具有组织管理员角色的用户以组织管理员身份邀请您加入组织。然后，通过邀请注册 {{site.data.keyword.Bluemix_notm}}。 




## 不支持用户批量注册
{: #ts_batchregistration}

在对 {{site.data.keyword.Bluemix_notm}} 注册用户时，必须单独注册每个用户。
 

{{site.data.keyword.Bluemix_notm}} 不提供同时注册多个用户的功能。
{: tsSymptoms}
 

{{site.data.keyword.Bluemix_notm}} 不支持用户批量注册。要对 {{site.data.keyword.Bluemix_notm}} 注册用户，必须单独注册每个用户。
{: tsCauses}
 

要对 {{site.data.keyword.Bluemix_notm}} 注册多个用户，必须为每个用户完成以下步骤：
{: tsResolve}

  1. 在 {{site.data.keyword.Bluemix_notm}} 控制台中单击**注册**。
  2. 按照向导的提示完成每个步骤。

    

## 无法装入 {{site.data.keyword.Bluemix_notm}} 页面
{: #ts_err}

在使用 {{site.data.keyword.Bluemix_notm}} 控制台时，您可能无法装入 {{site.data.keyword.Bluemix_notm}} 页面。相反，您可能会看到错误消息 BXNUI0001E 或 BXNUI0016E。
 

在使用 {{site.data.keyword.Bluemix_notm}} 控制台时，您可能会看到以下其中一条错误消息：
{: tsSymptoms}

`BXNUI0001E: 未装入页面，因为 Bluemix 未检测到是否存在会话。`


`BXNUI0016E: 未检索到应用程序和服务，因为未装入 Bluemix 页面。`

 
您可以根据需要完成以下一个或多个操作：
{: tsResolve}

  * 刷新或重新启动浏览器。
  * 注销 {{site.data.keyword.Bluemix_notm}}，并重新登录。
  * 使用浏览器的隐私浏览模式。 
  * 清除浏览器的 cookie 和高速缓存。
  * 使用其他浏览器。有关 {{site.data.keyword.Bluemix_notm}} 支持的浏览器版本的信息，请参阅 [{{site.data.keyword.Bluemix_notm}} 先决条件 ![外部链接图标](../icons/launch-glyph.svg)](https://developer.ibm.com/bluemix/support/#prereqs){: new_window}。
  * 如果安装了 cf 命令行界面，请输入 `cf apps` 命令以查看应用程序是否正在运行。
  
  
  
  
  

