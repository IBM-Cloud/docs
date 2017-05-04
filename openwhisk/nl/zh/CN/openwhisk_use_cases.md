---

copyright:
  years: 2016, 2017
lastupdated: "2017-03-15"

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

尽管基于微服务的解决方案具有优势，但要使用主流云技术来构建这些解决方案仍然很困难，这通常需要控制复杂的工具链，以及单独的构建和运行管道。小型敏捷团队要花太多时间来处理复杂的基础架构和操作事项（容错、负载平衡、自动扩展和日志记录），因此特别希望有一种方法能使用他们熟知惯用且最适合解决特定问题的编程语言来开发精简的、增加价值的代码。

{{site.data.keyword.openwhisk_short}} 具有模块化和内在可扩展的性质，因此非常适用于在操作中实现细颗粒度的逻辑片段。{{site.data.keyword.openwhisk_short}} 操作彼此独立，可以使用 {{site.data.keyword.openwhisk_short}} 支持的各种不同语言来实现，并可访问各种后端系统。每个操作都可以独立部署和管理，并可独立于其他操作进行扩展。操作之间的互连由 {{site.data.keyword.openwhisk_short}} 以规则、序列和命名约定的形式提供。这对基于微服务的应用程序来说是件好事。

支持 {{site.data.keyword.openwhisk_short}} 的另一重要理由是灾难恢复配置中系统的成本。下面我们将使用 PaaS 或 CaaS 的微服务与使用 {{site.data.keyword.openwhisk_short}} 的微服务比较一下。假定有 10 个微服务使用容器或 CloudFoundry 运行时，如果是在单个可用性专区 (AZ) 中就有 10 个持续运行中的计费进程，跨 2 个 AZ运行就有 20 个，而跨 2 个区域（每个区域 2 个专区）运行就有 40 个。通过在 {{site.data.keyword.openwhisk_short}} 中运行微服务来执行同样操作时，可以根据需要跨任意数量的 AZ 和区域来运行微服务，而不会产生丝毫的递增成本。

