# What does the Bluemix Logging service?

When you encounter errors in any stage from deployment to runtime, you can check the logs for clues that might help solve your issue.


Troubleshooting:
**Note:** Logs are not persisted between app crashes and deployments. When an app crashes and restarts the Instance ID is different.


----------------
When you define your organization's cloud operations management strategy, consider the logging and monitoring capabilities that a cloud platform like {{site.data.keyword.Bluemix}} offers you. {{site.data.keyword.Bluemix}} includes integrated logging and monitoring services across the platform.


You can use the {{site.data.keyword.Bluemix}} platform monitoring to:

* Collect and monitor performance information for app instances, and check whether they are functional.
* Gain insight on application operations, for example, detect the potential bottlenecks or when upgrades are required.
* Estimate resource usage and charges.
* Configure alerts and notifications that allow you to manage your cloud resources more efficiently.
* Define trends that you can use to plan future app requirements in your cloud platform.

---------------------
Monitoring the cloud environment is key to understanding how your applications are performing. You can use information provided by performance metrics to monitor how a service is running in the cloud, detect resource bottlenecks, and keep an eye on the service SLA. For example, when you analyze performance data for a service, you can detect situations that can lead to a resource bottleneck and consequently affect your service SLA to your clients. By taking early action, you can prevent situations that can impact your business negatively.  

Logging capabilities are key to understanding the behaviour of the cloud platform and you resources that are running in it. Logs provide information that you can use to provide an audit trail for an application, detect problems in your service, identify vulnerabilities, troubleshoot your app deployments and runtime behaviour, detect problems in the infrastructure where your app is running, trace your app across components in the cloud platform, and detect patterns that you can use to preempt actions that could affect your service SLA.

-----------------

Original

Cloud services use the logging and monitoring capabilities that are available in {{site.data.keyword.Bluemix}}.
You can integrate these services with your applications without the complexity of building and maintaining
the infrastructure that is typically associated with developing and launching new functionality as a custom service.



New:


Cloud services also leverage the logging and monitoring functionality that is available in Bluemix. They can send
logs and metrics by using crawlers.


we accept logs and metrics from other services through a series of service crawlers but we do not
have full compliance with bluemix services.  we do have a couple onboarded.

[2:22]  
so this paragraph
needs to explain how we do this and that we have some services doing this, but not "any" or "all" ye

----------------


With a platform-as-a-service (PaaS) things are much different, there is no way to SSH or FTP into the infrastructure running your app because that is all controlled by the platform.  In Cloud Foundry based PaaSes such as Bluemix, access to logs from an application are exposed via something called the Loggerator.  T

When you define your organization's cloud operations management strategy, you must consider the logging and monitoring capabilities that a cloud platform like {{site.data.keyword.Bluemix}} offers you. In a public or dedicated cloud environment, resources are provisioned on demand and hosted remotedly. Efficiency to monitor and analyze data

{{site.data.keyword.Bluemix}} includes functionality for monitoring usage of the cloud resources,  that would also alert them when they need additional resources and about applications for which these additional resources are needed. These monitoring capabilities include tools for monitoring CPU usage per computing resource, ratios between systems activity and user activity, and CPU usage from specific job tasks.

Also, organizations should have capabilities for predictive analytics that allow them to capture trending data on memory utilization and file system growth, so they can plan needed changes to computing resources before they encounter service availability issues. Not having these capabilities in place prevents organizations from taking timely actions for optimizing cloud resources in use to meet changes in business demand.

You need to plan for any auditing requirements, define operations to troubleshoot problems at the infrastructure levle, the runtime level or the application level, ability to trace across all components, ability to detect patterns that can help you preempt actions to meet your service SLAs towards your clients.


is where the ability to capture, visualize, analyze, and monitor resource performance data and logs for applications, runtimes, and infrastructure,  become of great importance. Visibility of your cloud environment, how your applications are performing,  

cloud monitoring platform enables IT organizations to really deliver the speed and service quality that users expect out of their cloud.
right-size capacity and optimize your monitoring and management processes.



{{site.data.keyword.Bluemix}} includes logging and monitoring functionality across the cloud platform.

Organizations using cloud computing services need to have visibility not only into the performance of applications that have moved to the cloud, but also into the different computing resources on which these applications depend. Typically, organizations find it easier to monitor the performance of applications that are hosted at a single server as opposed to the performance of composite applications that are pulling computing resources from different sources. This issue becomes even more complex if computing resources are hosted outside of corporate firewalls, and organizations do not have a full control and visibility into the performance of these applications.

finding a balance between scalability and flexibility of computing resources and ease of management and visibility into performance of the IT services relying on these resources.
it is important to have integrated logging and monitoring functionality with   cloud infrastructure resources, services, and applications. are core to have visibility of cloud resources and services
full control of the performance of cloud services in use.
Visibility of resources and services across the cloud environment
Performance of services that you as an organization are interested  (SLAs)
 ability to increase and decrease cloud resources used as the demand changes. In order to take a full advantage of this capability, organizations need to have full visibility into how their existing resources are being used in both internal and external environments.


