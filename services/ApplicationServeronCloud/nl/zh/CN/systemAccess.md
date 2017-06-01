---

copyright:
  years: 2015, 2016
lastupdated: "2017-02-24"

---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}

#系统访问
{: #system_access}


本部分讨论了创建和管理服务实例的方法以及访问系统和设置系统访问权的各种方法。
{: shortdesc}


## WebSphere Application Server in {{site.data.keyword.Bluemix_notm}} 中的 REST API 用法
{: #restapi_usage}

您可以使用以下其中一种方法创建、供应、管理和删除 WebSphere Application Server in {{site.data.keyword.Bluemix_notm}} 中的实例：

* 通过 {{site.data.keyword.Bluemix_notm}} UI 中的 {{site.data.keyword.Bluemix_notm}} 目录和服务仪表板。
* 通过创建使用 RESTful API 的应用程序或脚本。

通过使用符合 Swagger 2.0 的 REST API，客户可使用与门户网站和仪表板所提供的功能相同的功能。有关支持的 REST API 和资源的更多信息，请参阅 WebSphere Application Server in {{site.data.keyword.Bluemix_notm}} [REST API 文档](https://wasaas-broker.ng.bluemix.net/wasaas-broker/api#/){: new_window}。有关演示 REST API 用法的样本代码，请下载 Git 托管的 WebSphere Application Server in {{site.data.keyword.Bluemix_notm}} [REST API 样本](https://github.com/IBM-Bluemix/WebSphere-for-Bluemix-API-Usage){: new_window}。

**注：**创建服务实例之后，根据创建的 T 恤尺寸，可能无法立即使用您的服务。建议您查询 JSON 返回的**状态**字段，以确定服务实例的当前状态。

**注：**[REST API 样本](https://github.com/IBM-Bluemix/WebSphere-for-Bluemix-API-Usage){: new_window}中引用的 **apiEndpoint** URL 指向美国南部区域。如果您使用的是其他区域，请确保您的应用程序引用相应的 **apiEndpoint**。

*表 1. Rest API 实现的 API 端点 URL*

| **区域名称** | **地理位置** | **区域前缀** | **API 端点 URL** |       
|:-------------:|:----------:|:--------------:|:-------------:|
| 美国南部 | 美国得克萨斯州达拉斯 | ng | https://wasaas-broker.ng.bluemix.net/wasaas-broker/api  |
| 英国 | 英国伦敦 | eu-gb | https://wasaas-broker.eu-gb.bluemix.net/wasaas-broker/api  |
| 悉尼 | 澳大利亚悉尼 | au-syd | https://wasaas-broker.au-syd.bluemix.net/wasaas-broker/api  |
| 法兰克福 | 德国法兰克福 | eu-de | https://wasaas-broker.eu-de.bluemix.net/wasaas-broker/api  |



## 服务仪表板
{: #service_dashboard}

创建服务实例后，会将您带入服务仪表板。您可以始终通过单击组织仪表板中的服务图标，返回到服务仪表板。从服务仪表板，您可以访问：

* 此文档的链接
* 用于下载所需 OpenVPN 配置文件的链接
* 启动和停止虚拟机的能力。VM 初始启动
* 主机名
* 管理用户和管理密码
* 私有 SSH 密钥
* WebSphere® 管理用户和管理密码
* 管理中心和管理控制台 URL

**注**：根据特定的计算、内存和 I/O 资源量，对于处于“已停止”状态的累计 VM，我们会向客户减免 5%。客户的固定“已停止”实例数将会控制为 10 个 IP 地址或 64 GB 内存以内。


## 为 WebSphere Application Server in Bluemix 实例设置 openVPN
{: #setup_openvpn}

需要 OpenVPN 才能访问 Bluemix 虚拟机上的任何 WebSphere Application Server。必须使用管理员权限进行安装和运行。

### 使用以下指示信息，在 Windows 中设置 openVPN：

1. 通过 [openVPN Windows 下载](http://swupdate.openvpn.org/community/releases/)链接，下载
  * [openvpn-install-2.3.4-I001-x86_64.exe](https://swupdate.openvpn.org/community/releases/openvpn-install-2.3.4-I001-x86_64.exe){: new_window}（适用于 64 位），或
  * [openvpn-install-2.3.4-I001-i686.exe](https://swupdate.openvpn.org/community/releases/openvpn-install-2.3.4-I001-i686.exe){: new_window}（适用于 32 位）。
2. 确保[以 Windows 管理员身份运行](https://technet.microsoft.com/en-us/magazine/ff431742.aspx){: new_window}，并安装 openVPN。
3. 在服务仪表板中，使用 WebSphere Application Server in Bluemix 实例的 OpenVPN 下载链接下载 VPN 配置文件。将压缩文件中的全部 4 个文件解压缩到 **{OpenVPN home}\config** 目录。例如：

  <pre>  
C:\Program Files\OpenVPN\Config  </pre>
  {: codeblock}

4. 启动 openVPN 客户端程序“OpenVPN GUI”。确保选择[以 Windows 管理员身份运行](https://technet.microsoft.com/en-us/magazine/ff431742.aspx){: new_window}来启动程序。如果不以管理员身份运行，您可能无法连接。

### 使用以下指示信息，在 Linux 中设置 openVPN：
1. 要安装 openVPN，请遵循[指示信息](https://openvpn.net/index.php/access-server/docs/admin-guides/182-how-to-connect-to-access-server-with-linux-clients.html){: new_window}。
  * 如果需要手动下载并安装 RPM 软件包管理器，请转至 [openVPN unix/linux 下载](https://openvpn.net/index.php/access-server/download-openvpn-as-sw.html){: new_window}。您可能需要 Linux 管理员的帮助。
3. 在服务仪表板中，使用 WebSphere Application Server in Bluemix 实例的 OpenVPN 下载链接下载 VPN 配置文件。将文件解压缩到要从中启动 openVPN 客户端的目录。需要全部 4 个文件位于相同目录。
3. 启动 openVPN 客户端程序。打开终端窗口，并转至包含配置文件的目录。以 root 用户身份运行以下命令：

  <pre>
$ openvpn --config vt-wasaas-wasaas.ovpn  </pre>
  {: codeblock}  

### 使用以下指示信息，在 Mac 中配置 openVPN：
1. 一种方法是安装 [Tunnelblick](https://tunnelblick.net/){: new_window}（开放式源代码软件产品）。
2. 从 WebSphere 服务抽取 VPN 配置文件。Tunnelblick 提示您输入 Mac 的管理密码，并将配置添加到可以用来连接的 VPN 集。
3. 连接到 VPN 网络，然后可以访问虚拟机。第一次访问后，Tunnelblick 会缓存配置，并且您可以从 [Tunnelblick](https://tunnelblick.net/){: new_window} 连接。您可以将图标放在顶部菜单栏以方便访问。


## 使用 SSH 访问 WebSphere Application Server in Bluemix VM
{: #using_ssh}

这些指示信息假定您使用的是 OpenSSH 作为客户端。OpenSSH 通常适用于 Linux，也适用于在 Windows 上运行的 Cygwin。您还可以安装 OpenSSH，以从 Windows 命令提示符运行。

要验证 OpenSSH 的安装信息，请输入命令：
  
  ```
$ ssh -V
  ```
  {: codeblock}

以下消息是响应示例：
  ```
OpenSSH_6.6p1, OpenSSL 1.0.1g 7 Apr 2014
  ```
  {: codeblock}

使用以下指示信息，设置 WebSphere Application Server in Bluemix VM 的 SSH 访问权：

1. 查看在您第一次连接时出现的警告消息“无法确定主机 x.x.x.x 的真实性”。此消息是正常的。在出现提示时，选择 yes。此时将在 VM 上为用户 virtuser 安装公用密钥。
2. 使用专用密钥登录 virtuser。为了获取最佳结果，请使用专用密钥认证方法。
3. 将专用密钥的内容复制到文件。
4. 运行命令：

  <pre>
$ ssh virtuser@169.53.246.xxx -i /path/privateKeyFileName  </pre>
  {: codeblock}

5. 使用以下命令，将 virtuser 切换为 root 用户，以获取完整的 sysadmin 权限：

  <pre>
$ sudo su root  </pre>
  {: codeblock}

6. 如果您在使用专用 SSH 密钥访问系统时遇到问题，请使用提供的 root 密码。运行以下命令，以 root 用户身份登录，并提供密码。

 <pre>
$ ssh root@169.53.246.x  </pre>
  {: codeblock}

7. 无论是使用专用 SSH 密钥还是 root 密码访问系统，请立即更改 root 密码。
8. 要简化 SSH 命令，请在 %HOME%/.ssh 目录中创建名为“config”的文件。例如：

  <pre>
Host VM1
Hostname 169.53.246.xxx
User virtuser
IdentityFile /path/privateKeyFileName  </pre>
  {: codeblock}

9. 运行“ssh VM1”，并以 virtuser 进行连接。

## 系统路径
{: #system_paths}

* 可以从 */opt/IBM/WebSphere/Liberty/bin* 发出 Liberty Profile 命令。
* Liberty Profile 服务器概要文件位置为 */opt/IBM/WebSphere/Profiles/Liberty/servers/server1*。
* 可以从 */opt/IBM/WebSphere/AppServer/bin* 发出传统 WebSphere Application Server 命令。
* 服务器的传统 WebSphere Application Server 概要文件位置为 */opt/IBM/WebSphere/Profiles/DefaultAppSrv01/servers/server1*。

## 使用管理中心和管理控制台链接
{: #console_links}

当您单击管理中心或管理控制台的链接时，可能会收到*不可信的连接*警告。确切的消息文本会因浏览器不同而有所不同，按照以下确切的步骤忽略或消除该警告。

因为您使用的是 {{site.data.keyword.IBM}} 提供的链接，所以可以放心忽略该警告并进行连接。如果您的浏览器提供存储安全性异常的操作，那么执行该操作是防止未来出现该警告的最简便方法。

另一种选择是导出入局签署者证书，然后将其导入浏览器中作为可信根证书。此种选择可能需要您在 *hosts* 文件中添加条目，以便将 VM 的 IP 地址映射到证书发行方的通用名称。此名称采用以下格式：wl<pureapplication.ibmcloud.com。如果您现在在 URL 中使用主机名而非 IP 地址，那么应该正常连接。然后必须在 URL 中使用该主机名而非 IP 地址来访问管理中心或管理控制台。

最后，客户通常会为外部应用程序安装他们自己的根证书。有关更多信息，请参阅 [WebSphere Application Server](http://www.ibm.com/support/knowledgecenter/SSEQTP_8.5.5/com.ibm.websphere.base.doc/ae/tsec_securecomm.html?cp=SSEQTP_8.5.5%2F1-11-2-6&lang=en){: new_window} 或 [Liberty Core](http://www.ibm.com/support/knowledgecenter/SSD28V_8.5.5/com.ibm.websphere.wlp.core.doc/ae/twlp_sec_comm.html?lang=en){: new_window} IBM Knowledge Center。

## 防火墙端口
{: #firewall_ports}

您可能发现有必要打开防火墙上的端口，以允许访问应用程序和数据库。
  * 在每个 WebSphere Application Server in Bluemix 节点上，您会在 WAS_HOME/virtual/bin 目录中找到脚本 openFirewallPorts.sh。
  * 在每个 Liberty 集合主机上，您会在 WAS_HOME/virtual/bin 目录中找到脚本 openFirewallPorts.sh。

用法：
  ```
$ openFirewallPorts.sh -ports <PORT>:<PROTOCOL>,... -persist true|false
  ```
  {: codeblock}

* PORT 是端口号
* PROTOCOL 是 TCP 或 UDP
* -persist 为 true 或 false

要指定多个端口，请使用逗号“,”进行分隔。

**注**：所有打开端口的 sport 和 dport 已在防火墙的 INPUT 和 OUTPUT 部分打开。您必须使用 sudo 以 root 用户身份运行此脚本。还可以直接修改 iptables。

## 配置 Web 服务器
{: #configure_webserver}

供应单元或集合时，您收到预配置环境。尤其是对于传统 Network Deployment 单元，您收到以下环境：

* 与 IBM HTTP Server 并置的 Deployment Manager，用于开发和测试目的。

* 联合到 Deployment Manager 的定制节点。

* 全部初始供应到 STARTED 状态的 Deployment Manager、IHS Server 和 Node Agent。

如果您需要 Web 服务器处理所有用户请求，那么您在部署应用程序之后可能需要生成和传播插件。

**避免问题：**生成和传播插件之前，确保完成以下先决条件任务：

* 在本地 Windows、Linux 或 MAC 环境下，确保已配置 [openVPN](systemAccess.html#setup_openvpn) 并启动，并且您已经连接到相应的区域。

* 从 WebSphere Application Server in {{site.data.keyword.Bluemix_notm}} 服务仪表板中，单击**打开管理控制台**，并使用服务仪表板中提供的 wsadmin 和管理员密码登录。

* 从管理控制台，创建应用程序服务器（例如，***server1***），因为 Deployment Manager 是使用空的定制节点联合的。

* 启动所创建的服务器。

* 在应用程序安装期间，确保应用程序模块映射到您刚刚启动的服务器和 Web 服务器（例如，***webserver1***）。

以下高级步骤假定先决条件任务已完成：

1. 在“管理控制台”从“环境”选项生成插件：
   1. 选择“环境”>“更新全局 Web 服务器插件配置”
   2. 单击**确定**或者**覆盖以生成新插件配置文件**
2. 从 Deployment Manager，将插件复制到 Web 服务器配置：

  ```
   cp /opt/IBM/WebSphere/Profiles/DefaultDmgr01/config/cells/plugin-cfg.xml /opt/IBM/WebSphere/Plugins/config/webserver1/plugin-cfg.xml
  ```
  {: codeblock}
3. 在 **IHS_HOME/conf** 中编辑 **httpd.conf**（例如，*/opt/IBM/WebSphere/HTTPServer/conf*），并确保以下两行存在：

    ```
    LoadModule was_ap22_module /opt/IBM/WebSphere/Plugins/bin/64bits/mod_was_ap22_http.so
    WebSpherePluginConfig /opt/IBM/WebSphere/Plugins/config/webserver1/plugin-cfg.xml
    ```
    {: codeblock}  
4. 使用这两个命令打开端口：

  ```
   export serverPorts=2810:TCP,2810:UDP,8880:TCP,8880:UDP,9101:TCP,9101:UDP,9061:TCP,9061:UDP,9080:TCP,9080:UDP,9354:TCP,9354:UDP,9044:TCP,9044:UDP,9443:TCP,9443:UDP,5060:TCP,5060:UDP,5061:TCP,5061:UDP,11005:TCP,11005:UDP,11007:TCP,11007:UDP,9633:TCP,9633:UDP,7276:TCP,7276:UDP,7286:TCP,7286:UDP,5558:TCP,5558:UDP,5578:TCP,5578:UDP

   sudo /opt/IBM/WebSphere/AppServer/virtual/bin/openFirewallPorts.sh -ports $serverPorts -persist true
  ```
    {: codeblock}
5. 使用以下两个命令停止和启动 Web 服务器：
    ```
    sudo /opt/IBM/WebSphere/HTTPServer/bin/apachectl -k stop
    sudo /opt/IBM/WebSphere/HTTPServer/bin/apachectl -k start
    ```
    {: codeblock}
8. 通过插件访问应用程序：
  ```
   http://169.53.246.xxx/contextRoot/
  ```
  {: codeblock}

**注：**所提供的步骤显示您在尝试配置 Web 服务器时许多路径中的一个。如果需要更多帮助，请参阅 [IBM Knowledge Center](https://www.ibm.com/support/knowledgecenter/search/configure%20web%20server?scope=SSAW57_9.0.0){: new_window}。

**注：**如果您无法访问应用程序，可能遇到有关防火墙的端口访问问题。因此，您可能需要重新启动以下任一服务器：应用程序服务器、节点代理程序、Web 服务器和部署管理器。此外，您可能还需要访问 WebSphere Application Server in {{site.data.keyword.Bluemix_notm}} 服务仪表板并重新启动每个虚拟机。

## SSL 配置
{: #ssl_configuration}

传统 WebSphere Application Server 和 Liberty 概要文件是使用 [SSL_TLSv2](https://www.ibm.com/support/knowledgecenter/en/SSYKE2_8.0.0/com.ibm.java.security.component.80.doc/security-component/jsse2Docs/protocols.html){: new_window} 协议配置的。要更改协议，请修改以下文件：

对于传统 WebSphere Application Server：

1. 编辑 *profile_name*/config/cell/*cell_name* 中的 **security.xml**，并修改以下行：

  ```
  sslProtocol="SSL_TLSv2"
  ```
{: codeblock}

2. 编辑 /opt/IBM/WebSphere/Profiles/*profile_name*/properties 中的 **ssl.client.props**，并修改以下行：

  ```
  com.ibm.ssl.protocol=SSL_TLSv2
  ```
{: codeblock}

对于 Liberty 概要文件：

1. 编辑 /opt/IBM/WebSphere/Profiles/Liberty/servers/server1 中的 **server.xml**，并修改 defaultSSLConfig ssl 配置元素中的以下行：

  ```
  sslProtocol="SSL_TLSv2"
  ```
{: codeblock}
