---

copyright:
  years: 2015, 2016

---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}

#系统访问
{: #system_access}
以下主题包含如何创建和管理服务实例的方法以及如何访问系统并设置访问权的多种方法。
{: shortdesc}

*上次更新时间：2016 年 6 月 8 日*
{: .last-updated}

## WebSphere Application Server for {{site.data.keyword.Bluemix_notm}} 中的 REST API 用法
{: #restapi_usage}

您可以使用以下其中一种方法创建、供应、管理和删除 WebSphere Application Server for {{site.data.keyword.Bluemix_notm}} 中的实例：

* 通过 {{site.data.keyword.Bluemix_notm}} UI 中的 {{site.data.keyword.Bluemix_notm}} 目录和服务仪表板。
* 通过创建使用了我们提供的 RESTful API 的应用程序或脚本。

使用我们提供的符合 Swagger 2.0 的 REST API，客户可访问通过门户网站和仪表板提供的相同功能。有关支持的 REST API 和资源的更多信息，请参阅 WebSphere Application Server for {{site.data.keyword.Bluemix_notm}} [REST API 文档](https://new-console.{DomainName}/apidocs/212){: new_window}。

**注：**创建服务实例之后，根据创建的 T 恤型号，可能无法立即使用您的服务。建议您查询 JSON 返回的**状态**字段，以确定服务实例的当前状态。

**注：**缺省情况下，API BASE URL 指向[美国南部区域](https://wasaas-broker.ng.bluemix.net/wasaas-broker/api/v1){: new_window}中的端点。如果您使用英国或悉尼区域，请确保应用程序使用以下某个端点：

* [英国区域](https://wasaas-broker.eu-gb.bluemix.net/wasaas-broker/api/v1){: new_window}
* [悉尼区域](https://wasaas-broker.au-syd.bluemix.net/wasaas-broker/api/v1){: new_window}


## 服务仪表板
{: #service_dashboard}

创建服务实例后，会将您带入服务仪表板。您可以始终通过单击组织仪表板中的服务图标，返回到服务仪表板。从服务仪表板，您可以访问：

*  此文档的链接
*  用于下载所需 OpenVPN 配置文件的链接。
*  启动和停止虚拟机的能力。VM 初始启动。
*  主机名。
*  管理用户和管理密码。
*  私有 SSH 密钥。
*  WebSphere® 管理用户和管理密码。
*  管理中心和管理控制台 URL。

**注**：根据特定的计算、内存和 I/O 资源量，对于处于“已停止”状态的累计 VM，我们会向客户减免 5%。客户的固定“已停止”实例数将会控制为 10 个 IP 地址或 64 GB 内存以内。


## 为 WebSphere Application Server for Bluemix 实例设置 openVPN
{: #setup_openvpn}

需要 OpenVPN 才能访问 Bluemix 虚拟机上的任何 WebSphere Application Server。必须先安装 OpenVPN，并且以管理员权限运行。  

### 使用以下指示信息，在 Windows 中设置 openVPN：

1. 通过 [openVPN Windows 下载](http://swupdate.openvpn.org/community/releases/)链接，下载
  * [openvpn-install-2.3.4-I001-x86_64.exe](https://swupdate.openvpn.org/community/releases/openvpn-install-2.3.4-I001-x86_64.exe){: new_window}（适用于 64 位），或
  * [openvpn-install-2.3.4-I001-i686.exe](https://swupdate.openvpn.org/community/releases/openvpn-install-2.3.4-I001-i686.exe){: new_window}（适用于 32 位）。
2. 确保[以 Windows 管理员身份运行](https://technet.microsoft.com/en-us/magazine/ff431742.aspx){: new_window}，然后安装 openVPN。
3. 在服务仪表板中，使用 WebSphere Application Server for Bluemix 实例的 OpenVPN 下载链接下载 VPN 配置文件。将压缩文件中的全部 4 个文件解压缩到 **{OpenVPN home}\config** 目录。例如：

  <pre>  
C:\Program Files\OpenVPN\Config  </pre>
  {: codeblock}

4. 启动 openVPN 客户端程序“OpenVPN GUI”。确保选择[以 Windows 管理员身份运行](https://technet.microsoft.com/en-us/magazine/ff431742.aspx){: new_window}来启动程序。如果不以管理员身份运行，您可能无法连接。

### 使用以下指示信息，在 Linux 中设置 openVPN：
1. 要安装 openVPN，请遵循以下[指示信息](https://openvpn.net/index.php/access-server/docs/admin-guides/182-how-to-connect-to-access-server-with-linux-clients.html){: new_window}。
  * 如果需要手动下载并安装 RPM 软件包管理器，请转至 [openVPN unix/linux 下载](https://openvpn.net/index.php/access-server/download-openvpn-as-sw.html){: new_window}。您可能需要 Linux 管理员的帮助。
3. 在服务仪表板中，使用 WebSphere Application Server for Bluemix 实例的 OpenVPN 下载链接下载 VPN 配置文件。将文件解压缩到您计划要从中启动 openVPN 客户端的目录。需要全部 4 个文件位于相同目录。
3. 启动 openVPN 客户端程序。打开终端窗口，并转至包含配置文件的目录。以 root 用户身份运行以下命令：

  <pre>
$ openvpn --config vt-wasaas-wasaas.ovpn  </pre>
  {: codeblock}  

### 使用以下指示信息，在 Mac 中设置 openVPN：
1. 一种方法是安装 [Tunnelblick](https://tunnelblick.net/){: new_window}（开放式源代码软件产品）。
2. 从 WebSphere 服务抽取 VPN 配置文件。Tunnelblick 提示您输入 Mac 的管理密码，并将配置添加到可以用来连接的 VPN 集。
3. 连接到 VPN 网络，然后可以访问虚拟机。第一次访问后，Tunnelblick 会缓存配置，并且您可以从 [Tunnelblick](https://tunnelblick.net/){: new_window} 连接。您可以将图标放在顶部菜单栏以方便访问。


## 使用 SSH 访问 WebSphere Application Server for Bluemix VM
{: #using_ssh}

这些指示信息假定您使用的是 OpenSSH 作为客户端。OpenSSH 通常适用于 Linux，也适用于在 Windows 上运行的 Cygwin。您还可以安装 OpenSSH，以从 Windows 命令提示符运行。

要验证 OpenSSH 的安装信息，请输入命令：
  ```
$ ssh -V
  ```
  {: codeblock}

您将收到以下类似响应：
  ```
OpenSSH_6.6p1, OpenSSL 1.0.1g 7 Apr 2014
  ```
  {: codeblock}

使用以下指示信息，设置 WebSphere Application Server for Bluemix VM 的 SSH 访问权：

1. 查看在您第一次连接时出现的警告消息“无法确定主机 x.x.x.x 的真实性”。这是正常现象。在出现提示时，选择 yes。此时将在 VM 上为用户 virtuser 安装公用密钥。
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

最后，客户通常会为外部应用程序安装他们自己的根证书。有关更多信息，请参阅 [WebSphere Application Server](http://www.ibm.com/support/knowledgecenter/SSEQTP_8.5.5/com.ibm.websphere.base.doc/ae/tsec_securecomm.html?cp=SSEQTP_8.5.5%2F1-11-2-6&lang=en){: new_window} 或 [Liberty Core](http://www.ibm.com/support/knowledgecenter/SSD28V_8.5.5/com.ibm.websphere.wlp.core.doc/ae/twlp_sec_comm.html?lang=en){: new_window} Knowledge Center。

## 防火墙端口
{: #firewall_ports}

您可能发现有必要打开防火墙上的端口，以允许访问应用程序和数据库。
  * 在每个 WebSphere Application Server for Bluemix 节点上，您会在 WAS_HOME/virtual/bin 目录中找到脚本 openFirewallPorts.sh。
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

**注**：所打开端口的 sport 和 dport 已在防火墙的 INPUT 和 OUTPUT 部分打开。您必须使用 sudo 以 root 用户身份运行此脚本。还可以直接修改 iptables。