Of course, log data can give us better insights into detecting patterns and allow us to take action more quickly when that information is presented in visualized form. This method of analysis allows IT operations teams to create the transparency that is needed to understand what is occurring at any given point in time.

Kibana and Grafana are two open source tools that can visualize and understand trends within vast amounts of log data.

Kibana is a platform for analytics and visualization that allows you to explore, visualize, and build dashboards on top of the log data stored in Elasticsearch clusters. You can perform advanced data analysis and visualize your data in a variety of types of charts, tables, and maps.



Inability to monitor performance of applications that use a hybrid cloud approach

Capabilities Needed Tools for measuring the impact of rules for assigning cloud resources on quality of end-user experience

One of the key benefits of cloud computing services is flexibility of assigning resources needed to support demand from business users. In order to achieve this benefit, many organizations deploying cloud computing services are defining rules for assigning cloud resources to each of their critical IT services and applications. However, the effectiveness of these policies depends on the visibility that organizations have into how cloud resources are being used. Organizations that have technology tools in place to monitor how changes in policies that control allocation of cloud computing resources impact the performance of business-critical applications, as measured from end-users' perspective, are more likely to reap the full benefits from the deployment of cloud computing.

Ability to compare cloud service delivery to performance of the internal environment

Organizations can garner the full benefits of cloud computing services only if they can ensure that the performance of these services as experienced by business users is at optimal level. The best way for organizations to evaluate the performance of these services is to compare them to the performance of those services hosted and managed internally.

Having technology capabilities that allow organizations to measure key performance indicators (KPI) for application performance in both cloud and internal environments allows organizations to define proper benchmarks for evaluating performance of cloud services and make better decisions about value received from making changes in their IT management strategies.

An independent tool for monitoring/validating performance of a heterogeneous set of applications in the cloud

As organizations deploying cloud computing services trust third-party providers to deliver quality of service that would be acceptable to the end-users, they need to have technology tools in place to enable them to keep their service providers "honest" and have capabilities for monitoring levels of SLA achievements that go beyond monitoring capabilities provided by cloud vendors. As a part of their agreements with providers of public cloud services, organizations are requesting guarantees for levels of performance that service providers are expected to deliver. However, in order to ensure that these service levels are met, organizations need to have independent monitoring tools in place that allow them to monitor not only actual levels of performance as experienced by business users, but also enable them to conduct root cause analysis of problems as they occur. These monitoring tools include capabilities for monitoring application response times, service availability, page load times, and ability monitor traffic during peak times.

For organizations that want to receive the full value of cloud computing services it is critical to be able to understand if any performance issues that they experience are caused by their cloud service providers, network issues, or the design of the application itself.

Ability to monitor cloud applications alongside with internal IT systems

The majority of organizations deploying cloud computing services are selecting the hybrid model, which means that they are moving some of their applications into the cloud while other applications are still being hosted on internally managed servers and delivered over the corporate network. That requires that these organizations have two different sets of capabilities, one for monitoring the performance of applications hosted outside of their corporate firewalls and one for those hosted in their data centers. It is hence important for the monitoring tool to support integrating data from possibly two restrictive networks which form part of the data center.

Having this capability in place allows organizations to ensure optimal levels of performance of business-critical applications regardless of hosting method and in the process make their IT Operations more productive.



Organizations that are using the right mix of technology solutions for monitoring the performance of applications in the cloud are more likely to enjoy the following business benefits:

    Prevention and resolution of performance issues in a timely manner. Organizations that have visibility into resource utilization in the cloud are more likely to make educated and timely decisions about resource allocation, and therefore, to prevent performance problems before they impact their business users
    Ability to support changes in business demand. Full visibility into the performance of cloud services allows organizations to unlock the benefits of cloud computing, especially when it comes to improved flexibility of IT management. Organizations that have end-to-end visibility into the performance of cloud services and their internal infrastructure are able to make better decisions about adding or subtracting resources to support changes in business demand, which allows them to ensure a high level of quality of end-user experience at optimal cost.
    Ability to optimize spending decisions. Organizations deploying independent tools for monitoring performance, SLA achievements, and usage of cloud services are more likely to be able to make educated decisions about the return they are getting from their investment in cloud services.







------------------



The best practice for logging of Bluemix java applications is to write the log to stdout and have loggregator drain the logs or use services like log Analysis for long term persistence. You can configure 3rd party services like Splunk or Papertrail to drain your logs from loggregator. see http://docs.cloudfoundry.org/devguide/services/log-management-thirdparty-svc.html see https://www.ng.bluemix.net/docs/#services/monana/index.html#gettingstartedtemplate
