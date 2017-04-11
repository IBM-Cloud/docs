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

# {{site.data.keyword.openwhisk_short}} common use cases
{: #openwhisk_common_use_cases}

The execution model that is offered by {{site.data.keyword.openwhisk_short}} supports a variety of use cases. The following sections include typical examples. For a more detailed discussion of Serverless architecture, example uses cases, pros and cons discussion and implementation best practices, please read excellent [Mike Roberts article on Martin Fowler's blog](https://martinfowler.com/articles/serverless.html).
{: shortdesc}

## Microservices
{: #openwhisk_common_use_cases_microservices}

Despite their benefit, microservice-based solutions remain difficult to build using mainstream cloud technologies, often requiring control of a complex toolchain, and separate build and operations pipelines. Small and agile teams, spending too much time dealing with infrastructural and operational complexities (fault-tolerance, load balancing, auto-scaling, and logging), especially want a way to develop streamlined, value-adding code with programming languages they already know and love and that are best suited to solve particular problems.

The modular and inherently scalable nature of {{site.data.keyword.openwhisk_short}} makes it ideal for implementing granular pieces of logic in actions. {{site.data.keyword.openwhisk_short}} actions are independent of each other and can be implemented using variety of different languages supported by {{site.data.keyword.openwhisk_short}} and access various backend systems. Each action can be independently deployed and managed, is scaled independently of other actions. Interconnectivity between actions is provided by {{site.data.keyword.openwhisk_short}} in the form of rules, sequences and naming conventions. This bodes well for microservices based applications.

Another important argument in favor of {{site.data.keyword.openwhisk_short}} is the cost of a system in a disaster recovery configuration. Let's compare microservices with PaaS or CaaS vs. using {{site.data.keyword.openwhisk_short}}. Assuming we have 10 microservices using containers or CloudFoundry runtimes, that's 10 continuously running and billable processes in a single availability zone, 20 when running them across 2 AZs and 40 when running them across 2 regions with two zones each. When doing the same by running the microservices in {{site.data.keyword.openwhisk_short}}, you can run microservices across as many AZs and regions as you like, with not having to pay a penny of incremental costs.

[Logistics Wizard](https://www.ibm.com/blogs/bluemix/2017/02/microservices-multi-compute-approach-using-cloud-foundry-openwhisk/) is an enterprise-grade sample application which leverages {{site.data.keyword.openwhisk_short}} and CloudFoundry to build 12-factor style application. It is a smart supply chain management solution that aims to simulate an environment running an ERP system. It augments this ERP system with applications to improve the visibility and agility of supply chain managers.

## Web apps
{: #openwhisk_common_use_cases_webapps}

Given {{site.data.keyword.openwhisk_short}}’s event-driven nature, it offers several benefits for user-facing applications, whereas the HTTP requests coming from the user’s browser serve as the events. {{site.data.keyword.openwhisk_short}} applications use compute capacity and billed only when they are serving user requests. There is no such thing as idle standby or waiting mode. This makes {{site.data.keyword.openwhisk_short}} considerably less expensive compared to traditional containers or CloudFoundry applications that might be spending most of their time simply waiting for incoming user request and being billed for all that “sleeping” time. 

Full web application can be built and run with {{site.data.keyword.openwhisk_short}}. Combining serverless APIs with static file hosting for site resources, e.g. HTML, JavaScript and CSS, means we can build entire serverless web applications. The simplicity of operating a hosted {{site.data.keyword.openwhisk_short}} environment (or rather not having to operate anything at all since it is hosted on Bluemix) is a great benefit compared to standing up and operating a Node.js Express or other traditional server runtime.

Here are few examples on how to use {{site.data.keyword.openwhisk_short}} to build a web app:
- [Web Actions: Serverless Web Apps with {{site.data.keyword.openwhisk_short}}](https://medium.com/openwhisk/web-actions-serverless-web-apps-with-openwhisk-f21db459f9ba).
- [Build a user-facing {{site.data.keyword.openwhisk_short}} application with Bluemix and Node.js](https://www.ibm.com/developerworks/cloud/library/cl-openwhisk-node-bluemix-user-facing-app/index.html)
- [Serverless HTTP handlers with {{site.data.keyword.openwhisk_short}}](https://medium.com/openwhisk/serverless-http-handlers-with-openwhisk-90a986cc7cdd)

## IoT
{: #openwhisk_common_use_cases_iot}

Internet of Things scenarios are often inherently sensor-driven. For example, an action in {{site.data.keyword.openwhisk_short}} might be triggered if there is a need to react to a sensor that is exceeding a particular temperature. IoT interactions are usually stateless with potential for very high level of load in case of major events (natural disasters, significant weather events, traffic jams, etc.) This creates a need for an elastic system where normal workload might be small, but needs to scale very quickly with predictable response time and ability to handle extremely large number of events with no prior warning to the system. It is very hard to build a system to meet these requirements using traditional server architectures as they tend to either be underpowered and unable to handle peak in traffic or be overprovisioned and extremely expensive.

It is certainly possible to implement IoT applications using traditional server architectures, however in many cases the combination of different services and data bridges requires high performance and flexible pipelines, spanning from IoT devices up to cloud storage and an analytics platform. Often pre-configured bridges lack the programmability required to implement and fine-tune a particular solution architecture. Given the huge variety of possible pipelines and the lack of standardization around data fusion in general and in IoT in particular, there are many cases where the pipeline requires custom data transformation (for format conversion, filtering, augmentation, etc). {{site.data.keyword.openwhisk_short}} is an excellent tool to implement such a transformation, in a ‘serverless’ manner, where the custom logic is hosted on a fully managed and elastic cloud platform.

Here is a sample IoT application that uses {{site.data.keyword.openwhisk_short}}, NodeRed, Cognitive and other services: [Serverless transformation of IoT data-in-motion with {{site.data.keyword.openwhisk_short}}](https://medium.com/openwhisk/serverless-transformation-of-iot-data-in-motion-with-openwhisk-272e36117d6c#.akt3ocjdt).

![IoT solution architecture example](images/IoT_solution_architecture_example.png)

## API backend
{: #openwhisk_common_use_cases_iot}

Serverless computing platforms give developers a rapid way to build APIs without servers. {{site.data.keyword.openwhisk_short}} supports automatic generation of REST API for actions. The [experimental feature](./apigateway.md) of {{site.data.keyword.openwhisk_short}} allows you to invoke an action with HTTP methods other than POST and without the action's authorization API key through the {{site.data.keyword.openwhisk_short}} API Gateway. This capability is helpful not only for exposing APIs to external consumers, but also for building microservices applications.

Additionally, {{site.data.keyword.openwhisk_short}} actions can be connected to an API Management tool of choice (such as [IBM API Connect](https://www-03.ibm.com/software/products/en/api-connect) or other). Similar to other use cases, all considerations for scalability, and other Qualities of Services (QoS) apply. 

[Emoting](https://github.com/l2fprod/openwhisk-emoting) is a sample app that uses {{site.data.keyword.openwhisk_short}} actions via REST API.

Here is an example and a discussion of [using Serverless as an API backend](https://martinfowler.com/articles/serverless.html#ACoupleOfExamples).

## Mobile back end
{: #openwhisk_common_use_cases_mobile}

Many mobile applications require server-side logic. Given that mobile developers usually don’t have experience in managing server-side logic and would rather focus on the app that is running on the device, using {{site.data.keyword.openwhisk_short}} as the server-side back end is a good solution. In addition, the built-in support for server-side Swift allows developers to reuse their existing iOS programming skills. Mobile applications often have unpredictable load patterns and hosted {{site.data.keyword.openwhisk_short}} solution, such as IBM Bluemix can scale to meet practically any demand in workload without the need to provision resources ahead of time.

[Skylink](https://github.com/IBM-Bluemix/skylink) is a sample application that lets you connect a drone aircraft via iPad to the IBM Cloud with near realtime image analysis leveraging {{site.data.keyword.openwhisk_short}}, IBM Cloudant, IBM Watson, and Alchemy Vision.

[BluePic](https://github.com/IBM-Swift/BluePic) is a photo and image sharing application that allows you to take photos and share them with other BluePic users. This application demonstrates how to leverage, in a mobile iOS 10 application, a Kitura-based server application written in Swift, uses {{site.data.keyword.openwhisk_short}}, Cloudant, Object Storage for image data. AlchemyAPI is also used in the {{site.data.keyword.openwhisk_short}} sequence to analyze the image and extract text tags based on the content of the image and then to send a push notification to the user.

## Data processing
{: #openwhisk_common_use_cases_data}

With the amount of data now available, application development requires the ability to process new data, and potentially react to it. This requirement includes processing both structured database records as well as unstructured documents, images, or videos. {{site.data.keyword.openwhisk_short}} can be configured via system provided or custom feeds to react to changes in data and automatically execute actions on the incoming feeds of data. Actions can be programmed to process changes, transform data formats, send and receive messages, invoke other actions, update various data stores, including SQL based relational databases, in-memory data grids, NoSQL database, files, messaging brokers and variety of other systems. {{site.data.keyword.openwhisk_short}} rules and sequences provide flexibility to make changes in processing pipeline without programming - simply via configuration changes. This makes {{site.data.keyword.openwhisk_short}} based system highly agile and easily adaptable to changing requirements.

[OpenChecks](https://github.com/krook/openchecks) project is a proof of concept that shows how {{site.data.keyword.openwhisk_short}} can be used for processing the deposit of checks to a bank account using optical character recognition. It is currently built on the public Bluemix {{site.data.keyword.openwhisk_short}} service and relies on Cloudant and SoftLayer Object Storage. On premises, it could use CouchDB and OpenStack Swift. Other storage services could include FileNet or Cleversafe. Tesseract provides the OCR library.
## Cognitive
{: #openwhisk_common_use_cases_cognitive}

Cognitive technologies can be effectively combined with {{site.data.keyword.openwhisk_short}} to create powerful applications. For example, IBM Alchemy API and Watson Visual Recognition can be used with {{site.data.keyword.openwhisk_short}} to automatically extract useful information from videos without having to actually watch them. This can be simply a “cognitive” extension of the [Data Processing](#data-processing) use case discussed earlier. Another good use for {{site.data.keyword.openwhisk_short}} is to implement Bot function combined with cognitive services. 

Here is a sample application [Dark vision](https://github.com/IBM-Bluemix/openwhisk-darkvisionapp) that does just that. In this application the user uploads a video or image using the Dark Vision web application, which stores it in a Cloudant DB. Once the video is uploaded, {{site.data.keyword.openwhisk_short}} detects the new video by listening to Cloudant changes (trigger). {{site.data.keyword.openwhisk_short}} then triggers the video extractor action. During its execution, the extractor produces frames (images) and stores them in Cloudant. The frames are then processed using Watson Visual Recognition and the results are stored in the same Cloudant DB. The results can be viewed using Dark Vision web application OR an iOS application. Object Storage can be used in addition to Cloudant. When doing so, video and image metadata are stored in Cloudant and the media files are stored in Object Storage.

Here is an [example iOS Swift application](https://github.com/gconan/BluemixMobileServicesDemoApp) that shows {{site.data.keyword.openwhisk_short}}, IBM Mobile Analytics, Watson to analyze tone and post to a Slack channel.

## Event processing with Kafka or Message Hub 

{{site.data.keyword.openwhisk_short}} is very well suited to be used in combination with Kafka, IBM Message Hub service (Kafka based) and other messaging systems. The event driven nature of those systems requires event driven runtime to process messages and apply business logic to those messages, which is exactly what {{site.data.keyword.openwhisk_short}} provides with its feeds, triggers, actions, etc. Kafka and Message Hub are often used for very high and unpredictable volumes of workload and require that consumers of those messages need to be scalable on a moment's notice, which is again a sweet spot for {{site.data.keyword.openwhisk_short}}. {{site.data.keyword.openwhisk_short}} has built-in capability to consume messages as well as publish messages provided in the [openwhisk-package-kafka](https://github.com/openwhisk/openwhisk-package-kafka) package.

Here is an [example application that implements event processing scenario](https://github.com/IBM/openwhisk-data-processing-message-hub) with {{site.data.keyword.openwhisk_short}}, Message Hub and Kafka.
