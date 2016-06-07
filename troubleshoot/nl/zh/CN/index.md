---

copyright:
  years: 2015, 2016

---

{:tsSymptoms: .tsSymptoms} 
{:tsCauses: .tsCauses} 
{:tsResolve: .tsResolve} 
{:new_window: target="_blank"}  
{:shortdesc: .shortdesc}
{:codeblock: .codeblock} 

# 有关访问 {{site.data.keyword.Bluemix_notm}} 的故障诊断 
{: #accessing}

*上次更新时间：2016 年 5 月 16 日*

访问 {{site.data.keyword.Bluemix}} 的一般性问题可能包括用户无法登录到 {{site.data.keyword.Bluemix_notm}} 和帐户困于暂挂状态等。然而，在许多情况下，只需执行几个简单的步骤即可解决这些问题。
{:shortdesc}

## 无法登录到 {{site.data.keyword.Bluemix_notm}}
{: #ts_logintobm}

您必须具有有效的 IBM 标识和密码才能登录到 {{site.data.keyword.Bluemix_notm}}。


在尝试登录到 {{site.data.keyword.Bluemix_notm}} 时，您会看到以下错误消息： 
{: tsSymptoms} 

`下面输入的 IBM 标识和/或密码不正确。请重试。`


用于登录 {{site.data.keyword.Bluemix_notm}} 的 IBM 标识和密码无效。
{: tsCauses} 
 

要获取有效的 IBM 标识和密码，请转至我的 IBM 个人档案页面，然后完成以下其中一个步骤：
{: tsResolve}
  * 如果已注册 IBM 标识并且想要检查标识和密码是否有效，请单击**登录**，并在“登录”页面中输入 IBM 标识和密码。如果忘记密码，请单击“登录”页面右侧的**忘记密码**以重置密码。如果忘记 IBM 标识或密码问题仍未解决，请联系全球 IBM 注册帮助台来获取帮助。 
  * 如果没有 IBM 标识，请单击**注册**以注册 IBM 标识和密码。 
  
**注：**对于 IBM 员工，IBM 标识可能不同于内部网登录标识。 





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
nslookup mybluemix.net
```



## 帐户暂挂
{: #ts_accntpding}

如果帐户暂挂，那么无法登录到 {{site.data.keyword.Bluemix_notm}}。

 
在注册 {{site.data.keyword.Bluemix_notm}} 试用帐户后，可能无法登录到 {{site.data.keyword.Bluemix_notm}}。相反，会看到以下消息：
{: tsSymptoms}

<code>帐户暂挂。请等待最多 24 小时以获取电子邮件确认并请检查垃圾邮件文件夹。如果仍未收到确认电子邮件，请联系 <a href="http://ibm.biz/bluemixsupport.com" target="_blank">Bluemix 支持</a>。</code>


在注册 {{site.data.keyword.Bluemix_notm}} 试用帐户后，您将收到确认电子邮件。必须单击确认电子邮件中的链接以完成注册过程。
{: tsCauses} 

确认电子邮件将发送到提供的电子邮件地址。请检查收件箱和垃圾邮件文件夹。如果未收到确认电子邮件，请联系 [{{site.data.keyword.Bluemix_notm}} 支持](http://ibm.biz/bluemixsupport.com){: new_window}。  
{: tsResolve}



## 无法将用户添加到组
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

  1. 转至 {{site.data.keyword.Bluemix_notm}}“仪表板”，单击顶部菜单栏中的**帐户和支持**图标 ![帐户和支持](images/account_support.svg)，然后选择**管理组织**。
  2. 转至您的组织，并查看**用户**选项卡上的组织管理员信息。  
  
如果由于您是合作者（并非成员）而无法邀请用户，那么您必须删除您先前的 {{site.data.keyword.Bluemix_notm}} 帐户，然后被邀请以组织成员身份加入帐户。要删除您先前的帐户并以成员身份加入帐户，请完成以下步骤： 

  1. 联系 [{{site.data.keyword.Bluemix_notm}} 支持](http://ibm.biz/bluemixsupport){: new_window}，以打开一个支持凭单，请求删除您的帐户。如果存在与旧帐户相关联的数据并且想要将其保存并移动到新帐户，请在您的电子邮件中包含此信息。 
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

  1. 在 {{site.data.keyword.Bluemix_notm}} 用户界面的右上角单击**注册**。
  2. 按照向导的提示完成每个步骤。

    

## 无法装入 {{site.data.keyword.Bluemix_notm}} 页面
{: #ts_err}

在使用 {{site.data.keyword.Bluemix_notm}} 用户界面时，您可能无法装入 {{site.data.keyword.Bluemix_notm}} 页面。相反，您可能会看到错误消息 BXNUI0001E 或 BXNUI0016E。
 

在使用 {{site.data.keyword.Bluemix_notm}} 用户界面时，您可能看到以下一条错误消息：
{: tsSymptoms}

`BXNUI0001E: 未装入页面，因为 Bluemix 未检测到是否存在会话。`


`BXNUI0016E: 未检索到应用程序和服务，因为未装入 Bluemix 页面。`

 

您可以根据需要完成以下一个或多个操作：
{: tsResolve}

  * 刷新或重新启动浏览器。
  * 注销 {{site.data.keyword.Bluemix_notm}}，并重新登录。
  * 使用浏览器的隐私浏览模式。 
  * 清除浏览器的 cookie 和高速缓存。
  * 使用其他浏览器。有关 {{site.data.keyword.Bluemix_notm}} 支持的浏览器版本的信息，请参阅 [{{site.data.keyword.Bluemix_notm}} 先决条件](https://developer.ibm.com/bluemix/support/#prereqs){: new_window}。
  * 如果安装了 cf 命令行界面，请输入 `cf apps` 命令以查看应用程序是否正在运行。
  
  
  
  
  
## {{site.data.keyword.Bluemix_notm}} 顶部菜单栏消失
{: #ts_topmenubar}

调整浏览器窗口大小或使用移动设备时，可能看不到 {{site.data.keyword.Bluemix_notm}} 顶部菜单栏。


当您缩小浏览器窗口的大小或使用移动设备时，{{site.data.keyword.Bluemix_notm}} 顶部菜单栏会消失。顶部菜单栏消失时，以堆叠线图标形式显示的侧边抽屉菜单会显示在左上角。 
{: tsSymptoms}

 

{{site.data.keyword.Bluemix_notm}} 用户界面具有响应设计。当查看环境发生变化时，{{site.data.keyword.Bluemix_notm}} 用户界面的布局可能也会发生变化。 
{: tsCauses}
 

请改用左上角的侧边抽屉菜单。
{: tsResolve}








# 有关管理应用程序的故障诊断
{: #managingapps}

有关管理应用程序的一般性问题可能包括：无法更新应用程序；未显示双字节字符。然而，在许多情况下，只需执行几个简单的步骤即可解决这些问题。
{:shortdesc}





## 无法将应用程序切换到调试方式
{: #ts_debug}

如果 Java 虚拟机 (JVM) 版本为 8 或更低版本，那么可能无法启用调试方式。 


选择**启用应用程序调试**后，工具会尝试将应用程序切换到调试方式。然后，Eclipse 工作台会启动调试会话。工具成功启用调试方式时，Web 应用程序状态会依次显示 `Updating mode`、`Developing` 和 `Debugging`。
{: tsSymptoms}

但是，工具启用调试方式失败时，Web 应用程序状态只会依次显示 `Updating mode` 和 `Developing`，而不会显示 `Debugging`。工具还可能会在“控制台”视图中显示以下错误消息：

```
bluemixMgmgClient - ???? [pool-1-thread-1] .... ERROR --- ClientProxyImpl: Cannot create the websocket connections for MyWebProj
com.ibm.ws.cloudoe.management.client.exception.ApplicationManagementException: javax.websocket.DeploymentException: The HTTP request to initiate the  WebSocket connection failed
at com.ibm.ws.cloudoe.management.client.impl.ClientProxyImpl.onNewClientSocket(ClientProxyImpl.java:161)
at com.ibm.ws.cloudoe.management.client.impl.ClientProxyImpl$RunServerTask.run(ClientProxyImpl.java:267)
at java.util.concurrent.Executors$RunnableAdapter.call(Executors.java:522)
at java.util.concurrent.FutureTask.run(FutureTask.java:277)
at java.util.concurrent.ThreadPoolExecutor.runWorker(ThreadPoolExecutor.java:1153)
at java.util.concurrent.ThreadPoolExecutor$Worker.run(ThreadPoolExecutor.java:628)
at java.lang.Thread.run(Thread.java:785)
Caused by: javax.websocket.DeploymentException: The HTTP request to initiate the WebSocket connection failed
at  org.apache.tomcat.websocket.WsWebSocketContainer.connectToServer(WsWebSocketContainer.java:315)
at  com.ibm.ws.cloudoe.management.client.impl.ClientProxyImpl.onNewClientSocket(ClientProxyImpl.java:158)
... 6 more
Caused by: java.util.concurrent.TimeoutException
at org.apache.tomcat.websocket.AsyncChannelWrapperSecure$WrapperFuture.get(AsyncChannelWrapperSecure.java:505)
at org.apache.tomcat.websocket.WsWebSocketContainer.processResponse(WsWebSocketContainer.java:542)
at org.apache.tomcat.websocket.WsWebSocketContainer.connectToServer(WsWebSocketContainer.java:296)
... 7 more
[2016-01-15 13:33:51.075] bluemixMgmgClient - ????  [pool-1-thread-1] .... ERROR --- ClientProxyImpl: Cannot create the  websocket connections for MyWebProj
com.ibm.ws.cloudoe.management.client.exception.ApplicationManagementException: javax.websocket.DeploymentException: The HTTP request to initiate the  WebSocket connection failed
at com.ibm.ws.cloudoe.management.client.impl.ClientProxyImpl.onNewClientSocket(ClientProxyImpl.java:161)
at com.ibm.ws.cloudoe.management.client.impl.ClientProxyImpl$RunServerTask.run(ClientProxyImpl.java:267)
at java.util.concurrent.Executors$RunnableAdapter.call(Executors.java:522)
at java.util.concurrent.FutureTask.run(FutureTask.java:277)
at java.util.concurrent.ThreadPoolExecutor.runWorker(ThreadPoolExecutor.java:1153)
at java.util.concurrent.ThreadPoolExecutor$Worker.run(ThreadPoolExecutor.java:628)
at java.lang.Thread.run(Thread.java:785)
Caused by: javax.websocket.DeploymentException: The HTTP request to initiate the WebSocket connection failed
at org.apache.tomcat.websocket.WsWebSocketContainer.connectToServer(WsWebSocketContainer.java:315)
at com.ibm.ws.cloudoe.management.client.impl.ClientProxyImpl.onNewClientSocket(ClientProxyImpl.java:158)
... 6 more
Caused by: java.util.concurrent.TimeoutException
at org.apache.tomcat.websocket.AsyncChannelWrapperSecure$WrapperFuture.get(AsyncChannelWrapperSecure.java:505)
at org.apache.tomcat.websocket.WsWebSocketContainer.processResponse(WsWebSocketContainer.java:542)
at org.apache.tomcat.websocket.WsWebSocketContainer.connectToServer(WsWebSocketContainer.java:296)
... 7 more
```
 

以下 Java 虚拟机 (JVM) 版本无法建立调试会话：IBM JVM 7、IBM JVM 8 以及早于 Oracle JVM 8 的版本。
{: tsCauses}

如果工作台 JVM 是上述其中一个版本，那么在创建调试会话时可能会发生问题。工作台 JVM 版本通常是本地计算机的系统 JVM。系统 JVM 与运行中 Bluemix Java 应用程序的 JVM 不同。Bluemix Java 应用程序几乎总是在 IBM JVM 上运行，但有时会在 OpenJDK JVM 上运行。
  

要检查 IBM Eclipse Tools for Bluemix 运行的 Java 版本，请完成以下步骤：
{: tsResolve}

  1. 在 IBM Eclipse Tools for Bluemix 中，选择**帮助** > **关于 Eclipse** > **安装详细信息** > **配置**。
  2. 从列表中找到 `eclipse.vm` 属性。以下行是 `eclipse.vm` 属性的示例：
	
	```
	eclipse.vm=C:\Program Files\IBM\ibm-java-sdk-80-win-x86_64\bin\..\jre\bin\j9vm\jvm.dll
	```

  3. 在命令行中，从 Java 安装的 `bin` 目录输入 `java -version`。这将显示 IBM JVM 版本信息。

如果工作台 JVM 为 IBM JVM 7 或 8，或者为早于 Oracle JVM 8 的版本，请完成以下步骤来切换到 Oracle JVM 8：

  1. 下载并安装 Oracle JVM 8；请参阅 [Java SE Downloads](http://www.oracle.com/technetwork/java/javase/downloads/index.html){: new_window} 以获取详细信息。
  2. 重新启动 Eclipse。
  3. 检查 `eclipse.vm` 属性是否指向 Oracle JVM 8 的新安装。







## 无法执行请求的操作
{: #ts_authority}

没有相应的访问权限，您可能无法完成操作。

 

尝试对服务实例或应用程序实例执行操作时，无法完成请求的操作，并看到以下其中一条错误消息：
{: tsSymptoms}

`BXNUI0514E: 您不是 <orgName> 组织中任何空间的开发者。`


`服务器错误，状态码：403，错误代码：10003，消息：您无权执行请求的操作。`

 

您没有执行操作所需的相应级别的权限。
{: tsCauses}

  

要获取相应级别的权限，请使用以下其中一种方法：
{: tsResolve}
 * 选择您具有其开发者角色的另一个组织和空间。 
 * 请求组织管理员将您的角色更改为开发者，或者创建空间，然后为您分配开发者角色。有关详细信息，请参阅[管理组织](../admin/orgs_spaces.html)。
 

 


## 由于授权错误而无法访问 {{site.data.keyword.Bluemix_notm}} 服务
{: #ts_vcap}

应用程序访问 {{site.data.keyword.Bluemix_notm}} 服务时，如果服务凭证是硬编码到应用程序中的，那么可能会发生授权错误。 

将应用程序配置为与 {{site.data.keyword.Bluemix_notm}} 服务通信后，将应用程序部署到 {{site.data.keyword.Bluemix_notm}}。但是，无法使用应用程序来访问 {{site.data.keyword.Bluemix_notm}} 服务，并且会收到授权错误。
{: tsSymptoms}

硬编码到应用程序中的凭证可能不正确。每次重新创建服务时，用于访问该服务的凭证都会改变。
{: tsCauses}


不要将凭证硬编码到应用程序中，请改用 VCAP_SERVICES 环境变量中的连接参数。具体如何使用 VCAP_SERVICES 环境变量中的连接参数取决于程序语言。例如，对于 Node.js 应用程序，可以使用以下命令：
{: tsResolve}

```
process.env.VCAP_SERVICES
```
有关可在其他程序语言中使用的命令的更多信息，请参阅 [Java](http://docs.run.pivotal.io/buildpacks/java/java-tips.html#env-var){: new_window} 和 [Ruby](http://docs.run.pivotal.io/buildpacks/ruby/ruby-tips.html#env-var){: new_window}。 
 

 
 




## 无法使用 IBM Eclipse Tools for {{site.data.keyword.Bluemix_notm}} 部署应用程序
{: #ts_bm_tools_facet}

将不受支持构面应用于 Eclipse 项目时，可能无法使用 IBM Eclipse Tools for {{site.data.keyword.Bluemix_notm}} 将应用程序部署到 {{site.data.keyword.Bluemix_notm}}。 

 

使用 Cloud Foundry CLI 可将应用程序成功部署到 {{site.data.keyword.Bluemix_notm}}。但是，无法使用 IBM Eclipse Tools for {{site.data.keyword.Bluemix_notm}} 将应用程序部署到 {{site.data.keyword.Bluemix_notm}}，并且会看到以下错误消息：`项目构面 <facet_name> 不受支持。` 例如，`项目构面 Cloud Foundry Standalone Application V1.0 不受支持。`
{: tsSymptoms}

 

IBM Eclipse Tools for {{site.data.keyword.Bluemix_notm}} 通过项目构面将项目映射到 {{site.data.keyword.Bluemix_notm}} 运行时。构面为 Eclipse 中的 Java EE 项目定义需求，并用作运行时配置的一部分，以便将不同运行时与不同项目关联。如果应用于项目的构面不受 IBM Eclipse Tools for {{site.data.keyword.Bluemix_notm}} 支持，那么可能无法使用 IBM Eclipse Tools for {{site.data.keyword.Bluemix_notm}} 部署应用程序。
{: tsCauses}


必须从 Eclipse 项目中除去该构面，才能使用 IBM Eclipse Tools for {{site.data.keyword.Bluemix_notm}} 部署应用程序。
{: tsResolve} 

要除去该构面，请在 IBM Eclipse Tools for {{site.data.keyword.Bluemix_notm}} 中单击该项目的**项目>属性>项目构面**。然后，清除不受支持构面的复选框。 



## 收到 502 无效网关错误
{: #ts_502_error}

如果在与 {{site.data.keyword.Bluemix_notm}} 上的应用程序进行交互时收到“502 无效网关”错误，请检查 {{site.data.keyword.Bluemix_notm}} 状态页面，然后采取相应的措施。

 

您收到以“502 无效网关”开头的错误消息。例如，您可能会看到 `502 无效网关：注册的端点未能处理请求。`
{: tsSymptoms}

 

通常会在以下情况下发生“无效网关”错误：您访问某个 Web 站点，该站点使用代理服务器来存储和中继来自托管该站点的主服务器中的数据。主服务器和代理服务器之间可能未正确连接，因此您会在浏览器窗口中看到 HTTP 状态码 502。此状态码指示该站点的主服务器未收到代理服务器所期望的 HTTP 实施。
{: tsCauses}

其他导致“无效网关”错误的不太常见的原因包括：因特网服务提供商 (ISP) 信息遗失、防火墙配置错误以及浏览器高速缓存错误。 

 

如果您怀疑 {{site.data.keyword.Bluemix_notm}} 服务关闭，请先检查 [{{site.data.keyword.Bluemix_notm}} 状态](https://developer.ibm.com/bluemix/support/#status){: new_window}页面。您可能想要在其他 {{site.data.keyword.Bluemix_notm}} 区域使用该服务来作为一种变通方法。有关详细信息，请参阅[在另一个区域使用服务](../services/reqnsi.html#cross_region_service){: new_window}。如果服务状态正常，请尝试执行以下步骤来解决问题： 
{: tsResolve}

  * 重试操作：
    * 通过按键盘上的 F5 或单击刷新按钮，重新装入页面。如果此步骤无效，请清除浏览器的高速缓存和 cookie，然后再重新装入。
	* 使用其他浏览器。
	* 重新引导您的路由器、调制解调器和计算机。重新引导这些设备可以清理导致 502 错误的各种错误。 
  * 稍等，然后重试。在某些情况下，您的因特网服务提供商或 {{site.data.keyword.Bluemix_notm}} 服务可能会发生临时问题。您可以一直等到临时问题得到解决为止。
  * 如果问题持续存在，请联系 {{site.data.keyword.Bluemix_notm}} 支持。有关更多信息，请参阅[联系 {{site.data.keyword.Bluemix_notm}} 支持](../support/index.html#contacting-bluemix-support){: new_window}。 




## 超出磁盘配额
{: #ts_disk_quota}

如果磁盘空间不足，可以手动修改磁盘配额来获取更多的磁盘空间。

  

磁盘空间不足时，可能会看到一条消息，指示超过磁盘配额。为了解决该问题，您可能尝试了通过扩展应用程序实例来获取更多的磁盘空间。例如，您可能更改了应用程序详细信息页面上的内存配额，将大小从 256 MB 扩展到 1256 MB。但是，由于磁盘配额依然未变，所以您并没有获得更多的磁盘空间。 
{: tsSymptoms}


为应用程序分配的缺省磁盘配额为 1 GB。如果您需要更多的磁盘空间，必须手动指定磁盘配额。 
{: tsCauses}

 
使用以下某个方法可指定磁盘配额。可指定的最大磁盘配额为 2 GB。如果 2 GB 仍不够，请尝试外部服务，例如[对象存储](../services/ObjectStorage/index.html){: new_window}。
{: tsResolve}

  * 在 manifest.yml 文件中，添加以下项：
    ```
	disk_quota: <disk_quota>
	```
  * 在用于将应用程序推送到 {{site.data.keyword.Bluemix_notm}} 的 `cf push` 命令中使用 **-k** 选项：
    ```
	cf push appname -p app_path -k <disk_quota>
	```

	
	
## 无法添加 Git 存储库
{: #ts_cannot_addgit}

在“仪表板”上创建应用程序后，单击“添加 GIT”来创建 Git 存储库，但无法继续。



单击**添加 GIT** 后，有一个窗口打开，但发生以下某个问题：
{: tsSymptoms} 

  * 窗口挂起且屏幕空白。
  * 显示一条消息，指示第三方 cookie 存在问题。



您的浏览器可能配置为阻止设置 cookie。必须在 {{site.data.keyword.Bluemix_notm}} 控制台的上下文内从 hub.jazz.net 因特网域中的 IBM® Bluemix DevOps Services 站点设置该 cookie。
{: tsCauses}  

 

您可以使用以下其中一种方法来解决此问题：
{: tsResolve}

  * 按照从 {{site.data.keyword.Bluemix_notm}} 控制台打开的窗口中的指示信息执行操作。单击按钮。另一个浏览器窗口会暂时打开。在该窗口中，DevOps Services 会设置认证 cookie。
  * 在另一个浏览器选项卡中，转至 https://hub.jazz.net，然后登录。返回到 {{site.data.keyword.Bluemix_notm}} 控制台，然后刷新页面。再次单击**添加 GIT**。
  * 更改浏览器设置以启用第三方 cookie，然后再次单击“添加 GIT”。有关配置设置的详细信息，请参阅适用于您的浏览器的文档：
    * [Mozilla Firefox](https://support.mozilla.org/en-US/kb/enable-and-disable-cookies-website-preferences#w_how-do-i-change-cookie-settings){: new_window}
	* [Google Chrome](https://support.google.com/chrome/answer/95647){: new_window}
	* [Apple Safari](https://support.apple.com/kb/PH17191){: new_window}
	* [Microsoft Internet Explorer](http://windows.microsoft.com/en-us/internet-explorer/delete-manage-cookies#ie=ie-11){: new_window}
如果这些变通方法无法解决该问题，请向 idslogin@jazz.net 发送电子邮件。



## Android 应用程序收不到推送通知
{: #ts_push}

在无法访问 Google 的某些地区，Android 应用程序收不到您通过 IBM Push 服务发送出来的通知。在此情况下，可以使用第三方服务作为一种变通方法。

 

为 Bluemix 应用程序绑定推送服务，并将消息发送给已注册的设备。但在某些地区，在 Android 平台上开发的应用程序收不到您的通知。
{: tsSymptoms}

 
IBM Push 服务使用 Google 云消息传递 (GCM) 服务将通知分派到在 Android 平台上开发的移动应用程序。要使 Android 应用程序能够接收通知，移动应用程序必须可以访问 Google 云消息传递 (GCM) 服务。在 Android 应用程序无法访问 GCM 服务的区域，Android 应用程序收不到推送通知。
{: tsCauses}

 
使用不依赖于 GCM 服务的第三方服务作为一种变通方法，例如 [Pushy](https://pushy.me){: new_window}、[igetui](http://www.getui.com/){: new_window} 和 [jpush](https://www.jpush.cn/){: new_window}。
{: tsResolve}



## 超出组织的服务限制
{: #ts_servicelimit}

如果您是试用帐户用户，那么可能无法在超过组织服务限制的情况下在 {{site.data.keyword.Bluemix_notm}} 中创建应用程序。
 

尝试在 {{site.data.keyword.Bluemix_notm}} 中创建应用程序时，您会看到以下错误消息： 
{: tsSymptoms}

`BXNUI2032E: 未创建 <service_instances> 资源。联系 Cloud Foundry 来创建资源时，发生了错误。Cloud Foundry 消息：“已超过组织的服务限制。”`



在已超过您帐户可拥有的服务实例数的限制时，会发生此错误。试用帐户的最大服务实例数是 10。
{: tsCauses} 

 

删除不需要的任何服务实例，或者除去您可拥有的服务实例数的限制。
{: tsResolve}
 
  * 要删除服务实例，可以使用 {{site.data.keyword.Bluemix_notm}} 用户界面或者命令行界面。
    要使用 {{site.data.keyword.Bluemix_notm}} 用户界面删除服务实例，请完成下列步骤：
	  1. 在 {{site.data.keyword.Bluemix_notm}}“仪表板”上，单击左侧窗格中的**服务**。将显示服务磁贴。 
	  2. 在要删除的服务磁贴上，单击**菜单**图标。
	  3. 单击**删除服务**。在删除服务实例之后，会提示您重新编译打包绑定该服务实例的应用程序。 
    要使用命令行界面删除服务实例，请完成下列步骤：
	  1. 取消服务实例与应用程序的绑定，方法是输入 `cf unbind-service <appname> <service_instance_name>`。
	  2. 删除服务实例，方法是输入 `cf delete-service <service_instance_name>`。
	  3. 在删除服务实例之后，可能需要重新编译打包绑定该服务实例的应用程序，方法是输入 `cf restage <appname>`。
  * 要除去您可拥有的服务实例数的限制，请将试用帐户转换为付费帐户。有关如何将试用帐户转换为付费帐户的信息，请参阅[如何更改套餐](../pricing/index.html#changing){: new_window}。

  
  
## 无法在 {{site.data.keyword.Bluemix_notm}} 上运行可执行文件
{: #ts_executable}

如果可执行文件是在不同环境中开发的，那么可能无法在 {{site.data.keyword.Bluemix_notm}} 上运行这些可执行文件。 

 

如果可执行文件是在不同环境中开发的，那么无法在 {{site.data.keyword.Bluemix_notm}} 上运行这些可执行文件。
{: tsSymptoms}

 

如果要推送到 {{site.data.keyword.Bluemix_notm}} 的内容已经是可执行文件，那么该内容是先前构建的，不需要在 {{site.data.keyword.Bluemix_notm}} 上进行构建。在此情况下，无需任何 buildpack，可执行文件就可以在 {{site.data.keyword.Bluemix_notm}} 上运行。但是，必须向 {{site.data.keyword.Bluemix_notm}} 明确指示不需要 buildpack。
{: tsCauses}

 

当您将可执行文件推送到 {{site.data.keyword.Bluemix_notm}} 时，必须指定 null-buildpack，它指示不需要 buildpack。指定 null-buildpack 的方法是使用带 **-b** 选项的 `cf push` 命令：
{: tsResolve}

```
cf push appname -p <app_path> -c <start_command> -b <null-buildpack>
```
例如：
```
cf push appname -p <app_path> -c ./RunMeNow -b https://github.com/ryandotsmith/null-buildpack
```


## 超过组织的内存限制
{: #ts_outofmemory}

如果您是试用帐户用户，那么可能无法在超过组织内存限制的情况下将应用程序部署到 {{site.data.keyword.Bluemix_notm}}。您可以减少应用程序使用的内存，或者增加您帐户的内存配额。 



将应用程序部署到 {{site.data.keyword.Bluemix_notm}} 时，您会看到以下错误消息：
{: tsSymptoms} 

`失败 服务器错误，状态码：400，错误代码：100005，消息：您已超过组织的内存限制。`

 

当组织的剩余内存量低于您要部署的应用程序所需的内存量时，会发生此错误。试用帐户的最大内存配额为 2 GB。
{: tsCauses}



您可以增加帐户的内存配额，或者减少应用程序使用的内存。
{: tsResolve} 

  * 要增加帐户的内存配额，请将试用帐户转换为付费帐户。有关将试用帐户转换为付费帐户的信息，请参阅 [付费帐户](../pricing/index.html#pay-accounts){: new_window}。 
  * 要减少应用程序使用的内存，请使用 {{site.data.keyword.Bluemix_notm}} 用户界面或 cf 命令行界面。
    如果使用 {{site.data.keyword.Bluemix_notm}} 用户界面，请完成下列步骤：
	  1. 在 {{site.data.keyword.Bluemix_notm}}“仪表板”上，选择应用程序。这将打开应用程序详细信息页面。
	  2. 在运行时窗格中，可以减少应用程序的最大内存限制和/或应用程序实例数。 
	如果使用 cf 命令行界面，请完成下列步骤：
	  1. 检查应用程序使用了多少内存：
	  ```
	  cf apps
	  ```
	     cf apps 命令会列出当前空间中部署的所有应用程序。还会显示每个应用程序的状态。
      2. 要减少应用程序使用的内存量，请减少应用程序实例数和/或最大内存限制：
	  ```
	  cf push <appname> -p <app_path> -i <instance_number> -m <memory_limit>
      ```
	  3. 重新启动应用程序以使更改生效。



	  
## 应用程序不会自动重新启动
{: #ts_apps_not_auto_restarted}


当绑定到应用程序的服务停止工作时，该应用程序不会自动重新启动。	  
	  
 

当绑定到应用程序的服务崩溃时，应用程序可能会发生如中断、异常和连接失败等问题。 {{site.data.keyword.Bluemix_notm}} 不会自动重新启动应用程序，以便从这些问题中进行恢复。
{: tsSymptoms}



此行为是 Cloud Foundry 故意为之。
{: tsCauses} 

 

您可以通过在命令行界面中键入以下命令来手动重新启动应用程序：
{: tsResolve}

```
cf push <appname> -p <app_path>
```
此外，还可以对应用程序进行编码，以识别如中断、异常和连接失败等问题，并从这些问题中进行恢复。 

	  

## 推送应用程序时用户定义的变量丢失
{: #ts_varsnotretained}

从 IBM Eclipse Tools for {{site.data.keyword.Bluemix_notm}} 将应用程序推送到 {{site.data.keyword.Bluemix_notm}} 时，会重置您所指定的变量，但如果将变量保存到清单文件中，那么将另当别论。



从 IBM Eclipse Tools for {{site.data.keyword.Bluemix_notm}} 将应用程序推送到 {{site.data.keyword.Bluemix_notm}} 后，您所指定的变量会丢失。
{: tsSymptoms} 


只有将您所指定的变量保持到清单文件中，这些变量才会得到保存。
{: tsCauses} 

 

从 IBM Eclipse Tools for {{site.data.keyword.Bluemix_notm}} 将应用程序推送到 {{site.data.keyword.Bluemix_notm}} 时，请在“应用程序”向导的“应用程序详细信息”页面上选中**保存到清单文件**复选框。这样，您在向导中指定的变量就会保存到应用程序的清单文件中。 下次打开向导时，这些变量会自动显示出来。
{: tsResolve}



## {{site.data.keyword.Bluemix_notm}} Live Sync 图标不显示
{: #ts_llz_lkb_3r}

您在 IBM Bluemix DevOps Services 中创建了应用程序，但 Web IDE 中不显示 IBM Bluemix Live Sync 图标。

 

在 DevOps Services Web IDE 中编辑 Node.js 应用程序时，不显示 {{site.data.keyword.Bluemix_notm}} 的“实时编辑”、“快速重新启动”和“调试”图标。
{: tsSymptoms}

 

在以下情况下，这些图标不可用：
{: tsCauses}

  * `manifest.yml` 文件未存储在项目的顶层。
  * 应用程序存储在子目录中而不是项目顶层中，但未在 `manifest.yml` 文件中指定该子目录的路径。
  * 应用程序中不包含 `package.json` 文件。


使用以下其中一种方法可解决该问题： 
{: tsResolve} 

  * 如果 `manifest.yml` 文件未存储在项目的顶层，请将其存储在该位置。
  * 如果应用程序存储在子目录中，请在 `manifest.yml` 文件中指定该子目录的路径。
  ```
   path: path_to_application
   ```
  * 在应用程序所在的目录中创建 `package.json` 文件。

  
  
  

  
  

  
  
## 在 {{site.data.keyword.Bluemix_notm}} 上找不到组织
{: #ts_orgs}

在 {{site.data.keyword.Bluemix_notm}} 区域上工作时，可能在 {{site.data.keyword.Bluemix_notm}} 上找不到组织。
  
 

您可以成功登录到 {{site.data.keyword.Bluemix_notm}} 用户界面，但不能使用 cf 命令行界面或 Eclipse 插件来推送应用程序。
{: tsSymptoms}

尝试使用 cf 命令行界面将应用程序推送到 {{site.data.keyword.Bluemix_notm}} 时，您会看到以下某个错误消息（消息中指定了组织名称）： 

`查找组织时出错`

`找不到组织`


尝试使用 Cloud Foundry Eclipse 插件将应用程序推送到 {{site.data.keyword.Bluemix_notm}} 时，您会看到以下错误消息：

`找不到 cloudspace。`



发生此问题的原因是您要使用的区域的 API 端点未指定，且您要查找的组织可能位于其他区域中。
{: tsCauses} 

   
  
如果使用 cf 命令行界面将应用程序推送到 {{site.data.keyword.Bluemix_notm}}，请输入 cf api 命令并指定区域的 API 端点。例如，输入以下命令以连接到 {{site.data.keyword.Bluemix_notm}} 欧洲英国区域：
{: tsResolve}

```
cf api https://api.eu-gb.bluemix.net
```
如果要使用 Eclipse 工具将应用程序推送到 {{site.data.keyword.Bluemix_notm}}，必须先创建 {{site.data.keyword.Bluemix_notm}} 服务器，然后指定所创建组织所在的 {{site.data.keyword.Bluemix_notm}} 区域的 API 端点。有关使用 Eclipse 工具的更多信息，请参阅[使用 IBM Eclipse Tools for Bluemix 部署应用程序](../manageapps/eclipsetools/eclipsetools.html){: new_window}。  
  
  


## 无法创建应用程序路径
{: #ts_hostistaken}

将应用程序部署到 {{site.data.keyword.Bluemix_notm}} 时，如果您所指定的主机名已在使用，那么无法创建该应用程序的路径。



将应用程序部署到 {{site.data.keyword.Bluemix_notm}} 时，您会看到以下错误消息： 
{: tsSymptoms} 

`正在创建路径 hostname.domainname ... 失败 服务器错误，状态码：400，错误代码：210003，消息：所采用的主机为：hostname`



如果您所指定的主机名已在使用，那么会发生此问题。
{: tsCauses} 


  
您所指定的主机名在您所使用的域中必须是唯一的。要指定不同的主机名，请使用以下某个方法：
{: tsResolve} 

  * 如果通过使用 `manifest.yml` 文件来部署应用程序，请在 host 选项中指定主机名。	 
    ```
    host: <hostname>	
	```
  * 如果从命令提示符部署应用程序，请使用带有 **-n** 选项的 `cf push` 命令。 
    ```
    cf push <appname> -p <app_path> -n <hostname>
    ```


## 无法使用 cf push 命令推送 WAR 应用程序
{: #ts_cf_war}

如果未正确指定应用程序位置，那么可能无法使用 cf push 命令来将归档的 Web 应用程序推送到 {{site.data.keyword.Bluemix_notm}}。
	


使用 `cf push` 命令将 WAR 应用程序上传到 {{site.data.keyword.Bluemix_notm}} 时，您会看到错误消息：`编译打包错误：由于编译打包失败，无法获取实例。`
{: tsSymptoms} 

 

如果未指定 WAR 文件，或者未指定 WAR 文件的路径，那么可能会发生此问题。 
{: tsCauses}

 	
	
使用 **-p** 选项来指定 WAR 文件或将路径添加到 WAR 文件。例如：
{: tsResolve}

```
cf push MyUniqueAppName01 -p app.war
```

```
cf push MyUniqueAppName02 -p "./app.war"
```
有关 `cf push` 命令的更多信息，请输入 `cf push -h`。 	





## 将 Liberty 应用程序推送到 {{site.data.keyword.Bluemix_notm}} 时未正确显示双字节字符
{: #ts_doublebytes}

如果没有为 servlet 或 JSP 文件正确配置 Unicode 支持，那么可能未正确显示双字节字符。

 

将 Liberty 应用程序推送到 {{site.data.keyword.Bluemix_notm}} 时，未正确显示在应用程序内指定的双字节字符。
{: tsSymptoms}

 

如果没有为 servlet 或 JSP 文件正确配置 Unicode 支持，那么可能发生该问题。
{: tsCauses}


您可以在 servlet 或 JSP 文件内使用以下代码：
{: tsResolve} 

  * 在 servlet 源文件中， 
    ```
	response.setContentType("text/html; charset=UTF-8");
	```
  * 在 JSP 中， 
    ```
	<meta http-equiv="Content-Type" content="text/html; charset=UTF-8" />
	```
	
	
	

## 无法部署 Node.js 应用程序
{: #ts_nodejs_deploy}

您在更新 Node.js 应用程序或将 Node.js 应用程序部署到 {{site.data.keyword.Bluemix_notm}} 时可能会遇到问题。



您在更新 Node.js 应用程序或将 Node.js 应用程序部署到 {{site.data.keyword.Bluemix_notm}} 时，可能会看到以下其中一条错误消息：
{: tsSymptoms} 

`任何可用 buildpack 均未成功检测到应用程序。`


`实例（索引 0）未能开始接受连接。`


`由于编译打包失败，无法获取实例。`


 

以下原因可能导致问题：
{: tsCauses}
 
  * 未指定启动命令。
  * 部署 Node.js 应用程序所需的文件在应用程序中缺少，或者放置在除根目录外的文件夹中。
  


	
根据导致问题的原因，采取以下操作：
{: tsResolve} 

  * 通过以下其中一种方法来指定启动命令： 
      * 使用命令行界面。例如：
        ```
		cf push MyUniqueNodejs01 -p app_path -c "node app.js"
		```
	  * 使用 [package.json](https://docs.npmjs.com/json){: new_window} 文件。例如：
	    ```
		{
      ...
  	   "scripts": {
	 		 "start": "node app.js"
 	   }
	}
	    ```
	  * 使用 `manifest.yml` 文件。例如： 
	    ```
		applications:
  name: MyUniqueNodejs01
  ...
  command: node app.js
  ...
        ```

  * 确保 `package.json` 文件在 Node.js 应用程序中存在，才能启用用来识别应用程序的 Node.js buildpack。此外，您必须将此文件放置在应用程序的根目录中。	
    以下示例显示简单的 `package.json` 文件：  
	```
	{
        "name": "MyUniqueNodejs01",
        "version": "0.0.1",
        "description": "A sample package.json file",
        "dependencies": {
                "express": "3.4.x",
                "jade": "1.1.x"
        },
        "engines": {
                "node": "0.10.x"
        },
        "scripts": {
                  "start": "node app.js"
        }
 }
    ```
	
有关 Node.js 应用程序的更多提示，请参阅 [Tips for Node.js Applications](http://docs.cloudfoundry.org/buildpacks/node/node-tips.html){: new_window}。	




## 将 {{site.data.keyword.Bluemix_notm}} Liberty 应用程序从 Bluemix DevOps Services 导入到 Eclipse 之后 `server.xml` 文件中出现配置错误
{: #ts_eclipse}

在将 {{site.data.keyword.Bluemix_notm}} Liberty 应用程序从 IBM Bluemix DevOps Services 导入到 Eclipse 之后，如果在 `server.xml` 文件中看到配置错误，那么可能需要从项目中除去 `server.xml` 文件。 

 

在将 {{site.data.keyword.Bluemix_notm}} Liberty 应用程序从 {{site.data.keyword.Bluemix_notm}} DevOps Services 导入到 Eclipse 之后，您会在 Eclipse 问题视图中看到 `server.xml` 文件内的配置错误。
{: tsSymptoms}

 

将 Liberty 应用程序推送到 {{site.data.keyword.Bluemix_notm}} 时，Liberty buildpack 会使用 `server.xml` 文件来配置应用程序，并生成 `runtime-vars.xml` 文件。将应用程序导入到 Eclipse 时，本地环境中不存在 `runtime-vars.xml` 文件。
{: tsCauses}

 

您可以通过从项目中除去 server.xml 文件来解决此问题。将应用程序作为 WAR 应用程序进行推送时，buildpack 会动态创建 `server.xml` 文件。有关更多信息，请参阅 [Liberty for Java](../runtimes/liberty/index.html){: new_window}。
{: tsResolve}
	
	
## 无法使用定制 buildpack 编译打包应用程序
{: #ts_bp_compilation}

如果 buildpack 内的脚本为“不可执行”，那么可能无法使用定制 buildpack 将应用程序部署到 {{site.data.keyword.Bluemix_notm}}。



使用定制 buildpack 将应用程序部署到 {{site.data.keyword.Bluemix_notm}} 时，您会看到错误消息：`应用程序未能编译打包，因此没有要显示的实例。`
{: tsSymptoms} 


如果脚本（如检测脚本、编译脚本和发布检测）不可执行，那么可能发生此问题。
{: tsCauses}

 

您可以使用 [git update](http://git-scm.com/docs/git-update-index){: new_window} 命令将每个脚本的许可权更改为“可执行”。例如，可以键入 `git update --chmod=+x script.sh`。
{: tsResolve}
	
	
	
## 无法将应用程序从 DevOps Services 部署到 {{site.data.keyword.Bluemix_notm}}
{: #ts_devops_to_bm}

如果您的应用程序中不存在 `manifest.yml` 文件，那么可能无法将应用程序从 IBM Bluemix DevOps Services 推送到 {{site.data.keyword.Bluemix_notm}}。

 

将应用程序从 DevOps Services 部署到 {{site.data.keyword.Bluemix_notm}} 时，可能会显示错误消息：`检测不到受支持的应用程序类型`。
{: tsSymptoms}

 

发生此问题的原因可能是 DevOps Services 需要使用 `manifest.yml` 文件将应用程序部署到 {{site.data.keyword.Bluemix_notm}}。
{: tsCauses}

 

要解决此问题，您必须创建 `manifest.yml` 文件。有关如何创建 `manifest.yml` 文件的更多信息，请参阅[应用程序清单](../manageapps/depapps.html#appmanifest){: new_window}。
{: tsResolve}	
	




## 无法推送 Meteor 应用程序
{: #ts_meteor}

如果未正确指定 buildpack，那么可能无法将 Meteor 应用程序推送到 {{site.data.keyword.Bluemix_notm}}。

 

将 Meteor 应用程序部署到 {{site.data.keyword.Bluemix_notm}} 时，您可能会看到错误消息：`应用程序未能编译打包，因此没有要显示的实例。`
{: tsSymptoms}


发生此问题的原因是没有可用于 Meteor 应用程序的内置 buildpack。必须使用定制 buildpack。
{: tsCauses} 


 

要对 Meteor 应用程序使用定制 buildpack，请使用以下其中一种方法：
{: tsResolve}

  * 如果使用 `manifest.yml` 文件来部署应用程序，请使用 buildpack 选项来指定定制 buildpack 的 URL 或名称。例如：
```
  buildpack: https://github.com/Sing-Li/bluemix-bp-meteor 
  ```
  * 如果从命令提示符部署应用程序，请使用 `cf push` 命令并通过 **-b** 选项来指定定制 buildpack。例如：
    ```
	cf push appname -p app_path -b https://github.com/Sing-Li/bluemix-bp-meteor 
	```
	
  

    
## “部署到 {{site.data.keyword.Bluemix_notm}} 按钮”不部署应用程序
{: #deploytobluemixbuttondoesntdeployanapp}

如果您单击“部署到 {{site.data.keyword.Bluemix_notm}}”按钮之后，发现未克隆 Git 存储库或者未部署应用程序，请尝试针对下列问题的故障诊断方法。
  * [无法创建 Bluemix DevOps Services 项目](#project-cannot-be-created)
  * [在 DevOps Services 中找不到 Git 存储库并且无法克隆](#repo-not-found)
  * [在 DevOps Services 中克隆了 Git 存储库，但应用程序未部署到 {{site.data.keyword.Bluemix_notm}}](#repo-cloned-app-not-deployed)
有关如何创建按钮的更多信息，请参阅：创建“部署到 {{site.data.keyword.Bluemix_notm}}”按钮。

### 无法创建 Bluemix DevOps Services 项目
{: #project-cannot-be-created}

如果您发现无法创建 DevOps Services 项目，可能是因为您的 {{site.data.keyword.Bluemix_notm}} 帐户已到期。



单击了**部署到 Bluemix** 按钮，但“创建项目”步骤未成功完成。
{: tsSymptoms} 


您的 {{site.data.keyword.Bluemix_notm}} 帐户可能已到期。
{: tsCauses} 

使用以下其中一种方法可解决该问题：
{: tsResolve}

  * 登录 {{site.data.keyword.Bluemix_notm}} 并更新帐户信息。
  * 再次单击**部署到 Bluemix** 按钮。


### 在 DevOps Services 中找不到 Git 存储库并且无法克隆
{: #repo-not-found}

如果您发现未克隆 Git 存储库，那么可能是该存储库存在问题或者按钮片段存在问题。



单击了**部署到 Bluemix** 按钮，但在 DevOps Services 中找不到 Git 存储库并且无法克隆。“克隆存储库”步骤未成功完成。因此，无法将应用程序部署到 {{site.data.keyword.Bluemix_notm}}。 
{: tsSymptoms} 

发生此问题的原因可能如下：
{: tsCauses} 

  * Git 存储库可能不存在或不可访问。
  * 按钮片段的 HTML 中或 Markdown 中可能存在问题。
  * URL 中可能存在特殊字符、查询参数或碎片等问题，导致无法正常访问 Git 存储库。

使用以下其中一种方法可解决该问题：
{: tsResolve}

  * 验证 Git 存储库是否存在，是否为公共可访问，以及 URL 是否正确。
  * 验证片段中是否没有任何 HTML 或 Markdown 错误。
  * 如果特殊字符、查询参数或碎片导致 Git 存储库的 URL 存在问题，请将该 URL 编码到按钮片段中。
  

  
  
### 在 DevOps Services 中克隆了 Git 存储库，但应用程序未部署到 {{site.data.keyword.Bluemix_notm}}
{: #repo-cloned-app-not-deployed}

如果您发现应用程序未部署，那么可能是存储库中的代码存在问题。
     


单击了**部署到 Bluemix** 按钮，并且在 DevOps Services 中克隆了 Git 存储库，但应用程序未部署到 {{site.data.keyword.Bluemix_notm}}。“部署到 Bluemix”步骤未成功完成。
{: tsSymptoms} 

发生此问题的原因可能如下：
{: tsCauses}  

  * {{site.data.keyword.Bluemix_notm}} 空间中可能没有足够的空间来部署应用程序。 
  * 可能未在 `manifest.yml` 文件中声明必需的服务。
  * 可能在 `manifest.yml` 文件中声明了必需的服务，但该服务已存在于目标空间中。
  * 存储库中的代码可能存在问题。
要诊断问题，请查看该部署的构建和部署日志：
  1. “部署到 Bluemix”步骤未成功完成时，请单击上述“配置管道”步骤中的链接，以打开 Delivery Pipeline。
  2. 识别失败的构建或部署阶段。
  3. 在失败的阶段中，单击**查看日志和历史记录**。
  4. 找到错误消息。
   
使用以下其中一种方法可解决该问题：
{: tsResolve}

  * 如果错误消息指示 {{site.data.keyword.Bluemix_notm}} 空间中的空间不足，无法部署应用程序，那么请使用其他空间作为目标。
  * 如果错误消息指示未在 `manifest.yml` 文件中声明必需的服务，那么请通知存储库所有者必须添加必需的服务。
  * 如果错误消息指示目标空间中已存在必需的服务，那么请选择使用其他空间。
  * 如果错误消息指示构建中存在问题，那么请解决代码中导致无法构建应用程序的任何问题。要验证代码中是否没有任何问题，请使用 Git 命令来构建代码：
    1. 克隆 Git 存储库：
    ```
    git clone <git_repository_URL>
    ```
	2. 打开应用程序目录：
	```
	cd <appname>
	```
	3. 创建应用程序：
	```
	<appname> create
	```
	4. 如果需要，请供应附加组件。
	5. 添加所需的任何配置变量。
	6. 推送代码：
	```
	git push <appname> master
	```
	7. 验证应用程序构建是否正确。
	8. 如果需要，请运行发布部署命令：
	```
	<appname> run
	```
	9. 打开应用程序，验证应用程序是否正常运行：
	```
	<appname> open
	```
	



# 有关管理帐户的故障诊断
{: #managingaccounts}

管理帐户时，可能会遇到问题。例如，不同的应用程序共享同一域名；管理员无法查看所有组织。然而，在许多情况下，只需执行几个简单的步骤即可解决这些问题。
{:shortdesc}


## 帐户不活动
{: #ts_accnt_inactive}

如果您的帐户处于不活动状态，那么无法在 {{site.data.keyword.Bluemix_notm}} 中创建应用程序。 必须联系支持团队来解决此问题。



尝试在 {{site.data.keyword.Bluemix_notm}} 中创建应用程序时，您会看到以下错误消息：
{: tsSymptoms} 

`BXNUI0096E: 未创建应用程序。您的帐户处于不活动状态，因为它已被取消或暂挂。`


当您的 {{site.data.keyword.Bluemix_notm}} 帐户被取消或暂挂时，其状态会变为不活动。
{: tsCauses}

 

要重新激活您的帐户，请联系 [{{site.data.keyword.Bluemix_notm}} 支持](http://ibm.biz/bluemixsupport.com){: new_window}。在该电子邮件中，必须包含以下信息：
{: tsResolve}

  * 您用于登录到 {{site.data.keyword.Bluemix_notm}} 的 IBM 标识。
  * 要在其中创建应用程序的组织的名称。此信息可帮助支持团队确定在您组织内是否为您分配了正确的角色或成员资格。



## 没有空间与当前组织关联
{: #ts_no_space}

如果没有空间与您的当前组织关联，那么无法创建应用程序。



尝试在 {{site.data.keyword.Bluemix_notm}} 中创建应用程序时，您会看到以下错误消息：
{: tsSymptoms} 


`BXNUI0097E: 在添加应用程序之前，必须至少有一个空间与您的组织和区域相关联。在“仪表板”上，单击 **创建空间**。创建空间后，请重试。`



{{site.data.keyword.Bluemix_notm}} 中的应用程序必须在组织下的空间内创建。
{: tsCauses} 

 

要创建空间，请使用以下某种方法： 
{: tsResolve}
 
  * 在 {{site.data.keyword.Bluemix_notm}}“仪表板”上，选择要在其中创建空间的组织，然后单击**创建空间**。
  * 在 cf 命令行界面中，键入 ```cf create-space <space_name> -o <organization_name>```。
  
  
  
  
## 不同应用程序的域名相同
{: #ts_domain_diff}

您可能注意到数个应用程序在 {{site.data.keyword.Bluemix_notm}} 中共享同一 URL。

 

当您为空间内的不同应用程序分配相同 URL 路径时，可能会发生此问题。
{: tsCauses}

例如，将 myApp1 应用程序推送到 {{site.data.keyword.Bluemix_notm}}，并将域设置为“mynewapp.mybluemix.net”。然后，将另一个应用程序 myApp2 推送到同一空间，并将该应用程序的其中一个 URL 路径设置为“mynewapp.mybluemix.net”。现在，该路径映射到两个应用程序。

 

这是 {{site.data.keyword.Bluemix_notm}} 的受支持行为，您可以使用此操作来使应用程序升级时的停机时间为零。有关更多信息，请参阅蓝绿部署。
{: tsResolve}
  
	
	





## 无法添加信用卡
{: #ts_addcc}

无法提交信用卡信息，以将试用帐户转换为“现买现付”帐户。

 

“添加信用卡”页面上的“提交”按钮已禁用。
{: tsSymptoms}

 

在“添加信用卡”页面中未正确填写您的信息时会发生此问题。
{: tsCauses}

 

请完成以下步骤来解决此问题：
{: tsResolve}

  1. 在“添加信用卡”页面上，填写联系人信息、联系人地址和帐单地址部分中的所有必填字段。
  2. 选择**我已阅读并同意 IBM 条款和条件**，然后单击**提交**。此时将显示**选择付款方式**部分。
  3. 输入您的信用卡卡号、信用卡到期日期以及信用卡上的安全代码。然后，单击**提交**。





# 有关运行时的故障诊断
{: #runtimes}

使用 IBM® Bluemix™ 运行时的时候，可能会遇到问题。然而，在许多情况下，只需执行几个简单的步骤即可解决这些问题。
{:shortdesc}


## 推送应用程序时从高速缓存装入了过时的 buildpack
{: #ts_loading_bp}


您可能在推送应用程序时无法使用最新的 buildpack 组件。可以使用具有内置机制的 buildpack 来阻止装入过时的组件，或者可以在推送或重新编译打包应用程序之前，删除应用程序高速缓存目录中的内容。 

 

buildpack 更新后推送或重新编译打包应用程序时，不会自动装入最新的 buildpack 组件。结果应用程序就使用过时的 buildpack 组件。自上次推送应用程序以来已应用到 buildpack 的更新未实施。 
{: tsSymptoms}



某些 buildpack 未配置为从因特网自动下载所有更新的组件，以确保您始终使用最新的版本。
{: tsCauses} 

 

您可以使用具有内置机制的 buildpack 来避免装入过时的组件。以下 buildpack 是 2 个示例： 
{: tsResolve}

  * [Cloud Foundry Java buildpack](https://github.com/cloudfoundry/java-buildpack){: new_window}。此 buildpack 具有内置机制来确保使用 buildpack 的最新版本。有关此机制如何工作的更多信息，请参阅 [extending-caches.md](https://github.com/cloudfoundry/java-buildpack/blob/master/docs/extending-caches.md){: new_window}。 
  * [Cloud Foundry Node.js buildpack](https://github.com/cloudfoundry/nodejs-buildpack){: new_window}。此 buildpack 通过使用环境变量具有类似功能。要使 Node.js buildpack 每次都能够从因特网下载节点模型，请在 cf 命令行界面中键入以下命令： 	
  ```
  set NODE_MODULES_CACHE=false
  ```
如果您使用的 buildpack 不提供自动装入最新组件的机制，那么您可以手动删除高速缓存目录中的内容，并通过执行以下步骤重新推送应用程序：
  1. 检出空 buildpack 的分支，例如 https://github.com/ryandotsmith/null-buildpack。有关如何检出分支的信息，请参阅 [Git Basics - Getting a Git Repository](http://www.git-scm.com/book/en/v2/Git-Basics-Getting-a-Git-Repository){: new_window}。  
  2. 将以下行添加到 `null-buildpack/bin/compile` 文件，并落实更改。有关如何落实更改的信息，请参阅 [Git Basics - Recording Changes to the Repository](http://www.git-scm.com/book/en/v2/Git-Basics-Recording-Changes-to-the-Repository){: new_window}。
  ```
  rm -rfv $2/*
  ```
  3. 通过使用以下命令，使用修改用于删除高速缓存的空 buildpack 推送应用程序。完成此步骤后，会删除应用程序高速缓存目录中的所有内容。
  ```
  cf push appname -p app_path -b <modified_null_buildpack>
  ```
  4. 通过使用以下命令，使用想要使用的最新 buildpack 推送应用程序： 
  ```
  cf push appname -p app_path -b <latest_buildpack>
  ```
  
	


## 来自 PHP buildpack 的注意消息
{: #ts_phplog}

您可能会在日志中看到包含“注意”的消息。通过更改日志记录级别，可以停止记录这些消息。	
	
 

使用 PHP buildpack 将应用程序推送到 Bluemix 时，可能会看到包含`注意`的消息：
{: tsSymptoms}

```
• 2015-01-26T15:00:59.70+0100 [App/0] 错误 [26-Jan-2015 14:00:59] 注意：[pool www] 当 FPM 未以 root 用户身份运行时，会忽略“user”伪指令
• 2015-01-26T15:01:00.63+0100 [App/0] 错误 [26-Jan-2015 14:00:59] 注意：[pool www] 当 FPM 未以 root 用户身份运行时，会忽略“user”伪指令
• 2015-01-26T15:01:00.63+0100 [App/0] 错误 [26-Jan-2015 14:00:59] 注意：fpm 正在运行，pid 93
• 2015-01-26T15:01:00.63+0100 [App/0] 错误 [26-Jan-2015 14:00:59] 注意：准备就绪，可处理连接
```



在 PHP buildpack 中，error_log 参数用于定义日志记录级别。缺省情况下，`error_log` 参数的值为 **stderr notice**。以下示例显示 Cloud Foundry 所提供的 PHP buildpack 的 `nginx-defaults.conf` 文件中的缺省日志记录级别配置。有关更多信息，请参阅 [cloudfoundry/php-buildpack](https://github.com/cloudfoundry/php-buildpack/blob/ff71ea41d00c1226d339e83cf2c7d6dda6c590ef/defaults/config/nginx/1.5.x/nginx-defaults.conf){: new_window}。
{: tsCauses} 

```
daemon off;
error_log stderr notice;
pid @{HOME}/nginx/logs/nginx.pid;
```

 	
	
`注意`消息可供参考，但未必表明发生问题。要停止记录这些消息，可以将 buildpack 的 nginx-defaults.conf 文件中的日志记录级别从 stderr notice 更改为 stderr error。例如： 	
{: tsResolve}

```
daemon off;
error_log stderr error;
pid @{HOME}/nginx/logs/nginx.pid;
```
有关如何更改缺省日志记录配置的更多信息，请参阅 [error_log](http://nginx.org/en/docs/ngx_core_module.html#error_log){: new_window}。
	

## 无法将第三方 Python 库导入到 {{site.data.keyword.Bluemix_notm}}
{: #ts_importpylib}

您可能无法将第三方 Python 库导入到 {{site.data.keyword.Bluemix_notm}}。通过将配置文件添加到 Python 应用程序的根目录中，可以解决此问题。


当您尝试导入第三方 Python 库（如 `web.py` 库）时，`cf push` 命令会失败。
{: tsSymptoms}


 

在 Python 应用程序缺少配置信息的情况下，会发生此问题。
{: tsCauses}


 

要解决该问题，请将 `requirements.txt` 文件和 `Procfile` 文件添加到 Python 应用程序的根目录中。以下信息假定您要导入 web.py 库：
{: tsResolve}

  1. 将 `requirements.txt` 文件添加到 Python 应用程序的根目录中。
     `requirements.txt` 文件指定 Python 应用程序所需的库数据包以及数据包版本。以下示例显示的是 `requirements.txt` 文件的内容，其中 `web.py==0.37` 指示要下载的 `web.py` 库版本为 0.37，而 `wsgiref==0.1.2` 指示 web.py 库所需的 Web 服务器网关接口版本为 0.1.2。
	 ```
	 web.py==0.37
     wsgiref==0.1.2
	 ```
	有关如何配置 `requirements.txt` 文件的更多信息，请参阅 [Requirements files](https://pip.readthedocs.org/en/1.1/requirements.html)。 
	 
  2. 将 `Procfile` 文件添加到 Python 应用程序的根目录中。
`Procfile` 文件中必须包含 Python 应用程序的 start 命令。在以下命令中，*yourappname* 是 Python 应用程序的名称，*PORT* 是 Python 应用程序在接收应用程序用户请求时必须使用的端口号。*$PORT* 为可选项。如果不在 start 命令中指定 PORT，那么会改用应用程序中 `VCAP_APP_PORT` 环境变量下的端口号。
	```
	web: python <yourappname>.py $PORT
	```
现在，您可以将第三方 Python 库导入到 {{site.data.keyword.Bluemix_notm}}。	



## 实例详细信息页面上的操作按钮已禁用
{: #ts_actionsbutton}



“实例详细信息”页面上的“操作”按钮已禁用。
{: tsSymptoms} 

 

发生此问题的原因如下：
{: tsCauses}

  * 应用程序不是 Java™ Web 应用程序。“运行时管理实用程序 (RMU)”仅支持使用 Liberty buildpack 部署的 Web 应用程序。
  * 未使用嵌入式 Liberty buildpack 部署应用程序。
  * 使用早期版本 Liberty buildpack 部署应用程序。



如果该问题是由早期版本的 Liberty buildpack 导致的，请在 {{site.data.keyword.Bluemix_notm}} 中重新部署应用程序。否则，您可以向支持团队提供以下客户机应用程序日志文件：
{: tsResolve} 

  * logs/messages.log
  * logs/stdout.log
  * logs/stderr.log
  

  
  
## 打开跟踪或转储窗口时需要凭证
{: #ts_username}


 

打开跟踪和转储窗口时需要用户名和密码。
{: tsSymptoms}

 

由于登录会话超时，发生此问题。
{: tsCauses}

 

解决方案是重新输入用户名和密码。
{: tsResolve}




## 正在执行跟踪或转储操作时发生错误
{: #ts_target}

 

正在执行跟踪或转储操作时显示错误消息。该消息指示应用程序的目标实例未处于运行中状态：	
{: tsSymptoms}

```
实例 0：已成功设置跟踪规范
实例 2：已成功设置跟踪规范
实例 1：应用程序 abcd 的目标实例 1 未处于运行中状态。
实例 3：已成功设置跟踪规范
实例 4：已成功设置跟踪规范
```



发生此问题的原因如下：
{: tsCauses} 

  * 跟踪或转储管理功能仅用于正在运行的应用程序实例。无法在已停止、正在启动或已崩溃的应用程序实例上使用跟踪或转储操作。
  * 跟踪或转储对话框已打开时，应用程序实例的状态正在更改。 
  


解决方案是关闭窗口，然后重新打开。
{: tsResolve} 



## 实例具有不同的 traceSpecification 配置
{: #ts_different_config}

 

对于一个应用程序的不同实例，您可能会看到不同的 traceSpecification 配置。
{: tsSymptoms}

 

发生此问题的原因如下：
{: tsCauses}

  * 您先前可能更改了一个或多个实例的配置。更改一个实例的 traceSpecification 配置后，该更改并不会应用到同一应用程序的其他实例。例如，您的应用程序使用 log4j，并且此应用程序有 2 个实例。您可以将实例 0 的日志级别从信息更改为调试，但实例 1 的日志级别仍为信息。 
  * 应用程序向外扩展后有了新的实例。RMU 不会将现有实例的 traceSpecification 配置应用到向外扩展的新实例。新实例会使用缺省配置。例如，您的应用程序使用 log4j，并且此应用程序有 1 个实例。您可以将此实例的日志级别从信息更改为调试。进行此更改后，如果将应用程序向外扩展到 2 个实例，那么新实例的日志级别将为信息，而不是调试。
  


这是正常的情况。
{: tsResolve} 





## 超出磁盘配额
{: #ts_diskquota}

您可能会在应用程序日志中看到超过磁盘配额的消息。

 

您在应用程序日志中看到`超过磁盘配额`错误消息。
{: tsSymptoms}



此问题由以下某个原因导致： 
{: tsCauses} 

  * 生成转储文件，包含运行中的应用程序实例，且文件用完分配的磁盘配额。缺省情况下，一个应用程序实例的磁盘配额是 1 GB。您可以通过单击**仪表板>应用程序>应用程序运行时**来检查磁盘使用情况。以下示例显示某个应用程序的两个实例的运行时信息，包括磁盘使用情况：
    ```
    实例状态	CPU	内存使用情况 磁盘使用情况

	0		运行中	1.0%	344.8MB/512MB	236.8MB/1GB
	2		运行中	2.3%	361.2MB/512MB	235.7MB/1GB
    ```
  * 磁盘配额受当前组织配额限制。
  
  


您可以使用以下一种方法来解决此问题：
{: tsResolve} 

  * 下载转储文件后将其删除。
  * 通过将以下条目包含在部署清单中，使用更大的磁盘配额重新部署应用程序：
    ```
	disk_quota：2048
	```
	
	


