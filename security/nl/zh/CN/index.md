---



copyright:

  years: 2014, 2017

lastupdated: "2017-01-10"

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}

# {{site.data.keyword.Bluemix_notm}} 安全
{: #security}

{{site.data.keyword.Bluemix}} 平台是使用安全工程实践进行设计的，通过不同的层对整个网络和基础架构中的安全进行控制。{{site.data.keyword.Bluemix_notm}} 提供了一组安全服务，应用程序开发者可以使用这些服务来保护自己的移动和 Web 应用程序。这些优势组合在一起，使 {{site.data.keyword.Bluemix_notm}} 平台成为安全应用程序开发的不二选择。
{:shortdesc}

{{site.data.keyword.Bluemix_notm}} 遵循由 IBM 中的最佳做法驱动的系统、网络和安全工程方面的安全策略，从而确保安全就绪性。这些策略包括源代码扫描、动态扫描、威胁建模和渗透测试等做法。{{site.data.keyword.Bluemix_notm}} 遵循 IBM 产品安全事件响应小组 (PSIRT) 的安全事件管理流程。有关详细信息，请参阅 [IBM Security Vulnerability Management (PSIRT) ![外部链接图标](../icons/launch-glyph.svg "外部链接图标")](http://www-03.ibm.com/security/secure-engineering/process.html){: new_window} 站点。

{{site.data.keyword.Bluemix_notm}} Public 和 Dedicated 使用 {{site.data.keyword.BluSoftlayer}} 基础架构即服务 (IaaS) 云服务，并充分利用了其安全体系结构。{{site.data.keyword.BluSoftlayer}} IaaS 提供了多个重叠层来保护应用程序和数据。对于 {{site.data.keyword.Bluemix_notm}} Local，通过在位于公司防火墙后您自己的数据中心托管 {{site.data.keyword.Bluemix_notm}} Local，您可以拥有物理安全并提供基础架构。此外，{{site.data.keyword.Bluemix_notm}} 还在“平台即服务”层添加了不同类别（平台、数据和应用程序）的安全功能。

## {{site.data.keyword.Bluemix_notm}} 平台安全
{: #platform-security}

{{site.data.keyword.Bluemix_notm}} 为核心平台提供了功能性、基础架构、操作和物理安全（通过 {{site.data.keyword.BluSoftlayer}}）。但是，{{site.data.keyword.Bluemix_notm}} Local 的独特之处在于客户会提供基础架构和数据中心，并拥有物理安全。

基于 {{site.data.keyword.BluSoftlayer}} 的 {{site.data.keyword.Bluemix_notm}} 环境符合最严格的 IBM 信息技术 (IT) 安全标准，这些标准已达到或超过业界标准。这些标准包括以下方面：网络、数据加密和访问控制
 * 应用程序 ACL、许可权和渗透测试
 * 识别、认证和授权
 * 信息和数据保护
 * 服务完整性和可用性
 * 漏洞和修订管理
 * 拒绝服务和系统化攻击检测
 * 安全事件响应

![Bluemix 平台安全概况](images/platform_sec.svg)

图 1. {{site.data.keyword.Bluemix_notm}} 平台安全概况

通过 {{site.data.keyword.Bluemix_notm}} Local，可在公司防火墙后和数据中心内托管 {{site.data.keyword.Bluemix_notm}}。因此，某些方面的安全性将由您来负责。下图详细描述了哪些安全机制是客户拥有的，哪些是由 IBM 管理和维护的。

![Bluemix Local 平台安全概况](images/security_local_platform.svg) {: #localplatformsecurity}

图 2. {{site.data.keyword.Bluemix_notm}} Local 平台安全概况

IBM 通过中继（{{site.data.keyword.Bluemix_notm}} Local 随附的一种交付功能）对您数据中心内的 {{site.data.keyword.Bluemix_notm}} Local 进行安装、远程监视和管理。中继通过特定于每个 {{site.data.keyword.Bluemix_notm}} Local 实例的证书进行安全连接。有关 {{site.data.keyword.Bluemix_notm}} Local 和中继的更多信息，请参阅 [Bluemix Local](/docs/local/index.html)。

### 功能性安全

{{site.data.keyword.Bluemix_notm}} 提供了各种功能性安全功能，包括用户认证、访问授权、审计关键操作以及数据保护。

<dl>
<dt>认证</dt>
<dd>应用程序开发者使用 IBM Web 身份向 {{site.data.keyword.Bluemix_notm}} 进行认证。对于 {{site.data.keyword.Bluemix_notm}} Dedicated 和 Local，缺省情况下支持通过 LDAP 进行认证。根据请求，对于 {{site.data.keyword.Bluemix_notm}}，可以改为设置通过 IBM Web 身份进行认证。
</dd>

<dt>授权</dt>
<dd>{{site.data.keyword.Bluemix_notm}} 使用 Cloud Foundry 机制来确保每个应用程序开发者都只有权访问自己创建的应用程序和服务实例。对 {{site.data.keyword.Bluemix_notm}} 服务的授权基于 OAuth。对所有 {{site.data.keyword.Bluemix_notm}} 平台内部端点的访问对于外部用户是受限的。</dd>

<dt>审计</dt>
<dd>对应用程序开发者的所有成功和不成功认证尝试，都会创建审计日志。对运行 {{site.data.keyword.Bluemix_notm}} 应用程序的容器进行托管的 Linux 系统的特权访问，也会创建审计日志。</dd>

<dt>数据保护</dt>
<dd> 所有 {{site.data.keyword.Bluemix_notm}} 流量均通过 IBM WebSphere® DataPower® SOA Appliances 传输，该产品提供逆向代理、SSL 终止和负载均衡功能。下面是允许使用的 HTTP 方法：
<ul>
<li>DELETE</li>
<li>GET</li>
<li>HEAD</li>
<li>OPTIONS</li>
<li>POST</li>
<li>PUT</li>
<li>TRACE</li>
</ul>
HTTP 不活动超时为 2 分钟。</dd>
<dd>以下头由 DataPower 来填充：<dl>
<dt>$wsis</dt>
<dd>如果客户端连接为安全连接 (HTTPS)，将设置为 true；否则设置为 false。</dd>
<dt>$wssc</dt>
<dd>设置为以下某个客户机连接方案：https、http、ws 或 wss。</dd>
<dt>$wssn</dt>
<dd>设置为客户机所发送的主机名。</dd>
<dt>$wssp</dt>
<dd>设置为客户机连接到的服务器端口。</dd>
<dt>x-client-ip</dt>
<dd>设置为客户机 IP 地址。</dd>
<dt>x-forwarded-proto</dt>
<dd>设置为以下某个客户机连接方案：https、http、ws 或 wss。</dd>
</dl>
</dd>

<dt>安全开发实践</dt>
<dd> 对于 {{site.data.keyword.Bluemix_notm}} Public 和 Dedicated，将通过使用 IBM Security AppScan® Dynamic Analyzer，对各种 {{site.data.keyword.Bluemix_notm}} 组件定期执行安全漏洞扫描。执行威胁建模和渗透测试来检测和解决所有类型 {{site.data.keyword.Bluemix_notm}} 部署的任何潜在漏洞。此外，应用程序开发者还可以使用 AppScan Dynamic Analyzer 服务来保护自己在 {{site.data.keyword.Bluemix_notm}} 上部署的 Web 应用程序。</dd>
</dl>

### 基础架构安全

{{site.data.keyword.Bluemix_notm}} 基于 Cloud Foundry 构建，可为应用程序的运行提供稳健的基础。在该体系结构内，提供了多个组件用于安全保护和隔离。此外，还实施了变更管理以及备份和恢复过程来确保完整性和可用性。

<dl>
<dt>环境隔离</dt>
<dd> 对于 {{site.data.keyword.Bluemix_notm}} Public，开发环境和生产环境彼此隔离，可提高应用程序稳定性和安全。</dd>

<dt>防火墙</dt>
<dd> 防火墙已落实到位，可限制对 {{site.data.keyword.Bluemix_notm}} 网络的访问。对于 {{site.data.keyword.Bluemix_notm}} Local，公司防火墙会将您的 {{site.data.keyword.Bluemix_notm}} 实例与网络中的其余部分隔离开。</dd>

<dt>入侵防御</dt>
<dd>{{site.data.keyword.Bluemix_notm}} Public 和 Dedicated 支持通过入侵防御来发现威胁，以便解决这些威胁。入侵防御策略在防火墙上已启用。</dd>

<dt>安全应用程序容器管理</dt>
<dd>{{site.data.keyword.Bluemix_notm}} 应用程序彼此是隔开的，每个应用程序都在其自己的容器中运行，而每个容器都具有特定的处理器、内存和磁盘资源限制。</dd>

<dt>加强操作系统安全</dt>
<dd>IBM 管理员使用多种工具（例如 IBM Endpoint Manager）定期加强网络和操作系统安全。</dd>
</dl>

### 操作安全

{{site.data.keyword.Bluemix_notm}} 通过以下控件提供稳健的操作安全环境。

<dl>
<dt>漏洞扫描</dt>
<dd>{{site.data.keyword.Bluemix_notm}} 使用 Tenable Network Security 漏洞扫描工具 Nessus 来检测网络和主机配置中的任何问题，以便解决这些问题。</dd>

<dt>自动修订管理</dt>
<dd>{{site.data.keyword.Bluemix_notm}} 管理员会确保以适当的频率应用操作系统的修订。自动修订通过 IBM Endpoint Manager 启用。</dd>

<dt>审计日志整合和分析</dt>
<dd>{{site.data.keyword.Bluemix_notm}} 使用 IBM Security QRadar® 工具来整合 Linux 日志，从而监视对 Linux 系统的特权访问。{{site.data.keyword.Bluemix_notm}} 还使用 IBM QRadar 安全信息和事件管理 (SIEM) 来监视应用程序开发者的成功和不成功登录尝试。</dd>

<dt>用户访问管理</dt>
<dd>在 {{site.data.keyword.Bluemix_notm}} 中，按照职责分离准则来为用户分配精细的访问特权，并根据最低特权原则，确保用户只拥有执行其作业所需的访问权。在 {{site.data.keyword.Bluemix_notm}} Dedicated 和 Local 环境中，指派的管理员可以使用管理控制台来管理 {{site.data.keyword.Bluemix_notm}} 用户在其组织中的角色和许可权。有关详细信息，请参阅[管理 {{site.data.keyword.Bluemix_notm}}](/docs/admin/adminpublic.html#mng)。
</dd>
</dl>

### 物理安全

{{site.data.keyword.Bluemix_notm}} Public 和 Dedicated 依赖 {{site.data.keyword.BluSoftlayer}} 的网中网拓扑来确保物理网络安全。此网中网体系结构可确保只有经过授权的人员才能对系统进行完全访问。对于 {{site.data.keyword.Bluemix_notm}} Local，您拥有本地实例的物理安全。您的数据中心位于公司防火墙后，受到防火墙的保护。

在 {{site.data.keyword.BluSoftlayer}} 网中网内，公用网络层会处理访问受托管 Web 站点或联机资源的公共流量。专用网络层允许通过不同的独立第三方运营商经由 SSL、PPTP 或 IPSec VPN 网关进行真正的带外管理。数据中心到数据中心网络层在位于不同 {{site.data.keyword.BluSoftlayer}} 设施中的服务器之间提供免费、安全的连接。

每个 {{site.data.keyword.BluSoftlayer}} 数据中心都通过符合 SSAE 16 和业界公认要求的控件进行全面保护，无一例外。

## 数据安全
{: #data-security}

使用 {{site.data.keyword.Bluemix_notm}} 时，需要您与 {{site.data.keyword.Bluemix_notm}} 共同努力来保护数据，以防止未经授权的访问。

与运行中应用程序关联的数据的状态有以下三种：传输中的数据、静态数据和使用中的数据。

<dl>
<dt>传输中的数据</dt>
<dd>正在网络上的节点之间传输的数据。</dd>

<dt>静态数据</dt>
<dd>存储的数据。</dd>

<dt>使用中的数据</dt>
<dd>当前未存储但在某个端点上正在使用的数据。</dd>
</dl>

在规划数据安全时，每种类型的数据都需要考虑到。

{{site.data.keyword.Bluemix_notm}} 平台使用 SSL 来确保最终用户能够以安全方式访问应用程序，从而确保传输中的数据能够经由网络安全地到达位于 {{site.data.keyword.Bluemix_notm}} 内部网络边界上的 IBM DataPower Gateway。IBM DataPower Gateway 起到逆向代理的作用，可提供 SSL 终止功能。从那里到应用程序，IPSEC 用于在数据从 IBM DataPower Gateway 传输到应用程序时保护数据的安全。

对于使用中的数据和静态数据，其安全由您负责，因为应用程序由您开发。您可以利用 {{site.data.keyword.Bluemix_notm}}“目录”中提供的几个数据相关服务来帮助您解决这些问题。

## {{site.data.keyword.Bluemix_notm}} 应用程序安全
{: #application-security}

作为应用程序开发者，您必须为 {{site.data.keyword.Bluemix_notm}} 上运行的应用程序启用安全配置，包括应用程序数据保护。

可以使用多个 {{site.data.keyword.Bluemix_notm}} 服务提供的安全功能来保护应用程序。IBM 提供的所有 {{site.data.keyword.Bluemix_notm}} 服务均遵循 IBM 安全工程开发实践。

**注：**此处描述的一些服务可能不适用于 {{site.data.keyword.Bluemix_notm}} Dedicated 或 Local 实例。

### SSO 服务

IBM Single Sign On for {{site.data.keyword.Bluemix_notm}} 是一种基于策略的认证服务，用于为 Node.js 或 Liberty for Java™ 应用程序提供易于嵌入的单点登录功能。为了使应用程序开发者能够将单点登录功能嵌入到应用程序中，管理员会创建服务实例并添加身份源。

Single Sign On 服务支持多个存储用户凭证的身份源：

<dl>
<dt>SAML Enterprise</dt>
<dd>通过交换 SAML 令牌完成认证的用户注册表。</dd>

<dt>Cloud Directory</dt>
<dd>在 IBM Cloud 中托管的用户注册表。</dd>

<dt>社交身份源</dt>
<dd> 由 Google、Facebook 和 LinkedIn 维护的用户注册表。</dd>
</dl>

有关更多信息，请参阅 [Single Sign On 入门](/docs/services/SingleSignOn/index.html)。

### Application Security on Cloud

此服务提供对移动和 Web 应用程序的安全性分析，并允许您扫描源代码来查找安全漏洞。有关更多信息，请参阅 [Application Security on Cloud 入门](/docs/services/ApplicationSecurityonCloud/index.html)。

### 用于应用程序安全测试的 IBM UrbanCode 插件

通过 IBM Application Security Testing for {{site.data.keyword.Bluemix_notm}} 插件，可以对在 {{site.data.keyword.Bluemix_notm}} 上托管的 Web 或 Android 应用程序运行安全扫描。此插件由 IBM UrbanCode™ Deploy Community 开发并提供支持。

有关更多信息，请转至 [IBM Application Security Testing for Bluemix ![外部链接图标](../icons/launch-glyph.svg "外部链接图标")](https://developer.ibm.com/urbancode/plugindoc/ibmucd/ibm-application-security-testing-bluemix/1-0/){: new_window}。

### dashDB

dashDB 服务使用嵌入的 LDAP 服务器进行用户认证。应用程序和数据库之间的连接由 SSL 证书保护。此服务使用 DB2® 本机加密功能，以自动加密已部署的数据库和数据库备份。主密钥轮替每 90 天自动执行一次。

有关更多信息，请参阅 [dashDB 入门](/docs/services/dashDB/index.html)。

### Secure Gateway

通过 Secure Gateway 服务，可以将 {{site.data.keyword.Bluemix_notm}} 应用程序安全地连接到内部部署或云中的远程位置。该服务可提供安全连接，并在您的 {{site.data.keyword.Bluemix_notm}} 组织与要连接到的远程位置之间建立隧道。可以使用 {{site.data.keyword.Bluemix_notm}} 用户界面或 API 软件包来配置和创建安全网关。

有关更多信息，请参阅 [Secure Gateway 入门](/docs/services/SecureGateway/secure_gateway.html)。

### 安全信息和事件管理

您可以使用安全信息和事件管理 (SIEM) 工具来分析应用程序日志中的安全警报。其中一个此类工具是 IBM Security QRadar&reg; SIEM，该工具在云环境中提供安全智能。有关信息，请参阅 [IBM QRadar Security Intelligence Platform ![外部链接图标](../icons/launch-glyph.svg "外部链接图标")](http://www-01.ibm.com/support/knowledgecenter/SS42VS/welcome?lang=en){: new_window}。

