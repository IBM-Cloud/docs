---

 

copyright:

  years: 2015, 2016

 

---

{:codeblock: .codeblock}
{:shortdesc: .shortdesc}
{:new_window: target="_blank"}

# Getting started with the {{site.data.keyword.autoscaling}} service
{: #autoscaling}

*Last updated: 30 May 2015*

In {{site.data.keyword.Bluemix_notm}}, you can automatically manage your application capacity. Use the  {{site.data.keyword.autoscalingfull}} service to automatically increase or decrease the compute capacity of your application. The number of application instances are adjusted dynamically based on the {{site.data.keyword.autoscaling}} policy that you define.
{:shortdesc} 

## Using the {{site.data.keyword.autoscaling}} service in {{site.data.keyword.Bluemix_notm}}
{: #as-service}

To use the {{site.data.keyword.autoscaling}} service, complete the following steps:

1. On {{site.data.keyword.Bluemix_notm}}  Dashboard, click *Add a service or API*, and then select the {{site.data.keyword.autoscaling}} service from the DevOps section in the service catalog. A new window is displayed to present an overview of the {{site.data.keyword.autoscaling}} service.
2. Select the application that you want to bind the {{site.data.keyword.autoscaling}} service to, and click *Create*. <br/>
*Remember:* You can bind only one {{site.data.keyword.autoscaling}} service to an application. If the application is already bound with another {{site.data.keyword.autoscaling}} service, do not select the application in this step. Otherwise, you will get the CWSCV2004E error.<br/>The Restage Application window is displayed.
3. In the Restage Application window, click *Restage* to restage your application before you use the new {{site.data.keyword.autoscaling}} service that you just added. After restaging application is completed, you can start to configure the {{site.data.keyword.autoscaling}} service for your application.
4. To configure the {{site.data.keyword.autoscaling}} for an application, in the {{site.data.keyword.Bluemix_notm}}  user interface, click your application that the {{site.data.keyword.autoscaling}} service is bound to.
5. In the services section on the Dashboard, click the *Auto-Scaling* icon.
6. If you have not done so, define the {{site.data.keyword.autoscaling}} policy for the application by clicking *Create {{site.data.keyword.autoscaling}} Policy*.

Now you can configure the {{site.data.keyword.autoscaling}} policy, see the metric statistics, or view the scaling history for the application.
<dl>
<dt>Policy Configuration</dt>
<dd>Use this section to create or edit the scaling rules to specify the conditions in which certain scaling activities are to be triggered.<ul>
<li> For Liberty for Java™ applications, you can define scaling rules for JVM Heap, Memory, and Throughput.
<li> For Node.js applications, you can define scaling rules for Memory.
<li> For Ruby applications, you can define scaling rules for Memory.</ul>
*Note:* You can define multiple scaling rules for more than one metric type. However, the {{site.data.keyword.autoscaling}} service does not detect conflicts between scaling policies. When you define the scaling policy, you must ensure that multiple scaling rules do not conflict with one another. Otherwise, you might see the total instance number fluctuates because the application scales in 1 minute and scales out the next.<br/><br/>
If the workload of your application changes dramatically during the peak time and the spare time, you can create a scaling schedule to handle the different scaling requirements for different time periods. Use the Minimum Instance Count parameter that is specified in a schedule to define the baseline of the application instance number, while dynamic scaling rules still apply to the schedule to trigger the scaling in and scaling out actions.</dd>
<dt>Metric Statistics</dt>
<dd>Displays the metric statistics for the instances of your application. You can see the average statistics and select specific instance to see its statistic.</dd>
<dt>Scaling History</dt>
<dd>Displays the scaling history of your applications.<ul>
<li> Past Week: Displays the scaling history for the past week.
<li> Past Month: Displays the scaling history for the past month.
<li> Custom Range: You can set the time period.</ul>
*Note:* You can filter the history record by selecting Scaling Status or Scaling In/Out.</dd>
</dl>


## Policy fields for the {{site.data.keyword.autoscaling}} service
{: #policyfields}

| Field name  | Description |
|-------------|----------------------|
|*Allowable maixmum instance count* |	The maximum number of the application instance that can be started. If the current number of the application instances equals this value, the {{site.data.keyword.autoscaling}} service does not scale out the application any more. Default minimum instance count	The minimum number of the application instance that can be started. If the number of the instances equals this value, the {{site.data.keyword.autoscaling}} service dose not scale in the application any more. |
| *Metric Type*	| 	The supported metric types that can be monitored. For more information, see Table 2. |
| *Scale Out* | 	Specifies the threshold that triggers a scaling out action and how many instances are increased when the scaling out action is triggered. |
| *Scale In* |	Specifies a threshold that triggers a scaling in action and how many instances are decreased when the scaling in action is triggered. |
| *Statistic Window* |	The length of the past period when received metric values are recognized as valid. Metric values are valid only if the time stamps fall within this period. The unit of the Statistic Window parameter is second. |
| *Breach Duration*	| The length of the past period when a scaling action might be triggered. A scaling action is triggered when collected metric values are either above the upper threshold, or below the lower threshold longer than the time specified. The unit of the Breach Duration parameter is second. |
| *Cooldown period for scaling in* | After a scaling in action occurs, other scaling requests are ignored during the length of the period that is specified by the Cooldown period for scaling in parameter. The unit of this parameter is second. |
| *Cooldown period for scaling out*	| After a scaling out action occurs, other scaling requests are ignored during the length of the period that is specified by the Cooldown period for scaling out parameter. The unit of this parameter is second. |
| *Time Zone*	| The time zone where the schedule applies. |
| *Start Time*  |	The start time of a recurring schedule. |
| *End Time*    |	The end time of a recurring schedule.	|
| *Repeat On*	|	The day in a week when a recurring schedule applies. |
| *Minimum Instance Count* |	The minimum number of instances that can be started for the application during the specified time period in the schedule. |
| *Start Date&Time* |	The start date and time of the schedule set up on a specific date. |
| *End Date&Time* |	The end date and time of the schedule set up on a specific date.	|

Table 1. Policy fields in the scaling policy

| Metric name | Description | Supported application type |
|-------------|----------------------| ------------------- |
| *JVM heap* |	The usage percentage of the JVM heap memory.	| Liberty for Java |
| *Memory*   |	The usage percentage of the memory.	|  All |
| *Throughput* | The number of the processed requests per second.| Liberty for Java |
| *Response time* |	The response time of the processed requests.	| Liberty for Java |

Table 2. Supported metric names

*Note:* To collect Auto-Scaling metrics data, your application must be deployed as Liberty webapp so that measuring HTTP/HTTPS requests will be processed via Liberty web container.
For example, if you run a Spring Boot application as a "Main-Classs" app, the Liberty buildpack only provides java environment for you, and the app actually runs in the Spring embedded Tomcat container, thus no metrics data will be collected by the Auto-Scaling service. You must run your app as a Liberty WAR in order to work with Auto-Scaling service.


## Error messages
{: #errmsgs}
This section lists the warning and error messages that are produced by the {{site.data.keyword.autoscaling}} service.
 
### CWSCV2004E Another {{site.data.keyword.autoscaling}} service is already bound to application.
**You can bind only one {{site.data.keyword.autoscaling}} service to one application. This error occurs when you want to bind the {{site.data.keyword.autoscaling}} service to an application that is already bound with another {{site.data.keyword.autoscaling}} service.**

Select another application without any other {{site.data.keyword.autoscaling}} service bound to and bind the target {{site.data.keyword.autoscaling}} service to this application.
If you encounter this error in all the other cases, contact IBM Support.

### CWSCV6001E The API server cannot parse the input JSON strings for API: {0}.
**Problem occurs when parsing input JSON strings.**

Check the Input JSON with API document and correct the error in it.

### CWSCV6002E The API server cannot parse the output JSON strings for API: {0}.
**Problem occurs when parsing input JSON strings.**

Contact the Cloud Administrator for more information.

### CWSCV6003E Input JSON strings format error: {0} in the input JSON for API: {1}.
**Format error found when parsing input JSON strings.**

Check the Input JSON with API document and correct the error in it.

### CWSCV6004E Output JSON strings format error: {0} in the output JSON for API: {1}.
**Format error found when parsing output JSON strings.**

Contact the Cloud Administrator for more information.

### CWSCV6005E Internal server error happened during {0}.
**Internal server error occurs when processing the request.**

Contact the Cloud Administrator for more information.

### CWSCV6006E Calling CloudFoundry APIs failed: {0}
**Error occurred when calling CloudFoundry APIs.**

Contact the Cloud Administrator for more information.

### CWSCV6007E The application is not found: {0}
**The application is not found.**

Check application information for more information.

### CWSCV6008E Following error occurred when retrieving information for application {0}: {1}
**Retrieving application information failed with certain errors.**

Check application information for more information.

### CWSCV6009E Service: {0} for App {1} is not found.
**The service for this application cannot be found.**

Check service binding for this application for more information.

### CWSCV6010E Policy for App {0} is not found
**The policy for this application cannot be found.**

Check application configuration for more information.

### CWSCV6011E Internal Authentication failed during {0}
**Internal Authentication failed.**

Contact the Cloud Administrator for more information.

# rellinks
{: #rellinks}

## samples
{: #samples}

* [Tutorial: Make your application elastic on {{site.data.keyword.Bluemix_notm}}](http://www.ibm.com/developerworks/cloud/library/cl-autoscale-app/index.html){:new_window}
* [Cloud Foundry Architecture Labs](https://developer.ibm.com/bluemix/docs/category/cloud-foundry-docs/){:new_window}

## sdk
{: #sdk}

* [Rest API of IBM {{site.data.keyword.autoscaling}} for {{site.data.keyword.Bluemix_notm}}](https://new-console.{DomainName}/apidocs/48){:new_window}

## general
{: #general}

* [Scaling containers](https://www.{DomainName}/docs/containers/container_creating_ov.html#container_group_ov){:new_window}
* [Scaling virtual servers](https://www.{DomainName}/docs/virtualmachines/vm_index.html#vm_manage_instances){:new_window}
* [{{site.data.keyword.autoscaling}} CLI](../../cli/plugins/auto-scaling/index.html){:new_window}