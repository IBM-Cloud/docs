---

copyright:
  years: 2015, 2017
  
lastupdated: "2017-03-02"

---

{:tsSymptoms: .tsSymptoms} 
{:tsCauses: .tsCauses} 
{:tsResolve: .tsResolve} 
{:new_window: target="_blank"}  
{:shortdesc: .shortdesc}
{:codeblock: .codeblock} 



# 有关访问 {{site.data.keyword.Bluemix_notm}} 的故障诊断 
{: #accessing}


访问 {{site.data.keyword.Bluemix}} 的一般性问题可能包括登录到 {{site.data.keyword.Bluemix_notm}} 有问题或帐户处于暂挂状态。在许多情况下，只需执行几个简单的步骤即可解决这些问题。
{:shortdesc}

## 无法登录到 {{site.data.keyword.Bluemix_notm}}：密码不正确
{: #ts_logintobm}

您必须具有与 IBM 标识关联的有效密码才能登录到 {{site.data.keyword.Bluemix_notm}} 控制台。

您必须具有与 IBM 标识或 SoftLayer 标识关联的有效密码才能通过[客户门户网站](https://control.softlayer.com)登录。

尝试登录到 {{site.data.keyword.Bluemix_notm}} 时，显示了以下错误消息：
{: tsSymptoms} 

`输入的密码不正确。`

用于登录到 {{site.data.keyword.Bluemix_notm}} 的 IBM 标识和密码无效。
{: tsCauses} 
 
使用以下其中一种解决方案：
{: tsResolve}
 * 输入正确的密码。要检查 IBM 标识和密码是否有效，可以转至“我的 IBM 个人档案”页面，单击**登录**，并在“登录”页面中输入 IBM 标识和密码。 
 * 如果忘记密码，请单击**忘记密码**以重置密码。然后，返回到 [Bluemix 控制台](https://console.{DomainName})或[客户门户网站](https://control.softlayer.com)并重新登录。
 * 如果忘记 IBM 标识或密码问题仍未解决，请联系全球 IBM 注册帮助台来获取帮助。 
 * 要获取有效的 IBM 标识和密码，请转至“我的 IBM 个人档案”页面，然后单击**注册**。
  
**注：**如果您位于“登录到 IBM”页面上，并且登录过程出于任何原因（例如，重置密码）而中断，请返回到 [Bluemix 控制台](https://console.{DomainName})或[客户门户网站](https://control.softlayer.com)，然后重新启动登录过程。
 

## 无法登录到 {{site.data.keyword.Bluemix_notm}}：登录凭证无效
{: #ts_login_invalid_credentials}

使用 IBM 标识登录时，显示了以下消息：
{: tsSymptoms}

`提供的登录凭证无效。如果您有与帐户关联的 IBM 标识，请在此登录` 

* 您已切换到 IBM 标识，但尝试了使用先前的 SoftLayer 用户名和密码通过[客户门户网站](https://control.softlayer.com)登录。
{: tsCauses}

* 您尝试了通过[客户门户网站](https://control.softlayer.com)登录，但在“用户名”和“密码”字段中输入的是 IBM 标识和密码。 

单击消息中的**在此登录**，或转至“IBM 标识帐户登录”部分并单击**使用 IBM 标识登录**。
{: tsResolve}

不要使用用于先前 SoftLayer 标识的**用户名**和**密码**字段。


## 无法登录到 {{site.data.keyword.Bluemix_notm}}：无法识别 IBM 标识或电子邮件
{: #ts_softlayer_username}

登录到 {{site.data.keyword.Bluemix_notm}} 控制台时，显示了以下消息：
{: tsSymptoms} 

`无法识别此 IBM 标识或电子邮件。`

您尝试了登录到 {{site.data.keyword.Bluemix_notm}} 控制台，但未使用有效的 IBM 标识。例如，未输入 IBM 标识的标准电子邮件地址，或者尝试使用的是 SoftLayer 用户名和密码。
{: tsCauses}
 
您必须具有有效的 IBM 标识和密码才能登录到 {{site.data.keyword.Bluemix_notm}}。

 * 确保输入 IBM 标识的标准电子邮件地址。
 {: tsResolve}
 * 如果您是使用 SoftLayer 标识的 SoftLayer 用户，那么必须切换到客户门户网站以在您有权访问的每个帐户内进行 IBM 标识认证，然后才能使用 IBM 标识认证进行登录。有关更多信息，请参阅[切换到 IBM 标识](/docs/admin/softlayerlink.html#ibmid_switch)。


## 无法登录到 {{site.data.keyword.Bluemix_notm}}：IBM 标识与任何 IBM Cloud 帐户都不关联
{: #ts_login_noswitch}

使用 IBM 标识登录时，显示了以下消息：
{: tsSymptoms}

`由于认证成功，您已位于此页面中，但是此 IBM 标识未与任何 IBM Cloud 帐户关联。如果您认为这是错误，请联系帐户所有者或主用户。`

您已使用有效的 IBM 标识通过[客户门户网站](https://control.softlayer.com)登录，但未在 SoftLayer 中切换到 IBM 标识认证。
{: tsCauses} 
 
根据需要，完成以下检查：
{: tsResolve}
 * 联系主用户或帐户管理员来检查是否支持您切换到 IBM 标识认证。
 * 确保在 SoftLayer 帐户中完成“切换到 IBM 标识”步骤。请参阅[切换到 IBM 标识](/docs/admin/softlayerlink.html#ibmid_switch)。
 * 确保执行**将 SoftLayer 用户与 IBM 标识相关联**电子邮件中的操作。检查收件箱和垃圾邮件文件夹中是否有该电子邮件。要再次获取此电子邮件（例如，如果电子邮件已到期），请转至“控制门户网站”中的“编辑用户个人档案”页面，然后单击**重新发送电子邮件**。或者，请联系 [{{site.data.keyword.Bluemix_notm}} 支持 ![外部链接图标](../icons/launch-glyph.svg "外部链接图标")](http://ibm.biz/bluemixsupport.com){: new_window}。

**注：**如果您是直接使用 IBM 标识创建的 IBM 标识，那么会收到两封需要处理的电子邮件；一封来自 IBM 标识注册，一封来自 SoftLayer。确保执行这两封电子邮件中的操作。

根据帐户的设置方式，下面的一些登录选项可能适用： 
 * 使用 SoftLayer 标识的 SoftLayer 用户必须通过[客户门户网站](https://control.softlayer.com)登录。
 * 使用 IBM 标识且具有或不具有链接 Bluemix 帐户的 SoftLayer 用户可以通过[客户门户网站](https://control.softlayer.com)登录来打开 SoftLayer 客户门户网站，也可以通过 [Bluemix 控制台](https://console.{DomainName})登录来打开“基础架构”仪表板。 


## 无法登录到 {{site.data.keyword.Bluemix_notm}}：IBM 标识与任何 {{site.data.keyword.Bluemix_notm}} 帐户都不关联
{: #ts_unabletologin}

登录到 {{site.data.keyword.Bluemix_notm}} 时，显示了以下消息：
{: tsSymptoms} 
 
`由于认证成功，您已位于此页面中，但是此 IBM 标识未与任何 {{site.data.keyword.Bluemix_notm}} 帐户关联。`

您已使用有效的 IBM 标识通过 [Bluemix 控制台](https://console.{DomainName})登录，但还没有创建 {{site.data.keyword.Bluemix_notm}} 帐户。
{: tsCauses} 

要创建 {{site.data.keyword.Bluemix_notm}} 帐户，请执行注册过程。
{: tsResolve}

根据帐户的设置方式，下面的一些登录选项可能适用： 
 * 没有链接 SoftLayer 帐户的 Bluemix 用户必须通过 Bluemix 控制台登录。
 * 具有链接 SoftLayer 帐户的 Bluemix 用户可以通过 [Bluemix 控制台](https://console.{DomainName})或[客户门户网站](https://control.softlayer.com)登录。
 

## 无法登录到 {{site.data.keyword.Bluemix_notm}}：控制台未打开
{: #ts_login_stalls}

使用 IBM 标识登录时，显示了登录成功消息，但未返回到 [Bluemix 控制台](https://console.{DomainName})或[客户门户网站](https://control.softlayer.com)。
{: tsSymptoms}

使用以下其中一种解决方案：
{: tsResolve}
 * 关闭浏览器，清除高速缓存和 cookie，然后重试登录。
 * 确保是通过 [Bluemix 控制台](https://console.{DomainName})或[客户门户网站](https://control.softlayer.com)登录的，而不是直接从 IBM 标识认证服务进行登录。
 
 
## 无法登录到 {{site.data.keyword.Bluemix_notm}}：IBM 标识登录未完成
{: #ts_login_ibmid}

登录到 {{site.data.keyword.Bluemix_notm}} 时，使用 IBM 标识认证未完成。
{: tsSymptoms}

IBM 标识认证服务可能发生问题。
{: tsCauses}

在 [IBM BlueID ![外部链接图标](../icons/launch-glyph.svg "外部链接图标")](https://new.wind.ibmcloud.com/webapp/#/status/a1a0c5d743d94a6a9597087541564d8e){: new_window} 上检查该服务的状态，然后重试。
{: tsResolve}


## 无法登录到 {{site.data.keyword.Bluemix_notm}}：帐户暂挂
{: #ts_accntpding}

如果帐户暂挂，那么无法登录到 {{site.data.keyword.Bluemix_notm}}。
 
在注册 {{site.data.keyword.Bluemix_notm}} 试用帐户后，可能无法登录到 {{site.data.keyword.Bluemix_notm}}。将显示以下消息：
{: tsSymptoms}

<code>帐户暂挂。请等待最多 24 小时以获取电子邮件确认并请检查垃圾邮件文件夹。如果仍未收到确认电子邮件，请联系 <a href="http://ibm.biz/bluemixsupport.com" target="_blank">Bluemix 支持</a>。</code>


在注册 {{site.data.keyword.Bluemix_notm}} 试用帐户后，您将收到确认电子邮件。必须单击确认电子邮件中的链接以完成注册过程。
{: tsCauses} 

确认电子邮件将发送到提供的电子邮件地址。检查收件箱和垃圾邮件文件夹。如果尚未收到确认电子邮件，请联系 [{{site.data.keyword.Bluemix_notm}} 支持 ![外部链接图标](../icons/launch-glyph.svg "外部链接图标")](http://ibm.biz/bluemixsupport.com){: new_window}。  
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

如果无法邀请用户加入组织，并需要其他角色来完成此操作，请联系组织管理员来更改您的角色。要识别组织管理员，请完成以下步骤：
{: tsResolve}

  1. 转至 {{site.data.keyword.Bluemix_notm}}“仪表板”。在菜单栏中，单击**帐户**菜单项，然后单击**管理组织**。
  2. 转至您的组织，并查看**用户**选项卡上的组织管理员信息。  
  
如果您由于是合作者（并非成员）而无法邀请用户，那么您必须删除您先前的 {{site.data.keyword.Bluemix_notm}} 帐户，然后受邀以组织成员身份加入该帐户。要删除您先前的帐户并以成员身份加入帐户，请完成以下步骤： 

  1. 联系 [{{site.data.keyword.Bluemix_notm}} 支持 ![外部链接图标](../icons/launch-glyph.svg "外部链接图标")](http://ibm.biz/bluemixsupport){: new_window}，以开具一个支持凭单，请求删除您的帐户。如果存在与旧帐户相关联的数据并且想要将其保存并移动到新帐户，请在您的电子邮件中包含此信息。 
  2. 在您的帐户被删除后，让具有组织管理员角色的用户以组织管理员身份邀请您加入组织。然后，通过邀请注册 {{site.data.keyword.Bluemix_notm}}。 

## 不支持用户批量注册
{: #ts_batchregistration}

在对 {{site.data.keyword.Bluemix_notm}} 注册用户时，必须单独注册每个用户。

{{site.data.keyword.Bluemix_notm}} 不提供同时注册多个用户的功能。
{: tsSymptoms}
 
{{site.data.keyword.Bluemix_notm}} 不支持用户批量注册。要对 {{site.data.keyword.Bluemix_notm}} 注册用户，必须单独注册每个用户。
{: tsCauses}
 
要对 {{site.data.keyword.Bluemix_notm}} 注册多个用户，请为每个用户完成以下步骤：
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

根据需要完成以下一个或多个操作：
{: tsResolve}

  * 刷新或重新启动浏览器。
  * 注销 {{site.data.keyword.Bluemix_notm}}，并重新登录。
  * 使用浏览器的隐私浏览模式。 
  * 清除浏览器的 cookie 和高速缓存。
  * 使用其他浏览器。有关 {{site.data.keyword.Bluemix_notm}} 支持的浏览器版本的信息，请参阅 [Bluemix 先决条件](/docs/overview/whatisbluemix.html#prereqs)。
  * 如果安装了 cf 命令行界面，请输入 `cf apps` 命令以查看应用程序是否正在运行。