[Logistics Wizard](https://www.ibm.com/blogs/bluemix/2017/02/microservices-multi-compute-approach-using-cloud-foundry-openwhisk/) 是一个企业级样本应用程序，利用 {{site.data.keyword.openwhisk_short}} 和 CloudFoundry 来构建 12 因子样式的应用程序。这种智能供应链管理解决方案旨在模拟运行 ERP 系统的环境。它会使用应用程序来扩增此 ERP 系统，以提高供应链管理员的可视性和敏捷性。

## Web 应用程序
{: #openwhisk_common_use_cases_webapps}

鉴于 {{site.data.keyword.openwhisk_short}} 的事件驱动型性质，它对于面向用户的应用程序有若干优点，而来自用户浏览器的 HTTP 请求会充当事件。{{site.data.keyword.openwhisk_short}} 应用程序仅在处理用户请求时才使用计算能力并计费。不存在空闲备用或等待模式这类情况。而传统容器或 Cloud Foundry 应用程序可能大部分时间一直在等待入局用户请求，并且即使处于这些“睡眠”时间也照样要计费，相比之下，{{site.data.keyword.openwhisk_short}} 就要便宜得多。 

完整的 Web 应用程序可以使用 {{site.data.keyword.openwhisk_short}} 来构建并运行。将无服务器 API 与站点资源（例如，HTML、JavaScript 和 CSS）的静态文件托管相组合，意味着我们可以构建完整的无服务器 Web 应用程序。运行托管的 {{site.data.keyword.openwhisk_short}} 环境（或者干脆不必运行任何内容，因为是在 Bluemix 上托管）十分简单，这与维持并运行 Node.js Express 或其他传统服务器运行时相比，是一个非常大的优势。

下面是有关如何使用 {{site.data.keyword.openwhisk_short}} 构建 Web 应用程序的一些示例：
- [Web Actions: Serverless Web Apps with {{site.data.keyword.openwhisk_short}}](https://medium.com/openwhisk/web-actions-serverless-web-apps-with-openwhisk-f21db459f9ba)。
- [Build a user-facing {{site.data.keyword.openwhisk_short}} application with Bluemix and Node.js](https://www.ibm.com/developerworks/cloud/library/cl-openwhisk-node-bluemix-user-facing-app/index.html)
- [Serverless HTTP handlers with {{site.data.keyword.openwhisk_short}}](https://medium.com/openwhisk/serverless-http-handlers-with-openwhisk-90a986cc7cdd)

## IoT
{: #openwhisk_common_use_cases_iot}

Internet of Things 场景通常具备由传感器驱动的固有性质。例如，如果需要对超过特定温度的传感器做出反应，那么可能会触发 {{site.data.keyword.openwhisk_short}} 中的操作。IoT 交互通常是无状态的，有潜力应对发生重大事件（自然灾害、重大天气事件、交通堵塞等）时的超高负载水平。这将产生对弹性系统的需求，在这种系统中，正常工作负载可能很小，但需要能够以可预测的响应时间非常快速地进行扩展，并且有能力处理数量极其庞大的事件而无需对系统预先警告。使用传统服务器体系结构来构建满足这些需求的系统是非常困难的，因为它们往往要么能力不足，无法处理流量高峰情况，要么过度配置，费用极其高昂。

当然可以使用传统的服务器体系结构来实现 IoT 应用程序，但是在许多情况下，不同服务和数据网桥的组合需要高性能、灵活的管道，范围从 IoT 设备一直到云存储和分析平台。预配置的网桥往往缺乏实现和微调特定解决方案体系结构所需的可编程性。考虑到可能有种类庞杂的管道以及数据融合在一般情况下缺乏标准化（在 IoT 中尤其如此），在许多情况下，管道都需要定制数据变换（用于格式转换、过滤、扩充等）。{{site.data.keyword.openwhisk_short}} 是一款非常优秀的工具，能以“无服务器”方式实现此类变换，其中定制逻辑在完全受管的弹性云平台上进行托管。

下面是使用 {{site.data.keyword.openwhisk_short}}、NodeRed、Cognitive 和其他服务的样本 IoT 应用程序：[Serverless transformation of IoT data-in-motion with {{site.data.keyword.openwhisk_short}}](https://medium.com/openwhisk/serverless-transformation-of-iot-data-in-motion-with-openwhisk-272e36117d6c#.akt3ocjdt)。

![IoT 解决方案体系结构示例](images/IoT_solution_architecture_example.png)

## API 后端
{: #openwhisk_common_use_cases_iot}

通过无服务器计算平台，开发者能快速构建 API，而无需服务器。{{site.data.keyword.openwhisk_short}} 支持为操作自动生成 REST API。{{site.data.keyword.openwhisk_short}} 的[试验性功能](./apigateway.md)将允许您通过 POST 之外的 HTTP 方法调用操作，也允许在没有操作的授权 API 密钥的情况下，通过 {{site.data.keyword.openwhisk_short}} API 网关调用操作。此功能不仅对于向外部使用者公开 API 非常有用，同时对于构建微服务应用程序也十分有用。

此外，{{site.data.keyword.openwhisk_short}} 操作可以连接到所选的 API 管理工具（例如，[IBM API Connect](https://www-03.ibm.com/software/products/en/api-connect) 或其他工具）。与其他用例类似，所有关于可扩展性和其他服务质量 (QoS) 的注意事项都适用。 

[Emoting](https://github.com/l2fprod/openwhisk-emoting) 是一个样本应用程序，通过 REST API 来使用 {{site.data.keyword.openwhisk_short}} 操作。

下面是关于[将无服务器用作 API 后端](https://martinfowler.com/articles/serverless.html#ACoupleOfExamples)的示例和讨论。

## 移动后端
{: #openwhisk_common_use_cases_mobile}

许多移动应用程序需要服务器端逻辑。考虑到移动开发者通常在管理服务器端逻辑方面没有什么经验，而更倾向于关注设备上运行的应用程序，所以比较好的解决方案是将 {{site.data.keyword.openwhisk_short}} 用作服务器端后端。此外，对服务器端 Swift 的内置支持也允许开发者复用自己现有的 iOS 编程技能。移动应用程序通常具有不可预测的负载模式和托管的 {{site.data.keyword.openwhisk_short}} 解决方案，例如 IBM Bluemix 可以扩展以满足对工作负载的几乎任何需求，而无需提前供应资源。

[Skylink](https://github.com/IBM-Bluemix/skylink) 是一个样本应用程序，允许您通过 iPad 将无人驾驶飞机连接到 IBM 云，并利用 {{site.data.keyword.openwhisk_short}}、IBM Cloudant、IBM Watson 和 Alchemy Vision 进行近实时图像分析。

[BluePic](https://github.com/IBM-Swift/BluePic) 是一种照片和图像共享应用程序，允许您拍照并与其他 BluePic 用户共享。此应用程序演示了如何在移动 iOS 10 应用程序中利用以 Swift 编写的基于 Kitura 的服务器应用程序，并且将 {{site.data.keyword.openwhisk_short}}、Cloudant 和 Object Storage 用于图像数据。AlchemyAPI 还可用于 {{site.data.keyword.openwhisk_short}} 序列中，以分析图像并基于图像内容来抽取文本标记，然后向用户发送推送通知。

## 数据处理
{: #openwhisk_common_use_cases_data}

针对现在可用的数据量，应用程序开发需要处理新数据并可能对其做出响应的能力。此需求包括处理结构化数据库记录以及非结构化的文档、图像或视频。{{site.data.keyword.openwhisk_short}} 可以通过系统提供的订阅源或定制订阅源来进行配置，以对数据的变化做出反应，并对入局数据订阅源自动执行操作。操作可以编程为处理更改，变换数据格式，发送和接收消息，调用其他操作，更新各种数据存储（包括基于 SQL 的关系数据库、内存中数据网格、NoSQL 数据库、文件、消息传递代理和各种其他系统）。通过 {{site.data.keyword.openwhisk_short}} 规则和序列，可灵活地在处理管道时进行更改，无需编程 - 只需进行配置更改即可。这使得基于 {{site.data.keyword.openwhisk_short}} 的系统具有高度敏捷性，能轻松调整以适应不断变化的需求。

[OpenChecks](https://github.com/krook/openchecks) 项目是一种概念证明，显示了 {{site.data.keyword.openwhisk_short}} 可如何用于通过光学字符识别来处理将支票存入银行账户的过程。目前，此项目是基于公共 Bluemix {{site.data.keyword.openwhisk_short}} 服务构建的，并依赖于 Cloudant 和 SoftLayer Object Storage。在内部部署中，此项目可使用 CouchDB 和 OpenStack Swift。其他存储服务可能包括 FileNet 或 Cleversafe。Tesseract 提供 OCR 库。
## 认知
{: #openwhisk_common_use_cases_cognitive}

认知技术可以有效地与 {{site.data.keyword.openwhisk_short}} 组合使用来创建功能强大的应用程序。例如，IBM Alchemy API 和 Watson Visual Recognition 可以与 {{site.data.keyword.openwhisk_short}} 配合使用，以自动从视频中抽取有用的信息，而不必实际观看视频。这可能只是先前讨论的[数据处理](#data-processing)用例的“认知”扩展。{{site.data.keyword.openwhisk_short}} 的另一个有效用途是与认知服务组合使用来实现 Bot 功能。 

下面的样本应用程序 [Dark vision](https://github.com/IBM-Bluemix/openwhisk-darkvisionapp) 就可以做到这一点。在此应用程序中，用户使用 Dark Vision Web 应用程序上传视频或图像，该 Web 应用程序会将其存储在 Cloudant 数据库中。一旦上传视频后，{{site.data.keyword.openwhisk_short}} 会通过侦听 Cloudant 更改（触发器）来检测到新视频。然后，{{site.data.keyword.openwhisk_short}} 会触发视频抽取器操作。在其执行过程中，抽取器会生成帧（图像），并将其存储在 Cloudant 中。随后，将使用 Watson Visual Recognition 对这些帧进行处理，得到的结果将存储在相同的 Cloudant 数据库中。这些结果可以使用 Dark Vision Web 应用程序或 iOS 应用程序进行查看。除了 Cloudant 外，还可以使用 Object Storage。若使用 Object Storage，那么视频和图像元数据会存储在 Cloudant 中，而媒体文件存储在 Object Storage 中。

下面是[示例 iOS Swift 应用程序](https://github.com/gconan/BluemixMobileServicesDemoApp)，显示了 {{site.data.keyword.openwhisk_short}}、IBM Mobile Analytics 和 Watson 如何分析语调并将其发布到 Slack 通道。

## 使用 Kafka 或 Message Hub 进行事件处理 

{{site.data.keyword.openwhisk_short}} 非常适合与 Kafka、IBM Message Hub 服务（基于 Kafka）和其他消息传递系统组合使用。这些系统的性质是事件驱动型，因而需要事件驱动型运行时来处理消息并将业务逻辑应用于这些消息，这正是 {{site.data.keyword.openwhisk_short}} 通过其订阅源、触发器、操作等提供的功能。Kafka 和 Message Hub 通常用于处理非常高且不可预测的工作负载量，并且要求这些消息的使用者能随时进行扩展，这也正是 {{site.data.keyword.openwhisk_short}} 擅长之处。{{site.data.keyword.openwhisk_short}} 具有内置功能，可使用以及发布 [openwhisk-package-kafka](https://github.com/openwhisk/openwhisk-package-kafka) 包中提供的消息。

下面是通过 {{site.data.keyword.openwhisk_short}}、Message Hub 和 Kafka [实施事件处理场景的示例应用程序](https://github.com/IBM/openwhisk-data-processing-message-hub)。
