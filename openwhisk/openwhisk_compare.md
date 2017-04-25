---

copyright:
  years: 2016, 2017
lastupdated: 2017-03-16

---

{:shortdesc: .shortdesc}
{:codeblock: .codeblock}
{:screen: .screen}
{:pre: .pre}

# Function as a Service compared
{: #openwhisk_faas_compared}

Serverless architecture is not a panacea to all computing problems, but it does solve some. There are [many uses cases](./openwhisk_use_cases.html) when serverless design may be a good choice. Here we will compare the following architectures:

1. **Function as a Service (FaaS)** - managed OpenWhisk. Currently IBM is the only vendor offering managed [OpenWhisk on Bluemix](https://console.ng.bluemix.net/openwhisk).

2. **Infrastructure as a Service (IaaS)** with OpenWhisk Roll Your Own (RYO). End users can download OpenWhisk from Apache Incubation Project and install and run it on [Bluemix IaaS](https://console.ng.bluemix.net/catalog/?category=devices), or other [IaaS cloud](https://en.wikipedia.org/wiki/Cloud_computing#Infrastructure_as_a_service_.28IaaS.29).

3. **Platform as a Service (PaaS)** - managed application runtime. A good example is [Liberty for Java](https://console.ng.bluemix.net/catalog/starters/liberty-for-java) runtime managed by IBM Bluemix CloudFoundry implementation.

4. **Container as a Service (CaaS)** - managed container environment. A good example is IBM’s [Containers on Bluemix](https://console.ng.bluemix.net/catalog/?category=containerImages).

5. **Infrastructure as a Service (IaaS)** with Java EE runtime. A good example is [WebSphere Application Server VM on Bluemix](https://console.ng.bluemix.net/catalog/services/websphere-application-server) from IBM.

Here is a summary of pros and cons of each architecture choice from the **perspective of an end user** who is developing and operating applications on these different runtimes:


| Topic | (1) OpenWhisk FaaS | (2) OpenWhisk RYO | (3) PaaS | (4) CaaS | (5) IaaS+Java EE |
| --- | --- | --- | --- | --- | --- |
|	Application unit	|	Single function (usually small block of code in JavaScript, Swift or Docker container) - can be less than 1 Kb, but may be larger. Usually not more than few Kb.	|	Same as column (1)	|	Depending on the runtime used - could be an EAR or WAR file or other language specific application bundle, usually relatively large in size - Kb or even Mb with many services in a bundle, but can be as small as a single service	|	Docker container is the unit of deployment.	|	VM with App Server with EAR or WAR file and other dependencies - usually sized at Gb.	|
|	Resource footprint	|	End user does not pay or care about memory, CPU or other resources. While the action does have some footprint the user does not need to worry about it	|	High. The end user must first provision IaaS environment and only then install and configure OpenWhisk on top of it	|	Small. End user pays for memory and CPU for running apps, but nothing for apps that are not running	|	Small to Medium	|	High. End user has to pay for disk storage, memory, CPUs and possibly other components when the app is running. When it is stopped only the storage costs occur	|
|	Installation and setup	|	None required	|	Hard - all done by the end user	|	None required	|	Moderate - hw, networking, OS, container mgmt tools provided by CaaSs vendor, images, connectivity and instances by end user	|	Hard - hw, networking, OS, initial Java EE install provided by vendor, additional configuration, clustering, scaling by end user	|
|	Provisioning time	|	Milliseconds	|	See columns (4) and (5)	|	Minutes	|	Minutes	|	Hours	|
|	Ongoing administration	|	None	|	Hard	|	None	|	Moderate	|	Hard	|
|	Elastic scaling	|	Each action is always instantly and inherently scaled depending on the load. There is no need to provision VMs or other resources in advance	|	Not provided - end user must provide compute capacity on IaaS and manage scaling of VMs. Once VMs are scaled, the OpenWhisk will scale action automatically, but the resources must already be provisioned in advance	|	Automatic, but slow scaling. At the start of a peak for several minutes users may be waiting for scale action to complete. Auto scaling requires careful tuning	|	Automatic, but slow scaling. At the start of a peak for several minutes users may be waiting for scale action to complete. Auto scaling requires careful tuning	|	Not provided	|
|	Capacity planning	|	Not needed. FaaS will automatically provide as much capacity as needed	|	Need to provision enough capacity in advance or script it	|	Some capacity planning is needed, but some automatic capacity increase is provided	|	Some capacity planning is needed, but some automatic capacity increase is provided	|	Need to statically provision enough capacity to handle †for peak workload	|
|	Persistent connections and state	|	Very limited - can not keep a persistent connection, except in cases of container caching. Generally state must be kept in external resource	|	Same as column (1)	|	Supported - can keep an open socket or connection for long times, can store state in memory between calls	|	Supported - can keep an open socket or connection for long times, can store state in memory between calls	|	Supported - can keep an open socket or connection for long times, can store state in memory between calls	|
|	Maintenance	|	Not required - entire stack is managed by IBM	|	Significant - depending on the target environment, user must provision hw, networking, OS, storage, DB, install and maintain OpenWhisk, etc.	|	Not required - entire stack is managed by vendor	|	Significant - user must create and maintain custom †images, deploy and manage containers, connections between containers, etc.	|	Significant - user must allocate VMs, manage and scale Java EE servers individually	|
|	High Availability (HA) and Disaster Recovery (DR)	|	Inherent / no extra costs	|	Roll your own (RYO) 	|	Available at extra cost	|	Failed containers can be automatically restarted	|	Available at extra cost, semi-automatic. VMs can be automatically failed over	|
|	Security	|	Vendor provided	|	Roll your own (RYO)	|	Mix of RYO and vendor provided	|	Mix of RYO and vendor provided	|	Roll your own (RYO)	|
|	Developer velocity	|	Highest	|	Highest	|	Highest	|	Average	|	Slow	|
|	Resource utilization (idle resources that still needs to be paid for)	|	Resources are never ìidleî as they are invoked only when there is a request. When there is no workload, there is no resource allocation and no cost	|	Because this option is using IaaS or CaaS - similar considerations apply as in columns (4) and (5)	|	Some resources may be idle. Auto Scaling up and down helps to eliminate idle resources, but some number of running instances must always be present and these are likely to be used at less than 50% of their capacity. Stopped instances do not cost anything	|	Similar to column (3)	|	Some resources may be idle. Autoscaling is not supported. Some number of running instances must always be present and these are likely to be used at less than 50% of their capacity. Stopped instances may incur the cost of storage	|
|	Maturity	|	Early maturity	|	Early maturity	|	Early maturity	|	Moderate maturity	|	Very mature	|
|	Resource limits	|	[Some limits exist](./openwhisk_reference.html#openwhisk_syslimits)	|	Depends on allocated resources	|	No	|	No	|	No	|
|	Latency for rarely used services	|	Rare requests may initially see several seconds response time, but will be in ms range for subsequent requests	|	Depends	|	Very low	|	Very low	|	Very low - assuming the system has enough resources	|
|	Sweet spot type of application	|	Event processing, IoT, Mobile backend, microservices. Definitely not for monolithic applications. See [use cases](./openwhisk_use_cases.html)	|	Same as column (1), but when user wants to run on non-IBM cloud or run on-prem.	|	Web applications with 24x7 workload load, stateful services that need to keep the connection open for long periods of time. Can be used to run microservices or monolithic applications	|	Well suited for microservices applications.	|	Traditional enterprise applications migrated from on-prem to the cloud. Better suited for monolithic applications	|
|	Charging granularity and billing	|	[Per blocks of 100 milliseconds](https://console.ng.bluemix.net/openwhisk/learn/pricing)	|	Depending on implementation - if this is using IaaS or CaaS, then similar considerations apply - see columns (4) and (5)	|	Usually charged per hour (rarely per minute) for bundle of resources (CPU + memory + some disk space)	|	Similar to column (3)	|	Similar to column (3)	|
|	Total Cost of Ownership (TCO)	|	For its ìsweet spotî applications is likely to cost order of magnitude less than alternatives. Because resources are auto scaled, there is never an issue of over provisioning	|	For cloud deployments this is likely to be more expensive than OpenWhisk FaaS, but for on-prem deployment can be cheaper than traditional architectures	|	Relatively low - the user does not need to provision or manage resources and only needs to worry his application, but there is some level of overprovisioning compared to serverless	|	Moderate - the user needs to provision and manage containers and application, but there is some level of over provisioning compared to serverless and compared to PaaS	|	Relatively high, but considering that migration of legacy applications into cloud native model could be prohibitively expensive, this may be a viable and economical choice for those apps	|
