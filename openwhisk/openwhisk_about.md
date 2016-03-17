---

 

copyright:

  years: 2016

 

---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}
{:screen: .screen}
{:pre: .pre}

# About {{site.data.keyword.openwhisk}}

*Last updated: 22 February 2016*

The following sections provide details about {{site.data.keyword.openwhisk}}.
{: shortdesc}

## How {{site.data.keyword.openwhisk_short}} works
{: #openwhisk_how}

{{site.data.keyword.openwhisk_short}} is an event-driven compute platform that executes code in response to events or direct invocations.

The following figure shows the high-level {{site.data.keyword.openwhisk_short}} architecture.

![{{site.data.keyword.openwhisk_short}} architecture](OpenWhisk.png)

Examples of events include changes to database records, IoT sensor readings that exceed a certain temperature, new code commits to a GitHub repository, or simple HTTP requests from web or mobile apps. Events from external and internal event sources are channeled through a trigger, and rules allow actions to react to these events.

Actions can be small snippets of Javascript or Swift code, or custom binaries embedded in a Docker container. Actions in {{site.data.keyword.openwhisk_short}} are instantly deployed and executed whenever a trigger fires. The more triggers fire, the more actions get invoked. If no trigger fires, no action code is running, so there is no cost.

In addition to associating actions with triggers, it is possible to directly invoke an action by using the {{site.data.keyword.openwhisk_short}} API, CLI, or iOS SDK. A set of actions can also be chained without having to write any code. Each action in the chain is invoked in sequence with the output of one action passed as input to the next in the sequence.

With traditional long-running virtual machines or containers, it is common practice to deploy multiple VMs or containers to be resilient against outages of a single instance. However, {{site.data.keyword.openwhisk_short}} offers an alternative model with no resiliency-related cost overhead. The on-demand execution of actions provides inherent scalability and optimal utilization as the number of running actions always matches the trigger rate. Additionally, the developer now only focuses on his code and does not worry about monitoring, patching, and securing the underlying server, storage, network, and operating system infrastructure.

Integrations with additional services and event providers can be added with packages. A package is a bundle of feeds and actions. A feed is a piece of code that configures an external event source to fire trigger events. For example, a trigger created with a Cloudant change feed will configure a service to fire the trigger every time a document is modified or added to a Cloudant database. Actions in packages represent reusable logic that a service provider can make available so that developers can not only use the service as an event source, but also invoke APIs of that service.

An existing catalog of packages offers a quick way to enhance applications with useful capabilities, and to access external services in the ecosystem. Examples of external services that are {{site.data.keyword.openwhisk_short}}-enabled include Cloudant, The Weather Company, Slack, and GitHub.


## Common use cases
{: #openwhisk_use_cases}

The execution model offered by {{site.data.keyword.openwhisk_short}} supports a variety of use cases. The following sections include typical examples.

### Decomposition of applications into microservices
The modular and inherently scalable nature of {{site.data.keyword.openwhisk_short}} makes it suitable for implementing granular pieces of logic in actions. For example, {{site.data.keyword.openwhisk_short}} can be useful for removing load-intensive, potentially spiky (background) tasks from front-end code and implementing these tasks as actions.

### Mobile back end
Many mobile applications require server-side logic. Given that mobile developers usually don’t have experience in managing server-side logic and would rather focus on the app running on the device, using {{site.data.keyword.openwhisk_short}} as the server-side back end is a good solution. In addition, the built-in support for Swift allows developers to reuse their existing iOS programming skills.

### Data processing
With the amount of data now available, application development requires the ability to process new data, and potentially react to it. This requirement includes processing both structured database records as well as unstructured documents, images, or videos.

### IoT
Internet of Things scenarios are often inherently sensor-driven. For example, an action in {{site.data.keyword.openwhisk_short}} could be triggered if there is a need to react to a sensor exceeding a particular temperature.



