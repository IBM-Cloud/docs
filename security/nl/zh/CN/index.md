---

 

copyright:

  years: 2014, 2017
  
lastupdated: "2017-01-11"

 

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}

# {{site.data.keyword.Bluemix_notm}} 安全
{: #security}

{{site.data.keyword.Bluemix}} 平台是使用安全工程实践进行设计的，通过不同的层对整个网络和基础架构中的安全进行控制。{{site.data.keyword.Bluemix_notm}} 提供了一组安全服务，应用程序开发者可以使用这些服务来保护自己的移动和 Web 应用程序。这些优势组合在一起，使 {{site.data.keyword.Bluemix_notm}} 平台成为安全应用程序开发的不二选择。
{:shortdesc}

{{site.data.keyword.Bluemix_notm}} 遵循由 IBM 中的最佳做法驱动的系统、网络和安全工程方面的安全策略，从而确保安全就绪性。这些策略包括源代码扫描、动态扫描、威胁建模和渗透测试等做法。{{site.data.keyword.Bluemix_notm}} 遵循 IBM 产品安全事件响应小组 (PSIRT) 的安全事件管理流程。有关详细信息，请参阅 [IBM Security Vulnerability Management (PSIRT) ![外部链接图标](../icons/launch-glyph.svg)](http://www-03.ibm.com/security/secure-engineering/process.html){: new_window} 站点。

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

![Bluemix Local 平台安全概况](images/security_local_platform.svg)

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

通过 IBM Application Security Testing for {{site.data.keyword.Bluemix_notm}} 插件，可以对在 {{site.data.keyword.Bluemix_notm}} 上托管的 Web 或 Android 应用程序运行安全扫描。此插件由 IBM UrbanCode™ Deploy Community 在 IBM Bluemix DevOps Services 平台上开发并提供支持。

有关更多信息，请转至 [IBM Application Security Testing for Bluemix ![外部链接图标](../icons/launch-glyph.svg)](https://developer.ibm.com/urbancode/plugindoc/ibmucd/ibm-application-security-testing-bluemix/1-0/){: new_window}。

### dashDB

dashDB 服务使用嵌入的 LDAP 服务器进行用户认证。应用程序和数据库之间的连接由 SSL 证书保护。此服务使用 DB2® 本机加密功能，以自动加密已部署的数据库和数据库备份。主密钥轮替每 90 天自动执行一次。

有关更多信息，请参阅 [dashDB 入门](/docs/services/dashDB/index.html)。

### Secure Gateway

通过 Secure Gateway 服务，可以将 {{site.data.keyword.Bluemix_notm}} 应用程序安全地连接到内部部署或云中的远程位置。该服务可提供安全连接，并在您的 {{site.data.keyword.Bluemix_notm}} 组织与要连接到的远程位置之间建立隧道。可以使用 {{site.data.keyword.Bluemix_notm}} 用户界面或 API 软件包来配置和创建安全网关。

有关更多信息，请参阅 [Secure Gateway 入门](/docs/services/SecureGateway/secure_gateway.html)。

### 安全信息和事件管理

您可以使用安全信息和事件管理 (SIEM) 工具来分析应用程序日志中的安全警报。其中一个此类工具是 IBM Security QRadar&reg; SIEM，该工具在云环境中提供安全智能。有关信息，请参阅 [IBM QRadar Security Intelligence Platform ![外部链接图标](../icons/launch-glyph.svg)](http://www-01.ibm.com/support/knowledgecenter/SS42VS/welcome?lang=en){: new_window}。

## {{site.data.keyword.Bluemix_notm}} 安全部署
{: #security-deployment}

{{site.data.keyword.Bluemix_notm}} 安全部署体系结构包含适用于应用程序用户和开发者的不同信息流，可确保访问安全。

![Bluemix 安全部署体系结构](images/sec_deployment.svg)

图 3. Bluemix 安全部署体系结构

对于 {{site.data.keyword.Bluemix_notm}} *应用程序用户*，**应用程序用户流**如下所示：
 1. 经过具有适当入侵防御功能和网络安全的防火墙。
 2. 经过具有逆向代理和 SSL 终止代理功能的 IBM DataPower Gateway。
 3. 经过网络路由器。
 4. 到达 Droplet Execution Agent (DEA) 中的应用程序运行时。

{{site.data.keyword.Bluemix_notm}} *开发者*遵循两个主要流：一个用于登录，一个用于开发和部署。
 * **开发者登录流**包含以下内容：
    * 对于要登录到 {{site.data.keyword.Bluemix_notm}} Public 的开发者，信息流如下所示：
      1. 经过 IBM Single Sign On 服务。
      2. 经过 IBM Web 身份。
    * 对于要登录到 {{site.data.keyword.Bluemix_notm}} Dedicated 或 Local 的开发者，信息流将经过企业 LDAP。
 * **开发和部署流**如下所示：
    1. 经过具有适当入侵防御功能和网络安全的防火墙。这仅适用于 {{site.data.keyword.Bluemix_notm}} Dedicated。
    2. 经过具有逆向代理和 SSL 终止代理功能的 IBM DataPower Gateway。
    3. 经过网络路由器。
    4. 经过授权（通过使用 Cloud Foundry 云控制器），以确保仅访问开发者创建的应用程序和服务实例。

对于 {{site.data.keyword.Bluemix_notm}} Dedicated 和 {{site.data.keyword.Bluemix_notm}} Local *管理员*，**管理员流**如下所示：
 1. 经过具有适当入侵防御功能和网络安全的防火墙。
 2. 经过具有逆向代理和 SSL 终止代理功能的 IBM DataPower Gateway。
 3. 经过网络路由器。
 4. 在 {{site.data.keyword.Bluemix_notm}} 用户界面中访问“管理”页面。

除了这些方法中描述的用户，经过授权的 IBM 安全操作团队还会执行各种操作安全任务，例如：
 * 漏洞扫描。对于 {{site.data.keyword.Bluemix_notm}} Local，您拥有防火墙内的物理安全和任何扫描。
 * 用户访问管理。
 * 通过使用 IBM Endpoint Manager 定期应用修订，加强操作系统安全。
 * 通过入侵防御来管理风险。
 * 使用 QRadar 监视安全。
 * 在“管理”页面上提供有安全报告。

## 安全合规性
{: #compliance}

{{site.data.keyword.Bluemix}} 提供了一个您可以信任的安全云平台。{{site.data.keyword.Bluemix_notm}} 合规性是通过基于业界最佳安全标准（包括 ISO 27001 和 ISO 27002）构建的平台和服务来实现的。
{:shortdesc}

![欧盟数据保护示范条款](images/icon_eumc.png) **欧盟 (EU) 示范条款**是一种协议，用于保护从欧盟 (EU) 或欧洲经济区 (EEA) 传输到第三方国家或地区的个人数据。“欧盟 (EU) 示范条款”是由位于 EU 或 EEA 的客户（数据导出方）与位于第三方国家或地区的 IBM 数据处理方（数据导入方）之间签订的。[IBM SaaS 欧盟 (EU) 示范条款 ![外部链接图标](../icons/launch-glyph.svg)](http://www-01.ibm.com/common/ssi/cgi-bin/ssialias?subtype=ST&infotype=SA&htmlfid=KUJ12408USEN&attachment=KUJ12408USEN.PDF){: new_window} 包含数据导出方和数据导入方的权利和责任，以及数据主体的权利。“IBM SaaS 欧盟示范条款”可确保个人数据在第三方国家或地区处理时仍能受到像在 EU 或 EEA 中一样的保护。

对于要将源自欧洲经济区 (EEA) 的数据传输到 EEA 以外的国家或地区的客户，{{site.data.keyword.Bluemix}} 提供了“欧盟示范条例”，其形式得到了欧盟委员会和欧盟数据保护监管机构的批准。“欧盟示范条例”向欧盟客户保证，{{site.data.keyword.Bluemix_notm}} 在全球所有位置均支持必要的数据隐私保护。

![金融行业信息系统](images/FISC.gif) 对于日本的银行和相关金融机构，计算机系统必须具有适当的安全程序，这些程序应基于金融行业信息系统中心 (FISC) 安全准则。FISC 安全准则由日本金融厅 (FSA)、日本央行 (BOJ) 和 FISC 贯彻实施。
 

![ISO 27001/2](images/icon_iso27k1.png) {{site.data.keyword.Bluemix_notm}} 已通过**国际标准化组织 (ISO) 27001 和 27002 标准**的认证，这两个标准定义了信息安全管理过程的最佳做法。ISO 27001 是一种被广泛采用的全球安全标准。该标准概述了信息安全管理系统的要求，并提供了系统化方法，基于定期风险评估来管理公司和客户信息。最新标准 ISO/IEC 27001:2013 由**国际标准化组织 (ISO) 和国际电工技术委员会 (IEC)** 联合组建的 ISO/IEC 子委员会于 2013 年 9 月 25 日颁布。ISO 27001 标准根据不同组织的需求规定了应如何建立、实施和记录信息安全管理系统 (ISMS)，以及应如何实施安全性控制。ISO 27002 标准对 ISO 27001 中的每种安全性控制进行了详细的说明。ISO 27000 系列标准中包含了一个确定风险规模和评估资产价值的过程，旨在保护书面、口头和电子信息的机密性、完整性和可用性。

为了通过 ISO 27001:2013 认证，公司必须证明自己具有系统化的持续方法，用于管理会影响公司及客户信息的机密性、完整性和可用性的信息安全风险。此标准着重于测量和评估组织的信息安全管理系统 (ISMS) 的表现情况，并包含与信息安全相关且基于系统需求和其他需求的控制措施。

{{site.data.keyword.Bluemix_notm}} 经第三方安全公司审计，满足 ISO 27001 的所有要求：[Bluemix ISO 27001:2013 Certificate of Registration ![外部链接图标](../icons/launch-glyph.svg)](ftp://public.dhe.ibm.com/cloud/bluemix/compliance/Bluemix_ISO27K1_WWCert_2016.pdf){: new_window}。

![PCI DSS](images/icon_pci.png) **支付卡行业 (PCI) 数据安全标准 (DSS)** 是一种专用于保护信用卡数据的信息安全标准。PCI DSS 适用于支付卡处理中所涉及的所有实体，包括商家、处理机构、发卡人和服务提供者。此外，还适用于存储、处理或传输持卡人数据或敏感认证数据的其他所有实体。

如果您要存储或处理信用卡数据，那么支付卡行业 (PCI) 合规性和网络安全将是您企业关心的主要问题。为了确保有统一标准可供商家使用，支付卡行业安全标准委员会颁布了 PCI 数据安全标准。这些标准整合了用于保护持卡人数据的最佳实践，并且通常需要第三方合格服务评估方 (QSA) 进行验证。IBM 通过独立的 QSA 提供“合规证明”，帮助客户满足其 PCI 合规需求。“合规证明”可与 SOC 2 报告以及 ISO 27001 认证配合使用，以证明基础架构满足 PCI 控制要求。

{{site.data.keyword.Bluemix}} 通过批准的合格安全服务评估方 (QSA) 完成了年度 PCI DSS 评估。根据 PCI DSS V3.1 下的一级服务提供者要求，{{site.data.keyword.Bluemix_notm}} 被评为合规，如 [Bluemix PCI DSS AOC ![外部链接图标](../icons/launch-glyph.svg)](ftp://public.dhe.ibm.com/cloud/bluemix/compliance/IBM_Bluemix_PCI.pdf){: new_window} 中所概述。有关使您的 {{site.data.keyword.Bluemix_notm}} 环境符合 PCI DSS 评估要求的信息和帮助，请联系销售人员：[联系我们 ![外部链接图标](../icons/launch-glyph.svg)](https://console.ng.bluemix.net/?direct=classic/#/contactUs/cloudOEPaneId=contactUs){: new_window}。

![SSAE16 SOC1/2/3](images/icon_aicpa.png) **服务组织控制 (SOC)** 报告定义了如何对服务组织评估与安全性、可用性、处理完整性、机密性和隐私性相关的主要内部控制做法。这些报告是使用美国注册会计师协会 (AICPA) 指南生成的，包含以下各项： 
  * 组织监督
  * 供应商管理程序
  * 内部公司治理和风险管理流程
  * 法规监督
 
{{site.data.keyword.Bluemix_notm}} 提供 SOC 1、SOC 2 和 SOC 3 报告。有关其他信息，请联系 [{{site.data.keyword.Bluemix_notm}} 销售 ![外部链接图标](../icons/launch-glyph.svg)](mailto:bmxcert1@us.ibm.com){:new_window} 团队。 


![HIPAA](images/icon_hipaa.png) 美国国会在 1996 年颁布的《健康保险可移植性和责任法案》(HIPAA) 旨在保障员工在失业后仍能享受健康保险。HIPAA 由美国民权办公室以及卫生和公众服务部负责监管和实施。HIPAA 除了包含 1996 年法案中的规定外，还包含 2009 年颁布的《医疗信息技术促进经济和临床健康法案》(HITECH) 中的隐私要求。{{site.data.keyword.Bluemix_notm}} 符合 HIPAA 有关数据中心或服务提供者方面的所有要求。

有关使您的 Bluemix 环境达到 HIPAA 合规性、通过 HIPAA 合规性认证以及保持 HIPAA 合规性的更多信息或帮助，请联系 {{site.data.keyword.Bluemix_notm}} [销售 ![外部链接图标](../icons/launch-glyph.svg)](mailto:cloudplatform_compliance@us.ibm.com){:new_window}团队。


![ISO 27017](images/icon_ISO27017.png) ISO/IEC 27017:2015 针对适用于供应和使用云服务的信息安全控制措施提供了准则。此外，它还针对云服务提供商和云服务客户提供了实施指南。ISO 27017 针对 ISO/IEC 27002 中规定的相关控制措施提供了实施指南，同时还提供了专门与云服务相关的更多控制措施与指南。

{{site.data.keyword.Bluemix_notm}} 符合 ISO 27017:2015 的要求，这证明了 IBM 已落实了一套由特定于云的控制措施组成的成熟系统。此外，还表明了 IBM 致力于成为美国国内及全球 IaaS 领域的佼佼者。


![ISO 27018](images/icon_ISO27018.png) ISO 27018:2014 制定了人们普遍认可的控制目标、控制措施和准则，以实施各项措施来保护个人可标识信息 (PII)。这些措施符合 ISO 29100 中有关公共云计算环境的隐私原则。

特别是，ISO 27018:2014 规定了基于 ISO 27002 的准则。这些准则考虑了 PII 保护法规需求，这些需求可能适用于公共云服务提供商的信息安全风险环境背景。


![云安全联盟 - STAR Registrant](images/icon_CSA.png) 云安全联盟是一家非盈利性组织，使命是大力推广在云计算中提供安全保证的最佳实践。云安全联盟在贯彻其使命时使用的其中一个机制是安全、信任与保证注册项目 (STAR)。STAR 是可公共访问的免费注册项目，用于记录各种云计算产品提供的安全控制措施。


![CJIS 标准](images/icon_CJIS.png) 刑事司法信息系统部 (CJIS) 是美国联邦调查局司法部下属的一个部门。CJIS 部制定并颁布了安全政策 (CJISD-ITS-DOC-08140-5.4)。此安全政策包含最低信息安全需求、准则和协议，反映了执法部门和刑事司法机构保护刑事司法信息 (CJI) 的来源、传输、存储和生成的意愿。



### 平台和服务合规性
下表显示了 {{site.data.keyword.Bluemix_notm}} 中符合每种标准的服务。

|{{site.data.keyword.Bluemix_notm}} 组件		|FISC		|ISO 27001	|PCI |SOC 2 第 1 类		|
|:----------------------|:---------:|:---------:|:---------:|:---------:|
|{{site.data.keyword.Bluemix_notm}} 平台		|是			|是	|是	|是	|
|{{site.data.keyword.APIM}}			|是	|是 |是	|			|
|{{site.data.keyword.autoscaling}}			|是	|是 |是	|			|
|{{site.data.keyword.bigicloudst}}			|是 |是 |	|是 |
|{{site.data.keyword.cloudant}}				|是 |是 |	|是	|
|{{site.data.keyword.dashdbshort}}			|是	|是	|	|是	|
|{{site.data.keyword.datacshort}}			|是	|是	|是	|			|
|{{site.data.keyword.jazzhub_short}}					|是	|是	|	|			|
|{{site.data.keyword.containerlong}}			|是		|是	|	|			|
|{{site.data.keyword.mql}}				|是	|是	|是	|	 		|
|{{site.data.keyword.SecureGateway}}			|是	|是 |	|	 		|
|{{site.data.keyword.sescashort}}     |是 |是 |是	|  |
{: caption="表 1. 平台和服务合规性" caption-side="top"}

# 相关链接
{: #rellinks}

## 相关链接
{: #general}

* [IBM SaaS 安全性 ![外部链接图标](../icons/launch-glyph.svg)](http://www.ibm.com/cloud-computing/built-on-cloud/saas-security){: new_window}
* [Single Sign On 入门](/docs/services/SingleSignOn/index.html)
