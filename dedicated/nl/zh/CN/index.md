---



copyright:

  years: 2015, 2017

lastupdated: "2017-05-03"

---

{:shortdesc: .shortdesc}

# {{site.data.keyword.Bluemix_dedicated_notm}}
{: #dedicated}


{{site.data.keyword.Bluemix}} 是一种基于云的开放标准平台，用于构建、运行和管理应用程序。通过 {{site.data.keyword.Bluemix_dedicated_notm}}，您可以在您自己的专用 SoftLayer 环境中享受到 {{site.data.keyword.Bluemix_notm}} 为您提供的强大功能和简便性。该环境是以安全方式连接到 {{site.data.keyword.Bluemix_notm}} Public 环境和您自己的网络。
{:shortdesc}

无需额外付费，{{site.data.keyword.Bluemix_notm}} 的所有专用部署中都包含以下亮点和功能：VPN、专用虚拟局域网 (VLAN)、防火墙、与 LDAP 的连接、利用现有内部部署数据库和应用程序的能力、全天候现场安全防护、专用硬件以及标准支持。

缺省情况下，只能通过公司网络访问您的私有 {{site.data.keyword.Bluemix_notm}} 实例。例如，如果需要可直接从因特网、移动设备或专用数据库访问 {{site.data.keyword.Bluemix_notm}} 环境，那么需要额外的网络安全组件，这需要额外付费。

{{site.data.keyword.Bluemix_dedicated_notm}} 随附所有包含的 {{site.data.keyword.Bluemix_notm}} 运行时和 64 GB 计算资源内存。

此外，还有一组服务和组件包含在内或可选择购买。请查看下表以了解哪些服务和组件已包含在内，哪些服务和组件可选择购买。

| **类型**        | **名称**            | **描述** |
|-----------------|-------------------|-------------------|
|已包含 | [{{site.data.keyword.Bluemix_notm}} 运行时](/docs/cfapps/runtimes.html) | 使用运行时可快速启动并运行应用程序，无需设置和管理计算机与操作系统。所有 {{site.data.keyword.Bluemix_notm}} 运行时都可供您在 {{site.data.keyword.Bluemix_dedicated_notm}} 实例中使用。|
| 已包含 | [{{site.data.keyword.autoscaling}}](/docs/services/Auto-Scaling/index.html) | 根据策略，动态增大或减小应用程序的计算容量。通过此服务，您在 {{site.data.keyword.Bluemix_dedicated_notm}} 环境中的使用不受限制。注：自动扩展目前只适用于 Cloud Foundry 运行时 |
|可选 | [{{site.data.keyword.apiconnect_short}}](/docs/services/apiconnect/index.html) | {{site.data.keyword.apiconnect_long}} 将 {{site.data.keyword.APIM}} 和 IBM StrongLoop 集成到单个产品中，以提供一个综合解决方案来创建、运行、管理和强制执行 API 与微服务。 |
|可选 | [{{site.data.keyword.rules_short}}](/docs/services/rules/rules.html) | {{site.data.keyword.rules_short}} 提供了一个综合环境来自动化和执行频繁发生且可重复的基于规则的业务决策。此外，它通过降低对 IT 技能的需求，支持业务用户或开发者以更低的成本快速对决策建模并进行测试。 |
|可选 | [{{site.data.keyword.cloudant}}](/docs/services/Cloudant/index.html#Cloudant) | {{site.data.keyword.cloudant}} 提供了对始终启用的完全受管 NoSQL JSON 数据层的访问。此服务兼容 CouchDB，并且可通过易用的 HTTP 接口供移动和 Web 应用程序模型访问。 |
|可选 | [{{site.data.keyword.containershort}}](/docs/containers/container_index.html) | 在 {{site.data.keyword.Bluemix_dedicated_notm}} 上运行 Docker 容器。容器是包含应用程序运行所需的所有元素的虚拟软件对象。容器不仅具有资源隔离和分配的好处，而且还比虚拟机器（举例来说）的可移植性更好，且更有效率。有关硬件需求的信息，请参阅 [{{site.data.keyword.Bluemix_dedicated_notm}} 和 Bluemix Local 中的 IBM {{site.data.keyword.containershort}}](/docs/containers/container_ov.html#container_dl)。|
| 可选 | [{{site.data.keyword.contdelivery_short}}](/docs/services/ContinuousDelivery/index.html) | 使用 {{site.data.keyword.contdelivery_short}} Dedicated 可自动执行构建、单元测试、部署等操作。通过丰富的基于 Web 的 IDE 来编辑和推送代码。创建工具链以便进行支持开发、部署和操作任务的工具集成。 |
| 可选 | [{{site.data.keyword.dashdbshort}}](/docs/services/dashDB/dashDB.html) | IBM {{site.data.keyword.dashdbshort}} for Analytics 是完全管理的 SQL 云数据库服务，针对数据仓库和分析工作负载而进行了优化。IBM {{site.data.keyword.dashdbshort}} for Transactions 是完全管理的 SQL 云数据库服务，针对一般目的、Web 应用程序和事务工作负载而进行了优化。 |
| 可选 | [{{site.data.keyword.datacshort}}](/docs/services/DataCache/index.html#data_cache) | 此服务提供内存中数据网格，支持应用程序使用分布式高速缓存方案。包含 50 GB 内存中高速缓存。 |
| 可选 | [Dedicated GitHub Enterprise](/docs/services/ghededicated/index.html) | {{site.data.keyword.ghe_long}} 是 IBM Cloud 托管且完全管理的 GitHub 版本，提供了开发者喜爱的社交功能。此服务目前只可用于 {{site.data.keyword.Bluemix_dedicated_notm}} 环境。 |
| 可选 (Beta) | [日志记录](/docs/monitoringandlogging/cfapps_ml_logs_dedicated_ov.html#container_ml_logs_dedicated_ov) | 为 {{site.data.keyword.Bluemix_notm}} 用户界面中的 Cloud Foundry 应用程序和 Kibana 中的可搜索日志和仪表板提供日志。 |
| 可选 | [{{site.data.keyword.messagehub}}](/docs/services/MessageHub/index.html#messagehub) | {{site.data.keyword.messagehub}} 是一种可扩展的分布式消息传递总线，吞吐量高，可将内部部署和外部部署技术融合在一起。{{site.data.keyword.messagehub}} 基于 Apache Kafka，这是一种高速、耐用的可扩展实时消息传递引擎。 |
|可选 | [{{site.data.keyword.mobilepush}}](/docs/services/mobilepush/index.html) | {{site.data.keyword.mobilepush}} 是可用于向 iOS 和 Android 设备发送通知的服务。通知可以针对所有应用程序用户发送，也可以针对一组使用标记的特定用户和设备发送。您可以管理设备、标记和预订。还可以使用 SDK（软件开发包）和具象状态传输 (REST) 应用程序编程接口 (API) 来进一步开发您的客户机应用程序。|
|可选 | [{{site.data.keyword.SecureGateway}}](/docs/services/SecureGateway/secure_gateway.html) | {{site.data.keyword.SecureGateway}} 服务使您能够以安全方式将 {{site.data.keyword.Bluemix_notm}} 应用程序连接到内部部署或云中的远程位置。  |
|可选 | [{{site.data.keyword.sescashort}}](/docs/services/SessionCache/index.html#session_cache) | 为了提高冗余度，{{site.data.keyword.sescashort}} 提供了高速缓存中存储的会话的副本。因此，万一发生掉线或中断，客户机应用程序能够继续访问高速缓存中的会话。此服务支持 Web 和移动应用程序的会话高速缓存场景。 |
| 可选 | [{{site.data.keyword.iot_short}}](/docs/services/IoT/index.html) | 此服务允许应用程序与连接的设备、传感器和网关进行通信，以及使用这些设备、传感器和网关收集的数据。基本产品允许在专用环境中运行 {{site.data.keyword.iot_short}} 的专用版本，容量为 100,000 个并行连接设备或应用程序，数据交换量为 1.6 TB。 |
| 可选 | [{{site.data.keyword.appserver_short}}](/docs/services/ApplicationServeronCloud/index.html) | IBM {{site.data.keyword.appserver_short}} for IBM {{site.data.keyword.Bluemix_notm}} 是有助于在 {{site.data.keyword.Bluemix_notm}} 上托管的云环境中预配置的 {{site.data.keyword.appserver_short}} Liberty、Traditional Network Deployment 或 Traditional WebSphere Java EE 实例上执行快速设置的服务。 |
{: caption="表 1. 专用服务" caption-side="top"}
{: #table01}



有一些可选组件可供您购买，用于扩展资源和服务的容量。可以通过联系销售团队来购买其中任何组件；请转至[联系我们](https://console.ng.bluemix.net/?direct=classic/#/contactUs/cloudOEPaneId=contactUs)，以获取有关联系销售代表的信息。要增加服务的套餐，可以从目录的服务磁贴中选择套餐。

| **名称**            | **描述** |
|-------------------|-------------------|
|Dedicated {{site.data.keyword.apiconnect_short}} Professional 500 万次 API 调用 | 此环境允许在专用环境中运行 {{site.data.keyword.apiconnect_short}} 的专用版本，容量为每月针对部门 API 项目进行 500 万次 API 调用。 |
|Dedicated {{site.data.keyword.apiconnect_short}} Professional 增加 10 万次 API 调用 | {{site.data.keyword.apiconnect_short}} Professional 环境的扩展，用于每月提供额外 10 万次 API 调用容量。 |
|Dedicated {{site.data.keyword.apiconnect_short}} Enterprise 2500 万次 API 调用 | 此环境允许在专用环境中运行 {{site.data.keyword.apiconnect_short}} 的专用版本，容量为每月针对企业级 API 项目进行 2500 万次 API 调用。 |
|Dedicated {{site.data.keyword.apiconnect_short}} Enterprise 增加 10 万次 API 调用 | {{site.data.keyword.apiconnect_short}} Enterprise 环境的扩展，用于每月提供额外 10 万次 API 调用容量。 |
|IBM {{site.data.keyword.Bluemix_dedicated_notm}} {{site.data.keyword.rules_short}} 100 万个规则决策 | 规则决策是从规则执行服务器调用规则集的结果。必须获得充分的权利才能涵盖结算周期内执行或处理的规则决策总数（四舍五入到最接近的百万数）。由此云服务度量的规则决策是为了获取决策而对规则执行服务器发出的调用。云服务的专用部署按照相关费用度量值来度量约定的容量。在 {{site.data.keyword.Bluemix_dedicated_notm}} 平台上 {{site.data.keyword.rules_short}} 服务分配的缺省空间为 16 GB，在此空间中最多可以调用 10 个 1 GB 实例来执行授权的规则决策。如果超过该使用量限制，您必须另外购买容量来满足该使用量。 |
|Dedicated {{site.data.keyword.cloudant}} 增加 1.6 TB 容量 | 包含在专用环境中运行 {{site.data.keyword.cloudantfull}} 的专用版本，设计容量为 1.6 TB。  |
|Dedicated {{site.data.keyword.datacshort}} 和 {{site.data.keyword.sescashort}} 增加 50 GB 容量 | 此环境允许部署和运行 {{site.data.keyword.datacshort}} 和 {{site.data.keyword.sescashort}} 实例，最高累计容量为 50 GB。 |
|{{site.data.keyword.contdelivery_short}} Dedicated 实例 | 在专用环境中运行的 {{site.data.keyword.contdelivery_short}} 专用版本。容量由 {{site.data.keyword.contdelivery_short}} Dedicated 授权用户权利确定。 |
|{{site.data.keyword.contdelivery_short}} Dedicated 授权用户 | 授予对指定 {{site.data.keyword.contdelivery_short}} Dedicated 环境的授权用户访问权，并授权使用该环境。必须对属于包含 {{site.data.keyword.contdelivery_short}} 服务实例的 {{site.data.keyword.Bluemix_notm}} 组织的每一位用户都进行授权。 |
|Dedicated {{site.data.keyword.dashdbshort}} Enterprise 64.1 | 专用服务器上每个服务实例一个数据库，RAM 为 64 GB，16 个 vCPU。根据典型压缩率，建议预装入数据最多为 1 TB。  |
|Dedicated {{site.data.keyword.dashdbshort}} Enterprise 256.4 | 专用裸机服务器上每个服务实例一个数据库，RAM 为 256 GB，32 个内核。根据典型压缩率，建议预装入数据最多为 4 TB。 |
|Dedicated {{site.data.keyword.dashdbshort}} Enterprise 256.12  | 专用裸机服务器上每个服务实例一个数据库，RAM 为 256 GB，32 个内核。根据典型压缩率，建议预装入数据最多为 12 TB。这是高密度存储套餐，适用于数据量较高且查询无需以内存中速度运行的环境。 |
|IBM {{site.data.keyword.Bluemix_dedicated_notm}} {{site.data.keyword.dashdbshort}} Enterprise for Transactions 2.8.500 | 此专用实例支持联机事务处理 (OLTP) 工作负载，RAM 为 8 GB，用于数据和日志的空间为 500 GB。 |
|IBM {{site.data.keyword.Bluemix_dedicated_notm}} {{site.data.keyword.dashdbshort}} Enterprise for Transactions 12.128.1400 | 此专用实例支持联机事务处理 (OLTP) 工作负载，RAM 为 128 GB，用于数据和日志的 SSD 存储空间为 1.4 TB。 |
|IBM {{site.data.keyword.Bluemix_dedicated_notm}} {{site.data.keyword.dashdbshort}} Enterprise for Transactions High Availability 2.8.500 | 此专用实例支持联机事务处理 (OLTP) 工作负载，RAM 为 8 GB，用于数据和日志的空间为 500 GB，并包括一台额外的备用服务器以实现高可用性。 |
|IBM {{site.data.keyword.Bluemix_dedicated_notm}} {{site.data.keyword.dashdbshort}} Enterprise for Transactions High Availability 12.128.1400 | 此专用实例支持联机事务处理 (OLTP) 工作负载，RAM 为 128 GB，用于数据和日志的 SSD 存储空间为 1.4 TB，并包括一台额外的备用服务器以实现高可用性。 |
|{{site.data.keyword.Bluemix_dedicated_notm}} 社区服务  | 此环境允许部署和运行社区服务，每个社区服务最多共 50 个实例。  |
|{{site.data.keyword.Bluemix_dedicated_notm}} {{site.data.keyword.cloudant}} 集群实例 | 此可选组件包含您负责为其提供基础架构的 3 节点集群，并且存储和计算能力可以根据您的特定需求来确定。{{site.data.keyword.cloudant}} 提供了对始终启用的完全受管 NoSQL JSON 数据层的访问。此服务兼容 CouchDB，并且可通过易用的 HTTP 接口供移动和 Web 应用程序模型访问。 |
|IBM {{site.data.keyword.Bluemix_dedicated_notm}} {{site.data.keyword.messagehub}} | 该环境提供每个分区高达 10 GB 的发布/预订消息传递，限制为 100 个分区。 |
|IBM Bluemix Dedicated {{site.data.keyword.mobilepushshort}} | 此环境允许部署和执行 {{site.data.keyword.mobilepushshort}} 实例，每秒能接受 300 个请求。 |
|{{site.data.keyword.iot_short}} Dedicated 递增增加 | 此环境允许在专用环境中运行 {{site.data.keyword.iot_short}} 的专用版本，容量为 100,000 个并行连接设备或应用程序，数据交换量为 0.5 TB。 |
|IBM {{site.data.keyword.appserver_short}} for {{site.data.keyword.Bluemix_notm}} - Dedicated Small| 在 {{site.data.keyword.Bluemix_notm}} 上托管的云环境中预配置的 {{site.data.keyword.appserver_short}} Liberty、Traditional Network Deployment 或 Traditional WebSphere Java EE 实例，每月 64 个 vCore、128GB RAM 和 1TB HDD。 |
|IBM {{site.data.keyword.appserver_short}} for {{site.data.keyword.Bluemix_notm}} - Dedicated Medium| 在 {{site.data.keyword.Bluemix_notm}} 上托管的云环境中预配置的 {{site.data.keyword.appserver_short}} Liberty、Traditional Network Deployment 或 Traditional WebSphere Java EE 实例，每月 128 个 vCore、256GB RAM 和 2TB HDD。 |
|IBM {{site.data.keyword.appserver_short}} for {{site.data.keyword.Bluemix_notm}} - Dedicated Large| 在 {{site.data.keyword.Bluemix_notm}} 上托管的云环境中预配置的 {{site.data.keyword.appserver_short}} Liberty、Traditional Network Deployment 或 Traditional WebSphere Java EE 实例，每月 256 个 vCore、512GB RAM 和 4TB HDD。 |
|IBM {{site.data.keyword.appserver_short}} for {{site.data.keyword.Bluemix_notm}} - Dedicated| 在 {{site.data.keyword.Bluemix_notm}} 上托管的云环境中预配置的 {{site.data.keyword.appserver_short}} Liberty、Traditional Network Deployment 或 Traditional WebSphere Java EE 实例，具有 HDD 扩展和每月 1TB HDD。 |
{: caption="表 2. 可购买的可选服务组件" caption-side="top"}
{: #table02}



| **名称**            | **描述** |
|-------------------|-------------------|
|Dedicated Runtimes 增加 16 GB 容量  | 扩展运行时环境，以额外提供 16 GB 运行时容量。 |
|Dedicated Direct Link 1 Gbps 容量 | 此专用网络链路直接连接到相应的现有 {{site.data.keyword.BluSoftlayer}} 网络点，设计数据传输量最高 1 Gbps。 |
|Dedicated Direct Link 10 Gbps 容量 | 此专用网络链路直接连接到相应的现有 {{site.data.keyword.BluSoftlayer}} 网络点，设计数据传输量最高 10 Gbps。 |
|IBM Bluemix Dedicated 硬件防火墙 - 高可用性 | 冗余 1 Gbps 硬件防火墙，配置用于保护专用环境中同一 VLAN 中的单台服务器、多台服务器或所有服务器。 |
{: caption="表 3. 可购买的可选平台附加组件" caption-side="top"}
{: #table03}

**注**：{{site.data.keyword.Bluemix_dedicated_notm}} 组件可能指示特定配置的容量，例如千兆字节或每秒事务数。由于现实中云服务的任何配置的实际容量根据多种因素而变化，因此现实中的实际容量可能大于或小于配置的容量。

### 联合目录
{: #catalogdedicated}

{{site.data.keyword.Bluemix_dedicated_notm}} 包含一个私有目录，用于将公共部署、专用部署和本地部署中已批准的服务集中在一起。您甚至可以通过 {{site.data.keyword.Bluemix_notm}} 目录来发布您自己的服务并管理对这些服务的访问权。您可以选择根据自己的数据隐私和安全标准来确定哪些公共服务满足您的业务需求。

如果您的专用环境有私有的服务实例，那么您将看到目录中的该服务名称带有“专用”标记。与此类似，如果这是定制服务（即您使用的是服务代理程序创建的服务），那么您将看到列出服务名称时有“定制”字样。通过从 {{site.data.keyword.Bluemix_notm}} Public 使用联合，即可使用不带“专用”或“定制”标记列出的其他所有服务。联合服务提供了用于创建混合应用程序的功能，混合应用程序由公共服务和私有服务组成。

|服务	|在美国南部区域中可用	|在欧洲英国区域中可用 |在澳洲悉尼区域中可用|
|:----------|:------------------------------|:------------------|:------------------|
|{{site.data.keyword.alchemyapishort}} 		|是	   	|是  		|是|
|{{site.data.keyword.alertnotificationshort}}	|是		|是		|是	|
|{{site.data.keyword.apiconnect_short}}         |是            |是            |是  |
|{{site.data.keyword.appseccloudshort}}		|是		|是		|是 |
|{{site.data.keyword.apiconnect_short}} 	|是   	 	|是  	 	|是   |
|Automated Accessibility Checker |是       |是    |是   |
|{{site.data.keyword.rules_short}}		|是		|是		|是 |
|{{site.data.keyword.cloudant}}			|是		|是		|是 |
|{{site.data.keyword.iotmapinsights_short}}    |是  |是  |是  |
|{{site.data.keyword.conversationshort}}  |是  |是  |是  |
|{{site.data.keyword.dashdbshort}}		|是		|是		|是 |
|{{site.data.keyword.dataworks_short}}		|是		|是		|否|
|{{site.data.keyword.DB2OnCloud_short}}		|是		|是		|是 |
|Digital Content Checker |是  |是  |是  |
|{{site.data.keyword.documentconversionshort}}	|是		|是		|是|
|{{site.data.keyword.iotdriverinsights_short}}  |是 |是  |是  |
|{{site.data.keyword.geospatialshort_Geospatial}}	|是	|是		|是 |
|{{site.data.keyword.GlobalizationPipeline_short}}	|是		| 是		| 是 |
|{{site.data.keyword.identitymixershort}}		|是		|是		|是|
|{{site.data.keyword.iot4auto_short}} |是   |是  |是  |
|{{site.data.keyword.iotelectronics}}  |是  |是  |否 |
|{{site.data.keyword.iotinsurance_short}} |否   |否   |是  |
|{{site.data.keyword.twittershort}}		|是		|是		|是|
|{{site.data.keyword.languagetranslationshort}}	|是		|是		|是 |
|{{site.data.keyword.languagetranslatorshort}} |是  |是  |是  |
|{{site.data.keyword.dwl_short}}  |是  |是  |否  |
|{{site.data.keyword.eventhubshort}}		|是		|否		|否|
|{{site.data.keyword.messagehub}}		|是		|是		|否|
|{{site.data.keyword.manda}}			|是		|是		|是 |
|{{site.data.keyword.amashort}}			|是		|是		|是 |
|{{site.data.keyword.mqa}}			|是		|是		|是 |
|{{site.data.keyword.mql}}			|否		|否		|是 |
|{{site.data.keyword.nlclassifierlshort}} 	|是 		|是 		|是|
|{{site.data.keyword.personalityinsightsshort}}	|是		|是		|是|
|{{site.data.keyword.pm_short}}			|是		|是		|否 |
|{{site.data.keyword.mobilepush}}		|是		|是		|是 |
|{{site.data.keyword.retrieveandrankshort}}	|是 		|是 		|是|
|{{site.data.keyword.runbook_short}}		|是		|是		|是|
|{{site.data.keyword.SecureGateway}}		|是		|是		|是 |
|{{site.data.keyword.ssofull}}			|是		|否		|否|
|{{site.data.keyword.speechtotextshort}}	|是 		|是	 	|是|
|{{site.data.keyword.streaminganalyticsshort}}	|是		|是		|是 |
|{{site.data.keyword.texttospeechshort}} 	|是 		|是	 	|是|
|{{site.data.keyword.toneanalyzershort}} 	|是 		|是 		|是|
|{{site.data.keyword.tradeoffanalyticsshort}}	|是		|是		|是|
|{{site.data.keyword.visualrecognitionshort}}	|是 		|是	 	|是|
|{{site.data.keyword.iot_short}}		|是		|是		|否|
|{{site.data.keyword.weather_short}}		|是		|是		|是|
|{{site.data.keyword.workloadscheduler}}	|是		|是		|是 |
{: caption="表 4. 按区域为 Bluemix Public 联合提供的服务" caption-side="top"}
{: #table04}

**注**：此表中未包含第三方服务。请检查专用目录以获取第三方服务选项。



## {{site.data.keyword.Bluemix_dedicated_notm}} 体系结构
{: #dedicatedarch}

{{site.data.keyword.Bluemix_dedicated_notm}} 可以在全世界任何一个 [{{site.data.keyword.IBM_notm}} SoftLayer 数据中心 ![外部链接图标](../icons/launch-glyph.svg)](http://www.softlayer.com/data-centers){: new_window} 内进行部署。{{site.data.keyword.IBM_notm}} SoftLayer 提供了能达到最高性能的云基础架构。每个数据中心都采用严格的全天候安全控制。

每个 {{site.data.keyword.Bluemix_dedicated_notm}} 部署都专用于单一企业中专用网络内的 {{site.data.keyword.IBM_notm}} SoftLayer 专用硬件上。{{site.data.keyword.Bluemix_dedicated_notm}} 环境在基础架构、操作和物理安全方面所采用的安全标准与公共 {{site.data.keyword.Bluemix_notm}} 相同。但是，开发者对专用 {{site.data.keyword.Bluemix_notm}} 的访问由 LDAP 策略进行控制，这些策略可以由 {{site.data.keyword.Bluemix_notm}} 团队在设置您的环境时进行配置。在该专用环境中，您可以管理用户角色和许可权。有关详细信息，请参阅[管理用户和许可权](/docs/admin/index.html#oc_useradmin)。下图描述缺省 {{site.data.keyword.Bluemix_dedicated_notm}} 部署的逻辑体系结构。

![{{site.data.keyword.Bluemix_dedicated_notm}}](images/bm_dedicated_arch.png "{{site.data.keyword.Bluemix_dedicated_notm}} default architecture")

图 1. 详细 {{site.data.keyword.Bluemix_dedicated_notm}} 图缺省体系结构
{: #figure01}

之前体系结构图中描述的重要体系结构组件包括以下项：

<dl>
<dt>{{site.data.keyword.IBM_notm}} Cloud</dt>
<dd>
{{site.data.keyword.IBM_notm}} Cloud 环境总体包含以下重要的联网环境：
<ul>
<li>{{site.data.keyword.Bluemix_dedicated_notm}}</li>
<li>{{site.data.keyword.Bluemix_notm}} Public</li>
<li>{{site.data.keyword.IBM_notm}} 运营</li>
</ul>
</dd>
<dt>{{site.data.keyword.Bluemix_dedicated_notm}}</dt>
<dd>
这至少包含 Cloud Foundry 组件和一些专用应用程序服务。{{site.data.keyword.Bluemix_notm}} 提供了 Cloud Foundry 和基于 {{site.data.keyword.containerlong}} 的计算环境。企业可配置其中一个计算环境，也可以同时配置这两个计算环境。<br>
企业可添加其他专用应用程序服务。<br>
有关可添加的其他服务和计算功能，请参阅[表 2](#table02)。
</dd>
<dt>{{site.data.keyword.Bluemix_notm}} Public</dt>
<dd>
{{site.data.keyword.Bluemix_dedicated_notm}} 可能包含 {{site.data.keyword.Bluemix_notm}} Public 区域的出站连接。这可将公共服务联合到专用目录中。借助 {{site.data.keyword.Bluemix_notm}} Public 服务联合，开发者可方便地构建在企业的 {{site.data.keyword.Bluemix_dedicated_notm}} 上托管的应用程序，也可便利地访问在 {{site.data.keyword.Bluemix_notm}} Public 中运行的服务。可从 {{site.data.keyword.Bluemix_notm}} Public 联合的服务列表在[联合目录部分的表 4](#catalogdedicated) 上显示。
</dd>
<dt>{{site.data.keyword.IBM_notm}} 运营</dt>
<dd>
{{site.data.keyword.IBM_notm}} 可管理、监视和维护专用平台与专用服务，以便您可以专注于构建创新应用程序。{{site.data.keyword.IBM_notm}} 运营支持服务 (OSS) 团队使用 {{site.data.keyword.IBM_notm}} 运营网络的 VPN 隧道连接来执行多种操作。
</dd>
<dt>企业</dt>
<dd>
企业网络环境可能具有与 {{site.data.keyword.Bluemix_dedicated_notm}} 的安全专用双向网络链路。此网络链路允许在 {{site.data.keyword.Bluemix_dedicated_notm}} 中托管的应用程序访问企业中的服务和资源，包括数据源和企业服务。另外，此网络链路还允许 {{site.data.keyword.Bluemix_dedicated_notm}} 使用 LDAP 来认证企业开发者和管理员。
<br>
<br>
有多个选项可用于创建受保护的专用网络链路。请与 IBM 技术专家交流有关您企业的最佳联网选项。<br>
<br>
从 {{site.data.keyword.Bluemix_dedicated_notm}} 到企业网络的缺省连接使用虚拟专用网 (VPN)。{{site.data.keyword.Bluemix_dedicated_notm}} 具有为高可用性配置的专用 1 Gbps Vyatta VPN 终止。
<br>
在 {{site.data.keyword.Bluemix_dedicated_notm}} 的缺省体系结构（如[图 1](#figure01) 所示）中，没有直接来自因特网的入站网络流量。如果企业希望允许通过因特网访问在 {{site.data.keyword.Bluemix_dedicated_notm}} 上托管的应用程序，那么必须通过企业网络配置访问权。</dd>
</dl>


## 设置 {{site.data.keyword.Bluemix_dedicated_notm}}
{: #setupdedicated}

{{site.data.keyword.Bluemix_dedicated_notm}} 旨在提供专用版本的 {{site.data.keyword.Bluemix_notm}} Public 产品。您可以通过 IBM 托管的 {{site.data.keyword.BluSoftlayer}} 帐户，使用 {{site.data.keyword.Bluemix_notm}} 服务和运行时来满足计算需求。

IBM 为您提供了使用受密码保护的登录来访问 {{site.data.keyword.Bluemix_dedicated_notm}} 的方式。您可以访问服务、运行时和关联的资源，还可以部署和除去 {{site.data.keyword.Bluemix_notm}} 应用程序。IBM 利用多个 {{site.data.keyword.BluSoftlayer}} 位置来交付 {{site.data.keyword.Bluemix_dedicated_notm}}，因此您可以通过就近的位置来获取您的专用版本。

要设置专用版本的 {{site.data.keyword.Bluemix_notm}}，请执行以下操作：

<ol>
<li>首先联系 IBM 指定的客户代表或<a href="https://console.ng.bluemix.net/?direct=classic/#/contactUs/cloudOEPaneId=contactUs" target="_blank">联系 {{site.data.keyword.Bluemix_notm}} <img src="../icons/launch-glyph.svg" alt="外部链接图标"></a>。</li>
<li>与 IBM 一起设置您的 {{site.data.keyword.Bluemix_dedicated_notm}} 实例，费用由您支付。每月的经常性费用基于要使用的专用服务以及对所有 {{site.data.keyword.Bluemix_notm}} 公共服务的预订。对于超出预订协议范围的任何费用，您会收到相应发票。</li>
<li>为设置 {{site.data.keyword.Bluemix_dedicated_notm}} 实例的每个阶段确定截止期限。有关所涉及的每个阶段和任务的信息，请参阅 <a href="/docs/dedicated/index.html#rolesresponsibilities">{{site.data.keyword.Bluemix_dedicated_notm}} 角色和责任</a>。</li>
<li>为专用实例选择 <a href="http://www.softlayer.com/data-centers" target="_blank">{{site.data.keyword.BluSoftlayer}} 数据中心位置 <img src="../icons/launch-glyph.svg" alt="外部链接图标"></a>。然后，创建专用平台和帐户。针对您的帐户，为组织中需要启动并运行专用实例的人员分配必要的角色。有关分配的角色的信息，请参阅 <a href="/docs/dedicated/index.html#rolesresponsibilities">{{site.data.keyword.Bluemix_dedicated_notm}} 角色和责任</a>。
</li>
<li>定义并建立企业网络与 {{site.data.keyword.Bluemix_dedicated_notm}} 实例之间的网络连接。有一个必需的网络安全设备，包含防火墙和防侵入功能，但此选项会产生关联成本。<ol type="a">
	<li>IBM 为专用实例安装监视和安全基础架构。</li>
	<li>IBM 安装您所选的单租户专用服务。</li>
	<li>您提供网络配置和端点（IP 地址或防火墙等）以及对 LDAP 的访问权（以便集成到 {{site.data.keyword.Bluemix_notm}} 中）。</li>
	</ol>
</li>
<li>为您环境的管理团队确定并分配角色。
	<ol type="a">
	<li>IBM 根据您提供的信息配置网络访问和 LDAP。为您指定的联系人授予管理访问权。还必须指定一名联系人来负责记帐和提供相应支持。</li>
	<li>IBM 在您的专用环境中设置联合目录，用于显示您的专用服务。联合目录还包含从 {{site.data.keyword.Bluemix_notm}} Public 联合的其他服务，供您使用。您可以选择根据自己的数据隐私和安全标准来确定哪些公共服务满足您的业务需求。</li>
	<li>您验证网络和防火墙配置以及 LDAP 端点和访问权。</li>
	</ol>
</li>
</ol>

对您的环境进行初始部署和配置的过程应类似于以下列表。有关每个任务负责人员的详细信息，请参阅[角色和责任](index.html#rolesresponsibilities)。

<ol>
<li>您选择使用哪个数据中心来托管专用实例。有关数据中心选项的信息，请参阅 <a href="http://www.softlayer.com/data-centers" target="_blank">{{site.data.keyword.BluSoftlayer}} 数据中心位置 <img src="../icons/launch-glyph.svg" alt="外部链接图标"></a>。</li>
<li>您为部署指定域名，以及要使用的标识。设置 {{site.data.keyword.Bluemix_notm}} 实例时，您会得到三个域。请选取 <code>*mycompany*.*region*.bluemix.net</code> 和 <code>*mycompany*.*region*.mybluemix.net</code> 的前缀。然后，选择第三个域的全名。<br />
<p>您可以根据自己的需要选择任意数量的定制域。不过，您应负责获取定制域的证书。有关创建定制域的信息，请参阅<a href="/docs/manageapps/updapps.html#domain">创建和使用定制域</a>。</p></li>
<li>您确定使用哪个公共帐户的所有者来在 {{site.data.keyword.Bluemix_notm}} Public 中代表您的公司。IBM 使用此帐户来跟踪联合服务使用情况。</li>
<li>您选择数据中心安全连接的类型。可选类型包括 {{site.data.keyword.Bluemix_notm}} VPN、{{site.data.keyword.Bluemix_notm}} Direct Link 和 AT&T Net Bond。</li>
<li>您决定是否将允许通过公共因特网对您的专用环境进行任何访问。</li>
<li>您选择要使用的认证的类型。可选类型包括 IBM 标识或 Active Directory。有关使用和注册 IBM 标识的信息，请参阅<a href="https://www.ibm.com/account/profile/us?page=regfaqhelp#4">帮助和常见问题</a>页面。</li>
<li>您为您环境的管理团队确定并分配角色。有关必须分配的角色的信息，请参阅 <a href="/docs/dedicated/index.html#rolesresponsibilities">{{site.data.keyword.Bluemix_dedicated_notm}} 角色和责任</a>。</li>
<li>IBM 部署核心平台，其中包含弹性运行时、控制台、管理功能和监视。</li>
<li>IBM 配置您对环境的管理访问权。</li>
<li>您可以开始使用您的专用实例来响应警报，该实例由 IBM 操作团队进行监视。</li>
</ol>

{{site.data.keyword.Bluemix_notm}} 实例设置完成后，您可以使用“管理”页面来监视和管理 {{site.data.keyword.Bluemix_notm}} 实例。有关更多信息，请参阅[管理 {{site.data.keyword.Bluemix_notm}} Local 和 Dedicated](../admin/index.html#mng)。有关升级和维护的信息，请参阅[维护专用实例](index.html#maintaindedicated)。

##角色和责任
{: #rolesresponsibilities}

如果设置了 {{site.data.keyword.Bluemix_dedicated_notm}} 帐户，请为组织中需要启动并运行实例的人员分配必要的角色。

###角色

以下列表显示了分配的客户角色和责任：

<dl>
<dt>**采购联系人**</dt>
<dd>与 IBM 代表一起建立 {{site.data.keyword.Bluemix_dedicated_notm}} 环境，包括确定组织中负责项目各个方面的相应人员。分配有此角色的人员将负责项目管理，对模式选择、商业安排以及客户资源访问安排进行监督。采购联系人是设置专用实例和跟踪部署过程的总联系人。</dd>
<dt>**合规管理人员**</dt>
<dd>与 IBM 代表一起选择符合您安全需求的拓扑和部署选项。分配有此角色的人员可与 IBM 合规顾问一起确定哪些部署模式可达到合规目标。</dd>
<dt>**网络专家**</dt>
<dd>与 IBM 代表一起规划用于部署 {{site.data.keyword.Bluemix_notm}} 的网络。分配有此角色的人员负责审查 IBM 要求的联网规范，并与 IBM 一起制定实施规划。安装和验证阶段结束后，分配有此角色的人员可对网络配置是否符合公司标准进行审批。</dd>
<dt>**DevOps 联系人**</dt>
<dd>与 IBM 代表一起规划和应用 {{site.data.keyword.Bluemix_notm}} 平台、服务和运行时所需的维护更新。分配有此角色的人员还将与 IBM 代表一起配置 {{site.data.keyword.Bluemix_dedicated_notm}} 实例。</dd>
<dt>运营联系人</dt>
<dd>环境启动并开始运行后，可根据需要与 IBM 支持团队一起工作。此人员对管理控制台具有 Superuser 访问权，可以批准和安排 Bluemix 环境的维护更新，并且在发生关键事件时可随时与此人员取得联系。分配有此角色的人员必须具备 Bluemix 环境的技术知识，并且必须能够联系到公司内具备可能受影响的某一领域（包括联网或安全性，等等）相关专家技能的其他人员。
</dd>
</dl>

您的客户代表会与 IBM 专家进行合作，共同来确保您始终拥有所需的支持。对于您的帐户，您可以升级到“高级”支持层，以便与专用客户成功经理 (CSM) 进行合作。有关不同支持层的更多信息，请参阅[联系支持](../support/index.html#contacting-support)。CSM 会完成以下类型的任务：

<ul>
<li>实现 {{site.data.keyword.Bluemix_dedicated_notm}} 环境的快速采用。</li>
<li>提供宝贵的培训和支持资料，以提升您的自身实力。</li>
<li>培养您与所使用 {{site.data.keyword.Bluemix_notm}} 开发、支持和服务之间的长期关系。</li>
</ul>

在 {{site.data.keyword.Bluemix_notm}} 实例上与您合作的 {{site.data.keyword.Bluemix_notm}} 支持和运营团队可能需要访问您的本地环境，但仅出于以下原因才会这样做。

<ul>
<li>响应警报和执行操作维护</li>
<li>尝试重现支持凭单上报告的问题</li>
</ul>

### 责任

从设置环境到持续维护的过程中，必须完成各种任务。下表列出了在先启、进展和完成各阶段所需的任务以及完成任务的所有者。

先启阶段用于建立 {{site.data.keyword.Bluemix_dedicated_notm}} 环境。此阶段的主要目标包含以下内容：

- 复查财务协议，并确定交付的里程碑日期。
- 创建 {{site.data.keyword.Bluemix_notm}} 平台，并提供对运行时和服务的访问权。
- 定义并建立企业网络与 {{site.data.keyword.Bluemix_notm}} 运营之间的网络连接。
- 为管理团队确定并分配角色。

| **任务** | **任务详细信息** | **责任方** |
|----------|------------------|-----------------------|
|设置合规标准 | 确定环境所需的政府、行业和专有公司标准。 | 客户 |
|创建安全和合规性集成计划 | 创建安全和集成计划，其中包含达到安全合规性所需的成本、计划安排和资源。 | IBM |
|合规性计划审批 | 审批合规性计划。 | 客户 |
|创建环境规模标准 |  	基于预定义的选项来创建环境规模标准，这些选项将高可用性、灾难恢复目标以及初始 DEA 和服务供应全部考虑在内，其中初始 DEA 和服务供应是为使用平台创建的应用程序提供支持所必需的。您和 IBM 一起定义一些内容，例如需要哪些数据库，以及在客户的联合目录中提供哪些服务等。 | IBM 和客户共担责任 |
|选择体系结构 | 基于预定义的选项来选择体系结构，这些选项将高可用性和灾难恢复需求考虑在内。 | IBM |
|定义灾难恢复目标 | 为环境定义灾难恢复需求。 | 客户 |
|创建灾难恢复计划 | 协商和定义灾难恢复计划。IBM 创建灾难恢复模型，并与您协商在何处由您提供反馈和审批计划。 | IBM 和客户共担责任 |
|创建备份和恢复计划 | 创建备份和恢复计划，其中定义现场和非现场分布的备份的频率和需求。IBM 备份光纤网组件、IBM 服务、服务元数据（包括用户角色）等。您备份自己负责的任何特定于应用程序的数据。 | IBM 和客户共担责任 |
|确定用于事件检测和问题确定的工具 | 确定用于在 {{site.data.keyword.Bluemix_notm}} 平台级别进行事件检测和问题确定的 IBM 和第三方工具。 | IBM |
|定义上报计划 | 定义上报计划以分类和解决从监视组件检测到的事件。 | IBM |
|签署基础架构、平台和支持协议 | 签署预订协议，包括环境的财务条款和条件。签署支持预订。 | 客户 |
|采购环境 | 采购计算资源、网络和存储，包括用于托管 {{site.data.keyword.Bluemix_notm}} 的核心和服务 VLAN、用于托管 DataPower 的裸机服务以及 {{site.data.keyword.Bluemix_notm}} 防火墙。提供基础架构以允许使用 VPN 隧道。 | IBM |
|安装光纤网、应用程序以及监视和管理组件 | 安装、配置和验证光纤网组件（例如，BOSH Director、云控制器、运行状况管理器、消息传递、路由器、DEA 和服务提供者），以及在上报和问题检测计划中定义的监视组件。 | IBM |
|安装和配置安全组件 | 安装和配置与监视和上报计划绑定的安全组件，包括 IBM QRadar、凭证保险库、入侵防御系统、IBM BigFix 和 IBM Security Privileged Identity Management。 | IBM |
|安装和配置定制组件 |  	安装和配置位于 {{site.data.keyword.Bluemix_notm}} 产品和服务范围之外的定制组件。 | 客户 |
|建立初始网络配置 | 建立初始网络配置，包括防火墙、DataPower、Fortigate 和 DNS。 | IBM |
|连接 {{site.data.keyword.Bluemix_notm}} 管道 | 将 {{site.data.keyword.Bluemix_notm}} 持续集成和持续交付管道与 IBM 存储库相连接。 | IBM |
|定制外部解决方案组件 | 为灾难恢复方案定制负载均衡器。 | 客户 |
|安装 VPN 解决方案 | 安装双向 VPN 解决方案。 | IBM |
|配置登录服务器 | 配置登录服务器以与公司 LDAP 配合使用。 | IBM |
|跟踪安全性、合规性和审计控制的状态  | 跟踪状态，直到所有工具和流程全部落实到位，达到确定的合规性为止。 | 客户 |
|审查物理基础架构 | 审查托管解决方案组件的物理部署是否有威胁，并查看用于保护数据中心的安全性控制。 | 客户 |
|检查监视软件 | 检查上报和问题确定计划中定义的监视和管理组件。 | 客户 |
|检查操作系统 | 检查以确保操作系统映像达到合规标准。IBM 提供对操作系统映像的访问权。 | IBM 和客户共担责任 |
{: caption="表 5. 先启阶段任务" caption-side="top"}


接下来是进展阶段。进展阶段描述了您和 IBM Cloud 的持续协作关系。此阶段的主要目标包含以下内容：

- 审查容量并进行必要的调整。
- 审查维护和平台改进。
- 协调问题解决和根本原因分析活动。

| **任务** | **任务详细信息** | **责任方** |
|----------|------------------|-----------------------|
|审查每周容量报告 | 审查每周容量报告，并根据需要采取纠正措施。 | 客户 |
|创建每月预测 | 收集容量和使用量信息，并创建容量和使用量的每月预测。 | IBM 和客户共担责任 |
|审查容量预测 | 审查容量预测，这些预测与可能影响容量的外部事件以及与预期的新应用程序部署相关。与 IBM 一起审查预测并相应地进行规划。 | IBM 和客户共担责任 |
|审查预测 | 审查容量预测，这些预测与可能影响容量的外部事件相关。 | 客户 |
|调整容量 |  随着需求的变化来增减容量。 | IBM |
|发布即将到来的更新和维护 | 为必需的 IBM 组件维护创建文档。 | IBM |
|执行维护 | 与 IBM 一起安排必需的维护（维护时段为 21 天）。您可以提供在 21 天的时段内可能不适合进行维护的日期，然后 IBM 会尽量相应地制定维护计划。 | IBM 和客户共担责任 |
|地址供应失败 | 针对部署到“目录”的客户创建的服务，解决供应失败问题（如果发生）。 | IBM |
|执行网络和 IP 扫描 | 执行每日和每月网络和 IP 扫描。 | IBM 和客户共担责任 |
|提供对审计日志的访问权 | 提供对所有安全和管理审计日志的访问权。   | IBM 和客户共担责任 |
|执行测试 | 执行定期“关键运营控制”测试和第三方渗透测试。 | IBM 和客户共担责任 |
|状态报告、审计协调和合规性会议  | 完成状态报告、外部审计协调以及在合规性审查状态会议上陈述。 | IBM |
|聘用和业务需求核查 | 针对有权访问客户环境的 IBM 代表，完成每季度就业核查和持续业务需求核查。 | IBM |
|解决安全漏洞 | 解决报告的平台安全漏洞。 | IBM |
{: caption="表 6. 进展阶段任务" caption-side="top"}

最后是完成阶段，此阶段表示您和 IBM {{site.data.keyword.Bluemix_notm}} 之间的关系结束。此阶段的主要任务包含以下内容：

* 结束财务协议
* 除去所有网络连接
* 回收基础架构


| **任务** | **任务详细信息** | **责任方** |
|----------|------------------|-----------------------|
|结束财务协议 | 讨论并同意结束财务协议合同。 | IBM 和客户共担责任 |
|解除环境 | 关闭对环境的访问以及环境的凭证。 | IBM 和客户共担责任 |
|除去客户网络连接 | 除去 IBM 与客户环境之间的网络连接。 | IBM 和客户共担责任 |
|回收基础架构 | 您的环境将基于 {{site.data.keyword.BluSoftlayer}} 定义的流程进行回收。 | IBM |
{: caption="表 7. 完成阶段任务" caption-side="top"}

##维护专用实例
{: #maintaindedicated}

IBM 会在 IBM 认为适当的时候，为 {{site.data.keyword.Bluemix_notm}} 运行时和服务维护并安装更新与修订。在维护时段内，服务可能会不可用。此外，IBM 会与您合作安排对 {{site.data.keyword.Bluemix_notm}} 平台的维护更新。

{{site.data.keyword.Bluemix_dedicated_notm}} 需要以下类型的维护：
<dl>
<dt>**服务标准维护**</dt>
<dd>服务会利用预定义的标准维护时段，而这可能会导致服务不可用。IBM 无需客户批准就能执行服务维护，但在执行维护时 IBM 会尝试尽可能减小对您服务的影响。<br />
<br />
IBM 会发送有关在“状态”页面上针对每个维护时段计划进行哪些更改的广播报文。<br />
<br />
**重要信息**：在维护期间，某个服务可能不可用。</dd>

<dt>**{{site.data.keyword.Bluemix_notm}} 平台标准维护**</dt>
<dd>将根据您与 IBM 的协商在 21 天时段中应用维护更新。您为 IBM 提供了预先批准的维护时段以及可能不适用于您的特定日期或时间，IBM 会尽量将更新安排在您选择的日期内或相邻日期执行。<p>
<p>转至**管理 > 系统信息**以查看安排的和暂挂的维护更新。有关设置预先批准的时段、不可用的日期以及查看或批准安排的维护更新的更多信息，请参阅<a href="/docs/admin/index.html#oc_schedulemaintenance">维护更新</a>。</p></dd>
</dl>

**重要信息**：IBM 保留在必要时中断服务来实施紧急维护的权利。IBM 可能会更改所安排的维护时间，但会通知您任何此类更改以及任何紧急维护信息。

如果在维护更新后报告有问题，您与 {{site.data.keyword.Bluemix_notm}} 支持人员协商，允许 IBM 回滚更新是否对您最有利。IBM 会根据商定的结果回滚更新，使环境复原到先前的状态。

## {{site.data.keyword.Bluemix_dedicated_notm}} 的事件响应和支持
{: #incidentresponse}

### 客户检测到的问题

如果识别到需要 IBM 支持和操作人员关注的问题，您可以使用多种不同的方法来联系支持人员。有关如何联系支持人员的信息，请参阅[联系支持人员](../support/index.html#contacting-bluemix-support-local)。根据问题情况，您和/或 IBM 可合作解决问题。

### IBM 检测到的严重事件

严重事件是指紧迫的意外服务中断以及影响您的环境或用户的稳定性问题。如果 IBM 检测到您的环境内有严重事件，那么会在**状态**页面上借助通知来告知您。您还可以检查“状态”页面来获取平台或服务的任何已知问题。有关“状态”页面的更多信息，请参阅[查看状态](../admin/index.html#oc_status)。

如果要将通知与支持 Web Hook 的 Web Service 集成在一起，请参阅[通知和事件预订](../admin/index.html#oc_eventsubscription)，以获取有关如何扩展通知功能的信息。

![事件响应过程](../local/images/incidentresponseprocess.png "事件响应过程")

图 2. 事件响应过程

根据问题情况，您和/或 IBM 可合作解决问题。如果您有与事件相关的疑问，或者需要 IBM 代表帮助您解决问题，那么可以开具支持凭单。有关如何联系支持人员的信息，请参阅[联系支持人员](/docs/support/index.html#contacting-bluemix-support-local)。

**注**：将全天候监视严重性为 1 的支持凭单。其他凭单的处理时间是周日晚上 10:00 GMT 到周六凌晨 12:00 GMT。有关支持凭单严重性和使用支持的更多信息，请参阅<a href="/docs/support/index.html#contacting-bluemix-support-local">联系支持人员</a>。


## {{site.data.keyword.Bluemix_dedicated_notm}} 的灾难恢复
{: #dr}

{{site.data.keyword.Bluemix_short}} Dedicated 灾难恢复可按照与使用 {{site.data.keyword.Bluemix_short}} Public 时类似的方式进行设置。{{site.data.keyword.Bluemix_short}} Public 提供了持续可用的创新平台，具有多种自动防故障措施，可确保您的组织、空间和应用程序始终可用。将应用程序部署到多个地理区域可实现持续可用性，避免多个硬件或软件组件同时发生意外故障，或者整个数据中心发生故障。这样，即使一个地理位置发生自然灾害，分布在其他地理位置中的 {{site.data.keyword.Bluemix_notm}} Public 应用程序实例也会可用。
{: shortdesc}

{{site.data.keyword.Bluemix_short}} Dedicated 的灾难恢复是通过应用程序的持续可用性、平台固有的高可用性以及发生故障时恢复实例的能力来实现的。您负责通过将应用程序部署到多个区域来实现应用程序的持续可用性。高可用性是通过 Cloud Foundry 和其他组件中包含的各种技术在平台级别构建的。此外，您可以与 IBM 合作，共同来确保数据已正确备份，可随时满足您的实例复原需求。

### 实现 {{site.data.keyword.Bluemix_dedicated_notm}} 的持续可用性
{: #enabling}

缺省情况下，{{site.data.keyword.Bluemix_notm}} Public 会部署到多个地理位置。但是，要实现 {{site.data.keyword.Bluemix_dedicated_notm}} 实例的全球分布，您必须执行以下操作：

* 确保您的开发者通过手动或自动过程将应用程序部署在多个区域。两个区域之间的距离应超过 200 公里，以确保自然灾害不会同时影响到这两个地理位置。
* 配置全球负载均衡器（如 Akamai 或 Dyn），以指向至少位于两个不同区域中的应用程序。

**注**：并非所有 {{site.data.keyword.Bluemix_notm}} 服务都支持区域分布。构造应用程序时，如果想要实现地理分布，还必须确保该应用程序使用的服务具有数据同步这一关键功能。

#### 将 {{site.data.keyword.Bluemix_dedicated_notm}} 应用程序部署到多个地理位置
{: #deploying}

要部署到第二个位置或多个位置，必须采用与启用主地理位置类似的过程：

1. 启用新的专用环境来托管应用程序的其他实例。要创建新环境，请联系 IBM 销售团队来开始这一过程。有关设置专用实例的更多信息，请参阅[设置 {{site.data.keyword.Bluemix_dedicated_notm}}](/docs/dedicated/index.html#setupdedicated)。要访问每个环境，必须分别登录。托管环境的每个物理位置都应该至少距离原始位置 200 公里，才可确保可用性。
2. 获取要在其中托管新部署应用程序的域的唯一域名。例如，如果原始域为 *mycompany.caeast.bluemix.net*，那么可以使用新域（例如，*mycompany.cawest.bluemix.net*）来创建新的本地环境，并部署到新域。
3. 每次部署原始应用程序时，也都会部署到新位置。有关部署的更多信息，请参阅[上传应用程序](/docs/starters/upload_app.html)。


#### 为 {{site.data.keyword.Bluemix_dedicated_notm}} 启用全球负载均衡器
{: #glb}

全球负载均衡器不仅能确保持续可用性，是灾难恢复所必需的，而且还具有其他若干优点：

* 缺省情况下，将用户路由到距离最近的 {{site.data.keyword.Bluemix_notm}} 区域
* 基于性能进行路由
* 选择性将一定百分比的流量定向到新的应用程序版本
* 根据区域运行状况检查，提供站点故障转移
* 根据应用程序运行状况检查，提供站点故障转移
* 在端点之间使用加权路由

您可以选择全球负载均衡器，例如 Akamai 或 Dyn。有关将 Akamai 用作全球负载均衡器的更多信息，请参阅 [Global traffic management ![外部链接图标](../icons/launch-glyph.svg)](https://www.akamai.com/us/en/solutions/products/web-performance/global-traffic-management.jsp "在新窗口中打开"){: new_window}。有关将 Dyn 用作全球负载均衡器的更多信息，请参阅 [4 Reasons Businesses Are Taking Global Load Balancing to the Cloud ![外部链接图标](../icons/launch-glyph.svg)](http://dyn.com/blog/4-reasons-businesses-are-taking-global-load-balancing-to-the-cloud/){: new_window}。

### 高可用性
{: #ha}

除了可实现持续可用性外，{{site.data.keyword.Bluemix_notm}} 还使用 Cloud Foundry 和其他组件中内置的技术，在整个平台提供高可用性。

这些技术包括以下各项：

<dl>
<dt>Cloud Foundry 中的 DEA 可扩展性</dt>
<dd>Cloud Foundry <a href="https://docs.cloudfoundry.org/concepts/architecture/execution-agent.html" target="_blank">Droplet Execution Agent (DEA) <img src="../icons/launch-glyph.svg" alt="外部链接图标"></a> 会对其中运行的应用程序执行运行状况检查。如果应用程序或 DEA 本身存在问题，那么它会将应用程序的其他实例部署到备用 DEA 来解决该问题。有关更多信息，请参阅<a href="https://docs.cloudfoundry.org/concepts/high-availability.html" target="_blank">配置 CF 以通过冗余实现高可用性 <img src="../icons/launch-glyph.svg" alt="外部链接图标"></a>。<p>要确保应用程序的高可用性，您需要有足够的计算资源来均衡负载，并且还可能需要额外的计算资源来支持可能发生的故障。如果需要通过增大 DEA 池来扩展环境，以做好准备应对故障或满足应用程序实例高峰负载要求，您可以联系 IBM 代表来订购更多 DEA，并确保您有相应的硬件来支持添加的资源。
</p>
</dd>
<dt>{{site.data.keyword.BluSoftlayer}} 冗余</dt>
<dd>在专用环境中使用 {{site.data.keyword.BluSoftlayer}} 时，每个云存储集群中的数据都会写入多次，而且存储集群都配置有在发生驱动器故障时进行自动修复的功能。如果某个虚拟服务器发生问题，{{site.data.keyword.BluSoftlayer}} 会尝试在其他主机上重新启动该虚拟服务器。</dd>
<dt>元数据备份</dt>
<dd>元数据会使用 {{site.data.keyword.BluSoftlayer}} EVault Backup 来备份到至少 200 公里远的位置。</dd>
</dl>

##复原专用实例
{: #restorededicated}

系统会定期备份 {{site.data.keyword.Bluemix_dedicated_notm}} 设置、元数据和配置，以做好准备来应对环境中的任何意外中断。您负责备份的数据包括应用程序数据、云数据库服务数据和对象存储。

在数据备份过程中（包括系统元数据和配置），IBM 会完成以下任务：

<ul>
<li>加密所有备份副本并管理加密密钥</li>
<li>监视并管理备份活动</li>
<li>提供加密的备份文件</li>
<li>复原所请求的数据</li>
<li>管理备份和修订管理操作之间的计划冲突</li>
</ul>

由于保护专用数据至关重要，因此 IBM 在处理备份文件管理时需要您的协作，以便不将文件移出您的数据中心。具体来说，IBM 会要求您完成以下任务：

<ul>
<li>异地备份一份您的加密备份数据，与您所管理的任何其他备份数据的处理方法一样。</li>
<li>向 IBM 操作员提供备份文件，以防万一有任何需要复原的情况。</li>
</ul>

# rellinks
{: rellinks}
## general
{: general}
* [Discover: {{site.data.keyword.Bluemix_dedicated_notm}}](http://www.ibm.com/cloud-computing/bluemix/hybrid/dedicated/)
* [{{site.data.keyword.Bluemix_notm}} 中的新增功能](/docs/whatsnew/index.html)
* [{{site.data.keyword.Bluemix_notm}} 词汇表](/docs/overview/glossary/index.html)
* [管理 {{site.data.keyword.Bluemix_notm}} Local 和 {{site.data.keyword.Bluemix_dedicated_notm}}](/docs/admin/index.html#mng)
* [联系支持人员](/docs/support/index.html#getting-customer-support)
