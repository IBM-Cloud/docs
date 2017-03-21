---

copyright:
  years: 2016, 2017
lastupdated: "2016-02-21"

---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}
{:screen: .screen}
{:pre: .pre}

# {{site.data.keyword.openwhisk_short}} 一般用例
{: #openwhisk_common_use_cases}

{{site.data.keyword.openwhisk_short}} 提供的执行模型支持各种用例。以下各部分包含典型的示例。有关无服务器体系结构、示例用例、利弊讨论和实施最佳实践的更详细讨论，请阅读 [Martin Fowler 博客中 Mike Roberts 所写的精彩文章](https://martinfowler.com/articles/serverless.html)。
{: shortdesc}

## 微服务
{: #openwhisk_common_use_cases_microservices}

尽管基于微服务的解决方案具有优势，但要使用主流云技术来构建这些解决方案仍然很困难，这通常需要控制复杂的工具链，以及单独的构建和运行管道。小型敏捷团队要花太多时间来处理基础架构和操作复杂性（容错、负载平衡、自动扩展和日志记录），因此特别希望有一种方法能使用他们熟知惯用且最适合解决特定问题的编程语言来开发精简的、增加价值的代码。 

{{site.data.keyword.openwhisk_short}} 具有模块化和内在可扩展的性质，因此非常适用于在操作中实现细颗粒度的逻辑片段。{{site.data.keyword.openwhisk_short}} 操作彼此独立，可以使用 {{site.data.keyword.openwhisk_short}} 支持的各种不同语言来实现，并可访问各种后端系统。每个操作都可以独立部署和管理，并可独立于其他操作进行扩展。操作之间的互连由 {{site.data.keyword.openwhisk_short}} 以规则、序列和命名约定的形式提供。这对基于微服务的应用程序来说是件好事。

## Web 应用程序
{: #openwhisk_common_use_cases_webapps}

尽管 {{site.data.keyword.openwhisk_short}} 最初设计用于基于事件的编程，但对于面向用户的应用程序，它也具备若干优点。例如，如果将其与小型 Node.js 存根相组合，可以将其用于为相对容易调试的应用程序提供服务。此外，由于 {{site.data.keyword.openwhisk_short}} 应用程序的计算量比在 PaaS 平台上运行服务器进程所需的计算量少得多，因此也便宜得多。 

完整的 Web 应用程序可以使用 OpenWhisk 来构建并运行。将无服务器 API 与站点资源（例如，HTML、JavaScript 和 CSS）的静态文件托管相组合，意味着我们可以构建完整的无服务器 Web 应用程序。运行托管的 {{site.data.keyword.openwhisk_short}} 环境（或者干脆不必运行任何内容，因为是在 Bluemix 上托管）十分简单，这与维持并运行 Node.js Express 或其他传统服务器运行时相比，是一个非常大的优势。

其中很有用的一点是 {{site.data.keyword.openwhisk_short}} CLI *wsk* 工具的名为“--annotation web-export true”的选项，此选项支持通过 Web 浏览器访问代码。

下面是有关如何使用 {{site.data.keyword.openwhisk_short}} 构建 Web 应用程序的一些示例：
- [Web Actions: Serverless Web Apps with OpenWhisk](https://medium.com/openwhisk/web-actions-serverless-web-apps-with-openwhisk-f21db459f9ba)。
- [Build a user-facing {{site.data.keyword.openwhisk_short}} application with Bluemix and Node.js](https://www.ibm.com/developerworks/cloud/library/cl-openwhisk-node-bluemix-user-facing-app/index.html)
- [Serverless HTTP handlers with OpenWhisk](https://medium.com/openwhisk/serverless-http-handlers-with-openwhisk-90a986cc7cdd)

## IoT
{: #openwhisk_common_use_cases_iot}

当然可以使用传统的服务器体系结构来实现 IoT 应用程序，但是在许多情况下，不同服务和数据网桥的组合需要高性能、灵活的管道，范围从 IoT 设备一直到云存储和分析平台。预配置的网桥往往缺乏实现和微调特定解决方案体系结构所需的可编程性。考虑到可能有种类庞杂的管道以及数据融合在一般情况下缺乏标准化（在 IoT 中尤其如此），在许多情况下，管道都需要定制数据变换（用于格式转换、过滤、扩充等）。{{site.data.keyword.openwhisk_short}} 是一款非常优秀的工具，能以“无服务器”方式实现此类变换，其中定制逻辑在完全受管的弹性云平台上进行托管。

Internet of Things 场景通常具备由传感器驱动的固有性质。例如，如果需要对超过特定温度的传感器做出反应，那么可能会触发 {{site.data.keyword.openwhisk_short}} 中的操作。IoT 交互通常是无状态的，有潜力应对发生重大事件（自然灾害、重大天气事件、交通堵塞等）时的超高负载水平。这将产生对弹性系统的需求，在这种系统中，正常工作负载可能很小，但需要能够以可预测的响应时间非常快速地进行扩展，并且有能力处理数量极其庞大的事件而无需对系统预先警告。使用传统服务器体系结构来构建满足这些需求的系统是非常困难的，因为它们往往要么能力不足，无法处理流量高峰情况，要么过度配置，费用极其高昂。

下面是使用 OpenWhisk、NodeRed、Cognitive 和其他服务的样本 IoT 应用程序：[Serverless transformation of IoT data-in-motion with OpenWhisk](https://medium.com/openwhisk/serverless-transformation-of-iot-data-in-motion-with-openwhisk-272e36117d6c#.akt3ocjdt)。

![IoT 解决方案体系结构示例](images/IoT_solution_architecture_example.png)

## API 后端
{: #openwhisk_common_use_cases_iot}

通过无服务器计算平台，开发者能快速构建 API，而无需服务器。{{site.data.keyword.openwhisk_short}} 支持自动为操作生成 REST API，并且可以非常轻松地将您所选的 API 管理工具（例如 [IBM API Connect](https://www-03.ibm.com/software/products/en/api-connect) 或其他工具）连接到 OpenWhisk 提供的这些 REST API。与其他用例类似，所有关于可扩展性和其他服务质量 (QoS) 的注意事项都适用。 

下面是关于[将无服务器用作 API 后端](https://martinfowler.com/articles/serverless.html#ACoupleOfExamples)的示例和讨论。

## 移动后端
{: #openwhisk_common_use_cases_mobile}

许多移动应用程序需要服务器端逻辑。对于不想管理服务器端逻辑，而更倾向于关注在设备或浏览器上运行的应用程序的移动开发者，比较好的解决方案是将 {{site.data.keyword.openwhisk_short}} 用作服务器端后端。此外，内置 Swift 支持也允许开发者复用自己现有的 iOS 编程技能。移动应用程序通常具有不可预测的负载模式和托管的 {{site.data.keyword.openwhisk_short}} 解决方案，例如 IBM Bluemix 可以扩展以满足对工作负载的几乎任何需求，而无需提前供应资源。

## 数据处理
{: #openwhisk_common_use_cases_data}

针对现在可用的数据量，应用程序开发需要处理新数据并可能对其做出响应的能力。此需求包括处理结构化数据库记录以及非结构化的文档、图像或视频。{{site.data.keyword.openwhisk_short}} 可以通过系统提供的订阅源或定制订阅源来进行配置，以对数据的变化做出反应，并对入局数据订阅源自动执行操作。操作可以编程为处理更改，变换数据格式，发送和接收消息，调用其他操作，更新各种数据存储（包括基于 SQL 的关系数据库、内存中数据网格、NoSQL 数据库、文件、消息传递代理和各种其他系统）。通过 {{site.data.keyword.openwhisk_short}} 规则和序列，可灵活地在处理管道时进行更改，无需编程 - 只需进行配置更改即可。这使得基于 {{site.data.keyword.openwhisk_short}} 的系统具有高度敏捷性，能轻松调整以适应不断变化的需求。

## 认知
{: #openwhisk_common_use_cases_cognitive}

认知技术可以有效地与 {{site.data.keyword.openwhisk_short}} 组合使用来创建功能强大的应用程序。例如，IBM Alchemy API 和 Watson Visual Recognition 可以与 {{site.data.keyword.openwhisk_short}} 配合使用，以自动从视频中抽取有用的信息，而不必实际观看视频。 

下面的样本应用程序 [Dark vision](https://github.com/IBM-Bluemix/openwhisk-darkvisionapp) 就可以做到这一点。在此应用程序中，用户使用 Dark Vision Web 应用程序上传视频或图像，该 Web 应用程序会将其存储在 Cloudant 数据库中。一旦上传视频后，{{site.data.keyword.openwhisk_short}} 会通过侦听 Cloudant 更改（触发器）来检测到新视频。然后，{{site.data.keyword.openwhisk_short}} 会触发视频抽取器操作。在其执行过程中，抽取器会生成帧（图像），并将其存储在 Cloudant 中。随后，将使用 Watson Visual Recognition 对这些帧进行处理，得到的结果将存储在相同的 Cloudant 数据库中。这些结果可以使用 Dark Vision Web 应用程序或 iOS 应用程序进行查看。除了 Cloudant 外，还可以使用 Object Storage。若使用 Object Storage，那么视频和图像元数据会存储在 Cloudant 中，而媒体文件存储在 Object Storage 中。
