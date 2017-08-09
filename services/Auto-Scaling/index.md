---

 

copyright:

  years: 2015，2017
lastupdated: "2017-08-09"  
 

---

{:codeblock: .codeblock}
{:shortdesc: .shortdesc}
{:new_window: target="_blank"}

# Getting started with the {{site.data.keyword.autoscaling}} service
{: #autoscaling}


In {{site.data.keyword.Bluemix_notm}}, you can automatically manage your application capacity. Use the {{site.data.keyword.autoscaling}} service to automatically increase or decrease the compute capacity of your application. The number of application instances are adjusted dynamically based on the {{site.data.keyword.autoscaling}} policy that you define.
{:shortdesc} 

## Contents
  * [Using the {{site.data.keyword.autoscaling}} service in {{site.data.keyword.Bluemix_notm}}](#as-service)
  * [Configuring Node.js apps with the {{site.data.keyword.autoscaling}} service](#node-asagent)
  * [Configuring Swift apps with the {{site.data.keyword.autoscaling}} service](#swift-asagent)
  * [Manage {{site.data.keyword.autoscaling}} service through RESTful API](#RESTAPI)
  * [Manage {{site.data.keyword.autoscaling}} service through {{site.data.keyword.autoscaling}} CLI](#CLI)
  * [Policy fields for the {{site.data.keyword.autoscaling}} service](#policy_fields)
  * [Supported metric type for the {{site.data.keyword.autoscaling}} service](#metric_types)
  * [Error messages](#err_msg)

## Using the {{site.data.keyword.autoscaling}} service in {{site.data.keyword.Bluemix_notm}}
{: #as-service}

To use the {{site.data.keyword.autoscaling}} service, complete the following steps:

1. On {{site.data.keyword.Bluemix_notm}} Dashboard, click *Add a service or API*, and then select the {{site.data.keyword.autoscaling}} service from the `DevOps` section in the service catalog. A new window is displayed to present an overview of the {{site.data.keyword.autoscaling}} service.
2. Select the application that you want to bind the {{site.data.keyword.autoscaling}} service to, and click *Create*.  Then the Restage Application window is displayed.<br/>
*Note:*  
You can bind **only ONE** {{site.data.keyword.autoscaling}} service to an application. If the application is already bound with another {{site.data.keyword.autoscaling}} service, do not select the application in this step. Otherwise, you will get the CWSCV2004E error.
3. In the Restage Application window, click *Restage* to restage your application before you use the new {{site.data.keyword.autoscaling}} service that you just added. <br/><ul><li> For Liberty application, the {{site.data.keyword.autoscaling}} is auto-configured and ready for use after the application restage.</li> <li>For Node.js or Swift applications, you must update your application code to enable the {{site.data.keyword.autoscaling}} service before pushing the application to {{site.data.keyword.Bluemix_notm}}. Refer to <ul><li> [Configuring Node.js apps with the {{site.data.keyword.autoscaling}} service](index.html#node-asagent) </li> <li>[Configuring Swift apps with the {{site.data.keyword.autoscaling}} service](index.html#swift-asagent)</li></ul></ul> 
After restaging application is completed, you can start to configure the {{site.data.keyword.autoscaling}} service for your application.
4. To configure the {{site.data.keyword.autoscaling}} for an application, in the {{site.data.keyword.Bluemix_notm}} user interface, click your application that the {{site.data.keyword.autoscaling}} service is bound to.
5. In the services section on the Dashboard, click the *Auto-Scaling* icon.
6. If you have not done so, define the {{site.data.keyword.autoscaling}} policy for the application by clicking *Create {{site.data.keyword.autoscaling}} Policy*.

Now you can configure the {{site.data.keyword.autoscaling}} policy, see the metric statistics, or view the scaling history for the application.
<dl>
<dt>Policy Configuration</dt>
<dd>
Use this section to create or edit the scaling rules to specify the conditions in which certain scaling activities are to be triggered.
<ul>
<li> For Liberty for Java™ applications, you can define scaling rules for Heap, Memory, Response Time, and Throughput.
<li> For Node.js applications, you can define scaling rules for Heap, Memory, and Throughput.
<li> For Swift applications, you can define scaling rules for Memory, Throughput and Response Time.
<li> For Other applications, you can define scaling rules for Memory.
<br/> *Note:* You can define multiple scaling rules for more than one metric type. However, the {{site.data.keyword.autoscaling}} service does not detect conflicts between scaling policies. When you define the scaling policy, you must ensure that multiple scaling rules do not conflict with one another. Otherwise, you might see the total instance number fluctuates because the application scales in 1 minute and scales out the next.
</ul>

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


## Configuring Node.js apps with the {{site.data.keyword.autoscaling}} service
{: #node-asagent}

To enable the {{site.data.keyword.autoscaling}} service with your Node.js apps, besides service provision and binding steps, you need to complete the following steps as well before pushing the app to {{site.data.keyword.Bluemix_notm}}.
1. Enable `blumix-autoscaling-agent` in your application.
  + Update the package.json to create a dependency entry for *blumix-autoscaling-agent*. For example:<br/> 
  `"dependencies": {
    "bluemix-autoscaling-agent": "*"
  }`
2. Start *blumix-autoscaling-agent* with your application.
There are two ways to start the agent. Either works. 
  + The first way is to update the package.json file by adding `"start": "node -r bluemix-autoscaling-agent  app.js"` to *script* section. For example:<br/>
  ```
  "scripts": {
    "start": "node -r bluemix-autoscaling-agent app.js"
  }
  ```
  + The second way is to update your main file to add the agent declaration `var as_agent = require('bluemix-autoscaling-agent');` <br/>
  *Note:* `bluemix-autoscaling-agent` must be initialized prior to the npm modules you want to monitor, so you must call `require('bluemix-autoscaling-agent');` **prior to** the other `require` statements. <br/>
  The following code snippet shows a complete entry js file with the auto-scaling agent declaration.<br/> 
  ```
  var agent = require('bluemix-autoscaling-agent');
  var http = require('http');
  var server = http.createServer(function handler(req, res) {
    console.log("Hello!");
    
    }).listen(process.env.PORT || 3000);
  console.log('App is listening on port 3000');
  ```

3. (Optional) Set heap limit if you want to trigger scaling based on heap usage. Update package.json to define `max-old-space-size` based on the memory that you allocate for your app. <br/> For example: 
  `
  "scripts": {
    "start": "node --max-old-space-size=600 app.js"
  }
  `
<br/> If the value is not set when you start your application, the default Node.js heap limit 1.4GB is used as the maximum heap size regardless how much memory your app is allocated, which might lead to improper auto-scaling decisions.<br/>

A full sample of package.json:
  ```
  {
    "name": "Your-App",
    "version": "0.0.1",
    "description": "A sample nodejs app for Bluemix",
    "scripts": {
      "start": "node -r bluemix-autoscaling-agent --max-old-space-size=600 app.js"
    },
    "dependencies": {
      "bluemix-autoscaling-agent": "*"
    },
    "repository": {},
    "engines": {
      "node": "0.12.x"
    } 
  }
  ``` 

## Configuring Swift apps with the {{site.data.keyword.autoscaling}} service
{: #swift-asagent}

To enable the {{site.data.keyword.autoscaling}} service with your Swift apps, besides service provision and binding steps, you need to complete the following steps as well before pushing the app to {{site.data.keyword.Bluemix_notm}}.

1. Update Package.swift file to add dependency declaration of package SwiftMetrics: 
   ```
   Package(url: "https://github.com/RuntimeTools/SwiftMetrics.git" , majorVersion: 1)
   ```
   A sample Package.swift file is as below: 
```
import PackageDescription
let package = Package(
    name: "Your-App",
    targets: [
      Target(name: "Your-App", dependencies: [])
    ],
    dependencies: [
      .Package(url: "https://github.com/RuntimeTools/SwiftMetrics.git" , majorVersion: 1)
    ]) 
```
2. Add the SwiftMetrics modules to your Swift app. 
 + Import the packages.
```   
import SwiftMetrics
import SwiftMetricsKitura
import SwiftMetricsBluemix
```
 + Initialize and start the agent: 
    +  Declare variables of the SwiftMetrics and SwiftMonitor in your app.
      ```   
      let sm: SwiftMetrics
      let monitor: SwiftMonitor
      ```
    +  Create instances of the SwiftMetrics and SwiftMonitor classes in your app.
      ```   
      sm = try SwiftMetrics()
      _ = SwiftMetricsKitura(swiftMetricsInstance: sm)
      _ = SwiftMetricsBluemix(swiftMetricsInstance: sm)
      monitor = sm.monitor()
      ```
    +  A sample of a Swift app that uses SwiftMetrics and Kitura is shown below:
      ```
      import Configuration
      import CloudFoundryConfig
      import Kitura
      import SwiftyJSON
      import Dispatch
      import LoggerAPI
      import CloudFoundryEnv
      import SwiftMetrics
      import SwiftMetricsKitura
      import SwiftMetricsBluemix
      import Foundation
      public class Controller {
          let router: Router
          let configMgr: ConfigurationManager
          var jsonEndpointEnabled: Bool = true
          var jsonEndpointDelay: UInt32 = 0

          // Declare variables of the SwiftMetrics and SwiftMonitor in your app
          let sm: SwiftMetrics
          let monitor: SwiftMonitor

          var port: Int {
              get { return configMgr.port }
          }
          var url: String {
              get { return configMgr.url }
          }
          init() throws {
              configMgr = ConfigurationManager().load(.environmentVariables)

              //Create instances of the SwiftMetrics and SwiftMonitor classes in your app
              sm = try SwiftMetrics()
              _ = SwiftMetricsKitura(swiftMetricsInstance: sm)
              _ = SwiftMetricsBluemix(swiftMetricsInstance: sm)
              monitor = sm.monitor()

              // All web apps need a Router instance to define routes
              router = Router()
              // Serve static content from "public"
              router.all("/", middleware: StaticFileServer())
              // Basic GET request
              router.get("/hello", handler: getHello)
          }
          
          public func getHello(request: RouterRequest, response: RouterResponse, next: @escaping () -> Void) throws {
              Log.debug("GET - /hello route handler...")
              response.headers["Content-Type"] = "text/plain; charset=utf-8"
              try response.status(.OK).send("Hello from Kitura-Starter!").end()
          }

      }
      ```

*Note:* Currently only Swift application using Kitura framework is supported to use {{site.data.keyword.autoscaling}} service.

## Manage {{site.data.keyword.autoscaling}} service through RESTful API 
{: #RESTAPI}

{{site.data.keyword.autoscaling}} RESTful API provides an alternative way to manage {{site.data.keyword.autoscaling}} service beside the Bluemix UI, and it also supports the scaling data retrieval and analysis. It provides similar functionalities, such as Creating a Policy and Getting the Scaling History, as in the {{site.data.keyword.Bluemix_notm}} UI with API .

Before using the {{site.data.keyword.autoscaling}} RESTful API to manage the {{site.data.keyword.autoscaling}} service, please complete below prerequisites with this guide:
* Bind the {{site.data.keyword.autoscaling}} service with your application as described in previous section.
* Acquire the `AccessToken`
<br/>The user must provide a valid `AccessToken` obtained through CloudFoundry UAA procedure when invoke {{site.data.keyword.autoscaling}} service RESTful API. After a successful login with command line, the `AccessToken` can be obtained by either approach:
  <ul>
    <li> Command `cf oauth-token`</li>
  <li>Grab the `AccessToken` field from file `~/.cf/config.json` </li>
    </ul>
   *Note:*  The `AccessToken` may expired after a period. If you get a 401 Unauthorized response for REST API request again, you need to repeat above steps to refresh `AccessToken`. 
  
* Get endpoint of {{site.data.keyword.autoscaling}} API server <br/>

You can obtain the endpoint of {{site.data.keyword.autoscaling}} API server by checking the environment variable of `VCAP_SERVICE`  -> {{site.data.keyword.autoscaling}} service  ->  `api_url` 
```
   > cf env "Your-App"
   Getting env variables for app Your-App in org Your-Org / space Your-Space as ...
   OK

   System-Provided:
   {
     "VCAP_SERVICES": {
     "Auto-Scaling": [
     {
      "credentials": {
       "agentPassword": "....",
       "agentUsername": "agent",
       "api_url": "https://ScalingAPI.ng.bluemix.net",
       "app_id": "aa8d19b6-eceb-4b6e-b034-926a87e98a51",
       "service_id": "8f482f78-58d8-493c-829b-635e4cbfd817",
       "url": "https://Scaling.ng.bluemix.net"
      },
    ...
     }
   ...
```  

* Get the `app_id` of the application that you want to scale in or out with 
 the `cf app APPNAME --guid` command:
```
   > cf app Your-App --guid
   aa8d19b6-eceb-4b6e-b034-926a87e98a51
```
{{site.data.keyword.autoscaling}} service RESTful API document explain the details API definition:  [Rest API of IBM {{site.data.keyword.autoscaling}} for {{site.data.keyword.Bluemix_notm}}](https://new-console.stage1.ng.bluemix.net/apidocs/48){:new_window}.

A sample script to invoke {{site.data.keyword.autoscaling}} service RESTful API with *curl*:
```
cf login -a http://api.ng.bluemix.net -u Your-UserName -p Your-Password --skip-ssl-validation

accessToken=$(cf oauth-token)
API_url=$(cf env Your-App | grep "api_url" | awk '{print $2}' | sed -e "s/[\",]//g")
appId=$(cf app Your-App --guid)
policyJson="./policy.json"

echo "Create scaling policy using API :"
createPolicyUrl="${API_url}/v1/autoscaler/apps/${appId}/policy"
    
curl $createPolicyUrl -X 'PUT' -H 'Content-Type:application/json' -H 'Accept:application/json'  -H "Authorization:$accessToken" --data-binary @${policyJson} 
```

## Manage {{site.data.keyword.autoscaling}} service through {{site.data.keyword.autoscaling}} CLI 
{: #CLI}

The {{site.data.keyword.autoscaling}} CLI provides similar functionality as {{site.data.keyword.autoscaling}} RESTful API but in a more friendly way to configure {{site.data.keyword.autoscaling}} service. <br/>
For more details about how to install and use {{site.data.keyword.autoscaling}} CLI, see [{{site.data.keyword.autoscaling}} CLI](../../cli/plugins/auto-scaling/index.html){:new_window}

## Policy fields for the {{site.data.keyword.autoscaling}} service
{: #policy_fields}

| Field name  | Description |
|-------------|----------------------|
|*Minimum Instance Count* |  The minimum number of instances that can be started. If the number of the instances equals this value, the {{site.data.keyword.autoscaling}} service dose not scale in the application any more. |
|*Maximum instance count* | The maximum number of the application instance that can be started. If the current number of the application instances equals this value, the {{site.data.keyword.autoscaling}} service does not scale out the application any more. |
| *Metric Type* |   The supported metric types that can be monitored. For more information, see Table 2. |
| *Scale Out* |   Specifies the threshold that triggers a scaling out action and how many instances are increased when the scaling out action is triggered. |
| *Scale In* |  Specifies a threshold that triggers a scaling in action and how many instances are decreased when the scaling in action is triggered. |
| *Statistic Window* |  The length of the past period when received metric values are recognized as valid. Metric values are valid only if the time stamps fall within this period. The unit of the Statistic Window parameter is second. |
| *Breach Duration* | The length of the past period when a scaling action might be triggered. A scaling action is triggered when collected metric values are either above the upper threshold, or below the lower threshold longer than the time specified. The unit of the Breach Duration parameter is second. |
| *Cooldown period for scaling in* | After a scaling in action occurs, other scaling requests are ignored during the length of the period that is specified by the Cooldown period for scaling in parameter. The unit of this parameter is second. |
| *Cooldown period for scaling out* | After a scaling out action occurs, other scaling requests are ignored during the length of the period that is specified by the Cooldown period for scaling out parameter. The unit of this parameter is second. |
| *Time Zone* | The time zone where the schedule applies. |
| *Start Time*  | The start time of a recurring schedule. |
| *End Time*    | The end time of a recurring schedule. |
| *Repeat On* | The day in a week when a recurring schedule applies. |
| *Start Date&Time* | The start date and time of the schedule set up on a specific date. |
| *End Date&Time* | The end date and time of the schedule set up on a specific date.  |

{: caption="Table 1. Policy fields in the scaling policy" caption-side="top"}

## Supported metric type for the {{site.data.keyword.autoscaling}} service
{: #metric_types}
<br/>{{site.data.keyword.autoscaling}} service collects the runtime metrics for a Cloud Foundry application from the following data sources: 
* "Memory" metric collected from Cloud Foundry:  <br>
Cloud Foudry computes the memory usage from the "memory.stat" of cgroup with the formula below: <br>
`memory_usge = total_rss + total_cache - total_inactive_file`
   * total_cache:  memory used for page chache
   * total_rss:    memory resident in main memory (RAM)
   * total_inactive_file:  file-backed memory on inactive LRU list

* Metrics collected by Auto-Scaling data collector: <br/>
  * "Memory" metric:   
  {{site.data.keyword.autoscaling}} data collector grabs container memory usage with the [rss](https://en.wikipedia.org/wiki/Resident_set_size) value in file */proc/{pid}/stat*: <br/> 
  `memory_usage = RSS (total memory actually held in RAM for a process)`
  * "Heap" metric:
    * Lierty Java Runtime: Heap size that is used for current JVM.
    * Node.js : Heap size that is used for current V8 runtime.
  * "Response time" metric :  
  Aggregated the total elapsed time of all processed requests occurred in a specific window (aka *report interval*) , and take the average value as `response time`. 
  * "Throughput" metric:  
  The number of the processed requests per second.

### Metric types mapping for different runtimes:
| Metric name | Data Source | Supported Runtime type |
|-------------|----------------------| ------------------- |
| *Heap* |   Auto-Scaling data collector    | Liberty for Java , Node.js SDK |
| *Throughput* |  Auto-Scaling data collector| Liberty for Java , Node.js SDK, Swift (with Kitura) |
| *Response time* |   Auto-Scaling data collector | Liberty for Java , Swift (with Kitura)|
| *Memory*   | Auto-Scaling data collector   |  Liberty for Java , Node.js SDK, Swift (with Kitura)  |
| *Memory*   | Cloud Foundry   |  Runtimes other than Liberty for Java , Node.js SDK and Swift (with Kitura) |

{: caption="Table 2. Supported metric types" caption-side="top"}

*Note::* 
* To collect Response time/Throughput metrics data on Liberty for Java, your application must be deployed as Liberty web application so that measuring HTTP/HTTPS requests will be processed via Liberty web container.<br>
For example, if you run a Spring Boot application as a "Main-Classs" app, the Liberty buildpack only provides java environment for you, and the app actually runs in the Spring embedded Tomcat container, thus no metrics data will be collected by the Auto-Scaling service. You must run your app as a Liberty WAR in order to work with Auto-Scaling service.<br/> 
* For Swift application, only Kitura framework is supported for {{site.data.keyword.autoscaling}}.<br/> 

## Error messages
{: #err_msg}
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

* [Scaling containers](https://www.{DomainName}/docs/containers/container_ha.html#container_ha){:new_window}
* [Scaling virtual servers](https://www.{DomainName}/docs/virtualmachines/vm_index.html#vm_manage_instances){:new_window}
* [{{site.data.keyword.autoscaling}} CLI](../../cli/plugins/auto-scaling/index.html){:new_window}
* [{{site.data.keyword.autoscaling}} agent for Node.js](https://www.npmjs.com/package/bluemix-autoscaling-agent){:new_window}
* [Swift Application Metrics](https://github.com/RuntimeTools/SwiftMetrics){:new_window}
